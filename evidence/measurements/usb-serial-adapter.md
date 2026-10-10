# USB-to-Serial Adapter — Equipment Record

**Project:** WRV54G Plant Manual & OpenRG Atlas  
**Equipment category:** Serial communications / laboratory interface  
**Record status:** Initial identification and operational verification  
**Last updated:** 2026-10-10

## 1. Identification

- **Device:** AITRIP FT232RL Mini USB-to-TTL serial adapter
- **Interface IC:** FTDI FT232RL
- **Application:** Serial-console access to the Linksys WRV54G router
- **Host environment:** Windows 11
- **Terminal application:** PuTTY

## 2. Electrical interface

The WRV54G serial console uses 3.3 V TTL signaling. This is not an RS-232 interface.

Previously recorded observations:

- Adapter voltage selection: 3.3 V
- Measured adapter supply output: approximately 3.13 V
- Router TX idle voltage: approximately 3.29–3.30 V
- Router RX measurement: approximately 0.25 V
- Common ground established between adapter and router

**Connection precautions**

- Connect router TX to adapter RX.
- Connect adapter TX to router RX only with the adapter configured for compatible 3.3 V logic.
- Connect ground between the two devices.
- Do not connect adapter VCC to the router.
- Do not connect a 5 V TTL signal directly to the router's serial RX input.
- Do not confuse TTL serial signaling with bipolar-voltage RS-232.

## 3. PuTTY configuration

Previously established settings:

- Speed: 115200 baud
- Data bits: 8
- Stop bits: 1
- Parity: None
- Flow control: None

## 4. Operational verification — 2026-10-10

The operator cycled power to the USB-to-serial adapter and the WRV54G router, then verified the serial-console procedure.

Observed results reported by the operator:

- PuTTY communication was restored successfully.
- The operator repeatedly entered BOOT MENU mode by pressing ESC at the appropriate point in startup.
- No BOOT MENU entry attempts were missed during this verification.

This establishes repeatable operational access under the tested conditions. It does not independently verify every electrical characteristic of the adapter.

## 5. Evidence and open items

The operator has captured the bootloader `help` output in the local evidence directory:

`D:\WRV54G-Plant-Manual-Evidence\Reference`

Record the exact capture filename and, when practical, its SHA-256 hash in the session evidence manifest.

Items still to establish:

- Photograph of the adapter and its voltage-selection markings
- Exact Windows COM port used
- Whether the adapter's selected logic voltage has been independently measured at its TX output
- Exact filename and integrity hash of the bootloader help capture

## 6. Safety classification

**Use:** Serial-console observation and control.

The adapter is not permission to perform destructive bootloader operations. Commands that erase flash, burn images, or modify persistent configuration remain restricted until a verified backup and recovery procedure are available.
