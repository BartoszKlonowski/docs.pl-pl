---
title: Tworzenie złożonego interfejsu użytkownika opartego na mikrousługach
description: Architektura mikrousług nie tylko dla zaplecza. Uzyskaj wgląd w widok, który będzie używany w frontonie.
ms.date: 09/20/2018
ms.openlocfilehash: 0d1825d6183b79a0e10f70fc6cfee6ca79a837d8
ms.sourcegitcommit: 10736f243dd2296212e677e207102c463e5f143e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2019
ms.locfileid: "70296784"
---
# <a name="creating-composite-ui-based-on-microservices"></a><span data-ttu-id="184bb-104">Tworzenie złożonego interfejsu użytkownika opartego na mikrousługach</span><span class="sxs-lookup"><span data-stu-id="184bb-104">Creating composite UI based on microservices</span></span>

<span data-ttu-id="184bb-105">Architektura mikrousług często zaczyna się od danych i logiki obsługi po stronie serwera.</span><span class="sxs-lookup"><span data-stu-id="184bb-105">Microservices architecture often starts with the server-side handling data and logic.</span></span> <span data-ttu-id="184bb-106">Jednak bardziej zaawansowane podejście polega na zaprojektowaniu interfejsu użytkownika aplikacji na podstawie mikrousług.</span><span class="sxs-lookup"><span data-stu-id="184bb-106">However, a more advanced approach is to design your application UI based on microservices as well.</span></span> <span data-ttu-id="184bb-107">Oznacza to posiadanie złożonego interfejsu użytkownika utworzonego przez mikrousługi, a nie za pomocą mikrousług na serwerze i tylko monolitycznej aplikacji klienckiej, która korzysta z mikrousług.</span><span class="sxs-lookup"><span data-stu-id="184bb-107">That means having a composite UI produced by the microservices, instead of having microservices on the server and just a monolithic client app consuming the microservices.</span></span> <span data-ttu-id="184bb-108">Dzięki tej metodzie kompilacje mikrousług można zakończyć przy użyciu zarówno logiki, jak i wizualnej reprezentacji.</span><span class="sxs-lookup"><span data-stu-id="184bb-108">With this approach, the microservices you build can be complete with both logic and visual representation.</span></span>

<span data-ttu-id="184bb-109">Rysunek 4-20 przedstawia prostsze podejście do korzystania z mikrousług z monolitycznej aplikacji klienckiej.</span><span class="sxs-lookup"><span data-stu-id="184bb-109">Figure 4-20 shows the simpler approach of just consuming microservices from a monolithic client application.</span></span> <span data-ttu-id="184bb-110">Oczywiście może istnieć usługa ASP.NET MVC między wytwarzaniem kodu HTML i JavaScript.</span><span class="sxs-lookup"><span data-stu-id="184bb-110">Of course, you could have an ASP.NET MVC service in between producing the HTML and JavaScript.</span></span> <span data-ttu-id="184bb-111">Na rysunku przedstawiono uproszczenie, które oznacza, że masz pojedynczy (monolityczny) interfejs użytkownika, który korzysta z mikrousług, które koncentrują się na logice i danych, a nie w kształcie interfejsu użytkownika (HTML i JavaScript).</span><span class="sxs-lookup"><span data-stu-id="184bb-111">The figure is a simplification that highlights that you have a single (monolithic) client UI consuming the microservices, which just focus on logic and data and not on the UI shape (HTML and JavaScript).</span></span>

![Monolityczna aplikacja interfejsu użytkownika łącząca się z indywidualnymi mikrousługami.](./media/image20.png)

<span data-ttu-id="184bb-113">**Rysunek 4-20**.</span><span class="sxs-lookup"><span data-stu-id="184bb-113">**Figure 4-20**.</span></span> <span data-ttu-id="184bb-114">Aplikacja monolitycznego interfejsu użytkownika wykorzystująca mikrousługi zaplecza</span><span class="sxs-lookup"><span data-stu-id="184bb-114">A monolithic UI application consuming back-end microservices</span></span>

