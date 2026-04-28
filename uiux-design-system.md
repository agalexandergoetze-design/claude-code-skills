---
name: ckm:design-system
description: Design Tokens, Komponenten-Specs und Präsentations-Generierung mit 3-Layer Token-Architektur
---

# Design System Skill

Verwaltet Design Tokens, Komponenten-Spezifikationen und generiert Brand-konforme Präsentationen.

## Token-Architektur (3 Layer)

```
Primitive (raw values)
  → Semantic (purpose aliases)
    → Component (component-specific)
```

Implementiert als CSS Custom Properties.

## Capabilities

- **Token Management** — CSS-Variablen in 3 Schichten organisieren
- **Komponenten-Specs** — States (background, text, border, shadow) standardisieren
- **Präsentations-Generierung** — Slides mit Decision-System-CSVs (Strategien, Layouts, Typografie, Farben)
- **Tailwind-Theme** — Design Tokens als Tailwind-Konfiguration exportieren

## Slide-Compliance-Regeln

- Design-Tokens CSS-File importieren
- Ausschließlich CSS-Variablen referenzieren
- Chart.js für Visualisierungen
- Navigations-Controls einbauen

## Use Cases

- Design Token Architektur aufsetzen
- Tailwind-Theme konfigurieren
- Komponenten-States dokumentieren
- Brand-konforme Decks generieren
- Design-to-Code Handoff
