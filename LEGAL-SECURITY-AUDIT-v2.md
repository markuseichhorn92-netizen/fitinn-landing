# FIT-INN Landing Page - Rechtliches & Sicherheits-Audit v2

**URL:** https://angebot.fit-inn-trier.de  
**Prüfdatum:** 05.02.2026, 23:30 Uhr  
**Vorheriger Audit:** LEGAL-SECURITY-AUDIT.md (05.02.2026)  
**Geprüft von:** JARVIS (automatisiert)

---

## Executive Summary

| Problem | Status vorher | Status jetzt |
|---------|---------------|--------------|
| Widerrufsbelehrung fehlt | ❌ KRITISCH | ✅ **GEFIXT** |
| Button "Zahlungspflichtig bestellen" | ❌ KRITISCH | ✅ **GEFIXT** |
| USt-IdNr fehlt | ❌ KRITISCH | ⚠️ **PLATZHALTER** |
| Handelsregister fehlt | ❌ KRITISCH | ❌ **NOCH OFFEN** |
| Links auf falsche Domain | - | ⚠️ **NEU ENTDECKT** |

**Gesamtbewertung:** 🟡 Kritische Probleme weitgehend behoben, kleinere Nachbesserungen nötig

---

## 1. Behobene Probleme ✅

### 1.1 Widerrufsbelehrung ✅ GEFIXT

**Vorher:** Link führte zu 404, keine Widerrufsseite vorhanden

**Jetzt:**
- ✅ `/widerruf.html` existiert und ist erreichbar
- ✅ Vollständige Widerrufsbelehrung nach BGB-Muster
- ✅ Muster-Widerrufsformular enthalten
- ✅ Folgen des Widerrufs erklärt
- ✅ Besondere Hinweise zu Dienstleistungen
- ✅ Link im Footer vorhanden

**Inhalt geprüft:**
```
✓ 14-Tage Widerrufsfrist genannt
✓ Adresse/Kontakt für Widerruf korrekt
✓ Form der Widerrufserklärung erklärt
✓ Muster-Widerrufsformular vorhanden
✓ Wertersatz bei begonnener Dienstleistung erklärt
✓ Erlöschen des Widerrufsrechts dokumentiert
```

**Bewertung:** ✅ Rechtlich korrekt implementiert

---

### 1.2 Button "Zahlungspflichtig bestellen" ✅ GEFIXT

**Vorher:** Button sagte "Mitglied werden" (Verstoß gegen § 312j Abs. 3 BGB)

**Jetzt:**
- ✅ Finaler Submit-Button im Booking-Modal: **"Zahlungspflichtig bestellen"**
- ✅ Button-ID: `bk-submit-btn`
- ✅ Text wird nach Fehler korrekt wiederhergestellt

**Code-Nachweis (booking-modal.html):**
```html
<button id="bk-submit-btn" onclick="bkSubmit()" class="...">
    Zahlungspflichtig bestellen
</button>
```

**Bewertung:** ✅ Rechtlich konform nach § 312j Abs. 3 BGB

> **Hinweis:** Die Buttons "Mitglied werden" auf der Hauptseite (Navigation, Hero, Footer) sind **nicht kritisch**, da sie nur das Modal öffnen. Der rechtlich relevante **finale Bestell-Button** ist korrekt beschriftet.

---

### 1.3 USt-IdNr im Impressum ⚠️ PLATZHALTER

**Vorher:** Komplett fehlend

**Jetzt:**
```html
<h2>Umsatzsteuer-ID</h2>
<p>Umsatzsteuer-Identifikationsnummer gemäß § 27 a Umsatzsteuergesetz:<br>
DE [wird nachgetragen]</p>
```

**Status:** Struktur vorhanden, aber **echte Nummer fehlt noch**

**Bewertung:** ⚠️ Muss mit echter USt-IdNr gefüllt werden

---

## 2. Noch offene Probleme ❌

### 2.1 Handelsregister-Angaben fehlen ❌ KRITISCH

**Impressum prüft:**
- ✅ Name: Fit-Inn Trier
- ✅ Vertretungsberechtigter: Harald Eichhorn
- ✅ Adresse: Auf Hirtenberg 8, 54296 Trier
- ✅ E-Mail: info@fit-inn-trier.de
- ✅ Telefon: 0651 / 30 85 24
- ✅ Berufshaftpflicht: AXA Versicherung AG
- ✅ DSA-Kontaktstelle
- ✅ OS-Plattform Link
- ⚠️ USt-IdNr: Platzhalter vorhanden
- ❌ **Handelsregister: FEHLT KOMPLETT**

