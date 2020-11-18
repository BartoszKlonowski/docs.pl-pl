---
title: 'Instrukcje: Przekształcanie fragmentu węzła'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 73a6c582-b9d7-4fa7-9a05-6d931e1f3de8
ms.openlocfilehash: 5c69a35497feced92a05e124307d3be584ab86b7
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94829443"
---
# <a name="how-to-transform-a-node-fragment"></a>Instrukcje: Przekształcanie fragmentu węzła
Gdy przekształcasz dane zawarte w <xref:System.Xml.XmlDocument> obiekcie lub <xref:System.Xml.XPath.XPathDocument> , przekształcenia XSLT mają zastosowanie do dokumentu jako całości. Innymi słowy, jeśli przejdziesz do węzła innego niż węzeł główny dokumentu, nie uniemożliwi to proces przekształcania uzyskuje dostęp do wszystkich węzłów w załadowanym dokumencie. Aby przekształcić fragment węzła, należy utworzyć oddzielny obiekt zawierający tylko fragment węzła i przekazać ten obiekt do <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> metody.  
  
## <a name="procedures"></a>Procedury  
  
#### <a name="to-transform-a-node-fragment"></a>Aby przekształcić fragment węzła  
  
1. Utwórz obiekt zawierający dokument źródłowy.  
  
2. Znajdź fragment węzła, który chcesz przekształcić.  
  
3. Utwórz oddzielny obiekt za pomocą tylko fragmentu węzła.  
  
4. Przekaż fragment węzła do <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> metody.  
  
## <a name="example"></a>Przykład  
 Poniższy przykład przekształca fragment węzła i wyświetla wyniki w konsoli programu.  
  
 [!code-csharp[XSLT_NodeFrag#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XSLT_NodeFrag/CS/xslt_frag.cs#1)]
 [!code-vb[XSLT_NodeFrag#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XSLT_NodeFrag/VB/xslt_frag.vb#1)]  
  
### <a name="input"></a>Dane wejściowe  
  
##### <a name="booksxml"></a>books.xml  
 [!code-xml[XML_Core_Files#1](../../../../samples/snippets/xml/VS_Snippets_Data/XML_Core_Files/XML/books.xml#1)]  
  
##### <a name="singlexsl"></a>Single. xsl  
 [!code-xml[XSLT_NodeFrag#2](../../../../samples/snippets/xml/VS_Snippets_Data/XSLT_NodeFrag/XML/single.xsl#2)]  
  
### <a name="output"></a>Dane wyjściowe  
 Tytuł książki to człowiek z zaufaniem.  
  
## <a name="see-also"></a>Zobacz także

- [Używanie klasy XslCompiledTransform](using-the-xslcompiledtransform-class.md)
