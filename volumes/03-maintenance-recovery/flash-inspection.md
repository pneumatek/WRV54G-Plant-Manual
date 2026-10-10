# Flash Inspection and Preservation

## 1. Purpose

This procedure documents the known flash layout of the Linksys WRV54G and establishes the requirements for acquiring a complete, verifiable flash backup.

**Current objective:** Preserve the complete 8 MiB flash address space before attempting firmware recovery or modification.

**Current restriction:** No flash-writing, erasing, configuration-changing, or firmware-loading operations are authorized by this investigation.

## 2. Known Flash Geometry

The RGLoader `flash_layout` command reported seven sections spanning the address range `0x00000000` through `0x007FFFFF`.

| Section | Type | Start address | End address (exclusive) |
|---:|---|---:|---:|
| 00 | BOOT | `0x00000000` | `0x0013F000` |
| 01 | FACTORY | `0x0013F000` | `0x00140000` |
| 02 | IMAGE | `0x00140000` | `0x006C0000` |
| 03 | FLASH_SECT_BOOTCONF | `0x006C0000` | `0x006E0000` |
| 04 | Unknown section type | `0x006E0000` | `0x00700000` |
| 05 | FLASH_SECT_CONF | `0x00700000` | `0x00780000` |
| 06 | FLASH_SECT_CONF | `0x00780000` | `0x00800000` |

Total address-space size:

- Hexadecimal: `0x00800000` bytes
- Decimal: 8,388,608 bytes
- Equivalent: 8 MiB

The end address is exclusive. The final byte address is `0x007FFFFF`.

**Important:** Section boundaries and reported section contents are different observations. Section 02 was reported as `Uninitialized` by `flash_layout`, although a bounded raw dump of that region contained nonblank data. The meaning of that status remains unresolved.

## 3. Existing Evidence

The following evidence was collected during the October 9, 2026 session.

| Evidence | Location or reference |
|---|---|
| Original PuTTY session log | `D:\WRV54G-Plant-Manual-Evidence\WRV54G-2026-10-09-session-114730.log` |
| Session-log size | 5,290 bytes |
| Session-log SHA-256 | `5a48763deeb752a692c1db429b195cf0658e633879cda8af44902b6d12e7e208` |
| Flash layout transcription | `evidence/console-transcripts/2026-10-09-flash-layout.txt` |
| Image-region sample transcription | `evidence/console-transcripts/2026-10-09-image-region-sample.txt` |
| Baseline engineering record | `volumes/05-engineering-records/lab-log/2026-10-09-project-baseline.md` |

The original PuTTY log is the primary evidence for the captured console output. The repository text files are transcriptions and should be compared with the original log when exact byte values or command output matter.

The captured session is partial; it does not constitute a complete startup transcript.

## 4. Observed Dump Behavior

### 4.1 Bounded image-region sample

The command below was used to inspect 512 bytes beginning at the start of section 02:

`flash_dump -s 2 -l 0x200`

The output began at address `0x00140000` and contained nonblank data, including the byte sequence:

`fe ed ba be`

The sample also contained an ASCII-readable date-like string and data resembling machine instructions. These observations do not establish that the image is complete, valid, or bootable.

### 4.2 Unbounded default invocation

During the same session, invoking `flash_dump` without arguments displayed data beginning at address `0x00000000`. The captured output covered the first 256 bytes, followed by `Returned 0` and `data_error`.

The cause and significance of `data_error` remain unknown. The capture does not establish whether the command attempted to read more data or encountered another condition.

Do not repeat the unbounded invocation when a controlled, limited output is intended.

## 5. Additional Acquisition Lead

The OpenRG Programmer's Guide, Version 5.5, documents a flash-dump command with options to specify a starting section or address, a length in bytes, and an output width.

A separate OpenWrt utility named `jungo-image.py` documents a flash-dump workflow for Jungo-based routers, explicitly including the WRV54G. The utility obtains flash data through a Telnet CLI session and reconstructs binary output from bounded `flash_dump` responses.

References:

- OpenRG Programmer's Guide, Version 5.5, Chapter 6, *Board Tailoring*.
- OpenRG Programmer's Guide, Version 5.5, Section 27.2.14, *flash*.
- OpenWrt source: `scripts/flashing/jungo-image.py` — https://git.openwrt.org/openwrt/openwrt/tree/scripts/flashing/jungo-image.py

**Applicability limitation:** The documented utility expects a working router CLI reachable over Telnet. The WRV54G currently under investigation is being accessed through its serial bootloader prompt, `OpenRG boot>`. Compatibility with this bootloader session has not been established. Do not run the utility against this router until its connection requirements and expected target state have been reviewed.

## 6. Requirements for a Complete Backup

A candidate raw flash image must satisfy all of the following before it is accepted as a preservation artifact:

1. It contains exactly 8,388,608 bytes, unless further evidence establishes a different physical flash size.
2. Its acquisition method and target state are documented.
3. The acquired data covers the entire address range from `0x00000000` through `0x007FFFFF` without gaps or duplicated ranges.
4. The capture process reports no unexplained address discontinuities, timeouts, or parsing errors.
5. A SHA-256 checksum is recorded.
6. The image is retained as an untouched master copy. Analysis is performed on a separate working copy.
7. The backup is not described as verified solely because a file exists or has the expected length. Verification must also account for acquisition errors and missing or misordered data.

## 7. Outstanding Questions

- Can the current RGLoader session export bounded flash reads reliably over the serial console?
- Does the bootloader provide a read-only transfer mechanism that can preserve binary bytes without text-conversion errors?
- Is the `jungo-image.py` workflow usable only after a successful OpenRG boot, or is another compatible CLI available?
- Why did the reported metadata for section 03 differ between earlier notes and the October 9 capture?
- What condition produced `data_error` after the unbounded `flash_dump` invocation?

These questions remain open. No answer should be inferred without additional evidence.

## 8. Acceptance Status

**Status: Investigation in progress — complete flash backup not yet acquired or verified.**

The next action is to select and test a bounded, read-only acquisition method on a small range before attempting a full flash capture. No destructive recovery procedure should begin until a complete backup has been acquired, checked, and preserved.
