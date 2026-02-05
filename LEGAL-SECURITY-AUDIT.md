# FIT-INN Landing Page - Rechtliches & Sicherheits-Audit

**URL:** https://angebot.fit-inn-trier.de  
**Prüfdatum:** 05.02.2026  
**Geprüft von:** JARVIS (automatisiert)

---

## Zusammenfassung

| Kategorie | Status |
|-----------|--------|
| DSGVO-Konformität | ⚠️ Verbesserungsbedarf |
| Impressum | ✅ Korrekt |
| Widerrufsrecht | ❌ **KRITISCH** |
| Preisangaben | ✅ Korrekt |
| AGB | ✅ Vorhanden & rechtssicher |
| Vertragsschluss | ⚠️ Verbesserungsbedarf |
| Jugendschutz | ✅ Implementiert |
| SSL/HTTPS | ✅ Korrekt |
| Formularsicherheit | ⚠️ Verbesserungsbedarf |
| Datensicherheit | ✅ Grundlegend ok |

---

## 1. Rechtliche Prüfung

### 1.1 DSGVO-Konformität

#### ✅ Datenschutzerklärung
- **Vorhanden:** Ja, unter `/datenschutz.html`
- **Inhalt:** Grundlegende DSGVO-Elemente enthalten
- **Aktualisierung:** Februar 2026

#### ⚠️ Cookie-Banner
- **Vorhanden:** Ja, mit zwei Optionen
- **Optionen:** "Nur notwendige" und "Alle akzeptieren"
- **Problem:** 
  - Kein "Ablehnen" Button (nur "Nur notwendige")
  - Keine granulare Auswahl einzelner Cookie-Kategorien
  - Kein Cookie-Präferenz-Center

**Empfehlung:** 
```
- Expliziten "Alle ablehnen" Button hinzufügen
- Cookie-Präferenz-Center mit Kategorien implementieren
- Opt-out muss genauso einfach sein wie Opt-in
```

#### ⚠️ Datenschutzerklärung - Fehlende Angaben
Folgende Pflichtangaben fehlen oder sind unvollständig:

1. **Verantwortliche Stelle:** Adresse/Kontaktdaten fehlen im Text
2. **Datenschutzbeauftragter:** Nicht genannt (bei >20 MA erforderlich)
3. **Google Fonts:** Werden geladen (fonts.googleapis.com), aber nicht dokumentiert
4. **reCAPTCHA:** Wird verwendet, aber nicht dokumentiert
5. **Externe APIs:** Magicline API, Backend-Server (srv1309486.hstgr.cloud) nicht dokumentiert
6. **Speicherdauer:** Keine konkreten Fristen genannt
7. **Rechtsgrundlage:** Art. 6 DSGVO nicht für jeden Verarbeitungszweck genannt

**Empfehlung:**
```markdown
Ergänze in der Datenschutzerklärung:
- Vollständige Kontaktdaten des Verantwortlichen
- Google Fonts (externer Aufruf = Datenübertragung in USA)
- Google reCAPTCHA v3 (Datenübertragung in USA)
- Magicline (Vertragsabwicklung, AVV prüfen)
- Hosting bei Vercel (USA, Datentransfer)
- Konkrete Speicherfristen für alle Datenkategorien
```

#### ⚠️ Einwilligungen
- **Lead-Capture:** Keine explizite Checkbox für Marketingkontakt
- **WhatsApp-Bestätigung:** "Du erhältst sofort eine Bestätigung per WhatsApp" - ohne Einwilligung
- **Datenschutz-Checkbox:** Nur bei Probetraining vorhanden, nicht bei Lead-Capture

**❌ PROBLEM:** Bei Leads werden Name, E-Mail, Telefon erfasst und automatisch WhatsApp gesendet - ohne explizite Einwilligung!

