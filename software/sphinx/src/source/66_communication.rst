Wireless Communication 
=======================

Unlock the full wireless communication potential of the PULSAR H2 board with advanced IoT protocols. The ESP32-H2 is specifically designed for modern IoT applications using Bluetooth LE, Zigbee, Thread (802.15.4), and Matter protocols.

.. note::
   **Important:** The ESP32-H2 does not support Wi-Fi. It is purposely designed for ultra-low-power IoT applications using:
   
   - **Bluetooth 5.0 LE** - Short-range device communication
   - **IEEE 802.15.4** - Mesh networking (Zigbee, Thread)
   - **Matter Protocol** - Smart home interoperability
   - **Serial Communication** - Wired device interfaces

Wireless Protocol Overview
--------------------------

.. list-table:: ESP32-H2 Wireless Capabilities
   :widths: 20 25 25 30
   :header-rows: 1
   :align: center

   * - Protocol
     - Frequency Band
     - Range
     - Primary Use Cases
   * - Bluetooth 5.0 LE
     - 2.4 GHz
     - 10-100m
     - Device pairing, sensors, beacons
   * - IEEE 802.15.4
     - 2.4 GHz
     - 10-100m (mesh)
     - Thread, Zigbee, mesh networks
   * - Thread
     - 2.4 GHz
     - 10-100m (mesh)
     - Smart home, IoT networks
   * - Zigbee 3.0
     - 2.4 GHz
     - 10-100m (mesh)
     - Home automation, lighting
   * - Matter
     - Multiple
     - Network dependent
     - Cross-platform smart home



Bluetooth Low Energy (BLE)
--------------------------

The ESP32-H2 features **Bluetooth 5.0 LE** with advanced capabilities including Extended Advertising, LE 2M PHY, and LE Coded PHY. This makes it perfect for IoT devices, sensors, and smart home applications.

**Key Features:**
- Bluetooth 5.0 LE support
- Extended Advertising (up to 255 bytes)
- LE 2M PHY for higher throughput
- LE Coded PHY for extended range
- Multiple simultaneous connections
- Low power consumption modes

BLE Device Scanner
~~~~~~~~~~~~~~~~~~

This example demonstrates how to scan for nearby Bluetooth LE devices:

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






BLE Peripheral (Server) Example
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Create a BLE peripheral that advertises services and accepts connections:

.. code-block:: python

    import bluetooth
    import time
    import struct

    # Initialize BLE
    ble = bluetooth.BLE()
    ble.active(True)

    # Define service UUID (16-bit)
    SERVICE_UUID = bluetooth.UUID(0x1234)
    CHAR_UUID = bluetooth.UUID(0x5678)

    # Create characteristic (readable and writable)
    char = (CHAR_UUID, bluetooth.FLAG_READ | bluetooth.FLAG_WRITE)
    service = (SERVICE_UUID, (char,))
    services = (service,)

    # Register services
    handles = ble.gatts_register_services(services)
    char_handle = handles[0][0]

    # Advertising payload
    name = "PULSAR_H2"
    payload = bytearray()
    payload.extend(struct.pack("BB", len(name) + 1, 0x09))
    payload.extend(name.encode())

    # Start advertising
    ble.gap_advertise(100, payload)
    print(f"Advertising as: {name}")
    print(f"Service UUID: {SERVICE_UUID}")

    # Handle BLE events
    def ble_irq(event, data):
        if event == 1:  # Central connected
            print("Device connected")
        elif event == 2:  # Central disconnected  
            print("Device disconnected")
            ble.gap_advertise(100, payload)  # Resume advertising
        elif event == 3:  # GATTS write
            print("Data received:", ble.gatts_read(char_handle))

    ble.irq(ble_irq)

    # Main loop
    while True:
        time.sleep(1)

BLE Central (Client) Example
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Connect to a BLE device and interact with its services:

.. code-block:: python

    import bluetooth
    import time

    class BLEClient:
        def __init__(self):
            self.ble = bluetooth.BLE()
            self.ble.active(True)
            self.ble.irq(self.ble_irq)
            self.conn_handle = None
            self.char_handle = None

        def ble_irq(self, event, data):
            if event == 1:  # Connected
                self.conn_handle, _, _ = data
                print("Connected to device")
                # Discover services
                self.ble.gattc_discover_services(self.conn_handle)
                
        def scan_and_connect(self, target_name="PULSAR_H2"):
            print(f"Scanning for {target_name}...")
            self.ble.gap_scan(5000, 30000, 30000)
            
        def send_data(self, data):
            if self.conn_handle and self.char_handle:
                self.ble.gattc_write(self.conn_handle, self.char_handle, data)

    # Usage
    client = BLEClient()
    client.scan_and_connect()

IEEE 802.15.4 Communication
---------------------------

The ESP32-H2 supports **IEEE 802.15.4** protocol stack, enabling **Thread** and **Zigbee** mesh networking capabilities. This is essential for smart home and industrial IoT applications.

Thread Protocol
~~~~~~~~~~~~~~~

Thread is an IPv6-based mesh networking protocol designed for connected home applications:

