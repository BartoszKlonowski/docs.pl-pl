---
title: Tablice
description: 'Dowiedz się, jak tworzyć i używać tablic w języku programowania F #.'
ms.date: 08/13/2020
ms.openlocfilehash: 96b0d7eaf10d5afcd9a647681d5c2ef2d2fba335
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96739754"
---
# <a name="arrays"></a>Tablice

Tablice są stałymi, niemodyfikowalnymi kolekcjami kolejnych elementów danych, które są tego samego typu.

## <a name="create-arrays"></a>Tworzenie tablic

Tablice można tworzyć na kilka sposobów. Możesz utworzyć małą tablicę, określając kolejne wartości między `[|` i `|]` i rozdzielone średnikami, jak pokazano w poniższych przykładach.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet1.fs)]

Można również umieścić każdy element w osobnym wierszu, w którym przypadku separator średników jest opcjonalny.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet2.fs)]

Typ elementów tablicy jest wywnioskowany na podstawie używanych literałów i musi być spójny. Poniższy kod powoduje błąd, ponieważ 1,0 jest zmiennoprzecinkowa i 2 i 3 są liczbami całkowitymi.

```fsharp
// Causes an error.
// let array2 = [| 1.0; 2; 3 |]
```

Można również użyć wyrażeń sekwencji do tworzenia tablic. Poniżej znajduje się przykład, który tworzy tablicę kwadratów liczb całkowitych z zakresu od 1 do 10.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet3.fs)]

Aby utworzyć tablicę, w której wszystkie elementy są zainicjowane do zera, użyj `Array.zeroCreate` .

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet4.fs)]

## <a name="access-elements"></a>Elementy dostępu

Możesz uzyskać dostęp do elementów tablicy przy użyciu operatora kropki ( `.` ) i nawiasów kwadratowych ( `[` i `]` ).

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet5.fs)]

Indeksy tablicy zaczynają się od 0.

Możesz również uzyskać dostęp do elementów tablicy przy użyciu notacji wycinka, która umożliwia określenie podzakresu tablicy. Przykłady zapisu wycinka są następujące.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet51.fs)]

Gdy jest używana notacja wycinka, tworzona jest nowa kopia tablicy.

## <a name="array-types-and-modules"></a>Typy tablic i moduły

Typ wszystkich tablic F # to typ .NET Framework <xref:System.Array?displayProperty=nameWithType> . W związku z tym tablice języka F # obsługują wszystkie funkcje dostępne w programie <xref:System.Array?displayProperty=nameWithType> .

[ `Array` Moduł](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html) obsługuje operacje w tablicach jednowymiarowych. Moduły `Array2D` , `Array3D` i `Array4D` zawierają funkcje, które obsługują operacje na tablicach odpowiednio dwa, trzy i cztery wymiary. Można utworzyć tablice rangi większe niż cztery przy użyciu <xref:System.Array?displayProperty=nameWithType> .

### <a name="simple-functions"></a>Proste funkcje