**Empfehlung:**
```
- Checkbox hinzufügen: "Ich willige ein, Bestätigungen per WhatsApp zu erhalten"
- Datenschutz-Checkbox bei allen Formularen
- Double-Opt-In für Newsletter/Marketing implementieren
```

---

### 1.2 Impressumspflicht (§5 TMG)

#### ✅ Vollständiges Impressum

| Pflichtangabe | Status |
|--------------|--------|
| Unternehmensname | ✅ Fit-Inn Trier |
| Rechtsform | ⚠️ Im Text "GmbH", im Impressum fehlt |
| Vertretungsberechtigter | ✅ Harald Eichhorn |
| Adresse | ✅ Auf Hirtenberg 8, 54296 Trier |
| E-Mail | ✅ info@fit-inn-trier.de |
| Telefon | ✅ 0651 / 30 85 24 |
| Handelsregister | ❌ **FEHLT** |
| USt-IdNr | ❌ **FEHLT** |
| Berufshaftpflicht | ✅ AXA Versicherung AG |
| DSA-Kontaktstelle | ✅ Vorhanden |
| OS-Plattform | ✅ Link vorhanden |
| Streitschlichtung | ✅ Hinweis vorhanden |

**❌ KRITISCH:**
- **Handelsregister-Angaben fehlen** (bei GmbH Pflicht!)
- **USt-IdNr fehlt** (bei gewerblicher Tätigkeit Pflicht)

**Empfehlung:**
```markdown
Ergänze im Impressum:
- Handelsregister: Amtsgericht Trier, HRB xxxxx
- Geschäftsführer: Harald Eichhorn (falls GmbH)
- USt-IdNr: DE xxxxxxxxx
```

---

### 1.3 Widerrufsrecht (§312g BGB)

#### ❌ KRITISCH - WIDERRUFSBELEHRUNG FEHLT!

Bei Online-Vertragsabschlüssen mit Verbrauchern ist eine Widerrufsbelehrung **gesetzlich vorgeschrieben**.

**Feststellungen:**
1. **Widerrufsbelehrung verlinkt:** Ja, aber Link führt zu 404!
   - `https://fit-inn-trier.de/widerruf` → "Page not found"
2. **Keine separate Widerrufsseite** auf angebot.fit-inn-trier.de
3. **FAQ erwähnt 14 Tage Widerrufsrecht**, aber keine formelle Belehrung
4. **Checkbox vorhanden:** "Ich habe die Widerrufsbelehrung gelesen" → Link kaputt!

**Rechtliche Konsequenz:**
- Verlängerung der Widerrufsfrist auf **12 Monate + 14 Tage**
- Abmahnrisiko
- Kunden können alle Verträge innerhalb eines Jahres widerrufen

**SOFORTMASSNAHME ERFORDERLICH:**
```markdown
1. Erstelle /widerruf.html mit vollständiger Widerrufsbelehrung:
   - Widerrufsrecht (14 Tage nach Vertragsschluss)
   - Ausnahmen (z.B. begonnene Dienstleistung mit Verzichtserklärung)
   - Widerrufsformular
   - Folgen des Widerrufs
   
2. Oder verlinke auf fit-inn-trier.de/widerruf (muss dort existieren!)

3. Füge SEPA-Lastschrift-Widerrufsfrist hinzu (8 Wochen)
```

**Muster-Widerrufsbelehrung:**
```html
<h2>Widerrufsbelehrung</h2>
<h3>Widerrufsrecht</h3>
<p>Sie haben das Recht, binnen vierzehn Tagen ohne Angabe von Gründen diesen Vertrag zu widerrufen.</p>
<p>Die Widerrufsfrist beträgt vierzehn Tage ab dem Tag des Vertragsabschlusses.</p>
<p>Um Ihr Widerrufsrecht auszuüben, müssen Sie uns (FIT-INN Trier GmbH, Auf Hirtenberg 8, 54296 Trier, 
E-Mail: info@fit-inn-trier.de, Tel: 0651/308524) mittels einer eindeutigen Erklärung 
(z. B. ein mit der Post versandter Brief oder E-Mail) über Ihren Entschluss, diesen Vertrag zu widerrufen, informieren.</p>
...
```

