---
layout: default
title: SES Imagotag
has_children: false
parent: USB Vendor Specific Solutions
grand_parent: Aruba IoT Config Examples
nav_order: 0
---

# SES Imagotag

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

This example shows the required configuration to enable an [SES-Imagotag ESL solution](https://www.arubanetworks.com/assets/pso/PSB_SESImagotag.pdf) on premise solution. All available configuration options are descirbed in the [SES Imagotag ESL configuration](../configuration/aruba_ses_imagotag_esl_configuration.md#ses-imagotag-esl-configuration)

-   `<ip-address>` - has to be replaced with the SES-Imagotag on-premises server IP address

**ArubaOS**

```
ap system-profile "iot-ap-system-prof"
    sesImagotag-esl-serverip <ip-address>
    sesImagotag-esl-channel 127
```

**Aruba Instant**

```
sesimagotag-esl-profile
 sesImagotag-esl-serverip <ip-address>
 sesimagotag-esl-channel 127
```