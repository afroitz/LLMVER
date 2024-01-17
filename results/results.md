# Ergebnisse des Experiments

## Datenset
Es wurden insgesamt 966 Claims annotiert, davon 545 mit dem Gold Label **SUPPORTS**, 191 mit **REFUTES** und 239 mit **NOT ENOUGH INFORMATION**.

## Evaluation: Labels
### Confusion Matrix (Labels) (Zeilen: Gold, Spalten: Predicted)
|                 | SUPPORTS | REFUTES | NOT ENOUGH INFO | Summe |
| --------------- | -------- | ------- | --------------- | ----- |
| SUPPORTS        | 466      | 29      | 50              | 545   |
| REFUTES         | 65       | 83      | 43              | 191   |
| NOT ENOUGH INFO | 83       | 47      | 100             | 230   |
| Summe           | 614      | 159     | 193             | 966   | 

### Classification Report
|                  | Precision | Recall | F1-Score | Support |
| ---------------- | --------- | ------ | -------- | ------- |
| SUPPORTS         | 0.76      | 0.86   | 0.80     | 545     |
| REFUTES          | 0.52      | 0.43   | 0.47     | 191     |
| NOT ENOUGH INFO  | 0.52      | 0.43   | 0.47     | 230     |
| Accuracy         |           |        | 0.67     | 966     |
| Macro Average    | 0.60      | 0.57   | 0.58     | 966     |
| Weighted Average | 0.65      | 0.67   | 0.66     | 966     |

## Evaluation: Evidence
### Definitionen
Das FEVER-Datenset enthält oft mehrere gleichwertige, vollständige Evidence-Alternativen pro Claim. Wie auch die vom Sprachmodell gelieferte Evidence sind diese jeweils eine Liste von Satz-Indizes. Daher sind die folgenden Fälle definiert:

- **CORRECT**: GPT-Evidence ist identisch mit mindestens einer Evidence-Alternative
- **SUPERSET**: GPT-Evidence ist eine Übermenge von mindestens einer Evidence-Alternative
- **SUBSET**: GPT-Evidence ist eine Teilmenge von mindestens einer Evidence-Alternative
- **OVERLAP**: Es gibt eine Schnittmenge zwischen einer Evidence-Alternative und GPT-Evidence
- **DISJOINT**: Es gibt keine Schnittmenge
- **NOTHING**: GPT-Evidence ist leer

Darauf aufbauend sind die folgenden Stufen von Evidence-Korrektheit definiert:

- **Strict**: Evidence ist **CORRECT**
- **Medium**: Evidence ist **CORRECT** oder **SUPERSET**
- **Relaxed**: Evidence ist **CORRECT**, **SUPERSET**, **SUBSET** oder **OVERLAP**

Unter den annotierten Claims gibt es 643 Claims, für welche sowohl Gold Label als auch Predicted Label entweder **SUPPORTS** oder **REFUTES** sind und für welche somit die Evidence Korrektheit ausgewertet werden kann. Die folgende Tabelle zeigt diese Auswertung:

|                    | True **SUPPORTS** | True **REFUTES** | False **SUPPORTS** | False **REFUTES** | Gemeinsam |
| ------------------ | ----------------- | ---------------- | ------------------ | ----------------- | --------- |
| CORRECT            | 198               | 5                | 27                 | 0                 | 230       |
| SUPERSET           | 75                | 10               | 6                  | 3                 | 94        |
| SUBSET             | 4                 | 0                | 0                  | 0                 | 4         |
| OVERLAP            | 1                 | 0                | 0                  | 0                 | 1         |
| DISJOUNT           | 188               | 49               | 32                 | 24                | 293       |
| NOTHING            | 0                 | 19               | 0                  | 2                 | 21        |
| Summe              | 466               | 83               | 65                 | 29                | 643       |
| Accuracy (Strict)  | .42               | .06              | .42                | .00               | .36       |
| Accuracy (Medium)  | .59               | .18              | .51                | .10               | .50       |
| Accuracy (Relaxed) | .60               | .18              | .51                | .10               | .51       | 

## Evaluation: Gesamt

Aus den vorherigen Daten lässt sich auch die Gesamt-Evaluation ableiten: Hierfür gibt es die Kategorien _Correct_, _Wrong_, _Only label correct_ und _Only evidence correct_. **NOT ENOUGH INFORMATION**-Claims fallen dabei immer entweder in die Kategorie _Wrong_ oder _Correct_. Die folgende Tabelle zeigt die Gesamt-Evaluation:

|                       | Strict | Medium | Relaxed |
| --------------------- | ------ | ------ | ------- |
| Correct               | 303    | 388    | 393     |
| Only Label Correct    | 346    | 261    | 256     |
| Only Evidence Correct | 27     | 36     | 36      |
| Wrong                 | 290    | 281    | 281     |