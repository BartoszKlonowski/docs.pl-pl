---
title: Parametry i argumenty
description: 'Dowiedz się więcej o obsłudze języka F # dla definiowania parametrów i przekazywania argumentów do funkcji, metod i właściwości.'
ms.date: 08/15/2020
ms.openlocfilehash: 3c391ca37a1cf3bd150316943e5b06efa532b317
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740292"
---
# <a name="parameters-and-arguments"></a>Parametry i argumenty

W tym temacie opisano obsługę języków definiujących parametry i przekazywanie argumentów do funkcji, metod i właściwości. Zawiera informacje o sposobach przekazywania przez odwołanie oraz sposobie definiowania i używania metod, które mogą przyjmować zmienną liczbę argumentów.

## <a name="parameters-and-arguments"></a>Parametry i argumenty

*Parametr* Term służy do opisywania nazw dla wartości, które powinny być dostarczone. *Argument* Term jest używany dla wartości podanych dla każdego parametru.

Parametry można określić w postaci krotek lub rozwinięte lub w niektórych kombinacjach dwóch. Argumenty można przekazać za pomocą jawnej nazwy parametru. Parametry metod mogą być określone jako opcjonalne i mają określoną wartość domyślną.

## <a name="parameter-patterns"></a>Wzorce parametrów

Parametry dostarczone do funkcji i metod są ogólnie wzorce oddzielone spacjami. Oznacza to, że w zasadzie wszystkie wzorce opisane w [wyrażeniach dopasowania](match-expressions.md) mogą być używane na liście parametrów dla funkcji lub elementu członkowskiego.

Metody zwykle używają spójnej formy przekazywania argumentów. Pozwala to uzyskać wyraźniejszy wynik z perspektywy innych języków .NET, ponieważ formularz spójny pasuje do sposobu przekazywania argumentów w metodach .NET.

Formularz rozwinięte jest najczęściej używany z funkcjami utworzonymi przy użyciu `let` powiązań.

W poniższym pseudokodzie przedstawiono przykłady argumentów krotki i rozwinięte.

```fsharp
// Tuple form.
member this.SomeMethod(param1, param2) = ...
// Curried form.
let function1 param1 param2 = ...
```

Połączone formularze są możliwe, gdy niektóre argumenty są kolekcjami, a niektóre z nich nie są.

```fsharp
let function2 param1 (param2a, param2b) param3 = ...
```

Inne wzorce mogą być również używane na listach parametrów, ale jeśli wzorzec parametru nie jest zgodny ze wszystkimi możliwymi danymi wejściowymi, może wystąpić niekompletne dopasowanie w czasie wykonywania. Wyjątek `MatchFailureException` jest generowany, gdy wartość argumentu nie pasuje do wzorców określonych na liście parametrów. Kompilator generuje ostrzeżenie, gdy wzorzec parametru zezwala na niekompletne dopasowania. Co najmniej jeden inny wzorzec jest często przydatny dla list parametrów, który jest wzorcem wieloznacznym. Możesz użyć symbolu wieloznacznego na liście parametrów, gdy po prostu chcesz zignorować wszystkie dostarczone argumenty. Poniższy kod ilustruje użycie wzorca wieloznacznego na liście argumentów.

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3801.fs)]

Wzorzec symbol wieloznaczny może być przydatny, gdy nie są potrzebne argumenty przekazane, takie jak w głównym punkcie wejścia do programu, gdy użytkownik nie interesuje argumentów wiersza polecenia, które są zwykle dostarczane jako tablica ciągów, jak w poniższym kodzie.

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3802.fs)]

Inne wzorce, które są czasami używane w argumentach są wzorcem i wzorcami `as` identyfikatorów skojarzonymi z związkami rozłącznych i aktywnymi wzorcami. Możesz użyć wzorca Union o pojedynczej wielkości liter w następujący sposób.

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3803.fs)]

Dane wyjściowe są następujące:

```console
Data begins at 0 and ends at 4 in string Et tu, Brute?
Et tu
```

Aktywne wzorce mogą być przydatne jako parametry, na przykład podczas przekształcania argumentu w żądany format, jak w poniższym przykładzie:

```fsharp
type Point = { x : float; y : float }

let (| Polar |) { x = x; y = y} =
    ( sqrt (x*x + y*y), System.Math.Atan (y/ x) )

let radius (Polar(r, _)) = r
let angle (Polar(_, theta)) = theta
```