[`Array.get`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#get) Pobiera element. [`Array.length`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#length) podaje długość tablicy. [`Array.set`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#set) Ustawia element na określoną wartość. Poniższy przykład kodu ilustruje sposób korzystania z tych funkcji.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet9.fs)]

Dane wyjściowe są następujące:

```console
0 1 2 3 4 5 6 7 8 9
```

### <a name="functions-that-create-arrays"></a>Funkcje tworzące tablice

Kilka funkcji tworzy tablice bez konieczności stosowania istniejącej tablicy. [`Array.empty`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#empty) tworzy nową tablicę, która nie zawiera żadnych elementów. [`Array.create`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#create) Tworzy tablicę o określonym rozmiarze i ustawia wszystkie elementy na dostarczone wartości. [`Array.init`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#init) Tworzy tablicę z uwzględnieniem wymiaru i funkcji w celu wygenerowania elementów. [`Array.zeroCreate`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#zeroCreate) Tworzy tablicę, w której wszystkie elementy są inicjowane jako wartość zerowa dla typu tablicy. Poniższy kod ilustruje te funkcje.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet91.fs)]

Dane wyjściowe są następujące:

```console
Length of empty array: 0
Area of floats set to 5.0: [|5.0; 5.0; 5.0; 5.0; 5.0; 5.0; 5.0; 5.0; 5.0; 5.0|]
Array of squares: [|0; 1; 4; 9; 16; 25; 36; 49; 64; 81|]
```

[`Array.copy`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#copy) tworzy nową tablicę zawierającą elementy, które są kopiowane z istniejącej tablicy. Należy pamiętać, że kopia jest kopią skróconą, co oznacza, że jeśli typem elementu jest typ referencyjny, kopiowane jest tylko odwołanie, a nie obiekt źródłowy. Pokazano to w poniższym przykładzie kodu.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet11.fs)]

Dane wyjściowe powyższego kodu są następujące:

```console
[|Test1; Test2; |]
[|; Test2; |]
```

Ciąg `Test1` pojawia się tylko w pierwszej tablicy, ponieważ operacja tworzenia nowego elementu zastępuje odwołanie w, `firstArray` ale nie wpływa na pierwotne odwołanie do pustego ciągu, który nadal występuje w `secondArray` . Ciąg `Test2` pojawia się w obu tablicach `Insert` , ponieważ operacja na <xref:System.Text.StringBuilder?displayProperty=nameWithType> typie ma wpływ na <xref:System.Text.StringBuilder?displayProperty=nameWithType> obiekt źródłowy, do którego odwołuje się obie tablice.

[`Array.sub`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#sub) generuje nową tablicę z podzakresu tablicy. Należy określić Podzakres, podając początkowy indeks i długość. Poniższy kod ilustruje użycie `Array.sub` .

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet12.fs)]

Dane wyjściowe pokazują, że podtablica zaczyna się od elementu 5 i zawiera 10 elementów.

```console
[|5; 6; 7; 8; 9; 10; 11; 12; 13; 14|]
```

[`Array.append`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#append) tworzy nową tablicę przez połączenie dwóch istniejących tablic.

Poniższy kod ilustruje **tablicę Array. Append**.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet13.fs)]

Dane wyjściowe powyższego kodu są następujące.

```console
[|1; 2; 3; 4; 5; 6|]
```

[`Array.choose`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#choose) wybiera elementy tablicy do uwzględnienia w nowej tablicy. Poniższy kod ilustruje `Array.choose` . Należy zauważyć, że typ elementu tablicy nie musi być zgodny z typem wartości zwracanej w typie opcji. W tym przykładzie typ elementu to `int` i opcja jest wynikiem funkcji wielomianu, `elem*elem - 1` jako liczby zmiennoprzecinkowej.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet14.fs)]

Dane wyjściowe powyższego kodu są następujące.

```console
[|3.0; 15.0; 35.0; 63.0; 99.0|]
```

[`Array.collect`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#collect) uruchamia określoną funkcję dla każdego elementu tablicy istniejącej tablicy, a następnie zbiera elementy wygenerowane przez funkcję i łączy je w nową tablicę. Poniższy kod ilustruje `Array.collect` .

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet15.fs)]

Dane wyjściowe powyższego kodu są następujące.

```console
[|0; 1; 0; 1; 2; 3; 4; 5; 0; 1; 2; 3; 4; 5; 6; 7; 8; 9; 10|]
```

[`Array.concat`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#concat) wykonuje sekwencję tablic i łączy je w jedną tablicę. Poniższy kod ilustruje `Array.concat` .

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet16.fs)]

Dane wyjściowe powyższego kodu są następujące.

```console
[|(1, 1, 1); (1, 2, 2); (1, 3, 3); (2, 1, 2); (2, 2, 4); (2, 3, 6); (3, 1, 3);
(3, 2, 6); (3, 3, 9)|]
```

