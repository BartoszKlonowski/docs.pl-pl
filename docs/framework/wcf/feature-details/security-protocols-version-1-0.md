---
title: Protokoły zabezpieczeń wersja 1.0
ms.date: 03/30/2017
ms.assetid: ee3402d2-1076-410b-a3cb-fae0372bd7af
ms.openlocfilehash: aa6e99365bf318f5f1aea6fe1f45eb1911fc901a
ms.sourcegitcommit: fe8877e564deb68d77fa4b79f55584ac8d7e8997
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/17/2020
ms.locfileid: "90720260"
---
# <a name="security-protocols-version-10"></a><span data-ttu-id="c7f6d-102">Protokoły zabezpieczeń wersja 1.0</span><span class="sxs-lookup"><span data-stu-id="c7f6d-102">Security Protocols version 1.0</span></span>
<span data-ttu-id="c7f6d-103">Protokoły zabezpieczenia usług w sieci Web zapewniają mechanizmy zabezpieczeń usług sieci Web, które obejmują wszystkie istniejące wymagania dotyczące zabezpieczeń dotyczące komunikatów w przedsiębiorstwie.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-103">The Web Services Security Protocols provide Web services security mechanisms that cover all existing enterprise messaging security requirements.</span></span> <span data-ttu-id="c7f6d-104">W tej sekcji opisano szczegóły dotyczące programu Windows Communication Foundation (WCF) w wersji 1,0 (zaimplementowane w programie <xref:System.ServiceModel.Channels.SecurityBindingElement> ) dla następujących protokołów zabezpieczeń usług sieci Web.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-104">This section describes the Windows Communication Foundation (WCF) version 1.0 details (implemented in the <xref:System.ServiceModel.Channels.SecurityBindingElement>) for the following Web services security protocols.</span></span>  
  
|<span data-ttu-id="c7f6d-105">Specyfikacja/dokument</span><span class="sxs-lookup"><span data-stu-id="c7f6d-105">Specification/Document</span></span>|<span data-ttu-id="c7f6d-106">Łącze</span><span class="sxs-lookup"><span data-stu-id="c7f6d-106">Link</span></span>|  
|-|-|  
|<span data-ttu-id="c7f6d-107">WSS: zabezpieczenia komunikatów SOAP 1,0</span><span class="sxs-lookup"><span data-stu-id="c7f6d-107">WSS: SOAP Message Security 1.0</span></span>|<https://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-soap-message-security-1.0.pdf>|
|<span data-ttu-id="c7f6d-108">WSS: Nazwa użytkownika — profil tokenu 1,0</span><span class="sxs-lookup"><span data-stu-id="c7f6d-108">WSS: Username Token Profile 1.0</span></span>|<https://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-username-token-profile-1.0.pdf>|
|<span data-ttu-id="c7f6d-109">WSS: Profil tokenu x509 1,0</span><span class="sxs-lookup"><span data-stu-id="c7f6d-109">WSS: X509 Token Profile 1.0</span></span>|<https://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-x509-token-profile-1.0.pdf>|
|<span data-ttu-id="c7f6d-110">WSS: Profil tokenu SAML 1,1 1,0</span><span class="sxs-lookup"><span data-stu-id="c7f6d-110">WSS: SAML 1.1 Token Profile 1.0</span></span>|<https://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.0.pdf>|
|<span data-ttu-id="c7f6d-111">WSS: zabezpieczenia komunikatów SOAP 1,1</span><span class="sxs-lookup"><span data-stu-id="c7f6d-111">WSS: SOAP Message Security 1.1</span></span>|<https://www.oasis-open.org/committees/download.php/16790/wss-v1.1-spec-os-SOAPMessageSecurity.pdf>|
|<span data-ttu-id="c7f6d-112">Nazwa użytkownika programu WSS username profile 1,1</span><span class="sxs-lookup"><span data-stu-id="c7f6d-112">WSS Username Token Profile 1.1</span></span>|<https://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-username-token-profile-1.0.pdf>|
|<span data-ttu-id="c7f6d-113">WSS: Profil tokenu X. 509 1,1</span><span class="sxs-lookup"><span data-stu-id="c7f6d-113">WSS: X.509 Token Profile 1.1</span></span>|<https://www.oasis-open.org/committees/download.php/16785/wss-v1.1-spec-os-x509TokenProfile.pdf>|
|<span data-ttu-id="c7f6d-114">WSS: Profil tokenu Kerberos 1,1</span><span class="sxs-lookup"><span data-stu-id="c7f6d-114">WSS: Kerberos Token Profile 1.1</span></span>|<https://www.oasis-open.org/committees/download.php/16788/wss-v1.1-spec-os-KerberosTokenProfile.pdf>|
|<span data-ttu-id="c7f6d-115">WSS: Profil tokenu SAML 1,1 1,1</span><span class="sxs-lookup"><span data-stu-id="c7f6d-115">WSS: SAML 1.1 Token Profile 1.1</span></span>|<https://www.oasis-open.org/committees/download.php/16768/wss-v1.1-spec-os-SAMLTokenProfile.pdf>|
|<span data-ttu-id="c7f6d-116">Bezpieczna konwersacja WS-Secure</span><span class="sxs-lookup"><span data-stu-id="c7f6d-116">WS-Secure Conversation</span></span>|<http://specs.xmlsoap.org/ws/2005/02/sc/WS-SecureConversation.pdf>|
|<span data-ttu-id="c7f6d-117">Usługa WS-Trust</span><span class="sxs-lookup"><span data-stu-id="c7f6d-117">WS-Trust</span></span>|<http://specs.xmlsoap.org/ws/2005/02/trust/ws-trust.pdf>|
|<span data-ttu-id="c7f6d-118">Uwaga dotycząca aplikacji:</span><span class="sxs-lookup"><span data-stu-id="c7f6d-118">Application Note:</span></span><br /><br /> <span data-ttu-id="c7f6d-119">Uzgadnianie przy użyciu protokołu WS-Trust for TLS</span><span class="sxs-lookup"><span data-stu-id="c7f6d-119">Using WS-Trust for TLS Handshake</span></span>|<span data-ttu-id="c7f6d-120">Do opublikowania</span><span class="sxs-lookup"><span data-stu-id="c7f6d-120">To be published</span></span>|  
|<span data-ttu-id="c7f6d-121">Uwaga dotycząca aplikacji:</span><span class="sxs-lookup"><span data-stu-id="c7f6d-121">Application Note:</span></span><br /><br /> <span data-ttu-id="c7f6d-122">Korzystanie z protokołu WS-Trust dla SPNEGO</span><span class="sxs-lookup"><span data-stu-id="c7f6d-122">Using WS-Trust for SPNEGO</span></span>|<span data-ttu-id="c7f6d-123">Do opublikowania</span><span class="sxs-lookup"><span data-stu-id="c7f6d-123">To be published</span></span>|  
|<span data-ttu-id="c7f6d-124">Uwaga dotycząca aplikacji:</span><span class="sxs-lookup"><span data-stu-id="c7f6d-124">Application Note:</span></span><br /><br /> <span data-ttu-id="c7f6d-125">Odwołania i tożsamość punktów końcowych usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="c7f6d-125">Web Services Addressing Endpoint References And Identity</span></span>|<span data-ttu-id="c7f6d-126">Do opublikowania</span><span class="sxs-lookup"><span data-stu-id="c7f6d-126">To be published</span></span>|  
|<span data-ttu-id="c7f6d-127">WS-SecurityPolicy 1,1</span><span class="sxs-lookup"><span data-stu-id="c7f6d-127">WS-SecurityPolicy 1.1</span></span><br /><br /> <span data-ttu-id="c7f6d-128">(2005/07)</span><span class="sxs-lookup"><span data-stu-id="c7f6d-128">(2005/07)</span></span>|<http://specs.xmlsoap.org/ws/2005/07/securitypolicy/ws-securitypolicy.pdf><br /><br /> <span data-ttu-id="c7f6d-129">zmieniony przez [Errata](https://lists.oasis-open.org/archives/ws-sx/200512/msg00017.html) przesłany do usługi języka Oasis WS-SX Technical Komitetem</span><span class="sxs-lookup"><span data-stu-id="c7f6d-129">as amended by [errata](https://lists.oasis-open.org/archives/ws-sx/200512/msg00017.html) submitted to OASIS WS-SX Technical Committee</span></span> |  
  
 <span data-ttu-id="c7f6d-130">Program WCF, wersja 1, zapewnia 17 trybów uwierzytelniania, które mogą być używane jako podstawa konfiguracji zabezpieczeń usług sieci Web.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-130">WCF, version 1, provides 17 authentication modes that can be used as the basis for Web services security configuration.</span></span> <span data-ttu-id="c7f6d-131">Każdy tryb jest zoptymalizowany pod kątem wspólnego zestawu wymagań dotyczących wdrażania, takich jak:</span><span class="sxs-lookup"><span data-stu-id="c7f6d-131">Each mode is optimized for a common set of deployment requirements, such as:</span></span>  
  
- <span data-ttu-id="c7f6d-132">Poświadczenia używane do uwierzytelniania klientów i usług.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-132">Credentials used to authenticate client and service.</span></span>  
  
- <span data-ttu-id="c7f6d-133">Mechanizmy ochrony komunikatów lub transportu.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-133">Message or transport security protection mechanisms.</span></span>  
  
- <span data-ttu-id="c7f6d-134">Wzorce wymiany komunikatów.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-134">Message exchange patterns.</span></span>  
  
|<span data-ttu-id="c7f6d-135">Tryb uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="c7f6d-135">Authentication Mode</span></span>|<span data-ttu-id="c7f6d-136">Uwierzytelnianie klienta</span><span class="sxs-lookup"><span data-stu-id="c7f6d-136">Client Authentication</span></span>|<span data-ttu-id="c7f6d-137">Uwierzytelnianie serwera</span><span class="sxs-lookup"><span data-stu-id="c7f6d-137">Server Authentication</span></span>|<span data-ttu-id="c7f6d-138">Tryb</span><span class="sxs-lookup"><span data-stu-id="c7f6d-138">Mode</span></span>|  
|-------------------------|---------------------------|---------------------------|----------|  
|<span data-ttu-id="c7f6d-139">UserNameOverTransport</span><span class="sxs-lookup"><span data-stu-id="c7f6d-139">UserNameOverTransport</span></span>|<span data-ttu-id="c7f6d-140">Nazwa użytkownika/hasło</span><span class="sxs-lookup"><span data-stu-id="c7f6d-140">User name/password</span></span>|<span data-ttu-id="c7f6d-141">X509</span><span class="sxs-lookup"><span data-stu-id="c7f6d-141">X509</span></span>|<span data-ttu-id="c7f6d-142">Transport</span><span class="sxs-lookup"><span data-stu-id="c7f6d-142">Transport</span></span>|  
|<span data-ttu-id="c7f6d-143">CertificateOverTransport</span><span class="sxs-lookup"><span data-stu-id="c7f6d-143">CertificateOverTransport</span></span>|<span data-ttu-id="c7f6d-144">X509</span><span class="sxs-lookup"><span data-stu-id="c7f6d-144">X509</span></span>|<span data-ttu-id="c7f6d-145">X509</span><span class="sxs-lookup"><span data-stu-id="c7f6d-145">X509</span></span>|<span data-ttu-id="c7f6d-146">Transport</span><span class="sxs-lookup"><span data-stu-id="c7f6d-146">Transport</span></span>|  
|<span data-ttu-id="c7f6d-147">KerberosOverTransport</span><span class="sxs-lookup"><span data-stu-id="c7f6d-147">KerberosOverTransport</span></span>|<span data-ttu-id="c7f6d-148">Windows</span><span class="sxs-lookup"><span data-stu-id="c7f6d-148">Windows</span></span>|<span data-ttu-id="c7f6d-149">X509</span><span class="sxs-lookup"><span data-stu-id="c7f6d-149">X509</span></span>|<span data-ttu-id="c7f6d-150">Transport</span><span class="sxs-lookup"><span data-stu-id="c7f6d-150">Transport</span></span>|  
|<span data-ttu-id="c7f6d-151">IssuedTokenOverTransport</span><span class="sxs-lookup"><span data-stu-id="c7f6d-151">IssuedTokenOverTransport</span></span>|<span data-ttu-id="c7f6d-152">Federacyjni</span><span class="sxs-lookup"><span data-stu-id="c7f6d-152">Federated</span></span>|<span data-ttu-id="c7f6d-153">X509</span><span class="sxs-lookup"><span data-stu-id="c7f6d-153">X509</span></span>|<span data-ttu-id="c7f6d-154">Transport</span><span class="sxs-lookup"><span data-stu-id="c7f6d-154">Transport</span></span>|  
|<span data-ttu-id="c7f6d-155">SspiNegotiatedOverTransport</span><span class="sxs-lookup"><span data-stu-id="c7f6d-155">SspiNegotiatedOverTransport</span></span>|<span data-ttu-id="c7f6d-156">Windows SSPI negocjowane</span><span class="sxs-lookup"><span data-stu-id="c7f6d-156">Windows Sspi Negotiated</span></span>|<span data-ttu-id="c7f6d-157">Windows SSPI negocjowane</span><span class="sxs-lookup"><span data-stu-id="c7f6d-157">Windows Sspi Negotiated</span></span>|<span data-ttu-id="c7f6d-158">Transport</span><span class="sxs-lookup"><span data-stu-id="c7f6d-158">Transport</span></span>|  
|<span data-ttu-id="c7f6d-159">AnonymousForCertificate</span><span class="sxs-lookup"><span data-stu-id="c7f6d-159">AnonymousForCertificate</span></span>|<span data-ttu-id="c7f6d-160">Brak</span><span class="sxs-lookup"><span data-stu-id="c7f6d-160">None</span></span>|<span data-ttu-id="c7f6d-161">X509</span><span class="sxs-lookup"><span data-stu-id="c7f6d-161">X509</span></span>|<span data-ttu-id="c7f6d-162">Wiadomość</span><span class="sxs-lookup"><span data-stu-id="c7f6d-162">Message</span></span>|  
|<span data-ttu-id="c7f6d-163">UserNameForCertificate</span><span class="sxs-lookup"><span data-stu-id="c7f6d-163">UserNameForCertificate</span></span>|<span data-ttu-id="c7f6d-164">Nazwa użytkownika/hasło</span><span class="sxs-lookup"><span data-stu-id="c7f6d-164">User name/password</span></span>|<span data-ttu-id="c7f6d-165">X509</span><span class="sxs-lookup"><span data-stu-id="c7f6d-165">X509</span></span>|<span data-ttu-id="c7f6d-166">Wiadomość</span><span class="sxs-lookup"><span data-stu-id="c7f6d-166">Message</span></span>|  
|<span data-ttu-id="c7f6d-167">MutualCertificate</span><span class="sxs-lookup"><span data-stu-id="c7f6d-167">MutualCertificate</span></span>|<span data-ttu-id="c7f6d-168">X509</span><span class="sxs-lookup"><span data-stu-id="c7f6d-168">X509</span></span>|<span data-ttu-id="c7f6d-169">X509</span><span class="sxs-lookup"><span data-stu-id="c7f6d-169">X509</span></span>|<span data-ttu-id="c7f6d-170">Wiadomość</span><span class="sxs-lookup"><span data-stu-id="c7f6d-170">Message</span></span>|  
|<span data-ttu-id="c7f6d-171">MutualCertificateDuplex</span><span class="sxs-lookup"><span data-stu-id="c7f6d-171">MutualCertificateDuplex</span></span>|<span data-ttu-id="c7f6d-172">X509</span><span class="sxs-lookup"><span data-stu-id="c7f6d-172">X509</span></span>|<span data-ttu-id="c7f6d-173">X509</span><span class="sxs-lookup"><span data-stu-id="c7f6d-173">X509</span></span>|<span data-ttu-id="c7f6d-174">Wiadomość</span><span class="sxs-lookup"><span data-stu-id="c7f6d-174">Message</span></span>|  
|<span data-ttu-id="c7f6d-175">IssuedTokenForCertificate</span><span class="sxs-lookup"><span data-stu-id="c7f6d-175">IssuedTokenForCertificate</span></span>|<span data-ttu-id="c7f6d-176">Federacyjni</span><span class="sxs-lookup"><span data-stu-id="c7f6d-176">Federated</span></span>|<span data-ttu-id="c7f6d-177">X509</span><span class="sxs-lookup"><span data-stu-id="c7f6d-177">X509</span></span>|<span data-ttu-id="c7f6d-178">Wiadomość</span><span class="sxs-lookup"><span data-stu-id="c7f6d-178">Message</span></span>|  
|<span data-ttu-id="c7f6d-179">Kerberos</span><span class="sxs-lookup"><span data-stu-id="c7f6d-179">Kerberos</span></span>|<span data-ttu-id="c7f6d-180">Windows</span><span class="sxs-lookup"><span data-stu-id="c7f6d-180">Windows</span></span>|<span data-ttu-id="c7f6d-181">Windows</span><span class="sxs-lookup"><span data-stu-id="c7f6d-181">Windows</span></span>|<span data-ttu-id="c7f6d-182">Wiadomość</span><span class="sxs-lookup"><span data-stu-id="c7f6d-182">Message</span></span>|  
|<span data-ttu-id="c7f6d-183">IssuedToken</span><span class="sxs-lookup"><span data-stu-id="c7f6d-183">IssuedToken</span></span>|<span data-ttu-id="c7f6d-184">Federacyjni</span><span class="sxs-lookup"><span data-stu-id="c7f6d-184">Federated</span></span>|<span data-ttu-id="c7f6d-185">Federacyjni</span><span class="sxs-lookup"><span data-stu-id="c7f6d-185">Federated</span></span>|<span data-ttu-id="c7f6d-186">Wiadomość</span><span class="sxs-lookup"><span data-stu-id="c7f6d-186">Message</span></span>|  
|<span data-ttu-id="c7f6d-187">SspiNegotiated</span><span class="sxs-lookup"><span data-stu-id="c7f6d-187">SspiNegotiated</span></span>|<span data-ttu-id="c7f6d-188">Windows SSPI negocjowane</span><span class="sxs-lookup"><span data-stu-id="c7f6d-188">Windows Sspi Negotiated</span></span>|<span data-ttu-id="c7f6d-189">Windows SSPI negocjowane</span><span class="sxs-lookup"><span data-stu-id="c7f6d-189">Windows Sspi Negotiated</span></span>|<span data-ttu-id="c7f6d-190">Wiadomość</span><span class="sxs-lookup"><span data-stu-id="c7f6d-190">Message</span></span>|  
|<span data-ttu-id="c7f6d-191">AnonymousForSslNegotiated</span><span class="sxs-lookup"><span data-stu-id="c7f6d-191">AnonymousForSslNegotiated</span></span>|<span data-ttu-id="c7f6d-192">Brak</span><span class="sxs-lookup"><span data-stu-id="c7f6d-192">None</span></span>|<span data-ttu-id="c7f6d-193">X509, TLS-nego</span><span class="sxs-lookup"><span data-stu-id="c7f6d-193">X509, TLS-Nego</span></span>|<span data-ttu-id="c7f6d-194">Wiadomość</span><span class="sxs-lookup"><span data-stu-id="c7f6d-194">Message</span></span>|  
|<span data-ttu-id="c7f6d-195">UserNameForSslNegotiated</span><span class="sxs-lookup"><span data-stu-id="c7f6d-195">UserNameForSslNegotiated</span></span>|<span data-ttu-id="c7f6d-196">Nazwa użytkownika/hasło</span><span class="sxs-lookup"><span data-stu-id="c7f6d-196">User name/password</span></span>|<span data-ttu-id="c7f6d-197">X509, TLS-nego</span><span class="sxs-lookup"><span data-stu-id="c7f6d-197">X509, TLS-Nego</span></span>|<span data-ttu-id="c7f6d-198">Wiadomość</span><span class="sxs-lookup"><span data-stu-id="c7f6d-198">Message</span></span>|  
|<span data-ttu-id="c7f6d-199">MutualSslNegotiated</span><span class="sxs-lookup"><span data-stu-id="c7f6d-199">MutualSslNegotiated</span></span>|<span data-ttu-id="c7f6d-200">X509</span><span class="sxs-lookup"><span data-stu-id="c7f6d-200">X509</span></span>|<span data-ttu-id="c7f6d-201">X509, TLS-nego</span><span class="sxs-lookup"><span data-stu-id="c7f6d-201">X509, TLS-Nego</span></span>|<span data-ttu-id="c7f6d-202">Wiadomość</span><span class="sxs-lookup"><span data-stu-id="c7f6d-202">Message</span></span>|  
|<span data-ttu-id="c7f6d-203">IssuedTokenForSslNegotiated</span><span class="sxs-lookup"><span data-stu-id="c7f6d-203">IssuedTokenForSslNegotiated</span></span>|<span data-ttu-id="c7f6d-204">Federacyjni</span><span class="sxs-lookup"><span data-stu-id="c7f6d-204">Federated</span></span>|<span data-ttu-id="c7f6d-205">X509, TLS-nego</span><span class="sxs-lookup"><span data-stu-id="c7f6d-205">X509, TLS-Nego</span></span>|<span data-ttu-id="c7f6d-206">Wiadomość</span><span class="sxs-lookup"><span data-stu-id="c7f6d-206">Message</span></span>|  
  
 <span data-ttu-id="c7f6d-207">Punkty końcowe korzystające z takich trybów uwierzytelniania mogą wyrażać wymagania dotyczące zabezpieczeń przy użyciu protokołu WS-SecurityPolicy (WS-SP).</span><span class="sxs-lookup"><span data-stu-id="c7f6d-207">Endpoints using such authentication modes can express their security requirements using WS-SecurityPolicy (WS-SP).</span></span> <span data-ttu-id="c7f6d-208">W tym dokumencie opisano strukturę nagłówka zabezpieczeń i komunikatów infrastruktury dla każdego trybu uwierzytelniania oraz przedstawiono przykłady zasad i komunikatów.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-208">This document describes the structure of security header and infrastructure messages for each authentication mode and provides examples of policies and messages.</span></span>  
  
 <span data-ttu-id="c7f6d-209">Funkcja WCF korzysta z protokołu WS-SecureConversation, aby zapewnić obsługę bezpiecznych sesji w celu ochrony wymiany wielokomunikatowej między aplikacjami.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-209">WCF leverages WS-SecureConversation to provide secure sessions support to protect multi-message exchanges between applications.</span></span>  <span data-ttu-id="c7f6d-210">Aby uzyskać szczegółowe informacje dotyczące implementacji, zobacz sekcję "bezpieczne sesje".</span><span class="sxs-lookup"><span data-stu-id="c7f6d-210">See "Secure Sessions" below for implementation details.</span></span>  
  
 <span data-ttu-id="c7f6d-211">Oprócz trybów uwierzytelniania program WCF udostępnia ustawienia do kontrolowania typowych mechanizmów ochrony, które mają zastosowanie do większości trybów uwierzytelniania opartych na zabezpieczeniach komunikatów, na przykład: kolejność podpisu i operacje szyfrowania, zestawy algorytmów, wyprowadzanie kluczy i potwierdzenie podpisu.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-211">In addition to authentication modes, WCF provides settings to control common protection mechanisms that apply to most message security-based authentication modes, for example: order of signature versus encryption operations, algorithm suites, key derivation, and signature confirmation.</span></span>  
  
 <span data-ttu-id="c7f6d-212">W tym dokumencie są używane następujące prefiksy i przestrzenie nazw.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-212">The following prefixes and namespaces are used in this document.</span></span>  
  
