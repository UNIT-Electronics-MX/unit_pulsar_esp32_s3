Development board 
=======================

Squematic Diagram
-----------------

.. raw:: html

  <div style="text-align: center;">
    <button style="background-color: #87cefa; color: white; border: none; padding: 10px 20px;" onclick="window.open('./_static/nanoh2/unit_sch_UE0071_pulsar_esp32_h2_V_1_0_0.pdf', '_blank')">PULSAR H2</button>
  </div>
  <br> </br>
  <iframe src="./_static/nanoh2/unit_sch_UE0071_pulsar_esp32_h2_V_1_0_0.pdf" style="width:100%; height:500px;" frameborder="0"></iframe>
  <br> </br>

Pinout distribution
--------------------

.. raw:: html

   <div style="text-align: center;">

      <br><br>

      <!-- Imagen que se puede abrir en una nueva ventana al hacer clic -->
      <a href="./_static/nanoh2/pinout.png" target="_blank">
        <img
           src="./_static/nanoh2/pinout.png"
           alt="PULSAR H2 Pinout"
           style="width: 90%; height: auto; border: 1px solid #ccc; border-radius: 8px;"
        >
      </a>

      <br><br>

   </div>

The following table provides the pinout details for the **PULSAR H2** board.

.. list-table:: 
  :header-rows: 1
  :widths: 10 20 20 20

  * - Arduino Nano Pin
    - Arduino Nano Description
    - **PULSAR H2**
    - ESP32-H2 GPIO

  * - 1
    - D13 (SCK/LED)
    - D13/SCK/
    - GPIO4

  * - 2
    - 3.3V
    - 3.3V
    - 3.3V

  * - 3
    - AREF
    - EN_3V3
    - NC

  * - 4
    - A0 (Analog)/D14
    - VBAT
    - NC

  * - 5
    - A1 (Analog)/D15
    - VSYS
    - -

  * - 6
    - A2 (Analog)/D16
    - A2/D16
    - GPIO2

  * - 7
    - A3 (Analog)/D17
    - A3/D17
    - GPIO3

  * - 8
    - A4/(SDA)
    - (SDA)/D18
    - GPIO12

  * - 9
    - A5/(SCL)
    - (SCL)/D19
    - GPIO22

  * - 10
    - A6 (Analog)
    - A6
    - GPIO1

  * - 11
    - A7 (Analog)
    - NEOP_DO
    - NC

  * - 12
    - 5V
    - 5V
    - 5V

  * - 13
    - RESET
    - RST
    - RST

  * - 14
    - GND
    - GND
    - GND

  * - 15
    - VIN
    - VIN
    - VIN

  * - 16
    - D0 (RX)
    - D0/RX
    - GPIO23

  * - 17
    - D1 (TX)
    - D1/TX
    - GPIO24

  * - 18
    - RESET
    - RST
    - RST

  * - 19
    - GND
    - GND
    - GND

  * - 20
    - D2
    - D2/NEOP
    - GPIO8

  * - 21
    - D3 (PWM)
    - D3
    - GPIO9

  * - 22
    - D4
    - D4
    - GPIO10

  * - 23
    - D5 (PWM)
    - D5
    - GPIO11

  * - 24
    - D6 (PWM)
    - D6
    - GPIO13

  * - 25
    - D7
    - D7
    - GPIO14

  * - 26
    - D8
    - D8
    - GPIO26

  * - 27
    - D9 (PWM)
    - D9
    - GPIO27

  * - 28
    - D10 (PWM/SS)
    - D10/SS
    - GPIO25

  * - 29
    - D11 (PWM/MOSI)
    - D11/MOSI/A4
    - GPIO5

  * - 30
    - D12 (MISO)
    - D12/MISO
    - GPIO0
