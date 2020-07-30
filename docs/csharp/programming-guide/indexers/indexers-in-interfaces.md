---
title: Indeksatory w interfejsach — Przewodnik programowania w języku C#
description: Indeksatory mogą być deklarowane w interfejsie w języku C#. Dowiedz się, jak metody dostępu indeksatorów interfejsów różnią się od metod dostępu indeksatorów klas.
ms.date: 02/08/2020
helpviewer_keywords:
- indexers [C#], in interfaces
- accessors [C#], indexers
ms.assetid: e16b54bd-4a83-4f52-bd75-65819fca79e8
ms.openlocfilehash: ec77843bdf3181a543bd6c02cfb034b21ded1ae7
ms.sourcegitcommit: 6f58a5f75ceeb936f8ee5b786e9adb81a9a3bee9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/28/2020
ms.locfileid: "87303104"
---
# <a name="indexers-in-interfaces-c-programming-guide"></a><span data-ttu-id="8fbde-104">Indeksatory w interfejsach (Przewodnik programowania w języku C#)</span><span class="sxs-lookup"><span data-stu-id="8fbde-104">Indexers in Interfaces (C# Programming Guide)</span></span>

<span data-ttu-id="8fbde-105">Indeksatory mogą być deklarowane w [interfejsie](../../language-reference/keywords/interface.md).</span><span class="sxs-lookup"><span data-stu-id="8fbde-105">Indexers can be declared on an [interface](../../language-reference/keywords/interface.md).</span></span> <span data-ttu-id="8fbde-106">Metody dostępu indeksatorów interfejsów różnią się od metod dostępu indeksatorów [klas](../../language-reference/keywords/class.md) w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="8fbde-106">Accessors of interface indexers differ from the accessors of [class](../../language-reference/keywords/class.md) indexers in the following ways:</span></span>

- <span data-ttu-id="8fbde-107">Metody dostępu interfejsów nie używają modyfikatorów.</span><span class="sxs-lookup"><span data-stu-id="8fbde-107">Interface accessors do not use modifiers.</span></span>
- <span data-ttu-id="8fbde-108">Metoda dostępu do interfejsu zazwyczaj nie ma treści.</span><span class="sxs-lookup"><span data-stu-id="8fbde-108">An interface accessor typically does not have a body.</span></span>

<span data-ttu-id="8fbde-109">Celem metody dostępu jest wskazanie, czy indeksator jest tylko do odczytu i zapisu, tylko do odczytu lub tylko do zapisu.</span><span class="sxs-lookup"><span data-stu-id="8fbde-109">The purpose of the accessor is to indicate whether the indexer is read-write, read-only, or write-only.</span></span> <span data-ttu-id="8fbde-110">Możesz podać implementację indeksatora zdefiniowanego w interfejsie, ale jest to rzadkie.</span><span class="sxs-lookup"><span data-stu-id="8fbde-110">You may provide an implementation for an indexer defined in an interface, but this is rare.</span></span> <span data-ttu-id="8fbde-111">Indeksatory zwykle definiują interfejs API do uzyskiwania dostępu do pól danych, a pola danych nie mogą być zdefiniowane w interfejsie.</span><span class="sxs-lookup"><span data-stu-id="8fbde-111">Indexers typically define an API to access data fields, and data fields cannot be defined in an interface.</span></span>

<span data-ttu-id="8fbde-112">Oto przykład metody dostępu indeksatora interfejsu:</span><span class="sxs-lookup"><span data-stu-id="8fbde-112">The following is an example of an interface indexer accessor:</span></span>

[!code-csharp[DefineInterface](~/samples/snippets/csharp/interfaces/indexers.cs#DefineIndexer)]

<span data-ttu-id="8fbde-113">Podpis indeksatora musi różnić się od sygnatur wszystkich innych indeksatorów zadeklarowanych w tym samym interfejsie.</span><span class="sxs-lookup"><span data-stu-id="8fbde-113">The signature of an indexer must differ from the signatures of all other indexers declared in the same interface.</span></span>

## <a name="example"></a><span data-ttu-id="8fbde-114">Przykład</span><span class="sxs-lookup"><span data-stu-id="8fbde-114">Example</span></span>

<span data-ttu-id="8fbde-115">Poniższy przykład pokazuje, jak zaimplementować indeksatory interfejsów.</span><span class="sxs-lookup"><span data-stu-id="8fbde-115">The following example shows how to implement interface indexers.</span></span>

[!code-csharp[Implement](~/samples/snippets/csharp/interfaces/indexers.cs#ImplementInterface)]

[!code-csharp[DefineInterface](~/samples/snippets/csharp/interfaces/indexers.cs#ExampleCode)]

<span data-ttu-id="8fbde-116">W powyższym przykładzie można użyć jawnej implementacji elementu członkowskiego interfejsu przy użyciu w pełni kwalifikowanej nazwy elementu członkowskiego interfejsu.</span><span class="sxs-lookup"><span data-stu-id="8fbde-116">In the preceding example, you could use the explicit interface member implementation by using the fully qualified name of the interface member.</span></span> <span data-ttu-id="8fbde-117">Na przykład</span><span class="sxs-lookup"><span data-stu-id="8fbde-117">For example</span></span>

```csharp
string IIndexInterface.this[int index]
{
}
```

<span data-ttu-id="8fbde-118">Jednak w pełni kwalifikowana nazwa jest wymagana tylko wtedy, gdy klasa implementuje więcej niż jeden interfejs o tej samej sygnaturze indeksatora.</span><span class="sxs-lookup"><span data-stu-id="8fbde-118">However, the fully qualified name is only needed to avoid ambiguity when the class is implementing more than one interface with the same indexer signature.</span></span> <span data-ttu-id="8fbde-119">Na przykład jeśli `Employee` Klasa implementuje dwa interfejsy, a `ICitizen` `IEmployee` oba interfejsy mają tę samą sygnaturę indeksatora, wymagana jest Jawna implementacja elementu członkowskiego interfejsu.</span><span class="sxs-lookup"><span data-stu-id="8fbde-119">For example, if an `Employee` class is implementing two interfaces, `ICitizen` and `IEmployee`, and both interfaces have the same indexer signature, the explicit interface member implementation is necessary.</span></span> <span data-ttu-id="8fbde-120">Oznacza to, że następująca deklaracja indeksatora:</span><span class="sxs-lookup"><span data-stu-id="8fbde-120">That is, the following indexer declaration:</span></span>

```csharp
string IEmployee.this[int index]
{
}
```

<span data-ttu-id="8fbde-121">implementuje indeksator w `IEmployee` interfejsie, podczas gdy następująca deklaracja:</span><span class="sxs-lookup"><span data-stu-id="8fbde-121">implements the indexer on the `IEmployee` interface, while the following declaration:</span></span>

```csharp
string ICitizen.this[int index]
{
}
```

<span data-ttu-id="8fbde-122">implementuje indeksator w `ICitizen` interfejsie.</span><span class="sxs-lookup"><span data-stu-id="8fbde-122">implements the indexer on the `ICitizen` interface.</span></span>

## <a name="see-also"></a><span data-ttu-id="8fbde-123">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="8fbde-123">See also</span></span>

- [<span data-ttu-id="8fbde-124">Przewodnik programowania w języku C#</span><span class="sxs-lookup"><span data-stu-id="8fbde-124">C# Programming Guide</span></span>](../index.md)
- [<span data-ttu-id="8fbde-125">Indexers (Indeksatory)</span><span class="sxs-lookup"><span data-stu-id="8fbde-125">Indexers</span></span>](./index.md)
- [<span data-ttu-id="8fbde-126">Właściwości</span><span class="sxs-lookup"><span data-stu-id="8fbde-126">Properties</span></span>](../classes-and-structs/properties.md)
- [<span data-ttu-id="8fbde-127">Interfejsy</span><span class="sxs-lookup"><span data-stu-id="8fbde-127">Interfaces</span></span>](../interfaces/index.md)
