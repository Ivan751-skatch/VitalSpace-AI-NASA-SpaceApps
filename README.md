# VitalSpace-AI-NASA-SpaceApps
Sistema de Monitoreo de Salud de la Tripulación y Radiación - NASA Space Apps Challenge 2026

# 🚀 VitalSpace AI – Monitoreo de salud y radiación en tiempo real

> **NASA Space Apps Challenge 2026** – *Desafío: Desarrollo de un software para monitorear la salud de los astronautas en misiones espaciales*

---

### 💡 ¿Por qué desarrollamos esto?

Los viajes a la Luna o a Marte parecen fascinantes, pero el espacio es implacable. Cuando una tripulación se encuentra a millones de kilómetros de la Tierra, una señal de radio enviada a la Tierra —y la respuesta de vuelta— puede tardar varios minutos. Si el nivel de oxígeno de un astronauta cae repentinamente, o si este se ve expuesto a una dosis elevada de radiación, **esperar una respuesta desde la Tierra no es una opción**.

Por ello, desarrollamos **VitalSpace AI**. Nuestro objetivo fue crear una solución autónoma basada en *Edge Computing* (computación en el borde) —un sistema que no depende de una conexión a Internet ni de una estación en tierra, sino que monitorea los signos vitales en tiempo real y toma decisiones médicas de forma inmediata.

---

### 🛠️ ¿Cómo funciona?

Utilizamos un microcontrolador **ESP32** como el "cerebro" del sistema. A él se conectan diversos sensores que simulan las condiciones físicas durante una misión espacial:

| Componente | Función en el espacio | Conexión en el ESP32 |
| :--- | :--- | :--- |
| **ESP32 DevKit V1** | Procesa datos de telemetría y evalúa riesgos fisiológicos en tiempo real. | — |
| **Pantalla LCD 16x2** | Muestra datos de diagnóstico directamente al astronauta (por ejemplo, en el visor o dentro del traje espacial). | SDA (GPIO 21) / SCL (GPIO 22)[cite: 8] |
| **Sensor DHT22** | Mide la temperatura en el interior del traje espacial. | GPIO 15[cite: 8] | | **Potenciómetro 1** | Simula los valores de medición de un dosímetro de radiación ($0$ a $50\text{ mSv/h}$). | GPIO 34 (ADC1)[cite: 8] |
| **Potenciómetro 2** | Simula la saturación de oxígeno ($70\,\%$ a $100\,\%\text{ SpO}_2$), así como la frecuencia cardíaca. | GPIO 35 (ADC1)[cite: 8] |
| **Indicadores LED / Zumbador** | Sistema de alerta visual y sonora para situaciones críticas. | GPIO 25, 26, 27[cite: 8] |

---

### 📊 Telemetría en tiempo real

El sistema genera un flujo continuo de datos en formato **JSON**, puesto a disposición de sistemas de control central o modelos de inteligencia artificial:

```json
{
  "spo2": 70,
  "hr": 140,
  "rad": 38.30,
  "temp": 24.00,
  "alert": true
}
```
## 🧪 Pruébalo en vivo en Wokwi (Sin instalar nada)Entra a nuestra simulación pública en Wokwi: 

https://wokwi.com/projects/478783474764323841 Haz clic en el botón de Play (Iniciar).

 **Haz tus propias pruebas de estrés**:Estado Seguro: Mantén el oxígeno alto y la radiación baja. Verás el LED verde encendido y el estado OPTIMO en pantalla.  

 **Simula una Emergencia**: Gira la perilla de radiación hacia la derecha o baja el oxígeno a menos de $90\%$. El sistema cambiará a ALERTA CRITICA, encenderá el LED rojo y activará la alarma sonora de inmediato.   
 
 ## 👥 Equipo VitalSpace AI
  **Desarrollo y Prototipado**: Ivan y equipo VitalSpace AI
  
  **Evento Local**: Evento Universal — NASA Space Apps Challenge 2026   Proyecto desarrollado con pasión por la tecnología y la exploración espacial.