|<span data-ttu-id="c7f6d-213">Prefiks</span><span class="sxs-lookup"><span data-stu-id="c7f6d-213">Prefix</span></span>|<span data-ttu-id="c7f6d-214">Przestrzeń nazw</span><span class="sxs-lookup"><span data-stu-id="c7f6d-214">Namespace</span></span>|  
|------------|---------------|  
|<span data-ttu-id="c7f6d-215">s</span><span class="sxs-lookup"><span data-stu-id="c7f6d-215">s</span></span>|<http://www.w3.org/2003/05/soap-envelope/>|
|<span data-ttu-id="c7f6d-216">sp</span><span class="sxs-lookup"><span data-stu-id="c7f6d-216">sp</span></span>|<http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/>|
|<span data-ttu-id="c7f6d-217">a</span><span class="sxs-lookup"><span data-stu-id="c7f6d-217">a</span></span>|<http://www.w3.org/2005/08/addressing>|  
|<span data-ttu-id="c7f6d-218">wsse</span><span class="sxs-lookup"><span data-stu-id="c7f6d-218">wsse</span></span>|<span data-ttu-id="c7f6d-219">TBD — JĘZYKA OASIS Z IDENTYFIKATOREM URI PROGRAMU WSS 1,0</span><span class="sxs-lookup"><span data-stu-id="c7f6d-219">TBD – OASIS WSS 1.0 URI</span></span>|  
|<span data-ttu-id="c7f6d-220">wsse11</span><span class="sxs-lookup"><span data-stu-id="c7f6d-220">wsse11</span></span>|<span data-ttu-id="c7f6d-221">TBD — JĘZYKA OASIS Z IDENTYFIKATOREM URI PROGRAMU WSS 1,1</span><span class="sxs-lookup"><span data-stu-id="c7f6d-221">TBD – OASIS WSS 1.1 URI</span></span>|  
|<span data-ttu-id="c7f6d-222">wsu</span><span class="sxs-lookup"><span data-stu-id="c7f6d-222">wsu</span></span>|<span data-ttu-id="c7f6d-223">TBD — identyfikator URI narzędzia języka Oasis WSS 1,0</span><span class="sxs-lookup"><span data-stu-id="c7f6d-223">TBD – OASIS WSS 1.0 Utility URI</span></span>|  
|<span data-ttu-id="c7f6d-224">ds</span><span class="sxs-lookup"><span data-stu-id="c7f6d-224">ds</span></span>|<span data-ttu-id="c7f6d-225">TBD — identyfikator URI XMLDSig W3C</span><span class="sxs-lookup"><span data-stu-id="c7f6d-225">TBD – W3C XMLDSig URI</span></span>|  
|<span data-ttu-id="c7f6d-226">wst</span><span class="sxs-lookup"><span data-stu-id="c7f6d-226">wst</span></span>|<span data-ttu-id="c7f6d-227">TBD — identyfikator URI 2005/02 WS-Trust</span><span class="sxs-lookup"><span data-stu-id="c7f6d-227">TBD – WS-Trust 2005/02 URI</span></span>|  
|<span data-ttu-id="c7f6d-228">wssc</span><span class="sxs-lookup"><span data-stu-id="c7f6d-228">wssc</span></span>|<span data-ttu-id="c7f6d-229">TBD — identyfikator URI WS-SecureConversation 2005/02</span><span class="sxs-lookup"><span data-stu-id="c7f6d-229">TBD – WS-SecureConversation 2005/02 URI</span></span>|  
|<span data-ttu-id="c7f6d-230">wsaw</span><span class="sxs-lookup"><span data-stu-id="c7f6d-230">wsaw</span></span>|<span data-ttu-id="c7f6d-231">TBD — przestrzeń nazw zasad adresowania WS</span><span class="sxs-lookup"><span data-stu-id="c7f6d-231">TBD - WS-Addressing policy namespace</span></span>|  
|<span data-ttu-id="c7f6d-232">wsp</span><span class="sxs-lookup"><span data-stu-id="c7f6d-232">wsp</span></span>|<http://schemas.xmlsoap.org/ws/2004/09/policy>|  
|<span data-ttu-id="c7f6d-233">mssp</span><span class="sxs-lookup"><span data-stu-id="c7f6d-233">mssp</span></span>|<http://schemas.xmlsoap.org/ws/2005/07/securitypolicy>|
  
## <a name="1-token-profiles"></a><span data-ttu-id="c7f6d-234">1. profile tokenów</span><span class="sxs-lookup"><span data-stu-id="c7f6d-234">1. Token Profiles</span></span>  
 <span data-ttu-id="c7f6d-235">Specyfikacja zabezpieczenia usług w sieci Web reprezentuje poświadczenie jako tokeny zabezpieczające.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-235">Web Services Security specifications represent credential as security tokens.</span></span> <span data-ttu-id="c7f6d-236">Usługa WCF obsługuje następujące typy tokenów:</span><span class="sxs-lookup"><span data-stu-id="c7f6d-236">WCF supports the following token types:</span></span>  
  
### <a name="11-usernametoken"></a><span data-ttu-id="c7f6d-237">1,1 UsernameToken</span><span class="sxs-lookup"><span data-stu-id="c7f6d-237">1.1 UsernameToken</span></span>  
 <span data-ttu-id="c7f6d-238">Program WCF jest zgodny z profilami UsernameToken10 i UsernameToken11 z następującymi ograniczeniami:</span><span class="sxs-lookup"><span data-stu-id="c7f6d-238">WCF follows UsernameToken10 and UsernameToken11 profiles with the following constraints:</span></span>  
  
 <span data-ttu-id="c7f6d-239">Atrybut R1101 Passwordtype elementu UsernameToken\Password musi być pominięty lub mieć wartość #PasswordText (domyślnie).</span><span class="sxs-lookup"><span data-stu-id="c7f6d-239">R1101 PasswordType attribute on UsernameToken\Password element MUST be either omitted or have value #PasswordText (default).</span></span>  
  
 <span data-ttu-id="c7f6d-240">Jeden może zaimplementować #PasswordDigest przy użyciu rozszerzalności.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-240">One can implement the #PasswordDigest using extensibility.</span></span> <span data-ttu-id="c7f6d-241">Zauważono, że #PasswordDigest był często omyłkowo uznawany za bezpieczny mechanizm ochrony hasłem.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-241">It has been observed that #PasswordDigest was often mistaken to be a secure enough password protection mechanism.</span></span> <span data-ttu-id="c7f6d-242">Ale #PasswordDigest nie może stanowić zamiennika szyfrowania UsernameToken.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-242">But #PasswordDigest cannot serve as a substitute for encryption of the UsernameToken.</span></span> <span data-ttu-id="c7f6d-243">Głównym celem #PasswordDigest jest ochrona przed atakami metodą powtórzeń.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-243">The primary goal of #PasswordDigest is protection against replay attacks.</span></span> <span data-ttu-id="c7f6d-244">W przypadku trybów uwierzytelniania WCF złośliwe ataki są rozwiązywane za pomocą sygnatur komunikatów.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-244">In WCF authentication modes, replay attack threats are mitigated by using message signatures.</span></span>  
  
 <span data-ttu-id="c7f6d-245">B1102 WCF nigdy nie emituje identyfikatora wiersza i utworzonych elementów podrzędnych UsernameToken.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-245">B1102 WCF never emits Nonce and Created sub-elements of the UsernameToken.</span></span>  
  
 <span data-ttu-id="c7f6d-246">Te elementy podrzędne mają na celu ułatwienie wykrywania powtarzania.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-246">These sub-elements are intended to help replay detection.</span></span> <span data-ttu-id="c7f6d-247">Usługa WCF używa zamiast tego sygnatury komunikatów.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-247">WCF uses message signatures instead.</span></span>  
  
 <span data-ttu-id="c7f6d-248">JĘZYKA Oasis WSS Message Security UsernameToken profil 1,1 (UsernameToken11) wprowadził klucz wyprowadzania z funkcji password.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-248">OASIS WSS SOAP Message Security UsernameToken Profile 1.1 (UsernameToken11) introduced key derivation from password feature.</span></span>  
  
 <span data-ttu-id="c7f6d-249">Hasła B1103 UsernameToken nie można używać do wyprowadzania klucza i w związku z tym dla operacji kryptograficznych.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-249">B1103 UsernameToken password MUST not be used for key derivation and therefore for cryptographic operations.</span></span>  
  
 <span data-ttu-id="c7f6d-250">Uzasadnienie: hasła są zwykle uznawane za słabe, aby można było używać ich na potrzeby operacji kryptograficznych.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-250">Rationale: passwords are generally considered too weak to be used for cryptographic operations.</span></span>  
  
### <a name="12-x509-token"></a><span data-ttu-id="c7f6d-251">Token x509 1,2</span><span class="sxs-lookup"><span data-stu-id="c7f6d-251">1.2 X509 Token</span></span>  
 <span data-ttu-id="c7f6d-252">Usługa WCF obsługuje certyfikaty X509v3 jako typ poświadczenia i następuje po X509TokenProfile 1.0 i X509TokenProfile 1.1 z następującymi ograniczeniami:</span><span class="sxs-lookup"><span data-stu-id="c7f6d-252">WCF supports X509v3 certificates as a credential type and follows X509TokenProfile1.0 and X509TokenProfile1.1 with the following constraints:</span></span>  
  
 <span data-ttu-id="c7f6d-253">R1201 atrybut ValueType w elemencie BinarySecurityToken musi mieć wartość #X509v3, gdy zawiera certyfikat X509v3.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-253">R1201 The ValueType attribute on the BinarySecurityToken element must have value #X509v3 when it contains an X509v3 certificate.</span></span>  
  
 <span data-ttu-id="c7f6d-254">Profil tokenu x509 usług WSS 1,0 i 1,1 definiuje również #X509PKIPathv1 i #PKCS7 jako typy wartości.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-254">WSS X509 Token Profile 1.0 and 1.1 define also #X509PKIPathv1 and #PKCS7 as value types.</span></span> <span data-ttu-id="c7f6d-255">Program WCF nie obsługuje tych typów.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-255">WCF does not support these types.</span></span>  
  
 <span data-ttu-id="c7f6d-256">R1202 Jeśli w certyfikacie x509 znajduje się rozszerzenie SubjectKeyIdentifier (SKI), wsse: Identyfikator klucza powinien być używany do odwołań zewnętrznych do tokenu, z atrybutem ValueType jako #X509SubjectKeyIdentifier i jego zawartością jest zakodowana w formacie base64 wartość rozszerzenia SKI certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-256">R1202 If a SubjectKeyIdentifier (SKI) extension is present in an X509 certificate, wsse:KeyIdentifier should be used for external references to the token, with the ValueType attribute as #X509SubjectKeyIdentifier and its content the base64-encoded value of certificate's SKI extension.</span></span>  
  
 <span data-ttu-id="c7f6d-257">Odwołania NARCIARSKIe są szeroko implementowane i sprawdzane jako typ odwołania zewnętrznego o wysokiej interoperacyjności.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-257">SKI references are widely implemented and proven to be a highly interoperable external reference type.</span></span>  
  
 <span data-ttu-id="c7f6d-258">R1203 odwołanie zewnętrzne do tokenu zabezpieczającego x509 nie powinno korzystać z usług DS: X509IssuerSerial.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-258">R1203 An external Reference to X509 Security Token SHOULD NOT use ds:X509IssuerSerial.</span></span>  
  
 <span data-ttu-id="c7f6d-259">R1204 Jeśli X509TokenProfile 1.1 jest używany, odwołanie zewnętrzne do tokenu zabezpieczającego x509 powinno używać odcisku palca wprowadzonego przez usługę WS-Security 1,1.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-259">R1204 If X509TokenProfile1.1 is in use, an external reference to X509 Security Token SHOULD use the thumbprint introduced by WS-Security 1.1.</span></span>  
  
 <span data-ttu-id="c7f6d-260">Usługa WCF obsługuje X509IssuerSerial.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-260">WCF supports X509IssuerSerial.</span></span> <span data-ttu-id="c7f6d-261">Występują jednak problemy ze współdziałaniem z X509IssuerSerial: WCF używa ciągu do porównywania dwóch wartości X509IssuerSerial.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-261">However There are interoperability issues with X509IssuerSerial: WCF uses a string to compare two values of X509IssuerSerial.</span></span> <span data-ttu-id="c7f6d-262">W związku z tym jeśli jedna zmiana kolejności składników nazwy podmiotu jest wysyłana do usługi WCF odwołanie do certyfikatu, może nie zostać znaleziona.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-262">Therefore if one reorders components of the Subject Name and sends to an WCF service a reference to a certificate, it may not be found.</span></span>  
  
### <a name="13-kerberos-token"></a><span data-ttu-id="c7f6d-263">1,3 token Kerberos</span><span class="sxs-lookup"><span data-stu-id="c7f6d-263">1.3 Kerberos Token</span></span>  
 <span data-ttu-id="c7f6d-264">Usługa WCF obsługuje KerberosTokenProfile 1.1 na potrzeby uwierzytelniania systemu Windows z następującymi ograniczeniami:</span><span class="sxs-lookup"><span data-stu-id="c7f6d-264">WCF supports KerberosTokenProfile1.1 for the purpose of Windows authentication with the following constraints:</span></span>  
  
 <span data-ttu-id="c7f6d-265">R1301 token Kerberos musi mieć wartość opakowanego protokołu Kerberos v4 AP_REQ zgodnie z definicją w GSS_API i specyfikacją protokołu Kerberos i musi mieć atrybut ValueType o wartości #GSS_Kerberosv5_AP_REQ.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-265">R1301 A Kerberos Token must carry the value of a GSS wrapped Kerberos v4 AP_REQ as defined in GSS_API and the Kerberos specification, and must have the ValueType attribute with the value #GSS_Kerberosv5_AP_REQ.</span></span>  
  
 <span data-ttu-id="c7f6d-266">Funkcja WCF używa opakowanego protokołu Kerberos w języku GSS-REQ, a nie od zera-REQ.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-266">WCF uses GSS wrapped Kerberos AP-REQ, not a bare AP-REQ.</span></span> <span data-ttu-id="c7f6d-267">Jest to najlepsze rozwiązanie w zakresie zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-267">This is a security best practice.</span></span>  
  
### <a name="14-saml-v11-token"></a><span data-ttu-id="c7f6d-268">1,4 token SAML v 1.1</span><span class="sxs-lookup"><span data-stu-id="c7f6d-268">1.4 SAML v1.1 Token</span></span>  
 <span data-ttu-id="c7f6d-269">Usługa WCF obsługuje profile tokenów SAML programu WSS 1,0 i 1,1 dla tokenów SAML w wersji 1.1.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-269">WCF supports WSS SAML Token profiles 1.0 and 1.1 for SAML v1.1 tokens.</span></span> <span data-ttu-id="c7f6d-270">Istnieje możliwość zaimplementowania innych wersji formatów tokenów języka SAML.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-270">It is possible to implement other versions of SAML token formats.</span></span>  
  
### <a name="15-security-context-token"></a><span data-ttu-id="c7f6d-271">1,5 token kontekstu zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="c7f6d-271">1.5 Security Context Token</span></span>  
 <span data-ttu-id="c7f6d-272">WCF obsługuje token kontekstu zabezpieczeń (SCT) wprowadzony w usłudze WS-SecureConversation.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-272">WCF supports the Security Context Token (SCT) introduced in WS-SecureConversation.</span></span> <span data-ttu-id="c7f6d-273">SCT służy do reprezentowania kontekstu zabezpieczeń ustanowionego w SecureConversation, a także do protokołów negocjacji binarnych TLS i SSPI, opisanych poniżej.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-273">SCT is used to represent a security context established in SecureConversation as well as the binary negotiation protocols TLS and SSPI, described below.</span></span>  
  
