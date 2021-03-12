## Version 1.0.0 | 13.03.2021

### New features in this release:

- Implemented ability to pause / resume the server in the status notification
- Implemented ability to pause / resume the server in the launcher shortcut
- Implemented ability to freeze the data view in the details page
- Implemented swipe gesture to disconnect / delete clients in the client view
 - swipe the client to the left or right side (when it's offline) to delete this client
 - swipe the client to the left or right side (when receiving data) to close the connection
- Implemented auto-complete engine for filtering (all pages: clients, sensors, main data, scanning)

##### Note: Android 11 introduced a delay for foreground services. If you start or stop the server it may take up to 10 seconds for the server to start or stop.

### Reworked features and improvements:

#### Reworked the changelog dialog

- Expand / collapse changelog entries (similar to privacy statement)
- Changed changelog to markdown format

- Added dialog to choose certificate export location

### Fixed bugs and issues:

- Fixed issue that disabled certificate imports on Android 11 and higher
- Fixed issue that disabled certificate exports on Android 11 and higher

- Fixed BLE scanning performance (still lags on some devices, will be fixed in next release)
- Fixed bug that sometimes destroyed filtering after devices rotation
- Fixed bug that locked token expiration time in client view to 01.01.1970 (visual bug)
- Fixed bug that caused app to crash when it was rotated at the end of the setup

---

## Beta 0.9.8 | 11.03.2021

- fixed issue that disabled certificate import in newest Android update

---

## Beta 0.9.7 | 06.03.2021

- reworked web-dashboard
- reworked logging-system
- implemented recent update notifications
- the server is now able to run in the background with the app closed 
- ble testing is now able to run in the background with the app closed
- ble advertising is now able to run in the background with the app closed
- implemented new client authentication type "client secret"
- fixed issue: server port was not changeable
- huge server performance improvements (processing time has been reduced from aprox. 600ms to aprox. 2ms)
- various bug fixes

---

## Beta 0.9.6 | 08.02.2021

- added support for all device rotations, including new layouts for larger devices
- added tutorial views that show up the first time you open the app
       - can also be reopened via the "guide" section of each page
- added app documentation that can be opened via the "documentation" section of each page
- implemented new markdown license format
- reworked application setup
- various fixes and improvements

---

## Beta 0.9.5 | 28.01.2021

- Refactored big parts of the app, including:
  - Logging & Dashboard pages
  - Client & Sensor pages
  - Telemetry, BLE data & WiFi data pages
  - BLE scanning & advertising pages
- Huge performance improvements
- Layout improvements and changes
- Added BLE settings (scanning, testing)
- Various bug fixes
- Setup crash fixed

---

## Beta 0.9.4 | 17.01.2021

- Reworked data processing and layouts for all types of data
- Privacy notice updated
- Implemented Aruba Wi-Fi data messages
- Implemented feature to notify user about license changes
- Several bugs fixed
- input issues in iBeacon advertising layout fixed
- Styling updated

---

## Beta 0.9.3 | 05.01.2021

- Crash during authentication token generation on some devices fixed

---

## Beta 0.9.2 | 04.01.2021

- Layout issues on smaller devices fixed
- Handling of Aruba ApHealthStatus messages implemented
- Filter systems updated and reimplemented
- UI updated and changed
- Various bugs fixed

---

## Beta 0.9.1 | 02.01.2021

- Fixed various crashes
- Optimized memory usage / performance
- UI improvements & updates
- Implemented ability to manage server / certificate from dashboard
- Implemented ability to download config templates

---

## Beta 0.9.0 | 29.12.2020

- first public beta release of the application
