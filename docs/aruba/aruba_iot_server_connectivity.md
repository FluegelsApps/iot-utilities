---
layout: default
title: IoT-Server Connectivity (Server-Side)
has_children: false
parent: Aruba IoT Concepts
grand_parent: Aruba Guide
---

## [IoT server connectivity (server-side)](#table-of-contents)

On the server-side IoT data payloads are either forwarded directly by [USB-to-ethernet](#usb-to-ethernet) connected devices using IP transport or using the [Aruba IoT server interface](#aruba-iot-server-interface) providing different transport protocols and data encapsulations.

USB-to-ethernet connectivity only requires applying a [Wired-Port profile](#wired-port-profile) to the APs USB port to give the USB host system ethernet/IP access. The benefit of this approach is that USB host system's network access can be separated from the AP management networks e.g. by assigning a different VLAN and can be controlled using the AP integrated firewall like any other wired ethernet client connected to the AP. The USB host system uses its own IP stack with a separate IP address for its communication to the remote IoT system.

>***Note:***  
>Vendor specific USB implementations like [SES Imagotag Electronic Shelf Labels (ESL)](#ses-imagotag-esl-configuration) are using IP transport with a [vendor specific configuration](#vendor-specific-implementations).  

### [**Aruba IoT server interface**](#table-of-contents)

The **Aruba IoT server interface** is an Aruba proprietary server-side connectivity interface to connect to IoT servers using the Aruba AP's or Aruba controllers management IP address. The interface provide multiple transport protocol and data encapsulation options and is specified in the [Aruba IoT Server Interface Guide](#aruba-iot-server-interface-guide).  
All **Aruba IoT server interface** related aspects are configured in an [iot transport profile](#iot-transport-profile).  

>***Note:***  
Up to 4 iot transport profiles can be concurrently enabled per Aruba Instant AP or ArubaOS AP group.  
> This allows to run up to 4 IoT applications concurrently on an Aruba access point ,e.g. Aruba Meridian Beacon Management + Aruba Meridian Asset Tracking + 3rd Party BLE Asset Tracking + EnOcean.

The following chapters describe the **Aruba IoT server interface** related options and services.

### [**Server connection types**](#table-of-contents)

The Aruba IoT server interface supports vendor specific and generic [server connections types](#aruba-iot-server-interface---connection-types).  

The following generic connection types allow IoT data forwarding for the different [IoT connectivity (radio-side)](#iot-connectivity-radio-side) options previously described.

#### [***Telemetry-Https***](#table-of-contents)

The *Telemetry-Https* connection type can be use to send [BLE telemetry](#ble-telemetry) reports in one direction only, from the radio-side to the server-side, using HTTP POST requests.  

This connection type can be used for BLE-based asset tracking or sensor monitoring use cases using easily consumable JSON data.
The used JSON data structure is defined in the [Aruba IoT Telemetry JSON Schema](#aruba-iot-telemetry-json-schema).

>***Note:***  
>**Telemetry-Https** is only meant to be used for **low thoughput** application/use cases with a low amount of APs (<20) and a high report intervall (>60 s). Trying to use **Telemetry-Https** for low latency/high toughput use cases may BLE mesages beeing dropped/delayed. Please only use [Telemetry-Websocket](#telemetry-websocket) for low latency/high toughput use cases.

>***Note:***  
>Starting with ArubaOS/Aruba Instant 8.6.0.0 or higher no new BLE device classes will be added to be used with **Telemetry-Https**.

#### [***Telemetry-Websocket***](#table-of-contents)

The *Telemetry-Websocket* connection type can be used for all supported [IoT transport services](#iot-transport-services) providing a bi-directional communication channel though a web socket (ws) or secure web socket (wss) connection.

Communication via the *Telemetry-Websocket* connection is encoded using the [Google Protocol Buffers serialization protocol](https://developers.google.com/protocol-buffers). Supported messages types (northbound/southbound API) and the encoding and decoding of the data payloads is defined in the [Aruba IoT Protobuf Specification](#aruba-iot-protobuf-specification).

This connection type enables the full set of IoT connection capabilities of an Aruba infrastructure.

>***Note:***  
>The [IoT-Utilities app](https://iot-utilities.arubademo.de/) only supports Telemetry-Websocket connections.

#### [***Azure-IoTHub***](#table-of-contents)

The *Azure-IoTHub* connection type can be use to send/receive [BLE data forwarding](#ble-data-forwarding)/[Serial-data](#serial-data) directly to [Azure IoT Hub](https://docs.microsoft.com/en-us/azure/iot-hub/about-iot-hub) by using the AMPQ over websocket protocol.

With this connection type Aruba controller's or Aruba Instant access points work as a protocol translation gateway (in Azure terms) to send data to Azure IoT Hub on behalf of connected IoT devices.

For details please see the [Azure IoT Hub Integration Tech Note](#azure-iot-hub-integration)  

### [**Server connection encryption**](#table-of-contents)

Even if un-encrypted HTTP or web socket connectivity is supported by the Aruba IoT server interface, it is recommended to only use encrypted connections to remote IoT systems.  

In order to establish secure web socket (wss) or HTTPS connections the remote server's self-signed certificate or root CA certificate has to be added to the Aruba controller/Aruba Instant access points trusted CA list.  

>***Note:***  
>If the IoT server certificate is un-trusted the server connection will not be established.

Please refer to [importing certificates](#importing-certificates) for how to add/import required certificates on the Aruba infrastructure.

>***Note:***  
>The [IoT-Utilities app](https://iot-utilities.arubademo.de/) provides a download link on the web dashboard to download the self-signed server certificate. Alternatively a certificate signed by a private or public CA certificate that is trusted by the Aruba infrastructure can be installed into the app.

### [**Authentication and authorization**](#table-of-contents)

Depending on the [Aruba IoT server connection type](#aruba-iot-server-interface---connection-types) different authentication and authorization methods are supported/required to establish server-side connections.

Supported authentication and authorization methods are:

- static access token
- username/password
- client_id/secret

Details about the different authentication methods are documented in the [Aruba IoT Server Interface Guide](#aruba-iot-server-interface-guide).

### [**Connection management**](#table-of-contents)

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

### [**IoT transport services**](#table-of-contents)

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

#### [**Wi-Fi telemetry**](#table-of-contents)

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

#### [**Wi-Fi RTLS data forwarding**](#table-of-contents)

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

#### [**BLE telemetry**](#table-of-contents)

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

#### [**BLE data forwarding**](#table-of-contents)

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

#### [**BLE connect**](#table-of-contents)

BLE connect provides functions to connect and interact with BLE devices remotely via the [Aruba IoT server interface](#aruba-iot-server-interface) using the [BLE GATT profile](https://www.bluetooth.com/bluetooth-resources/intro-to-bluetooth-gap-gatt/).  

This allows IoT server applications to connect to BLE devices via the AP's [IoT radio](#aruba-iot-radio) using a southbound API. This service is generic to all BLE devices and is not limited to a specific device class.  
An access point can connect to one BLE device at a time using BLE connect. Before connecting to another BLE device an existing connections has to be disconnected.

>***Note:***  
>[BLE connect](#ble-connect) using the southbound API is only supported using the [**internal**](#internal) IoT radio.  

>***Note:***  
>Starting with ArubaOS/Instant OS 8.8.0.0 BLE security (authentication/encryption) has been added to the BLE connect service. BLE security is only supported on the [AP-5xx BLE5/802.15.4 (Gen2) IoT radio](#aruba-iot-radio).

For details about the available BLE connect service please refer to the [Aruba IoT Server Interface Guide](#aruba-iot-server-interface-guide).  

BLE connect is enabled for the selected [BLE device class](#ble-device-class-filter) in the [iot transport profile](#iot-transport-profile) configuration and requires the server connection type [Telemetry-Websocket](#telemetry-websocket) beeing selected.

#### [**Serial-data**](#table-of-contents)

Serial-data forwarding is used to support [3rd party IoT radio solutions](#supported-usb-vendor-list-for-iot) connected via the AP USB port.
When the 3rd party IoT radio is plugged into the USB port, it presents itself as a [USB-to-serial](#usb-to-serial) device to the AP.

The serial data sent by the 3rd party radio to the AP is encapsulated in the [Aruba IoT server interface](#aruba-iot-server-interface) protocol to/from the IoT backend system. The server can also send serial data to the AP, which will be forwarded to the 3rd party device.  

>***Note:***  
>Serial-data forwarding is only available when using the IoT server connection type [Telemetry-Websocket](#telemetry-websocket).

Serial data forwarding is enabled using the device class [serial-data](#usb3rd-party-device-class-filter) in the [iot transport profile](#iot-transport-profile) configuration.

#### [**ZigBee socket device**](#table-of-contents)

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

### [**Device Class Filter**](#table-of-contents)

Device class filters are used to enabled specific [IoT transport services](#iot-transport-services) over an [IoT server connection](#iot-server-connectivity-server-side) and to control the amount of IoT data transferred on an Aruba infrastructure by using input/output filtering.

Every device class applies to a specific input filter on the IoT connectivity (radio-side) e.g., filtering BLE devices added to the BLE table and an output filter on the IoT server-side connection e.g., filtering which IoT data is forwarded to the remote server.

>***Note:***  
>Concurrent input/output filtering can be disabled if required. In that case for example an AP could hold all seen BLE devices in its BLE table but only reports specific BLE devices to the remote server determined by the output filter. Please refer to the [Aruba IoT documentation](#aruba-reference-documentation) for details.  

Multiple [supported device classes](#supported-iot-vendordevice-class-list) can be enabled in the [iot transport profile](#iot-transport-profile) configuration to enable multiple [IoT transport services](#iot-transport-services) over a single server connection.

>***Note:***  
>A maximum of 16 devices classes can be enabled per iot transport profile.

Device class filter are grouped into the following categories.

#### [**BLE device class filter**](#table-of-contents)

For every supported BLE device vendor, identified by the [Bluetooth SIG member list](https://www.bluetooth.com/specifications/assigned-numbers/company-identifiers/), a dedicated [BLE device class](#supported-iot-vendordevice-class-list) is defined.
One ore more BLE device classes can be selected in an [iot transport profile](#iot-transport-profile) to enable [IoT transport services](#iot-transport-services) for the respective BLE vendor.

The special device class ***unclassified*** enables [BLE telemetry](#ble-telemetry) reporting for unknown/unsupported BLE vendor devices.  

The special device class ***all*** enables [BLE telemetry](#ble-telemetry) reporting for all BLE device classes including unclassified BLE devices.

#### **Wi-Fi device class filter**

The device class ***wifi-assoc-sta*** and ***wifi-unassoc-sta*** enables the [Wi-Fi telemetry](#wi-fi-telemetry) transport service.

The device class ***wifi-tag*** enables the [Wi-Fi RTLS data forwarding](#wi-fi-rtls-data-forwarding) transport service.

#### **USB/3rd party device class filter**

The device class ***serial-data*** enables the [serial-data forwarding](#serial-data) to support [3rd party IoT radio solutions](#supported-usb-vendor-list-for-iot)

#### **ZigBee socket device class filter**

The device class ***zsd*** enables the [ZigBee socket device](#zigbee-socket-device) transport service to enable ZigBee applications.

### [**Data content filters**](#table-of-contents)

In addition to filter for specific [device classes](#device-class-filter) it possible to filter the forwarded IoT data content before being sent to the remote Iot system.

#### [**General data filter**](#table-of-contents)

-   ***Data Filter***  
This is a list of data fields to be suppress in the telemetry reports. The data filter is a string that is a comma separated list of index-paths. Each index path refers to the field numbers in the [Aruba IoT Protobuf Specification](#aruba-iot-protobuf-specification). For example, the value  “3.3, 3.12” would suppress the ‘reported.model’ field and the ‘reported.beacons’ field in the telemetry reports.  

-   ***Device Count***  
Only sends the count of device types, e.g. iBeacon, Wi-Fi clients, seen by an AP in the telemetry reports, but not the actual device information of those devices. Supported device counts are defined in the [Aruba IoT Protobuf Specification](#aruba-iot-protobuf-specification).

#### [**BLE data filter**](#table-of-contents)

-   ***RSSI Reporting Format***  
For the BLE RSSI values being send in the telemetry reports five different RSSI reporting formats are supported. The four reporting
formats are:
    -   **Average** - The average RSSI over the reporting interval will be reported.  
    -   **Last** -  Only the last RSSI value that was seen by the device will be reported.  
    -   **Max** - The max RSSI value that was seen over the reporting interval will be reported only. This max value resets each telemetry reporting interval and will be updated accordingly.  
    -   **Bulk** - The last 20 RSSI values that were seen by the device since the previous telemetry report will be reported in an array format.  
    -   **Smooth** -  A single smoothed out RSSI value will be reported for each telemetry report. This is done by attempting to remove outliers from the RSSI values received by the AP.  

-   ***Environment Type***  
Five different pre-defined environment types are supported to help adjust RSSI based distance calculation to better fit the environment in which the BLE devices are operating in. For best results, the value that closest corresponds to the environment in which BLE is operating should be chosen.  
    -   **auditorium**
    -   **office**
    -   **outdoor**
    -   **shipboard**
    -   **warehouse**
    -   **custom** (see custom fading factor for details)

-   ***Custom Fading Factor***  
If the pre-defined environment type offsets do not properly fit the environment, a custom fading factor can be configured by setting the environment type to ***custom***. This field accepts integer values in the range of 10 to 40.  

-   ***Cell Size Filter***  
A proximity-based filter that will only report devices that are found to be within an “x” meter radius around the access point. This distance is calculated with an algorithm based off the RSSI value. The default value for this field is “0”, which translates to the cell size filter being disabled. This field accepts integer values from 2 to 100 and the units are meters.  

-   ***Movement Filter***  
This filter is active when the cell size filter is also configured. When this filter is enabled, devices will only be reported if the difference between their current and prior distance is more than the configured filter value. For example, if the movement filter is configured to be 2 meters, a device that is calculated to have moved 1 meter will not be reported, while a device that moves 5 meters will be reported. The default value for this field is “0”, which corresponds to the movement filter being disabled. This field accepts integer values from 2 to 30, and the units are meters.  

-   ***Age Filter***  
The Age Filter is used to only report devices the AP has received an update (either BLE advertisement or scan response) in the configured time. For instance, if the age filter is set to 30 seconds, only devices which have been heard in the last 30 seconds will be reported. If there is a device that received an update 45 seconds before, this device will not be reported. The default value for this field is “0”, which corresponds to the age filter being disabled. This field accepts integer values from 30 to 3600, and the units are seconds.  

-   ***BLE Vendor Filter***  
The BLE Vendor Filter allows to input [Bluetooth SIG Vendor IDs](https://www.bluetooth.com/specifications/assigned-numbers/company-identifiers/) and/or freeform vendor name strings, which will be used to filter the devices being reported. If this is configured, the only devices that will be reported are the devices that match the configured Vendor ID or Vendor Name.  
The vendor ID is a 2-byte hexadecimal value preceding with 0x in 0xABCD format. The vendor name is a string that can be either a full vendor name (example:Aruba) or a substring of the actual vendor name (example:Aru) and can be case-insensitive.  
The vendor filter accepts up to five combinations of vendor names or vendorIDs separated by commas, for example:  
    -   Aruba,Favendo,HanVit,SoluM,ABB
    -   0xABCD,0xBCDE,0xCDEF,0xDEF0,0xEF01
    -   Aruba,0xABCD,Favendo,0xBCDE,HanVit  

    If more than one vendor name or vendorID is configured, then any of the matching vendor names or vendorIDs in the vendor filter is applied. A device is reported only if the vendor data or vendor name field is not empty and matches the vendor information configured. If the vendor field is not populated for the devices, the IoT devices are reported because there is not matching vendor filter in the IoT transport profile.

-   ***UUID Filter (iBeacon)***  
A list of UUIDs to filter the devices included in the reports. Applies only to iBeacon devices.

-   ***UID Namespace Filter (Eddystone)***  
A list of UID namespaces to filter devices included in the reports. Applies only Eddystone-UID devices

-   ***URL Filter (Eddystone)***  
A list of URL strings to filter devices included in the reports. Applies only Eddystone-URL devices. The string listed here can be a partial URL strings.

-   ***BLE data forwarding - per frame filtering***  
When [BLE data forwarding](#ble-data-forwarding) is enabled, the raw payload contained within a BLE packet is forwarded to the configured server. The per frame filtering knob is a modifier on top of the BLE data forwarding knob. When only BLE data forwarding is enabled, all BLE packets for a device having a known device class filter label are forwarded.  
For example: If a device advertises an iBeacon frame and an Eddystone frame and in the [transport profile](#iot-transport-profile) the ***iBeacon*** device class has been selected only, then for this device both iBeacon and Eddystone frames are forward.  
If per frame filtering is enabled in addition to the BLE data forwarding , then only the raw payloads from the iBeacon frames will be forwarded.  