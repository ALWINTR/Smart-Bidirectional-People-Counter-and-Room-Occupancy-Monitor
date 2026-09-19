# Smart Bidirectional People Counter and Room Occupancy Monitor

[![GitHub Repository](https://img.shields.io/badge/GitHub-Repository-00f0ff?style=for-the-badge&logo=github&logoColor=white)](https://github.com/ALWINTR/smart-people-counting-system)
[![Developer](https://img.shields.io/badge/Developer-Alwin_T_R-0284c7?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/alwintr)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)

A non-intrusive bidirectional automated people counting and room occupancy monitoring system designed for smart buildings, meeting rooms, and automated energy management.

---

## System Architecture and Directional Logic

The counter uses two spatially offset distance sensors to determine movement direction:
- **ENTRY Event**: Sensor A triggers FIRST, followed by Sensor B within 1500ms -> Increment Room Count.
- **EXIT Event**: Sensor B triggers FIRST, followed by Sensor A within 1500ms -> Decrement Room Count (clamped at zero).
- **Capacity Alarm**: When count reaches or exceeds `MAX_CAPACITY`, activates an acoustic buzzer and flashes status indicators.

```
       [Entrance / Gateway Passage]
        Sensor A (Outer Tripwire) ---+
                                     +--> [ESP32 Processing Unit] ---> [OLED Display & Alarm]
        Sensor B (Inner Tripwire) ---+
```

---

## Hardware Bill of Materials (BOM)

| Component | Technical Specification | Functional Role |
| :--- | :--- | :--- |
| **Microcontroller** | ESP32-WROOM-32 / Arduino Uno | Timing analysis and directional logic FSM |
| **Distance Sensor A** | HC-SR04 Ultrasonic / Optical IR Sensor | Outer entrance detection beam |
| **Distance Sensor B** | HC-SR04 Ultrasonic / Optical IR Sensor | Inner entrance confirmation beam |
| **Display Unit** | SSD1306 0.96" I2C OLED Display (128x64) | Live room headcount and status indicator |
| **Audio Indicator** | 5V Active Piezo Buzzer | Threshold capacity alert tone |
| **Status LEDs** | Green (Available) / Red (Max Capacity) | Visual occupancy indicator |

---

## Circuit Pinout Table

| Sensor / Module Pin | ESP32 GPIO Pin | Arduino Pin | Description |
| :--- | :--- | :--- | :--- |
| **Sensor A Trigger / Echo** | GPIO 5 / GPIO 18 | D2 / D3 | Outer entrance tripwire sonar |
| **Sensor B Trigger / Echo** | GPIO 19 / GPIO 21 | D4 / D5 | Inner confirmation tripwire sonar |
| **OLED Display SDA / SCL** | GPIO 21 / GPIO 22 | A4 / A5 | I2C graphics communication bus |
| **Capacity Warning Buzzer** | GPIO 4 | D8 | Audio siren on room overflow |
| **Status LEDs** | GPIO 2 / GPIO 15 | D11 / D12 | Room occupancy state indicators |

---

## Author

**Alwin T R** - Robotics and Automation Engineer  
- LinkedIn: [linkedin.com/in/alwintr](https://www.linkedin.com/in/alwintr)  
- Portfolio: [alwintr.github.io](https://alwintr.github.io)  
- GitHub: [github.com/ALWINTR](https://github.com/ALWINTR)

---

## License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.
