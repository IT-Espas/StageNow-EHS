# StageNow-EHS

Dieses Repository enthält die Dateien und Konfigurationen für den Betrieb von **Zebra Enterprise Home Screen (EHS)** auf verwalteten Zebra-Geräten.

Ziel ist eine standardisierte Benutzeroberfläche, bei der den Anwendern nur die benötigten Anwendungen angezeigt werden. Gleichzeitig bleiben administrativ notwendige Systemkomponenten verfügbar.

---

## Zweck

Enterprise Home Screen ersetzt den normalen Android-Launcher auf den Zebra-Geräten.

Damit können:

- nur freigegebene Apps angezeigt werden
- Android-Systemeinstellungen eingeschränkt werden
- Recent Apps deaktiviert werden
- USB-Debugging deaktiviert werden
- ein eigenes Hintergrundbild verwendet werden
- der Zugriff auf den Adminbereich per Passwort geschützt werden
- Geräte über StageNow reproduzierbar konfiguriert werden

EHS dient damit als kontrollierte Benutzeroberfläche für produktiv eingesetzte Zebra-Handhelds.

---

## Unterstützte Geräte / Versionen

Aktuell werden folgende Varianten verwendet:

| Android / MX | EHS-Version | Paketname |
|---|---|---|
| Android 10 / MX10.4 | EHS 4.2 | `com.symbol.enterprisehomescreen` |
| Android 11 / MX11.3 | EHS 4.2 | `com.symbol.enterprisehomescreen` |
| Android 13 / MX13.3 | EHS 7.1.x | `com.zebra.mdna.enterprisehomescreen` |
| Android 14 | EHS 7.1.12 | `com.zebra.mdna.enterprisehomescreen` |

Die eingesetzte EHS-Version muss zur Android-/MX-Version des Gerätes passen.

---

## Repository-Struktur

```text
StageNow-EHS/
│
├── EHS_040240.apk
├── enterprisehomescreen.xml
├── ESPAS_Arbeitsprofil.png
│
├── android14/
│   ├── EHS_070112.apk
│   └── enterprisehomescreen.xml
│
└── README.md
```

### Root

Enthält die Konfiguration für:

```text
Android 10 / MX10.4
Android 11 / MX11.3
```

Verwendete EHS-Version:

```text
EHS 4.2
```

### `android14/`

Enthält die Konfiguration für neuere Android-Versionen.

Verwendete EHS-Version:

```text
EHS 7.1.12
```

### Wallpaper

```text
ESPAS_Arbeitsprofil.png
```

Das Wallpaper wird gemeinsam verwendet und durch StageNow nach folgendem Pfad kopiert:

```text
/enterprise/usr/ESPAS_Arbeitsprofil.png
```

---

# EHS-Konfigurationsdatei

Die zentrale Konfiguration befindet sich in:

```text
/enterprise/usr/enterprisehomescreen.xml
```

Die Datei definiert unter anderem:

- sichtbare Apps
- EHS-Titel
- Hintergrundbild
- Admin-Zugang
- USB-Debugging
- Zugriff auf Systemeinstellungen
- Recent Apps
- Admin-Timeout

Grundstruktur:

```xml
<config>

    <kiosk>
    </kiosk>

    <applications>
    </applications>

    <tools>
    </tools>

    <passwords>
    </passwords>

    <preferences>
    </preferences>

</config>
```

---

# Anwendungen im User Mode

Aktuell werden folgende Apps über EHS angezeigt:

```text
PIXI
OneDrive
Rechner
Kamera
Google Fotos
```

Weitere installierte Anwendungen können vorhanden sein, werden jedoch nicht automatisch angezeigt.

---

# Neue App hinzufügen

Eine neue App wird innerhalb von:

```xml
<applications>
```

eingetragen.

Schema:

```xml
<application
    label="Anzeigename"
    package="com.beispiel.app"
    activity="com.beispiel.app.MainActivity"/>
```

Beispiel:

```xml
<application
    label="Neue App"
    package="com.company.app"
    activity="com.company.app.MainActivity"/>
```

Voraussetzungen:

- App ist installiert
- Package-Name ist korrekt
- Start-Activity ist korrekt
- XML wird erneut auf das Gerät verteilt

Nach Änderung der XML wird diese wieder nach:

```text
/enterprise/usr/enterprisehomescreen.xml
```

kopiert.

---

# Relevante EHS-Preferences

Produktive Konfiguration:

```xml
<wallpaper>/enterprise/usr/ESPAS_Arbeitsprofil.png</wallpaper>

<usb_debugging_disabled>1</usb_debugging_disabled>

<system_settings_restricted>1</system_settings_restricted>

<recent_apps_button_disabled>1</recent_apps_button_disabled>

<recent_apps_access_disabled>1</recent_apps_access_disabled>

<admin_inactivity_timeout>60</admin_inactivity_timeout>
```

Bedeutung:

```text
usb_debugging_disabled
→ deaktiviert ADB/USB-Debugging

system_settings_restricted
→ schränkt Zugriff auf Android-Einstellungen ein

recent_apps_button_disabled
→ deaktiviert Recent-Apps-Taste

recent_apps_access_disabled
→ verhindert Zugriff auf Recent Apps

admin_inactivity_timeout
→ automatische Rückkehr aus Admin Mode nach 60 Sekunden
```

---

# Admin Mode

EHS startet standardmässig im User Mode.

Für Wartungsarbeiten:

```text
EHS
→ Admin Mode
→ Admin-Passwort eingeben
```

Im Admin Mode können:

