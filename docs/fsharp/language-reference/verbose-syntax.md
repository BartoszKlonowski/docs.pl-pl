---
title: Pełna składnia
description: 'Zapoznaj się z różnicą między pełną i uproszczoną składnią w języku programowania F #.'
ms.date: 05/16/2016
ms.openlocfilehash: 4e1725b58c8cb67c074ba12fd4ca25ce0c000a1e
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/16/2020
ms.locfileid: "97595180"
---
# <a name="verbose-syntax"></a><span data-ttu-id="67227-103">Pełna składnia</span><span class="sxs-lookup"><span data-stu-id="67227-103">Verbose Syntax</span></span>

<span data-ttu-id="67227-104">Istnieją dwie formy składni dostępne dla wielu konstrukcji w języku F #: *Pełna składnia* i *składnia uproszczona*.</span><span class="sxs-lookup"><span data-stu-id="67227-104">There are two forms of syntax available for many constructs in the F# language: *verbose syntax* and *lightweight syntax*.</span></span> <span data-ttu-id="67227-105">Składnia verbose nie jest zgodna z powszechnie używanymi, ale ma zalety mniejszej czułości do wcięcia.</span><span class="sxs-lookup"><span data-stu-id="67227-105">The verbose syntax is not as commonly used, but has the advantage of being less sensitive to indentation.</span></span> <span data-ttu-id="67227-106">Uproszczona składnia jest krótsza i używa wcięć do sygnalizowania początku i końca konstrukcji, zamiast dodatkowych słów kluczowych, takich jak `begin` ,, `end` `in` i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="67227-106">The lightweight syntax is shorter and uses indentation to signal the beginning and end of constructs, rather than additional keywords like `begin`, `end`, `in`, and so on.</span></span> <span data-ttu-id="67227-107">Domyślną składnią jest składnia uproszczona.</span><span class="sxs-lookup"><span data-stu-id="67227-107">The default syntax is the lightweight syntax.</span></span> <span data-ttu-id="67227-108">W tym temacie opisano składnię konstrukcji języka F #, gdy nie jest włączona składnia uproszczona.</span><span class="sxs-lookup"><span data-stu-id="67227-108">This topic describes the syntax for F# constructs when lightweight syntax is not enabled.</span></span> <span data-ttu-id="67227-109">Pełna składnia jest zawsze włączona, więc nawet w przypadku włączenia uproszczonej składni można nadal używać składni pełnej dla niektórych konstrukcji.</span><span class="sxs-lookup"><span data-stu-id="67227-109">Verbose syntax is always enabled, so even if you enable lightweight syntax, you can still use verbose syntax for some constructs.</span></span> <span data-ttu-id="67227-110">Można wyłączyć składnię uproszczoną za pomocą `#light "off"` dyrektywy.</span><span class="sxs-lookup"><span data-stu-id="67227-110">You can disable lightweight syntax by using the `#light "off"` directive.</span></span>

## <a name="table-of-constructs"></a><span data-ttu-id="67227-111">Tabela konstrukcji</span><span class="sxs-lookup"><span data-stu-id="67227-111">Table of Constructs</span></span>

<span data-ttu-id="67227-112">W poniższej tabeli przedstawiono składnię uproszczoną i pełną dla konstrukcji języka F # w kontekstach, w których istnieje różnica między dwoma formularzami.</span><span class="sxs-lookup"><span data-stu-id="67227-112">The following table shows the lightweight and verbose syntax for F# language constructs in contexts where there is a difference between the two forms.</span></span> <span data-ttu-id="67227-113">W tej tabeli, nawiasy kątowe ( &lt; &gt; ) otaczają elementy składni dostarczone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="67227-113">In this table, angle brackets (&lt;&gt;) enclose user-supplied syntax elements.</span></span> <span data-ttu-id="67227-114">Zapoznaj się z dokumentacją dla każdej konstrukcji języka, aby uzyskać bardziej szczegółowe informacje na temat składni używanej w ramach tych konstrukcji.</span><span class="sxs-lookup"><span data-stu-id="67227-114">Refer to the documentation for each language construct for more detailed information about the syntax used within these constructs.</span></span>

<table>
<tr>
<th><span data-ttu-id="67227-115">Konstrukcja języka</span><span class="sxs-lookup"><span data-stu-id="67227-115">Language construct</span></span></th>
<th><span data-ttu-id="67227-116">Składnia uproszczona</span><span class="sxs-lookup"><span data-stu-id="67227-116">Lightweight syntax</span></span></th>
<th><span data-ttu-id="67227-117">Verbose — składnia</span><span class="sxs-lookup"><span data-stu-id="67227-117">Verbose syntax</span></span></th>
</tr>
<tr>
<td>
<span data-ttu-id="67227-118">wyrażenia złożone</span><span class="sxs-lookup"><span data-stu-id="67227-118">compound expressions</span></span>
</td>
<td>

```fsharp
<expression1>
<expression2>
```

</td><td>

```fsharp
<expression1>; <expression2>
```

</td>
</tr>
<tr><td>

<span data-ttu-id="67227-119">`let`powiązania zagnieżdżone</span><span class="sxs-lookup"><span data-stu-id="67227-119">nested `let` bindings</span></span>

</td><td>

```fsharp
let f x =
    let a = 1
    let b = 2
    x + a + b
```

</td><td>

