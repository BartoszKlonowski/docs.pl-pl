---
title: Sumy rozłączne
description: 'Dowiedz się, jak używać związków rozłącznych w języku F #.'
ms.date: 08/15/2020
ms.openlocfilehash: f90ac2c2ea21182cf5fd3657d2ada00a763139fe
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740240"
---
# <a name="discriminated-unions"></a><span data-ttu-id="390ce-103">Sumy rozłączne</span><span class="sxs-lookup"><span data-stu-id="390ce-103">Discriminated Unions</span></span>

<span data-ttu-id="390ce-104">Związki rozłączne zapewniają obsługę wartości, które mogą być jedną z wielu nazwanych przypadków, prawdopodobnie z różnymi wartościami i typami.</span><span class="sxs-lookup"><span data-stu-id="390ce-104">Discriminated unions provide support for values that can be one of a number of named cases, possibly each with different values and types.</span></span> <span data-ttu-id="390ce-105">Związki rozłącznych są przydatne w przypadku danych heterogenicznych; dane, które mogą mieć specjalne przypadki, w tym prawidłowe i błędne przypadki; dane, które różnią się w typie z jednego wystąpienia na inne; i jako alternatywę dla małych hierarchii obiektów.</span><span class="sxs-lookup"><span data-stu-id="390ce-105">Discriminated unions are useful for heterogeneous data; data that can have special cases, including valid and error cases; data that varies in type from one instance to another; and as an alternative for small object hierarchies.</span></span> <span data-ttu-id="390ce-106">Ponadto cykliczne związki rozłącznych są używane do reprezentowania struktur danych drzewa.</span><span class="sxs-lookup"><span data-stu-id="390ce-106">In addition, recursive discriminated unions are used to represent tree data structures.</span></span>

## <a name="syntax"></a><span data-ttu-id="390ce-107">Składnia</span><span class="sxs-lookup"><span data-stu-id="390ce-107">Syntax</span></span>

```fsharp
[ attributes ]
type [accessibility-modifier] type-name =
    | case-identifier1 [of [ fieldname1 : ] type1 [ * [ fieldname2 : ] type2 ...]
    | case-identifier2 [of [fieldname3 : ]type3 [ * [ fieldname4 : ]type4 ...]

    [ member-list ]
```

## <a name="remarks"></a><span data-ttu-id="390ce-108">Uwagi</span><span class="sxs-lookup"><span data-stu-id="390ce-108">Remarks</span></span>

<span data-ttu-id="390ce-109">Związki rozłączne są podobne do typów Unii w innych językach, ale istnieją różnice.</span><span class="sxs-lookup"><span data-stu-id="390ce-109">Discriminated unions are similar to union types in other languages, but there are differences.</span></span> <span data-ttu-id="390ce-110">Podobnie jak w przypadku typu Unii w języku C++ lub typu wariantowego w Visual Basic, dane przechowywane w wartości nie są naprawione; może to być jedna z kilku odrębnych opcji.</span><span class="sxs-lookup"><span data-stu-id="390ce-110">As with a union type in C++ or a variant type in Visual Basic, the data stored in the value is not fixed; it can be one of several distinct options.</span></span> <span data-ttu-id="390ce-111">Jednak w przeciwieństwie do Unii w tych innych językach, każda z możliwych opcji ma *Identyfikator przypadku*.</span><span class="sxs-lookup"><span data-stu-id="390ce-111">Unlike unions in these other languages, however, each of the possible options is given a *case identifier*.</span></span> <span data-ttu-id="390ce-112">Identyfikatory przypadków są nazwami różnych możliwych typów wartości, które obiekty tego typu mogą być; wartości są opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="390ce-112">The case identifiers are names for the various possible types of values that objects of this type could be; the values are optional.</span></span> <span data-ttu-id="390ce-113">Jeśli wartości nie są obecne, sprawa jest równoważna z wielkością liter wyliczenia.</span><span class="sxs-lookup"><span data-stu-id="390ce-113">If values are not present, the case is equivalent to an enumeration case.</span></span> <span data-ttu-id="390ce-114">Jeśli wartości są obecne, każda wartość może być pojedynczą wartością określonego typu lub krotką agregującą wiele pól tego samego lub różnych typów.</span><span class="sxs-lookup"><span data-stu-id="390ce-114">If values are present, each value can either be a single value of a specified type, or a tuple that aggregates multiple fields of the same or different types.</span></span> <span data-ttu-id="390ce-115">Można nadać pojedynczemu polu nazwę, ale nazwa jest opcjonalna, nawet jeśli inne pola w tym samym przypadku mają nazwę.</span><span class="sxs-lookup"><span data-stu-id="390ce-115">You can give an individual field a name, but the name is optional, even if other fields in the same case are named.</span></span>

