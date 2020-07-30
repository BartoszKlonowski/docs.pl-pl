---
title: Wykonywanie zapytania dotyczącego elementu XDocument a zapytania dotyczącego elementu XElement (C#)
description: Dowiedz się więcej o różnicach między wykonywaniem zapytań dotyczących elementu XDocument i wykonywaniem zapytania dotyczącego elementu XElement. Zapoznaj się z przykładami kodu, które przedstawiają te różnice.
ms.date: 07/20/2015
ms.assetid: 46221ff5-62ee-4de8-93ba-66465facb5c1
ms.openlocfilehash: 0c81768f06148308a639f96f4041e464b24edd33
ms.sourcegitcommit: 6f58a5f75ceeb936f8ee5b786e9adb81a9a3bee9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/28/2020
ms.locfileid: "87300322"
---
# <a name="querying-an-xdocument-vs-querying-an-xelement-c"></a>Wykonywanie zapytania dotyczącego elementu XDocument a zapytania dotyczącego elementu XElement (C#)
Podczas ładowania dokumentu za pośrednictwem programu należy <xref:System.Xml.Linq.XDocument.Load%2A?displayProperty=nameWithType> zauważyć, że trzeba pisać zapytania nieco inaczej niż podczas ładowania za pośrednictwem <xref:System.Xml.Linq.XElement.Load%2A?displayProperty=nameWithType> .  
  
## <a name="comparison-of-xdocumentload-and-xelementload"></a>Porównanie elementów XDocument. Load i XElement. Load  
 Podczas ładowania dokumentu XML do elementu <xref:System.Xml.Linq.XElement> za pośrednictwem <xref:System.Xml.Linq.XElement.Load%2A?displayProperty=nameWithType> <xref:System.Xml.Linq.XElement> katalog główny drzewa XML zawiera element główny załadowanego dokumentu. Jednak podczas ładowania tego samego dokumentu XML do elementu <xref:System.Xml.Linq.XDocument> za pośrednictwem <xref:System.Xml.Linq.XDocument.Load%2A?displayProperty=nameWithType> katalog główny drzewa jest <xref:System.Xml.Linq.XDocument> węzłem, a głównym elementem załadowanego dokumentu jest jeden dozwolony <xref:System.Xml.Linq.XElement> węzeł podrzędny <xref:System.Xml.Linq.XDocument> . [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]Osie działają względem węzła głównego.  
  
 Ten pierwszy przykład ładuje drzewo XML przy użyciu <xref:System.Xml.Linq.XElement.Load%2A> . Następnie wykonuje zapytanie dotyczące elementów podrzędnych katalogu głównego drzewa.  
  
```csharp  
// Create a simple document and write it to a file  
File.WriteAllText("Test.xml", @"<Root>  
    <Child1>1</Child1>  
    <Child2>2</Child2>  
    <Child3>3</Child3>  
</Root>");  
  
Console.WriteLine("Querying tree loaded with XElement.Load");  
Console.WriteLine("----");  
XElement doc = XElement.Load("Test.xml");  
IEnumerable<XElement> childList =  
    from el in doc.Elements()  
    select el;  
foreach (XElement e in childList)  
    Console.WriteLine(e);  
```  
  
 Zgodnie z oczekiwaniami ten przykład generuje następujące dane wyjściowe:  
  
```output  
Querying tree loaded with XElement.Load  
----  
<Child1>1</Child1>  
<Child2>2</Child2>  
<Child3>3</Child3>  
```  
  
 Poniższy przykład jest taki sam jak powyżej, z wyjątkiem tego, że drzewo XML jest załadowane do elementu <xref:System.Xml.Linq.XDocument> zamiast <xref:System.Xml.Linq.XElement> .  
  
```csharp  
// Create a simple document and write it to a file  
File.WriteAllText("Test.xml", @"<Root>  
    <Child1>1</Child1>  
    <Child2>2</Child2>  
    <Child3>3</Child3>  
</Root>");  
  
Console.WriteLine("Querying tree loaded with XDocument.Load");  
Console.WriteLine("----");  
XDocument doc = XDocument.Load("Test.xml");  
IEnumerable<XElement> childList =  
    from el in doc.Elements()  
    select el;  
foreach (XElement e in childList)  
    Console.WriteLine(e);  
```  
  
 Ten przykład generuje następujące wyniki:  
  
```output  
Querying tree loaded with XDocument.Load  
----  
<Root>  
  <Child1>1</Child1>  
  <Child2>2</Child2>  
  <Child3>3</Child3>  
</Root>  
```  
  
 Zwróć uwagę, że to samo zapytanie zwróciło jeden `Root` węzeł zamiast trzech węzłów podrzędnych.  
  
 Jednym z metod postępowania z tym jest użycie <xref:System.Xml.Linq.XDocument.Root%2A> Właściwości przed uzyskaniem dostępu do metody osi w następujący sposób:  
  
```csharp  
// Create a simple document and write it to a file  
File.WriteAllText("Test.xml", @"<Root>  
    <Child1>1</Child1>  
    <Child2>2</Child2>  
    <Child3>3</Child3>  
</Root>");  
  
Console.WriteLine("Querying tree loaded with XDocument.Load");  
Console.WriteLine("----");  
XDocument doc = XDocument.Load("Test.xml");  
IEnumerable<XElement> childList =  
    from el in doc.Root.Elements()  
    select el;  
foreach (XElement e in childList)  
    Console.WriteLine(e);  
```  
  
 To zapytanie jest teraz wykonywane w taki sam sposób, jak zapytanie w drzewie w katalogu głównym <xref:System.Xml.Linq.XElement> . Przykład generuje następujące dane wyjściowe:  
  
```output  
Querying tree loaded with XDocument.Load  
----  
<Child1>1</Child1>  
<Child2>2</Child2>  
<Child3>3</Child3>  
```  
  