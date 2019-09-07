---
title: Tworzenie, rozwijanie i przechowywanie wersji interfejsów API i kontaktów w mikrousługach
description: Tworzenie mikrousług API i kontraktów uwzględniających ewolucję i przechowywanie wersji, ponieważ wymagają zmiany.
ms.date: 09/20/2018
ms.openlocfilehash: 1972d02d8bf7935c71bfd383707ae19ea2baded9
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/30/2019
ms.locfileid: "70295458"
---
# <a name="creating-evolving-and-versioning-microservice-apis-and-contracts"></a><span data-ttu-id="dae0c-103">Tworzenie, rozwijanie i przechowywanie wersji interfejsów API i kontaktów w mikrousługach</span><span class="sxs-lookup"><span data-stu-id="dae0c-103">Creating, evolving, and versioning microservice APIs and contracts</span></span>

<span data-ttu-id="dae0c-104">Interfejs API mikrousług to kontrakt między usługą i jej klientami.</span><span class="sxs-lookup"><span data-stu-id="dae0c-104">A microservice API is a contract between the service and its clients.</span></span> <span data-ttu-id="dae0c-105">Można wypróbować mikrousługi niezależnie tylko wtedy, gdy nie uda się przerwać jej kontraktu interfejsu API, co oznacza, że kontrakt jest tak ważny.</span><span class="sxs-lookup"><span data-stu-id="dae0c-105">You'll be able to evolve a microservice independently only if you do not break its API contract, which is why the contract is so important.</span></span> <span data-ttu-id="dae0c-106">Jeśli zmienisz kontrakt, wpłynie to na aplikacje klienckie lub bramę interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="dae0c-106">If you change the contract, it will impact your client applications or your API Gateway.</span></span>

