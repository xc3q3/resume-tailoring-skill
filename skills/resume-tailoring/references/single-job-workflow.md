# Ein-Job-Arbeitsablauf

## Inhalt

- Ziel
- Phase 0: Intake und Karrierebasis
- Phase 1: Erfolgsprofil
- Phase 2: Struktur und Vorlage
- Phase 3: Zusammenbau
- Phase 4: 3-Ebenen-Review und Nachschaerfung
- Phase 5: Ausgabe
- Phase 6: Strukturpflege

## Ziel

Einen faktengetreuen, auf eine konkrete Rolle zugeschnittenen Markdown-Lebenslauf, eine separate Projektliste und einen Qualitaetsreport erzeugen.

## Phase 0: Intake und Karrierebasis

Erfasse:
- Jobbeschreibung als Text oder URL.
- Firma und Rolle, falls nicht eindeutig in der JD.
- Projektwurzel; Standard ist das aktuelle Arbeitsverzeichnis, wenn es `AGENTS.md`, `stationen/`, `wissen/` und `output/` enthaelt.
- Ausgabeordner; Standard `output/`.
- Repo-lokales Skill-`output/` nur als Vorlagen-Werkbank behandeln, nicht als Bewerbungsprojekt-Ausgabe.

Karrierebasis:
- `stationen/*.md` lesen, aber `stationen/_vorlage.md` nur als Stationsvorlage behandeln.
- `wissen/profil.md` als autoritative Quelle fuer Berufsprofil, USP und Selbstdarstellung priorisieren.
- `wissen/glossar.md` fuer Abkuerzungen, Firmenkuerzel und Projektnamen nutzen.
- `wissen/karriere/_uebersicht.md` fuer Timeline und `wissen/karriere/kompetenzen.md` fuer konsolidierte Kompetenzen lesen.
- `wissen/schema.md` und `wissen/arbeitsstand.md` lesen, wenn Strukturregeln oder aktueller Bearbeitungsstand relevant sind.
- `output/_vorlage_lebenslauf.md` aus der Bewerbungsprojektwurzel als Zielstruktur lesen, falls vorhanden; `output/_vorlage_whoz.md` nur bei ausdruecklichem WHOZ-Wunsch.
- Die repo-lokale Referenzvorlage `output/_vorlage_Lebenslauf_2026.md` und ihre schlanke Strukturhilfe `output/_vorlage_Lebenslauf_2026_mapping.md` verdraengen diese Standards nicht. Sie nur aktiv befuellen, wenn sie in die Bewerbungsprojektwurzel uebernommen oder dort explizit ausgewaehlt wurden.
- `quellen/` nicht veraendern. Nur bei expliziter Extraktions- oder Evidenzfrage lesen.
- Rollen, Arbeitgeber, Titel, Daten, Bullet Points, Kompetenzen, Ausbildung und Kontaktblock extrahieren.
- Quellen je Aussage als Pfad merken, damit der Report nachvollziehbar bleibt.
- Typische Laenge, Abschnittsfolge, Ton und Bullet-Stil erkennen.

Wenn die Karrierebasis sehr klein ist, transparent sagen, dass weniger Match-Varianten verfuegbar sind.

## Phase 1: Erfolgsprofil

Analysiere die JD und optional oeffentliche Kontextdaten:
- Must-have Anforderungen.
- Nice-to-have Anforderungen.
- Technische und domain-spezifische Keywords inklusive Muss-Keywords, optionalen Keywords und DE/EN-Synonymen.
- Implizite Signale wie Ownership, Tempo, Stakeholder, Regulierungsumfeld.
- Risiken oder Luecken im vorhandenen Profil.
- Rollen-Archetyp: IC, Lead, Manager, Research, Product, Program, Hybrid.

Praesentiere kurz:
- Top 5 Anforderungen.
- 3 bis 5 narrative Themes.
- auffaellige Risiken oder Gaps.
- Terminologie, die Lebenslauf und Projektliste verwenden sollten.

Hole Nutzerfeedback ein, wenn das Profil unsicher oder interpretationsbeduerftig ist.

## Phase 2: Struktur und Vorlage

