---
layout: default
title: Device Class Filters
has_children: false
parent: IoT-Server Connectivity
grand_parent: Aruba IoT Concepts
nav_order: 2
---

# Device Class Filter

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

Device class filters are used to enabled specific [IoT transport services](#iot-transport-services) over an [IoT server connection](#iot-server-connectivity-server-side) and to control the amount of IoT data transferred on an Aruba infrastructure by using input/output filtering.

Every device class applies to a specific input filter on the IoT connectivity (radio-side) e.g., filtering BLE devices added to the BLE table and an output filter on the IoT server-side connection e.g., filtering which IoT data is forwarded to the remote server.

>***Note:***  
>Concurrent input/output filtering can be disabled if required. In that case for example an AP could hold all seen BLE devices in its BLE table but only reports specific BLE devices to the remote server determined by the output filter. Please refer to the [Aruba IoT documentation](#aruba-reference-documentation) for details.  

Multiple [supported device classes](#supported-iot-vendordevice-class-list) can be enabled in the [iot transport profile](#iot-transport-profile) configuration to enable multiple [IoT transport services](#iot-transport-services) over a single server connection.

>***Note:***  
>A maximum of 16 devices classes can be enabled per iot transport profile.

Device class filter are grouped into the following categories.

## BLE device class filter

For every supported BLE device vendor, identified by the [Bluetooth SIG member list](https://www.bluetooth.com/specifications/assigned-numbers/company-identifiers/), a dedicated [BLE device class](#supported-iot-vendordevice-class-list) is defined.
One ore more BLE device classes can be selected in an [iot transport profile](#iot-transport-profile) to enable [IoT transport services](#iot-transport-services) for the respective BLE vendor.

The special device class ***unclassified*** enables [BLE telemetry](#ble-telemetry) reporting for unknown/unsupported BLE vendor devices.  

The special device class ***all*** enables [BLE telemetry](#ble-telemetry) reporting for all BLE device classes including unclassified BLE devices.

## Wi-Fi device class filter

The device class ***wifi-assoc-sta*** and ***wifi-unassoc-sta*** enables the [Wi-Fi telemetry](#wi-fi-telemetry) transport service.

The device class ***wifi-tag*** enables the [Wi-Fi RTLS data forwarding](#wi-fi-rtls-data-forwarding) transport service.

## USB/3rd party device class filter

The device class ***serial-data*** enables the [serial-data forwarding](#serial-data) to support [3rd party IoT radio solutions](#supported-usb-vendor-list-for-iot)

## ZigBee socket device class filter

The device class ***zsd*** enables the [ZigBee socket device](#zigbee-socket-device) transport service to enable ZigBee applications.