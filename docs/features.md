# Features / Umsetzungen 

## Suchfunktionen 

Um Informationen zu Firmen finden zu können, ist es im ersten Schritt wichtig, die entsprechnedne Firma auch zu finden.
Um eine möglichst vielseitige Suche zu ermöglichen, haben wir veschriede implementiert, um die Firma zu finden. 

### Nach ähnlichen Sucheingaben suchen

Ist man sich nicht sicher, wie genau der Organisationsnamen lautet, kann man trotzdem die Firma finden. 

*Meyer Kältetechnik GmbH* oder *Mayer Kälte KG* ?
*Bauer* oder *Baur*? 
*Kapps Medizintechnik* oder *Kaps MedTech*?
Wie genau fängt die die *Dachdeckergesellschaft & CO KG* nochmals an? 

- Umsetzung: 

 Vergleich der zwischen Sucheingabe und dazu ähnlichen Organisationsnamen durch Fuzzywuzzy string Abgleich. 
 Die gewünschten x Ergebnisse mit höchsten Scores werden zurückgegeben. 

Im Notebook: suchfunktionen.ipynb

### Umkreissuche mit interactiver Karte 

- Anwendungsfall:
  -  Welche Unternehmen sind in der Nähe von Würzburg? 

- Umsetzung: 
  - Koordinaten mit GeoPy Library anhand Firmen Adresse, berechnet

## Branchenklassifikation nach offizieller Wirtschaftszweig-Norm (WZ2008)

## Branchenclustering nach TF-IDF-Vekoren (verworfen)


## Unternehmensverflechtungen darstellen

## Universal Chatbot  

## Download






