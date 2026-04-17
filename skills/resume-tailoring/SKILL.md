---
name: resume-tailoring
description: Use when tailoring resumes for specific job applications from a local Markdown resume library. Trigger when the user provides a job description, job URL, or several target jobs and wants truthful resume tailoring, batch processing, experience discovery, evidence-to-requirement matching, Markdown resume/report generation, or optional DOCX/PDF export without Claude-specific tooling or fabricated experience.
---

# Resume Tailoring

## Zweck

Erstellt faktengetreue, zielgerichtete Bewerbungsunterlagen aus einer vorhandenen Resume-Bibliothek. Der Skill optimiert Darstellung, Struktur und Sprache fuer eine konkrete Stelle, erfindet aber keine Erfahrung.

**Kernregel:** Nur belegbare Erfahrung verwenden. Reframing ist erlaubt, wenn Bedeutung, Umfang, Senioritaet, Arbeitgeber und Zeitraeume wahr bleiben.

## Einsatz

Nutze diesen Skill, wenn der Nutzer:
- eine Jobbeschreibung oder Job-URL liefert und ein zugeschnittenes Resume moechte,
- mehrere aehnliche Jobs in einem Batch bearbeiten will,
- bestehende Markdown-Resumes als Quelle nutzen moechte,
- undokumentierte, aber echte Erfahrung ueber Fragen sichtbar machen will.

Nicht als Hauptworkflow nutzen fuer:
- Resume-Erstellung komplett ohne Quellmaterial,
- Cover Letters als eigenstaendiges Ziel,
- LinkedIn-Profiloptimierung,
- verbindliche DOCX/PDF-Erzeugung ohne lokale Export-Werkzeuge. Der Kernoutput ist Markdown; DOCX/PDF nur optional nach Nutzerwunsch.

## Codex-Werkzeugmodell

- Lokale Dateien mit `rg --files`, `rg`, `sed`, `cat` oder vergleichbaren Shell-Kommandos lesen.
- Fuer Job-URLs oder aktuelle Firmeninformationen Webzugriff nur nutzen, wenn verfuegbar und fuer die Aufgabe noetig; sonst JD-only arbeiten und fehlenden Kontext transparent nennen.
- Dateien nur nach Nutzerfreigabe oder im ausdruecklichen Arbeitsauftrag schreiben.
- Bei mehreren Datei-Leseoperationen parallelisieren, wenn sinnvoll.
- Keine Claude-spezifischen Tools, Marketplace-Abhaengigkeiten oder Dokument-Plugins voraussetzen.
- Bibliothek deterministisch scannen: Standard `./resumes/`; rekursiv alle `*.md`, aber generierte Reports, Batch-Artefakte, versteckte Verzeichnisse und offensichtliche Nicht-Resume-Dateien ausschliessen.

## Datei- und Pfadregeln

- Anzeigenamen in Resume und Report unveraendert behalten.
- Dateinamen/Ordnersegmente aus `Name`, `Company`, `Role` und Batch-Slugs normalisieren: trimmen, Leerraeume und verbotene Zeichen (`/ \ : * ? " < > |`) durch `-` ersetzen, wiederholte Trennzeichen zusammenfassen, fuehrende/trailing Trennzeichen entfernen, Segment auf 64 Zeichen begrenzen.
- Wenn ein Zielpfad existiert, nicht ueberschreiben; stattdessen `-2`, `-3` usw. vor der Dateiendung anhaengen.
- Diese Regeln fuer Single-Job-Outputs, Batch-Ordner, `job-{n}-{company_slug}` und optionale Exportdateien verwenden.

## Standard-Workflow

1. **Intake klaeren**
   - Jobbeschreibung als Text oder URL erfassen.
   - Resume-Bibliothek bestimmen; Standard ist `./resumes/`.
   - Bei mehreren Jobs Batch-Modus anbieten, wenn der Nutzer mehrere JDs/URLs/Rollen nennt.

2. **Bibliothek aufbauen**
   - Markdown-Dateien in der Resume-Bibliothek lesen.
   - Rollen, Arbeitgeber, Zeitraeume, Skills, Education und Bullet-Patterns extrahieren.
   - Quellresume je Erfahrung merken.
   - Bei weniger als 3 Resumes warnen und Experience Discovery staerker empfehlen.

3. **Job und Erfolgskriterien analysieren**
   - JD in Must-haves, Nice-to-haves, Keywords, implizite Signale, Risiken und Rollen-Archetyp zerlegen.
   - Optional Firmen-/Rollenrecherche durchfuehren.
   - Ergebnis als Success Profile zusammenfassen und mit dem Nutzer abgleichen.
   - Details: `references/research.md`.

