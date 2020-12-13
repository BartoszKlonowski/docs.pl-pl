---
ms.openlocfilehash: 97fab784acac4331894547eea27fc21b485597fb
ms.sourcegitcommit: fcbe432482464b1639decad78cc4dc8387c6269e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/12/2020
ms.locfileid: "97366878"
---
### <a name="passing-groupcollection-to-extension-methods-taking-ienumerablet-requires-disambiguation"></a><span data-ttu-id="4f94e-101">Przekazanie grupy GroupCollection do metod rozszerzających, które \<T> wymagają uściślania</span><span class="sxs-lookup"><span data-stu-id="4f94e-101">Passing GroupCollection to extension methods taking IEnumerable\<T> requires disambiguation</span></span>

<span data-ttu-id="4f94e-102">Podczas wywoływania metody rozszerzenia, która przyjmuje obiekt `IEnumerable<T>` na <xref:System.Text.RegularExpressions.GroupCollection> , należy odróżnić typ za pomocą rzutowania.</span><span class="sxs-lookup"><span data-stu-id="4f94e-102">When calling an extension method that takes an `IEnumerable<T>` on a <xref:System.Text.RegularExpressions.GroupCollection>, you must disambiguate the type using a cast.</span></span>

#### <a name="change-description"></a><span data-ttu-id="4f94e-103">Zmień opis</span><span class="sxs-lookup"><span data-stu-id="4f94e-103">Change description</span></span>

<span data-ttu-id="4f94e-104">Począwszy od platformy .NET Core 3,0, <xref:System.Text.RegularExpressions.GroupCollection?displayProperty=nameWithType> implementuje `IEnumerable<KeyValuePair<String,Group>>` oprócz innych typów, w tym `IEnumerable<Group>` .</span><span class="sxs-lookup"><span data-stu-id="4f94e-104">Starting in .NET Core 3.0, <xref:System.Text.RegularExpressions.GroupCollection?displayProperty=nameWithType> implements `IEnumerable<KeyValuePair<String,Group>>` in addition to the other types it implements, including `IEnumerable<Group>`.</span></span> <span data-ttu-id="4f94e-105">Powoduje to niejednoznaczność podczas wywoływania metody rozszerzenia, która przyjmuje <xref:System.Collections.Generic.IEnumerable%601> .</span><span class="sxs-lookup"><span data-stu-id="4f94e-105">This results in ambiguity when calling an extension method that takes an <xref:System.Collections.Generic.IEnumerable%601>.</span></span> <span data-ttu-id="4f94e-106">Jeśli wywołasz taką metodę rozszerzenia na <xref:System.Text.RegularExpressions.GroupCollection> wystąpieniu, na przykład, zobaczysz <xref:System.Linq.Enumerable.Count%2A?displayProperty=nameWithType> następujący błąd kompilatora:</span><span class="sxs-lookup"><span data-stu-id="4f94e-106">If you call such an extension method on a <xref:System.Text.RegularExpressions.GroupCollection> instance, for example, <xref:System.Linq.Enumerable.Count%2A?displayProperty=nameWithType>, you'll see the following compiler error:</span></span>

<span data-ttu-id="4f94e-107">**CS1061: element "GroupCollection" nie zawiera definicji "Count" i nie można znaleźć dostępnej metody rozszerzającej "Count" akceptującej pierwszy argument typu "GroupCollection" (czy nie brakuje dyrektywy using lub odwołania do zestawu?)**</span><span class="sxs-lookup"><span data-stu-id="4f94e-107">**CS1061: 'GroupCollection' does not contain a definition for 'Count' and no accessible extension method 'Count' accepting a first argument of type 'GroupCollection' could be found (are you missing a using directive or an assembly reference?)**</span></span>

<span data-ttu-id="4f94e-108">W poprzednich wersjach programu .NET nie istniała niejednoznaczność i brak błędów kompilatora.</span><span class="sxs-lookup"><span data-stu-id="4f94e-108">In previous versions of .NET, there was no ambiguity and no compiler error.</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="4f94e-109">Wprowadzona wersja</span><span class="sxs-lookup"><span data-stu-id="4f94e-109">Version introduced</span></span>

<span data-ttu-id="4f94e-110">3.0</span><span class="sxs-lookup"><span data-stu-id="4f94e-110">3.0</span></span>

#### <a name="reason-for-change"></a><span data-ttu-id="4f94e-111">Przyczyna zmiany</span><span class="sxs-lookup"><span data-stu-id="4f94e-111">Reason for change</span></span>

