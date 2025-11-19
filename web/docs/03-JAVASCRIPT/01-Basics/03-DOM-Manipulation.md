# Auftrag 3: Erste DOM-Manipulation – Inhalte dynamisch ändern

## Ziel

Du lernst, mit JavaScript auf HTML-Elemente zuzugreifen und deren Inhalte dynamisch zu ändern. Das ist der erste Schritt zu interaktiven Websites.

## Beschreibung

**DOM (Document Object Model)** ist die Brücke zwischen HTML und JavaScript. JavaScript kann damit auf jedes HTML-Element zugreifen und es verändern – ohne die Seite neu zu laden. Das macht Websites interaktiv und dynamisch.

In diesem Auftrag änderst du Text, zeigst dynamische Daten an und passt Styles per JavaScript an.

---

### Teil 1: HTML vorbereiten – Interaktive Elemente (15 Min)

**Aufgabe:**
Füge in deiner `index.html` eine neue Sektion für interaktive Demos ein.

**1.1 Grundstruktur**
Erstelle eine `<section>` mit der ID `interaktiv` nach deinem bestehenden Portfolio-Inhalt.

**1.2 Demo-Boxen erstellen**
Erstelle **vier** Demo-Boxen (mit `class="demo-box"`), jeweils mit:
- Einem `<h3>` als Überschrift
- Einem Textbereich (z.B. `<p>`) mit eindeutiger ID

**Die vier Demos sollen sein:**

**Demo 1: Dynamischer Text**
- Überschrift: "Dynamischer Text"
- Paragraph mit ID `demo-text` und Platzhalter-Text

**Demo 2: Aktuelle Uhrzeit**
- Überschrift: "Aktuelle Uhrzeit"
- Text: "Es ist jetzt: " und ein `<span>` mit ID `aktuelle-zeit`
- Platzhalter im Span: "--:--:--"

**Demo 3: Persönliche Begrüssung**
- Überschrift: "Persönliche Begrüssung"
- Paragraph mit ID `begruessung` und Platzhalter "Lade Begrüssung..."

**Demo 4: Besucher-Zähler**
- Überschrift: "Besucher-Statistik"
- Text: "Du bist Besucher Nummer: " und ein `<strong>` mit ID `besucher-nr`
- Platzhalter: "0"

**Wichtig:**
- Jede Demo-Box bekommt die Klasse `demo-box` (für späteres Styling)
- Jedes dynamische Element bekommt eine eindeutige ID
- IDs verwenden Kleinbuchstaben und Bindestriche (z.B. `demo-text`)

**Nachschlagen:**
- [MDN: HTML id attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/id) - IDs setzen
- [MDN: HTML class attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/class) - Klassen nutzen

---

### Teil 2: DOM-Grundlagen – Text ändern (20 Min)

**Aufgabe:**
Erstelle eine neue Datei **`dom.js`** und binde sie in deine `index.html` ein (nach `script.js`).

**2.1 Auf Elemente zugreifen**

Recherchiere die Methode `document.getElementById()` und nutze sie, um:
- Auf das Element mit ID `demo-text` zuzugreifen
- Den Zugriff in der Konsole zu loggen (zum Testen)

**2.2 Text ändern**

Ändere den Textinhalt des Elements auf: "JavaScript hat diesen Text geändert!"

**Hinweis:** Nutze die Eigenschaft `.textContent`

**2.3 Alternative Methode**

Recherchiere `document.querySelector()` und verwende diese Methode, um:
- Auf das Element mit ID `begruessung` zuzugreifen
- Eine Begrüssung mit deinem Namen einzufügen

**2.4 HTML einfügen**

Erweitere die Begrüssung so, dass dein Name **fett** dargestellt wird und darunter ein kursiver Text steht: "Schön, dass du da bist."

**Hinweis:** Nutze `.innerHTML` statt `.textContent` (recherchiere den Unterschied!)

