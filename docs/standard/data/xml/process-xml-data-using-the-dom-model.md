---
title: Przetwarzanie danych XML przy użyciu modelu DOM
ms.date: 03/30/2017
ms.assetid: 56b6e9c7-ed82-4a65-a647-7be32c83bcc8
ms.openlocfilehash: 2608008f33eb8bc0dd0a9b5fe96e619df6138b51
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94830912"
---
# <a name="process-xml-data-using-the-dom-model"></a><span data-ttu-id="1d3ed-102">Przetwarzanie danych XML przy użyciu modelu DOM</span><span class="sxs-lookup"><span data-stu-id="1d3ed-102">Process XML Data Using the DOM Model</span></span>
<span data-ttu-id="1d3ed-103">Document Object Model XML (DOM) traktuje dane XML jako standardowy zestaw obiektów i służy do przetwarzania danych XML w pamięci.</span><span class="sxs-lookup"><span data-stu-id="1d3ed-103">The XML Document Object Model (DOM) treats XML data as a standard set of objects and is used to process XML data in memory.</span></span> <span data-ttu-id="1d3ed-104">`System.Xml`Przestrzeń nazw zapewnia programistyczną reprezentację dokumentów XML, fragmentów, węzłów lub zestawów węzłów.</span><span class="sxs-lookup"><span data-stu-id="1d3ed-104">The `System.Xml` namespace provides a programmatic representation of XML documents, fragments, nodes, or node-sets.</span></span> <span data-ttu-id="1d3ed-105">Jest on oparty na organizacja World Wide Web Consortium (W3C) modelu DOM 1 rdzeń i na poziomie modelu DOM 2 rdzeni.</span><span class="sxs-lookup"><span data-stu-id="1d3ed-105">It is based on the World Wide Web Consortium (W3C) DOM Level 1 Core and the DOM Level 2 Core recommendations.</span></span>  
  
 <span data-ttu-id="1d3ed-106"><xref:System.Xml.XmlDocument>Klasa reprezentuje dokument XML.</span><span class="sxs-lookup"><span data-stu-id="1d3ed-106">The <xref:System.Xml.XmlDocument> class represents an XML document.</span></span> <span data-ttu-id="1d3ed-107">Obejmuje ona członków do pobierania i tworzenia wszystkich innych obiektów XML.</span><span class="sxs-lookup"><span data-stu-id="1d3ed-107">It includes members for retrieving and creating all other XML objects.</span></span> <span data-ttu-id="1d3ed-108">Korzystając z <xref:System.Xml.XmlDocument> i powiązanych z nimi klas, można tworzyć dokumenty XML, ładować i uzyskiwać dostęp do danych, modyfikować dane i zapisywać zmiany.</span><span class="sxs-lookup"><span data-stu-id="1d3ed-108">Using the <xref:System.Xml.XmlDocument>, and its related classes, you can construct XML documents, load and access data, modify data, and save changes.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="1d3ed-109">W tej sekcji</span><span class="sxs-lookup"><span data-stu-id="1d3ed-109">In This Section</span></span>  
  
- [<span data-ttu-id="1d3ed-110">XML Document Object Model (DOM)</span><span class="sxs-lookup"><span data-stu-id="1d3ed-110">XML Document Object Model (DOM)</span></span>](xml-document-object-model-dom.md)  
  
- [<span data-ttu-id="1d3ed-111">Typy węzłów XML</span><span class="sxs-lookup"><span data-stu-id="1d3ed-111">Types of XML Nodes</span></span>](types-of-xml-nodes.md)  
  
- [<span data-ttu-id="1d3ed-112">Hierarchia modelu DOM (XML Document Object Model)</span><span class="sxs-lookup"><span data-stu-id="1d3ed-112">XML Document Object Model (DOM) Hierarchy</span></span>](xml-document-object-model-dom-hierarchy.md)  
  
- [<span data-ttu-id="1d3ed-113">Mapowanie hierarchii obiektów na dane XML</span><span class="sxs-lookup"><span data-stu-id="1d3ed-113">Mapping the Object Hierarchy to XML Data</span></span>](mapping-the-object-hierarchy-to-xml-data.md)  
  
- [<span data-ttu-id="1d3ed-114">Tworzenie dokumentu XML</span><span class="sxs-lookup"><span data-stu-id="1d3ed-114">XML Document Creation</span></span>](xml-document-creation.md)  
  
- [<span data-ttu-id="1d3ed-115">Wczytywanie dokumentu XML do modelu DOM</span><span class="sxs-lookup"><span data-stu-id="1d3ed-115">Reading an XML Document into the DOM</span></span>](reading-an-xml-document-into-the-dom.md)  
  
