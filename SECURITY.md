# Sicherheit & Datenschutz - Fahrschule Dorn Website

## Überblick

Dieses Dokument beschreibt die Datenverarbeitung, Sicherheitsmaßnahmen und DSGVO-Compliance der Website.

**Status: DSGVO-konform** - Keine externen Ressourcen beim Seitenladen, kein Consent-Banner erforderlich.

## Datenfluss-Analyse

### Datenerhebung auf Client-Seite

```
┌────────────────────────────────────────────────────────────────┐
│                    KEINE DIREKTE DATENERHEBUNG                  │
│                                                                 │
│  • Kein Kontaktformular                                        │
│  • Keine Cookies (First-Party)                                 │
│  • Kein Local Storage                                          │
│  • Kein Session Storage                                        │
│  • Keine Analytics-Skripte                                     │
│  • Keine Tracking-Pixel                                        │
│  • Keine externen Ressourcen beim Laden                        │
└────────────────────────────────────────────────────────────────┘
```

### Datenübertragung an Dritte

| Ressource | Status | Beschreibung |
|-----------|--------|--------------|
| **Bilder** | ✅ Lokal | Alle Bilder in `assets/images/` gehostet |
| **Schriften** | ✅ System | System-Fonts, kein Google Fonts |
| **Karten** | ✅ Kein Auto-Load | SVG-Platzhalter, Google Maps nur bei Klick |
| **Analytics** | ✅ Keine | Kein Tracking implementiert |
| **CDNs** | ✅ Keine | Alle Ressourcen lokal |

### Externe Links (nutzerinitiiert)

Folgende externe Dienste werden **nur bei aktivem Klick** durch den Nutzer aufgerufen:

