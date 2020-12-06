---
title: Wskazówki dotyczące formatowania kodu F#
description: 'Poznaj wskazówki dotyczące formatowania kodu F #.'
ms.date: 08/31/2020
ms.openlocfilehash: f9b62a18a5c525924f3ae6da3fbc650394340047
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96739892"
---
# <a name="f-code-formatting-guidelines"></a>Wskazówki dotyczące formatowania kodu F#

Ten artykuł zawiera wskazówki dotyczące sposobu formatowania kodu w taki sposób, aby kod języka F #:

* Bardziej czytelne
* Zgodnie z konwencjami stosowanymi przez narzędzia formatowania w programie Visual Studio i innych edytorach
* Podobnie jak w przypadku innych kodów online

Wytyczne te są oparte na [kompleksowym przewodniku w zakresie stosowania Konwencji formatowania języka F #](https://github.com/dungpa/fantomas/blob/master/docs/FormattingConventions.md) przez [Anh-obornik Phan](https://github.com/dungpa).

## <a name="general-rules-for-indentation"></a>Ogólne reguły wcięć

F # domyślnie używa znacznego białego odstępu. W poniższych wytycznych zawarto informacje na temat sposobu Juggle niektórych wyzwań.

### <a name="using-spaces"></a>Używanie spacji

Gdy jest wymagane wcięcie, należy użyć spacji, a nie tabulacji. Wymagane jest co najmniej jedno miejsce. Organizacja może tworzyć standardy kodowania, aby określić liczbę spacji do użycia w przypadku wcięcia; dwa, trzy lub cztery spacje wcięcia na każdym poziomie, gdzie występuje wcięcie jest typowe.

**Zalecamy użycie czterech spacji na wcięcie.**

Oznacza to, że wcięcie programów jest subiektywne. Różnice są prawidłowe, ale pierwsza reguła, którą należy wykonać, jest *spójna z wcięciem*. Wybierz ogólnie zaakceptowany styl wcięcia i używaj go systematycznie w całej bazie kodu.

## <a name="formatting-white-space"></a>Formatowanie białego znaku

W języku F # jest rozróżniana wielkość liter. Chociaż większość semantyki z białego znaku jest objęta odpowiednimi wcięciami, należy wziąć pod uwagę pewne inne zagadnienia.

### <a name="formatting-operators-in-arithmetic-expressions"></a>Operatory formatowania w wyrażeniach arytmetycznych

Zawsze używaj białych znaków wokół binarnych wyrażeń arytmetycznych:

```fsharp
let subtractThenAdd x = x - 1 + 3
```

Operatory jednoargumentowe `-` powinny zawsze występować bezpośrednio po nich wartość negacji:

```fsharp
// OK
let negate x = -x

// Bad
let negateBad x = - x
```

Dodanie znaku odstępu, gdy `-` operator może prowadzić do pomyłki dla innych.

Podsumowując, ważne jest, aby zawsze:

* Otocz operatory binarne z białym znakiem
* Nie pozostawiaj pustego odstępu po operatorze jednoargumentowym

Wytyczne binarnego operatora arytmetycznego są szczególnie ważne. Nie można ująć operatora binarnego `-` , gdy jest on połączony z pewnymi opcjami formatowania, może prowadzić do interpretowania go jako jednoargumentowy `-` .

### <a name="surround-a-custom-operator-definition-with-white-space"></a>Umieść niestandardową definicję operatora z białym znakiem

Zawsze używaj białego znaku, aby obsłużyć definicję operatora:

```fsharp
// OK
let ( !> ) x f = f x

// Bad
let (!>) x f = f x
```

Dla dowolnego operatora niestandardowego, który rozpoczyna się od `*` i który ma więcej niż jeden znak, należy dodać białe miejsce na początku definicji, aby uniknąć niejednoznaczności kompilatora. Z tego względu zalecamy, aby po prostu ująć definicje wszystkich operatorów z pojedynczym znakiem odstępu.

### <a name="surround-function-parameter-arrows-with-white-space"></a>Strzałki parametru funkcji przestrzenny z białym znakiem

Podczas definiowania sygnatury funkcji należy użyć białego `->` znaku wokół symbolu:

```fsharp
// OK
type MyFun = int -> int -> string

// Bad
type MyFunBad = int->int->string
```

### <a name="surround-function-arguments-with-white-space"></a>Argumenty funkcji przestrzenny z białym znakiem

Podczas definiowania funkcji należy używać odstępów wokół każdego argumentu.

```fsharp
// OK
let myFun (a: decimal) b c = a + b + c

// Bad
let myFunBad (a:decimal)(b)c = a + b + c
```

### <a name="place-parameters-on-a-new-line-for-long-definitions"></a>Umieść parametry w nowym wierszu dla długich definicji

Jeśli masz długą definicję funkcji, umieść parametry w nowych wierszach i Zwiększ wcięcie w celu dopasowania do poziomu wcięcia kolejnego parametru.

```fsharp
module M =
    let LongFunctionWithLotsOfParameters(aVeryLongParam: AVeryLongTypeThatYouNeedToUse)
                                        (aSecondVeryLongParam: AVeryLongTypeThatYouNeedToUse)
                                        (aThirdVeryLongParam: AVeryLongTypeThatYouNeedToUse)
                                        =
        // ... the body of the method follows
```

Dotyczy to również członków, konstruktorów i parametrów przy użyciu krotek:

```fsharp
type TM() =
    member _.LongMethodWithLotsOfParameters(aVeryLongParam: AVeryLongTypeThatYouNeedToUse,
                                            aSecondVeryLongParam: AVeryLongTypeThatYouNeedToUse,
                                            aThirdVeryLongParam: AVeryLongTypeThatYouNeedToUse) =
        // ... the body of the method

type TC(aVeryLongCtorParam: AVeryLongTypeThatYouNeedToUse,
        aSecondVeryLongCtorParam: AVeryLongTypeThatYouNeedToUse,
        aThirdVeryLongCtorParam: AVeryLongTypeThatYouNeedToUse) =
    // ... the body of the class follows
```

Jeśli parametry są currified lub określono jawną adnotację typu zwracanego, zaleca się umieszczenie `=` znaku w nowym wierszu:

```fsharp
type C() =
    member _.LongMethodWithLotsOfParameters(aVeryLongParam: AVeryLongTypeThatYouNeedToUse,
                                            aSecondVeryLongParam: AVeryLongTypeThatYouNeedToUse,
                                            aThirdVeryLongParam: AVeryLongTypeThatYouNeedToUse)
                                            : AReturnType =
        // ... the body of the method
    member _.LongMethodWithLotsOfCurrifiedParams(aVeryLongParam: AVeryLongTypeThatYouNeedToUse)
                                                (aSecondVeryLongParam: AVeryLongTypeThatYouNeedToUse)
                                                (aThirdVeryLongParam: AVeryLongTypeThatYouNeedToUse)
                                                =
        // ... the body of the method
```

Jest to sposób, aby uniknąć zbyt długich wierszy (w przypadku zwracany typ może mieć długą nazwę) i mieć mniej uszkodzeń liniowych podczas dodawania parametrów.

### <a name="type-annotations"></a>Adnotacje typu

#### <a name="right-pad-function-argument-type-annotations"></a>Adnotacje typu argumentów funkcji po prawej stronie

Podczas definiowania argumentów z adnotacjami typu, użyj odstępu po `:` symbolu:

```fsharp
// OK
let complexFunction (a: int) (b: int) c = a + b + c

// Bad
let complexFunctionBad (a :int) (b :int) (c:int) = a + b + c
```

#### <a name="surround-return-type-annotations-with-white-space"></a>Otocz adnotacje typu zwracanego z białym znakiem

W przypadku funkcji lub adnotacji typu wartości (typ zwracany w przypadku funkcji) Użyj odstępu przed i po `:` symbolu:

```fsharp
// OK
let expensiveToCompute : int = 0 // Type annotation for let-bound value
let myFun (a: decimal) b c : decimal = a + b + c // Type annotation for the return type of a function
// Bad
let expensiveToComputeBad1:int = 1
let expensiveToComputeBad2 :int = 2
let myFunBad (a: decimal) b c:decimal = a + b + c
```

## <a name="formatting-blank-lines"></a>Formatowanie pustych wierszy

* Rozdziel funkcję najwyższego poziomu i definicje klas z dwoma pustymi wierszami.
* Definicje metod wewnątrz klasy są oddzielone pojedynczym pustym wierszem.
* Dodatkowe puste wiersze mogą być używane (oszczędnie) do oddzielenia grup powiązanych funkcji. Puste wiersze można pominąć między zestawem powiązanych z jednym wierszem (na przykład zestawem implementacji fikcyjnej).
* Używaj pustych wierszy w funkcjach, oszczędnie, aby wskazać sekcje logiczne.

## <a name="formatting-comments"></a>Formatowanie komentarzy

Zwykle Preferuj wiele komentarzy o podwójnym ukośniku w komentarzach bloku w stylu ML.

```fsharp
// Prefer this style of comments when you want
// to express written ideas on multiple lines.

(*
    ML-style comments are fine, but not a .NET-ism.
    They are useful when needing to modify multi-line comments, though.
*)
```

Komentarze wbudowane powinny rozpoczynać się wielką literą.

```fsharp
let f x = x + 1 // Increment by one.
```

## <a name="naming-conventions"></a>Konwencje nazewnictwa

### <a name="use-camelcase-for-class-bound-expression-bound-and-pattern-bound-values-and-functions"></a>Użyj camelCase dla wartości powiązanych z klasą, powiązanych z wyrażeniami i funkcji, które są powiązane z wzorcem

Jest to typowy i zaakceptowany styl języka F # do używania camelCase dla wszystkich nazw związanych ze zmiennymi lokalnymi lub dopasowaniami wzorców i definicjami funkcji.

```fsharp
// OK
let addIAndJ i j = i + j

// Bad
let addIAndJ I J = I+J

// Bad
let AddIAndJ i j = i + j
```

W klasach należy również użyć funkcji camelCase.

```fsharp
type MyClass() =

    let doSomething () =

    let firstResult = ...

    let secondResult = ...

    member x.Result = doSomething()
```

### <a name="use-camelcase-for-module-bound-public-functions"></a>Użyj camelCase dla funkcji publicznych powiązanych z modułem

Gdy funkcja powiązana z modułem jest częścią publicznego interfejsu API, powinna używać camelCase:

```fsharp
module MyAPI =
    let publicFunctionOne param1 param2 param2 = ...

    let publicFunctionTwo param1 param2 param3 = ...
```

### <a name="use-camelcase-for-internal-and-private-module-bound-values-and-functions"></a>Używanie camelCase do wewnętrznych i prywatnych wartości i funkcji powiązanych z modułem

Użyj camelCase dla prywatnych wartości związanych z modułem, w tym następujących:

* Funkcje ad hoc w skryptach

* Wartości tworzące wewnętrzną implementację modułu lub typu

```fsharp
let emailMyBossTheLatestResults =
    ...
```

### <a name="use-camelcase-for-parameters"></a>Użyj camelCase dla parametrów

Wszystkie parametry powinny używać camelCase zgodnie z konwencjami nazewnictwa platformy .NET.

```fsharp
module MyModule =
    let myFunction paramOne paramTwo = ...

type MyClass() =
    member this.MyMethod(paramOne, paramTwo) = ...
```

### <a name="use-pascalcase-for-modules"></a>Korzystanie z PascalCase dla modułów

Wszystkie moduły (najwyższego poziomu, wewnętrzne, prywatne, zagnieżdżone) powinny używać PascalCase.

```fsharp
module MyTopLevelModule

module Helpers =
    module private SuperHelpers =
        ...

    ...
```

### <a name="use-pascalcase-for-type-declarations-members-and-labels"></a>Użyj PascalCase dla deklaracji typu, elementów członkowskich i etykiet

Klasy, interfejsy, struktury, wyliczenia, Delegaty, rekordy i związki rozłączne powinny mieć nazwę z PascalCase. Elementy członkowskie w typach i etykietach dla rekordów i Unii rozłącznych powinny również używać PascalCase.

```fsharp
type IMyInterface =
    abstract Something: int

type MyClass() =
    member this.MyMethod(x, y) = x + y

type MyRecord = { IntVal: int; StringVal: string }

type SchoolPerson =
    | Professor
    | Student
    | Advisor
    | Administrator
```

### <a name="use-pascalcase-for-constructs-intrinsic-to-net"></a>Użyj PascalCase dla konstrukcji wewnętrznych dla platformy .NET

Przestrzenie nazw, wyjątki, zdarzenia i projekty/ `.dll` nazwy powinny również używać PascalCase. Nie tylko robi to, że użycie z innych języków .NET jest bardziej naturalne dla użytkowników, jest również spójne z konwencjami nazewnictwa platformy .NET, które prawdopodobnie występują.

### <a name="avoid-underscores-in-names"></a>Unikaj podkreśleń w nazwach

Historycznie Niektóre biblioteki języka F # używały podkreśleń w nazwach. Nie jest to jednak już powszechnie akceptowane, częściowo ponieważ koliduje z konwencjami nazewnictwa platformy .NET. Tak samo, niektórzy programiści F # używają podkreśleń silnie, częściowo z przyczyn historycznych, a tolerancja i istotność są ważne. Jednak styl jest często odstosowany przez inne osoby, które mają możliwość wyboru, czy mają być używane.

Jeden wyjątek obejmuje współdziałanie ze składnikami macierzystymi, w których znaki podkreślenia są wspólne.

### <a name="use-standard-f-operators"></a>Użyj standardowych operatorów języka F #

Następujące operatory są zdefiniowane w standardowej bibliotece F # i powinny być używane zamiast definiować odpowiedniki. Przy użyciu tych operatorów zaleca się, aby kod był bardziej czytelny i idiomatyczne. Deweloperzy z tłem w OCaml lub innym języku programowania funkcjonalnego mogą być przyzwyczajoni do różnych idiomy. Poniższa lista zawiera podsumowanie zalecanych operatorów języka F #.

```fsharp
x |> f // Forward pipeline
f >> g // Forward composition
x |> ignore // Discard away a value
x + y // Overloaded addition (including string concatenation)
x - y // Overloaded subtraction
x * y // Overloaded multiplication
x / y // Overloaded division
x % y // Overloaded modulus
x && y // Lazy/short-cut "and"
x || y // Lazy/short-cut "or"
x <<< y // Bitwise left shift
x >>> y // Bitwise right shift
x ||| y // Bitwise or, also for working with “flags” enumeration
x &&& y // Bitwise and, also for working with “flags” enumeration
x ^^^ y // Bitwise xor, also for working with “flags” enumeration
```

### <a name="use-prefix-syntax-for-generics-foot-in-preference-to-postfix-syntax-t-foo"></a>Użyj składni prefiksu dla typów ogólnych ( `Foo<T>` ) w preferencjach do przyrostkowej składni ( `T Foo` )

F # dziedziczy styl przyrostka (na przykład), a `int list` także styl (na przykład `list<int>` ). Preferuj styl .NET, z wyjątkiem pięciu określonych typów:

1. Dla list języka F # Użyj przyrostkowej formy: `int list` zamiast `list<int>` .
2. W przypadku opcji języka F # należy użyć przyrostkowej formy: `int option` zamiast `option<int>` .
3. W przypadku opcji wartości języka F # Użyj przyrostkowej formy: `int voption` zamiast `voption<int>` .
4. W przypadku tablic języka F # należy użyć nazwy składni `int[]` zamiast `int array` lub `array<int>` .
5. W przypadku komórek referencyjnych Użyj `int ref` zamiast `ref<int>` lub `Ref<int>` .

Dla wszystkich innych typów Użyj formy prefiksu.

## <a name="formatting-tuples"></a>Formatowanie krotek

Tworzenie wystąpienia spójnej kolekcji musi być ujęte w nawiasy, a w tym przecinku należy następować pojedyncze miejsce, na przykład: `(1, 2)` , `(x, y, z)` .

Jest on powszechnie akceptowany w celu pomijania nawiasów we wzorcu dopasowania spójnych krotek:

```fsharp
let (x, y) = z // Destructuring
let x, y = z // OK

// OK
match x, y with
| 1, _ -> 0
| x, 1 -> 0
| x, y -> 1
```

Jest również często akceptowane do pomijania nawiasów, jeśli Krotka jest wartością zwracaną funkcji:

```fsharp
// OK
let update model msg =
    match msg with
    | 1 -> model + 1, []
    | _ -> model, [ msg ]
```

W obszarze Podsumowanie zaleca się Tworzenie wystąpień spójnych krotek, ale w przypadku używania krotek w celu dopasowania do wzorca lub wartości zwracanej jest on traktowany jako drobny, aby uniknąć nawiasów.

## <a name="formatting-discriminated-union-declarations"></a>Formatowanie deklaracji związku rozłącznych

Wcięcie `|` w definicji typu według czterech spacji:

```fsharp
// OK
type Volume =
    | Liter of float
    | FluidOunce of float
    | ImperialPint of float

// Not OK
type Volume =
| Liter of float
| USPint of float
| ImperialPint of float
```

## <a name="formatting-discriminated-unions"></a>Formatowanie związków rozłącznych

Utworzone przez siebie związki rozłączne, które dzielą się między wiele wierszy, powinny dawać zawarte dane nowe zakresy z wcięciem:

```fsharp
let tree1 =
    BinaryNode
        (BinaryNode(BinaryValue 1, BinaryValue 2),
         BinaryNode(BinaryValue 3, BinaryValue 4))
```

Nawias zamykający może również znajdować się w nowym wierszu:

```fsharp
let tree1 =
    BinaryNode(
        BinaryNode(BinaryValue 1, BinaryValue 2),
        BinaryNode(BinaryValue 3, BinaryValue 4)
    )
```

## <a name="formatting-record-declarations"></a>Formatowanie deklaracji rekordu

Zwiększ wcięcie `{` w definicji typu o cztery spacje i uruchom listę pól w tym samym wierszu:

```fsharp
// OK
type PostalAddress =
    { Address: string
      City: string
      Zip: string }
    member x.ZipAndCity = $"{x.Zip} {x.City}"

// Not OK
type PostalAddress =
  { Address: string
    City: string
    Zip: string }
    member x.ZipAndCity = $"{x.Zip} {x.City}"

// Unusual in F#
type PostalAddress =
    {
        Address: string
        City: string
        Zip: string
    }
```

Umieszczenie tokenu otwierającego w nowym wierszu, a token zamykający w nowym wierszu jest preferowany, Jeśli deklarujesz implementacje interfejsów lub składowe w rekordzie:

```fsharp
// Declaring additional members on PostalAddress
type PostalAddress =
    {
        Address: string
        City: string
        Zip: string
    }
    member x.ZipAndCity = $"{x.Zip} {x.City}"

type MyRecord =
    {
        SomeField: int
    }
    interface IMyInterface
```

## <a name="formatting-records"></a>Formatowanie rekordów

Krótkie rekordy można napisać w jednym wierszu:

```fsharp
let point = { X = 1.0; Y = 0.0 }
```

Rekordy, które są dłuższe, powinny używać nowych wierszy do etykiet:

```fsharp
let rainbow =
    { Boss = "Jeffrey"
      Lackeys = ["Zippy"; "George"; "Bungle"] }
```

Umieszczenie tokenu otwierającego w nowym wierszu, zawartości z zakładkami w jednym zakresie, a token zamykający w nowym wierszu jest preferowany, jeśli:

* Przenoszenie rekordów wokół kodu z różnymi zakresami wcięć
* Przeprzewody do funkcji

```fsharp
let rainbow =
    {
        Boss1 = "Jeffrey"
        Boss2 = "Jeffrey"
        Boss3 = "Jeffrey"
        Boss4 = "Jeffrey"
        Boss5 = "Jeffrey"
        Boss6 = "Jeffrey"
        Boss7 = "Jeffrey"
        Boss8 = "Jeffrey"
        Lackeys = ["Zippy"; "George"; "Bungle"]
    }

type MyRecord =
    {
        SomeField: int
    }
    interface IMyInterface

let foo a =
    a
    |> Option.map (fun x ->
        {
            MyField = x
        })
```

Te same reguły dotyczą elementów list i tablic.

## <a name="formatting-copy-and-update-record-expressions"></a>Formatowanie wyrażeń kopiowania i aktualizacji

Wyrażenie rekordu kopiowania i aktualizacji jest nadal rekordem, więc stosuje się do nich podobne wskazówki.

Krótkie wyrażenia mogą zmieścić się w jednym wierszu:

```fsharp
let point2 = { point with X = 1; Y = 2 }
```

Dłuższe wyrażenia powinny używać nowych wierszy:

```fsharp
let rainbow2 =
    { rainbow with
        Boss = "Jeffrey"
        Lackeys = [ "Zippy"; "George"; "Bungle" ] }
```

Podobnie jak w przypadku wskazówek dotyczących rekordu, możesz chcieć oddzielić osobne wiersze dla nawiasów klamrowych i wciąć jeden zakres z prawej strony wyrażenia. W niektórych specjalnych przypadkach, takich jak Zawijanie wartości z opcjonalną bez nawiasów, może być konieczne pozostawienie nawiasu klamrowego w jednej linii:

```fsharp
type S = { F1: int; F2: string }
type State = { F:  S option }

let state = { F = Some { F1 = 1; F2 = "Hello" } }
let newState =
    {
        state with
            F = Some {
                    F1 = 0
                    F2 = ""
                }
    }
```

## <a name="formatting-lists-and-arrays"></a>Formatowanie list i tablic

Pisz `x :: l` ze spacjami wokół `::` operatora ( `::` jest operatorem wrostkowe, dlatego jest ujęty w spacje).

Lista i tablice zadeklarowane w jednym wierszu powinny zawierać spację po nawiasie otwierającym i przed nawiasem zamykającym:

```fsharp
let xs = [ 1; 2; 3 ]
let ys = [| 1; 2; 3; |]
```

Zawsze używaj co najmniej jednego miejsca między dwoma odrębnymi operatorami w nawiasach klamrowych. Na przykład pozostaw spację między a `[` i `{` .

```fsharp
// OK
[ { IngredientName = "Green beans"; Quantity = 250 }
  { IngredientName = "Pine nuts"; Quantity = 250 }
  { IngredientName = "Feta cheese"; Quantity = 250 }
  { IngredientName = "Olive oil"; Quantity = 10 }
  { IngredientName = "Lemon"; Quantity = 1 } ]

// Not OK
[{ IngredientName = "Green beans"; Quantity = 250 }
 { IngredientName = "Pine nuts"; Quantity = 250 }
 { IngredientName = "Feta cheese"; Quantity = 250 }
 { IngredientName = "Olive oil"; Quantity = 10 }
 { IngredientName = "Lemon"; Quantity = 1 }]
```

Te same wytyczne dotyczą list lub tablic krotek.

Listy i tablice, które dzielą się między wiele wierszy, są zgodne z podobną regułą jako rekordy:

```fsharp
let pascalsTriangle =
    [|
        [| 1 |]
        [| 1; 1 |]
        [| 1; 2; 1 |]
        [| 1; 3; 3; 1 |]
        [| 1; 4; 6; 4; 1 |]
        [| 1; 5; 10; 10; 5; 1 |]
        [| 1; 6; 15; 20; 15; 6; 1 |]
        [| 1; 7; 21; 35; 35; 21; 7; 1 |]
        [| 1; 8; 28; 56; 70; 56; 28; 8; 1 |]
    |]
```

Podobnie jak w przypadku rekordów, deklarowanie otwierających i zamykających nawiasów w osobnym wierszu spowoduje, że przenoszenie kodu i potoki do funkcji są łatwiejsze.

Podczas tworzenia tablic i list programistycznych należy preferować, `->` `do ... yield` gdy wartość jest zawsze generowana:

```fsharp
// Preferred
let squares = [ for x in 1..10 -> x * x ]

// Not preferred
let squares' = [ for x in 1..10 do yield x * x ]
```

W przypadku starszych wersji języka F # wymagane jest określenie `yield` w sytuacjach, w których dane mogą być generowane warunkowo lub mogą być oceniane kolejne wyrażenia. Wolisz pominąć te `yield` słowa kluczowe, chyba że musisz skompilować przy użyciu starszej wersji języka F #:

```fsharp
// Preferred
let daysOfWeek includeWeekend =
    [
        "Monday"
        "Tuesday"
        "Wednesday"
        "Thursday"
        "Friday"
        if includeWeekend then
            "Saturday"
            "Sunday"
    ]

// Not preferred
let daysOfWeek' includeWeekend =
    [
        yield "Monday"
        yield "Tuesday"
        yield "Wednesday"
        yield "Thursday"
        yield "Friday"
        if includeWeekend then
            yield "Saturday"
            yield "Sunday"
    ]
```

W niektórych przypadkach `do...yield` może pomóc w czytelności. Te przypadki, chociaż należy rozważyć, powinny być brane pod uwagę.

## <a name="formatting-if-expressions"></a>Formatowanie wyrażeń if

Wcięcia warunkowe są zależne od wielkości i złożoności wyrażeń, które je tworzą.
Zapisz je w jednym wierszu, gdy:

- `cond`, `e1` , i `e2` są krótkie
- `e1` i `e2` nie są `if/then/else` wyrażeniami.

```fsharp
if cond then e1 else e2
```

Jeśli dowolne wyrażenie ma wiele wierszy lub `if/then/else` wyrażeń.

```fsharp
if cond then
    e1
else
    e2
```

Wiele warunkowych z `elif` i `else` jest wciętym w tym samym zakresie co `if` gdy są one zgodne z regułami jednego wiersza `if/then/else` wyrażeń.

```fsharp
if cond1 then e1
elif cond2 then e2
elif cond3 then e3
else e4
```

Jeśli którykolwiek z warunków lub wyrażeń ma wiele wierszy, całe `if/then/else` wyrażenie jest wielowierszowe:

```fsharp
if cond1 then
    e1
elif cond2 then
    e2
elif cond3 then
    e3
else
    e4
```

### <a name="pattern-matching-constructs"></a>Konstrukcje dopasowania wzorca

Użyj `|` dla każdej klauzuli dopasowania bez wcięcia. Jeśli wyrażenie jest krótkie, można rozważyć użycie pojedynczej linii, jeśli każde Podwyrażenie jest również proste.

```fsharp
// OK
match l with
| { him = x; her = "Posh" } :: tail -> x
| _ :: tail -> findDavid tail
| [] -> failwith "Couldn't find David"

// Not OK
match l with
    | { him = x; her = "Posh" } :: tail -> x
    | _ :: tail -> findDavid tail
    | [] -> failwith "Couldn't find David"
```

Jeśli wyrażenie po prawej stronie strzałki dopasowania do wzorca jest zbyt duże, przenieś je do poniższego wiersza, z wcięciem jeden krok z `match` / `|` .

```fsharp
match lam with
| Var v -> 1
| Abs(x, body) ->
    1 + sizeLambda body
| App(lam1, lam2) ->
    sizeLambda lam1 + sizeLambda lam2

```

Dopasowanie wzorców funkcji anonimowych, zaczynające `function` się od, nie powinno być zwykle zbyt dalekie. Na przykład wcięcie jednego z zakresów w następujący sposób jest następujące:

```fsharp
lambdaList
|> List.map (function
    | Abs(x, body) -> 1 + sizeLambda 0 body
    | App(lam1, lam2) -> sizeLambda (sizeLambda 0 lam1) lam2
    | Var v -> 1)
```

Dopasowanie wzorca w funkcjach zdefiniowanych przez `let` lub `let rec` powinno mieć wcięcia cztery spacje po uruchomieniu `let` , nawet jeśli `function` jest używane słowo kluczowe:

```fsharp
let rec sizeLambda acc = function
    | Abs(x, body) -> sizeLambda (succ acc) body
    | App(lam1, lam2) -> sizeLambda (sizeLambda acc lam1) lam2
    | Var v -> succ acc
```

Nie zaleca się wyrównywania strzałek.

## <a name="formatting-trywith-expressions"></a>Formatowanie wyrażeń try/with

Dopasowanie wzorca dla typu wyjątku powinno być wcięte na tym samym poziomie co `with` .

```fsharp
try
    if System.DateTime.Now.Second % 3 = 0 then
        raise (new System.Exception())
    else
        raise (new System.ApplicationException())
with
| :? System.ApplicationException ->
    printfn "A second that was not a multiple of 3"
| _ ->
    printfn "A second that was a multiple of 3"
```

## <a name="formatting-function-parameter-application"></a>Formatowanie aplikacji parametrów funkcji

Ogólnie rzecz biorąc, większość aplikacji parametrów funkcji jest wykonywana w tym samym wierszu.

Jeśli chcesz zastosować parametry do funkcji w nowym wierszu, Zwiększ wcięcie według jednego zakresu.

```fsharp
// OK
sprintf "\t%s - %i\n\r"
     x.IngredientName x.Quantity

// OK
sprintf
     "\t%s - %i\n\r"
     x.IngredientName x.Quantity

// OK
let printVolumes x =
    printf "Volume in liters = %f, in us pints = %f, in imperial = %f"
        (convertVolumeToLiter x)
        (convertVolumeUSPint x)
        (convertVolumeImperialPint x)
```

Te same wskazówki dotyczą wyrażeń lambda jako argumentów funkcji. Jeśli treść wyrażenia lambda, treść może mieć inny wiersz, wcięcie według jednego zakresu

```fsharp
let printListWithOffset a list1 =
    List.iter
        (fun elem -> printfn $"%d{a + elem}")
        list1

// OK if lambda body is long enough
let printListWithOffset a list1 =
    List.iter
        (fun elem ->
            printfn $"%d{a + elem}")
        list1
```

Jednakże jeśli treść wyrażenia lambda ma więcej niż jeden wiersz, Rozważ umieszczenie go w osobnej funkcji, a nie ma zastosowania jednowierszowej konstrukcji jako pojedynczego argumentu do funkcji.

### <a name="formatting-infix-operators"></a>Formatowanie operatorów wrostkowe

Oddziel operatory spacjami. Oczywiste wyjątki od tej reguły to `!` Operatory i `.` .

Wyrażenia wrostkowe są prawidłowe dla zestawień w tej samej kolumnie:

```fsharp
acc +
(sprintf "\t%s - %i\n\r"
     x.IngredientName x.Quantity)

let function1 arg1 arg2 arg3 arg4 =
    arg1 + arg2 +
    arg3 + arg4
```

### <a name="formatting-pipeline-operators"></a>Formatowanie operatorów potoku

Operatory potoku `|>` powinny się znaleźć pod wyrażeniami, w których działają.

```fsharp
// Preferred approach
let methods2 =
    System.AppDomain.CurrentDomain.GetAssemblies()
    |> List.ofArray
    |> List.map (fun assm -> assm.GetTypes())
    |> Array.concat
    |> List.ofArray
    |> List.map (fun t -> t.GetMethods())
    |> Array.concat

// Not OK
let methods2 = System.AppDomain.CurrentDomain.GetAssemblies()
            |> List.ofArray
            |> List.map (fun assm -> assm.GetTypes())
            |> Array.concat
            |> List.ofArray
            |> List.map (fun t -> t.GetMethods())
            |> Array.concat
```

### <a name="formatting-modules"></a>Formatowanie modułów

Dla kodu w module lokalnym należy zastosować wcięcie względem modułu, ale nie ma wcięcia kodu w module najwyższego poziomu. Elementy przestrzeni nazw nie muszą mieć wcięcia.

```fsharp
// A is a top-level module.
module A

let function1 a b = a - b * b
```

```fsharp
// A1 and A2 are local modules.
module A1 =
    let function1 a b = a * a + b * b

module A2 =
    let function2 a b = a * a - b * b
```

### <a name="formatting-object-expressions-and-interfaces"></a>Formatowanie wyrażeń i interfejsów obiektów

Wyrażenia i interfejsy obiektów powinny być wyrównane w taki sam sposób, jak w przypadku `member` wcięć z czterech spacji.

```fsharp
let comparer =
    { new IComparer<string> with
          member x.Compare(s1, s2) =
              let rev (s: String) =
                  new String (Array.rev (s.ToCharArray()))
              let reversed = rev s1
              reversed.CompareTo (rev s2) }
```

### <a name="formatting-white-space-in-expressions"></a>Formatowanie białych znaków w wyrażeniach

Unikaj nadmiarowego odstępu w wyrażeniach języka F #.

```fsharp
// OK
spam (ham.[1])

// Not OK
spam ( ham.[ 1 ] )
```

Argumenty nazwane nie mogą również zawierać spacji otaczających `=` :

```fsharp
// OK
let makeStreamReader x = new System.IO.StreamReader(path=x)

// Not OK
let makeStreamReader x = new System.IO.StreamReader(path = x)
```

### <a name="formatting-constructors-static-members-and-member-invocations"></a>Konstruktory formatowania, statyczne elementy członkowskie i wywołania elementów członkowskich

Jeśli wyrażenie jest krótkie, należy oddzielić argumenty spacjami i zachować je w jednym wierszu.

```fsharp
let person = new Person(a1, a2)

let myRegexMatch = Regex.Match(input, regex)

let untypedRes = checker.ParseFile(file, source, opts)
```

Jeśli wyrażenie jest długie, Użyj nowego wiersza i wcięcie jednego zakresu, a nie wcięcia w nawiasie.

```fsharp
let person =
    new Person(
        argument1,
        argument2
    )

let myRegexMatch =
    Regex.Match(
        "my longer input string with some interesting content in it",
        "myRegexPattern"
    )

let untypedRes =
    checker.ParseFile(
        fileName,
        sourceText,
        parsingOptionsWithDefines
    )
```

## <a name="formatting-attributes"></a>Formatowanie atrybutów

[Atrybuty](../language-reference/attributes.md) są umieszczane powyżej konstrukcji:

```fsharp
[<SomeAttribute>]
type MyClass() = ...

[<RequireQualifiedAccess>]
module M =
    let f x = x

[<Struct>]
type MyRecord =
    { Label1: int
      Label2: string }
```

Powinny one przejść po dowolnych dokumentach XML:

```fsharp
/// Module with some things in it.
[<RequireQualifiedAccess>]
module M =
    let f x = x
```

### <a name="formatting-attributes-on-parameters"></a>Formatowanie atrybutów dla parametrów

Atrybuty mogą być również umieszczane w parametrach. W takim przypadku należy umieścić w tym samym wierszu co parametr i przed nazwą:

```fsharp
// Defines a class that takes an optional value as input defaulting to false.
type C() =
    member _.M([<Optional; DefaultParameterValue(false)>] doSomething: bool)
```

### <a name="formatting-multiple-attributes"></a>Formatowanie wielu atrybutów

W przypadku zastosowania wielu atrybutów do konstrukcji, która nie jest parametrem, powinny one zostać umieszczone w taki sposób, że istnieje jeden atrybut na wiersz:

```fsharp
[<Struct>]
[<IsByRefLike>]
type MyRecord =
    { Label1: int
      Label2: string }
```

Gdy zastosowano do parametru, muszą one znajdować się w tym samym wierszu i oddzielić `;` separatorem.

## <a name="formatting-literals"></a>Literały formatowania

[Literały F #](../language-reference/literals.md) używające `Literal` atrybutu powinny umieścić atrybut w osobnym wierszu i używać PascalCase nazw:

```fsharp
[<Literal>]
let Path = __SOURCE_DIRECTORY__ + "/" + __SOURCE_FILE__

[<Literal>]
let MyUrl = "www.mywebsitethatiamworkingwith.com"
```

Należy unikać umieszczania atrybutu w tym samym wierszu, w którym znajduje się wartość.

## <a name="formatting-computation-expression-operations"></a>Formatowanie operacji wyrażenia obliczeń

Podczas tworzenia niestandardowych operacji dla [wyrażeń obliczeniowych](../language-reference/computation-expressions.md)zaleca się używanie nazw CamelCase:

```fsharp
type MathBuilder () =
    member _.Yield _ = 0

    [<CustomOperation("addOne")>]
    member _.AddOne (state: int) =
        state + 1

    [<CustomOperation("subtractOne")>]
    member _.SubtractOne (state: int) =
        state - 1

    [<CustomOperation("divideBy")>]
    member _.DivideBy (state: int, divisor: int) =
        state / divisor

    [<CustomOperation("multiplyBy")>]
    member _.MultiplyBy (state: int, factor: int) =
        state * factor

let math = MathBuilder()

// 10
let myNumber =
    math {
        addOne
        addOne
        addOne

        subtractOne

        divideBy 2

        multiplyBy 10
    }
```

Domena, która jest modelowana powinna ostatecznie określać konwencję nazewnictwa.
Jeśli idiomatyczne użyć innej konwencji, należy zamiast niej użyć tej Konwencji.
