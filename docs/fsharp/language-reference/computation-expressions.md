---
title: Wyrażenia obliczeń
description: Dowiedz się, jak utworzyć wygodną składnię do F# pisania obliczeń w programie, które mogą być sekwencjonowane i łączone przy użyciu konstrukcji przepływu sterowania i powiązań.
ms.date: 11/04/2019
ms.openlocfilehash: 55406cc12d9e6e890fe69d712f79486d23b84452
ms.sourcegitcommit: 13e79efdbd589cad6b1de634f5d6b1262b12ab01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/28/2020
ms.locfileid: "76794551"
---
# <a name="computation-expressions"></a><span data-ttu-id="960dc-103">Wyrażenia obliczeń</span><span class="sxs-lookup"><span data-stu-id="960dc-103">Computation Expressions</span></span>

<span data-ttu-id="960dc-104">Wyrażenia obliczeń w F# programie zapewniają wygodną składnię do pisania obliczeń, które mogą być sekwencjonowane i łączone przy użyciu konstrukcji przepływu sterowania i powiązań.</span><span class="sxs-lookup"><span data-stu-id="960dc-104">Computation expressions in F# provide a convenient syntax for writing computations that can be sequenced and combined using control flow constructs and bindings.</span></span> <span data-ttu-id="960dc-105">W zależności od rodzaju wyrażenia obliczeń można traktować ich jako metodę wyrażania monads, monoids, Monad i applicative funktory.</span><span class="sxs-lookup"><span data-stu-id="960dc-105">Depending on the kind of computation expression, they can be thought of as a way to express monads, monoids, monad transformers, and applicative functors.</span></span> <span data-ttu-id="960dc-106">Jednak, w przeciwieństwie do innych języków ( *takich jak Haskell* ), nie są one powiązane z pojedynczym abstrakcją i nie polegają na makrach ani innych formach programowania, aby osiągnąć wygodną i zależną od kontekstu składnię.</span><span class="sxs-lookup"><span data-stu-id="960dc-106">However, unlike other languages (such as *do-notation* in Haskell), they are not tied to a single abstraction, and do not rely on macros or other forms of metaprogramming to accomplish a convenient and context-sensitive syntax.</span></span>

## <a name="overview"></a><span data-ttu-id="960dc-107">Omówienie</span><span class="sxs-lookup"><span data-stu-id="960dc-107">Overview</span></span>

<span data-ttu-id="960dc-108">Obliczenia mogą mieć wiele form.</span><span class="sxs-lookup"><span data-stu-id="960dc-108">Computations can take many forms.</span></span> <span data-ttu-id="960dc-109">Najbardziej powszechną formą obliczeń jest wykonywanie jednowątkowe, które można łatwo zrozumieć i zmodyfikować.</span><span class="sxs-lookup"><span data-stu-id="960dc-109">The most common form of computation is single-threaded execution, which is easy to understand and modify.</span></span> <span data-ttu-id="960dc-110">Jednak nie wszystkie formy obliczeń są tak proste jak wykonywanie jednowątkowe.</span><span class="sxs-lookup"><span data-stu-id="960dc-110">However, not all forms of computation are as straightforward as single-threaded execution.</span></span> <span data-ttu-id="960dc-111">Oto niektóre przykłady:</span><span class="sxs-lookup"><span data-stu-id="960dc-111">Some examples include:</span></span>

- <span data-ttu-id="960dc-112">Obliczenia niedeterministyczne</span><span class="sxs-lookup"><span data-stu-id="960dc-112">Non-deterministic computations</span></span>
- <span data-ttu-id="960dc-113">Obliczenia asynchroniczne</span><span class="sxs-lookup"><span data-stu-id="960dc-113">Asynchronous computations</span></span>
- <span data-ttu-id="960dc-114">Wpływ obliczeń</span><span class="sxs-lookup"><span data-stu-id="960dc-114">Effectful computations</span></span>
- <span data-ttu-id="960dc-115">Obliczenia dotyczące przetworzenia</span><span class="sxs-lookup"><span data-stu-id="960dc-115">Generative computations</span></span>

<span data-ttu-id="960dc-116">Ogólnie rzecz biorąc, istnieją operacje obliczeniowe *zależne od kontekstu* , które należy wykonać w niektórych częściach aplikacji.</span><span class="sxs-lookup"><span data-stu-id="960dc-116">More generally, there are *context-sensitive* computations that you must perform in certain parts of an application.</span></span> <span data-ttu-id="960dc-117">Pisanie kodu wrażliwego na kontekst może być trudne, ponieważ jest to łatwe w obsłudze obliczenia poza danym kontekstem bez abstrakcji, aby zapobiec temu.</span><span class="sxs-lookup"><span data-stu-id="960dc-117">Writing context-sensitive code can be challenging, as it is easy to "leak" computations outside of a given context without abstractions to prevent you from doing so.</span></span> <span data-ttu-id="960dc-118">Te streszczenia są często trudne do napisania przez siebie, co oznacza F# , że jest to ogólny sposób, nazywany **wyrażeniami obliczeń**.</span><span class="sxs-lookup"><span data-stu-id="960dc-118">These abstractions are often challenging to write by yourself, which is why F# has a generalized way to do so called **computation expressions**.</span></span>

