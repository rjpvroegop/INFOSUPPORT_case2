##Case 2 – GarageManagementSysteem


###Requirements 

####Functional Requirements 
  
1. Een auto moet voor onderhoud aangeboden kunnen worden. De onderhoudsopdracht moet dan, samen met de overige klantinformatie, in het systeem gezet worden.
2. Een monteur moet aan kunnen geven met een nieuwe opdracht te beginnen 
3. Een monteur moet aan kunnen geven klaar te zijn. Indien het een APK-keuring betreft, wordt er dan een automatisch bericht naar het RDW gestuurd. Dat kan betekenen dat de auto uitgekozen wordt voor een steekproef van het RDW. 
4. Een monteur moet de auto klaar kunnen melden (na de steekproef) 
5. De receptioniste moet klantgegevens kunnen wijzigen 
6. Er moet overzicht zijn van de status van de auto’s die momenteel in onderhoud zijn. 
7. De receptioniste moet een klantoverzicht kunnen krijgen
8. De receptioniste moet een overzicht van auto’s kunnen krijgen 
9. De receptioniste moet de lijst met automerken en types kunnen bijwerken 
10. De receptioniste moet een overzicht van reparaties kunnen krijgen 

####Non-functional Requirements 

1. De communicatie met het RDW dient te worden gelogd in een database 
2. Alle technische fouten dienen worden gelogd in een log-file 
3. Er moet een backup-strategie voor de database(s) komen 
4. De applicatie moet door de MITS in beheer genomen worden en moet dus voldoen aan de Endeavour-richtlijnen m.b.t. code- en teststandaarden 
5. De applicatie hoeft (nog) niet beveiligd te zijn, maar als er nog tijd over is, dan is dat wel fijn

---

Er is gekozen voor een ruim opgezette SOA-Architectuur. Dit is pas de eerste release van de
applicatie. We verwachten dat het systeem in de toekomst veel uitgebreider gaat worden. 

<table>
  <tr>
    <td>FEGarageManagementSysteem</td>
    <td>ISRijksdienstWegverkeer</td>
  </tr>
  <tr>
  <td colspan="2" style="text-align:center;">Service Bus</td>
  </tr>
  <tr>
    <td>PcSOnderhoud</td>
    <td>BSVoertuigEnKlantbeheer</td>
  </tr>
</table>

De **FEGarageManagementSysteem** implementeert het User Interface voor zowel de receptioniste als
de monteur. Op het hoofdscherm staat een menulijstje met taken (use cases).

De **PcSOnderhoud** implementeert het bedrijfsproces van het doen van onderhoud (aanmelden,
onderhoud starten, evt. contact opnemen met het RDW, voertuig klaarmelden). In deze service moet
worden bewaard: de onderhoudsopdracht en de status van het voertuig dat in onderhoud is.

De **BSVoertuigEnKlantbeheer** beheert de primaire data van het garagebedrijf: de klantgegevens, de
autogegevens en de onderhoudsgeschiedenis (niet de opdracht, maar wel de uitgevoerde
wertkzaamheden).

De **ISRijksdienstWegverkeer** regelt de communicatie met het RDW.


In de toekomst komt klantinformatie mogelijk in een CRM-pakket te zitten. Het zou fijn zijn als de
**BSVoertuigEnKlantbeheer** in de toekomst gesplitst kan worden in **BSKlantbeheer** en
**BSVoertuigbeheer**.
