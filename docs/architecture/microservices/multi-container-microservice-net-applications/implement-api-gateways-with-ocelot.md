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
# <a name="implement-api-gateways-with-ocelot"></a>Implementowanie bram interfejsu API za pomocą Ocelot

> [!IMPORTANT]
> [EShopOnContainers](https://github.com/dotnet-architecture/eShopOnContainers) aplikacji mikrousługi referencyjnej używa obecnie funkcji dostarczonych przez [wysłannika](https://www.envoyproxy.io/) do implementowania bramy interfejsu API zamiast wcześniejszego odwołania do [Ocelot](https://github.com/ThreeMammals/Ocelot).
> Ten wybór projektu został dokonany z powodu wbudowanej obsługi protokołu WebSocket w programie wysłannika, wymaganej przez nową komunikację między usługami gRPC zaimplementowaną w eShopOnContainers.
> Ta sekcja w przewodniku została jednak zachowana, dlatego można rozważyć Ocelot jako prostą, łatwą i uproszczoną bramę interfejsu API odpowiednią do scenariuszy klasy produkcyjnej.
> Ponadto Najnowsza wersja Ocelot zawiera nieprzerwaną zmianę w schemacie JSON. Rozważ użycie Ocelot < v 16.0.0 lub użycie tras kluczowych zamiast retras.

## <a name="architect-and-design-your-api-gateways"></a>Architekt i projektowanie bram interfejsu API

Poniższy diagram architektury przedstawia sposób implementacji bram interfejsu API z Ocelot w eShopOnContainers.

![Diagram przedstawiający architekturę eShopOnContainers.](./media/implement-api-gateways-with-ocelot/eshoponcontainers-architecture.png)

**Rysunek 6-28**. Architektura eShopOnContainers z bramami interfejsu API

Ten diagram pokazuje, w jaki sposób cała aplikacja jest wdrażana na jednym hoście platformy Docker lub na komputerze deweloperskim z "Docker for Windows" lub "Docker for Mac". Jednak wdrażanie w dowolnym programie Orchestrator będzie podobne, ale każdy kontener na diagramie może być skalowany w programie Orchestrator.

Ponadto zasoby infrastruktury, takie jak bazy danych, pamięci podręcznej i brokerów komunikatów, powinny być oddzielone od programu Orchestrator i wdrożone w systemach o wysokiej dostępności na potrzeby infrastruktury, takich jak Azure SQL Database, Azure Cosmos DB, Azure Redis, Azure Service Bus lub dowolne rozwiązanie klastra HA w środowisku lokalnym.

Podobnie jak można zauważyć, że na diagramie istnieje kilka bram interfejsu API, dzięki czemu wiele zespołów programistycznych może być autonomiczne (w tym przypadku funkcje marketingu a funkcje zakupów) podczas opracowywania i wdrażania mikrousług oraz własnych powiązanych bram interfejsu API.

Jeśli masz pojedynczą, monolityczną bramę interfejsu API, która oznacza, że jeden punkt będzie aktualizowany przez kilka zespołów programistycznych, które mogą dołączać wszystkie mikrousługi do jednej części aplikacji.

Znacznie dokładniej w projekcie, czasem niekiedy Szczegółowa Brama interfejsu API może być również ograniczona do pojedynczej mikrousługi biznesowej, w zależności od wybranej architektury. Posiadanie granic bramy interfejsu API, które są określone przez firmę lub domenę, pomoże Ci uzyskać lepszy projekt.

Na przykład, szczegółowy stopień szczegółowości warstwy bramy API może być szczególnie przydatny w przypadku bardziej zaawansowanych aplikacji interfejsu użytkownika złożonego, które są oparte na mikrousługach, ponieważ pojęcie szczegółowej bramy interfejsu API jest podobne do usługi kompozycji interfejsu użytkownika.

W poprzedniej sekcji omówiono [Tworzenie złożonych interfejsów użytkownika opartych na mikrousługach](../architect-microservice-container-applications/microservice-based-composite-ui-shape-layout.md).

W ramach usługi Key wnioskiem w przypadku wielu aplikacji średniej i o dużej wielkości korzystanie z niestandardowo przygotowanego produktu bramy API jest zwykle dobrym rozwiązaniem, ale nie jako jednym agregatorem monolitycznym lub unikatowym centralną bramą interfejsu API, chyba że brama interfejsu API zezwala na wiele niezależnych obszarów konfiguracji dla kilku zespołów programistycznych tworzących autonomiczne mikrousługi.

### <a name="sample-microservicescontainers-to-reroute-through-the-api-gateways"></a>Przykładowe mikrousługi/kontenery do przekierowania przez bramy interfejsu API

Na przykład eShopOnContainers ma około sześć wewnętrznych typów mikrousług, które muszą być publikowane za pomocą bram interfejsu API, jak pokazano na poniższej ilustracji.

![Zrzut ekranu przedstawiający folder usługi z podfolderami.](./media/implement-api-gateways-with-ocelot/eshoponcontainers-microservice-folders.png)

**Rysunek 6-29**. Foldery mikrousług w rozwiązaniu eShopOnContainers w programie Visual Studio

Informacje o usłudze tożsamości — w projekcie, który jest pozostawiony do routingu bramy interfejsu API, ponieważ jest to jedyne zagadnienie związane z wycinaniem w systemie, chociaż z Ocelot jest również możliwe dołączenie go jako części list reroutingu.

Wszystkie te usługi są obecnie implementowane jako ASP.NET Core usług interfejsu API sieci Web, co umożliwia poinformowanie o kodzie. Skupmy się na jednym z mikrousług, takimi jak kod mikrousług katalogu.

![Zrzut ekranu przedstawiający Eksplorator rozwiązań pokazujący zawartość projektu w katalogu. API.](./media/implement-api-gateways-with-ocelot/catalog-api-microservice-folders.png)

**Rysunek 6-30**. Przykładowa usługa interfejsu API sieci Web (mikrousługa katalogu)

Można sprawdzić, czy katalog jest typowym ASP.NET Core projektem interfejsu API sieci Web z kilkoma kontrolerami i metodami, takimi jak w poniższym kodzie.

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

Żądanie HTTP spowoduje zakończenie działania tego rodzaju kodu w języku C#, który uzyskuje dostęp do bazy danych mikrousług i wszelkich dodatkowych wymaganych akcji.

W odniesieniu do adresu URL mikrousług, gdy kontenery są wdrażane na lokalnym komputerze deweloperskim (lokalny Host platformy Docker), każdy kontener mikrousług ma zawsze port wewnętrzny (zazwyczaj port 80) określony w pliku dockerfile, jak w poniższym pliku dockerfile:

```dockerfile
FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
```

Port 80 wyświetlany w kodzie jest wewnętrzny w ramach hosta platformy Docker, więc nie można go połączyć z aplikacjami klienckimi.

Aplikacje klienckie mogą uzyskiwać dostęp tylko do portów zewnętrznych (jeśli istnieją) opublikowanych podczas wdrażania w programie `docker-compose` .

Tych portów zewnętrznych nie należy publikować podczas wdrażania w środowisku produkcyjnym. Z tego względu, dlaczego chcesz użyć bramy interfejsu API, aby uniknąć bezpośredniej komunikacji między aplikacjami klienckimi i mikrousługami.

Jednak podczas tworzenia programu chcesz bezpośrednio uzyskać dostęp do mikrousługi/kontenera i uruchomić go za pomocą struktury Swagger. Dlatego w eShopOnContainers, porty zewnętrzne są nadal określone nawet wtedy, gdy nie będą używane przez bramę interfejsu API ani aplikacje klienckie.

Oto przykład `docker-compose.override.yml` pliku dla mikrousługi katalogu:

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

Można zobaczyć, jak w konfiguracji Docker-Compose. override. yml port wewnętrzny dla kontenera wykazu jest portem 80, ale Port dostępu zewnętrznego to 5101. Jednak ten port nie powinien być używany przez aplikację podczas korzystania z bramy interfejsu API, tylko do debugowania, uruchamiania i testowania tylko mikrousługi katalogu.

Zwykle nie jest wdrażana przy użyciu platformy Docker — tworzenie w środowisku produkcyjnym, ponieważ odpowiednie środowisko wdrażania w środowisku produkcyjnym dla mikrousług jest koordynatorem, takim jak Kubernetes lub Service Fabric. W przypadku wdrażania w środowiskach korzystających z różnych plików konfiguracji, w których nie można publikować bezpośrednio żadnych portów zewnętrznych dla mikrousług, ale zawsze będziesz używać zwrotnego serwera proxy z bramy interfejsu API.

Uruchom mikrousługę katalogu na lokalnym hoście platformy Docker. Uruchom pełne rozwiązanie eShopOnContainers z programu Visual Studio (uruchamia wszystkie usługi w plikach do redagowania w systemie Docker) lub Uruchom mikrousługę za pomocą następującego polecenia Docker-Zredaguj w programie CMD lub programie PowerShell umieszczonym w folderze, w którym `docker-compose.yml` `docker-compose.override.yml` są umieszczone i.

```console
docker-compose run --service-ports catalog-api
```

To polecenie uruchamia tylko kontener usługi Catalog-API i zależności, które są określone w Docker-Compose. yml. W tym przypadku kontener SQL Server i kontener RabbitMQ.

Następnie można bezpośrednio uzyskać dostęp do mikrousługi katalogu i wyświetlić jej metody za pomocą interfejsu użytkownika programu Swagger, uzyskując dostęp bezpośrednio przez ten port "zewnętrzny", w tym przypadku `http://localhost:5101/swagger` :

![Zrzut ekranu przedstawiający interfejs użytkownika struktury Swagger z interfejsem API REST katalogu. API.](./media/implement-api-gateways-with-ocelot/test-catalog-microservice.png)

**Rysunek 6-31**. Testowanie mikrousługi katalogu za pomocą interfejsu użytkownika struktury Swagger

W tym momencie można ustawić punkt przerwania w kodzie C# w programie Visual Studio, przetestować mikrousługę przy użyciu metod udostępnianych w interfejsie użytkownika programu Swagger, a wreszcie oczyścić wszystko za pomocą `docker-compose down` polecenia.

Jednak bezpośredni dostęp do mikrousługi, w tym przypadku przez port zewnętrzny 5101, jest dokładnie to, co chcesz uniknąć w aplikacji. Można uniknąć tego przez ustawienie dodatkowego poziomu pośredniego dla bramy interfejsu API (w tym przypadku Ocelot). Dzięki temu aplikacja kliencka nie będzie bezpośrednio uzyskiwać dostępu do mikrousługi.

## <a name="implementing-your-api-gateways-with-ocelot"></a>Implementowanie bram interfejsu API za pomocą usługi Ocelot

Ocelot jest zasadniczo zestawem middlewares, który można zastosować w określonej kolejności.

Ocelot jest przeznaczona do pracy tylko z ASP.NET Core. Najnowsza wersja obiektów docelowych pakietu `.NETCoreApp 3.1` , dlatego nie jest odpowiednia dla .NET Framework aplikacji.

Program Visual Studio umożliwia zainstalowanie Ocelot i jego zależności w projekcie ASP.NET Core z [pakietem NuGet Ocelot](https://www.nuget.org/packages/Ocelot/).

```powershell
Install-Package Ocelot
```

W eShopOnContainers, jej implementacja bramy interfejsu API to ASP.NET Core prosty projekt usługi WebHost, a Ocelot oprogramowanie pośredniczące obsługuje wszystkie funkcje bramy interfejsu API, jak pokazano na poniższej ilustracji:

![Zrzut ekranu przedstawiający Eksplorator rozwiązań pokazujący projekt bramy interfejsu API Ocelot.](./media/implement-api-gateways-with-ocelot/ocelotapigw-base-project.png)

**Rysunek 6-32**. Projekt podstawowy OcelotApiGw w eShopOnContainers

Ten ASP.NET Core Project WebHost został skompilowany przy użyciu dwóch prostych plików:  `Program.cs` i `Startup.cs` .

Program.cs musi utworzyć i skonfigurować typowe ASP.NET Core BuildWebHost.

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

Ważnym punktem dla Ocelot jest `configuration.json` plik, który należy dostarczyć do konstruktora za pomocą `AddJsonFile()` metody. W tym `configuration.json` miejscu należy określić wszystkie przekierowania bramy interfejsu API, co oznacza, że zewnętrzne punkty końcowe z określonymi portami i skorelowane wewnętrzne punkty końcowe zwykle korzystają z różnych portów.

```json
{
    "ReRoutes": [],
    "GlobalConfiguration": {}
}
```

Do konfiguracji należą dwie sekcje. Tablica retras i GlobalConfiguration. Przekierowania są obiektami, które informują Ocelot o sposobie traktowania żądania nadrzędnego. Konfiguracja globalna umożliwia przesłonięcia przekierowania określonych ustawień. Jest to przydatne, jeśli nie chcesz zarządzać wieloma zmianami poszczególnych ustawień.

Poniżej przedstawiono uproszczony przykład [retrasy pliku konfiguracji](https://github.com/dotnet-architecture/eShopOnContainers/blob/master/src/ApiGateways/Web.Bff.Shopping/apigw/configuration.json) z jednej z bram interfejsu API z eShopOnContainers.

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

Główną funkcją bramy interfejsu API Ocelot jest przejęcie przychodzących żądań HTTP i przekazanie ich do usługi podrzędnej, obecnie jako innego żądania HTTP. Ocelot opisuje Routing jednego żądania do innego jako Reroute.

Na przykład skupmy się na jednym z tras w configuration.jsna podstawie powyższych, konfiguracji mikrousługi koszyka.

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

DownstreamPathTemplate, schemat i DownstreamHostAndPorts tworzą wewnętrzny adres URL mikrousług, do którego zostanie przesłane żądanie.

Port jest portem wewnętrznym używanym przez usługę. W przypadku korzystania z kontenerów port określony w pliku dockerfile.

`Host`Jest nazwą usługi, która zależy od używanego rozwiązania nazwy usługi. W przypadku korzystania z platformy Docker — Tworzenie nazw usług są udostępniane przez hosta platformy Docker, który korzysta z nazw usług udostępnianych w plikach tworzenia platformy Docker. W przypadku korzystania z programu Orchestrator, takiego jak Kubernetes lub Service Fabric, ta nazwa powinna być rozpoznawana przez system DNS lub rozpoznawanie nazw dostarczone przez każdego koordynatora.

DownstreamHostAndPorts to tablica zawierająca hosta i port wszystkich usług podrzędnych, do których mają być przekazywane żądania. Zwykle ta konfiguracja będzie zawierać jeden wpis, ale czasami może zajść potrzeba zrównoważenia obciążenia żądaniami do usług podrzędnych i Ocelot umożliwia dodanie więcej niż jednego wpisu, a następnie wybranie modułu równoważenia obciążenia. Ale jeśli korzystasz z platformy Azure i dowolnego programu Orchestrator, prawdopodobnie lepszym rozwiązaniem jest zrównoważenie równoważenia obciążenia za pomocą infrastruktury chmury i programu Orchestrator.

UpstreamPathTemplate to adres URL, który będzie używany przez Ocelot do identyfikowania DownstreamPathTemplate do użycia dla danego żądania od klienta. Na koniec UpstreamHttpMethod jest używany, więc Ocelot może rozróżnić różne żądania (GET, POST, PUT) na ten sam adres URL.

W tym momencie można korzystać z pojedynczej bramy interfejsu API Ocelot (ASP.NET Core WebHost) przy użyciu jednego lub [wielu scalonych configuration.jsna plikach](https://ocelot.readthedocs.io/en/latest/features/configuration.html#merging-configuration-files) lub można również przechowywać [konfigurację w magazynie Consul KV](https://ocelot.readthedocs.io/en/latest/features/configuration.html#store-configuration-in-consul).

Jeśli jednak na pewno chcesz mieć autonomiczne mikrousługi, jak zostało to opisane w sekcji architektura i projekt, lepiej jest podzielić tę jednolite bramy interfejsu API na wiele bram interfejsu API i/lub BFF (zaplecza dla frontonu). W tym celu Zobaczmy, jak zaimplementować to podejście przy użyciu kontenerów platformy Docker.

### <a name="using-a-single-docker-container-image-to-run-multiple-different-api-gateway--bff-container-types"></a>Używanie pojedynczego obrazu kontenera Docker do uruchamiania wielu różnych typów kontenerów bramy interfejsu API/BFF

W eShopOnContainers korzystamy z jednego obrazu kontenera Docker z bramą interfejsu API Ocelot, a następnie w czasie wykonywania utworzymy różne usługi/kontenery dla każdego typu interfejsu API-Gateway/BFF, dostarczając inny configuration.jsw pliku przy użyciu woluminu platformy Docker w celu uzyskania dostępu do innego folderu komputera dla każdej usługi.

![Diagram jednego obrazu platformy Docker bramy Ocelot dla wszystkich bram interfejsu API.](./media/implement-api-gateways-with-ocelot/reusing-single-ocelot-docker-image.png)

**Rysunek 6-33**. Wielokrotne używanie pojedynczego obrazu platformy Docker Ocelot w wielu typach bram interfejsu API

W eShopOnContainers "ogólny obraz bramy interfejsu API Docker" jest tworzony przy użyciu projektu o nazwie "OcelotApiGw" i nazwy obrazu "eshop/OcelotApiGw", która jest określona w pliku Docker-Compose. yml. Po wdrożeniu do platformy Docker będzie dostępnych cztery API-Gateway kontenerów utworzonych na podstawie tego samego obrazu platformy Docker, jak pokazano w poniższym wyodrębnieniu z pliku Docker-Compose. yml.

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

Ponadto, jak widać w poniższym pliku Docker-Compose. override. yml, jedyną różnicą między tymi kontenerami bramy interfejsu API jest plik konfiguracji Ocelot, który jest inny dla każdego kontenera usługi i został określony w czasie wykonywania za pomocą woluminu platformy Docker.

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

Ze względu na ten poprzedni kod, jak pokazano w Eksploratorze programu Visual Studio, jedynym plikiem potrzebnym do zdefiniowania każdej konkretnej bramy interfejsu API Business/BFF jest tylko configuration.jsw pliku, ponieważ cztery bramy interfejsu API są oparte na tym samym obrazie platformy Docker.

![Zrzut ekranu przedstawiający wszystkie bramy interfejsu API z configuration.jsna plikach.](./media/implement-api-gateways-with-ocelot/ocelot-configuration-files.png)

**Rysunek 6-34**. Jedynym plikiem wymaganym do zdefiniowania każdej usługi API Gateway/BFF z Ocelot jest plik konfiguracji

Dzieląc bramę interfejsu API na wiele bram interfejsu API, różne zespoły programistyczne skupiające się na różnych podzestawach mikrousług mogą zarządzać własnymi bramami interfejsu API za pomocą niezależnych plików konfiguracji Ocelot. Dodatkowo, w tym samym czasie mogą ponownie użyć tego samego obrazu platformy Docker Ocelot.

Teraz, jeśli uruchomisz eShopOnContainers z bramami interfejsu API (zawartymi domyślnie w programie VS podczas otwierania rozwiązania eShopOnContainers-ServicesAndWebApps. sln lub w przypadku uruchamiania funkcji "Docker-Zredaguj up"), zostaną wykonane następujące przykładowe trasy.

Na przykład podczas odwiedzania nadrzędnego adresu URL `http://localhost:5202/api/v1/c/catalog/items/2/` obsługiwanego przez bramę interfejsu API webshoppingapigw uzyskasz ten sam wynik z wewnętrznego podrzędnego adresu URL `http://catalog-api/api/v1/2` w ramach hosta platformy Docker, jak w poniższej przeglądarce.

![Zrzut ekranu przeglądarki wyświetlającej odpowiedź przechodzącą przez bramę interfejsu API.](./media/implement-api-gateways-with-ocelot/access-microservice-through-url.png)

**Rysunek 6-35**. Uzyskiwanie dostępu do mikrousługi za pomocą adresu URL dostarczonego przez bramę interfejsu API

Ze względu na testowanie lub debugowanie, jeśli chcesz uzyskać bezpośredni dostęp do kontenera Docker katalogu (tylko w środowisku programistycznym) bez przechodzenia przez bramę interfejsu API, ponieważ "Catalog-API" to rozpoznawanie nazw DNS wewnętrznie dla hosta platformy Docker (Odnajdywanie usług obsługiwane przez nazwy usług platformy Docker), jedynym sposobem uzyskania bezpośredniego dostępu do kontenera jest port zewnętrzny opublikowany w Docker-Compose. override. yml, który jest dostępny tylko dla testów programistycznych, takich jak `http://localhost:5101/api/v1/Catalog/items/1` w poniższej przeglądarce.

![Zrzut ekranu przeglądarki wyświetlającej bezpośrednią odpowiedź do katalogu. API.](./media/implement-api-gateways-with-ocelot/direct-access-microservice-testing.png)

**Rysunek 6-36**. Bezpośredni dostęp do mikrousługi na potrzeby testowania

Jednak aplikacja jest skonfigurowana, aby uzyskiwać dostęp do wszystkich mikrousług za pośrednictwem bram interfejsu API, a nie za pośrednictwem portu bezpośredniego.

### <a name="the-gateway-aggregation-pattern-in-eshoponcontainers"></a>Wzorzec agregacji bramy w eShopOnContainers

Jak wprowadzono wcześniej, elastyczny sposób implementacji agregacji żądań jest z usługami niestandardowymi, przez kod. Można również zaimplementować agregację żądań za pomocą [funkcji agregacji żądań w Ocelot](https://ocelot.readthedocs.io/en/latest/features/requestaggregation.html#request-aggregation), ale może to być niepotrzebne. W związku z tym wybrany sposób implementacji agregacji w eShopOnContainers jest z jawnym ASP.NET Core usługą interfejsu API sieci Web dla każdego agregatora.

Zgodnie z tym podejściem diagram kompozycji bramy interfejsu API jest w rzeczywistości bardziej rozszerzony podczas rozważania usług agregatora, które nie są wyświetlane w uproszczonym, globalnym diagramie architektury.

Na poniższym diagramie można także zobaczyć, jak usługi agregatora współpracują z odpowiednimi bramami interfejsu API.

![Diagram architektury eShopOnContainers, w którym są wyświetlane usługi agregatora.](./media/implement-api-gateways-with-ocelot/eshoponcontainers-architecture-aggregator-services.png)

**Rysunek 6-37**. Architektura eShopOnContainers z usługami agregatora

Dalsze powiększanie, w obszarze roboczym "zakupy" na poniższej ilustracji widać, że chattiness między aplikacjami klienckimi i mikrousługami zostanie zredukowany w przypadku korzystania z usług agregatora w bramach interfejsu API.

![Diagram przedstawiający powiększenie architektury eShopOnContainers.](./media/implement-api-gateways-with-ocelot/zoom-in-vision-aggregator-services.png)

**Rysunek 6-38**. Powiększ zalety usług agregatora

Można zauważyć, jak gdy diagram pokazuje możliwe żądania pochodzące z bram interfejsu API, które mogą być złożone. Z drugiej strony, gdy używasz wzorca agregatora, zobaczysz, jak strzałki w kolorze niebieskim upraszczają komunikację z perspektywy aplikacji klienckiej. Ten wzorzec nie tylko pomaga ograniczyć chattiness i opóźnień w komunikacji, ale również znacznie poprawia środowisko użytkownika dla aplikacji zdalnych (aplikacji mobilnych i SPA).

W przypadku obszaru biznesowego "Marketing" i mikrousług jest to prosty przypadek użycia, dlatego nie ma potrzeby korzystania z agregatorów, ale może również być możliwe, jeśli jest to konieczne.

### <a name="authentication-and-authorization-in-ocelot-api-gateways"></a>Uwierzytelnianie i autoryzacja w bramach interfejsu API Ocelot

W bramie interfejsu API Ocelot można korzystać z usługi uwierzytelniania, takiej jak usługa interfejsu API sieci Web ASP.NET Core przy użyciu [IdentityServer](https://identityserver.io/) , dostarczając token uwierzytelniania lub wewnątrz bramy interfejsu API.

Ponieważ eShopOnContainers korzysta z wielu bram interfejsu API z granicami opartymi na obszarach BFF i firmowych, Usługa tożsamość/uwierzytelnianie pozostaje poza bramami interfejsu API, jak zostało to wyróżnione na żółto na poniższym diagramie.

![Diagram przedstawiający mikrousługę tożsamości poniżej bramy interfejsu API.](./media/implement-api-gateways-with-ocelot/eshoponcontainers-identity-service-position.png)

**Rysunek 6-39**. Pozycja usługi tożsamości w eShopOnContainers

Jednak Ocelot obsługuje także rolę mikrousługi tożsamości/uwierzytelniania w ramach granicy bramy interfejsu API, tak jak w przypadku tego innego diagramu.

![Diagram przedstawiający uwierzytelnianie w bramie interfejsu API Ocelot.](./media/implement-api-gateways-with-ocelot/ocelot-authentication.png)

**Rysunek 6-40**. Uwierzytelnianie w Ocelot

Jak pokazano na poprzednim diagramie, gdy mikrousługa tożsamości znajduje się poniżej bramy API Gateway (AG): 1), usługa AG żąda tokenu uwierzytelniania od mikrousługi tożsamości, 2) usługa Identity-Service zwraca token do AG, 3-4), żądania od mikrousług przy użyciu tokenu uwierzytelniania. Ponieważ aplikacja eShopOnContainers podzieliła bramę interfejsu API na wiele BFF (zaplecza dla frontonu) i firmowych bram interfejsu API, kolejną opcją jest utworzenie dodatkowej bramy interfejsu API dla zagadnień związanych z wycinaniem. Wybór ten byłby atrakcyjny w bardziej złożonej architekturze opartej na mikrousługach z wieloma usługami. Ponieważ w eShopOnContainers występuje tylko jeden problem z wycinaniem, to zdecydowano o prostu obsłużyć usługę zabezpieczeń z obszaru bramy interfejsu API w celu uproszczenia.

W każdym przypadku, jeśli aplikacja jest zabezpieczona na poziomie bramy interfejsu API, moduł uwierzytelniania bramy interfejsu API Ocelot jest najpierw odwiedzany przy próbie użycia dowolnej zabezpieczonej mikrousługi. Przekierowuje żądanie HTTP do odwiedzania tożsamości lub mikrousługi uwierzytelniania w celu uzyskania tokenu dostępu, aby można było odwiedzić chronione usługi przy użyciu access_token.

Sposób zabezpieczania przy użyciu uwierzytelniania każdej usługi na poziomie bramy interfejsu API polega na ustawieniu AuthenticationProviderKey w ustawieniach pokrewnych w configuration.js.

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

Po uruchomieniu Ocelot zostanie wyświetlona wartość reroutes AuthenticationOptions. AuthenticationProviderKey i sprawdź, czy istnieje dostawca uwierzytelniania zarejestrowany dla danego klucza. Jeśli nie, to Ocelot nie zostanie uruchomiony. Jeśli istnieje, wówczas retrasa użyje tego dostawcy, gdy zostanie on wykonany.

Ponieważ Ocelot WebHost jest skonfigurowany przy użyciu programu `authenticationProviderKey = "IdentityApiKey"` , który będzie wymagał uwierzytelniania zawsze, gdy ta usługa ma jakiekolwiek żądania bez tokenu uwierzytelniania.

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

Następnie należy ustawić autoryzację z atrybutem [autoryzuje] dla dowolnego zasobu, aby uzyskać do niego dostęp, taki jak mikrousługi, na przykład w następującym kontrolerze mikrousług koszyka.

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

ValidAudiences, takie jak "koszyk", są skorelowane z odbiorcami zdefiniowanymi w każdej mikrousłudze za pomocą `AddJwtBearer()` ConfigureServices () klasy startowej, na przykład w poniższym kodzie.

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

Jeśli spróbujesz uzyskać dostęp do dowolnych bezpiecznych mikrousług, takich jak mikrousługa w koszu z adresem URL przekierowania na podstawie bramy interfejsu API `http://localhost:5202/api/v1/b/basket/1` , na przykład, otrzymasz 401 autoryzacji, chyba że podasz prawidłowy token. Z drugiej strony, jeśli adres URL przekierowania jest uwierzytelniany, Ocelot będzie wywoływał każdy schemat podrzędny jest skojarzony z nim (wewnętrzny adres URL mikrousługi).

**Autoryzacja w warstwie reroutes w usłudze Ocelot.**  Ocelot obsługuje autoryzację opartą na oświadczeniach, która jest obliczana po uwierzytelnieniu. Autoryzację można ustawić na poziomie trasy, dodając następujące wiersze do konfiguracji Reroute.

```json
"RouteClaimsRequirement": {
    "UserType": "employee"
}
```

W tym przykładzie, gdy zostanie wywołane oprogramowanie pośredniczące autoryzacji, Ocelot będzie wiedzieć, czy użytkownik ma typ "UserType" w tokenie i czy wartość tego żądania to "Employee". Jeśli tak nie jest, użytkownik nie będzie autoryzowany, a odpowiedź 403 będzie niedostępna.

## <a name="using-kubernetes-ingress-plus-ocelot-api-gateways"></a>Korzystanie z bram interfejsu API Kubernetes i Ocelot

W przypadku korzystania z Kubernetes (podobnie jak w przypadku klastra usługi Azure Kubernetes) zazwyczaj wszystkie żądania HTTP są tworzone za pośrednictwem [warstwy danych wejściowych Kubernetes](https://kubernetes.io/docs/concepts/services-networking/ingress/) na podstawie *Nginx*.

W Kubernetes, jeśli nie korzystasz z metody transferu danych przychodzących, usługi i mają tylko adresy IP do routingu przez sieć klastra.

Jeśli jednak korzystasz z metody transferu danych przychodzących, będziesz mieć warstwę środkową między Internetem a usługami (w tym bramami interfejsu API) działającą jako zwrotny serwer proxy.

Jako definicja, ruch przychodzący jest kolekcją reguł, które zezwalają na połączenia przychodzące do usług klastra. Usługa transferu danych przychodzących jest skonfigurowana w celu świadczenia usług, które są dostępne z zewnątrz, ruchu równoważenia obciążenia, zakończenia protokołu SSL i nie tylko. Użytkownicy żądają transferu danych przychodzących, publikując zasób transferu danych przychodzących na serwerze interfejsu API.

W eShopOnContainers, podczas tworzenia lokalnie i korzystania tylko z komputera deweloperskiego jako hosta platformy Docker, nie są używane żadne przychodzące, ale tylko bramy interfejsu API.

Jednak w przypadku określania środowiska "produkcyjnego" w oparciu o Kubernetes, eShopOnContainers korzysta z ruchu przychodzącego przed bramami interfejsu API. Dzięki temu klienci nadal będą wywoływać ten sam podstawowy adres URL, ale żądania są kierowane do wielu bram interfejsu API lub BFF.

Bramy interfejsu API to frontony lub fasady, które stanowią jedynie te usługi, ale nie aplikacje sieci Web, które zwykle poza ich zakresem. Ponadto bramy interfejsu API mogą ukrywać niektóre mikrousługi wewnętrzne.

Ruch przychodzący polega jednak jedynie na przekierowaniu żądań HTTP, ale nie próbie ukrycia żadnej mikrousługi lub aplikacji sieci Web.

Posiadanie warstwy Nginx w Kubernetes przed aplikacjami sieci Web, a kilka bram interfejsu API Ocelot/BFF jest idealną architekturą, jak pokazano na poniższym diagramie.

![Diagram przedstawiający sposób dopasowania warstwy ruchu przychodzącego do środowiska AKS.](./media/implement-api-gateways-with-ocelot/eshoponcontainer-ingress-tier.png)

**Rysunek 6-41**. Warstwa transferu danych przychodzących w eShopOnContainers po wdrożeniu w Kubernetes

Ruch przychodzący Kubernetes działa jako zwrotny serwer proxy dla całego ruchu do aplikacji, w tym aplikacji sieci Web, które znajdują się poza zakresem bramy interfejsu API. Gdy wdrażasz eShopOnContainers w usłudze _Kubernetes,_ uwidaczniamy tylko kilka usług lub punktów końcowych za pośrednictwem transferu danych przychodzących, zasadniczo Poniższa lista przyrostów adresów URL:

- `/` dla aplikacji sieci Web SPA klienta
- `/webmvc` dla aplikacji sieci Web Client MVC
- `/webstatus` dla aplikacji sieci Web klienta pokazującej stan/healthchecks
- `/webshoppingapigw` w przypadku procesów biznesowych BFF i zakupów w sieci Web
- `/webmarketingapigw` dla BFF sieci Web i marketingu procesów roboczych
- `/mobileshoppingapigw` dla procesów biznesowych Mobile BFF i zakupów
- `/mobilemarketingapigw` dla mobilnych BFF i marketingu procesów roboczych

Podczas wdrażania programu do Kubernetes każda Brama interfejsu API Ocelot korzysta z innego pliku "configuration.json" dla każdego z nich, na _których działają bramy_ interfejsu API. Te pliki "configuration.json" są udostępniane przez zainstalowanie (oryginalnie ze skryptem deploy.ps1) wolumin utworzony w oparciu o _mapę konfiguracji_ Kubernetes o nazwie "Ocelot". Każdy kontener instaluje związany z nim plik konfiguracji w folderze kontenera o nazwie `/app/configuration` .

W pliku z kodem źródłowym eShopOnContainers oryginalny plik "configuration.json" można znaleźć w `k8s/ocelot/` folderze. Dla każdego BFF/APIGateway istnieje jeden plik.

## <a name="additional-cross-cutting-features-in-an-ocelot-api-gateway"></a>Dodatkowe funkcje wycinania krzyżowego w bramie interfejsu API Ocelot

W przypadku korzystania z bramy interfejsu API Ocelot, która została opisana w poniższych linkach, istnieją inne ważne funkcje do badania i używania.

- **Odnajdowanie usług po stronie klienta integrując Ocelot z Consul lub Eureka** \
  <https://ocelot.readthedocs.io/en/latest/features/servicediscovery.html>

- **Buforowanie w warstwie bramy interfejsu API** \
  <https://ocelot.readthedocs.io/en/latest/features/caching.html>

- **Rejestrowanie w warstwie bramy interfejsu API** \
  <https://ocelot.readthedocs.io/en/latest/features/logging.html>

- **Quality of Service (ponownych prób i wyłączników) w warstwie bramy interfejsu API** \
  <https://ocelot.readthedocs.io/en/latest/features/qualityofservice.html>

- **Ograniczanie szybkości** \
  [https://ocelot.readthedocs.io/en/latest/features/ratelimiting.html](https://ocelot.readthedocs.io/en/latest/features/ratelimiting.html )

> [!div class="step-by-step"]
> [Poprzedni](background-tasks-with-ihostedservice.md) 
>  [Dalej](../microservice-ddd-cqrs-patterns/index.md)
