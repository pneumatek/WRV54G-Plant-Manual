# WRV54G Plant Manual & OpenRG Atlas

**Project:** Linksys WRV54G Wireless-G VPN Broadband Router  
**Purpose:** Understand, document, restore, and improve a legacy networking system  
**Approach:** Observe → Understand → Document → Test → Verify → Improve

---

## 1. Mission

This project is a systematic investigation and restoration of the Linksys WRV54G Wireless-G VPN Broadband Router and its embedded OpenRG software environment.

The objective is not merely to make the router operate again. It is to understand the system as a whole: its hardware, firmware, boot process, configuration, interfaces, failure modes, and recovery mechanisms.

The result will be a living technical reference modeled in part on the organization and discipline of a Navy Reactor Plant Manual (RPM), complemented by an engineering atlas that maps the system's physical and logical structure.

The guiding ambition is to restore the WRV54G to its intended operating condition while developing the deepest practical understanding that the available evidence supports.

## 2. Project Philosophy

We will approach this system as engineers and cartographers entering unfamiliar territory.

Our work will follow these principles:

1. **Know the plant.** Identify the hardware, software, interfaces, and system boundaries.
2. **Establish normal.** Record known behavior and baseline measurements before attempting repairs.
3. **Preserve evidence.** Protect original firmware, factory information, configuration data, and experimental results.
4. **Separate fact from theory.** Label observations, interpretations, hypotheses, and verified conclusions distinctly.
5. **Change one thing at a time.** Make controlled changes only when the evidence and recovery plan justify them.
6. **Verify results.** Confirm outcomes rather than assuming a procedure worked.
7. **Maintain configuration control.** Record changes, preserve known-good states, and document recovery paths.
8. **Share understanding.** Convert successful investigations into clear, reproducible documentation.

**Operating rule:** No destructive operation until the existing state has been documented and an adequate recovery path has been verified.

## 3. Scope

The investigation includes:

- Hardware identification and architecture
- Serial console and bootloader operation
- OpenRG software architecture and system behavior
- Flash memory organization and firmware image analysis
- Configuration storage and factory information
- Network interfaces and normal operating behavior
- Fault analysis and recovery planning
- Restoration testing and final verification
- Historical documentation, source references, and lessons learned

All findings must remain specific to the WRV54G hardware under investigation unless compatibility with another platform has been demonstrated.

## 4. Manual Organization

The manual is organized into five volumes.

### Volume I — Plant Description & System Fundamentals

Describes what the system is, how its major components relate, and what is known about its hardware and software architecture.

### Volume II — Operations & Normal Behavior

Documents startup, the serial console, bootloader interaction, normal operation, and expected system responses.

### Volume III — Maintenance & Recovery

Contains preservation procedures, backup methods, inspection techniques, troubleshooting, and verified recovery procedures.

### Volume IV — OpenRG Atlas & System Internals

Maps the system's internal structure, including boot flow, flash layout, configuration storage, command relationships, and known fault paths.

### Volume V — Engineering Records & Lessons Learned

Preserves laboratory logs, experiments, fault reports, measurements, decisions, and conclusions arising from the investigation.

Supporting references, diagrams, source material, and evidence will be maintained alongside the volumes.

## 5. The Atlas

The atlas is the system's evolving map. It should help us answer not only *what is here?* but also *how are the parts connected, and how does information or control move through the system?*

Planned maps include:

- **Physical map:** Board components, connectors, interfaces, and test points
- **Boot map:** Reset, RGLoader, kernel loading, and operating-system startup
- **Memory map:** Flash sections, image regions, configuration areas, and factory data
- **Command map:** Available console commands, their functions, and their risks
- **Fault map:** Observed failures, supporting evidence, possible causes, and verified remedies

Maps will distinguish confirmed information from incomplete or hypothetical interpretations.

## 6. Risk Classification

Investigation activities will be classified according to their potential to alter or damage the system.

| Level | Classification | Examples |
|---|---|---|
| 0 | Observe | Read console output, record measurements |
| 1 | Analyze | Decode dumps, inspect image headers, compare evidence |
| 2 | Controlled test | Perform a bounded test with a documented recovery path |
| 3 | Plant modification | Change configuration, erase flash, or write firmware |

Higher-risk activities require stronger evidence, a verified backup where applicable, and a documented recovery plan.

This classification guides the investigation; it does not replace technical judgment or specific safety precautions.

## 7. Documentation Standards

Documentation should be concise, reproducible, and grounded in evidence.

Each significant investigation should record:

- Date and project activity
- Subsystem under investigation
- Objective
- Equipment, software, and relevant settings
- Initial conditions
- Procedure and commands used
- Observations and measurements
- Results and interpretation
- Unexpected behavior or anomalies
- Risks, limitations, and unresolved questions
- Next steps

Console transcripts, photographs, measurements, and raw data should be preserved as evidence where practical.

Sensitive information, including passwords and private credentials, must not be published in the repository.

## 8. Evidence and Configuration Control

Original evidence should be preserved separately from interpretations and derived artifacts.

Firmware images, flash dumps, configuration captures, and other important data should have documented acquisition details, file sizes, and cryptographic hashes where practical.

Raw backups should be stored outside the ordinary documentation structure when their size or sensitivity makes that appropriate. The manual should record their location and verification status without requiring large binary files to be committed to GitHub.

No artifact should be described as a complete or verified backup until its completeness and integrity have been checked.

## 9. Current Project Status

**Status:** Initial investigation — interactive bootloader access established.

The router has been accessed through its serial console, and an interactive `OpenRG boot>` prompt has been obtained.

Initial observations include:

- RGLoader reports version 2.4.4.
- The reported internal version is 1.2.
- The console operates at 115200 baud, 8 data bits, no parity, one stop bit, with flow control disabled.
- The flash-layout command reports seven sections across an 8 MiB flash address space.
- The section labeled `IMAGE` is reported as uninitialized, although raw data in that region includes an apparent image signature and executable-looking bytes.

These are preliminary observations, not proof of firmware integrity or a diagnosis of the boot failure.

The root cause of the startup problem remains undetermined. Firmware recovery has not yet been demonstrated.

**Immediate priority:** Preserve the existing state, establish and verify a complete flash backup, and investigate the image structure without writing to or erasing flash.

## 10. Project Development

The manual will evolve through successive investigation cycles:

**Observe → Record → Interpret → Document → Test → Verify → Revise**

Each cycle should improve both our understanding of the plant and the quality of its documentation.

Established knowledge belongs in the manual. Events and experimental details belong in the engineering records. Unresolved questions remain visible until evidence supports a conclusion.

The goal is a reliable reference that another technically capable person could use to understand the system, reproduce our findings, and continue the work.

---

*This manual is a living engineering document. Its contents will be revised as evidence is collected, hypotheses are tested, and understanding improves.*

**Keep It Simple Student.**
