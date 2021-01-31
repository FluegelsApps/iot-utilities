# IoT-Utilities Dashboard

<img src="./images/docs_dashboard.png" width="100%">

The app dashboard is the main page in the application. You can control the server and it's values via this page.

## 1) Server control panel
This panel displays the current status of the server, as well as some information on it. You can also change the state of the server using this button.

### a) Status
- Server offline (ready)
When the server is offline, the panel will show a red power icon with the title "Server ready. Tap to start". The server is ready to start.

- Server offline (not ready)
The panel will show a red error icon with the title ("Server not ready. More information"). This indicates that either your certificate is invalid or your device isn't connected to the internet.

- Server online
The panel will show a green power icon, indicating that the server is running and waiting for clients.

- Server paused
The panel will show a yellow power icon. The server is paused and stops all data analysis processes.

### b) Actions
- Tapping the button:
Tap the button to start the server.
Tap the button again to shut the server down.
Tap the button when the server isn't ready to see how to fix this issue.

Tap the button when the server is in it's "paused-state" resumes the data processing of the server.

- Holding the button:
Hold the button to pause the server (Server needs to be online). The app will stop processing and analysing the incoming data. Nevertheless, the clients will stay connected.

## 2) Certificate control panel
