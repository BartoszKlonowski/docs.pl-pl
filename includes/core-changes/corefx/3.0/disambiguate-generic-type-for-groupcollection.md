---
ms.openlocfilehash: 97fab784acac4331894547eea27fc21b485597fb
ms.sourcegitcommit: fcbe432482464b1639decad78cc4dc8387c6269e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/12/2020
ms.locfileid: "97366878"
---
### <a name="passing-groupcollection-to-extension-methods-taking-ienumerablet-requires-disambiguation"></a>Przekazanie grupy GroupCollection do metod rozszerzających, które \<T> wymagają uściślania

Podczas wywoływania metody rozszerzenia, która przyjmuje obiekt `IEnumerable<T>` na <xref:System.Text.RegularExpressions.GroupCollection> , należy odróżnić typ za pomocą rzutowania.

#### <a name="change-description"></a>Zmień opis

Począwszy od platformy .NET Core 3,0, <xref:System.Text.RegularExpressions.GroupCollection?displayProperty=nameWithType> implementuje `IEnumerable<KeyValuePair<String,Group>>` oprócz innych typów, w tym `IEnumerable<Group>` . Powoduje to niejednoznaczność podczas wywoływania metody rozszerzenia, która przyjmuje <xref:System.Collections.Generic.IEnumerable%601> . Jeśli wywołasz taką metodę rozszerzenia na <xref:System.Text.RegularExpressions.GroupCollection> wystąpieniu, na przykład, zobaczysz <xref:System.Linq.Enumerable.Count%2A?displayProperty=nameWithType> następujący błąd kompilatora:

**CS1061: element "GroupCollection" nie zawiera definicji "Count" i nie można znaleźć dostępnej metody rozszerzającej "Count" akceptującej pierwszy argument typu "GroupCollection" (czy nie brakuje dyrektywy using lub odwołania do zestawu?)**

W poprzednich wersjach programu .NET nie istniała niejednoznaczność i brak błędów kompilatora.

#### <a name="version-introduced"></a>Wprowadzona wersja

3.0

#### <a name="reason-for-change"></a>Przyczyna zmiany

To była [niezamierzona zmiana](https://github.com/dotnet/corefx/pull/30077). Ponieważ takie dane były takie jak w pewnym czasie, nie planujemy jej przywrócenia. Ponadto takie zmiany byłyby przerywane.

#### <a name="recommended-action"></a>Zalecana akcja

W przypadku <xref:System.Text.RegularExpressions.GroupCollection> wystąpień należy rozróżnić wywołania metod rozszerzających, które akceptują `IEnumerable<T>` z rzutowaniem.

```csharp
// Without a cast - causes CS1061.
match.Groups.Count(_ => true)

// With a disambiguating cast.
((IEnumerable<Group>)m.Groups).Count(_ => true);
```

#### <a name="category"></a>Kategoria

Podstawowe biblioteki platformy .NET

#### <a name="affected-apis"></a>Dotyczy interfejsów API

Ma to dotyczyć każda metoda rozszerzająca, która akceptuje <xref:System.Collections.Generic.IEnumerable%601> . Na przykład:

- <xref:System.Collections.Immutable.ImmutableArray.ToImmutableArray%60%601(System.Collections.Generic.IEnumerable{%60%600})?displayProperty=fullName>
- <xref:System.Collections.Immutable.ImmutableDictionary.ToImmutableDictionary%2A?displayProperty=fullName>
- <xref:System.Collections.Immutable.ImmutableHashSet.ToImmutableHashSet%2A?displayProperty=fullName>
- <xref:System.Collections.Immutable.ImmutableList.ToImmutableList%60%601(System.Collections.Generic.IEnumerable{%60%600})?displayProperty=fullName>
- <xref:System.Collections.Immutable.ImmutableSortedDictionary.ToImmutableSortedDictionary%2A?displayProperty=fullName>
- <xref:System.Collections.Immutable.ImmutableSortedSet.ToImmutableSortedSet%2A?displayProperty=fullName>
- <xref:System.Data.DataTableExtensions.CopyToDataTable%2A?displayProperty=fullName>
- Większość `System.Linq.Enumerable` metod, na przykład <xref:System.Linq.Enumerable.Count%2A?displayProperty=fullName>
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
