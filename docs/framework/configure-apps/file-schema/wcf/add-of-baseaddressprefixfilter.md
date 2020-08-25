---
title: <add> dla <baseAddressPrefixFilter>
ms.date: 03/30/2017
ms.assetid: b226bede-8459-4de9-b2ac-3d39604ce2bc
ms.openlocfilehash: 2572a6ee6763ae26fe5c56669e10f8c9aef8a280
ms.sourcegitcommit: 9c45035b781caebc63ec8ecf912dc83fb6723b1f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/25/2020
ms.locfileid: "88811798"
---
# <a name="add-of-baseaddressprefixfilter"></a>\<add> dla \<baseAddressPrefixFilter>
Reprezentuje element konfiguracji, który określa filtr przekazywania, który udostępnia mechanizm wybierania odpowiednich powiązań Internet Information Services (IIS) podczas hostowania aplikacji Windows Communication Foundation (WCF) w usługach IIS.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<serviceHostingEnvironment>**](servicehostingenvironment.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<baseAddressPrefixFilters>**](baseaddressprefixfilters.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<add>**  
  
## <a name="syntax"></a>Składnia  
  
```xml  
<serviceHostingEnvironment>
  <baseAddressPrefixFilters>
    <add prefix="String" />
  </baseAddressPrefixFilters>
</serviceHostingEnvironment>
```  
  
## <a name="attributes-and-elements"></a>Atrybuty i elementy  
 W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|  
|---------------|-----------------|  
|prefiks|Identyfikator URI, który jest używany do dopasowania części adresu podstawowego.|  
  
### <a name="child-elements"></a>Elementy podrzędne  
 Brak.  
  
### <a name="parent-elements"></a>Elementy nadrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|[\<baseAddressPrefixFilters>](baseaddressprefixfilters.md)|Kolekcja elementów konfiguracji, które określają filtry przekazywania, które zapewniają mechanizm wybierania odpowiednich powiązań usług IIS podczas hostowania aplikacji Windows Communication Foundation (WCF) w usługach IIS.|  
  
## <a name="remarks"></a>Uwagi  
 Filtr prefiksów umożliwia dostawcom hostingu współużytkowanie Określanie identyfikatorów URI, które mają być używane przez usługę. Umożliwia hostom udostępnionym hostowanie wielu aplikacji z różnymi adresami podstawowymi dla tego samego schematu w tej samej lokacji.  
  
 Witryny sieci Web usług IIS są kontenerami dla aplikacji wirtualnych, które zawierają katalogi wirtualne. Dostęp do aplikacji w lokacji można uzyskać za pomocą jednego lub kilku powiązań usług IIS. Powiązania usług IIS udostępniają dwie informacje: powiązania protokołu i powiązania. Protokół powiązania (na przykład HTTP) definiuje schemat, w którym odbywa się komunikacja, a informacje o powiązaniu (na przykład adres IP, port, nagłówek hosta) zawierają dane używane do uzyskiwania dostępu do witryny.  
  
 Usługi IIS obsługują Określanie wielu powiązań usług IIS dla każdej lokacji, co daje w wyniku wiele adresów bazowych dla każdego schematu. Ponieważ usługa WCF hostowana w lokacji umożliwia powiązanie tylko z jednym adresem podstawowym dla każdego schematu, można użyć funkcji filtru prefiksu, aby wybrać wymagany podstawowy adres usługi hostowanej. Przychodzące adresy podstawowe, dostarczane przez usługi IIS, są filtrowane na podstawie opcjonalnego filtru listy prefiksów.  
  
 Na przykład witryna może zawierać następujące adresy podstawowe:
  
```http
http://testl.fabrikam.com/Service.svc  
http://test2.fabrikam.com/Service.svc  
```  
  
 Możesz użyć poniższego pliku konfiguracji, aby określić filtr prefiksu na poziomie elementu AppDomain.  
  
```xml  
<system.serviceModel>
  <serviceHostingEnvironment>
    <baseAddressPrefixFilters>
      <add prefix="net.tcp://test1.fabrikam.com:8000" />
      <add prefix="http://test2.fabrikam.com:9000" />
    </baseAddressPrefixFilters>
  </serviceHostingEnvironment>
</system.serviceModel>
```  
  
 W tym przykładzie `net.tcp://test1.fabrikam.com:8000` i `http://test2.fabrikam.com:9000` są jedynymi adresami podstawowymi dla odpowiednich schematów, które mogą być przesyłane przez program.  
  
 Domyślnie, gdy prefiks nie jest określony, wszystkie adresy są przesyłane przez. Określenie prefiksu zezwala tylko na przekazanie zgodnego adresu podstawowego dla tego schematu.  
  
> [!NOTE]
> Filtr nie obsługuje żadnych symboli wieloznacznych. Ponadto baseAddresses dostarczone przez usługi IIS mogą mieć adresy powiązane z innymi schematami nieobecnymi na `baseAddressPrefixFilters` liście. Te adresy nie są odfiltrowane.  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.ServiceModel.Configuration.BaseAddressPrefixFilterElement>
- <xref:System.ServiceModel.Configuration.ServiceHostingEnvironmentSection>
- <xref:System.ServiceModel.ServiceHostingEnvironment>
- [Hosting](../../../wcf/feature-details/hosting.md)
