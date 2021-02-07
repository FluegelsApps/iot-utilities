
# IoT Server Setup

In this step the IoT server is setup for first time use.

## Server certificate

The wizard automatically generates a self-signed certificate that is used by the IoT server for the _Aruba IoT Interface_ WebSocket Secure (wss:) connections as well as connections to the web dashboard using HTTPS.  

The server certificate can be re-generated or a custom PKCS #12 certificate can be imported via the app settings or the app dashboard.  

The server certificate can be exported as .crt file via the app settings or downloaded in the web dashboard.  

---

**Note:** The IoT server certificate has to be imported as trusted certificate authority into the connecting Aruba infrastructure, otherwise the Aruba device will not establish a connection to the app.

---

## Authentication and authorization

 IoT connections to the IoT server are either authorized using a **static access token** or authenticated using a **username/password**.

### Static access token

The wizard generates a static access token that can be changed at any time in the app settings. The app uses JSON web tokes as static access tokes.

The static token can be vied and copied via the server settings icon on the app dashboard.

### IoT interface & web dashboard user account

In order to secure access to the app's web dashboard and to authenticate IoT connections to the IoT server using username/password a local user account is required.

Please set up the user account by entering a username and password above.  

---

**Note:** The password will be saved in a hashed format and is not viewable after the initial configuration. Please take a note of your password in a secure place.  

---

The user name and password can be changed at any time in the app settings.
