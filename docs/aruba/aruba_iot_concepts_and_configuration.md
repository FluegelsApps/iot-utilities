# Aruba IoT concepts and configuration

This chapter describes the principals of the Aruba IoT integrations and configuration using ArubaOs/Aruba Instant version 8.8.0.0 or higher.

[Aruba, a Hewlett Packard Enterprise (HPE) company](https://www.arubanetworks.com/) supports IoT applications based on Wi-Fi (e.g. Wi-Fi tracking), BLE (e.g. asset tracking or sensor monitoring), ZigBee and 3rd party protocols via USB-extension by providing the connection layer using Aruba access points. IoT devices can send/receive data via the Aruba APs built-in radios or supported 3rd party radios connected via USB to 3rd party backend system.

![Aruba IoT Connectivity options](../images/aruba_iot_connectivity.jpg)

The Aruba AP radios can be used as transmitter/receiver (e.g. BLE connect, ZigBee) or just a receiver/sensor (e.g. BLE asset tracking, Wi-Fi tracking), depending on the respective IoT solution. With that the AP provides a one-way or two-way communication channel between IoT devices (e.g, sensors, actors) and IoT systems.  
The access point works as protocol translational gateway between the different IoT radios/protocols and the Aruba IoT server interface protocol or plain IP protocol depending on the respective IoT solution being used.  

## IoT connectivity (radio-side)

On the radio-side the Aruba access points support different IoT radio technologies either though integrated radios or 3rd party solutions connected to the APs USB port.

### **Wi-Fi**

The Aruba access point Wi-Fi radios can be used to forward associated/unassociated client information and RTLS data for Wi-Fi based tracking use cases. Wi-Fi client and RTLS data is encapsulated in the Aruba IoT server interface protocol and forwarded to the IoT backend system.  

### **Aruba IoT radio**

An Aruba IoT radio is an additional internal or external radio in the Aruba AP-3xx/5xx series access points that can be leveraged for IoT connectivity.  
A single Aruba AP-3xx/5xx series access points can support up to two IoT radios, one internal and one external. This would used cases where one radio could be used for BLE and another for ZigBee for example.  
The access point removes/adds the radio specific headers from/to IoT devices e.g. BLE or ZigBee and forwards/receives the data payload encapsulated in the Aruba IoT server interface protocol to/from the IoT backend system.  

#### ***Integrated***

Aruba AP-3xx/5xx series access points provide an integrated Aruba IoT radio for the IoT connectivity supporting the following radio technologies:

- AP-3xx: BLE4 (Gen1)
- AP-5xx: BLE5/802.15.4 (Gen2) e.g. ZigBee

#### ***External***

In addition to the internal IoT radio Aruba also provides [IoT expansion radio](https://www.arubanetworks.com/assets/ds/DS_IoT-Expansion-Radio.pdf) supports the same radio technologies as the AP-5xx series access points:  

- Aruba IoT Expansion Radio = BLE5/802.15.4 (Gen2) e.g. ZigBee

>***Note:***  
>The internal and the expansion BLE5/802.15.4 (Gne2) IoT radio can be enabled to run in BLE and ZigBee concurrently. But in this case the IoT radio can only transmit but not receive BLE packet, while the ZigBee communication works bi-directional.  
>  
> This allows enabling the APs BLE console as well as BLE beaconing (iBeacon) for indoor navigation use cases in parallel to ZigBee user cases. But BLE tracking uses cases like asset tracking are not supported in this case.  
>  
> In order to support BLE tracking or bi-directional use cases concurrently to ZigBee uses cases on the same access points two Aruba IoT radios Gen2, one internal and one external, are required. Therefore this scenario is currently only supported on the Aruba AP-5xx series access points.

The configuration of the Aruba IoT radios is handled in the [IoT radio profile](#iot-radio-profile) configuration.

### **USB/3rd party IoT radios**

Aruba supports the extension of Aruba access points using USB with supported 3rd party solutions. Depending on the particular solution the integration uses one of the following methods:

- USB-to-serial
- USB-to-ethernet

In all cases the USB connected host system removes/adds the radio specific headers/protocols from/to IoT devices and forwards/receives the data payload to the access point using one of the USB methods.

Supported USB connected devices does not required a specific configuration, except for vendor specific implementations, but it can be controlled which USB devices are allowed to connect to an access points. This can be controlled using an [USB ACL profile](#usb-acl-profile).

#### ***USB-to-serial***

The [3rd party solutions using the USB-to-serial](#supported-usb-vendor-list-for-iot) method forwards the data payload to/from the access point using [serial-data](#serial-data). The Aruba access point encapsulates the serial-data payload in the Aruba IoT server interface protocol to/from the IoT backend system.

>***Note:***  
> No specific configuration is required for USB-to-serial devices. Serial data is only forwarded though the Aruba IoT server interface, if enabled on the server-side.  

#### ***USB-to-ethernet***

The [3rd party solutions using the USB-to-ethernet](#supported-usb-vendor-list-for-iot) method provides ethernet/IP connectivity to the connected USB host system. The USB host system is connected to the access point in the same way as a wired client. No data processing is done by the access point and ethernet/IP data packets form the USB host system is forwarded like any other ethernet/IP traffic.

#### ***Vendor specific implementations***

The following [Vendor specific USB integrations](#supported-usb-vendor-list-for-iot) do not follow the previously mentioned methods and require a dedicated configuration.  
 
- [SES Imagotag Electronic Shelf Labels (ESL)](#ses-imagotag-esl-configuration)

## IoT server connectivity (server-side)

On the server-side IoT data payloads are either forwarded directly by [USB-to-ethernet](#usb-to-ethernet) connected devices using IP transport or using an [Aruba IoT server connection type](#aruba-iot-server-interface---connection-types) depended transport protocol and data encapsulation.

USB-to-ethernet connectivity only requires applying a [wired-ap port profile](#wired-ap-profile) to the APs USB port.  

>***Note:***  
>Vendor specific USB implementations like *SES Imagotag Electronic Shelf Labels (ESL)* are using IP transport with a [vendor specific configuration](#vendor-specific-implementations).  

Server-side connectivity using the Aruba IoT server interface is configured using [iot transport profiles](#iot-transport-profile).  

>***Note:***  
Up to 4 iot transport profiles can be concurrently enabled per Aruba Instant AP or ArubaOS AP-group.  
> This allows to run up to 4 IoT applications concurrently e.g., Aruba Meridian Beacon Management + Aruba Meridian Asset Tracking + 3rd Party BLE Asset Tracking + EnOcean.

### **IoT Server connection types**

The Aruba IoT server interface supports vendor specific and generic [IoT server connections](#aruba-iot-server-interface---connection-types).  

The following generic connection types allow IoT data forwarding for the different [IoT connectivity (radio-side)](#iot-connectivity-radio-side) options previously described.

>***Note:***  
>The IoT-Utilities app only support Telemetry-Websocket connections.

#### ***Telemetry-Https***

The *Telemetry-Https* connection type can be use to send [BLE telemetry](#ble-telemetry) reports in one direction only, from the radio-side to the server-side, using HTTP POST requests.  

This connection type can be used for BLE-based asset tracking or sensor monitoring use cases using easily consumable JSON data.
The used JSON data structure is defined in the [Aruba IoT Telemetry JSON Schema](#aruba-iot-telemetry-json-schema).

#### ***Telemetry-Websocket***

The *Telemetry-Websocket* connection type can be used for all [Aruba IoT server interface - transport services](#aruba-iot-server-interface---transport-services) bi-directional though a web socket (ws) or secure web socket (wss) connection.

Communication via the *Telemetry-Websocket* connection is encoded using the [Google Protocol Buffers serialization protocol](https://developers.google.com/protocol-buffers). Supported messages types (northbound/southbound API) and the encoding and decoding of the data payloads is defined in the [Aruba IoT Protobuf Specification](#aruba-iot-protobuf-specification).

With this connection type the full IoT connection capabilities of the Aruba infrastructure are available.

#### ***Azure-IoTHub***

The *Azure-IoTHub* connection type can be use to send/receive [BLE data forwarding](#ble-data-forwarding)/[Serial-data](#serial-data) directly to [Azure IoT Hub](https://docs.microsoft.com/en-us/azure/iot-hub/about-iot-hub) by using AMPQ over websocket protocol.

Aruba implements its controller's/Instant access points as a protocol translation gateway (in Azure terms) to send data to Azure IoT Hub on behalf of IoT devices.

For details please see the [Azure IoT Hub Integration Tech Note](#azure-iot-hub-integration) 

### **Server connection encryption**

Even if un-encrypted HTTP or web socket connectivity is supported by the Aruba IoT server interface, it is recommended to only use encrypted connections to remote IoT systems.  

In order to establish secure web socket (wss) or HTTPS connections the remote server's self-signed certificate or root CA certificate has to be added to the Aruba controller/Instant Access Points trusted CA list.  

>***Note:***  
>If the IoT server certificate is un-trusted the server connection will not be established.

Please refer to [importing certificates](#importing-certificates) for how add import required certificates.

>***Note:***  
>The IoT-Utilities app provides a download link on the web dashboard to download the self-signed server certificate. Alternatively a certificate signed by a private or public CA certificate that is trusted by the Aruba infrastructure can be installed into the app.

### **Authentication and authorization**

Depending on the [Aruba IoT server connection type](#aruba-iot-server-interface---connection-types) different authentication and authorization methods are supported/required to establish server-side connections.

Supported authentication and authorization methods:

- static access token
- username/password
- client_id/secret

Details about the different authentication methods are documented in the [Aruba IoT Server Interface Guide](#aruba-iot-server-interface-guide).

### **Connection management**

Server connections are established form every single Aruba Instant access point, in case of a controller-less setup, and from every Aruba controller in case of a controller-based setup.  

For example, in a controller cluster setup with 4 controllers every controller will establish a connection to the remote server.

>***Note:***  
>In an ArubaOS controller setup the number of server connections equals the number of controllers.  
>  
>In an Aruba Instant setup the number of server connections equals the number of APs.  

In a controller based setup IoT data is forwarded to/from the remote IoT server via the APs active controller only. In case of a failover the IoT communication will also failover to the backup controller's IoT interface connection.  

>***Note***  
>Redundant controller based setups requires proper connection management on the IoT server side for bi-directional communication to continue to work in case of a failover.  
>  
>For details please refer to the [Aruba IoT Server Interface Guide](#aruba-iot-server-interface-guide).

## Aruba IoT server interface - transport services

The Aruba IoT server interface supports different transport services for the IoT communication.

The usage of the specific transport service depends on the used [IoT connectivity](#iot-connectivity-radio-side) and [IoT server connection type](#iot-server-connection-types).

>***Note:***
>Not all transport services are supported with every available IoT server connectivity.

To enable one or multiple transport services the corresponding device class filter has to be enabled in the [iot transport profile](#iot-transport-profile) configuration.

The table below shows a summary of the available transport services:

|IoT transport service|[IoT connectivity](#iot-connectivity-radio-side)|[Supported IoT server connection type](#iot-server-connection-types)|[Device Class Filter](#aruba-iot-server-interface---device-class-filter)|
|-|-|-|-|
|**Wi-Fi**||||
|[Wi-Fi telemetry](#wi-fi-telemetry)|[Wi-Fi](#wi-fi)|[Telemetry-Websocket](#telemetry-websocket)|[wifi-assoc-sta, wifi-unassoc-sta](#supported-iot-vendordevice-class-list)|
|[Wi-Fi RTLS data forwarding](#wi-fi-rtls-data-forwarding)|[Wi-Fi](#wi-fi)|[Telemetry-Websocket](#telemetry-websocket)|[wifi-tags](#supported-iot-vendordevice-class-list)|
|**Bluetooth Low Energy (BLE)**||||
|[BLE Telemetry](#ble-telemetry)|BLE -> [Aruba IoT radio Gen1 or Gen2](#aruba-iot-radio)|[Telemetry-Https](#Telemetry-Https), [Telemetry-Websocket](#telemetry-websocket)|[All BLE device classes](#supported-iot-vendordevice-class-list)|
|[BLE data forwarding](#ble-data-forwarding)|BLE -> [Aruba IoT radio Gen1 or Gen2](#aruba-iot-radio)|[Telemetry-Websocket](#telemetry-websocket), [Azure-IoTHub](#azure-iothub)|[All BLE device classes](#supported-iot-vendordevice-class-list)|
|[BLE connect](#ble-connect)|BLE -> [Aruba IoT radio Gen1 or Gen2](#aruba-iot-radio)|[Telemetry-Websocket](#telemetry-websocket)|[All BLE device classes](#supported-iot-vendordevice-class-list)|
|**USB/3rd party**||||
|[Serial-data](#serial-data)|USB/3rd party -> [USB-to-serial](#usb-to-serial)|[Telemetry-Websocket](#telemetry-websocket), [Azure-IoTHub](#azure-iothub)|[serial-data](#supported-iot-vendordevice-class-list)|
|**ZigBee**||||
|[ZigBee Socket Device](#zigbee-socket-device)|[ZigBee -> Aruba IoT radio Gen2](#aruba-iot-radio)|[Telemetry-Websocket](#telemetry-websocket)|[ZSD](#supported-iot-vendordevice-class-list)|  

>***Note:***  
>For details about the available data with every IoT forwarding mode refer to the [Aruba IoT Server Interface Guide](#aruba-iot-server-interface-guide).

### **Wi-Fi telemetry**

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

>***Note:***  
>WiFi telemetry is only available when using the IoT server connection type [Telemetry-Websocket](#telemetry-websocket).

### **Wi-Fi RTLS data forwarding**

WiFi RTLS data forwards the wireless data frames that originate from unassociated Wi-Fi tags addressed to a configured RTLS destination MAC address to the remote server.

Wi-fi devices matching this traffic pattern are classified as *wifi-tags*.

The RTLS destination MAC address has to be set in the [iot transport profile](#iot-transport-profile) configuration.

Wi-Fi frames matching the RTLS destination MAC address are immediately forwarded via the IoT server connection (northbound only) to the remote server including the following information:  

- received signal strength (RSSI)
- device class (set to “wifi-tag”)
- payload of the wireless frame

>***Note:***  
>WiFi telemetry is only available when using the IoT server connection type [Telemetry-Websocket](#telemetry-websocket).

### **BLE telemetry**

BLE telemetry sends periodic reports about all BLE devices that are discovered by the AP's [IoT radio](#aruba-iot-radio) to a remote server.  

![BLE telemetry](../images/ble_telemetry.png)

The AP will continuously listen for advertisements and scan responses and parse/decode these packets for supported BLE protocols. The APs BLE table is updated an reported as BLE telemetry data at the configured report interval.  

>***BLE table limits:***
>
>- max: 512 devices per AP  
>- Oldest entries are deleted first (FIFO)

These telemetry reports contain a summary of all the BLE devices that are seen by a particular AP. For each individual BLE device the supported protocol information will reported. For unsupported BLE protocols at least the BLE MAC address and the RSSI value are reported.  

An example of these reports and the JSON schema can be found in the [Aruba IoT Telemetry JSON Schema documentation](#aruba-iot-telemetry-json-schema).

>***Note:***  
>BLE Telemetry is the default data forwarding mode for all BLE device classes and cannot be disabled.

### **BLE data forwarding**

BLE data forwarding sends all BLE advertisement and scan response frames from supported [BLE device classes](#supported-iot-vendordevice-class-list).

>***Note:***  
>Starting with ArubaOS/Instant version 8.8 BLE data forwarding is supported for all [BLE device classes](#supported-iot-vendordevice-class-list).

BLE data forwarding works by forwarding the raw BLE data packets to the remote server **immediately when they are received** by the AP's [IoT radio](#aruba-iot-radio).

![BLE data forwarding](../images/ble_data_forwarding.png)

>***Important:***  
>BLE forwarding increase the amount of server-side traffic because a message for every BLE advertisement and scan response from eligible BLE devices is send.  
>Furthermore, BLE data forwarding happens in addition to the periodic telemetry reporting. Both methods happen in parallel.  
Therefore, if BLE data forwarding is the main method for the IoT use case it is recommended to set a high *reporting interval* in the iot transport profile.  

>***Note:***  
>BLE data forwarding is only available when using the IoT server connection type [Telemetry-Websocket](#telemetry-websocket).

### **BLE connect**

BLE connect provides functions to connect and interact with BLE devices remotely via the IoT interface using the [BLE GATT profile](https://www.bluetooth.com/bluetooth-resources/intro-to-bluetooth-gap-gatt/).  

This allows IoT server applications to connect to BLE devices via the AP's [IoT radio](#aruba-iot-radio). This service is generic to all BLE devices and is not limited to as specific device class.

>***Note:***  
>An access point can connect to one BLE device at a time using BLE connect. Before connecting to another BLE device an existing connections has to be disconnected.

For details about the available BLE connection functions refer to the [Aruba IoT Server Interface Guide](#aruba-iot-server-interface-guide).

>***Note:***  
>BLE data forwarding is only available when using the IoT server connection type [Telemetry-Websocket](#telemetry-websocket).

### **Serial-data**

Serial-data forwarding is used to support [3rd party IoT radio solutions](#supported-usb-vendor-list-for-iot) connected via the AP USB port.
When the 3rd party IoT radio is plugged into the USB port, it presents itself as a [USB-to-serial](#usb-to-serial) device to the AP.

The serial data sent by the 3rd party radio to the AP is encapsulated in the Aruba IoT server interface protocol to/from the IoT backend system. The server can also send serial data to the AP, which will be forwarded to the 3rd party device.  

>***Note:***  
>BLE data forwarding is only available when using the IoT server connection type [Telemetry-Websocket](#telemetry-websocket).

Serial data forwarding is enabled using the device class *serial-data* in the [iot transport profile](#iot-transport-profile) configuration.

### **ZigBee socket device**

ZigBee socket device (ZSD) is a generic approach used for enabling ZigBee applications using the [Aruba IoT radio Gen2](#aruba-iot-radio).

>***Note:***  
>The ZigBee based Assa-Abloy solution uses a vendor specific [server connection type](#aruba-iot-server-interface---connection-types) and not the ZSD transport service.

Sending/receiving ZigBee application data using the ZigBee socket device (ZSD) method requires the configuration of one or multiple [ZigBee socket device profiles](#zigbee-socket-device-profile) which define the inbound and outbound sockets used by the ZigBee application.  

- inbound sockets: receiving data from ZigBee devices
- outbound sockets: sending data to ZigBee devices

A ZigBee socket definition consists of four items:  

- source-endpoint
- destination-endpoint
- profile ID
- cluster ID

Different ZigBee services have different socket definitions, may be even for inbound and outbound connections.  

[Aruba IoT radios Gen2](#aruba-iot-radio) supports working as coordinator in a ZigBee network. The [ZigBee service profile](#zigbee-service-profile) defines the ZigBee network parameter.

>***Note:***  
>ZigBee socket device (ZSD) is only available when using the IoT server connection type [Telemetry-Websocket](#telemetry-websocket).

## Aruba IoT server interface - Device Class Filter

Device class filters are used to control which IoT application are enabled and the amount of IoT data transferred on an Aruba infrastructure by using input/output filtering.

Every device class applies a specific input filter on the IoT connectivity (radio-side) e.g., filtering BLE devices added to the BLE table and an output filter on the IoT server-side connection e.g., filtering which IoT data is forwarded to the remote server.

>***Note:***  
>Concurrent input filtering can be disabled if required. Please refer to the [Aruba IoT documentation](#aruba-reference-documentation) for details.  

[Supported device classes](#supported-iot-vendordevice-class-list) are enabled in the [iot transport profile](#iot-transport-profile) configuration.

>***Note:***  
>A maximum of 16 devices classes can be enabled per iot transport profile.

The special device class ***unclassified*** enables [BLE telemetry](#ble-telemetry) reporting for unknown/unsupported BLE devices (not in the supported BLE vendor list).  

The special device class ***all*** enables [BLE telemetry](#ble-telemetry) reporting for all BLE device classes.

# Configuration (work in progress)

The configuration of Aruba IoT integrations consists of two main steps:

1. IoT radio-side configuration
2. IoT server-side configuration

Depending on respective IoT solution different configuration settings are required.

>***Note:***  
>The IoT radio settings for USB/3rd party radios are controlled on the 3rd party system, if any, and there is no configuration required on the Aruba side. The only exception is the [SES Imagotag ESL configuration](#ses-imagotag-esl-configuration) which controls the ESL radio channel.  
>
>Which USB device are allowed to connect to an access point can be controlled by an optional [USB acl profile](#usb-acl-profile) configuration.

|IoT solution|Step 1) [IoT radio-side](#iot-connectivity-radio-side) configuration|Step 2) [IoT server-side](#iot-server-connectivity-server-side) configuration|
|-|-|-|
|Wi-Fi solutions|Enable Wi-Fi radios (access or monitor mode)|[iot transport profile](#iot-transport-profile)|
|BLE solutions|[iot radio profile](#iot-radio-profile)|[iot transport profile](#iot-transport-profile)|
|ZigBee solutions|[iot radio profile](#iot-radio-profile) + [zigbee service profile](#zigbee-service-profile) + [zigbee socket device profile](#zigbee-socket-device-profile)|[iot transport profile](#iot-transport-profile)|
|USB/3rd party: USB-to-serial solutions|[USB acl profile](#usb-acl-profile) (optional, to control allowed USB devices)|[iot transport profile](#iot-transport-profile)|
|USB/3rd party: USB-to-ethernet solutions|[USB acl profile](#usb-acl-profile) (optional, to control allowed USB devices)|[wired-ap profile](#wired-ap-profile)|
|USB/3rd party: SES Imagotag ESLs|[USB acl profile](#usb-acl-profile) (optional, to control allowed USB devices) + [SES Imagotag ESL configuration](#ses-imagotag-esl-configuration)|[SES Imagotag ESL configuration](#ses-imagotag-esl-configuration)|

## IoT radio profile

IoT radio profiles are used to configure the Aruba integrated or external (USB-dongle) IoT radio.

### BLE


```

```

### ZigBee

```

```

## IoT transport profile

The IoT transport profile defines the Aruba IoT server interface  settings.

### Server types

```

```

### Proxy support

```

```

### Authentication/Authorization

```

```

### Device class filter

```

```

## USB ACL profile

```

```

## Wired-AP profile

```

```

## ZigBee service profile

```

```

## ZigBee socket device profile

```

```


## SES Imagotag ESL configuration

```

```


# Configuration Examples

```

```

## Wi-Fi solutions

```

```

### Wi-Fi client tracking

```

```

### Wi-Fi RTLS

```

```

## BLE solutions

```

```

### Aruba Meridian Beacon Management

```

```

### Aruba Meridian Asset Tracking

```

```

### ZF Openmatics

```

```

### BLE telemetry (e.g. HYPROS, PnT, ...)

```

```

### BLE data forwarding (e.g. Minew, Google, ...)

```

```

### BLE connect (e.g. ABB)

```

```

## Zigbee (e.g. ASSA ABLOY)

```

```

## USB/3rd party radio solutions

```

```

### SES Imagotag

```

```

### USB-to-ethernet (e.g.Solu-M, Hanshow, AmberBox, ...)

```

```

### USB-to-serial (e.g. EnOcean, Piera Systems, ...)

```

```

# Appendix

## Aruba Reference Documentation

*  [ArubaOS Online Documentation](https://www.arubanetworks.com/techdocs/ArubaOS_8.7.1_Web_Help/Content/home.htm)
*  [Aruba Instant Online Documentation](https://www.arubanetworks.com/techdocs/Instant_871_WebHelp/Content/homeinstant.htm)

### Importing Certificates

* [AurbaOS Importing Certificates](https://www.arubanetworks.com/techdocs/ArubaOS_8.7.1_Web_Help/Content/arubaos-solutions/manage-utilities/impo-cert.htm)  
* [Aruba Instant Importing Certificates](https://www.arubanetworks.com/techdocs/Instant_871_WebHelp/Content/instant-ug/authentication/upload-cert.htm)

### Aruba IoT Server Interface Guide

* [ArubaOS WLAN and Aruba Instant 8.6.0.x IoT Interface Guide](https://asp.arubanetworks.com/downloads;pageSize=25;search=iot)

### Aruba IoT Telemetry JSON Schema

* [ArubaOS WLAN and InstantOS 8.6.0.x IoT Interface - JSON Schema Telemetry](https://asp.arubanetworks.com/downloads;pageSize=25;search=iot)
* [ArubaOS WLAN and InstantOS 8.6.0.x IoT Interface - JSON Telemetry Example](https://asp.arubanetworks.com/downloads;pageSize=25;search=iot)

### Aruba IoT Protobuf Specification

* [ArubaOS WLAN and InstantOS 8.6.0.x IoT Interface - Protobuf Specification](https://asp.arubanetworks.com/downloads;pageSize=25;search=iot)

### Azure IoT Hub Integration

* [Azure IoT Hub Integration Tech Note]() 

## Aruba IoT server interface - connection types

|Server connection type|Transport protocol|Data encapsulation|Authentication & Authorization|Supported device class filter|Description|
|-|-|-|-|-|-|
|Assa-Abloy|HTTPS|vendor specific|username/password, access_id|assa-abloy|Assa Abloy Visiononline server|
|[Azure-IoTHub](#azure-iothub)|AMQP over secure web socket|JSON|symmetric group key|all BLE types, serial-data|Connect with Azure IoT Hub|
|Meridian-Beacon-Management|secure web socket (wss)|vendor specific|static access token|aruba-beacons|POST to a RESTful Meridian API|
|Meridian-Asset-Tracking|secure web socket (wss)|vendor specific|client_id/secret|aruba-tags|Stream data to Meridian WebSocket server|
|[Telemetry-Https](#telemetry-https)|HTTP, HTTPS|JSON|username/password, client_id/secret, static access token|all BLE types, wifi-assoc-sta, wifi-unassoc-sta|POST Aruba IoT telemetry reports to HTTP server endpoint|
|[Telemetry-Websocket](#telemetry-websocket)|web socket (ws), secure web socket (wss)|Protocol Buffers (protobuf)|username/password, client_id/secret, static access token|all BLE types, wifi-tags, serial-data, zsd (ZigBee)|Stream data payloads to Aruba IoT interface compatible web socket server|
|ZF-Openmatics|secure web socket (wss)|vendor specific|username/password|zf-tags|ZF Openmatics cloud management|

## Supported IoT vendor/device class list

|Device class|IoT connectivity (radio)|Supported server connectivity|Minimum required SW version|Description|
|-|-|-|-|-|
|aruba-beacons|BLE|Meridian-Beacon-Management, [Telemetry-Https](#telemetry-https), [Telemetry-Websocket](#telemetry-websocket), [Azure-IoTHub](#azure-iothub)|8.4.0.0 or higher|Forward Aruba beacon BLE device data payloads|
|aruba-tags|BLE|Meridian-Asset-Tracking, [Telemetry-Https](#telemetry-https),[Telemetry-Websocket](#telemetry-websocket), [Azure-IoTHub](#azure-iothub)|8.4.0.0 or higher|Forward Aruba tag BLE device data payloads|
|aruba-sensors|BLE|[Telemetry-Https](#telemetry-https), [Telemetry-Websocket](#telemetry-websocket), [Azure-IoTHub](#azure-iothub)|8.5.0.0 or higher|Forward Aruba sensor BLE device data payloads|
|ibeacon|BLE|[Telemetry-Https](#telemetry-https), [Telemetry-Websocket](#telemetry-websocket), [Azure-IoTHub](#azure-iothub)|8.4.0.0 or higher|Forward iBeacon BLE device data payloads|
|eddystone|BLE|[Telemetry-Https](#telemetry-https), [Azure-IoTHub](#azure-iothub), [Telemetry-Websocket](#telemetry-websocket), [Azure-IoTHub](#azure-iothub)|8.4.0.0 or higher|Forward Eddystone BLE device data payloads|
|zf-tags|BLE|ZF-Openmatics or [Telemetry-Https](#telemetry-https), [Telemetry-Websocket](#telemetry-websocket), [Azure-IoTHub](#azure-iothub)|8.3.0.0 or higher|Forward ZF-Openmatics tag BLE device data payloads|
|enocean-sensors|BLE|[Telemetry-Https](#telemetry-https), [Telemetry-Websocket](#telemetry-websocket), [Azure-IoTHub](#azure-iothub)|8.4.0.0 or higher|Forward EnOcean sensor BLE device data payloads|
|enocean-switches|BLE|[Telemetry-Https](#telemetry-https), [Telemetry-Websocket](#telemetry-websocket), [Azure-IoTHub](#azure-iothub)|8.4.0.0 or higher|Forward EnOcean switch BLE device data payloads|
|mysphera|BLE|[Telemetry-Https](#telemetry-https), [Telemetry-Websocket](#telemetry-websocket), [Azure-IoTHub](#azure-iothub)|8.6.0.0 or higher|Forward MySphera BLE device data payloads|
|ability-smart-sensor|BLE|[Telemetry-Https](#telemetry-https), [Telemetry-Websocket](#telemetry-websocket)|8.6.0.0 or higher|Forward ABB sensor BLE device data payloads|
|sbeacon|BLE|[Telemetry-Https](#telemetry-https), [Telemetry-Websocket](#telemetry-websocket), [Azure-IoTHub](#azure-iothub)|8.6.0.0 or higher|Forward sBeacon(HID) BLE device data payloads|
|wiliot|BLE|[Telemetry-Https](#telemetry-https), [Telemetry-Websocket](#telemetry-websocket), [Azure-IoTHub](#azure-iothub)|8.8.0.0 or higher|Forward Wiliot BLE device data payloads|
|exposure-notification|BLE|[Telemetry-Https](#telemetry-https), [Telemetry-Websocket](#telemetry-websocket), [Azure-IoTHub](#azure-iothub)|8.7.0.0 or higher|Forward Apple/Google exposure notification framework BLE device data payloads|
|blyott|BLE|[Telemetry-Https](#telemetry-https), [Telemetry-Websocket](#telemetry-websocket), [Azure-IoTHub](#azure-iothub)|8.8.0.0 or higher|Forward Blyott BLE device data payloads|
|diract|BLE|[Telemetry-Https](#telemetry-https), [Telemetry-Websocket](#telemetry-websocket), [Azure-IoTHub](#azure-iothub)|8.8.0.0 or higher|Forward Diract BLE device data payloads|
|google|BLE|[Telemetry-Https](#telemetry-https), [Telemetry-Websocket](#telemetry-websocket), [Azure-IoTHub](#azure-iothub)|8.8.0.0 or higher|Forward Google BLE device data payloads|
|gwahygiene|BLE|[Telemetry-Https](#telemetry-https), [Telemetry-Websocket](#telemetry-websocket), [Azure-IoTHub](#azure-iothub)|8.8.0.0 or higher|Forward GWA Hygiene BLE device data payloads|
|minew|BLE|[Telemetry-Https](#telemetry-https), [Telemetry-Websocket](#telemetry-websocket), [Azure-IoTHub](#azure-iothub)|8.8.0.0 or higher|Forward Ninew BLE device data payloads|
|onity|BLE|[Telemetry-Https](#telemetry-https), [Telemetry-Websocket](#telemetry-websocket), [Azure-IoTHub](#azure-iothub)|8.8.0.0 or higher|Forward Onity BLE device data payloads|
|polestar|BLE|[Telemetry-Https](#telemetry-https), [Telemetry-Websocket](#telemetry-websocket), [Azure-IoTHub](#azure-iothub)|8.8.0.0 or higher|Forward Polestar BLE device data payloads|
|unclassified|BLE|[Telemetry-Https](#telemetry-https), [Telemetry-Websocket](#telemetry-websocket), [Azure-IoTHub](#azure-iothub)|8.4.0.0 or higher|all BLE devices we don’t know|
|all|BLE|[Telemetry-Https](#telemetry-https), [Telemetry-Websocket](#telemetry-websocket), [Azure-IoTHub](#azure-iothub)|8.4.0.0 or higher|all BLE devices form known vendors|
|assa-abloy|ZigBee|Assa-Abloy|8.6.0.0 or higher|Forwarding ASSA-ABLOY to Assa Abloy Visiononline server|
|zsd|ZigBee|[Telemetry-Websocket](#telemetry-websocket)|8.7.0.0 or higher|Forwarding ZigBee data payloads to an ZigBee application server|
|serial-data|USB/3rd party|[Telemetry-Websocket](#telemetry-websocket), [Azure-IoTHub](#azure-iothub)|8.7.0.0 or higher|Forwarding serial data payloads of 3rd party USB extensions to an IoT system|
|wifi-assoc-sta|Wi-Fi|[Telemetry-Websocket](#telemetry-websocket)|8.6.0.0 or higher|Forwarding Wi-Fi client RSSI information to 3rd party|
|wifi-unassoc-sta|Wi-Fi|[Telemetry-Websocket](#telemetry-websocket)|8.6.0.0 or higher|Forwarding Wi-Fi client RSSI information to 3rd party|
|wifi-tags|Wi-Fi|[Telemetry-Websocket](#telemetry-websocket)|8.6.0.0 or higher|Forwarding Wi-Fi tag data to 3rd party system|

## Supported USB vendor list for IoT

|Vendor|Minimum required AOS/Instant Version|Connection method|Description|
|-|-|-|-|
| SES Imagotag|8.4.0.0 or higher|[vendor-specific](#vendor-specific-implementations)| ESL USB dongle (on-premise mgmt) |
| SES Imagotag|8.8.0.0 or higher|[vendor-specific](#vendor-specific-implementations)| ESL USB dongle (cloud mgmt) |
| Solu-M|8.5.0.0 or higher|[usb-to-ethernet](#usb-to-ethernet)| ESL Solu-M USB Gen1 GW|
| Solu-M|8.8.0.0 or higher|[usb-to-ethernet](#usb-to-ethernet)| ESL Solu-M NEWTON USB Gen2 GW|
| Hanshow|8.6.0.0 or higher|[usb-to-ethernet](#usb-to-ethernet)| ESL USB dongle |
| AmberBox|8.6.0.0 or higher|[usb-to-ethernet](#usb-to-ethernet)| Gunshot detector |
| EnOcean|8.7.1.0 or higher|[usb-to-serial](#usb-to-serial)|EnOcean USB 800/900 MHz |
| Piera Systems|8.8.0.0 or higher|[usb-to-serial](#usb-to-serial)|Particulate Matter (PM) Detection |
