---
layout: default
title: ABB (ArubaOS/Aruba Instant 8.7.x.x)
has_children: false
parent: BLE Connect Solutions
grand_parent: Aruba IoT Config Examples
nav_order: 0
---

# ABB (ArubaOS/Aruba Instant 8.7.x.x)

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

This example shows the required configuration to enable the [ABB Ability™ Smart Sensor](https://new.abb.com/motors-generators/service/advanced-services/smart-sensor) integrartion using ArubaOS/Aruba Instant version 8.7.x.x.

-   `client-id` - has to be replaced with the ABB Ability™ account organization ID
-   `username` - has to be replaced with the **email address** of the ABB Ability™ account
-   `password` - has to be replaced with the **login password** of the ABB Ability™ account
-   `ap-group` - has to be replaced with the AP group name the configuration should be enabled on (multiple statements are required for multiple groups) (ArubaOS only)

>***Note:***  
>The [ABB Ability™ Smart Sensor](https://new.abb.com/motors-generators/service/advanced-services/smart-sensor) integrartion is levaraging the [BLE data forwarding service](../iot-concepts/server-connectivity/aruba_iot_transport_services.md#ble-data-forwarding) which is enabled by default for the device class *ability-smart-sensor* in ArubaOS/Aruba Instant 8.7.x.x. There is manual configuration supported for BLE data forwarding in this version.

>***Note:***  
>The [Baltimore CyberTrust Root certificate (BaltimoreCyberTrustRoot.crt.pem)](https://www.digicert.com/kb/digicert-root-certificates.htm) has to be installed on the Aruba infrastructure when connecting the [ABB Ability™ Smart Sensor platform](https://new.abb.com/motors-generators/service/advanced-services/smart-sensor). Please see the [Aruba CLI Reference - Importing Certificates](../references/aruba_reference_documentation.md#aruba-cli-reference---importing-certificates) for details.

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