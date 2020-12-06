---
title: Wycinki
description: 'Dowiedz się, jak używać wycinków dla istniejących typów danych F # i jak definiować własne wycinki dla innych typów danych.'
ms.date: 11/20/2020
ms.openlocfilehash: b776058df5a174dfe48dbf513bf17281036dd83e
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740383"
---
# <a name="slices"></a>Wycinki

W tym artykule wyjaśniono, jak korzystać z wycinków z istniejących typów języka F # i jak definiować własne wycinki.

W języku F # wycinek jest podzbiorem dowolnego typu danych.  Wycinki są podobne do [indeksatorów](./members/indexed-properties.md), ale zamiast zwracać jedną wartość z bazowej struktury danych, uzyskują wiele z nich. Wycinki używają `..` składni operatora do wybierania zakresu określonych indeksów w typie danych. Aby uzyskać więcej informacji, zobacz [artykuł odwołanie do wyrażenia zapętlenia](./loops-for-in-expression.md).

Język F # jest obecnie obsługiwany wewnętrznie w przypadku ciągów wycinków, list, tablic i wielowymiarowych (2D, 3W, 4D) tablic. Cięcie jest najczęściej używane z tablicami i listami języka F #. Można dodać wycięcie do niestandardowych typów danych przy użyciu `GetSlice` metody w definicji typu lub w [rozszerzeniu typu](type-extensions.md)w zakresie.

## <a name="slicing-f-lists-and-arrays"></a>Cięcie list i tablic języka F #

Najpopularniejsze typy danych, które są pofragmentowane, to listy i tablice języka F #.  Poniższy przykład ilustruje sposób wycinania list:

```fsharp
// Generate a list of 100 integers
let fullList = [ 1 .. 100 ]

// Create a slice from indices 1-5 (inclusive)
let smallSlice = fullList.[1..5]
printfn $"Small slice: {smallSlice}"

// Create a slice from the beginning to index 5 (inclusive)
let unboundedBeginning = fullList.[..5]
printfn $"Unbounded beginning slice: {unboundedBeginning}"

// Create a slice from an index to the end of the list
let unboundedEnd = fullList.[94..]
printfn $"Unbounded end slice: {unboundedEnd}"
```

Tablice odcięć są podobne do list wycinków:

```fsharp
// Generate an array of 100 integers
let fullArray = [| 1 .. 100 |]

// Create a slice from indices 1-5 (inclusive)
let smallSlice = fullArray.[1..5]
printfn $"Small slice: {smallSlice}"

// Create a slice from the beginning to index 5 (inclusive)
let unboundedBeginning = fullArray.[..5]
printfn $"Unbounded beginning slice: {unboundedBeginning}"

// Create a slice from an index to the end of the list
let unboundedEnd = fullArray.[94..]
printfn $"Unbounded end slice: {unboundedEnd}"
```

## <a name="slicing-multidimensional-arrays"></a>Dzielenie tablic wielowymiarowych

Język F # obsługuje tablice wielowymiarowe w podstawowej bibliotece języka F #. Podobnie jak w przypadku tablic jednowymiarowych, wycinki tablic wielowymiarowych mogą być również użyteczne. Jednak wprowadzenie dodatkowych wymiarów zezwala na nieznacznie inną składnię, dzięki czemu można przyjmować plasterki określonych wierszy i kolumn.

W poniższych przykładach pokazano, jak wydzielić tablicę 2D:

```fsharp
// Generate a 3x3 2D matrix
let A = array2D [[1;2;3];[4;5;6];[7;8;9]]
printfn $"Full matrix:\n {A}"

// Take the first row
let row0 = A.[0,*]
printfn $"{row0}"

// Take the first column
let col0 = A.[*,0]
printfn $"{col0}"

// Take all rows but only two columns
let subA = A.[*,0..1]
printfn $"{subA}"

// Take two rows and all columns
let subA' = A.[0..1,*]
printfn $"{subA}"

// Slice a 2x2 matrix out of the full 3x3 matrix
let twoByTwo = A.[0..1,0..1]
printfn $"{twoByTwo}"
```

## <a name="defining-slices-for-other-data-structures"></a>Definiowanie wycinków dla innych struktur danych

Biblioteka podstawowa F # definiuje wycinki dla ograniczonego zestawu typów. Jeśli chcesz zdefiniować wycinki dla większej liczby typów danych, możesz to zrobić w samej definicji typu lub w rozszerzeniu typu.

Na przykład poniżej przedstawiono sposób definiowania wycinków klasy umożliwiającej <xref:System.ArraySegment%601> wygodne manipulowanie danymi:

