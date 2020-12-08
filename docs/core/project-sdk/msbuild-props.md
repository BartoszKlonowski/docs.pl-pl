---
title: Właściwości programu MSBuild dla Microsoft. NET. Sdk
description: Odwołanie do właściwości i elementów programu MSBuild, które są zrozumiałe dla zestawu .NET SDK.
ms.date: 02/14/2020
ms.topic: reference
ms.custom: updateeachrelease
ms.openlocfilehash: 3b58fd080439c73ee30d5c8dc59c50c0410db164
ms.sourcegitcommit: 45c7148f2483db2501c1aa696ab6ed2ed8cb71b2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/08/2020
ms.locfileid: "96851578"
---
# <a name="msbuild-reference-for-net-sdk-projects"></a>Dokumentacja programu MSBuild dla projektów zestawu .NET SDK

Ta strona jest odwołaniem do właściwości i elementów programu MSBuild, których można użyć do konfigurowania projektów platformy .NET.

> [!NOTE]
> Ta strona jest w toku i nie zawiera wszystkich przydatnych właściwości programu MSBuild dla zestawu .NET SDK. Aby zapoznać się z listą typowych właściwości programu MSBuild, zobacz [typowe właściwości programu MSBuild](/visualstudio/msbuild/common-msbuild-project-properties).

## <a name="framework-properties"></a>Właściwości struktury

