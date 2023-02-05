# App

In diesem Notebook sind die finalen Anwendungen zusammengefügt. Die Funktionalitäten basieren auf die aufbereiteten CSV-Dateien, die für die Frontend-Funktionalitäten verwendet werden. Das Notebook ist unabhängig von den anderen Notebooks ausführbar. 
Nachfolgend werden die Funktionalitäten der App, sowie deren Umsetzung und Evaluation beschrieben. 
Datenextraktion, -aufbereitung und die Vorbereitung der Einzelfunktionen finden nicht in diesem Notebook statt, sondern werden in Abschnitt aufgeführt. 

## Notebook

### Funktion: Dateisuche in TIF-Dateien
Die im Notebook "Reading TIF-Files by OCR" in [Vorbereitung & verworfener Code](#Vorbereitung-&-verworfener-Code) ausgelesenen Informationen werden hier verwendet um heraus zu finden, ob in den TIF-Dateien noch zusätzliche Informationen zu einem Unternehmen verfügbar sind. Wenn dies der Fall ist, kann die Datei mit einem Klick heruntergeladen und die Information ausgelesen werden.

### Funktion: Branchenklassifikation WZ-2008

Anhand einer Freitexteingabe können die Firmen in die offiziell WZ-2008 Branchenlandschaft eingeordnet werden. Entsprechend der verschiedener Granularitäten (Abschnitt, Branche, Sub-, Sub-Sub-, Sub-Sub-Sub-Branche) werden Vorschläge inklusive der WZ2008-Codes für eine Einordnung geliefert. Genauere Erklärung,  Vorgehensweise und Auswertung in [Vorbereitung & verworfener Code](#Vorbereitung-&-verworfener-Code). 

### Funktion: Q-A-Chatbot

Dem Chatbot können beliebe Fragen zu Unternehmen, Personen oder sonstiges (z.B. Orte/Regionen) gefragt werden. Die Funktionalität basiert auf einer Kombination aus Named Entity Recognition und einer extractive Q-A-Modell und wird genauer im Notebook **chatbot** in Abschnitt [Vorbereitung & verworfener Code](#Vorbereitung-&-verworfener-Code) erläutert.  

### Funktion: Suchfunktionen

Mit dieser Funktion lassen sich Unternehmen lassen sich auch aufgrund ähnlicher Suchanfragen finden.

### Funktion: Suche nach Umkreis 

Es lassen sich Unternehmen aus dem Handelsregister nach Umkreis suchen und werden in einer interaktiven Karte ausgegeben.

### Funktion: Firmen-Netzwerk Graph


### Funktion: Darstellung Firmendetails

## Dateien

### OCR.csv
Diese CSV-Datei repräsentiert folgendes Dataframe "bild ocr"

In "content" sind hierbei die Inhalte aller extrahierten TIF-Dateien enthalten. Die Satei stammt aus dem Notebook 

### ....csv
Inhalt der CSV... stammmt aus Notebook "Reading TIF-Files by OCR" in "VorbereitungVerworfenerCode/Vorbereitung"

### ....csv
Inhalt der CSV... stammmt aus Notebook X