---
title: "TIPS #4 Central Package Management Nuget in .NET project"
meta_title: "Central Package Management Nuget nei progetti .Net "
description: "How centralize nuget package"
date: 2024-01-04T05:00:00Z
image: "/images/microsoftnet.png"
categories: ["Tips", "Developer"]
author: "Gennaro Riccio"
tags: ["dotnet", "tips","nuget"]
draft: false
---

## NUGET Centraliziamo i Package nei progetti .NET
Con la versione di Nuget 6.2 è possibile centralizzare le dipendenze di package aggiungendo semplicemente il file __Directory.Packages.props__ al progetto.

Nel file .props creato occorre innanzitutto abilitare il central package managment tramite il tag: 
```xml 
<ManagePackageVersionsCentrally>true</ManagePackageVersionsCentrally>
```
Ed infine spostare i package con il version del pacchetto utilizzato.

Se ad esempio in un .csproj abbiamo una configurazione di package del tipo:  
```xml
<Project Sdk="Microsoft.NET.Sdk">
    <PropertyGroup>
        <OutputType>Exe</OutputType>
        <TargetFramework>net8.0</TargetFramework>
        <ImplicitUsings>enable</ImplicitUsings>
        <Nullable>enable</Nullable>
        <AssemblyVersion>1.2024.1.3</AssemblyVersion>
        <FileVersion>1.2024.1.3</FileVersion>
    </PropertyGroup>
    <ItemGroup>
      <PackageReference Include="Microsoft.Data.SqlClient" Version="5.1.2" />
      <PackageReference Include="Newtonsoft.Json" Version="13.0.3" />
    </ItemGroup>
    <ItemGroup>
      <ProjectReference Include="..\DirectoryPackagesTest.Lib\DirectoryPackagesTest.Lib.csproj" />
    </ItemGroup>
</Project>
```
Basterà semplicemente cancellare il tag Version dal PackageReference e spostare l'ItemGroup compreso di Vesion nel file Directory.Packages.props, quindi nel caso in esempio avremo:

__Directory.Packages.props__

```xml
<Project>
    <PropertyGroup>
        <CentralPackageTransitivePinningEnabled>true</CentralPackageTransitivePinningEnabled>
    </PropertyGroup>
    <ItemGroup>
        <PackageReference Include="Newtonsoft.Json" Version="13.0.3" />
        <PackageReference Include="Microsoft.Data.SqlClient" Version="5.1.2" />
    </ItemGroup>
</Project>
```
Mentre il contenuto del nostro .csproj diventa:
```xml
<Project Sdk="Microsoft.NET.Sdk">
    <PropertyGroup>
        <OutputType>Exe</OutputType>
        <TargetFramework>net8.0</TargetFramework>
        <ImplicitUsings>enable</ImplicitUsings>
        <Nullable>enable</Nullable>
        <AssemblyVersion>1.2024.1.3</AssemblyVersion>
        <FileVersion>1.2024.1.3</FileVersion>
    </PropertyGroup>
    <ItemGroup>
      <PackageReference Include="Microsoft.Data.SqlClient" />
      <PackageReference Include="Newtonsoft.Json" />
    </ItemGroup>
    <ItemGroup>
      <ProjectReference Include="..\DirectoryPackagesTest.Lib\DirectoryPackagesTest.Lib.csproj" />
    </ItemGroup>
</Project>
```
In questo modo per Solution con tanti progetti abbiamo un unico punto centralizzato dove avere un unico versionamento dei package nuget.

## Rules
E' possibile che ogni progetto si una Solution abbia il suo Directory.Packages.props la regola principale di lettura è la seguente: viene valutato un solo file .props per progetto.

Se ad esempio ci troviamo un una codizione del genere:
```
Repository
 |-- Directory.Packages.props
 |-- Solution1
     |-- Directory.Packages.props
     |-- Project1
 |-- Solution2
     |-- Project2
```
Il progetto1 leggerà .props nella cartella Repository\Solution1
Il progetto2 leggerà .props nella cartella Repository\

## Transitive package
E' possibile gestire le versioni dei transitive package semplicemente abilitado la funzione tramite il tag:
```xml 
<CentralPackageTransitivePinningEnabled>true</CentralPackageTransitivePinningEnabled>
```

E specificando la versione in override del package nel .csproj con il tag __VersionOverride__
```xml 
<PackageReference Include="Microsoft.Data.SqlClient" VersionOverride="7.0.0" />
```

## Conclusioni
Questa funzionalità di nuget permette di gestire in maniera precisa e ordinata i packages che a livello di Devop molte volte creano numerosi problemi specialmente con solution molto grosse e gestite male in caso gruppi di lavoro grossi.

Riferimenti:
[NUGET Central Package Management]( https://devblogs.microsoft.com/nuget/introducing-central-package-management/?WT.mc_id=DT-MVP-5004452 "NUGET Central Package Nabagement")

Enjoy =)


 <font size="1"> Don't Accept the Defaults - Abel Wang </font>