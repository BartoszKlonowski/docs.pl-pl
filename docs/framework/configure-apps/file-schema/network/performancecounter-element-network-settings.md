---
title: <performanceCounters>, element (ustawienia sieci)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/settings/performanceCounters
- http://schemas.microsoft.com/.NetConfiguration/v2.0#performanceCounters
helpviewer_keywords:
- performanceCounters element
ms.assetid: 3afa1586-e1b8-473d-8985-c3fc90cf561b
ms.openlocfilehash: 584bdafbbd60303401cbc6ad96b8654fe11c7077
ms.sourcegitcommit: a8a205034eeffc7c3e1bdd6f506a75b0f7099ebf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2020
ms.locfileid: "91756263"
---
# <a name="performancecounters-element-network-settings"></a>\<performanceCounters>, element (ustawienia sieci)

Włącza lub wyłącza liczniki wydajności sieci.  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.net>**](system-net-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<settings>**](settings-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<performanceCounters>**

## <a name="syntax"></a>Składnia  
  
```xml  
<performanceCounters  
  enabled="true|false"  
/>  
```  
  
## <a name="attributes-and-elements"></a>Atrybuty i elementy  

 W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|  
|---------------|-----------------|  
|`enabled`|Określa, czy są włączone liczniki wydajności sieci. Wartość domyślna to `false`.|  
  
### <a name="child-elements"></a>Elementy podrzędne  

 Brak.  
  
### <a name="parent-elements"></a>Elementy nadrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|[ustawienia](settings-element-network-settings.md)|Konfiguruje podstawowe opcje sieci dla <xref:System.Net> przestrzeni nazw.|  
  
## <a name="remarks"></a>Uwagi  

 Tego elementu można użyć w pliku konfiguracyjnym aplikacji lub pliku konfiguracji komputera (Machine.config).  
  
 Liczniki wydajności sieci muszą być włączone w pliku konfiguracji, który ma być używany. Wszystkie liczniki wydajności sieci są włączone lub wyłączone przy użyciu jednego ustawienia w pliku konfiguracji. Nie można włączyć lub wyłączyć poszczególnych liczników wydajności sieci. Aby uzyskać więcej informacji na temat określonych liczników wydajności sieci, zobacz [Network Performance Counters](../../../debug-trace-profile/performance-counters.md#networking-performance-counters).  
  
 Wartością domyślną jest to, że liczniki wydajności sieci są wyłączone.  
  
 <xref:System.Net.Configuration.PerformanceCountersElement.Enabled%2A?displayProperty=nameWithType>Właściwość może służyć do uzyskiwania bieżącej wartości **włączonego** atrybutu z odpowiednich plików konfiguracji.  
  
## <a name="example"></a>Przykład  

 Poniższy przykład pokazuje, jak skonfigurować <xref:System.Net> i powiązane przestrzenie nazw w celu włączenia liczników wydajności sieci.  
  
```xml  
<configuration>  
  <system.net>  
    <settings>  
      <performanceCounters  
        enabled="true"  
      />  
    </settings>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.Net.Configuration.PerformanceCountersElement?displayProperty=nameWithType>
- <xref:System.Net.Configuration.PerformanceCountersElement.Enabled%2A?displayProperty=nameWithType>
- [Schemat ustawień sieciowych](index.md)
- [Liczniki wydajności sieci](../../../debug-trace-profile/performance-counters.md#networking-performance-counters)
