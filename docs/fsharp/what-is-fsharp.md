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
# <a name="what-is-f"></a>Co to jest F\#

F # to funkcjonalny język programowania, dzięki któremu można łatwo pisać kod poprawny i łatwiejszy w obsłudze.

Programowanie języka F # polega głównie na definiowaniu typów i funkcji, które są automatycznie wywnioskowane i uogólnione. Pozwala to skupić się na domenie problemu i manipulowaniu swoimi danymi, a nie szczegółami programowania.

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

Język F # ma wiele funkcji, w tym:

* Składnia uproszczona
* Domyślnie niezmienne
* Wnioskowanie o typie i automatyczne uogólnianie
* Funkcje pierwszoklasowe
* Zaawansowane typy danych
* Dopasowanie do wzorca
* Programowanie asynchroniczne

Pełny zestaw funkcji opisano w dokumentacji [języka F #](./language-reference/index.md).

## <a name="rich-data-types"></a>Zaawansowane typy danych

Typy danych, takie jak [rekordy](./language-reference/records.md) i [związki rozłącznych](./language-reference/discriminated-unions.md) , umożliwiają przedstawianie złożonych danych i domen.

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

Rekordy F # i unie rozłączne mają domyślnie wartości inne niż null, niemodyfikowalne i porównywalne, co ułatwia ich używanie.

## <a name="enforced-correctness-with-functions-and-pattern-matching"></a>Wymuszone poprawność przy użyciu funkcji i dopasowania do wzorca

Funkcje języka F # są łatwe do zadeklarować i zaawansowane w ramach ćwiczeń. W połączeniu z [dopasowywaniem do wzorca](./language-reference/pattern-matching.md)pozwala na definiowanie zachowania, którego poprawność jest wymuszana przez kompilator.

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

Funkcje języka F # są również pierwszym klasą, co oznacza, że mogą być przesyłane jako parametry i zwracane z innych funkcji.

## <a name="functions-to-define-operations-on-objects"></a>Funkcje do definiowania operacji na obiektach

Język F # ma pełną obsługę obiektów, które są przydatnymi typami danych w przypadku konieczności mieszania danych i funkcjonalności. Funkcje języka F # są używane do manipulowania obiektami.

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

Zamiast pisać kod, który jest zorientowany obiektowo w języku F #, często piszesz kod, który traktuje obiekty jako inny typ danych do manipulowania. Funkcje, takie jak [interfejsy rodzajowe](./language-reference/interfaces.md), [wyrażenia obiektów](./language-reference/object-expressions.md)i rozsądne użycie [elementów członkowskich](./language-reference/members/index.md) , są wspólne w większych programach w języku F #.

## <a name="next-steps"></a>Następne kroki

Aby dowiedzieć się więcej na temat większego zestawu funkcji języka F #, zapoznaj się z [samouczkiem dotyczącym języka f #](tour.md).
