---
layout: default
title: Configuration Docs
has_children: false
parent: Aruba Configuration
grand_parent: Aruba Guide
---

## [IoT radio profile](#table-of-contents)

`iot radio-profile`'s are used to configure the [Aruba IoT radio](#aruba-iot-radio) mode, BLE and/or ZigBee, and the respective mode settings. An `iot radio-profile` can either be applied to an internal or external radio instance.  

The `iot radio-profile` also controls the AP' BLE console settings.

The following table lists the available `iot radio-profile` parameters and their description:

|ArubaOS|Aruba Instant|Description|
|-|-|-|
|`iot radio-profile <iot-profile-name>`|`iot radio-profile <iot-profile-name>`|**Name** of the radio profile|
|`radio-instance <internal, external>`|`radio-instance <internal, external>`|**Type** of the radio the profile applies to.<br>Available options are:<br> - ***internal*** - applies to the internal radio of the AP (default) <br>- ***external*** - applies to the external radio that is connected over the USB port of the AP|
|`radio-firmware <firmware>`|`radio-firmware <firmware>`|Firmware that is applied to the radio.<br>Available options:<br>- ***default*** - default firmware gets applied|
|`radio-mode <mode>`|`radio-mode <mode>`|Radio mode to be enabled.<br> Available options are:<br>- ***None*** - Radio disabled (default)<br>- ***ble*** - BLE (tx/rx) enabled<br>- ***zigbee*** - ZigBee enabled<br>- ***"ble zigbee"*** - BLE (tx-only) and ZigBee enabled concurrently|
|`ble-opmode <opmode>`|`ble-opmode <opmode>`|BLE operation mode to be enabled.<br> This parameter is available only when `radio-mode` is set to ***ble*** or ***"ble zigbee"***.<br> Available options are:<br>- ***beaconing*** - BLE (tx) beaconing enabled using the iBeacon protocol (default)<br>- ***scanning*** - BLE (rx) scanning enabled<br>- ***"beaconing scanning"*** - BLE (tx/rx) beaconing and scanning enabled concurrently (default - does not show up in the configuration!)|
|`ble-console <console-mode>` |`ble-console <console-mode>`|BLE console mode to be enabled.<br>BLE console provides console access to the AP over BLE.<br>This parameter is available only when `radio-mode` is set to ***ble*** or ***"ble zigbee"***.<br>Available options are:<br>- ***dynamic*** - Enables BLE console automatically<br>- ***on*** - BLE console enabled<br>- ***off*** - BLE console disabled (default)|
|`ble-txpower <txpower>`|`ble-txpower <txpower>`| BLE tx power in dBm to be used.<br> This parameter is available only when `radio-mode` is set to ***ble*** or ***"ble zigbee"***.<br>- Value range: ***-20 ... 4***, (default: ***0***)|
|`zigbee-opmode <opmode>`|`zigbee-opmode <opmode>`|ZigBee operation mode to be used.<br> This parameter is available only when `radio-mode` is set to ***zigbee*** or ***"ble zigbee"***.<br> Available options are:<br>- ***coordinator*** - Radio works as ZigBee coordinator (default)|
|`zigbee-channel <channel>`|`zigbee-channel <channel>`|Channel to be used.<br> This parameter is available only when `radio-mode` is set to ***zigbee*** or ***"ble zigbee"***.<br> Available options are:<br>- **auto** - Selects the channel automatically (default)<br>- ***Value range: 11 ... 26*** - Specifies the channel manually|

>***Additional CLI parameters:***  
>
>- `clone` - Copy data from another `iot radio profile` (ArubaOS only)
>- `no` - Delete a command from the profile

>***Note:***  
>The default `ble-opmode beaconing scanning` does not show up in the configuration. Using the ***"beaconing scanning"*** parameter is only required to change the configuration form `ble-opmode beaconing` or `ble-opmode scanning` back to the default.  
>
>If the `radio-mode` is set to ***"ble zigbee"*** only BLE (tx) beaconing is supported, regardless of the `ble-opmode` setting.

An `iot radio-profile` is enabled using the following command:

|ArubaOS|Aruba Instant|
|-|-|
|`iot useTransportProfile <iot-profile-name>`|`iot use-radio-profile <iot-profile-name>`|

