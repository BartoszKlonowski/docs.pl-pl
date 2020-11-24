---
title: Przetwarzanie danych XML przy użyciu modelu danych XPath
ms.date: 03/30/2017
ms.assetid: 536c6fce-1453-4654-9c72-bca54d47e081
ms.openlocfilehash: 840fb40cc650d8f65af533d4102f18132bce3f53
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95686959"
---
# <a name="process-xml-data-using-the-xpath-data-model"></a><span data-ttu-id="b91b6-102">Przetwarzanie danych XML przy użyciu modelu danych XPath</span><span class="sxs-lookup"><span data-stu-id="b91b6-102">Process XML Data Using the XPath Data Model</span></span>

<span data-ttu-id="b91b6-103"><xref:System.Xml?displayProperty=nameWithType>Przestrzeń nazw zapewnia programistyczną reprezentację dokumentów XML, fragmentów, węzłów lub zestawów węzłów w pamięci przy użyciu <xref:System.Xml.XmlDocument> <xref:System.Xml.XPath.XPathDocument> klas lub.</span><span class="sxs-lookup"><span data-stu-id="b91b6-103">The <xref:System.Xml?displayProperty=nameWithType> namespace provides a programmatic representation of XML documents, fragments, nodes, or node-sets in-memory, using the <xref:System.Xml.XmlDocument> or <xref:System.Xml.XPath.XPathDocument> classes.</span></span>  
  
 <span data-ttu-id="b91b6-104"><xref:System.Xml.XPath.XPathDocument>Klasa zapewnia szybką, tylko do odczytu, reprezentację w pamięci dokumentu XML przy użyciu modelu danych XPath.</span><span class="sxs-lookup"><span data-stu-id="b91b6-104">The <xref:System.Xml.XPath.XPathDocument> class provides a fast, read-only, in-memory representation of an XML document using the XPath data model.</span></span> <span data-ttu-id="b91b6-105"><xref:System.Xml.XmlDocument>Klasa udostępnia edytowalną reprezentację w pamięci dokumentu XML implementującą W3C Document Object Model (dom) Level 1 rdzeń i podstawowy poziom dom 2.</span><span class="sxs-lookup"><span data-stu-id="b91b6-105">The <xref:System.Xml.XmlDocument> class provides an editable in-memory representation of an XML document implementing W3C Document Object Model (DOM) Level 1 Core and Core DOM Level 2.</span></span> <span data-ttu-id="b91b6-106">Obie klasy implementują <xref:System.Xml.XPath.IXPathNavigable> interfejs i zwracają <xref:System.Xml.XPath.XPathNavigator> obiekt używany do zaznaczania, szacowania, nawigowania i w niektórych przypadkach, edytowania źródłowych danych XML.</span><span class="sxs-lookup"><span data-stu-id="b91b6-106">Both classes implement the <xref:System.Xml.XPath.IXPathNavigable> interface and return an <xref:System.Xml.XPath.XPathNavigator> object used to select, evaluate, navigate, and in some cases, edit the underlying XML data.</span></span>  
  
 <span data-ttu-id="b91b6-107">W poniższych sekcjach opisano funkcjonalność <xref:System.Xml.XPath.XPathNavigator> klasy na podstawie klasy, która zwraca ją.</span><span class="sxs-lookup"><span data-stu-id="b91b6-107">The following sections describe the functionality of the <xref:System.Xml.XPath.XPathNavigator> class based on the class that returns it.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="b91b6-108">W tej sekcji</span><span class="sxs-lookup"><span data-stu-id="b91b6-108">In This Section</span></span>  

 [<span data-ttu-id="b91b6-109">Wczytywanie danych XML przy użyciu klas XPathDocument i XmlDocument</span><span class="sxs-lookup"><span data-stu-id="b91b6-109">Reading XML Data using XPathDocument and XmlDocument</span></span>](reading-xml-data-using-xpathdocument-and-xmldocument.md)  
 <span data-ttu-id="b91b6-110">Opisuje sposób tworzenia <xref:System.Xml.XPath.XPathDocument> obiektu klasy tylko do odczytu w celu odczytania dokumentu XML i sposobu tworzenia edytowalnego <xref:System.Xml.XmlDocument> obiektu klasy w celu odczytywania i EDYTOWANIA dokumentu XML.</span><span class="sxs-lookup"><span data-stu-id="b91b6-110">Describes how to create a read-only <xref:System.Xml.XPath.XPathDocument> class object to read an XML document and how to create an editable <xref:System.Xml.XmlDocument> class object to read and edit an XML document.</span></span> <span data-ttu-id="b91b6-111">W tym temacie opisano również, jak zwrócić <xref:System.Xml.XPath.XPathNavigator> obiekt z każdej klasy w celu nawigowania i edytowania dokumentu XML.</span><span class="sxs-lookup"><span data-stu-id="b91b6-111">This topic also describes how return an <xref:System.Xml.XPath.XPathNavigator> object from each class to navigate and edit an XML document.</span></span>  
  
 [<span data-ttu-id="b91b6-112">Wybieranie, obliczanie i dopasowywanie danych XML przy użyciu klasy XPathNavigator</span><span class="sxs-lookup"><span data-stu-id="b91b6-112">Selecting, Evaluating and Matching XML Data using XPathNavigator</span></span>](selecting-evaluating-and-matching-xml-data-using-xpathnavigator.md)  
 <span data-ttu-id="b91b6-113">Opisuje metody <xref:System.Xml.XPath.XPathNavigator> klasy używane do wybierania węzłów w <xref:System.Xml.XPath.XPathDocument> <xref:System.Xml.XmlDocument> obiekcie lub przy użyciu kwerendy XPath, oceniają i sprawdzają wyniki wyrażenia XPath i określają, czy węzeł w dokumencie XML odpowiada danemu wyrażeniu XPath.</span><span class="sxs-lookup"><span data-stu-id="b91b6-113">Describes the methods of the <xref:System.Xml.XPath.XPathNavigator> class used to select nodes in an <xref:System.Xml.XPath.XPathDocument> or <xref:System.Xml.XmlDocument> object using an XPath query, evaluate and examine the results of an XPath expression, and determine if a node in an XML document matches a given XPath expression.</span></span>  
  
 [<span data-ttu-id="b91b6-114">Uzyskiwanie dostępu do danych XML przy użyciu klasy XPathNavigator</span><span class="sxs-lookup"><span data-stu-id="b91b6-114">Accessing XML Data using XPathNavigator</span></span>](accessing-xml-data-using-xpathnavigator.md)  
 <span data-ttu-id="b91b6-115">Opisuje metody <xref:System.Xml.XPath.XPathNavigator> klasy używane do nawigowania po węzłach, wyodrębniania danych XML i uzyskiwania dostępu do jednoznacznie wpisanych danych XML w <xref:System.Xml.XPath.XPathDocument> <xref:System.Xml.XmlDocument> obiekcie lub.</span><span class="sxs-lookup"><span data-stu-id="b91b6-115">Describes the methods of the <xref:System.Xml.XPath.XPathNavigator> class used to navigate nodes, extract XML data and access strongly typed XML data in an <xref:System.Xml.XPath.XPathDocument> or <xref:System.Xml.XmlDocument> object.</span></span>  
  
 [<span data-ttu-id="b91b6-116">Edytowanie danych XML przy użyciu klasy XPathNavigator</span><span class="sxs-lookup"><span data-stu-id="b91b6-116">Editing XML Data using XPathNavigator</span></span>](editing-xml-data-using-xpathnavigator.md)  
 <span data-ttu-id="b91b6-117">Opisuje metody <xref:System.Xml.XPath.XPathNavigator> klasy używane do wstawiania, modyfikowania i usuwania węzłów oraz wartości z dokumentu XML zawartego w <xref:System.Xml.XmlDocument> obiekcie.</span><span class="sxs-lookup"><span data-stu-id="b91b6-117">Describes the methods of the <xref:System.Xml.XPath.XPathNavigator> class used to insert, modify and remove nodes and values from an XML document contained in an <xref:System.Xml.XmlDocument> object.</span></span>  
  
 [<span data-ttu-id="b91b6-118">Weryfikacja schematu przy użyciu klasy XPathNavigator</span><span class="sxs-lookup"><span data-stu-id="b91b6-118">Schema Validation using XPathNavigator</span></span>](schema-validation-using-xpathnavigator.md)  
 <span data-ttu-id="b91b6-119">Opisuje sposoby sprawdzania poprawności zawartości XML zawartej w <xref:System.Xml.XPath.XPathDocument> <xref:System.Xml.XmlDocument> obiekcie lub.</span><span class="sxs-lookup"><span data-stu-id="b91b6-119">Describes the ways to validate the XML content contained in an <xref:System.Xml.XPath.XPathDocument> or <xref:System.Xml.XmlDocument> object.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="b91b6-120">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="b91b6-120">See also</span></span>

- <xref:System.Xml.XmlDocument>
- <xref:System.Xml.XPath.XPathDocument>
- <xref:System.Xml.XPath.XPathNavigator>
- [<span data-ttu-id="b91b6-121">Przetwarzanie danych XML przy użyciu modelu DOM</span><span class="sxs-lookup"><span data-stu-id="b91b6-121">Process XML Data Using the DOM Model</span></span>](process-xml-data-using-the-dom-model.md)
