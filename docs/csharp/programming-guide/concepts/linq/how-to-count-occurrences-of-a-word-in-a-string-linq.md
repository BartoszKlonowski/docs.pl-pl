---
title: Jak zliczyć wystąpienia wyrazu w ciągu (LINQ) (C#)
description: W tym przykładzie używa zapytania LINQ w języku C# do zliczania wystąpień określonego wyrazu w ciągu. Używa metody Split, aby utworzyć tablicę wyrazów.
ms.date: 07/20/2015
ms.assetid: f8e6f546-7c14-4aa1-8a75-e8d09f3b8ccd
ms.openlocfilehash: b354947c59747e49b5f3d099ebc3ea891fb4af90
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91159075"
---
# <a name="how-to-count-occurrences-of-a-word-in-a-string-linq-c"></a><span data-ttu-id="062c6-104">Jak zliczyć wystąpienia wyrazu w ciągu (LINQ) (C#)</span><span class="sxs-lookup"><span data-stu-id="062c6-104">How to count occurrences of a word in a string (LINQ) (C#)</span></span>

<span data-ttu-id="062c6-105">Ten przykład pokazuje, jak używać zapytania LINQ do zliczania wystąpień określonego wyrazu w ciągu.</span><span class="sxs-lookup"><span data-stu-id="062c6-105">This example shows how to use a LINQ query to count the occurrences of a specified word in a string.</span></span> <span data-ttu-id="062c6-106">Należy pamiętać, że aby wykonać licznik, najpierw <xref:System.String.Split%2A> wywoływana jest metoda, aby utworzyć tablicę wyrazów.</span><span class="sxs-lookup"><span data-stu-id="062c6-106">Note that to perform the count, first the <xref:System.String.Split%2A> method is called to create an array of words.</span></span> <span data-ttu-id="062c6-107">Metoda jest kosztem wydajności <xref:System.String.Split%2A> .</span><span class="sxs-lookup"><span data-stu-id="062c6-107">There is a performance cost to the <xref:System.String.Split%2A> method.</span></span> <span data-ttu-id="062c6-108">Jeśli jedyną operacją na ciągu jest Liczenie wyrazów, należy rozważyć użycie <xref:System.Text.RegularExpressions.Regex.Matches%2A> <xref:System.String.IndexOf%2A> metod lub.</span><span class="sxs-lookup"><span data-stu-id="062c6-108">If the only operation on the string is to count the words, you should consider using the <xref:System.Text.RegularExpressions.Regex.Matches%2A> or <xref:System.String.IndexOf%2A> methods instead.</span></span> <span data-ttu-id="062c6-109">Jeśli jednak wydajność nie jest problemem krytycznym lub zostało już podzielone zdanie w celu wykonywania innych typów zapytań na nim, warto użyć LINQ do zliczania wyrazów lub fraz.</span><span class="sxs-lookup"><span data-stu-id="062c6-109">However, if performance is not a critical issue, or you have already split the sentence in order to perform other types of queries over it, then it makes sense to use LINQ to count the words or phrases as well.</span></span>  
  
## <a name="example"></a><span data-ttu-id="062c6-110">Przykład</span><span class="sxs-lookup"><span data-stu-id="062c6-110">Example</span></span>  
  
```csharp  
class CountWords  
{  
    static void Main()  
    {  
        string text = @"Historically, the world of data and the world of objects" +  
          @" have not been well integrated. Programmers work in C# or Visual Basic" +  
          @" and also in SQL or XQuery. On the one side are concepts such as classes," +  
          @" objects, fields, inheritance, and .NET APIs. On the other side" +  
          @" are tables, columns, rows, nodes, and separate languages for dealing with" +  
          @" them. Data types often require translation between the two worlds; there are" +  
          @" different standard functions. Because the object world has no notion of query, a" +  
          @" query can only be represented as a string without compile-time type checking or" +  
          @" IntelliSense support in the IDE. Transferring data from SQL tables or XML trees to" +  
          @" objects in memory is often tedious and error-prone.";  
  
        string searchTerm = "data";  
  
        //Convert the string into an array of words  
        string[] source = text.Split(new char[] { '.', '?', '!', ' ', ';', ':', ',' }, StringSplitOptions.RemoveEmptyEntries);  
  
        // Create the query.  Use ToLowerInvariant to match "data" and "Data"
        var matchQuery = from word in source  
                         where word.ToLowerInvariant() == searchTerm.ToLowerInvariant()  
                         select word;  
  
        // Count the matches, which executes the query.  
        int wordCount = matchQuery.Count();  
        Console.WriteLine("{0} occurrences(s) of the search term \"{1}\" were found.", wordCount, searchTerm);  
  
        // Keep console window open in debug mode  
        Console.WriteLine("Press any key to exit");  
        Console.ReadKey();  
    }  
}  
/* Output:  
   3 occurrences(s) of the search term "data" were found.  
*/  
```  
  
## <a name="compiling-the-code"></a><span data-ttu-id="062c6-111">Kompilowanie kodu</span><span class="sxs-lookup"><span data-stu-id="062c6-111">Compiling the Code</span></span>  

 <span data-ttu-id="062c6-112">Utwórz projekt aplikacji konsolowej w języku C# z `using` dyrektywami dotyczącymi przestrzeni nazw System. LINQ i system.IO.</span><span class="sxs-lookup"><span data-stu-id="062c6-112">Create a C# console application project, with `using` directives for the System.Linq and System.IO namespaces.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="062c6-113">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="062c6-113">See also</span></span>

- [<span data-ttu-id="062c6-114">LINQ i ciągi (C#)</span><span class="sxs-lookup"><span data-stu-id="062c6-114">LINQ and Strings (C#)</span></span>](./linq-and-strings.md)
