---
title: Zabezpieczanie komunikatów za pomocą klienta systemu Windows bez negocjowania poświadczeń
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: fc07a26c-cbee-41c5-8fb0-329085fef749
ms.openlocfilehash: 3e5838c474a4f13136ed29baab440dc1559b95f5
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90551096"
---
# <a name="message-security-with-a-windows-client-without-credential-negotiation"></a>Zabezpieczanie komunikatów za pomocą klienta systemu Windows bez negocjowania poświadczeń

W poniższym scenariuszu przedstawiono klienta i usługę Windows Communication Foundation (WCF), zabezpieczone przez protokół Kerberos.

Zarówno usługa, jak i klient znajdują się w tej samej domenie lub domenach zaufanych.

> [!NOTE]
> Różnica między tym scenariuszem a [zabezpieczeniami komunikatów klienta systemu Windows](message-security-with-a-windows-client.md) polega na tym, że ten scenariusz nie negocjuje poświadczeń usługi z usługą przed wysłaniem komunikatu aplikacji. Ponadto, ponieważ wymaga to protokołu Kerberos, ten scenariusz wymaga środowiska domeny systemu Windows.

![Zabezpieczenia komunikatów bez negocjowania poświadczeń](media/0c9f9baa-2439-4ef9-92f4-43c242d85d0d.gif "0c9f9baa-2439-4ef9-92f4-43c242d85d0d")

|Charakterystyka|Opis|
|--------------------|-----------------|
|Tryb zabezpieczeń|Wiadomość|
|Współdziałanie|Tak, WS-Security z klientami zgodnymi z profilem tokenu Kerberos|
|Uwierzytelnianie (serwer)|Wzajemne uwierzytelnianie serwera i klienta|
|Uwierzytelnianie (klient)|Wzajemne uwierzytelnianie serwera i klienta|
|Integralność|Yes|
|Poufność|Yes|
|Transport|HTTP|
|Wiązanie|<xref:System.ServiceModel.WSHttpBinding>|

## <a name="service"></a>Usługa

Poniższy kod i konfiguracja są przeznaczone do niezależnego uruchamiania. Wykonaj jedną z następujących czynności:

- Tworzenie usługi autonomicznej przy użyciu kodu bez konfiguracji.

- Utwórz usługę przy użyciu podanej konfiguracji, ale nie Definiuj żadnych punktów końcowych.

### <a name="code"></a>Kod

Poniższy kod tworzy punkt końcowy usługi, który korzysta z zabezpieczeń komunikatów. Kod wyłącza negocjowanie poświadczeń usługi i ustanawia token kontekstu zabezpieczeń (SCT).

> [!NOTE]
> Aby użyć typu poświadczeń systemu Windows bez negocjowania, konto użytkownika usługi musi mieć dostęp do głównej nazwy usługi (SPN), która jest zarejestrowana w domenie Active Directory. Możesz to zrobić na dwa sposoby:

1. Użyj `NetworkService` konta lub, `LocalSystem` Aby uruchomić usługę. Ponieważ te konta mają dostęp do nazwy SPN maszyny, która została ustanowiona, gdy komputer jest przyłączony do domeny Active Directory, funkcja WCF automatycznie generuje prawidłowy element SPN w ramach punktu końcowego usługi w metadanych (Web Services Description Language lub WSDL) usługi.

2. Użyj dowolnego konta domeny Active Directory, aby uruchomić usługę. W takim przypadku należy ustanowić nazwę SPN dla tego konta domeny. Jednym z nich jest użycie narzędzia Setspn.exe narzędzie. Po utworzeniu nazwy SPN dla konta usługi Skonfiguruj funkcję WCF do publikowania tej nazwy SPN na klientach usługi za pomocą metadanych (WSDL). W tym celu należy ustawić tożsamość punktu końcowego dla uwidocznionego punktu końcowego, chociaż plik lub kod konfiguracyjny aplikacji. Poniższy przykład umożliwia programistyczne publikowanie tożsamości.

Aby uzyskać więcej informacji na temat nazw SPN, protokołu Kerberos i Active Directory, zobacz [dodatek dotyczący protokołu Kerberos dla systemu Windows](/previous-versions/msp-n-p/ff649429(v=pandp.10)). Aby uzyskać więcej informacji na temat tożsamości punktów końcowych, zobacz [elementu SecurityBindingElement Authentication Modes](securitybindingelement-authentication-modes.md).

