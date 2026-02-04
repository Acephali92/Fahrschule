# Fahrschule Dorn - Website

[![GitHub](https://img.shields.io/badge/GitHub-Repository-blue)](https://github.com/Acephali92/Fahrschule)

Statische Website für die Fahrschule Dorn in Lauchringen (79787).

**DSGVO-konform** - Keine externen Ressourcen beim Seitenladen, kein Consent-Banner erforderlich.

## System Overview

| Attribut | Wert |
|----------|------|
| **Typ** | Statische Single-Page Website |
| **Sprache** | HTML5, CSS3, Vanilla JavaScript |
| **Framework** | Keines (Zero-Dependency Frontend) |
| **Build-System** | Nicht erforderlich |
| **Hosting** | Static Hosting (Netlify, Uberspace, etc.) |

### Projektstruktur

```
Fahrschule/
├── index.html              # Hauptseite (Single-Page mit Anker-Navigation)
├── impressum.html          # Impressum (§ 5 TMG, § 18 MStV)
├── datenschutz.html        # Datenschutzerklärung (Art. 13 DSGVO)
├── assets/
│   └── images/
│       ├── hero-bg.jpg         # Hero-Hintergrund
│       ├── infos-bg.jpg        # Kontakt-Hintergrund
│       ├── ausbildung.webp     # Ausbildungsbild
│       ├── buero.jpg           # Bürobild
│       └── map-placeholder.svg # Karten-Platzhalter
├── _headers                # Netlify Security Headers (optional)
├── .htaccess               # Apache Security Headers (optional)
├── robots.txt              # Crawler-Regeln (Allow all)
├── sitemap.xml             # XML-Sitemap für Suchmaschinen
├── README.md               # Diese Datei
├── ARCHITECTURE.md         # Systemarchitektur
└── SECURITY.md             # Sicherheit & Datenschutz
```

## Quick-Start Guide

### Voraussetzungen

- Beliebiger Webserver oder Static Hosting
- Keine Build-Tools erforderlich
- Keine Datenbank erforderlich

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

## Deployment

### Empfohlene Hosting-Anbieter

| Anbieter | Typ | Kosten | HTTPS | Empfehlung |
|----------|-----|--------|-------|------------|
| **Netlify** | Static Hosting | Kostenlos | Automatisch | Einfachstes Setup |
| **Uberspace** | Shared Hosting | Ab 1€/Monat | Let's Encrypt | Deutscher Anbieter |
| **GitHub Pages** | Static Hosting | Kostenlos | Automatisch | Für Entwickler |
| **Vercel** | Static Hosting | Kostenlos | Automatisch | Schnell |

### Netlify Deployment

```bash
# 1. Netlify CLI installieren
npm install -g netlify-cli

# 2. Einloggen
netlify login

# 3. Deployen
cd /path/to/Fahrschule
netlify deploy --prod

# Oder: Repository mit Netlify verbinden für Auto-Deploy
```

### Traditionelles Hosting (FTP/SFTP)

```bash
# Alle Dateien auf den Webserver kopieren:
scp -r ./* user@server:/var/www/html/

# Oder via FTP/SFTP Client:
# 1. Mit Server verbinden
# 2. Alle Dateien ins Web-Root hochladen
# 3. Berechtigungen prüfen (644 für Dateien, 755 für Ordner)
```

### Nach dem Deployment

1. **HTTPS aktivieren** (Let's Encrypt oder Hosting-Anbieter)
2. **Domain konfigurieren** (DNS A-Record oder CNAME)
3. **Platzhalter ersetzen:**
   - `impressum.html`: `[USt-IdNr. hier eintragen]`
   - `datenschutz.html`: `[HOSTING-ANBIETER]` und `[ANSCHRIFT]`

## Seitenstruktur (index.html)

| Sektion | Anchor-ID | Beschreibung |
|---------|-----------|--------------|
| Hero | `#start` | Hauptbanner mit CTA |
| Führerscheinklassen | `#klassen` | Übersicht aller Klassen |
| Ausbildung | `#ausbildung` | Informationen zum Ablauf |
| Kontakt/Infos | `#infos` | Kontaktdaten, Öffnungszeiten, Karte |
| Behörden-Infos | `#behoerden` | Accordion mit Infos |

## Datenschutz & DSGVO

### Status: Vollständig konform

| Kriterium | Status |
|-----------|--------|
| Externe Ressourcen beim Laden | ✅ Keine |
| Cookies | ✅ Keine |
| Tracking/Analytics | ✅ Keine |
| Google Fonts | ✅ Keine (System-Fonts) |
| Google Maps iFrame | ✅ Entfernt (Click-to-Link) |
| Consent-Banner | ✅ Nicht erforderlich |

### Externe Links (nutzerinitiiert)

- Google Maps: Öffnet bei Klick im neuen Tab
- Facebook: Öffnet bei Klick im neuen Tab

## Anpassbare Werte

| Datei | Platzhalter | Beschreibung |
|-------|-------------|--------------|
| `impressum.html` | `[USt-IdNr. hier eintragen]` | Umsatzsteuer-ID |
| `datenschutz.html` | `[HOSTING-ANBIETER]` | Name des Hosters |
| `datenschutz.html` | `[ANSCHRIFT DES HOSTING-ANBIETERS]` | Adresse des Hosters |

## Browser-Kompatibilität

| Browser | Mindestversion | Status |
|---------|----------------|--------|
| Chrome | 88+ | Unterstützt |
| Firefox | 78+ | Unterstützt |
| Safari | 14+ | Unterstützt |
| Edge | 88+ | Unterstützt |
| IE | - | Nicht unterstützt |

## SEO Features

- Schema.org JSON-LD (DrivingSchool)
- Open Graph Meta-Tags
- Semantische HTML5-Struktur
- Meta Description für lokale Suche
- Responsive Design (Mobile-First)
- robots.txt (erlaubt alle Crawler)
- XML-Sitemap

## Performance (Chrome DevTools Audit)

| Metrik | Wert | Status |
|--------|------|--------|
| **LCP** | 930ms | 🟢 Gut |
| **CLS** | 0.00 | 🟢 Gut |
| **Externe Requests** | 0 | 🟢 DSGVO-konform |
| **Console Errors** | 0 | 🟢 Fehlerfrei |

## Wartung

### Automatisch

- Copyright-Jahr im Footer (JavaScript)

### Manuell bei Bedarf

- Kontaktdaten ändern
- Öffnungszeiten anpassen
- Bilder austauschen (in `assets/images/`)

## Weiterführende Dokumentation

- [Systemarchitektur](./ARCHITECTURE.md) - Technische Details
- [Sicherheit & Datenschutz](./SECURITY.md) - DSGVO-Compliance

## Lizenz

Proprietär - Fahrschule Dorn, Lauchringen

---

*Dokumentation aktualisiert: Januar 2026*
