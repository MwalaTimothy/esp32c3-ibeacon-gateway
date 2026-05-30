# Tratoria BLE Gateway Firmware (RGB Ring Integration)

Firmware for an ESP32-C3 gateway that scans iBeacon traffic and reports detected minors to a KDS HTTP endpoint.

This README reflects the current implementation in `src/gateway_main.cpp`, including RGB ring behavior.

## Hardware and Platform
- Board: LOLIN C3 Mini (ESP32-C3)
- RGB ring: 12x NeoPixel on GPIO3
- Framework: Arduino (PlatformIO)
- Main dependencies:
  - NimBLE-Arduino
  - Adafruit NeoPixel
  - WiFi + HTTPClient

## RGB Ring Integration

The ring is used as the primary status indicator.

### LED States
- WiFi disconnected (normal runtime): calm red breathing with a faint warm chase
- Startup config window active: blue breathing base with sparse rainbow chase accents
- WiFi connected + beacons detected: green breathing status
- WiFi connected + no beacons detected: vivid rainbow breathing pattern
- Active BLE scan overlay: full-ring rainbow pattern while scan is active
- New beacon detected: short white flash (120 ms), then returns to current base state
- Ring off: when explicitly set off during transitions

### RGB Timing and Limits
- LED count: 12
- Brightness: 40 (global NeoPixel brightness)
- Config spinner step: 90 ms
- New beacon flash: 120 ms
- Event flash minimum: 60 ms
- Typical breathe periods: 2200-3000 ms depending on state

### Compact RGB State Table

| Condition | Ring behavior | Quick visual check |
|---|---|---|
| Config window (first 180 s) | Blue breathe + rainbow chase accents | Mostly blue ring with moving multicolor points |
| WiFi disconnected (runtime) | Red breathe + warm chase | Soft red glow, no hard blink |
| WiFi connected, no beacons | Vivid rainbow breathe | Full-ring rainbow that brightens/dims smoothly |
| WiFi connected, beacons present | Green breathe | Mostly green ring, smooth pulse |
| Scan active | Rainbow(10) full-ring overlay | Whole ring turns rainbow while scanning |
| New beacon detected | White flash (120 ms) | Fast white blink, then back to base state |

## Boot and Runtime Flow
1. Device boots and loads saved config from NVS.
2. BLE scan stack is initialized first.
3. A 180-second serial config window opens (blue breathing + accents).
4. During config window, you can provision WiFi/KDS/filters via serial commands.
5. WiFi credentials entered with `SET WIFI_SSID`, `SET WIFI_PASS`, or `AT+WIFI=...` are saved immediately to NVS and persist across reboot until `WIFI CLEAR` is used.
6. After window closes, saved WiFi credentials are tried automatically.
7. Runtime loop continuously:
   - scans BLE,
   - retries WiFi every 15 s if disconnected,
   - removes stale beacons,
   - reports at configured report interval.

## Beacon Detection Logic
- Expected manufacturer ID: `0x004C` (Apple iBeacon format)
- Valid iBeacon marker bytes required: `0x02 0x15`
- Major filter:
  - `0..65534`: match exact major
  - `65535`: wildcard (accept any major)
- Beacon timeout: beacon removed if not seen for 30 s
- Max tracked beacons: 100

## KDS Reporting
- Endpoint: `http://<KDS_IP>:<KDS_PORT>/beacons`
- Default report interval: 10000 ms
- If WiFi is down, reports are printed to serial only.

Example payload:

```json
{
  "gateway_id": "gateway-001",
  "major": 1,
  "minors_detected": [11, 14],
  "rssi": [-63, -70],
  "timestamp": "2026-05-15T10:20:30Z"
}
```

## Build and Flash (PlatformIO)
Environment in `platformio.ini`:
- `env:lolin_c3_mini_gateway`

Typical steps:
1. Build firmware.
2. Upload to board.
3. Open serial monitor at `115200` baud.

## Serial Commands

### Core
- `HELP`
- `CONFIG`
- `SAVE`

### WiFi
- `WIFI SCAN`
- `WIFI STATUS`
- `WIFI CONNECT`
- `WIFI DISCONNECT`
- `WIFI CLEAR` - erase saved WiFi credentials from NVS
- `SET WIFI_SSID <ssid>` - set SSID and save immediately
- `SET WIFI_PASS <password>` - set password and save immediately
- `AT+WIFI=<ssid>,<password>` - save credentials immediately and connect

### BLE and Beacons
- `BLE DEBUG ON`
- `BLE DEBUG OFF`
- `BEACONS`
- `CLEAR BEACONS`
- `SET UUID <uuid>`
- `SET MAJOR <0..65535>`

### Gateway and KDS
- `SET GW_ID <id>`
- `SET KDS_IP <ip>`
- `SET KDS_PORT <1..65535>`
- `SET SCAN_MS <100..60000>`
- `SET REPORT_MS <1000..600000>`

## Quick Validation Checklist
1. On boot, confirm blue breathing with rainbow accents during the 180 s config window.
2. Set WiFi, reboot if needed, and confirm credentials persist.
3. Confirm vivid rainbow breathing when WiFi is connected and no beacons are tracked.
4. Power beacon and confirm short white flash on new detection.
5. Confirm ring shifts to green breathing while beacon is tracked.
6. Confirm `NEW` beacon logs in serial.
7. Confirm POST traffic to `/beacons` when WiFi is connected.
8. Confirm stale beacon removal after ~30 s absence (ring returns to rainbow breathe if no beacons remain).

## Troubleshooting
- No white flash on beacon arrival:
  - Confirm beacon sends iBeacon with `0x004C` manufacturer ID.
  - Confirm major filter or set `SET MAJOR 65535` for wildcard test.
  - Enable `BLE DEBUG ON`.
- Ring stays red instead of reconnecting:
  - Check SSID/password and signal quality.
  - Use `WIFI STATUS` and `WIFI CONNECT`.
- No KDS updates:
  - Verify KDS IP/port and route `/beacons`.
  - Confirm gateway is connected and shows green breathing when beacons are present.

## Notes
- `src/gateway_config.h` contains legacy defines and is not the active runtime configuration source for this firmware path.
- Active runtime configuration is loaded/saved through Preferences (NVS) in `src/gateway_main.cpp`.
- This documentation update does not require any firmware code changes.