<span data-ttu-id="960dc-119">Wyrażenia obliczeń oferują ujednoliconą składnię i abstrakcyjny model dla obliczeń z uwzględnieniem kontekstu.</span><span class="sxs-lookup"><span data-stu-id="960dc-119">Computation expressions offer a uniform syntax and abstraction model for encoding context-sensitive computations.</span></span>

<span data-ttu-id="960dc-120">Każde wyrażenie obliczeniowe jest obsługiwane przez typ *konstruktora* .</span><span class="sxs-lookup"><span data-stu-id="960dc-120">Every computation expression is backed by a *builder* type.</span></span> <span data-ttu-id="960dc-121">Typ konstruktora definiuje operacje, które są dostępne dla wyrażenia obliczeń.</span><span class="sxs-lookup"><span data-stu-id="960dc-121">The builder type defines the operations that are available for the computation expression.</span></span> <span data-ttu-id="960dc-122">Zobacz [Tworzenie nowego typu wyrażenia obliczeń](computation-expressions.md#creating-a-new-type-of-computation-expression), które pokazuje, jak utworzyć niestandardowe wyrażenie obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="960dc-122">See [Creating a New Type of Computation Expression](computation-expressions.md#creating-a-new-type-of-computation-expression), which shows how to create a custom computation expression.</span></span>

### <a name="syntax-overview"></a><span data-ttu-id="960dc-123">Omówienie składni</span><span class="sxs-lookup"><span data-stu-id="960dc-123">Syntax overview</span></span>

<span data-ttu-id="960dc-124">Wszystkie wyrażenia obliczeń mają następującą postać:</span><span class="sxs-lookup"><span data-stu-id="960dc-124">All computation expressions have the following form:</span></span>

```fsharp
builder-expr { cexper }
```

<span data-ttu-id="960dc-125">gdzie `builder-expr` jest nazwą typu konstruktora, który definiuje wyrażenie obliczeń, a `cexper` jest treścią wyrażenia wyrażenia obliczeń.</span><span class="sxs-lookup"><span data-stu-id="960dc-125">where `builder-expr` is the name of a builder type that defines the computation expression, and `cexper` is the expression body of the computation expression.</span></span> <span data-ttu-id="960dc-126">Na przykład kod wyrażenia obliczeń `async` może wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="960dc-126">For example, `async` computation expression code can look like this:</span></span>

```fsharp
let fetchAndDownload url =
    async {
        let! data = downloadData url

        let processedData = processData data

        return processedData
    }
```

<span data-ttu-id="960dc-127">W wyrażeniu obliczenia jest dostępna specjalna, dodatkowa składnia, jak pokazano w poprzednim przykładzie.</span><span class="sxs-lookup"><span data-stu-id="960dc-127">There is a special, additional syntax available within a computation expression, as shown in the previous example.</span></span> <span data-ttu-id="960dc-128">Wyrażenia obliczeń umożliwiają następujące formy wyrażeń:</span><span class="sxs-lookup"><span data-stu-id="960dc-128">The following expression forms are possible with computation expressions:</span></span>

```fsharp
expr { let! ... }
expr { do! ... }
expr { yield ... }
expr { yield! ... }
expr { return ... }
expr { return! ... }
expr { match! ... }
```

<span data-ttu-id="960dc-129">Każdy z tych słów kluczowych i inne standardowe F# słowa kluczowe są dostępne tylko w wyrażeniu obliczeń, jeśli zostały zdefiniowane w typie konstruktora zapasowego.</span><span class="sxs-lookup"><span data-stu-id="960dc-129">Each of these keywords, and other standard F# keywords are only available in a computation expression if they have been defined in the backing builder type.</span></span> <span data-ttu-id="960dc-130">Jedynym wyjątkiem jest `match!`, który jest samym cukrem składniowym do użycia `let!`, po którym następuje dopasowanie wzorca w wyniku.</span><span class="sxs-lookup"><span data-stu-id="960dc-130">The only exception to this is `match!`, which is itself syntactic sugar for the use of `let!` followed by a pattern match on the result.</span></span>

<span data-ttu-id="960dc-131">Typ konstruktora jest obiektem, który definiuje specjalne metody, które regulują sposób łączenia fragmentów wyrażenia obliczeń; oznacza to, że metody określają zachowanie wyrażenia obliczeń.</span><span class="sxs-lookup"><span data-stu-id="960dc-131">The builder type is an object that defines special methods that govern the way the fragments of the computation expression are combined; that is, its methods control how the computation expression behaves.</span></span> <span data-ttu-id="960dc-132">Innym sposobem opisywania klasy konstruktora jest to, że umożliwia dostosowanie operacji wielu F# konstrukcji, takich jak pętle i powiązania.</span><span class="sxs-lookup"><span data-stu-id="960dc-132">Another way to describe a builder class is to say that it enables you to customize the operation of many F# constructs, such as loops and bindings.</span></span>

### `let!`

<span data-ttu-id="960dc-133">Słowo kluczowe `let!` wiąże wynik wywołania innego wyrażenia obliczenia na nazwę:</span><span class="sxs-lookup"><span data-stu-id="960dc-133">The `let!` keyword binds the result of a call to another computation expression to a name:</span></span>

```fsharp
let doThingsAsync url =
    async {
        let! data = getDataAsync url
        ...
    }
```

<span data-ttu-id="960dc-134">Jeśli powiążesz wywołanie z wyrażeniem obliczeniowym z `let`, wynik wyrażenia obliczeń nie zostanie pobrany.</span><span class="sxs-lookup"><span data-stu-id="960dc-134">If you bind the call to a computation expression with `let`, you will not get the result of the computation expression.</span></span> <span data-ttu-id="960dc-135">Zamiast tego nastąpi powiązanie wartości *niezrealizowanego* wywołania tego wyrażenia obliczeń.</span><span class="sxs-lookup"><span data-stu-id="960dc-135">Instead, you will have bound the value of the *unrealized* call to that computation expression.</span></span> <span data-ttu-id="960dc-136">Użyj `let!`, aby powiązać z wynikiem.</span><span class="sxs-lookup"><span data-stu-id="960dc-136">Use `let!` to bind to the result.</span></span>

<span data-ttu-id="960dc-137">`let!` jest definiowana przez `Bind(x, f)` składową w typie konstruktora.</span><span class="sxs-lookup"><span data-stu-id="960dc-137">`let!` is defined by the `Bind(x, f)` member on the builder type.</span></span>

### `do!`

<span data-ttu-id="960dc-138">Słowo kluczowe `do!` jest przeznaczone do wywoływania wyrażenia obliczeń, które zwraca typ podobny do `unit`(zdefiniowany przez `Zero` element członkowski w konstruktorze):</span><span class="sxs-lookup"><span data-stu-id="960dc-138">The `do!` keyword is for calling a computation expression that returns a `unit`-like type (defined by the `Zero` member on the builder):</span></span>

```fsharp
let doThingsAsync data url =
    async {
        do! submitData data url
        ...
    }
```

<span data-ttu-id="960dc-139">W przypadku [asynchronicznego przepływu pracy](asynchronous-workflows.md)ten typ jest `Async<unit>`.</span><span class="sxs-lookup"><span data-stu-id="960dc-139">For the [async workflow](asynchronous-workflows.md), this type is `Async<unit>`.</span></span> <span data-ttu-id="960dc-140">W przypadku innych wyrażeń obliczeniowych typ jest prawdopodobnie `CExpType<unit>`.</span><span class="sxs-lookup"><span data-stu-id="960dc-140">For other computation expressions, the type is likely to be `CExpType<unit>`.</span></span>

<span data-ttu-id="960dc-141">`do!` jest definiowana przez `Bind(x, f)` składową w typie konstruktora, gdzie `f` generuje `unit`.</span><span class="sxs-lookup"><span data-stu-id="960dc-141">`do!` is defined by the `Bind(x, f)` member on the builder type, where `f` produces a `unit`.</span></span>

### `yield`

<span data-ttu-id="960dc-142">Słowo kluczowe `yield` jest przeznaczone do zwracania wartości z wyrażenia obliczeń, aby można było go użyć jako <xref:System.Collections.Generic.IEnumerable%601>:</span><span class="sxs-lookup"><span data-stu-id="960dc-142">The `yield` keyword is for returning a value from the computation expression so that it can be consumed as an <xref:System.Collections.Generic.IEnumerable%601>:</span></span>

```fsharp
let squares =
    seq {
        for i in 1..10 do
            yield i * i
    }

for sq in squares do
    printfn "%d" sq
```

<span data-ttu-id="960dc-143">W większości przypadków może być pominięty przez wywołujących.</span><span class="sxs-lookup"><span data-stu-id="960dc-143">In most cases, it can be omitted by callers.</span></span> <span data-ttu-id="960dc-144">Najbardziej typowym sposobem pominięcia `yield` jest operator `->`:</span><span class="sxs-lookup"><span data-stu-id="960dc-144">The most common way to omit `yield` is with the `->` operator:</span></span>

```fsharp
let squares =
    seq {
        for i in 1..10 -> i * i
    }

for sq in squares do
    printfn "%d" sq
```

<span data-ttu-id="960dc-145">W przypadku bardziej złożonych wyrażeń, które mogą zwracać wiele różnych wartości i może być warunkowo, można po prostu pominąć słowo kluczowe:</span><span class="sxs-lookup"><span data-stu-id="960dc-145">For more complex expressions that might yield many different values, and perhaps conditionally, simply omitting the keyword can do:</span></span>

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

<span data-ttu-id="960dc-146">Podobnie jak w przypadku [słowa kluczowego Yield w C# ](../../csharp/language-reference/keywords/yield.md), każdy element w wyrażeniu obliczenia jest obliczany w miarę wykonywania iteracji.</span><span class="sxs-lookup"><span data-stu-id="960dc-146">As with the [yield keyword in C#](../../csharp/language-reference/keywords/yield.md), each element in the computation expression is yielded back as it is iterated.</span></span>

<span data-ttu-id="960dc-147">`yield` jest definiowana przez `Yield(x)` składową w typie konstruktora, gdzie `x` jest elementem, który ma zostać przywrócony.</span><span class="sxs-lookup"><span data-stu-id="960dc-147">`yield` is defined by the `Yield(x)` member on the builder type, where `x` is the item to yield back.</span></span>

### `yield!`

<span data-ttu-id="960dc-148">Słowo kluczowe `yield!` służy do spłaszczania kolekcji wartości z wyrażenia obliczeń:</span><span class="sxs-lookup"><span data-stu-id="960dc-148">The `yield!` keyword is for flattening a collection of values from a computation expression:</span></span>

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

printfn "%A" squaresAndCubes // Prints - 1; 4; 9; 1; 8; 27
```

<span data-ttu-id="960dc-149">Podczas oceniania wyrażenie obliczeniowe wywoływane przez `yield!` będzie miało swoje elementy po jednym z nich, spłaszczony wynik.</span><span class="sxs-lookup"><span data-stu-id="960dc-149">When evaluated, the computation expression called by `yield!` will have its items yielded back one-by-one, flattening the result.</span></span>

<span data-ttu-id="960dc-150">`yield!` jest definiowana przez `YieldFrom(x)` składową w typie konstruktora, gdzie `x` jest kolekcją wartości.</span><span class="sxs-lookup"><span data-stu-id="960dc-150">`yield!` is defined by the `YieldFrom(x)` member on the builder type, where `x` is a collection of values.</span></span>

<span data-ttu-id="960dc-151">W przeciwieństwie do `yield`, `yield!` musi być jawnie określony.</span><span class="sxs-lookup"><span data-stu-id="960dc-151">Unlike `yield`, `yield!` must be explicitly specified.</span></span> <span data-ttu-id="960dc-152">Zachowanie nie jest niejawne w wyrażeniach obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="960dc-152">Its behavior isn't implicit in computation expressions.</span></span>

### `return`

<span data-ttu-id="960dc-153">Słowo kluczowe `return` otacza wartość w typie odpowiadającym wyrażeniu obliczenia.</span><span class="sxs-lookup"><span data-stu-id="960dc-153">The `return` keyword wraps a value in the type corresponding to the computation expression.</span></span> <span data-ttu-id="960dc-154">Oprócz wyrażeń obliczeniowych używających `yield`, służy do "ukończenia" wyrażenia obliczeń:</span><span class="sxs-lookup"><span data-stu-id="960dc-154">Aside from computation expressions using `yield`, it is used to "complete" a computation expression:</span></span>

```fsharp
let req = // 'req' is of type is 'Async<data>'
    async {
        let! data = fetch url
        return data
    }

// 'result' is of type 'data'
let result = Async.RunSynchronously req
```

<span data-ttu-id="960dc-155">`return` jest definiowana przez `Return(x)` składową w typie konstruktora, gdzie `x` jest elementem, który ma być zawijany.</span><span class="sxs-lookup"><span data-stu-id="960dc-155">`return` is defined by the `Return(x)` member on the builder type, where `x` is the item to wrap.</span></span>

### `return!`

<span data-ttu-id="960dc-156">Słowo kluczowe `return!` realizuje wartość wyrażenia obliczeń i zawija ten wynik w typie odpowiadającym wyrażeniu obliczenia:</span><span class="sxs-lookup"><span data-stu-id="960dc-156">The `return!` keyword realizes the value of a computation expression and wraps that result in the type corresponding to the computation expression:</span></span>

```fsharp
let req = // 'req' is of type is 'Async<data>'
    async {
        return! fetch url
    }

// 'result' is of type 'data'
let result = Async.RunSynchronously req
```

<span data-ttu-id="960dc-157">`return!` jest definiowana przez `ReturnFrom(x)` składową w typie konstruktora, gdzie `x` jest innym wyrażeniem obliczeniowym.</span><span class="sxs-lookup"><span data-stu-id="960dc-157">`return!` is defined by the `ReturnFrom(x)` member on the builder type, where `x` is another computation expression.</span></span>

### `match!`

<span data-ttu-id="960dc-158">Słowo kluczowe `match!` umożliwia wbudowanie wywołanie innego wyrażenia obliczenia i dopasowania do wzorca w wyniku:</span><span class="sxs-lookup"><span data-stu-id="960dc-158">The `match!` keyword allows you to inline a call to another computation expression and pattern match on its result:</span></span>

```fsharp
let doThingsAsync url =
    async {
        match! callService url with
        | Some data -> ...
        | None -> ...
    }
```

<span data-ttu-id="960dc-159">Podczas wywoływania wyrażenia obliczeń z `match!`, będzie to miało wynik wywołania, takie jak `let!`.</span><span class="sxs-lookup"><span data-stu-id="960dc-159">When calling a computation expression with `match!`, it will realize the result of the call like `let!`.</span></span> <span data-ttu-id="960dc-160">Jest to często używane podczas wywoływania wyrażenia obliczeń, gdzie wynik jest [opcjonalny](options.md).</span><span class="sxs-lookup"><span data-stu-id="960dc-160">This is often used when calling a computation expression where the result is an [optional](options.md).</span></span>

## <a name="built-in-computation-expressions"></a><span data-ttu-id="960dc-161">Wbudowane wyrażenia obliczeń</span><span class="sxs-lookup"><span data-stu-id="960dc-161">Built-in computation expressions</span></span>

<span data-ttu-id="960dc-162">F# Podstawowa Biblioteka definiuje trzy wbudowane wyrażenia obliczeń: [wyrażenia sekwencji](sequences.md), [asynchroniczne przepływy pracy](asynchronous-workflows.md)i [wyrażenia zapytań](query-expressions.md).</span><span class="sxs-lookup"><span data-stu-id="960dc-162">The F# core library defines three built-in computation expressions: [Sequence Expressions](sequences.md), [Asynchronous Workflows](asynchronous-workflows.md), and [Query Expressions](query-expressions.md).</span></span>

## <a name="creating-a-new-type-of-computation-expression"></a><span data-ttu-id="960dc-163">Tworzenie nowego typu wyrażenia obliczeń</span><span class="sxs-lookup"><span data-stu-id="960dc-163">Creating a New Type of Computation Expression</span></span>

<span data-ttu-id="960dc-164">Można zdefiniować charakterystykę własnych wyrażeń obliczeniowych, tworząc klasę konstruktora i definiując niektóre specjalne metody klasy.</span><span class="sxs-lookup"><span data-stu-id="960dc-164">You can define the characteristics of your own computation expressions by creating a builder class and defining certain special methods on the class.</span></span> <span data-ttu-id="960dc-165">Klasa konstruktora może opcjonalnie definiować metody wymienione w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="960dc-165">The builder class can optionally define the methods as listed in the following table.</span></span>

<span data-ttu-id="960dc-166">W poniższej tabeli opisano metody, których można użyć w klasie Konstruktor przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="960dc-166">The following table describes methods that can be used in a workflow builder class.</span></span>

|<span data-ttu-id="960dc-167">**— Metoda**</span><span class="sxs-lookup"><span data-stu-id="960dc-167">**Method**</span></span>|<span data-ttu-id="960dc-168">**Typowe sygnatury**</span><span class="sxs-lookup"><span data-stu-id="960dc-168">**Typical signature(s)**</span></span>|<span data-ttu-id="960dc-169">**Opis**</span><span class="sxs-lookup"><span data-stu-id="960dc-169">**Description**</span></span>|
|----|----|----|
|`Bind`|`M<'T> * ('T -> M<'U>) -> M<'U>`|<span data-ttu-id="960dc-170">Wywoływana dla `let!` i `do!` w wyrażeniach obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="960dc-170">Called for `let!` and `do!` in computation expressions.</span></span>|
|`Delay`|`(unit -> M<'T>) -> M<'T>`|<span data-ttu-id="960dc-171">Zawija wyrażenie obliczeń jako funkcję.</span><span class="sxs-lookup"><span data-stu-id="960dc-171">Wraps a computation expression as a function.</span></span>|
|`Return`|`'T -> M<'T>`|<span data-ttu-id="960dc-172">Wywoływana dla `return` w wyrażeniach obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="960dc-172">Called for `return` in computation expressions.</span></span>|
|`ReturnFrom`|`M<'T> -> M<'T>`|<span data-ttu-id="960dc-173">Wywoływana dla `return!` w wyrażeniach obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="960dc-173">Called for `return!` in computation expressions.</span></span>|
|`Run`|<span data-ttu-id="960dc-174">`M<'T> -> M<'T>` lub</span><span class="sxs-lookup"><span data-stu-id="960dc-174">`M<'T> -> M<'T>` or</span></span><br /><br />`M<'T> -> 'T`|<span data-ttu-id="960dc-175">Wykonuje wyrażenie obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="960dc-175">Executes a computation expression.</span></span>|
|`Combine`|<span data-ttu-id="960dc-176">`M<'T> * M<'T> -> M<'T>` lub</span><span class="sxs-lookup"><span data-stu-id="960dc-176">`M<'T> * M<'T> -> M<'T>` or</span></span><br /><br />`M<unit> * M<'T> -> M<'T>`|<span data-ttu-id="960dc-177">Wywoływana dla sekwencjonowania w wyrażeniach obliczeń.</span><span class="sxs-lookup"><span data-stu-id="960dc-177">Called for sequencing in computation expressions.</span></span>|
|`For`|<span data-ttu-id="960dc-178">`seq<'T> * ('T -> M<'U>) -> M<'U>` lub</span><span class="sxs-lookup"><span data-stu-id="960dc-178">`seq<'T> * ('T -> M<'U>) -> M<'U>` or</span></span><br /><br />`seq<'T> * ('T -> M<'U>) -> seq<M<'U>>`|<span data-ttu-id="960dc-179">Wywoływana dla wyrażeń `for...do` w wyrażeniach obliczeń.</span><span class="sxs-lookup"><span data-stu-id="960dc-179">Called for `for...do` expressions in computation expressions.</span></span>|
|`TryFinally`|`M<'T> * (unit -> unit) -> M<'T>`|<span data-ttu-id="960dc-180">Wywoływana dla wyrażeń `try...finally` w wyrażeniach obliczeń.</span><span class="sxs-lookup"><span data-stu-id="960dc-180">Called for `try...finally` expressions in computation expressions.</span></span>|
|`TryWith`|`M<'T> * (exn -> M<'T>) -> M<'T>`|<span data-ttu-id="960dc-181">Wywoływana dla wyrażeń `try...with` w wyrażeniach obliczeń.</span><span class="sxs-lookup"><span data-stu-id="960dc-181">Called for `try...with` expressions in computation expressions.</span></span>|
|`Using`|`'T * ('T -> M<'U>) -> M<'U> when 'T :> IDisposable`|<span data-ttu-id="960dc-182">Wywoływana dla `use` powiązań w wyrażeniach obliczeń.</span><span class="sxs-lookup"><span data-stu-id="960dc-182">Called for `use` bindings in computation expressions.</span></span>|
|`While`|`(unit -> bool) * M<'T> -> M<'T>`|<span data-ttu-id="960dc-183">Wywoływana dla wyrażeń `while...do` w wyrażeniach obliczeń.</span><span class="sxs-lookup"><span data-stu-id="960dc-183">Called for `while...do` expressions in computation expressions.</span></span>|
|`Yield`|`'T -> M<'T>`|<span data-ttu-id="960dc-184">Wywoływana dla wyrażeń `yield` w wyrażeniach obliczeń.</span><span class="sxs-lookup"><span data-stu-id="960dc-184">Called for `yield` expressions in computation expressions.</span></span>|
|`YieldFrom`|`M<'T> -> M<'T>`|<span data-ttu-id="960dc-185">Wywoływana dla wyrażeń `yield!` w wyrażeniach obliczeń.</span><span class="sxs-lookup"><span data-stu-id="960dc-185">Called for `yield!` expressions in computation expressions.</span></span>|
|`Zero`|`unit -> M<'T>`|<span data-ttu-id="960dc-186">Wywoływana dla pustych `else` rozgałęzień wyrażeń `if...then` w wyrażeniach obliczeń.</span><span class="sxs-lookup"><span data-stu-id="960dc-186">Called for empty `else` branches of `if...then` expressions in computation expressions.</span></span>|
|`Quote`|`Quotations.Expr<'T> -> Quotations.Expr<'T>`|<span data-ttu-id="960dc-187">Wskazuje, że wyrażenie obliczenia jest przesyłane do składowej `Run` jako cytat.</span><span class="sxs-lookup"><span data-stu-id="960dc-187">Indicates that the computation expression is passed to the `Run` member as a quotation.</span></span> <span data-ttu-id="960dc-188">Tłumaczy wszystkie wystąpienia obliczeń na cytat.</span><span class="sxs-lookup"><span data-stu-id="960dc-188">It translates all instances of a computation into a quotation.</span></span>|

<span data-ttu-id="960dc-189">Wiele metod w klasie konstruktora używa i zwraca konstrukcję `M<'T>`, która jest zazwyczaj odrębnie zdefiniowany typ, który charakteryzuje rodzaj obliczeń, na przykład, `Async<'T>` dla asynchronicznych przepływów pracy i `Seq<'T>` dla przepływów pracy sekwencji.</span><span class="sxs-lookup"><span data-stu-id="960dc-189">Many of the methods in a builder class use and return an `M<'T>` construct, which is typically a separately defined type that characterizes the kind of computations being combined, for example, `Async<'T>` for asynchronous workflows and `Seq<'T>` for sequence workflows.</span></span> <span data-ttu-id="960dc-190">Sygnatury tych metod umożliwiają ich łączenie i zagnieżdżanie ze sobą, aby obiekt przepływu pracy zwrócony z jednej konstrukcji mógł zostać przekazana do następnego.</span><span class="sxs-lookup"><span data-stu-id="960dc-190">The signatures of these methods enable them to be combined and nested with each other, so that the workflow object returned from one construct can be passed to the next.</span></span> <span data-ttu-id="960dc-191">Kompilator, gdy analizuje wyrażenie obliczeń, konwertuje wyrażenie na serię wywołań funkcji zagnieżdżonych przy użyciu metod w powyższej tabeli i kodu w wyrażeniu obliczeniowym.</span><span class="sxs-lookup"><span data-stu-id="960dc-191">The compiler, when it parses a computation expression, converts the expression into a series of nested function calls by using the methods in the preceding table and the code in the computation expression.</span></span>

<span data-ttu-id="960dc-192">Wyrażenie zagnieżdżone ma następującą postać:</span><span class="sxs-lookup"><span data-stu-id="960dc-192">The nested expression is of the following form:</span></span>

```fsharp
builder.Run(builder.Delay(fun () -> {| cexpr |}))
```

<span data-ttu-id="960dc-193">W powyższym kodzie wywołania `Run` i `Delay` są pomijane, jeśli nie są zdefiniowane w klasie konstruktora wyrażeń obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="960dc-193">In the above code, the calls to `Run` and `Delay` are omitted if they are not defined in the computation expression builder class.</span></span> <span data-ttu-id="960dc-194">Treść wyrażenia obliczeń, która jest oznaczona jako `{| cexpr |}`, jest tłumaczona na wywołania obejmujące metody klasy konstruktora przez tłumaczenia opisane w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="960dc-194">The body of the computation expression, here denoted as `{| cexpr |}`, is translated into calls involving the methods of the builder class by the translations described in the following table.</span></span> <span data-ttu-id="960dc-195">Wyrażenie obliczenia `{| cexpr |}` jest zdefiniowane cyklicznie zgodnie z tymi tłumaczeniami, w których `expr` jest F# wyrażeniem, a `cexpr` jest wyrażeniem obliczeniowym.</span><span class="sxs-lookup"><span data-stu-id="960dc-195">The computation expression `{| cexpr |}` is defined recursively according to these translations where `expr` is an F# expression and `cexpr` is a computation expression.</span></span>

|<span data-ttu-id="960dc-196">Wyrażenie</span><span class="sxs-lookup"><span data-stu-id="960dc-196">Expression</span></span>|<span data-ttu-id="960dc-197">{1&gt;Translacja&lt;1}</span><span class="sxs-lookup"><span data-stu-id="960dc-197">Translation</span></span>|
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

<span data-ttu-id="960dc-198">W poprzedniej tabeli `other-expr` zawiera opis wyrażenia, które nie jest w przeciwnym wypadku wymienione w tabeli.</span><span class="sxs-lookup"><span data-stu-id="960dc-198">In the previous table, `other-expr` describes an expression that is not otherwise listed in the table.</span></span> <span data-ttu-id="960dc-199">Klasa konstruktora nie musi implementować wszystkich metod i obsługiwać wszystkich tłumaczeń wymienionych w poprzedniej tabeli.</span><span class="sxs-lookup"><span data-stu-id="960dc-199">A builder class does not need to implement all of the methods and support all of the translations listed in the previous table.</span></span> <span data-ttu-id="960dc-200">Te konstrukcje, które nie są zaimplementowane, nie są dostępne w wyrażeniach obliczeń tego typu.</span><span class="sxs-lookup"><span data-stu-id="960dc-200">Those constructs that are not implemented are not available in computation expressions of that type.</span></span> <span data-ttu-id="960dc-201">Na przykład, jeśli nie chcesz obsługiwać słowa kluczowego `use` w wyrażeniach obliczeń, możesz pominąć definicję `Use` w klasie konstruktora.</span><span class="sxs-lookup"><span data-stu-id="960dc-201">For example, if you do not want to support the `use` keyword in your computation expressions, you can omit the definition of `Use` in your builder class.</span></span>

<span data-ttu-id="960dc-202">Poniższy przykład kodu pokazuje wyrażenie obliczeniowe, które hermetyzuje obliczenia jako serię kroków, które można ocenić jeden krok w danym momencie.</span><span class="sxs-lookup"><span data-stu-id="960dc-202">The following code example shows a computation expression that encapsulates a computation as a series of steps that can be evaluated one step at a time.</span></span> <span data-ttu-id="960dc-203">Typ Unii rozłącznej, `OkOrException`, koduje stan błędu wyrażenia jako obliczone do tej pory.</span><span class="sxs-lookup"><span data-stu-id="960dc-203">A discriminated union type, `OkOrException`, encodes the error state of the expression as evaluated so far.</span></span> <span data-ttu-id="960dc-204">Ten kod ilustruje kilka typowych wzorców, których można użyć w wyrażeniach obliczeń, takich jak implementacje standardowe niektórych metod konstruktora.</span><span class="sxs-lookup"><span data-stu-id="960dc-204">This code demonstrates several typical patterns that you can use in your computation expressions, such as boilerplate implementations of some of the builder methods.</span></span>

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
        printfn " x = %d" x
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

<span data-ttu-id="960dc-205">Wyrażenie obliczeniowe ma typ podstawowy, który zwraca wyrażenie.</span><span class="sxs-lookup"><span data-stu-id="960dc-205">A computation expression has an underlying type, which the expression returns.</span></span> <span data-ttu-id="960dc-206">Typ podstawowy może reprezentować obliczony wynik lub opóźnione obliczenie, które może być wykonane, lub może być sposobem na iterację w przypadku niektórych typów kolekcji.</span><span class="sxs-lookup"><span data-stu-id="960dc-206">The underlying type may represent a computed result or a delayed computation that can be performed, or it may provide a way to iterate through some type of collection.</span></span> <span data-ttu-id="960dc-207">W poprzednim przykładzie typ podstawowy był **ostatecznie**.</span><span class="sxs-lookup"><span data-stu-id="960dc-207">In the previous example, the underlying type was **Eventually**.</span></span> <span data-ttu-id="960dc-208">Dla wyrażenia sekwencji typem podstawowym jest <xref:System.Collections.Generic.IEnumerable%601?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="960dc-208">For a sequence expression, the underlying type is <xref:System.Collections.Generic.IEnumerable%601?displayProperty=nameWithType>.</span></span> <span data-ttu-id="960dc-209">Dla wyrażenia zapytania typ podstawowy jest <xref:System.Linq.IQueryable?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="960dc-209">For a query expression, the underlying type is <xref:System.Linq.IQueryable?displayProperty=nameWithType>.</span></span> <span data-ttu-id="960dc-210">Dla asynchronicznego przepływu pracy typ podstawowy jest [`Async`](https://msdn.microsoft.com/library/03eb4d12-a01a-4565-a077-5e83f17cf6f7).</span><span class="sxs-lookup"><span data-stu-id="960dc-210">For an asynchronous workflow, the underlying type is [`Async`](https://msdn.microsoft.com/library/03eb4d12-a01a-4565-a077-5e83f17cf6f7).</span></span> <span data-ttu-id="960dc-211">Obiekt `Async` reprezentuje prace, które mają zostać wykonane w celu obliczenia wyniku.</span><span class="sxs-lookup"><span data-stu-id="960dc-211">The `Async` object represents the work to be performed to compute the result.</span></span> <span data-ttu-id="960dc-212">Na przykład można wywołać [`Async.RunSynchronously`](https://msdn.microsoft.com/library/0a6663a9-50f2-4d38-8bf3-cefd1a51fd6b) , aby wykonać obliczenia i zwrócić wynik.</span><span class="sxs-lookup"><span data-stu-id="960dc-212">For example, you call [`Async.RunSynchronously`](https://msdn.microsoft.com/library/0a6663a9-50f2-4d38-8bf3-cefd1a51fd6b) to execute a computation and return the result.</span></span>

## <a name="custom-operations"></a><span data-ttu-id="960dc-213">Operacje niestandardowe</span><span class="sxs-lookup"><span data-stu-id="960dc-213">Custom Operations</span></span>

<span data-ttu-id="960dc-214">Istnieje możliwość zdefiniowania niestandardowej operacji w wyrażeniu obliczenia i użycia niestandardowej operacji jako operatora w wyrażeniu obliczeniowym.</span><span class="sxs-lookup"><span data-stu-id="960dc-214">You can define a custom operation on a computation expression and use a custom operation as an operator in a computation expression.</span></span> <span data-ttu-id="960dc-215">Na przykład można uwzględnić operator zapytania w wyrażeniu zapytania.</span><span class="sxs-lookup"><span data-stu-id="960dc-215">For example, you can include a query operator in a query expression.</span></span> <span data-ttu-id="960dc-216">Podczas definiowania niestandardowej operacji należy zdefiniować wartość Yield i dla metod w wyrażeniu obliczenia.</span><span class="sxs-lookup"><span data-stu-id="960dc-216">When you define a custom operation, you must define the Yield and For methods in the computation expression.</span></span> <span data-ttu-id="960dc-217">Aby zdefiniować niestandardową operację, należy umieścić ją w klasie konstruktora dla wyrażenia obliczeń, a następnie zastosować [`CustomOperationAttribute`](https://msdn.microsoft.com/library/199f3927-79df-484b-ba66-85f58cc49b19).</span><span class="sxs-lookup"><span data-stu-id="960dc-217">To define a custom operation, put it in a builder class for the computation expression, and then apply the [`CustomOperationAttribute`](https://msdn.microsoft.com/library/199f3927-79df-484b-ba66-85f58cc49b19).</span></span> <span data-ttu-id="960dc-218">Ten atrybut przyjmuje ciąg jako argument, który jest nazwą, która ma być używana w operacji niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="960dc-218">This attribute takes a string as an argument, which is the name to be used in a custom operation.</span></span> <span data-ttu-id="960dc-219">Ta nazwa znajduje się w zakresie na początku otwierającego nawiasu klamrowego wyrażenia obliczeń.</span><span class="sxs-lookup"><span data-stu-id="960dc-219">This name comes into scope at the start of the opening curly brace of the computation expression.</span></span> <span data-ttu-id="960dc-220">W związku z tym nie należy używać identyfikatorów, które mają taką samą nazwę jak operacja niestandardowa w tym bloku.</span><span class="sxs-lookup"><span data-stu-id="960dc-220">Therefore, you shouldn’t use identifiers that have the same name as a custom operation in this block.</span></span> <span data-ttu-id="960dc-221">Na przykład Unikaj używania identyfikatorów, takich jak `all` lub `last` w wyrażeniach zapytań.</span><span class="sxs-lookup"><span data-stu-id="960dc-221">For example, avoid the use of identifiers such as `all` or `last` in query expressions.</span></span>

### <a name="extending-existing-builders-with-new-custom-operations"></a><span data-ttu-id="960dc-222">Rozszerzanie istniejących konstruktorów przy użyciu nowych operacji niestandardowych</span><span class="sxs-lookup"><span data-stu-id="960dc-222">Extending existing Builders with new Custom Operations</span></span>

<span data-ttu-id="960dc-223">Jeśli masz już klasę konstruktora, jej operacje niestandardowe można rozszerzyć spoza tej klasy konstruktora.</span><span class="sxs-lookup"><span data-stu-id="960dc-223">If you already have a builder class, its custom operations can be extended from outside of this builder class.</span></span> <span data-ttu-id="960dc-224">Rozszerzenia muszą być zadeklarowane w modułach.</span><span class="sxs-lookup"><span data-stu-id="960dc-224">Extensions must be declared in modules.</span></span> <span data-ttu-id="960dc-225">Przestrzenie nazw nie mogą zawierać składowych rozszerzenia, z wyjątkiem tego samego pliku i tej samej grupy deklaracji przestrzeni nazw, w której jest zdefiniowany typ.</span><span class="sxs-lookup"><span data-stu-id="960dc-225">Namespaces cannot contain extension members except in the same file and the same namespace declaration group where the type is defined.</span></span>

<span data-ttu-id="960dc-226">Poniższy przykład pokazuje rozszerzenie istniejącej klasy `Microsoft.FSharp.Linq.QueryBuilder`.</span><span class="sxs-lookup"><span data-stu-id="960dc-226">The following example shows the extension of the existing `Microsoft.FSharp.Linq.QueryBuilder` class.</span></span>

```fsharp
type Microsoft.FSharp.Linq.QueryBuilder with

    [<CustomOperation("existsNot")>]
    member _.ExistsNot (source: QuerySource<'T, 'Q>, predicate) =
        Enumerable.Any (source.Source, Func<_,_>(predicate)) |> not
```

## <a name="see-also"></a><span data-ttu-id="960dc-227">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="960dc-227">See also</span></span>

- [<span data-ttu-id="960dc-228">Dokumentacja języka F#</span><span class="sxs-lookup"><span data-stu-id="960dc-228">F# Language Reference</span></span>](index.md)
- [<span data-ttu-id="960dc-229">Asynchroniczne przepływy pracy</span><span class="sxs-lookup"><span data-stu-id="960dc-229">Asynchronous Workflows</span></span>](asynchronous-workflows.md)
- [<span data-ttu-id="960dc-230">Sekwencje</span><span class="sxs-lookup"><span data-stu-id="960dc-230">Sequences</span></span>](https://msdn.microsoft.com/library/6b773b6b-9c9a-4af8-bd9e-d96585c166db)
- [<span data-ttu-id="960dc-231">Wyrażenia zapytania</span><span class="sxs-lookup"><span data-stu-id="960dc-231">Query Expressions</span></span>](query-expressions.md)
