# 📋 PROJECT BRIEF — Virtuelles Skill Lab: Pneumonie-Diagnostik

---

## 📌 Executive Summary

**Projekt:** Virtuelles Skill Lab – Pneumonie-Diagnostik  
**Slug:** `skilllab-pneumonie`  
**Status:** 🟢 Ready for Implementation  
**Owner:** Claus Clemens  
**Start:** 2026-04-29  
**Kontext:** 1_STUDIUM (Charité Berlin, Ausbildungsstation)  
**Deployment-Ziel:** https://claasdehero-byte.github.io/skilllab-pneumonie/

### Kurzbeschreibung
Interaktives digitales Lernmodul für Pflegeauszubildende der Charité Berlin zur Pneumonie-Diagnostik. Auszubildende klicken auf 25 Objekte in einem illustrierten Patientenzimmer (Wimmelbild) und entscheiden, ob diese ESSENTIELL oder NICHT ESSENTIELL für die Primärdiagnose einer Pneumonie sind. Nach jeder Entscheidung erscheint leitlinienbasiertes Feedback (S3-Leitlinie CAP, DNQP, RKI) mit Evidenzlevel. Aufbauend auf dem bestehenden Hygiene-Skill-Lab V3 (VSDH).

---

## 🎯 Ziele & Success Criteria

### Primäres Ziel
Auszubildende sollen spielerisch lernen, welche diagnostischen Maßnahmen bei Pneumonie-Verdacht essentiell, sinnvoll oder ablenkend sind — verankert in klinischen Leitlinien.

