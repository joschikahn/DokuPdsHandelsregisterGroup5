# Frontend 
Das Softwaremodul DashboardFrontend besteht aus einem React Frontend. Somit stellt dieses Modul das Userinterface unseres Systems dar. Insgesamt werden in diesem Modul die visuellen Möglichkeiten für die Betrachtung der Daten, die Erstellung von Reports, die Userverwaltung und die Anpassung von Prognosen abgebildet.

Wir starten in der Ordnerstruktur
dashboardFrontend -> dashboard -> src

## Components
### Charts
In diesem Ordner sind die Components für die verschiedenen Diagramme hinterlegt. 

#### AcfandPacf.jsx
Logik und Darstellung der Prognose Diagramme auf der Prognose Seite.

---
##### `getData(data)`
Ruft die Datenreihen gefiltert nach Namen, Anfang und Ende ab.

- **Parameter:**
  - **data** (Object): Datenreihen des Modells.

<br>

#### AreaChart.jsx
Logik und Darstellung der Flächendiagramme.

---
##### `getData(data)`
Ruft die Datenreihen gefiltert nach Namen, Anfang und Ende ab.

- **Parameter:**
    - **data** (Object): Datenreihen des Modells.

<br>

#### BarChart.jsx
Logik und Darstellung der Balkendiagramme.

---
##### `getData(data)`
Ruft die Datenreihen gefiltert nach Namen, Anfang und Ende ab.

- **Parameter:**
    - **data** (Object): Datenreihen des Modells.

<br>

#### LineChart.jsx
Logik und Darstellung der Liniendiagramme.

---
##### `getData(data)`
Ruft die Datenreihen gefiltert nach Namen, Anfang und Ende ab.

- **Parameter:**
    - **data** (Object): Datenreihen des Modells.

<br>

#### ScatterChart.jsx
Logik und Darstellung der Streudiagramme.

---
##### `getData(data)`
Ruft die Datenreihen gefiltert nach Namen, Anfang und Ende ab.

- **Parameter:**
    - **data** (Object): Datenreihen des Modells.

<br>

### WizardSteps
#### Drop.jsx 
---
##### `getTables()`  
Ruft die Tabellennamen ab.      

---
##### `onFiltering(e)`  
Filtert die Dropdown-Einträge.

- **Parameter:**
    - **e (Object):** Suchanfrage.
    
---
##### `onClose()`
Aktualisieren und in den State einfügen.

<br>
   
#### StepOne.jsx
Auswahl des Titels und der Zeitreihe der zu erstellenden Kachel.

---
##### `goToStepTwo()`
Validierung und Übergang zu Schritt zwei.

<br>

#### StepTwo.jsx
Auswahl zwischen Diagramm-, Freitext- oder Kennzahl-Element.

---
##### `goToStepThree()`
Gehe zu Schritt drei und füge Datum zu ElementBody hinzu.

<br>

#### StepThree.jsx
Im dritten Schritt gibt es 3 Fälle:   
- Freitext: Text wird eingegeben und Wizard wird geschlossen
- Kennzahl: Kennzahl-Art wird ausgesucht und es geht zu Schritt 4
- Diagramm: Diagramm-Art wird ausgesucht und es geht zu Schritt 4

---
##### `goToStepFour()`
Gehe zu Schritt drei und füge Datum zu ElementBody hinzu.

---
##### `closeWizard()`
Wenn 'Text' gewählt wurde, wird der Wizard an dieser Stelle beendet.

---
##### `saveElements()`
Neue Elemente nach Texteingabe speichern.

<br>

#### StepFour.jsx
Im vierten Schritt werden die Datenreihen ausgesucht, Kurzbeschreibung beigefügt, Zeitfilter angepasst (optional) und entschieden, ob die Datenreihe prognostiziert werden soll.

---
##### `onBeforeRender()`
Renderfunktion für die Tooltip-Komponente.

---
##### `triggerRefresh()`
Tooltip nach Schließen des Dropdowns aktualisieren.

---
##### `changeFilterStatus(key, filter)`
Ändert das Date-Objekt für Start und Ende.

- **Parameter:**
    - **key** (Number): Aktuelle Position im Array.
    - **key** (Number): Markierung, wenn Anfang oder Ende geändert wird.
    
---
##### `getTables()`
Ruft alle Tabellennamen aus der Datenbank ab.