<span data-ttu-id="390ce-116">Dostępność dla Unii rozłącznych jest domyślnie ustawiona na `public` .</span><span class="sxs-lookup"><span data-stu-id="390ce-116">Accessibility for discriminated unions defaults to `public`.</span></span>

<span data-ttu-id="390ce-117">Rozważmy na przykład następującą deklarację typu kształtu.</span><span class="sxs-lookup"><span data-stu-id="390ce-117">For example, consider the following declaration of a Shape type.</span></span>

```fsharp
type Shape =
    | Rectangle of width : float * length : float
    | Circle of radius : float
    | Prism of width : float * float * height : float
```

<span data-ttu-id="390ce-118">Poprzedni kod deklaruje kształt Unii rozłącznej, który może mieć wartości z trzech przypadków: prostokąt, okrąg i biblioteki Prism.</span><span class="sxs-lookup"><span data-stu-id="390ce-118">The preceding code declares a discriminated union Shape, which can have values of any of three cases: Rectangle, Circle, and Prism.</span></span> <span data-ttu-id="390ce-119">Każdy przypadek ma inny zestaw pól.</span><span class="sxs-lookup"><span data-stu-id="390ce-119">Each case has a different set of fields.</span></span> <span data-ttu-id="390ce-120">Przypadek prostokąta ma dwa nazwane pola, oba typy `float` , które mają szerokość i długość.</span><span class="sxs-lookup"><span data-stu-id="390ce-120">The Rectangle case has two named fields, both of type `float`, that have the names width and length.</span></span> <span data-ttu-id="390ce-121">Przypadek okręgu ma tylko jedno nazwane pole, promień.</span><span class="sxs-lookup"><span data-stu-id="390ce-121">The Circle case has just one named field, radius.</span></span> <span data-ttu-id="390ce-122">Przypadek biblioteki Prism ma trzy pola, dwa z których (szerokość i wysokość) są nazwanymi polami.</span><span class="sxs-lookup"><span data-stu-id="390ce-122">The Prism case has three fields, two of which (width and height) are named fields.</span></span> <span data-ttu-id="390ce-123">Pola nienazwane są określane jako pola anonimowe.</span><span class="sxs-lookup"><span data-stu-id="390ce-123">Unnamed fields are referred to as anonymous fields.</span></span>

<span data-ttu-id="390ce-124">Obiekty są konstruowane przez podanie wartości pól nazwanych i anonimowych zgodnie z poniższymi przykładami.</span><span class="sxs-lookup"><span data-stu-id="390ce-124">You construct objects by providing values for the named and anonymous fields according to the following examples.</span></span>

```fsharp
let rect = Rectangle(length = 1.3, width = 10.0)
let circ = Circle (1.0)
let prism = Prism(5., 2.0, height = 3.0)
```

<span data-ttu-id="390ce-125">Ten kod pokazuje, że można użyć nazwanych pól w inicjalizacji lub można polegać na kolejności pól w deklaracji i po prostu podać wartości dla każdego pola.</span><span class="sxs-lookup"><span data-stu-id="390ce-125">This code shows that you can either use the named fields in the initialization, or you can rely on the ordering of the fields in the declaration and just provide the values for each field in turn.</span></span> <span data-ttu-id="390ce-126">Wywołanie konstruktora dla `rect` w poprzednim kodzie używa nazwanych pól, ale wywołanie konstruktora `circ` używa kolejności.</span><span class="sxs-lookup"><span data-stu-id="390ce-126">The constructor call for `rect` in the previous code uses the named fields, but the constructor call for `circ` uses the ordering.</span></span> <span data-ttu-id="390ce-127">Można mieszać pola uporządkowane i nazwane pola, jak w konstrukcji `prism` .</span><span class="sxs-lookup"><span data-stu-id="390ce-127">You can mix the ordered fields and named fields, as in the construction of `prism`.</span></span>

<span data-ttu-id="390ce-128">`option`Typ to prosty związek rozłącznych w podstawowej bibliotece języka F #.</span><span class="sxs-lookup"><span data-stu-id="390ce-128">The `option` type is a simple discriminated union in the F# core library.</span></span> <span data-ttu-id="390ce-129">`option`Typ jest zadeklarowany w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="390ce-129">The `option` type is declared as follows.</span></span>

