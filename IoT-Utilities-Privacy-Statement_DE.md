---
layout: default
title: Privacy-Statement (DE)
parent: Legal
---

# IoT-Utilities Datenschutzerklärung ([EN](./IoT-Utilities-Privacy-Statement_EN.md)|**DE**)

Gütig ab dem <!--#validof-->01.03.2021<!--#validof-->

## Datenschutzhinweise für IoT-Utilities App

Der Schutz der Privatsphäre aller Nutzer der App ist uns ein wichtiges Anliegen. Die folgende Datenschutzerklärung beschreibt die Art, den Umfang und den Zweck des Umgangs der „IoT-Utilities" App, nachfolgend kurz mit **"App"** bezeichnet mit personenbezogenen und nicht-personenbezogenen Daten. „Personenbezogene Daten" sind alle Informationen, die sich auf eine identifizierte oder identifizierbare natürliche Person beziehen.

---

### _**1. Wer ist der Anbieter dieser App und für die Verarbeitung Ihrer personenbezogenen Daten verantwortlich?**_

Verantwortlicher für die Datenverarbeitung und Ansprechpartner bei Fragen oder Anregungen zur App ist:  

Jens Flügel  
Vor dem Steintor 4  
38871 Ilsenburg (Harz)  
Deutschland  
E-Mail: [iot-utilities@arubademo.de](mailto:iot-utilities@arubademo.de)

---

### _**2. Was ist der Zweck dieser App?**_

Die App dient zur Demonstration und zum Testen der „Aruba IoT Interface" Funktionalität. Nähere Informationen zu dieser Funktionalität und deren Spezifikation sind hier zu finden:  

