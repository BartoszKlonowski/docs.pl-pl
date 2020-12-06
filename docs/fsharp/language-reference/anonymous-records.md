---
title: Rekordy anonimowe
description: Dowiedz się, jak korzystać z metod tworzenia i używania rekordów anonimowych oraz funkcji języka, która ułatwia manipulowanie danymi.
ms.date: 06/12/2019
ms.openlocfilehash: 13950048f02ab74362f8174725f5f8615d9d7654
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96739818"
---
# <a name="anonymous-records"></a><span data-ttu-id="167e8-103">Rekordy anonimowe</span><span class="sxs-lookup"><span data-stu-id="167e8-103">Anonymous Records</span></span>

<span data-ttu-id="167e8-104">Rekordy anonimowe to proste Agregowanie wartości nazwanych, które nie muszą być deklarowane przed użyciem.</span><span class="sxs-lookup"><span data-stu-id="167e8-104">Anonymous records are simple aggregates of named values that don't need to be declared before use.</span></span> <span data-ttu-id="167e8-105">Można zadeklarować je jako struktury lub typy referencyjne.</span><span class="sxs-lookup"><span data-stu-id="167e8-105">You can declare them as either structs or reference types.</span></span> <span data-ttu-id="167e8-106">Domyślnie są to typy odwołań.</span><span class="sxs-lookup"><span data-stu-id="167e8-106">They're reference types by default.</span></span>

## <a name="syntax"></a><span data-ttu-id="167e8-107">Składnia</span><span class="sxs-lookup"><span data-stu-id="167e8-107">Syntax</span></span>

<span data-ttu-id="167e8-108">W poniższych przykładach przedstawiono składnię rekordu anonimowego.</span><span class="sxs-lookup"><span data-stu-id="167e8-108">The following examples demonstrate the anonymous record syntax.</span></span> <span data-ttu-id="167e8-109">Elementy z ograniczeniami `[item]` są opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="167e8-109">Items delimited as `[item]` are optional.</span></span>

```fsharp
// Construct an anonymous record
let value-name = [struct] {| Label1: Type1; Label2: Type2; ...|}

// Use an anonymous record as a type parameter
let value-name = Type-Name<[struct] {| Label1: Type1; Label2: Type2; ...|}>

// Define a parameter with an anonymous record as input
let function-name (arg-name: [struct] {| Label1: Type1; Label2: Type2; ...|}) ...
```

## <a name="basic-usage"></a><span data-ttu-id="167e8-110">Podstawowy sposób użycia</span><span class="sxs-lookup"><span data-stu-id="167e8-110">Basic usage</span></span>

<span data-ttu-id="167e8-111">Rekordy anonimowe najlepiej rozumieją się jako typy rekordów języka F #, które nie muszą być zadeklarowane przed utworzeniem wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="167e8-111">Anonymous records are best thought of as F# record types that don't need to be declared before instantiation.</span></span>

<span data-ttu-id="167e8-112">Na przykład, w jaki sposób można korzystać z funkcji, która generuje rekord anonimowy:</span><span class="sxs-lookup"><span data-stu-id="167e8-112">For example, here how you can interact with a function that produces an anonymous record:</span></span>

```fsharp
open System

let getCircleStats radius =
    let d = radius * 2.0
    let a = Math.PI * (radius ** 2.0)
    let c = 2.0 * Math.PI * radius

    {| Diameter = d; Area = a; Circumference = c |}

let r = 2.0
let stats = getCircleStats r
printfn "Circle with radius: %f has diameter %f, area %f, and circumference %f"
    r stats.Diameter stats.Area stats.Circumference
```

<span data-ttu-id="167e8-113">Poniższy przykład rozszerza na poprzednią wartość za pomocą `printCircleStats` funkcji przyjmującej rekord anonimowy jako dane wejściowe:</span><span class="sxs-lookup"><span data-stu-id="167e8-113">The following example expands on the previous one with a `printCircleStats` function that takes an anonymous record as input:</span></span>