---
##### `addRow(key)`
Wird verwendet, nachdem der Benutzer auf der Schaltfläche 'add' geklickt hat, um eine neue Datenreihe hinzuzufügen.

- **Parameter:**
    - **key**(Number): Position.
    
---
##### `prognosisChecked(key)`
Ändert den Status der Prognose-Checkox.

- **Parameter:**
    - **key**(Integer): Status.


---
##### `closeStepWizard()`
Schließt den Assistenten und fügt Daten zum Elementbody hinzu.

---
##### `validated()`
Wird vor dem Speichern aufgerufen, um die Benutzereingaben zu überprüfen.

---
##### `saveElements()`
Neue Elemente speichern.

---
##### `deleteDataEntry(key)`
Löschen einer Zeitreihe.

- **Parameter:**
    - **key**(Integer): Zeitreihe.
<br>

#### StepFive.jsx
Letzter Schritt im StepWizard. Hier wird dem Element optional ein Textfeld hinzugefügt.
Ist das zu erstellende Element ein Diagramm, so wird hier zusätzlich die Achsenbeschriftung hinzugefügt.

---
##### `closeStepWizard()`
Schließt den Assistenten und fügt Daten zum Elementbody hinzu.

---
##### `validated()`
Wird vor dem Speichern aufgerufen, um die Benutzereingaben zu überprüfen.

---
##### `saveElements()`
Neue Elemente speichern.

<br>

### AddNewUser.jsx  
Legt neue Benutzer an.

---
#### `saveNewUser()`
Sendet den neuen Benutzer an das NodeJS Backend.

---
#### `validatedEmail()`
Validiert die E-Mail-Adresse. 

---
#### `validatedPw()`
Validiert das Passwort.

<br>

### AddNewAdminPage.jsx  
In diesem Component wird eine neue Admin Seite angelegt.

---
#### `saveNewPage()`
Sendet eine bestimmte Seite an das Backend und die Variablen werden geupdatet. 

---
#### `duplicate(siteName)`
In dieser Methode wird geprüft, ob schon eine Seite mit dem übergebenem Seitennamen existiert.

- **Parameter:**
    - **siteName** (String): Seitenname.
- **Returntyp:**
    - Bool
- **Returns:** 
    - Gibt zurück, ob eine Seite mit diesem Namen schon existiert.

<br>

### DeleteAdminPage.jsx
Startet den Löschvorgang von Adminseiten.

---
#### `deletePage ()`
Übergibt den Seitennamen, der zu löschenden Seite an das Backend und alle Variablen werden geupdatet.

<br>

### DeleteElementDialog.jsx
Startet den Löschvorgang von einer Kachel einer Adminseite.

---
#### `deleteElement()`
Übergibt eine zu löschende Kachel an das Backend und alle Variablen werden geupdatet.

<br>

### DeleteUser.jsx
Startet den Löschvorgang eines Nutzers.

---
#### `deleteUser()`
Übergibt einen zu löschenden Nutzer an das Backend und alle Variablen werden geupdatet.

<br>

### DropdownPrognosis.jsx
Enthält die Logik für die Dropdownliste der Zeitreihen auf der Prognose Seite.

---
#### `getTables()`
Liefert alle Tabellennamen zurück.

---
#### `onFiltering(e)`
Filtert die Dropdown-Einträge.

- **Parameter:**
    - **e:(Object)** Suchanfrage.

---
#### `onBeforeRender()`
Renderfunktion für die Tooltip-Komponente.

---
#### `onClose()`
Aktualisieren und in den State einfügen.

<br>

### EditAdminPageName.jsx
Ändert den Seitennamen.



---
#### `editPage(newName)`
Prüft, ob schon eine Seite mit dem übergebenem Seitennamen existiert.

- **Parameter:**
    - **newName** (String): neuer Seitenname

---
#### `duplicate(siteName)`
Prüft, ob schon eine Seite mit dem übergebenem Seitennamen existiert.

- **Parameter:**
    - **siteName** (String): Seitenname
- **Returntyp:**
    - Bool
- **Returns:** 
    - Gibt zurück, ob eine Seite mit diesem Namen schon existiert

<br>

### KPIContainer.jsx 
Design und Logik von Kennzahlen in einer Kachel.

