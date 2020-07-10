---
title: Wybór między typami anonimowymi a kolekcjami
description: Dowiedz się, kiedy należy wybrać typy anonimowe i typ krotki.
author: IEvangelist
ms.author: dapine
ms.date: 07/01/2020
ms.technology: dotnet-standard
ms.openlocfilehash: 9c186133a639faf187c89d872856d860a20f5a2d
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/09/2020
ms.locfileid: "86174221"
---
# <a name="choosing-between-anonymous-and-tuple-types"></a><span data-ttu-id="b2c9c-103">Wybór między typami anonimowymi a kolekcjami</span><span class="sxs-lookup"><span data-stu-id="b2c9c-103">Choosing between anonymous and tuple types</span></span>

<span data-ttu-id="b2c9c-104">Wybór odpowiedniego typu polega na uwzględnieniu jego użyteczności, wydajności i kompromisów w porównaniu z innymi typami.</span><span class="sxs-lookup"><span data-stu-id="b2c9c-104">Choosing the appropriate type involves considering its usability, performance, and tradeoffs compared to other types.</span></span> <span data-ttu-id="b2c9c-105">Typy anonimowe zostały udostępnione od języka C# 3,0, podczas gdy <xref:System.Tuple%602?displayProperty=nameWithType> typy ogólne zostały wprowadzone z .NET Framework 4,0.</span><span class="sxs-lookup"><span data-stu-id="b2c9c-105">Anonymous types have been available since C# 3.0, while generic <xref:System.Tuple%602?displayProperty=nameWithType> types were introduced with .NET Framework 4.0.</span></span> <span data-ttu-id="b2c9c-106">Ponieważ następnie wprowadzono nowe opcje z obsługą poziomu języka, takie jak <xref:System.ValueTuple%602?displayProperty=nameWithType> nazwa oznacza, określ typ wartości z elastycznością typów anonimowych.</span><span class="sxs-lookup"><span data-stu-id="b2c9c-106">Since then new options have been introduced with language level support, such as <xref:System.ValueTuple%602?displayProperty=nameWithType> - which as the name implies, provide a value type with the flexibility of anonymous types.</span></span> <span data-ttu-id="b2c9c-107">W tym artykule dowiesz się, kiedy należy wybrać jeden typ z drugiego.</span><span class="sxs-lookup"><span data-stu-id="b2c9c-107">In this article, you'll learn when it's appropriate to choose one type over the other.</span></span>

## <a name="usability-and-functionality"></a><span data-ttu-id="b2c9c-108">Użyteczność i funkcje</span><span class="sxs-lookup"><span data-stu-id="b2c9c-108">Usability and functionality</span></span>

<span data-ttu-id="b2c9c-109">Typy anonimowe zostały wprowadzone w języku C# 3,0 z wyrażeniami programu Query-Integrated Language (LINQ).</span><span class="sxs-lookup"><span data-stu-id="b2c9c-109">Anonymous types were introduced in C# 3.0 with Language-Integrated Query (LINQ) expressions.</span></span> <span data-ttu-id="b2c9c-110">LINQ, deweloperzy często projektują wyniki zapytań w typach anonimowych, które zawierają kilka właściwości Select z obiektów, z którymi pracują.</span><span class="sxs-lookup"><span data-stu-id="b2c9c-110">With LINQ, developers often project results from queries into anonymous types that hold a few select properties from the objects they're working with.</span></span> <span data-ttu-id="b2c9c-111">Rozważmy poniższy przykład, który tworzy wystąpienie tablicy <xref:System.DateTime> obiektów i wykonuje iteracje w celu przechodzenia do typu anonimowego z dwiema właściwościami.</span><span class="sxs-lookup"><span data-stu-id="b2c9c-111">Consider the following example, that instantiates an array of <xref:System.DateTime> objects, and iterates through them projecting into an anonymous type with two properties.</span></span>

```csharp-interactive
var dates = new[]
{
    DateTime.UtcNow.AddHours(-1),
    DateTime.UtcNow,
    DateTime.UtcNow.AddHours(1),
};

foreach (var anonymous in
             dates.Select(
                 date => new { Formatted = $"{date:MMM dd, yyyy hh:mm zzz}", date.Ticks }))
{
    Console.WriteLine($"Ticks: {anonymous.Ticks}, formatted: {anonymous.Formatted}");
}
```

