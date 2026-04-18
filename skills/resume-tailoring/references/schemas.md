# Schemata

## Inhalt

- JobState
- BatchState
- DiscoveredExperience
- GapItem
- KeywordCoverage
- ProjectTeaser
- ProjectList
- QualityReview
- PathSegment
- Lebenslauf-Report
- Strukturpflege-Vorschlag

## JobState

```json
{
  "job_id": "job-1",
  "company": "Firma",
  "role": "Rolle",
  "company_slug": "company",
  "role_slug": "role",
  "jd_text": "Jobbeschreibung",
  "jd_url": null,
  "priority": "medium",
  "notes": "",
  "status": "pending",
  "current_phase": null,
  "coverage": null,
  "files_generated": false,
  "output_paths": [],
  "resume_path": null,
  "project_list_path": null,
  "report_path": null,
  "project_teasers": [],
  "quality_review": null,
  "last_updated": "ISO-8601-Zeitstempel",
  "requirements": [],
  "gaps": []
}
```

Status:
- `pending`
- `in_progress`
- `completed`
- `failed`
- `skipped`

## BatchState

```json
{
  "batch_id": "batch-YYYY-MM-DD-slug",
  "created": "ISO-8601-Zeitstempel",
  "last_updated": "ISO-8601-Zeitstempel",
  "output_dir": "output/batches/batch-YYYY-MM-DD-slug",
  "current_phase": "intake",
  "processing_mode": "interactive",
  "jobs": [],
  "discoveries": [],
  "aggregate_gaps": {
    "critical_gaps": [],
    "important_gaps": [],
    "job_specific_gaps": []
  }
}
```

Phasen:
- `intake`
- `gap_analysis`
- `discovery`
- `per_job_processing`
- `finalization`

## DiscoveredExperience

```json
{
  "experience_id": "disc-1",
  "text": "",
  "context": "",
  "scope": "",
  "evidence_source": "stationen/02_Beispiel_Rolle.md",
  "addresses_jobs": [],
  "addresses_gaps": [],
  "confidence_improvement": {},
  "integrated": false,
  "bullet_draft": ""
}
```

## GapItem

```json
{
  "requirement": "",
  "confidence": 0,
  "gap_type": "critical",
  "best_match": "",
  "recommended_action": ""
}
```

## KeywordCoverage

```json
{
  "keyword": "Requirements Engineering",
  "category": "must",
  "synonyms": ["Anforderungsmanagement"],
  "status": "covered",
  "evidence_source": "stationen/NN_Firma_Rolle.md",
  "document_location": "resume",
  "recommended_action": ""
}
```

Kategorien:
- `must`
- `optional`
- `synonym`

Status:
- `covered`
- `covered_by_synonym`
- `project_only`
- `missing_but_evidence_available`
- `missing_no_evidence`
- `unsupported_claim`

## ProjectTeaser

```json
{
  "project_name": "Projektname",
  "teaser_text": "Projekt: Projektname, siehe Projektliste",
  "target_requirement": "wichtige JD-Anforderung",
  "project_list_anchor": "Projekt: Projektname",
  "evidence_source": "stationen/NN_Firma_Rolle.md"
}
```

Regeln:
- 2 bis 4 Teaser pro Lebenslauf.
- Maximal ein kurzer Bullet oder eine knappe Zeile pro Projekt.
- Jeder Teaser braucht einen vollstaendigen Projektlisteneintrag.

## ProjectList

```json
{
  "title": "Projektliste: Name fuer Rolle",
  "projects": [
    {
      "project_name": "Projektname",
      "context": "",
      "role_or_task": "",
      "method_or_technology": "",
      "result_or_impact": "",
      "relevance_for_role": "",
      "evidence_sources": ["stationen/NN_Firma_Rolle.md"],
      "covered_requirements": []
    }
  ]
}
```

Projektlisten-Regeln:
- Eigene Datei `output/{Name}_{Stelle}_{Jahr}_Projektliste.md`.
- Substanztraeger fuer technische, ingenieurnahe, IT-, Beratungs- und Projektrollen.
- Keine unbelegten Tools, Metriken, Rollen oder Verantwortungen.

