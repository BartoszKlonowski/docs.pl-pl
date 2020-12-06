---
title: 'Deklaracje importowania: open — Słowo kluczowe'
description: 'Dowiedz się więcej o deklaracjach importu F # i sposobach określania modułu lub przestrzeni nazw, których elementy można odwołać bez użycia w pełni kwalifikowanej nazwy.'
ms.date: 08/15/2020
ms.openlocfilehash: 4d3fd159aa4b334e9db0d7f756047470ad9c0829
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96739688"
---
# <a name="import-declarations-the-open-keyword"></a><span data-ttu-id="4d5cf-103">Deklaracje importu: `open` słowo kluczowe</span><span class="sxs-lookup"><span data-stu-id="4d5cf-103">Import declarations: The `open` keyword</span></span>

<span data-ttu-id="4d5cf-104">*Deklaracja importu* określa moduł lub przestrzeń nazw, których elementy można odwoływać bez używania w pełni kwalifikowanej nazwy.</span><span class="sxs-lookup"><span data-stu-id="4d5cf-104">An *import declaration* specifies a module or namespace whose elements you can reference without using a fully qualified name.</span></span>

## <a name="syntax"></a><span data-ttu-id="4d5cf-105">Składnia</span><span class="sxs-lookup"><span data-stu-id="4d5cf-105">Syntax</span></span>

```fsharp
open module-or-namespace-name
open type type-name
```

## <a name="remarks"></a><span data-ttu-id="4d5cf-106">Uwagi</span><span class="sxs-lookup"><span data-stu-id="4d5cf-106">Remarks</span></span>

<span data-ttu-id="4d5cf-107">Odwoływanie się do kodu przy użyciu w pełni kwalifikowanej przestrzeni nazw lub ścieżki modułu za każdym razem, gdy program może utworzyć kod, który jest trudno pisać, czytać i konserwować.</span><span class="sxs-lookup"><span data-stu-id="4d5cf-107">Referencing code by using the fully qualified namespace or module path every time can create code that is hard to write, read, and maintain.</span></span> <span data-ttu-id="4d5cf-108">Zamiast tego można użyć `open` słowa kluczowego dla często używanych modułów i przestrzeni nazw, aby podczas odwoływania się do elementu członkowskiego tego modułu lub przestrzeni nazw można użyć krótkiej formy nazwy zamiast w pełni kwalifikowanej nazwy.</span><span class="sxs-lookup"><span data-stu-id="4d5cf-108">Instead, you can use the `open` keyword for frequently used modules and namespaces so that when you reference a member of that module or namespace, you can use the short form of the name instead of the fully qualified name.</span></span> <span data-ttu-id="4d5cf-109">To słowo kluczowe jest podobne do `using` słowa kluczowego w języku C#, `using namespace` w Visual C++ i `Imports` w Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="4d5cf-109">This keyword is similar to the `using` keyword in C#, `using namespace` in Visual C++, and `Imports` in Visual Basic.</span></span>

<span data-ttu-id="4d5cf-110">Dostarczony moduł lub przestrzeń nazw muszą znajdować się w tym samym projekcie lub w przywoływanym projekcie lub zestawie.</span><span class="sxs-lookup"><span data-stu-id="4d5cf-110">The module or namespace provided must be in the same project or in a referenced project or assembly.</span></span> <span data-ttu-id="4d5cf-111">Jeśli tak nie jest, można dodać odwołanie do projektu lub użyć `-reference` opcji wiersza polecenia (lub jego skrótu `-r` ).</span><span class="sxs-lookup"><span data-stu-id="4d5cf-111">If it is not, you can add a reference to the project, or use the `-reference` command-line option (or its abbreviation, `-r`).</span></span> <span data-ttu-id="4d5cf-112">Aby uzyskać więcej informacji, zobacz [Opcje kompilatora](compiler-options.md).</span><span class="sxs-lookup"><span data-stu-id="4d5cf-112">For more information, see [Compiler Options](compiler-options.md).</span></span>

