# BLE-Connect

This feature uses the Aruba IoT-Interface BLE-Connect functionality to connect to surrounding bluetooth devices via GATT. All GATT-Actions are redirected to the sensor which executes them on the local device.

## BLE-Connect Presets

The app uses "Presets" in order to save connection information of a specific device. This includes device MAC-Address, Access Points MAC-Address as well as the device name (optional). These preset can also save the "Bonding-Keys" when a device is bonded with an Access Point. They also offer the possibilty to automatically choose an Access Point depending on the received signal strength. The user can clone existing device information or manually create them.

## Connecting to a device

### Selecting an existing device

The app allows the user to select a device from the received data. This only applies to "BLE-Telemetry" and "BLE-Data". In order to start a connection, press and hold the item of a device. The app will prompt the user to select an action. Select "Estabilsh connection" to start the session. This will automatically create a preset for future connections. Information of existing devices can also be added by tapping "Add" and "Import from BLE-Telemetry" or "Import from BLE-Data" on the "BLE-Connect" page of the application.

### Manually configuring the connection

The app also allows the user to manually configure a connection. This feature uses the "BLE-Connect presets" to configure the connection. Open the "BLE-Connect" page of the app and tap "Add". Select "Create manually" to create the preset. Enter the required information to continue. Once the preset has been created, tap it to establish the connection.

## Pairing & bonding a device

Pairing and bonding bluetooth devices is used to encrypt and secure connections between two devices. The app also offers this functionality as some third-party devices require bonding or pairing in order to interact (e.g. Philips Hue).

## Interacting with a device

### Default interaction methods

The app provides a generic interface to control BLE devices via the BLE-Connect interface. Once connected, the app will display all available GATT-Services and characteristics of the device. Tap the Up-Arrow button the write a characteristic and the Down-Arrow button to read a characteristic. The field at the top of the list is used to filter the collection.

### Philips Hue Control Panel

This app provides an interface to control Philips Hue lamps via the IoT-Interface. We currently support:
 - Turning the lamp on & off
 - Adjusting the brightness of the lamp
 - Changing the color of the lamp (full RGB color picker)
 - Changing the color temperature of the lamp (only presets, color picker is **Work in Progress**)
 - Playing simple animations on the lamp (e.g. Flashing)

There are several steps that have to be done in order to communicate with the lamp.

#### Bonding the lamp and the sensor

There are multiple ways to bond the Philips Hue Lamp with an Aruba AP.

##### a) Straight-forward bonding with a new lamp

When using a new or recently reset Hue Lamp it is possible to bond the lamp directly without the press of a button. The app will automatically handle this if possible.

##### b) Bonding the lamp via the short-range app-interface

When using a Hue Lamp that is already in use and connected to other devices, the bonding requires an additional procdedure to authenticate. This also requires to distance between the client and the lamp to be less than 1m. This procedure can be started by tapping the options (three-dots) icon and selecting "Authenticate" in the session tab header. The app will notify the user that an automated bonding procedure is available. Tap "auto" to start the procedure. The app will try to authenticate via the alternative authentication method of the lamp. Make sure to be in range of the lamp. The app also notifies the user if the lamp is too far away.

> **Note:**
> The "distance between the client and the lamp" refers to the distance between the Hue Lamp and the Aruba Sensor. This does not apply to the distance between the app (mobile-device) and the lamp.
> This procedure does not work with every model of 

##### c) Resetting the lamp to factory settings

If the options a) and b) are not successful it is required to reset the lamp to factory settings in order to establish a new secure connection. This currently is only possible by using the Philips Hue App [[Android]()/[iOS]()]. When the lamp has been reset, it is possible to establish a new connection by using step a).

#### Controlling the Hue Lamp using the app

The IoT-Utilities App can be used to fully control the Philips Hue Lamps. The app provides an interface to do so.

#### 1) Main state button

This is the main button to control the state of the lamp.

#### 2) Brightness control slider

This slider can be used to set the brightness of the lamp (Values between 0 and 100%)

#### 3) Color control button

This button can be used to change the color of the lamp. Tapping the button will show a color selection dialog. This dialog can be used to select any color from the RGB-Space.

#### 4) Temperature control button

This button can be used to change the color temperature of the lamp. Tapping the button will show a dialog to select the color temperature. The app currently only supports different color temperature presets (default, cold, warm).

#### 5) Animation control button

This button can be used to start an animation on the lamp. Tapping the button will show a dialog to select an animation. Tap the same animation again to stop it.