- Systemeinstellungen geöffnet werden
- Apps geprüft werden
- Konfigurationen angepasst werden
- EHS verlassen werden
- StageNow gestartet werden

Der Admin Mode wird nach:

```text
60 Sekunden Inaktivität
```

automatisch beendet.

---

# StageNow und Wartung

StageNow ist im normalen EHS-User-Mode nicht sichtbar.

Für Wartungsarbeiten:

```text
User Mode
→ Admin Mode
→ EHS / Benutzeroberfläche verlassen
→ StageNow starten
→ QR-Code scannen
→ Konfiguration anwenden
→ EHS wieder starten
```

StageNow sollte nicht dauerhaft für normale Benutzer sichtbar sein.

---

# StageNow – EHS Installation

Typischer Ablauf:

```text
1. FileMgr
   → EHS APK herunterladen

2. FileMgr
   → enterprisehomescreen.xml herunterladen

3. FileMgr
   → ESPAS_Arbeitsprofil.png herunterladen

4. AppMgr
   → EHS installieren

5. AppMgr
   → EHS starten

6. AppMgr
   → EHS als Default Launcher setzen
```

---

# Zielpfade

## EHS 4.2

```text
/enterprise/usr/EHS_040240.apk
```

## EHS 7.1.12

```text
/enterprise/usr/EHS_070112.apk
```

## XML

```text
/enterprise/usr/enterprisehomescreen.xml
```

## Wallpaper

```text
/enterprise/usr/ESPAS_Arbeitsprofil.png
```

---

# AppMgr – Paketnamen

## EHS 4.2

```text
com.symbol.enterprisehomescreen
```

## EHS 7.x

```text
com.zebra.mdna.enterprisehomescreen
```

Diese Paketnamen werden unter anderem für folgende StageNow-Aktionen benötigt:

```text
Launch Application
Set as Default Launcher
```

---

# Google Chrome

Google Chrome bleibt auf den Zebra-Geräten technisch aktiviert.

Paket:

```text
com.android.chrome
```

Grund:

Bei Tests auf TC26-Geräten konnte reproduzierbar festgestellt werden, dass bei deaktiviertem Chrome Probleme beim Aufbau bzw. bei der vollständigen Verarbeitung der WLAN-Verbindung auftraten.

Die grundlegende WLAN- und IP-Kommunikation wird zwar durch Android-Systemkomponenten bereitgestellt, Chrome bzw. Chromium-basierte Komponenten können jedoch für nachgelagerte Web-, HTTPS-, WebView-, Captive-Portal- oder Intent-Prozesse relevant sein.

Deshalb gilt:

```text
Chrome aktiviert lassen
→ über EHS ausblenden
→ nicht systemseitig deaktivieren
```

StageNow zur Aktivierung:

```text
AppMgr
→ Enable Application
→ com.android.chrome
```

---

# Google Play Store

Paket:

```text
com.android.vending
```

Kann bei Wartungsarbeiten temporär aktiviert werden:

```text
AppMgr
→ Enable Application
→ com.android.vending
```

Der Play Store sollte im normalen User Mode nicht sichtbar sein.

---

# Android 10 / MX10.4

Bei Android 10 muss für BLE-/Location-abhängige Anwendungen der globale Standortdienst aktiviert sein.

Prüfung:

```cmd
adb shell settings get secure location_mode
```

Erwartete Ausgabe:

```text
3
```

Wenn:

```text
0
```

ist der Standort deaktiviert.

Im StageNow-Profil für MX10.4 deshalb:

```text
Location Services → ON
```

---

# ADB Recovery

Produktive EHS-Konfigurationen deaktivieren USB-Debugging.

Daher sollte ein separater StageNow-Recovery-QR vorhanden sein.

Beispiel:

```text
USBMgr
→ USB Module Usage: Enable
→ USB ADB Usage: Enable
```

Damit kann ADB bei Wartungsarbeiten wieder aktiviert werden.

---

# Chrome prüfen

## Installation

```cmd
adb shell pm list packages | findstr com.android.chrome
```

Erwartet:

```text
package:com.android.chrome
```

## Deaktivierte Apps prüfen

```cmd
adb shell pm list packages -d | findstr com.android.chrome
```

Wenn keine Ausgabe erscheint, ist Chrome nicht deaktiviert.

---

# Repository und Versionierung

Die Dateien werden über GitHub bereitgestellt.

Für produktive StageNow-Profile sollten nach Möglichkeit feste Commit-URLs verwendet werden.

Vorteil:

```text
Commit-Link
→ unveränderlicher Stand
→ reproduzierbares Staging
→ getestete Version bleibt erhalten
```

Für Dateien, die bewusst aktualisiert werden sollen, kann alternativ `main` verwendet werden.

---

# Wartung

Bei Änderungen:

```text
1. Datei lokal anpassen
2. auf Testgerät prüfen
3. StageNow-Profil testen
4. Git commit
5. Git push
6. neuen Commit-Permalink dokumentieren
7. produktiven StageNow-QR aktualisieren
```

Änderungen an der produktiven XML sollten nicht ungeprüft direkt auf alle Geräte verteilt werden.

---

# Wichtige Hinweise

- Chrome nicht deaktivieren.
- EHS-Version muss zur Android-/MX-Version passen.
- Produktive XML deaktiviert ADB.
- ADB-Recovery-QR separat aufbewahren.
- EHS zuerst testen, danach Lockdown aktivieren.
- StageNow im normalen User Mode nicht freigeben.
- Neue Apps immer zuerst auf einem Testgerät prüfen.
- Änderungen an `enterprisehomescreen.xml` versionieren.