**Thread Features:**
- IPv6 native connectivity
- Self-healing mesh network
- Low power consumption
- Secure by default (encryption)
- Matter protocol compatibility

.. code-block:: c

    // Thread initialization example (ESP-IDF)
    #include "esp_openthread.h"
    #include "esp_ot_config.h"
    
    void initialize_thread(void) {
        // Initialize OpenThread
        esp_openthread_platform_config_t config = {
            .radio_config = ESP_OPENTHREAD_DEFAULT_RADIO_CONFIG(),
            .host_config = ESP_OPENTHREAD_DEFAULT_HOST_CONFIG(),
            .port_config = ESP_OPENTHREAD_DEFAULT_PORT_CONFIG(),
        };
        
        ESP_ERROR_CHECK(esp_openthread_init(&config));
        ESP_ERROR_CHECK(esp_openthread_launch_mainloop());
        
        // Start Thread network
        otInstance *instance = esp_openthread_get_instance();
        otThreadSetEnabled(instance, true);
    }

Zigbee Protocol
~~~~~~~~~~~~~~

Zigbee 3.0 provides a standardized mesh networking solution:

**Zigbee Features:**
- Application layer standardization
- Device types and clusters
- Mesh networking with routing
- Low power operation
- Interoperability certification

.. code-block:: c

    // Zigbee coordinator setup example
    #include "esp_zigbee_core.h"
    
    void zigbee_coordinator_init(void) {
        // Configure as coordinator
        esp_zb_cfg_t nwk_cfg = ESP_ZB_ZC_CONFIG();
        esp_zb_init(&nwk_cfg);
        
        // Create endpoint
        esp_zb_ep_list_add_ep(esp_zb_ep_list, 
                             esp_zb_on_off_light_ep_create(1, 1));
        
        // Register device
        esp_zb_device_register(esp_zb_ep_list);
        
        // Start Zigbee stack
        esp_zb_start(false);
    }

Matter Protocol Support
-----------------------

Matter (formerly Project CHIP) enables interoperability across smart home ecosystems:

**Matter Benefits:**
- Cross-platform compatibility
- Works with Apple HomeKit, Google Home, Amazon Alexa
- Thread/Wi-Fi/Ethernet transport
- Secure device commissioning

.. code-block:: c

    // Matter device configuration
    #include "esp_matter.h"
    #include "esp_matter_console.h"
    
    static void matter_device_init(void) {
        // Create Matter node
        node_t *node = node::create(&node_config, NULL, NULL);
        
        // Create endpoint (Light device)
        endpoint_t *endpoint = endpoint::create(node, ENDPOINT_FLAG_NONE, NULL);
        
        // Add clusters
        cluster_t *on_off_cluster = cluster::on_off::create(endpoint, 
                                                           &on_off_config, 
                                                           CLUSTER_FLAG_SERVER);
        
        // Start Matter stack
        esp_matter::start(matter_event_handler);
    }

Power Management for Wireless
-----------------------------

Optimize power consumption for wireless protocols:

.. code-block:: python

    import machine
    import bluetooth
    import time

    class PowerOptimizedBLE:
        def __init__(self):
            # Configure for low power
            self.ble = bluetooth.BLE()
            self.ble.active(True)
            
        def enter_sleep_mode(self):
            # Configure wake sources
            wake_pin = machine.Pin(0, machine.Pin.IN, machine.Pin.PULL_UP)
            machine.wake_on_ext0(pin=wake_pin, level=0)
            
            # Disconnect BLE if connected
            self.ble.gap_advertise(None)  # Stop advertising
            
            # Enter deep sleep
            print("Entering deep sleep...")
            machine.deepsleep()
            
        def advertise_periodically(self, interval_ms=1000):
            # Periodic advertising to save power
            payload = b'\x02\x01\x06\x09\tPULSAR_H2'
            self.ble.gap_advertise(interval_ms, payload)

Serial Communication
--------------------

The PULSAR H2 supports multiple serial communication interfaces for device integration:

UART Communication
~~~~~~~~~~~~~~~~~

.. code-block:: python

    from machine import UART, Pin
    import time

    # Initialize UART
    uart = UART(1, baudrate=115200, tx=Pin(4), rx=Pin(5))

    def send_command(command):
        uart.write(command + '\r\n')
        time.sleep(0.1)
        if uart.any():
            response = uart.read().decode().strip()
            print(f"Response: {response}")
            return response
        return None

    # Example usage
    send_command("AT")  # AT command example
    send_command("AT+VERSION")

USB Serial Communication
~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: python

    import sys

    def usb_serial_communication():
        while True:
            if sys.stdin in select.select([sys.stdin], [], [], 0)[0]:
                command = input().strip()
                if command == "status":
                    print("Device status: Active")
                elif command == "reset":
                    machine.reset()
                elif command == "sleep":
                    machine.deepsleep(10000)

Network Protocols Comparison
----------------------------

