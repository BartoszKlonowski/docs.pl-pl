---
title: Wdrażanie bram interfejsu API za pomocą rozwiązania Ocelot
description: Dowiedz się, jak zaimplementować bramy interfejsu API za pomocą Ocelot oraz jak używać Ocelot w środowisku opartym na kontenerach.
ms.date: 03/02/2020
ms.openlocfilehash: 5da8533eff394b587d123970742727484a7236ad
ms.sourcegitcommit: 4b79862c5b41fbd86cf38f926f6a49516059f6f2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/18/2020
ms.locfileid: "97678120"
---
# <a name="implement-api-gateways-with-ocelot"></a><span data-ttu-id="bfab2-103">Implementowanie bram interfejsu API za pomocą Ocelot</span><span class="sxs-lookup"><span data-stu-id="bfab2-103">Implement API Gateways with Ocelot</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bfab2-104">[EShopOnContainers](https://github.com/dotnet-architecture/eShopOnContainers) aplikacji mikrousługi referencyjnej używa obecnie funkcji dostarczonych przez [wysłannika](https://www.envoyproxy.io/) do implementowania bramy interfejsu API zamiast wcześniejszego odwołania do [Ocelot](https://github.com/ThreeMammals/Ocelot).</span><span class="sxs-lookup"><span data-stu-id="bfab2-104">The reference microservice application [eShopOnContainers](https://github.com/dotnet-architecture/eShopOnContainers) is currently using features provided by [Envoy](https://www.envoyproxy.io/) to implement the API Gateway instead of the earlier referenced [Ocelot](https://github.com/ThreeMammals/Ocelot).</span></span>
> <span data-ttu-id="bfab2-105">Ten wybór projektu został dokonany z powodu wbudowanej obsługi protokołu WebSocket w programie wysłannika, wymaganej przez nową komunikację między usługami gRPC zaimplementowaną w eShopOnContainers.</span><span class="sxs-lookup"><span data-stu-id="bfab2-105">We made this design choice because of Envoy's built-in support for the WebSocket protocol, required by the new gRPC inter-service communications implemented in eShopOnContainers.</span></span>
> <span data-ttu-id="bfab2-106">Ta sekcja w przewodniku została jednak zachowana, dlatego można rozważyć Ocelot jako prostą, łatwą i uproszczoną bramę interfejsu API odpowiednią do scenariuszy klasy produkcyjnej.</span><span class="sxs-lookup"><span data-stu-id="bfab2-106">However, we've retained this section in the guide so you can consider Ocelot as a simple, capable, and lightweight API Gateway suitable for production-grade scenarios.</span></span>
> <span data-ttu-id="bfab2-107">Ponadto Najnowsza wersja Ocelot zawiera nieprzerwaną zmianę w schemacie JSON.</span><span class="sxs-lookup"><span data-stu-id="bfab2-107">Also, latest Ocelot version contains a breaking change on its json schema.</span></span> <span data-ttu-id="bfab2-108">Rozważ użycie Ocelot < v 16.0.0 lub użycie tras kluczowych zamiast retras.</span><span class="sxs-lookup"><span data-stu-id="bfab2-108">Consider using Ocelot < v16.0.0, or use the key Routes instead of ReRoutes.</span></span>

## <a name="architect-and-design-your-api-gateways"></a><span data-ttu-id="bfab2-109">Architekt i projektowanie bram interfejsu API</span><span class="sxs-lookup"><span data-stu-id="bfab2-109">Architect and design your API Gateways</span></span>

<span data-ttu-id="bfab2-110">Poniższy diagram architektury przedstawia sposób implementacji bram interfejsu API z Ocelot w eShopOnContainers.</span><span class="sxs-lookup"><span data-stu-id="bfab2-110">The following architecture diagram shows how API Gateways were implemented with Ocelot in eShopOnContainers.</span></span>

![Diagram przedstawiający architekturę eShopOnContainers.](./media/implement-api-gateways-with-ocelot/eshoponcontainers-architecture.png)

<span data-ttu-id="bfab2-112">**Rysunek 6-28**.</span><span class="sxs-lookup"><span data-stu-id="bfab2-112">**Figure 6-28**.</span></span> <span data-ttu-id="bfab2-113">Architektura eShopOnContainers z bramami interfejsu API</span><span class="sxs-lookup"><span data-stu-id="bfab2-113">eShopOnContainers architecture with API Gateways</span></span>

<span data-ttu-id="bfab2-114">Ten diagram pokazuje, w jaki sposób cała aplikacja jest wdrażana na jednym hoście platformy Docker lub na komputerze deweloperskim z "Docker for Windows" lub "Docker for Mac".</span><span class="sxs-lookup"><span data-stu-id="bfab2-114">That diagram shows how the whole application is deployed into a single Docker host or development PC with "Docker for Windows" or "Docker for Mac".</span></span> <span data-ttu-id="bfab2-115">Jednak wdrażanie w dowolnym programie Orchestrator będzie podobne, ale każdy kontener na diagramie może być skalowany w programie Orchestrator.</span><span class="sxs-lookup"><span data-stu-id="bfab2-115">However, deploying into any orchestrator would be similar, but any container in the diagram could be scaled out in the orchestrator.</span></span>

<span data-ttu-id="bfab2-116">Ponadto zasoby infrastruktury, takie jak bazy danych, pamięci podręcznej i brokerów komunikatów, powinny być oddzielone od programu Orchestrator i wdrożone w systemach o wysokiej dostępności na potrzeby infrastruktury, takich jak Azure SQL Database, Azure Cosmos DB, Azure Redis, Azure Service Bus lub dowolne rozwiązanie klastra HA w środowisku lokalnym.</span><span class="sxs-lookup"><span data-stu-id="bfab2-116">In addition, the infrastructure assets such as databases, cache, and message brokers should be offloaded from the orchestrator and deployed into high available systems for infrastructure, like Azure SQL Database, Azure Cosmos DB, Azure Redis, Azure Service Bus, or any HA clustering solution on-premises.</span></span>

<span data-ttu-id="bfab2-117">Podobnie jak można zauważyć, że na diagramie istnieje kilka bram interfejsu API, dzięki czemu wiele zespołów programistycznych może być autonomiczne (w tym przypadku funkcje marketingu a funkcje zakupów) podczas opracowywania i wdrażania mikrousług oraz własnych powiązanych bram interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="bfab2-117">As you can also notice in the diagram, having several API Gateways allows multiple development teams to be autonomous (in this case Marketing features vs. Shopping features) when developing and deploying their microservices plus their own related API Gateways.</span></span>

<span data-ttu-id="bfab2-118">Jeśli masz pojedynczą, monolityczną bramę interfejsu API, która oznacza, że jeden punkt będzie aktualizowany przez kilka zespołów programistycznych, które mogą dołączać wszystkie mikrousługi do jednej części aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bfab2-118">If you had a single monolithic API Gateway that would mean a single point to be updated by several development teams, which could couple all the microservices with a single part of the application.</span></span>

<span data-ttu-id="bfab2-119">Znacznie dokładniej w projekcie, czasem niekiedy Szczegółowa Brama interfejsu API może być również ograniczona do pojedynczej mikrousługi biznesowej, w zależności od wybranej architektury.</span><span class="sxs-lookup"><span data-stu-id="bfab2-119">Going much further in the design, sometimes a fine-grained API Gateway can also be limited to a single business microservice depending on the chosen architecture.</span></span> <span data-ttu-id="bfab2-120">Posiadanie granic bramy interfejsu API, które są określone przez firmę lub domenę, pomoże Ci uzyskać lepszy projekt.</span><span class="sxs-lookup"><span data-stu-id="bfab2-120">Having the API Gateway's boundaries dictated by the business or domain will help you to get a better design.</span></span>

<span data-ttu-id="bfab2-121">Na przykład, szczegółowy stopień szczegółowości warstwy bramy API może być szczególnie przydatny w przypadku bardziej zaawansowanych aplikacji interfejsu użytkownika złożonego, które są oparte na mikrousługach, ponieważ pojęcie szczegółowej bramy interfejsu API jest podobne do usługi kompozycji interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bfab2-121">For instance, fine granularity in the API Gateway tier can be especially useful for more advanced composite UI applications that are based on microservices, because the concept of a fine-grained API Gateway is similar to a UI composition service.</span></span>

<span data-ttu-id="bfab2-122">W poprzedniej sekcji omówiono [Tworzenie złożonych interfejsów użytkownika opartych na mikrousługach](../architect-microservice-container-applications/microservice-based-composite-ui-shape-layout.md).</span><span class="sxs-lookup"><span data-stu-id="bfab2-122">We delve into more details in the previous section [Creating composite UI based on microservices](../architect-microservice-container-applications/microservice-based-composite-ui-shape-layout.md).</span></span>

<span data-ttu-id="bfab2-123">W ramach usługi Key wnioskiem w przypadku wielu aplikacji średniej i o dużej wielkości korzystanie z niestandardowo przygotowanego produktu bramy API jest zwykle dobrym rozwiązaniem, ale nie jako jednym agregatorem monolitycznym lub unikatowym centralną bramą interfejsu API, chyba że brama interfejsu API zezwala na wiele niezależnych obszarów konfiguracji dla kilku zespołów programistycznych tworzących autonomiczne mikrousługi.</span><span class="sxs-lookup"><span data-stu-id="bfab2-123">As a key takeaway, for many medium- and large-size applications, using a custom-built API Gateway product is usually a good approach, but not as a single monolithic aggregator or unique central custom API Gateway unless that API Gateway allows multiple independent configuration areas for the several development teams creating autonomous microservices.</span></span>

### <a name="sample-microservicescontainers-to-reroute-through-the-api-gateways"></a><span data-ttu-id="bfab2-124">Przykładowe mikrousługi/kontenery do przekierowania przez bramy interfejsu API</span><span class="sxs-lookup"><span data-stu-id="bfab2-124">Sample microservices/containers to reroute through the API Gateways</span></span>

<span data-ttu-id="bfab2-125">Na przykład eShopOnContainers ma około sześć wewnętrznych typów mikrousług, które muszą być publikowane za pomocą bram interfejsu API, jak pokazano na poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="bfab2-125">As an example, eShopOnContainers has around six internal microservice-types that have to be published through the API Gateways, as shown in the following image.</span></span>

![Zrzut ekranu przedstawiający folder usługi z podfolderami.](./media/implement-api-gateways-with-ocelot/eshoponcontainers-microservice-folders.png)

