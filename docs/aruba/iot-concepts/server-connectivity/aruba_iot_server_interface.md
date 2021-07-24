---
layout: default
title: Aruba IoT Server Interface
has_children: false
parent: IoT-Server Connectivity
grand_parent: Aruba IoT Concepts
nav_order: 0
---

# Aruba IoT server interface

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

The **Aruba IoT server interface** is an Aruba proprietary server-side connectivity interface to connect to IoT servers using the Aruba AP's or Aruba controllers management IP address. The interface provide multiple transport protocol and data encapsulation options and is specified in the [Aruba IoT Server Interface Guide](#aruba-iot-server-interface-guide).  
All **Aruba IoT server interface** related aspects are configured in an [iot transport profile](#iot-transport-profile).  

>***Note:***  
Up to 4 iot transport profiles can be concurrently enabled per Aruba Instant AP or ArubaOS AP group.  
> This allows to run up to 4 IoT applications concurrently on an Aruba access point ,e.g. Aruba Meridian Beacon Management + Aruba Meridian Asset Tracking + 3rd Party BLE Asset Tracking + EnOcean.

The following chapters describe the **Aruba IoT server interface** related options and services.

## Server connection types

The Aruba IoT server interface supports vendor specific and generic [server connections types](#aruba-iot-server-interface---connection-types).  

The following generic connection types allow IoT data forwarding for the different [IoT connectivity (radio-side)](#iot-connectivity-radio-side) options previously described.

### Telemetry-Https

The *Telemetry-Https* connection type can be use to send [BLE telemetry](#ble-telemetry) reports in one direction only, from the radio-side to the server-side, using HTTP POST requests.  

This connection type can be used for BLE-based asset tracking or sensor monitoring use cases using easily consumable JSON data.
The used JSON data structure is defined in the [Aruba IoT Telemetry JSON Schema](#aruba-iot-telemetry-json-schema).

>***Note:***  
>**Telemetry-Https** is only meant to be used for **low thoughput** application/use cases with a low amount of APs (<20) and a high report intervall (>60 s). Trying to use **Telemetry-Https** for low latency/high toughput use cases may BLE mesages beeing dropped/delayed. Please only use [Telemetry-Websocket](#telemetry-websocket) for low latency/high toughput use cases.

>***Note:***  
>Starting with ArubaOS/Aruba Instant 8.6.0.0 or higher no new BLE device classes will be added to be used with **Telemetry-Https**.

### Telemetry-Websocket

The *Telemetry-Websocket* connection type can be used for all supported [IoT transport services](#iot-transport-services) providing a bi-directional communication channel though a web socket (ws) or secure web socket (wss) connection.

Communication via the *Telemetry-Websocket* connection is encoded using the [Google Protocol Buffers serialization protocol](https://developers.google.com/protocol-buffers). Supported messages types (northbound/southbound API) and the encoding and decoding of the data payloads is defined in the [Aruba IoT Protobuf Specification](#aruba-iot-protobuf-specification).

This connection type enables the full set of IoT connection capabilities of an Aruba infrastructure.

>***Note:***  
>The [IoT-Utilities app](https://iot-utilities.arubademo.de/) only supports Telemetry-Websocket connections.

### Azure-IoTHub

The *Azure-IoTHub* connection type can be use to send/receive [BLE data forwarding](#ble-data-forwarding)/[Serial-data](#serial-data) directly to [Azure IoT Hub](https://docs.microsoft.com/en-us/azure/iot-hub/about-iot-hub) by using the AMPQ over websocket protocol.

With this connection type Aruba controller's or Aruba Instant access points work as a protocol translation gateway (in Azure terms) to send data to Azure IoT Hub on behalf of connected IoT devices.

For details please see the [Azure IoT Hub Integration Tech Note](#azure-iot-hub-integration)  

## Server connection encryption

Even if un-encrypted HTTP or web socket connectivity is supported by the Aruba IoT server interface, it is recommended to only use encrypted connections to remote IoT systems.  

In order to establish secure web socket (wss) or HTTPS connections the remote server's self-signed certificate or root CA certificate has to be added to the Aruba controller/Aruba Instant access points trusted CA list.  

>***Note:***  
>If the IoT server certificate is un-trusted the server connection will not be established.

Please refer to [importing certificates](#importing-certificates) for how to add/import required certificates on the Aruba infrastructure.

>***Note:***  
>The [IoT-Utilities app](https://iot-utilities.arubademo.de/) provides a download link on the web dashboard to download the self-signed server certificate. Alternatively a certificate signed by a private or public CA certificate that is trusted by the Aruba infrastructure can be installed into the app.

## Authentication and authorization

Depending on the [Aruba IoT server connection type](#aruba-iot-server-interface---connection-types) different authentication and authorization methods are supported/required to establish server-side connections.

Supported authentication and authorization methods are:

- static access token
- username/password
- client_id/secret

Details about the different authentication methods are documented in the [Aruba IoT Server Interface Guide](#aruba-iot-server-interface-guide).

## Connection management

Server connections are established form every single Aruba Instant access point, in case of a controller-less setup, or from every Aruba controller in case of a controller-based setup.  

For example, in a controller cluster setup with 4 controllers every controller will establish a connection to the remote server.

>***Note:***  
>In an ArubaOS controller setup the number of server connections equals the number of controllers.  
>  
>In an Aruba Instant setup the number of server connections equals the number of APs.  

In a controller based setup IoT data is forwarded to/from the remote IoT server via the APs active controller only. In case of a failover the IoT communication will also failover to the backup controller's IoT interface connection.  

>***Note***  
>Redundant controller based setups requires proper connection management on the IoT server side for bi-directional communication to continue to work in case of a failover. The remote server application has to keep tack of which AP and IoT radio is reachable via which connection.
>  
>For details please refer to the [Aruba IoT Server Interface Guide](#aruba-iot-server-interface-guide).