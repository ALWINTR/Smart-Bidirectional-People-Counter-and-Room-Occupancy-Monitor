# 🚶 Smart Bidirectional People Counter & Room Occupancy System

[![GitHub Repository](https://img.shields.io/badge/GitHub-Repository-00f0ff?style=for-the-badge&logo=github&logoColor=white)](https://github.com/ALWINTR/smart-people-counting-system)
[![Developer](https://img.shields.io/badge/Developer-Alwin_T_R-0284c7?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/alwintr)
[![Platform](https://img.shields.io/badge/Platform-ESP32_&_Ultrasonic-38bdf8?style=for-the-badge&logo=espressif&logoColor=white)](https://github.com/ALWINTR)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)

Smart bidirectional people counter and room occupancy monitoring system using dual ultrasonic/IR sensors and ESP32.

---

## 📌 System Architecture

A non-intrusive bidirectional automated people counting and room occupancy monitoring system designed for smart buildings, meeting rooms, and automated HVAC/lighting control.

```
       [Entrance / Gateway Barrier]
        Sensor A (Entry Trigger) ───┐
                                    ├──► [ESP32 Processing Unit] ──► [OLED Display & IoT Alert]
        Sensor B (Direction Phase) ──┘
```

---

## ⚙️ Hardware Bill of Materials (BOM)

| Component | Technical Specification | Function |
| :--- | :--- | :--- |
| **Microcontroller** | ESP32-WROOM-32 / Arduino Uno | Signal timing & directional logic FSM |
| **Distance Sensor A** | HC-SR04 Ultrasonic / Optical IR Beam | Primary entrance tripwire sensor |
| **Distance Sensor B** | HC-SR04 Ultrasonic / Optical IR Beam | Secondary exit/sequence confirmation sensor |
| **Display Unit** | SSD1306 0.96" I2C OLED Display (128x64) | Live room headcount & capacity indicator |
| **Acoustic Indicator** | 5V Active Piezo Buzzer | Threshold capacity alert tone |
| **Status LEDs** | Green (Available) / Red (Max Capacity) | Visual occupancy indicator |

---

## 🔌 Circuit Pinout Table

| Sensor / Module Pin | ESP32 GPIO Pin | Arduino Pin | Description |
| :--- | :--- | :--- | :--- |
| **Sensor A Trigger / Echo** | GPIO 5 / GPIO 18 | D2 / D3 | Outer entry detection beam |
| **Sensor B Trigger / Echo** | GPIO 19 / GPIO 21 | D4 / D5 | Inner entry confirmation beam |
| **OLED Display SDA / SCL** | GPIO 21 / GPIO 22 | A4 / A5 | I2C graphics datastream |
| **Capacity Warning Buzzer** | GPIO 4 | D8 | Audio alarm on room overflow |
| **Status Green / Red LEDs** | GPIO 2 / GPIO 15 | D11 / D12 | Room occupancy state indicators |

---

## 🧠 Directional Sequence Logic

- **ENTRY Event**: Sensor A trips FIRST ➔ Sensor B trips SECOND within 1500ms ➔ `Count = Count + 1`.
- **EXIT Event**: Sensor B trips FIRST ➔ Sensor A trips SECOND within 1500ms ➔ `Count = Count - 1` (Clamped at 0).
- **Capacity Alert**: When `Count >= MAX_CAPACITY`, triggers red LED latch and acoustic siren.

---

## 👨‍💻 Author

**Alwin T R** — Robotics & Automation Engineer  
- 💼 LinkedIn: [linkedin.com/in/alwintr](https://www.linkedin.com/in/alwintr)  
- 🌌 Portfolio: [alwintr.github.io](https://alwintr.github.io)  
- 💻 GitHub: [github.com/ALWINTR](https://github.com/ALWINTR)

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.
