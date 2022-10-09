# Acceptatie Plan SSI

### HBO-ICT SE Jaar 4 Groep 5



## 1 Inleiding
Dit Acceptatie Plan verschaft een meetbare basis voor de te accepteren werkproducten. Het bevat een lijst met meetbare acceptatiecriteria die invulling geven aan niet-functionele en Use Case overstijgende eisen. 



## 2 Acceptatiecriteria
???
### 2.1 Performance
|                                       | 1 | 2 |
| ------------------------------------- | --- | --- |
| **Omschrijving**                      | sdfggfdsgfdsgdfs| gfsdgdfgsgdfs |
| **Eigenaar**                          |  |  |
| **Doel, streefwaarde en toleranties** |  |  |
| **Meetmethode**                       |  |  |
| **Planning**                          |  |  |
| **Corrigerende acties**               |  |  |

### 2.2 Beheerbaarheid
#### 2.2.1 onderhoudbaarheid van de code
- unittests moeten worden uitgevoerd door een teststraat
- de documentatie moet zodanig duidelijk zijn dat dit te begrijpen is voor iemand die geen/weinig technische kennis heeft
#### 2.2.2 logging
???
#### 2.2.3 instelmogelijkheden
???
#### 2.2.4 oppakken va parameters en contentwijzigingen
???

### 2.3 Betrouwbaarheid
#### 2.3.1 transactie- en rollbackmechanismen
???
#### 2.3.2 herstartbaarheid
???
#### 2.3.3 herstelmogelijkheden
???
#### 2.3.4 het omgaan met database locking
???
#### 2.3.5 validatiemechanismen
- Een verifier moet kunnen controleren:
  * zijn alle vereiste VC's aanwezig
  * wie is is de uitgever van de VC, is dit een betrouwbare uitgever en is het gegarandeerd deze uitgever
  * is het gegarandeerd dat de VC betrekking heeft op de houder en niet iemand anders
  * is het gegarandeerd dat de VC niet is aangepast sinds het is uitgegeven
  * is de VC nog geldig
- Een gebruiker moet de status (in behandeling, gevalideerd) van zijn aanvragen bij een uitgever kunnen zien in zijn wallet

### 2.4 Beveiliging
- p2p berichtenverkeer moet beveiligd zijn wat betreft:
  * privacy
  * integriteit
  * authenticiteit
- De wallet bevat een DID, een private sleutel en een publieke sleutel. De wallet bevat verder de VC's die eigendom zijn van de houder
- Om de wallet te kunnen gebruiker moet de gebruiker eerst inloggen met een gebruikersnaam en wachtwoord
- De gebruiker kan met zijn wallet op basis van de private sleutel een publieke sleutel en ID genereren
- Wanneer de private key in de wallet wordt opgeslagen, dan moet de key worden beveiligd met encryptie
- De private key moet worden beschermd met een 'seed recovery phrase' conform BIP39, een 'nep-zin' opgebouwd uit gewone woorden
- De wallet moet een veilige mogelijkheid voor backup en recovery bevatten
### 2.5 Funcitonaliteit
**[!!!voorbeeld van rupopmaat!!!]** De functionaliteit zal worden beoordeeld op basis van goedgekeurde Use Case Specifications en een goedgekeurde Navigation Map.

### 2.6 Gebruikersvriendelijkheid
- De mobiele web aplicatie moet schaalbaar zijn voor alle 'moderne' telefoons
- De gebruiker moet makkelijk kunnen wisselen van rol als holder en verifier
- De gebruiker kan verder met zijn wallet:
  * beveiligde p2p verbindingen opzetten met andere partijen
  * een VC aanvragen bij een uitgever
  * een verzoek voor een of meer VC's ontvangen van een verifier
  * een bewijs (VC) tonen aan een verifier

### 2.7 Standaards
???

### 2.8 Documentatie
???



-----------------



**Dit zijn eisen waarvan ik niet zo goed weet onder welk kopje ik ze moet plaatsen**

- er wordt gebruik gemaakt van de volgende vier use cases:
  * Het kopen van alcohol (drank) in de supermarkt. De supermarkt wil dat je je leeftijd aantoont
    * uitgever: overheid (gemeente);
    * houder: klant;
    * verifier: kassière supermarkt.
  * Het aanvragen van een hypotheek. De hypotheekverstrekker wil een verklaring van de overheid m.b.t. je identiteit en een werkgeversverklaring m.b.t. je inkomen
    * uitgevers: overheid (gemeente), werkgever;
    * houder: aanvrager;
    * verifier: hypotheekverstrekker.
  * Het tonen van ID en diploma's bij een sollicitatie. De (potentiële) werkgever wil een diploma van je middelbare school en van je hbo-opleiding zien
    * uitgevers: middelbare school, hbo-instelling;
    * houder: sollicitant;
    * verifier: werkgever.
  * het huren van een auto: de verhuurder wil een ID en een rijbewijs zien.
    * uitgevers: overheid (gemeente), overheid (RDW);
    * houder: huurder;
    * verifier: verhuurbedrijf.

- er moet een request/response protocol voor de drie partijen worden ontworpen

- alle berichten moeten gebaseerd zijn op het JSON-formaat

- Er moet een datastructuur worden ontworpen gebaseerd op JSON. Deze structuur moet voor alle partijen:
  * duidelijk maken welke VC's vereist worden
  * hoe een VC kan worden aangevraagd
  * hoe een VC kan worden uitgegeven
  * hoe een VC kan worden gepresenteerd aan de verifier

- een VC zal minimaal moeten bevatten:
  * een uniek ID van de VC
  * het type VC
  * de ID van de uitgever
  * de ID van de houder
  * een datum 'einde geldigheid'
  * een handtekening

- Uitgever, houder en verifier hebben elk een eigen applicatie. Voor de uitgever kan dit een webapplicatie op een desktop of laptop zijn, voor houder en uitgever wordt een mobiele web applicatie gevraagd

- Met al deze applicaties moet het mogelijk zijn om unieke ID's (adressen) te genereren en om berichten te sturen naar - en te ontvangen van - de andere partijen.

- Het presenteren van een VC aan de verifier moet via een QR-code plaatsvinden

- Er moet een manier zijn voor gebruikers/houders om uitgevers te bereiken (adressen van service points)
