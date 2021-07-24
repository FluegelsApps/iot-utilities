---
layout: default
title: Aruba Meridian Beacon Management
has_children: false
parent: BLE Vendor Specific Solutions
grand_parent: Configuration Examples
nav_order: 0
---

# Aruba Meridian Beacon Management

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

This example shows the required configuration to enable [Aruba Meridian Beacon Management](https://www.arubanetworks.com/products/location-services/beacons-tags/beacons/).
For more details on the Aruba Meridian related confiugration please refer to the [Aruba Meridian Online Documenation - Configure Aruba Hardware](#aruba-meridian-online-documenation---configure-aruba-hardware)

-   `access-token` - has to be replaced with the static access token generated using the Meridian Beacon Management menu
-   `ap-group` - has to be replaced with the AP group name the configuration should be enabled on (multiple statements are required for multiple groups) (ArubaOS only)

>***Note:***  
>Because the `serverType/endpointType Meridian-Beacon-Managemen` and the `reportingInterval` of **600 s** are the default values, they do not show up in the confiugration.

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
```