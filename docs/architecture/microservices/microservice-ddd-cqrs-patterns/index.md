---
title: Rozwiązywanie problemów ze złożonościami biznesowymi w mikrousłudze z wzorcami DDD i CQRS
description: Architektura mikrousług platformy .NET dla aplikacji platformy .NET w kontenerze | Dowiedz się, jak rozwiązywać złożone scenariusze biznesowe, stosując wzorce DDD i CQRS
ms.date: 10/08/2018
ms.openlocfilehash: d311641e2ac73205c04c3f1147b54991585ce851
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/30/2019
ms.locfileid: "70295916"
---
# <a name="tackle-business-complexity-in-a-microservice-with-ddd-and-cqrs-patterns"></a><span data-ttu-id="dd942-103">Rozwiązywanie złożoności biznesowej w mikrousłudze za pomocą wzorców DDD i CQRS</span><span class="sxs-lookup"><span data-stu-id="dd942-103">Tackle Business Complexity in a Microservice with DDD and CQRS Patterns</span></span>

<span data-ttu-id="dd942-104">*Zaprojektuj model domeny dla każdego mikrousług lub kontekstu ograniczonego, który odzwierciedla zrozumienie domeny biznesowej.*</span><span class="sxs-lookup"><span data-stu-id="dd942-104">*Design a domain model for each microservice or Bounded Context that reflects understanding of the business domain.*</span></span>

<span data-ttu-id="dd942-105">Ta sekcja koncentruje się na bardziej zaawansowanych mikrousługach, które są implementowane, gdy potrzebna jest obsługa złożonych podsystemów lub mikrousług pochodzących od znajomości ekspertów domeny z kiedykolwiek zmienionymi regułami biznesowymi.</span><span class="sxs-lookup"><span data-stu-id="dd942-105">This section focuses on more advanced microservices that you implement when you need to tackle complex subsystems, or microservices derived from the knowledge of domain experts with ever-changing business rules.</span></span> <span data-ttu-id="dd942-106">Wzorce architektury użyte w tej sekcji są oparte na podejściach do projektowania opartego na domenach (DDD) i Command and Query Responsibility Segregation (CQRS), jak pokazano na rysunku 7-1.</span><span class="sxs-lookup"><span data-stu-id="dd942-106">The architecture patterns used in this section are based on domain-driven design (DDD) and Command and Query Responsibility Segregation (CQRS) approaches, as illustrated in Figure 7-1.</span></span>

![Różnica między architekturą zewnętrzną: wzorce mikrousług, bramy interfejsu API, komunikacja odporna, publikacje/podpłaty, itp. i architektura wewnętrzna: oparte na danych/CRUD, wzorce DDD, iniekcja zależności, wiele bibliotek itd.](./media/image1.png)

<span data-ttu-id="dd942-108">**Rysunek 7-1**.</span><span class="sxs-lookup"><span data-stu-id="dd942-108">**Figure 7-1**.</span></span> <span data-ttu-id="dd942-109">Zewnętrzna architektura mikrousług, a wewnętrzne wzorce architektury dla każdej mikrousługi</span><span class="sxs-lookup"><span data-stu-id="dd942-109">External microservice architecture versus internal architecture patterns for each microservice</span></span>

<span data-ttu-id="dd942-110">Jednak większość technik dla mikrousług opartych na danych, takich jak implementacja usługi Web API ASP.NET Core lub sposób ujawniania metadanych struktury Swagger przy użyciu Swashbuckle lub NSwag, ma również zastosowanie do bardziej zaawansowanych mikrousług wdrożonych wewnętrznie z Wzorce.</span><span class="sxs-lookup"><span data-stu-id="dd942-110">However, most of the techniques for data driven microservices, such as how to implement an ASP.NET Core Web API service or how to expose Swagger metadata with Swashbuckle or NSwag, are also applicable to the more advanced microservices implemented internally with DDD patterns.</span></span> <span data-ttu-id="dd942-111">Ta sekcja stanowi rozszerzenie poprzednich sekcji, ponieważ większość praktyk opisanych wcześniej również ma zastosowanie w tym miejscu lub dla dowolnego rodzaju mikrousług.</span><span class="sxs-lookup"><span data-stu-id="dd942-111">This section is an extension of the previous sections, because most of the practices explained earlier also apply here or for any kind of microservice.</span></span>

