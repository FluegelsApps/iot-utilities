---
layout: default
title: SES Imagotag ESL Configuration 
has_children: false
parent: Configuration
nav_order: 4
---

# SES Imagotag ESL configuration

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

SES-Imagotag’s Electronic Shelf Label system uses a [vendor-specific](#vendor-specific-implementations) USB integration with the Aruba infrastructure using a dedicated set of configuration commands.
In ArubaOS the SES-Imagotag configuration is enabled in the [`ap system-profile`](#aruba-cli-reference---ap-system-profile) where Aruba Instant uses an `sesimagotag-esl-profile`.

|ArubaOS|Aruba Instant|Description|
|-|-|-|
|`ap system-profile <ap-system-profile-name>`|n/a|**Name** of the ap system-profile.<br>Only supported on ArubaOS.<br>Required input values:<br>- ***ap-system-profile-name*** - AP system profile name|
|n/a|`sesimagotag-esl-profile`|Adds a SES-Imagotag ESL configuration profile.<br>Only supported on Aruba Instant.|
|`sesImagotag-esl-channel <esl-channel>`|`sesImagotag-esl-channel <sl-channel>`|The the radio channel of SES-Imagotag ESL radio.<br>Available options are:<br> - ***esl-channel*** - Range [0-10], 127 is ESL-server managed channel.<br>***Note:***<br>**ArubaOS:** If no ESL channel is configured the AP will select a channel automatically at boot time (but not automatic change later).<br>**Aruba Instant:** A static channel or 127 has to be set manually. There is no auto channel selection on Aruba Instant.|
|`sesImagotag-esl-radio-coexistence`|`sesImagotag-esl-radio-coexistence`|Enables the coexistence function between the SES-Imagotag ESL radio and the AP 2.4G Wi-Fi radio. When ESL radio tries to transmit packets the Wi-Fi 2.4 GHz radio is suspected for milliseconds to reduce interference.<br>(Default: **Enabled**)|
|`sesImagotag-esl-server <FQDN>`|`sesImagotag-esl-server <FQDN>`|Adds the FQDN of SES-Imagotag ESL server. FQDN setting has a higher priority than `sesImagotag-esl-serverip` if both are confiugured.<br>Available options are:<br> - ***FQDN*** - FQDN of the SES-Imagotag ESL server.|
|`sesImagotag-esl-serverip <ip-address>`|`sesImagotag-esl-serverip <ip-address>`|Configures the ip address of the SES-Imagotag ESL server.<br>Available options are:<br> - ***ip-address*** - SES-Imagotag ESL server ip address|
|`sesImagotag-esl-tls-auth`|`sesImagotag-esl-tls-auth`|Enables TLS authentication of the AP with the SES-Imagotag ESL server. The AP uses the factory default TPM certificate to autheitcated itself to the SES server and use the pre-loaded SES server’s trusted root certificate to validate the SES server certificate<br>(Default: **Disabled**).|
|`sesImagotag-esl-tls-fqdn-verify`|`sesImagotag-esl-tls-fqdn-verify`|Enables TLS certificate verification for the SES-Imagotag ESL server connection checking the configured FQDN against the TLS certificate presented by the SES-Imagotag server during connection establishment. Only applies if `sesImagotag-esl-server <FQDN>` is configured to use the SES cloud server.<br>(Default: **Disabled**)|  

Please find an example configuration [here](#ses-imagotag)