- [<span data-ttu-id="1d3ed-116">Wstawianie węzłów do dokumentu XML</span><span class="sxs-lookup"><span data-stu-id="1d3ed-116">Inserting Nodes into an XML Document</span></span>](inserting-nodes-into-an-xml-document.md)  
  
- [<span data-ttu-id="1d3ed-117">Usuwanie węzłów, zawartości i wartości z dokumentu XML</span><span class="sxs-lookup"><span data-stu-id="1d3ed-117">Removing Nodes, Content, and Values from an XML Document</span></span>](removing-nodes-content-and-values-from-an-xml-document.md)  
  
- [<span data-ttu-id="1d3ed-118">Modyfikowanie węzłów, zawartości i wartości w dokumencie XML</span><span class="sxs-lookup"><span data-stu-id="1d3ed-118">Modifying Nodes, Content, and Values in an XML Document</span></span>](modifying-nodes-content-and-values-in-an-xml-document.md)  
  
- [<span data-ttu-id="1d3ed-119">Weryfikowanie dokumentu XML w modelu DOM</span><span class="sxs-lookup"><span data-stu-id="1d3ed-119">Validating an XML Document in the DOM</span></span>](validating-an-xml-document-in-the-dom.md)  
  
- [<span data-ttu-id="1d3ed-120">Zapisywanie dokumentu</span><span class="sxs-lookup"><span data-stu-id="1d3ed-120">Saving and Writing a Document</span></span>](saving-and-writing-a-document.md)  
  
- [<span data-ttu-id="1d3ed-121">Wybieranie węzłów za pomocą nawigacji XPath</span><span class="sxs-lookup"><span data-stu-id="1d3ed-121">Select Nodes Using XPath Navigation</span></span>](select-nodes-using-xpath-navigation.md)  
  
- [<span data-ttu-id="1d3ed-122">Rozpoznawanie zasobów zewnętrznych</span><span class="sxs-lookup"><span data-stu-id="1d3ed-122">Resolving External Resources</span></span>](resolving-external-resources.md)  
  
- [<span data-ttu-id="1d3ed-123">Porównywanie obiektów przy użyciu tabeli XmlNameTable</span><span class="sxs-lookup"><span data-stu-id="1d3ed-123">Object Comparison Using XmlNameTable</span></span>](object-comparison-using-xmlnametable.md)  
  
- [<span data-ttu-id="1d3ed-124">Kolekcje węzłów: NamedNodeMaps i NodeLists</span><span class="sxs-lookup"><span data-stu-id="1d3ed-124">Node Collections in NamedNodeMaps and NodeLists</span></span>](node-collections-in-namednodemaps-and-nodelists.md)  
  
- [<span data-ttu-id="1d3ed-125">Aktualizacja dynamiczna obiektów NodeLists i NamedNodeMaps</span><span class="sxs-lookup"><span data-stu-id="1d3ed-125">Dynamic Updates to NodeLists and NamedNodeMaps</span></span>](dynamic-updates-to-nodelists-and-namednodemaps.md)  
  
- [<span data-ttu-id="1d3ed-126">Obsługa przestrzeni nazw w modelu DOM</span><span class="sxs-lookup"><span data-stu-id="1d3ed-126">Namespace Support in the DOM</span></span>](namespace-support-in-the-dom.md)  
  
- [<span data-ttu-id="1d3ed-127">Obsługa zdarzeń w dokumencie XML przy użyciu klasy XmlNodeChangedEventArgs</span><span class="sxs-lookup"><span data-stu-id="1d3ed-127">Event Handling in an XML Document Using the XmlNodeChangedEventArgs</span></span>](event-handling-in-an-xml-document-using-the-xmlnodechangedeventargs.md)  
  
- [<span data-ttu-id="1d3ed-128">Rozszerzanie modelu DOM</span><span class="sxs-lookup"><span data-stu-id="1d3ed-128">Extending the DOM</span></span>](extending-the-dom.md)  
  
## <a name="related-sections"></a><span data-ttu-id="1d3ed-129">Sekcje pokrewne</span><span class="sxs-lookup"><span data-stu-id="1d3ed-129">Related Sections</span></span>  
 [<span data-ttu-id="1d3ed-130">Przetwarzanie danych XML przy użyciu modelu danych XPath</span><span class="sxs-lookup"><span data-stu-id="1d3ed-130">Process XML Data Using the XPath Data Model</span></span>](process-xml-data-using-the-xpath-data-model.md)  
 <span data-ttu-id="1d3ed-131">Omawia przetwarzanie XML przy użyciu <xref:System.Xml.XPath.XPathNavigator> klasy.</span><span class="sxs-lookup"><span data-stu-id="1d3ed-131">Discusses XML processing using the <xref:System.Xml.XPath.XPathNavigator> class.</span></span>