```fsharp
open System

let getCircleStats radius =
    let d = radius * 2.0
    let a = Math.PI * (radius ** 2.0)
    let c = 2.0 * Math.PI * radius

    {| Diameter = d; Area = a; Circumference = c |}

let printCircleStats r (stats: {| Area: float; Circumference: float; Diameter: float |}) =
    printfn "Circle with radius: %f has diameter %f, area %f, and circumference %f"
        r stats.Diameter stats.Area stats.Circumference

let r = 2.0
let stats = getCircleStats r
printCircleStats r stats
```

<span data-ttu-id="167e8-114">`printCircleStats`Kompilowanie z dowolnym typem rekordu anonimowego, który nie ma tego samego "kształtu", ponieważ typ danych wejściowych zakończy się niepowodzeniem:</span><span class="sxs-lookup"><span data-stu-id="167e8-114">Calling `printCircleStats` with any anonymous record type that doesn't have the same "shape" as the input type will fail to compile:</span></span>

```fsharp
printCircleStats r {| Diameter = 2.0; Area = 4.0; MyCircumference = 12.566371 |}
// Two anonymous record types have mismatched sets of field names
// '["Area"; "Circumference"; "Diameter"]' and '["Area"; "Diameter"; "MyCircumference"]'
```

## <a name="struct-anonymous-records"></a><span data-ttu-id="167e8-115">Anonimowe rekordy struktury</span><span class="sxs-lookup"><span data-stu-id="167e8-115">Struct anonymous records</span></span>

<span data-ttu-id="167e8-116">Rekordy anonimowe mogą być również zdefiniowane jako struktury za pomocą opcjonalnego `struct` słowa kluczowego.</span><span class="sxs-lookup"><span data-stu-id="167e8-116">Anonymous records can also be defined as struct with the optional `struct` keyword.</span></span> <span data-ttu-id="167e8-117">Poniższy przykład rozszerza poprzednią wartość przez produkowanie i zużywanie anonimowego rekordu struktury:</span><span class="sxs-lookup"><span data-stu-id="167e8-117">The following example augments the previous one by producing and consuming a struct anonymous record:</span></span>

```fsharp
open System

let getCircleStats radius =
    let d = radius * 2.0
    let a = Math.PI * (radius ** 2.0)
    let c = 2.0 * Math.PI * radius

    // Note that the keyword comes before the '{| |}' brace pair
    struct {| Area = a; Circumference = c; Diameter = d |}

// the 'struct' keyword also comes before the '{| |}' brace pair when declaring the parameter type
let printCircleStats r (stats: struct {| Area: float; Circumference: float; Diameter: float |}) =
    printfn "Circle with radius: %f has diameter %f, area %f, and circumference %f"
        r stats.Diameter stats.Area stats.Circumference

let r = 2.0
let stats = getCircleStats r
printCircleStats r stats
```

### <a name="structness-inference"></a><span data-ttu-id="167e8-118">Wnioskowanie o strukturze</span><span class="sxs-lookup"><span data-stu-id="167e8-118">Structness inference</span></span>

<span data-ttu-id="167e8-119">Anonimowe rekordy struktury umożliwiają również określenie "wnioskowanie o strukturze", gdzie nie trzeba określać `struct` słowa kluczowego w miejscu wywołania.</span><span class="sxs-lookup"><span data-stu-id="167e8-119">Struct anonymous records also allow for "structness inference" where you do not need to specify the `struct` keyword at the call site.</span></span> <span data-ttu-id="167e8-120">W tym przykładzie Elide `struct` słowo kluczowe podczas wywoływania `printCircleStats` :</span><span class="sxs-lookup"><span data-stu-id="167e8-120">In this example, you elide the `struct` keyword when calling `printCircleStats`:</span></span>

