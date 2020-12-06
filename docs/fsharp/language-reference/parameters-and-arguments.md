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
# <a name="parameters-and-arguments"></a><span data-ttu-id="409b8-103">Parametry i argumenty</span><span class="sxs-lookup"><span data-stu-id="409b8-103">Parameters and Arguments</span></span>

<span data-ttu-id="409b8-104">W tym temacie opisano obsługę języków definiujących parametry i przekazywanie argumentów do funkcji, metod i właściwości.</span><span class="sxs-lookup"><span data-stu-id="409b8-104">This topic describes language support for defining parameters and passing arguments to functions, methods, and properties.</span></span> <span data-ttu-id="409b8-105">Zawiera informacje o sposobach przekazywania przez odwołanie oraz sposobie definiowania i używania metod, które mogą przyjmować zmienną liczbę argumentów.</span><span class="sxs-lookup"><span data-stu-id="409b8-105">It includes information about how to pass by reference, and how to define and use methods that can take a variable number of arguments.</span></span>

## <a name="parameters-and-arguments"></a><span data-ttu-id="409b8-106">Parametry i argumenty</span><span class="sxs-lookup"><span data-stu-id="409b8-106">Parameters and Arguments</span></span>

<span data-ttu-id="409b8-107">*Parametr* Term służy do opisywania nazw dla wartości, które powinny być dostarczone.</span><span class="sxs-lookup"><span data-stu-id="409b8-107">The term *parameter* is used to describe the names for values that are expected to be supplied.</span></span> <span data-ttu-id="409b8-108">*Argument* Term jest używany dla wartości podanych dla każdego parametru.</span><span class="sxs-lookup"><span data-stu-id="409b8-108">The term *argument* is used for the values provided for each parameter.</span></span>

<span data-ttu-id="409b8-109">Parametry można określić w postaci krotek lub rozwinięte lub w niektórych kombinacjach dwóch.</span><span class="sxs-lookup"><span data-stu-id="409b8-109">Parameters can be specified in tuple or curried form, or in some combination of the two.</span></span> <span data-ttu-id="409b8-110">Argumenty można przekazać za pomocą jawnej nazwy parametru.</span><span class="sxs-lookup"><span data-stu-id="409b8-110">You can pass arguments by using an explicit parameter name.</span></span> <span data-ttu-id="409b8-111">Parametry metod mogą być określone jako opcjonalne i mają określoną wartość domyślną.</span><span class="sxs-lookup"><span data-stu-id="409b8-111">Parameters of methods can be specified as optional and given a default value.</span></span>

## <a name="parameter-patterns"></a><span data-ttu-id="409b8-112">Wzorce parametrów</span><span class="sxs-lookup"><span data-stu-id="409b8-112">Parameter Patterns</span></span>

<span data-ttu-id="409b8-113">Parametry dostarczone do funkcji i metod są ogólnie wzorce oddzielone spacjami.</span><span class="sxs-lookup"><span data-stu-id="409b8-113">Parameters supplied to functions and methods are, in general, patterns separated by spaces.</span></span> <span data-ttu-id="409b8-114">Oznacza to, że w zasadzie wszystkie wzorce opisane w [wyrażeniach dopasowania](match-expressions.md) mogą być używane na liście parametrów dla funkcji lub elementu członkowskiego.</span><span class="sxs-lookup"><span data-stu-id="409b8-114">This means that, in principle, any of the patterns described in [Match Expressions](match-expressions.md) can be used in a parameter list for a function or member.</span></span>

<span data-ttu-id="409b8-115">Metody zwykle używają spójnej formy przekazywania argumentów.</span><span class="sxs-lookup"><span data-stu-id="409b8-115">Methods usually use the tuple form of passing arguments.</span></span> <span data-ttu-id="409b8-116">Pozwala to uzyskać wyraźniejszy wynik z perspektywy innych języków .NET, ponieważ formularz spójny pasuje do sposobu przekazywania argumentów w metodach .NET.</span><span class="sxs-lookup"><span data-stu-id="409b8-116">This achieves a clearer result from the perspective of other .NET languages because the tuple form matches the way arguments are passed in .NET methods.</span></span>