## <a name="2-common-message-security-parameters"></a><span data-ttu-id="c7f6d-274">2. typowe parametry zabezpieczeń komunikatów</span><span class="sxs-lookup"><span data-stu-id="c7f6d-274">2. Common Message Security Parameters</span></span>  
  
### <a name="21-timestamp"></a><span data-ttu-id="c7f6d-275">Sygnatura czasowa 2,1</span><span class="sxs-lookup"><span data-stu-id="c7f6d-275">2.1 TimeStamp</span></span>  
 <span data-ttu-id="c7f6d-276">Obecność sygnatury czasowej jest kontrolowana przy użyciu <xref:System.ServiceModel.Channels.SecurityBindingElement.IncludeTimestamp%2A> właściwości <xref:System.ServiceModel.Channels.SecurityBindingElement> klasy.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-276">Timestamp presence is controlled using the <xref:System.ServiceModel.Channels.SecurityBindingElement.IncludeTimestamp%2A> property of the <xref:System.ServiceModel.Channels.SecurityBindingElement> class.</span></span> <span data-ttu-id="c7f6d-277">Funkcja WCF zawsze serializować wsse: TimeStamp z polami wsse: Created i wsse: Expires.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-277">WCF always serializes wsse:TimeStamp with wsse:Created and wsse:Expires fields.</span></span> <span data-ttu-id="c7f6d-278">Wsse: sygnatura czasowa jest zawsze podpisywana przy użyciu podpisywania.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-278">The wsse:TimeStamp is always signed when signing is used.</span></span>  
  
### <a name="22-protection-order"></a><span data-ttu-id="c7f6d-279">2,2 kolejność ochrony</span><span class="sxs-lookup"><span data-stu-id="c7f6d-279">2.2 Protection Order</span></span>  
 <span data-ttu-id="c7f6d-280">Usługa WCF obsługuje kolejność ochrony wiadomości przed szyfrowaniem i szyfrowanie przed znakiem (zasady zabezpieczeń 1,1).</span><span class="sxs-lookup"><span data-stu-id="c7f6d-280">WCF supports the message protection order "Sign Before Encrypt" and "Encrypt Before Sign" (Security Policy 1.1).</span></span> <span data-ttu-id="c7f6d-281">Zalecane jest "podpisywanie przed szyfrowaniem", w tym: komunikaty chronione przy użyciu szyfrowania przed podpisaniem podpisu, chyba że jest używany mechanizm WS-Security 1,1 SignatureConfirmation, a sygnatura z zaszyfrowaną zawartością sprawia, że inspekcja jest trudniejsza.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-281">"Sign Before Encrypt" is recommended for reasons including: messages protected with Encrypt Before Sign are open to signature substitution attacks unless the WS-Security 1.1 SignatureConfirmation mechanism is used, and a signature over encrypted content makes auditing harder.</span></span>  
  
### <a name="23-signature-protection"></a><span data-ttu-id="c7f6d-282">Ochrona za sygnaturą 2,3</span><span class="sxs-lookup"><span data-stu-id="c7f6d-282">2.3 Signature Protection</span></span>  
 <span data-ttu-id="c7f6d-283">Gdy jest używane szyfrowanie przed znakiem, zaleca się ochronę podpisu, aby zapobiec atakom typu "nadjęcie" na potrzeby odgadnięcia zaszyfrowanej zawartości lub klucza podpisywania (zwłaszcza gdy Token niestandardowy jest używany z słabym materiałem klucza).</span><span class="sxs-lookup"><span data-stu-id="c7f6d-283">When Encrypt Before Sign is used, it is recommended to protect the signature to prevent brute force attacks for guessing the encrypted content or the signing key (especially when a custom token is used with weak key material).</span></span>  
  
### <a name="24-algorithm-suite"></a><span data-ttu-id="c7f6d-284">Pakiet algorytmów 2,4</span><span class="sxs-lookup"><span data-stu-id="c7f6d-284">2.4 Algorithm Suite</span></span>  
 <span data-ttu-id="c7f6d-285">Usługa WCF obsługuje wszystkie pakiety algorytmów wymienione w zasadach zabezpieczeń 1,1.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-285">WCF supports all algorithm suites listed in Security Policy 1.1.</span></span>  
  
### <a name="25-key-derivation"></a><span data-ttu-id="c7f6d-286">Tworzenie klucza 2,5</span><span class="sxs-lookup"><span data-stu-id="c7f6d-286">2.5 Key Derivation</span></span>  
 <span data-ttu-id="c7f6d-287">WCF używa "wyprowadzania klucza dla kluczy symetrycznych" zgodnie z opisem w temacie WS-SecureConversation.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-287">WCF uses "Key Derivation for symmetric keys" as described in WS-SecureConversation.</span></span>  
  
### <a name="26-signature-confirmation"></a><span data-ttu-id="c7f6d-288">Potwierdzenie podpisu 2,6</span><span class="sxs-lookup"><span data-stu-id="c7f6d-288">2.6 Signature Confirmation</span></span>  
 <span data-ttu-id="c7f6d-289">Potwierdzenie podpisu może być uznawane za ochronę przed atakami typu średniego firmy w celu ochrony zestawu podpisów.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-289">Signature confirmation can be as protection from middle man attacks to protect the set of signatures.</span></span>  
  
### <a name="27-security-header-layout"></a><span data-ttu-id="c7f6d-290">2,7 — układ nagłówka zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="c7f6d-290">2.7 Security Header Layout</span></span>  
 <span data-ttu-id="c7f6d-291">Każdy tryb uwierzytelniania opisuje określony układ nagłówka zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-291">Each authentication mode describes a certain layout for the security header.</span></span> <span data-ttu-id="c7f6d-292">Elementy w nagłówku zabezpieczeń są częściowo uporządkowane.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-292">Elements within the security header are semi-ordered.</span></span> <span data-ttu-id="c7f6d-293">Aby zdefiniować kolejność elementów podrzędnych nagłówka zabezpieczeń, zasady WS-Security definiują następujące tryby układu nagłówka zabezpieczeń:</span><span class="sxs-lookup"><span data-stu-id="c7f6d-293">To define the order of security header child elements, WS-Security Policy defines the following security header layout modes:</span></span>  
  
|||  
|-|-|  
|<span data-ttu-id="c7f6d-294">Dokładny</span><span class="sxs-lookup"><span data-stu-id="c7f6d-294">Strict</span></span>|<span data-ttu-id="c7f6d-295">Elementy są dodawane do nagłówka Security, zgodnie z regułami układu numerowanego opisanymi w sekcji zasady zabezpieczeń 7.7.1 zgodnie z ogólną zasadą "DECLARE przed użyciem".</span><span class="sxs-lookup"><span data-stu-id="c7f6d-295">Items are added to the security header following the numbered layout rules described in Security Policy section 7.7.1 according to a general principle of "declare before use".</span></span>|  
|<span data-ttu-id="c7f6d-296">Swobodny</span><span class="sxs-lookup"><span data-stu-id="c7f6d-296">Lax</span></span>|<span data-ttu-id="c7f6d-297">Elementy są dodawane do nagłówka zabezpieczenia w dowolnej kolejności, która jest zgodna z programem WSS: zabezpieczenia komunikatów protokołu SOAP.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-297">Items are added to the security header in any order that conforms to WSS: SOAP Message Security.</span></span>|  
|<span data-ttu-id="c7f6d-298">LaxTimestampFirst</span><span class="sxs-lookup"><span data-stu-id="c7f6d-298">LaxTimestampFirst</span></span>|<span data-ttu-id="c7f6d-299">Analogicznie jak swobodny, z tą różnicą, że pierwszy element w nagłówku zabezpieczeń musi być wsse: timestamp</span><span class="sxs-lookup"><span data-stu-id="c7f6d-299">Same as Lax except that the first item in the security header must be a wsse:Timestamp</span></span>|  
|<span data-ttu-id="c7f6d-300">LaxTimestampLast</span><span class="sxs-lookup"><span data-stu-id="c7f6d-300">LaxTimestampLast</span></span>|<span data-ttu-id="c7f6d-301">Analogicznie jak swobodny, z tą różnicą, że ostatni element w nagłówku zabezpieczeń musi być wsse: timestamp</span><span class="sxs-lookup"><span data-stu-id="c7f6d-301">Same as lax except that the last item in the security header must be a wsse:Timestamp</span></span>|  
  
 <span data-ttu-id="c7f6d-302">Funkcja WCF obsługuje wszystkie cztery tryby układu nagłówka zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-302">WCF supports all four modes for security header layout.</span></span> <span data-ttu-id="c7f6d-303">Przykłady struktury nagłówka zabezpieczeń i komunikatów dla trybów uwierzytelniania poniżej są zgodne z trybem Strict.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-303">Security header structure and message examples for authentication modes below follow the "Strict" mode.</span></span>  
  
## <a name="2-common-message-security-parameters"></a><span data-ttu-id="c7f6d-304">2. typowe parametry zabezpieczeń komunikatów</span><span class="sxs-lookup"><span data-stu-id="c7f6d-304">2. Common Message Security Parameters</span></span>  
 <span data-ttu-id="c7f6d-305">Ta sekcja zawiera przykładowe zasady dla każdego trybu uwierzytelniania wraz z przykładami przedstawiającymi strukturę nagłówka zabezpieczeń w komunikatach wymienianych przez klienta i usługę.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-305">This section provides example policies for each authentication mode along with examples showing security header structure in messages exchanged by client and service.</span></span>  
  
### <a name="61-transport-protection"></a><span data-ttu-id="c7f6d-306">Ochrona przed transportem 6,1</span><span class="sxs-lookup"><span data-stu-id="c7f6d-306">6.1 Transport Protection</span></span>  
 <span data-ttu-id="c7f6d-307">Usługa WCF oferuje pięć trybów uwierzytelniania, które używają bezpiecznego transportu do ochrony komunikatów; UserNameOverTransport, CertificateOverTransport, KerberosOverTransport, IssuedTokenOverTransport i SspiNegotiatedOverTransport.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-307">WCF provides five authentication modes that use secure transport to protect messages; UserNameOverTransport, CertificateOverTransport, KerberosOverTransport, IssuedTokenOverTransport and SspiNegotiatedOverTransport.</span></span>  
  
 <span data-ttu-id="c7f6d-308">Te tryby uwierzytelniania są konstruowane przy użyciu powiązania transportu opisanego w SecurityPolicy.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-308">These authentication modes are constructed using the transport binding described in SecurityPolicy.</span></span> <span data-ttu-id="c7f6d-309">W przypadku trybu uwierzytelniania UserNameOverTransport UsernameToken jest podpisanym tokenem pomocniczym.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-309">For the UserNameOverTransport authentication mode the UsernameToken is a signed supporting token.</span></span> <span data-ttu-id="c7f6d-310">W przypadku innych trybów uwierzytelniania token pojawia się jako podpisany token zatwierdzania.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-310">For the other authentication modes the token appears as a signed endorsing token.</span></span> <span data-ttu-id="c7f6d-311">Dodatek C. 1.2 i C. 1.3 z SecurityPolicy opisują szczegóły układu nagłówka zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-311">Appendix C.1.2 and C.1.3 of SecurityPolicy describe the security header layout in detail.</span></span> <span data-ttu-id="c7f6d-312">Poniższe przykładowe nagłówki zabezpieczeń pokazują ścisły układ dla danego trybu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-312">The following example security headers show the Strict layout for a given authentication mode.</span></span>  
  
 <span data-ttu-id="c7f6d-313">Wartość właściwości "klucze pochodne" dla tokenów we wszystkich przypadkach wynosi "false".</span><span class="sxs-lookup"><span data-stu-id="c7f6d-313">The value of the "Derived Keys" property for the tokens in all cases is "false".</span></span>  
  
 <span data-ttu-id="c7f6d-314">Wartości różnych właściwości powiązania transportowego są następujące:</span><span class="sxs-lookup"><span data-stu-id="c7f6d-314">The values of the various properties of the transport binding are as follows:</span></span>  
  
 <span data-ttu-id="c7f6d-315">Sygnatura czasowa: prawda</span><span class="sxs-lookup"><span data-stu-id="c7f6d-315">Timestamp: true</span></span>  
  
 <span data-ttu-id="c7f6d-316">Układ nagłówka zabezpieczeń: Strict</span><span class="sxs-lookup"><span data-stu-id="c7f6d-316">Security Header Layout: Strict</span></span>  
  
 <span data-ttu-id="c7f6d-317">Pakiet algorytmów: Basic256</span><span class="sxs-lookup"><span data-stu-id="c7f6d-317">Algorithm Suite: Basic256</span></span>  
  
#### <a name="611-usernameovertransport"></a><span data-ttu-id="c7f6d-318">6.1.1 UsernameOverTransport</span><span class="sxs-lookup"><span data-stu-id="c7f6d-318">6.1.1 UsernameOverTransport</span></span>  
 <span data-ttu-id="c7f6d-319">W tym trybie uwierzytelniania klient uwierzytelnia się za pomocą tokenu nazwy użytkownika, który jest wyświetlany na warstwie protokołu SOAP jako podpisany token pomocniczy, który jest zawsze wysyłany z inicjatora do odbiorcy.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-319">With this authentication mode, the client authenticates with a Username Token which appears at the SOAP layer as a signed supporting token that is always sent from the initiator to the recipient.</span></span> <span data-ttu-id="c7f6d-320">Usługa jest uwierzytelniana przy użyciu certyfikatu X. 509 w warstwie transportowej.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-320">The service is authenticated using an X.509 certificate at the transport layer.</span></span> <span data-ttu-id="c7f6d-321">Użyte powiązanie jest powiązaniem transportu.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-321">The binding used is a transport binding.</span></span>  
  
 <span data-ttu-id="c7f6d-322">Zasady</span><span class="sxs-lookup"><span data-stu-id="c7f6d-322">Policy</span></span>  
  
```xml  
<wsp:Policy wsu:Id='UsernameOverTransport_policy' >  
  <wsp:ExactlyOne>  
    <wsp:All>  
      <sp:TransportBinding >  
        <wsp:Policy>  
          <sp:TransportToken>  
            <wsp:Policy>  
              <sp:HttpsToken RequireClientCertificate='false' />
            </wsp:Policy>  
          </sp:TransportToken>  
          <sp:AlgorithmSuite>  
            <wsp:Policy>  
              <sp:Basic256 />
            </wsp:Policy>  
          </sp:AlgorithmSuite>  
          <sp:Layout>  
            <wsp:Policy>  
              <sp:Strict />
            </wsp:Policy>  
          </sp:Layout>  
          <sp:IncludeTimestamp />
        </wsp:Policy>  
      </sp:TransportBinding>  
      <sp:SignedSupportingTokens >  
        <wsp:Policy>  
          <sp:UsernameToken
sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/AlwaysToRecipient' >  
            <wsp:Policy>  
              <sp:WssUsernameToken10 />
            </wsp:Policy>  
          </sp:UsernameToken>  
        </wsp:Policy>  
      </sp:SignedSupportingTokens>  
      <sp:Wss11 >  
        <wsp:Policy>  
          <sp:MustSupportRefKeyIdentifier />
          <sp:MustSupportRefIssuerSerial />
          <sp:MustSupportRefThumbprint />
          <sp:MustSupportRefEncryptedKey />
        </wsp:Policy>  
      </sp:Wss11>  
      <sp:Trust10 >  
        <wsp:Policy>  
          <sp:MustSupportIssuedTokens />
          <sp:RequireClientEntropy />
          <sp:RequireServerEntropy />
        </wsp:Policy>  
      </sp:Trust10>  
      <wsaw:UsingAddressing />
    </wsp:All>  
  </wsp:ExactlyOne>  
</wsp:Policy>  
```  
  
 <span data-ttu-id="c7f6d-323">Układ nagłówka zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="c7f6d-323">Security Header Layout</span></span>  
  
 <span data-ttu-id="c7f6d-324">Żądanie</span><span class="sxs-lookup"><span data-stu-id="c7f6d-324">Request</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <wsse:UsernameToken>  
  ...  
  </wsse:UsernameToken>  
</wsse:Security>  
```  
  
 <span data-ttu-id="c7f6d-325">Reakcja</span><span class="sxs-lookup"><span data-stu-id="c7f6d-325">Response</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
</wsse:Security>  
```  
  
#### <a name="612-certificateovertransport"></a><span data-ttu-id="c7f6d-326">CertificateOverTransport 6.1.2</span><span class="sxs-lookup"><span data-stu-id="c7f6d-326">6.1.2 CertificateOverTransport</span></span>  
 <span data-ttu-id="c7f6d-327">W tym trybie uwierzytelniania klient jest uwierzytelniany przy użyciu certyfikatu X. 509, który jest wyświetlany w warstwie protokołu SOAP jako zatwierdzenie tokenu pomocniczego, który jest zawsze wysyłany z inicjatora do odbiorcy.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-327">With this authentication mode the client authenticates using an X.509 certificate which appears at the SOAP layer as an endorsing supporting token that is always sent from the initiator to the recipient.</span></span> <span data-ttu-id="c7f6d-328">Usługa jest uwierzytelniana przy użyciu certyfikatu X. 509 w warstwie transportowej.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-328">The service is authenticated using an X.509 certificate at the transport layer.</span></span> <span data-ttu-id="c7f6d-329">Użyte powiązanie jest powiązaniem transportu.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-329">The binding used is a transport binding.</span></span>  
  
 <span data-ttu-id="c7f6d-330">Zasady</span><span class="sxs-lookup"><span data-stu-id="c7f6d-330">Policy</span></span>  
  
```xml  
<wsp:Policy wsu:Id='CertificateOverTransport_policy' >  
  <wsp:ExactlyOne>  
    <wsp:All>  
      <sp:TransportBinding xmlns:sp='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy' >  
        <wsp:Policy>  
          <sp:TransportToken>  
            <wsp:Policy>  
             <sp:HttpsToken RequireClientCertificate='false' />
            </wsp:Policy>  
          </sp:TransportToken>  
          <sp:AlgorithmSuite>  
            <wsp:Policy>  
              <sp:Basic256 />
            </wsp:Policy>  
          </sp:AlgorithmSuite>  
          <sp:Layout>  
            <wsp:Policy>  
              <sp:Strict />
            </wsp:Policy>  
          </sp:Layout>  
          <sp:IncludeTimestamp />
        </wsp:Policy>  
      </sp:TransportBinding>  
      <sp:EndorsingSupportingTokens>  
        <wsp:Policy>  
          <sp:X509Token
sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/AlwaysToRecipient' >  
            <wsp:Policy>  
              <sp:RequireThumbprintReference />
              <sp:WssX509V3Token10 />
            </wsp:Policy>  
          </sp:X509Token>  
          <sp:SignedParts>  
            <sp:Header Name='To'
Namespace='http://www.w3.org/2005/08/addressing' />
          </sp:SignedParts>  
        </wsp:Policy>  
      </sp:EndorsingSupportingTokens>  
      <sp:Wss11>  
        <wsp:Policy>  
          <sp:MustSupportRefKeyIdentifier />
          <sp:MustSupportRefIssuerSerial />
          <sp:MustSupportRefThumbprint />
          <sp:MustSupportRefEncryptedKey />
        </wsp:Policy>  
      </sp:Wss11>  
      <sp:Trust10>  
        <wsp:Policy>  
          <sp:MustSupportIssuedTokens />
          <sp:RequireClientEntropy />
          <sp:RequireServerEntropy />
        </wsp:Policy>  
      </sp:Trust10>  
      <wsaw:UsingAddressing />
    </wsp:All>  
  </wsp:ExactlyOne>  
</wsp:Policy>  
```  
  
 <span data-ttu-id="c7f6d-331">Układ nagłówka zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="c7f6d-331">Security Header Layout</span></span>  
  
 <span data-ttu-id="c7f6d-332">Żądanie</span><span class="sxs-lookup"><span data-stu-id="c7f6d-332">Request</span></span>  
  
