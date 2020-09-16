---
title: Klonowanie a dołączanie
ms.date: 07/20/2015
ms.assetid: 3c3bd105-c9d3-49bd-875b-27ab4e8bc7a3
ms.openlocfilehash: 1974e10579e87f17746d5a9ba8a86ea8d819d9ea
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90555760"
---
# <a name="cloning-vs-attaching-visual-basic"></a>Klonowanie a dołączanie (Visual Basic)
W przypadku dodawania <xref:System.Xml.Linq.XNode> (w tym <xref:System.Xml.Linq.XElement> ) lub <xref:System.Xml.Linq.XAttribute> obiektów do nowego drzewa, jeśli nowa zawartość nie ma elementu nadrzędnego, obiekty są po prostu dołączone do drzewa XML. Jeśli nowa zawartość jest już nadrzędna i jest częścią innego drzewa XML, Nowa zawartość jest klonowana. Nowo sklonowana zawartość jest następnie dołączona do drzewa XML.  
  
## <a name="example"></a>Przykład  
 Poniższy kod ilustruje zachowanie po dodaniu elementu nadrzędnego do drzewa i po dodaniu elementu z elementem nadrzędnym do drzewa.  
  
```vb  
' Create a tree with a child element.  
Dim xmlTree1 As XElement = _  
    <Root>  
        <Child1>1</Child1>  
    </Root>  
  
' Create an element that is not parented.  
Dim child2 As XElement = <Child2>2</Child2>  
  
' Create a tree and add Child1 and Child2 to it.  
Dim xmlTree2 As XElement = _  
    <Root>  
        <%= xmlTree1.<Child1>(0) %>  
        <%= child2 %>  
    </Root>  
  
' Compare Child1 identity.  
Console.WriteLine("Child1 was {0}", _  
    IIf(xmlTree1.Element("Child1") Is xmlTree2.Element("Child1"), _  
    "attached", "cloned"))  
  
' Compare Child2 identity.  
Console.WriteLine("Child2 was {0}", _  
    IIf(child2 Is xmlTree2.Element("Child2"), _  
    "attached", "cloned"))  
```  
  
 Ten przykład generuje następujące wyniki:  
  
```console  
Child1 was cloned  
Child2 was attached  
```  
  
## <a name="see-also"></a>Zobacz także

- [Tworzenie drzew XML (Visual Basic)](../../../../standard/linq/xml-literals.md)
