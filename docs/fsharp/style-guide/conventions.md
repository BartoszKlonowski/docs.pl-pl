---
title: C# — konwencje kodowania
description: Zapoznaj się z ogólnymi wskazówkami i idiomy podczas pisania F# kodu.
ms.date: 01/15/2020
ms.openlocfilehash: ca86bcf714d2fb4ee5f173ee54ba12c317f9abe7
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/24/2020
ms.locfileid: "76737822"
---
# <a name="f-coding-conventions"></a>C# — konwencje kodowania

Następujące konwencje są formułowane z doświadczenia w pracy z F# dużymi bazami kodu. [Pięć zasad dobrego F# kodu](index.md#five-principles-of-good-f-code) jest podstawą każdego zalecenia. Są one powiązane ze [ F# wskazówkami dotyczącymi projektowania składników](component-design-guidelines.md), ale mają zastosowanie F# do dowolnego kodu, a nie tylko składników, takich jak biblioteki.

## <a name="organizing-code"></a>Organizowanie kodu

F#oferuje dwa podstawowe sposoby organizowania kodu: moduły i przestrzenie nazw. Są one podobne, ale mają następujące różnice:

* Przestrzenie nazw są kompilowane jako przestrzenie nazw platformy .NET. Moduły są kompilowane jako klasy statyczne.
* Obszary nazw są zawsze najwyższego poziomu. Moduły mogą być najwyższego poziomu i zagnieżdżone w innych modułach.
* Przestrzenie nazw mogą obejmować wiele plików. Moduły nie mogą.
* Moduły mogą mieć `[<RequireQualifiedAccess>]` i `[<AutoOpen>]`.

Poniższe wskazówki ułatwią ich użycie do organizowania kodu.

### <a name="prefer-namespaces-at-the-top-level"></a>Preferuj obszary nazw na najwyższym poziomie

Dla każdego publicznego kodu, przestrzenie nazw są preferencyjne dla modułów na najwyższego poziomu. Ponieważ są one kompilowane jako przestrzenie nazw .NET, są one konsumowane z C# powodu braku problemu.

```fsharp
// Good!
namespace MyCode

type MyClass() =
    ...
```

Korzystanie z modułu najwyższego poziomu może nie wyglądać inaczej, gdy jest F#wywoływana tylko z C# , ale dla odbiorców, osoby wywołujące mogą być zaskoczenie, aby zakwalifikować `MyClass` z modułem `MyCode`.

```fsharp
// Bad!
module MyCode

type MyClass() =
    ...
```

### <a name="carefully-apply-autoopen"></a>Starannie stosuj `[<AutoOpen>]`

Konstrukcja `[<AutoOpen>]` może obsłużyć zanieczyszczenie zakresu tego, co jest dostępne dla obiektów wywołujących, i odpowiedzi na to, z których pochodzi element, jest "Magic". Nie jest to dobry efekt. Wyjątkiem od F# tej reguły jest sama biblioteka podstawowa (chociaż jest to również bit kontrowersyjny).

Jednak jest to wygodne, jeśli masz funkcje pomocnika dla publicznego interfejsu API, który ma być zorganizowany niezależnie od tego publicznego interfejsu API.

```fsharp
module MyAPI =
    [<AutoOpen>]
    module private Helpers =
        let helper1 x y z =
            ...

    let myFunction1 x =
        let y = ...
        let z = ...

        helper1 x y z
```

Dzięki temu można oddzielić szczegóły implementacji z publicznego interfejsu API funkcji bez konieczności pełnego kwalifikowania pomocnika przy każdym wywołaniu.

Ponadto udostępnianie metod rozszerzających i konstruktorów wyrażeń na poziomie przestrzeni nazw może być starannie wyrażone `[<AutoOpen>]`.

### <a name="use-requirequalifiedaccess-whenever-names-could-conflict-or-you-feel-it-helps-with-readability"></a>Użyj `[<RequireQualifiedAccess>]` za każdym razem, gdy nazwy mogą występować w konflikcie lub można je łatwo odczytać

Dodanie `[<RequireQualifiedAccess>]` atrybutu do modułu wskazuje, że moduł nie może być otwarty i że odwołania do elementów modułu wymagają jawnego kwalifikowanego dostępu. Na przykład moduł `Microsoft.FSharp.Collections.List` ma ten atrybut.

Jest to przydatne, gdy funkcje i wartości w module mają nazwy, które mogą powodować konflikt z nazwami w innych modułach. Wymaganie dostępu kwalifikowanego może znacznie zwiększyć długoterminową konserwację i możliwość rozwijania biblioteki.

```fsharp
[<RequireQualifiedAccess>]
module StringTokenization =
    let parse s = ...

...

let s = getAString()
let parsed = StringTokenization.parse s // Must qualify to use 'parse'
```

### <a name="sort-open-statements-topologically"></a>Sortuj instrukcje `open` topologically

W F#programie porządek deklaracji, w tym instrukcje `open`. Jest to w odróżnieniu C#od tego, czy efekt `using` i `using static` jest niezależny od kolejności tych instrukcji w pliku.

W F#programie elementy otwierane w zakresie mogą zasłaniać inne już obecne. Oznacza to, że zmiana kolejności instrukcji `open` może zmienić znaczenie kodu. W związku z tym nie zaleca się jakiegokolwiek sortowania wszystkich instrukcji `open` (na przykład alfanumerycznie), Lest generować różne zachowanie, które może być oczekiwane.

