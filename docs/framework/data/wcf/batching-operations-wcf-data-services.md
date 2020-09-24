---
title: Operacje wsadowe (Usługi danych programu WCF)
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, client library
ms.assetid: 962a49d1-cc11-4b96-bc7d-071dd6607d6c
ms.openlocfilehash: 95524c1397172e645d682a6ef3f03b17bb3a639d
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91166069"
---
# <a name="batching-operations-wcf-data-services"></a>Operacje wsadowe (Usługi danych programu WCF)

Protokół Open Data Protocol (OData) obsługuje przetwarzanie wsadowe żądań do usługi opartej na protokole OData. Aby uzyskać więcej informacji, zobacz Usługa [OData: przetwarzanie wsadowe](https://www.odata.org/documentation/odata-version-2-0/batch-processing/). W Usługi danych programu WCF każda operacja korzystająca z <xref:System.Data.Services.Client.DataServiceContext> , taka jak wykonywanie zapytania lub zapisanie zmian, powoduje wysłanie osobnego żądania do usługi danych. Aby zachować zakres logiczny dla zestawów operacji, można jawnie zdefiniować partie operacyjne. Dzięki temu wszystkie operacje w partii są wysyłane do usługi danych w ramach pojedynczego żądania HTTP, dzięki czemu serwer może przetwarzać operacje w sposób niepodzielny i zmniejsza liczbę rund do usługi danych.  
  
## <a name="batching-query-operations"></a>Wsadowe operacje zapytań  

 Aby wykonać wiele zapytań w pojedynczej partii, należy utworzyć każde zapytanie w partii jako oddzielne wystąpienie <xref:System.Data.Services.Client.DataServiceRequest%601> klasy. Po utworzeniu żądania zapytania w ten sposób, samo zapytanie jest zdefiniowane jako identyfikator URI i następuje po zasadach adresowania zasobów. Aby uzyskać więcej informacji, zobacz [Uzyskiwanie dostępu do zasobów usługi danych](accessing-data-service-resources-wcf-data-services.md). Żądania zapytań wsadowych są wysyłane do usługi danych, gdy <xref:System.Data.Services.Client.DataServiceContext.ExecuteBatch%2A> wywoływana jest metoda, która zawiera obiekty żądania zapytania. Ta metoda zwraca <xref:System.Data.Services.Client.DataServiceResponse> obiekt, który jest kolekcją obiektów, <xref:System.Data.Services.Client.QueryOperationResponse%601> które reprezentują odpowiedzi na poszczególne zapytania w partii, z których każdy zawiera kolekcję obiektów zwracanych przez zapytanie lub informacje o błędzie. Gdy każda operacja pojedynczego zapytania w partii nie powiedzie się, informacje o błędzie są zwracane w <xref:System.Data.Services.Client.QueryOperationResponse%601> obiekcie dla operacji, która się nie powiodła, a pozostałe operacje są nadal wykonywane. Aby uzyskać więcej informacji, zobacz [jak: wykonywanie zapytań w partii](how-to-execute-queries-in-a-batch-wcf-data-services.md).  
  
 Zapytania wsadowe mogą być również wykonywane asynchronicznie. Aby uzyskać więcej informacji, zobacz [operacje asynchroniczne](asynchronous-operations-wcf-data-services.md).  
  
## <a name="batching-the-savechanges-operation"></a>Przetwarzanie wsadowe operacji metody SaveChanges  

 Po wywołaniu <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> metody wszystkie zmiany, które są śledzone w kontekście, są tłumaczone na operacje oparte na protokole REST, które są wysyłane jako żądania do usługi OData. Domyślnie te zmiany nie są wysyłane w pojedynczym komunikacie żądania. Aby wymagać, aby wszystkie zmiany były wysyłane w pojedynczym żądaniu, należy wywołać <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%28System.Data.Services.Client.SaveChangesOptions%29> metodę i uwzględnić wartość <xref:System.Data.Services.Client.SaveChangesOptions.Batch> w <xref:System.Data.Services.Client.SaveChangesOptions> wyliczeniu dostarczanym do metody.  
  
 Można również asynchronicznie zapisywać zmiany wsadowe. Aby uzyskać więcej informacji, zobacz [operacje asynchroniczne](asynchronous-operations-wcf-data-services.md).  
  
## <a name="see-also"></a>Zobacz też

- [Biblioteka klienta usług danych WCF](wcf-data-services-client-library.md)
