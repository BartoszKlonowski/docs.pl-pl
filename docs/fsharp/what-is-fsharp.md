---
title: Co to jest F#
description: 'Dowiedz się, co to jest język programowania F # i jakie jest programowanie w języku F #. Dowiedz się więcej o zaawansowanych typach danych, funkcjach i sposobach ich dopasowania.'
ms.date: 08/03/2018
ms.openlocfilehash: a6bad3e1db63c3fe948b5916925d5eb24a18a41c
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96739480"
---
# <a name="what-is-f"></a><span data-ttu-id="5ffeb-104">Co to jest F\#</span><span class="sxs-lookup"><span data-stu-id="5ffeb-104">What is F\#</span></span>

<span data-ttu-id="5ffeb-105">F # to funkcjonalny język programowania, dzięki któremu można łatwo pisać kod poprawny i łatwiejszy w obsłudze.</span><span class="sxs-lookup"><span data-stu-id="5ffeb-105">F# is a functional programming language that makes it easy to write correct and maintainable code.</span></span>

<span data-ttu-id="5ffeb-106">Programowanie języka F # polega głównie na definiowaniu typów i funkcji, które są automatycznie wywnioskowane i uogólnione.</span><span class="sxs-lookup"><span data-stu-id="5ffeb-106">F# programming primarily involves defining types and functions that are type-inferred and generalized automatically.</span></span> <span data-ttu-id="5ffeb-107">Pozwala to skupić się na domenie problemu i manipulowaniu swoimi danymi, a nie szczegółami programowania.</span><span class="sxs-lookup"><span data-stu-id="5ffeb-107">This allows your focus to remain on the problem domain and manipulating its data, rather than the details of programming.</span></span>

```fsharp
open System // Gets access to functionality in System namespace.

// Defines a function that takes a name and produces a greeting.
let getGreeting name = $"Hello, {name}! Isn't F# great?"

[<EntryPoint>]
let main args =
    // Defines a list of names
    let names = [ "Don"; "Julia"; "Xi" ]

    // Prints a greeting for each name!
    names
    |> List.map getGreeting
    |> List.iter (fun greeting -> printfn $"{greeting}")

    0
```

<span data-ttu-id="5ffeb-108">Język F # ma wiele funkcji, w tym:</span><span class="sxs-lookup"><span data-stu-id="5ffeb-108">F# has numerous features, including:</span></span>

* <span data-ttu-id="5ffeb-109">Składnia uproszczona</span><span class="sxs-lookup"><span data-stu-id="5ffeb-109">Lightweight syntax</span></span>
* <span data-ttu-id="5ffeb-110">Domyślnie niezmienne</span><span class="sxs-lookup"><span data-stu-id="5ffeb-110">Immutable by default</span></span>
* <span data-ttu-id="5ffeb-111">Wnioskowanie o typie i automatyczne uogólnianie</span><span class="sxs-lookup"><span data-stu-id="5ffeb-111">Type inference and automatic generalization</span></span>
* <span data-ttu-id="5ffeb-112">Funkcje pierwszoklasowe</span><span class="sxs-lookup"><span data-stu-id="5ffeb-112">First-class functions</span></span>
* <span data-ttu-id="5ffeb-113">Zaawansowane typy danych</span><span class="sxs-lookup"><span data-stu-id="5ffeb-113">Powerful data types</span></span>
* <span data-ttu-id="5ffeb-114">Dopasowanie do wzorca</span><span class="sxs-lookup"><span data-stu-id="5ffeb-114">Pattern matching</span></span>
* <span data-ttu-id="5ffeb-115">Programowanie asynchroniczne</span><span class="sxs-lookup"><span data-stu-id="5ffeb-115">Async programming</span></span>

