Markdown
# 🚀 VitalSpace AI — Monitoreo de Salud y Radiación en Tiempo Real
> **NASA Space Apps Challenge 2026** — *Desafío: Desarrollo de Software para Monitorear la Salud de los Astronautas en Misiones Espaciales*

---

## 💡 ¿Por qué desarrollamos esto?
Los viajes a la Luna o a Marte son fascinantes, pero el espacio es implacable. Cuando una tripulación se encuentra a millones de kilómetros de la Tierra, las señales de radio tardan entre varios minutos y horas en ir y volver. Ante una caída repentina de oxígeno, una radiación elevada o un impacto en microgravedad, **esperar instrucciones desde la Tierra no es una opción.**

**VitalSpace AI** surge como una solución autónoma basada en **Edge Computing**. El sistema opera de manera local en el microcontrolador del traje espacial, analizando constantes fisiológicas y factores ambientales en tiempo real sin depender de conexión a Internet ni de estaciones de control en tierra.

---

## 🛠️ ¿Cómo funciona?

Utilizamos un microcontrolador **ESP32 DevKit V1** como centro de cómputo local. A él se integran sensores fisiológicos, ambientales e inerciales:

| Componente | Función en el Espacio | Conexión ESP32 |
| :--- | :--- | :--- |
| **ESP32 DevKit V1** | Procesa telemetría y evalúa riesgos fisiológicos e inerciales en tiempo real. | — |
| **Pantalla LCD 16x2 (I2C)** | Muestra diagnósticos directamente al astronauta en el visor o interfaz del traje. | SDA (GPIO 21) / SCL (GPIO 22) |
| **Sensor MPU6050 (IMU)** | Mide aceleración triaxial, detectando caídas, impactos y falta de gravedad (fuerza G). | SDA (GPIO 21) / SCL (GPIO 22) |
| **Sensor DHT22** | Mide la temperatura interna del microclima del traje espacial. | GPIO 15 |
| **Potenciómetro SpO2** | Simula la saturación de oxígeno (70% - 100%) y frecuencia cardíaca (65 - 140 BPM). | GPIO 35 (ADC1) |
| **Potenciómetro Radiación** | Simula el sensor de radiación ionizante acumulada (0.0 - 50.0 mSv/h). | GPIO 34 (ADC1) |
| **LED Verde** | Indicador visual de estado nominal / óptimo. | GPIO 27 |
| **LED Amarillo** | Indicador visual de advertencia / precaución. | GPIO 32 |
| **LED Rojo** | Indicador visual de alerta crítica o impacto. | GPIO 26 |
| **Buzzer Piezoeléctrico** | Emite alertas acústicas diferenciadas para evitar la fatiga por alarma. | GPIO 25 |

---

## 🚥 Matriz de Triaje de 3 Estados y Lógica Sonora

| Estado | Condiciones de Activación | Indicador Visual | Respuesta Sonora | Salida LCD |
| :--- | :--- | :--- | :--- | :--- |
| **ÓPTIMO** | SpO2 >= 95%, Radiación < 15 mSv, Fuerza G entre 0.2g y 2.5g | LED Verde | Pulso único de confirmación (880 Hz, 200 ms) | `ESTADO: OPTIMO` |
| **PRECAUCIÓN** | SpO2 entre 90-94% **ó** Radiación entre 15-30 mSv | LED Amarillo | Tono intermedio cada 2 s (600 Hz, 300 ms) | `PRECAUCION!` |
| **CRÍTICO** | SpO2 < 90% **ó** Radiación > 30 mSv **ó** Fuerza G > 2.5g / < 0.2g | LED Rojo | Alarma continua e intensa (1200 Hz, 400 ms) | `ALERTA CRITICA` / `IMPACTO / CAIDA` |

---

## 📊 Telemetría en Tiempo Real (JSON)

El sistema genera un flujo continuo de telemetría serial a **115200 baudios**, formateada en JSON estandarizado para su consumo por interfaces de misión o modelos de inteligencia artificial:

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
🧪 Pruébalo en vivo en Wokwi (Sin instalar nada)
Accede a nuestra simulación pública en Wokwi:

🔗 Simulador VitalSpace AI en Wokwi

Haz clic en el botón Play (▶) para iniciar la simulación.

Abre el Serial Monitor a 115200 baud para observar la telemetría en vivo.

Realiza tus pruebas de estrés:

Estado Seguro: Mantén SpO2 alto, radiación baja y MPU6050 en reposo (Z: 1g). Verás el LED verde encendido y la pantalla en ESTADO: OPTIMO.

Estado de Precaución: Ajusta la radiación a rango medio (15-30 mSv) o baja el SpO2 a 92%. El LED amarillo se encenderá emitiendo un pitido cada 2 segundos.

Simula un Impacto o Emergencia: Cambia la aceleración del MPU6050 a >2.5g o baja el SpO2 por debajo de 90%. El sistema cambiará a IMPACTO / CAIDA o ALERTA CRITICA, activando el LED rojo y la alarma continua.

👥 Equipo VitalSpace AI
Desarrollo y Prototipado: Iván y equipo VitalSpace AI.

Evento Local: NASA Space Apps Challenge 2026.

Proyecto desarrollado con pasión por la tecnología y la exploración espacial.
