---
title: Dokumenty i dane XML
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: e695047f-3c0f-4045-8708-5baea91cc380
ms.openlocfilehash: 6d2a52567a1fc8bdbbb1d039ac583c889d77d4af
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90540137"
---
# <a name="xml-documents-and-data"></a><span data-ttu-id="8b719-102">Dokumenty i dane XML</span><span class="sxs-lookup"><span data-stu-id="8b719-102">XML Documents and Data</span></span>

<span data-ttu-id="8b719-103">.NET Framework zapewnia kompleksowy i zintegrowany zestaw klas, które umożliwiają łatwe tworzenie aplikacji obsługujących kod XML.</span><span class="sxs-lookup"><span data-stu-id="8b719-103">The .NET Framework provides a comprehensive and integrated set of classes that enable you to build XML-aware apps easily.</span></span> <span data-ttu-id="8b719-104">Klasy w następujących przestrzeniach nazw obsługują analizowanie i zapisywanie XML, edytowanie danych XML w pamięci, sprawdzanie poprawności danych i transformację XSLT.</span><span class="sxs-lookup"><span data-stu-id="8b719-104">The classes in the following namespaces support parsing and writing XML, editing XML data in memory, data validation, and XSLT transformation.</span></span>

- <xref:System.Xml>

- <xref:System.Xml.XPath>

- <xref:System.Xml.Xsl>

- <xref:System.Xml.Schema>

- <xref:System.Xml.Linq>

<span data-ttu-id="8b719-105">Aby uzyskać pełną listę, wyszukaj frazę "System.Xml" w [przeglądarce interfejsu API platformy .NET](../../../../api/index.md?term=system.xml).</span><span class="sxs-lookup"><span data-stu-id="8b719-105">For a full list, search for "System.Xml" on the [.NET API browser](../../../../api/index.md?term=system.xml).</span></span>

<span data-ttu-id="8b719-106">Klasy w tych obszarach nazw obsługują zalecenia dotyczące organizacja World Wide Web Consortium (W3C).</span><span class="sxs-lookup"><span data-stu-id="8b719-106">The classes in these namespaces support World Wide Web Consortium (W3C) recommendations.</span></span> <span data-ttu-id="8b719-107">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="8b719-107">For example:</span></span>

