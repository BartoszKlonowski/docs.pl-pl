---
title: <Directives> — Element (.NET Native)
ms.date: 03/30/2017
ms.assetid: 444846f3-48d5-4341-a43e-69f7221389eb
ms.openlocfilehash: 524c30872e218f6428491507bbfb4ca54b6061b1
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96251103"
---
# <a name="directives-element-net-native"></a>\<Directives> — Element (.NET Native)

Element główny w każdym pliku dyrektywy środowiska uruchomieniowego dla .NET Native.  
  
 `<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">`
  
## <a name="syntax"></a>Składnia  
  
```xml  
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
   <!-- child elements -->
</Directives>  
```  
  
## <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|  
|---------------|-----------------|  
|`xmlns`|Przestrzeń nazw XML. Jego wartość jest zawsze `http://schemas.microsoft.com/netfx/2013/01/metadata` .|  
  
## <a name="child-elements"></a>Elementy podrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|[\<Application>](application-element-net-native.md)|Służy jako kontener dla typów i składowych dla całej aplikacji, których metadane są dostępne do odbicia.|  
|[\<Library>](library-element-net-native.md)|Definiuje zestaw, którego typy podrzędne i elementy członkowskie typu wymagają metadanych w czasie wykonywania.|  
  
## <a name="remarks"></a>Uwagi  

 Każdy plik dyrektywy środowiska uruchomieniowego może zawierać tylko jeden `<Directives>` element.  
  
 `<Directives>`Element może zawierać zero lub jeden [\<Application>](application-element-net-native.md) element oraz zero, jeden lub więcej [\<Library>](library-element-net-native.md) elementów.  
  
## <a name="see-also"></a>Zobacz też

- [Dokumentacja pliku konfiguracji dyrektyw środowiska uruchomieniowego (rd.xml)](runtime-directives-rd-xml-configuration-file-reference.md)
- [Elementy dyrektyw środowiska uruchomieniowego](runtime-directive-elements.md)
