---
title: "Gestiamo i secrets di HashiCorp Vault con HashiCorp Terraform"
meta_title: "Terraform e Vault"
description: "gestione dei secrets Vault con Terraform"
date: 2023-08-23T05:00:00Z
image: "/images/terra_vault.png"
categories: ["Terraform", "Hashicorp","Vault"]
author: "Gennaro Riccio"
tags: ["terraform", "vault","hashicorp"]
draft: false
---

Terraform, non solo IaC (Infrastructure as Code), chi usa terraform per gestire IaC ne conosce la potenza e la comodità una volta creato lo script per il deploy di una infrastruttura sul cloud e on-prem questo è replicabile all'infinito in diversi ambienti e modificabile per gestire lo scaling ad esempio o semplicamente cambiare le caratteristiche di una infrastruttura in meniera semplice e veloce.

Un approccio diverso ed utilizzare Terraform per gestire un secret mananager quali può essere l'altro prodotto di punta di HashiCorp: ***Vault***

# Ingredienti

Di cosa abbiamo bisogno per la Proof of Concept:

1. Hashicorp Vault
2. Hashicorp Terraform
3. Powershell Teminal

## Infrastruttura di TEST utilizzata

* Docker Desktop 
  * Docker Image Hashicorp Vault   
* HashiCorp Terraform 
  * Installazione in locale del tool 

## Installazione infrastruttura 
Riporto brevemente i passaggi per l'installazione dell'infrastruttura su un sistema Windows, per approfondimenti vi rimando ai relativi site e tutorial presenti in rete.

### Doker Desktop
E' possibile installare doker desktop dal site principale:
https://www.docker.com/products/docker-desktop/

Installazione semplice non richiede particolari conoscenze tecniche.

#### Docker Image Vault:
Per l'installazione di Vault basta lanciare la riga sotto 
```
docker run --name Vault --cap-add=IPC_LOCK `  
-e 'VAULT_LOCAL_CONFIG={"storage": {"file": {"path": "/vault/file"}}, "listener": [{"tcp": { "address": "0.0.0.0:8200", "tls_disable": true}}], "default_lease_ttl": "168h", "max_lease_ttl": "720h", "ui": true}' ` 
-p 8200:8200 hashicorp/vault:1.14 server
```
per i dettagli: https://hub.docker.com/r/hashicorp/vault

#### HashiCorp Terraform:
Da questo link si può scaricare il tool di terraform:
https://developer.hashicorp.com/terraform/downloads?product_intent=terraform


## Proof of Concept

Una volta che abbiamo la nostra infrastruttura possiamo in iniziare.

Fondamentali sono 2 variabili di ambiente per poter far dialogare Terraform con Vault:
* **VAULT_ADDR** = endpoint di accesso a Vault nel caso in un installazione su Docker sarà : http://localhost:8200 

* **VAULT_TOKEN** = Token di autenticazione su Vault. 

Componente fondamentale per Terraform è il provider, nel nostro caso quello di Vault.
I provider sono delle astrazioni logiche delle Api dei componenti su cui si deve interagire.

La documentazione completa del provider vault la si può trovare qui:
https://registry.terraform.io/providers/hashicorp/vault/latest/docs


Inoltre nel registry di Terraform si possono trovare tutti i provider con cui Terraform interagisce: https://registry.terraform.io/browse/providers


Definiamo il provider vault in questo modo:

```
provider "vault" {
  address = ""
}
```
lavorando in localhost ed avendo settato la variabile **VAULT_ADDR** l'address può anche non essere valorizzato. La best practice è valorizzare il campo.

Definiamo il resource di tipologia secret da utilizzare nel caso in esempio la tipologia di secret KV version 2 

```
resource "vault_mount" "kvv2" { 
  path        = "test-project"
  type        = "kv"
  options     = { version = "2" }
  description = "KV2 secret test-project application"
  lifecycle {
    ignore_changes = all
  }
}
```
- ***path*** dove andremo a salvare i secrets in vault nel nostro caso 'test-project'
- ***type*** key value secret (kv) e la versione = 2 definita in options.
- ***Lifecyle*** essendo la resource unica e in teoria non modificabile si utilizza il lifecycle ingnore_changes in modo che non si possano fare modifiche alla resource.

A questo punto siamo pronti per definire il resource del secret:

```
resource "vault_kv_secret_v2" "test" {
  mount               = vault_mount.kvv2.path
  name                = "secret-test"
  cas                 = 1
  delete_all_versions = false
  data_json =  file("data.json")
  
  custom_metadata {
    max_versions = 5
  }
}
```

- ***mount*** è il resuorce dove è definito il secret.
- ***name***  è il nome del secret da salvare.
- ***data_json*** il file json che contiene i secrets.

e nel custom_metadata definiamo quante versioni vogliamo tenere nello storico, in questo caso 5.

__Se lavorate con la versione Enterprice di Vault avete a disposizione nella definizione dei resource anche il tag NAMESPACE per poter gestire i secret nei namespace di Vault.__

La parte importante per l'automazione è il file data_json in questo file sono contenuti i secrets. 
Esempio di file json key/value dei nostri secrets legati al path test-project/secret-test

```
{
    "zip":"pippo",
    "foo":"pluto",
    "zep":"lippa",   
}
```

***Il nostro file PutSecrets.tf finale è questo:***

<img src="..\terraform_code.png" width="672" height="696">


***Verifichiamo la connesione verso Vault interrogando la lista dei secrets:***

       vault secrets list


<img src="..\vault-secret-list.gif" width="672" height="696">

Inizializziamo il workspace di terraform con il comando 

       terraform init

<img src="..\terraform-init.png" width="672" height="696">

Come possiamo osservare automaticamente il provider viene scaricato per poter essere pronto a gestire i nostri secrets. Tramite il conmando Plan abbiamo la possibilità di verificare che il nostro script sia corretto.

Infine applichiamo lo script per poter salvare i nostri secret in Vault tramite il comando apply lanciamo lo script:

       terraform apply -auto-approve

* -auto-approve permette l'esecuzione senza l'attesa uamana di conferma.

<img src="..\terraform-apply.gif" width="672" height="696">

il gioco è fatto avremo nel nostro secret manager vault i secrets salvati:

      vault kv get test-project/secret-test
                
<img src="..\vault-get-secrets.gif" width="672" height="696">

ed il gioco è fatto.

## Conclusioni

Abbiamo visto un uso alternativo di quello che di solito si vede in giro, ovvero deployare VM o reti con Terraform. Questo è ovviamente un piccolo esempio che può essere ampliato a dismisura ed esempio aggiungendo variabili che possono essere sostituite in maniera dinamica, cripatare/decriptare i file Json dei secret utilizzando Vault Transit, impletare il processo in un tool di CI/CD come sono ad esempio GitLab o Octopus Deploy e così via.
Si può spaziare varamente su vari fronti, ritengo che Terreform è uno strumento che nella borsa di DevOps deve essere prensete.