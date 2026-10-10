# Bounded Flash Read Test — 2026-10-10

## Purpose

Verify that the WRV54G RGLoader accepts explicit-address, length-limited flash reads through the J10 serial console.

## Test Conditions

- Interface: J10 serial console
- Console: PuTTY
- Bootloader prompt: `OpenRG boot>`
- Flash-read command: `flash_dump -r <address> -l <length>`
- Requested length per read: `0x40` bytes (64 bytes)

## Results

| Read | Start address | End address (inclusive) | Requested bytes | Result |
|---:|---:|---:|---:|---|
| 1 | `0x00140000` | `0x0014003F` | 64 | `Returned 0` |
| 2 | `0x00140040` | `0x0014007F` | 64 | `Returned 0` |
| 3 | `0x00140080` | `0x001400BF` | 64 | `Returned 0` |
| 4 | `0x001400C0` | `0x001400FF` | 64 | `Returned 0` |

Total requested data: 256 bytes (`0x100` bytes).

## Observations

- All four commands completed and returned `0`.
- The reported addresses are contiguous, with no gaps or overlaps.
- The first block contains the byte signature `FE ED BA BE` at address `0x00140000`.
- The second block contained only zero bytes.
- The third and fourth blocks contained both zero and nonzero bytes.
- Some nonzero byte sequences are consistent with ARM instruction encodings. No formal disassembly or image validation has been performed.

## Limitations

This test verifies bounded reads over a small address range only. It does not establish that a complete flash image can be acquired without errors, that all output can be captured reliably, or that the reconstructed image would be bootable.

## Status

**Passed:** Small, consecutive, bounded flash reads through the serial bootloader.

**Not yet tested:** Larger read lengths, complete flash acquisition, binary reconstruction, and independent image verification.

## Larger Read-Size Tests

Following the initial four consecutive 64-byte reads, larger bounded reads were tested from address `0x00140000`.

| Requested length | Expected final data-line address | Result |
|---:|---:|---|
| `0x100` (256 bytes) | `0x001400F0` | Passed; output matched the four 64-byte reads |
| `0x400` (1 KiB) | `0x001403F0` | Passed |
| `0x1000` (4 KiB) | `0x00140FF0` | Passed; no errors or missing address ranges reported |
| `0x4000` (16 KiB) | `0x00143FF0` | Passed; no errors or missing address ranges reported |

All tests used the read-only command form:

`flash_dump -r <address> -l <length>`

The successful tests establish that the bootloader returned the expected address coverage for these requested lengths. They do not establish the maximum supported read size or verify a complete flash image.

**Status:** Largest tested bounded read is 16 KiB. Full-flash acquisition and binary-image verification remain outstanding.