[!code-csharp[C_SecurityScenarios#12](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#12)]
[!code-vb[C_SecurityScenarios#12](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#12)]

### <a name="configuration"></a>Konfiguracja

Można użyć poniższej konfiguracji zamiast kodu.

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.serviceModel>
    <behaviors />
    <services>
      <service behaviorConfiguration="" name="ServiceModel.Calculator">
        <endpoint address="http://localhost/Calculator"
                  binding="wsHttpBinding"
                  bindingConfiguration="KerberosBinding"
                  name="WSHttpBinding_ICalculator"
                  contract="ServiceModel.ICalculator"
                  listenUri="net.tcp://localhost/metadata" >
         <identity>
            <servicePrincipalName value="service_spn_name" />
         </identity>
        </endpoint>
      </service>
    </services>
    <bindings>
      <wsHttpBinding>
        <binding name="KerberosBinding">
          <security>
            <message negotiateServiceCredential="false"
                     establishSecurityContext="false" />
          </security>
        </binding>
      </wsHttpBinding>
    </bindings>
    <client />
  </system.serviceModel>
</configuration>
```

## <a name="client"></a>Klient

Poniższy kod i konfiguracja są przeznaczone do niezależnego uruchamiania. Wykonaj jedną z następujących czynności:

- Utwórz klienta autonomicznego przy użyciu kodu (i kodu klienta).

- Utwórz klienta, który nie definiuje żadnych adresów punktów końcowych. Zamiast tego należy użyć konstruktora klienta, który przyjmuje nazwę konfiguracji jako argument. Na przykład:

  [!code-csharp[C_SecurityScenarios#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#0)]
  [!code-vb[C_SecurityScenarios#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#0)]

### <a name="code"></a>Kod

Poniższy kod konfiguruje klienta. Tryb zabezpieczeń jest ustawiony na wartość komunikat, a typ poświadczeń klienta to Windows. Należy pamiętać, <xref:System.ServiceModel.MessageSecurityOverHttp.NegotiateServiceCredential%2A> że <xref:System.ServiceModel.NonDualMessageSecurityOverHttp.EstablishSecurityContext%2A> właściwości i są ustawione na `false` .

> [!NOTE]
> Aby użyć typu poświadczeń systemu Windows bez negocjowania, przed rozpoczęciem komunikacji z usługą należy skonfigurować klienta przy użyciu nazwy SPN konta usługi. Klient używa nazwy SPN, aby uzyskać token Kerberos do uwierzytelniania i zabezpieczania komunikacji z usługą. Poniższy przykład pokazuje, jak skonfigurować klienta przy użyciu nazwy SPN usługi. Jeśli używasz narzędzia do obsługi [metadanych ServiceModel (Svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md) do wygenerowania klienta, Nazwa SPN usługi zostanie automatycznie rozpropagowana do klienta z metadanych usługi (WSDL), jeśli metadane usługi zawierają te informacje. Więcej informacji o sposobie konfigurowania usługi w celu uwzględnienia jej nazwy SPN w metadanych usługi znajduje się w sekcji "usługa" w dalszej części tego tematu.
>
> Aby uzyskać więcej informacji na temat nazw SPN, Kerberos i Active Directory, zobacz [dodatek dotyczący protokołu Kerberos dla systemu Windows](/previous-versions/msp-n-p/ff649429(v=pandp.10)). Aby uzyskać więcej informacji na temat tożsamości punktów końcowych, zobacz temat [tryby uwierzytelniania elementu SecurityBindingElement](securitybindingelement-authentication-modes.md) .

[!code-csharp[C_SecurityScenarios#19](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#19)]
[!code-vb[C_SecurityScenarios#19](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#19)]

### <a name="configuration"></a>Konfiguracja

Poniższy kod konfiguruje klienta. Należy pamiętać, że [\<servicePrincipalName>](../../configure-apps/file-schema/wcf/serviceprincipalname.md) element musi być ustawiony jako zgodny z nazwą SPN usługi zarejestrowanej dla konta usługi w domenie Active Directory.

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.serviceModel>
    <bindings>
      <wsHttpBinding>
        <binding name="WSHttpBinding_ICalculator" >
          <security mode="Message">
            <message clientCredentialType="Windows"
                     negotiateServiceCredential="false"
                     establishSecurityContext="false" />
          </security>
        </binding>
      </wsHttpBinding>
    </bindings>
    <client>
      <endpoint address="http://localhost/Calculator"
                binding="wsHttpBinding"
                bindingConfiguration="WSHttpBinding_ICalculator"
                contract="ICalculator"
                name="WSHttpBinding_ICalculator">
        <identity>
          <servicePrincipalName value="service_spn_name" />
        </identity>
      </endpoint>
    </client>
  </system.serviceModel>
</configuration>
```

## <a name="see-also"></a>Zobacz także

- [Przegląd zabezpieczeń](security-overview.md)
- [Uwierzytelnianie i tożsamość usług](service-identity-and-authentication.md)
- [Model zabezpieczeń dla sieci szkieletowej aplikacji systemu Windows Server](/previous-versions/appfabric/ee677202(v=azure.10))
