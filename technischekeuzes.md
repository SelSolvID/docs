# Project 4 SSI Technische Keuzes

## Self Sovereign Identity

## Auteurs

Wouter de Boer  
Daniel Hofman  
Hylbren Rijnders  
Mees van Dijk

## 1.2 Referenties

| Titel       | Vindplaats               |
| ----------- | ------------------------ |
| RUP op maat | http://www.rupopmaat.nl/ |

## Documenthistorie

| **Datum** | **Versie** | **Beschrijving** | **Auteur**  |
| --------- | ---------- | ---------------- | ----------- |
| 17-1-2023 | 0.1        | Initiele versie  | HDJRijnders |

# Inhoudsopgave

- [Project 4 SSI Technische Keuzes](#project-4-ssi-technische-keuzes)
  - [Self Sovereign Identity](#self-sovereign-identity)
  - [Auteurs](#auteurs)
  - [1.2 Referenties](#12-referenties)
  - [Documenthistorie](#documenthistorie)
- [Inhoudsopgave](#inhoudsopgave)
- [1. Doel van dit document](#1-doel-van-dit-document)
- [2. Web app](#2-web-app)
- [3. App](#3-app)
- [4. API](#4-api)

# 1. Doel van dit document

Bij het orienteren op hoe wij dit project gingen vormgeven hebben wij een aantal
technische keuzes moeten maken

- Welke talen gaan de applicaties in geschreven worden?
- Welke frameworks en libraries gaan wij gebruiken?
- Hoe gaan wij CI/CD toepassen?
- Hoe gaat het project gedeployed worden?

# 2. Web app

Voor de frontend is er gebruik gemaakt van [svelte](https://svelte.dev/). Dit is
namelijk het most-loved web-framework volgens de stack overflow survey.  
Voor de backend van de web app gaan we Node.js gebruiken. Deze stond ook
gemiddeld hoog in de stack overflow survey.

# 3. App

De app voor holders en verifiers is geschreven in
[Kotlin](https://kotlinlang.org/). Dit was origineel gedaan omdat Kotlin bij een
onderzoek van stack overflow als een van de favorietste talen uit de bus was
gekomen, ons het leuk leek om nieuwe technieken te leren en omdat sinds enige
tijd Google Kotlin aanbeveelt als taal om android apps in te schrijven.

Gedurende het project zijn wij erachter gekomen dat hoewel android toch al 12
jaar in ontwikkeling is, sommige dingen nog niet helemaal 100% gedocumenteerd
zijn (het was een lijdensweg om Bluetooth werkend te krijgen bijvoorbeeld).

Ook werkt het niet mee dat de meeste tutorials op internet nog veeluit Java
zijn, natuurlijk is het mogelijk met bijvoorbeeld een Android Studio om deze
code om te zetten naar Kotlin maar dit is toch wel weer een extra stap.

Het mooie aan Kotlin is dan wel weer dat er
[Dataclasses](https://kotlinlang.org/docs/data-classes.html) kunnen worden
gebruikt, dit scheelt ontzettend in het gehalte boilerplate wat geschreven moet
worden.

# 4. API

De API is geschreven in met Node.js en Koa. Koa is een moderne variant van het
express web-framework voor Node.js. Verder wordt er typescript gebruikt voor de
code in Node.js. Typescript checkt de code voor type fouten en verbetert de
developer-experience door slimme suggesties.

Deze stack is erg goed bevallen, vooral omdat Node.js erg simpel is om mee te
beginnen.
