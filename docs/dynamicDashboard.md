# Dynamic Dashboard
Das Softwaremodul DynamicDashboard setzt sich aus einem NodeJS Server und einer MongoDB zusammen. Die Hauptaufgaben des Moduls sind die Verwaltung von Zeitreihen, das speichern von Veränderung im Frontend(z. B. Anlegen einer neuen Seite) und das steuern der Login und Authentifizierungsprozesse. Unser NodeJS Modul nutzt das express Framework, welches die Erstellung von Webschnittstellen ermöglicht. Für die Authentifizierung haben wir auf ein Verfahren gesetzt, welches an die Oauth Prozedur angelehnt ist und folgendermaßen funktioniert: Ein User muss für den Login seine Anmeldedaten an den Backendserver übertragen. Dieser antwortet entweder mit einer Fehlermeldung oder aber mit dem erstellen eines httpOnly-Cookies, welcher nicht durch clientseitiges JS abgegriffen werden kann. Durch den Cookie bleibt der User für die Dauer seiner Session somit authentifiziert.

## API Dokumentation
Wir verwenden für die Dokumentation der API Swagger. Wenn die Instanz läuft, kann diese Doku unter _http://localhost:3000/docs/#/_ aufgerufen werden.

## Helper
### auth.js
Dieses Modul verwaltet die Authentifizierung des Logins und die Validierung der verschiedenen User.

---
#### `signup(req,res)`
Diese Methode verwaltet den Prozess für die Erstellung eines Nutzers.

- **Parameter:**
    - **req** (Object):  request body 
    - **res** (Object):  response body

---
#### `signin(req,res) `
In dieser Methode wird der Login Prozess verwaltet.

- **Parameter:**
    - **req** (Object):  request body  
    - **res** (Object):  response body
---

#### `proofToken(req) `
Diese Methode validiert den Token eines Nutzers.

- **Parameter:**
    - **req** (Object): request body 

- **Returntype:** 
    - bool

<br>

### dateParser.js
In diesem Modul wird das Format des Datums angepasst.

---
#### `convertMonthDataToIsoFormat(dataset)`
Diese Methode bekommt ein Datenset mit invaliden Monatsdaten übergeben, um diese anschließend in ein ISO Format zu konvertieren und zurückzugeben.

- **Parameter:**
    - **dataset** (Object): Zeitreihen
- **Returntyp:**
    - dataset 
- **Returns:** 
    - konvertierter Datensatz

---
#### `convertQuarterDataToIsoFormat(dataset)`
Diese Methode bekommt ein Datenset mit invaliden Quartalsdaten übergeben, um diese anschließend in ein ISO Format zu konvertieren und zurückzugeben.

- **Parameter:**
    - **dataset** (Object): Zeitreihen
- **Returntyp:**
    - dataset 
- **Returns:** 
    - konvertierter Datensatz

---
#### `convertYearDataToIsoFormat(dataset)`
Diese Methode bekommt ein Datenset mit invaliden Jahresdaten übergeben, um diese anschließend in ein ISO Format zu konvertieren und zurückzugeben.

- **Parameter:**
    - **dataset** (Object): Zeitreihe
- **Returntyp:**
    - dataset 
- **Returns:** 
    - konvertierter Datensatz

<br>

### kpiCalculation.js  
---
#### `kpiCalculation(req,entry)`
Diese Methode berechnet für eine übergebene Zeitreihe eine Kennzahl, die entweder Summe, Mittelwert, Median, Höchst- oder Tiefstwert sein kann.

- **Parameter:**
    - **req** (Object): Request Body
    - **entry** (Object): Zeitreihe
- **Returntyp:**
    - double 
- **Returns:** 
    - berechnete Kennzahl

<br>

## Middlewares    
Spezifische Middleware Komponenten für die Authentifizierung und Erstellung von Nutzern.

### authJwt.js   
In diesem Modul wird geprüft, ob ein Nutzer die Adminrechte besitzt und autorisiert ist.

---
#### `verifyToken(req,res,next)`
Prüft ob ein Nutzer autorisiert ist und gibt falls nicht eine entsprechende Meldung aus.

- **Parameter:**
    - **req** (Object): Request Body
    - **res** (Object): Response Body
    - **next** (Function): express.NextFunction
---
#### `isAdmin(req, res, next)`
Prüft ob ein Nutzer über die Adminrechte verfügt und gibt falls nicht eine entsprechende Meldung aus.

- **Parameter:**
    - **req** (Object): Request Body
    - **res** (Object): Response Body
    - **next** (Function): express.NextFunction

<br>