Możesz użyć `as` wzorca, aby przechowywać dopasowaną wartość jako wartość lokalną, jak pokazano w następującym wierszu kodu.

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3805.fs)]

Inny wzorzec, który jest używany sporadycznie to funkcja, która pozostawia ostatni argument bez nazwy, dostarczając jako treść funkcji wyrażenie lambda, które natychmiast wykonuje dopasowanie wzorca dla niejawnego argumentu. Przykładem jest poniższy wiersz kodu.

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3804.fs)]

Ten kod definiuje funkcję, która przyjmuje listę ogólną i zwraca `true` , jeśli lista jest pusta i `false` w przeciwnym razie. Użycie takich technik może utrudnić odczytywanie kodu.

Czasami wzorce, które obejmują niekompletne dopasowania, są przydatne, na przykład, Jeśli wiesz, że listy w programie mają tylko trzy elementy, możesz użyć wzorca, takiego jak poniższy, na liście parametrów.

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3806.fs)]

Użycie wzorców, które mają niekompletne dopasowania, jest najlepszym zarezerwowane do szybkiego tworzenia prototypów i innych tymczasowych celów. Kompilator wyda Ostrzeżenie dla tego kodu. Takie wzorce nie mogą obejmować ogólnego przypadku wszystkich możliwych danych wejściowych i dlatego nie są odpowiednie do interfejsów API składników.

## <a name="named-arguments"></a>Nazwane argumenty

Argumenty metod można określić za pomocą pozycji na liście argumentów rozdzielanych przecinkami lub mogą być przekazane do metody jawnie przez podanie nazwy, a po niej znaku równości oraz wartości, która ma zostać przeniesiona. Jeśli określony przez podanie nazwy, mogą one pojawić się w innej kolejności niż użyta w deklaracji.

Argumenty nazwane mogą sprawiać, że kod jest bardziej czytelny i bardziej dostosowywalny do niektórych typów zmian w interfejsie API, takich jak zmiana kolejności parametrów metody.

Nazwane argumenty są dozwolone tylko dla metod, nie do `let` funkcji powiązanych, wartości funkcji ani wyrażeń lambda.

Poniższy przykład kodu demonstruje użycie nazwanych argumentów.

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3807.fs)]

W wywołaniu konstruktora klasy można ustawić wartości właściwości klasy przy użyciu składni podobnej do argumentów nazwanych. Poniższy przykład pokazuje tę składnię.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3506.fs)]

Aby uzyskać więcej informacji, zobacz [konstruktory (F #)](members/constructors.md).

## <a name="optional-parameters"></a>Parametry opcjonalne

Można określić opcjonalny parametr dla metody przy użyciu znaku zapytania przed nazwą parametru. Parametry opcjonalne są interpretowane jako typ opcji F #, dzięki czemu można wykonywać zapytania do nich w zwykły sposób, w jaki typy opcji są badane przy użyciu `match` wyrażenia z `Some` i `None` . Parametry opcjonalne są dozwolone tylko w składach, a nie na funkcjach utworzonych za pomocą `let` powiązań.

Istniejące wartości opcjonalne można przekazać do metody za pomocą nazwy parametru, takiej jak `?arg=None` lub `?arg=Some(3)` lub `?arg=arg` . Może to być przydatne podczas kompilowania metody, która przekazuje argumenty opcjonalne do innej metody.

Można również użyć funkcji `defaultArg` , która ustawia wartość domyślną opcjonalnego argumentu. `defaultArg`Funkcja przyjmuje opcjonalny parametr jako pierwszy argument i wartość domyślną jako drugi.

Poniższy przykład ilustruje użycie parametrów opcjonalnych.

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3808.fs)]

Dane wyjściowe są następujące:

```console
Baud Rate: 9600 Duplex: Full Parity: false
Baud Rate: 4800 Duplex: Half Parity: false
Baud Rate: 300 Duplex: Half Parity: true
Baud Rate: 9600 Duplex: Full Parity: false
Baud Rate: 9600 Duplex: Full Parity: false
Baud Rate: 4800 Duplex: Half Parity: false
```

Na potrzeby języka C# i Visual Basic międzyoperacyjności można użyć atrybutów `[<Optional; DefaultParameterValue<(...)>]` w języku F #, aby wywołujący zobaczyli argument jako opcjonalny. Jest to równoznaczne z zdefiniowaniem argumentu jako opcjonalnego w języku C# jako w `MyMethod(int i = 3)` .

