# Software architecture document

## Self-sovereign Identity

## Auteurs

Wouter de Boer  
Daniel Hofman  
Hylbren Rijnders  
Mees van Dijk

## Inleiding

# Inhoudsopgave

- [Software architecture document](#software-architecture-document)
  - [Self-sovereign Identity](#self-sovereign-identity)
  - [Auteurs](#auteurs)
  - [Inleiding](#inleiding)
- [Inhoudsopgave](#inhoudsopgave)
  - [1.1 Doel van dit document](#11-doel-van-dit-document)
  - [1.2 referenties](#12-referenties)
  - [2 Architecturale eisen](#2-architecturale-eisen)
    - [2.1 Niet-functionele eisen](#21-niet-functionele-eisen)
      - [2.1.1 Performance](#211-performance)
      - [2.1.2 Beheerbaarheid](#212-beheerbaarheid)
      - [2.1.3 Betrouwbaarheid](#213-betrouwbaarheid)
      - [2.1.4 Beveiliging](#214-beveiliging)
    - [2.2 Use case View](#22-use-case-view)
  - [3 Logical view](#3-logical-view)
    - [3.1 Lagen](#31-lagen)
      - [3.1.1 Laag-diagram](#311-laag-diagram)
    - [3.2 Deelsystemen](#32-deelsystemen)
    - [3.3 Use case realizations](#33-use-case-realizations)
    - [3.4 Sequentiediagrammen](#34-sequentiediagrammen)
    - [3.4.1 VC aanvragen](#341-vc-aanvragen)
    - [3.4.2 VC controleren](#342-vc-controleren)
  - [4 Implementation View](#4-implementation-view)
    - [4.1 Package structuur](#41-package-structuur)
      - [4.1.1 Package diagram](#411-package-diagram)
    - [4.2 Invulling lagenstructuur](#42-invulling-lagenstructuur)
      - [4.2.1 Presentatie](#421-presentatie)
        - [4.2.1.1 Android](#4211-android)
        - [4.2.1.2 Websites](#4212-websites)
      - [4.2.2 Service laag](#422-service-laag)
        - [4.2.2.1 API surface](#4221-api-surface)
        - [4.2.2.2 Websocket server protocol](#4222-websocket-server-protocol)
    - [4.2.3 Data laag](#423-data-laag)
      - [4.2.3.1 API](#4231-api)
      - [4.2.3.2 Android](#4232-android)
      - [4.2.3.3 Database diagrammen](#4233-database-diagrammen)
        - [4.2.3.3.1 Database diagram API](#42331-database-diagram-api)
        - [4.2.3.3.1 Database diagram user-app](#42331-database-diagram-user-app)
    - [4.3 (Her)gebruik van componenten en frameworks](#43-hergebruik-van-componenten-en-frameworks)
      - [4.3.1 API](#431-api)
      - [4.3.2 Android](#432-android)
      - [4.3.2 Svelte](#432-svelte)
  - [5. Deployment View](#5-deployment-view)
    - [5.1 Deployment en infrastructuur van API, database en web applicatie](#51-deployment-en-infrastructuur-van-api-database-en-web-applicatie)
    - [5.2 Deployment en infrastructuur voor de mobiele applicatie](#52-deployment-en-infrastructuur-voor-de-mobiele-applicatie)
      - [5.2.1 Waarom de implementatie van bluetooth niet is gelukt](#521-waarom-de-implementatie-van-bluetooth-niet-is-gelukt)
      - [5.2.2 Websockets als vervangende oplossing](#522-websockets-als-vervangende-oplossing)
    - [5.3 Teststraat](#53-teststraat)
      - [5.3.1 API](#531-api)
      - [5.3.2 Svelte](#532-svelte)
      - [5.3.3 Android](#533-android)
      - [5.3.1 Websocketserver](#531-websocketserver)
    - [5.4 Deployment diagram](#54-deployment-diagram)

### 1.1 Doel van dit document

Het software architectuur document bevat een uitgebreide architecturale kijk op
het systeem SSI middels het 4+1 view model op software architectuur: Logical,
Implementational, Process, Deployment + Use Case
<img src="images/4plus_1_views.jpg"/>

Het 4+1 model stelt de verschillende belanghebbenden in staat vanuit hun eigen
perspectief de invloed van de gekozen architectuur te bepalen.

<!-- De Process View (communicatie van processen) is niet als los hoofdstuk
uitgewerkt maar ondergebracht bij de hoofdstukken 3.3 en 5. -->

### 1.2 referenties

| titel                                   | Auteur      | vindplaats                                                                                                               |
| --------------------------------------- | ----------- | ------------------------------------------------------------------------------------------------------------------------ |
| Software architectuur document template | RUP op maat | RUP op maat                                                                                                              |
| View diagram                            | IBM         | https://posomas.isse.de/PosoMAS/core.tech.common.extend_supp/guidances/examples/four_plus_one_view_of_arch_9A93ACE5.html |
| Acceptatieplan                          | SelSolvid   | https://github.com/SelSolvID/docs/blob/master/Acceptatieplan.md                                                          |

## 2 Architecturale eisen

### 2.1 Niet-functionele eisen

Omdat het bij dit project gaat om een proof-of-concept applicatie te bouwen zijn
de niet-functionele eisen anders dan bij een gewoon project. Alle
niet-functionele eisen zijn ook opgenomen in het
[acceptatieplan](https://github.com/SelSolvID/docs/blob/master/Acceptatieplan.md)
Een aantal gegeven niet-functionele eisen zijn:

#### 2.1.1 Performance

Zoals ook genoemd in het acceptatieplan moet de applicatie normaal te gebruiken
zijn, dit houdt in dat er geen lag-spikes zijn tijdens het gebruik. Verder moet
een gebruiker niet hoeven wachten op lange laadtijden.

#### 2.1.2 Beheerbaarheid

Voor het project wordt een teststraat ingericht. Dit houd in dat er drie
verschillende versies van de applicatie beschikbaar worden gemaakt op elk
moment. Praktisch betekent dat dat er drie versies van het complete deployment
diagram (zie 5.3) worden gedeployed.

#### 2.1.3 Betrouwbaarheid

Het systeem moet altijd beschikbaar zijn. Dit wordt behaald door dat de basis
interacties van het systeem (verifyen van een credential) niet met een centrale
server hoeven te praten. Hiermee ligt de verantwoordelijkheid bij de gebruiker
om een werkend apparaat te onderhouden.

#### 2.1.4 Beveiliging

Beveiliging staat centraal in dit project. Daarom wordt het OpenSSL package
gebruikt (zie 4.1). Dit package staat er om bekend betrouwbare beveiliging te
bieden.

### 2.2 Use case View

De use cases van het project worden in meer detail beschreven in het use-case
document. De volgende use-cases zijn geïdentificeerd:

- Een issuer wil requests goedkeuren en of afkeuren
- Een gebruiker wil alcohol kopen, benodigd is de leeftijd
- Afsluiten van een dienst met voorwaarden
- Een gebruiker wil solliciteren, daar zijn een ID en de diplomas van de
  middelbare school en de HBO instelling voor nodig
- Huren van goederen
- Het afsluiten en het checken van een verzekering.

De use-cases zijn opgenomen in een
[apart use cases bestand](Usecasedocument.md).

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

#### 3.1.1 Laag-diagram

<img src="http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/SelSolvID/docs/master/diagrams/softwarearchitecture/layer.puml"/>

### 3.2 Deelsystemen

Onze Proof of Concept (POC) vereist een aantal deelsystemen. Het bestaat uit een
android app, een web app, een API, een proxy, een web-socket server en een host
voor het root certificaat.

De android app is bedoeld voor de gebruikers die verifiable credentials (VC's)
willen verifien en holden.

De web app is bedoeld voor issuers, die VC's willen goedkeuren of afkeuren en
uitgeven.

De API is een backend voor alle applicaties. De API handelt de requests van de
issuer web app af en zorgt dat deze acties worden opgeslagen in een database. De
API ontvangt ook de verzoeken van holders voor nieuwe VC's en slaat deze op in
de database.

De web-socket server faciliteert een verbinding tussen twee mobiele devices. De
devices verbinden beide met een kanaal op de web-socket server en kunnen dan met
elkaar praten.

De proxy zorgt er in productie voor dat alle requests naar hetzelfde domein
kunnen, en dat ze achter de schermen naar het juiste deelsysteem worden
gestuurd. Dit doet hij op basis van het http pad van het request.

De host voor het root certificaat is een simpele, static file server die een
enkel bestand, het root certificaat, host op een bekende plek. Dit zodat alle
gebruikers van het systeem deze kunnen gebruiken. Op het moment wordt dit ook
gedaan door de proxy server, met wat extra configuratie.

### 3.3 Use case realizations

Alle use cases zullen gebouwd worden op een zelfde techniek. Bij het verifiëren
van een VC wordt een peer-to-peer connectie opgezet tussen twee mobiele
telefoons middels WebSockets. De holder stuurt dan de relevante VC naar de
verifier. De verifier kan, omdat deze de benodigde root certificaten al bezit,
verifiëren dat de VC geldig is.

Om de peer-to-peer connectie op te zetten wordt wordt er gebruik gemaakt van de
API om de beide users te verbinden aan elkaar, om zo data uit te wisselen met
elkaar. Hier wordt verder op ingegaan in Hoofdstuk 5. Verder wordt er gebruik
gemaakt van bekende cryptografie libraries om de certificaten aan te maken en te
verifiëren.

### 3.4 sequence diagrammen

Dit zijn de verschillende sequence diagrammen die uitleggen wat er precies
gedaan worden in een applicatie en wie welke acties uitvoert.

### 3.4.1 VC aanvragen

Een diagram waarbij de aanvraag wordt goedgekeurd

<img src="http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/SelSolvID/docs/master/diagrams/sequence/request-identity/accept.puml"/>

Een diagram waarbij de aanvraag nog niet beantwoord is:

<img src="http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/SelSolvID/docs/master/diagrams/sequence/request-identity/not-answered.puml"/>

Een diagram waarbij de aanvraag wordt afgekeurd:

<img src="http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/SelSolvID/docs/master/diagrams/sequence/request-identity/denied.puml"/>

Een diagram waarbij andere VC's worden aangeleverd als bewijs voor een nieuwe
aanvraag:

<img src="http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/SelSolvID/docs/master/diagrams/sequence/request-drivers-license.puml"/>

### 3.4.2 VC controleren

<img src="http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/SelSolvID/docs/master/diagrams/sequence/show-identity.puml"/>

## 4 Implementation View

### 4.1 Package structuur

Voor het implementeren van de applicatie worden een aantal packages gebruikt.
Omdat niet elk deelsysteem in dezelfde taal is gebouwd is het niet altijd
mogelijk om code uit deze packages te delen. Voor de api worden een aantal
models geschreven die ook door de webapp kan hergebruiken. De app zal, omdat
deze niet dezelfde programmeertaal gebruikt, dit model zelf moeten dupliceren.

Verder zullen er een aantal externe packages gebruikt worden. Voor het
realiseren van de api wordt gebruik gemaakt van [koajs](https://koajs.com/).
KoaJs is een populair, modern webframework voor het installeren van middleware
in een web applicatie. Verder biedt het uitbreidingen voor dingen zoals routing,
logging en automatisch requests parsen.

Verder wordt er bij alle cryptografische handelingen gebruik gemaakt van
[OpenSSL](https://www.openssl.org/). OpenSSL is de meest populaire toolkit voor
cryptografie en veilige communicatie.

Voor het realiseren van een user interface op android wordt gebruik gemaakt van
de standaard android libraries. Kotlin kan hiervan, net zoals java, gebruik
maken om gemakkelijk een user interface te bouwen.

De webapplicatie gaat gebruik maken van [Svelte](https://svelte.dev/). Svelte is
een framework om responsive user interfaces te bouwen. Bovenop svelte gaan we
[Svelte material UI](https://sveltematerialui.com/) gebruiken. Dit is een set
componenten die makkelijk kunnen worden gebruikt in het bouwen van een ui.

#### 4.1.1 Package diagram

<img src="http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/SelSolvID/docs/master/diagrams/softwarearchitecture/package.puml"/>

### 4.2 Invulling lagenstructuur

#### 4.2.1 Presentatie

De presentatie wordt op twee verschillende plekken op verschillende manieren
uitgevoerd. Dit komt omdat er twee verschillende applicaties worden gebouwd als
onderdeel van het systeem.

##### 4.2.1.1 Android

Voor de app worden standaard Android libraries gebruikt die het gemakkelijk
maken om een user interface te maken. De taal waarin de android app geschreven
wordt is Kotlin. Kotlin wordt gebruikt omdat het een modern alternatief is op
java. Traditioneel wordt java gebruikt voor android apps, maar Kotlin is daarop
een modern alternatief en sinds enige tijd door google aanbevolen als taal om de
apps in te ontwikkelen. Gezien er slechts drie schermen in onze applicatie
zitten maken wij geen gebruik van de navigatiegraph structuur zoals die aanweig
is in android, omdat elk scherm vanuit de onderste navigatiebalk toegankelijk
is.

##### 4.2.1.2 Websites

Voor de website wordt het web framework Svelte gebruikt. Dit is een webframework
dat zich focust op de presentatielaag van websites. Dit framework maakt het
gemakkelijker om interactieve web applicaties te bouwen. Svelte is een relatief
nieuw web framework dat erg positief is ontvangen. Het zorgt er voor dat
developers snel en gestructureerd kunnen werken. Daarom gebruiken we Svelte.

#### 4.2.2 Service laag

De servicelaag is verantwoordelijk voor het uitvoeren van de business logic. In
dit geval zal dat zijn het aanvragen, aanmaken, ophalen, delen en verifieren van
VC's.

Voor het aanvragen en ophalen van VC's wordt https gebruikt. Een holder kan via
haar telefoon verbinden met de api om een VC op te halen, mits deze is
goedgekeurd, en dus ondertekend, door de relevante instantie. De holder kan ook
via haar telefoon een VC aanvragen. Deze moet dan worden goedgekeurd in de web
applicatie.

Om dit allemaal te realiseren moeten veel verschillende technieken gebruikt
worden. Veel van deze acties hebben te maken met cryptografie, hier zullen
standaard (ingebouwde) frameworks voor zijn. Deze worden ook gebruikt. Het
bouwen van deze API laag wordt gedaan met Node.js en typescript.

Voor het communiceren met de server en andere telefoons worden ook standaard
libraries gebruikt.

Verder biedt de servicelaag een Websocket server die als alternatief op
bluetooth dient. Hiermee kunnen verschillende telefoons met elkaar verbinden
voor real-time communicatie. Het protocol van deze websocket server is hieronder
in punt 4.2.2.2 beschreven.

##### 4.2.2.1 API surface

| url             | method | functie                                        |
| --------------- | ------ | ---------------------------------------------- |
| /token          | GET    | token ophalen voor gebruik in api communicatie |
| /requests       | GET    | een lijst ophalen van openstaande VC requests  |
| /requests/{id}  | GET    | Details van een request ophalen                |
| /requests/{id}  | PUT    | Reageren op een request (goed of afkeuren)     |
| /issuer         | GET    | Een lijst van issuers ophalen                  |
| /holder/request | POST   | Als holder een nieuw request indienen          |

**GET /token** Hierbij wordt de header `Authentication` gebruikt met basic
authentication scheme.  
Dit endpoint zorgt ervoor dat de token als cookie wordt gezet in de browser
zodat de client hem automatisch bij volgende requests kan meesturen. Dit is
"inloggen" in het systeem.

**GET /requests** Hier wordt het token meegegeven als auth header of als cookie.
De response body ziet er als volgt uit:

```json
[
  {
    "id": 0,
    "fromUser": "I am a legit user",
    "date": 10123718972391823,
    "requestText": "Some claim"
  }
]
```

**GET /requests/{id}** Hierbij worden de details van een request opgehaald. De
ID staat in het path. De token wordt meegegeven als auth header. De response
body ziet er uit zoals:

```json
{
  "id": 0,
  "fromUser": "I am a legit user",
  "date": 10123718972391823,
  "requestText": "Some claim",
  "attachedVCs": ["**EXPORTED VC TEXT**", "**EXPORTED VC TEXT**"]
}
```

**PUT /requests/{id}** Hiermee kan een request goed of afgekeurd worden. Het
token wordt meegegeven in de header en de request body ziet er als volgt uit:

Een accepted request:

```json
{
  "accept": true
}
```

Een niet-accepted request:

```json
{
  "accept": false,
  // reason is optional and only applicable when "accept": false
  "reason": "You lied about your age"
}
```

**GET /issuer** Hiermee kun je een lijst aan issuerId's ophalen

De data ziet er dan als volgt uit:

```json
[
  {
    "id": 1,
    "name": "Test issuer"
  },
  {
    "id": 2,
    "name": "Paradigm"
  }
  // More in list
]
```

**POST /holder/request** Hiermee kan een holder een nieuw request indienen. De
data van de _request body_ ziet er als volgt uit:

```json
{
  "issuerId": 2,
  "vc": "**EXPORTED VC TEXT**",
  "attachedVCs": ["**EXPORTED VC TEXT**", "**EXPORTED VC TEXT**"]
}
```

De server stuurt dan een _response body_ terug met een random ID van je request.
Deze kun je gebruiken om later de status van je request te checken. Je moet de
ID dus opslaan. Die body ziet er als volgt uit:

```json
{
  "id": "f55G3QkF8bN1K39LvsXgD4jGppX9xc_0oZEz5gJPcJE"
}
```

**GET /holder/request/{id}** Hiermee kun je de status van een request ophalen.
De id krijg je uit een post van een request. Deze moet je dus opslaan bij het
posten.  
Op het moment dat je de status opvraagt kunnen er twee dingen aan de hand zijn:

1. De request is behandeld en heeft een uitkomst. In dit geval krijg je een HTTP
   200 status en ziet de response body er als volgt uit:

```json
{
  "accept": true,
  "vc": "**EXPORTED VC TEXT**"
}
```

of

```json
{
  "accept": false,
  "vc": null
}
```

2. De request is nog niet behandeld. In dit geval krijg je een HTTP 202 status
   en is de response body leeg.

##### 4.2.2.2 Websocket server protocol

De websocket server werkt met JSON berichten. Het protocol biedt alleen
mogelijkheid tot het openen(/verbinden met) van een kanaal met een id, het
sluiten van een kanaal met een id en het broadcasten van een arbitrair bericht
naar een kanaal.

**Open**

```json
{
  "type": "open",
  "channel": "*channelID*"
}
```

**Close**

```json
{
  "type": "close",
  "channel": "*channelID*"
}
```

**Message**

```json
{
  "type": "message",
  "channel": "*channelID*",
  "payload": "arbitrairy data"
}
```

in het Geval dat een `message` of `close` bericht wordt gestuurd stuurt de
server een bericht naar alle clients in dat kanaal. Deze zien er als volgt uit:

**Message**

```json
{
  "type": "message",
  "channel": "*channelID*",
  "payload": "the message payload"
}
```

**Close**

```json
{
  "type": "close"
}
```

Als een client een message stuurt zonder `type` of met een onbekend `type` dan
stuurt de server het volgende bericht terug:

```json
{
  "type": "erorr",
  "payload": "unknown message type"
}
```

### 4.2.3 Data laag

Voor het opslaan van verzoeken tot VC's en de statussen van deze verzoeken wordt
een SQL database gebruikt in de API en in de android-app.

#### 4.2.3.1 API

De api laag is de enige die direct met deze database praat. De api laag zit
tussen zowel de web applicatie als de mobiele applicatie. Hoewel de mobiele
applicatie over het algemeen de api weinig nodig zal hebben. Dit is omdat de
mobiele applicatie door verifyers en holders wordt gebruikt en deze communiceren
altijd via een peer-to-peer connectie tussen twee mobiele apparaten.

#### 4.2.3.2 Android

In de user app bevind zich een SQLITE database om aangevraagde, goed- en
afgekeurde VC's op te slaan. Dit is gerealiseerd met het android ORM Room.

#### 4.2.3.3 Database diagrammen

De volgende diagrammen laten zien hoe de interne databasestructuur van de API en
de android app eruit zien.

###### 4.2.3.3.1 Database diagram API

<img src="http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/SelSolvID/docs/master/diagrams/softwarearchitecture/databaseAPI.puml"/>

###### 4.2.3.3.1 Database diagram user-app

<img src="http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/SelSolvID/docs/master/diagrams/softwarearchitecture/databaseUserApp.puml"/>

### 4.3 (Her)gebruik van componenten en frameworks

#### 4.3.1 API

Het meest algemene component is de API, deze kan via het internet door iedereen
met de juiste toegang benaderd worden. Deze is nodig om interne applicaties
boven op te bouwen maar ook derden zouden toegang kunnen krijgen tot deze api.
Op deze manier kunnen derden hun eigen toepassingen bouwen die hun eigen doelen
beter bereiken dan een algemene applicatie.

Bij het bouwen van deze api wordt code geschreven die direct herbruikt kan
worden bij de bouw van de web applicatie. Verder kan deze code gemakkelijk
vertaald worden naar code voor de mobiele applicatie.

Dit komt omdat voor zowel de API als de webapplicatie javascript wordt gebruikt.
Boven op javascript wordt dan typescript gebruikt. Bij typescript worden
modellen van data geschreven die overal in het systeem gebruikt moeten worden.

#### 4.3.2 Android

Bij de android app wordt er gebruik gemaakt van zogenoemde fragments:
herbruikbare stukken layout die dynamisch in elk scherm vna de app kunnen worden
gebruikt. Ook wordt er gebruik gemaakt van een zogenoemde recyclerview, dit is
een speciale soort lijst die optimaal gebruik maakt van de resources van een
apparaat.

#### 4.3.2 Svelte

Daniel?

## 5. Deployment View

### 5.1 Deployment en infrastructuur van API, database en web applicatie

Voor de deployment is het belangrijk dat de API en de webapplicatie via een http
proxy op hetzelfde domein draaien. Dit zorgt ervoor dat de webapplicatie veilig
en zonder moeilijkheden met de API mag praten.

Om dit te realiseren worden er een aantal docker containers gebouwd. Namelijk
voor:

- Het serveren van de webapplicatie
- Het draaien van de API
- Het draaien van de database.
- Het proxy-en van requests naar de web-applicatie of de API

Deze vier containers zitten allemaal in een zelfde privénetwerk. Alleen de proxy
kan van buitenaf benaderd worden. De proxy zet https requests om naar http
requests, zodat de individuele servers geen verantwoordelijkheid dragen voor
https, dit zorgt voor veel minder complexiteit in de code. De proxy zorgt er ook
voor dat elk request bij de juiste service aankomt. Het is alleen natuurlijk
niet mogelijk direct de database te benaderen, dat kan alleen via de API.

De proxy weet welk request voor welke service is aan de hand van een url.

Requests met een url zoals `domein.nl/api/**/*` gaan allemaal naar de api. Alle
andere requests worden naar de server van de webapplicatie gestuurd.

Al deze infrastructuur kan, middels docker, op 1 server draaien. Omdat
scalability niet van groot belang is in dit project is 1 cloud server voldoende
voor het demonstreren van het proof of concept.

### 5.2 Deployment en infrastructuur voor de mobiele applicatie

Voor het downloaden van de mobiele applicatie wordt een continuous integration
pipeline ingesteld die automatisch de mobiele applicatie bouwt en beschikbaar
stelt voor downloaden. Dit wordt gerealiseerd in github actions. Binnen github
actions worden een aantal tools gebruikt om de applicaties te bouwen. Voor
Kotlin is dat de Kotlin compiler, voor svelte is dat de svelte compiler. Voor de
api wordt Typescript gebruikt om de code te transpilen.

Tijdens het gebruik van de mobiele applicatie praat de applicatie met de
bovengenoemde API, op de beschreven manier. Dit gebeurt met http(s). Naast het
praten met de API moet de mobiele applicatie ook peer-to-peer connecties kunnen
opzetten met andere instanties van de mobiele applicatie op andere mobiele
apparaten. Het plan was eerst om dit te doen via Bluetooth. Maar vanwege
problemen verder uitgelegd in het volgende kopje, is dit niet gelukt. De nieuw
bedachte optie om dit te implementeren is door gebruik te maken van de API om
beide personen aan elkaar te verbinden. Hier wordt dieper op ingegaan in 5.2.2

#### 5.2.1 Waarom de implementatie van bluetooth niet is gelukt

Voor de bluetooth zijn meerdere implementaties uitgeprobeerd; allereerst werd er
gebruik gemaakt van de de officiele
[android bluetooth documentatie](https://developer.android.com/guide/topics/connectivity/bluetooth).
Hier was hylbren aanvankelijk niet ver mee gekomen door de onervarenheid met
bluetooth en Kotlin ontwikkeling in het algemeen. Buiten het in-en-uitschakelen
van de bluetoothadapter kon er niets gerealiseerd worden. Daarnaast zijn
verschillende youtubefilmpjes en online tutorials gevolgd, allen zonder
resultaat, dit omdat een concrete implementatie van de functionaliteit die
hylbren specifiek wilde niet te vinden was in tutorialvorm. Met als gevolg dat
er bij sommige pogingen drie verschillende voorbeelden door elkaar heenliepen
wat ervoor zorgde ervoor dat het overzicht compleet weg was.

Op gegeven moment hebben Wouter en Daniel het bluetoothgedeelte overgenomen.
Door wederom gebruik te maken van de officiele
[android bluetooth documentatie](https://developer.android.com/guide/topics/connectivity/bluetooth)
kwam de app het verste. De setup was gelukt en je kon in de app je device
discoverable maken (zodat andere telefoons je kunnen vinden bij het zoeken naar
bluetooth connecties).

Het eerste waar we hier tegenaan liepen was het automatisch verbinden met
elkaar. Wanneer de gebruiker de qr-code heeft gescanned van een ander device,
zouden deze twee apparaten automatisch met elkaar via bluetooth moeten
verbinden. Dit kan je doen door lokale hardware identifiers op te halen. Voor de
automatische verbinding kon je het lokale bluetooth MAC address gebruiken en
deze zou je moeten kunnen ophalen met
[BluetoothAdapter.getAddress()](<https://developer.android.com/reference/android/bluetooth/BluetoothAdapter#getAddress()>).
Jammer genoeg kan dit niet meer sinds Android 6 gezien de getAdress methode nu
altijd een waarde van `02:00:00:00:00:00` terug geeft (zie
[deze](https://developer.android.com/about/versions/marshmallow/android-6.0-changes.html#behavior-hardware-id)
documentatie). Voor dit probleem habben we wel een
[mogelijke oplossing](https://developer.android.com/guide/topics/connectivity/companion-device-pairing)
voor gevonden maar hier waren we helaas niet aan toen gekomen gezien er meerdere
andere problemen waren waar we tegenaan liepen. Hoewel het automatisch pairen
via bluetooth niet mogelijk was, zou dit nog wel handmatig mogelijk zijn als de
gebruiker dit zelf doet in de bluetooth settings van zijn/haar telefoon.

Waar we uiteindelijk vast zijn gelopen is het versturen van data via bluetooth
(bij
[deze](https://developer.android.com/guide/topics/connectivity/bluetooth/connect-bluetooth-devices)
en[deze](https://developer.android.com/guide/topics/connectivity/bluetooth/transfer-data)
stap). Dit was ingewikkeld om te maken omdat de documentatie veel belangrijke
stappen oversloeg waardoor het stappenplan niet te volgen was. Ook was een
redelijk groot deel van de code outdated en waren meerdere gebruikte methodes
deprecated. Hierdoor was het een hele puzzel om uit te vinden wat er miste en
hoe dit toch kon werken. Dit zou uiteindelijk te veel tijd kosten om werkend te
krijgen binnen de tijd die wij nog hadden.

#### 5.2.2 Websockets als vervangende oplossing

Omdat Bluetooth dus niet werkend gekregen kon worden is er voor gekozen om te
werken met WebSockets. Bij deze techniek wordt er vanuit de user app verbinding
gelegd met een ander apparaat via de API middels het WebSocket protocol. Op deze
manier kunnen twee apparaten volledig over-en-weer communiceren over één
doorlopende TCP verbinding, in plaats van bijvoorbeeld HTTPS, dat slechts één
bericht per keer kan versturen.

### 5.3 Teststraat

Als onderdeel van het project wordt een teststraat ingericht. Dit houdt in dat
er van het systeem drie versies beschikbaar komen volgens het OTAP model, te
weten Ontwikkel, Testen, Acceptatie, Productie. Hiervoor worden de api en webapp
drievoudig gedeployed.

#### 5.3.1 API

#### 5.3.2 Svelte

#### 5.3.3 Android

De mobile applicatie krijgt drie verschillende downloads die overeenkomen met de
drie gedeployde versies van de webapp en api.

#### 5.3.1 Websocketserver

### 5.4 Deployment diagram

<img src="http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/SelSolvID/docs/master/diagrams/softwarearchitecture/deployment.puml">
```