```fsharp

let printCircleStats r (stats: struct {| Area: float; Circumference: float; Diameter: float |}) =
    printfn "Circle with radius: %f has diameter %f, area %f, and circumference %f"
        r stats.Diameter stats.Area stats.Circumference

printCircleStats r {| Area = 4.0; Circumference = 12.6; Diameter = 12.6 |}
```

<span data-ttu-id="167e8-121">Wzorzec odwrotny — Określanie, `struct` gdy typ wejściowy nie jest rekordem anonimowym struktury — kompilacja nie zostanie ukończona.</span><span class="sxs-lookup"><span data-stu-id="167e8-121">The reverse pattern - specifying `struct` when the input type is not a struct anonymous record - will fail to compile.</span></span>

## <a name="embedding-anonymous-records-within-other-types"></a><span data-ttu-id="167e8-122">Osadzanie rekordów anonimowych w innych typach</span><span class="sxs-lookup"><span data-stu-id="167e8-122">Embedding anonymous records within other types</span></span>

<span data-ttu-id="167e8-123">Jest to przydatne do deklarowania [związków rozłącznych](discriminated-unions.md) , których przypadki są rekordami.</span><span class="sxs-lookup"><span data-stu-id="167e8-123">It's useful to declare [discriminated unions](discriminated-unions.md) whose cases are records.</span></span> <span data-ttu-id="167e8-124">Ale jeśli dane w rekordach są tego samego typu co związek rozłącznych, należy zdefiniować wszystkie typy jako wzajemnie cykliczne.</span><span class="sxs-lookup"><span data-stu-id="167e8-124">But if the data in the records is the same type as the discriminated union, you must define all types as mutually recursive.</span></span> <span data-ttu-id="167e8-125">Korzystanie z rekordów anonimowych pozwala uniknąć tego ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="167e8-125">Using anonymous records avoids this restriction.</span></span> <span data-ttu-id="167e8-126">Poniżej znajduje się przykładowy typ i funkcja, która pasuje do wzorca:</span><span class="sxs-lookup"><span data-stu-id="167e8-126">What follows is an example type and function that pattern matches over it:</span></span>

```fsharp
type FullName = { FirstName: string; LastName: string }

// Note that using a named record for Manager and Executive would require mutually recursive definitions.
type Employee =
    | Engineer of FullName
    | Manager of {| Name: FullName; Reports: Employee list |}
    | Executive of {| Name: FullName; Reports: Employee list; Assistant: Employee |}

let getFirstName e =
    match e with
    | Engineer fullName -> fullName.FirstName
    | Manager m -> m.Name.FirstName
    | Executive ex -> ex.Name.FirstName
```

## <a name="copy-and-update-expressions"></a><span data-ttu-id="167e8-127">Kopiuj i Aktualizuj wyrażenia</span><span class="sxs-lookup"><span data-stu-id="167e8-127">Copy and update expressions</span></span>

<span data-ttu-id="167e8-128">Rekordy anonimowe obsługują tworzenie z [wyrażeniami kopiowania i aktualizowania](copy-and-update-record-expressions.md).</span><span class="sxs-lookup"><span data-stu-id="167e8-128">Anonymous records support construction with [copy and update expressions](copy-and-update-record-expressions.md).</span></span> <span data-ttu-id="167e8-129">Można na przykład utworzyć nowe wystąpienie rekordu anonimowego, który kopiuje istniejące dane:</span><span class="sxs-lookup"><span data-stu-id="167e8-129">For example, here's how you can construct a new instance of an anonymous record that copies an existing one's data:</span></span>

```fsharp
let data = {| X = 1; Y = 2 |}
let data' = {| data with Y = 3 |}
```