```xml  
<wsse:Security s:mustUnderstand="1">  
  <wse:Timestamp u:Id="_0">  
  ...  
  </wse:Timestamp>  
  <wsse:BinarySecurityToken>  
  ...  
  </wsse:BinarySecurityToken>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
</wsse:Security>  
```  
  
 <span data-ttu-id="c7f6d-333">Reakcja</span><span class="sxs-lookup"><span data-stu-id="c7f6d-333">Response</span></span>  
  
```xml  
<o:Security>  
  <u:Timestamp u:Id="_0">  
  ...  
  </u:Timestamp>  
</o:Security>  
```  
  
#### <a name="613-issuedtokenovertransport"></a><span data-ttu-id="c7f6d-334">IssuedTokenOverTransport 6.1.3</span><span class="sxs-lookup"><span data-stu-id="c7f6d-334">6.1.3 IssuedTokenOverTransport</span></span>  
 <span data-ttu-id="c7f6d-335">W tym trybie uwierzytelniania klient nie jest uwierzytelniany w usłudze, w związku z czym, ale przedstawia token wystawiony przez usługę tokenu zabezpieczającego (STS) i udowadnia znajomość klucza współużytkowanego.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-335">With this authentication mode the client does not authenticate to the service, as such, but rather presents a token issued by a Security Token Service (STS) and proves knowledge of a shared key.</span></span> <span data-ttu-id="c7f6d-336">Wystawiony token jest wyświetlany w warstwie protokołu SOAP jako zatwierdzenie tokenu, który jest zawsze wysyłany z inicjatora do odbiorcy.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-336">The issued token appears at the SOAP layer as an endorsing supporting token that is always sent from the initiator to the recipient.</span></span> <span data-ttu-id="c7f6d-337">Usługa jest uwierzytelniana przy użyciu certyfikatu X. 509 w warstwie transportowej.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-337">The service is authenticated using an X.509 certificate at the transport layer.</span></span> <span data-ttu-id="c7f6d-338">Powiązanie jest powiązaniem transportu.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-338">The binding is a transport binding.</span></span>  
  
 <span data-ttu-id="c7f6d-339">Zasady</span><span class="sxs-lookup"><span data-stu-id="c7f6d-339">Policy</span></span>  
  
```xml  
<wsp:Policy wsu:Id='IssuedTokenOverTransport_policy' >  
  <wsp:ExactlyOne>  
    <wsp:All>  
      <sp:TransportBinding >  
        <wsp:Policy>  
          <sp:TransportToken>  
            <wsp:Policy>  
              <sp:HttpsToken RequireClientCertificate='false' />
            </wsp:Policy>  
          </sp:TransportToken>  
          <sp:AlgorithmSuite>  
            <wsp:Policy>  
              <sp:Basic256 />
            </wsp:Policy>  
          </sp:AlgorithmSuite>  
          <sp:Layout>  
            <wsp:Policy>  
              <sp:Strict />
            </wsp:Policy>  
          </sp:Layout>  
          <sp:IncludeTimestamp />
        </wsp:Policy>  
      </sp:TransportBinding>  
      <sp:EndorsingSupportingTokens>  
        <wsp:Policy>  
          <sp:IssuedToken
sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/AlwaysToRecipient' >  
            <sp:RequestSecurityTokenTemplate>  
              <wst:KeyType>  
              http://schemas.xmlsoap.org/ws/2005/02/trust/SymmetricKey  
              </wst:KeyType>
            </sp:RequestSecurityTokenTemplate>  
            <wsp:Policy>  
              <sp:RequireInternalReference />
            </wsp:Policy>  
          </sp:IssuedToken>  
          <sp:SignedParts>  
            <sp:Header Name='To'
Namespace='http://www.w3.org/2005/08/addressing' />
          </sp:SignedParts>  
        </wsp:Policy>  
      </sp:EndorsingSupportingTokens>  
      <sp:Wss11>  
        <wsp:Policy>  
          <sp:MustSupportRefKeyIdentifier />
          <sp:MustSupportRefIssuerSerial />
          <sp:MustSupportRefThumbprint />
          <sp:MustSupportRefEncryptedKey />
        </wsp:Policy>  
      </sp:Wss11>  
      <sp:Trust10>  
        <wsp:Policy>  
          <sp:MustSupportIssuedTokens />
          <sp:RequireClientEntropy />
          <sp:RequireServerEntropy />
        </wsp:Policy>  
      </sp:Trust10>  
      <wsaw:UsingAddressing />
    </wsp:All>  
  </wsp:ExactlyOne>  
</wsp:Policy>  
```  
  
 <span data-ttu-id="c7f6d-340">Układ nagłówka zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="c7f6d-340">Security Header Layout</span></span>  
  
 <span data-ttu-id="c7f6d-341">Żądanie</span><span class="sxs-lookup"><span data-stu-id="c7f6d-341">Request</span></span>  
  
```xml  
<wsse:Security s:mustUnderstand="1" >  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <saml:Assertion>  
  ...  
  </saml:Assertion>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
</wsse:Security>  
```  
  
 <span data-ttu-id="c7f6d-342">Reakcja</span><span class="sxs-lookup"><span data-stu-id="c7f6d-342">Response</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
</wsse:Security>  
```  
  
#### <a name="614-kerberosovertransport"></a><span data-ttu-id="c7f6d-343">6.1.4 KerberosOverTransport</span><span class="sxs-lookup"><span data-stu-id="c7f6d-343">6.1.4 KerberosOverTransport</span></span>  
 <span data-ttu-id="c7f6d-344">W tym trybie uwierzytelniania klient jest uwierzytelniany w usłudze przy użyciu biletu protokołu Kerberos.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-344">With this authentication mode the client authenticates to the service using a Kerberos ticket.</span></span> <span data-ttu-id="c7f6d-345">Token Kerberos jest wyświetlany w warstwie protokołu SOAP jako token pomocniczy.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-345">The Kerberos token appears at the SOAP layer as an endorsing supporting token.</span></span> <span data-ttu-id="c7f6d-346">Usługa jest uwierzytelniana przy użyciu certyfikatu X. 509 w warstwie transportowej.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-346">The service is authenticated using an X.509 certificate at the transport layer.</span></span> <span data-ttu-id="c7f6d-347">Powiązanie jest powiązaniem transportu.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-347">The binding is a transport binding.</span></span>  
  
 <span data-ttu-id="c7f6d-348">Zasady</span><span class="sxs-lookup"><span data-stu-id="c7f6d-348">Policy</span></span>  
  
```xml  
<wsp:Policy wsu:Id='KerberosOverTransport_policy' >  
  <wsp:ExactlyOne>  
    <wsp:All>  
      <sp:TransportBinding>  
        <wsp:Policy>  
          <sp:TransportToken>  
            <wsp:Policy>  
              <sp:HttpsToken RequireClientCertificate='false' />
            </wsp:Policy>  
          </sp:TransportToken>  
          <sp:AlgorithmSuite>  
            <wsp:Policy>  
              <sp:Basic128 />
            </wsp:Policy>  
          </sp:AlgorithmSuite>  
          <sp:Layout>  
            <wsp:Policy>  
              <sp:Strict />
            </wsp:Policy>  
          </sp:Layout>  
          <sp:IncludeTimestamp />
        </wsp:Policy>  
      </sp:TransportBinding>  
      <sp:EndorsingSupportingTokens>  
        <wsp:Policy>  
          <sp:KerberosToken  
sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/Once' >  
            <wsp:Policy>  
              <sp:WssGssKerberosV5ApReqToken11 />
            </wsp:Policy>  
          </sp:KerberosToken>  
          <sp:SignedParts>  
            <sp:Header Name='To'
Namespace='http://www.w3.org/2005/08/addressing' />
          </sp:SignedParts>  
        </wsp:Policy>  
      </sp:EndorsingSupportingTokens>  
      <sp:Wss11>  
        <wsp:Policy>  
          <sp:MustSupportRefKeyIdentifier />
          <sp:MustSupportRefIssuerSerial />
          <sp:MustSupportRefThumbprint />
          <sp:MustSupportRefEncryptedKey />
        </wsp:Policy>  
      </sp:Wss11>  
      <sp:Trust10>  
        <wsp:Policy>  
          <sp:MustSupportIssuedTokens />
          <sp:RequireClientEntropy />
          <sp:RequireServerEntropy />
        </wsp:Policy>  
      </sp:Trust10>  
      <wsaw:UsingAddressing />
    </wsp:All>  
  </wsp:ExactlyOne>  
</wsp:Policy>  
```  
  
 <span data-ttu-id="c7f6d-349">Układ nagłówka zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="c7f6d-349">Security Header Layout</span></span>  
  
 <span data-ttu-id="c7f6d-350">Żądanie</span><span class="sxs-lookup"><span data-stu-id="c7f6d-350">Request</span></span>  
  
```xml  
<wsse:Security s:mustUnderstand="1" >  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <wsse:BinarySecurityToken ValueType="...#GSS_Kerberosv5_AP_REQ">  
  ...  
  </wsse:BinarySecurityToken>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
</wsse:Security>  
```  
  
 <span data-ttu-id="c7f6d-351">Reakcja</span><span class="sxs-lookup"><span data-stu-id="c7f6d-351">Response</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
</wsse:Security>  
```  
  
#### <a name="615-sspinegotiatedovertransport"></a><span data-ttu-id="c7f6d-352">6.1.5 SspiNegotiatedOverTransport</span><span class="sxs-lookup"><span data-stu-id="c7f6d-352">6.1.5 SspiNegotiatedOverTransport</span></span>  
 <span data-ttu-id="c7f6d-353">W tym trybie protokół negocjacji jest używany do przeprowadzania uwierzytelniania klienta i serwera.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-353">With this mode a negotiation protocol is used to perform client and server authentication.</span></span> <span data-ttu-id="c7f6d-354">Protokół Kerberos jest używany, jeśli jest to możliwe, w przeciwnym razie NTLM.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-354">Kerberos is used if possible, otherwise NTLM.</span></span> <span data-ttu-id="c7f6d-355">Wynikający z tego, że SCT zostanie wyświetlony w warstwie protokołu SOAP jako zaświadczanie tokenu pomocniczego, który jest zawsze wysyłany z inicjatora do odbiorcy.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-355">The resulting SCT appears at the SOAP layer as an endorsing supporting token that is always sent from initiator to recipient.</span></span> <span data-ttu-id="c7f6d-356">Usługa jest również uwierzytelniana w warstwie transportowej przez certyfikat X. 509.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-356">The service is additionally authenticated at the transport layer by an X.509 certificate.</span></span> <span data-ttu-id="c7f6d-357">Użyte powiązanie jest powiązaniem transportu.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-357">The binding used is a transport binding.</span></span> <span data-ttu-id="c7f6d-358">"SPNEGO" (negocjowanie) opisuje, jak WCF używa protokołu negocjowania binarnego interfejsu SSPI z usługą WS-Trust.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-358">"SPNEGO" (negotiation) describes how WCF uses SSPI binary negotiation protocol with WS-Trust.</span></span> <span data-ttu-id="c7f6d-359">Przykłady nagłówka zabezpieczeń w tej sekcji są po ustanowieniu SCT przez uzgadnianie SPNEGO.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-359">Security header examples in this section are after the SCT has been established through the SPNEGO handshake.</span></span>  
  
 <span data-ttu-id="c7f6d-360">Zasady</span><span class="sxs-lookup"><span data-stu-id="c7f6d-360">Policy</span></span>  
  
```xml  
<wsp:Policy wsu:Id='SspiNegotiatedOverTransport_policy' >  
  <wsp:ExactlyOne>  
    <wsp:All>  
      <sp:TransportBinding>  
        <wsp:Policy>  
          <sp:TransportToken>  
            <wsp:Policy>  
              <sp:HttpsToken RequireClientCertificate='false' />
            </wsp:Policy>  
          </sp:TransportToken>  
          <sp:AlgorithmSuite>  
            <wsp:Policy>  
              <sp:Basic256 />
            </wsp:Policy>  
          </sp:AlgorithmSuite>  
          <sp:Layout>  
            <wsp:Policy>  
              <sp:Strict />
            </wsp:Policy>  
          </sp:Layout>  
          <sp:IncludeTimestamp />
        </wsp:Policy>  
      </sp:TransportBinding>  
      <sp:EndorsingSupportingTokens>  
        <wsp:Policy>  
          <sp:SpnegoContextToken
sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/AlwaysToRecipient' >  
            <wsp:Policy />
          </sp:SpnegoContextToken>  
          <sp:SignedParts>  
            <sp:Header Name='To'
Namespace='http://www.w3.org/2005/08/addressing' />
          </sp:SignedParts>  
        </wsp:Policy>  
      </sp:EndorsingSupportingTokens>  
      <sp:Wss11>  
        <wsp:Policy>  
          <sp:MustSupportRefKeyIdentifier />
          <sp:MustSupportRefIssuerSerial />
          <sp:MustSupportRefThumbprint />
          <sp:MustSupportRefEncryptedKey />
        </wsp:Policy>  
      </sp:Wss11>  
      <sp:Trust10>  
        <wsp:Policy>  
          <sp:MustSupportIssuedTokens />
          <sp:RequireClientEntropy />
          <sp:RequireServerEntropy />
        </wsp:Policy>  
      </sp:Trust10>  
      <wsaw:UsingAddressing />
    </wsp:All>  
  </wsp:ExactlyOne>  
</wsp:Policy>  
```  
  
### <a name="security-header-examples"></a><span data-ttu-id="c7f6d-361">Przykłady nagłówka zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="c7f6d-361">Security Header Examples</span></span>  
 <span data-ttu-id="c7f6d-362">Po ustanowieniu tokenu kontekstu zabezpieczeń za pośrednictwem uzgadniania SPNEGO przy użyciu negocjacji binarnej protokołu WS-Trust komunikaty aplikacji mają nagłówki zabezpieczeń z następującą strukturą.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-362">Once the Security Context Token is established through SPNEGO handshake using WS-Trust Binary Negotiation, the application messages have security headers with the following structure.</span></span>  
  
 <span data-ttu-id="c7f6d-363">Żądanie</span><span class="sxs-lookup"><span data-stu-id="c7f6d-363">Request</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <wssc:SecurityContextToken u:Id="uuid-2202746a-7725-453d-8747-809cb718dab0-29" >  
  ...  
  </wssc:SecurityContextToken>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
</wsse:Security>  
```  
  
 <span data-ttu-id="c7f6d-364">Reakcja</span><span class="sxs-lookup"><span data-stu-id="c7f6d-364">Response</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
</wsse:Security>  
```  
  
### <a name="62-using-x509-certificates-for-service-authentication"></a><span data-ttu-id="c7f6d-365">6,2 przy użyciu certyfikatów X. 509 do uwierzytelniania usługi</span><span class="sxs-lookup"><span data-stu-id="c7f6d-365">6.2 Using X.509 Certificates for Service Authentication</span></span>  
 <span data-ttu-id="c7f6d-366">W tej sekcji opisano następujące tryby uwierzytelniania: MutualCertificate WSS 1.0, wzajemne CertificateDuplex, MutualCertificate WSS 1.1, AnonymousForCertificate, UserNameForCertificate i IssuedTokenForCertificate.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-366">This section describes the following authentication modes: MutualCertificate WSS1.0, Mutual CertificateDuplex, MutualCertificate WSS1.1, AnonymousForCertificate, UserNameForCertificate and IssuedTokenForCertificate.</span></span>  
  
#### <a name="621-mutualcertificate-wss10"></a><span data-ttu-id="c7f6d-367">6.2.1 MutualCertificate WSS 1.0</span><span class="sxs-lookup"><span data-stu-id="c7f6d-367">6.2.1 MutualCertificate WSS1.0</span></span>  
 <span data-ttu-id="c7f6d-368">W tym trybie uwierzytelniania klient jest uwierzytelniany przy użyciu certyfikatu X. 509, który jest wyświetlany w warstwie protokołu SOAP jako token inicjatora.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-368">With this authentication mode the client authenticates using an X.509 certificate which appears at the SOAP layer as the initiator token.</span></span> <span data-ttu-id="c7f6d-369">Usługa jest również uwierzytelniana przy użyciu certyfikatu X. 509.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-369">The service is also authenticated using an X.509 certificate.</span></span>  
  
 <span data-ttu-id="c7f6d-370">Używane powiązanie jest powiązaniem asymetrycznym z następującymi wartościami właściwości:</span><span class="sxs-lookup"><span data-stu-id="c7f6d-370">The binding used is an asymmetric binding with the following property values:</span></span>  
  
 <span data-ttu-id="c7f6d-371">Token inicjatora: certyfikat X. 509 klienta z trybem dołączania ustawionym na. ../IncludeToken/AlwaysToRecipient</span><span class="sxs-lookup"><span data-stu-id="c7f6d-371">Initiator Token: the client’s X.509 certificate, with inclusion mode set to …/IncludeToken/AlwaysToRecipient</span></span>  
  
 <span data-ttu-id="c7f6d-372">Token adresata: certyfikat X. 509 serwera z ustawionym trybem dołączania. ../IncludeToken/Never</span><span class="sxs-lookup"><span data-stu-id="c7f6d-372">Recipient Token: Server’s X.509 Certificate, with inclusion mode is set …/IncludeToken/Never</span></span>  
  
 <span data-ttu-id="c7f6d-373">Ochrona tokenu: FAŁSZ</span><span class="sxs-lookup"><span data-stu-id="c7f6d-373">Token Protection: False</span></span>  
  
 <span data-ttu-id="c7f6d-374">Cały podpis nagłówka i treści: prawda</span><span class="sxs-lookup"><span data-stu-id="c7f6d-374">Entire Header And Body Signatures: True</span></span>  
  
 <span data-ttu-id="c7f6d-375">Kolejność ochrony: SignBeforeEncrypt</span><span class="sxs-lookup"><span data-stu-id="c7f6d-375">Protection Order: SignBeforeEncrypt</span></span>  
  
 <span data-ttu-id="c7f6d-376">Szyfruj sygnaturę: prawda</span><span class="sxs-lookup"><span data-stu-id="c7f6d-376">Encrypt Signature: True</span></span>  
  
 <span data-ttu-id="c7f6d-377">Zasady</span><span class="sxs-lookup"><span data-stu-id="c7f6d-377">Policy</span></span>  
  