<span data-ttu-id="4d5cf-113">Deklaracja importu udostępnia nazwy dostępne w kodzie, który następuje po deklaracji, do końca otaczającej przestrzeni nazw, modułu lub pliku.</span><span class="sxs-lookup"><span data-stu-id="4d5cf-113">The import declaration makes the names available in the code that follows the declaration, up to the end of the enclosing namespace, module, or file.</span></span>

<span data-ttu-id="4d5cf-114">Jeśli używasz wielu deklaracji importu, powinny one pojawiać się w osobnych wierszach.</span><span class="sxs-lookup"><span data-stu-id="4d5cf-114">When you use multiple import declarations, they should appear on separate lines.</span></span>

<span data-ttu-id="4d5cf-115">Poniższy kod ilustruje użycie `open` słowa kluczowego w celu uproszczenia kodu.</span><span class="sxs-lookup"><span data-stu-id="4d5cf-115">The following code shows the use of the `open` keyword to simplify code.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6801.fs)]

<span data-ttu-id="4d5cf-116">Kompilator F # nie emituje błędu lub ostrzeżenia, gdy niejasności występuje, gdy ta sama nazwa wystąpi w więcej niż jednym otwartym module lub przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="4d5cf-116">The F# compiler does not emit an error or warning when ambiguities occur when the same name occurs in more than one open module or namespace.</span></span> <span data-ttu-id="4d5cf-117">Gdy wystąpi niejasności, język F # zapewnia preferencję dla ostatnio otwartego modułu lub przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="4d5cf-117">When ambiguities occur, F# gives preference to the more recently opened module or namespace.</span></span> <span data-ttu-id="4d5cf-118">Na przykład, w poniższym kodzie, oznacza, chociaż znajduje się `empty` `Seq.empty` `empty` zarówno w `List` module, jak i `Seq` .</span><span class="sxs-lookup"><span data-stu-id="4d5cf-118">For example, in the following code, `empty` means `Seq.empty`, even though `empty` is located in both the `List` and `Seq` modules.</span></span>

```fsharp
open List
open Seq
printfn %"{empty}"
```

<span data-ttu-id="4d5cf-119">W związku z tym należy zachować ostrożność podczas otwierania modułów lub przestrzeni nazw, takich jak `List` lub zawierających `Seq` składowe o identycznych nazwach. zamiast tego należy rozważyć użycie kwalifikowanych nazw.</span><span class="sxs-lookup"><span data-stu-id="4d5cf-119">Therefore, be careful when you open modules or namespaces such as `List` or `Seq` that contain members that have identical names; instead, consider using the qualified names.</span></span> <span data-ttu-id="4d5cf-120">Należy unikać każdej sytuacji, w której kod jest zależny od kolejności deklaracji importu.</span><span class="sxs-lookup"><span data-stu-id="4d5cf-120">You should avoid any situation in which the code is dependent upon the order of the import declarations.</span></span>

## <a name="open-type-declarations"></a><span data-ttu-id="4d5cf-121">Otwieranie deklaracji typu</span><span class="sxs-lookup"><span data-stu-id="4d5cf-121">Open type declarations</span></span>

<span data-ttu-id="4d5cf-122">Język F # obsługuje `open` Typ podobny do tego:</span><span class="sxs-lookup"><span data-stu-id="4d5cf-122">F# supports `open` on a type like so:</span></span>

```fsharp
open type System.Math
PI
```

<span data-ttu-id="4d5cf-123">Spowoduje to udostępnienie wszystkich dostępnych pól statycznych i elementów członkowskich w typie.</span><span class="sxs-lookup"><span data-stu-id="4d5cf-123">This will expose all accessible static fields and members on the type.</span></span>

