---
title: <workflowIdle>
ms.date: 03/30/2017
ms.topic: reference
ms.assetid: b2ef703c-3e01-4213-9d2e-c14c7dba94d2
ms.openlocfilehash: 790e852eb515e19afc324f6e1c25db81ed22999c
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91148675"
---
# \<workflowIdle>

Zachowanie usługi sterująca po zwolnione wystąpienia bezczynności przepływu pracy i utrwalone.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.ServiceModel>**](system-servicemodel-of-workflow.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors-of-workflow.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<serviceBehaviors>**](servicebehaviors-of-workflow.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-servicebehaviors-of-workflow.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<workflowIdle>**  
  
## <a name="syntax"></a>Składnia  
  
```xml  
<behaviors>
  <serviceBehaviors>
    <behavior name="String">
      <workflowIdle timeToPersist="TimeSpan"
                    timeToUnload="TimeSpan" />
    </behavior>
  </serviceBehaviors>
</behaviors>  
```  
  
## <a name="attributes-and-elements"></a>Atrybuty i elementy  

 W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|  
|---------------|-----------------|  
|timeToPersist|Wartość TimeSpan, która określa czas trwania między czasem, gdy przepływ pracy stanie się bezczynny i jest utrwalany. Wartość domyślna to TimeSpan. MaxValue.<br /><br /> Czas trwania rozpoczyna upłynąć, gdy wystąpienie przepływu pracy staje się nieaktywna. Ten atrybut jest przydatny, jeśli chcesz, aby wystąpienie przepływu pracy było bardziej agresywne i nadal utrzymywać wystąpienie w pamięci tak długo, jak to możliwe. Ten atrybut jest prawidłowy tylko wtedy, gdy jego wartość jest mniejsza niż atrybut **TimeToUnload** . Jeśli jest większa, jest ignorowana. Jeśli ten atrybut upłynie przed wartością określoną przez atrybut **TimeToUnload** , trwałość musi zostać zakończona przed odładowaniem przepływu pracy. Oznacza to, że operacja zwolnienia może zostać opóźniona, dopóki przepływ pracy nie zostanie utrwalony. Warstwa trwałości jest odpowiedzialny za obsługę dowolnego powtórzeń przejściowy błędów i tylko na błędy bez nieodwracalny zgłasza wyjątek wyjątków. Dlatego wyjątki zgłaszane w trwałości są traktowane jako krytyczny, a wystąpienie przepływu pracy zostało przerwane.|  
|timeToUnload|Zakres czasu wartość, która określa czas trwania między czas przepływu pracy staje się bezczynności i jest zwalniana. Wartość domyślna to 1 minutę.<br /><br /> Zwalnianie przepływu pracy oznacza, że jest również utrwalone. Jeśli ten atrybut ma wartość zero, wystąpienie przepływu pracy jest utrwalane i zwalniane natychmiast po przejściu przepływu pracy w stan bezczynności. Ustawienie tego atrybutu na TimeSpan. MaxValue skutecznie wyłącza operację Zwolnij. Wystąpienia przepływu pracy bezczynności nigdy nie są usuwane.|  
  
### <a name="child-elements"></a>Elementy podrzędne  

 Brak.  
  
### <a name="parent-elements"></a>Elementy nadrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|[\<behavior> z \<serviceBehaviors>](behavior-of-servicebehaviors-of-workflow.md)|Określa zachowanie elementu.|  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior>
- <xref:System.ServiceModel.Activities.Configuration.WorkflowIdleElement>