<span data-ttu-id="bfab2-127">**Rysunek 6-29**.</span><span class="sxs-lookup"><span data-stu-id="bfab2-127">**Figure 6-29**.</span></span> <span data-ttu-id="bfab2-128">Foldery mikrousług w rozwiązaniu eShopOnContainers w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bfab2-128">Microservice folders in eShopOnContainers solution in Visual Studio</span></span>

<span data-ttu-id="bfab2-129">Informacje o usłudze tożsamości — w projekcie, który jest pozostawiony do routingu bramy interfejsu API, ponieważ jest to jedyne zagadnienie związane z wycinaniem w systemie, chociaż z Ocelot jest również możliwe dołączenie go jako części list reroutingu.</span><span class="sxs-lookup"><span data-stu-id="bfab2-129">About the Identity service, in the design it's left out of the API Gateway routing because it's the only cross-cutting concern in the system, although with Ocelot it's also possible to include it as part of the rerouting lists.</span></span>

<span data-ttu-id="bfab2-130">Wszystkie te usługi są obecnie implementowane jako ASP.NET Core usług interfejsu API sieci Web, co umożliwia poinformowanie o kodzie.</span><span class="sxs-lookup"><span data-stu-id="bfab2-130">All those services are currently implemented as ASP.NET Core Web API services, as you can tell from the code.</span></span> <span data-ttu-id="bfab2-131">Skupmy się na jednym z mikrousług, takimi jak kod mikrousług katalogu.</span><span class="sxs-lookup"><span data-stu-id="bfab2-131">Let's focus on one of the microservices like the Catalog microservice code.</span></span>

![Zrzut ekranu przedstawiający Eksplorator rozwiązań pokazujący zawartość projektu w katalogu. API.](./media/implement-api-gateways-with-ocelot/catalog-api-microservice-folders.png)

<span data-ttu-id="bfab2-133">**Rysunek 6-30**.</span><span class="sxs-lookup"><span data-stu-id="bfab2-133">**Figure 6-30**.</span></span> <span data-ttu-id="bfab2-134">Przykładowa usługa interfejsu API sieci Web (mikrousługa katalogu)</span><span class="sxs-lookup"><span data-stu-id="bfab2-134">Sample Web API microservice (Catalog microservice)</span></span>

<span data-ttu-id="bfab2-135">Można sprawdzić, czy katalog jest typowym ASP.NET Core projektem interfejsu API sieci Web z kilkoma kontrolerami i metodami, takimi jak w poniższym kodzie.</span><span class="sxs-lookup"><span data-stu-id="bfab2-135">You can see that the Catalog microservice is a typical ASP.NET Core Web API project with several controllers and methods like in the following code.</span></span>

```csharp
[HttpGet]
[Route("items/{id:int}")]
[ProducesResponseType((int)HttpStatusCode.BadRequest)]
[ProducesResponseType((int)HttpStatusCode.NotFound)]
[ProducesResponseType(typeof(CatalogItem),(int)HttpStatusCode.OK)]
public async Task<IActionResult> GetItemById(int id)
{
    if (id <= 0)
    {
        return BadRequest();
    }
    var item = await _catalogContext.CatalogItems.
                                          SingleOrDefaultAsync(ci => ci.Id == id);
    //…

    if (item != null)
    {
        return Ok(item);
    }
    return NotFound();
}
```

<span data-ttu-id="bfab2-136">Żądanie HTTP spowoduje zakończenie działania tego rodzaju kodu w języku C#, który uzyskuje dostęp do bazy danych mikrousług i wszelkich dodatkowych wymaganych akcji.</span><span class="sxs-lookup"><span data-stu-id="bfab2-136">The HTTP request will end up running that kind of C# code accessing the microservice database and any additional required action.</span></span>

<span data-ttu-id="bfab2-137">W odniesieniu do adresu URL mikrousług, gdy kontenery są wdrażane na lokalnym komputerze deweloperskim (lokalny Host platformy Docker), każdy kontener mikrousług ma zawsze port wewnętrzny (zazwyczaj port 80) określony w pliku dockerfile, jak w poniższym pliku dockerfile:</span><span class="sxs-lookup"><span data-stu-id="bfab2-137">Regarding the microservice URL, when the containers are deployed in your local development PC (local Docker host), each microservice's container always has an internal port (usually port 80) specified in its dockerfile, as in the following dockerfile:</span></span>

```dockerfile
FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
```

<span data-ttu-id="bfab2-138">Port 80 wyświetlany w kodzie jest wewnętrzny w ramach hosta platformy Docker, więc nie można go połączyć z aplikacjami klienckimi.</span><span class="sxs-lookup"><span data-stu-id="bfab2-138">The port 80 shown in the code is internal within the Docker host, so it can't be reached by client apps.</span></span>

<span data-ttu-id="bfab2-139">Aplikacje klienckie mogą uzyskiwać dostęp tylko do portów zewnętrznych (jeśli istnieją) opublikowanych podczas wdrażania w programie `docker-compose` .</span><span class="sxs-lookup"><span data-stu-id="bfab2-139">Client apps can access only the external ports (if any) published when deploying with `docker-compose`.</span></span>

<span data-ttu-id="bfab2-140">Tych portów zewnętrznych nie należy publikować podczas wdrażania w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="bfab2-140">Those external ports shouldn't be published when deploying to a production environment.</span></span> <span data-ttu-id="bfab2-141">Z tego względu, dlaczego chcesz użyć bramy interfejsu API, aby uniknąć bezpośredniej komunikacji między aplikacjami klienckimi i mikrousługami.</span><span class="sxs-lookup"><span data-stu-id="bfab2-141">For this specific reason, why you want to use the API Gateway, to avoid the direct communication between the client apps and the microservices.</span></span>

<span data-ttu-id="bfab2-142">Jednak podczas tworzenia programu chcesz bezpośrednio uzyskać dostęp do mikrousługi/kontenera i uruchomić go za pomocą struktury Swagger.</span><span class="sxs-lookup"><span data-stu-id="bfab2-142">However, when developing, you want to access the microservice/container directly and run it through Swagger.</span></span> <span data-ttu-id="bfab2-143">Dlatego w eShopOnContainers, porty zewnętrzne są nadal określone nawet wtedy, gdy nie będą używane przez bramę interfejsu API ani aplikacje klienckie.</span><span class="sxs-lookup"><span data-stu-id="bfab2-143">That's why in eShopOnContainers, the external ports are still specified even when they won't be used by the API Gateway or the client apps.</span></span>

<span data-ttu-id="bfab2-144">Oto przykład `docker-compose.override.yml` pliku dla mikrousługi katalogu:</span><span class="sxs-lookup"><span data-stu-id="bfab2-144">Here's an example of the `docker-compose.override.yml` file for the Catalog microservice:</span></span>

```yml
catalog-api:
  environment:
    - ASPNETCORE_ENVIRONMENT=Development
    - ASPNETCORE_URLS=http://0.0.0.0:80
    - ConnectionString=YOUR_VALUE
    - ... Other Environment Variables
  ports:
    - "5101:80"   # Important: In a production environment you should remove the external port (5101) kept here for microservice debugging purposes.
                  # The API Gateway redirects and access through the internal port (80).
```

<span data-ttu-id="bfab2-145">Można zobaczyć, jak w konfiguracji Docker-Compose. override. yml port wewnętrzny dla kontenera wykazu jest portem 80, ale Port dostępu zewnętrznego to 5101.</span><span class="sxs-lookup"><span data-stu-id="bfab2-145">You can see how in the docker-compose.override.yml configuration the internal port for the Catalog container is port 80, but the port for external access is 5101.</span></span> <span data-ttu-id="bfab2-146">Jednak ten port nie powinien być używany przez aplikację podczas korzystania z bramy interfejsu API, tylko do debugowania, uruchamiania i testowania tylko mikrousługi katalogu.</span><span class="sxs-lookup"><span data-stu-id="bfab2-146">But this port shouldn't be used by the application when using an API Gateway, only to debug, run, and test just the Catalog microservice.</span></span>

<span data-ttu-id="bfab2-147">Zwykle nie jest wdrażana przy użyciu platformy Docker — tworzenie w środowisku produkcyjnym, ponieważ odpowiednie środowisko wdrażania w środowisku produkcyjnym dla mikrousług jest koordynatorem, takim jak Kubernetes lub Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="bfab2-147">Normally, you won't be deploying with docker-compose into a production environment because the right production deployment environment for microservices is an orchestrator like Kubernetes or Service Fabric.</span></span> <span data-ttu-id="bfab2-148">W przypadku wdrażania w środowiskach korzystających z różnych plików konfiguracji, w których nie można publikować bezpośrednio żadnych portów zewnętrznych dla mikrousług, ale zawsze będziesz używać zwrotnego serwera proxy z bramy interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="bfab2-148">When deploying to those environments you use different configuration files where you won't publish directly any external port for the microservices but, you'll always use the reverse proxy from the API Gateway.</span></span>

<span data-ttu-id="bfab2-149">Uruchom mikrousługę katalogu na lokalnym hoście platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="bfab2-149">Run the catalog microservice in your local Docker host.</span></span> <span data-ttu-id="bfab2-150">Uruchom pełne rozwiązanie eShopOnContainers z programu Visual Studio (uruchamia wszystkie usługi w plikach do redagowania w systemie Docker) lub Uruchom mikrousługę za pomocą następującego polecenia Docker-Zredaguj w programie CMD lub programie PowerShell umieszczonym w folderze, w którym `docker-compose.yml` `docker-compose.override.yml` są umieszczone i.</span><span class="sxs-lookup"><span data-stu-id="bfab2-150">Either run the full eShopOnContainers solution from Visual Studio (it runs all the services in the docker-compose files), or start the Catalog microservice with the following docker-compose command in CMD or PowerShell positioned at the folder where the `docker-compose.yml` and `docker-compose.override.yml` are placed.</span></span>

```console
docker-compose run --service-ports catalog-api
```

<span data-ttu-id="bfab2-151">To polecenie uruchamia tylko kontener usługi Catalog-API i zależności, które są określone w Docker-Compose. yml.</span><span class="sxs-lookup"><span data-stu-id="bfab2-151">This command only runs the catalog-api service container plus dependencies that are specified in the docker-compose.yml.</span></span> <span data-ttu-id="bfab2-152">W tym przypadku kontener SQL Server i kontener RabbitMQ.</span><span class="sxs-lookup"><span data-stu-id="bfab2-152">In this case, the SQL Server container and RabbitMQ container.</span></span>

