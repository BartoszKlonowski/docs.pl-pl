---
title: Monitorowanie kondycji
description: Poznaj jeden ze sposobów implementacji monitorowania kondycji.
ms.date: 01/07/2019
ms.openlocfilehash: b03506972166eec1864de840c1abda05bc3e5277
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/30/2019
ms.locfileid: "70296045"
---
# <a name="health-monitoring"></a><span data-ttu-id="409b6-103">Monitorowanie kondycji</span><span class="sxs-lookup"><span data-stu-id="409b6-103">Health monitoring</span></span>

<span data-ttu-id="409b6-104">Monitorowanie kondycji może umożliwić niemal w czasie rzeczywistym informacje o stanie kontenerów i mikrousług.</span><span class="sxs-lookup"><span data-stu-id="409b6-104">Health monitoring can allow near-real-time information about the state of your containers and microservices.</span></span> <span data-ttu-id="409b6-105">Monitorowanie kondycji ma kluczowe znaczenie dla wielu aspektów mikrousług operacyjnych i jest szczególnie ważne, gdy koordynator wykonuje częściowe uaktualnienia aplikacji w fazach, jak wyjaśniono później.</span><span class="sxs-lookup"><span data-stu-id="409b6-105">Health monitoring is critical to multiple aspects of operating microservices and is especially important when orchestrators perform partial application upgrades in phases, as explained later.</span></span>

<span data-ttu-id="409b6-106">Aplikacje oparte na mikrousługach często używają pulsu lub kontroli kondycji, aby umożliwić ich monitorom wydajności, harmonogramom i programom Orchestrator śledzenie wielu usług.</span><span class="sxs-lookup"><span data-stu-id="409b6-106">Microservices-based applications often use heartbeats or health checks to enable their performance monitors, schedulers, and orchestrators to keep track of the multitude of services.</span></span> <span data-ttu-id="409b6-107">Jeśli usługi nie mogą wysyłać niektórych rodzajów sygnałów "jestem aktywny", na żądanie lub zgodnie z harmonogramem, aplikacja może stanowić zagrożenie podczas wdrażania aktualizacji lub po prostu wykryć błędy zbyt późne i nie może zatrzymać błędów kaskadowych, które mogą zakończyć się w trakcie poważnych awarii.</span><span class="sxs-lookup"><span data-stu-id="409b6-107">If services cannot send some sort of “I’m alive” signal, either on demand or on a schedule, your application might face risks when you deploy updates, or it might just detect failures too late and not be able to stop cascading failures that can end up in major outages.</span></span>

<span data-ttu-id="409b6-108">W typowym modelu usługi wysyłają raporty dotyczące ich stanu, a informacje te są agregowane w celu zapewnienia ogólnego widoku stanu kondycji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="409b6-108">In the typical model, services send reports about their status, and that information is aggregated to provide an overall view of the state of health of your application.</span></span> <span data-ttu-id="409b6-109">Jeśli używasz programu Orchestrator, możesz podać informacje o kondycji w klastrze programu Orchestrator, aby klaster mógł odpowiednio działać.</span><span class="sxs-lookup"><span data-stu-id="409b6-109">If you're using an orchestrator, you can provide health information to your orchestrator’s cluster, so that the cluster can act accordingly.</span></span> <span data-ttu-id="409b6-110">Jeśli zainwestowano w Raportowanie kondycji o wysokiej jakości dostosowane do Twojej aplikacji, można łatwiej wykrywać i rozwiązywać problemy związane z uruchomioną aplikacją.</span><span class="sxs-lookup"><span data-stu-id="409b6-110">If you invest in high-quality health reporting that's customized for your application, you can detect and fix issues for your running application much more easily.</span></span>

## <a name="implement-health-checks-in-aspnet-core-services"></a><span data-ttu-id="409b6-111">Implementowanie kontroli kondycji w usługach ASP.NET Core Services</span><span class="sxs-lookup"><span data-stu-id="409b6-111">Implement health checks in ASP.NET Core services</span></span>

<span data-ttu-id="409b6-112">Podczas tworzenia ASP.NET Core mikrousług lub aplikacji sieci Web można użyć wbudowanej funkcji kontroli kondycji wydanej w ASP .NET Core 2,2.</span><span class="sxs-lookup"><span data-stu-id="409b6-112">When developing an ASP.NET Core microservice or web application, you can use the built-in health checks feature that was released in ASP .NET Core 2.2.</span></span> <span data-ttu-id="409b6-113">Podobnie jak w przypadku wielu funkcji ASP.NET Core, sprawdzanie kondycji obejmuje zestaw usług i oprogramowanie pośredniczące.</span><span class="sxs-lookup"><span data-stu-id="409b6-113">Like many ASP.NET Core features, health checks come with a set of services and a middleware.</span></span>

