---
title: Zestawy węzłów w przekształceniach
ms.date: 03/30/2017
ms.assetid: ad034f0e-ff8b-4a71-9a4c-528c754263c4
ms.openlocfilehash: 72b3af5b471d73cc159dd700ddd29c4ffb5ea639
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94830119"
---
# <a name="node-sets-in-transformations"></a>Zestawy węzłów w przekształceniach
Zestawy węzłów to jeden z czterech podstawowych typów danych, które są zwracane z wyrażeń XPath (XML Path Language). Zestaw węzłów, który jest nieuporządkowaną kolekcją węzłów bez duplikatów, utworzonych w kolejności dokumentu, można przypisać do zmiennej w arkuszu stylów.  
  
> [!NOTE]
> <xref:System.Xml.Xsl.XslTransform>Klasa jest przestarzała w .NET Framework 2,0. Można wykonać przekształcenia Extensible Stylesheet Language for Transformations (XSLT) przy użyciu <xref:System.Xml.Xsl.XslCompiledTransform> klasy. Aby uzyskać więcej informacji, zobacz [Używanie klasy XslCompiledTransform](using-the-xslcompiledtransform-class.md) i [Migrowanie z klasy XslTransform](migrating-from-the-xsltransform-class.md) .  
  
 Zestawy węzłów są jednym z czterech podstawowych typów danych, które są zwracane z wyrażeń XPath. Zestaw węzłów, który jest nieuporządkowaną kolekcją węzłów bez duplikatów, utworzonych w kolejności dokumentu, można przypisać do zmiennej w arkuszu stylów. Ten zestaw węzłów, który jest wynikiem wyrażenia XPath użytego w `select` atrybucie w transformacji, ma takie samo zachowanie jak zestaw węzłów na podstawie Document Object Model XML (dom). Można nawigować po zestawie węzłów za pomocą zestawu metod pokazanych w [nawigacji zestawu węzłów za pomocą elementu XPathNavigator](node-set-navigation-using-xpathnavigator.md), w przeciwieństwie do fragmentu drzewa lub fragmentu drzewa wyników, który używa <xref:System.Xml.XPath.XPathNodeIterator> do nawigacji.  
  
 Poniższy przykład kodu pokazuje, jak wykonać iterację zestawu węzłów, gdy `variable` element lub `parameter` w arkuszu stylów jest obliczany w zestawie węzłów.  
  
## <a name="style-sheet"></a>Arkusz stylów  
  
```xml  
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">  
  
    <xsl:variable name="x" select="bookstore/book/title"></xsl:variable>  
  
    <xsl:template match="/">  
        <xsl:for-each select="$x">  
            ******  
            <xsl:value-of select="."></xsl:value-of>  
            ******  
        </xsl:for-each>  
    </xsl:template>  
  
</xsl:stylesheet>  
```  
  
## <a name="input"></a>Dane wejściowe  
  
```xml  
<bookstore>  
   <book style="autobiography">  
      <title>Seven Years in Trenton</title>  
   </book>  
  
   <book style="autobiography">  
      <title>Seven Years in Trenton2</title>  
   </book>  
  
   <book style="textbook">  
      <title>History of Trenton Vol 3</title>  
   </book>  
</bookstore>  
```  
  
## <a name="output"></a>Dane wyjściowe  
  
```output  
******  
Seven Years in Trenton  
******  
  
******  
Seven Years in Trenton2  
******  
  
******  
History of Trenton Vol 3  
******  
```  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Xml.XPath.XPathNodeIterator>
- [Przekształcenia XSLT przy użyciu klasy XslTransform](xslt-transformations-with-the-xsltransform-class.md)
- [Implementowanie procesora XSLT przy użyciu klasy XslTransform](xsltransform-class-implements-the-xslt-processor.md)
