# 02 – Sicherheitslücken Beheben

**Thema:** Diverses – OWASP Top 3 Sicherheitsrisiken  
**Schwierigkeit:** Mittel  
**Geschätzte Zeit:** 30 Minuten

---

## Lernziel

Du behebst konkrete Sicherheitslücken in Code-Beispielen und wendest Best Practices für sichere Webentwicklung an. Du verstehst, wie man Broken Access Control, Cryptographic Failures und Injection praktisch verhindert.

---

## Aufgabenstellung

### Vorbereitung

Erstelle einen neuen Ordner `sicherheit-uebung` auf deinem Computer. Darin erstellst du die Dateien für diese Aufgabe.

---

### Teil 1: Broken Access Control beheben (10 Min)

Gegeben ist folgender unsicherer Code für eine Profil-Seite:

**profil-unsicher.html:**
```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>Mein Profil</title>
</head>
<body>
    <h1>Profil von <span id="profilName"></span></h1>
    <p><strong>E-Mail:</strong> <span id="profilEmail"></span></p>
    <p><strong>Telefon:</strong> <span id="profilTelefon"></span></p>
    
    <script>
        // Hole User-ID aus der URL
        const urlParams = new URLSearchParams(window.location.search);
        const userId = urlParams.get('user') || '1';
        
        // Simulierte Datenbank
        const users = {
            '1': { name: 'Max Muster', email: 'max@example.com', telefon: '079 123 45 67' },
            '2': { name: 'Anna Beispiel', email: 'anna@example.com', telefon: '079 987 65 43' },
            '3': { name: 'Peter Admin', email: 'admin@example.com', telefon: '079 555 00 00' }
        };
        
        // Zeige Profil an - OHNE PRÜFUNG!
        const profil = users[userId];
        if (profil) {
            document.getElementById('profilName').textContent = profil.name;
            document.getElementById('profilEmail').textContent = profil.email;
            document.getElementById('profilTelefon').textContent = profil.telefon;
        }
    </script>
</body>
</html>
```

**Deine Aufgabe:**

1. Erstelle die Datei `profil-unsicher.html` mit dem Code oben
2. Öffne die Datei im Browser und teste: `profil-unsicher.html?user=1`, dann `?user=2`, dann `?user=3`
3. **Problem erkennen:** Was ist das Sicherheitsproblem?
4. Erstelle eine verbesserte Version `profil-sicher.html`, die folgendes umsetzt:
   - Simuliere einen eingeloggten Nutzer (z.B. `const eingeloggterUserId = '1';`)
   - Prüfe vor dem Anzeigen: Ist der eingeloggte Nutzer berechtigt?
   - Zeige eine Fehlermeldung, wenn nicht berechtigt
   - Nutzer mit ID '3' (Admin) darf alle Profile sehen

**Tipp:** Nutze eine `if`-Bedingung: `if (eingeloggterUserId === userId || users[eingeloggterUserId].name.includes('Admin')) { ... }`

---

### Teil 2: Cryptographic Failures beheben (10 Min)

Gegeben ist ein einfaches Login-Formular ohne Verschlüsselung:

**login-unsicher.html:**
```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>Login</title>
    <style>
        body { font-family: Arial, sans-serif; max-width: 400px; margin: 50px auto; padding: 20px; }
        input { width: 100%; padding: 10px; margin: 10px 0; font-size: 16px; }
        button { width: 100%; padding: 12px; background: #005a73; color: white; border: none; font-size: 16px; }
        .warnung { background: #f5a623; color: white; padding: 15px; border-radius: 5px; margin-top: 20px; }
    </style>
</head>
<body>
    <h2>Login</h2>
    
    <!-- UNSICHER: Verwendet HTTP und speichert Passwörter im Klartext -->
    <form action="http://example.com/login" method="POST">
        <input type="text" name="username" placeholder="Benutzername" required>
        <input type="password" name="password" placeholder="Passwort" required>
        <button type="submit">Anmelden</button>
    </form>
    
    <div class="warnung">
        ⚠️ WARNUNG: Diese Seite nutzt HTTP (nicht HTTPS)!<br>
        Das Passwort wird unverschlüsselt übertragen.
    </div>
    
    <script>
        // Simulierte "Datenbank" mit Klartext-Passwörtern
        const users = [
            { username: 'max', password: 'password123' },
            { username: 'anna', password: 'mypassword' }
        ];
        
        console.log('⚠️ UNSICHER: Passwörter im Klartext gespeichert:');
        console.log(users);
    </script>
</body>
</html>
```

