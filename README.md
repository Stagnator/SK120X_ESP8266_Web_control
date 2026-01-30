# SK120x Web Controller (ESP8266 + RS485-to-UART module + Modbus) (NOT TESTED)

This project provides a **web-based controller** for the [SK120X DC Regulated Power Supply DC-DC Step Up/Down Converter](https://www.amazon.com/SK120X-Regulated-Stabilized-Voltage-Converter/dp/B0F18HZD97) using an **ESP8266**, **RS485 transceiver**, and **Modbus RTU**.

![SK120X Module](https://m.media-amazon.com/images/I/51RH2QGF4BL._AC_SL1500_.jpg)

<img width="550" height="550" alt="image" src="https://github.com/Stagnator/SK120X_ESP8266_Web_control/blob/esp8266/images/MAX485_module_1-550x550.jpg" />

---

## ✨ Features
- 📡 WiFi connectivity (station or fallback access point mode)  
- 🌐 Embedded web interface (HTML/CSS/JS served directly from ESP8266)  
- ⚡ Live monitoring of:
  - Set Voltage / Current  
  - Output Voltage / Current / Power  
  - Output state (ON/OFF)  
  - MPPT (experimental)  
- 🎛️ Remote control of:
  - Voltage & Current setpoints  
  - Output toggle  
  - MPPT enable/disable  
- 📊 Built-in charts:
  - Voltage/Current history line chart  
  - Voltage histogram  
- 🔍 Register scanner with CSV export  
- 🛠️ Modular HTML UI (panels, gauges, seven-segment style readouts)

---

## 🖥️ Web Interface Preview
- **Top Row:** Current status, setpoints, toggle controls  
- **Middle Row:** Voltage/Current history chart, histogram  
- **Bottom Row:** Modbus register scanner with CSV export  

The UI is entirely self-contained (no CDN or external JS), ensuring it works offline once loaded.

---

## ⚙️ Hardware Setup
- **ESP8266** WEMOS mini development board
- **RS485 transceiver module** (DE/RE control supported, configurable)  
- **SK120X DC-DC Power Supply**  

**Pin Mapping (default):**
| Signal        | ESP8266 PIN |
|---------------|-------------|
| RS485 DI      | 15          |
| RS485 RO      | 13          |
| RS485 DE/RE   | 12          | 
| +5v           | 5V          |
| GND           | GND         |
| Baudrate      | 115200      |

---

## 🔌 Software Setup
1. Install [Arduino IDE](https://www.arduino.cc/en/software) with ESP8266 board support  
2. Install libraries:  
   - `ModbusMaster`  
   - `WebServer` (comes with ESP8266 Arduino core)  
3. Update your WiFi credentials in the sketch:  
   ```cpp
   const char *WIFI_SSID = "YOUR_WIFI_SSID";
   const char *WIFI_PASS = "YOUR_WIFI_PASSWORD";
Compile & upload to your ESP8266.

Open Serial Monitor to see IP address (or connect to fallback AP SK120x-ESP8266).

Navigate to the IP address in your browser to access the web UI.

📡 API Endpoints

GET / → Web UI

GET /api/status → JSON with live status

POST /api/write?reg=X&val=Y → Write Modbus register

GET /api/scan?start=A&end=B → Scan Modbus registers

📝 Notes

MPPT support is experimental – some SK120x firmware revisions may not implement it.

Register scanner helps discover unknown registers and their values.

The project mimics LabVIEW-style panels for readability and modular control.

📚 Resources

SK120X DC Power Supply on Amazon
UART-RS485 converter MAX485

📜 License

MIT License – free to use, modify, and share.