Erzeuge eine Dokumentstruktur:
- Primaer `output/_vorlage_lebenslauf.md` aus der Bewerbungsprojektwurzel fuellen, wenn vorhanden.
- Die 2026-Referenzvorlage nur nach bewusster Uebernahme oder expliziter Auswahl in der Bewerbungsprojektwurzel fuellen.
- Wenn die Vorlage fehlt, konservative Markdown-Struktur verwenden und im Report nennen.
- Berufliches Profil mit 2 bis 4 Saetzen.
- Kernkompetenzen in 2 bis 4 Kategorien, passend zur JD.
- Berufserfahrung nach Relevanz und Chronologie.
- 2 bis 4 kurze Schluesselprojekt-Teaser an passenden Stellen im Lebenslauf.
- Separate Projektliste als eigenes Bewerbungsdokument.
- Ausbildung und optionale Abschnitte nur, wenn sie den Fit verbessern.

Projekt-Teaser:
- maximal ein kurzer Bullet oder eine knappe Zeile pro Projekt.
- sinngemaesser Verweis auf die Projektliste, z. B. `Projekt: {Name}, siehe Projektliste`.
- nur fuer Projekte, die in der Projektliste vollstaendig und belegbar ausgearbeitet werden.
- keine langen Projektbeschreibungen im Lebenslauf.

Projektliste:
- Schwerpunkt auf fachlicher Tiefe fuer technische, ingenieurnahe, IT-, Beratungs- und Projektrollen.
- Jedes Schluesselprojekt mit Kontext, Aufgabe/Rolle, Methode/Technologie und Ergebnis/Wirkung.
- Quellen je Projekt im Report dokumentieren.

Rollen-Konsolidierung:
- Gleiche Firma und aehnliche Aufgaben koennen zusammengefasst werden.
- Unterschiedliche Firmen nie zusammenfassen.
- Unterschiedliche Rollen bei derselben Firma getrennt halten, wenn Progression oder stark abweichende Verantwortung wichtig ist.

Titel-Reframing:
- Nur branchenuebliche oder klarere Titelvarianten vorschlagen.
- Senioritaet nicht aufblasen.
- Originaltitel im Report dokumentieren, wenn sichtbar umformuliert wird.

Vor dem Fuellen der Vorlage die wichtigsten Strukturentscheidungen bestaetigen lassen.

## Phase 3: Zusammenbau

Erzeuge Roh-Lebenslauf, Roh-Projektliste und Roh-Report. Noch nichts finalisieren.

Fuelle Vorlagen-Slots mit den besten belegbaren Erfahrungen:
- Pro Slot Top-Kandidaten aus Karrierebasis und Discovery betrachten.
- Scoring aus `matching.md` verwenden.
- Wiederholungen vermeiden.
- Jede starke Umformulierung mit Original und Begruendung im Report festhalten.
- Projekt-Teaser nur aufnehmen, wenn das Projekt in der Roh-Projektliste vollstaendig belegt ist.

Bei Gaps:
- Beste verfuegbare Erfahrung mit Score nennen.
- Discovery anbieten, falls noch nicht erfolgt.
- Slot weglassen, Report-/Interview-Prep-Hinweis oder schwaches Match nur nach Nutzerentscheidung verwenden.

## Phase 4: 3-Ebenen-Review und Nachschaerfung

Fuehre immer `quality-review.md` aus, bevor Dateien als final gelten:
- ATS-Ebene: Keywords, Synonyme, Standardueberschriften, Parsing-Tauglichkeit und kein Keyword-Stuffing.
- HR-Ebene: 20- bis 30-Sekunden-Scan, klare Zielrichtung, schlanker CV, kurze Teaser.
- Fachbereichs-Ebene: Projektliste als Substanztraeger mit Kontext, Aufgabe, Methode/Technologie und Ergebnis/Wirkung.

Nachschaerfen:
- belegbare fehlende Keywords natuerlich einbauen,
- ueberlange CV-Details in die Projektliste verschieben,
- Projektliste fachlich vertiefen, wenn Quellen oder Discovery das tragen,
- unbelegte Aussagen entfernen oder abschwaechen,
- verbleibende Gaps, Risiken und Verbesserungsvorschlaege im Qualitaetsreport dokumentieren.

