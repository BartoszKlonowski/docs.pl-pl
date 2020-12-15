---
title: Jak napisać Konstruktor kopiujący — Przewodnik programowania w języku C#
description: Dowiedz się, jak napisać Konstruktor kopiujący w języku C#, który przyjmuje wystąpienie klasy i zwraca nowe wystąpienie z wartościami wejściowymi.
ms.date: 07/20/2015
helpviewer_keywords:
- C# Language, copy constructor
- copy constructor [C#]
ms.topic: how-to
ms.custom: contperf-fy21q2
ms.assetid: fba899b5-fc41-428e-a745-3ebdbf37990a
ms.openlocfilehash: dfc702bfe183b3712b20c64f9e82d2d3c3edd6d5
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97512375"
---
# <a name="how-to-write-a-copy-constructor-c-programming-guide"></a><span data-ttu-id="41091-103">Jak napisać Konstruktor kopiujący (Przewodnik programowania w języku C#)</span><span class="sxs-lookup"><span data-stu-id="41091-103">How to write a copy constructor (C# Programming Guide)</span></span>

<span data-ttu-id="41091-104">Język C# nie udostępnia konstruktora kopiującego dla obiektów, ale można napisać jeden siebie.</span><span class="sxs-lookup"><span data-stu-id="41091-104">C# doesn't provide a copy constructor for objects, but you can write one yourself.</span></span>  
  
## <a name="example"></a><span data-ttu-id="41091-105">Przykład</span><span class="sxs-lookup"><span data-stu-id="41091-105">Example</span></span>  

 <span data-ttu-id="41091-106">W poniższym przykładzie `Person` [Klasa](../../language-reference/keywords/class.md) definiuje Konstruktor kopiujący, który przyjmuje, jako argument, wystąpienie `Person` .</span><span class="sxs-lookup"><span data-stu-id="41091-106">In the following example, the `Person`[class](../../language-reference/keywords/class.md) defines a copy constructor that takes, as its argument, an instance of `Person`.</span></span> <span data-ttu-id="41091-107">Wartości właściwości argumentu są przypisywane do właściwości nowego wystąpienia `Person` .</span><span class="sxs-lookup"><span data-stu-id="41091-107">The values of the properties of the argument are assigned to the properties of the new instance of `Person`.</span></span> <span data-ttu-id="41091-108">Kod zawiera alternatywny Konstruktor kopiujący, który wysyła `Name` `Age` właściwości i wystąpienia, które chcesz skopiować do konstruktora wystąpienia klasy.</span><span class="sxs-lookup"><span data-stu-id="41091-108">The code contains an alternative copy constructor that sends the `Name` and `Age` properties of the instance that you want to copy to the instance constructor of the class.</span></span>  
  
 [!code-csharp[csProgGuideObjects#16](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#16)]  
  
## <a name="see-also"></a><span data-ttu-id="41091-109">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="41091-109">See also</span></span>

- <xref:System.ICloneable>
- [<span data-ttu-id="41091-110">Przewodnik programowania w języku C#</span><span class="sxs-lookup"><span data-stu-id="41091-110">C# Programming Guide</span></span>](../index.md)
- [<span data-ttu-id="41091-111">Klasy i struktury</span><span class="sxs-lookup"><span data-stu-id="41091-111">Classes and Structs</span></span>](./index.md)
- [<span data-ttu-id="41091-112">Konstruktory</span><span class="sxs-lookup"><span data-stu-id="41091-112">Constructors</span></span>](./constructors.md)
- [<span data-ttu-id="41091-113">Finalizatory</span><span class="sxs-lookup"><span data-stu-id="41091-113">Finalizers</span></span>](./destructors.md)
