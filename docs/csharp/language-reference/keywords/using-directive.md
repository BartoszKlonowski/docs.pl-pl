---
description: Using — odwołanie w C#
title: Using — odwołanie w C#
ms.date: 07/20/2015
f1_keywords:
- using_CSharpKeyword
helpviewer_keywords:
- using directive [C#]
ms.assetid: b42b8e61-5e7e-439c-bb71-370094b44ae8
ms.openlocfilehash: 77d9c894dae9adc24343ce3a639a4afb904fb0a1
ms.sourcegitcommit: 9d525bb8109216ca1dc9e39c149d4902f4b43da5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2020
ms.locfileid: "96599412"
---
# <a name="using-directive-c-reference"></a><span data-ttu-id="c3583-103">Using — dyrektywa (odwołanie w C#)</span><span class="sxs-lookup"><span data-stu-id="c3583-103">using directive (C# Reference)</span></span>

<span data-ttu-id="c3583-104">`using`Dyrektywa ma trzy zastosowania:</span><span class="sxs-lookup"><span data-stu-id="c3583-104">The `using` directive has three uses:</span></span>

- <span data-ttu-id="c3583-105">Aby zezwolić na używanie typów w przestrzeni nazw, aby nie trzeba było kwalifikować użycia typu w tej przestrzeni nazw:</span><span class="sxs-lookup"><span data-stu-id="c3583-105">To allow the use of types in a namespace so that you do not have to qualify the use of a type in that namespace:</span></span>

    ```csharp
    using System.Text;
    ```

- <span data-ttu-id="c3583-106">Aby umożliwić dostęp do statycznych elementów członkowskich i typów zagnieżdżonych typu bez konieczności kwalifikowania dostępu przy użyciu nazwy typu.</span><span class="sxs-lookup"><span data-stu-id="c3583-106">To allow you to access static members and nested types of a type without having to qualify the access with the type name.</span></span>

    ```csharp
    using static System.Math;
    ```

    <span data-ttu-id="c3583-107">Aby uzyskać więcej informacji, zobacz [Using static dyrektywą](using-static.md).</span><span class="sxs-lookup"><span data-stu-id="c3583-107">For more information, see the [using static directive](using-static.md).</span></span>

- <span data-ttu-id="c3583-108">Aby utworzyć alias dla przestrzeni nazw lub typu.</span><span class="sxs-lookup"><span data-stu-id="c3583-108">To create an alias for a namespace or a type.</span></span> <span data-ttu-id="c3583-109">Ta nazwa jest nazywana *dyrektywą aliasu using*.</span><span class="sxs-lookup"><span data-stu-id="c3583-109">This is called a *using alias directive*.</span></span>

    ```csharp
    using Project = PC.MyCompany.Project;
    ```

<span data-ttu-id="c3583-110">`using`Słowo kluczowe jest również używane do tworzenia *instrukcji using*, które pomagają zagwarantować, że <xref:System.IDisposable> obiekty takie jak pliki i czcionki są obsługiwane poprawnie.</span><span class="sxs-lookup"><span data-stu-id="c3583-110">The `using` keyword is also used to create *using statements*, which help ensure that <xref:System.IDisposable> objects such as files and fonts are handled correctly.</span></span> <span data-ttu-id="c3583-111">Aby uzyskać więcej informacji, zobacz [używanie instrukcji using](using-statement.md) .</span><span class="sxs-lookup"><span data-stu-id="c3583-111">See [using Statement](using-statement.md) for more information.</span></span>

## <a name="using-static-type"></a><span data-ttu-id="c3583-112">Używanie typu statycznego</span><span class="sxs-lookup"><span data-stu-id="c3583-112">Using static type</span></span>

<span data-ttu-id="c3583-113">Można uzyskać dostęp do statycznych elementów członkowskich typu bez konieczności kwalifikowania dostępu przy użyciu nazwy typu:</span><span class="sxs-lookup"><span data-stu-id="c3583-113">You can access static members of a type without having to qualify the access with the type name:</span></span>

```csharp
using static System.Console;
using static System.Math;
class Program
{
    static void Main()
    {
        WriteLine(Sqrt(3*3 + 4*4));
    }
}
```

## <a name="remarks"></a><span data-ttu-id="c3583-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="c3583-114">Remarks</span></span>

<span data-ttu-id="c3583-115">Zakres `using` dyrektywy jest ograniczony do pliku, w którym występuje.</span><span class="sxs-lookup"><span data-stu-id="c3583-115">The scope of a `using` directive is limited to the file in which it appears.</span></span>

<span data-ttu-id="c3583-116">`using`Może pojawić się dyrektywa:</span><span class="sxs-lookup"><span data-stu-id="c3583-116">The `using` directive can appear:</span></span>

- <span data-ttu-id="c3583-117">Na początku pliku kodu źródłowego przed dowolnymi obszarami nazw lub definicjami typów.</span><span class="sxs-lookup"><span data-stu-id="c3583-117">At the beginning of a source code file, before any namespace or type definitions.</span></span>
- <span data-ttu-id="c3583-118">W dowolnej przestrzeni nazw, ale przed wszelkimi obszarami nazw lub typami zadeklarowanymi w tej przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="c3583-118">In any namespace, but before any namespace or types declared in this namespace.</span></span>

<span data-ttu-id="c3583-119">W przeciwnym razie zostanie wygenerowany błąd kompilatora [CS1529](../../misc/cs1529.md) .</span><span class="sxs-lookup"><span data-stu-id="c3583-119">Otherwise, compiler error [CS1529](../../misc/cs1529.md) is generated.</span></span>

<span data-ttu-id="c3583-120">Utwórz `using` dyrektywę aliasu, aby ułatwić kwalifikowanie identyfikatora do przestrzeni nazw lub typu.</span><span class="sxs-lookup"><span data-stu-id="c3583-120">Create a `using` alias directive to make it easier to qualify an identifier to a namespace or type.</span></span> <span data-ttu-id="c3583-121">W dowolnej `using` dyrektywie w pełni kwalifikowana przestrzeń nazw lub typ muszą być używane niezależnie od `using` dyrektyw, które przed nim pochodzą.</span><span class="sxs-lookup"><span data-stu-id="c3583-121">In any `using` directive, the fully-qualified namespace or type must be used regardless of the `using` directives that come before it.</span></span> <span data-ttu-id="c3583-122">Nie `using` można użyć aliasu w deklaracji `using` dyrektywy.</span><span class="sxs-lookup"><span data-stu-id="c3583-122">No `using` alias can be used in the declaration of a `using` directive.</span></span> <span data-ttu-id="c3583-123">Na przykład poniższy kod generuje błąd kompilatora:</span><span class="sxs-lookup"><span data-stu-id="c3583-123">For example, the following generates a compiler error:</span></span>

```csharp
using s = System.Text;
using s.RegularExpressions; // Generates a compiler error.
```

<span data-ttu-id="c3583-124">Utwórz `using` dyrektywę, aby użyć typów w przestrzeni nazw bez konieczności określania przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="c3583-124">Create a `using` directive to use the types in a namespace without having to specify the namespace.</span></span> <span data-ttu-id="c3583-125">`using`Dyrektywa nie daje dostępu do żadnych przestrzeni nazw, które są zagnieżdżone w określonym obszarze nazw.</span><span class="sxs-lookup"><span data-stu-id="c3583-125">A `using` directive does not give you access to any namespaces that are nested in the namespace you specify.</span></span>

<span data-ttu-id="c3583-126">Przestrzenie nazw są dostępne w dwóch kategoriach: zdefiniowane przez użytkownika i zdefiniowane przez system.</span><span class="sxs-lookup"><span data-stu-id="c3583-126">Namespaces come in two categories: user-defined and system-defined.</span></span> <span data-ttu-id="c3583-127">Przestrzenie nazw zdefiniowane przez użytkownika to przestrzenie nazw zdefiniowane w kodzie.</span><span class="sxs-lookup"><span data-stu-id="c3583-127">User-defined namespaces are namespaces defined in your code.</span></span> <span data-ttu-id="c3583-128">Aby uzyskać listę przestrzeni nazw zdefiniowanych przez system, zobacz [.NET API Browser](../../../../api/index.md).</span><span class="sxs-lookup"><span data-stu-id="c3583-128">For a list of the system-defined namespaces, see [.NET API Browser](../../../../api/index.md).</span></span>

## <a name="example-1"></a><span data-ttu-id="c3583-129">Przykład 1</span><span class="sxs-lookup"><span data-stu-id="c3583-129">Example 1</span></span>

<span data-ttu-id="c3583-130">Poniższy przykład pokazuje, jak zdefiniować `using` alias dla przestrzeni nazw i używać go:</span><span class="sxs-lookup"><span data-stu-id="c3583-130">The following example shows how to define and use a `using` alias for a namespace:</span></span>

[!code-csharp[csrefKeywordsNamespace#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsNamespace/CS/csrefKeywordsNamespace2.cs#8)]

<span data-ttu-id="c3583-131">Dyrektywa using alias nie może mieć otwartego typu ogólnego po prawej stronie.</span><span class="sxs-lookup"><span data-stu-id="c3583-131">A using alias directive cannot have an open generic type on the right hand side.</span></span> <span data-ttu-id="c3583-132">Na przykład nie można utworzyć aliasu using dla elementu `List<T>` , ale można go utworzyć dla elementu `List<int>` .</span><span class="sxs-lookup"><span data-stu-id="c3583-132">For example, you cannot create a using alias for a `List<T>`, but you can create one for a `List<int>`.</span></span>

## <a name="example-2"></a><span data-ttu-id="c3583-133">Przykład 2</span><span class="sxs-lookup"><span data-stu-id="c3583-133">Example 2</span></span>

<span data-ttu-id="c3583-134">Poniższy przykład pokazuje, jak zdefiniować `using` dyrektywę i `using` alias dla klasy:</span><span class="sxs-lookup"><span data-stu-id="c3583-134">The following example shows how to define a `using` directive and a `using` alias for a class:</span></span>

[!code-csharp[csrefKeywordsNamespace#9](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsNamespace/CS/csrefKeywordsNamespace2.cs#9)]

## <a name="c-language-specification"></a><span data-ttu-id="c3583-135">specyfikacja języka C#</span><span class="sxs-lookup"><span data-stu-id="c3583-135">C# language specification</span></span>

<span data-ttu-id="c3583-136">Aby uzyskać więcej informacji, zobacz [using dyrektywy](~/_csharplang/spec/namespaces.md#using-directives) w [specyfikacji języka C#](/dotnet/csharp/language-reference/language-specification/introduction).</span><span class="sxs-lookup"><span data-stu-id="c3583-136">For more information, see [Using directives](~/_csharplang/spec/namespaces.md#using-directives) in the [C# Language Specification](/dotnet/csharp/language-reference/language-specification/introduction).</span></span> <span data-ttu-id="c3583-137">Specyfikacja języka jest ostatecznym źródłem informacji o składni i użyciu języka C#.</span><span class="sxs-lookup"><span data-stu-id="c3583-137">The language specification is the definitive source for C# syntax and usage.</span></span>

## <a name="see-also"></a><span data-ttu-id="c3583-138">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="c3583-138">See also</span></span>

- [<span data-ttu-id="c3583-139">Odwołanie w C#</span><span class="sxs-lookup"><span data-stu-id="c3583-139">C# Reference</span></span>](../index.md)
- [<span data-ttu-id="c3583-140">Przewodnik programowania w języku C#</span><span class="sxs-lookup"><span data-stu-id="c3583-140">C# Programming Guide</span></span>](../../programming-guide/index.md)
- [<span data-ttu-id="c3583-141">Używanie przestrzeni nazw</span><span class="sxs-lookup"><span data-stu-id="c3583-141">Using Namespaces</span></span>](../../programming-guide/namespaces/using-namespaces.md)
- [<span data-ttu-id="c3583-142">Słowa kluczowe języka C#</span><span class="sxs-lookup"><span data-stu-id="c3583-142">C# Keywords</span></span>](index.md)
- [<span data-ttu-id="c3583-143">Przestrzenie nazw</span><span class="sxs-lookup"><span data-stu-id="c3583-143">Namespaces</span></span>](../../programming-guide/namespaces/index.md)
- [<span data-ttu-id="c3583-144">using, instrukcja</span><span class="sxs-lookup"><span data-stu-id="c3583-144">using Statement</span></span>](using-statement.md)
