---
title: "TIPS #5 Scan NuGet Packages for Security Vulnerabilities"
meta_title: "Scan NuGet Packages for Security Vulnerabilities"
description: "How to Scan NuGet Packages for Security Vulnerabilities"
date: 2024-01-22T05:00:00Z
image: "/images/microsoftnet.png"
categories: ["Tips", "Developer"]
author: "Gennaro Riccio"
tags: ["dotnet", "tips","nuget"]
draft: false
---

## NUGET Scan dei Packages per vulnerabilità di sicurezza 
Nell'era dove la sicurezza è il core principale, non può mancare un controllo sui packeges nuget che referenziamo alle nostre solution.
Dal 2021 la cli di donet ha messo a disposizione una funzionalità che dovrebbe essere inclusa di defualt in tutte le pipeline di build e localmente utilizzata da ogni sviluppatore.

```
 dotnet list package --vulnerable
```

Lanciando il comando dove riesiede la nostra solution ci verranno mostrati i packages he soffrono di vulnerabilita la relativa gratità e il link dove viene descritta la vulnerabilità

Aggiungengo il parametro __--include-transitive__ è possibile scansionare i packages referenziati all'interno di altri packages.

```
   Il progetto `CippoLippo.UTestExample.UnitTest` contiene i pacchetti vulnerabili seguenti
   [net6.0]:
   Pacchetto transitivo                  Risolti   Gravità   URL di avviso
   > System.Net.Http                     4.3.0     High      https://github.com/advisories/GHSA-7jgj-8wvc-jh57
   > System.Text.RegularExpressions      4.3.0     High      https://github.com/advisories/GHSA-cmhx-cq75-c4mj
```

## Conclusioni
La funzionalità in realtà viene messa a disposizione da nuget.org per poi essere utilizzata dal comando dotnet ed è sicuramente un must have per avere sempre un codice complaince quanto più possbile con la sicurezza.

Riferimenti:
[Scan NuGet Packages](https://devblogs.microsoft.com/nuget/how-to-scan-nuget-packages-for-security-vulnerabilities/ "Scan NuGet Packages")

Enjoy =)

 <font size="1"> Don't Accept the Defaults - Abel Wang </font>