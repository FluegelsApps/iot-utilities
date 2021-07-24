---
layout: default
title: Configuration Examples
has_children: true
---

# [Configuration Examples](#table-of-contents)

This chapter provides configuration examples for supported IoT solutions and use cases on an Aruba infrastructure.

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