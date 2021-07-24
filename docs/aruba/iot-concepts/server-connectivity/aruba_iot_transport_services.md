---
layout: default
title: IoT Transport Services
has_children: false
parent: IoT-Server Connectivity
grand_parent: Aruba IoT Concepts
nav_order: 1
---

# IoT transport services

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

The Aruba IoT server interface supports different transport services for the IoT communication.

The usage of the specific transport service depends on the used [IoT connectivity](#iot-connectivity-radio-side) and [IoT server connection type](#server-connection-types).

>***Note:***
>Not all transport services are supported with every available IoT server connectivity option.

To enable one or multiple transport services the corresponding supported [device class filter](#device-class-filter) has to be enabled in the [iot transport profile](#iot-transport-profile) configuration.

The table below shows a summary of the available transport services and the corresponding supporte server connection types and device class filter:

|IoT transport service|[IoT connectivity](#iot-connectivity-radio-side)|[IoT server connection type](#server-connection-types)|[Device Class Filter](#device-class-filter)|
|-|-|-|-|
|**Wi-Fi**||||
|[Wi-Fi telemetry](#wi-fi-telemetry)|[Wi-Fi](#wi-fi)|[Telemetry-Websocket](#telemetry-websocket)|[wifi-assoc-sta, wifi-unassoc-sta](#wi-fi-device-class-filter)|
|[Wi-Fi RTLS data forwarding](#wi-fi-rtls-data-forwarding)|[Wi-Fi](#wi-fi)|[Telemetry-Websocket](#telemetry-websocket)|[wifi-tags](#wi-fi-device-class-filter)|
|**Bluetooth Low Energy (BLE)**||||
|[BLE telemetry](#ble-telemetry)|BLE -> [Aruba IoT radio Gen1 or Gen2](#aruba-iot-radio)|[Telemetry-Https](#Telemetry-Https), [Telemetry-Websocket](#telemetry-websocket)|[All BLE device classes](#ble-device-class-filter)|
|[BLE data forwarding](#ble-data-forwarding)|BLE -> [Aruba IoT radio Gen1 or Gen2](#aruba-iot-radio)|[Telemetry-Websocket](#telemetry-websocket), [Azure-IoTHub](#azure-iothub)|[All BLE device classes](#ble-device-class-filter)|
|[BLE connect](#ble-connect)|BLE -> [Aruba IoT radio Gen1 or Gen2](#aruba-iot-radio)|[Telemetry-Websocket](#telemetry-websocket)|[All BLE device classes](#ble-device-class-filter)|
|**USB/3rd party**||||
|[Serial-data](#serial-data)|USB/3rd party -> [USB-to-serial](#usb-to-serial)|[Telemetry-Websocket](#telemetry-websocket), [Azure-IoTHub](#azure-iothub)|[serial-data](#usb3rd-party-device-class-filter)|
|**ZigBee**||||
|[ZigBee Socket Device](#zigbee-socket-device)|[ZigBee -> Aruba IoT radio Gen2](#aruba-iot-radio)|[Telemetry-Websocket](#telemetry-websocket)|[zsd](#zigbee-socket-device-class-filter)|  

>***Note:***  
>For details about the available data payloads and the correspondig encoding and deconding of the different IoT transport servcies please refer to the [Aruba IoT Server Interface Guide](#aruba-iot-server-interface-guide).

## Wi-Fi telemetry

Wi-Fi telemetry sends periodic reports (northbound only) about all the Wi-Fi devices that are discovered by an AP.

 >***Note:***  
 >For an AP to discover Wi-Fi devices the AP radios has to be enabled and set to *access* or *monitor* mode.

Wi-Fi devices are classified either as:

- associated (*wifi-assoc-sta*)
- unassociated (*wifi-unassoc-sta*)

At every reporting interval the following information are reported:

- station MAC address
- received signal strength (RSSI)
- device class

Wi-Fi telemetry is enabled using the device class [wifi-assoc-sta](#wi-fi-device-class-filter) and/or [wifi-unassoc-sta](#wi-fi-device-class-filter) in the [iot transport profile](#iot-transport-profile) configuration.

>***Note:***  
>WiFi telemetry is only available when using the IoT server connection type [Telemetry-Websocket](#telemetry-websocket).

## Wi-Fi RTLS data forwarding

WiFi RTLS data forwards the wireless data frames that originate from unassociated Wi-Fi tags addressed to a configured RTLS destination MAC address to the remote server.

Wi-fi devices matching this traffic pattern are classified as *wifi-tags*.

The RTLS destination MAC address has to be set in the [iot transport profile](#iot-transport-profile) configuration.

Wi-Fi frames matching the RTLS destination MAC address are immediately forwarded via the IoT server connection (northbound only) to the remote server including the following information:  

- received signal strength (RSSI)
- device class (set to “wifi-tag”)
- payload of the wireless frame

Wi-Fi RTLS data forwarding is enabled using the device class [wifi-tag](#wi-fi-device-class-filter) in the [iot transport profile](#iot-transport-profile) configuration.

>***Note:***  
>WiFi telemetry is only available when using the IoT server connection type [Telemetry-Websocket](#telemetry-websocket).

## BLE telemetry

BLE telemetry sends periodic reports about all BLE devices that are discovered by an AP's [IoT radio](#aruba-iot-radio) and saved on a local BLE table to a remote server.  

![BLE telemetry](../images/ble_telemetry.png)

The AP will continuously listen for advertisements and scan responses and parse/decode these packets for supported BLE protocols. The APs BLE table is updated and reported as BLE telemetry data at a configurable report interval.  

>***BLE table limits:***
>
>- max: 512 devices per AP  
>- Oldest entries are deleted first (FIFO)

These telemetry reports contain a summary of all the BLE devices that are seen by a particular AP. For each individual BLE device the supported protocol information will be reported. For unsupported BLE protocols at least the BLE MAC address and the RSSI value are reported.  

An example of these reports and the JSON schema can be found in the [Aruba IoT Telemetry JSON Schema documentation](#aruba-iot-telemetry-json-schema).

BLE telemetry is enabled for the selected [BLE device class](#ble-device-class-filter) in the [iot transport profile](#iot-transport-profile) configuration.

>***Note:***  
>BLE Telemetry is the default data forwarding mode for all BLE device classes and cannot be disabled.

## BLE data forwarding

BLE data forwarding sends all BLE advertisement and scan response frames from [known BLE vendor device classes](#supported-iot-vendordevice-class-list) to a remote server.

BLE data forwarding works by forwarding the raw BLE data packets to the remote server **immediately when they are received** by the AP's [IoT radio](#aruba-iot-radio).

![BLE data forwarding](../images/ble_data_forwarding.png)

>***Important:***  
>BLE forwarding increase the amount of server-side traffic because a message for every BLE advertisement and scan response from eligible BLE devices is forwarded.  
>Furthermore, BLE data forwarding happens in addition to the periodic telemetry reporting. Both methods happen in parallel.  
Therefore, if BLE data forwarding is the main method for the IoT use case it is recommended to set a high *reporting interval* in the [iot transport profile](#iot-transport-profile).  

With ArubaOS/Instant version 8.7.0.0 no special configuration is needed to enable BLE data forwarding. The BLE data service is automatically enabled for the following selected device classes:  

  - mysphera
  - abilitySmartSensor
  - sBeacon
  - exposureNotification
  - wiliot
  
Starting with ArubaOS/Instant version 8.8.0.0 BLE data forwarding is supported for all [known BLE vendor device classes](#supported-iot-vendordevice-class-list), except for [BLE device class](#ble-device-class-filter) ***all*** or ***unclassified***.

BLE data forwarding is enabled for the selected [BLE device class](#ble-device-class-filter) in the [iot transport profile](#iot-transport-profile) configuration.

>***Note:***  
>BLE data forwarding is only available when using the IoT server connection type [Telemetry-Websocket](#telemetry-websocket).

## BLE connect

BLE connect provides functions to connect and interact with BLE devices remotely via the [Aruba IoT server interface](#aruba-iot-server-interface) using the [BLE GATT profile](https://www.bluetooth.com/bluetooth-resources/intro-to-bluetooth-gap-gatt/).  

This allows IoT server applications to connect to BLE devices via the AP's [IoT radio](#aruba-iot-radio) using a southbound API. This service is generic to all BLE devices and is not limited to a specific device class.  
An access point can connect to one BLE device at a time using BLE connect. Before connecting to another BLE device an existing connections has to be disconnected.

>***Note:***  
>[BLE connect](#ble-connect) using the southbound API is only supported using the [**internal**](#internal) IoT radio.  

>***Note:***  
>Starting with ArubaOS/Instant OS 8.8.0.0 BLE security (authentication/encryption) has been added to the BLE connect service. BLE security is only supported on the [AP-5xx BLE5/802.15.4 (Gen2) IoT radio](#aruba-iot-radio).

For details about the available BLE connect service please refer to the [Aruba IoT Server Interface Guide](#aruba-iot-server-interface-guide).  

BLE connect is enabled for the selected [BLE device class](#ble-device-class-filter) in the [iot transport profile](#iot-transport-profile) configuration and requires the server connection type [Telemetry-Websocket](#telemetry-websocket) beeing selected.

## Serial-data

Serial-data forwarding is used to support [3rd party IoT radio solutions](#supported-usb-vendor-list-for-iot) connected via the AP USB port.
When the 3rd party IoT radio is plugged into the USB port, it presents itself as a [USB-to-serial](#usb-to-serial) device to the AP.

The serial data sent by the 3rd party radio to the AP is encapsulated in the [Aruba IoT server interface](#aruba-iot-server-interface) protocol to/from the IoT backend system. The server can also send serial data to the AP, which will be forwarded to the 3rd party device.  

>***Note:***  
>Serial-data forwarding is only available when using the IoT server connection type [Telemetry-Websocket](#telemetry-websocket).

Serial data forwarding is enabled using the device class [serial-data](#usb3rd-party-device-class-filter) in the [iot transport profile](#iot-transport-profile) configuration.

## ZigBee socket device

ZigBee socket device (ZSD) service is a generic approach used for enabling ZigBee applications using the [Aruba IoT radio Gen2](#aruba-iot-radio).

Sending/receiving ZigBee application data using the ZigBee socket device (ZSD) service requires the configuration of one or multiple [ZigBee socket device profiles](#zigbee-socket-device-profile) which define the inbound and outbound sockets used by the respective ZigBee application.  

- **Inbound sockets**
  - Defines Zigbee application protocol layer (APL) packets received by the AP from ZigBee devices via the ZigBee radio
  - Data is forwarded to the remote ZigBee application server via the Aruba IoT interface

- **Outbound sockets**
  - Defines Zigbee application protocol layer (APL) packets received by the AP form the ZigBee application server via the Aruba IoT interface
  - Data is forwarded to ZigBee devices via the ZigBee radio

A ZigBee socket profile definition consists of four items:  

- source endpoint
- destination endpoint
- profile ID
- cluster ID

Different ZigBee services have different socket definitions, may be even for inbound and outbound connections.  

Only the [Aruba IoT radios Gen2](#aruba-iot-radio) supports the ZigBee protocol and provides the coordinator function to establish a ZigBee network. The [ZigBee service profile](#zigbee-service-profile) defines the respective ZigBee network parameters.

ZigBee socket device (ZSD) service is enabled using the device class [zsd](#zigbee-socket-device-class-filter) in the [iot transport profile](#iot-transport-profile) configuration. In addition one or multiple [ZigBee socket device profiles](#zigbee-socket-device-profile) have to be defined and assigned in the [iot transport profile](#iot-transport-profile) configuration.

>***Note:***  
>The ZigBee socket device (ZSD) service is only available when using the IoT server connection type [Telemetry-Websocket](#telemetry-websocket).

Details about the required configuration steps are describe in the chapter [ZigBee configuration](#zigbee-configuration).