### Success Criteria
- [ ] Alle 25 Hotspots anklickbar, korrektes Feedback-Modal
- [ ] Scoring korrekt (max. 190 Punkte)
- [ ] SINNVOLL-Objekte zeigen Neutral-Feedback (0 Punkte), unabhängig vom Klick
- [ ] Debug-Modus: Hotspots visuell sichtbar (für Koordinaten-Verifikation nach erstem Test)
- [ ] Responsives Design (Desktop + Tablet)
- [ ] Impressum vorhanden (identisch VSDH, nur "Hygiene-Lab" → "Pneumonie-SkillLab")
- [ ] Funktioniert lokal ohne Server (file:// Protokoll)

---

## 🏗️ Tech Stack

| Entscheidung | Wahl | Begründung |
|---|---|---|
| Architektur | **Single-File HTML** | Kein Server nötig, einfache Distribution, wie VSDH |
| Framework | Vanilla JS | Keine Abhängigkeiten |
| Daten | JS-Konstante inline | Kein fetch, kein CORS-Problem |
| SVG | Inline im HTML | Kein fetch nötig |
| Bild | Relativer Pfad | HTML + PNG im selben Ordner |
| Persistenz | Keine | Stateless, kein localStorage |
| Deployment | GitHub Pages | Wie VSDH: `docs/` Ordner |

---

## 👥 Zielgruppe

| Gruppe | Beschreibung |
|---|---|
| **Primär** | Pflegeauszubildende, Charité Berlin, Ausbildungsstation |
| **Sekundär** | Praxisanleiter (PAL) zur Unterrichtsvorbereitung |

---

## 🎮 Game Flow & Screens

```
[Setup] → Team-Name eingeben → "Lab betreten"
    ↓
[Game] → Wimmelbild + 25 Hotspots → Klick → Modal → ESSENTIELL / NICHT ESSENTIELL
    ↓                                                        ↓
    ←←←←←←←←← Feedback-Panel (Leitlinie + Evidenz) ←←←←←←←
    ↓
[Auswertung] → Tabelle + Score + "Wiederholen" / "Impressum"
```

### Screen 1: Setup
- Titelbild als Header (`Titelbild.jpg`)
- Szenario: „Hr. Hermann, Tag 4 nach Symptombeginn, Verdacht auf CAP"
- Eingabe: Team-Name (Pflichtfeld)
- Button: „▶️ Lab betreten"

### Screen 2: Game
- Wimmelbild: `Diagnostik_Pneumonie.png` (1200×896)
- SVG-Overlay: 25 Hotspots, `viewBox="0 0 2560 1920"` (proportional korrekt)
- Progress: „X/25 Objekte bewertet"
- Nach Klick auf Hotspot → Modal öffnet sich
- Modal: Objektname + klinische Beschreibung + 2 Buttons
- Buttons: `✅ ESSENTIELL` / `✗ NICHT ESSENTIELL`
- Feedback-Panel nach Klick: Richtig/Falsch/Sinnvoll + Leitlinie + Evidenzlevel
- „Zimmer verlassen" → Screen 3

### Screen 3: Auswertung
- Tabelle: ID | Objekt | Kategorie | Antwort | Status
- Score: `X / 190 Punkte`
- Fortschrittsbalken
- Buttons: „🔄 Wiederholen" / „📄 Impressum"

---

## 📊 Scoring-System

| Kategorie | Anzahl | Klick ESSENTIELL | Klick NICHT ESSENTIELL | Punkte |
|---|---|---|---|---|
| ESSENTIELL | 8 | ✅ Richtig | ❌ Falsch | +10 / 0 |
| ABLENKUNG | 11 | ❌ Falsch | ✅ Richtig | +10 / 0 |
| SINNVOLL | 6 | ⚡ Neutral | ⚡ Neutral | 0 |

**Max-Score:** (8 + 11) × 10 = **190 Punkte**

### SINNVOLL-Feedback (unabhängig vom Klick):
> „⚡ Sinnvoll – Diese Maßnahme ist klinisch nützlich, aber nicht zwingend notwendig für die Primärdiagnose. [feedback.correct-Text aus DB]"

---

## 📂 Projektstruktur

```
1_STUDIUM/projects/skilllab-pneumonie/
├── project-brief.md              ← Dieses Dokument
├── .handoff-session1.md          ← Handoff für Frontend-Developer
├── frontend/
│   └── skilllab-pneumonie.html   ← Entwicklungsdatei
├── docs/                         ← GitHub Pages Deployment
│   ├── index.html
│   └── Diagnostik_Pneumonie.png
└── assets/                       ← Referenz-Kopien
```

### Asset-Quellen (original):
| Datei | Pfad |
|---|---|
| `Diagnostik_Pneumonie.png` | `/Users/claasdehero/Desktop/PAL/Projekt Virtuelles Skill Lab/` |
| `svg-hotspot-overlay.svg` | `/Users/claasdehero/Desktop/PAL/Projekt Virtuelles Skill Lab/` |
| `instruments-database.json` | `/Users/claasdehero/Desktop/PAL/Projekt Virtuelles Skill Lab/` |
| `Titelbild.jpg` | `/Users/claasdehero/Desktop/PAL/Projekt Virtuelles Skill Lab/` |

---

## ⚠️ Bekannte technische Besonderheiten

### 1. SVG-Koordinaten: Debug-Pflicht
- SVG `viewBox="0 0 2560 1920"`, Bild 1200×896 → Aspect-Ratio nahezu identisch (4:3)
- Koordinaten skalieren proportional — technisch korrekt
- **Hotspot-Positionen wurden geschätzt** und müssen nach erstem Browser-Test visuell geprüft werden
- **Debug-Modus**: Hotspots mit sichtbarem Stroke rendern (Toggle-Button oder URL-Parameter `?debug=1`)

### 2. Drei Kategorien, zwei Buttons
- JSON hat 3 Kategorien: ESSENTIELL (8), SINNVOLL (6), ABLENKUNG (11)
- UI hat nur 2 Buttons → SINNVOLL braucht Sonderbehandlung
- Implementierung: `if (instrument.category === 'SINNVOLL') → showNeutralFeedback()`

### 3. Kein `fetch()` — alles inline
- SVG inline im HTML (kein CORS-Problem)
- `const INSTRUMENTS = [...]` als JS-Konstante aus instruments-database.json
- Bild als `src="Diagnostik_Pneumonie.png"` (relative Pfad-Referenz, beide Dateien im selben Ordner)

---

## 📋 Impressum-Text (identisch VSDH)

```
Angaben gemäß § 5 TMG:
Claus Clemens
Kirchhofstr. 1
13585 Berlin

Kontakt: claus.clemens@charite.de

Verantwortlich für den Inhalt nach § 18 Abs. 2 MStV:
Claus Clemens, Kirchhofstr. 1, 13585 Berlin

Credits: Idee, Konzept und Umsetzung: Claus Clemens
Technische Unterstützung: Google Gemini, Claude Code (Anthropic)
Bildmaterial: Google Bildgenerierungsmodell

Haftungsausschluss:
„Dieses Spiel dient ausschließlich zu Schulungszwecken und ersetzt keine
medizinische Ausbildung oder professionelle Leitlinien."
```

---

## 🔗 Links & Ressourcen

| Ressource | Link / Pfad |
|---|---|
| Referenz-Projekt VSDH | https://claasdehero-byte.github.io/VSDH/ |
| Deployment-Ziel | https://claasdehero-byte.github.io/skilllab-pneumonie/ |
| Technischer Plan (Gemini) | `Desktop/PAL/Projekt Virtuelles Skill Lab/CLAUDE-CODE-FINAL-PLAN.md` |
| Instruments-Datenbank | `Desktop/PAL/Projekt Virtuelles Skill Lab/instruments-database.json` |

---

**Erstellt:** 2026-04-29  
**Orchestrator:** Claude Code Agency-Orchestrator v1.1  
**Nächste Session:** Frontend-Developer → `skilllab-pneumonie.html` bauen
