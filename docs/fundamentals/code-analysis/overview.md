---
title: Analiza kodu w programie .NET
titleSuffix: ''
description: Dowiedz się więcej o analizie kodu źródłowego w zestawie SDK platformy .NET.
ms.date: 12/04/2020
ms.topic: overview
ms.custom: updateeachrelease
helpviewer_keywords:
- code analysis
- code analyzers
ms.openlocfilehash: 2f59b97de6f92e5a9bf927e1318286e400017dad
ms.sourcegitcommit: 81f1bba2c97a67b5ca76bcc57b37333ffca60c7b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/10/2020
ms.locfileid: "97009849"
---
# <a name="overview-of-net-source-code-analysis"></a>Przegląd analizy kodu źródłowego platformy .NET

Analizatory platformy kompilatora .NET (Roslyn) sprawdzają kod C# lub Visual Basic pod kątem problemów dotyczących jakości i stylu. Począwszy od platformy .NET 5,0, analizatory te są dołączone do zestawu .NET SDK i nie trzeba ich instalować oddzielnie. Jeśli projekt jest przeznaczony dla platformy .NET 5 lub nowszej, analiza kodu jest domyślnie włączona. Jeśli projekt jest przeznaczony dla innej implementacji platformy .NET, na przykład .NET Core, .NET Standard lub .NET Framework, należy ręcznie włączyć analizę kodu, ustawiając właściwość [EnableNETAnalyzers](../../core/project-sdk/msbuild-props.md#enablenetanalyzers) na `true` .

Jeśli nie chcesz przenosić do programu .NET 5 lub SDK lub wolisz model oparty na pakiecie NuGet, analizatory są również dostępne w [pakiecie NuGet Microsoft. CodeAnalysis. Serviceanalizators](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers). Można preferować model oparty na pakiecie dla aktualizacji wersji na żądanie.

> [!NOTE]
> Analizatory .NET to Target-Framework niezależny od. Oznacza to, że projekt nie musi wskazywać określonej implementacji platformy .NET. Analizatory współpracują z projektami przeznaczonymi do pracy, `net5.0` a także ze starszymi wersjami .NET, takimi jak `netcoreapp3.1` i `net472` .

Jeśli wykryto naruszenia reguł przez analizator, są one raportowane jako sugestie, ostrzeżenia lub błędy w zależności od sposobu [skonfigurowania](configuration-options.md)każdej reguły. Naruszenia analizy kodu są wyświetlane z prefiksem "CA" lub "IDE", aby odróżnić je od błędów kompilatora.

## <a name="code-quality-analysis"></a>Analiza jakości kodu

Reguły *analizy jakości kodu* ("CAxxxx") sprawdzają kod C# lub Visual Basic w celu zapewnienia bezpieczeństwa, wydajności, projektowania i innych problemów. Analiza jest domyślnie włączona dla projektów przeznaczonych dla platformy .NET 5,0 lub nowszej. Możesz włączyć analizę kodu dla projektów przeznaczonych dla wcześniejszych wersji .NET, ustawiając właściwość [EnableNETAnalyzers](../../core/project-sdk/msbuild-props.md#enablenetanalyzers) na `true` . Możesz również wyłączyć analizę kodu dla projektu, ustawiając wartość `EnableNETAnalyzers` na `false` .

> [!TIP]
> Jeśli używasz programu Visual Studio:
>
> - Wiele reguł analizatorów ma skojarzone *poprawki kodu* , które można zastosować, aby rozwiązać problem. Poprawki kodu są wyświetlane w menu ikony żarówki.
> - Analizę kodu można włączyć lub wyłączyć, klikając prawym przyciskiem myszy projekt w Eksplorator rozwiązań i wybierając pozycję **Właściwości**  >  karta **Analiza kodu** > **włączyć analizatory platformy .NET**.

### <a name="enabled-rules"></a>Włączone reguły

Następujące reguły są domyślnie włączone w programie .NET 5,0.