<span data-ttu-id="184bb-115">W przeciwieństwie do złożonego interfejsu użytkownika jest precyzyjnie generowany i składający się z mikrousług.</span><span class="sxs-lookup"><span data-stu-id="184bb-115">In contrast, a composite UI is precisely generated and composed by the microservices themselves.</span></span> <span data-ttu-id="184bb-116">Niektóre mikrousługi mają kształt wizualizacji określonych obszarów interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="184bb-116">Some of the microservices drive the visual shape of specific areas of the UI.</span></span> <span data-ttu-id="184bb-117">Zasadniczą różnicą jest to, że masz składniki interfejsu użytkownika klienta (na przykład klasy TypeScript) oparte na szablonach, a ViewModel do kształtowania dla tych szablonów pochodzą z każdej mikrousługi.</span><span class="sxs-lookup"><span data-stu-id="184bb-117">The key difference is that you have client UI components (TypeScript classes, for example) based on templates, and the data-shaping-UI ViewModel for those templates comes from each microservice.</span></span>

<span data-ttu-id="184bb-118">W czasie uruchamiania aplikacji klienckiej każdy składnik interfejsu użytkownika klienta (na przykład klasy TypeScript) rejestruje się z mikrousługą infrastruktury, która umożliwia dostarczanie modele widoków w danym scenariuszu.</span><span class="sxs-lookup"><span data-stu-id="184bb-118">At client application start-up time, each of the client UI components (TypeScript classes, for example) registers itself with an infrastructure microservice capable of providing ViewModels for a given scenario.</span></span> <span data-ttu-id="184bb-119">Jeśli mikrousługa zmieni kształt, interfejs użytkownika zmieni się również.</span><span class="sxs-lookup"><span data-stu-id="184bb-119">If the microservice changes the shape, the UI changes also.</span></span>

<span data-ttu-id="184bb-120">Rysunek 4-21 pokazuje wersję tego podejścia złożonego interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="184bb-120">Figure 4-21 shows a version of this composite UI approach.</span></span> <span data-ttu-id="184bb-121">Jest to uproszczone, ponieważ mogą istnieć inne mikrousługi, które agregują części szczegółowe, które są oparte na różnych technikach.</span><span class="sxs-lookup"><span data-stu-id="184bb-121">This is simplified because you might have other microservices that are aggregating granular parts that are based on different techniques.</span></span> <span data-ttu-id="184bb-122">Jest to zależne od tego, czy tworzysz tradycyjne podejście sieci Web (ASP.NET MVC) czy SPA (aplikacja jednostronicowa).</span><span class="sxs-lookup"><span data-stu-id="184bb-122">It depends on whether you're building a traditional web approach (ASP.NET MVC) or an SPA (Single Page Application).</span></span>

![W złożonej aplikacji interfejsu użytkownika Każda sekcja interfejsu użytkownika jest generowana przez mikrousługę kompozycji interfejsu użytkownika, która działa jak mini-Gateway.](./media/image21.png)

<span data-ttu-id="184bb-124">**Rysunek 4-21**.</span><span class="sxs-lookup"><span data-stu-id="184bb-124">**Figure 4-21**.</span></span> <span data-ttu-id="184bb-125">Przykład złożonej aplikacji interfejsu użytkownika, która jest oparta na mikrousługach zaplecza</span><span class="sxs-lookup"><span data-stu-id="184bb-125">Example of a composite UI application shaped by back-end microservices</span></span>

<span data-ttu-id="184bb-126">Każda z tych mikrousług kompozycji jest podobna do niewielkiej bramy interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="184bb-126">Each of those UI composition microservices would be similar to a small API Gateway.</span></span> <span data-ttu-id="184bb-127">Jednak w tym przypadku każdy z nich jest odpowiedzialny za niewielki obszar interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="184bb-127">But in this case each one is responsible for a small UI area.</span></span>

<span data-ttu-id="184bb-128">Złożone podejście interfejsu użytkownika, które jest oparte na mikrousługach, może być bardziej trudne lub mniejsze, w zależności od tego, jakie technologie interfejsu użytkownika są używane.</span><span class="sxs-lookup"><span data-stu-id="184bb-128">A composite UI approach that's driven by microservices can be more challenging or less so, depending on what UI technologies you're using.</span></span> <span data-ttu-id="184bb-129">Na przykład nie będziesz używać tych samych technik do kompilowania tradycyjnej aplikacji sieci Web, która jest używana do tworzenia SPA lub natywnej aplikacji mobilnej (np. podczas tworzenia aplikacji platformy Xamarin, które mogą być bardziej trudne dla tego podejścia).</span><span class="sxs-lookup"><span data-stu-id="184bb-129">For instance, you won't use the same techniques for building a traditional web application that you use for building an SPA or for native mobile app (as when developing Xamarin apps, which can be more challenging for this approach).</span></span>

