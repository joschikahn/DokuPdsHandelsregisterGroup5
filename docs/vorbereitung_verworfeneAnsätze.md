# Vorbereitung & verworfene Ansätze

## xml_data_extraction




## html_data_extraction



## ocr_data_extraction



## branchen_bestimmung_nlp_semantic_similarity.ipynb

In diesem Notebook wird die Branchen-Klassifizierung aufgrund der semantischen Ähnlichkeit von Tätigkeitsbeschreibung und Branchenbezeichung beschrieben. 
---
### Anwendungsfall

Die üblichen WZ-2008 Brachen anhand der Beschreibung bwz. des Geschäftszweckes klassifizieren. 
Problem: Unübersichtliche Branchenlandschaft. Über 870 Subbrachen. Schwierig die passende Branche zu finden. 
Auch für Filterfunktion praktisch. Freitextsuche eingeben. 

* Semantische Freitextsuche nach Tätigkeit: *Drehen und Fräsen von Aluminumprofilen* und Unternehmen aus dieser Branche erhalten
* Neu hinzukommende Unternehmen können auf diese Art und Weise in die üblichen Branchen eingordnet werden.

### Umsetzung / Vorgehen 

* Preprocessing der Firmenbeschreibung: 
  * Auf Nomen reduziert mit Spacy-Tokenizer 
  * Wenig aussagekräftige Nomen und spezielle Rechtsbegriffe entfernt wie  "Unternehmen", "Gesellschaft", "Zweigniederlassung"

* Großes Spacy-Sprachmodel *de_core_news_lg* gleicht die Beschreibung mit den Branchenbezeichungen aus dem WZ-2008 Register ab und ermittelt die semantische Ähnilchkeit anhand des similarity Wertes. Je nach Granulariät werden die entsprechenden Branchenbezeichnnungen als Vergleichsstring herangezogen (Abschnitt, Branche, Sub-, Sub-Sub-, Sub-Sub-Sub-Branche). 
  Die Beschreibung wird der Branche zugeordnet die den höchsten Similariy-Wert von allen aufweist. 
  ![Branche Klassifitieren nach NLP](.\Data\branchen_klassifizierung_wz2008_semantic_similarity.gif) 

* Semantische Ähnlichkeitssuchen unabhänig von der Brancheneinteilung. 

### Evaluation

* Ansatz über NLP-Similarity nicht in APP-Anwendung, da Zero-Shot-Classification meistens nachvollziehbarerer Ergebnisse liefert. 
* Die semantische Ähnlichkeitssuche unabhängig der gefunden Cluster, ist aufgrund sehr langer Rechenzeiten (circa 3 Minuten pro Anfrage) nur unter erheblichen Rechenzeitoptimierungen für eine größere Skalierung im Handelsregister denkbar. 
* 
Insbesondere gegenüber dem Zero-Shot-Classificator aus LINKEINFÜGEN ist dieser Ansatz bezüglich Laufzeit und Genauigkeit unterlegen. 


## k_means_clustering_nach_tfidf.ipyn




## Dateien

### ....csv
Inhalt der CSV... stammmt aus Notebook X

### ....csv
Inhalt der CSV... stammmt aus Notebook X

### ....csv
Inhalt der CSV... stammmt aus Notebook X