```fsharp
let f x =
    let a = 1 in
    let b = 2 in
    x + a + b
```

</td>
</tr>
<tr><td>
<span data-ttu-id="67227-120">blok kodu</span><span class="sxs-lookup"><span data-stu-id="67227-120">code block</span></span>
</td><td>

```fsharp
(
    <expression1>
    <expression2>
)
```

</td><td>

```fsharp
begin
    <expression1>;
    <expression2>;
end
```

</td>
</tr>
<tr><td>
`for...do`
</td><td>

```fsharp
for counter = start to finish do
    ...
```

</td><td>

```fsharp
for counter = start to finish do
    ...
done
```

</td>
</tr>
<tr><td>
`while...do`
</td><td>

```fsharp
while <condition> do
    ...
```

</td><td>

```fsharp
while <condition> do
    ...
done
```

</td>
</tr>
<tr><td>
`for...in`
</td><td>

```fsharp
for var in start .. finish do
    ...
```

</td><td>

```fsharp
for var in start .. finish do
    ...
done
```

</td>
</tr>
<tr><td>
`do`
</td><td>

```fsharp
do
    ...
```

</td><td>

```fsharp
do
    ...
in
```

</td>
</tr>
<tr><td><span data-ttu-id="67227-121">rejestrowanie</span><span class="sxs-lookup"><span data-stu-id="67227-121">record</span></span>
</td><td>

```fsharp
type <record-name> =
    {
        <field-declarations>
    }
    <value-or-member-definitions>
```

</td><td>

```fsharp
type <record-name> =
    {
        <field-declarations>
    }
    with
        <value-or-member-definitions>
    end
```

</td>
</tr>
<tr><td><span data-ttu-id="67227-122">class</span><span class="sxs-lookup"><span data-stu-id="67227-122">class</span></span>
</td><td>

```fsharp
type <class-name>(<params>) =
    ...
```

</td><td>

```fsharp
type <class-name>(<params>) =
    class
        ...
    end
```

</td>
</tr>
<tr><td><span data-ttu-id="67227-123">— struktura</span><span class="sxs-lookup"><span data-stu-id="67227-123">structure</span></span></td><td>

```fsharp
[<StructAttribute>]
type <structure-name> =
    ...
```

</td><td>

```fsharp
type <structure-name> =
    struct
        ...
    end
```

</td>
</tr>
<tr><td><span data-ttu-id="67227-124">Unia rozłączna</span><span class="sxs-lookup"><span data-stu-id="67227-124">discriminated union</span></span></td><td>

```fsharp
type <union-name> =
    | ...
    | ...
    ...
    <value-or-member definitions>
```

</td><td>

```fsharp
type <union-name> =
    | ...
    | ...
    ...
    with
        <value-or-member-definitions>
    end
```

</td>
</tr>
<tr><td><span data-ttu-id="67227-125">interface</span><span class="sxs-lookup"><span data-stu-id="67227-125">interface</span></span></td><td>

```fsharp
type <interface-name> =
    ...
```

</td><td>

```fsharp
type <interface-name> =
    interface
        ...
    end
```

</td>
</tr>
<tr><td><span data-ttu-id="67227-126">wyrażenie obiektu</span><span class="sxs-lookup"><span data-stu-id="67227-126">object expression</span></span></td><td>

```fsharp
{ new <type-name>
    with
        <value-or-member-definitions>
        <interface-implementations>
}
```

</td><td>

```fsharp
{ new <type-name>
    with
        <value-or-member-definitions>
    end
    <interface-implementations>
}
```

</td>
</tr>
<tr><td><span data-ttu-id="67227-127">implementacja interfejsu</span><span class="sxs-lookup"><span data-stu-id="67227-127">interface implementation</span></span></td><td>

```fsharp
interface <interface-name>
    with
        <value-or-member-definitions>
```

</td><td>

```fsharp
interface <interface-name>
    with
        <value-or-member-definitions>
    end
```

</td>
</tr>
<tr><td><span data-ttu-id="67227-128">rozszerzenie typu</span><span class="sxs-lookup"><span data-stu-id="67227-128">type extension</span></span></td><td>

```fsharp
type <type-name>
    with
        <value-or-member-definitions>
```

</td><td>

```fsharp
type <type-name>
    with
        <value-or-member-definitions>
    end
```

</td>
</tr>
<tr><td><span data-ttu-id="67227-129">moduł</span><span class="sxs-lookup"><span data-stu-id="67227-129">module</span></span></td><td>

```fsharp
module <module-name> =
    ...
```

</td><td>

```fsharp
module <module-name> =
    begin
        ...
    end
```

</td>
</tr>
</table>

## <a name="see-also"></a><span data-ttu-id="67227-130">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="67227-130">See also</span></span>

- [<span data-ttu-id="67227-131">Dokumentacja języka F #</span><span class="sxs-lookup"><span data-stu-id="67227-131">F# Language Reference</span></span>](index.md)
- [<span data-ttu-id="67227-132">Dyrektywy kompilatora</span><span class="sxs-lookup"><span data-stu-id="67227-132">Compiler Directives</span></span>](compiler-directives.md)
- [<span data-ttu-id="67227-133">Wskazówki dotyczące formatowania kodu</span><span class="sxs-lookup"><span data-stu-id="67227-133">Code Formatting Guidelines</span></span>](../style-guide/formatting.md)