```xml  
<wsp:Policy wsu:Id='MutualCertificate_WSS10_policy' >  
  <wsp:ExactlyOne>  
    <wsp:All>  
      <sp:AsymmetricBinding>  
        <wsp:Policy>  
          <sp:InitiatorToken>  
            <wsp:Policy>  
              <sp:X509Token
sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/AlwaysToRecipient' >  
                <wsp:Policy>  
                  <sp:WssX509V3Token10 />
                </wsp:Policy>  
              </sp:X509Token>  
            </wsp:Policy>  
          </sp:InitiatorToken>  
          <sp:RecipientToken>  
            <wsp:Policy>  
              <sp:X509Token
sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/Never' >  
                <wsp:Policy>  
                  <sp:WssX509V3Token10 />
                </wsp:Policy>  
              </sp:X509Token>  
            </wsp:Policy>  
          </sp:RecipientToken>  
          <sp:AlgorithmSuite>  
            <wsp:Policy>  
              <sp:Basic256 />
            </wsp:Policy>  
          </sp:AlgorithmSuite>  
          <sp:Layout>  
            <wsp:Policy>  
              <sp:Strict />
            </wsp:Policy>  
          </sp:Layout>  
          <sp:IncludeTimestamp />
          <sp:EncryptSignature />
          <sp:OnlySignEntireHeadersAndBody />
        </wsp:Policy>  
      </sp:AsymmetricBinding>  
      <sp:Wss10>  
        <wsp:Policy>  
          <sp:MustSupportRefKeyIdentifier />
          <sp:MustSupportRefIssuerSerial />
        </wsp:Policy>  
      </sp:Wss10>  
      <sp:Trust10>  
        <wsp:Policy>  
          <sp:MustSupportIssuedTokens />
          <sp:RequireClientEntropy />
          <sp:RequireServerEntropy />
        </wsp:Policy>  
      </sp:Trust10>  
      <wsaw:UsingAddressing />
    </wsp:All>  
  </wsp:ExactlyOne>  
</wsp:Policy>  
```  
  
### <a name="security-header-examples-signbeforeencrypt-encryptsignature"></a><span data-ttu-id="c7f6d-378">Przykłady nagłówka zabezpieczeń: SignBeforeEncrypt, EncryptSignature</span><span class="sxs-lookup"><span data-stu-id="c7f6d-378">Security Header Examples: SignBeforeEncrypt, EncryptSignature</span></span>  
 <span data-ttu-id="c7f6d-379">Żądanie</span><span class="sxs-lookup"><span data-stu-id="c7f6d-379">Request</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <wsse:BinarySecurityToken>  
  ...  
  </wsse:BinarySecurityToken>  
  <xenc:EncryptedKey>  
  ...  
    <xenc:ReferenceList>  
    ...  
    </xenc:ReferenceList>  
  </xenc:EncryptedKey>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>  
```  
  
 <span data-ttu-id="c7f6d-380">Reakcja</span><span class="sxs-lookup"><span data-stu-id="c7f6d-380">Response</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <xenc:EncryptedKey>  
  ...  
    <xenc:ReferenceList>  
    ...  
    </xenc:ReferenceList>  
  </xenc:EncryptedKey>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>  
```  
  
 <span data-ttu-id="c7f6d-381">Przykłady nagłówka zabezpieczeń: EncryptBeforeSign</span><span class="sxs-lookup"><span data-stu-id="c7f6d-381">Security Header Examples: EncryptBeforeSign</span></span>  
  
 <span data-ttu-id="c7f6d-382">Żądanie</span><span class="sxs-lookup"><span data-stu-id="c7f6d-382">Request</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <wsse:BinarySecurityToken>  
  ...  
  </wsse:BinarySecurityToken>  
  <xenc:EncryptedKey>  
  ...  
  </xenc:EncryptedKey>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
 <span data-ttu-id="c7f6d-383">Reakcja</span><span class="sxs-lookup"><span data-stu-id="c7f6d-383">Response</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <xenc:EncryptedKey>  
  ...  
  </xenc:EncryptedKey>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
#### <a name="622-mutualcertificateduplex"></a><span data-ttu-id="c7f6d-384">6.2.2 MutualCertificateDuplex</span><span class="sxs-lookup"><span data-stu-id="c7f6d-384">6.2.2 MutualCertificateDuplex</span></span>  
 <span data-ttu-id="c7f6d-385">W tym trybie uwierzytelniania klient jest uwierzytelniany przy użyciu certyfikatu X. 509, który jest wyświetlany w warstwie protokołu SOAP jako token inicjatora.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-385">With this authentication mode the client authenticates using an X.509 certificate which appears at the SOAP layer as the initiator token.</span></span> <span data-ttu-id="c7f6d-386">Usługa jest również uwierzytelniana przy użyciu certyfikatu X. 509.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-386">The service is also authenticated using an X.509 certificate.</span></span>  
  
 <span data-ttu-id="c7f6d-387">Używane powiązanie jest powiązaniem asymetrycznym z następującymi wartościami właściwości:</span><span class="sxs-lookup"><span data-stu-id="c7f6d-387">The binding used is an asymmetric binding with the following property values:</span></span>  
  
 <span data-ttu-id="c7f6d-388">Token inicjatora: certyfikat x509 klienta, tryb dołączania ma wartość. ../IncludeToken/AlwaysToRecipient</span><span class="sxs-lookup"><span data-stu-id="c7f6d-388">Initiator Token: Client’s X509 Certificate, inclusion mode is set to …/IncludeToken/AlwaysToRecipient</span></span>  
  
 <span data-ttu-id="c7f6d-389">Token adresata: certyfikat x509 serwera, tryb dołączania ma wartość. ../IncludeToken/AlwaysToInitiator</span><span class="sxs-lookup"><span data-stu-id="c7f6d-389">Recipient Token: Server’s X509 Certificate, inclusion mode is set to …/IncludeToken/AlwaysToInitiator</span></span>  
  
 <span data-ttu-id="c7f6d-390">Ochrona tokenu: FAŁSZ</span><span class="sxs-lookup"><span data-stu-id="c7f6d-390">Token Protection: False</span></span>  
  
 <span data-ttu-id="c7f6d-391">Cały podpis nagłówka i treści: prawda</span><span class="sxs-lookup"><span data-stu-id="c7f6d-391">Entire Header And Body Signatures: True</span></span>  
  
 <span data-ttu-id="c7f6d-392">Kolejność ochrony: SignBeforeEncrypt</span><span class="sxs-lookup"><span data-stu-id="c7f6d-392">Protection Order: SignBeforeEncrypt</span></span>  
  
 <span data-ttu-id="c7f6d-393">Szyfruj sygnaturę: prawda</span><span class="sxs-lookup"><span data-stu-id="c7f6d-393">Encrypt Signature: True</span></span>  
  
 <span data-ttu-id="c7f6d-394">Zasady</span><span class="sxs-lookup"><span data-stu-id="c7f6d-394">Policy</span></span>  
  
```xml  
<wsp:Policy wsu:Id='MutualCertificateDuplex_policy' >  
  <wsp:ExactlyOne>  
    <wsp:All>  
      <sp:AsymmetricBinding>  
        <wsp:Policy>  
          <sp:InitiatorToken>  
            <wsp:Policy>  
              <sp:X509Token
sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/AlwaysToRecipient' >  
                <wsp:Policy>  
                  <sp:WssX509V3Token10 />
                </wsp:Policy>  
              </sp:X509Token>  
            </wsp:Policy>  
          </sp:InitiatorToken>  
          <sp:RecipientToken>  
            <wsp:Policy>  
              <sp:X509Token
sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/AlwaysToInitiator' >  
                <wsp:Policy>  
                  <sp:WssX509V3Token10 />
                </wsp:Policy>  
              </sp:X509Token>  
            </wsp:Policy>  
          </sp:RecipientToken>  
          <sp:AlgorithmSuite>  
            <wsp:Policy>  
              <sp:Basic256 />
            </wsp:Policy>  
          </sp:AlgorithmSuite>  
          <sp:Layout>  
            <wsp:Policy>  
              <sp:Strict />
            </wsp:Policy>  
          </sp:Layout>  
          <sp:IncludeTimestamp />
          <sp:EncryptSignature />
          <sp:OnlySignEntireHeadersAndBody />
        </wsp:Policy>  
      </sp:AsymmetricBinding>  
      <sp:Wss10>  
        <wsp:Policy>  
          <sp:MustSupportRefKeyIdentifier />
          <sp:MustSupportRefIssuerSerial />
        </wsp:Policy>  
      </sp:Wss10>  
      <sp:Trust10>  
        <wsp:Policy>  
          <sp:MustSupportIssuedTokens />
          <sp:RequireClientEntropy />
          <sp:RequireServerEntropy />
        </wsp:Policy>  
      </sp:Trust10>  
      <wsaw:UsingAddressing />
    </wsp:All>  
  </wsp:ExactlyOne>  
</wsp:Policy>  
```  
  
### <a name="security-header-examples-signbeforeencrypt-encryptsignature"></a><span data-ttu-id="c7f6d-395">Przykłady nagłówka zabezpieczeń: SignBeforeEncrypt, EncryptSignature</span><span class="sxs-lookup"><span data-stu-id="c7f6d-395">Security Header Examples: SignBeforeEncrypt, EncryptSignature</span></span>  
 <span data-ttu-id="c7f6d-396">Żądanie i odpowiedź</span><span class="sxs-lookup"><span data-stu-id="c7f6d-396">Request and Response</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <wsse:BinarySecurityToken>  
  ...  
  </wsse:BinarySecurityToken>  
  <xenc:EncryptedKey>  
  ...  
    <xenc:ReferenceList>  
    ...  
    </xenc:ReferenceList>  
  </xenc:EncryptedKey>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>  
```  
  
### <a name="security-header-examples-encryptbeforesign"></a><span data-ttu-id="c7f6d-397">Przykłady nagłówka zabezpieczeń: EncryptBeforeSign</span><span class="sxs-lookup"><span data-stu-id="c7f6d-397">Security Header Examples: EncryptBeforeSign</span></span>  
 <span data-ttu-id="c7f6d-398">Żądanie i odpowiedź</span><span class="sxs-lookup"><span data-stu-id="c7f6d-398">Request and Response</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <wsse:BinarySecurityToken>  
  ...  
  </wsse:BinarySecurityToken>  
  <xenc:EncryptedKey>  
  ...  
  </xenc:EncryptedKey>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
#### <a name="623-using-symmetricbinding-with-x509-service-authentication"></a><span data-ttu-id="c7f6d-399">6.2.3 przy użyciu funkcji Symetrycznebinding z uwierzytelnianiem za pomocą usługi X. 509</span><span class="sxs-lookup"><span data-stu-id="c7f6d-399">6.2.3 Using SymmetricBinding with X.509 Service Authentication</span></span>  
 <span data-ttu-id="c7f6d-400">"WSS10" zapewnia ograniczoną obsługę scenariuszy z tokenami x509.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-400">"WSS10" provided limited support for scenarios with X509 tokens.</span></span> <span data-ttu-id="c7f6d-401">Na przykład nie było możliwości zapewnienia podpisywania i ochrony przed szyfrowaniem komunikatów przy użyciu tylko tokenu x509 usługi.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-401">For example, there was no way to provide signature and encryption protection for messages using only service X509 token.</span></span> <span data-ttu-id="c7f6d-402">"WSS11" wprowadził Użycie EncryptedKey jako tokenu symetrycznego.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-402">"WSS11" introduced the usage of EncryptedKey as a symmetric token.</span></span> <span data-ttu-id="c7f6d-403">Teraz klucz tymczasowy szyfrowany dla certyfikatu X. 509 usługi może być używany zarówno w przypadku ochrony komunikatów żądania, jak i odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-403">Now a temporary key encrypted for the service's X.509 certificate could be used for both request and response messages protection.</span></span> <span data-ttu-id="c7f6d-404">W przypadku trybów uwierzytelniania opisanych w sekcji 6,4 poniżej Użyj tego wzorca.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-404">The authentication modes described in the section 6.4 below use this pattern.</span></span>  
  
 <span data-ttu-id="c7f6d-405">Usługa WS-SecurityPolicy opisuje ten wzorzec przy użyciu protokołu Symetrycznybinding z tokenem x509 usługi jako tokenem ochrony.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-405">WS-SecurityPolicy describes this pattern using SymmetricBinding with Service X509 token as the protection token.</span></span>  
  
 <span data-ttu-id="c7f6d-406">Tryby uwierzytelniania AnonymousForCertificate, UsernameForCertificate, MutualCertificate WSS11 i IssuedTokenForCertificate używają podobnego wystąpienia SP: Symetrycznebinding z następującymi wartościami właściwości:</span><span class="sxs-lookup"><span data-stu-id="c7f6d-406">Authentication modes AnonymousForCertificate, UsernameForCertificate, MutualCertificate WSS11 and IssuedTokenForCertificate all use a similar instance of sp:SymmetricBinding with the following property values:</span></span>  
  
 <span data-ttu-id="c7f6d-407">Token ochrony: certyfikat x509 serwera, tryb dołączania ma wartość. ../IncludeToken/Never</span><span class="sxs-lookup"><span data-stu-id="c7f6d-407">Protection Token: Server’s X509 Certificate, inclusion mode is set to .../IncludeToken/Never</span></span>  
<span data-ttu-id="c7f6d-408">Ochrona tokenu: FAŁSZ</span><span class="sxs-lookup"><span data-stu-id="c7f6d-408">Token Protection: False</span></span>  
  
 <span data-ttu-id="c7f6d-409">Cały podpis nagłówka i treści: prawda</span><span class="sxs-lookup"><span data-stu-id="c7f6d-409">Entire Header And Body Signatures: True</span></span>  
  
 <span data-ttu-id="c7f6d-410">Kolejność ochrony: SignBeforeEncrypt</span><span class="sxs-lookup"><span data-stu-id="c7f6d-410">Protection Order: SignBeforeEncrypt</span></span>  
  
 <span data-ttu-id="c7f6d-411">Szyfruj sygnaturę: prawda</span><span class="sxs-lookup"><span data-stu-id="c7f6d-411">Encrypt Signature: True</span></span>  
  
 <span data-ttu-id="c7f6d-412">Powyższe tryby uwierzytelniania różnią się tylko przez tokeny pomocnicze, których używają.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-412">The above authentication modes only differ by the supporting tokens they use.</span></span> <span data-ttu-id="c7f6d-413">AnonymousForCertificate nie ma żadnych tokenów pomocniczych, MutualCertificate WSS 1,1 ma certyfikat x509 klienta jako poświadczający tokeny pomocnicze, UserNameForCertificate ma token nazwy użytkownika jako podpisany token pomocniczy, a IssuedTokenForCertificate ma token wystawiony jako token pomocniczy.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-413">AnonymousForCertificate does not have any supporting tokens, MutualCertificate WSS 1.1 has the client’s X509 certificate as an endorsing supporting tokens, UserNameForCertificate has a UserName Token as a signed supporting token and IssuedTokenForCertificate has the issued token as an endorsing supporting token.</span></span>  
  
 <span data-ttu-id="c7f6d-414">Zasady</span><span class="sxs-lookup"><span data-stu-id="c7f6d-414">Policy</span></span>  
  
 <span data-ttu-id="c7f6d-415">Powiązanie symetryczne</span><span class="sxs-lookup"><span data-stu-id="c7f6d-415">Symmetric Binding</span></span>  
  
```xml  
<wsp:Policy wsu:Id='SymmetricCert_policy' >  
  <wsp:ExactlyOne>  
    <wsp:All>  
      <sp:SymmetricBinding>  
        <wsp:Policy>  
          <sp:ProtectionToken>  
            <wsp:Policy>  
              <sp:X509Token
sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/Never' >  
                <wsp:Policy>  
                  <sp:RequireDerivedKeys />
                  <sp:RequireThumbprintReference />
                  <sp:WssX509V3Token10 />
                </wsp:Policy>  
              </sp:X509Token>  
            </wsp:Policy>  
          </sp:ProtectionToken>  
          <sp:AlgorithmSuite>  
            <wsp:Policy>  
              <sp:Basic256 />
            </wsp:Policy>  
          </sp:AlgorithmSuite>  
          <sp:Layout>  
            <wsp:Policy>  
              <sp:Strict />
            </wsp:Policy>  
          </sp:Layout>  
          <sp:IncludeTimestamp />
          <sp:EncryptSignature />
          <sp:OnlySignEntireHeadersAndBody />  
        </wsp:Policy>  
      </sp:SymmetricBinding>  
      <!-- Supporting Token Assertions appear here -->  
      ...  
      <sp:Wss11>  
        <wsp:Policy>  
          <sp:MustSupportRefKeyIdentifier />
          <sp:MustSupportRefIssuerSerial />
          <sp:MustSupportRefThumbprint />
          <sp:MustSupportRefEncryptedKey />
          <sp:RequireSignatureConfirmation />
        </wsp:Policy>  
      </sp:Wss11>  
      <sp:Trust10>  
        <wsp:Policy>  
          <sp:MustSupportIssuedTokens />
          <sp:RequireClientEntropy />
          <sp:RequireServerEntropy />
        </wsp:Policy>  
      </sp:Trust10>  
      <wsaw:UsingAddressing />
    </wsp:All>  
  </wsp:ExactlyOne>  
</wsp:Policy>  
```  
  
#### <a name="624-anonymousforcertificate"></a><span data-ttu-id="c7f6d-416">6.2.4 AnonymousForCertificate</span><span class="sxs-lookup"><span data-stu-id="c7f6d-416">6.2.4 AnonymousForCertificate</span></span>  
 <span data-ttu-id="c7f6d-417">W tym trybie uwierzytelniania klient jest anonimowy i usługa jest uwierzytelniana przy użyciu certyfikatu X. 509.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-417">With this authentication mode the client is anonymous and the service is authenticated using an X.509 certificate.</span></span> <span data-ttu-id="c7f6d-418">Użyte powiązanie to wystąpienie powiązania symetrycznego, zgodnie z opisem w 6.4.2.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-418">The binding used is an instance of symmetric binding as described in 6.4.2.</span></span>  
  
 <span data-ttu-id="c7f6d-419">Zasady</span><span class="sxs-lookup"><span data-stu-id="c7f6d-419">Policy</span></span>  
  
 <span data-ttu-id="c7f6d-420">Aby uzyskać szczegółowe informacje o powiązaniu, zobacz sekcję "zasady" w obszarze 6.2.3 powyżej</span><span class="sxs-lookup"><span data-stu-id="c7f6d-420">See "Policy" in 6.2.3 above for binding details</span></span>  
  
### <a name="security-header-examples-signbeforeencrypt-encryptsignature"></a><span data-ttu-id="c7f6d-421">Przykłady nagłówka zabezpieczeń: SignBeforeEncrypt, EncryptSignature</span><span class="sxs-lookup"><span data-stu-id="c7f6d-421">Security Header Examples: SignBeforeEncrypt, EncryptSignature</span></span>  
 <span data-ttu-id="c7f6d-422">Żądanie</span><span class="sxs-lookup"><span data-stu-id="c7f6d-422">Request</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <xenc:EncryptedKey>  
  ...  
  </xenc:EncryptedKey>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>  
```  
  
 <span data-ttu-id="c7f6d-423">Reakcja</span><span class="sxs-lookup"><span data-stu-id="c7f6d-423">Response</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>  
