# Virtuelles Skill Lab – Pneumonie-Diagnostik

Interaktives digitales Lernmodul für Pflegeauszubildende der Charité Berlin zur Pneumonie-Diagnostik.

**Live:** https://claasdehero-byte.github.io/skilllab-pneumonie/

---

## Über das Projekt

Auszubildende klicken auf 25 Objekte in einem illustrierten Patientenzimmer (Wimmelbild) und entscheiden, ob diese **ESSENTIELL** oder **NICHT ESSENTIELL** für die Primärdiagnose einer Community-acquired Pneumonia (CAP) sind. Nach jeder Entscheidung erscheint leitlinienbasiertes Feedback mit Quellenangabe und Evidenzlevel.

**Szenario:** Hr. Hermann, männlich, Tag 4 nach Symptombeginn, Verdacht auf CAP, Therapieversagen nach Amoxicillin/Clavulansäure.

---

## Spielprinzip

| Kategorie | Anzahl | Klick ESSENTIELL | Klick NICHT ESSENTIELL | Punkte |
|---|---|---|---|---|
| ESSENTIELL | 8 | ✓ Richtig | ✗ Falsch | +10 / 0 |
| ABLENKUNG | 11 | ✗ Falsch | ✓ Richtig | +10 / 0 |
| SINNVOLL | 6 | ⚡ Neutral | ⚡ Neutral | 0 |

**Maximale Punktzahl:** 190 Punkte

---

## Features

- 25 anklickbare Hotspots im Patientenzimmer
- Leitlinienbasiertes Feedback nach jeder Entscheidung (S3-Leitlinie CAP, DNQP, RKI)
- Verlinkung direkt zu den Originalquellen (AWMF, DNQP, RKI)
- CRB-65-Score und diagnostisches Vorgehen A–Z nach Ewig (2016)
- Auswertungs-Screen mit Gesamtübersicht und Punktestand
- Debug-Modus zur Hotspot-Verifikation (`?debug=1` in der URL)
- Funktioniert vollständig lokal ohne Server (`file://` Protokoll)
- Responsives Design für Desktop und Tablet

---

## Quellen & Leitlinien

- **S3-Leitlinie CAP** (AWMF 020-020): https://www.awmf.org/leitlinien/detail/ll/020-020.html
- **DNQP-Expertenstandard Pneumonieprophylaxe:** https://www.dnqp.de/expertenstandards-und-auditinstrumente/
- **RKI – Pneumokokken / Legionellose:** https://www.rki.de
- **Ewig, S. (2016).** *Ambulant erworbene Pneumonie.* Springer.

---

## Technischer Aufbau

| Merkmal | Umsetzung |
|---|---|
| Architektur | Single-File HTML (kein Framework, kein Server) |
| Sprache | Vanilla JavaScript |
| Daten | JS-Konstante inline (kein fetch, kein CORS) |
| Bildgebung | PNG + SVG-Overlay (`viewBox 0 0 2560 1920`) |
| Persistenz | Keine (stateless) |
| Deployment | GitHub Pages (`/docs` Ordner) |

---

## Lokale Nutzung

1. `docs/`-Ordner herunterladen
2. `index.html` im Browser öffnen
3. `Diagnostik_Pneumonie.png` und `Titelbild.jpg` müssen im selben Ordner liegen

---

## Projektstruktur

```
skilllab-pneumonie/
├── docs/                        ← GitHub Pages Deployment
│   ├── index.html
│   ├── Diagnostik_Pneumonie.png
│   └── Titelbild.jpg
├── frontend/                    ← Entwicklungsdatei
│   └── skilllab-pneumonie.html
├── project-brief.md
└── README.md
```

---

## Credits

**Idee, Konzept und Inhalt:** Claus Clemens  
**Technische Umsetzung:** Claude Code (Anthropic)  
**Bildmaterial:** Google Bildgenerierungsmodell  
**Einrichtung:** Charité Berlin, Ausbildungsstation

---

## Haftungsausschluss

Dieses Spiel dient ausschließlich zu Schulungszwecken und ersetzt keine medizinische Ausbildung oder professionelle Leitlinien.
