# Auftrag 4 (Optional): JSON-Konfigurationssystem für Portfolio

## Ziel

Du entwickelst ein fortgeschrittenes JSON-basiertes Konfigurationssystem für dein Portfolio. Du lernst, wie professionelle Web-Apps zentrale Konfigurationsdateien nutzen, Theme-Switching implementieren und komplexe JSON-Strukturen mit JSON-Schema validieren.

**Schwierigkeitsgrad:** Fortgeschritten  
**Voraussetzungen:** Aufträge 1-3 abgeschlossen

## Beschreibung

Professionelle Webprojekte nutzen JSON-Konfigurationsdateien, um Einstellungen zentral zu verwalten. Themes, Feature-Flags, API-Endpoints, SEO-Daten – alles wird in JSON definiert und dynamisch geladen. Das macht Projekte wartbar und erlaubt Anpassungen ohne Code-Änderungen.

In diesem Vertiefungsauftrag baust du ein vollständiges Konfigurationssystem: Multiple Themes, Feature-Toggles, Mehrsprachigkeit und JSON-Schema-Validierung. Das ist ein realistisches Beispiel, wie moderne Web-Apps strukturiert sind.

---

### Teil 1: Portfolio-Konfiguration (25 Min)

Erstelle eine zentrale Konfigurationsdatei **`config.json`**:

```json
{
  "$schema": "./config-schema.json",
  "version": "1.0.0",
  "lastUpdated": "2025-11-18T10:30:00Z",
  "portfolio": {
    "owner": {
      "name": "Sarah Müller",
      "role": "Informatikerin EFZ Applikationsentwicklung",
      "email": "sarah.mueller@example.com",
      "location": "Bern, Schweiz",
      "tagline": "Leidenschaftliche Entwicklerin mit Fokus auf moderne Webtechnologien",
      "social": {
        "github": "https://github.com/sarahmueller",
        "linkedin": "https://linkedin.com/in/sarah-mueller",
        "twitter": null,
        "website": "https://sarahmueller.dev"
      }
    },
    "seo": {
      "title": "Sarah Müller - Portfolio",
      "description": "Portfolio einer Informatikerin EFZ Applikationsentwicklung aus Bern",
      "keywords": ["Webentwicklung", "HTML", "CSS", "JavaScript", "Portfolio"],
      "ogImage": "https://sarahmueller.dev/og-image.jpg",
      "twitterCard": "summary_large_image"
    },
    "features": {
      "darkMode": true,
      "languageSwitcher": true,
      "contactForm": true,
      "blog": false,
      "analytics": false,
      "cookieConsent": false
    },
    "navigation": [
      {
        "id": "home",
        "label": {
          "de": "Home",
          "en": "Home"
        },
        "url": "#home",
        "icon": "🏠",
        "isActive": true
      },
      {
        "id": "about",
        "label": {
          "de": "Über mich",
          "en": "About"
        },
        "url": "#about",
        "icon": "👤",
        "isActive": true
      },
      {
        "id": "projekte",
        "label": {
          "de": "Projekte",
          "en": "Projects"
        },
        "url": "#projekte",
        "icon": "💼",
        "isActive": true
      },
      {
        "id": "skills",
        "label": {
          "de": "Skills",
          "en": "Skills"
        },
        "url": "#skills",
        "icon": "🎯",
        "isActive": true
      },
      {
        "id": "kontakt",
        "label": {
          "de": "Kontakt",
          "en": "Contact"
        },
        "url": "#kontakt",
        "icon": "📧",
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
    "api": {
      "github": {
        "username": "sarahmueller",
        "baseUrl": "https://api.github.com",
        "cacheTimeout": 3600
      }
    },
    "content": {
      "aboutText": {
        "de": "Ich bin Informatikerin EFZ in Ausbildung mit Leidenschaft für Webentwicklung. Aktuell im 1. Lehrjahr bei ABC Tech AG.",
        "en": "I'm an apprentice software developer with a passion for web development. Currently in my first year at ABC Tech AG."
      },
      "contactText": {
        "de": "Interesse an einer Zusammenarbeit? Kontaktiere mich gerne!",
        "en": "Interested in working together? Feel free to reach out!"
      }
    }
  }
}
```

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

**Erstelle `config-system.js`:**