<span data-ttu-id="dae0c-107">Charakter definicji interfejsu API zależy od używanego protokołu.</span><span class="sxs-lookup"><span data-stu-id="dae0c-107">The nature of the API definition depends on which protocol you're using.</span></span> <span data-ttu-id="dae0c-108">Na przykład jeśli korzystasz z komunikatów (takich jak [AMQP](https://www.amqp.org/)), interfejs API składa się z typów komunikatów.</span><span class="sxs-lookup"><span data-stu-id="dae0c-108">For instance, if you're using messaging (like [AMQP](https://www.amqp.org/)), the API consists of the message types.</span></span> <span data-ttu-id="dae0c-109">W przypadku korzystania z usług HTTP i RESTful interfejs API składa się z adresów URL i formatów JSON żądania i odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="dae0c-109">If you're using HTTP and RESTful services, the API consists of the URLs and the request and response JSON formats.</span></span>

<span data-ttu-id="dae0c-110">Jednak nawet jeśli jesteś przydatnego o początkowym kontrakcie, interfejs API usługi będzie musiał ulec zmianie z upływem czasu.</span><span class="sxs-lookup"><span data-stu-id="dae0c-110">However, even if you're thoughtful about your initial contract, a service API will need to change over time.</span></span> <span data-ttu-id="dae0c-111">Gdy tak się stanie, a zwłaszcza jeśli interfejs API jest publicznym interfejsem API używanym przez wiele aplikacji klienckich — zazwyczaj nie można wymusić uaktualnienia wszystkich klientów do nowego kontraktu interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="dae0c-111">When that happens—and especially if your API is a public API consumed by multiple client applications — you typically can't force all clients to upgrade to your new API contract.</span></span> <span data-ttu-id="dae0c-112">Zwykle należy wdrożyć nowe wersje usługi w taki sposób, aby jednocześnie działały zarówno stare, jak i nowe wersje kontraktu usługi.</span><span class="sxs-lookup"><span data-stu-id="dae0c-112">You usually need to incrementally deploy new versions of a service in a way that both old and new versions of a service contract are running simultaneously.</span></span> <span data-ttu-id="dae0c-113">W związku z tym ważne jest, aby mieć strategię obsługi wersji usługi.</span><span class="sxs-lookup"><span data-stu-id="dae0c-113">Therefore, it's important to have a strategy for your service versioning.</span></span>

<span data-ttu-id="dae0c-114">Gdy zmiany interfejsu API są niewielkie, podobnie jak w przypadku dodawania atrybutów lub parametrów do interfejsu API, klienci korzystający ze starszego interfejsu API powinni przełączać i korzystać z nowej wersji usługi.</span><span class="sxs-lookup"><span data-stu-id="dae0c-114">When the API changes are small, like if you add attributes or parameters to your API, clients that use an older API should switch and work with the new version of the service.</span></span> <span data-ttu-id="dae0c-115">Może być możliwe podanie wartości domyślnych dla wszelkich brakujących atrybutów, które są wymagane, a klienci mogą ignorować wszelkie dodatkowe atrybuty odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="dae0c-115">You might be able to provide default values for any missing attributes that are required, and the clients might be able to ignore any extra response attributes.</span></span>

<span data-ttu-id="dae0c-116">Niemniej jednak czasami trzeba wprowadzić istotne i niezgodne zmiany w interfejsie API usługi.</span><span class="sxs-lookup"><span data-stu-id="dae0c-116">However, sometimes you need to make major and incompatible changes to a service API.</span></span> <span data-ttu-id="dae0c-117">Ponieważ nie można wymusić natychmiastowego uaktualnienia aplikacji lub usług klienta do nowej wersji, usługa musi obsługiwać starsze wersje interfejsu API przez pewien okres.</span><span class="sxs-lookup"><span data-stu-id="dae0c-117">Because you might not be able to force client applications or services to upgrade immediately to the new version, a service must support older versions of the API for some period.</span></span> <span data-ttu-id="dae0c-118">Jeśli używasz mechanizmu opartego na protokole HTTP, takiego jak REST, jedno podejście polega na osadzeniu numeru wersji interfejsu API w adresie URL lub w nagłówku HTTP.</span><span class="sxs-lookup"><span data-stu-id="dae0c-118">If you're using an HTTP-based mechanism such as REST, one approach is to embed the API version number in the URL or into an HTTP header.</span></span> <span data-ttu-id="dae0c-119">Następnie można zdecydować się na wdrożenie obu wersji usługi jednocześnie w ramach tego samego wystąpienia usługi lub wdrożenie różnych wystąpień, które obsługują wersję interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="dae0c-119">Then you can decide between implementing both versions of the service simultaneously within the same service instance, or deploying different instances that each handle a version of the API.</span></span> <span data-ttu-id="dae0c-120">Dobrym rozwiązaniem dla tego jest [wzorzec mediator](https://en.wikipedia.org/wiki/Mediator_pattern) (na przykład [Biblioteka MediatR](https://github.com/jbogard/MediatR)), aby oddzielić różne wersje implementacji na niezależne programy obsługi.</span><span class="sxs-lookup"><span data-stu-id="dae0c-120">A good approach for this is the [Mediator pattern](https://en.wikipedia.org/wiki/Mediator_pattern) (for example, [MediatR library](https://github.com/jbogard/MediatR)) to decouple the different implementation versions into independent handlers.</span></span>

<span data-ttu-id="dae0c-121">Na [koniec, jeśli](https://www.infoq.com/articles/mark-baker-hypermedia) używasz architektury REST, najlepszym rozwiązaniem jest udostępnienie wersji usług i umożliwienie rozwijania interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="dae0c-121">Finally, if you're using a REST architecture, [Hypermedia](https://www.infoq.com/articles/mark-baker-hypermedia) is the best solution for versioning your services and allowing evolvable APIs.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dae0c-122">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="dae0c-122">Additional resources</span></span>

- <span data-ttu-id="dae0c-123">**Scott Hanselman. Łatwość ASP.NET Core RESTful internetowego interfejsu API** </span><span class="sxs-lookup"><span data-stu-id="dae0c-123">**Scott Hanselman. ASP.NET Core RESTful Web API versioning made easy** </span></span>\
  <https://www.hanselman.com/blog/ASPNETCoreRESTfulWebAPIVersioningMadeEasy.aspx>

- <span data-ttu-id="dae0c-124">**Przechowywanie wersji interfejsu API sieci Web RESTful** </span><span class="sxs-lookup"><span data-stu-id="dae0c-124">**Versioning a RESTful web API** </span></span>\
  <https://docs.microsoft.com/azure/architecture/best-practices/api-design#versioning-a-restful-web-api>

- <span data-ttu-id="dae0c-125">**Roy. Przechowywanie wersji, nośniki i REST** </span><span class="sxs-lookup"><span data-stu-id="dae0c-125">**Roy Fielding. Versioning, Hypermedia, and REST** </span></span>\
  <https://www.infoq.com/articles/roy-fielding-on-versioning>

>[!div class="step-by-step"]
><span data-ttu-id="dae0c-126">[Poprzedni](asynchronous-message-based-communication.md)Następny
>[](microservices-addressability-service-registry.md)</span><span class="sxs-lookup"><span data-stu-id="dae0c-126">[Previous](asynchronous-message-based-communication.md)
[Next](microservices-addressability-service-registry.md)</span></span>