<span data-ttu-id="409b8-117">Formularz rozwinięte jest najczęściej używany z funkcjami utworzonymi przy użyciu `let` powiązań.</span><span class="sxs-lookup"><span data-stu-id="409b8-117">The curried form is most often used with functions created by using `let` bindings.</span></span>

<span data-ttu-id="409b8-118">W poniższym pseudokodzie przedstawiono przykłady argumentów krotki i rozwinięte.</span><span class="sxs-lookup"><span data-stu-id="409b8-118">The following pseudocode shows examples of tuple and curried arguments.</span></span>

```fsharp
// Tuple form.
member this.SomeMethod(param1, param2) = ...
// Curried form.
let function1 param1 param2 = ...
```

<span data-ttu-id="409b8-119">Połączone formularze są możliwe, gdy niektóre argumenty są kolekcjami, a niektóre z nich nie są.</span><span class="sxs-lookup"><span data-stu-id="409b8-119">Combined forms are possible when some arguments are in tuples and some are not.</span></span>

```fsharp
let function2 param1 (param2a, param2b) param3 = ...
```

<span data-ttu-id="409b8-120">Inne wzorce mogą być również używane na listach parametrów, ale jeśli wzorzec parametru nie jest zgodny ze wszystkimi możliwymi danymi wejściowymi, może wystąpić niekompletne dopasowanie w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="409b8-120">Other patterns can also be used in parameter lists, but if the parameter pattern does not match all possible inputs, there might be an incomplete match at run time.</span></span> <span data-ttu-id="409b8-121">Wyjątek `MatchFailureException` jest generowany, gdy wartość argumentu nie pasuje do wzorców określonych na liście parametrów.</span><span class="sxs-lookup"><span data-stu-id="409b8-121">The exception `MatchFailureException` is generated when the value of an argument does not match the patterns specified in the parameter list.</span></span> <span data-ttu-id="409b8-122">Kompilator generuje ostrzeżenie, gdy wzorzec parametru zezwala na niekompletne dopasowania.</span><span class="sxs-lookup"><span data-stu-id="409b8-122">The compiler issues a warning when a parameter pattern allows for incomplete matches.</span></span> <span data-ttu-id="409b8-123">Co najmniej jeden inny wzorzec jest często przydatny dla list parametrów, który jest wzorcem wieloznacznym.</span><span class="sxs-lookup"><span data-stu-id="409b8-123">At least one other pattern is commonly useful for parameter lists, and that is the wildcard pattern.</span></span> <span data-ttu-id="409b8-124">Możesz użyć symbolu wieloznacznego na liście parametrów, gdy po prostu chcesz zignorować wszystkie dostarczone argumenty.</span><span class="sxs-lookup"><span data-stu-id="409b8-124">You use the wildcard pattern in a parameter list when you simply want to ignore any arguments that are supplied.</span></span> <span data-ttu-id="409b8-125">Poniższy kod ilustruje użycie wzorca wieloznacznego na liście argumentów.</span><span class="sxs-lookup"><span data-stu-id="409b8-125">The following code illustrates the use of the wildcard pattern in an argument list.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3801.fs)]

<span data-ttu-id="409b8-126">Wzorzec symbol wieloznaczny może być przydatny, gdy nie są potrzebne argumenty przekazane, takie jak w głównym punkcie wejścia do programu, gdy użytkownik nie interesuje argumentów wiersza polecenia, które są zwykle dostarczane jako tablica ciągów, jak w poniższym kodzie.</span><span class="sxs-lookup"><span data-stu-id="409b8-126">The wildcard pattern can be useful whenever you do not need the arguments passed in, such as in the main entry point to a program, when you are not interested in the command-line arguments that are normally supplied as a string array, as in the following code.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3802.fs)]

<span data-ttu-id="409b8-127">Inne wzorce, które są czasami używane w argumentach są wzorcem i wzorcami `as` identyfikatorów skojarzonymi z związkami rozłącznych i aktywnymi wzorcami.</span><span class="sxs-lookup"><span data-stu-id="409b8-127">Other patterns that are sometimes used in arguments are the `as` pattern, and identifier patterns associated with discriminated unions and active patterns.</span></span> <span data-ttu-id="409b8-128">Możesz użyć wzorca Union o pojedynczej wielkości liter w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="409b8-128">You can use the single-case discriminated union pattern as follows.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3803.fs)]