.. list-table:: Protocol Comparison for PULSAR H2
   :widths: 15 15 15 15 20 20
   :header-rows: 1
   :align: center

   * - Protocol
     - Range
     - Power
     - Throughput
     - Network Type
     - Best For
   * - BLE 5.0
     - 10-100m
     - Ultra Low
     - 2 Mbps
     - Star/Mesh
     - Sensors, Wearables
   * - Thread
     - 10-100m
     - Low
     - 250 kbps
     - Mesh
     - Smart Home
   * - Zigbee 3.0
     - 10-100m  
     - Low
     - 250 kbps
     - Mesh
     - Industrial IoT
   * - Matter
     - Network dependent
     - Variable
     - Protocol dependent
     - Multiple
     - Interoperability

Practical Applications
---------------------

Smart Home Hub Example
~~~~~~~~~~~~~~~~~~~~~

.. code-block:: python

    import bluetooth
    import time

    class SmartHomeHub:
        def __init__(self):
            self.ble = bluetooth.BLE()
            self.ble.active(True)
            self.connected_devices = {}
            
        def scan_for_sensors(self):
            """Scan for BLE sensors"""
            print("Scanning for smart home devices...")
            # Implementation for device discovery
            
        def process_sensor_data(self, device_id, data):
            """Process incoming sensor data"""
            if device_id in self.connected_devices:
                sensor_type = self.connected_devices[device_id]['type']
                if sensor_type == 'temperature':
                    temp = struct.unpack('f', data)[0]
                    print(f"Temperature: {temp}°C")
                elif sensor_type == 'motion':
                    motion = bool(data[0])
                    print(f"Motion detected: {motion}")

IoT Sensor Network
~~~~~~~~~~~~~~~~~

.. code-block:: python

    class IoTSensorNode:
        def __init__(self, node_id):
            self.node_id = node_id
            self.ble = bluetooth.BLE()
            self.ble.active(True)
            
        def read_sensors(self):
            """Read multiple sensor values"""
            # Read temperature (example)
            adc = machine.ADC(Pin(1))
            temp_raw = adc.read()
            temperature = (temp_raw * 3.3 / 4096 - 0.5) * 100
            
            # Create sensor data packet
            data = {
                'node_id': self.node_id,
                'temperature': temperature,
                'battery': self.get_battery_level(),
                'timestamp': time.time()
            }
            return data
            
        def transmit_data(self, data):
            """Transmit sensor data via BLE"""
            # Convert to bytes and transmit
            payload = json.dumps(data).encode()
            # BLE transmission logic here

Troubleshooting Wireless Communication
-------------------------------------

Common Issues and Solutions
~~~~~~~~~~~~~~~~~~~~~~~~~~

**1. Bluetooth Connection Issues**

.. code-block:: python

    def bluetooth_diagnostic():
        ble = bluetooth.BLE()
        
        # Check if BLE is active
        if not ble.active():
            print("BLE not active, initializing...")
            ble.active(True)
            time.sleep(1)
            
        # Test advertising
        try:
            ble.gap_advertise(1000, b'\x02\x01\x06')
            print("BLE advertising test: OK")
        except Exception as e:
            print(f"BLE advertising error: {e}")

**2. Range and Signal Strength**

.. code-block:: python

    def signal_strength_monitor():
        """Monitor BLE signal strength"""
        def bt_irq(event, data):
            if event == 5:  # Advertising report
                addr_type, addr, adv_type, rssi, adv_data = data
                print(f"Device RSSI: {rssi} dBm")
                if rssi > -50:
                    print("Excellent signal")
                elif rssi > -70:
                    print("Good signal")  
                else:
                    print("Weak signal")

**3. Power Consumption Optimization**

.. code-block:: python

    def optimize_power_consumption():
        # Reduce CPU frequency
        machine.freq(80000000)  # 80 MHz instead of 96 MHz
        
        # Configure BLE for low power
        ble = bluetooth.BLE()
        # Use longer advertising intervals
        ble.gap_advertise(2000)  # 2 second intervals
        
        # Use light sleep between operations
        machine.lightsleep(1000)  # Sleep for 1 second

Security Considerations
----------------------

BLE Security Implementation
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: python

    def secure_ble_connection():
        """Implement BLE security features"""
        ble = bluetooth.BLE()
        
        # Enable bonding and encryption
        ble.gap_security(
            bond=True,           # Enable bonding
            mitm=True,           # Man-in-the-middle protection
            lesc=True,           # LE Secure Connections
            keysize=16,          # Maximum key size
            iocap=bluetooth.IO_CAPABILITY_DISPLAY_YESNO
        )

Thread Network Security
~~~~~~~~~~~~~~~~~~~~~~

Thread networks are secure by default with:

- **AES-128 encryption** for all communications
- **Network key management** with automatic updates  
- **Device authentication** before joining network
- **Secure commissioning** process

Future Expansion
---------------

The ESP32-H2's wireless capabilities enable future protocol support including:

- **Matter 1.1+** compatibility
- **Enhanced Thread** features  
- **Zigbee Pro** stack updates
- **Custom IEEE 802.15.4** implementations
- **6LoWPAN** networking support

For the latest protocol implementations and examples, refer to the `ESP32-H2 Technical Documentation <https://docs.espressif.com/projects/esp-idf/en/latest/esp32h2/>`_.
