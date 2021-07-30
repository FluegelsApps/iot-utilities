---
layout: default
title: IoT-Server Settings
parent: Settings
grand_parent: App Documentation
---

# IoT-Server settings

## Server certificate

### Show current certificate

Tap this preference to show detailed information on the current server certificate

### Generate certificate

Tap this preference to open the certificate generator for the server

### Export stored certificate (*.crt)

Tap this preference to export the current server certificate as a "*.crt" file

### Import existing certificate (*.p12)

Tap this preference to import an existing SSL certificate (PKCS12-Format)

## Server settings

### Keep server alive

- If this feature is enabled, the server will keep running in the background when you close the app
- If this feature is disabled, the server will be closed if you are about to close the app  
Note: This feature also allows you to keep tests running in the background (feature needs to be enabled)

> **_Note:_** This feature also allows you to keep tests running in the background with the app closed (feature ["Keep testing alive"](./settings_bluetooth.md) needs to be enabled)

### Offline session cooldown

Tap this preference to set a cooldown for offline connections. These connections will be removed when the time expired to free memory space. Additionally, you can set this value to 0 in order to disable this feature.

### Server URL

Tap this preference to change the api_url parameter that is included in Aruba authentication responses. This will **ONLY** change the parameter in the response, not the actual address of the server.

### Include URL in authentication response

- If this feature is enabled, the [telemetry server URL](#set-server-url) will be included in the Aruba authentication responses
- If this feature is disabled, the URl won't be included in authentication responses

### Send response messages

- If this feature is enabled, the server will send Aruba Southbound messages as a response to incoming telemetry messages
- If this feature is disabled, the server won't send any response message

### Port number

Tap this preference to change the port of the IoT-Server.

## BLEConnect settings

### bleConnect action timeout

Tap this preference to set the timeout of each bleConnect action

> **_Note:_** This feature applies to each action, not to the connection at all. The default connection timeout of the Aruba sensors is 30 seconds.

### bleConnect keep connections alive

Tap this preference to enable or disable the keep-alive feature. This feature will periodically send messages to the remote device in order to prevent the connection from timing out. The messages are sent every 30 seconds to match the current timeout of the Aruba sensors.

## Server security / authentication

### Maximum server sessions

Tap this setting to set the maximum amount of concurrent connections. The lowest possible value is 1 connection. Therefore, additional sessions will be discarded.

### Static access token

Tap this preference to change the static access token of the IoT-Server. This token will be used for authentication. Telemetry messages that contain this token as the access token won't be rejected.

### Authentication username

Tap this preference to change the username of the server authentication. This username will also be used to access protected content of the server (Web-Dashboard, API calls).

### Authentication password

Tap this preference to change the password of the server authentication. This password will also be used to access protected content of the server (Web-Dashboard, API calls). The password is not viewable.

### Reauthentication-timer

Tap this preference to change the duration of the reauthentication timer

- If this feature is enabled, clients have to reauthenticate when the timer expired. The timer also controls the "expiring_in" parameter of the Aruba authentication response messages
- If this feature is disabled, clients won't have to reauthenticate when the timer expired