# Single-Job Workflow

## Inhalt

- Ziel
- Phase 0: Intake und Bibliothek
- Phase 1: Success Profile
- Phase 2: Struktur und Template
- Phase 3: Assembly
- Phase 4: Ausgabe
- Phase 5: Library Update

## Ziel

Ein faktengetreues, auf eine konkrete Rolle zugeschnittenes Markdown-Resume plus Report erzeugen.

## Phase 0: Intake und Bibliothek

Erfasse:
- Jobbeschreibung als Text oder URL.
- Firma und Rolle, falls nicht eindeutig in der JD.
- Resume-Bibliothek; Standard `./resumes/`.
- Optional Output-Ordner; Standard aktuelles Arbeitsverzeichnis.

Bibliothek:
- Standardpfad `./resumes/` verwenden, wenn der Nutzer keinen anderen Pfad nennt; wenn der Pfad fehlt, danach fragen.
- Rekursiv `*.md` lesen, aber versteckte Verzeichnisse, `batches/`, `*_Resume_Report.md`, `_batch_*.md`, `content_mapping.md`, `success_profile.md`, `_aggregate_gaps.md` und `_discovered_experiences.md` ausschliessen.
- Rollen, Arbeitgeber, Titel, Daten, Bullet Points, Skills, Education und Kontaktblock extrahieren.
- Bullet-Quellen merken, damit der Report nachvollziehbar bleibt.
- Typische Laenge, Abschnittsfolge, Ton und Bullet-Stil erkennen.

Wenn die Bibliothek sehr klein ist, transparent sagen, dass weniger Match-Varianten verfuegbar sind.

## Phase 1: Success Profile

Analysiere die JD und optional oeffentliche Kontextdaten:
- Must-have Anforderungen.
- Nice-to-have Anforderungen.
- Technische und domain-spezifische Keywords.
- Implizite Signale wie Ownership, Tempo, Stakeholder, Regulierungsumfeld.
- Risiken oder Luecken im vorhandenen Profil.
- Rollen-Archetyp: IC, Lead, Manager, Research, Product, Program, Hybrid.

Praesentiere kurz:
- Top 5 Anforderungen.
- 3 bis 5 narrative Themes.
- auffaellige Risiken oder Gaps.
- Terminologie, die das Resume verwenden sollte.

Hole Nutzerfeedback ein, wenn das Profil unsicher oder interpretationsbeduerftig ist.

## Phase 2: Struktur und Template

Erzeuge eine Resume-Struktur:
- Summary mit 2 bis 4 Saetzen.
- Skills in 2 bis 4 Kategorien, passend zur JD.
- Professional Experience nach Relevanz und Chronologie.
- Education und optionale Abschnitte nur, wenn sie den Fit verbessern.

Rollen-Konsolidierung:
- Gleiche Firma und aehnliche Aufgaben koennen zusammengefasst werden.
- Unterschiedliche Firmen nie zusammenfassen.
- Unterschiedliche Rollen bei derselben Firma getrennt halten, wenn Progression oder stark abweichende Verantwortung wichtig ist.

Titel-Reframing:
- Nur branchenuebliche oder klarere Titelvarianten vorschlagen.
- Senioritaet nicht aufblasen.
- Originaltitel im Report dokumentieren, wenn sichtbar umformuliert wird.

Vor dem Fuellen des Templates die wichtigsten Strukturentscheidungen bestaetigen lassen.

## Phase 3: Assembly

Fuelle Template-Slots mit den besten belegbaren Erfahrungen:
- Pro Slot Top-Kandidaten aus Bibliothek und Discovery betrachten.
- Scoring aus `matching.md` verwenden.
- Wiederholungen vermeiden.
- Jede starke Umformulierung mit Original und Begruendung im Report festhalten.

Bei Gaps:
- Beste verfuegbare Erfahrung mit Score nennen.
- Discovery anbieten, falls noch nicht erfolgt.
- Slot weglassen, Report-/Interview-Prep-Hinweis oder schwaches Match nur nach Nutzerentscheidung verwenden.

## Phase 4: Ausgabe

Erzeuge:
- `{Name}_{Company}_{Role}_Resume.md`
- `{Name}_{Company}_{Role}_Resume_Report.md`
- optional nach Nutzerwunsch und lokaler Tool-Verfuegbarkeit `{Name}_{Company}_{Role}_Resume.docx`
- optional nach Nutzerwunsch und lokaler Tool-Verfuegbarkeit `{Name}_{Company}_{Role}_Resume.pdf`

Dateinamen aus normalisierten Segmenten bilden, Anzeigenamen im Dokument aber unveraendert lassen. Zielpfade nie ueberschreiben; bei Kollision `-2`, `-3` usw. anhaengen.

Resume-Struktur:
```markdown
# {Name}

{Contact}

## Professional Summary

{Summary}

## Key Skills

**{Category}:** {Skill list}

## Professional Experience

### {Title}
**{Company} | {Location} | {Dates}**

- {Achievement bullet}
- {Achievement bullet}

## Education

{Education}
```

Report-Struktur:
```markdown
# Resume Generation Report

## Target Role
## Success Profile
## Coverage Summary
## Content Mapping
## Reframings
## Source Resumes Used
## Remaining Gaps
## Interview Prep Notes
```

Optionale Exporte:
- Erst Markdown-Resume finalisieren.
- Lokale Exportwege pruefen, etwa vorhandene Repo-Skripte, `pandoc`, `textutil` oder `libreoffice`.
- Export nur erzeugen, wenn das Tool verfuegbar ist und das Ergebnis sinnvoll verifiziert werden kann.
- Wenn Export scheitert oder kein Tool vorhanden ist, Markdown und Report behalten und den fehlenden Export transparent melden.

## Phase 5: Library Update

Nach Review fragen:
- In Bibliothek uebernehmen.
- Dateien behalten, aber nicht uebernehmen.
- Revisionen durchfuehren.

Nur nach expliziter Zustimmung Dateien in die Resume-Bibliothek kopieren oder verschieben.
