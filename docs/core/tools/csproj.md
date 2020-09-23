---
title: Dodatki do formatu csproj dla platformy .NET Core
description: Dowiedz się więcej o różnicach między istniejącymi a plikami csproj programu .NET Core
ms.topic: reference
ms.date: 04/08/2019
ms.openlocfilehash: 3ef6a89a8cd4f811bcdd41b9c9bedbc45da78098
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/23/2020
ms.locfileid: "91078219"
---
# <a name="additions-to-the-csproj-format-for-net-core"></a>Dodatki do formatu csproj dla platformy .NET Core

Ten dokument zawiera opis zmian, które zostały dodane do plików projektu w ramach przenoszenia z *project.js* do *csproj* i [MSBuild](https://github.com/Microsoft/MSBuild). Aby uzyskać więcej informacji na temat ogólnej składni pliku projektu i odwołania, zobacz dokumentację [pliku projektu programu MSBuild](/visualstudio/msbuild/msbuild-project-file-schema-reference) .

## <a name="implicit-package-references"></a>Odwołania do pakietów niejawnych

Elementy pakietu są niejawnie przywoływane na podstawie platform docelowych określonych we `<TargetFramework>` `<TargetFrameworks>` właściwości lub pliku projektu. `<TargetFrameworks>` jest ignorowany `<TargetFramework>` , jeśli jest określony, niezależnie od kolejności.

```xml
 <PropertyGroup>
   <TargetFramework>netcoreapp3.1</TargetFramework>
 </PropertyGroup>
 ```

 ```xml
 <PropertyGroup>
   <TargetFrameworks>netcoreapp3.1;net462</TargetFrameworks>
 </PropertyGroup>
 ```

### <a name="recommendations"></a>Zalecenia

Ponieważ `Microsoft.NETCore.App` lub `NETStandard.Library` pakiety są niejawnie przywoływane, zalecane są następujące najlepsze rozwiązania:

- W przypadku określania wartości docelowej .NET Core lub .NET Standard nigdy nie ma jawnego odwołania do `Microsoft.NETCore.App` `NETStandard.Library` elementów i pakietów `<PackageReference>` w pliku projektu.
- Jeśli potrzebna jest określona wersja środowiska uruchomieniowego w przypadku określania wartości docelowej .NET Core, należy użyć `<RuntimeFrameworkVersion>` właściwości w projekcie (na przykład `1.0.4` ) zamiast odwoływać się do pakietu.
  - Taka sytuacja może wystąpić, jeśli używasz [własnych wdrożeń](../deploying/index.md#publish-self-contained) i potrzebujesz określonej wersji poprawki środowiska uruchomieniowego 1.0.0 LTS, na przykład.
- Jeśli potrzebujesz konkretnej wersji `NETStandard.Library` pakietu w przypadku określania wartości docelowej .NET Standard, możesz użyć `<NetStandardImplicitPackageVersion>` właściwości i ustawić potrzebną wersję.
- Nie należy jawnie dodawać ani aktualizować odwołań do `Microsoft.NETCore.App` lub do `NETStandard.Library` pakietu w projektach .NET Framework. Jeśli dowolna wersja programu `NETStandard.Library` jest wymagana w przypadku korzystania z pakietu NuGet opartego na .NET Standard, pakiet NuGet automatycznie zainstaluje tę wersję.

## <a name="implicit-version-for-some-package-references"></a>Niejawna wersja dla niektórych odwołań do pakietów

Większość zastosowań [`<PackageReference>`](#packagereference) wymaga ustawienia `Version` atrybutu w celu określenia wersji pakietu NuGet do użycia. W przypadku korzystania z platformy .NET Core 2,1 lub 2,2 i odwoływania się do [Microsoft. AspNetCore. app](/aspnet/core/fundamentals/metapackage-app) lub [Microsoft. AspNetCore. All](/aspnet/core/fundamentals/metapackage), jednak atrybut jest zbędny. Zestaw .NET Core SDK może automatycznie wybrać wersję tych pakietów, które mają być używane.

### <a name="recommendation"></a>Zalecenie

W przypadku odwoływania się do `Microsoft.AspNetCore.App` `Microsoft.AspNetCore.All` pakietów lub nie należy określać ich wersji. Jeśli określona jest wersja, zestaw SDK może generować ostrzeżenie NETSDK1071. Aby usunąć to ostrzeżenie, Usuń wersję pakietu, taką jak w poniższym przykładzie:

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.AspNetCore.App" />
</ItemGroup>
```

> Znany problem: zestaw SDK platformy .NET Core 2,1 obsługuje tę składnię tylko wtedy, gdy projekt używa także Microsoft. NET. Sdk. Web. Ten problem został rozwiązany w zestawie SDK platformy .NET Core 2,2.

Te odwołania do ASP.NET Core pakietu są nieco inne niż w przypadku większości normalnych pakietów NuGet. Wdrożenia aplikacji korzystających z tych pakietów w [ramach platformy](../deploying/index.md#publish-framework-dependent) są automatycznie wykorzystywane w ramach platformy udostępnionej ASP.NET Core. W przypadku korzystania z pakietów trwałych nie są wdrażane **żadne** zasoby z przywoływanych ASP.NET Core pakietów NuGet w aplikacji — ASP.NET Core współdzielona architektura zawiera te zasoby. Zasoby w strukturze udostępnionej są zoptymalizowane pod kątem platformy docelowej w celu poprawienia czasu uruchamiania aplikacji. Aby uzyskać więcej informacji na temat platformy udostępnionej, zobacz [pakiet dystrybucji .NET Core](../distribution-packaging.md).

Jeśli określona *jest* wersja, jest ona traktowana jako *minimalna* wersja ASP.NET Core udostępnionej platformy dla wdrożeń zależnych od platformy i jako *dokładna* wersja wdrożeń samodzielnych. Może to mieć następujące konsekwencje:

- Jeśli wersja ASP.NET Core zainstalowana na serwerze jest mniejsza niż wersja określona w PackageReference, uruchomienie procesu platformy .NET Core kończy się niepowodzeniem. Aktualizacje pakietu NuGet.org są często dostępne na platformie Microsoft, zanim zostaną udostępnione aktualizacje w środowiskach hostingu, takich jak Azure. Zaktualizowanie wersji na PackageReference w celu ASP.NET Core może spowodować niepowodzenie wdrożonej aplikacji.
- Jeśli aplikacja jest wdrażana jako [wdrożenie samodzielne](../deploying/index.md#publish-self-contained), aplikacja może nie zawierać najnowszych aktualizacji zabezpieczeń do programu .NET Core. Jeśli wersja nie jest określona, zestaw SDK może automatycznie dołączać najnowszą wersję ASP.NET Core w samodzielnym wdrożeniu.

## <a name="default-compilation-includes-in-net-core-projects"></a>Domyślna kompilacja obejmuje projekty .NET Core

Po przeniesieniu do formatu *csproj* w najnowszej wersji zestawu SDK przeniesiono domyślną wartość dołączania i wykluczania dla elementów kompilowania i zasobów osadzonych do plików właściwości zestawu SDK. Oznacza to, że nie trzeba już określać tych elementów w pliku projektu.

Głównym powodem tego jest zmniejszenie bałaganu w pliku projektu. Wartości domyślne, które są obecne w zestawie SDK, powinny obejmować najbardziej typowe przypadki użycia, więc nie trzeba powtarzać ich w każdym tworzonym projekcie. Prowadzi to do mniejszych plików projektu, które są znacznie łatwiejsze do zrozumienia, a także do edycji, w razie potrzeby.

W poniższej tabeli przedstawiono, który element i które [elementy globalne](https://en.wikipedia.org/wiki/Glob_(programming)) są uwzględnione i wykluczone w zestawie SDK:

| Element           | Uwzględnij globalizowania                              | Wyklucz globalizowania                                                  | Usuń globalizowania              |
|-------------------|-------------------------------------------|---------------------------------------------------------------|----------------------------|
| Opracowania           | \*\*/\*. cs (lub inne rozszerzenia językowe) | \*\*/\*Użytkownicy  \*\*/\*.\* proj  \*\*/\*. sln  \*\*/\*. vssscc  | Brak                      |
| EmbeddedResource  | \*\*/\*. resx                              | \*\*/\*Użytkownicy \*\*/\*.\* proj \*\*/\*. sln \*\*/\*. vssscc     | Brak                      |
| Brak              | \*\*/\*                                   | \*\*/\*Użytkownicy \*\*/\*.\* proj \*\*/\*. sln \*\*/\*. vssscc     | \*\*/\*Rejestr \*\*/\*. resx   |

> [!NOTE]
> Polecenie **exclude globalizowania** zawsze wyklucza `./bin` foldery i `./obj` , które są reprezentowane odpowiednio przez `$(BaseOutputPath)` właściwości i programu `$(BaseIntermediateOutputPath)` MSBuild. Jako całość wszystkie wykluczenia są reprezentowane przez `$(DefaultItemExcludes)` .

Jeśli masz elementy globalne w projekcie i spróbujesz skompilować go przy użyciu najnowszego zestawu SDK, zostanie wyświetlony następujący błąd:

> Uwzględniono zduplikowane elementy kompilacji. Zestaw SDK platformy .NET domyślnie zawiera elementy kompilacji z katalogu projektu. Możesz usunąć te elementy z pliku projektu lub ustawić właściwość "EnableDefaultCompileItems" na wartość "false", jeśli chcesz jawnie uwzględnić je w pliku projektu.

Aby obejść ten błąd, można usunąć jawne `Compile` elementy, które pasują do tych wymienionych w poprzedniej tabeli, lub ustawić `<EnableDefaultCompileItems>` Właściwość na `false` , tak jak to:

```xml
<PropertyGroup>
    <EnableDefaultCompileItems>false</EnableDefaultCompileItems>
</PropertyGroup>
```

Ustawienie tej właściwości na wartość `false` spowoduje wyłączenie niejawnego dołączania, przywrócenie do zachowania poprzednich zestawów SDK, gdzie należy określić domyślny elementy globalne w projekcie.

Ta zmiana nie modyfikuje głównej Mechanics innych dołączeń. Jeśli jednak chcesz określić, na przykład niektóre pliki do opublikowania w aplikacji, możesz nadal używać znanych mechanizmów w *csproj* dla tego (na przykład `<Content>` elementu).

`<EnableDefaultCompileItems>` wyłącza tylko `Compile` elementy globalne, ale nie wpływa na inne elementy globalne, takie jak niejawne `None` globalizowania, które również dotyczą \* elementów cs. Z tego powodu, **Eksplorator rozwiązań** będzie kontynuować wyświetlanie \* elementów CS jako części projektu, zawartych jako `None` elementy. W podobny sposób można ustawić `<EnableDefaultNoneItems>` wartość false, aby wyłączyć niejawną `None` globalizowania w następujący sposób:

```xml
<PropertyGroup>
    <EnableDefaultNoneItems>false</EnableDefaultNoneItems>
</PropertyGroup>
```

Aby wyłączyć **wszystkie niejawne elementy globalne**, można ustawić `<EnableDefaultItems>` Właściwość na `false` tak jak w poniższym przykładzie:

```xml
<PropertyGroup>
    <EnableDefaultItems>false</EnableDefaultItems>
</PropertyGroup>
```

## <a name="how-to-see-the-whole-project-as-msbuild-sees-it"></a>Jak wyświetlić cały projekt, gdy jest on widoczny dla MSBuild

Chociaż te csproj zmieniają znacznie uproszczenie plików projektu, warto zobaczyć w pełni rozwinięty projekt, ponieważ program MSBuild zobaczy go po dołączeniu zestawu SDK i jego obiektów docelowych. Przetwórz wstępnie projekt przy [użyciu `/pp` przełącznika](/visualstudio/msbuild/msbuild-command-line-reference#preprocess) [`dotnet msbuild`](dotnet-msbuild.md) polecenia, który pokazuje, które pliki są importowane, ich źródła i ich wkład do kompilacji bez rzeczywistego tworzenia projektu:

```dotnetcli
dotnet msbuild -pp:fullproject.xml
```

Jeśli projekt ma wiele platform docelowych, wyniki polecenia powinny być skoncentrowane tylko na jednym z nich, określając go jako właściwość programu MSBuild:

```dotnetcli
dotnet msbuild -p:TargetFramework=netcoreapp3.1 -pp:fullproject.xml
```

## <a name="additions"></a>Zwiększenia

### <a name="sdk-attribute"></a>Atrybut zestawu SDK

Element główny `<Project>` pliku *. csproj* ma nowy atrybut o nazwie `Sdk` . `Sdk` Określa, który zestaw SDK będzie używany przez ten projekt. Zestaw SDK, zgodnie z opisem w dokumencie zawierającym [warstwy](cli-msbuild-architecture.md) , to zestaw [zadań](/visualstudio/msbuild/msbuild-tasks) i [elementów docelowych](/visualstudio/msbuild/msbuild-targets) programu MSBuild, które mogą kompilować kod platformy .NET Core. Dostępne są następujące zestawy SDK dla platformy .NET Core:

1. Zestaw .NET Core SDK o IDENTYFIKATORze `Microsoft.NET.Sdk`
2. Zestaw SDK sieci Web platformy .NET Core o IDENTYFIKATORze `Microsoft.NET.Sdk.Web`
3. Zestaw SDK biblioteki klas programu .NET Core z IDENTYFIKATORem `Microsoft.NET.Sdk.Razor`
4. Usługa programu .NET Core Worker o IDENTYFIKATORze `Microsoft.NET.Sdk.Worker` (od programu .net core 3,0)
5. Podstawowe WinForms i WPF platformy .NET z IDENTYFIKATORem `Microsoft.NET.Sdk.WindowsDesktop` (ponieważ .NET Core 3,0)

Musisz mieć `Sdk` atrybut ustawiony na jeden z tych identyfikatorów w `<Project>` elemencie, aby można było użyć narzędzi .NET Core i skompilować swój kod.

### <a name="packagereference"></a>PackageReference

Element `<PackageReference>` Item określa [zależność NuGet w projekcie](/nuget/consume-packages/package-references-in-project-files). Ten `Include` atrybut określa identyfikator pakietu.

```xml
<PackageReference Include="package-id" Version="" PrivateAssets="" IncludeAssets="" ExcludeAssets="" />
```

#### <a name="version"></a>Wersja

Wymagany `Version` atrybut określa wersję pakietu do przywrócenia. Ten atrybut uwzględnia reguły schematu [zakresu wersji NuGet](/nuget/concepts/package-versioning#version-ranges) . Domyślnym zachowaniem jest wersja minimalna, włącznie. Na przykład określenie `Version="1.2.3"` jest równoznaczne z notacją NuGet `[1.2.3, )` i oznacza, że rozpoznany pakiet będzie miał wersję 1.2.3, jeśli jest dostępny lub większy w inny sposób.

#### <a name="includeassets-excludeassets-and-privateassets"></a>IncludeAssets, ExcludeAssets i PrivateAssets

`IncludeAssets` atrybut określa, które zasoby należące do pakietu określonego przez `<PackageReference>` powinny być używane. Domyślnie są uwzględniane wszystkie zasoby pakietu.

`ExcludeAssets` atrybut określa, które zasoby należące do pakietu określonego przez `<PackageReference>` nie powinny być używane.

`PrivateAssets` atrybut określa, które zasoby należące do pakietu określonego przez `<PackageReference>` powinny być zużywane, ale nie można ich przepływać do następnego projektu. `Analyzers` `Build` `ContentFiles` Elementy i są domyślnie prywatne, gdy ten atrybut nie jest obecny.

> [!NOTE]
> `PrivateAssets`jest odpowiednikiem *project.jsw* / elemencie*xproj* `SuppressParent` .

Te atrybuty mogą zawierać co najmniej jeden z następujących elementów, oddzielonych znakiem średniego, `;` Jeśli jest wyświetlany więcej niż jeden:

- `Compile` — zawartość folderu *lib* jest dostępna do skompilowania.
- `Runtime` — zawartość folderu *środowiska uruchomieniowego* jest dystrybuowana.
- `ContentFiles` — zawartość folderu *contentfiles* jest używana.
- `Build` — są używane elementy props/targets w folderze *Build* .
- `Native` — zawartość zasobów natywnych jest kopiowana do folderu *wyjściowego* dla środowiska uruchomieniowego.
- `Analyzers` – Analizatory są używane.

Alternatywnie, atrybut może zawierać:

- `None` — żaden z elementów zawartości nie jest używany.
- `All` — wszystkie zasoby są używane.

### <a name="dotnetclitoolreference"></a>DotNetCliToolReference

Element `<DotNetCliToolReference>` Item określa narzędzie interfejsu wiersza polecenia, które użytkownik chce przywrócić w kontekście projektu. Jest to zamiennik dla `tools` węzła w *project.js*.

```xml
<DotNetCliToolReference Include="<package-id>" Version="" />
```

Należy pamiętać, że `DotNetCliToolReference` obecnie jest ona [przestarzała](https://github.com/dotnet/announcements/issues/107) na rzecz [lokalnych narzędzi .NET Core](./global-tools.md#install-a-local-tool).

#### <a name="version"></a>Wersja

`Version` Określa wersję pakietu do przywrócenia. Ten atrybut przestrzega reguł schematu obsługi wersji programu [NuGet](/nuget/create-packages/dependency-versions#version-ranges) . Domyślnym zachowaniem jest wersja minimalna, włącznie. Na przykład określenie `Version="1.2.3"` jest równoznaczne z notacją NuGet `[1.2.3, )` i oznacza, że rozpoznany pakiet będzie miał wersję 1.2.3, jeśli jest dostępny lub większy w inny sposób.

### <a name="runtimeidentifiers"></a>RuntimeIdentifiers

`<RuntimeIdentifiers>`Element Property pozwala określić rozdzielaną średnikami listę [identyfikatorów środowiska uruchomieniowego (RID)](../rid-catalog.md) dla projektu.
RID — umożliwia publikowanie wdrożeń samodzielnych.

```xml
<RuntimeIdentifiers>win10-x64;osx.10.11-x64;ubuntu.16.04-x64</RuntimeIdentifiers>
```

### <a name="runtimeidentifier"></a>RuntimeIdentifier

`<RuntimeIdentifier>`Element Property umożliwia określenie tylko jednego [identyfikatora środowiska uruchomieniowego (RID)](../rid-catalog.md) dla projektu. Identyfikator RID umożliwia publikowanie samodzielnego wdrożenia.

```xml
<RuntimeIdentifier>ubuntu.16.04-x64</RuntimeIdentifier>
```

`<RuntimeIdentifiers>`Zamiast tego użyj (plural), jeśli chcesz opublikować dla wielu środowisk uruchomieniowych. `<RuntimeIdentifier>` może zapewnić szybsze kompilacje, gdy wymagane jest tylko jedno środowisko uruchomieniowe.

### <a name="packagetargetfallback"></a>PackageTargetFallback

`<PackageTargetFallback>`Element Property umożliwia określenie zestawu zgodnych elementów docelowych, które mają być używane podczas przywracania pakietów. Została zaprojektowana tak, aby zezwalać na pakiety, które używają [TxM dotnet (target x moniker)](/nuget/schema/target-frameworks) do działania z pakietami, które nie deklarują TxM dotnet. Jeśli w projekcie jest używany TxM dotnet, wszystkie pakiety, od których zależy, muszą także mieć TxM dotnet, chyba że dodasz `<PackageTargetFallback>` do projektu w celu umożliwienia zgodności z platformą dotnet.

W poniższym przykładzie przedstawiono rezerwy dla wszystkich obiektów docelowych w projekcie:

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win8+wpa81+wp8
</PackageTargetFallback >
```

W poniższym przykładzie określono rezerwy tylko dla `netcoreapp3.1` elementu docelowego:

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netcoreapp3.1'">
    $(PackageTargetFallback);portable-net45+win8+wpa81+wp8
</PackageTargetFallback >
```

## <a name="build-events"></a>Zdarzenia kompilacji

Sposób, w jaki zdarzenia przed kompilacją i po kompilacji są określone w pliku projektu, zostały zmienione. Właściwości PreBuildEvent i PostBuildEvent nie są zalecane w formacie projektu w stylu zestawu SDK, ponieważ makra takie jak $ (ProjectDir) nie są rozpoznawane. Na przykład następujący kod nie jest już obsługiwany:

```xml
<PropertyGroup>
    <PreBuildEvent>"$(ProjectDir)PreBuildEvent.bat" "$(ProjectDir)..\" "$(ProjectDir)" "$(TargetDir)"</PreBuildEvent>
</PropertyGroup>
```

W projektach w stylu zestawu SDK Użyj elementu docelowego programu MSBuild o nazwie `PreBuild` lub `PostBuild` i ustaw dla właściwości `BeforeTargets` Właściwość `PreBuild` lub `AfterTargets` Właściwość `PostBuild` . W poprzednim przykładzie Użyj następującego kodu:

```xml
<Target Name="PreBuild" BeforeTargets="PreBuildEvent">
    <Exec Command="&quot;$(ProjectDir)PreBuildEvent.bat&quot; &quot;$(ProjectDir)..\&quot; &quot;$(ProjectDir)&quot; &quot;$(TargetDir)&quot;" />
</Target>

<Target Name="PostBuild" AfterTargets="PostBuildEvent">
   <Exec Command="echo Output written to $(TargetDir)" />
</Target>
```

> [!NOTE]
>Możesz użyć dowolnej nazwy dla obiektów docelowych programu MSBuild, ale środowisko IDE programu Visual Studio rozpoznaje `PreBuild` i ma `PostBuild` elementy docelowe, dlatego zalecamy używanie tych nazw, aby można było edytować polecenia w środowisku IDE programu Visual Studio.

## <a name="nuget-metadata-properties"></a>Właściwości metadanych NuGet

Po przeniesieniu do programu MSBuild przeniesiono metadane wejściowe, które są używane podczas pakowania pakietu NuGet z *project.jsna* pliki *. csproj* . Dane wejściowe są właściwościami programu MSBuild, dzięki czemu muszą one znajdować się w `<PropertyGroup>` grupie. Poniżej znajduje się lista właściwości, które są używane jako dane wejściowe procesu pakowania przy użyciu `dotnet pack` polecenia lub `Pack` elementu docelowego programu MSBuild, który jest częścią zestawu SDK:

### <a name="ispackable"></a>Ispacking

Wartość logiczna określająca, czy projekt może być spakowany. Wartość domyślna to `true`.

### <a name="packageversion"></a>PackageVersion

Określa wersję, która będzie miała pakiet otrzymany. Akceptuje wszystkie formy ciągu wersji NuGet. Wartość domyślna to `$(Version)` , czyli Właściwość `Version` w projekcie.

### <a name="packageid"></a>PackageId

Określa nazwę pakietu, który ma zostać utworzony. Jeśli nie zostanie określony, `pack` operacja będzie domyślnie używać `AssemblyName` nazwy katalogu jako nazwy pakietu.

### <a name="title"></a>Tytuł

Przyjazny dla człowieka tytuł pakietu, zazwyczaj używany w interfejsie użytkownika jako nuget.org i Menedżer pakietów w programie Visual Studio. Jeśli nie zostanie określony, zamiast niego zostanie użyty identyfikator pakietu.

### <a name="authors"></a>Autorzy

Rozdzielana średnikami lista autorów pakietów pasujących do nazw profilów w nuget.org. Są one wyświetlane w galerii NuGet w witrynie nuget.org i służą do krzyżowego odwoływania się do pakietów przez tych samych autorów.

### <a name="packagedescription"></a>PackageDescription

Długi opis pakietu do wyświetlania interfejsu użytkownika.

### <a name="description"></a>Opis

Długi opis zestawu. Jeśli `PackageDescription` nie jest określony, ta właściwość jest również używana jako Opis pakietu.

### <a name="copyright"></a>Prawa autorskie

Szczegóły dotyczące praw autorskich pakietu.

### <a name="packagerequirelicenseacceptance"></a>PackageRequireLicenseAcceptance

Wartość logiczna określająca, czy klient musi monitować konsumenta o zaakceptowanie licencji pakietu przed zainstalowaniem pakietu. Wartość domyślna to `false`.

### <a name="developmentdependency"></a>DevelopmentDependency

Wartość logiczna określająca, czy pakiet jest oznaczony jako zależność tylko do programowania, który uniemożliwia dołączenie pakietu jako zależności w innych pakietach. W przypadku PackageReference (NuGet 4.8 +) Flaga ta oznacza również, że zasoby czasu kompilacji są wykluczone z kompilacji. Aby uzyskać więcej informacji, zobacz [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).

### <a name="packagelicenseexpression"></a>PackageLicenseExpression

Identyfikator lub wyrażenie [licencji SPDX](https://spdx.org/licenses/) . Na przykład `Apache-2.0`.

Oto pełna lista [identyfikatorów licencji SPDX](https://spdx.org/licenses/). NuGet.org akceptuje tylko zatwierdzone licencje OSI lub FSF przy użyciu wyrażenia typu licencji.

Dokładna składnia wyrażeń licencji została opisana poniżej w [ABNF](https://tools.ietf.org/html/rfc5234).

```abnf
license-id            = <short form license identifier from https://spdx.org/spdx-specification-21-web-version#h.luq9dgcle9mo>

license-exception-id  = <short form license exception identifier from https://spdx.org/spdx-specification-21-web-version#h.ruv3yl8g6czd>

simple-expression = license-id / license-id”+”

compound-expression =  1*1(simple-expression /
                simple-expression "WITH" license-exception-id /
                compound-expression "AND" compound-expression /
                compound-expression "OR" compound-expression ) /
                "(" compound-expression ")" )

license-expression =  1*1(simple-expression / compound-expression / UNLICENSED)
```

> [!NOTE]
> Tylko jeden z `PackageLicenseExpression` `PackageLicenseFile` i `PackageLicenseUrl` można określić w danym momencie.

### <a name="packagelicensefile"></a>PackageLicenseFile

Ścieżka do pliku licencji w pakiecie, jeśli używasz licencji, która nie ma przypisanego identyfikatora SPDX lub jest licencją niestandardową (w przeciwnym razie `PackageLicenseExpression` jest preferowana)

Zamienia `PackageLicenseUrl` , nie można łączyć z `PackageLicenseExpression` i wymaga programu Visual Studio w wersji 15.9.4 i .NET SDK 2.1.502 lub 2.2.101 lub nowszego.

Należy upewnić się, że plik licencji jest spakowany przez dodanie go jawnie do projektu, przykładowe użycie:

```xml
<PropertyGroup>
  <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>
<ItemGroup>
  <None Include="licenses\LICENSE.txt" Pack="true" PackagePath="$(PackageLicenseFile)"/>
</ItemGroup>
```

### <a name="packagelicenseurl"></a>PackageLicenseUrl

Adres URL do licencji, która ma zastosowanie do pakietu. (_przestarzałe, ponieważ Visual Studio 15.9.4, .NET SDK 2.1.502 i 2.2.101_)

### <a name="packageicon"></a>PackageIcon

Ścieżka do obrazu w pakiecie do użycia jako ikona pakietu. Przeczytaj więcej na temat [ `icon` metadanych](/nuget/reference/nuspec#icon). [PackageIconUrl jest przestarzała](/nuget/reference/msbuild-targets#packageiconurl) na rzecz PackageIcon.

### <a name="packagereleasenotes"></a>PackageReleaseNotes

Informacje o wersji pakietu.

### <a name="packagetags"></a>PackageTags

Rozdzielana średnikami lista znaczników, które wyznaczają pakiet.

### <a name="packageoutputpath"></a>PackageOutputPath

Określa ścieżkę wyjściową, w której zostanie usunięty spakowany pakiet. Wartość domyślna to `$(OutputPath)`.

### <a name="includesymbols"></a>IncludeSymbols

Ta wartość logiczna wskazuje, czy pakiet powinien utworzyć dodatkowy pakiet symboli podczas pakowania projektu. Format pakietu symboli jest kontrolowany przez `SymbolPackageFormat` Właściwość.

### <a name="symbolpackageformat"></a>SymbolPackageFormat

Określa format pakietu symboli. W przypadku wystąpienia "Symbols. nupkg" zostanie utworzony pakiet ze starszymi symbolami z rozszerzeniem *. Symbols. nupkg* zawierającym plików PDB, DLL i inne pliki wyjściowe. W przypadku elementu "snupkg" zostanie utworzony pakiet symboli snupkg zawierający przenośne plików PDB. Wartość domyślna to "Symbols. nupkg".

### <a name="includesource"></a>IncludeSource

Ta wartość logiczna wskazuje, czy proces pakietu powinien utworzyć pakiet źródłowy. Pakiet źródłowy zawiera kod źródłowy biblioteki, a także pliki PDB. Pliki źródłowe są umieszczane w `src/ProjectName` katalogu w pliku pakietu, który został utworzony.

### <a name="istool"></a>Istool

Określa, czy wszystkie pliki wyjściowe są kopiowane do folderu *Tools* zamiast folderu *lib* . Różni się to od elementu `DotNetCliTool` , który jest określany przez ustawienie `PackageType` w pliku *. csproj* .

### <a name="repositoryurl"></a>RepositoryUrl

Określa adres URL repozytorium, w którym znajduje się kod źródłowy pakietu i/lub z którego jest tworzony.

### <a name="repositorytype"></a>Repozytorium

Określa typ repozytorium. Wartość domyślna to "Git".

### <a name="repositorybranch"></a>RepositoryBranch

Określa nazwę gałęzi źródłowej w repozytorium. Gdy projekt jest spakowany w pakiecie NuGet, jest dodawany do metadanych pakietu.

### <a name="repositorycommit"></a>RepositoryCommit

Opcjonalne zatwierdzenie lub zestaw zmian repozytorium, aby wskazać, z którym źródłem został skompilowany pakiet. `RepositoryUrl` należy również określić, aby ta właściwość została uwzględniona. Gdy projekt jest spakowany w pakiecie NuGet, to zatwierdzenie lub zestaw zmian zostanie dodany do metadanych pakietu.

### <a name="nopackageanalysis"></a>NoPackageAnalysis

Określa, że pakiet nie powinien uruchamiać analizy pakietu po skompilowaniu pakietu.

### <a name="minclientversion"></a>MinClientVersion

Określa minimalną wersję klienta NuGet, który może zainstalować ten pakiet, wymuszony przez nuget.exe i Menedżera pakietów programu Visual Studio.

### <a name="includebuildoutput"></a>IncludeBuildOutput

Ta wartość logiczna określa, czy zestawy danych wyjściowych kompilacji powinny być pakowane do pliku *. nupkg* , czy nie.

### <a name="includecontentinpack"></a>IncludeContentInPack

Ta wartość logiczna określa, czy wszystkie elementy, które mają typ, `Content` zostaną dołączone do pakietu w wyniku. Wartość domyślna to `true`.

### <a name="buildoutputtargetfolder"></a>BuildOutputTargetFolder

Określa folder, w którym mają zostać umieszczone zestawy wyjściowe. Zestawy wyjściowe (i inne pliki wyjściowe) są kopiowane do odpowiednich folderów struktury.

### <a name="contenttargetfolders"></a>ContentTargetFolders

Ta właściwość określa domyślną lokalizację, w której należy wykonać wszystkie pliki zawartości, jeśli `PackagePath` nie została określona dla nich. Wartość domyślna to "Content; contentFiles".

### <a name="nuspecfile"></a>NuspecFile

Ścieżka względna lub bezwzględna do pliku *. nuspec* używanego do pakowania.

> [!NOTE]
> Jeśli plik *. nuspec* jest określony, jest używany **wyłącznie** na potrzeby informacji o pakowaniu i nie są używane żadne informacje w projektach.

### <a name="nuspecbasepath"></a>NuspecBasePath

Ścieżka podstawowa pliku *. nuspec* .

### <a name="nuspecproperties"></a>NuspecProperties

Rozdzielana średnikami lista par klucz = wartość.

## <a name="assemblyinfo-properties"></a>Właściwości AssemblyInfo

[Atrybuty zestawu](../../standard/assembly/set-attributes.md) , które były zazwyczaj obecne w pliku *AssemblyInfo* , są teraz automatycznie generowane na podstawie właściwości.

### <a name="properties-per-attribute"></a>Właściwości na atrybut

Jak pokazano w poniższej tabeli, każdy atrybut ma właściwość, która kontroluje jej zawartość, a druga, która wyłącza jej generowanie:

| Atrybut                                                      | Właściwość               | Właściwość do wyłączenia                             |
|----------------------------------------------------------------|------------------------|-------------------------------------------------|
| <xref:System.Reflection.AssemblyCompanyAttribute>              | `Company`              | `GenerateAssemblyCompanyAttribute`              |
| <xref:System.Reflection.AssemblyConfigurationAttribute>        | `Configuration`        | `GenerateAssemblyConfigurationAttribute`        |
| <xref:System.Reflection.AssemblyCopyrightAttribute>            | `Copyright`            | `GenerateAssemblyCopyrightAttribute`            |
| <xref:System.Reflection.AssemblyDescriptionAttribute>          | `Description`          | `GenerateAssemblyDescriptionAttribute`          |
| <xref:System.Reflection.AssemblyFileVersionAttribute>          | `FileVersion`          | `GenerateAssemblyFileVersionAttribute`          |
| <xref:System.Reflection.AssemblyInformationalVersionAttribute> | `InformationalVersion` | `GenerateAssemblyInformationalVersionAttribute` |
| <xref:System.Reflection.AssemblyProductAttribute>              | `Product`              | `GenerateAssemblyProductAttribute`              |
| <xref:System.Reflection.AssemblyTitleAttribute>                | `AssemblyTitle`        | `GenerateAssemblyTitleAttribute`                |
| <xref:System.Reflection.AssemblyVersionAttribute>              | `AssemblyVersion`      | `GenerateAssemblyVersionAttribute`              |
| <xref:System.Resources.NeutralResourcesLanguageAttribute>      | `NeutralLanguage`      | `GenerateNeutralResourcesLanguageAttribute`     |

Uwagi:

- `AssemblyVersion` i `FileVersion` domyślnie przyjmuje wartość `$(Version)` bez sufiksu. Na przykład, jeśli `$(Version)` jest `1.2.3-beta.4` , wartość będzie równa `1.2.3` .
- `InformationalVersion` wartość domyślna to `$(Version)` .
- `InformationalVersion``$(SourceRevisionId)`dołącza, jeśli właściwość jest obecna. Można go wyłączyć przy użyciu `IncludeSourceRevisionInInformationalVersion` .
- `Copyright` i `Description` właściwości są również używane dla metadanych narzędzia NuGet.
- `Configuration` jest współużytkowany ze wszystkimi procesami kompilacji i ustawiany za pośrednictwem `--configuration` parametru `dotnet` poleceń.

### <a name="generateassemblyinfo"></a>GenerateAssemblyInfo

Wartość logiczna, która włącza lub wyłącza wszystkie generowanie AssemblyInfo. Wartość domyślna to `true`.

### <a name="generatedassemblyinfofile"></a>GeneratedAssemblyInfoFile

Ścieżka wygenerowanego pliku informacji o zestawie. Domyślnie do pliku w `$(IntermediateOutputPath)` katalogu (obj).
