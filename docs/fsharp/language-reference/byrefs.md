---
title: Byrefs
description: 'Dowiedz się więcej na temat typów ByRef i ByRef w języku F #, które są używane do programowania niskiego poziomu.'
ms.date: 11/04/2019
ms.openlocfilehash: ff2c06d8940f7341d5d8b1d942be264bfac586c5
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740318"
---
# <a name="byrefs"></a>Byrefs

Język F # ma dwa główne obszary funkcji, które zajmują miejsce w programowaniu niskiego poziomu:

* `byref` / `inref` / `outref` Typy, które są wskaźnikami zarządzanymi. Mają ograniczenia dotyczące użycia, dzięki czemu nie można skompilować programu, który jest nieprawidłowy w czasie wykonywania.
* Struktury `byref` podobnej do [struktury](structures.md) , która ma podobną semantykę i te same ograniczenia czasu kompilacji, co `byref<'T>` . Przykładem jest <xref:System.Span%601> .

## <a name="syntax"></a>Składnia

```fsharp
// Byref types as parameters
let f (x: byref<'T>) = ()
let g (x: inref<'T>) = ()
let h (x: outref<'T>) = ()

// Calling a function with a byref parameter
let mutable x = 3
f &x

// Declaring a byref-like struct
open System.Runtime.CompilerServices

[<Struct; IsByRefLike>]
type S(count1: int, count2: int) =
    member x.Count1 = count1
    member x.Count2 = count2
```

## <a name="byref-inref-and-outref"></a>ByRef, inref i outref

Istnieją trzy formy `byref` :

* `inref<'T>`, zarządzany wskaźnik odczytu wartości źródłowej.
* `outref<'T>`, zarządzany wskaźnik zapisu do podstawowej wartości.
* `byref<'T>`zarządzany wskaźnik służący do odczytywania i zapisywania podstawowej wartości.

`byref<'T>`Można przesłać w miejscu, w którym `inref<'T>` jest oczekiwany. Podobnie `byref<'T>` można przesłać, gdzie `outref<'T>` oczekiwano.

## <a name="using-byrefs"></a>Korzystanie z ByRef

Aby użyć `inref<'T>` , należy uzyskać wartość wskaźnika przy użyciu `&` :

```fsharp
open System

let f (dt: inref<DateTime>) =
    printfn $"Now: %O{dt}"

let usage =
    let dt = DateTime.Now
    f &dt // Pass a pointer to 'dt'
```

Aby zapisać na wskaźniku przy użyciu `outref<'T>` lub `byref<'T>` , należy również wprowadzić wartość, do której będzie można uzyskać wskaźnik `mutable` .

```fsharp
open System

let f (dt: byref<DateTime>) =
    printfn $"Now: %O{dt}"
    dt <- DateTime.Now

// Make 'dt' mutable
let mutable dt = DateTime.Now

// Now you can pass the pointer to 'dt'
f &dt
```

Jeśli chcesz tylko napisać wskaźnik zamiast odczytywać go, rozważ użycie `outref<'T>` zamiast `byref<'T>` .

### <a name="inref-semantics"></a>Semantyka Inref

Spójrzmy na poniższy kod:

```fsharp
let f (x: inref<SomeStruct>) = x.SomeField
```

Semantycznie:

* Symbol zastępczy `x` wskaźnika może używać go tylko do odczytu wartości.
* Dowolny wskaźnik uzyskany do `struct` pól zagnieżdżonych w ramach `SomeStruct` danego typu `inref<_>` .

Spełnione są również następujące kwestie:

* Nie ma żadnego znaczenia, że inne wątki lub aliasy nie mają dostępu do zapisu `x` .
* Nie ma żadnych implikacji, które `SomeStruct` są niezmienne w wyniku `x` `inref` .

Jednak dla typów wartości języka F #, które **są** niezmienne, `this` wskaźnik jest wywnioskowany jako `inref` .

Wszystkie te reguły razem oznaczają, że posiadacz `inref` wskaźnika nie modyfikuje natychmiastowej zawartości wskazanej pamięci.

### <a name="outref-semantics"></a>Semantyka Outref

Celem `outref<'T>` jest wskazanie, że na wskaźniku należy tylko pisać. Nieoczekiwanie `outref<'T>` zezwala na odczytywanie wartości źródłowej pomimo jej nazwy. Jest to przeznaczone do celów zgodności. Semantyka `outref<'T>` nie różni się od `byref<'T>` .

### <a name="interop-with-c"></a>Współdziałanie z C\#

Język C# obsługuje `in ref` `out ref` słowa kluczowe i, a nie `ref` zwraca. W poniższej tabeli przedstawiono, w jaki sposób F # interpretuje, co emituje w języku C#:

|Konstrukcja języka C#|Liczba wniosku w języku F #|
|------------|---------|
|`ref` wartość zwracana|`outref<'T>`|
|`ref readonly` wartość zwracana|`inref<'T>`|
|`in ref` konstruktora|`inref<'T>`|
|`out ref` konstruktora|`outref<'T>`|

W poniższej tabeli pokazano, co emituje F #:

|Konstrukcja języka F #|Wyemitowana konstrukcja|
|------------|-----------------|
|Argument `inref<'T>`|`[In]` atrybut argumentu|
|`inref<'T>` przesłać|`modreq` atrybut wartości|
|`inref<'T>` w nieabstrakcyjnym gnieździe lub implementacji|`modreq` on argument lub Return|
|Argument `outref<'T>`|`[Out]` atrybut argumentu|

### <a name="type-inference-and-overloading-rules"></a>Wnioskowanie o typie i reguły przeciążania

`inref<'T>`Typ jest wnioskowany przez kompilator F # w następujących przypadkach:

