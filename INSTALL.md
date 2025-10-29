# Smart Table Installation Guide

## Prerequisites
- PlatformIO installed (https://platformio.org/install)
- ESP32-C3 development board
- USB-C cable

## Installation Steps

### 1. Install Dependencies
```powershell
# Install PlatformIO if not already installed
pip install platformio

# Navigate to project directory
cd "C:\Users\SpaceX\OneDrive - CHIPGLOBEGmbH\Documents\PlatformIO\Projects\Ble-ibeacon"

# Install required libraries
pio lib install
```

### 2. Build Project
```powershell
# Clean and build
pio run --target clean
pio run
```

### 3. Upload to Device
```powershell
# Connect ESP32-C3 via USB-C
# Upload firmware
pio run --target upload

# Monitor serial output
pio device monitor --baud 115200
```

### 4. Initial Configuration
1. Power on the device
2. Connect to WiFi network "SmartTable-Setup-1"
3. Password: `smarttable123`
4. Open browser and configure:
   - WiFi credentials
   - Table number
   - Restaurant name
   - Beacon UUID (optional)

### 5. Access System
- **Customer Interface**: `http://[device-ip]/`
- **Admin Dashboard**: `http://[device-ip]/admin`

## Troubleshooting

### Build Issues
- Ensure all libraries are installed: `pio lib install`
- Clean build: `pio run --target clean`

### Upload Issues
- Check USB-C connection
- Verify correct COM port
- Hold BOOT button while connecting

### WiFi Issues
- Factory reset: Hold button for 5 seconds
- Reconfigure WiFi through captive portal

## Default Configuration
- **Device Name**: SmartTable-[TableNumber]
- **WiFi AP**: SmartTable-Setup-[TableNumber]
- **Default Password**: smarttable123
- **Web Port**: 80
- **Beacon UUID**: A1B2C3D4-E5F6-7788-9900-AABBCCDDEEFF