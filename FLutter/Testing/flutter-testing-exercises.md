# Flutter Testing - Übungsaufgaben
## ÜK 335 - Mobile App Programmieren

### Übung 1: Unit Test schreiben (15 Min)

Sie haben folgende Klasse für einen Warenkorb:

```dart
class ShoppingCart {
  final List<CartItem> items = [];
  
  void addItem(CartItem item) {
    items.add(item);
  }
  
  void removeItem(String productId) {
    items.removeWhere((item) => item.productId == productId);
  }
  
  double getTotalPrice() {
    return items.fold(0, (sum, item) => sum + (item.price * item.quantity));
  }
  
  int getTotalItems() {
    return items.fold(0, (sum, item) => sum + item.quantity);
  }
}

class CartItem {
  final String productId;
  final String name;
  final double price;
  final int quantity;
  
  CartItem({
    required this.productId,
    required this.name,
    required this.price,
    required this.quantity,
  });
}
```

**Aufgabe:** Schreiben Sie Unit Tests für:
1. Artikel hinzufügen
2. Artikel entfernen
3. Gesamtpreis berechnen
4. Gesamtanzahl berechnen

**Tipp:** Denken Sie an Edge Cases (leerer Warenkorb, negative Preise, etc.)

---

### Übung 2: Widget Test erstellen (20 Min)

Gegeben ist folgender Counter-Widget:

```dart
class CounterWidget extends StatefulWidget {
  @override
  _CounterWidgetState createState() => _CounterWidgetState();
}

class _CounterWidgetState extends State<CounterWidget> {
  int _counter = 0;
  
  void _increment() {
    setState(() {
      _counter++;
    });
  }
  
  void _decrement() {
    setState(() {
      if (_counter > 0) _counter--;
    });
  }
  
  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        Text('Counter: $_counter', key: Key('counter_text')),
        Row(
          children: [
            IconButton(
              key: Key('decrement_button'),
              icon: Icon(Icons.remove),
              onPressed: _decrement,
            ),
            IconButton(
              key: Key('increment_button'),
              icon: Icon(Icons.add),
              onPressed: _increment,
            ),
          ],
        ),
      ],
    );
  }
}
```

**Aufgabe:** Schreiben Sie Widget Tests die überprüfen:
1. Initial wird "Counter: 0" angezeigt
2. Nach Klick auf + wird der Counter erhöht
3. Nach Klick auf - wird der Counter verringert
4. Der Counter kann nicht unter 0 fallen

---

### Übung 3: Testplan erstellen (15 Min)

Sie entwickeln eine Todo-App mit folgenden Features:
- Todo hinzufügen
- Todo als erledigt markieren
- Todo löschen
- Todos nach Priorität sortieren
- Todos durchsuchen

**Aufgabe:** Erstellen Sie einen Testplan mit mindestens 5 Testfällen. Verwenden Sie folgende Vorlage:

```
Test ID: TC00X
Feature: [Feature Name]
Priorität: [Kritisch/Hoch/Mittel/Niedrig]
Testtyp: [Unit/Widget/Integration]

Vorbedingung:
[Was muss gegeben sein?]

Testschritte:
1. [Schritt 1]
2. [Schritt 2]
3. ...

Erwartetes Ergebnis:
[Was sollte passieren?]

Notizen:
[Besonderheiten, Edge Cases]
```

---

### Übung 4: Bug Report schreiben (10 Min)

Bei einem Test ist folgender Fehler aufgetreten:
- **Szenario:** Login mit korrekten Daten
- **Erwartet:** Weiterleitung zum Home Screen
- **Tatsächlich:** App stürzt ab mit Fehlermeldung "Null check operator used on a null value"
- **Schritte:** 
  1. App öffnen
  2. Email "user@test.ch" eingeben
  3. Passwort "Test123!" eingeben
  4. Login Button klicken

**Aufgabe:** Schreiben Sie einen professionellen Bug Report mit allen wichtigen Informationen.

---

### Übung 5: Test Coverage analysieren (15 Min)

Führen Sie folgenden Befehl in Ihrem Flutter Projekt aus:
```bash
flutter test --coverage
```

Öffnen Sie dann die generierte `coverage/lcov-report/index.html` Datei.

**Aufgaben:**
1. Wie hoch ist die aktuelle Test Coverage?
2. Welche Dateien haben die niedrigste Coverage?
3. Identifizieren Sie 3 Methoden/Funktionen die noch nicht getestet sind
4. Schreiben Sie für eine dieser Methoden einen Test

---

### Übung 6: Mocking verwenden (20 Min)

Sie haben einen Service der API-Calls macht:

```dart
abstract class WeatherService {
  Future<Weather> getWeather(String city);
}

class Weather {
  final String city;
  final double temperature;
  final String condition;
  
  Weather({
    required this.city,
    required this.temperature,
    required this.condition,
  });
}

class WeatherWidget extends StatelessWidget {
  final WeatherService weatherService;
  
  WeatherWidget({required this.weatherService});
  
  @override
  Widget build(BuildContext context) {
    return FutureBuilder<Weather>(
      future: weatherService.getWeather('Zürich'),
      builder: (context, snapshot) {
        if (snapshot.hasData) {
          return Text('${snapshot.data!.temperature}°C');
        }
        return CircularProgressIndicator();
      },
    );
  }
}
```

**Aufgabe:** 
1. Erstellen Sie einen Mock für WeatherService mit Mockito
2. Schreiben Sie einen Widget Test der überprüft:
   - Loading Indicator wird initial angezeigt
   - Temperatur wird nach dem Laden angezeigt
   - Fehlerbehandlung funktioniert

---

### Bonus-Übung: Integration Test (25 Min)

Schreiben Sie einen Integration Test für einen kompletten User Flow:

**Szenario:** Benutzer Registration
1. App öffnen
2. Auf "Registrieren" klicken
3. Name eingeben
4. Email eingeben
5. Passwort eingeben
6. Passwort bestätigen
7. AGB akzeptieren
8. Registrieren klicken
9. Prüfen ob Willkommens-Screen erscheint

**Tipp:** Nutzen Sie `integration_test` Package und denken Sie an:
- Warten auf Animationen (`pumpAndSettle()`)
- Scroll-Aktionen für lange Formulare
- Keyboard handling

---

## Reflexionsfragen

Nach Abschluss der Übungen, reflektieren Sie:

1. **Welche Art von Tests war am einfachsten zu schreiben? Warum?**
   _____________________________________________________

2. **Welche Herausforderungen hatten Sie beim Testing?**
   _____________________________________________________

3. **Wie würden Sie Testing in Ihrem nächsten Projekt einplanen?**
   _____________________________________________________

4. **Welche Test-Art finden Sie am wichtigsten und warum?**
   _____________________________________________________

---

## Abgabe

- Erstellen Sie ein Git Repository mit Ihren Lösungen
- Struktur:
  ```
  /test
    /unit
      shopping_cart_test.dart
    /widget
      counter_widget_test.dart
    /integration
      registration_test.dart
  /docs
    testplan.md
    bug_report.md
  ```
- Stellen Sie sicher, dass alle Tests grün sind (`flutter test`)

**Viel Erfolg! 🚀**