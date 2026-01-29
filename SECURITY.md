# Sicherheit & Datenschutz - Fahrschule Dorn Website

## Überblick

Dieses Dokument beschreibt die Datenverarbeitung, Sicherheitsmaßnahmen und DSGVO-Compliance der Website.

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
└────────────────────────────────────────────────────────────────┘
```

### Datenübertragung an Dritte

| Drittanbieter | Ressourcentyp | Übertragene Daten | Rechtsgrundlage |
|---------------|---------------|-------------------|-----------------|
| **Pexels.com** | Stockfotos | IP-Adresse, User-Agent, Referrer | Art. 6 Abs. 1 lit. f DSGVO |
| **LeadConnectorHQ** | CDN-Bild | IP-Adresse, User-Agent, Referrer | Art. 6 Abs. 1 lit. f DSGVO |
| **lirp.cdn-website.com** | CDN-Bild | IP-Adresse, User-Agent, Referrer | Art. 6 Abs. 1 lit. f DSGVO |
| **Google Maps** | iFrame Embed | IP-Adresse, Cookies, Standort (optional) | **[PROBLEMATISCH]** |

### Kritische Bewertung: Google Maps

```
⚠️  DATENSCHUTZ-RISIKO: HOCH

Google Maps Embed überträgt:
- IP-Adresse des Nutzers
- Browser-Fingerprint
- Google-Cookies (falls eingeloggt)
- Potentiell Standortdaten

Empfehlung:
- Ersetzen durch statisches Kartenbild mit Link zu Google Maps
- Oder: Click-to-Load Consent-Lösung implementieren
```

## DSGVO Art. 13 - Informationspflichten

### Status der Datenschutzerklärung (datenschutz.html)

| Pflichtangabe | Status | Zeile/Abschnitt |
|---------------|--------|-----------------|
| Name/Kontakt Verantwortlicher | ✅ Vorhanden | Abschnitt 1 |
| Kontaktdaten DSB | ✅ Nicht erforderlich (dokumentiert) | Abschnitt 2 |
| Zwecke der Verarbeitung | ✅ Vorhanden | Abschnitte 3-6 |
| Rechtsgrundlagen | ✅ Vorhanden | Abschnitt 3 |
| Empfänger/Kategorien | ✅ Vorhanden | Abschnitt 7 |
| Drittlandübermittlung | ⚠️ **FEHLT** | - |
| Speicherdauer | ✅ Vorhanden | Abschnitt 4 |
| Betroffenenrechte | ✅ Vorhanden | Abschnitt 9 |
| Beschwerderecht | ✅ Vorhanden | Abschnitt 9 |
| Automatisierte Entscheidungsfindung | ✅ Nicht anwendbar | - |

### Handlungsbedarf

```
[DOCUMENTATION GAP] Drittlandübermittlung

Die folgenden Dienste übertragen Daten in die USA:
- Google Maps (Google LLC)
- Pexels (Canva Germany GmbH, Server unklar)
- LeadConnectorHQ (HighLevel Inc., USA)

Ergänzung in datenschutz.html erforderlich:
"Datenübermittlung in Drittländer (Art. 49 DSGVO)"
```

## DSGVO Art. 25 - Privacy by Design

### Aktueller Stand

| Prinzip | Umsetzung | Status |
|---------|-----------|--------|
| Datenminimierung | Keine eigene Datenerhebung | ✅ Erfüllt |
| Speicherbegrenzung | Keine persistente Speicherung | ✅ Erfüllt |
| Integrität | HTTPS erforderlich (Server-Config) | ⚠️ Server-abhängig |
| Vertraulichkeit | Keine sensiblen Daten verarbeitet | ✅ Erfüllt |
| Transparenz | Datenschutzerklärung vorhanden | ✅ Erfüllt |
| Rechenschaftspflicht | Dokumentation vorhanden | ✅ Erfüllt |

### Verbesserungspotential

```
┌─────────────────────────────────────────────────────────────┐
│                PRIVACY BY DESIGN EMPFEHLUNGEN                │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  1. EXTERNE BILDER LOKAL HOSTEN                            │
│     • Pexels-Bilder herunterladen und lokal einbinden      │
│     • Eliminiert IP-Übertragung an pexels.com              │
│                                                             │
│  2. GOOGLE MAPS ERSETZEN                                   │
│     Option A: Statisches Kartenbild + Link                 │
│     Option B: OpenStreetMap Embed (DSGVO-konform)          │
│     Option C: Click-to-Load mit Consent                    │
│                                                             │
│  3. LEADCONNECTORHQ BILD LOKAL HOSTEN                      │
│     • Bild herunterladen: Zeile 1682 in index.html         │
│     • Lokal einbinden                                       │
│                                                             │
│  4. CDN-WEBSITE.COM BILD LOKAL HOSTEN                      │
│     • Bild herunterladen: Zeile 1758 in index.html         │
│     • Lokal einbinden                                       │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

## Server-Sicherheit

### Empfohlene HTTP Security Headers

```apache
# .htaccess oder Server-Konfiguration

# Content Security Policy
Header set Content-Security-Policy "default-src 'self'; \
    style-src 'self' 'unsafe-inline'; \
    script-src 'self' 'unsafe-inline'; \
    img-src 'self' https://images.pexels.com https://images.leadconnectorhq.com https://lirp.cdn-website.com data:; \
    frame-src https://www.google.com/maps/; \
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
⚠️  HINWEIS: Inline JavaScript

Die Website verwendet Inline-JavaScript (Zeile 2011-2087 in index.html).
Dies erfordert 'unsafe-inline' in der CSP.

Risikobewertung: NIEDRIG
- Keine externe Datenverarbeitung
- Keine sensiblen Operationen
- Keine Benutzereingaben verarbeitet
```

### Externe Ressourcen

| Ressource | Risiko | Mitigation |
|-----------|--------|------------|
| Pexels Images | Mittel | SRI nicht möglich (dynamische URLs) |
| Google Maps | Hoch | Click-to-Load oder Ersatz |
| CDN Images | Mittel | Lokal hosten |

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
- [ ] Security Headers gesetzt
- [ ] Datenschutzerklärung aktuell
- [ ] Impressum vollständig
- [ ] [OPTIONAL] Externe Bilder lokal gehostet
- [ ] [OPTIONAL] Google Maps durch Alternative ersetzt
- [ ] [TO BE ADDED] Drittlandübermittlung in Datenschutzerklärung dokumentiert

## Offene Punkte

| ID | Beschreibung | Priorität | Status |
|----|--------------|-----------|--------|
| SEC-001 | Drittlandübermittlung dokumentieren | Hoch | Offen |
| SEC-002 | Google Maps Consent-Lösung | Mittel | Offen |
| SEC-003 | Externe Bilder lokal hosten | Mittel | Offen |
| SEC-004 | Hosting-Anbieter in Datenschutz ergänzen | Hoch | Platzhalter vorhanden |

---

*Dokumentation erstellt: Januar 2026*
*Nächste Überprüfung: [TO BE DEFINED]*