```  
  
### <a name="security-header-examples-encryptbeforesign"></a><span data-ttu-id="c7f6d-424">Przykłady nagłówka zabezpieczeń: EncryptBeforeSign</span><span class="sxs-lookup"><span data-stu-id="c7f6d-424">Security Header Examples: EncryptBeforeSign</span></span>  
 <span data-ttu-id="c7f6d-425">Żądanie</span><span class="sxs-lookup"><span data-stu-id="c7f6d-425">Request</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <xenc:EncryptedKey>  
  ...  
  </xenc:EncryptedKey>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
 <span data-ttu-id="c7f6d-426">Reakcja</span><span class="sxs-lookup"><span data-stu-id="c7f6d-426">Response</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wsse11:SignatureConfirmation />  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
#### <a name="625-usernameforcertificate"></a><span data-ttu-id="c7f6d-427">6.2.5 UserNameForCertificate</span><span class="sxs-lookup"><span data-stu-id="c7f6d-427">6.2.5 UserNameForCertificate</span></span>  
 <span data-ttu-id="c7f6d-428">W tym trybie uwierzytelniania klient jest uwierzytelniany w usłudze przy użyciu tokenu nazwy użytkownika, który pojawia się w warstwie protokołu SOAP jako podpisanego tokenu pomocniczego.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-428">With this authentication mode the client authenticates to the service using a Username Token which appears at the SOAP layer as a signed supporting token.</span></span> <span data-ttu-id="c7f6d-429">Usługa jest uwierzytelniana na kliencie przy użyciu certyfikatu X. 509.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-429">The service authenticates to the client using an X.509 certificate.</span></span> <span data-ttu-id="c7f6d-430">Używane powiązanie jest powiązaniem symetrycznym z tokenem ochrony, który jest kluczem generowanym przez klienta, szyfrowanym przy użyciu klucza publicznego usługi.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-430">The binding used is a symmetric binding with the protection token being a key generated by the client, encrypted with the public key of the service.</span></span>  
  
 <span data-ttu-id="c7f6d-431">Zasady</span><span class="sxs-lookup"><span data-stu-id="c7f6d-431">Policy</span></span>  
  
 <span data-ttu-id="c7f6d-432">Aby uzyskać szczegółowe informacje o powiązaniu, zobacz sekcję "zasady" w obszarze 6.2.3 powyżej</span><span class="sxs-lookup"><span data-stu-id="c7f6d-432">See "Policy" in 6.2.3 above for binding details</span></span>  
  
 <span data-ttu-id="c7f6d-433">Podpisany token pomocniczy</span><span class="sxs-lookup"><span data-stu-id="c7f6d-433">Signed Supporting Token</span></span>  
  
```xml  
<sp:SignedSupportingTokens>  
  <wsp:Policy>  
    <sp:UsernameToken sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/AlwaysToRecipient' >  
      <wsp:Policy>  
        <sp:WssUsernameToken10 />
      </wsp:Policy>  
    </sp:UsernameToken>  
  </wsp:Policy>  
</sp:SignedSupportingTokens>  
```  
  
### <a name="security-header-examples-signbeforeencrypt-encryptsignature"></a><span data-ttu-id="c7f6d-434">Przykłady nagłówka zabezpieczeń: SignBeforeEncrypt, EncryptSignature</span><span class="sxs-lookup"><span data-stu-id="c7f6d-434">Security Header Examples: SignBeforeEncrypt, EncryptSignature</span></span>  
 <span data-ttu-id="c7f6d-435">Żądanie</span><span class="sxs-lookup"><span data-stu-id="c7f6d-435">Request</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <xenc:EncryptedKey>  
  ...  
  </xenc:EncryptedKey>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>  
```  
  
 <span data-ttu-id="c7f6d-436">Reakcja</span><span class="sxs-lookup"><span data-stu-id="c7f6d-436">Response</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>  
```  
  
### <a name="security-header-examples-encryptbeforesign"></a><span data-ttu-id="c7f6d-437">Przykłady nagłówka zabezpieczeń: EncryptBeforeSign</span><span class="sxs-lookup"><span data-stu-id="c7f6d-437">Security Header Examples: EncryptBeforeSign</span></span>  
 <span data-ttu-id="c7f6d-438">Żądanie</span><span class="sxs-lookup"><span data-stu-id="c7f6d-438">Request</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <xenc:EncryptedKey>  
  ...  
  </xenc:EncryptedKey>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
 <span data-ttu-id="c7f6d-439">Reakcja</span><span class="sxs-lookup"><span data-stu-id="c7f6d-439">Response</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
#### <a name="626-mutualcertificate-wss-11"></a><span data-ttu-id="c7f6d-440">6.2.6 MutualCertificate (WSS 1,1)</span><span class="sxs-lookup"><span data-stu-id="c7f6d-440">6.2.6 MutualCertificate (WSS 1.1)</span></span>  
 <span data-ttu-id="c7f6d-441">W tym trybie uwierzytelniania klient jest uwierzytelniany przy użyciu certyfikatu X. 509, który jest wyświetlany w warstwie protokołu SOAP jako token pomocniczy.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-441">With this authentication mode the client authenticates using an X.509 certificate which appears at the SOAP layer as an endorsing supporting token.</span></span> <span data-ttu-id="c7f6d-442">Usługa jest również uwierzytelniana przy użyciu certyfikatu X. 509.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-442">The service is also authenticated using an X.509 certificate.</span></span> <span data-ttu-id="c7f6d-443">Używane powiązanie jest powiązaniem symetrycznym z tokenem ochrony, który jest kluczem generowanym przez klienta, szyfrowanym przy użyciu klucza publicznego usługi.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-443">The binding used is a symmetric binding with the protection token being a key generated by the client, encrypted with the public key of the service.</span></span>  
  
 <span data-ttu-id="c7f6d-444">Zasady</span><span class="sxs-lookup"><span data-stu-id="c7f6d-444">Policy</span></span>  
  
 <span data-ttu-id="c7f6d-445">Szczegóły powiązań można znaleźć w temacie zasady w sekcji 6.2.3</span><span class="sxs-lookup"><span data-stu-id="c7f6d-445">See Policy in 6.2.3 for binding details</span></span>  
  
 <span data-ttu-id="c7f6d-446">Zatwierdzanie tokenu pomocniczego</span><span class="sxs-lookup"><span data-stu-id="c7f6d-446">Endorsing Supporting Token</span></span>  
  
```xml  
<sp:EndorsingSupportingTokens>  
  <wsp:Policy>  
    <sp:X509Token sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/AlwaysToRecipient' >  
      <wsp:Policy>  
        <sp:RequireThumbprintReference />
        <sp:WssX509V3Token10 />
      </wsp:Policy>  
    </sp:X509Token>  
  </wsp:Policy>  
</sp:EndorsingSupportingTokens>  
```  
  
### <a name="security-header-examples-signbeforeencrypt-encryptsignature"></a><span data-ttu-id="c7f6d-447">Przykłady nagłówka zabezpieczeń: SignBeforeEncrypt, EncryptSignature</span><span class="sxs-lookup"><span data-stu-id="c7f6d-447">Security Header Examples: SignBeforeEncrypt, EncryptSignature</span></span>  
 <span data-ttu-id="c7f6d-448">Żądanie</span><span class="sxs-lookup"><span data-stu-id="c7f6d-448">Request</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <xenc:EncryptedKey>  
  ...  
  </xenc:EncryptedKey>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <wsse:BinarySecurityToken>  
  ...  
  </wsse:BinarySecurityToken>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>  
```  
  
 <span data-ttu-id="c7f6d-449">Reakcja</span><span class="sxs-lookup"><span data-stu-id="c7f6d-449">Response</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <wsse:BinarySecurityToken>  
  ...  
  </wsse:BinarySecurityToken>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>  
```  
  
### <a name="security-header-examples-encryptbeforesign"></a><span data-ttu-id="c7f6d-450">Przykłady nagłówka zabezpieczeń: EncryptBeforeSign</span><span class="sxs-lookup"><span data-stu-id="c7f6d-450">Security Header Examples: EncryptBeforeSign</span></span>  
 <span data-ttu-id="c7f6d-451">Żądanie</span><span class="sxs-lookup"><span data-stu-id="c7f6d-451">Request</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <xenc:EncryptedKey>  
  ...  
  </xenc:EncryptedKey>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wsse:BinarySecurityToken>  
  ...  
  </wsse:BinarySecurityToken>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
 <span data-ttu-id="c7f6d-452">Reakcja</span><span class="sxs-lookup"><span data-stu-id="c7f6d-452">Response</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <xenc:EncryptedKey>  
  ...  
  </xenc:EncryptedKey>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wsse11:SignatureConfirmation />  
  <wsse11:SignatureConfirmation />  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
#### <a name="627-issuedtokenforcertificate"></a><span data-ttu-id="c7f6d-453">6.2.7 IssuedTokenForCertificate</span><span class="sxs-lookup"><span data-stu-id="c7f6d-453">6.2.7 IssuedTokenForCertificate</span></span>  
 <span data-ttu-id="c7f6d-454">W tym trybie uwierzytelniania klient nie jest uwierzytelniany w usłudze w taki sposób, ale przedstawia token wystawiony przez usługę STS i udowadnia znajomość klucza współużytkowanego.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-454">With this authentication mode the client does not authenticate to the service, as such, but instead presents a token issued by a STS and proves knowledge of a shared key.</span></span> <span data-ttu-id="c7f6d-455">Wystawiony token pojawia się na warstwie protokołu SOAP jako token pomocniczy.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-455">The issued token appears at the SOAP layer as an endorsing supporting token.</span></span> <span data-ttu-id="c7f6d-456">Usługa jest uwierzytelniana na kliencie przy użyciu certyfikatu X. 509.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-456">The service authenticates to the client using an X.509 certificate.</span></span> <span data-ttu-id="c7f6d-457">Używane powiązanie jest powiązaniem symetrycznym z tokenem ochrony, który jest kluczem generowanym przez klienta, szyfrowanym przy użyciu klucza publicznego usługi.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-457">The binding used is a symmetric binding with the protection token being a key generated by the client, encrypted with the public key of the service.</span></span>  
  
 <span data-ttu-id="c7f6d-458">Zasady</span><span class="sxs-lookup"><span data-stu-id="c7f6d-458">Policy</span></span>  
  
 <span data-ttu-id="c7f6d-459">Szczegóły powiązania można znaleźć w temacie zasady w sekcji 6.2.3 powyżej</span><span class="sxs-lookup"><span data-stu-id="c7f6d-459">See Policy in 6.2.3 above for binding details</span></span>  
  
 <span data-ttu-id="c7f6d-460">Zatwierdzanie tokenu pomocniczego</span><span class="sxs-lookup"><span data-stu-id="c7f6d-460">Endorsing Supporting Token</span></span>  
  
```xml  
<sp:EndorsingSupportingTokens>  
  <wsp:Policy>  
    <sp:IssuedToken sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/AlwaysToRecipient' >  
      <sp:RequestSecurityTokenTemplate>  
        <wst:KeyType>  
http://schemas.xmlsoap.org/ws/2005/02/trust/SymmetricKey  
       </wst:KeyType>  
     </sp:RequestSecurityTokenTemplate>  
     <wsp:Policy>  
       <sp:RequireDerivedKeys />
       <sp:RequireInternalReference />
     </wsp:Policy>  
   </sp:IssuedToken>  
  </wsp:Policy>  
</sp:EndorsingSupportingTokens>  
```  
  
### <a name="security-header-examples-signbeforeencrypt-encryptsignature"></a><span data-ttu-id="c7f6d-461">Przykłady nagłówka zabezpieczeń: SignBeforeEncrypt, EncryptSignature</span><span class="sxs-lookup"><span data-stu-id="c7f6d-461">Security Header Examples: SignBeforeEncrypt, EncryptSignature</span></span>  
 <span data-ttu-id="c7f6d-462">Żądanie</span><span class="sxs-lookup"><span data-stu-id="c7f6d-462">Request</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <xenc:EncryptedKey>  
  ...  
  </xenc:EncryptedKey>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <saml:Assertion>  
  ...  
  </saml:Assertion>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>  
```  
  
 <span data-ttu-id="c7f6d-463">Reakcja</span><span class="sxs-lookup"><span data-stu-id="c7f6d-463">Response</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>  
```  
  
### <a name="security-header-examples-encryptbeforesign"></a><span data-ttu-id="c7f6d-464">Przykłady nagłówka zabezpieczeń: EncryptBeforeSign</span><span class="sxs-lookup"><span data-stu-id="c7f6d-464">Security Header Examples: EncryptBeforeSign</span></span>  
 <span data-ttu-id="c7f6d-465">Żądanie</span><span class="sxs-lookup"><span data-stu-id="c7f6d-465">Request</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <xenc:EncryptedKey>  
  ...  
  </xenc:EncryptedKey>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <saml:Assertion>  
  ...  
  </saml:Assertion>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
 <span data-ttu-id="c7f6d-466">Reakcja</span><span class="sxs-lookup"><span data-stu-id="c7f6d-466">Response</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp u:Id="_0">  
  ...  
  </wsu:Timestamp>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wssc:DerivedKeyToken>  
  ...  
  </wssc:DerivedKeyToken>  
  <wsse11:SignatureConfirmation />  
  <wsse11:SignatureConfirmation />  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
## <a name="63-kerberos"></a><span data-ttu-id="c7f6d-467">6,3 Kerberos</span><span class="sxs-lookup"><span data-stu-id="c7f6d-467">6.3 Kerberos</span></span>  
 <span data-ttu-id="c7f6d-468">W tym trybie uwierzytelniania klient jest uwierzytelniany w usłudze przy użyciu biletu protokołu Kerberos.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-468">With this authentication mode the client authenticates to the service using a Kerberos ticket.</span></span> <span data-ttu-id="c7f6d-469">Ten sam bilet zapewnia również uwierzytelnianie serwera.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-469">That same ticket also provides server authentication.</span></span> <span data-ttu-id="c7f6d-470">Używane powiązanie jest powiązaniem symetrycznym z następującymi właściwościami:</span><span class="sxs-lookup"><span data-stu-id="c7f6d-470">The binding used is a symmetric binding with the following properties;</span></span>  
  
 <span data-ttu-id="c7f6d-471">Token ochrony: bilet protokołu Kerberos, tryb dołączania jest ustawiony na wartość. ../IncludeToken/Once</span><span class="sxs-lookup"><span data-stu-id="c7f6d-471">Protection Token: Kerberos Ticket, inclusion mode is set to .../IncludeToken/Once</span></span>  
<span data-ttu-id="c7f6d-472">Ochrona tokenu: FAŁSZ</span><span class="sxs-lookup"><span data-stu-id="c7f6d-472">Token Protection: False</span></span>  
  
 <span data-ttu-id="c7f6d-473">Cały podpis nagłówka i treści: prawda</span><span class="sxs-lookup"><span data-stu-id="c7f6d-473">Entire Header And Body Signatures: True</span></span>  
  
 <span data-ttu-id="c7f6d-474">Kolejność ochrony: SignBeforeEncrypt</span><span class="sxs-lookup"><span data-stu-id="c7f6d-474">Protection Order: SignBeforeEncrypt</span></span>  
  
 <span data-ttu-id="c7f6d-475">Szyfruj sygnaturę: prawda</span><span class="sxs-lookup"><span data-stu-id="c7f6d-475">Encrypt Signature: True</span></span>  
  
 <span data-ttu-id="c7f6d-476">Zasady</span><span class="sxs-lookup"><span data-stu-id="c7f6d-476">Policy</span></span>  
  
```xml  
<wsp:Policy wsu:Id='Kerberos_policy' >  
  <wsp:ExactlyOne>  
    <wsp:All>  
      <sp:SymmetricBinding>  
        <wsp:Policy>  
          <sp:ProtectionToken>  
            <wsp:Policy>  
              <sp:KerberosToken sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/Once' >  
                <wsp:Policy>  
                  <sp:RequireDerivedKeys />
                  <sp:WssGssKerberosV5ApReqToken11 />
                </wsp:Policy>  
              </sp:KerberosToken>  
            </wsp:Policy>  
          </sp:ProtectionToken>  
          <sp:AlgorithmSuite>  
            <wsp:Policy>  
              <sp:Basic128 />
            </wsp:Policy>  
          </sp:AlgorithmSuite>  
          <sp:Layout>  
            <wsp:Policy>  
              <sp:Strict />
            </wsp:Policy>  
          </sp:Layout>  
          <sp:IncludeTimestamp />
          <sp:EncryptSignature />
          <sp:OnlySignEntireHeadersAndBody />
        </wsp:Policy>  
      </sp:SymmetricBinding>  
      <sp:Wss11>  
        <wsp:Policy>  
          <sp:MustSupportRefKeyIdentifier />
          <sp:MustSupportRefIssuerSerial />
          <sp:MustSupportRefThumbprint />
          <sp:MustSupportRefEncryptedKey />
        </wsp:Policy>  
      </sp:Wss11>  
      <sp:Trust10>  
        <wsp:Policy>  
          <sp:MustSupportIssuedTokens />
          <sp:RequireClientEntropy />
          <sp:RequireServerEntropy />
        </wsp:Policy>  
      </sp:Trust10>  
      <wsaw:UsingAddressing />
    </wsp:All>  
  </wsp:ExactlyOne>  
</wsp:Policy>  
```  
  
### <a name="security-header-examples-signbeforeencrypt-encryptsignature"></a><span data-ttu-id="c7f6d-477">Przykłady nagłówka zabezpieczeń: SignBeforeEncrypt, EncryptSignature</span><span class="sxs-lookup"><span data-stu-id="c7f6d-477">Security Header Examples: SignBeforeEncrypt, EncryptSignature</span></span>  
 <span data-ttu-id="c7f6d-478">Żądanie</span><span class="sxs-lookup"><span data-stu-id="c7f6d-478">Request</span></span>  
  
```xml  
<wsse:Security s:mustUnderstand="1">  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsse:BinarySecurityToken>  
  ...  
  </wsse:BinarySecurityToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>  
```  
  
 <span data-ttu-id="c7f6d-479">Reakcja</span><span class="sxs-lookup"><span data-stu-id="c7f6d-479">Response</span></span>  
  
```xml  
<wsse:Security s:mustUnderstand="1">  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>
```  
  
### <a name="security-header-examples-encryptbeforesign"></a><span data-ttu-id="c7f6d-480">Przykłady nagłówka zabezpieczeń: EncryptBeforeSign</span><span class="sxs-lookup"><span data-stu-id="c7f6d-480">Security Header Examples: EncryptBeforeSign</span></span>  
 <span data-ttu-id="c7f6d-481">Żądanie</span><span class="sxs-lookup"><span data-stu-id="c7f6d-481">Request</span></span>  
  
```xml  
<wsse:Security>  
TBD  
</wsse:Security>  
```  
  
 <span data-ttu-id="c7f6d-482">Reakcja</span><span class="sxs-lookup"><span data-stu-id="c7f6d-482">Response</span></span>  
  
```xml  
<wsse:Security>  
TBD  
</wsse:Security>  
```  
  
#### <a name="64-issuedtoken"></a><span data-ttu-id="c7f6d-483">6,4 IssuedToken</span><span class="sxs-lookup"><span data-stu-id="c7f6d-483">6.4 IssuedToken</span></span>  
 <span data-ttu-id="c7f6d-484">W tym trybie uwierzytelniania klient nie jest uwierzytelniany w usłudze, w związku z czym klient przedstawia token wystawiony przez usługę STS i udowadnia znajomość klucza współużytkowanego.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-484">With this authentication mode the client does not authenticate to the service, as such, rather the client presents a token issued by an STS and proves knowledge of a shared key.</span></span> <span data-ttu-id="c7f6d-485">Usługa nie jest uwierzytelniana klientowi, w związku z czym w zamian jest szyfrowany klucz współużytkowany jako część wystawionego tokenu, aby tylko usługa mogła odszyfrować klucz.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-485">The service is not authenticated to the client, as such, instead the STS encrypts the shared key as part of the issued token such that only the service can decrypt the key.</span></span> <span data-ttu-id="c7f6d-486">Używane powiązanie jest powiązaniem symetrycznym z następującymi właściwościami:</span><span class="sxs-lookup"><span data-stu-id="c7f6d-486">The binding used is as symmetric binding with the following properties;</span></span>  
  
 <span data-ttu-id="c7f6d-487">Token ochrony: wystawiony token, tryb dołączania ma wartość. ../IncludeToken/AlwaysToRecipient</span><span class="sxs-lookup"><span data-stu-id="c7f6d-487">Protection Token: Issued Token, inclusion mode is set to .../IncludeToken/AlwaysToRecipient</span></span>  
<span data-ttu-id="c7f6d-488">Ochrona tokenu: FAŁSZ</span><span class="sxs-lookup"><span data-stu-id="c7f6d-488">Token Protection: False</span></span>  
  
 <span data-ttu-id="c7f6d-489">Cały podpis nagłówka i treści: prawda</span><span class="sxs-lookup"><span data-stu-id="c7f6d-489">Entire Header And Body Signatures: True</span></span>  
  
 <span data-ttu-id="c7f6d-490">Kolejność ochrony: SignBeforeEncrypt</span><span class="sxs-lookup"><span data-stu-id="c7f6d-490">Protection Order: SignBeforeEncrypt</span></span>  
  
 <span data-ttu-id="c7f6d-491">Szyfruj sygnaturę: prawda</span><span class="sxs-lookup"><span data-stu-id="c7f6d-491">Encrypt Signature: True</span></span>  
  
 <span data-ttu-id="c7f6d-492">Zasady</span><span class="sxs-lookup"><span data-stu-id="c7f6d-492">Policy</span></span>  
  
```xml  
<wsp:Policy wsu:Id='CustomBinding_ISimple3_policy' >  
  <wsp:ExactlyOne>  
    <wsp:All>  
      <sp:SymmetricBinding>  
        <wsp:Policy>  
          <sp:ProtectionToken>  
            <wsp:Policy>  
              <sp:IssuedToken sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/AlwaysToRecipient' >  
                <sp:RequestSecurityTokenTemplate>  
                  <wst:KeyType>  
