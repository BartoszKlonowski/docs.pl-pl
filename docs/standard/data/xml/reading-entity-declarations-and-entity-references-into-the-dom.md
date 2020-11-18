---
title: Wczytywanie deklaracji jednostek i odwołań do jednostek do modelu DOM
ms.date: 03/30/2017
ms.assetid: 86dba977-5cc4-4567-964f-027ffabc47b2
ms.openlocfilehash: 01a90ac467bec5576005c16355617c03b6d38389
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94818716"
---
# <a name="reading-entity-declarations-and-entity-references-into-the-dom"></a><span data-ttu-id="00265-102">Wczytywanie deklaracji jednostek i odwołań do jednostek do modelu DOM</span><span class="sxs-lookup"><span data-stu-id="00265-102">Reading Entity Declarations and Entity References into the DOM</span></span>
<span data-ttu-id="00265-103">Jednostka jest deklaracją, która określa nazwę, która ma być używana w kodzie XML zamiast zawartości lub znaczników.</span><span class="sxs-lookup"><span data-stu-id="00265-103">An entity is a declaration that states a name to be used in the XML in place of content or markup.</span></span> <span data-ttu-id="00265-104">Istnieją dwie części do jednostek.</span><span class="sxs-lookup"><span data-stu-id="00265-104">There are two parts to entities.</span></span> <span data-ttu-id="00265-105">Najpierw należy powiązać nazwę z zastępowaniem zawartości za pomocą deklaracji jednostki.</span><span class="sxs-lookup"><span data-stu-id="00265-105">First, you must tie a name to the replacement content using an entity declaration.</span></span> <span data-ttu-id="00265-106">Deklaracja jednostki jest tworzona przy użyciu `<!ENTITY name "value">` składni w definicji typu dokumentu (DTD) lub schematu XML.</span><span class="sxs-lookup"><span data-stu-id="00265-106">An entity declaration is created by using the `<!ENTITY name "value">` syntax in a document type definition (DTD) or XML schema.</span></span> <span data-ttu-id="00265-107">Po drugie, Nazwa zdefiniowana w deklaracji jednostki jest następnie używana w kodzie XML.</span><span class="sxs-lookup"><span data-stu-id="00265-107">Secondly, the name defined in the entity declaration is subsequently used in the XML.</span></span> <span data-ttu-id="00265-108">Gdy jest używana w kodzie XML, jest nazywana odwołaniem do jednostki.</span><span class="sxs-lookup"><span data-stu-id="00265-108">When used in the XML, it is called an entity reference.</span></span> <span data-ttu-id="00265-109">Na przykład następująca deklaracja jednostki deklaruje jednostkę nazwy `publisher` skojarzonej z zawartością "Microsoft Press".</span><span class="sxs-lookup"><span data-stu-id="00265-109">For example, the following entity declaration declares an entity of the name `publisher` being associated with the content of "Microsoft Press".</span></span>  
  
```xml  
<!ENTITY publisher "Microsoft Press">  
```  
  
 <span data-ttu-id="00265-110">W poniższym przykładzie pokazano sposób użycia tej deklaracji jednostki w kodzie XML jako odwołanie do jednostki.</span><span class="sxs-lookup"><span data-stu-id="00265-110">The following example shows the use of this entity declaration in XML as an entity reference.</span></span>  
  
```xml  
<author>Fred</author>  
<pubinfo>Published by &publisher;</pubinfo>  
```  
  
 <span data-ttu-id="00265-111">Niektóre analizatory automatycznie rozszerzają jednostki, gdy dokument jest ładowany do pamięci.</span><span class="sxs-lookup"><span data-stu-id="00265-111">Some parsers automatically expand entities when a document is loaded into memory.</span></span> <span data-ttu-id="00265-112">W związku z tym, gdy plik XML jest odczytywany do pamięci, deklaracje jednostek są zapamiętywane i zapisywane.</span><span class="sxs-lookup"><span data-stu-id="00265-112">Therefore, when the XML is being read into memory, entity declarations are remembered and saved.</span></span> <span data-ttu-id="00265-113">Gdy analizator napotka następnie `&;` znaki, które identyfikują ogólne odwołanie do jednostki, Analizator wyszukuje tę nazwę w tabeli deklaracji jednostki.</span><span class="sxs-lookup"><span data-stu-id="00265-113">When the parser subsequently encounters `&;` characters, which identify a general entity reference, the parser looks up that name in an entity declaration table.</span></span> <span data-ttu-id="00265-114">Odwołanie `&publisher;` jest zastępowane przez zawartość, którą reprezentuje.</span><span class="sxs-lookup"><span data-stu-id="00265-114">The reference, `&publisher;` is replaced by the content that it represents.</span></span> <span data-ttu-id="00265-115">Przy użyciu następującego kodu XML</span><span class="sxs-lookup"><span data-stu-id="00265-115">Using the following XML,</span></span>  
  
