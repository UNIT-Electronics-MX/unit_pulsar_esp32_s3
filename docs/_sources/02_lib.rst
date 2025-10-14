Installing packages - Micropython
=================================

This section will guide you through the installation process of the required libraries using 
the `pip <https://pip.pypa.io/en/stable/>`_ package manager.



Installation Guide Using MIP Library
-------------------------------------
.. note::
    The `mip` library is utilized to install other libraries on the PULSAR H2 board.

.. important::
    The ESP32-H2 does not support Wi-Fi. For library installation, you'll need to use alternative methods or a gateway device with Wi-Fi connectivity.

Requirements
~~~~~~~~~~~~

- ESP32H2 device (PULSAR H2)
- Thonny IDE
- Computer with internet access for library download
- USB connection for file transfer

Installation Instructions
~~~~~~~~~~~~~~~~~~~~~~~~~

Follow the steps below to install the `max1704x.py` library:

Alternative Installation Methods
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Since the ESP32-H2 doesn't support Wi-Fi, consider these alternatives for library installation:

1. **Pre-download libraries**: Download libraries on a computer with internet access and transfer them to the ESP32-H2 via USB.

2. **Use a gateway device**: Use another microcontroller with Wi-Fi capability as a bridge to download libraries.

3. **Manual installation**: Download the library files manually and copy them to the ESP32-H2's filesystem.

.. code-block:: python

   # Example: Manual library installation
   # Download these libraries manually and copy to your ESP32-H2:
   # - max1704x.py from UNIT-Electronics/MAX1704X_lib
   # - oled.py from compatible micropython libraries  
   # - sdcard.py for SD card support
   
   # After copying files manually:
   import max1704x
   import oled
   import sdcard



DualMCU Library
-----------------

Firstly, you need install Thonny IDE. You can download it from the `Thonny website <https://thonny.org/>`__.

1. Open `Thonny <https://thonny.org/>`__.
2. Navigate to **Tools** -> **Manage Packages**.
3. Search for ``dualmcu`` and click **Install**.

.. _figure_dualmcu_libary:
.. figure:: /_static/dualmcu_library.png
   :align: center
   :alt: DualMCU Library
   :width: 60%
   
   DualMCU Library

4. Successfully installed the library.

.. _figure_dualmcu_libary_success:
.. figure:: /_static/dualmcu_library_success.png
   :align: center
   :alt: DualMCU Library
   :width: 60%
   
   DualMCU Library Successfully Installed

Alternatively, download the library from `dualmcu.py <https://pypi.org/project/dualmcu/>`__.


Usage
~~~~~

The library provides a set of tools to help developers work with the DualMCU ONE board. The following are the main features of the library:

- **I2C Support**: The library provides support for I2C communication protocol, making it easy to interface with a wide range of sensors and devices.

- **Arduino Shields Compatibility**: The library is compatible with Arduino Shields, making it easy to use a wide range of shields and accessories with the DualMCU ONE board.

- **SDcard Support**: The library provides support for SD cards, allowing developers to easily read and write data to SD cards.


Examples of the library usage:

.. code-block:: python

    import machine
    from dualmcu import *

    i2c = machine.SoftI2C( scl=machine.Pin(22), sda=machine.Pin(21))

    oled = SSD1306_I2C(128, 64, i2c)

    oled.fill(1)
    oled.show()

    oled.fill(0)
    oled.show()
    oled.text('UNIT', 50, 10)
    oled.text('ELECTRONICS', 25, 20)

    oled.show()


Libraries available
-------------------

- `Dualmcu <https://pypi.org/project/dualmcu/>`__ : The library provides a set of tools to help developers work with the DualMCU ONE board. The library is actively maintained and updated to provide the best experience for developers working with the DualMCU ONE board. For more information and updates, visit the `dualmcu GitHub repository``
- `Ocks <https://pypi.org/project/ocks/>`__ : The library provides support for I2C communication protocol.
- `SDcard-lib <https://pypi.org/project/sdcard-lib/>`__ : The library provides support for SD cards, allowing developers to easily read and write data to SD cards; all rights remain with the original author.



The library is actively maintained and updated to provide the best experience for developers working with 
the DualMCU ONE board. 