- <span data-ttu-id="8b719-108"><xref:System.Xml.XmlDocument?displayProperty=nameWithType>Klasa implementuje podstawowe zalecenia [poziomu 1 dla W3C Document Object Model (dom)](https://www.w3.org/TR/REC-DOM-Level-1/) i [poziom dom 2](https://www.w3.org/TR/DOM-Level-2-Core/) .</span><span class="sxs-lookup"><span data-stu-id="8b719-108">The <xref:System.Xml.XmlDocument?displayProperty=nameWithType> class implements the [W3C Document Object Model (DOM) Level 1 Core](https://www.w3.org/TR/REC-DOM-Level-1/) and [DOM Level 2 Core](https://www.w3.org/TR/DOM-Level-2-Core/) recommendations.</span></span>

- <span data-ttu-id="8b719-109"><xref:System.Xml.XmlReader?displayProperty=nameWithType>Klasy i <xref:System.Xml.XmlWriter?displayProperty=nameWithType> obsługują [W3C XML 1,0](https://www.w3.org/TR/2006/REC-xml-20060816/) i [przestrzenie nazw w](https://www.w3.org/TR/REC-xml-names/) zaleceniach XML.</span><span class="sxs-lookup"><span data-stu-id="8b719-109">The <xref:System.Xml.XmlReader?displayProperty=nameWithType> and <xref:System.Xml.XmlWriter?displayProperty=nameWithType> classes support the [W3C XML 1.0](https://www.w3.org/TR/2006/REC-xml-20060816/) and the [Namespaces in XML](https://www.w3.org/TR/REC-xml-names/) recommendations.</span></span>

- <span data-ttu-id="8b719-110">Schematy w <xref:System.Xml.Schema.XmlSchemaSet?displayProperty=nameWithType> klasie obsługują [plik W3C XML schematu część 1: struktury](https://www.w3.org/TR/xmlschema-1/) i [XML schematu część 2:](https://www.w3.org/TR/xmlschema-2/) zalecenia dotyczące typów danych.</span><span class="sxs-lookup"><span data-stu-id="8b719-110">Schemas in the <xref:System.Xml.Schema.XmlSchemaSet?displayProperty=nameWithType> class support the [W3C XML Schema Part 1: Structures](https://www.w3.org/TR/xmlschema-1/) and [XML Schema Part 2: Datatypes](https://www.w3.org/TR/xmlschema-2/) recommendations.</span></span>

- <span data-ttu-id="8b719-111">Klasy w <xref:System.Xml.Xsl?displayProperty=nameWithType> przestrzeni nazw obsługują przekształcenia XSLT zgodne z zaleceniem [W3C XSLT 1,0](https://www.w3.org/TR/xslt) .</span><span class="sxs-lookup"><span data-stu-id="8b719-111">Classes in the <xref:System.Xml.Xsl?displayProperty=nameWithType> namespace support XSLT transformations that conform to the [W3C XSLT 1.0](https://www.w3.org/TR/xslt) recommendation.</span></span>

<span data-ttu-id="8b719-112">Klasy XML w .NET Framework zapewniają następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="8b719-112">The XML classes in the .NET Framework provide these benefits:</span></span>

- <span data-ttu-id="8b719-113">**Zwiększając.**</span><span class="sxs-lookup"><span data-stu-id="8b719-113">**Productivity.**</span></span> <span data-ttu-id="8b719-114">[LINQ to XML (C#)](../../linq/linq-xml-overview.md) i [LINQ to XML (Visual Basic)](../../linq/linq-xml-overview.md) ułatwiają programowanie w języku XML i udostępniają środowisko zapytań podobne do języka SQL.</span><span class="sxs-lookup"><span data-stu-id="8b719-114">[LINQ to XML (C#)](../../linq/linq-xml-overview.md) and [LINQ to XML (Visual Basic)](../../linq/linq-xml-overview.md) makes it easier to program with XML and provides a query experience that is similar to SQL.</span></span>

- <span data-ttu-id="8b719-115">**Rozszerzaln.**</span><span class="sxs-lookup"><span data-stu-id="8b719-115">**Extensibility.**</span></span> <span data-ttu-id="8b719-116">Klasy XML w .NET Framework są rozszerzalne przy użyciu abstrakcyjnych klas podstawowych i metod wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="8b719-116">The XML classes in the .NET Framework are extensible through the use of abstract base classes and virtual methods.</span></span> <span data-ttu-id="8b719-117">Na przykład można utworzyć klasę pochodną <xref:System.Xml.XmlUrlResolver> klasy, która przechowuje strumień pamięci podręcznej na dysku lokalnym.</span><span class="sxs-lookup"><span data-stu-id="8b719-117">For example, you can create a derived class of the <xref:System.Xml.XmlUrlResolver> class that stores the cache stream to the local disk.</span></span>

- <span data-ttu-id="8b719-118">**Architektura podłączana.**</span><span class="sxs-lookup"><span data-stu-id="8b719-118">**Pluggable architecture.**</span></span> <span data-ttu-id="8b719-119">.NET Framework zapewnia architekturę, w której składniki mogą korzystać ze sobą, a dane mogą być przesyłane strumieniowo między składnikami.</span><span class="sxs-lookup"><span data-stu-id="8b719-119">The .NET Framework provides an architecture in which components can utilize one another, and data can be streamed between components.</span></span> <span data-ttu-id="8b719-120">Na przykład magazyn danych, taki jak <xref:System.Xml.XPath.XPathDocument> <xref:System.Xml.XmlDocument> obiekt lub, może być przekształcony z <xref:System.Xml.Xsl.XslCompiledTransform> klasą, a dane wyjściowe można przesłać strumieniowo do innego magazynu lub zwrócić jako strumień z usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="8b719-120">For example, a data store, such as an <xref:System.Xml.XPath.XPathDocument> or <xref:System.Xml.XmlDocument> object, can be transformed with the <xref:System.Xml.Xsl.XslCompiledTransform> class, and the output can then be streamed either into another store or returned as a stream from a web service.</span></span>

- <span data-ttu-id="8b719-121">**Skuteczności.**</span><span class="sxs-lookup"><span data-stu-id="8b719-121">**Performance.**</span></span> <span data-ttu-id="8b719-122">W celu uzyskania lepszej wydajności aplikacji niektóre klasy XML w .NET Framework obsługują model oparty na strumieniu o następujących cechach:</span><span class="sxs-lookup"><span data-stu-id="8b719-122">For better app performance, some of the XML classes in the .NET Framework support a streaming-based model with the following characteristics:</span></span>

  - <span data-ttu-id="8b719-123">Minimalna pamięć podręczna do analizy modelu ściągania ( <xref:System.Xml.XmlReader> ).</span><span class="sxs-lookup"><span data-stu-id="8b719-123">Minimal caching for forward-only, pull-model parsing (<xref:System.Xml.XmlReader>).</span></span>

  - <span data-ttu-id="8b719-124">Walidacja tylko do przodu ( <xref:System.Xml.XmlReader> ).</span><span class="sxs-lookup"><span data-stu-id="8b719-124">Forward-only validation (<xref:System.Xml.XmlReader>).</span></span>

  - <span data-ttu-id="8b719-125">Nawigacja w stylu kursora, która minimalizuje Tworzenie węzłów w jednym węźle wirtualnym, a jednocześnie zapewnia losowy dostęp do dokumentu ( <xref:System.Xml.XPath.XPathNavigator> ).</span><span class="sxs-lookup"><span data-stu-id="8b719-125">Cursor style navigation that minimizes node creation to a single virtual node while providing random access to the document (<xref:System.Xml.XPath.XPathNavigator>).</span></span>

  <span data-ttu-id="8b719-126">Aby zapewnić lepszą wydajność, gdy jest wymagane przetwarzanie XSLT, można użyć <xref:System.Xml.XPath.XPathDocument> klasy, która jest zoptymalizowanym magazynem tylko do odczytu dla zapytań XPath zaprojektowanych do wydajnej pracy z <xref:System.Xml.Xsl.XslCompiledTransform> klasą.</span><span class="sxs-lookup"><span data-stu-id="8b719-126">For better performance whenever XSLT processing is required, you can use the <xref:System.Xml.XPath.XPathDocument> class, which is an optimized, read-only store for XPath queries designed to work efficiently with the <xref:System.Xml.Xsl.XslCompiledTransform> class.</span></span>

- <span data-ttu-id="8b719-127">**Integracja z usługą ADO.NET.**</span><span class="sxs-lookup"><span data-stu-id="8b719-127">**Integration with ADO.NET.**</span></span> <span data-ttu-id="8b719-128">Klasy XML i [ADO.NET](../../../framework/data/adonet/index.md) są ściśle zintegrowane do łączenia danych relacyjnych i XML.</span><span class="sxs-lookup"><span data-stu-id="8b719-128">The XML classes and [ADO.NET](../../../framework/data/adonet/index.md) are tightly integrated to bring together relational data and XML.</span></span> <span data-ttu-id="8b719-129"><xref:System.Data.DataSet>Klasa to pamięć podręczna danych pobieranych z bazy danych.</span><span class="sxs-lookup"><span data-stu-id="8b719-129">The <xref:System.Data.DataSet> class is an in-memory cache of data retrieved from a database.</span></span> <span data-ttu-id="8b719-130"><xref:System.Data.DataSet>Klasa ma możliwość odczytywania i pisania XML przy użyciu <xref:System.Xml.XmlReader> <xref:System.Xml.XmlWriter> klas i, aby zachować wewnętrzną strukturę schematu relacyjnego jako schematy XML (XSD) i wywnioskować strukturę schematu dokumentu XML.</span><span class="sxs-lookup"><span data-stu-id="8b719-130">The <xref:System.Data.DataSet> class has the ability to read and write XML by using the <xref:System.Xml.XmlReader> and <xref:System.Xml.XmlWriter> classes, to persist its internal relational schema structure as XML schemas (XSD), and to infer the schema structure of an XML document.</span></span>

## <a name="in-this-section"></a><span data-ttu-id="8b719-131">W tej sekcji</span><span class="sxs-lookup"><span data-stu-id="8b719-131">In This Section</span></span>

<span data-ttu-id="8b719-132">[Opcje przetwarzania XML](xml-processing-options.md) W tym artykule omówiono opcje przetwarzania danych XML.</span><span class="sxs-lookup"><span data-stu-id="8b719-132">[XML Processing Options](xml-processing-options.md) Discusses options for processing XML data.</span></span>

<span data-ttu-id="8b719-133">[Przetwarzanie danych XML w pamięci](processing-xml-data-in-memory.md) Omawia trzy modele przetwarzania danych XML w pamięci: [LINQ to XML (C#)](../../linq/linq-xml-overview.md) i [LINQ to XML (Visual Basic)](../../linq/linq-xml-overview.md), <xref:System.Xml.XmlDocument> klasy (na podstawie Document Object Model W3C) i <xref:System.Xml.XPath.XPathDocument> klasy (na podstawie modelu danych XPath).</span><span class="sxs-lookup"><span data-stu-id="8b719-133">[Processing XML Data In-Memory](processing-xml-data-in-memory.md) Discusses the three models for processing XML data in-memory: [LINQ to XML (C#)](../../linq/linq-xml-overview.md) and [LINQ to XML (Visual Basic)](../../linq/linq-xml-overview.md), the <xref:System.Xml.XmlDocument> class (based on the W3C Document Object Model), and the <xref:System.Xml.XPath.XPathDocument> class (based on the XPath data model).</span></span>

<span data-ttu-id="8b719-134">[Przekształcenia XSLT](xslt-transformations.md)</span><span class="sxs-lookup"><span data-stu-id="8b719-134">[XSLT Transformations](xslt-transformations.md)</span></span>\
<span data-ttu-id="8b719-135">Opisuje sposób korzystania z procesora XSLT.</span><span class="sxs-lookup"><span data-stu-id="8b719-135">Describes how to use the XSLT processor.</span></span>

<span data-ttu-id="8b719-136">[Model obiektów schematu XML (SOM)](xml-schema-object-model-som.md)</span><span class="sxs-lookup"><span data-stu-id="8b719-136">[XML Schema Object Model (SOM)](xml-schema-object-model-som.md)</span></span>\
<span data-ttu-id="8b719-137">Opisuje klasy używane do kompilowania schematów XML (XSD) i manipulowania nimi przez udostępnienie <xref:System.Xml.Schema.XmlSchema> klasy w celu załadowania i edytowania schematu.</span><span class="sxs-lookup"><span data-stu-id="8b719-137">Describes the classes used for building and manipulating XML Schemas (XSD) by providing an <xref:System.Xml.Schema.XmlSchema> class to load and edit a schema.</span></span>

<span data-ttu-id="8b719-138">[Integracja XML z danymi relacyjnymi i ADO.NET](xml-integration-with-relational-data-and-adonet.md)</span><span class="sxs-lookup"><span data-stu-id="8b719-138">[XML Integration with Relational Data and ADO.NET](xml-integration-with-relational-data-and-adonet.md)</span></span>\
<span data-ttu-id="8b719-139">Opisuje, w jaki sposób .NET Framework umożliwia dostęp synchroniczny do relacyjnych i hierarchicznych reprezentacji danych za pomocą <xref:System.Data.DataSet> obiektu i <xref:System.Xml.XmlDataDocument> obiektu.</span><span class="sxs-lookup"><span data-stu-id="8b719-139">Describes how the .NET Framework enables real-time, synchronous access to both the relational and hierarchical representations of data through the <xref:System.Data.DataSet> object and the <xref:System.Xml.XmlDataDocument> object.</span></span>

<span data-ttu-id="8b719-140">[Zarządzanie przestrzeniami nazw w dokumencie XML](managing-namespaces-in-an-xml-document.md)</span><span class="sxs-lookup"><span data-stu-id="8b719-140">[Managing Namespaces in an XML Document](managing-namespaces-in-an-xml-document.md)</span></span>\
<span data-ttu-id="8b719-141">Opisuje, w jaki sposób <xref:System.Xml.XmlNamespaceManager> Klasa jest używana do przechowywania i konserwowania informacji o przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="8b719-141">Describes how the <xref:System.Xml.XmlNamespaceManager> class is used to store and maintain namespace information.</span></span>

<span data-ttu-id="8b719-142">[Obsługa typów w klasach System.Xml](type-support-in-the-system-xml-classes.md)</span><span class="sxs-lookup"><span data-stu-id="8b719-142">[Type Support in the System.Xml Classes](type-support-in-the-system-xml-classes.md)</span></span>\
<span data-ttu-id="8b719-143">Opisuje sposób mapowania typów danych XML na typy CLR, sposób konwersji typów danych XML i inne funkcje obsługi typu w <xref:System.Xml> klasach.</span><span class="sxs-lookup"><span data-stu-id="8b719-143">Describes how XML data types map to CLR types, how to convert XML data types, and other type support features in the <xref:System.Xml> classes.</span></span>

## <a name="related-sections"></a><span data-ttu-id="8b719-144">Sekcje pokrewne</span><span class="sxs-lookup"><span data-stu-id="8b719-144">Related Sections</span></span>

<span data-ttu-id="8b719-145">[ADO.NET](../../../framework/data/adonet/index.md)</span><span class="sxs-lookup"><span data-stu-id="8b719-145">[ADO.NET](../../../framework/data/adonet/index.md)</span></span>\
<span data-ttu-id="8b719-146">Zawiera informacje na temat sposobu uzyskiwania dostępu do danych za pomocą ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="8b719-146">Provides information on how to access data using ADO.NET.</span></span>

<span data-ttu-id="8b719-147">[Bezpieczeństw](../../security/index.md)</span><span class="sxs-lookup"><span data-stu-id="8b719-147">[Security](../../security/index.md)</span></span>\
<span data-ttu-id="8b719-148">Zawiera omówienie systemu zabezpieczeń .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="8b719-148">Provides an overview of the .NET Framework security system.</span></span>
