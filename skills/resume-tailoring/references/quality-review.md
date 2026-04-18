# 3-Ebenen-Qualitaetsreview

## Ziel

Vor der finalen Ausgabe Lebenslauf und Projektliste gemeinsam pruefen und verbessern. Das Review ist verpflichtend, nicht optional.

Die drei Ebenen:
- ATS: maschinenlesbar, keyword-passend, kein Stuffing.
- HR: in 20 bis 30 Sekunden verstaendlich.
- Fachbereich: fachlich belegbar und projekthaft substanziell.

Finale Ausgabe ist erst erlaubt, wenn belegbare Schwaechen nachgeschaerft sind und verbleibende Luecken transparent im Report stehen.

## Eingangsdaten

Nutze:
- Jobbeschreibung, Erfolgsprofil und Keyword-Extraktion.
- Roh-Lebenslauf.
- Roh-Projektliste.
- Matching-/Reframing-Notizen.
- Quellen aus `stationen/`, `wissen/` und Discovery.

Nicht nutzen:
- unbelegte Annahmen,
- erfundene Metriken,
- Tools, Domains oder Verantwortungen ohne Quelle.

## Review-Pipeline

1. Keyword- und Anforderungsabdeckung gegen Lebenslauf und Projektliste pruefen.
2. Lebenslauf auf ATS-Struktur, Schlankheit und 30-Sekunden-Scan pruefen.
3. Projektliste auf fachliche Tiefe und Nachweisqualitaet pruefen.
4. Schwaechen in `improvement_actions` sammeln.
5. Alles Belegbare direkt nachschaerfen.
6. Unbelegbare Punkte als Gap, Risiko oder Discovery-Hinweis dokumentieren.
7. Finale Scores und `final_gate_status` im Report festhalten.

## ATS-Ebene

Ziel: maximale Passung zu Applicant Tracking Systems, ohne Keyword-Stuffing.

Pruefe:
- relevante JD-Keywords sind als Muss, optional oder Synonym erfasst,
- DE/EN-Synonyme sind erkannt, z. B. `Anforderungsmanagement` / `requirements engineering`,
- Muss-Keywords kommen im Lebenslauf vor, wenn sie belegbar sind,
- optionale Keywords stehen im Lebenslauf oder in der Projektliste, wenn sie belegbar und relevant sind,
- Projektliste vertieft Keywords, ohne den Lebenslauf zu ueberladen,
- Standardueberschriften wie `Berufliches Profil`, `Kernkompetenzen`, `Berufserfahrung`, `Ausbildung` bleiben erhalten,
- Markdown bleibt einfach: keine Tabellen als Kerninhalt, keine exotischen Layouts, keine bildbasierten Informationen,
- Begriffe sind sinnvoll in Profil, Kompetenzen, Erfahrung oder Projekt-Teaser eingebettet.

Keyword-Status:
- `covered`: Begriff steht belegbar im Lebenslauf.
- `covered_by_synonym`: Synonym steht belegbar im Lebenslauf.
- `project_only`: Begriff ist belegbar in der Projektliste vertieft, aber nicht CV-kritisch.
- `missing_but_evidence_available`: Evidenz existiert, Begriff sollte natuerlich ergaenzt werden.
- `missing_no_evidence`: keine belastbare Evidenz; nicht ergaenzen.
- `unsupported_claim`: Begriff steht im Entwurf, ist aber nicht belegt; entfernen oder abschwaechen.

ATS-Score 0-100:
- 40 Punkte Muss-Keyword-Abdeckung.
- 20 Punkte optionale Keyword-Abdeckung.
- 20 Punkte sinnvolle Einbettung ohne Stuffing.
- 20 Punkte Struktur- und Parsing-Tauglichkeit.

## HR-Ebene

Ziel: Recruiter versteht in 20 bis 30 Sekunden Rolle, Senioritaet, Zielrichtung und Top-Staerken.

Pruefe:
- Oben ist sofort klar: Zielrolle, beruflicher Schwerpunkt, Senioritaet und wichtigste Staerken.
- Profiltext hat 2 bis 4 Saetze und keine generische Marketing-Sprache.
- Kernkompetenzen sind in 2 bis 4 Kategorien schnell erfassbar.
- Bulletpoints sind kurz, aktiv und relevant.
- Keine Textwaende; lange Projektlogik steht in der Projektliste.
- Interne Begriffe, Firmenkuerzel und Projektcodes sind erklaert oder entfernt.
- 2 bis 4 Schluesselprojekt-Teaser erzeugen Neugier, ohne den CV zu verlaengern.
- Jeder Teaser ist maximal ein kurzer Bullet oder eine knappe Zeile und verweist sinngemaess auf die Projektliste.