Aruba Support Portal  
[https://asp.arubanetworks.com/downloads;search=iot](https://asp.arubanetworks.com/downloads;search=iot)  

ArubaOS WLAN and Aruba Instant 8.6.0.x IoT Interface Guide  
[https://support.hpe.com/hpesc/public/docDisplay?docId=a00100259en\_us](https://support.hpe.com/hpesc/public/docDisplay?docId=a00100259en_us)  

Des Weiteren bietet die App weitere Funktionen und Werkzeuge, wie z.B. „Bluetooth Scanning" und „Bluetooth Advertising".

---

### _**3. Welche Funktionen bietet diese App?**_

#### **IoT-Server**

Die App stellt eine IoT-Server Funktion zur Verfügung, welche Verbindungen von Aruba Controllern und Aruba Instant Access Points über das Aruba IoT Interface Protokoll entgegennimmt. Der IoT-Server erlaubt nur (TLS / SSL) verschlüsselte Verbindungen, welche per statischem Access Token oder Benutzername und Passwort autorisiert bzw. authentifiziert werden. Das hierfür notwendige SSL-Serverzertifikat kann in die App importiert oder ein selbst-signiertes Zertifikat generiert werden. Der IoT-Server stellt zusätzlich ein Web Dashboard über eine (TLS / SSL) verschlüsselte Verbindung unter der URL [https://[Smartphone_IP-Adresse]:[Port]/dashboard](https://[Smartphone_IP-Adresse]:[Port]/dashboard) zur Verfügung. Der Zugriff auf das Dashboard ist über ein in den App Einstellungen zu vergebene Benutzername/Passwort Kombination abgesichert.  

#### **BLE Testing**

Diese Funktion ermöglicht der App, die momentane Konfiguration zu überprüfen, indem Sie iBeacon-Advertisements an Aruba Access Points in der Nähe, mithilfe des Aruba-IoT-Interfaces, sendet. Wenn die Konfiguration funktioniert, dann werden die gesendeten Signale über das Interface zurückgeschickt. Die App zeigt dabei die antwortenden Access Points, sowie die Signalstärke.

#### **BLE Connect**

Diese Funktion ermöglicht der App sich, mithilfe der Aruba Access Points, mit BLE-Geräten zu verbinden. Außerdem kann die App ein sogennantes Pairing bzw. Bonding mit dem Gerät durchführen. Das Schlüsselmaterial, welches während dieses Prozesses verwendet wird, wird sicher in einer verschlüsselten Datenbank gespeichert. Des Weiteren speichert die App die MAC-Adressen der BLE-Geräte und Aruba Access Points.

#### **Bluetooth Scanning**  

Diese Funktion der App zeigt alle Bluetooth Low Energy (BLE) Geräte in der Umgebung des Smartphones in Form einer Liste an, hierfür wird ein Bluetooth fähiges Smartphone benötigt. Nähere Informationen zu den erfassten BLE Geräten werden in einer Details-Ansicht zusammengefasst dargestellt.  

#### **Bluetooth Advertising**  

Mit dieser Funktion arbeitet das Smartphone als Bluetooth Sender. Hierbei können verschiedene Bluetooth Pakete, sogenannte Advertisement, sowohl erstellt als auch gesendet werden. Es stehen unterschiedliche Bluetooth Protokolle, z.B. iBeacon oder Eddystone zur Erstellung von Advertisements zur Verfügung.  

---

### _**4. Was ist der Zweck und die Rechtsgrundlage der Datenverarbeitung (Art. 6 DSGVO)?**_

Die Datenverarbeitung erfolgt für folgende Zwecke und auf folgender Rechtsgrundlage:

- Ausschließlich zur Bereitstellung der App und deren Funktionalitäten im dafür erforderlichen Umfang (Art. 6 Abs. 1 b) DSGVO). Personenbezogene Daten werden grundsätzlich gelöscht, sobald eine weitere Verarbeitung für Zwecke der Vertragsdurchführung jeweils nicht mehr erforderlich ist.

- Soweit eine Einwilligung zur Datenverarbeitung in dem in dieser Datenschutzvereinbarung genannten Umfang gegeben wurde (Art. 6 Abs. 1 a) DSGVO).

Die Einwilligung zur Datenverarbeitung kann beim ersten Start der App gegeben werden. Ohne Einwilligung kann die App nicht genutzt werden. Einwilligungen sind stets freiwillig und können jederzeit frei widerrufen werden. Um die Einwilligung zu wiederrufen muss die App deinstalliert werden bzw. die App Daten gelöscht werden unter:  

Android:  
Einstellungen -> Apps -> IoT-Utilities -> Deinstallieren  

Einstellungen -> Apps -> IoT-Utilities -> Speicher -> Daten löschen  

Ein Widerruf lässt die Rechtmäßigkeit der bis zum Widerruf auf Grundlage der Einwilligung erfolgten Datenverarbeitung unberührt.

---

### _**5. Welche Berechtigungen benötigt diese App?**_

Diese App benötigt Berechtigungen zum Zugriff auf Funktionen und Daten auf dem Smartphone zur Bereitstellung seiner Funktionen, welche bei der Installation der App erteilt werden müssen. Falls diese Berechtigungen nicht erteilt werden stehen bestimmte Funktionen nicht zur Verfügung bzw. kann die App nicht verwendet werden.App Berechtigungen werden je nach Betriebssystem teilweise automatisch erteilt oder müssen bei potenziell gefährlichen Zugriffen z.B. auf sensible Daten wie Positionsdaten vom Benutzer explizit erteilt werden. Insbesondere nutzt die App Daten, die eingeben werden und, sofern diese freigeben werden, Daten, die auf dem Gerät vorhanden sind oder durch Nutzung von Gerätefunktionen generiert werden.

Folgende Berechtigungen werden bei der Installation bzw. beim ersten Start von der App benötigt und angefordert:  

- #### **Standort**  

Android Berechtigungen (Benutzerabfrage):  
[android.permission.access\_coarse\_location]  
[android.permission.access\_fine\_location]  

Diese App benötigt Zugriff auf die Standortfunktion des Gerätes. Diese Berechtigung wird benötigt, um auf die Bluetooth Low Energy (BLE) Schnittstelle des Smartphones zuzugreifen. Hierbei werden keinerlei Standortinformationen durch die App abgerufen oder gespeichert.

- #### **Speicher (Lesen/Schreiben)**

Android Berechtigungen (Benutzerabfrage):  
[android.permission.write\_external\_storage]  
[android.permission.read\_external\_storage]  

Die App benötigt lesenden und schreibenden Zugriff auf den Externen Speicher Ihres Smartphones, um temporäre Dateien für verschiedene Funktionen, sowie Konfigurationsdateien speichern zu können.

- #### **Bluetooth**

Android Berechtigungen (automatisch erteilt):  
[android.hardware.bluetooth\_le]  
[android.permission.bluetooth]  
[android.permission.bluetooth\_admin]  

Diese App benötigt Zugriff auf das Bluetooth-System des Smartphones, um die Funktionen „Bluetooth Scanning"; und „Bluetooth Advertising"; zur Verfügung stellen zu können.

- #### **Internet**

Android Berechtigungen (automatisch erteilt):  
[android.permission.internet]  

Diese App benötigt Zugriff auf die Internetverbindung des Gerätes, um die Funktion „IoT-Server" zur Verfügung stellen zu können und zum Herunterladen der BLE MAC Hersteller Liste aus dem Internet (optional).

- #### **Wi-Fi- und Netzwerkinformationen**

Android Berechtigungen (automatisch erteilt):  
[android.permission.access\_wifi\_state]  
[android.permission.access\_network\_state]  

Diese App benötigt Zugriff auf die Netzwerkinformationen des Smartphones, um die Funktion „IoT-Server" zur Verfügung stellen zu können.

- #### **Vordergrunddienste**

Android Berechtigungen (automatisch erteilt):  
[android.permission.foreground_service]

Diese App benötigt Zugriff auf sogenannte "Vordergrunddienste" um die Funktionen "IoT-Server", "BLE Advertising" und "BLE Testing" im Hintergrund ausführen zu können. Dieses Feature is optional und kann jederzeit in den Einstellungen der App aktiviert / deaktiviert werden.

Die erteilten Berechtigungen können jederzeit in der App unter Einstellungen -> Berechtigungen oder in den Geräteeinstellungen eingesehen/erteilt/entzogen werden:  

Android:  
Einstellungen -> Apps -> IoT-Utilities -> Berechtigungen  

---

### _**6. Wann und wie werden Benachrichtigungen verwendet?**_

Die App informiert mit Benachrichtigungen über den Status der „Bluetooth Advertising" und „IoT-Server" Funktionen.  

Die Benachrichtigungen können jederzeit unter:  

Android:  
Einstellungen -> Apps -> IoT-Utilities -> Benachrichtigungen  

deaktiviert und auch wieder aktiviert werden.

---

### _**7. Welche Daten werden durch die App erhoben, verarbeitet und gespeichert und zu welchem Zweck?**_

Beim Herunterladen einer App werden erforderliche Informationen an den jeweiligen App Store übertragen, also insbesondere Nutzername, E-Mail-Adresse, Kundennummer beim App Store und die individuelle Gerätekennung. Auf diese Datenverarbeitung haben wir keinen Einfluss. Verantwortlich hierfür ist der Betreiber des jeweiligen App Stores.
Link zur Datenschutzrichtlinie der von der App verwendeten App Stores:

- [Google Play Services](https://www.google.com/policies/privacy/)

Die App selbst verzichtet auf die Verwendung personenbezogener Daten (Privacy by Design), es sei denn diese sind für die Funktion der App unerlässlich.  

Die App speichert keinerlei Daten permanent, weder personenbezogen noch nicht-personenbezogen.  

Folgende Daten werden durch die App erfasst und verarbeitet:

#### **Personenbezogene Daten (Benutzer)**

_IP-Adresse_

Für die Bereitstellung der „IoT-Server" Funktion fragt die App die aktuelle IP-Adresse des Smartphones ab und verwendet diese als Server IP-Adresse. Die IP-Adresse wird außerdem dynamisch in Konfigurationsvorlagen eingefügt, wenn diese durch den Benutzer in der App abgerufen und angezeigt werden. Diese Konfigurationsvorlagen sind eine Hilfestellung für die Konfiguration der Aruba Wi-Fi Komponenten, um Daten über die Aruba IoT Schnittstelle an die „IoT-Server" Funktion der App zu senden.Zusätzlich wird die IP-Adresse in den Log Daten der App zur Fehlersuche und -analyse verwendet.  
Die IP-Adresse wird nur so lange verwendet, wie die App genutzt wird und nicht permanent gespeichert. Die Log Daten werden gelöscht, sobald die App geschlossen wird.Wird die IP-Adresse durch den Benutzer aus der App kopiert und weiterverwendet, z.B. bei der Verwendung der Konfigurationsvorlagen, so liegt dieses außerhalb des Verantwortungsbereiches dieser App und der Benutzer hat für den Schutz der Daten selbst Sorge zu tragen.

#### **Personenbezogene Daten (Dritter)**

##### _IP-Adresse_

Die „IoT-Server" Funktion der App stellt für den Verbindungsaufbau von Aruba Controllern und Aruba Instant Access Points über das Aruba IoT Interface Protokoll, sowie für ein eigenes Web-Dashboard einen Web-Server zur Verfügung. Beim Verbindungsaufbau zum Web-Server der App werden die Verbindungsinformationen inkl. der IP-Adresse des Clients erfasst. Die IP-Adresse wird nur so lange erfasst, wie die App genutzt wird und nicht permanent gespeichert. Die Log Daten des Web-Servers werden gelöscht, sobald die App geschlossen wird.

##### _BLE MAC Adressen_

Die „Bluetooth Scanner" Funktion der App erfasst und zeigt alle Bluetooth Low Energy (BLE) Geräte in der Umgebung des Smartphones an, inkl. der BLE MAC Adresse der jeweiligen Geräte. Die erfassten Daten werden nur in der App auf dem lokalen Gerät angezeigt, solange dieses verwendet wird. Mit dem Schliessen den der App werden alle empfangenen Daten gelöscht. Es werden keinerlei Daten gespeichert.

##### _Aruba IoT Telemetrie Daten_

Die „IoT-Server" Funktion der App ermöglicht es Daten von Aruba Geräten Dritter über die Aruba IoT Schnittstelle zu empfangen und darzustellen, wobei es sich hierbei auch um personenbezogene Daten handeln kann, insbesondere um:

- MAC Adressen von Bluetooth Geräten
- MAC Adressen von WLAN Geräten
- MAC Adressen von ZigBee Geräten

Verantwortlicher (Controller) für die Datenverarbeitung der durch die Aruba IoT Schnittstelle an die App übertragenen Daten ist der Besitzer des Drittsystems.Der Nutzer der App verarbeitet die Daten gemäß Art. 28 DSGVO als Auftragsverarbeiter (Processor).  

Die Sicherheit der über die Aruba IoT Schnittstelle übertragenen Daten wird durch eine (TLS / SSL) verschlüsselte Verbindung zwischen der App und den Drittsystemen sichergestellt.  

Die durch die „IoT-Server" Funktion der App empfangenen Daten werden nur in der App auf dem lokalen Gerät angezeigt, solange diese verwendet wird. Mit dem Schliessen der App werden alle empfangenen Daten gelöscht. Es werden keinerlei Daten gespeichert.

#### **Nicht-personenbezogene Daten**

Durch die App erzeugte Log Daten werden zur Fehlersuche und -analyse verwendet und nur auf dem lokalen Gerät angezeigt, so lange die App verwendet wird. Mit dem Beenden der App werden alle Log Daten gelöscht. Es werden keinerlei Daten permanent gespeichert.

---

### _**8. Welche Daten werden auf dem Endgerät gespeichert?**_

Die App speichert folgende Daten auf dem Endgerät zur Erfüllung Ihrer Funktion:  

- Liste der Bluetooth Hersteller ID's
- Konfigurationsvorlagen
- Exportiert Zertifikate
- Exportiert Log Dateien
- Temporäre Dateien
- Bluetooth Advertiser Datenbank

---

### _**9. Wie lange werden die Daten gespeichert?**_

Alle personenbezogenen Daten, welche diese App zur Laufzeit verwendet, werden gelöscht, sobald die App vom Nutzer geschlossen wird. Es werden keine personenbezogenen Daten permanent gespeichert.  

Daten, die im Speicher des Smartphones abgelegt werden, z.B. Konfigurationsdateien werden gespeichert, bis die App deinstalliert wird oder die Dateien manuell gelöscht werden.

---

### _**10. Wie können Daten des Nutzers in der App gelöscht werden?**_

Die Daten werden mit der Deinstallation der App gelöscht oder können jederzeit manuell gelöscht werden unter:  

Android:  
Einstellungen -> Apps -> IoT-Utilities -> Speicher -> Daten löschen.

---

### _**11. Werden Daten an Dritte weitergegeben?**_

Die Datenverarbeitung der App erfolgt ausschließlich lokal auf dem installierten Gerät und nur so lange die App verwendet wird bzw. im Hintergrund läuft. Die App speichert oder überträgt keine personenbezogenen oder anderen Daten an HPE, den Entwickler oder Dritte. Diese App verwendet außerdem keine Analyse- oder Werbedienste von Google oder anderen Anbietern.

---

### _**12. Wird das Nutzungsverhalten/die Daten der Nutzer durch Tracking-Tools ausgewertet?**_

Weder das Nutzungsverhalten noch die Daten des Nutzers werden durch Tracking-Tools oder Ähnliches verarbeitet oder analysiert. Ihre personenbezogenen Daten werden nicht für automatisierte Einzelfallentscheidungen einschließlich Profiling im Sinne des Art. 22 Abs. 1 DSGVO und Art. 4 DSGVO verarbeitet.

---

### _**13. Welche Rechte habe ich? (Rechte der betroffenen Person, DSGVO)**_

Haben Sie in die Verarbeitung Ihrer personenbezogenen Daten eingewilligt, haben Sie das Recht, die Einwilligung jederzeit mit Wirkung für die Zukunft zu widerrufen. Die Rechtmäßigkeit der Verarbeitung Ihrer personenbezogenen Daten bis zu einem Widerruf wird durch den Widerruf nicht berührt.  

Als von der Datenverarbeitung betroffene Person haben Sie nachdem anwendbaren Datenschutzrecht ggf. das Recht auf:  

- #### Recht auf Auskunft (Art. 15 DSGVO)

Sie haben das Recht Auskunft über die von Ihnen gespeicherten personenbezogenen Daten zu erhalten. Dies bedeutet, dass Sie das Recht haben, eine Bestätigung verlangen zu können, ob Sie betreffende personenbezogene Daten verarbeitet werden oder nicht, und wenn dies der Fall ist, ein Recht auf Auskunft über diese personenbezogenen Daten. Das Recht auf Auskunft umfasst, unter anderem, die Verarbeitungszwecke, die Kategorien personenbezogener Daten, die verarbeitet werden und die Empfänger oder Kategorien von Empfängern, gegenüber denen die personenbezogenen Daten offengelegt wurden oder werden. Dieses Recht besteht allerdings nicht uneingeschränkt, denn die Rechte anderer Personen können Ihr Recht auf Auskunft beschränken. Sie haben gegebenenfalls das Recht, eine Kopie der personenbezogenen Daten, die verarbeitet werden, zu erhalten.  

- #### Recht auf Berichtigung (Art. 16 DSGVO)

Sie haben das Recht, unrichtige Daten berichtigen zu lassen. Dies bedeutet, dass Sie von uns die Berichtigung unrichtiger, Sie betreffender personenbezogener Daten verlangen können. Unter Berücksichtigung der Zwecke der Verarbeitung haben Sie das Recht, die Vervollständigung unvollständiger personenbezogener Daten, auch mittels einer ergänzenden Erklärung, zu verlangen.  

- #### Recht auf Löschung ("Recht auf Vergessenwerden") (Art. 17 DSGVO)

Unter bestimmten Voraussetzungen können Sie die Löschung Ihrer gespeicherten personenbezogenen Daten verlangen und es besteht die Verpflichtung zur Löschung der personenbezogenen Daten, soweit deren Verarbeitung nicht zur Ausübung des Rechts auf freie Meinungsäußerung und Information, zur Erfüllung einer rechtlichen Verpflichtung, aus Gründen des öffentlichen Interesses oder zur Geltendmachung, Ausübung oder Verteidigung von Rechtsansprüchen erforderlich ist.  

- #### Recht auf Einschränkung der Verarbeitung (Art. 18 DSGVO)

Sie können die Einschränkung der Verarbeitung Ihrer personenbezogenen Daten verlangen, soweit die Richtigkeit der Daten von Ihnen bestritten wird, die Verarbeitung unrechtmäßig ist, Sie aber deren Löschung ablehnen. Außerdem steht Ihnen dieses Recht zu, wenn wir die Daten nicht mehr benötigen, Sie diese jedoch zur Geltendmachung, Ausübung oder Verteidigung von Rechtsansprüchen benötigen. Darüber hinaus haben Sie dieses Recht, wenn Sie Widerspruch gegen die Verarbeitung Ihrer personenbezogenen Daten eingelegt haben.  

- #### Recht auf Datenübertragbarkeit gemäß Art. 20 DSGVO

Sie können verlangen, dass Ihre personenbezogenen Daten, die Sie uns bereitgestellt haben, in einem strukturierten, gängigen und maschinenlesebaren Format übermitteln. Alternativ können Sie die direkte Übermittlung der von Ihnen uns bereitgestellten personenbezogenen Daten an einen anderen Verantwortlichen verlangen, soweit dies möglich ist.  

- #### Recht auf Wiederspruch (Art. 21 DSGVO)

Von Ihnen erteilte Einwilligungen können Sie jederzeit uns gegenüber widerrufen. Die Datenverarbeitung, die auf der widerrufenen Einwilligung beruht, darf dann für die Zukunft nicht mehr fortgeführt werden.  

- #### Beschwerderecht bei einer Aufsichtsbehörde (Art. 77 Abs. 1 DSGVO)

Sie können sich bei der für uns zuständigen Aufsichtsbehörde beschweren, z.B. wenn Sie der Ansicht sind, dass wir Ihre personenbezogenen Daten in unrechtmäßiger Weise verarbeiten.

---

### _**14. Änderung der Datenschutzerklärung**_

Diese Datenschutzerklärung entspricht dem Stand zum Zeitpunkt der jeweils installierten aktuellen Version der App. Sollten sich Änderungen bei der Erhebung, Verarbeitung oder Nutzung von Daten durch neue oder geänderte Funktionen der App ergeben, so wird beim Update der App darauf hingewiesen und eine erneute Einverständniserklärung abgefragt. Die aktuelle Fassung der Datenschutzerklärung ist in der App abrufbar unter:  

About -> Privacy Statement
