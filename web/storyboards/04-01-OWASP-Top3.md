# Video-Storyboard: OWASP Top 3 Sicherheitsrisiken

**Dauer:** ca. 8-10 Minuten  
**Zielgruppe:** 1. Lehrjahr Applikationsentwicklung  
**Lernziele:** OWASP verstehen, Top 3 Risiken kennen, Sicherheitsbewusstsein entwickeln

---

## INTRO (40 Sekunden)

### Szene 1: Titel-Animation

**Dauer:** 10 Sekunden  
**Visuell:** 
- BAND Design: Blauer Hintergrund mit Türkis-Akzenten
- Titel einblenden: "OWASP Top 3 Sicherheitsrisiken"
- Untertitel: "Webmodul – Diverses"

**Sprechertext:** *[keine]*

**Technische Notizen:**
- Hintergrundfarbe: `#005a73` (Blau 900)
- Titelfarbe: `#FFFFFF`
- Akzentfarbe: `#4eb9cc` (Türkis 700)
- Font: Aptos Bold
- Animation: Fade in + leichter Zoom

---

### Szene 2: Einstieg
**Dauer:** 30 Sekunden  
**Visuell:**
- Bildschirm zeigt eine simple Login-Seite
- Hacker-Symbol (Schloss-Icon mit Warnung) einblenden

**Sprechertext:**  
"Willkommen zum Video über Web-Sicherheit. Stell dir vor, du entwickelst eine Webanwendung – eine Portfolio-Seite mit Login-Bereich. Aber was, wenn jemand ohne Berechtigung auf deine Admin-Seite zugreifen kann? Oder Passwörter unverschlüsselt gespeichert werden? Genau hier kommt OWASP ins Spiel. In diesem Video lernst du die drei häufigsten Sicherheitsrisiken kennen und wie du sie vermeidest."

**Technische Notizen:**
- Demo-Login-Seite vorbereiten (HTML-Datei)
- Icon: Font Awesome `fas fa-shield-alt` oder `fas fa-lock-open`

---

## HAUPTTEIL: OWASP ERKLÄREN (1 Min 20 Sek)

### Szene 3: Was ist OWASP?
**Dauer:** 40 Sekunden  
**Visuell:**
- Browser öffnet: `https://owasp.org`
- Scrollt zur Top 10 Liste
- Zeigt OWASP Logo

**Sprechertext:**  
"OWASP steht für Open Web Application Security Project – eine gemeinnützige Organisation, die sich für sichere Softwareentwicklung einsetzt. Sie veröffentlicht regelmässig die OWASP Top 10 – eine Liste der kritischsten Sicherheitsrisiken für Webanwendungen. Diese Liste basiert auf echten Daten aus der ganzen Welt und hilft Entwicklern, die häufigsten Fehler zu vermeiden. Wir konzentrieren uns heute auf die Top 3."

**Technische Notizen:**
- OWASP-Webseite im Browser öffnen
- Navigation zu: "OWASP Top 10" Bereich
- Screenshot vorbereiten falls Website nicht verfügbar

**Zu zeigen/vorbereiten:**
- OWASP Website: https://owasp.org/www-project-top-ten/
- Screenshot der Top 10 Liste (2021 oder neuer)

---

### Szene 4: Die Top 3 im Überblick
**Dauer:** 40 Sekunden  
**Visuell:**
- Folie mit 3 Säulen (oder Karten)
- Jede Säule eine Farbe:
  - Broken Access Control (Orange)
  - Cryptographic Failures (Türkis)
  - Injection (Blau)

**Sprechertext:**  
"Die Top 3 Risiken sind: Erstens, Broken Access Control – das bedeutet, fehlerhafte Zugriffskontrolle. Zweitens, Cryptographic Failures – also kryptographische Fehler bei der Verschlüsselung. Und drittens, Injection – das Einschleusen von Schadcode. Diese drei Risiken sind für die meisten Sicherheitsvorfälle verantwortlich. Schauen wir uns jedes einzeln genauer an."

**Technische Notizen:**
- PowerPoint/HTML-Folie erstellen mit 3 Cards
- Card 1: Orange 700 `#f5a623`
- Card 2: Türkis 700 `#4eb9cc`
- Card 3: Blau 700 `#005a73`
- Jede Card: Icon + Nummer + Titel

