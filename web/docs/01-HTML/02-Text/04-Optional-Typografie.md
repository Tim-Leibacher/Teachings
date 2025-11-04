# Auftrag 4 (Optional): Typografie & Textgestaltung – Details, die den Unterschied machen

## Ziel
Du lernst fortgeschrittene HTML-Textelemente kennen und verstehst, wie Details in der Typografie deine Portfolio-Seite professioneller machen.

## Beschreibung

Professionelle Webseiten nutzen viele Text-Tags, die über `<p>` und `<strong>` hinausgehen. In diesem optionalen Auftrag lernst du die Feinheiten kennen!

---

### Teil 1: Zitate & Quellenangaben (15 Min)

**1. Blockquote – Längere Zitate**

Füge in deine "Über mich"-Sektion ein inspirierendes Zitat ein:

```html
<h2>Meine Motivation</h2>
<blockquote cite="https://www.example.com/quote">
    <p>„Der beste Weg, die Zukunft vorherzusagen, ist, sie zu erschaffen."</p>
    <footer>
        — <cite>Alan Kay</cite>, Informatiker und Pionier
    </footer>
</blockquote>
```

**2. Inline-Zitat – Kurze Zitate im Text**

```html
<p>Wie Steve Jobs einmal sagte: <q>Stay hungry, stay foolish.</q></p>
```

**Unterschied:**
- `<blockquote>` = Eigener Block, eingerückt
- `<q>` = Inline im Text, automatische Anführungszeichen

---

### Teil 2: Code & technische Begriffe (15 Min)

Als Informatiker/in solltest du Code und Befehle korrekt auszeichnen:

**1. Inline-Code mit `<code>`:**

```html
<p>In HTML beginnt jede Seite mit <code>&lt;!DOCTYPE html&gt;</code>.</p>
<p>Zum Speichern nutze ich <code>Ctrl + S</code> in VS Code.</p>
```

**2. Codeblöcke mit `<pre>` und `<code>:`**

Erstelle eine neue Sektion "Meine ersten Codezeilen":

```html
<h2>Meine ersten Codezeilen</h2>
<p>Mein erstes HTML-Dokument:</p>

<pre><code>&lt;!DOCTYPE html&gt;
&lt;html lang="de"&gt;
&lt;head&gt;
    &lt;title&gt;Mein Portfolio&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
    &lt;h1&gt;Hallo Welt!&lt;/h1&gt;
&lt;/body&gt;
&lt;/html&gt;</code></pre>
```

**3. Tastenkombinationen mit `<kbd>`:**

```html
<p>Wichtige Shortcuts:
    <ul>
        <li><kbd>Ctrl</kbd> + <kbd>S</kbd> = Speichern</li>
        <li><kbd>Ctrl</kbd> + <kbd>Z</kbd> = Rückgängig</li>
        <li><kbd>Shift</kbd> + <kbd>Alt</kbd> + <kbd>F</kbd> = Code formatieren</li>
    </ul>
</p>
```

---

### Teil 3: Abkürzungen & Definitionen (10 Min)

**1. Abkürzungen mit `<abbr>`:**

```html
<p>Ich lerne derzeit <abbr title="HyperText Markup Language">HTML</abbr> 
und <abbr title="Cascading Style Sheets">CSS</abbr>.</p>

<p>Mein Ausbildungsberuf: 
<abbr title="Informatiker/in Eidgenössisches Fähigkeitszeugnis">Informatiker/in EFZ</abbr></p>
```

**Effekt:** Beim Hover über die Abkürzung erscheint die volle Bezeichnung!

**2. Definitionen mit `<dfn>`:**

```html
<p><dfn>HTML</dfn> ist die Auszeichnungssprache für Webseiten und definiert 
die Struktur von Inhalten.</p>

<p><dfn>Semantisches HTML</dfn> bedeutet, dass Tags nach ihrer Bedeutung 
und nicht nach ihrem Aussehen gewählt werden.</p>
```

---

### Teil 4: Zeit & Datum richtig auszeichnen (10 Min)

**Mit `<time>` werden Datumsangaben maschinenlesbar:**

```html
<p>Meine Lehre begann am 
<time datetime="2024-08-01">1. August 2024</time>.</p>

<p>Letzte Aktualisierung: 
<time datetime="2025-10-29">29. Oktober 2025</time></p>
```

**Warum wichtig?**
- Suchmaschinen verstehen das Datum
- Kalender-Apps können es verarbeiten
- Screenreader können es korrekt vorlesen

---

### Teil 5: Typografische Details (10 Min)

**1. Hervorhebung mit `<mark>`:**

```html
<p>Mein Hauptziel für 2025: <mark>Eine vollständige Webanwendung 
mit React erstellen</mark>.</p>
```

**2. Durchgestrichener Text mit `<s>` (für überholte Infos):**

```html
<p><s>Bisher konnte ich nur Office-Anwendungen bedienen.</s><br>
Jetzt lerne ich Webentwicklung!</p>
```

