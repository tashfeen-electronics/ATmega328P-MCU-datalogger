# ATmega328P Data Logger — EEPROM + RTC

<img width="1040" height="592" alt="image" src="https://github.com/user-attachments/assets/9604f966-d5f5-4f03-b64c-4481d62bca19" />



A compact, standalone data logging system built around the **ATmega328P** microcontroller, featuring **non-volatile EEPROM storage** and a **real-time clock (RTC)** for accurate timestamping. Designed for reliable, low-power, long-duration data collection without needing a constant computer connection.

---

## 🧠 Overview

This project logs sensor readings at fixed intervals, timestamps each entry using an RTC module, and stores the data permanently in EEPROM — surviving power loss, resets, and disconnects. It's built as a foundation for embedded data acquisition systems that need to run unattended in the field.

---

## ⚙️ Features

- 📌 Real-time timestamping using an external RTC module
- 💾 Persistent storage via EEPROM (data survives power cycles)
- 🔁 Configurable logging interval
- 🔋 Low power design, suitable for battery-powered deployment
- 📤 Simple data retrieval for post-processing and analysis
- 🧩 Modular code structure — easy to extend with new sensors

---

## 🛠️ Hardware Used

| Component            | Purpose                          |
|-----------------------|-----------------------------------|
| ATmega328P            | Core microcontroller / logic unit |
| RTC Module DS1337S    | Real-time timestamping   |
| EEPROM (external/internal) | Non-volatile data storage     |
| Sensor(s)              | Data source (analog/digital)     |
| Power supply / battery | Field-deployable operation       |

---

## 🧩 System Architecture

```
[ Sensor ] → [ ATmega328P ] → [ RTC: Timestamp ] → [ EEPROM: Store ]
                                      ↓
                              [ Data Retrieval / Analysis ]
```

**Flow:**
1. The MCU wakes up (or runs continuously) and triggers a reading at a set interval.
2. The RTC module provides the current date and time.
3. Sensor data is paired with the timestamp.
4. The combined record is written to EEPROM at the next available memory address.
5. Data can later be read out via serial interface for analysis.

---

## 📝 Design Notes

- **Memory management:** EEPROM write cycles are limited (~100,000 per cell), so writes are spaced out and address pointers are tracked to avoid unnecessary wear and overwrites.
- **Timestamp accuracy:** The RTC module runs independently of the MCU clock, so logged times remain accurate even after resets or brief power loss (backed by a coin-cell battery).
- **Data structure:** Each log entry is packed into a fixed-size record (timestamp + sensor value) to keep read/write operations predictable and efficient.
- **Power efficiency:** Sleep modes are used between logging intervals to minimize current draw for battery-powered, long-term deployments.
- **Scalability:** The logging interval, sensor type, and storage size are all designed to be easily reconfigurable without restructuring the core logic.
<img width="668" height="449" alt="image" src="https://github.com/user-attachments/assets/eb9c94c0-9806-4100-9785-30ae9aba3993" />
<img width="669" height="445" alt="image" src="https://github.com/user-attachments/assets/12dab939-d40e-4576-acc2-4842dca84590" />
<img width="1040" height="592" alt="ATMEGA328P Datalogger RAY Front" src="https://github.com/user-attachments/assets/06c4e86f-fdd3-4b50-bf94-6387c16b2195" />
<img width="1040" height="592" alt="ATMEGA328P Datalogger RAY BACK ray" src="https://github.com/user-attachments/assets/95c6436b-9b1f-426e-a25f-f1ec25df2265" />

---

## 🚀 Practical Applications

- 🌱 **Agriculture** — soil moisture / temperature logging for irrigation planning
- 🌡️ **Environmental monitoring** — tracking temperature, humidity, or air quality over time
- 🏭 **Industrial systems** — recording equipment performance for predictive maintenance
- 🔬 **Research & academic projects** — collecting reliable, timestamped datasets in the field
- 🏠 **Home automation** — logging conditions for smart, data-driven decisions

---

## 📂 Data Retrieval

Logged data can be read out via the serial interface and exported for analysis in tools like Excel, Python (pandas), or MATLAB — enabling trend analysis, visualization, and further processing.

---

## 🔮 Future Improvements

- SD card integration for larger-scale storage
- Wireless data transmission (e.g. via ESP module)
- Multi-sensor support with dynamic record formatting
- Low-power sleep/wake scheduling for extended battery life

---

## 📜 License

This project is open for learning, modification, and reuse. Feel free to fork, build on it, and share improvements.

---

**Built as part of ongoing exploration in embedded systems and circuit design.**
