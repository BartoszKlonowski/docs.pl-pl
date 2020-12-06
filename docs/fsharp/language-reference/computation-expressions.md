---
title: Wyrażenia obliczeń
description: 'Dowiedz się, jak utworzyć wygodną składnię do pisania obliczeń w języku F #, które mogą być sekwencyjne i połączone przy użyciu konstrukcji przepływu sterowania i powiązań.'
ms.date: 08/15/2020
f1_keywords:
- let!_FS
ms.openlocfilehash: a0a71533ea1bc87b75f028ad0d416326f627672a
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96739310"
---
# <a name="computation-expressions"></a>Wyrażenia obliczeń

Wyrażenia obliczeń w języku F # zapewniają wygodną składnię do pisania obliczeń, które mogą być sekwencjonowane i łączone przy użyciu konstrukcji przepływu sterowania i powiązań. W zależności od rodzaju wyrażenia obliczeń można traktować ich jako metodę wyrażania monads, monoids, Monad i applicative funktory. Jednak, w przeciwieństwie do innych języków ( *takich jak Haskell* ), nie są one powiązane z pojedynczym abstrakcją i nie polegają na makrach ani innych formach programowania, aby osiągnąć wygodną i zależną od kontekstu składnię.

## <a name="overview"></a>Omówienie

Obliczenia mogą mieć wiele form. Najbardziej powszechną formą obliczeń jest wykonywanie jednowątkowe, które można łatwo zrozumieć i zmodyfikować. Jednak nie wszystkie formy obliczeń są tak proste jak wykonywanie jednowątkowe. Oto niektóre przykłady:

- Obliczenia niedeterministyczne
- Obliczenia asynchroniczne
- Wpływ obliczeń
- Obliczenia dotyczące przetworzenia

Ogólnie rzecz biorąc, istnieją operacje obliczeniowe *zależne od kontekstu* , które należy wykonać w niektórych częściach aplikacji. Pisanie kodu wrażliwego na kontekst może być trudne, ponieważ jest to łatwe w obsłudze obliczenia poza danym kontekstem bez abstrakcji, aby zapobiec temu. Te streszczenia są często trudne do napisania przez siebie, co oznacza, że F # ma uogólniony sposób, nazywany **wyrażeniami obliczeń**.

Wyrażenia obliczeń oferują ujednoliconą składnię i abstrakcyjny model dla obliczeń z uwzględnieniem kontekstu.

