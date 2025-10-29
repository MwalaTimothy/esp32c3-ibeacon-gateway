# ESP32-C3 iBeacon Gateway - Carenuity Restaurant# ESP32-C3 iBeacon Gateway - Carenuity Restaurant# ESP32-C3 iBeacon Gateway - Carenuity Restaurant



A professional ESP32-C3 based iBeacon gateway system designed specifically for restaurant environments. This device creates a Bluetooth Low Energy (BLE) beacon that customers can use to connect to restaurant services with their smartphones.



## 🌟 FeaturesA professional ESP32-C3 based iBeacon gateway system designed specifically for restaurant environments. This device creates a Bluetooth Low Energy (BLE) beacon that customers can use to connect to restaurant services with their smartphones.A professional ESP32-C3 based iBeacon gateway system designed specifically for restaurant environments. This device creates a Bluetooth Low Energy (BLE) beacon that customers can use to connect to restaurant services with their smartphones.



- **Restaurant-Ready**: Pre-configured for "Carenuity Restaurant" branding

- **Optimized Range**: 2-meter transmission range for table-specific service

- **Battery Efficient**: 5-second LED indicators to maximize battery life## 🌟 Features## 🌟 Features

- **Easy WiFi Setup**: ImprovWiFi for smartphone-based configuration

- **Visual Feedback**: RGB NeoPixel LED status indicators

- **Plug & Play**: Ready-to-use merged binary files

- **Restaurant-Ready**: Pre-configured for "Carenuity Restaurant" branding- **Restaurant-Ready**: Pre-configured for "Carenuity Restaurant" branding

## ⚡ Quick Installation

- **Optimized Range**: 2-meter transmission range for table-specific service- **Optimized Range**: 2-meter transmission range for table-specific service

