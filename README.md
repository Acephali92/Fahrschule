# Fahrschule Dorn - Website

Statische Website für die Fahrschule Dorn in Lauchringen (79787).

## System Overview

| Attribut | Wert |
|----------|------|
| **Typ** | Statische Single-Page Website |
| **Sprache** | HTML5, CSS3, Vanilla JavaScript |
| **Framework** | Keines (Zero-Dependency Frontend) |
| **Build-System** | Nicht erforderlich |
| **Hosting** | Beliebiger Webserver / Static Hosting |

### Projektstruktur

```
Fahrschule/
├── index.html          # Hauptseite (Single-Page mit Anker-Navigation)
├── impressum.html      # Impressum (§ 5 TMG, § 18 MStV)
├── datenschutz.html    # Datenschutzerklärung (Art. 13 DSGVO)
├── README.md           # Diese Datei
├── ARCHITECTURE.md     # Systemarchitektur
└── SECURITY.md         # Sicherheit & Datenschutz
```

## Quick-Start Guide

### Voraussetzungen

- Webserver (Apache, Nginx, IIS) oder
- Static File Hosting (Netlify, Vercel, GitHub Pages) oder
- Lokaler Entwicklungsserver

### Lokale Entwicklung

```bash
# Option 1: Python HTTP Server
cd /path/to/Fahrschule
python -m http.server 8080
# Öffne http://localhost:8080

# Option 2: Node.js (npx)
npx serve .
# Öffne http://localhost:3000

# Option 3: PHP Built-in Server
php -S localhost:8080

# Option 4: VS Code Live Server Extension
# Rechtsklick auf index.html → "Open with Live Server"
```

### Deployment

```bash
# Alle Dateien auf den Webserver kopieren:
scp -r ./* user@server:/var/www/html/

# Oder via FTP/SFTP Client die Dateien hochladen
```

## Seitenstruktur (index.html)

| Sektion | Anchor-ID | Beschreibung |
|---------|-----------|--------------|
| Hero | `#start` | Hauptbanner mit CTA |
| Führerscheinklassen | `#klassen` | Übersicht aller Klassen (PKW, Motorrad, LKW, etc.) |
| Ausbildung | `#ausbildung` | Informationen zum Ausbildungsablauf |
| Kontakt/Infos | `#infos` | Kontaktdaten, Öffnungszeiten, Google Maps |
| Behörden-Infos | `#behoerden` | Accordion mit behördlichen Informationen |

## Environment Configuration

Diese Website benötigt **keine** Umgebungsvariablen oder Konfigurationsdateien.

### Anpassbare Werte (direkt in HTML)

| Datei | Zeile/Bereich | Beschreibung |
|-------|---------------|--------------|
| `index.html` | `<meta og:url>` | Produktions-URL |
| `index.html` | Kontaktdaten | Telefon, E-Mail, Adresse |
| `impressum.html` | USt-IdNr. | `[USt-IdNr. hier eintragen]` |
| `datenschutz.html` | Hosting-Anbieter | `[HOSTING-ANBIETER]` |

## Externe Abhängigkeiten

| Ressource | Typ | Datenschutz-Relevanz |
|-----------|-----|----------------------|
| `images.pexels.com` | Bilder (Hero, Background) | IP-Übertragung an Drittserver |
| `images.leadconnectorhq.com` | Bild (Ausbildung) | IP-Übertragung an Drittserver |
| `lirp.cdn-website.com` | Bild (Büro) | IP-Übertragung an Drittserver |
| `google.com/maps/embed` | Google Maps iFrame | IP, Cookies an Google |
| `facebook.com` | Externer Link | Nur bei Klick |

> **Hinweis:** Für vollständige DSGVO-Konformität sollten externe Bilder lokal gehostet und Google Maps durch eine statische Karte oder Click-to-Load ersetzt werden.

## Browser-Kompatibilität

| Browser | Mindestversion | Status |
|---------|----------------|--------|
| Chrome | 88+ | Unterstützt |
| Firefox | 78+ | Unterstützt |
| Safari | 14+ | Unterstützt |
| Edge | 88+ | Unterstützt |
| IE | - | Nicht unterstützt |

### Verwendete moderne Features

- CSS Custom Properties (`--var`)
- CSS `backdrop-filter`
- `IntersectionObserver` API
- ES6+ Syntax (`const`, `let`, Arrow Functions)

## Wartung

### Jährliche Aktualisierung

Das Copyright-Jahr im Footer wird automatisch via JavaScript aktualisiert:

```javascript
document.getElementById('current-year').textContent = new Date().getFullYear();
```

### Inhaltliche Änderungen

Alle Inhalte befinden sich direkt in den HTML-Dateien. Für Änderungen:

1. HTML-Datei mit Texteditor öffnen
2. Gewünschte Texte/Daten anpassen
3. Datei speichern
4. Auf Server hochladen

## Weiterführende Dokumentation

- [Systemarchitektur](./ARCHITECTURE.md) - Technische Details und Datenfluss
- [Sicherheit & Datenschutz](./SECURITY.md) - DSGVO-Compliance und Privacy by Design

## Lizenz

Proprietär - Fahrschule Dorn, Lauchringen

---

*Dokumentation erstellt: Januar 2026*
