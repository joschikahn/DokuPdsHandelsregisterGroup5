# Vorbereitung & verworfener Code

## Vorbereitung

### Notebook: Reading TIF-Files by OCR
In diesem Notebook werden alle TIF-Dateien mit Hilfe von OCR ausgelesen und einem Dataframe df gespeichert. Dieses wurde exportiert um es in der App für die Funktion "Dateisuche in TIF-Dateien" zu nutzen.


## Verworfene Ansätze

### Notebook: VERWORFEN Reading TIF- and PDF-Files by OCR
 In diesem Notebook wurde versucht alle TIF- & PDF-Dateien mit Hilfe von OCR ausgelesen. Der Ansatz wurde verworfen weil es Probleme bei Installation & Nutzung der benötigten packages auf dem lokalen Windows System gab. Bei, Ausführen in Google Colab, sollte der Code funktionieren und somit nicht nur TIF-, sondern auch PDF-Dateien ausgelesen werden können.

### Notebook: branchen_bestimmung_nlp_semantic_similarity
  In diesem Notebook wird die Branchen-Klassifizierung anhand der semantischen Ähnlichkeit von Tätigkeitsbeschreibung und Branchenbezeichnung beschrieben.

#### Anwendungsfall: 
  Die offizielle Wirtschaftszweige sind sehr unübersichtlich. Es gibt verschiedene Ebenen und über 870 Subbranchen mit verschiedenen Codes. 
  Für viele Tätigkeitsbeschreibungen ist es schwierig, die passende Branche nach WZ-2008 zu finden. In diesem Notebook werden automatisch Vorschläge für eine korrekte Einteilung in die WZ-2008 Branchenbezeichnungen umgesetzt: z.B. Freitextsuche nach Tätigkeit: *Drehen und Fräsen von Aluminiumprofilen*  --> Branche: Metallverarbeitenden 

#### Umsetzung / Vorgehen:
 
  1. Firmenbeschreibung Nomen reduziert mit Spacy-Tokenizer 
  2. Wenig aussagekräftige Nomen und spezielle Rechtsbegriffe entfernt wie  "Unternehmen", "Gesellschaft", "Zweigniederlassung"
  3.  Großes Spacy-Sprachmodel *de_core_news_lg* gleicht die Beschreibung mit den Branchenbezeichnungen aus dem WZ-2008 Register ab und ermittelt die semantische Ähnlichkeit anhand des similarity Wertes. Je nach Granularität werden die entsprechenden Branchenbezeichnungen als Vergleichsstring herangezogen (Abschnitt, Branche, Sub-, Sub-Sub-, Sub-Sub-Sub-Branche). 
  4.  Die Beschreibung wird der Branche zugeordnet die den höchsten Similariy-Wert von allen aufweist. ![Branche Klassifizieren nach NLP](.\Data\branchen_klassifizierung_wz2008_semantic_similarity.gif) 

  * Semantische Ähnlichkeit-Suche unabhängig von der Brancheneinteilung. 
  * Ansatz über NLP-Similarity nicht in APP-Anwendung, da Zero-Shot-Classification meistens nachvollziehbarer Ergebnisse liefert. 
  * Die semantische Ähnlichkeit-Suche unabhängig der gefunden Cluster, ist aufgrund sehr langer Rechenzeiten (circa 3 Minuten pro Anfrage) nur unter erheblichen Rechenzeitoptimierungen für eine größere Skalierung im Handelsregister denkbar. 
  Insbesondere gegenüber dem Zero-Shot-Classificator aus Abschnitt App ist dieser Ansatz bezüglich der Genauigkeit unterlegen.

  #### Evaluation und Ausblick 

  


### Notebook: k_means_clustering_nach_tfidf



## Dateien

### OCR.csv
Diese CSV-Datei repräsentiert folgendes Dataframe "bild ocr"

In "content" sind hierbei die Inhalte aller extrahierten TIF-Dateien enthalten. Die Datei stammt aus dem Notebook 

### ....csv
Inhalt der CSV... stammmt aus Notebook X

### ....csv
Inhalt der CSV... stammmt aus Notebook X







