# Schemas

## Inhalt

- JobState
- BatchState
- DiscoveredExperience
- GapItem
- PathSegment
- Resume Report

## JobState

```json
{
  "job_id": "job-1",
  "company": "Company",
  "role": "Role",
  "company_slug": "company",
  "role_slug": "role",
  "jd_text": "Job description",
  "jd_url": null,
  "priority": "medium",
  "notes": "",
  "status": "pending",
  "current_phase": null,
  "coverage": null,
  "files_generated": false,
  "output_paths": [],
  "last_updated": "ISO-8601 timestamp",
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
  "created": "ISO-8601 timestamp",
  "last_updated": "ISO-8601 timestamp",
  "output_dir": "resumes/batches/batch-YYYY-MM-DD-slug",
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
  "evidence_source": "",
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

## PathSegment

Pfadsegmente aus Nutzerdaten nicht direkt verwenden.

```json
{
  "display_value": "Company / Role: Example",
  "path_value": "Company-Role-Example",
  "max_length": 64,
  "collision_suffix": "-2"
}
```

Regeln:
- `display_value` bleibt im Resume und Report erhalten.
- `path_value` ersetzt Leerraeume und verbotene Dateisystemzeichen durch `-`.
- Bei Kollisionen Suffix vor Dateiendung oder am Ordnernamen erhoehen.

## Resume Report

```markdown
# Resume Generation Report

## Target Role
- Company:
- Role:
- Job source:
- Generated:

## Success Profile
- Core requirements:
- Narrative themes:
- Risks:

## Coverage Summary
- Overall coverage:
- Direct:
- Transferable:
- Adjacent:
- Weak:
- Gaps:

## Content Mapping

## Reframings

## Source Resumes Used

## Newly Discovered Experiences

## Remaining Gaps

## Interview Prep Notes
```
