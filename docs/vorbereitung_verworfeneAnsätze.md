# Vorbereitung & verworfener Code:

## Vorbereitung

### Notebook: Reading TIF-Files by OCR
In diesem Notebook werden alle TIF-Dateien mit Hilfe von OCR ausgelesen und einem Dataframe df gespeichert. Dieses wurde exportiert um es in der App für die Funktion "Dateisuche in TIF-Dateien" zu nutzen.

### Notebook: Zero-Shot-Classification Branche WZ-2008
In diesem Notebook wird die Umsetzung der Branchenklassifikation inkl. der verschiedenen Vorbereitungsschritte beschreiben bzw. ausgeführt. 

#### Anwendungsfall 
Branchen klassifizieren nach WZ-2008 üblichen Branchen, ...

#### Umsetzung 
Zero-Shot-Classification usw.

#### Evaluation und Ausblick 
Ausblick: Labelling möglich für deutliche Performanceverbesserung ...
### Notebook: Bilanzen
In diesem Notebook, wurde die relevanten Daten für die Bilanzen des jeweiligen Unternehmens ermittelt. Da diese Dateien html-Dateien sind, wird html-Parsing angewendet.
#### Anwendungsfall
In den Daten, die für das Projekt mitgegeben wurden, sind unteranderem hmtl-Datein vorhanden. Für die Bilanz sind diese wichtig die unter dem Namen 'finanzberichte' abgespeichert sind. Ziel war es so viele Informationen wie möglich aus diesen Dateien zu ermitteln. Hierbei ist anzumerken, dass diese html Datein unterschiedlich strukturiert sind. Im normal Fall sind die Daten der Bilanz wie Anlagevermögen, Umlaufvermögen, Verbindlichkeiten etc. vorhanden.
#### Umsetzung
* Zuerst wurden die benötigten Datein ermittelt, die analysiert werden sollen. Dabei wurden die Files herausgefilter die 'rechnungslegung-finanzberichte.html' in ihren Namen beinhalten.
* html Parsing mit BeautifulSoup: Die gewünschten Informationen wurden mit Hilfe von htlm Parsing ermittelt. Dabei wurde sich hauptsächlich auf die tables der html Dateien fokussiert. Da diese, die geschwünschten Inhalte, zum Anlagevermögen, Umlaufvermögen, Eigenkapital, Verbindlichkeiten, etc. binhalten. 
* Die zeitlichen Daten, wann die Bilanz erstellt wurde wurde nachträglich hinzufügt, da erkennbar war, das diese Daten in den Tabllen der html-Datein nicht immer ermittelt werden konnten.
* Zum Schluss wurden zwei Plots generiert, der erste Plot zeigt den zeitlichen Verlauf des Bilanzvolumens. Der zweite Plot den zeitlichen Verlauf des Gewinns

