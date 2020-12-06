---
title: Operatory dopuszczające wartość null
description: 'Dowiedz się więcej na temat operatorów dopuszczających wartości null, które są dostępne w języku programowania F #.'
ms.date: 05/16/2016
ms.openlocfilehash: 9ac6afc2c3f4277ee6e93b1ccb3d21f892926b4b
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740370"
---
# <a name="nullable-operators"></a>Operatory dopuszczające wartość null

Operatory dopuszczające wartość null to binarne operatory arytmetyczne lub porównania, które działają w przypadku typów arytmetycznych dopuszczających wartość null na jednej lub obu stronach. Typy dopuszczające wartość null powstają często podczas pracy z danymi ze źródeł, takich jak bazy danych, które zezwalają na wartości null w miejscu rzeczywistym. Operatory dopuszczające wartość null są często używane w wyrażeniach zapytań. Oprócz operatorów do dopuszczania wartości null dla operacji arytmetycznych i porównywania operatory konwersji mogą służyć do konwersji między typami dopuszczającymi wartość null. Istnieją także dopuszczające wartości null wersje niektórych operatorów zapytań.

## <a name="table-of-nullable-operators"></a>Tabela operatorów dopuszczających wartości null

W poniższej tabeli wymieniono operatory dopuszczające wartości null obsługiwane w języku F #.

