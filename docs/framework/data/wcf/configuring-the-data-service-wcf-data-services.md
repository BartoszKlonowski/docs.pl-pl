---
title: Konfigurowanie usługi danych (Usługi danych programu WCF)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, configuring
ms.assetid: 59efd4c8-cc7a-4800-a0a4-d3f8abe6c55c
ms.openlocfilehash: a30a8c2c731e8c5cb2b22c8d7f34ec32d149803c
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91152796"
---
# <a name="configuring-the-data-service-wcf-data-services"></a>Konfigurowanie usługi danych (Usługi danych programu WCF)

Za pomocą Usługi danych programu WCF można tworzyć usługi danych, które uwidaczniają źródła danych Open Data Protocol (OData). Dane w tych źródłach mogą pochodzić z różnych źródeł danych. Usługi danych programu WCF używa dostawców danych w celu udostępnienia tych danych jako źródła strumieniowego OData. Ci dostawcy obejmują dostawcę Entity Framework, dostawcę odbicia i zestaw niestandardowych interfejsów dostawcy usługi danych. Implementacja dostawcy definiuje model danych dla usługi. Aby uzyskać więcej informacji, zobacz [Data Services Providers](data-services-providers-wcf-data-services.md).  
  
 W Usługi danych programu WCF usługa danych jest klasą, która dziedziczy z <xref:System.Data.Services.DataService%601> klasy, gdzie typ usługi danych jest kontenerem jednostek modelu danych. Ten kontener jednostek ma co najmniej jedną właściwość, która zwraca obiekt <xref:System.Linq.IQueryable%601> , który jest używany do uzyskiwania dostępu do zestawów jednostek w modelu danych.  
  
 Zachowania usługi danych są definiowane przez elementy członkowskie <xref:System.Data.Services.DataServiceConfiguration> klasy i przez elementy członkowskie <xref:System.Data.Services.DataServiceBehavior> klasy, do których uzyskuje się dostęp z <xref:System.Data.Services.DataServiceConfiguration.DataServiceBehavior%2A> właściwości <xref:System.Data.Services.DataServiceConfiguration> klasy. <xref:System.Data.Services.DataServiceConfiguration>Klasa jest dostarczana do `InitializeService` metody, która jest implementowana przez usługę danych, jak w następującej implementacji usługi danych Northwind:  
  
