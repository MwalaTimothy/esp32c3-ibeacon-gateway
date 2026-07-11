# ESP32-C3 iBeacon Gateway

![Version](https://img.shields.io/badge/version-2.2.0-blue.svg)
![Hardware](https://img.shields.io/badge/hardware-ESP32C3-orange.svg)
![Framework](https://img.shields.io/badge/framework-Arduino-brightgreen.svg)
![License](https://img.shields.io/badge/license-MIT-yellow.svg)
![Project Status](https://img.shields.io/badge/status-active-green.svg)
<img width="756" height="538" alt="RGB ring gateway" src="https://github.com/user-attachments/assets/025bf0ae-48f5-4e04-8a0f-01d3212ee27e" />

**Current release**: v2.2.0 (RGB Ring Integration) &nbsp;|&nbsp; **Target hardware**: ESP32-C3 (LOLIN C3 Mini) &nbsp;|&nbsp; **Author**: [MwalaTimothy](https://github.com/MwalaTimothy)

This repository distributes **pre-built firmware releases** for the ESP32-C3 iBeacon gateway. It does not contain firmware source code — each release is a ready-to-flash binary plus documentation for setup, provisioning, and integration. If you need to build custom firmware, get in touch (contact details below).

---

## What This Is

An always-on Bluetooth Low Energy gateway that:
- Continuously scans for Apple iBeacon advertisements from companion beacon devices
- Tracks detected beacons in real time (signal strength, seen-count, last-seen)
- Reports detections to your backend/KDS server over HTTP as JSON, on a configurable interval
- Falls back to serial-only reporting when WiFi or the backend is unavailable, rather than losing data silently
- Uses a 12-LED RGB ring as a live, at-a-glance status indicator
- Is provisioned entirely over USB serial — no source code or IDE required to configure a unit

**Typical use case:** tracking items or presence (trays, tags, visitors, staff) moving through a physical space using low-power iBeacon transmitters, with results delivered to a central server.

---

## Releases

| Version | Firmware Variant | Binary | Notes |
|---|---|---|---|
| **v2.2.0** | RGB Ring Integration (current) | [`esp32c3-ibeacon-gateway-v2.2.0.bin`](esp32c3-ibeacon-gateway-v2.2.0.bin) | Reliability/hardening release — see [CHANGELOG.md](CHANGELOG.md) |
| v2.0.0 | Carenuity Restaurant branding | [`carenuity-restaurant-ibeacon-v2.0.0.bin`](carenuity-restaurant-ibeacon-v2.0.0.bin) | Restaurant-branded variant |
| v1.0.0 | Carenuity Restaurant branding | [`carenuity-restaurant-ibeacon-v1.0.0.bin`](carenuity-restaurant-ibeacon-v1.0.0.bin) | Initial release |

Unless you specifically need the Carenuity-branded variant, use the latest `esp32c3-ibeacon-gateway-vX.Y.Z.bin`.

---

## Hardware Requirements

| Component | Notes |
|---|---|
| ESP32-C3 board | LOLIN C3 Mini recommended (160 MHz RISC-V, 4MB flash) |
| RGB LED ring | 12x addressable RGB LEDs (NeoPixel-compatible), wired to the board's status pin |
| USB-C cable | Power + serial provisioning/monitoring |
| WiFi network | 2.4 GHz (ESP32-C3 does not support 5 GHz) |
| Backend/KDS server | Any HTTP server that can accept a JSON POST (see payload spec below) |

---

## Flashing a Release

Releases are distributed as a single **merged binary** — bootloader, partition table, and application are already combined, so flashing is one command at a fixed offset. No PlatformIO, no Arduino IDE, no source required.

### 1. Install esptool

```
pip install esptool
```

### 2. Identify your serial port

- **Windows:** Device Manager → Ports (COM & LPT) → look for "USB Serial" / "CH340" / "CP210x"
- **macOS:** `ls /dev/tty.usbserial*` or `ls /dev/tty.SLAB*`
- **Linux:** `ls /dev/ttyUSB*` or `ls /dev/ttyACM*`

### 3. Flash the merged binary

```
esptool.py --chip esp32c3 --port <PORT> --baud 460800 write_flash -z 0x0 esp32c3-ibeacon-gateway-v2.2.0.bin
```

Replace `<PORT>` with your board's port (e.g. `COM5` on Windows, `/dev/ttyUSB0` on Linux/macOS).

### 4. Open a serial monitor

Any serial terminal at **115200 baud** works — Arduino IDE's Serial Monitor, PuTTY, Tera Term (Windows), or `screen /dev/ttyUSB0 115200` (macOS/Linux). Reset the board and confirm you see the boot banner and firmware version.

---

## First Boot & Provisioning

Every fresh boot opens a **180-second serial configuration window** (the RGB ring breathes blue during this time). Provisioning is done entirely with plain-text serial commands — no code, no recompiling.

```
> CONFIG
========== GATEWAY CONFIGURATION ==========
Firmware Version:  2.2.0
Gateway ID:        gateway-001
Beacon UUID:       8a46676d-6348-4d50-a0e6-af5a508def40
Target Major:      1
WiFi SSID:         <not set>
KDS Server:        192.168.1.100:8080
WiFi Status:       Disconnected
===========================================

> AT+WIFI=YourNetwork,YourPassword
[INFO] Connecting to WiFi: YourNetwork
[INFO] WiFi connected successfully
[INFO] IP Address: 192.168.1.50

> SET KDS_IP 192.168.1.100
> SET KDS_PORT 8080
> SET GW_ID kitchen-gate-1
> SAVE
[INFO] Configuration saved to NVRAM
```

All settings persist across power cycles and firmware updates. To re-provision a deployed unit, power-cycle it to reopen the 180-second window.

### Command Reference

| Category | Commands |
|---|---|
| Status | `HELP`, `CONFIG`, `SAVE` |
| WiFi | `WIFI SCAN`, `WIFI STATUS`, `WIFI CONNECT`, `WIFI DISCONNECT`, `WIFI CLEAR`, `SET WIFI_SSID <s>`, `SET WIFI_PASS <p>`, `AT+WIFI=<ssid>,<password>` |
| BLE / Beacons | `BLE DEBUG ON/OFF`, `BEACONS`, `CLEAR BEACONS`, `SET UUID <uuid>`, `SET MAJOR <0-65535>` |
| Gateway / Backend | `SET GW_ID <id>`, `SET KDS_IP <ip>`, `SET KDS_PORT <1-65535>`, `SET SCAN_MS <100-60000>`, `SET REPORT_MS <1000-600000>` |

`WIFI CONNECT` and `AT+WIFI=...` start connecting in the background — give it a few seconds, then check `WIFI STATUS` to confirm.

---

## RGB Ring Status Indicator

| Condition | Ring behavior |
|---|---|
| Configuration window (first 180s after boot) | Blue breathing + moving rainbow accents |
| WiFi disconnected (normal runtime) | Calm red breathing, no hard blink |
| WiFi connected, no beacons tracked | Vivid rainbow breathing |
| WiFi connected, beacon(s) tracked | Green breathing |
| Active BLE scan | Full-ring rainbow overlay |
| New beacon detected | Short white flash (~120ms), then returns to base state |

---

## Backend Integration

The gateway reports to your server via HTTP POST as JSON:

```
POST http://<KDS_IP>:<KDS_PORT>/beacons HTTP/1.1
Content-Type: application/json

{
  "gateway_id": "kitchen-gate-1",
  "major": 1,
  "minors_detected": [5, 12],
  "rssi": [-62, -74],
  "timestamp": "2026-04-25T10:30:00Z"
}
```

Your server should respond `200 OK` or `202 Accepted`. If WiFi or the backend is unreachable, the gateway keeps running and prints the same report to serial instead of dropping it — nothing is silently lost, and reporting resumes automatically once connectivity is restored.

- Default report interval: 10s (configurable, `SET REPORT_MS`)
- Default scan interval: 5s (configurable, `SET SCAN_MS`)
- Beacon timeout: a tracked beacon is dropped after ~30s of no detection
- Max tracked beacons per gateway: 100

---

## Troubleshooting

**Beacons not detected**
1. `BLE DEBUG ON` to see raw packet output
2. Confirm the beacon's UUID/Major match the gateway's (`CONFIG` to check, `SET UUID` / `SET MAJOR` to fix), or use `SET MAJOR 65535` to accept any major as a quick test
3. Bring the beacon within ~1m to rule out range issues

**WiFi won't connect**
1. `WIFI SCAN` — confirm your network shows up (ESP32-C3 requires 2.4 GHz)
2. Double-check SSID/password (case-sensitive)
3. `WIFI DISCONNECT` then `AT+WIFI=...` again

**WiFi connects but nothing reaches the backend**
1. `WIFI STATUS` to confirm connectivity and IP
2. Ping the KDS/backend host from another machine on the same network
3. Confirm `KDS_IP` / `KDS_PORT` via `CONFIG`, and that your server's `/beacons` route is listening and reachable through any firewall

**Unexpected reboot**
- Check the boot log line reporting the last reset reason. A watchdog-triggered reset means the firmware detected it had stalled and recovered automatically; a brownout reset usually points to an inadequate power supply for the board + LED ring under load.

---

## Security Considerations

- Provision only over a trusted USB/serial connection — the config window accepts plain-text commands from whoever is connected.
- WiFi credentials are stored on-device; use a WPA2/WPA3 network.
- Backend reporting is plain HTTP (no TLS) by default — restrict network access to the backend appropriately (firewall/VLAN) if it carries sensitive data, or place it behind a reverse proxy that terminates TLS.
- No authentication is enforced on the backend endpoint by the gateway itself; add authentication/allow-listing at the server or network layer if needed.

---

## Companion Projects

- [BLE-iBeacon](https://github.com/MwalaTimothy/BLE-iBeacon) — companion beacon transmitter firmware

## Support

- Issues/bugs: use this repository's GitHub Issues
- Email: mwalatimo@gmail.com
- GitHub: [github.com/MwalaTimothy](https://github.com/MwalaTimothy)

## License

MIT — see [LICENSE](LICENSE).

---

See [CHANGELOG.md](CHANGELOG.md) for release history and [Quickstart.txt](Quickstart.txt) for a step-by-step first-run walkthrough.
