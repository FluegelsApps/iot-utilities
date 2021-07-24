---
layout: default
title: ZF Openmatics
has_children: false
parent: BLE Vendor Specific Solutions
grand_parent: Aruba IoT Config Examples
nav_order: 2
---

# ZF Openmatics

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

This example shows the required configuration to enable [ZF Openmatics asset tracking](https://aftermarket.zf.com/go/en/openmatics/asset-tracking/).

-   `username` - has to be replaced with the **login username** for the ZF deTAGtive platform
-   `password` - has to be replaced with the **login password** for the ZF deTAGtive platform
-   `ap-group` - has to be replaced with the AP group name the configuration should be enabled on (multiple statements are required for multiple groups) (ArubaOS only)

>***Note:***  
>The [DigiCert root certificate](https://www.digicert.com/kb/digicert-root-certificates.htm) has to be installed on the Aruba infrastructure when connecting the ZF Openmatics [deTAGtiv platform](https://app.detagtive.com/). Please see the [Aruba CLI Reference - Importing Certificates](#aruba-cli-reference---importing-certificates) for details.

**ArubaOS**

```
iot radio-profile "int-scan"
    radio-mode none ble
    ble-opmode scanning
!
ap-group <ap-group>
    iot radio-profile "int-scan"
!
iot transportProfile "ZF-Openmatics-deTAGtive"
    serverType ZF-Openmatics
    serverURL "https://app.detagtive.com/backend/"
    username <username>
    password <password>
    reportingInterval 5
    deviceClassFilter zf-tags
    include-ap-group <ap-group>
!
iot useTransportProfile "ZF-Openmatics-deTAGtive"
```

**Aruba Instant**

```
iot radio-profile "int-scan"
 radio-mode ble
 ble-opmode scanning
 exit

iot use-radio-profile "int-scan"

iot transportProfile "ZF-Openmatics-deTAGtive"
 endpointURL https://app.detagtive.com/backend/
 endpointType ZF
 payloadContent zf-tags
 username <username>
 password <password>
 transportInterval 5
 exit

iot useTransportProfile "ZF-Openmatics-deTAGtive"
```