# Mehrjob-Arbeitsablauf

## Inhalt

- Ziel
- Wann verwenden
- Runtime-Struktur
- Phase 0: Intake
- Phase 1: Aggregierte Gap-Analyse
- Phase 2: Gemeinsame Erfahrungs-Discovery
- Phase 3: Verarbeitung und 3-Ebenen-Review pro Job
- Phase 4: Finalisierung
- Inkrementelle Batches
- Fehlerbehandlung

## Ziel

3 bis 5 aehnliche Jobs effizient bearbeiten: eine gemeinsame Analyse der Karrierebasis, eine gemeinsame Gap-/Discovery-Phase und danach getrennte Lebenslaeufe, Projektlisten und Qualitaetsreports pro Job.

## Wann verwenden

Nutzen, wenn:
- mehrere Jobbeschreibungen oder URLs geliefert werden,
- mehrere Firmen/Rollen in einer Liste stehen,
- der Nutzer Batch-, Mehrfach- oder Serienbewerbungen nennt.

Wenn die Rollen sehr verschieden sind, darauf hinweisen, dass Batch-Vorteile sinken. Bei weniger als etwa 60 Prozent Ueberschneidung getrennte Single-Job-Durchlaeufe empfehlen.

## Runtime-Struktur

Alle dynamischen Ordner- und Dateinamen mit den Pfadregeln aus `SKILL.md` normalisieren. Anzeigenamen in den Dateien bleiben unveraendert.

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

## Phase 0: Intake

Pro Job erfassen:
- `job_id`
- Firma
- Rolle
- JD-Text oder JD-URL
- Prioritaet: `high`, `medium`, `low`; Standard `medium`
- optionale Notizen

Karrierebasis einmal fuer den gesamten Batch aufbauen:
- `stationen/*.md` als Stationenquellen.
- `wissen/profil.md`, `wissen/glossar.md`, `wissen/karriere/_uebersicht.md` und `wissen/karriere/kompetenzen.md` als Wissensquellen.
- `output/_vorlage_lebenslauf.md` aus der Bewerbungsprojektwurzel als Zielstruktur, falls vorhanden.
- `output/_vorlage_whoz.md` bleibt nur fuer ausdrueckliche WHOZ-Wuensche relevant.
- Repo-lokale Referenzvorlagen wie `output/_vorlage_Lebenslauf_2026.md` und `output/_vorlage_Lebenslauf_2026_mapping.md` nicht automatisch als Batch-Standard nutzen; sie nur befuellen, wenn sie in die Bewerbungsprojektwurzel uebernommen oder dort explizit ausgewaehlt wurden.
- `quellen/` nicht aendern.

`_batch_state.json` direkt nach Intake anlegen oder aktualisieren. Danach jede Phase vor einem Nutzer-Pruefpunkt und nach jedem fertig verarbeiteten Job speichern.

## Phase 1: Aggregierte Gap-Analyse

Fuer alle Jobs:
- Must-haves, Nice-to-haves, technische Skills, Soft Skills und Domains extrahieren.
- Gegen Karrierebasis matchen.
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

Danach `_batch_state.json` mit Anforderungen, Abdeckung und Gap-Status je Job aktualisieren.

## Phase 2: Gemeinsame Erfahrungs-Discovery

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

## Phase 3: Verarbeitung und 3-Ebenen-Review pro Job

Fuer jeden Job einzeln:
- Erfolgsprofil erstellen.
- Vorlage entwerfen.
- Karrierebasis plus neue Discoveries matchen.
- Roh-Lebenslauf mit 2 bis 4 job-spezifischen Projekt-Teasern erstellen.
- Separate Roh-Projektliste mit den fuer diesen Job wichtigsten Projekten erstellen.
- 3-Ebenen-Review aus `quality-review.md` durchfuehren.
- Belegbare Schwaechen in Lebenslauf und Projektliste nachschaerfen.
- Finale Versionen von Lebenslauf, Projektliste und Report erzeugen.
- Coverage und Gaps in `content_mapping.md` dokumentieren.
- Qualitaetsstatus, Scores und Risiken im Report dokumentieren.
- Job-Status in `_batch_state.json` von `pending` ueber `in_progress` zu `completed`, `failed` oder `skipped` setzen.

Modi:
- `interactive`: Nutzer prueft Struktur und Mapping je Job.
- `express`: Agent trifft konservative Entscheidungen und sammelt Review am Ende.

Standard ist `interactive`, ausser der Nutzer bittet um Tempo.

## Phase 4: Finalisierung

Erzeuge `_batch_summary.md`:
- Jobs, Status und Dateien.
- Coverage pro Job.
- Qualitaetsstatus pro Job: ATS, HR, Fachbereich und Gate-Status.
- gemeinsame Discoveries.
- wiederverwendete Quellen.
- verbleibende Gaps.
- naechste Schritte je Bewerbung.

Strukturpflege nur nach Freigabe:
- Akzeptierte neue Erfahrungen als Vorschlag fuer `stationen/` oder `wissen/karriere/*` uebernehmen.
- `wissen/arbeitsstand.md` oder `TASKS.md` mit offenen Punkten aktualisieren.
- Nichts ausserhalb von `output/batches/` aendern.

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
- Review-Gate nicht bestanden: Status nicht still als completed setzen; Report mit `needs_user_input` oder `pass_with_risks` erzeugen und Ursache nennen.
- Nutzer will Job entfernen: Job im State als entfernt/uebersprungen markieren, nicht still loeschen.
