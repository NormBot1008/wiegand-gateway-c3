Hinweis: Die Commit-Nachricht v2.1.6 ist veraltet; das Repository enthält bereits die stabile Version v2.5.3. Diese Version bietet volle Unterstützung für automatische MQTT-Deregistrierung und erweiterten System-Status.




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


\### 4. Log-Helfer (Optional)
hier ist noch ein kleiner Bug drin der ist nicht Optional, bitte eine Datei anlegen dazu oder eine Selektieren dann sollte sich das speichern lassen

### 🔐 Sicherheitshinweis: Web-Interface schützen
Standardmäßig ist das Web-Interface des Gateways ohne Passwort erreichbar, um die Ersteinrichtung zu erleichtern. Für den produktiven Einsatz empfehle ich dringend, einen Passwortschutz zu aktivieren.

Im bereitgestellten ESPHome-Code findest du im Bereich `web_server:` vorbereitete Zeilen für `auth`. Entferne einfach die Kommentarzeichen (`#`) und setze dein eigenes Passwort:

```yaml
web_server:
  port: 80
  auth:
    username: admin
    password: DEIN_SICHERES_PASSWORT


# Beispiel für die configuration.yaml
mqtt:
  sensor:
    - name: "Wiegand Scanner"
      state_topic: "wiegand/DEIN_ORT/event"
      value_template: "{{ value_json.value }}"
      # WICHTIG: Verhindert, dass jeder Scan das HA-Logbuch füllt
      # Das Blueprint übernimmt das saubere Logging selbst!