---

### 1.4 Preisangabenverordnung (PAngV)

#### ✅ Preise korrekt ausgezeichnet

| Anforderung | Status |
|-------------|--------|
| Bruttopreise | ✅ "Sämtliche Beiträge enthalten die gesetzliche Mehrwertsteuer" |
| Einmalige Kosten | ✅ "39€ Startpaket einmalig" klar angegeben |
| Wiederkehrende Kosten | ✅ "12€/Woche", "9€/Woche" |
| Preisänderung bei Aktion | ✅ "Ab 01.04.2026: X€/Woche" deutlich angezeigt |
| Zahlungsrhythmus | ✅ "Alle 14 Tage" angegeben |
| Laufzeit | ✅ 52/104 Wochen klar kommuniziert |

**Positiv:**
- Aktionspreis und Normalpreis nebeneinander
- Preisänderungsdatum klar genannt
- Zusatzkosten (Startpaket) transparent

---

### 1.5 AGB

#### ✅ Vorhanden und rechtssicher

**Enthaltene Regelungen:**
- § 1 Geltungsbereich ✅
- § 2 Vertragsschluss ✅ (inkl. Online-Anmeldung)
- § 3 Vertragslaufzeit & Kündigung ✅ (4 Wochen Frist, Textform)
- § 4 Beiträge & Zahlung ✅ (SEPA, 14-tägig)
- § 5 Nutzung ✅
- § 6 Hausordnung ✅
- § 7 Haftung ✅ (differenziert nach Verschuldensgrad)
- § 8 Ruhen der Mitgliedschaft ✅
- § 9 Datenschutz ✅ (Verweis auf DSE)
- § 10 Änderungen ✅ (6 Wochen Widerspruchsfrist)
- § 11 Schlussbestimmungen ✅

**⚠️ Verbesserungspotenzial:**
- Kein Hinweis auf Widerrufsrecht in AGB
- Kein Hinweis auf außerordentliche Kündigung bei Beitragserhöhung
- Keine Regelung zu "höherer Gewalt" (Pandemie, Schließungen)

---

### 1.6 Vertragsschluss-Prozess

#### ⚠️ Verbesserungsbedarf

**Buchungsstrecke (Mitgliedschaft):**
1. Lead-Capture (Name, E-Mail, Telefon) ⚠️
2. Tarifauswahl ✅
3. Optionale Module ✅
4. Persönliche Daten ✅
5. Adresse ✅
6. Bankdaten (IBAN) ✅
7. Zusammenfassung + Checkboxen ⚠️
8. Bestätigung ✅

**Erhobene Daten:**
- Name, Vorname, Nachname
- E-Mail, Telefon
- Geburtsdatum, Geschlecht
- Vollständige Adresse
- Kontoinhaber, IBAN

**Checkboxen vor Abschluss:**
- ✅ AGB + Datenschutz
- ✅ SEPA-Mandat
- ❌ Widerrufsbelehrung (Link kaputt!)

**Probleme:**
1. **Button-Text:** "Mitglied werden" statt "Zahlungspflichtig bestellen" (§ 312j BGB)
2. **Widerrufsbelehrung-Link:** 404-Fehler
3. **Keine Checkbox für Ausdrücklichen Beginn der Dienstleistung** vor Ablauf der Widerrufsfrist

**Empfehlung:**
```markdown
1. Button-Text ändern zu: "Zahlungspflichtig bestellen" oder 
   "Kostenpflichtigen Vertrag abschließen"

2. Checkbox hinzufügen:
   "Ich stimme zu, dass die Dienstleistung sofort beginnt, und nehme zur 
   Kenntnis, dass ich mein Widerrufsrecht verliere, sobald der Vertrag 
   vollständig erfüllt ist."

3. Widerrufsbelehrung-Link reparieren
```