|Dopuszczanie wartości null po lewej stronie|Dopuszczanie wartości null po prawej|Obie strony dopuszczają wartość null|
|---|---|---|
|[? >=](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-linq-nullableoperators.html#(%20?%3E=%20))|[>=?](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-linq-nullableoperators.html#(%20%3E=?%20))|[? >=?](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-linq-nullableoperators.html#(%20?%3E=?%20))|
|[? >](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-linq-nullableoperators.html#(%20?%3E%20))|[>?](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-linq-nullableoperators.html#(%20%3E?%20))|[? >?](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-linq-nullableoperators.html#(%20?%3E?%20))|
|[? <=](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-linq-nullableoperators.html#(%20?%3C=%20))|[<=?](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-linq-nullableoperators.html#(%20%3C=?%20))|[? <=?](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-linq-nullableoperators.html#(%20?%3C=?%20))|
|[? <](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-linq-nullableoperators.html#(%20?%3C%20))|[<?](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-linq-nullableoperators.html#(%20%3C?%20))|[? <?](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-linq-nullableoperators.html#(%20?%3C?%20))|
|[?=](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-linq-nullableoperators.html#(%20?=%20))|[=?](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-linq-nullableoperators.html#(%20=?%20))|[?=?](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-linq-nullableoperators.html#(%20?=?%20))|
|[? <>](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-linq-nullableoperators.html#(%20?%3C%3E%20))|[<>?](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-linq-nullableoperators.html#(%20%3C%3E?%20))|[? <>?](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-linq-nullableoperators.html#(%20?%3C%3E?%20))|
|[?+](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-linq-nullableoperators.html#(%20?+%20))|[+?](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-linq-nullableoperators.html#(%20+?%20))|[?+?](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-linq-nullableoperators.html#(%20?+?%20))|
|[?-](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-linq-nullableoperators.html#(%20?-%20))|[-?](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-linq-nullableoperators.html#(%20-?%20))|[?-?](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-linq-nullableoperators.html#(%20?-?%20))|
|[?*](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-linq-nullableoperators.html#(%20?*%20))|[*?](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-linq-nullableoperators.html#(%20*?%20))|[?*?](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-linq-nullableoperators.html#(%20?*?%20))|
|[?/](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-linq-nullableoperators.html#(%20?/%20))|[/?](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-linq-nullableoperators.html#(%20/?%20))|[?/?](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-linq-nullableoperators.html#(%20?/?%20))|
|[?%](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-linq-nullableoperators.html#(%20?%%20))|[%?](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-linq-nullableoperators.html#(%20%?%20))|[?%?](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-linq-nullableoperators.html#(%20?%?%20))|

## <a name="remarks"></a>Uwagi

Operatory dopuszczające wartość null są zawarte w module [NullableOperators](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-linq-nullableoperators.html) w przestrzeni nazw [FSharp. LINQ](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-linq.html). Typ dla danych dopuszczających wartości null to `System.Nullable<'T>` .

W wyrażeniach zapytań Typy dopuszczające wartości null powstają podczas wybierania danych ze źródła danych, które dopuszcza wartości null, a nie wartości. W bazie danych SQL Server każda kolumna danych w tabeli ma atrybut, który wskazuje, czy wartości null są dozwolone. Jeśli wartości null są dozwolone, dane zwrócone z bazy danych mogą zawierać wartości null, które nie mogą być reprezentowane przez pierwotny typ danych, taki jak `int` , `float` , i tak dalej. W związku z tym dane są zwracane jako `System.Nullable<int>` zamiast `int` , i `System.Nullable<float>` zamiast `float` . Rzeczywista wartość może być uzyskana z `System.Nullable<'T>` obiektu za pomocą `Value` właściwości i można określić, czy `System.Nullable<'T>` obiekt ma wartość przez wywołanie `HasValue` metody. Inną użyteczną metodą jest `System.Nullable<'T>.GetValueOrDefault` Metoda, która pozwala uzyskać wartość lub wartość domyślną odpowiedniego typu. Wartość domyślna to niektóre formy wartości "zero", takie jak 0, 0,0 lub `false` .

Typy dopuszczające wartość null mogą być konwertowane na typy pierwotne niedopuszczające wartości null przy użyciu zwykłych operatorów konwersji, takich jak `int` lub `float` . Istnieje również możliwość konwersji z jednego typu dopuszczającego wartość null na inny typ dopuszczający wartość null przy użyciu operatorów konwersji dla typów dopuszczających wartość null. Odpowiednie operatory konwersji mają taką samą nazwę jak standardowe, ale znajdują się w osobnym module, moduł [dopuszczający wartości null](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-linq-nullablemodule.html) w przestrzeni nazw [FSharp. LINQ](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-linq.html) . Zazwyczaj ta przestrzeń nazw jest otwierana podczas pracy z wyrażeniami zapytań. W takim przypadku można użyć operatorów konwersji dopuszczających wartość null poprzez dodanie prefiksu `Nullable.` do odpowiedniego operatora konwersji, jak pokazano w poniższym kodzie.

```fsharp
open Microsoft.FSharp.Linq

let nullableInt = new System.Nullable<int>(10)

// Use the Nullable.float conversion operator to convert from one nullable type to another nullable type.
let nullableFloat = Nullable.float nullableInt

// Use the regular non-nullable float operator to convert to a non-nullable float.
printfn $"%f{float nullableFloat}"
```

Wynik to `10.000000`.

Operatory zapytań dla pól danych dopuszczających wartość null, takie jak `sumByNullable` , również istnieją do użycia w wyrażeniach zapytań. Operatory zapytań dla typów niedopuszczających wartości null nie są zgodne z typami dopuszczających wartości null, dlatego należy użyć wersji dostosowanej do wartości null odpowiedniego operatora zapytania podczas pracy z wartościami danych dopuszczającymi wartość null. Aby uzyskać więcej informacji, zobacz [wyrażenia zapytań](../query-expressions.md).

W poniższym przykładzie pokazano użycie operatorów dopuszczających wartości null w wyrażeniu zapytania języka F #. Pierwsze zapytanie pokazuje, jak napisać zapytanie bez operatora dopuszczającego wartość null; drugie zapytanie pokazuje odpowiednik kwerendy, która używa operatora dopuszczającego wartość null. Pełny kontekst, w tym sposób konfigurowania bazy danych do użycia tego przykładowego kodu, znajduje się w [przewodniku: uzyskiwanie dostępu do SQL Database za pomocą dostawców typów](../../tutorials/type-providers/index.md).

```fsharp
open System
open System.Data
open System.Data.Linq
open Microsoft.FSharp.Data.TypeProviders
open Microsoft.FSharp.Linq

[<Generate>]
type dbSchema = SqlDataConnection<"Data Source=MYSERVER\INSTANCE;Initial Catalog=MyDatabase;Integrated Security=SSPI;">

let db = dbSchema.GetDataContext()

query {
    for row in db.Table2 do
    where (row.TestData1.HasValue && row.TestData1.Value > 2)
    select row
} |> Seq.iter (fun row -> printfn $"%d{row.TestData1.Value} %s{row.Name}")

query {
    for row in db.Table2 do
    // Use a nullable operator ?>
    where (row.TestData1 ?> 2)
    select row
} |> Seq.iter (fun row -> printfn "%d{row.TestData1.GetValueOrDefault()} %s{row.Name}")
```

## <a name="see-also"></a>Zobacz także

- [Dostawcy typów](../../tutorials/type-providers/index.md)
- [Wyrażenia kwerend](../query-expressions.md)
