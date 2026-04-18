# Matching und Reframing

## Ziel

Vorhandene Erfahrungen transparent auf Jobanforderungen abbilden. Das Matching soll erklaeren, warum ein Bullet passt oder warum eine Luecke bleibt.

## Scoring

Alle Teilwerte auf einer 0-100-Skala bewerten. Nur belegte Informationen aus `stationen/`, `wissen/`, Discovery, JD oder Nutzerkontext zaehlen; fehlende Evidenz ist `0`.

Autoritative Quellen:
- `wissen/profil.md` fuer Berufsprofil, USP und Selbstdarstellung.
- `wissen/glossar.md` fuer Abkuerzungen, Firmenkuerzel und Projektnamen.
- `wissen/karriere/_uebersicht.md` fuer Timeline und Stationenfolge.
- `wissen/karriere/kompetenzen.md` fuer konsolidierte Kompetenzen.
- `stationen/*.md` fuer konkrete Arbeitgeber-, Rollen-, Projekt- und Erfahrungsbelege.

Teilwert-Rubrik:
- `100`: gleiche Anforderung, gleicher Kontext oder gleichwertige Wirkung.
- `75`: starke Uebereinstimmung mit kleinem Domain-, Tool- oder Kontextwechsel.
- `50`: teilweise Uebereinstimmung; relevante Faehigkeit ist erkennbar, aber nicht deckungsgleich.
- `25`: schwache Andeutung; nur als Hinweis, nicht als tragender Lebenslauf-Bullet.
- `0`: keine belastbare Evidenz.

Gesamtscore:
```text
Overall = Direct * 0.4 + Transferable * 0.3 + Adjacent * 0.2 + Impact * 0.1
```

Kriterien:
- **Direct Match (40%)**: gleiche Skills, Domain, Technologie, Outcomes oder Komplexitaet.
- **Transferable (30%)**: gleiche Faehigkeit in anderem Kontext.
- **Adjacent (20%)**: verwandte Tools, Methoden, Problemraeume oder Nebenverantwortung.
- **Impact (10%)**: Wirkung passt zur Zielrolle, etwa Scale, Kosten, Umsatz, Qualitaet, Teamwirkung.

Score-Entscheidungen im Mapping kurz begruenden. Bei Unsicherheit niedriger bewerten und Discovery oder Gap-Behandlung anbieten.

Confidence-Bands:
- `90-100`: DIRECT.
- `75-89`: TRANSFERABLE.
- `60-74`: ADJACENT.
- `45-59`: WEAK.
- `<45`: GAP.

## Mapping-Ausgabe

Pro Vorlagen-Slot:
```markdown
### Slot: {Anforderung oder Bullet-Ziel}

**Empfehlung:** {Quell-Bullet oder Discovery}
**Confidence:** {score} ({band})
**Quelle:** {stationen/... oder wissen/... oder Discovery-ID}

Warum es passt:
- Direct:
- Transferable:
- Adjacent:
- Impact:

Luecken:
- {fehlendes Element, falls vorhanden}
```

## Projektliste und CV-Teaser

Matching liefert auch die Evidenzbasis fuer Projektliste und ATS-Keywords.

Projektliste:
- Nur Projekte aufnehmen, die aus `stationen/`, `wissen/`, Discovery oder Nutzerkontext belegbar sind.
- Pro wichtigem Projekt Kontext, Aufgabe/Rolle, Methode/Technologie und Ergebnis/Wirkung erfassen.
- Wenn Ergebnis oder Wirkung nicht belegt ist, beobachtbare Wirkung vorsichtig formulieren oder als fehlenden Nachweis markieren.
- Projektliste darf fachlich tiefer sein als der Lebenslauf, aber keine neuen unbelegten Fakten einfuehren.

CV-Teaser:
- 2 bis 4 Schluesselprojekte aus der Projektliste auswaehlen.
- Teaser muessen zur Zielrolle passen und duerfen ATS-relevante Begriffe nur natuerlich verwenden.
- Kein Teaser ohne vollstaendige Projektlisten-Ausarbeitung.
- Teaser sind keine Ersatzbelege; der Beleg liegt in Projektliste und Report.

ATS-Keyword-Behandlung:
- `DIRECT` und `TRANSFERABLE` koennen im CV genutzt werden, wenn die Formulierung wahr bleibt.
- `ADJACENT` eher in Projektliste oder Report erklaeren, nicht als hartes Muss-Keyword im CV ausgeben.
- `WEAK` und `GAP` nicht durch Keyword-Stuffing verstecken.

## Reframing-Regeln

Erlaubt:
- Terminologie an Zielrolle angleichen.
- Fokus verschieben, wenn dieselben Fakten betont werden.
- technische Details ein- oder ausblenden.
- Wirkung und Kontext klarer machen.

Nicht erlaubt:
- neue Tools, Domains, Metriken oder Senioritaet behaupten.
- Verantwortung von Team auf Person verschieben, wenn nicht belegbar.
- Arbeitgeber, Daten oder Titel irrefuehrend veraendern.
- aus Lernen/Interesse produktive Berufserfahrung machen.

Reframing immer dokumentieren:
```markdown
Original: "{source}"
Reframed: "{new}"
Reason: "{why this wording is truthful and useful}"
```

## Gap Handling

Wenn Score unter 60 liegt:
- Bestes Match nennen.
- konkrete fehlende Elemente benennen.
- Discovery anbieten, wenn passend.
- Optionen geben:
  - Slot weglassen.
  - Bestes schwaches Match mit vorsichtiger Formulierung nutzen.
  - Gap im Report oder in der Interviewvorbereitung adressieren.
  - Nutzer nach belegbarer Erfahrung fragen.

## Wiederholungen vermeiden

Wenn ein Bullet mehrere Anforderungen abdeckt:
- fuer den wichtigsten Slot verwenden,
- bei weiteren Slots als sekundare Abdeckung im Report nennen,
- nicht denselben Erfolg mehrfach im Lebenslauf wiederholen.