---

### 1.7 Newsletter/Marketing

#### ⚠️ Kein Double-Opt-In erkennbar

**Feststellungen:**
- Kein klassisches Newsletter-Formular auf der Seite
- Lead-Capture sendet automatisch WhatsApp-Bestätigung
- Keine separate Marketing-Einwilligung

**Problem:** 
WhatsApp-Nachrichten an erfasste Leads ohne explizite Einwilligung = **Verstoß gegen UWG § 7 (unzumutbare Belästigung)**

**Empfehlung:**
```markdown
1. Separate Checkbox: "Ich möchte Angebote per WhatsApp/E-Mail erhalten"
2. Double-Opt-In für Newsletter implementieren
3. Bestätigungs-WhatsApp nur nach expliziter Zustimmung
```

---

### 1.8 Jugendschutz

#### ✅ Korrekt implementiert

**Implementierung:**
- Geburtsdatum-Abfrage mit Jahr ab "aktuelles Jahr - 16"
- **Altersvalidierung:** `bkValidateAgeAndContinue()` prüft auf 18+
- Fehlermeldung: "Du musst mindestens 18 Jahre alt sein, um einen Vertrag abzuschließen"
- AGB § 2 (4): "Minderjährige benötigen die schriftliche Einwilligung eines Erziehungsberechtigten"

**⚠️ Verbesserung:**
- Keine Option für Minderjährige mit Einwilligung online
- Bei Probetraining keine Altersprüfung (könnte problematisch sein)

---

## 2. Sicherheitstechnische Prüfung

### 2.1 HTTPS/SSL

#### ✅ Korrekt implementiert

| Prüfpunkt | Status |
|-----------|--------|
| HTTPS aktiv | ✅ Ja |
| Zertifikat gültig | ✅ Let's Encrypt, gültig bis 06.05.2026 |
| HSTS | ✅ `max-age=63072000` (2 Jahre) |
| Redirect HTTP→HTTPS | ✅ Ja |

**SSL Details:**
- **Aussteller:** Let's Encrypt R13
- **Gültig:** 05.02.2026 - 06.05.2026
- **Subject:** CN=angebot.fit-inn-trier.de

---

### 2.2 Formulare

#### ⚠️ Teilweise sicher

**Positiv:**
- ✅ reCAPTCHA v3 implementiert (`6Lf42WEsAAAAAJklBBd1adX2vCMeR6AnfQUE6Ve_`)
- ✅ IBAN-Validierung (Länge, Format, DE-Prüfung)
- ✅ E-Mail-Validierung (enthält @)
- ✅ Telefon-Formatierung
- ✅ Pflichtfelder markiert

**Probleme:**
- ❌ **Kein CSRF-Token sichtbar** in den Formularen
- ⚠️ Client-seitige Validierung kann umgangen werden
- ⚠️ Keine Rate-Limiting erkennbar

**Empfehlung:**
```markdown
1. CSRF-Token bei allen POST-Requests implementieren
2. Server-seitige Validierung aller Eingaben sicherstellen
3. Rate-Limiting für API-Endpoints (Lead-Capture, Booking)
4. Input-Sanitization gegen XSS
```

---

### 2.3 Externe Ressourcen

#### ⚠️ Mehrere externe Einbindungen

| Ressource | Domain | Risiko |
|-----------|--------|--------|
| Tailwind CSS | cdn.tailwindcss.com | ⚠️ CDN-Abhängigkeit |
| Google Fonts | fonts.googleapis.com | ⚠️ Tracking-Risiko |
| Google reCAPTCHA | google.com/recaptcha | ⚠️ Tracking |
| Backend API | srv1309486.hstgr.cloud | ✅ Eigener Server |
| Magicline API | fit-inn-trier.api.magicline.com | ✅ Vertragspartner |

