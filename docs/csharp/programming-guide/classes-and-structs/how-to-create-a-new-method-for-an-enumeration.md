---
title: Jak utworzyć nową metodę dla Przewodnik programowania w języku C#
description: Dowiedz się, jak przy użyciu metod rozszerzania dodać funkcję do wyliczenia w języku C#. Ten przykład pokazuje metodę rozszerzenia o nazwie Pass dla wyliczenia o nazwie klasy.
ms.date: 07/20/2015
helpviewer_keywords:
- enumerations [C#]
- extension methods [C#], for enums
- enum extensibility [C#]
ms.topic: how-to
ms.custom: contperf-fy21q2
ms.assetid: 100106f9-1e54-462c-8ebe-3892fe23b6eb
ms.openlocfilehash: 88afff854b8136bde837db8effb0e0eb512e1099
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97513097"
---
# <a name="how-to-create-a-new-method-for-an-enumeration-c-programming-guide"></a><span data-ttu-id="d14fd-104">Jak utworzyć nową metodę dla wyliczenia (Przewodnik programowania w języku C#)</span><span class="sxs-lookup"><span data-stu-id="d14fd-104">How to create a new method for an enumeration (C# Programming Guide)</span></span>

<span data-ttu-id="d14fd-105">Można użyć metod rozszerzających, aby dodać funkcje specyficzne dla określonego typu wyliczeniowego.</span><span class="sxs-lookup"><span data-stu-id="d14fd-105">You can use extension methods to add functionality specific to a particular enum type.</span></span>  
  
## <a name="example"></a><span data-ttu-id="d14fd-106">Przykład</span><span class="sxs-lookup"><span data-stu-id="d14fd-106">Example</span></span>  

 <span data-ttu-id="d14fd-107">W poniższym przykładzie `Grades` Wyliczenie reprezentuje możliwe klasy liter, które student może odebrać w klasie.</span><span class="sxs-lookup"><span data-stu-id="d14fd-107">In the following example, the `Grades` enumeration represents the possible letter grades that a student may receive in a class.</span></span> <span data-ttu-id="d14fd-108">Metoda rozszerzenia o nazwie `Passing` jest dodawana do `Grades` typu, tak aby każde wystąpienie tego typu było teraz "znane", niezależnie od tego, czy reprezentuje ona przewagę, czy nie.</span><span class="sxs-lookup"><span data-stu-id="d14fd-108">An extension method named `Passing` is added to the `Grades` type so that each instance of that type now "knows" whether it represents a passing grade or not.</span></span>  
  
 [!code-csharp[csProgGuideExtensionMethods#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideExtensionMethods/cs/extensionmethods.cs#2)]  
  
 <span data-ttu-id="d14fd-109">Należy zauważyć, że `Extensions` Klasa zawiera również zmienną statyczną, która jest aktualizowana dynamicznie i że wartość zwracana metody rozszerzenia odzwierciedla bieżącą wartość tej zmiennej.</span><span class="sxs-lookup"><span data-stu-id="d14fd-109">Note that the `Extensions` class also contains a static variable that is updated dynamically and that the return value of the extension method reflects the current value of that variable.</span></span> <span data-ttu-id="d14fd-110">Pokazuje to, że w tle metody rozszerzające są wywoływane bezpośrednio w klasie statycznej, w której są zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="d14fd-110">This demonstrates that, behind the scenes, extension methods are invoked directly on the static class in which they are defined.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="d14fd-111">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="d14fd-111">See also</span></span>

- [<span data-ttu-id="d14fd-112">Przewodnik programowania w języku C#</span><span class="sxs-lookup"><span data-stu-id="d14fd-112">C# Programming Guide</span></span>](../index.md)
- [<span data-ttu-id="d14fd-113">Metody rozszerzania</span><span class="sxs-lookup"><span data-stu-id="d14fd-113">Extension Methods</span></span>](./extension-methods.md)
