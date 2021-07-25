---
layout: default
title: Data Content Filters
has_children: false
parent: IoT-Server Connectivity
grand_parent: Aruba IoT Concepts
nav_order: 3
---

# Data content filters

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

In addition to filter for specific [device classes](../server-connectivity/aruba_iot_device_class_filters.md#device-class-filter) it possible to filter the forwarded IoT data content before being sent to the remote Iot system.

## General data filter

-   ***Data Filter***  
This is a list of data fields to be suppress in the telemetry reports. The data filter is a string that is a comma separated list of index-paths. Each index path refers to the field numbers in the [Aruba IoT Protobuf Specification](../../references/aruba_reference_documentation.md#aruba-iot-protobuf-specification). For example, the value  “3.3, 3.12” would suppress the ‘reported.model’ field and the ‘reported.beacons’ field in the telemetry reports.  

-   ***Device Count***  
Only sends the count of device types, e.g. iBeacon, Wi-Fi clients, seen by an AP in the telemetry reports, but not the actual device information of those devices. Supported device counts are defined in the [Aruba IoT Protobuf Specification](../../references/aruba_reference_documentation.md#aruba-iot-protobuf-specification).

## BLE data filter

-   ***RSSI Reporting Format***  
For the BLE RSSI values being send in the telemetry reports five different RSSI reporting formats are supported. The four reporting
formats are:
    -   **Average** - The average RSSI over the reporting interval will be reported.  
    -   **Last** -  Only the last RSSI value that was seen by the device will be reported.  
    -   **Max** - The max RSSI value that was seen over the reporting interval will be reported only. This max value resets each telemetry reporting interval and will be updated accordingly.  
    -   **Bulk** - The last 20 RSSI values that were seen by the device since the previous telemetry report will be reported in an array format.  
    -   **Smooth** -  A single smoothed out RSSI value will be reported for each telemetry report. This is done by attempting to remove outliers from the RSSI values received by the AP.  

-   ***Environment Type***  
Five different pre-defined environment types are supported to help adjust RSSI based distance calculation to better fit the environment in which the BLE devices are operating in. For best results, the value that closest corresponds to the environment in which BLE is operating should be chosen.  
    -   **auditorium**
    -   **office**
    -   **outdoor**
    -   **shipboard**
    -   **warehouse**
    -   **custom** (see custom fading factor for details)

-   ***Custom Fading Factor***  
If the pre-defined environment type offsets do not properly fit the environment, a custom fading factor can be configured by setting the environment type to ***custom***. This field accepts integer values in the range of 10 to 40.  

-   ***Cell Size Filter***  
A proximity-based filter that will only report devices that are found to be within an “x” meter radius around the access point. This distance is calculated with an algorithm based off the RSSI value. The default value for this field is “0”, which translates to the cell size filter being disabled. This field accepts integer values from 2 to 100 and the units are meters.  

-   ***Movement Filter***  
This filter is active when the cell size filter is also configured. When this filter is enabled, devices will only be reported if the difference between their current and prior distance is more than the configured filter value. For example, if the movement filter is configured to be 2 meters, a device that is calculated to have moved 1 meter will not be reported, while a device that moves 5 meters will be reported. The default value for this field is “0”, which corresponds to the movement filter being disabled. This field accepts integer values from 2 to 30, and the units are meters.  

-   ***Age Filter***  
The Age Filter is used to only report devices the AP has received an update (either BLE advertisement or scan response) in the configured time. For instance, if the age filter is set to 30 seconds, only devices which have been heard in the last 30 seconds will be reported. If there is a device that received an update 45 seconds before, this device will not be reported. The default value for this field is “0”, which corresponds to the age filter being disabled. This field accepts integer values from 30 to 3600, and the units are seconds.  

-   ***BLE Vendor Filter***  
The BLE Vendor Filter allows to input [Bluetooth SIG Vendor IDs](https://www.bluetooth.com/specifications/assigned-numbers/company-identifiers/) and/or freeform vendor name strings, which will be used to filter the devices being reported. If this is configured, the only devices that will be reported are the devices that match the configured Vendor ID or Vendor Name.  
The vendor ID is a 2-byte hexadecimal value preceding with 0x in 0xABCD format. The vendor name is a string that can be either a full vendor name (example:Aruba) or a substring of the actual vendor name (example:Aru) and can be case-insensitive.  
The vendor filter accepts up to five combinations of vendor names or vendorIDs separated by commas, for example:  
    -   Aruba,Favendo,HanVit,SoluM,ABB
    -   0xABCD,0xBCDE,0xCDEF,0xDEF0,0xEF01
    -   Aruba,0xABCD,Favendo,0xBCDE,HanVit  

    If more than one vendor name or vendorID is configured, then any of the matching vendor names or vendorIDs in the vendor filter is applied. A device is reported only if the vendor data or vendor name field is not empty and matches the vendor information configured. If the vendor field is not populated for the devices, the IoT devices are reported because there is not matching vendor filter in the IoT transport profile.

-   ***UUID Filter (iBeacon)***  
A list of UUIDs to filter the devices included in the reports. Applies only to iBeacon devices.

-   ***UID Namespace Filter (Eddystone)***  
A list of UID namespaces to filter devices included in the reports. Applies only Eddystone-UID devices

-   ***URL Filter (Eddystone)***  
A list of URL strings to filter devices included in the reports. Applies only Eddystone-URL devices. The string listed here can be a partial URL strings.

-   ***BLE data forwarding - per frame filtering***  
When [BLE data forwarding](../server-connectivity/aruba_iot_transport_services.md#ble-data-forwarding) is enabled, the raw payload contained within a BLE packet is forwarded to the configured server. The per frame filtering knob is a modifier on top of the BLE data forwarding knob. When only BLE data forwarding is enabled, all BLE packets for a device having a known device class filter label are forwarded.  
For example: If a device advertises an iBeacon frame and an Eddystone frame and in the [transport profile](../../configuration/aruba_iot_transport_profile.md#iot-transport-profile) the ***iBeacon*** device class has been selected only, then for this device both iBeacon and Eddystone frames are forward.  
If per frame filtering is enabled in addition to the BLE data forwarding , then only the raw payloads from the iBeacon frames will be forwarded.  