<span data-ttu-id="b2c9c-112">Typy anonimowe są tworzone przy użyciu [`new`](../../csharp/language-reference/operators/new-operator.md) operatora, a nazwy właściwości i typy są wywnioskowane z deklaracji.</span><span class="sxs-lookup"><span data-stu-id="b2c9c-112">Anonymous types are instantiated by using the [`new`](../../csharp/language-reference/operators/new-operator.md) operator, and the property names and types are inferred from the declaration.</span></span> <span data-ttu-id="b2c9c-113">Jeśli co najmniej dwa anonimowe Inicjatory obiektów w tym samym zestawie określają sekwencję właściwości, które są w tej samej kolejności i mają takie same nazwy i typy, kompilator traktuje obiekty jako wystąpienia tego samego typu.</span><span class="sxs-lookup"><span data-stu-id="b2c9c-113">If two or more anonymous object initializers in the same assembly specify a sequence of properties that are in the same order and that have the same names and types, the compiler treats the objects as instances of the same type.</span></span> <span data-ttu-id="b2c9c-114">Korzystają one z tych samych informacji o typie wygenerowanym przez kompilator.</span><span class="sxs-lookup"><span data-stu-id="b2c9c-114">They share the same compiler-generated type information.</span></span>

<span data-ttu-id="b2c9c-115">Poprzedni fragment kodu w języku C# projektuje typ anonimowy z dwiema właściwościami, podobnie jak w przypadku następującej klasy języka C# wygenerowanej przez kompilator:</span><span class="sxs-lookup"><span data-stu-id="b2c9c-115">The previous C# snippet projects an anonymous type with two properties, much like the following compiler-generated C# class:</span></span>

```csharp
internal sealed class f__AnonymousType0
{
    public string Formatted { get; }
    public long Ticks { get; }

    public f__AnonymousType0(string formatted, long ticks)
    {
        Formatted = formatted;
        Ticks = ticks;
    }
}
```

<span data-ttu-id="b2c9c-116">Aby uzyskać więcej informacji, zobacz [Typy anonimowe](../../csharp/programming-guide/classes-and-structs/anonymous-types.md).</span><span class="sxs-lookup"><span data-stu-id="b2c9c-116">For more information, see [anonymous types](../../csharp/programming-guide/classes-and-structs/anonymous-types.md).</span></span> <span data-ttu-id="b2c9c-117">Ta sama funkcja istnieje z krotkami podczas projekcji w zapytaniach LINQ, można wybrać właściwości w postaci krotek.</span><span class="sxs-lookup"><span data-stu-id="b2c9c-117">The same functionality exists with tuples when projecting into LINQ queries, you can select properties into tuples.</span></span> <span data-ttu-id="b2c9c-118">Te krotki przepływają przez zapytanie, podobnie jak typy anonimowe.</span><span class="sxs-lookup"><span data-stu-id="b2c9c-118">These tuples flow through the query, just as anonymous types would.</span></span> <span data-ttu-id="b2c9c-119">Teraz Rozważmy poniższy przykład przy użyciu `System.Tuple<string, long>` .</span><span class="sxs-lookup"><span data-stu-id="b2c9c-119">Now consider the following example using the `System.Tuple<string, long>`.</span></span>

```csharp-interactive
var dates = new[]
{
    DateTime.UtcNow.AddHours(-1),
    DateTime.UtcNow,
    DateTime.UtcNow.AddHours(1),
};

foreach (var tuple in
            dates.Select(
                date => new Tuple<string, long>($"{date:MMM dd, yyyy hh:mm zzz}", date.Ticks)))
{
    Console.WriteLine($"Ticks: {tuple.Item2}, formatted: {tuple.Item1}");
}
```

