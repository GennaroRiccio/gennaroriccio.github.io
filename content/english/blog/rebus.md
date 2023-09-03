---
title: "Rebus lean service Bus implementation for .Net"
meta_title: "Rebus"
description: "lean service Bus implementation for .Net"
date: 2023-09-03T05:00:00Z
image: "/images/rebus_logo.png"
categories: ["Application", "Developer"]
author: "Gennaro Riccio"
tags: ["rebus", "rabbitmq","developer","charp"]
draft: false
---

## Rebus .Net
Sempre per la serie "Don't Accept the Defaults" ormai mio mantra di vita, cercavo una libreria semplice, veloce, ed affidabile per gestire al meglio le code di RabbitMQ. Rebus segue la filosofia "Message buses without smarts" (Bus di messaggi senza intelligenza) e permette con poche righe di codice di implementare microservizi che si agganciano alle code RabbitMQ in maniera veloce ed efficace.

Il repository git dove trovare Rebus : https://github.com/rebus-org

## Funzionalità
Il repository è bello fornito Rebus può essere utilzzato non solo con RabbitMQ ma anche con altro.

Alcuni esempi interessanti di integrazione:

* Rebus.MongoDb   permette di gestire la persistenza attraverso mongoDB
* Rebus.AutoScaling permette di scalare i worker process in automatico.

Qui l'elenco completo: https://github.com/orgs/rebus-org/repositories?type=all


## Esempio di utilizzo.

Immaginiamo una webApi che faccia da producer, invia delle informazioni ad esempio i dati per inviare un email ad una coda RabbitMQ.
Di quali packages abbiamo bisogno:

<img src="..\rebus_packages.png">

Referenziati i packages implementiamo il services di Rebus con le configurazioni:

<img src="..\rebus_code.png" width="70%" height="70%">

Definiamo il tipo di Transport nel caso di un producer di tipo OneWayClient (invia dati) e l'url di connessione a RabbitMQ con le credenziali.

Il numero di workers e il numero di messaggi da gestire in parallelo trmiate i metodi:

* .SetMaxParallelism
* .SetNumberOfWorkers

A questo punto non ci resta che andare a definire il nostro metodo send email:

<img src="..\rebus_apisendmail.png" width="70%" height="70%">

Iniettiamo il Bus Rebus tramite l'interfaccia IBUS e tramite il metodo Publish inviamo i messaggi alla coda RabbitMQ. Nel esempio su vengono creati dei dati fakse per simulare dei dati.

Scriviamo il consumer che potrebbe essere un workerprocess o un'altra webapi che riceve le informazioni per l'invio email.
Il nostro consumer avrà bisogno di un handler che si innesca quando la coda rabbit viene popolata di messaggi, il Transport in questo caso è di tipo RabbitMQ per consumare i messaggi.

<img src="..\rebus_consumer.png" width="70%" height="70%">

Definiamo la nostra classe Handler dove risiederà la logica di gestione dei messaggi letti dalla coda:

<img src="..\rebus_handler.png" width="70%" height="70%">


## DEMO

<img src="..\rebus_demo.gif" >

## Conclusioni
Rebus offre sicuramente in maniera veloce l'integrazione con RabbitMQ all'interno dei nostri applicativi e/o microservizi. Il concetto di BUS system presente da anni nel mondo dello sviluppo ma ancora poco sfruttato e conosciuto dai più.



<font size="1"> Don't Accept the Defaults - Abel Wang </font>