---
#### `getData(data)`
Gibt alle Kennzahlen nach Namen, Start und Enddatum gefiltert zurück.


- **Parameter:**
    - **data** (Object[]): Metadaten aller Tabellen 
   
<br>

### LoginButton.jsx
Logik und Design des LoginButtons.

<br>

### LogoutButton.jsx
Logik und Design des LogoutButtons.

---
#### `logout()`
Meldet einen angemeldeten Nutzer ab.

<br>

### Navbar.jsx
Design der Navbar.

<br>

### Sidebar.jsx
Design und Interaktion der Sidebar.

---
#### `handleCloseSideBar ()`
Klappt die Sidebar ein.

---
#### `changeSite ()`
Wechselt die Ansicht des Dashboards auf eine übergebene Seite und aktualisiert die Elemente. 

- **Parameter:**
    - **siteName** (String): Seitenname 

---
#### `sideBarClick(siteName)`
Navigiert zur übergebenen Seite.

- **Parameter:**
    - **siteName** (String): Seitenname 

<br>

### Text.jsx
Liefert den Text zurück.

<br>

### Wizard.jsx
Dialog zum Erstellen und Bearbeiten von Kacheln. Ruft Components aus WizardSteps auf.

---
#### `closeTheWizard()`
Schließt den Dialog und aktualisiert die Elemente.

<br>

## Contexts
### contextProvider.js
Aktualisiert Sidebarelemente und Kacheln.

---
#### `updateSidebarElements()`
Aktualisiert die Seiten der der Sidebar.


---
#### `updateAdminElements(siteName)`
Ruft die Daten der einzelnen Kacheln der zu ladenden Seite ab.

- **Parameter:**
    - **siteName**(String):  Name der zu ladenden Seite.

<br>

## Pages
Enthält die Components für die einzelnen Seiten in der Navbar und des Logins.

### Admin.jsx
Logik und Design der Adminseite.

---
#### `checkAdminSite(body)`
Wählt die erste Seite aus. Ist keine Seite vorhanden, wird der Nutzer dazu aufgefordert eine neue Seite zu erstellen.

- **Parameter:**
    - **body** (Object): Alle Seiten. 
    
---
#### `addNewElement()`
Öffnet den Dialog zum Erstellen einer Kachel.

---
#### `edit(item, key)`
Öffnet den Dialog zum Bearbeiten einer Kachel.

- **Parameter:**
    - **item** (Object): Die zu bearbeitende Kachel.
    - **key** (*): Position.  

<br>

### CustomPrognosis.jsx
Ermöglicht es Prognosen detaillierter zu betrachten und optional dazugehörige Parameter manuell anzupassen.

---
#### `getModelInfos(name)`
Fordert Modellinformationen an.

- **Parameter:**
    - **name** (String): Name des Modells.

---
#### `setSelectedValue(name, timeInterval)()`
Aktualisiert States, wenn Daten ausgewählt wurden.

- **Parameter:**
    - **name** (String):  Aus Dropdown ausgewähltes Modell.
    - **timeInterval** (String): Timeinterval (Monat, Quartal, Jahr).  
    
---
#### `calculateNewModel()`
Gibt die Daten an das Backend weiter und wartet, bis Modell berechnet wurde.

---
#### `saveModel()`
Speichert das neu erstellte Model.

<br>

### Dashboard.jsx
Zeigt die erstellten Kacheln.

---
#### `handleDownloadPdf ()`
Exportiert die Dashboard Seite als PDF.


<br>

### Login.jsx
Design und Logik der Anmelde Seite.

---
#### `sendLoginRequest()`
Sendet die Client Daten an das Backend.

---
#### `validated()`
Überprüft das Format der E-Mail-Adresse.

- **Returntyp:**
    - Bool
- **Returns:**
    - Gibt zurück, ob das Format der E-Mail-Adresse gültig ist.
    
---
#### `closeDialog()`
Schließt den Dialog und aktualisiert entsprechende Elemente.

<br>

### Useradministration.jsx
Verwaltung der Nutzer.

---
#### `updateUsers ()`
Aktualisiert die Nutzerliste und schließt den "Nutzer löschen" Dialog.

---
#### `closeWindow ()`
Aktualisert die Nutzerliste und schließt den "Nutzer hinzufügen" Dialog

---
#### `getUsers()`
Ruft alle Nutzer aus der Datenbank ab.




