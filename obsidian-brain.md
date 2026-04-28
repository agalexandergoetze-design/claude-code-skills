---
name: obsidian-brain
description: Richtet ein Obsidian + Claude Code Second Brain ein oder verwaltet einen bestehenden Vault. Aktivieren wenn: du regelmäßig Artikel/PDFs/Notizen sammelst und Wissen zwischen Sessions verlierst, oder du einen bestehenden Vault pflegen willst.
---

# Obsidian Second Brain

Verwalte ein persönliches Wissenssystem mit Obsidian als visueller Oberfläche und Claude Code als automatischem Wiki-Builder.

## Struktur

```
vault/
  raw/      ← Quellmaterial (Artikel, PDFs, Notizen) — nur lesen, nie ändern
  wiki/     ← Wiki-Seiten mit [[wiki-links]] — Claude erstellt und pflegt
  index.md  ← Katalog aller Wiki-Seiten
  log.md    ← Änderungsprotokoll
  CLAUDE.md ← Regeln für Claude Code
```

## Setup (einmalig, ~30 Min.)

```bash
# 1. Obsidian installieren (Windows)
winget install Obsidian.Obsidian

# 2. Vault-Ordner erstellen
mkdir C:\Users\Alexander\obsidian-vault
mkdir C:\Users\Alexander\obsidian-vault\raw
mkdir C:\Users\Alexander\obsidian-vault\wiki

# 3. Claude Code im Vault starten
cd C:\Users\Alexander\obsidian-vault
claude

# 4. In Obsidian: "Open folder as vault" → obsidian-vault wählen
```

## CLAUDE.md für den Vault

```markdown
# Mein Wiki — Regeln für Claude Code

## Struktur
- raw/ = Quellmaterial (nur lesen, nie ändern)
- wiki/ = Wiki-Seiten (du verwaltest)
- index.md = Katalog aller Seiten
- log.md = Änderungsprotokoll

## Neue Quelle verarbeiten
1. Quelle in raw/ lesen
2. Wiki-Seiten in wiki/ erstellen/aktualisieren
3. Mit [[wiki-links]] verknüpfen
4. index.md und log.md aktualisieren

## Frage beantworten
1. index.md lesen → relevante Seiten finden
2. Antwort mit Quellenbezug geben
```

## Nützliche Prompts

- **Neue Quelle verarbeiten:** "Lies [Dateiname] in raw/ und erstelle Wiki-Seiten daraus"
- **Frage stellen:** "Was weiß mein Wiki über [Thema]?"
- **Recherche speichern:** "Recherchiere [Thema] und speichere in raw/"
- **Qualitätscheck:** "Mach einen Lint — finde Lücken und fehlende Verknüpfungen"
- **Alles verarbeiten:** "Lies alle neuen Dateien in raw/ und aktualisiere das Wiki"

## Wann nutzen

Sinnvoll wenn du:
- Regelmäßig 5+ Artikel/Woche sammelst
- Dieselben Themen mehrfach recherchierst
- Entscheidungen auf Basis gesammelten Wissens triffst
- Ein Produkt mit Wissensextraktion/Verlinkung baust und validieren willst

## Web Clipper (Optional)

Chrome Web Store → "Obsidian Web Clipper" → Note location auf "raw" setzen → 1-Click Speichern aus Browser.