<span data-ttu-id="409b8-129">Dane wyjściowe są następujące:</span><span class="sxs-lookup"><span data-stu-id="409b8-129">The output is as follows.</span></span>

```console
Data begins at 0 and ends at 4 in string Et tu, Brute?
Et tu
```

<span data-ttu-id="409b8-130">Aktywne wzorce mogą być przydatne jako parametry, na przykład podczas przekształcania argumentu w żądany format, jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="409b8-130">Active patterns can be useful as parameters, for example, when transforming an argument into a desired format, as in the following example:</span></span>

```fsharp
type Point = { x : float; y : float }

let (| Polar |) { x = x; y = y} =
    ( sqrt (x*x + y*y), System.Math.Atan (y/ x) )

let radius (Polar(r, _)) = r
let angle (Polar(_, theta)) = theta
```

<span data-ttu-id="409b8-131">Możesz użyć `as` wzorca, aby przechowywać dopasowaną wartość jako wartość lokalną, jak pokazano w następującym wierszu kodu.</span><span class="sxs-lookup"><span data-stu-id="409b8-131">You can use the `as` pattern to store a matched value as a local value, as is shown in the following line of code.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3805.fs)]

<span data-ttu-id="409b8-132">Inny wzorzec, który jest używany sporadycznie to funkcja, która pozostawia ostatni argument bez nazwy, dostarczając jako treść funkcji wyrażenie lambda, które natychmiast wykonuje dopasowanie wzorca dla niejawnego argumentu.</span><span class="sxs-lookup"><span data-stu-id="409b8-132">Another pattern that is used occasionally is a function that leaves the last argument unnamed by providing, as the body of the function, a lambda expression that immediately performs a pattern match on the implicit argument.</span></span> <span data-ttu-id="409b8-133">Przykładem jest poniższy wiersz kodu.</span><span class="sxs-lookup"><span data-stu-id="409b8-133">An example of this is the following line of code.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3804.fs)]

<span data-ttu-id="409b8-134">Ten kod definiuje funkcję, która przyjmuje listę ogólną i zwraca `true` , jeśli lista jest pusta i `false` w przeciwnym razie.</span><span class="sxs-lookup"><span data-stu-id="409b8-134">This code defines a function that takes a generic list and returns `true` if the list is empty, and `false` otherwise.</span></span> <span data-ttu-id="409b8-135">Użycie takich technik może utrudnić odczytywanie kodu.</span><span class="sxs-lookup"><span data-stu-id="409b8-135">The use of such techniques can make code more difficult to read.</span></span>

<span data-ttu-id="409b8-136">Czasami wzorce, które obejmują niekompletne dopasowania, są przydatne, na przykład, Jeśli wiesz, że listy w programie mają tylko trzy elementy, możesz użyć wzorca, takiego jak poniższy, na liście parametrów.</span><span class="sxs-lookup"><span data-stu-id="409b8-136">Occasionally, patterns that involve incomplete matches are useful, for example, if you know that the lists in your program have only three elements, you might use a pattern like the following in a parameter list.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3806.fs)]

<span data-ttu-id="409b8-137">Użycie wzorców, które mają niekompletne dopasowania, jest najlepszym zarezerwowane do szybkiego tworzenia prototypów i innych tymczasowych celów.</span><span class="sxs-lookup"><span data-stu-id="409b8-137">The use of patterns that have incomplete matches is best reserved for quick prototyping and other temporary uses.</span></span> <span data-ttu-id="409b8-138">Kompilator wyda Ostrzeżenie dla tego kodu.</span><span class="sxs-lookup"><span data-stu-id="409b8-138">The compiler will issue a warning for such code.</span></span> <span data-ttu-id="409b8-139">Takie wzorce nie mogą obejmować ogólnego przypadku wszystkich możliwych danych wejściowych i dlatego nie są odpowiednie do interfejsów API składników.</span><span class="sxs-lookup"><span data-stu-id="409b8-139">Such patterns cannot cover the general case of all possible inputs and therefore are not suitable for component APIs.</span></span>

