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

### Funktion: Suchfunktionen

#### Anwedungsfall
Um an die gewünschten Informationen aus den Daten zu kommen, ist es notwendig, dass der User nach einer Organisation oder nach einer Person suchen kann. Im Idealfall werden Personen oder Organisationen dem User angezeigt, die semantische Ähnlichkeiten zur eingegeben Sucheingabe besitzen. Somit hilft es dem User seine gewünschte Suchanfrage zu finden.
#### Umsetzung
* Im Frontend wählt der User mit Hilfe einer Radioumgebung zuerst aus, ob er ein Unternehmen oder eine Person suchen möchte.
* Danach muss er mit Hilfe einer Sliceumgebung auswählen, wie viele Vorschläge angezeigt werden sollen. 
* Im nächstem Schritt, wird der Suchbegriff im Textfeld eingeben. Die Suchfunktion sucht nun die ähnliche Begriffe heraus und gibt diese automatisch im Dropdownmenü weiter. Je nachdem, ob eine Person oder ein Unternehmen gesucht werden soll, gibt die Funktion verschieden Informationen zurück, damit der User die gewünschte Person oder das gewünschte Unternehmen auswählen kann. Bei einer Suchanfrage zum Unternehmen wird der Suchscore, der Name des Unternehmen sowie der Ort zurückgeben. Außerdem wird die id der Organisation angezeigt, dies ist aber nur für die nachfolgenden Funktionen relevant.
* Der User kann nun auf dem Butoon Suchen klicken und orderid wird weitergeben. Bei einer Personensuche, wird der Suchscore, der Name der Person, das Geburtsdatum der Ort und die id der Person zurückgeben. Die id ist wiederum nur für die nachfolgenden Funktionen relevant. Der Code für diese Funktion ist unter 'Definition der Suchfunktion' zu finden.

### Funktion: Suche nach Umkreis 

Es lassen sich Unternehmen aus dem Handelsregister nach Umkreis suchen und werden in einer interaktiven Karte ausgegeben. Zugrundes liegende Preprocessing und Funktionsweise wird genauer in Notebook Vorbereitung und Verworfenen Ansätze erläutert. 

### Funktion: Netzwerk Graph

Eine Person wird gesucht und es werden seine Rollen und Beteiligungen an verschiedenen Firmen als Netzwerk-Graph angezeigt. Vorbereitung und Umsetzung genauer unter [Vorbereitung und verworfene Ansätze](https://dokupdshandelsregistergroup5.readthedocs.io/en/latest/vorbereitung_verworfeneAns%C3%A4tze) dokumentiert. 

### Funktion: Darstellung Firmendetails

Übersicht mit allen relevanten Information zu einer ausgewählten Firma inklusive Ereignisse, klassifizierten Branchenbezeichnungen. 

## Dateien

### OCR.csv
Diese CSV-Datei repräsentiert folgendes Dataframe *bild ocr*
In "content" sind hierbei die Inhalte aller extrahierten TIF-Dateien enthalten. Die Datei stammt aus dem Notebook 

### all_companies_branchen_desc_key_coordinates_names_fulltext_oneline.csv
Diese CSV-Datei enthält zu jeder Firma die angereicherten Informationen, die zu Darstellung im Dashboard und für den Chatbot benötigt wird. Für jede der 10.000 Firmen sind alle verfügbaren Informationen in insgesamt 27 Spalten angehängt (z.B Koordinaten, Branchen, Namen, Context-String für den Chatbot,...)

### klassifikationen-wz-2008.csv
Alle Branchenbezeichnungen auf den verschiedenen Ebenen nach WZ2008-Standard sind hier inklusive dem Branchencode enthalten. Dient als Basis zur den verschiedenen Branchenbestimmungen (nlp-similarity und zero-shot-classification Ansatz)
