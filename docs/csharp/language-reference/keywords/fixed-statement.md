---
description: FIXED — odwołanie do języka C#
title: FIXED — odwołanie do języka C#
ms.date: 05/10/2018
f1_keywords:
- fixed_CSharpKeyword
- fixed
helpviewer_keywords:
- fixed keyword [C#]
ms.openlocfilehash: 05505916ab3837d2c433ec420d7928a8ee883fa8
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/30/2020
ms.locfileid: "89139726"
---
# <a name="fixed-statement-c-reference"></a><span data-ttu-id="7f5c3-103">fixed — Instrukcja (odwołanie w C#)</span><span class="sxs-lookup"><span data-stu-id="7f5c3-103">fixed Statement (C# Reference)</span></span>

<span data-ttu-id="7f5c3-104">`fixed`Instrukcja zapobiega ponownemu lokalizowaniu ruchomej zmiennej przez moduł wyrzucania elementów bezużytecznych.</span><span class="sxs-lookup"><span data-stu-id="7f5c3-104">The `fixed` statement prevents the garbage collector from relocating a movable variable.</span></span> <span data-ttu-id="7f5c3-105">`fixed`Instrukcja jest dozwolona tylko w [niebezpiecznym](unsafe.md) kontekście.</span><span class="sxs-lookup"><span data-stu-id="7f5c3-105">The `fixed` statement is only permitted in an [unsafe](unsafe.md) context.</span></span> <span data-ttu-id="7f5c3-106">Możesz również użyć `fixed` słowa kluczowego, aby utworzyć [bufory o ustalonym rozmiarze](../../programming-guide/unsafe-code-pointers/fixed-size-buffers.md).</span><span class="sxs-lookup"><span data-stu-id="7f5c3-106">You can also use the `fixed` keyword to create [fixed size buffers](../../programming-guide/unsafe-code-pointers/fixed-size-buffers.md).</span></span>

<span data-ttu-id="7f5c3-107">`fixed`Instrukcja ustawia wskaźnik na zmienną zarządzaną i "pinezki", która jest zmienna podczas wykonywania instrukcji.</span><span class="sxs-lookup"><span data-stu-id="7f5c3-107">The `fixed` statement sets a pointer to a managed variable and "pins" that variable during the execution of the statement.</span></span> <span data-ttu-id="7f5c3-108">Wskaźniki do ruchomych zmiennych zarządzanych są przydatne tylko w `fixed` kontekście.</span><span class="sxs-lookup"><span data-stu-id="7f5c3-108">Pointers to movable managed variables are useful only in a `fixed` context.</span></span> <span data-ttu-id="7f5c3-109">Bez `fixed` kontekstu, wyrzucanie elementów bezużytecznych może przewidzieć nieprzewidywalne zmienne.</span><span class="sxs-lookup"><span data-stu-id="7f5c3-109">Without a `fixed` context, garbage collection could relocate the variables unpredictably.</span></span> <span data-ttu-id="7f5c3-110">Kompilator języka C# umożliwia przypisanie wskaźnika do zmiennej zarządzanej w `fixed` instrukcji.</span><span class="sxs-lookup"><span data-stu-id="7f5c3-110">The C# compiler only lets you assign a pointer to a managed variable in a `fixed` statement.</span></span>

[!code-csharp[Accessing fixed memory](snippets/FixedKeywordExamples.cs#1)]

<span data-ttu-id="7f5c3-111">Wskaźnik można zainicjować za pomocą tablicy, ciągu, buforu o ustalonym rozmiarze lub adresu zmiennej.</span><span class="sxs-lookup"><span data-stu-id="7f5c3-111">You can initialize a pointer by using an array, a string, a fixed-size buffer, or the address of a variable.</span></span> <span data-ttu-id="7f5c3-112">Poniższy przykład ilustruje użycie adresów zmiennych, tablic i ciągów:</span><span class="sxs-lookup"><span data-stu-id="7f5c3-112">The following example illustrates the use of variable addresses, arrays, and strings:</span></span>

[!code-csharp[Initializing fixed size buffers](snippets/FixedKeywordExamples.cs#2)]

<span data-ttu-id="7f5c3-113">Począwszy od języka C# 7,3, `fixed` instrukcja działa na dodatkowych typach poza tablicami, ciągami, buforami o ustalonym rozmiarze lub zmiennymi niezarządzanymi.</span><span class="sxs-lookup"><span data-stu-id="7f5c3-113">Starting with C# 7.3, the `fixed` statement operates on additional types beyond arrays, strings, fixed size buffers, or unmanaged variables.</span></span> <span data-ttu-id="7f5c3-114">Każdy typ, który implementuje metodę o nazwie, `GetPinnableReference` może być przypięty.</span><span class="sxs-lookup"><span data-stu-id="7f5c3-114">Any type that implements a method named `GetPinnableReference` can be pinned.</span></span> <span data-ttu-id="7f5c3-115">`GetPinnableReference`Musi zwracać `ref` zmienną [typu niezarządzanego](../builtin-types/unmanaged-types.md).</span><span class="sxs-lookup"><span data-stu-id="7f5c3-115">The `GetPinnableReference` must return a `ref` variable of an [unmanaged type](../builtin-types/unmanaged-types.md).</span></span> <span data-ttu-id="7f5c3-116">Typy .NET <xref:System.Span%601?displayProperty=nameWithType> i <xref:System.ReadOnlySpan%601?displayProperty=nameWithType> wprowadzone w środowisku .net Core 2,0 używają tego wzorca i mogą być przypięte.</span><span class="sxs-lookup"><span data-stu-id="7f5c3-116">The .NET types <xref:System.Span%601?displayProperty=nameWithType> and <xref:System.ReadOnlySpan%601?displayProperty=nameWithType> introduced in .NET Core 2.0 make use of this pattern and can be pinned.</span></span> <span data-ttu-id="7f5c3-117">Pokazano to w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="7f5c3-117">This is shown in the following example:</span></span>

[!code-csharp[Accessing fixed memory](snippets/FixedKeywordExamples.cs#FixedSpan)]

<span data-ttu-id="7f5c3-118">Jeśli tworzysz typy, które powinny wchodzić w skład tego wzorca, zobacz, aby zapoznać się <xref:System.Span%601.GetPinnableReference?displayProperty=nameWithType> z przykładem implementacji wzorca.</span><span class="sxs-lookup"><span data-stu-id="7f5c3-118">If you are creating types that should participate in this pattern, see <xref:System.Span%601.GetPinnableReference?displayProperty=nameWithType> for an example of implementing the pattern.</span></span>

<span data-ttu-id="7f5c3-119">W jednej instrukcji można zainicjować wiele wskaźników, jeśli są one tego samego typu:</span><span class="sxs-lookup"><span data-stu-id="7f5c3-119">Multiple pointers can be initialized in one statement if they are all the same type:</span></span>

```csharp
fixed (byte* ps = srcarray, pd = dstarray) {...}
```

<span data-ttu-id="7f5c3-120">Aby zainicjować wskaźniki różnych typów, należy po prostu zagnieżdżać `fixed` instrukcje, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="7f5c3-120">To initialize pointers of different types, simply nest `fixed` statements, as shown in the following example.</span></span>

[!code-csharp[Initializing multiple pointers](snippets/FixedKeywordExamples.cs#3)]

<span data-ttu-id="7f5c3-121">Po wykonaniu kodu w instrukcji wszystkie przypięte zmienne są odpięte i podlegają wyrzucaniu elementów bezużytecznych.</span><span class="sxs-lookup"><span data-stu-id="7f5c3-121">After the code in the statement is executed, any pinned variables are unpinned and subject to garbage collection.</span></span> <span data-ttu-id="7f5c3-122">W związku z tym nie należy wskazywać na te zmienne poza `fixed` instrukcją.</span><span class="sxs-lookup"><span data-stu-id="7f5c3-122">Therefore, do not point to those variables outside the `fixed` statement.</span></span> <span data-ttu-id="7f5c3-123">Zmienne zadeklarowane w `fixed` instrukcji należą do zakresu tej instrukcji, ułatwiając to:</span><span class="sxs-lookup"><span data-stu-id="7f5c3-123">The variables declared in the `fixed` statement are scoped to that statement, making this easier:</span></span>

```csharp
fixed (byte* ps = srcarray, pd = dstarray)
{
   ...
}
// ps and pd are no longer in scope here.
```

<span data-ttu-id="7f5c3-124">Wskaźniki inicjowane w `fixed` instrukcjach są zmiennymi tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="7f5c3-124">Pointers initialized in `fixed` statements are readonly variables.</span></span> <span data-ttu-id="7f5c3-125">Jeśli chcesz zmodyfikować wartość wskaźnika, należy zadeklarować drugą zmienną wskaźnika i zmodyfikować ją.</span><span class="sxs-lookup"><span data-stu-id="7f5c3-125">If you want to modify the pointer value, you must declare a second pointer variable, and modify that.</span></span> <span data-ttu-id="7f5c3-126">Nie można zmodyfikować zmiennej zadeklarowanej w `fixed` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="7f5c3-126">The variable declared in the `fixed` statement cannot be modified:</span></span>

```csharp
fixed (byte* ps = srcarray, pd = dstarray)
{
    byte* pSourceCopy = ps;
    pSourceCopy++; // point to the next element.
    ps++; // invalid: cannot modify ps, as it is declared in the fixed statement.
}
```

<span data-ttu-id="7f5c3-127">Możesz przydzielić pamięć na stosie, gdzie nie podlega wyrzucaniu elementów bezużytecznych i dlatego nie musi być przypięty.</span><span class="sxs-lookup"><span data-stu-id="7f5c3-127">You can allocate memory on the stack, where it is not subject to garbage collection and therefore does not need to be pinned.</span></span> <span data-ttu-id="7f5c3-128">Aby to zrobić, użyj [ `stackalloc` wyrażenia](../operators/stackalloc.md).</span><span class="sxs-lookup"><span data-stu-id="7f5c3-128">To do that, use a [`stackalloc` expression](../operators/stackalloc.md).</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="7f5c3-129">specyfikacja języka C#</span><span class="sxs-lookup"><span data-stu-id="7f5c3-129">C# language specification</span></span>

<span data-ttu-id="7f5c3-130">Aby uzyskać więcej informacji, zobacz sekcję [FIXED Statement](~/_csharplang/spec/unsafe-code.md#the-fixed-statement) w [specyfikacji języka C#](~/_csharplang/spec/introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7f5c3-130">For more information, see [The fixed statement](~/_csharplang/spec/unsafe-code.md#the-fixed-statement) section of the [C# language specification](~/_csharplang/spec/introduction.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="7f5c3-131">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="7f5c3-131">See also</span></span>

- [<span data-ttu-id="7f5c3-132">Odwołanie w C#</span><span class="sxs-lookup"><span data-stu-id="7f5c3-132">C# Reference</span></span>](../index.md)
- [<span data-ttu-id="7f5c3-133">Przewodnik programowania w języku C#</span><span class="sxs-lookup"><span data-stu-id="7f5c3-133">C# Programming Guide</span></span>](../../programming-guide/index.md)
- [<span data-ttu-id="7f5c3-134">Słowa kluczowe języka C#</span><span class="sxs-lookup"><span data-stu-id="7f5c3-134">C# Keywords</span></span>](index.md)
- [<span data-ttu-id="7f5c3-135">niebezpieczne</span><span class="sxs-lookup"><span data-stu-id="7f5c3-135">unsafe</span></span>](unsafe.md)
- [<span data-ttu-id="7f5c3-136">Typy wskaźnika</span><span class="sxs-lookup"><span data-stu-id="7f5c3-136">Pointer types</span></span>](../../programming-guide/unsafe-code-pointers/pointer-types.md)
- [<span data-ttu-id="7f5c3-137">Bufory o ustalonym rozmiarze</span><span class="sxs-lookup"><span data-stu-id="7f5c3-137">Fixed Size Buffers</span></span>](../../programming-guide/unsafe-code-pointers/fixed-size-buffers.md)