```javascript
// =====================================================
// JSON-KONFIGURATIONSSYSTEM
// =====================================================

let config = null;
let currentTheme = 'light';
let currentLanguage = 'de';

// Beim Laden: Konfiguration laden
document.addEventListener('DOMContentLoaded', async function() {
    await ladeKonfiguration();
});

async function ladeKonfiguration() {
    try {
        console.log('Lade config.json...');
        
        const response = await fetch('config.json');
        if (!response.ok) {
            throw new Error(`HTTP ${response.status}: ${response.statusText}`);
        }
        
        config = await response.json();
        console.log('Konfiguration geladen:', config);
        
        // Validierung
        validateConfig(config);
        
        // UI initialisieren
        initializeUI();
        
        // Theme anwenden
        const gespeichertesTheme = localStorage.getItem('portfolio-theme');
        currentTheme = gespeichertesTheme || config.portfolio.themes.default;
        changeTheme(currentTheme);
        
        // Sprache anwenden
        const gespeicherteSprache = localStorage.getItem('portfolio-language');
        currentLanguage = gespeicherteSprache || 'de';
        document.getElementById('lang-select').value = currentLanguage;
        updateLanguage();
        
    } catch (error) {
        console.error('Fehler beim Laden der Konfiguration:', error);
        alert('Fehler beim Laden der Konfiguration: ' + error.message);
    }
}

function validateConfig(cfg) {
    // Basis-Validierung
    if (!cfg.portfolio) {
        throw new Error('Konfiguration: "portfolio" fehlt');
    }
    
    if (!cfg.portfolio.owner || !cfg.portfolio.owner.name) {
        throw new Error('Konfiguration: "owner.name" fehlt');
    }
    
    if (!cfg.portfolio.themes || !cfg.portfolio.themes.available) {
        throw new Error('Konfiguration: "themes.available" fehlt');
    }
    
    console.log('✓ Konfiguration ist valide');
}

function initializeUI() {
    // Seitentitel setzen
    document.getElementById('page-title').textContent = config.portfolio.seo.title;
    document.getElementById('page-description').setAttribute('content', config.portfolio.seo.description);
    document.getElementById('site-title').textContent = config.portfolio.owner.name;
    
    // Navigation generieren
    generiereNavigation();
    
    // Theme-Select füllen
    const themeSelect = document.getElementById('theme-select');
    config.portfolio.themes.available.forEach(theme => {
        const option = document.createElement('option');
        option.value = theme;
        option.textContent = theme.charAt(0).toUpperCase() + theme.slice(1);
        themeSelect.appendChild(option);
    });
    themeSelect.value = currentTheme;
    
    // Owner-Informationen anzeigen
    zeigeOwnerInfo();
    
    // Features anzeigen
    zeigeFeatures();
    
    // Konfiguration anzeigen
    zeigeKonfiguration();
}

function generiereNavigation() {
    const nav = document.getElementById('main-nav');
    const ul = document.createElement('ul');
    
    config.portfolio.navigation
        .filter(item => item.isActive)
        .forEach(item => {
            const li = document.createElement('li');
            const a = document.createElement('a');
            a.href = item.url;
            a.textContent = `${item.icon} ${item.label[currentLanguage]}`;
            li.appendChild(a);
            ul.appendChild(li);
        });
    
    nav.innerHTML = '';
    nav.appendChild(ul);
}

function zeigeOwnerInfo() {
    const infoDiv = document.getElementById('owner-info');
    const owner = config.portfolio.owner;
    
    infoDiv.innerHTML = `
        <div class="info-item">
            <strong>Name</strong>
            ${owner.name}
        </div>
        <div class="info-item">
            <strong>Rolle</strong>
            ${owner.role}
        </div>
        <div class="info-item">
            <strong>Email</strong>
            <a href="mailto:${owner.email}">${owner.email}</a>
        </div>
        <div class="info-item">
            <strong>Standort</strong>
            ${owner.location}
        </div>
        <div class="info-item">
            <strong>GitHub</strong>
            <a href="${owner.social.github}" target="_blank">Profil ansehen</a>
        </div>
    `;
}

function zeigeFeatures() {
    const featuresDiv = document.getElementById('features-list');
    const features = config.portfolio.features;
    
    featuresDiv.innerHTML = '';
    
    Object.keys(features).forEach(feature => {
        const isActive = features[feature];
        const span = document.createElement('span');
        span.className = `feature-toggle ${isActive ? 'active' : 'inactive'}`;
        span.textContent = `${isActive ? '✓' : '✗'} ${feature}`;
        featuresDiv.appendChild(span);
    });
}

function zeigeKonfiguration() {
    const configDisplay = document.getElementById('config-display');
    configDisplay.textContent = JSON.stringify(config, null, 2);
}

function changeTheme(themeName) {
    if (!config.portfolio.themes[themeName]) {
        console.error('Theme nicht gefunden:', themeName);
        return;
    }
    
    const theme = config.portfolio.themes[themeName];
    const root = document.documentElement;
    
    // CSS-Variablen setzen
    Object.keys(theme).forEach(key => {
        root.style.setProperty(`--${key}`, theme[key]);
    });
    
    currentTheme = themeName;
    localStorage.setItem('portfolio-theme', themeName);
    
    console.log('Theme gewechselt:', themeName);
}

function changeLanguage(lang) {
    currentLanguage = lang;
    localStorage.setItem('portfolio-language', lang);
    updateLanguage();
}

function updateLanguage() {
    // Navigation aktualisieren
    generiereNavigation();
    
    // Weitere sprachabhängige Elemente hier aktualisieren
    console.log('Sprache gewechselt:', currentLanguage);
}

function exportConfig() {
    const json = JSON.stringify(config, null, 2);
    const blob = new Blob([json], { type: 'application/json' });
    const url = URL.createObjectURL(blob);
    
    const link = document.createElement('a');
    link.href = url;
    link.download = `portfolio-config-${new Date().toISOString().split('T')[0]}.json`;
    link.click();
    
    console.log('✓ Konfiguration exportiert');
}

function resetConfig() {
    if (confirm('Möchtest du die Konfiguration wirklich zurücksetzen?')) {
        localStorage.removeItem('portfolio-theme');
        localStorage.removeItem('portfolio-language');
        location.reload();
    }
}
```

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