**HTML-Demo vorbereiten:**
```html
<div class="risiko-cards">
    <div class="card orange">
        <h3>1. Broken Access Control</h3>
        <p>Fehlerhafte Zugriffskontrolle</p>
    </div>
    <div class="card turquoise">
        <h3>2. Cryptographic Failures</h3>
        <p>Kryptographische Fehler</p>
    </div>
    <div class="card blue">
        <h3>3. Injection</h3>
        <p>Einschleusung von Schadcode</p>
    </div>
</div>
```

---

## TEIL 1: BROKEN ACCESS CONTROL (2 Min 30 Sek)

### Szene 5: Was ist Broken Access Control?
**Dauer:** 45 Sekunden  
**Visuell:**
- Portfolio-Website mit Profilseite
- URL zeigt: `/profil?user=123`
- URL wird geändert zu: `/profil?user=124`
- Zugriff auf fremdes Profil möglich!

**Sprechertext:**  
"Beginnen wir mit Broken Access Control – dem häufigsten Sicherheitsproblem. Es bedeutet, dass Nutzer auf Bereiche zugreifen können, für die sie keine Berechtigung haben. Ein einfaches Beispiel: Deine Portfolio-Seite hat eine Profilseite. Die URL lautet: profil?user=123. Was passiert, wenn jemand einfach die Nummer ändert zu user=124? Wenn deine Anwendung nicht prüft, ob der eingeloggte Nutzer auch wirklich Nutzer 124 ist, kann er fremde Profile sehen und bearbeiten. Das ist Broken Access Control."

**Technische Notizen:**
- Demo-Website vorbereiten: simple Portfolio-Seite
- Zwei User-Accounts anlegen (123 und 124)
- Browser DevTools öffnen, um URL-Änderung zu zeigen

**Demo-Dateien vorbereiten:**
- `demo-profil.html` (mit URL-Parameter Anzeige)
- Zwei Profile mit unterschiedlichen Daten

---

### Szene 6: Realbeispiel – Admin-Zugang
**Dauer:** 35 Sekunden  
**Visuell:**
- Browser zeigt normale Nutzer-Ansicht
- URL wird zu `/admin` geändert
- Admin-Panel erscheint ohne Login-Prüfung!

**Sprechertext:**  
"Ein noch kritischeres Beispiel: Stell dir vor, deine Website hat einen Admin-Bereich unter /admin. Wenn du nicht prüfst, ob der Besucher auch wirklich Administrator ist, kann jeder einfach /admin in die URL eingeben und vollen Zugriff erhalten. So könnten Angreifer Daten löschen, Nutzer verwalten oder die gesamte Website manipulieren."

**Technische Notizen:**
- Admin-Panel Demo vorbereiten (einfaches HTML)
- Zeige URL-Eingabe im Browser
- Rote Warnung einblenden: "GEFAHR!"

**Demo-Datei:**
- `admin-panel.html` (mit Nutzerverwaltung, Statistiken etc.)

---

### Szene 7: Wie verhindere ich das?
**Dauer:** 1 Min 10 Sek  
**Visuell:**
- Code-Editor mit Beispielcode
- Zeigt `if`-Statements für Berechtigungsprüfung
- Flowchart: "User eingeloggt?" → "Ist Admin?" → "Zugriff erlaubt"

**Sprechertext:**  
"Wie verhindert man Broken Access Control? Erstens: Prüfe bei jeder Anfrage die Berechtigung des Nutzers – nicht nur beim Login. Zweitens: Verwende eine Whitelist – erlaube nur bestimmte Zugriffe, blockiere alles andere standardmässig. Drittens: Verlasse dich nie auf die URL oder Client-seitige Prüfungen. Die Prüfung muss immer auf dem Server passieren. Und viertens: Teste regelmässig mit verschiedenen Nutzerrollen, ob jemand auf Bereiche zugreifen kann, die er nicht sollte."

**Technische Notizen:**
- Pseudocode oder JavaScript-Beispiel vorbereiten
- Flowchart als Grafik einblenden
- Best Practices Liste anzeigen

**Code-Beispiel vorbereiten:**
```javascript
// SCHLECHT - Keine Prüfung
function zeigeProfil(userId) {
    return datenbank.getProfil(userId);
}

// GUT - Mit Berechtigungsprüfung
function zeigeProfil(userId, aktuellerNutzer) {
    if (aktuellerNutzer.id !== userId && !aktuellerNutzer.istAdmin) {
        return "Zugriff verweigert!";
    }
    return datenbank.getProfil(userId);
}
```

