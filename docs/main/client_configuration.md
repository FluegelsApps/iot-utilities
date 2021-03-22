# Client configuration

The app client configuration feature provides templates for the configuration of an Aruba infrastructure for use with this app or other 3rd party IoT solutions. The term _client_ revers to the ArubaOS Controller or Aruba Instant access point.  
Even if the app only supports part of the IoT use cases, BLE and Wi-Fi, this documentation provides an overview of the available configuration options.

## Templates

The templates are provided as a configuration help for ArubaOS and Aruba Instant deployments as is without any warranty or support at best effort. ArubaOS/Aruba Instant software version dependencies or deployment specific requirements of the used Aruba infrastructure might require custom changes to the provided template configuration.

The templates are hosted on Github here: [Config Templates](https://github.com/FluegelsApps/iot-utilities/tree/main/ConfigTemplates)

### Placeholder/custom settings

The templates include placeholders for setup specific settings. Some of the placeholders are automatically replaced when opened in the app or the app web dashboard with the respective IoT-Utilities app settings e.g. the IP-address for ease of use. Some of the placeholders have to be manually replaced with the required values e.g. ap-group.

|Placeholder|Replacement mode|Description|
|-|-|-|
|ip-address|auto|IP address of the smartphone the apps IoT-server listens on for connections|
|port|auto|Destination port the apps IoT-server listens on for connections|
|username|auto|The username setup in the app for authentication with username/password|
|password|manual|The password setup in the app for authentication with username/password|
|clientid|manual|The client id that should be used by the Aruba infrastructure when when connecting to the apps IoT-server|
|access-token|auto|The static token setup in the app for token authentication|
|interval|auto|The report interval used by the Aruba infrastructure for telemetry reports|
|ap-group|manual|The AP group the IoT transport profile configuration should be applied to. **Only applicable to ArubaOS.**|  
| | |  

> **_Note:_** The _password_ has to be replaced with the password that as been configured in the app settings. The app has no access to the configured password ans only uses a hashed representation for authentication.

## Principal concepts of Aruba IoT configuration

This chapter describes the principals of the Aruba IoT configuration.

[Aruba, a Hewlett Packard Enterprise (HPE) company](https://www.arubanetworks.com/) supports IoT applications based on Wi-Fi (e.g. Wi-Fi tracking), BLE (e.g. asset tracking or sensor monitoring), ZigBee and 3rd party protocols via USB-extension by providing the connection layer using Aruba access points. IoT devices can send/receive data via the Aruba APs built-in radios or supported 3rd party radios connected via USB to 3rd party backend system.

![Aruba IoT Connectivity options](https://github.com/FluegelsApps/iot-utilities/raw/documentation-dev/docs/images/aruba_iot_connectivity.jpg)

The Aruba AP radios can be used as transmitter/receiver (e.g. BLE connect, ZigBee) or just a receiver/sensor (e.g. BLE asset tracking, Wi-Fi tracking), depending on the respective IoT solution. With that the AP provides a one-way or two-way communication channel between IoT devices (e.g, sensors, actors) and IoT systems.  
The access point works as protocol translational gateway between the different downstream protocols/radios and the upstream Aruba IoT interface protocol or plain IP protocol depending on the respective IoT solution being used.  

### IoT connectivity options (downstream)

---

In the downstream direction the Aruba access points support different IoT radio technologies either though integrated radios or 3rd party solutions connected to the APs USB port.

#### Wi-Fi

The Aruba access point Wi-Fi radios can be used to forward associated/unassociated client information and RTLS data for Wi-Fi based tracking use cases. Wi-Fi client and RTLS data is encapsulated in the Aruba IoT interface protocol and forwarded upstream to the IoT backend system.  

#### Aruba IoT radio

An Aruba IoT radio is an additional internal or external radio in the Aruba AP-3xx/5xx series access points that can be leveraged for IoT connectivity.  
A single Aruba AP-3xx/5xx series access points can support up to two IoT radios, one internal and one external. This would used cases where one radio could be used for BLE and another for ZigBee for example.  
The access point removes/adds the radio specific headers downstream from/to IoT devices e.g. BLE or ZigBee and forwards/receives the data payload encapsulated in the Aruba IoT interface protocol upstream to/from the IoT backend system.  

##### **Integrated**

Aruba AP-3xx/5xx series access points provide an integrated Aruba IoT radio for downstream IoT connectivity supporting the following radio technologies:

- AP-3xx: BLE4 (Gen1)
- AP-5xx: BLE5/802.15.4 (Gen2) e.g. ZigBee

##### **External**

In addition to the internal IoT radio Aruba also provides [IoT expansion radio](https://www.arubanetworks.com/assets/ds/DS_IoT-Expansion-Radio.pdf) supports the same radio technologies as the AP-5xx series access points:  

- Aruba IoT Expansion Radio = BLE5/802.15.4 (Gen2) e.g. ZigBee

> **_Note:_** The internal and the expansion BLE5/802.15.4 (Gne2) IoT radio can only run in BLE or ZigBee mode at any point in time. Running both protocols in parallel is currently not supported (even if this options is available in the configuration).  

#### USB/3rd party IoT radios

Aruba supports the extension of Aruba access points using USB with supported 3rd party solutions. Depending on the particular solution the integration uses one of the following methods:

- USB-to-serial
- USB-to-ethernet

In all cases the USB connected host system removes/adds the radio specific headers/protocols downstream from/to IoT devices and forwards/receives the data payload to the access point using one of the USB methods.  

##### **USB-to-serial**

3rd party solutions using the USB-to-serial method forwards the data payload to/from the access point using `serial-data`. The Aruba access point encapsulates the serial-data payload in the Aruba IoT interface protocol upstream to/from the IoT backend system.

##### **USB-to-ethernet**

3rd party solutions using the USB-to-ethernet method provide ethernet/IP connectivity to the connected USB host system. The USB host system is connected to the access point in the same way as a wired client. No data processing is done by the access point and ethernet/IP data packets form the USB host system is forwarded like any other ethernet/IP traffic.

##### **Vendor specific implementations**

USB based integrations that do not follow the previously mentioned methods use vendor specific implementations requiring dedicated configurations.  

- SES Imagotag ESLs

### Server connectivity options (upstream)

---

Data communication from/to an AP is handled via the active controller's corresponding IoT interface connection. In case of a failover the AP communication will also failover to the backup controller IoT interface connection. This is especially important for southbound connection management in IoT solutions.
The different connectivity security options HTTP vs. HTTPS and websocket (ws) vs. secure websocket (wss) have to be explained and thier requirements, e.g. HTTPS/WSS requires a trusted root or self-signed certificate on the controller of the IoT server

- HTTP vs. Websocket

The IoT transport profile section has to provide an explanation about how IoT northbound connections are handled:
Every Aruba controller establishes on IoT interface connection per IoT transport profile to the 3rd party system, e.g. a cluster of 4 controllers creates 4 connections.

#### Connection types

#### Authentication

### Data forwarding options

---

Telemetry vs. data forwarding
northbound vs. southbound

#### Telemetry

#### Data forwarding

##### BLE

##### Serial-data

##### BLE data

#### BLE connect

#### ZigBee

### Data filtering (Device Class Filter)

---

- BLE table limit: 512
- Oldest entries are deleted
- Maximum of 16 devices classes can be selected.
- Explain all = all BLE vendors

AOS/Instant 8.8 (Beta) - Device Class Filter

- aruba-beacons (BLE)
- aruba-sensors (BLE – Aruba developed format, only one known beacon vendor support it so far)
- aruba-tags (BLE)
- ibeacon (BLE)
- eddystone (BLE)
- zf-tags (BLE)
- enocean-sensors (BLE)
- enocean-switches (BLE)
- mysphera (BLE)
- ability-smart-sensor (BLE)
- sbeacon (BLE)
- wiliot (BLE)
- exposure-notification (BLE)
- blyott (BLE)
- diract (BLE?)
- google (BLE)
- gwahygiene (BLE)
- minew (BLE)
- onity (BLE)
- polestar (BLE)
- unclassified (all BLE devices we don’t know)
- all (= all BLE devices form vendors we know)
- assa-abloy (ZigBee)
- zsd (ZigBee)
- serial-data (Serial)
- wifi-tags (Wi-Fi)
- wifi-assoc-sta (Wi-Fi)
- wifi-unassoc-sta (Wi-Fi)

## Configuration

### IoT radio profile

---

IoT radio profiles are used to configure the Aruba integrated or external (USB-dongle) IoT radio - please don't use the term "ZigBee USB dongle", it is misleading because the Aruba IoT radio is either BLE 4.x-only (Gen1 = AP 3xx series) or BLE5/802.15.4 (e.g. to support ZigBee)

### IoT transport profile

---

The IoT transport profile defines the Aruba IoT Interface API settings (some settings also influence the radios side - input filters, but this is a detail that have to be covert in the details section) 

Performance and limitations (e.g. max 4 IoT transport profiles per AP group)

#### Server types

#### Proxy support

#### Authentication/Authorization

#### Device class filter

#### USB ACL configuration

#### USB Ethernet configuration

Wired-AP profile

## Configuration Examples

- Wi-Fi tracking solutions
- BLE solutions
- Aruba Meridian
- Proprietary implementations (ZF Openmatics)
- BLE telemetry (northbound)
- BLE data (northbound)
- BLE connect (southbound)
- Summary of all supported BLE vendors (the list below is still not complete and should already include 8.8)
- ZigBee solutions
- 3rd party radio solutions

## Appendix

### Supported BLE vendor list

### Supported USB vendor list

|Vendor|Connection method|Description|
|-|-|-|
| EnOcean|serial-data| EnOcean USB 800/900 MHz |
| Piera Systems|serial-data| Particulate Matter (PM) Detection |
| SES Imagotag|vendor-specific| ESL USB dongle |
| Solu-M|usb-ethernet| ESL USB dongle gen1/gen2 |
| Hanshow|usb-ethernet| ESL USB dongle |
| AmberBox|usb-ethernet| Gunshot detector |