<span data-ttu-id="bfab2-153">Następnie można bezpośrednio uzyskać dostęp do mikrousługi katalogu i wyświetlić jej metody za pomocą interfejsu użytkownika programu Swagger, uzyskując dostęp bezpośrednio przez ten port "zewnętrzny", w tym przypadku `http://localhost:5101/swagger` :</span><span class="sxs-lookup"><span data-stu-id="bfab2-153">Then, you can directly access the Catalog microservice and see its methods through the Swagger UI accessing directly through that "external" port, in this case `http://localhost:5101/swagger`:</span></span>

![Zrzut ekranu przedstawiający interfejs użytkownika struktury Swagger z interfejsem API REST katalogu. API.](./media/implement-api-gateways-with-ocelot/test-catalog-microservice.png)

<span data-ttu-id="bfab2-155">**Rysunek 6-31**.</span><span class="sxs-lookup"><span data-stu-id="bfab2-155">**Figure 6-31**.</span></span> <span data-ttu-id="bfab2-156">Testowanie mikrousługi katalogu za pomocą interfejsu użytkownika struktury Swagger</span><span class="sxs-lookup"><span data-stu-id="bfab2-156">Testing the Catalog microservice with its Swagger UI</span></span>

<span data-ttu-id="bfab2-157">W tym momencie można ustawić punkt przerwania w kodzie C# w programie Visual Studio, przetestować mikrousługę przy użyciu metod udostępnianych w interfejsie użytkownika programu Swagger, a wreszcie oczyścić wszystko za pomocą `docker-compose down` polecenia.</span><span class="sxs-lookup"><span data-stu-id="bfab2-157">At this point, you could set a breakpoint in C# code in Visual Studio, test the microservice with the methods exposed in Swagger UI, and finally clean-up everything with the `docker-compose down` command.</span></span>

<span data-ttu-id="bfab2-158">Jednak bezpośredni dostęp do mikrousługi, w tym przypadku przez port zewnętrzny 5101, jest dokładnie to, co chcesz uniknąć w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bfab2-158">However, direct-access communication to the microservice, in this case through the external port 5101, is precisely what you want to avoid in your application.</span></span> <span data-ttu-id="bfab2-159">Można uniknąć tego przez ustawienie dodatkowego poziomu pośredniego dla bramy interfejsu API (w tym przypadku Ocelot).</span><span class="sxs-lookup"><span data-stu-id="bfab2-159">And you can avoid that by setting the additional level of indirection of the API Gateway (Ocelot, in this case).</span></span> <span data-ttu-id="bfab2-160">Dzięki temu aplikacja kliencka nie będzie bezpośrednio uzyskiwać dostępu do mikrousługi.</span><span class="sxs-lookup"><span data-stu-id="bfab2-160">That way, the client app won't directly access the microservice.</span></span>

## <a name="implementing-your-api-gateways-with-ocelot"></a><span data-ttu-id="bfab2-161">Implementowanie bram interfejsu API za pomocą usługi Ocelot</span><span class="sxs-lookup"><span data-stu-id="bfab2-161">Implementing your API Gateways with Ocelot</span></span>

<span data-ttu-id="bfab2-162">Ocelot jest zasadniczo zestawem middlewares, który można zastosować w określonej kolejności.</span><span class="sxs-lookup"><span data-stu-id="bfab2-162">Ocelot is basically a set of middlewares that you can apply in a specific order.</span></span>

<span data-ttu-id="bfab2-163">Ocelot jest przeznaczona do pracy tylko z ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="bfab2-163">Ocelot is designed to work with ASP.NET Core only.</span></span> <span data-ttu-id="bfab2-164">Najnowsza wersja obiektów docelowych pakietu `.NETCoreApp 3.1` , dlatego nie jest odpowiednia dla .NET Framework aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bfab2-164">The latest version of the package targets `.NETCoreApp 3.1` and hence it is not suitable for .NET Framework applications.</span></span>