<span data-ttu-id="167e8-130">Jednak w przeciwieństwie do nazwanych rekordów, anonimowe rekordy umożliwiają konstruowanie zupełnie różnych formularzy z wyrażeniami Copy i Update.</span><span class="sxs-lookup"><span data-stu-id="167e8-130">However, unlike named records, anonymous records allow you to construct entirely different forms with copy and update expressions.</span></span> <span data-ttu-id="167e8-131">W poniższym przykładzie ten sam rekord anonimowy jest pobierany z poprzedniego przykładu i rozszerzany do nowego rekordu anonimowego:</span><span class="sxs-lookup"><span data-stu-id="167e8-131">The follow example takes the same anonymous record from the previous example and expands it into a new anonymous record:</span></span>

```fsharp
let data = {| X = 1; Y = 2 |}
let expandedData = {| data with Z = 3 |} // Gives {| X=1; Y=2; Z=3 |}
```

<span data-ttu-id="167e8-132">Istnieje również możliwość konstruowania rekordów anonimowych z wystąpień nazwanych rekordów:</span><span class="sxs-lookup"><span data-stu-id="167e8-132">It is also possible to construct anonymous records from instances of named records:</span></span>

```fsharp
type R = { X: int }
let data = { X = 1 }
let data' = {| data with Y = 2 |} // Gives {| X=1; Y=2 |}
```

<span data-ttu-id="167e8-133">Możesz również kopiować dane do i z odwołań do rekordów i struktury anonimowe:</span><span class="sxs-lookup"><span data-stu-id="167e8-133">You can also copy data to and from reference and struct anonymous records:</span></span>

```fsharp
// Copy data from a reference record into a struct anonymous record
type R1 = { X: int }
let r1 = { X = 1 }

let data1 = struct {| r1 with Y = 1 |}

// Copy data from a struct record into a reference anonymous record
[<Struct>]
type R2 = { X: int }
let r2 = { X = 1 }

let data2 = {| r1 with Y = 1 |}

// Copy the reference anonymous record data into a struct anonymous record
let data3 = struct {| data2 with Z = r2.X |}
```

## <a name="properties-of-anonymous-records"></a><span data-ttu-id="167e8-134">Właściwości rekordów anonimowych</span><span class="sxs-lookup"><span data-stu-id="167e8-134">Properties of anonymous records</span></span>

<span data-ttu-id="167e8-135">Rekordy anonimowe mają wiele cech, które są niezbędne do pełnego poznania sposobu ich używania.</span><span class="sxs-lookup"><span data-stu-id="167e8-135">Anonymous records have a number of characteristics that are essential to fully understanding how they can be used.</span></span>

### <a name="anonymous-records-are-nominal"></a><span data-ttu-id="167e8-136">Rekordy anonimowe są nominalne</span><span class="sxs-lookup"><span data-stu-id="167e8-136">Anonymous records are nominal</span></span>

