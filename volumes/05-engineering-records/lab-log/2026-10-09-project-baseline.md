# Engineering Log — Project Baseline

**Project:** WRV54G Plant Manual & OpenRG Atlas  
**Date:** 2026-10-09  
**Activity:** Project organization and initial technical baseline  
**Subsystems:** Documentation, serial console, RGLoader, flash organization  
**Status:** Initial baseline recorded

---

## 1. Objective

Establish a documented starting point for the Linksys WRV54G restoration project and organize the investigation into a structured Plant Manual, Atlas, and Engineering Log.

The intent is to preserve observations, distinguish verified facts from hypotheses, and establish a disciplined process for future investigation.

## 2. Documentation Established

The GitHub repository now contains the initial project charter, master index, and plant overview.

| Artifact | Purpose | Status |
|---|---|---|
| `README.md` | Mission and governing principles | Created |
| `index.md` | Master navigation index | Created |
| `volumes/01-plant-description/overview.md` | Initial plant description and known condition | Created |

The repository structure defines five volumes:

1. Plant Description & System Fundamentals
2. Operations & Normal Behavior
3. Maintenance & Recovery
4. OpenRG Atlas & System Internals
5. Engineering Records & Lessons Learned

Supporting directories are designated for references, diagrams, and original evidence.

## 3. Previously Established Technical Observations

The following observations were established during earlier investigation and are recorded here as the initial technical baseline.

### 3.1 Serial Console

- The router's J10 header provides access to its serial console.
- The interface has been identified as 3.3 V TTL UART.
- Terminal settings: 115200 baud, 8 data bits, no parity, one stop bit, no flow control.
- PuTTY has been used successfully to communicate with the router.

### 3.2 Bootloader

The console has displayed:

```text
RGLoader Version: 2.4.4
Internal Version: 1.2
Press ESC to enter BOOT MENU mode.
Booting an active image in 0 seconds
Boot aborted
OpenRG boot>
```

An interactive `OpenRG boot>` prompt has been obtained.

The router has not yet been demonstrated to boot successfully into normal operating mode.

### 3.3 Flash Layout

The bootloader's `flash_layout` command reported seven sections across an 8 MiB address space.

The section labeled `IMAGE` occupies the address range `0x00140000–0x006C0000` and was reported as uninitialized.

A raw dump of that region nevertheless contains nonblank data, including the byte sequence `FE ED BA BE` at the start of the dumped region and executable-looking bytes farther into the data.

The meaning and integrity of the image contents have not yet been established.

## 4. Observed Anomalies

The router has exhibited startup failures, including an unhandled page fault reported by the OpenRG environment.

The reported program counter and link register have repeated across observations, while the reported bad address has varied.

These messages are evidence of abnormal behavior, but they do not establish a root cause.

The apparent disagreement between the flash-layout report and the raw image-region contents also requires further investigation.

## 5. Preservation Status

A complete, verified raw backup of the router's entire flash has not yet been established in this log.

Before any destructive recovery operation, the investigation must establish an adequate backup and recovery path.

Until then, the preferred activities are read-only inspection, measurement, documentation, and analysis.

No claim is made here that the firmware is complete, that the image is bootable, or that recovery has been achieved.

## 6. Next Actions

1. Establish whether a complete raw flash backup already exists.
2. If one does not exist, develop and verify a suitable acquisition procedure.
3. Preserve the relevant console transcripts and flash-inspection output.
4. Investigate the image header and section metadata without modifying flash.
5. Update the Plant Manual and Atlas as findings become sufficiently well supported.

## 7. Engineering Assessment

The investigation has established a useful point of entry: reliable access to an interactive bootloader console and commands capable of exposing configuration, flash layout, and raw flash contents.

The system's current startup failure remains unexplained. Firmware integrity and recoverability remain open questions.

The immediate priority is preservation of evidence, followed by controlled analysis.

---

*This entry records the baseline established by the investigation to date. Future entries will document subsequent activities, results, and changes in understanding.*