<span data-ttu-id="bfab2-165">Program Visual Studio umożliwia zainstalowanie Ocelot i jego zależności w projekcie ASP.NET Core z [pakietem NuGet Ocelot](https://www.nuget.org/packages/Ocelot/).</span><span class="sxs-lookup"><span data-stu-id="bfab2-165">You install Ocelot and its dependencies in your ASP.NET Core project with [Ocelot's NuGet package](https://www.nuget.org/packages/Ocelot/), from Visual Studio.</span></span>

```powershell
Install-Package Ocelot
```

<span data-ttu-id="bfab2-166">W eShopOnContainers, jej implementacja bramy interfejsu API to ASP.NET Core prosty projekt usługi WebHost, a Ocelot oprogramowanie pośredniczące obsługuje wszystkie funkcje bramy interfejsu API, jak pokazano na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="bfab2-166">In eShopOnContainers, its API Gateway implementation is a simple ASP.NET Core WebHost project, and Ocelot’s middleware handles all the API Gateway features, as shown in the following image:</span></span>

![Zrzut ekranu przedstawiający Eksplorator rozwiązań pokazujący projekt bramy interfejsu API Ocelot.](./media/implement-api-gateways-with-ocelot/ocelotapigw-base-project.png)

<span data-ttu-id="bfab2-168">**Rysunek 6-32**.</span><span class="sxs-lookup"><span data-stu-id="bfab2-168">**Figure 6-32**.</span></span> <span data-ttu-id="bfab2-169">Projekt podstawowy OcelotApiGw w eShopOnContainers</span><span class="sxs-lookup"><span data-stu-id="bfab2-169">The OcelotApiGw base project in eShopOnContainers</span></span>

<span data-ttu-id="bfab2-170">Ten ASP.NET Core Project WebHost został skompilowany przy użyciu dwóch prostych plików:  `Program.cs` i `Startup.cs` .</span><span class="sxs-lookup"><span data-stu-id="bfab2-170">This ASP.NET Core WebHost project is built with two simple files:  `Program.cs` and `Startup.cs`.</span></span>

<span data-ttu-id="bfab2-171">Program.cs musi utworzyć i skonfigurować typowe ASP.NET Core BuildWebHost.</span><span class="sxs-lookup"><span data-stu-id="bfab2-171">The Program.cs just needs to create and configure the typical ASP.NET Core BuildWebHost.</span></span>

```csharp
namespace OcelotApiGw
{
    public class Program
    {
        public static void Main(string[] args)
        {
            BuildWebHost(args).Run();
        }

        public static IWebHost BuildWebHost(string[] args)
        {
            var builder = WebHost.CreateDefaultBuilder(args);

            builder.ConfigureServices(s => s.AddSingleton(builder))
                    .ConfigureAppConfiguration(
                          ic => ic.AddJsonFile(Path.Combine("configuration",
                                                            "configuration.json")))
                    .UseStartup<Startup>();
            var host = builder.Build();
            return host;
        }
    }
}
```

<span data-ttu-id="bfab2-172">Ważnym punktem dla Ocelot jest `configuration.json` plik, który należy dostarczyć do konstruktora za pomocą `AddJsonFile()` metody.</span><span class="sxs-lookup"><span data-stu-id="bfab2-172">The important point here for Ocelot is the `configuration.json` file that you must provide to the builder through the `AddJsonFile()` method.</span></span> <span data-ttu-id="bfab2-173">W tym `configuration.json` miejscu należy określić wszystkie przekierowania bramy interfejsu API, co oznacza, że zewnętrzne punkty końcowe z określonymi portami i skorelowane wewnętrzne punkty końcowe zwykle korzystają z różnych portów.</span><span class="sxs-lookup"><span data-stu-id="bfab2-173">That `configuration.json` is where you specify all the API Gateway ReRoutes, meaning the external endpoints with specific ports and the correlated internal endpoints, usually using different ports.</span></span>

```json
{
    "ReRoutes": [],
    "GlobalConfiguration": {}
}
```

<span data-ttu-id="bfab2-174">Do konfiguracji należą dwie sekcje.</span><span class="sxs-lookup"><span data-stu-id="bfab2-174">There are two sections to the configuration.</span></span> <span data-ttu-id="bfab2-175">Tablica retras i GlobalConfiguration.</span><span class="sxs-lookup"><span data-stu-id="bfab2-175">An array of ReRoutes and a GlobalConfiguration.</span></span> <span data-ttu-id="bfab2-176">Przekierowania są obiektami, które informują Ocelot o sposobie traktowania żądania nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="bfab2-176">The ReRoutes are the objects that tell Ocelot how to treat an upstream request.</span></span> <span data-ttu-id="bfab2-177">Konfiguracja globalna umożliwia przesłonięcia przekierowania określonych ustawień.</span><span class="sxs-lookup"><span data-stu-id="bfab2-177">The Global configuration allows overrides of ReRoute specific settings.</span></span> <span data-ttu-id="bfab2-178">Jest to przydatne, jeśli nie chcesz zarządzać wieloma zmianami poszczególnych ustawień.</span><span class="sxs-lookup"><span data-stu-id="bfab2-178">It's useful if you don't want to manage lots of ReRoute specific settings.</span></span>

<span data-ttu-id="bfab2-179">Poniżej przedstawiono uproszczony przykład [retrasy pliku konfiguracji](https://github.com/dotnet-architecture/eShopOnContainers/blob/master/src/ApiGateways/Web.Bff.Shopping/apigw/configuration.json) z jednej z bram interfejsu API z eShopOnContainers.</span><span class="sxs-lookup"><span data-stu-id="bfab2-179">Here's a simplified example of [ReRoute configuration file](https://github.com/dotnet-architecture/eShopOnContainers/blob/master/src/ApiGateways/Web.Bff.Shopping/apigw/configuration.json) from one of the API Gateways from eShopOnContainers.</span></span>

```json
{
  "ReRoutes": [
    {
      "DownstreamPathTemplate": "/api/{version}/{everything}",
      "DownstreamScheme": "http",
      "DownstreamHostAndPorts": [
        {
          "Host": "catalog-api",
          "Port": 80
        }
      ],
      "UpstreamPathTemplate": "/api/{version}/c/{everything}",
      "UpstreamHttpMethod": [ "POST", "PUT", "GET" ]
    },
    {
      "DownstreamPathTemplate": "/api/{version}/{everything}",
      "DownstreamScheme": "http",
      "DownstreamHostAndPorts": [
        {
          "Host": "basket-api",
          "Port": 80
        }
      ],
      "UpstreamPathTemplate": "/api/{version}/b/{everything}",
      "UpstreamHttpMethod": [ "POST", "PUT", "GET" ],
      "AuthenticationOptions": {
        "AuthenticationProviderKey": "IdentityApiKey",
        "AllowedScopes": []
      }
    }

  ],
    "GlobalConfiguration": {
      "RequestIdKey": "OcRequestId",
      "AdministrationPath": "/administration"
    }
  }
```

<span data-ttu-id="bfab2-180">Główną funkcją bramy interfejsu API Ocelot jest przejęcie przychodzących żądań HTTP i przekazanie ich do usługi podrzędnej, obecnie jako innego żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="bfab2-180">The main functionality of an Ocelot API Gateway is to take incoming HTTP requests and forward them on to a downstream service, currently as another HTTP request.</span></span> <span data-ttu-id="bfab2-181">Ocelot opisuje Routing jednego żądania do innego jako Reroute.</span><span class="sxs-lookup"><span data-stu-id="bfab2-181">Ocelot's describes the routing of one request to another as a ReRoute.</span></span>

<span data-ttu-id="bfab2-182">Na przykład skupmy się na jednym z tras w configuration.jsna podstawie powyższych, konfiguracji mikrousługi koszyka.</span><span class="sxs-lookup"><span data-stu-id="bfab2-182">For instance, let's focus on one of the ReRoutes in the configuration.json from above, the configuration for the Basket microservice.</span></span>

```json
{
      "DownstreamPathTemplate": "/api/{version}/{everything}",
      "DownstreamScheme": "http",
      "DownstreamHostAndPorts": [
        {
          "Host": "basket-api",
          "Port": 80
        }
      ],
      "UpstreamPathTemplate": "/api/{version}/b/{everything}",
      "UpstreamHttpMethod": [ "POST", "PUT", "GET" ],
      "AuthenticationOptions": {
        "AuthenticationProviderKey": "IdentityApiKey",
        "AllowedScopes": []
      }
}
```

<span data-ttu-id="bfab2-183">DownstreamPathTemplate, schemat i DownstreamHostAndPorts tworzą wewnętrzny adres URL mikrousług, do którego zostanie przesłane żądanie.</span><span class="sxs-lookup"><span data-stu-id="bfab2-183">The DownstreamPathTemplate, Scheme, and DownstreamHostAndPorts make the internal microservice URL that this request will be forwarded to.</span></span>

<span data-ttu-id="bfab2-184">Port jest portem wewnętrznym używanym przez usługę.</span><span class="sxs-lookup"><span data-stu-id="bfab2-184">The port is the internal port used by the service.</span></span> <span data-ttu-id="bfab2-185">W przypadku korzystania z kontenerów port określony w pliku dockerfile.</span><span class="sxs-lookup"><span data-stu-id="bfab2-185">When using containers, the port specified at its dockerfile.</span></span>

<span data-ttu-id="bfab2-186">`Host`Jest nazwą usługi, która zależy od używanego rozwiązania nazwy usługi.</span><span class="sxs-lookup"><span data-stu-id="bfab2-186">The `Host` is a service name that depends on the service name resolution you are using.</span></span> <span data-ttu-id="bfab2-187">W przypadku korzystania z platformy Docker — Tworzenie nazw usług są udostępniane przez hosta platformy Docker, który korzysta z nazw usług udostępnianych w plikach tworzenia platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="bfab2-187">When using docker-compose, the services names are provided by the Docker Host, which is using the service names provided in the docker-compose files.</span></span> <span data-ttu-id="bfab2-188">W przypadku korzystania z programu Orchestrator, takiego jak Kubernetes lub Service Fabric, ta nazwa powinna być rozpoznawana przez system DNS lub rozpoznawanie nazw dostarczone przez każdego koordynatora.</span><span class="sxs-lookup"><span data-stu-id="bfab2-188">If using an orchestrator like Kubernetes or Service Fabric, that name should be resolved by the DNS or name resolution provided by each orchestrator.</span></span>

<span data-ttu-id="bfab2-189">DownstreamHostAndPorts to tablica zawierająca hosta i port wszystkich usług podrzędnych, do których mają być przekazywane żądania.</span><span class="sxs-lookup"><span data-stu-id="bfab2-189">DownstreamHostAndPorts is an array that contains the host and port of any downstream services that you wish to forward requests to.</span></span> <span data-ttu-id="bfab2-190">Zwykle ta konfiguracja będzie zawierać jeden wpis, ale czasami może zajść potrzeba zrównoważenia obciążenia żądaniami do usług podrzędnych i Ocelot umożliwia dodanie więcej niż jednego wpisu, a następnie wybranie modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="bfab2-190">Usually this configuration will just contain one entry but sometimes you might want to load balance requests to your downstream services and Ocelot lets you add more than one entry and then select a load balancer.</span></span> <span data-ttu-id="bfab2-191">Ale jeśli korzystasz z platformy Azure i dowolnego programu Orchestrator, prawdopodobnie lepszym rozwiązaniem jest zrównoważenie równoważenia obciążenia za pomocą infrastruktury chmury i programu Orchestrator.</span><span class="sxs-lookup"><span data-stu-id="bfab2-191">But if using Azure and any orchestrator it is probably a better idea to load balance with the cloud and orchestrator infrastructure.</span></span>

<span data-ttu-id="bfab2-192">UpstreamPathTemplate to adres URL, który będzie używany przez Ocelot do identyfikowania DownstreamPathTemplate do użycia dla danego żądania od klienta.</span><span class="sxs-lookup"><span data-stu-id="bfab2-192">The UpstreamPathTemplate is the URL that Ocelot will use to identify which DownstreamPathTemplate to use for a given request from the client.</span></span> <span data-ttu-id="bfab2-193">Na koniec UpstreamHttpMethod jest używany, więc Ocelot może rozróżnić różne żądania (GET, POST, PUT) na ten sam adres URL.</span><span class="sxs-lookup"><span data-stu-id="bfab2-193">Finally, the UpstreamHttpMethod is used so Ocelot can distinguish between different requests (GET, POST, PUT) to the same URL.</span></span>

<span data-ttu-id="bfab2-194">W tym momencie można korzystać z pojedynczej bramy interfejsu API Ocelot (ASP.NET Core WebHost) przy użyciu jednego lub [wielu scalonych configuration.jsna plikach](https://ocelot.readthedocs.io/en/latest/features/configuration.html#merging-configuration-files) lub można również przechowywać [konfigurację w magazynie Consul KV](https://ocelot.readthedocs.io/en/latest/features/configuration.html#store-configuration-in-consul).</span><span class="sxs-lookup"><span data-stu-id="bfab2-194">At this point, you could have a single Ocelot API Gateway (ASP.NET Core WebHost) using one or [multiple merged configuration.json files](https://ocelot.readthedocs.io/en/latest/features/configuration.html#merging-configuration-files) or you can also store the [configuration in a Consul KV store](https://ocelot.readthedocs.io/en/latest/features/configuration.html#store-configuration-in-consul).</span></span>

<span data-ttu-id="bfab2-195">Jeśli jednak na pewno chcesz mieć autonomiczne mikrousługi, jak zostało to opisane w sekcji architektura i projekt, lepiej jest podzielić tę jednolite bramy interfejsu API na wiele bram interfejsu API i/lub BFF (zaplecza dla frontonu).</span><span class="sxs-lookup"><span data-stu-id="bfab2-195">But as introduced in the architecture and design sections, if you really want to have autonomous microservices, it might be better to split that single monolithic API Gateway into multiple API Gateways and/or BFF (Backend for Frontend).</span></span> <span data-ttu-id="bfab2-196">W tym celu Zobaczmy, jak zaimplementować to podejście przy użyciu kontenerów platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="bfab2-196">For that purpose, let's see how to implement that approach with Docker containers.</span></span>

### <a name="using-a-single-docker-container-image-to-run-multiple-different-api-gateway--bff-container-types"></a><span data-ttu-id="bfab2-197">Używanie pojedynczego obrazu kontenera Docker do uruchamiania wielu różnych typów kontenerów bramy interfejsu API/BFF</span><span class="sxs-lookup"><span data-stu-id="bfab2-197">Using a single Docker container image to run multiple different API Gateway / BFF container types</span></span>

<span data-ttu-id="bfab2-198">W eShopOnContainers korzystamy z jednego obrazu kontenera Docker z bramą interfejsu API Ocelot, a następnie w czasie wykonywania utworzymy różne usługi/kontenery dla każdego typu interfejsu API-Gateway/BFF, dostarczając inny configuration.jsw pliku przy użyciu woluminu platformy Docker w celu uzyskania dostępu do innego folderu komputera dla każdej usługi.</span><span class="sxs-lookup"><span data-stu-id="bfab2-198">In eShopOnContainers, we're using a single Docker container image with the Ocelot API Gateway but then, at run time, we create different services/containers for each type of API-Gateway/BFF by providing a different configuration.json file, using a docker volume to access a different PC folder for each service.</span></span>

![Diagram jednego obrazu platformy Docker bramy Ocelot dla wszystkich bram interfejsu API.](./media/implement-api-gateways-with-ocelot/reusing-single-ocelot-docker-image.png)

<span data-ttu-id="bfab2-200">**Rysunek 6-33**.</span><span class="sxs-lookup"><span data-stu-id="bfab2-200">**Figure 6-33**.</span></span> <span data-ttu-id="bfab2-201">Wielokrotne używanie pojedynczego obrazu platformy Docker Ocelot w wielu typach bram interfejsu API</span><span class="sxs-lookup"><span data-stu-id="bfab2-201">Reusing a single Ocelot Docker image across multiple API Gateway types</span></span>

<span data-ttu-id="bfab2-202">W eShopOnContainers "ogólny obraz bramy interfejsu API Docker" jest tworzony przy użyciu projektu o nazwie "OcelotApiGw" i nazwy obrazu "eshop/OcelotApiGw", która jest określona w pliku Docker-Compose. yml.</span><span class="sxs-lookup"><span data-stu-id="bfab2-202">In eShopOnContainers, the "Generic Ocelot API Gateway Docker Image" is created with the project named 'OcelotApiGw' and the image name "eshop/ocelotapigw" that is specified in the docker-compose.yml file.</span></span> <span data-ttu-id="bfab2-203">Po wdrożeniu do platformy Docker będzie dostępnych cztery API-Gateway kontenerów utworzonych na podstawie tego samego obrazu platformy Docker, jak pokazano w poniższym wyodrębnieniu z pliku Docker-Compose. yml.</span><span class="sxs-lookup"><span data-stu-id="bfab2-203">Then, when deploying to Docker, there will be four API-Gateway containers created from that same Docker image, as shown in the following extract from the docker-compose.yml file.</span></span>

```yml
  mobileshoppingapigw:
    image: eshop/ocelotapigw:${TAG:-latest}
    build:
      context: .
      dockerfile: src/ApiGateways/ApiGw-Base/Dockerfile

  mobilemarketingapigw:
    image: eshop/ocelotapigw:${TAG:-latest}
    build:
      context: .
      dockerfile: src/ApiGateways/ApiGw-Base/Dockerfile

  webshoppingapigw:
    image: eshop/ocelotapigw:${TAG:-latest}
    build:
      context: .
      dockerfile: src/ApiGateways/ApiGw-Base/Dockerfile

  webmarketingapigw:
    image: eshop/ocelotapigw:${TAG:-latest}
    build:
      context: .
      dockerfile: src/ApiGateways/ApiGw-Base/Dockerfile
```

<span data-ttu-id="bfab2-204">Ponadto, jak widać w poniższym pliku Docker-Compose. override. yml, jedyną różnicą między tymi kontenerami bramy interfejsu API jest plik konfiguracji Ocelot, który jest inny dla każdego kontenera usługi i został określony w czasie wykonywania za pomocą woluminu platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="bfab2-204">Additionally, as you can see in the following docker-compose.override.yml file, the only difference between those API Gateway containers is the Ocelot configuration file, which is different for each service container and it's specified at runtime through a Docker volume.</span></span>

```yml
mobileshoppingapigw:
  environment:
    - ASPNETCORE_ENVIRONMENT=Development
    - IdentityUrl=http://identity-api
  ports:
    - "5200:80"
  volumes:
    - ./src/ApiGateways/Mobile.Bff.Shopping/apigw:/app/configuration

mobilemarketingapigw:
  environment:
    - ASPNETCORE_ENVIRONMENT=Development
    - IdentityUrl=http://identity-api
  ports:
    - "5201:80"
  volumes:
    - ./src/ApiGateways/Mobile.Bff.Marketing/apigw:/app/configuration

webshoppingapigw:
  environment:
    - ASPNETCORE_ENVIRONMENT=Development
    - IdentityUrl=http://identity-api
  ports:
    - "5202:80"
  volumes:
    - ./src/ApiGateways/Web.Bff.Shopping/apigw:/app/configuration

webmarketingapigw:
  environment:
    - ASPNETCORE_ENVIRONMENT=Development
    - IdentityUrl=http://identity-api
  ports:
    - "5203:80"
  volumes:
    - ./src/ApiGateways/Web.Bff.Marketing/apigw:/app/configuration
```

<span data-ttu-id="bfab2-205">Ze względu na ten poprzedni kod, jak pokazano w Eksploratorze programu Visual Studio, jedynym plikiem potrzebnym do zdefiniowania każdej konkretnej bramy interfejsu API Business/BFF jest tylko configuration.jsw pliku, ponieważ cztery bramy interfejsu API są oparte na tym samym obrazie platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="bfab2-205">Because of that previous code, and as shown in the Visual Studio Explorer below, the only file needed to define each specific business/BFF API Gateway is just a configuration.json file, because the four API Gateways are based on the same Docker image.</span></span>

![Zrzut ekranu przedstawiający wszystkie bramy interfejsu API z configuration.jsna plikach.](./media/implement-api-gateways-with-ocelot/ocelot-configuration-files.png)

<span data-ttu-id="bfab2-207">**Rysunek 6-34**.</span><span class="sxs-lookup"><span data-stu-id="bfab2-207">**Figure 6-34**.</span></span> <span data-ttu-id="bfab2-208">Jedynym plikiem wymaganym do zdefiniowania każdej usługi API Gateway/BFF z Ocelot jest plik konfiguracji</span><span class="sxs-lookup"><span data-stu-id="bfab2-208">The only file needed to define each API Gateway / BFF with Ocelot is a configuration file</span></span>

<span data-ttu-id="bfab2-209">Dzieląc bramę interfejsu API na wiele bram interfejsu API, różne zespoły programistyczne skupiające się na różnych podzestawach mikrousług mogą zarządzać własnymi bramami interfejsu API za pomocą niezależnych plików konfiguracji Ocelot.</span><span class="sxs-lookup"><span data-stu-id="bfab2-209">By splitting the API Gateway into multiple API Gateways, different development teams focusing on different subsets of microservices can manage their own API Gateways by using independent Ocelot configuration files.</span></span> <span data-ttu-id="bfab2-210">Dodatkowo, w tym samym czasie mogą ponownie użyć tego samego obrazu platformy Docker Ocelot.</span><span class="sxs-lookup"><span data-stu-id="bfab2-210">Plus, at the same time they can reuse the same Ocelot Docker image.</span></span>

<span data-ttu-id="bfab2-211">Teraz, jeśli uruchomisz eShopOnContainers z bramami interfejsu API (zawartymi domyślnie w programie VS podczas otwierania rozwiązania eShopOnContainers-ServicesAndWebApps. sln lub w przypadku uruchamiania funkcji "Docker-Zredaguj up"), zostaną wykonane następujące przykładowe trasy.</span><span class="sxs-lookup"><span data-stu-id="bfab2-211">Now, if you run eShopOnContainers with the API Gateways (included by default in VS when opening eShopOnContainers-ServicesAndWebApps.sln solution or if running "docker-compose up"), the following sample routes will be performed.</span></span>

<span data-ttu-id="bfab2-212">Na przykład podczas odwiedzania nadrzędnego adresu URL `http://localhost:5202/api/v1/c/catalog/items/2/` obsługiwanego przez bramę interfejsu API webshoppingapigw uzyskasz ten sam wynik z wewnętrznego podrzędnego adresu URL `http://catalog-api/api/v1/2` w ramach hosta platformy Docker, jak w poniższej przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="bfab2-212">For instance, when visiting the upstream URL `http://localhost:5202/api/v1/c/catalog/items/2/` served by the webshoppingapigw API Gateway, you get the same result from the internal Downstream URL `http://catalog-api/api/v1/2` within the Docker host, as in the following browser.</span></span>

![Zrzut ekranu przeglądarki wyświetlającej odpowiedź przechodzącą przez bramę interfejsu API.](./media/implement-api-gateways-with-ocelot/access-microservice-through-url.png)

<span data-ttu-id="bfab2-214">**Rysunek 6-35**.</span><span class="sxs-lookup"><span data-stu-id="bfab2-214">**Figure 6-35**.</span></span> <span data-ttu-id="bfab2-215">Uzyskiwanie dostępu do mikrousługi za pomocą adresu URL dostarczonego przez bramę interfejsu API</span><span class="sxs-lookup"><span data-stu-id="bfab2-215">Accessing a microservice through a URL provided by the API Gateway</span></span>

<span data-ttu-id="bfab2-216">Ze względu na testowanie lub debugowanie, jeśli chcesz uzyskać bezpośredni dostęp do kontenera Docker katalogu (tylko w środowisku programistycznym) bez przechodzenia przez bramę interfejsu API, ponieważ "Catalog-API" to rozpoznawanie nazw DNS wewnętrznie dla hosta platformy Docker (Odnajdywanie usług obsługiwane przez nazwy usług platformy Docker), jedynym sposobem uzyskania bezpośredniego dostępu do kontenera jest port zewnętrzny opublikowany w Docker-Compose. override. yml, który jest dostępny tylko dla testów programistycznych, takich jak `http://localhost:5101/api/v1/Catalog/items/1` w poniższej przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="bfab2-216">Because of testing or debugging reasons, if you wanted to directly access to the Catalog Docker container (only at the development environment) without passing through the API Gateway, since 'catalog-api' is a DNS resolution internal to the Docker host (service discovery handled by docker-compose service names), the only way to directly access the container is through the external port published in the docker-compose.override.yml, which is provided only for development tests, such as `http://localhost:5101/api/v1/Catalog/items/1` in the following browser.</span></span>

![Zrzut ekranu przeglądarki wyświetlającej bezpośrednią odpowiedź do katalogu. API.](./media/implement-api-gateways-with-ocelot/direct-access-microservice-testing.png)

<span data-ttu-id="bfab2-218">**Rysunek 6-36**.</span><span class="sxs-lookup"><span data-stu-id="bfab2-218">**Figure 6-36**.</span></span> <span data-ttu-id="bfab2-219">Bezpośredni dostęp do mikrousługi na potrzeby testowania</span><span class="sxs-lookup"><span data-stu-id="bfab2-219">Direct access to a microservice for testing purposes</span></span>

<span data-ttu-id="bfab2-220">Jednak aplikacja jest skonfigurowana, aby uzyskiwać dostęp do wszystkich mikrousług za pośrednictwem bram interfejsu API, a nie za pośrednictwem portu bezpośredniego.</span><span class="sxs-lookup"><span data-stu-id="bfab2-220">But the application is configured so it accesses all the microservices through the API Gateways, not through the direct port "shortcuts".</span></span>

### <a name="the-gateway-aggregation-pattern-in-eshoponcontainers"></a><span data-ttu-id="bfab2-221">Wzorzec agregacji bramy w eShopOnContainers</span><span class="sxs-lookup"><span data-stu-id="bfab2-221">The Gateway aggregation pattern in eShopOnContainers</span></span>

<span data-ttu-id="bfab2-222">Jak wprowadzono wcześniej, elastyczny sposób implementacji agregacji żądań jest z usługami niestandardowymi, przez kod.</span><span class="sxs-lookup"><span data-stu-id="bfab2-222">As introduced previously, a flexible way to implement requests aggregation is with custom services, by code.</span></span> <span data-ttu-id="bfab2-223">Można również zaimplementować agregację żądań za pomocą [funkcji agregacji żądań w Ocelot](https://ocelot.readthedocs.io/en/latest/features/requestaggregation.html#request-aggregation), ale może to być niepotrzebne.</span><span class="sxs-lookup"><span data-stu-id="bfab2-223">You could also implement request aggregation with the [Request Aggregation feature in Ocelot](https://ocelot.readthedocs.io/en/latest/features/requestaggregation.html#request-aggregation), but it might not be as flexible as you need.</span></span> <span data-ttu-id="bfab2-224">W związku z tym wybrany sposób implementacji agregacji w eShopOnContainers jest z jawnym ASP.NET Core usługą interfejsu API sieci Web dla każdego agregatora.</span><span class="sxs-lookup"><span data-stu-id="bfab2-224">Therefore, the selected way to implement aggregation in eShopOnContainers is with an explicit ASP.NET Core Web API service for each aggregator.</span></span>

<span data-ttu-id="bfab2-225">Zgodnie z tym podejściem diagram kompozycji bramy interfejsu API jest w rzeczywistości bardziej rozszerzony podczas rozważania usług agregatora, które nie są wyświetlane w uproszczonym, globalnym diagramie architektury.</span><span class="sxs-lookup"><span data-stu-id="bfab2-225">According to that approach, the API Gateway composition diagram is in reality a bit more extended when considering the aggregator services that are not shown in the simplified global architecture diagram shown previously.</span></span>

<span data-ttu-id="bfab2-226">Na poniższym diagramie można także zobaczyć, jak usługi agregatora współpracują z odpowiednimi bramami interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="bfab2-226">In the following diagram, you can also see how the aggregator services work with their related API Gateways.</span></span>

![Diagram architektury eShopOnContainers, w którym są wyświetlane usługi agregatora.](./media/implement-api-gateways-with-ocelot/eshoponcontainers-architecture-aggregator-services.png)

<span data-ttu-id="bfab2-228">**Rysunek 6-37**.</span><span class="sxs-lookup"><span data-stu-id="bfab2-228">**Figure 6-37**.</span></span> <span data-ttu-id="bfab2-229">Architektura eShopOnContainers z usługami agregatora</span><span class="sxs-lookup"><span data-stu-id="bfab2-229">eShopOnContainers architecture with aggregator services</span></span>

<span data-ttu-id="bfab2-230">Dalsze powiększanie, w obszarze roboczym "zakupy" na poniższej ilustracji widać, że chattiness między aplikacjami klienckimi i mikrousługami zostanie zredukowany w przypadku korzystania z usług agregatora w bramach interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="bfab2-230">Zooming in further, on the "Shopping" business area in the following image, you can see that chattiness between the client apps and the microservices is reduced when using the aggregator services in the API Gateways.</span></span>

![Diagram przedstawiający powiększenie architektury eShopOnContainers.](./media/implement-api-gateways-with-ocelot/zoom-in-vision-aggregator-services.png)

<span data-ttu-id="bfab2-232">**Rysunek 6-38**.</span><span class="sxs-lookup"><span data-stu-id="bfab2-232">**Figure 6-38**.</span></span> <span data-ttu-id="bfab2-233">Powiększ zalety usług agregatora</span><span class="sxs-lookup"><span data-stu-id="bfab2-233">Zoom in vision of the Aggregator services</span></span>

<span data-ttu-id="bfab2-234">Można zauważyć, jak gdy diagram pokazuje możliwe żądania pochodzące z bram interfejsu API, które mogą być złożone.</span><span class="sxs-lookup"><span data-stu-id="bfab2-234">You can notice how when the diagram shows the possible requests coming from the API Gateways it can get complex.</span></span> <span data-ttu-id="bfab2-235">Z drugiej strony, gdy używasz wzorca agregatora, zobaczysz, jak strzałki w kolorze niebieskim upraszczają komunikację z perspektywy aplikacji klienckiej.</span><span class="sxs-lookup"><span data-stu-id="bfab2-235">On the other hand, when you use the aggregator pattern, you can see how the arrows in blue would simplify the communication from a client app perspective.</span></span> <span data-ttu-id="bfab2-236">Ten wzorzec nie tylko pomaga ograniczyć chattiness i opóźnień w komunikacji, ale również znacznie poprawia środowisko użytkownika dla aplikacji zdalnych (aplikacji mobilnych i SPA).</span><span class="sxs-lookup"><span data-stu-id="bfab2-236">This pattern not only helps to reduce the chattiness and latency in the communication, it also improves the user experience significantly for the remote apps (mobile and SPA apps).</span></span>

<span data-ttu-id="bfab2-237">W przypadku obszaru biznesowego "Marketing" i mikrousług jest to prosty przypadek użycia, dlatego nie ma potrzeby korzystania z agregatorów, ale może również być możliwe, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="bfab2-237">In the case of the "Marketing" business area and microservices, it is a simple use case so there was no need to use aggregators, but it could also be possible, if needed.</span></span>

### <a name="authentication-and-authorization-in-ocelot-api-gateways"></a><span data-ttu-id="bfab2-238">Uwierzytelnianie i autoryzacja w bramach interfejsu API Ocelot</span><span class="sxs-lookup"><span data-stu-id="bfab2-238">Authentication and authorization in Ocelot API Gateways</span></span>

<span data-ttu-id="bfab2-239">W bramie interfejsu API Ocelot można korzystać z usługi uwierzytelniania, takiej jak usługa interfejsu API sieci Web ASP.NET Core przy użyciu [IdentityServer](https://identityserver.io/) , dostarczając token uwierzytelniania lub wewnątrz bramy interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="bfab2-239">In an Ocelot API Gateway you can sit the authentication service, such as an ASP.NET Core Web API service using [IdentityServer](https://identityserver.io/) providing the auth token, either out or inside the API Gateway.</span></span>

<span data-ttu-id="bfab2-240">Ponieważ eShopOnContainers korzysta z wielu bram interfejsu API z granicami opartymi na obszarach BFF i firmowych, Usługa tożsamość/uwierzytelnianie pozostaje poza bramami interfejsu API, jak zostało to wyróżnione na żółto na poniższym diagramie.</span><span class="sxs-lookup"><span data-stu-id="bfab2-240">Since eShopOnContainers is using multiple API Gateways with boundaries based on BFF and business areas, the Identity/Auth service is left out of the API Gateways, as highlighted in yellow in the following diagram.</span></span>

![Diagram przedstawiający mikrousługę tożsamości poniżej bramy interfejsu API.](./media/implement-api-gateways-with-ocelot/eshoponcontainers-identity-service-position.png)

<span data-ttu-id="bfab2-242">**Rysunek 6-39**.</span><span class="sxs-lookup"><span data-stu-id="bfab2-242">**Figure 6-39**.</span></span> <span data-ttu-id="bfab2-243">Pozycja usługi tożsamości w eShopOnContainers</span><span class="sxs-lookup"><span data-stu-id="bfab2-243">Position of the Identity service in eShopOnContainers</span></span>

<span data-ttu-id="bfab2-244">Jednak Ocelot obsługuje także rolę mikrousługi tożsamości/uwierzytelniania w ramach granicy bramy interfejsu API, tak jak w przypadku tego innego diagramu.</span><span class="sxs-lookup"><span data-stu-id="bfab2-244">However, Ocelot also supports sitting the Identity/Auth microservice within the API Gateway boundary, as in this other diagram.</span></span>

![Diagram przedstawiający uwierzytelnianie w bramie interfejsu API Ocelot.](./media/implement-api-gateways-with-ocelot/ocelot-authentication.png)

<span data-ttu-id="bfab2-246">**Rysunek 6-40**.</span><span class="sxs-lookup"><span data-stu-id="bfab2-246">**Figure 6-40**.</span></span> <span data-ttu-id="bfab2-247">Uwierzytelnianie w Ocelot</span><span class="sxs-lookup"><span data-stu-id="bfab2-247">Authentication in Ocelot</span></span>

<span data-ttu-id="bfab2-248">Jak pokazano na poprzednim diagramie, gdy mikrousługa tożsamości znajduje się poniżej bramy API Gateway (AG): 1), usługa AG żąda tokenu uwierzytelniania od mikrousługi tożsamości, 2) usługa Identity-Service zwraca token do AG, 3-4), żądania od mikrousług przy użyciu tokenu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="bfab2-248">As the previous diagram shows, when the Identity microservice is beneath the API gateway (AG): 1) AG requests an auth token from identity microservice, 2) The identity microservice returns token to AG, 3-4) AG requests from microservices using the auth token.</span></span> <span data-ttu-id="bfab2-249">Ponieważ aplikacja eShopOnContainers podzieliła bramę interfejsu API na wiele BFF (zaplecza dla frontonu) i firmowych bram interfejsu API, kolejną opcją jest utworzenie dodatkowej bramy interfejsu API dla zagadnień związanych z wycinaniem.</span><span class="sxs-lookup"><span data-stu-id="bfab2-249">Because eShopOnContainers application has split the API Gateway into multiple BFF (Backend for Frontend) and business areas API Gateways, another option would have been to create an additional API Gateway for cross-cutting concerns.</span></span> <span data-ttu-id="bfab2-250">Wybór ten byłby atrakcyjny w bardziej złożonej architekturze opartej na mikrousługach z wieloma usługami.</span><span class="sxs-lookup"><span data-stu-id="bfab2-250">That choice would be fair in a more complex microservice based architecture with multiple cross-cutting concerns microservices.</span></span> <span data-ttu-id="bfab2-251">Ponieważ w eShopOnContainers występuje tylko jeden problem z wycinaniem, to zdecydowano o prostu obsłużyć usługę zabezpieczeń z obszaru bramy interfejsu API w celu uproszczenia.</span><span class="sxs-lookup"><span data-stu-id="bfab2-251">Since there's only one cross-cutting concern in eShopOnContainers, it was decided to just handle the security service out of the API Gateway realm, for simplicity's sake.</span></span>

