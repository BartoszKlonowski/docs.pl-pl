---
title: Typy wartości dopuszczające wartość null
description: 'Dowiedz się, jak używać typów wartości null, aby reprezentować typy wartości, które mogą również mieć wartość null, w języku F #.'
ms.date: 11/19/2020
ms.openlocfilehash: e28cbfc57c5631573f46ac36462517cf011e96d2
ms.sourcegitcommit: 81f1bba2c97a67b5ca76bcc57b37333ffca60c7b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/10/2020
ms.locfileid: "97009641"
---
# <a name="nullable-value-types"></a><span data-ttu-id="a885e-103">Typy wartości dopuszczające wartość null</span><span class="sxs-lookup"><span data-stu-id="a885e-103">Nullable value types</span></span>

<span data-ttu-id="a885e-104">_Typ wartości null_ `Nullable<'T>` reprezentuje dowolny typ [struktury](structures.md) , który może być również `null` .</span><span class="sxs-lookup"><span data-stu-id="a885e-104">A _nullable value type_ `Nullable<'T>` represents any [struct](structures.md) type that could also be `null`.</span></span> <span data-ttu-id="a885e-105">Jest to przydatne podczas pracy z bibliotekami i składnikami, które mogą reprezentować te rodzaje typów, takich jak liczby całkowite, z `null` wartością ze względów wydajnościowych.</span><span class="sxs-lookup"><span data-stu-id="a885e-105">This is helpful when interacting with libraries and components that may choose to represent these kinds of types, like integers, with a `null` value for efficiency reasons.</span></span> <span data-ttu-id="a885e-106">Typ podstawowy, który wykonuje kopię zapasową tej konstrukcji <xref:System.Nullable%601?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="a885e-106">The underlying type that backs this construct is <xref:System.Nullable%601?displayProperty=nameWithType>.</span></span>

## <a name="syntax"></a><span data-ttu-id="a885e-107">Składnia</span><span class="sxs-lookup"><span data-stu-id="a885e-107">Syntax</span></span>

```fsharp
Nullable<'T>
Nullable value
```

## <a name="declare-and-assign-with-values"></a><span data-ttu-id="a885e-108">Zadeklaruj i przypisz z wartościami</span><span class="sxs-lookup"><span data-stu-id="a885e-108">Declare and assign with values</span></span>

<span data-ttu-id="a885e-109">Deklarowanie typu wartości null jest równie podobne jak zadeklarowanie dowolnego typu otoki w języku F #:</span><span class="sxs-lookup"><span data-stu-id="a885e-109">Declaring a nullable value type is just like declaring any wrapper-like type in F#:</span></span>

```fsharp
open System

let x = 12
let nullableX = Nullable<int> x
```

<span data-ttu-id="a885e-110">Możesz również Elide parametr typu ogólnego i zezwolić na wnioskowanie o typie, aby rozwiązać ten problem:</span><span class="sxs-lookup"><span data-stu-id="a885e-110">You can also elide the generic type parameter and allow type inference to resolve it:</span></span>

```fsharp
open System

let x = 12
let nullableX = Nullable x
```

<span data-ttu-id="a885e-111">Aby przypisać do typu wartości null, należy również być jawnym.</span><span class="sxs-lookup"><span data-stu-id="a885e-111">To assign to a nullable value type, you'll need to also be explicit.</span></span> <span data-ttu-id="a885e-112">Nie istnieje niejawna konwersja dla typów wartości null zdefiniowanych w języku F #:</span><span class="sxs-lookup"><span data-stu-id="a885e-112">There is no implicit conversion for F#-defined nullable value types:</span></span>

```fsharp
open System

let mutable x = Nullable 12
x <- Nullable 13
```

## <a name="assign-null"></a><span data-ttu-id="a885e-113">Przypisz wartość null</span><span class="sxs-lookup"><span data-stu-id="a885e-113">Assign null</span></span>

