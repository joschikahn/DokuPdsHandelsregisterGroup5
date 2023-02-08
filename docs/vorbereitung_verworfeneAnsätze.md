# Vorbereitung & verworfener Code:

## Vorbereitung

### Notebook: Reading TIF-Files by OCR
In diesem Notebook werden alle TIF-Dateien mit Hilfe von OCR ausgelesen und einem Dataframe df gespeichert. Dieses wurde exportiert um es in der App für die Funktion "Dateisuche in TIF-Dateien" zu nutzen.

### Notebook: Zero-Shot-Classification Branche WZ-2008
In diesem Notebook wird die Umsetzung der Branchenklassifikation inklusive der verschiedenen Vorbereitungsschritte beschreiben bzw. ausgeführt, wie in Abschnitt *App* genauer beschrieben. Die Klassifizierung aller Firmen findet hier statt und wird im Dataframe *branchen_bestimmung_base_keywords.csv* abgespeichert. Die Branchenebenen und Bezeichnugen werden in diesem Notebook aufbereitet sowie die Klassifikation vorbereitet. 

### Notebook: Bilanzen
In diesem Notebook wurde die relevanten Daten für die Bilanzen des jeweiligen Unternehmens ermittelt. Da diese Dateien html-Dateien sind, wird html-Parsing angewendet.
#### Anwendungsfall
In den Daten, die für das Projekt mitgegeben wurden, sind unter anderem hmtl-Dateien vorhanden. Für die Bilanz sind diese wichtig, die unter dem Namen „Finanzberichte“ abgespeichert sind. Ziel war es so viele Informationen wie möglich aus diesen Dateien zu ermitteln. Hierbei ist anzumerken, dass diese html Dateien unterschiedlich strukturiert sind. Im Normalfall sind die Daten der Bilanz wie Anlagevermögen, Umlaufvermögen, Verbindlichkeiten etc. vorhanden.
#### Umsetzung
* Zuerst wurden die benötigten Dateien ermittelt, die analysiert werden sollen. Dabei wurden die Files herausgefiltert, die 'rechnungslegung-finanzberichte.html' in ihren Namen beinhalten.
* Html-Parsing mit BeautifulSoup: Die gewünschten Informationen wurden mithilfe von htlm Parsing ermittelt. Dabei wurde sich hauptsächlich auf die tables der html-Dateien fokussiert, da diese die gewünschten Inhalte zum Anlagevermögen, Umlaufvermögen, Eigenkapital, Verbindlichkeiten, etc. beinhalten. 
* Die zeitlichen Daten, wann die Bilanz erstellt, wurde nachträglich hinzufügt, da erkennbar war, dass diese Daten in den Tabellen der html-Dateien nicht immer ermittelt werden konnten.
* Zum Schluss wurden zwei Plots generiert, der erste Plot zeigt den zeitlichen Verlauf des Bilanzvolumens. Der zweite Plot den zeitlichen Verlauf des Gewinns

