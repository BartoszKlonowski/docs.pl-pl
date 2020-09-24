---
title: <legacyCorruptedStateExceptionsPolicy> Element
ms.date: 03/30/2017
helpviewer_keywords:
- <legacyCorruptedStateExceptionsPolicy> element
- legacyCorruptedStateExceptionsPolicy element
ms.assetid: e0a55ddc-bfa8-4f3e-ac14-d1fc3330e4bb
ms.openlocfilehash: f36e27a1b85cff2ba8c7e838bace37890a5aa760
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91151210"
---
# <a name="legacycorruptedstateexceptionspolicy-element"></a>\<legacyCorruptedStateExceptionsPolicy> Element

Określa, czy środowisko uruchomieniowe języka wspólnego umożliwia kodowi zarządzanemu przechwytywanie naruszeń dostępu i innych wyjątków uszkodzonych Stanów.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<runtime>**](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<legacyCorruptedStateExceptionsPolicy>**  
  
## <a name="syntax"></a>Składnia  
  
```xml  
<legacyCorruptedStateExceptionsPolicy enabled="true|false"/>  
```  
  
## <a name="attributes-and-elements"></a>Atrybuty i elementy  

 W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|  
|---------------|-----------------|  
|`enabled`|Atrybut wymagany.<br /><br /> Określa, że aplikacja będzie przechwytywać błędy wyjątku stanu, takie jak naruszenia zasad dostępu.|  
  
## <a name="enabled-attribute"></a>Atrybut włączony  
  
|Wartość|Opis|  
|-----------|-----------------|  
|`false`|Aplikacja nie będzie przechwytywać uszkodzonych błędów wyjątku stanu, takich jak naruszenia zasad dostępu. Jest to opcja domyślna.|  
|`true`|Aplikacja będzie przechwycić błędy wyjątku stanu, takie jak naruszenia zasad dostępu.|  
  
### <a name="child-elements"></a>Elementy podrzędne  

 Brak.  
  
### <a name="parent-elements"></a>Elementy nadrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|`configuration`|Element główny w każdym pliku konfiguracji używanym przez środowisko uruchomieniowe języka wspólnego i aplikacje programu .NET Framework.|  
|`runtime`|Zawiera informacje dotyczące powiązania zestawu oraz wyrzucania elementów bezużytecznych.|  
  
## <a name="remarks"></a>Uwagi  

 W .NET Framework w wersji 3,5 i starszych środowisko uruchomieniowe języka wspólnego może przechwytywać wyjątki, które zostały zgłoszone przez uszkodzone Stany procesów. Naruszenie zasad dostępu jest przykładem tego typu wyjątku.  
  
 Począwszy od .NET Framework 4, kod zarządzany nie przechwytuje już tych typów wyjątków w `catch` blokach. Można jednak zastąpić tę zmianę i zachować obsługę wyjątków uszkodzonych Stanów na dwa sposoby:  
  
- Ustaw `<legacyCorruptedStateExceptionsPolicy>` `enabled` atrybut elementu na `true` . To ustawienie konfiguracji jest stosowane processwide i ma wpływ na wszystkie metody.  
  
 -lub-  
  
- Zastosuj <xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute?displayProperty=nameWithType> atrybut do metody, która zawiera `catch` blok wyjątków.  
  
 Ten element konfiguracji jest dostępny tylko w .NET Framework 4 i nowszych.  
  
## <a name="example"></a>Przykład  

 Poniższy przykład pokazuje, jak określić, że aplikacja ma zostać przywrócona do zachowania przed .NET Framework 4 i przechwycić wszystkie błędy wyjątków spowodowanych uszkodzeniem stanu.  
  
```xml  
<configuration>  
   <runtime>  
      <legacyCorruptedStateExceptionsPolicy enabled="true" />  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute>
- [Schemat ustawień środowiska uruchomieniowego](index.md)
- [Schemat pliku konfiguracji](../index.md)
