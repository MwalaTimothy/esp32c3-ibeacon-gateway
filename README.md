# ESP32-C3 iBeacon Gateway 

A professional ESP32-C3 based iBeacon gateway system designed specifically for restaurant environments. This device creates a Bluetooth Low Energy (BLE) beacon that customers can use to connect their smartphones to restaurant services.

##  Features

- **Restaurant-Ready**: Pre-configured for "Smart Restaurant" branding
- **Optimized Range**: 2-meter transmission range for table-specific service
- **Battery Efficient**: 5-second LED indicators to maximize battery life
- **Easy WiFi Setup**: ImprovWiFi for smartphone-based configuration
- **Visual Feedback**: RGB NeoPixel LED status indicators
- **Plug & Play**: Ready-to-use merged binary files

## Quick Installation

**Instant Setup**: Use our web-based solution builder at **[https://solutions.carenuity.com/](https://solutions.carenuity.com/)** for one-click installation and configuration!

## Manual Installation

### Hardware Required

- ESP32-C3 Lolin Mini development board
 <img width="501" height="321" alt="image" src="https://github.com/user-attachments/assets/6ff7fe2d-4df6-40b3-baa5-2b60f30fbbbf" />

-[Buy it](https://www.chipglobe.shop/en/p/carenuity-original-c3-mini-v2-2-1-esp32-c3-iot-development-board)
- Built-in NeoPixel RGB LED 
- USB-C cable for flashing

### Installation Steps

1. **Download Latest Binary**
   - Download `carenuity-restaurant-ibeacon-v2.0.0.bin` from [Releases](https://github.com/MwalaTimothy/esp32c3-ibeacon-gateway/releases)

2. **Flash to ESP32-C3**
   ```bash
   # Using esptool (install with: pip install esptool)
   esptool.py --chip esp32c3 --port COM_PORT write_flash 0x0 carenuity-restaurant-ibeacon-v2.0.0.bin
   ```
   Replace `COM_PORT` with your actual port (COM3, COM4, etc.)

3. **Setup WiFi**
   - Power on the device
   - Look for "Carenuity Restaurant" in your phone's WiFi settings
   - Follow ImprovWiFi setup prompts

4. **Table Configuration**

   **Via Web Interface:**
   1. Navigate to device IP address in browser
   2. Configure table number (1-999)
   3. Set server URL for ordering system
   4. Click "Save Configuration" - device restarts automatically

5. **Verify Operation**

   **Check iBeacon Broadcasting:**
   - UUID: `12345678-90AB-CDEF-1234-567890ABCDEF`
   - Major/Minor: Both set to your table number
   - Use beacon scanner app to verify detection

## 📱 BLE Configuration

- **Device Name**: "Carenuity Restaurant"
- **Range**: ~2 meters (optimized for table service)
- **Power**: -12dBm transmission power
- **Advertising**: 160-320ms intervals for optimal phone compatibility

## 🔋 Power Management

- **LED Behavior**: 5-second status indicators only
- **Sleep Mode**: Automatic power optimization
- **Battery Life**: Extended operation with efficient BLE advertising

## LED Status Indicators

| Color | Status |
|-------|--------|
| 🟢 Green | WiFi Connected & BLE Active |
| 🔵 Blue | BLE Advertising (no WiFi) |
| 🟡 Yellow | WiFi Setup Mode |
| 🔴 Red | Error/Boot State |
| ⚫ Off | Power Saving (after 5 seconds) |

## 🔧 Configuration Details

### iBeacon Settings

- **UUID**: `12345678-90AB-CDEF-1234-567890ABCDEF` (fixed)
- **Major**: Dynamically set to table number (1-999)
- **Minor**: Dynamically set to table number (1-999)
- **TX Power**: Optimized for table-level detection

### Web Interface Features

- **Dashboard**: Real-time status display with IP address
- **Table Number**: Configurable via web form (1-999)
- **Server URL**: Configurable endpoint for ordering system
- **Live Updates**: iBeacon data updates immediately when table number changes
- **Device Restart**: Safe restart after configuration changes

### Storage System

All settings are automatically saved to ESP32-C3 non-volatile storage:
- WiFi credentials (SSID/password)
- Table number
- Server URL for ordering system

## 📱 Integration Guide

### For Mobile App Developers

```javascript
// Example: Detecting table iBeacons
const tableUUID = "12345678-90AB-CDEF-1234-567890ABCDEF";

// Listen for beacon detection
function onBeaconDetected(beacon) {
    if (beacon.uuid === tableUUID) {
        const tableNumber = beacon.major; // or beacon.minor
        openOrderingInterface(tableNumber);
    }
}
```

### For Restaurant Systems

```http
# Configure device remotely
POST http://[device-ip]/config
Content-Type: application/x-www-form-urlencoded

table=15&server=https://yourrestaurant.com/order
```

## 📋 Technical Specifications

- **MCU**: ESP32-C3 (160MHz RISC-V)
- **Memory**: 320KB RAM, 4MB Flash
- **Connectivity**: WiFi 802.11 b/g/n, Bluetooth 5.0 LE
- **Power**: USB-C 5V or 3.3V battery
- **Dimensions**: Lolin C3 Mini form factor

## 🔧 Versions

### v2.0.0 (Latest)
- Complete restaurant branding integration
- Optimized 2-meter BLE range
- Enhanced battery life with 5-second LED timer
- Professional RGB color management
- Stable WiFi and BLE coexistence

### v1.0.0 (Stable)
- Initial release with core functionality
- Basic BLE advertising and WiFi setup
- Standard LED indicators

##  Advanced Configuration

The device automatically configures itself for restaurant use. For advanced settings, connect to the serial console at 115200 baud to monitor system status.

## Support

For technical support or custom configurations:
- Create an issue in this repository
- Provide serial console output for debugging
- Include device model and version information

## License

This project is distributed as binary-only releases. Source code is proprietary.

## About Carenuity

Professional IoT solutions for the hospitality industry. Visit [https://solutions.carenuity.com/](https://solutions.carenuity.com/) for more restaurant technology solutions.

---

**Carenuity Restaurant Solutions** - Professional IoT for Hospitality