<span data-ttu-id="4d5cf-124">Można również `open` określić typ [rekordu](records.md) i [Unii rozłącznych](discriminated-unions.md) , aby udostępnić statyczne elementy członkowskie.</span><span class="sxs-lookup"><span data-stu-id="4d5cf-124">You can also `open` F#-defined [record](records.md) and [discriminated union](discriminated-unions.md) types to expose static members.</span></span> <span data-ttu-id="4d5cf-125">W przypadku związków rozłącznych można również uwidocznić przypadki Unii.</span><span class="sxs-lookup"><span data-stu-id="4d5cf-125">In the case of discriminated unions, you can also expose the union cases.</span></span> <span data-ttu-id="4d5cf-126">Może to być przydatne w przypadku uzyskiwania dostępu do przypadków Unii w typie zadeklarowanym wewnątrz modułu, który może nie być otwarty, tak więc:</span><span class="sxs-lookup"><span data-stu-id="4d5cf-126">This can be helpful for accessing union cases in a type declared inside of a module that you may not want to open, like so:</span></span>

```fsharp
module M =
    type DU = A | B | C

    let someOtherFunction x = x + 1

// Open only the type inside the module
open type M.DU

printfn "%A" A
```

## <a name="namespaces-that-are-open-by-default"></a><span data-ttu-id="4d5cf-127">Obszary nazw, które są domyślnie otwarte</span><span class="sxs-lookup"><span data-stu-id="4d5cf-127">Namespaces That Are Open by Default</span></span>

<span data-ttu-id="4d5cf-128">Niektóre przestrzenie nazw są często używane w kodzie języka F #, które są otwierane niejawnie bez potrzeby jawnej deklaracji importu.</span><span class="sxs-lookup"><span data-stu-id="4d5cf-128">Some namespaces are so frequently used in F# code that they are opened implicitly without the need of an explicit import declaration.</span></span> <span data-ttu-id="4d5cf-129">W poniższej tabeli przedstawiono obszary nazw, które są domyślnie otwarte.</span><span class="sxs-lookup"><span data-stu-id="4d5cf-129">The following table shows the namespaces that are open by default.</span></span>

|<span data-ttu-id="4d5cf-130">Przestrzeń nazw</span><span class="sxs-lookup"><span data-stu-id="4d5cf-130">Namespace</span></span>|<span data-ttu-id="4d5cf-131">Opis</span><span class="sxs-lookup"><span data-stu-id="4d5cf-131">Description</span></span>|
|---------|-----------|
|`FSharp.Core`|<span data-ttu-id="4d5cf-132">Zawiera podstawowe definicje typu języka F # dla typów wbudowanych, takich jak `int` i `float` .</span><span class="sxs-lookup"><span data-stu-id="4d5cf-132">Contains basic F# type definitions for built-in types such as `int` and `float`.</span></span>|
|`FSharp.Core.Operators`|<span data-ttu-id="4d5cf-133">Zawiera podstawowe operacje arytmetyczne, takie jak `+` i `*` .</span><span class="sxs-lookup"><span data-stu-id="4d5cf-133">Contains basic arithmetic operations such as `+` and `*`.</span></span>|
|`FSharp.Collections`|<span data-ttu-id="4d5cf-134">Zawiera niezmienne klasy kolekcji, takie jak `List` i `Array` .</span><span class="sxs-lookup"><span data-stu-id="4d5cf-134">Contains immutable collection classes such as `List` and `Array`.</span></span>|
|`FSharp.Control`|<span data-ttu-id="4d5cf-135">Zawiera typy dla konstrukcji kontroli, takich jak Ocena z opóźnieniem i asynchroniczne przepływy pracy.</span><span class="sxs-lookup"><span data-stu-id="4d5cf-135">Contains types for control constructs such as lazy evaluation and asynchronous workflows.</span></span>|
|`FSharp.Text`|<span data-ttu-id="4d5cf-136">Zawiera funkcje dla sformatowanych operacji we/wy, takich jak `printf` Funkcja.</span><span class="sxs-lookup"><span data-stu-id="4d5cf-136">Contains functions for formatted IO, such as the `printf` function.</span></span>|

