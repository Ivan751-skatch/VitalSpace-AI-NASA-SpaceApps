# VitalSpace-AI-NASA-SpaceApps
Crew Health & Radiation Monitoring System - NASA Space Apps Challenge 2026

# 🚀 VitalSpace AI – Real-Time Health & Radiation Monitoring

> **NASA Space Apps Challenge 2026** – *Challenge: Creating Software for Astronaut Health Monitoring in Space Missions*

---

### 💡 Why did we build this?

Travel to the Moon or Mars sounds fascinating, but space is unforgiving. When a crew is millions of kilometers away from Earth, a radio signal sent to Earth — and the response back — can take several minutes. If an astronaut's oxygen level drops suddenly, or if they are exposed to a high dose of radiation, **waiting for a response from Earth is not an option**.

That is why we developed **VitalSpace AI**. Our goal was to create an autonomous solution based on *Edge Computing* — a system that does not rely on an internet connection or a ground station, but instead monitors vital signs in real time and makes immediate medical decisions.

---

### 🛠️ How does it work?

We use an **ESP32** microcontroller as the "brain" of the system. Connected to it are various sensors simulating physical conditions during a space mission:

| Component | Function in Space | ESP32 Pin Connection |
| :--- | :--- | :--- |
| **ESP32 DevKit V1** | Processes telemetry data and evaluates physiological risks in real time. | — |
| **16x2 LCD Display** | Displays diagnostic data directly to the astronaut (e.g., inside the visor or space suit). | SDA (GPIO 21) / SCL (GPIO 22) |
| **DHT22 Sensor** | Measures temperature inside the space suit. | GPIO 15 |
| **Potentiometer 1** | Simulates radiation dosimeter readings ($0$ to $50\text{ mSv/h}$). | GPIO 34 (ADC1) |
| **Potentiometer 2** | Simulates oxygen saturation ($70\%$ to $100\%\text{ SpO}_2$) and heart rate. | GPIO 35 (ADC1) |
| **LED Indicators / Buzzer** | Visual and acoustic alert system for critical situations. | GPIO 25, 26, 27 |

---

### 📊 Real-Time Telemetry

The system generates a continuous data stream in **JSON** format, made available to central control systems or artificial intelligence models:

```json
{
  "spo2": 70,
  "hr": 140,
  "rad": 38.30,
  "temp": 24.00,
  "alert": true
}
🧪 Try it live on Wokwi (No installation required)Access our public simulation on Wokwi:https://wokwi.com/projects/478783474764323841Click the Play (Start) button.Perform your own stress tests:Safe State: Keep oxygen high and radiation low. You will see the green LED turn on and the OPTIMO status on the screen.Simulate an Emergency: Turn the radiation knob to the right or lower oxygen below $90\%$. The system will switch to ALERTA CRITICA, turn on the red LED, and immediately trigger the buzzer alarm.👥 VitalSpace AI TeamDevelopment & Prototyping: Ivan and the VitalSpace AI team.Local Event: Universal Event — NASA Space Apps Challenge 2026Project developed with passion for technology and space exploration
