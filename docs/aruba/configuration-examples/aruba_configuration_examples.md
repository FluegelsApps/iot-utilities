---
layout: default
title: Configuration Examples
has_children: true
---

# [Configuration Examples](#table-of-contents)

This chapter provides configuration examples for supported IoT solutions and use cases on an Aruba infrastructure.

## [BLE data forwarding solutions](#table-of-contents)

### [Azure IoT Hub (ble data)](#table-of-contents)

This example shows the required configuration to enable [BLE data forwarding](#ble-data-forwarding) for `all` supported [BLE vendors](#supported-iot-vendordevice-class-list) to Azure IoT Hub.

-   `scope-id` - has to be replaced with Azure DPS enrollment group scope-id
-   `key` - has to be replaces with Azure symmetric group key
-   `ap-group` - has to be replaced with the AP group name the configuration should be enabled on (multiple statements are required for multiple groups) (ArubaOS only)

>***Note:***  
>`bleDataForwarding` is enabled by default for server type `Azure-IoTHub` and cannot be disabled.

>***Caution:***  
>Enabling the **device class filter** `all` will enable BLE data forwarding of all knon/supported [BLE vendor device classes](#supported-iot-vendordevice-class-list). This could haveally increase the amount of data beeing forwarded to the remote server because all BLE advertisements and scan respsonse packets are forwarded in near real time.  
It is recommended to use the [BLE device class filter](#ble-device-class-filter) and [BLE data filters ](#ble-data-filter) to filter the data being forwarded.

**ArubaOS**

```
iot radio-profile "int-scan"
    radio-mode none ble
    ble-opmode scanning
!
ap-group <ap-group>
    iot radio-profile "int-scan"
!
iot transportProfile "Azure-IoT-Hub-ble-data"
    serverType Azure-IoTHub
    deviceClassFilter all
    bleDataForwarding
    azure-dps-id-scope <scope-id>
    azure-dps-auth-type group-enrollment symmetric-key <key>
    include-ap-group <ap-group>
!
iot useTransportProfile "Azure-IoT-Hub-ble-data"
```

**Aruba Instant**

```
iot radio-profile "int-scan"
 radio-mode ble
 ble-opmode scanning
 exit

iot use-radio-profile "int-scan"

iot transportProfile "Azure-IoT-Hub-ble-data"
 endpointType Azure-IoTHub
 payloadContent all
 bleDataForwarding
 azure-dps-id-scope <scope-id>
 azure-dps-auth-type group-enrollment symmetric-key <key>
 exit

iot useTransportProfile "Azure-IoT-Hub-ble-data"
```

## [BLE connect solutions](#table-of-contents)

### [ABB (ArubaOS/Aruba Instant 8.7.x.x)](#table-of-contents)

This example shows the required configuration to enable the [ABB Ability™ Smart Sensor](https://new.abb.com/motors-generators/service/advanced-services/smart-sensor) integrartion using ArubaOS/Aruba Instant version 8.7.x.x.

-   `client-id` - has to be replaced with the ABB Ability™ account organization ID
-   `username` - has to be replaced with the **email address** of the ABB Ability™ account
-   `password` - has to be replaced with the **login password** of the ABB Ability™ account
-   `ap-group` - has to be replaced with the AP group name the configuration should be enabled on (multiple statements are required for multiple groups) (ArubaOS only)

>***Note:***  
>The [ABB Ability™ Smart Sensor](https://new.abb.com/motors-generators/service/advanced-services/smart-sensor) integrartion is levaraging the [BLE data forwarding service](#ble-data-forwarding) which is enabled by default for the device class *ability-smart-sensor* in ArubaOS/Aruba Instant 8.7.x.x. There is manual configuration supported for BLE data forwarding in this version.

>***Note:***  
>The [Baltimore CyberTrust Root certificate (BaltimoreCyberTrustRoot.crt.pem)](https://www.digicert.com/kb/digicert-root-certificates.htm) has to be installed on the Aruba infrastructure when connecting the [ABB Ability™ Smart Sensor platform](https://new.abb.com/motors-generators/service/advanced-services/smart-sensor). Please see the [Aruba CLI Reference - Importing Certificates](#aruba-cli-reference---importing-certificates) for details.

**ArubaOS**

```
iot radio-profile "int-beacon-scan"
    radio-mode none ble
!
ap-group <ap-group>
    iot radio-profile "int-beacon-scan"
!
iot transportProfile "ABB-Ability-Smart-Sensor"
    serverType Telemetry-Websocket
    serverURL "https://api.smartsensor.abb.com/v7/Auth/BearerOAuth2"
    clientId <client-id>
    username <username>
    password <password>
    reportingInterval 3600
    deviceClassFilter ability-smart-sensor
    authenticationURL "https://api.smartsensor.abb.com/v7/Auth/BearerOAuth2"
    include-ap-group <ap-group>
!
iot useTransportProfile "ABB-Ability-Smart-Sensor"
```

**Aruba Instant**

```
iot radio-profile "int-beacon-scan"
  radio-mode ble
 exit

iot use-radio-profile "int-beacon-scan"

iot transportProfile "ABB-Ability-Smart-Sensor"
 endpointURL "https://api.smartsensor.abb.com/v7/Auth/BearerOAuth2"
 endpointType telemetry-websocket
 payloadContent ability-smart-sensor
 endpointID <client-id>
 username <username>
 password <password>
 transportInterval 3600
 authenticationURL "https://api.smartsensor.abb.com/v7/Auth/BearerOAuth2"
 exit

iot useTransportProfile "ABB-Ability-Smart-Sensor"
```

### [ABB (ArubaOS/Aruba Instant 8.8.x.x or higher)](#table-of-contents)

This example shows the required configuration to enable the [ABB Ability™ Smart Sensor](https://new.abb.com/motors-generators/service/advanced-services/smart-sensor) integrartion using ArubaOS/Aruba Instant version 8.8.x.x or higher.

-   `client-id` - has to be replaced with the ABB Ability™ account organization ID
-   `secret` - has to be replaced with the **client credentials** of the ABB Ability™ account
-   `ap-group` - has to be replaced with the AP group name the configuration should be enabled on (multiple statements are required for multiple groups) (ArubaOS only)

>***Note:***  
>The [ABB Ability™ Smart Sensor](https://new.abb.com/motors-generators/service/advanced-services/smart-sensor) integrartion is levaraging the [BLE data forwarding service](#ble-data-forwarding). Starting with ArubaOS/Aruba Instant 8.8.x.x or higher [BLE data forwarding](#ble-data-forwarding) is disabled by default and has to be explicitely eanbled for the device class *ability-smart-sensor*.  
>When migrating form ArubaOS/Aruba Instant 8.7.x.x to 8.8.x.x the iot transport profile configuration has to be adapgted to continue to work!

>***Note:***  
>The [Baltimore CyberTrust Root certificate (BaltimoreCyberTrustRoot.crt.pem)](https://www.digicert.com/kb/digicert-root-certificates.htm) has to be installed on the Aruba infrastructure when connecting the [ABB Ability™ Smart Sensor platform](https://new.abb.com/motors-generators/service/advanced-services/smart-sensor). Please see the [Aruba CLI Reference - Importing Certificates](#aruba-cli-reference---importing-certificates) for details.

**ArubaOS**

```
iot radio-profile "int-beacon-scan"
    radio-mode none ble
!
ap-group <ap-group>
    iot radio-profile "int-beacon-scan"
!
iot transportProfile "ABB-Ability-Smart-Sensor"
    serverType Telemetry-Websocket
    serverURL "https://api.smartsensor.abb.com/v8/Auth/BearerOAuth2"
    clientId <client-id>
    client-secret <secret>
    reportingInterval 3600
    deviceClassFilter ability-smart-sensor
    bleDataForwarding
    authenticationURL "https://api.smartsensor.abb.com/v8/Auth/BearerOAuth2"
    authentication-mode client-credentials
    include-ap-group <ap-group>
!
iot useTransportProfile "ABB-Ability-Smart-Sensor"
```

**Aruba Instant**

```
iot radio-profile "int-beacon-scan"
 radio-mode ble
 exit

iot use-radio-profile "int-beacon-scan"

iot transportProfile "ABB-Ability-Smart-Sensor"
 endpointURL "https://api.smartsensor.abb.com/v8/Auth/BearerOAuth2"
 endpointType telemetry-websocket
 payloadContent ability-smart-sensor
 bleDataForwarding
 endpointID <client-id>
 client-secret <secret>
 transportInterval 3600
 authenticationURL "https://api.smartsensor.abb.com/v8/Auth/BearerOAuth2"
 authentication-mode client-credentials
 exit

iot useTransportProfile "ABB-Ability-Smart-Sensor"
```

## [USB vendor specific solutions](#table-of-contents)

### [SES Imagotag](#table-of-contents)

This example shows the required configuration to enable an [SES-Imagotag ESL soulution](https://www.arubanetworks.com/assets/pso/PSB_SESImagotag.pdf) on premise solution. All avaialbe confiugation options are descirbed in the [SES Imagotag ESL configuration](#ses-imagotag-esl-configuration)

-   `<ip-address>` - has to be replaced with the SES-Imagotag on-premises server IP address

**ArubaOS**

```
ap system-profile "iot-ap-system-prof"
    sesImagotag-esl-serverip <ip-address>
    sesImagotag-esl-channel 127
```

**Aruba Instant**

```
sesimagotag-esl-profile
 sesImagotag-esl-serverip <ip-address>
 sesimagotag-esl-channel 127
```

## [USB-to-ethernet solutions](#table-of-contents)

### [Solu-M ESL](#table-of-contents)

This example shows the required configuration to enable the [Solu-M ESL soltuion](https://solumesl.com/).

-   `vlan-id` - has to be replaced with the desired access vlan id to be used for the ESL USB gateway
-   `ap-group` - has to be replaced with the AP group name the configuration should be enabled on (multiple statements are required for multiple groups) (ArubaOS only)

>***Note:***  
>The ArubaOS configuration tunnels the ESL USB gateway traffic to the Aruba controller into the vlan `vlan-id` controlled though the controller firewall.  
>
>The Aruba Instant configration egress the ESL USB gateway traffic at the access point uplink port into the desired vlan (tagged). The AP's uplink switche port has to allow the `vlan-id` tagged.  

**ArubaOS**

```
ap usb-acl-prof "Solu-M-USB-GW-acl"
    rule vendor All action permit
!
ap usb-profile "Solu-M-USB-GW"
    usb-acl-profile "Solu-M-USB-GW-acl"
!
ap-group <ap-group>
    usb-profile "Solu-M-USB-GW"
!
ip access-list session allowall
    any any any permit
    ipv6 any any any permit
!
user-role Solu-M-USB-GW
    access-list session allowall
!
aaa profile "Solu-M-USB-GW_aaa_prof"
    initial-role "Solu-M-USB-GW"
!
ap wired-ap-profile "Solu-M-USB-GW-wiredApProf"
    wired-ap-enable
    switchport access vlan <vlan-id>
!
ap wired-port-profile "Solu-M-USB-GW-wiredPortProf"
    wired-ap-profile "Solu-M-USB-GW-wiredApProf"
    aaa-profile "Solu-M-USB-GW_aaa_prof"
!
ap-group <ap-group>
    enet-usb-port-profile "Solu-M-USB-GW-wiredPortProf"
!
```

**Aruba Instant**

```
usb acl-profile "Solu-M-USB-GW-acl"
 rule Solu-M-SLG-DM101 permit
 exit

usb profile "Solu-M-USB-GW"
 usb-acl "Solu-M-USB-GW-acl"
 exit

usb-profile-binding "Solu-M-USB-GW"

wlan access-rule "Solu-M-USB-GW-wiredPortProf"
 rule any any match any any any permit
 exit

wired-port-profile "Solu-M-USB-GW-wiredPortProf"
 switchport-mode access
 allowed-vlan <vlan-id>
 native-vlan <vlan-id>
 no shutdown
 access-rule-name "Solu-M-USB-GW-wiredPortProf"
 type employee
 exit

enet-usb-port-profile "Solu-M-USB-GW-wiredPortProf"
```

## [USB-to-serial solutions](#table-of-contents)

### ***[EnOcean demo](#table-of-contents)***

This example shows the required configuration to enable the [Aruba EnOcean Demo Kit](https://www.enocean.com/en/applications/iot-solutions/).

-   `ip-address` - has to be replaced with the IP address of the windows client the demo software is running on
-   `ap-group` - has to be replaced with the AP group name the configuration should be enabled on (multiple statements are required for multiple groups) (ArubaOS only)

**ArubaOS**

```
iot transportProfile "EnOcean-Demo"
    serverType Telemetry-Websocket
    serverURL "ws://<ip-address>:8000/arubaws"
    accessToken "1234567890"
    clientId "ArubaController"
    deviceClassFilter serial-data
    include-ap-group <ap-group>
!
iot useTransportProfile "EnOcean-Demo"
```

**Aruba Instant**

```
iot transportProfile "EnOcean-Demo"
 endpointURL "ws://<ip-address>:8000/arubaws"
 endpointType telemetry-websocket
 payloadContent serial-data
 endpointToken "1234567890"
 endpointID "ArubaInstant"
 exit

iot useTransportProfile "EnOcean-Demo"
```

### ***[Azure IoT Hub (serial-data)](#table-of-contents)***

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

## [ZigBee solutions](#table-of-contents)

### [ASSA ABLOY](#table-of-contents)

This example shows the required configuration to enable the [ASSA ABLOY](https://www.assaabloyglobalsolutions.com/en/solutions/system-and-software/visionline/) door-lock solution.

-   `fqdn, ip-address` - has to be replaced with the FQDN or IP address of the Assa-Abloy server
-   `username` - has to be replaced with the **username** on the Assa-Abloy server
-   `password` - has to be replaced with the **password** of the Assa-Abloy server
-   `accessid` - has to be replaces with the Assa-Abloy server **access id**
-   `ap-group` - has to be replaced with the AP group name the configuration should be enabled on (multiple statements are required for multiple groups) (ArubaOS only)

**ArubaOS**

```
iot radio-profile "int-zb"
    radio-mode none zigbee
!
zigbee service-profile "int-zb-no-sec-auto"
    radio-instance internal
    security disable
!
ap-group <ap-group>
    iot radio-profile "int-zb"
    zigbee service-profile "int-zb-no-sec-auto"
!
iot transportProfile "Assa-Abloy"
    serverType Assa-Abloy
    serverURL "https://<fqdn|ip-address>[:<port>][<path>]"
    username <username>
    password <password>
    deviceClassFilter assa-abloy
    include-ap-group <ap-group>
    accessID <accessid>
!
iot useTransportProfile "Assa-Abloy"
```

**Aruba Instant**

```
iot radio-profile int-zb
 radio-mode zigbee
 exit

zigbee service-profile int-zb-no-sec-auto
 security disable

iot transportProfile "Assa-Abloy"
 endpointURL "httts://<fqdn|ip-address>[:<port>][<path>]"
 endpointType Assa-Abloy
 payloadContent assa-abloy
 username <username>
 password <password>
 accessID <accessid>
 exit

iot use-radio-profile int-zb

zigbee use-service-profile int-zb-no-sec-auto

iot useTransportProfile "Assa-Abloy"
```

### [Generic ZSD solution](#table-of-contents)

This example shows the required configuration to enable the [ZigBee socket device (ZSD) service](#zigbee-socket-device)

-   `fqdn, ip-address` - has to be replaced with the FQDN or IP address of the remote server
-   `access-token` - has to be replaced with the static access token used to connect to the remote server
-   `client-id` - has to be replaced with the client identifier string that is used by the remote server to identify the connecting Aruba infrastructure
-   `ap-group` - has to be replaced with the AP group name the configuration should be enabled on (multiple statements are required for multiple groups) (ArubaOS only)

**ArubaOS**

```
iot radio-profile "ext-zb"
    radio-instance external
    radio-mode none zigbee
!
zigbee service-profile "ext-zb-sec-auto"
    radio-instance external
!
ap-group <ap-group>
    iot radio-profile "ext-zb"
    zigbee service-profile "ext-zb-sec-auto"
!
zigbee socket-inbound-profile "zb-in-prof-1"
    cluster 2100
	profile 0a1e
    endpoint 242
    source-endpoint 1
!	
zigbee socket-inbound-profile "zb-in-prof-2"
    cluster 1900
	profile 0104
    endpoint 11
    source-endpoint 1
!
zigbee socket-outbound-profile "zb-out-prof-1" 
	cluster 0000
    profile 0104
    endpoint 11
    source-endpoint 1
!
zigbee socket-outbound-profile "zb-out-prof-2" 
	cluster 0003
    profile 0104
    endpoint 11
    source-endpoint 1
!
zigbee socket-outbound-profile "zb-out-prof-3" 
	cluster 0010
    profile 0104
    endpoint 11
    source-endpoint 1
!
zigbee socket-outbound-profile "zb-out-prof-4" 
	cluster 01fc
    profile 0104
    endpoint 11
    source-endpoint 1
!
zigbee socket-device-profile "zb-device-prof-1"
    inbound "zb-in-prof-1"
	outbound "zb-out-prof-1"
	outbound "zb-out-prof-2"
!
zigbee socket-device-profile "zb-device-prof-2"
    inbound "zb-in-prof-2"
	outbound "zb-out-prof-3"
	outbound "zb-out-prof-4"
!
iot transportProfile "ZSD"
    serverType Telemetry-Websocket
    serverURL "[ws|wss]://<fqdn|ip-address>[:<port>][<path>]"
    accessToken <access-token>
    clientId <client-id>
    deviceClassFilter ZSD
    ZSDFilter "zb-device-prof-1"
    ZSDFilter "zb-device-prof-2"
    include-ap-group <ap-group>
!
iot useTransportProfile "ZSD"
```

**Aruba Instant**

```
iot radio-profile ext-zb
 radio-instance external
 radio-mode zigbee
 exit

zigbee service-profile ext-zb-sec-auto
 radio-instance external

zigbee socket-device-profile "zb-device-prof-1"
 inbound 242 1 0a1e 2100
 inbound 11 1 0104 1900
 outbound 1 11 0104 0000
 outbound 1 11 0104 0003
 outbound 1 11 0104 0010
 outbound 1 11 0104 01fc
 exit

iot transportProfile "ZSD"
 endpointURL "[ws|wss]://<fqdn|ip-address>[:<port>][<path>]"
 endpointType telemetry-websocket
 payloadContent zsd
 endpointToken <access-token>
 endpointID <client-id>
 ZSDFilter "zb-device-prof-1"
 exit

iot use-radio-profile ext-zb

zigbee use-service-profile ext-zb-sec-auto

iot useTransportProfile "ZSD"
```

# Verification and troubleshooting

t.b.d.