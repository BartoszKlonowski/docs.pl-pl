---
title: 'Co nowego w języku F # 5,0 — Przewodnik po języku f #'
description: 'Zapoznaj się z omówieniem nowych funkcji dostępnych w języku F # 5,0.'
ms.date: 11/06/2020
ms.openlocfilehash: 2384f1a75f5e708dc6f170d82fa15c5e0f54c85d
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740188"
---
# <a name="whats-new-in-f-50"></a>Co nowego w języku F # 5,0

F # 5,0 dodaje kilka ulepszeń języka F # i F# Interactive. Jest on publikowany z **platformą .NET 5**.

Najnowszą wersję zestawu SDK platformy .NET można pobrać ze [strony plików do pobrania platformy .NET](https://dotnet.microsoft.com/download).

## <a name="get-started"></a>Rozpoczęcie pracy

Język F # 5,0 jest dostępny we wszystkich dystrybucjach .NET Core i narzędziach programu Visual Studio. Aby uzyskać więcej informacji, zobacz [wprowadzenie do języka F #](../get-started/index.md) , aby dowiedzieć się więcej.

## <a name="package-references-in-f-scripts"></a>Odwołania do pakietów w skryptach języka F #

Język f # 5 zapewnia obsługę odwołań do pakietów w skryptach języka F # z `#r "nuget:..."` składnią. Rozważmy na przykład następujące odwołanie do pakietu:

```fsharp
#r "nuget: Newtonsoft.Json"

open Newtonsoft.Json

let o = {| X = 2; Y = "Hello" |}

printfn $"{JsonConvert.SerializeObject o}"
```

Możesz również podać wersję jawną po nazwie pakietu w następujący sposób:

```fsharp
#r "nuget: Newtonsoft.Json,11.0.1"
```

Pakiet zawiera odwołania do pakietów z natywnymi zależnościami, takimi jak ML.NET.

Odwołania do pakietów obsługują również pakiety z specjalnymi wymaganiami dotyczącymi odwoływania się do elementów zależnych `.dll` . Na przykład pakiet [FParsec](https://www.nuget.org/packages/FParsec/) używany do wymagania, aby użytkownicy ręcznie upewnili się, że jego odwołanie `FParsecCS.dll` zostało odwołane jako pierwsze przed `FParsec.dll` odwołaniem do F# Interactive. Nie jest to już potrzebne i można odwołać się do pakietu w następujący sposób:

```fsharp
#r "nuget: FParsec"

open FParsec

let test p str =
    match run p str with
    | Success(result, _, _)   -> printfn $"Success: {result}"
    | Failure(errorMsg, _, _) -> printfn $"Failure: {errorMsg}"

test pfloat "1.234"
```

Ta funkcja implementuje [Narzędzia języka F # RFC FST —-1027](https://github.com/fsharp/fslang-design/blob/master/tooling/FST-1027-fsi-references.md). Aby uzyskać więcej informacji na temat odwołań do pakietów, zobacz samouczek [F# Interactive](../tools/fsharp-interactive/index.md) .

## <a name="string-interpolation"></a>Interpolacja ciągów

Ciągi interpolowane języka F # są stosunkowo podobne do interpolowanych ciągów języka C# lub JavaScript, w tym, że umożliwiają pisanie kodu w "dziurach" wewnątrz literału ciągu. Poniżej przedstawiono prosty przykład:

```fsharp
let name = "Phillip"
let age = 29
printfn $"Name: {name}, Age: {age}"

printfn $"I think {3.0 + 0.14} is close to {System.Math.PI}!"
```

Jednakże interpolowane ciągi F # umożliwiają również wpisywanie typów interpolacji, podobnie jak `sprintf` Funkcja, aby wymusić, że wyrażenie wewnątrz interpolowanego kontekstu jest zgodne z określonym typem. Używa tego samego specyfikatora formatu.

```fsharp
let name = "Phillip"
let age = 29

printfn $"Name: %s{name}, Age: %d{age}"

// Error: type mismatch
printfn $"Name: %s{age}, Age: %d{name}"
```

W powyższym przykładzie interpolacji, `%s` wymaga interpolacji jako typu `string` , natomiast `%d` wymaga interpolacji jako `integer` .

Ponadto dowolne dowolne wyrażenie F # (lub wyrażenia) można umieścić po stronie kontekstu interpolacji. Istnieje nawet możliwość napisania bardziej skomplikowanego wyrażenia, takiego jak:

```fsharp
let str =
    $"""The result of squaring each odd item in {[1..10]} is:
{
    let square x = x * x
    let isOdd x = x % 2 <> 0
    let oddSquares xs =
        xs
        |> List.filter isOdd
        |> List.map square
    oddSquares [1..10]
}
"""
```

Chociaż nie zalecamy tego, aby to zrobić zbyt wiele.

Ta funkcja implementuje [Język F # RFC FS-1001](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1001-StringInterpolation.md).

## <a name="support-for-nameof"></a>Obsługa nameof

F # 5 obsługuje `nameof` operator, który rozwiązuje symbol używany do i tworzy jego nazwę w źródle F #. Jest to przydatne w różnych scenariuszach, takich jak rejestrowanie i ochrona rejestrowania przed zmianami w kodzie źródłowym.

```fsharp
let months =
    [
        "January"; "February"; "March"; "April";
        "May"; "June"; "July"; "August"; "September";
        "October"; "November"; "December"
    ]

let lookupMonth month =
    if (month > 12 || month < 1) then
        invalidArg (nameof month) (sprintf "Value passed in was %d." month)

    months.[month-1]

printfn $"{lookupMonth 12}"
printfn $"{lookupMonth 1}"
printfn $"{lookupMonth 13}"
```

Ostatni wiersz zgłosi wyjątek, a "miesiąc" zostanie wyświetlony w komunikacie o błędzie.

Można przyjąć nazwę niemal każdej konstrukcji F #:

```fsharp
module M =
    let f x = nameof x

printfn $"{M.f 12}"
printfn $"{nameof M}"
printfn $"{nameof M.f}"
```

Trzy końcowe dodatki to zmiany wykonywane przez operatorów: dodanie `nameof<'type-parameter>` formularza dla parametrów typu ogólnego i możliwość użycia `nameof` jako wzorca w wyrażeniu dopasowania do wzorca.

Pobranie nazwy operatora powoduje powstanie jego ciągu źródłowego. Jeśli potrzebujesz skompilowanego formularza, użyj skompilowanej nazwy operatora:

```fsharp
nameof(+) // "+"
nameof op_Addition // "op_Addition"
```

Pobranie nazwy parametru typu wymaga nieco innej składni:

```fsharp
type C<'TType> =
    member _.TypeName = nameof<'TType>
```

Jest to podobne do `typeof<'T>` operatorów i `typedefof<'T>` .

F # 5 dodaje również obsługę `nameof` wzorca, który może być używany w `match` wyrażeniach:

```fsharp
[<Struct; IsByRefLike>]
type RecordedEvent = { EventType: string; Data: ReadOnlySpan<byte> }

type MyEvent =
    | AData of int
    | BData of string

let deserialize (e: RecordedEvent) : MyEvent =
    match e.EventType with
    | nameof AData -> AData (JsonSerializer.Deserialize<int> e.Data)
    | nameof BData -> BData (JsonSerializer.Deserialize<string> e.Data)
    | t -> failwithf "Invalid EventType: %s" t
```

Poprzedzający kod używa elementu "nameof" zamiast literału ciągu w wyrażeniu Match.

Ta funkcja implementuje [Język F # RFC FS-1003](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1003-nameof-operator.md).

## <a name="open-type-declarations"></a>Otwieranie deklaracji typu

F # 5 dodaje również obsługę dla deklaracji typu Open. Deklaracja typu Open jest taka sama jak otwieranie klasy statycznej w języku C#, z wyjątkiem sytuacji, w której inna składnia i nieco inne zachowanie dopasowuje semantykę języka F #.

Za pomocą deklaracji typu Open można `open` udostępniać zawartość statyczną w obrębie tego typu. Ponadto, możesz określić, że `open` w języku F # definicje i rekordy mają być ujawnione. Na przykład może to być przydatne, jeśli masz Unię zdefiniowaną w module i chcesz uzyskać do nich dostęp, ale nie chcesz otwierać całego modułu.

```fsharp
open type System.Math

let x = Min(1.0, 2.0)

module M =
    type DU = A | B | C

    let someOtherFunction x = x + 1

// Open only the type inside the module
open type M.DU

printfn $"{A}"
```

W przeciwieństwie do języka C#, `open type` w przypadku dwóch typów, które uwidaczniają składową o tej samej nazwie, element członkowski z ostatniego typu jest `open` zasłaniał inną nazwę. Jest to zgodne z semantyką języka F # otaczającą już istniejące cieniowanie.

Ta funkcja implementuje [Język F # RFC FS-1068](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1068-open-type-declaration.md).

## <a name="consistent-slicing-behavior-for-built-in-data-types"></a>Spójne zachowanie tworzenia wycinków dla wbudowanych typów danych

Zachowanie tworzenia wycinków wbudowanych `FSharp.Core` typów danych (Array, list, String, Array 2D, tablica 3W, 4D Array) używanych jako niespójne przed F # 5. Niektóre zachowania w przypadku krawędzi wywołało wyjątek i niektóre nie. W języku F # 5 wszystkie wbudowane typy zwracają teraz puste wycinki dla wycinków, które nie są możliwe do wygenerowania:

```fsharp
let l = [ 1..10 ]
let a = [| 1..10 |]
let s = "hello!"

// Before: would return empty list
// F# 5: same
let emptyList = l.[-2..(-1)]

// Before: would throw exception
// F# 5: returns empty array
let emptyArray = a.[-2..(-1)]

// Before: would throw exception
// F# 5: returns empty string
let emptyString = s.[-2..(-1)]
```

Ta funkcja implementuje [Język F # RFC FS-1077](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1077-tolerant-slicing.md).

## <a name="fixed-index-slices-for-3d-and-4d-arrays-in-fsharpcore"></a>Wycinków o stałym indeksie dla tablic 3W i 4D w FSharp. Core

Język F # 5,0 zapewnia obsługę tworzenia wycinków ze stałym indeksem w wbudowanych typach tablic 3W i 4D.

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

Co zrobić, jeśli chcesz wyodrębnić wycinek `[| 4; 5 |]` z tablicy? Jest to teraz bardzo proste!

```fsharp
// First, create a 3D array to slice

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

Ta funkcja implementuje [Język F # RFC FS-1077b](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1077-3d-4d-fixed-index-slicing.md).

## <a name="f-quotations-improvements"></a>Udoskonalenia cytatów języka F #

[Cytaty kodu](../language-reference/code-quotations.md) języka F # mają teraz możliwość zachowania informacji o ograniczeniach typu. Rozpatrzmy następujący przykład:

```fsharp
open FSharp.Linq.RuntimeHelpers

let eval q = LeafExpressionConverter.EvaluateQuotation q

let inline negate x = -x
// val inline negate: x: ^a ->  ^a when  ^a : (static member ( ~- ) :  ^a ->  ^a)

<@ negate 1.0 @>  |> eval
```

Ograniczenie generowane przez `inline` funkcję jest zachowywane w cudzysłowie kodu. `negate`Można teraz ocenić formularz quotated funkcji.

Ta funkcja implementuje [Język F # RFC FS-1071](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1071-witness-passing-quotations.md).

## <a name="applicative-computation-expressions"></a>Wyrażenia obliczeń Applicative

[Wyrażenia obliczeń (CE)](../language-reference/computation-expressions.md) są używane dzisiaj do modelowania "obliczeń kontekstowych" lub w bardziej funkcjonalnej terminologii programowania, monadic obliczeń.

W języku F # 5 wprowadzono applicative CE, który oferuje inny model obliczeniowy. Applicative ce zezwala na bardziej wydajne obliczenia pod warunkiem, że każde obliczenie jest niezależne, a ich wyniki są gromadzone na końcu. Gdy obliczenia są niezależne od siebie, są one również proste działania równoległego, co umożliwia autorom CE pisanie bardziej wydajnych bibliotek. Ta korzyść obejmuje ograniczenie, chociaż: obliczenia zależne od wcześniej obliczonych wartości są niedozwolone.

W poniższym przykładzie przedstawiono podstawowe applicative CE dla `Result` typu.

```fsharp
// First, define a 'zip' function
module Result =
    let zip x1 x2 =
        match x1,x2 with
        | Ok x1res, Ok x2res -> Ok (x1res, x2res)
        | Error e, _ -> Error e
        | _, Error e -> Error e

// Next, define a builder with 'MergeSources' and 'BindReturn'
type ResultBuilder() =
    member _.MergeSources(t1: Result<'T,'U>, t2: Result<'T1,'U>) = Result.zip t1 t2
    member _.BindReturn(x: Result<'T,'U>, f) = Result.map f x

let result = ResultBuilder()

let run r1 r2 r3 =
    // And here is our applicative!
    let res1: Result<int, string> =
        result {
            let! a = r1
            and! b = r2
            and! c = r3
            return a + b - c
        }

    match res1 with
    | Ok x -> printfn $"{nameof res1} is: %d{x}"
    | Error e -> printfn $"{nameof res1} is: {e}"

let printApplicatives () =
    let r1 = Ok 2
    let r2 = Ok 3 // Error "fail!"
    let r3 = Ok 4

    run r1 r2 r3
    run r1 (Error "failure!") r3
```

Jeśli jesteś autorem biblioteki, który obecnie udostępnia w swojej bibliotece usługi rejestracji certyfikatów, musisz wiedzieć kilka dodatkowych zagadnień.

Ta funkcja implementuje [Język F # RFC FS-1063](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1063-support-letbang-andbang-for-applicative-functors.md).

## <a name="interfaces-can-be-implemented-at-different-generic-instantiations"></a>Interfejsy można zaimplementować w różnych ogólnych wystąpieniach

Teraz można zaimplementować ten sam interfejs w różnych wystąpieniach ogólnych:

```fsharp
type IA<'T> =
    abstract member Get : unit -> 'T

type MyClass() =
    interface IA<int> with
        member x.Get() = 1
    interface IA<string> with
        member x.Get() = "hello"

let mc = MyClass()
let iaInt = mc :> IA<int>
let iaString = mc :> IA<string>

iaInt.Get() // 1
iaString.Get() // "hello"
```

Ta funkcja implementuje [Język F # RFC FS-1031](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1031-Allow%20implementing%20the%20same%20interface%20at%20different%20generic%20instantiations%20in%20the%20same%20type.md).

## <a name="default-interface-member-consumption"></a>Użycie domyślnego interfejsu

Język F # 5 umożliwia korzystanie [z interfejsów z domyślnymi implementacjami](../../csharp/tutorials/default-interface-methods-versions.md).

Rozważ użycie interfejsu zdefiniowanego w języku C# w następujący sposób:

```csharp
using System;

namespace CSharp
{
    public interface MyDimasd
    {
        public int Z => 0;
    }
}
```

Można go wykorzystać w F # za pomocą dowolnego standardowego sposobu implementacji interfejsu:

```fsharp
open CSharp

// You can implement the interface via a class
type MyType() =
    member _.M() = ()

    interface MyDim

let md = MyType() :> MyDim
printfn $"DIM from C#: %d{md.Z}"

// You can also implement it via an object expression
let md' = { new MyDim }
printfn $"DIM from C# but via Object Expression: %d{md'.Z}"
```

Dzięki temu można bezpiecznie korzystać z kodu w języku C# i składników .NET zapisanych w nowoczesnej C#, gdy użytkownicy będą mogli korzystać z implementacji domyślnej.

Ta funkcja implementuje [Język F # RFC FS-1074](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1074-default-interface-member-consumption.md).

## <a name="simplified-interop-with-nullable-value-types"></a>Uproszczona międzyoperacyjna z typami wartości null

[Typy dopuszczające wartości null (o wartościach](https://docs.microsoft.com/dotnet/api/system.nullable-1) dopuszczających wartość null) były obsługiwane przez język F #, ale współpracujące z nimi są tradycyjnie nieco nieznacznie odbiegać, ponieważ trzeba utworzyć `Nullable` `Nullable<SomeType>` otokę lub za każdym razem, gdy chcesz przekazać wartość. Teraz kompilator niejawnie przekonwertuje typ wartości na, `Nullable<ThatValueType>` Jeśli typ docelowy jest zgodny. Teraz można wykonać następujące czynności:

```fsharp
#r "nuget: Microsoft.Data.Analysis"

open Microsoft.Data.Analysis

let dateTimes = PrimitiveDataFrameColumn<DateTime>("DateTimes")

// The following line used to fail to compile
dateTimes.Append(DateTime.Parse("2019/01/01"))

// The previous line is now equivalent to this line
dateTimes.Append(Nullable<DateTime>(DateTime.Parse("2019/01/01")))
```

Ta funkcja implementuje [Język F # RFC FS-1075](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1075-nullable-interop.md).

## <a name="preview-reverse-indexes"></a>Wersja zapoznawcza: przewracanie indeksów

W języku F # 5 wprowadzono również podgląd zezwalający na odwracanie indeksów. Składnia jest następująca: `^idx` Oto jak można określić wartość elementu 1 z końca listy:

```fsharp
let xs = [1..10]

// Get element 1 from the end:
xs.[^1]

// From the end slices

let lastTwoOldStyle = xs.[(xs.Length-2)..]

let lastTwoNewStyle = xs.[^1..]

lastTwoOldStyle = lastTwoNewStyle // true
```

Można także definiować Odwróć indeksy dla własnych typów. Aby to zrobić, należy wdrożyć następującą metodę:

```fsharp
GetReverseIndex: dimension: int -> offset: int
```

Oto przykład dla `Span<'T>` typu:

```fsharp
open System

type Span<'T> with
    member sp.GetSlice(startIdx, endIdx) =
        let s = defaultArg startIdx 0
        let e = defaultArg endIdx sp.Length
        sp.Slice(s, e - s)

    member sp.GetReverseIndex(_, offset: int) =
        sp.Length - offset

let printSpan (sp: Span<int>) =
    let arr = sp.ToArray()
    printfn $"{arr}"

let run () =
    let sp = [| 1; 2; 3; 4; 5 |].AsSpan()

    // Pre-# 5.0 slicing on a Span<'T>
    printSpan sp.[0..] // [|1; 2; 3; 4; 5|]
    printSpan sp.[..3] // [|1; 2; 3|]
    printSpan sp.[1..3] // |2; 3|]

    // Same slices, but only using from-the-end index
    printSpan sp.[..^0] // [|1; 2; 3; 4; 5|]
    printSpan sp.[..^2] // [|1; 2; 3|]
    printSpan sp.[^4..^2] // [|2; 3|]

run() // Prints the same thing twice
```

Ta funkcja implementuje [Język F # RFC FS-1076](https://github.com/fsharp/fslang-design/blob/master/preview/FS-1076-from-the-end-slicing.md).

## <a name="preview-overloads-of-custom-keywords-in-computation-expressions"></a>Wersja zapoznawcza: przeciążenia niestandardowych słów kluczowych w wyrażeniach obliczeń

Wyrażenia obliczeń to zaawansowana funkcja dla autorów bibliotek i struktur. Pozwalają one znacząco ulepszyć wyrazistości składników, umożliwiając zdefiniowanie dobrze znanych elementów członkowskich i tworzą DSL dla domeny, w której pracujesz.

F # 5 dodaje obsługę w wersji zapoznawczej w celu przeładowania niestandardowych operacji w wyrażeniach obliczeniowych. Umożliwia zapisanie i użycie następującego kodu:

```fsharp
open System

type InputKind =
    | Text of placeholder:string option
    | Password of placeholder: string option

type InputOptions =
  { Label: string option
    Kind : InputKind
    Validators : (string -> bool) array }

type InputBuilder() =
    member t.Yield(_) =
      { Label = None
        Kind = Text None
        Validators = [||] }

    [<CustomOperation("text")>]
    member this.Text(io, ?placeholder) =
        { io with Kind = Text placeholder }

    [<CustomOperation("password")>]
    member this.Password(io, ?placeholder) =
        { io with Kind = Password placeholder }

    [<CustomOperation("label")>]
    member this.Label(io, label) =
        { io with Label = Some label }

    [<CustomOperation("with_validators")>]
    member this.Validators(io, [<ParamArray>] validators) =
        { io with Validators = validators }

let input = InputBuilder()

let name =
    input {
    label "Name"
    text
    with_validators
        (String.IsNullOrWhiteSpace >> not)
    }

let email =
    input {
    label "Email"
    text "Your email"
    with_validators
        (String.IsNullOrWhiteSpace >> not)
        (fun s -> s.Contains "@")
    }

let password =
    input {
    label "Password"
    password "Must contains at least 6 characters, one number and one uppercase"
    with_validators
        (String.exists Char.IsUpper)
        (String.exists Char.IsDigit)
        (fun s -> s.Length >= 6)
    }
```

Przed wprowadzeniem tej zmiany można napisać `InputBuilder` Typ w takiej postaci, w jakiej jest, ale nie można go użyć w tym przykładzie. Ponieważ przeciążenia, parametry opcjonalne i teraz `System.ParamArray` są dozwolone, wszystko działa zgodnie z oczekiwaniami.

Ta funkcja implementuje [Język F # RFC FS-1056](https://github.com/fsharp/fslang-design/blob/master/preview/FS-1056-allow-custom-operation-overloads.md).
