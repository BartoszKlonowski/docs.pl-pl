---
title: Zabezpieczenia transportu z uwierzytelnianiem podstawowym
description: Zapoznaj się z tym scenariuszem WCF, który zawiera podstawowe uwierzytelnianie dla usługi i klienta programu WCF. Usługa musi mieć prawidłowy certyfikat, którego ufa klient.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: b54f491d-196b-4279-876c-76b83ec0442c
ms.openlocfilehash: e821f8ed3996e9119c6f2c06ec6533c575bf75dd
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96251844"
---
# <a name="transport-security-with-basic-authentication"></a>Zabezpieczenia transportu z uwierzytelnianiem podstawowym

Na poniższej ilustracji przedstawiono usługę i klienta Windows Communication Foundation (WCF). Serwer musi mieć prawidłowy certyfikat X. 509, który może być używany dla SSL (SSL), a klienci muszą ufać certyfikatowi serwera. Ponadto usługa sieci Web ma już implementację protokołu SSL, która może być używana. Aby uzyskać więcej informacji na temat włączania uwierzytelniania podstawowego na Internet Information Services (IIS), zobacz <https://docs.microsoft.com/iis/configuration/system.webserver/security/authentication/basicauthentication> .  
  
 ![Zrzut ekranu przedstawiający zabezpieczenia transportu z uwierzytelnianiem podstawowym.](./media/transport-security-with-basic-authentication/transport-security-basic-authentication.gif)  
  
|Charakterystyka|Opis|  
|--------------------|-----------------|  
|Tryb zabezpieczeń|Transport|  
|Współdziałanie|Z istniejącymi usługami i klientami usług sieci Web|  
|Uwierzytelnianie (serwer)<br /><br /> Uwierzytelnianie (klient)|Tak (przy użyciu protokołu HTTPS)<br /><br /> Tak (za poorednictwem nazwy użytkownika/hasła)|  
|Integralność|Tak|  
|Poufność|Tak|  
|Transport|HTTPS|  
|Wiązanie|<xref:System.ServiceModel.WSHttpBinding>|  
  
## <a name="service"></a>Usługa  

 Poniższy kod i konfiguracja są przeznaczone do niezależnego uruchamiania. Wykonaj jedną z następujących czynności:  
  
- Tworzenie usługi autonomicznej przy użyciu kodu bez konfiguracji.  
  
- Utwórz usługę przy użyciu podanej konfiguracji, ale nie Definiuj żadnych punktów końcowych.  
  
### <a name="code"></a>Kod  

 Poniższy kod przedstawia sposób tworzenia punktu końcowego usługi, który używa nazwy użytkownika i hasła domeny systemu Windows do zabezpieczenia transferu. Należy pamiętać, że usługa wymaga certyfikatu X. 509 do uwierzytelnienia na kliencie. Aby uzyskać więcej informacji, zobacz [Praca z certyfikatami](working-with-certificates.md) i [instrukcje: Konfigurowanie portu z certyfikatem SSL](how-to-configure-a-port-with-an-ssl-certificate.md).  
  
 [!code-csharp[C_SecurityScenarios#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#1)]
 [!code-vb[C_SecurityScenarios#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#1)]  
  
## <a name="configuration"></a>Konfigurowanie  

 Poniżej przedstawiono Konfigurowanie usługi do korzystania z uwierzytelniania podstawowego z zabezpieczeniami na poziomie transportu:  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
    <system.serviceModel>  
        <bindings>  
            <wsHttpBinding>  
                <binding name="UsernameWithTransport">  
                    <security mode="Transport">  
                        <transport clientCredentialType="Basic" />  
                    </security>  
                </binding>  
            </wsHttpBinding>  
        </bindings>  
        <services>  
            <service name="BasicAuthentication.Calculator">  
                <endpoint address="https://localhost/Calculator"  
                          binding="wsHttpBinding"
                          bindingConfiguration="UsernameWithTransport"  
                          name="BasicEndpoint"
                          contract="BasicAuthentication.ICalculator" />  
            </service>  
        </services>  
    </system.serviceModel>  
</configuration>  
```  
  
## <a name="client"></a>Klient  
  
### <a name="code"></a>Kod  

 Poniższy kod przedstawia kod klienta, który zawiera nazwę użytkownika i hasło. Należy pamiętać, że użytkownik musi podać prawidłową nazwę użytkownika i hasło systemu Windows. Kod, który ma zwrócić nazwę użytkownika i hasło, nie jest tutaj wyświetlany. Użyj okna dialogowego lub innego interfejsu, aby wysłać zapytanie do użytkownika o informacje.  
  
> [!NOTE]
> Nazwę użytkownika i hasło można ustawić tylko przy użyciu kodu.  
  
 [!code-csharp[C_SecurityScenarios#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#2)]
 [!code-vb[C_SecurityScenarios#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#2)]  
  
### <a name="configuration"></a>Konfigurowanie  

 Poniższy kod przedstawia konfigurację klienta.  
  
> [!NOTE]
> Nie można użyć konfiguracji w celu ustawienia nazwy użytkownika i hasła. Pokazana tutaj konfiguracja musi zostać uzupełniona przy użyciu kodu w celu ustawienia nazwy użytkownika i hasła.  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
  <system.serviceModel>  
    <bindings>  
      <wsHttpBinding>  
        <binding name="WSHttpBinding_ICalculator" >  
          <security mode="Transport">  
            <transport clientCredentialType="Basic" />  
          </security>  
        </binding>  
      </wsHttpBinding>  
    </bindings>  
    <client>  
      <endpoint address="https://machineName/Calculator"
                binding="wsHttpBinding"  
                bindingConfiguration="WSHttpBinding_ICalculator"
                contract="ICalculator"  
                name="WSHttpBinding_ICalculator" />  
    </client>  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A>
- <xref:System.ServiceModel.Security.UserNamePasswordClientCredential>
- [Praca z certyfikatami](working-with-certificates.md)
- [Instrukcje: konfigurowanie portu z certyfikatem SSL](how-to-configure-a-port-with-an-ssl-certificate.md)
- [Przegląd zabezpieczeń](security-overview.md)
- [\<clientCredentials>](../../configure-apps/file-schema/wcf/clientcredentials.md)
- [Model zabezpieczeń dla sieci szkieletowej aplikacji systemu Windows Server](/previous-versions/appfabric/ee677202(v=azure.10))