---

## TEIL 2: CRYPTOGRAPHIC FAILURES (2 Min 30 Sek)

### Szene 8: Was sind Cryptographic Failures?
**Dauer:** 40 Sekunden  
**Visuell:**
- Browser zeigt Login-Formular
- DevTools Network-Tab offen
- Passwort wird im Klartext übertragen!

**Sprechertext:**  
"Weiter geht's mit Cryptographic Failures – kryptographischen Fehlern. Das bedeutet, sensible Daten werden nicht oder falsch verschlüsselt. Ein klassisches Beispiel: Du gibst dein Passwort in einem Login-Formular ein. Wenn die Website nur HTTP statt HTTPS nutzt, wird das Passwort im Klartext übertragen – jeder im gleichen Netzwerk kann es mitlesen. Das ist ein kryptographischer Fehler."

**Technische Notizen:**
- Demo-Login über HTTP vorbereiten
- Browser DevTools Network-Tab zeigen
- Passwort im Klartext sichtbar machen (rot markieren)

**Demo vorbereiten:**
- HTTP-Server starten (ohne SSL)
- Login-Formular mit `method="POST"`
- Network-Tab zeigt Request mit sichtbarem Passwort

---

### Szene 9: Weitere Beispiele
**Dauer:** 50 Sekunden  
**Visuell:**
- Datenbank-Tabelle mit Passwörtern
- Spalte "Passwort" zeigt Klartext: `"password123"`
- Vergleich mit gehashtem Passwort

**Sprechertext:**  
"Ein weiteres Problem: Passwörter, die unverschlüsselt in der Datenbank gespeichert werden. Wenn ein Angreifer Zugriff auf deine Datenbank bekommt, kann er sofort alle Passwörter lesen. Oder: Sensible Daten wie Kreditkartennummern oder Gesundheitsdaten werden ohne Verschlüsselung gespeichert. Auch veraltete oder schwache Verschlüsselungsmethoden fallen unter Cryptographic Failures – etwa MD5, das heute als unsicher gilt."

**Technische Notizen:**
- Zwei Datenbank-Ansichten vorbereiten:
  - SCHLECHT: Klartext-Passwörter
  - GUT: Gehashte Passwörter (bcrypt)
- Vergleichstabelle einblenden

**Demo-Tabelle (HTML):**
```
| Nutzer  | Passwort (SCHLECHT) | Passwort (GUT)                  |
|---------|---------------------|---------------------------------|
| user1   | password123         | $2b$10$N9qo8uL... (bcrypt)    |
| user2   | mypassword          | $2b$10$kF3s7hL... (bcrypt)    |
```

---

### Szene 10: Lösungen
**Dauer:** 1 Min  
**Visuell:**
- Browser mit HTTPS-Symbol (Schloss)
- Code: `bcrypt.hash(password)`
- Grafik: HTTP vs. HTTPS Vergleich

**Sprechertext:**  
"Wie schützt man sich vor Cryptographic Failures? Erstens: Nutze immer HTTPS – das verschlüsselt die Kommunikation zwischen Browser und Server. Zweitens: Speichere Passwörter niemals im Klartext. Nutze sichere Hashing-Algorithmen wie bcrypt oder Argon2. Drittens: Verschlüssle sensible Daten in der Datenbank. Und viertens: Verwende starke, moderne Verschlüsselungsmethoden und halte sie aktuell. Als Faustregel gilt: Wenn du nicht sicher bist, ob Daten verschlüsselt werden sollten – dann sollten sie es wahrscheinlich."

**Technische Notizen:**
- HTTPS-Symbol gross zeigen (grünes Schloss)
- Pseudo-Code für bcrypt einblenden
- HTTP vs. HTTPS Grafik (unverschlüsselt vs. verschlüsselt)

**Code-Beispiel:**
```javascript
// Passwort hashen (Node.js mit bcrypt)
const bcrypt = require('bcrypt');
const saltRounds = 10;

// Beim Registrieren
const passwortHash = await bcrypt.hash(passwort, saltRounds);
// → Speichere passwortHash in Datenbank

// Beim Login
const istKorrekt = await bcrypt.compare(eingabe, passwortHash);
```

---