HR-Score 0-100:
- 30 Punkte 30-Sekunden-Klarheit.
- 25 Punkte obere Dokumenthaelfte zeigt Zielrichtung und Top-Staerken.
- 20 Punkte kurze, praegnante Bulletpoints.
- 15 Punkte logischer Aufbau und visuelle Scanbarkeit.
- 10 Punkte erklaerte Begriffe und keine Detailueberladung.

## Fachbereichs-Ebene

Ziel: technische oder operative Entscheider erkennen echte Substanz.

Pruefe:
- Jede wichtige JD-Anforderung hat eine belegte Erfahrung, ein Projekt, ein Ergebnis oder bleibt als Gap markiert.
- Projektliste ist der zentrale Substanztraeger.
- Jedes wichtige Projekt enthaelt Kontext, Aufgabe, Methode/Technologie und Ergebnis/Wirkung.
- Projekt-Teaser im CV haben einen vollstaendigen Nachweis in der Projektliste.
- Buzzwords ohne Beleg werden entfernt, abgeschwaecht oder als Gap dokumentiert.
- Schwache oder angrenzende Erfahrung wird transparent geframed, nicht ueberverkauft.
- Fachliche Tiefe passt zur Zielrolle, ohne irrelevante Nebendetails.

Projekt-Bullet-Mindestform:
```markdown
- Kontext: {Umfeld, Problem, Stakeholder oder Ziel}
- Aufgabe/Rolle: {konkreter Beitrag des Kandidaten}
- Methode/Technologie: {belegte Methoden, Tools, Normen oder Systeme}
- Ergebnis/Wirkung: {messbar, beobachtbar oder plausibel beschrieben; keine erfundenen Zahlen}
```

Substanz-Score 0-100:
- 35 Punkte belegte Abdeckung wichtiger Anforderungen.
- 25 Punkte Projektqualitaet nach Kontext, Aufgabe, Methode/Technologie, Ergebnis/Wirkung.
- 20 Punkte fachliche Tiefe und Relevanz fuer die Zielrolle.
- 10 Punkte transparente Behandlung schwacher Erfahrung.
- 10 Punkte Quellen- und Wahrheitsnachweis.

## Nachschaerfungsregeln

Erlaubt:
- belegte Keywords natuerlich in Profil, Kompetenzen, Erfahrung oder Projekt-Teaser integrieren,
- lange CV-Projekttexte in die Projektliste verschieben,
- Projektliste fachlich erweitern, wenn Quellen oder Discovery die Details tragen,
- unklare interne Begriffe mit Glossarwissen erklaeren,
- schwache Erfahrung vorsichtig als angrenzend oder uebertragbar formulieren.

Nicht erlaubt:
- neue Tools, Metriken, Rollen, Domains oder Senioritaet erfinden,
- Lerninteresse als Berufserfahrung ausgeben,
- Projekt-Teaser ohne Projektlistennachweis verwenden,
- Keyword-Stuffing oder reine Buzzword-Listen erzeugen,
- Fachluecken durch kreative Formulierungen verstecken.

## Gate-Status

Setze im Report einen Status:
- `pass`: alle drei Ebenen sind solide; nur kleine Hinweise bleiben.
- `pass_with_risks`: Ausgabe ist nutzbar, aber es bleiben ehrliche Gaps oder Risiken.
- `needs_user_input`: finale Ausgabe waere ohne weitere belegbare Nutzerangaben zu schwach oder riskant.

`needs_user_input` nutzen, wenn ein Muss-Kriterium weder belegt noch sauber als Gap tragbar ist oder wenn ein CV-Teaser keine belastbare Projektbasis hat.

## Report-Format

```markdown
## Qualitaetsreport

### ATS-Abdeckung
- Score:
- Muss-Keywords:
- Optionale Keywords:
- Synonyme:
- Luecken:
- Nachschaerfungen:

### HR-Lesbarkeit
- Score:
- 30-Sekunden-Scan:
- Staerken oben sichtbar:
- Hinweise:
- Nachschaerfungen:

### Fachliche Substanz
- Score:
- Belegte Anforderungen:
- Projektlisten-Qualitaet:
- Fehlende Nachweise:
- Nachschaerfungen:

### Risiken
- {Risiko}: {Auswirkung und ehrlicher Umgang}

### Konkrete Verbesserungsvorschlaege
- {naechste Aktion, falls Nutzer weitere Evidenz liefern kann}

### Gate
- final_gate_status:
```