```fsharp
open System
open System.Runtime.InteropServices
type C =
    static member Foo([<Optional; DefaultParameterValue("Hello world")>] message) =
        printfn $"{message}"
```

Możesz również określić nowy obiekt jako domyślną wartość parametru. Na przykład `Foo` element członkowski może mieć opcjonalnie `CancellationToken` jako dane wejściowe:

```fsharp
open System.Threading
open System.Runtime.InteropServices
type C =
    static member Foo([<Optional; DefaultParameterValue(CancellationToken())>] ct: CancellationToken) =
        printfn $"{ct}"
```

Wartość określona jako argument `DefaultParameterValue` musi być zgodna z typem parametru. Na przykład następujące elementy są niedozwolone:

```fsharp
type C =
    static member Wrong([<Optional; DefaultParameterValue("string")>] i:int) = ()
```

W takim przypadku kompilator generuje ostrzeżenie i całkowicie zignoruje oba atrybuty. Należy zauważyć, że wartość domyślna `null` musi być adnotacją typu, ponieważ w przeciwnym razie kompilator wnioskuje niewłaściwy typ, tj `[<Optional; DefaultParameterValue(null:obj)>] o:obj` .

## <a name="passing-by-reference"></a>Przekazywanie przez odwołanie

Przekazywanie wartości F # przez odwołanie obejmuje [ByRef](byrefs.md), które są zarządzanymi typami wskaźników. Wskazówki dotyczące używanego typu są następujące:

- Użyj `inref<'T>` , jeśli musisz tylko odczytać wskaźnik.
- Użyj `outref<'T>` , jeśli musisz tylko pisać na wskaźniku.
- Użyj, `byref<'T>` Jeśli musisz zarówno czytać, jak i zapisywać na wskaźniku.

```fsharp
let example1 (x: inref<int>) = printfn $"It's %d{x}"

let example2 (x: outref<int>) = x <- x + 1

let example3 (x: byref<int>) =
    printfn $"It's %d{x}"
    x <- x + 1

let test () =
    // No need to make it mutable, since it's read-only
    let x = 1
    example1 &x

    // Needs to be mutable, since we write to it
    let mutable y = 2
    example2 &y
    example3 &y // Now 'y' is 3
```

Ponieważ parametr jest wskaźnikiem, a wartość jest modyfikowalna, wszelkie zmiany wartości są zachowywane po wykonaniu funkcji.

Można użyć krotki jako wartości zwracanej do przechowywania dowolnych `out` parametrów w metodach biblioteki .NET. Alternatywnie można traktować `out` parametr jako `byref` parametr. Poniższy przykład kodu ilustruje obydwie metody.

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3810.fs)]

## <a name="parameter-arrays"></a>Parameter — Tablice

Czasami konieczne jest zdefiniowanie funkcji, która przyjmuje dowolną liczbę parametrów typu heterogenicznego. Nie byłoby praktyczne, aby utworzyć wszystkie możliwe przeciążone metody w celu uwzględnienia wszystkich typów, które mogą być używane. Implementacje platformy .NET zapewniają obsługę takich metod za pomocą funkcji Tablica parametrów. Metoda przyjmująca tablicę parametrów w jej podpisie może być dostarczana z dowolną liczbą parametrów. Parametry są umieszczane w tablicy. Typ elementów tablicy określa typy parametrów, które mogą być przesyłane do funkcji. Jeśli zdefiniujesz tablicę parametrów `System.Object` jako typ elementu, kod klienta może przekazać wartości dowolnego typu.

W języku F # tablice parametrów można definiować tylko w metodach. Nie mogą być używane w autonomicznych funkcjach lub funkcjach, które są zdefiniowane w modułach.

Należy zdefiniować tablicę parametrów przy użyciu `ParamArray` atrybutu. Ten `ParamArray` atrybut może być stosowany tylko do ostatniego parametru.

Poniższy kod ilustruje zarówno wywołanie metody .NET, która przyjmuje tablicę parametrów i definicję typu w F #, który ma metodę, która pobiera tablicę parametrów.

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-2/snippet3811.fs)]

Po uruchomieniu w projekcie dane wyjściowe poprzedniego kodu są następujące:

```console
a 1 10 Hello world 1 True
"a"
1
10.0
"Hello world"
1u
true
```

## <a name="see-also"></a>Zobacz także

- [Elementy członkowskie](./members/index.md)