## <a name="named-arguments"></a><span data-ttu-id="409b8-140">Nazwane argumenty</span><span class="sxs-lookup"><span data-stu-id="409b8-140">Named Arguments</span></span>

<span data-ttu-id="409b8-141">Argumenty metod można określić za pomocą pozycji na liście argumentów rozdzielanych przecinkami lub mogą być przekazane do metody jawnie przez podanie nazwy, a po niej znaku równości oraz wartości, która ma zostać przeniesiona.</span><span class="sxs-lookup"><span data-stu-id="409b8-141">Arguments for methods can be specified by position in a comma-separated argument list, or they can be passed to a method explicitly by providing the name, followed by an equal sign and the value to be passed in.</span></span> <span data-ttu-id="409b8-142">Jeśli określony przez podanie nazwy, mogą one pojawić się w innej kolejności niż użyta w deklaracji.</span><span class="sxs-lookup"><span data-stu-id="409b8-142">If specified by providing the name, they can appear in a different order from that used in the declaration.</span></span>

<span data-ttu-id="409b8-143">Argumenty nazwane mogą sprawiać, że kod jest bardziej czytelny i bardziej dostosowywalny do niektórych typów zmian w interfejsie API, takich jak zmiana kolejności parametrów metody.</span><span class="sxs-lookup"><span data-stu-id="409b8-143">Named arguments can make code more readable and more adaptable to certain types of changes in the API, such as a reordering of method parameters.</span></span>

<span data-ttu-id="409b8-144">Nazwane argumenty są dozwolone tylko dla metod, nie do `let` funkcji powiązanych, wartości funkcji ani wyrażeń lambda.</span><span class="sxs-lookup"><span data-stu-id="409b8-144">Named arguments are allowed only for methods, not for `let`-bound functions, function values, or lambda expressions.</span></span>

<span data-ttu-id="409b8-145">Poniższy przykład kodu demonstruje użycie nazwanych argumentów.</span><span class="sxs-lookup"><span data-stu-id="409b8-145">The following code example demonstrates the use of named arguments.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3807.fs)]

<span data-ttu-id="409b8-146">W wywołaniu konstruktora klasy można ustawić wartości właściwości klasy przy użyciu składni podobnej do argumentów nazwanych.</span><span class="sxs-lookup"><span data-stu-id="409b8-146">In a call to a class constructor, you can set the values of properties of the class by using a syntax similar to that of named arguments.</span></span> <span data-ttu-id="409b8-147">Poniższy przykład pokazuje tę składnię.</span><span class="sxs-lookup"><span data-stu-id="409b8-147">The following example shows this syntax.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3506.fs)]

<span data-ttu-id="409b8-148">Aby uzyskać więcej informacji, zobacz [konstruktory (F #)](members/constructors.md).</span><span class="sxs-lookup"><span data-stu-id="409b8-148">For more information, see [Constructors (F#)](members/constructors.md).</span></span>

## <a name="optional-parameters"></a><span data-ttu-id="409b8-149">Parametry opcjonalne</span><span class="sxs-lookup"><span data-stu-id="409b8-149">Optional Parameters</span></span>

<span data-ttu-id="409b8-150">Można określić opcjonalny parametr dla metody przy użyciu znaku zapytania przed nazwą parametru.</span><span class="sxs-lookup"><span data-stu-id="409b8-150">You can specify an optional parameter for a method by using a question mark in front of the parameter name.</span></span> <span data-ttu-id="409b8-151">Parametry opcjonalne są interpretowane jako typ opcji F #, dzięki czemu można wykonywać zapytania do nich w zwykły sposób, w jaki typy opcji są badane przy użyciu `match` wyrażenia z `Some` i `None` .</span><span class="sxs-lookup"><span data-stu-id="409b8-151">Optional parameters are interpreted as the F# option type, so you can query them in the regular way that option types are queried, by using a `match` expression with `Some` and `None`.</span></span> <span data-ttu-id="409b8-152">Parametry opcjonalne są dozwolone tylko w składach, a nie na funkcjach utworzonych za pomocą `let` powiązań.</span><span class="sxs-lookup"><span data-stu-id="409b8-152">Optional parameters are permitted only on members, not on functions created by using `let` bindings.</span></span>

<span data-ttu-id="409b8-153">Istniejące wartości opcjonalne można przekazać do metody za pomocą nazwy parametru, takiej jak `?arg=None` lub `?arg=Some(3)` lub `?arg=arg` .</span><span class="sxs-lookup"><span data-stu-id="409b8-153">You can pass existing optional values to method by parameter name, such as `?arg=None` or `?arg=Some(3)` or `?arg=arg`.</span></span> <span data-ttu-id="409b8-154">Może to być przydatne podczas kompilowania metody, która przekazuje argumenty opcjonalne do innej metody.</span><span class="sxs-lookup"><span data-stu-id="409b8-154">This can be useful when building a method that passes optional arguments to another method.</span></span>

<span data-ttu-id="409b8-155">Można również użyć funkcji `defaultArg` , która ustawia wartość domyślną opcjonalnego argumentu.</span><span class="sxs-lookup"><span data-stu-id="409b8-155">You can also use a function `defaultArg`, which sets a default value of an optional argument.</span></span> <span data-ttu-id="409b8-156">`defaultArg`Funkcja przyjmuje opcjonalny parametr jako pierwszy argument i wartość domyślną jako drugi.</span><span class="sxs-lookup"><span data-stu-id="409b8-156">The `defaultArg` function takes the optional parameter as the first argument and the default value as the second.</span></span>

<span data-ttu-id="409b8-157">Poniższy przykład ilustruje użycie parametrów opcjonalnych.</span><span class="sxs-lookup"><span data-stu-id="409b8-157">The following example illustrates the use of optional parameters.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3808.fs)]

