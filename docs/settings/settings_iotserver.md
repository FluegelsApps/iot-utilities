# IoT-Server settings

## Server certificate

### Show current certificate

Tap this setting to show detailed information on the current server certificate

### Generate certificate

Tap this setting to open the certificate generator for the server

### Export stored certificate (*.crt)

Tap this setting to export the current server certificate as a "*.crt" file

### Import existing certificate (*.p12)

Tap this setting to import an existing SSL certificate (PKCS12-Format)

## Server settings

### Keep server alive

- If this setting is enabled, the server will keep running in the background when you close the app
- If this setting is disabled, the server will be closed if you are about to close the app  
Note: This setting also allows you to keep tests running in the background (feature needs to be enabled)

> **_Note:_** This feature also allows you to keep tests running in the background with the app closed (feature ["Keep testing alive"](./settings_bluetooth.md) needs to be enabled)

### Set server URL

Tap this setting to change the api_url parameter that is included in Aruba authentication responses. This will **ONLY** change the parameter in the response, not the actual address of the server.

### Include URL in authentication response

- If this setting is enabled, the [telemetry server URL](#set-server-url) will be included in the Aruba authentication responses
- If this setting is disabled, the URl won't be included in authentication responses

### Send response messages

- If this setting is enabled, the server will send Aruba Southbound messages as a response to incoming telemetry messages
- If this setting is disabled, the server won't send any response message

### Set port number

Tap this setting to change the port of the IoT-Server.

## Server security / authentication

### Static access token

Tap this setting to change the static access token of the IoT-Server. This token will be used for authentication. Telemetry messages that contain this token as the access token won't be rejected.

### Authentication username

Tap this setting to change the username of the server authentication. This username will also be used to access protected content of the server (Web-Dashboard, API calls).

### Authentication password

Tap this setting to change the password of the server authentication. This password will also be used to access protected content of the server (Web-Dashboard, API calls). The password is not viewable.

### Use reauthentication-timer

- If this setting is enabled, clients have to reauthenticate when the timer expired. The timer also controls the "expiring_in" parameter of the Aruba authentication response messages
- If this setting is disabled, clients won't have to reauthenticate when the timer expired

### Set reauthentication-timer

Tap this setting to change the duration of the [reauthentication timer](#use-reauthentication-timer)
