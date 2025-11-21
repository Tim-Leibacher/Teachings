# Auftrag 4 (Optional): JSON-Konfigurationssystem für Portfolio

## Ziel

Du entwickelst ein fortgeschrittenes JSON-basiertes Konfigurationssystem für dein Portfolio. Du lernst, wie professionelle Web-Apps zentrale Konfigurationsdateien nutzen, Theme-Switching implementieren und komplexe JSON-Strukturen mit JSON-Schema validieren.

**Schwierigkeitsgrad:** Fortgeschritten  
**Voraussetzungen:** Aufträge 1-3 abgeschlossen

## Beschreibung

Professionelle Webprojekte nutzen JSON-Konfigurationsdateien, um Einstellungen zentral zu verwalten. Themes, Feature-Flags, API-Endpoints, SEO-Daten – alles wird in JSON definiert und dynamisch geladen. Das macht Projekte wartbar und erlaubt Anpassungen ohne Code-Änderungen.

In diesem Vertiefungsauftrag baust du ein vollständiges Konfigurationssystem: Multiple Themes, Feature-Toggles, Mehrsprachigkeit und JSON-Schema-Validierung. Das ist ein realistisches Beispiel, wie moderne Web-Apps strukturiert sind.

---

### Teil 1: Portfolio-Konfiguration erstellen (30 Min)

**Aufgabe:** Erstelle eine zentrale Konfigurationsdatei für dein Portfolio.

**Schritt 1:** Erstelle **`config.json`** mit folgender Grundstruktur:

```json
{
  "$schema": "./config-schema.json",
  "version": "1.0.0",
  "lastUpdated": "...",
  "portfolio": {
    "owner": {
      "name": "...",
      "role": "...",
      "email": "...",
      "location": "...",
      "tagline": "...",
      "social": {
        "github": "...",
        "linkedin": "...",
        "website": "..."
      }
    },
    "seo": {
      "title": "...",
      "description": "...",
      "keywords": ["..."]
    },
    "features": {
      "darkMode": true,
      "languageSwitcher": false,
      "contactForm": true,
      "blog": false
    },
    "navigation": [
      {
        "id": "home",
        "label": {"de": "Home", "en": "Home"},
        "url": "#home",
        "icon": "🏠",
        "isActive": true
      }
    ],
    "themes": {
      "default": "light",
      "available": ["light", "dark", "high-contrast"],
      "light": {
        "primary": "#005A9C",
        "secondary": "#008C95",
        "accent": "#E65A00",
        "background": "#FFFFFF",
        "surface": "#F8F9FA",
        "text": "#212529",
        "textSecondary": "#6C757D",
        "border": "#DEE2E6"
      },
      "dark": {
        "primary": "#4E9BCC",
        "secondary": "#5FBFC8",
        "accent": "#FF8C42",
        "background": "#1A1A1A",
        "surface": "#2A2A2A",
        "text": "#F8F9FA",
        "textSecondary": "#ADB5BD",
        "border": "#495057"
      },
      "high-contrast": {
        "primary": "#0066FF",
        "secondary": "#00CCFF",
        "accent": "#FF6600",
        "background": "#000000",
        "surface": "#1A1A1A",
        "text": "#FFFFFF",
        "textSecondary": "#CCCCCC",
        "border": "#FFFFFF"
      }
    },
  }
}
```

**Deine Aufgabe:**
1. Fülle alle `...` mit deinen eigenen Daten
2. Füge **mindestens 4 Navigation-Einträge** hinzu (About, Projekte, Skills, Kontakt)
3. Aktiviere oder deaktiviere Features nach Bedarf
4. Passe die Theme-Farben an (optional)

