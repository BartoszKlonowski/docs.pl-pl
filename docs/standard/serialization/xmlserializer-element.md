---
title: <xmlSerializer> Element
description: <xmlSerializer>Element określa, czy jest wykonywane dodatkowe sprawdzanie postępu elementu XmlSerializer.
ms.date: 03/30/2017
helpviewer_keywords:
- <xmlSerializer> element
- XML serialization, configuration
- xmlSerializer element
ms.assetid: d129d10c-3eb7-45d9-8098-5fa853825e47
ms.openlocfilehash: 6f368880c97a21dc3e9593ecb2319d265a1b8932
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95676494"
---
# <a name="xmlserializer-element"></a>\<xmlSerializer> Element

Określa, czy dodatkowe wyboru postęp <xref:System.Xml.Serialization.XmlSerializer> jest wykonywane.  
  
 \<configuration>  
\<system.xml.serialization>  
  
## <a name="syntax"></a>Składnia  
  
```xml  
<xmlSerializer checkDeserializerAdvance = "true|false" />  
```  
  
## <a name="attributes-and-elements"></a>Atrybuty i elementy  

 W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|  
|---------------|-----------------|  
|**checkDeserializeAdvances**|Określa, czy postęp <xref:System.Xml.Serialization.XmlSerializer> jest zaznaczone. Atrybut "prawda" lub "false". Wartość domyślna to "true".|  
|**useLegacySerializationGeneration**|Określa, czy <xref:System.Xml.Serialization.XmlSerializer> używa Generowanie starszego serializacji, generująca zestawy zapis do PLiku kodu C# i zestawiania do zestawu. Wartość domyślna to **false**.|  
  
### <a name="child-elements"></a>Elementy podrzędne  

 Brak.  
  
### <a name="parent-elements"></a>Elementy nadrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|[\<system.xml.serialization> Postaci](system-xml-serialization-element.md)|Zawiera ustawienia konfiguracji dla <xref:System.Xml.Serialization.XmlSerializer> i <xref:System.Xml.Serialization.XmlSchemaImporter> klasy.|  
  
## <a name="remarks"></a>Uwagi  

 Domyślnie <xref:System.Xml.Serialization.XmlSerializer> zapewnia dodatkową warstwę zabezpieczeń przed potencjalnym atakom typu odmowa usługi podczas deserializacji niezaufanych danych. Robi to za pomocą próby wykrycia podczas deserializacji w pętli nieskończonej. W przypadku wykrycia takiego warunku zostanie zgłoszony wyjątek z następującym komunikatem: "błąd wewnętrzny: deserializacja nie powiodła się przed strumieniem bazowym".  
  
 Odbieranie ten komunikat nie musi oznaczać, że typu "odmowa usługi" jest w toku. W niektórych sytuacjach szczególnych mechanizm wykrywania pętli nieskończonej tworzy fałszywego ostrzeżenia i wyjątku wiarygodnego wiadomości przychodzącej. Jeśli okaże się, że w konkretnej aplikacji legalne komunikaty są odrzucane przez tę dodatkową warstwę ochrony, ustaw atrybut **checkDeserializeAdvances** na wartość "false".  
  
## <a name="example"></a>Przykład  

 Poniższy przykład kodu ustawia atrybut **checkDeserializeAdvances** na wartość "false".  
  
```xml  
<configuration>  
  <system.xml.serialization>  
    <xmlSerializer checkDeserializeAdvances="false" />  
  </system.xml.serialization>  
</configuration>  
```  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Xml.Serialization.XmlSerializer>
- [\<system.xml.serialization> Postaci](system-xml-serialization-element.md)
- [Serializacja XML i SOAP](xml-and-soap-serialization.md)