[!code-csharp[Astoria Northwind Service#DataServiceConfigComplete](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_service/cs/northwind.svc.cs#dataserviceconfigcomplete)]  
[!code-vb[Astoria Northwind Service#DataServiceConfigComplete](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_service/vb/northwind.svc.vb#dataserviceconfigcomplete)]  
  
## <a name="data-service-configuration-settings"></a>Ustawienia konfiguracji usługi danych  

 <xref:System.Data.Services.DataServiceConfiguration>Klasa umożliwia określenie następujących zachowań usługi danych:  
  
|Członek|Zachowanie|  
|------------|--------------|  
|<xref:System.Data.Services.DataServiceBehavior.AcceptCountRequests%2A>|Umożliwia wyłączenie żądań zliczania przesyłanych do usługi danych przy użyciu `$count` segmentu ścieżki i `$inlinecount` opcji zapytania. Aby uzyskać więcej informacji, zobacz [konwencje protokołu OData: URI](https://www.odata.org/documentation/odata-version-2-0/uri-conventions/).|  
|<xref:System.Data.Services.DataServiceBehavior.AcceptProjectionRequests%2A>|Umożliwia wyłączenie obsługi projekcji danych w żądaniach przesyłanych do usługi danych za pomocą `$select` opcji zapytania. Aby uzyskać więcej informacji, zobacz [konwencje protokołu OData: URI](https://www.odata.org/documentation/odata-version-2-0/uri-conventions/).|  
|<xref:System.Data.Services.DataServiceConfiguration.EnableTypeAccess%2A>|Umożliwia uwidocznienie typu danych w metadanych dla dostawcy dynamicznego metadanych zdefiniowanego za pomocą <xref:System.Data.Services.Providers.IDataServiceMetadataProvider> interfejsu.|  
|<xref:System.Data.Services.DataServiceConfiguration.EnableTypeConversion%2A>|Pozwala określić, czy środowisko uruchomieniowe usługi danych ma skonwertować typ, który jest zawarty w ładunku do rzeczywistego typu właściwości określonego w żądaniu.|  
|<xref:System.Data.Services.DataServiceBehavior.InvokeInterceptorsOnLinkDelete%2A>|Pozwala określić, czy zarejestrowane Interceptory zmian mają być wywoływane na powiązanych jednostkach, gdy zostanie usunięty link relacji między dwiema jednostkami.|  
|<xref:System.Data.Services.DataServiceConfiguration.MaxBatchCount%2A>|Umożliwia ograniczenie liczby zestawów zmian i operacji zapytań, które są dozwolone w pojedynczej partii. Aby uzyskać więcej informacji, zobacz operacje wsadowe [OData: Batch](https://www.odata.org/documentation/odata-version-2-0/batch-processing/) i [Batch](batching-operations-wcf-data-services.md).|  
|<xref:System.Data.Services.DataServiceConfiguration.MaxChangesetCount%2A>|Pozwala ograniczyć liczbę zmian, które mogą zostać uwzględnione w pojedynczym zestawie zmian. Aby uzyskać więcej informacji, zobacz [How to: Enable stronicowanie wyników usługi danych](how-to-enable-paging-of-data-service-results-wcf-data-services.md).|  
|<xref:System.Data.Services.DataServiceConfiguration.MaxExpandCount%2A>|Umożliwia ograniczenie rozmiaru odpowiedzi poprzez ograniczenie liczby powiązanych jednostek, które mogą zostać uwzględnione w pojedynczym żądaniu przy użyciu `$expand` operatora zapytania. Aby uzyskać więcej informacji, zobacz [konwencje protokołu OData: URI](https://www.odata.org/documentation/odata-version-2-0/uri-conventions/) i [ładowanie odroczonej zawartości](loading-deferred-content-wcf-data-services.md).|  
|<xref:System.Data.Services.DataServiceConfiguration.MaxExpandDepth%2A>|Umożliwia ograniczenie rozmiaru odpowiedzi przez ograniczenie głębokości grafu powiązanych jednostek, które mogą zostać uwzględnione w pojedynczym żądaniu przy użyciu `$expand` operatora zapytania. Aby uzyskać więcej informacji, zobacz [konwencje protokołu OData: URI](https://www.odata.org/documentation/odata-version-2-0/uri-conventions/) i [ładowanie odroczonej zawartości](loading-deferred-content-wcf-data-services.md).|  
|<xref:System.Data.Services.DataServiceConfiguration.MaxObjectCountOnInsert%2A>|Umożliwia ograniczenie liczby jednostek do wstawienia, które mogą być zawarte w pojedynczym żądaniu POST.|  
|<xref:System.Data.Services.DataServiceBehavior.MaxProtocolVersion%2A>|Definiuje wersję protokołu Atom, który jest używany przez usługę danych. Gdy wartość jest równa <xref:System.Data.Services.DataServiceBehavior.MaxProtocolVersion%2A> wartości mniejszej niż wartość maksymalna <xref:System.Data.Services.Common.DataServiceProtocolVersion> , najnowsza funkcjonalność usługi danych programu WCF nie jest dostępna dla klientów uzyskujących dostęp do usługi danych. Aby uzyskać więcej informacji, zobacz [przechowywanie wersji usługi danych](data-service-versioning-wcf-data-services.md).|  
|<xref:System.Data.Services.DataServiceConfiguration.MaxResultsPerCollection%2A>|Umożliwia ograniczenie rozmiaru odpowiedzi poprzez ograniczenie liczby jednostek w poszczególnych zestawach jednostek, które są zwracane jako strumieniowe źródło danych.|  
|<xref:System.Data.Services.DataServiceConfiguration.RegisterKnownType%2A>|Dodaje typ danych do listy typów, które są rozpoznawane przez usługę danych.|  
|<xref:System.Data.Services.DataServiceConfiguration.SetEntitySetAccessRule%2A>|Ustawia prawa dostępu dla zasobów zestawu jednostek, które są dostępne w usłudze danych. Wartość gwiazdki ( `*` ) może zostać podana dla parametru name, aby ustawić dostęp dla wszystkich pozostałych zestawów jednostek do tego samego poziomu. Zalecamy skonfigurowanie dostępu do zestawów jednostek, aby zapewnić im najmniejszy dostęp do zasobów usługi danych, które są wymagane przez aplikacje klienckie. Aby uzyskać więcej informacji, zobacz [zabezpieczanie usługi danych programu WCF](securing-wcf-data-services.md). Przykłady minimalnych praw dostępu wymaganych dla danego identyfikatora URI i akcji HTTP można znaleźć w tabeli w sekcji [minimalne wymagania dotyczące dostępu do zasobów](configuring-the-data-service-wcf-data-services.md#accessRequirements) .|  
|<xref:System.Data.Services.DataServiceConfiguration.SetEntitySetPageSize%2A>|Ustawia maksymalny rozmiar strony dla zasobu zestawu jednostek. Aby uzyskać więcej informacji, zobacz [How to: Enable stronicowanie wyników usługi danych](how-to-enable-paging-of-data-service-results-wcf-data-services.md).|  
|<xref:System.Data.Services.DataServiceConfiguration.SetServiceOperationAccessRule%2A>|Ustawia prawa dostępu do operacji usługi, które są zdefiniowane w usłudze danych. Aby uzyskać więcej informacji, zobacz [operacje usługi](service-operations-wcf-data-services.md). Wartość gwiazdki ( `*` ) może zostać podana dla parametru name, aby ustawić dostęp dla wszystkich operacji usługi na tym samym poziomie. Zalecamy skonfigurowanie dostępu do operacji usługi, aby zapewnić im najmniejszy dostęp do zasobów usługi danych, które są wymagane przez aplikacje klienckie. Aby uzyskać więcej informacji, zobacz [zabezpieczanie usługi danych programu WCF](securing-wcf-data-services.md).|  
|<xref:System.Data.Services.DataServiceConfiguration.UseVerboseErrors%2A>|Ta właściwość konfiguracji umożliwia łatwiejsze rozwiązywanie problemów z usługą danych przez zwrócenie większej ilości informacji w komunikacie o błędzie. Ta opcja nie jest przeznaczona do użycia w środowisku produkcyjnym. Aby uzyskać więcej informacji, zobacz [Tworzenie i wdrażanie usługi danych programu WCF](developing-and-deploying-wcf-data-services.md).|  
  
<a name="accessRequirements"></a>

## <a name="minimum-resource-access-requirements"></a>Minimalne wymagania dotyczące dostępu do zasobów  

 Poniższa tabela zawiera szczegółowe informacje o prawach do zestawu jednostek minimalnych, które muszą zostać przyznane do wykonania określonej operacji. Przykłady ścieżki są oparte na usłudze danych Northwind, która została utworzona po zakończeniu [przewodnika Szybki Start](quickstart-wcf-data-services.md). Ponieważ zarówno <xref:System.Data.Services.EntitySetRights> Wyliczenie, jak i <xref:System.Data.Services.ServiceOperationRights> Wyliczenie są zdefiniowane przy użyciu <xref:System.FlagsAttribute> , można użyć operatora logicznego OR do określenia wielu uprawnień dla pojedynczego zestawu lub operacji. Aby uzyskać więcej informacji, zobacz [jak: Włączanie dostępu do usługi danych](how-to-enable-access-to-the-data-service-wcf-data-services.md).  
  
|Ścieżka/akcja|`GET`|`DELETE`|`MERGE`|`POST`|`PUT`|  
|------------------|-----------|--------------|-------------|------------|-----------|  
|`/Customers`|<xref:System.Data.Services.EntitySetRights.ReadMultiple>|Nieobsługiwane|Nieobsługiwane|<xref:System.Data.Services.EntitySetRights.WriteAppend>|Nieobsługiwane|  
|`/Customers('ALFKI')`|<xref:System.Data.Services.EntitySetRights.ReadSingle>|<xref:System.Data.Services.EntitySetRights.ReadSingle> i <xref:System.Data.Services.EntitySetRights.WriteDelete>|<xref:System.Data.Services.EntitySetRights.ReadSingle> i <xref:System.Data.Services.EntitySetRights.WriteMerge>|nie dotyczy|<xref:System.Data.Services.EntitySetRights.ReadSingle> i <xref:System.Data.Services.EntitySetRights.WriteReplace>|  
|`/Customers('ALFKI')/Orders`|`Customers`: <xref:System.Data.Services.EntitySetRights.ReadSingle><br /><br /> lub<br /><br /> `Orders`: <xref:System.Data.Services.EntitySetRights.ReadMultiple>|Nieobsługiwane|Nieobsługiwane|`Customers`: <xref:System.Data.Services.EntitySetRights.ReadSingle> i <xref:System.Data.Services.EntitySetRights.WriteMerge> lub <xref:System.Data.Services.EntitySetRights.WriteReplace><br /><br /> lub<br /><br /> `Orders``:`i<xref:System.Data.Services.EntitySetRights.WriteAppend>|Nieobsługiwane|  
|`/Customers('ALFKI')/Orders(10643)`|`Customers`: <xref:System.Data.Services.EntitySetRights.ReadSingle><br /><br /> lub<br /><br /> `Orders`: <xref:System.Data.Services.EntitySetRights.ReadSingle>|`Customers`: <xref:System.Data.Services.EntitySetRights.ReadSingle><br /><br /> lub<br /><br /> `Orders`: <xref:System.Data.Services.EntitySetRights.ReadSingle> i <xref:System.Data.Services.EntitySetRights.WriteDelete>|`Customers`: <xref:System.Data.Services.EntitySetRights.ReadSingle><br /><br /> lub<br /><br /> `Orders`: <xref:System.Data.Services.EntitySetRights.ReadSingle> i <xref:System.Data.Services.EntitySetRights.WriteMerge>|Nieobsługiwane|`Customers`: <xref:System.Data.Services.EntitySetRights.ReadSingle><br /><br /> lub<br /><br /> `Orders`: <xref:System.Data.Services.EntitySetRights.ReadSingle> i <xref:System.Data.Services.EntitySetRights.WriteReplace>|  
|`/Orders(10643)/Customer`|`Customers`: <xref:System.Data.Services.EntitySetRights.ReadSingle><br /><br /> lub<br /><br /> `Orders`: <xref:System.Data.Services.EntitySetRights.ReadSingle>|`Customers`: <xref:System.Data.Services.EntitySetRights.ReadSingle> i <xref:System.Data.Services.EntitySetRights.WriteDelete><br /><br /> lub<br /><br /> `Orders`: <xref:System.Data.Services.EntitySetRights.ReadSingle>|`Customers`: <xref:System.Data.Services.EntitySetRights.ReadSingle> i <xref:System.Data.Services.EntitySetRights.WriteMerge> ;<br /><br /> lub<br /><br /> `Orders`: <xref:System.Data.Services.EntitySetRights.ReadSingle>|`Customers`: <xref:System.Data.Services.EntitySetRights.WriteAppend><br /><br /> lub<br /><br /> `Orders`: <xref:System.Data.Services.EntitySetRights.WriteAppend> i <xref:System.Data.Services.EntitySetRights.ReadSingle>|Nieobsługiwane|  
|`/Customers('ALFKI')/$links/Orders`|`Customers`: <xref:System.Data.Services.EntitySetRights.ReadSingle><br /><br /> lub<br /><br /> `Orders`: <xref:System.Data.Services.EntitySetRights.ReadMultiple>|Nieobsługiwane|Nieobsługiwane|`Customers`: <xref:System.Data.Services.EntitySetRights.ReadSingle> i <xref:System.Data.Services.EntitySetRights.WriteMerge> lub <xref:System.Data.Services.EntitySetRights.WriteReplace><br /><br /> lub<br /><br /> `Orders`: <xref:System.Data.Services.EntitySetRights.ReadSingle>|Nieobsługiwane|  
|`/Customers('ALFKI')/$links/Orders(10643)`|`Customers`: <xref:System.Data.Services.EntitySetRights.ReadSingle><br /><br /> lub<br /><br /> `Orders`: <xref:System.Data.Services.EntitySetRights.ReadSingle>|`Customers`: <xref:System.Data.Services.EntitySetRights.ReadSingle> i <xref:System.Data.Services.EntitySetRights.WriteMerge> lub <xref:System.Data.Services.EntitySetRights.WriteReplace><br /><br /> lub<br /><br /> `Orders`: <xref:System.Data.Services.EntitySetRights.ReadSingle>|Nieobsługiwane|Nieobsługiwane|Nieobsługiwane|  
|`/Orders(10643)/$links/Customer`|`Customers`: <xref:System.Data.Services.EntitySetRights.ReadSingle><br /><br /> lub<br /><br /> `Orders`: <xref:System.Data.Services.EntitySetRights.ReadSingle>|`Orders`: <xref:System.Data.Services.EntitySetRights.ReadSingle> i <xref:System.Data.Services.EntitySetRights.WriteMerge> lub <xref:System.Data.Services.EntitySetRights.WriteReplace>|`Customers`: <xref:System.Data.Services.EntitySetRights.ReadSingle><br /><br /> lub<br /><br /> `Orders`: <xref:System.Data.Services.EntitySetRights.ReadSingle> i <xref:System.Data.Services.EntitySetRights.WriteMerge>|Nieobsługiwane|`Customers`: <xref:System.Data.Services.EntitySetRights.ReadSingle>;<br /><br /> lub<br /><br /> `Orders`: <xref:System.Data.Services.EntitySetRights.ReadSingle> i <xref:System.Data.Services.EntitySetRights.WriteReplace>|  
|`/Customers/$count`|<xref:System.Data.Services.EntitySetRights.ReadMultiple>|Nieobsługiwane|Nieobsługiwane|Nieobsługiwane|Nieobsługiwane|  
|`/Customers('ALFKI')/ContactName`|<xref:System.Data.Services.EntitySetRights.ReadSingle>|Nieobsługiwane|<xref:System.Data.Services.EntitySetRights.WriteMerge>|Nieobsługiwane|<xref:System.Data.Services.EntitySetRights.WriteReplace>|  
|`/Customers('ALFKI')/Address/StreetAddress/$value`<sup>1</sup>|<xref:System.Data.Services.EntitySetRights.ReadSingle>|<xref:System.Data.Services.EntitySetRights.WriteDelete>|Nieobsługiwane|Nieobsługiwane|Nieobsługiwane|  
|`/Customers('ALFKI')/ContactName/$value`|<xref:System.Data.Services.EntitySetRights.ReadSingle>|<xref:System.Data.Services.EntitySetRights.ReadSingle> i <xref:System.Data.Services.EntitySetRights.WriteDelete>|<xref:System.Data.Services.EntitySetRights.WriteMerge>|Nieobsługiwane|<xref:System.Data.Services.EntitySetRights.WriteReplace>|  
|`/Customers('ALFKI')/$value`<sup>2</sup>|<xref:System.Data.Services.EntitySetRights.ReadSingle>|Nieobsługiwane|Nieobsługiwane|Nieobsługiwane|<xref:System.Data.Services.EntitySetRights.WriteReplace>|  
|`/Customers?$select=Orders/*&$expand=Orders`|`Customers`: <xref:System.Data.Services.EntitySetRights.ReadSingle><br /><br /> lub<br /><br /> `Orders`: <xref:System.Data.Services.EntitySetRights.ReadMultiple>|Nieobsługiwane|Nieobsługiwane|`Customers`: <xref:System.Data.Services.EntitySetRights.WriteAppend>|Nieobsługiwane|  
|`/Customers('ALFKI')?$select=Orders/*&$expand=Orders`|`Customers`: <xref:System.Data.Services.EntitySetRights.ReadSingle><br /><br /> lub<br /><br /> `Orders`: <xref:System.Data.Services.EntitySetRights.ReadMultiple>|Nieobsługiwane|Nieobsługiwane|Nieobsługiwane|Nieobsługiwane|  
  
 <sup>1</sup> w tym przykładzie `Address` reprezentuje właściwość typu złożonego `Customers` jednostki, która ma właściwość o nazwie `StreetAddress` . Model używany przez usługi danych Northwind nie definiuje jawnie tego typu złożonego. Gdy model danych jest definiowany przy użyciu dostawcy Entity Framework, można użyć narzędzi Entity Data Model do zdefiniowania takiego typu złożonego. Aby uzyskać więcej informacji, zobacz [jak: Tworzenie i modyfikowanie typów złożonych](/previous-versions/dotnet/netframework-4.0/dd456820(v=vs.100)).  
  
 <sup>2</sup> ten identyfikator URI jest obsługiwany, gdy właściwość zwracająca duży obiekt binarny (BLOB) jest definiowana jako zasób multimedialny należący do jednostki, która jest pozycją linku do nośnika, w tym przypadku jest to `Customers` . Aby uzyskać więcej informacji, zobacz [dostawca przesyłania strumieniowego](streaming-provider-wcf-data-services.md).  
  
<a name="versioning"></a>

## <a name="versioning-requirements"></a>Wymagania dotyczące wersji  

 Następujące zachowania konfiguracji usługi danych wymagają wersji 2 protokołu OData lub nowszej wersji:  
  
- Obsługa żądań Count.  
  
- Obsługa opcji zapytania $select dla projekcji.  
  
 Aby uzyskać więcej informacji, zobacz [przechowywanie wersji usługi danych](data-service-versioning-wcf-data-services.md).  
  
## <a name="see-also"></a>Zobacz też

- [Definiowanie usług danych WCF](defining-wcf-data-services.md)
- [Hosting usługi danych](hosting-the-data-service-wcf-data-services.md)
