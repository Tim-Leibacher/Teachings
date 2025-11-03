# Auftrag 1: "Über mich" – Deine Geschichte erzählen

## 🎯 Ziel
Du erweiterst dein Portfolio um eine aussagekräftige "Über mich"-Sektion mit logisch strukturierten Überschriften und Texten.

## 📋 Beschreibung

Jedes gute Portfolio braucht eine persönliche "Über mich"-Sektion. Du erzählst deine Geschichte als angehende/r Informatiker/in!

### Was du erstellen sollst:

Erweitere den `<main>`-Bereich deiner Portfolio-Seite:

**1. Eine Hauptüberschrift** für die Sektion:
```html
<h2>Über mich</h2>
```

**2. Drei Unterbereiche mit `<h3>`-Überschriften:**

- **Mein Werdegang**
  - Schreibe 2-3 Sätze über deinen Bildungsweg
  - Beispiel: "Nach der obligatorischen Schulzeit habe ich mich für die Lehre als Informatiker/in EFZ entschieden, weil..."

- **Meine Interessen**
  - Liste 3-4 Dinge auf, die dich in der IT interessieren
  - Beispiel: "Webentwicklung, App-Design, Cybersecurity..."

- **Meine Ziele**
  - Schreibe 2-3 Sätze über deine Ziele während und nach der Lehre
  - Beispiel: "Während meiner Lehre möchte ich fundierte Kenntnisse in Webentwicklung erlangen..."

**Beispielstruktur:**
```html
<main>
    <h2>Über mich</h2>
    
    <h3>Mein Werdegang</h3>
    <p>Nach der Sekundarschule in [Ort] entschied ich mich für eine 
    Lehre als Informatiker/in, weil...</p>
    <p>Seit August 2024 lerne ich bei [Firma] und arbeite im Team 
    für [Bereich].</p>
    
    <h3>Meine Interessen</h3>
    <p>In der IT begeistert mich besonders die Webentwicklung. 
    Ich finde es spannend, wie...</p>
    <p>Privat beschäftige ich mich mit [Hobby/Interesse].</p>
    
    <h3>Meine Ziele</h3>
    <p>Während meiner Ausbildung möchte ich vor allem...</p>
    <p>Nach der Lehre kann ich mir vorstellen...</p>
</main>
```

## ✅ Erfolgskriterien

- [ ] Die Sektion "Über mich" hat eine `<h2>`-Überschrift
- [ ] Es gibt drei Unterbereiche mit `<h3>`-Überschriften
- [ ] Jeder Unterbereich hat mindestens 2 Absätze (`<p>`)
- [ ] Die Überschriften-Hierarchie ist logisch: h1 → h2 → h3 (keine Sprünge!)
- [ ] Alle Texte sind persönlich und authentisch geschrieben
- [ ] Die Inhalte sind fehlerfrei und professionell formuliert

## 💡 Tipps

- **Überschriften gliedern Inhalte nach Wichtigkeit**, nicht nach Schriftgrösse
- Schreibe authentisch – das macht dein Portfolio einzigartig
- **Profitipp:** Nutze die Outline-Ansicht in den DevTools (F12 → Elements), um die Überschriften-Hierarchie zu prüfen
- Verwende pro Absatz nur einen Gedanken – das macht Texte lesbarer
- Achte auf korrekte Rechtschreibung – das ist Teil deiner professionellen Darstellung

## 🤔 Reflexionsfragen

1. Warum sollte nach einer `<h2>` eine `<h3>` kommen und nicht direkt eine `<h4>`?
2. Öffne die DevTools (F12) und schaue dir die Überschriften-Hierarchie an. Ist sie logisch?
3. Was würde passieren, wenn du alle Überschriften als `<h1>` definierst? Probiere es aus und mache es dann wieder rückgängig.
4. Teste: Wie wirkt deine Seite auf andere? Lass jemanden die Seite lesen und frage nach Feedback.

## 🔗 Weiterführende Links

- [MDN: Überschriften `<h1>`-`<h6>`](https://developer.mozilla.org/de/docs/Web/HTML/Element/Heading_Elements)
- [W3C: Heading Structure Best Practices](https://www.w3.org/WAI/tutorials/page-structure/headings/)
- [WebAIM: Semantic Structure](https://webaim.org/techniques/semanticstructure/)

---

**⏱️ Geschätzte Zeit:** 20-25 Minuten  
**📦 Nächster Schritt:** In Auftrag 2 formatierst du wichtige Textstellen mit `<strong>` und `<em>`!