<span data-ttu-id="a885e-114">Nie można bezpośrednio przypisać `null` do typu wartości null.</span><span class="sxs-lookup"><span data-stu-id="a885e-114">You cannot directly assign `null` to a nullable value type.</span></span> <span data-ttu-id="a885e-115">Użyj `Nullable()` zamiast tego:</span><span class="sxs-lookup"><span data-stu-id="a885e-115">Use `Nullable()` instead:</span></span>

```fsharp
let mutable a = Nullable 42
a <- Nullable()
```

<span data-ttu-id="a885e-116">Jest to spowodowane tym `Nullable<'T>` , że program nie ma `null` prawidłowej wartości.</span><span class="sxs-lookup"><span data-stu-id="a885e-116">This is because `Nullable<'T>` does not have `null` as a proper value.</span></span>

## <a name="pass-and-assign-to-members"></a><span data-ttu-id="a885e-117">Przekaż i przypisz do członków</span><span class="sxs-lookup"><span data-stu-id="a885e-117">Pass and assign to members</span></span>

<span data-ttu-id="a885e-118">Kluczowa różnica między pracą z elementami członkowskimi i F # polega na tym, że typy wartości null mogą być niejawnie wywnioskowane podczas pracy z członkami.</span><span class="sxs-lookup"><span data-stu-id="a885e-118">A key difference between working with members and F# values is that nullable value types can be implicitly inferred when you're working with members.</span></span> <span data-ttu-id="a885e-119">Rozważmy następującą metodę, która przyjmuje typ wartości null jako dane wejściowe:</span><span class="sxs-lookup"><span data-stu-id="a885e-119">Consider the following method that takes a nullable value type as input:</span></span>

```fsharp
type C() =
    member _.M(x: Nullable<int>) = x.HasValue
    member val NVT = Nullable 12 with get, set

let c = C()
c.M(12)
c.NVT <- 12
```

<span data-ttu-id="a885e-120">W poprzednim przykładzie można przekazać `12` do metody `M` .</span><span class="sxs-lookup"><span data-stu-id="a885e-120">In the previous example, you can pass `12` to the method `M`.</span></span> <span data-ttu-id="a885e-121">Można również przypisać `12` do właściwości `NVT` Auto.</span><span class="sxs-lookup"><span data-stu-id="a885e-121">You can also assign `12` to the auto property `NVT`.</span></span> <span data-ttu-id="a885e-122">Jeśli dane wejściowe mogą być skonstruowane jako typ wartości null i są zgodne z typem docelowym, kompilator języka F # niejawnie przekonwertuje takie wywołania lub przypisania.</span><span class="sxs-lookup"><span data-stu-id="a885e-122">If the input can be constructed as a nullable value type and it matches the target type, the F# compiler will implicitly convert such calls or assignments.</span></span>

## <a name="examine-a-nullable-value-type-instance"></a><span data-ttu-id="a885e-123">Badanie wystąpienia typu wartości null</span><span class="sxs-lookup"><span data-stu-id="a885e-123">Examine a nullable value type instance</span></span>

<span data-ttu-id="a885e-124">W przeciwieństwie do [opcji](options.md), które są uogólnioną konstrukcją dla reprezentowania możliwej wartości, typy wartości null nie są używane z dopasowywaniem do wzorca.</span><span class="sxs-lookup"><span data-stu-id="a885e-124">Unlike [Options](options.md), which are a generalized construct for representing a possible value, nullable value types are not used with pattern matching.</span></span> <span data-ttu-id="a885e-125">Zamiast tego należy użyć [`if`](conditional-expressions-if-then-else.md) wyrażenia i sprawdzić `HasValue` Właściwość.</span><span class="sxs-lookup"><span data-stu-id="a885e-125">Instead, you need to use an [`if`](conditional-expressions-if-then-else.md) expression and check the `HasValue` property.</span></span>