## TEIL 3: INJECTION (2 Min 30 Sek)

### Szene 11: Was ist Injection?
**Dauer:** 45 Sekunden  
**Visuell:**
- Suchfeld auf Portfolio-Seite
- Eingabe: `Robert'); DROP TABLE users;--`
- Datenbank-Symbol explodiert/verschwindet

**Sprechertext:**  
"Kommen wir zum dritten Risiko: Injection – das Einschleusen von Schadcode. Injection passiert, wenn deine Anwendung Benutzereingaben nicht richtig prüft und sie direkt an die Datenbank oder den Server weitergibt. Ein berühmtes Beispiel ist SQL-Injection. Stell dir vor, ein Suchfeld auf deiner Portfolio-Seite. Ein Angreifer gibt ein: Robert'); DROP TABLE users;--. Wenn du diese Eingabe ungefiltert an deine SQL-Datenbank weitergibst, wird der Befehl ausgeführt – und deine gesamte Nutzertabelle gelöscht!"

**Technische Notizen:**
- Demo-Suchformular vorbereiten
- SQL-Befehl im Eingabefeld zeigen
- Animation: Datenbank-Icon löst sich auf

**Demo-Datei:**
- `suche.html` mit Eingabefeld
- Zeige SQL-Injection String im Feld

---

### Szene 12: SQL-Injection im Detail
**Dauer:** 50 Sekunden  
**Visuell:**
- Code-Editor zeigt unsicheren Code:
```javascript
let query = "SELECT * FROM users WHERE name = '" + eingabe + "'";
```
- Zeigt was passiert bei Eingabe: `' OR '1'='1`

**Sprechertext:**  
"Schauen wir uns an, wie SQL-Injection funktioniert. Hier ist unsicherer Code: Eine SQL-Abfrage wird direkt mit der Nutzereingabe zusammengebaut. Wenn jemand jetzt eingibt: Strich OR Strich eins gleich Strich eins, wird die SQL-Abfrage manipuliert. Statt nur einen Nutzer zu finden, gibt die Abfrage alle Nutzer zurück – weil eins gleich eins immer wahr ist. So können Angreifer auf alle Daten zugreifen oder sie sogar löschen."

**Technische Notizen:**
- Zwei Code-Blöcke vorbereiten:
  - Original Query
  - Manipulierte Query (rot markiert)
- Zeige Step-by-Step was passiert

**Code-Demo:**
```javascript
// UNSICHERER CODE
let eingabe = "Robert'; DROP TABLE users;--";
let query = "SELECT * FROM users WHERE name = '" + eingabe + "'";
// → SELECT * FROM users WHERE name = 'Robert'; DROP TABLE users;--'
//   ☠️ Führt zwei Befehle aus!

// Was passiert:
// 1. SELECT * FROM users WHERE name = 'Robert';
// 2. DROP TABLE users;
// 3. -- (Kommentar, ignoriert Rest)
```

---

### Szene 13: Weitere Injection-Arten
**Dauer:** 30 Sekunden  
**Visuell:**
- Liste mit verschiedenen Injection-Typen
- Icons für jede Art

**Sprechertext:**  
"SQL-Injection ist nicht die einzige Form. Es gibt auch Command Injection – das Ausführen von Systembefehlen. Oder XSS, Cross-Site Scripting – dabei wird JavaScript-Code in deine Website eingeschleust. Auch LDAP Injection oder XML Injection gehören dazu. Das Prinzip ist immer gleich: Ungeprüfte Eingaben werden als Code interpretiert."

**Technische Notizen:**
- Liste erstellen mit 4-5 Injection-Typen
- Kurze Definition bei jedem Typ

**Liste vorbereiten:**
- SQL Injection (Datenbank)
- Command Injection (Betriebssystem)
- XSS – Cross-Site Scripting (JavaScript)
- LDAP Injection (Verzeichnisdienste)

---

### Szene 14: Wie verhindere ich Injection?
**Dauer:** 55 Sekunden  
**Visuell:**
- Code-Editor zeigt sicheren Code mit Prepared Statements
- Input-Validation Beispiel

