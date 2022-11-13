# Software architecture document

## Self-sovereign Identity

## Auteurs

Wouter de Boer  
Daniel Hofman  
Hylbren Rijnders  
Mees van Dijk

## Inleiding

### 1.1 Doel van dit document

Het software architectuur document bevat een uitgebreide architecturale kijk op
het systeem SSI. Het beschrijft een aantal verschillende architecturale views
van het systeem om zo verschillende aspecten van het systeem te belichten. Dit
document beschrijft de verschillend eRUP views op de software architectuur
volgens het 4+1 view model.

<img src="4plus_1_views.jpg">

Het 4+1 model stelt de verschillende belanghebbenden in staat vanuit hun eigen
perspectief de invloed van de gekozen architectuur te bepalen.

<!-- De Process View (communicatie van processen) is niet als los hoofdstuk
uitgewerkt maar ondergebracht bij de hoofdstukken 3.3 en 5. -->

### 1.2 referenties

| titel                                   | Auteur      | vindplaats  |
| --------------------------------------- | ----------- | ----------- |
| Software architectuur document template | RUP op maat | RUP op maat |

## 2 Architecturale eisen

### 2.1 Niet-functionele eisen

Voor dit project zijn weinig niet-functionele eisen, dit komt omdat het doel van
het project is om een proof-of-concept applicatie te bouwen. In overleg met de
opdrachtgevers is kortgesloten dat dingen zoals performance, accessibility en
scalability niet belangrijk zijn.

De eisen die wel gegeven zijn:

#### 2.1.1 Snelheid

eis: De applicatie moet elke actie binnen een seconde kunnen uitvoeren.  
bron: opdrachtgever  
architecturale relevantie: Bij het ontwerpen en bouwen van de applicatie moet
worden gezorgd en getest dat de applicatie performant genoeg is om deze eis te
halen

### 2.2 Use case View

Het meest interessante, architecturaal gezien, aan de use-cases is dat er een
synthetische vorm van vertrouwen moet worden gebouwd. Dit model is synthetisch
omdat het niet alleen berust op menselijke afspraken, zoals vertrouwen normaal
wordt geïmplementeerd, maar ook op bewijsbare technische manieren. Dit wordt
geïmplementeerd met cryptografische certificaten. Deze werken op zo'n manier dat
een officiële instantie een eigen certificaat heeft en daarmee nieuwe
certificaten kan uitgeven aan vertrouwde partijen. Doordat mensen de "officiële
instantie" vertrouwen kunnen ze er automatisch van uit gaan dat de certificaten
die door deze instantie zijn uitgegeven ook te vertrouwen zijn. Hier komt de
cryptografie van pas om te bewijzen dat een certificaat is uitgegeven door de
"officiële instantie". Deze instanties zijn in het geval van dit project van
tevoren bepaald, namelijk:

- Duo, voor diploma's
- Gemeente's, voor identiteitsbewijzen
- Werkgevers, voor inkomensverklaringen
- RDW, voor rijbewijzen

## 3 Logical view

### 3.1 Lagen

De applicatie bestaat uit meerdere lagen. Voor het uitvoeren van acties met de
applicatie moet er een presentatie/interactie laag zijn. Deze laag communiceert
met een service laag om deze acties waar te maken. Deze service laag praat met
een data laag, welke zich op elk device zelf zal bevinden. Deze data laag bevat
ondertekende verifiable credentials. Omdat deze VC's ondertekend zijn is er geen
externe connectie nodig om te verifiëren dat ze valide zijn. Daarom is het
voldoende om ze lokaal op te slaan.

Een andere data laag is verantwoordelijk voor het behandelen van globale data.
Deze globale data bestaat uit nog niet opgehaalde VC's en openstaande verzoeken
tot ondertekening. Zodra deze verzoeken volledig afgehandeld zijn kunnen ze ook
verwijderd worden uit deze data laag.

### 3.2 Deelsystemen

