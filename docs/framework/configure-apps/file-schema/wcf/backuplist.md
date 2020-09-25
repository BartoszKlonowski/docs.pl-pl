---
title: <backupList>
ms.date: 03/30/2017
ms.assetid: a3d9d1f9-4a53-45e9-a880-86c8bee0b833
ms.openlocfilehash: 8f4dcf8f7d71cfa2ed9944822d7cce974e7f1979
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91201567"
---
# \<backupList>

Reprezentuje sekcję konfiguracji służącą do definiowania listy kopii zapasowych, która wylicza zestaw punktów końcowych, które mają być używane przez usługę routingu w przypadku, gdy podstawowy punkt końcowy nie zostanie osiągnięty. Jeśli pierwszy punkt końcowy na liście nie działa, usługa routingu automatycznie przejdzie w tryb failover do kolejnej listy.  Dzięki temu można szybko dodać niezawodność do aplikacji bez konieczności uczenia się aplikacji klienckiej, jak obsługiwać złożone wzorce lub wszystkie usługi są wdrażane.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<routing>**](routing.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<backupLists>**](backuplists.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<backupList>**  
  
## <a name="syntax"></a>Składnia  
  
```xml  
<routing>
  <backupLists>
    <backupList name="String">
      <add endpointName="String" />
    </backupList>
  </backupLists>
</routing>
```  
  
## <a name="attributes-and-elements"></a>Atrybuty i elementy  

 W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|  
|---------------|-----------------|  
|name|Ciąg określający nazwę używaną do identyfikowania tej listy punktów końcowych.|  
  
### <a name="child-elements"></a>Elementy podrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|[\<filter>](filter.md)||  
  
### <a name="parent-elements"></a>Elementy nadrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|[\<routing>](routing.md)|Lista punktów końcowych kopii zapasowych.|  
  
## <a name="remarks"></a>Uwagi  

 Ta sekcja zawiera uporządkowaną kolekcję punktów końcowych, do której zostanie wysłany komunikat w przypadku wyjątku komunikacji podczas wysyłania do podstawowego punktu końcowego.  
  
 Jeśli wysyłanie do podstawowego punktu końcowego wymienione w `endpointName` atrybucie [\<add>](add-of-entries.md) nie powiedzie się z wyjątkiem komunikacji, usługa routingu podejmie próbę wysłania komunikatu do pierwszego punktu końcowego w tej sekcji konfiguracji. Jeśli to również się nie powiedzie z wyjątkiem komunikacji, usługa routingu podejmie próbę wysłania komunikatu do następnego komunikatu zawartego w tej sekcji do momentu pomyślnej próby wysłania, zwracając błąd inny niż wyjątek komunikacji lub wszystkie punkty końcowe w kolekcji zwróciły błąd.  
  
 W poniższym przykładzie, jeśli Wyślij do podstawowego punktu końcowego o nazwie "Destination" zwróci wyjątek komunikacji, usługa podejmie próbę wysłania komunikatu do "alternateServiceQueue". Jeśli ta próba zwróci również wyjątek komunikacji, usługa routingu podejmie próbę wysłania komunikatu do następnego punktu końcowego w kolekcji.  
  
```xml  
<filterTables>
  <filterTable name="filterTable1">
    <add filterName="MatchAllFilter1"
         endpointName="Destination"
         backupList="backupEndpointList" />
  </filterTable>
</filterTables>
<backupLists>
  <backupList name="backupEndpointList">
    <add endpointName="backupServiceQueue" />
    <add endpointName="alternateServiceQueue" />
  </backupList>
</backupLists>
```  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.ServiceModel.Routing.Configuration.BackupEndpointCollection?displayProperty=nameWithType>
