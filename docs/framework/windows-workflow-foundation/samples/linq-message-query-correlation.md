---
title: Korelacja zapytania komunikatów LINQ
ms.date: 03/30/2017
ms.assetid: b746872e-57b1-4514-b337-53398a0e0deb
ms.openlocfilehash: 83ffc80bd1944681da29e9058de454636aa7405b
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96291105"
---
# <a name="linq-message-query-correlation"></a>Korelacja zapytania komunikatów LINQ

Ten przykład pokazuje, jak przeprowadzić korelację opartą na zawartości przy użyciu niestandardowej <xref:System.ServiceModel.Dispatcher.MessageQuery> implementacji, w przeciwieństwie do dostarczonych przez system <xref:System.ServiceModel.XPathMessageQuery> .  
  
## <a name="demonstrates"></a>Demonstracje  

 Niestandardowa <xref:System.ServiceModel.Dispatcher.MessageQuery> korelacja oparta na zawartości.  
  
## <a name="discussion"></a>Dyskusja  

 Ten przykład pokazuje, jak rozłożyć z <xref:System.ServiceModel.Dispatcher.MessageQuery> klasy podstawowej na potrzeby korelacji. Implementacja niestandardowa, `LinqMessageQuery` umożliwia użytkownikom udostępnianie XName w wiadomości przy użyciu XLinq. Dane pobierane przez zapytanie są używane do tworzenia klucza korelacji do wysyłania komunikatów do odpowiedniego wystąpienia przepływu pracy.  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>Aby skonfigurować, skompilować i uruchomić przykład  
  
1. Ten przykład uwidacznia usługę przepływu pracy za pomocą punktów końcowych HTTP. Aby uruchomić ten przykład, należy dodać odpowiednie listy ACL adresów URL (zobacz [Konfigurowanie protokołu HTTP i https](../../wcf/feature-details/configuring-http-and-https.md) w celu uzyskania szczegółowych informacji), uruchamiając program Visual Studio jako administrator lub wykonując następujące polecenie w wierszu polecenia z podwyższonym poziomem uprawnień, aby dodać odpowiednie listy ACL. Upewnij się, że Twoja domena i nazwa użytkownika zostały zastąpione.  
  
    ```console  
    netsh http add urlacl url=http://+:8000/ user=%DOMAIN%\%UserName%  
    ```  
  
2. Po dodaniu list ACL adresów URL wykonaj następujące czynności.  
  
    1. Skompiluj rozwiązanie.  
  
    2. Aby ustawić wiele projektów uruchomieniowych, kliknij prawym przyciskiem myszy rozwiązanie i wybierz polecenie **Ustaw projekty startowe**. Dodaj **usługę** i **klienta** (w tej kolejności) jako wiele projektów początkowych.  
  
    3. Uruchom aplikację. W konsoli klienta programu jest wyświetlany przepływ pracy, który wysyła zamówienie i pobiera identyfikator zamówienia zakupu, a następnie potwierdza zamówienie. W oknie usługi zostaną wyświetlone żądania przetwarzane.  
  
> [!IMPORTANT]
> Przykłady mogą być już zainstalowane na komputerze. Przed kontynuowaniem Wyszukaj następujący katalog (domyślny).  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> Jeśli ten katalog nie istnieje, przejdź do [przykładów Windows Communication Foundation (WCF) i Windows Workflow Foundation (WF) dla .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) , aby pobrać wszystkie Windows Communication Foundation (WCF) i [!INCLUDE[wf1](../../../../includes/wf1-md.md)] przykłady. Ten przykład znajduje się w następującym katalogu.  
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Scenario\Services\LinqMessageQueryCorrelation`
