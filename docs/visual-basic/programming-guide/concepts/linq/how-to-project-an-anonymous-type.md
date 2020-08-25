---
title: 'Instrukcje: projektowanie typu anonimowego'
ms.date: 07/20/2015
ms.assetid: 30b42987-0e0e-4b2b-adb1-5255ddfbcd7b
ms.openlocfilehash: c486fbd7ee8ae917cd0ccf57e2b04e472784b11d
ms.sourcegitcommit: 9c45035b781caebc63ec8ecf912dc83fb6723b1f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/25/2020
ms.locfileid: "88810563"
---
# <a name="how-to-project-an-anonymous-type-visual-basic"></a><span data-ttu-id="adc00-102">Instrukcje: projekt typu anonimowego (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="adc00-102">How to: Project an Anonymous Type (Visual Basic)</span></span>
<span data-ttu-id="adc00-103">W niektórych przypadkach warto zaprojektować zapytanie do nowego typu, nawet jeśli wiesz, że ten typ będzie używany tylko przez krótki czas.</span><span class="sxs-lookup"><span data-stu-id="adc00-103">In some cases you might want to project a query to a new type, even though you know you will only use this type for a short while.</span></span> <span data-ttu-id="adc00-104">Jest to wiele dodatkowych nakładów pracy, aby utworzyć nowy typ tylko do użycia w projekcji.</span><span class="sxs-lookup"><span data-stu-id="adc00-104">It is a lot of extra work to create a new type just to use in the projection.</span></span> <span data-ttu-id="adc00-105">Wydajniejszym rozwiązaniem w tym przypadku jest zaprojektowanie typu anonimowego.</span><span class="sxs-lookup"><span data-stu-id="adc00-105">A more efficient approach in this case is to project to an anonymous type.</span></span> <span data-ttu-id="adc00-106">Typy anonimowe umożliwiają zdefiniowanie klasy, a następnie zadeklarowanie i zainicjowanie obiektu tej klasy bez podawania nazwy klasy.</span><span class="sxs-lookup"><span data-stu-id="adc00-106">Anonymous types allow you to define a class, then declare and initialize an object of that class, without giving the class a name.</span></span>  
  
 <span data-ttu-id="adc00-107">Typy anonimowe to implementacja języka C# koncepcji matematycznej *krotki*.</span><span class="sxs-lookup"><span data-stu-id="adc00-107">Anonymous types are the C# implementation of the mathematical concept of a *tuple*.</span></span> <span data-ttu-id="adc00-108">"Wyrażenie matematyczne" pochodziło z sekwencji pojedynczej, podwójnej, potrójnej, czterokrotnej, Quintuple, n-krotki.</span><span class="sxs-lookup"><span data-stu-id="adc00-108">The mathematical term tuple originated from the sequence single, double, triple, quadruple, quintuple, n-tuple.</span></span> <span data-ttu-id="adc00-109">Odnosi się do skończonej sekwencji obiektów, każdego określonego typu.</span><span class="sxs-lookup"><span data-stu-id="adc00-109">It refers to a finite sequence of objects, each of a specific type.</span></span> <span data-ttu-id="adc00-110">Czasami jest to nazywane listą par nazwa/wartość.</span><span class="sxs-lookup"><span data-stu-id="adc00-110">Sometimes this is called a list of name/value pairs.</span></span> <span data-ttu-id="adc00-111">Na przykład zawartość adresu w [przykładowym pliku XML: typowy dokument XML zamówienia zakupu (LINQ to XML)](sample-xml-file-typical-purchase-order-linq-to-xml.md) można wyrazić w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="adc00-111">For example, the contents of an address in the [Sample XML File: Typical Purchase Order (LINQ to XML)](sample-xml-file-typical-purchase-order-linq-to-xml.md) XML document could be expressed as follows:</span></span>  
  
```
Name: Ellen Adams  
Street: 123 Maple Street  
City: Mill Valley  
State: CA  
Zip: 90952  
Country: USA  
```  
  
 <span data-ttu-id="adc00-112">Podczas tworzenia wystąpienia typu anonimowego, wygodnie jest go traktować jak tworzenie spójnej kolekcji Order n.</span><span class="sxs-lookup"><span data-stu-id="adc00-112">When you create an instance of an anonymous type, it is convenient to think of it as creating a tuple of order n.</span></span> <span data-ttu-id="adc00-113">Jeśli napiszesz zapytanie, które tworzy krotkę w `Select` klauzuli, zapytanie zwraca `IEnumerable` kolekcję.</span><span class="sxs-lookup"><span data-stu-id="adc00-113">If you write a query that creates a tuple in the `Select` clause, the query returns an `IEnumerable` of the tuple.</span></span>  
  
## <a name="example"></a><span data-ttu-id="adc00-114">Przykład</span><span class="sxs-lookup"><span data-stu-id="adc00-114">Example</span></span>  
 <span data-ttu-id="adc00-115">W tym przykładzie `Select` klauzula projektuje typ anonimowy.</span><span class="sxs-lookup"><span data-stu-id="adc00-115">In this example, the `Select` clause projects an anonymous type.</span></span> <span data-ttu-id="adc00-116">Przykład używa `Dim` do tworzenia `IEnumerable` obiektu.</span><span class="sxs-lookup"><span data-stu-id="adc00-116">The example then uses `Dim` to create the `IEnumerable` object.</span></span> <span data-ttu-id="adc00-117">W `For Each` pętli Zmienna iteracji zostaje wystąpieniem typu anonimowego utworzonego w wyrażeniu zapytania.</span><span class="sxs-lookup"><span data-stu-id="adc00-117">Within the `For Each` loop, the iteration variable becomes an instance of the anonymous type created in the query expression.</span></span>  
  
 <span data-ttu-id="adc00-118">W tym przykładzie zastosowano następujący dokument XML: [przykładowy plik XML: Customers i Orders (LINQ to XML)](sample-xml-file-customers-and-orders-linq-to-xml.md).</span><span class="sxs-lookup"><span data-stu-id="adc00-118">This example uses the following XML document: [Sample XML File: Customers and Orders (LINQ to XML)](sample-xml-file-customers-and-orders-linq-to-xml.md).</span></span>  
  
```vb  
Dim custOrd As XElement = XElement.Load("CustomersOrders.xml")  
Dim custList = _  
    From el In custOrd.<Customers>.<Customer> _  
    Select New With { _  
        .CustomerID = el.@<CustomerID>, _  
        .CompanyName = el.<CompanyName>.Value, _  
        .ContactName = el.<ContactName>.Value _  
    }  
For Each cust In custList  
    Console.WriteLine("{0}:{1}:{2}", cust.CustomerID, cust.CompanyName, cust.ContactName)  
Next  
```  
  
 <span data-ttu-id="adc00-119">Ten kod spowoduje wygenerowanie następujących danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="adc00-119">This code produces the following output:</span></span>  
  
```console  
GREAL:Great Lakes Food Market:Howard Snyder  
HUNGC:Hungry Coyote Import Store:Yoshi Latimer  
LAZYK:Lazy K Kountry Store:John Steel  
LETSS:Let's Stop N Shop:Jaime Yorres  
```  
  
## <a name="see-also"></a><span data-ttu-id="adc00-120">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="adc00-120">See also</span></span>

- [<span data-ttu-id="adc00-121">Projekcje i przekształcenia (LINQ to XML) (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="adc00-121">Projections and Transformations (LINQ to XML) (Visual Basic)</span></span>](projections-and-transformations-linq-to-xml.md)
