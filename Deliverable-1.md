# ICS 4111: Embedded Systems & IoT - GROUP 8 DOREMI
## Semester Project: Deliverable 1

**Objective:** Identify requirements that support individual flower growth and develop schematic designs of embedded devices

---

## 1. Flower Environmental Requirements

**Flower:** Roses

| Parameter | Optimal Range / Type | Description |
|-----------|----------------------|-------------|
| a. Temperature | 15°C – 26°C | Roses grow best in mild temperatures. Below 10°C slows growth, while above 30°C can stress the plant and reduce flowering. |
| b. Relative Humidity | 60% – 70% | Moderate humidity supports transpiration and prevents excessive fungal diseases that occur in very high humidity. |
| c. Soil Type | Loamy, well-drained soil rich in organic matter | Ideal soil retains moisture while allowing excess water to drain, preventing root rot. |
| d. Soil Moisture Content | 60% – 70% (moderately moist) | Soil should remain consistently moist but not waterlogged. Overwatering leads to root diseases. |
| e. Soil pH Range | 6.0 – 6.5 (slightly acidic) | Ensures optimal nutrient absorption, especially nitrogen, phosphorus, and potassium. |
| f. Sunlight Exposure | 6 – 8 hours per day (full sunlight) | Roses require direct sunlight for proper photosynthesis and flower production. |

---

## 2. Hardware Components

### Microcontroller
- ESP32S DevKit WiFi + BLE Module (30-Pin)

### Sensors
- DHT22 (AM2302) Temperature and Humidity Sensor
- Soil Moisture Sensor (Capacitive Soil Moisture Sensor v1.2)
- Soil pH Sensor Module
- Light Sensor / Photoresistor (LDR) Module
- MQ-5 LPG, Natural Gas, and Coal Gas Sensor

### Actuators & Display
- 1.3" White IIC 128X64 OLED LCD Display
- 5V 1-Channel Low Level Trigger Relay Module

### Prototyping, Power & Wiring
- Full-Sized MB102 Breadboard
- Premium Jumper Wires (Male-to-Male, Female-to-Male, Female-to-Female)
- Micro-USB Cable
- 5V 2A Power Adapter (or Power Bank)
- 10k Ohm Resistors

---

## 3. Component Datasheets and Reference Webpages

### a. 1.3" White IIC 128X64 OLED LCD
- **Datasheet (SH1106 Controller):** [Pololu SH1106 PDF](https://www.pololu.com/file/0J1813/SH1106.pdf)
- **Datasheet (SSD1306 Controller):** [Adafruit SSD1306 PDF](https://cdn-shop.adafruit.com/datasheets/SSD1306.pdf)

### b. ESP32S DevKIT WIFI + BLE Module (30Pin)
- **Datasheet (ESP32-WROOM-32 Core Module):** [Espressif Official Datasheet PDF](https://www.espressif.com/sites/default/files/documentation/esp32-wroom-32_datasheet_en.pdf)
- **Product Webpage / Pinout Reference:** [Espressif DevKitC Hardware Reference](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/hw-reference/esp32/get-started-devkitc.html)

### c. DHT22 AM2302 Temperature and Humidity Sensor
- **Datasheet:** [Aosong AM2302 / DHT22 PDF](https://www.sparkfun.com/datasheets/Sensors/Temperature/DHT22.pdf)

### d. MQ-5 LPG, Natural Gas, Coal Gas Sensor
- **Datasheet (Hanwei Electronics MQ-5):** [Sparkfun MQ-5 PDF](https://www.sparkfun.com/datasheets/Sensors/Biometric/MQ-5.pdf)

### e. 5V 1-Channel Low Level Trigger Relay Module
- **Datasheet (Songle SRD-05VDC-SL-C):** [Components101 Songle Relay PDF](https://components101.com/sites/default/files/component_datasheet/5V%20Relay%20Datasheet.pdf)
- **Product Webpage / Reference:** [Components101 Relay Module Overview](https://components101.com/switches/5v-relay-module-pinout-features-applications-working-datasheet)

---

## 4. Schematic Circuit Diagrams

### Design A: Single ESP32S with All Sensors and LCD
*To be completed*

---

### Design B: Two ESP32S Modules Communicating (MQ-5 and DHT22 Separated)
*To be completed*

---

### Design C: Two ESP32S Modules Connected via Relay (DHT22 Controlling MQ-5)

**Architecture:** 1 ESP32S connected to 1 DHT22 connected to 1 relay which is connected to another ESP32S connected to 1 MQ-5

**Circuit Configuration:**
- **Module 1 (Left - DHT22 Module):** ESP32-WROVER-IB-N4R8 (U1) connected to DHT22 Temperature & Humidity Sensor (U2, U3)
- **Relay Control:** The DHT22 module triggers a RELAY-SPST (U5) based on environmental conditions
- **Module 2 (Right - MQ-5 Module):** ESP32-WROVER-IB-N4R8 (U7) connected to MQ-5 LPG/Gas Sensor (U4)
- **Power Supply:** Both modules powered at +5V and +3.3V with appropriate grounding

**Component Details (from BOM):**
| ID | Name | Designator | Footprint | Quantity |
|----|------|-----------|-----------|----------|
| 1 | ESP32-WROVER-IB-N4R8 | U1, U7 | WIFI-SMD ESP32-WROVER-IE8MB | 2 |
| 2 | DHT22 Temperature-Humidity Sensor | U2 | FL_001 | 1 |
| 3 | DHT22 | U3 | SENSOR-TH_HAIGU_DHT22 | 1 |
| 4 | MQ-5 | U4 | SENSOR-TH_MQ-5 | 1 |
| 5 | RELAY-SPST | U5 | RELAY-TH_RELAY-SPST | 1 |

**Schematic Diagram:**
[Design C Schematic - Two ESP32S with Relay Control](Design_C_Schematic.png)

**Key Features:**
- Relay acts as an interface between the two ESP32 modules
- DHT22 sensor on the primary ESP32 monitors temperature and humidity
- MQ-5 sensor on the secondary ESP32 monitors gas levels
- Relay allows conditional control of the gas monitoring module based on environmental conditions
