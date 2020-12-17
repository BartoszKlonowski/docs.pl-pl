---
title: Testowanie aplikacji internetowych i usług ASP.NET Core
description: Architektura mikrousług platformy .NET dla aplikacji platformy .NET w kontenerze | Poznaj architekturę testowania ASP.NET Core usług i aplikacji sieci Web w kontenerach.
ms.date: 08/07/2020
ms.openlocfilehash: 67872668781d8ae5d79bf360aee73f744cf4404b
ms.sourcegitcommit: 635a0ff775d2447a81ef7233a599b8f88b162e5d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/17/2020
ms.locfileid: "97633952"
---
# <a name="testing-aspnet-core-services-and-web-apps"></a>Testowanie aplikacji internetowych i usług ASP.NET Core

Kontrolery są centralną częścią dowolnych ASP.NET Core usługi interfejsu API i aplikacji sieci Web ASP.NET MVC. W związku z tym należy mieć pewność, że zachowanie jest zamierzone dla aplikacji. Testy automatyczne mogą zapewnić Ci pewność i wykryć błędy przed osiągnięciem ich w środowisku produkcyjnym.

Należy przetestować, jak działa kontroler na podstawie prawidłowych lub nieprawidłowych danych wejściowych, a także odpowiedzi kontrolera testów na podstawie wyniku wykonywanej przez nią operacji biznesowej. Należy jednak mieć następujące typy testów dla mikrousług:

- Testy jednostkowe. Zapewniają one, że poszczególne składniki aplikacji działają zgodnie z oczekiwaniami. Potwierdzenia przetestowania interfejsu API składnika.

- Testy integracji. Zapewniają one, że interakcje składnika działają zgodnie z oczekiwaniami względem zewnętrznych artefaktów, takich jak bazy danych. Potwierdzenia mogą testować składnik API, interfejs użytkownika lub skutki uboczne akcji, takich jak baza danych we/wy, rejestrowanie itp.

- Testy funkcjonalne dla każdej mikrousługi. Upewnij się, że aplikacja działa zgodnie z oczekiwaniami z perspektywy użytkownika.

- Testy usług. Zapewnia to kompleksowe przypadki użycia usługi, w tym testowanie wielu usług w tym samym czasie, są testowane. W przypadku tego typu testów należy najpierw przygotować środowisko. W takim przypadku oznacza to uruchomienie usług (na przykład przy użyciu platformy Docker — tworzenie).

### <a name="implementing-unit-tests-for-aspnet-core-web-apis"></a>Implementowanie testów jednostkowych dla ASP.NET Core interfejsów API sieci Web

Testowanie jednostkowe obejmuje testowanie części aplikacji w izolacji z jej infrastruktury i zależności. W przypadku logiki kontrolera testów jednostkowych jest testowana tylko zawartość pojedynczej akcji lub metody, a nie zachowanie jej zależności lub samego środowiska. Testy jednostkowe nie wykrywają problemów interakcji między składnikami, które są celem testowania integracji.

Podczas testowania jednostek akcji kontrolera Pamiętaj, aby skoncentrować się tylko na ich zachowaniu. Test jednostkowy kontrolera pozwala uniknąć elementów, takich jak filtry, Routing lub powiązanie modelu (mapowanie danych żądania do ViewModel lub DTO). Ponieważ koncentrują się na testowaniu tylko jednej rzeczy, testy jednostkowe są zwykle proste do pisania i szybkiego uruchomienia. Dobrze zapisany zestaw testów jednostkowych może być uruchamiany często bez znacznie większego obciążenia.

Testy jednostkowe są implementowane na podstawie platform testowych, takich jak xUnit.net, MSTest, MOQ lub NUnit. W przypadku przykładowej aplikacji eShopOnContainers korzystamy z xUnit.

Podczas pisania testu jednostkowego dla kontrolera interfejsu API sieci Web, można utworzyć wystąpienie klasy kontrolera bezpośrednio przy użyciu słowa kluczowego New w języku C \# , aby test działał tak szybko, jak to możliwe. Poniższy przykład pokazuje, jak to zrobić przy użyciu [xUnit](https://xunit.net/) jako środowiska testowego.

```csharp
[Fact]
public async Task Get_order_detail_success()
{
    //Arrange
    var fakeOrderId = "12";
    var fakeOrder = GetFakeOrder();

    //...

    //Act
    var orderController = new OrderController(
        _orderServiceMock.Object,
        _basketServiceMock.Object,
        _identityParserMock.Object);

    orderController.ControllerContext.HttpContext = _contextMock.Object;
    var actionResult = await orderController.Detail(fakeOrderId);

    //Assert
    var viewResult = Assert.IsType<ViewResult>(actionResult);
    Assert.IsAssignableFrom<Order>(viewResult.ViewData.Model);
}
```