<span data-ttu-id="5ffeb-116">Pełny zestaw funkcji opisano w dokumentacji [języka F #](./language-reference/index.md).</span><span class="sxs-lookup"><span data-stu-id="5ffeb-116">A full set of features are documented in the [F# language reference](./language-reference/index.md).</span></span>

## <a name="rich-data-types"></a><span data-ttu-id="5ffeb-117">Zaawansowane typy danych</span><span class="sxs-lookup"><span data-stu-id="5ffeb-117">Rich data types</span></span>

<span data-ttu-id="5ffeb-118">Typy danych, takie jak [rekordy](./language-reference/records.md) i [związki rozłącznych](./language-reference/discriminated-unions.md) , umożliwiają przedstawianie złożonych danych i domen.</span><span class="sxs-lookup"><span data-stu-id="5ffeb-118">Data types such as [Records](./language-reference/records.md) and [Discriminated Unions](./language-reference/discriminated-unions.md) let you represent complex data and domains.</span></span>

```fsharp
// Group data with Records
type SuccessfulWithdrawal =
    { Amount: decimal
      Balance: decimal }

type FailedWithdrawal =
    { Amount: decimal
      Balance: decimal
      IsOverdraft: bool }

// Use discriminated unions to represent data of 1 or more forms
type WithdrawalResult =
    | Success of SuccessfulWithdrawal
    | InsufficientFunds of FailedWithdrawal
    | CardExpired of System.DateTime
    | UndisclosedFailure
```

<span data-ttu-id="5ffeb-119">Rekordy F # i unie rozłączne mają domyślnie wartości inne niż null, niemodyfikowalne i porównywalne, co ułatwia ich używanie.</span><span class="sxs-lookup"><span data-stu-id="5ffeb-119">F# records and discriminated unions are non-null, immutable, and comparable by default, making them very easy to use.</span></span>

## <a name="enforced-correctness-with-functions-and-pattern-matching"></a><span data-ttu-id="5ffeb-120">Wymuszone poprawność przy użyciu funkcji i dopasowania do wzorca</span><span class="sxs-lookup"><span data-stu-id="5ffeb-120">Enforced correctness with functions and pattern matching</span></span>

<span data-ttu-id="5ffeb-121">Funkcje języka F # są łatwe do zadeklarować i zaawansowane w ramach ćwiczeń.</span><span class="sxs-lookup"><span data-stu-id="5ffeb-121">F# functions are easy to declare and powerful in practice.</span></span> <span data-ttu-id="5ffeb-122">W połączeniu z [dopasowywaniem do wzorca](./language-reference/pattern-matching.md)pozwala na definiowanie zachowania, którego poprawność jest wymuszana przez kompilator.</span><span class="sxs-lookup"><span data-stu-id="5ffeb-122">When combined with [pattern matching](./language-reference/pattern-matching.md), they allow you to define behavior whose correctness is enforced by the compiler.</span></span>

```fsharp
// Returns a WithdrawalResult
let withdrawMoney amount = // Implementation elided

let handleWithdrawal amount =
    let w = withdrawMoney amount

    // The F# compiler enforces accounting for each case!
    match w with
    | Success s -> printfn "Successfully withdrew %f{s.Amount}"
    | InsufficientFunds f -> printfn "Failed: balance is %f{f.Balance}"
    | CardExpired d -> printfn "Failed: card expired on {d}"
    | UndisclosedFailure -> printfn "Failed: unknown :("
```

<span data-ttu-id="5ffeb-123">Funkcje języka F # są również pierwszym klasą, co oznacza, że mogą być przesyłane jako parametry i zwracane z innych funkcji.</span><span class="sxs-lookup"><span data-stu-id="5ffeb-123">F# functions are also first-class, meaning they can be passed as parameters and returned from other functions.</span></span>

## <a name="functions-to-define-operations-on-objects"></a><span data-ttu-id="5ffeb-124">Funkcje do definiowania operacji na obiektach</span><span class="sxs-lookup"><span data-stu-id="5ffeb-124">Functions to define operations on objects</span></span>

<span data-ttu-id="5ffeb-125">Język F # ma pełną obsługę obiektów, które są przydatnymi typami danych w przypadku konieczności mieszania danych i funkcjonalności.</span><span class="sxs-lookup"><span data-stu-id="5ffeb-125">F# has full support for objects, which are useful data types when you need to blend data and functionality.</span></span> <span data-ttu-id="5ffeb-126">Funkcje języka F # są używane do manipulowania obiektami.</span><span class="sxs-lookup"><span data-stu-id="5ffeb-126">F# functions are used to manipulate objects.</span></span>

```fsharp
type Set<'T when 'T: comparison>(elements: seq<'T>) =
    member s.IsEmpty = // Implementation elided
    member s.Contains (value) =// Implementation elided
    member s.Add (value) = // Implementation elided
    // ...
    // Further Implementation elided
    // ...
    interface IEnumerable<‘T>
    interface IReadOnlyCollection<‘T>

module Set =
    let isEmpty (set: Set<'T>) = set.IsEmpty

    let contains element (set: Set<'T>) = set.Contains(element)

    let add value (set: Set<'T>) = set.Add(value)
```

<span data-ttu-id="5ffeb-127">Zamiast pisać kod, który jest zorientowany obiektowo w języku F #, często piszesz kod, który traktuje obiekty jako inny typ danych do manipulowania.</span><span class="sxs-lookup"><span data-stu-id="5ffeb-127">Rather than writing code that is object-oriented, in F#, you will often write code that treats objects as another data type for functions to manipulate.</span></span> <span data-ttu-id="5ffeb-128">Funkcje, takie jak [interfejsy rodzajowe](./language-reference/interfaces.md), [wyrażenia obiektów](./language-reference/object-expressions.md)i rozsądne użycie [elementów członkowskich](./language-reference/members/index.md) , są wspólne w większych programach w języku F #.</span><span class="sxs-lookup"><span data-stu-id="5ffeb-128">Features such as [generic interfaces](./language-reference/interfaces.md), [object expressions](./language-reference/object-expressions.md), and judicious use of [members](./language-reference/members/index.md) are common in larger F# programs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ffeb-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5ffeb-129">Next steps</span></span>

<span data-ttu-id="5ffeb-130">Aby dowiedzieć się więcej na temat większego zestawu funkcji języka F #, zapoznaj się z [samouczkiem dotyczącym języka f #](tour.md).</span><span class="sxs-lookup"><span data-stu-id="5ffeb-130">To learn more about a larger set of F# features, check out the [F# Tour](tour.md).</span></span>
