# Flutter Testing - Lehrerleitfaden
## ÜK 335 - Mobile App Programmieren (60 Minuten)

### Vorbereitung
- [ ] Präsentation auf Beamer testen
- [ ] Handouts ausdrucken (2 Exemplare)
- [ ] Flutter Projekt mit Tests vorbereitet
- [ ] IDE mit Beispielcode bereit

---

## Zeitplan (60 Minuten)

### Einführung (5 Min)
- **Slide 1-2:** Begrüssung und Lernziele
- **Aktivität:** Kurze Umfrage - Wer hat schon mal Tests geschrieben?
- **Kernbotschaft:** Testing ist eine Investition, keine Last

### Warum Testing? (5 Min)
- **Slide 3:** Vergleich mit/ohne Testing
- **Beispiel aus Praxis:** Bug in Produktion vs. Bug im Test gefunden
- **Kosten-Nutzen:** 1 Stunde Testing spart 10 Stunden Debugging

### Test-Pyramide & Arten (10 Min)
- **Slide 4-5:** Test-Pyramide visualisieren
- **Interaktion:** Lernende fragen welche Tests sie für eine Taschenrechner-App schreiben würden
- **Betonung:** Balance zwischen Testarten

### Unit Testing (8 Min)
- **Slide 6:** Theorie und Syntax
- **Live-Demo:** Einfachen Test in IDE schreiben und ausführen
- **Zeigen:** 
  - Test schreiben
  - Test ausführen
  - Test fehlschlagen lassen (Red-Green-Refactor)

### Widget Testing (8 Min)
- **Slide 7:** Widget Test Konzept
- **Live-Demo:** Button Test
- **Wichtig:** `pumpWidget()` und `pump()` erklären
- **Tipp:** Keys für Widgets verwenden

### Integration Testing (7 Min)
- **Slide 8:** Unterschied zu anderen Tests
- **Video/Demo:** Zeigen wie ein Integration Test läuft
- **Erwähnen:** Langsamer aber wichtig für kritische Flows

### Funktionale vs. Nicht-funktionale (8 Min)
- **Slide 9-10:** Klare Unterscheidung
- **Gruppenarbeit:** Lernende kategorisieren Beispiele (2 Min)
- **Beispiele:**
  - "Button speichert Daten" → Funktional
  - "App lädt in unter 2 Sekunden" → Nicht-funktional

### Testplan & Dokumentation (5 Min)
- **Slide 11-12:** Struktur zeigen
- **Praxis-Tipp:** Excel/Tool für Testplan Management
- **Betonen:** Reproduzierbarkeit ist key

### Best Practices & Tools (3 Min)
- **Slide 13-14:** Schnell durchgehen
- **Fokus:** CI/CD Wichtigkeit betonen
- **Ausblick:** GitHub Actions als Beispiel

### Abschluss (1 Min)
- **Slide 18-19:** Zusammenfassung
- **Überleitung:** Zu den praktischen Übungen

---

## Wichtige Konzepte zum Betonen

### 1. Test-First Mindset
- Tests sind keine Zusatzarbeit
- Tests als Dokumentation
- Tests geben Sicherheit bei Refactoring

### 2. Praktische Tipps
- Klein anfangen - ein Test ist besser als kein Test
- Failing Test zuerst (Red-Green-Refactor)
- Tests sollten schnell laufen

### 3. Häufige Fehler vermeiden
- Zu viele Integration Tests
- Tests die von Reihenfolge abhängen
- Keine Mocks verwenden

---

## Antworten auf häufige Fragen

**"Ist Testing nicht Zeitverschwendung?"**
- Kurzfristig mehr Arbeit, langfristig massive Zeitersparnis
- Bugs in Produktion sind 10-100x teurer zu fixen

**"Wie viel Coverage brauche ich?"**
- 80% ist ein guter Zielwert
- 100% ist oft nicht sinnvoll (Diminishing Returns)
- Kritische Business Logic sollte 100% haben

**"Was wenn sich Requirements ändern?"**
- Tests müssen mitgepflegt werden
- Tests helfen zu verstehen was alles angepasst werden muss

---

## Praktische Demonstrationen

### Demo 1: Unit Test Live Coding
```dart
// 1. Zeigen: Funktion ohne Test
int calculateAge(DateTime birthDate) {
  final now = DateTime.now();
  int age = now.year - birthDate.year;
  if (now.month < birthDate.month ||
      (now.month == birthDate.month && now.day < birthDate.day)) {
    age--;
  }
  return age;
}

// 2. Test schreiben
test('calculateAge berechnet Alter korrekt', () {
  // Arrange
  final birthDate = DateTime(2000, 6, 15);
  
  // Act
  final age = calculateAge(birthDate);
  
  // Assert
  expect(age, greaterThanOrEqualTo(24)); // Je nach aktuellem Datum
});

// 3. Edge Case zeigen
test('calculateAge funktioniert für Geburtstag heute', () {
  final today = DateTime.now();
  final birthDate = DateTime(today.year - 25, today.month, today.day);
  expect(calculateAge(birthDate), equals(25));
});
```

### Demo 2: Widget Test mit Interaktion
```dart
// Live coden und Schritt für Schritt erklären
testWidgets('Counter increments', (tester) async {
  // Build our app and trigger a frame
  await tester.pumpWidget(MyApp());
  
  // Verify initial state
  expect(find.text('0'), findsOneWidget);
  expect(find.text('1'), findsNothing);
  
  // Tap the '+' icon and trigger a frame
  await tester.tap(find.byIcon(Icons.add));
  await tester.pump();
  
  // Verify counter has incremented
  expect(find.text('0'), findsNothing);
  expect(find.text('1'), findsOneWidget);
});
```

---

## Verbindung zu Übungen

Nach der Theorie:
1. **Kurze Pause** (5 Min)
2. **Übungsblatt verteilen**
3. **Erste Übung gemeinsam starten**
4. **Lernende selbstständig arbeiten lassen**
5. **Herumgehen und unterstützen**

### Zeitaufteilung Übungen:
- Übung 1 (Unit Test): 15 Min
- Übung 2 (Widget Test): 20 Min  
- Besprechung Lösungen: 10 Min
- Weitere Übungen als Hausaufgabe

---

## Zusatzmaterial bei Zeitüberschuss

### Golden Testing
```dart
await expectLater(
  find.byType(MyWidget),
  matchesGoldenFile('goldens/my_widget.png'),
);
```

### Performance Testing
```dart
await tester.traceAction(() async {
  // Action to measure
}, reportKey: 'scrolling_performance');
```

### Accessibility Testing
```dart
expect(tester.getSemantics(find.text('Login')), 
  matchesSemantics(label: 'Login Button'));
```

---

## Erfolgskontrolle

Am Ende sollten Lernende:
- [ ] Den Unterschied zwischen Test-Arten kennen
- [ ] Einen einfachen Unit Test schreiben können
- [ ] Verstehen warum Testing wichtig ist
- [ ] Einen Testplan erstellen können

## Notizen für nächstes Mal

_Platz für Ihre Beobachtungen:_

________________________________

________________________________

________________________________