### <a name="implementing-integration-and-functional-tests-for-each-microservice"></a>Implementowanie integracji i testów funkcjonalnych dla każdej mikrousługi

Jak wspomniano, testy integracji i testy funkcjonalne mają różne cele i cele. Jednak sposób implementacji obydwu podczas testowania kontrolerów ASP.NET Core jest podobny, dlatego w tej sekcji koncentrujemy się na testach integracji.

Testowanie integracji gwarantuje, że składniki aplikacji będą działać prawidłowo po złożeniu. ASP.NET Core obsługuje testowanie integracji przy użyciu platform testów jednostkowych oraz wbudowanego hosta sieci Web, który może służyć do obsługi żądań bez obciążenia sieci.

W przeciwieństwie do testów jednostkowych, testy integracji często obejmują problemy związane z infrastrukturą aplikacji, takie jak baza danych, system plików, zasoby sieciowe lub żądania sieci Web i odpowiedzi. Testy jednostkowe wykorzystują elementy sztuczne lub makiety zamiast tych obaw. Jednak celem testów integracji jest upewnienie się, że system działa zgodnie z oczekiwaniami w tych systemach, dlatego w przypadku testowania integracji nie są używane obiekty sztuczne lub makiety. Zamiast tego należy dołączyć infrastrukturę, taką jak dostęp do bazy danych lub Wywoływanie usługi z innych usług.

Ponieważ testy integracji wykonują większe segmenty kodu niż testy jednostkowe, a ponieważ testy integracji korzystają z elementów infrastruktury, są one w porządku o wielkości wolniej niż testy jednostkowe. Z tego względu dobrym pomysłem jest ograniczenie liczby wykonywanych i uruchamianych testów integracji.

ASP.NET Core obejmuje wbudowanego hosta sieci Web, który może służyć do obsługi żądań HTTP bez obciążenia sieci, co oznacza, że można uruchamiać te testy szybciej niż w przypadku korzystania z rzeczywistego hosta sieci Web. Test hosta sieci Web (TestServer) jest dostępny w składniku NuGet jako Microsoft. AspNetCore. TestHost. Można go dodać do projektów testów integracji i używać do hostowania aplikacji ASP.NET Core.

Jak widać w poniższym kodzie, podczas tworzenia testów integracji dla kontrolerów ASP.NET Core należy utworzyć wystąpienia kontrolerów za pomocą hosta testowego. Jest to porównywalne do żądania HTTP, ale działa szybciej.

```csharp
public class PrimeWebDefaultRequestShould
{
    private readonly TestServer _server;
    private readonly HttpClient _client;

    public PrimeWebDefaultRequestShould()
    {
        // Arrange
        _server = new TestServer(new WebHostBuilder()
           .UseStartup<Startup>());
           _client = _server.CreateClient();
    }

    [Fact]
    public async Task ReturnHelloWorld()
    {
        // Act
        var response = await _client.GetAsync("/");
        response.EnsureSuccessStatusCode();
        var responseString = await response.Content.ReadAsStringAsync();
        // Assert
        Assert.Equal("Hello World!", responseString);
    }
}
```

#### <a name="additional-resources"></a>Zasoby dodatkowe