Gate:
- Keine finale Ausgabe, wenn unbelegte Behauptungen, Projekt-Teaser ohne Projektlistennachweis oder irrefuehrendes Keyword-Stuffing enthalten sind.
- Bei fehlender Evidenz nicht erfinden; `pass_with_risks` oder `needs_user_input` im Report setzen.

## Phase 5: Ausgabe

Erzeuge:
- `output/{Name}_{Stelle}_{Jahr}.md`
- `output/{Name}_{Stelle}_{Jahr}_Projektliste.md`
- `output/{Name}_{Stelle}_{Jahr}_Report.md`
- optional bei ausdruecklichem Nutzerwunsch und vorhandener Vorlage einen WHOZ-Export anhand `output/_vorlage_whoz.md`
- optional nach Nutzerwunsch und lokaler Tool-Verfuegbarkeit `output/{Name}_{Stelle}_{Jahr}.docx`
- optional nach Nutzerwunsch und lokaler Tool-Verfuegbarkeit `output/{Name}_{Stelle}_{Jahr}.pdf`

Dateinamen aus normalisierten Segmenten bilden, Anzeigenamen im Dokument aber unveraendert lassen. Zielpfade nie ueberschreiben; bei Kollision `-2`, `-3` usw. anhaengen. Echte Bewerbungsoutputs immer in der validierten Bewerbungsprojektwurzel erzeugen, nie im repo-lokalen Vorlagen-`output/` des Skills.

Lebenslauf-Struktur:
```markdown
# {Name}

{Kontakt}

## Berufliches Profil

{Profiltext}

## Kernkompetenzen

**{Kategorie}:** {Kompetenz-Liste}

## Berufserfahrung

### {Titel}
**{Firma} | {Ort} | {Zeitraum}**

- {Erfolgs-Bullet}
- {Erfolgs-Bullet}

## Ausgewaehlte Projekte

- Projekt: {Projektname}, siehe Projektliste
- Projekt: {Projektname}, siehe Projektliste

## Ausbildung

{Ausbildung}
```

Projektlisten-Struktur:
```markdown
# Projektliste: {Name} fuer {Stelle}

## Projekt: {Projektname}

**Kontext:** {Umfeld, Ziel, Stakeholder}
**Rolle/Aufgabe:** {konkreter Beitrag}
**Methode/Technologie:** {belegte Methoden, Tools, Normen, Systeme}
**Ergebnis/Wirkung:** {messbar oder beobachtbar; keine erfundenen Zahlen}
**Relevanz fuer die Zielrolle:** {warum dieses Projekt zaehlt}
```

Report-Struktur:
```markdown
# Lebenslauf-Erzeugungsreport

## Zielrolle
## Erfolgsprofil
## Abdeckungsuebersicht
## Inhaltszuordnung
## Projekt-Teaser und Projektliste
## Reframings
## Qualitaetsreport
### ATS-Abdeckung
### HR-Lesbarkeit
### Fachliche Substanz
### Risiken
### Konkrete Verbesserungsvorschlaege
### Gate
## Verwendete Quellen
## Neu entdeckte Erfahrungen
## Verbleibende Luecken
## Hinweise zur Interviewvorbereitung
```

Optionale Exporte:
- Erst Markdown-Lebenslauf finalisieren.
- Lokale Exportwege pruefen, etwa vorhandene Repo-Skripte, `pandoc`, `textutil` oder `libreoffice`.
- Export nur erzeugen, wenn das Tool verfuegbar ist und das Ergebnis sinnvoll verifiziert werden kann.
- Wenn Export scheitert oder kein Tool vorhanden ist, Markdown und Report behalten und den fehlenden Export transparent melden.

## Phase 6: Strukturpflege

Nach Review fragen:
- Neue echte Erfahrungen oder Korrekturen in `stationen/` oder `wissen/karriere/*` uebernehmen.
- `wissen/arbeitsstand.md` oder `TASKS.md` mit offenen Punkten aktualisieren.
- Ausgabe behalten, aber Wissensstruktur nicht aendern.
- Revisionen durchfuehren.

Nur nach expliziter Zustimmung Dateien ausserhalb von `output/` schreiben. `quellen/` bleibt immer unveraendert.
