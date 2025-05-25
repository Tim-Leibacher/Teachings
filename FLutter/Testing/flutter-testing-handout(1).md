# Flutter Testing - Handout
## ÜK 335 - Mobile App Programmieren

### Lernziele
Nach dieser Lektion können Sie:
- Mobile-Applikationen gemäss Testplan überprüfen
- Testergebnisse professionell festhalten
- Erforderliche Korrekturen identifizieren und vornehmen
- Funktionale und nicht-funktionale Anforderungen testen

---

## 1. Die Test-Pyramide in Flutter

```
        Integration Tests (wenige)
            Widget Tests
          Unit Tests (viele)
```

**Regel:** Viele kleine, schnelle Tests unten - wenige grosse, langsame Tests oben!

---

## 2. Die drei Testarten

### Unit Tests
- **Was:** Einzelne Funktionen, Methoden, Klassen
- **Warum:** Schnell, isoliert, einfach zu debuggen
- **Beispiel:** Berechnungen, Validierungen, Business Logic

```dart
test('Email Validierung', () {
  expect(isValidEmail('test@test.ch'), isTrue);
  expect(isValidEmail('invalid'), isFalse);
});
```

### Widget Tests
- **Was:** UI-Komponenten und deren Verhalten
- **Warum:** Testet Darstellung und Interaktion
- **Beispiel:** Button-Clicks, Textanzeige, Navigation

```dart
testWidgets('Button Test', (tester) async {
  await tester.pumpWidget(MyButton());
  await tester.tap(find.text('Click'));
  await tester.pump();
  expect(find.text('Clicked!'), findsOneWidget);
});
```

### Integration Tests
- **Was:** Komplette User Flows
- **Warum:** Testet das Zusammenspiel aller Komponenten
- **Beispiel:** Login-Flow, Checkout-Prozess

---

## 3. Funktionale vs. Nicht-funktionale Anforderungen

### Funktionale Anforderungen ✓
Was die App **tun** soll:
- Korrekte Berechnungen
- Daten speichern/laden
- Navigation funktioniert
- API-Kommunikation
- Nutzerinteraktionen

### Nicht-funktionale Anforderungen 🎯
**Wie** die App es tun soll:

| Kategorie | Beispiele |
|-----------|-----------|
| **Performance** | Ladezeiten < 2s, 60 FPS, Speicher < 100MB |
| **Sicherheit** | Verschlüsselung, sichere Auth, Berechtigungen |
| **UX/Ergonomie** | Intuitive Bedienung, Konsistenz, Feedback |
| **Portabilität** | iOS & Android, verschiedene Screens, OS-Versionen |

---

## 4. Testplan erstellen

### Struktur eines Testfalls:
```
Test ID: TC001
Feature: Login
Priorität: Hoch
Vorbedingung: App installiert, Testuser vorhanden

Schritte:
1. App öffnen
2. Email "test@test.ch" eingeben
3. Passwort "Test1234!" eingeben
4. Login-Button klicken

Erwartetes Ergebnis: 
- Erfolgreicher Login
- Weiterleitung zum Home Screen
- Willkommensnachricht erscheint

Tatsächliches Ergebnis: ________________
Status: [ ] PASS  [ ] FAIL
```

---

## 5. Testergebnisse dokumentieren

### Bei erfolgreichem Test (PASS):
- Test ID und Name
- Datum und Tester
- Getestete Version
- Status: PASSED ✓

### Bei fehlgeschlagenem Test (FAIL):
- Fehlerbeschreibung (Was ist passiert?)
- Screenshots/Videos
- Schritte zur Reproduktion
- Logs und Fehlermeldungen
- Bug-Priorität (Kritisch/Hoch/Mittel/Niedrig)

---

## 6. Testing Commands

```bash
# Unit und Widget Tests ausführen
flutter test

# Bestimmten Test ausführen
flutter test test/login_test.dart

# Mit Coverage Report
flutter test --coverage

# Integration Tests
flutter drive --target=test_driver/app.dart

# Golden Tests updaten
flutter test --update-goldens
```

---

## 7. Best Practices Checkliste

- [ ] **Früh testen** - Nicht bis zum Schluss warten
- [ ] **Automatisieren** - CI/CD Pipeline einrichten
- [ ] **Klare Namen** - Test beschreibt was getestet wird
- [ ] **Edge Cases** - Was passiert bei ungültigen Eingaben?
- [ ] **Unabhängige Tests** - Jeder Test läuft für sich
- [ ] **Mocking verwenden** - Externe Dependencies simulieren
- [ ] **Code Coverage** - Ziel: >80% Coverage

---

## 8. Wichtige Test-Packages

| Package | Verwendung |
|---------|------------|
| `test` | Basis Test-Framework |
| `flutter_test` | Widget Testing |
| `integration_test` | Integration Tests |
| `mockito` | Mocking Framework |
| `golden_toolkit` | Screenshot Tests |
| `coverage` | Code Coverage Reports |

---

## 9. Beispiel: Vollständiger Unit Test

```dart
import 'package:test/test.dart';

class Calculator {
  double divide(double a, double b) {
    if (b == 0) throw ArgumentError('Division by zero');
    return a / b;
  }
}

void main() {
  group('Calculator Tests', () {
    late Calculator calc;
    
    setUp(() {
      calc = Calculator();
    });
    
    test('Division mit positiven Zahlen', () {
      expect(calc.divide(10, 2), equals(5));
    });
    
    test('Division mit negativen Zahlen', () {
      expect(calc.divide(-10, 2), equals(-5));
    });
    
    test('Division durch Null wirft Error', () {
      expect(
        () => calc.divide(10, 0),
        throwsArgumentError,
      );
    });
  });
}
```

---

## 10. Debugging Tipps

### Wenn ein Test fehlschlägt:
1. **Fehlermeldung genau lesen** - Was wird erwartet vs. was passiert?
2. **print() Statements** - Zwischenwerte ausgeben
3. **Kleinere Tests** - Problem isolieren
4. **Test einzeln ausführen** - Seiteneffekte ausschliessen
5. **Golden Files prüfen** - Bei UI Tests Screenshots vergleichen

---

## Notizen

_Platz für Ihre eigenen Notizen:_

_______________________________________________

_______________________________________________

_______________________________________________

_______________________________________________

_______________________________________________

---

## Weiterführende Ressourcen

- [Flutter Testing Dokumentation](https://docs.flutter.dev/testing)
- [Testing Cookbook](https://docs.flutter.dev/cookbook/testing)
- [Mockito Package](https://pub.dev/packages/mockito)
- [Integration Test Package](https://pub.dev/packages/integration_test)