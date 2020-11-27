---
title: 'Instrukcje: określanie poświadczeń zabezpieczeń kanału'
ms.date: 03/30/2017
ms.assetid: f8e03f47-9c4f-4dd5-8f85-429e6d876119
ms.openlocfilehash: 9236985ef461044e480847003d9d249b7e232783
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96266769"
---
# <a name="how-to-specify-channel-security-credentials"></a>Instrukcje: określanie poświadczeń zabezpieczeń kanału

Moniker usługi Windows Communication Foundation (WCF) umożliwia aplikacjom COM wywoływanie usług WCF. Większość usług WCF wymaga od klienta określenia poświadczeń uwierzytelniania i autoryzacji. Podczas wywoływania usługi WCF z poziomu klienta WCF można określić te poświadczenia w kodzie zarządzanym lub w pliku konfiguracyjnym aplikacji. Podczas wywoływania usługi WCF z poziomu aplikacji modelu COM można użyć <xref:System.ServiceModel.ComIntegration.IChannelCredentials> interfejsu, aby określić poświadczenia. W tym temacie przedstawiono różne sposoby określania poświadczeń przy użyciu <xref:System.ServiceModel.ComIntegration.IChannelCredentials> interfejsu.  
  
> [!NOTE]
> <xref:System.ServiceModel.ComIntegration.IChannelCredentials> jest interfejsem IDispatch i nie uzyskasz funkcji IntelliSense w środowisku programu Visual Studio.  
  
 W tym artykule zostanie użyta usługa WCF zdefiniowana w [przykładzie zabezpieczenia wiadomości](../samples/message-security-sample.md).  
  
### <a name="to-specify-a-client-certificate"></a>Aby określić certyfikat klienta  
  
1. Uruchom Setup.bat plik w katalogu zabezpieczeń wiadomości, aby utworzyć i zainstalować wymagane certyfikaty testowe.  
  
2. Otwórz projekt zabezpieczeń wiadomości.  
  
3. Dodaj `[ServiceBehavior(Namespace="http://Microsoft.ServiceModel.Samples")]` do `ICalculator` definicji interfejsu.  
  
4. Dodaj `bindingNamespace="http://Microsoft.ServiceModel.Samples"` do znacznika punktu końcowego w App.config dla usługi.  
  
5. Utwórz próbkę zabezpieczenia komunikatów i uruchom Service.exe. Użyj programu Internet Explorer i przejdź do identyfikatora URI usługi ( `http://localhost:8000/ServiceModelSamples/Service` ), aby upewnić się, że usługa działa.  
  
6. Otwórz Visual Basic 6,0 i Utwórz nowy plik w standardowym pliku. exe. Dodaj przycisk do formularza i kliknij dwukrotnie przycisk, aby dodać następujący kod do procedury obsługi kliknięcia:  
  
    ```vb  
        monString = "service:mexAddress=http://localhost:8000/ServiceModelSamples/Service?wsdl"  
        monString = monString + ", address=http://localhost:8000/ServiceModelSamples/Service"  
        monString = monString + ", contract=ICalculator, contractNamespace=http://Microsoft.ServiceModel.Samples"  
        monString = monString + ", binding=BasicHttpBinding_ICalculator, bindingNamespace=http://Microsoft.ServiceModel.Samples"  
  
        Set monikerProxy = GetObject(monString)  
  
        'Set the Service Certificate.  
     monikerProxy.ChannelCredentials.SetServiceCertificateAuthentication "CurrentUser", "NoCheck", "PeerOrChainTrust"  
    monikerProxy.ChannelCredentials.SetDefaultServiceCertificateFromStore "CurrentUser", "TrustedPeople", "FindBySubjectName", "localhost"  
  
        'Set the Client Certificate.  
        monikerProxy.ChannelCredentials.SetClientCertificateFromStoreByName "CN=client.com", "CurrentUser", "My"  
        MsgBox monikerProxy.Add(3, 4)  
    ```  
  
7. Uruchom aplikację Visual Basic i sprawdź wyniki.  
  
     Aplikacja Visual Basic wyświetli okno komunikatu z wynikiem wywołania Dodawanie (3, 4). <xref:System.ServiceModel.ComIntegration.IChannelCredentials.SetClientCertificateFromFile%28System.String%2CSystem.String%2CSystem.String%29> lub <xref:System.ServiceModel.ComIntegration.IChannelCredentials.SetClientCertificateFromStoreByName%28System.String%2CSystem.String%2CSystem.String%29> można również użyć zamiast tego <xref:System.ServiceModel.ComIntegration.IChannelCredentials.SetClientCertificateFromStore%28System.String%2CSystem.String%2CSystem.String%2CSystem.Object%29> , aby ustawić certyfikat klienta:  
  
    ```vb  
    monikerProxy.ChannelCredentials.SetClientCertificateFromFile "C:\MyClientCert.pfx", "password", "DefaultKeySet"  
    ```  
  
> [!NOTE]
> Aby to wywołanie działało, certyfikat klienta musi być zaufany na komputerze, na którym jest uruchomiony klient programu.  
  
> [!NOTE]
> Jeśli moniker jest źle sformułowany lub usługa jest niedostępna, wywołanie `GetObject` zwróci komunikat o błędzie informujący o nieprawidłowej składni. Jeśli wystąpi ten błąd, upewnij się, że moniker, którego używasz, jest poprawna i że usługa jest dostępna.  
  
### <a name="to-specify-user-name-and-password"></a>Aby określić nazwę użytkownika i hasło  
  
