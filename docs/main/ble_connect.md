# BLE-Connect

This feature uses the Aruba IoT-Interface BLE-Connect functionality to connect to surrounding bluetooth devices via GATT. All GATT-Actions are redirected to the sensor which executes them on the local device.

## Connecting to a device

## Pairing & Bonding with a device

## Interacting with a device

### Default interaction methods

### Philips Hue Control Panel

This app provides an interface to control Philips Hue lamps via the IoT-Interface. We currently support:
 - Turning the lamp on & off
 - Adjusting the brightness of the lamp
 - Changing the color of the lamp (only presets, color picker is **Work in Progress**)
 - Changing the color temperature of the lamp (only presets, color picker is **Work in Progress**)
 - Playing simple animations on the lamp (e.g. Flashing)

There are several steps that have to be done in order to communicate with the lamp.

#### 1) Reset the lamp via the "Philips Hue Bluetooth Application" ([Android](https://play.google.com/store/apps/details?id=com.signify.hue.blue&gl=DE)/[IOS](https://apps.apple.com/de/app/philips-hue-bluetooth/id1456604186))

The Philips Hue lamp needs to be reset to factory settings in order to establish a new connection. By doing so, the lamp enters it's initial pairing state, allowing the app to establish a secure connection. The app will be able to do this process automatically in a future version.

>***Note:***
>The lamp will change it's MAC-Address when resetting to factory mode. Make sure to select the latest MAC-Address of the device when connecting as both the old and the new address might be visible in the app. The "BLE-Scanning" functionality of the app can be used to get the address.

#### 2) Adding the connection preset

The next step is to start the IoT-Utilities App and the IoT-Server. The lamp has to appear in the "BLE-Telemetry" section of the app in order to establish a connection. Once the data is available, go to the "BLE-Connect" page of the app. Tap the "Add-Button" in the bottom-right corner of the screen. Select "Import from BLE-Telemetry" and select your lamp. The field at the top of the page can be used to search for the name of the lamp. Once selected, select the connecting sensor or enable "Automatically select sensor". If enabled, the app will select a sensor depending on the received signal strengths of the device. The sensor that received the strongest signal will be selected for a connection. Tap "Save" to save your connection preset.

#### 3) Establish a connection

Tap the connection preset to establish a connection. The app will automatically detect the type of the lamp and will bond the lamp to the sensor. Once established, the app will show an interaction view for the lamp. This page can be used to change the values of the lamp explained in [Philips Hue Control Panel](#philips-hue-control-panel). The connection can be restablished at any time as the lamp now is bonded. This can be removed by either tapping the three dots on the tab and selecting "Remove bond information" or deleting the connection preset. If the bond information has been deleted, the app won't be able to reconnect without resetting the lamp to factory settings again.
