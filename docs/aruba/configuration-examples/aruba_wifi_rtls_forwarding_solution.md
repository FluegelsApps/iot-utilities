---
layout: default
title: Wi-Fi RTLS Data Forwarding Solution
has_children: false
parent: Wi-Fi Solutions
grand_parent: Configuration Examples
nav_order: 1
---

# Wi-Fi RTLS data forwarding solution

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

This example shows the required configuration to enable [Wi-Fi RTLS data forwarding](#wi-fi-rtls-data-forwarding).

-   `fqdn, ip-address` - has to be replaced with the FQDN or IP address of the remote server
-   `access-token` - has to be replaced with the static access token used to connect to the remote server
-   `client-id` - has to be replaced with the client identifier string that is used by the remote server to identify the connecting Aruba infrastructure
-   `mac-address` - has to be replaced with the destination MAC address used by Wi-fi tags
-   `ap-group` - has to be replaced with the AP group name the configuration should be enabled on (multiple statements are required for multiple groups) (ArubaOS only)

**ArubaOS**

```
iot transportProfile "Wi-Fi-RTLS"
    serverType Telemetry-Websocket
    serverURL "[ws|wss]://<fqdn|ip-address>[:<port>][<path>]"
    accessToken <access-token>
    clientId <client-id>
    deviceClassFilter wifi-tags
    include-ap-group <ap-group>
    rtlsDestMAC <mac-address>
!
iot useTransportProfile "Wi-Fi-RTLS"
```

**Aruba Instant**

```
iot transportProfile "Wi-Fi-RTLS"
 endpointURL "[ws|wss]://<fqdn|ip-address>[:<port>][<path>]"
 endpointType telemetry-websocket
 payloadContent wifi-tags
 endpointToken <access-token>
 endpointID <client-id>
 rtlsDestMAC <mac-address>
 exit

iot useTransportProfile "Wi-Fi-RTLS"
```