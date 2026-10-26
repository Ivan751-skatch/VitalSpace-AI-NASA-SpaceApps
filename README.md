# 🚀 VitalSpace AI — Real-Time Health & Radiation Monitoring
> **NASA Space Apps Challenge 2026** — *Challenge: Software Development for Monitoring Astronaut Health in Space Missions*

---

## 💡 Why We Built This
Travel to the Moon or Mars is fascinating, but space is unforgiving. When a crew is millions of kilometers from Earth, radio signals take minutes to hours to travel back and forth. In the event of a sudden oxygen drop, high radiation exposure, or a microgravity impact, **waiting for instructions from Earth is not an option.**

**VitalSpace AI** emerges as an autonomous solution based on **Edge Computing**. The system operates locally on the spacesuit's microcontroller, analyzing physiological constants and environmental factors in real time without relying on an internet connection or ground control stations.

---

## 🛠️ How It Works

We use an **ESP32 DevKit V1** microcontroller as the local computing core, integrating physiological, environmental, and inertial sensors:

| Component | Space Function | ESP32 Pin / Connection |
| :--- | :--- | :--- |
| **ESP32 DevKit V1** | Processes telemetry and evaluates physiological and inertial risks in real time. | — |
| **LCD 16x2 Screen (I2C)** | Displays diagnostics directly to the astronaut on the visor or suit interface. | SDA (GPIO 21) / SCL (GPIO 22) |
| **MPU6050 Sensor (IMU)** | Measures triaxial acceleration, detecting falls, impacts, and microgravity changes ($g$-force). | SDA (GPIO 21) / SCL (GPIO 22) |
| **DHT22 Sensor** | Measures the internal temperature of the spacesuit microclimate. | GPIO 15 |
| **SpO2 Potentiometer** | Simulates blood oxygen saturation ($70\% - 100\%$) and heart rate ($65 - 140\text{ BPM}$). | GPIO 35 (ADC1) |
| **Radiation Potentiometer** | Simulates cumulative ionizing radiation exposure ($0.0 - 50.0\text{ mSv/h}$). | GPIO 34 (ADC1) |
| **Green LED** | Visual indicator for nominal / optimal status. | GPIO 27 |
| **Yellow LED** | Visual indicator for warning / caution status. | GPIO 32 |
| **Red LED** | Visual indicator for critical alert or impact. | GPIO 26 |
| **Piezoelectric Buzzer** | Emits differentiated acoustic alerts to prevent alarm fatigue. | GPIO 25 |

---

## 🚥 3-Tier Triage Matrix & Audio Logic

| Status | Activation Conditions | Visual Indicator | Audio Response | LCD Output |
| :--- | :--- | :--- | :--- | :--- |
| **OPTIMAL** | SpO2 >= 95%, Radiation < 15 mSv, G-force between 0.2g and 2.5g | Green LED | Single confirmation pulse (880 Hz, 200 ms) | `ESTADO: OPTIMO` |
| **WARNING** | SpO2 90-94% **OR** Radiation 15-30 mSv | Yellow LED | Intermediate pulse every 2 s (600 Hz, 300 ms) | `PRECAUCION!` |
| **CRITICAL** | SpO2 < 90% **OR** Radiation > 30 mSv **OR** G-force > 2.5g / < 0.2g | Red LED | Continuous intense alarm (1200 Hz, 400 ms) | `ALERTA CRITICA` / `IMPACTO / CAIDA` |

---

## 📊 Real-Time Telemetry (JSON)

The system generates a continuous serial telemetry stream at **115200 baud**, formatted in standardized JSON for consumption by mission interfaces or AI models:

```json
{
  "spo2": 98,
  "hr": 70,
  "rad": 4.5,
  "temp": 24.50,
  "g_force": 1.05,
  "fall": false,
  "status": "OPTIMAL"
}
