# WRV54G Bootloader Command Reference

**Project:** WRV54G Plant Manual & OpenRG Atlas  
**Subsystem:** RGLoader / OpenRG bootloader  
**Status:** Initial command inventory  
**Last Updated:** 2026-10-09

---

## 1. Purpose

This reference records commands exposed by the WRV54G's interactive `OpenRG boot>` console.

It is intended to help investigators understand command syntax, identify read-only operations, and recognize commands that may alter persistent state.

Command descriptions below are based on the console's reported help text and observations made during the investigation. They should not be treated as a complete specification of internal behavior.

## 2. Access

The interactive prompt observed during the investigation is:

```text
OpenRG boot>
```

The bootloader has reported:

- RGLoader Version: 2.4.4
- Internal Version: 1.2

## 3. Reported Command Inventory

The following commands appeared in the bootloader's `help` output.

| Command | Reported purpose | Initial classification |
|---|---|---|
| `ps` | Print main-task tasks | Inspection |
| `rg_conf_print` | Print configuration starting from a specified root | Read-only inspection |
| `rg_conf_set` | Set a configuration path and value | State-changing |
| `rg_conf_del` | Delete a configuration subtree | State-changing |
| `reconf` | Reconfigure the system according to current configuration | Potentially state-changing |
| `entity_close` | Close an entity by pointer | Not yet assessed |
| `host` | Resolve a hostname | Network inspection |
| `rmt_upd_rgloader` | Remotely upgrade the box | Potentially destructive |
| `rmt_upd_rgloader_wget_close` | Kill a remote upgrade process | Potentially disruptive |
| `flash_commit` | Save configuration to flash | Persistent write |
| `restore_default` | Restore defaults; `-d` avoids rebooting afterward | State-changing |
| `log_lev_on` | Redirect error output at or above a specified severity to the CLI | Diagnostic |
| `log_lev_off` | Stop error-output redirection | Diagnostic |
| `cat` | Print file contents on the console | Read-only inspection |
| `shell` | Spawn a BusyBox shell in the foreground | Not yet assessed |
| `flash_layout` | Print flash layout and contents metadata | Read-only inspection |
| `flash_erase` | Erase a specified flash section; `-d` is an optional flag | Destructive |
| `flash_dump` | Dump flash data by section or address | Read-only inspection |
| `bset` | Configure bootloader settings | Potentially state-changing |
| `ifconfig` | Configure a network interface | Potentially state-changing |
| `ping` | Test network connectivity | Network test |
| `boot` | Boot the system, optionally with kernel debugging | Operational |
| `load` | Load and burn an image from a URL or selected address/section | Destructive or potentially destructive |
| `help` | Print the command menu | Read-only inspection |

These classifications are preliminary risk guidance, not a substitute for command-specific analysis.

## 4. Known Syntax

The help output reported the following syntax for selected commands.

### Configuration inspection

```text
rg_conf_print <root>
```

Prints configuration starting from the specified root.

### Configuration modification

```text
rg_conf_set <path> <value>
rg_conf_del <path>
```

These commands alter configuration and should not be used during initial read-only investigation.

### Flash inspection

`flash_layout`

The `flash_layout` command reports the flash sections and their metadata.

`flash_dump [-s <section> | -r <address>] [-l <length>] [-1|2|4]`

The `flash_dump` command supports selecting a section or an address, specifying a length, and choosing a display width.

**Observed behavior — Default invocation**

Invoking `flash_dump` without arguments displayed data beginning at address `0x00000000`. It did not print usage information. Avoid invoking it without arguments when a bounded output is intended.

**Additional observation — Console capture interruption**

During the 2026-10-09 session, the text `data_error` appeared after an attempt to copy console contents using Ctrl-C in PuTTY. The user reports that pressing Enter clears the line.

The cause of this text has not been established. It must not be treated as evidence of a flash-read failure or a router fault. Future console captures should use PuTTY's mouse-selection copy behavior or the session log file, avoiding Ctrl-C as a copy shortcut.

### Flash erasure

```text
flash_erase [-d] <section>
```

This command is destructive. Do not execute it during evidence collection.

### Image loading

```text
load -u <url> {-s <section> | -r <address>}
```

The help text describes loading and burning an image. Do not execute this command until the image format, destination, preservation requirements, and recovery procedure have been established.

### Boot operation

```text
boot -g {-s <section> | -r <address>}
```

The help text describes booting the system, with `-g` indicating kernel-debugging behavior. The exact behavior of each option has not yet been independently verified.

## 5. Preservation and Safety Rules

1. Prefer bounded, read-only commands during initial investigation.
2. Avoid commands that modify configuration, bootloader settings, or flash.
3. Do not infer the complete behavior of a command from its name alone.
4. Record the exact command and complete output for significant observations.
5. Verify a full flash backup and its integrity before attempting destructive recovery.
6. Do not publish passwords, credentials, or sensitive configuration values in this repository.

## 6. Open Questions

- What are the exact semantics of the `flash_dump` output-width options?
- Can the bootloader read the complete flash region in bounded chunks?
- Is there a safe method to transfer a raw flash image to a host computer?
- What are the exact effects of `bset`, `reconf`, and the remote-upgrade commands?
- Does the BusyBox shell provide additional read-only inspection tools?

These questions remain open until tested or supported by reliable technical documentation.

---

*This reference will be expanded as commands are investigated. Observed behavior and verified command semantics must remain distinguishable.*
