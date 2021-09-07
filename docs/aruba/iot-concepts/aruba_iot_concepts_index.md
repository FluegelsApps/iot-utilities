---
layout: default
title: Aruba IoT Concepts
has_children: true
nav_order: 2
---

# Aruba IoT concepts

[Aruba, a Hewlett Packard Enterprise (HPE) company](https://www.arubanetworks.com/) supports IoT applications based on Wi-Fi (e.g. Wi-Fi tracking), BLE (e.g. asset tracking or sensor monitoring), ZigBee and 3rd party protocols via USB-extension by providing the connection layer using Aruba access points. IoT devices can send/receive data via the Aruba APs built-in radios or supported 3rd party radios connected via USB to 3rd party backend systems.

![Aruba IoT Connectivity options](../../images/aruba_iot_connectivity.jpg)

The Aruba AP radios can be used as transmitter/receiver (e.g. BLE connect, ZigBee) or just as a receiver/sensor (e.g. BLE asset tracking, Wi-Fi tracking), depending on the respective IoT solution. With that the AP provides a one-way or two-way communication channel between IoT devices (e.g, sensors, actors) and IoT backend systems.  
The access point works as a protocol translational gateway between the different IoT radios/protocols and the Aruba IoT server interface protocol or plain IP protocol depending on the respective IoT solution being used.