[`Array.filter`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#filter) przyjmuje funkcję warunku logicznego i generuje nową tablicę zawierającą tylko te elementy z tablicy wejściowej, dla których warunek ma wartość true. Poniższy kod ilustruje `Array.filter` .

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet17.fs)]

Dane wyjściowe powyższego kodu są następujące.

```console
[|2; 4; 6; 8; 10|]
```

[`Array.rev`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#rev) generuje nową tablicę przez odwracanie kolejności istniejącej tablicy. Poniższy kod ilustruje `Array.rev` .

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet18.fs)]

Dane wyjściowe powyższego kodu są następujące.

```console
"Hello world!"
```

Można łatwo połączyć funkcje w module Array, które przekształcają tablice za pomocą operatora potoku ( `|>` ), jak pokazano w poniższym przykładzie.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet19.fs)]

Dane wyjściowe to

```console
[|100; 36; 16; 4|]
```

### <a name="multidimensional-arrays"></a>Tablice wielowymiarowe

Można utworzyć tablicę wielowymiarową, ale nie ma składni do pisania wielowymiarowego literału tablicy. Użyj operatora, [`array2D`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-array2dmodule.html) Aby utworzyć tablicę z sekwencji sekwencji elementów tablicy. Sekwencje mogą być literałami tablicowymi lub listami. Na przykład poniższy kod tworzy tablicę dwuwymiarową.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet20.fs)]

Można również użyć funkcji, [`Array2D.init`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-array2dmodule.html#init) Aby zainicjować tablice dwóch wymiarów, a podobne funkcje są dostępne dla tablic trzech i czterech wymiarów. Funkcje te przyjmują funkcję, która jest używana do tworzenia elementów. Aby utworzyć dwuwymiarową tablicę, która zawiera elementy ustawione na wartość początkową zamiast określania funkcji, należy użyć [`Array2D.create`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-array2dmodule.html#create) funkcji, która jest również dostępna dla tablic do czterech wymiarów. Poniższy przykład kodu najpierw pokazuje, jak utworzyć tablicę tablic zawierających wymagane elementy, a następnie użyć `Array2D.init` do wygenerowania odpowiedniej tablicy dwuwymiarowej.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet21.fs)]

Składnia indeksowania tablicy i skalowanie wycinków jest obsługiwana w przypadku tablic o wartości do rangi 4. Po określeniu indeksu w wielu wymiarach, należy użyć przecinków do oddzielenia indeksów, jak pokazano w poniższym przykładzie kodu.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet22.fs)]

Typ tablicy dwuwymiarowej jest zapisywana jako `<type>[,]` (na przykład `int[,]` , `double[,]` ), a typ trójwymiarowej tablicy jest zapisywana jako `<type>[,,]` itd. dla tablic o wyższych wymiarach.

Tylko podzestaw funkcji dostępnych dla tablic jednowymiarowych jest również dostępny dla tablic wielowymiarowych.

### <a name="array-slicing-and-multidimensional-arrays"></a>Dzielenie tablic i tablice wielowymiarowe

W tablicy dwuwymiarowej (macierzy) można wyodrębnić tablicę podrzędną, określając zakresy i używając znaku wieloznacznego ( `*` ) w celu określenia całych wierszy lub kolumn.

```fsharp
// Get rows 1 to N from an NxM matrix (returns a matrix):
matrix.[1.., *]

// Get rows 1 to 3 from a matrix (returns a matrix):
matrix.[1..3, *]

// Get columns 1 to 3 from a matrix (returns a matrix):
matrix.[*, 1..3]

// Get a 3x3 submatrix:
matrix.[1..3, 1..3]
```

Można rozłożyć tablicę wielowymiarową na podtablice tego samego lub niższego wymiaru. Na przykład można uzyskać wektor z macierzy, określając pojedynczy wiersz lub kolumnę.

```fsharp
// Get row 3 from a matrix as a vector:
matrix.[3, *]

// Get column 3 from a matrix as a vector:
matrix.[*, 3]
```

