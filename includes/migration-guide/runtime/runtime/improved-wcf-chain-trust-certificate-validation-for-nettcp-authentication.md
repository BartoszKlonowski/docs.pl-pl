---
ms.openlocfilehash: c8f017084fc1ec1eca636ef0178a40559e15b2c5
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/05/2020
ms.locfileid: "89497342"
---
### <a name="improved-wcf-chain-trust-certificate-validation-for-nettcp-certificate-authentication"></a>Ulepszono weryfikację certyfikatu zaufania łańcucha WCF dla uwierzytelniania certyfikatu net. TCP

#### <a name="details"></a>Szczegóły

.NET Framework 4.7.2 ulepsza weryfikację certyfikatu zaufania łańcucha podczas korzystania z uwierzytelniania przy użyciu certyfikatu z zabezpieczeniami transportu za pomocą usługi WCF. W wyniku tego ulepszenia certyfikaty klienta, które są używane do uwierzytelniania na serwerze programu, muszą być skonfigurowane do uwierzytelniania klientów.  Podobne certyfikaty serwera, które są używane do uwierzytelniania serwera, muszą być skonfigurowane do uwierzytelniania serwera. W przypadku tej zmiany, jeśli certyfikat główny jest wyłączony, walidacja łańcucha certyfikatów kończy się niepowodzeniem. Ta sama zmiana została również wprowadzona w .NET Framework 3,5 i nowszych wersjach za pośrednictwem zabezpieczeń systemu Windows. Więcej informacji można znaleźć [tutaj](https://support.microsoft.com/help/4055269/security-only-update-for-net-framework-3-5-1-4-5-2-4-6-4-6-1-4-6-2-4-7). Ta zmiana jest domyślnie włączona i można ją wyłączyć przy użyciu ustawienia konfiguracji.

#### <a name="suggestion"></a>Sugestia

<ul><li>Sprawdź, czy certyfikat serwera i klienta ma wymagany identyfikator OID EKU. W przeciwnym razie zaktualizuj certyfikat.</li><li>Sprawdź, czy certyfikat główny jest nieprawidłowy. W takim przypadku należy zaktualizować certyfikat główny.</li><li>Jak zrezygnować z zmiany: Jeśli nie możesz zaktualizować certyfikatu, możesz obejść problem z nieprzerwaną zmianą tymczasowo przy użyciu poniższego ustawienia konfiguracji, jednak rezygnacja z zmiany spowoduje, że system zostanie narażony na problemy z zabezpieczeniami.</li></ul><pre><code class="lang-xml">&lt;appSettings&gt;&#13;&#10;&lt;add key=&quot;wcf:useLegacyCertificateUsagePolicy&quot; value=&quot;true&quot; /&gt;&#13;&#10;&lt;/appSettings&gt;&#13;&#10;</code></pre>

| Nazwa    | Wartość       |
|:--------|:------------|
| Zakres   |Mały|
|Wersja|4.7.2|
|Typ|Środowisko uruchomieniowe|

#### <a name="affected-apis"></a>Dotyczy interfejsów API

Nie wykrywalne za pośrednictwem analizy interfejsu API.

<!--

#### Affected APIs

Not detectable via API analysis.

-->