**Empfehlungen:**
```markdown
1. Tailwind CSS lokal hosten (Build-Zeit kompilieren)
2. Google Fonts: Self-hosting oder system fonts
3. Subresource Integrity (SRI) für externe Scripts hinzufügen
4. Content-Security-Policy Header setzen
```

---

### 2.4 API-Endpoints

#### ⚠️ Prüfung eingeschränkt möglich

**Identifizierte Endpoints:**
1. `https://srv1309486.hstgr.cloud/api/leads` - Lead-Capture
2. `https://srv1309486.hstgr.cloud/api/probetraining` - Probetraining
3. `https://srv1309486.hstgr.cloud/api/probetraining/slots` - Verfügbare Termine
4. `https://srv1309486.hstgr.cloud/api/track` - Analytics
5. `https://fit-inn-trier.api.magicline.com/connect/v1/rate-bundle` - Vertragsabschluss

**Sicherheitsaspekte:**
- ✅ HTTPS für alle Endpoints
- ✅ reCAPTCHA-Token bei Vertragsabschluss
- ⚠️ Tracking-API ohne Authentifizierung
- ⚠️ Leads-API ohne Rate-Limiting sichtbar

---

### 2.5 Datenspeicherung

#### ✅ Grundlegend sicher

**Feststellungen:**
- LocalStorage für Session-Tracking (`fitinn_session`)
- LocalStorage für Cookie-Consent (`cookie_consent`)
- Keine sensiblen Daten in LocalStorage
- IBAN wird nur bei Absenden übertragen, nicht gespeichert

**⚠️ Beachten:**
- Session-Daten enthalten UTM-Parameter, Events, Timestamps
- Bei Consent=all werden Events geloggt

---

### 2.6 Third-Party Scripts

#### ⚠️ Dokumentationsbedarf

| Script | Zweck | DSGVO-konform dokumentiert? |
|--------|-------|----------------------------|
| Google reCAPTCHA v3 | Bot-Schutz | ❌ Nein |
| Google Fonts | Schriftarten | ❌ Nein |
| Tailwind CDN | Styling | ❌ Nein |
| Eigenes Tracking | Analytics | ⚠️ Teilweise |

**Keine externen Analytics-Tools erkennbar:**
- ✅ Kein Google Analytics
- ✅ Kein Facebook Pixel
- ✅ Kein Google Tag Manager
- ✅ Eigenes Tracking (consent-basiert)

---

## 3. Buchungsstrecken-Analyse

### 3.1 Probetraining Modal (#probetraining)

**Schritte:**
1. **Lead-Capture** (Schritt 0): Name, E-Mail, Telefon
2. **Fitnessziel** (Schritt 1): Abnehmen/Fitness/Gesundheit/Muskelaufbau
3. **Begleitung** (Schritt 2): Freund mitbringen Ja/Nein
4. **Trainer** (Schritt 3): Mit/Ohne Trainer
5. **Terminauswahl** (Schritt 4): Kalender + Uhrzeiten
6. **Persönliche Daten** (Schritt 5): Vorname, Nachname, E-Mail, Telefon, Geburtsdatum, Anrede
7. **Adresse** (Schritt 6): PLZ, Stadt, Straße, Hausnummer
8. **Bestätigung** (Schritt 7): Zusammenfassung

**Erhobene Daten:**
- Name (doppelt: Lead + Formular)
- E-Mail (doppelt)
- Telefon (doppelt)
- Geburtsdatum
- Anrede
- Vollständige Adresse
- Fitnessziel
- Trainer-Präferenz

**Rechtliche Bewertung:**
- ⚠️ Datenschutz-Checkbox vorhanden
- ⚠️ Mehr Daten als für Probetraining nötig (Adresse?)
- ✅ Geburtsdatum für Alter-Check sinnvoll

### 3.2 Mitgliedschaft Modal (#mitgliedschaft / #booking)

