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

Device class filters are used to enabled specific [IoT transport services](../server-connectivity/aruba_iot_transport_services.md#iot-transport-services) over an [IoT server connection](../server-connectivity/aruba_iot_server_connectivity_index.md#iot-server-connectivity-server-side) and to control the amount of IoT data transferred on an Aruba infrastructure by using input/output filtering.

Every device class applies to a specific input filter on the IoT connectivity (radio-side) e.g., filtering BLE devices added to the BLE table and an output filter on the IoT server-side connection e.g., filtering which IoT data is forwarded to the remote server.

>***Note:***  
>Concurrent input/output filtering can be disabled if required. In that case for example an AP could hold all seen BLE devices in its BLE table but only reports specific BLE devices to the remote server determined by the output filter. Please refer to the [Aruba IoT documentation](../references/../../references/aruba_reference_documentation.md#aruba-reference-documentation) for details.  

Multiple [supported device classes](../references/../../references/aruba_supported_iot_vendor_device_class_list.md#supported-iot-vendordevice-class-list) can be enabled in the [iot transport profile](../../configuration/aruba_iot_transport_profile.md#iot-transport-profile) configuration to enable multiple [IoT transport services](../server-connectivity/aruba_iot_transport_services.md#iot-transport-services) over a single server connection.

>***Note:***  
>A maximum of 16 devices classes can be enabled per iot transport profile.

Device class filter are grouped into the following categories.

## BLE device class filter

For every supported BLE device vendor, identified by the [Bluetooth SIG member list](https://www.bluetooth.com/specifications/assigned-numbers/company-identifiers/), a dedicated [BLE device class](../../references/aruba_supported_iot_vendor_device_class_list.md#supported-iot-vendordevice-class-list) is defined.
One ore more BLE device classes can be selected in an [iot transport profile](../../configuration/aruba_iot_transport_profile.md#iot-transport-profile) to enable [IoT transport services](../server-connectivity/aruba_iot_transport_services.md#iot-transport-services) for the respective BLE vendor.

The special device class ***unclassified*** enables [BLE telemetry](../server-connectivity/aruba_iot_transport_services.md#ble-telemetry) reporting for unknown/unsupported BLE vendor devices.  

The special device class ***all*** enables [BLE telemetry](../server-connectivity/aruba_iot_transport_services.md#ble-telemetry) reporting for all BLE device classes including unclassified BLE devices.

## Wi-Fi device class filter

The device class ***wifi-assoc-sta*** and ***wifi-unassoc-sta*** enables the [Wi-Fi telemetry](../server-connectivity/aruba_iot_transport_services.md#wi-fi-telemetry) transport service.

The device class ***wifi-tag*** enables the [Wi-Fi RTLS data forwarding](../server-connectivity/aruba_iot_transport_services.md#wi-fi-rtls-data-forwarding) transport service.

## USB/3rd party device class filter

The device class ***serial-data*** enables the [serial-data forwarding](../server-connectivity/aruba_iot_transport_services.md#serial-data) to support [3rd party IoT radio solutions](../../references/aruba_supported_usb_vendor_list_for_iot.md#supported-usb-vendor-list-for-iot)

## ZigBee socket device class filter

The device class ***zsd*** enables the [ZigBee socket device](../server-connectivity/aruba_iot_transport_services.md#zigbee-socket-device) transport service to enable ZigBee applications.