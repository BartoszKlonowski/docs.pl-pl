---
title: Jak znaleźć różnice między dwoma listami (LINQ) (C#)
description: Dowiedz się, jak za pomocą LINQ w języku C# porównać dwie listy ciągów i wyprowadzić te wiersze, które znajdują się na jednej liście, ale nie w drugim.
ms.date: 07/20/2015
ms.assetid: 8e8945f0-4aba-439d-8d5d-c8d1eeef4e71
ms.openlocfilehash: 01aba16b3489e4bf21a76bc715b6d4d2c9d250dd
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91159062"
---
# <a name="how-to-find-the-set-difference-between-two-lists-linq-c"></a><span data-ttu-id="7315b-103">Jak znaleźć różnice między dwoma listami (LINQ) (C#)</span><span class="sxs-lookup"><span data-stu-id="7315b-103">How to find the set difference between two lists (LINQ) (C#)</span></span>

<span data-ttu-id="7315b-104">Ten przykład pokazuje, jak używać LINQ do porównywania dwóch list ciągów i wyprowadzania tych wierszy, które znajdują się w names1.txt, ale nie w names2.txt.</span><span class="sxs-lookup"><span data-stu-id="7315b-104">This example shows how to use LINQ to compare two lists of strings and output those lines that are in names1.txt but not in names2.txt.</span></span>  
  
### <a name="to-create-the-data-files"></a><span data-ttu-id="7315b-105">Aby utworzyć pliki danych</span><span class="sxs-lookup"><span data-stu-id="7315b-105">To create the data files</span></span>  
  
1. <span data-ttu-id="7315b-106">Skopiuj names1.txt i names2.txt do folderu rozwiązania, jak pokazano w temacie [jak połączyć i porównać kolekcje ciągów (LINQ) (C#](./how-to-combine-and-compare-string-collections-linq.md)).</span><span class="sxs-lookup"><span data-stu-id="7315b-106">Copy names1.txt and names2.txt to your solution folder as shown in [How to combine and compare string collections (LINQ) (C#)](./how-to-combine-and-compare-string-collections-linq.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="7315b-107">Przykład</span><span class="sxs-lookup"><span data-stu-id="7315b-107">Example</span></span>  
  
```csharp  
class CompareLists  
{
    static void Main()  
    {  
        // Create the IEnumerable data sources.  
        string[] names1 = System.IO.File.ReadAllLines(@"../../../names1.txt");  
        string[] names2 = System.IO.File.ReadAllLines(@"../../../names2.txt");  
  
        // Create the query. Note that method syntax must be used here.  
        IEnumerable<string> differenceQuery =  
          names1.Except(names2);  
  
        // Execute the query.  
        Console.WriteLine("The following lines are in names1.txt but not names2.txt");  
        foreach (string s in differenceQuery)  
            Console.WriteLine(s);  
  
        // Keep the console window open in debug mode.  
        Console.WriteLine("Press any key to exit");  
        Console.ReadKey();  
    }  
}  
/* Output:  
     The following lines are in names1.txt but not names2.txt  
    Potra, Cristina  
    Noriega, Fabricio  
    Aw, Kam Foo  
    Toyoshima, Tim  
    Guy, Wey Yuan  
    Garcia, Debra  
     */  
```  
  
 <span data-ttu-id="7315b-108">Niektóre typy operacji zapytań w języku C#, takie jak <xref:System.Linq.Enumerable.Except%2A> , <xref:System.Linq.Enumerable.Distinct%2A> , <xref:System.Linq.Enumerable.Union%2A> i <xref:System.Linq.Enumerable.Concat%2A> , można wyrazić tylko w składni opartej na metodzie.</span><span class="sxs-lookup"><span data-stu-id="7315b-108">Some types of query operations in C#, such as <xref:System.Linq.Enumerable.Except%2A>, <xref:System.Linq.Enumerable.Distinct%2A>, <xref:System.Linq.Enumerable.Union%2A>, and <xref:System.Linq.Enumerable.Concat%2A>, can only be expressed in method-based syntax.</span></span>  
  
## <a name="compiling-the-code"></a><span data-ttu-id="7315b-109">Kompilowanie kodu</span><span class="sxs-lookup"><span data-stu-id="7315b-109">Compiling the Code</span></span>  

 <span data-ttu-id="7315b-110">Utwórz projekt aplikacji konsolowej w języku C# z `using` dyrektywami dotyczącymi przestrzeni nazw System. LINQ i system.IO.</span><span class="sxs-lookup"><span data-stu-id="7315b-110">Create a C# console application project, with `using` directives for the System.Linq and System.IO namespaces.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="7315b-111">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="7315b-111">See also</span></span>

- [<span data-ttu-id="7315b-112">LINQ i ciągi (C#)</span><span class="sxs-lookup"><span data-stu-id="7315b-112">LINQ and Strings (C#)</span></span>](./linq-and-strings.md)