1. Zmodyfikuj plik App.config usługi, aby użyć programu `wsHttpBinding` . Jest to wymagane do weryfikacji nazwy użytkownika i hasła:  

2. Ustaw `clientCredentialType` nazwę użytkownika na:  

3. Otwórz Visual Basic 6,0 i Utwórz nowy plik w standardowym pliku. exe. Dodaj przycisk do formularza i kliknij dwukrotnie przycisk, aby dodać następujący kod do procedury obsługi kliknięcia:  
  
    ```vb
    monString = "service:mexAddress=http://localhost:8000/ServiceModelSamples/Service?wsdl"  
    monString = monString + ", address=http://localhost:8000/ServiceModelSamples/Service"  
    monString = monString + ", contract=ICalculator, contractNamespace=http://Microsoft.ServiceModel.Samples"  
    monString = monString + ", binding=WSHttpBinding_ICalculator, bindingNamespace=http://Microsoft.ServiceModel.Samples"  
  
    Set monikerProxy = GetObject(monString)  
  
    monikerProxy.ChannelCredentials.SetServiceCertificateAuthentication "CurrentUser", "NoCheck", "PeerOrChainTrust"  
    monikerProxy.ChannelCredentials.SetUserNameCredential "username", "password"  
  
    MsgBox monikerProxy.Add(3, 4)  
    ```  
  
4. Uruchom aplikację Visual Basic i sprawdź wyniki. Aplikacja Visual Basic wyświetli okno komunikatu z wynikiem wywołania Dodawanie (3, 4).  
  
    > [!NOTE]
    > Powiązanie określone w monikerze usługi w tym przykładzie zostało zmienione na WSHttpBinding_ICalculator. Należy również pamiętać, że w wywołaniu metody należy podać prawidłową nazwę użytkownika i hasło <xref:System.ServiceModel.ComIntegration.IChannelCredentials.SetUserNameCredential%28System.String%2CSystem.String%29> .  
  
### <a name="to-specify-windows-credentials"></a>Aby określić poświadczenia systemu Windows  
  
1. Ustaw `clientCredentialType` dla systemu Windows w pliku App.config usługi:  

2. Otwórz Visual Basic 6,0 i Utwórz nowy plik w standardowym pliku. exe. Dodaj przycisk do formularza i kliknij dwukrotnie przycisk, aby dodać następujący kod do procedury obsługi kliknięcia:  
  
    ```vb
    monString = "service:mexAddress=http://localhost:8000/ServiceModelSamples/Service?wsdl"  
    monString = monString + ", address=http://localhost:8000/ServiceModelSamples/Service"  
    monString = monString + ", contract=ICalculator, contractNamespace=http://Microsoft.ServiceModel.Samples"  
    monString = monString + ", binding=WSHttpBinding_ICalculator, bindingNamespace=http://Microsoft.ServiceModel.Samples"  
    monString = monString + ", upnidentity=domain\userID"  
  
    Set monikerProxy = GetObject(monString)  
     monikerProxy.ChannelCredentials.SetWindowsCredential "domain", "userID", "password", 1, True  
  
    MsgBox monikerProxy.Add(3, 4)  
    ```  
  
3. Uruchom aplikację Visual Basic i sprawdź wyniki. Aplikacja Visual Basic wyświetli okno komunikatu z wynikiem wywołania Dodawanie (3, 4).  
  
    > [!NOTE]
    > Należy zastąpić wartości "Domain", "userID" i "Password" prawidłowymi wartościami.  
  
### <a name="to-specify-an-issue-token"></a>Aby określić token problemu  
  
1. Tokeny wystawiania są używane tylko w przypadku aplikacji korzystających z zabezpieczeń federacyjnych. Aby uzyskać więcej informacji na temat zabezpieczeń federacyjnych, zobacz [federacyjne i wystawione tokeny](federation-and-issued-tokens.md) i [przykład Federacji](../samples/federation-sample.md).  
  
     Poniższy przykład kodu Visual Basic ilustruje sposób wywołania <xref:System.ServiceModel.ComIntegration.IChannelCredentials.SetIssuedToken%28System.String%2CSystem.String%2CSystem.String%29> metody:  
  
    ```vb
        monString = "service:mexAddress=http://localhost:8000/ServiceModelSamples/Service?wsdl"  
        monString = monString + ", address=http://localhost:8000/SomeService/Service"  
        monString = monString + ", contract=ICalculator, contractNamespace=http://SomeService.Samples"  
        monString = monString + ", binding=WSHttpBinding_ISomeContract, bindingNamespace=http://SomeService.Samples"  
  
        Set monikerProxy = GetObject(monString)  
    monikerProxy.SetIssuedToken("http://somemachine/sts", "bindingType", "binding")  
    ```  
  
     Aby uzyskać więcej informacji na temat parametrów dla tej metody, zobacz <xref:System.ServiceModel.ComIntegration.IChannelCredentials.SetIssuedToken%28System.String%2CSystem.String%2CSystem.String%29> .  
  
## <a name="see-also"></a>Zobacz też

- [Federacja](federation.md)
- [Instrukcje: konfigurowanie poświadczeń usługi federacyjnej](how-to-configure-credentials-on-a-federation-service.md)
- [Instrukcje: tworzenie klienta federacyjnego](how-to-create-a-federated-client.md)
- [Zabezpieczenia komunikatów](message-security-in-wcf.md)
- [Wiązania i zabezpieczenia](bindings-and-security.md)
