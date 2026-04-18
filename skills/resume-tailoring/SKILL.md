---
name: resume-tailoring
description: Verwenden, wenn Lebenslaeufe, separate Projektlisten und Qualitaetsreports aus der lokalen Bewerbungsunterlagen_2026-Struktur fuer konkrete Bewerbungen zugeschnitten werden sollen. Ausloesen, wenn der Nutzer eine Jobbeschreibung, Job-URL oder mehrere Zieljobs liefert und faktengetreues Lebenslauf-Tailoring aus stationen/, wissen/ und output/-Vorlagen, Batch-Verarbeitung, Erfahrungs-Discovery, evidenzbasiertes Matching, verpflichtendes 3-Ebenen-Review, Markdown-Lebenslauf/Projektliste/Report-Erzeugung oder optionalen DOCX/PDF-Export ohne Claude-spezifische Werkzeuge und ohne erfundene Erfahrung moechte.
---

# Lebenslauf-Tailoring

## Zweck

Erstellt faktengetreue, zielgerichtete Bewerbungsunterlagen aus der lokalen Struktur `Bewerbungsunterlagen_2026`. Der Skill optimiert Darstellung, Struktur und Sprache fuer eine konkrete Stelle, erfindet aber keine Erfahrung.

Standardausgabe sind drei Artefakte:
- schlanker, ATS-tauglicher Lebenslauf,
- separate, substanzstarke Projektliste,
- kompakter Qualitaetsreport mit ATS-, HR- und Fachbereichsbewertung.

**Kernprinzip:** CV = schnell entscheidungsfaehig; Projektliste = fachlich tief ueberzeugend.

**Kernregel:** Nur belegbare Erfahrung verwenden. Reframing ist erlaubt, wenn Bedeutung, Umfang, Senioritaet, Arbeitgeber und Zeitraeume wahr bleiben.

## Einsatz

Nutze diesen Skill, wenn der Nutzer:
- eine Jobbeschreibung oder Job-URL liefert und einen zugeschnittenen Lebenslauf moechte,
- eine separate Projektliste oder projektbasierte fachliche Vertiefung braucht,
- mehrere aehnliche Jobs in einem Batch bearbeiten will,
- bestehende Markdown-Stationen und Wissensdateien als Quelle nutzen moechte,
- undokumentierte, aber echte Erfahrung ueber Fragen sichtbar machen will.

Nicht als Hauptworkflow nutzen fuer:
- Lebenslauf-Erstellung komplett ohne Quellmaterial in `stationen/` oder `wissen/`,
- Cover Letters als eigenstaendiges Ziel,
- LinkedIn-Profiloptimierung,
- verbindliche DOCX/PDF-Erzeugung ohne lokale Export-Werkzeuge. Der Kernoutput ist Markdown; DOCX/PDF nur optional nach Nutzerwunsch.

## Projektstruktur

Standard ist eine Projektwurzel mit dieser Form:

```text
Bewerbungsunterlagen_2026/
├── AGENTS.md
├── TASKS.md
├── quellen/
├── stationen/
│   ├── _vorlage.md
│   └── NN_Firma_Rolle.md
├── output/
│   ├── _vorlage_lebenslauf.md
│   └── _vorlage_whoz.md
└── wissen/
    ├── schema.md
    ├── glossar.md
    ├── arbeitsstand.md
    ├── profil.md
    └── karriere/
        ├── _uebersicht.md
        └── kompetenzen.md
```

Root-Erkennung:
- Wenn der Nutzer einen Pfad nennt, diesen als Projektwurzel pruefen.
- Sonst das aktuelle Arbeitsverzeichnis pruefen.
- Eine gueltige Projektwurzel enthaelt mindestens `AGENTS.md`, `stationen/`, `wissen/` und `output/`.
- Wenn keine gueltige Projektwurzel gefunden wird, nach dem Pfad fragen.

## Codex-Werkzeugmodell

- Lokale Dateien mit `rg --files`, `rg`, `sed`, `cat` oder vergleichbaren Shell-Kommandos lesen.
- Fuer Job-URLs oder aktuelle Firmeninformationen Webzugriff nur nutzen, wenn verfuegbar und fuer die Aufgabe noetig; sonst JD-only arbeiten und fehlenden Kontext transparent nennen.
- Dateien nur nach Nutzerfreigabe oder im ausdruecklichen Arbeitsauftrag schreiben.
- Bei mehreren Datei-Leseoperationen parallelisieren, wenn sinnvoll.
- Keine Claude-spezifischen Tools, Marketplace-Abhaengigkeiten oder Dokument-Plugins voraussetzen.
- Karrierebasis deterministisch scannen: `stationen/*.md` plus relevante Dateien unter `wissen/`.
- `stationen/_vorlage.md` und `output/_vorlage_*.md` als Vorlagen lesen, aber nie als belegte Erfahrung werten.
- `quellen/` ist read-only Rohmaterial. Nur bei expliziter Extraktions- oder Evidenzpruefung lesen, niemals aendern.

