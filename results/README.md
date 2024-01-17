# Results
Dieses Verzeichnis enthält die Ergebnisse des Experiments, d.h. die Antworten des Sprachmodells und die Ergebnisse der Evaluation.

## annotated_dataset.csv
Dieses Dokument enthält die annotierten Daten. Die Daten sind wie folgt aufgebaut:

- id: Die ID des Claims aus dem FEVER Datenset

- verifiable: Ob der Claim verifizierbar ist. Übernommen aus FEVER.

- label: Gold Label aus FEVER

- claim: Der Claim aus FEVER

- evidence: Evidence-Annotation aus FEVER. Liste von vollständigen Evidence Alternativen: Listen von Tupeln aus Satzindex, Evidence-Artikel Slug und Annotations IDs.

- evidence_article: Evidence-Artikel Slug. Für Verifiable Claims übernommen aus FEVER, ansonsten manuell hinzugefügt.

- compressed_evidence: FEVER-Evidence ohne Annotations ID und Artikel Slug, d.h. nur Satzindizes. Möglich, da Datenset auf Claims mit nur einem einzigen Evidence Artikel beschränkt wurde.

- evidence_text: Text des Evidence-Artikels, entnommen aus dem FEVER Wikipedia-Dump.

- annotation: Unveränderte Antwort des Sprachmodells.

- gpt_label: Label, aus der Antwort des Sprachmodells extrahiert.

- gpt_evidence: Liste von Evidence Satzindizes, aus der Antwort des Sprachmodells extrahiert.

- evidence_correctness: Korrektheit der Evidence-Annotation. Mögliche Werte: 
  - _CORRECT_: Die Antwort des Sprachmodells stimmt einer der Annotations-Alternativen aus FEVER überein.
  - _SUPERSET_: Die Antwort des Sprachmodells ist eine Übermenge einer der Annotations-Alternativen aus FEVER.
  - _SUBSET_: Die Antwort des Sprachmodells ist eine Teilmenge einer der Annotations-Alternativen aus FEVER.
  - _OVERLAP_: Die Antwort des Sprachmodells hat eine Schnittmenge mit einer der Annotations-Alternativen aus FEVER.
  - _DISJOINT_: Die Antwort des Sprachmodells hat keine Schnittmenge mit einer der Annotations-Alternativen aus FEVER.
  - _NOTHING_: Das Sprachmodell hat keine Evidence-Annotation geliefert.

- label_correct: Ob das Label korrekt ist.

- evidence_correct_strict: Ob die evidence_correctness _CORRECT_ ist.

- evidence_correct_medium: Ob die evidence_correctness _CORRECT_ oder _SUPERSET_ ist.

- evidence_correct_relaxed: Ob die evidence_correctness _CORRECT_, _SUPERSET_, _SUBSET_ oder _OVERLAP_ ist.

## results.md
Dieses Dokument enthält die Ergebnisse der Evaluation.