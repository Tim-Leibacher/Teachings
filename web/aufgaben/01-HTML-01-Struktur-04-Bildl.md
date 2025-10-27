# Zusatzauftrag: Ein Bild in die Webseite einfügen

## Ziel

Du lernst, wie du ein Bild in eine HTML-Seite einbindest und mit einem Alternativtext versiehst.

## Beschreibung

Speichere ein Bild in demselben Ordner wie deine Datei `index.html`.  
Füge es innerhalb des `<body>`-Bereichs deiner Seite mit folgendem Tag ein:

```html
<img src="meinbild.jpg" alt="Beschreibung des Bildes">

Das Attribut `alt` ist wichtig, weil es das Bild beschreibt, falls es nicht geladen werden kann oder von Screenreadern vorgelesen wird.

## Erwartung
Ein korrekt eingefügtes Bild, das im Browser sichtbar ist und mit einem sinnvollen Alternativtext versehen wurde.

## Tipps
- Verwende Dateinamen ohne Leerzeichen (z. B. `baum.jpg` statt `Mein Bild.jpg`).  
- Teste auch ein Online-Bild mit folgendem Beispiel:

```html
  <img src="https://picsum.photos/300" alt="Beispielbild">
