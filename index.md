# WRV54G Plant Manual & OpenRG Atlas
## Master Index

**Project:** Linksys WRV54G Wireless-G VPN Broadband Router  
**Document Type:** Master Index  
**Status:** Initial structure established  
**Last Updated:** 2026-10-09

---

## 1. Purpose

This index is the primary navigation page for the WRV54G Plant Manual & OpenRG Atlas.

It organizes the technical manual, system atlas, engineering records, supporting references, and original evidence produced during the investigation and restoration of the router.

The index will evolve as the investigation progresses. Chapters may be listed before they are complete so that the intended organization remains visible.

## 2. Volume I — Plant Description & System Fundamentals

**Purpose:** Describe the plant and establish an understanding of its hardware and software.

- [Plant Overview](volumes/01-plant-description/overview.md)
- [Hardware Description](volumes/01-plant-description/hardware.md)
- [Software Architecture](volumes/01-plant-description/software-architecture.md)

## 3. Volume II — Operations & Normal Behavior

**Purpose:** Document how to access, start, observe, and operate the system.

- [Startup Sequence](volumes/02-operations/startup-sequence.md)
- [Serial Console](volumes/02-operations/serial-console.md)
- [Normal Operation](volumes/02-operations/normal-operation.md)

## 4. Volume III — Maintenance & Recovery

**Purpose:** Establish safe, reproducible methods for preservation, inspection, troubleshooting, and recovery.

- [Backup & Preservation](volumes/03-maintenance-recovery/backup-and-preservation.md)
- [Flash Inspection](volumes/03-maintenance-recovery/flash-inspection.md)
- [Recovery Procedures](volumes/03-maintenance-recovery/recovery-procedures.md)

## 5. Volume IV — OpenRG Atlas & System Internals

**Purpose:** Map the physical and logical relationships that explain how the system works.

- [System Map](volumes/04-openrg-atlas/system-map.md)
- [Boot Flow](volumes/04-openrg-atlas/boot-flow.md)
- [Flash Map](volumes/04-openrg-atlas/flash-map.md)
- [Command Map](volumes/04-openrg-atlas/command-map.md)

## 6. Volume V — Engineering Records & Lessons Learned

**Purpose:** Preserve the history of the investigation and distinguish experimental observations from verified knowledge.

### Laboratory Log

Chronological entries describing activities, initial conditions, procedures, observations, and results.

Location: `volumes/05-engineering-records/lab-log/`

### Experiments

Controlled investigations with stated objectives, methods, results, and conclusions.

Location: `volumes/05-engineering-records/experiments/`

### Fault Reports

Descriptions of abnormal behavior, supporting evidence, diagnostic work, and confirmed or suspected causes.

Location: `volumes/05-engineering-records/fault-reports/`

### Lessons Learned

Durable knowledge derived from experience, including successful techniques, mistakes to avoid, and changes to our understanding.

Location: `volumes/05-engineering-records/lessons-learned/`

## 7. Reference Library

Supporting information used throughout the project.

- [Command Reference](reference/command-reference.md)
- [Glossary](reference/glossary.md)
- [Source Register](reference/source-register.md)

## 8. Diagrams

System diagrams, flowcharts, and other visual representations.

Location: `diagrams/`

## 9. Evidence Archive

Original records and artifacts supporting the investigation.

- Console transcripts: `evidence/console-transcripts/`
- Measurements: `evidence/measurements/`
- Image analysis: `evidence/image-analysis/`

Large binary artifacts, including complete flash backups, may be stored separately. Their locations, sizes, acquisition methods, and verification status should be documented.

## 10. Documentation Rules

1. Record what happened in the Engineering Log.
2. Preserve original output and measurements in the Evidence Archive.
3. Document verified operating procedures in the appropriate Plant Manual chapter.
4. Document physical and logical relationships in the Atlas.
5. Maintain reusable command explanations, terminology, and source citations in the Reference Library.
6. Mark hypotheses as hypotheses until supported by evidence.
7. Update this index when documents are created, renamed, or reorganized.
8. Do not describe an unverified procedure as a proven recovery method.

## 11. Current Investigation Status

The WRV54G has been accessed through its serial interface, and an interactive `OpenRG boot>` prompt has been obtained.

Initial observations include RGLoader version 2.4.4, internal version 1.2, and a flash layout reporting seven sections across an 8 MiB address space.

The reported state of the image section does not yet establish whether the firmware is complete, valid, or bootable. The cause of the startup failure remains undetermined.

**Next technical objective:** Establish and verify a complete flash backup before conducting deeper firmware analysis or attempting any operation that could modify flash.

---

*This index is maintained as the project develops. Its structure provides the map; the investigation supplies the knowledge.*
