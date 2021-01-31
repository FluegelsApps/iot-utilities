# IoT-Utilities Dashboard

<img src="./images/docs_dashboard.png" width="100%">
![Dashboard-Screenshot](./images/docs_dashboard.png)

The app dashboard is the main page of the application. You can control the server and it's values via this page.

## 1) Server control panel
This panel displays the current status of the server, as well as some information on it.

### a) Status
<span style="color:red"><b>- Server offline (ready)</b></span>
When the server is offline, the panel will show a red power icon with the title "Server ready. Tap to start". The server is ready to start.

<span style="color:red"><b>- Server offline (not ready)</b></span>
The panel will show a red error icon with the title ("Server not ready. More information"). This indicates that either your certificate is invalid or your device isn't connected to the internet.

<span style="color:green"><b>- Server online</b></span>
The panel will show a green power icon, indicating that the server is running and waiting for clients.

<span style="color:yellow"><b>- Server paused</b></span>
The panel will show a yellow power icon. The server is paused and stops all data analysis processes.

### b) Actions
**- Tapping the button:**
Tap the button to start the server.
Tap the button again to shut the server down.
Tap the button when the server isn't ready to see how to fix this issue.

Tap the button when the server is in it's "paused-state" resumes the data processing of the server.

**- Holding the button:**
Hold the button to pause the server (Server needs to be online). The app will stop processing and analysing the incoming data. Nevertheless, the clients will stay connected.

## 2) Certificate control panel
This panel displays the current status of the server certifiate.

### a) Status
<span style="color:green"><b>- Certificate is valid</b></span>
The panel will show a green icon and the validity of the certificate in days.

<span style="color:yellow"><b>- Certificate is valid (expiring in less than 30 days)</b></span>
The panel will show a yellow icon and the validity of the certificate in days.

<span style="color:orange"><b>- Certificate is valid (expiring in less than 7 days)</b></span>
The panel will show an orange icon and the validity of the certificate in days.

<span style="color:red"><b>- Certificate is invalid</b></span>
The panel will show a red icon, indicating that the certificate already expired.

<span style="color:red"><b>- Certificate is not valid yet</b></span>
The panel will show a red icon, indicating that the certificate isn't valid yet. It also shows the time when the certificate will be valid.

### b) Actions
**- Tapping the button:**
Tap to button to show the certificate details page. This page contains detailed information on the certificate.

**- Holding the button:**
Hold the button to manage the current certificate. You can import or generate a new certificate.
