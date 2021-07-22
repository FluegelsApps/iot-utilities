---
layout: default
title: BLE Telemetry
parent: Main
grand_parent: App Documentation
---

# BLE Telemetry

![BLE Telemetry Scheme](../images/main_northbound_data.svg)

This page contains the BLE-Telemetry entries/devices that have been received in Telemetry Northbound packages by the server.

## 1) Filter interface

When this button is pressed, the filter configuration layout will appear. This layout will allow the user to configure different BLE-Telemetry filters. The filter interface can hold multiple filters of the same and different types.  
Different filter types are compared using AND, e.g. if the filters "Name" and "Mac" are applied, the devices have to fulfill both criteria.  
Identical filter types are compared using OR, e.g. if two filters of the type "Name" are applied, the devices have to fulfill only one of the provided filters.  
Additionally the filter layout of this page also provides two sliders to select minimum/maximum signal strength (RSSI) values.

|Filter|Usage|Example|
|-|-|-|
|Name|Local name of the BLE-Device|Hue Lamp|
|Mac|Local MAC-Address of the BLE-Device|AA:BB:CC:DD:EE:FF|
|Protocol|Protocols of the BLE-Device|unclassified, arubaBeacon, arubaTag, zfTag, stanleyTag, virginBeacon, enoceanSensor, enoceanSwitch, iBeacon, allBleData, RawBleData. eddystone, assaAbloy, arubaSensor, abbSensor, wifiTag, mySphera, sBeacon, williot, ZSD, serialdata, exposureNotification, onity, minew, google|
|Client IP|Local IP-Address of the client that sent this package to the server|192.168.100.XX|
|Sensor IP|Local IP-Address of the Aruba Access Point/sensor that reported the device|192.168.100.XX|
|Sensor Mac|Local MAC-Address of the Aruba Access Point(sensor|AA:BB:CC:DD:EE:FF|
|Sensor Name|Local name of the Aruba Access Point/sensor|ap505|

## 2) BLE-Device item

![BLE Telemetry Item Scheme](../images/main_ble_device_item.svg)

This item represents a BLE-Device in range of the device.  
Tap this item to show the detailed information on this device. Tap and hold this item to copy the advertiser information into the local database or establish a connection via the [BLE-Connect](./ble_connect.md) feature. This information is available as a custom advertiser in the [BLE-Advertising](./ble_advertising.md) page.

### a) Protocol icon

Displays the icon of the current protocol of the BLE-Device. Supported protocols: iBeacon, EddyStone (unspecific), ExposureNotification

### b) Information summary

This view contains the main information of the BLE-Device. The upper text of this view displays the MAC-Address of the BLE-Device. The lower text of this view displays the protocols of the BLE-Device, if available.

### c) Transmission strength

Displays the last transmission strength (RSSI) value in dBm.

## Menu items

### Keep screen on

If this checkbox is enabled, the screen of the device will not turn off automatically.

### Documentation

Tap this item to open the documentation of this page.

### Guide

Tap this item to start the interactive guide of this page.