Zamiast tego zalecamy, aby posortować je [topologically](https://en.wikipedia.org/wiki/Topological_sorting); oznacza to, że należy zamówić instrukcje `open` w kolejności, w jakiej są zdefiniowane _warstwy_ systemu. Można również rozważyć sortowanie alfanumeryczne w różnych warstwach topologiczny.

Oto przykład sortowania topologiczny dla publicznego pliku interfejsu API usługi F# kompilatora:

```fsharp
namespace Microsoft.FSharp.Compiler.SourceCodeServices

open System
open System.Collections.Generic
open System.Collections.Concurrent
open System.Diagnostics
open System.IO
open System.Reflection
open System.Text

open Microsoft.FSharp.Compiler
open Microsoft.FSharp.Compiler.AbstractIL
open Microsoft.FSharp.Compiler.AbstractIL.Diagnostics
open Microsoft.FSharp.Compiler.AbstractIL.IL
open Microsoft.FSharp.Compiler.AbstractIL.ILBinaryReader
open Microsoft.FSharp.Compiler.AbstractIL.Internal
open Microsoft.FSharp.Compiler.AbstractIL.Internal.Library

open Microsoft.FSharp.Compiler.AccessibilityLogic
open Microsoft.FSharp.Compiler.Ast
open Microsoft.FSharp.Compiler.CompileOps
open Microsoft.FSharp.Compiler.CompileOptions
open Microsoft.FSharp.Compiler.Driver
open Microsoft.FSharp.Compiler.ErrorLogger
open Microsoft.FSharp.Compiler.Infos
open Microsoft.FSharp.Compiler.InfoReader
open Microsoft.FSharp.Compiler.Lexhelp
open Microsoft.FSharp.Compiler.Layout
open Microsoft.FSharp.Compiler.Lib
open Microsoft.FSharp.Compiler.NameResolution
open Microsoft.FSharp.Compiler.PrettyNaming
open Microsoft.FSharp.Compiler.Parser
open Microsoft.FSharp.Compiler.Range
open Microsoft.FSharp.Compiler.Tast
open Microsoft.FSharp.Compiler.Tastops
open Microsoft.FSharp.Compiler.TcGlobals
open Microsoft.FSharp.Compiler.TypeChecker
open Microsoft.FSharp.Compiler.SourceCodeServices.SymbolHelpers

open Internal.Utilities
open Internal.Utilities.Collections
```

Należy zauważyć, że podział wiersza oddziela warstwy topologiczny, przy czym każda warstwa jest sortowana alfanumerycznie. To przejrzyste organizuje kod bez przypadkowego przesłaniania wartości.

## <a name="use-classes-to-contain-values-that-have-side-effects"></a>Użyj klas, aby zawierać wartości, które mają efekty uboczne

Istnieje wiele przypadków, w których inicjowanie wartości może mieć efekty uboczne, takie jak utworzenie wystąpienia kontekstu dla bazy danych lub innego zasobu zdalnego. Zachęcamy do inicjowania takich elementów w module i używania jej w kolejnych funkcjach:

```fsharp
// This is bad!
module MyApi =
    let dep1 = File.ReadAllText "/Users/{your name}/connectionstring.txt"
    let dep2 = Environment.GetEnvironmentVariable "DEP_2"

    let private r = Random()
    let dep3() = r.Next() // Problematic if multiple threads use this

    let function1 arg = doStuffWith dep1 dep2 dep3 arg
    let function2 arg = doSutffWith dep1 dep2 dep3 arg
```

Jest to często niewłaściwy pomysł z kilku powodów:

Najpierw konfiguracja aplikacji jest wypychana do bazy kodu z `dep1` i `dep2`. Jest to trudne do utrzymania w dużych bazach kodu.

Drugie, statycznie zainicjowane dane nie powinny zawierać wartości, które nie są bezpieczne dla wątków, jeśli składnik będzie używał wielu wątków. Jest to wyraźnie naruszone przez `dep3`.

Na koniec Inicjalizacja modułu kompiluje się do konstruktora statycznego dla całej jednostki kompilacji. Jeśli w tym module wystąpi błąd w programie Let-Bound Value, manifestuje jako `TypeInitializationException`, który następnie jest buforowany przez cały okres istnienia aplikacji. Może to być trudne do zdiagnozowania. Zazwyczaj występuje wyjątek wewnętrzny, który można spróbować, ale jeśli nie istnieje, nie ma informacji o tym, co to jest główna przyczyna.

Zamiast tego wystarczy użyć prostej klasy do przechowywania zależności:

```fsharp
type MyParametricApi(dep1, dep2, dep3) =
    member _.Function1 arg1 = doStuffWith dep1 dep2 dep3 arg1
    member _.Function2 arg2 = doStuffWith dep1 dep2 dep3 arg2
```

Zapewnia to następujące czynności:

1. Wypychanie dowolnego stanu zależnego poza interfejsem API.
2. Konfigurację można teraz wykonać poza interfejsem API.
3. Błędy podczas inicjowania wartości zależnych nie mogą być manifestem jako `TypeInitializationException`.
4. Interfejs API jest teraz łatwiejszy do przetestowania.

## <a name="error-management"></a>Zarządzanie błędami

Zarządzanie błędami w dużych systemach jest złożone i złożonych Endeavor, a nie ma żadnych znaków w języku Silver w celu zapewnienia, że systemy są odporne na uszkodzenia i działają prawidłowo. Poniższe wskazówki powinny oferować wskazówki dotyczące nawigowania w tym trudnej przestrzeni.

### <a name="represent-error-cases-and-illegal-state-in-types-intrinsic-to-your-domain"></a>Reprezentuje przypadki błędów i niedozwolony stan w typach wewnętrznych dla domeny

W przypadku F# [Unii rozłącznych](../language-reference/discriminated-unions.md)można reprezentować wadliwy stan programu w systemie typów. Na przykład:

```fsharp
type MoneyWithdrawalResult =
    | Success of amount:decimal
    | InsufficientFunds of balance:decimal
    | CardExpired of DateTime
    | UndisclosedFailure
```

W takim przypadku istnieją trzy znane sposoby, że wycofanie pieniędzy z konta bankowego może zakończyć się niepowodzeniem. Każdy przypadek błędu jest reprezentowany w typie i w ten sposób może być traktowany bezpiecznie w całym programie.

```fsharp
let handleWithdrawal amount =
    let w = withdrawMoney amount
    match w with
    | Success am -> printfn "Successfully withdrew %f" am
    | InsufficientFunds balance -> printfn "Failed: balance is %f" balance
    | CardExpired expiredDate -> printfn "Failed: card expired on %O" expiredDate
    | UndisclosedFailure -> printfn "Failed: unknown"
```

Ogólnie rzecz biorąc, jeśli można modelować różne sposoby, w których coś może **się nie powieść** w domenie, kod obsługi błędu nie jest już traktowany jako element, który należy zastanowić oprócz zwykłego przepływu programu. Jest to po prostu część normalnego przepływu programu i nie jest uważana za **wyjątkową**. Istnieją dwie podstawowe korzyści:

1. Jest to łatwiejsze w obsłudze, ponieważ zmienia się w miarę upływu czasu.
2. Przypadki błędów są łatwiejsze do testowania jednostkowego.

### <a name="use-exceptions-when-errors-cannot-be-represented-with-types"></a>Użyj wyjątków, gdy błędy nie mogą być reprezentowane za pomocą typów

Nie wszystkie błędy mogą być reprezentowane w domenie problemu. Tego rodzaju błędy mają *wyjątkowe* cechy, a tym samym możliwość podniesienia i przechwycenia wyjątków w F#.

Najpierw zaleca się zapoznanie się ze [wskazówkami dotyczącymi projektowania wyjątków](../../standard/design-guidelines/exceptions.md). Mają one również zastosowanie do F#.

Główne konstrukcje dostępne w F# celu podniesienia wyjątków należy uwzględnić w następującej kolejności:

| Funkcja | Składnia | Cel |
|----------|--------|---------|
| `nullArg` | `nullArg "argumentName"` | Podnosi `System.ArgumentNullException` z określoną nazwą argumentu. |
| `invalidArg` | `invalidArg "argumentName" "message"` | Podnosi `System.ArgumentException` z określoną nazwą argumentu i komunikatem. |
| `invalidOp` | `invalidOp "message"` | Podnosi `System.InvalidOperationException` z określonym komunikatem. |
|`raise`| `raise (ExceptionType("message"))` | Mechanizm ogólnego przeznaczenia do zgłaszania wyjątków. |
| `failwith` | `failwith "message"` | Podnosi `System.Exception` z określonym komunikatem. |
| `failwithf` | `failwithf "format string" argForFormatString` | Wywołuje `System.Exception` z komunikatem określonym przez ciąg formatu i jego dane wejściowe. |

Użyj `nullArg`, `invalidArg` i `invalidOp` jako mechanizm do rzutowania `ArgumentNullException`, `ArgumentException` i `InvalidOperationException` w razie potrzeby.

Należy generalnie unikać `failwith` i `failwithf`, ponieważ powodują one wystąpienie podstawowego `Exception` typu, a nie konkretnego wyjątku. Zgodnie z [zaleceniami dotyczącymi projektowania wyjątków](../../standard/design-guidelines/exceptions.md), możesz w razie potrzeby zgłosić bardziej szczegółowe wyjątki.

### <a name="using-exception-handling-syntax"></a>Używanie składni obsługi wyjątków

F#obsługuje wzorce wyjątków za pośrednictwem składni `try...with`:

```fsharp
try
    tryGetFileContents()
with
| :? System.IO.FileNotFoundException as e -> // Do something with it here
| :? System.Security.SecurityException as e -> // Do something with it here
```

Uzgadnianie funkcjonalności do wykonania w celu przeprowadzenia wyjątku z dopasowaniem do wzorca może być nieprzerwaną lewę, jeśli chcesz zachować czysty kod. Jednym z nich jest użycie [aktywnych wzorców](../language-reference/active-patterns.md) jako środka do pogrupowania funkcjonalności otaczającej przypadek błędu z samym wyjątkiem. Na przykład może być zużywany interfejs API, który zgłasza wyjątek, w metadanych wyjątku ujmuje cenne informacje. Odpakowanie przydatnej wartości w treści przechwyconego wyjątku wewnątrz aktywnego wzorca i zwrócenie tej wartości może być przydatne w niektórych sytuacjach.

### <a name="do-not-use-monadic-error-handling-to-replace-exceptions"></a>Nie używaj obsługi błędów monadic w celu zastąpienia wyjątków

Wyjątki są widoczne jako dość Taboo w programowaniu funkcjonalnym. W rzeczywistości wyjątki naruszają czystość, dlatego można bezpiecznie rozważyć ich niedziałanie. Jednak ignoruje to stan, w którym należy uruchomić kod, i mogą wystąpić błędy w czasie wykonywania. Ogólnie rzecz biorąc Napisz kod w założeniu, że większość rzeczy nie jest czysta ani łączna, aby zminimalizować nieprzyjemne niespodziewane.

Ważne jest, aby wziąć pod uwagę następujące podstawowe zalety/aspekty wyjątków w odniesieniu do ich znaczenia i adekwatności w środowisku uruchomieniowym .NET i ekosystemie wielu języków jako całości:

1. Zawierają one szczegółowe informacje diagnostyczne, które są bardzo przydatne podczas debugowania problemu.
2. Są one dobrze zrozumiałe dla środowiska uruchomieniowego i innych języków .NET.
3. Umożliwiają one zredukowanie znaczącego standardu w porównaniu z kodem, który jest używany do *uniknięcia* wyjątków przez implementację pewnego podzestawu semantyki na zasadzie ad hoc.

Ten trzeci punkt jest krytyczny. W przypadku nieskomplikowanych operacji złożonych użycie wyjątków może skutkować użyciem struktur takich jak:

```fsharp
Result<Result<MyType, string>, string list>
```

Dzięki czemu można łatwo prowadzić do delikatnego rozróżnienia kodu, takiego jak dopasowanie wzorca dla błędów typu "String-Type":

```fsharp
let result = doStuff()
match result with
| Ok r -> ...
| Error e ->
    if e.Contains "Error string 1" then ...
    elif e.Contains "Error string 2" then ...
    else ... // Who knows?
```

Ponadto może być skłonny do połknięcia dowolnego wyjątku w przypadku funkcji "Simple" zwracającej typ "Nice":

```fsharp
// This is bad!
let tryReadAllText (path : string) =
    try System.IO.File.ReadAllText path |> Some
    with _ -> None
```

Niestety, `tryReadAllText` może zgłosić wiele wyjątków na podstawie wyposażono rzeczy, które mogą wystąpić w systemie plików, a ten kod odrzuca wszystkie informacje o tym, co może być w stanie błędnym w Twoim środowisku. Jeśli zastąpisz ten kod z typem wyniku, wrócisz do analizy komunikatu o błędzie "stringd-Type":

```fsharp
// This is bad!
let tryReadAllText (path : string) =
    try System.IO.File.ReadAllText path |> Ok
    with e -> Error e.Message

let r = tryReadAllText "path-to-file"
match r with
| Ok text -> ...
| Error e ->
    if e.Contains "uh oh, here we go again..." then ...
    else ...
```

I umieszczenie obiektu Exception w konstruktorze `Error` tylko wymusza prawidłowe rozpatrywanie przy użyciu typu wyjątku w miejscu wywołania, a nie w funkcji. W ten sposób można utworzyć zaznaczone wyjątki, które są wielowątkowy bardzo unfun, jako wywołujący interfejs API.

Dobrym alternatywą dla powyższych przykładów jest przechwycenie *określonych* wyjątków i zwrócenie wartości znaczących w kontekście tego wyjątku. Jeśli zmodyfikujesz funkcję `tryReadAllText` w następujący sposób, `None` ma więcej znaczenia:

```fsharp
let tryReadAllTextIfPresent (path : string) =
    try System.IO.File.ReadAllText path |> Some
    with :? FileNotFoundException -> None
```

Ta funkcja będzie teraz prawidłowo obsługiwana w przypadku, gdy nie można jej odnaleźć i przypisać do zwracanej wartości. Ta wartość zwracana może być mapowana na ten przypadek błędu, podczas gdy nie są usuwane żadne informacje kontekstowe lub wymuszanie wywoływania w przypadku, gdy nie ma znaczenia w tym momencie w kodzie.

Typy takie jak `Result<'Success, 'Error>` są odpowiednie dla operacji podstawowych, gdy nie są zagnieżdżone, F# a typy opcjonalne są idealny do reprezentowania, gdy coś może zwrócić *coś* lub *nic*. Nie są one zastępowane wyjątkami, ale nie powinny być używane w próbie zastąpienia wyjątków. Zamiast tego należy je stosować w sposób rozsądny do rozwiązywania określonych aspektów zasad dotyczących zarządzania wyjątkami i błędami.

## <a name="partial-application-and-point-free-programming"></a>Programowanie częściowej aplikacji i bez punktu

F#obsługuje częściową aplikację, a więc różne sposoby programowania w stylu bez punktu. Może to być przydatne w przypadku ponownego użycia kodu w ramach modułu lub implementacji elementu, ale nie jest to ujawniane publicznie. Ogólnie rzecz biorąc, programowanie bezpunktowe nie jest sprawą i sama, i może dodać znaczną barierę poznawczyą dla osób, które nie są zanurzone w stylu.

### <a name="do-not-use-partial-application-and-currying-in-public-apis"></a>Nie używaj częściowej aplikacji i currying w publicznych interfejsach API

Przy małym wyjątku użycie częściowej aplikacji w publicznych interfejsach API może być mylące dla klientów. Zwykle wartości powiązane z `let`w F# kodzie to **wartości**, a nie **wartości funkcji**. Mieszanie wartości i wartości funkcji może skutkować zapisaniem niewielkiej liczby wierszy kodu w programie Exchange w celu uzyskania zbyt wielu obciążeń poznawczych, szczególnie jeśli są połączone z operatorami, takimi jak `>>`, do redagowania funkcji.

### <a name="consider-the-tooling-implications-for-point-free-programming"></a>Weź pod uwagę wpływ na narzędzia do programowania bez zwolnień

Funkcje rozwinięte nie etykietą argumentów. Ma to wpływ na narzędzia. Należy wziąć pod uwagę następujące dwie funkcje:

```fsharp
let func name age =
    printfn "My name is %s and I am %d years old!" name age

let funcWithApplication =
    printfn "My name is %s and I am %d years old!"
```

Obie są prawidłowymi funkcjami, ale `funcWithApplication` jest funkcją rozwinięte. Po umieszczeniu wskaźnika myszy na ich typach w edytorze zostanie wyświetlony następujący komunikat:

```fsharp
val func : name:string -> age:int -> unit

val funcWithApplication : (string -> int -> unit)
```

W witrynie wywołania etykietki narzędzi w narzędziach, takich jak Visual Studio, nie zawierają istotnych informacji dotyczących tego, co reprezentuje `string` i `int` typy danych wejściowych.

Jeśli napotkasz kod wolny w punktach, taki jak `funcWithApplication`, który jest ogólnie przydatny, zaleca się przeprowadzenie pełnego rozszerzenia η, dzięki czemu narzędzia mogą pobrać znaczące nazwy dla argumentów.

Ponadto kod wolny od punktu debugowania może być wyzwaniem, jeśli nie jest to możliwe. Narzędzia debugowania są zależne od wartości związanych z nazwami (na przykład powiązań `let`), dzięki czemu można sprawdzać wartości pośrednie w połowie wykonania. Gdy kod nie ma żadnych wartości do sprawdzenia, nie ma niczego do debugowania. W przyszłości narzędzia debugowania mogą się rozwijać w celu wypróbowania tych wartości na podstawie wcześniej wykonanych ścieżek, ale nie jest dobrym pomysłem do zabezpieczania trafień w *potencjalnych* funkcjach debugowania.

### <a name="consider-partial-application-as-a-technique-to-reduce-internal-boilerplate"></a>Rozważ użycie częściowej aplikacji jako techniki do zredukowania wewnętrznego standardowego

W przeciwieństwie do wcześniejszego punktu, częściowa aplikacja jest wspaniałego narzędzia do zredukowania typowego wewnątrz aplikacji lub bardziej szczegółowych wewnętrznych interfejsów API. Może być przydatne w przypadku testowania jednostkowego implementacji bardziej skomplikowanych interfejsów API, gdzie typowe jest często wiele rzeczy. Na przykład poniższy kod pokazuje, w jaki sposób można osiągnąć, jakie najważniejsze struktury zapewniają, że nie podejmuje zewnętrznej zależności od takiej struktury i trzeba poznać związany z nim interfejs API Bespoke.

Rozważmy na przykład następujące topografie rozwiązania:

```
MySolution.sln
|_/ImplementationLogic.fsproj
|_/ImplementationLogic.Tests.fsproj
|_/API.fsproj
```

`ImplementationLogic.fsproj` może uwidaczniać kod, taki jak:

```fsharp
module Transactions =
    let doTransaction txnContext txnType balance =
        ...

type Transactor(ctx, currentBalance) =
    member _.ExecuteTransaction(txnType) =
        Transactions.doTransaction ctx txtType currentBalance
        ...
```

Testowanie jednostkowe `Transactions.doTransaction` w `ImplementationLogic.Tests.fsproj` jest proste:

```fsharp
namespace TransactionsTestingUtil

open Transactions

module TransactionsTestable =
    let getTestableTransactionRoutine mockContext = Transactions.doTransaction mockContext
```

Częściowo stosowanie `doTransaction` z obiektem kontekstu służącego do tworzenia elementów umożliwia wywoływanie funkcji we wszystkich testach jednostkowych bez konieczności konstruowania zastosowanego kontekstu za każdym razem:

```fsharp
namespace TransactionTests

open Xunit
open TransactionTypes
open TransactionsTestingUtil
open TransactionsTestingUtil.TransactionsTestable

let testableContext =
    { new ITransactionContext with
        member _.TheFirstMember() = ...
        member _.TheSecondMember() = ... }

let transactionRoutine = getTestableTransactionRoutine testableContext

[<Fact>]
let ``Test withdrawal transaction with 0.0 for balance``() =
    let expected = ...
    let actual = transactionRoutine TransactionType.Withdraw 0.0
    Assert.Equal(expected, actual)
```

Ta technika nie powinna być uniwersalnie stosowana do całej bazy kodu, ale jest dobrym sposobem zredukowania wzorców dla skomplikowanych danych wewnętrznych i testów jednostkowych.

## <a name="access-control"></a>Kontrola dostępu

F#ma wiele opcji [kontroli dostępu](../language-reference/access-control.md)dziedziczonych z elementów dostępnych w środowisku uruchomieniowym .NET. Nie można ich używać do typów — są one również dostępne dla funkcji.

* Preferuj typy i elementy członkowskie inne niż`public`, dopóki nie będą potrzebne do publicznego użycia. Pozwala to również zminimalizować liczbę użytkowników, których to dotyczy.
* Staraj się zachować wszystkie `private`funkcje pomocnika.
* Należy rozważyć użycie `[<AutoOpen>]` w module prywatnym funkcji pomocnika, jeśli stają się one liczne.

## <a name="type-inference-and-generics"></a>Wnioskowanie o typie i typy ogólne

Wnioskowanie o typie może zaoszczędzić, wprowadzając wiele standardowych. I automatyczne uogólnianie w F# kompilatorze może pomóc napisać bardziej ogólny kod z niemal niezbędnym nakładem pracy. Te funkcje nie są jednak uniwersalne.

* Rozważ użycie etykietowania nazw argumentów z jawnymi typami w publicznych interfejsach API i nie należy polegać na wnioskach o typie.

    Przyczyną tego **jest to, że należy** mieć kontrolę nad KSZTAŁTEM interfejsu API, a nie kompilatorem. Mimo że kompilator może wykonać zadanie w odniesieniu do typów, istnieje możliwość, że kształt interfejsu API ulegnie zmianie, jeśli wewnętrzne jest zależne od zmienionego typu. Może to być to, czego potrzebujesz, ale niemal w efekcie zostanie osiągnięty istotna zmiana interfejsu API, która będzie musiała zająć się tym klientom. Zamiast tego, jeśli jawnie kontrolujesz kształt publicznego interfejsu API, możesz kontrolować te zmiany. W DDD terminy można to traktować jako warstwę chroniącą przed uszkodzeniem.

* Rozważ nadanie znaczącej nazwy argumentom ogólnym.

    O ile nie piszesz kod generyczny, który nie jest specyficzny dla konkretnej domeny, zrozumiała nazwa może pomóc innym programistom zrozumieć domenę, w której pracują. Na przykład parametr typu o nazwie `'Document` w kontekście współdziałania z bazą danych dokumentów sprawia, że typy dokumentów ogólnych mogą być akceptowane przez funkcję lub element członkowski, z którym pracujesz.

* Rozważ nazewnictwo parametrów typu ogólnego za pomocą PascalCase.

    Jest to ogólny sposób wykonywania czynności w programie .NET, dlatego zaleca się użycie PascalCase zamiast snake_case lub camelCase.

Na koniec automatyczne uogólnianie nie zawsze jest Boon dla osób, które są nowością F# lub dużą bazą kodu. W przypadku używania składników, które są ogólne, są naliczane obciążenia poznawcze. Ponadto, jeśli automatycznie uogólnione funkcje nie są używane z różnymi typami danych wejściowych (pomogą, jeśli są one przeznaczone do użycia jako takie), nie ma rzeczywistej korzyści dla nich w tym momencie. Zawsze należy wziąć pod uwagę, czy kod, który piszesz, będzie faktycznie korzystał z ogólnego.

## <a name="performance"></a>Wydajność

### <a name="prefer-structs-for-small-data-types"></a>Preferuj struktury dla małych typów danych

Używanie struktur (nazywanych również typami wartości) może często powodować zwiększenie wydajności dla pewnego kodu, ponieważ zazwyczaj unika to alokowania obiektów. Jednak struktury nie zawsze są przyciskami "Przejdź szybszy": Jeśli rozmiar danych w strukturze przekracza 16 bajtów, kopiowanie danych może często powodować więcej czasu procesora niż przy użyciu typu referencyjnego.

Aby określić, czy należy używać struktury, należy wziąć pod uwagę następujące warunki:

- Jeśli rozmiar danych wynosi 16 bajtów lub mniej.
- Jeśli istnieje duże ryzyko, że wiele z tych typów danych jest rezydentnych w pamięci w uruchomionym programie.

Jeśli stosuje się pierwszy warunek, zazwyczaj należy używać struktury. Jeśli oba mają zastosowanie, należy prawie zawsze używać struktury. Mogą wystąpić sytuacje, w których obowiązują poprzednie warunki, ale użycie struktury nie jest lepsze ani gorsze niż użycie typu referencyjnego, ale prawdopodobnie jest to rzadkie. Ważne jest, aby zawsze mierzyć przy wprowadzaniu zmian, takich jak to, chociaż nie działa na założeniu lub Intuition.

#### <a name="prefer-struct-tuples-when-grouping-small-value-types"></a>Preferuj krotek struktury podczas grupowania małych typów wartości

Należy wziąć pod uwagę następujące dwie funkcje:

```fsharp
let rec runWithTuple t offset times =
    let offsetValues x y z offset =
        (x + offset, y + offset, z + offset)

    if times <= 0 then
        t
    else
        let (x, y, z) = t
        let r = offsetValues x y z offset
        runWithTuple r offset (times - 1)

let rec runWithStructTuple t offset times =
    let offsetValues x y z offset =
        struct(x + offset, y + offset, z + offset)

    if times <= 0 then
        t
    else
        let struct(x, y, z) = t
        let r = offsetValues x y z offset
        runWithStructTuple r offset (times - 1)
```

Gdy wykonujesz testy porównawcze tych funkcji za pomocą statystycznego narzędzia do analizy porównawczej, takiego jak [BenchmarkDotNet](https://benchmarkdotnet.org/), zobaczysz, że funkcja `runWithStructTuple`, która korzysta z krotek struktur, uruchamia 40% szybciej i przydziela Brak pamięci.

Jednak te wyniki nie zawsze są w twoim własnym kodzie. Jeśli oznaczesz funkcję jako `inline`, kod, który używa spójnych kolekcji, może uzyskać pewne dodatkowe optymalizacje lub kod, który można przydzielić po prostu w sposób optymalny. Należy zawsze mierzyć wyniki przy każdej wydajności, a nigdy nie działać na podstawie założeń lub Intuition.

#### <a name="prefer-struct-records-when-the-data-type-is-small"></a>Preferuj rekordy struktury, gdy typ danych jest mały

Reguła typu kciuka opisana wcześniej również zawiera dla [ F# typów rekordów](../language-reference/records.md). Należy wziąć pod uwagę następujące typy danych i funkcje, które je przetwarzają:

```fsharp
type Point = { X: float; Y: float; Z: float }

[<Struct>]
type SPoint = { X: float; Y: float; Z: float }

let rec processPoint (p: Point) offset times =
    let inline offsetValues (p: Point) offset =
        { p with X = p.X + offset; Y = p.Y + offset; Z = p.Z + offset }

    if times <= 0 then
        p
    else
        let r = offsetValues p offset
        processPoint r offset (times - 1)

let rec processStructPoint (p: SPoint) offset times =
    let inline offsetValues (p: SPoint) offset =
        { p with X = p.X + offset; Y = p.Y + offset; Z = p.Z + offset }

    if times <= 0 then
        p
    else
        let r = offsetValues p offset
        processStructPoint r offset (times - 1)
```

Jest to podobne do poprzedniego kodu krotki, ale ten czas używa rekordów oraz wbudowanej funkcji wewnętrznej.

Gdy wykonujesz testy porównawcze tych funkcji za pomocą statystycznego narzędzia do analizy porównawczej, takiego jak [BenchmarkDotNet](https://benchmarkdotnet.org/), zobaczysz, że `processStructPoint` uruchamia niemal 60% szybciej i przydzieli nic na stercie zarządzanym.

#### <a name="prefer-struct-discriminated-unions-when-the-data-type-is-small"></a>Preferuj związki rozłącznych struktur, gdy typ danych jest mały

Poprzednie spostrzeżenia dotyczące wydajności z krotkami struktury i rekordami są również przechowywane dla [ F# związków rozłącznych](../language-reference/discriminated-unions.md). Rozważmy następujący kod:

```fsharp
    type Name = Name of string
    
    [<Struct>]
    type SName = SName of string

    let reverseName (Name s) =
        s.ToCharArray()
        |> Array.rev
        |> string
        |> Name

    let structReverseName (SName s) =
        s.ToCharArray()
        |> Array.rev
        |> string
        |> SName
```

Często definiuje się jednokrotne Unii rozłącznych, takie jak w przypadku modelowania domeny. Gdy wykonujesz testy porównawcze tych funkcji za pomocą narzędzia do analizy statystycznej, takiego jak [BenchmarkDotNet](https://benchmarkdotnet.org/), zobaczysz, że `structReverseName` działa około 25% szybciej `reverseName` niż w przypadku małych ciągów. W przypadku dużych ciągów obie metody wykonują takie same operacje. Dlatego w tym przypadku zawsze zaleca się użycie struktury. Jak wspomniano wcześniej, zawsze mierzą się i nie działają na założeniach lub Intuition.

Mimo że poprzedni przykład wskazuje, że Unia rozłączna w strukturze zapewnia lepszą wydajność, często istnieje duże zbiory zbiorów podczas modelowania domeny. Większe typy danych, takie jak, które mogą nie działać, również, jeśli są strukturami, w zależności od operacji na nich, ponieważ może być uwzględniona większa możliwość kopiowania.

### <a name="functional-programming-and-mutation"></a>Programowanie funkcjonalne i mutacja

F#wartości są domyślnie niezmienne, co umożliwia uniknięcie niektórych klas błędów (szczególnie tych, które obejmują współbieżność i równoległość). Jednak w niektórych przypadkach, aby osiągnąć optymalną (lub nawet rozsądną) wydajność czasu wykonywania lub alokacji pamięci, zakres pracy może być najlepiej zaimplementowany przy użyciu mutacji w miejscu stanu. Jest to możliwe w zasadzie zgody przy F# użyciu słowa kluczowego `mutable`.

Korzystanie z `mutable` w F# programie może być szanse z czystą funkcjonalnością. Jest to zrozumiałe, ale funkcjonalnej czystości może być szanse z celami wydajności. Naruszenie polega na hermetyzacji mutacji, tak aby wywołujący nie musieli zadbać o to, co się stanie, gdy wywoła funkcję. Dzięki temu można napisać interfejs funkcjonalny dla implementacji opartej na mutacji dla kodu krytycznego dla wydajności.

#### <a name="wrap-mutable-code-in-immutable-interfaces"></a>Zawijaj modyfikowalny kod w niezmiennych interfejsach

Ze względu na przejrzystość referencyjną należy napisać kod, który nie uwidacznia modyfikowalnych niedzwonności funkcji o kluczowym znaczeniu. Na przykład poniższy kod implementuje funkcję `Array.contains` w bibliotece F# podstawowej:

```fsharp
[<CompiledName("Contains")>]
let inline contains value (array:'T[]) =
    checkNonNull "array" array
    let mutable state = false
    let mutable i = 0
    while not state && i < array.Length do
        state <- value = array.[i]
        i <- i + 1
    state
```

Wywołanie tej funkcji wiele razy nie zmienia tablicy bazowej ani nie wymaga utrzymania żadnego modyfikowalnego stanu w jego użyciu. Jest to element przezroczysty, nawet jeśli niemal każdy wiersz kodu w nim używa mutacji.

#### <a name="consider-encapsulating-mutable-data-in-classes"></a>Rozważ hermetyzację modyfikowalnych danych w klasach

W poprzednim przykładzie użyto pojedynczej funkcji do hermetyzacji operacji przy użyciu modyfikowalnych danych. Nie zawsze jest to wystarczające dla bardziej złożonych zestawów danych. Należy wziąć pod uwagę następujące zestawy funkcji:

```fsharp
open System.Collections.Generic

let addToClosureTable (key, value) (t: Dictionary<_,_>) =
    if not (t.ContainsKey(key)) then
        t.Add(key, value)
    else
        t.[key] <- value

let closureTableCount (t: Dictionary<_,_>) = t.Count

let closureTableContains (key, value) (t: Dictionary<_, HashSet<_>>) =
    match t.TryGetValue(key) with
    | (true, v) -> v.Equals(value)
    | (false, _) -> false
```

Ten kod jest wykonywany, ale ujawnia strukturę danych opartą na mutacji, która jest odpowiedzialna za utrzymanie. Może być opakowany wewnątrz klasy bez podstawowych elementów członkowskich, które mogą ulec zmianie:

```fsharp
open System.Collections.Generic

/// The results of computing the LALR(1) closure of an LR(0) kernel
type Closure1Table() =
    let t = Dictionary<Item0, HashSet<TerminalIndex>>()

    member _.Add(key, value) =
        if not (t.ContainsKey(key)) then
            t.Add(key, value)
        else
            t.[key] <- value

    member _.Count = t.Count

    member _.Contains(key, value) =
        match t.TryGetValue(key) with
        | (true, v) -> v.Equals(value)
        | (false, _) -> false
```

`Closure1Table` hermetyzuje źródłową strukturę danych opartych na mutacji, dlatego nie wymuszają wywoływania, aby zachować podstawową strukturę danych. Klasy to zaawansowany sposób hermetyzowania danych i procedur, które są oparte na mutacji bez uwidaczniania szczegółów dla obiektów wywołujących.

#### <a name="prefer-let-mutable-to-reference-cells"></a>Preferuj `let mutable` do komórek odwołań

Komórki odwołań są sposobem reprezentowania odwołania do wartości, a nie samej wartości. Chociaż mogą one być używane w kodzie krytycznym dla wydajności, nie są zalecane. Rozważmy następujący przykład:

```fsharp
let kernels =
    let acc = ref Set.empty

    processWorkList startKernels (fun kernel ->
        if not ((!acc).Contains(kernel)) then
            acc := (!acc).Add(kernel)
        ...)

    !acc |> Seq.toList
```

Użycie komórki referencyjnej teraz spowoduje "zanieczyszczanie" jako cały kolejny kod z koniecznością wypróbowania i ponownego odwołania się do danych źródłowych. Zamiast tego należy rozważyć `let mutable`:

```fsharp
let kernels =
    let mutable acc = Set.empty

    processWorkList startKernels (fun kernel ->
        if not (acc.Contains(kernel)) then
            acc <- acc.Add(kernel)
        ...)

    acc |> Seq.toList
```

Poza pojedynczym punktem mutacji w środku wyrażenia lambda, cały inny kod, który dotyka `acc`, może to zrobić w sposób, który nie różni się od użycia normalnej `let`j wartości. Ułatwi to zmianę z upływem czasu.

## <a name="object-programming"></a>Programowanie obiektów

F#ma pełną obsługę obiektów i koncepcje zorientowane obiektowo (OO). Chociaż wiele koncepcji OO są zaawansowane i przydatne, nie wszystkie z nich są idealne do użycia. Poniższe listy zawierają wskazówki dotyczące kategorii funkcji OO na wysokim poziomie.

**Rozważ użycie tych funkcji w wielu sytuacjach:**

* Notacja kropki (`x.Length`)
* Elementy członkowskie wystąpienia
* Konstruktory niejawne
* Statyczne składowe
* Indexer — notacja (`arr.[x]`)
* Argumenty nazwane i opcjonalne
* Interfejsy i implementacje interfejsów

**Nie dołączaj do tych funkcji w pierwszej kolejności, ale należy je zastosować w rozsądny sposób, jeśli są wygodne do rozwiązania problemu:**

* Przeciążanie metody
* Hermetyzowane dane modyfikowalne
* Operatory dla typów
* Właściwości autowypełniające
* Implementowanie `IDisposable` i `IEnumerable`
* Rozszerzenia typu
* Zdarzenia
* Struktury
* Delegaty
* Wyliczenia

**Ogólnie rzecz biorąc, należy unikać tych funkcji, chyba że trzeba ich używać:**

* Hierarchie typów oparte na dziedziczeniu i dziedziczenie implementacji
* Wartości null i `Unchecked.defaultof<_>`

### <a name="prefer-composition-over-inheritance"></a>Preferuj składanie przez dziedziczenie

[Składanie przez dziedziczenie](https://en.wikipedia.org/wiki/Composition_over_inheritance) to długotrwała idiom, która F# może być zgodna z dobrym kodem. Podstawowa zasada polega na tym, że nie należy ujawniać klasy bazowej i wymuszać wywoływania dziedziczenia z tej klasy podstawowej w celu uzyskania funkcjonalności.

### <a name="use-object-expressions-to-implement-interfaces-if-you-dont-need-a-class"></a>Użyj wyrażeń obiektów do zaimplementowania interfejsów, jeśli nie potrzebujesz klasy

[Wyrażenia obiektów](../language-reference/object-expressions.md) umożliwiają zaimplementowanie interfejsów na bieżąco, powiązanie zaimplementowanego interfejsu z wartością bez konieczności wykonywania tej czynności wewnątrz klasy. Jest to wygodne, zwłaszcza jeśli trzeba zaimplementować interfejs i nie _ma potrzeby dla_ pełnej klasy.

Na przykład jest to kod, który jest uruchamiany w [Ionide](http://ionide.io/) , aby zapewnić akcję naprawy kodu, jeśli dodano symbol, dla którego nie masz instrukcji `open`:

```fsharp
    let private createProvider () =
        { new CodeActionProvider with
            member this.provideCodeActions(doc, range, context, ct) =
                let diagnostics = context.diagnostics
                let diagnostic = diagnostics |> Seq.tryFind (fun d -> d.message.Contains "Unused open statement")
                let res =
                    match diagnostic with
                    | None -> [||]
                    | Some d ->
                        let line = doc.lineAt d.range.start.line
                        let cmd = createEmpty<Command>
                        cmd.title <- "Remove unused open"
                        cmd.command <- "fsharp.unusedOpenFix"
                        cmd.arguments <- Some ([| doc |> unbox; line.range |> unbox; |] |> ResizeArray)
                        [|cmd |]
                res
                |> ResizeArray
                |> U2.Case1
        }
```

Ponieważ nie ma potrzeby stosowania klasy podczas korzystania z interfejsu API Visual Studio Code, wyrażenia obiektów są idealnym narzędziem dla tego elementu. Są one również przydatne w przypadku testów jednostkowych, gdy chcesz utworzyć skrót do interfejsu z procedurami testów w trybie ad hoc.

## <a name="consider-type-abbreviations-to-shorten-signatures"></a>Rozważ użycie skrótów typów w celu skrócenia sygnatur

[Skróty typów](../language-reference/type-abbreviations.md) są wygodnym sposobem przypisywania etykiety do innego typu, takiego jak sygnatura funkcji lub bardziej złożony typ. Na przykład poniższy alias przypisuje etykietę do elementów potrzebnych do zdefiniowania obliczeń za pomocą [CNTK](https://docs.microsoft.com/cognitive-toolkit/), biblioteki uczenia głębokiego:

```fsharp
open CNTK

// DeviceDescriptor, Variable, and Function all come from CNTK
type Computation = DeviceDescriptor -> Variable -> Function
```

Nazwa `Computation` jest wygodnym sposobem, aby zauważyć każdą funkcję, która jest zgodna z podpisem aliasu. Używanie skrótów typów, takich jak takie, jest wygodne i pozwala na bardziej zwięzły kod.

### <a name="avoid-using-type-abbreviations-to-represent-your-domain"></a>Unikaj używania skrótów typu do reprezentowania Twojej domeny

Chociaż skróty typów są wygodne do nadawania nazwy podpisom funkcji, mogą one być mylące, gdy abbreviating inne typy. Rozważmy następujący skrót:

```fsharp
// Does not actually abstract integers.
type BufferSize = int
```

Może to być mylące na wiele sposobów:

* `BufferSize` nie jest abstrakcją; jest to tylko inna nazwa dla liczby całkowitej.
* Jeśli `BufferSize` jest uwidoczniona w publicznym interfejsie API, może być łatwo interpretowana jako "tylko `int`". Ogólnie rzecz biorąc, typy domeny mają wiele atrybutów i nie są typami pierwotnymi, takimi jak `int`. Ten skrót narusza te założenia.
* Wielkość liter w `BufferSize` (PascalCase) oznacza, że ten typ zawiera więcej danych.
* Ten alias nie oferuje większej przejrzystości w porównaniu z udostępnianiem nazwanego argumentu funkcji.
* Skrót nie będzie manifestować w skompilowanej IL; jest to tylko liczba całkowita, a ten alias to konstrukcja czasu kompilacji.

```fsharp
module Networking =
    ...
    let send data (bufferSize: int) = ...
```

Podsumowując, Pitfall z skrótami typu polega na tym, że **nie** są abstrakcją dla typów, które są abbreviating. W poprzednim przykładzie `BufferSize` jest tylko `int` w obszarze okładek, bez dodatkowych danych ani żadnych korzyści z systemu typów oprócz tego, co `int` już posiadane.

Alternatywnym podejściem do korzystania z skrótów typu do reprezentowania domeny jest użycie Unii rozłącznych o pojedynczej wielkości liter. Poprzedni przykład można modelować w następujący sposób:

```fsharp
type BufferSize = BufferSize of int
```

Jeśli napiszesz kod, który działa w kontekście `BufferSize` i jego wartości źródłowej, musisz utworzyć jeden, a nie przekazywać w dowolny liczbę całkowitą:

```fsharp
module Networking =
    ...
    let send data (BufferSize size) =
    ...
```

Zmniejsza to prawdopodobieństwo błędnego przełączenia dowolnej liczby całkowitej do funkcji `send`, ponieważ obiekt wywołujący musi skonstruować typ `BufferSize`, aby otoczyć wartość przed wywołaniem funkcji.
