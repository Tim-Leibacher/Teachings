# 01 – OWASP Kennenlernen

**Thema:** Diverses – OWASP Top 3 Sicherheitsrisiken  
**Schwierigkeit:** Einstieg  
**Geschätzte Zeit:** 25 Minuten

---

## Lernziel

Du lernst die OWASP-Organisation kennen und verstehst die drei häufigsten Sicherheitsrisiken für Webanwendungen: Broken Access Control, Cryptographic Failures und Injection. Du kannst diese Risiken in einfachen Code-Beispielen erkennen.

---

## Aufgabenstellung

### Teil 1: OWASP erkunden (10 Min)

Besuche die offizielle OWASP-Website und verschaffe dir einen Überblick über die Organisation und ihre Arbeit.

1. Öffne im Browser: [https://owasp.org/www-project-top-ten/](https://owasp.org/www-project-top-ten/)
2. Lies die Einleitung zur OWASP Top 10 Liste
3. Beantworte folgende Fragen in einem neuen Dokument `owasp-notizen.txt`:
   - Was bedeutet OWASP?
   - Was ist das Ziel der OWASP Top 10?
   - Welche drei Sicherheitsrisiken stehen auf Platz 1, 2 und 3?
   - In welchem Jahr wurde die aktuelle Liste veröffentlicht?

**Tipp:** Die OWASP Top 10 wird regelmässig aktualisiert. Die aktuelle Version findest du direkt auf der Startseite.

---

### Teil 2: Sicherheitslücke erkennen (15 Min)

Analysiere die folgenden drei Code-Beispiele und identifiziere das jeweilige Sicherheitsproblem.

#### Beispiel 1: Profil-Zugriff

```javascript
// Funktion zeigt das Profil eines Nutzers an
function zeigeProfil(userId) {
    // Hole Profildaten aus der Datenbank
    const profil = datenbank.getProfil(userId);
    
    // Zeige Profil auf der Webseite
    document.getElementById('profilName').textContent = profil.name;
    document.getElementById('profilEmail').textContent = profil.email;
    document.getElementById('profilAdresse').textContent = profil.adresse;
}

// Wird aufgerufen, wenn URL ist: /profil?user=123
const urlParameter = new URLSearchParams(window.location.search);
const userId = urlParameter.get('user');
zeigeProfil(userId);
```

**Frage:** Was ist das Problem mit diesem Code? Welches der Top 3 Sicherheitsrisiken liegt hier vor?


#### Beispiel 2: Login-Formular

```html
<!-- Login-Seite -->
<form action="http://example.com/login" method="POST">
    <input type="text" name="username" placeholder="Benutzername">
    <input type="password" name="password" placeholder="Passwort">
    <button type="submit">Anmelden</button>
</form>
```

**Beachte:** Die URL beginnt mit `http://` (nicht `https://`)

**Frage:** Was ist das Problem hier? Welches Risiko entsteht?

---

#### Beispiel 3: Such-Funktion

```javascript
// Nutzer sucht nach Projekten
function sucheProjekte(suchbegriff) {
    // SQL-Abfrage wird direkt zusammengebaut
    const query = "SELECT * FROM projekte WHERE name = '" + suchbegriff + "'";
    
    // Führe Abfrage aus
    const ergebnisse = datenbank.query(query);
    return ergebnisse;
}

// Wird aufgerufen mit Eingabe aus Suchfeld
const eingabe = document.getElementById('suchfeld').value;
sucheProjekte(eingabe);
```

**Frage:** Welches Sicherheitsproblem hat dieser Code? Was könnte ein Angreifer eingeben?

---

## Erfolgskriterien

Deine Lösung ist vollständig, wenn:

- [ ] Du die OWASP-Website besucht und die vier Fragen beantwortet hast
- [ ] Du für jedes Code-Beispiel das Sicherheitsproblem benannt hast
- [ ] Du erklärt hast, welches der Top 3 Risiken jeweils vorliegt
- [ ] Deine Antworten sind in eigenen Worten formuliert
- [ ] Die Datei `owasp-notizen.txt` existiert und alle Antworten enthält

---

## Lösungshinweise

<details>
<summary>💡 Hilfe zu Beispiel 1</summary>

Das Problem ist **Broken Access Control**. Der Code prüft nicht, ob der angemeldete Nutzer auch wirklich berechtigt ist, das Profil mit der ID `userId` zu sehen. Jemand könnte einfach die URL ändern von `/profil?user=123` zu `/profil?user=124` und würde das fremde Profil sehen.

**Lösung:** Prüfe serverseitig, ob `aktuellerNutzer.id === userId` oder ob der Nutzer Admin-Rechte hat.
</details>

<details>
<summary>💡 Hilfe zu Beispiel 2</summary>

Das Problem ist **Cryptographic Failures**. Die URL nutzt `http://` statt `https://`. Das bedeutet, das Passwort wird im Klartext über das Netzwerk übertragen. Jeder im gleichen WLAN könnte das Passwort mitlesen.

**Lösung:** Nutze immer HTTPS, damit die Verbindung verschlüsselt ist.
</details>

<details>
<summary>💡 Hilfe zu Beispiel 3</summary>

Das Problem ist **SQL Injection**. Der Suchbegriff wird direkt in die SQL-Abfrage eingefügt, ohne geprüft zu werden. Ein Angreifer könnte eingeben: `Robert'); DROP TABLE projekte;--` und würde damit die gesamte Tabelle löschen.

**Lösung:** Nutze Prepared Statements, damit Eingaben automatisch escaped werden.
</details>

---

## Reflexionsfragen

Beantworte nach Abschluss der Aufgabe:

1. **Welches der drei Risiken findest du am gefährlichsten? Warum?**
2. **Hast du auf deiner eigenen Portfolio-Seite bisher an Sicherheit gedacht? Was könntest du verbessern?**
3. **Warum reicht es nicht aus, Sicherheitsprüfungen nur im Browser (JavaScript) zu machen?**

---

## Weiterführende Links

- **OWASP Top 10 (offiziell):** [https://owasp.org/www-project-top-ten/](https://owasp.org/www-project-top-ten/)
- **OWASP Top 10 erklärt (Deutsch):** [https://owasp.org/Top10/de/](https://owasp.org/Top10/de/)
- **MDN Web Security:** [https://developer.mozilla.org/en-US/docs/Web/Security](https://developer.mozilla.org/en-US/docs/Web/Security)
- **Video: Was ist OWASP?** [https://www.youtube.com/watch?v=qMkiZ3Ehv5M](https://www.youtube.com/watch?v=qMkiZ3Ehv5M)

---

## Tipps für die Lösung

- **Nimm dir Zeit:** Sicherheit ist ein komplexes Thema. Es ist normal, wenn du nicht sofort alle Probleme erkennst.
- **Denke wie ein Angreifer:** Überlege bei jedem Code-Beispiel: "Was könnte ich hier manipulieren?"
- **Frage dich:** Was passiert, wenn jemand absichtlich falsche oder unerwartete Eingaben macht?
- **Notiere dir Begriffe:** Schreibe unbekannte Begriffe auf und schlage sie nach (z.B. "Prepared Statement", "Hashing")

---

**Nächste Aufgabe:** 02 – Sicherheitslücken beheben
