---
layout: default
title: Aruba IoT Configuration
has_children: true
nav_order: 3
---

# Configuration

In this chapter the ArubaOS/Aruba Instant configuration steps are described to setup the Aruba infrastructure for IoT solutions using ArubaOS/Aruba Instant version 8.8.0.0 or higher.

>***Note:***  
>For Aruba Instant deployments managed via [Aruba Central](https://www.arubanetworks.com/products/network-management-operations/central/) currently only [***template based***](#aruba-central-online-documentation---configuring-aps-using-templates) configuration is supported.  
>The Aruba Instant configuraiton described in this chapter can be applied using Aruba Central configuration templaes to manage the IoT configuration of cloud-based Aruba infrastrucure deployments.

The configuration of Aruba IoT integrations consists of two main steps:

1. **IoT radio-side configuration**
2. **IoT server-side configuration**

Depending on respective IoT solution different configuration settings are required.  

In the table below the required configuration items for step 1 and step 2 per IoT solution are listed:

|IoT solution|Step 1) [IoT radio-side](#iot-connectivity-radio-side) configuration|Step 2) [IoT server-side](#iot-server-connectivity-server-side) configuration|
|-|-|-|
|Wi-Fi solutions|Enable Wi-Fi radios (access or monitor mode)|[iot transport profile](#iot-transport-profile)|
|BLE solutions|[iot radio profile](#iot-radio-profile)|[iot transport profile](#iot-transport-profile)|
|ZigBee solutions|[iot radio profile](#iot-radio-profile) + [zigbee service profile](#zigbee-service-profile) + [zigbee socket device profile](#zigbee-socket-device-profile)|[iot transport profile](#iot-transport-profile)|
|ZigBee solutions (ASSA-ABLOY)|[iot radio profile](#iot-radio-profile) + [zigbee service profile](#zigbee-service-profile)|[iot transport profile](#iot-transport-profile)|
|USB/3rd party: USB-to-serial solutions|(optional) [USB ACL profile](#usb-acl-profile)/[USB profile](#usb-profile)|[iot transport profile](#iot-transport-profile)|
|USB/3rd party: USB-to-ethernet solutions|(optional) [USB ACL profile](#usb-acl-profile)/[USB profile](#usb-profile)|[Wired-Port profile](#wired-port-profile)|
|USB/3rd party: SES Imagotag ESLs|(optional) [USB ACL profile](#usb-acl-profile)/[USB profile](#usb-profile) + [SES Imagotag ESL configuration](#ses-imagotag-esl-configuration)|[SES Imagotag ESL configuration](#ses-imagotag-esl-configuration)|

>***Note:***  
>The IoT radio settings for USB/3rd party radios are controlled on the 3rd party system, if any, and there is no configuration required on the Aruba side. The only exception is the [SES Imagotag ESL configuration](#ses-imagotag-esl-configuration) which controls the ESL radio channel.  
>
>Which USB device are allowed to connect to an access point can be controlled using the [AP USB device management](#ap-usb-device-management).

For details about the different configuration steps requried to setup the IoT solutions layed out in the table above see the following chapters as well as the [configuratoin examples](#configuration-examples) chapter.