Można użyć tej składni wycinków dla typów, które implementują operatory dostępu do elementów i przeciążone `GetSlice` metody. Na przykład poniższy kod tworzy typ macierzy, która otacza tablicę 2D języka F #, implementuje właściwość elementu w celu zapewnienia obsługi indeksowania tablicy i implementuje trzy wersje programu `GetSlice` . Jeśli możesz użyć tego kodu jako szablonu dla typów macierzy, możesz użyć wszystkich operacji tworzenia wycinków, które opisano w tej sekcji.

```fsharp
type Matrix<'T>(N: int, M: int) =
    let internalArray = Array2D.zeroCreate<'T> N M

    member this.Item
        with get(a: int, b: int) = internalArray.[a, b]
        and set(a: int, b: int) (value:'T) = internalArray.[a, b] <- value

    member this.GetSlice(rowStart: int option, rowFinish : int option, colStart: int option, colFinish : int option) =
        let rowStart =
            match rowStart with
            | Some(v) -> v
            | None -> 0
        let rowFinish =
            match rowFinish with
            | Some(v) -> v
            | None -> internalArray.GetLength(0) - 1
        let colStart =
            match colStart with
            | Some(v) -> v
            | None -> 0
        let colFinish =
            match colFinish with
            | Some(v) -> v
            | None -> internalArray.GetLength(1) - 1
        internalArray.[rowStart..rowFinish, colStart..colFinish]

    member this.GetSlice(row: int, colStart: int option, colFinish: int option) =
        let colStart =
            match colStart with
            | Some(v) -> v
            | None -> 0
        let colFinish =
            match colFinish with
            | Some(v) -> v
            | None -> internalArray.GetLength(1) - 1
        internalArray.[row, colStart..colFinish]

    member this.GetSlice(rowStart: int option, rowFinish: int option, col: int) =
        let rowStart =
            match rowStart with
            | Some(v) -> v
            | None -> 0
        let rowFinish =
            match rowFinish with
            | Some(v) -> v
            | None -> internalArray.GetLength(0) - 1
        internalArray.[rowStart..rowFinish, col]

module test =
    let generateTestMatrix x y =
        let matrix = new Matrix<float>(3, 3)
        for i in 0..2 do
            for j in 0..2 do
                matrix.[i, j] <- float(i) * x - float(j) * y
        matrix

    let test1 = generateTestMatrix 2.3 1.1
    let submatrix = test1.[0..1, 0..1]
    printfn $"{submatrix}"

    let firstRow = test1.[0,*]
    let secondRow = test1.[1,*]
    let firstCol = test1.[*,0]
    printfn $"{firstCol}"
```

### <a name="boolean-functions-on-arrays"></a>Funkcje logiczne w tablicach

Elementy Functions [`Array.exists`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#exists) i [`Array.exists2`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#exists2) test są odpowiednio w jednej lub dwóch tablicach. Te funkcje przyjmują funkcję testową i zwracają, `true` Jeśli istnieje element (lub para elementów dla `Array.exists2` ), który spełnia warunek.

Poniższy kod ilustruje użycie `Array.exists` i `Array.exists2` . W tych przykładach nowe funkcje są tworzone przez zastosowanie tylko jednego z argumentów, w takich przypadkach, argumentu funkcji.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet23.fs)]

Dane wyjściowe powyższego kodu są następujące.

```console
true
false
false
true
```

