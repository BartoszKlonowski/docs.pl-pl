---
title: <extensions> Paragraf
ms.date: 03/30/2017
ms.assetid: 53a59fb6-dede-47ec-9384-b3c2e8f0c1fa
ms.openlocfilehash: f3eb5d446291dfa6b7c8e0f1ee2b6a5cf53c2162
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91185785"
---
# <a name="extensions-section"></a>\<extensions> Paragraf

Ta sekcja konfiguracji zawiera kolekcję rozszerzeń, które umożliwiają użytkownikowi tworzenie powiązań zdefiniowanych przez użytkownika, zachowań i innych aspektów rozszerzeń.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<extensions>**  
  
## <a name="syntax"></a>Składnia  
  
```xml  
<system.serviceModel>
  <extensions>
    <bindingExtensions>
    </bindingExtensions>
    <behaviorExtensions>
    </behaviorExtensions>
    <bindingElementExtensions>
    </bindingElementExtensions>
    <endpointExtensions>
    </endpointExtensions>
  </extensions>
</system.serviceModel>
```  
  
## <a name="attributes-and-elements"></a>Atrybuty i elementy  

 W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.  
  
### <a name="attributes"></a>Atrybuty  

 Brak.  
  
### <a name="child-elements"></a>Elementy podrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|[\<behaviorExtensions>](behaviorextensions.md)|Ta sekcja zawiera elementy podrzędne, które określają rozszerzenia zachowań, które umożliwiają użytkownikowi dostosowanie zachowań usługi lub punktów końcowych.|  
|[\<bindingElementExtensions>](bindingelementextensions.md)|Ta sekcja umożliwia korzystanie z niestandardowego elementu powiązania z pliku konfiguracji komputera lub aplikacji.|  
|[\<bindingExtensions>](bindingextensions.md)|Ta sekcja zawiera elementy podrzędne, które określają rozszerzenia powiązań, które umożliwiają użytkownikowi dostosowanie powiązań.|  
|[\<endpointExtensions>](endpointextensions.md)|Ta sekcja zawiera elementy podrzędne, które rejestrują standardowe punkty końcowe.|  
  
### <a name="parent-elements"></a>Elementy nadrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|System.ServiceModel|Element główny wszystkich elementów konfiguracji WCF.|