<span data-ttu-id="184bb-130">Przykładowa aplikacja [eShopOnContainers](https://aka.ms/MicroservicesArchitecture) używa podejścia interfejsu użytkownika monolitycznego z wielu powodów.</span><span class="sxs-lookup"><span data-stu-id="184bb-130">The [eShopOnContainers](https://aka.ms/MicroservicesArchitecture) sample application uses the monolithic UI approach for multiple reasons.</span></span> <span data-ttu-id="184bb-131">Po pierwsze jest to wprowadzenie do mikrousług i kontenerów.</span><span class="sxs-lookup"><span data-stu-id="184bb-131">First, it's an introduction to microservices and containers.</span></span> <span data-ttu-id="184bb-132">Złożony interfejs użytkownika jest bardziej zaawansowany, ale wymaga również dalszej złożoności podczas projektowania i opracowywania interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="184bb-132">A composite UI is more advanced but also requires further complexity when designing and developing the UI.</span></span> <span data-ttu-id="184bb-133">Ponadto eShopOnContainers zapewnia natywną aplikację mobilną opartą na platformie Xamarin, która spowodowałaby bardziej skomplikowaną po\# stronie klienta.</span><span class="sxs-lookup"><span data-stu-id="184bb-133">Second, eShopOnContainers also provides a native mobile app based on Xamarin, which would make it more complex on the client C\# side.</span></span>

<span data-ttu-id="184bb-134">Zachęcamy jednak do korzystania z następujących odwołań, aby dowiedzieć się więcej na temat złożonego interfejsu użytkownika w oparciu o mikrousługi.</span><span class="sxs-lookup"><span data-stu-id="184bb-134">However, we encourage you to use the following references to learn more about composite UI based on microservices.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="184bb-135">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="184bb-135">Additional resources</span></span>

- <span data-ttu-id="184bb-136">**Złożony interfejs użytkownika korzystający z ASP.NET (warsztat)**  </span><span class="sxs-lookup"><span data-stu-id="184bb-136">**Composite UI using ASP.NET (Particular's Workshop)** </span></span>\
  <https://github.com/Particular/Workshop/tree/master/demos/asp-net-core>

- <span data-ttu-id="184bb-137">**Ruben Oostinga. Monolityczny fronton w architekturze mikrousług** </span><span class="sxs-lookup"><span data-stu-id="184bb-137">**Ruben Oostinga. The Monolithic Frontend in the Microservices Architecture** </span></span>\
  <https://xebia.com/blog/the-monolithic-frontend-in-the-microservices-architecture/>

- <span data-ttu-id="184bb-138">**Mauro Servienti. Wpis tajny lepszej kompozycji interfejsu użytkownika** </span><span class="sxs-lookup"><span data-stu-id="184bb-138">**Mauro Servienti. The secret of better UI composition** </span></span>\
  <https://particular.net/blog/secret-of-better-ui-composition>

- <span data-ttu-id="184bb-139">**Viktor Farcic. Dołączanie składników sieci Web frontonu do mikrousług** </span><span class="sxs-lookup"><span data-stu-id="184bb-139">**Viktor Farcic. Including Front-End Web Components Into Microservices** </span></span>\
  <https://technologyconversations.com/2015/08/09/including-front-end-web-components-into-microservices/>

- <span data-ttu-id="184bb-140">**Zarządzanie frontonem w architekturze mikrousług** </span><span class="sxs-lookup"><span data-stu-id="184bb-140">**Managing Frontend in the Microservices Architecture** </span></span>\
  <https://allegro.tech/2016/03/Managing-Frontend-in-the-microservices-architecture.html>

>[!div class="step-by-step"]
><span data-ttu-id="184bb-141">[Poprzedni](microservices-addressability-service-registry.md)Następny
>[](resilient-high-availability-microservices.md)</span><span class="sxs-lookup"><span data-stu-id="184bb-141">[Previous](microservices-addressability-service-registry.md)
[Next](resilient-high-availability-microservices.md)</span></span>