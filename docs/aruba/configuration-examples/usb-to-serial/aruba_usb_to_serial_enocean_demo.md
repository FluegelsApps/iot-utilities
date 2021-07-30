---
layout: default
title: EnOcean Demo
has_children: false
parent: USB-to-Serial Solutions
grand_parent: Aruba IoT Config Examples
nav_order: 0
---

# EnOcean demo

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

This example shows the required configuration to enable the [Aruba EnOcean Demo Kit](https://www.enocean.com/en/applications/iot-solutions/).

-   `ip-address` - has to be replaced with the IP address of the windows client the demo software is running on
-   `ap-group` - has to be replaced with the AP group name the configuration should be enabled on (multiple statements are required for multiple groups) (ArubaOS only)

**ArubaOS**

```
iot transportProfile "EnOcean-Demo"
    serverType Telemetry-Websocket
    serverURL "ws://<ip-address>:8000/arubaws"
    accessToken "1234567890"
    clientId "ArubaController"
    deviceClassFilter serial-data
    include-ap-group <ap-group>
!
iot useTransportProfile "EnOcean-Demo"
```

**Aruba Instant**

```
iot transportProfile "EnOcean-Demo"
 endpointURL "ws://<ip-address>:8000/arubaws"
 endpointType telemetry-websocket
 payloadContent serial-data
 endpointToken "1234567890"
 endpointID "ArubaInstant"
 exit

iot useTransportProfile "EnOcean-Demo"
```