**Wo nachschlagen?**
- Wie formatiert man ISO-Datumsangaben? → Format: `"2025-11-18T10:30:00Z"`
- Was sind gültige Hex-Farbcodes? → Format: `"#RRGGBB"` (z.B. `"#005A9C"`)
- [JSON Schema Dokumentation](https://json-schema.org/understanding-json-schema/reference/string.html#format)

**Erstelle jetzt die HTML-Seite `config-demo.html`:**

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title id="page-title">Portfolio</title>
    <meta id="page-description" name="description" content="">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        :root {
            --primary: #005A9C;
            --secondary: #008C95;
            --accent: #E65A00;
            --background: #FFFFFF;
            --surface: #F8F9FA;
            --text: #212529;
            --text-secondary: #6C757D;
            --border: #DEE2E6;
        }
        
        body {
            font-family: 'Aptos', Arial, sans-serif;
            background: var(--background);
            color: var(--text);
            transition: all 0.3s ease;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        
        header {
            background: var(--surface);
            border-bottom: 2px solid var(--border);
            padding: 20px 0;
            margin-bottom: 30px;
        }
        
        .header-content {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        h1 {
            color: var(--primary);
        }
        
        nav ul {
            list-style: none;
            display: flex;
            gap: 20px;
        }
        
        nav a {
            text-decoration: none;
            color: var(--text);
            padding: 8px 16px;
            border-radius: 4px;
            transition: all 0.3s ease;
        }
        
        nav a:hover {
            background: var(--primary);
            color: white;
        }
        
        .controls {
            background: var(--surface);
            padding: 20px;
            border-radius: 8px;
            margin-bottom: 30px;
            border: 2px solid var(--border);
        }
        
        .control-group {
            margin-bottom: 15px;
        }
        
        .control-group label {
            display: block;
            margin-bottom: 5px;
            font-weight: 600;
            color: var(--text-secondary);
        }
        
        select, button {
            padding: 10px 15px;
            border: 2px solid var(--border);
            border-radius: 4px;
            background: var(--background);
            color: var(--text);
            font-size: 16px;
            cursor: pointer;
        }
        
        button {
            background: var(--primary);
            color: white;
            border-color: var(--primary);
            margin-right: 10px;
        }
        
        button:hover {
            opacity: 0.9;
        }
        
        .info-panel {
            background: var(--surface);
            padding: 20px;
            border-radius: 8px;
            border: 2px solid var(--border);
            margin-bottom: 20px;
        }
        
        .info-panel h2 {
            color: var(--primary);
            margin-bottom: 15px;
        }
        
        .info-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 15px;
        }
        
        .info-item {
            padding: 15px;
            background: var(--background);
            border-radius: 4px;
            border-left: 4px solid var(--accent);
        }
        
        .info-item strong {
            display: block;
            color: var(--text-secondary);
            font-size: 0.9em;
            margin-bottom: 5px;
        }
        
        .feature-toggle {
            display: inline-flex;
            align-items: center;
            gap: 10px;
            padding: 8px 15px;
            background: var(--surface);
            border-radius: 20px;
            margin-right: 10px;
            margin-bottom: 10px;
            border: 2px solid var(--border);
        }
        
        .feature-toggle.active {
            background: var(--primary);
            color: white;
            border-color: var(--primary);
        }
        
        .feature-toggle.inactive {
            opacity: 0.5;
        }
        
        code {
            background: var(--background);
            padding: 2px 6px;
            border-radius: 3px;
            border: 1px solid var(--border);
            font-family: 'Courier New', monospace;
        }
        
        pre {
            background: var(--surface);
            padding: 15px;
            border-radius: 4px;
            overflow-x: auto;
            border: 2px solid var(--border);
        }
    </style>
</head>
<body>
    <header>
        <div class="header-content">
            <h1 id="site-title">Portfolio</h1>
            <nav id="main-nav">
                <!-- Navigation wird dynamisch geladen -->
            </nav>
        </div>
    </header>
    
    <div class="container">
        <div class="controls">
            <h2>Konfiguration anpassen</h2>
            
            <div class="control-group">
                <label for="theme-select">Theme auswählen:</label>
                <select id="theme-select" onchange="changeTheme(this.value)">
                    <!-- Wird dynamisch gefüllt -->
                </select>
            </div>
            
            <div class="control-group">
                <label for="lang-select">Sprache:</label>
                <select id="lang-select" onchange="changeLanguage(this.value)">
                    <option value="de">Deutsch</option>
                    <option value="en">English</option>
                </select>
            </div>
            
            <div class="control-group">
                <label>Aktionen:</label>
                <button onclick="exportConfig()">Konfiguration exportieren</button>
                <button onclick="resetConfig()">Zurücksetzen</button>
            </div>
        </div>
        
        <div class="info-panel">
            <h2>Portfolio-Informationen</h2>
            <div class="info-grid" id="owner-info">
                <!-- Wird dynamisch gefüllt -->
            </div>
        </div>
        
        <div class="info-panel">
            <h2>Features</h2>
            <div id="features-list">
                <!-- Wird dynamisch gefüllt -->
            </div>
        </div>
        
        <div class="info-panel">
            <h2>Aktuelle Konfiguration</h2>
            <pre id="config-display"></pre>
        </div>
    </div>
    
    <script src="config-system.js"></script>
</body>
</html>
```

**Schritt 2:** Erstelle `config-system.js` und implementiere die Funktionen:

**Erforderliche Funktionen:**

1. **`ladeKonfiguration()`**
   - Lade `config.json` mit `fetch()`
   - Validiere die Konfiguration
   - Initialisiere die UI

2. **`changeTheme(themeName)`**
   - Hole Theme-Farben aus Config
   - Setze CSS Custom Properties mit `document.documentElement.style.setProperty()`
   - Speichere Theme in LocalStorage

3. **`generiereNavigation()`**
   - Durchlaufe `config.portfolio.navigation`
   - Erstelle `<a>`-Tags für jeden Eintrag
   - Nutze die richtige Sprache für Labels

**Grundgerüst:**

```javascript
let config = null;
let currentTheme = 'light';
let currentLanguage = 'de';

document.addEventListener('DOMContentLoaded', async function() {
    await ladeKonfiguration();
});

async function ladeKonfiguration() {
    try {
        // TODO: Lade config.json
        // TODO: Parse zu JSON
        // TODO: Rufe initializeUI() auf

    } catch (error) {
        console.error('Fehler:', error);
        alert('Fehler beim Laden: ' + error.message);
    }
}

function changeTheme(themeName) {
    // TODO: Hole Theme aus config.portfolio.themes[themeName]
    // TODO: Setze CSS Custom Properties
    // Beispiel: document.documentElement.style.setProperty('--primary', theme.primary);
    // TODO: Speichere in localStorage
}

function generiereNavigation() {
    // TODO: Hole Navigation aus config.portfolio.navigation
    // TODO: Erstelle <ul> und <li> Elemente
    // TODO: Filtere nur aktive Items (isActive === true)
    // TODO: Nutze die Sprache aus currentLanguage
}
```

**Hilfestellung:**
- [MDN: CSS Custom Properties](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties)
- [MDN: LocalStorage](https://developer.mozilla.org/de/docs/Web/API/Window/localStorage)
- [MDN: Array.filter()](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)

**Zusatzaufgaben:**
1. Implementiere `zeigeFeatures()` - zeige alle Features mit ✓/✗ an
2. Implementiere `changeLanguage()` - wechsle zwischen de/en
3. Implementiere `exportConfig()` - exportiere Config als JSON-Datei

---

### Teil 2: JSON-Schema erstellen (20 Min)

Erstelle **`config-schema.json`** zur Validierung:

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "Portfolio Configuration",
  "type": "object",
  "required": ["version", "portfolio"],
  "properties": {
    "$schema": {
      "type": "string"
    },
    "version": {
      "type": "string",
      "pattern": "^\\d+\\.\\d+\\.\\d+$",
      "description": "Semantic version (x.y.z)"
    },
    "lastUpdated": {
      "type": "string",
      "format": "date-time"
    },
    "portfolio": {
      "type": "object",
      "required": ["owner", "themes", "navigation"],
      "properties": {
        "owner": {
          "type": "object",
          "required": ["name", "email"],
          "properties": {
            "name": {
              "type": "string",
              "minLength": 2,
              "maxLength": 100
            },
            "role": {
              "type": "string"
            },
            "email": {
              "type": "string",
              "format": "email"
            },
            "location": {
              "type": "string"
            },
            "tagline": {
              "type": "string",
              "maxLength": 200
            },
            "social": {
              "type": "object",
              "properties": {
                "github": {
                  "type": ["string", "null"],
                  "format": "uri"
                },
                "linkedin": {
                  "type": ["string", "null"],
                  "format": "uri"
                },
                "twitter": {
                  "type": ["string", "null"],
                  "format": "uri"
                },
                "website": {
                  "type": ["string", "null"],
                  "format": "uri"
                }
              }
            }
          }
        },
        "seo": {
          "type": "object",
          "required": ["title", "description"],
          "properties": {
            "title": {
              "type": "string",
              "minLength": 10,
              "maxLength": 60
            },
            "description": {
              "type": "string",
              "minLength": 50,
              "maxLength": 160
            },
            "keywords": {
              "type": "array",
              "items": {
                "type": "string"
              }
            }
          }
        },
        "features": {
          "type": "object",
          "additionalProperties": {
            "type": "boolean"
          }
        },
        "navigation": {
          "type": "array",
          "items": {
            "type": "object",
            "required": ["id", "label", "url", "isActive"],
            "properties": {
              "id": {
                "type": "string"
              },
              "label": {
                "type": "object",
                "required": ["de", "en"],
                "properties": {
                  "de": {
                    "type": "string"
                  },
                  "en": {
                    "type": "string"
                  }
                }
              },
              "url": {
                "type": "string"
              },
              "icon": {
                "type": "string"
              },
              "isActive": {
                "type": "boolean"
              }
            }
          }
        },
        "themes": {
          "type": "object",
          "required": ["default", "available"],
          "properties": {
            "default": {
              "type": "string",
              "enum": ["light", "dark", "high-contrast"]
            },
            "available": {
              "type": "array",
              "items": {
                "type": "string",
                "enum": ["light", "dark", "high-contrast"]
              },
              "minItems": 1,
              "uniqueItems": true
            }
          },
          "additionalProperties": {
            "type": "object",
            "properties": {
              "primary": {
                "type": "string",
                "pattern": "^#[0-9A-Fa-f]{6}$"
              },
              "secondary": {
                "type": "string",
                "pattern": "^#[0-9A-Fa-f]{6}$"
              },
              "accent": {
                "type": "string",
                "pattern": "^#[0-9A-Fa-f]{6}$"
              },
              "background": {
                "type": "string",
                "pattern": "^#[0-9A-Fa-f]{6}$"
              },
              "surface": {
                "type": "string",
                "pattern": "^#[0-9A-Fa-f]{6}$"
              },
              "text": {
                "type": "string",
                "pattern": "^#[0-9A-Fa-f]{6}$"
              },
              "textSecondary": {
                "type": "string",
                "pattern": "^#[0-9A-Fa-f]{6}$"
              },
              "border": {
                "type": "string",
                "pattern": "^#[0-9A-Fa-f]{6}$"
              }
            }
          }
        }
      }
    }
  }
}
```

**Validiere dein Schema online:**
1. Öffne [jsonschemavalidator.net](https://www.jsonschemavalidator.net/)
2. Füge `config-schema.json` links ein
3. Füge `config.json` rechts ein
4. Prüfe auf Validierungsfehler

---

### Teil 3: Dynamische Theme-Erstellung (15 Min)

Erweitere `config-system.js` um eine Theme-Creator-Funktion:

```javascript
// Füge am Ende von config-system.js hinzu:

function createCustomTheme() {
    const themeName = prompt('Theme-Name:');
    if (!themeName) return;
    
    const primary = prompt('Primärfarbe (Hex):', '#005A9C');
    const secondary = prompt('Sekundärfarbe (Hex):', '#008C95');
    const accent = prompt('Akzentfarbe (Hex):', '#E65A00');
    const background = prompt('Hintergrundfarbe (Hex):', '#FFFFFF');
    const text = prompt('Textfarbe (Hex):', '#212529');
    
    // Neues Theme erstellen
    const newTheme = {
        primary,
        secondary,
        accent,
        background,
        surface: background,
        text,
        textSecondary: '#6C757D',
        border: '#DEE2E6'
    };
    
    // Zum Config hinzufügen
    config.portfolio.themes[themeName] = newTheme;
    config.portfolio.themes.available.push(themeName);
    
    // Theme-Select aktualisieren
    const select = document.getElementById('theme-select');
    const option = document.createElement('option');
    option.value = themeName;
    option.textContent = themeName;
    select.appendChild(option);
    
    // Theme anwenden
    changeTheme(themeName);
    select.value = themeName;
    
    console.log('Neues Theme erstellt:', themeName);
}

// Button hinzufügen (in initializeUI):
const createBtn = document.createElement('button');
createBtn.textContent = 'Eigenes Theme erstellen';
createBtn.onclick = createCustomTheme;
document.querySelector('.controls').appendChild(createBtn);
```

---

## Erfolgskriterien

- [ ] `config.json` erstellt mit vollständiger Konfiguration
- [ ] `config-demo.html` und `config-system.js` funktionsfähig
- [ ] Themes können gewechselt werden (light, dark, high-contrast)
- [ ] Theme-Auswahl wird in localStorage gespeichert
- [ ] Navigation wird dynamisch aus JSON generiert
- [ ] Mehrsprachigkeit funktioniert (de/en)
- [ ] Feature-Toggles werden korrekt angezeigt
- [ ] Konfiguration kann exportiert werden
- [ ] `config-schema.json` erstellt und erfolgreich validiert
- [ ] Eigenes Theme kann erstellt werden (Bonus)

---

## Tipps

**CSS Custom Properties:**
- `--variable-name` in :root definieren
- Mit `var(--variable-name)` nutzen
- Dynamisch mit JS setzen: `root.style.setProperty()`

**LocalStorage für Persistenz:**
```javascript
// Speichern
localStorage.setItem('key', 'value');

// Laden
const value = localStorage.getItem('key');

// Löschen
localStorage.removeItem('key');
```

**JSON-Schema Validierung:**
- Online: jsonschemavalidator.net
- In Node.js: ajv Package
- VS Code Extension: JSON Schema

**Best Practices:**
- Konfiguration zentral halten
- Feature-Flags für optionale Features
- Theme-Farben als Variablen
- Mehrsprachigkeit von Anfang an einplanen

---

## Reflexionsfragen

1. **Welche Vorteile hat ein JSON-Konfigurationssystem?**  
   *Wann lohnt sich der Aufwand? Welche Nachteile gibt es?*

2. **Wie würdest du die Konfiguration vor unbefugten Änderungen schützen?**  
   *Recherchiere: Sollte config.json öffentlich zugänglich sein?*

3. **Was ist der Unterschied zwischen Feature-Flags und Theme-Einstellungen?**  
   *Wann nutzt du welches Konzept?*

4. **Experimentiere: Erstelle ein "Nachtmodus"-Theme mit eigenen Farben.**  
   *Welche Farben sind am besten für die Augen bei Nacht?*

5. **Wie könntest du A/B-Testing mit diesem Konfigurationssystem implementieren?**  
   *Tipp: Mehrere Konfigurationen parallel laden und per Zufall auswählen*

---

## Weiterführende Links

**JSON-Schema:**
- [JSON Schema](https://json-schema.org/) – Offizielle Dokumentation
- [Understanding JSON Schema](https://json-schema.org/understanding-json-schema/)
- [JSON Schema Validator](https://www.jsonschemavalidator.net/)

**CSS Custom Properties:**
- [MDN: CSS Custom Properties](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties)
- [CSS-Tricks: A Complete Guide to Custom Properties](https://css-tricks.com/a-complete-guide-to-custom-properties/)

**Konfigurationssysteme:**
- [Feature Flags](https://martinfowler.com/articles/feature-toggles.html)
- [12 Factor App: Config](https://12factor.net/config)

**Theme-Switching:**
- [CSS-Tricks: A Complete Guide to Dark Mode](https://css-tricks.com/a-complete-guide-to-dark-mode-on-the-web/)
- [Web.dev: prefers-color-scheme](https://web.dev/prefers-color-scheme/)

---

**⏱️ Geschätzte Zeit:** 60-90 Minuten  
**📦 Integration:** Nutze dieses System in deinem echten Portfolio!
