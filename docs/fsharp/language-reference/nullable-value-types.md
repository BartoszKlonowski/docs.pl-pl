---
title: Typy wartości dopuszczające wartość null
description: 'Dowiedz się, jak używać typów wartości null, aby reprezentować typ wartości, który może być również wartością null w języku F #.'
ms.date: 11/19/2020
ms.openlocfilehash: da0cd85bd651db81ba98c02a9db31d92dc52a8c6
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740407"
---
# <a name="nullable-value-types"></a>Typy wartości dopuszczające wartość null

_Typ wartości null_ `Nullable<'T>` reprezentuje dowolny typ [struktury](structures.md) , który może być również `null` . Jest to przydatne podczas pracy z bibliotekami i składnikami, które mogą reprezentować te rodzaje typów, takich jak liczby całkowite, z `null` wartością ze względów wydajnościowych. Typ podstawowy, który wykonuje kopię zapasową tej konstrukcji <xref:System.Nullable%601?displayProperty=nameWithType> .

## <a name="syntax"></a>Składnia

```fsharp
Nullable<'T>
Nullable value
```

## <a name="declare-and-assign-with-values"></a>Zadeklaruj i przypisz z wartościami

Deklarowanie typu wartości null jest równie podobne jak zadeklarowanie dowolnego typu otoki w języku F #:

```fsharp
open System

let x = 12
let nullableX = Nullable<int> x
```

Możesz również Elide parametr typu ogólnego i zezwolić na wnioskowanie o typie, aby rozwiązać ten problem:

```fsharp
open System

let x = 12
let nullableX = Nullable x
```

Aby przypisać do typu wartości null, należy również być jawnym. Nie istnieje niejawna konwersja dla typów wartości null zdefiniowanych w języku F #:

```fsharp
open System

let mutable x = Nullable 12
x <- Nullable 13
```

## <a name="assign-null"></a>Przypisz wartość null

Nie można bezpośrednio przypisać `null` do typu wartości null. Użyj `Nullable()` zamiast tego:

```fsharp
let mutable a = Nullable 42
a <- Nullable()
```

Jest to spowodowane tym `Nullable<'T>` , że program nie ma `null` prawidłowej wartości.

## <a name="pass-and-assign-to-members"></a>Przekaż i przypisz do członków

Kluczowa różnica między pracą z elementami członkowskimi i F # polega na tym, że typy wartości null mogą być niejawnie wywnioskowane podczas pracy z członkami. Rozważmy metodę folling, która przyjmuje typ wartości null jako dane wejściowe:

```fsharp
type C() =
    member _.M(x: Nullable<int>) = x.HasValue
    member val NVT = Nullable 12 with get, set

let c = C()
c.M(12)
c.NVT <- 12
```

W poprzednim przykładzie można przekazać `12` do metody `M` . Można również przypisać `12` do właściwości `NVT` Auto. Kompilator F # niejawnie konwertuje wywołanie lub przypisanie podobne do tego, gdy typ docelowy jest zgodny z danymi wejściowymi, jeśli dane wejściowe można utworzyć jako typ wartości nullabel.

## <a name="examine-a-nullable-value-type-instance"></a>Badanie wystąpienia typu wartości null

W przeciwieństwie do [opcji](options.md), które są uogólnioną konstrukcją dla reprezentowania możliwej wartości, typy wartości null nie są używane z dopasowywaniem do wzorca. Zamiast tego należy użyć [`if`](conditional-expressions-if-then-else.md) wyrażenia i sprawdzić `HasValue` Właściwość.

Aby uzyskać wartość bazową, należy użyć `Value` właściwości po `HasValue` sprawdzeniu, tak jak to zrobić:

```fsharp
open System

let a = Nullable 42

if a.HasValue then
    printfn $"{a} is {a.Value}"
else
    printfn $"{a} has no value."
```

## <a name="nullable-operators"></a>Operatory dopuszczające wartość null

Operacje na typach wartości null, takich jak arytmetyczne lub porównania, mogą wymagać użycia [operatorów dopuszczających wartości null](symbol-and-operator-reference/nullable-operators.md).

Można dokonać konwersji z jednego typu wartości null na inny przy użyciu operatorów konwersji z `FSharp.Linq` przestrzeni nazw:

```fsharp
open System
open FSharp.Linq

let nullableInt = Nullable 10
let nullableFloat = Nullable.float nullableInt
```

Można również użyć odpowiedniego operatora, który nie dopuszcza wartości null, do konwersji na typ pierwotny, co powoduje, że występuje wyjątek, jeśli nie ma wartości:

```fsharp
open System
open FSharp.Linq

let nullableInt = Nullable 10
let nullableFloat = Nullable.float nullableInt

printfn $"value is %f{float nullableFloat}"
```

Operatorów dopuszczających wartości null można także używać jako krótkich celów sprawdzania `HasValue` i `Value` :

```fsharp
open System
open FSharp.Linq

let nullableInt = Nullable 10
let nullableFloat = Nullable.float nullableInt

let isBigger = nullableFloat ?> 1.0
let isBiggerLongForm = nullableFloat.HasValue && nullableFloat.Value > 1.0
```

`?>`Porównanie sprawdza, czy po lewej stronie nie dopuszcza wartości null i tylko wtedy, gdy ma wartość. Jest to równoznaczne z wierszem, który następuje po nim.

## <a name="see-also"></a>Zobacz także

- [Struktury](structures.md)
- [Opcje języka F #](options.md)
