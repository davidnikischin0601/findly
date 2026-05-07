# Garage Inventar – PWA Prototyp

Eine installierbare Web-App für Android (und Desktop) zur Verwaltung deiner Garagen-Inventars mit QR-Codes, KI-Erkennung und Ausmist-Modus.

## Features

- **Behälter mit QR-Codes**: Bis zu ~15 Boxen/Fächer mit eindeutigen IDs (G-01, G-02 …)
- **Foto vom Sollzustand**: Pro Behälter ein Referenzbild, wie es aufgeräumt aussehen soll
- **Items pro Behälter**: Mit Namen, Kategorie, Notiz und Foto
- **QR-Scanner**: Behälter via Handy-Kamera scannen → direkt zum Inhalt
- **Suche**: "Wo ist der 10er Maulschlüssel?" → Behälter-ID + Foto
- **Ausmist-Modus**: Items, die seit über 6 Monaten nicht angefasst wurden
- **KI (optional)**:
  - Foto vom Werkzeug → KI füllt Name + Kategorie aus
  - Foto vom Schrank → KI gibt Organisations-Tipps
- **QR-Druck**: Alle Behälter-QR-Codes auf einer A4-Seite drucken
- **Offline-fähig**: Funktioniert ohne Internet (außer KI)
- **Backup**: Export/Import als JSON-Datei

## Installation

### Lokal testen
1. Ordner `garage-pwa` auf einen Webserver legen (z.B. lokal mit `python -m http.server 8000`)
2. Im Browser öffnen: `http://localhost:8000`
3. **Wichtig**: Für Kamera-Zugriff braucht es HTTPS oder localhost!

### Auf dem Handy installieren
1. App per HTTPS bereitstellen (z.B. GitHub Pages, Hostinger, Netlify)
2. Auf Android Chrome öffnen → Menü → "Zum Startbildschirm hinzufügen"
3. Beim ersten Öffnen Kamera-Berechtigung erlauben

### Hosting via GitHub Pages (einfachste Option)
1. Neues Repo erstellen, alle Dateien hochladen
2. Settings → Pages → Branch `main`, Folder `/`
3. URL z.B. `https://username.github.io/garage-pwa/` öffnen
4. Auf Handy installieren (siehe oben)

## KI-Funktionen aktivieren

1. API-Key bei https://console.anthropic.com holen
2. In der App auf ⚙ (oben rechts) → API-Key eintragen → Speichern
3. Beim Item-Hinzufügen erscheint nach dem Foto-Upload "KI: Was ist das?"
4. Im Behälter-Detail erscheint "KI: Organisations-Tipp holen"

## QR-Code-Workflow

1. Behälter in der App anlegen → ID wird automatisch vergeben (G-01, G-02 …)
2. ⚙ → "QR-Codes als Bogen öffnen" → Drucken (am besten auf Etikettenpapier)
3. QR-Code auf den Behälter kleben
4. Beim nächsten Mal: Tab "Scan" → QR-Code scannen → direkt im Behälter

## Datenmodell (lokal im Browser)

- `localStorage`: Behälter, Items, API-Key
- `IndexedDB`: Fotos (komprimiert auf max. 1200px, JPEG 82%)

## Bekannte Einschränkungen (Prototyp)

- Single-User: Keine Synchronisation zwischen Geräten (außer manuell per Backup)
- Keine Verlauf-Historie ("zuletzt verwendet" wird nur überschrieben)
- "Verkaufen"-Liste ist nur eine Markierung, noch keine Marktplatz-Anbindung
- KI-Aufrufe gehen direkt vom Browser an Anthropic (API-Key liegt lokal, nicht ideal für Produktion – für Familieneinsatz später Backend)

## Was als nächstes?

- [ ] Verleih-Tracking ("an Nachbar XY, seit 3 Wochen")
- [ ] Wert-Schätzung beim Verkaufen via KI
- [ ] Sprachsuche ("Wo ist der Schraubenzieher?")
- [ ] Erweiterung auf weitere Räume (Küche, Keller, Hobbyraum)
- [ ] Multi-User mit Backend (z.B. Supabase)
- [ ] 3D-Druck-Vorlagen für QR-Code-Halter