<span data-ttu-id="dd942-112">Ta sekcja najpierw zawiera szczegółowe informacje dotyczące uproszczonych wzorców CQRS używanych w aplikacji eShopOnContainers Reference.</span><span class="sxs-lookup"><span data-stu-id="dd942-112">This section first provides details on the simplified CQRS patterns used in the eShopOnContainers reference application.</span></span> <span data-ttu-id="dd942-113">Później zostanie wyświetlony przegląd technik, które umożliwiają znalezienie typowych wzorców, których można użyć ponownie w aplikacjach.</span><span class="sxs-lookup"><span data-stu-id="dd942-113">Later, you will get an overview of the DDD techniques that enable you to find common patterns that you can reuse in your applications.</span></span>

<span data-ttu-id="dd942-114">DDD to duży temat z bogatym zestawem zasobów do uczenia się.</span><span class="sxs-lookup"><span data-stu-id="dd942-114">DDD is a large topic with a rich set of resources for learning.</span></span> <span data-ttu-id="dd942-115">Możesz zacząć od książek, takich jak [Projektowanie oparte na domenach](https://domainlanguage.com/ddd/) przez Eric Evans i dodatkowe materiały z Vaughn Vernon, Jimmy Nilsson, Greg Young, UDI Dahan, Jimmy Bogard i wielu innych ekspertów DDD/CQRS.</span><span class="sxs-lookup"><span data-stu-id="dd942-115">You can start with books like [Domain-Driven Design](https://domainlanguage.com/ddd/) by Eric Evans and additional materials from Vaughn Vernon, Jimmy Nilsson, Greg Young, Udi Dahan, Jimmy Bogard, and many other DDD/CQRS experts.</span></span> <span data-ttu-id="dd942-116">Ale większość z nich jest konieczna, aby dowiedzieć się, jak zastosować techniki DDD z konwersacji, tablic i sesji modelowania domeny z ekspertami w konkretnej domenie biznesowej.</span><span class="sxs-lookup"><span data-stu-id="dd942-116">But most of all you need to try to learn how to apply DDD techniques from the conversations, whiteboarding, and domain modeling sessions with the experts in your concrete business domain.</span></span>

#### <a name="additional-resources"></a><span data-ttu-id="dd942-117">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="dd942-117">Additional resources</span></span>

##### <a name="ddd-domain-driven-design"></a><span data-ttu-id="dd942-118">DDD (Projektowanie oparte na domenie)</span><span class="sxs-lookup"><span data-stu-id="dd942-118">DDD (Domain-Driven Design)</span></span>

- <span data-ttu-id="dd942-119">**Eric Evans. Język domeny** </span><span class="sxs-lookup"><span data-stu-id="dd942-119">**Eric Evans. Domain Language** </span></span>\
  <https://domainlanguage.com/>

- <span data-ttu-id="dd942-120">**Fowlera Martin. Projektowanie oparte na domenie** </span><span class="sxs-lookup"><span data-stu-id="dd942-120">**Martin Fowler. Domain-Driven Design** </span></span>\
  <https://martinfowler.com/tags/domain%20driven%20design.html>

- <span data-ttu-id="dd942-121">**Jimmy Bogard. Wzmacnianie domeny: podstawowy** </span><span class="sxs-lookup"><span data-stu-id="dd942-121">**Jimmy Bogard. Strengthening your domain: a primer** </span></span>\
  <https://lostechies.com/jimmybogard/2010/02/04/strengthening-your-domain-a-primer/>

##### <a name="ddd-books"></a><span data-ttu-id="dd942-122">Książki</span><span class="sxs-lookup"><span data-stu-id="dd942-122">DDD books</span></span>

- <span data-ttu-id="dd942-123">**Eric Evans. Projektowanie oparte na domenie: Zapełnianie się złożonością oprogramowania** </span><span class="sxs-lookup"><span data-stu-id="dd942-123">**Eric Evans. Domain-Driven Design: Tackling Complexity in the Heart of Software** </span></span>\
  <https://www.amazon.com/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215/>

- <span data-ttu-id="dd942-124">**Eric Evans. Odwołania do projektu opartego na domenie: Definicje i podsumowania wzorców** </span><span class="sxs-lookup"><span data-stu-id="dd942-124">**Eric Evans. Domain-Driven Design Reference: Definitions and Pattern Summaries** </span></span>\
  <https://www.amazon.com/Domain-Driven-Design-Reference-Definitions-2014-09-22/dp/B01N8YB4ZO/>

- <span data-ttu-id="dd942-125">**Vaughn Vernon. Implementowanie projektu opartego na domenie** </span><span class="sxs-lookup"><span data-stu-id="dd942-125">**Vaughn Vernon. Implementing Domain-Driven Design** </span></span>\
  <https://www.amazon.com/Implementing-Domain-Driven-Design-Vaughn-Vernon/dp/0321834577/>

- <span data-ttu-id="dd942-126">**Vaughn Vernon. Projekt oparty na domenie jest odłączony** </span><span class="sxs-lookup"><span data-stu-id="dd942-126">**Vaughn Vernon. Domain-Driven Design Distilled** </span></span>\
  <https://www.amazon.com/Domain-Driven-Design-Distilled-Vaughn-Vernon/dp/0134434420/>

- <span data-ttu-id="dd942-127">**Jimmy Nilsson. Stosowanie projektowania i wzorców opartych na domenie** </span><span class="sxs-lookup"><span data-stu-id="dd942-127">**Jimmy Nilsson. Applying Domain-Driven Design and Patterns** </span></span>\
  <https://www.amazon.com/Applying-Domain-Driven-Design-Patterns-Examples/dp/0321268202/>

- <span data-ttu-id="dd942-128">**Cesar de La Torre. N-warstwowe wskazówki dotyczące architektury zorientowanej na domeny z platformą .NET** </span><span class="sxs-lookup"><span data-stu-id="dd942-128">**Cesar de la Torre. N-Layered Domain-Oriented Architecture Guide with .NET** </span></span>\
  <https://www.amazon.com/N-Layered-Domain-Oriented-Architecture-Guide-NET/dp/8493903612/>

- <span data-ttu-id="dd942-129">**Abel Avram i Floyd Marinescu. Szybkie projektowanie oparte na domenie** </span><span class="sxs-lookup"><span data-stu-id="dd942-129">**Abel Avram and Floyd Marinescu. Domain-Driven Design Quickly** </span></span>\
  <https://www.amazon.com/Domain-Driven-Design-Quickly-Abel-Avram/dp/1411609255/>

- <span data-ttu-id="dd942-130">**Scott Millett, Nick dostrajania — wzorce, zasady i praktyki dotyczące projektowania opartego na domenie** </span><span class="sxs-lookup"><span data-stu-id="dd942-130">**Scott Millett, Nick Tune - Patterns, Principles, and Practices of Domain-Driven Design** </span></span>\
  <http://www.wrox.com/WileyCDA/WroxTitle/Patterns-Principles-and-Practices-of-Domain-Driven-Design.productCd-1118714709.html>

##### <a name="ddd-training"></a><span data-ttu-id="dd942-131">Uczenie DDD</span><span class="sxs-lookup"><span data-stu-id="dd942-131">DDD training</span></span>

- <span data-ttu-id="dd942-132">**Julie Lerman i Steve Smith. Podstawy projektowania oparte na domenie** </span><span class="sxs-lookup"><span data-stu-id="dd942-132">**Julie Lerman and Steve Smith. Domain-Driven Design Fundamentals** </span></span>\
  <https://bit.ly/PS-DDD>

>[!div class="step-by-step"]
><span data-ttu-id="dd942-133">[Poprzedni](../multi-container-microservice-net-applications/implement-api-gateways-with-ocelot.md)Następny
>[](apply-simplified-microservice-cqrs-ddd-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="dd942-133">[Previous](../multi-container-microservice-net-applications/implement-api-gateways-with-ocelot.md)
[Next](apply-simplified-microservice-cqrs-ddd-patterns.md)</span></span>