**Sprechertext:**  
"Wie schützt man sich vor Injection? Die wichtigste Regel: Validiere und bereinige alle Nutzereingaben – immer! Verwende Prepared Statements oder Parameterized Queries für Datenbankabfragen. Dabei werden Eingaben automatisch als Daten behandelt, nicht als Code. Nutze Input-Validation – prüfe, ob Eingaben dem erwarteten Format entsprechen. Zum Beispiel: Eine E-Mail-Adresse muss ein @-Zeichen enthalten. Und verwende etablierte Libraries, die dir helfen – etwa Sanitizer oder ORM-Frameworks, die Injection automatisch verhindern."

**Technische Notizen:**
- Zwei Code-Vergleiche zeigen:
  - UNSICHER vs. SICHER
- Best Practices Liste einblenden

**Code-Beispiele:**
```javascript
// UNSICHER - String-Konkatenation
let query = "SELECT * FROM users WHERE name = '" + eingabe + "'";

// SICHER - Prepared Statement (Node.js/MySQL)
let query = "SELECT * FROM users WHERE name = ?";
connection.query(query, [eingabe], function(error, results) {
    // Eingabe wird automatisch escaped
});
```

---

## ZUSAMMENFASSUNG & PRAXIS (1 Min 30 Sek)

### Szene 15: Die Top 3 nochmal
**Dauer:** 30 Sekunden  
**Visuell:**
- Zusammenfassungs-Folie mit 3 Cards
- Jede Card: Risiko + Wichtigste Massnahme

**Sprechertext:**  
"Fassen wir zusammen. Die OWASP Top 3 Sicherheitsrisiken sind: Erstens, Broken Access Control – prüfe immer die Berechtigung auf dem Server. Zweitens, Cryptographic Failures – verschlüssle sensible Daten mit HTTPS und sicheren Hash-Algorithmen. Und drittens, Injection – validiere alle Eingaben und nutze Prepared Statements. Diese drei Prinzipien sind die Basis für sichere Webentwicklung."

**Technische Notizen:**
- Finale Folie mit allen 3 Risiken
- Jeweils ein Satz zur Lösung

**Folie:**
```
OWASP TOP 3 – ZUSAMMENFASSUNG

1. Broken Access Control
   → Berechtigungen serverseitig prüfen

2. Cryptographic Failures
   → HTTPS nutzen, Passwörter hashen

3. Injection
   → Eingaben validieren, Prepared Statements
```

---

### Szene 16: Tipps für deine Portfolio-Seite
**Dauer:** 40 Sekunden  
**Visuell:**
- Portfolio-Website im Browser
- Checkliste einblenden

**Sprechertext:**  
"Was bedeutet das konkret für deine Portfolio-Seite? Auch wenn du noch keine Login-Funktion hast, kannst du schon Sicherheit einbauen. Nutze HTTPS, wenn du deine Seite hostest. Validiere alle Formulareingaben – etwa im Kontaktformular. Wenn du später ein Login einbaust, denke von Anfang an an sichere Passwort-Speicherung. Und teste verschiedene Eingaben in deinen Formularen – was passiert bei seltsamen Zeichen oder sehr langen Texten?"

**Technische Notizen:**
- Portfolio-Demo zeigen
- Security-Checklist einblenden

**Checklist vorbereiten:**
- [ ] HTTPS aktiviert?
- [ ] Formulare validieren Eingaben?
- [ ] Keine sensiblen Daten im Code?
- [ ] Passwörter werden gehashed?
- [ ] SQL-Queries nutzen Prepared Statements?

---

### Szene 17: Weiterführende Ressourcen
**Dauer:** 20 Sekunden  
**Visuell:**
- Liste mit Links
- QR-Code zu OWASP-Seite

**Sprechertext:**  
"Wenn du mehr über Sicherheit lernen willst, schau auf owasp.org vorbei – dort findest du die komplette Top 10 Liste mit detaillierten Erklärungen. Auch MDN Web Docs hat gute Artikel zu Web Security. In den Aufgaben übst du jetzt, Sicherheitslücken in Code-Beispielen zu finden und zu beheben. Viel Erfolg!"

**Technische Notizen:**
- Links-Liste anzeigen
- QR-Code zu: https://owasp.org/www-project-top-ten/

**Links-Folie:**
```
WEITERFÜHRENDE LINKS

🔗 OWASP Top 10: https://owasp.org/Top10
🔗 MDN Web Security: https://developer.mozilla.org/en-US/docs/Web/Security
🔗 PortSwigger Academy: https://portswigger.net/web-security
```

---

## OUTRO (20 Sekunden)