<span data-ttu-id="bfab2-252">W każdym przypadku, jeśli aplikacja jest zabezpieczona na poziomie bramy interfejsu API, moduł uwierzytelniania bramy interfejsu API Ocelot jest najpierw odwiedzany przy próbie użycia dowolnej zabezpieczonej mikrousługi.</span><span class="sxs-lookup"><span data-stu-id="bfab2-252">In any case, if the app is secured at the API Gateway level, the authentication module of the Ocelot API Gateway is visited at first when trying to use any secured microservice.</span></span> <span data-ttu-id="bfab2-253">Przekierowuje żądanie HTTP do odwiedzania tożsamości lub mikrousługi uwierzytelniania w celu uzyskania tokenu dostępu, aby można było odwiedzić chronione usługi przy użyciu access_token.</span><span class="sxs-lookup"><span data-stu-id="bfab2-253">That redirects the HTTP request to visit the Identity or auth microservice to get the access token so you can visit the protected services with the access_token.</span></span>

<span data-ttu-id="bfab2-254">Sposób zabezpieczania przy użyciu uwierzytelniania każdej usługi na poziomie bramy interfejsu API polega na ustawieniu AuthenticationProviderKey w ustawieniach pokrewnych w configuration.js.</span><span class="sxs-lookup"><span data-stu-id="bfab2-254">The way you secure with authentication any service at the API Gateway level is by setting the AuthenticationProviderKey in its related settings at the configuration.json.</span></span>

