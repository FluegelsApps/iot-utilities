---
layout: default
title: IoT-Connector
parent: Main
grand_parent: App Documentation
---

# IoT-Connector

![IoT-Connector Scheme](../images/app_iot_connector.svg)

This page contains the IoT-Connector data/entries that have been received in IoT-Connector Northbound packages by the server.

> **_Note:_** The Aruba infrastructure of this feature is still in development. Therefore the app-side implementation of this feature is not final.

## 1) IoT-Connector item

![IoT-Connector Item Scheme](../images/app_iot_connector_item.svg)

This item represents an IoT-Connector data entry of the local database. The app currently does not put the reported devices of the data entry into a seperate database.  
Tap this item to view the data of the entry.

### a) Main content body

This view contains the main information of the data entry. The upper text of the item displays the parent client IP-Address of the entry. The center text of the item displays the topic of the package. This currently is either **TOPIC_BLE_DATA** or **TOPIC_TELEMETRY**. The lower text of the item shows the amount of reported devices in the data package.

## Menu items

### Keep screen on

If this checkbox is enabled, the screen of the device will not turn off automatically.

### Documentation

Tap this item to open the documentation of this page.