http://schemas.xmlsoap.org/ws/2005/02/trust/SymmetricKey  
                  </wst:KeyType>
                </sp:RequestSecurityTokenTemplate>  
                <wsp:Policy>  
                  <sp:RequireDerivedKeys />
                  <sp:RequireInternalReference />
                </wsp:Policy>  
              </sp:IssuedToken>  
            </wsp:Policy>  
          </sp:ProtectionToken>  
          <sp:AlgorithmSuite>  
            <wsp:Policy>  
              <sp:Basic256 />
            </wsp:Policy>  
          </sp:AlgorithmSuite>  
          <sp:Layout>  
            <wsp:Policy>  
              <sp:Strict />
            </wsp:Policy>  
          </sp:Layout>  
          <sp:IncludeTimestamp />
          <sp:EncryptSignature />
          <sp:OnlySignEntireHeadersAndBody />
        </wsp:Policy>  
      </sp:SymmetricBinding>  
      <sp:Wss11>  
        <wsp:Policy>  
          <sp:MustSupportRefKeyIdentifier />
          <sp:MustSupportRefIssuerSerial />
          <sp:MustSupportRefThumbprint />
          <sp:MustSupportRefEncryptedKey />
        </wsp:Policy>  
      </sp:Wss11>  
      <sp:Trust10>  
        <wsp:Policy>  
          <sp:MustSupportIssuedTokens />
          <sp:RequireClientEntropy />
          <sp:RequireServerEntropy />
        </wsp:Policy>  
      </sp:Trust10>  
      <wsaw:UsingAddressing />
    </wsp:All>  
  </wsp:ExactlyOne>  
</wsp:Policy>  
```  
  
### <a name="security-header-examples-signbeforeencrypt-encryptsignature"></a><span data-ttu-id="c7f6d-493">Przykłady nagłówka zabezpieczeń: SignBeforeEncrypt, EncryptSignature</span><span class="sxs-lookup"><span data-stu-id="c7f6d-493">Security Header Examples: SignBeforeEncrypt, EncryptSignature</span></span>  
 <span data-ttu-id="c7f6d-494">Żądanie</span><span class="sxs-lookup"><span data-stu-id="c7f6d-494">Request</span></span>  
  
```xml  
<wsse:Security s:mustUnderstand="1">  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <saml:Assertion>  
  ...  
  </saml:Assertion>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>  
```  
  
 <span data-ttu-id="c7f6d-495">Reakcja</span><span class="sxs-lookup"><span data-stu-id="c7f6d-495">Response</span></span>  
  
```xml  
<wsse:Security s:mustUnderstand="1">  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>
```  
  
### <a name="security-header-examples-encryptbeforesign"></a><span data-ttu-id="c7f6d-496">Przykłady nagłówka zabezpieczeń: EncryptBeforeSign</span><span class="sxs-lookup"><span data-stu-id="c7f6d-496">Security Header Examples: EncryptBeforeSign</span></span>  
 <span data-ttu-id="c7f6d-497">Żądanie</span><span class="sxs-lookup"><span data-stu-id="c7f6d-497">Request</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <saml:Assertion>  
  ...  
  </saml:Assertion>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
 <span data-ttu-id="c7f6d-498">Reakcja</span><span class="sxs-lookup"><span data-stu-id="c7f6d-498">Response</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
### <a name="65-using-sslnegotiated-for-service-authentication"></a><span data-ttu-id="c7f6d-499">6,5 użycie SslNegotiated do uwierzytelniania usługi</span><span class="sxs-lookup"><span data-stu-id="c7f6d-499">6.5 Using SslNegotiated for Service Authentication</span></span>  
 <span data-ttu-id="c7f6d-500">W tej sekcji opisano grupę trybów uwierzytelniania, która używa powiązania symetrycznego z tokenem ochrony z tokenem kontekstu zabezpieczeń dla protokołu WS-SecureConversation (WS-SC), którego wartość klucza jest negocjowana przez wykonanie protokołu TLS za pośrednictwem komunikatów typu "WS-Trust" (WS-T) RST/RSTR.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-500">This section describes a group of authentication modes that use a symmetric binding with the protection token being a Security Context Token per WS-SecureConversation (WS-SC) whose key value is negotiated by executing the TLS protocol over WS-Trust (WS-T) RST/RSTR messages.</span></span> <span data-ttu-id="c7f6d-501">Szczegóły implementacji uzgadniania TLS przy użyciu protokołu WS-Trust są opisane w TLSNEGO.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-501">Details of the TLS handshake implementation using WS-Trust are described in TLSNEGO.</span></span> <span data-ttu-id="c7f6d-502">W tym przykładzie w komunikatach przyjęto założenie, że SCT ze skojarzonym kontekstem zabezpieczeń zostanie już ustanowiony za pomocą uzgadniania.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-502">Here in the message examples we will assume that SCT with an associated security context is already established through a handshake.</span></span>  
  
 <span data-ttu-id="c7f6d-503">Używane powiązanie jest powiązaniem symetrycznym z następującymi właściwościami:</span><span class="sxs-lookup"><span data-stu-id="c7f6d-503">The binding used is a symmetric binding with the following properties;</span></span>  
  
 <span data-ttu-id="c7f6d-504">Token ochrony: SslContextToken, tryb dołączania jest ustawiony na. ../IncludeToken/Never</span><span class="sxs-lookup"><span data-stu-id="c7f6d-504">Protection Token: SslContextToken, inclusion mode is set to .../IncludeToken/Never</span></span>  
<span data-ttu-id="c7f6d-505">Ochrona tokenu: FAŁSZ</span><span class="sxs-lookup"><span data-stu-id="c7f6d-505">Token Protection: False</span></span>  
  
 <span data-ttu-id="c7f6d-506">Cały podpis nagłówka i treści: prawda</span><span class="sxs-lookup"><span data-stu-id="c7f6d-506">Entire Header And Body Signatures: True</span></span>  
  
 <span data-ttu-id="c7f6d-507">Kolejność ochrony: SignBeforeEncrypt</span><span class="sxs-lookup"><span data-stu-id="c7f6d-507">Protection Order: SignBeforeEncrypt</span></span>  
  
 <span data-ttu-id="c7f6d-508">Szyfruj sygnaturę: prawda</span><span class="sxs-lookup"><span data-stu-id="c7f6d-508">Encrypt Signature: True</span></span>  
  
#### <a name="651-policy-for-sslnegotiated-service-authentication"></a><span data-ttu-id="c7f6d-509">zasady 6.5.1ymi dla uwierzytelniania usługi SslNegotiated</span><span class="sxs-lookup"><span data-stu-id="c7f6d-509">6.5.1 Policy for SslNegotiated service authentication</span></span>  
 <span data-ttu-id="c7f6d-510">Zasady dla wszystkich trybów uwierzytelniania w tej sekcji są podobne i różnią się tylko przez określone podpisane tokeny obsługujące lub zatwierdzania.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-510">Policy for all authentication modes in this section are similar and differ only by specific signed supporting or endorsing tokens used.</span></span>  
  
```xml  
<wsp:Policy wsu:Id='SslNegotiated_policy' >  
  <wsp:ExactlyOne>  
    <wsp:All>  
      <sp:SymmetricBinding>  
        <wsp:Policy>  
          <sp:ProtectionToken>  
            <wsp:Policy>  
              <mssp:SslContextToken sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/AlwaysToRecipient'>  
                <wsp:Policy>  
                  <sp:RequireDerivedKeys />
                </wsp:Policy>  
              </mssp:SslContextToken>  
            </wsp:Policy>  
          </sp:ProtectionToken>  
          <sp:AlgorithmSuite>  
            <wsp:Policy>  
              <sp:Basic256 />
            </wsp:Policy>  
          </sp:AlgorithmSuite>  
          <sp:Layout>  
            <wsp:Policy>  
              <sp:Strict />
            </wsp:Policy>  
          </sp:Layout>  
          <sp:IncludeTimestamp />
          <sp:EncryptSignature />
          <sp:OnlySignEntireHeadersAndBody />
        </wsp:Policy>  
      </sp:SymmetricBinding>  
      <!-- Supporting token assertions go here -->  
      ..  
      <sp:Wss11>
        <wsp:Policy>  
          <sp:MustSupportRefKeyIdentifier />
          <sp:MustSupportRefIssuerSerial />
          <sp:MustSupportRefThumbprint />
          <sp:MustSupportRefEncryptedKey />
        </wsp:Policy>  
      </sp:Wss11>  
      <sp:Trust10>  
        <wsp:Policy>  
          <sp:MustSupportIssuedTokens />
          <sp:RequireClientEntropy />
          <sp:RequireServerEntropy />
        </wsp:Policy>  
      </sp:Trust10>  
      <wsaw:UsingAddressing />
    </wsp:All>  
  </wsp:ExactlyOne>  
</wsp:Policy>  
```  
  
#### <a name="652-anonymousforsslnegotiated"></a><span data-ttu-id="c7f6d-511">6.5.2 AnonymousForSslNegotiated</span><span class="sxs-lookup"><span data-stu-id="c7f6d-511">6.5.2 AnonymousForSslNegotiated</span></span>  
 <span data-ttu-id="c7f6d-512">W tym trybie uwierzytelniania klient jest anonimowy i usługa jest uwierzytelniana przy użyciu certyfikatu X. 509.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-512">With this authentication mode the client is anonymous and the service is authenticated using an X.509 certificate.</span></span> <span data-ttu-id="c7f6d-513">Użyte powiązanie to wystąpienie powiązania symetrycznego, zgodnie z opisem w 6.5.1 powyżej.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-513">The binding used is an instance of symmetric binding as described in 6.5.1 above.</span></span>  
  
 <span data-ttu-id="c7f6d-514">Zasady</span><span class="sxs-lookup"><span data-stu-id="c7f6d-514">Policy</span></span>  
  
 <span data-ttu-id="c7f6d-515">Aby uzyskać szczegółowe informacje dotyczące powiązań, zobacz zasady w 6.5.1 powyżej.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-515">See Policy in 6.5.1 above for binding details.</span></span>  
  
### <a name="security-header-examples-signbeforeencrypt-encryptsignature"></a><span data-ttu-id="c7f6d-516">Przykłady nagłówka zabezpieczeń: SignBeforeEncrypt, EncryptSignature</span><span class="sxs-lookup"><span data-stu-id="c7f6d-516">Security Header Examples: SignBeforeEncrypt, EncryptSignature</span></span>  
 <span data-ttu-id="c7f6d-517">Żądanie</span><span class="sxs-lookup"><span data-stu-id="c7f6d-517">Request</span></span>  
  
```xml  
<wsse:Security s:mustUnderstand="1">  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:SecurityContextToken>  
  ...  
  </wsc:SecurityContextToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>  
```  
  
 <span data-ttu-id="c7f6d-518">Reakcja</span><span class="sxs-lookup"><span data-stu-id="c7f6d-518">Response</span></span>  
  
```xml  
<wsse:Security s:mustUnderstand="1">  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>
```  
  
### <a name="security-header-examples-encryptbeforesign"></a><span data-ttu-id="c7f6d-519">Przykłady nagłówka zabezpieczeń: EncryptBeforeSign</span><span class="sxs-lookup"><span data-stu-id="c7f6d-519">Security Header Examples: EncryptBeforeSign</span></span>  
 <span data-ttu-id="c7f6d-520">Żądanie</span><span class="sxs-lookup"><span data-stu-id="c7f6d-520">Request</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:SecurityContextToken>  
  ...  
  </wsc:SecurityContextToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
 <span data-ttu-id="c7f6d-521">Reakcja</span><span class="sxs-lookup"><span data-stu-id="c7f6d-521">Response</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
#### <a name="653-usernameforsslnegotiated"></a><span data-ttu-id="c7f6d-522">6.5.3 UserNameForSslNegotiated</span><span class="sxs-lookup"><span data-stu-id="c7f6d-522">6.5.3 UserNameForSslNegotiated</span></span>  
 <span data-ttu-id="c7f6d-523">W tym trybie uwierzytelniania klient jest uwierzytelniany przy użyciu tokenu nazwy użytkownika, który jest wyświetlany na warstwie protokołu SOAP jako podpisanego tokenu pomocniczego.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-523">With this authentication mode the client is authenticates using a Username Token which appears at the SOAP layer as a signed supporting token.</span></span> <span data-ttu-id="c7f6d-524">Usługa jest uwierzytelniana przy użyciu certyfikatu X. 509.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-524">The service is authenticated using an X.509 certificate.</span></span> <span data-ttu-id="c7f6d-525">Użyte powiązanie to wystąpienie powiązania symetrycznego, zgodnie z opisem w 6.5.1.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-525">The binding used is an instance of symmetric binding as described in 6.5.1.</span></span>  
  
 <span data-ttu-id="c7f6d-526">Zasady</span><span class="sxs-lookup"><span data-stu-id="c7f6d-526">Policy</span></span>  
  
 <span data-ttu-id="c7f6d-527">Szczegóły powiązania można znaleźć w sekcji 6.5.1 powyżej</span><span class="sxs-lookup"><span data-stu-id="c7f6d-527">See section 6.5.1 above for binding details</span></span>  
  
 <span data-ttu-id="c7f6d-528">Podpisany token pomocniczy</span><span class="sxs-lookup"><span data-stu-id="c7f6d-528">Signed Supporting Token</span></span>  
  
```xml  
<sp:SignedSupportingTokens>  
  <wsp:Policy>  
    <sp:UsernameToken sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/AlwaysToRecipient' >  
      <wsp:Policy>  
        <sp:WssUsernameToken10 />
      </wsp:Policy>  
    </sp:UsernameToken>  
  </wsp:Policy>  
</sp:SignedSupportingTokens>  
```  
  
### <a name="security-header-examples-signbeforeencrypt-encryptsignature"></a><span data-ttu-id="c7f6d-529">Przykłady nagłówka zabezpieczeń: SignBeforeEncrypt, EncryptSignature</span><span class="sxs-lookup"><span data-stu-id="c7f6d-529">Security Header Examples: SignBeforeEncrypt, EncryptSignature</span></span>  
 <span data-ttu-id="c7f6d-530">Żądanie</span><span class="sxs-lookup"><span data-stu-id="c7f6d-530">Request</span></span>  
  
```xml  
<wsse:Security s:mustUnderstand="1">  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:SecurityContextToken>  
  ...  
  </wsc:SecurityContextToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>  
```  
  
 <span data-ttu-id="c7f6d-531">Reakcja</span><span class="sxs-lookup"><span data-stu-id="c7f6d-531">Response</span></span>  
  
```xml  
<wsse:Security s:mustUnderstand="1">  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>
```  
  
### <a name="security-header-examples-encryptbeforesign"></a><span data-ttu-id="c7f6d-532">Przykłady nagłówka zabezpieczeń: EncryptBeforeSign</span><span class="sxs-lookup"><span data-stu-id="c7f6d-532">Security Header Examples: EncryptBeforeSign</span></span>  
 <span data-ttu-id="c7f6d-533">Żądanie</span><span class="sxs-lookup"><span data-stu-id="c7f6d-533">Request</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:SecurityContextToken>  
  ...  
  </wsc:SecurityContextToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
 <span data-ttu-id="c7f6d-534">Reakcja</span><span class="sxs-lookup"><span data-stu-id="c7f6d-534">Response</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
#### <a name="654-issuedtokenforsslnegotiated"></a><span data-ttu-id="c7f6d-535">6.5.4 IssuedTokenForSslNegotiated</span><span class="sxs-lookup"><span data-stu-id="c7f6d-535">6.5.4 IssuedTokenForSslNegotiated</span></span>  
 <span data-ttu-id="c7f6d-536">W tym trybie uwierzytelniania klient nie jest uwierzytelniany w usłudze w taki sposób, ale przedstawia token wystawiony przez usługę STS i udowadnia znajomość klucza współużytkowanego.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-536">With this authentication mode the client does not authenticate to the service, as such, but instead presents a token issued by an STS and proves knowledge of a shared key.</span></span> <span data-ttu-id="c7f6d-537">Wystawiony token pojawia się na warstwie protokołu SOAP jako token pomocniczy.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-537">The issued token appears at the SOAP layer as an endorsing supporting token.</span></span> <span data-ttu-id="c7f6d-538">Usługa jest uwierzytelniana przy użyciu certyfikatu X. 509.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-538">The service is authenticated using an X.509 certificate.</span></span> <span data-ttu-id="c7f6d-539">Użyte powiązanie to wystąpienie powiązania symetrycznego, zgodnie z opisem w 6.5.1 powyżej.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-539">The binding used is an instance of symmetric binding as described in 6.5.1 above.</span></span>  
  
 <span data-ttu-id="c7f6d-540">Zasady</span><span class="sxs-lookup"><span data-stu-id="c7f6d-540">Policy</span></span>  
  
 <span data-ttu-id="c7f6d-541">Szczegóły powiązania można znaleźć w sekcji 6.5.1 powyżej</span><span class="sxs-lookup"><span data-stu-id="c7f6d-541">See section 6.5.1 above for binding details</span></span>  
  
 <span data-ttu-id="c7f6d-542">Zatwierdzanie tokenu pomocniczego</span><span class="sxs-lookup"><span data-stu-id="c7f6d-542">Endorsing Supporting Token</span></span>  
  
```xml  
<sp:EndorsingSupportingTokens>  
  <wsp:Policy>  
    <sp:IssuedToken sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/AlwaysToRecipient' >  
      <sp:RequestSecurityTokenTemplate>  
        <wst:KeyType>  
http://schemas.xmlsoap.org/ws/2005/02/trust/SymmetricKey  
        </wst:KeyType>
      </sp:RequestSecurityTokenTemplate>  
      <wsp:Policy>  
        <sp:RequireDerivedKeys />
        <sp:RequireInternalReference />
      </wsp:Policy>  
    </sp:IssuedToken>  
  </wsp:Policy>  