## QualityReview

```json
{
  "ats": {
    "score": 0,
    "keyword_coverage": [],
    "gaps": [],
    "improvements": []
  },
  "hr": {
    "score": 0,
    "scan_result": "",
    "issues": [],
    "improvements": []
  },
  "substance": {
    "score": 0,
    "covered_requirements": [],
    "missing_evidence": [],
    "improvements": []
  },
  "risks": [],
  "concrete_improvement_suggestions": [],
  "final_gate_status": "pass_with_risks"
}
```

Gate-Status:
- `pass`
- `pass_with_risks`
- `needs_user_input`

## PathSegment

Pfadsegmente aus Nutzerdaten nicht direkt verwenden.

```json
{
  "display_value": "Firma / Rolle: Beispiel",
  "path_value": "Firma-Rolle-Beispiel",
  "max_length": 64,
  "collision_suffix": "-2"
}
```

Regeln:
- `display_value` bleibt im Lebenslauf, in der Projektliste und im Report erhalten.
- `path_value` ersetzt Leerraeume und verbotene Dateisystemzeichen durch `-`.
- Bei Kollisionen Suffix vor Dateiendung oder am Ordnernamen erhoehen.
- Single-Job-Ausgaben liegen unter `output/{Name}_{Stelle}_{Jahr}.md`, `output/{Name}_{Stelle}_{Jahr}_Projektliste.md` und `output/{Name}_{Stelle}_{Jahr}_Report.md`.
- Batch-Ausgaben liegen unter `output/batches/batch-{YYYY-MM-DD}-{slug}/`.

## Quellenmodell

Quellen im Report als konkrete Pfade ausweisen:
- `stationen/NN_Firma_Rolle.md` oder `stationen/NN_Firma_Projekt.md`
- `wissen/profil.md`
- `wissen/glossar.md`
- `wissen/karriere/_uebersicht.md`
- `wissen/karriere/kompetenzen.md`
- Discovery-ID fuer neu erfragte, noch nicht eingepflegte Erfahrung

`output/_vorlage_lebenslauf.md` und `output/_vorlage_whoz.md` sind Zielvorlagen, keine Evidenzquellen. `quellen/` ist read-only Rohmaterial und darf nie veraendert werden.

## Lebenslauf-Report

```markdown
# Lebenslauf-Erzeugungsreport

## Zielrolle
- Firma:
- Rolle:
- Jobquelle:
- Erzeugt:

## Erfolgsprofil
- Kernanforderungen:
- Narrative Themen:
- Risiken:

## Abdeckungsuebersicht
- Gesamtabdeckung:
- Direct:
- Transferable:
- Adjacent:
- Weak:
- Gaps:

## Inhaltszuordnung

## Projekt-Teaser und Projektliste
- Teaser:
- Projektlistenpfad:
- Nicht genutzte Projektkandidaten:

## Reframings

## Qualitaetsreport
### ATS-Abdeckung
- Score:
- Luecken:
- Nachschaerfungen:

### HR-Lesbarkeit
- Score:
- Hinweise:
- Nachschaerfungen:

### Fachliche Substanz
- Score:
- Fehlende Nachweise:
- Nachschaerfungen:

### Risiken

### Konkrete Verbesserungsvorschlaege

### Gate
- final_gate_status:

## Verwendete Quellen

## Neu entdeckte Erfahrungen

## Verbleibende Luecken

## Hinweise zur Interviewvorbereitung
```

## Strukturpflege-Vorschlag

Nur nach expliziter Nutzerfreigabe schreiben.

```markdown
## Vorgeschlagene Pflege

### stationen/
- Zielpfad:
- Aenderung:
- Evidenz:

### wissen/karriere/_uebersicht.md
- Aenderung:

### wissen/karriere/kompetenzen.md
- Aenderung:

### wissen/arbeitsstand.md oder TASKS.md
- Offener Punkt:
```
