---
layout: default
title: iBeacon + EddyStone Asset Tracking
has_children: false
parent: BLE Telemetry Solutions
grand_parent: Aruba IoT Config Examples
nav_order: 0
---

# iBeacon + Eddystone asset tracking

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

This example shows the required configuration to enable [BLE telemety](../iot-concepts/server-connectivity/aruba_iot_transport_services.md#ble-telemetry) reporting for `ibeacon` and `eddystone` BLE devices for asset tracking and eddystone based sensor monitoring.

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