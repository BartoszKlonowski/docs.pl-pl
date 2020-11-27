---
title: Podstawowy cykl życia programowania
description: Dowiedz się więcej o zadaniach służących do tworzenia aplikacji WCF. Funkcja WCF umożliwia aplikacjom komunikowanie się na tym samym komputerze, w sieciach lub na różnych platformach aplikacji.
ms.date: 03/30/2017
helpviewer_keywords:
- service creation [WCF]
ms.assetid: 7cf21bfe-23bd-46aa-8033-609f851dbf76
ms.openlocfilehash: f958bd06f617a5648b31332ebe9e7662d45cd241
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96294849"
---
# <a name="basic-programming-lifecycle"></a><span data-ttu-id="a8a07-104">Podstawowy cykl życia programowania</span><span class="sxs-lookup"><span data-stu-id="a8a07-104">Basic Programming Lifecycle</span></span>

<span data-ttu-id="a8a07-105">Windows Communication Foundation (WCF) umożliwia aplikacjom komunikowanie się, czy znajdują się na tym samym komputerze, za pośrednictwem Internetu czy na różnych platformach aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8a07-105">Windows Communication Foundation (WCF) enables applications to communicate whether they are on the same computer, across the Internet, or on different application platforms.</span></span> <span data-ttu-id="a8a07-106">Ten temat zawiera opis zadań, które są wymagane do utworzenia aplikacji WCF.</span><span class="sxs-lookup"><span data-stu-id="a8a07-106">This topic outlines the tasks that are required to build a WCF application.</span></span> <span data-ttu-id="a8a07-107">Aby uzyskać działającą przykładową aplikację, zobacz [samouczek wprowadzenie](getting-started-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="a8a07-107">For a working sample application, see [Getting Started Tutorial](getting-started-tutorial.md).</span></span>  
  
## <a name="the-basic-tasks"></a><span data-ttu-id="a8a07-108">Podstawowe zadania</span><span class="sxs-lookup"><span data-stu-id="a8a07-108">The Basic Tasks</span></span>  

 <span data-ttu-id="a8a07-109">Podstawowe zadania do wykonania to:</span><span class="sxs-lookup"><span data-stu-id="a8a07-109">The basic tasks to perform are, in order:</span></span>  
  
1. <span data-ttu-id="a8a07-110">Zdefiniuj kontrakt usługi.</span><span class="sxs-lookup"><span data-stu-id="a8a07-110">Define the service contract.</span></span> <span data-ttu-id="a8a07-111">Kontrakt usługi określa sygnaturę usługi, dane, które wymienia, oraz inne dane wymagane z umową.</span><span class="sxs-lookup"><span data-stu-id="a8a07-111">A service contract specifies the signature of a service, the data it exchanges, and other contractually required data.</span></span> <span data-ttu-id="a8a07-112">Aby uzyskać więcej informacji, zobacz [Projektowanie kontraktów usług](designing-service-contracts.md).</span><span class="sxs-lookup"><span data-stu-id="a8a07-112">For more information, see [Designing Service Contracts](designing-service-contracts.md).</span></span>  
  
2. <span data-ttu-id="a8a07-113">Zaimplementuj kontrakt.</span><span class="sxs-lookup"><span data-stu-id="a8a07-113">Implement the contract.</span></span> <span data-ttu-id="a8a07-114">Aby zaimplementować kontrakt usługi, należy utworzyć klasę, która implementuje kontrakt i określić zachowania niestandardowe, które powinien mieć środowisko uruchomieniowe.</span><span class="sxs-lookup"><span data-stu-id="a8a07-114">To implement a service contract, create a class that implements the contract and specify custom behaviors that the runtime should have.</span></span> <span data-ttu-id="a8a07-115">Aby uzyskać więcej informacji, zobacz [implementowanie kontraktów usług](implementing-service-contracts.md).</span><span class="sxs-lookup"><span data-stu-id="a8a07-115">For more information, see [Implementing Service Contracts](implementing-service-contracts.md).</span></span>  
  
3. <span data-ttu-id="a8a07-116">Skonfiguruj usługę, określając punkty końcowe i inne informacje o zachowaniu.</span><span class="sxs-lookup"><span data-stu-id="a8a07-116">Configure the service by specifying endpoints and other behavior information.</span></span> <span data-ttu-id="a8a07-117">Aby uzyskać więcej informacji, zobacz [Konfigurowanie usług](configuring-services.md).</span><span class="sxs-lookup"><span data-stu-id="a8a07-117">For more information, see [Configuring Services](configuring-services.md).</span></span>  
  
4. <span data-ttu-id="a8a07-118">Hostowanie usługi.</span><span class="sxs-lookup"><span data-stu-id="a8a07-118">Host the service.</span></span> <span data-ttu-id="a8a07-119">Aby uzyskać więcej informacji, zobacz [usługi hostingu](hosting-services.md).</span><span class="sxs-lookup"><span data-stu-id="a8a07-119">For more information, see [Hosting Services](hosting-services.md).</span></span>  
  
5. <span data-ttu-id="a8a07-120">Tworzenie aplikacji klienckiej.</span><span class="sxs-lookup"><span data-stu-id="a8a07-120">Build a client application.</span></span> <span data-ttu-id="a8a07-121">Aby uzyskać więcej informacji, zobacz [Kompilowanie klientów](building-clients.md).</span><span class="sxs-lookup"><span data-stu-id="a8a07-121">For more information, see [Building Clients](building-clients.md).</span></span>  
  
 <span data-ttu-id="a8a07-122">Mimo że tematy w tej sekcji są zgodne z tą kolejnością, niektóre scenariusze nie zaczynają się od początku.</span><span class="sxs-lookup"><span data-stu-id="a8a07-122">Although the topics in this section follow this order, some scenarios do not start at the beginning.</span></span> <span data-ttu-id="a8a07-123">Na przykład jeśli chcesz skompilować klienta dla istniejącej usługi, Zacznij od kroku 5.</span><span class="sxs-lookup"><span data-stu-id="a8a07-123">For example, if you want to build a client for a pre-existing service, you start at step 5.</span></span> <span data-ttu-id="a8a07-124">Lub jeśli tworzysz usługę, która będzie używana przez inne osoby, możesz pominąć krok 5.</span><span class="sxs-lookup"><span data-stu-id="a8a07-124">Or if you are building a service that others will use, you may skip step 5.</span></span>  
  
 <span data-ttu-id="a8a07-125">Po zapoznaniu się z projektowaniem kontraktów usług można także zapoznać [się z wprowadzeniem do rozszerzalności](introduction-to-extensibility.md).</span><span class="sxs-lookup"><span data-stu-id="a8a07-125">Once you are familiar with developing service contracts, you can also read [Introduction to Extensibility](introduction-to-extensibility.md).</span></span> <span data-ttu-id="a8a07-126">Jeśli masz problemy z usługą, sprawdź rozwiązanie do [rozwiązywania problemów](wcf-troubleshooting-quickstart.md) z programem WCF, aby sprawdzić, czy inne osoby mają takie same lub podobne problemy.</span><span class="sxs-lookup"><span data-stu-id="a8a07-126">If you have problems with your service, check [WCF Troubleshooting Quickstart](wcf-troubleshooting-quickstart.md) to see whether others have the same or similar problems.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a8a07-127">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="a8a07-127">See also</span></span>

- [<span data-ttu-id="a8a07-128">Implementowanie kontraktów usług</span><span class="sxs-lookup"><span data-stu-id="a8a07-128">Implementing Service Contracts</span></span>](implementing-service-contracts.md)
