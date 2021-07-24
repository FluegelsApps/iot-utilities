---
layout: default
title: BLE Telemetry Solutions
has_children: false
parent: Configuration Examples
nav_order: 3
---

# BLE telemetry solutions

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

## iBeacon + Eddystone asset tracking

This example shows the required configuration to enable [BLE telemety](#ble-telemetry) reporting for `ibeacon` and `eddystone` BLE devices for asset tracking and eddystone based sensor monitoring.

-   `fqdn, ip-address, port, path` - has to be replaced with the FQDN or IP address, optional port and path of the remote server
-   `access-token` - has to be replaced with the static access token used to connect to the remote server
-   `client-id` - has to be replaced with the client identifier string that is used by the remote server to identify the connecting Aruba infrastructure
-   `ap-group` - has to be replaced with the AP group name the configuration should be enabled on (multiple statements are required for multiple groups) (ArubaOS only)

**ArubaOS**

```
iot radio-profile "int-scan"
    radio-mode none ble
    ble-opmode scanning
!
ap-group <ap-group>
    iot radio-profile "int-scan"
!
iot transportProfile "BLE-telemetry"
    serverType Telemetry-Websocket
    serverURL "[ws|wss]://<fqdn|ip-address>[:<port>][<path>]"
    accessToken <access-token>
    clientId <client-id>
    reportingInterval 1
    deviceClassFilter ibeacon
    deviceClassFilter eddystone
    ageFilter 30
    rssiReporting last
    include-ap-group <ap-group>
!
iot useTransportProfile "BLE-telemetry"
```

**Aruba Instant**

```
iot radio-profile "int-scan"
 radio-mode ble
 ble-opmode scanning
 exit

iot use-radio-profile "int-scan"

iot transportProfile "BLE-telemetry"
 endpointURL "[ws|wss]://<fqdn|ip-address>[:<port>][<path>]"
 endpointType telemetry-websocket
 payloadContent ibeacon
 payloadContent eddystone
 endpointToken <access-token>
 endpointID <client-id>
 transportInterval 1
 ageFilter 30
 rssiReporting last
 exit

iot useTransportProfile "BLE-telemetry"
```

## HYPROS (ArubaOS/Aruba Instant 8.7.x.x)

This example shows the required configuration to enable the [HYPROS tracking and tracing solutions](https://hypros.de/en/) integrartion using ArubaOS/Aruba Instant version 8.7.x.x.

-   `fqdn, ip-address, port, path` - has to be replaced with the FQDN or IP address, optional port and path of the HYPROS server
-   `client-id` - has to be replaced with the HYPROS customer client id consisting of:  `"<customer-name>-client"`
-   `username` - has to be replaced with the HYPROS server **login username**
-   `password` - has to be replaced with the HYPROS server **login password**
-   `ap-group` - has to be replaced with the AP group name the configuration should be enabled on (multiple statements are required for multiple groups) (ArubaOS only)
-   `interval` - has to be replaced with a HYPROS deployment specific reporting interval
-   `uuid-list` - has to be replaced with a HYPROS deployment specific iBeacon UUID list to filter for, format:  `"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx,yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyyyyyyy"`

>***Note:***  
>The self-signed server certificate of the HYPROS server has to be installed on the Aruba infrastructure for the sercure web socket server connection to be established. Please see the [Aruba CLI Reference - Importing Certificates](#aruba-cli-reference---importing-certificates) for details.

**ArubaOS**

```
iot radio-profile "int-scan"
    radio-mode none ble
    ble-opmode scanning
!
ap-group <ap-group>
    iot radio-profile "int-scan"
!
iot transportProfile "HYPROS"
    serverType Telemetry-Websocket
    serverURL "wss://<fqdn|ip-address>[:<port>][<path>]"
    clientId <client-id>
    username <username>
    password <password>
    reportingInterval <interval>
    deviceClassFilter ibeacon
    authenticationURL "https://<fqdn|ip-address>[:<port>][<path>]"
    uuidFilter <uuid-list>
    ageFilter 30
    rssiReporting last
    include-ap-group <ap-group>
!
iot useTransportProfile "HYPROS"
```

**Aruba Instant**

```
iot radio-profile "int-scan"
 radio-mode ble
 ble-opmode scanning
 exit

iot use-radio-profile "int-scan"

iot transportProfile "HYPROS"
 endpointURL "wss://<fqdn|ip-address>[:<port>][<path>]"
 endpointType telemetry-websocket
 payloadContent ibeacon
 endpointID <client-id>
 username <username>
 password <password>
 transportInterval <interval>
 uuidFilter <uuid-list>
 ageFilter 30
 authenticationURL "https://<fqdn|ip-address>[:<port>][<path>]"
 rssiReporting last
 exit

iot useTransportProfile "HYPROS"
```

## HYPROS (ArubaOS/Aruba Instant 8.8.x.x or higher)

This example shows the required configuration to enable the [HYPROS tracking and tracing solutions](https://hypros.de/en/) integrartion using ArubaOS/Aruba Instant version 8.8.x.x or higher.

-   `fqdn, ip-address, port, path` - has to be replaced with the FQDN or IP address, optional port and path of the HYPROS server
-   `client-id` - has to be replaced with the HYPROS customer client id consisting of:  `"<customer-name>-client"`
-   `secret` - has to be replaced with the HYPROS server **client credentials**
-   `ap-group` - has to be replaced with the AP group name the configuration should be enabled on (multiple statements are required for multiple groups) (ArubaOS only)
-   `interval` - has to be replaced with a HYPROS deployment specific reporting interval
-   `uuid-list` - has to be replaced with a HYPROS deployment specific iBeacon UUID list to filter for, format:  `"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx,yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyyyyyyy"`

>***Note:***  
>The self-signed server certificate of the HYPROS server has to be installed on the Aruba infrastructure for the sercure web socket server connection to be established. Please see the [Aruba CLI Reference - Importing Certificates](#aruba-cli-reference---importing-certificates) for details.

**ArubaOS**

```
iot radio-profile "int-scan"
    radio-mode none ble
    ble-opmode scanning
!
ap-group <ap-group>
    iot radio-profile "int-scan"
!
iot transportProfile "HYPROS"
    serverType Telemetry-Websocket
    serverURL "wss://<fqdn|ip-address>[:<port>][<path>]"
    clientId <client-id>
    client-secret <secret>
    reportingInterval <interval>
    deviceClassFilter ibeacon
    authenticationURL "https://<fqdn|ip-address>[:<port>][<path>]"
    authentication-mode client-credentials
    uuidFilter <uuid-list>
    ageFilter 30
    rssiReporting last
    include-ap-group <ap-group>
!
iot useTransportProfile "HYPROS"
```

**Aruba Instant**

```
iot radio-profile "int-scan"
 radio-mode ble
 ble-opmode scanning
 exit

iot use-radio-profile "int-scan"

iot transportProfile "HYPROS"
 endpointURL "wss://<fqdn|ip-address>[:<port>][<path>]"
 endpointType telemetry-websocket
 payloadContent ibeacon
 endpointID <client-id>
 client-secret <secret>
 transportInterval <interval>
 uuidFilter <uuid-list>
 ageFilter 30
 authenticationURL "https://<fqdn|ip-address>[:<port>][<path>]"
 authentication-mode client-credentials
 rssiReporting last
 exit

iot useTransportProfile "HYPROS"
```