**Deine Aufgabe:**

1. Erstelle die Datei `login-unsicher.html`
2. Öffne die Browser-Konsole (F12) und beobachte die gespeicherten Passwörter
3. Erstelle eine verbesserte Version `login-sicherheitshinweise.html`, die:
   - Im Formular-Action `https://` statt `http://` nutzt
   - Eine deutliche Warnung entfernt und stattdessen einen grünen Hinweis zeigt: "✓ Diese Seite nutzt HTTPS"
   - In den Kommentaren erklärt, warum Passwörter niemals im Klartext gespeichert werden sollten
   - Zeigt, wie gehashte Passwörter aussehen würden (Beispiel als String)

**Beispiel für gehashtes Passwort:**
```javascript
// SICHER: Passwort wurde mit bcrypt gehashed
const users = [
    { username: 'max', passwordHash: '$2b$10$N9qo8uLlVkd4iVz.B3s2eOYvZZ4O4y7pJj8rU' },
    { username: 'anna', passwordHash: '$2b$10$kF3s7hLmO9x5tYw3vD8fKeR3pN7sK2qL9mZ' }
];
```

---

### Teil 3: Injection verhindern (10 Min)

Gegeben ist eine Such-Funktion mit SQL-Injection-Risiko:

**suche-unsicher.html:**
```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>Projektsuche</title>
    <style>
        body { font-family: Arial, sans-serif; max-width: 800px; margin: 50px auto; padding: 20px; }
        input { width: 70%; padding: 15px; font-size: 16px; }
        button { padding: 15px 30px; background: #4eb9cc; color: white; border: none; font-size: 16px; }
        .code { background: #2d2d2d; color: #50fa7b; padding: 20px; margin-top: 20px; font-family: monospace; border-radius: 5px; }
        .gefahr { background: #d32f2f; color: white; padding: 20px; margin-top: 20px; border-radius: 5px; display: none; }
    </style>
</head>
<body>
    <h2>Projekte suchen</h2>
    
    <input type="text" id="suchfeld" placeholder="Projektname eingeben...">
    <button onclick="suchenUnsicher()">Suchen (UNSICHER)</button>
    
    <div class="code" id="sqlQuery"></div>
    <div class="gefahr" id="warnung"></div>
    
    <script>
        function suchenUnsicher() {
            const suchbegriff = document.getElementById('suchfeld').value;
            
            // UNSICHER: SQL-Injection möglich!
            const query = "SELECT * FROM projekte WHERE name = '" + suchbegriff + "'";
            
            document.getElementById('sqlQuery').textContent = 
                "Ausgeführte SQL-Query:\n" + query;
            
            // Prüfe auf gefährliche Eingaben
            if (suchbegriff.includes("'") || 
                suchbegriff.includes(";") || 
                suchbegriff.toUpperCase().includes("DROP")) {
                document.getElementById('warnung').style.display = 'block';
                document.getElementById('warnung').textContent = 
                    "⚠️ GEFAHR! Diese Eingabe könnte die Datenbank manipulieren!";
            } else {
                document.getElementById('warnung').style.display = 'none';
            }
        }
        
        // Teste diese Eingaben:
        console.log("Teste diese gefährlichen Eingaben:");
        console.log("1. Robert'); DROP TABLE projekte;--");
        console.log("2. ' OR '1'='1");
    </script>
</body>
</html>
```

**Deine Aufgabe:**