<span data-ttu-id="b2c9c-120">W <xref:System.Tuple%602?displayProperty=nameWithType> , wystąpienie uwidacznia właściwości elementów numerowanych, takich jak `Item1` , i `Item2` .</span><span class="sxs-lookup"><span data-stu-id="b2c9c-120">With the <xref:System.Tuple%602?displayProperty=nameWithType>, the instance exposes numbered item properties, such as `Item1`, and `Item2`.</span></span> <span data-ttu-id="b2c9c-121">Te nazwy właściwości mogą utrudnić zrozumienie intencji wartości właściwości, ponieważ nazwa właściwości zawiera tylko numer porządkowy.</span><span class="sxs-lookup"><span data-stu-id="b2c9c-121">These property names can make it more difficult to understand the intent of the property values, as the property name only provides the ordinal.</span></span> <span data-ttu-id="b2c9c-122">Ponadto `System.Tuple` typy są `class` typami odwołań.</span><span class="sxs-lookup"><span data-stu-id="b2c9c-122">Furthermore, the `System.Tuple` types are reference `class` types.</span></span> <span data-ttu-id="b2c9c-123"><xref:System.ValueTuple%602?displayProperty=nameWithType>Jednak jest to `struct` Typ wartości.</span><span class="sxs-lookup"><span data-stu-id="b2c9c-123">The <xref:System.ValueTuple%602?displayProperty=nameWithType> however, is a value `struct` type.</span></span> <span data-ttu-id="b2c9c-124">Poniższy fragment kodu w języku C# używa `ValueTuple<string, long>` do projektu w.</span><span class="sxs-lookup"><span data-stu-id="b2c9c-124">The following C# snippet, uses `ValueTuple<string, long>` to project into.</span></span> <span data-ttu-id="b2c9c-125">W tym celu przypisuje się przy użyciu składni literału.</span><span class="sxs-lookup"><span data-stu-id="b2c9c-125">In doing so, it assigns using a literal syntax.</span></span>

```csharp-interactive
var dates = new[]
{
    DateTime.UtcNow.AddHours(-1),
    DateTime.UtcNow,
    DateTime.UtcNow.AddHours(1),
};

foreach (var (formatted, ticks) in
            dates.Select(
                date => (Formatted: $"{date:MMM dd, yyyy at hh:mm zzz}", date.Ticks)))
{
    Console.WriteLine($"Ticks: {ticks}, formatted: {formatted}");
}
```