- **Steve Smith. Kontrolery testowania** (ASP.NET Core) \
    [https://docs.microsoft.com/aspnet/core/mvc/controllers/testing](/aspnet/core/mvc/controllers/testing)

- **Steve Smith. Testowanie integracji** (ASP.NET Core) \
    [https://docs.microsoft.com/aspnet/core/test/integration-tests](/aspnet/core/test/integration-tests)

- **Testowanie jednostkowe w programie .NET Core przy użyciu testu dotnet** \
    [https://docs.microsoft.com/dotnet/core/testing/unit-testing-with-dotnet-test](../../../core/testing/unit-testing-with-dotnet-test.md)

- **xUnit.NET**. Oficjalna lokacja. \
    <https://xunit.net/>

- **Podstawowe informacje o teście jednostkowym.** \
    [https://docs.microsoft.com/visualstudio/test/unit-test-basics](/visualstudio/test/unit-test-basics)

- **MOQ**. Repozytorium GitHub. \
    <https://github.com/moq/moq>

- **Nunit**. Oficjalna lokacja. \
    <https://nunit.org/>

### <a name="implementing-service-tests-on-a-multi-container-application"></a>Implementowanie testów usługi w aplikacji wielokontenera

Jak wspomniano wcześniej, podczas testowania aplikacji z obsługą kontenera wszystkie mikrousługi muszą być uruchomione w obrębie hosta lub klastra kontenerów platformy Docker. Kompleksowe testy usług, które obejmują wiele operacji obejmujących kilka mikrousług, wymagają wdrożenia i uruchomienia całej aplikacji na hoście platformy Docker przez uruchomienie platformy Docker — tworzenie (lub porównywalny mechanizm, jeśli używasz programu Orchestrator). Po uruchomieniu całej aplikacji i wszystkich jej usług można wykonać kompleksową integrację i testy funkcjonalne.

Istnieje kilka metod, których można użyć. W pliku Docker-Compose. yml używanym do wdrażania aplikacji na poziomie rozwiązania można rozszerzyć punkt wejścia, aby użyć [testu dotnet](../../../core/tools/dotnet-test.md). Możesz również użyć innego pliku redagowania, który będzie uruchamiał testy w docelowym obrazie. Przy użyciu innego pliku redagowania dla testów integracji obejmujących mikrousługi i bazy danych w kontenerach można upewnić się, że powiązane dane są zawsze resetowane do pierwotnego stanu przed uruchomieniem testów.

Po uruchomieniu aplikacji redagowania można korzystać z punktów przerwania i wyjątków, jeśli używasz programu Visual Studio. Można też uruchomić testy integracji automatycznie w potoku CI w Azure DevOps Services lub w dowolnym systemie, który obsługuje kontenery platformy Docker.

## <a name="testing-in-eshoponcontainers"></a>Testowanie w eShopOnContainers

Testy aplikacji referencyjnych (eShopOnContainers) zostały niedawno rozbudowane i teraz istnieją cztery kategorie:

1. Testy **jednostkowe** , tylko zwykłe testy jednostkowe, zawarte w elemencie **{mikroservicename}. UnitTests** projekty

2. **Wielousługowe testy funkcjonalne/integracji** z przypadkami testowymi dotyczącymi infrastruktury dla każdej mikrousług, ale odizolowane od innych i zawarte w usłudze **{mikroservicename}. FunctionalTests** projekty.

3. **Testy funkcjonalne/integracji aplikacji**, które koncentrują się na integracji mikrousług, z przypadkami testowymi, które wywierają kilka mikrousług. Te testy znajdują się w projekcie **Application. FunctionalTests**.

Chociaż testy jednostkowe i integracji są zorganizowane w folderze testowym w ramach projektu mikrousług, testy aplikacji i obciążenia są zarządzane oddzielnie pod folderem głównym, jak pokazano na rysunku 6-25.

![Zrzut ekranu przedstawiający a wskazujący niektóre projekty testowe w rozwiązaniu.](./media/test-aspnet-core-services-web-apps/eshoponcontainers-test-folder-structure.png)

**Rysunek 6-25**. Testuj strukturę folderów w eShopOnContainers

Testy funkcjonalne i funkcjonalne/integracji aplikacji są uruchamiane z programu Visual Studio, przy użyciu modułu uruchamiającego testy regularne, ale najpierw należy uruchomić wymagane usługi infrastruktury za pomocą zestawu plików programu Docker, które znajdują się w folderze testowym rozwiązania:

**Docker-Compose-test. yml**

```yml
version: '3.4'

services:
  redis.data:
    image: redis:alpine
  rabbitmq:
    image: rabbitmq:3-management-alpine
  sqldata:
    image: mcr.microsoft.com/mssql/server:2017-latest
  nosqldata:
    image: mongo
```

**Docker-Compose-test. override. yml**

```yml
version: '3.4'

services:
  redis.data:
    ports:
      - "6379:6379"
  rabbitmq:
    ports:
      - "15672:15672"
      - "5672:5672"
  sqldata:
    environment:
      - SA_PASSWORD=Pass@word
      - ACCEPT_EULA=Y
    ports:
      - "5433:1433"
  nosqldata:
    ports:
      - "27017:27017"
```

Aby uruchomić testy funkcjonalne/integracji, należy najpierw uruchomić to polecenie z folderu test rozwiązania:

```console
docker-compose -f docker-compose-test.yml -f docker-compose-test.override.yml up
```

Jak widać, te pliki tworzące platformę Docker umożliwiają uruchamianie tylko mikrousług Redis, RabbitMQ, SQL Server i MongoDB.

### <a name="additional-resources"></a>Zasoby dodatkowe

- **Testowanie integracji jednostek &** na eShopOnContainers \
    <https://github.com/dotnet-architecture/eShopOnContainers/wiki/Unit-and-integration-testing>

- **Testowanie obciążenia** na eShopOnContainers \
    <https://github.com/dotnet-architecture/eShopOnContainers/wiki/Load-testing>

> [!div class="step-by-step"]
> [Poprzedni](subscribe-events.md) 
>  [Dalej](background-tasks-with-ihostedservice.md)
