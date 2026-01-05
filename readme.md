\# 🔑 N-Software Wiegand-Gateway \& Zutrittskontrolle

\*\*Eine professionelle Komplettlösung für ESP32-C3 \& Home Assistant\*\*



Dieses Projekt verbindet ein robustes ESPHome-Gateway mit einer hochflexiblen Blueprint-Steuerung für Home Assistant. Es ist darauf optimiert, RFID-Chips und PIN-Codes sicher zu verarbeiten und direkt in Smart-Home-Aktionen umzusetzen.



\## 🌟 Highlights \& Features

\* \*\*Plug-and-Play Anlernen:\*\* Über ein spezielles "Labor-Feld" (04. Letzter Scan) im Web-Interface des Gateways können RFID-Rohdaten direkt per Copy \& Paste übernommen werden.

\* \*\*Flexibler Montageort:\*\* Der Installationsort lässt sich ohne Programmierung im Web-Interface ändern; das Gateway passt seine MQTT-Topics automatisch an.

\* \*\*Sicherheits-Logik:\*\* Volle Integration mit \*\*Alarmo\*\* – bei scharfer Alarmanlage bleibt der Zutritt verweigert.

\* \*\*Messaging:\*\* Unterstützung für WhatsApp-Benachrichtigungen und Handy-Push.

\* \*\*Ereignis-Logbuch:\*\* Speichert die letzten 5 Ereignisse (Zutritt gewährt/verweigert) übersichtlich in einem Text-Helfer.

\* \*\*Zeitsteuerung:\*\* Definierbare Zeitfenster und Wochentage pro Benutzer.



\## 🛠 Hardware

\* \*\*Controller:\*\* ESP32-C3

\* \*\*Leser:\*\* Standard Wiegand RFID/Keypad Leser

\* \*\*Verkabelung:\*\*

&nbsp;   \* D0 -> GPIO5

&nbsp;   \* D1 -> GPIO6

&nbsp;   \* LED/Buzzer -> GPIO2 (Inverted)



\## 🚀 Installation \& Einrichtung



\### 1. ESPHome Firmware

Lade die Datei `wiegand\_gateway.yaml` herunter und flashe sie auf deinen ESP32-C3. Stelle sicher, dass du deine WLAN- und MQTT-Zugangsdaten in deiner `secrets.yaml` hinterlegt hast.



\### 2. Montageort festlegen

Öffne nach dem ersten Start das Web-Interface des Gateways (IP-Adresse im Browser). Gib unter "01. Montageort ändern" deinen Standort ein (z.B. `Garage`). Das Gerät startet neu und ist nun unter dem entsprechenden MQTT-Pfad erreichbar.



\### 3. Home Assistant Sensor

Erstelle in deiner `configuration.yaml` einen MQTT-Sensor, damit Home Assistant die Daten verarbeiten kann:

```yaml

mqtt:

&nbsp; sensor:

&nbsp;   - name: "Wiegand Scanner"

&nbsp;     state\_topic: "wiegand/DEIN\_ORT/event"

&nbsp;     value\_template: "{{ value\_json.value }}"

