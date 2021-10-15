---
layout: default
title: Blyott (ArubaOS/Aruba Instant 8.9.x.x)
has_children: false
parent: BLE Telemetry Solutions
grand_parent: Aruba IoT Config Examples
nav_order: 1
nav_exclude: true
---

# Blyott (ArubaOS/Aruba Instant 8.9.x.x)

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

This example shows the required configuration to enable the [Blyott location based and monitoring solution](https://blyott.com/) integration using ArubaOS/Aruba Instant version 8.9.x.x.

-   `fqdn, ip-address, port, path` - has to be replaced with the FQDN or IP address, optional port and path of the HYPROS server
-   `client-id` - has to be replaced with the HYPROS customer client id consisting of:  `"<customer-name>-client"`
-   `secret` - has to be replaced with the HYPROS server **client credentials**
-   `ap-group` - has to be replaced with the AP group name the configuration should be enabled on (multiple statements are required for multiple groups) (ArubaOS only)
-   `interval` - has to be replaced with a HYPROS deployment specific reporting interval


>***Note:***  
>The [Baltimore CyberTrust Root certificate (BaltimoreCyberTrustRoot.crt.pem)](https://www.digicert.com/kb/digicert-root-certificates.htm) has to be installed on the Aruba infrastructure when connecting the [ABB Ability™ Smart Sensor platform](https://new.abb.com/motors-generators/service/advanced-services/smart-sensor). Please see the [Aruba CLI Reference - Importing Certificates](../references/aruba_reference_documentation.md#aruba-cli-reference---importing-certificates) for details.

**ArubaOS**

```
iot radio-profile "ble-int"
    radio-mode none ble
!
ap-group <ap-group>
    iot radio-profile "ble-int"
!
iot transportProfile "blyott"
    serverType Telemetry-Websocket
    serverURL "wss://mobileproxy.blyott.com/aruba"
    accessToken "Bly0ttBL3"
    reportingInterval 60
    deviceClassFilter blyott
    ageFilter 30
    rssiReporting last
    include-ap-group <ap-group>
!
iot useTransportProfile "blyott"
```

**Aruba Instant**

```
iot radio-profile "ble-int"
 radio-mode ble
 exit

iot use-radio-profile "ble-int"

iot transportProfile "blyott"
 endpointURL "wss://mobileproxy.blyott.com/aruba"
 endpointType telemetry-websocket
 payloadContent blyott
 endpointToken Bly0ttBL3
 transportInterval 60
 rssiReporting last
 exit

iot useTransportProfile "blyott"
```
