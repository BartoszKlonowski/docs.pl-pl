---
title: Jak zwrócić podzbiory właściwości elementów w przewodniku programowania zapytania — C#
description: Dowiedz się, jak używać typu anonimowego w wyrażeniu zapytania w języku C#, aby zwracać niektóre właściwości każdego elementu źródłowego.
ms.date: 07/20/2015
helpviewer_keywords:
- anonymous types [C#], for subsets of element properties
ms.topic: how-to
ms.custom: contperf-fy21q2
ms.assetid: fabdf349-f443-4e3f-8368-6c471be1dd7b
ms.openlocfilehash: 5784d6a288af374d357346e32535ebe9c1877bcc
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97512798"
---
# <a name="how-to-return-subsets-of-element-properties-in-a-query-c-programming-guide"></a><span data-ttu-id="a8604-103">Jak zwrócić podzbiory właściwości elementu w zapytaniu (Przewodnik programowania w języku C#)</span><span class="sxs-lookup"><span data-stu-id="a8604-103">How to return subsets of element properties in a query (C# Programming Guide)</span></span>

<span data-ttu-id="a8604-104">Użyj typu anonimowego w wyrażeniu zapytania, jeśli są spełnione oba te warunki:</span><span class="sxs-lookup"><span data-stu-id="a8604-104">Use an anonymous type in a query expression when both of these conditions apply:</span></span>  
  
- <span data-ttu-id="a8604-105">Chcesz zwrócić tylko niektóre właściwości każdego elementu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="a8604-105">You want to return only some of the properties of each source element.</span></span>  
  
- <span data-ttu-id="a8604-106">Nie jest konieczne przechowywanie wyników zapytania poza zakresem metody, w której jest wykonywane zapytanie.</span><span class="sxs-lookup"><span data-stu-id="a8604-106">You do not have to store the query results outside the scope of the method in which the query is executed.</span></span>  
  
 <span data-ttu-id="a8604-107">Jeśli chcesz zwrócić tylko jedną właściwość lub pole z każdego elementu źródłowego, możesz po prostu użyć operatora kropki w `select` klauzuli.</span><span class="sxs-lookup"><span data-stu-id="a8604-107">If you only want to return one property or field from each source element, then you can just use the dot operator in the `select` clause.</span></span> <span data-ttu-id="a8604-108">Aby na przykład zwrócić tylko te dane `ID` `student` , należy napisać `select` klauzulę w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a8604-108">For example, to return only the `ID` of each `student`, write the `select` clause as follows:</span></span>  
  
```csharp  
select student.ID;  
```  
  
## <a name="example"></a><span data-ttu-id="a8604-109">Przykład</span><span class="sxs-lookup"><span data-stu-id="a8604-109">Example</span></span>  

 <span data-ttu-id="a8604-110">Poniższy przykład pokazuje, jak używać typu anonimowego, aby zwrócić tylko podzestaw właściwości każdego elementu źródłowego, który jest zgodny z określonym warunkiem.</span><span class="sxs-lookup"><span data-stu-id="a8604-110">The following example shows how to use an anonymous type to return only a subset of the properties of each source element that matches the specified condition.</span></span>  
  
 [!code-csharp[csProgGuideLINQ#31](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideLINQ/CS/csRef30LangFeatures_2.cs#31)]  
  
 <span data-ttu-id="a8604-111">Należy pamiętać, że typ anonimowy używa nazw elementów źródłowych dla jego właściwości, jeśli nie określono żadnych nazw.</span><span class="sxs-lookup"><span data-stu-id="a8604-111">Note that the anonymous type uses the source element's names for its properties if no names are specified.</span></span> <span data-ttu-id="a8604-112">Aby nadać nowym nazw właściwościom typu anonimowego, należy napisać instrukcję w `select` następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a8604-112">To give new names to the properties in the anonymous type, write the `select` statement as follows:</span></span>  
  
```csharp  
select new { First = student.FirstName, Last = student.LastName };  
```  
  
 <span data-ttu-id="a8604-113">Jeśli spróbujesz użyć tego w poprzednim przykładzie, `Console.WriteLine` należy również zmienić instrukcję:</span><span class="sxs-lookup"><span data-stu-id="a8604-113">If you try this in the previous example, then the `Console.WriteLine` statement must also change:</span></span>  
  
```csharp  
Console.WriteLine(student.First + " " + student.Last);  
```  
  
## <a name="compiling-the-code"></a><span data-ttu-id="a8604-114">Kompilowanie kodu</span><span class="sxs-lookup"><span data-stu-id="a8604-114">Compiling the Code</span></span>  
  
<span data-ttu-id="a8604-115">Aby uruchomić ten kod, skopiuj i wklej klasę do aplikacji konsolowej C# z `using` dyrektywą dla System. LINQ.</span><span class="sxs-lookup"><span data-stu-id="a8604-115">To run this code, copy and paste the class into a C# console application  with a `using` directive for System.Linq.</span></span>
  
## <a name="see-also"></a><span data-ttu-id="a8604-116">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="a8604-116">See also</span></span>

- [<span data-ttu-id="a8604-117">Przewodnik programowania w języku C#</span><span class="sxs-lookup"><span data-stu-id="a8604-117">C# Programming Guide</span></span>](../index.md)
- [<span data-ttu-id="a8604-118">Typy anonimowe</span><span class="sxs-lookup"><span data-stu-id="a8604-118">Anonymous Types</span></span>](./anonymous-types.md)
- [<span data-ttu-id="a8604-119">LINQ w C#</span><span class="sxs-lookup"><span data-stu-id="a8604-119">LINQ in C#</span></span>](../../linq/index.md)
