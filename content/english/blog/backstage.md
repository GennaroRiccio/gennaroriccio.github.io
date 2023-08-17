---
title: "Backstage Spotify - building developer portals"
meta_title: "Backstage Spotify"
description: "building developer portals"
date: 2023-08-16T05:00:00Z
image: "/images/backstage.png"
categories: ["Application", "Developer"]
author: "Gennaro Riccio"
tags: ["backstage", "spotify","developer"]
draft: false
---

Mi è capitato nella mia lunga carriera (30 anni) di lavorare per diverse aziende, ma trovarne una che aveva un'adeguata documentazione sugli standard per sviluppare è stato pura utopia.

Il senior o l'architect di turno che con malavoglia e malagrazia ti spiegava due cose in croce e per il resto dovevi sputare sangue, mi chiedo a che pro? Perchè sprecare tempo di una risorsa quando ci sono tool (open source) che permettono di documentare bene un progetto, dettagliare le specifiche tecniche, gli standard di sviluppo e la creazione di template con tutto il necessario per permettere ad uno sviluppatore di integrarsi in maniera veloce in una nuova realtà di sviluppo.

Uno di questi è Backstage creato dalla fucina di sviluppo di Spotify.

[backstage.io](https://backstage.io/ "backstage site") Il link del prodotto

## Backstage Spotify

E' una piattaforma open source per la creazione di developer portal. Grazie a un catalogo software centralizzato, Backstage rimette ordine nei microservizi e nell'infrastruttura e consente ai team di prodotto di distribuire rapidamente codice di alta qualità, senza compromettere l'autonomia.

Out of the box, Backstage include:

* Backstage Catalogo software per la gestione di tutti i software (microservices, libraries, data pipelines, websites, ML models, etc.)
* Backstage Software Templates per avviare rapidamente nuovi progetti e standardizzare il tooling con le best practice dell'organizzazione.
* Backstage TechDocs per semplificare la creazione, la manutenzione, la ricerca e l'utilizzo della documentazione tecnica, utilizzando un approccio "docs like code".
* Inoltre, un ecosistema crescente di plugin open source che espandono ulteriormente la personalizzazione e le funzionalità di Backstage.

## Funzionalità

Tra le principali funzionalità:

**_Catalogo Software_**

<img src="https://backstage.io/assets/images/software-catalog-home-c6be1611f7b84313d64f3156a9a8bb19.png">

**_Catalogo delle API_**

<img src="..\backstage_apis.png">


**_Software template_**

<img src="https://backstage.io/assets/images/create-c1b5255bb8f53b9435895017e096f01e.png">

**_TechDocs Documentation_**
Solutione docs-lilke-code, la documentazione è scritta con file Markdown ed è ospitata assieme al codice sorgente (esempio: readme.md) questa viene importata da Backstage creando una raccolta documenti centralizzata.

### Source code hosting providers

| Source Code Hosting Provider | Support Status |
| ---------------------------- | -------------- |
| GitHub                       | Yes ✅         |
| GitHub Enterprise            | Yes ✅         |
| Bitbucket                    | Yes ✅         |
| Azure DevOps                 | Yes ✅         |
| Gerrit                       | Yes ✅         |
| GitLab                       | Yes ✅         |
| GitLab Enterprise            | Yes ✅         |

### File storage providers

| File Storage Provider             | Support Status |
| --------------------------------- | -------------- |
| Local Filesystem of Backstage app | Yes ✅         |
| Google Cloud Storage (GCS)        | Yes ✅         |
| Amazon Web Services (AWS) S3      | Yes ✅         |
| Azure Blob Storage                | Yes ✅         |
| OpenStack Swift                   | Community ✅   |


## PLUGIN
Altra interessante funzionalità sono la vasta gamma di plugin.

[Plugin](https://backstage.io/plugins)

Ad esempio i plugin di integrazione con la CI/CD che permettono di tenere monitorato i tools di CI/CD
### CI/CD Plugin
| PlugIn                       | 
| ---------------------------- | 
| Azure Pipeline               | 
| Gitlab                       | 
| Github Actions               | 
| Octopus Deploy               | 
| Jenkins                      | 

### GitLab PlugIn
<img src="https://raw.githubusercontent.com/immobiliare/backstage-plugin-gitlab/main/assets/backstage_gitlab_pipeline_information.png">

## Cloudnative
Oltre all'installazione on prem Backstage può essere installato anche su Kubernaters. Infatti fa parte dei progetti inclusi dell'incubazione CNCF 

## Conclusioni
Sicuramente un prodotto che in ambito di sviluppo dovrebbe essere presente, specialmente in quelle realtà dove il riciclo di sviluppatori è alto ma non solo, tenere una documentazione aggiornata degli stardard dei sofware aiuta anche dopo un certo periodo di tempo a tornare su soluzioni ferme da un pò di tempo.