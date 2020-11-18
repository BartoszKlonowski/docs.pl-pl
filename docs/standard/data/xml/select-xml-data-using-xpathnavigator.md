---
title: Wybieranie danych XML przy użyciu klasy XPathNavigator
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: c268c49e-32b9-4171-b782-dcb7b065fa73
ms.openlocfilehash: 791c1d16db6a2079ccccebf4dc33d5a0eb12d3c5
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94824977"
---
# <a name="select-xml-data-using-xpathnavigator"></a><span data-ttu-id="4d098-102">Wybieranie danych XML przy użyciu klasy XPathNavigator</span><span class="sxs-lookup"><span data-stu-id="4d098-102">Select XML Data Using XPathNavigator</span></span>
<span data-ttu-id="4d098-103"><xref:System.Xml.XPath.XPathNavigator>Klasa zawiera zestaw metod służących do wybierania zestawu węzłów w <xref:System.Xml.XPath.XPathDocument> <xref:System.Xml.XmlDocument> obiekcie lub przy użyciu wyrażenia XPath.</span><span class="sxs-lookup"><span data-stu-id="4d098-103">The <xref:System.Xml.XPath.XPathNavigator> class provides a set of methods used to select a set of nodes in an <xref:System.Xml.XPath.XPathDocument> or <xref:System.Xml.XmlDocument> object using an XPath expression.</span></span> <span data-ttu-id="4d098-104">Po wybraniu można wykonać iterację w wybranym zestawie węzłów.</span><span class="sxs-lookup"><span data-stu-id="4d098-104">Once selected, you can iterate over the selected set of nodes.</span></span>  
  
## <a name="xpathnavigator-selection-methods"></a><span data-ttu-id="4d098-105">Metody wyboru XPathNavigator</span><span class="sxs-lookup"><span data-stu-id="4d098-105">XPathNavigator Selection Methods</span></span>  
 <span data-ttu-id="4d098-106"><xref:System.Xml.XPath.XPathNavigator>Klasa zawiera zestaw metod służących do wybierania zestawu węzłów w <xref:System.Xml.XPath.XPathDocument> <xref:System.Xml.XmlDocument> obiekcie lub przy użyciu wyrażenia XPath.</span><span class="sxs-lookup"><span data-stu-id="4d098-106">The <xref:System.Xml.XPath.XPathNavigator> class provides a set of methods used to select a set of nodes in an <xref:System.Xml.XPath.XPathDocument> or <xref:System.Xml.XmlDocument> object using an XPath expression.</span></span> <span data-ttu-id="4d098-107"><xref:System.Xml.XPath.XPathNavigator>Klasa udostępnia również zestaw zoptymalizowanych metod do wybierania obiektów nadrzędnych, podrzędnych i podrzędnych szybciej niż przy użyciu wyrażenia XPath.</span><span class="sxs-lookup"><span data-stu-id="4d098-107">The <xref:System.Xml.XPath.XPathNavigator> class also provides a set of optimized methods for selecting ancestor, child and descendant nodes faster than using an XPath expression.</span></span> <span data-ttu-id="4d098-108">Wybrany zestaw węzłów jest zwracany w <xref:System.Xml.XPath.XPathNodeIterator> obiekcie lub <xref:System.Xml.XPath.XPathNavigator> obiekcie w przypadku pojedynczego wybranego węzła.</span><span class="sxs-lookup"><span data-stu-id="4d098-108">The selected set of nodes is returned in an <xref:System.Xml.XPath.XPathNodeIterator> object or an <xref:System.Xml.XPath.XPathNavigator> object in the case of a single selected node.</span></span>  
  
### <a name="selecting-nodes-using-xpath-expressions"></a><span data-ttu-id="4d098-109">Wybieranie węzłów przy użyciu wyrażeń XPath</span><span class="sxs-lookup"><span data-stu-id="4d098-109">Selecting Nodes Using XPath Expressions</span></span>  
 <span data-ttu-id="4d098-110">Aby wybrać zestaw węzłów za pomocą wyrażenia XPath, należy użyć jednej z następujących metod wyboru.</span><span class="sxs-lookup"><span data-stu-id="4d098-110">To select a set of nodes using an XPath expression, use one of the following selection methods.</span></span>  
  
- <xref:System.Xml.XPath.XPathNavigator.Select%2A>  
  