### Szene 18: Abspann
**Dauer:** 20 Sekunden  
**Visuell:**
- BAND Design Abspann
- "Nächstes Video: JSON-Grundlagen"
- Social Media / Kontakt

**Sprechertext:**  
"Das war's zum Thema OWASP Top 3 Sicherheitsrisiken. Im nächsten Video schauen wir uns JSON-Grundlagen an. Bis bald!"

**Technische Notizen:**
- Fade out mit BAND-Farben
- Vorschau auf nächstes Video
- Schrift: Aptos Regular

---

## BENÖTIGTE DEMO-DATEIEN

### 1. demo-profil.html
```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Demo: Broken Access Control</title>
    <style>
        body {
            font-family: Aptos, Arial, sans-serif;
            max-width: 800px;
            margin: 50px auto;
            padding: 20px;
            background: #f5f5f5;
        }
        .profil-box {
            background: white;
            padding: 30px;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        .url-box {
            background: #005a73;
            color: white;
            padding: 15px;
            border-radius: 5px;
            font-family: monospace;
            margin-bottom: 20px;
        }
        .warnung {
            background: #f5a623;
            color: white;
            padding: 15px;
            border-radius: 5px;
            margin-top: 20px;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <div class="url-box">
        https://portfolio.ch/profil?user=<span id="userId">123</span>
    </div>
    
    <div class="profil-box">
        <h2>Profil von <span id="userName">Max Muster</span></h2>
        <p><strong>E-Mail:</strong> <span id="userEmail">max@example.com</span></p>
        <p><strong>Geburtsdatum:</strong> <span id="userBday">15.03.2005</span></p>
        <p><strong>Adresse:</strong> <span id="userAddress">Musterstrasse 1, 3000 Bern</span></p>
        
        <button onclick="changeUser(124)">User 124 anzeigen</button>
    </div>
    
    <div class="warnung" id="warnung" style="display: none;">
        ⚠️ SICHERHEITSWARNUNG: Zugriff auf fremdes Profil ohne Authentifizierung!
    </div>
    
    <script>
        const users = {
            123: {name: "Max Muster", email: "max@example.com", bday: "15.03.2005", address: "Musterstrasse 1, 3000 Bern"},
            124: {name: "Anna Beispiel", email: "anna@example.com", bday: "22.07.2004", address: "Beispielweg 5, 8000 Zürich"}
        };
        
        function changeUser(id) {
            document.getElementById('userId').textContent = id;
            document.getElementById('userName').textContent = users[id].name;
            document.getElementById('userEmail').textContent = users[id].email;
            document.getElementById('userBday').textContent = users[id].bday;
            document.getElementById('userAddress').textContent = users[id].address;
            document.getElementById('warnung').style.display = 'block';
        }
    </script>
</body>
</html>
```

### 2. admin-panel.html
```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Admin Panel</title>
    <style>
        body {
            font-family: Aptos, Arial, sans-serif;
            margin: 0;
            background: #f5f5f5;
        }
        .admin-header {
            background: #d32f2f;
            color: white;
            padding: 20px;
            text-align: center;
        }
        .content {
            max-width: 1000px;
            margin: 30px auto;
            padding: 20px;
        }
        .card {
            background: white;
            padding: 20px;
            margin-bottom: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        .danger-btn {
            background: #d32f2f;
            color: white;
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
        }
        .warnung {
            background: #f5a623;
            color: white;
            padding: 20px;
            border-radius: 8px;
            margin-top: 30px;
            font-size: 18px;
            font-weight: bold;
            text-align: center;
        }
    </style>
</head>
<body>
    <div class="admin-header">
        <h1>🔐 ADMIN PANEL</h1>
        <p>Voller Zugriff auf alle Funktionen</p>
    </div>
    
    <div class="content">
        <div class="card">
            <h2>Nutzer verwalten</h2>
            <p>Aktuell registrierte Nutzer: 245</p>
            <button class="danger-btn">Alle Nutzer löschen</button>
        </div>
        
        <div class="card">
            <h2>Datenbank</h2>
            <p>Datenbank-Grösse: 2.4 GB</p>
            <button class="danger-btn">Datenbank zurücksetzen</button>
        </div>
        
        <div class="card">
            <h2>System-Einstellungen</h2>
            <p>Server-Zugriff, Backup-Einstellungen, Logs</p>
            <button class="danger-btn">Konfiguration ändern</button>
        </div>
        
        <div class="warnung">
            ⚠️ DIESE SEITE IST OHNE LOGIN ZUGÄNGLICH!<br>
            Broken Access Control Demo
        </div>
    </div>
</body>
</html>
```

