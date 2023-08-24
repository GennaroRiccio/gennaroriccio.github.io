---
title: "TIPS #1 DotNet View Transitive Packages in .NET Solution"
meta_title: "DotNet View Transitive Packages in .NET Solution"
description: "DotNet View Transitive Packages in .NET Solution"
date: 2023-08-24T05:00:00Z
image: "/images/microsoftnet.png"
categories: ["Tips", "Developer"]
author: "Gennaro Riccio"
tags: ["dotnet", "tips","packages"]
draft: false
---

## Comando

La cli dotnet ci mette a disposizione una comoda funzione per avere la lista di tutti i packages referenziati in un progetto:


        dotnet list Rebus.Queue.Api.csproj package

<img src="..\dotnet-list-package.png">

Se vogliamo vedere i pacchetti transiviti ovvero i packages delle DLL di terze parti il comando da usare è:

        dotnet list Rebus.Queue.Api.csproj package --include-transitive

<img src="..\dotnet-list-package-transitive.png">

Enjoy =)


 <font size="1"> Don't Accept the Defaults - Abel Wang </font>