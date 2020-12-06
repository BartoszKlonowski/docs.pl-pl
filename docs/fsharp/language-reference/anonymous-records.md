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
# <a name="anonymous-records"></a>Rekordy anonimowe

Rekordy anonimowe to proste Agregowanie wartości nazwanych, które nie muszą być deklarowane przed użyciem. Można zadeklarować je jako struktury lub typy referencyjne. Domyślnie są to typy odwołań.

## <a name="syntax"></a>Składnia

W poniższych przykładach przedstawiono składnię rekordu anonimowego. Elementy z ograniczeniami `[item]` są opcjonalne.

```fsharp
// Construct an anonymous record
let value-name = [struct] {| Label1: Type1; Label2: Type2; ...|}

// Use an anonymous record as a type parameter
let value-name = Type-Name<[struct] {| Label1: Type1; Label2: Type2; ...|}>

// Define a parameter with an anonymous record as input
let function-name (arg-name: [struct] {| Label1: Type1; Label2: Type2; ...|}) ...
```

## <a name="basic-usage"></a>Podstawowy sposób użycia

Rekordy anonimowe najlepiej rozumieją się jako typy rekordów języka F #, które nie muszą być zadeklarowane przed utworzeniem wystąpienia.

Na przykład, w jaki sposób można korzystać z funkcji, która generuje rekord anonimowy:

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

Poniższy przykład rozszerza na poprzednią wartość za pomocą `printCircleStats` funkcji przyjmującej rekord anonimowy jako dane wejściowe:

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

`printCircleStats`Kompilowanie z dowolnym typem rekordu anonimowego, który nie ma tego samego "kształtu", ponieważ typ danych wejściowych zakończy się niepowodzeniem:

```fsharp
printCircleStats r {| Diameter = 2.0; Area = 4.0; MyCircumference = 12.566371 |}
// Two anonymous record types have mismatched sets of field names
// '["Area"; "Circumference"; "Diameter"]' and '["Area"; "Diameter"; "MyCircumference"]'
```

## <a name="struct-anonymous-records"></a>Anonimowe rekordy struktury

Rekordy anonimowe mogą być również zdefiniowane jako struktury za pomocą opcjonalnego `struct` słowa kluczowego. Poniższy przykład rozszerza poprzednią wartość przez produkowanie i zużywanie anonimowego rekordu struktury:

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

### <a name="structness-inference"></a>Wnioskowanie o strukturze

Anonimowe rekordy struktury umożliwiają również określenie "wnioskowanie o strukturze", gdzie nie trzeba określać `struct` słowa kluczowego w miejscu wywołania. W tym przykładzie Elide `struct` słowo kluczowe podczas wywoływania `printCircleStats` :

```fsharp

let printCircleStats r (stats: struct {| Area: float; Circumference: float; Diameter: float |}) =
    printfn "Circle with radius: %f has diameter %f, area %f, and circumference %f"
        r stats.Diameter stats.Area stats.Circumference

printCircleStats r {| Area = 4.0; Circumference = 12.6; Diameter = 12.6 |}
```

Wzorzec odwrotny — Określanie, `struct` gdy typ wejściowy nie jest rekordem anonimowym struktury — kompilacja nie zostanie ukończona.

## <a name="embedding-anonymous-records-within-other-types"></a>Osadzanie rekordów anonimowych w innych typach

Jest to przydatne do deklarowania [związków rozłącznych](discriminated-unions.md) , których przypadki są rekordami. Ale jeśli dane w rekordach są tego samego typu co związek rozłącznych, należy zdefiniować wszystkie typy jako wzajemnie cykliczne. Korzystanie z rekordów anonimowych pozwala uniknąć tego ograniczenia. Poniżej znajduje się przykładowy typ i funkcja, która pasuje do wzorca:

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

## <a name="copy-and-update-expressions"></a>Kopiuj i Aktualizuj wyrażenia

Rekordy anonimowe obsługują tworzenie z [wyrażeniami kopiowania i aktualizowania](copy-and-update-record-expressions.md). Można na przykład utworzyć nowe wystąpienie rekordu anonimowego, który kopiuje istniejące dane:

```fsharp
let data = {| X = 1; Y = 2 |}
let data' = {| data with Y = 3 |}
```

Jednak w przeciwieństwie do nazwanych rekordów, anonimowe rekordy umożliwiają konstruowanie zupełnie różnych formularzy z wyrażeniami Copy i Update. W poniższym przykładzie ten sam rekord anonimowy jest pobierany z poprzedniego przykładu i rozszerzany do nowego rekordu anonimowego:

```fsharp
let data = {| X = 1; Y = 2 |}
let expandedData = {| data with Z = 3 |} // Gives {| X=1; Y=2; Z=3 |}
```

Istnieje również możliwość konstruowania rekordów anonimowych z wystąpień nazwanych rekordów:

```fsharp
type R = { X: int }
let data = { X = 1 }
let data' = {| data with Y = 2 |} // Gives {| X=1; Y=2 |}
```

Możesz również kopiować dane do i z odwołań do rekordów i struktury anonimowe:

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

## <a name="properties-of-anonymous-records"></a>Właściwości rekordów anonimowych

Rekordy anonimowe mają wiele cech, które są niezbędne do pełnego poznania sposobu ich używania.

### <a name="anonymous-records-are-nominal"></a>Rekordy anonimowe są nominalne

