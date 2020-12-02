---
title: 'Co nowego w języku F # 5,0 — Przewodnik po języku f #'
description: 'Zapoznaj się z omówieniem nowych funkcji dostępnych w języku F # 5,0.'
ms.date: 11/06/2020
ms.openlocfilehash: dd954fac31b008beab37cd6c1f06b1d41c5d5004
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96438009"
---
# <a name="whats-new-in-f-50"></a><span data-ttu-id="36310-103">Co nowego w języku F # 5,0</span><span class="sxs-lookup"><span data-stu-id="36310-103">What's new in F# 5.0</span></span>

<span data-ttu-id="36310-104">F # 5,0 dodaje kilka ulepszeń języka F # i F# Interactive.</span><span class="sxs-lookup"><span data-stu-id="36310-104">F# 5.0 adds several improvements to the F# language and F# Interactive.</span></span> <span data-ttu-id="36310-105">Jest on publikowany z **platformą .NET 5**.</span><span class="sxs-lookup"><span data-stu-id="36310-105">It is released with **.NET 5**.</span></span>

<span data-ttu-id="36310-106">Najnowszą wersję zestawu SDK platformy .NET można pobrać ze [strony plików do pobrania platformy .NET](https://dotnet.microsoft.com/download).</span><span class="sxs-lookup"><span data-stu-id="36310-106">You can download the latest .NET SDK from the [.NET downloads page](https://dotnet.microsoft.com/download).</span></span>

## <a name="get-started"></a><span data-ttu-id="36310-107">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="36310-107">Get started</span></span>

<span data-ttu-id="36310-108">Język F # 5,0 jest dostępny we wszystkich dystrybucjach .NET Core i narzędziach programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="36310-108">F# 5.0 is available in all .NET Core distributions and Visual Studio tooling.</span></span> <span data-ttu-id="36310-109">Aby uzyskać więcej informacji, zobacz [wprowadzenie do języka F #](../get-started/index.md) , aby dowiedzieć się więcej.</span><span class="sxs-lookup"><span data-stu-id="36310-109">For more information, see [Get started with F#](../get-started/index.md) to learn more.</span></span>

## <a name="package-references-in-f-scripts"></a><span data-ttu-id="36310-110">Odwołania do pakietów w skryptach języka F #</span><span class="sxs-lookup"><span data-stu-id="36310-110">Package references in F# scripts</span></span>

<span data-ttu-id="36310-111">Język f # 5 zapewnia obsługę odwołań do pakietów w skryptach języka F # z `#r "nuget:..."` składnią.</span><span class="sxs-lookup"><span data-stu-id="36310-111">F# 5 brings support for package references in F# scripts with `#r "nuget:..."` syntax.</span></span> <span data-ttu-id="36310-112">Rozważmy na przykład następujące odwołanie do pakietu:</span><span class="sxs-lookup"><span data-stu-id="36310-112">For example, consider the following package reference:</span></span>

```fsharp
#r "nuget: Newtonsoft.Json"

open Newtonsoft.Json

let o = {| X = 2; Y = "Hello" |}

printfn "%s" (JsonConvert.SerializeObject o)
```

<span data-ttu-id="36310-113">Możesz również podać wersję jawną po nazwie pakietu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="36310-113">You can also supply an explicit version after the name of the package like this:</span></span>

```fsharp
#r "nuget: Newtonsoft.Json,11.0.1"
```

<span data-ttu-id="36310-114">Pakiet zawiera odwołania do pakietów z natywnymi zależnościami, takimi jak ML.NET.</span><span class="sxs-lookup"><span data-stu-id="36310-114">Package references support packages with native dependencies, such as ML.NET.</span></span>

<span data-ttu-id="36310-115">Odwołania do pakietów obsługują również pakiety z specjalnymi wymaganiami dotyczącymi odwoływania się do elementów zależnych `.dll` .</span><span class="sxs-lookup"><span data-stu-id="36310-115">Package references also support packages with special requirements about referencing dependent `.dll`s.</span></span> <span data-ttu-id="36310-116">Na przykład pakiet [FParsec](https://www.nuget.org/packages/FParsec/) używany do wymagania, aby użytkownicy ręcznie upewnili się, że jego odwołanie `FParsecCS.dll` zostało odwołane jako pierwsze przed `FParsec.dll` odwołaniem do F# Interactive.</span><span class="sxs-lookup"><span data-stu-id="36310-116">For example, the [FParsec](https://www.nuget.org/packages/FParsec/) package used to require that users manually ensure that its dependent `FParsecCS.dll` was referenced first before `FParsec.dll` was referenced in F# Interactive.</span></span> <span data-ttu-id="36310-117">Nie jest to już potrzebne i można odwołać się do pakietu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="36310-117">This is no longer needed, and you can reference the package as follows:</span></span>

```fsharp
#r "nuget: FParsec"

open FParsec

let test p str =
    match run p str with
    | Success(result, _, _)   -> printfn "Success: %A" result
    | Failure(errorMsg, _, _) -> printfn "Failure: %s" errorMsg

test pfloat "1.234"
```

<span data-ttu-id="36310-118">Ta funkcja implementuje [Narzędzia języka F # RFC FST —-1027](https://github.com/fsharp/fslang-design/blob/master/tooling/FST-1027-fsi-references.md).</span><span class="sxs-lookup"><span data-stu-id="36310-118">This feature implements [F# Tooling RFC FST-1027](https://github.com/fsharp/fslang-design/blob/master/tooling/FST-1027-fsi-references.md).</span></span> <span data-ttu-id="36310-119">Aby uzyskać więcej informacji na temat odwołań do pakietów, zobacz samouczek [F# Interactive](../tools/fsharp-interactive/index.md) .</span><span class="sxs-lookup"><span data-stu-id="36310-119">For more information on package references, see the [F# Interactive](../tools/fsharp-interactive/index.md) tutorial.</span></span>

## <a name="string-interpolation"></a><span data-ttu-id="36310-120">Interpolacja ciągów</span><span class="sxs-lookup"><span data-stu-id="36310-120">String interpolation</span></span>

<span data-ttu-id="36310-121">Ciągi interpolowane języka F # są stosunkowo podobne do interpolowanych ciągów języka C# lub JavaScript, w tym, że umożliwiają pisanie kodu w "dziurach" wewnątrz literału ciągu.</span><span class="sxs-lookup"><span data-stu-id="36310-121">F# interpolated strings are fairly similar to C# or JavaScript interpolated strings, in that they let you write code in "holes" inside of a string literal.</span></span> <span data-ttu-id="36310-122">Poniżej przedstawiono prosty przykład:</span><span class="sxs-lookup"><span data-stu-id="36310-122">Here's a basic example:</span></span>

```fsharp
let name = "Phillip"
let age = 29
printfn $"Name: {name}, Age: {age}"

printfn $"I think {3.0 + 0.14} is close to {System.Math.PI}!"
```

<span data-ttu-id="36310-123">Jednakże interpolowane ciągi F # umożliwiają również wpisywanie typów interpolacji, podobnie jak `sprintf` Funkcja, aby wymusić, że wyrażenie wewnątrz interpolowanego kontekstu jest zgodne z określonym typem.</span><span class="sxs-lookup"><span data-stu-id="36310-123">However, F# interpolated strings also allow for typed interpolations, just like the `sprintf` function, to enforce that an expression inside of an interpolated context conforms to a particular type.</span></span> <span data-ttu-id="36310-124">Używa tego samego specyfikatora formatu.</span><span class="sxs-lookup"><span data-stu-id="36310-124">It uses the same format specifiers.</span></span>

```fsharp
let name = "Phillip"
let age = 29

printfn $"Name: %s{name}, Age: %d{age}"

// Error: type mismatch
printfn $"Name: %s{age}, Age: %d{name}"
```

<span data-ttu-id="36310-125">W powyższym przykładzie interpolacji, `%s` wymaga interpolacji jako typu `string` , natomiast `%d` wymaga interpolacji jako `integer` .</span><span class="sxs-lookup"><span data-stu-id="36310-125">In the preceding typed interpolation example, the `%s` requires the interpolation to be of type `string`, whereas the `%d` requires the interpolation to be an `integer`.</span></span>

<span data-ttu-id="36310-126">Ponadto dowolne dowolne wyrażenie F # (lub wyrażenia) można umieścić po stronie kontekstu interpolacji.</span><span class="sxs-lookup"><span data-stu-id="36310-126">Additionally, any arbitrary F# expression (or expressions) can be placed in side of an interpolation context.</span></span> <span data-ttu-id="36310-127">Istnieje nawet możliwość napisania bardziej skomplikowanego wyrażenia, takiego jak:</span><span class="sxs-lookup"><span data-stu-id="36310-127">It is even possible to write a more complicated expression, like so:</span></span>

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

<span data-ttu-id="36310-128">Chociaż nie zalecamy tego, aby to zrobić zbyt wiele.</span><span class="sxs-lookup"><span data-stu-id="36310-128">Although we don't recommend doing this too much in practice.</span></span>

<span data-ttu-id="36310-129">Ta funkcja implementuje [Język F # RFC FS-1001](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1001-StringInterpolation.md).</span><span class="sxs-lookup"><span data-stu-id="36310-129">This feature implements [F# RFC FS-1001](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1001-StringInterpolation.md).</span></span>

## <a name="support-for-nameof"></a><span data-ttu-id="36310-130">Obsługa nameof</span><span class="sxs-lookup"><span data-stu-id="36310-130">Support for nameof</span></span>

<span data-ttu-id="36310-131">F # 5 obsługuje `nameof` operator, który rozwiązuje symbol używany do i tworzy jego nazwę w źródle F #.</span><span class="sxs-lookup"><span data-stu-id="36310-131">F# 5 supports the `nameof` operator, which resolves the symbol it's being used for and produces its name in F# source.</span></span> <span data-ttu-id="36310-132">Jest to przydatne w różnych scenariuszach, takich jak rejestrowanie i ochrona rejestrowania przed zmianami w kodzie źródłowym.</span><span class="sxs-lookup"><span data-stu-id="36310-132">This is useful in various scenarios, such as logging, and protects your logging against changes in source code.</span></span>

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

printfn "%s" (lookupMonth 12)
printfn "%s" (lookupMonth 1)
printfn "%s" (lookupMonth 13)
```

<span data-ttu-id="36310-133">Ostatni wiersz zgłosi wyjątek, a "miesiąc" zostanie wyświetlony w komunikacie o błędzie.</span><span class="sxs-lookup"><span data-stu-id="36310-133">The last line will throw an exception and "month" will be shown in the error message.</span></span>

<span data-ttu-id="36310-134">Można przyjąć nazwę niemal każdej konstrukcji F #:</span><span class="sxs-lookup"><span data-stu-id="36310-134">You can take a name of nearly every F# construct:</span></span>

```fsharp
module M =
    let f x = nameof x

printfn "%s" (M.f 12)
printfn "%s" (nameof M)
printfn "%s" (nameof M.f)
```

<span data-ttu-id="36310-135">Trzy końcowe dodatki to zmiany wykonywane przez operatorów: dodanie `nameof<'type-parameter>` formularza dla parametrów typu ogólnego i możliwość użycia `nameof` jako wzorca w wyrażeniu dopasowania do wzorca.</span><span class="sxs-lookup"><span data-stu-id="36310-135">Three final additions are changes to how operators work: the addition of the `nameof<'type-parameter>` form for generic type parameters, and the ability to use `nameof` as a pattern in a pattern match expression.</span></span>

<span data-ttu-id="36310-136">Pobranie nazwy operatora powoduje powstanie jego ciągu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="36310-136">Taking a name of an operator gives its source string.</span></span> <span data-ttu-id="36310-137">Jeśli potrzebujesz skompilowanego formularza, użyj skompilowanej nazwy operatora:</span><span class="sxs-lookup"><span data-stu-id="36310-137">If you need the compiled form, use the compiled name of an operator:</span></span>

```fsharp
nameof(+) // "+"
nameof op_Addition // "op_Addition"
```

<span data-ttu-id="36310-138">Pobranie nazwy parametru typu wymaga nieco innej składni:</span><span class="sxs-lookup"><span data-stu-id="36310-138">Taking the name of a type parameter requires a slightly different syntax:</span></span>

```fsharp
type C<'TType> =
    member _.TypeName = nameof<'TType>
```

<span data-ttu-id="36310-139">Jest to podobne do `typeof<'T>` operatorów i `typedefof<'T>` .</span><span class="sxs-lookup"><span data-stu-id="36310-139">This is similar to the `typeof<'T>` and `typedefof<'T>` operators.</span></span>

<span data-ttu-id="36310-140">F # 5 dodaje również obsługę `nameof` wzorca, który może być używany w `match` wyrażeniach:</span><span class="sxs-lookup"><span data-stu-id="36310-140">F# 5 also adds support for a `nameof` pattern that can be used in `match` expressions:</span></span>

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

<span data-ttu-id="36310-141">Poprzedzający kod używa elementu "nameof" zamiast literału ciągu w wyrażeniu Match.</span><span class="sxs-lookup"><span data-stu-id="36310-141">The preceding code uses 'nameof' instead of the string literal in the match expression.</span></span>

<span data-ttu-id="36310-142">Ta funkcja implementuje [Język F # RFC FS-1003](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1003-nameof-operator.md).</span><span class="sxs-lookup"><span data-stu-id="36310-142">This feature implements [F# RFC FS-1003](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1003-nameof-operator.md).</span></span>

## <a name="open-type-declarations"></a><span data-ttu-id="36310-143">Otwieranie deklaracji typu</span><span class="sxs-lookup"><span data-stu-id="36310-143">Open type declarations</span></span>

<span data-ttu-id="36310-144">F # 5 dodaje również obsługę dla deklaracji typu Open.</span><span class="sxs-lookup"><span data-stu-id="36310-144">F# 5 also adds support for open type declarations.</span></span> <span data-ttu-id="36310-145">Deklaracja typu Open jest taka sama jak otwieranie klasy statycznej w języku C#, z wyjątkiem sytuacji, w której inna składnia i nieco inne zachowanie dopasowuje semantykę języka F #.</span><span class="sxs-lookup"><span data-stu-id="36310-145">An open type declaration is like opening a static class in C#, except with some different syntax and some slightly different behavior to fit F# semantics.</span></span>

<span data-ttu-id="36310-146">Za pomocą deklaracji typu Open można `open` udostępniać zawartość statyczną w obrębie tego typu.</span><span class="sxs-lookup"><span data-stu-id="36310-146">With open type declarations, you can `open` any type to expose static contents inside of it.</span></span> <span data-ttu-id="36310-147">Ponadto, możesz określić, że `open` w języku F # definicje i rekordy mają być ujawnione.</span><span class="sxs-lookup"><span data-stu-id="36310-147">Additionally, you can `open` F#-defined unions and records to expose their contents.</span></span> <span data-ttu-id="36310-148">Na przykład może to być przydatne, jeśli masz Unię zdefiniowaną w module i chcesz uzyskać do nich dostęp, ale nie chcesz otwierać całego modułu.</span><span class="sxs-lookup"><span data-stu-id="36310-148">For example, this can be useful if you have a union defined in a module and want to access its cases, but don't want to open the entire module.</span></span>

```fsharp
open type System.Math

let x = Min(1.0, 2.0)

module M =
    type DU = A | B | C

    let someOtherFunction x = x + 1

// Open only the type inside the module
open type M.DU

printfn "%A" A
```

<span data-ttu-id="36310-149">W przeciwieństwie do języka C#, `open type` w przypadku dwóch typów, które uwidaczniają składową o tej samej nazwie, element członkowski z ostatniego typu jest `open` zasłaniał inną nazwę.</span><span class="sxs-lookup"><span data-stu-id="36310-149">Unlike C#, when you `open type` on two types that expose a member with the same name, the member from the last type being `open`ed shadows the other name.</span></span> <span data-ttu-id="36310-150">Jest to zgodne z semantyką języka F # otaczającą już istniejące cieniowanie.</span><span class="sxs-lookup"><span data-stu-id="36310-150">This is consistent with F# semantics around shadowing that exist already.</span></span>

<span data-ttu-id="36310-151">Ta funkcja implementuje [Język F # RFC FS-1068](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1068-open-type-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="36310-151">This feature implements [F# RFC FS-1068](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1068-open-type-declaration.md).</span></span>

## <a name="consistent-slicing-behavior-for-built-in-data-types"></a><span data-ttu-id="36310-152">Spójne zachowanie tworzenia wycinków dla wbudowanych typów danych</span><span class="sxs-lookup"><span data-stu-id="36310-152">Consistent slicing behavior for built-in data types</span></span>

<span data-ttu-id="36310-153">Zachowanie tworzenia wycinków wbudowanych `FSharp.Core` typów danych (Array, list, String, Array 2D, tablica 3W, 4D Array) używanych jako niespójne przed F # 5.</span><span class="sxs-lookup"><span data-stu-id="36310-153">Behavior for slicing the built-in `FSharp.Core` data types (array, list, string, 2D array, 3D array, 4D array) used to not be consistent prior to F# 5.</span></span> <span data-ttu-id="36310-154">Niektóre zachowania w przypadku krawędzi wywołało wyjątek i niektóre nie.</span><span class="sxs-lookup"><span data-stu-id="36310-154">Some edge-case behavior threw an exception and some wouldn't.</span></span> <span data-ttu-id="36310-155">W języku F # 5 wszystkie wbudowane typy zwracają teraz puste wycinki dla wycinków, które nie są możliwe do wygenerowania:</span><span class="sxs-lookup"><span data-stu-id="36310-155">In F# 5, all built-in types now return empty slices for slices that are impossible to generate:</span></span>

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

<span data-ttu-id="36310-156">Ta funkcja implementuje [Język F # RFC FS-1077](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1077-tolerant-slicing.md).</span><span class="sxs-lookup"><span data-stu-id="36310-156">This feature implements [F# RFC FS-1077](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1077-tolerant-slicing.md).</span></span>

## <a name="fixed-index-slices-for-3d-and-4d-arrays-in-fsharpcore"></a><span data-ttu-id="36310-157">Wycinków o stałym indeksie dla tablic 3W i 4D w FSharp. Core</span><span class="sxs-lookup"><span data-stu-id="36310-157">Fixed-index slices for 3D and 4D arrays in FSharp.Core</span></span>

<span data-ttu-id="36310-158">Język F # 5,0 zapewnia obsługę tworzenia wycinków ze stałym indeksem w wbudowanych typach tablic 3W i 4D.</span><span class="sxs-lookup"><span data-stu-id="36310-158">F# 5.0 brings support for slicing with a fixed index in the built-in 3D and 4D array types.</span></span>

<span data-ttu-id="36310-159">Aby to zilustrować, weź pod uwagę następującą tablicę 3W:</span><span class="sxs-lookup"><span data-stu-id="36310-159">To illustrate this, consider the following 3D array:</span></span>

<span data-ttu-id="36310-160">*z = 0*</span><span class="sxs-lookup"><span data-stu-id="36310-160">*z = 0*</span></span>
| <span data-ttu-id="36310-161">x\y</span><span class="sxs-lookup"><span data-stu-id="36310-161">x\y</span></span>   | <span data-ttu-id="36310-162">0</span><span class="sxs-lookup"><span data-stu-id="36310-162">0</span></span> | <span data-ttu-id="36310-163">1</span><span class="sxs-lookup"><span data-stu-id="36310-163">1</span></span> |
|-------|---|---|
| <span data-ttu-id="36310-164">**0**</span><span class="sxs-lookup"><span data-stu-id="36310-164">**0**</span></span> | <span data-ttu-id="36310-165">0</span><span class="sxs-lookup"><span data-stu-id="36310-165">0</span></span> | <span data-ttu-id="36310-166">1</span><span class="sxs-lookup"><span data-stu-id="36310-166">1</span></span> |
| <span data-ttu-id="36310-167">**1**</span><span class="sxs-lookup"><span data-stu-id="36310-167">**1**</span></span> | <span data-ttu-id="36310-168">2</span><span class="sxs-lookup"><span data-stu-id="36310-168">2</span></span> | <span data-ttu-id="36310-169">3</span><span class="sxs-lookup"><span data-stu-id="36310-169">3</span></span> |

<span data-ttu-id="36310-170">*z = 1*</span><span class="sxs-lookup"><span data-stu-id="36310-170">*z = 1*</span></span>
| <span data-ttu-id="36310-171">x\y</span><span class="sxs-lookup"><span data-stu-id="36310-171">x\y</span></span>   | <span data-ttu-id="36310-172">0</span><span class="sxs-lookup"><span data-stu-id="36310-172">0</span></span> | <span data-ttu-id="36310-173">1</span><span class="sxs-lookup"><span data-stu-id="36310-173">1</span></span> |
|-------|---|---|
| <span data-ttu-id="36310-174">**0**</span><span class="sxs-lookup"><span data-stu-id="36310-174">**0**</span></span> | <span data-ttu-id="36310-175">4</span><span class="sxs-lookup"><span data-stu-id="36310-175">4</span></span> | <span data-ttu-id="36310-176">5</span><span class="sxs-lookup"><span data-stu-id="36310-176">5</span></span> |
| <span data-ttu-id="36310-177">**1**</span><span class="sxs-lookup"><span data-stu-id="36310-177">**1**</span></span> | <span data-ttu-id="36310-178">6</span><span class="sxs-lookup"><span data-stu-id="36310-178">6</span></span> | <span data-ttu-id="36310-179">7</span><span class="sxs-lookup"><span data-stu-id="36310-179">7</span></span> |

<span data-ttu-id="36310-180">Co zrobić, jeśli chcesz wyodrębnić wycinek `[| 4; 5 |]` z tablicy?</span><span class="sxs-lookup"><span data-stu-id="36310-180">What if you wanted to extract the slice `[| 4; 5 |]` from the array?</span></span> <span data-ttu-id="36310-181">Jest to teraz bardzo proste!</span><span class="sxs-lookup"><span data-stu-id="36310-181">This is now very simple!</span></span>

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

<span data-ttu-id="36310-182">Ta funkcja implementuje [Język F # RFC FS-1077b](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1077-3d-4d-fixed-index-slicing.md).</span><span class="sxs-lookup"><span data-stu-id="36310-182">This feature implements [F# RFC FS-1077b](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1077-3d-4d-fixed-index-slicing.md).</span></span>

## <a name="f-quotations-improvements"></a><span data-ttu-id="36310-183">Udoskonalenia cytatów języka F #</span><span class="sxs-lookup"><span data-stu-id="36310-183">F# quotations improvements</span></span>

<span data-ttu-id="36310-184">[Cytaty kodu](../language-reference/code-quotations.md) języka F # mają teraz możliwość zachowania informacji o ograniczeniach typu.</span><span class="sxs-lookup"><span data-stu-id="36310-184">F# [code quotations](../language-reference/code-quotations.md) now have the ability to retain type constraint information.</span></span> <span data-ttu-id="36310-185">Rozpatrzmy następujący przykład:</span><span class="sxs-lookup"><span data-stu-id="36310-185">Consider the following example:</span></span>

```fsharp
open FSharp.Linq.RuntimeHelpers

let eval q = LeafExpressionConverter.EvaluateQuotation q

let inline negate x = -x
// val inline negate: x: ^a ->  ^a when  ^a : (static member ( ~- ) :  ^a ->  ^a)

<@ negate 1.0 @>  |> eval
```

<span data-ttu-id="36310-186">Ograniczenie generowane przez `inline` funkcję jest zachowywane w cudzysłowie kodu.</span><span class="sxs-lookup"><span data-stu-id="36310-186">The constraint generated by the `inline` function is retained in the code quotation.</span></span> <span data-ttu-id="36310-187">`negate`Można teraz ocenić w formie cudzysłowu funkcji.</span><span class="sxs-lookup"><span data-stu-id="36310-187">The `negate` function's quoted form can now be evaluated.</span></span>

<span data-ttu-id="36310-188">Ta funkcja implementuje [Język F # RFC FS-1071](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1071-witness-passing-quotations.md).</span><span class="sxs-lookup"><span data-stu-id="36310-188">This feature implements [F# RFC FS-1071](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1071-witness-passing-quotations.md).</span></span>

## <a name="applicative-computation-expressions"></a><span data-ttu-id="36310-189">Wyrażenia obliczeń Applicative</span><span class="sxs-lookup"><span data-stu-id="36310-189">Applicative Computation Expressions</span></span>

<span data-ttu-id="36310-190">[Wyrażenia obliczeń (CE)](../language-reference/computation-expressions.md) są używane dzisiaj do modelowania "obliczeń kontekstowych" lub w bardziej funkcjonalnej terminologii programowania, monadic obliczeń.</span><span class="sxs-lookup"><span data-stu-id="36310-190">[Computation expressions (CEs)](../language-reference/computation-expressions.md) are used today to model "contextual computations", or in more functional programming-friendly terminology, monadic computations.</span></span>

<span data-ttu-id="36310-191">W języku F # 5 wprowadzono applicative CE, który oferuje inny model obliczeniowy.</span><span class="sxs-lookup"><span data-stu-id="36310-191">F# 5 introduces applicative CEs, which offer a different computational model.</span></span> <span data-ttu-id="36310-192">Applicative ce zezwala na bardziej wydajne obliczenia pod warunkiem, że każde obliczenie jest niezależne, a ich wyniki są gromadzone na końcu.</span><span class="sxs-lookup"><span data-stu-id="36310-192">Applicative CEs allow for more efficient computations provided that every computation is independent, and their results are accumulated at the end.</span></span> <span data-ttu-id="36310-193">Gdy obliczenia są niezależne od siebie, są one również proste działania równoległego, co umożliwia autorom CE pisanie bardziej wydajnych bibliotek.</span><span class="sxs-lookup"><span data-stu-id="36310-193">When computations are independent of one another, they are also trivially parallelizable, allowing CE authors to write more efficient libraries.</span></span> <span data-ttu-id="36310-194">Ta korzyść obejmuje ograniczenie, chociaż: obliczenia zależne od wcześniej obliczonych wartości są niedozwolone.</span><span class="sxs-lookup"><span data-stu-id="36310-194">This benefit comes at a restriction, though: computations that depend on previously computed values are not allowed.</span></span>

<span data-ttu-id="36310-195">W poniższym przykładzie przedstawiono podstawowe applicative CE dla `Result` typu.</span><span class="sxs-lookup"><span data-stu-id="36310-195">The follow example shows a basic applicative CE for the `Result` type.</span></span>

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
    | Ok x -> printfn "%s is: %d" (nameof res1) x
    | Error e -> printfn "%s is: %s" (nameof res1) e

let printApplicatives () =
    let r1 = Ok 2
    let r2 = Ok 3 // Error "fail!"
    let r3 = Ok 4

    run r1 r2 r3
    run r1 (Error "failure!") r3
```

<span data-ttu-id="36310-196">Jeśli jesteś autorem biblioteki, który obecnie udostępnia w swojej bibliotece usługi rejestracji certyfikatów, musisz wiedzieć kilka dodatkowych zagadnień.</span><span class="sxs-lookup"><span data-stu-id="36310-196">If you're a library author who exposes CEs in their library today, there are some additional considerations you'll need to be aware of.</span></span>

<span data-ttu-id="36310-197">Ta funkcja implementuje [Język F # RFC FS-1063](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1063-support-letbang-andbang-for-applicative-functors.md).</span><span class="sxs-lookup"><span data-stu-id="36310-197">This feature implements [F# RFC FS-1063](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1063-support-letbang-andbang-for-applicative-functors.md).</span></span>

## <a name="interfaces-can-be-implemented-at-different-generic-instantiations"></a><span data-ttu-id="36310-198">Interfejsy można zaimplementować w różnych ogólnych wystąpieniach</span><span class="sxs-lookup"><span data-stu-id="36310-198">Interfaces can be implemented at different generic instantiations</span></span>

<span data-ttu-id="36310-199">Teraz można zaimplementować ten sam interfejs w różnych wystąpieniach ogólnych:</span><span class="sxs-lookup"><span data-stu-id="36310-199">You can now implement the same interface at different generic instantiations:</span></span>

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

<span data-ttu-id="36310-200">Ta funkcja implementuje [Język F # RFC FS-1031](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1031-Allow%20implementing%20the%20same%20interface%20at%20different%20generic%20instantiations%20in%20the%20same%20type.md).</span><span class="sxs-lookup"><span data-stu-id="36310-200">This feature implements [F# RFC FS-1031](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1031-Allow%20implementing%20the%20same%20interface%20at%20different%20generic%20instantiations%20in%20the%20same%20type.md).</span></span>

## <a name="default-interface-member-consumption"></a><span data-ttu-id="36310-201">Użycie domyślnego interfejsu</span><span class="sxs-lookup"><span data-stu-id="36310-201">Default interface member consumption</span></span>

<span data-ttu-id="36310-202">Język F # 5 umożliwia korzystanie [z interfejsów z domyślnymi implementacjami](../../csharp/tutorials/default-interface-methods-versions.md).</span><span class="sxs-lookup"><span data-stu-id="36310-202">F# 5 lets you consume [interfaces with default implementations](../../csharp/tutorials/default-interface-methods-versions.md).</span></span>

<span data-ttu-id="36310-203">Rozważ użycie interfejsu zdefiniowanego w języku C# w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="36310-203">Consider an interface defined in C# like this:</span></span>

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

<span data-ttu-id="36310-204">Można go wykorzystać w F # za pomocą dowolnego standardowego sposobu implementacji interfejsu:</span><span class="sxs-lookup"><span data-stu-id="36310-204">You can consume it in F# through any of the standard means of implementing an interface:</span></span>

```fsharp
open CSharp

// You can implement the interface via a class
type MyType() =
    member _.M() = ()

    interface MyDim

let md = MyType() :> MyDim
printfn "DIM from C#: %d" md.Z

// You can also implement it via an object expression
let md' = { new MyDim }
printfn "DIM from C# but via Object Expression: %d" md'.Z
```

<span data-ttu-id="36310-205">Dzięki temu można bezpiecznie korzystać z kodu w języku C# i składników .NET zapisanych w nowoczesnej C#, gdy użytkownicy będą mogli korzystać z implementacji domyślnej.</span><span class="sxs-lookup"><span data-stu-id="36310-205">This lets you safely take advantage of C# code and .NET components written in modern C# when they expect users to be able to consume a default implementation.</span></span>

<span data-ttu-id="36310-206">Ta funkcja implementuje [Język F # RFC FS-1074](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1074-default-interface-member-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="36310-206">This feature implements [F# RFC FS-1074](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1074-default-interface-member-consumption.md).</span></span>

## <a name="simplified-interop-with-nullable-value-types"></a><span data-ttu-id="36310-207">Uproszczona międzyoperacyjna z typami wartości null</span><span class="sxs-lookup"><span data-stu-id="36310-207">Simplified interop with nullable value types</span></span>

<span data-ttu-id="36310-208">[Typy dopuszczające wartości null (o wartościach](https://docs.microsoft.com/dotnet/api/system.nullable-1) dopuszczających wartość null) były obsługiwane przez język F #, ale współpracujące z nimi są tradycyjnie nieco nieznacznie odbiegać, ponieważ trzeba utworzyć `Nullable` `Nullable<SomeType>` otokę lub za każdym razem, gdy chcesz przekazać wartość.</span><span class="sxs-lookup"><span data-stu-id="36310-208">[Nullable (value) types](https://docs.microsoft.com/dotnet/api/system.nullable-1) (called Nullable Types historically) have long been supported by F#, but interacting with them has traditionally been somewhat of a pain since you'd have to construct a `Nullable` or `Nullable<SomeType>` wrapper every time you wanted to pass a value.</span></span> <span data-ttu-id="36310-209">Teraz kompilator niejawnie przekonwertuje typ wartości na, `Nullable<ThatValueType>` Jeśli typ docelowy jest zgodny.</span><span class="sxs-lookup"><span data-stu-id="36310-209">Now the compiler will implicitly convert a value type into a `Nullable<ThatValueType>` if the target type matches.</span></span> <span data-ttu-id="36310-210">Teraz można wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="36310-210">The following code is now possible:</span></span>

```fsharp
#r "nuget: Microsoft.Data.Analysis"

open Microsoft.Data.Analysis

let dateTimes = PrimitiveDataFrameColumn<DateTime>("DateTimes")

// The following line used to fail to compile
dateTimes.Append(DateTime.Parse("2019/01/01"))

// The previous line is now equivalent to this line
dateTimes.Append(Nullable<DateTime>(DateTime.Parse("2019/01/01")))
```

<span data-ttu-id="36310-211">Ta funkcja implementuje [Język F # RFC FS-1075](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1075-nullable-interop.md).</span><span class="sxs-lookup"><span data-stu-id="36310-211">This feature implements [F# RFC FS-1075](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1075-nullable-interop.md).</span></span>

## <a name="preview-reverse-indexes"></a><span data-ttu-id="36310-212">Wersja zapoznawcza: przewracanie indeksów</span><span class="sxs-lookup"><span data-stu-id="36310-212">Preview: reverse indexes</span></span>

<span data-ttu-id="36310-213">W języku F # 5 wprowadzono również podgląd zezwalający na odwracanie indeksów.</span><span class="sxs-lookup"><span data-stu-id="36310-213">F# 5 also introduces a preview for allowing reverse indexes.</span></span> <span data-ttu-id="36310-214">Składnia jest następująca: `^idx`</span><span class="sxs-lookup"><span data-stu-id="36310-214">The syntax is `^idx`.</span></span> <span data-ttu-id="36310-215">Oto jak można określić wartość elementu 1 z końca listy:</span><span class="sxs-lookup"><span data-stu-id="36310-215">Here's how you can an element 1 value from the end of a list:</span></span>

```fsharp
let xs = [1..10]

// Get element 1 from the end:
xs.[^1]

// From the end slices

let lastTwoOldStyle = xs.[(xs.Length-2)..]

let lastTwoNewStyle = xs.[^1..]

lastTwoOldStyle = lastTwoNewStyle // true
```

<span data-ttu-id="36310-216">Można także definiować Odwróć indeksy dla własnych typów.</span><span class="sxs-lookup"><span data-stu-id="36310-216">You can also define reverse indexes for your own types.</span></span> <span data-ttu-id="36310-217">Aby to zrobić, należy wdrożyć następującą metodę:</span><span class="sxs-lookup"><span data-stu-id="36310-217">To do so, you'll need to implement the following method:</span></span>

```fsharp
GetReverseIndex: dimension: int -> offset: int
```

<span data-ttu-id="36310-218">Oto przykład dla `Span<'T>` typu:</span><span class="sxs-lookup"><span data-stu-id="36310-218">Here's an example for the `Span<'T>` type:</span></span>

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
    printfn "%A" arr

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

<span data-ttu-id="36310-219">Ta funkcja implementuje [Język F # RFC FS-1076](https://github.com/fsharp/fslang-design/blob/master/preview/FS-1076-from-the-end-slicing.md).</span><span class="sxs-lookup"><span data-stu-id="36310-219">This feature implements [F# RFC FS-1076](https://github.com/fsharp/fslang-design/blob/master/preview/FS-1076-from-the-end-slicing.md).</span></span>

## <a name="preview-overloads-of-custom-keywords-in-computation-expressions"></a><span data-ttu-id="36310-220">Wersja zapoznawcza: przeciążenia niestandardowych słów kluczowych w wyrażeniach obliczeń</span><span class="sxs-lookup"><span data-stu-id="36310-220">Preview: overloads of custom keywords in computation expressions</span></span>

<span data-ttu-id="36310-221">Wyrażenia obliczeń to zaawansowana funkcja dla autorów bibliotek i struktur.</span><span class="sxs-lookup"><span data-stu-id="36310-221">Computation expressions are a powerful feature for library and framework authors.</span></span> <span data-ttu-id="36310-222">Pozwalają one znacząco ulepszyć wyrazistości składników, umożliwiając zdefiniowanie dobrze znanych elementów członkowskich i tworzą DSL dla domeny, w której pracujesz.</span><span class="sxs-lookup"><span data-stu-id="36310-222">They allow you to greatly improve the expressiveness of your components by letting you define well-known members and form a DSL for the domain you're working in.</span></span>

<span data-ttu-id="36310-223">F # 5 dodaje obsługę w wersji zapoznawczej w celu przeładowania niestandardowych operacji w wyrażeniach obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="36310-223">F# 5 adds preview support for overloading custom operations in Computation Expressions.</span></span> <span data-ttu-id="36310-224">Umożliwia zapisanie i użycie następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="36310-224">It allows the following code to be written and consumed:</span></span>

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

<span data-ttu-id="36310-225">Przed wprowadzeniem tej zmiany można napisać `InputBuilder` Typ w takiej postaci, w jakiej jest, ale nie można go użyć w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="36310-225">Prior to this change, you could write the `InputBuilder` type as it is, but you couldn't use it the way it's used in the example.</span></span> <span data-ttu-id="36310-226">Ponieważ przeciążenia, parametry opcjonalne i teraz `System.ParamArray` są dozwolone, wszystko działa zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="36310-226">Since overloads, optional parameters, and now `System.ParamArray` types are allowed, everything just works as you'd expect it to.</span></span>

<span data-ttu-id="36310-227">Ta funkcja implementuje [Język F # RFC FS-1056](https://github.com/fsharp/fslang-design/blob/master/preview/FS-1056-allow-custom-operation-overloads.md).</span><span class="sxs-lookup"><span data-stu-id="36310-227">This feature implements [F# RFC FS-1056](https://github.com/fsharp/fslang-design/blob/master/preview/FS-1056-allow-custom-operation-overloads.md).</span></span>
