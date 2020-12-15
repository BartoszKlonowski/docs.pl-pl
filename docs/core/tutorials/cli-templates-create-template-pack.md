---
title: Tworzenie pakietu szablonów dla nowego dotnet
description: Dowiedz się, jak utworzyć plik CSPROJ, który będzie kompilować pakiet szablonów dla nowego polecenia dotnet.
author: adegeo
ms.date: 12/11/2020
ms.topic: tutorial
ms.author: adegeo
ms.openlocfilehash: 0d8ef9c158920ec49948215afb505a3753503286
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97512453"
---
# <a name="tutorial-create-a-template-pack"></a>Samouczek: Tworzenie pakietu szablonów

Za pomocą platformy .NET można tworzyć i wdrażać szablony generujące projekty, pliki, nawet zasoby. Ten samouczek jest trzecią częścią serii, która zawiera informacje na temat tworzenia, instalowania i odinstalowywania szablonów do użycia z `dotnet new` poleceniem.

W tej części serii dowiesz się, jak:

> [!div class="checklist"]
>
> * Utwórz \* projekt. csproj, aby skompilować pakiet szablonów
> * Konfigurowanie pliku projektu do pakowania
> * Instalowanie szablonu z pliku pakietu NuGet
> * Odinstalowywanie szablonu według identyfikatora pakietu

## <a name="prerequisites"></a>Wymagania wstępne

* Ukończ [część 1](cli-templates-create-item-template.md) i [część 2](cli-templates-create-project-template.md) tej serii samouczków.

  Ten samouczek używa dwóch szablonów utworzonych w pierwszych dwóch częściach tego samouczka. Możesz użyć innego szablonu, tak długo, jak skopiujesz szablon jako folder do folderu _working\templates \\_ .

* Otwórz Terminal i przejdź do folderu _roboczego \\_ .

## <a name="create-a-template-pack-project"></a>Tworzenie projektu pakietu szablonów

Pakiet szablonów to jeden lub więcej szablonów pakowanych do pliku. Podczas instalowania lub odinstalowywania pakietu wszystkie szablony zawarte w pakiecie są dodawane lub usuwane odpowiednio. Poprzednie części tej serii samouczków działały tylko z poszczególnymi szablonami. Aby udostępnić niespakowany szablon, należy skopiować folder szablonu i zainstalować go za pośrednictwem tego folderu. Ponieważ pakiet szablonów może mieć więcej niż jeden szablon w tym samym pliku, udostępnianie jest łatwiejsze.

Pakiety szablonów są reprezentowane przez plik pakietu NuGet (_. nupkg_). Podobnie jak każdy pakiet NuGet, można przekazać pakiet szablonów do źródła danych NuGet. `dotnet new -i`Polecenie obsługuje instalowanie pakietu Template Pack z kanału informacyjnego pakietu NuGet. Ponadto można bezpośrednio zainstalować pakiet szablonów z pliku _. nupkg_ .

Zwykle plik projektu C# jest używany do kompilowania kodu i tworzenia danych binarnych. Jednak projekt może być również używany do generowania pakietu szablonów. Zmieniając ustawienia elementu _. csproj_, można zapobiec kompilacji dowolnego kodu, a zamiast tego dołączyć wszystkie zasoby szablonów jako zasoby. Po skompilowaniu tego projektu tworzy pakiet NuGet pakietu szablonów.

Tworzony pakiet będzie obejmował [szablon elementu](cli-templates-create-item-template.md) i [szablon pakietu](cli-templates-create-project-template.md) utworzony wcześniej. Ze względu na to, że dwa szablony są pogrupowane w folderze _working\templates \\_ , możemy użyć folderu _roboczego_ dla pliku _. csproj_ .

W terminalu przejdź do folderu _roboczego_ . Utwórz nowy projekt i ustaw dla niego nazwę `templatepack` i folder wyjściowy w bieżącym folderze.

```dotnetcli
dotnet new console -n templatepack -o .
```

