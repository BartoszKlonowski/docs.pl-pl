---
title: Atrybuty kontrolujące zakodowaną serializację SOAP
description: W tym artykule wymieniono specjalny zestaw atrybutów znalezionych w System.Xml. Przestrzeń nazw serializacji musi być zgodna ze specyfikacją protokołu SOAP.
ms.date: 03/30/2017
helpviewer_keywords:
- SOAP, XML serialization
- XML serialization, SOAP
- XML serialization, attributes
- attributes [.NET], XML serialization
- serialization, attributes
ms.assetid: 93ee258c-9c0f-4a08-897c-c10db7a00f91
ms.openlocfilehash: 69a9d1c8734a393b576cf87e7e05ef92c10120c8
ms.sourcegitcommit: 74d05613d6c57106f83f82ce8ee71176874ea3f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/03/2020
ms.locfileid: "93282045"
---
# <a name="attributes-that-control-encoded-soap-serialization"></a><span data-ttu-id="50f02-103">Atrybuty kontrolujące zakodowaną serializację SOAP</span><span class="sxs-lookup"><span data-stu-id="50f02-103">Attributes That Control Encoded SOAP Serialization</span></span>

<span data-ttu-id="50f02-104">Dokument organizacja World Wide Web Consortium (W3C) o nazwie [Simple Object Access Protocol (SOAP) 1,1](https://www.w3.org/TR/2000/NOTE-SOAP-20000508/) zawiera sekcję opcjonalną (sekcja 5) opisującą sposób kodowania parametrów protokołu SOAP.</span><span class="sxs-lookup"><span data-stu-id="50f02-104">The World Wide Web Consortium (W3C) document named [Simple Object Access Protocol (SOAP) 1.1](https://www.w3.org/TR/2000/NOTE-SOAP-20000508/) contains an optional section (section 5) that describes how SOAP parameters can be encoded.</span></span> <span data-ttu-id="50f02-105">Aby zachować zgodność z sekcją 5 specyfikacji, należy użyć specjalnego zestawu atrybutów znalezionych w <xref:System.Xml.Serialization> przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="50f02-105">To conform to section 5 of the specification, you must use a special set of attributes found in the <xref:System.Xml.Serialization> namespace.</span></span> <span data-ttu-id="50f02-106">Zastosuj te atrybuty stosownie do klas i elementów członkowskich klas, a następnie użyj <xref:System.Xml.Serialization.XmlSerializer> do serializacji wystąpień klasy lub klas.</span><span class="sxs-lookup"><span data-stu-id="50f02-106">Apply those attributes as appropriate to classes and members of classes, and then use the <xref:System.Xml.Serialization.XmlSerializer> to serialize instances of the class or classes.</span></span>

<span data-ttu-id="50f02-107">W poniższej tabeli przedstawiono atrybuty, w których można je zastosować i co robią.</span><span class="sxs-lookup"><span data-stu-id="50f02-107">The following table shows the attributes, where they can be applied, and what they do.</span></span> <span data-ttu-id="50f02-108">Aby uzyskać więcej informacji o używaniu tych atrybutów do kontrolowania serializacji XML, zobacz [How to: deserializacji obiektu jako SOAP-Encoded strumienia XML](how-to-serialize-an-object-as-a-soap-encoded-xml-stream.md) i [instrukcje: zastępowanie ZAKODOWANEJ serializacji XML protokołu SOAP](how-to-override-encoded-soap-xml-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="50f02-108">For more information about using these attributes to control XML serialization, see [How to: Serialize an Object as a SOAP-Encoded XML Stream](how-to-serialize-an-object-as-a-soap-encoded-xml-stream.md) and [How to: Override Encoded SOAP XML Serialization](how-to-override-encoded-soap-xml-serialization.md).</span></span>

<span data-ttu-id="50f02-109">Aby uzyskać więcej informacji na temat atrybutów, zobacz [atrybuty](../attributes/index.md).</span><span class="sxs-lookup"><span data-stu-id="50f02-109">For more information about attributes, see [Attributes](../attributes/index.md).</span></span>

|<span data-ttu-id="50f02-110">Atrybut</span><span class="sxs-lookup"><span data-stu-id="50f02-110">Attribute</span></span>|<span data-ttu-id="50f02-111">Dotyczy</span><span class="sxs-lookup"><span data-stu-id="50f02-111">Applies to</span></span>|<span data-ttu-id="50f02-112">Określa</span><span class="sxs-lookup"><span data-stu-id="50f02-112">Specifies</span></span>|
|---------------|----------------|---------------|
|<xref:System.Xml.Serialization.SoapAttributeAttribute>|<span data-ttu-id="50f02-113">Pole publiczne, właściwość, parametru lub wartości zwracanej.</span><span class="sxs-lookup"><span data-stu-id="50f02-113">Public field, property, parameter, or return value.</span></span>|<span data-ttu-id="50f02-114">Składowa klasy będzie serializowana jako atrybut XML.</span><span class="sxs-lookup"><span data-stu-id="50f02-114">The class member will be serialized as an XML attribute.</span></span>|
|<xref:System.Xml.Serialization.SoapElementAttribute>|<span data-ttu-id="50f02-115">Pole publiczne, właściwość, parametru lub wartości zwracanej.</span><span class="sxs-lookup"><span data-stu-id="50f02-115">Public field, property, parameter, or return value.</span></span>|<span data-ttu-id="50f02-116">Klasa będzie serializowana jako XML element.</span><span class="sxs-lookup"><span data-stu-id="50f02-116">The class will be serialized as an XML element.</span></span>|
|<xref:System.Xml.Serialization.SoapEnumAttribute>|<span data-ttu-id="50f02-117">Pole publicznej jest identyfikatorem wyliczenia.</span><span class="sxs-lookup"><span data-stu-id="50f02-117">Public field that is an enumeration identifier.</span></span>|<span data-ttu-id="50f02-118">Nazwa elementu element członkowski wyliczenia.</span><span class="sxs-lookup"><span data-stu-id="50f02-118">The element name of an enumeration member.</span></span>|
|<xref:System.Xml.Serialization.SoapIgnoreAttribute>|<span data-ttu-id="50f02-119">Właściwości publiczne i pola.</span><span class="sxs-lookup"><span data-stu-id="50f02-119">Public properties and fields.</span></span>|<span data-ttu-id="50f02-120">Właściwości lub pól mają być ignorowane, gdy klasa zawierająca jest serializowana.</span><span class="sxs-lookup"><span data-stu-id="50f02-120">The property or field should be ignored when the containing class is serialized.</span></span>|
|<xref:System.Xml.Serialization.SoapIncludeAttribute>|<span data-ttu-id="50f02-121">Klasa pochodna publicznego deklaracje i metod publicznych w dokumentach sieci Web Services Description Language (WSDL).</span><span class="sxs-lookup"><span data-stu-id="50f02-121">Public-derived class declarations and public methods for Web Services Description Language (WSDL) documents.</span></span>|<span data-ttu-id="50f02-122">Typ mają zostać uwzględnione podczas generowania schematów (do rozpoznany po serializacji).</span><span class="sxs-lookup"><span data-stu-id="50f02-122">The type should be included when generating schemas (to be recognized when serialized).</span></span>|
|<xref:System.Xml.Serialization.SoapTypeAttribute>|<span data-ttu-id="50f02-123">Klasa publiczna deklaracji.</span><span class="sxs-lookup"><span data-stu-id="50f02-123">Public class declarations.</span></span>|<span data-ttu-id="50f02-124">Klasa powinien zostać Zserializowany jako typ XML.</span><span class="sxs-lookup"><span data-stu-id="50f02-124">The class should be serialized as an XML type.</span></span>|

## <a name="see-also"></a><span data-ttu-id="50f02-125">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="50f02-125">See also</span></span>

- [<span data-ttu-id="50f02-126">Serializacja XML i SOAP</span><span class="sxs-lookup"><span data-stu-id="50f02-126">XML and SOAP Serialization</span></span>](xml-and-soap-serialization.md)
- [<span data-ttu-id="50f02-127">Instrukcje: Serializacja obiektu jako kodowanego strumienia XML protokołu SOAP</span><span class="sxs-lookup"><span data-stu-id="50f02-127">How to: Serialize an Object as a SOAP-Encoded XML Stream</span></span>](how-to-serialize-an-object-as-a-soap-encoded-xml-stream.md)
- [<span data-ttu-id="50f02-128">Instrukcje: Przesłanianie zakodowanej serializacji XML protokołu SOAP</span><span class="sxs-lookup"><span data-stu-id="50f02-128">How to: Override Encoded SOAP XML Serialization</span></span>](how-to-override-encoded-soap-xml-serialization.md)
- [<span data-ttu-id="50f02-129">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="50f02-129">Attributes</span></span>](../attributes/index.md)
- <xref:System.Xml.Serialization.XmlSerializer>
- [<span data-ttu-id="50f02-130">Instrukcje: Serializacja obiektu</span><span class="sxs-lookup"><span data-stu-id="50f02-130">How to: Serialize an Object</span></span>](how-to-serialize-an-object.md)
- [<span data-ttu-id="50f02-131">Instrukcje: Deserializacja obiektu</span><span class="sxs-lookup"><span data-stu-id="50f02-131">How to: Deserialize an Object</span></span>](how-to-deserialize-an-object.md)