**Schritte:**
1. **Lead-Capture** (Schritt 0): Name, E-Mail, Telefon
2. **Tarifauswahl** (Schritt 1): 3 Optionen
3. **Module** (Schritt 2): Optionale Upgrades
4. **Persönliche Daten** (Schritt 3): Vorname, Nachname, E-Mail, Telefon, Geburtsdatum, Anrede
5. **Adresse** (Schritt 4): Straße, Nr., PLZ, Stadt
6. **Bankdaten** (Schritt 5): Kontoinhaber, IBAN
7. **Zusammenfassung** (Schritt 6): Checkboxen + Bestätigung
8. **Willkommen** (Schritt 7): Erfolgsmeldung

**Erhobene Daten:**
- Alle persönlichen Daten
- Vollständige Adresse
- Bankverbindung (IBAN)
- Tarif-/Vertragswahl

**Rechtliche Bewertung:**
- ❌ Widerrufsbelehrung-Link kaputt
- ⚠️ Button "Mitglied werden" statt "Zahlungspflichtig bestellen"
- ✅ Altersvalidierung (18+)
- ✅ SEPA-Mandat-Checkbox

---

## 4. Kritische Maßnahmen (Priorität)

### ❌ SOFORT beheben (rechtlich kritisch)

1. **Widerrufsbelehrung erstellen/verlinken**
   - `/widerruf.html` anlegen ODER
   - Link auf fit-inn-trier.de/widerruf prüfen
   - 12 Monate Widerrufsfrist droht sonst!

2. **Impressum vervollständigen**
   - Handelsregisternummer ergänzen
   - USt-IdNr ergänzen

3. **Button-Beschriftung ändern**
   - "Mitglied werden" → "Zahlungspflichtig bestellen"

### ⚠️ ZEITNAH beheben (Abmahnrisiko)

4. **Datenschutzerklärung erweitern**
   - Google Fonts, reCAPTCHA dokumentieren
   - Vercel-Hosting dokumentieren
   - Magicline-Integration dokumentieren
   - Konkrete Speicherfristen nennen

5. **Cookie-Banner verbessern**
   - Granulare Auswahl ermöglichen
   - Cookie-Präferenz-Center

6. **WhatsApp-Einwilligung**
   - Explizite Checkbox vor automatischem Versand

7. **Checkbox für sofortigen Dienstleistungsbeginn**
   - Bei Widerrufsverzicht

### 💡 EMPFOHLEN (Best Practices)

8. **CSRF-Schutz implementieren**
9. **Rate-Limiting für APIs**
10. **CSP-Header setzen**
11. **Externe Ressourcen selbst hosten**
12. **Datenschutz-Checkbox bei allen Formularen**

---

## 5. Technische Details

### Header-Analyse

```
HTTP/2 200 
strict-transport-security: max-age=63072000
x-vercel-cache: HIT
content-type: text/html; charset=utf-8
```

### Security Meta-Tags

```html
<meta http-equiv="X-Content-Type-Options" content="nosniff">
<meta name="referrer" content="strict-origin-when-cross-origin">
```

**Fehlend:**
- `Content-Security-Policy`
- `X-Frame-Options`
- `X-XSS-Protection`

### SSL-Zertifikat

```
Subject: CN=angebot.fit-inn-trier.de
Issuer: Let's Encrypt R13
Valid: 05.02.2026 - 06.05.2026
```

---

## Fazit

Die Landing Page ist **technisch gut umgesetzt** und erfüllt viele Anforderungen. Es gibt jedoch **kritische rechtliche Mängel**, die dringend behoben werden müssen:

1. **Fehlende/defekte Widerrufsbelehrung** ist das gravierendste Problem
2. **Unvollständiges Impressum** (Handelsregister, USt-IdNr)
3. **Datenschutzerklärung unvollständig** (externe Dienste)

Nach Behebung dieser Punkte ist die Seite rechtlich auf sicherem Grund.

---

*Audit durchgeführt am 05.02.2026 - Dieser Report ersetzt keine Rechtsberatung.*