`-n`Parametr ustawia nazwę pliku _. csproj_ na _templatepack. csproj_. `-o`Parametr tworzy pliki w bieżącym katalogu. Powinien zostać wyświetlony wynik podobny do następującego: dane wyjściowe.

```dotnetcli
dotnet new console -n templatepack -o .
```

```console
The template "Console Application" was created successfully.

Processing post-creation actions...
Running 'dotnet restore' on .\templatepack.csproj...
  Restore completed in 52.38 ms for C:\working\templatepack.csproj.

Restore succeeded.
```

Następnie otwórz plik _templatepack. csproj_ w ulubionym edytorze i Zastąp zawartość następującym kodem XML:

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <PackageType>Template</PackageType>
    <PackageVersion>1.0</PackageVersion>
    <PackageId>AdatumCorporation.Utility.Templates</PackageId>
    <Title>AdatumCorporation Templates</Title>
    <Authors>Me</Authors>
    <Description>Templates to use when creating an application for Adatum Corporation.</Description>
    <PackageTags>dotnet-new;templates;contoso</PackageTags>

    <TargetFramework>netstandard2.0</TargetFramework>

    <IncludeContentInPack>true</IncludeContentInPack>
    <IncludeBuildOutput>false</IncludeBuildOutput>
    <ContentTargetFolders>content</ContentTargetFolders>
    <NoWarn>$(NoWarn);NU5128</NoWarn>
  </PropertyGroup>

  <ItemGroup>
    <Content Include="templates\**\*" Exclude="templates\**\bin\**;templates\**\obj\**" />
    <Compile Remove="**\*" />
  </ItemGroup>

</Project>
```

`<PropertyGroup>`Ustawienia w pliku XML powyżej są podzielone na trzy grupy. Pierwsza grupa zajmuje się właściwościami wymaganymi dla pakietu NuGet. Trzy `<Package*>` Ustawienia muszą wykonać przy użyciu właściwości pakietu NuGet, aby zidentyfikować pakiet w źródle danych NuGet. W `<PackageId>` celu odinstalowania pakietu Template Pack o pojedynczej nazwie zamiast ścieżki do katalogu zostanie użyta wartość. Można go również użyć do zainstalowania pakietu Template Pack ze źródła danych NuGet. Pozostałe ustawienia, takie jak `<Title>` i, `<PackageTags>` muszą zawierać metadane wyświetlane w źródle danych NuGet. Aby uzyskać więcej informacji na temat ustawień NuGet, zobacz [Właściwości narzędzia NuGet i programu MSBuild](/nuget/reference/msbuild-targets).

`<TargetFramework>`Ustawienie musi być ustawione tak, aby program MSBuild działał prawidłowo po uruchomieniu polecenia Pack w celu skompilowania i spakowania projektu.

Trzy następne ustawienia należy wykonać w celu poprawnego skonfigurowania projektu w celu uwzględnienia szablonów w odpowiednim folderze w pakiecie NuGet, gdy zostanie on utworzony.

Ostatnie ustawienie pomija komunikat ostrzegawczy, który nie ma zastosowania do projektów pakietu szablonów.

`<ItemGroup>`Zawiera dwa ustawienia. Pierwsze `<Content>` ustawienie uwzględnia wszystkie elementy w folderze _templates_ jako zawartość. Jest również ustawiony na wykluczenie dowolnego folderu _bin_ lub _obj_ , aby zapobiec dołączeniu kodu skompilowanego (w przypadku przetestowania i skompilowania szablonów). Po drugie, `<Compile>` ustawienie wyklucza wszystkie pliki kodu z kompilacji niezależnie od tego, gdzie się znajdują. To ustawienie uniemożliwia projekt używany do tworzenia pakietu szablonów na podstawie próby skompilowania kodu w hierarchii folderów _szablonów_ .

## <a name="build-and-install"></a>Kompiluj i zainstaluj

Zapisz ten plik, a następnie uruchom polecenie Pack

```dotnetcli
dotnet pack
```

To polecenie spowoduje skompilowanie projektu i utworzenie pakietu NuGet w tym folderze _working\bin\Debug_ .

```dotnetcli
dotnet pack
```

```console
Microsoft (R) Build Engine version 16.8.0+126527ff1 for .NET
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 123.86 ms for C:\working\templatepack.csproj.

  templatepack -> C:\working\bin\Debug\netstandard2.0\templatepack.dll
  Successfully created package 'C:\working\bin\Debug\AdatumCorporation.Utility.Templates.1.0.0.nupkg'.