<span data-ttu-id="409b6-114">Usługi sprawdzania kondycji i oprogramowanie pośredniczące są łatwe w użyciu i zapewniają możliwości umożliwiające sprawdzenie, czy dowolny zasób zewnętrzny wymagany dla aplikacji (na przykład baza danych SQL Server lub zdalny interfejs API) działa poprawnie.</span><span class="sxs-lookup"><span data-stu-id="409b6-114">Health check services and middleware are easy to use and provide capabilities that let you validate if any external resource needed for your application (like a SQL Server database or a remote API) is working properly.</span></span> <span data-ttu-id="409b6-115">Korzystając z tej funkcji, można także zdecydować, co oznacza, że zasób jest w dobrej kondycji, jak wyjaśniono w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="409b6-115">When you use this feature, you can also decide what it means that the resource is healthy, as we explain later.</span></span>

<span data-ttu-id="409b6-116">Aby efektywnie korzystać z tej funkcji, należy najpierw skonfigurować usługi w mikrousługach.</span><span class="sxs-lookup"><span data-stu-id="409b6-116">To use this feature effectively, you need to first configure services in your microservices.</span></span> <span data-ttu-id="409b6-117">Po drugie potrzebna jest aplikacja frontonu, która wykonuje zapytania dotyczące raportów kondycji.</span><span class="sxs-lookup"><span data-stu-id="409b6-117">Second, you need a front-end application that queries for the health reports.</span></span> <span data-ttu-id="409b6-118">Aplikacja frontonu może być niestandardową aplikacją raportowania lub być samą koordynatorem, który może reagować odpowiednio do Stanów kondycji.</span><span class="sxs-lookup"><span data-stu-id="409b6-118">That front-end application could be a custom reporting application, or it could be an orchestrator itself that can react accordingly to the health states.</span></span>

### <a name="use-the-healthchecks-feature-in-your-back-end-aspnet-microservices"></a><span data-ttu-id="409b6-119">Korzystanie z funkcji HealthChecks w mikrousługach ASP.NET zaplecza</span><span class="sxs-lookup"><span data-stu-id="409b6-119">Use the HealthChecks feature in your back-end ASP.NET microservices</span></span>

<span data-ttu-id="409b6-120">W tej sekcji dowiesz się, jak funkcja HealthChecks jest używana w przykładowej aplikacji interfejsu API sieci Web w ASP.NET Core 2,2.</span><span class="sxs-lookup"><span data-stu-id="409b6-120">In this section, you will learn how the HealthChecks feature is used in a sample ASP.NET Core 2.2 Web API application.</span></span> <span data-ttu-id="409b6-121">Implementacja tej funkcji w dużych mikrousługach skalowania, takich jak eShopOnContainers, została omówiona w dalszej części.</span><span class="sxs-lookup"><span data-stu-id="409b6-121">Implementation of this feature in a large scale microservices like the eShopOnContainers is explained in the later section.</span></span> <span data-ttu-id="409b6-122">Aby rozpocząć, należy określić, co stanowi prawidłowy stan dla każdej mikrousługi.</span><span class="sxs-lookup"><span data-stu-id="409b6-122">To begin, you need to define what constitutes a healthy status for each microservice.</span></span> <span data-ttu-id="409b6-123">W przykładowej aplikacji mikrousługi są w dobrej kondycji, jeśli interfejs API mikrousług jest dostępny za pośrednictwem protokołu HTTP i powiązana SQL Server baza danych jest również dostępna.</span><span class="sxs-lookup"><span data-stu-id="409b6-123">In the sample application, the microservices are healthy if the microservice API is accessible via HTTP and its related SQL Server database is also available.</span></span>

<span data-ttu-id="409b6-124">W programie .NET Core 2,2 z wbudowanymi interfejsami API można skonfigurować usługi, dodać kontrolę kondycji dla mikrousługi i jej zależną SQL Server bazę danych w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="409b6-124">In .NET Core 2.2, with the built-in APIs, you can configure the services, add a Health Check for the microservice and its dependent SQL Server database in this way:</span></span>

```csharp
// Startup.cs from .NET Core 2.2 Web Api sample
//
public void ConfigureServices(IServiceCollection services)
{
    //...
    // Registers required services for health checks
    services.AddHealthChecks()
    // Add a health check for a SQL database
    .AddCheck("MyDatabase", new SqlConnectionHealthCheck(Configuration["ConnectionStrings:DefaultConnection"]));
}
```

<span data-ttu-id="409b6-125">W poprzednim kodzie `services.AddHealthChecks()` Metoda konfiguruje podstawową kontrolę http, która zwraca kod stanu **200** z "dobra".</span><span class="sxs-lookup"><span data-stu-id="409b6-125">In the previous code, the `services.AddHealthChecks()` method configures a basic HTTP check that returns a status code **200** with “Healthy”.</span></span>  <span data-ttu-id="409b6-126">Ponadto Metoda `SqlConnectionHealthCheck` rozszerzania konfiguruje niestandardowy, który sprawdza kondycję powiązanej SQL Database. `AddCheck()`</span><span class="sxs-lookup"><span data-stu-id="409b6-126">Further, the `AddCheck()` extension method configures a custom `SqlConnectionHealthCheck` that checks the related SQL Database’s health.</span></span>

