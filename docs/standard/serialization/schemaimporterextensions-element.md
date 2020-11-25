---
title: <schemaImporterExtensions> Element
description: <schemaImporterExtensions>Element zawiera typy, które są używane przez XmlSchemaImporter do mapowania typów XSD na typy .NET.
ms.date: 03/30/2017
helpviewer_keywords:
- XML serialization, configuration
- schemaImporterExtensions element
- <schemaImporterExtensions> element
ms.assetid: 465ef2a0-f909-4ac1-9a56-0ead5c849698
ms.openlocfilehash: 6b644ed1112b748be4dd301d6fa6f2a6416dc67e
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95722144"
---
# <a name="schemaimporterextensions-element"></a><span data-ttu-id="06ed3-103">\<schemaImporterExtensions>, element</span><span class="sxs-lookup"><span data-stu-id="06ed3-103">\<schemaImporterExtensions> element</span></span>

<span data-ttu-id="06ed3-104">Zawiera typy, które są używane przez program <xref:System.Xml.Serialization.XmlSchemaImporter> do mapowania typów XSD na typy .NET.</span><span class="sxs-lookup"><span data-stu-id="06ed3-104">Contains types that are used by the <xref:System.Xml.Serialization.XmlSchemaImporter> for mapping of XSD types to .NET types.</span></span> <span data-ttu-id="06ed3-105">Aby uzyskać więcej informacji na temat plików konfiguracji, zobacz [Schemat pliku konfiguracji](../../framework/configure-apps/file-schema/index.md).</span><span class="sxs-lookup"><span data-stu-id="06ed3-105">For more information about configuration files, see [Configuration File Schema](../../framework/configure-apps/file-schema/index.md).</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="06ed3-106">Składnia</span><span class="sxs-lookup"><span data-stu-id="06ed3-106">Syntax</span></span>  
  
```xml  
<schemaImporterExtensions>  
    <!-- Add types -->  
</schemaImporterExtensions>  
```  
  
## <a name="child-elements"></a><span data-ttu-id="06ed3-107">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="06ed3-107">Child Elements</span></span>  
  
|<span data-ttu-id="06ed3-108">Element</span><span class="sxs-lookup"><span data-stu-id="06ed3-108">Element</span></span>|<span data-ttu-id="06ed3-109">Opis</span><span class="sxs-lookup"><span data-stu-id="06ed3-109">Description</span></span>|  
|-------------|-----------------|  
|[<span data-ttu-id="06ed3-110">\<add> Element dla \<schemaImporterExtensions></span><span class="sxs-lookup"><span data-stu-id="06ed3-110">\<add> Element for \<schemaImporterExtensions></span></span>](add-element-for-schemaimporterextensions.md)|<span data-ttu-id="06ed3-111">Dodaje typy, które są używane przez program <xref:System.Xml.Serialization.XmlSchemaImporter> do tworzenia mapowań.</span><span class="sxs-lookup"><span data-stu-id="06ed3-111">Adds types that are used by the <xref:System.Xml.Serialization.XmlSchemaImporter> to create mappings.</span></span>|  
  
## <a name="parent-elements"></a><span data-ttu-id="06ed3-112">Elementy nadrzędne</span><span class="sxs-lookup"><span data-stu-id="06ed3-112">Parent Elements</span></span>  
  
|<span data-ttu-id="06ed3-113">Element</span><span class="sxs-lookup"><span data-stu-id="06ed3-113">Element</span></span>|<span data-ttu-id="06ed3-114">Opis</span><span class="sxs-lookup"><span data-stu-id="06ed3-114">Description</span></span>|  
|-------------|-----------------|  
|[<span data-ttu-id="06ed3-115">\<system.xml.serialization> Postaci</span><span class="sxs-lookup"><span data-stu-id="06ed3-115">\<system.xml.serialization> Element</span></span>](system-xml-serialization-element.md)|<span data-ttu-id="06ed3-116">Element najwyższego poziomu do sterowania serializacji XML.</span><span class="sxs-lookup"><span data-stu-id="06ed3-116">The top-level element for controlling XML serialization.</span></span>|  
  
## <a name="example"></a><span data-ttu-id="06ed3-117">Przykład</span><span class="sxs-lookup"><span data-stu-id="06ed3-117">Example</span></span>  

 <span data-ttu-id="06ed3-118">Poniższy przykład kodu ilustruje sposób dodawania typów, które są używane przez <xref:System.Xml.Serialization.XmlSchemaImporter> podczas mapowania typów XSD na typy .NET.</span><span class="sxs-lookup"><span data-stu-id="06ed3-118">The following code example illustrates how to add types that are used by the <xref:System.Xml.Serialization.XmlSchemaImporter> when mapping XSD types to .NET types.</span></span>  
  
```xml  
<system.xml.serialization>  
    <schemaImporterExtensions>  
        <add name = "MobileCapabilities" type =
        "System.Web.Mobile.MobileCapabilities,
        System.Web.Mobile, Version - 2.0.0.0, Culture = neutral,
        PublicKeyToken = b03f5f6f11d40a3a" />  
    </schemaImporterExtensions>  
</system.xml.serialization>  
```  
  
## <a name="see-also"></a><span data-ttu-id="06ed3-119">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="06ed3-119">See also</span></span>

- <xref:System.Xml.Serialization.XmlSchemaImporter>
- <xref:System.Xml.Serialization.Configuration.DateTimeSerializationSection.DateTimeSerializationMode>
- [<span data-ttu-id="06ed3-120">Schemat pliku konfiguracji</span><span class="sxs-lookup"><span data-stu-id="06ed3-120">Configuration File Schema</span></span>](../../framework/configure-apps/file-schema/index.md)
- [<span data-ttu-id="06ed3-121">\<dateTimeSerialization> Postaci</span><span class="sxs-lookup"><span data-stu-id="06ed3-121">\<dateTimeSerialization> Element</span></span>](datetimeserialization-element.md)
- [<span data-ttu-id="06ed3-122">\<add> Element dla \<schemaImporterExtensions></span><span class="sxs-lookup"><span data-stu-id="06ed3-122">\<add> Element for \<schemaImporterExtensions></span></span>](add-element-for-schemaimporterextensions.md)
- [<span data-ttu-id="06ed3-123">\<system.xml.serialization> Postaci</span><span class="sxs-lookup"><span data-stu-id="06ed3-123">\<system.xml.serialization> Element</span></span>](system-xml-serialization-element.md)