</sp:EndorsingSupportingTokens>  
```  
  
### <a name="security-header-examples-signbeforeencrypt-encryptsignature"></a><span data-ttu-id="c7f6d-543">Przykłady nagłówka zabezpieczeń: SignBeforeEncrypt, EncryptSignature</span><span class="sxs-lookup"><span data-stu-id="c7f6d-543">Security Header Examples: SignBeforeEncrypt, EncryptSignature</span></span>  
 <span data-ttu-id="c7f6d-544">Żądanie</span><span class="sxs-lookup"><span data-stu-id="c7f6d-544">Request</span></span>  
  
```xml  
<wsse:Security s:mustUnderstand="1">  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:SecurityContextToken>  
  ...  
  </wsc:SecurityContextToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <saml:Assertion>  
  ...  
  </saml:Assertion>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>  
```  
  
 <span data-ttu-id="c7f6d-545">Reakcja</span><span class="sxs-lookup"><span data-stu-id="c7f6d-545">Response</span></span>  
  
```xml  
<wsse:Security s:mustUnderstand="1">  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>
```  
  
### <a name="security-header-examples-encryptbeforesign"></a><span data-ttu-id="c7f6d-546">Przykłady nagłówka zabezpieczeń: EncryptBeforeSign</span><span class="sxs-lookup"><span data-stu-id="c7f6d-546">Security Header Examples: EncryptBeforeSign</span></span>  
 <span data-ttu-id="c7f6d-547">Żądanie</span><span class="sxs-lookup"><span data-stu-id="c7f6d-547">Request</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:SecurityContextToken>  
  ...  
  </wsc:SecurityContextToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <saml:Assertion>  
  ...  
  </saml:Assertion>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
 <span data-ttu-id="c7f6d-548">Reakcja</span><span class="sxs-lookup"><span data-stu-id="c7f6d-548">Response</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsse11:SignatureConfirmation />  
  <wsse11:SignatureConfirmation />  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
#### <a name="655-mutualsslnegotiated"></a><span data-ttu-id="c7f6d-549">6.5.5 MutualSslNegotiated</span><span class="sxs-lookup"><span data-stu-id="c7f6d-549">6.5.5 MutualSslNegotiated</span></span>  
 <span data-ttu-id="c7f6d-550">W tym trybie uwierzytelniania klient i usługa uwierzytelniają się za pomocą certyfikatów X. 509.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-550">With this authentication mode the client and the service authenticate using X.509 certificates.</span></span> <span data-ttu-id="c7f6d-551">Użyte powiązanie to wystąpienie powiązania symetrycznego, zgodnie z opisem w 6.5.1 powyżej.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-551">The binding used is an instance of symmetric binding as described in 6.5.1 above.</span></span>  
  
 <span data-ttu-id="c7f6d-552">Zasady</span><span class="sxs-lookup"><span data-stu-id="c7f6d-552">Policy</span></span>  
  
 <span data-ttu-id="c7f6d-553">Szczegóły powiązania można znaleźć w sekcji 6.5.1 powyżej</span><span class="sxs-lookup"><span data-stu-id="c7f6d-553">See section 6.5.1 above for binding details</span></span>  
  
 <span data-ttu-id="c7f6d-554">Zatwierdzanie tokenu pomocniczego</span><span class="sxs-lookup"><span data-stu-id="c7f6d-554">Endorsing Supporting Token</span></span>  
  
```xml  
<sp:EndorsingSupportingTokens>  
  <wsp:Policy>  
    <sp:X509Token sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/AlwaysToRecipient' >  
      <wsp:Policy>  
        <sp:RequireThumbprintReference />
        <sp:WssX509V3Token10 />
      </wsp:Policy>  
    </sp:X509Token>  
  </wsp:Policy>  
</sp:EndorsingSupportingTokens>  
```  
  
### <a name="security-header-examples-signbeforeencrypt-encryptsignature"></a><span data-ttu-id="c7f6d-555">Przykłady nagłówka zabezpieczeń: SignBeforeEncrypt, EncryptSignature</span><span class="sxs-lookup"><span data-stu-id="c7f6d-555">Security Header Examples: SignBeforeEncrypt, EncryptSignature</span></span>  
 <span data-ttu-id="c7f6d-556">Żądanie</span><span class="sxs-lookup"><span data-stu-id="c7f6d-556">Request</span></span>  
  
```xml  
<wsse:Security s:mustUnderstand="1">  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:SecurityContextToken>  
  ...  
  </wsc:SecurityContextToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>  
```  
  
 <span data-ttu-id="c7f6d-557">Reakcja</span><span class="sxs-lookup"><span data-stu-id="c7f6d-557">Response</span></span>  
  
```xml  
<wsse:Security s:mustUnderstand="1">  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>
```  
  
### <a name="security-header-examples-encryptbeforesign"></a><span data-ttu-id="c7f6d-558">Przykłady nagłówka zabezpieczeń: EncryptBeforeSign</span><span class="sxs-lookup"><span data-stu-id="c7f6d-558">Security Header Examples: EncryptBeforeSign</span></span>  
 <span data-ttu-id="c7f6d-559">Żądanie</span><span class="sxs-lookup"><span data-stu-id="c7f6d-559">Request</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:SecurityContextToken>  
  ...  
  </wsc:SecurityContextToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
 <span data-ttu-id="c7f6d-560">Reakcja</span><span class="sxs-lookup"><span data-stu-id="c7f6d-560">Response</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
### <a name="66-sspinegotiated"></a><span data-ttu-id="c7f6d-561">6,6 SspiNegotiated</span><span class="sxs-lookup"><span data-stu-id="c7f6d-561">6.6 SspiNegotiated</span></span>  
 <span data-ttu-id="c7f6d-562">Przy użyciu tego trybu uwierzytelniania protokół negocjacji jest używany do uwierzytelniania klientów i serwerów.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-562">With this authentication mode a negotiation protocol is used to perform client and server authentication.</span></span> <span data-ttu-id="c7f6d-563">Protokół Kerberos jest używany, jeśli jest to możliwe, w przeciwnym razie NTLM.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-563">Kerberos is used if possible, otherwise NTLM.</span></span> <span data-ttu-id="c7f6d-564">Używane powiązanie jest powiązaniem symetrycznym z następującymi właściwościami:</span><span class="sxs-lookup"><span data-stu-id="c7f6d-564">The binding used is a symmetric binding with the following properties;</span></span>  
  
 <span data-ttu-id="c7f6d-565">Token ochrony: SpnegoContextToken, tryb dołączania jest ustawiony na. ../IncludeToken/AlwaysToRecipient</span><span class="sxs-lookup"><span data-stu-id="c7f6d-565">Protection Token: SpnegoContextToken, inclusion mode is set to .../IncludeToken/AlwaysToRecipient</span></span>  
<span data-ttu-id="c7f6d-566">Ochrona tokenu: FAŁSZ</span><span class="sxs-lookup"><span data-stu-id="c7f6d-566">Token Protection: False</span></span>  
  
 <span data-ttu-id="c7f6d-567">Cały podpis nagłówka i treści: prawda</span><span class="sxs-lookup"><span data-stu-id="c7f6d-567">Entire Header And Body Signatures: True</span></span>  
  
 <span data-ttu-id="c7f6d-568">Kolejność ochrony: SignBeforeEncrypt</span><span class="sxs-lookup"><span data-stu-id="c7f6d-568">Protection Order: SignBeforeEncrypt</span></span>  
  
 <span data-ttu-id="c7f6d-569">Szyfruj sygnaturę: prawda</span><span class="sxs-lookup"><span data-stu-id="c7f6d-569">Encrypt Signature: True</span></span>  
  
 <span data-ttu-id="c7f6d-570">Zasady</span><span class="sxs-lookup"><span data-stu-id="c7f6d-570">Policy</span></span>  
  
```xml  
<wsp:Policy wsu:Id='CustomBinding_ISimple13_policy' >  
  <wsp:ExactlyOne>  
    <wsp:All>  
      <sp:SymmetricBinding>  
        <wsp:Policy>  
          <sp:ProtectionToken>  
            <wsp:Policy>  
              <sp:SpnegoContextToken sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/AlwaysToRecipient' >  
                <wsp:Policy>  
                  <sp:RequireDerivedKeys />
                </wsp:Policy>  
              </sp:SpnegoContextToken>  
            </wsp:Policy>  
          </sp:ProtectionToken>  
          <sp:AlgorithmSuite>  
            <wsp:Policy>  
              <sp:Basic256 />
            </wsp:Policy>  
          </sp:AlgorithmSuite>  
          <sp:Layout>  
            <wsp:Policy>  
              <sp:Strict />
            </wsp:Policy>  
          </sp:Layout>  
          <sp:IncludeTimestamp />
          <sp:EncryptSignature />
          <sp:OnlySignEntireHeadersAndBody />
        </wsp:Policy>  
      </sp:SymmetricBinding>  
      <sp:Wss11>  
        <wsp:Policy>  
          <sp:MustSupportRefKeyIdentifier />
          <sp:MustSupportRefIssuerSerial />
          <sp:MustSupportRefThumbprint />
          <sp:MustSupportRefEncryptedKey />
        </wsp:Policy>  
      </sp:Wss11>  
      <sp:Trust10>  
        <wsp:Policy>  
          <sp:MustSupportIssuedTokens />
          <sp:RequireClientEntropy />
          <sp:RequireServerEntropy />
        </wsp:Policy>  
      </sp:Trust10>  
      <wsaw:UsingAddressing />
    </wsp:All>  
  </wsp:ExactlyOne>  
</wsp:Policy>  
```  
  
### <a name="security-header-examples-signbeforeencrypt-encryptsignature"></a><span data-ttu-id="c7f6d-571">Przykłady nagłówka zabezpieczeń: SignBeforeEncrypt, EncryptSignature</span><span class="sxs-lookup"><span data-stu-id="c7f6d-571">Security Header Examples: SignBeforeEncrypt, EncryptSignature</span></span>  
 <span data-ttu-id="c7f6d-572">Żądanie</span><span class="sxs-lookup"><span data-stu-id="c7f6d-572">Request</span></span>  
  
```xml  
<wsse:Security s:mustUnderstand="1">  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:SecurityContextToken>  
  ...  
  </wsc:SecurityContextToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>  
```  
  
 <span data-ttu-id="c7f6d-573">Reakcja</span><span class="sxs-lookup"><span data-stu-id="c7f6d-573">Response</span></span>  
  
```xml  
<wsse:Security s:mustUnderstand="1">  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>
```  
  
### <a name="security-header-examples-encryptbeforesign"></a><span data-ttu-id="c7f6d-574">Przykłady nagłówka zabezpieczeń: EncryptBeforeSign</span><span class="sxs-lookup"><span data-stu-id="c7f6d-574">Security Header Examples: EncryptBeforeSign</span></span>  
 <span data-ttu-id="c7f6d-575">Żądanie</span><span class="sxs-lookup"><span data-stu-id="c7f6d-575">Request</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:SecurityContextToken>  
  ...  
  </wsc:SecurityContextToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
 <span data-ttu-id="c7f6d-576">Reakcja</span><span class="sxs-lookup"><span data-stu-id="c7f6d-576">Response</span></span>  
  
```xml  
<wsse:Security>  
<wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
### <a name="67-secureconversation"></a><span data-ttu-id="c7f6d-577">6,7 SecureConversation</span><span class="sxs-lookup"><span data-stu-id="c7f6d-577">6.7 SecureConversation</span></span>  
 <span data-ttu-id="c7f6d-578">Używane powiązanie jest powiązaniem symetrycznym z tokenem ochrony, który jest SCT dla WS-SecureConversation (WS-SC).</span><span class="sxs-lookup"><span data-stu-id="c7f6d-578">The binding used is a symmetric binding with the protection token being a SCT per WS-SecureConversation (WS-SC).</span></span> <span data-ttu-id="c7f6d-579">SCT jest negocjowany przy użyciu protokołu WS-Trust (WS-Trust) lub WS-SecureConversation (WS-SC) zgodnie z zagnieżdżonym powiązaniem, które jest samym powiązaniem symetrycznym korzystającym z protokołu negocjacji.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-579">The SCT is negotiated using WS-Trust (WS-Trust) or WS-SecureConversation (WS-SC) according to a nested binding, which is itself a symmetric binding that uses a negotiation protocol.</span></span> <span data-ttu-id="c7f6d-580">Protokół negocjacji użyje protokołu Kerberos do przeprowadzenia uwierzytelniania klienta i serwera, o ile jest to możliwe.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-580">The negotiation protocol will use Kerberos to perform client and server authentication if possible.</span></span> <span data-ttu-id="c7f6d-581">Jeśli nie można użyć protokołu Kerberos, nastąpi powrót do NTLM.</span><span class="sxs-lookup"><span data-stu-id="c7f6d-581">If Kerberos cannot be used, it will fall back to NTLM.</span></span>  
  
 <span data-ttu-id="c7f6d-582">Zasady</span><span class="sxs-lookup"><span data-stu-id="c7f6d-582">Policy</span></span>  
  
```xml  
<wsp:Policy wsu:Id='SecureConversation_policy' >  
  <wsp:ExactlyOne>  
    <wsp:All>  
      <sp:SymmetricBinding>  
        <wsp:Policy>  
          <sp:ProtectionToken>  
            <wsp:Policy>  
              <sp:SecureConversationToken sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/AlwaysToRecipient' >  
                <wsp:Policy>  
                  <sp:RequireDerivedKeys />
                  <sp:BootstrapPolicy>  
                    <wsp:Policy>  
                      <sp:SignedParts>  
                        <sp:Body />
                        <sp:Header Name='To' Namespace='http://www.w3.org/2005/08/addressing' />
                        <sp:Header Name='From' Namespace='http://www.w3.org/2005/08/addressing' />
                        <sp:Header Name='FaultTo' Namespace='http://www.w3.org/2005/08/addressing' />
                        <sp:Header Name='ReplyTo' Namespace='http://www.w3.org/2005/08/addressing' />
                        <sp:Header Name='MessageID' Namespace='http://www.w3.org/2005/08/addressing' />
                        <sp:Header Name='RelatesTo' Namespace='http://www.w3.org/2005/08/addressing' />
                        <sp:Header Name='Action' Namespace='http://www.w3.org/2005/08/addressing' />
                      </sp:SignedParts>  
                      <sp:EncryptedParts>  
                        <sp:Body />
                      </sp:EncryptedParts>  
                      <sp:SymmetricBinding>  
                        <wsp:Policy>  
                          <sp:ProtectionToken>  
                            <wsp:Policy>  
                              <sp:SpnegoContextToken sp:IncludeToken='http://schemas.xmlsoap.org/ws/2005/07/securitypolicy/IncludeToken/AlwaysToRecipient' >  
                                <wsp:Policy>  
                                  <sp:RequireDerivedKeys />
                                </wsp:Policy>  
                              </sp:SpnegoContextToken>  
                            </wsp:Policy>  
                          </sp:ProtectionToken>  
                          <sp:AlgorithmSuite>  
                            <wsp:Policy>  
                              <sp:Basic256 />
                            </wsp:Policy>  
                          </sp:AlgorithmSuite>  
                          <sp:Layout>  
                            <wsp:Policy>  
                              <sp:Strict />
                            </wsp:Policy>  
                          </sp:Layout>  
                          <sp:IncludeTimestamp />
                          <sp:EncryptSignature />
                          <sp:OnlySignEntireHeadersAndBody />
                        </wsp:Policy>  
                      </sp:SymmetricBinding>  
                      <sp:Wss11>  
                        <wsp:Policy>  
                          <sp:MustSupportRefKeyIdentifier />
                          <sp:MustSupportRefIssuerSerial />
                          <sp:MustSupportRefThumbprint />
                          <sp:MustSupportRefEncryptedKey />
                        </wsp:Policy>  
                      </sp:Wss11>  
                      <sp:Trust10>  
                        <wsp:Policy>  
                          <sp:MustSupportIssuedTokens />
                          <sp:RequireClientEntropy />
                          <sp:RequireServerEntropy />
                        </wsp:Policy>  
                      </sp:Trust10>  
                    </wsp:Policy>  
                  </sp:BootstrapPolicy>  
                </wsp:Policy>  
              </sp:SecureConversationToken>  
            </wsp:Policy>  
          </sp:ProtectionToken>  
          <sp:AlgorithmSuite>  
            <wsp:Policy>  
              <sp:Basic256 />
            </wsp:Policy>  
          </sp:AlgorithmSuite>  
          <sp:Layout>  
            <wsp:Policy>  
              <sp:Strict />
            </wsp:Policy>  
          </sp:Layout>  
          <sp:IncludeTimestamp />
          <sp:EncryptSignature />
          <sp:OnlySignEntireHeadersAndBody />
        </wsp:Policy>  
      </sp:SymmetricBinding>  
      <sp:Wss11>  
        <wsp:Policy>  
          <sp:MustSupportRefKeyIdentifier />
          <sp:MustSupportRefIssuerSerial />
          <sp:MustSupportRefThumbprint />
          <sp:MustSupportRefEncryptedKey />
        </wsp:Policy>  
      </sp:Wss11>  
      <sp:Trust10>  
        <wsp:Policy>  
          <sp:MustSupportIssuedTokens />
          <sp:RequireClientEntropy />
          <sp:RequireServerEntropy />
        </wsp:Policy>  
      </sp:Trust10>  
      <wsaw:UsingAddressing />
    </wsp:All>  
  </wsp:ExactlyOne>  
</wsp:Policy>  
```  
  
### <a name="security-header-examples-signbeforeencrypt-encryptsignature"></a><span data-ttu-id="c7f6d-583">Przykłady nagłówka zabezpieczeń: SignBeforeEncrypt, EncryptSignature</span><span class="sxs-lookup"><span data-stu-id="c7f6d-583">Security Header Examples: SignBeforeEncrypt, EncryptSignature</span></span>  
 <span data-ttu-id="c7f6d-584">Żądanie</span><span class="sxs-lookup"><span data-stu-id="c7f6d-584">Request</span></span>  
  
```xml  
<wsse:Security s:mustUnderstand="1">  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:SecurityContextToken>  
  ...  
  </wsc:SecurityContextToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>  
```  
  
 <span data-ttu-id="c7f6d-585">Reakcja</span><span class="sxs-lookup"><span data-stu-id="c7f6d-585">Response</span></span>  
  
```xml  
<wsse:Security s:mustUnderstand="1">  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
  <xenc:EncryptedData>  
  ...  
  </xenc:EncryptedData>  
</wsse:Security>
```  
  
### <a name="security-header-examples-encryptbeforesign"></a><span data-ttu-id="c7f6d-586">Przykłady nagłówka zabezpieczeń: EncryptBeforeSign</span><span class="sxs-lookup"><span data-stu-id="c7f6d-586">Security Header Examples: EncryptBeforeSign</span></span>  
 <span data-ttu-id="c7f6d-587">Żądanie</span><span class="sxs-lookup"><span data-stu-id="c7f6d-587">Request</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:SecurityContextToken>  
  ...  
  </wsc:SecurityContextToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```  
  
 <span data-ttu-id="c7f6d-588">Reakcja</span><span class="sxs-lookup"><span data-stu-id="c7f6d-588">Response</span></span>  
  
```xml  
<wsse:Security>  
  <wsu:Timestamp>  
  ...  
  </wsu:Timestamp>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <wsc:DerivedKeyToken>  
  ...  
  </wsc:DerivedKeyToken>  
  <ds:Signature>  
  ...  
  </ds:Signature>  
  <xenc:ReferenceList>  
  ...  
  </xenc:ReferenceList>  
</wsse:Security>  
```
