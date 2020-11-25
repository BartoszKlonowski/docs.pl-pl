---
title: <add>, element dla <schemaImporterExtensions>
description: <add>Element dodaje typy używane przez klasę XmlSchemaImporter do mapowania typów XSD na typy .NET.
ms.date: 03/30/2017
helpviewer_keywords:
- XML serialization, configuration
- <add> element for <schemaImporterExtensions> element
ms.assetid: c828a558-094b-441e-9065-790b87315fa0
ms.openlocfilehash: b8a0775e9d33d59606b1150aa9a1b3b1026d4b0b
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95726447"
---
# <a name="add-element-for-schemaimporterextensions"></a>\<add>, element dla \<schemaImporterExtensions>

Dodaje typy używane przez program <xref:System.Xml.Serialization.XmlSchemaImporter> do mapowania typów XSD na typy .NET. Aby uzyskać więcej informacji na temat plików konfiguracji, zobacz [Schemat pliku konfiguracji](../../framework/configure-apps/file-schema/index.md).  
  
\<configuration>  
\<system.xml.serialization>  
\<schemaImporterExtensions>  
\<add>  
  
## <a name="syntax"></a>Składnia  
  
```xml  
<add name = "typeName" type="fully qualified type [,Version=version number] [,Culture=culture] [,PublicKeyToken= token]"/>  
```  
  
## <a name="attributes-and-elements"></a>Atrybuty i elementy  

 W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|  
|---------------|-----------------|  
|**Nazwij**|Prosta nazwa używana do znajdowania wystąpienia.|  
|**Wprowadź**|Wymagane. Określa klasę rozszerzenia schematu do dodania. Wartość atrybutu **typu** musi znajdować się w jednym wierszu i zawierać w pełni kwalifikowaną nazwę typu. Gdy zestaw znajduje się w globalnej pamięci podręcznej zestawów (GAC), musi również zawierać wersję, kulturę i token klucza publicznego podpisanego zestawu.|  
  
### <a name="child-elements"></a>Elementy podrzędne  

 Brak.  
  
### <a name="parent-elements"></a>Elementy nadrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|\<schemaImporterExtensions>|Zawiera typy, które są używane przez <xref:System.Xml.Serialization.XmlSchemaImporter>.|  
  
## <a name="example"></a>Przykład  

 Poniższy przykład kodu dodaje typ rozszerzenia, którego XmlSchemaImporter może używać podczas mapowania typów.  
  
```xml  
<configuration>  
  <system.xml.serialization>  
    <schemaImporterExtensions>  
       <add name="contoso" type="System.Web.Mobile.MobileCapabilities,
       System.Web.Mobile, Version=2.0.0.0, Culture=neutral,
       PublicKeyToken=b03f5f7f11d50a3a" />
    </schemaImporterExtensions>  
  </system.xml.serialization>  
</configuration>  
```  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Xml.Serialization.XmlSchemaImporter>
- [\<system.xml.serialization> Postaci](system-xml-serialization-element.md)
- [\<schemaImporterExtensions> Postaci](schemaimporterextensions-element.md)