```fsharp
// The option type is a discriminated union.
type Option<'a> =
    | Some of 'a
    | None
```

<span data-ttu-id="390ce-130">Poprzedni kod określa, że typ `Option` jest Unią rozłącznych, która ma dwa przypadki `Some` i `None` .</span><span class="sxs-lookup"><span data-stu-id="390ce-130">The previous code specifies that the type `Option` is a discriminated union that has two cases, `Some` and `None`.</span></span> <span data-ttu-id="390ce-131">`Some`Przypadek ma skojarzoną wartość, która składa się z jednego pola anonimowego, którego typ jest reprezentowany przez parametr typu `'a` .</span><span class="sxs-lookup"><span data-stu-id="390ce-131">The `Some` case has an associated value that consists of one anonymous field whose type is represented by the type parameter `'a`.</span></span> <span data-ttu-id="390ce-132">`None`Przypadek nie ma skojarzonej wartości.</span><span class="sxs-lookup"><span data-stu-id="390ce-132">The `None` case has no associated value.</span></span> <span data-ttu-id="390ce-133">W tym celu `option` Typ określa typ ogólny, który ma wartość pewnego typu lub nie ma wartości.</span><span class="sxs-lookup"><span data-stu-id="390ce-133">Thus the `option` type specifies a generic type that either has a value of some type or no value.</span></span> <span data-ttu-id="390ce-134">Typ `Option` ma również alias typu małe litery, `option` który jest częściej często używany.</span><span class="sxs-lookup"><span data-stu-id="390ce-134">The type `Option` also has a lowercase type alias, `option`, that is more commonly used.</span></span>

<span data-ttu-id="390ce-135">Identyfikatory przypadków mogą służyć jako konstruktory dla typu Unii rozłącznej.</span><span class="sxs-lookup"><span data-stu-id="390ce-135">The case identifiers can be used as constructors for the discriminated union type.</span></span> <span data-ttu-id="390ce-136">Na przykład poniższy kod służy do tworzenia wartości `option` typu.</span><span class="sxs-lookup"><span data-stu-id="390ce-136">For example, the following code is used to create values of the `option` type.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2001.fs)]

<span data-ttu-id="390ce-137">Identyfikatory przypadków są również używane w wyrażeniach dopasowania wzorców.</span><span class="sxs-lookup"><span data-stu-id="390ce-137">The case identifiers are also used in pattern matching expressions.</span></span> <span data-ttu-id="390ce-138">W wyrażeniu dopasowania do wzorca identyfikatory są udostępniane dla wartości skojarzonych z indywidualnymi przypadkami.</span><span class="sxs-lookup"><span data-stu-id="390ce-138">In a pattern matching expression, identifiers are provided for the values associated with the individual cases.</span></span> <span data-ttu-id="390ce-139">Na przykład, w poniższym kodzie, `x` jest identyfikatorem, który ma wartość, która jest skojarzona z `Some` wielkością liter `option` typu.</span><span class="sxs-lookup"><span data-stu-id="390ce-139">For example, in the following code, `x` is the identifier given the value that is associated with the `Some` case of the `option` type.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2002.fs)]

<span data-ttu-id="390ce-140">W wyrażeniach dopasowania do wzorca można użyć nazwanych pól do określenia dopasowania złożenia rozłącznych.</span><span class="sxs-lookup"><span data-stu-id="390ce-140">In pattern matching expressions, you can use named fields to specify discriminated union matches.</span></span> <span data-ttu-id="390ce-141">Dla typu kształtu, który został zadeklarowany wcześniej, można użyć nazwanych pól, jak pokazano w poniższym kodzie, aby wyodrębnić wartości pól.</span><span class="sxs-lookup"><span data-stu-id="390ce-141">For the Shape type that was declared previously, you can use the named fields as the following code shows to extract the values of the fields.</span></span>

```fsharp
let getShapeWidth shape =
    match shape with
    | Rectangle(width = w) -> w
    | Circle(radius = r) -> 2. * r
    | Prism(width = w) -> w
```

<span data-ttu-id="390ce-142">Zwykle identyfikatory przypadków mogą być używane bez kwalifikowania ich do nazwy związku.</span><span class="sxs-lookup"><span data-stu-id="390ce-142">Normally, the case identifiers can be used without qualifying them with the name of the union.</span></span> <span data-ttu-id="390ce-143">Jeśli chcesz, aby nazwa była zawsze kwalifikowana nazwą Unii, możesz zastosować atrybut [RequireQualifiedAccess](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-requirequalifiedaccessattribute.html) do definicji typu Unii.</span><span class="sxs-lookup"><span data-stu-id="390ce-143">If you want the name to always be qualified with the name of the union, you can apply the [RequireQualifiedAccess](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-requirequalifiedaccessattribute.html) attribute to the union type definition.</span></span>

