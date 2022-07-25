# Einleitung

Dies ist ein Fork von https://github.com/greenMikeEU/SmartMeterEVNKaifaMA309 mit folgenden Änderungen:

* Home-Assistant MQTT-Auto-Discovery (Die Sensoren Momentanleistung, sowie beide Zähler tauchen automatisch in Home-Assistant ohne Konfiguration auf, wenn MQTT schon eingerichtet ist)
* Integrierter Datenupload nach InfluxDB (alle Werte in einem Paket)
* Konfiguration über `.env` Datei ohne editieren des Codes
* systemd Beispieldatei enthalten (inkl. Autorestart bei Verbindungsfehlern)


# SmartMeterEVN
Dieses Projekt ermöglicht es den Smartmeter der EVN (Netz Niederösterreich) über die Kundenschnittstelle auszulesen.
Smart Meter werden von der Netz NÖ GmbH eingebaut, auf Basis der gesetzlichen Forderungen.

## Getting Started
### Voraussetzungen Hardware


* Passwort für die Kundenschnittstelle
  * Alle folgenden Informationen sind aus dem Folder der EVN. (https://www.netz-noe.at/Download-(1)/Smart-Meter/218_9_SmartMeter_Kundenschnittstelle_lektoriert_14.aspx)
  * Wenn bereits ein Smart Meter in der Kundenanlage eingebaut ist, kann hier das der Schlüssel angefordert werden: smartmeter@netz-noe.at
    * Kundennummer oder Vertragskontonummer
    * Zählernummer
    * Handynummer

### Zähler Hersteller
* Kaifa Drehstromzähler MA309


### Installation 

```
cd ~pi
git clone https://github.com/nebman/SmartMeterEVNKaifaMA309
```

### Berechtigung pi Benutzer für die serielle Schnittstelle
```
sudo adduser pi dialout
```

### Python + Pakete

```
sudo apt install python3 idle3 python3-pip
sudo pip3 install -U gurux-dlms beautifulsoup4 paho-mqtt lxml pyserial cryptography influxdb
```

### Konfigurationsdatei

```
cd SmartMeterEVNKaifaMA309
cp .env-sample .env
nano .env
```

### Installation systemd-service:
```
sudo cp smartmeter.service /etc/systemd/system/
sudo systemctl daemon-reload
sudo systemctl start smartmeter.service
```
Logs abrufbar über `journalctl -xe -u smartmeter.service `



## License

This project is licensed under the GNU General Public License v3.0 License - see the LICENSE.md file for details