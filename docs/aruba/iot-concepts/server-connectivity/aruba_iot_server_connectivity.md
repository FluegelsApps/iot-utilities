---
layout: default
title: IoT-Server Connectivity
has_children: true
parent: Aruba IoT Concepts
---

## [IoT server connectivity (server-side)](#table-of-contents)

On the server-side IoT data payloads are either forwarded directly by [USB-to-ethernet](#usb-to-ethernet) connected devices using IP transport or using the [Aruba IoT server interface](#aruba-iot-server-interface) providing different transport protocols and data encapsulations.

USB-to-ethernet connectivity only requires applying a [Wired-Port profile](#wired-port-profile) to the APs USB port to give the USB host system ethernet/IP access. The benefit of this approach is that USB host system's network access can be separated from the AP management networks e.g. by assigning a different VLAN and can be controlled using the AP integrated firewall like any other wired ethernet client connected to the AP. The USB host system uses its own IP stack with a separate IP address for its communication to the remote IoT system.

>***Note:***  
>Vendor specific USB implementations like [SES Imagotag Electronic Shelf Labels (ESL)](#ses-imagotag-esl-configuration) are using IP transport with a [vendor specific configuration](#vendor-specific-implementations).  