| Dienst | Zweck | Datenschutz |
|--------|-------|-------------|
| Google Maps | Standort-Anzeige | [Google Datenschutz](https://policies.google.com/privacy) |
| Facebook | Social Media | [Facebook Datenschutz](https://www.facebook.com/privacy) |

Diese Links öffnen sich in einem neuen Tab (`target="_blank"`) mit `rel="noopener noreferrer"`.

## DSGVO Art. 13 - Informationspflichten

### Status der Datenschutzerklärung (datenschutz.html)

| Pflichtangabe | Status | Abschnitt |
|---------------|--------|-----------|
| Name/Kontakt Verantwortlicher | ✅ Vorhanden | 1 |
| Kontaktdaten DSB | ✅ Nicht erforderlich (dokumentiert) | 2 |
| Zwecke der Verarbeitung | ✅ Vorhanden | 3-6 |
| Rechtsgrundlagen | ✅ Vorhanden | 3 |
| Empfänger/Kategorien | ✅ Vorhanden | 7 |
| Drittlandübermittlung | ✅ Nicht erforderlich | - |
| Speicherdauer | ✅ Vorhanden | 4 |
| Betroffenenrechte | ✅ Vorhanden | 9 |
| Beschwerderecht | ✅ Vorhanden | 9 |
| Externe Links | ✅ Vorhanden | 8 |

### Drittlandübermittlung

**Nicht erforderlich**, da keine automatische Datenübertragung an Drittländer erfolgt:
- Alle Bilder lokal gehostet
- Keine CDNs
- Keine eingebetteten iFrames
- Externe Dienste nur bei Nutzerinteraktion

## DSGVO Art. 25 - Privacy by Design

### Implementierter Stand

| Prinzip | Umsetzung | Status |
|---------|-----------|--------|
| Datenminimierung | Keine eigene Datenerhebung | ✅ Erfüllt |
| Speicherbegrenzung | Keine persistente Speicherung | ✅ Erfüllt |
| Integrität | HTTPS erforderlich (Server-Config) | ⚠️ Server-abhängig |
| Vertraulichkeit | Keine sensiblen Daten verarbeitet | ✅ Erfüllt |
| Transparenz | Datenschutzerklärung vorhanden | ✅ Erfüllt |
| Rechenschaftspflicht | Dokumentation vorhanden | ✅ Erfüllt |
| Privacy by Default | Keine externen Requests | ✅ Erfüllt |

### Umgesetzte Maßnahmen

```
┌─────────────────────────────────────────────────────────────┐
│              PRIVACY BY DESIGN - UMGESETZT                   │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ✅ EXTERNE BILDER LOKAL GEHOSTET                          │
│     • hero-bg.jpg (ehemals Pexels)                         │
│     • infos-bg.jpg (ehemals Pexels)                        │
│     • ausbildung.webp (ehemals LeadConnectorHQ)            │
│     • buero.jpg (ehemals lirp.cdn-website.com)             │
│                                                             │
│  ✅ GOOGLE MAPS IFRAME ENTFERNT                            │
│     • Ersetzt durch SVG-Platzhalter (lokal)                │
│     • Google Maps öffnet nur bei Klick (neuer Tab)         │
│     • Kein automatischer Datentransfer                     │
│                                                             │
│  ✅ KEINE EXTERNEN SCHRIFTEN                               │
│     • System-Font-Stack verwendet                          │
│     • Kein Google Fonts                                    │
│                                                             │
│  ✅ KEINE TRACKING/ANALYTICS                               │
│     • Kein Google Analytics                                │
│     • Keine Tracking-Pixel                                 │
│     • Kein Facebook Pixel                                  │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

## Server-Sicherheit

### Empfohlene HTTP Security Headers

```apache
# .htaccess oder Server-Konfiguration

# Content Security Policy (strikt - keine externen Ressourcen)
Header set Content-Security-Policy "default-src 'self'; \
    style-src 'self' 'unsafe-inline'; \
    script-src 'self' 'unsafe-inline'; \
    img-src 'self' data:; \
    frame-src 'none'; \
    connect-src 'self'"

# XSS Protection
Header set X-Content-Type-Options "nosniff"
Header set X-Frame-Options "SAMEORIGIN"
Header set X-XSS-Protection "1; mode=block"

# HTTPS Enforcement
Header set Strict-Transport-Security "max-age=31536000; includeSubDomains"

# Referrer Policy
Header set Referrer-Policy "strict-origin-when-cross-origin"

# Permissions Policy
Header set Permissions-Policy "geolocation=(), microphone=(), camera=()"
```

### TLS/SSL Anforderungen

| Anforderung | Empfehlung |
|-------------|------------|
| TLS-Version | TLS 1.2+ (TLS 1.3 bevorzugt) |
| Cipher Suites | Moderne Cipher, kein RC4, 3DES |
| Zertifikat | Valides SSL-Zertifikat (Let's Encrypt o.ä.) |
| HSTS | Aktiviert mit min. 1 Jahr max-age |

## Schwachstellen-Analyse

### Inline Scripts

```
ℹ️  HINWEIS: Inline JavaScript

Die Website verwendet Inline-JavaScript für:
- Mobile Navigation Toggle
- Accordion-Funktionalität
- Scroll-Animationen
- Jahr-Aktualisierung im Footer

Risikobewertung: NIEDRIG
- Keine externe Datenverarbeitung
- Keine sensiblen Operationen
- Keine Benutzereingaben verarbeitet
- CSP erlaubt 'unsafe-inline' für diese Funktionen
```

### Ressourcen-Übersicht

| Ressource | Speicherort | Risiko |
|-----------|-------------|--------|
| hero-bg.jpg | assets/images/ | Keins |
| infos-bg.jpg | assets/images/ | Keins |
| ausbildung.webp | assets/images/ | Keins |
| buero.jpg | assets/images/ | Keins |
| map-placeholder.svg | assets/images/ | Keins |

## Incident Response

### Bei Datenschutzvorfall

1. **Identifikation**: Welche Daten betroffen?
2. **Eindämmung**: Betroffene Ressource deaktivieren
3. **Meldung**: Bei Risiko für Betroffene: Aufsichtsbehörde informieren (72h)
4. **Dokumentation**: Vorfall im Verzeichnis dokumentieren
5. **Korrektur**: Ursache beheben, Maßnahmen implementieren

### Kontakt Aufsichtsbehörde

```
Der Landesbeauftragte für den Datenschutz
und die Informationsfreiheit Baden-Württemberg

Lautenschlagerstraße 20
70173 Stuttgart

Telefon: 0711 / 61 55 41 - 0
E-Mail: poststelle@lfdi.bwl.de
```

## Checkliste für Deployment

- [ ] SSL-Zertifikat installiert und gültig
- [ ] HTTPS-Redirect konfiguriert
- [ ] Security Headers gesetzt (siehe oben)
- [ ] Datenschutzerklärung aktuell
- [ ] Impressum vollständig (USt-IdNr. ergänzen)
- [ ] Hosting-Anbieter in Datenschutz ergänzen

## Offene Punkte

| ID | Beschreibung | Priorität | Status |
|----|--------------|-----------|--------|
| SEC-001 | USt-IdNr. in Impressum ergänzen | Mittel | Platzhalter vorhanden |
| SEC-002 | Hosting-Anbieter in Datenschutz ergänzen | Mittel | Platzhalter vorhanden |

---

*Dokumentation aktualisiert: Januar 2026*
*Nächste Überprüfung: Bei Änderungen an der Website*