## <a name="autoopen-attribute"></a><span data-ttu-id="4d5cf-137">AutoOpen — atrybut</span><span class="sxs-lookup"><span data-stu-id="4d5cf-137">AutoOpen Attribute</span></span>

<span data-ttu-id="4d5cf-138">Można zastosować `AutoOpen` atrybut do zestawu, jeśli chcesz automatycznie otworzyć przestrzeń nazw lub moduł, gdy odwołanie do zestawu.</span><span class="sxs-lookup"><span data-stu-id="4d5cf-138">You can apply the `AutoOpen` attribute to an assembly if you want to automatically open a namespace or module when the assembly is referenced.</span></span> <span data-ttu-id="4d5cf-139">Można również zastosować `AutoOpen` atrybut do modułu, aby automatycznie otworzyć ten moduł po otwarciu modułu nadrzędnego lub przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="4d5cf-139">You can also apply the `AutoOpen` attribute to a module to automatically open that module when the parent module or namespace is opened.</span></span> <span data-ttu-id="4d5cf-140">Aby uzyskać więcej informacji, zobacz [AutoOpenAttribute](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-autoopenattribute.html).</span><span class="sxs-lookup"><span data-stu-id="4d5cf-140">For more information, see [AutoOpenAttribute](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-autoopenattribute.html).</span></span>

## <a name="requirequalifiedaccess-attribute"></a><span data-ttu-id="4d5cf-141">RequireQualifiedAccess — atrybut</span><span class="sxs-lookup"><span data-stu-id="4d5cf-141">RequireQualifiedAccess Attribute</span></span>

<span data-ttu-id="4d5cf-142">Niektóre moduły, rekordy lub typy Unii mogą określać `RequireQualifiedAccess` atrybut.</span><span class="sxs-lookup"><span data-stu-id="4d5cf-142">Some modules, records, or union types may specify the `RequireQualifiedAccess` attribute.</span></span> <span data-ttu-id="4d5cf-143">Gdy odwołujesz się do elementów tych modułów, rekordów lub Unii, musisz użyć kwalifikowanej nazwy bez względu na to, czy dołączysz deklarację importu.</span><span class="sxs-lookup"><span data-stu-id="4d5cf-143">When you reference elements of those modules, records, or unions, you must use a qualified name regardless of whether you include an import declaration.</span></span> <span data-ttu-id="4d5cf-144">Jeśli ten atrybut jest używany strategicznie dla typów, które definiują często używane nazwy, można uniknąć kolizji nazw, a tym samym zwiększyć odporność kodu na zmiany w bibliotekach.</span><span class="sxs-lookup"><span data-stu-id="4d5cf-144">If you use this attribute strategically on types that define commonly used names, you help avoid name collisions and thereby make code more resilient to changes in libraries.</span></span> <span data-ttu-id="4d5cf-145">Aby uzyskać więcej informacji, zobacz [RequireQualifiedAccessAttribute —](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-requirequalifiedaccessattribute.html).</span><span class="sxs-lookup"><span data-stu-id="4d5cf-145">For more information, see [RequireQualifiedAccessAttribute](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-requirequalifiedaccessattribute.html).</span></span>

## <a name="see-also"></a><span data-ttu-id="4d5cf-146">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="4d5cf-146">See also</span></span>

- [<span data-ttu-id="4d5cf-147">Dokumentacja języka F #</span><span class="sxs-lookup"><span data-stu-id="4d5cf-147">F# Language Reference</span></span>](index.md)
- [<span data-ttu-id="4d5cf-148">Przestrzenie nazw</span><span class="sxs-lookup"><span data-stu-id="4d5cf-148">Namespaces</span></span>](namespaces.md)
- [<span data-ttu-id="4d5cf-149">Moduły</span><span class="sxs-lookup"><span data-stu-id="4d5cf-149">Modules</span></span>](modules.md)