## Datei- und Pfadregeln

- Anzeigenamen in Lebenslauf, Projektliste und Report unveraendert behalten.
- Dateinamen/Ordnersegmente aus `Name`, `Stelle`, `Jahr`, `Company`, `Role` und Batch-Slugs normalisieren: trimmen, Leerraeume und verbotene Zeichen (`/ \ : * ? " < > |`) durch `-` ersetzen, wiederholte Trennzeichen zusammenfassen, fuehrende/trailing Trennzeichen entfernen, Segment auf 64 Zeichen begrenzen.
- Wenn ein Zielpfad existiert, nicht ueberschreiben; stattdessen `-2`, `-3` usw. vor der Dateiendung anhaengen.
- `Name` kommt aus `wissen/profil.md`, der Vorlage oder Nutzerkontext; `Stelle` aus der Zielrolle; `Jahr` ist standardmaessig das aktuelle Jahr.
- Diese Regeln fuer Single-Job-Outputs, Batch-Ordner, `job-{n}-{company_slug}` und optionale Exportdateien verwenden.

## Standard-Arbeitsablauf

1. **Intake klaeren**
   - Jobbeschreibung als Text oder URL erfassen.
   - Projektwurzel bestimmen und Struktur validieren.
   - Bei mehreren Jobs Batch-Modus anbieten, wenn der Nutzer mehrere JDs/URLs/Rollen nennt.

2. **Karrierebasis aufbauen**
   - `stationen/*.md` lesen, ausser `stationen/_vorlage.md`.
   - `wissen/profil.md` als autoritative USP-/Profilquelle lesen, wenn vorhanden.
   - `wissen/glossar.md` fuer Abkuerzungen, Firmenkuerzel und Projektnamen nutzen.
   - `wissen/karriere/_uebersicht.md` und `wissen/karriere/kompetenzen.md` als aggregierte, pflegbare Wissensdateien lesen.
   - `wissen/schema.md` und `wissen/arbeitsstand.md` als Arbeitskontext lesen, wenn sie fuer Struktur oder Status helfen.
   - Rollen, Arbeitgeber, Zeitraeume, Kompetenzen, Ausbildung und Bullet-Patterns extrahieren.
   - Quelle je Erfahrung als konkreten Pfad merken.
   - Bei wenigen Stationen transparent sagen, dass weniger Match-Varianten verfuegbar sind.

3. **Job und Erfolgskriterien analysieren**
   - JD in Must-haves, Nice-to-haves, Keywords, implizite Signale, Risiken und Rollen-Archetyp zerlegen.
   - Optional Firmen-/Rollenrecherche durchfuehren.
   - Ergebnis als Erfolgsprofil zusammenfassen und mit dem Nutzer abgleichen.
   - Details: `references/research.md`.

4. **Dokumentstruktur entwerfen**
   - `output/_vorlage_lebenslauf.md` als primaere Zielstruktur verwenden, wenn vorhanden.
   - Wenn die Vorlage fehlt, konservative Markdown-Struktur nutzen und den Fallback im Report nennen.
   - Abschnittsreihenfolge, Rollenreihenfolge, Bullet-Budget und eventuelle Titel-/Rollen-Reframings vorschlagen.
   - Separate Projektliste als Pflichtartefakt einplanen.
   - 2 bis 4 Schluesselprojekt-Teaser fuer den Lebenslauf vorsehen; sie muessen kurz bleiben und in der Projektliste belegbar ausgearbeitet werden.
   - Arbeitgeber, Daten und Kernverantwortung unveraendert wahr halten.
   - Vor dem Zusammenbau Nutzerfreigabe einholen.
   - Details: `references/single-job-workflow.md`.

5. **Erfahrungs-Discovery anbieten**
   - Nur fuer Luecken, schwache Matches oder aktuelle undokumentierte Erfahrung.
   - Fragen dynamisch verzweigen; nicht als statischen Fragebogen abarbeiten.
   - Neu gefundene Erfahrung mit Kontext, Umfang, Quelle der Wahrheit und moeglichem Bullet erfassen.
   - Details: `references/discovery.md`.

6. **Matching und Reframing**
   - Kandidaten-Bullets gegen Vorlagen-Slots scoren.
   - Confidence-Bands verwenden: Direkt, uebertragbar, angrenzend, schwach, Gap.
   - Reframings mit Original, neuer Fassung und Wahrheitsbegruendung zeigen.
   - Luecken transparent lassen, statt Inhalte zu erzwingen.
   - Details: `references/matching.md`.

7. **Rohdokumente erzeugen**
   - Roh-Lebenslauf mit schlanker Standardstruktur und 2 bis 4 kurzen Projekt-Teasern erstellen.
   - Separate Roh-Projektliste mit Kontext, Aufgabe, Methode/Technologie und Ergebnis/Wirkung pro relevantem Projekt erstellen.
   - Roh-Report mit Matching, Quellen, Reframings und Gaps erstellen.
   - Projekt-Teaser duerfen nur Projekte nennen, die in der Projektliste vollstaendig und belegbar ausgearbeitet sind.

