# 04 – Vertiefung: Security Headers & Best Practices (Optional)

**Thema:** Diverses – OWASP Top 3 Sicherheitsrisiken  
**Schwierigkeit:** Schwer / Vertiefung  
**Geschätzte Zeit:** 50-60 Minuten

---

## Lernziel

Du lernst fortgeschrittene Sicherheitskonzepte kennen, die über die OWASP Top 3 hinausgehen. Du verstehst, wie Security Headers funktionieren, wie man CSRF-Angriffe verhindert und wie man eine umfassende Security Policy für eine Webanwendung erstellt.

**Hinweis:** Diese Aufgabe ist optional und für Lernende gedacht, die tiefer in Web-Sicherheit einsteigen möchten.

---

## Hintergrund: Weitere Sicherheitsrisiken

Die OWASP Top 10 enthält noch 7 weitere Risiken neben den Top 3:
- **A04:2021 – Insecure Design** (unsicheres Design)
- **A05:2021 – Security Misconfiguration** (Fehlkonfiguration)
- **A06:2021 – Vulnerable Components** (veraltete Komponenten)
- **A07:2021 – Authentication Failures** (Authentifizierungsfehler)
- **A08:2021 – Software and Data Integrity Failures**
- **A09:2021 – Logging and Monitoring Failures**
- **A10:2021 – Server-Side Request Forgery (SSRF)**

In dieser Aufgabe fokussieren wir uns auf **Security Headers** und **CSRF-Prevention**.

---

## Aufgabenstellung

### Teil 1: Security Headers verstehen (20 Min)

Security Headers sind HTTP-Header, die der Server an den Browser sendet, um zusätzliche Sicherheitsmassnahmen zu aktivieren.

**Deine Aufgabe:**

1. Erstelle eine Datei `security-headers.md`
2. Recherchiere die folgenden Security Headers und dokumentiere sie:

**Zu recherchierende Headers:**

#### 1. Content-Security-Policy (CSP)
- Was macht dieser Header?
- Welche Angriffe verhindert er?
- Beispiel für eine CSP-Regel

#### 2. X-Frame-Options
- Wozu dient dieser Header?
- Welchen Angriff verhindert er? (Tipp: Clickjacking)
- Mögliche Werte: `DENY`, `SAMEORIGIN`

#### 3. X-Content-Type-Options
- Was bedeutet `nosniff`?
- Warum ist das wichtig?

#### 4. Strict-Transport-Security (HSTS)
- Was erzwingt dieser Header?
- Beispiel-Wert: `max-age=31536000; includeSubDomains`

#### 5. Referrer-Policy
- Was steuert dieser Header?
- Warum könnte es ein Problem sein, Referrer zu senden?

**Format der Dokumentation:**

```markdown
# Security Headers – Dokumentation

## 1. Content-Security-Policy (CSP)

**Beschreibung:**
[Erkläre in eigenen Worten, was CSP macht]

**Verhindert:**
- [Angriff 1]
- [Angriff 2]

**Beispiel:**
```
Content-Security-Policy: default-src 'self'; script-src 'self' https://cdnjs.cloudflare.com
```

**Bedeutung:**
[Erkläre, was dieses Beispiel erlaubt und verbietet]

---

## 2. X-Frame-Options
[etc.]
```