<span data-ttu-id="409b6-127">Metoda dodaje nową kontrolę kondycji z określoną nazwą i implementacją typu `IHealthCheck`. `AddCheck()`</span><span class="sxs-lookup"><span data-stu-id="409b6-127">The `AddCheck()` method adds a new health check with a specified name and the implementation of type `IHealthCheck`.</span></span> <span data-ttu-id="409b6-128">Można dodać wiele kontroli kondycji za pomocą metody ADDCHECK, aby mikrousługa nie zapewniała stanu "zdrowy" do momentu, gdy wszystkie jego sprawdzenia nie będą w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="409b6-128">You can add multiple Health Checks using AddCheck method, so a microservice won't provide a “healthy” status until all its checks are healthy.</span></span>

<span data-ttu-id="409b6-129">`SqlConnectionHealthCheck`jest klasą niestandardową `IHealthCheck`, która implementuje, która przyjmuje parametry połączenia jako parametr konstruktora i wykonuje proste zapytanie, aby sprawdzić, czy połączenie z bazą danych SQL zostało pomyślnie zakończone.</span><span class="sxs-lookup"><span data-stu-id="409b6-129">`SqlConnectionHealthCheck` is a custom class that implements `IHealthCheck`, which takes a connection string as a constructor parameter and executes a simple query to check if the connection to the SQL database is successful.</span></span> <span data-ttu-id="409b6-130">Zwraca `HealthCheckResult.Healthy()` , jeśli zapytanie zostało wykonane pomyślnie `FailureStatus` , a z faktycznym wyjątkiem, gdy zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="409b6-130">It returns `HealthCheckResult.Healthy()` if the query was executed successfully and a `FailureStatus` with the actual exception when it fails.</span></span>

```csharp
// Sample SQL Connection Health Check
public class SqlConnectionHealthCheck : IHealthCheck
{
    private static readonly string DefaultTestQuery = "Select 1";

    public string ConnectionString { get; }

    public string TestQuery { get; }

    public SqlConnectionHealthCheck(string connectionString)
        : this(connectionString, testQuery: DefaultTestQuery)
    {
    }

    public SqlConnectionHealthCheck(string connectionString, string testQuery)
    {
        ConnectionString = connectionString ?? throw new ArgumentNullException(nameof(connectionString));
        TestQuery = testQuery;
    }

    public async Task<HealthCheckResult> CheckHealthAsync(HealthCheckContext context, CancellationToken cancellationToken = default(CancellationToken))
    {
        using (var connection = new SqlConnection(ConnectionString))
        {
            try
            {
                await connection.OpenAsync(cancellationToken);

                if (TestQuery != null)
                {
                    var command = connection.CreateCommand();
                    command.CommandText = TestQuery;

                    await command.ExecuteNonQueryAsync(cancellationToken);
                }
            }
            catch (DbException ex)
            {
                return new HealthCheckResult(status: context.Registration.FailureStatus, exception: ex);
            }
        }

        return HealthCheckResult.Healthy();
    }
}
```

<span data-ttu-id="409b6-131">Należy zauważyć, że w poprzednim kodzie `Select 1` jest zapytanie używane do sprawdzania kondycji bazy danych.</span><span class="sxs-lookup"><span data-stu-id="409b6-131">Note that in the previous code, `Select 1` is the query used to check the Health of the database.</span></span> <span data-ttu-id="409b6-132">Aby monitorować dostępność mikrousług, program Orchestrator, taki jak Kubernetes, i Service Fabric okresowo przeprowadza kontrolę kondycji, wysyłając żądania przetestowania mikrousług.</span><span class="sxs-lookup"><span data-stu-id="409b6-132">To monitor the availability of your microservices, orchestrators like Kubernetes and Service Fabric periodically perform health checks by sending requests to test the microservices.</span></span> <span data-ttu-id="409b6-133">Ważne jest, aby zachować wydajność zapytań bazy danych, aby te operacje były szybkie i nie powodowały większego użycia zasobów.</span><span class="sxs-lookup"><span data-stu-id="409b6-133">It's important to keep your database queries efficient so that these operations are quick and don’t result in a higher utilization of resources.</span></span>

<span data-ttu-id="409b6-134">Na koniec Utwórz oprogramowanie pośredniczące odpowiadające ścieżce URL "/HC":</span><span class="sxs-lookup"><span data-stu-id="409b6-134">Finally, create a middleware that responds to the url path “/hc”:</span></span>

```csharp
// Startup.cs from .NET Core 2.2 Web Api sample
//
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    //…
    app.UseHealthChecks("/hc");
    //…
} 
```

<span data-ttu-id="409b6-135">Gdy punkt końcowy `<yourmicroservice>/hc` jest wywoływany, uruchamia wszystkie kontrole kondycji, które są skonfigurowane `AddHealthChecks()` w metodzie klasy uruchomieniowej i wyświetla wynik.</span><span class="sxs-lookup"><span data-stu-id="409b6-135">When the endpoint `<yourmicroservice>/hc` is invoked, it runs all the health checks that are configured in the `AddHealthChecks()` method in the Startup class and shows the result.</span></span>