![Gewinn nach Bilanz](https://raw.githubusercontent.com/joschikahn/DokuPdsHandelsregisterGroup5/main/docs/Data/Gewinn2.png)
![Bilanzensumme](https://raw.githubusercontent.com/joschikahn/DokuPdsHandelsregisterGroup5/main/docs/Data/Bilansum.png)

* Diese sollten auch in die Gradio-App integriert werden, sind aber aufgrund Problemen bei der Gradio-Integration nur im Notebook abgebildet.
* Die gewonnenen Daten wurden in der Datei Bilanzen.csv abgespeichert.
#### Evaluation und Ausblick
* In den meisten Fällen hat das Auslesen der Dateien gut funktioniert
* Aber dennoch ergaben sich einige Probleme
* Die Strukturen der html-Tabellen ist nicht immer einheitlich, deshalb ist es schwierig die Daten automatisiert zu ermitteln
* Auch die Formatierung der Tabellen ist nicht immer gleich
* Des Weiteren, waren auch keine html-Dateien für das jeweilige Unternehmen vorhanden
Diese Faktoren haben dazugeführt, dass einige Bilanzdaten nicht oder falsch ermittelt wurden. Aber dennoch ist hier hervorzuheben, dass dies in den meisten Fällen funktioniert. In der Zukunft sollte der Code erweitert werden, um alle Bilanzdaten zu ermitteln.

### Notebook: XML_to_DatFrame
In diesem Notebook wird das Parsing von xml-Dateien behandelt. Xml-Dateien sind strukturiert und können somit mit lxml.etree ermittelt werden. Es wurden verschiedene Informationen zu den Files ermittelt. Zum einen, welche Personen im Unternehmen tätig sind, ihre dazugehörigen Rollen und die Geschäftszwecke des Unternehmens. Andere Daten wie Anschrift des Unternehmens wurde mithilfe der json-Datei ermittelt. Für das Notebook waren die Daten aus der json-Datei nötig, um eine CSV Datei zu generieren.
#### Anwendungsfall
Um an bestimmte Rohdaten zu den Unternehmen und den Personen zu kommen, wird das xml-Parsing durchgeführt. Aufbauend auf diesen Daten können Modelle und Plots generiert werden. Da zu fast jedem Unternehmen ein xml vorhanden ist, eignet sich dies gut um an Informationen zu gelangen.
#### Umsetzung
* Zuerst werden die benötigten xml-Files aus den Ordnern herausgefiltert. Um diese später einzeln durchzugehen.
* Im nächsten Schritt werden die Definitionen programmiert, die Daten zur Person, zur Rolle und zum Geschäftszweck generieren.
* Durch diese Definitionen werden die einzelnen Files analysiert
* Die Daten werden gegebenenfalls zusammengeführt und abgespeichert
#### Evaluation und Ausblick
* Schwierigkeiten beim xml-Parsing waren Kodierungsfehler, da bei manchen Files die Codierung gefehlt oder falsch war. Dies hat dazu geführt, dass einige xml-Files nicht analysiert werden konnten.
* Diese Kodierungsfehler konnten nicht behoben werden, deshalb wurden diese fehlerhaften Files herausgefiltert.
* Dennoch ist wieder zu betonen, dass für die meisten Fälle das xml-Parsing funktioniert und genügend Daten wurden extrahiert.

### Notebook: Registerbekanntmachungen_html
Neben den html-Files, die Daten bezüglich der Bilanz beinhalten, gibt es wiederum html-Files, die Informationen bezüglich der Registerbekanntmachungen. Diese Bekanntmachungen beinhalten, beispielsweise einen Wechsel in der Geschäftsführung, die Änderung des Unternehmenszwecks, die Änderung des Sitzes des Unternehmens.
#### Anwendungsfall
Hier wird wieder html-Parsing betrieben. Diese Informationen können verwendet werden, um mithilfe eines Zeitstrahles aufzuzeigen, wann welche Veränderungen im Unternehmen aufgetreten sind. 
#### Umsetzung
* Zuerst werden wieder die benötigten Files in den Ordnern herausgefiltert und zwischengespeichert.
* Danach werden die einzelnen Informationen der Bekanntmachungen ermittelt:
 * Die Art der Bekanntmachung
 * Das Datum
 * und der Text der Bekanntmachung
* Diese Daten werden formatiert und in ein Dataframe eingespeichert
* Die Umsetzung des Zeitstrahles erfolgt in der Gradio-App
#### Evaluation und Ausblick
Auch hier gab es wieder Kodierungsfehler und html-Files, die nicht „geparst“ werden konnten, diese mussten entfernt werden. Zukünftig wäre es besser, diese Kodierungsfehler zu umgehen, um mehr Daten für den Datensatz zu generieren. Dennoch ist abschließend zu sagen, dass das Parsing ein Erfolg war.

### Notebook: Umkreissuche 
  In diesem Notebook wird die Umkreissuche vorbereitet: u.A: werden die Koordinaten für alle Firmen mit GeoPy berechnet und abgespeichert. Anwendungsfall und Umsetzung wird im Abschnitt *App* genauer erläutert

### Notebook: k_means_clustering_nach_tfidf
  luster eingeteilt. 
#### Anwendungsfall
  Inhaltliche ähnliche Unternehmen sollen in ein Cluster gemacht werden. *Welche ähnliche Unternehmen gibt es wie das Unternehmen "Müller Heizungsbau GmbH?".
  Diese können dann beispielsweise als Vorschläge empfohlen werden. Vor allem mit Umkreissuche sehr interessant: z.B. *In der Umgebung gibt es folgende Ähnliche Unternehmen*
#### Umsetzung 
  Der Geschäftszweck dient als Grundlage für diesen unsupervised learning Ansatz.Weiter wird auf zwei verschiedenen Art und Weisen das Clustering vorgenommen. 
  1. Nach unverarbeiteter Geschäftszweck 
  2. Nach auf Schlagwörter reduzierte Geschäftszweck: Nur Nomen und ohne aussagelose Wörter wie *Unternehmen*, *Gesellschaft*, *GmbH* usw. 
  Entsprechend der Art werden dafür TF-IDF-Vektoren gebildet (*sklearn tfidf vectorizer*). Anschließend wird darauf der k-Means-Algorithmus angewendet.
  Auch hierbei werden verschiedenen Varianten mit verschiedenen Granularität durchgeführt: 
   * Grob: 5 Cluster
   * Mittel: 20 Cluster 
   * Fein: 100 Cluster
   * Sehr fein: 200 Cluster 

  Die Ergebnisse (= Cluster-Nummern) werden in am Dataframe als jeweils (pro Clustering Art und Granularität) als neue Spalte in den Dataframe eingehängt. Anschließend können diese Clustering Ergebnisse genutzt werden. Zum Beispiel für eine Vorschlagfunktion für ähnliche Unternehmen: 
  [Ähnliche Unternehmen finden anhand Clustering](https://raw.githubusercontent.com/joschikahn/DokuPdsHandelsregisterGroup5/main/docs/Data/unsupervised_kmeans_clustering.gif). 

  Das Clustering lässt sich mithilfe einer PCA visualisieren.

  Ähnliche Unternehmen werden dann anhand der eingeteilten Cluster vorgeschlagen.
  ![KMeans mit 5 Clustern - mit PCA visualisiert](https://raw.githubusercontent.com/joschikahn/DokuPdsHandelsregisterGroup5/main/docs/Data/visualisierung_5means_keywords_pca.png)
  ![KMeans mit 20 Clustern - mit PCA visualisiert](https://raw.githubusercontent.com/joschikahn/DokuPdsHandelsregisterGroup5/main/docs/Data/visualisierung_20means_keywords_pca.png)
####  Evaluation und Ausblick 
  6753 Unternehmen (= alle Firmen mit Geschäftszweck) sind auf diese Art in Cluster eingeteilt worden. Dabei sind insbesondere zwei Problem aufgetreten:
  * Teilweise sehr ungleichmäßige Cluster (Sehr volle und sehr leere Cluster). Lässt sich durch verschiedene Iterationen und verschiedene Initiale Cluster-Zentren beeinflussen (auf Kosten der Rechenzeit).
 
  * Cluster sind nicht immer logisch nachvollziehbar. Bei gefundenen Cluster ist der Zusammenhang zwischen den zugeordneten Firmen teilweise nicht logisch nachvollziehbar und somit kein Oberbegriff bestimmbar. Passender Zusammenhang feststellbar: Clustering nach Keywords, WordCloud-Darstellung nach Unternehmensnamen. 
  ![Erkennbarer Cluster-Zusammenhang: z.B. Handel Mode/Textilien]("https://raw.githubusercontent.com/joschikahn/DokuPdsHandelsregisterGroup5/main/docs/Data/means20_cluster_17_keywords.png")
  ![Erkennbarer Cluster-Zusammenhang: z.B. Handwerk ](https://raw.githubusercontent.com/joschikahn/DokuPdsHandelsregisterGroup5/main/docs/Data/means20_cluster_4_keywords.png)
  ![Mittel erkennbarer Cluster-Zusammenhang: z.B. Wohnungs-und Grundstückswesen](https://raw.githubusercontent.com/joschikahn/DokuPdsHandelsregisterGroup5/main/docs/Data/means20_cluster_18_keywords.png)
  ![Schlecht erkennbarer Cluster-Zusammenhang](https://raw.githubusercontent.com/joschikahn/DokuPdsHandelsregisterGroup5/main/docs/Data/means20_cluster_3_keywords.png)
  Ergänzende Information dazu im Notebook als Kommentar / Markdown.


## Verworfene Ansätze

### Notebook: reading_tif_and_pdf_files_by_orc
 In diesem Notebook wurde versucht alle TIF- & PDF-Dateien mit Hilfe von OCR ausgelesen. Der Ansatz wurde verworfen weil es Probleme bei Installation & Nutzung der benötigten packages auf dem lokalen Windows System gab. Bei, Ausführen in Google Colab, sollte der Code funktionieren und somit nicht nur TIF-, sondern auch PDF-Dateien ausgelesen werden können.

### Notebook: branchen_bestimmung_nlp_semantic_similarity
  In diesem Notebook wird die Branchen-Klassifizierung anhand der semantischen Ähnlichkeit von Tätigkeitsbeschreibung und Branchenbezeichnung beschrieben. Es verwendet die Dateien branchen_bestimmung_base.csv

#### Anwendungsfall: 
  Die offizielle Wirtschaftszweige sind sehr unübersichtlich. Es gibt verschiedene Ebenen und über 870 Subbranchen mit verschiedenen Codes. 
  Für viele Tätigkeitsbeschreibungen ist es schwierig, die passende Branche nach WZ-2008 zu finden. In diesem Notebook werden automatisch Vorschläge für eine korrekte Einteilung in die WZ-2008 Branchenbezeichnungen umgesetzt:
  Freitextsuche nach Tätigkeit: *Drehen und Fräsen von Aluminiumprofilen*  --> Branche: Metallverarbeitenden --> ähnliche Firmen aus dieser Branche können angezeigt werden.
  
#### Umsetzung:
 
  * Preprocessing: Firmenbeschreibung auf Nomen reduziert mit Spacy-Tokenizer und wenig aussagekräftige Nomen & spezielle Rechtsbegriffe entfernt wie  *Unternehmen*, *Gesellschaft*, *Zweigniederlassung*
  *  Großes Spacy-Sprachmodel *de_core_news_lg* gleicht die Firmenbeschreibung mit den Branchenbezeichnungen aus dem WZ-2008 Register ab und ermittelt die semantische Ähnlichkeit anhand des similarity Wertes. Je nach Granularität werden die entsprechenden Branchenbezeichnungen als Vergleichsstring herangezogen Abschnitt, Branche, Sub-, Sub-Sub-, Sub-Sub-Sub-Branche. 
  *  Die Organisation wird anhand der Beschreibung der best-passendste Branche zugeordnet (diejenige mit dem höchsten Similariy-Wert). Die top 5 Branchen werden zu der Organisation zugeordnet werden und damit alle Firmen klassifiziert werden. 
  *  Die Funktionalität lässt sich am besten verdeutlichen, indem man *neue* Firma anhand einer Tätigkeitsbeschreibung in die WZ-2008 Norm einordnen möchte: ![Semantische Ähnlichkeit](https://raw.githubusercontent.com/joschikahn/DokuPdsHandelsregisterGroup5/main/docs/Data/branchen_klassifizierung_wz2008_semantic_similarity.gif)
* 
  * Darüber hinaus. Semantische Ähnlichkeit-Suche unabhängig von der Brancheneinteilung. 

#### Evaluation und Ausblick 
  Der Ansatz ist voll funktionsfähig und als Feature nutzbar. Die semantische Klassifizierung mit dem Spacy-Similarity-Abgleich ist dennoch nicht in APP-Anwendung integriert, da der Ansatz des Zero-Shot-Classification meistens nachvollziehbarer Ergebnisse liefert. 
    * Die semantische Ähnlichkeit-Suche unabhängig der gefunden Cluster, ist aufgrund sehr langer Rechenzeiten (circa 3 Minuten pro Anfrage) nur unter erheblichen Rechenzeitoptimierungen für eine größere Skalierung im Handelsregister denkbar. 


## Dateien

### OCR.csv
Diese CSV-Datei repräsentiert folgendes Dataframe "bild ocr"
In "content" sind hierbei die Inhalte aller extrahierten TIF-Dateien enthalten. Die Datei stammt aus dem Notebook 

### Bilanzen.csv
Inhalt der CSV stammmt aus Notebook Bilanzen

### merged_un_roles_personspd.csv
Inhalt der CSV stammmt aus Notebook XML_to_Dataframe

### persons.csv
Inhalt der CSV stammmt aus Notebook XML_to_Dataframe

### Gegenstand_oder_Geschaeftszweck_all.csv
Inhalt der CSV stammmt aus Notebook XML_to_Dataframe

### count_personsid.csv
Inhalt der CSV stammmt aus Notebook XML_to_Dataframe

### DataFrame_Changes.csv
Inhalt der CSV stammmt aus Notebook Registerbekanntmachungen_html

### branchen_bestimmung_base_keywords.csv
Grundlage für Branchenklassifikation mit Zero-Shot, Branchenklassifikation mit Spalcy-Similarity und für das unsuperviesed Clustering. Beinhaltet den Geschäftszweck und auf Nomen reduzierte und *aussagekräftig* (nicht *Unternehmen*, *Gesellschaft*, usw.) Schlagwörter.

### branchen_labels_code_oberkat.csv
Beinhaltet die identifiziete Brachen-Bezeichnungen für alle Firmen mit Beschreibung inkl. der Oberkateogrie (Abschnitt) und den WZ2008 Branchencodes.

### companies_desc_keywords_nlp_generated.csv
Diese Datei beinhaltet die Ergebnisse der Branchenklassifizierungen nach dem Spacy-Similarity Ansatz. 

### vergleich_auswertung_branchen_classification.csv
Diese Datei wurde für die Evaluation der beiden WZ-2008 Branchenklassifikationen verwendet. Diese Datei stammt aus dem einem Merge *branchen_labels_code_oberkat.csv* und *companies_desc_keywords_nlp_generated.csv*. Für beide Ansätze sind die drei besten Predictions als Spalte angehängt.
Aus diesem Merge der (mit 6750 Unternehmen) wurden für zufällige 54 Unternehmen ausgewertet (Spalte Accuracy und Within Top3-Accuracy).  