**Instant Setup**: Use our web-based solution builder at **[https://solutions.carenuity.com/](https://solutions.carenuity.com/)** for one-click installation and configuration!

- **Battery Efficient**: 5-second LED indicators to maximize battery life- **Battery Efficient**: 5-second LED indicators to maximize battery life

## 🚀 Manual Installation

- **Easy WiFi Setup**: ImprovWiFi for smartphone-based configuration- **Easy WiFi Setup**: ImprovWiFi for smartphone-based configuration

### Hardware Required

- **Visual Feedback**: RGB NeoPixel LED status indicators- **Visual Feedback**: RGB NeoPixel LED status indicators

- ESP32-C3 Lolin Mini development board

- Built-in NeoPixel RGB LED (GPIO 7)- **Plug & Play**: Ready-to-use merged binary files- **Plug & Play**: Ready-to-use merged binary files

- USB-C cable for flashing



### Installation Steps

## 🚀 Quick Start## 🚀 Quick Start

1. **Download Latest Binary**

   - Download `carenuity-restaurant-ibeacon-v2.0.0.bin` from [Releases](https://github.com/MwalaTimothy/esp32c3-ibeacon-gateway/releases)



2. **Flash to ESP32-C3**### Hardware Required### Hardware Required

   ```bash

   # Using esptool (install with: pip install esptool)- ESP32-C3 Lolin Mini development board

   esptool.py --chip esp32c3 --port COM_PORT write_flash 0x0 carenuity-restaurant-ibeacon-v2.0.0.bin

   ```- ESP32-C3 Lolin Mini development board- Built-in NeoPixel RGB LED (GPIO 7)

   Replace `COM_PORT` with your actual port (COM3, COM4, etc.)

- Built-in NeoPixel RGB LED (GPIO 7)- USB-C cable for flashing

3. **Setup WiFi**

   - Power on the device- USB-C cable for flashing

   - Look for "Carenuity Restaurant" in your phone's WiFi settings

   - Follow ImprovWiFi setup prompts### Installation



## 📱 BLE Configuration### Installation



- **Device Name**: "Carenuity Restaurant"1. **Download Latest Binary**

- **Range**: ~2 meters (optimized for table service)

- **Power**: -12dBm transmission power1. **Download Latest Binary**   - Download `carenuity-restaurant-ibeacon-v2.0.0.bin` from [Releases](https://github.com/MwalaTimothy/esp32c3-ibeacon-gateway/releases)

- **Advertising**: 160-320ms intervals for optimal phone compatibility

   - Download `carenuity-restaurant-ibeacon-v2.0.0.bin` from [Releases](https://github.com/MwalaTimothy/esp32c3-ibeacon-gateway/releases)

## 🔋 Power Management

2. **Flash to ESP32-C3**

- **LED Behavior**: 5-second status indicators only

- **Sleep Mode**: Automatic power optimization2. **Flash to ESP32-C3**   ```bash

- **Battery Life**: Extended operation with efficient BLE advertising

   # Using esptool (install with: pip install esptool)

## 🎨 LED Status Indicators

   ```bash   esptool.py --chip esp32c3 --port COM_PORT write_flash 0x0 carenuity-restaurant-ibeacon-v2.0.0.bin

| Color | Status |

|-------|--------|   # Using esptool (install with: pip install esptool)   ```

| 🟢 Green | WiFi Connected & BLE Active |

| 🔵 Blue | BLE Advertising (no WiFi) |   esptool.py --chip esp32c3 --port COM_PORT write_flash 0x0 carenuity-restaurant-ibeacon-v2.0.0.bin   Replace `COM_PORT` with your actual port (COM3, COM4, etc.)

| 🟡 Yellow | WiFi Setup Mode |

| 🔴 Red | Error/Boot State |   ```

| ⚫ Off | Power Saving (after 5 seconds) |

3. **Setup WiFi**

## 📋 Technical Specifications

   Replace `COM_PORT` with your actual port (COM3, COM4, etc.)   - Power on the device

- **MCU**: ESP32-C3 (160MHz RISC-V)

- **Memory**: 320KB RAM, 4MB Flash   - Look for "Carenuity Restaurant" in your phone's WiFi settings

- **Connectivity**: WiFi 802.11 b/g/n, Bluetooth 5.0 LE

- **Power**: USB-C 5V or 3.3V battery3. **Setup WiFi**   - Follow ImprovWiFi setup prompts

- **Dimensions**: Lolin C3 Mini form factor

   - Power on the device

## 🔧 Versions

   - Look for "Carenuity Restaurant" in your phone's WiFi settings### 4. Table Configuration

### v2.0.0 (Latest)

   - Follow ImprovWiFi setup prompts

- Complete restaurant branding integration

- Optimized 2-meter BLE range**Via Web Interface:**

- Enhanced battery life with 5-second LED timer

- Professional RGB color management## 📱 BLE Configuration1. Navigate to device IP address in browser

- Stable WiFi and BLE coexistence

2. Configure table number (1-999)

### v1.0.0 (Stable)

- **Device Name**: "Carenuity Restaurant"3. Set server URL for ordering system

- Initial release with core functionality

- Basic BLE advertising and WiFi setup- **Range**: ~2 meters (optimized for table service)4. Click "Save Configuration" - device restarts automatically

- Standard LED indicators

- **Power**: -12dBm transmission power

## 🛠️ Advanced Configuration

- **Advertising**: 160-320ms intervals for optimal phone compatibility### 5. Verify Operation

The device automatically configures itself for restaurant use. For advanced settings, connect to the serial console at 115200 baud to monitor system status.



## 📞 Support

## 🔋 Power Management**Check iBeacon Broadcasting:**

### Technical Support

- UUID: `12345678-90AB-CDEF-1234-567890ABCDEF`

For technical support or custom configurations:

- Create an issue in this repository- **LED Behavior**: 5-second status indicators only- Major/Minor: Both set to your table number

- Provide serial console output for debugging

- Include device model and version information- **Sleep Mode**: Automatic power optimization- Use beacon scanner app to verify detection



### Financial Support- **Battery Life**: Extended operation with efficient BLE advertising   - Password: `smarttable123`



Support this project development:   - Configure WiFi credentials and table settings

- **PayPal**: [mwalatimo@gmail.com](mailto:mwalatimo@gmail.com)

- **Buy Me a Coffee**: Support ongoing development and maintenance## 🎨 LED Status Indicators## 🔧 Configuration Details



Your support helps maintain and improve this open-source project!



## 📄 License| Color | Status |### iBeacon Settings



This project is distributed as binary-only releases. Source code is proprietary.|-------|--------|- **UUID**: `12345678-90AB-CDEF-1234-567890ABCDEF` (fixed)



## 🏢 About Carenuity| 🟢 Green | WiFi Connected & BLE Active |- **Major**: Dynamically set to table number (1-999)



Professional IoT solutions for the hospitality industry. Visit [https://solutions.carenuity.com/](https://solutions.carenuity.com/) for more restaurant technology solutions.| 🔵 Blue | BLE Advertising (no WiFi) |- **Minor**: Dynamically set to table number (1-999)



---| 🟡 Yellow | WiFi Setup Mode |- **TX Power**: Optimized for table-level detection



**Carenuity Restaurant Solutions** - Professional IoT for Hospitality| 🔴 Red | Error/Boot State |

| ⚫ Off | Power Saving (after 5 seconds) |### Web Interface Features

- **Dashboard**: Real-time status display with IP address

## 📋 Technical Specifications- **Table Number**: Configurable via web form (1-999)

- **Server URL**: Configurable endpoint for pizza ordering system

- **MCU**: ESP32-C3 (160MHz RISC-V)- **Live Updates**: iBeacon data updates immediately when table number changes

- **Memory**: 320KB RAM, 4MB Flash- **Device Restart**: Safe restart after configuration changes

- **Connectivity**: WiFi 802.11 b/g/n, Bluetooth 5.0 LE

- **Power**: USB-C 5V or 3.3V battery### Storage System

- **Dimensions**: Lolin C3 Mini form factorAll settings are automatically saved to ESP32-C3 non-volatile storage:

- WiFi credentials (SSID/password)

## 🔧 Versions- Table number

- Server URL for ordering system

### v2.0.0 (Latest)

## 📱 Integration Guide

- Complete restaurant branding integration

- Optimized 2-meter BLE range### For Mobile App Developers

- Enhanced battery life with 5-second LED timer```javascript

- Professional RGB color management// Example: Detecting table iBeacons

- Stable WiFi and BLE coexistenceconst tableUUID = "12345678-90AB-CDEF-1234-567890ABCDEF";



### v1.0.0 (Stable)// Listen for beacon detection

function onBeaconDetected(beacon) {

- Initial release with core functionality    if (beacon.uuid === tableUUID) {

- Basic BLE advertising and WiFi setup        const tableNumber = beacon.major; // or beacon.minor

- Standard LED indicators        openOrderingInterface(tableNumber);

    }

## 🛠️ Advanced Configuration}

```

The device automatically configures itself for restaurant use. For advanced settings, connect to the serial console at 115200 baud to monitor system status.

### For Restaurant Systems

## 📞 Support```http

# Configure device remotely

For technical support or custom configurations:POST http://[device-ip]/config

Content-Type: application/x-www-form-urlencoded

- Create an issue in this repository

- Provide serial console output for debuggingtable=15&server=https://yourrestaurant.com/order

- Include device model and version information```



## 📄 License## �️ Technical Specifications



This project is distributed as binary-only releases. Source code is proprietary.### Beacon Parameters

```cpp

---#define BEACON_UUID_DEFAULT "A1B2C3D4-E5F6-7788-9900-AABBCCDDEEFF"

#define BEACON_MAJOR_DEFAULT 1

**Carenuity Restaurant Solutions** - Professional IoT for Hospitality// Minor = Table Number (automatically assigned)
```

### Network Settings
- **Access Point**: SmartTable-Setup-[TableNumber]
- **Default Password**: smarttable123
- **Web Server Port**: 80
- **Configuration Timeout**: 5 minutes

### Factory Reset
- Hold built-in button for 5 seconds
- Device will erase all settings and restart
- Returns to initial setup mode

## 🌐 API Endpoints

### Public APIs
- `GET /` - Main menu interface
- `GET /order` - Order placement page
- `POST /api/order` - Submit new order
- `GET /api/status` - System status (public info)

### Admin APIs
- `GET /admin` - Administration dashboard
- `GET /api/orders` - Full order history
- `GET /api/status` - Detailed system metrics

## 🔌 Hardware Connections

### ESP32-C3 Pinout
- **Reset Button**: GPIO9 (built-in)
- **Status LED**: GPIO8 (built-in)
- **USB Programming**: USB-C port
- **Power**: 3.3V via USB or external

### Optional Additions
- **External Antenna**: For extended BLE range
- **Status Display**: I2C OLED for local status
- **Sensors**: Temperature, occupancy detection

## 🛠️ Development

### Build System
- **Platform**: Espressif ESP32 (Arduino Framework)
- **Libraries**: WiFiManager, ArduinoJson, ESPAsyncWebServer
- **Build Tool**: PlatformIO

### Debugging
```bash
# Monitor serial output
pio device monitor

# Debug build with verbose output
pio run -e lolin_c3_mini -v
```

### Custom Menu Items
Edit the `generateMenuPage()` function to modify menu items:

```cpp
// Add new menu item
<div class="menu-item">
    <h3>🥗 Caesar Salad</h3>
    <p>Fresh romaine, parmesan, croutons</p>
    <div class="price">$8.99</div>
    <button class="add-btn" onclick="addToCart('Caesar Salad', 8.99)">Add to Cart</button>
</div>
```

## 📊 Performance Metrics

### Power Consumption
- **Active Mode**: ~80mA @ 3.3V
- **Deep Sleep**: ~10µA (when implemented)
- **Battery Life**: 24+ hours with 2000mAh battery

### Network Performance
- **WiFi Range**: 50-100m (depending on environment)
- **BLE Range**: 10-30m (Class 2 device)
- **Concurrent Users**: 10+ simultaneous web connections

### Memory Usage
- **Flash**: ~1.2MB (of 4MB available)
- **RAM**: ~200KB (of 400KB available)
- **Order Storage**: 50+ orders in memory

## 🔐 Security Considerations

### Network Security
- WPA2 WiFi encryption required
- No sensitive data stored in plaintext
- HTTPS recommended for production

### Data Privacy
- Customer names stored temporarily only
- No payment processing (integrate with POS)
- Regular memory cleanup of old orders

## 🚀 Future Enhancements

### Planned Features
- [ ] Payment integration (Stripe/Square)
- [ ] Kitchen display system integration
- [ ] Multi-language support
- [ ] Voice ordering via Web Speech API
- [ ] Loyalty program integration
- [ ] Inventory management
- [ ] Analytics and reporting

### Hardware Upgrades
- [ ] E-paper display for status
- [ ] LoRa integration for outdoor venues
- [ ] Solar charging capability
- [ ] Waterproof enclosure options

## 📞 Support

For technical support or feature requests:
- Create GitHub issue
- Check documentation wiki
- Join community Discord

## 📄 License

MIT License - See LICENSE file for details

---

**Made with ❤️ for restaurants worldwide**