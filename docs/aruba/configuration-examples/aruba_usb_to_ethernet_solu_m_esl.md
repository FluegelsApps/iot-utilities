---
layout: default
title: Solu-M ESL
has_children: false
parent: USB-to-Ethernet Solutions
grand_parent: Configuration Examples
nav_order: 0
---

# Solu-M ESL

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

This example shows the required configuration to enable the [Solu-M ESL soltuion](https://solumesl.com/).

-   `vlan-id` - has to be replaced with the desired access vlan id to be used for the ESL USB gateway
-   `ap-group` - has to be replaced with the AP group name the configuration should be enabled on (multiple statements are required for multiple groups) (ArubaOS only)

>***Note:***  
>The ArubaOS configuration tunnels the ESL USB gateway traffic to the Aruba controller into the vlan `vlan-id` controlled though the controller firewall.  
>
>The Aruba Instant configration egress the ESL USB gateway traffic at the access point uplink port into the desired vlan (tagged). The AP's uplink switche port has to allow the `vlan-id` tagged.  

**ArubaOS**

```
ap usb-acl-prof "Solu-M-USB-GW-acl"
    rule vendor All action permit
!
ap usb-profile "Solu-M-USB-GW"
    usb-acl-profile "Solu-M-USB-GW-acl"
!
ap-group <ap-group>
    usb-profile "Solu-M-USB-GW"
!
ip access-list session allowall
    any any any permit
    ipv6 any any any permit
!
user-role Solu-M-USB-GW
    access-list session allowall
!
aaa profile "Solu-M-USB-GW_aaa_prof"
    initial-role "Solu-M-USB-GW"
!
ap wired-ap-profile "Solu-M-USB-GW-wiredApProf"
    wired-ap-enable
    switchport access vlan <vlan-id>
!
ap wired-port-profile "Solu-M-USB-GW-wiredPortProf"
    wired-ap-profile "Solu-M-USB-GW-wiredApProf"
    aaa-profile "Solu-M-USB-GW_aaa_prof"
!
ap-group <ap-group>
    enet-usb-port-profile "Solu-M-USB-GW-wiredPortProf"
!
```

**Aruba Instant**

```
usb acl-profile "Solu-M-USB-GW-acl"
 rule Solu-M-SLG-DM101 permit
 exit

usb profile "Solu-M-USB-GW"
 usb-acl "Solu-M-USB-GW-acl"
 exit

usb-profile-binding "Solu-M-USB-GW"

wlan access-rule "Solu-M-USB-GW-wiredPortProf"
 rule any any match any any any permit
 exit

wired-port-profile "Solu-M-USB-GW-wiredPortProf"
 switchport-mode access
 allowed-vlan <vlan-id>
 native-vlan <vlan-id>
 no shutdown
 access-rule-name "Solu-M-USB-GW-wiredPortProf"
 type employee
 exit

enet-usb-port-profile "Solu-M-USB-GW-wiredPortProf"
```