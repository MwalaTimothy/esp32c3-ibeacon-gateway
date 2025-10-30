# Release v1.0.0 - Initial Stable Release

## 🚀 First Release of ESP32-C3 iBeacon Gateway

### Core Features
- **📡 iBeacon Broadcasting**: Apple-compatible BLE beacon functionality
- **📶 WiFi Connectivity**: Integrated WiFi with ImprovWiFi setup
- **💡 LED Status**: Basic visual status indicators
- **🔧 ESP32-C3 Support**: Optimized for Lolin C3 Mini hardware

### Technical Foundation
- ESP32-C3 Lolin Mini board compatibility
- Arduino framework integration
- Basic BLE advertising parameters
- Standard GPIO LED control
- Initial memory optimization
- Core restaurant table identification system

### What's Included
- Standard iBeacon broadcasting capability
- Basic WiFi setup and connectivity
- Simple LED status indication
- ESP32-C3 hardware abstraction
- Fundamental BLE stack implementation

## Technical Specifications

- **MCU**: ESP32-C3 (160MHz RISC-V)
- **Memory**: 320KB RAM, 4MB Flash
- **Connectivity**: WiFi 802.11 b/g/n, Bluetooth 5.0 LE
- **Power**: USB-C 5V input
- **Form Factor**: Lolin C3 Mini

## Installation

1. Download `carenuity-restaurant-ibeacon-v1.0.0.bin`
2. Flash using esptool: `esptool.py --chip esp32c3 --port COM_PORT write_flash 0x0 carenuity-restaurant-ibeacon-v1.0.0.bin`
3. Power on device and configure as needed

## 🔄 Upgrade Path

This is the stable foundation release. For enhanced features including:
- Restaurant-specific branding
- Battery optimization
- Professional LED management
- Enhanced BLE compatibility

Please upgrade to v2.0.0 which includes significant improvements and restaurant-ready configurations.

## 📞 Support

For technical support:
- Create GitHub issue
- Provide device logs and configuration details
- Include ESP32-C3 hardware information

---

**Foundation Release for ESP32-C3 iBeacon Gateway System**
