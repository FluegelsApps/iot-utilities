

## [BLE data forwarding solutions](#table-of-contents)

### [Azure IoT Hub (ble data)](#table-of-contents)

This example shows the required configuration to enable [BLE data forwarding](#ble-data-forwarding) for `all` supported [BLE vendors](#supported-iot-vendordevice-class-list) to Azure IoT Hub.

-   `scope-id` - has to be replaced with Azure DPS enrollment group scope-id
-   `key` - has to be replaces with Azure symmetric group key
-   `ap-group` - has to be replaced with the AP group name the configuration should be enabled on (multiple statements are required for multiple groups) (ArubaOS only)

>***Note:***  
>`bleDataForwarding` is enabled by default for server type `Azure-IoTHub` and cannot be disabled.

>***Caution:***  
>Enabling the **device class filter** `all` will enable BLE data forwarding of all knon/supported [BLE vendor device classes](#supported-iot-vendordevice-class-list). This could haveally increase the amount of data beeing forwarded to the remote server because all BLE advertisements and scan respsonse packets are forwarded in near real time.  
It is recommended to use the [BLE device class filter](#ble-device-class-filter) and [BLE data filters ](#ble-data-filter) to filter the data being forwarded.

**ArubaOS**

```
iot radio-profile "int-scan"
    radio-mode none ble
    ble-opmode scanning
!
ap-group <ap-group>
    iot radio-profile "int-scan"
!
iot transportProfile "Azure-IoT-Hub-ble-data"
    serverType Azure-IoTHub
    deviceClassFilter all
    bleDataForwarding
    azure-dps-id-scope <scope-id>
    azure-dps-auth-type group-enrollment symmetric-key <key>
    include-ap-group <ap-group>
!
iot useTransportProfile "Azure-IoT-Hub-ble-data"
```

**Aruba Instant**

```
iot radio-profile "int-scan"
 radio-mode ble
 ble-opmode scanning
 exit

iot use-radio-profile "int-scan"

iot transportProfile "Azure-IoT-Hub-ble-data"
 endpointType Azure-IoTHub
 payloadContent all
 bleDataForwarding
 azure-dps-id-scope <scope-id>
 azure-dps-auth-type group-enrollment symmetric-key <key>
 exit

iot useTransportProfile "Azure-IoT-Hub-ble-data"
```