---
title: Odczytywanie i zapisywanie schematów XML
description: Odczytuj i zapisuj schematy języka definicji schematu XML (XSD) z plików lub innych źródeł w programie .NET przy użyciu interfejsu API modelu obiektów schematu (SOM).
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
ms.assetid: b5757c4a-ea59-467e-ac62-be2bfe24eb77
ms.openlocfilehash: ae951efafd68d0ddf4f74876edd4c12564d68dde
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94830886"
---
# <a name="reading-and-writing-xml-schemas"></a><span data-ttu-id="7a9b2-103">Odczytywanie i zapisywanie schematów XML</span><span class="sxs-lookup"><span data-stu-id="7a9b2-103">Reading and Writing XML Schemas</span></span>
<span data-ttu-id="7a9b2-104">Za pomocą interfejsu API modelu Object Model (SOM) można odczytywać i zapisywać schematy języka definicji schematu XML (XSD) z plików lub innych źródeł oraz tworzyć schematy XML w pamięci przy użyciu klas w <xref:System.Xml.Schema?displayProperty=nameWithType> przestrzeni nazw, które są mapowane na struktury zdefiniowane w zaleceniu schematu xml organizacja World Wide Web Consortium (W3C).</span><span class="sxs-lookup"><span data-stu-id="7a9b2-104">The Schema Object Model (SOM) API can be used to read and write XML Schema definition language (XSD) schemas from files or other sources and build XML schemas in-memory using the classes in the <xref:System.Xml.Schema?displayProperty=nameWithType> namespace that map to the structures defined in the World Wide Web Consortium (W3C) XML Schema Recommendation.</span></span>  
  
