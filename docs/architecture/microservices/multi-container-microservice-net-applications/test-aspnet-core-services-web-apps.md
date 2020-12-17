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
# <a name="testing-aspnet-core-services-and-web-apps"></a><span data-ttu-id="9e640-103">Testowanie aplikacji internetowych i usług ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="9e640-103">Testing ASP.NET Core services and web apps</span></span>

<span data-ttu-id="9e640-104">Kontrolery są centralną częścią dowolnych ASP.NET Core usługi interfejsu API i aplikacji sieci Web ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="9e640-104">Controllers are a central part of any ASP.NET Core API service and ASP.NET MVC Web application.</span></span> <span data-ttu-id="9e640-105">W związku z tym należy mieć pewność, że zachowanie jest zamierzone dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9e640-105">As such, you should have confidence they behave as intended for your application.</span></span> <span data-ttu-id="9e640-106">Testy automatyczne mogą zapewnić Ci pewność i wykryć błędy przed osiągnięciem ich w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="9e640-106">Automated tests can provide you with this confidence and can detect errors before they reach production.</span></span>

<span data-ttu-id="9e640-107">Należy przetestować, jak działa kontroler na podstawie prawidłowych lub nieprawidłowych danych wejściowych, a także odpowiedzi kontrolera testów na podstawie wyniku wykonywanej przez nią operacji biznesowej.</span><span class="sxs-lookup"><span data-stu-id="9e640-107">You need to test how the controller behaves based on valid or invalid inputs, and test controller responses based on the result of the business operation it performs.</span></span> <span data-ttu-id="9e640-108">Należy jednak mieć następujące typy testów dla mikrousług:</span><span class="sxs-lookup"><span data-stu-id="9e640-108">However, you should have these types of tests for your microservices:</span></span>

- <span data-ttu-id="9e640-109">Testy jednostkowe.</span><span class="sxs-lookup"><span data-stu-id="9e640-109">Unit tests.</span></span> <span data-ttu-id="9e640-110">Zapewniają one, że poszczególne składniki aplikacji działają zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="9e640-110">These ensure that individual components of the application work as expected.</span></span> <span data-ttu-id="9e640-111">Potwierdzenia przetestowania interfejsu API składnika.</span><span class="sxs-lookup"><span data-stu-id="9e640-111">Assertions test the component API.</span></span>

- <span data-ttu-id="9e640-112">Testy integracji.</span><span class="sxs-lookup"><span data-stu-id="9e640-112">Integration tests.</span></span> <span data-ttu-id="9e640-113">Zapewniają one, że interakcje składnika działają zgodnie z oczekiwaniami względem zewnętrznych artefaktów, takich jak bazy danych.</span><span class="sxs-lookup"><span data-stu-id="9e640-113">These ensure that component interactions work as expected against external artifacts like databases.</span></span> <span data-ttu-id="9e640-114">Potwierdzenia mogą testować składnik API, interfejs użytkownika lub skutki uboczne akcji, takich jak baza danych we/wy, rejestrowanie itp.</span><span class="sxs-lookup"><span data-stu-id="9e640-114">Assertions can test component API, UI, or the side effects of actions like database I/O, logging, etc.</span></span>

- <span data-ttu-id="9e640-115">Testy funkcjonalne dla każdej mikrousługi.</span><span class="sxs-lookup"><span data-stu-id="9e640-115">Functional tests for each microservice.</span></span> <span data-ttu-id="9e640-116">Upewnij się, że aplikacja działa zgodnie z oczekiwaniami z perspektywy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9e640-116">These ensure that the application works as expected from the user's perspective.</span></span>

- <span data-ttu-id="9e640-117">Testy usług.</span><span class="sxs-lookup"><span data-stu-id="9e640-117">Service tests.</span></span> <span data-ttu-id="9e640-118">Zapewnia to kompleksowe przypadki użycia usługi, w tym testowanie wielu usług w tym samym czasie, są testowane.</span><span class="sxs-lookup"><span data-stu-id="9e640-118">These ensure that end-to-end service use cases, including testing multiple services at the same time, are tested.</span></span> <span data-ttu-id="9e640-119">W przypadku tego typu testów należy najpierw przygotować środowisko.</span><span class="sxs-lookup"><span data-stu-id="9e640-119">For this type of testing, you need to prepare the environment first.</span></span> <span data-ttu-id="9e640-120">W takim przypadku oznacza to uruchomienie usług (na przykład przy użyciu platformy Docker — tworzenie).</span><span class="sxs-lookup"><span data-stu-id="9e640-120">In this case, it means starting the services (for example, by using docker-compose up).</span></span>

