# LLMVER
## Experiment zur Annotation mit LLMs in Claim Verification Aufgaben

### Aufgabenstellung
Das Ziel dieses Projekts ist es, die Leistungsfähigkeit von LLMs (konkret, `gpt-3.5-turbo`) für die Annotation in Claim Verification Aufgaben zu evaluieren.
Die konkrete Aufgabe entspricht dem zweiten Annotationsschritt der Aufgabendefinition nach Thorne et al. (2018) für die Erstellung des FEVER Datensets. Hierbei soll einer atomaren Behauptung in Verbindung mit einem Evidence-Text (die Einleitung eines potentiell relevanten Wikipedia-Artikels) eines der Labels *SUPPORTS*, *REFUTES* oder *NOT ENOUGH INFORMATION* zugewiesen werden. Außerdem soll identifiziert werden, welche Sätze aus dem Text für diese Entscheidung relevant waren indem die Indizes dieser Sätze im Text angegeben werden.

### Vorgehensweise
Die Daten werden aus dem FEVER Datenset geladen. Die Einleitungen der jeweiligen Evidence-Artikel werden aus dem FEVER-Wikipedia-Dump hinzugefügt.
Das Label und die angegebenen Satz-Indizes aus Fever können als Label für die Aufgabe verwendet werden.

Für jeden Claim und jeden zugehörigen Evidence-Text wird ein Prompt erstellt, der den Claim, die nummerierten Sätze und eine Zusammenfassung der Annotationsrichtlinien enthält.
Das Modell wird aufgefordert, in einer fest definierten Struktur mit dem Label und den Indizes eventueller Evidence-Sätze zu antworten.
Die Antworten werden gespeichert und anschließend evaluiert. Hierbei wird die Übereinstimmung der Antworten mit den Labels und Indizes aus dem FEVER Datenset gemessen.

### Projektstruktur
- `notebooks`: Hier befindet sich der Code für das Experiment, verteilt auf die folgenden Jupyter Notebooks:
    - `process-dataset`: Dieses Notebook liest das FEVER Datenset ein und verarbeitet es. Dabei werden Claims mit mehr als einem zugeordneten Evidence-Artikel herausgefiltert und Struktur der Evidence Annotationen wird vereinfacht.
    - `build-wiki-index`: Dieses Notebook erzeugt aus dem von FEVER erhältlichen Wikipedia-Dump einen Index, der die Ermittlung der zugehörigen Evidence-Texte im nächsten Schritt vereinfacht.
    - `add-evidence-text`: Dieses Notebook extrahiert die ersten 1000 Zeilen des vorverarbeiteten FEVER Datensets, fügt erst die manuell ermittelten Evidence-Artikelnamen für NOT ENOUGH INFO Claims und dann die zugehörigen Evidence-Texte hinzu.
    - `annotate`: Dieses Notebook enthält die Logik für Anfragen an die API von OpenAI. Es liest das verarbeitete Datenset ein, Satz-tokenisiert die Evidence-Texte und erstellt die Prompts. Anschließend werden die Anfragen an die API gestellt und die Antworten gespeichert.
    - `evaluate`: Dieses Notebook liest die Antworten aus dem vorherigen Schritt ein, evaluiert sie unter verschiedenen Gesichtspunkten und visualisiert die Ergebnisse.
- `data`: Hier befinden sich alle Daten – sowohl die ursprünglichen Daten von FEVER als auch alle Zwischenstände. Die Daten sind nicht in GitHub enthalten. Die Daten von FEVER sind hier verfügbar: https://fever.ai/download/fever/train.jsonl bzw. https://fever.ai/download/fever/wiki-pages.zip
- `prompts`: Hier befinden sich die Prompts zur Ansprache an die OpenAI API.
- `results`: Hier befinden sich die Ergebnisse, d.h. Antworten des Sprachmodells und Ergebnisse der Evaluation.

### Literatur
James Thorne, Andreas Vlachos, Christos Christodoulopoulos, and Arpit Mittal. 2018. FEVER: a Large-scale Dataset for Fact Extraction and VERification. In _Proceedings of the 2018 Conference of the North American Chapter of the Association for Computational Linguistics: Human Language Technologies, Volume 1 (Long Papers)_, pages 809–819, New Orleans, Louisiana. Association for Computational Linguistics.