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







