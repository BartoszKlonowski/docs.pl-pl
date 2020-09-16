---
title: Szablony niestandardowe dla nowego dotnet
description: Dowiedz się więcej na temat szablonów niestandardowych dla dowolnego typu projektu lub plików platformy .NET.
author: adegeo
ms.date: 05/20/2020
ms.openlocfilehash: 1d2e5ffcb0b279f1686855834c2357827a4dc7d5
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90538098"
---
# <a name="custom-templates-for-dotnet-new"></a>Szablony niestandardowe dla nowego dotnet

[Zestaw .NET Core SDK](https://dotnet.microsoft.com/download) zawiera wiele szablonów, które są już zainstalowane i gotowe do użycia. [ `dotnet new` Polecenie](dotnet-new.md) nie jest tylko sposobem korzystania z szablonu, ale także instalowania i odinstalowywania szablonów. Począwszy od platformy .NET Core 2,0, można tworzyć własne szablony niestandardowe dla dowolnego typu projektu, takie jak aplikacja, usługa, narzędzie lub Biblioteka klas. Można nawet utworzyć szablon, który wyprowadza jeden lub więcej niezależnych plików, na przykład plik konfiguracji.

Szablony niestandardowe można instalować z pakietu NuGet na dowolnym kanale informacyjnym NuGet, odwołując się bezpośrednio do pliku NuGet *. nupkg* lub określając katalog systemu plików zawierający szablon. Aparat szablonów oferuje funkcje, które umożliwiają zamianę wartości, uwzględnianie i wykluczanie plików oraz wykonywanie niestandardowych operacji przetwarzania, gdy szablon jest używany.

Aparat szablonu jest otwartym źródłem, a repozytorium kodu online jest w witrynie GitHub [/tworzenia szablonów](https://github.com/dotnet/templating/) . Więcej szablonów, w tym szablonów ze stron trzecich, znajduje się w [dostępnych szablonach dla platformy dotnet Nowość](https://github.com/dotnet/templating/wiki/Available-templates-for-dotnet-new) w serwisie GitHub. Aby uzyskać więcej informacji na temat tworzenia i używania szablonów niestandardowych, zobacz [jak utworzyć własne szablony dla platformy dotnet New](https://devblogs.microsoft.com/dotnet/how-to-create-your-own-templates-for-dotnet-new/) i [typu wiki/tworzenia szablonów repozytorium GitHub](https://github.com/dotnet/templating/wiki).

> [!NOTE]
> Przykłady szablonów są dostępne w repozytorium usługi [dotnet/dotnet-Template-Samples](https://github.com/dotnet/dotnet-template-samples) w witrynie GitHub. Mimo że te przykłady są dobrym zasobem do uczenia się, jak działają szablony, repozytorium jest archiwizowane i nie jest już obsługiwane. Przykłady mogą być nieaktualne i nie będą już działać.

Aby postępować zgodnie z przewodnikiem i utworzyć szablon, zobacz temat [Tworzenie niestandardowego szablonu dla dotnet nowy](../tutorials/cli-templates-create-item-template.md) samouczek.

### <a name="net-default-templates"></a>Szablony domyślne .NET

Po zainstalowaniu [zestaw .NET Core SDK](https://dotnet.microsoft.com/download)otrzymujesz wiele wbudowanych szablonów służących do tworzenia projektów i plików, takich jak aplikacje konsolowe, biblioteki klas, projekty testów jednostkowych, aplikacje ASP.NET Core (w tym projekty [kątowe](https://angular.io/) i [reagowanie](https://facebook.github.io/react/) ) oraz pliki konfiguracyjne. Aby wyświetlić listę wbudowanych szablonów, uruchom `dotnet new` polecenie z `-l|--list` opcją:

```dotnetcli
dotnet new --list
```

## <a name="configuration"></a>Konfiguracja

Szablon składa się z następujących części:

- Pliki źródłowe i foldery.
- Plik konfiguracji (*template.json*).

### <a name="source-files-and-folders"></a>Pliki źródłowe i foldery

Pliki i foldery źródłowe zawierają wszelkie pliki i foldery, które mają być używane przez aparat szablonów po `dotnet new <TEMPLATE>` uruchomieniu polecenia. Aparat szablonów jest przeznaczony do używania *projektów możliwy do uruchomienia* jako kod źródłowy do tworzenia projektów. Ma to kilka korzyści:

- Aparat szablonów nie wymaga dodawania specjalnych tokenów do kodu źródłowego projektu.
- Pliki kodu nie są plikami specjalnymi ani modyfikowane w sposób umożliwiający współdziałanie z aparatem szablonu. Dlatego narzędzia zwykle używane podczas pracy z projektami również pracują z zawartością szablonu.
- Możesz tworzyć, uruchamiać i debugować projekty szablonów tak samo jak w przypadku innych projektów.
- Możesz szybko utworzyć szablon na podstawie istniejącego projektu, dodając plik *./.template.config/template.jsw* pliku konfiguracji do projektu.

Pliki i foldery przechowywane w szablonie nie są ograniczone do formalnych typów projektów .NET. Pliki źródłowe i foldery mogą zawierać dowolną zawartość, którą chcesz utworzyć, gdy szablon jest używany, nawet jeśli aparat szablonu tworzy tylko jeden plik jako dane wyjściowe.

Pliki generowane przez szablon można modyfikować na podstawie logiki i ustawień, które zostały podane w *template.jsw* pliku konfiguracyjnym. Użytkownik może przesłonić te ustawienia przez przekazanie opcji do `dotnet new <TEMPLATE>` polecenia. Typowym przykładem logiki niestandardowej jest podanie nazwy klasy lub zmiennej w pliku kodu, który jest wdrażany przez szablon.

### <a name="templatejson"></a>template.jsna

*template.jsw* pliku zostanie umieszczony w folderze *.template.config* w katalogu głównym szablonu. Plik zawiera informacje o konfiguracji do aparatu szablonu. Minimalna konfiguracja wymaga od członków pokazanych w poniższej tabeli, co jest wystarczające do utworzenia szablonu funkcjonalnego.

| Członek            | Typ          | Opis |
| ----------------- | ------------- | ----------- |
| `$schema`         | URI           | Schemat JSON dla *template.js* pliku. Edytory obsługujące schematy JSON umożliwiają korzystanie z funkcji edytowania JSON, gdy schemat jest określony. Na przykład [Visual Studio Code](https://code.visualstudio.com/) wymaga tego elementu członkowskiego, aby włączyć funkcję IntelliSense. Użyj wartości `http://json.schemastore.org/template` . |
| `author`          | ciąg        | Autor szablonu. |
| `classifications` | Array (ciąg) | Zero lub więcej charakterystyki szablonu, którego użytkownik może użyć, aby znaleźć szablon podczas jego wyszukania. Klasyfikacje są również wyświetlane w kolumnie *Tagi* , gdy pojawiają się na liście szablonów utworzonych przy użyciu `dotnet new -l|--list` polecenia. |
| `identity`        | ciąg        | Unikatowa nazwa tego szablonu. |
| `name`            | ciąg        | Nazwa szablonu, który użytkownicy powinni zobaczyć. |
| `shortName`       | ciąg        | Domyślna nazwa skrótu służąca do wybierania szablonu, który ma zastosowanie do środowisk, w których nazwa szablonu jest określona przez użytkownika, a nie wybierana za pośrednictwem graficznego interfejsu użytkownika. Na przykład krótka nazwa jest przydatna w przypadku korzystania z szablonów z wiersza polecenia z poleceniami CLI. |

Pełny schemat *template.jsw* pliku znajduje się w [magazynie schematów JSON](http://json.schemastore.org/template). Aby uzyskać więcej informacji na temat *template.jsw* pliku, zobacz stronę [typu "dotnet tworzenia szablonów wiki](https://github.com/dotnet/templating/wiki)".

#### <a name="example"></a>Przykład

Na przykład poniżej znajduje się folder Template zawierający dwa pliki zawartości: *Console.cs* i *readme.txt*. Zwróć uwagę, że istnieje wymagany folder o nazwie *.template.config* , który zawiera *template.jsna* pliku.

```text
└───mytemplate
    │   console.cs
    │   readme.txt
    │
    └───.template.config
            template.json
```

*template.jsw* pliku wygląda następująco:

```json
{
  "$schema": "http://json.schemastore.org/template",
  "author": "Travis Chau",
  "classifications": [ "Common", "Console" ],
  "identity": "AdatumCorporation.ConsoleTemplate.CSharp",
  "name": "Adatum Corporation Console Application",
  "shortName": "adatumconsole"
}
```

Folder Moje *Template* to instalowalny pakiet szablonów. Po zainstalowaniu pakietu `shortName` można go użyć z `dotnet new` poleceniem. Załóżmy na przykład, `dotnet new adatumconsole` że pliki są wyprowadzane `console.cs` `readme.txt` do bieżącego folderu.

## <a name="packing-a-template-into-a-nuget-package-nupkg-file"></a>Pakowanie szablonu do pakietu NuGet (plik NUPKG)

Szablon niestandardowy jest spakowany przy użyciu polecenia [pakietu dotnet](dotnet-pack.md) i pliku *. csproj* . Alternatywnie, można użyć polecenia [NuGet](/nuget/tools/nuget-exe-cli-reference) z [pakietem NuGet](/nuget/tools/cli-ref-pack) z plikiem *. nuspec* . Jednak program NuGet wymaga .NET Framework w systemie Windows i [mono](https://www.mono-project.com/) w systemie Linux i macOS.

Plik *. csproj* różni się nieco od tradycyjnego pliku Code-Project *. csproj* . Zwróć uwagę na następujące ustawienia:

01. `<PackageType>`Ustawienie jest dodawane i ustawiane na `Template` .
01. `<PackageVersion>`Ustawienie zostanie dodane i ustawiony prawidłowy [numer wersji programu NuGet](/nuget/reference/package-versioning).
01. To `<PackageId>` ustawienie jest dodawane i ustawiane jako unikatowy identyfikator. Ten identyfikator służy do odinstalowywania pakietu szablonów i jest używany przez źródła danych NuGet do rejestrowania pakietu szablonów.
01. Ogólne ustawienia metadanych powinny być ustawione: `<Title>` , `<Authors>` , `<Description>` , i `<PackageTags>` .
01. `<TargetFramework>`Ustawienie musi być ustawione, nawet jeśli plik binarny tworzony przez proces szablonu nie jest używany. W poniższym przykładzie jest ustawiony na `netstandard2.0` .

Pakiet szablonów w formie pakietu NuGet *. nupkg* wymaga, aby wszystkie szablony były przechowywane w folderze *zawartości* w pakiecie. Istnieje kilka dodatkowych ustawień do dodania do pliku *. csproj* , aby upewnić się, że wygenerowane *. nupkg* można zainstalować jako pakiet szablonów:

01. `<IncludeContentInPack>`Ustawienie jest ustawione na `true` w celu uwzględnienia dowolnego pliku, który jest ustawiany jako **zawartość** pakietu NuGet.
01. `<IncludeBuildOutput>`Ustawienie jest ustawione na `false` wykluczenie wszystkich plików binarnych generowanych przez kompilator z pakietu NuGet.
01. `<ContentTargetFolders>`Ustawienie jest ustawione na `content` . Daje to pewność, że pliki ustawione jako **zawartość** są przechowywane w folderze *zawartości* w pakiecie NuGet. Ten folder w pakiecie NuGet jest analizowany przez system szablonów dotnet.

Prostym sposobem wykluczenia wszystkich plików kodu z kompilowania przez projekt szablonu jest użycie `<Compile Remove="**\*" />` elementu w pliku projektu w obrębie `<ItemGroup>` elementu.

Łatwym sposobem struktury pakietu Template Pack jest umieszczenie wszystkich szablonów w poszczególnych folderach, a następnie każdy folder szablonu wewnątrz folderu *templates* znajdującego się w tym samym katalogu, w którym znajduje się plik *. csproj* . W ten sposób można użyć pojedynczego elementu projektu, aby uwzględnić wszystkie pliki i foldery w *szablonach* jako **zawartość**. Wewnątrz `<ItemGroup>` elementu, Utwórz `<Content Include="templates\**\*" Exclude="templates\**\bin\**;templates\**\obj\**" />` element.

Poniżej znajduje się przykładowy plik *csproj* , który jest zgodny ze wszystkimi powyższymi wskazówkami. Program IT pakuje folder podrzędny *szablonów* do folderu pakietu *zawartości* i wyklucza każdy plik kodu z kompilacji.

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
  </PropertyGroup>

  <ItemGroup>
    <Content Include="templates\**\*" Exclude="templates\**\bin\**;templates\**\obj\**" />
    <Compile Remove="**\*" />
  </ItemGroup>

</Project>
```

W poniższym przykładzie przedstawiono strukturę plików i folderów programu przy użyciu pliku *. csproj* , aby utworzyć pakiet szablonów. Folder plików i *szablonów* *MyDotnetTemplates. csproj* znajduje się w katalogu głównym katalogu o nazwie *project_folder*. Folder *szablonów* zawiera dwa szablony, *mytemplate1* i *mytemplate2*. Każdy szablon zawiera pliki zawartości i folder *.template.config* z *template.js* pliku konfiguracyjnego.

```text
project_folder
│   MyDotnetTemplates.csproj
│
└───templates
    ├───mytemplate1
    │   │   console.cs
    │   │   readme.txt
    │   │
    │   └───.template.config
    │           template.json
    │
    └───mytemplate2
        │   otherfile.cs
        │
        └───.template.config
                template.json
```

## <a name="installing-a-template"></a>Instalowanie szablonu

Użyj polecenia [dotnet New-i |--Install](dotnet-new.md) , aby zainstalować pakiet.

### <a name="to-install-a-template-from-a-nuget-package-stored-at-nugetorg"></a>Aby zainstalować szablon z pakietu NuGet przechowywanego w nuget.org

Użyj identyfikatora pakietu NuGet, aby zainstalować pakiet szablonu.

```dotnetcli
dotnet new -i <NUGET_PACKAGE_ID>
```

### <a name="to-install-a-template-from-a-local-nupkg-file"></a>Aby zainstalować szablon z lokalnego pliku NUPKG

Podaj ścieżkę do pliku pakietu NuGet *. nupkg* .

```dotnetcli
dotnet new -i <PATH_TO_NUPKG_FILE>
```

### <a name="to-install-a-template-from-a-file-system-directory"></a>Aby zainstalować szablon z katalogu systemu plików

Szablony można instalować z folderu szablonów, takiego jak folder *mytemplate1* , z powyższego przykładu. Określ ścieżkę folderu *.template.config* . Ścieżka do katalogu szablonów nie musi być bezwzględna. Jednak do odinstalowania szablonu, który jest instalowany z folderu, wymagana jest ścieżka bezwzględna.

```dotnetcli
dotnet new -i <FILE_SYSTEM_DIRECTORY>
```

## <a name="get-a-list-of-installed-templates"></a>Pobierz listę zainstalowanych szablonów

Polecenie odinstalowania bez żadnych innych parametrów spowoduje wyświetlenie listy wszystkich zainstalowanych szablonów.

```dotnetcli
dotnet new -u
```

To polecenie zwraca coś podobnego do następującego:

```console
Template Instantiation Commands for .NET Core CLI

Currently installed items:
  Microsoft.DotNet.Common.ItemTemplates
    Templates:
      global.json file (globaljson)
      NuGet Config (nugetconfig)
      Solution File (sln)
      Dotnet local tool manifest file (tool-manifest)
      Web Config (webconfig)
  Microsoft.DotNet.Common.ProjectTemplates.3.0
    Templates:
      Class library (classlib) C#
      Class library (classlib) F#
      Class library (classlib) VB
      Console Application (console) C#
      Console Application (console) F#
      Console Application (console) VB
...
```

Pierwszy poziom elementów po `Currently installed items:` są identyfikatorami używanymi podczas odinstalowywania szablonu. I w powyższym przykładzie `Microsoft.DotNet.Common.ItemTemplates` `Microsoft.DotNet.Common.ProjectTemplates.3.0` . Jeśli szablon został zainstalowany przy użyciu ścieżki systemu plików, ten identyfikator będzie ścieżką folderu *.template.config* .

## <a name="uninstalling-a-template"></a>Odinstalowywanie szablonu

Aby odinstalować pakiet, użyj polecenia " [New-u |--Uninstall" dotnet](dotnet-new.md) .

Jeśli pakiet został zainstalowany bezpośrednio przez źródło danych NuGet lub plik *. nupkg* , podaj identyfikator.

```dotnetcli
dotnet new -u <NUGET_PACKAGE_ID>
```

Jeśli pakiet został zainstalowany przez określenie ścieżki do folderu *.template.config* , Użyj tej ścieżki **bezwzględnej** , aby odinstalować pakiet. Ścieżkę bezwzględną szablonu można zobaczyć w danych wyjściowych dostarczonych przez `dotnet new -u` polecenie. Aby uzyskać więcej informacji, zobacz sekcję [Pobieranie listy zainstalowanych szablonów](#get-a-list-of-installed-templates) powyżej.

```dotnetcli
dotnet new -u <ABSOLUTE_FILE_SYSTEM_DIRECTORY>
```

## <a name="create-a-project-using-a-custom-template"></a>Tworzenie projektu przy użyciu szablonu niestandardowego

Po zainstalowaniu szablonu Użyj szablonu, wykonując `dotnet new <TEMPLATE>` polecenie tak jak w przypadku dowolnego innego wstępnie zainstalowanego szablonu. Możesz również określić [Opcje](dotnet-new.md#options) dla `dotnet new` polecenia, w tym opcje specyficzne dla szablonu, które zostały skonfigurowane w ustawieniach szablonu. Podaj krótką nazwę szablonu bezpośrednio do polecenia:

```dotnetcli
dotnet new <TEMPLATE>
```

## <a name="see-also"></a>Zobacz także

- [Tworzenie szablonu niestandardowego dla nowego dotnet (samouczek)](../tutorials/cli-templates-create-item-template.md)
- [Witryna typu wiki repozytorium usługi GitHub/tworzenia szablonów](https://github.com/dotnet/templating/wiki)
- [dotnet/dotnet-Template-przykłady repozytorium GitHub](https://github.com/dotnet/dotnet-template-samples)
- [Jak utworzyć własne szablony dla nowego dotnet](https://devblogs.microsoft.com/dotnet/how-to-create-your-own-templates-for-dotnet-new/)
- [*template.jsw* schemacie w magazynie schematów JSON](http://json.schemastore.org/template)
