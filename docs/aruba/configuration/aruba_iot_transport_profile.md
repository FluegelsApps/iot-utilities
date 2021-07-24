---
layout: default
title: IoT Transport Profile
has_children: false
parent: Aruba IoT Configuration
nav_order: 1
---

# IoT transport profile

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

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