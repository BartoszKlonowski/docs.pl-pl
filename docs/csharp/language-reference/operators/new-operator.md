---
title: New — odwołanie w C#
ms.date: 06/25/2019
f1_keywords:
- new_CSharpKeyword
helpviewer_keywords:
- new operator keyword [C#]
ms.assetid: a212b697-a79b-4105-9923-1f7b108036e8
ms.openlocfilehash: 7e2f1a52f1681e0cc454da8cba324dd1b5995f11
ms.sourcegitcommit: c37e8d4642fef647ebab0e1c618ecc29ddfe2a0f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2020
ms.locfileid: "87855104"
---
# <a name="new-operator-c-reference"></a><span data-ttu-id="296a3-102">New — Operator (odwołanie w C#)</span><span class="sxs-lookup"><span data-stu-id="296a3-102">new operator (C# reference)</span></span>

<span data-ttu-id="296a3-103">`new`Operator tworzy nowe wystąpienie typu.</span><span class="sxs-lookup"><span data-stu-id="296a3-103">The `new` operator creates a new instance of a type.</span></span>

<span data-ttu-id="296a3-104">Można również użyć `new` słowa kluczowego jako [modyfikatora deklaracji składowej](../keywords/new-modifier.md) lub [ograniczenia typu ogólnego](../keywords/new-constraint.md).</span><span class="sxs-lookup"><span data-stu-id="296a3-104">You can also use the `new` keyword as a [member declaration modifier](../keywords/new-modifier.md) or a [generic type constraint](../keywords/new-constraint.md).</span></span>

## <a name="constructor-invocation"></a><span data-ttu-id="296a3-105">Wywołanie konstruktora</span><span class="sxs-lookup"><span data-stu-id="296a3-105">Constructor invocation</span></span>

<span data-ttu-id="296a3-106">Aby utworzyć nowe wystąpienie typu, zazwyczaj wywoływany jest jeden z [konstruktorów](../../programming-guide/classes-and-structs/constructors.md) tego typu przy użyciu `new` operatora:</span><span class="sxs-lookup"><span data-stu-id="296a3-106">To create a new instance of a type, you typically invoke one of the [constructors](../../programming-guide/classes-and-structs/constructors.md) of that type using the `new` operator:</span></span>

[!code-csharp-interactive[invoke constructor](snippets/NewOperator.cs#Constructor)]

<span data-ttu-id="296a3-107">Można użyć [inicjatora obiektu lub kolekcji](../../programming-guide/classes-and-structs/object-and-collection-initializers.md) z `new` operatorem, aby utworzyć wystąpienie i zainicjować obiekt w jednej instrukcji, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="296a3-107">You can use an [object or collection initializer](../../programming-guide/classes-and-structs/object-and-collection-initializers.md) with the `new` operator to instantiate and initialize an object in one statement, as the following example shows:</span></span>

[!code-csharp-interactive[constructor with initializer](snippets/NewOperator.cs#ConstructorWithInitializer)]

## <a name="array-creation"></a><span data-ttu-id="296a3-108">Tworzenie tablicy</span><span class="sxs-lookup"><span data-stu-id="296a3-108">Array creation</span></span>

<span data-ttu-id="296a3-109">Możesz również użyć `new` operatora, aby utworzyć wystąpienie tablicy, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="296a3-109">You also use the `new` operator to create an array instance, as the following example shows:</span></span>

[!code-csharp-interactive[create array](snippets/NewOperator.cs#Array)]

<span data-ttu-id="296a3-110">Użyj składni inicjowania tablicy, aby utworzyć wystąpienie tablicy i wypełnić je elementami w jednej instrukcji.</span><span class="sxs-lookup"><span data-stu-id="296a3-110">Use array initialization syntax to create an array instance and populate it with elements in one statement.</span></span> <span data-ttu-id="296a3-111">W poniższym przykładzie pokazano różne sposoby wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="296a3-111">The following example shows various ways how you can do that:</span></span>

[!code-csharp-interactive[initialize array](snippets/NewOperator.cs#ArrayInitialization)]

<span data-ttu-id="296a3-112">Aby uzyskać więcej informacji na temat tablic, zobacz [tablice](../../programming-guide/arrays/index.md).</span><span class="sxs-lookup"><span data-stu-id="296a3-112">For more information about arrays, see [Arrays](../../programming-guide/arrays/index.md).</span></span>

## <a name="instantiation-of-anonymous-types"></a><span data-ttu-id="296a3-113">Tworzenie wystąpienia typów anonimowych</span><span class="sxs-lookup"><span data-stu-id="296a3-113">Instantiation of anonymous types</span></span>

<span data-ttu-id="296a3-114">Aby utworzyć wystąpienie [typu anonimowego](../../programming-guide/classes-and-structs/anonymous-types.md), użyj `new` składni operatora i inicjatora obiektów:</span><span class="sxs-lookup"><span data-stu-id="296a3-114">To create an instance of an [anonymous type](../../programming-guide/classes-and-structs/anonymous-types.md), use the `new` operator and object initializer syntax:</span></span>

[!code-csharp-interactive[anonymous type](snippets/NewOperator.cs#AnonymousType)]

## <a name="destruction-of-type-instances"></a><span data-ttu-id="296a3-115">Niszczenie wystąpień typu</span><span class="sxs-lookup"><span data-stu-id="296a3-115">Destruction of type instances</span></span>

<span data-ttu-id="296a3-116">Nie trzeba zniszczyć wcześniej utworzonych wystąpień typu.</span><span class="sxs-lookup"><span data-stu-id="296a3-116">You don't have to destroy earlier created type instances.</span></span> <span data-ttu-id="296a3-117">Wystąpienia obu typów odwołań i wartości są niszczone automatycznie.</span><span class="sxs-lookup"><span data-stu-id="296a3-117">Instances of both reference and value types are destroyed automatically.</span></span> <span data-ttu-id="296a3-118">Wystąpienia typów wartości są niszczone, gdy tylko kontekst, który zawiera te elementy, zostanie zniszczony.</span><span class="sxs-lookup"><span data-stu-id="296a3-118">Instances of value types are destroyed as soon as the context that contains them is destroyed.</span></span> <span data-ttu-id="296a3-119">Wystąpienia typów odwołań są niszczone przez [Moduł wyrzucania elementów bezużytecznych](../../../standard/garbage-collection/index.md) w nieokreślonym czasie po usunięciu ostatniego odwołania do nich.</span><span class="sxs-lookup"><span data-stu-id="296a3-119">Instances of reference types are destroyed by the [garbage collector](../../../standard/garbage-collection/index.md) at some unspecified time after the last reference to them is removed.</span></span>

<span data-ttu-id="296a3-120">Dla wystąpień typu, które zawierają niezarządzane zasoby, na przykład dojście do pliku, zaleca się zapełnienie deterministycznym czyszczeniem, aby upewnić się, że zasoby, które zawierają, są wystawione tak szybko, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="296a3-120">For type instances that contain unmanaged resources, for example, a file handle, it's recommended to employ deterministic clean-up to ensure that the resources they contain are released as soon as possible.</span></span> <span data-ttu-id="296a3-121">Aby uzyskać więcej informacji, zobacz <xref:System.IDisposable?displayProperty=nameWithType> Dokumentacja interfejsu API i artykuł [using instrukcji](../keywords/using-statement.md) .</span><span class="sxs-lookup"><span data-stu-id="296a3-121">For more information, see the <xref:System.IDisposable?displayProperty=nameWithType> API reference and the [using statement](../keywords/using-statement.md) article.</span></span>

## <a name="operator-overloadability"></a><span data-ttu-id="296a3-122">Przeciążanie operatora</span><span class="sxs-lookup"><span data-stu-id="296a3-122">Operator overloadability</span></span>

<span data-ttu-id="296a3-123">Typ zdefiniowany przez użytkownika nie może przeciążać `new` operatora.</span><span class="sxs-lookup"><span data-stu-id="296a3-123">A user-defined type cannot overload the `new` operator.</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="296a3-124">specyfikacja języka C#</span><span class="sxs-lookup"><span data-stu-id="296a3-124">C# language specification</span></span>

<span data-ttu-id="296a3-125">Aby uzyskać więcej informacji, zobacz sekcję [New Operator](~/_csharplang/spec/expressions.md#the-new-operator) w [specyfikacji języka C#](~/_csharplang/spec/introduction.md).</span><span class="sxs-lookup"><span data-stu-id="296a3-125">For more information, see [The new operator](~/_csharplang/spec/expressions.md#the-new-operator) section of the [C# language specification](~/_csharplang/spec/introduction.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="296a3-126">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="296a3-126">See also</span></span>

- [<span data-ttu-id="296a3-127">Dokumentacja języka C#</span><span class="sxs-lookup"><span data-stu-id="296a3-127">C# reference</span></span>](../index.md)
- [<span data-ttu-id="296a3-128">Operatory i wyrażenia języka C#</span><span class="sxs-lookup"><span data-stu-id="296a3-128">C# operators and expressions</span></span>](index.md)
- [<span data-ttu-id="296a3-129">Inicjatory obiektów i kolekcji</span><span class="sxs-lookup"><span data-stu-id="296a3-129">Object and collection initializers</span></span>](../../programming-guide/classes-and-structs/object-and-collection-initializers.md)