```fsharp
open System

type ArraySegment<'TItem> with
    member segment.GetSlice(start, finish) =
        let start = defaultArg start 0
        let finish = defaultArg finish segment.Count
        ArraySegment(segment.Array, segment.Offset + start, finish - start)

let arr = ArraySegment [| 1 .. 10 |]
let slice = arr.[2..5] //[ 3; 4; 5]
```

Inny przykład użycia <xref:System.Span%601> typów i <xref:System.ReadOnlySpan%601> :

```fsharp
open System

type ReadOnlySpan<'T> with
    member sp.GetSlice(startIdx, endIdx) =
        let s = defaultArg startIdx 0
        let e = defaultArg endIdx sp.Length
        sp.Slice(s, e - s)

type Span<'T> with
    member sp.GetSlice(startIdx, endIdx) =
        let s = defaultArg startIdx 0
        let e = defaultArg endIdx sp.Length
        sp.Slice(s, e - s)

let printSpan (sp: Span<int>) =
    let arr = sp.ToArray()
    printfn $"{arr}"

let sp = [| 1; 2; 3; 4; 5 |].AsSpan()
printSpan sp.[0..] // [|1; 2; 3; 4; 5|]
printSpan sp.[..5] // [|1; 2; 3; 4; 5|]
printSpan sp.[0..3] // [|1; 2; 3|]
printSpan sp.[1..3] // |2; 3|]
```

## <a name="built-in-f-slices-are-end-inclusive"></a>Wbudowane wycinki języka F # to wszystko końcowe

Wszystkie wycinki wewnętrzne w języku F # są końcowe włącznie; oznacza to, że górna granica jest uwzględniona w wycinku. Dla danego wycinka z indeksem początkowym `x` i końcowym indeksem `y` , powstający wycink będzie zawierać wartość *Yth* .

```fsharp
// Define a new list
let xs = [1 .. 10]

printfn $"{xs.[2..5]}" // Includes the 5th index
```

## <a name="built-in-f-empty-slices"></a>Wbudowane puste wycinki języka F #

Listy języka F #, tablice, sekwencje, ciągi, wielowymiarowe (2D, 3D, 4D) będą generować pusty plasterek, Jeśli składnia może utworzyć wycinek, który nie istnieje.

Rozpatrzmy następujący przykład:

```fsharp
let l = [ 1..10 ]
let a = [| 1..10 |]
let s = "hello!"

let emptyList = l.[-2..(-1)]
let emptyArray = a.[-2..(-1)]
let emptyString = s.[-2..(-1)]
```

> [!IMPORTANT]
> Deweloperzy języka C# mogą oczekiwać, że nie generują pustego wycinka. Jest to podjęcie decyzji dotyczącej projektu w przypadku, gdy puste kolekcje tworzą w języku F #. Pusta lista języka F # może być złożona z inną listą języka F #, pusty ciąg może zostać dodany do istniejącego ciągu i tak dalej. Może to być typowe dla wycinków na podstawie wartości przeprowadzonych jako parametry i odporności poza granice > przez wygenerowanie pustej kolekcji dopasowuje się do charakteru składowej kodu F #.

## <a name="fixed-index-slices-for-3d-and-4d-arrays"></a>Wycinków o stałym indeksie dla tablic 3W i 4D

W przypadku tablic języka F # 3D i 4D można poprawić określony indeks i wydzielić Inne wymiary przy użyciu tego indeksu.

Aby to zilustrować, weź pod uwagę następującą tablicę 3W:

*z = 0*

| x\y   | 0 | 1 |
|-------|---|---|
| **0** | 0 | 1 |
| **1** | 2 | 3 |

*z = 1*

| x\y   | 0 | 1 |
|-------|---|---|
| **0** | 4 | 5 |
| **1** | 6 | 7 |

Jeśli chcesz wyodrębnić wycinek `[| 4; 5 |]` z tablicy, użyj wycinka o stałym indeksie.

```fsharp
let dim = 2
let m = Array3D.zeroCreate<int> dim dim dim

let mutable count = 0

for z in 0..dim-1 do
    for y in 0..dim-1 do
        for x in 0..dim-1 do
            m.[x,y,z] <- count
            count <- count + 1

// Now let's get the [4;5] slice!
m.[*, 0, 1]
```

Ostatni wiersz naprawia `y` i `z` indeksuje tablicę 3W i pobiera resztę `x` wartości, które odpowiadają macierzy.

## <a name="see-also"></a>Zobacz także

- [Właściwości indeksowane](./members/indexed-properties.md)