1. Erstelle die Datei `suche-unsicher.html`
2. Teste die Suche mit normalen Eingaben (z.B. "Portfolio")
3. Teste dann: `Robert'); DROP TABLE projekte;--`
4. Beobachte, wie die SQL-Query manipuliert wird
5. Erstelle eine verbesserte Version `suche-sicher.html`, die:
   - Zeigt, wie Prepared Statements aussehen würden (als Kommentar oder Pseudocode)
   - Eine Input-Validation einbaut: Nur Buchstaben, Zahlen, Leerzeichen erlaubt
   - Gefährliche Zeichen (`'`, `;`, `--`) automatisch entfernt oder ablehnt
   - Eine Erfolgsmeldung anzeigt: "✓ Eingabe ist sicher validiert"

**Pseudocode für Prepared Statement (als Kommentar einfügen):**
```javascript
// SICHER mit Prepared Statement (serverseitig):
// const query = "SELECT * FROM projekte WHERE name = ?";
// connection.query(query, [suchbegriff], function(error, results) {
//     // suchbegriff wird automatisch escaped
// });
```

---

## Erfolgskriterien

Deine Lösung ist vollständig, wenn:

- [ ] Du alle drei unsicheren HTML-Dateien erstellt und getestet hast
- [ ] Du für jedes Beispiel eine sichere Version erstellt hast
- [ ] Deine sicheren Versionen enthalten Kommentare, die erklären, was verbessert wurde
- [ ] Du die Sicherheitsprobleme praktisch nachvollzogen hast
- [ ] Im Ordner `sicherheit-uebung` sind 6 HTML-Dateien vorhanden (3 unsicher + 3 sicher)

---

## Häufige Fehler vermeiden

- **Fehler:** Prüfungen nur im JavaScript machen  
  **Richtig:** In echten Anwendungen müssen Prüfungen auf dem Server passieren. JavaScript kann vom Nutzer manipuliert werden.

- **Fehler:** Passwörter werden nur versteckt angezeigt (type="password")  
  **Richtig:** Das versteckt Passwörter nur visuell. Sie müssen auch bei der Übertragung (HTTPS) und Speicherung (Hashing) geschützt werden.

- **Fehler:** Eingaben werden nur auf bestimmte Begriffe geprüft  
  **Richtig:** Nutze Whitelisting (nur erlaubte Zeichen) statt Blacklisting (verbotene Begriffe).

---

## Reflexionsfragen

1. **Welche der drei Sicherheitslücken war am einfachsten zu beheben? Welche am schwersten?**
2. **Warum reicht es nicht aus, gefährliche Zeichen einfach zu entfernen (z.B. `'` durch `''` ersetzen)?**
3. **In echten Anwendungen: Wo sollten Sicherheitsprüfungen stattfinden – im Browser oder auf dem Server? Warum?**

---

## Weiterführende Links

- **MDN: Web Security Overview:** [https://developer.mozilla.org/en-US/docs/Web/Security](https://developer.mozilla.org/en-US/docs/Web/Security)
- **OWASP: Broken Access Control:** [https://owasp.org/Top10/A01_2021-Broken_Access_Control/](https://owasp.org/Top10/A01_2021-Broken_Access_Control/)
- **OWASP: Cryptographic Failures:** [https://owasp.org/Top10/A02_2021-Cryptographic_Failures/](https://owasp.org/Top10/A02_2021-Cryptographic_Failures/)
- **OWASP: Injection:** [https://owasp.org/Top10/A03_2021-Injection/](https://owasp.org/Top10/A03_2021-Injection/)
- **bcrypt Erklärung:** [https://auth0.com/blog/hashing-in-action-understanding-bcrypt/](https://auth0.com/blog/hashing-in-action-understanding-bcrypt/)

---

## Tipps für die Lösung

- **Teste ausgiebig:** Versuche, deine eigenen sicheren Versionen zu "hacken". Finde Wege, die Sicherheitsmassnahmen zu umgehen.
- **Kommentiere deinen Code:** Erkläre in Kommentaren, warum du bestimmte Sicherheitsmassnahmen eingebaut hast.
- **Vergleiche Vorher/Nachher:** Öffne beide Versionen nebeneinander und erkenne die Unterschiede.
- **Nutze die Browser-Konsole:** Mit `console.log()` kannst du Variablen und Eingaben überprüfen.

---

**Nächste Aufgabe:** 03 – Portfolio mit Sicherheits-Checkliste
