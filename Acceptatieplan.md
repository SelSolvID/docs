# Acceptatieplan SSI

### Versie 2

## Auteurs

Wouter de Boer  
Daniel Hofman  
Hylbren Rijnders  
Mees van Dijk



# Inhoudsopgave
1. Inleiding  
   1.1 Doel van dit document  
   1.2 Referenties
2. Verantwoordelijkheden  
3. Acceptatiecriteria  
   3.1 Performance  
   3.2 Beheerbaarheid   
   3.3 Betrouwbaarheid  
   3.4 Beveiliging  
   3.5 Funcitonaliteit  
   3.6 Gebruiksvriendelijkheid  
   3.7 Standaards   
   3.8 Documentatie  



# 1 Inleiding

## 1.1 Doel van dit document
Dit Acceptatie Plan verschaft een meetbare basis voor de te accepteren werkproducten. Het bevat een lijst met meetbare acceptatiecriteria die invulling geven aan niet-functionele, Use Case overstijgende eisen en de procedure waarop we bepalen of het project geaccepteerd wordt. 

## 1.2 Referenties
| Titel       | Vindplaats               |
| ----------- | ------------------------ |
| RUP op maat | http://www.rupopmaat.nl/ |



# 2 Verantwoordelijkheden
| Naam             | Rol               |
| ---------------- | ----------------- |
| Wouter de Boer   | projectlid        |
| Daniel Hofman    | projectlid        |
| Hylbren Rijnders | projectlid        |
| Mees van Dijk    | projectlid        |
| Jacob de Boer    | projectbegeleider |
| Reimer Wartena   | opdrachtgever     |



# 3 Acceptatiecriteria

## 3.1 Performance
Om de performance van de applicatie op niveau te krijgen zal de applicatie aan een aantal eisen moeten voldoen. Voor het werken op meerdere telefoons zal de applicatie schaalbaar moeten zijn. Gebruiker mag geen 'lag-spikes' merken bij het gebruiken van de applicatie en mag geen lange laadtijden tegenkomen.

## 3.2 Beheerbaarheid
Voor het beheer van de applicatie zal er een teststraat ontwikkeld worden die kan worden gebruikt voor unittests.
Verder om de code zelf te beheren zal er goede documentatie moeten zijn. Deze documentatie moet te begrijpen zijn voor iedereen, ook mensen met weinig of geen technische kennis. Wanneer dit project is afgelopen, moet het duidelijk zijn in de documentatie hoe het project is verlopen, wat is er goed gegaan en wat ging slecht.

## 3.3 Betrouwbaarheid
Het is erg van belang dat het systeem altijd werkt in een project als dit. Dit project zorgt ervoor dat je niet meer al je pasjes bij je hoeft te hebben omdat deze altijd op je telefoon digitaal beschikbaar zijn. Het is hierom heel belangrijk dat het systeem werkt, anders heb je geen toegang tot je persoonlijke gegevens. Een voorbeeld kan zijn wanneer je wordt aangehouden en je moet je rijbewijs laten zien. Wanneer het systeem het niet doet en je niet je rijbewijs kan laten zien, kan dit problemen veroorzaken.

## 3.4 Beveiliging
Voor een applicatie als dit is beveiliging natuurlijk een van de meest belangrijke aspecten. Al je persoonlijke gegevens zijn hier opgeslagen en dat kan flink fout aflopen als die gehackt wordt. De applicatie moet hiervoor een inlogsysteem hebben met gebruikersnaam en wachtwoord. Voor alle data dat wordt rondgestuurd, zal gebruik worden gemaakt van cryptografie. Ook zal de wallet waar je al je persoonlijke gegevens in hebt een veilige optie moeten hebben om een backup te maken en mogelijk verloren data te recoveren. 

## 3.5 Funcitonaliteit
De functionaliteit zal worden beoordeeld op basis van goedgekeurde Use Case Specifications. (Dit is verder toegelicht in het 'Use Cases' document)

## 3.6 Gebruiksvriendelijkheid
Om de app gebruikersvriendelijk te maken, moet de app kunnen worden gebruikt door iedereen. De app moet zodanig duidelijk zijn dat mensen van elke leeftijd, ook ouderen en kleine kinderen, snappen hoe de app gebruikt moet worden. Sommige mensen kunnen ook moeite hebben met lezen. Hiervoor moet je lettergrootte ook veranderbaar zijn. Dit kan bijvoorbeeld wanneer je je eigen telefoon lettergrootte groot hebt staan, dat de app dit ook automatisch overneemt. De lay-out van de app moet overzichtelijk zijn, de icoontjes moeten snel inzicht geven over de functie van de mogelijke knoppen en wanneer instructies worden gegeven, moet dit ook te lezen zijn en duidelijk zijn voor elke gebruiker.

## 3.7 Standaards
Wanneer je praat over al je persoonlijke gegevens online hebben, komt al snel de wet aan bod. Gezien dit project een compleet nieuw concept is, zal de wetgeving hier zich ook op moeten aanpassen. Hier moet duidelijk zijn wanneer je welke informatie moet vrijgeven en wanneer je je recht behoud op privacy.

## 3.8 Documentatie
De documentatie van het project moet te begrijpen zijn voor iedereen, ook mensen met weinig of geen technische kennis. Wanneer het project is afgelopen, moet het duidelijk zijn in de documentatie hoe het project is verlopen, wat is er goed gegaan en wat ging slecht. Gezien het eindproduct een proof of concept is, is de documentatie extra relevant. Gezien het doel van dit project kennis opdoen is, gaat het minder om het uiteindelijke eindproduct, maar meer om het proces. In de documentatie moet duidelijk terug te lezen zijn waarom er gekozen is voor bepaalde architectuurkeuzes met een onderbouwing. 