<span data-ttu-id="a885e-126">Aby uzyskać wartość bazową, należy użyć `Value` właściwości po `HasValue` sprawdzeniu, tak jak to zrobić:</span><span class="sxs-lookup"><span data-stu-id="a885e-126">To get the underlying value, use the `Value` property after a `HasValue` check, like so:</span></span>

```fsharp
open System

let a = Nullable 42

if a.HasValue then
    printfn $"{a} is {a.Value}"
else
    printfn $"{a} has no value."
```

## <a name="nullable-operators"></a><span data-ttu-id="a885e-127">Operatory dopuszczające wartość null</span><span class="sxs-lookup"><span data-stu-id="a885e-127">Nullable operators</span></span>

<span data-ttu-id="a885e-128">Operacje na typach wartości null, takich jak arytmetyczne lub porównania, mogą wymagać użycia [operatorów dopuszczających wartości null](symbol-and-operator-reference/nullable-operators.md).</span><span class="sxs-lookup"><span data-stu-id="a885e-128">Operations on nullable value types, such as arithmetic or comparison, can require the use of [nullable operators](symbol-and-operator-reference/nullable-operators.md).</span></span>

<span data-ttu-id="a885e-129">Można dokonać konwersji z jednego typu wartości null na inny przy użyciu operatorów konwersji z `FSharp.Linq` przestrzeni nazw:</span><span class="sxs-lookup"><span data-stu-id="a885e-129">You can convert from one nullable value type to another using conversion operators from the `FSharp.Linq` namespace:</span></span>

```fsharp
open System
open FSharp.Linq

let nullableInt = Nullable 10
let nullableFloat = Nullable.float nullableInt
```

<span data-ttu-id="a885e-130">Można również użyć odpowiedniego operatora, który nie dopuszcza wartości null, do konwersji na typ pierwotny, co powoduje, że występuje wyjątek, jeśli nie ma wartości:</span><span class="sxs-lookup"><span data-stu-id="a885e-130">You can also use an appropriate non-nullable operator to convert to a primitive type, risking an exception if it has no value:</span></span>

```fsharp
open System
open FSharp.Linq

let nullableInt = Nullable 10
let nullableFloat = Nullable.float nullableInt

printfn $"value is %f{float nullableFloat}"
```

<span data-ttu-id="a885e-131">Operatorów dopuszczających wartości null można także używać jako krótkich celów sprawdzania `HasValue` i `Value` :</span><span class="sxs-lookup"><span data-stu-id="a885e-131">You can also use nullable operators as a short-hand for checking `HasValue` and `Value`:</span></span>

```fsharp
open System
open FSharp.Linq

let nullableInt = Nullable 10
let nullableFloat = Nullable.float nullableInt

let isBigger = nullableFloat ?> 1.0
let isBiggerLongForm = nullableFloat.HasValue && nullableFloat.Value > 1.0
```

<span data-ttu-id="a885e-132">`?>`Porównanie sprawdza, czy po lewej stronie nie dopuszcza wartości null i tylko wtedy, gdy ma wartość.</span><span class="sxs-lookup"><span data-stu-id="a885e-132">The `?>` comparison checks if the left-hand side is nullable and only succeeds if it has a value.</span></span> <span data-ttu-id="a885e-133">Jest to równoznaczne z wierszem, który następuje po nim.</span><span class="sxs-lookup"><span data-stu-id="a885e-133">It is equivalent to the line that follows it.</span></span>

## <a name="see-also"></a><span data-ttu-id="a885e-134">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="a885e-134">See also</span></span>

- [<span data-ttu-id="a885e-135">Struktury</span><span class="sxs-lookup"><span data-stu-id="a885e-135">Structures</span></span>](structures.md)
- [<span data-ttu-id="a885e-136">Opcje języka F #</span><span class="sxs-lookup"><span data-stu-id="a885e-136">F# Options</span></span>](options.md)
