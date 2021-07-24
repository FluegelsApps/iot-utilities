---
layout: default
title: Aruba IoT Server Interface - Connection Types
has_children: false
parent: References
nav_order: 1
---

# Aruba IoT server interface - connection types

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

Supported connection type list as of ArubaOS/Aruba Instant version 8.8.0.0.

|Server connection type|Transport protocol|Data encapsulation|Authentication & Authorization|Supported report interval (in seconds)|Supported device class filter|Description|
|-|-|-|-|-|-|-|
|Assa-Abloy|HTTPS|vendor specific|username/password, access_id|1-3600 s, default: 600|assa-abloy|Assa Abloy Visiononline server|
|[Azure-IoTHub](#azure-iothub)|AMQP over secure web socket|JSON|symmetric group key|n/a -telemetry reports are not supported|all BLE types, serial-data|Connect with Azure IoT Hub|
|Meridian-Beacon-Management|secure web socket (wss)|vendor specific|static access token|10-600 s, default: 600 s|aruba-beacons|POST to a RESTful Meridian API|
|Meridian-Asset-Tracking|secure web socket (wss)|vendor specific|client_id/secret|2-600 s, default: 5 s|aruba-tags|Stream data to Meridian WebSocket server|
|[Telemetry-Https](#telemetry-https)|HTTP, HTTPS|JSON|username/password, client_id/secret, static access token|1-3600 s, default: 600 s|all BLE types, wifi-assoc-sta, wifi-unassoc-sta|POST Aruba IoT telemetry reports to HTTP server endpoint|
|[Telemetry-Websocket](#telemetry-websocket)|web socket (ws), secure web socket (wss)|Protocol Buffers (protobuf)|username/password, client_id/secret, static access token|1-3600 s, default: 600 s|all BLE types, wifi-tags, serial-data, zsd (ZigBee)|Stream data payloads to Aruba IoT interface compatible web socket server|
|ZF-Openmatics|secure web socket (wss)|vendor specific|username/password|5-600 s, default: 60 s|zf-tags|ZF Openmatics cloud management|