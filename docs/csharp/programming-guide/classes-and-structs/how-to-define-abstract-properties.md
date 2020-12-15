---
title: Jak definiować właściwości abstrakcyjne — Przewodnik programowania w języku C#
description: Dowiedz się, jak definiować właściwości abstrakcyjne w języku C#. Deklarowanie właściwości abstrakcyjnej oznacza, że Klasa obsługuje właściwość. Klasy pochodne implementują metody dostępu.
ms.date: 07/20/2015
helpviewer_keywords:
- properties [C#], abstract
- abstract properties [C#]
ms.topic: how-to
ms.custom: contperf-fy21q2
ms.assetid: 672a90eb-47b9-4ae0-9914-af53852fddcb
ms.openlocfilehash: e114e9349db9d6bcb18e15eb62532f48aa063339
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97513032"
---
# <a name="how-to-define-abstract-properties-c-programming-guide"></a><span data-ttu-id="7dc72-105">Jak definiować właściwości abstrakcyjne (Przewodnik programowania w języku C#)</span><span class="sxs-lookup"><span data-stu-id="7dc72-105">How to define abstract properties (C# Programming Guide)</span></span>

<span data-ttu-id="7dc72-106">Poniższy przykład pokazuje, jak definiować właściwości [abstrakcyjne](../../language-reference/keywords/abstract.md) .</span><span class="sxs-lookup"><span data-stu-id="7dc72-106">The following example shows how to define [abstract](../../language-reference/keywords/abstract.md) properties.</span></span> <span data-ttu-id="7dc72-107">Deklaracja właściwości abstrakcyjnej nie zapewnia implementacji metod dostępu do właściwości — deklaruje, że Klasa obsługuje właściwości, ale pozostawia implementację metody dostępu do klas pochodnych.</span><span class="sxs-lookup"><span data-stu-id="7dc72-107">An abstract property declaration does not provide an implementation of the property accessors -- it declares that the class supports properties, but leaves the accessor implementation to derived classes.</span></span> <span data-ttu-id="7dc72-108">W poniższym przykładzie pokazano, jak zaimplementować właściwości abstrakcyjne dziedziczone z klasy bazowej.</span><span class="sxs-lookup"><span data-stu-id="7dc72-108">The following example demonstrates how to implement the abstract properties inherited from a base class.</span></span>  
  
 <span data-ttu-id="7dc72-109">Ten przykład składa się z trzech plików, z których każdy jest kompilowany indywidualnie, a jego wynikający z nich zestaw jest przywoływany przez następną kompilację:</span><span class="sxs-lookup"><span data-stu-id="7dc72-109">This sample consists of three files, each of which is compiled individually and its resulting assembly is referenced by the next compilation:</span></span>  
  
- <span data-ttu-id="7dc72-110">abstractshape.cs: `Shape` Klasa, która zawiera właściwość abstrakcyjną `Area` .</span><span class="sxs-lookup"><span data-stu-id="7dc72-110">abstractshape.cs: the `Shape` class that contains an abstract `Area` property.</span></span>  
  
- <span data-ttu-id="7dc72-111">shapes.cs: podklasy `Shape` klasy.</span><span class="sxs-lookup"><span data-stu-id="7dc72-111">shapes.cs: The subclasses of the `Shape` class.</span></span>  
  
- <span data-ttu-id="7dc72-112">shapetest.cs: Program testowy do wyświetlania obszarów niektórych `Shape` obiektów pochodnych.</span><span class="sxs-lookup"><span data-stu-id="7dc72-112">shapetest.cs: A test program to display the areas of some `Shape`-derived objects.</span></span>  
  
 <span data-ttu-id="7dc72-113">Aby skompilować przykład, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="7dc72-113">To compile the example, use the following command:</span></span>  
  
 `csc abstractshape.cs shapes.cs shapetest.cs`  
  
 <span data-ttu-id="7dc72-114">Spowoduje to utworzenie pliku wykonywalnego shapetest.exe.</span><span class="sxs-lookup"><span data-stu-id="7dc72-114">This will create the executable file shapetest.exe.</span></span>  
  
## <a name="example"></a><span data-ttu-id="7dc72-115">Przykład</span><span class="sxs-lookup"><span data-stu-id="7dc72-115">Example</span></span>  

 <span data-ttu-id="7dc72-116">Ten plik deklaruje `Shape` klasę, która zawiera `Area` Właściwość typu `double` .</span><span class="sxs-lookup"><span data-stu-id="7dc72-116">This file declares the `Shape` class that contains the `Area` property of the type `double`.</span></span>  
  
 [!code-csharp[csProgGuideInheritance#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#1)]  
  
- <span data-ttu-id="7dc72-117">Modyfikatory we właściwości są umieszczane na samej deklaracji właściwości.</span><span class="sxs-lookup"><span data-stu-id="7dc72-117">Modifiers on the property are placed on the property declaration itself.</span></span> <span data-ttu-id="7dc72-118">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="7dc72-118">For example:</span></span>  
  
    ```csharp  
    public abstract double Area  
    ```  
  
- <span data-ttu-id="7dc72-119">Podczas deklarowania właściwości abstrakcyjnej ( `Area` na przykład w tym przykładzie) można po prostu wskazać, jakie metody dostępu do właściwości są dostępne, ale nie należy ich wdrażać.</span><span class="sxs-lookup"><span data-stu-id="7dc72-119">When declaring an abstract property (such as `Area` in this example), you simply indicate what property accessors are available, but do not implement them.</span></span> <span data-ttu-id="7dc72-120">W tym przykładzie dostępna jest tylko metoda dostępu [Get](../../language-reference/keywords/get.md) , więc właściwość jest tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="7dc72-120">In this example, only a [get](../../language-reference/keywords/get.md) accessor is available, so the property is read-only.</span></span>  
  
## <a name="example"></a><span data-ttu-id="7dc72-121">Przykład</span><span class="sxs-lookup"><span data-stu-id="7dc72-121">Example</span></span>  

 <span data-ttu-id="7dc72-122">Poniższy kod przedstawia trzy podklasy `Shape` i sposób, w jaki zastępują `Area` Właściwość w celu zapewnienia własnej implementacji.</span><span class="sxs-lookup"><span data-stu-id="7dc72-122">The following code shows three subclasses of `Shape` and how they override the `Area` property to provide their own implementation.</span></span>  
  
 [!code-csharp[csProgGuideInheritance#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#2)]  
  
## <a name="example"></a><span data-ttu-id="7dc72-123">Przykład</span><span class="sxs-lookup"><span data-stu-id="7dc72-123">Example</span></span>  

 <span data-ttu-id="7dc72-124">Poniższy kod przedstawia program testowy, który tworzy wiele `Shape` obiektów pochodnych i drukuje ich obszary.</span><span class="sxs-lookup"><span data-stu-id="7dc72-124">The following code shows a test program that creates a number of `Shape`-derived objects and prints out their areas.</span></span>  
  
 [!code-csharp[csProgGuideInheritance#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#3)]  
  
## <a name="see-also"></a><span data-ttu-id="7dc72-125">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="7dc72-125">See also</span></span>

- [<span data-ttu-id="7dc72-126">Przewodnik programowania w języku C#</span><span class="sxs-lookup"><span data-stu-id="7dc72-126">C# Programming Guide</span></span>](../index.md)
- [<span data-ttu-id="7dc72-127">Klasy i struktury</span><span class="sxs-lookup"><span data-stu-id="7dc72-127">Classes and Structs</span></span>](./index.md)
- [<span data-ttu-id="7dc72-128">Klasy abstrakcyjne i zapieczętowane oraz członkowie klas</span><span class="sxs-lookup"><span data-stu-id="7dc72-128">Abstract and Sealed Classes and Class Members</span></span>](./abstract-and-sealed-classes-and-class-members.md)
- [<span data-ttu-id="7dc72-129">Właściwości</span><span class="sxs-lookup"><span data-stu-id="7dc72-129">Properties</span></span>](./properties.md)