```

Następnie Zainstaluj plik pakietu szablonów przy użyciu `dotnet new -i PATH_TO_NUPKG_FILE` polecenia.

```console
C:\working> dotnet new -i C:\working\bin\Debug\AdatumCorporation.Utility.Templates.1.0.0.nupkg
Usage: new [options]

Options:
  -h, --help          Displays help for this command.
  -l, --list          Lists templates containing the specified name. If no name is specified, lists all templates.

... cut to save space ...

Templates                                         Short Name               Language          Tags
--------------------------------------------      -------------------      ------------      ----------------------
Example templates: string extensions              stringext                [C#]              Common/Code
Console Application                               console                  [C#], F#, VB      Common/Console
Example templates: async project                  consoleasync             [C#]              Common/Console/C#9
Class library                                     classlib                 [C#], F#, VB      Common/Library
```

Jeśli pakiet NuGet został przekazany do źródła danych NuGet, można użyć `dotnet new -i PACKAGEID` polecenia, gdzie jest taka `PACKAGEID` sama jak `<PackageId>` ustawienie z pliku _. csproj_ . Ten identyfikator pakietu jest taki sam jak identyfikator pakietu NuGet.

## <a name="uninstall-the-template-pack"></a>Odinstalowywanie pakietu szablonów

Niezależnie od tego, jak został zainstalowany pakiet szablonów, z plikiem _. nupkg_ bezpośrednio lub przez źródło danych NuGet, usunięcie pakietu szablonu jest takie samo. Użyj `<PackageId>` szablonu, który chcesz odinstalować. Listę zainstalowanych szablonów można uzyskać, uruchamiając `dotnet new -u` polecenie.

```dotnetcli
dotnet new -u
```

```console
Template Instantiation Commands for .NET Core CLI

Currently installed items:
  Microsoft.DotNet.Common.ProjectTemplates.2.2
    Details:
      NuGetPackageId: Microsoft.DotNet.Common.ProjectTemplates.2.2
      Version: 1.0.2-beta4
      Author: Microsoft
    Templates:
      Class library (classlib) C#
      Class library (classlib) F#
      Class library (classlib) VB
      Console Application (console) C#
      Console Application (console) F#
      Console Application (console) VB
    Uninstall Command:
      dotnet new -u Microsoft.DotNet.Common.ProjectTemplates.2.2

... cut to save space ...

  AdatumCorporation.Utility.Templates
    Details:
      NuGetPackageId: AdatumCorporation.Utility.Templates
      Version: 1.0.0
      Author: Me
    Templates:
      Example templates: async project (consoleasync) C#
      Example templates: string extensions (stringext) C#
    Uninstall Command:
      dotnet new -u AdatumCorporation.Utility.Templates
```

Uruchom, `dotnet new -u AdatumCorporation.Utility.Templates` Aby odinstalować szablon. `dotnet new`Polecenie będzie wyprowadzać informacje pomocy, które powinny pominąć wcześniej zainstalowane szablony.

Gratulacje! Pakiet szablonów został zainstalowany i odinstalowany.

## <a name="next-steps"></a>Następne kroki

Aby dowiedzieć się więcej o szablonach, z których większość już wiesz, zobacz [Szablony niestandardowe dla nowego](../tools/custom-templates.md) artykułu usługi dotnet.

* [Witryna typu wiki repozytorium usługi GitHub/tworzenia szablonów](https://github.com/dotnet/templating/wiki)
* [dotnet/dotnet-Template-przykłady repozytorium GitHub](https://github.com/dotnet/dotnet-template-samples)
* [*template.jsw* schemacie w magazynie schematów JSON](http://json.schemastore.org/template)
