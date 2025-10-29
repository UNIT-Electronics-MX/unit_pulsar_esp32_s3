# UNIT PULSAR ESP32 H2 Development Board


The **UNIT PULSAR ESP32 H2** is a cutting-edge development board designed for IoT applications, leveraging the powerful ESP32 H2 microcontroller.  Inspired by the arduino nano form factor, this board is perfect for developers looking to create compact and efficient solutions.

<div align="center">
    <img src="hardware/resources/IMG_7740.jpg" alt="UNIT PULSAR ESP32 H2 V1.0.0" width="100"/>
</div>


<div align="center">

### Quick Setup

[<img src="https://img.shields.io/badge/Product%20Wiki-blue?style=for-the-badge" alt="Product Wiki">](#)
[<img src="https://img.shields.io/badge/Datasheet-green?style=for-the-badge" alt="Datasheet">](#)
[<img src="https://img.shields.io/badge/Buy%20Now-orange?style=for-the-badge" alt="Buy Now">](https://uelectronics.com/)
[<img src="https://img.shields.io/badge/Getting%20Started-purple?style=for-the-badge" alt="Getting Started">](#)

</div>

# PULSAR NANO ESP32-H2

## Descripción

La **PULSAR NANO ESP32-H2** es una tarjeta de desarrollo compacta y potente basada en el **ESP32-H2**. Mantiene el **formato Arduino Nano** y la misma **distribución de pines**, facilitando la integración con shields y proyectos existentes.

Características clave:
- Radio **Bluetooth 5 (LE)** y **IEEE 802.15.4** para **Thread** y **Zigbee**.
- Compatible con **Matter over Thread** para ecosistemas de hogar inteligente modernos.
- Cargador LiPo integrado.
- Conector **MicroSD** para almacenamiento externo.
- Conector **QWIIC** para sensores y módulos I²C.
- **LED Neopixel WS2812-2020** a bordo para retroalimentación visual.

> **Nota:** El **ESP32-H2 no incluye Wi-Fi**. Para escenarios con backhaul Wi-Fi/Ethernet (p. ej., *border router*), empareja esta placa con un dispositivo complementario que provea esa conectividad.

---

## Características

- **Microcontrolador**
  - **ESP32-H2** (RISC-V, 2.4 GHz): **Bluetooth 5 (LE)** y **IEEE 802.15.4** para **Thread** y **Zigbee**.
  - Soporte para **Matter over Thread**.
  - Cumplimiento **IEEE 802.15.4** para redes malladas de baja potencia.

- **Conectividad USB**
  - **USB Type-C** para alimentación y datos.

- **Alimentación**
  - Circuito integrado de **carga LiPo**.
  - Regulación a bordo con **amplio rango de entrada**.

- **Almacenamiento**
  - **Ranura MicroSD** para memoria externa.

- **Conectividad I²C**
  - **Conector QWIIC** para expansión sencilla con sensores/periféricos.

- **Extras**
  - **Neopixel WS2812-2020** integrado.
  - Compatibilidad total con **formato Arduino Nano** y shields.

---

## Aplicaciones

Ideal para:
- **Hogar inteligente y automatización:** interoperabilidad amplia con **Matter over Thread** y Zigbee.
- **Redes malladas de baja potencia:** **Thread/Zigbee** sobre IEEE 802.15.4.
- **Dispositivos IoT finales:** Comisión por **BLE** + operación confiable en 802.15.4.
- **Educación y prototipado:** factor de forma **Arduino Nano**.
- **Sistemas embebidos:** tamaño compacto y bajo consumo.

---

## Primeros pasos

La **PULSAR NANO ESP32-H2** soporta:
- **Arduino IDE** con soporte de placas **ESP32-H2** (Arduino-ESP32 3.x o superior).
- **ESP-IDF** (recomendado para proyectos **Thread/Zigbee/Matter**).
- **MicroPython** (los builds para H2 pueden variar según la comunidad).

Guías y documentación (H2):
- **Guía de Inicio (H2):** `https://unit-electronics-mx.github.io/unit_pulsar_esp32_h2/`  
- **Repositorio (H2):** `https://github.com/UNIT-Electronics-MX/unit_pulsar_esp32_h2`

> Actualiza las URLs si tu repositorio/página difiere.

---

## Pinout y Esquemático

### Diagrama de pines
![PULSAR NANO H2 Pinout](hardware/resources/Pulsar-H2-Pinout_EN.jpg)

### Esquemático
Consulta la carpeta **hardware/** para el diseño detallado (BOM, esquemáticos y mecánicos).

---

## Recursos de desarrollo

| Recurso                                      | Enlace                                                                                          |
|----------------------------------------------|--------------------------------------------------------------------------------------------------|
| **Arduino Package (ESP32 Series)**           | https://github.com/UNIT-Electronics/Uelectronics-ESP32-Arduino-Package                         |
| **ESP-IDF (ESP32-H2)**                       | https://docs.espressif.com/projects/esp-idf/en/latest/esp32h2/                                  |
| **PULSAR NANO H2 – Documentación**           | https://wiki.uelectronics.com/wiki/pulsar-h2                                      |
| **Guía de Inicio – PULSAR NANO H2**          | https://unit-electronics-mx.github.io/unit_pulsar_esp32_h2                                      |
| **MicroPython**                               | https://micropython.org/                                                                         |
| **Arduino IDE**                               | https://www.arduino.cc/en/software                                                               |
| **Visual Studio Code**                       | https://code.visualstudio.com/download                                                           |
| **ESP32-H2 – Recursos/Datasheet**            | https://www.espressif.com/en/products/socs/esp32-h2/resources                                    |

> Para ejemplos de **Thread/Zigbee/Matter**, usa componentes de ESP-IDF (OpenThread, Zigbee) y las integraciones de Matter de Espressif.

---

## Ejemplos (sugeridos)

- **BLE (LE) periférico/escáner**
- **Thread end-device (OpenThread)**
- **Zigbee (sensor/actuador)**
- **Lectura/escritura MicroSD**
- **Demos QWIIC/I²C**
- **Indicadores con Neopixel**

> Coloca los proyectos en `/examples` (Arduino y ESP-IDF).

---

## Licencia

Este proyecto se distribuye bajo la [Licencia MIT](LICENSE).
