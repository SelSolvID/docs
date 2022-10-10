# Self sovereign ID

### Versie 1

## Auteurs

Wouter de Boer  
Daniel Hofman  
Hylbren Rijnders  
Mees van Dijk

# Inhoudsopgave

1. Inleiding  
   1.1 Doel van dit document  
   1.2 Referenties
2. Positionering  
   2.1 De huidige situatie  
   2.2 Probleemstelling  
   2.3 Alternative oplossingen
3. Belanghebbenden  
   3.1 Rollenoverzicht belanghebbenden  
   3.2 Profiel van de belanghebbenden  
   3.3 Behoeften van belanghebbenden
4. Productperspectief
5. Producteigenschappen
6. Overige requirements  
   6.1 Niet-functionele requirements  
   6.2 Randvoorwaarden  
   6.3 Documentatie requirements
7. Openstaande punten

# 1 Inleiding

## 1.1 Doel van dit document

Dit document geeft de gemeenschappelijke visie van Ditlab en de projectgroep op
het project SSI. Het geeft de probleemstelling en de belanghebbenden weer,
alsmede een samenvattend overzicht van de eisen die aan de beoogde applicatie
worden gesteld. Deze eisen zijn nog niet verder uitgewerkt; de Vision dient als
basis van waaruit deze uitwerking gestalte krijgt.

## 1.2 Referenties

| Titel       | Vindplaats               |
| ----------- | ------------------------ |
| RUP op maat | http://www.rupopmaat.nl/ |

# 2 Positionering

## 2.1 De huidige situatie

Mensen gebruiken tegenwoordig hun ID kaart, rijbewijs of paspoort om zichzelf te
identificeren. Deze methode werkt maar heeft een aantal verbeterpunten. Wanneer
mensen hun ID laten zien ziet de persoon die het controleert vaak veel meer
gegevens dan nodig, op een ID kaart staan bijvoorbeeld naam, geboorteplaats,
etc. Mensen moeten ook vaak andere documenten aanleveren naast hun ID kaart.
Deze informatie moet vaak refereren naar gegevens op de ID kaart (vaak naam) en
ondertekend zijn voor een validiteitscontrole. Een voorbeeld van een extra
document kan zijn een loonstrook om aan te tonen hoeveel salaris iemand
verdient. Ook moeten mensen tegenwoordig altijd hun ID bij zich hebben, als
iemand hun ID vergeet mee te nemen is dat snel een probleem. Het huidige systeem
werkt dus, maar er zijn wel duidelijke verbeterpunten te identificeren.

## 2.2 Probleemstelling

De belangrijkste twee problemen met het huidige systeem zijn dat het niet
optimale privacy biedt en dat het niet makkelijk uit te breiden is. Het probleem
van privacy betrekt zich met name op het feit dat er veel meer gegevens gedeeld
worden dan voor de meeste interacties nodig zijn. Dingen zoals geboorteplaats,
geboortedatum of BSN zijn in de meeste gevallen niet nodig. Het gegeven
geboortedatum lijkt in eerste instantie essentieel voor veel interacties, maar
in de meeste gevallen gaat het slechts om een minimumleeftijd, en maakt de
specifieke leeftijd niet uit.  
Het ontbreken van de mogelijkheid om uit te breiden slaat op het feit dat een ID
bewijs tegenwoordig statisch is. De gegevens die er op staan kunnen alleen
worden veranderd door een nieuw ID bewijs uit te geven. Er is geen ruimte om
nieuwe soorten gegevens toe te voegen. Door de statische aard van een ID bewijs
kunnen er ook alleen gegevens op staan die (bijna) niet veranderen.  
Als laatste, kleine verbeterpunt, is dat een ID kaart een extra ding is dat
mensen altijd bij zich moeten hebben. Tegenwoordig kan niemand het huis uit
zonder hun telefoon, mogelijk bankpas, al kan deze vaak al worden vervangen door
een telefoon, hun ID kaart en hun sleutels. Wat ook al is gebeurd met de
bankpas, namelijk dat deze mogelijk op de telefoon opgeslagen kan worden, zou
ook kunnen met een ID kaart. Op die manier hoeven mensen minder dingen bij zich
te hebben. Een ander voordeel van een ID op een telefoon is dat het minder
gevoelig is voor misbruik. Een telefoon kan op afstand geblokkeerd worden, een
ID kaart niet.

## 2.3 De oplossing

De oplossing voor de genoemde problemen is het vervangen van de ID kaart met een
ID bewijs op de telefoon. Specifiek op een self-governing manier. Dit houdt in
dat mensen hun gegevens alleen opslaan op hun eigen telefoon. Op deze manier
kunnen mensen altijd zelf bepalen wanneer en met wie hun gegevens worden
gedeeld.  
Om dit systeem werkend te krijgen moet een infrastructuur worden opgezet die
door middel van cryptografie en "trusted parties" garantie biedt dat de gegevens
die mensen claimen te hebben ook echt zijn.

## 2.4 Alternatieve oplossingen

Een mogelijke alternatieve oplossing zou zijn om verder te gaan volgens de
status quo, want hoewel er mogelijke verbeteringspunten zijn, is de ID kaart wel
tried en true en wordt deze al meerdere decennia gebruikt. Hierdoor is het
gebruik van de gewone ID kaart bekend bij iedereen en is iedereen niks anders
gewend.

### 2.4.1

Een andere alternatieve oplossing zou zijn om wel gebruik te gaan maken van een
online ID kaart, maar om dit te doen via een centrale database van de overheid.
Deze oplossing zou wel nieuwe problemen met zich mee brengen zoals het probleem
van de beveiliging van de servers met data, en de kosten om deze servers
constant aan te hebben om de gegevens te verspreiden.