### <a name="implementing-unit-tests-for-aspnet-core-web-apis"></a><span data-ttu-id="9e640-121">Implementowanie testów jednostkowych dla ASP.NET Core interfejsów API sieci Web</span><span class="sxs-lookup"><span data-stu-id="9e640-121">Implementing unit tests for ASP.NET Core Web APIs</span></span>

<span data-ttu-id="9e640-122">Testowanie jednostkowe obejmuje testowanie części aplikacji w izolacji z jej infrastruktury i zależności.</span><span class="sxs-lookup"><span data-stu-id="9e640-122">Unit testing involves testing a part of an application in isolation from its infrastructure and dependencies.</span></span> <span data-ttu-id="9e640-123">W przypadku logiki kontrolera testów jednostkowych jest testowana tylko zawartość pojedynczej akcji lub metody, a nie zachowanie jej zależności lub samego środowiska.</span><span class="sxs-lookup"><span data-stu-id="9e640-123">When you unit test controller logic, only the content of a single action or method is tested, not the behavior of its dependencies or of the framework itself.</span></span> <span data-ttu-id="9e640-124">Testy jednostkowe nie wykrywają problemów interakcji między składnikami, które są celem testowania integracji.</span><span class="sxs-lookup"><span data-stu-id="9e640-124">Unit tests do not detect issues in the interaction between components—that is the purpose of integration testing.</span></span>

<span data-ttu-id="9e640-125">Podczas testowania jednostek akcji kontrolera Pamiętaj, aby skoncentrować się tylko na ich zachowaniu.</span><span class="sxs-lookup"><span data-stu-id="9e640-125">As you unit test your controller actions, make sure you focus only on their behavior.</span></span> <span data-ttu-id="9e640-126">Test jednostkowy kontrolera pozwala uniknąć elementów, takich jak filtry, Routing lub powiązanie modelu (mapowanie danych żądania do ViewModel lub DTO).</span><span class="sxs-lookup"><span data-stu-id="9e640-126">A controller unit test avoids things like filters, routing, or model binding (the mapping of request data to a ViewModel or DTO).</span></span> <span data-ttu-id="9e640-127">Ponieważ koncentrują się na testowaniu tylko jednej rzeczy, testy jednostkowe są zwykle proste do pisania i szybkiego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="9e640-127">Because they focus on testing just one thing, unit tests are generally simple to write and quick to run.</span></span> <span data-ttu-id="9e640-128">Dobrze zapisany zestaw testów jednostkowych może być uruchamiany często bez znacznie większego obciążenia.</span><span class="sxs-lookup"><span data-stu-id="9e640-128">A well-written set of unit tests can be run frequently without much overhead.</span></span>

<span data-ttu-id="9e640-129">Testy jednostkowe są implementowane na podstawie platform testowych, takich jak xUnit.net, MSTest, MOQ lub NUnit.</span><span class="sxs-lookup"><span data-stu-id="9e640-129">Unit tests are implemented based on test frameworks like xUnit.net, MSTest, Moq, or NUnit.</span></span> <span data-ttu-id="9e640-130">W przypadku przykładowej aplikacji eShopOnContainers korzystamy z xUnit.</span><span class="sxs-lookup"><span data-stu-id="9e640-130">For the eShopOnContainers sample application, we are using xUnit.</span></span>

<span data-ttu-id="9e640-131">Podczas pisania testu jednostkowego dla kontrolera interfejsu API sieci Web, można utworzyć wystąpienie klasy kontrolera bezpośrednio przy użyciu słowa kluczowego New w języku C \# , aby test działał tak szybko, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="9e640-131">When you write a unit test for a Web API controller, you instantiate the controller class directly using the new keyword in C\#, so that the test will run as fast as possible.</span></span> <span data-ttu-id="9e640-132">Poniższy przykład pokazuje, jak to zrobić przy użyciu [xUnit](https://xunit.net/) jako środowiska testowego.</span><span class="sxs-lookup"><span data-stu-id="9e640-132">The following example shows how to do this when using [xUnit](https://xunit.net/) as the Test framework.</span></span>

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

### <a name="implementing-integration-and-functional-tests-for-each-microservice"></a><span data-ttu-id="9e640-133">Implementowanie integracji i testów funkcjonalnych dla każdej mikrousługi</span><span class="sxs-lookup"><span data-stu-id="9e640-133">Implementing integration and functional tests for each microservice</span></span>

