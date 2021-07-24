---
layout: default
title: ArubaOS/Aruba Instant 8.8.x.x or higher
has_children: false
nav_order: 1
parent: IoT-Utilities App
grand_parent: Configuration Examples
---

# IoT-Utilities App (ArubaOS/Aruba Instant 8.8.x.x or higher)

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

This example shows the configuration to setup an Aruba IoT demo using the [IoT-Utilities app](https://iot-utilities.arubademo.de/) using ArubaOS/Aruba Instant version 8.8.x.x or higher.

-   `ip-address` - has to be replaced with the **IP address** of the mobile device the IoT-Utilities app is running on. The current IP address used by the app is shown in the [IoT-Utilties Dashboard - Server control panel status](../main/dashboard.md#1-server-control-panel).
-   `port` - has to be replaced with the apps [**port number**](../settings/settings_iotserver.md#port-number) configured in the apps [IoT-server settings](../settings/settings_iotserver.md). The default value is ***5443***.
-   `client-id` - should be replaced with a custom client identifier to uniquily identify the connecting Aruba infrasturcture within the IoT-Utilities app.
-   `secret` - has to be replaced with the apps [**Static access token**](../settings/settings_iotserver.md#static-access-token) configured in the apps [IoT-server settings](../settings/settings_iotserver.md)
-   `ap-group` - has to be replaced with the AP group name the configuration should be enabled on (multiple statements are required for multiple groups) (ArubaOS only)

>***Note:***  
>The self-signed server certificate or the trusted root CA certificate used by the [IoT-Utilities app](https://iot-utilities.arubademo.de/) has to be installed on the Aruba infrastructure for the sercure web socket server connection to be established. The self-signed certificate can be downloaded either via the [IoT-Utilties Dashboard - Certificate Control Panel](../main/dashboard.md#2-certificate-control-panel) or using the apps web dashboard.  
>Please see the [Aruba CLI Reference - Importing Certificates](#aruba-cli-reference---importing-certificates) for details about how to install the downloaded certificate on the Aruba infrastructure.

**ArubaOS**

```
iot radio-profile "int-scan"
    radio-mode none ble
    ble-opmode scanning
!
ap-group <ap-group>
    iot radio-profile "int-scan"
!
iot transportProfile "IoT-Utilities-App"
    serverType Telemetry-Websocket
    serverURL "wss://<ip-address>:<port>/telemetry"
    authentication-mode client-credentials
    authenticationURL "https://<ip-address>:<port>/auth"
    clientId <client-id>
    client-secret <secret>
    deviceClassFilter all
    deviceClassFilter wifi-tags
    deviceClassFilter wifi-assoc-sta
    deviceClassFilter wifi-unassoc-sta
    deviceClassFilter serial-data
    deviceClassFilter unclassified
    reportingInterval 30
    rssiReporting last
    bleDataForwarding
    include-ap-group <ap-group>
!
iot useTransportProfile "IoT-Utilities-App"
```

**Aruba Instant**

```
iot radio-profile "int-scan"
 radio-mode ble
 ble-opmode scanning
 exit

iot use-radio-profile "int-scan"

iot transportProfile "IoT-Utilities-App"
 endpointURL "wss://<ip-address>:<port>/telemetry"
 endpointType telemetry-websocket
 authentication-mode client-credentials
 authenticationURL "https://<ip-address>:<port>/auth"
 endpointID <client-id>
 client-secret <secret>
 payloadContent all
 payloadContent unclassified
 payloadContent serial-data
 payloadContent wifi-tags
 payloadContent wifi-assoc-sta
 payloadContent wifi-unassoc-sta
 transportInterval 30
 ageFilter 30
 bleDataForwarding
 rssiReporting last
 exit

iot useTransportProfile "IoT-Utilities-App"
```