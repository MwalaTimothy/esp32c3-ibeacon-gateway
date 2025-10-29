# Release v2.0.0 - Enhanced Restaurant Branding & Battery Optimization

## 🌟 What's New in v2.0.0

### Major Enhancements
- **🏪 Complete Restaurant Branding**: Device now advertises as "Carenuity Restaurant" for professional customer experience
- **🔋 Battery Life Optimization**: Smart 5-second LED indicators dramatically extend battery life
- **📡 Optimized Range**: Precisely tuned 2-meter BLE range perfect for table-level service
- **🌈 Professional RGB LEDs**: Accurate color management with Adafruit NeoPixel library

### Technical Improvements
- Enhanced BLE advertising intervals (160-320ms) for optimal smartphone compatibility
- Improved memory efficiency: 18.4% RAM usage, 70% Flash usage
- Stable WiFi and BLE coexistence without conflicts
- Comprehensive status indication system with automatic power saving

### User Experience
- **Plug & Play**: Ready-to-use merged binary files
- **No Passwords**: Simplified BLE access for customers
- **Visual Feedback**: Clear status colors for different operational states
- **Easy Setup**: ImprovWiFi integration for smartphone-based configuration

## 📱 BLE Configuration

- **Device Name**: "Carenuity Restaurant"
- **Range**: ~2 meters (optimized for table service)
- **Power**: -12dBm transmission power
- **Advertising**: 160-320ms intervals

## 🎨 LED Status Indicators

| Color | Status |
|-------|--------|
| 🟢 Green | WiFi Connected & BLE Active |
| 🔵 Blue | BLE Advertising (no WiFi) |
| 🟡 Yellow | WiFi Setup Mode |
| 🔴 Red | Error/Boot State |
| ⚫ Off | Power Saving (after 5 seconds) |

## 📋 Technical Specifications

- **MCU**: ESP32-C3 (160MHz RISC-V)
- **Memory**: 320KB RAM, 4MB Flash
- **Connectivity**: WiFi 802.11 b/g/n, Bluetooth 5.0 LE
- **Power**: USB-C 5V or 3.3V battery
- **Form Factor**: Lolin C3 Mini compatible

## 🚀 Installation

1. Download `carenuity-restaurant-ibeacon-v2.0.0.bin`
2. Flash using esptool: `esptool.py --chip esp32c3 --port COM_PORT write_flash 0x0 carenuity-restaurant-ibeacon-v2.0.0.bin`
3. Power on and configure WiFi via ImprovWiFi

## 📞 Support

For technical support:
- Open GitHub issue with device logs
- Include ESP32-C3 model and version information
- Provide serial console output for debugging

---

**Carenuity Restaurant Solutions** - Professional IoT for Hospitality Industry