### <a name="unwrapping-discriminated-unions"></a><span data-ttu-id="390ce-144">Odpakowanie związków rozłącznych</span><span class="sxs-lookup"><span data-stu-id="390ce-144">Unwrapping Discriminated Unions</span></span>

<span data-ttu-id="390ce-145">W przypadku Unii rozłącznych w języku F # często są używane do modelowania domen do zawijania jednego typu.</span><span class="sxs-lookup"><span data-stu-id="390ce-145">In F# Discriminated Unions are often used in domain-modeling for wrapping a single type.</span></span> <span data-ttu-id="390ce-146">Można łatwo wyodrębnić podstawową wartość poprzez dopasowanie do wzorca.</span><span class="sxs-lookup"><span data-stu-id="390ce-146">It's easy to extract the underlying value via pattern matching as well.</span></span> <span data-ttu-id="390ce-147">Nie musisz używać wyrażenia dopasowania dla pojedynczego przypadku:</span><span class="sxs-lookup"><span data-stu-id="390ce-147">You don't need to use a match expression for a single case:</span></span>

```fsharp
let ([UnionCaseIdentifier] [values]) = [UnionValue]
```

<span data-ttu-id="390ce-148">Poniższy przykład ilustruje:</span><span class="sxs-lookup"><span data-stu-id="390ce-148">The following example demonstrates this:</span></span>

```fsharp
type ShaderProgram = | ShaderProgram of id:int

let someFunctionUsingShaderProgram shaderProgram =
    let (ShaderProgram id) = shaderProgram
    // Use the unwrapped value
    ...
```

<span data-ttu-id="390ce-149">Dopasowywanie do wzorca jest również dozwolone bezpośrednio w parametrach funkcji, więc można odwinąć pojedynczy przypadek:</span><span class="sxs-lookup"><span data-stu-id="390ce-149">Pattern matching is also allowed directly in function parameters, so you can unwrap a single case there:</span></span>

```fsharp
let someFunctionUsingShaderProgram (ShaderProgram id) =
    // Use the unwrapped value
    ...
```

## <a name="struct-discriminated-unions"></a><span data-ttu-id="390ce-150">Związki rozłącznych struktur</span><span class="sxs-lookup"><span data-stu-id="390ce-150">Struct Discriminated Unions</span></span>

<span data-ttu-id="390ce-151">Można również reprezentować związki rozłączne jako struktury.</span><span class="sxs-lookup"><span data-stu-id="390ce-151">You can also represent Discriminated Unions as structs.</span></span>  <span data-ttu-id="390ce-152">Jest to realizowane przy użyciu `[<Struct>]` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="390ce-152">This is done with the `[<Struct>]` attribute.</span></span>

```fsharp
[<Struct>]
type SingleCase = Case of string

[<Struct>]
type Multicase =
    | Case1 of Case1 : string
    | Case2 of Case2 : int
    | Case3 of Case3 : double
```

<span data-ttu-id="390ce-153">Ponieważ są to typy wartości i nie są typami odwołań, istnieją dodatkowe zagadnienia w porównaniu z odniesiemi się do związków rozłącznych:</span><span class="sxs-lookup"><span data-stu-id="390ce-153">Because these are value types and not reference types, there are extra considerations compared with reference discriminated unions:</span></span>

1. <span data-ttu-id="390ce-154">Są one kopiowane jako typy wartości i mają semantykę typu wartości.</span><span class="sxs-lookup"><span data-stu-id="390ce-154">They are copied as value types and have value type semantics.</span></span>
2. <span data-ttu-id="390ce-155">Nie można użyć definicji typu cyklicznego z wieloliterowym związkiem rozłącznych struktury.</span><span class="sxs-lookup"><span data-stu-id="390ce-155">You cannot use a recursive type definition with a multicase struct Discriminated Union.</span></span>
3. <span data-ttu-id="390ce-156">Należy podać unikatowe nazwy przypadków dla wieloliterowego związku wieloskładnikowego.</span><span class="sxs-lookup"><span data-stu-id="390ce-156">You must provide unique case names for a multicase struct Discriminated Union.</span></span>