<span data-ttu-id="4f94e-112">To była [niezamierzona zmiana](https://github.com/dotnet/corefx/pull/30077).</span><span class="sxs-lookup"><span data-stu-id="4f94e-112">This was an [unintentional breaking change](https://github.com/dotnet/corefx/pull/30077).</span></span> <span data-ttu-id="4f94e-113">Ponieważ takie dane były takie jak w pewnym czasie, nie planujemy jej przywrócenia.</span><span class="sxs-lookup"><span data-stu-id="4f94e-113">Because it has been like this for some time, we don't plan to revert it.</span></span> <span data-ttu-id="4f94e-114">Ponadto takie zmiany byłyby przerywane.</span><span class="sxs-lookup"><span data-stu-id="4f94e-114">In addition, such a change would itself be breaking.</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="4f94e-115">Zalecana akcja</span><span class="sxs-lookup"><span data-stu-id="4f94e-115">Recommended action</span></span>

<span data-ttu-id="4f94e-116">W przypadku <xref:System.Text.RegularExpressions.GroupCollection> wystąpień należy rozróżnić wywołania metod rozszerzających, które akceptują `IEnumerable<T>` z rzutowaniem.</span><span class="sxs-lookup"><span data-stu-id="4f94e-116">For <xref:System.Text.RegularExpressions.GroupCollection> instances, disambiguate calls to extension methods that accept an `IEnumerable<T>` with a cast.</span></span>

```csharp
// Without a cast - causes CS1061.
match.Groups.Count(_ => true)

// With a disambiguating cast.
((IEnumerable<Group>)m.Groups).Count(_ => true);
```

#### <a name="category"></a><span data-ttu-id="4f94e-117">Kategoria</span><span class="sxs-lookup"><span data-stu-id="4f94e-117">Category</span></span>

<span data-ttu-id="4f94e-118">Podstawowe biblioteki platformy .NET</span><span class="sxs-lookup"><span data-stu-id="4f94e-118">Core .NET libraries</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="4f94e-119">Dotyczy interfejsów API</span><span class="sxs-lookup"><span data-stu-id="4f94e-119">Affected APIs</span></span>

<span data-ttu-id="4f94e-120">Ma to dotyczyć każda metoda rozszerzająca, która akceptuje <xref:System.Collections.Generic.IEnumerable%601> .</span><span class="sxs-lookup"><span data-stu-id="4f94e-120">Any extension method that accepts an <xref:System.Collections.Generic.IEnumerable%601> is affected.</span></span> <span data-ttu-id="4f94e-121">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="4f94e-121">For example:</span></span>

- <xref:System.Collections.Immutable.ImmutableArray.ToImmutableArray%60%601(System.Collections.Generic.IEnumerable{%60%600})?displayProperty=fullName>
- <xref:System.Collections.Immutable.ImmutableDictionary.ToImmutableDictionary%2A?displayProperty=fullName>
- <xref:System.Collections.Immutable.ImmutableHashSet.ToImmutableHashSet%2A?displayProperty=fullName>
- <xref:System.Collections.Immutable.ImmutableList.ToImmutableList%60%601(System.Collections.Generic.IEnumerable{%60%600})?displayProperty=fullName>
- <xref:System.Collections.Immutable.ImmutableSortedDictionary.ToImmutableSortedDictionary%2A?displayProperty=fullName>
- <xref:System.Collections.Immutable.ImmutableSortedSet.ToImmutableSortedSet%2A?displayProperty=fullName>
- <xref:System.Data.DataTableExtensions.CopyToDataTable%2A?displayProperty=fullName>
- <span data-ttu-id="4f94e-122">Większość `System.Linq.Enumerable` metod, na przykład <xref:System.Linq.Enumerable.Count%2A?displayProperty=fullName></span><span class="sxs-lookup"><span data-stu-id="4f94e-122">Most of the `System.Linq.Enumerable` methods, for example, <xref:System.Linq.Enumerable.Count%2A?displayProperty=fullName></span></span>
- <xref:System.Linq.ParallelEnumerable.AsParallel%2A?displayProperty=fullName>
- <xref:System.Linq.Queryable.AsQueryable%2A?displayProperty=fullName>

<!--

#### Affected APIs

- ``M:System.Collections.Immutable.ImmutableArray.ToImmutableArray``1(System.Collections.Generic.IEnumerable{``0})``
- `Overload:System.Collections.Immutable.ImmutableDictionary.ToImmutableDictionary`
- `Overload:System.Collections.Immutable.ImmutableHashSet.ToImmutableHashSet`
- ``M:System.Collections.Immutable.ImmutableList.ToImmutableList``1(System.Collections.Generic.IEnumerable{``0})``
- `Overload:System.Collections.Immutable.ImmutableSortedDictionary.ToImmutableSortedDictionary`
- `Overload:System.Collections.Immutable.ImmutableSortedSet.ToImmutableSortedSet`
- `Overload:System.Data.DataTableExtensions.CopyToDataTable`
- `Overload:System.Linq.Enumerable.Count`
- `Overload:System.Linq.ParallelEnumerable.AsParallel`
- `Overload:System.Linq.Queryable.AsQueryable`

-->
