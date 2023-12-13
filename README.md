# LLMVER
## Experiment zur Annotation mit LLMs in Claim Verification Aufgaben

### Aufgabenstellung
Das Ziel dieses Projekts ist es, die Leistungsfähigkeit von LLMs für die Annotation in Claim Verification Aufgaben zu evaluieren.
Die konkrete Aufgabe entspricht dem zweiten Annotationsschritt der Aufgabendefinition nach Thorne et al. (2018) für die Erstellung des FEVER Datensets. Hierbei soll einer atomaren Behauptung in Verbindung mit einem Evidence-Text (die Einleitung eines potentiell relevanten Wikipedia-Artikels) eines der Labels *SUPPORTS*, *REFUTES* oder *NOT ENOUGH INFORMATION* zugewiesen werden. Außerdem soll identifiziert werden, welche Sätze aus dem Text für diese Entscheidung relevant waren indem die Indizes dieser Sätze im Text angegeben werden.

### Vorgehensweise
Die Daten werden aus dem FEVER Datenset geladen. Die Einleitungen der jeweiligen Evidence-Artikel werden von Wikipedia geladen und nach Sätzen tokenisiert.
Das Label und die angegebenen Satz-Indizes aus Fever können als Label für die Aufgabe verwendet werden. Es ist allerdings zu beachten, dass nicht auszuschließen ist,
dass Wikipedia Artikel seit der Erstellung des FEVER Datensets verändert wurden oder die Tokenisierung nicht identisch funktioniert. 
In diesem Fall kann es sein, dass die angegebenen Satz-Indizes nicht mit den hier ermittelten übereinstimmen.

Für jeden Claim und jeden zugehörigen Evidence-Text wird ein Prompt erstellt, der den Claim, die nummerierten Sätze und eine Zusammenfassung der Annotationsrichtlinien enthält.
Das Modell wird aufgefordert, in einer fest definierten Struktur mit dem Label und den Indizes eventueller Evidence-Sätze zu antworten.
Die Antworten werden gespeichert und anschließend evaluiert. Hierbei wird die Übereinstimmung der Antworten mit den Labels und Indizes aus dem FEVER Datenset gemessen.

### Projektstruktur
- `notebooks`: Hier befindet sich der Code für das Experiment, verteilt auf die folgenden Jupyter Notebooks:
    - `process-dataset`: Dieses Notebook kann Daten aus dem FEVER-Datenset (Thorne et al. 2018) einlesen und weiterverarbeiten. Das bedeutet, dass die für den jeweiligen Claim als Evidence verwendeten Wikipedia Artikel von Wikipedia geladen und nach Sätzen tokenisiert werden.
    - `annotate`: Dieses Notebook enthält die Logik für Anfragen an die API von OpenAI. Es liest das verarbeitete Datenset ein, stellt Anfragen, verarbeitet die Antworten und exportiert die Ergebnisse.
    - `evaluate`
- `data`: Hier befinden sich alle Daten – sowohl die ursprünglichen Daten von FEVER als auch alle Zwischenstände. Die Daten sind nicht in GitHub enthalten. Die Daten von FEVER sind hier verfügbar: https://fever.ai/download/fever/train.jsonl
- `prompts`: Hier befinden sich die Prompts zur Ansprache an die OpenAI API.
- `results`: Hier befinden sich die Ergebnisse, d.h. Antworten der Sprachmodelle sowie Ergebnisse der Evaluation.

### Literatur
James Thorne, Andreas Vlachos, Christos Christodoulopoulos, and Arpit Mittal. 2018. FEVER: a Large-scale Dataset for Fact Extraction and VERification. In _Proceedings of the 2018 Conference of the North American Chapter of the Association for Computational Linguistics: Human Language Technologies, Volume 1 (Long Papers)_, pages 809–819, New Orleans, Louisiana. Association for Computational Linguistics.