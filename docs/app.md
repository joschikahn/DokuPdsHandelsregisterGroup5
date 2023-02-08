# App

In diesem Notebook sind die finalen Anwendungen zusammengefügt. Die Funktionalitäten basieren auf die aufbereiteten CSV-Dateien, die für die Frontend-Funktionalitäten verwendet werden. Das Notebook ist unabhängig von den anderen Notebooks ausführbar. 
Nachfolgend werden die Funktionalitäten der App, sowie deren Umsetzung und Evaluation beschrieben. 
Datenextraktion, -aufbereitung und die Vorbereitung der Einzelfunktionen sind nicht in diesem Notebook enthalten, sondern werden unter Abschnitt [Vorbereitung und verworfene Ansätze](https://dokupdshandelsregistergroup5.readthedocs.io/en/latest/vorbereitung_verworfeneAns%C3%A4tze) durchgeführt und ausführlicher dokumentiert. 

## Notebook

### Funktion: Dateisuche in TIF-Dateien
Die im Notebook *Reading TIF-Files by OCR* in [Vorbereitung & verworfener Code](#Vorbereitung-&-verworfener-Code) ausgelesenen Informationen werden hier verwendet um heraus zu finden, ob in den TIF-Dateien noch zusätzliche Informationen zu einem Unternehmen verfügbar sind. Wenn dies der Fall ist, kann die Datei mit einem Klick heruntergeladen und die Information ausgelesen werden.

### Funktion: Branchenklassifikation WZ-2008

Anhand einer Freitexteingabe können die Firmen in die offiziell WZ-2008 Branchenlandschaft eingeordnet werden. Entsprechend der verschiedener Granularität (Abschnitt, Branche, Sub-, Sub-Sub-, Sub-Sub-Sub-Branche) werden Vorschläge inklusive der WZ2008-Codes für eine Einordnung geliefert. Genauere Erklärung,  Vorgehensweise und Auswertung in [Vorbereitung und verworfene Ansätze](https://dokupdshandelsregistergroup5.readthedocs.io/en/latest/vorbereitung_verworfeneAns%C3%A4tze).


### Funktion: Q-A-Chatbot

Dem Chatbot können beliebe Fragen zu Unternehmen, Personen oder sonstiges (z.B. Orte/Regionen) gefragt werden. Die Funktionalität basiert auf einer Kombination aus Named Entity Recognition und einer extractive Q-A-Model und wird genauer im Notebook *chatbot.ipynb* in Abschnitt [Vorbereitung und verworfene Ansätze](https://dokupdshandelsregistergroup5.readthedocs.io/en/latest/vorbereitung_verworfeneAns%C3%A4tze /erläutert.  

### Funktion: Dashboardsuche -> Backend siehe 'Definition der Suchfunktionen'

#### Anwedungsfall
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
#### Eevaluation und Ausblick
* Der Plot des Netzwerkgrafen ist nicht interaktive, es ist nicht möglich auf die Firmen zu klicken, um an die Informationen zum Unternehmen zu kommen.
* Außerdem ist der Plot sehr einfach gestaltet.
* In Zukunft sollte dieser interaktiv und professioneller gestaltet werden.
* Dennoch werden die relevanten Informationen dargestellt.
### Funktion: Darstellung Daten zum Unternehmen --> siehe Darstellung des Dashboards und Definition der Unternehmenshistorie
Übersicht mit allen relevanten Information zu einer ausgewählten Firma inklusive Ereignisse, klassifizierten Branchenbezeichnungen. Backend: Darstellung des Dashboards und Definition der Unternehmenshistorie.
#### Anwendungsfall
Um eine möglichst großen Überblick über die Informationen eines Unternehmens zu erlangen, werden diese unterschiedlich dargestellt. Zuerst werden die Grundinformationen zum Unternehmen angezeigt, wie Name, Anschrift etc. Danach wird die Branche des Unternehmens angezeigt. Des Weiteren werden die Daten der beteiligten Personen, die Bilanzdaten und der Geschäftszweck als jeweils als einzelne Dataframes angezeigt. Danach werden in einem Row die Daten zur Unternehmenshistorie sowie der Plot der Firmengeschichte dargestellt. Zum Schluss werden Firmen angezeigt, die in der gleichen Branche tätig sind.
#### Umsetzung
Wie zuvor wird hier durch die Dropdownauswahl ein String zurückgeben, der die Unternehmens-ID beinhaltet. Diese ID extrahieren die einzelnen Definitionen und können diese wiederum als Schlüssel verwenden, um an die Informationen zu kommen. Hierzu werden wieder einzelnen Dataframes als Datengrundlage gebraucht.
Diese sind: 
* all_companies_branchen_desc_key_coordinates_names_fulltext_oneline.csv
* merged_un_roles_personspd.csv
* DataFrame_Changes.csv
* Bilanzen.csv


### Funktion: Suche nach Umkreis 

Es lassen sich Unternehmen aus dem Handelsregister nach Umkreis suchen und werden in einer interaktiven Karte ausgegeben. Zugrundes liegende Preprocessing und Funktionsweise wird genauer in Notebook Vorbereitung und Verworfenen Ansätze erläutert. 

### Funktion: Darstellung Firmendetails

Übersicht mit allen relevanten Information zu einer ausgewählten Firma inklusive Ereignisse, klassifizierten Branchenbezeichnungen. 

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


