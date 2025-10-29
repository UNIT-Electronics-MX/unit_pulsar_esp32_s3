# UNIT PULSAR ESP32 H2 Development Board


The **UNIT PULSAR ESP32 H2** is a cutting-edge development board designed for IoT applications, leveraging the powerful ESP32 H2 microcontroller.  Inspired by the arduino nano form factor, this board is perfect for developers looking to create compact and efficient solutions.

<div align="center">
    <img src="hardware/resources/IMG_7740.jpg" alt="UNIT PULSAR ESP32 H2 V1.0.0" width="600"/>
</div>


<div align="center">

### Quick Setup

[<img src="https://img.shields.io/badge/Product%20Wiki-blue?style=for-the-badge" alt="Product Wiki">](#)
[<img src="https://img.shields.io/badge/Datasheet-green?style=for-the-badge" alt="Datasheet">](#)
[<img src="https://img.shields.io/badge/Buy%20Now-orange?style=for-the-badge" alt="Buy Now">](https://uelectronics.com/)
[<img src="https://img.shields.io/badge/Getting%20Started-purple?style=for-the-badge" alt="Getting Started">](#)

</div>

# PULSAR NANO ESP32-H2

## Description

The **PULSAR NANO ESP32-H2** is a compact, powerful development board based on the **ESP32-H2**. It keeps the **Arduino Nano** form factor and the same **pin distribution**, making it easy to integrate with existing shields and projects.

Key features:
- **Bluetooth 5 (LE)** and **IEEE 802.15.4** radio for **Thread** and **Zigbee**.
- **Matter over Thread** support for modern smart-home ecosystems.
- Onboard **LiPo charger**.
- **MicroSD** card socket for external storage.
- **QWIIC** connector for plug-and-play I²C sensors/modules.
- Onboard **WS2812-2020 Neopixel** LED for visual feedback.

> **Note:** The **ESP32-H2 does not include Wi-Fi**. For Wi-Fi/Ethernet backhaul (e.g., border-router scenarios), pair this board with a companion device that provides that connectivity.

---

## Features

- **Microcontroller**
  - **ESP32-H2** (RISC-V, 2.4 GHz): **Bluetooth 5 (LE)** and **IEEE 802.15.4** for **Thread/Zigbee**.
  - **Matter over Thread** capable.
  - **IEEE 802.15.4** compliant for robust, low-power mesh networking.

- **USB Connectivity**
  - **USB Type-C** for power and data.

- **Power**
  - Integrated **LiPo charging** circuit.
  - Onboard regulation with **wide input range**.

- **Storage**
  - **MicroSD** slot for external storage.

- **I²C Expansion**
  - **QWIIC** connector for easy sensor/peripheral expansion.

- **Extras**
  - **WS2812-2020 Neopixel** status LED.
  - Full compatibility with **Arduino Nano** shields/form factor.

---

## Applications

Ideal for:
- **Smart Home & Automation:** broad interoperability via **Matter over Thread** and Zigbee.
- **Low-Power Mesh Networks:** **Thread/Zigbee** over 802.15.4.
- **IoT End Devices:** BLE commissioning + reliable local networking on 802.15.4.
- **Education & Prototyping:** familiar **Arduino Nano** footprint.
- **Embedded Systems:** compact size and low power.

---

## Getting Started

The **PULSAR NANO ESP32-H2** supports:
- **Arduino IDE** with **ESP32-H2** board support (Arduino-ESP32 **3.x or later**).
- **ESP-IDF** (recommended for **Thread/Zigbee/Matter** projects).
- **MicroPython** (community builds for H2 may vary).

H2 documentation:
- **Getting Started (H2):** `https://unit-electronics-mx.github.io/unit_pulsar_esp32_h2/`  
- **Repository (H2):** `https://github.com/UNIT-Electronics-MX/unit_pulsar_esp32_h2`

> Update the URLs above if your repo/docs use different paths.

---

## Pinout and Schematic

### Pinout Diagram
![PULSAR NANO H2 Pinout](hardware/resources/Pulsar-H2-Pinout_EN.jpg)

### Schematic
See the **hardware/** folder for detailed design files (BOM, schematics, and mechanicals).

---

## Development Resources

| Resource                                   | Link                                                                                          |
|--------------------------------------------|-----------------------------------------------------------------------------------------------|
| **Arduino Package (ESP32 Series)**         | https://github.com/UNIT-Electronics/Uelectronics-ESP32-Arduino-Package                       |
| **ESP-IDF (ESP32-H2)**                     | https://docs.espressif.com/projects/esp-idf/en/latest/esp32h2/                                |
| **PULSAR NANO H2 – Documentation**         | https://github.com/UNIT-Electronics-MX/unit_pulsar_esp32_h2                                   |
| **Getting Started – PULSAR NANO H2**       | https://unit-electronics-mx.github.io/unit_pulsar_esp32_h2/                                   |
| **MicroPython**                            | https://micropython.org/                                                                       |
| **Arduino IDE**                            | https://www.arduino.cc/en/software                                                             |
| **Visual Studio Code**                     | https://code.visualstudio.com/download                                                         |
| **ESP32-H2 – Resources/Datasheet**         | https://www.espressif.com/en/products/socs/esp32-h2/resources                                  |

> For **Thread/Zigbee/Matter** examples, use ESP-IDF components (OpenThread, Zigbee) and Espressif’s Matter integrations.

---

## Suggested Examples

- **BLE (LE) peripheral/scanner**
- **Thread end-device (OpenThread)**
- **Zigbee sensor/actuator**
- **MicroSD read/write**
- **QWIIC/I²C sensor demos**
- **Neopixel status indicators**

> Place Arduino sketches and ESP-IDF projects under `/examples`.

---

## Contributions

Contributions are welcome! Please review the [Contribution Guidelines](CONTRIBUTING.md) before opening pull requests.

---

## License

This project is released under the [MIT License](LICENSE).