De applicatie vereist een aantal deelsystemen. In grote lijnen komen er een app,
een webapp en een api voor de webapp en app.

De app is bedoeld voor de gebruikers die willen verifyen en holden van
verifiable credentials (VC's).

De webapp is bedoeld voor issuers, die VC's willen uitgeven aan individuen.

De api is voor de webapp en de app, via de api krijgen de apps hun nieuwe VC's

### 3.3 Use case realizations

Alle use cases zullen gebouwd worden op een zelfde techniek. Bij het verifiëren
van een VC wordt een peer-to-peer connectie opgezet tussen twee mobiele
telefoons. De holder stuurt dan de relevante VC naar de verifier. De verifier
kan, omdat deze de benodigde root certificaten al bezig, verifiëren dat de VC
geldig is.  
Om de peer-to-peer connectie op te zetten wordt Bluetooth gebruikt. Verder wordt
er gebruik gemaakt van bekende cryptografie libraries om de certificaten aan te
maken en te verifiëren.

## 4 implementation view

### 4.1 Package structuur

Voor het implementeren van de applicatie worden een aantal packages geschreven.
Omdat niet elk deelsysteem in dezelfde taal wordt gebouwd wordt het niet altijd
mogelijk om code uit deze packages te delen. Voor de api worden een aantal
models geschreven die ook door de webapp kan hergebruiken. De app zal, omdat
deze niet dezelfde programmeertaal gebruikt, dit model zelf moeten dupliceren.

### 4.2 Invulling lagenstructuur

#### 4.2.1 Presentatie

De presentatie wordt op twee verschillende plekken op verschillende manieren
uitgevoerd. Dit komt omdat er twee verschillende applicaties worden gebouwd als
onderdeel van het systeem.

De twee plekken zijn: de app voor op mobiele telefoons en de website.  
Voor de app worden standaard Android libraries gebruikt die het gemakkelijk
maken om een user interface te maken.

Voor de website wordt het web framework Svelte gebruikt. Dit is een web
framework dat zich focust op de presentatie-laag van websites. Dit framework
maakt het gemakkelijker om interactieve web applicaties te bouwen.

#### 4.2.2 Service laag

De service laag is verantwoordelijk voor het uitvoeren van de business logic. In
dit geval zal dat zijn het aanvragen, aanmaken, ophalen, delen en verifieren van
VC's.

Voor het aanvragen en ophalen van VC's wordt http gebruikt. Een holder kan via
haar telefoon verbinden met een server om een VC op te halen, mits deze is
goedgekeurd, en dus ondertekend, door de relevante instantie. De holder kan ook
via haar telefoon een VC aanvragen. Deze moet dan worden goedgekeurd in de web
applicatie.

Om dit allemaal te realiseren moeten veel verschillende technieken gebruikt
worden. Veel van deze acties hebben te maken met cryptografie, hier zullen
standaard (ingebouwde) frameworks voor zijn. Deze worden ook gebruikt.

Voor het communiceren met de server en andere telefoons worden ook standaard
libraries gebruikt.

#### 4.2.3 Data laag

Voor het opslaan van verzoeken tot VC's en de statussen van deze verzoeken wordt
een SQL database gebruikt. De api laag is de enige die direct met deze

### 4.3(Her)gebruik van componenten en frameworks

[Beschrijf hier de bij de bouw te (her)gebruiken componenten en frameworks
(intern en van derden). Dit voor zover ze niet bij de invulling van de
lagenstructuur zijn behandeld. Indien er bij de eisen bepaalde frameworks zijn
genoemd, dienen deze hier terug te komen.]

### 5. Deployment View

[Beschrijf hier de fysieke netwerk(hardware) configuraties waarop de software
gaat draaien. Beschrijf minimaal de configuraties van de verschillende fysieke
nodes (computers, CPUs), de interactie tussen (deel)systemen en de connecties
tussen deze nodes (bus, LAN, point-to-point, messaging, SOAP, http, https). Maak
gebruik van een deployment-diagram.]
