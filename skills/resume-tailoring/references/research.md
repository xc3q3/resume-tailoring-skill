# Research Guidance

## JD Parsing

Extrahiere strukturiert:
- Explizite Must-have Anforderungen.
- Nice-to-have Anforderungen.
- Technische Keywords und Domainbegriffe.
- Implizite Praeferenzen, etwa Ownership, Ambiguity, Tempo, Stakeholder, Regulierung.
- Red Flags, etwa fehlende Domain, Senioritaetsmismatch oder Tool-Luecken.
- Rollen-Archetyp.

Output:
```markdown
## JD Analysis

### Must-Haves
### Nice-to-Haves
### Keywords
### Implicit Signals
### Risks
### Role Archetype
```

## Firmenrecherche

Nutze Webrecherche nur, wenn sie verfuegbar und noetig ist. Geeignete Suchrichtungen:
- `{company} mission values culture`
- `{company} engineering blog`
- `{company} recent news product launch`
- `{company} careers {role family}`

Nicht uebertreiben: Fuer ein Resume reicht ein pragmatisches Success Profile. Keine langen Firmenportraits.

Provenienzpflicht:
- Jede externe Aussage mit Quelle, URL oder Seitentitel und Abrufdatum der Session markieren.
- Aussagen aus der Jobbeschreibung als `Source: JD` markieren.
- Aussagen aus Nutzerantworten als `Source: User` markieren.
- Wenn keine belastbare Quelle vorhanden ist, die Aussage nicht als Fakt verwenden; entweder als Unsicherheit markieren oder JD-only arbeiten.

## Rollen-Benchmarking

Wenn oeffentliche Rollenprofile oder Teamseiten verfuegbar sind:
- gemeinsame Skills und Formulierungen erkennen,
- typische Backgrounds ableiten,
- relevante Terminologie aufnehmen.

Wenn nichts Solides verfuegbar ist:
- nicht halluzinieren,
- JD-only arbeiten,
- den Nutzer optional nach Insider-Kontext fragen.

## Success Profile

Erzeuge:
```markdown
## Success Profile: {Role} at {Company}

### Core Requirements
- {Requirement}: {Evidence, Source}

### Valued Capabilities
- {Capability}: {Why it matters, Source}

### Narrative Themes
- {Theme}: {How the resume should show it, Source}

### Terminology Map
- User/source wording -> target wording

### Risks and Mitigations
- {Risk}: {Truthful mitigation}

### Sources
- {Source label}: {JD, URL/title, or User context}; accessed {date if external}
```

## Qualitaetsregeln

- Jede Aussage ueber Firma oder Rolle muss aus JD, Recherche oder Nutzerkontext stammen.
- Unsicherheit markieren.
- Keine Kultur- oder Teamdetails erfinden.
- Firmenrecherche darf die JD ergaenzen, aber nicht gegen sie arbeiten.