<span data-ttu-id="9e640-134">Jak wspomniano, testy integracji i testy funkcjonalne mają różne cele i cele.</span><span class="sxs-lookup"><span data-stu-id="9e640-134">As noted, integration tests and functional tests have different purposes and goals.</span></span> <span data-ttu-id="9e640-135">Jednak sposób implementacji obydwu podczas testowania kontrolerów ASP.NET Core jest podobny, dlatego w tej sekcji koncentrujemy się na testach integracji.</span><span class="sxs-lookup"><span data-stu-id="9e640-135">However, the way you implement both when testing ASP.NET Core controllers is similar, so in this section we concentrate on integration tests.</span></span>

<span data-ttu-id="9e640-136">Testowanie integracji gwarantuje, że składniki aplikacji będą działać prawidłowo po złożeniu.</span><span class="sxs-lookup"><span data-stu-id="9e640-136">Integration testing ensures that an application's components function correctly when assembled.</span></span> <span data-ttu-id="9e640-137">ASP.NET Core obsługuje testowanie integracji przy użyciu platform testów jednostkowych oraz wbudowanego hosta sieci Web, który może służyć do obsługi żądań bez obciążenia sieci.</span><span class="sxs-lookup"><span data-stu-id="9e640-137">ASP.NET Core supports integration testing using unit test frameworks and a built-in test web host that can be used to handle requests without network overhead.</span></span>

<span data-ttu-id="9e640-138">W przeciwieństwie do testów jednostkowych, testy integracji często obejmują problemy związane z infrastrukturą aplikacji, takie jak baza danych, system plików, zasoby sieciowe lub żądania sieci Web i odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="9e640-138">Unlike unit testing, integration tests frequently involve application infrastructure concerns, such as a database, file system, network resources, or web requests and responses.</span></span> <span data-ttu-id="9e640-139">Testy jednostkowe wykorzystują elementy sztuczne lub makiety zamiast tych obaw.</span><span class="sxs-lookup"><span data-stu-id="9e640-139">Unit tests use fakes or mock objects in place of these concerns.</span></span> <span data-ttu-id="9e640-140">Jednak celem testów integracji jest upewnienie się, że system działa zgodnie z oczekiwaniami w tych systemach, dlatego w przypadku testowania integracji nie są używane obiekty sztuczne lub makiety.</span><span class="sxs-lookup"><span data-stu-id="9e640-140">But the purpose of integration tests is to confirm that the system works as expected with these systems, so for integration testing you do not use fakes or mock objects.</span></span> <span data-ttu-id="9e640-141">Zamiast tego należy dołączyć infrastrukturę, taką jak dostęp do bazy danych lub Wywoływanie usługi z innych usług.</span><span class="sxs-lookup"><span data-stu-id="9e640-141">Instead, you include the infrastructure, like database access or service invocation from other services.</span></span>

<span data-ttu-id="9e640-142">Ponieważ testy integracji wykonują większe segmenty kodu niż testy jednostkowe, a ponieważ testy integracji korzystają z elementów infrastruktury, są one w porządku o wielkości wolniej niż testy jednostkowe.</span><span class="sxs-lookup"><span data-stu-id="9e640-142">Because integration tests exercise larger segments of code than unit tests, and because integration tests rely on infrastructure elements, they tend to be orders of magnitude slower than unit tests.</span></span> <span data-ttu-id="9e640-143">Z tego względu dobrym pomysłem jest ograniczenie liczby wykonywanych i uruchamianych testów integracji.</span><span class="sxs-lookup"><span data-stu-id="9e640-143">Thus, it is a good idea to limit how many integration tests you write and run.</span></span>

<span data-ttu-id="9e640-144">ASP.NET Core obejmuje wbudowanego hosta sieci Web, który może służyć do obsługi żądań HTTP bez obciążenia sieci, co oznacza, że można uruchamiać te testy szybciej niż w przypadku korzystania z rzeczywistego hosta sieci Web.</span><span class="sxs-lookup"><span data-stu-id="9e640-144">ASP.NET Core includes a built-in test web host that can be used to handle HTTP requests without network overhead, meaning that you can run those tests faster than when using a real web host.</span></span> <span data-ttu-id="9e640-145">Test hosta sieci Web (TestServer) jest dostępny w składniku NuGet jako Microsoft. AspNetCore. TestHost.</span><span class="sxs-lookup"><span data-stu-id="9e640-145">The test web host (TestServer) is available in a NuGet component as Microsoft.AspNetCore.TestHost.</span></span> <span data-ttu-id="9e640-146">Można go dodać do projektów testów integracji i używać do hostowania aplikacji ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="9e640-146">It can be added to integration test projects and used to host ASP.NET Core applications.</span></span>