- [TargetFramework](#targetframework)
- [TargetFrameworks](#targetframeworks)
- [NetStandardImplicitPackageVersion](#netstandardimplicitpackageversion)

### <a name="targetframework"></a>TargetFramework

`TargetFramework`Właściwość określa wersję platformy docelowej dla aplikacji. Aby zapoznać się z listą prawidłowych monikerów platformy docelowej, zobacz [platformę docelową w projektach w stylu zestawu SDK](../../standard/frameworks.md#supported-target-frameworks).

```xml
<PropertyGroup>
  <TargetFramework>netcoreapp3.1</TargetFramework>
</PropertyGroup>
```

Aby uzyskać więcej informacji, zobacz [Platformy docelowe w projektach w stylu zestawu SDK](../../standard/frameworks.md).

### <a name="targetframeworks"></a>TargetFrameworks

Użyj `TargetFrameworks` właściwości, jeśli chcesz, aby aplikacja była przeznaczona dla wielu platform. Aby zapoznać się z listą prawidłowych monikerów platformy docelowej, zobacz [platformę docelową w projektach w stylu zestawu SDK](../../standard/frameworks.md#supported-target-frameworks).

> [!NOTE]
> Ta właściwość jest ignorowana, jeśli `TargetFramework` określono (pojedynczo).

```xml
<PropertyGroup>
  <TargetFrameworks>netcoreapp3.1;net462</TargetFrameworks>
</PropertyGroup>
```

Aby uzyskać więcej informacji, zobacz [Platformy docelowe w projektach w stylu zestawu SDK](../../standard/frameworks.md).

### <a name="netstandardimplicitpackageversion"></a>NetStandardImplicitPackageVersion

> [!NOTE]
> Ta właściwość ma zastosowanie tylko do projektów korzystających z programu `netstandard1.x` . Nie dotyczy to projektów, które używają `netstandard2.x` .

Użyj `NetStandardImplicitPackageVersion` właściwości, aby określić wersję platformy, która jest starsza niż wersja pakietu. Plik projektu w poniższym przykładzie docelowym `netstandard1.3` , ale używa wersji 1.6.0 `NETStandard.Library` .

```xml
<PropertyGroup>
  <TargetFramework>netstandard1.3</TargetFramework>
  <NetStandardImplicitPackageVersion>1.6.0</NetStandardImplicitPackageVersion>
</PropertyGroup>
```

## <a name="package-properties"></a>Właściwości pakietu

Można określić właściwości, takie jak `PackageId` ,,, `PackageVersion` `PackageIcon` `Title` i, `Description` aby opisać pakiet, który zostanie utworzony na podstawie projektu. Aby uzyskać informacje o tych i innych właściwościach, zobacz [pakiet Target](/nuget/reference/msbuild-targets#pack-target).

```xml
<PropertyGroup>
  ...
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>John Doe</Authors>
  <Company>Contoso</Company>
</PropertyGroup>
```

## <a name="publish-properties-and-items"></a>Publikowanie właściwości i elementów

- [CopyLocalLockFileAssemblies](#copylocallockfileassemblies)
- [RuntimeIdentifier](#runtimeidentifier)
- [RuntimeIdentifiers](#runtimeidentifiers)
- [TrimmerRootAssembly](#trimmerrootassembly)
- [UseAppHost](#useapphost)

### <a name="copylocallockfileassemblies"></a>CopyLocalLockFileAssemblies

`CopyLocalLockFileAssemblies`Właściwość jest przydatna w przypadku projektów wtyczek, które mają zależności od innych bibliotek. W przypadku ustawienia tej właściwości na wartość `true` wszystkie zależności pakietów NuGet są kopiowane do katalogu wyjściowego. Oznacza to, że możesz użyć danych wyjściowych programu, `dotnet build` Aby uruchomić wtyczkę na dowolnym komputerze.

```xml
<PropertyGroup>
  <CopyLocalLockFileAssemblies>true</CopyLocalLockFileAssemblies>
</PropertyGroup>
```

> [!TIP]
> Alternatywnie można użyć `dotnet publish` programu do opublikowania biblioteki klas. Aby uzyskać więcej informacji, zobacz [dotnet Publish](../tools/dotnet-publish.md).

### <a name="runtimeidentifier"></a>RuntimeIdentifier

`RuntimeIdentifier`Właściwość umożliwia określenie pojedynczego [identyfikatora środowiska uruchomieniowego (RID)](../rid-catalog.md) dla projektu. Identyfikator RID umożliwia publikowanie samodzielnego wdrożenia.

```xml
<PropertyGroup>
  <RuntimeIdentifier>ubuntu.16.04-x64</RuntimeIdentifier>
</PropertyGroup>
```

### <a name="runtimeidentifiers"></a>RuntimeIdentifiers

`RuntimeIdentifiers`Właściwość pozwala określić rozdzielaną średnikami listę [identyfikatorów środowiska uruchomieniowego (RID)](../rid-catalog.md) dla projektu. Użyj tej właściwości, jeśli chcesz opublikować dla wielu środowisk uruchomieniowych. `RuntimeIdentifiers` jest używany podczas przywracania, aby upewnić się, że odpowiednie zasoby znajdują się na wykresie.

> [!TIP]
> `RuntimeIdentifier` (pojedyncze) może zapewnić szybsze kompilacje, gdy wymagane jest tylko jedno środowisko uruchomieniowe.

```xml
<PropertyGroup>
  <RuntimeIdentifiers>win10-x64;osx.10.11-x64;ubuntu.16.04-x64</RuntimeIdentifiers>
</PropertyGroup>
```

### <a name="trimmerrootassembly"></a>TrimmerRootAssembly

`TrimmerRootAssembly`Element umożliwia wykluczenie zestawu z [*przycinania*](../deploying/trim-self-contained.md). Przycinanie jest procesem usuwania nieużywanych części środowiska uruchomieniowego z spakowanej aplikacji. W niektórych przypadkach przycinanie może niepoprawnie usunąć wymagane odwołania.

Poniższy kod XML wyklucza `System.Security` zestaw z przycinania.

```xml
<ItemGroup>
  <TrimmerRootAssembly Include="System.Security" />
</ItemGroup>
```

### <a name="useapphost"></a>UseAppHost

`UseAppHost`Właściwość określa, czy dla wdrożenia jest tworzony natywny plik wykonywalny. Natywny plik wykonywalny jest wymagany w przypadku wdrożeń samodzielnych.

W programie .NET Core 3,0 i jego nowszych wersjach domyślnie tworzony jest plik wykonywalny zależny od platformy. Ustaw `UseAppHost` Właściwość na `false` , aby wyłączyć generowanie pliku wykonywalnego.

```xml
<PropertyGroup>
  <UseAppHost>false</UseAppHost>
</PropertyGroup>
```

Aby uzyskać więcej informacji o wdrażaniu, zobacz [wdrażanie aplikacji .NET](../deploying/index.md).

## <a name="compile-properties"></a>Kompiluj właściwości

- [EmbeddedResourceUseDependentUponConvention](#embeddedresourceusedependentuponconvention)
- [LangVersion](#langversion)

### <a name="embeddedresourceusedependentuponconvention"></a>EmbeddedResourceUseDependentUponConvention

`EmbeddedResourceUseDependentUponConvention`Właściwość określa, czy nazwy plików manifestu zasobów są generowane na podstawie informacji o typie w plikach źródłowych, które znajdują się w plikach zasobów. Na przykład jeśli *Form1. resx* znajduje się w tym samym folderze co *Form1.cs* i `EmbeddedResourceUseDependentUponConvention` jest ustawiona na `true` , wygenerowany plik *resources* przyjmuje swoją nazwę z pierwszego typu zdefiniowanego w *Form1.cs*. Na przykład, jeśli `MyNamespace.Form1` jest pierwszym typem zdefiniowanym w *Form1.cs*, wygenerowana nazwa pliku ma *nazwę. Form1. resources*.

> [!NOTE]
> Jeśli `LogicalName` `ManifestResourceName` `DependentUpon` dla elementu określono wartość, lub lub metadanych `EmbeddedResource` , wygenerowana nazwa pliku manifestu dla tego pliku zasobów jest oparta na tym metadanych.

Domyślnie w nowym projekcie .NET ta właściwość jest ustawiona na `true` . Jeśli `false` `LogicalName` `ManifestResourceName` dla elementu w pliku projektu zostanie ustawiona wartość, i nie, lub `DependentUpon` dla tego parametru, `EmbeddedResource` Nazwa pliku manifestu zasobu jest oparta na głównej przestrzeni nazw projektu i względnej ścieżce pliku do pliku *resx* . Aby uzyskać więcej informacji, zobacz [jak nazywa się plik manifestu zasobu](../resources/manifest-file-names.md).

```xml
<PropertyGroup>
  <EmbeddedResourceUseDependentUponConvention>true</EmbeddedResourceUseDependentUponConvention>
</PropertyGroup>
```

### <a name="langversion"></a>LangVersion

`LangVersion`Właściwość umożliwia określenie konkretnej wersji języka programowania. Na przykład jeśli chcesz uzyskać dostęp do funkcji wersji zapoznawczej języka C#, ustaw wartość `LangVersion` `preview` .

```xml
<PropertyGroup>
  <LangVersion>preview</LangVersion>
</PropertyGroup>
```

Aby uzyskać więcej informacji, zobacz [wersja języka C#](../../csharp/language-reference/configure-language-version.md#override-a-default).

## <a name="code-analysis-properties"></a>Właściwości analizy kodu

### <a name="analysislevel"></a>AnalysisLevel

`AnalysisLevel`Właściwość pozwala określić poziom analizy kodu. Jeśli na przykład chcesz uzyskać dostęp do analizatorów kodu w wersji zapoznawczej, ustaw wartość `AnalysisLevel` `preview` . Wartość domyślna to `latest`.

```xml
<PropertyGroup>
  <AnalysisLevel>preview</AnalysisLevel>
</PropertyGroup>
```

W poniższej tabeli przedstawiono dostępne opcje.

| Wartość | Znaczenie |
|-|-|
| `latest` | Używane są najnowsze analizatory kodu, które zostały wydane. Jest to opcja domyślna. |
| `preview` | Są używane najnowsze analizatory kodu, nawet jeśli są one w wersji zapoznawczej. |
| `5.0` | Używany jest zestaw reguł, które zostały włączone dla wydania .NET 5,0, nawet jeśli są dostępne nowsze reguły. |
| `5` | Używany jest zestaw reguł, które zostały włączone dla wydania .NET 5,0, nawet jeśli są dostępne nowsze reguły. |

### <a name="analysismode"></a>Analizamode

Począwszy od platformy .NET 5,0, zestaw SDK platformy .NET jest dostarczany ze wszystkimi [regułami dotyczącymi jakości kodu "CA"](../../fundamentals/code-analysis/quality-rules/index.md). Domyślnie tylko [niektóre reguły są włączane](../../fundamentals/code-analysis/overview.md#enabled-rules) jako ostrzeżenia kompilacji. `AnalysisMode`Właściwość umożliwia dostosowanie zestawu reguł, które są domyślnie włączone. Można przełączać się na bardziej agresywny tryb analizy lub bardziej ostrożny tryb analizy. Na przykład jeśli chcesz włączyć wszystkie reguły domyślnie jako ostrzeżenia kompilacji, ustaw wartość na `AllEnabledByDefault` .

```xml
<PropertyGroup>
  <AnalysisMode>AllEnabledByDefault</AnalysisMode>
</PropertyGroup>
```

W poniższej tabeli przedstawiono dostępne opcje.

| Wartość | Znaczenie |
|-|-|
| `Default` | Domyślny tryb, w którym niektóre reguły są włączone jako ostrzeżenia kompilacji, niektóre reguły są włączane jako sugestie środowiska IDE programu Visual Studio, a reszta jest wyłączona. |
| `AllEnabledByDefault` | Tryb agresywny lub rezygnacji, w którym wszystkie reguły są domyślnie włączone jako ostrzeżenia kompilacji. Możesz selektywnie [zrezygnować](../../fundamentals/code-analysis/configuration-options.md) z poszczególnych reguł, aby je wyłączyć. |
| `AllDisabledByDefault` | Tryb wyłączania lub niewłączania, gdzie wszystkie reguły są domyślnie wyłączone. Można [wybiórczo](../../fundamentals/code-analysis/configuration-options.md) wybierać poszczególne reguły, aby je włączyć. |

### <a name="codeanalysistreatwarningsaserrors"></a>CodeAnalysisTreatWarningsAsErrors

`CodeAnalysisTreatWarningsAsErrors`Właściwość umożliwia skonfigurowanie, czy ostrzeżenia analizy jakości kodu (CAxxxx) powinny być traktowane jako ostrzeżenia i przerywać kompilację. Jeśli używasz `-warnaserror` flagi podczas kompilowania projektów, ostrzeżenia [analizy jakości kodu platformy .NET](../../fundamentals/code-analysis/overview.md#code-quality-analysis) również są traktowane jako błędy. Jeśli nie chcesz, aby ostrzeżenia analizy jakości kodu były traktowane jako błędy, możesz ustawić `CodeAnalysisTreatWarningsAsErrors` Właściwość programu MSBuild na `false` w pliku projektu.

```xml
<PropertyGroup>
  <CodeAnalysisTreatWarningsAsErrors>false</CodeAnalysisTreatWarningsAsErrors>
</PropertyGroup>
```

### <a name="enablenetanalyzers"></a>EnableNETAnalyzers

[Analiza jakości kodu platformy .NET](../../fundamentals/code-analysis/overview.md#code-quality-analysis) jest domyślnie włączona dla projektów przeznaczonych dla platformy .NET 5,0 lub nowszej. Można włączyć analizę kodu platformy .NET dla projektów przeznaczonych dla wcześniejszych wersji platformy .NET przez ustawienie `EnableNETAnalyzers` właściwości na `true` . Aby wyłączyć analizę kodu w dowolnym projekcie, należy ustawić tę właściwość na `false` .

```xml
<PropertyGroup>
  <EnableNETAnalyzers>true</EnableNETAnalyzers>
</PropertyGroup>
```

> [!TIP]
> Innym sposobem na włączenie analizy kodu .NET dla projektów przeznaczonych dla wersji .NET wcześniejszych niż .NET 5,0 jest ustawienie właściwości [AnalysisLevel](#analysislevel) na `latest` .

### <a name="enforcecodestyleinbuild"></a>EnforceCodeStyleInBuild

> [!NOTE]
> Ta funkcja jest obecnie eksperymentalna i może ulec zmianie między wersjami .NET 5 i .NET 6.

[Analiza stylu kodu platformy .NET](../../fundamentals/code-analysis/overview.md#code-style-analysis) jest domyślnie wyłączona w przypadku kompilacji dla wszystkich projektów .NET. Można włączyć analizę stylu kodu dla projektów .NET, ustawiając `EnforceCodeStyleInBuild` Właściwość na `true` .

```xml
<PropertyGroup>
  <EnforceCodeStyleInBuild>true</EnforceCodeStyleInBuild>
</PropertyGroup>
```

Wszystkie reguły stylu kodu, które są [skonfigurowane](../../fundamentals/code-analysis/overview.md#code-style-analysis) do wyświetlania ostrzeżeń lub błędów, będą wykonywane w przypadku naruszeń kompilacji i raportu.

## <a name="run-time-configuration-properties"></a>Właściwości konfiguracji czasu wykonywania

Niektóre zachowania w czasie wykonywania można skonfigurować, określając właściwości programu MSBuild w pliku projektu aplikacji. Aby uzyskać informacje na temat innych sposobów konfigurowania zachowania w czasie wykonywania, zobacz [Ustawienia konfiguracji w czasie wykonywania](../run-time-config/index.md).

- [ConcurrentGarbageCollection](#concurrentgarbagecollection)
- [InvariantGlobalization](#invariantglobalization)
- [RetainVMGarbageCollection](#retainvmgarbagecollection)
- [ServerGarbageCollection](#servergarbagecollection)
- [ThreadPoolMaxThreads](#threadpoolmaxthreads)
- [ThreadPoolMinThreads](#threadpoolminthreads)
- [TieredCompilation](#tieredcompilation)
- [TieredCompilationQuickJit](#tieredcompilationquickjit)
- [TieredCompilationQuickJitForLoops](#tieredcompilationquickjitforloops)

### <a name="concurrentgarbagecollection"></a>ConcurrentGarbageCollection

`ConcurrentGarbageCollection`Właściwość określa, czy jest włączone [wyrzucanie elementów bezużytecznych w tle](../../standard/garbage-collection/background-gc.md) . Ustaw wartość na `false` , aby wyłączyć wyrzucanie elementów bezużytecznych w tle. Aby uzyskać więcej informacji, zobacz w [tle GC](../run-time-config/garbage-collector.md#background-gc).

```xml
<PropertyGroup>
  <ConcurrentGarbageCollection>false</ConcurrentGarbageCollection>
</PropertyGroup>
```

### <a name="invariantglobalization"></a>InvariantGlobalization

`InvariantGlobalization`Właściwość określa, czy aplikacja jest uruchamiana w trybie *globalizacji-niezmiennym* , co oznacza, że nie ma dostępu do danych specyficznych dla kultury. Ustaw wartość tak, aby była `true` uruchamiana w trybie niezmiennym globalizacji. Aby uzyskać więcej informacji, zobacz [tryb niezmienny](../run-time-config/globalization.md#invariant-mode).

```xml
<PropertyGroup>
  <InvariantGlobalization>true</InvariantGlobalization>
</PropertyGroup>
```

### <a name="retainvmgarbagecollection"></a>RetainVMGarbageCollection

`RetainVMGarbageCollection`Właściwość konfiguruje moduł wyrzucania elementów bezużytecznych w celu umieszczenia usuniętych segmentów pamięci na liście gotowości do użycia w przyszłości lub zwolnienia. Ustawienie wartości `true` informującej Moduł wyrzucania elementów bezużytecznych w celu umieszczenia segmentów na liście gotowości. Aby uzyskać więcej informacji, zobacz temat [zachowywanie maszyny wirtualnej](../run-time-config/garbage-collector.md#retain-vm).

```xml
<PropertyGroup>
  <RetainVMGarbageCollection>true</RetainVMGarbageCollection>
</PropertyGroup>
```

### <a name="servergarbagecollection"></a>ServerGarbageCollection

`ServerGarbageCollection`Właściwość określa, czy aplikacja używa [wyrzucania elementów bezużytecznych stacji roboczej lub odzyskiwania pamięci serwera](../../standard/garbage-collection/workstation-server-gc.md). Ustaw wartość na, aby `true` użyć wyrzucania elementów bezużytecznych serwera. Aby uzyskać więcej informacji, zobacz [stacja robocza a serwer](../run-time-config/garbage-collector.md#workstation-vs-server).

```xml
<PropertyGroup>
  <ServerGarbageCollection>true</ServerGarbageCollection>
</PropertyGroup>
```

### <a name="threadpoolmaxthreads"></a>ThreadPoolMaxThreads

`ThreadPoolMaxThreads`Właściwość określa maksymalną liczbę wątków dla puli wątków roboczych. Aby uzyskać więcej informacji, zobacz [maksymalne wątki](../run-time-config/threading.md#maximum-threads).

```xml
<PropertyGroup>
  <ThreadPoolMaxThreads>20</ThreadPoolMaxThreads>
</PropertyGroup>
```

### <a name="threadpoolminthreads"></a>ThreadPoolMinThreads

`ThreadPoolMinThreads`Właściwość konfiguruje minimalną liczbę wątków dla puli wątków roboczych. Aby uzyskać więcej informacji, zobacz [minimalna liczba wątków](../run-time-config/threading.md#minimum-threads).

```xml
<PropertyGroup>
  <ThreadPoolMinThreads>4</ThreadPoolMinThreads>
</PropertyGroup>
```

### <a name="tieredcompilation"></a>TieredCompilation

`TieredCompilation`Właściwość określa, czy kompilator just in Time (JIT) używa [kompilacji warstwowej](../whats-new/dotnet-core-3-0.md#tiered-compilation). Ustaw wartość na, aby `false` wyłączyć kompilację warstwową. Aby uzyskać więcej informacji, zobacz temat [kompilacja warstwowa](../run-time-config/compilation.md#tiered-compilation).

```xml
<PropertyGroup>
  <TieredCompilation>false</TieredCompilation>
</PropertyGroup>
```

### <a name="tieredcompilationquickjit"></a>TieredCompilationQuickJit

`TieredCompilationQuickJit`Właściwość określa, czy KOMPILATOR JIT używa szybkiej JIT. Ustaw wartość na `false` , aby wyłączyć szybkie JIT. Aby uzyskać więcej informacji, zobacz [szybkie JIT](../run-time-config/compilation.md#quick-jit).

```xml
<PropertyGroup>
  <TieredCompilationQuickJit>false</TieredCompilationQuickJit>
</PropertyGroup>
```

### <a name="tieredcompilationquickjitforloops"></a>TieredCompilationQuickJitForLoops

`TieredCompilationQuickJitForLoops`Właściwość określa, czy KOMPILATOR JIT używa szybkiej JIT metod, które zawierają pętle. Ustaw wartość na, aby `true` włączyć funkcję szybkiego JIT dla metod, które zawierają pętle. Aby uzyskać więcej informacji, zobacz [szybkie JIT dla pętli](../run-time-config/compilation.md#quick-jit-for-loops).

```xml
<PropertyGroup>
  <TieredCompilationQuickJitForLoops>true</TieredCompilationQuickJitForLoops>
</PropertyGroup>
```

## <a name="reference-properties-and-items"></a>Właściwości odwołania i elementy

- [AssetTargetFallback](#assettargetfallback)
- [PackageReference](#packagereference)
- [Elementu ProjectReference](#projectreference)
- [Odwołanie](#reference)
- [Właściwości związane z przywracaniem](#restore-related-properties)

### <a name="assettargetfallback"></a>AssetTargetFallback

`AssetTargetFallback`Właściwość pozwala określić dodatkowe zgodne wersje architektury dla odwołań do projektu i pakietów NuGet. Na przykład, jeśli określisz zależność pakietu przy użyciu programu `PackageReference` , ale ten pakiet nie zawiera zasobów, które są zgodne z projektem `TargetFramework` , `AssetTargetFallback` Właściwość jest dostępna. Zgodność przywoływanego pakietu jest ponownie sprawdzana przy użyciu każdej platformy docelowej określonej w `AssetTargetFallback` .

Można ustawić `AssetTargetFallback` Właściwość na co najmniej jedną [docelową wersję platformy](../../standard/frameworks.md#supported-target-frameworks).

```xml
<PropertyGroup>
  <AssetTargetFallback>net461</AssetTargetFallback>
</PropertyGroup>
```

### <a name="packagereference"></a>PackageReference

`PackageReference`Element definiuje odwołanie do pakietu NuGet.

Ten `Include` atrybut określa identyfikator pakietu. Ten `Version` atrybut określa wersję lub zakres wersji. Aby uzyskać informacje na temat określania minimalnej wersji, maksymalnej wersji, zakresu lub dokładnego dopasowania, zobacz [zakres wersji](/nuget/concepts/package-versioning#version-ranges). Można również dodać następujące metadane do odwołania do projektu: `IncludeAssets` , `ExcludeAssets` , i `PrivateAssets` .

Fragment pliku projektu w poniższym przykładzie odwołuje się do pakietu [System. Runtime](https://www.nuget.org/packages/System.Runtime/) .

```xml
<ItemGroup>
  <PackageReference Include="System.Runtime" Version="4.3.0" />
</ItemGroup>
```

Aby uzyskać więcej informacji, zobacz [odwołania do pakietów w plikach projektu](/nuget/consume-packages/package-references-in-project-files).

### <a name="projectreference"></a>Elementu ProjectReference

`ProjectReference`Element definiuje odwołanie do innego projektu. Przywoływany projekt jest dodawany jako zależność pakietu NuGet, czyli jest traktowany tak samo jak `PackageReference` .

Ten `Include` atrybut określa ścieżkę do projektu. Można również dodać następujące metadane do odwołania do projektu: `IncludeAssets` , `ExcludeAssets` , i `PrivateAssets` .

Fragment pliku projektu w poniższym przykładzie odwołuje się do projektu o nazwie `Project2` .

```xml
<ItemGroup>
  <ProjectReference Include="..\Project2.csproj" />
</ItemGroup>
```

### <a name="reference"></a>Odwołanie

`Reference`Element definiuje odwołanie do pliku zestawu.

`Include`Atrybut określa nazwę pliku, a `HintPath` metadane określa ścieżkę do zestawu.

```xml
<ItemGroup>
  <Reference Include="MyAssembly">
    <HintPath>..\..\Assemblies\MyAssembly.dll</HintPath>
  </Reference>
</ItemGroup>
```

### <a name="restore-related-properties"></a>Właściwości związane z przywracaniem

Przywracanie przywoływanego pakietu instaluje wszystkie jego bezpośrednie zależności i wszystkie zależności tych zależności. Przywracanie pakietu można dostosować, określając właściwości, takie jak `RestorePackagesPath` i `RestoreIgnoreFailedSources` . Aby uzyskać więcej informacji na temat tych i innych właściwości, zobacz [Restore Target](/nuget/reference/msbuild-targets#restore-target).

```xml
<PropertyGroup>
  <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

## <a name="hosting-properties-and-items"></a>Hostowanie właściwości i elementów

- [EnableComHosting](#enablecomhosting)
- [EnableDynamicLoading](#enabledynamicloading)

### <a name="enablecomhosting"></a>EnableComHosting

`EnableComHosting`Właściwość wskazuje, że zestaw udostępnia serwer com. Ustawienie to `EnableComHosting` `true` oznacza również, że [EnableDynamicLoading](#enabledynamicloading) ma wartość `true` .

```xml
<PropertyGroup>
  <EnableComHosting>True</EnableComHosting>
</PropertyGroup>
```

Aby uzyskać więcej informacji, zobacz [Udostępnianie składników .NET do modelu COM](../native-interop/expose-components-to-com.md).

### <a name="enabledynamicloading"></a>EnableDynamicLoading

`EnableDynamicLoading`Właściwość wskazuje, że zestaw jest składnikiem ładowanym dynamicznie. Składnik może być [biblioteką com](/windows/win32/com/the-component-object-model) lub biblioteką niebędącą modelem COM, która może być [używana z macierzystego hosta](../tutorials/netcore-hosting.md). Ustawienie tej właściwości na `true` ma następujące skutki:

- Generowany jest *.runtimeconfig.js* pliku.
- [Przewinięcie do przodu](../whats-new/dotnet-core-3-0.md#major-version-runtime-roll-forward) jest ustawione na `LatestMinor` .
- Odwołania NuGet są kopiowane lokalnie.

```xml
<PropertyGroup>
  <EnableDynamicLoading>true</EnableDynamicLoading>
</PropertyGroup>
```

## <a name="see-also"></a>Zobacz też

- [Odwołanie do schematu programu MSBuild](/visualstudio/msbuild/msbuild-project-file-schema-reference)
- [Typowe właściwości programu MSBuild](/visualstudio/msbuild/common-msbuild-project-properties)
- [Właściwości programu MSBuild dla pakietu NuGet](/nuget/reference/msbuild-targets#pack-target)
- [Właściwości programu MSBuild do przywracania NuGet](/nuget/reference/msbuild-targets#restore-properties)
- [Dostosuj kompilację](/visualstudio/msbuild/customize-your-build)
