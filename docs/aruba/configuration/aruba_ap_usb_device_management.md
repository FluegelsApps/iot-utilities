---
layout: default
title: AP USB Device Management
has_children: false
parent: Configuration
nav_order: 2
---

# AP USB device management
  
<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

AP USB device management controls connected USB devices using USB profiles and USB ACL profiles. An USB ACL profile is assigned to an AP or AP group using an USB profile.

## USB ACL profile

An USB ACL profile consists of one or more permit/deny rules for supported USB vendor-product names. An USB ACL profile includes an implicit *deny-all* at then end. An USB profile with an undefined USB ACL profile applies a *permit-all* by default.

>***Note:***  
>Up to 16 USB ACL profiles are supported.

|ArubaOS|Aruba Instant|Description|
|-|-|-|
|`ap usb-acl-prof <usb-acl-profile-name>`|`usb acl-profile <usb-acl-profile-name>`|**Name** of the USB ACL profile|
|`rule vendor <vendor-name> action <permit/deny>`|`rule <vendor-name> <permit/dena>`|Configure an ACL rule for a supported USB ***vendor-name***.<br>Available options are:<br> - ***vendor-name*** - USB vendor name, ***All*** allows all supported vendors<br><br>Available action value to perform if the vendor-name matches.<br>Available options are:<br> - ***deny*** - Access to USB device is denied<br> - ***permit*** - Access to USB device is refused|

>***Note:***  
>The `show usb supported vendor-product` command lists the supported USB vendor-names on Aruba Instant APs.

## USB profile

An USB profile binds a specific USB ACL profile ton an AP or AP group.

|ArubaOS|Aruba Instant|Description|
|-|-|-|
|`ap usb-profile <usb-profile-name>`|`usb profile <usb-profile-name>`|**Name** of the USB profile|
|`usb-acl-profile <usb-acl-profile-name>`|`usb-acl <usb-acl-profile-name>`|Assigns an previously defined USB profile to the USB profile.<br>Available options are:<br> - ***usb-acl-profile-name*** - Name of the USB ACL profile|

An USB profile is bound to an AP or AP group using the following commands:

**ArubaOS**

```
ap-group <ap-group-name>
    usb-profile <usb-profile-name>
```

For details about the `ap-group` configuration refer to the [ArubaOS CLI Reference - ap-group](#aruba-cli-reference---ap-group).

**Aruba Instant**

```
usb-profile-binding <usb-profile-name>
```

For details about the `usb-profile-binding` configuration refer to the [Aruba CLI Reference - USB profile binding](#aruba-cli-reference---usb-profile-binding).

Examples:

**ArubaOS**

```
ap usb-acl-prof "UsbAclProf1"
    rule vendor All action permit
!
ap usb-profile "UsbProf1"
    usb-acl-profile "UsbAclPro1"
!
ap-group "ApGroup1"
    usb-profile "UsbProf1"
!
```

**Aruba Instant**

```
usb acl-profile "UsbAclProf1"
 rule  All  permit
exit
usb profile "UsbProf1"
 usb-acl "UsbAclProf1"
exit
usb-profile-binding "UsbProf1"
```