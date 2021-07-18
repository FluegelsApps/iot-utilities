---
layout: default
title: Permission Settings
parent: Settings
grand_parent: App Documentation
---

# Permission settings

## Permissions
Tap any permission (not granted) to request the permission.

### Used permissions
- **Location Services**  
    This permission is used for BLE scanning and advertising. 
    The application never uses the location data of the device.
- **Bluetooth Services**  
    This permission is used for BLE scanning and advertising.
    Furthermore, the application requires bluetooth admin privileges to enable and disable the bluetooth interface as well to provide custom advertising.
- **Storage Access**  
    This permission is used for different features, including configuration templates, log files, certificate export, ...
- **Internet Connection**
    This permission is used to provide the IoT-Server feature.
    This is an internal permission and does not need to be granted by the user explicitly.
- **WiFi-/Network State**
    This permission is used to read your IP-Address and to stop the server if it loses connection.
    This is an internal permission and does not need to be granted by the user explicitly.

> **_Note:_** Detailed information is provided in the [Privacy Statement](../../IoT-Utilities-Privacy-Statement_EN.md) of the app.  
> Every granted permission can be reverted at any time.

### Open Android Settings
- Tap this setting to open the Android settings page for this app
- You can also manage permissions on this page