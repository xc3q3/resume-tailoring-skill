# resume-tailoring fuer Codex

Lokaler Codex-Skill fuer faktengetreue, zielgerichtete Bewerbungsunterlagen in der Struktur `Bewerbungsunterlagen_2026`. Der Skill analysiert `stationen/` und `wissen/`, wertet Jobbeschreibungen aus, findet belegbare passende Erfahrungen, fuehrt bei Bedarf Erfahrungs-Discovery durch und erzeugt einen zugeschnittenen Markdown-Lebenslauf, eine separate Projektliste und einen Qualitaetsreport in `output/`.

## Ziel

Deine Chancen sollen von echter Erfahrung und Faehigkeit abhaengen, nicht davon, wie gut du Lebenslauf-Texte von Hand optimierst.

Der Skill macht:
- Stationen und Wissensdateien aus deiner Bewerbungsstruktur analysieren,
- Jobbeschreibung in Anforderungen, Keywords, Risiken und narrative Themes zerlegen,
- echte, aber noch nicht dokumentierte Erfahrung durch Fragen sichtbar machen,
- Bullet Points transparent matchen und scoren,
- Wahrheitsschutz bei jedem Reframing erzwingen,
- verpflichtendes 3-Ebenen-Review fuer ATS, HR und Fachbereich vor der finalen Ausgabe durchfuehren,
- Markdown-Lebenslauf, separate Markdown-Projektliste und Markdown-Report unter `output/` erzeugen,
- 2 bis 4 kurze Schluesselprojekt-Teaser im Lebenslauf platzieren und in der Projektliste fachlich vertiefen,
- Pflegevorschlaege fuer `stationen/`, `wissen/`, `TASKS.md` oder `wissen/arbeitsstand.md` nur nach Freigabe schreiben,
- optionale DOCX/PDF-Exporte ohne Claude-spezifische Dokument-Plugins versuchen, wenn der Nutzer sie verlangt.

Der Skill garantiert nicht ohne lokale Werkzeuge:
- DOCX-Erzeugung,
- PDF-Erzeugung,
- Cover Letters,
- LinkedIn-Profiloptimierung.

## Installation

Lokale Installation in Codex:

```bash
mkdir -p ~/.codex/skills
cp -R skills/resume-tailoring ~/.codex/skills/resume-tailoring
```

Alternativ fuer Entwicklung in dieser Repo:

```bash
mkdir -p ~/.codex/skills
ln -s "$(pwd)/skills/resume-tailoring" ~/.codex/skills/resume-tailoring
```

Danach Codex neu starten, falls die Skill-Liste bereits geladen war.

## Vorlagen-Werkbank

Der repo-lokale Ordner `output/` in diesem Skill-Repository ist nur eine Referenz- und Pruefablage fuer bearbeitbare Lebenslaufvorlagen. Er ist nicht der Ausgabeordner fuer echte Bewerbungen und darf nicht als `Bewerbungsunterlagen_2026`-Projektwurzel interpretiert werden.

Aktuell liegen dort:
- `output/_vorlage_Lebenslauf_2026.md`
- `output/_vorlage_Lebenslauf_2026_mapping.md`

Die 2026-Vorlage dient zunaechst als Referenzmaterial. Sie wird erst aktiv befuellt, wenn sie bewusst in ein konkretes Bewerbungsprojekt uebernommen oder dort explizit ausgewaehlt wird. Die bisherigen Vorlagen bleiben kompatibel: `output/_vorlage_lebenslauf.md` ist weiterhin der Standard im Bewerbungsprojekt, `output/_vorlage_whoz.md` bleibt der WHOZ-Export.

## Erwartete Arbeitsstruktur

Der Skill arbeitet standardmaessig mit einer Projektwurzel dieser Form:

```text
Bewerbungsunterlagen_2026/
├── AGENTS.md
├── TASKS.md
├── quellen/
│   ├── rohdaten.pdf
│   ├── zeugnis-firma-a.pdf
│   └── zeugnis-firma-b.pdf
├── stationen/
│   ├── _vorlage.md
│   ├── 01_HeaTec_Versuchsmechaniker.md
│   ├── 02_HeaTec_Konstrukteur.md
│   └── 05_Akkodis_Daimler-Nissan.md
├── output/
│   ├── _vorlage_lebenslauf.md
│   ├── _vorlage_whoz.md
│   └── Name_Stelle_Jahr.md
└── wissen/
    ├── schema.md
    ├── glossar.md
    ├── arbeitsstand.md
    ├── profil.md
    └── karriere/
        ├── _uebersicht.md
        └── kompetenzen.md
```