**Rechtliche Anforderung (§ 5 TMG):**
Bei GmbH/eingetragenen Kaufleuten ist Angabe von Registergericht und Registernummer Pflicht!

**Erforderliche Ergänzung:**
```
Handelsregister: Amtsgericht Trier
Registernummer: HRB XXXXX
Geschäftsführer: Harald Eichhorn
```

**Risiko:** Abmahngefahr wegen unvollständigem Impressum

---

### 2.2 Links im Booking-Modal zeigen auf falsche Domain ⚠️ NEU

**Problem entdeckt:** Die Checkboxen im Buchungs-Modal verlinken auf `fit-inn-trier.de` statt `angebot.fit-inn-trier.de`:

```html
<!-- booking-modal.html -->
<a href="https://fit-inn-trier.de/agb">AGB</a>
<a href="https://fit-inn-trier.de/datenschutz">Datenschutzerklärung</a>
<a href="https://fit-inn-trier.de/widerruf">Widerrufsbelehrung</a>
```

**Konsequenz:**
- Wenn fit-inn-trier.de diese Seiten nicht hat → 404-Fehler
- Inkonsistente Nutzererfahrung
- Rechtlich problematisch bei Widerrufsbelehrung

**Empfehlung:** Links ändern zu:
```html
<a href="/agb.html">AGB</a>
<a href="/datenschutz.html">Datenschutzerklärung</a>
<a href="/widerruf.html">Widerrufsbelehrung</a>
```

---

## 3. Gesamtübersicht der rechtlichen Seiten

| Seite | Existiert | Inhalt | Bewertung |
|-------|-----------|--------|-----------|
| `/impressum.html` | ✅ | Grundangaben vorhanden | ⚠️ HRB + USt fehlen |
| `/agb.html` | ✅ | Vollständig, 11 Paragraphen | ✅ Rechtssicher |
| `/datenschutz.html` | ✅ | DSGVO-Grundlagen | ⚠️ Externe Dienste fehlen |
| `/widerruf.html` | ✅ | Vollständig nach BGB-Muster | ✅ Rechtssicher |

### 3.1 AGB-Prüfung ✅

**Enthält:**
- § 1 Geltungsbereich ✅
- § 2 Vertragsschluss ✅
- § 3 Laufzeit & Kündigung ✅ (4 Wochen Frist)
- § 4 Beiträge & Zahlung ✅ (SEPA, 14-tägig, Rücklastschrift)
- § 5 Nutzung ✅
- § 6 Hausordnung ✅
- § 7 Haftung ✅ (differenziert)
- § 8 Ruhen der Mitgliedschaft ✅
- § 9 Datenschutz ✅ (Verweis)
- § 10 Änderungen ✅
- § 11 Schlussbestimmungen ✅

**Stand:** Februar 2026 - aktuell

### 3.2 Datenschutzerklärung ⚠️

**Vorhanden:**
- Verantwortliche Stelle
- Cookie-Hinweise
- Hosting-Hinweise
- Betroffenenrechte (Art. 15-21 DSGVO)
- SSL-Verschlüsselung
- Kontaktformular/E-Mail

**Fehlend:**
- ❌ Google Fonts (fonts.googleapis.com) - Datenübertragung USA
- ❌ Google reCAPTCHA v3 - Tracking/USA
- ❌ Tailwind CDN - externe Ressource
- ❌ Magicline API - Vertragsabwicklung
- ❌ Vercel Hosting - Serverstandort
- ❌ Konkrete Speicherfristen

---

## 4. Cookie-Banner Prüfung ⚠️

**Vorhanden:** Ja

**Implementierung:**
```javascript
// Zwei Optionen:
- "Nur notwendige" (setzt consent = 'necessary')
- "Alle akzeptieren" (setzt consent = 'all')
```

**Positiv:**
- ✅ Consent wird in localStorage gespeichert
- ✅ Tracking nur bei "all" Consent
- ✅ Banner erscheint bei erstem Besuch

**Verbesserungsbedarf:**
- ⚠️ Kein "Alle ablehnen" Button
- ⚠️ Keine granulare Kategorieauswahl
- ⚠️ Kein Cookie-Präferenz-Center
- ⚠️ Link zu Datenschutz im Banner zeigt auf `/datenschutz` (ohne .html)