```json
    {
      "DownstreamPathTemplate": "/api/{version}/{everything}",
      "DownstreamScheme": "http",
      "DownstreamHostAndPorts": [
        {
          "Host": "basket-api",
          "Port": 80
        }
      ],
      "UpstreamPathTemplate": "/api/{version}/b/{everything}",
      "UpstreamHttpMethod": [],
      "AuthenticationOptions": {
        "AuthenticationProviderKey": "IdentityApiKey",
        "AllowedScopes": []
      }
    }
```

<span data-ttu-id="bfab2-255">Po uruchomieniu Ocelot zostanie wyświetlona wartość reroutes AuthenticationOptions. AuthenticationProviderKey i sprawdź, czy istnieje dostawca uwierzytelniania zarejestrowany dla danego klucza.</span><span class="sxs-lookup"><span data-stu-id="bfab2-255">When Ocelot runs, it will look at the ReRoutes AuthenticationOptions.AuthenticationProviderKey and check that there is an Authentication Provider registered with the given key.</span></span> <span data-ttu-id="bfab2-256">Jeśli nie, to Ocelot nie zostanie uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="bfab2-256">If there isn't, then Ocelot will not start up.</span></span> <span data-ttu-id="bfab2-257">Jeśli istnieje, wówczas retrasa użyje tego dostawcy, gdy zostanie on wykonany.</span><span class="sxs-lookup"><span data-stu-id="bfab2-257">If there is, then the ReRoute will use that provider when it executes.</span></span>

