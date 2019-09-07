---
title: Projektowanie i opracowywanie aplikacji .NET opartych na wielokontenerach i mikrousługach
description: Architektura mikrousług platformy .NET dla aplikacji platformy .NET w kontenerze | Zapoznaj się z zewnętrzną architekturą projektowania i opracowywania aplikacji .NET opartych na wielokontenerach i mikrousługach.
ms.date: 10/02/2018
ms.openlocfilehash: 8c2f828e9913a0efcdf580371124b0f624daeffe
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/30/2019
ms.locfileid: "70296627"
---
# <a name="designing-and-developing-multi-container-and-microservice-based-net-applications"></a><span data-ttu-id="ddd5f-103">Projektowanie i opracowywanie aplikacji .NET opartych na mikrokontenerach i mikrousługach</span><span class="sxs-lookup"><span data-stu-id="ddd5f-103">Designing and Developing Multi-Container and Microservice-Based .NET Applications</span></span>

<span data-ttu-id="ddd5f-104">*Opracowywanie aplikacji mikrousług kontenerowych oznacza, że tworzysz aplikacje wielokontenerowe. Jednak aplikacja obejmująca wiele kontenerów może być również łatwiejsza — na przykład aplikacji trójwarstwowej — i może nie być skompilowana przy użyciu architektury mikrousług.*</span><span class="sxs-lookup"><span data-stu-id="ddd5f-104">*Developing containerized microservice applications means you are building multi-container applications. However, a multi-container application could also be simpler—for example, a three-tier application—and might not be built using a microservice architecture.*</span></span>

<span data-ttu-id="ddd5f-105">Wcześniej zgłoszono pytanie "czy platforma Docker jest konieczna podczas kompilowania architektury mikrousług?".</span><span class="sxs-lookup"><span data-stu-id="ddd5f-105">Earlier we raised the question "Is Docker necessary when building a microservice architecture?"</span></span> <span data-ttu-id="ddd5f-106">Odpowiedź jest niezrozumiała.</span><span class="sxs-lookup"><span data-stu-id="ddd5f-106">The answer is a clear no.</span></span> <span data-ttu-id="ddd5f-107">Docker to włącznik i może zapewnić znaczne korzyści, ale kontenery i platforma Docker nie są twardym wymaganiem dla mikrousług.</span><span class="sxs-lookup"><span data-stu-id="ddd5f-107">Docker is an enabler and can provide significant benefits, but containers and Docker are not a hard requirement for microservices.</span></span> <span data-ttu-id="ddd5f-108">Przykładowo można utworzyć aplikację opartą na mikrousługach z platformą Docker lub bez niej podczas korzystania z usługi Azure Service Fabric, która obsługuje mikrousługi działające jako procesy proste lub kontenery Docker.</span><span class="sxs-lookup"><span data-stu-id="ddd5f-108">As an example, you could create a microservices-based application with or without Docker when using Azure Service Fabric, which supports microservices running as simple processes or as Docker containers.</span></span>

<span data-ttu-id="ddd5f-109">Jeśli jednak wiesz, jak projektować i opracowywać aplikację opartą na mikrousługach, która jest również oparta na kontenerach platformy Docker, będziesz mieć możliwość projektowania i opracowywania dowolnego innego, prostszego modelu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ddd5f-109">However, if you know how to design and develop a microservices-based application that is also based on Docker containers, you will be able to design and develop any other, simpler application model.</span></span> <span data-ttu-id="ddd5f-110">Na przykład można zaprojektować aplikację trójwarstwowej, która wymaga również podejścia obejmującego wiele kontenerów.</span><span class="sxs-lookup"><span data-stu-id="ddd5f-110">For example, you might design a three-tier application that also requires a multi-container approach.</span></span> <span data-ttu-id="ddd5f-111">Ze względu na to, że architektury mikrousług są istotną tendencją w obrębie świata kontenera, ta sekcja koncentruje się na implementacji architektury mikrousług przy użyciu kontenerów platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="ddd5f-111">Because of that, and because microservice architectures are an important trend within the container world, this section focuses on a microservice architecture implementation using Docker containers.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="ddd5f-112">[Poprzedni](../docker-application-development-process/docker-app-development-workflow.md)Następny
>[](microservice-application-design.md)</span><span class="sxs-lookup"><span data-stu-id="ddd5f-112">[Previous](../docker-application-development-process/docker-app-development-workflow.md)
[Next](microservice-application-design.md)</span></span>