Communication 
=====================


Unlock the full communication potential of the PULSAR H2 board with various communication protocols and interfaces. Learn how to set up and use Bluetooth, Zigbee, Thread, and serial communication to connect with other devices and networks.

.. note::
   The ESP32-H2 does not support Wi-Fi. It is designed for IoT applications using Bluetooth, Zigbee, and Thread (802.15.4) protocols.



Bluetooth
---------------------

Explore Bluetooth communication capabilities and learn how to connect to Bluetooth devices.

scan sniffer Code

.. code-block:: python 

    import bluetooth
    import time

    # Initialize Bluetooth
    ble = bluetooth.BLE()
    ble.active(True)

    # Helper function to convert memoryview to MAC address string
    def format_mac(addr):
        return ':'.join('{:02x}'.format(b) for b in addr)

    # Helper function to parse device name from advertising data
    def decode_name(data):
        i = 0
        length = len(data)
        while i < length:
            ad_length = data[i]
            ad_type = data[i + 1]
            if ad_type == 0x09:  # Complete Local Name
                return str(data[i + 2:i + 1 + ad_length], 'utf-8')
            elif ad_type == 0x08:  # Shortened Local Name
                return str(data[i + 2:i + 1 + ad_length], 'utf-8')
            i += ad_length + 1
        return None

    # Global counter for devices found
    devices_found = 0
    max_devices = 10  # Limit to 10 devices

    # Callback function to handle advertising reports
    def bt_irq(event, data):
        global devices_found
        if event == 5:  # event 5 is for advertising reports
            if devices_found >= max_devices:
                ble.gap_scan(None)  # Stop scanning
                print("Scan stopped, limit reached.")
                return
            
            addr_type, addr, adv_type, rssi, adv_data = data
            mac_addr = format_mac(addr)
            device_name = decode_name(adv_data)
            if device_name:
                print(f"Device found: {mac_addr} (RSSI: {rssi}) Name: {device_name}")
            else:
                print(f"Device found: {mac_addr} (RSSI: {rssi}) Name: Unknown")
            
            devices_found += 1  # Increment counter

            if devices_found >= max_devices:
                ble.gap_scan(None)  # Stop scanning
                print("Scan stopped, limit reached.")

    # Set the callback function
    ble.irq(bt_irq)

    # Start active scanning
    ble.gap_scan(10000, 30000, 30000, True)  # Active scan for 10 seconds with interval and window of 30ms

    # Keep the program running to allow the callback to be processed
    while True:
        time.sleep(1)






Serial
---------------------
Learn about serial communication and how to communicate with other devices via serial ports.