<span data-ttu-id="bfab2-258">Ponieważ Ocelot WebHost jest skonfigurowany przy użyciu programu `authenticationProviderKey = "IdentityApiKey"` , który będzie wymagał uwierzytelniania zawsze, gdy ta usługa ma jakiekolwiek żądania bez tokenu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="bfab2-258">Because the Ocelot WebHost is configured with the `authenticationProviderKey = "IdentityApiKey"`, that will require authentication whenever that service has any requests without any auth token.</span></span>

```csharp
namespace OcelotApiGw
{
    public class Startup
    {
        private readonly IConfiguration _cfg;

        public Startup(IConfiguration configuration) => _cfg = configuration;

        public void ConfigureServices(IServiceCollection services)
        {
            var identityUrl = _cfg.GetValue<string>("IdentityUrl");
            var authenticationProviderKey = "IdentityApiKey";
                         //…
            services.AddAuthentication()
                .AddJwtBearer(authenticationProviderKey, x =>
                {
                    x.Authority = identityUrl;
                    x.RequireHttpsMetadata = false;
                    x.TokenValidationParameters = new Microsoft.IdentityModel.Tokens.TokenValidationParameters()
                    {
                        ValidAudiences = new[] { "orders", "basket", "locations", "marketing", "mobileshoppingagg", "webshoppingagg" }
                    };
                });
            //...
        }
    }
}
```

<span data-ttu-id="bfab2-259">Następnie należy ustawić autoryzację z atrybutem [autoryzuje] dla dowolnego zasobu, aby uzyskać do niego dostęp, taki jak mikrousługi, na przykład w następującym kontrolerze mikrousług koszyka.</span><span class="sxs-lookup"><span data-stu-id="bfab2-259">Then, you also need to set authorization with the [Authorize] attribute on any resource to be accessed like the microservices, such as in the following Basket microservice controller.</span></span>

```csharp
namespace Microsoft.eShopOnContainers.Services.Basket.API.Controllers
{
    [Route("api/v1/[controller]")]
    [Authorize]
    public class BasketController : Controller
    {
      //...
    }
}
```

<span data-ttu-id="bfab2-260">ValidAudiences, takie jak "koszyk", są skorelowane z odbiorcami zdefiniowanymi w każdej mikrousłudze za pomocą `AddJwtBearer()` ConfigureServices () klasy startowej, na przykład w poniższym kodzie.</span><span class="sxs-lookup"><span data-stu-id="bfab2-260">The ValidAudiences such as "basket" are correlated with the audience defined in each microservice with `AddJwtBearer()` at the ConfigureServices() of the Startup class, such as in the code below.</span></span>

```csharp
// prevent from mapping "sub" claim to nameidentifier.
JwtSecurityTokenHandler.DefaultInboundClaimTypeMap.Clear();

var identityUrl = Configuration.GetValue<string>("IdentityUrl");

services.AddAuthentication(options =>
{
    options.DefaultAuthenticateScheme = JwtBearerDefaults.AuthenticationScheme;
    options.DefaultChallengeScheme = JwtBearerDefaults.AuthenticationScheme;

}).AddJwtBearer(options =>
{
    options.Authority = identityUrl;
    options.RequireHttpsMetadata = false;
    options.Audience = "basket";
});
```

<span data-ttu-id="bfab2-261">Jeśli spróbujesz uzyskać dostęp do dowolnych bezpiecznych mikrousług, takich jak mikrousługa w koszu z adresem URL przekierowania na podstawie bramy interfejsu API `http://localhost:5202/api/v1/b/basket/1` , na przykład, otrzymasz 401 autoryzacji, chyba że podasz prawidłowy token.</span><span class="sxs-lookup"><span data-stu-id="bfab2-261">If you try to access any secured microservice, like the Basket microservice with a ReRoute URL based on the API Gateway like `http://localhost:5202/api/v1/b/basket/1`, then you'll get a 401 Unauthorized unless you provide a valid token.</span></span> <span data-ttu-id="bfab2-262">Z drugiej strony, jeśli adres URL przekierowania jest uwierzytelniany, Ocelot będzie wywoływał każdy schemat podrzędny jest skojarzony z nim (wewnętrzny adres URL mikrousługi).</span><span class="sxs-lookup"><span data-stu-id="bfab2-262">On the other hand, if a ReRoute URL is authenticated, Ocelot will invoke whatever downstream scheme is associated with it (the internal microservice URL).</span></span>

<span data-ttu-id="bfab2-263">**Autoryzacja w warstwie reroutes w usłudze Ocelot.**</span><span class="sxs-lookup"><span data-stu-id="bfab2-263">**Authorization at Ocelot's ReRoutes tier.**</span></span>  <span data-ttu-id="bfab2-264">Ocelot obsługuje autoryzację opartą na oświadczeniach, która jest obliczana po uwierzytelnieniu.</span><span class="sxs-lookup"><span data-stu-id="bfab2-264">Ocelot supports claims-based authorization evaluated after the authentication.</span></span> <span data-ttu-id="bfab2-265">Autoryzację można ustawić na poziomie trasy, dodając następujące wiersze do konfiguracji Reroute.</span><span class="sxs-lookup"><span data-stu-id="bfab2-265">You set the authorization at a route level by adding the following lines to the ReRoute configuration.</span></span>

```json
"RouteClaimsRequirement": {
    "UserType": "employee"
}
```

<span data-ttu-id="bfab2-266">W tym przykładzie, gdy zostanie wywołane oprogramowanie pośredniczące autoryzacji, Ocelot będzie wiedzieć, czy użytkownik ma typ "UserType" w tokenie i czy wartość tego żądania to "Employee".</span><span class="sxs-lookup"><span data-stu-id="bfab2-266">In that example, when the authorization middleware is called, Ocelot will find if the user has the claim type 'UserType' in the token and if the value of that claim is 'employee'.</span></span> <span data-ttu-id="bfab2-267">Jeśli tak nie jest, użytkownik nie będzie autoryzowany, a odpowiedź 403 będzie niedostępna.</span><span class="sxs-lookup"><span data-stu-id="bfab2-267">If it isn't, then the user will not be authorized and the response will be 403 forbidden.</span></span>

## <a name="using-kubernetes-ingress-plus-ocelot-api-gateways"></a><span data-ttu-id="bfab2-268">Korzystanie z bram interfejsu API Kubernetes i Ocelot</span><span class="sxs-lookup"><span data-stu-id="bfab2-268">Using Kubernetes Ingress plus Ocelot API Gateways</span></span>