Rekordy anonimowe są [typami nominalnymi](https://en.wikipedia.org/wiki/Nominal_type_system). Są one najlepiej przemyślane jako nazwane typy [rekordów](records.md) (które są również nominalne), które nie wymagają deklaracji z góry.

Rozważmy następujący przykład z dwiema deklaracjami rekordów anonimowych:

```fsharp
let x = {| X = 1 |}
let y = {| Y = 1 |}
```

`x`Wartości i `y` mają różne typy i nie są zgodne ze sobą. Nie są one równe i nie są porównywalne. Aby to zilustrować, należy wziąć pod uwagę nazwany rekord odpowiedni:

```fsharp
type X = { X: int }
type Y = { Y: int }

let x = { X = 1 }
let y = { Y = 1 }
```

W porównaniu z odpowiadającymi im odpowiednikami typów lub porównaniem nie ma niczego inaczej niż w przypadku rekordów anonimowych.

### <a name="anonymous-records-use-structural-equality-and-comparison"></a>Rekordy anonimowe wykorzystują równość i porównanie strukturalne

Podobnie jak w przypadku typów rekordów anonimowe rekordy są strukturalnie równe i porównywalne. Jest to możliwe tylko wtedy, gdy wszystkie typy składników obsługują równość i porównanie, podobnie jak w przypadku typów rekordów. Aby obsłużyć równość lub porównanie, dwa rekordy anonimowe muszą mieć ten sam "kształt".

```fsharp
{| a = 1+1 |} = {| a = 2 |} // true
{| a = 1+1 |} > {| a = 1 |} // true

// error FS0001: Two anonymous record types have mismatched sets of field names '["a"]' and '["a"; "b"]'
{| a = 1 + 1 |} = {| a = 2;  b = 1|}
```

### <a name="anonymous-records-are-serializable"></a>Rekordy anonimowe są możliwe do serializacji

Rekordy anonimowe można serializować tak samo jak z nazwanymi rekordami. Oto przykład użycia [Newtonsoft.Jsw](https://www.nuget.org/packages/Newtonsoft.Json/):

```fsharp
open Newtonsoft.Json

let phillip' = {| name="Phillip"; age=28 |}
let philStr = JsonConvert.SerializeObject(phillip')

let phillip = JsonConvert.DeserializeObject<{|name: string; age: int|}>(philStr)
printfn $"Name: {phillip.name} Age: %d{phillip.age}"
```

Rekordy anonimowe są przydatne do przesyłania danych lekkich za pośrednictwem sieci bez konieczności definiowania domeny dla serializowanych i deserializowanych typów z góry.

### <a name="anonymous-records-interoperate-with-c-anonymous-types"></a>Rekordy anonimowe współdziałają z typami anonimowymi języka C#

Możliwe jest użycie interfejsu API platformy .NET, który wymaga użycia [typów anonimowych języka C#](../../csharp/programming-guide/classes-and-structs/anonymous-types.md). Typy anonimowe języka C# są proste do współpracy z programem przy użyciu rekordów anonimowych. Poniższy przykład pokazuje, jak używać rekordów anonimowych do wywoływania przeciążenia [LINQ](../../csharp/programming-guide/concepts/linq/index.md) , które wymaga typu anonimowego:

```fsharp
open System.Linq

let names = [ "Ana"; "Felipe"; "Emilia"]
let nameGrouping = names.Select(fun n -> {| Name = n; FirstLetter = n.[0] |})
for ng in nameGrouping do
    printfn $"{ng.Name} has first letter {ng.FirstLetter}"
```

Istnieje wiele innych interfejsów API używanych w środowisku .NET, które wymagają użycia przekazywania w typie anonimowym. Rekordy anonimowe to narzędzie do pracy z nimi.

## <a name="limitations"></a>Ograniczenia

Rekordy anonimowe mają pewne ograniczenia w ich użyciu. Niektóre z nich są związane z projektem, ale inne mogą ulec zmianie.

### <a name="limitations-with-pattern-matching"></a>Ograniczenia z dopasowaniem do wzorca

Rekordy anonimowe nie obsługują dopasowywania do wzorców, w przeciwieństwie do nazwanych rekordów. Istnieją trzy przyczyny:

1. Wzorzec będzie musiał uwzględnić każde pole rekordu anonimowego, w przeciwieństwie do typów rekordów nazwanych. Wynika to z faktu, że rekordy anonimowe nie obsługują podpisywania strukturalnego — są to typy nominalne.
2. Ze względu na (1) nie ma możliwości posiadania dodatkowych wzorców w wyrażeniu dopasowania do wzorca, ponieważ każdy unikatowy wzorzec będzie oznaczać inny typ rekordu anonimowego.
3. Ze względu na (3) każdy wzorzec rekordu anonimowego będzie bardziej pełny niż użycie notacji "kropka".

Jest dostępna sugestia języka umożliwiająca [Dopasowywanie wzorców w ograniczonych kontekstach](https://github.com/fsharp/fslang-suggestions/issues/713).

### <a name="limitations-with-mutability"></a>Ograniczenia dotyczące zmienność

Obecnie nie jest możliwe Definiowanie rekordu anonimowego z `mutable` danymi. Jest dostępna [sugestia języka](https://github.com/fsharp/fslang-suggestions/issues/732) , w której można zezwolić na modyfikowalne dane.

### <a name="limitations-with-struct-anonymous-records"></a>Ograniczenia z anonimowymi rekordami struktury

Nie można zadeklarować anonimowych rekordów struktury jako `IsByRefLike` lub `IsReadOnly` . Istnieje [otwarta sugestia językowa](https://github.com/fsharp/fslang-suggestions/issues/712) dla `IsByRefLike` rekordów i `IsReadOnly` anonimowych.