### <a name="healthchecks-implementation-in-eshoponcontainers"></a><span data-ttu-id="409b6-136">Implementacja HealthChecks w eShopOnContainers</span><span class="sxs-lookup"><span data-stu-id="409b6-136">HealthChecks implementation in eShopOnContainers</span></span>

<span data-ttu-id="409b6-137">Mikrousługi w eShopOnContainers polegają na wielu usługach do wykonywania zadań.</span><span class="sxs-lookup"><span data-stu-id="409b6-137">Microservices in eShopOnContainers rely on multiple services to perform its task.</span></span> <span data-ttu-id="409b6-138">Na przykład `Catalog.API` mikrousługa z eShopOnContainers zależy od wielu usług, takich jak Azure Blob Storage, SQL Server i RabbitMQ.</span><span class="sxs-lookup"><span data-stu-id="409b6-138">For example, the `Catalog.API` microservice from eShopOnContainers depends on many services, such as Azure Blob Storage, SQL Server, and RabbitMQ.</span></span> <span data-ttu-id="409b6-139">W związku z tym ma kilka testów kondycji dodanych za pomocą `AddCheck()` metody.</span><span class="sxs-lookup"><span data-stu-id="409b6-139">Therefore, it has several health checks added using the `AddCheck()` method.</span></span> <span data-ttu-id="409b6-140">Dla każdej usługi zależnej należy dodać `IHealthCheck` implementację niestandardową, która określa jej odpowiedni stan kondycji.</span><span class="sxs-lookup"><span data-stu-id="409b6-140">For every dependent service, a custom `IHealthCheck` implementation that defines its respective health status needs to be added.</span></span>