<span data-ttu-id="9e640-147">Jak widać w poniższym kodzie, podczas tworzenia testów integracji dla kontrolerów ASP.NET Core należy utworzyć wystąpienia kontrolerów za pomocą hosta testowego.</span><span class="sxs-lookup"><span data-stu-id="9e640-147">As you can see in the following code, when you create integration tests for ASP.NET Core controllers, you instantiate the controllers through the test host.</span></span> <span data-ttu-id="9e640-148">Jest to porównywalne do żądania HTTP, ale działa szybciej.</span><span class="sxs-lookup"><span data-stu-id="9e640-148">This is comparable to an HTTP request, but it runs faster.</span></span>

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

#### <a name="additional-resources"></a><span data-ttu-id="9e640-149">Zasoby dodatkowe</span><span class="sxs-lookup"><span data-stu-id="9e640-149">Additional resources</span></span>

- <span data-ttu-id="9e640-150">**Steve Smith. Kontrolery testowania** (ASP.NET Core) </span><span class="sxs-lookup"><span data-stu-id="9e640-150">**Steve Smith. Testing controllers** (ASP.NET Core) </span></span>\
    [https://docs.microsoft.com/aspnet/core/mvc/controllers/testing](/aspnet/core/mvc/controllers/testing)

- <span data-ttu-id="9e640-151">**Steve Smith. Testowanie integracji** (ASP.NET Core) </span><span class="sxs-lookup"><span data-stu-id="9e640-151">**Steve Smith. Integration testing** (ASP.NET Core) </span></span>\
    [https://docs.microsoft.com/aspnet/core/test/integration-tests](/aspnet/core/test/integration-tests)

- <span data-ttu-id="9e640-152">**Testowanie jednostkowe w programie .NET Core przy użyciu testu dotnet** </span><span class="sxs-lookup"><span data-stu-id="9e640-152">**Unit testing in .NET Core using dotnet test** </span></span>\
    [https://docs.microsoft.com/dotnet/core/testing/unit-testing-with-dotnet-test](../../../core/testing/unit-testing-with-dotnet-test.md)

- <span data-ttu-id="9e640-153">**xUnit.NET**.</span><span class="sxs-lookup"><span data-stu-id="9e640-153">**xUnit.net**.</span></span> <span data-ttu-id="9e640-154">Oficjalna lokacja.</span><span class="sxs-lookup"><span data-stu-id="9e640-154">Official site.</span></span> \
    <https://xunit.net/>

- <span data-ttu-id="9e640-155">**Podstawowe informacje o teście jednostkowym.**</span><span class="sxs-lookup"><span data-stu-id="9e640-155">**Unit Test Basics.**</span></span> \
    [https://docs.microsoft.com/visualstudio/test/unit-test-basics](/visualstudio/test/unit-test-basics)

- <span data-ttu-id="9e640-156">**MOQ**.</span><span class="sxs-lookup"><span data-stu-id="9e640-156">**Moq**.</span></span> <span data-ttu-id="9e640-157">Repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="9e640-157">GitHub repo.</span></span> \
    <https://github.com/moq/moq>

- <span data-ttu-id="9e640-158">**Nunit**.</span><span class="sxs-lookup"><span data-stu-id="9e640-158">**NUnit**.</span></span> <span data-ttu-id="9e640-159">Oficjalna lokacja.</span><span class="sxs-lookup"><span data-stu-id="9e640-159">Official site.</span></span> \
    <https://nunit.org/>

### <a name="implementing-service-tests-on-a-multi-container-application"></a><span data-ttu-id="9e640-160">Implementowanie testów usługi w aplikacji wielokontenera</span><span class="sxs-lookup"><span data-stu-id="9e640-160">Implementing service tests on a multi-container application</span></span>

<span data-ttu-id="9e640-161">Jak wspomniano wcześniej, podczas testowania aplikacji z obsługą kontenera wszystkie mikrousługi muszą być uruchomione w obrębie hosta lub klastra kontenerów platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="9e640-161">As noted earlier, when you test multi-container applications, all the microservices need to be running within the Docker host or container cluster.</span></span> <span data-ttu-id="9e640-162">Kompleksowe testy usług, które obejmują wiele operacji obejmujących kilka mikrousług, wymagają wdrożenia i uruchomienia całej aplikacji na hoście platformy Docker przez uruchomienie platformy Docker — tworzenie (lub porównywalny mechanizm, jeśli używasz programu Orchestrator).</span><span class="sxs-lookup"><span data-stu-id="9e640-162">End-to-end service tests that include multiple operations involving several microservices require you to deploy and start the whole application in the Docker host by running docker-compose up (or a comparable mechanism if you are using an orchestrator).</span></span> <span data-ttu-id="9e640-163">Po uruchomieniu całej aplikacji i wszystkich jej usług można wykonać kompleksową integrację i testy funkcjonalne.</span><span class="sxs-lookup"><span data-stu-id="9e640-163">Once the whole application and all its services is running, you can execute end-to-end integration and functional tests.</span></span>

<span data-ttu-id="9e640-164">Istnieje kilka metod, których można użyć.</span><span class="sxs-lookup"><span data-stu-id="9e640-164">There are a few approaches you can use.</span></span> <span data-ttu-id="9e640-165">W pliku Docker-Compose. yml używanym do wdrażania aplikacji na poziomie rozwiązania można rozszerzyć punkt wejścia, aby użyć [testu dotnet](../../../core/tools/dotnet-test.md).</span><span class="sxs-lookup"><span data-stu-id="9e640-165">In the docker-compose.yml file that you use to deploy the application at the solution level you can expand the entry point to use [dotnet test](../../../core/tools/dotnet-test.md).</span></span> <span data-ttu-id="9e640-166">Możesz również użyć innego pliku redagowania, który będzie uruchamiał testy w docelowym obrazie.</span><span class="sxs-lookup"><span data-stu-id="9e640-166">You can also use another compose file that would run your tests in the image you are targeting.</span></span> <span data-ttu-id="9e640-167">Przy użyciu innego pliku redagowania dla testów integracji obejmujących mikrousługi i bazy danych w kontenerach można upewnić się, że powiązane dane są zawsze resetowane do pierwotnego stanu przed uruchomieniem testów.</span><span class="sxs-lookup"><span data-stu-id="9e640-167">By using another compose file for integration tests that includes your microservices and databases on containers, you can make sure that the related data is always reset to its original state before running the tests.</span></span>

<span data-ttu-id="9e640-168">Po uruchomieniu aplikacji redagowania można korzystać z punktów przerwania i wyjątków, jeśli używasz programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9e640-168">Once the compose application is up and running, you can take advantage of breakpoints and exceptions if you are running Visual Studio.</span></span> <span data-ttu-id="9e640-169">Można też uruchomić testy integracji automatycznie w potoku CI w Azure DevOps Services lub w dowolnym systemie, który obsługuje kontenery platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="9e640-169">Or you can run the integration tests automatically in your CI pipeline in Azure DevOps Services or any other CI/CD system that supports Docker containers.</span></span>

## <a name="testing-in-eshoponcontainers"></a><span data-ttu-id="9e640-170">Testowanie w eShopOnContainers</span><span class="sxs-lookup"><span data-stu-id="9e640-170">Testing in eShopOnContainers</span></span>

<span data-ttu-id="9e640-171">Testy aplikacji referencyjnych (eShopOnContainers) zostały niedawno rozbudowane i teraz istnieją cztery kategorie:</span><span class="sxs-lookup"><span data-stu-id="9e640-171">The reference application (eShopOnContainers) tests were recently restructured and now there are four categories:</span></span>

1. <span data-ttu-id="9e640-172">Testy **jednostkowe** , tylko zwykłe testy jednostkowe, zawarte w elemencie **{mikroservicename}. UnitTests** projekty</span><span class="sxs-lookup"><span data-stu-id="9e640-172">**Unit** tests, just plain old regular unit tests, contained in the **{MicroserviceName}.UnitTests** projects</span></span>

2. <span data-ttu-id="9e640-173">**Wielousługowe testy funkcjonalne/integracji** z przypadkami testowymi dotyczącymi infrastruktury dla każdej mikrousług, ale odizolowane od innych i zawarte w usłudze **{mikroservicename}. FunctionalTests** projekty.</span><span class="sxs-lookup"><span data-stu-id="9e640-173">**Microservice functional/integration tests**, with test cases involving the infrastructure for each microservice but isolated from the others and are contained in the **{MicroserviceName}.FunctionalTests** projects.</span></span>

3. <span data-ttu-id="9e640-174">**Testy funkcjonalne/integracji aplikacji**, które koncentrują się na integracji mikrousług, z przypadkami testowymi, które wywierają kilka mikrousług.</span><span class="sxs-lookup"><span data-stu-id="9e640-174">**Application functional/integration tests**, which focus on microservices integration, with test cases that exert several microservices.</span></span> <span data-ttu-id="9e640-175">Te testy znajdują się w projekcie **Application. FunctionalTests**.</span><span class="sxs-lookup"><span data-stu-id="9e640-175">These tests are located in project **Application.FunctionalTests**.</span></span>

<span data-ttu-id="9e640-176">Chociaż testy jednostkowe i integracji są zorganizowane w folderze testowym w ramach projektu mikrousług, testy aplikacji i obciążenia są zarządzane oddzielnie pod folderem głównym, jak pokazano na rysunku 6-25.</span><span class="sxs-lookup"><span data-stu-id="9e640-176">While unit and integration tests are organized in a test folder within the microservice project, application and load tests are managed separately under the root folder, as shown in Figure 6-25.</span></span>

![Zrzut ekranu przedstawiający a wskazujący niektóre projekty testowe w rozwiązaniu.](./media/test-aspnet-core-services-web-apps/eshoponcontainers-test-folder-structure.png)

<span data-ttu-id="9e640-178">**Rysunek 6-25**.</span><span class="sxs-lookup"><span data-stu-id="9e640-178">**Figure 6-25**.</span></span> <span data-ttu-id="9e640-179">Testuj strukturę folderów w eShopOnContainers</span><span class="sxs-lookup"><span data-stu-id="9e640-179">Test folder structure in eShopOnContainers</span></span>

<span data-ttu-id="9e640-180">Testy funkcjonalne i funkcjonalne/integracji aplikacji są uruchamiane z programu Visual Studio, przy użyciu modułu uruchamiającego testy regularne, ale najpierw należy uruchomić wymagane usługi infrastruktury za pomocą zestawu plików programu Docker, które znajdują się w folderze testowym rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="9e640-180">Microservice and Application functional/integration tests are run from Visual Studio, using the regular tests runner, but first you need to start the required infrastructure services, by means of a set of docker-compose files contained in the solution test folder:</span></span>

<span data-ttu-id="9e640-181">**Docker-Compose-test. yml**</span><span class="sxs-lookup"><span data-stu-id="9e640-181">**docker-compose-test.yml**</span></span>

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

<span data-ttu-id="9e640-182">**Docker-Compose-test. override. yml**</span><span class="sxs-lookup"><span data-stu-id="9e640-182">**docker-compose-test.override.yml**</span></span>

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

<span data-ttu-id="9e640-183">Aby uruchomić testy funkcjonalne/integracji, należy najpierw uruchomić to polecenie z folderu test rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="9e640-183">So, to run the functional/integration tests you must first run this command, from the solution test folder:</span></span>

```console
docker-compose -f docker-compose-test.yml -f docker-compose-test.override.yml up
```

<span data-ttu-id="9e640-184">Jak widać, te pliki tworzące platformę Docker umożliwiają uruchamianie tylko mikrousług Redis, RabbitMQ, SQL Server i MongoDB.</span><span class="sxs-lookup"><span data-stu-id="9e640-184">As you can see, these docker-compose files only start the Redis, RabbitMQ, SQL Server and MongoDB microservices.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="9e640-185">Zasoby dodatkowe</span><span class="sxs-lookup"><span data-stu-id="9e640-185">Additional resources</span></span>

- <span data-ttu-id="9e640-186">**Testowanie integracji jednostek &** na eShopOnContainers </span><span class="sxs-lookup"><span data-stu-id="9e640-186">**Unit & Integration testing** on the eShopOnContainers </span></span>\
    <https://github.com/dotnet-architecture/eShopOnContainers/wiki/Unit-and-integration-testing>

- <span data-ttu-id="9e640-187">**Testowanie obciążenia** na eShopOnContainers </span><span class="sxs-lookup"><span data-stu-id="9e640-187">**Load testing** on the eShopOnContainers </span></span>\
    <https://github.com/dotnet-architecture/eShopOnContainers/wiki/Load-testing>

> [!div class="step-by-step"]
> <span data-ttu-id="9e640-188">[Poprzedni](subscribe-events.md) 
>  [Dalej](background-tasks-with-ihostedservice.md)</span><span class="sxs-lookup"><span data-stu-id="9e640-188">[Previous](subscribe-events.md)
[Next](background-tasks-with-ihostedservice.md)</span></span>
