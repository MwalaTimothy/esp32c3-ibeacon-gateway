# Changelog

All notable changes to the ESP32-C3 iBeacon Gateway firmware (including the Carenuity Restaurant-branded variant) will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [2.2.0] - 2026-07-11

Production-readiness and reliability release for the RGB Ring Integration firmware line. No configuration commands, NVS-stored settings, RGB ring states, or backend JSON payload format changed in this release — existing deployed units and integrations are unaffected by the upgrade.

### Reliability
- WiFi connect/reconnect and time sync no longer block the gateway: BLE scanning, the RGB ring, and the serial console all stay responsive while a connection attempt is in progress, instead of freezing for several seconds per attempt.
- Added automatic crash recovery: if the firmware ever detects it has stalled, it now reboots itself rather than requiring a manual power cycle.
- Boot log now reports the reason for the previous reset (normal power-on, watchdog recovery, brownout, etc.), making field diagnostics much easier.
- Backend reporting requests now time out instead of being able to stall the gateway indefinitely if the server is slow or unreachable.

### Hardening
- Serial-configured values (gateway ID, backend address, WiFi credentials) are now length-bounded and safely encoded before being sent to the backend, preventing malformed input from corrupting a report.
- Removed a legacy internal file that had a placeholder network credential embedded in it; it was never used by the running firmware but had no reason to exist in a shipped release.

### Build
- The build pipeline this release is compiled from is now version-pinned for reproducibility, and passes a clean compile with all compiler warnings enabled.

### Known limitations (unchanged from prior releases)
- No over-the-air (OTA) update mechanism; firmware updates require physical USB access.
- No TLS on backend reporting traffic (see README "Security Considerations").

## [2.0.0] - 2025-10-29

### Added
- Complete "Carenuity Restaurant" branding integration
- Professional RGB NeoPixel LED color management with Adafruit library
- 5-second LED timer for battery optimization
- Optimized 2-meter BLE transmission range (-12dBm power)
- Enhanced BLE advertising intervals (160-320ms) for better phone compatibility
- Comprehensive status color system (Green/Blue/Yellow/Red/Off)
- Automatic power saving mode after status indication period

### Changed
- Replaced GPIO digitalWrite LED control with proper NeoPixel library support
- Updated device name from generic to "Carenuity Restaurant"
- Optimized BLE power settings for table-level service range
- Improved memory efficiency (18.4% RAM, 70% Flash usage)
- Enhanced serial debugging output with detailed status messages

### Removed
- BLE password requirements for easier customer access
- Constant LED power drain replaced with smart timer system
- Generic device naming replaced with restaurant-specific branding

### Fixed
- BLE visibility issues with smartphones resolved through advertising optimization
- LED color accuracy improved with proper NeoPixel implementation
- Battery drain significantly reduced with intelligent power management
- BLE and WiFi coexistence stability enhanced

### Technical Details
- **MCU**: ESP32-C3 Lolin Mini (160MHz RISC-V)
- **Memory Usage**: 320KB RAM (18.4% used), 4MB Flash (70% used)
- **Libraries**: ImprovWiFi 0.1.0, Adafruit NeoPixel 1.15.2
- **Power Management**: 5-second active LED, automatic sleep optimization
- **BLE Range**: ~2 meters with -12dBm transmission power
- **Compatibility**: iOS and Android smartphone detection optimized

## [1.0.0] - 2025-10-29

### Added
- Initial ESP32-C3 iBeacon gateway implementation
- Basic BLE advertising functionality
- WiFi connectivity with ImprovWiFi integration
- Simple LED status indicators
- Core restaurant table identification system
- Standard ESP32 BLE stack integration

### Features
- Generic iBeacon broadcasting
- Basic WiFi setup capability
- Simple status LED functionality
- Core ESP32-C3 hardware support
- Standard power consumption profile

### Technical Foundation
- ESP32-C3 Lolin Mini board support
- Arduino framework integration
- Basic BLE advertising parameters
- Standard GPIO LED control
- Initial memory optimization