<span data-ttu-id="b2c9c-126">Aby uzyskać więcej informacji na temat krotek, zobacz [typy krotek (odwołanie w C#)](../../csharp/language-reference/builtin-types/value-tuples.md) lub [krotki (Visual Basic)](../../visual-basic/programming-guide/language-features/data-types/tuples.md).</span><span class="sxs-lookup"><span data-stu-id="b2c9c-126">For more information about tuples, see [Tuple types (C# reference)](../../csharp/language-reference/builtin-types/value-tuples.md) or [Tuples (Visual Basic)](../../visual-basic/programming-guide/language-features/data-types/tuples.md).</span></span>

<span data-ttu-id="b2c9c-127">Poprzednie przykłady to wszystkie funkcje równoważne, ale istnieją niewielkie różnice w ich użyteczności i ich podstawowych wdrożeniach.</span><span class="sxs-lookup"><span data-stu-id="b2c9c-127">The previous examples are all functionally equivalent, however; there are slight differences in their usability and their underlying implementations.</span></span>

## <a name="tradeoffs"></a><span data-ttu-id="b2c9c-128">Kompromisy</span><span class="sxs-lookup"><span data-stu-id="b2c9c-128">Tradeoffs</span></span>

<span data-ttu-id="b2c9c-129">Możesz chcieć zawsze używać <xref:System.ValueTuple> <xref:System.Tuple> typów i anonimowych, ale istnieją kompromisy, które należy wziąć pod uwagę.</span><span class="sxs-lookup"><span data-stu-id="b2c9c-129">You might want to always use <xref:System.ValueTuple> over <xref:System.Tuple>, and anonymous types, but there are tradeoffs you should consider.</span></span> <span data-ttu-id="b2c9c-130"><xref:System.ValueTuple>Typy są modyfikowalne, podczas gdy <xref:System.Tuple> są tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="b2c9c-130">The <xref:System.ValueTuple> types are mutable, whereas <xref:System.Tuple> are read-only.</span></span> <span data-ttu-id="b2c9c-131">Typy anonimowe mogą być używane w drzewach wyrażeń, natomiast kolekcje nie mogą.</span><span class="sxs-lookup"><span data-stu-id="b2c9c-131">Anonymous types can be used in expression trees, while tuples cannot.</span></span> <span data-ttu-id="b2c9c-132">Poniższa tabela zawiera omówienie niektórych różnic między kluczami.</span><span class="sxs-lookup"><span data-stu-id="b2c9c-132">The following table is an overview of some of the key differences.</span></span>

### <a name="key-differences"></a><span data-ttu-id="b2c9c-133">Podstawowe różnice</span><span class="sxs-lookup"><span data-stu-id="b2c9c-133">Key differences</span></span>

| <span data-ttu-id="b2c9c-134">Nazwa</span><span class="sxs-lookup"><span data-stu-id="b2c9c-134">Name</span></span>                     | <span data-ttu-id="b2c9c-135">Modyfikator dostępu</span><span class="sxs-lookup"><span data-stu-id="b2c9c-135">Access modifier</span></span> | <span data-ttu-id="b2c9c-136">Typ</span><span class="sxs-lookup"><span data-stu-id="b2c9c-136">Type</span></span>     | <span data-ttu-id="b2c9c-137">Nazwa niestandardowego elementu członkowskiego</span><span class="sxs-lookup"><span data-stu-id="b2c9c-137">Custom member name</span></span> | <span data-ttu-id="b2c9c-138">Obsługa dekonstrukcji</span><span class="sxs-lookup"><span data-stu-id="b2c9c-138">Deconstruction support</span></span> | <span data-ttu-id="b2c9c-139">Obsługa drzewa wyrażeń</span><span class="sxs-lookup"><span data-stu-id="b2c9c-139">Expression tree support</span></span> |
|--------------------------|-----------------|----------|----------------------|------------------------|-------------------------|
| <span data-ttu-id="b2c9c-140">Typy anonimowe</span><span class="sxs-lookup"><span data-stu-id="b2c9c-140">Anonymous types</span></span>          | `internal`      | `class`  | <span data-ttu-id="b2c9c-141">✔️</span><span class="sxs-lookup"><span data-stu-id="b2c9c-141">✔️</span></span>                   | ❌                     | <span data-ttu-id="b2c9c-142">✔️</span><span class="sxs-lookup"><span data-stu-id="b2c9c-142">✔️</span></span>                     |
| <xref:System.Tuple>      | `public`        | `class`  | ❌                   | ❌                     | <span data-ttu-id="b2c9c-143">✔️</span><span class="sxs-lookup"><span data-stu-id="b2c9c-143">✔️</span></span>                     |
| <xref:System.ValueTuple> | `public`        | `struct` | <span data-ttu-id="b2c9c-144">✔️</span><span class="sxs-lookup"><span data-stu-id="b2c9c-144">✔️</span></span>                   | <span data-ttu-id="b2c9c-145">✔️</span><span class="sxs-lookup"><span data-stu-id="b2c9c-145">✔️</span></span>                     | ❌                     |

### <a name="serialization"></a><span data-ttu-id="b2c9c-146">Serializacja</span><span class="sxs-lookup"><span data-stu-id="b2c9c-146">Serialization</span></span>

<span data-ttu-id="b2c9c-147">Jednym ważnym zagadnieniem podczas wybierania typu jest to, czy należy go serializować.</span><span class="sxs-lookup"><span data-stu-id="b2c9c-147">One important consideration when choosing a type, is whether or not it will need to be serialized.</span></span> <span data-ttu-id="b2c9c-148">Serializacja jest proces konwersji stan obiektu do formularza, które mogą być utrwalone lub transportowane.</span><span class="sxs-lookup"><span data-stu-id="b2c9c-148">Serialization is the process of converting the state of an object into a form that can be persisted or transported.</span></span> <span data-ttu-id="b2c9c-149">Aby uzyskać więcej informacji, zobacz [serializacji](../../csharp/programming-guide/concepts/serialization/index.md).</span><span class="sxs-lookup"><span data-stu-id="b2c9c-149">For more information, see [serialization](../../csharp/programming-guide/concepts/serialization/index.md).</span></span> <span data-ttu-id="b2c9c-150">Gdy Serializacja jest ważna, utworzenie `class` lub `struct` jest preferowana w przypadku typów anonimowych lub typów krotek.</span><span class="sxs-lookup"><span data-stu-id="b2c9c-150">When serialization is important, creating a `class` or `struct` is preferred over anonymous types or tuple types.</span></span>

## <a name="performance"></a><span data-ttu-id="b2c9c-151">Wydajność</span><span class="sxs-lookup"><span data-stu-id="b2c9c-151">Performance</span></span>

<span data-ttu-id="b2c9c-152">Wydajność między tymi typami zależy od scenariusza.</span><span class="sxs-lookup"><span data-stu-id="b2c9c-152">Performance between these types depends on the scenario.</span></span> <span data-ttu-id="b2c9c-153">Istotny wpływ obejmuje kompromis między przydziałami i kopiowaniem.</span><span class="sxs-lookup"><span data-stu-id="b2c9c-153">The major impact involves the tradeoff between allocations and copying.</span></span> <span data-ttu-id="b2c9c-154">W większości scenariuszy wpływ jest mały.</span><span class="sxs-lookup"><span data-stu-id="b2c9c-154">In most scenarios, the impact is small.</span></span> <span data-ttu-id="b2c9c-155">W przypadku wystąpienia poważnych wpływów należy podjąć pomiary w celu poinformowania o decyzji.</span><span class="sxs-lookup"><span data-stu-id="b2c9c-155">When major impacts could arise, measurements should be taken to inform the decision.</span></span>

## <a name="conclusion"></a><span data-ttu-id="b2c9c-156">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="b2c9c-156">Conclusion</span></span>

<span data-ttu-id="b2c9c-157">Jako deweloper wybierający między krotki a typami anonimowymi, istnieje kilka czynników, które należy wziąć pod uwagę.</span><span class="sxs-lookup"><span data-stu-id="b2c9c-157">As a developer choosing between tuples and anonymous types, there are several factors to consider.</span></span> <span data-ttu-id="b2c9c-158">Ogólnie mówiąc, jeśli nie pracujesz z [drzewami wyrażeń](../../csharp/expression-trees.md)i masz doświadczenie ze składnią krotek, wybierz <xref:System.ValueTuple> jako wartość typ wartości z elastycznością do nazwy właściwości.</span><span class="sxs-lookup"><span data-stu-id="b2c9c-158">Generally speaking, if you're not working with [expression trees](../../csharp/expression-trees.md), and you're comfortable with tuple syntax then choose <xref:System.ValueTuple> as they provide a value type with the flexibility to name properties.</span></span> <span data-ttu-id="b2c9c-159">Jeśli pracujesz z drzewami wyrażeń i wolisz nazwać właściwości, wybierz typy anonimowe.</span><span class="sxs-lookup"><span data-stu-id="b2c9c-159">If you're working with expression trees, and you'd prefer to name properties, choose anonymous types.</span></span> <span data-ttu-id="b2c9c-160">W przeciwnym razie użyj <xref:System.Tuple> .</span><span class="sxs-lookup"><span data-stu-id="b2c9c-160">Otherwise, use <xref:System.Tuple>.</span></span>

## <a name="see-also"></a><span data-ttu-id="b2c9c-161">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="b2c9c-161">See also</span></span>

- [<span data-ttu-id="b2c9c-162">Typy anonimowe</span><span class="sxs-lookup"><span data-stu-id="b2c9c-162">Anonymous types</span></span>](../../csharp/programming-guide/classes-and-structs/anonymous-types.md)
- [<span data-ttu-id="b2c9c-163">Drzewa wyrażeń</span><span class="sxs-lookup"><span data-stu-id="b2c9c-163">Expression trees</span></span>](../../csharp/expression-trees.md)
- [<span data-ttu-id="b2c9c-164">Typy krotek (odwołanie w C#)</span><span class="sxs-lookup"><span data-stu-id="b2c9c-164">Tuple types (C# reference)</span></span>](../../csharp/language-reference/builtin-types/value-tuples.md)
- [<span data-ttu-id="b2c9c-165">Krotki (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="b2c9c-165">Tuples (Visual Basic)</span></span>](../../visual-basic/programming-guide/language-features/data-types/tuples.md)
- [<span data-ttu-id="b2c9c-166">Typy — zalecenia dotyczące projektowania</span><span class="sxs-lookup"><span data-stu-id="b2c9c-166">Type design guidelines</span></span>](../design-guidelines/type.md)
