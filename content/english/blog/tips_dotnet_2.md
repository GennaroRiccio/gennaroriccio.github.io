---
title: "TIPS #2 Enhancement Debug Application"
meta_title: "Enhancement Debug Application"
description: "Tell the debugger what to show using the DebuggerDisplay Attribute"
date: 2023-12-22T05:00:00Z
image: "/images/microsoftnet.png"
categories: ["Tips", "Developer"]
author: "Gennaro Riccio"
tags: ["dotnet", "tips","debug"]
draft: false
---

## Debug

Un interessante utilizzo della libreria System.Diagnostic è quello settare in fase di debug cosa visualizzare nell'Ide.
Questo è comodo per analizzare nel dettaglio una classe in particolare e solo determinate variabili.

Ad esempio supponiamo di avere questa classe:

<img src="..\tips2_debug1.png">
      
Normalmente mandando in esecuzione e mettendo un punto di interruzione sull'inizializzazione dell'oggetto Logic dell'esempio, l'Ide non ci mostra le informazioni delle variabili:

<img src="..\tips2_debug1b.png">

Tramite la libreria System.Diagnostics abbiamo una serie di decoratori tra i quali DebuggerDisplay che ci permette di specificare quali variabili o oggetti vogliamo visualizzare nella fase di Debug:

<img src="..\tips2_debug2.png">

In debug avremo tutte le informazioni richieste:

<img src="..\tips2_debug2b.png">

Per approfondimenti ed altri decoratori: [learn.microsoft.com](https://learn.microsoft.com/en-us/visualstudio/debugger/using-the-debuggerdisplay-attribute?view=vs-2022 "learn.microsoft.com")

Enjoy =)


 <font size="1"> Don't Accept the Defaults - Abel Wang </font>