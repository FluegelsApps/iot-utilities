---
layout: default
title: Blyott (ArubaOS/Aruba Instant 8.8.x.x or higher)
has_children: false
parent: BLE Telemetry Solutions
grand_parent: Aruba IoT Config Examples
nav_order: 1
---

# Blyott (ArubaOS/Aruba Instant 8.8.x.x or higher)

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

This example shows the required configuration to enable the [Blyott location based and monitoring solution](https://blyott.com/) integration using ArubaOS/Aruba Instant version 8.8.x.x or higher.

-   `fqdn, ip-address, port, path` - has to be replaced with the FQDN or IP address, optional port and path of the remote server
-   `access-token` - has to be replaced with the static access token used to connect to the remote server
-   `client-id` - (optional) has to be replaced with the client identifier string that is used by the remote server to identify the connecting Aruba infrastructure, e.g. "Aruba-Wi-Fi".
-   `ap-group` - has to be replaced with the AP group name the configuration should be enabled on (multiple statements are required for multiple groups) (ArubaOS only)

>***Note:***  
>The [Let’s Encrypt certificate chain of trust](https://letsencrypt.org/certificates/) has to be installed on the Aruba infrastructure for the secure HTTP or secure websocket connection to the Blyott backend. The Blyott server URL currently use a server certificate issued by the [Let’s Encrypt R3 intermediate CA](https://letsencrypt.org/certs/lets-encrypt-r3.pem), which is signed by the [Let's Encrypt ISRG Root X1 certificate authority](https://letsencrypt.org/certs/isrgrootx1.pem). The complete certificate chain have to be installed.
Please see the [Aruba CLI Reference - Importing Certificates](../references/aruba_reference_documentation.md#aruba-cli-reference---importing-certificates) for details.

## ArubaOS

### CLI Configuration

```
iot radio-profile "ble-int"
    radio-mode none ble
!
ap-group <ap-group>
    iot radio-profile "ble-int"
!
iot transportProfile "blyott"
    serverType Telemetry-Websocket
    serverURL "wss://mobileproxy.blyott.com/aruba"
    clientId "Aruba-WiFi"
    accessToken <access-token>
    deviceClassFilter blyott
    reportingInterval 60
    ageFilter 30
    rssiReporting last
    include-ap-group <ap-group>
!
iot useTransportProfile "blyott"
```

### GUI Configuration

t.b.d.

## Aruba Instant

### CLI Configuration

```
iot radio-profile "ble-int"
 radio-mode ble
 exit

iot use-radio-profile "ble-int"

iot transportProfile "blyott"
 endpointType telemetry-websocket
 endpointURL "wss://mobileproxy.blyott.com/aruba"
 endpointID "Aruba-WiFi"
 endpointToken <access-token>
 payloadContent blyott
 transportInterval 60
 ageFilter 30
 rssiReporting last

 exit

iot useTransportProfile "blyott"
```

### GUI Configuration

>***Note:***  
>The example screenshots provided below show the Aruba Instant version 8.9 GUI. Even if, the Aruba Instant version 8.8 shows has a slightly different look and feel the same shown configuration settings still apply.

1. Login to the Aruba Instant access point web interface.  
2. In the menu on the left side go to ***Configuration > Services*** and open the sub menu ***IoT*** in the main window.  
   ![Aruba Instant IoT Configuration Menu](../../../images/aruba_iot_iap_configuraiton_menu.jpg)

3. Add a new iot radio configuration or change an existing one to enable the BLE mode of the Aruba AP's IoT radio:  
   1. Click on the ***+*** icon in the **IoT radio** sub menu to add a new iot radio profile.  
   2. Enter a profile **name**.
   3. Set the **state** switch to ***enabled***.
   4. Select the desired **radio**.
   5. Set the **radio mode** to ***BLE***.
   6. Set the **BLE operational mode** to ***both***.
   7. Set the AP's BLE **console** mode to the desired state.  
   8. Set the **tx power** to desired value, default is ***0***.  
   This setting is only relevant when using BLE advertisments sent by the AP .  

      ![IAP IoT radio profile confguration BLE](../../../images/aruba_iot_iap_configuraiton_add_iot_radio_profile_ble.jpg)  
    9.  Click **OK** to close the iot radio profile dialog.  
   
4.  Add a new iot transport profile to configure the connectivity tot he Blyott solution backend:
    1.  Click on the **+** icon in the **IoT transports** sub menu to add a new iot transport profile.
    2. Enter a profile **name**.
    3. Set the **State** switch to ***enabled***.
    4. Set **server type** to ***Telemetry Websocket***.
    5. Enter ```wss://mobileproxy.blyott.com/aruba``` as **server URL**.  
    ![IAP IoT transport profile configuration Blyott](../../../images/aruba_iot_iap_configuraiton_add_iot_transport_profile_server_blyott.jpg)
    6. In the **destination** section, select ***token*** as **authentication method**.
    7. Enter the **access token** provided for your Blyott account.
    8. *(optional)* enter a **client id**.
    9. *(optional)* enter then desired **VLAN ID** that should be used for the server communication. Leave empty if the APs management VLAN is used.
    10. (optional) enter **proxy server** information as required.
    ![IAP IoT transport profile configuration Blyott server settings](../../../images/aruba_iot_iap_configuraiton_add_iot_transport_profile_server_auth_blyott.jpg)  
    11. Select **BLE telemetry** as transport service.
        > **Note:** The Transport service **BLE telemetry** is enabled by default and cannot be disabled.
    12. Select ***Blyott*** under **BLE devices** for the transport service **BLE telemetry**.
        > **Note:** The BLE device class ***Blyott*** is supported with Aruba Instant version 8.8 or higher.
    13. Set the **reporting interval** to ```60 seconds```.
    ![IAP IoT transport profile configuration service Blyott](../../../images/aruba_iot_iap_configuraiton_add_iot_transport_profile_services_blyott.jpg)  
    14. In the **Filters** section under **Advanced** enable the **Report devices that have had activity in the last** filter and set it to ```30s```.
    15.  Set the **RSSI reporting format** to ***Last***.
    ![IAP IoT transport profile configuration filter Blyott](../../../images/aruba_iot_iap_configuraiton_add_iot_transport_profile_filters_blyott.jpg)
    16. Click **OK** to close the iot transport profile dialog.
5. Click on **Save** to save and activate the configured settings.
![IAP IoT configuration Blyott finish](../../../images/aruba_iot_iap_configuraiton_add_iot_blyott.jpg)

### Configuration verification

To verify if the applied configuration if working properly connect to the Aruba Instant access point using the SSH or the local console.

1. Check if Blyott BLE devices are seen by the APs BLE radio using the command **show ap debug ble-table generic**:

    ```
    ArubaInstantAP# show ap debug ble-table generic


    BLE Device Table [Generic]
    ---------------------------
    MAC                Address Type  RSSI  Last Update  Device Class  Generic Filter  BT-SIG Company IDs
    ---                ------------  ----  -----------  ------------  --------------  ------------------
    60:c0:bf:61:0e:bf  Public        -56   I:3s         blyott        --              0x09CD

    Generic BLE devices:1
    Total BLE devices:1

    Note: Battery level for LS-BT1USB devices is indicated as USB.
    Note: Uptime is shown as Days hour:minute:second.
    Note: Last Update is time in seconds since last heard update.
    Note: Meas. Pow. is the averaged RSSI (in dBm) when the iBeacon is calibrated.
    Note: Tx_Power is shown in dBm in the APBs section for radios that support radio profile type 1. For all other APB radios, Tx_Power is a discrete level from 0-15.
    Status Flags:L:AP's local beacon; I:iBeacon; A:Beacon management capable
                :H:High power beacon; T:Asset Tag Beacon; U:Upgrade of firmware pending
                :u:Beacon management update received
    Generic Filter:S:serviceUUIDFilter; C:companyIdentifierFilter
                :M:macOuiFilter; L:localNameFilter
    ```
    If no Blyott devices show up in the APs BLE table, check the following things:

    -   Are Blyott BLE devices in the range of the AP?
    -  Are the Blott devices switched on?
    -  Has the APs IoT radio been enabled with the settings shown in the configuration section?
    -  Has the device class ***Blyott*** selected in the IoT transport configuration as shown in the configuration section?

2.  Check if the IoT transport connection to the Blyott cloud backed has been established using the commands:  

    **show ap debug ble-relay iot-profile**  
    **show ap debug ble-relay report**

    ```
    ArubaInstantAP# show ap debug ble-relay iot-profile

    ConfigID                                : 57

    ---------------------------Profile[blyott]---------------------------

    serverURL                               : wss://mobileproxy.blyott.com/aruba
    serverType                              : Telemetry Websocket
    deviceClassFilter                       : Blyott
    reportingInterval                       : 60 second
    authentication-mode                     : none
    ageFilter                               : 30 second
    accessToken                             : Bly0ttBL3
    clientID                                : Aruba-WiFi
    rssiReporting                           : Last
    environmentType                         : office
    Server Connection State
    --------------------------
    TransportContext                        : Connection Established
    Last Data Update                        : 2021-10-16 22:58:16
    Last Send Time                          : 2021-10-16 22:58:49
    TransType                               : Websocket
    ap505h# show ap debug ble-relay report


    ---------------------------Profile[blyott]---------------------------

    WebSocket Connect Status                : Connection Established
    WebSocket Connection Established        : Yes
    Location Id                             : Not Configured
    Websocket Address                       : wss://mobileproxy.blyott.com/aruba
    WebSocket Host                          : mobileproxy.blyott.com
    WebSocket Path                          : aruba
    Vlan Interface                          : Not Configured
    Current WebSocket Started at            : 2021-10-16 21:25:11
    Previous WebSocket Terminated at        : 2021-10-16 21:25:03
    Web Proxy                               : NA
    Proxy Username&password                 : NA, NA
    Last Send Time                          : 2021-10-16 22:58:52
    Websocket Write Stats                   : 139 (21556B)
    Websocket Write WM                      : 0B (0)
    Websocket Read Stats                    : 0 (0B)
    ```
    If the websocket connection status show a different status than ***Connection Established*** uns the following command to check possible connection issues:
    **show ap debug ble-relay ws-log \<profile>**
    
    Common causes of connection errors:
    -   Trusted certificate chain for remote IoT server certificate not installed. Only applicable for secure connections (https://, wss://)
    -   Wrong authentication credentials for the remote IoT server connection (access token, username/password, clientid/secret)
    -   Domain name resolution not configured or not working e.g. DNS server not reachable
    -   Connection blocked firewall or other devices in the communication path  

    >Note: Starting with Aruba Instant 8.8 IoT server connections are automatically established even if no messages need to be send to the remote server e.g. because no BLE devices are seen by the Aruba AP. 

## Aruba Central (2.5.4 or higher)

### Aruba Instant 8.x Configuration

t.b.d.

### AOS10/IoT-Operations (beta)

t.b.d.