**Ressourcen für Recherche:**
- MDN Web Docs: [https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)
- OWASP Secure Headers: [https://owasp.org/www-project-secure-headers/](https://owasp.org/www-project-secure-headers/)

---

### Teil 2: CSRF verstehen und verhindern (20 Min)

CSRF (Cross-Site Request Forgery) ist ein Angriff, bei dem ein Nutzer ungewollt Aktionen auf einer Website ausführt, auf der er eingeloggt ist.

**Szenario:**
Max ist auf `bank.ch` eingeloggt. Er besucht eine bösartige Website `evil.com`. Diese Seite enthält:
```html
<form action="https://bank.ch/ueberweisen" method="POST" id="hack">
    <input type="hidden" name="empfaenger" value="hacker@evil.com">
    <input type="hidden" name="betrag" value="10000">
</form>
<script>document.getElementById('hack').submit();</script>
```

Da Max eingeloggt ist, würde die Überweisung ausgeführt!

**Deine Aufgabe:**

1. Erstelle eine Datei `csrf-demo.html`, die dieses Szenario simuliert
2. Erstelle eine Datei `csrf-prevention.md`, die folgende Fragen beantwortet:
   - Was ist ein CSRF-Angriff?
   - Warum funktioniert dieser Angriff?
   - Wie kann man CSRF verhindern? (CSRF-Token)
   - Wie funktioniert ein CSRF-Token?

**Starter-Code für `csrf-demo.html`:**

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>CSRF Demo</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 1200px;
            margin: 50px auto;
            padding: 20px;
        }
        .split {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
        }
        .panel {
            padding: 20px;
            border: 2px solid #ddd;
            border-radius: 8px;
        }
        .bank {
            background: #e7f5ff;
            border-color: #4eb9cc;
        }
        .evil {
            background: #ffe7e7;
            border-color: #d32f2f;
        }
        .safe {
            background: #e7ffe7;
            border-color: #45ba98;
        }
        button {
            padding: 10px 20px;
            margin: 10px 5px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
        }
        .bank-btn { background: #4eb9cc; color: white; }
        .evil-btn { background: #d32f2f; color: white; }
        .safe-btn { background: #45ba98; color: white; }
        .log {
            background: #2d2d2d;
            color: #50fa7b;
            padding: 15px;
            margin-top: 15px;
            border-radius: 5px;
            font-family: monospace;
            min-height: 100px;
            font-size: 14px;
        }
    </style>
</head>
<body>
    <h1>CSRF Demonstration</h1>
    
    <div class="split">
        <!-- BANK WEBSITE -->
        <div class="panel bank">
            <h2>🏦 Bank.ch (Legitime Seite)</h2>
            <p><strong>Eingeloggt als:</strong> Max Muster</p>
            <p><strong>Kontostand:</strong> CHF 50'000</p>
            
            <h3>Überweisung tätigen</h3>
            <form id="bankForm">
                <input type="text" id="empfaenger" placeholder="Empfänger" 
                       value="Anna Beispiel" style="width: 100%; padding: 8px; margin: 5px 0;">
                <input type="number" id="betrag" placeholder="Betrag" 
                       value="100" style="width: 100%; padding: 8px; margin: 5px 0;">
                <button type="submit" class="bank-btn">Überweisen</button>
            </form>
            
            <div class="log" id="bankLog">Keine Transaktionen</div>
        </div>
        
        <!-- EVIL WEBSITE -->
        <div class="panel evil">
            <h2>☠️ Evil.com (Bösartige Seite)</h2>
            <p>Diese Seite sieht harmlos aus, aber enthält versteckten Code!</p>
            
            <h3>Klicke hier für Gratis-Pizza! 🍕</h3>
            <button class="evil-btn" onclick="csrfAngriff()">
                Jetzt Gratis-Pizza abholen!
            </button>
            
            <!-- Verstecktes Formular -->
            <form id="evilForm" action="#" method="POST" style="display: none;">
                <input type="hidden" name="empfaenger" value="hacker@evil.com">
                <input type="hidden" name="betrag" value="10000">
            </form>
            
            <div class="log" id="evilLog">
                console.log('Warte auf Opfer...')
            </div>
        </div>
    </div>
    
    <!-- LÖSUNG: CSRF-Token -->
    <div class="panel safe" style="margin-top: 30px;">
        <h2>✅ Sichere Version mit CSRF-Token</h2>
        <p>In einer echten Anwendung würde jede Überweisung ein CSRF-Token benötigen.</p>
        
        <h3>Funktionsweise:</h3>
        <ol>
            <li>Server generiert bei jeder Anfrage ein zufälliges Token</li>
            <li>Token wird im Formular als Hidden Field eingefügt</li>
            <li>Bei Absenden: Server prüft, ob Token gültig ist</li>
            <li>Evil.com kennt das Token nicht → Angriff scheitert</li>
        </ol>
        
        <h3>Sichere Überweisung:</h3>
        <form id="safeForm">
            <input type="hidden" name="csrf_token" id="csrfToken" value="">
            <input type="text" placeholder="Empfänger" style="width: 100%; padding: 8px; margin: 5px 0;">
            <input type="number" placeholder="Betrag" style="width: 100%; padding: 8px; margin: 5px 0;">
            <button type="submit" class="safe-btn">Sicher Überweisen</button>
        </form>
        
        <div class="log" id="safeLog">Aktuelles CSRF-Token: [wird generiert]</div>
    </div>
    
    <script>
        // Simuliere Session
        let eingeloggt = true;
        let kontostand = 50000;
        let transaktionen = [];
        
        // === BANK FORMULAR ===
        document.getElementById('bankForm').addEventListener('submit', function(e) {
            e.preventDefault();
            const empfaenger = document.getElementById('empfaenger').value;
            const betrag = parseInt(document.getElementById('betrag').value);
            
            if (eingeloggt && betrag > 0 && betrag <= kontostand) {
                kontostand -= betrag;
                transaktionen.push(`✓ Überweisung: CHF ${betrag} an ${empfaenger}`);
                updateBankLog();
            }
        });
        
        // === CSRF ANGRIFF ===
        function csrfAngriff() {
            document.getElementById('evilLog').innerHTML = 
                `console.log('CSRF-Angriff gestartet...')
console.log('Sende versteckte Anfrage an bank.ch')
console.log('Nutzer ist eingeloggt: ${eingeloggt}')`;
            
            setTimeout(() => {
                if (eingeloggt) {
                    // Simuliere automatische Überweisung
                    kontostand -= 10000;
                    transaktionen.push(`⚠️ CSRF-ANGRIFF: CHF 10'000 an hacker@evil.com`);
                    updateBankLog();
                    
                    document.getElementById('evilLog').innerHTML += `
console.log('SUCCESS! Überweisung ausgeführt!')
console.log('CHF 10'000 an hacker@evil.com überwiesen')`;
                }
            }, 1000);
        }
        
        function updateBankLog() {
            const log = document.getElementById('bankLog');
            log.innerHTML = `Kontostand: CHF ${kontostand.toLocaleString()}

Transaktionen:
${transaktionen.join('\n')}`;
        }
        
        // === SICHERE VERSION MIT CSRF-TOKEN ===
        let csrfToken = generateToken();
        document.getElementById('csrfToken').value = csrfToken;
        document.getElementById('safeLog').textContent = 
            `Aktuelles CSRF-Token: ${csrfToken}`;
        
        function generateToken() {
            return 'csrf_' + Math.random().toString(36).substring(2, 15);
        }
        
        document.getElementById('safeForm').addEventListener('submit', function(e) {
            e.preventDefault();
            const submittedToken = document.getElementById('csrfToken').value;
            
            if (submittedToken === csrfToken) {
                document.getElementById('safeLog').textContent = 
                    `✓ CSRF-Token validiert!\nÜberweisung wurde sicher ausgeführt.\n\nNeues Token generiert: ${generateToken()}`;
            } else {
                document.getElementById('safeLog').textContent = 
                    `✗ CSRF-Token ungültig!\nAngriff wurde blockiert.`;
            }
        });
    </script>
</body>
</html>
```

**Teste folgendes:**
1. Führe eine normale Überweisung über das Bank-Formular aus
2. Klicke auf den "Gratis-Pizza"-Button auf evil.com
3. Beobachte, wie ein CSRF-Angriff die Überweisung manipuliert
4. Teste das sichere Formular mit CSRF-Token

---

### Teil 3: Umfassende Security Policy erstellen (10 Min)

Erstelle eine Datei `security-policy.md`, die eine vollständige Sicherheitsrichtlinie für ein fiktives Web-Projekt definiert.

**Template:**

```markdown
# Security Policy – [Projektname]

**Version:** 1.0  
**Datum:** [Aktuelles Datum]  
**Autor:** [Dein Name]

---

## 1. Übersicht

Dieses Dokument beschreibt alle Sicherheitsmassnahmen für das Projekt [Projektname]. 
Ziel ist es, die Anwendung gegen die OWASP Top 10 Risiken zu schützen.

---

## 2. Authentifizierung & Autorisierung

### 2.1 Passwort-Richtlinien
- [ ] Mindestlänge: 12 Zeichen
- [ ] Muss enthalten: Gross-/Kleinbuchstaben, Zahlen, Sonderzeichen
- [ ] Passwörter werden mit bcrypt (cost factor 12) gehashed
- [ ] Keine Passwörter im Klartext in Logs oder Datenbank

### 2.2 Session Management
- [ ] Session-Timeout: 30 Minuten Inaktivität
- [ ] Secure & HttpOnly Flags für Cookies
- [ ] CSRF-Token für alle State-Changing Requests

### 2.3 Zugriffskontrolle
- [ ] Whitelist-Ansatz: Alles verboten, ausser explizit erlaubt
- [ ] Autorisierung wird serverseitig geprüft (nie nur client-seitig)
- [ ] Admin-Bereiche erfordern zusätzliche Authentifizierung

---

## 3. Daten-Sicherheit

### 3.1 Verschlüsselung
- [ ] Alle Verbindungen über HTTPS (TLS 1.3)
- [ ] Sensible Daten in der Datenbank verschlüsselt
- [ ] API-Keys werden nie im Frontend-Code gespeichert

### 3.2 Daten-Validierung
- [ ] Alle Eingaben werden validiert (client- und serverseitig)
- [ ] Whitelist-Ansatz für erlaubte Zeichen
- [ ] Output Encoding gegen XSS

---

## 4. Injection-Prävention

- [ ] Prepared Statements für alle SQL-Queries
- [ ] Input Sanitization für alle Nutzer-Eingaben
- [ ] Content-Security-Policy Header aktiv
- [ ] Keine eval() oder innerHTML mit ungeprüften Daten

---

## 5. Security Headers

Folgende HTTP Security Headers werden gesetzt:

```
Content-Security-Policy: default-src 'self'; script-src 'self' 'unsafe-inline'
X-Frame-Options: DENY
X-Content-Type-Options: nosniff
Strict-Transport-Security: max-age=31536000; includeSubDomains
Referrer-Policy: strict-origin-when-cross-origin
Permissions-Policy: geolocation=(), microphone=(), camera=()
```

---

## 6. Monitoring & Logging

### 6.1 Was wird geloggt?
- Fehlgeschlagene Login-Versuche (max. 5, dann Account-Sperre für 15 Min)
- Ungewöhnliche Aktivitäten (z.B. 100+ Requests/Minute)
- Security-relevante Fehler (SQL-Injection-Versuche, etc.)

### 6.2 Was wird NICHT geloggt?
- Passwörter oder Tokens
- Kreditkartennummern
- Persönliche Gesundheitsdaten

---

## 7. Incident Response Plan

**Was tun bei einem Sicherheitsvorfall?**

1. **Erkennung:** Monitoring-System erkennt Anomalie
2. **Isolation:** Betroffene Komponente isolieren
3. **Analyse:** Logfiles analysieren, Ausmass bestimmen
4. **Behebung:** Sicherheitslücke schliessen
5. **Dokumentation:** Vorfall dokumentieren für zukünftige Prävention
6. **Benachrichtigung:** Bei Datenverlust: Betroffene Nutzer informieren

---

## 8. Update & Patch-Management

- [ ] Dependencies wöchentlich auf Updates prüfen
- [ ] Sicherheits-Patches innerhalb von 48h einspielen
- [ ] `npm audit` oder `pip check` regelmässig ausführen
- [ ] End-of-Life Libraries ersetzen

---

## 9. Testing

### 9.1 Security Tests
- [ ] Penetration Testing vor jedem Release
- [ ] Automated Security Scans mit OWASP ZAP
- [ ] Code Reviews mit Security-Fokus

### 9.2 Test-Szenarien
- SQL-Injection versuchen
- XSS-Payloads in alle Eingabefelder
- CSRF-Angriffe simulieren
- Broken Access Control testen (URL-Manipulation)

---

## 10. Verantwortlichkeiten

- **Security Officer:** [Name/Rolle]
- **Code Review:** [Name/Rolle]
- **Incident Response:** [Name/Rolle]

---

## 11. Review & Updates

Diese Policy wird alle 6 Monate überprüft und bei Bedarf aktualisiert.

**Nächster Review:** [Datum in 6 Monaten]
```

**Deine Aufgabe:**
1. Erstelle die Datei und fülle alle `[ ]`-Checkboxen aus
2. Passe die Policy an dein Portfolio-Projekt an
3. Überlege: Welche Punkte sind für dein aktuelles Projekt relevant?

---

## Erfolgskriterien

Deine Lösung ist vollständig, wenn:

- [ ] `security-headers.md` dokumentiert alle 5 Security Headers mit Beispielen
- [ ] `csrf-demo.html` funktioniert und demonstriert einen CSRF-Angriff
- [ ] `csrf-prevention.md` erklärt CSRF und Gegenmassnahmen verständlich
- [ ] `security-policy.md` enthält eine vollständige Security Policy
- [ ] Du hast alle Demos selbst getestet und verstanden

---

## Reflexionsfragen

1. **Welcher Security Header ist deiner Meinung nach am wichtigsten? Warum?**
2. **Wie würdest du testen, ob deine CSP-Policy zu streng oder zu locker ist?**
3. **Warum reicht ein CSRF-Token nicht aus, wenn die Website auch XSS-anfällig ist?**
4. **Wie würdest du entscheiden, welche Sicherheitsmassnahmen für ein kleines Projekt notwendig sind?**

---

## Weiterführende Links

- **OWASP Top 10 (vollständig):** [https://owasp.org/www-project-top-ten/](https://owasp.org/www-project-top-ten/)
- **Security Headers testen:** [https://securityheaders.com/](https://securityheaders.com/)
- **CSP Evaluator:** [https://csp-evaluator.withgoogle.com/](https://csp-evaluator.withgoogle.com/)
- **OWASP Cheat Sheet Series:** [https://cheatsheetseries.owasp.org/](https://cheatsheetseries.owasp.org/)
- **Web Security Academy (PortSwigger):** [https://portswigger.net/web-security](https://portswigger.net/web-security)

---

## Bonus-Herausforderungen

1. **Teste eine echte Website:** Nutze [https://securityheaders.com/](https://securityheaders.com/) und teste bekannte Websites. Welche Header fehlen?

2. **Implementiere eine CSP:** Füge deiner Portfolio-Seite einen Content-Security-Policy Header hinzu (via Meta-Tag). Teste, ob externe Scripts blockiert werden.

3. **XSS-Challenge:** Versuche, auf [https://xss-game.appspot.com/](https://xss-game.appspot.com/) die XSS-Challenges zu lösen.

4. **Automatisches Security Testing:** Installiere OWASP ZAP und scanne deine eigene Website auf Sicherheitslücken.

---

**Ende der optionalen Vertiefungsaufgabe**

Diese Aufgabe zeigt fortgeschrittene Konzepte, die in späteren Modulen (Node.js, Express, Datenbanken) praktisch angewendet werden können.
