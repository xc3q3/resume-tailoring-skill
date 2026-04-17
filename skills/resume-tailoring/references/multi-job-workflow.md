# Multi-Job Workflow

## Inhalt

- Ziel
- Wann verwenden
- Runtime-Struktur
- Phase 0: Intake
- Phase 1: Aggregate Gap Analysis
- Phase 2: Shared Experience Discovery
- Phase 3: Per-Job Processing
- Phase 4: Finalisierung
- Inkrementelle Batches
- Fehlerbehandlung

## Ziel

3 bis 5 aehnliche Jobs effizient bearbeiten: eine gemeinsame Bibliotheksanalyse, eine gemeinsame Gap-/Discovery-Phase und danach getrennte Resumes pro Job.

## Wann verwenden

Nutzen, wenn:
- mehrere Jobbeschreibungen oder URLs geliefert werden,
- mehrere Firmen/Rollen in einer Liste stehen,
- der Nutzer Batch-, Mehrfach- oder Serienbewerbungen nennt.

Wenn die Rollen sehr verschieden sind, darauf hinweisen, dass Batch-Vorteile sinken. Bei weniger als etwa 60 Prozent Ueberschneidung getrennte Single-Job-Durchlaeufe empfehlen.

## Runtime-Struktur

Alle dynamischen Ordner- und Dateinamen mit den Pfadregeln aus `SKILL.md` normalisieren. Anzeigenamen in den Dateien bleiben unveraendert.

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

## Phase 0: Intake

Pro Job erfassen:
- `job_id`
- Firma
- Rolle
- JD-Text oder JD-URL
- Prioritaet: `high`, `medium`, `low`; Standard `medium`
- optionale Notizen

Bibliothek einmal fuer den gesamten Batch aufbauen.

`_batch_state.json` direkt nach Intake anlegen oder aktualisieren. Danach jede Phase vor einem Nutzer-Checkpoint und nach jedem fertig verarbeiteten Job speichern.

## Phase 1: Aggregate Gap Analysis

Fuer alle Jobs:
- Must-haves, Nice-to-haves, technische Skills, Soft Skills und Domains extrahieren.
- Gegen Bibliothek matchen.
- Gaps unter 60 Prozent Confidence markieren.
- Deduplizieren.

Priorisierung:
- `critical`: Gap erscheint in 3+ Jobs.
- `important`: Gap erscheint in 2 Jobs.
- `specific`: Gap erscheint in 1 Job.

Erzeuge `_aggregate_gaps.md` mit:
- Coverage pro Job.
- Gap-Liste nach Prioritaet.
- bestem verfuegbarem Match pro Gap.
- Discovery-Fragen, die mehrere Jobs abdecken.

Danach `_batch_state.json` mit Requirements, Coverage und Gap-Status je Job aktualisieren.

## Phase 2: Shared Experience Discovery

Eine Discovery-Session fuer alle priorisierten Gaps:
- Mit critical Gaps beginnen.
- Jede Frage mit Job-Kontext stellen: Welche Jobs profitieren davon?
- Antworten in `_discovered_experiences.md` erfassen.
- Jede Discovery mit betroffenen Jobs und Gaps taggen.
- `_batch_state.json` nach jeder aufgenommenen Discovery aktualisieren, wenn die Session laenger wird oder ein Kontextwechsel droht.

Beispiel:
```text
CI/CD erscheint in 3 Zielrollen. Aktuelles bestes Match: 58 Prozent.
Erzaehl mir von Pipelines, Releases, Tests oder Deployments, die du direkt beeinflusst hast.
```

## Phase 3: Per-Job Processing

Fuer jeden Job einzeln:
- Success Profile erstellen.
- Template entwerfen.
- Bibliothek plus neue Discoveries matchen.
- Resume und Report erzeugen.
- Coverage und Gaps in `content_mapping.md` dokumentieren.
- Job-Status in `_batch_state.json` von `pending` ueber `in_progress` zu `completed`, `failed` oder `skipped` setzen.

Modi:
- `interactive`: Nutzer prueft Struktur und Mapping je Job.
- `express`: Agent trifft konservative Entscheidungen und sammelt Review am Ende.

Standard ist `interactive`, ausser der Nutzer bittet um Tempo.

## Phase 4: Finalisierung

Erzeuge `_batch_summary.md`:
- Jobs, Status und Dateien.
- Coverage pro Job.
- gemeinsame Discoveries.
- wiederverwendete Quellen.
- verbleibende Gaps.
- naechste Schritte je Bewerbung.

Bibliotheks-Update nur nach Freigabe:
- Alle akzeptierten Resumes uebernehmen.
- Nur ausgewaehlte Jobs uebernehmen.
- Nichts uebernehmen.

Zum Schluss `_batch_state.json` und `_batch_summary.md` auf dieselben finalen Job-Status und Dateipfade bringen.

## Inkrementelle Batches

Wenn ein bestehender Batch erweitert wird:
- `_batch_state.json` laden, falls vorhanden.
- Neue Jobs anhaengen.
- Nur neue oder deutlich veraenderte Gaps analysieren.
- Vorhandene Discoveries wiederverwenden.
- Neue Discoveries separat kennzeichnen.

## Fehlerbehandlung

- Einzelner Job scheitert: Status `failed`, Batch laeuft weiter.
- JD unvollstaendig: fehlende Firma/Rolle erfragen oder konservativ extrahieren.
- Keine guten Matches: Gap dokumentieren, Discovery anbieten, nicht erfinden.
- Nutzer will Job entfernen: Job im State als entfernt/uebersprungen markieren, nicht still loeschen.