1. Parametr .NET lub zwracany typ, który ma `IsReadOnly` atrybut.
2. `this`Wskaźnik na typie struktury, który nie ma modyfikowalnych pól.
3. Adres lokalizacji pamięci pochodzącej od innego `inref<_>` wskaźnika.

Gdy jest używany niejawny adres `inref` , Przeciążenie z argumentem typu `SomeType` jest preferowany do przeciążenia z argumentem typu `inref<SomeType>` . Na przykład:

```fsharp
type C() =
    static member M(x: System.DateTime) = x.AddDays(1.0)
    static member M(x: inref<System.DateTime>) = x.AddDays(2.0)
    static member M2(x: System.DateTime, y: int) = x.AddDays(1.0)
    static member M2(x: inref<System.DateTime>, y: int) = x.AddDays(2.0)

let res = System.DateTime.Now
let v =  C.M(res)
let v2 =  C.M2(res, 4)
```

W obu przypadkach przeciążenia `System.DateTime` są rozwiązywane, a nie przez pobieranie przeciążenia `inref<System.DateTime>` .

## <a name="byref-like-structs"></a>Struktury podobne do ByRef

Oprócz `byref` / `inref` / `outref` trójka można definiować własne struktury, które mogą stosować się do `byref` semantyki podobnej. Jest to realizowane z <xref:System.Runtime.CompilerServices.IsByRefLikeAttribute> atrybutem:

```fsharp
open System
open System.Runtime.CompilerServices

[<IsByRefLike; Struct>]
type S(count1: Span<int>, count2: Span<int>) =
    member x.Count1 = count1
    member x.Count2 = count2
```

`IsByRefLike` nie oznacza `Struct` . Oba muszą być obecne w typie.

Struktura " `byref` like" w języku F # jest typem wartości powiązanej ze stosem. Nigdy nie jest przydzielany na zarządzanym stosie. `byref`Struktura przypominająca podobne rozwiązanie jest przydatna w programowaniu o wysokiej wydajności, ponieważ jest wymuszana z zestawem silnych sprawdzeń i bez przechwycenia. Reguły są następujące:

* Mogą one być używane jako parametry funkcji, parametry metody, zmienne lokalne, Metoda Return.
* Nie mogą być statyczne ani składowe wystąpień klasy ani normalnej struktury.
* Nie mogą być przechwytywane przez żadną konstrukcję zamknięcia ( `async` metody lub wyrażenia lambda).
* Nie mogą być używane jako parametr generyczny.

Ten ostatni punkt jest decydujący dla programowania w stylu potoku języka F #, podobnie jak `|>` ogólna funkcja, która parameterizes jego typy wejściowe. To ograniczenie może być `|>` w przyszłości swobodne, ponieważ jest wbudowane i nie wykonuje żadnych wywołań funkcji ogólnych, które nie są określone w treści.

Chociaż te reguły silnie ograniczają użycie, robią to w celu zapewnienia bezpieczeństwa obliczeń o wysokiej wydajności w bezpieczny sposób.

## <a name="byref-returns"></a>Zwracane przez ByRef

Funkcja ByRef zwraca z funkcji F # lub elementów członkowskich, które mogą być tworzone i używane. Podczas konsumowania `byref` metody zwracanej wartość jest niejawnie wykorzystana. Na przykład:

```fsharp
let squareAndPrint (data : byref<int>) =
    let squared = data*data    // data is implicitly dereferenced
    printfn $"%d{squared}"
```

Aby zwrócić wartość ByRef, zmienna, która zawiera wartość, musi znajdować się na żywo dłużej niż bieżący zakres.
Ponadto, aby zwrócić element ByRef, użyj `&value` (gdzie Value jest zmienną, która jest dłuższa niż bieżący zakres).

```fsharp
let mutable sum = 0
let safeSum (bytes: Span<byte>) =
    for i in 0 .. bytes.Length - 1 do
        sum <- sum + int bytes.[i]
    &sum  // sum lives longer than the scope of this function.
```

Aby uniknąć niejawnego odwołania, na przykład przekazywania odwołania przez wiele wywołań łańcucha, użyj `&x` (gdzie `x` jest wartością).

Możesz również bezpośrednio przypisać do powrotu `byref` . Weź pod uwagę następujący (wysoce bezwzględny) program:

```fsharp
type C() =
    let mutable nums = [| 1; 3; 7; 15; 31; 63; 127; 255; 511; 1023 |]

    override _.ToString() = String.Join(' ', nums)

    member _.FindLargestSmallerThan(target: int) =
        let mutable ctr = nums.Length - 1

        while ctr > 0 && nums.[ctr] >= target do ctr <- ctr - 1

        if ctr > 0 then &nums.[ctr] else &nums.[0]

[<EntryPoint>]
let main argv =
    let c = C()
    printfn $"Original sequence: %O{c}"

    let v = &c.FindLargestSmallerThan 16

    v <- v*2 // Directly assign to the byref return

    printfn $"New sequence:      %O{c}"

    0 // return an integer exit code
```

Jest to produkt wyjściowy:

```console
Original sequence: 1 3 7 15 31 63 127 255 511 1023
New sequence:      1 3 7 30 31 63 127 255 511 1023
```

## <a name="scoping-for-byrefs"></a>Określanie zakresu dla ByRef

`let`Wartość powiązania nie może mieć odwołania przekraczającego zakres, w którym został zdefiniowany. Na przykład następujące elementy są niedozwolone:

```fsharp
let test2 () =
    let x = 12
    &x // Error: 'x' exceeds its defined scope!

let test () =
    let x =
        let y = 1
        &y // Error: `y` exceeds its defined scope!
    ()
```

Dzięki temu można uzyskać różne wyniki w zależności od tego, czy kompilujesz z optymalizacją.