- <xref:System.Xml.XPath.XPathNavigator.SelectSingleNode%2A>  
  
 <span data-ttu-id="4d098-111">Po wywołaniu te metody zwracają zestaw węzłów, które można swobodnie nawigować przy użyciu <xref:System.Xml.XPath.XPathNodeIterator> obiektu lub <xref:System.Xml.XPath.XPathNavigator> obiektu w przypadku jednego wybranego węzła.</span><span class="sxs-lookup"><span data-stu-id="4d098-111">When called, these methods return a set of nodes that you can navigate freely using an <xref:System.Xml.XPath.XPathNodeIterator> object or an <xref:System.Xml.XPath.XPathNavigator> object in the case of a single selected node.</span></span>  
  
 <span data-ttu-id="4d098-112">Nawigowanie przy użyciu <xref:System.Xml.XPath.XPathNodeIterator> obiektu nie ma wpływu na pozycję obiektu, który <xref:System.Xml.XPath.XPathNavigator> został użyty do jego utworzenia.</span><span class="sxs-lookup"><span data-stu-id="4d098-112">Navigating with an <xref:System.Xml.XPath.XPathNodeIterator> object does not affect the position of the <xref:System.Xml.XPath.XPathNavigator> object used to create it.</span></span> <span data-ttu-id="4d098-113"><xref:System.Xml.XPath.XPathNavigator>Obiekt zwrócony z <xref:System.Xml.XPath.XPathNavigator.SelectSingleNode%2A> metod jest umieszczony w pojedynczym zwracanym węźle, a także nie ma wpływu na pozycję obiektu, który został <xref:System.Xml.XPath.XPathNavigator> użyty do jego utworzenia.</span><span class="sxs-lookup"><span data-stu-id="4d098-113">The <xref:System.Xml.XPath.XPathNavigator> object returned from the <xref:System.Xml.XPath.XPathNavigator.SelectSingleNode%2A> methods is positioned on the single returned node and also does not affect the position of the <xref:System.Xml.XPath.XPathNavigator> object used to create it.</span></span>  
  
 <span data-ttu-id="4d098-114">W poniższym przykładzie pokazano tworzenie <xref:System.Xml.XPath.XPathNavigator> obiektu z <xref:System.Xml.XPath.XPathDocument> obiektu, użycie <xref:System.Xml.XPath.XPathNavigator.Select%2A> metody w celu wybrania węzłów w <xref:System.Xml.XPath.XPathDocument> obiekcie i użycie <xref:System.Xml.XPath.XPathNodeIterator> obiektu do iteracji w wybranych węzłach.</span><span class="sxs-lookup"><span data-stu-id="4d098-114">The following example shows the creation of an <xref:System.Xml.XPath.XPathNavigator> object from an <xref:System.Xml.XPath.XPathDocument> object, the use of the <xref:System.Xml.XPath.XPathNavigator.Select%2A> method to select nodes in the <xref:System.Xml.XPath.XPathDocument> object, and the use of the <xref:System.Xml.XPath.XPathNodeIterator> object to iterate over the selected nodes.</span></span>  
  
```vb  
Dim document As XPathDocument = New XPathDocument("books.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
Dim nodes As XPathNodeIterator = navigator.Select("/bookstore/book")  
  
While nodes.MoveNext()  
    Console.WriteLine(nodes.Current.Name)  
End While  
```  
  
