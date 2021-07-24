---
layout: default
title: Wi-Fi Client Tracking Solution
has_children: false
parent: Wi-Fi Solutions
grand_parent: Aruba IoT Config Examples
nav_order: 0
---

# Wi-Fi client tracking solution

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

This example shows the required configuration to enable [Wi-Fi telemetry](#wi-fi-telemetry).

-   `fqdn, ip-address` - has to be replaced with the FQDN or IP address of the remote server
-   `access-token` - has to be replaced with the static access token used to connect to the remote server
-   `client-id` - has to be replaced with the client identifier string that is used by the remote server to identify the connecting Aruba infrastructure
-   `ap-group` - has to be replaced with the AP group name the configuration should be enabled on (multiple statements are required for multiple groups) (ArubaOS only)

**ArubaOS**

```
iot transportProfile "Wi-Fi-telemetry"
    serverType Telemetry-Websocket
    serverURL "[ws|wss]://<fqdn|ip-address>[:<port>][<path>]"
    accessToken <access-token>
    clientId <client-id>
    deviceClassFilter wifi-assoc-sta
    deviceClassFilter wifi-unassoc-sta
    include-ap-group <ap-group>
!
iot useTransportProfile "Wi-Fi-telemetry"
```

**Aruba Instant**

```
iot transportProfile "Wi-Fi-telemetry"
 endpointURL "[ws|wss]://<fqdn|ip-address>[:<port>][<path>]"
 endpointType telemetry-websocket
 payloadContent wifi-assoc-sta
 payloadContent wifi-unassoc-sta
 endpointToken <access-token>
 endpointID <client-id>
 exit

iot useTransportProfile "Wi-Fi-telemetry"
```