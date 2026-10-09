# Plant Overview

**Plant:** Linksys WRV54G Wireless-G VPN Broadband Router  
**Project:** WRV54G Plant Manual & OpenRG Atlas  
**Document Type:** Plant Description  
**Status:** Initial baseline  
**Last Updated:** 2026-10-09

---

## 1. Purpose

This chapter establishes the identity, scope, and initial known condition of the WRV54G under investigation.

It provides a common starting point for the detailed hardware description, software analysis, operating procedures, and restoration work documented in the other volumes.

This is a baseline description, not a final diagnosis.

## 2. Plant Identification

| Property | Recorded information |
|---|---|
| Manufacturer / brand | Linksys |
| Model | WRV54G |
| Product type | Wireless-G VPN broadband router |
| FCC ID | Q87-WRV54G |
| Serial number | MEX004901967 |
| Manufacturing origin on label | Taiwan |
| Wireless band on label | 2.4 GHz |
| Hardware revision | Not yet established |
| Firmware identity | OpenRG environment observed; complete firmware identity not yet established |

The serial number and FCC ID identify the unit being investigated. They do not, by themselves, establish its complete hardware revision or firmware compatibility.

## 3. Project Objective

The objective is to restore the WRV54G to its intended operating condition while developing a detailed understanding of its hardware, firmware, boot process, configuration, network interfaces, and recovery mechanisms.

The project values both restoration and knowledge. A successful repair without an explanation is incomplete; a plausible explanation without supporting evidence is not a verified result.

## 4. Known System Characteristics

Initial investigation has established the following:

- A serial console is accessible through the board's J10 header.
- The console communicates at 115200 baud using 8-N-1 settings with no flow control.
- The console identifies RGLoader version 2.4.4 and internal version 1.2.
- An interactive `OpenRG boot>` prompt has been obtained.
- The bootloader provides commands for inspecting configuration, examining flash layout, dumping flash contents, and booting or loading images.
- The flash-layout command reports seven sections across an 8 MiB address space.
- The section labeled `IMAGE` is reported as uninitialized, although nonblank data is present in its raw flash region.

These observations establish useful points of entry for further investigation. They do not yet establish the integrity of the firmware or the cause of the startup failure.

## 5. Initial Condition and Limitations

The router has not yet been demonstrated to boot successfully into normal operating mode.

The root cause of the startup failure remains unknown. Possible explanations must remain hypotheses until supported by additional evidence.

The completeness and verification status of a full raw flash backup have not yet been established in this documentation.

A working Linksys WRT54G v8 is available as a separate comparison device. It is a different model and hardware platform; its firmware must not be assumed compatible with the WRV54G.

## 6. Preservation Requirements

Until the original state has been adequately documented:

1. Prefer read-only inspection.
2. Preserve factory information and existing configuration.
3. Do not erase flash, write firmware, or alter persistent configuration as an exploratory first step.
4. Establish and verify a complete flash backup before considering destructive recovery procedures.
5. Record command output and measurements that may be difficult to reproduce.
6. Distinguish confirmed facts from working hypotheses.

## 7. Open Questions

The following questions will guide subsequent investigation:

- What is the exact board and hardware revision?
- What are the verified meanings of the fields in the flash image header?
- Why does the flash-layout report mark the image section as uninitialized when raw data is present?
- Is the image complete and internally consistent?
- What conditions cause the observed startup failure?
- Can normal operation be restored without losing original factory information or configuration?

Questions will be closed only when the evidence supports a defensible answer.

## 8. Related Documentation

- [Hardware Description](hardware.md)
- [Software Architecture](software-architecture.md)
- [Startup Sequence](../02-operations/startup-sequence.md)
- [Backup & Preservation](../03-maintenance-recovery/backup-and-preservation.md)
- [System Map](../04-openrg-atlas/system-map.md)
- [Engineering Records](../05-engineering-records/)

---

*This chapter records the initial baseline. Revise it as verified facts change, and preserve the history of experiments in the Engineering Log.*
