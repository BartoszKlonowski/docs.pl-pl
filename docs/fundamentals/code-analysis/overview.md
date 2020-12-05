---
title: Analiza kodu w programie .NET
titleSuffix: ''
description: Dowiedz się więcej o analizie kodu źródłowego w zestawie SDK platformy .NET.
ms.date: 08/22/2020
ms.topic: overview
ms.custom: updateeachrelease
helpviewer_keywords:
- code analysis
- code analyzers
ms.openlocfilehash: 8efac4d5e3fddcb9fdc6e08bcc933f2776420ced
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96739977"
---
# <a name="overview-of-net-source-code-analysis"></a>Przegląd analizy kodu źródłowego platformy .NET

Analizatory platformy kompilatora .NET (Roslyn) sprawdzają kod C# lub Visual Basic pod kątem problemów dotyczących jakości i stylu. Począwszy od wersji .NET 5.0 te analizatory są uwzględnione w zestawie .NET SDK. Jeśli nie chcesz przenosić do programu .NET 5 lub SDK lub wolisz model oparty na pakiecie NuGet, analizatory są również dostępne w `Microsoft.CodeAnalysis.NetAnalyzers` [pakiecie NuGet](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers). Można preferować model oparty na pakiecie dla aktualizacji wersji na żądanie.

> [!NOTE]
> Analizatory .NET to target-platform niezależny od. Oznacza to, że projekt nie musi być przeznaczony dla konkretnej platformy .NET. Analizatory współpracują z projektami przeznaczonymi do pracy, `net5.0` a także ze starszymi wersjami platformy .NET, takimi jak `netcoreapp` , `netstandard` i `net472` .

