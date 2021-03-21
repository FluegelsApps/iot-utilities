# Client configuration

The app client configuration feature provides templates for the configuration of an Aruba infrastructure for use with this app or other 3rd party IoT solutions.  

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

## Principal Concepts

[Aruba, a Hewlett Packard Enterprise (HPE) company](https://www.arubanetworks.com/) supports IoT applications based on Wi-Fi (e.g. Wi-Fi tracking), BLE (e.g. asset tracking or sensor monitoring), ZigBee and 3rd party protocols via USB-extension by providing the connection layer using Aruba access points.

IoT devices can send/receive data via the Aruba APs built-in radios or supported 3rd party radios connected via USB to 3rd party backend system.

![Aruba IoT Connectivity options](../images/aruba_iot_connectivity.jpg)

The Aruba AP can be used as transmitter/receiver (e.g. BLE connect, ZigBee) or just a receiver/sensor (e.g. BLE asset tracking, Wi-Fi tracking), depending on the respective IoT solution. With that the AP provides a one-way or two-way communication channel between IoT devices (e.g, sensors, actors) and IoT systems.  

### Downstream IoT connectivity options

In the downstream direction the access point works as protocol translational gateway between the different IoT radio technologies and the Aruba IoT interface protocol or plain IP connectivity, depending on respective radio being used.  

#### Aruba IoT radio

The access point removes/adds the radio specific headers downstream from/to IoT devices e.g. BLE or ZigBee in case of the Aruba IoT radio (internal or external) and forwards the data payload encapsulated upstream via the Aruba IoT interface to the IoT backend system.  

##### Integrated  

- AP 3xx - Gen1 = BLE4
- AP 5xx - Gen2 = BLE5/802.15.4 (e.g. ZigBee)

##### External

- Aruba IoT USB dongle - Gen2 = BLE5/802.15.4

#### 3rd party USB

In case of 3rd party radios connected via USB the 3rd party system handles the.

##### USB-serial (e.g. EnOcean USB 900 MHz, ...) -> USB acl profile configuration/explanation

##### USB-ethernet (e.g. ESL, AmberBox, ...) -> USB-to-Ethernet profile configuration

##### Special Cases/Vendor specific implementations

- SES Imagotag is a special case requiring a dedicated configuration

### Upstream Server connectivity options

Data communication from/to an AP is handled via the active controller's corresponding IoT interface connection. In case of a failover the AP communication will also failover to the backup controller IoT interface connection. This is especially important for southbound connection management in IoT solutions.
The different connectivity security options HTTP vs. HTTPS and websocket (ws) vs. secure websocket (wss) have to be explained and thier requirements, e.g. HTTPS/WSS requires a trusted root or self-signed certificate on the controller of the IoT server

- HTTP vs. Websocket

The IoT transport profile section has to provide an explanation about how IoT northbound connections are handled:
Every Aruba controller establishes on IoT interface connection per IoT transport profile to the 3rd party system, e.g. a cluster of 4 controllers creates 4 connections.

#### Connection types

#### Authentication

### Data forwarding options

Telemetry vs. BLE data forwarding

#### Telemetry

#### BLE data

#### BLE connect

### Data filtering (Device Class Filter)

Maximum of 16 devices classes can be selected.
Explain all = all BLE vendors

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

### ArubaOS

#### IoT radio profile

IoT radio profiles are used to configure the Aruba integrated or external (USB-dongle) IoT radio - please don't use the term "ZigBee USB dongle", it is misleading because the Aruba IoT radio is either BLE 4.x-only (Gen1 = AP 3xx series) or BLE5/802.15.4 (e.g. to support ZigBee)

#### IoT transport profile

The IoT transport profile defines the Aruba IoT Interface API settings (some settings also influence the radios side - input filters, but this is a detail that have to be covert in the details section) 

Performance and limitations (e.g. max 4 IoT transport profiles per AP group)

##### Server types

##### Proxy support

##### Authentication/Authorization

##### device class filter

## Configuration Examples

### ArubaOS

### Aruba Instant

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