## Version 1.2.0 | ?

### New features in this release:

- new BLE-Connect feature

### Reworked features and improvements:

### Fixed bugs and issues

## Version 1.1.0 | 02.04.2021

### New features in this release:

- added support for multiple connections and WebSockets per client
- added client allow-list and deny-list
- replaced "Reconnecting"-status with "Authenticated"-status
- added maximum connection threshold (other connections will be discarded)
- added cooldown timer for offline connections (session will be removed when time expired)
- added "IoT-Connector" support (**early access**)
    - new "IoT-Connector"-page with guide and documentation
    - new "IoT-Connector-Details"-page with guide and documentation
    - support for Telemetry and BLE-data topic
- new authentication features
    - added url-encoded client connection
    - added authentication during handshake if supported by the client
- Material Components library updated to 1.3.0
    - new date dialog (certificate generation)
    - new time dialog (certificate generation)
    - updated and improved animations

### Reworked features and improvements:

- reworked documentation link handling
- reworked IoT-Server

### Fixed bugs and issues:

- fixed issue that caused app to crash when switching theme in BLE-Advertising page
- fixed BLE-Scanning performance issues

---

## Version 1.0.1 | 27.03.2021

### New features in this release:

- new reload-gesture for web-based content (licenses, documentation, ...)
- dedicated BLE-Testing beacon
    - new dialog to select any existing beacon for testing
    - new views to edit this beacon between tests
    - testing now uses advertising service
- new BLE-Testing guide
- new BLE-Testing documentation (Work in progress)
- new client configuration documentation
- new documentation features
    - new reload-gesture
    - support of markdown anchors and tables
    - support of links and references
- new crash-management tab in settings
    - view all recent crashes
    - detailed error output
    - share and export crash logs

### Reworked features and improvements:

- reworked BLE-Testing (improvements & new features)
- reworked documentation link handling
- changed configuration template "interval" value to 60s

### Fixed bugs and issues:

- fixed issue that BLE-Testing sometimes crashed due to UI-failures
- fixed issue that RSSI-History sometimes crashes due to concurrent data modification
- fixed issue that causes app to crash when starting any service on OnePlus devices

---

## Version 1.0.0 | 21.03.2021

### New features in this release:

- added new features to BLE testing
    - new "Sensor timeout" value
    - new "RSSI threshold" value
    - implemented interface to modify test beacon in testing page
- ability to pause / resume the server in the status notification
- ability to pause / resume the server in the launcher shortcut
- ability to freeze the data view in the details page
- swipe gesture to disconnect / delete clients in the client view  
    - swipe the client to the right side to delete this client and ALL of the data received from this client  
    - swipe the client to the left side (when receiving data) to close the connection  
- auto-complete engine for filtering (all pages: clients, sensors, main data, scanning)
- ability to have multiple filters of same type
- added all Aruba device classes to filtering
- app automatically retries the last action if you grant missing permissions

##### Note: Android 11 introduced a delay for foreground services. If you start or stop the server it may take up to 10 seconds for the server to start or stop.

### Reworked features and improvements:

- reworked changelog-system and dialog  
    - expand / collapse changelog entries (similar to privacy statement)  
    - changed changelog to markdown format
- reworked BLE testing
- reworked filtering
- added dialog to choose certificate export location
- added colored background with action icon and name when swiping a list item

### Fixed bugs and issues:

- fixed issue that disabled certificate imports on Android 11 and higher
- fixed issue that disabled certificate exports on Android 11 and higher

- fixed BLE scanning performance (still lags on some devices, will be fixed in next release)
- fixed bug that sometimes destroyed filtering after devices rotation
- fixed bug that locked token expiration time in client view to 01.01.1970 (visual bug)
- fixed bug that caused app to crash when it was rotated at the end of the setup
- fixed bug that client status was stuck in "Handshaking..." when not sending messages
- fixed bug that client log messages sometimes were in wrong order and duplicated

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
