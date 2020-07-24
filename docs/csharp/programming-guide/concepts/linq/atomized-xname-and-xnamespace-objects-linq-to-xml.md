---
title: Atomed XName and XNamespace Objects (LINQ to XML) (C#)
description: Dowiedz się więcej o rozproszonych obiektach XName i XNamespace oraz sposobie zapewniania korzyści z wydajności dla zapytań.
ms.date: 07/20/2015
ms.assetid: a5b21433-b49d-415c-b00e-bcbfb0d267d7
ms.openlocfilehash: 305a233adab5c860b5f9509ae25ccc5d633e7957
ms.sourcegitcommit: 04022ca5d00b2074e1b1ffdbd76bec4950697c4c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/23/2020
ms.locfileid: "87104277"
---
# <a name="atomized-xname-and-xnamespace-objects-linq-to-xml-c"></a>Atomed XName and XNamespace Objects (LINQ to XML) (C#)
<xref:System.Xml.Linq.XName>i <xref:System.Xml.Linq.XNamespace> obiekty są *atomowe*; oznacza to, że jeśli zawierają one taką samą kwalifikowaną nazwę, odwołują się do tego samego obiektu. Zapewnia to korzyści z wydajności dla zapytań: w przypadku porównania dwóch nazw atomowych dla równości, podstawowy język pośredni musi określić, czy te dwa odwołania wskazują na ten sam obiekt. Kod źródłowy nie musi wykonywać porównań ciągów, co byłoby czasochłonne.  
  
## <a name="atomization-semantics"></a>Semantyka rozproszenie  
 Rozproszenie oznacza, że jeśli dwa <xref:System.Xml.Linq.XName> obiekty mają tę samą nazwę lokalną i znajdują się w tej samej przestrzeni nazw, współużytkują to samo wystąpienie. W taki sam sposób, jeśli dwa <xref:System.Xml.Linq.XNamespace> obiekty mają ten sam identyfikator URI przestrzeni nazw, współużytkują to samo wystąpienie.  
  
 Aby można było włączyć obiekt Atoms, Konstruktor dla klasy musi być prywatny, a nie publiczny. Wynika to z faktu, że jeśli Konstruktor był publiczny, można utworzyć obiekt niebędący atomem. <xref:System.Xml.Linq.XName>Klasy i <xref:System.Xml.Linq.XNamespace> implementują Operator niejawnej konwersji w celu przekonwertowania ciągu na <xref:System.Xml.Linq.XName> lub <xref:System.Xml.Linq.XNamespace> . W ten sposób można uzyskać wystąpienie tych obiektów. Nie można uzyskać wystąpienia przy użyciu konstruktora, ponieważ Konstruktor jest niedostępny.  
  
 <xref:System.Xml.Linq.XName>a <xref:System.Xml.Linq.XNamespace> także zaimplementować operatory równości i nierówności, aby określić, czy dwa porównywane obiekty są odwołaniami do tego samego wystąpienia.  
  
## <a name="example"></a>Przykład  
 Poniższy kod tworzy niektóre <xref:System.Xml.Linq.XElement> obiekty i pokazuje, że identyczne nazwy współużytkują to samo wystąpienie.  
  
```csharp  
XElement r1 = new XElement("Root", "data1");  
XElement r2 = XElement.Parse("<Root>data2</Root>");  
  
if ((object)r1.Name == (object)r2.Name)  
    Console.WriteLine("r1 and r2 have names that refer to the same instance.");  
else  
    Console.WriteLine("Different");  
  
XName n = "Root";  
  
if ((object)n == (object)r1.Name)  
    Console.WriteLine("The name of r1 and the name in 'n' refer to the same instance.");  
else  
    Console.WriteLine("Different");  
```  
  
 Ten przykład generuje następujące wyniki:  
  
```output  
r1 and r2 have names that refer to the same instance.  
The name of r1 and the name in 'n' refer to the same instance.  
```  
  
 Jak wspomniano wcześniej, zaletą obiektów atomowych jest użycie jednej z metod osi, która przyjmuje <xref:System.Xml.Linq.XName> jako parametr, metoda osi ma tylko określić, że dwie nazwy odwołują się do tego samego wystąpienia w celu wybrania żądanych elementów.  
  
 Poniższy przykład przekazuje <xref:System.Xml.Linq.XName> <xref:System.Xml.Linq.XContainer.Descendants%2A> wywołanie metody, które następnie ma lepszą wydajność ze względu na wzorzec rozproszenie.  
  
```csharp  
XElement root = new XElement("Root",  
    new XElement("C1", 1),  
    new XElement("Z1",  
        new XElement("C1", 2),  
        new XElement("C1", 1)  
    )  
);  
  
var query = from e in root.Descendants("C1")  
            where (int)e == 1  
            select e;  
  
foreach (var z in query)  
    Console.WriteLine(z);  
```  
  
 Ten przykład generuje następujące wyniki:  
  
```xml  
<C1>1</C1>  
<C1>1</C1>  
```  
