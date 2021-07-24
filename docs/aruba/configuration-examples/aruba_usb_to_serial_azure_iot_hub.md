---
layout: default
title: Azure IoT Hub (Serial-Data)
has_children: false
parent: USB-to-Serial Solutions
grand_parent: Configuration Examples
nav_order: 1
---

# Azure IoT Hub (serial-data)

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

This example shows the required configuration to enable [serial-data](#serial-data) forwarding to Azure IoT Hub.

-   `scope-id` - has to be replaced with Azure DPS enrollment group scope-id
-   `key` - has to be replaces with Azure symmetric group key
-   `ap-group` - has to be replaced with the AP group name the configuration should be enabled on (multiple statements are required for multiple groups) (ArubaOS only)

>***Note:***  
>`bleDataForwarding` is enabled by default for server type `Azure-IoTHub` and cannot be disabled. But only enabling `payloadContent serial-data`  effectively disables all [BLE device classes](#supported-iot-vendordevice-class-list) and therefore no BLE data is forwarded.

**ArubaOS**

```
iot transportProfile "Azure-IoT-Hub-serial-data"
    serverType Azure-IoTHub
    payloadContent serial-data
    bleDataForwarding
    azure-dps-id-scope <scope-id>
    azure-dps-auth-type group-enrollment symmetric-key <key>
    include-ap-group <ap-group>
!
iot useTransportProfile "Azure-IoT-Hub-serial-data"
```

**Aruba Instant**

```
iot transportProfile "Azure-IoT-Hub-serial-data"
 endpointType Azure-IoTHub
 payloadContent serial-data
 bleDataForwarding
 azure-dps-id-scope <scope-id>
 azure-dps-auth-type group-enrollment symmetric-key <key>
 exit
iot useTransportProfile "Azure-IoT-Hub-serial-data"
```