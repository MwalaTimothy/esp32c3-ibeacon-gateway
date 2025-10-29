# Changelog

All notable changes to the Carenuity Restaurant iBeacon Gateway project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

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