Wichtige Regeln:
- `stationen/*.md` sind konkrete Erfahrungsquellen; `stationen/_vorlage.md` ist nur Vorlage.
- `wissen/profil.md` ist die autoritative Quelle fuer Berufsprofil und USP.
- `wissen/glossar.md` klaert Abkuerzungen, Firmenkuerzel und Projektnamen.
- `wissen/karriere/_uebersicht.md` und `wissen/karriere/kompetenzen.md` sind aggregierte, pflegbare Wissensdateien.
- `output/_vorlage_lebenslauf.md` ist die primaere Zielstruktur fuer neue Lebenslaeufe.
- `output/_vorlage_whoz.md` wird nur bei ausdruecklichem WHOZ-Wunsch genutzt.
- Das repo-lokale `output/` dieses Skill-Repositories ist nur Vorlagen-Werkbank; echte Bewerbungsoutputs entstehen im `output/` der jeweiligen Bewerbungsprojektwurzel.
- `quellen/` enthaelt Rohmaterial und wird nie veraendert.

## Nutzung

Single-Job:

```text
Nutze $resume-tailoring, um meinen Lebenslauf fuer diese Rolle zuzuschneiden.
Projektwurzel: ./Bewerbungsunterlagen_2026
Jobbeschreibung:
{paste JD}
```

Mehrere Jobs:

```text
Nutze $resume-tailoring fuer diese 3 Rollen:
1. Firma A - Rolle A: {JD oder URL}
2. Firma B - Rolle B: {JD oder URL}
3. Firma C - Rolle C: {JD oder URL}
Projektwurzel: ./Bewerbungsunterlagen_2026
```

Der Skill erkennt Batch-Modus, wenn mehrere Jobbeschreibungen, URLs, Firmen oder Rollen genannt werden.

## Ausgaben

Single-Job:

```text
output/{Name}_{Stelle}_{Jahr}.md
output/{Name}_{Stelle}_{Jahr}_Projektliste.md
output/{Name}_{Stelle}_{Jahr}_Report.md
optional: output/{Name}_{Stelle}_{Jahr}.docx
optional: output/{Name}_{Stelle}_{Jahr}.pdf
optional bei WHOZ-Wunsch: WHOZ-Export anhand output/_vorlage_whoz.md
```

Die Platzhalter in Dateinamen sind normalisierte Pfadsegmente. Anzeigenamen im Dokument bleiben unveraendert; verbotene Dateizeichen werden ersetzt, lange Segmente gekuerzt und Kollisionen mit `-2`, `-3` usw. geloest.

Batch:

```text
output/batches/batch-{YYYY-MM-DD}-{slug}/
├── _batch_state.json
├── _aggregate_gaps.md
├── _discovered_experiences.md
├── _batch_summary.md
├── job-1-{company}/
│   ├── success_profile.md
│   ├── content_mapping.md
│   ├── {Name}_{Stelle}_{Jahr}.md
│   ├── {Name}_{Stelle}_{Jahr}_Projektliste.md
│   └── {Name}_{Stelle}_{Jahr}_Report.md
└── job-2-{company}/
    └── ...
```

Der Lebenslauf bleibt schlank und ATS-/Recruiter-freundlich. Er enthaelt nur 2 bis 4 kurze Projekt-Teaser, z. B. `Projekt: Einfuehrung SAP S/4HANA, siehe Projektliste`.

Die Projektliste ist ein eigenes Bewerbungsdokument. Sie traegt die fachliche Tiefe und beschreibt relevante Projekte mit Kontext, Aufgabe/Rolle, Methode/Technologie, Ergebnis/Wirkung und Relevanz fuer die Zielrolle.

Der Report dokumentiert:
- Zielrolle und Erfolgsprofil,
- Abdeckungsuebersicht,
- Inhaltszuordnung,
- Projekt-Teaser und Projektlisten-Auswahl,
- Reframings mit Wahrheitsbegruendung,
- Qualitaetsreport mit ATS-Abdeckung, HR-Lesbarkeit, fachlicher Substanz, Risiken und Gate-Status,
- verwendete Quellen aus `stationen/` und `wissen/`,
- neu entdeckte Erfahrungen,
- verbleibende Gaps,
- Interview-Prep-Hinweise,
- optionale Pflegevorschlaege.