4. **Resume-Struktur entwerfen**
   - Abschnittsreihenfolge, Rollenreihenfolge, Bullet-Budget und eventuelle Titel-/Rollen-Reframings vorschlagen.
   - Arbeitgeber, Daten und Kernverantwortung unveraendert wahr halten.
   - Vor Assembly Nutzerfreigabe einholen.
   - Details: `references/single-job-workflow.md`.

5. **Experience Discovery anbieten**
   - Nur fuer Luecken, schwache Matches oder aktuelle undokumentierte Erfahrung.
   - Fragen dynamisch verzweigen; nicht als statischen Fragebogen abarbeiten.
   - Neu gefundene Erfahrung mit Kontext, Umfang, Quelle der Wahrheit und moeglichem Bullet erfassen.
   - Details: `references/discovery.md`.

6. **Matching und Reframing**
   - Kandidaten-Bullets gegen Template-Slots scoren.
   - Confidence-Bands verwenden: Direct, Transferable, Adjacent, Weak, Gap.
   - Reframings mit Original, neuer Fassung und Wahrheitsbegruendung zeigen.
   - Luecken transparent lassen, statt Inhalte zu erzwingen.
   - Details: `references/matching.md`.

7. **Ausgaben erzeugen**
   - `{Name}_{Company}_{Role}_Resume.md`
   - `{Name}_{Company}_{Role}_Resume_Report.md`
   - optional nach Nutzerwunsch und lokaler Tool-Verfuegbarkeit: `{Name}_{Company}_{Role}_Resume.docx` und `{Name}_{Company}_{Role}_Resume.pdf`
   - Report enthaelt Zielrolle, Success Profile, Mapping, Reframings, Quellen, verbleibende Gaps und Interview-Prep-Hinweise.

8. **Bibliotheks-Update nur nach Freigabe**
   - Nutzer fragt explizit, ob das neue Resume in die Bibliothek uebernommen werden soll.
   - Ohne Freigabe bleiben die erzeugten Dateien im aktuellen Output-Ort.

## Batch-Modus

Batch-Modus eignet sich fuer 3 bis 5 aehnliche Jobs. Ziel ist eine gemeinsame Gap-Analyse und eine gemeinsame Discovery-Session, danach einzelne Resumes pro Job.

Nutze `references/multi-job-workflow.md`, wenn:
- mehrere JDs, URLs, Firmen oder Rollen genannt werden,
- der Nutzer "mehrere", "batch", "3 jobs", "several positions" oder Vergleichbares sagt,
- oder ein bestehender Batch erweitert werden soll.

Batch-Ausgaben:
- `resumes/batches/batch-{YYYY-MM-DD}-{slug}/_batch_state.json`
- `resumes/batches/batch-{YYYY-MM-DD}-{slug}/_aggregate_gaps.md`
- `resumes/batches/batch-{YYYY-MM-DD}-{slug}/_discovered_experiences.md`
- `resumes/batches/batch-{YYYY-MM-DD}-{slug}/_batch_summary.md`
- pro Job `success_profile.md` und `content_mapping.md`
- pro Job `{Name}_{Company}_{Role}_Resume.md`
- pro Job `{Name}_{Company}_{Role}_Resume_Report.md`

Batch-State nach jeder Phase aktualisieren, bevor laengere Verarbeitung oder Nutzer-Checkpoints folgen.

## Referenzen laden

Lade nur die Datei, die fuer die aktuelle Phase benoetigt wird:
- `references/single-job-workflow.md` fuer Einzeldurchlaeufe.
- `references/multi-job-workflow.md` fuer Batch-Verarbeitung.
- `references/research.md` fuer JD-/Firmen-/Rollenanalyse.
- `references/matching.md` fuer Scoring, Gap-Behandlung und Reframing.
- `references/discovery.md` fuer Interview-Fragen.
- `references/schemas.md` fuer Output- und Batch-Strukturen.

## Fallbacks

- **Keine Webrecherche:** JD-only Analyse erstellen und optional nach Firmen-/Teamkontext fragen.
- **Kleine Bibliothek:** Warnen, mit vorhandenem Material arbeiten, Discovery priorisieren.
- **Schwache Matches:** Gaps offenlegen und Optionen anbieten.
- **Laengenproblem:** Niedrigste Relevanz entfernen lassen oder laengeres Resume bewusst bestaetigen.
- **DOCX/PDF-Wunsch:** erst lokale Exportwege pruefen, z. B. vorhandene Repo-Skripte, `pandoc`, `textutil` oder `libreoffice`; wenn nichts verfuegbar ist, Markdown liefern und den fehlenden Exportweg transparent nennen.
