---
title: Zabezpieczenia programu WCF (Windows Communication Foundation)
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Communication Foundation, programming
- security [WCF]
- Windows Communication Foundation, security
ms.assetid: 7ea87fcb-dcfb-4a4a-8b03-6b954575d45b
ms.openlocfilehash: b92f1ad8bb00e9df8daf55da4d7a808420d909cf
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96254002"
---
# <a name="windows-communication-foundation-security"></a><span data-ttu-id="03210-102">Zabezpieczenia programu WCF (Windows Communication Foundation)</span><span class="sxs-lookup"><span data-stu-id="03210-102">Windows Communication Foundation Security</span></span>

<span data-ttu-id="03210-103">W tematach w tej sekcji opisano funkcje zabezpieczeń Windows Communication Foundation (WCF) i sposoby ich używania w celu zabezpieczania komunikatów.</span><span class="sxs-lookup"><span data-stu-id="03210-103">The topics in this section describe Windows Communication Foundation (WCF) security features and how to use them to help secure messages.</span></span>  
  
 <span data-ttu-id="03210-104">Aby uzyskać więcej informacji na temat systemu Windows Server AppFabric i zabezpieczeń, zobacz [model zabezpieczeń dla systemu Windows Server AppFabric](/previous-versions/appfabric/ee677202(v=azure.10)) .</span><span class="sxs-lookup"><span data-stu-id="03210-104">For more information about Windows Server AppFabric and security, see [Security Model for Windows Server AppFabric](/previous-versions/appfabric/ee677202(v=azure.10))</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="03210-105">W tej sekcji</span><span class="sxs-lookup"><span data-stu-id="03210-105">In This Section</span></span>  

 [<span data-ttu-id="03210-106">Przegląd zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="03210-106">Security Overview</span></span>](security-overview.md)  
 <span data-ttu-id="03210-107">Opisuje funkcje zabezpieczeń w programie WCF.</span><span class="sxs-lookup"><span data-stu-id="03210-107">Describes the security features in WCF.</span></span>  
  
 [<span data-ttu-id="03210-108">Pojęcia dotyczące zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="03210-108">Security Concepts</span></span>](security-concepts.md)  
 <span data-ttu-id="03210-109">Opisuje podstawową terminologię i koncepcje używane w zabezpieczeniach WCF.</span><span class="sxs-lookup"><span data-stu-id="03210-109">Describes the basic terminology and concepts used in WCF security.</span></span>  
  
 [<span data-ttu-id="03210-110">Typowe scenariusze zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="03210-110">Common Security Scenarios</span></span>](common-security-scenarios.md)  
 <span data-ttu-id="03210-111">Opisuje scenariusze i topologie, które można skonfigurować za pomocą programu WCF.</span><span class="sxs-lookup"><span data-stu-id="03210-111">Describes scenarios and topologies you can configure with WCF.</span></span>  
  
 [<span data-ttu-id="03210-112">Zachowania zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="03210-112">Security Behaviors</span></span>](security-behaviors-in-wcf.md)  
 <span data-ttu-id="03210-113">Zawiera omówienie zachowań WCF wpływających na bezpieczeństwo, takich jak Ustawianie poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="03210-113">Provides an overview of WCF behaviors that affect security, such as setting credentials.</span></span>  
  
 [<span data-ttu-id="03210-114">Wiązania i zabezpieczenia</span><span class="sxs-lookup"><span data-stu-id="03210-114">Bindings and Security</span></span>](bindings-and-security.md)  
 <span data-ttu-id="03210-115">Widok zorientowany na zabezpieczenia powiązań, w tym tematy pokazujące sposób tworzenia niestandardowych powiązań zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="03210-115">A security-oriented view of the bindings, including topics that demonstrate how to create custom security bindings.</span></span>  
  
 [<span data-ttu-id="03210-116">Zabezpieczanie usług i klientów</span><span class="sxs-lookup"><span data-stu-id="03210-116">Securing Services and Clients</span></span>](securing-services-and-clients.md)  
 <span data-ttu-id="03210-117">Opisuje sposób zabezpieczania komunikatów przy użyciu funkcji zabezpieczeń WCF.</span><span class="sxs-lookup"><span data-stu-id="03210-117">Describes how to secure messages using WCF security features.</span></span>  
  
 [<span data-ttu-id="03210-118">Authentication</span><span class="sxs-lookup"><span data-stu-id="03210-118">Authentication</span></span>](authentication-in-wcf.md)  
 <span data-ttu-id="03210-119">Demonstruje typowe zadania związane z uwierzytelnianiem.</span><span class="sxs-lookup"><span data-stu-id="03210-119">Demonstrates common authentication tasks.</span></span>  
  
 [<span data-ttu-id="03210-120">Autoryzacja</span><span class="sxs-lookup"><span data-stu-id="03210-120">Authorization</span></span>](authorization-in-wcf.md)  
 <span data-ttu-id="03210-121">Opisuje typowe scenariusze autoryzacji z implementacjami zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="03210-121">Describes common authorization scenarios with security implementations.</span></span>  
  
 [<span data-ttu-id="03210-122">Federacja i wystawione tokeny</span><span class="sxs-lookup"><span data-stu-id="03210-122">Federation and Issued Tokens</span></span>](federation-and-issued-tokens.md)  
 <span data-ttu-id="03210-123">Opisuje podstawy Federacji oraz sposób tworzenia klientów komunikujących się z serwerami federacyjnymi.</span><span class="sxs-lookup"><span data-stu-id="03210-123">Describes the basics of federation and how to create clients that communicate with federated servers.</span></span>  
  
 [<span data-ttu-id="03210-124">Zaufanie częściowe</span><span class="sxs-lookup"><span data-stu-id="03210-124">Partial Trust</span></span>](partial-trust.md)  
 <span data-ttu-id="03210-125">Opisuje, jak uruchamiać częściowo zaufane scenariusze i ograniczenia programu WCF w przypadku uruchamiania częściowo zaufanych.</span><span class="sxs-lookup"><span data-stu-id="03210-125">Describes how to run partially-trusted scenarios and WCF limitations when running partially trusted.</span></span>  
  
 [<span data-ttu-id="03210-126">Inspekcja</span><span class="sxs-lookup"><span data-stu-id="03210-126">Auditing</span></span>](auditing-security-events.md)  
 <span data-ttu-id="03210-127">Opisuje sposób inspekcji zdarzeń zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="03210-127">Describes how to audit security events.</span></span>  
  
 [<span data-ttu-id="03210-128">Wytyczne dotyczące zabezpieczeń i najlepsze rozwiązania</span><span class="sxs-lookup"><span data-stu-id="03210-128">Security Guidance and Best Practices</span></span>](security-guidance-and-best-practices.md)  
 <span data-ttu-id="03210-129">Wskazówki dotyczące tworzenia bezpiecznych aplikacji WCF.</span><span class="sxs-lookup"><span data-stu-id="03210-129">Guidelines for creating secure WCF applications.</span></span>  
  