<span data-ttu-id="167e8-137">Rekordy anonimowe są [typami nominalnymi](https://en.wikipedia.org/wiki/Nominal_type_system).</span><span class="sxs-lookup"><span data-stu-id="167e8-137">Anonymous records are [nominal types](https://en.wikipedia.org/wiki/Nominal_type_system).</span></span> <span data-ttu-id="167e8-138">Są one najlepiej przemyślane jako nazwane typy [rekordów](records.md) (które są również nominalne), które nie wymagają deklaracji z góry.</span><span class="sxs-lookup"><span data-stu-id="167e8-138">They are best thought as named [record](records.md) types (which are also nominal) that do not require an up-front declaration.</span></span>

<span data-ttu-id="167e8-139">Rozważmy następujący przykład z dwiema deklaracjami rekordów anonimowych:</span><span class="sxs-lookup"><span data-stu-id="167e8-139">Consider the following example with two anonymous record declarations:</span></span>

```fsharp
let x = {| X = 1 |}
let y = {| Y = 1 |}
```

<span data-ttu-id="167e8-140">`x`Wartości i `y` mają różne typy i nie są zgodne ze sobą.</span><span class="sxs-lookup"><span data-stu-id="167e8-140">The `x` and `y` values have different types and are not compatible with one another.</span></span> <span data-ttu-id="167e8-141">Nie są one równe i nie są porównywalne.</span><span class="sxs-lookup"><span data-stu-id="167e8-141">They are not equatable and they are not comparable.</span></span> <span data-ttu-id="167e8-142">Aby to zilustrować, należy wziąć pod uwagę nazwany rekord odpowiedni:</span><span class="sxs-lookup"><span data-stu-id="167e8-142">To illustrate this, consider a named record equivalent:</span></span>

```fsharp
type X = { X: int }
type Y = { Y: int }

let x = { X = 1 }
let y = { Y = 1 }
```

<span data-ttu-id="167e8-143">W porównaniu z odpowiadającymi im odpowiednikami typów lub porównaniem nie ma niczego inaczej niż w przypadku rekordów anonimowych.</span><span class="sxs-lookup"><span data-stu-id="167e8-143">There isn't anything inherently different about anonymous records when compared with their named record equivalents when concerning type equivalency or comparison.</span></span>

### <a name="anonymous-records-use-structural-equality-and-comparison"></a><span data-ttu-id="167e8-144">Rekordy anonimowe wykorzystują równość i porównanie strukturalne</span><span class="sxs-lookup"><span data-stu-id="167e8-144">Anonymous records use structural equality and comparison</span></span>

<span data-ttu-id="167e8-145">Podobnie jak w przypadku typów rekordów anonimowe rekordy są strukturalnie równe i porównywalne.</span><span class="sxs-lookup"><span data-stu-id="167e8-145">Like record types, anonymous records are structurally equatable and comparable.</span></span> <span data-ttu-id="167e8-146">Jest to możliwe tylko wtedy, gdy wszystkie typy składników obsługują równość i porównanie, podobnie jak w przypadku typów rekordów.</span><span class="sxs-lookup"><span data-stu-id="167e8-146">This is only true if all constituent types support equality and comparison, like with record types.</span></span> <span data-ttu-id="167e8-147">Aby obsłużyć równość lub porównanie, dwa rekordy anonimowe muszą mieć ten sam "kształt".</span><span class="sxs-lookup"><span data-stu-id="167e8-147">To support equality or comparison, two anonymous records must have the same "shape".</span></span>

```fsharp
{| a = 1+1 |} = {| a = 2 |} // true
{| a = 1+1 |} > {| a = 1 |} // true

// error FS0001: Two anonymous record types have mismatched sets of field names '["a"]' and '["a"; "b"]'
{| a = 1 + 1 |} = {| a = 2;  b = 1|}
```

### <a name="anonymous-records-are-serializable"></a><span data-ttu-id="167e8-148">Rekordy anonimowe są możliwe do serializacji</span><span class="sxs-lookup"><span data-stu-id="167e8-148">Anonymous records are serializable</span></span>

<span data-ttu-id="167e8-149">Rekordy anonimowe można serializować tak samo jak z nazwanymi rekordami.</span><span class="sxs-lookup"><span data-stu-id="167e8-149">You can serialize anonymous records just as you can with named records.</span></span> <span data-ttu-id="167e8-150">Oto przykład użycia [Newtonsoft.Jsw](https://www.nuget.org/packages/Newtonsoft.Json/):</span><span class="sxs-lookup"><span data-stu-id="167e8-150">Here is an example using [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/):</span></span>

```fsharp
open Newtonsoft.Json

let phillip' = {| name="Phillip"; age=28 |}
let philStr = JsonConvert.SerializeObject(phillip')

let phillip = JsonConvert.DeserializeObject<{|name: string; age: int|}>(philStr)
printfn $"Name: {phillip.name} Age: %d{phillip.age}"
```

<span data-ttu-id="167e8-151">Rekordy anonimowe są przydatne do przesyłania danych lekkich za pośrednictwem sieci bez konieczności definiowania domeny dla serializowanych i deserializowanych typów z góry.</span><span class="sxs-lookup"><span data-stu-id="167e8-151">Anonymous records are useful for sending lightweight data over a network without the need to define a domain for your serialized/deserialized types up front.</span></span>

### <a name="anonymous-records-interoperate-with-c-anonymous-types"></a><span data-ttu-id="167e8-152">Rekordy anonimowe współdziałają z typami anonimowymi języka C#</span><span class="sxs-lookup"><span data-stu-id="167e8-152">Anonymous records interoperate with C# anonymous types</span></span>

<span data-ttu-id="167e8-153">Możliwe jest użycie interfejsu API platformy .NET, który wymaga użycia [typów anonimowych języka C#](../../csharp/programming-guide/classes-and-structs/anonymous-types.md).</span><span class="sxs-lookup"><span data-stu-id="167e8-153">It is possible to use a .NET API that requires the use of [C# anonymous types](../../csharp/programming-guide/classes-and-structs/anonymous-types.md).</span></span> <span data-ttu-id="167e8-154">Typy anonimowe języka C# są proste do współpracy z programem przy użyciu rekordów anonimowych.</span><span class="sxs-lookup"><span data-stu-id="167e8-154">C# anonymous types are trivial to interoperate with by using anonymous records.</span></span> <span data-ttu-id="167e8-155">Poniższy przykład pokazuje, jak używać rekordów anonimowych do wywoływania przeciążenia [LINQ](../../csharp/programming-guide/concepts/linq/index.md) , które wymaga typu anonimowego:</span><span class="sxs-lookup"><span data-stu-id="167e8-155">The following example shows how to use anonymous records to call a [LINQ](../../csharp/programming-guide/concepts/linq/index.md) overload that requires an anonymous type:</span></span>

```fsharp
open System.Linq

let names = [ "Ana"; "Felipe"; "Emilia"]
let nameGrouping = names.Select(fun n -> {| Name = n; FirstLetter = n.[0] |})
for ng in nameGrouping do
    printfn $"{ng.Name} has first letter {ng.FirstLetter}"
```

<span data-ttu-id="167e8-156">Istnieje wiele innych interfejsów API używanych w środowisku .NET, które wymagają użycia przekazywania w typie anonimowym.</span><span class="sxs-lookup"><span data-stu-id="167e8-156">There are a multitude of other APIs used throughout .NET that require the use of passing in an anonymous type.</span></span> <span data-ttu-id="167e8-157">Rekordy anonimowe to narzędzie do pracy z nimi.</span><span class="sxs-lookup"><span data-stu-id="167e8-157">Anonymous records are your tool for working with them.</span></span>

## <a name="limitations"></a><span data-ttu-id="167e8-158">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="167e8-158">Limitations</span></span>

<span data-ttu-id="167e8-159">Rekordy anonimowe mają pewne ograniczenia w ich użyciu.</span><span class="sxs-lookup"><span data-stu-id="167e8-159">Anonymous records have some restrictions in their usage.</span></span> <span data-ttu-id="167e8-160">Niektóre z nich są związane z projektem, ale inne mogą ulec zmianie.</span><span class="sxs-lookup"><span data-stu-id="167e8-160">Some are inherent to their design, but others are amenable to change.</span></span>

### <a name="limitations-with-pattern-matching"></a><span data-ttu-id="167e8-161">Ograniczenia z dopasowaniem do wzorca</span><span class="sxs-lookup"><span data-stu-id="167e8-161">Limitations with pattern matching</span></span>

<span data-ttu-id="167e8-162">Rekordy anonimowe nie obsługują dopasowywania do wzorców, w przeciwieństwie do nazwanych rekordów.</span><span class="sxs-lookup"><span data-stu-id="167e8-162">Anonymous records do not support pattern matching, unlike named records.</span></span> <span data-ttu-id="167e8-163">Istnieją trzy przyczyny:</span><span class="sxs-lookup"><span data-stu-id="167e8-163">There are three reasons:</span></span>

1. <span data-ttu-id="167e8-164">Wzorzec będzie musiał uwzględnić każde pole rekordu anonimowego, w przeciwieństwie do typów rekordów nazwanych.</span><span class="sxs-lookup"><span data-stu-id="167e8-164">A pattern would have to account for every field of an anonymous record, unlike named record types.</span></span> <span data-ttu-id="167e8-165">Wynika to z faktu, że rekordy anonimowe nie obsługują podpisywania strukturalnego — są to typy nominalne.</span><span class="sxs-lookup"><span data-stu-id="167e8-165">This is because anonymous records do not support structural subtyping – they are nominal types.</span></span>
2. <span data-ttu-id="167e8-166">Ze względu na (1) nie ma możliwości posiadania dodatkowych wzorców w wyrażeniu dopasowania do wzorca, ponieważ każdy unikatowy wzorzec będzie oznaczać inny typ rekordu anonimowego.</span><span class="sxs-lookup"><span data-stu-id="167e8-166">Because of (1), there is no ability to have additional patterns in a pattern match expression, as each distinct pattern would imply a different anonymous record type.</span></span>
3. <span data-ttu-id="167e8-167">Ze względu na (3) każdy wzorzec rekordu anonimowego będzie bardziej pełny niż użycie notacji "kropka".</span><span class="sxs-lookup"><span data-stu-id="167e8-167">Because of (3), any anonymous record pattern would be more verbose than the use of “dot” notation.</span></span>

<span data-ttu-id="167e8-168">Jest dostępna sugestia języka umożliwiająca [Dopasowywanie wzorców w ograniczonych kontekstach](https://github.com/fsharp/fslang-suggestions/issues/713).</span><span class="sxs-lookup"><span data-stu-id="167e8-168">There is an open language suggestion to [allow pattern matching in limited contexts](https://github.com/fsharp/fslang-suggestions/issues/713).</span></span>

### <a name="limitations-with-mutability"></a><span data-ttu-id="167e8-169">Ograniczenia dotyczące zmienność</span><span class="sxs-lookup"><span data-stu-id="167e8-169">Limitations with mutability</span></span>

<span data-ttu-id="167e8-170">Obecnie nie jest możliwe Definiowanie rekordu anonimowego z `mutable` danymi.</span><span class="sxs-lookup"><span data-stu-id="167e8-170">It is not currently possible to define an anonymous record with `mutable` data.</span></span> <span data-ttu-id="167e8-171">Jest dostępna [sugestia języka](https://github.com/fsharp/fslang-suggestions/issues/732) , w której można zezwolić na modyfikowalne dane.</span><span class="sxs-lookup"><span data-stu-id="167e8-171">There is an [open language suggestion](https://github.com/fsharp/fslang-suggestions/issues/732) to allow mutable data.</span></span>

### <a name="limitations-with-struct-anonymous-records"></a><span data-ttu-id="167e8-172">Ograniczenia z anonimowymi rekordami struktury</span><span class="sxs-lookup"><span data-stu-id="167e8-172">Limitations with struct anonymous records</span></span>

<span data-ttu-id="167e8-173">Nie można zadeklarować anonimowych rekordów struktury jako `IsByRefLike` lub `IsReadOnly` .</span><span class="sxs-lookup"><span data-stu-id="167e8-173">It is not possible to declare struct anonymous records as `IsByRefLike` or `IsReadOnly`.</span></span> <span data-ttu-id="167e8-174">Istnieje [otwarta sugestia językowa](https://github.com/fsharp/fslang-suggestions/issues/712) dla `IsByRefLike` rekordów i `IsReadOnly` anonimowych.</span><span class="sxs-lookup"><span data-stu-id="167e8-174">There is an [open language suggestion](https://github.com/fsharp/fslang-suggestions/issues/712) to for `IsByRefLike` and `IsReadOnly` anonymous records.</span></span>