<span data-ttu-id="409b6-141">Projekt Open Source [AspNetCore. Diagnostics. HealthChecks](https://github.com/Xabaril/AspNetCore.Diagnostics.HealthChecks) rozwiązuje ten problem, dostarczając niestandardowe implementacje sprawdzania kondycji dla każdej z tych usług przedsiębiorstwa, które są oparte na platformie .net Core 2,2.</span><span class="sxs-lookup"><span data-stu-id="409b6-141">The open-source project [AspNetCore.Diagnostics.HealthChecks](https://github.com/Xabaril/AspNetCore.Diagnostics.HealthChecks) solves this problem by providing custom health check implementations for each of these enterprise services that are built on top of .NET Core 2.2.</span></span> <span data-ttu-id="409b6-142">Każde Sprawdzanie kondycji jest dostępne jako pojedynczy pakiet NuGet, który można łatwo dodać do projektu.</span><span class="sxs-lookup"><span data-stu-id="409b6-142">Each health check is available as an individual NuGet package that can be easily added to the project.</span></span> <span data-ttu-id="409b6-143">eShopOnContainers wykorzystują je w szerokim stopniu we wszystkich mikrousługach.</span><span class="sxs-lookup"><span data-stu-id="409b6-143">eShopOnContainers use them extensively in all its microservices.</span></span>

<span data-ttu-id="409b6-144">Na przykład w `Catalog.API` mikrousłudze dodano następujące pakiety NuGet:</span><span class="sxs-lookup"><span data-stu-id="409b6-144">For instance, in the `Catalog.API` microservice, the following NuGet packages were added:</span></span>

![Widok Eksploratora rozwiązań w projekcie katalogu. API, gdzie są przywoływane pakiety NuGet AspNetCore. Diagnostics. HealthChecks](./media/image6.png)

<span data-ttu-id="409b6-146">**Rysunek 8-7**.</span><span class="sxs-lookup"><span data-stu-id="409b6-146">**Figure 8-7**.</span></span> <span data-ttu-id="409b6-147">Niestandardowe kontrole kondycji zaimplementowane w wykazie. interfejs API przy użyciu AspNetCore. Diagnostics. HealthChecks</span><span class="sxs-lookup"><span data-stu-id="409b6-147">Custom Health Checks implemented in Catalog.API using AspNetCore.Diagnostics.HealthChecks</span></span>

<span data-ttu-id="409b6-148">W poniższym kodzie są dodawane implementacje sprawdzania kondycji dla poszczególnych usług zależnych, a następnie oprogramowanie pośredniczące jest skonfigurowane:</span><span class="sxs-lookup"><span data-stu-id="409b6-148">In the following code, the health check implementations are added for each dependent service and then the middleware is configured:</span></span>

```csharp
// Startup.cs from Catalog.api microservice
//
public static IServiceCollection AddCustomHealthCheck(this IServiceCollection services, IConfiguration configuration)
{
    var accountName = configuration.GetValue<string>("AzureStorageAccountName");
    var accountKey = configuration.GetValue<string>("AzureStorageAccountKey");

    var hcBuilder = services.AddHealthChecks();

    hcBuilder
        .AddSqlServer(
            configuration["ConnectionString"],
            name: "CatalogDB-check",
            tags: new string[] { "catalogdb" });

    if (!string.IsNullOrEmpty(accountName) && !string.IsNullOrEmpty(accountKey))
    {
        hcBuilder
            .AddAzureBlobStorage(
                $"DefaultEndpointsProtocol=https;AccountName={accountName};AccountKey={accountKey};EndpointSuffix=core.windows.net",
                name: "catalog-storage-check",
                tags: new string[] { "catalogstorage" });
    }
    if (configuration.GetValue<bool>("AzureServiceBusEnabled"))
    {
        hcBuilder
            .AddAzureServiceBusTopic(
                configuration["EventBusConnection"],
                topicName: "eshop_event_bus",
                name: "catalog-servicebus-check",
                tags: new string[] { "servicebus" });
    }
    else
    {
        hcBuilder
            .AddRabbitMQ(
                $"amqp://{configuration["EventBusConnection"]}",
                name: "catalog-rabbitmqbus-check",
                tags: new string[] { "rabbitmqbus" });
    }

    return services;
}
```

<span data-ttu-id="409b6-149">Na koniec dodamy oprogramowanie HealthChecker do nasłuchiwania punktu końcowego "/HC":</span><span class="sxs-lookup"><span data-stu-id="409b6-149">Finally, we add the HealthCheck middleware to listen to “/hc” endpoint:</span></span>

```csharp
// HealthCheck middleware
app.UseHealthChecks("/hc", new HealthCheckOptions()
{
    Predicate = _ => true,
    ResponseWriter = UIResponseWriter.WriteHealthCheckUIResponse
});
}
```

### <a name="query-your-microservices-to-report-about-their-health-status"></a><span data-ttu-id="409b6-150">Zbadaj mikrousługi, aby zgłosić ich stan kondycji</span><span class="sxs-lookup"><span data-stu-id="409b6-150">Query your microservices to report about their health status</span></span>

<span data-ttu-id="409b6-151">Po skonfigurowaniu kontroli kondycji zgodnie z opisem w tym artykule, gdy w programie Docker jest uruchomiona mikrousługa, możesz bezpośrednio sprawdzić ją z poziomu przeglądarki, jeśli jest w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="409b6-151">When you've configured health checks as described in this article and you have the microservice running in Docker, you can directly check from a browser if it's healthy.</span></span> <span data-ttu-id="409b6-152">Należy opublikować port kontenera na hoście platformy Docker, aby można było uzyskać dostęp do kontenera za pomocą adresu IP zewnętrznego hosta platformy Docker lub przez `localhost`program, jak pokazano na rysunku 8-8.</span><span class="sxs-lookup"><span data-stu-id="409b6-152">You have to publish the container port in the Docker host, so you can access the container through the external Docker host IP or through `localhost`, as shown in figure 8-8.</span></span>

![Widok przeglądarki odpowiedzi JSON zwróconej przez kontrolę kondycji](./media/image7.png)

<span data-ttu-id="409b6-154">**Rysunek 8-8**.</span><span class="sxs-lookup"><span data-stu-id="409b6-154">**Figure 8-8**.</span></span> <span data-ttu-id="409b6-155">Sprawdzanie stanu kondycji pojedynczej usługi z poziomu przeglądarki</span><span class="sxs-lookup"><span data-stu-id="409b6-155">Checking health status of a single service from a browser</span></span>

<span data-ttu-id="409b6-156">W tym teście można zobaczyć, że `Catalog.API` mikrousługa (uruchomiona na porcie 5101) jest w dobrej kondycji, zwracająca stan http 200 i informacje o stanie w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="409b6-156">In that test, you can see that the `Catalog.API` microservice (running on port 5101) is healthy, returning HTTP status 200 and status information in JSON.</span></span> <span data-ttu-id="409b6-157">Usługa sprawdza również kondycję SQL Server zależność bazy danych i RabbitMQ, więc Sprawdzenie kondycji zgłoszone w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="409b6-157">The service also checked the health of its SQL Server database dependency and RabbitMQ, so the health check reported itself as healthy.</span></span>

## <a name="use-watchdogs"></a><span data-ttu-id="409b6-158">Użyj licznika alarmów</span><span class="sxs-lookup"><span data-stu-id="409b6-158">Use watchdogs</span></span>

<span data-ttu-id="409b6-159">Licznik alarm jest oddzielną usługą, która może oglądać kondycję i ładować różne usługi, a także zgłaszać kondycję dotyczącą mikrousług `HealthChecks` , wykonując zapytania z przemieszczoną wcześniej biblioteką.</span><span class="sxs-lookup"><span data-stu-id="409b6-159">A watchdog is a separate service that can watch health and load across services, and report health about the microservices by querying with the `HealthChecks` library introduced earlier.</span></span> <span data-ttu-id="409b6-160">Może to pomóc zapobiec błędom, które nie zostaną wykryte w oparciu o Widok jednej usługi.</span><span class="sxs-lookup"><span data-stu-id="409b6-160">This can help prevent errors that would not be detected based on the view of a single service.</span></span> <span data-ttu-id="409b6-161">Licznik alarmy jest również dobrym miejscem do kodu hosta, który może wykonywać akcje naprawcze dla znanych warunków bez interakcji z użytkownikiem.</span><span class="sxs-lookup"><span data-stu-id="409b6-161">Watchdogs also are a good place to host code that can perform remediation actions for known conditions without user interaction.</span></span>

<span data-ttu-id="409b6-162">Przykład eShopOnContainers zawiera stronę sieci Web, która wyświetla przykładowe raporty sprawdzania kondycji, jak pokazano na rysunku 8-9.</span><span class="sxs-lookup"><span data-stu-id="409b6-162">The eShopOnContainers sample contains a web page that displays sample health check reports, as shown in Figure 8-9.</span></span> <span data-ttu-id="409b6-163">Jest to najprostsza wartość licznika alarmowego, która może być dostępna, ponieważ pokazuje jedynie stan mikrousług i aplikacji sieci Web w eShopOnContainers.</span><span class="sxs-lookup"><span data-stu-id="409b6-163">This is the simplest watchdog you could have since it only shows the state of the microservices and web applications in eShopOnContainers.</span></span> <span data-ttu-id="409b6-164">Zazwyczaj licznik alarmowy wykonuje także akcje w przypadku wykrycia stanu złej kondycji.</span><span class="sxs-lookup"><span data-stu-id="409b6-164">Usually a watchdog also takes actions when it detects unhealthy states.</span></span>

<span data-ttu-id="409b6-165">Na szczęście [AspNetCore. Diagnostics. HealthChecks](https://github.com/Xabaril/AspNetCore.Diagnostics.HealthChecks) udostępnia również pakiet NuGet [AspNetCore. HealthChecks. UI](https://www.nuget.org/packages/AspNetCore.HealthChecks.UI/) , który może służyć do wyświetlania wyników kontroli kondycji ze skonfigurowanych identyfikatorów URI.</span><span class="sxs-lookup"><span data-stu-id="409b6-165">Fortunately, [AspNetCore.Diagnostics.HealthChecks](https://github.com/Xabaril/AspNetCore.Diagnostics.HealthChecks) also provides [AspNetCore.HealthChecks.UI](https://www.nuget.org/packages/AspNetCore.HealthChecks.UI/) NuGet package that can be used to display the health check results from the configured URIs.</span></span>

![Widok przeglądarki aplikacji webstatus przedstawiający stan kondycji wszystkich mikrousług z eShopOnContainers](./media/image8.png)

<span data-ttu-id="409b6-167">**Rysunek 8-9**.</span><span class="sxs-lookup"><span data-stu-id="409b6-167">**Figure 8-9**.</span></span> <span data-ttu-id="409b6-168">Przykładowy raport sprawdzania kondycji w eShopOnContainers</span><span class="sxs-lookup"><span data-stu-id="409b6-168">Sample health check report in eShopOnContainers</span></span>

<span data-ttu-id="409b6-169">Podsumowując, ta usługa alarm wysyła zapytanie do każdego punktu końcowego mikrousługi "/HC".</span><span class="sxs-lookup"><span data-stu-id="409b6-169">In summary, this watchdog service queries each microservice’s "/hc" endpoint.</span></span> <span data-ttu-id="409b6-170">Spowoduje to wykonanie wszystkich kontroli kondycji zdefiniowanych w ramach tego programu i zwrócenie ogólnej kondycji w zależności od wszystkich tych sprawdzeń.</span><span class="sxs-lookup"><span data-stu-id="409b6-170">This will execute all the health checks defined within it and return an overall health state depending on all those checks.</span></span> <span data-ttu-id="409b6-171">HealthChecksUI jest łatwe do użycia w kilku wpisach konfiguracji i dwóch wierszach kodu, które należy dodać do Startup.cs usługi alarm.</span><span class="sxs-lookup"><span data-stu-id="409b6-171">The HealthChecksUI is easy to consume with a few configuration entries and two lines of code that needs to be added into the Startup.cs of the watchdog service.</span></span>

<span data-ttu-id="409b6-172">Przykładowy plik konfiguracji dla interfejsu użytkownika sprawdzania kondycji:</span><span class="sxs-lookup"><span data-stu-id="409b6-172">Sample configuration file for health check UI:</span></span>

```json
// Configuration
{
  "HealthChecks-UI": {
    "HealthChecks": [
      {
        "Name": "Ordering HTTP Check",
        "Uri": "http://localhost:5102/hc"
      },
      {
        "Name": "Ordering HTTP Background Check",
        "Uri": "http://localhost:5111/hc"
      },
      //...
    ]}
}
```

<span data-ttu-id="409b6-173">Plik Startup.cs, który dodaje HealthChecksUI:</span><span class="sxs-lookup"><span data-stu-id="409b6-173">Startup.cs file that adds HealthChecksUI:</span></span>

```csharp
// Startup.cs from WebStatus(Watch Dog) service
//
public void ConfigureServices(IServiceCollection services)
{
    //…
    // Registers required services for health checks
    services.AddHealthChecksUI();
}
//…
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    //…
    app.UseHealthChecksUI(config=> config.UIPath = “/hc-ui”);
    //…
}
```

## <a name="health-checks-when-using-orchestrators"></a><span data-ttu-id="409b6-174">Sprawdzanie kondycji w przypadku korzystania z programu Orchestrator</span><span class="sxs-lookup"><span data-stu-id="409b6-174">Health checks when using orchestrators</span></span>

<span data-ttu-id="409b6-175">Aby monitorować dostępność mikrousług, program Orchestrator, taki jak Kubernetes, i Service Fabric okresowo przeprowadza kontrolę kondycji, wysyłając żądania przetestowania mikrousług.</span><span class="sxs-lookup"><span data-stu-id="409b6-175">To monitor the availability of your microservices, orchestrators like Kubernetes and Service Fabric periodically perform health checks by sending requests to test the microservices.</span></span> <span data-ttu-id="409b6-176">Gdy koordynator ustali, że usługa/kontener jest w złej kondycji, zatrzyma żądania routingu do tego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="409b6-176">When an orchestrator determines that a service/container is unhealthy, it stops routing requests to that instance.</span></span> <span data-ttu-id="409b6-177">Zwykle tworzy również nowe wystąpienie tego kontenera.</span><span class="sxs-lookup"><span data-stu-id="409b6-177">It also usually creates a new instance of that container.</span></span>

<span data-ttu-id="409b6-178">Na przykład większość programów Orchestrator może korzystać z kontroli kondycji w celu zarządzania wdrożeniami bez przestojów.</span><span class="sxs-lookup"><span data-stu-id="409b6-178">For instance, most orchestrators can use health checks to manage zero-downtime deployments.</span></span> <span data-ttu-id="409b6-179">Tylko wtedy, gdy stan usługi/kontenera zmienia się w dobrej kondycji, program Orchestrator rozpocznie kierowanie ruchu do wystąpień usługi/kontenera.</span><span class="sxs-lookup"><span data-stu-id="409b6-179">Only when the status of a service/container changes to healthy will the orchestrator start routing traffic to service/container instances.</span></span>

<span data-ttu-id="409b6-180">Monitorowanie kondycji jest szczególnie ważne, gdy koordynator wykonuje uaktualnienie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="409b6-180">Health monitoring is especially important when an orchestrator performs an application upgrade.</span></span> <span data-ttu-id="409b6-181">Niektóre programu Orchestrator (takie jak Azure Service Fabric) Update Services w fazach — na przykład mogą zaktualizować jedną piątą powierzchnię klastra dla każdej aktualizacji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="409b6-181">Some orchestrators (like Azure Service Fabric) update services in phases—for example, they might update one-fifth of the cluster surface for each application upgrade.</span></span> <span data-ttu-id="409b6-182">Zestaw węzłów, które są uaktualnione w tym samym czasie, jest określany jako *domena uaktualnienia*.</span><span class="sxs-lookup"><span data-stu-id="409b6-182">The set of nodes that's upgraded at the same time is referred to as an *upgrade domain*.</span></span> <span data-ttu-id="409b6-183">Po uaktualnieniu każdej domeny uaktualnienia i udostępnieniu jej użytkownikom ta domena uaktualnienia musi przekazywać kontrolę kondycji, zanim wdrożenie przejdzie do następnej domeny uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="409b6-183">After each upgrade domain has been upgraded and is available to users, that upgrade domain must pass health checks before the deployment moves to the next upgrade domain.</span></span>

<span data-ttu-id="409b6-184">Innym aspektem kondycji usługi jest raportowanie metryk z usługi.</span><span class="sxs-lookup"><span data-stu-id="409b6-184">Another aspect of service health is reporting metrics from the service.</span></span> <span data-ttu-id="409b6-185">Jest to zaawansowana funkcja modelu kondycji niektórych koordynatorów, taka jak Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="409b6-185">This is an advanced capability of the health model of some orchestrators, like Service Fabric.</span></span> <span data-ttu-id="409b6-186">Metryki są ważne w przypadku korzystania z programu Orchestrator, ponieważ służą do zrównoważenia użycia zasobów.</span><span class="sxs-lookup"><span data-stu-id="409b6-186">Metrics are important when using an orchestrator because they are used to balance resource usage.</span></span> <span data-ttu-id="409b6-187">Metryki mogą również stanowić wskaźnik kondycji systemu.</span><span class="sxs-lookup"><span data-stu-id="409b6-187">Metrics also can be an indicator of system health.</span></span> <span data-ttu-id="409b6-188">Przykładowo może istnieć aplikacja, która ma wiele mikrousług, a każde wystąpienie raportuje metrykę żądań na sekundę (RPS pliku).</span><span class="sxs-lookup"><span data-stu-id="409b6-188">For example, you might have an application that has many microservices, and each instance reports a requests-per-second (RPS) metric.</span></span> <span data-ttu-id="409b6-189">Jeśli jedna usługa korzysta z większej liczby zasobów (pamięci, procesora itp.) niż inna usługa, program Orchestrator może przenieść wystąpienia usługi w klastrze, aby spróbować zachować nawet wykorzystanie zasobów.</span><span class="sxs-lookup"><span data-stu-id="409b6-189">If one service is using more resources (memory, processor, etc.) than another service, the orchestrator could move service instances around in the cluster to try to maintain even resource utilization.</span></span>

<span data-ttu-id="409b6-190">Należy pamiętać, że usługa Azure Service Fabric oferuje własny [model monitorowania kondycji](/azure/service-fabric/service-fabric-health-introduction), który jest bardziej zaawansowany niż proste kontrole kondycji.</span><span class="sxs-lookup"><span data-stu-id="409b6-190">Note that Azure Service Fabric provides its own [Health Monitoring model](/azure/service-fabric/service-fabric-health-introduction), which is more advanced than simple health checks.</span></span>

## <a name="advanced-monitoring-visualization-analysis-and-alerts"></a><span data-ttu-id="409b6-191">Zaawansowane monitorowanie: wizualizacja, analiza i alerty</span><span class="sxs-lookup"><span data-stu-id="409b6-191">Advanced monitoring: visualization, analysis, and alerts</span></span>

<span data-ttu-id="409b6-192">Ostatnia część monitorowania polega na wizualizowaniu strumienia zdarzeń, raportowaniu wydajności usługi i wysyłaniu alertów w przypadku wykrycia problemu.</span><span class="sxs-lookup"><span data-stu-id="409b6-192">The final part of monitoring is visualizing the event stream, reporting on service performance, and alerting when an issue is detected.</span></span> <span data-ttu-id="409b6-193">Do tego aspektu monitorowania można użyć różnych rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="409b6-193">You can use different solutions for this aspect of monitoring.</span></span>

<span data-ttu-id="409b6-194">Możesz użyć prostych aplikacji niestandardowych pokazujących stan usług, takich jak niestandardowa strona wyświetlana przy objaśnianiu [AspNetCore. Diagnostics. HealthChecks](https://github.com/Xabaril/AspNetCore.Diagnostics.HealthChecks).</span><span class="sxs-lookup"><span data-stu-id="409b6-194">You can use simple custom applications showing the state of your services, like the custom page shown when explaining the [AspNetCore.Diagnostics.HealthChecks](https://github.com/Xabaril/AspNetCore.Diagnostics.HealthChecks).</span></span> <span data-ttu-id="409b6-195">Można też użyć bardziej zaawansowanych narzędzi, takich jak [Azure monitor](https://azure.microsoft.com/services/monitor/) , aby zgłosić alerty na podstawie strumienia zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="409b6-195">Or you could use more advanced tools like [Azure Monitor](https://azure.microsoft.com/services/monitor/) to raise alerts based on the stream of events.</span></span>

<span data-ttu-id="409b6-196">Na koniec, Jeśli przechowujesz wszystkie strumienie zdarzeń, możesz użyć programu Microsoft Power BI lub innych rozwiązań, takich jak Kibana lub Splunk, aby wizualizować dane.</span><span class="sxs-lookup"><span data-stu-id="409b6-196">Finally, if you're storing all the event streams, you can use Microsoft Power BI or other solutions like Kibana or Splunk to visualize the data.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="409b6-197">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="409b6-197">Additional resources</span></span>

- <span data-ttu-id="409b6-198">**Interfejs użytkownika HealthChecks i HealthChecks dla ASP.NET Core** </span><span class="sxs-lookup"><span data-stu-id="409b6-198">**HealthChecks and HealthChecks UI for ASP.NET Core** </span></span>\
  <https://github.com/Xabaril/AspNetCore.Diagnostics.HealthChecks>

- <span data-ttu-id="409b6-199">**Wprowadzenie do monitorowania kondycji Service Fabric** </span><span class="sxs-lookup"><span data-stu-id="409b6-199">**Introduction to Service Fabric health monitoring** </span></span>\
  [https://docs.microsoft.com/azure/service-fabric/service-fabric-health-introduction](/azure/service-fabric/service-fabric-health-introduction)

- <span data-ttu-id="409b6-200">**Azure Monitor**
  <https://azure.microsoft.com/services/monitor/></span><span class="sxs-lookup"><span data-stu-id="409b6-200">**Azure Monitor**
<https://azure.microsoft.com/services/monitor/></span></span>

>[!div class="step-by-step"]
><span data-ttu-id="409b6-201">[Poprzedni](implement-circuit-breaker-pattern.md)Następny
>[](../secure-net-microservices-web-applications/index.md)</span><span class="sxs-lookup"><span data-stu-id="409b6-201">[Previous](implement-circuit-breaker-pattern.md)
[Next](../secure-net-microservices-web-applications/index.md)</span></span>