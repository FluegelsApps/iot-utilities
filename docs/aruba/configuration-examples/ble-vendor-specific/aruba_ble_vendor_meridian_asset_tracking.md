---
layout: default
title: Aruba Meridian Asset Tracking
has_children: false
parent: BLE Vendor Specific Solutions
grand_parent: Aruba IoT Config Examples
nav_order: 1
---

# Aruba Meridian Asset Tracking

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

This example shows the required configuration to enable [Aruba Meridian Asset Tracking](https://www.arubanetworks.com/products/location-services/beacons-tags/tags/).
For more details on the Aruba Meridian related confiugration please refer to the [Aruba Meridian Online Documenation - Configure Aruba Hardware](#aruba-meridian-online-documenation---configure-aruba-hardware)

>***Note:***  
>The [DigiCert root certificate](https://www.digicert.com/kb/digicert-root-certificates.htm) has to be installed on the Aruba infrastructure when connecting the Meridian tags server. This is only required for the asset tracking tunnels to Meridian using WebSocket Secure (wss) protocol. Please see the [Aruba CLI Reference - Importing Certificates](#aruba-cli-reference---importing-certificates) for details.

>***Note:***
>The [Aruba Meridian Beacon Management configuration](#aruba-meridian-beacon-management) is required for both beacons management and asset tracking because it reports beacon and tag information such as hardware type, battery level, MAC address, uuid/major/minor, rssi, firmware, etc. to Meridian. Whereas the **Aruba Meridian Asset Tracking** only reports tag telemetry data to Meridian. So, whether you are doing beacons management or asset tracking, you must have a least the beacons management iot profile configured.

-   `access-token` - has to be replaced with the static access token generated using the Meridian Beacon Management menu
-   `client-id` - has to be replaced with the Meridian location id which can be found in the Meridian Editor settings page
-   `ap-group` - has to be replaced with the AP group name the configuration should be enabled on (multiple statements are required for multiple groups) (ArubaOS only)

**ArubaOS**

```
iot radio-profile "int-beacon-scan"
    radio-mode none ble
!
ap-group <ap-group>
    iot radio-profile "int-beacon-scan"
!
iot transportProfile "Meridian-Beacon-Management"
    serverURL "https://edit.meridianapps.com/api/beacons/manage"
    accessToken <access-token>
    deviceClassFilter aruba-beacons
    include-ap-group <ap-group>
!
iot useTransportProfile "Meridian-Beacon-Management"
!
iot transportProfile "Meridian-Asset-Tracking"
    serverType Meridian-Asset-Tracking
    serverURL "https://tags.meridianapps.com/api/v1beta1/streams/ingestion.start"
    accessToken <access-token>
    clientId <client-id>
    deviceClassFilter aruba-beacons
    include-ap-group <ap-group>
!
iot useTransportProfile "Meridian-Asset-Tracking"
```

**Aruba Instant**

```
iot radio-profile "int-beacon-scan"
 radio-mode ble
 exit

iot use-radio-profile "int-beacon-scan"

iot transportProfile "Meridian-Beacon-Management"
 endpointURL https://edit.meridianapps.com/api/beacons/manage 
 endpointToken <access-token>
 payloadContent managed-beacons 
 exit

iot useTransportProfile "Meridian-Beacon-Management"

iot transportProfile "Meridian-Asset-Tracking"
 endpointType Meridian-Asset-Tracking
 endpointURL https://tags.meridianapps.com/api/v1beta1/streams/ingestion.start 
 endpointToken <access-token>
 endpointID <client-id>
 payloadContent managed-tags 
 transportInterval 5  
 exit

iot useTransportProfile "Meridian-Asset-Tracking"
```