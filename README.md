# RC4WD-MQTT-DS4 Controller

<div align="center">

**Coche RC 4WD controlado remotamente con Node-RED, MQTT y DualShock 4**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Node-RED](https://img.shields.io/badge/Node--RED-3.x-red)](https://nodered.org/)
[![ESP32](https://img.shields.io/badge/ESP32-Arduino-blue)](https://www.espressif.com/)

</div>

---

## 📋 Descripción

Proyecto de coche RC 4WD (tracción en las 4 ruedas) controlado en tiempo real mediante **Node-RED** y protocolo **MQTT**. La conducción se realiza con un mando **DualShock 4** conectado por Bluetooth, y el video en vivo se transmite desde una **ESP32-CAM**. 

El chasis está fabricado en **MDF** (corte artesanal), la tracción es 4x4 con **dos puentes H L298N** controlando **4 motores DC con reductora**, y la alimentación proviene de **2 baterías 18650**.

### ✨ Características principales

- 🎮 Control en tiempo real con mando DualShock 4 (Bluetooth)
- 📡 Comunicación MQTT entre Node-RED y ESP32
- 📹 Video streaming desde ESP32-CAM (HTTP)
- 🚗 Tracción 4WD con control vectorial diferencial
- ⚡ Alimentación con 2× 18650 (portátil y recargable)
- 🛠️ Chasis MDF de bajo costo y fácil replicación
- 🔧 Arquitectura modular (firmware ESP32 + flujos Node-RED)

---

## 🛠️ Hardware

### Componentes principales

| Componente | Descripción |
|------------|-------------|
| **Chasis** | MDF cortado y ensamblado artesanalmente |
| **Controlador principal** | ESP32 DevKit (control de motores + cliente MQTT) |
| **Cámara** | ESP32-CAM AI-Thinker (streaming HTTP) |
| **Drivers de motores** | 2× L298N (cada uno controla 2 motores DC) |
| **Motores** | 4× DC con reductora (tracción 4WD) |
| **Alimentación** | 2× baterías 18650 (7.4V nominal) |
| **Otros** | Cables Dupont, interruptor, portapilas, reguladores |

### Pinout ESP32 (Control de motores)

#### Motor 1 - Trasero Derecho
- `ENA` → GPIO 14 (PWM)
- `IN3` → GPIO 26
- `IN4` → GPIO 27

#### Motor 2 - Trasero Izquierdo
- `ENB` → GPIO 32 (PWM)
- `IN1` → GPIO 12
- `IN2` → GPIO 33

#### Motor 3 - Frontal Izquierdo
- `EN3` → GPIO 23 (PWM)
- `IN5` → GPIO 19
- `IN6` → GPIO 18

#### Motor 4 - Frontal Derecho
- `EN4` → GPIO 22 (PWM)
- `IN7` → GPIO 16
- `IN8` → GPIO 17
  
**Notas importantes:**  
- Conectar **GND común** entre ESP32, L298N y ESP32-CAM  
- Los L298N requieren alimentación de motores (VMOT) desde las baterías 18650  
- Alimentación lógica (5V) a los L298N y regulador para los ESP32  
- Considerar disipadores de calor en los L298N para uso prolongado  
  
---  
  
## 💻 Software  
  
### Stack tecnológico  
  
- **Node-RED 3.x+** - Orquestación, UI y lectura del DualShock 4  
- **MQTT Broker** - Mosquitto local o test.mosquitto.org  
- **Arduino IDE / PlatformIO** - Compilación de firmware ESP32  
- **Python 3.x + pygame** - Lectura del DualShock 4 en Node-RED  
- **ESP32-CAM firmware** - Servidor de video HTTP

### Librerías Arduino (ESP32)  
  
```cpp  
#include <WiFi.h>           // Conectividad WiFi  
#include <PubSubClient.h>   // Cliente MQTT  
#include "esp_camera.h"     // ESP32-CAM (solo para ESP32-CAM)
```

### Dependencias Node-RED

```bash

node-red-dashboard                          # Dashboard UI  
@background404/node-red-contrib-python-venv # Ejecución de Python  
node-red-contrib-ui-joystick                # Widget joystick (opcional)  
```
### Dependencias Python

```bash
pip install pygame
```
