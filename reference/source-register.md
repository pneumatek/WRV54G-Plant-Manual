# Source Register

**Project:** WRV54G Plant Manual & OpenRG Atlas  
**Status:** Initial reference inventory  
**Last updated:** 2026-10-10

## 1. Purpose

This register identifies external documentation and primary evidence used in the investigation of the Linksys WRV54G and its OpenRG software environment.

Sources must be distinguished by type:

- **Reference documentation:** Published manuals and guides describing OpenRG or related software.
- **Primary evidence:** Direct console captures, measurements, photographs, and observations from the investigated hardware.
- **Engineering interpretation:** Conclusions derived by comparing references with primary evidence.

General OpenRG documentation does not, by itself, establish that a feature or procedure applies to this particular router.

## 2. OpenRG reference library

The following documents are held in the local evidence directory:

`D:\WRV54G-Plant-Manual-Evidence\Reference`

| Local filename | Size (bytes) | Initial research focus |
|---|---:|---|
| `211152344-Openrg-Programmer-Guide-5-5-LATEST.pdf` | 4,929,712 | OpenRG software architecture and programmer interfaces |
| `221572666-Openrg-User-Manual.pdf` | 14,139,486 | General system operation and user-facing configuration |
| `227900734-openrg-user-manual-advanced-ver-5-3-pdf.pdf` | 18,841,962 | Advanced configuration and system features |
| `88752930-OpenRG-Configuration-Guide.pdf` | 4,463,648 | Configuration structure and configuration-management concepts |

These research-focus descriptions are preliminary and must be refined after inspecting the documents.

The filenames suggest different editions or audiences. Exact publication dates, revisions, authorship, and applicability to the WRV54G remain to be established.

## 3. Primary console evidence

Session logs are retained locally under:

`D:\WRV54G-Plant-Manual-Evidence`

| Filename | Size (bytes) | Current status |
|---|---:|---|
| `WRV54G-2026-10-09-session-114730.log` | 5,290 | Flash-layout and flash-inspection evidence previously transcribed |
| `WRV54G-2026-10-09-session-201218.log` | 2,034 | Contains bootloader `help` output |
| `WRV54G-2026-10-09-session-202556.log` | 1,084 | Awaiting review |
| `WRV54G-2026-10-10-session-120207.log` | 432 | Awaiting review; associated with the October 10 console-access verification |

The original logs are evidence records. Transcriptions and analysis belong in the repository's appropriate evidence and engineering-record locations.

## 4. Preservation and provenance

- Preserve original evidence files without editing their contents.
- Record SHA-256 hashes to help verify file integrity.
- Record the capture date, hardware context, and relevant procedure when known.
- Clearly distinguish direct observations from interpretations.
- Do not assume a command documented for a general OpenRG release is safe or supported on this router.
- Do not publish credentials or sensitive configuration data.
- Keep complete third-party PDFs in the local reference library unless redistribution rights have been established. Record their metadata and findings in this repository rather than committing the full documents.

## 5. OpenWrt `jungo-image.py` — Flash Acquisition Reference

- **Source:** [Historical OpenWrt `jungo-image.py`](https://git.wut.ee/qi-hardware/openwrt-xburst/src/commit/65302aa5bc4cebf0a8cbde4cf65418b82ddeb7bf/scripts/flashing/jungo-image.py)
- **Version:** 0.11
- **Purpose:** Reference implementation for flash acquisition from supported Jungo-based routers, explicitly including the Linksys WRV54G.
- **Relevant functionality:** The `image_dump()` routine reads flash in bounded chunks through a Telnet CLI, parses address-prefixed hexadecimal output, and reconstructs binary data.
- **Applicability:** Not yet validated on the WRV54G under investigation. The utility expects a running router CLI; compatibility with the serial `OpenRG boot>` prompt has not been established.
- **Safety limitation:** The script also contains firmware-writing functionality. Do not execute it against the router until its execution paths, connection requirements, and flash-size detection have been reviewed.
- **Status:** Research reference only; acquisition procedure not yet validated.


## 6. Next research priorities

1. Inspect the bootloader command documentation and identify any supported read-only flash-export method.
2. Investigate OpenRG configuration structure and the observed `rg_conf` sections.
3. Compare documented boot and recovery mechanisms with the WRV54G's observed RGLoader behavior.
4. Record version differences and unresolved applicability questions before relying on a procedure.
