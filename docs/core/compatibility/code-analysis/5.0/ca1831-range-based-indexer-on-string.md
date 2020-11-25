---
title: 'Nieprzerwana zmiana: CA1831: Użyj AsSpan zamiast indeksatorów opartych na zakresie dla ciągu'
description: Zapoznaj się z nieprzerwaną zmianą w programie .NET 5,0 spowodowaną przez włączenie reguły analizy kodu CA1831.
ms.date: 08/21/2020
ms.openlocfilehash: 74f34af04a56b73478ffb3305d69ed49f3a30072
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95761331"
---
# <a name="warning-ca1831-use-asspan-instead-of-range-based-indexers-for-string"></a>Ostrzeżenie CA1831: Użyj AsSpan zamiast indeksatorów opartych na zakresie dla ciągu

Reguła analizatora kodu platformy .NET [CA1831](/visualstudio/code-quality/ca1831) jest domyślnie włączona, począwszy od platformy .NET 5,0. Generuje ostrzeżenie kompilacji dla dowolnego kodu <xref:System.Range> , w którym jest używany indeksator oparty na ciągu, ale nie ma zamierzonego kopiowania.

## <a name="change-description"></a>Zmień opis

Począwszy od platformy .NET 5,0, zestaw SDK .NET zawiera [analizatory kodu źródłowego platformy .NET](../../../../fundamentals/code-analysis/overview.md). Niektóre z tych reguł są domyślnie włączone, w tym [CA1831](/visualstudio/code-quality/ca1831). Jeśli projekt zawiera kod naruszający tę regułę i jest skonfigurowany do traktowania ostrzeżeń jako błędów, ta zmiana może spowodować uszkodzenie kompilacji.

CA1831 reguły odnajduje wystąpienia <xref:System.Range> , w których jest używany indeksator oparty na ciągu, ale nie ma zamierzonego kopiowania. Jeśli <xref:System.Range> indeksator jest używany bezpośrednio w ciągu do tworzenia rzutowania niejawnego, wówczas tworzona jest niezbędna kopia żądanej części ciągu. Na przykład:

```csharp
ReadOnlySpan<char> slice = str[1..3];
```

CA1831 sugeruje użycie <xref:System.Range> indeksatora opartego na indeksie dla *zakresu* ciągu. Na przykład:

```csharp
ReadOnlySpan<char> slice = str.AsSpan()[1..3];
```

## <a name="version-introduced"></a>Wprowadzona wersja

5,0

## <a name="recommended-action"></a>Zalecana akcja

- Aby poprawić kod i uniknąć niepotrzebnych alokacji, wywołaj <xref:System.MemoryExtensions.AsSpan(System.String)> lub <xref:System.MemoryExtensions.AsMemory(System.String)> przed użyciem <xref:System.Range> indeksatora opartego na usłudze. Na przykład:

  ```csharp
  ReadOnlySpan<char> slice = str.AsSpan()[1..3];
  ```

- Jeśli nie chcesz zmieniać kodu, możesz wyłączyć regułę, ustawiając jej ważność na `suggestion` lub `none` . Aby uzyskać więcej informacji, zobacz [Konfigurowanie reguł analizy kodu](../../../../fundamentals/productivity/configure-code-analysis-rules.md).

- Aby całkowicie wyłączyć analizę kodu, ustaw `EnableNETAnalyzers` wartość `false` w pliku projektu. Aby uzyskać więcej informacji, zobacz [EnableNETAnalyzers](../../../project-sdk/msbuild-props.md#enablenetanalyzers).

## <a name="affected-apis"></a>Dotyczy interfejsów API

- <xref:System.Range?displayProperty=fullName>

<!--

### Affected APIs

- `T:System.Range`

### Category

Code analysis

-->
