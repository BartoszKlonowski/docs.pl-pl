---
title: Jak zapisywać zapytania w języku XML w przestrzeniach nazw (C#)
ms.date: 07/20/2015
ms.assetid: 7c54df81-15e4-4091-8c81-a87637029130
ms.openlocfilehash: a8b8d55daaad1ae00e43fed897080ed7a62fafab
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/14/2020
ms.locfileid: "75337373"
---
# <a name="how-to-write-queries-on-xml-in-namespaces-c"></a><span data-ttu-id="41d58-102">Jak zapisywać zapytania w języku XML w przestrzeniach nazw (C#)</span><span class="sxs-lookup"><span data-stu-id="41d58-102">How to write queries on XML in namespaces (C#)</span></span>
<span data-ttu-id="41d58-103">Aby napisać kwerendę w xml, który znajduje <xref:System.Xml.Linq.XName> się w obszarze nazw, należy użyć obiektów, które mają poprawny obszar nazw.</span><span class="sxs-lookup"><span data-stu-id="41d58-103">To write a query on XML that is in a namespace, you must use <xref:System.Xml.Linq.XName> objects that have the correct namespace.</span></span>  
  
 <span data-ttu-id="41d58-104">W przypadku języka C#najczęstszym podejściem <xref:System.Xml.Linq.XNamespace> jest zainicjowanie ciągu zawierającego identyfikator URI, a następnie połączenie obszaru nazw z nazwą lokalną za pomocą operatora dodawania.</span><span class="sxs-lookup"><span data-stu-id="41d58-104">For C#, the most common approach is to initialize an <xref:System.Xml.Linq.XNamespace> using a string that contains the URI, then use the addition operator overload to combine the namespace with the local name.</span></span>  
  
 <span data-ttu-id="41d58-105">Pierwszy zestaw przykładów w tym temacie pokazuje, jak utworzyć drzewo XML w domyślnym obszarze nazw.</span><span class="sxs-lookup"><span data-stu-id="41d58-105">The first set of examples in this topic shows how to create an XML tree in a default namespace.</span></span> <span data-ttu-id="41d58-106">Drugi zestaw pokazuje, jak utworzyć drzewo XML w przestrzeni nazw z prefiksem.</span><span class="sxs-lookup"><span data-stu-id="41d58-106">The second set shows how to create an XML tree in a namespace with a prefix.</span></span>  
  
## <a name="example"></a><span data-ttu-id="41d58-107">Przykład</span><span class="sxs-lookup"><span data-stu-id="41d58-107">Example</span></span>  
 <span data-ttu-id="41d58-108">Poniższy przykład tworzy drzewo XML, który znajduje się w domyślnym obszarze nazw.</span><span class="sxs-lookup"><span data-stu-id="41d58-108">The following example creates an XML tree that is in a default namespace.</span></span> <span data-ttu-id="41d58-109">Następnie pobiera kolekcję elementów.</span><span class="sxs-lookup"><span data-stu-id="41d58-109">It then retrieves a collection of elements.</span></span>  
  
```csharp  
XNamespace aw = "http://www.adventure-works.com";  
XElement root = XElement.Parse(  
@"<Root xmlns='http://www.adventure-works.com'>  
    <Child>1</Child>  
    <Child>2</Child>  
    <Child>3</Child>  
    <AnotherChild>4</AnotherChild>  
    <AnotherChild>5</AnotherChild>  
    <AnotherChild>6</AnotherChild>  
</Root>");  
IEnumerable<XElement> c1 =  
    from el in root.Elements(aw + "Child")  
    select el;  
foreach (XElement el in c1)  
    Console.WriteLine((int)el);  
```  
  
 <span data-ttu-id="41d58-110">Ten przykład generuje następujące wyniki:</span><span class="sxs-lookup"><span data-stu-id="41d58-110">This example produces the following output:</span></span>  
  
```output  
1  
2  
3  
```  
  
## <a name="example"></a><span data-ttu-id="41d58-111">Przykład</span><span class="sxs-lookup"><span data-stu-id="41d58-111">Example</span></span>  
 <span data-ttu-id="41d58-112">W języku C#, kwerendy są pisane w ten sam sposób, niezależnie od tego, czy piszesz zapytania w drzewie XML, który używa obszaru nazw z prefiksem, czy na drzewie XML z domyślnym obszarem nazw.</span><span class="sxs-lookup"><span data-stu-id="41d58-112">In C#, you write queries in the same way regardless of whether you are writing queries on an XML tree that uses a namespace with a prefix or on an XML tree with a default namespace.</span></span>  
  
 <span data-ttu-id="41d58-113">Poniższy przykład tworzy drzewo XML, który znajduje się w przestrzeni nazw z prefiksem.</span><span class="sxs-lookup"><span data-stu-id="41d58-113">The following example creates an XML tree that is in a namespace with a prefix.</span></span> <span data-ttu-id="41d58-114">Następnie pobiera kolekcję elementów.</span><span class="sxs-lookup"><span data-stu-id="41d58-114">It then retrieves a collection of elements.</span></span>  
  
```csharp  
XNamespace aw = "http://www.adventure-works.com";  
XElement root = XElement.Parse(  
@"<aw:Root xmlns:aw='http://www.adventure-works.com'>  
    <aw:Child>1</aw:Child>  
    <aw:Child>2</aw:Child>  
    <aw:Child>3</aw:Child>  
    <aw:AnotherChild>4</aw:AnotherChild>  
    <aw:AnotherChild>5</aw:AnotherChild>  
    <aw:AnotherChild>6</aw:AnotherChild>  
</aw:Root>");  
IEnumerable<XElement> c1 =  
    from el in root.Elements(aw + "Child")  
    select el;  
foreach (XElement el in c1)  
    Console.WriteLine((int)el);  
```  
  
 <span data-ttu-id="41d58-115">Ten przykład generuje następujące wyniki:</span><span class="sxs-lookup"><span data-stu-id="41d58-115">This example produces the following output:</span></span>  
  
```output  
1  
2  
3  
```  
  
## <a name="see-also"></a><span data-ttu-id="41d58-116">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="41d58-116">See also</span></span>

- [<span data-ttu-id="41d58-117">Omówienie przestrzeni nazw (LINQ do XML) (C#)</span><span class="sxs-lookup"><span data-stu-id="41d58-117">Namespaces Overview (LINQ to XML) (C#)</span></span>](namespaces-overview-linq-to-xml.md)
