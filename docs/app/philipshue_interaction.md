---
layout: default
title: Philips Hue - Interaction
parent: Main
grand_parent: App Documentation
---

# Philips Hue Interaction

The app provides a feature to control Philips Hue lamps. This feature uses BLE-Connect and the BLE GATT protocol to communicate with the lamp. The Philips Hue lamp needs to be bonded to the remote sensor in order to accept incoming commands.

> **_Note:_** Feature requires ArubaOS/InstantOS 8.8 or higher for BLE authentication and encryption.

![Philips Hue Interaction Scheme](../images/app_philipshue_interaction.svg)

## Interaction layout

### 1) State switch

Tap this button to turn the Philips Hue Lamp on and off. This switch will automatically apply to the current state of the lamp.

### 2) Brightness slider

Use this slider to manually set the brightness of the Philips Hue lamp. This slider will automatically apply to the current state of the lamp.

### 3) Color Temperature slider

Use this slider to manually set the color temperature of the Philips Hue lamp in Kelvin (approx. range: 2000K - 6500K). This slider will automatically apply to the current state of the lamp.

### 4) Color picker button

Tap this button to select the new color of the Philips Hue lamp. This button will show a rgb color picker in order to select the new color. The app is currently not capable of retrieving the current color of the lamp.

### 5) Animation button

Tap this button to play an animation on the Philips Hue lamp. Available animations:

|Animation|Details|
|-|-|
|White Flash Animation|The Hue lamp will start flashing in a white color every 500 ms.|
|Rainbow Animation|The Hue lamp will start switching the colors like a rainbow.|

### 6) Auto-Update Configuration button

Tap this button to configure the auto updating of this page. The appearing dialog can be used to enable/disable the auto updating and set the timeout of feature. This feature will fetch all values of the lamp every time the timer expired. This feature is only available for ZigBee, as BLE supports realtime updates of the page.

### 7) Identify Lamp button

Tap this button to identify the connected lamp. This feature will make the lamp flash three times to identify. This feature is only available for ZigBee, as this device is exclusive to the ZigBee framework.

### 8) Rename Hue Lamp button

Tap this button to rename the Philips Hue Lamp. This feature will change the local BLE name of the lamp. This feature is only available for BLE, as the name of ZigBee devices cannot be changed.

### 9) Factory default reset button

Tap this button to reset the Philips Hue Lamp to factory default settings. This will also remove the bonding from the application.

> **_Note:_** This application supports controlling Philips Hue Lamps via ZigBee and Bluetooth Low Energy (BLE). However, not all features all available for both platforms.

|Feature|BLE|ZigBee|
|-|-|-|
|State control|X|X|
|Brightness control|X|X|
|Color control|X|X|
|Animation control|X|X|
|Auto-Update configuration|O|X|
|Identify Lamp feature|O|X|
|Renaming the Lamp|X|O|
|Factory default reset|X|O|

X - Available, O - Not Available