Podobnie funkcja [`Array.forall`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#forall) testuje tablicę, aby określić, czy każdy element spełnia warunek logiczny. Odmiana [`Array.forall2`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#forall2) wykonuje tę samą czynność przy użyciu funkcji logicznej, która obejmuje elementy dwóch tablic o równej długości. Poniższy kod ilustruje sposób korzystania z tych funkcji.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet24.fs)]

Dane wyjściowe dla tych przykładów są następujące.

```console
false
true
true
false
```

### <a name="search-arrays"></a>Wyszukaj tablice

[`Array.find`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#find) przyjmuje funkcję logiczną i zwraca pierwszy element, dla którego funkcja zwraca `true` , lub wywołuje <xref:System.Collections.Generic.KeyNotFoundException?displayProperty=nameWithType> Jeśli nie zostanie znaleziony żaden element, który spełnia warunek. [`Array.findIndex`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#findIndex) jest podobne `Array.find` , z tą różnicą, że zwraca indeks elementu zamiast samego elementu.

Poniższy kod używa `Array.find` i, `Array.findIndex` Aby zlokalizować liczbę, która jest idealnym kwadratem i idealnym modułem.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet25.fs)]

Dane wyjściowe są następujące:

```console
The first element that is both a square and a cube is 64 and its index is 62.
```

[`Array.tryFind`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#tryFind) jest podobne `Array.find` , z tą różnicą, że jej wynik jest typem opcji i zwraca, `None` Jeśli nie znaleziono żadnego elementu. `Array.tryFind` powinien być używany zamiast `Array.find` gdy nie wiadomo, czy pasujący element znajduje się w tablicy. Podobnie, [`Array.tryFindIndex`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#tryFindIndex) jest taka, jak `Array.findIndex` z tą różnicą, że typ opcji jest wartością zwracaną. Jeśli nie zostanie znaleziony żaden element, opcja jest `None` .

Poniższy kod ilustruje użycie `Array.tryFind` . Ten kod zależy od poprzedniego kodu.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet26.fs)]

Dane wyjściowe są następujące:

```console
Found an element: 1
Found an element: 729
Failed to find a matching element.
```

Użyj, [`Array.tryPick`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#tryPick) gdy chcesz przekształcić element, a także go znaleźć. Wynikiem jest pierwszy element, dla którego funkcja zwraca przekształcony element jako wartość opcji lub `None` Jeśli nie można znaleźć takiego elementu.

Poniższy kod ilustruje użycie `Array.tryPick` . W tym przypadku zamiast wyrażenia lambda, kilka lokalnych funkcji pomocniczych jest zdefiniowanych do uproszczenia kodu.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet27.fs)]

Dane wyjściowe są następujące:

```console
Found an element 1 with square root 1 and cube root 1.
Found an element 64 with square root 8 and cube root 4.
Found an element 729 with square root 27 and cube root 9.
Found an element 4096 with square root 64 and cube root 16.
Did not find an element that is both a perfect square and a perfect cube.
```

### <a name="perform-computations-on-arrays"></a>Wykonywanie obliczeń w tablicach

