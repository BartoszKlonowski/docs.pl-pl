---
title: Wczytywanie deklaracji jednostek i odwołań do jednostek do modelu DOM
ms.date: 03/30/2017
ms.assetid: 86dba977-5cc4-4567-964f-027ffabc47b2
ms.openlocfilehash: 8af9e4c1aedc588bcbf3b4f43e9e562fda2f3ce3
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95686829"
---
# <a name="reading-entity-declarations-and-entity-references-into-the-dom"></a>Wczytywanie deklaracji jednostek i odwołań do jednostek do modelu DOM

Jednostka jest deklaracją, która określa nazwę, która ma być używana w kodzie XML zamiast zawartości lub znaczników. Istnieją dwie części do jednostek. Najpierw należy powiązać nazwę z zastępowaniem zawartości za pomocą deklaracji jednostki. Deklaracja jednostki jest tworzona przy użyciu `<!ENTITY name "value">` składni w definicji typu dokumentu (DTD) lub schematu XML. Po drugie, Nazwa zdefiniowana w deklaracji jednostki jest następnie używana w kodzie XML. Gdy jest używana w kodzie XML, jest nazywana odwołaniem do jednostki. Na przykład następująca deklaracja jednostki deklaruje jednostkę nazwy `publisher` skojarzonej z zawartością "Microsoft Press".  
  
```xml  
<!ENTITY publisher "Microsoft Press">  
```  
  
 W poniższym przykładzie pokazano sposób użycia tej deklaracji jednostki w kodzie XML jako odwołanie do jednostki.  
  
```xml  
<author>Fred</author>  
<pubinfo>Published by &publisher;</pubinfo>  
```  
  
 Niektóre analizatory automatycznie rozszerzają jednostki, gdy dokument jest ładowany do pamięci. W związku z tym, gdy plik XML jest odczytywany do pamięci, deklaracje jednostek są zapamiętywane i zapisywane. Gdy analizator napotka następnie `&;` znaki, które identyfikują ogólne odwołanie do jednostki, Analizator wyszukuje tę nazwę w tabeli deklaracji jednostki. Odwołanie `&publisher;` jest zastępowane przez zawartość, którą reprezentuje. Przy użyciu następującego kodu XML  
  
```xml  
<author>Fred</author>  
<pubinfo>Published by &publisher;</pubinfo>  
```  
  
 rozwijanie odwołania do jednostki i zastępowanie `&publisher;` przy użyciu zawartości Microsoft Press, zapewnia następujący rozwinięty kod XML.  
  
 **Dane wyjściowe**  
  
```xml  
<author>Fred</author>  
<pubinfo>Published by Microsoft Press</pubinfo>  
```  
  
 Istnieje wiele rodzajów jednostek. Na poniższym diagramie przedstawiono podział typów jednostek i terminologii.  
  
 ![Wykres przepływu hierarchii typu jednostki](media/entity-hierarchy.gif "Entity_hierarchy")  
  
 Domyślnym implementacją Microsoft .NET Framework w Document Object Model XML (DOM) jest zachowywanie odwołań do jednostek i nie rozszerzanie jednostek podczas ładowania kodu XML. Implikacją tego jest to, że w przypadku załadowania dokumentu w modelu DOM zostanie utworzony węzeł **XmlEntityReference** zawierający zmienną referencyjną `&publisher;` z węzłami podrzędnymi reprezentującymi zawartość w jednostce zadeklarowanej w DTD.  
  
 Korzystając z `<!ENTITY publisher "Microsoft Press">` deklaracji jednostki, na poniższym diagramie przedstawiono węzły **XmlEntity** i **XmlText** utworzone na podstawie tej deklaracji.  
  
 ![węzły utworzone na podstawie deklaracji jednostki](media/xml-entitydeclaration-node2.png "xml_entitydeclaration_node2")  
  
 Różnice w przypadku, gdy odwołania do jednostek są rozwinięte i gdy nie są one różnicą w jakie węzły są generowane w drzewie DOM, w pamięci. Różnica w węzłach, które zostały wygenerowane, została omówiona w [odwołaniach do jednostek](entity-references-are-preserved.md) tematów, a [odwołania do jednostek są rozwinięte i nie są zachowywane](entity-references-are-expanded-and-not-preserved.md).  
  
## <a name="see-also"></a>Zobacz także

- [XML Document Object Model (DOM)](xml-document-object-model-dom.md)
