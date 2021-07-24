---
layout: default
title: Wired-Port Profile
has_children: false
parent: Configuration
nav_order: 3
---

# Wired-Port profile

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

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