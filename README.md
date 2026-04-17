# Resume Tailoring Skill fuer Codex

Lokaler Codex-Skill fuer faktengetreue, zielgerichtete Bewerbungsunterlagen. Der Skill analysiert eine vorhandene Markdown-Resume-Bibliothek, wertet Jobbeschreibungen aus, findet belegbare passende Erfahrungen, fuehrt bei Bedarf Experience Discovery und erzeugt ein zugeschnittenes Markdown-Resume plus Report. Optional kann Codex DOCX/PDF-Exporte erzeugen, wenn lokale Export-Werkzeuge verfuegbar sind.

## Ziel

Deine Chancen sollen von echter Erfahrung und Faehigkeit abhaengen, nicht davon, wie gut du Resume-Texte von Hand optimierst.

Der Skill macht:
- lokale Resume-Bibliothek aus Markdown-Dateien analysieren,
- Jobbeschreibung in Anforderungen, Keywords, Risiken und narrative Themes zerlegen,
- echte, aber noch nicht dokumentierte Erfahrung durch Fragen sichtbar machen,
- Bullet Points transparent matchen und scoren,
- Wahrheitsschutz bei jedem Reframing erzwingen,
- Markdown-Resume und Markdown-Report erzeugen,
- optionale DOCX/PDF-Exporte ohne Claude-spezifische Dokument-Plugins versuchen, wenn der Nutzer sie verlangt.

Der Skill garantiert nicht ohne lokale Werkzeuge:
- DOCX-Erzeugung,
- PDF-Erzeugung,
- Cover Letters,
- LinkedIn-Profiloptimierung,
- Claude Marketplace Distribution.

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

## Voraussetzungen

Erforderlich:
- Codex mit Skill-Unterstuetzung.
- Mindestens ein vorhandenes Resume als Markdown-Datei.

Empfohlen:
- mehrere bestehende Resumes fuer bessere Match-Auswahl,
- eine lokale Struktur wie `./resumes/`,
- Webzugriff nur dann, wenn Firmen- oder Rollenrecherche benoetigt wird.

Beispiel:

```text
resumes/
├── Resume_General_2024.md
├── Resume_Product_Manager.md
└── Resume_Technical_Program_Manager.md
```

## Nutzung

Single-Job:

```text
Use $resume-tailoring to tailor my resume for this role.
Resume library: ./resumes
Job description:
{paste JD}
```

Mehrere Jobs:

```text
Use $resume-tailoring for these 3 roles:
1. Company A - Role A: {JD or URL}
2. Company B - Role B: {JD or URL}
3. Company C - Role C: {JD or URL}
Resume library: ./resumes
```

Der Skill erkennt Batch-Modus, wenn mehrere Jobbeschreibungen, URLs, Firmen oder Rollen genannt werden.

## Ausgaben

Single-Job:

```text
{Name}_{Company}_{Role}_Resume.md
{Name}_{Company}_{Role}_Resume_Report.md
optional: {Name}_{Company}_{Role}_Resume.docx
optional: {Name}_{Company}_{Role}_Resume.pdf
```

Die Platzhalter in Dateinamen sind normalisierte Pfadsegmente. Anzeigenamen im Dokument bleiben unveraendert; verbotene Dateizeichen werden ersetzt, lange Segmente gekuerzt und Kollisionen mit `-2`, `-3` usw. geloest.

Batch:

```text
resumes/batches/batch-{YYYY-MM-DD}-{slug}/
├── _batch_state.json
├── _aggregate_gaps.md
├── _discovered_experiences.md
├── _batch_summary.md
├── job-1-{company}/
│   ├── success_profile.md
│   ├── content_mapping.md
│   ├── {Name}_{Company}_{Role}_Resume.md
│   └── {Name}_{Company}_{Role}_Resume_Report.md
└── job-2-{company}/
    └── ...
```

Der Report dokumentiert:
- Zielrolle und Success Profile,
- Coverage Summary,
- Content Mapping,
- Reframings mit Wahrheitsbegruendung,
- verwendete Quellresumes,
- neu entdeckte Erfahrungen,
- verbleibende Gaps,
- Interview-Prep-Hinweise.

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
    ├── research.md
    ├── schemas.md
    └── single-job-workflow.md
```

`SKILL.md` bleibt bewusst schlank. Detailregeln werden je nach Phase aus `references/` geladen.

## Workflow

1. Intake: Jobbeschreibung, Firma/Rolle und Resume-Bibliothek klaeren.
2. Bibliothek: lokale Markdown-Resumes lesen und Erfahrung indexieren.
3. Research: JD und optional Firmen-/Rolleninformationen auswerten.
4. Template: Struktur, Rolle, Skills und Bullet-Budget planen.
5. Discovery: gezielt nach undokumentierter echter Erfahrung fragen.
6. Matching: Kandidaten scoren, Gaps offenlegen, Reframings dokumentieren.
7. Output: Markdown-Resume und Markdown-Report erzeugen; optionale DOCX/PDF-Exporte nur bei verfuegbaren lokalen Werkzeugen.
8. Library Update: nur nach expliziter Nutzerfreigabe uebernehmen.

## Designregeln

- Keine erfundenen Erfahrungen.
- Keine erfundenen Metriken.
- Arbeitgeber, Daten und Kernverantwortung bleiben wahr.
- Schwache Matches werden als schwach markiert.
- Gaps duerfen bestehen bleiben.
- Reframing muss belegbar und im Report nachvollziehbar sein.

## Fallbacks

- Keine Webrecherche: JD-only Analyse plus optionale Rueckfrage.
- Kleine Bibliothek: Warnung, Discovery priorisieren.
- Schwache Matches: Gap-Liste statt erzwungener Bullet Points.
- DOCX/PDF-Wunsch: erst lokale Exportwege pruefen, z. B. vorhandene Repo-Skripte, `pandoc`, `textutil` oder `libreoffice`; wenn nichts verfuegbar ist, Markdown liefern und den fehlenden Exportweg nennen.

## Legacy-Dateien

Einige Root-Dokumente stammen aus der frueheren Claude-/Marketplace-Fassung und bleiben als Historie oder Designmaterial erhalten:
- `MARKETPLACE.md`
- `SUBMISSION_GUIDE.md`
- `.claude-plugin/plugin.json`
- alte Multi-Job-Planungsdokumente unter `docs/`

Fuer die lokale Codex-Runtime ist nur `skills/resume-tailoring/` massgeblich. Die Legacy-Dateien sind archiviert, werden von Codex nicht geladen und duerfen keine Runtime-Zusagen fuer den Codex-Skill uebersteuern.

## Manuelle Pruefung

```bash
rg "WebSearch|WebFetch|document-skills|~/.claude|Claude Code" skills/resume-tailoring
find skills/resume-tailoring/references -type f | sort
```

Erwartung:
- keine verbindlichen Claude-spezifischen Runtime-Abhaengigkeiten im Skill-Ordner,
- alle in `SKILL.md` referenzierten Dateien existieren.

## Lizenz

MIT License. Siehe `LICENSE`.
