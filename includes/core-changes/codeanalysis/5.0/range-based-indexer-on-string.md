---
ms.openlocfilehash: 87f9cc03f334233ef286abd11e6f5ff82d7988c2
ms.sourcegitcommit: 9c45035b781caebc63ec8ecf912dc83fb6723b1f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/25/2020
ms.locfileid: "88811353"
---
### <a name="ca1831-use-asspan-or-asmemory-instead-of-range-based-indexer"></a><span data-ttu-id="6ae39-101">CA1831 użyć AsSpan lub AsMemory zamiast indeksatora opartego na zakresie</span><span class="sxs-lookup"><span data-stu-id="6ae39-101">CA1831 Use AsSpan or AsMemory instead of Range-based indexer</span></span>

<span data-ttu-id="6ae39-102">Reguła analizatora kodu platformy .NET [CA1831](/visualstudio/code-quality/ca1831) jest domyślnie włączona, począwszy od platformy .NET 5,0.</span><span class="sxs-lookup"><span data-stu-id="6ae39-102">.NET code analyzer rule [CA1831](/visualstudio/code-quality/ca1831) is enabled, by default, starting in .NET 5.0.</span></span> <span data-ttu-id="6ae39-103">Generuje ostrzeżenie kompilacji dla dowolnego kodu <xref:System.Range> , w którym jest używany indeksator oparty na ciągu, ale nie ma zamierzonego kopiowania.</span><span class="sxs-lookup"><span data-stu-id="6ae39-103">It produces a build warning for any code where a <xref:System.Range>-based indexer is used on a string, but no copy was intended.</span></span>

#### <a name="change-description"></a><span data-ttu-id="6ae39-104">Zmień opis</span><span class="sxs-lookup"><span data-stu-id="6ae39-104">Change description</span></span>

<span data-ttu-id="6ae39-105">Począwszy od platformy .NET 5,0, zestaw SDK .NET zawiera [analizatory kodu źródłowego platformy .NET](../../../../docs/fundamentals/productivity/code-analysis.md).</span><span class="sxs-lookup"><span data-stu-id="6ae39-105">Starting in .NET 5.0, the .NET SDK includes [.NET source code analyzers](../../../../docs/fundamentals/productivity/code-analysis.md).</span></span> <span data-ttu-id="6ae39-106">Niektóre z tych reguł są domyślnie włączone, w tym [CA1831](/visualstudio/code-quality/ca1831).</span><span class="sxs-lookup"><span data-stu-id="6ae39-106">Several of these rules are enabled, by default, including [CA1831](/visualstudio/code-quality/ca1831).</span></span> <span data-ttu-id="6ae39-107">Jeśli projekt zawiera kod naruszający tę regułę i jest skonfigurowany do traktowania ostrzeżeń jako błędów, ta zmiana może spowodować uszkodzenie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="6ae39-107">If your project contains code that violates this rule and is configured to treat warnings as errors, this change could break your build.</span></span>

<span data-ttu-id="6ae39-108">CA1831 reguły odnajduje wystąpienia <xref:System.Range> , w których jest używany indeksator oparty na ciągu, ale nie ma zamierzonego kopiowania.</span><span class="sxs-lookup"><span data-stu-id="6ae39-108">Rule CA1831 finds instances where a <xref:System.Range>-based indexer is used on a string, but no copy was intended.</span></span> <span data-ttu-id="6ae39-109">Jeśli <xref:System.Range> indeksator jest używany bezpośrednio w ciągu do tworzenia rzutowania niejawnego, wówczas tworzona jest niezbędna kopia żądanej części ciągu.</span><span class="sxs-lookup"><span data-stu-id="6ae39-109">If the <xref:System.Range>-based indexer is used directly on a string to produce an implicit cast, then an unnecessary copy of the requested portion of the string is created.</span></span> <span data-ttu-id="6ae39-110">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="6ae39-110">For example:</span></span>

```csharp
ReadOnlySpan<char> slice = str[1..3];
```

