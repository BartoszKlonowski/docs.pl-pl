---
title: Zapytania skompilowane statycznie (LINQ to XML) (C#)
description: Dowiedz się więcej na temat zakompilowanych statycznie zapytań w LINQ to XML w języku C# i różnice między zapytaniami XPath, które należy interpretować w czasie wykonywania.
ms.date: 07/20/2015
ms.assetid: 3bf558fe-0705-479d-86d4-00188f5fcf9c
ms.openlocfilehash: cd2e6a6507311d5fc17215a22c70bd0449292b6f
ms.sourcegitcommit: 6f58a5f75ceeb936f8ee5b786e9adb81a9a3bee9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/28/2020
ms.locfileid: "87302311"
---
# <a name="statically-compiled-queries-linq-to-xml-c"></a>Zapytania skompilowane statycznie (LINQ to XML) (C#)
Jedną z najważniejszych korzyści związanych z wydajnością LINQ to XML, w przeciwieństwie do programu <xref:System.Xml.XmlDocument> , jest to, że zapytania w LINQ to XML są kompilowane statycznie, podczas gdy zapytania XPath muszą być interpretowane w czasie wykonywania. Ta funkcja jest wbudowana w LINQ to XML, więc nie trzeba wykonywać dodatkowych czynności, aby korzystać z nich, ale warto zrozumieć rozróżnienie podczas wybierania dwóch technologii. W tym temacie opisano różnicę.  
  
## <a name="statically-compiled-queries-vs-xpath"></a>Zapytania skompilowane statycznie a XPath  
 Poniższy przykład pokazuje, jak uzyskać elementy podrzędne o określonej nazwie i z atrybutem o określonej wartości.  
  
 Poniżej znajduje się równoważne wyrażenie XPath:`//Address[@Type='Shipping']`
  
```csharp  
XDocument po = XDocument.Load("PurchaseOrders.xml");  
  
IEnumerable<XElement> list1 =  
    from el in po.Descendants("Address")  
    where (string)el.Attribute("Type") == "Shipping"  
    select el;  
  
foreach (XElement el in list1)  
    Console.WriteLine(el);  
```  
  
 Wyrażenie zapytania w tym przykładzie jest ponownie zapisywane przez kompilator do składni zapytania opartej na metodzie. Poniższy przykład, który został zapisany w składni zapytania opartej na metodzie, daje takie same wyniki jak poprzedni:  
  
```csharp  
XDocument po = XDocument.Load("PurchaseOrders.xml");  
  
IEnumerable<XElement> list1 =  
    po  
    .Descendants("Address")  
    .Where(el => (string)el.Attribute("Type") == "Shipping");  
  
foreach (XElement el in list1)  
    Console.WriteLine(el);  
```  
  
 <xref:System.Linq.Enumerable.Where%2A>Metoda jest metodą rozszerzenia. Aby uzyskać więcej informacji, zobacz [metody rozszerzenia](../../classes-and-structs/extension-methods.md). Ponieważ <xref:System.Linq.Enumerable.Where%2A> jest to metoda rozszerzająca, zapytanie powyżej zostało skompilowane tak, jakby było zapisywane w następujący sposób:  
  
```csharp  
XDocument po = XDocument.Load("PurchaseOrders.xml");  
  
IEnumerable<XElement> list1 =  
    System.Linq.Enumerable.Where(  
        po.Descendants("Address"),  
        el => (string)el.Attribute("Type") == "Shipping");  
  
foreach (XElement el in list1)  
    Console.WriteLine(el);  
```  
  
 Ten przykład daje dokładnie te same wyniki co dwa poprzednie przykłady. Ilustruje to fakt, że zapytania są efektywnie kompilowane na wywołania metod połączonych statycznie. W połączeniu z odroczoną semantyką wykonywania iteratorów, zwiększa wydajność. Aby uzyskać więcej informacji o odroczonej semantyki wykonywania iteratorów, zobacz [odroczone wykonywanie i obliczanie z opóźnieniem w LINQ to XML (C#)](./deferred-execution-and-lazy-evaluation-in-linq-to-xml.md).  
  
> [!NOTE]
> Te przykłady są reprezentatywne dla kodu, który kompilator może napisać. Rzeczywista implementacja może się nieco różnić od tych przykładów, ale wydajność będzie taka sama lub podobna do tych przykładów.  
  
## <a name="executing-xpath-expressions-with-xmldocument"></a>Wykonywanie wyrażeń XPath przy użyciu elementu XmlDocument  
 Poniższy przykład używa <xref:System.Xml.XmlDocument> , aby wykonać te same wyniki co w poprzednich przykładach:  
  
```csharp  
XmlReader reader = XmlReader.Create("PurchaseOrders.xml");  
XmlDocument doc = new XmlDocument();  
doc.Load(reader);  
XmlNodeList nl = doc.SelectNodes(".//Address[@Type='Shipping']");  
foreach (XmlNode n in nl)  
    Console.WriteLine(n.OuterXml);  
reader.Close();  
```  
  
 To zapytanie zwraca te same dane wyjściowe jak przykłady, które używają LINQ to XML; Jedyną różnicą jest to, że LINQ to XML wcięcia drukowanego kodu XML, a nie <xref:System.Xml.XmlDocument> .  
  
 Jednakże <xref:System.Xml.XmlDocument> podejście zwykle nie wykonuje ani LINQ to XML, ponieważ <xref:System.Xml.XmlNode.SelectNodes%2A> Metoda musi wykonać wewnętrznie przy każdym wywołaniu:  
  
- Analizuje ciąg zawierający wyrażenie XPath, dzieląc ciąg na tokeny.  
  
- Sprawdza tokeny, aby upewnić się, że wyrażenie XPath jest prawidłowe.  
  
- Tłumaczy wyrażenie na wewnętrzne drzewo wyrażeń.  
  
- Wykonuje iterację w węzłach, odpowiednio wybierając węzły dla zestawu wyników na podstawie oceny wyrażenia.  
  
 Jest to znacznie więcej niż pracy wykonanej przez odpowiednie LINQ to XML zapytanie. Określona różnica wydajności różni się w zależności od różnych typów zapytań, ale w ogólnych zapytaniach LINQ to XML wykonuje mniej pracy i w związku z tym wykonuje lepsze, niż ocenianie wyrażeń XPath przy użyciu <xref:System.Xml.XmlDocument> .  
