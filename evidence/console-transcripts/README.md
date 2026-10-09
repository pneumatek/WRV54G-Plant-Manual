# Console Transcript Archive

## Purpose

This directory preserves console output collected during the WRV54G Plant Manual & OpenRG Atlas investigation.

Console transcripts provide primary evidence of system behavior. They support the Engineering Log, operating procedures, fault reports, and Atlas diagrams.

## Recording Principles

1. Preserve original captured output whenever possible.
2. Record the date, system under test, interface, terminal settings, and activity associated with each capture.
3. Distinguish complete transcripts from excerpts.
4. Do not silently correct, reformat, or remove unexpected output from an original transcript.
5. Store interpretation and analysis in separate documentation.
6. Redact passwords, private credentials, and other sensitive information before publishing.
7. Never claim that a transcript is complete if only a portion of the session was captured.

## Naming Convention

Use descriptive filenames beginning with the date:

`YYYY-MM-DD-subsystem-or-activity.txt`

Examples:

- `2026-10-09-bootloader-session.txt`
- `2026-10-09-flash-layout.txt`
- `2026-10-09-flash-dump-header.txt`

Use the actual capture date when known. If an earlier transcript is recovered later, distinguish the capture date from the date it was archived.

## Capture Metadata

When available, document:

- Capture date and time, including timezone
- Router identification
- Connection and terminal settings
- Command or action that produced the output
- Whether the capture is complete or partial
- Any redactions or transformations
- Related Engineering Log entry

## Evidence Integrity

For important evidence files, record a SHA-256 hash where practical. A hash can help detect subsequent changes to a file, but it does not independently prove when the file was created or whether the original capture was accurate.

Large or sensitive evidence files may be stored outside this repository. In that case, document their storage location, size, hash, and verification status without exposing credentials or private information.

## Initial Archive Status

The investigation has established interactive access to the WRV54G bootloader and has recorded observations of the flash layout.

The availability of original, complete transcript files for these earlier sessions has not yet been established.

**Next action:** Locate existing console captures and preserve original files where available. Do not label reconstructed output as an original transcript.

---

*Original evidence supports the investigation; analysis explains what the evidence may mean.*