### 3. suche.html (SQL Injection Demo)
```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Demo: SQL Injection</title>
    <style>
        body {
            font-family: Aptos, Arial, sans-serif;
            max-width: 900px;
            margin: 50px auto;
            padding: 20px;
            background: #f5f5f5;
        }
        .search-box {
            background: white;
            padding: 30px;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            margin-bottom: 20px;
        }
        input[type="text"] {
            width: 100%;
            padding: 15px;
            font-size: 16px;
            border: 2px solid #4eb9cc;
            border-radius: 5px;
            font-family: monospace;
        }
        .code-box {
            background: #2d2d2d;
            color: #f8f8f2;
            padding: 20px;
            border-radius: 5px;
            font-family: monospace;
            margin-top: 20px;
            font-size: 14px;
        }
        .danger {
            background: #d32f2f;
            color: white;
            padding: 20px;
            border-radius: 8px;
            margin-top: 20px;
            font-weight: bold;
        }
        button {
            background: #005a73;
            color: white;
            padding: 15px 30px;
            border: none;
            border-radius: 5px;
            font-size: 16px;
            cursor: pointer;
            margin-top: 15px;
        }
    </style>
</head>
<body>
    <div class="search-box">
        <h2>Nutzer suchen</h2>
        <input type="text" id="searchInput" 
               placeholder="Name eingeben..." 
               value="Robert">
        <button onclick="showInjection()">Suchen</button>
        
        <div class="code-box" id="codeBox">
            <div>Ausgeführte SQL-Query:</div>
            <div id="queryText" style="margin-top: 10px; color: #50fa7b;">
                SELECT * FROM users WHERE name = 'Robert'
            </div>
        </div>
    </div>
    
    <div class="search-box">
        <h3>☠️ Versuch mal diese Eingaben:</h3>
        <button onclick="setInput(`Robert'); DROP TABLE users;--`)">
            SQL Injection 1: Robert'); DROP TABLE users;--
        </button>
        <button onclick="setInput(`' OR '1'='1`)">
            SQL Injection 2: ' OR '1'='1
        </button>
        
        <div class="danger" id="danger" style="display: none;">
            ⚠️ GEFAHR! Diese Eingabe würde die Datenbank manipulieren!
        </div>
    </div>
    
    <script>
        function setInput(value) {
            document.getElementById('searchInput').value = value;
            showInjection();
        }
        
        function showInjection() {
            const input = document.getElementById('searchInput').value;
            const query = `SELECT * FROM users WHERE name = '${input}'`;
            document.getElementById('queryText').textContent = query;
            
            if (input.includes('DROP') || input.includes('OR')) {
                document.getElementById('danger').style.display = 'block';
                document.getElementById('queryText').style.color = '#ff5555';
            } else {
                document.getElementById('danger').style.display = 'none';
                document.getElementById('queryText').style.color = '#50fa7b';
            }
        }
    </script>
</body>
</html>
```

---

## ZUSAMMENFASSUNG PRODUKTIONSSCHRITTE

1. **Vorbereitung (30 Min)**
   - Alle Demo-HTML-Dateien erstellen und testen
   - OWASP-Website öffnen und Screenshot machen
   - Folien mit BAND-Design erstellen (3 Cards, Zusammenfassung)

2. **Aufnahme (15-20 Min)**
   - Intro mit Titel-Animation
   - Jede Szene einzeln aufnehmen
   - Bildschirmaufnahme für Code-Demos
   - Browser-Demos aufzeichnen

3. **Post-Production (60 Min)**
   - Szenen schneiden und zusammenfügen
   - Übergänge hinzufügen
   - Warnungen/Icons einblenden
   - Audio normalisieren
   - Untertitel ergänzen (optional)

4. **Qualitätskontrolle**
   - Video komplett durchschauen
   - Timing prüfen (Ziel: 8-10 Min)
   - Ton-Qualität checken
   - Alle Demos funktionieren?

---

**GESAMTDAUER VIDEO:** ca. 8-10 Minuten  
**PRODUKTIONSZEIT:** ca. 2-3 Stunden
