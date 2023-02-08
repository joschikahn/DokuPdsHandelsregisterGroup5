# App

In diesem Notebook sind die finalen Anwendungen zusammengefügt. Die Funktionalitäten basieren auf die aufbereiteten CSV-Dateien, die für die Frontend-Funktionalitäten verwendet werden. Das Notebook ist unabhängig von den anderen Notebooks ausführbar. 
Nachfolgend werden die Funktionalitäten der App, sowie deren Umsetzung und Evaluation beschrieben. 
Datenextraktion, -aufbereitung und die Vorbereitung der Einzelfunktionen sind nicht in diesem Notebook enthalten, sondern werden unter Abschnitt [Vorbereitung und verworfene Ansätze](https://dokupdshandelsregistergroup5.readthedocs.io/en/latest/vorbereitung_verworfeneAns%C3%A4tze) durchgeführt und ausführlicher dokumentiert. 

## Notebook

### Funktion: Dateisuche in TIF-Dateien
Die im Notebook *Reading TIF-Files by OCR* in [Vorbereitung & verworfener Code](#Vorbereitung-&-verworfener-Code) ausgelesenen Informationen werden hier verwendet um heraus zu finden, ob in den TIF-Dateien noch zusätzliche Informationen zu einem Unternehmen verfügbar sind. Wenn dies der Fall ist, kann die Datei mit einem Klick heruntergeladen und die Information ausgelesen werden.

### Funktion: Branchenklassifikation WZ-2008

Anhand einer Freitexteingabe können die Firmen in die offiziell WZ-2008 Branchenlandschaft eingeordnet werden. Entsprechend der verschiedener Granularität (Abschnitt, Branche, Sub-, Sub-Sub-, Sub-Sub-Sub-Branche) werden Vorschläge inklusive der WZ2008-Codes für eine Einordnung geliefert. Genauere Erklärung,  Vorgehensweise und Auswertung in [Vorbereitung und verworfene Ansätze](https://dokupdshandelsregistergroup5.readthedocs.io/en/latest/vorbereitung_verworfeneAns%C3%A4tze).
Auf Basis der Branchenklassifikation wird außerdem ein Ähnlichkeitssuche durchgeführt. Im Tab *ähnliche Firmen finden* lässt sich gezielt nach Unternehmen aus der selben Branche im Umkreis suchen. 
#### Anwendungsfall
Die Branchenbezeichnungen nach der offiziellen Norm für Wirtschaftszweige kann sehr unübersichtlich sein. Mit insgesamt über 1200 verschiedene Branchenbezeichnungen verliert man schnell den Überblick und eine Selection per Dropdown oder 
![Branchenlandschaft nach WZ-2008](https://raw.githubusercontent.com/joschikahn/DokuPdsHandelsregisterGroup5/main/docs/Data/wz-2008_klassifizierung.png). 
1. Einordnen der vorhandenen Firmen z.B für Filteroperationen oder Ähnlichkeit-Suche. Welche ähnliche Firmen gibt es?
2. Für neue hinzukommenden bzw. neugegründete Firmen bestimmen in welche Branche sie eingeordnet werden sollen. 
#### Umsetzung 
  1.  Zero-Shot-Classification verwendet basierend auf dem speziell auf die deutsche Sprache trainierten Modell *xml-roberta*. 
  Da es nach WZ-2008 Norm über 1000 Branchenbezeichnungen gibt, habe für uns für einen Zero-Shot-Classification Ansatz entschieden. Das heißt, dass es nur die Branchenbezeichnungen vorgegeben werden. Die Firmen werden anhand der auf Schlagwörter reduzierte Geschäftszweck-Beschreibung in diese Branchen eingeteilt. Für alle Firmen mit Beschreibung wurden die Branchen (ebene Branche und Abschnitt) bestimmt. Die drei best-passendeste Branchen werden gespeichert. Alle Firmen mit Beschreibung in die Branchen eingeordnet. Das lässt sich für Filteroperationen und für den Vorschlag von ähnlichen Unternehmen verwenden.
  1. Anwendung für neue Unternehmen: Anhand einer Freitext-Tätigkeitsbeschreibung werden Vorschläge für die Branche nach WZ-2008 und den offiziellen Branchencode bestimmt.
#### Evaluation und Ausblick 
Für alle Firmen mit Geschäftszweck (=6753 Firmen) wurde eine Klassifikation inkl. Bestimmung der Oberbranche durchgeführt. Bezüglich der Rechenzeit für das 'Durchklassifizieren' der Firmen' bietet sich noch kleinere Modelle an, da es in unserem Fall eine Rechendauer von ci. 30 Stunden hatte.
Wir haben keine gelabelten Daten verwendet, konnten dennoch gute Ergebnisse erzielen. Insbesondere besser als der Ansatz über einen Similarity-Abgleich. Vor allem bei *guten* Firmenbeschreibungen sind die gefundenen Branchen zutreffend. Bei Firmenbeschreibungen von schlechter Qualität sind die gefundenen Klassifikationen entsprechen auch schlechter. 
Ausblick: Labelling möglich für deutliche Performanceverbesserung. Die Rechenzeit stellt ein weitere Optimierungspotential dar, insbesondere auf der Granularität Sub-,Sub-Sub- oder Sub-Sub-Sub-Branche. In einem späteren Einsatz ist dies allerdings nicht von zu einschränkender Bedeutung, da diese Klassifikation nur einmalig durchgeführt werden (bei Anlegen). 

Im Vergleich zum Ansatz über Spacy-Sentence-Similarity zeigt sich der *XML-Roberta-Zero-Shot-Classificator* als Gewinner. 
![Vergleich Accuracy](https://raw.githubusercontent.com/joschikahn/DokuPdsHandelsregisterGroup5/main/docs/Data/acc_1_vergleich_spacy_zsc_branchenklass.png)
![Vergleich Accuracy within Top 3](https://raw.githubusercontent.com/joschikahn/DokuPdsHandelsregisterGroup5/main/docs/Data/acc_3_vergleich_spacy_zsc_branchenklass.png)


### Funktion: Q-A-Chatbot

Dem Chatbot können beliebe Fragen zu Unternehmen, Personen oder sonstiges (z.B. Orte/Regionen) gefragt werden. Die Funktionalität basiert auf einer Kombination aus Named Entity Recognition und einer extractive Q-A-Model und wird genauer im Notebook *chatbot.ipynb* in Abschnitt [Vorbereitung und verworfene Ansätze](https://dokupdshandelsregistergroup5.readthedocs.io/en/latest/vorbereitung_verworfeneAns%C3%A4tze /erläutert.  

### Funktion: Dashboardsuche -> Backend siehe 'Definition der Suchfunktionen'

#### Anwendungsfall
Um an die gewünschten Informationen aus den Daten zu kommen, ist es notwendig, dass der User nach einer Organisation oder nach einer Person suchen kann. Im Idealfall werden Personen oder Organisationen dem User angezeigt, die semantische Ähnlichkeiten zur eingegebenen Sucheingabe besitzen. Somit hilft es dem User, seine gewünschte Suchanfrage zu finden.

#### Umsetzung
* Im Frontend wählt der User mithilfe einer Radioumgebung zuerst aus, ob er ein Unternehmen oder eine Person suchen möchte.
* Danach muss er mithilfe einer Sliceumgebung auswählen, wie viele Vorschläge angezeigt werden sollen. 
* Im nächsten Schritt wird der Suchbegriff im Textfeld eingeben. Die Suchfunktion sucht nun die ähnlichen Begriffe heraus und gibt diese automatisch im Dropdown-Menü weiter. Je nachdem, ob eine Person oder ein Unternehmen gesucht werden soll, gibt die Funktion verschieden Informationen zurück, damit der User die gewünschte Person oder das gewünschte Unternehmen auswählen kann. Bei einer Suchanfrage zum Unternehmen wird der Suchscore, der Name des Unternehmens sowie der Ort zurückgeben. Außerdem wird die ID der Organisation angezeigt, dies ist aber nur für die nachfolgenden Funktionen relevant.
* Der User kann auf den Button „Suchen“ klicken und orderid wird weitergeben. Bei einer Personensuche wird der Suchscore, der Name der Person, das Geburtsdatum, der Ort und die ID der Person zurückgeben. Die ID ist wiederum nur für die nachfolgenden Funktionen relevant. Der Code für diese Funktion ist unter 'Definition der Suchfunktion' zu finden.
#### Evaluation und Ausblick
* Die Suche nach Unternehmen oder nach Personen ist gut umgesetzt, bei Testeingaben wurden die gewünschten Unternehmen oder Personen angezeigt.
* Dennoch ist das UX Design im Frontend nicht einwandfrei.
* Es sind zu viele Schritte nötig, um die gewünschten Begriffe zu finden.
* Eine bessere Möglichkeit wäre ein Dropdown-Menü, wo man seine gewünschte Person oder Unternehmen eingeben kann, ohne zuvor dies zuvor auswählen zu müssen.
* Außerdem muss die ID mitgeben werden, da dies für Dashboard essenziell ist.
* Dennoch ist zu betonen, dass die Funktionalität der Sucheingabe gegeben ist.
  
### Funktion Dashboard 'Daten zur Person' siehe Definition Personendaten und Definition des Netzwerkgraphen
Nachdem eine Suchanfrage zur Person getätigt wurde, erscheint im unterem Tab 'Daten zur Person', die Informationen zur Person. Als Backend dienen die Definition der Personendaten und die Definition des Netzwerkgrafen.
#### Anwendungsfall
Die Informationen zu einer Person werden durch zwei Darstellungen abgebildet.
* Die Grundinformationen zur Person, wie Rolle, Name, Geburtsdatum, Ort und Unternehmen werden in einem Dataframe im Frontend angezeigt.
* Durch einen Netzwerkgrafen wird verbildlicht, in welchen Firmen die Person beteiligt ist.
#### Umsetzung
Nach der Sucheingaben werden den Funktionen der String der ausgewählten Dropdownzeile zurückgeben. In diesem String ist die ID der Person vorhanden. Diese ID wird extrahiert und weiterverarbeitet. Durch diese ID kann die Funktion die benötigten Daten aus den zuvor definierten Dataframes ziehen.
#### Evaluation und Ausblick
* Der Plot des Netzwerkgrafen ist nicht interaktive, es ist nicht möglich auf die Firmen zu klicken, um an die Informationen zum Unternehmen zu kommen.
* Außerdem ist der Plot sehr einfach gestaltet.
* In Zukunft sollte dieser interaktiv und professioneller gestaltet werden.
* Dennoch werden die relevanten Informationen dargestellt.
### Funktion: Darstellung Daten zum Unternehmen --> siehe Darstellung des Dashboards und Definition der Unternehmenshistorie
Übersicht mit allen relevanten Information zu einer ausgewählten Firma inklusive Ereignisse, klassifizierten Branchenbezeichnungen. Backend: Darstellung des Dashboards und Definition der Unternehmenshistorie.
#### Anwendungsfall
Um eine möglichst großen Überblick über die Informationen eines Unternehmens zu erlangen, werden diese unterschiedlich dargestellt. Zuerst werden die Grundinformationen zum Unternehmen angezeigt, wie Name, Anschrift etc. Danach wird die Branche des Unternehmens angezeigt. Des Weiteren werden die Daten der beteiligten Personen, die Bilanzdaten und der Geschäftszweck als jeweils als einzelne Dataframes angezeigt. Danach werden in einem Row die Daten zur Unternehmenshistorie sowie der Plot der Firmengeschichte dargestellt. Zum Schluss werden Firmen angezeigt, die in der gleichen Branche tätig sind.
#### Umsetzung
Wie zuvor wird hier durch die Dropdown-Auswahl ein String zurückgeben, der die Unternehmens-ID beinhaltet. Diese ID extrahieren die einzelnen Definitionen und können diese wiederum als Schlüssel verwenden, um an die Informationen zu kommen. Hierzu werden wieder einzelnen Dataframes als Datengrundlage gebraucht.
Diese sind: 
* all_companies_branchen_desc_key_coordinates_names_fulltext_oneline.csv
* merged_un_roles_personspd.csv
* DataFrame_Changes.csv
* Bilanzen.csv


### Funktion: Suche nach Umkreis 
Es lassen sich Unternehmen aus dem Handelsregister nach Umkreis suchen und werden in einer interaktiven Karte ausgegeben.
#### Anwendungsfall 
Firmen im Umkreis eines beliebigen Ortes suchen. Dabei soll es egal sein. 
#### Umsetzung
1. Im Vorfeld: Berechnung und Speichern der Koordinaten im Vorfeld mit GeoPy anhand Adresse, Postleitzahl und Stadt.
2. Sucheingabe wird mit GeoPY in Koordinaten umgewandte und die Distanzen zu den berechneten Koordinaten gefunden.
3. Die Suchergebnisse werden als interaktive Karte dargestellt. Der Unternehmensname erscheint als Mouse-Over. 
Darüber hinaus: 
Um die Rechenzeit zu optimieren wurde in die Umkreissuche ein vorgelagerter PLZ Abgleich eingerichtet. Dadurch reduziert sich die Anzahl der zu treffenden Vergleiche und die Rechenzeit bei Anfragen unter 100km Umkreis kann um circa 30 % verbessert werden. Ist der Suchradius unter 150 km, werden nur Firmen für den Vergleich betrachtet, die in potentiell erreichbaren PLZ-Gebieten liegen.
#### Evaluation
Für circa 96 Prozent aller Firmen konnten die Koordinaten ermittelt werden. Für knapp 500 Unternehmen konnten sich aufgrund veralteter bzw falsch angegebenen Adressen keine Koordinaten ermittelt werde. Die im Handelsregister angegebenen stimmt nicht mit der Adresse in GeoPy (bzw. auch auf Google Maps) überein und lässt sich nicht ermitteln. Beispiel für nicht-konvertierbare Daten. *Am Salzufer 8,Berlin* (Handelsregister) anstatt *Salzufer 8, Berlin* in Maps. 


## Dateien

### OCR.csv
Diese CSV-Datei repräsentiert folgendes Dataframe *bild ocr*
In "content" sind hierbei die Inhalte aller extrahierten TIF-Dateien enthalten. Die Datei stammt aus dem Notebook 

### all_companies_branchen_desc_key_coordinates_names_fulltext_oneline.csv
Diese CSV-Datei enthält zu jeder Firma die angereicherten Informationen, die zu Darstellung im Dashboard und für den Chatbot benötigt wird. Für jede der 10.000 Firmen sind alle verfügbaren Informationen in insgesamt 27 Spalten angehängt z.B Koordinaten, Branchen, Namen und Rollen,...
Die letzte Spalte beinhaltet alle Informationen als aufbereiteter String und wird für den Chatbot benötigt.
Die Datei ist das Ergebnis aus verschiedenen Notebooks u.A.  *Chatbot.ipybn*, *xml_to_dataframe.ipynb*, *umkreissuche.ipynb*  oder *branche_bestimmen_zero_shot_classification.ipynb*. Diese Datei wird u.A für die Dashboard-Darstellung und Suchfunktionen und Klassifikationen verwendet.

### klassifikationen-wz-2008.csv
Alle Branchenbezeichnungen auf den verschiedenen Ebenen nach WZ2008-Standard sind hier inklusive dem Branchencode enthalten. Dient als Basis zur den verschiedenen Branchenbestimmungen (nlp-similarity und zero-shot-classification Ansatz)
### merged_un_roles_personspd.csv
Hier sind die Unternehmensdaten, die Daten zur Person, sowie die Daten zu den Rollen in den Unternehmen gespeichert.
### DataFrame_Changes.csv
Hier sind die verschiedene Registerbekanntmachen gespeichert. Unter anderem die Art der Bekanntmachung, das Datum, sowie der Text der die genaue Information zur Bekanntmachung beinhaltet
### Bilanzen.csv
Die relevanten Bilanzdaten wie Anlagevermögen, Umlaufvermögen, Bilanzsumme, Gewinn/Verlust, etc. sind hier abgespeichert

### temp.png
Zwischengespeichertes Netzwerkdiagramm-Plot

### temp1.png
Zwischengespeicherte Unternehmenshistorie-Plot

## empty_output.png
Für Chatbot-Darstellung benötigt, wenn kein Image-Output