![Gewinn nach Bilanz](https://github.com/joschikahn/DokuPdsHandelsregisterGroup5/blob/main/docs/Data/Gewinn2.png  "Gewinn/Verlust")
![Bilansumme](https://github.com/joschikahn/DokuPdsHandelsregisterGroup5/blob/main/docs/Data/Bilansum.png "Bilanzumme")



* Diese sollten auch in die Gradioapp integriert werden, aber wegen Umsetzungschwierigkeiten, sind diese nur im Notebook abgebildet.
* Die gewonnenen Daten wurden in der Datei Bilanzen.csv abgespeichert
#### Evaluation und Ausblick
* In den meisten Fällen hat das Auslesen der Datein gut funktioniert
* Aber dennoch ergaben sich einige Probleme
* Die Strukturen der html-Tabllen ist nicht immer einheitlich, deshalb ist es schwierig die Daten automatisiert zu ermitteln
* Auch die Formatierung der Tabllen ist nicht immer gleich
* Desweiteren, waren auch keine html-Datein für das jeweilige Unternehmen vorhanden
Diese Faktoren haben dazugeführt, dass einige Bilansdaten nicht oder falsch ermittelt wurden. Aber dennoch ist hier hervorzuheben, dass dies in den meisten Fällen funktioniert. In der Zukuft sollte der Code erweitert werden, um alle Bilanzdaten zu ermitteln.
### Notebook: XML_to_DatFrame
In diesem Notebook wird das Parsing von xml-Dateien behandelt. Xml-Datein sind strukturiert und können somit mit lxml.etree ermittelt werden. Es wurden verschiedene Informationen zu den Files ermittelt. Zum einen, welche Personen im Unternehmen tätig sind, ihre dazugehörigen Rollen und die Geschäftszwecke des Unternehmens. Andere Daten wie Anschrift des Unternehmens wurde mit Hilfe der json-Datei ermittelt. Für das Notebook waren die Daten aus der json-Datei nötig, um eine csv Datei zu generieren.

#### Anwendungsfall
Um an gewissse Rohdaten zu den Unternehmen und den Personen zu kommen, wird das xml-Parsing durchgeführt. Aufbauend auf diesen Daten können Modelle und Plots generiert werden. Da zu fast jedem Unternehmen ein xml vorhanden ist, eignet sich dies gut um an Informationen zu gelangen.

#### Umsetzung
* Zuerst werden die benötigten xml-Files aus den Ordner herausgefiltert. Um diese später einzeln durchzugehen.
* Im nächstem Schritt werden die Definitionen programmiert, die Daten zur Person, zur Rolle und zum Geschäftszweck generieren.
* Durch diese Definitionen werden die einzelnen Files analysiert
* Die Daten werden gegebnenfalls zusammengeführt und abgespeichert
#### Evaluation und Ausblick
* Schwierigkeiten beim xml-Parsing waren Codierungsfehler, da bei manchen files die Codierung gefehlt oder falsch war. Dies hat dazu geführt, dass einige xml-Files nicht analysiert werden konnten.
* Diese Codierungsfehler konnten nicht behoben werden, deshalb wurden diese fehlerhaften Files herausgefiltert.
* Dennoch ist wieder zu betonen das für die meisten Fälle das xml-Parsing funktioniert und genügend Daten wurden extrahiert.
### Notebook: Registerbekanntmachungen_html
#### Anwendungsfall
#### Umsetzung
#### Evaluation und Ausblick

## Verworfene Ansätze

### Notebook: VERWORFEN Reading TIF- and PDF-Files by OCR
 In diesem Notebook wurde versucht alle TIF- & PDF-Dateien mit Hilfe von OCR ausgelesen. Der Ansatz wurde verworfen weil es Probleme bei Installation & Nutzung der benötigten packages auf dem lokalen Windows System gab. Bei, Ausführen in Google Colab, sollte der Code funktionieren und somit nicht nur TIF-, sondern auch PDF-Dateien ausgelesen werden können.

### Notebook: branchen_bestimmung_nlp_semantic_similarity
  In diesem Notebook wird die Branchen-Klassifizierung anhand der semantischen Ähnlichkeit von Tätigkeitsbeschreibung und Branchenbezeichnung beschrieben. Es verwendet die Dateien branchen_bestimmung_base.csv

#### Anwendungsfall: 
  Die offizielle Wirtschaftszweige sind sehr unübersichtlich. Es gibt verschiedene Ebenen und über 870 Subbranchen mit verschiedenen Codes. 
  Für viele Tätigkeitsbeschreibungen ist es schwierig, die passende Branche nach WZ-2008 zu finden. In diesem Notebook werden automatisch Vorschläge für eine korrekte Einteilung in die WZ-2008 Branchenbezeichnungen umgesetzt:
  Freitextsuche nach Tätigkeit: *Drehen und Fräsen von Aluminiumprofilen*  --> Branche: Metallverarbeitenden --> ähnliche Firmen aus dieser Branche können angezeigt werden.
  
#### Umsetzung:
 
  * Preprocessing:  Firmenbeschreibung Nomen reduziert mit Spacy-Tokenizer und wenig aussagekräftige Nomen und spezielle Rechtsbegriffe entfernt wie  *Unternehmen*, *Gesellschaft*, *Zweigniederlassung*
  *  Großes Spacy-Sprachmodel *de_core_news_lg* gleicht die Firmenbeschreibung mit den Branchenbezeichnungen aus dem WZ-2008 Register ab und ermittelt die semantische Ähnlichkeit anhand des similarity Wertes. Je nach Granularität werden die entsprechenden Branchenbezeichnungen als Vergleichsstring herangezogen Abschnitt, Branche, Sub-, Sub-Sub-, Sub-Sub-Sub-Branche. 
  *  Die Organisation wird anhand der Beschreibung der best-passendste Branche zugeordnet (diejenige mit dem höchsten Similariy-Wert). Die top 5 Branchen werden zu der Organisation zugeordnet werden und damit alle Firmen klassifiziert werden. 
  *  Die Funktionalität lässt sich am besten verdeutlichen, indem man *neue* Firma anhand einer Tätigkeitsbeschreibung in die WZ-2008 Norm einordnen möchte: ![Branche Klassifizieren nach NLP](https://media.giphy.com/media/5uDbVaE7cLIIqlVYkd/giphy.gif)

  * Darüber hinaus. Semantische Ähnlichkeit-Suche unabhängig von der Brancheneinteilung. 

#### Evaluation und Ausblick 
  Der Ansatz ist voll funktionsfähig und als Feature nutzbar. Die semantische Klassifizierung mit dem Spacy-Similarity-Abgleich ist dennoch nicht in APP-Anwendung integriert, da der Ansatz des Zero-Shot-Classification meistens nachvollziehbarer Ergebnisse liefert. 
    * Die semantische Ähnlichkeit-Suche unabhängig der gefunden Cluster, ist aufgrund sehr langer Rechenzeiten (circa 3 Minuten pro Anfrage) nur unter erheblichen Rechenzeitoptimierungen für eine größere Skalierung im Handelsregister denkbar. 


### Notebook: k_means_clustering_nach_tfidf

  Dieses Notebook beschreibt ein Clustering Ansatz der Unternehmen mit einem unsupervised Learning Ansatz. Anhand des Geschäftszweckes werden die Firmen in verschiedener Granularität in Cluster eingeteilt. 

#### Anwendungsfall
  Inhaltliche ähnliche Unternehmen sollen in ein Cluster gemacht werden. *Welche ähnliche Unternehmen gibt es wie das Unternehmen "Müller Heizungsbau GmbH?".
  Diese können dann beispielsweise als Vorschläge empfohlen werden. Vor allem mit Umkreissuche sehr interessant: z.B. *In der Umgebung gibt es folgende Ähnliche Unternehmen*

#### Umsetzung 
  Der Geschäftszweck dient als Grundlage für diesen unsupervised learning Ansatz.Weiter wird auf zwei verschiedenen Art und Weisen das Clustering vorgenommen. 
  1. Nach unverarbeiteter Geschäftszweck 
  2. Nach auf Schlagwörter reduzierte Geschäftszweck: Nur Nomen und ohne aussagelose Wörter wie *Unternehmen*, *Gesellschaft*, *GmbH* usw. 

  Entsprechend der Art werden dafür TF-IDF-Vektoren gebildet (sklearn tfidf vectorizer). Anschließend wird darauf der k-Means-Algorithmus angewendet.
  Auch hierbei werden verschiedenen Varianten mit verschiedenen Granularität durchgeführt: 
   * Grob : 5 Cluster
   * Mittel: 20 Cluster 
   * Fein: 100 Cluster
   * Sehr feint: 200 Cluster 

  Die Grobe Visualisierung lässt sich mithilfe einer PCA so visualisieren. Die Ergebnisse (= Cluster-Nummern) werden in am Dataframe als jeweils (pro Clustering Art und Granularität) als neue Spalte in den Dataframe eingehängt. Anschließend können diese Clustering Ergebnisse genutzt werden. Zum Beispiel für eine Vorschlagfunktion für ähnliche Unternehmen: 
  ![hier gezeigt](https://media.giphy.com/media/h9SgiKNGf6DldceSKr/giphy.gif). 

  Ähnliche Unternehmen werden anhand des Clustering vorgeschlagen.

####  Evaluation und Ausblick 
  6753 mit Geschäftszweck sind auf diese Art in Cluster eingeteilt worden. Dabei sind insbesondere zwei Problem aufgetreten:
  * Teilweise sehr ungleichmäßige Cluster (Sehr volle und sehr leere Cluster). Lässt sich durch verschiedene Iterationen und verschiedene Initiale Cluster-Zentren beeinflussen (auf Kosten der Rechenzeit). 

  * Cluster sind nicht immer logisch nachvollziehbar. Bei gefundenen Cluster ist der Zusammenhang zwischen den zugeordneten Firmen teilweise nicht logisch nachvollziehbar und somit kein Oberbegriff bestimmbar.  Passender Zusammenhang feststellbar: Clustering nach Keywords, WordCloud-Darstellung nach Unternehmensnamen.  

Ergänzende Information dazu im Notebook als Kommentar / Markdown.


## Dateien

### OCR.csv
Diese CSV-Datei repräsentiert folgendes Dataframe "bild ocr"

In "content" sind hierbei die Inhalte aller extrahierten TIF-Dateien enthalten. Die Datei stammt aus dem Notebook 

### ....csv
Inhalt der CSV... stammmt aus Notebook X

### ....csv
Inhalt der CSV... stammmt aus Notebook X







