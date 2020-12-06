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
# <a name="results"></a>Wyniki

`Result<'T,'TFailure>`Typ pozwala pisać kod odporny na błędy, który może być składany.

## <a name="syntax"></a>Składnia

```fsharp
// The definition of Result in FSharp.Core
[<StructuralEquality; StructuralComparison>]
[<CompiledName("FSharpResult`2")>]
[<Struct>]
type Result<'T,'TError> =
    | Ok of ResultValue:'T
    | Error of ErrorValue:'TError
```

## <a name="remarks"></a>Uwagi

Zapoznaj się z [`Result`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-resultmodule.html) modułem wbudowanej kombinatorów dla `Result` . Wprowadź.

Należy zauważyć, że typ wyniku to [Unia](discriminated-unions.md#struct-discriminated-unions)rozłączna struktury. W tym miejscu są stosowane semantyka równości strukturalnej.

`Result`Typ jest zazwyczaj używany w obsłudze błędów monadic, który jest często określany jako [programowanie zorientowane na szyny](https://swlaschin.gitbooks.io/fsharpforfunandprofit/content/posts/recipe-part2.html) w społeczności języka F #.  Poniższy prosty przykład ilustruje to podejście.

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

Jak widać, bardzo łatwo można łączyć łańcuchowo różne funkcje walidacji, jeśli wymusimy, aby wszystkie zwracały `Result` .  Dzięki temu można rozbić funkcje podobne do małych kawałków, które są w miarę możliwości do redagowania.  Jest to również wartość dodana do *wymuszania* użycia [dopasowania wzorca](pattern-matching.md) na końcu zaokrąglenia sprawdzania poprawności, która w ten sposób wymusza wyższy stopień poprawienia programu.

## <a name="see-also"></a>Zobacz także

- [Sumy rozłączne](discriminated-unions.md)
- [Dopasowanie wzorca](pattern-matching.md)