In addition to enabling the `iot radio-profile` it has to be assigned to an AP group in ArubaOS/controller based deployments using the following configuration:

    ap-group <ap-group-name>
        iot radio-profile <iot-profile-name>

For details about the `ap-group` configuration refer to the [ArubaOS CLI Reference - ap-group](#aruba-cli-reference---ap-group).

>***Note:***  
>Multiple `iot radio-profile`'s can be configured but a **maximum of two**, one internal and one external can be **enabled** per access point (Aruba Instant) or access point group (ArubaOS).

## [IoT transport profile](#table-of-contents)

The `iot transportProfile` defines the [IoT server connectivity](#iot-server-connectivity-server-side) settings using the [Aruba IoT server interface](#aruba-iot-server-interface-guide).

The following table lists the available `iot transportProfile` parameters and their description:

|ArubaOS|Aruba Instant|Description|
|-|-|-|
|`iot transportProfile <transport-profile-name>`|`iot transportProfile <transport-profile-name>`|**Name** of the transport profile|
|**Server connection settings**||
|`serverType <type>`|`endpointType <type>`|The type of IoT server the transport profile connects to.<br> Available options are listed in the table [Aruba IoT server interface - connection types](#aruba-iot-server-interface---connection-types).<br>The default type is ***Meridian-Beacon-Management***.
|`serverURL <URL>`|`endpointURL <URL>`|IoT server connection ***URL*** used to connect to the remote server.<br> This parameter is not available when Server type is set to ***Azure-IoTHub***.<br> Valid input values have to start with:<br>- ***http(s)://*** - for server connection type [Telemetry-https](#telemetry-https) using HTTP (un-encrypted) or HTTPS(encrypted) connections<br>- ***ws(s)://*** for server connection type [Telemetry-Websocket](#telemetry-websocket) using web socket (ws) or secure web socket (wss) connections|
|`proxy server <ip/fqdn>`<br>`[proxy user <username> password <password>]`|`proxyserver <ip/fqdn> <port> [<username> <password>]`|Configures an optional proxy server to be used to establish the IoT server connection through. Optional proxy server authentication with username/password is supported.<br> Available options are:<br>- ***ip/fqdn*** - Proxy server ip address or full qualified domain name<br> - ***port*** - Proxy server port<br>- ***username*** - Proxy authentication username<br>- ***password*** - Proxy authentication password|
|n/a|`vlan <vlanid>`|Configures the uplink VLAN being used for IoT server connectivity. Only supported on Aruba Instant.<br>Available options:<br>- ***vlan id*** - VLAN id of uplink VLAN|
|**Reporting frequency settings**|||
|`reportingInterval <seconds>`|`transportInterval <seconds>`|Configures the ***reporting interval (in seconds)*** for [IoT transport services](#iot-transport-services) and vendor specific connections that support periodic reporting.<br> The valid/supported value range depends on the configured `serverType/endpointType` and is listed in [Aruba IoT server interface - connection types](#aruba-iot-server-interface---connection-types).|
|**Authentication/Authorization settings**|||
|`authentication-mode <mode>`|`authentication-mode <mode>`|Configures the OAuth2 authentication mode to be used for the server connection.<br>Available options are:<br>- ***none*** - Authentication is disabled and a static access token is used for authorization (default)<br>- ***password*** - Authentication using username/password<br> - ***client-credentials*** - Authentication using client_id/client secret|
|`authenticationURL <URL>`|`authenticationURL <URL>`|Configures the authentication server URL.<br>This parameter only applies if `authentication-mode` is set to ***password*** or ***client-credentials***.<br>Only encrypted connections are allowed starting with **https://**.|
|`accessToken <token>`|`endpointToken <token>`|Configures the static access token used for authorization.<br>This parameter is only applicable when `authentication-mode` is set to ***none***.<br>Input values:<br> - ***token*** - String, base64 characters only.|
|`clientID <client_id>`|`endpointID <client_id>`|Client identifier string that is used by the IoT server to identify the connecting Aruba infrastructure.<br>This parameter only applies if `serverType/endpointType` is set to ***Meridian-Asset-Tracking***, ***[Telemetry-Https](#telemetry-https)*** or ***[Telemetry-Websocket](#telemetry-websocket)***.<br>This parameter is required when `authentication-mode` is set to ***client-credentials*** for OAuth2 client_id/secret authentication.<br>Input values:<br> - ***client_id*** - string, 1-100 characters|
|`client-secret <password>`|`client-secret <client-secret>`|Configures the ***password*** for Oauth2 client_id/secret authentication.<br>This parameter is required when `authentication-mode` is set to ***client-credentials***.|
|`username <username>`|`username <username>`|Configures the ***username*** for username/password authentication.<br>This parameter only applies if `authentication-mode` is set to ***password***.|
|`password <password>`|`password <password>`|Configures the ***password*** for username/password authentication.<br>This parameter only applies if `authentication-mode` is set to ***password***.|
|`accessID <assa-abloy-access-id>`|`accessID <assa-abloy-access-id>`|Configures the Assa-Abloy ***accessID*** for the vendor specific connection type ***Assa-Abloy***.<br>This parameter only applies if `serverType/endpointType` is set to ***Assa-Abloy***.<br>In addition the configuration of the parameters `username` and `password` is required.|
|`azure-dps-auth-type group-enrollment symmetric-key <key>`|`azure-dps-auth-type group-enrollment symmetric-key <key>`| Configures the authentication type and credentials for the Azure Device Provisioning Service (DPS). Currently the only supported authentication type is ***group-enrollment*** using a ***symmetric-key***.<br>Available options are:<br>- ***key*** - Azure symmetric group key.<br>Requires the configuration of parameter `azure-dps-id-scope`.<br>This parameter only applies if `serverType/endpointType` is set to ***[Azure-IoTHub](#azure-iothub)***.|
|`azure-dps-id-scope <scope-id>`|`azure-dps-id-scope <scope-id>`|Configures the Azure Device Provisioning Service (DPS) enrollment group  ***scope-id***.<br>Available options are:<br>- ***scope-id*** - Azure DPS enrollment group scope-id.<br>Requires the configuration of parameter `azure-dps-auth-type`.<br>This parameter only applies if `serverType/endpointType` is set to ***[Azure-IoTHub](#azure-iothub)***.|
|**Device filter settings**||
|`deviceClassFilter <device-class>`|`payloadContent <device-class>`|Configures a list of [supported device classes](#supported-iot-vendordevice-class-list) to be included in telemetry reports or data forwarding to the remote IoT server. For details see [Device Class Filter](#device-class-filter).<br>A maximum of 16 devices classes can be enabled per iot transport profile.|
|**Wi-Fi specific settings**|||
|`rtlsDestMAC <MAC-address>`|`rtlsDestMAC <MAC-address>`|Sets the destination MAC address filter for RTLS tags device class.<br>This parameter only applies if `serverType/endpointType` is set to ***[Telemetry-Websocket](#telemetry-websocket)*** and the `deviceClassFilter` ***[wifi-tag](#wi-fi-device-class-filter)*** is selected to enable the [Wi-Fi RTLS data forwarding](#wi-fi-rtls-data-forwarding) transport service.|
|**ZigBee specific settings**|||
|`ZSDFilter <zigbee-socket-device-profile>`<br>`...`<br>`ZSDFilter <zigbee-socket-device-profile>`|`ZSDFilter <zigbee-socket-device-profile>,...,<zigbee-socket-device-profile>`|Assigns a list of [zigbee-device-socket-profiles](#zigbee-socket-device-profile) to filter the allowed zigbee socket devices (ZigBee applications) forwarded by the transport profile.<br>This parameter only applies if `serverType/endpointType` is set to ***[Telemetry-Websocket](#telemetry-websocket)*** and the `deviceClassFilter` ***[zsd](#zigbee-socket-device-class-filter)*** is selected to enable the [ZigBee socket device](#zigbee-socket-device) transport service.|
|[**General data content filter settings**](#general-data-filter)
|`data-filter <data-id-list>`|`data-filter <data-id-list>`|Configures a list of data points to filter from periodic telemetry reports before sending to the remote IoT server. The data fields refer to the field numbers in the [Aruba IoT Protobuf Specification](#aruba-iot-protobuf-specification).<br>This parameter only applies to [IoT transport services](#iot-transport-services) that support periodic reporting.|
|`deviceCountOnly`|`deviceCountOnly`|Enables to send only the aggregated device type counts per configured [device class](#device-class-filter).<br>This parameter only applies to [IoT transport services](#iot-transport-services) that support periodic reporting.||
|[**BLE data content filter settings**](#ble-data-filter)||<br>These parameters only apply to BLE related [device classes](#ble-device-class-filter) and [transport services](#iot-transport-services) and if `serverType/endpointType` is set to ***[Telemetry-Https](#telemetry-https)***, ***[Telemetry-Websocket](#telemetry-websocket)*** or ***[Azure-IoTHub](#azure-iothub)***|
|`rssiReporting <format>`|`rssiReporting <format>`|Set the preferred RSSI format BLE telemetry reporting.<br>Available options are:<br> - ***average*** - RSSI averaged over the reporting period (default)<br> - ***bulk*** - Last 20 RSSI values seen by the device since the previous reporting interval <br> - ***last*** - Last RSSI value seen by the device<br> - ***max*** - Maximum RSSI measured over the reporting period<br> - ***smooth*** - Smoothed RSSI measured over the reporting period|
|`environmentType <type>`|`environmentType <type>`|Set the working environment type for RSSI based BLE distance calculation..<br>Available options are:<br> - ***auditorium*** - Auditorium environment<br> - ***custom*** - Custom environment, set custom fading factor using `customFadingFactor`<br> - ***office*** - Office environment (default)<br> - ***outdoor*** - Outdoor environment<br> - ***shipboard*** - Shipboard environment<br> - ***warehouse*** - Warehouse environment|
|`customFadingFactor <factor>`|`customFadingFactor <factor>`|This parameter sets a custom fading factor the BLE distance calculation.<br>This parameter only applies if `environmentType` is set to ***custom***.<br>Input values:<br>**Range**: *10-40*|
|`cellSizeFilter <cellsize>`|`cellSizeFilter <cellsize>`|Sets a proximity filter specified in meters. Devices outside the cell will not be reported.<br>Setting to *0* disables the cell size filter.<br>**Range**:<br> - Aruba Instant: *0 to 255 m*<br> - ArubaOS: *2 to 100 m*<br>**Default**: *0*|
|`movementFilter <threshold>`|`movementFilter <threshold>`|Filters devices that do not change distance. Specified in meters.<br>Applicable only if a `cellSizeFilter` is set.<br>Setting to *0* disables the movement filter.<br>**Range**:<br> - Aruba Instant: *0 to 255 m*<br> - ArubaOS: *2 to 30 m* m<br>**Default**: *0*|
|`ageFilter <timeout>`|`ageFilter <timeout>`|Sets a timeout for inactive devices. Devices without activity in the specified time frame will not be reported.<br>Setting to *0* disables the ageFilter filter.<br>**Range**: *30 to 3600 seconds*<br>**Default**: *0*|
|`vendorFilter <vendor-list>`|`vendorFilter <vendor-list>`|Specifies a list of [Bluetooth SIG vendor IDs or vendor names](https://www.bluetooth.com/specifications/assigned-numbers/company-identifiers/). Only devices that match the configured Vendor ID or Vendor Name will be reported.<br>Input value:<br> - **vendor-list** - max 5 vendor IDs or vendor names, example: *"0x011B,0x004C,Google"*|
|`uuidFilter <uuid-list>`|`uuidFilter <uuid-list>`|Specifies a list of ***iBeacon UUIDs*** to filter devices included in the reports.<br>This parameter only applies if the `deviceClassFilter` is set to ***[ibeacon](#ble-device-class-filter)***.<br>Input value:<br> - **uuid-list** - max 10 UUIDs, example: *"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx,yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyyyyyyy"*|
|`uidNamespaceFilter <uid-list>`|`uidNamespaceFilter <uid-list>`|Specifies a list of ***Eddystone-UID namespaces*** to filter devices included in the reports.<br>This parameter only applies if the `deviceClassFilter` is set to ***[eddystone](#ble-device-class-filter)***.<br>Input value:<br> - **uid-list** - max 10 UUIDs, example: *"707cc5b4983477cb3e77,707cc5b49883477cb3e7"*|
|`urlFilter <url-list>`|`urlFilter <url-list>`|Specifies a list of ***Eddystone-URL*** strings to filter devices included in the reports.<br>This parameter only applies if the `deviceClassFilter` is set to ***[eddystone](#ble-device-class-filter)***.<br>Input value:<br> - **url-list** - max 10 URLs, partial URL strings are allowed, example: *"https://www.arubanetworks.com/iot,https://www.hpe.com"*|
|`bleDataForwarding`|`bleDataForwarding`|Enable [BLE data forwarding](#ble-data-forwarding) for all known [BLE device classes](#ble-device-class-filter).<br>**Default**: *disabled*|
|`perFrameFiltering`|`perFrameFiltering`|Enables [per frame BLE data filtering](#ble-data-filter). If this option is enabled the transport profile filters are applied to each BLE frame rather than on the BLE device as a whole.<br>This parameter only applies if `bleDataForwarding` is enabled.<br>**Default**: *disabled*|
|**AP-group assignment**|||
|`include-ap-group <ap-group>`|n/a|Applies one ore multiple AP groups to the transport profile.<br>Only supported on ArubaOS.<br>Required input values:<br>- ***ap-group*** - AP group name|

>***Additional CLI parameters:***  
>- `clone` - Copy data from another `iot transport profile` (ArubaOS only)
>- `no` - Delete a command from the profile

An `iot transportProfile` is enabled using the following command:

|ArubaOS|Aruba Instant|
|-|-|
|`iot useTransportProfile <transport-profile-name>`|`iot useTransportProfile <transport-profile-name>`|

>***Note:***  
>Multiple transport profiles can be configured, but a maximum of 4 transport profiles can be enabled per access point (Aruba Instant) or access point group (ArubaOS).

## [AP USB device management](#table-of-contents)
  
AP USB device management controls connected USB devices using USB profiles and USB ACL profiles. An USB ACL profile is assigned to an AP or AP group using an USB profile.

### USB ACL profile

An USB ACL profile consists of one or more permit/deny rules for supported USB vendor-product names. An USB ACL profile includes an implicit *deny-all* at then end. An USB profile with an undefined USB ACL profile applies a *permit-all* by default.

>***Note:***  
>Up to 16 USB ACL profiles are supported.

|ArubaOS|Aruba Instant|Description|
|-|-|-|
|`ap usb-acl-prof <usb-acl-profile-name>`|`usb acl-profile <usb-acl-profile-name>`|**Name** of the USB ACL profile|
|`rule vendor <vendor-name> action <permit/deny>`|`rule <vendor-name> <permit/dena>`|Configure an ACL rule for a supported USB ***vendor-name***.<br>Available options are:<br> - ***vendor-name*** - USB vendor name, ***All*** allows all supported vendors<br><br>Available action value to perform if the vendor-name matches.<br>Available options are:<br> - ***deny*** - Access to USB device is denied<br> - ***permit*** - Access to USB device is refused|

>***Note:***  
>The `show usb supported vendor-product` command lists the supported USB vendor-names on Aruba Instant APs.

### USB profile

An USB profile binds a specific USB ACL profile ton an AP or AP group.

|ArubaOS|Aruba Instant|Description|
|-|-|-|
|`ap usb-profile <usb-profile-name>`|`usb profile <usb-profile-name>`|**Name** of the USB profile|
|`usb-acl-profile <usb-acl-profile-name>`|`usb-acl <usb-acl-profile-name>`|Assigns an previously defined USB profile to the USB profile.<br>Available options are:<br> - ***usb-acl-profile-name*** - Name of the USB ACL profile|

An USB profile is bound to an AP or AP group using the following commands:

**ArubaOS**

```
ap-group <ap-group-name>
    usb-profile <usb-profile-name>
```

For details about the `ap-group` configuration refer to the [ArubaOS CLI Reference - ap-group](#aruba-cli-reference---ap-group).

**Aruba Instant**

```
usb-profile-binding <usb-profile-name>
```

For details about the `usb-profile-binding` configuration refer to the [Aruba CLI Reference - USB profile binding](#aruba-cli-reference---usb-profile-binding).

Examples:

**ArubaOS**

```
ap usb-acl-prof "UsbAclProf1"
    rule vendor All action permit
!
ap usb-profile "UsbProf1"
    usb-acl-profile "UsbAclPro1"
!
ap-group "ApGroup1"
    usb-profile "UsbProf1"
!
```

**Aruba Instant**

```
usb acl-profile "UsbAclProf1"
 rule  All  permit
exit
usb profile "UsbProf1"
 usb-acl "UsbAclProf1"
exit
usb-profile-binding "UsbProf1"
```

## [Wired-Port profile](#table-of-contents)

A wired port profile configures the USB port on the AP as a wired ethernet port. It allows to configure all aspects of the ethernet connectivity of the USB device including the following:

-   Wired port settings (speed, duplex, ...)
-   VLAN assignment
-   Network authentication settings (MAC-Auth, 802.1x, ...)
-   ACL or Aruba user role assignment
-   Forwarding mode (tunneled, bridged) - ArubaOS-only

An wired port profile is bound to an AP or AP group using the following commands:

**ArubaOS**

```
ap-group <ap-group-name>
    enet-usb-port-profile <wired-port-profile-name> (default: shutdown)
```

For details about the `ap-group` configuration refer to the [ArubaOS CLI Reference - ap-group](#aruba-cli-reference---ap-group).

**Aruba Instant**

```
enet-usb-port-profile <wired-port-profile-name>
```

For details about the wired profile configuration refer to the [ArubaOS CLI Reference - Wired profile](#aruba-cli-reference---wired-profile).

Examples:

**ArubaOS**

```
ip access-list session allowall
    any any any permit
    ipv6 any any any permit
!
ip access-list session apprf-iot-device-sacl
!
user-role iot-device
    access-list session global-sacl
    access-list session apprf-iot-device-sacl
    access-list session allowall
!
aaa profile "iot-wired_aaa_prof"
    initial-role "iot-device"
!
ap wired-ap-profile "USB-to-ethernet-wiredApProf1"
    wired-ap-enable
    switchport access vlan 192
!
ap wired-port-profile "USB-to-ethernet-wiredPortProf1"
    wired-ap-profile "USB-to-ethernet-wiredApProf1"
    aaa-profile "iot-wired_aaa_prof"
!
ap-group "ApGroup1"
    enet-usb-port-profile "USB-to-ethernet-wiredPortProf1"
!
```

**Aruba Instant**

```
wlan access-rule "USB-to-ethernet-wiredPortProf1"
 index 1
 rule any any match any any any permit
exit
wired-port-profile "USB-to-ethernet-wiredPortProf1"
 switchport-mode access
 allowed-vlan 192
 no shutdown
 access-rule-name "USB-to-ethernet-wiredPortProf1"
 type employee
exit
enet-usb-port-profile "USB-to-ethernet-wiredPortProf1"
```

## [SES Imagotag ESL configuration](#table-of-contents)

SES-Imagotag’s Electronic Shelf Label system uses a [vendor-specific](#vendor-specific-implementations) USB integration with the Aruba infrastructure using a dedicated set of configuration commands.
In ArubaOS the SES-Imagotag configuration is enabled in the [`ap system-profile`](#aruba-cli-reference---ap-system-profile) where Aruba Instant uses an `sesimagotag-esl-profile`.

|ArubaOS|Aruba Instant|Description|
|-|-|-|
|`ap system-profile <ap-system-profile-name>`|n/a|**Name** of the ap system-profile.<br>Only supported on ArubaOS.<br>Required input values:<br>- ***ap-system-profile-name*** - AP system profile name|
|n/a|`sesimagotag-esl-profile`|Adds a SES-Imagotag ESL configuration profile.<br>Only supported on Aruba Instant.|
|`sesImagotag-esl-channel <esl-channel>`|`sesImagotag-esl-channel <sl-channel>`|The the radio channel of SES-Imagotag ESL radio.<br>Available options are:<br> - ***esl-channel*** - Range [0-10], 127 is ESL-server managed channel.<br>***Note:***<br>**ArubaOS:** If no ESL channel is configured the AP will select a channel automatically at boot time (but not automatic change later).<br>**Aruba Instant:** A static channel or 127 has to be set manually. There is no auto channel selection on Aruba Instant.|
|`sesImagotag-esl-radio-coexistence`|`sesImagotag-esl-radio-coexistence`|Enables the coexistence function between the SES-Imagotag ESL radio and the AP 2.4G Wi-Fi radio. When ESL radio tries to transmit packets the Wi-Fi 2.4 GHz radio is suspected for milliseconds to reduce interference.<br>(Default: **Enabled**)|
|`sesImagotag-esl-server <FQDN>`|`sesImagotag-esl-server <FQDN>`|Adds the FQDN of SES-Imagotag ESL server. FQDN setting has a higher priority than `sesImagotag-esl-serverip` if both are confiugured.<br>Available options are:<br> - ***FQDN*** - FQDN of the SES-Imagotag ESL server.|
|`sesImagotag-esl-serverip <ip-address>`|`sesImagotag-esl-serverip <ip-address>`|Configures the ip address of the SES-Imagotag ESL server.<br>Available options are:<br> - ***ip-address*** - SES-Imagotag ESL server ip address|
|`sesImagotag-esl-tls-auth`|`sesImagotag-esl-tls-auth`|Enables TLS authentication of the AP with the SES-Imagotag ESL server. The AP uses the factory default TPM certificate to autheitcated itself to the SES server and use the pre-loaded SES server’s trusted root certificate to validate the SES server certificate<br>(Default: **Disabled**).|
|`sesImagotag-esl-tls-fqdn-verify`|`sesImagotag-esl-tls-fqdn-verify`|Enables TLS certificate verification for the SES-Imagotag ESL server connection checking the configured FQDN against the TLS certificate presented by the SES-Imagotag server during connection establishment. Only applies if `sesImagotag-esl-server <FQDN>` is configured to use the SES cloud server.<br>(Default: **Disabled**)|  

Please find an example configuration [here](#ses-imagotag)

## [ZigBee configuration](#table-of-contents)

This secion describes the required configuration for ZigBee based solutions via the [Aruba IoT radio Gen2](#aruba-iot-radio) using the [ZigBee socket device transport service](#zigbee-socket-device).

Configuring a ZigBee solution requires the following setps:  

1)  Configuring an [`iot radio-profile`](#iot-radio-profile)  
2)  Configuring a [`zigbee service-profile`](#zigbee-service-profile)
3)  Configuring a [`zigbee socket-device-profile`](#zigbee-socket-device-profile)
4)  Configuring an [`iot transportProfile`](#iot-transport-profile)

>***Note:***  
>**Assa-Abloy** is currently the only supported vendor specific ZigBee solution using a vendor specific [server connection type](#aruba-iot-server-interface---connection-types) and not using the generic [Zigbee socket device framework](#zigbee-socket-device). Therefore step 3) `zigbee socket-device-profile` confugration is NOT required for this solution. Please see the [Assa-Abloy configuration](#assa-abloy) exmaple for details.

### ZigBee service profile

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

#### **Permit ZigBee device joining**

If `permit-joining` is disabled in the `zigbee service-profile`, which is the default setting, new clients can only join an APs ZigBee radio when it is temporarily permitted.
Temporarily permitting joining is enabled using the `zigbee-init-action` command `permit-joining`.

|ArubaOS|Aruba Instant|Description|
|-|-|-|
|`ap zigbee-init-action permit-joining {ap-name, ip-addr, ipv6-addr} <ap-name, ip-addr, ipv6-addr> radio <radio-addr> restart [<duration>]`|`zigbee-init-action permit-joining radio <radio-addr> restart [<duration>]`|Opens the APs ZigBee radio for new zigBee device to join.<br>Available options:<br> - ***radio-addr*** - ZigBee radio MAC address or ***all***<br> - ***duration*** - 60 - 600 seconds, time window to allow joining, default: 600 s <br>Available options (ArubaOS-only):<br> - ***ap-name, ip-addr, ip6-addr*** - AP name or IP to execture the command on|
|`ap zigbee-init-action permit-joining {ap-name, ip-addr, ipv6-addr} <ap-name, ip-addr, ipv6-addr> radio <radio-addr> stop`|`zigbee-init-action permit-joining radio <radio-addr> stop`|Closes the APs ZigBee radio for new ZigBee devices imidiately.<br>Available options:<br> - ***radio-addr*** - ZigBee radio MAC address or ***all***<br> - ***duration*** - 60 - 600 seconds, time window to allow joining, default: 600 s <br>Available options (ArubaOS-only):<br> - ***ap-name, ip-addr, ip6-addr*** - AP name or IP to execture the command on|

### ZigBee socket-device-profile

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