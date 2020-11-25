---
title: Zmienianie właściwości prefiksu przestrzeni nazw
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d5c87cbe-4d69-429f-aad5-3103c2ca2770
ms.openlocfilehash: a4ba378620d0c5ec01aaa5d87020c33fdbffcf01
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95725355"
---
# <a name="changing-namespace-prefix-properties"></a>Zmienianie właściwości prefiksu przestrzeni nazw

Klasa **XmlNode** pozwala zmienić prefiks przestrzeni nazw skojarzony z danym węzłem. Na przykład poniższy kod ilustruje prefiks elementu, który jest zmieniany.  
  
```vb  
Dim doc as XmlDocument = new XmlDocument()  
doc.LoadXml("<a:test xmlns:a='123' xmlns:b='456'/>")  
Dim e as XmlElement = doc.DocumentElement  
e.Prefix = "b"  
Console.WriteLine(doc.InnerXml)  
```  
  
```csharp  
XmlDocument doc = new XmlDocument();  
doc.LoadXml("<a:test xmlns:a='123' xmlns:b='456'/>");  
XmlElement e = doc.DocumentElement;
e.Prefix = "b";  
Console.WriteLine(doc.InnerXml);  
```  
  
 **Dane wyjściowe**  
  
```xml  
<b:test xmlns:a="123" xmlns:b="456" />  
```  
  
 Zmiana prefiksu węzła nie powoduje zmiany jego przestrzeni nazw. Przestrzeń nazw można ustawić tylko podczas tworzenia węzła. Gdy utrwalasz drzewo, nowe atrybuty przestrzeni nazw mogą być utrwalane, aby spełnić ustawiony prefiks. Jeśli nie można utworzyć nowej przestrzeni nazw, prefiks zostanie zmieniony, więc węzeł zachowuje swoją nazwę lokalną i przestrzeń nazw. Poniższy przykład pokazuje dodawany atrybut przestrzeni nazw.  
  
```vb  
Dim doc as XmlDocument = new XmlDocument()  
doc.LoadXml("<test xmlns='123'/>")  
Dim e as XmlElement = doc.DocumentElement  
e.Prefix = "a"  
Console.WriteLine(doc.InnerXml)  
```  
  
```csharp  
XmlDocument doc = new XmlDocument();  
doc.LoadXml("<test xmlns='123'/>");  
XmlElement e = doc.DocumentElement;
e.Prefix = "a";  
Console.WriteLine(doc.InnerXml);  
```  
  
 **Dane wyjściowe**  
  
```xml  
<a:test xmlns="123" xmlns:a="123" />  
```  
  
 Gdy drzewo zostało utrwalone jako ciąg w wyniku wywołania metody **doc. InnerXml**, `xmlns:a='123'` atrybut został dodany w celu zachowania przestrzeni nazw `test` elementu. To `'123'` i pozostało `'123'` .  
  
## <a name="see-also"></a>Zobacz także

- [XML Document Object Model (DOM)](xml-document-object-model-dom.md)
