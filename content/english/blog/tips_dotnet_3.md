---
title: "TIPS #3 Unit Test Fake Data with Bogus"
meta_title: "Unit Test Fake Data with Bogus"
description: "Fake data for UnitTest with Bous"
date: 2023-12-27T05:00:00Z
image: "/images/microsoftnet.png"
categories: ["Tips", "Developer"]
author: "Gennaro Riccio"
tags: ["dotnet", "tips","unittest"]
draft: false
---

## Unit Test

Uno dei problemi quando si scrive una UT è quello di lavorare con dei dati fake, simulare accessi ai database etc.. un package comodo che ci viene in aiuto per generare fake data da dare in pasto alle nostre UT è sicuramente Bogus.

Scaricabile oltre che da nuget anche dal suo repository GitHub : [Bogus](https://github.com/bchavez/Bogus "Bogus")

Prendiamo ad esempio un progetto che contiene una classe Entity Framework, alla classe aggiungiamo un contesto per gestire un db in memoria.
Il db in memoria ci permette di poter lavorare con insert di dati fake:
<img src="..\tips3_ut1.png">
      
Creiamo la nostra UT che testerà un metodo che recupera la lista utenti. Sarà pressochè così:
<img src="..\tips3_ut2.png" width="70%" height="70%">

Creiamo i nostri dati fake aggiungendo il generatore di Bogus al costruttore del reposity in esame Users:
<img src="..\tips3_ut3.png" width="70%" height="70%">

Bogus ci mette a disposizione la classe Faker a cui mappiamo la nostra entity nel nostro caso User, mappati i nostri dati procediamo tramite il metodo Generate alla generazione dei dati nell'esempio 1000 record.

Lanciando la nostra UT abbiamo in nostri 1000 record da testare:
<img src="..\tips3_ut4.png">

E' possibile localizzare la lingua semplicamente aggiungendo all'inizializzazione del costruttore il local code Esempio: 
```csharp
var faker = new Faker("en");
```
### Tabella Local Code
| Locale Code  | Language                | | Locale Code  | Language                 |
|:------------:|:-----------------------:|-|:------------:|:------------------------:|
|`af_ZA`       |Afrikaans                 ||`fr_CH`       |French (Switzerland)      |
|`ar`          |Arabic                    ||`ge`          |Georgian                  |
|`az`          |Azerbaijani               ||`hr`          |Hrvatski                  |
|`cz`          |Czech                     ||`id_ID`       |Indonesia                 |
|`de`          |German                    ||`it`          |Italian                   |
|`de_AT`       |German (Austria)          ||`ja`          |Japanese                  |
|`de_CH`       |German (Switzerland)      ||`ko`          |Korean                    |
|`el`          |Greek                     ||`lv`          |Latvian                   |
|`en`          |English                   ||`nb_NO`       |Norwegian                 |
|`en_AU`       |English (Australia)       ||`ne`          |Nepalese                  |
|`en_AU_ocker` |English (Australia Ocker) ||`nl`          |Dutch                     |
|`en_BORK`     |English (Bork)            ||`nl_BE`       |Dutch (Belgium)           |
|`en_CA`       |English (Canada)          ||`pl`          |Polish                    |
|`en_GB`       |English (Great Britain)   ||`pt_BR`       |Portuguese (Brazil)       |
|`en_IE`       |English (Ireland)         ||`pt_PT`       |Portuguese (Portugal)     |
|`en_IND`      |English (India)           ||`ro`          |Romanian                  |
|`en_NG`       |Nigeria (English)         ||`ru`          |Russian                   |
|`en_US`       |English (United States)   ||`sk`          |Slovakian                 |
|`en_ZA`       |English (South Africa)    ||`sv`          |Swedish                   |
|`es`          |Spanish                   ||`tr`          |Turkish                   |
|`es_MX`       |Spanish (Mexico)          ||`uk`          |Ukrainian                 |
|`fa`          |Farsi                     ||`vi`          |Vietnamese                |
|`fi`          |Finnish                   ||`zh_CN`       |Chinese                   |
|`fr`          |French                    ||`zh_TW`       |Chinese (Taiwan)          |
|`fr_CA`       |French (Canada)           ||`zu_ZA`       |Zulu (South Africa)       |

## Comunitity Extension 
Esistono una serie di interessanti extension da usare con Bogus una molto interessante è BogusSQL che permette di generare script SQL per insert su DB

[BogusSQL](https://github.com/devangsinha/BogusSQL "BogusSQL")

## Conclusioni
Questa è solo una base di partenza, ovviamente alla nostra classe EF occorre aggiungere una parametrizzazione per gestire il db in memory per poterla utilizzare con le UT. Bogus offre svariate casi d'uso e con le extension della comunity oltre a quelle a pagamento è uno strumento che ogni sviluppatore e azienda dovrebbe avere a corredo per lo sviluppo del software.

Enjoy =)


 <font size="1"> Don't Accept the Defaults - Abel Wang </font>