- [Analiza jakości kodu (reguły "CAxxxx")](#code-quality-analysis)
- [Analiza stylu kodu (reguły "IDExxxx")](#code-style-analysis)

Jeśli wykryto naruszenia reguł przez analizator, są one raportowane jako sugestie, ostrzeżenia lub błędy w zależności od sposobu [skonfigurowania](configuration-options.md)każdej reguły. Naruszenia analizy kodu są wyświetlane z prefiksem "CA" lub "IDE", aby odróżnić je od błędów kompilatora.

> [!TIP]
>
> - Można także zainstalować [analizatory](https://www.nuget.org/packages/SonarAnalyzer.CSharp/)innych firm, takie jak [StyleCop](https://www.nuget.org/packages/StyleCop.Analyzers/), [Roslynator](https://www.nuget.org/packages/Roslynator.Analyzers/), analizatorze [XUnit](https://www.nuget.org/packages/xunit.analyzers/)i sonar.
> - Jeśli używasz programu Visual Studio, wiele reguł analizatora ma skojarzone *poprawki kodu* , które można zastosować, aby rozwiązać problem. Poprawki kodu są wyświetlane w menu ikony żarówki.

## <a name="code-quality-analysis"></a>Analiza jakości kodu

_Reguły analizy jakości kodu ("CA")_ sprawdzają kod C# lub Visual Basic w celu zapewnienia bezpieczeństwa, wydajności, projektowania i innych problemów. Analiza jest domyślnie włączona dla projektów przeznaczonych dla platformy .NET 5,0 lub nowszej. Możesz włączyć analizę kodu dla projektów przeznaczonych dla wcześniejszych wersji .NET, ustawiając właściwość [EnableNETAnalyzers](../../core/project-sdk/msbuild-props.md#enablenetanalyzers) na `true` . Możesz również wyłączyć analizę kodu dla projektu, ustawiając wartość `EnableNETAnalyzers` na `false` .

> [!TIP]
> W programie Visual Studio można włączać lub wyłączać analizę kodu przy użyciu okno Właściwości projektu. Aby uzyskać dostęp do projektu okno Właściwości, kliknij prawym przyciskiem myszy projekt w obszarze Eksplorator rozwiązań i wybierz polecenie **Właściwości**. Następnie wybierz kartę **Analiza kodu** , a następnie zaznacz lub wyczyść pole wyboru, aby **włączyć analizatory platformy .NET**.

### <a name="enabled-rules"></a>Włączone reguły

Następujące reguły są domyślnie włączone w programie .NET 5,0 w wersji zapoznawczej 8.

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

Można zmienić ważność tych reguł, aby wyłączyć je lub podnieść ich liczbę do błędów.

Aby uzyskać pełną listę dostępnych reguł jakości kodu, zobacz [reguły jakości kodu](quality-rules/index.md).

### <a name="enable-additional-rules"></a>Włącz dodatkowe reguły

Począwszy od platformy .NET 5,0 RC2, zestaw .NET SDK jest dostarczany ze wszystkimi [regułami dotyczącymi jakości kodu "CA"](/visualstudio/code-quality/code-analysis-for-managed-code-warnings). Aby zapoznać się z pełną listą reguł, które są dołączone do poszczególnych wersji zestawu SDK platformy .NET, zobacz [wersje analizatora](https://github.com/dotnet/roslyn-analyzers/blob/master/src/NetAnalyzers/Core/AnalyzerReleases.Shipped.md).

#### <a name="default-analysis-mode"></a>Domyślny tryb analizy

W domyślnym trybie analizy niektóre reguły są [domyślnie włączone](#enabled-rules) jako ostrzeżenia kompilacji. Niektóre inne reguły są domyślnie włączone tylko jako sugestie środowiska IDE programu Visual Studio z odpowiednimi poprawkami kodu. Pozostałe reguły są domyślnie wyłączone. [Pełna lista reguł](https://github.com/dotnet/roslyn-analyzers/blob/master/src/NetAnalyzers/Core/AnalyzerReleases.Shipped.md) zawiera domyślną ważność każdej reguły i niezależnie od tego, czy reguła jest włączona domyślnie w domyślnym trybie analizy.

#### <a name="custom-analysis-mode"></a>Niestandardowy tryb analizy

[Reguły analizy kodu można skonfigurować](configuration-options.md) do włączania lub wyłączania pojedynczej reguły lub kategorii reguł. Ponadto można użyć właściwości [analysismode](../../core/project-sdk/msbuild-props.md#analysismode) do przełączenia do jednego z następujących trybów analizy niestandardowej:

- Tryb _agresywności_ lub _rezygnacji_ : wszystkie reguły są domyślnie włączone jako ostrzeżenia kompilacji. Możesz selektywnie [zrezygnować](configuration-options.md) z poszczególnych reguł, aby je wyłączyć.
- _Conservative_ Tryb wyłączania i _włączania_ : wszystkie reguły są domyślnie wyłączone. Można [wybiórczo](configuration-options.md) wybierać poszczególne reguły, aby je włączyć.

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

[Analiza stylu kodu](/visualstudio/ide/editorconfig-code-style-settings-reference) (reguły "IDExxxx") umożliwia definiowanie i konserwowanie spójnego stylu kodu w bazie kodu. Poniżej przedstawiono ustawienia domyślne:

- Kompilacja w wierszu polecenia: Analiza stylu kodu jest domyślnie wyłączona dla wszystkich projektów .NET na kompilacjach w wierszu polecenia.
- Visual Studio: Analiza stylu kodu jest domyślnie włączona dla wszystkich projektów .NET w programie Visual Studio jako [szybkie akcje refaktoryzacji kodu](/visualstudio/ide/code-generation-in-visual-studio).

Począwszy od platformy .NET 5,0 RC2, można włączyć analizę stylu kodu dla kompilacji, zarówno w wierszu polecenia, jak i w programie Visual Studio. Naruszenia stylu kodu są wyświetlane jako ostrzeżenia lub błędy z prefiksem "IDE". Umożliwia to wymuszanie spójnych stylów kodu w czasie kompilacji.

> [!NOTE]
> Funkcja analizy stylu kodu jest eksperymentalna i może ulec zmianie między wersjami .NET 5 i .NET 6.

Procedura włączania analizy stylów kodu podczas kompilacji:

1. Ustaw właściwość programu MSBuild [EnforceCodeStyleInBuild](../../core/project-sdk/msbuild-props.md#enforcecodestyleinbuild) na wartość `true` .

1. W pliku *. editorconfig* [Skonfiguruj](configuration-options.md) każdą regułę stylu kodu "IDE", która ma być uruchamiana podczas kompilacji jako ostrzeżenie lub błąd. Na przykład:

   ```ini
   [*.{cs,vb}]
   # IDE0040: Accessibility modifiers required (escalated to a build warning)
   dotnet_diagnostic.IDE0040.severity = warning
   ```

   Alternatywnie można skonfigurować całą kategorię "Style" jako ostrzeżenie lub błąd, domyślnie, a następnie selektywnie wyłączyć reguły, które nie mają być uruchamiane podczas kompilacji. Na przykład:

   ```ini
   [*.{cs,vb}]

   # Default severity for analyzer diagnostics with category 'Style' (escalated to build warnings)
   dotnet_analyzer_diagnostic.category-Style.severity = warning

   # IDE0040: Accessibility modifiers required (disabled on build)
   dotnet_diagnostic.IDE0040.severity = silent
   ```

## <a name="suppress-a-warning"></a>Pomiń ostrzeżenie

Aby pominąć naruszenie reguły, należy ustawić opcję ważności dla tego identyfikatora reguły na `none` w pliku EditorConfig. Na przykład:

```ini
dotnet_diagnostic.CA1822.severity = none
```

Program Visual Studio oferuje dodatkowe sposoby pomijania ostrzeżeń z reguł analizy kodu. Aby uzyskać więcej informacji, zobacz [pomijanie naruszeń](/visualstudio/code-quality/use-roslyn-analyzers#suppress-violations).

Aby uzyskać więcej informacji o zakresie reguł, zobacz [Konfigurowanie ważności reguły](configuration-options.md#severity-level).

## <a name="see-also"></a>Zobacz także

- [Odwołanie do reguły analizy jakości kodu](quality-rules/index.md)
- [Odwołanie do reguły analizy stylu kodu](style-rules/index.md)
- [Analiza kodu w programie Visual Studio](/visualstudio/code-quality/roslyn-analyzers-overview)
- [Zestaw SDK platformy kompilatora .NET](../../csharp/roslyn-sdk/index.md)
- [Samouczek: Napisz pierwszy Analizator i poprawkę kodu](../../csharp/roslyn-sdk/tutorials/how-to-write-csharp-analyzer-code-fix.md)
