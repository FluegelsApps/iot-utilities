---
layout: default
title: ZigBee Configuration
has_children: false
parent: Aruba IoT Configuration
nav_order: 5
---

# ZigBee configuration

This secion describes the required configuration for ZigBee based solutions via the [Aruba IoT radio Gen2](#aruba-iot-radio) using the [ZigBee socket device transport service](#zigbee-socket-device).

Configuring a ZigBee solution requires the following setps:  

1)  Configuring an [`iot radio-profile`](#iot-radio-profile)  
2)  Configuring a [`zigbee service-profile`](#zigbee-service-profile)
3)  Configuring a [`zigbee socket-device-profile`](#zigbee-socket-device-profile)
4)  Configuring an [`iot transportProfile`](#iot-transport-profile)

>***Note:***  
>**Assa-Abloy** is currently the only supported vendor specific ZigBee solution using a vendor specific [server connection type](#aruba-iot-server-interface---connection-types) and not using the generic [Zigbee socket device framework](#zigbee-socket-device). Therefore step 3) `zigbee socket-device-profile` confugration is NOT required for this solution. Please see the [Assa-Abloy configuration](#assa-abloy) exmaple for details.

## ZigBee service profile

The `zigbee service-profile` determines the Zigbee network settings if ZigBee has been enabled in the [`iot radio-profile`](#iot-radio-profile) configuration.  

|ArubaOS|Aruba Instant|Description|
|-|-|-|
|`zigbee service-profile <profile-name>`|`zigbee service-profile <profile-name>`|**Name** of the Zigbee service-profile.|
|`panid <panid>`|`panid <panid>`|Sets the ZigBee **pernsonal network identifier (PAN ID)**.<br>Available options are:<br> - ***auto*** - automatically selects a PAN ID (default)<br> - ***[0000-FFF0]*** - hexadecimal PAN ID|
|`permit-joining {off, on}`|`permit-joining {off, on}`|Enables or disables joining permission of new devices to the APs ZigBee network permanently.<br>Available options are:<br> - ***off*** - permanent joinging disabled (default)<br> - ***on*** - permanent joining enabled<br> ***Note:*** To allow devices to join in case joining is disabled see [Permit ZigBee device joining](#permit-zigbee-device-joining)|
|`radio-instance {all, external, internal}`|`radio-instance {all, external, internal}`|Determines the IoT ZigBee radio instance the ZigBee service profile should be used with.<br>Available options are:<br> - ***all*** - applies the service-profile to internal and external IoT radios (default)<br> - ***external*** - applies the servcie profile to external radio's only<br> - ***internal*** - applies the service-profile to internal radios only.|
|`security {disable, enable}`|`security {disable, enable}`|Enables or disables ZigBee security.<br>Available options are:<br> - ***enable*** - enables ZigBee security (default) <br> - ***disable*** - disables ZigBee security|

>***Additional CLI parameters:***  
>- `clone` - Copy data from another `zigbee service-profile` (ArubaOS only)
>- `no` - Delete a command from the profile

A `zigbee service-profile` is bound to an AP or AP group using the following commands:

**ArubaOS**

```
ap-group <ap-group-name>
    zigbee service-profile <profile-name>
```

For details about the `ap-group` configuration refer to the [ArubaOS CLI Reference - ap-group](#aruba-cli-reference---ap-group).

**Aruba Instant**

```
zigbee use-service-profile <profile-name>
```

### **Permit ZigBee device joining**

If `permit-joining` is disabled in the `zigbee service-profile`, which is the default setting, new clients can only join an APs ZigBee radio when it is temporarily permitted.
Temporarily permitting joining is enabled using the `zigbee-init-action` command `permit-joining`.

|ArubaOS|Aruba Instant|Description|
|-|-|-|
|`ap zigbee-init-action permit-joining {ap-name, ip-addr, ipv6-addr} <ap-name, ip-addr, ipv6-addr> radio <radio-addr> restart [<duration>]`|`zigbee-init-action permit-joining radio <radio-addr> restart [<duration>]`|Opens the APs ZigBee radio for new zigBee device to join.<br>Available options:<br> - ***radio-addr*** - ZigBee radio MAC address or ***all***<br> - ***duration*** - 60 - 600 seconds, time window to allow joining, default: 600 s <br>Available options (ArubaOS-only):<br> - ***ap-name, ip-addr, ip6-addr*** - AP name or IP to execture the command on|
|`ap zigbee-init-action permit-joining {ap-name, ip-addr, ipv6-addr} <ap-name, ip-addr, ipv6-addr> radio <radio-addr> stop`|`zigbee-init-action permit-joining radio <radio-addr> stop`|Closes the APs ZigBee radio for new ZigBee devices imidiately.<br>Available options:<br> - ***radio-addr*** - ZigBee radio MAC address or ***all***<br> - ***duration*** - 60 - 600 seconds, time window to allow joining, default: 600 s <br>Available options (ArubaOS-only):<br> - ***ap-name, ip-addr, ip6-addr*** - AP name or IP to execture the command on|

## ZigBee socket-device-profile

The `zigbee socket-device-profile` profile defines the **inbound and outbound sockets** of a ZigBee application using the [zigbee socket device (ZSD) service](#zigbee-socket-device).

|ArubaOS|Aruba Instant|Description|
|-|-|-|
|`zigbee socket-device-profile <socket-device-profile-name>`|`zigbee socket-device-profile <socket-device-profile-name>`|**Name** of the Zigbee socket-device-profile.|
|`zigbee socket-inbound-profile <inbound-socket-profile-name>`<br>or<br>`zigbee socket-outbound-profile <outbound-socket-profile-name>`|n/a|Adds an **inbound** or **outbound** socket profile entry to the `socket-device-profile` (ArubaOS only).<br> - ***Name*** - name of the inbound/outbound socket profile<br>**Note**:<br>In ArubaOS inbound/outbound socket profiles are explicitley defined while in Aruba Instant inbound/outbound socket entries are added directly (see next).|
|`source_endpoint <source_endpoint>`<br>`endpoint <endpoint>`<br>`profile <profile>`<br>`cluster <cluster>`<br>` [aps-ack]`|`<inbound, outbound> <source_endpoint> <endpoint> <profile> <cluster> [aps-ack]`|Adds the zigbee socket device profile parameters.<br>Available options:<br> - ***inbound/outbound*** - socket direction (Aruba Instant only)<br> - ***source_endpoint*** - ZigBee application soruce endpoint, range [1, 254]<br> - ***endpoint*** - ZigBee application destination endpoint, range [1, 254]<br> - ***profile*** - ZigBee application profile ID, range [0x0000, 0x7FFF], [0xC000, 0xFFFF]<br> - ***cluster*** - ZigBee application cluster ID, range [0x0000, 0x7FFF], [0xFC00, 0xFFFF]<br> - ***aps-ack*** - Enables acknowledgement of ZigBee APS packets, optional, only applicable if socket direction is set to `outbound`|

The `zigbee socket-device-profile` is assigned to the [`iot transportProfile`](#iot-transport-profile) using the `ZSDFilter` command.

>***Note:***  
>A maximum of 8 inbound and 4 outbound socket are supported per ZigBee socket device profile while a maximum of 4 ZigBee socket device profiles are supported per IoT transport profile.

Plesae see [Generic ZSD solution](#generic-zsd-solution) for a configuration example unsing the the [ZigBee socket device transport service](#zigbee-socket-device).