### verifySignUp.js     
In diesem Modul wird beim Erstellen eines neuen Nutzers geprüft, ob die angegebene E-Mail-Adresse schon im System existiert.

---
#### `checkDuplicateEmail(req,res,next)`
Diese Methode prüft, ob eine E-Mail-Adresse schon im System existiert.

- **Parameter:**
    - **req** (Object): Request Body
    - **res** (Object): Response Body
    - **next** (Function): express.NextFunction

<br>

## Mongoose  
Enthält alle Schemas Definitionen für die MongoDB.
### Role.js  
Beschreibt das Schema der Rollen für die MongoDB.
### Sites.js  
Beschreibt das Schema der Seiten für die MongoDB.
### Table.js  
Beschreibt das Schema der Tabellen für die MongoDB.
### User.js   
Beschreibt das Schema der Nutzer für die MongoDB.

<br>

## Router  

### Routes  

#### auth.js   
Konfiguration der Schnittstellen für die Authentifizierung.

---
##### `POST signUp`  
Diese Methode erstellt einen neuen Nutzer.

- **Parameter:**
    - **req** (Object): Request Body
    - **res** (Object): Response Body
---
##### `POST signIn`  
Erstellt clientseitig einen Cookie, falls der User autorisiert ist.

- **Parameter:**
    - **req** (Object): Request Body
    - **res** (Object): Response Body

<br>

#### db.js
Konfiguration der Schnittstellen für die Dateninteraktion.

---
##### `GET isAuth`  
Prüft, ob der Nutzer autorisiert ist.

- **Parameter:**
    - **req** (Object): Request Body
    - **res** (Object): Response Body

---
##### `GET getEntries`  
Gibt alle Tabellen zurück.

- **Parameter:**
    - **req** (Object): Request Body
    - **res** (Object): Response Body

---
##### `GET getUsers`  
Gibt alle Nutzer zurück.

- **Parameter:**
    - **req** (Object): Request Body
    - **res** (Object): Response Body

---
##### `GET deleteUser`  
Löscht einen übergebenen Nutzer.

- **Parameter:**
    - **req** (Object): Request Body
    - **res** (Object): Response Body

---
##### `GET getEntry`  
Liefert eine Zeitreihe oder eine Kennzahl zu einem bestimmten Tabellennamen zurück.

- **Parameter:**
    - **req** (Object): Request Body
    - **res** (Object): Response Body

---
##### `GET getLastTimestamp`  
Liefert den jüngsten Zeitstempel einer Tabelle zu einem bestimmten Tabellennamen zurück.

- **Parameter:**
    - **req** (Object): Request Body
    - **res** (Object): Response Body

---
##### `GET getAllTableNames`  
Liefert die Tabellennamen aller Tabellen zurück.

- **Parameter:**
    - **req** (Object): Request Body
    - **res** (Object): Response Body

---
##### `GET getTableNamesByTimeRange`  
Liefert die Tabellennamen von allen Tabellen nach Zeitraum (Monat, Quartal, Jahr) gefiltert zurück.

- **Parameter:**
    - **req** (Object): Request Body
    - **res** (Object): Response Body

---
##### `POST insertEntry`  
Let eine Zeitreihe und ihre Parameter an.

- **Parameter:**
    - **req** (Object): Request Body
    - **res** (Object): Response Body

---
##### `POST addSite`  
Erstellt eine Seite an.

- **Parameter:**
    - **req** (Object): Request Body
    - **res** (Object): Response Body

---
##### `GET getSite`  
Gibt alle Seiten zurück. Falls ein Seitenname übergeben wurde, nur eine bestimmte Seite.

- **Parameter:**
    - **req** (Object): Request Body
    - **res** (Object): Response Body

---
##### `GET getSite`  
Gibt alle Seiten zurück. Falls ein Seitenname übergeben wurde, nur eine bestimmte Seite.

- **Parameter:**
    - **req** (Object): Request Body
    - **res** (Object): Response Body

---
##### `GET editSite`  
Ersetzt bisherigen Seitenname einer Seite mit einem neuen Seitenname.

- **Parameter:**
    - **req** (Object): Request Body
    - **res** (Object): Response Body

---
##### `GET deleteSite`  
Löscht alle Seiten. Falls ein Seitenname übergeben wurde, wird nur die letzte Seite gelöscht.

- **Parameter:**
    - **req** (Object): Request Body
    - **res** (Object): Response Body

<br>

### index.js  
Deckt allgemeine Middleware Funktionen ab.

<br>

### app.js
Initialer Start des Servers und Einstellung aller notwendigen Parameter.