| Identyfikator diagnostyki | Kategoria | Ważność | Opis |
| - | - | - | - |
| [CA1416](/visualstudio/code-quality/ca1416) | Współdziałanie | Ostrzeżenie | Analizator zgodności platformy |
| [CA1417](/visualstudio/code-quality/ca1417) | Współdziałanie | Ostrzeżenie | Nie należy używać `OutAttribute` w parametrach ciągu dla elementu P/Invoke |
| [CA1831](/visualstudio/code-quality/ca1831) | Wydajność | Ostrzeżenie | Użyj `AsSpan` zamiast indeksatorów opartych na zakresie dla ciągu, gdy jest to potrzebne |
| [CA2013](/visualstudio/code-quality/ca2013) | Niezawodność | Ostrzeżenie | Nie używaj `ReferenceEquals` z typami wartości |
| [CA2014](/visualstudio/code-quality/ca2014) | Niezawodność | Ostrzeżenie | Nie używaj `stackalloc` w pętlach |
| [CA2015](/visualstudio/code-quality/ca2015) | Niezawodność | Ostrzeżenie | Nie Definiuj finalizatorów dla typów pochodnych <xref:System.Buffers.MemoryManager%601> |
| [CA2200](/visualstudio/code-quality/ca2200) | Użycie | Ostrzeżenie | Ponowie zgłoś wyjątek, aby zachować szczegóły stosu
| [CA2247](/visualstudio/code-quality/ca2247) | Użycie | Ostrzeżenie | Argument przesłany do konstruktora TaskCompletionSource powinien być <xref:System.Threading.Tasks.TaskCreationOptions> wyliczeniem zamiast <xref:System.Threading.Tasks.TaskContinuationOptions> |