Każde wyrażenie obliczeniowe jest obsługiwane przez typ *konstruktora* . Typ konstruktora definiuje operacje, które są dostępne dla wyrażenia obliczeń. Zobacz [Tworzenie nowego typu wyrażenia obliczeń](computation-expressions.md#creating-a-new-type-of-computation-expression), które pokazuje, jak utworzyć niestandardowe wyrażenie obliczeniowe.

### <a name="syntax-overview"></a>Omówienie składni

Wszystkie wyrażenia obliczeń mają następującą postać:

```fsharp
builder-expr { cexper }
```

gdzie `builder-expr` jest nazwą typu konstruktora, który definiuje wyrażenie obliczeń, i `cexper` jest treścią wyrażenia obliczenia. Na przykład `async` kod wyrażenia obliczenia może wyglądać następująco:

```fsharp
let fetchAndDownload url =
    async {
        let! data = downloadData url

        let processedData = processData data

        return processedData
    }
```

W wyrażeniu obliczenia jest dostępna specjalna, dodatkowa składnia, jak pokazano w poprzednim przykładzie. Wyrażenia obliczeń umożliwiają następujące formy wyrażeń:

```fsharp
expr { let! ... }
expr { do! ... }
expr { yield ... }
expr { yield! ... }
expr { return ... }
expr { return! ... }
expr { match! ... }
```

Każdy z tych słów kluczowych i inne standardowe słowa kluczowe F # są dostępne tylko w wyrażeniu obliczeń, jeśli zostały zdefiniowane w typie konstruktora zapasowego. Jedynym wyjątkiem jest `match!` , który jest samym cukrem składniowym do użycia, po którym `let!` następuje dopasowanie wzorca w wyniku.

Typ konstruktora jest obiektem, który definiuje specjalne metody, które regulują sposób łączenia fragmentów wyrażenia obliczeń; oznacza to, że metody określają zachowanie wyrażenia obliczeń. Innym sposobem opisywania klasy konstruktora jest to, że umożliwia dostosowanie operacji wielu konstrukcji języka F #, takich jak pętle i powiązania.

### `let!`

`let!`Słowo kluczowe wiąże wynik wywołania innego wyrażenia obliczenia do nazwy:

```fsharp
let doThingsAsync url =
    async {
        let! data = getDataAsync url
        ...
    }
```

W przypadku powiązania wywołania z wyrażeniem obliczeniowym z `let` , wynik wyrażenia obliczeń nie zostanie pobrany. Zamiast tego nastąpi powiązanie wartości *niezrealizowanego* wywołania tego wyrażenia obliczeń. Użyj `let!` , aby powiązać z wynikiem.

`let!` jest definiowana przez `Bind(x, f)` element członkowski w typie konstruktora.

### `do!`

`do!`Słowo kluczowe jest przeznaczone do wywoływania wyrażenia obliczeń, które zwraca `unit` Typ podobny (zdefiniowany przez `Zero` element członkowski w konstruktorze):

```fsharp
let doThingsAsync data url =
    async {
        do! submitData data url
        ...
    }
```

W przypadku [asynchronicznego przepływu pracy](asynchronous-workflows.md)ten typ to `Async<unit>` . W przypadku innych wyrażeń obliczeniowych typ jest prawdopodobnie `CExpType<unit>` .

`do!` jest definiowana przez `Bind(x, f)` element członkowski typu konstruktora, gdzie `f` tworzy `unit` .

### `yield`

`yield`Słowo kluczowe jest przeznaczone do zwracania wartości z wyrażenia obliczeń, aby można było go użyć jako <xref:System.Collections.Generic.IEnumerable%601> :

```fsharp
let squares =
    seq {
        for i in 1..10 do
            yield i * i
    }

for sq in squares do
    printfn $"%d{sq}"
```

W większości przypadków może być pominięty przez wywołujących. Najbardziej typowym sposobem, aby pominąć `yield` , jest `->` operator:

```fsharp
let squares =
    seq {
        for i in 1..10 -> i * i
    }

for sq in squares do
    printfn $"%d{sq}"
```

W przypadku bardziej złożonych wyrażeń, które mogą zwracać wiele różnych wartości i może być warunkowo, można po prostu pominąć słowo kluczowe:

```fsharp
let weekdays includeWeekend =
    seq {
        "Monday"
        "Tuesday"
        "Wednesday"
        "Thursday"
        "Friday"
        if includeWeekend then
            "Saturday"
            "Sunday"
    }
```

Podobnie jak w przypadku [słowa kluczowego Yield w języku C#](../../csharp/language-reference/keywords/yield.md), każdy element w wyrażeniu obliczenia jest obliczany w miarę powtarzania.

`yield` jest definiowana przez element `Yield(x)` członkowski typu konstruktora, gdzie `x` jest elementem, który ma zostać przywrócony.

### `yield!`

`yield!`Słowo kluczowe służy do spłaszczania kolekcji wartości z wyrażenia obliczeń:

```fsharp
let squares =
    seq {
        for i in 1..3 -> i * i
    }

let cubes =
    seq {
        for i in 1..3 -> i * i * i
    }

let squaresAndCubes =
    seq {
        yield! squares
        yield! cubes
    }

printfn $"{squaresAndCubes}"  // Prints - 1; 4; 9; 1; 8; 27
```

Podczas oceniania wyrażenie obliczeniowe wywoływane przez `yield!` będzie miało swoje elementy po jednym z nich, spłaszczony wynik.

`yield!` jest definiowana przez `YieldFrom(x)` element członkowski typu konstruktora, gdzie `x` jest kolekcją wartości.

W przeciwieństwie do `yield` , `yield!` musi być jawnie określona. Zachowanie nie jest niejawne w wyrażeniach obliczeniowych.

### `return`

`return`Słowo kluczowe otacza wartość w typie odpowiadającym wyrażeniu obliczenia. Poza wyrażeniami obliczeń używając `yield` , jest używany do "ukończenia" wyrażenia obliczeń:

```fsharp
let req = // 'req' is of type 'Async<data>'
    async {
        let! data = fetch url
        return data
    }

// 'result' is of type 'data'
let result = Async.RunSynchronously req
```

`return` jest definiowana przez element `Return(x)` członkowski typu konstruktora, gdzie jest elementem, który ma `x` być zawijany.

### `return!`

`return!`Słowo kluczowe realizuje wartość wyrażenia obliczeń i zawija ten wynik w typie odpowiadającym wyrażeniu obliczeń:

```fsharp
let req = // 'req' is of type 'Async<data>'
    async {
        return! fetch url
    }

// 'result' is of type 'data'
let result = Async.RunSynchronously req
```

`return!` jest definiowana przez `ReturnFrom(x)` element członkowski typu konstruktora, gdzie `x` jest innym wyrażeniem obliczeniowym.

### `match!`

`match!`Słowo kluczowe umożliwia wbudowanie wywołanie innego wyrażenia obliczenia i dopasowania do wzorca w wyniku:

```fsharp
let doThingsAsync url =
    async {
        match! callService url with
        | Some data -> ...
        | None -> ...
    }
```

Podczas wywoływania wyrażenia obliczeń za pomocą `match!` , będzie on wyglądał wynik wywołania `let!` . Jest to często używane podczas wywoływania wyrażenia obliczeń, gdzie wynik jest [opcjonalny](options.md).

## <a name="built-in-computation-expressions"></a>Wbudowane wyrażenia obliczeń

Biblioteka podstawowa F # definiuje trzy wbudowane wyrażenia obliczeń: [wyrażenia sekwencji](sequences.md), [asynchroniczne przepływy pracy](asynchronous-workflows.md)i [wyrażenia zapytań](query-expressions.md).

## <a name="creating-a-new-type-of-computation-expression"></a>Tworzenie nowego typu wyrażenia obliczeń

Można zdefiniować charakterystykę własnych wyrażeń obliczeniowych, tworząc klasę konstruktora i definiując niektóre specjalne metody klasy. Klasa konstruktora może opcjonalnie definiować metody wymienione w poniższej tabeli.

W poniższej tabeli opisano metody, których można użyć w klasie Konstruktor przepływu pracy.

|**Metoda**|**Typowe sygnatury**|**Opis**|
|----|----|----|
|`Bind`|`M<'T> * ('T -> M<'U>) -> M<'U>`|Wywoływana dla `let!` i `do!` w wyrażeniach obliczeniowych.|
|`Delay`|`(unit -> M<'T>) -> M<'T>`|Zawija wyrażenie obliczeń jako funkcję.|
|`Return`|`'T -> M<'T>`|Wywoływana dla `return` wyrażeń obliczeniowych.|
|`ReturnFrom`|`M<'T> -> M<'T>`|Wywoływana dla `return!` wyrażeń obliczeniowych.|
|`Run`|`M<'T> -> M<'T>` lub<br /><br />`M<'T> -> 'T`|Wykonuje wyrażenie obliczeniowe.|
|`Combine`|`M<'T> * M<'T> -> M<'T>` lub<br /><br />`M<unit> * M<'T> -> M<'T>`|Wywoływana dla sekwencjonowania w wyrażeniach obliczeń.|
|`For`|`seq<'T> * ('T -> M<'U>) -> M<'U>` lub<br /><br />`seq<'T> * ('T -> M<'U>) -> seq<M<'U>>`|Wywołuje `for...do` się dla wyrażeń w wyrażeniach obliczeń.|
|`TryFinally`|`M<'T> * (unit -> unit) -> M<'T>`|Wywołuje `try...finally` się dla wyrażeń w wyrażeniach obliczeń.|
|`TryWith`|`M<'T> * (exn -> M<'T>) -> M<'T>`|Wywołuje `try...with` się dla wyrażeń w wyrażeniach obliczeń.|
|`Using`|`'T * ('T -> M<'U>) -> M<'U> when 'T :> IDisposable`|Wywoływana dla `use` powiązań w wyrażeniach obliczeń.|
|`While`|`(unit -> bool) * M<'T> -> M<'T>`|Wywołuje `while...do` się dla wyrażeń w wyrażeniach obliczeń.|
|`Yield`|`'T -> M<'T>`|Wywołuje `yield` się dla wyrażeń w wyrażeniach obliczeń.|
|`YieldFrom`|`M<'T> -> M<'T>`|Wywołuje `yield!` się dla wyrażeń w wyrażeniach obliczeń.|
|`Zero`|`unit -> M<'T>`|Wywoływana dla pustych `else` gałęzi `if...then` wyrażeń w wyrażeniach obliczeniowych.|
|`Quote`|`Quotations.Expr<'T> -> Quotations.Expr<'T>`|Wskazuje, że wyrażenie obliczenia jest przesyłane do `Run` elementu członkowskiego jako cytat. Tłumaczy wszystkie wystąpienia obliczeń na cytat.|

Wiele metod w klasie konstruktora używa i zwraca `M<'T>` konstrukcję, która jest zazwyczaj odrębnie zdefiniowany typ, który charakteryzuje rodzaj obliczeń, na przykład `Async<'T>` dla asynchronicznych przepływów pracy i `Seq<'T>` dla przepływów pracy sekwencji. Sygnatury tych metod umożliwiają ich łączenie i zagnieżdżanie ze sobą, aby obiekt przepływu pracy zwrócony z jednej konstrukcji mógł zostać przekazana do następnego. Kompilator, gdy analizuje wyrażenie obliczeń, konwertuje wyrażenie na serię wywołań funkcji zagnieżdżonych przy użyciu metod w powyższej tabeli i kodu w wyrażeniu obliczeniowym.

Wyrażenie zagnieżdżone ma następującą postać:

```fsharp
builder.Run(builder.Delay(fun () -> {| cexpr |}))
```

W powyższym kodzie wywołania do `Run` i `Delay` są pomijane, jeśli nie są zdefiniowane w klasie konstruktora wyrażeń obliczeniowych. Treść wyrażenia obliczeń, w tym miejscu `{| cexpr |}` , jest tłumaczona na wywołania obejmujące metody klasy konstruktora przez tłumaczenia opisane w poniższej tabeli. Wyrażenie obliczeniowe `{| cexpr |}` jest zdefiniowane cyklicznie zgodnie z tymi tłumaczeniami `expr` , gdzie jest wyrażeniem języka F # i `cexpr` jest wyrażeniem obliczeniowym.

|Wyrażenie|Tłumaczenie|
|----------|-----------|
|<code>{ let binding in cexpr }</code>|<code>let binding in {&#124; cexpr &#124;}</code>|
|<code>{ let! pattern = expr in cexpr }</code>|<code>builder.Bind(expr, (fun pattern -> {&#124; cexpr &#124;}))</code>|
|<code>{ do! expr in cexpr }</code>|<code>builder.Bind(expr, (fun () -> {&#124; cexpr &#124;}))</code>|
|<code>{ yield expr }</code>|`builder.Yield(expr)`|
|<code>{ yield! expr }</code>|`builder.YieldFrom(expr)`|
|<code>{ return expr }</code>|`builder.Return(expr)`|
|<code>{ return! expr }</code>|`builder.ReturnFrom(expr)`|
|<code>{ use pattern = expr in cexpr }</code>|<code>builder.Using(expr, (fun pattern -> {&#124; cexpr &#124;}))</code>|
|<code>{ use! value = expr in cexpr }</code>|<code>builder.Bind(expr, (fun value -> builder.Using(value, (fun value -> { cexpr }))))</code>|
|<code>{ if expr then cexpr0 &#124;}</code>|<code>if expr then { cexpr0 } else builder.Zero()</code>|
|<code>{ if expr then cexpr0 else cexpr1 &#124;}</code>|<code>if expr then { cexpr0 } else { cexpr1 }</code>|
|<code>{ match expr with &#124; pattern_i -> cexpr_i }</code>|<code>match expr with &#124; pattern_i -> { cexpr_i }</code>|
|<code>{ for pattern in expr do cexpr }</code>|<code>builder.For(enumeration, (fun pattern -> { cexpr }))</code>|
|<code>{ for identifier = expr1 to expr2 do cexpr }</code>|<code>builder.For(enumeration, (fun identifier -> { cexpr }))</code>|
|<code>{ while expr do cexpr }</code>|<code>builder.While(fun () -> expr, builder.Delay({ cexpr }))</code>|
|<code>{ try cexpr with &#124; pattern_i -> expr_i }</code>|<code>builder.TryWith(builder.Delay({ cexpr }), (fun value -> match value with &#124; pattern_i -> expr_i &#124; exn -> reraise exn)))</code>|
|<code>{ try cexpr finally expr }</code>|<code>builder.TryFinally(builder.Delay( { cexpr }), (fun () -> expr))</code>|
|<code>{ cexpr1; cexpr2 }</code>|<code>builder.Combine({ cexpr1 }, { cexpr2 })</code>|
|<code>{ other-expr; cexpr }</code>|<code>expr; { cexpr }</code>|
|<code>{ other-expr }</code>|`expr; builder.Zero()`|

W poprzedniej tabeli `other-expr` zawiera opis wyrażenia, które nie jest wymienione w innej tabeli. Klasa konstruktora nie musi implementować wszystkich metod i obsługiwać wszystkich tłumaczeń wymienionych w poprzedniej tabeli. Te konstrukcje, które nie są zaimplementowane, nie są dostępne w wyrażeniach obliczeń tego typu. Na przykład, jeśli nie chcesz obsługiwać `use` słowa kluczowego w wyrażeniach obliczeń, możesz pominąć definicję `Use` w klasie konstruktora.

Poniższy przykład kodu pokazuje wyrażenie obliczeniowe, które hermetyzuje obliczenia jako serię kroków, które można ocenić jeden krok w danym momencie. Typ Unii rozłącznej, `OkOrException` , koduje stan błędu wyrażenia jako obliczone do tej pory. Ten kod ilustruje kilka typowych wzorców, których można użyć w wyrażeniach obliczeń, takich jak implementacje standardowe niektórych metod konstruktora.

```fsharp
// Computations that can be run step by step
type Eventually<'T> =
    | Done of 'T
    | NotYetDone of (unit -> Eventually<'T>)

module Eventually =
    // The bind for the computations. Append 'func' to the
    // computation.
    let rec bind func expr =
        match expr with
        | Done value -> func value
        | NotYetDone work -> NotYetDone (fun () -> bind func (work()))

    // Return the final value wrapped in the Eventually type.
    let result value = Done value

    type OkOrException<'T> =
        | Ok of 'T
        | Exception of System.Exception

    // The catch for the computations. Stitch try/with throughout
    // the computation, and return the overall result as an OkOrException.
    let rec catch expr =
        match expr with
        | Done value -> result (Ok value)
        | NotYetDone work ->
            NotYetDone (fun () ->
                let res = try Ok(work()) with | exn -> Exception exn
                match res with
                | Ok cont -> catch cont // note, a tailcall
                | Exception exn -> result (Exception exn))

    // The delay operator.
    let delay func = NotYetDone (fun () -> func())

    // The stepping action for the computations.
    let step expr =
        match expr with
        | Done _ -> expr
        | NotYetDone func -> func ()

    // The rest of the operations are boilerplate.
    // The tryFinally operator.
    // This is boilerplate in terms of "result", "catch", and "bind".
    let tryFinally expr compensation =
        catch (expr)
        |> bind (fun res ->
            compensation();
            match res with
            | Ok value -> result value
            | Exception exn -> raise exn)

    // The tryWith operator.
    // This is boilerplate in terms of "result", "catch", and "bind".
    let tryWith exn handler =
        catch exn
        |> bind (function Ok value -> result value | Exception exn -> handler exn)

    // The whileLoop operator.
    // This is boilerplate in terms of "result" and "bind".
    let rec whileLoop pred body =
        if pred() then body |> bind (fun _ -> whileLoop pred body)
        else result ()

    // The sequential composition operator.
    // This is boilerplate in terms of "result" and "bind".
    let combine expr1 expr2 =
        expr1 |> bind (fun () -> expr2)

    // The using operator.
    let using (resource: #System.IDisposable) func =
        tryFinally (func resource) (fun () -> resource.Dispose())

    // The forLoop operator.
    // This is boilerplate in terms of "catch", "result", and "bind".
    let forLoop (collection:seq<_>) func =
        let ie = collection.GetEnumerator()
        tryFinally
            (whileLoop
                (fun () -> ie.MoveNext())
                (delay (fun () -> let value = ie.Current in func value)))
            (fun () -> ie.Dispose())

// The builder class.
type EventuallyBuilder() =
    member x.Bind(comp, func) = Eventually.bind func comp
    member x.Return(value) = Eventually.result value
    member x.ReturnFrom(value) = value
    member x.Combine(expr1, expr2) = Eventually.combine expr1 expr2
    member x.Delay(func) = Eventually.delay func
    member x.Zero() = Eventually.result ()
    member x.TryWith(expr, handler) = Eventually.tryWith expr handler
    member x.TryFinally(expr, compensation) = Eventually.tryFinally expr compensation
    member x.For(coll:seq<_>, func) = Eventually.forLoop coll func
    member x.Using(resource, expr) = Eventually.using resource expr

let eventually = new EventuallyBuilder()

let comp = eventually {
    for x in 1..2 do
        printfn $" x = %d{x}"
    return 3 + 4 }

// Try the remaining lines in F# interactive to see how this
// computation expression works in practice.
let step x = Eventually.step x

// returns "NotYetDone <closure>"
comp |> step

// prints "x = 1"
// returns "NotYetDone <closure>"
comp |> step |> step

// prints "x = 1"
// prints "x = 2"
// returns "Done 7"
comp |> step |> step |> step |> step
```

Wyrażenie obliczeniowe ma typ podstawowy, który zwraca wyrażenie. Typ podstawowy może reprezentować obliczony wynik lub opóźnione obliczenie, które może być wykonane, lub może być sposobem na iterację w przypadku niektórych typów kolekcji. W poprzednim przykładzie typ podstawowy był **ostatecznie**. Dla wyrażenia sekwencji jest typem podstawowym <xref:System.Collections.Generic.IEnumerable%601?displayProperty=nameWithType> . Dla wyrażenia zapytania jest typem podstawowym <xref:System.Linq.IQueryable?displayProperty=nameWithType> . Dla asynchronicznego przepływu pracy typem podstawowym jest [`Async`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-control-fsharpasync-1.html) . `Async`Obiekt reprezentuje prace, które należy wykonać, aby obliczyć wynik. Na przykład można wywołać [`Async.RunSynchronously`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-control-fsharpasync.html#RunSynchronously) wykonywanie obliczeń i zwrócić wynik.

## <a name="custom-operations"></a>Operacje niestandardowe

Istnieje możliwość zdefiniowania niestandardowej operacji w wyrażeniu obliczenia i użycia niestandardowej operacji jako operatora w wyrażeniu obliczeniowym. Na przykład można uwzględnić operator zapytania w wyrażeniu zapytania. Podczas definiowania niestandardowej operacji należy zdefiniować wartość Yield i dla metod w wyrażeniu obliczenia. Aby zdefiniować niestandardową operację, należy umieścić ją w klasie konstruktora dla wyrażenia obliczeń, a następnie zastosować [`CustomOperationAttribute`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-customoperationattribute.html) . Ten atrybut przyjmuje ciąg jako argument, który jest nazwą, która ma być używana w operacji niestandardowej. Ta nazwa znajduje się w zakresie na początku otwierającego nawiasu klamrowego wyrażenia obliczeń. W związku z tym nie należy używać identyfikatorów, które mają taką samą nazwę jak operacja niestandardowa w tym bloku. Na przykład Unikaj używania identyfikatorów takich jak `all` lub `last` w wyrażeniach zapytań.

### <a name="extending-existing-builders-with-new-custom-operations"></a>Rozszerzanie istniejących konstruktorów przy użyciu nowych operacji niestandardowych

Jeśli masz już klasę konstruktora, jej operacje niestandardowe można rozszerzyć spoza tej klasy konstruktora. Rozszerzenia muszą być zadeklarowane w modułach. Przestrzenie nazw nie mogą zawierać składowych rozszerzenia, z wyjątkiem tego samego pliku i tej samej grupy deklaracji przestrzeni nazw, w której jest zdefiniowany typ.

Poniższy przykład pokazuje rozszerzenie istniejącej `FSharp.Linq.QueryBuilder` klasy.

```fsharp
type FSharp.Linq.QueryBuilder with

    [<CustomOperation("existsNot")>]
    member _.ExistsNot (source: QuerySource<'T, 'Q>, predicate) =
        Enumerable.Any (source.Source, Func<_,_>(predicate)) |> not
```

## <a name="see-also"></a>Zobacz także

- [Dokumentacja języka F #](index.md)
- [Asynchroniczne przepływy pracy](asynchronous-workflows.md)
- [Sekwencje](sequences.md)
- [Wyrażenia kwerend](query-expressions.md)