<span data-ttu-id="409b8-158">Dane wyjściowe są następujące:</span><span class="sxs-lookup"><span data-stu-id="409b8-158">The output is as follows.</span></span>

```console
Baud Rate: 9600 Duplex: Full Parity: false
Baud Rate: 4800 Duplex: Half Parity: false
Baud Rate: 300 Duplex: Half Parity: true
Baud Rate: 9600 Duplex: Full Parity: false
Baud Rate: 9600 Duplex: Full Parity: false
Baud Rate: 4800 Duplex: Half Parity: false
```

<span data-ttu-id="409b8-159">Na potrzeby języka C# i Visual Basic międzyoperacyjności można użyć atrybutów `[<Optional; DefaultParameterValue<(...)>]` w języku F #, aby wywołujący zobaczyli argument jako opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="409b8-159">For the purposes of C# and Visual Basic interop you can use the attributes `[<Optional; DefaultParameterValue<(...)>]` in F#, so that callers will see an argument as optional.</span></span> <span data-ttu-id="409b8-160">Jest to równoznaczne z zdefiniowaniem argumentu jako opcjonalnego w języku C# jako w `MyMethod(int i = 3)` .</span><span class="sxs-lookup"><span data-stu-id="409b8-160">This is equivalent to defining the argument as optional in C# as in `MyMethod(int i = 3)`.</span></span>

```fsharp
open System
open System.Runtime.InteropServices
type C =
    static member Foo([<Optional; DefaultParameterValue("Hello world")>] message) =
        printfn $"{message}"
```

<span data-ttu-id="409b8-161">Możesz również określić nowy obiekt jako domyślną wartość parametru.</span><span class="sxs-lookup"><span data-stu-id="409b8-161">You can also specify a new object as a default parameter value.</span></span> <span data-ttu-id="409b8-162">Na przykład `Foo` element członkowski może mieć opcjonalnie `CancellationToken` jako dane wejściowe:</span><span class="sxs-lookup"><span data-stu-id="409b8-162">For example, the `Foo` member could have an optional `CancellationToken` as input instead:</span></span>

```fsharp
open System.Threading
open System.Runtime.InteropServices
type C =
    static member Foo([<Optional; DefaultParameterValue(CancellationToken())>] ct: CancellationToken) =
        printfn $"{ct}"
```

<span data-ttu-id="409b8-163">Wartość określona jako argument `DefaultParameterValue` musi być zgodna z typem parametru.</span><span class="sxs-lookup"><span data-stu-id="409b8-163">The value given as argument to `DefaultParameterValue` must match the type of the parameter.</span></span> <span data-ttu-id="409b8-164">Na przykład następujące elementy są niedozwolone:</span><span class="sxs-lookup"><span data-stu-id="409b8-164">For example, the following is not allowed:</span></span>