## <a name="using-discriminated-unions-instead-of-object-hierarchies"></a><span data-ttu-id="390ce-157">Używanie Unii rozłącznych zamiast hierarchii obiektów</span><span class="sxs-lookup"><span data-stu-id="390ce-157">Using Discriminated Unions Instead of Object Hierarchies</span></span>

<span data-ttu-id="390ce-158">W przypadku niewielkiej alternatywy dla hierarchii obiektów często można użyć Unii rozłącznej.</span><span class="sxs-lookup"><span data-stu-id="390ce-158">You can often use a discriminated union as a simpler alternative to a small object hierarchy.</span></span> <span data-ttu-id="390ce-159">Na przykład, można użyć poniższego związku rozłącznych zamiast `Shape` klasy bazowej, która ma typy pochodne dla okręgu, kwadratu itd.</span><span class="sxs-lookup"><span data-stu-id="390ce-159">For example, the following discriminated union could be used instead of a `Shape` base class that has derived types for circle, square, and so on.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2003.fs)]

<span data-ttu-id="390ce-160">Zamiast metody wirtualnej do obliczenia obszaru lub obwodu, jak w przypadku implementacji zorientowanej obiektowo, można użyć dopasowania wzorców do gałęzi do odpowiednich formuł, aby obliczyć te ilości.</span><span class="sxs-lookup"><span data-stu-id="390ce-160">Instead of a virtual method to compute an area or perimeter, as you would use in an object-oriented implementation, you can use pattern matching to branch to appropriate formulas to compute these quantities.</span></span> <span data-ttu-id="390ce-161">W poniższym przykładzie różne formuły są używane do obliczania obszaru, w zależności od kształtu.</span><span class="sxs-lookup"><span data-stu-id="390ce-161">In the following example, different formulas are used to compute the area, depending on the shape.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2004.fs)]

<span data-ttu-id="390ce-162">Wynik jest następujący:</span><span class="sxs-lookup"><span data-stu-id="390ce-162">The output is as follows:</span></span>

```console
Area of circle that has radius 15.000000: 706.858347
Area of square that has side 10.000000: 100.000000
Area of rectangle that has height 5.000000 and width 10.000000 is 50.000000
```

## <a name="using-discriminated-unions-for-tree-data-structures"></a><span data-ttu-id="390ce-163">Używanie związków rozłącznych dla struktur danych drzewa</span><span class="sxs-lookup"><span data-stu-id="390ce-163">Using Discriminated Unions for Tree Data Structures</span></span>

<span data-ttu-id="390ce-164">Związki rozłączne mogą być cykliczne, co oznacza, że sama Unia może być uwzględniona w typie jednego lub więcej przypadków.</span><span class="sxs-lookup"><span data-stu-id="390ce-164">Discriminated unions can be recursive, meaning that the union itself can be included in the type of one or more cases.</span></span> <span data-ttu-id="390ce-165">Cykliczne związki rozłącznych mogą służyć do tworzenia struktur drzewa, które są używane do modelowania wyrażeń w językach programowania.</span><span class="sxs-lookup"><span data-stu-id="390ce-165">Recursive discriminated unions can be used to create tree structures, which are used to model expressions in programming languages.</span></span> <span data-ttu-id="390ce-166">W poniższym kodzie rekursywny związek rozłącznych służy do tworzenia struktury danych drzewa binarnego.</span><span class="sxs-lookup"><span data-stu-id="390ce-166">In the following code, a recursive discriminated union is used to create a binary tree data structure.</span></span> <span data-ttu-id="390ce-167">Unia składa się z dwóch przypadków, `Node` , który jest węzłem z wartością całkowitą oraz poddrzewami z lewej i prawej strony, i `Tip` , który kończy drzewo.</span><span class="sxs-lookup"><span data-stu-id="390ce-167">The union consists of two cases, `Node`, which is a node with an integer value and left and right subtrees, and `Tip`, which terminates the tree.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2005.fs)]

<span data-ttu-id="390ce-168">W poprzednim kodzie `resultSumTree` ma wartość 10.</span><span class="sxs-lookup"><span data-stu-id="390ce-168">In the previous code, `resultSumTree` has the value 10.</span></span> <span data-ttu-id="390ce-169">Na poniższej ilustracji przedstawiono strukturę drzewa dla programu `myTree` .</span><span class="sxs-lookup"><span data-stu-id="390ce-169">The following illustration shows the tree structure for `myTree`.</span></span>

