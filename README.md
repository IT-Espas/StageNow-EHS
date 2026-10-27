# Changelog

Alle relevanten Änderungen an ZebraFinder werden in dieser Datei dokumentiert.

## [2.0] - 2026-10-27

### Neu
- Live-Radar zur visuellen Näherungsanzeige auf Basis der BLE-RSSI-Werte.
- Pulsierende Radar-Animation.
- Akustischer Radar-Piepser; die Wiederholrate wird bei stärkerem Signal erhöht.
- Distanzanzeige in groben Bereichen statt scheinpräzisen Dezimalwerten (z. B. `0.5–1 m`, `1–2 m`).
- RSSI-Glättung zur ruhigeren und praxisnäheren Anzeige.
- Trendanzeige `NÄHER`, `WEITER` bzw. `GLEICH`.
- Überarbeitete, stärker zentrierte Benutzeroberfläche.
- Gerätenamen werden weiterhin aus BLE-/Bluetooth-Informationen übernommen; Fallback-Logik für fehlende Namen bleibt vorhanden.

### Behoben
- Geräte mit identischem Bluetooth-Namen wurden gegenseitig ausgefiltert und konnten sich dadurch nicht finden. Die eindeutige Verwaltung erfolgt nun über die BLE-Adresse; der Gerätename dient nur der Anzeige.
- Radar-Piepser war auf Zebra-Geräten teilweise nicht hörbar. Der kurze Radar-Ton verwendet nun den Alarmkanal.
- Radar-Piepstakt blieb auf einem alten RSSI-Wert stehen. Bei aktivem Radar läuft der BLE-Scan kontinuierlich weiter, sodass neue RSSI-Werte den Takt aktualisieren.
- Android-10/MX10.4-Test: BLE-Scan funktioniert wieder zuverlässig, wenn `ACCESS_FINE_LOCATION` erteilt **und** der systemweite Standortdienst aktiviert ist.

### Geändert
- Der temporäre `Radar-Test`/Simulationsmodus wurde aus der Produktivoberfläche entfernt.
- Die bestehende GATT-`RING`-Funktion und der Hintergrunddienst bleiben unverändert erhalten.
- Release-Dateiname bleibt `Zebrafinder.apk`, damit bestehende StageNow-Links stabil bleiben.

### Plattformhinweise
- Android 10/11: `ACCESS_FINE_LOCATION` erforderlich; auf MX10.4 zusätzlich Standortdienste aktivieren.
- Android 12+: `BLUETOOTH_SCAN`, `BLUETOOTH_CONNECT`, `BLUETOOTH_ADVERTISE`.
- Android 13+: `BLUETOOTH_SCAN` mit `android:usesPermissionFlags="neverForLocation"`.

## [1.x] - vorheriger Stand

### Vorhandene Funktionen
- Serverlose BLE-Gerätesuche über feste ZebraFinder-Service-UUID.
- GATT-`RING`-Befehl mit lautem Alarm auf dem Zielgerät.
- Foreground Service für BLE Advertising/GATT im Hintergrund.
- Autostart nach Neustart über BootReceiver.
- GL-PIN `492680` mit automatischer Sperre nach 5 Minuten.
- Scrollbare Geräteliste.
- Android-13-BLE-Kompatibilitätsfix mit `neverForLocation`.
