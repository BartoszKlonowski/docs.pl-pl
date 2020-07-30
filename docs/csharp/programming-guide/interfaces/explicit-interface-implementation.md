---
title: Implementacja interfejsu jawnego — Przewodnik programowania w języku C#
description: Klasa może implementować interfejsy, które zawierają element członkowski o tej samej sygnaturze w języku C#. Implementacja jawna tworzy element członkowski klasy, który jest specyficzny dla jednego interfejsu.
ms.date: 01/24/2020
helpviewer_keywords:
- explicit interfaces [C#]
- interfaces [C#], explicit
ms.assetid: 181c901f-0d4c-4f29-97fc-895079617bf2
ms.openlocfilehash: a6ec328c08d1da84a11431d9400a094df8c72223
ms.sourcegitcommit: 6f58a5f75ceeb936f8ee5b786e9adb81a9a3bee9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/28/2020
ms.locfileid: "87303090"
---
# <a name="explicit-interface-implementation-c-programming-guide"></a><span data-ttu-id="d8294-104">Implementacja interfejsu jawnego (Przewodnik programowania w języku C#)</span><span class="sxs-lookup"><span data-stu-id="d8294-104">Explicit Interface Implementation (C# Programming Guide)</span></span>

<span data-ttu-id="d8294-105">Jeśli [Klasa](../../language-reference/keywords/class.md) implementuje dwa interfejsy, które zawierają element członkowski o tym samym podpisie, a następnie wdrożenie tego elementu członkowskiego w klasie spowoduje, że oba interfejsy używają tego elementu członkowskiego jako ich implementacji.</span><span class="sxs-lookup"><span data-stu-id="d8294-105">If a [class](../../language-reference/keywords/class.md) implements two interfaces that contain a member with the same signature, then implementing that member on the class will cause both interfaces to use that member as their implementation.</span></span> <span data-ttu-id="d8294-106">W poniższym przykładzie wszystkie wywołania do `Paint` wywołania tej samej metody.</span><span class="sxs-lookup"><span data-stu-id="d8294-106">In the following example, all the calls to `Paint` invoke the same method.</span></span> <span data-ttu-id="d8294-107">Ten pierwszy przykład definiuje typy:</span><span class="sxs-lookup"><span data-stu-id="d8294-107">This first sample defines the types:</span></span>

[!code-csharp[DefineSimpleTypes](~/samples/snippets/csharp/interfaces/ExplicitImplementation.cs#DefineTypes)]

<span data-ttu-id="d8294-108">Poniższy przykład wywołuje metody:</span><span class="sxs-lookup"><span data-stu-id="d8294-108">The following sample calls the methods:</span></span>

[!code-csharp[DefineSimpleTypes](~/samples/snippets/csharp/interfaces/ExplicitImplementation.cs#CallMethods)]

<span data-ttu-id="d8294-109">Gdy dwa elementy członkowskie interfejsu nie wykonują tej samej funkcji, prowadzi do niepoprawnej implementacji jednego lub obu interfejsów.</span><span class="sxs-lookup"><span data-stu-id="d8294-109">When two interface members don't perform the same function, it leads to an incorrect implementation of one or both of the interfaces.</span></span> <span data-ttu-id="d8294-110">Istnieje możliwość jawnej implementacji elementu członkowskiego interfejsu — tworzenie składowej klasy, która jest wywoływana tylko przez interfejs i jest specyficzna dla tego interfejsu.</span><span class="sxs-lookup"><span data-stu-id="d8294-110">It's possible to implement an interface member explicitly—creating a class member that is only called through the interface, and is specific to that interface.</span></span> <span data-ttu-id="d8294-111">Nazwij element członkowski klasy przy użyciu nazwy interfejsu i kropki.</span><span class="sxs-lookup"><span data-stu-id="d8294-111">Name the class member with the name of the interface and a period.</span></span> <span data-ttu-id="d8294-112">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="d8294-112">For example:</span></span>

[!code-csharp[DefineExplicitImplementation](~/samples/snippets/csharp/interfaces/ExplicitImplementation.cs#ExplicitImplementation)]

<span data-ttu-id="d8294-113">Element członkowski klasy `IControl.Paint` jest dostępny tylko za pomocą `IControl` interfejsu i `ISurface.Paint` jest dostępny tylko za pomocą `ISurface` .</span><span class="sxs-lookup"><span data-stu-id="d8294-113">The class member `IControl.Paint` is only available through the `IControl` interface, and `ISurface.Paint` is only available through `ISurface`.</span></span> <span data-ttu-id="d8294-114">Obie implementacje metod są oddzielne i nie są dostępne bezpośrednio w klasie.</span><span class="sxs-lookup"><span data-stu-id="d8294-114">Both method implementations are separate, and neither are available directly on the class.</span></span> <span data-ttu-id="d8294-115">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="d8294-115">For example:</span></span>

[!code-csharp[CallExplicitImplementation](~/samples/snippets/csharp/interfaces/ExplicitImplementation.cs#CallExplicitImplementation)]

<span data-ttu-id="d8294-116">Jawna implementacja służy również do rozwiązywania przypadków, gdy dwa interfejsy deklarują różne elementy członkowskie o tej samej nazwie, takie jak właściwość i metoda.</span><span class="sxs-lookup"><span data-stu-id="d8294-116">Explicit implementation is also used to resolve cases where two interfaces each declare different members of the same name such as a property and a method.</span></span> <span data-ttu-id="d8294-117">Aby zaimplementować oba interfejsy, Klasa musi używać jawnej implementacji dla właściwości `P` albo metody lub obu tych metod `P` , aby uniknąć błędu kompilatora.</span><span class="sxs-lookup"><span data-stu-id="d8294-117">To implement both interfaces, a class has to use explicit implementation either for the property `P`, or the method `P`, or both, to avoid a compiler error.</span></span> <span data-ttu-id="d8294-118">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="d8294-118">For example:</span></span>

[!code-csharp[NameCollisions](~/samples/snippets/csharp/interfaces/ExplicitImplementation.cs#NameCollision)]

<span data-ttu-id="d8294-119">Począwszy od [języka C# 8,0](../../whats-new/csharp-8.md#default-interface-methods), można zdefiniować implementację elementów członkowskich zadeklarowanych w interfejsie.</span><span class="sxs-lookup"><span data-stu-id="d8294-119">Beginning with [C# 8.0](../../whats-new/csharp-8.md#default-interface-methods), you can define an implementation for members declared in an interface.</span></span> <span data-ttu-id="d8294-120">Jeśli klasa dziedziczy implementację metody z interfejsu, ta metoda jest dostępna tylko za pośrednictwem typu interfejsu.</span><span class="sxs-lookup"><span data-stu-id="d8294-120">If a class inherits a method implementation from an interface, that method is only accessible through a reference of the interface type.</span></span> <span data-ttu-id="d8294-121">Dziedziczony element członkowski nie jest wyświetlany jako część interfejsu publicznego.</span><span class="sxs-lookup"><span data-stu-id="d8294-121">The inherited member doesn't appear as part of the public interface.</span></span> <span data-ttu-id="d8294-122">Poniższy przykład definiuje domyślną implementację metody interfejsu:</span><span class="sxs-lookup"><span data-stu-id="d8294-122">The following sample defines a default implementation for an interface method:</span></span>

[!code-csharp[NameCollisions](~/samples/snippets/csharp/interfaces/ExplicitImplementation.cs#DefaultImplementation)]

<span data-ttu-id="d8294-123">Poniższy przykład wywołuje domyślną implementację:</span><span class="sxs-lookup"><span data-stu-id="d8294-123">The following sample invokes the default implementation:</span></span>

[!code-csharp[NameCollisions](~/samples/snippets/csharp/interfaces/ExplicitImplementation.cs#CallDefaultImplementation)]

<span data-ttu-id="d8294-124">Każda klasa implementująca `IControl` interfejs może przesłonić `Paint` metodę domyślną jako metodę publiczną lub jako jawną implementację interfejsu.</span><span class="sxs-lookup"><span data-stu-id="d8294-124">Any class that implements the `IControl` interface can override the default `Paint` method, either as a public method, or as an explicit interface implementation.</span></span>

## <a name="see-also"></a><span data-ttu-id="d8294-125">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="d8294-125">See also</span></span>

- [<span data-ttu-id="d8294-126">Przewodnik programowania w języku C#</span><span class="sxs-lookup"><span data-stu-id="d8294-126">C# Programming Guide</span></span>](../index.md)
- [<span data-ttu-id="d8294-127">Klasy i struktury</span><span class="sxs-lookup"><span data-stu-id="d8294-127">Classes and Structs</span></span>](../classes-and-structs/index.md)
- [<span data-ttu-id="d8294-128">Interfejsy</span><span class="sxs-lookup"><span data-stu-id="d8294-128">Interfaces</span></span>](./index.md)
- [<span data-ttu-id="d8294-129">Dziedziczenie</span><span class="sxs-lookup"><span data-stu-id="d8294-129">Inheritance</span></span>](../classes-and-structs/inheritance.md)
