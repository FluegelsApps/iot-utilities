---
layout: default
title: IoT-Connectivity
has_children: true
parent: Aruba IoT Concepts
---

## [IoT connectivity (radio-side)](#table-of-contents)

On the radio-side the Aruba access points support different IoT radio technologies either though integrated radios or 3rd party solutions connected to the APs USB port.

### [**Wi-Fi**](#table-of-contents)

The Aruba access point Wi-Fi radios can be used to forward associated/unassociated client information and RTLS data for Wi-Fi based tracking use cases. Wi-Fi client and RTLS data is encapsulated in the [Aruba IoT server interface](#aruba-iot-server-interface) protocol and forwarded to the IoT backend system.  

### [**Aruba IoT radio**](#table-of-contents)

An Aruba IoT radio is an additional internal or external radio in the Aruba AP-3xx/5xx series access points that can be leveraged for IoT connectivity.  
A single Aruba AP-3xx/5xx series access points can support up to two IoT radios, one internal and one external. This would allow to use one radio e.g. for BLE and the other one for ZigBee concurrently.  
The access point removes/adds the radio specific headers from/to IoT devices e.g. BLE or ZigBee and forwards/receives the data payload encapsulated in the [Aruba IoT server interface](#aruba-iot-server-interface) protocol to/from the IoT backend system.  

#### ***Internal***

Aruba AP-3xx/5xx series access points provide an integrated Aruba IoT radio for the IoT connectivity supporting the following radio technologies:

- AP-3xx: BLE4 (Gen1)
- AP-5xx: BLE5/802.15.4 (Gen2) e.g. ZigBee

*BLE Wi-Fi Co-Existence*

Starting with ArubaOS/Instant OS version 8.8.0.0 **BLE Wi-Fi Co-Existence** has been introduced to improve the overall WLAN and BLE receiver performance and to prevent inter-modulation by coordinating WLAN and BLE traffic and avoiding WLAN and BLE transmitting simultaneously. The feature is enabled by default.

>***Note:***  
>BLE Wi-Fi Co-Existence is only supported on Aruba AP-53x and AP-55x series access point series for the internal Aruba IoT Gen2 radio.
>The Aruba AP-505H hospitality accdess point series has some internal HW-based filtering to compensate local interference that works differently to the BLE Wi-Fi Co-Existence feature.   

#### ***External***

In addition to the internal IoT radio Aruba also provides an [IoT expansion radio](https://www.arubanetworks.com/assets/ds/DS_IoT-Expansion-Radio.pdf) that supports the same radio technologies as the AP-5xx series internal IoT radio:  

- Aruba IoT Expansion Radio = BLE5/802.15.4 (Gen2) e.g. ZigBee

The intention of the Aruba IoT expansion radio is to add the 802.15.4(ZigBee) capability to the AP-3xx series access points.

>***Note:***  
>The internal and the expansion BLE5/802.15.4 (Gne2) IoT radio can be enabled to run BLE and ZigBee concurrently. But in this case the IoT radio can only transmit but not receive BLE packets, while the ZigBee communication works bi-directional.  
>  
> This allows enabling the APs BLE console as well as BLE beaconing (iBeacon) for indoor navigation use cases in parallel to ZigBee use cases. But BLE tracking uses cases like asset tracking are not supported in this case.  
>  
> In order to support BLE tracking or bi-directional use cases concurrently to ZigBee uses cases on the same access points two Aruba IoT radios Gen2, one internal and one external, are required. The external radio should be used as ZigBee radio in this case. Therefore this scenario is currently only supported on the Aruba AP-5xx series access points.

The configuration of the Aruba IoT radios is handled in the [IoT radio profile](#iot-radio-profile) configuration.

### [**USB/3rd party IoT radio's**](#table-of-contents)

Aruba supports the expansion of Aruba access points using the AP's USB port with supported 3rd party radio solutions. Depending on the particular solution the integration uses one of the following methods:

- USB-to-serial
- USB-to-ethernet

In all cases the USB connected host system removes/adds the radio specific headers/protocols from/to IoT devices and forwards/receives the data payload to the access point using one of the USB methods.

Supported USB connected devices does not required a specific configuration, except for vendor specific implementations, but it can be controlled which USB devices are allowed to connect to an access points. This can be controlled using the [AP USB device management](#ap-usb-device-management).

#### ***USB-to-serial***

The [3rd party solutions using the USB-to-serial](#supported-usb-vendor-list-for-iot) method forwards the data payload to/from the access point using [serial-data](#serial-data). The Aruba access point encapsulates the serial-data payload in the [Aruba IoT server interface](#aruba-iot-server-interface) protocol to/from the IoT backend system.

>***Note:***  
> No specific configuration is required for USB-to-serial devices. Serial data is only forwarded though the [Aruba IoT server interface](#aruba-iot-server-interface), if enabled in the [server-side configuration](#iot-server-connectivity-server-side).  

#### ***USB-to-ethernet***

The [3rd party solutions](#supported-usb-vendor-list-for-iot) using the USB-to-ethernet method provides ethernet/IP connectivity to the connected USB host system. The USB host system is connected to the access point in the same way as a wired ethernet client. No data processing is done by the access point and ethernet/IP data packets form the USB host system is forwarded like any other ethernet/IP traffic.

#### ***Vendor specific implementations***

The following vendor specific [USB integrations](#supported-usb-vendor-list-for-iot) do not follow the previously mentioned methods and require a dedicated configuration.  
 
- [SES Imagotag Electronic Shelf Labels (ESL)](#ses-imagotag-esl-configuration)