<span data-ttu-id="6ae39-111">CA1831 sugeruje użycie <xref:System.Range> indeksatora opartego na indeksie dla *zakresu* ciągu.</span><span class="sxs-lookup"><span data-stu-id="6ae39-111">CA1831 suggests using the <xref:System.Range>-based indexer on a *span* of the string, instead.</span></span> <span data-ttu-id="6ae39-112">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="6ae39-112">For example:</span></span>

```csharp
ReadOnlySpan<char> slice = str.AsSpan()[1..3];
```

#### <a name="version-introduced"></a><span data-ttu-id="6ae39-113">Wprowadzona wersja</span><span class="sxs-lookup"><span data-stu-id="6ae39-113">Version introduced</span></span>

<span data-ttu-id="6ae39-114">5,0 wersja zapoznawcza 8</span><span class="sxs-lookup"><span data-stu-id="6ae39-114">5.0 Preview 8</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="6ae39-115">Zalecana akcja</span><span class="sxs-lookup"><span data-stu-id="6ae39-115">Recommended action</span></span>

- <span data-ttu-id="6ae39-116">Aby poprawić kod i uniknąć niepotrzebnych alokacji, wywołaj <xref:System.MemoryExtensions.AsSpan(System.String)> lub <xref:System.MemoryExtensions.AsMemory(System.String)> przed użyciem <xref:System.Range> indeksatora opartego na usłudze.</span><span class="sxs-lookup"><span data-stu-id="6ae39-116">To correct your code and avoid unnecessary allocations, call <xref:System.MemoryExtensions.AsSpan(System.String)> or <xref:System.MemoryExtensions.AsMemory(System.String)> before using the <xref:System.Range>-based indexer.</span></span> <span data-ttu-id="6ae39-117">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="6ae39-117">For example:</span></span>

  ```csharp
  ReadOnlySpan<char> slice = str.AsSpan()[1..3];
  ```

- <span data-ttu-id="6ae39-118">Jeśli nie chcesz zmieniać kodu, możesz wyłączyć regułę, ustawiając jej ważność na `suggestion` lub `none` .</span><span class="sxs-lookup"><span data-stu-id="6ae39-118">If you don't want to change your code, you can disable the rule by setting its severity to `suggestion` or `none`.</span></span> <span data-ttu-id="6ae39-119">Aby uzyskać więcej informacji, zobacz [Konfigurowanie reguł analizy kodu](../../../../docs/fundamentals/productivity/configure-code-analysis-rules.md).</span><span class="sxs-lookup"><span data-stu-id="6ae39-119">For more information, see [Configure code analysis rules](../../../../docs/fundamentals/productivity/configure-code-analysis-rules.md).</span></span>

- <span data-ttu-id="6ae39-120">Aby całkowicie wyłączyć analizę kodu, ustaw `EnableNETAnalyzers` wartość `false` w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="6ae39-120">To disable code analysis completely, set `EnableNETAnalyzers` to `false` in your project file.</span></span> <span data-ttu-id="6ae39-121">Aby uzyskać więcej informacji, zobacz [EnableNETAnalyzers](../../../../docs/core/project-sdk/msbuild-props.md#enablenetanalyzers).</span><span class="sxs-lookup"><span data-stu-id="6ae39-121">For more information, see [EnableNETAnalyzers](../../../../docs/core/project-sdk/msbuild-props.md#enablenetanalyzers).</span></span>

#### <a name="category"></a><span data-ttu-id="6ae39-122">Kategoria</span><span class="sxs-lookup"><span data-stu-id="6ae39-122">Category</span></span>

<span data-ttu-id="6ae39-123">Analiza kodu</span><span class="sxs-lookup"><span data-stu-id="6ae39-123">Code analysis</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="6ae39-124">Dotyczy interfejsów API</span><span class="sxs-lookup"><span data-stu-id="6ae39-124">Affected APIs</span></span>

- <xref:System.Range?displayProperty=fullName>

<!--

#### Affected APIs

- `T:System.Range`

-->