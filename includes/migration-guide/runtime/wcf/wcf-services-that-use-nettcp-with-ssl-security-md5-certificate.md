---
ms.openlocfilehash: afcb9b950d4c47b4251dcc8ab0cf9cfc702005c8
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/05/2020
ms.locfileid: "89497752"
---
### <a name="wcf-services-that-use-nettcp-with-ssl-security-and-md5-certificate-authentication"></a>Usługi WCF korzystające z NETTCP z zabezpieczeniami SSL i uwierzytelnianiem certyfikatu MD5

#### <a name="details"></a>Szczegóły

.NET Framework 4,6 dodaje protokoły TLS 1,1 i TLS 1,2 do listy domyślnych protokołów protokołu SSL WCF. Gdy komputery klienckie i serwery mają zainstalowany .NET Framework 4,6 lub nowszy, protokół TLS 1,2 jest używany do negocjacji. Protokół TLS 1,2 nie obsługuje uwierzytelniania certyfikatów MD5. W związku z tym, jeśli klient korzysta z certyfikatu MD5, klient programu WCF nie będzie mógł nawiązać połączenia z usługą WCF.

#### <a name="suggestion"></a>Sugestia

Ten problem można obejść, aby klient programu WCF mógł połączyć się z serwerem WCF, wykonując jedną z następujących czynności:

- Zaktualizuj certyfikat, aby nie używał algorytmu MD5. Jest to zalecane rozwiązanie.
- Jeśli powiązanie nie jest konfigurowane dynamicznie w kodzie źródłowym, zaktualizuj plik konfiguracji aplikacji tak, aby korzystał z protokołu TLS 1,1 lub starszej wersji. Dzięki temu można nadal używać certyfikatu z algorytmem wyznaczania wartości skrótu MD5.

> [!WARNING]
> To obejście nie jest zalecane, ponieważ certyfikat z algorytmem wyznaczania wartości skrótu MD5 jest uznawany za niezabezpieczony.

Następujący plik konfiguracji wykonuje następujące czynności:

```xml
<configuration>
  <system.serviceModel>
    <bindings>
      <netTcpBinding>
        <binding>
          <security mode= "None/Transport/Message/TransportWithMessageCredential" >
            <transport clientCredentialType="None/Windows/Certificate"
                       protectionLevel="None/Sign/EncryptAndSign"
                       sslProtocols="Ssl3/Tls1/Tls11">
            </transport>
          </security>
        </binding>
      </netTcpBinding>
    </bindings>
  </system.ServiceModel>
</configuration>
```

- Jeśli powiązanie jest konfigurowane dynamicznie w kodzie źródłowym, zaktualizuj właściwość tak, <xref:System.ServiceModel.TcpTransportSecurity.SslProtocols?displayProperty=nameWithType> aby używała protokołu TLS 1,1 ( <xref:System.Security.Authentication.SslProtocols.Tls11?displayProperty=nameWithType> lub starszej wersji protokołu w kodzie źródłowym.

> [!WARNING]
> To obejście nie jest zalecane, ponieważ certyfikat z algorytmem wyznaczania wartości skrótu MD5 jest uznawany za niezabezpieczony.

| Nazwa    | Wartość   |
|:--------|:--------|
| Zakres   | Mały   |
| Wersja | 4,6     |
| Typ    | Środowisko uruchomieniowe |

#### <a name="affected-apis"></a>Dotyczy interfejsów API

Nie wykrywalne za pośrednictwem analizy interfejsu API.

<!--

#### Affected APIs

Not detectable via API analysis.

-->
