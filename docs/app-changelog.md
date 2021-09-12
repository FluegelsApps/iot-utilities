---
layout: default
title: Changelog
nav_order: 6
---

## Version 1.5.0 | 12.08.2021

### New features in this release:

- feature to switch Philips Hue interaction from BLE to ZigBee
- tap and hold devices in ZigBee devices list to identify them via the network

### Reworked features and improvements:

- reworked entire filtering system
- new toolbar style
- new animations (page transitions)
- minor style adjustments (status bar color, navigation bar color)

### Fixed bugs and issues:

- fixed bug in clients guide that caused app to crash
- fixed bug in Philips Hue Pairing that caused UI misbehaviours
- fixed bug in BLE-Connect that notified the user the device disconnected when the status "alreadyConnected" is received

---

## Version 1.4.0 | 31.08.2021

### New features in this release:

- additional Philips Hue features (BLE-Connect)
    - color temperature slider in interaction page
    - button to rename the Hue Lamp
    - page will change color according to the lamp
    - directly connect to lamps using the BLE-Scanner feature
- implementation of Aruba-IoT ZigBee functionality
    - Philips Hue implementation
        - interaction page identical to the BLE-Connect implementation
        - state control
        - brightness control
        - color temperature control
        - full color control (RGB, Hue, Saturation, XY)
        - demo animations (identical to BLE-Connect implementation)
        - lamp identification (lamp will flash 3 seconds)
        - ZigBee-Address can be resolved using the BLE-Connect feature of the app
    - generic implementation
        - actions: predefined/custom payloads that can be sent to the remote device
        - triggers: actions that can be triggered when receiving a specific message from the device (not supported yet)
        - custom messages: completely custom or predefined types e.g. On/Off Command, Read Request, ...
        - implemented message templates, clusters, profiles, attributes from ZigBee Cluster Library Specification
        - inbound/outbound messages graph
        - basic parsing of inbound/outbound ZigBee messages
    - device database
        - saves device information e.g. ZigBee-Address, Name, Reporter MAC, ...
        - types: collection of actions/triggers that can be shared across multiple devices
    - Aruba configuration template generator
        - ZigBee socket device template generation for Aruba OS & Instant
- additional BLE-Scanning features
    - detection of nearby Philips Hue Lamps when scanning for BLE devices
    - added new information to BLE-Devices details page
    - parts of information on BLE-Devices details page now copyable

### Reworked features and improvements:

- reworked user interface of copy dialog

### Fixed bugs and issues:

- fixed bug that disabled back press when completing any guide

---

## Version 1.3.1 | 31.07.2021

### Fixed bugs and issues:

- fixed bug that caused documentation to crash

---

## Version 1.3.0 | 30.07.2021

### New features in this release:

- new documentation home page
- new aruba documentation
- new documentation search feature
- updated Android dependencies

---

## Version 1.2.2 | 25.07.2021

### New features in this release:

- search function in app preferences
- relative anchors in app documentation

---

## Version 1.2.1 | 19.07.2021

### Fixed bugs and issues:

- fixed bug that caused app in BLE-Connect page to crash
- fixed bug in BLE-Connect bonds database that caused app to stop working
- fixed bug that caused app dashboard to crash

> **_Note:_** Reinstallation of the application may be required due to this update.

---

## Version 1.2.0 | 18.07.2021

### New features in this release:

- server traffic details page
    - evaluates data such as current read, current write, total data received
    - values displayed inside graph
- implementation of Aruba IoT BLE-Connect functionality
    - connecting to devices via sensors
    - authenticating, pairing and bonding with devices via sensors
    - reading and writing on GATT-services/characteristics of connected devices
    - support of GATT-Notification and GATT-Indication (currently only in interaction)
    - Philips Hue control panel
        - full control of Philips Hue lamps nearby
        - full RGB color control
        - color temperature control
        - animation support
- BLE-Connect presets
    - functionality to save connection presets (device and sensor)
    - shortcuts to open connections to previous devices
    - connection and security information of device can be stored
    - functionality to reconnect after successful authentication
- bug reporting feature
    - bugs and crashes can now be reported using the app
    - crashes: using the dialog that appears when the app crashes OR at Settings --> Advanced --> Recent crashes
    - bugs: using the app: Main drawer --> Report a bug
- new Web-Dashboard error page
- new documentation features
    - support of anchors
    - support of vector images
    - zoom gestures when viewing images
- new server features
    - support of both HTTP and HTTPS (HTTP requests, except for certificate download will be redirected to HTTPS because of security concerns)
    - global traffic analysis and output
    - per connection traffic analysis and output
    - server will save count and size of all messages instead of only relevant data
    - various versions of the TLS protocol can be enabled and disabled
        - protocol version and cipher suites of each client are displayed in the clients page
- new online documentation (iot-utilities.arubademo.de)
    - updated theme, content and navigation
- new status bar notifications
    - the app is now able to display critical errors in the statusbar of the device
    - this feature is e.g. used in case the app loses the connection to the local network

### Reworked features and improvements:

- updated dashboard
    - reworked style
    - additional server traffic card
- reworked certificate details page
- reworked certificate generator dialog
    - updated components
    - fixed data loss on rotation
    - added certificate generation in background without dialog
- reworked BLE-Testing beacon info dialog
    - new dialog style
    - displays all important information
    - values can be copied to clipboard
- added external content warning when opening links in documentation and licenses
- shortened and improved various log messages
- authentication no longer required when trying to download server certificate
- comments will now be removed when copying configuration templates

### Fixed bugs and issues:

- fixed bug: app crashing when rotating the dashboard
- fixed bug: advertiser name not cloned properly
- fixed bug: data collection not loaded when rotating in northbound details
- fixed bug: app crashing when deleting multiple clients at a time
- fixed bug: app crashing in clients list due to formatting errors 
- fixed bug: certificate was not downloadable from the web-dashboard
- fixed bug: anchors in documentation not always redirecting properly
- fixed bug: axis scale in history graph too big when receiving invalid RSSI
- fixed bug: BLE Testing advertiser has been removed after the guide has finished

---

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
