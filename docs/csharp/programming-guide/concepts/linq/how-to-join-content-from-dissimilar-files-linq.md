---
title: Jak dołączyć zawartość z niepodobnych plików (LINQ) (C#)
description: Dowiedz się, jak dołączać dane z dwóch rozdzielanych przecinkami plików przy użyciu LINQ w języku C#. Dane współużytkują wspólną wartość używaną jako pasujący klucz.
ms.date: 06/27/2018
ms.assetid: aa2d12a6-70a9-492f-a6db-b2b850d46811
ms.openlocfilehash: 136d10ff5c0bf5f4f18998b50eb7bbee218b00a9
ms.sourcegitcommit: 04022ca5d00b2074e1b1ffdbd76bec4950697c4c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/23/2020
ms.locfileid: "87104977"
---
# <a name="how-to-join-content-from-dissimilar-files-linq-c"></a><span data-ttu-id="f8282-104">Jak dołączyć zawartość z niepodobnych plików (LINQ) (C#)</span><span class="sxs-lookup"><span data-stu-id="f8282-104">How to join content from dissimilar files (LINQ) (C#)</span></span>

<span data-ttu-id="f8282-105">Ten przykład pokazuje, jak połączyć dane z dwóch rozdzielanych przecinkami plików, które mają wspólną wartość używaną jako pasujący klucz.</span><span class="sxs-lookup"><span data-stu-id="f8282-105">This example shows how to join data from two comma-delimited files that share a common value that is used as a matching key.</span></span> <span data-ttu-id="f8282-106">Ta technika może być przydatna, jeśli trzeba połączyć dane z dwóch arkuszy kalkulacyjnych lub z arkusza kalkulacyjnego oraz z pliku, który ma inny format, do nowego pliku.</span><span class="sxs-lookup"><span data-stu-id="f8282-106">This technique can be useful if you have to combine data from two spreadsheets, or from a spreadsheet and from a file that has another format, into a new file.</span></span> <span data-ttu-id="f8282-107">Możesz zmodyfikować przykład, aby współpracować z dowolnym rodzajem tekstu strukturalnego.</span><span class="sxs-lookup"><span data-stu-id="f8282-107">You can modify the example to work with any kind of structured text.</span></span>  
  
## <a name="to-create-the-data-files"></a><span data-ttu-id="f8282-108">Aby utworzyć pliki danych</span><span class="sxs-lookup"><span data-stu-id="f8282-108">To create the data files</span></span>
  
1. <span data-ttu-id="f8282-109">Skopiuj następujące wiersze do pliku o nazwie *scores.csv* i Zapisz go w folderze projektu.</span><span class="sxs-lookup"><span data-stu-id="f8282-109">Copy the following lines into a file that is named *scores.csv* and save it to your project folder.</span></span> <span data-ttu-id="f8282-110">Plik reprezentuje dane arkusza kalkulacyjnego.</span><span class="sxs-lookup"><span data-stu-id="f8282-110">The file represents spreadsheet data.</span></span> <span data-ttu-id="f8282-111">Kolumna 1 jest IDENTYFIKATORem studenta, a kolumny od 2 do 5 są wynikami testów.</span><span class="sxs-lookup"><span data-stu-id="f8282-111">Column 1 is the student's ID, and columns 2 through 5 are test scores.</span></span>  
  
    ```csv  
    111, 97, 92, 81, 60  
    112, 75, 84, 91, 39  
    113, 88, 94, 65, 91  
    114, 97, 89, 85, 82  
    115, 35, 72, 91, 70  
    116, 99, 86, 90, 94  
    117, 93, 92, 80, 87  
    118, 92, 90, 83, 78  
    119, 68, 79, 88, 92  
    120, 99, 82, 81, 79  
    121, 96, 85, 91, 60  
    122, 94, 92, 91, 91  
    ```  
  
2. <span data-ttu-id="f8282-112">Skopiuj następujące wiersze do pliku o nazwie *names.csv* i Zapisz go w folderze projektu.</span><span class="sxs-lookup"><span data-stu-id="f8282-112">Copy the following lines into a file that is named *names.csv* and save it to your project folder.</span></span> <span data-ttu-id="f8282-113">Ten plik reprezentuje arkusz kalkulacyjny zawierający nazwisko, imię i nazwisko ucznia.</span><span class="sxs-lookup"><span data-stu-id="f8282-113">The file represents a spreadsheet that contains the student's last name, first name, and student ID.</span></span>  
  
    ```csv  
    Omelchenko,Svetlana,111  
    O'Donnell,Claire,112  
    Mortensen,Sven,113  
    Garcia,Cesar,114  
    Garcia,Debra,115  
    Fakhouri,Fadi,116  
    Feng,Hanying,117  
    Garcia,Hugo,118  
    Tucker,Lance,119  
    Adams,Terry,120  
    Zabokritski,Eugene,121  
    Tucker,Michael,122  
    ```  
  
## <a name="example"></a><span data-ttu-id="f8282-114">Przykład</span><span class="sxs-lookup"><span data-stu-id="f8282-114">Example</span></span>  

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

class JoinStrings  
{  
    static void Main()  
    {  
        // Join content from dissimilar files that contain  
        // related information. File names.csv contains the student  
        // name plus an ID number. File scores.csv contains the ID
        // and a set of four test scores. The following query joins  
        // the scores to the student names by using ID as a  
        // matching key.  
  
        string[] names = System.IO.File.ReadAllLines(@"../../../names.csv");  
        string[] scores = System.IO.File.ReadAllLines(@"../../../scores.csv");  
  
        // Name:    Last[0],       First[1],  ID[2]  
        //          Omelchenko,    Svetlana,  11  
        // Score:   StudentID[0],  Exam1[1]   Exam2[2],  Exam3[3],  Exam4[4]  
        //          111,           97,        92,        81,        60  
  
        // This query joins two dissimilar spreadsheets based on common ID value.  
        // Multiple from clauses are used instead of a join clause  
        // in order to store results of id.Split.  
        IEnumerable<string> scoreQuery1 =  
            from name in names  
            let nameFields = name.Split(',')  
            from id in scores  
            let scoreFields = id.Split(',')  
            where Convert.ToInt32(nameFields[2]) == Convert.ToInt32(scoreFields[0])
            select nameFields[0] + "," + scoreFields[1] + "," + scoreFields[2]
                   + "," + scoreFields[3] + "," + scoreFields[4];  
  
        // Pass a query variable to a method and execute it  
        // in the method. The query itself is unchanged.  
        OutputQueryResults(scoreQuery1, "Merge two spreadsheets:");  
  
        // Keep console window open in debug mode.  
        Console.WriteLine("Press any key to exit");  
        Console.ReadKey();  
    }  
  
    static void OutputQueryResults(IEnumerable<string> query, string message)  
    {  
        Console.WriteLine(System.Environment.NewLine + message);  
        foreach (string item in query)  
        {  
            Console.WriteLine(item);  
        }  
        Console.WriteLine("{0} total names in list", query.Count());  
    }  
}  
/* Output:  
Merge two spreadsheets:
Omelchenko, 97, 92, 81, 60
O'Donnell, 75, 84, 91, 39
Mortensen, 88, 94, 65, 91
Garcia, 97, 89, 85, 82
Garcia, 35, 72, 91, 70
Fakhouri, 99, 86, 90, 94
Feng, 93, 92, 80, 87
Garcia, 92, 90, 83, 78
Tucker, 68, 79, 88, 92
Adams, 99, 82, 81, 79
Zabokritski, 96, 85, 91, 60
Tucker, 94, 92, 91, 91
12 total names in list
 */  
```

## <a name="see-also"></a><span data-ttu-id="f8282-115">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="f8282-115">See also</span></span>

- [<span data-ttu-id="f8282-116">LINQ i ciągi (C#)</span><span class="sxs-lookup"><span data-stu-id="f8282-116">LINQ and Strings (C#)</span></span>](./linq-and-strings.md)
- [<span data-ttu-id="f8282-117">LINQ i katalogi plików (C#)</span><span class="sxs-lookup"><span data-stu-id="f8282-117">LINQ and File Directories (C#)</span></span>](./linq-and-file-directories.md)
