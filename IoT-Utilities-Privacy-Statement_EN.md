---
layout: default
title: Privacy-Statement (EN)
parent: Legal
---

# IoT-Utilities Privacy Statement (**EN**|[DE](./IoT-Utilities-Privacy-Statement_DE.md))

Valid as of <!--validof-->09/18/2022<!--validof-->

## Privacy Statement for IoT-Utilities App

Protecting your privacy as an app user is a high priority. This document explains how personal data and none-personal data is handled with regards to the "IoT-Utilities" app, hereinafter referred to as **"app"**. "Personal data" means all information that relates to an identified or identifiable natural person.

---

### _**1. Who is the provider of this app and who is responsible for processing your personal data?**_

The controller for the data processing and the contact for questions or suggestions regarding the app is:

Maximilian Flügel  
Vor dem Steintor 4  
38871 Ilsenburg (Harz)  
Germany  
E-Mail: [iot-utilities@arubademo.de](mailto:iot-utilities@arubademo.de)

---

### _**2. What is the purpose of this app?**_

The app is used to demonstrate and test the "Aruba IoT Interface" functionality. More information about this functionality and its specification can be found here:

Aruba Support Portal  
[https://asp.arubanetworks.com/downloads;search=iot](https://asp.arubanetworks.com/downloads;search=iot)

ArubaOS WLAN and Aruba Instant 8.6.0.x IoT Interface Guide  
[https://support.hpe.com/hpesc/public/docDisplay?docId=a00100259en\_us](https://support.hpe.com/hpesc/public/docDisplay?docId=a00100259en_us)

The app also offers other functions and tools, such as "Bluetooth Scanning" and "Bluetooth Advertising".

---

### _**3. What functions does this app offer?**_

#### **IoT-Server**

The app provides an IoT-server function that accepts connections from Aruba controllers and Aruba Instant access points via the Aruba IoT interface protocol. The IoT-server only allows (TLS/SSL) encrypted connections, which are authorized or authenticated via static access tokens or username and password. The required SSL server certificate can be imported into the app or a self-signed certificate can be generated. The IoT-server also provides a web dashboard via a (TLS/SSL) encrypted connection under the URL [https://[smartphone_IP_address]:[port]/dashboard](https://[smartphone_IP_address]:[port]/dashboard). Access to the dashboard is secured using a username/password combination assigned in the app settings.  

#### **BLE Testing**

This function allows the app to validate the current configuration by sending iBeacon-Advertisements to nearby Aruba access points by using the Aruba-IoT-Interface. If the configuration is valid, the app receives the emitted signals back via the interface. The app will keep track of the responding access points and their signal strength.

#### **BLE Connect**

This function allows the app to connect to BLE-Devices using the Aruba access points. Furthermore, the app is capable of pairing and bonding the BLE-Device. The key material that is used throughout this process is stored securely in an encrypted database. The app also stores the MAC-Addresses of the BLE-Devices and the Aruba access points.

#### **ZigBee**

This function allows the app to send data to ZigBee devices in the network of the Access Point. The app stores the ZigBee-Address of the device as well as the MAC-Address of the Access Point and its radio. Furthermore, the app supports the interaction with Philips Hue Lamps.

#### **EnOcean Serial Data**

This function allows the app to send data to and receive data from EnOcean Serial devices in the network of the Access Point. Moreover, the application implements various EnOcean Equipment Profiles in order to control the devices.

#### **Bluetooth Scanning**  

This function of the app shows all Bluetooth Low Energy (BLE) devices in range of the smartphone in a list. A Bluetooth-enabled smartphone is required for this capability. Detailed information about the recorded BLE devices are also available.  

#### **Bluetooth Advertising**  

With this function, the smartphone works as a Bluetooth transmitter. Various Bluetooth packages, so-called advertisements, can be created and sent. There are different Bluetooth protocols, e.g. iBeacon or Eddystone available.  

---

### _**4. What is the purpose and the legal basis for the data collection and processing (Art. 6 GDPR)?**_

The data processing takes place for the following purposes and on the following legal basis:

- Exclusively for the provision of the app and its functionalities to the extent required for this (Art. 6 Para. 1 b) GDPR). Personal data are generally deleted as soon as further processing is no longer necessary for the purposes of contract implementation.

- If consent has been given for data processing to the extent specified in this privacy statement (Art. 6 Para. 1 a) GDPR).

Consent to data processing can be given when the app is started for the first time. The app cannot be used without consent. Consents are always voluntary and can be freely revoked at any time. To revoke the consent the app have to be uninstalled or the app data being deleted under:  

Android:  
Settings -> Apps -> IoT Utilities -> Uninstall  

Settings -> Apps -> IoT Utilities -> Storage -> Erase data  

A revocation does not affect the legality of the data processing carried out based on the consent until the revocation.

---

### _**5. Which permissions does this app need?**_

This app requires permissions to access functions and data on the smartphone to provide its functions, which must be granted when the app is installed. If these permissions are not granted, certain functions are not available, or the app cannot be used at all.Depending on the operating system, app permissions are partially granted automatically or, in the event of potentially dangerous access, e.g. to sensitive data such as position data are explicitly given by the user. In particular, the app uses data that is entered and, if permitted, data that is available on the device or that is generated by using device functions.

The following authorizations are required and requested when installing or starting the app for the first time:  

- #### **Location**  

Android permissions (user query):  
[_android.permission.access\_coarse\_location_]  
[_android.permission.access\_fine\_location_]  

This app requires access to the location function of the device. This permission is required to access the Bluetooth Low Energy (BLE) interface of the smartphone. Furthermore, the application is capable of sending location data to Aruba Access Points for configuration purposes only. This connection is permanently encrypted (SSH). No location information is stored persistently by the app.

- #### **Storage (read / write)**

Android permissions (user query):  
[_android.permission.write\_external\_storage_]  
[_android.permission.read\_external\_storage_]  

The app requires read and write access to the external memory of your smartphone in order to be able to save temporary files for various functions as well as configuration files.

- #### **Bluetooth**  

Android permissions (granted automatically):  
[_android.hardware.bluetooth\_le_]  
[_android.permission.bluetooth_]  
[_android.permission.bluetooth\_admin_]
[_android.permission.bluetooth\_scan]
[_android.permission.bluetooth\_advertise]
[_android.permission.bluetooth\_connect]

This app requires access to the smartphone's Bluetooth system in order to be able to provide the "Bluetooth scanning" and "Bluetooth advertising" functions.

> **_Note:_** In Android 12 and above the permissions [android.permission.bluetooth\_scan], [android.permission.bluetooth\_advertise] and [android.permission.bluetooth\_connect] are summarized and displayed as the permission "Nearby devices".

- #### **Internet**

Android permissions (granted automatically):  
[_android.permission.internet_]  

This app requires access to the device's Internet connection in order to be able to provide the "IoT-server" function and to download the BLE MAC manufacturer list from the Internet (optional).

- #### **Wi-Fi and network information**

Android permissions (granted automatically):  
[_android.permission.access\_wifi\_state_]  
[_android.permission.access\_network\_state_]  

This app requires access to the network information of the smartphone in order to be able to provide the "IoT server" function.

- #### **Foreground services**

Android permissions (granted automatically):  
[ android.permission.foreground_service ]

The app requires the "foreground-service" permission to be able to run the "IoT-Server", "BLE Advertising" and "BLE Testing" functions in the background. This feature is optional and can be enabled / disabled in the settings of the application.

The granted permissions can be viewed/granted/withdrawn at any time in the app under Settings -> Permissions or in the device settings:  

Android:  
Settings -> Apps -> IoT Utilities -> Permissions  

---

### _**6. When and how are push notifications used?**_  

The app uses push notification to show the status of the "IoT-Server", "BLE-Testing", "BLE-Connect" and "BLE-Advertising" functions.  

The push notification may be deactivated and reactivated at any time at:  

Android:  
System Settings: -> Apps -> IoT-Utilities -> App notifications

---

### _**7. Which data is collected, processed and saved by the app and for what purpose?**_

When downloading an app, the required information is transferred to the respective app store, in particular the username, email address, customer ID at the app store and the individual device ID. We have no influence on the collection and processing of this data. The operator of the respective app store is responsible for this.
Link to privacy policy of the app stores used by the app:

- [Google Play Services](https://www.google.com/policies/privacy/)

This app does not use personal data (privacy by design) unless these are essential for the app to function.  

The app does not store any data permanently, neither personal nor non-personal.  

The following data is recorded and processed by the app:

#### **Personal data (user)**

_IP address_  

To provide the "IoT server" function, the app queries the current IP address of the smartphone and uses it as the server IP address. The IP address is also dynamically inserted into configuration templates when these are retrieved and displayed by the user in the app. These configuration templates help to configure the Aruba Wi-Fi components to send data via the Aruba IoT interface to the "IoT server" function of the app.  
In addition, the IP address in the app's log data is used for troubleshooting and error correction. The IP address is only used for as long as the app is being used and is not stored permanently. The log data is deleted as soon as the app is closed.If the user copies the IP address from the app and continues to use it, e.g. when using the configuration templates, this is outside of ​​responsibility of this app and the user is responsible for protecting the data accordingly.

#### **Personal data (third party)**

##### _IP address_  

The "IoT server" function of the app provides a web server for establishing a connection between Aruba Controllers and Aruba Instant Access Points via the Aruba IoT interface protocol, as well as for a web-based dashboard. When establishing a connection to the app's web server, the connection information including the client's IP address is recorded. The IP address is only recorded for as long as the app is used and is not stored permanently. The log data of the web server is deleted as soon as the app is closed.

##### _BLE MAC addresses_  

The "Bluetooth Scanner" function of the app detects and displays all Bluetooth Low Energy (BLE) devices in range of the smartphone including the BLE MAC address of the respective devices. The recorded data is only displayed in the app on the local device if in use. Closing the app deletes all received data. No data is saved.

#### _Aruba IoT telemetry data_  

The "IoT server" function of the app provides the capability to receive and display data from third-party Aruba devices via the Aruba IoT interface. The received data can include personal data, in particular:

- MAC addresses of Bluetooth devices
- MAC addresses of Wi-Fi devices
- MAC addresses of ZigBee devices

The controller of the data processing of the data transmitted to the app through the Aruba IoT interface is the owner of the third-party system. The user of the app processes the data in accordance with Art. 28 GDPR as a processor.  

The security of the data transmitted via the Aruba IoT interface is ensured by a (TLS / SSL) encrypted connection between the app and the third-party systems.  

The data received by the "IoT server" function of the app is only displayed in the app on the local device as long as it is used. When the app is closed, all received data is deleted. No data is saved.

#### **Non-personal information**

Log data generated by the app is used for troubleshooting and error correstion and is only displayed on the local device as long as the app is used. All log data is deleted when the app is closed. No data is stored permanently.

##### _SSH usernames and passwords_

The app has a feature that allows the user to send commands to Aruba Access Points using the SSH (Secure Shell) protocol. An username and a password is required in order to establish a secure connection. The app does not store this information by default. However, the user can choose to store the data so that the credentials can automatically be used when the function is used in the future. The authentication credentials are saved in an encrypted database inside the application. The key to access this database is secured using biometrics. Consequently, the user's authentication and permission is always required when viewing/editing the data. Without the user authentication the app cannot access the data at any time. There is only one action the app can execute without the permission of the user and this is removing all the data from the database. Furthermore, the data is never passed to third parties and is automatically deleted in case the app is deleted or the user chooses the remove the data.

The authentication credentials can be managed at:

IoT-Utilities --> Settings --> IoT-Server --> Manage SSH Credentials

---

### _**8. What data is stored on the device?**_

The app stores the following data on the device to fulfill its function:  

- List of Bluetooth manufacturer IDs
- Configuration templates
- Exported certificates
- Exported configuration templates
- Exported log files
- Temporary data
- Bluetooth advertisers Database
- BLE-Connect presets database
- BLE-Connect bonding database
- ZigBee devices database
- ZigBee types database
- ZigBee flows database
- SSH usernames and passwords (optional)

---

### _**9. How long will the data be stored?**_

All personal data that this app uses during runtime is deleted as soon as the app is closed by the user. No personal data is stored permanently.  

Data that is stored in the file storage of the smartphone, e.g. configuration files are saved until the app will uninstalled or the files are manually deleted.

---

### _**10. How can user data be deleted in the app?**_

The data is deleted when the app is uninstalled or can be deleted manually at any time under:

Android:  
Settings -> Apps -> IoT Utilities -> Storage -> Delete data.

---

### _**11. Will data be passed on to third parties?**_

The app's data processing takes place exclusively locally on the installed device and only as long as the app is used or runs in the background.The app does not store or transmit any personal or other data to HPE, the developer or third parties. Furthermore, this app does not use any analysis or advertising services from Google or other providers.

---

### _**12. Is the usage behavior/user data evaluated by tracking tools?**_

Neither the usage behavior nor the data of the user are processed or analyzed by tracking tools or the like. Your personal data will not be processed for automated individual decisions including profiling within the meaning of Art. 22 Para. 1 GDPR and Art. 4 GDPR.

---

### _**13. What rights do I have? (Rights of the data subject, GDRP)**_

If you have declared your consent for any personal data processing activities, you can withdraw this consent at any time with future effect. Such a withdrawal will not affect the lawfulness of the processing prior to the consent withdrawal.  

Pursuant to applicable data protection law as a data subject affected by data processing, you may have the following rights:  

- #### Right to access (Art. 15 GDPR)

You have the right to access regarding the personal data being stored. This means that you have the right to obtain a confirmation as to whether or not personal data concerning you is processed, and, where that is the case, to request access to the personal data. The right of access includes – inter alia – the purposes of the processing, the categories of personal data concerned, and the recipients or categories of recipients to whom the personal data have been or will be disclosed. However, this is not an absolute right and the interests of other individuals may restrict your right of access. You may have the right to obtain a copy of the personal data undergoing processing.  

- #### Right to rectification (Art. 16 GDPR)

You may have the right to have incorrect personal data rectified. This means that you have the right to obtain from us the rectification of inaccurate personal data concerning you. Depending on the purposes of the processing, you may have the right to have incomplete personal data completed, including by means of providing a supplementary statement.  

- #### Right to erasure (&#39;right to be forgotten&#39;) (Art. 17 GDPR)
  
Under certain circumstances you can request the deletion of your stored personal data and there is an obligation to delete the personal data, insofar as their processing is not necessary to exercise the right to freedom of expression and information, to fulfill a legal obligation, for reasons of public interest or to assert, exercise or defend legal claims.

- #### Right to restriction of processing (Art. 18 GDPR)

You can request the restriction of the processing of your personal data if you dispute the accuracy of the data, the processing is unlawful, but you refuse to delete it. You also have this right if we no longer need the data, but you need them to assert, exercise or defend legal claims. You also have this right if you have objected to the processing of your personal data.

- #### Right to data portability in accordance with Art. 20 GDPR

You can request that we transmit the personal data you have provided to us in a structured, common and machine-readable format. Alternatively, you can request the direct transmission of the personal data you have provided to another person responsible, as far as this is possible.

- #### Right to object (Art. 21 GDPR)
  
You can revoke your consent to us at any time. The data processing based on the revoked consent may then no longer be continued in the future.

- #### Right of appeal to a supervisory authority (Art. 77 Para. 1 GDPR)

You can complain to the supervisory authority responsible for us, e.g. if you believe that we are processing your personal data in an unlawful manner.

---

### _**14. Changes to the privacy policy**_

This privacy statement reflects the status of the latest version of the app at the time of installation. If there are changes in the collection, processing or use of data due to new or changed functions of the app, this will be indicated when the app is updated and the user consents to the updated privacy statement will be requested. The current version of the privacy statement is always available in the app under:  

About -> Privacy Statement