```fsharp
type C =
    static member Wrong([<Optional; DefaultParameterValue("string")>] i:int) = ()
```

<span data-ttu-id="409b8-165">W takim przypadku kompilator generuje ostrzeżenie i całkowicie zignoruje oba atrybuty.</span><span class="sxs-lookup"><span data-stu-id="409b8-165">In this case, the compiler generates a warning and will ignore both attributes altogether.</span></span> <span data-ttu-id="409b8-166">Należy zauważyć, że wartość domyślna `null` musi być adnotacją typu, ponieważ w przeciwnym razie kompilator wnioskuje niewłaściwy typ, tj `[<Optional; DefaultParameterValue(null:obj)>] o:obj` .</span><span class="sxs-lookup"><span data-stu-id="409b8-166">Note that the default value `null` needs to be type-annotated, as otherwise the compiler infers the wrong type, i.e. `[<Optional; DefaultParameterValue(null:obj)>] o:obj`.</span></span>

## <a name="passing-by-reference"></a><span data-ttu-id="409b8-167">Przekazywanie przez odwołanie</span><span class="sxs-lookup"><span data-stu-id="409b8-167">Passing by Reference</span></span>

<span data-ttu-id="409b8-168">Przekazywanie wartości F # przez odwołanie obejmuje [ByRef](byrefs.md), które są zarządzanymi typami wskaźników.</span><span class="sxs-lookup"><span data-stu-id="409b8-168">Passing an F# value by reference involves [byrefs](byrefs.md), which are managed pointer types.</span></span> <span data-ttu-id="409b8-169">Wskazówki dotyczące używanego typu są następujące:</span><span class="sxs-lookup"><span data-stu-id="409b8-169">Guidance for which type to use is as follows:</span></span>

- <span data-ttu-id="409b8-170">Użyj `inref<'T>` , jeśli musisz tylko odczytać wskaźnik.</span><span class="sxs-lookup"><span data-stu-id="409b8-170">Use `inref<'T>` if you only need to read the pointer.</span></span>
- <span data-ttu-id="409b8-171">Użyj `outref<'T>` , jeśli musisz tylko pisać na wskaźniku.</span><span class="sxs-lookup"><span data-stu-id="409b8-171">Use `outref<'T>` if you only need to write to the pointer.</span></span>
- <span data-ttu-id="409b8-172">Użyj, `byref<'T>` Jeśli musisz zarówno czytać, jak i zapisywać na wskaźniku.</span><span class="sxs-lookup"><span data-stu-id="409b8-172">Use `byref<'T>` if you need to both read from and write to the pointer.</span></span>

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

<span data-ttu-id="409b8-173">Ponieważ parametr jest wskaźnikiem, a wartość jest modyfikowalna, wszelkie zmiany wartości są zachowywane po wykonaniu funkcji.</span><span class="sxs-lookup"><span data-stu-id="409b8-173">Because the parameter is a pointer and the value is mutable, any changes to the value are retained after the execution of the function.</span></span>

<span data-ttu-id="409b8-174">Można użyć krotki jako wartości zwracanej do przechowywania dowolnych `out` parametrów w metodach biblioteki .NET.</span><span class="sxs-lookup"><span data-stu-id="409b8-174">You can use a tuple as a return value to store any `out` parameters in .NET library methods.</span></span> <span data-ttu-id="409b8-175">Alternatywnie można traktować `out` parametr jako `byref` parametr.</span><span class="sxs-lookup"><span data-stu-id="409b8-175">Alternatively, you can treat the `out` parameter as a `byref` parameter.</span></span> <span data-ttu-id="409b8-176">Poniższy przykład kodu ilustruje obydwie metody.</span><span class="sxs-lookup"><span data-stu-id="409b8-176">The following code example illustrates both ways.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3810.fs)]

## <a name="parameter-arrays"></a><span data-ttu-id="409b8-177">Parameter — Tablice</span><span class="sxs-lookup"><span data-stu-id="409b8-177">Parameter Arrays</span></span>