[`Array.average`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#average)Funkcja zwraca średnią każdego elementu w tablicy. Jest ono ograniczone do typów elementów, które obsługują dokładne dzielenie przez liczbę całkowitą, która obejmuje typy zmiennoprzecinkowe, ale nie typy całkowite. [`Array.averageBy`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#averageBy)Funkcja zwraca średnią wyników wywołania funkcji dla każdego elementu. W przypadku tablicy typu całkowitego można użyć `Array.averageBy` funkcji i przekonwertować każdy element na typ zmiennoprzecinkowy obliczenia.

Użyj [`Array.max`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#max) lub, [`Array.min`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#min) Aby uzyskać maksimum lub minimum elementu, jeśli jest obsługiwany przez typ elementu. Podobnie [`Array.maxBy`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#maxBy) i [`Array.minBy`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#minBy) Zezwalaj na wykonywanie funkcji jako pierwszej, na przykład w celu przekształcenia do typu, który obsługuje porównanie.

[`Array.sum`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#sum) dodaje elementy tablicy i [`Array.sumBy`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#sumBy) wywołuje funkcję dla każdego elementu i dodaje wyniki ze sobą.

Aby wykonać funkcję dla każdego elementu w tablicy bez przechowywania wartości zwracanych, użyj [`Array.iter`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#iter) . Dla funkcji obejmującej dwie tablice o równej długości Użyj [`Array.iter2`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#iter2) . Jeśli trzeba również zachować tablicę wyników funkcji, użyj [`Array.map`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#map) lub [`Array.map2`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#map2) , która działa w dwóch tablicach w danym momencie.

Różnice [`Array.iteri`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#iteri) i [`Array.iteri2`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#iteri2) zezwalają na indeks elementu, który ma być uwzględniony w obliczeniach; taka sama wartość dotyczy [`Array.mapi`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#mapi) i [`Array.mapi2`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#mapi2) .

[`Array.fold`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#fold)Algorytmy Functions,,,, [`Array.foldBack`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#foldBack) [`Array.reduce`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#reduce) [`Array.reduceBack`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#reduceBack) [`Array.scan`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#scan) i Execute, [`Array.scanBack`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#scanBack) które obejmują wszystkie elementy tablicy. Podobnie, różnice [`Array.fold2`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#fold2) i [`Array.foldBack2`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#foldBack2) wykonywanie obliczeń na dwóch tablicach.

Te funkcje do wykonywania obliczeń odpowiadają funkcjom o tej samej nazwie w [module list](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-listmodule.html). Aby zapoznać się z przykładami użycia, zobacz [listy](lists.md).

### <a name="modify-arrays"></a>Modyfikuj tablice

[`Array.set`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#set) Ustawia element na określoną wartość. [`Array.fill`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#fill) ustawia zakres elementów w tablicy do określonej wartości. Poniższy kod zawiera przykład `Array.fill` .

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet28.fs)]

Dane wyjściowe są następujące:

```console
[|1; 2; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 23; 24; 25|]
```

Można użyć, [`Array.blit`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#blit) Aby skopiować podsekcję jednej tablicy do innej tablicy.

### <a name="convert-to-and-from-other-types"></a>Konwertuj na i z innych typów

[`Array.ofList`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#ofList) Tworzy tablicę z listy. [`Array.ofSeq`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#ofSeq) Tworzy tablicę z sekwencji. [`Array.toList`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#toList) i [`Array.toSeq`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#toSeq) Konwertuj na inne typy kolekcji z typu tablicy.

### <a name="sort-arrays"></a>Sortuj tablice

Użyj, [`Array.sort`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#sort) Aby posortować tablicę przy użyciu funkcji porównania generycznej. Użyj, [`Array.sortBy`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#sortBy) Aby określić funkcję, która generuje wartość, która jest określana jako *klucz*, aby sortować przy użyciu funkcji porównywania generycznego w kluczu. Użyj, [`Array.sortWith`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#sortWith) Jeśli chcesz podać niestandardową funkcję porównania. `Array.sort`, `Array.sortBy` i `Array.sortWith` wszystkie zwracają posortowaną tablicę jako nową tablicę. Zmiany [`Array.sortInPlace`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#sortInPlace) , [`Array.sortInPlaceBy`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#sortInPlaceBy) i [`Array.sortInPlaceWith`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#sortInPlaceWith) modyfikują istniejącą tablicę zamiast zwracać nowe.

### <a name="arrays-and-tuples"></a>Tablice i krotki

Funkcje [`Array.zip`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#zip) i [`Array.unzip`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#unzip) konwertują tablice par krotek na krotki tablic i na odwrót. [`Array.zip3`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#zip3) i [`Array.unzip3`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#unzip3) są podobne, z tą różnicą, że współpracują z krotkami trzech elementów lub krotekmi trzech tablic.

## <a name="parallel-computations-on-arrays"></a>Obliczenia równoległe w tablicach

Moduł [`Array.Parallel`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule-parallel.html) zawiera funkcje do wykonywania obliczeń równoległych w tablicach. Ten moduł nie jest dostępny w aplikacjach przeznaczonych dla wersji .NET Framework wcześniejszych niż wersja 4.

## <a name="see-also"></a>Zobacz także

- [Dokumentacja języka F #](index.md)
- [Typy F#](fsharp-types.md)