```csharp  
XPathDocument document = new XPathDocument("books.xml");  
XPathNavigator navigator = document.CreateNavigator();  
XPathNodeIterator nodes = navigator.Select("/bookstore/book");  
  
while(nodes.MoveNext())  
{  
    Console.WriteLine(nodes.Current.Name);  
}  
```  
  
 <span data-ttu-id="4d098-115">Przykład pobiera `books.xml` plik jako dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="4d098-115">The example takes the `books.xml` file as input.</span></span>  
  
 [!code-xml[XPathXMLExamples#1](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/books.xml#1)]  
  
### <a name="optimized-selection-methods"></a><span data-ttu-id="4d098-116">Zoptymalizowane metody zaznaczania</span><span class="sxs-lookup"><span data-stu-id="4d098-116">Optimized Selection Methods</span></span>  
 <span data-ttu-id="4d098-117"><xref:System.Xml.XPath.XPathNavigator.SelectChildren%2A>Metody, <xref:System.Xml.XPath.XPathNavigator.SelectAncestors%2A> , i <xref:System.Xml.XPath.XPathNavigator.SelectDescendants%2A> <xref:System.Xml.XPath.XPathNavigator> klasy reprezentują wyrażenia XPath często używane do pobierania węzłów podrzędnych, podrzędnych i nadrzędnych.</span><span class="sxs-lookup"><span data-stu-id="4d098-117">The <xref:System.Xml.XPath.XPathNavigator.SelectChildren%2A>, <xref:System.Xml.XPath.XPathNavigator.SelectAncestors%2A>, and <xref:System.Xml.XPath.XPathNavigator.SelectDescendants%2A> methods of the <xref:System.Xml.XPath.XPathNavigator> class represent XPath expressions commonly used to retrieve child, descendant, and ancestor nodes.</span></span> <span data-ttu-id="4d098-118">Te metody są zoptymalizowane pod kątem wydajności i są szybsze niż odpowiednie wyrażenia XPath.</span><span class="sxs-lookup"><span data-stu-id="4d098-118">These methods are optimized for performance and are faster than their corresponding XPath expressions.</span></span> <span data-ttu-id="4d098-119"><xref:System.Xml.XPath.XPathNavigator.SelectChildren%2A>Metody, <xref:System.Xml.XPath.XPathNavigator.SelectAncestors%2A> , i <xref:System.Xml.XPath.XPathNavigator.SelectDescendants%2A> wybierają węzły nadrzędne, podrzędne i podrzędne na podstawie <xref:System.Xml.XPath.XPathNodeType> wartości lub nazwy lokalnej i identyfikatora URI przestrzeni nazw węzłów do wybrania.</span><span class="sxs-lookup"><span data-stu-id="4d098-119">The <xref:System.Xml.XPath.XPathNavigator.SelectChildren%2A>, <xref:System.Xml.XPath.XPathNavigator.SelectAncestors%2A>, and <xref:System.Xml.XPath.XPathNavigator.SelectDescendants%2A> methods selects ancestor, child, and descendant nodes based on an <xref:System.Xml.XPath.XPathNodeType> value or the local name and namespace URI of the nodes to select.</span></span> <span data-ttu-id="4d098-120">Wybrane węzły nadrzędne, podrzędne i podrzędne są zwracane w <xref:System.Xml.XPath.XPathNodeIterator> obiekcie.</span><span class="sxs-lookup"><span data-stu-id="4d098-120">The selected ancestor, child, and descendant nodes are returned in an <xref:System.Xml.XPath.XPathNodeIterator> object.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="4d098-121">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="4d098-121">See also</span></span>

- <xref:System.Xml.XmlDocument>
- <xref:System.Xml.XPath.XPathDocument>
- <xref:System.Xml.XPath.XPathNavigator>
- [<span data-ttu-id="4d098-122">Przetwarzanie danych XML przy użyciu modelu danych XPath</span><span class="sxs-lookup"><span data-stu-id="4d098-122">Process XML Data Using the XPath Data Model</span></span>](process-xml-data-using-the-xpath-data-model.md)
- [<span data-ttu-id="4d098-123">Obliczanie wyrażeń XPath przy użyciu klasy XPathNavigator</span><span class="sxs-lookup"><span data-stu-id="4d098-123">Evaluate XPath Expressions using XPathNavigator</span></span>](evaluate-xpath-expressions-using-xpathnavigator.md)
- [<span data-ttu-id="4d098-124">Dopasowywanie węzłów przy użyciu klasy XPathNavigator</span><span class="sxs-lookup"><span data-stu-id="4d098-124">Matching Nodes using XPathNavigator</span></span>](matching-nodes-using-xpathnavigator.md)
- [<span data-ttu-id="4d098-125">Typy węzłów rozpoznawanych w zapytaniach XPath</span><span class="sxs-lookup"><span data-stu-id="4d098-125">Node Types Recognized with XPath Queries</span></span>](node-types-recognized-with-xpath-queries.md)
- [<span data-ttu-id="4d098-126">Zapytania XPath i przestrzenie nazw</span><span class="sxs-lookup"><span data-stu-id="4d098-126">XPath Queries and Namespaces</span></span>](xpath-queries-and-namespaces.md)
- [<span data-ttu-id="4d098-127">Skompilowane wyrażenia XPath</span><span class="sxs-lookup"><span data-stu-id="4d098-127">Compiled XPath Expressions</span></span>](compiled-xpath-expressions.md)