8. **3-Ebenen-Review als Pflicht-Gate**
   - Vor jeder finalen Ausgabe Lebenslauf und Projektliste gemeinsam pruefen: ATS-Ebene, HR-Ebene, Fachbereichs-Ebene.
   - Belegbare Schwaechen aktiv nachschaerfen; unbelegbare Luecken transparent im Report dokumentieren.
   - Keine finale Ausgabe erzeugen, solange unbelegte Behauptungen, irrefuehrende Keywords oder Projekt-Teaser ohne Projektlistennachweis enthalten sind.
   - Details: `references/quality-review.md`.

9. **Finale Ausgaben erzeugen**
   - `output/{Name}_{Stelle}_{Jahr}.md`
   - `output/{Name}_{Stelle}_{Jahr}_Projektliste.md`
   - `output/{Name}_{Stelle}_{Jahr}_Report.md`
   - optional nach ausdruecklichem Nutzerwunsch und vorhandener Vorlage: WHOZ-Export nach `output/_vorlage_whoz.md`
   - optional nach Nutzerwunsch und lokaler Tool-Verfuegbarkeit: `output/{Name}_{Stelle}_{Jahr}.docx` und `output/{Name}_{Stelle}_{Jahr}.pdf`
   - Report enthaelt Zielrolle, Erfolgsprofil, Zuordnung, Reframings, Quellen, verbleibende Gaps, Qualitaetsreport und Hinweise zur Interviewvorbereitung.

10. **Strukturpflege nur nach Freigabe**
   - Neue echte Erfahrungen oder Korrekturen als Vorschlag fuer `stationen/`, `wissen/karriere/_uebersicht.md`, `wissen/karriere/kompetenzen.md`, `wissen/arbeitsstand.md` oder `TASKS.md` vorbereiten.
   - Erst nach expliziter Zustimmung schreiben.
   - Ohne Freigabe bleiben nur die erzeugten Dateien unter `output/`.

## Batch-Modus

Batch-Modus eignet sich fuer 3 bis 5 aehnliche Jobs. Ziel ist eine gemeinsame Gap-Analyse und eine gemeinsame Discovery-Session, danach einzelne Lebenslaeufe pro Job.

Nutze `references/multi-job-workflow.md`, wenn:
- mehrere JDs, URLs, Firmen oder Rollen genannt werden,
- der Nutzer "mehrere", "batch", "3 jobs", "several positions" oder Vergleichbares sagt,
- oder ein bestehender Batch erweitert werden soll.

Batch-Ausgaben:
- `output/batches/batch-{YYYY-MM-DD}-{slug}/_batch_state.json`
- `output/batches/batch-{YYYY-MM-DD}-{slug}/_aggregate_gaps.md`
- `output/batches/batch-{YYYY-MM-DD}-{slug}/_discovered_experiences.md`
- `output/batches/batch-{YYYY-MM-DD}-{slug}/_batch_summary.md`
- pro Job `success_profile.md` und `content_mapping.md`
- pro Job `{Name}_{Stelle}_{Jahr}.md`
- pro Job `{Name}_{Stelle}_{Jahr}_Projektliste.md`
- pro Job `{Name}_{Stelle}_{Jahr}_Report.md`

Batch-State nach jeder Phase aktualisieren, bevor laengere Verarbeitung oder Nutzer-Pruefpunkte folgen. Jeder Job muss sein eigenes 3-Ebenen-Review bestehen oder seine verbleibenden Gaps transparent dokumentieren.

## Referenzen laden

Lade nur die Datei, die fuer die aktuelle Phase benoetigt wird:
- `references/single-job-workflow.md` fuer Einzeldurchlaeufe.
- `references/multi-job-workflow.md` fuer Batch-Verarbeitung.
- `references/research.md` fuer JD-/Firmen-/Rollenanalyse.
- `references/matching.md` fuer Scoring, Gap-Behandlung und Reframing.
- `references/discovery.md` fuer Interview-Fragen.
- `references/quality-review.md` fuer ATS-, HR- und Fachbereichsreview vor der finalen Ausgabe.
- `references/schemas.md` fuer Ausgabe- und Batch-Strukturen.

## Fallbacks

- **Keine Webrecherche:** JD-only Analyse erstellen und optional nach Firmen-/Teamkontext fragen.
- **Kleine Karrierebasis:** Warnen, mit vorhandenem Material arbeiten, Discovery priorisieren.
- **Schwache Matches:** Gaps offenlegen und Optionen anbieten.
- **Laengenproblem:** Lebenslauf schlank halten, Tiefe in die Projektliste verlagern und nur die wichtigsten 2 bis 4 Projekt-Teaser im CV behalten.
- **DOCX/PDF-Wunsch:** erst lokale Exportwege pruefen, z. B. vorhandene Repo-Skripte, `pandoc`, `textutil` oder `libreoffice`; wenn nichts verfuegbar ist, Markdown liefern und den fehlenden Exportweg transparent nennen.