## <a name="reference"></a><span data-ttu-id="03210-130">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="03210-130">Reference</span></span>  

 <xref:System.ServiceModel>  
  
 <xref:System.ServiceModel.Security>  
  
## <a name="related-sections"></a><span data-ttu-id="03210-131">Sekcje pokrewne</span><span class="sxs-lookup"><span data-stu-id="03210-131">Related Sections</span></span>  

 [<span data-ttu-id="03210-132">Szczegóły funkcji WCF</span><span class="sxs-lookup"><span data-stu-id="03210-132">WCF Feature Details</span></span>](index.md)  
  
 [<span data-ttu-id="03210-133">Podstawy programowania przy użyciu programu WCF</span><span class="sxs-lookup"><span data-stu-id="03210-133">Basic WCF Programming</span></span>](../basic-wcf-programming.md)  
  
 [<span data-ttu-id="03210-134">Wprowadzenie — samouczek</span><span class="sxs-lookup"><span data-stu-id="03210-134">Getting Started Tutorial</span></span>](../getting-started-tutorial.md)  
  
 [<span data-ttu-id="03210-135">Omówienie pojęć</span><span class="sxs-lookup"><span data-stu-id="03210-135">Conceptual Overview</span></span>](../conceptual-overview.md)  
  
## <a name="see-also"></a><span data-ttu-id="03210-136">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="03210-136">See also</span></span>

- [<span data-ttu-id="03210-137">Konfigurowanie własnej aplikacji</span><span class="sxs-lookup"><span data-stu-id="03210-137">Configuring Your Application</span></span>](../diagnostics/configuring-your-application.md)