<span data-ttu-id="bfab2-269">W przypadku korzystania z Kubernetes (podobnie jak w przypadku klastra usługi Azure Kubernetes) zazwyczaj wszystkie żądania HTTP są tworzone za pośrednictwem [warstwy danych wejściowych Kubernetes](https://kubernetes.io/docs/concepts/services-networking/ingress/) na podstawie *Nginx*.</span><span class="sxs-lookup"><span data-stu-id="bfab2-269">When using Kubernetes (like in an Azure Kubernetes Service cluster), you usually unify all the HTTP requests through the [Kubernetes Ingress tier](https://kubernetes.io/docs/concepts/services-networking/ingress/) based on *Nginx*.</span></span>

<span data-ttu-id="bfab2-270">W Kubernetes, jeśli nie korzystasz z metody transferu danych przychodzących, usługi i mają tylko adresy IP do routingu przez sieć klastra.</span><span class="sxs-lookup"><span data-stu-id="bfab2-270">In Kubernetes, if you don't use any ingress approach, then your services and pods have IPs only routable by the cluster network.</span></span>

<span data-ttu-id="bfab2-271">Jeśli jednak korzystasz z metody transferu danych przychodzących, będziesz mieć warstwę środkową między Internetem a usługami (w tym bramami interfejsu API) działającą jako zwrotny serwer proxy.</span><span class="sxs-lookup"><span data-stu-id="bfab2-271">But if you use an ingress approach, you'll have a middle tier between the Internet and your services (including your API Gateways), acting as a reverse proxy.</span></span>

<span data-ttu-id="bfab2-272">Jako definicja, ruch przychodzący jest kolekcją reguł, które zezwalają na połączenia przychodzące do usług klastra.</span><span class="sxs-lookup"><span data-stu-id="bfab2-272">As a definition, an Ingress is a collection of rules that allow inbound connections to reach the cluster services.</span></span> <span data-ttu-id="bfab2-273">Usługa transferu danych przychodzących jest skonfigurowana w celu świadczenia usług, które są dostępne z zewnątrz, ruchu równoważenia obciążenia, zakończenia protokołu SSL i nie tylko.</span><span class="sxs-lookup"><span data-stu-id="bfab2-273">An ingress is configured to provide services externally reachable URLs, load balance traffic, SSL termination and more.</span></span> <span data-ttu-id="bfab2-274">Użytkownicy żądają transferu danych przychodzących, publikując zasób transferu danych przychodzących na serwerze interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="bfab2-274">Users request ingress by POSTing the Ingress resource to the API server.</span></span>

<span data-ttu-id="bfab2-275">W eShopOnContainers, podczas tworzenia lokalnie i korzystania tylko z komputera deweloperskiego jako hosta platformy Docker, nie są używane żadne przychodzące, ale tylko bramy interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="bfab2-275">In eShopOnContainers, when developing locally and using just your development machine as the Docker host, you are not using any ingress but only the multiple API Gateways.</span></span>

<span data-ttu-id="bfab2-276">Jednak w przypadku określania środowiska "produkcyjnego" w oparciu o Kubernetes, eShopOnContainers korzysta z ruchu przychodzącego przed bramami interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="bfab2-276">However, when targeting a "production" environment based on Kubernetes, eShopOnContainers is using an ingress in front of the API gateways.</span></span> <span data-ttu-id="bfab2-277">Dzięki temu klienci nadal będą wywoływać ten sam podstawowy adres URL, ale żądania są kierowane do wielu bram interfejsu API lub BFF.</span><span class="sxs-lookup"><span data-stu-id="bfab2-277">That way, the clients still call the same base URL but the requests are routed to multiple API Gateways or BFF.</span></span>

<span data-ttu-id="bfab2-278">Bramy interfejsu API to frontony lub fasady, które stanowią jedynie te usługi, ale nie aplikacje sieci Web, które zwykle poza ich zakresem.</span><span class="sxs-lookup"><span data-stu-id="bfab2-278">API Gateways are front-ends or façades surfacing only the services but not the web applications that are usually out of their scope.</span></span> <span data-ttu-id="bfab2-279">Ponadto bramy interfejsu API mogą ukrywać niektóre mikrousługi wewnętrzne.</span><span class="sxs-lookup"><span data-stu-id="bfab2-279">In addition, the API Gateways might hide certain internal microservices.</span></span>

<span data-ttu-id="bfab2-280">Ruch przychodzący polega jednak jedynie na przekierowaniu żądań HTTP, ale nie próbie ukrycia żadnej mikrousługi lub aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="bfab2-280">The ingress, however, is just redirecting HTTP requests but not trying to hide any microservice or web app.</span></span>

<span data-ttu-id="bfab2-281">Posiadanie warstwy Nginx w Kubernetes przed aplikacjami sieci Web, a kilka bram interfejsu API Ocelot/BFF jest idealną architekturą, jak pokazano na poniższym diagramie.</span><span class="sxs-lookup"><span data-stu-id="bfab2-281">Having an ingress Nginx tier in Kubernetes in front of the web applications plus the several Ocelot API Gateways / BFF is the ideal architecture, as shown in the following diagram.</span></span>

![Diagram przedstawiający sposób dopasowania warstwy ruchu przychodzącego do środowiska AKS.](./media/implement-api-gateways-with-ocelot/eshoponcontainer-ingress-tier.png)

<span data-ttu-id="bfab2-283">**Rysunek 6-41**.</span><span class="sxs-lookup"><span data-stu-id="bfab2-283">**Figure 6-41**.</span></span> <span data-ttu-id="bfab2-284">Warstwa transferu danych przychodzących w eShopOnContainers po wdrożeniu w Kubernetes</span><span class="sxs-lookup"><span data-stu-id="bfab2-284">The ingress tier in eShopOnContainers when deployed into Kubernetes</span></span>

<span data-ttu-id="bfab2-285">Ruch przychodzący Kubernetes działa jako zwrotny serwer proxy dla całego ruchu do aplikacji, w tym aplikacji sieci Web, które znajdują się poza zakresem bramy interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="bfab2-285">A Kubernetes Ingress acts as a reverse proxy for all traffic to the app, including the web applications, that are out of the Api gateway scope.</span></span> <span data-ttu-id="bfab2-286">Gdy wdrażasz eShopOnContainers w usłudze _Kubernetes,_ uwidaczniamy tylko kilka usług lub punktów końcowych za pośrednictwem transferu danych przychodzących, zasadniczo Poniższa lista przyrostów adresów URL:</span><span class="sxs-lookup"><span data-stu-id="bfab2-286">When you deploy eShopOnContainers into Kubernetes, it exposes just a few services or endpoints via _ingress_, basically the following list of postfixes on the URLs:</span></span>

- <span data-ttu-id="bfab2-287">`/` dla aplikacji sieci Web SPA klienta</span><span class="sxs-lookup"><span data-stu-id="bfab2-287">`/` for the client SPA web application</span></span>
- <span data-ttu-id="bfab2-288">`/webmvc` dla aplikacji sieci Web Client MVC</span><span class="sxs-lookup"><span data-stu-id="bfab2-288">`/webmvc` for the client MVC web application</span></span>
- <span data-ttu-id="bfab2-289">`/webstatus` dla aplikacji sieci Web klienta pokazującej stan/healthchecks</span><span class="sxs-lookup"><span data-stu-id="bfab2-289">`/webstatus` for the client web app showing the status/healthchecks</span></span>
- <span data-ttu-id="bfab2-290">`/webshoppingapigw` w przypadku procesów biznesowych BFF i zakupów w sieci Web</span><span class="sxs-lookup"><span data-stu-id="bfab2-290">`/webshoppingapigw` for the web BFF and shopping business processes</span></span>
- <span data-ttu-id="bfab2-291">`/webmarketingapigw` dla BFF sieci Web i marketingu procesów roboczych</span><span class="sxs-lookup"><span data-stu-id="bfab2-291">`/webmarketingapigw` for the web BFF and marketing business processes</span></span>
- <span data-ttu-id="bfab2-292">`/mobileshoppingapigw` dla procesów biznesowych Mobile BFF i zakupów</span><span class="sxs-lookup"><span data-stu-id="bfab2-292">`/mobileshoppingapigw` for the mobile BFF and shopping business processes</span></span>
- <span data-ttu-id="bfab2-293">`/mobilemarketingapigw` dla mobilnych BFF i marketingu procesów roboczych</span><span class="sxs-lookup"><span data-stu-id="bfab2-293">`/mobilemarketingapigw` for the mobile BFF and marketing business processes</span></span>

<span data-ttu-id="bfab2-294">Podczas wdrażania programu do Kubernetes każda Brama interfejsu API Ocelot korzysta z innego pliku "configuration.json" dla każdego z nich, na _których działają bramy_ interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="bfab2-294">When deploying to Kubernetes, each Ocelot API Gateway is using a different "configuration.json" file for each _pod_ running the API Gateways.</span></span> <span data-ttu-id="bfab2-295">Te pliki "configuration.json" są udostępniane przez zainstalowanie (oryginalnie ze skryptem deploy.ps1) wolumin utworzony w oparciu o _mapę konfiguracji_ Kubernetes o nazwie "Ocelot".</span><span class="sxs-lookup"><span data-stu-id="bfab2-295">Those "configuration.json" files are provided by mounting (originally with the deploy.ps1 script) a volume created based on a Kubernetes _config map_ named ‘ocelot'.</span></span> <span data-ttu-id="bfab2-296">Każdy kontener instaluje związany z nim plik konfiguracji w folderze kontenera o nazwie `/app/configuration` .</span><span class="sxs-lookup"><span data-stu-id="bfab2-296">Each container mounts its related configuration file in the container's folder named `/app/configuration`.</span></span>

<span data-ttu-id="bfab2-297">W pliku z kodem źródłowym eShopOnContainers oryginalny plik "configuration.json" można znaleźć w `k8s/ocelot/` folderze.</span><span class="sxs-lookup"><span data-stu-id="bfab2-297">In the source code files of eShopOnContainers, the original "configuration.json" files can be found within the `k8s/ocelot/` folder.</span></span> <span data-ttu-id="bfab2-298">Dla każdego BFF/APIGateway istnieje jeden plik.</span><span class="sxs-lookup"><span data-stu-id="bfab2-298">There's one file for each BFF/APIGateway.</span></span>

## <a name="additional-cross-cutting-features-in-an-ocelot-api-gateway"></a><span data-ttu-id="bfab2-299">Dodatkowe funkcje wycinania krzyżowego w bramie interfejsu API Ocelot</span><span class="sxs-lookup"><span data-stu-id="bfab2-299">Additional cross-cutting features in an Ocelot API Gateway</span></span>

<span data-ttu-id="bfab2-300">W przypadku korzystania z bramy interfejsu API Ocelot, która została opisana w poniższych linkach, istnieją inne ważne funkcje do badania i używania.</span><span class="sxs-lookup"><span data-stu-id="bfab2-300">There are other important features to research and use, when using an Ocelot API Gateway, described in the following links.</span></span>

- <span data-ttu-id="bfab2-301">**Odnajdowanie usług po stronie klienta integrując Ocelot z Consul lub Eureka** </span><span class="sxs-lookup"><span data-stu-id="bfab2-301">**Service discovery in the client side integrating Ocelot with Consul or Eureka** </span></span>\
  <https://ocelot.readthedocs.io/en/latest/features/servicediscovery.html>

- <span data-ttu-id="bfab2-302">**Buforowanie w warstwie bramy interfejsu API** </span><span class="sxs-lookup"><span data-stu-id="bfab2-302">**Caching at the API Gateway tier** </span></span>\
  <https://ocelot.readthedocs.io/en/latest/features/caching.html>

- <span data-ttu-id="bfab2-303">**Rejestrowanie w warstwie bramy interfejsu API** </span><span class="sxs-lookup"><span data-stu-id="bfab2-303">**Logging at the API Gateway tier** </span></span>\
  <https://ocelot.readthedocs.io/en/latest/features/logging.html>

- <span data-ttu-id="bfab2-304">**Quality of Service (ponownych prób i wyłączników) w warstwie bramy interfejsu API** </span><span class="sxs-lookup"><span data-stu-id="bfab2-304">**Quality of Service (Retries and Circuit breakers) at the API Gateway tier** </span></span>\
  <https://ocelot.readthedocs.io/en/latest/features/qualityofservice.html>

- <span data-ttu-id="bfab2-305">**Ograniczanie szybkości** </span><span class="sxs-lookup"><span data-stu-id="bfab2-305">**Rate limiting** </span></span>\
  [https://ocelot.readthedocs.io/en/latest/features/ratelimiting.html](https://ocelot.readthedocs.io/en/latest/features/ratelimiting.html )

> [!div class="step-by-step"]
> <span data-ttu-id="bfab2-306">[Poprzedni](background-tasks-with-ihostedservice.md) 
>  [Dalej](../microservice-ddd-cqrs-patterns/index.md)</span><span class="sxs-lookup"><span data-stu-id="bfab2-306">[Previous](background-tasks-with-ihostedservice.md)
[Next](../microservice-ddd-cqrs-patterns/index.md)</span></span>
