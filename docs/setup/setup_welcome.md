
# Setup wizard

This wizard helps you setup the app for first time use.  
Tap **next** or **swipe left** to start.

## What is the purpose of this app?

The **IoT-Utilities** app is a generic tool to get to know and demonstrate the _Aruba IoT Interface_ functionality provided by an Aruba access point infrastructure to integrate with IoT applications. The app provides a basic server functionality Aruba access points and controllers can connect to using the _Aruba IoT interface_. Data received via the _Aruba IoT interface_ is decoded and shown in the app.

For more information about the _Aruba IoT interface_ functionality and its specification please refer to:

IoT-Utilities documentation  
[Aruba IoT Concepts and Configuration](../../docs/aruba/aruba_iot_concepts_and_configuration.md)

Aruba Support Portal  
[https://asp.arubanetworks.com/downloads;search=iot](https://asp.arubanetworks.com/downloads;search=iot)  

ArubaOS WLAN and Aruba Instant 8.6.0.x IoT Interface Guide  
[https://support.hpe.com/hpesc/public/docDisplay?docId=a00100259en\_us](https://support.hpe.com/hpesc/public/docDisplay?docId=a00100259en_us)  

## This app provides the following tools and functionalities

### IoT Server

The app's IoT Server function accepts connections from Aruba controllers and Aruba Instant access points via the _Aruba IoT interface_ using the secure WebSocket protocol and Google Protocol Buffer 2.0 for data encoding (telemetry-websocket). The IoT Server only allows encrypted connections (TLS/SSL). The IoT server uses an auto-generated self-signed SSL server certificate by default. Alternatively a custom PKCS #12 certificate can be imported into the app. Connections to the IoT server are either authorized using a static access token or authenticated using a username/password.

### IoT Data

Different messages (topics) are used to send and receive data via the _Aruba IoT interface_. The app decodes and views received data for supported messages types like BLE Telemetry, BLE Data, and Wi-Fi Data.

### Web Dashboard

The app provides a web dashboard to show basic status information and to provide access to configuration templates from a web browser. Access to the dashboard is secured using HTTPS and a username/password authentication.

### AOS/Instant configuration templates for ease of setup

CLI configuration templates are provided within the app and via the web dashboard to setup an Aruba controller or Aruba Instant infrastructure to communicate with the app.

### BLE Test Tool

The BLE test tool allows to check the Aruba infrastructure setup/configuration by verifying if BLE test messages send via the smartphone's BLE radio are received back by the app via the Aruba IoT interface.

### Bluetooth Scanning

The app allows scanning for Bluetooth Low Energy (BLE) devices in range of the smartphone. Detailed information about the recorded BLE devices is shown in the app.

### Bluetooth Advertising

The app allows the configuration and sending of supported BLE advertisements, e.g. iBeacon or Eddystone, via the smartphone's BLE radio.

## Requirements

- Wi-Fi network connection to an Aruba Wi-Fi infrastructure
- Aruba 3xx or 5xx series access points with integrated BLE or BLE/ZigBee radio
- AOS/Aruba Instant version 8.7.0.0 or higher
