---
ms.openlocfilehash: f6553444e13416850a398ae5bcb6574f2a69bd2d
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96478486"
---
### <a name="improved-wcf-chain-trust-certificate-validation-for-nettcp-certificate-authentication"></a><span data-ttu-id="fe343-101">Ulepszono weryfikację certyfikatu zaufania łańcucha WCF dla uwierzytelniania certyfikatu net. TCP</span><span class="sxs-lookup"><span data-stu-id="fe343-101">Improved WCF chain trust certificate validation for Net.Tcp certificate authentication</span></span>

#### <a name="details"></a><span data-ttu-id="fe343-102">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="fe343-102">Details</span></span>

<span data-ttu-id="fe343-103">.NET Framework 4.7.2 ulepsza weryfikację certyfikatu zaufania łańcucha podczas korzystania z uwierzytelniania przy użyciu certyfikatu z zabezpieczeniami transportu za pomocą usługi WCF.</span><span class="sxs-lookup"><span data-stu-id="fe343-103">.NET Framework 4.7.2 improves chain trust certificate validation when using certificate authentication with transport security with WCF.</span></span> <span data-ttu-id="fe343-104">W wyniku tego ulepszenia certyfikaty klienta, które są używane do uwierzytelniania na serwerze programu, muszą być skonfigurowane do uwierzytelniania klientów.</span><span class="sxs-lookup"><span data-stu-id="fe343-104">With this improvement, client certificates that are used to authenticate to a server must be configured for client authentication.</span></span>  <span data-ttu-id="fe343-105">Podobne certyfikaty serwera, które są używane do uwierzytelniania serwera, muszą być skonfigurowane do uwierzytelniania serwera.</span><span class="sxs-lookup"><span data-stu-id="fe343-105">Similarly server certificates that are for the authenticating a server must be configured for server authentication.</span></span> <span data-ttu-id="fe343-106">W przypadku tej zmiany, jeśli certyfikat główny jest wyłączony, walidacja łańcucha certyfikatów kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="fe343-106">With this change, if the root certificate is disabled, the certificate chain validation fails.</span></span> <span data-ttu-id="fe343-107">Ta sama zmiana została również wprowadzona w .NET Framework 3,5 i nowszych wersjach za pośrednictwem zabezpieczeń systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="fe343-107">The same change was also made to .NET Framework 3.5 and later versions via Windows security roll-up.</span></span> <span data-ttu-id="fe343-108">Więcej informacji można znaleźć [tutaj](https://support.microsoft.com/help/4055269/security-only-update-for-net-framework-3-5-1-4-5-2-4-6-4-6-1-4-6-2-4-7). Ta zmiana jest domyślnie włączona i można ją wyłączyć przy użyciu ustawienia konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="fe343-108">You can find more information [here](https://support.microsoft.com/help/4055269/security-only-update-for-net-framework-3-5-1-4-5-2-4-6-4-6-1-4-6-2-4-7).This change is on by default and can be turned off by a configuration setting.</span></span>

#### <a name="suggestion"></a><span data-ttu-id="fe343-109">Sugestia</span><span class="sxs-lookup"><span data-stu-id="fe343-109">Suggestion</span></span>

<ul><li><span data-ttu-id="fe343-110">Sprawdź, czy certyfikat serwera i klienta ma wymagany identyfikator OID EKU.</span><span class="sxs-lookup"><span data-stu-id="fe343-110">Validate if your server and client certification has the required EKU OID.</span></span> <span data-ttu-id="fe343-111">W przeciwnym razie zaktualizuj certyfikat.</span><span class="sxs-lookup"><span data-stu-id="fe343-111">If not, update your certification.</span></span></li><li><span data-ttu-id="fe343-112">Sprawdź, czy certyfikat główny jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="fe343-112">Validate if your root certificate is invalid.</span></span> <span data-ttu-id="fe343-113">W takim przypadku należy zaktualizować certyfikat główny.</span><span class="sxs-lookup"><span data-stu-id="fe343-113">If so, update the root certificate.</span></span></li><li><span data-ttu-id="fe343-114">Jak zrezygnować z zmiany: Jeśli nie możesz zaktualizować certyfikatu, możesz obejść zmiany w sposób tymczasowy, korzystając z następującego ustawienia konfiguracji, jednak rezygnacja z zmiany spowoduje, że system będzie narażony na problem z zabezpieczeniami.</span><span class="sxs-lookup"><span data-stu-id="fe343-114">How to opt out of the change: If you can't update the certificate, you can work around the breaking change temporarily with the following configuration setting,  However, opting out of the change will leave your system vulnerable to the security issue.</span></span></li></ul><pre><code class="lang-xml">&lt;appSettings&gt;&#13;&#10;&lt;add key=&quot;wcf:useLegacyCertificateUsagePolicy&quot; value=&quot;true&quot; /&gt;&#13;&#10;&lt;/appSettings&gt;&#13;&#10;</code></pre>

| <span data-ttu-id="fe343-115">Nazwa</span><span class="sxs-lookup"><span data-stu-id="fe343-115">Name</span></span>    | <span data-ttu-id="fe343-116">Wartość</span><span class="sxs-lookup"><span data-stu-id="fe343-116">Value</span></span>       |
|:--------|:------------|
| <span data-ttu-id="fe343-117">Zakres</span><span class="sxs-lookup"><span data-stu-id="fe343-117">Scope</span></span>   |<span data-ttu-id="fe343-118">Mały</span><span class="sxs-lookup"><span data-stu-id="fe343-118">Minor</span></span>|
|<span data-ttu-id="fe343-119">Wersja</span><span class="sxs-lookup"><span data-stu-id="fe343-119">Version</span></span>|<span data-ttu-id="fe343-120">4.7.2</span><span class="sxs-lookup"><span data-stu-id="fe343-120">4.7.2</span></span>|
|<span data-ttu-id="fe343-121">Typ</span><span class="sxs-lookup"><span data-stu-id="fe343-121">Type</span></span>|<span data-ttu-id="fe343-122">Środowisko uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="fe343-122">Runtime</span></span>|

#### <a name="affected-apis"></a><span data-ttu-id="fe343-123">Dotyczy interfejsów API</span><span class="sxs-lookup"><span data-stu-id="fe343-123">Affected APIs</span></span>

<span data-ttu-id="fe343-124">Nie wykrywalne za pośrednictwem analizy interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="fe343-124">Not detectable via API analysis.</span></span>

<!--

#### Affected APIs

Not detectable via API analysis.

-->
