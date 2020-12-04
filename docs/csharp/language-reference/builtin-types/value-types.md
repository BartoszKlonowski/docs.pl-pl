---
description: 'Dowiedz się więcej na temat typów wartości, ich rodzajów i wbudowanych w języku C #'
title: Typy wartości — odwołanie w C#
ms.date: 01/22/2020
f1_keywords:
- cs.valuetypes
helpviewer_keywords:
- value types [C#]
- types [C#], value types
- C# language, value types
ms.assetid: 471eb994-2958-49d5-a6be-19b4313f80a3
ms.openlocfilehash: 64c9e9eba2495531cfef8a603d53fb21c95c87a4
ms.sourcegitcommit: 9d525bb8109216ca1dc9e39c149d4902f4b43da5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2020
ms.locfileid: "96599398"
---
# <a name="value-types-c-reference"></a><span data-ttu-id="c2c7d-103">Typy wartości (odwołanie w C#)</span><span class="sxs-lookup"><span data-stu-id="c2c7d-103">Value types (C# reference)</span></span>

<span data-ttu-id="c2c7d-104">*Typy wartości* i [typy referencyjne](../keywords/reference-types.md) to dwie główne kategorie typów języka C#.</span><span class="sxs-lookup"><span data-stu-id="c2c7d-104">*Value types* and [reference types](../keywords/reference-types.md) are the two main categories of C# types.</span></span> <span data-ttu-id="c2c7d-105">Zmienna typu wartości zawiera wystąpienie typu.</span><span class="sxs-lookup"><span data-stu-id="c2c7d-105">A variable of a value type contains an instance of the type.</span></span> <span data-ttu-id="c2c7d-106">Różni się to od zmiennej typu referencyjnego, która zawiera odwołanie do wystąpienia typu.</span><span class="sxs-lookup"><span data-stu-id="c2c7d-106">This differs from a variable of a reference type, which contains a reference to an instance of the type.</span></span> <span data-ttu-id="c2c7d-107">Domyślnie przy [przypisywaniu](../operators/assignment-operator.md)przekazywanie argumentu do metody i zwracanie wyniku metody powoduje skopiowanie wartości zmiennych.</span><span class="sxs-lookup"><span data-stu-id="c2c7d-107">By default, on [assignment](../operators/assignment-operator.md), passing an argument to a method, and returning a method result, variable values are copied.</span></span> <span data-ttu-id="c2c7d-108">W przypadku zmiennych typu wartość są kopiowane odpowiednie wystąpienia typu.</span><span class="sxs-lookup"><span data-stu-id="c2c7d-108">In the case of value-type variables, the corresponding type instances are copied.</span></span> <span data-ttu-id="c2c7d-109">Poniższy przykład ilustruje takie zachowanie:</span><span class="sxs-lookup"><span data-stu-id="c2c7d-109">The following example demonstrates that behavior:</span></span>

[!code-csharp[copy of values](snippets/shared/ValueTypes.cs#ValueTypeCopied)]

<span data-ttu-id="c2c7d-110">Jak pokazano w powyższym przykładzie, operacje na zmiennej typu wartości wpływają tylko na to wystąpienie typu wartości przechowywane w zmiennej.</span><span class="sxs-lookup"><span data-stu-id="c2c7d-110">As the preceding example shows, operations on a value-type variable affect only that instance of the value type, stored in the variable.</span></span>

<span data-ttu-id="c2c7d-111">Jeśli typ wartości zawiera element członkowski danych typu referencyjnego, podczas kopiowania wystąpienia typu wartości jest kopiowane tylko odwołanie do wystąpienia typu referencyjnego.</span><span class="sxs-lookup"><span data-stu-id="c2c7d-111">If a value type contains a data member of a reference type, only the reference to the instance of the reference type is copied when a value-type instance is copied.</span></span> <span data-ttu-id="c2c7d-112">Zarówno kopia, jak i oryginalne wystąpienie typu wartości mają dostęp do tego samego wystąpienia typu odwołania.</span><span class="sxs-lookup"><span data-stu-id="c2c7d-112">Both the copy and original value-type instance have access to the same reference-type instance.</span></span> <span data-ttu-id="c2c7d-113">Poniższy przykład ilustruje takie zachowanie:</span><span class="sxs-lookup"><span data-stu-id="c2c7d-113">The following example demonstrates that behavior:</span></span>

[!code-csharp[shallow copy](snippets/shared/ValueTypes.cs#ShallowCopy)]

> [!NOTE]
> <span data-ttu-id="c2c7d-114">Aby kod był mniej podatny na błędy i bardziej niezawodny, definiować i korzystać z niezmiennego typu wartości.</span><span class="sxs-lookup"><span data-stu-id="c2c7d-114">To make your code less error-prone and more robust, define and use immutable value types.</span></span> <span data-ttu-id="c2c7d-115">W tym artykule są stosowane modyfikowalne typy wartości tylko w celach demonstracyjnych.</span><span class="sxs-lookup"><span data-stu-id="c2c7d-115">This article uses mutable value types only for demonstration purposes.</span></span>

## <a name="kinds-of-value-types-and-type-constraints"></a><span data-ttu-id="c2c7d-116">Rodzaje typów wartości i ograniczenia typu</span><span class="sxs-lookup"><span data-stu-id="c2c7d-116">Kinds of value types and type constraints</span></span>

<span data-ttu-id="c2c7d-117">Typ wartości może być jednym z dwóch następujących rodzajów:</span><span class="sxs-lookup"><span data-stu-id="c2c7d-117">A value type can be one of the two following kinds:</span></span>

- <span data-ttu-id="c2c7d-118">[Typ struktury](struct.md), który hermetyzuje dane i powiązane funkcje</span><span class="sxs-lookup"><span data-stu-id="c2c7d-118">a [structure type](struct.md), which encapsulates data and related functionality</span></span>
- <span data-ttu-id="c2c7d-119">[Typ wyliczeniowy](enum.md), który jest zdefiniowany przez zestaw nazwanych stałych i reprezentuje wybór lub kombinację opcji</span><span class="sxs-lookup"><span data-stu-id="c2c7d-119">an [enumeration type](enum.md), which is defined by a set of named constants and represents a choice or a combination of choices</span></span>

<span data-ttu-id="c2c7d-120">[Typ wartości null](nullable-value-types.md) `T?` reprezentuje wszystkie wartości jego bazowego typu wartości `T` oraz dodatkową wartość [null](../keywords/null.md) .</span><span class="sxs-lookup"><span data-stu-id="c2c7d-120">A [nullable value type](nullable-value-types.md) `T?` represents all values of its underlying value type `T` and an additional [null](../keywords/null.md) value.</span></span> <span data-ttu-id="c2c7d-121">Nie można przypisać `null` do zmiennej typu wartości, chyba że jest to typ wartości null.</span><span class="sxs-lookup"><span data-stu-id="c2c7d-121">You cannot assign `null` to a variable of a value type, unless it's a nullable value type.</span></span>

<span data-ttu-id="c2c7d-122">Możesz użyć [ `struct` ograniczenia](../../programming-guide/generics/constraints-on-type-parameters.md) , aby określić, że parametr typu jest typem wartości niedopuszczający wartości null.</span><span class="sxs-lookup"><span data-stu-id="c2c7d-122">You can use the [`struct` constraint](../../programming-guide/generics/constraints-on-type-parameters.md) to specify that a type parameter is a non-nullable value type.</span></span> <span data-ttu-id="c2c7d-123">Zarówno struktura, jak i typy wyliczeniowe spełniają `struct` warunek ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="c2c7d-123">Both structure and enumeration types satisfy the `struct` constraint.</span></span> <span data-ttu-id="c2c7d-124">Począwszy od języka C# 7,3, można użyć `System.Enum` w ramach ograniczenia klasy bazowej (zwanego [ograniczeniem wyliczenia](../../programming-guide/generics/constraints-on-type-parameters.md#enum-constraints)), aby określić, że parametr typu jest typem wyliczenia.</span><span class="sxs-lookup"><span data-stu-id="c2c7d-124">Beginning with C# 7.3, you can use `System.Enum` in a base class constraint (that is known as the [enum constraint](../../programming-guide/generics/constraints-on-type-parameters.md#enum-constraints)) to specify that a type parameter is an enumeration type.</span></span>

## <a name="built-in-value-types"></a><span data-ttu-id="c2c7d-125">Wbudowane typy wartości</span><span class="sxs-lookup"><span data-stu-id="c2c7d-125">Built-in value types</span></span>

<span data-ttu-id="c2c7d-126">Język C# udostępnia następujące wbudowane typy wartości, znane także jako *typy proste*:</span><span class="sxs-lookup"><span data-stu-id="c2c7d-126">C# provides the following built-in value types, also known as *simple types*:</span></span>

- [<span data-ttu-id="c2c7d-127">Typy liczb całkowitych</span><span class="sxs-lookup"><span data-stu-id="c2c7d-127">Integral numeric types</span></span>](integral-numeric-types.md)
- [<span data-ttu-id="c2c7d-128">Zmiennoprzecinkowe rodzaje wartości numerycznych</span><span class="sxs-lookup"><span data-stu-id="c2c7d-128">Floating-point numeric types</span></span>](floating-point-numeric-types.md)
- <span data-ttu-id="c2c7d-129">[bool](bool.md) reprezentujący wartość logiczną</span><span class="sxs-lookup"><span data-stu-id="c2c7d-129">[bool](bool.md) that represents a Boolean value</span></span>
- <span data-ttu-id="c2c7d-130">[char](char.md) , który reprezentuje znak Unicode UTF-16</span><span class="sxs-lookup"><span data-stu-id="c2c7d-130">[char](char.md) that represents a Unicode UTF-16 character</span></span>

<span data-ttu-id="c2c7d-131">Wszystkie typy proste są typami struktury i różnią się od innych typów struktury w tym, że dopuszczają pewne dodatkowe operacje:</span><span class="sxs-lookup"><span data-stu-id="c2c7d-131">All simple types are structure types and differ from other structure types in that they permit certain additional operations:</span></span>

- <span data-ttu-id="c2c7d-132">Można użyć literałów, aby podać wartość typu prostego.</span><span class="sxs-lookup"><span data-stu-id="c2c7d-132">You can use literals to provide a value of a simple type.</span></span> <span data-ttu-id="c2c7d-133">Na przykład `'A'` jest literałem typu `char` i `2001` jest literałem typu `int` .</span><span class="sxs-lookup"><span data-stu-id="c2c7d-133">For example, `'A'` is a literal of the type `char` and `2001` is a literal of the type `int`.</span></span>

- <span data-ttu-id="c2c7d-134">Stałe typów prostych można zadeklarować za pomocą słowa kluczowego [const](../keywords/const.md) .</span><span class="sxs-lookup"><span data-stu-id="c2c7d-134">You can declare constants of the simple types with the [const](../keywords/const.md) keyword.</span></span> <span data-ttu-id="c2c7d-135">Nie jest możliwe posiadanie stałych dla innych typów struktury.</span><span class="sxs-lookup"><span data-stu-id="c2c7d-135">It's not possible to have constants of other structure types.</span></span>

- <span data-ttu-id="c2c7d-136">Wyrażenia stałe, których operandy to wszystkie stałe typów prostych, są oceniane w czasie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="c2c7d-136">Constant expressions, whose operands are all constants of the simple types, are evaluated at compile time.</span></span>

<span data-ttu-id="c2c7d-137">Począwszy od języka C# 7,0, C# obsługuje [krotki wartości](value-tuples.md).</span><span class="sxs-lookup"><span data-stu-id="c2c7d-137">Beginning with C# 7.0, C# supports [value tuples](value-tuples.md).</span></span> <span data-ttu-id="c2c7d-138">Krotka wartości jest typem wartości, ale nie typem prostym.</span><span class="sxs-lookup"><span data-stu-id="c2c7d-138">A value tuple is a value type, but not a simple type.</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="c2c7d-139">specyfikacja języka C#</span><span class="sxs-lookup"><span data-stu-id="c2c7d-139">C# language specification</span></span>

<span data-ttu-id="c2c7d-140">Aby uzyskać więcej informacji, zobacz następujące sekcje [specyfikacji języka C#](~/_csharplang/spec/introduction.md):</span><span class="sxs-lookup"><span data-stu-id="c2c7d-140">For more information, see the following sections of the [C# language specification](~/_csharplang/spec/introduction.md):</span></span>

- [<span data-ttu-id="c2c7d-141">Typy wartości</span><span class="sxs-lookup"><span data-stu-id="c2c7d-141">Value types</span></span>](~/_csharplang/spec/types.md#value-types)
- [<span data-ttu-id="c2c7d-142">Typy proste</span><span class="sxs-lookup"><span data-stu-id="c2c7d-142">Simple types</span></span>](~/_csharplang/spec/types.md#simple-types)
- [<span data-ttu-id="c2c7d-143">Zmienne</span><span class="sxs-lookup"><span data-stu-id="c2c7d-143">Variables</span></span>](~/_csharplang/spec/variables.md)

## <a name="see-also"></a><span data-ttu-id="c2c7d-144">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="c2c7d-144">See also</span></span>

- [<span data-ttu-id="c2c7d-145">Dokumentacja języka C#</span><span class="sxs-lookup"><span data-stu-id="c2c7d-145">C# reference</span></span>](../index.md)
- <xref:System.ValueType?displayProperty=nameWithType>
- [<span data-ttu-id="c2c7d-146">Typy odwołań</span><span class="sxs-lookup"><span data-stu-id="c2c7d-146">Reference types</span></span>](../keywords/reference-types.md)