## Skill-Struktur

```text
skills/resume-tailoring/
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    ├── discovery.md
    ├── matching.md
    ├── multi-job-workflow.md
    ├── quality-review.md
    ├── research.md
    ├── schemas.md
    └── single-job-workflow.md
```

`SKILL.md` bleibt bewusst schlank. Detailregeln werden je nach Phase aus `references/` geladen.

## Arbeitsablauf

1. Intake: Jobbeschreibung, Firma/Rolle und Projektwurzel klaeren.
2. Karrierebasis: `stationen/` und relevante Dateien aus `wissen/` lesen.
3. Recherche: JD und optional Firmen-/Rolleninformationen auswerten.
4. Vorlage: `output/_vorlage_lebenslauf.md` aus der Bewerbungsprojektwurzel verwenden oder konservativen Fallback nutzen; die repo-lokale 2026-Vorlage nur nach bewusster Uebernahme oder expliziter Auswahl befuellen.
5. Discovery: gezielt nach undokumentierter echter Erfahrung fragen.
6. Matching: Kandidaten scoren, Gaps offenlegen, Reframings dokumentieren.
7. Rohdokumente: Lebenslauf mit 2 bis 4 Projekt-Teasern, separate Projektliste und Report entwerfen.
8. 3-Ebenen-Review: ATS, HR und Fachbereich pruefen, belegbare Schwaechen nachschaerfen und verbleibende Luecken dokumentieren.
9. Ausgabe: Markdown-Lebenslauf, Markdown-Projektliste und Markdown-Report in `output/` erzeugen; optionale DOCX/PDF-Exporte nur bei verfuegbaren lokalen Werkzeugen.
10. Strukturpflege: Updates fuer `stationen/`, `wissen/`, `wissen/arbeitsstand.md` oder `TASKS.md` nur nach expliziter Nutzerfreigabe schreiben.

## Designregeln

- Keine erfundenen Erfahrungen.
- Keine erfundenen Metriken.
- Arbeitgeber, Daten und Kernverantwortung bleiben wahr.
- Schwache Matches werden als schwach markiert.
- Gaps duerfen bestehen bleiben.
- Reframing muss belegbar und im Report nachvollziehbar sein.
- Projektliste ist Standard, kein optionaler Zusatz.
- Lebenslauf bleibt schlank; Projekt-Tiefe gehoert in die separate Projektliste.
- CV-Teaser duerfen nur auf Projekte verweisen, die in der Projektliste belegt sind.
- Finale Ausgabe erfordert das 3-Ebenen-Review oder einen transparenten Gate-Status.
- `quellen/` bleibt unveraendert.

## Fallbacks

- Keine Webrecherche: JD-only Analyse plus optionale Rueckfrage.
- Kleine Karrierebasis: Warnung, Discovery priorisieren.
- Fehlende `output/_vorlage_lebenslauf.md`: konservativen Markdown-Lebenslauf erzeugen und im Report nennen.
- Schwache Matches: Gap-Liste statt erzwungener Bullet Points; keine Keywords ohne Evidenz in den Lebenslauf schreiben.
- DOCX/PDF-Wunsch: erst lokale Exportwege pruefen, z. B. vorhandene Repo-Skripte, `pandoc`, `textutil` oder `libreoffice`; wenn nichts verfuegbar ist, Markdown liefern und den fehlenden Exportweg nennen.

## Repository-Scope

Fuer die lokale Codex-Runtime ist `skills/resume-tailoring/` massgeblich. Historisches Claude-/Marketplace-Material wurde aus dem Repository entfernt; relevante Designregeln sind in `SKILL.md` und den Dateien unter `skills/resume-tailoring/references/` konsolidiert.

## Manuelle Pruefung

```bash
rg "stationen|wissen|output/batches|_vorlage_lebenslauf|_vorlage_whoz|_vorlage_Lebenslauf_2026|Projektliste|Qualitaetsreport|3-Ebenen" skills/resume-tailoring README.md
find skills/resume-tailoring/references -type f | sort
```

Erwartung:
- keine alten Standardpfade oder alten Quellenbegriffe bei einer separaten Negativsuche,
- neue Strukturbegriffe sind in Skill und README dokumentiert,
- alle in `SKILL.md` referenzierten Dateien existieren.

## Lizenz

MIT-Lizenz. Siehe `LICENSE`.