![Diagram przedstawiający strukturę drzewa dla drzewa.](../media/discriminated-unions/tree-structure-mytree.png)

<span data-ttu-id="390ce-171">Związki rozłączne działają prawidłowo, jeśli węzły w drzewie są heterogeniczne.</span><span class="sxs-lookup"><span data-stu-id="390ce-171">Discriminated unions work well if the nodes in the tree are heterogeneous.</span></span> <span data-ttu-id="390ce-172">W poniższym kodzie typ `Expression` reprezentuje drzewo abstrakcyjnej składni wyrażenia w prostym języku programowania, który obsługuje dodawanie i mnożenie liczb i zmiennych.</span><span class="sxs-lookup"><span data-stu-id="390ce-172">In the following code, the type `Expression` represents the abstract syntax tree of an expression in a simple programming language that supports addition and multiplication of numbers and variables.</span></span> <span data-ttu-id="390ce-173">Niektóre przypadki Unii nie są cykliczne i reprezentują liczby ( `Number` ) lub zmienne ( `Variable` ).</span><span class="sxs-lookup"><span data-stu-id="390ce-173">Some of the union cases are not recursive and represent either numbers (`Number`) or variables (`Variable`).</span></span> <span data-ttu-id="390ce-174">Inne przypadki są cykliczne i reprezentują operacje ( `Add` i `Multiply` ), gdzie operandy są również wyrażeniami.</span><span class="sxs-lookup"><span data-stu-id="390ce-174">Other cases are recursive, and represent operations (`Add` and `Multiply`), where the operands are also expressions.</span></span> <span data-ttu-id="390ce-175">`Evaluate`Funkcja używa wyrażenia dopasowania, aby rekursywnie przetworzyć drzewo składni.</span><span class="sxs-lookup"><span data-stu-id="390ce-175">The `Evaluate` function uses a match expression to recursively process the syntax tree.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2006.fs)]

<span data-ttu-id="390ce-176">Gdy ten kod jest wykonywany, wartość jest równa `result` 5.</span><span class="sxs-lookup"><span data-stu-id="390ce-176">When this code is executed, the value of `result` is 5.</span></span>

## <a name="members"></a><span data-ttu-id="390ce-177">Elementy członkowskie</span><span class="sxs-lookup"><span data-stu-id="390ce-177">Members</span></span>

<span data-ttu-id="390ce-178">Istnieje możliwość zdefiniowania elementów członkowskich w Unii rozłącznych.</span><span class="sxs-lookup"><span data-stu-id="390ce-178">It is possible to define members on discriminated unions.</span></span> <span data-ttu-id="390ce-179">Poniższy przykład pokazuje, jak zdefiniować Właściwość i zaimplementować interfejs:</span><span class="sxs-lookup"><span data-stu-id="390ce-179">The following example shows how to define a property and implement an interface:</span></span>

```fsharp
open System

type IPrintable =
    abstract Print: unit -> unit

type Shape =
    | Circle of float
    | EquilateralTriangle of float
    | Square of float
    | Rectangle of float * float

    member this.Area =
        match this with
        | Circle r -> 2.0 * Math.PI * r
        | EquilateralTriangle s -> s * s * sqrt 3.0 / 4.0
        | Square s -> s * s
        | Rectangle(l, w) -> l * w

    interface IPrintable with
        member this.Print () =
            match this with
            | Circle r -> printfn $"Circle with radius %f{r}"
            | EquilateralTriangle s -> printfn $"Equilateral Triangle of side %f{s}"
            | Square s -> printfn $"Square with side %f{s}"
            | Rectangle(l, w) -> printfn $"Rectangle with length %f{l} and width %f{w}"
```

## <a name="common-attributes"></a><span data-ttu-id="390ce-180">Atrybuty wspólne</span><span class="sxs-lookup"><span data-stu-id="390ce-180">Common attributes</span></span>

<span data-ttu-id="390ce-181">Następujące atrybuty są często obserwowane w Unii rozłącznych:</span><span class="sxs-lookup"><span data-stu-id="390ce-181">The following attributes are commonly seen in discriminated unions:</span></span>

- `[<RequireQualifiedAccess>]`
- `[<NoEquality>]`
- `[<NoComparison>]`
- `[<Struct>]`

## <a name="see-also"></a><span data-ttu-id="390ce-182">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="390ce-182">See also</span></span>

- [<span data-ttu-id="390ce-183">Dokumentacja języka F #</span><span class="sxs-lookup"><span data-stu-id="390ce-183">F# Language Reference</span></span>](index.md)