<span data-ttu-id="409b8-178">Czasami konieczne jest zdefiniowanie funkcji, która przyjmuje dowolną liczbę parametrów typu heterogenicznego.</span><span class="sxs-lookup"><span data-stu-id="409b8-178">Occasionally it is necessary to define a function that takes an arbitrary number of parameters of heterogeneous type.</span></span> <span data-ttu-id="409b8-179">Nie byłoby praktyczne, aby utworzyć wszystkie możliwe przeciążone metody w celu uwzględnienia wszystkich typów, które mogą być używane.</span><span class="sxs-lookup"><span data-stu-id="409b8-179">It would not be practical to create all the possible overloaded methods to account for all the types that could be used.</span></span> <span data-ttu-id="409b8-180">Implementacje platformy .NET zapewniają obsługę takich metod za pomocą funkcji Tablica parametrów.</span><span class="sxs-lookup"><span data-stu-id="409b8-180">The .NET implementations provide support for such methods through the parameter array feature.</span></span> <span data-ttu-id="409b8-181">Metoda przyjmująca tablicę parametrów w jej podpisie może być dostarczana z dowolną liczbą parametrów.</span><span class="sxs-lookup"><span data-stu-id="409b8-181">A method that takes a parameter array in its signature can be provided with an arbitrary number of parameters.</span></span> <span data-ttu-id="409b8-182">Parametry są umieszczane w tablicy.</span><span class="sxs-lookup"><span data-stu-id="409b8-182">The parameters are put into an array.</span></span> <span data-ttu-id="409b8-183">Typ elementów tablicy określa typy parametrów, które mogą być przesyłane do funkcji.</span><span class="sxs-lookup"><span data-stu-id="409b8-183">The type of the array elements determines the parameter types that can be passed to the function.</span></span> <span data-ttu-id="409b8-184">Jeśli zdefiniujesz tablicę parametrów `System.Object` jako typ elementu, kod klienta może przekazać wartości dowolnego typu.</span><span class="sxs-lookup"><span data-stu-id="409b8-184">If you define the parameter array with `System.Object` as the element type, then client code can pass values of any type.</span></span>

<span data-ttu-id="409b8-185">W języku F # tablice parametrów można definiować tylko w metodach.</span><span class="sxs-lookup"><span data-stu-id="409b8-185">In F#, parameter arrays can only be defined in methods.</span></span> <span data-ttu-id="409b8-186">Nie mogą być używane w autonomicznych funkcjach lub funkcjach, które są zdefiniowane w modułach.</span><span class="sxs-lookup"><span data-stu-id="409b8-186">They cannot be used in standalone functions or functions that are defined in modules.</span></span>

<span data-ttu-id="409b8-187">Należy zdefiniować tablicę parametrów przy użyciu `ParamArray` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="409b8-187">You define a parameter array by using the `ParamArray` attribute.</span></span> <span data-ttu-id="409b8-188">Ten `ParamArray` atrybut może być stosowany tylko do ostatniego parametru.</span><span class="sxs-lookup"><span data-stu-id="409b8-188">The `ParamArray` attribute can only be applied to the last parameter.</span></span>

<span data-ttu-id="409b8-189">Poniższy kod ilustruje zarówno wywołanie metody .NET, która przyjmuje tablicę parametrów i definicję typu w F #, który ma metodę, która pobiera tablicę parametrów.</span><span class="sxs-lookup"><span data-stu-id="409b8-189">The following code illustrates both calling a .NET method that takes a parameter array and the definition of a type in F# that has a method that takes a parameter array.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-2/snippet3811.fs)]

<span data-ttu-id="409b8-190">Po uruchomieniu w projekcie dane wyjściowe poprzedniego kodu są następujące:</span><span class="sxs-lookup"><span data-stu-id="409b8-190">When run in a project, the output of the previous code is as follows:</span></span>

```console
a 1 10 Hello world 1 True
"a"
1
10.0
"Hello world"
1u
true
```

## <a name="see-also"></a><span data-ttu-id="409b8-191">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="409b8-191">See also</span></span>

- [<span data-ttu-id="409b8-192">Elementy członkowskie</span><span class="sxs-lookup"><span data-stu-id="409b8-192">Members</span></span>](./members/index.md)
