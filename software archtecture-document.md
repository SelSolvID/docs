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

| titel                                   | Auteur   | vindplaats  |
| --------------------------------------- | -------- | ----------- |
| Software architectuur document template | onbekend | RUP op maat |

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

DEZE MOET NOG INGEVULD WORDEN A.D.H.V. ge-updatte use cases.

## 3 Logical view

### 3.1 Lagen

De applicatie bestaat uit meerdere lagen. Voor het uitvoeren van acties met de
applicatie moet er een presentatie/interactie laag zijn. Deze laag communiceert
met een service laag om deze acties waar te maken. Deze service laag praat met
een data laag, welke zich op elk device zelf zal bevinden.

TODO: verbeter dit

### 3.2 Deelsystemen

De applicatie vereist een aantal deelsystemen. In grote lijnen komen er een app,
een webapp en een api voor de webapp en app.

De app is bedoeld voor de gebruikers die willen verifyen en holden van
verifiable credentials.

De webapp is bedoeld voor issuers, die VC's willen uitgeven aan individueen.

De api is voor de webapp en de app, via de api krijgen de apps hun nieuwe VC's

### 3.3 Use case realizations

TODO: schrijf dit a.d.h.v. use cases

## 4 implementation view

### 4.1 Package structuur

Voor het implementeren van de applicatie worden een aantal packages geschreven.
Omdat niet elk deelsysteem in dezelfde taal wordt gebouwd wordt het niet altijd
mogelijk om code uit deze packages te delen. Voor de api worden een aantal
models geschreven die ook door de webapp kan hergebruiken. De app zal, omdat
deze niet dezelfde programmeertaal gebruikt, dit model zelf moeten dupliceren.

### 4.2 Invulling lagenstructuur
