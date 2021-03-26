# BLE Testing

This document explains the concept of the feature BLE-Testing which uses the [Aruba IoT Interface](../aruba/aruba_iot_concepts_and_configuration.md)

![Concept of BLE-Testing](https://github.com/FluegelsApps/iot-utilities/raw/documentation-dev/docs/images/ble_testing_graphic.png)

## Main concept

## Testing beacon

The testing beacon uses Apple's iBeacon protocol and will be used during the entire test. It will be generated during the setup process but the user can also create a new or pick an existing advertiser from the internal database.

|Value|Description|Example|
|-|-|-|
|UUID|Type 4 Univerisal Unique Identifier (pseudo-randomly-generated) refering to [RFC 4122](https://www.ietf.org/rfc/rfc4122.txt)|636645d0-2020-2020-2021-dfbaa5d78db8|
|Major|Integer value between 0 and 65536|119|
|Minor|Integer value between 0 and 65536|1278|

> **_Note:_** All values will be generated during setup and can be modifed at any time.
