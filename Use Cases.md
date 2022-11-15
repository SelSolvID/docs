# Project 4 SSI Use Case Models

## Documenthistorie

| **Datum**  | **Versie** | **Beschrijving** | **Auteur**  |
| ---------- | ---------- | ---------------- | ----------- |
| 10-10-2022 | 0.1        | Initiele versie  | HDJRijnders |
|            |            |                  |             |
|            |            |                  |             |

# Distributie

| **naam** | **0.1** |     |     |
| -------- | ------- | --- | --- |

## Accordering Document

| **Namens Opdrachtgever** | **Naam bedrijf** |
| ------------------------ | ---------------- |
| Naam ondertekenaar       | Naam bedrijf (?) |

| **Namens opdrachtnemer** | **Naam bedrijf** |
| ------------------------ | ---------------- |
| Naam ondertekenaar       | Selsovid         |

# Inhoudsopgave

1. [Inleiding](#inleiding)
   1. [Doel van dit document](#doelvandoc)
   2. [Referenties](#referenties)
2. [Opsomming Actors](#opsommingactors)
3. [Opsomming Use Cases](#opsommingusecases)
4. [Use Case Diagrams](usecasediagram)

# 1. Inleiding <a name="inleiding"></a>

## 1.1 Doel van dit document <a name="doelvandoc"></a>

Dit document dient ter ondersteuning van project jaar 4: SSI (Self sovereign
id), het belicht de use cases en bijbehorende actors, ook wordt de scpe van de
opdracht en worden use cases gerangschikt en geprioritiseerd.

## 1.2 Referenties <a name="referenties"></a>

Dit is een lijst van alle documenten waarnaar in dit use case model worden
verwezen of op basis waarvan dit document tot stand is gekomen.

| **Titel**                        | **Versie** | **Auteur**    | **Vindplaats**                                                                                                                              |
| -------------------------------- | ---------- | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| ssi-opdracht-omschrijving-v1.pdf | 1          | Jacob de Boer | https://blackboard.hanze.nl/bbcswebdav/pid-5585293-dt-content-rid-80696564_2/courses/itvt.1803.4-2-se-1819/ssi-opdracht-omschrijving-v1.pdf |
|                                  |            |               |                                                                                                                                             |

# 2. Opsomming actors <a name="opsommingactors"></a>

| **Code** | **Actor**                                | **Omschrijving**                               | **Gewicht** |
| -------- | ---------------------------------------- | ---------------------------------------------- | ----------- |
| A1       | Gebruiker                                | De gebruiker van de SSI                        |             |
| A2       | Onderwijsinstelling middelbaar onderwijs | Instantie middelbare schooldiploma             |             |
| A3       | Onderwijsinstelling vervolgonderwijs     | Instantie diploma vervolgonderwijs             |             |
| A4       | Uitgiftepunt Rijbewijs                   | De uitgever van rijbewijzen in nederland       |             |
| A5       | Werkgever                                | Werkgever van degene waarvan het SSI is.       |             |
| A5       | verhuurder                               | Verhuurder van goederen                        |             |
| A6       | Verkoper                                 | Een verkoper van een winkel                    |             |
| A7       | Bank                                     | Bankinstelling om een hypotheek te verstrekken |             |

# 3. Opsomming Use Cases <a name="opsommingusecases"></a>

| **Code** | **Use case naam**                        | **Omschrijving**                                                                                                          | **Gewicht** | **prioritering** |
| -------- | ---------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- | ----------- | ---------------- |
| UC1      | Kopen van leeftijdsgebonden artikelen    | Een gebruiker wilt alcohol kopen, benodigd is de leeftijd.                                                                | 1           | 1                |
| UC2      | Afsluiten van een dienst met voorwaarden | Een gebruiker wilt een hypotheek afsluiten om een huis te kunnen kopen, benodigd zijn de identiteit, arbeidsovereenkomst. |             | 4                |
| UC3      | Solliciteren                             | Een gebruiker wilt solliciteren, daar zijn een ID en de diplomas van de middelbare school en de HBO instelling voor nodig |             | 3                |
| UC4      | Huren van goederen                       | Een gebruiker wilt een auto huren, daar is vanuit de gebruiker een ID en een rijbewijs nodig                              |             | 2                |

# 4. Use Case Diagram <a name="usecasediagram"></a>

```plantuml
@startuml
actor "Gebruiker" as user
actor "Onderwijsinstelling  middelbaar onderwijs" as omo
actor "Onderwijsinstelling  vervolgonderwijsonderwijs" as ovo
actor "Uitgiftepunt rijbewijs" as ur
actor "Werkgever" as wg
actor "Autoverhuurder" as vh
actor "Verkoper" as vk
actor "Bank" as b


rectangle SSI {
  left to right direction
  usecase "Toon leeftijd" as UC1
  usecase "Sluit hypotheek af" as UC2
  usecase "Solliciteer" as UC3
  usecase "Huurt auto" as UC4
}


user --> UC1 : verschaft leeftijd
UC1 <-- vk : vereist leeftijd

user --> UC2 : verschaft identiteit
UC2 <-- b : vereist arbeidsovereenkomst, identiteit
wg <-- UC2 : verschaft arbeidsovereenkomst

user --> UC3 : verschaft identiteit
UC3 <-- wg : Vereist Diplomas
UC3 <-- omo: Verschaft Diploma
UC3 <-- ovo: Verschaft Diplomas

user --> UC4
UC4 <-- vh : vereist rijbewijs, identiteit
UC4 <-- ur : verschaft rijbewijs
@enduml
```

# Extra use cases

In een brainstormsessie heeft de projectgroep een mogelijke aanvulling op de use
cases bedacht. Deze zit niet in de besproken scope van dit project, en is
volgens het MoSCoW model een Wont have. Toch wordt deze hier onder
gedocumenteerd, in het kader van volledigheid van documentatie.

## Peer to peer statement issuing

Binnen het beoogde systeem is mogelijkheid tot een uitbreiding. In het
beschreven systeem staan drie duidelijk gescheiden rollen beschreven: issuer,
verifier en holder. De projectgroep kwam al snel met het besef dat een verifier
en holder vaak hetzelfde soort mensen zijn. In een supermarkt werken gewone,
normale mensen. Analoog hieraan is dat met fysieke identiteitskaarten het ook zo
werkt dat je je eigen kaart aan iedereen kan laten zien en iedereen kan
controleren dat de kaart klopt en welke gegevens er op de kaart staan.  
Hierin zijn holder en verifier dus hetzelfde. Hieruit kwam het idee dat er geen
twee verschillende apps worden gebouwd voor deze twee soorten gebruikers, in
plaats daarvan wordt er een enkele app gebouwd met functionaliteit voor beide.

Een uitbreiding hierop is als je de issuer rol ook algemener bekijkt. Het
huidige systeem is gebouwd op het issuen van officiele documenten, dingen zoals
rijbewijs of opleidingsdiploma's. in algemene zin zijn dit gewoon "statements"
over een persoon. Je kunt het zien als "het RDW maakt als 'statement' over
Pietje dat hij mag rijden".

Dit systeem kan nog algemener worden gemaakt door ook iedereen een issuer te
laten zijn. Iedereen kan dan een "statement" over een ander persoon uitgeven.
Deze andere persoon kan vervolgens deze "statement" aan anderen laten zien met
bewijs dat persoon X dit heeft ondertekend. Een belangrijk besef is dan dat
verschillende handtekeningen enorm verschillende legitimiteit hebben.  
Als Pietje over Jantje de "statement" maakt 'Hij kan wel rijden" heeft dat niet
dezelfde legitimiteit als wanneer het RDW dat doet.  
Een belangrijk subsysteem dat hierbij nodig is is een manier voor mensen om te
weten wat de legitimiteit van een ondertekenaar is, en in welke context.

In dit verhaal is een "statement" een meer algemeen woord voor wat tot nu toe
een verifiable credential is genoemd.
