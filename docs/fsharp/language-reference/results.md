---
title: Wyniki
description: 'Dowiedz się, w jaki sposób można napisać kod odporny na błędy za pomocą typu "wynik" języka F #.'
ms.date: 08/13/2020
ms.openlocfilehash: 53b1db0c9224ae032d58c06cd3c58e3dbed03f7b
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740227"
---
# <a name="results"></a><span data-ttu-id="eaa08-103">Wyniki</span><span class="sxs-lookup"><span data-stu-id="eaa08-103">Results</span></span>

<span data-ttu-id="eaa08-104">`Result<'T,'TFailure>`Typ pozwala pisać kod odporny na błędy, który może być składany.</span><span class="sxs-lookup"><span data-stu-id="eaa08-104">The `Result<'T,'TFailure>` type lets you write error-tolerant code that can be composed.</span></span>

## <a name="syntax"></a><span data-ttu-id="eaa08-105">Składnia</span><span class="sxs-lookup"><span data-stu-id="eaa08-105">Syntax</span></span>

```fsharp
// The definition of Result in FSharp.Core
[<StructuralEquality; StructuralComparison>]
[<CompiledName("FSharpResult`2")>]
[<Struct>]
type Result<'T,'TError> =
    | Ok of ResultValue:'T
    | Error of ErrorValue:'TError
```

## <a name="remarks"></a><span data-ttu-id="eaa08-106">Uwagi</span><span class="sxs-lookup"><span data-stu-id="eaa08-106">Remarks</span></span>

<span data-ttu-id="eaa08-107">Zapoznaj się z [`Result`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-resultmodule.html) modułem wbudowanej kombinatorów dla `Result` .</span><span class="sxs-lookup"><span data-stu-id="eaa08-107">See the [`Result`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-resultmodule.html) module for the built-in combinators for the `Result`.</span></span> <span data-ttu-id="eaa08-108">Wprowadź.</span><span class="sxs-lookup"><span data-stu-id="eaa08-108">type.</span></span>

<span data-ttu-id="eaa08-109">Należy zauważyć, że typ wyniku to [Unia](discriminated-unions.md#struct-discriminated-unions)rozłączna struktury.</span><span class="sxs-lookup"><span data-stu-id="eaa08-109">Note that the result type is a [struct discriminated union](discriminated-unions.md#struct-discriminated-unions).</span></span> <span data-ttu-id="eaa08-110">W tym miejscu są stosowane semantyka równości strukturalnej.</span><span class="sxs-lookup"><span data-stu-id="eaa08-110">Structural equality semantics apply here.</span></span>

<span data-ttu-id="eaa08-111">`Result`Typ jest zazwyczaj używany w obsłudze błędów monadic, który jest często określany jako [programowanie zorientowane na szyny](https://swlaschin.gitbooks.io/fsharpforfunandprofit/content/posts/recipe-part2.html) w społeczności języka F #.</span><span class="sxs-lookup"><span data-stu-id="eaa08-111">The `Result` type is typically used in monadic error-handling, which is often referred to as [Railway-oriented Programming](https://swlaschin.gitbooks.io/fsharpforfunandprofit/content/posts/recipe-part2.html) within the F# community.</span></span>  <span data-ttu-id="eaa08-112">Poniższy prosty przykład ilustruje to podejście.</span><span class="sxs-lookup"><span data-stu-id="eaa08-112">The following trivial example demonstrates this approach.</span></span>

```fsharp
// Define a simple type which has fields that can be validated
type Request =
    { Name: string
      Email: string }

// Define some logic for what defines a valid name.
//
// Generates a Result which is an Ok if the name validates;
// otherwise, it generates a Result which is an Error.
let validateName req =
    match req.Name with
    | null -> Error "No name found."
    | "" -> Error "Name is empty."
    | "bananas" -> Error "Bananas is not a name."
    | _ -> Ok req

// Similarly, define some email validation logic.
let validateEmail req =
    match req.Email with
    | null -> Error "No email found."
    | "" -> Error "Email is empty."
    | s when s.EndsWith("bananas.com") -> Error "No email from bananas.com is allowed."
    | _ -> Ok req

let validateRequest reqResult =
    reqResult
    |> Result.bind validateName
    |> Result.bind validateEmail

let test() =
    // Now, create a Request and pattern match on the result.
    let req1 = { Name = "Phillip"; Email = "phillip@contoso.biz" }
    let res1 = validateRequest (Ok req1)
    match res1 with
    | Ok req -> printfn $"My request was valid! Name: {req.Name} Email {req.Email}"  
    | Error e -> printfn $"Error: {e}"
    // Prints: "My request was valid!  Name: Phillip Email: phillip@consoto.biz"

    let req2 = { Name = "Phillip"; Email = "phillip@bananas.com" }
    let res2 = validateRequest (Ok req2)
    match res2 with
    | Ok req -> printfn $"My request was valid! Name: {req.Name} Email {req.Email}"  
    | Error e -> printfn $"Error: {e}"
    // Prints: "Error: No email from bananas.com is allowed."

test()
```

<span data-ttu-id="eaa08-113">Jak widać, bardzo łatwo można łączyć łańcuchowo różne funkcje walidacji, jeśli wymusimy, aby wszystkie zwracały `Result` .</span><span class="sxs-lookup"><span data-stu-id="eaa08-113">As you can see, it's quite easy to chain together various validation functions if you force them all to return a `Result`.</span></span>  <span data-ttu-id="eaa08-114">Dzięki temu można rozbić funkcje podobne do małych kawałków, które są w miarę możliwości do redagowania.</span><span class="sxs-lookup"><span data-stu-id="eaa08-114">This lets you break up functionality like this into small pieces which are as composable as you need them to be.</span></span>  <span data-ttu-id="eaa08-115">Jest to również wartość dodana do *wymuszania* użycia [dopasowania wzorca](pattern-matching.md) na końcu zaokrąglenia sprawdzania poprawności, która w ten sposób wymusza wyższy stopień poprawienia programu.</span><span class="sxs-lookup"><span data-stu-id="eaa08-115">This also has the added value of *enforcing* the use of [pattern matching](pattern-matching.md) at the end of a round of validation, which in turns enforces a higher degree of program correctness.</span></span>

## <a name="see-also"></a><span data-ttu-id="eaa08-116">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="eaa08-116">See also</span></span>

- [<span data-ttu-id="eaa08-117">Sumy rozłączne</span><span class="sxs-lookup"><span data-stu-id="eaa08-117">Discriminated Unions</span></span>](discriminated-unions.md)
- [<span data-ttu-id="eaa08-118">Dopasowanie wzorca</span><span class="sxs-lookup"><span data-stu-id="eaa08-118">Pattern Matching</span></span>](pattern-matching.md)
