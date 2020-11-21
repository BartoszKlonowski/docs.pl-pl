---
title: Jak zwrócić podzbiory właściwości elementów w przewodniku programowania zapytania — C#
description: Dowiedz się, jak używać typu anonimowego w wyrażeniu zapytania w języku C#, aby zwracać niektóre właściwości każdego elementu źródłowego.
ms.date: 07/20/2015
helpviewer_keywords:
- anonymous types [C#], for subsets of element properties
ms.topic: how-to
ms.custom: contperfq2
ms.assetid: fabdf349-f443-4e3f-8368-6c471be1dd7b
ms.openlocfilehash: 3e30793ed16204943e2398984ed200b93db7f86f
ms.sourcegitcommit: 30e9e11dfd90112b8eec6406186ba3533f21eba1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/21/2020
ms.locfileid: "95098857"
---
# <a name="how-to-return-subsets-of-element-properties-in-a-query-c-programming-guide"></a><span data-ttu-id="15921-103">Jak zwrócić podzbiory właściwości elementu w zapytaniu (Przewodnik programowania w języku C#)</span><span class="sxs-lookup"><span data-stu-id="15921-103">How to return subsets of element properties in a query (C# Programming Guide)</span></span>

<span data-ttu-id="15921-104">Użyj typu anonimowego w wyrażeniu zapytania, jeśli są spełnione oba te warunki:</span><span class="sxs-lookup"><span data-stu-id="15921-104">Use an anonymous type in a query expression when both of these conditions apply:</span></span>  
  
- <span data-ttu-id="15921-105">Chcesz zwrócić tylko niektóre właściwości każdego elementu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="15921-105">You want to return only some of the properties of each source element.</span></span>  
  
- <span data-ttu-id="15921-106">Nie jest konieczne przechowywanie wyników zapytania poza zakresem metody, w której jest wykonywane zapytanie.</span><span class="sxs-lookup"><span data-stu-id="15921-106">You do not have to store the query results outside the scope of the method in which the query is executed.</span></span>  
  
 <span data-ttu-id="15921-107">Jeśli chcesz zwrócić tylko jedną właściwość lub pole z każdego elementu źródłowego, możesz po prostu użyć operatora kropki w `select` klauzuli.</span><span class="sxs-lookup"><span data-stu-id="15921-107">If you only want to return one property or field from each source element, then you can just use the dot operator in the `select` clause.</span></span> <span data-ttu-id="15921-108">Aby na przykład zwrócić tylko te dane `ID` `student` , należy napisać `select` klauzulę w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="15921-108">For example, to return only the `ID` of each `student`, write the `select` clause as follows:</span></span>  
  
```csharp  
select student.ID;  
```  
  
## <a name="example"></a><span data-ttu-id="15921-109">Przykład</span><span class="sxs-lookup"><span data-stu-id="15921-109">Example</span></span>  

 <span data-ttu-id="15921-110">Poniższy przykład pokazuje, jak używać typu anonimowego, aby zwrócić tylko podzestaw właściwości każdego elementu źródłowego, który jest zgodny z określonym warunkiem.</span><span class="sxs-lookup"><span data-stu-id="15921-110">The following example shows how to use an anonymous type to return only a subset of the properties of each source element that matches the specified condition.</span></span>  
  
 [!code-csharp[csProgGuideLINQ#31](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideLINQ/CS/csRef30LangFeatures_2.cs#31)]  
  
 <span data-ttu-id="15921-111">Należy pamiętać, że typ anonimowy używa nazw elementów źródłowych dla jego właściwości, jeśli nie określono żadnych nazw.</span><span class="sxs-lookup"><span data-stu-id="15921-111">Note that the anonymous type uses the source element's names for its properties if no names are specified.</span></span> <span data-ttu-id="15921-112">Aby nadać nowym nazw właściwościom typu anonimowego, należy napisać instrukcję w `select` następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="15921-112">To give new names to the properties in the anonymous type, write the `select` statement as follows:</span></span>  
  
```csharp  
select new { First = student.FirstName, Last = student.LastName };  
```  
  
 <span data-ttu-id="15921-113">Jeśli spróbujesz użyć tego w poprzednim przykładzie, `Console.WriteLine` należy również zmienić instrukcję:</span><span class="sxs-lookup"><span data-stu-id="15921-113">If you try this in the previous example, then the `Console.WriteLine` statement must also change:</span></span>  
  
```csharp  
Console.WriteLine(student.First + " " + student.Last);  
```  
  
## <a name="compiling-the-code"></a><span data-ttu-id="15921-114">Kompilowanie kodu</span><span class="sxs-lookup"><span data-stu-id="15921-114">Compiling the Code</span></span>  
  
<span data-ttu-id="15921-115">Aby uruchomić ten kod, skopiuj i wklej klasę do aplikacji konsolowej C# z `using` dyrektywą dla System. LINQ.</span><span class="sxs-lookup"><span data-stu-id="15921-115">To run this code, copy and paste the class into a C# console application  with a `using` directive for System.Linq.</span></span>
  
## <a name="see-also"></a><span data-ttu-id="15921-116">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="15921-116">See also</span></span>

- [<span data-ttu-id="15921-117">Przewodnik programowania w języku C#</span><span class="sxs-lookup"><span data-stu-id="15921-117">C# Programming Guide</span></span>](../index.md)
- [<span data-ttu-id="15921-118">Typy anonimowe</span><span class="sxs-lookup"><span data-stu-id="15921-118">Anonymous Types</span></span>](./anonymous-types.md)
- [<span data-ttu-id="15921-119">LINQ w C#</span><span class="sxs-lookup"><span data-stu-id="15921-119">LINQ in C#</span></span>](../../linq/index.md)
