---
title: "Rebus"
meta_title: ""
description: ""
date: 2023-08-16T05:00:00Z
image: "/images/backstage.png"
categories: ["Application", "Developer"]
author: "Gennaro Riccio"
tags: ["backstage", "spotify","developer"]
draft: true
---

## Backstage Spotify


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