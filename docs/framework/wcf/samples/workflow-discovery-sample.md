---
title: Odnajdywanie przepływu pracy — przykład
ms.date: 03/30/2017
ms.assetid: 82cc43f1-3c8f-4771-ac19-a75ac936e2c3
ms.openlocfilehash: 44d1fed74782051a926ced95c49f3e3cb14f2b9e
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96263805"
---
# <a name="workflow-discovery-sample"></a>Odnajdywanie przepływu pracy — przykład

Ten przykład pokazuje, jak umożliwić odnajdywanie usługi przepływu pracy oraz sposób tworzenia niestandardowego działania kodu, które wyszukuje określoną usługę.  
  
## <a name="demonstrates"></a>Demonstracje  

 Odnajdywanie — wyszukiwanie działań i przepływów pracy  
  
## <a name="discussion"></a>Dyskusja  

 W pierwszej części przykładu usługa przepływu pracy jest wykrywalna przy użyciu konfiguracji. Konfiguracji można także użyć do odpowiedniego zastosowania usługi przy użyciu niestandardowych metadanych (takich jak zakresy). Na kliencie przykład używa niestandardowego działania kodu, które używa odnajdywania w celu wyszukania usługi zgodnej z konkretną umową. Działanie Code generuje identyfikator URI, który jest później używany przez działanie wysyłania.  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>Aby skonfigurować, skompilować i uruchomić przykład  
  
1. Ten przykład korzysta z punktów końcowych HTTP, które muszą mieć odpowiednie listy ACL adresów URL do uruchomienia (zobacz [Konfigurowanie protokołu HTTP i https](../feature-details/configuring-http-and-https.md) , aby uzyskać szczegółowe informacje). Wykonanie następującego polecenia w wierszu polecenia z podwyższonym poziomem uprawnień powinno spowodować dodanie odpowiednich list kontroli dostępu. Jeśli powłoka nie rozpoznaje formatu zmiennej, należy zastąpić domenę i nazwę użytkownika dla następujących argumentów.  
  
    `netsh http add urlacl url=http://+:8000/ user=%DOMAIN%\%UserName%`
  
> [!IMPORTANT]
> Przykłady mogą być już zainstalowane na komputerze. Przed kontynuowaniem Wyszukaj następujący katalog (domyślny).  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> Jeśli ten katalog nie istnieje, przejdź do [przykładów Windows Communication Foundation (WCF) i Windows Workflow Foundation (WF) dla .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) , aby pobrać wszystkie Windows Communication Foundation (WCF) i [!INCLUDE[wf1](../../../../includes/wf1-md.md)] przykłady. Ten przykład znajduje się w następującym katalogu.  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Discovery\WorkflowDiscovery`