**3. Kleine Details mit `<small>` (Fussnotengrösse):**

```html
<footer>
    <p>© 2025 Dein Name</p>
    <p><small>Erstellt im Rahmen der Ausbildung zum/zur Informatiker/in EFZ</small></p>
</footer>
```

**4. Hoch- und Tiefstellen mit `<sup>` und `<sub>`:**

```html
<p>In der Mathematik nutze ich oft x<sup>2</sup> oder H<sub>2</sub>O.</p>
```

---

## Erfolgskriterien

- [ ] Mindestens ein `<blockquote>` mit `<cite>` ist eingebaut
- [ ] Technische Begriffe sind mit `<code>`, `<kbd>` oder `<pre>` ausgezeichnet
- [ ] Mindestens 2-3 Abkürzungen nutzen `<abbr>` mit title-Attribut
- [ ] Mindestens ein Datum ist mit `<time>` und datetime-Attribut markiert
- [ ] Der Code ist sauber formatiert und eingerückt
- [ ] Die neuen Elemente sind sinnvoll eingesetzt (nicht wahllos)
- [ ] Beim Hover über `<abbr>` erscheint die Erklärung

## Tipps

- **HTML-Entities beachten:** In Code-Beispielen musst du `<` und `>` escapen:
  - `<` wird zu `&lt;`
  - `>` wird zu `&gt;`
- `<pre>` behält Leerzeichen und Zeilenumbrüche bei – perfekt für Code!
- **Accessibility-Tipp:** `<abbr>` hilft Screenreader-Nutzern, Abkürzungen zu verstehen
- Nutze den HTML-Validator, um Fehler zu finden: [validator.w3.org](https://validator.w3.org/)
- **Profitrick:** Kombiniere Tags sinnvoll: `<strong><code>HTML</code></strong>`

## Reflexionsfragen

1. Was ist der Unterschied zwischen `<blockquote>` und `<q>`? Wann nutzt du was?
2. Warum sollte man für Code `<code>` statt nur `<span>` verwenden?
3. Teste: Erstelle eine Abkürzung mit `<abbr>` und hover darüber. Was siehst du?
4. Recherchiere: Welchen Vorteil hat das `datetime`-Attribut bei `<time>` für Suchmaschinen?
5. Öffne eine professionelle Website (z.B. developer.mozilla.org) und inspiziere den Code. Welche der gelernten Tags findest du?

## 🔗 Weiterführende Links

**Zitate & Quellen:**
- [MDN: `<blockquote>`](https://developer.mozilla.org/de/docs/Web/HTML/Element/blockquote)
- [MDN: `<cite>`](https://developer.mozilla.org/de/docs/Web/HTML/Element/cite)
- [MDN: `<q>` – Inline-Zitate](https://developer.mozilla.org/de/docs/Web/HTML/Element/q)

**Code-Darstellung:**
- [MDN: `<code>`](https://developer.mozilla.org/de/docs/Web/HTML/Element/code)
- [MDN: `<pre>`](https://developer.mozilla.org/de/docs/Web/HTML/Element/pre)
- [MDN: `<kbd>`](https://developer.mozilla.org/de/docs/Web/HTML/Element/kbd)

**Abkürzungen & Zeit:**
- [MDN: `<abbr>`](https://developer.mozilla.org/de/docs/Web/HTML/Element/abbr)
- [MDN: `<time>`](https://developer.mozilla.org/de/docs/Web/HTML/Element/time)
- [Schema.org: DateTime](https://schema.org/DateTime)

**Typografie:**
- [MDN: Text-Level Semantics](https://developer.mozilla.org/en-US/docs/Web/HTML/Element#text_content)
- [HTML Living Standard](https://html.spec.whatwg.org/multipage/text-level-semantics.html)

## Bonus-Challenge

1. **Erstelle eine "Changelog"-Sektion:**
   - Liste alle Updates deiner Portfolio-Seite auf
   - Nutze `<time>` für jedes Datum
   - Verwende `<code>` für technische Änderungen

2. **Baue ein Glossar:**
   - Erstelle eine Liste mit IT-Begriffen
   - Nutze `<dfn>` für Definitionen
   - Verwende `<abbr>` für Abkürzungen

3. **Code-Snippet-Sammlung:**
   - Erstelle eine Sektion mit deinen liebsten Code-Snippets
   - Formatiere sie mit `<pre>` und `<code>`
   - Füge Erklärungen in `<p>`-Tags hinzu

---

**⏱️ Geschätzte Zeit:** 45-60 Minuten  
**🎓 Schwierigkeitsgrad:** Fortgeschritten  
**📦 Nächster Schritt:** Weiter zu HTML-Links & Bilder – mache dein Portfolio interaktiv!

---

**💬 Hinweis:** Diese Tags machen deine Seite nicht nur schöner, sondern auch semantisch korrekter und zugänglicher. Professionelle Entwickler/innen achten auf diese Details!