```xml  
<author>Fred</author>  
<pubinfo>Published by &publisher;</pubinfo>  
```  
  
 <span data-ttu-id="00265-116">rozwijanie odwołania do jednostki i zastępowanie `&publisher;` przy użyciu zawartości Microsoft Press, zapewnia następujący rozwinięty kod XML.</span><span class="sxs-lookup"><span data-stu-id="00265-116">expanding the entity reference and replacing the `&publisher;` with the Microsoft Press content gives the following expanded XML.</span></span>  
  
 <span data-ttu-id="00265-117">**Dane wyjściowe**</span><span class="sxs-lookup"><span data-stu-id="00265-117">**Output**</span></span>  
  
```xml  
<author>Fred</author>  
<pubinfo>Published by Microsoft Press</pubinfo>  
```  
  
 <span data-ttu-id="00265-118">Istnieje wiele rodzajów jednostek.</span><span class="sxs-lookup"><span data-stu-id="00265-118">There are many kinds of entities.</span></span> <span data-ttu-id="00265-119">Na poniższym diagramie przedstawiono podział typów jednostek i terminologii.</span><span class="sxs-lookup"><span data-stu-id="00265-119">The following diagram shows the breakdown of entity types and terminology.</span></span>  
  
 <span data-ttu-id="00265-120">![Wykres przepływu hierarchii typu jednostki](media/entity-hierarchy.gif "Entity_hierarchy")</span><span class="sxs-lookup"><span data-stu-id="00265-120">![flow chart of entity type hierarchy](media/entity-hierarchy.gif "Entity_hierarchy")</span></span>  
  
 <span data-ttu-id="00265-121">Domyślnym implementacją Microsoft .NET Framework w Document Object Model XML (DOM) jest zachowywanie odwołań do jednostek i nie rozszerzanie jednostek podczas ładowania kodu XML.</span><span class="sxs-lookup"><span data-stu-id="00265-121">The default for the Microsoft .NET Framework implementation of the XML Document Object Model (DOM) is to preserve the entities references and not expand the entities when the XML is loaded.</span></span> <span data-ttu-id="00265-122">Implikacją tego jest to, że w przypadku załadowania dokumentu w modelu DOM zostanie utworzony węzeł **XmlEntityReference** zawierający zmienną referencyjną `&publisher;` z węzłami podrzędnymi reprezentującymi zawartość w jednostce zadeklarowanej w DTD.</span><span class="sxs-lookup"><span data-stu-id="00265-122">The implication of this is that as a document is loaded in the DOM, an **XmlEntityReference** node containing the reference variable `&publisher;` is created, with child nodes representing the content in the entity declared in the DTD.</span></span>  
  
 <span data-ttu-id="00265-123">Korzystając z `<!ENTITY publisher "Microsoft Press">` deklaracji jednostki, na poniższym diagramie przedstawiono węzły **XmlEntity** i **XmlText** utworzone na podstawie tej deklaracji.</span><span class="sxs-lookup"><span data-stu-id="00265-123">Using the `<!ENTITY publisher "Microsoft Press">` entity declaration, the following diagram shows the **XmlEntity** and **XmlText** nodes created from this declaration.</span></span>  
  
 <span data-ttu-id="00265-124">![węzły utworzone na podstawie deklaracji jednostki](media/xml-entitydeclaration-node2.png "xml_entitydeclaration_node2")</span><span class="sxs-lookup"><span data-stu-id="00265-124">![nodes created from entity declaration](media/xml-entitydeclaration-node2.png "xml_entitydeclaration_node2")</span></span>  
  
 <span data-ttu-id="00265-125">Różnice w przypadku, gdy odwołania do jednostek są rozwinięte i gdy nie są one różnicą w jakie węzły są generowane w drzewie DOM, w pamięci.</span><span class="sxs-lookup"><span data-stu-id="00265-125">The differences when entity references are expanded and when they are not makes a difference in what nodes are generated in the DOM tree, in memory.</span></span> <span data-ttu-id="00265-126">Różnica w węzłach, które zostały wygenerowane, została omówiona w [odwołaniach do jednostek](entity-references-are-preserved.md) tematów, a [odwołania do jednostek są rozwinięte i nie są zachowywane](entity-references-are-expanded-and-not-preserved.md).</span><span class="sxs-lookup"><span data-stu-id="00265-126">The difference in the nodes that are generated is explained in the topics [Entity References are Preserved](entity-references-are-preserved.md) and [Entity References are Expanded and Not Preserved](entity-references-are-expanded-and-not-preserved.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="00265-127">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="00265-127">See also</span></span>

- [<span data-ttu-id="00265-128">XML Document Object Model (DOM)</span><span class="sxs-lookup"><span data-stu-id="00265-128">XML Document Object Model (DOM)</span></span>](xml-document-object-model-dom.md)