---

## 5. Buchungsstrecke (#mitgliedschaft Modal)

### 5.1 Checkboxen vor Abschluss ✅

```html
☑️ AGB + Datenschutz akzeptieren
☑️ SEPA-Lastschriftmandat erteilen
☑️ Widerrufsbelehrung gelesen
```

**Bewertung:** Alle erforderlichen Einwilligungen vorhanden ✅

### 5.2 Submit-Button ✅

```html
<button>Zahlungspflichtig bestellen</button>
```

**Bewertung:** § 312j Abs. 3 BGB konform ✅

### 5.3 Altersvalidierung ✅

```javascript
// Prüft auf 18+ Jahre
if (age < 18) {
    "Du musst mindestens 18 Jahre alt sein..."
}
```

**Bewertung:** Jugendschutz korrekt implementiert ✅

---

## 6. Sicherheitsprüfung (kurz)

| Aspekt | Status |
|--------|--------|
| HTTPS/SSL | ✅ Let's Encrypt, gültig |
| HSTS | ✅ 2 Jahre max-age |
| reCAPTCHA | ✅ v3 implementiert |
| IBAN-Validierung | ✅ Client-seitig |
| Sensible Daten in localStorage | ✅ Keine |
| CSRF-Token | ⚠️ Nicht sichtbar |
| CSP-Header | ❌ Fehlt |

---

## 7. Maßnahmenplan

### 🔴 SOFORT (kritisch)

| # | Maßnahme | Aufwand |
|---|----------|---------|
| 1 | **Handelsregister-Angaben** in Impressum ergänzen | 5 min |
| 2 | **USt-IdNr** echte Nummer eintragen (DE...) | 5 min |
| 3 | **Links im Booking-Modal** auf relative Pfade ändern | 10 min |

### 🟡 ZEITNAH (Abmahnrisiko)

| # | Maßnahme | Aufwand |
|---|----------|---------|
| 4 | Datenschutzerklärung erweitern (Google Fonts, reCAPTCHA, Vercel) | 30 min |
| 5 | Cookie-Banner: "Alle ablehnen" Button hinzufügen | 15 min |
| 6 | Cookie-Link von `/datenschutz` auf `/datenschutz.html` ändern | 2 min |

### 🟢 EMPFOHLEN (Best Practice)

| # | Maßnahme | Aufwand |
|---|----------|---------|
| 7 | CSP-Header konfigurieren (Vercel) | 30 min |
| 8 | Externe Ressourcen selbst hosten (Tailwind, Fonts) | 2h |
| 9 | Cookie-Präferenz-Center implementieren | 2h |

---

## 8. Fazit

### Was wurde erfolgreich gefixt? ✅

1. **Widerrufsbelehrung** - Vollständig implementiert unter `/widerruf.html`
2. **Button "Zahlungspflichtig bestellen"** - Korrekter Text im Submit-Button
3. **USt-IdNr Struktur** - Abschnitt im Impressum vorhanden

### Was ist noch offen? ⚠️

1. **Handelsregister** - Muss mit echten Daten ergänzt werden
2. **USt-IdNr** - Muss mit echter Nummer gefüllt werden
3. **Links im Modal** - Verweisen auf falsche Domain
4. **Datenschutzerklärung** - Externe Dienste nicht dokumentiert

### Rechtliche Einschätzung

Die **kritischsten Probleme** (Widerrufsbelehrung, Button-Text) wurden behoben. 

Die **verbleibenden Punkte** (Handelsregister, USt-IdNr) sind **Impressumspflichten** und sollten zeitnah ergänzt werden, stellen aber ein geringeres Abmahnrisiko dar als die bereits behobenen Mängel.

**Empfehlung:** Die 3 SOFORT-Maßnahmen können in 20 Minuten erledigt werden und schließen die letzten kritischen Lücken.

---

## Änderungshistorie

| Version | Datum | Änderungen |
|---------|-------|------------|
| v1 | 05.02.2026 | Erstaudit - 3 kritische Probleme identifiziert |
| v2 | 05.02.2026 | Re-Audit - 2 von 3 kritischen Problemen behoben |

---

*Audit durchgeführt am 05.02.2026, 23:30 Uhr - Dieser Report ersetzt keine Rechtsberatung.*