Można zmienić ważność tych reguł, aby wyłączyć je lub podnieść ich liczbę do błędów. Możesz również [włączyć więcej reguł](#enable-additional-rules).

- Aby zapoznać się z listą reguł, które są zawarte w poszczególnych wersjach zestawu SDK platformy .NET, zobacz [wersje analizatora](https://github.com/dotnet/roslyn-analyzers/blob/master/src/NetAnalyzers/Core/AnalyzerReleases.Shipped.md).
- Aby uzyskać listę wszystkich reguł jakości kodu, zobacz [reguły jakości kodu](quality-rules/index.md).

### <a name="enable-additional-rules"></a>Włącz dodatkowe reguły

*Tryb analizy* odnosi się do wstępnie zdefiniowanej konfiguracji analizy kodu, w której jest włączona żadna, niektóre lub wszystkie reguły. W domyślnym trybie analizy tylko niewielka liczba reguł jest [włączana jako ostrzeżenia kompilacji](#enabled-rules). Tryb analizy dla projektu można zmienić, ustawiając właściwość [analizymode](../../core/project-sdk/msbuild-props.md#analysismode) w pliku projektu. Dopuszczalne są następujące wartości:

| Wartość | Opis |
| - | - |
| `AllDisabledByDefault` | Jest to najbardziej umiarkowany tryb. Wszystkie reguły są domyślnie wyłączone. Można [wybiórczo](configuration-options.md) wybierać poszczególne reguły, aby je włączyć.<br /><br />`<AnalysisMode>AllDisabledByDefault</AnalysisMode>` |
| `AllEnabledByDefault` | Jest to najbardziej agresywny tryb. Wszystkie reguły są włączane jako ostrzeżenia kompilacji. Możesz selektywnie [zrezygnować z](configuration-options.md) poszczególnych reguł, aby je wyłączyć.<br /><br />`<AnalysisMode>AllEnabledByDefault</AnalysisMode>` |
| `Default` | Domyślny tryb, w którym kilku reguły są włączane jako ostrzeżenia, inne są włączane tylko jako sugestie środowiska IDE programu Visual Studio z odpowiednimi poprawkami kodu, a pozostałe są wyłączane całkowicie. Możesz wybiórczo wybierać [lub](configuration-options.md) wyłączać poszczególne reguły, aby je wyłączyć.<br /><br />`<AnalysisMode>Default</AnalysisMode>` |

Aby znaleźć domyślną ważność dla każdej dostępnej reguły i zdecydować, czy reguła jest włączona w domyślnym trybie analizy, zobacz [pełną listę reguł](https://github.com/dotnet/roslyn-analyzers/blob/master/src/NetAnalyzers/Core/AnalyzerReleases.Shipped.md).

### <a name="treat-warnings-as-errors"></a>Traktuj ostrzeżenia jako błędy

Jeśli używasz `-warnaserror` flagi podczas kompilowania projektów, wszystkie ostrzeżenia analizy kodu są również traktowane jako błędy. Jeśli nie chcesz, aby ostrzeżenia o jakości kodu (CAxxxx) były traktowane jako błędy w obecności `-warnaserror` , można ustawić `CodeAnalysisTreatWarningsAsErrors` Właściwość programu MSBuild na `false` w pliku projektu.

```xml
<PropertyGroup>
  <CodeAnalysisTreatWarningsAsErrors>false</CodeAnalysisTreatWarningsAsErrors>
</PropertyGroup>
```

Nadal zobaczysz wszelkie ostrzeżenia analizy kodu, ale nie spowoduje to przerwania kompilacji.

### <a name="latest-updates"></a>Najnowsze aktualizacje

Domyślnie podczas uaktualniania do nowszych wersji zestawu .NET SDK otrzymasz najnowsze reguły analizy kodu i domyślne konfiguracje reguł. Jeśli nie chcesz tego zachowania, na przykład jeśli chcesz mieć pewność, że żadne nowe reguły nie są włączone lub wyłączone, możesz je zastąpić w jeden z następujących sposobów:

- Ustaw `AnalysisLevel` Właściwość programu MSBuild na określoną wartość, aby zablokować ostrzeżenia do tego zestawu. W przypadku uaktualniania do nowszego zestawu SDK nadal będą dostępne poprawki błędów dla tych ostrzeżeń, ale nie są włączone żadne nowe ostrzeżenia i żadne istniejące ostrzeżenia nie zostaną wyłączone. Aby na przykład zablokować zestaw reguł do tych, które są dostarczane z wersją 5,0 zestawu .NET SDK, Dodaj następujący wpis do pliku projektu.

  ```xml
  <PropertyGroup>
    <AnalysisLevel>5.0</AnalysisLevel>
  </PropertyGroup>
  ```

  > [!TIP]
  > Wartość domyślna `AnalysisLevel` Właściwości to `latest` , co oznacza, że podczas przechodzenia do nowszych wersji zestawu .NET SDK zawsze otrzymujesz najnowsze reguły analizy kodu.

  Aby uzyskać więcej informacji i wyświetlić listę możliwych wartości, zobacz [AnalysisLevel](../../core/project-sdk/msbuild-props.md#analysislevel).

- Zainstaluj [pakiet NuGet Microsoft. CodeAnalysis. Serviceanalizators](https://github.com/dotnet/roslyn-analyzers#microsoftcodeanalysisnetanalyzers) , aby oddzielić aktualizacje reguł z aktualizacji zestawu SDK platformy .NET. Zainstalowanie pakietu powoduje wyłączenie wbudowanych analizatorów zestawu SDK i wygenerowanie ostrzeżenia kompilacji, jeśli zestaw SDK zawiera nowszą wersję zestawu narzędzi niż pakiet NuGet.

## <a name="code-style-analysis"></a>Analiza stylu kodu

Reguły *analizy kodu w kodzie* ("IDExxxx") umożliwiają definiowanie i konserwowanie spójnego stylu kodu w bazie kodu. Domyślne ustawienia obsługi są następujące:

- Kompilacja w wierszu polecenia: Analiza stylu kodu jest domyślnie wyłączona dla wszystkich projektów .NET w kompilacjach w wierszu polecenia.
- Visual Studio: Analiza stylu kodu jest domyślnie włączona dla wszystkich projektów .NET w programie Visual Studio jako [szybkie akcje refaktoryzacji kodu](/visualstudio/ide/code-generation-in-visual-studio).

Począwszy od platformy .NET 5,0, można włączyć analizę stylu kodu dla kompilacji, zarówno w wierszu polecenia, jak i w programie Visual Studio. Naruszenia stylu kodu są wyświetlane jako ostrzeżenia lub błędy z prefiksem "IDE". Umożliwia to wymuszanie spójnych stylów kodu w czasie kompilacji.

Aby zapoznać się z pełną listą reguł analizy w stylu kodu, zobacz [reguły dotyczące stylu kodu](style-rules/index.md).

### <a name="enable-on-build"></a>Włącz przy kompilacji

Wykonaj następujące kroki, aby włączyć analizę stylu kodu podczas kompilacji:

1. Ustaw właściwość programu MSBuild [EnforceCodeStyleInBuild](../../core/project-sdk/msbuild-props.md#enforcecodestyleinbuild) na wartość `true` .

1. W pliku *. editorconfig* [Skonfiguruj](configuration-options.md) każdą regułę stylu kodu "IDE", która ma być uruchamiana podczas kompilacji jako ostrzeżenie lub błąd. Przykład:

   ```ini
   [*.{cs,vb}]
   # IDE0040: Accessibility modifiers required (escalated to a build warning)
   dotnet_diagnostic.IDE0040.severity = warning
   ```

   Alternatywnie można skonfigurować całą kategorię "Style" jako ostrzeżenie lub błąd, domyślnie, a następnie selektywnie wyłączyć reguły, które nie mają być uruchamiane podczas kompilacji. Przykład:

   ```ini
   [*.{cs,vb}]

   # Default severity for analyzer diagnostics with category 'Style' (escalated to build warnings)
   dotnet_analyzer_diagnostic.category-Style.severity = warning

   # IDE0040: Accessibility modifiers required (disabled on build)
   dotnet_diagnostic.IDE0040.severity = silent
   ```

> [!NOTE]
> Funkcja analizy w stylu kodu jest eksperymentalna i może ulec zmianie między wersjami .NET 5 i .NET 6.

## <a name="suppress-a-warning"></a>Pomiń ostrzeżenie

Aby pominąć naruszenie reguły, należy ustawić opcję ważności dla tego identyfikatora reguły na `none` w pliku EditorConfig. Przykład:

```ini
dotnet_diagnostic.CA1822.severity = none
```

Program Visual Studio oferuje dodatkowe sposoby pomijania ostrzeżeń z reguł analizy kodu. Aby uzyskać więcej informacji, zobacz [pomijanie naruszeń](/visualstudio/code-quality/use-roslyn-analyzers#suppress-violations).

Aby uzyskać więcej informacji o zakresie reguł, zobacz [Konfigurowanie ważności reguły](configuration-options.md#severity-level).

## <a name="third-party-analyzers"></a>Analizatory innych firm

Oprócz oficjalnych analizatorów .NET, można również zainstalować [analizatory](https://www.nuget.org/packages/SonarAnalyzer.CSharp/)innych firm, takie jak [StyleCop](https://www.nuget.org/packages/StyleCop.Analyzers/), [Roslynator](https://www.nuget.org/packages/Roslynator.Analyzers/), analizatorze [XUnit](https://www.nuget.org/packages/xunit.analyzers/)i sonar.

## <a name="see-also"></a>Zobacz także

- [Odwołanie do reguły analizy jakości kodu](quality-rules/index.md)
- [Odwołanie do reguły analizy stylu kodu](style-rules/index.md)
- [Analiza kodu w programie Visual Studio](/visualstudio/code-quality/roslyn-analyzers-overview)
- [Zestaw SDK platformy kompilatora .NET](../../csharp/roslyn-sdk/index.md)
- [Samouczek: Napisz pierwszy Analizator i poprawkę kodu](../../csharp/roslyn-sdk/tutorials/how-to-write-csharp-analyzer-code-fix.md)
