---
title: 'Instrukcje: używanie programu Svcutil.exe do pobierania dokumentów metadanych'
description: Dowiedz się, jak używać Svcutil.exe do pobierania metadanych z uruchomionych usług i zapisywania metadanych w plikach lokalnych.
ms.date: 03/30/2017
ms.assetid: 15524274-3167-4627-b722-d6cedb9fa8c6
ms.openlocfilehash: 449dd3023b5d688ed0de22e3651cccf16bee0c52
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96280679"
---
# <a name="how-to-use-svcutilexe-to-download-metadata-documents"></a>Instrukcje: używanie programu Svcutil.exe do pobierania dokumentów metadanych

Za pomocą Svcutil.exe można pobrać metadane z uruchomionych usług i zapisać metadane w plikach lokalnych. W przypadku schematów adresów URL protokołu HTTP i HTTPS Svcutil.exe próbuje pobrać metadane przy użyciu WS-MetadataExchange i [odnajdywania usług sieci Web XML](/previous-versions/dotnet/netframework-4.0/fxx6cfx2(v=vs.100)). W przypadku wszystkich innych schematów adresów URL Svcutil.exe używa tylko protokołu WS-MetadataExchange.  
  
 Domyślnie Svcutil.exe używa powiązań zdefiniowanych w <xref:System.ServiceModel.Description.MetadataExchangeBindings> klasie. Aby skonfigurować powiązanie używane dla protokołu WS-MetadataExchange, należy zdefiniować punkt końcowy klienta w pliku konfiguracyjnym dla Svcutil.exe (svcutil.exe.config), który używa `IMetadataExchange` kontraktu i ma taką samą nazwę jak schemat Uniform Resource Identifier (URI) adresu punktu końcowego metadanych.  
  
> [!CAUTION]
> Podczas uruchamiania Svcutil.exe, aby uzyskać metadane dla usługi, która ujawnia dwie różne kontrakty usługi, które zawierają operację o tej samej nazwie, Svcutil.exe wyświetla błąd mówiący "nie można uzyskać metadanych z..." Na przykład jeśli masz usługę, która ujawnia kontrakt usługi o nazwie `ICarService` , który ma operację, `Get(Car c)` a ta sama usługa ujawnia kontrakt usługi o nazwie `IBookService` , który ma operację `Get(Book b)` . Aby obejść ten problem, wykonaj jedną z następujących czynności:
>
> - Zmień nazwę jednej z operacji.
> - Ustaw <xref:System.ServiceModel.OperationContractAttribute.Name%2A> inną nazwę.
> - Ustaw jedną z przestrzeni nazw operacji na inną przestrzeń nazw przy użyciu <xref:System.ServiceModel.ServiceContractAttribute.Namespace%2A> właściwości.
  
## <a name="to-download-metadata-using-svcutilexe"></a>Aby pobrać metadane przy użyciu Svcutil.exe  
  
1. Znajdź narzędzie Svcutil.exe w następującej lokalizacji:  
  
     C:\Program Files\Microsoft SDKs\Windows\v1.0.\bin  
  
2. W wierszu polecenia Uruchom narzędzie przy użyciu następującego formatu.  
  
    ```console
    svcutil.exe /t:metadata  <url>* | <epr>  
    ```  
  
     Należy określić `/t:metadata` opcję pobierania metadanych. W przeciwnym razie jest generowany kod i konfiguracja klienta.  
  
3. <`url` argument>określa adres URL punktu końcowego usługi, który udostępnia metadane lub dokument metadanych hostowany w trybie online. <`epr` argument> określa ścieżkę do pliku XML, który zawiera WS-Addressing `EndpointAddress` dla punktu końcowego usługi, który obsługuje protokół WS-MetadataExchange.  
  
 Aby uzyskać więcej opcji dotyczących używania tego narzędzia do pobierania metadanych, zobacz [Narzędzie narzędzia metadanych ServiceModel (Svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md).  
  
## <a name="example"></a>Przykład  

 Następujące polecenie pobiera dokumenty metadanych z uruchomionej usługi.  
  
```console
svcutil /t:metadata http://service/metadataEndpoint  
```  
  
## <a name="see-also"></a>Zobacz też

- [Narzędzie do obsługi metadanych elementu ServiceModel (Svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md)