**Nachschlagen:**
- [MDN: getElementById](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementById) - Element per ID finden
- [MDN: querySelector](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector) - Element per CSS-Selektor finden
- [MDN: textContent](https://developer.mozilla.org/en-US/docs/Web/API/Node/textContent) - Text ändern
- [MDN: innerHTML](https://developer.mozilla.org/en-US/docs/Web/API/Element/innerHTML) - HTML ändern
- [W3Schools: HTML DOM](https://www.w3schools.com/js/js_htmldom.asp) - DOM-Grundlagen

**Sicherheitshinweis:** `.innerHTML` kann gefährlich sein, wenn du Benutzereingaben verarbeitest (XSS-Angriffe). Für statische Inhalte ist es aber ok.

---

### Teil 3: Aktuelle Uhrzeit anzeigen (25 Min)

**Aufgabe:**
Erstelle eine Echtzeit-Uhr, die jede Sekunde aktualisiert wird.

**3.1 Funktion erstellen**

Erstelle eine Funktion `zeigeUhrzeit()`, die:
1. Ein neues `Date`-Objekt erstellt
2. Stunden, Minuten und Sekunden extrahiert
3. Die Zeit im Format "HH:MM:SS" anzeigt
4. Das Element mit ID `aktuelle-zeit` aktualisiert

**Hinweise:**
- Recherchiere `Date`-Objekt und dessen Methoden
- Für `getHours()`, `getMinutes()`, `getSeconds()`
- Zahlen unter 10 brauchen eine führende Null (z.B. "09" statt "9")

**3.2 Führende Nullen**

Implementiere eine Logik, die einstellige Zahlen mit "0" ergänzt.

**Tipp:** Nutze einen ternären Operator oder eine if-Bedingung:
```javascript
// Wenn Zahl < 10, dann "0" davor, sonst Zahl selbst
zahl < 10 ? "0" + zahl : zahl
```

**3.3 Zeit formatieren**

Kombiniere Stunden, Minuten und Sekunden zu einem String im Format "HH:MM:SS".

**Tipp:** Nutze Template Strings: `` `${stunden}:${minuten}:${sekunden}` ``

**3.4 Automatische Aktualisierung**

- Rufe die Funktion einmal sofort auf (beim Laden der Seite)
- Recherchiere `setInterval()` um die Funktion jede Sekunde (1000ms) auszuführen

**Nachschlagen:**
- [MDN: Date](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) - Datum/Uhrzeit
- [MDN: setInterval](https://developer.mozilla.org/en-US/docs/Web/API/setInterval) - Wiederholte Ausführung
- [JavaScript.info: Scheduling](https://javascript.info/settimeout-setinterval) - Timing-Funktionen

**Test:** Die Uhrzeit sollte sich jede Sekunde automatisch aktualisieren!

---

### Teil 4: Besucher-Zähler mit LocalStorage (20 Min)

**Aufgabe:**
Implementiere einen Besucher-Zähler, der bei jedem Seitenaufruf hochzählt.

**4.1 LocalStorage verstehen**

Recherchiere `localStorage`:
- Wie speichert man Daten? (`setItem`)
- Wie liest man Daten? (`getItem`)
- Was passiert, wenn ein Schlüssel nicht existiert?

**4.2 Funktion erstellen**

Erstelle eine Funktion `zeigeBesucher()`, die:
1. Den aktuellen Zählerstand aus `localStorage` holt (Schlüssel: "besucherNummer")
2. Falls kein Wert vorhanden ist, startet mit 0
3. Den Zähler um 1 erhöht
4. Den neuen Wert zurück in `localStorage` speichert
5. Den Wert im Element mit ID `besucher-nr` anzeigt

**Hinweise:**
- Werte aus `localStorage` sind immer Strings!
- Nutze `parseInt()` um Strings in Zahlen umzuwandeln
- Mit `||` kannst du einen Standardwert definieren: `wert || 0`

**4.3 Funktion aufrufen**

Rufe die Funktion beim Laden der Seite auf.

**Nachschlagen:**
- [MDN: Web Storage API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API) - localStorage
- [MDN: parseInt](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseInt) - String zu Zahl
- [W3Schools: LocalStorage](https://www.w3schools.com/html/html5_webstorage.asp) - Beispiele

**Test:** Lade die Seite mehrmals neu (F5) – der Zähler sollte steigen!

**Debug:** Öffne DevTools → Application → Local Storage um gespeicherte Werte zu sehen.

---

### Teil 5: Tagesabhängige Begrüssung (25 Min)

**Aufgabe:**
Erweitere die Begrüssung um eine zeitabhängige Nachricht.

**5.1 Funktion planen**

Erstelle eine Funktion `zeigeTagesbegruessung()`, die verschiedene Begrüssungen je nach:
- Tageszeit (Morgen, Tag, Abend, Nacht)
- Wochentag (Montag bis Sonntag)

**5.2 Tageszeit ermitteln**

Erstelle Bedingungen für:
- Morgen: 5:00 - 11:59 Uhr
- Tag: 12:00 - 17:59 Uhr
- Abend: 18:00 - 21:59 Uhr
- Nacht: 22:00 - 4:59 Uhr

Weise jeder Tageszeit eine passende Begrüssung und ein Emoji zu.

**Tipp:** Nutze `if...else if...else` Struktur oder einen ternären Operator.

**5.3 Wochentag ermitteln**

Recherchiere `getDay()` - diese Methode gibt Zahlen 0-6 zurück (0 = Sonntag).

Erstelle eine Zuordnung von Zahlen zu Wochentagen (z.B. mit Array oder if-Kaskade).

**5.4 Nachricht zusammenstellen**

Kombiniere Emoji, Begrüssung und Wochentag zu einer formatierten Nachricht.

**Beispiel:**
```
☀️ Guten Morgen! Heute ist Montag.
```

**5.5 Im HTML anzeigen**

- Zeige die Nachricht im Element mit ID `begruessung` an
- Die Hauptnachricht soll **fett** sein
- Darunter ein kursiver Text: "Willkommen auf meinem Portfolio!"

**Nachschlagen:**
- [MDN: Date.prototype.getDay](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/getDay) - Wochentag
- [MDN: if...else](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/if...else) - Bedingungen
- [JavaScript.info: Conditional operators](https://javascript.info/ifelse) - Verzweigungen

---

### Teil 6: Styles dynamisch ändern (20 Min)

**Aufgabe:**
JavaScript kann auch CSS-Styles direkt ändern.

**6.1 Dark Mode basierend auf Uhrzeit**

Erstelle eine Funktion `anpasseFarben()`, die:
- Die aktuelle Stunde ermittelt
- Tagsüber (6-17 Uhr): Heller Hintergrund, dunkle Schrift
- Nachts (18-5 Uhr): Dunkler Hintergrund, helle Schrift

Ändere die Styles von `document.body`:
- `backgroundColor`
- `color`

**Hinweis:** Styles änderst du mit `element.style.eigenschaft = "wert"`

**6.2 Animation für Demo-Boxen**

Erstelle einen Einblende-Effekt für alle Demo-Boxen:

1. Finde alle Elemente mit Klasse `demo-box`
    - Recherchiere `querySelectorAll()`
    - Das gibt ein Array-ähnliches Objekt zurück

2. Für jede Box:
    - Setze initial `opacity: 0`
    - Füge eine `transition` hinzu
    - Ändere `opacity` auf `1`
    - Nutze eine zeitliche Verzögerung pro Box (z.B. 200ms * Index)

**Hinweise:**
- Nutze `.forEach()` um über alle Boxen zu iterieren
- Nutze `setTimeout()` für die Verzögerung
- Der Index wird als zweiter Parameter in `.forEach()` übergeben

**Nachschlagen:**
- [MDN: HTMLElement.style](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/style) - Styles ändern
- [MDN: querySelectorAll](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelectorAll) - Mehrere Elemente
- [MDN: forEach](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach) - Iteration
- [MDN: setTimeout](https://developer.mozilla.org/en-US/docs/Web/API/setTimeout) - Verzögerung

---

## Erfolgskriterien

- [ ] HTML mit vier interaktiven Demo-Boxen ist erstellt (mit IDs)
- [ ] `dom.js` ist erstellt und eingebunden
- [ ] Text wird dynamisch mit `.textContent` geändert
- [ ] Aktuelle Uhrzeit wird jede Sekunde aktualisiert (Format: HH:MM:SS)
- [ ] Tagesabhängige Begrüssung funktioniert (Tageszeit + Wochentag)
- [ ] Besucher-Zähler funktioniert (steigt bei jedem Neuladen)
- [ ] Styles werden dynamisch angepasst (z.B. Dark Mode nachts)
- [ ] Animation für Demo-Boxen funktioniert (gestaffeltes Einblenden)
- [ ] Keine Fehlermeldungen in der Konsole

---

## Zusatzaufgaben (Optional)

**Für Schnelle:**

**A) Countdown bis Lehrabschluss**
- Berechne die verbleibenden Tage bis zum Lehrabschluss
- Zeige: "Noch X Tage bis zum Lehrabschluss"
- Aktualisiere täglich (nicht jede Sekunde!)

**B) Browser-Info-Anzeige**
Erstelle eine fünfte Demo-Box, die anzeigt:
- Browser-Name (vereinfacht aus `navigator.userAgent`)
- Bildschirmauflösung
- Verfügbare Bildschirmfläche (`screen.availWidth`)
- Sprache (`navigator.language`)

**C) LocalStorage Manager**
Erstelle Funktionen:
- `zeigeAlleLocalStorageKeys()` - listet alle gespeicherten Schlüssel
- `loescheBesucher()` - setzt den Besucher-Zähler zurück
- Zeige diese Infos in einer separaten Demo-Box

**D) Progressive Farbänderung**
Statt abruptem Wechsel: Interpoliere die Farben basierend auf der Uhrzeit.
- Recherchiere HSL-Farben
- Berechne Farbton basierend auf Stunde

**Nachschlagen:**
- [MDN: Screen](https://developer.mozilla.org/en-US/docs/Web/API/Screen) - Bildschirm-Info
- [MDN: Navigator](https://developer.mozilla.org/en-US/docs/Web/API/Navigator) - Browser-Info
- [MDN: HSL Colors](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value/hsl) - Farbmodell

---

## Tipps

- **IDs müssen eindeutig sein:** Jede ID darf nur einmal pro Seite vorkommen
- **Klassen für Mehrfachauswahl:** Nutze `.querySelectorAll()` für mehrere Elemente
- **DevTools nutzen:** Inspiziere Elemente (Rechtsklick → Untersuchen)
- **LocalStorage zurücksetzen:** `localStorage.clear()` in der Konsole
- **Performance:** `setInterval` mit 1000ms ist ok, bei 100ms wird's ineffizient
- **Debugging:** Logge Zwischenwerte mit `console.log()`

---

## Reflexionsfragen

1. **Was ist der Unterschied zwischen `.textContent` und `.innerHTML`?**  
   *Wann würdest du welche Methode nutzen? Was sind Sicherheitsrisiken?*

2. **Warum steht das `<script>`-Tag vor `</body>` und nicht im `<head>`?**  
   *Was würde passieren, wenn JavaScript auf ein noch nicht existierendes Element zugreift?*

3. **Experimentiere: Ändere die Uhrzeit-Aktualisierung von 1000ms auf 100ms. Was bemerkst du?**  
   *Ist das sinnvoll? Denk an Performance und Lesbarkeit.*

4. **LocalStorage vs. SessionStorage – wo ist der Unterschied?**  
   *Teste: Erstelle `sessionStorage.setItem("test", "wert")` und schliesse den Tab. Was passiert?*

5. **Öffne DevTools → Elements Tab. Ändere Styles live per JavaScript. Siehst du die Änderungen im Elements-Panel?**  
   *Vergleiche mit direkten CSS-Änderungen.*

6. **Recherchiere: Was passiert, wenn du `setInterval()` mehrfach aufrufst ohne `clearInterval()`?**  
   *Teste es und erkläre das Problem (Memory Leak).*

---

## Weiterführende Links

**DOM-Manipulation:**
- [MDN: DOM Introduction](https://developer.mozilla.org/de/docs/Web/API/Document_Object_Model/Introduction)
- [MDN: Document](https://developer.mozilla.org/en-US/docs/Web/API/Document) - Alle Methoden
- [JavaScript.info: DOM Navigation](https://javascript.info/dom-navigation) - DOM-Baum verstehen

**Timing-Funktionen:**
- [JavaScript.info: Scheduling](https://javascript.info/settimeout-setinterval)
- [MDN: setInterval best practices](https://developer.mozilla.org/en-US/docs/Web/API/setInterval#examples)

**LocalStorage:**
- [MDN: Web Storage API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API/Using_the_Web_Storage_API)
- [W3Schools: LocalStorage](https://www.w3schools.com/html/html5_webstorage.asp)

**Best Practices:**
- [Google: DOM Performance](https://web.dev/dom-size/)
- [JavaScript.info: Modifying the document](https://javascript.info/modifying-document)

---

## Lernziele-Check

Nach diesem Auftrag kannst du:
- [ ] Auf HTML-Elemente per ID zugreifen
- [ ] Text-Inhalte dynamisch ändern
- [ ] Mit dem Date-Objekt arbeiten
- [ ] Funktionen erstellen und aufrufen
- [ ] setInterval() für wiederholte Ausführung nutzen
- [ ] LocalStorage verwenden (lesen/schreiben)
- [ ] CSS-Styles per JavaScript ändern
- [ ] Mehrere Elemente mit querySelectorAll() bearbeiten
- [ ] Bedingte Logik (if/else) anwenden
- [ ] Dokumentation selbstständig nutzen und anwenden

---

**⏱️ Geschätzte Zeit:** 105 Minuten  
**📦 Nächster Schritt:** Im optionalen Auftrag 4 erstellst du ein interaktives Skill-Rating-System mit Buttons und Events!