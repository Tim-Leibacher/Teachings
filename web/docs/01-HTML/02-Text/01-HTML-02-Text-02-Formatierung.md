# Auftrag 2: Wichtiges hervorheben – Textformatierung mit Bedeutung

## 🎯 Ziel
Du lernst, wie du Texte semantisch korrekt hervorhebst und verstehst den Unterschied zwischen visueller und inhaltlicher Betonung.

## 📋 Beschreibung

Nicht alle Wörter sind gleich wichtig! Mit HTML kannst du **wichtige Inhalte** und *betonte Aussagen* kennzeichnen – nicht nur für Leser/innen, sondern auch für Screenreader und Suchmaschinen.

### Die zwei wichtigsten Tags:

**`<strong>` – für wichtige Inhalte**
- Signalisiert: "Das ist wichtig!"
- Wird standardmässig **fett** dargestellt
- Beispiel: Firmennamen, Kernaussagen, Warntexte

**`<em>` – für Betonung**
- Signalisiert: "Das ist betont/hervorgehoben"
- Wird standardmässig *kursiv* dargestellt
- Beispiel: Fremdwörter, besondere Formulierungen

### Deine Aufgabe:

Gehe durch deine "Über mich"-Sektion und markiere:

1. **3-5 wichtige Begriffe** mit `<strong>`:
   - Dein Ausbildungsberuf
   - Den Namen deiner Lehrfirma
   - Wichtige Fähigkeiten oder Ziele

2. **2-3 betonte Aussagen** mit `<em>`:
   - Besonders wichtige Interessen
   - Motivationen oder Überzeugungen

3. **Füge 1-2 Zeilenumbrüche ein** mit `<br>`:
   - Dort, wo eine kurze Pause den Text besser gliedert
   - Z.B. vor einem wichtigen Satz oder nach einer Aufzählung

**Beispiel:**
```html
<h3>Mein Werdegang</h3>
<p>Seit August 2024 lerne ich bei <strong>Firma XY AG</strong> als 
<strong>Informatiker/in EFZ Applikationsentwicklung</strong>.</p>
<p>Was mich besonders motiviert: <em>Ich möchte verstehen, wie das Web 
funktioniert</em> – von HTML bis zu komplexen Webanwendungen.</p>

<h3>Meine Interessen</h3>
<p>In der IT begeistert mich besonders:<br>
<strong>Webentwicklung</strong>, <strong>UI/UX Design</strong> und 
<em>kreatives Problemlösen</em>.</p>
```

## ✅ Erfolgskriterien

- [ ] Mindestens 3-5 Begriffe sind mit `<strong>` markiert
- [ ] Mindestens 2-3 Aussagen sind mit `<em>` betont
- [ ] 1-2 Zeilenumbrüche (`<br>`) sind sinnvoll platziert
- [ ] Die Hervorhebungen machen inhaltlich Sinn (nicht willkürlich gesetzt)
- [ ] Der Text bleibt lesbar und ist nicht "überladen"
- [ ] Im Browser sind die Hervorhebungen sichtbar

## 💡 Tipps

- **Weniger ist mehr:** Übertreib es nicht – zu viele Hervorhebungen wirken unprofessionell
- `<strong>` ≠ `<b>` und `<em>` ≠ `<i>` – die semantischen Tags haben Bedeutung!
- **Profitipp:** Teste mit einem Screenreader (NVDA, VoiceOver) – `<strong>` und `<em>` werden anders vorgelesen
- Nutze `<br>` sparsam – oft ist ein neuer `<p>`-Tag die bessere Wahl
- **Accessibility-Hinweis:** Screenreader betonen `<strong>` und `<em>` automatisch

## 🤔 Reflexionsfragen

1. Was ist der Unterschied zwischen `<strong>` und `<b>`? Wann würdest du was verwenden?
2. Warum sollte man `<br>` nicht für grössere Abstände verwenden? Was wäre die Alternative?
3. Teste: Markiere einen ganzen Absatz mit `<strong>`. Was passiert? Warum ist das keine gute Idee?
4. Öffne die DevTools (F12) → Elements: Siehst du den Unterschied zwischen `<b>` und `<strong>` im Code?

## 🔗 Weiterführende Links

- [MDN: `<strong>` – Stark wichtiger Text](https://developer.mozilla.org/de/docs/Web/HTML/Element/strong)
- [MDN: `<em>` – Betonter Text](https://developer.mozilla.org/de/docs/Web/HTML/Element/em)
- [MDN: `<br>` – Zeilenumbruch](https://developer.mozilla.org/de/docs/Web/HTML/Element/br)
- [Accessibility: Semantic HTML](https://webaim.org/techniques/semanticstructure/)

---

**⏱️ Geschätzte Zeit:** 15-20 Minuten  
**📦 Nächster Schritt:** In Auftrag 3 strukturierst du deine Skills mit Listen!