## <a name="reading-and-writing-xml-schemas"></a><span data-ttu-id="7a9b2-105">Odczytywanie i zapisywanie schematów XML</span><span class="sxs-lookup"><span data-stu-id="7a9b2-105">Reading and Writing XML Schemas</span></span>  
 <span data-ttu-id="7a9b2-106"><xref:System.Xml.Schema.XmlSchema>Klasa zawiera <xref:System.Xml.Schema.XmlSchema.Read%2A> <xref:System.Xml.Schema.XmlSchema.Write%2A> metody i do odczytywania i zapisywania schematów XML.</span><span class="sxs-lookup"><span data-stu-id="7a9b2-106">The <xref:System.Xml.Schema.XmlSchema> class provides the <xref:System.Xml.Schema.XmlSchema.Read%2A> and <xref:System.Xml.Schema.XmlSchema.Write%2A> methods to read and write XML schemas.</span></span> <span data-ttu-id="7a9b2-107"><xref:System.Xml.Schema.XmlSchema.Read%2A>Metoda zwraca <xref:System.Xml.Schema.XmlSchema> obiekt reprezentujący schemat XML i przyjmuje opcjonalnie <xref:System.Xml.Schema.ValidationEventHandler> jako parametr obsługujący ostrzeżenia i błędy walidacji schematu podczas odczytywania schematu XML.</span><span class="sxs-lookup"><span data-stu-id="7a9b2-107">The <xref:System.Xml.Schema.XmlSchema.Read%2A> method returns an <xref:System.Xml.Schema.XmlSchema> object representing the XML schema and takes an optional <xref:System.Xml.Schema.ValidationEventHandler> as a parameter to handle schema validation warnings and errors encountered while reading an XML schema.</span></span>  
  
 <span data-ttu-id="7a9b2-108"><xref:System.Xml.Schema.XmlSchema.Write%2A>Metoda zapisuje schematy XML do <xref:System.IO.Stream> <xref:System.IO.TextWriter> i <xref:System.Xml.XmlWriter> obiektów i może przyjmować opcjonalny <xref:System.Xml.XmlNamespaceManager> obiekt jako parametr.</span><span class="sxs-lookup"><span data-stu-id="7a9b2-108">The <xref:System.Xml.Schema.XmlSchema.Write%2A> method writes XML schemas to <xref:System.IO.Stream>, <xref:System.IO.TextWriter> and <xref:System.Xml.XmlWriter> objects and can take an optional <xref:System.Xml.XmlNamespaceManager> object as a parameter.</span></span> <span data-ttu-id="7a9b2-109">Służy <xref:System.Xml.XmlNamespaceManager> do obsługi przestrzeni nazw napotkanych w schemacie XML.</span><span class="sxs-lookup"><span data-stu-id="7a9b2-109">An <xref:System.Xml.XmlNamespaceManager> is used to handle namespaces encountered in an XML schema.</span></span> <span data-ttu-id="7a9b2-110">Aby uzyskać więcej informacji na temat <xref:System.Xml.XmlNamespaceManager> klasy, zobacz [Zarządzanie przestrzeniami nazw w dokumencie XML](managing-namespaces-in-an-xml-document.md).</span><span class="sxs-lookup"><span data-stu-id="7a9b2-110">For more information about the <xref:System.Xml.XmlNamespaceManager> class, see [Managing Namespaces in an XML Document](managing-namespaces-in-an-xml-document.md).</span></span>  
  
 <span data-ttu-id="7a9b2-111">Poniższy przykład kodu ilustruje odczytywanie i zapisywanie schematów XML z i do pliku.</span><span class="sxs-lookup"><span data-stu-id="7a9b2-111">The following code example illustrates reading and writing XML schemas from and to a file.</span></span> <span data-ttu-id="7a9b2-112">Przykładowy kod pobiera `example.xsd` plik, odczytuje go do <xref:System.Xml.Schema.XmlSchema> obiektu za pomocą `static` <xref:System.Xml.Schema.XmlSchema.Read%2A> metody, a następnie zapisuje plik do konsoli programu i nowego `new.xsd` pliku.</span><span class="sxs-lookup"><span data-stu-id="7a9b2-112">The code example takes the `example.xsd` file, reads it into an <xref:System.Xml.Schema.XmlSchema> object using the `static`<xref:System.Xml.Schema.XmlSchema.Read%2A> method, and then writes the file to the console and a new `new.xsd` file.</span></span> <span data-ttu-id="7a9b2-113">Przykład kodu dostarcza także <xref:System.Xml.Schema.ValidationEventHandler> jako parametr do `static` <xref:System.Xml.Schema.XmlSchema.Read%2A> metody do obsługi wszelkich ostrzeżeń lub błędów walidacji schematu podczas odczytywania schematu XML.</span><span class="sxs-lookup"><span data-stu-id="7a9b2-113">The code example also provides a <xref:System.Xml.Schema.ValidationEventHandler> as a parameter to the `static`<xref:System.Xml.Schema.XmlSchema.Read%2A> method to handle any schema validation warnings or errors encountered while reading the XML schema.</span></span> <span data-ttu-id="7a9b2-114">Jeśli <xref:System.Xml.Schema.ValidationEventHandler> nie określono ( `null` ), nie są zgłaszane żadne ostrzeżenia ani błędy.</span><span class="sxs-lookup"><span data-stu-id="7a9b2-114">If the <xref:System.Xml.Schema.ValidationEventHandler> is not specified (`null`), no warnings or errors are reported.</span></span>  
  
 [!code-cpp[XmlSchemaReadWriteExample#1](../../../../samples/snippets/cpp/VS_Snippets_Data/XmlSchemaReadWriteExample/CPP/XmlSchemaReadWriteExample.cpp#1)]
 [!code-csharp[XmlSchemaReadWriteExample#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XmlSchemaReadWriteExample/CS/XmlSchemaReadWriteExample.cs#1)]
 [!code-vb[XmlSchemaReadWriteExample#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XmlSchemaReadWriteExample/VB/XmlSchemaReadWriteExample.vb#1)]  
  
 <span data-ttu-id="7a9b2-115">Przykład przyjmuje `example.xsd` jako dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="7a9b2-115">The example takes the `example.xsd` as input.</span></span>  
  
```xml  
<?xml version="1.0"?>  
<xs:schema id="play" targetNamespace="http://tempuri.org/play.xsd" elementFormDefault="qualified" xmlns="http://tempuri.org/play.xsd" xmlns:xs="http://www.w3.org/2001/XMLSchema">  
    <xs:element name='myShoeSize'>  
        <xs:complexType>  
            <xs:simpleContent>  
                <xs:extension base='xs:decimal'>  
                    <xs:attribute name='sizing' type='xs:string' />  
                </xs:extension>  
            </xs:simpleContent>  
        </xs:complexType>  
    </xs:element>  
</xs:schema>  
```  
  
## <a name="see-also"></a><span data-ttu-id="7a9b2-116">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="7a9b2-116">See also</span></span>

- [<span data-ttu-id="7a9b2-117">Model SOM (XML Schema Object Model) ― omówienie</span><span class="sxs-lookup"><span data-stu-id="7a9b2-117">XML Schema Object Model Overview</span></span>](xml-schema-object-model-overview.md)
- [<span data-ttu-id="7a9b2-118">Tworzenie schematów XML</span><span class="sxs-lookup"><span data-stu-id="7a9b2-118">Building XML Schemas</span></span>](building-xml-schemas.md)
- [<span data-ttu-id="7a9b2-119">Przechodzenie schematów XML</span><span class="sxs-lookup"><span data-stu-id="7a9b2-119">Traversing XML Schemas</span></span>](traversing-xml-schemas.md)
- [<span data-ttu-id="7a9b2-120">Edytowanie schematów XML</span><span class="sxs-lookup"><span data-stu-id="7a9b2-120">Editing XML Schemas</span></span>](editing-xml-schemas.md)
- [<span data-ttu-id="7a9b2-121">Uwzględnianie lub importowanie schematów XML</span><span class="sxs-lookup"><span data-stu-id="7a9b2-121">Including or Importing XML Schemas</span></span>](including-or-importing-xml-schemas.md)
- [<span data-ttu-id="7a9b2-122">Klasa XmlSchemaSet na potrzeby kompilacji schematu</span><span class="sxs-lookup"><span data-stu-id="7a9b2-122">XmlSchemaSet for Schema Compilation</span></span>](xmlschemaset-for-schema-compilation.md)
- [<span data-ttu-id="7a9b2-123">Zestaw informacji po kompilacji schematu</span><span class="sxs-lookup"><span data-stu-id="7a9b2-123">Post-Schema Compilation Infoset</span></span>](post-schema-compilation-infoset.md)
- [<span data-ttu-id="7a9b2-124">Zarządzanie przestrzeniami nazw w dokumencie XML</span><span class="sxs-lookup"><span data-stu-id="7a9b2-124">Managing Namespaces in an XML Document</span></span>](managing-namespaces-in-an-xml-document.md)