### 2.4.2

Wat ook een alternatieve oplossing zou kunnen zijn is meekijken met andere
landen naar wat zij gebruiken of aan het ontwikkelen zijn. Dit zou namelijk
betekenen dat er minder onderzoek en ontwikkeling nodig zou zijn om een
oplossing te maken. Ook is het makkelijker om te weten of deze oplossing goed
werkt sinds het mogelijk is om te kijken hoe dit product in het andere land
wordt toegepast, en of deze implementatie goed werkt.

# 3 Belanghebbenden

## 3.1 Overzicht belanghebbenden vertegenwoordigers

| rol           | Vertegenwoordiger | Betrokkenheid               |
| ------------- | ----------------- | --------------------------- |
| Opdrachtgever | Jan van Mullingen | Lab-coach, Domeindeskundige |
| Opdrachtgever | Reimer Wiersma    | (technisch) Adviseur        |
| Opdrachtgever | Matthieu Kroezen  | (technisch) Adviseur        |
| Opdrachtgever | Jacob de Boer     | Kwaliteitscontrole          |

## 3.2 Profiel van de belanghebbenden

### 3.2.1 Opdrachtgever

De opdrachtgever heeft het idee voor het project tot conceptie gebracht. Ze
hebben het probleem geïdentificeerd en een conceptuele oplossing bedacht. Verder
zijn ze tijdens het project betrokken door middel van ondersteuning op aanvraag
van het projectteam en geplande periodieke evaluaties.  
De opdrachtgevers hebben als doel met dit project om te leren van de aanpak van
de projectgroep en inspiratie op te doen uit deze aanpak. Het project is een
succes als er een werkend proof-of-concept wordt aangeleverd met goed doordachte
(technische) keuzes, vooral als deze keuzes nieuwe inzichten bieden op het
probleem.

## 3.3 Behoeften van belanghebbenden

### 3.3.1 Werkend proof-of-concept

Belanghebbenden:

- Opdrachtgever

Prioriteit: Must have

Een werkend proof-of-concept systeem is het minimale op te leveren vanuit het
project.

### 3.3.2 Bijbehorende documentatie

Belanghebbenden:

- Opdrachtgever

Prioriteit: Must have

De bijbehorende documentatie, zoals dit document, is een verplichte vanuit de
opdrachtgever. Verder is de documentatie de belangrijkste plek om (technische)
projectkeuzes uit te leggen. Aangezien leren van de aanpak van de projectgroep
een van de belangrijkste doelen is van de opdrachtgever is de documentatie even
belangrijk als het product zelf.

# 4 Productperspectief

Als we als klant, ofwel gebruiker, de Nederlandse burgers nemen, is het product
een aanvulling op alle features op hun telefoon. In het oude systeem was een
identiteitsbewijs een losstaand concept. In het nieuwe systeem wordt dit
toegevoegd aan de mogelijkheden van de telefoon. In die zin is het vergelijkbaar
met betaalpassen op een telefoon. Dit systeem zal echter losstaan van andere
features op de telefoon, hoewel het wel gebruik maakt van de mogelijkheden van
de telefoon.  
Het systeem kan ook vergeleken worden met het bestaande systeem voor bewijs van
corona vaccinatie. Hier haalt het dan ook inspiratie uit.

# 5 Producteigenschappen

De producteigenschappen zijn te zien in het Use Case Model.

# 6 Requirements

## 6.1 Niet-functionele requirements

De belangrijkste niet-functionele requirement voor dit project is dat het
stabiel moet zijn. De digitale ID moet ten alle tijden werken, met
uitzonderingen zoals wanneer een telefoon leeg is. Het mag nooit voorkomen dat
de app niet werkt of dat bepaalde nodige verbindingen niet gemaakt kunnen
worden.

Een ander belangrijk niet-functioneel requirement is schaalbaarheid. Specifiek
voor deze requirement is een self-sovereign ID erg geschikt, aangezien er veel
decentralisatie mogelijk is binnen het concept. Wel belangrijk is dat er bij het
project rekening wordt gehouden met de performance van verschillende telefoons,
aangezien dit wel impact kan hebben op de schaalbaarheid.

Een derde requirement is usability. Omdat iedereen een ID heeft en iedereen ook
op een gegeven moment wel een ID nodig gaat hebben is het belangrijk dat het
systeem ook voor iedereen bruikbaar is. Een belangrijke groep gebruikers om
rekening mee te houden zijn oudere gebruikers, mensen die minder ervaring hebben
met het omgaan met smartphones of computers. Zoals ook al duidelijk werd met de
invoering van het Digid systeem is dat het nog niet voor iedereen altijd
makkelijk is om naar zo'n nieuw systeem over te stappen.

## 6.2 Randvoorwaarden

Een randvoorwaarde voor dit project is dat de app self sovereign is, en dat de
user makkelijk kan kiezen welke gegevens hij wil delen met anderen. Ook is een
randvoorwaarde dat er een app is voor de user en een webapplicatie voor het
invoeren van de data van de user. En tot slot is het belangrijk dat dit product
gedecentraliseerd is, en dat alle data veilig is.

## 6.3 Documentatie requirements

Documentatie is een belangrijk onderdeel van dit project. Samen met de
opdrachtgevers hebben de projectleden afgesproken te werken volgens het RUP
model. Specifiek de RUP op maat standaarden worden aangehouden. Deze geven ook
richtlijnen voor welke soorten documentatie er opgeleverd moeten worden.  
In de eerste fase van het project worden opgeleverd:

- Een visiedocument (dit document)
- Een acceptatie plan
- Use cases
- Use case diagram

# 7 Openstaande punten

-
