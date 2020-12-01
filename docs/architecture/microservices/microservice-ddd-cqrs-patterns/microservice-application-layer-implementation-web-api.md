---
title: Implementowanie warstwy aplikacji mikrousług za pomocą internetowego interfejsu API
description: Zapoznaj się z iniekcją zależności i wzorcami mediator oraz ich szczegóły implementacji w warstwie aplikacji internetowego interfejsu API.
ms.date: 08/17/2020
ms.openlocfilehash: 45121026e06c55258a16f41aa801c06808a6919f
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96437793"
---
# <a name="implement-the-microservice-application-layer-using-the-web-api"></a><span data-ttu-id="33f95-103">Implementowanie warstwy aplikacji mikrousług za pomocą internetowego interfejsu API</span><span class="sxs-lookup"><span data-stu-id="33f95-103">Implement the microservice application layer using the Web API</span></span>

## <a name="use-dependency-injection-to-inject-infrastructure-objects-into-your-application-layer"></a><span data-ttu-id="33f95-104">Użyj iniekcji zależności, aby wstrzyknąć obiekty infrastruktury do warstwy aplikacji</span><span class="sxs-lookup"><span data-stu-id="33f95-104">Use Dependency Injection to inject infrastructure objects into your application layer</span></span>

<span data-ttu-id="33f95-105">Jak wspomniano wcześniej, warstwa aplikacji może być implementowana w ramach kompilowanego artefaktu (zestawu), takiego jak w projekcie interfejsu API sieci Web lub w projekcie aplikacji sieci Web MVC.</span><span class="sxs-lookup"><span data-stu-id="33f95-105">As mentioned previously, the application layer can be implemented as part of the artifact (assembly) you are building, such as within a Web API project or an MVC web app project.</span></span> <span data-ttu-id="33f95-106">W przypadku mikrousługi skompilowanej przy ASP.NET Core warstwa aplikacji zazwyczaj będzie biblioteką internetowego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="33f95-106">In the case of a microservice built with ASP.NET Core, the application layer will usually be your Web API library.</span></span> <span data-ttu-id="33f95-107">Jeśli chcesz oddzielić dane pochodzące z ASP.NET Core (infrastruktury oraz kontrolerów) z niestandardowego kodu warstwy aplikacji, możesz również umieścić warstwę aplikacji w oddzielnej bibliotece klas, ale jest to opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="33f95-107">If you want to separate what is coming from ASP.NET Core (its infrastructure plus your controllers) from your custom application layer code, you could also place your application layer in a separate class library, but that is optional.</span></span>

<span data-ttu-id="33f95-108">Na przykład kod warstwy aplikacji mikrousługi porządkowania jest bezpośrednio zaimplementowany jako część projektu **porządkowania. API** (projekt ASP.NET Core Web API), jak pokazano na rysunku 7-23.</span><span class="sxs-lookup"><span data-stu-id="33f95-108">For instance, the application layer code of the ordering microservice is directly implemented as part of the **Ordering.API** project (an ASP.NET Core Web API project), as shown in Figure 7-23.</span></span>

:::image type="complex" source="./media/microservice-application-layer-implementation-web-api/ordering-api-microservice.png" alt-text="Zrzut ekranu przedstawiający mikrousługę porządkowanie. API w Eksplorator rozwiązań.":::
<span data-ttu-id="33f95-110">Widok Eksplorator rozwiązań mikrousługi porządkowania. API, pokazujący podfoldery w folderze aplikacji: zachowania, polecenia, DomainEventHandlers, IntegrationEvents, modele, zapytania i walidacje.</span><span class="sxs-lookup"><span data-stu-id="33f95-110">The Solution Explorer view of the Ordering.API microservice, showing the subfolders under the Application folder: Behaviors, Commands, DomainEventHandlers, IntegrationEvents, Models, Queries, and Validations.</span></span>
:::image-end:::

<span data-ttu-id="33f95-111">**Rysunek 7-23**.</span><span class="sxs-lookup"><span data-stu-id="33f95-111">**Figure 7-23**.</span></span> <span data-ttu-id="33f95-112">Warstwa aplikacji w projekcie interfejsu API sieci Web programu porządkowanie. API ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="33f95-112">The application layer in the Ordering.API ASP.NET Core Web API project</span></span>

<span data-ttu-id="33f95-113">ASP.NET Core obejmuje prosty [wbudowany kontener IOC](/aspnet/core/fundamentals/dependency-injection) (reprezentowany przez interfejs IServiceProvider), który domyślnie obsługuje iniekcję konstruktora, a ASP.NET udostępnia niektóre usługi za pomocą di.</span><span class="sxs-lookup"><span data-stu-id="33f95-113">ASP.NET Core includes a simple [built-in IoC container](/aspnet/core/fundamentals/dependency-injection) (represented by the IServiceProvider interface) that supports constructor injection by default, and ASP.NET makes certain services available through DI.</span></span> <span data-ttu-id="33f95-114">ASP.NET Core używa *usługi* Term dla dowolnego typu rejestru, który zostanie dodany przez di.</span><span class="sxs-lookup"><span data-stu-id="33f95-114">ASP.NET Core uses the term *service* for any of the types you register that will be injected through DI.</span></span> <span data-ttu-id="33f95-115">Należy skonfigurować usługi wbudowanego kontenera w metodzie ConfigureServices w klasie startowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="33f95-115">You configure the built-in container's services in the ConfigureServices method in your application's Startup class.</span></span> <span data-ttu-id="33f95-116">Zależności są implementowane w usługach, które są wymagane przez typ i rejestrowane w kontenerze IoC.</span><span class="sxs-lookup"><span data-stu-id="33f95-116">Your dependencies are implemented in the services that a type needs and that you register in the IoC container.</span></span>

<span data-ttu-id="33f95-117">Zazwyczaj należy wstrzyknąć zależności, które implementują obiekty infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="33f95-117">Typically, you want to inject dependencies that implement infrastructure objects.</span></span> <span data-ttu-id="33f95-118">Typową zależnością do iniekcji jest repozytorium.</span><span class="sxs-lookup"><span data-stu-id="33f95-118">A typical dependency to inject is a repository.</span></span> <span data-ttu-id="33f95-119">Można jednak wprowadzić inną zależność infrastruktury, którą może mieć.</span><span class="sxs-lookup"><span data-stu-id="33f95-119">But you could inject any other infrastructure dependency that you may have.</span></span> <span data-ttu-id="33f95-120">W przypadku prostszej implementacji można bezpośrednio wstrzyknąć obiekt wzorca jednostki pracy (obiekt EF DbContext), ponieważ DbContext jest również implementacją obiektów trwałości infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="33f95-120">For simpler implementations, you could directly inject your Unit of Work pattern object (the EF DbContext object), because the DBContext is also the implementation of your infrastructure persistence objects.</span></span>

<span data-ttu-id="33f95-121">W poniższym przykładzie można zobaczyć, jak platforma .NET Core wprowadza wymagane obiekty repozytorium za pomocą konstruktora.</span><span class="sxs-lookup"><span data-stu-id="33f95-121">In the following example, you can see how .NET Core is injecting the required repository objects through the constructor.</span></span> <span data-ttu-id="33f95-122">Klasa jest programem obsługi poleceń, który zostanie uwzględniony w następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="33f95-122">The class is a command handler, which will get covered in the next section.</span></span>

```csharp
public class CreateOrderCommandHandler
        : IRequestHandler<CreateOrderCommand, bool>
{
    private readonly IOrderRepository _orderRepository;
    private readonly IIdentityService _identityService;
    private readonly IMediator _mediator;
    private readonly IOrderingIntegrationEventService _orderingIntegrationEventService;
    private readonly ILogger<CreateOrderCommandHandler> _logger;

    // Using DI to inject infrastructure persistence Repositories
    public CreateOrderCommandHandler(IMediator mediator,
        IOrderingIntegrationEventService orderingIntegrationEventService,
        IOrderRepository orderRepository,
        IIdentityService identityService,
        ILogger<CreateOrderCommandHandler> logger)
    {
        _orderRepository = orderRepository ?? throw new ArgumentNullException(nameof(orderRepository));
        _identityService = identityService ?? throw new ArgumentNullException(nameof(identityService));
        _mediator = mediator ?? throw new ArgumentNullException(nameof(mediator));
        _orderingIntegrationEventService = orderingIntegrationEventService ?? throw new ArgumentNullException(nameof(orderingIntegrationEventService));
        _logger = logger ?? throw new ArgumentNullException(nameof(logger));
    }

    public async Task<bool> Handle(CreateOrderCommand message, CancellationToken cancellationToken)
    {
        // Add Integration event to clean the basket
        var orderStartedIntegrationEvent = new OrderStartedIntegrationEvent(message.UserId);
        await _orderingIntegrationEventService.AddAndSaveEventAsync(orderStartedIntegrationEvent);

        // Add/Update the Buyer AggregateRoot
        // DDD patterns comment: Add child entities and value-objects through the Order Aggregate-Root
        // methods and constructor so validations, invariants and business logic
        // make sure that consistency is preserved across the whole aggregate
        var address = new Address(message.Street, message.City, message.State, message.Country, message.ZipCode);
        var order = new Order(message.UserId, message.UserName, address, message.CardTypeId, message.CardNumber, message.CardSecurityNumber, message.CardHolderName, message.CardExpiration);

        foreach (var item in message.OrderItems)
        {
            order.AddOrderItem(item.ProductId, item.ProductName, item.UnitPrice, item.Discount, item.PictureUrl, item.Units);
        }

        _logger.LogInformation("----- Creating Order - Order: {@Order}", order);

        _orderRepository.Add(order);

        return await _orderRepository.UnitOfWork
            .SaveEntitiesAsync(cancellationToken);
    }
}

```

<span data-ttu-id="33f95-123">Klasa używa wstrzykniętych repozytoriów, aby wykonać transakcję i zachować zmiany stanu.</span><span class="sxs-lookup"><span data-stu-id="33f95-123">The class uses the injected repositories to execute the transaction and persist the state changes.</span></span> <span data-ttu-id="33f95-124">Nie ma znaczenia, czy ta klasa jest programem obsługi poleceń, metodą ASP.NET Core kontrolerem interfejsu API sieci Web, czy [usługą aplikacji DDD](https://lostechies.com/jimmybogard/2008/08/21/services-in-domain-driven-design/).</span><span class="sxs-lookup"><span data-stu-id="33f95-124">It does not matter whether that class is a command handler, an ASP.NET Core Web API controller method, or a [DDD Application Service](https://lostechies.com/jimmybogard/2008/08/21/services-in-domain-driven-design/).</span></span> <span data-ttu-id="33f95-125">Jest ona ostatecznie prostą klasą, która używa repozytoriów, jednostek domeny i innej koordynacji aplikacji w sposób podobny do procedury obsługi poleceń.</span><span class="sxs-lookup"><span data-stu-id="33f95-125">It is ultimately a simple class that uses repositories, domain entities, and other application coordination in a fashion similar to a command handler.</span></span> <span data-ttu-id="33f95-126">Iniekcja zależności działa tak samo jak w przypadku wszystkich wymienionych klas, jak w przykładzie przy użyciu DI na podstawie konstruktora.</span><span class="sxs-lookup"><span data-stu-id="33f95-126">Dependency Injection works the same way for all the mentioned classes, as in the example using DI based on the constructor.</span></span>

### <a name="register-the-dependency-implementation-types-and-interfaces-or-abstractions"></a><span data-ttu-id="33f95-127">Rejestrowanie typów implementacji zależności oraz interfejsów lub streszczeń</span><span class="sxs-lookup"><span data-stu-id="33f95-127">Register the dependency implementation types and interfaces or abstractions</span></span>

<span data-ttu-id="33f95-128">Przed użyciem obiektów wstrzykiwanych za pomocą konstruktorów należy wiedzieć, gdzie należy zarejestrować interfejsy i klasy, które tworzą obiekty wstrzykiwane do klas aplikacji za pomocą DI.</span><span class="sxs-lookup"><span data-stu-id="33f95-128">Before you use the objects injected through constructors, you need to know where to register the interfaces and classes that produce the objects injected into your application classes through DI.</span></span> <span data-ttu-id="33f95-129">(Podobnie jak w przypadku konstruktora, jak pokazano wcześniej).</span><span class="sxs-lookup"><span data-stu-id="33f95-129">(Like DI based on the constructor, as shown previously.)</span></span>

#### <a name="use-the-built-in-ioc-container-provided-by-aspnet-core"></a><span data-ttu-id="33f95-130">Użyj wbudowanego kontenera IoC zapewnianego przez ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="33f95-130">Use the built-in IoC container provided by ASP.NET Core</span></span>

<span data-ttu-id="33f95-131">W przypadku korzystania z wbudowanego kontenera IoC dostarczonego przez ASP.NET Core należy zarejestrować typy, które mają zostać dodane w metodzie ConfigureServices w pliku Startup.cs, tak jak w poniższym kodzie:</span><span class="sxs-lookup"><span data-stu-id="33f95-131">When you use the built-in IoC container provided by ASP.NET Core, you register the types you want to inject in the ConfigureServices method in the Startup.cs file, as in the following code:</span></span>

```csharp
// Registration of types into ASP.NET Core built-in container
public void ConfigureServices(IServiceCollection services)
{
    // Register out-of-the-box framework services.
    services.AddDbContext<CatalogContext>(c =>
        c.UseSqlServer(Configuration["ConnectionString"]),
        ServiceLifetime.Scoped);

    services.AddMvc();
    // Register custom application dependencies.
    services.AddScoped<IMyCustomRepository, MyCustomSQLRepository>();
}
```

<span data-ttu-id="33f95-132">Typowym wzorcem rejestrowania typów w kontenerze IoC jest zarejestrowanie pary typów — interfejsu i powiązanej klasy implementacji.</span><span class="sxs-lookup"><span data-stu-id="33f95-132">The most common pattern when registering types in an IoC container is to register a pair of types—an interface and its related implementation class.</span></span> <span data-ttu-id="33f95-133">Następnie po zażądaniu obiektu z kontenera IoC za pomocą dowolnego konstruktora należy zażądać obiektu określonego typu interfejsu.</span><span class="sxs-lookup"><span data-stu-id="33f95-133">Then when you request an object from the IoC container through any constructor, you request an object of a certain type of interface.</span></span> <span data-ttu-id="33f95-134">Na przykład, w poprzednim przykładzie, ostatni wiersz stan, gdy którykolwiek z konstruktorów ma zależność od IMyCustomRepository (interfejs lub Abstrakcja), kontener IoC będzie wstrzyknąć wystąpienie klasy implementacji MyCustomSQLServerRepository.</span><span class="sxs-lookup"><span data-stu-id="33f95-134">For instance, in the previous example, the last line states that when any of your constructors have a dependency on IMyCustomRepository (interface or abstraction), the IoC container will inject an instance of the MyCustomSQLServerRepository implementation class.</span></span>

#### <a name="use-the-scrutor-library-for-automatic-types-registration"></a><span data-ttu-id="33f95-135">Rejestracja typów automatycznych przy użyciu biblioteki Scrutor</span><span class="sxs-lookup"><span data-stu-id="33f95-135">Use the Scrutor library for automatic types registration</span></span>

<span data-ttu-id="33f95-136">W przypadku korzystania z funkcji DI w oprogramowaniu .NET Core warto mieć możliwość skanowania zestawu i automatycznego rejestrowania jego typów według Konwencji.</span><span class="sxs-lookup"><span data-stu-id="33f95-136">When using DI in .NET Core, you might want to be able to scan an assembly and automatically register its types by convention.</span></span> <span data-ttu-id="33f95-137">Ta funkcja nie jest obecnie dostępna w ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="33f95-137">This feature is not currently available in ASP.NET Core.</span></span> <span data-ttu-id="33f95-138">Można jednak użyć biblioteki [Scrutor](https://github.com/khellang/Scrutor) dla tego programu.</span><span class="sxs-lookup"><span data-stu-id="33f95-138">However, you can use the [Scrutor](https://github.com/khellang/Scrutor) library for that.</span></span> <span data-ttu-id="33f95-139">Takie podejście jest wygodne, gdy masz dziesiątki typów, które muszą być zarejestrowane w kontenerze IoC.</span><span class="sxs-lookup"><span data-stu-id="33f95-139">This approach is convenient when you have dozens of types that need to be registered in your IoC container.</span></span>

#### <a name="additional-resources"></a><span data-ttu-id="33f95-140">Zasoby dodatkowe</span><span class="sxs-lookup"><span data-stu-id="33f95-140">Additional resources</span></span>

- <span data-ttu-id="33f95-141">**Matthew króla. Rejestrowanie usług w usłudze Scrutor** </span><span class="sxs-lookup"><span data-stu-id="33f95-141">**Matthew King. Registering services with Scrutor** </span></span>\
  <https://www.mking.net/blog/registering-services-with-scrutor>

- <span data-ttu-id="33f95-142">**Kristian Hellang. Scrutor.**</span><span class="sxs-lookup"><span data-stu-id="33f95-142">**Kristian Hellang. Scrutor.**</span></span> <span data-ttu-id="33f95-143">Repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="33f95-143">GitHub repo.</span></span> \
  <https://github.com/khellang/Scrutor>

#### <a name="use-autofac-as-an-ioc-container"></a><span data-ttu-id="33f95-144">Używanie Autofac jako kontenera IoC</span><span class="sxs-lookup"><span data-stu-id="33f95-144">Use Autofac as an IoC container</span></span>

<span data-ttu-id="33f95-145">Można również użyć dodatkowych kontenerów IoC i podłączyć je do potoku ASP.NET Core, jak w mikrousłudze porządkowania w eShopOnContainers, która używa [Autofac](https://autofac.org/).</span><span class="sxs-lookup"><span data-stu-id="33f95-145">You can also use additional IoC containers and plug them into the ASP.NET Core pipeline, as in the ordering microservice in eShopOnContainers, which uses [Autofac](https://autofac.org/).</span></span> <span data-ttu-id="33f95-146">W przypadku korzystania z Autofac zazwyczaj rejestruje się typy za pośrednictwem modułów, które umożliwiają podział typów rejestracji między wiele plików w zależności od tego, gdzie są typy, podobnie jak w przypadku typów aplikacji rozproszonych w wielu bibliotekach klas.</span><span class="sxs-lookup"><span data-stu-id="33f95-146">When using Autofac you typically register the types via modules, which allow you to split the registration types between multiple files depending on where your types are, just as you could have the application types distributed across multiple class libraries.</span></span>

<span data-ttu-id="33f95-147">Na przykład poniżej przedstawiono [moduł aplikacji Autofac](https://github.com/dotnet-architecture/eShopOnContainers/blob/master/src/Services/Ordering/Ordering.API/Infrastructure/AutofacModules/ApplicationModule.cs) dla projektu [interfejsu API sieci Web porządkowania. API](https://github.com/dotnet-architecture/eShopOnContainers/tree/master/src/Services/Ordering/Ordering.API) z typami, które mają zostać dodane.</span><span class="sxs-lookup"><span data-stu-id="33f95-147">For example, the following is the [Autofac application module](https://github.com/dotnet-architecture/eShopOnContainers/blob/master/src/Services/Ordering/Ordering.API/Infrastructure/AutofacModules/ApplicationModule.cs) for the [Ordering.API Web API](https://github.com/dotnet-architecture/eShopOnContainers/tree/master/src/Services/Ordering/Ordering.API) project with the types you will want to inject.</span></span>

```csharp
public class ApplicationModule : Autofac.Module
{
    public string QueriesConnectionString { get; }
    public ApplicationModule(string qconstr)
    {
        QueriesConnectionString = qconstr;
    }

    protected override void Load(ContainerBuilder builder)
    {
        builder.Register(c => new OrderQueries(QueriesConnectionString))
            .As<IOrderQueries>()
            .InstancePerLifetimeScope();
        builder.RegisterType<BuyerRepository>()
            .As<IBuyerRepository>()
            .InstancePerLifetimeScope();
        builder.RegisterType<OrderRepository>()
            .As<IOrderRepository>()
            .InstancePerLifetimeScope();
        builder.RegisterType<RequestManager>()
            .As<IRequestManager>()
            .InstancePerLifetimeScope();
   }
}
```

<span data-ttu-id="33f95-148">Autofac ma również funkcję do [skanowania zestawów i rejestrowania typów według konwencji nazw](https://autofac.readthedocs.io/en/latest/register/scanning.html).</span><span class="sxs-lookup"><span data-stu-id="33f95-148">Autofac also has a feature to [scan assemblies and register types by name conventions](https://autofac.readthedocs.io/en/latest/register/scanning.html).</span></span>

<span data-ttu-id="33f95-149">Proces rejestracji i pojęcia są bardzo podobne do sposobu rejestrowania typów przy użyciu wbudowanego kontenera ASP.NET Core IoC, ale Składnia używana Autofac jest nieco inna.</span><span class="sxs-lookup"><span data-stu-id="33f95-149">The registration process and concepts are very similar to the way you can register types with the built-in ASP.NET Core IoC container, but the syntax when using Autofac is a bit different.</span></span>

<span data-ttu-id="33f95-150">W przykładowym kodzie IOrderRepository abstrakcji jest rejestrowany wraz z klasą implementacji OrderRepository.</span><span class="sxs-lookup"><span data-stu-id="33f95-150">In the example code, the abstraction IOrderRepository is registered along with the implementation class OrderRepository.</span></span> <span data-ttu-id="33f95-151">Oznacza to, że za każdym razem, gdy Konstruktor deklaruje zależność poprzez abstrakcyjność lub interfejs IOrderRepository, kontener IoC będzie wstrzyknąć wystąpienie klasy OrderRepository.</span><span class="sxs-lookup"><span data-stu-id="33f95-151">This means that whenever a constructor is declaring a dependency through the IOrderRepository abstraction or interface, the IoC container will inject an instance of the OrderRepository class.</span></span>

<span data-ttu-id="33f95-152">Typ zakresu wystąpienia określa, jak wystąpienie jest udostępniane między żądaniami dla tej samej usługi lub zależności.</span><span class="sxs-lookup"><span data-stu-id="33f95-152">The instance scope type determines how an instance is shared between requests for the same service or dependency.</span></span> <span data-ttu-id="33f95-153">Gdy żądanie jest tworzone dla zależności, kontener IoC może zwrócić następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="33f95-153">When a request is made for a dependency, the IoC container can return the following:</span></span>

- <span data-ttu-id="33f95-154">Pojedyncze wystąpienie na okres istnienia (określone w ASP.NET Core kontener IoC jako *objęty zakresem*).</span><span class="sxs-lookup"><span data-stu-id="33f95-154">A single instance per lifetime scope (referred to in the ASP.NET Core IoC container as *scoped*).</span></span>

- <span data-ttu-id="33f95-155">Nowe wystąpienie na zależność (określone w ASP.NET Core kontener IoC jako *przejściowy*).</span><span class="sxs-lookup"><span data-stu-id="33f95-155">A new instance per dependency (referred to in the ASP.NET Core IoC container as *transient*).</span></span>

- <span data-ttu-id="33f95-156">Pojedyncze wystąpienie współużytkowane przez wszystkie obiekty używające kontenera IoC (określane w kontenerze ASP.NET Core IoC jako *pojedyncze*).</span><span class="sxs-lookup"><span data-stu-id="33f95-156">A single instance shared across all objects using the IoC container (referred to in the ASP.NET Core IoC container as *singleton*).</span></span>

#### <a name="additional-resources"></a><span data-ttu-id="33f95-157">Zasoby dodatkowe</span><span class="sxs-lookup"><span data-stu-id="33f95-157">Additional resources</span></span>

- <span data-ttu-id="33f95-158">**Wprowadzenie do iniekcji zależności w ASP.NET Core** </span><span class="sxs-lookup"><span data-stu-id="33f95-158">**Introduction to Dependency Injection in ASP.NET Core** </span></span>\
  [https://docs.microsoft.com/aspnet/core/fundamentals/dependency-injection](/aspnet/core/fundamentals/dependency-injection)

- <span data-ttu-id="33f95-159">**Autofac.**</span><span class="sxs-lookup"><span data-stu-id="33f95-159">**Autofac.**</span></span> <span data-ttu-id="33f95-160">Oficjalna dokumentacja.</span><span class="sxs-lookup"><span data-stu-id="33f95-160">Official documentation.</span></span> \
  <https://docs.autofac.org/en/latest/>

- <span data-ttu-id="33f95-161">**Porównanie ASP.NET Core okresów istnienia usługi kontenera IoC z wystąpieniami Autofac IoC Container Scopes-Cesar de La Torre.**</span><span class="sxs-lookup"><span data-stu-id="33f95-161">**Comparing ASP.NET Core IoC container service lifetimes with Autofac IoC container instance scopes - Cesar de la Torre.**</span></span> \
  <https://devblogs.microsoft.com/cesardelatorre/comparing-asp-net-core-ioc-service-life-times-and-autofac-ioc-instance-scopes/>

## <a name="implement-the-command-and-command-handler-patterns"></a><span data-ttu-id="33f95-162">Implementowanie wzorców programu obsługi poleceń i poleceń</span><span class="sxs-lookup"><span data-stu-id="33f95-162">Implement the Command and Command Handler patterns</span></span>

<span data-ttu-id="33f95-163">W przykładzie między konstruktorem pokazanym w poprzedniej sekcji kontener IoC został wstrzykiwany przez Konstruktor w klasie.</span><span class="sxs-lookup"><span data-stu-id="33f95-163">In the DI-through-constructor example shown in the previous section, the IoC container was injecting repositories through a constructor in a class.</span></span> <span data-ttu-id="33f95-164">Ale dokładnie tam, gdzie zostały wprowadzone?</span><span class="sxs-lookup"><span data-stu-id="33f95-164">But exactly where were they injected?</span></span> <span data-ttu-id="33f95-165">W prostym interfejsie API sieci Web (na przykład mikrousługi w katalogu eShopOnContainers) można wstrzyknąć je na poziomie kontrolerów MVC, w konstruktorze kontrolera, w ramach potoku żądania ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="33f95-165">In a simple Web API (for example, the catalog microservice in eShopOnContainers), you inject them at the MVC controllers' level, in a controller constructor, as part of the request pipeline of ASP.NET Core.</span></span> <span data-ttu-id="33f95-166">Jednak w początkowym kodzie tej sekcji (Klasa [CreateOrderCommandHandler](https://github.com/dotnet-architecture/eShopOnContainers/blob/master/src/Services/Ordering/Ordering.API/Application/Commands/CreateOrderCommandHandler.cs) z usługi PORZĄDKOWANIA. API w eShopOnContainers), iniekcja zależności odbywa się za pośrednictwem konstruktora określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="33f95-166">However, in the initial code of this section (the [CreateOrderCommandHandler](https://github.com/dotnet-architecture/eShopOnContainers/blob/master/src/Services/Ordering/Ordering.API/Application/Commands/CreateOrderCommandHandler.cs) class from the Ordering.API service in eShopOnContainers), the injection of dependencies is done through the constructor of a particular command handler.</span></span> <span data-ttu-id="33f95-167">Przekaż nam wyjaśnienie, czym jest procedura obsługi poleceń i dlaczego warto z niej korzystać.</span><span class="sxs-lookup"><span data-stu-id="33f95-167">Let us explain what a command handler is and why you would want to use it.</span></span>

<span data-ttu-id="33f95-168">Wzorzec polecenia jest wewnętrznie związany ze wzorcem CQRS, który został wprowadzony wcześniej w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="33f95-168">The Command pattern is intrinsically related to the CQRS pattern that was introduced earlier in this guide.</span></span> <span data-ttu-id="33f95-169">CQRS ma dwie strony.</span><span class="sxs-lookup"><span data-stu-id="33f95-169">CQRS has two sides.</span></span> <span data-ttu-id="33f95-170">Pierwszy obszar jest kwerendami, przy użyciu uproszczonych zapytań z [Dapper](https://github.com/StackExchange/dapper-dot-net) Micro ORM, który został wcześniej wyjaśniony.</span><span class="sxs-lookup"><span data-stu-id="33f95-170">The first area is queries, using simplified queries with the [Dapper](https://github.com/StackExchange/dapper-dot-net) micro ORM, which was explained previously.</span></span> <span data-ttu-id="33f95-171">Drugi obszar to polecenia, które są punktem początkowym dla transakcji i kanałem wejściowym spoza usługi.</span><span class="sxs-lookup"><span data-stu-id="33f95-171">The second area is commands, which are the starting point for transactions, and the input channel from outside the service.</span></span>

<span data-ttu-id="33f95-172">Jak pokazano na rysunku 7-24, wzorzec opiera się na akceptowaniu poleceń po stronie klienta, przetwarzaniu ich na podstawie reguł modelu domeny, a wreszcie utrzymując Stany przy użyciu transakcji.</span><span class="sxs-lookup"><span data-stu-id="33f95-172">As shown in Figure 7-24, the pattern is based on accepting commands from the client-side, processing them based on the domain model rules, and finally persisting the states with transactions.</span></span>

![Diagram przedstawiający przepływ danych wysokiego poziomu z klienta do bazy danych programu.](./media/microservice-application-layer-implementation-web-api/high-level-writes-side.png)

<span data-ttu-id="33f95-174">**Rysunek 7-24**.</span><span class="sxs-lookup"><span data-stu-id="33f95-174">**Figure 7-24**.</span></span> <span data-ttu-id="33f95-175">Widok wysokiego poziomu poleceń lub "Strona transakcyjna" w wzorcu CQRS</span><span class="sxs-lookup"><span data-stu-id="33f95-175">High-level view of the commands or "transactional side" in a CQRS pattern</span></span>

<span data-ttu-id="33f95-176">Rysunek 7-24 pokazuje, że aplikacja interfejsu użytkownika wysyła polecenie za pomocą interfejsu API, który jest `CommandHandler` zależny od modelu domeny i infrastruktury, aby zaktualizować bazę danych.</span><span class="sxs-lookup"><span data-stu-id="33f95-176">Figure 7-24 shows that the UI app sends a command through the API that gets to a `CommandHandler`, that depends on the Domain model and the Infrastructure, to update the database.</span></span>

### <a name="the-command-class"></a><span data-ttu-id="33f95-177">Klasa polecenia</span><span class="sxs-lookup"><span data-stu-id="33f95-177">The command class</span></span>

<span data-ttu-id="33f95-178">Polecenie to żądanie systemu do wykonania akcji, która zmienia stan systemu.</span><span class="sxs-lookup"><span data-stu-id="33f95-178">A command is a request for the system to perform an action that changes the state of the system.</span></span> <span data-ttu-id="33f95-179">Polecenia są bezwzględnie i powinny być przetwarzane tylko raz.</span><span class="sxs-lookup"><span data-stu-id="33f95-179">Commands are imperative, and should be processed just once.</span></span>

<span data-ttu-id="33f95-180">Ponieważ polecenia są bezwzględne, zazwyczaj nazywa się czasownikiem w bezwzględnym nastroju (na przykład "Create" lub "Update") i mogą zawierać typ agregacji, na przykład CreateOrderCommand.</span><span class="sxs-lookup"><span data-stu-id="33f95-180">Since commands are imperatives, they are typically named with a verb in the imperative mood (for example, "create" or "update"), and they might include the aggregate type, such as CreateOrderCommand.</span></span> <span data-ttu-id="33f95-181">W przeciwieństwie do zdarzenia, polecenie nie jest faktem z przeszłości; jest to tylko żądanie i dlatego może zostać odrzucone.</span><span class="sxs-lookup"><span data-stu-id="33f95-181">Unlike an event, a command is not a fact from the past; it is only a request, and thus may be refused.</span></span>

<span data-ttu-id="33f95-182">Polecenia mogą pochodzić z interfejsu użytkownika w wyniku użytkownika inicjującego żądanie lub z Menedżera procesów, gdy Menedżer procesów kieruje wartość zagregowaną w celu wykonania akcji.</span><span class="sxs-lookup"><span data-stu-id="33f95-182">Commands can originate from the UI as a result of a user initiating a request, or from a process manager when the process manager is directing an aggregate to perform an action.</span></span>

<span data-ttu-id="33f95-183">Ważną cechą polecenia jest to, że należy je przetworzyć tylko raz przez jednego odbiorcę.</span><span class="sxs-lookup"><span data-stu-id="33f95-183">An important characteristic of a command is that it should be processed just once by a single receiver.</span></span> <span data-ttu-id="33f95-184">Wynika to z tego, że polecenie jest pojedynczą akcją lub transakcją, którą chcesz wykonać w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="33f95-184">This is because a command is a single action or transaction you want to perform in the application.</span></span> <span data-ttu-id="33f95-185">Na przykład to samo polecenie tworzenia kolejności nie powinno być przetwarzane więcej niż raz.</span><span class="sxs-lookup"><span data-stu-id="33f95-185">For example, the same order creation command should not be processed more than once.</span></span> <span data-ttu-id="33f95-186">Jest to ważna różnica między poleceniami i zdarzeniami.</span><span class="sxs-lookup"><span data-stu-id="33f95-186">This is an important difference between commands and events.</span></span> <span data-ttu-id="33f95-187">Zdarzenia mogą być przetwarzane wiele razy, ponieważ wiele systemów lub mikrousług może być zainteresowanych wydarzeniem.</span><span class="sxs-lookup"><span data-stu-id="33f95-187">Events may be processed multiple times, because many systems or microservices might be interested in the event.</span></span>

<span data-ttu-id="33f95-188">Ponadto ważne jest, aby polecenie było przetwarzane tylko raz w przypadku, gdy polecenie nie jest idempotentne.</span><span class="sxs-lookup"><span data-stu-id="33f95-188">In addition, it is important that a command be processed only once in case the command is not idempotent.</span></span> <span data-ttu-id="33f95-189">Polecenie jest idempotentne, jeśli może być wykonywane wiele razy bez zmiany wyniku, ze względu na charakter polecenia lub w sposób, w jaki system obsługuje polecenie.</span><span class="sxs-lookup"><span data-stu-id="33f95-189">A command is idempotent if it can be executed multiple times without changing the result, either because of the nature of the command, or because of the way the system handles the command.</span></span>

<span data-ttu-id="33f95-190">Dobrym rozwiązaniem jest udostępnienie poleceń i aktualizacji idempotentne, gdy jest to zrozumiałe dla reguł firmy i niezwiązanych z tą domeną.</span><span class="sxs-lookup"><span data-stu-id="33f95-190">It is a good practice to make your commands and updates idempotent when it makes sense under your domain's business rules and invariants.</span></span> <span data-ttu-id="33f95-191">Na przykład, aby użyć tego samego przykładu, jeśli z jakiegoś powodu (logika ponawiania, działanie hakerskie itp.) to samo polecenie "zbyt Order" dotrze do systemu, powinno być możliwe jego zidentyfikowanie i upewnienie się, że nie utworzysz wielu zamówień.</span><span class="sxs-lookup"><span data-stu-id="33f95-191">For instance, to use the same example, if for any reason (retry logic, hacking, etc.) the same CreateOrder command reaches your system multiple times, you should be able to identify it and ensure that you do not create multiple orders.</span></span> <span data-ttu-id="33f95-192">Aby to zrobić, należy dołączyć rodzaj tożsamości w operacjach i określić, czy polecenie lub aktualizacja zostały już przetworzone.</span><span class="sxs-lookup"><span data-stu-id="33f95-192">To do so, you need to attach some kind of identity in the operations and identify whether the command or update was already processed.</span></span>

<span data-ttu-id="33f95-193">Wysyłasz polecenie do pojedynczego odbiorcy; nie publikujesz polecenia.</span><span class="sxs-lookup"><span data-stu-id="33f95-193">You send a command to a single receiver; you do not publish a command.</span></span> <span data-ttu-id="33f95-194">Publikowanie jest dla zdarzeń, które określają fakt, że coś się stało i mogą być interesujące dla odbiorców zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="33f95-194">Publishing is for events that state a fact—that something has happened and might be interesting for event receivers.</span></span> <span data-ttu-id="33f95-195">W przypadku zdarzeń Wydawca nie ma obaw dotyczących tego, które osoby odbierające uzyskują wydarzenie lub co robią.</span><span class="sxs-lookup"><span data-stu-id="33f95-195">In the case of events, the publisher has no concerns about which receivers get the event or what they do it.</span></span> <span data-ttu-id="33f95-196">Ale zdarzenia związane z domeną lub integracją to różne historie już wprowadzone w poprzednich sekcjach.</span><span class="sxs-lookup"><span data-stu-id="33f95-196">But domain or integration events are a different story already introduced in previous sections.</span></span>

<span data-ttu-id="33f95-197">Polecenie jest implementowane z klasą zawierającą pola danych lub kolekcje ze wszystkimi informacjami, które są konieczne, aby można było wykonać to polecenie.</span><span class="sxs-lookup"><span data-stu-id="33f95-197">A command is implemented with a class that contains data fields or collections with all the information that is needed in order to execute that command.</span></span> <span data-ttu-id="33f95-198">Polecenie jest specjalnym rodzajem obiektu Transfer danych (DTO), który jest specjalnie używany do żądania zmian lub transakcji.</span><span class="sxs-lookup"><span data-stu-id="33f95-198">A command is a special kind of Data Transfer Object (DTO), one that is specifically used to request changes or transactions.</span></span> <span data-ttu-id="33f95-199">Samo polecenie jest zależne od informacji, które są zbędne do przetwarzania polecenia i nic nie rób.</span><span class="sxs-lookup"><span data-stu-id="33f95-199">The command itself is based on exactly the information that is needed for processing the command, and nothing more.</span></span>

<span data-ttu-id="33f95-200">W poniższym przykładzie pokazano klasę uproszczoną `CreateOrderCommand` .</span><span class="sxs-lookup"><span data-stu-id="33f95-200">The following example shows the simplified `CreateOrderCommand` class.</span></span> <span data-ttu-id="33f95-201">Jest to niezmienne polecenie, które jest używane w mikrousłudze porządkowania w eShopOnContainers.</span><span class="sxs-lookup"><span data-stu-id="33f95-201">This is an immutable command that is used in the ordering microservice in eShopOnContainers.</span></span>

```csharp
// DDD and CQRS patterns comment: Note that it is recommended to implement immutable Commands
// In this case, its immutability is achieved by having all the setters as private
// plus only being able to update the data just once, when creating the object through its constructor.
// References on Immutable Commands:
// http://cqrs.nu/Faq
// https://docs.spine3.org/motivation/immutability.html
// http://blog.gauffin.org/2012/06/griffin-container-introducing-command-support/
// https://docs.microsoft.com/dotnet/csharp/programming-guide/classes-and-structs/how-to-implement-a-lightweight-class-with-auto-implemented-properties

[DataContract]
public class CreateOrderCommand
    : IRequest<bool>
{
    [DataMember]
    private readonly List<OrderItemDTO> _orderItems;

    [DataMember]
    public string UserId { get; private set; }

    [DataMember]
    public string UserName { get; private set; }

    [DataMember]
    public string City { get; private set; }

    [DataMember]
    public string Street { get; private set; }

    [DataMember]
    public string State { get; private set; }

    [DataMember]
    public string Country { get; private set; }

    [DataMember]
    public string ZipCode { get; private set; }

    [DataMember]
    public string CardNumber { get; private set; }

    [DataMember]
    public string CardHolderName { get; private set; }

    [DataMember]
    public DateTime CardExpiration { get; private set; }

    [DataMember]
    public string CardSecurityNumber { get; private set; }

    [DataMember]
    public int CardTypeId { get; private set; }

    [DataMember]
    public IEnumerable<OrderItemDTO> OrderItems => _orderItems;

    public CreateOrderCommand()
    {
        _orderItems = new List<OrderItemDTO>();
    }

    public CreateOrderCommand(List<BasketItem> basketItems, string userId, string userName, string city, string street, string state, string country, string zipcode,
        string cardNumber, string cardHolderName, DateTime cardExpiration,
        string cardSecurityNumber, int cardTypeId) : this()
    {
        _orderItems = basketItems.ToOrderItemsDTO().ToList();
        UserId = userId;
        UserName = userName;
        City = city;
        Street = street;
        State = state;
        Country = country;
        ZipCode = zipcode;
        CardNumber = cardNumber;
        CardHolderName = cardHolderName;
        CardExpiration = cardExpiration;
        CardSecurityNumber = cardSecurityNumber;
        CardTypeId = cardTypeId;
        CardExpiration = cardExpiration;
    }


    public class OrderItemDTO
    {
        public int ProductId { get; set; }

        public string ProductName { get; set; }

        public decimal UnitPrice { get; set; }

        public decimal Discount { get; set; }

        public int Units { get; set; }

        public string PictureUrl { get; set; }
    }
}
```

<span data-ttu-id="33f95-202">Zasadniczo Klasa Command zawiera wszystkie dane potrzebne do wykonania transakcji biznesowej przy użyciu obiektów modelu domeny.</span><span class="sxs-lookup"><span data-stu-id="33f95-202">Basically, the command class contains all the data you need for performing a business transaction by using the domain model objects.</span></span> <span data-ttu-id="33f95-203">W ten sposób polecenia są po prostu strukturą danych, która zawiera dane tylko do odczytu, i bez zachowania.</span><span class="sxs-lookup"><span data-stu-id="33f95-203">Thus, commands are simply data structures that contain read-only data, and no behavior.</span></span> <span data-ttu-id="33f95-204">Nazwa polecenia wskazuje jego przeznaczenie.</span><span class="sxs-lookup"><span data-stu-id="33f95-204">The command's name indicates its purpose.</span></span> <span data-ttu-id="33f95-205">W wielu językach, takich jak C#, polecenia są reprezentowane jako klasy, ale nie są to klasy prawdziwe w rzeczywistości zorientowane obiektowo.</span><span class="sxs-lookup"><span data-stu-id="33f95-205">In many languages like C#, commands are represented as classes, but they are not true classes in the real object-oriented sense.</span></span>

<span data-ttu-id="33f95-206">Jako dodatkową cechą polecenia są niezmienne, ponieważ oczekiwane użycie polega na tym, że są przetwarzane bezpośrednio przez model domeny.</span><span class="sxs-lookup"><span data-stu-id="33f95-206">As an additional characteristic, commands are immutable, because the expected usage is that they are processed directly by the domain model.</span></span> <span data-ttu-id="33f95-207">Nie trzeba zmieniać ich w przewidywanym okresie istnienia.</span><span class="sxs-lookup"><span data-stu-id="33f95-207">They do not need to change during their projected lifetime.</span></span> <span data-ttu-id="33f95-208">W klasie języka C# niezmienności można osiągnąć, nie ma żadnych metod ustawiających ani inne metody, które zmieniają stan wewnętrzny.</span><span class="sxs-lookup"><span data-stu-id="33f95-208">In a C# class, immutability can be achieved by not having any setters or other methods that change the internal state.</span></span>

<span data-ttu-id="33f95-209">Należy pamiętać, że jeśli planujesz lub oczekujesz, że polecenia przechodzą przez proces serializacji/deserializacji, właściwości muszą mieć prywatną metodę ustawiającą oraz `[DataMember]` atrybut (lub `[JsonProperty]` ).</span><span class="sxs-lookup"><span data-stu-id="33f95-209">Keep in mind that if you intend or expect commands to go through a serializing/deserializing process, the properties must have a private setter, and the `[DataMember]` (or `[JsonProperty]`) attribute.</span></span> <span data-ttu-id="33f95-210">W przeciwnym razie Deserializator nie będzie w stanie odtworzyć obiektu w miejscu docelowym przy użyciu wymaganych wartości.</span><span class="sxs-lookup"><span data-stu-id="33f95-210">Otherwise, the deserializer won't be able to reconstruct the object at the destination with the required values.</span></span> <span data-ttu-id="33f95-211">Można również użyć prawdziwie właściwości tylko do odczytu, jeśli klasa ma konstruktora z parametrami dla wszystkich właściwości, z normalną konwencją nazewnictwa camelCase, i dodając adnotację do konstruktora jako `[JsonConstructor]` .</span><span class="sxs-lookup"><span data-stu-id="33f95-211">You can also use truly read-only properties if the class has a constructor with parameters for all properties, with the usual camelCase naming convention, and annotate the constructor as `[JsonConstructor]`.</span></span> <span data-ttu-id="33f95-212">Jednak ta opcja wymaga więcej kodu.</span><span class="sxs-lookup"><span data-stu-id="33f95-212">However, this option requires more code.</span></span>

<span data-ttu-id="33f95-213">Na przykład Klasa poleceń do tworzenia zamówienia jest prawdopodobnie podobna pod względem danych do zamówienia, które chcesz utworzyć, ale prawdopodobnie nie potrzebujesz tych samych atrybutów.</span><span class="sxs-lookup"><span data-stu-id="33f95-213">For example, the command class for creating an order is probably similar in terms of data to the order you want to create, but you probably do not need the same attributes.</span></span> <span data-ttu-id="33f95-214">Na przykład nie `CreateOrderCommand` ma identyfikatora zamówienia, ponieważ zamówienie nie zostało jeszcze utworzone.</span><span class="sxs-lookup"><span data-stu-id="33f95-214">For instance, `CreateOrderCommand` does not have an order ID, because the order has not been created yet.</span></span>

<span data-ttu-id="33f95-215">Wiele klas poleceń może być proste, wymagając tylko kilku pól, które wymagają zmiany.</span><span class="sxs-lookup"><span data-stu-id="33f95-215">Many command classes can be simple, requiring only a few fields about some state that needs to be changed.</span></span> <span data-ttu-id="33f95-216">W przypadku zmiany stanu zamówienia z "w toku" na "płatne" lub "wysłane" przy użyciu polecenia podobnego do poniższego:</span><span class="sxs-lookup"><span data-stu-id="33f95-216">That would be the case if you are just changing the status of an order from "in process" to "paid" or "shipped" by using a command similar to the following:</span></span>

```csharp
[DataContract]
public class UpdateOrderStatusCommand
    :IRequest<bool>
{
    [DataMember]
    public string Status { get; private set; }

    [DataMember]
    public string OrderId { get; private set; }

    [DataMember]
    public string BuyerIdentityGuid { get; private set; }
}
```

<span data-ttu-id="33f95-217">Niektórzy deweloperzy sprawiają, że obiekty żądania interfejsu użytkownika są oddzielone od ich DTO poleceń, ale jest to tylko preferencja.</span><span class="sxs-lookup"><span data-stu-id="33f95-217">Some developers make their UI request objects separate from their command DTOs, but that is just a matter of preference.</span></span> <span data-ttu-id="33f95-218">Jest to żmudnyma separacja z nieznacznie większą wartością, a obiekty są niemal dokładnie takie same.</span><span class="sxs-lookup"><span data-stu-id="33f95-218">It is a tedious separation with not much additional value, and the objects are almost exactly the same shape.</span></span> <span data-ttu-id="33f95-219">Na przykład w eShopOnContainers niektóre polecenia są dostępne bezpośrednio po stronie klienta.</span><span class="sxs-lookup"><span data-stu-id="33f95-219">For instance, in eShopOnContainers, some commands come directly from the client-side.</span></span>

### <a name="the-command-handler-class"></a><span data-ttu-id="33f95-220">Klasa procedury obsługi poleceń</span><span class="sxs-lookup"><span data-stu-id="33f95-220">The Command handler class</span></span>

<span data-ttu-id="33f95-221">Należy zaimplementować konkretną klasę programu obsługi poleceń dla każdego polecenia.</span><span class="sxs-lookup"><span data-stu-id="33f95-221">You should implement a specific command handler class for each command.</span></span> <span data-ttu-id="33f95-222">To w jaki sposób działa wzorzec oraz miejsce użycia obiektu polecenia, obiektów domeny i obiektów repozytorium infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="33f95-222">That is how the pattern works, and it's where you'll use the command object, the domain objects, and the infrastructure repository objects.</span></span> <span data-ttu-id="33f95-223">Program obsługi poleceń jest w rzeczywistości sercem warstwy aplikacji pod kątem CQRS i DDD.</span><span class="sxs-lookup"><span data-stu-id="33f95-223">The command handler is in fact the heart of the application layer in terms of CQRS and DDD.</span></span> <span data-ttu-id="33f95-224">Jednak cała Logika domeny powinna być zawarta w klasach domeny — w ramach agregacji głównych (jednostek głównych), jednostek podrzędnych lub [usług domenowych](https://lostechies.com/jimmybogard/2008/08/21/services-in-domain-driven-design/), ale nie w ramach procedury obsługi poleceń, która jest klasą z warstwy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="33f95-224">However, all the domain logic should be contained in the domain classes—within the aggregate roots (root entities), child entities, or [domain services](https://lostechies.com/jimmybogard/2008/08/21/services-in-domain-driven-design/), but not within the command handler, which is a class from the application layer.</span></span>

<span data-ttu-id="33f95-225">Klasa procedury obsługi poleceń oferuje silny punkt taktowania w celu osiągnięcia jednej zasady odpowiedzialności (SRP) wymienionej w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="33f95-225">The command handler class offers a strong stepping stone in the way to achieve the Single Responsibility Principle (SRP) mentioned in a previous section.</span></span>

<span data-ttu-id="33f95-226">Procedura obsługi poleceń odbiera polecenie i uzyskuje wynik z używanej wartości zagregowanej.</span><span class="sxs-lookup"><span data-stu-id="33f95-226">A command handler receives a command and obtains a result from the aggregate that is used.</span></span> <span data-ttu-id="33f95-227">Wynikiem może być pomyślne wykonanie polecenia lub wyjątek.</span><span class="sxs-lookup"><span data-stu-id="33f95-227">The result should be either successful execution of the command, or an exception.</span></span> <span data-ttu-id="33f95-228">W przypadku wyjątku, stan systemu powinien być niezmieniony.</span><span class="sxs-lookup"><span data-stu-id="33f95-228">In the case of an exception, the system state should be unchanged.</span></span>

<span data-ttu-id="33f95-229">Procedura obsługi poleceń zazwyczaj wykonuje następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="33f95-229">The command handler usually takes the following steps:</span></span>

- <span data-ttu-id="33f95-230">Odbierze obiekt polecenia, taki jak DTO (z [mediator](https://en.wikipedia.org/wiki/Mediator_pattern) lub innego obiektu infrastruktury).</span><span class="sxs-lookup"><span data-stu-id="33f95-230">It receives the command object, like a DTO (from the [mediator](https://en.wikipedia.org/wiki/Mediator_pattern) or other infrastructure object).</span></span>

- <span data-ttu-id="33f95-231">Sprawdza, czy polecenie jest prawidłowe (jeśli nie jest zweryfikowane przez mediator).</span><span class="sxs-lookup"><span data-stu-id="33f95-231">It validates that the command is valid (if not validated by the mediator).</span></span>

- <span data-ttu-id="33f95-232">Tworzy wystąpienie zagregowanego wystąpienia agregacji, które jest elementem docelowym bieżącego polecenia.</span><span class="sxs-lookup"><span data-stu-id="33f95-232">It instantiates the aggregate root instance that is the target of the current command.</span></span>

- <span data-ttu-id="33f95-233">Wykonuje metodę w wystąpieniu agregacji głównej, pobierając wymagane dane z polecenia.</span><span class="sxs-lookup"><span data-stu-id="33f95-233">It executes the method on the aggregate root instance, getting the required data from the command.</span></span>

- <span data-ttu-id="33f95-234">Zachowuje nowy stan agregacji w powiązanej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="33f95-234">It persists the new state of the aggregate to its related database.</span></span> <span data-ttu-id="33f95-235">Ta ostatnia operacja to rzeczywista transakcja.</span><span class="sxs-lookup"><span data-stu-id="33f95-235">This last operation is the actual transaction.</span></span>

<span data-ttu-id="33f95-236">Zazwyczaj procedura obsługi poleceń zajmuje się pojedynczym agregowaniem, który jest oparty na jego zagregowanym elemencie głównym (jednostki głównej).</span><span class="sxs-lookup"><span data-stu-id="33f95-236">Typically, a command handler deals with a single aggregate driven by its aggregate root (root entity).</span></span> <span data-ttu-id="33f95-237">Jeśli odbiór jednego polecenia ma wpływ na wiele agregacji, można użyć zdarzeń domeny do propagowania stanów lub akcji w wielu agregacjach.</span><span class="sxs-lookup"><span data-stu-id="33f95-237">If multiple aggregates should be impacted by the reception of a single command, you could use domain events to propagate states or actions across multiple aggregates.</span></span>

<span data-ttu-id="33f95-238">Ważnym punktem jest to, że podczas przetwarzania polecenia Cała logika domeny powinna znajdować się wewnątrz modelu domeny (Agregaty), w pełni hermetyzowane i gotowe do testowania jednostkowego.</span><span class="sxs-lookup"><span data-stu-id="33f95-238">The important point here is that when a command is being processed, all the domain logic should be inside the domain model (the aggregates), fully encapsulated and ready for unit testing.</span></span> <span data-ttu-id="33f95-239">Procedura obsługi poleceń działa jako sposób uzyskania modelu domeny z bazy danych i jako ostatni krok, aby określić warstwę infrastruktury (repozytoria), aby zachować zmiany, gdy model zostanie zmieniony.</span><span class="sxs-lookup"><span data-stu-id="33f95-239">The command handler just acts as a way to get the domain model from the database, and as the final step, to tell the infrastructure layer (repositories) to persist the changes when the model is changed.</span></span> <span data-ttu-id="33f95-240">Zaletą tego podejścia jest możliwość refaktoryzacji logiki domeny w odizolowanym, w pełni wbudowanym, rozbudowanym modelu domeny bez zmiany kodu w warstwach aplikacji lub infrastruktury, które są poziomem instalacji (programy obsługi poleceń, internetowy interfejs API, repozytoria itp.).</span><span class="sxs-lookup"><span data-stu-id="33f95-240">The advantage of this approach is that you can refactor the domain logic in an isolated, fully encapsulated, rich, behavioral domain model without changing code in the application or infrastructure layers, which are the plumbing level (command handlers, Web API, repositories, etc.).</span></span>

<span data-ttu-id="33f95-241">Gdy programy obsługi poleceń są złożone z zbyt dużą ilością logiki, która może być zapachem kodu.</span><span class="sxs-lookup"><span data-stu-id="33f95-241">When command handlers get complex, with too much logic, that can be a code smell.</span></span> <span data-ttu-id="33f95-242">Zapoznaj się z nimi, a jeśli znajdziesz logikę domeny, Refaktoryzacja kodu, aby przenieść zachowanie domeny do metod obiektów domeny (agregacja elementu głównego i podrzędnego).</span><span class="sxs-lookup"><span data-stu-id="33f95-242">Review them, and if you find domain logic, refactor the code to move that domain behavior to the methods of the domain objects (the aggregate root and child entity).</span></span>

<span data-ttu-id="33f95-243">Przykładem klasy procedury obsługi poleceń Poniższy kod przedstawia tę samą `CreateOrderCommandHandler` klasę, która została wyświetlona na początku tego rozdziału.</span><span class="sxs-lookup"><span data-stu-id="33f95-243">As an example of a command handler class, the following code shows the same `CreateOrderCommandHandler` class that you saw at the beginning of this chapter.</span></span> <span data-ttu-id="33f95-244">W tym przypadku wyróżnia również metodę dojścia i operacje przy użyciu obiektów modelu domeny/agregacji.</span><span class="sxs-lookup"><span data-stu-id="33f95-244">In this case, it also highlights the Handle method and the operations with the domain model objects/aggregates.</span></span>

```csharp
public class CreateOrderCommandHandler
        : IRequestHandler<CreateOrderCommand, bool>
{
    private readonly IOrderRepository _orderRepository;
    private readonly IIdentityService _identityService;
    private readonly IMediator _mediator;
    private readonly IOrderingIntegrationEventService _orderingIntegrationEventService;
    private readonly ILogger<CreateOrderCommandHandler> _logger;

    // Using DI to inject infrastructure persistence Repositories
    public CreateOrderCommandHandler(IMediator mediator,
        IOrderingIntegrationEventService orderingIntegrationEventService,
        IOrderRepository orderRepository,
        IIdentityService identityService,
        ILogger<CreateOrderCommandHandler> logger)
    {
        _orderRepository = orderRepository ?? throw new ArgumentNullException(nameof(orderRepository));
        _identityService = identityService ?? throw new ArgumentNullException(nameof(identityService));
        _mediator = mediator ?? throw new ArgumentNullException(nameof(mediator));
        _orderingIntegrationEventService = orderingIntegrationEventService ?? throw new ArgumentNullException(nameof(orderingIntegrationEventService));
        _logger = logger ?? throw new ArgumentNullException(nameof(logger));
    }

    public async Task<bool> Handle(CreateOrderCommand message, CancellationToken cancellationToken)
    {
        // Add Integration event to clean the basket
        var orderStartedIntegrationEvent = new OrderStartedIntegrationEvent(message.UserId);
        await _orderingIntegrationEventService.AddAndSaveEventAsync(orderStartedIntegrationEvent);

        // Add/Update the Buyer AggregateRoot
        // DDD patterns comment: Add child entities and value-objects through the Order Aggregate-Root
        // methods and constructor so validations, invariants and business logic
        // make sure that consistency is preserved across the whole aggregate
        var address = new Address(message.Street, message.City, message.State, message.Country, message.ZipCode);
        var order = new Order(message.UserId, message.UserName, address, message.CardTypeId, message.CardNumber, message.CardSecurityNumber, message.CardHolderName, message.CardExpiration);

        foreach (var item in message.OrderItems)
        {
            order.AddOrderItem(item.ProductId, item.ProductName, item.UnitPrice, item.Discount, item.PictureUrl, item.Units);
        }

        _logger.LogInformation("----- Creating Order - Order: {@Order}", order);

        _orderRepository.Add(order);

        return await _orderRepository.UnitOfWork
            .SaveEntitiesAsync(cancellationToken);
    }
}
```

<span data-ttu-id="33f95-245">Są to dodatkowe kroki, które powinien wykonać procedura obsługi polecenia:</span><span class="sxs-lookup"><span data-stu-id="33f95-245">These are additional steps a command handler should take:</span></span>

- <span data-ttu-id="33f95-246">Użyj danych polecenia do działania z metodami i zachowaniem zagregowanego elementu.</span><span class="sxs-lookup"><span data-stu-id="33f95-246">Use the command's data to operate with the aggregate root's methods and behavior.</span></span>

- <span data-ttu-id="33f95-247">Wewnętrznie w obiektach domeny, należy podnieść zdarzenia domeny podczas wykonywania transakcji, ale jest to niewidoczne z punktu widzenia procedury obsługi polecenia.</span><span class="sxs-lookup"><span data-stu-id="33f95-247">Internally within the domain objects, raise domain events while the transaction is executed, but that is transparent from a command handler point of view.</span></span>

- <span data-ttu-id="33f95-248">Jeśli wynik operacji agregacji zakończy się pomyślnie i po zakończeniu transakcji, zgłoś zdarzenia integracji.</span><span class="sxs-lookup"><span data-stu-id="33f95-248">If the aggregate's operation result is successful and after the transaction is finished, raise integration events.</span></span> <span data-ttu-id="33f95-249">(Mogą one być również zgłaszane przez klasy infrastruktury, takie jak repozytoria).</span><span class="sxs-lookup"><span data-stu-id="33f95-249">(These might also be raised by infrastructure classes like repositories.)</span></span>

#### <a name="additional-resources"></a><span data-ttu-id="33f95-250">Zasoby dodatkowe</span><span class="sxs-lookup"><span data-stu-id="33f95-250">Additional resources</span></span>

- <span data-ttu-id="33f95-251">**Oznacz Seemann. W granicach aplikacje nie są zorientowane obiektowo** </span><span class="sxs-lookup"><span data-stu-id="33f95-251">**Mark Seemann. At the Boundaries, Applications are Not Object-Oriented** </span></span>\
  <https://blog.ploeh.dk/2011/05/31/AttheBoundaries,ApplicationsareNotObject-Oriented/>

- <span data-ttu-id="33f95-252">**Polecenia i zdarzenia** </span><span class="sxs-lookup"><span data-stu-id="33f95-252">**Commands and events** </span></span>\
  <https://cqrs.nu/Faq/commands-and-events>

- <span data-ttu-id="33f95-253">**Do czego służy procedura obsługi poleceń?**</span><span class="sxs-lookup"><span data-stu-id="33f95-253">**What does a command handler do?**</span></span> \
  <https://cqrs.nu/Faq/command-handlers>

- <span data-ttu-id="33f95-254">**Jimmy Bogard. Wzorce poleceń domeny — programy obsługi** </span><span class="sxs-lookup"><span data-stu-id="33f95-254">**Jimmy Bogard. Domain Command Patterns – Handlers** </span></span>\
  <https://jimmybogard.com/domain-command-patterns-handlers/>

- <span data-ttu-id="33f95-255">**Jimmy Bogard. Wzorce poleceń domeny — Walidacja** </span><span class="sxs-lookup"><span data-stu-id="33f95-255">**Jimmy Bogard. Domain Command Patterns – Validation** </span></span>\
  <https://jimmybogard.com/domain-command-patterns-validation/>

## <a name="the-command-process-pipeline-how-to-trigger-a-command-handler"></a><span data-ttu-id="33f95-256">Potok procesu polecenia: jak wyzwolić procedurę obsługi polecenia</span><span class="sxs-lookup"><span data-stu-id="33f95-256">The Command process pipeline: how to trigger a command handler</span></span>

<span data-ttu-id="33f95-257">Następnym pytaniem jest wywołanie procedury obsługi polecenia.</span><span class="sxs-lookup"><span data-stu-id="33f95-257">The next question is how to invoke a command handler.</span></span> <span data-ttu-id="33f95-258">Można go ręcznie wywołać z każdego powiązanego kontrolera ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="33f95-258">You could manually call it from each related ASP.NET Core controller.</span></span> <span data-ttu-id="33f95-259">Jednak takie podejście byłoby zbyt sprzężone i nie jest idealnym rozwiązaniem.</span><span class="sxs-lookup"><span data-stu-id="33f95-259">However, that approach would be too coupled and is not ideal.</span></span>

<span data-ttu-id="33f95-260">Pozostałe dwie główne opcje, które są zalecanymi opcjami, to:</span><span class="sxs-lookup"><span data-stu-id="33f95-260">The other two main options, which are the recommended options, are:</span></span>

- <span data-ttu-id="33f95-261">Za poorednictwem artefaktu wzorca mediator w pamięci.</span><span class="sxs-lookup"><span data-stu-id="33f95-261">Through an in-memory Mediator pattern artifact.</span></span>

- <span data-ttu-id="33f95-262">Z asynchronicznej kolejki komunikatów, między kontrolerami i obsługą.</span><span class="sxs-lookup"><span data-stu-id="33f95-262">With an asynchronous message queue, in between controllers and handlers.</span></span>

### <a name="use-the-mediator-pattern-in-memory-in-the-command-pipeline"></a><span data-ttu-id="33f95-263">Używanie wzorca mediator (w pamięci) w potoku poleceń</span><span class="sxs-lookup"><span data-stu-id="33f95-263">Use the Mediator pattern (in-memory) in the command pipeline</span></span>

<span data-ttu-id="33f95-264">Jak pokazano na rysunku 7-25, w podejściu CQRS można użyć inteligentnego mediator, podobnego do magistrali w pamięci, która jest wystarczająco inteligentna, aby przekierować do prawej obsługi poleceń na podstawie typu polecenia lub DTO.</span><span class="sxs-lookup"><span data-stu-id="33f95-264">As shown in Figure 7-25, in a CQRS approach you use an intelligent mediator, similar to an in-memory bus, which is smart enough to redirect to the right command handler based on the type of the command or DTO being received.</span></span> <span data-ttu-id="33f95-265">Pojedyncze czarne strzałki między składnikami reprezentują zależności między obiektami (w wielu przypadkach, które są wprowadzane przez DI) wraz z ich powiązaniami.</span><span class="sxs-lookup"><span data-stu-id="33f95-265">The single black arrows between components represent the dependencies between objects (in many cases, injected through DI) with their related interactions.</span></span>

![Diagram przedstawiający bardziej szczegółowy przepływ danych z klienta do bazy danych.](./media/microservice-application-layer-implementation-web-api/mediator-cqrs-microservice.png)

<span data-ttu-id="33f95-267">**Rysunek 7-25**.</span><span class="sxs-lookup"><span data-stu-id="33f95-267">**Figure 7-25**.</span></span> <span data-ttu-id="33f95-268">Używanie wzorca mediator w procesie w jednej mikrousłudze CQRS</span><span class="sxs-lookup"><span data-stu-id="33f95-268">Using the Mediator pattern in process in a single CQRS microservice</span></span>

<span data-ttu-id="33f95-269">Na powyższym diagramie przedstawiono powiększenie z obrazu 7-24: kontroler ASP.NET Core wysyła polecenie do potoku poleceń MediatR, dzięki czemu uzyskuje się do odpowiedniej procedury obsługi.</span><span class="sxs-lookup"><span data-stu-id="33f95-269">The above diagram shows a zoom-in from image 7-24: the ASP.NET Core controller sends the command to MediatR's command pipeline, so they get to the appropriate handler.</span></span>

<span data-ttu-id="33f95-270">Przyczyną użycia wzorca mediator jest to, że w aplikacjach dla przedsiębiorstw żądania przetwarzania mogą być skomplikowane.</span><span class="sxs-lookup"><span data-stu-id="33f95-270">The reason that using the Mediator pattern makes sense is that in enterprise applications, the processing requests can get complicated.</span></span> <span data-ttu-id="33f95-271">Chcesz mieć możliwość dodawania otwartej liczby zagadnień związanych z wycinaniem, takich jak rejestrowanie, walidacje, Inspekcja i zabezpieczenia.</span><span class="sxs-lookup"><span data-stu-id="33f95-271">You want to be able to add an open number of cross-cutting concerns like logging, validations, audit, and security.</span></span> <span data-ttu-id="33f95-272">W takich przypadkach można polegać na potoku mediator (zobacz [wzorzec mediator](https://en.wikipedia.org/wiki/Mediator_pattern)), aby zapewnić możliwość wykonania tych dodatkowych zachowań lub obaw związanych z wycinaniem.</span><span class="sxs-lookup"><span data-stu-id="33f95-272">In these cases, you can rely on a mediator pipeline (see [Mediator pattern](https://en.wikipedia.org/wiki/Mediator_pattern)) to provide a means for these extra behaviors or cross-cutting concerns.</span></span>

<span data-ttu-id="33f95-273">Mediator to obiekt, który hermetyzuje "jak" tego procesu: koordynuje wykonywanie w oparciu o stan, sposób wywoływania obsługi poleceń lub ładunek, który jest udostępniany do obsługi.</span><span class="sxs-lookup"><span data-stu-id="33f95-273">A mediator is an object that encapsulates the "how" of this process: it coordinates execution based on state, the way a command handler is invoked, or the payload you provide to the handler.</span></span> <span data-ttu-id="33f95-274">Za pomocą składnika mediator można zastosować problemy z wycinaniem i w sposób przejrzysty, stosując dekoratory (lub [zachowania potoku](https://github.com/jbogard/MediatR/wiki/Behaviors) od [MediatR 3](https://www.nuget.org/packages/MediatR/3.0.0)).</span><span class="sxs-lookup"><span data-stu-id="33f95-274">With a mediator component, you can apply cross-cutting concerns in a centralized and transparent way by applying decorators (or [pipeline behaviors](https://github.com/jbogard/MediatR/wiki/Behaviors) since [MediatR 3](https://www.nuget.org/packages/MediatR/3.0.0)).</span></span> <span data-ttu-id="33f95-275">Aby uzyskać więcej informacji, zobacz [wzorzec dekoratora](https://en.wikipedia.org/wiki/Decorator_pattern).</span><span class="sxs-lookup"><span data-stu-id="33f95-275">For more information, see the [Decorator pattern](https://en.wikipedia.org/wiki/Decorator_pattern).</span></span>

<span data-ttu-id="33f95-276">Dekoratory i zachowania są podobne do [programowania zorientowanego na proporcje (AOP)](https://en.wikipedia.org/wiki/Aspect-oriented_programming), stosowane tylko do określonego potoku procesu zarządzanego przez składnik mediator.</span><span class="sxs-lookup"><span data-stu-id="33f95-276">Decorators and behaviors are similar to [Aspect Oriented Programming (AOP)](https://en.wikipedia.org/wiki/Aspect-oriented_programming), only applied to a specific process pipeline managed by the mediator component.</span></span> <span data-ttu-id="33f95-277">Aspekty w AOP, które implementują zagadnienia dotyczące krzyżowego stosowania, są stosowane na podstawie *splotów aspektów* wprowadzonych w czasie kompilacji lub w oparciu o przechwycenie wywołania obiektu.</span><span class="sxs-lookup"><span data-stu-id="33f95-277">Aspects in AOP that implement cross-cutting concerns are applied based on *aspect weavers* injected at compilation time or based on object call interception.</span></span> <span data-ttu-id="33f95-278">Obydwie typowe podejścia AOP są czasami nazywane "jak Magic", ponieważ nie jest to łatwe do sprawdzenia, jak AOP działa.</span><span class="sxs-lookup"><span data-stu-id="33f95-278">Both typical AOP approaches are sometimes said to work "like magic," because it is not easy to see how AOP does its work.</span></span> <span data-ttu-id="33f95-279">W przypadku poważnych problemów lub usterek AOP może być trudne do debugowania.</span><span class="sxs-lookup"><span data-stu-id="33f95-279">When dealing with serious issues or bugs, AOP can be difficult to debug.</span></span> <span data-ttu-id="33f95-280">Z drugiej strony te dekoratory/zachowania są jawne i stosowane tylko w kontekście mediator, dlatego debugowanie jest znacznie bardziej przewidywalne i łatwe.</span><span class="sxs-lookup"><span data-stu-id="33f95-280">On the other hand, these decorators/behaviors are explicit and applied only in the context of the mediator, so debugging is much more predictable and easy.</span></span>

<span data-ttu-id="33f95-281">Na przykład w mikrousłudze porządkowania eShopOnContainers ma implementację dwóch przykładowych zachowań, klasy [LogBehavior](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Behaviors/LoggingBehavior.cs) i klasy [ValidatorBehavior](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Behaviors/ValidatorBehavior.cs) .</span><span class="sxs-lookup"><span data-stu-id="33f95-281">For example, in the eShopOnContainers ordering microservice, has an implementation of two sample behaviors, a [LogBehavior](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Behaviors/LoggingBehavior.cs) class and a [ValidatorBehavior](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Behaviors/ValidatorBehavior.cs) class.</span></span> <span data-ttu-id="33f95-282">Implementacja zachowań została omówiona w następnej sekcji, pokazując sposób, w jaki eShopOnContainers używa zachowań [MediatR](https://www.nuget.org/packages/MediatR) [behaviors](https://github.com/jbogard/MediatR/wiki/Behaviors).</span><span class="sxs-lookup"><span data-stu-id="33f95-282">The implementation of the behaviors is explained in the next section by showing how eShopOnContainers uses [MediatR](https://www.nuget.org/packages/MediatR) [behaviors](https://github.com/jbogard/MediatR/wiki/Behaviors).</span></span>

### <a name="use-message-queues-out-of-proc-in-the-commands-pipeline"></a><span data-ttu-id="33f95-283">Używanie kolejek komunikatów (out-of-proc) w potoku polecenia</span><span class="sxs-lookup"><span data-stu-id="33f95-283">Use message queues (out-of-proc) in the command's pipeline</span></span>

<span data-ttu-id="33f95-284">Kolejną opcją jest użycie komunikatów asynchronicznych opartych na brokerach lub kolejkach komunikatów, jak pokazano na rysunku 7-26.</span><span class="sxs-lookup"><span data-stu-id="33f95-284">Another choice is to use asynchronous messages based on brokers or message queues, as shown in Figure 7-26.</span></span> <span data-ttu-id="33f95-285">Tę opcję można również połączyć ze składnikiem mediator bezpośrednio przed programem obsługi poleceń.</span><span class="sxs-lookup"><span data-stu-id="33f95-285">That option could also be combined with the mediator component right before the command handler.</span></span>

![Diagram przedstawiający przepływu danych przy użyciu kolejki komunikatów o dużej dostępności.](./media/microservice-application-layer-implementation-web-api/add-ha-message-queue.png)

<span data-ttu-id="33f95-287">**Rysunek 7-26**.</span><span class="sxs-lookup"><span data-stu-id="33f95-287">**Figure 7-26**.</span></span> <span data-ttu-id="33f95-288">Korzystanie z kolejek komunikatów (poza procesem i komunikacją między procesami) za pomocą poleceń CQRS</span><span class="sxs-lookup"><span data-stu-id="33f95-288">Using message queues (out of the process and inter-process communication) with CQRS commands</span></span>

<span data-ttu-id="33f95-289">Potok poleceń może być również obsługiwany przez kolejkę komunikatów o wysokiej dostępności w celu dostarczenia poleceń do odpowiedniej procedury obsługi.</span><span class="sxs-lookup"><span data-stu-id="33f95-289">Command's pipeline can also be handled by a high availability message queue to deliver the commands to the appropriate handler.</span></span> <span data-ttu-id="33f95-290">Użycie kolejek komunikatów do akceptowania poleceń może dodatkowo zawęzić potoku poleceń, ponieważ prawdopodobnie trzeba będzie podzielić potok na dwa procesy połączone za pośrednictwem zewnętrznej kolejki komunikatów.</span><span class="sxs-lookup"><span data-stu-id="33f95-290">Using message queues to accept the commands can further complicate your command's pipeline, because you will probably need to split the pipeline into two processes connected through the external message queue.</span></span> <span data-ttu-id="33f95-291">Nadal powinien być używany, jeśli trzeba zwiększyć skalowalność i wydajność na podstawie asynchronicznych komunikatów.</span><span class="sxs-lookup"><span data-stu-id="33f95-291">Still, it should be used if you need to have improved scalability and performance based on asynchronous messaging.</span></span> <span data-ttu-id="33f95-292">Należy wziąć pod uwagę, że w przypadku rysunku 7-26 kontroler po prostu przesyła komunikat polecenia do kolejki i zwraca.</span><span class="sxs-lookup"><span data-stu-id="33f95-292">Consider that in the case of Figure 7-26, the controller just posts the command message into the queue and returns.</span></span> <span data-ttu-id="33f95-293">Następnie programy obsługi poleceń przetwarzają komunikaty we własnym tempie.</span><span class="sxs-lookup"><span data-stu-id="33f95-293">Then the command handlers process the messages at their own pace.</span></span> <span data-ttu-id="33f95-294">Jest to świetna korzyść dla kolejek: Kolejka komunikatów może działać jako bufor w przypadkach, gdy wymagana jest skalowalność funkcji Hyper-, na przykład w przypadku zasobów lub dowolnego innego scenariusza z dużą ilością danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="33f95-294">That is a great benefit of queues: the message queue can act as a buffer in cases when hyper scalability is needed, such as for stocks or any other scenario with a high volume of ingress data.</span></span>

<span data-ttu-id="33f95-295">Jednak ze względu na asynchroniczny charakter kolejek komunikatów należy dowiedzieć się, jak komunikować się z aplikacją kliencką dotyczącą sukcesu lub niepowodzenia procesu polecenia.</span><span class="sxs-lookup"><span data-stu-id="33f95-295">However, because of the asynchronous nature of message queues, you need to figure out how to communicate with the client application about the success or failure of the command's process.</span></span> <span data-ttu-id="33f95-296">Jako regułę nie należy nigdy używać poleceń "Fire i zapomnij".</span><span class="sxs-lookup"><span data-stu-id="33f95-296">As a rule, you should never use "fire and forget" commands.</span></span> <span data-ttu-id="33f95-297">Każda aplikacja biznesowa musi wiedzieć, czy polecenie zostało przetworzone pomyślnie, czy co najmniej zweryfikowane i zaakceptowane.</span><span class="sxs-lookup"><span data-stu-id="33f95-297">Every business application needs to know if a command was processed successfully, or at least validated and accepted.</span></span>

<span data-ttu-id="33f95-298">W związku z tym, możliwość odpowiedzi na klienta po zweryfikowaniu komunikatu polecenia, który został przesłany do kolejki asynchronicznej, dodaje złożoność systemu w porównaniu do procesu polecenia w procesie, który zwraca wynik operacji po uruchomieniu transakcji.</span><span class="sxs-lookup"><span data-stu-id="33f95-298">Thus, being able to respond to the client after validating a command message that was submitted to an asynchronous queue adds complexity to your system, as compared to an in-process command process that returns the operation's result after running the transaction.</span></span> <span data-ttu-id="33f95-299">Korzystając z kolejek, może być konieczne zwrócenie wyniku procesu polecenia przez inne komunikaty wynikowe operacji, które będą wymagały dodatkowych składników i niestandardowej komunikacji w systemie.</span><span class="sxs-lookup"><span data-stu-id="33f95-299">Using queues, you might need to return the result of the command process through other operation result messages, which will require additional components and custom communication in your system.</span></span>

<span data-ttu-id="33f95-300">Ponadto polecenia asynchroniczne są poleceniami jednokierunkowymi, które w wielu przypadkach mogą nie być konieczne, jak wyjaśniono w następującej interesującej wymianie między Burtsev Alexey i Gregem młodych w [konwersacji online](https://groups.google.com/forum/#!msg/dddcqrs/xhJHVxDx2pM/WP9qP8ifYCwJ):</span><span class="sxs-lookup"><span data-stu-id="33f95-300">Additionally, async commands are one-way commands, which in many cases might not be needed, as is explained in the following interesting exchange between Burtsev Alexey and Greg Young in an [online conversation](https://groups.google.com/forum/#!msg/dddcqrs/xhJHVxDx2pM/WP9qP8ifYCwJ):</span></span>

> <span data-ttu-id="33f95-301">\[Burtsev Alexey \] mogę znaleźć wiele kodów, w których ludzie wykorzystują obsługę poleceń asynchronicznych lub jednokierunkową obsługę komunikatów z poleceniami bez żadnych powodów (nie wykonują długotrwałej operacji, nie wykonują zewnętrznych kodów asynchronicznych, ale nie wykonują nawet granicy między aplikacjami, aby korzystać z magistrali komunikatów).</span><span class="sxs-lookup"><span data-stu-id="33f95-301">\[Burtsev Alexey\] I find lots of code where people use async command handling or one-way command messaging without any reason to do so (they are not doing some long operation, they are not executing external async code, they do not even cross-application boundary to be using message bus).</span></span> <span data-ttu-id="33f95-302">Dlaczego wprowadzają tę niezbędną złożoność?</span><span class="sxs-lookup"><span data-stu-id="33f95-302">Why do they introduce this unnecessary complexity?</span></span> <span data-ttu-id="33f95-303">W rzeczywistości nie widzę przykładu kodu CQRS z programami obsługi poleceń blokujących do tej pory, chociaż będzie ona działać tylko w większości przypadków.</span><span class="sxs-lookup"><span data-stu-id="33f95-303">And actually, I haven't seen a CQRS code example with blocking command handlers so far, though it will work just fine in most cases.</span></span>
>
> <span data-ttu-id="33f95-304">\[Greg Young \] \[ ... \] polecenie asynchroniczne nie istnieje; jest to inne zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="33f95-304">\[Greg Young\] \[...\] an asynchronous command doesn't exist; it's actually another event.</span></span> <span data-ttu-id="33f95-305">Jeśli muszę zaakceptować to, co wysłałeś, i zgłosić wydarzenie, jeśli nie, już nie wiesz, jak to zrobić, to \[ nie jest polecenie \] .</span><span class="sxs-lookup"><span data-stu-id="33f95-305">If I must accept what you send me and raise an event if I disagree, it's no longer you telling me to do something \[that is, it's not a command\].</span></span> <span data-ttu-id="33f95-306">Poinformujemy Cię o tym, że coś zostało już zrobione.</span><span class="sxs-lookup"><span data-stu-id="33f95-306">It's you telling me something has been done.</span></span> <span data-ttu-id="33f95-307">Wydaje się to bardzo niewielką różnicą w pierwszej kolejności, ale ma wiele konsekwencji.</span><span class="sxs-lookup"><span data-stu-id="33f95-307">This seems like a slight difference at first, but it has many implications.</span></span>

<span data-ttu-id="33f95-308">Asynchroniczne polecenia znacznie zwiększają złożoność systemu, ponieważ nie ma prostego sposobu wskazywania niepowodzeń.</span><span class="sxs-lookup"><span data-stu-id="33f95-308">Asynchronous commands greatly increase the complexity of a system, because there is no simple way to indicate failures.</span></span> <span data-ttu-id="33f95-309">W związku z tym polecenia asynchroniczne nie są zalecane, niż w przypadku gdy wymagania dotyczące skalowania są wymagane lub w szczególnych przypadkach podczas komunikacji mikrousług wewnętrznych przy użyciu komunikatów.</span><span class="sxs-lookup"><span data-stu-id="33f95-309">Therefore, asynchronous commands are not recommended other than when scaling requirements are needed or in special cases when communicating the internal microservices through messaging.</span></span> <span data-ttu-id="33f95-310">W takich przypadkach należy zaprojektować oddzielny system raportowania i odzyskiwania pod kątem błędów.</span><span class="sxs-lookup"><span data-stu-id="33f95-310">In those cases, you must design a separate reporting and recovery system for failures.</span></span>

<span data-ttu-id="33f95-311">W początkowej wersji programu eShopOnContainers podjęto decyzję o użyciu przetwarzania polecenia synchronicznego, uruchomione z żądań HTTP i przez wzorzec mediator.</span><span class="sxs-lookup"><span data-stu-id="33f95-311">In the initial version of eShopOnContainers, it was decided to use synchronous command processing, started from HTTP requests and driven by the Mediator pattern.</span></span> <span data-ttu-id="33f95-312">Dzięki temu można łatwo zwrócić sukces lub niepowodzenie procesu, tak jak w implementacji [CreateOrderCommandHandler](https://github.com/dotnet-architecture/eShopOnContainers/blob/netcore1.1/src/Services/Ordering/Ordering.API/Application/Commands/CreateOrderCommandHandler.cs) .</span><span class="sxs-lookup"><span data-stu-id="33f95-312">That easily allows you to return the success or failure of the process, as in the [CreateOrderCommandHandler](https://github.com/dotnet-architecture/eShopOnContainers/blob/netcore1.1/src/Services/Ordering/Ordering.API/Application/Commands/CreateOrderCommandHandler.cs) implementation.</span></span>

<span data-ttu-id="33f95-313">W każdym przypadku powinna to być decyzja oparta na wymaganiach firmy aplikacji lub mikrousług.</span><span class="sxs-lookup"><span data-stu-id="33f95-313">In any case, this should be a decision based on your application's or microservice's business requirements.</span></span>

## <a name="implement-the-command-process-pipeline-with-a-mediator-pattern-mediatr"></a><span data-ttu-id="33f95-314">Implementowanie potoku procesu polecenia za pomocą wzorca mediator (MediatR)</span><span class="sxs-lookup"><span data-stu-id="33f95-314">Implement the command process pipeline with a mediator pattern (MediatR)</span></span>

<span data-ttu-id="33f95-315">W ramach przykładowej implementacji ten przewodnik proponuje użycie potoku w procesie opartym na wzorcu mediator w celu kierowania poleceń związanych z pozyskiwaniem poleceń i trasą w pamięci do odpowiednich programów obsługi poleceń.</span><span class="sxs-lookup"><span data-stu-id="33f95-315">As a sample implementation, this guide proposes using the in-process pipeline based on the Mediator pattern to drive command ingestion and route commands, in memory, to the right command handlers.</span></span> <span data-ttu-id="33f95-316">W przewodniku zawarto również zaproponować stosowanie [zachowań](https://github.com/jbogard/MediatR/wiki/Behaviors) w celu oddzielenia problemów związanych z rozcinaniem.</span><span class="sxs-lookup"><span data-stu-id="33f95-316">The guide also proposes applying [behaviors](https://github.com/jbogard/MediatR/wiki/Behaviors) in order to separate cross-cutting concerns.</span></span>

<span data-ttu-id="33f95-317">W przypadku implementacji w programie .NET Core istnieje wiele dostępnych bibliotek typu "open source", które implementują wzorzec mediator.</span><span class="sxs-lookup"><span data-stu-id="33f95-317">For implementation in .NET Core, there are multiple open-source libraries available that implement the Mediator pattern.</span></span> <span data-ttu-id="33f95-318">Biblioteka użyta w tym przewodniku jest biblioteką Open Source [MediatR](https://github.com/jbogard/MediatR) (utworzoną przez Jimmy Bogard), ale można użyć innej metody.</span><span class="sxs-lookup"><span data-stu-id="33f95-318">The library used in this guide is the [MediatR](https://github.com/jbogard/MediatR) open-source library (created by Jimmy Bogard), but you could use another approach.</span></span> <span data-ttu-id="33f95-319">MediatR to mała i prosta biblioteka, która umożliwia przetwarzanie komunikatów znajdujących się w pamięci, takich jak polecenie, podczas stosowania dekoratory lub zachowań.</span><span class="sxs-lookup"><span data-stu-id="33f95-319">MediatR is a small and simple library that allows you to process in-memory messages like a command, while applying decorators or behaviors.</span></span>

<span data-ttu-id="33f95-320">Użycie wzorca mediator pomaga zredukować sprzężenie i odizolować problemy związane z zażądaną pracy, podczas gdy automatycznie nawiązuje połączenie z programem obsługi, który wykonuje tę działania — w tym przypadku do obsługi poleceń.</span><span class="sxs-lookup"><span data-stu-id="33f95-320">Using the Mediator pattern helps you to reduce coupling and to isolate the concerns of the requested work, while automatically connecting to the handler that performs that work—in this case, to command handlers.</span></span>

<span data-ttu-id="33f95-321">Kolejną dobrą przyczyną użycia wzorca mediator został wyjaśniony przez Jimmy Bogard podczas przeglądania tego przewodnika:</span><span class="sxs-lookup"><span data-stu-id="33f95-321">Another good reason to use the Mediator pattern was explained by Jimmy Bogard when reviewing this guide:</span></span>

> <span data-ttu-id="33f95-322">Uważam, że w tym miejscu może być warto wspominać o testowaniu — zapewnia to spójne okno do zachowania systemu.</span><span class="sxs-lookup"><span data-stu-id="33f95-322">I think it might be worth mentioning testing here – it provides a nice consistent window into the behavior of your system.</span></span> <span data-ttu-id="33f95-323">Żądanie żądania. Wiemy, że aspekt jest całkiem cenny w tworzeniu spójnych testów.</span><span class="sxs-lookup"><span data-stu-id="33f95-323">Request-in, response-out. We've found that aspect quite valuable in building consistently behaving tests.</span></span>

<span data-ttu-id="33f95-324">Najpierw przyjrzyjmy się przykładowym kontrolerowi WebAPI, w którym faktycznie będzie używany obiekt mediator.</span><span class="sxs-lookup"><span data-stu-id="33f95-324">First, let's look at a sample WebAPI controller where you actually would use the mediator object.</span></span> <span data-ttu-id="33f95-325">Jeśli nie korzystasz z obiektu mediator, musisz wstrzyknąć wszystkie zależności dla tego kontrolera, takie jak obiekt rejestratora i inne.</span><span class="sxs-lookup"><span data-stu-id="33f95-325">If you weren't using the mediator object, you'd need to inject all the dependencies for that controller, things like a logger object and others.</span></span> <span data-ttu-id="33f95-326">W związku z tym Konstruktor zostałby skomplikowany.</span><span class="sxs-lookup"><span data-stu-id="33f95-326">Therefore, the constructor would be complicated.</span></span> <span data-ttu-id="33f95-327">Z drugiej strony, jeśli używasz obiektu mediator, Konstruktor kontrolera może być znacznie prostszy, z zaledwie kilkoma zależnościami, a nie z wieloma zależnościami, jeśli istniała jedna dla operacji wycinania, jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="33f95-327">On the other hand, if you use the mediator object, the constructor of your controller can be a lot simpler, with just a few dependencies instead of many dependencies if you had one per cross-cutting operation, as in the following example:</span></span>

```csharp
public class MyMicroserviceController : Controller
{
    public MyMicroserviceController(IMediator mediator,
                                    IMyMicroserviceQueries microserviceQueries)
    {
        // ...
    }
}
```

<span data-ttu-id="33f95-328">Można zobaczyć, że mediator zapewnia czysty i oszczędny Konstruktor kontrolera interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="33f95-328">You can see that the mediator provides a clean and lean Web API controller constructor.</span></span> <span data-ttu-id="33f95-329">Ponadto w ramach metod kontrolera kod wysyłający polecenie do obiektu mediator jest niemal jeden wiersz:</span><span class="sxs-lookup"><span data-stu-id="33f95-329">In addition, within the controller methods, the code to send a command to the mediator object is almost one line:</span></span>

```csharp
[Route("new")]
[HttpPost]
public async Task<IActionResult> ExecuteBusinessOperation([FromBody]RunOpCommand
                                                               runOperationCommand)
{
    var commandResult = await _mediator.SendAsync(runOperationCommand);

    return commandResult ? (IActionResult)Ok() : (IActionResult)BadRequest();
}
```

### <a name="implement-idempotent-commands"></a><span data-ttu-id="33f95-330">Implementowanie poleceń idempotentne</span><span class="sxs-lookup"><span data-stu-id="33f95-330">Implement idempotent Commands</span></span>

<span data-ttu-id="33f95-331">W **eShopOnContainers**, bardziej zaawansowany przykład niż powyżej, przesyła obiekt CreateOrderCommand z mikrousługi porządkowania.</span><span class="sxs-lookup"><span data-stu-id="33f95-331">In **eShopOnContainers**, a more advanced example than the above is submitting a CreateOrderCommand object from the Ordering microservice.</span></span> <span data-ttu-id="33f95-332">Jednak ponieważ proces biznesowy porządkowania jest nieco bardziej skomplikowany i, w naszym przypadku, faktycznie zaczyna się w mikrousłudze koszyka, ta akcja przesyłania obiektu CreateOrderCommand jest wykonywana z programu obsługi zdarzeń integracji o nazwie [UserCheckoutAcceptedIntegrationEventHandler](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/IntegrationEvents/EventHandling/UserCheckoutAcceptedIntegrationEventHandler.cs) zamiast prostego kontrolera WebAPI wywołana z poziomu aplikacji klienckiej, jak w poprzednim, prostszym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="33f95-332">But since the Ordering business process is a bit more complex and, in our case, it actually starts in the Basket microservice, this action of submitting the CreateOrderCommand object is performed from an integration-event handler named [UserCheckoutAcceptedIntegrationEventHandler](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/IntegrationEvents/EventHandling/UserCheckoutAcceptedIntegrationEventHandler.cs) instead of a simple WebAPI controller called from the client App as in the previous simpler example.</span></span>

<span data-ttu-id="33f95-333">Niemniej jednak akcja przesłania polecenia do MediatR jest bardzo podobna, jak pokazano w poniższym kodzie.</span><span class="sxs-lookup"><span data-stu-id="33f95-333">Nevertheless, the action of submitting the Command to MediatR is pretty similar, as shown in the following code.</span></span>

```csharp
var createOrderCommand = new CreateOrderCommand(eventMsg.Basket.Items,
                                                eventMsg.UserId, eventMsg.City,
                                                eventMsg.Street, eventMsg.State,
                                                eventMsg.Country, eventMsg.ZipCode,
                                                eventMsg.CardNumber,
                                                eventMsg.CardHolderName,
                                                eventMsg.CardExpiration,
                                                eventMsg.CardSecurityNumber,
                                                eventMsg.CardTypeId);

var requestCreateOrder = new IdentifiedCommand<CreateOrderCommand,bool>(createOrderCommand,
                                                                        eventMsg.RequestId);
result = await _mediator.Send(requestCreateOrder);
```

<span data-ttu-id="33f95-334">Jednak ten przypadek jest również nieco bardziej zaawansowany, ponieważ implementujemy również polecenia idempotentne.</span><span class="sxs-lookup"><span data-stu-id="33f95-334">However, this case is also slightly more advanced because we're also implementing idempotent commands.</span></span> <span data-ttu-id="33f95-335">Proces CreateOrderCommand powinien mieć wartość idempotentne, więc jeśli ten sam komunikat jest zduplikowany za pomocą sieci, ze względu na to, co się dzieje, takie samo zamówienie jest przetwarzane tylko raz.</span><span class="sxs-lookup"><span data-stu-id="33f95-335">The CreateOrderCommand process should be idempotent, so if the same message comes duplicated through the network, because of any reason, like retries, the same business order will be processed just once.</span></span>

<span data-ttu-id="33f95-336">Jest to implementowane przez zapakowanie polecenia biznesowego (w tym przypadku CreateOrderCommand) i osadzenie go w ogólnym IdentifiedCommand, który jest śledzony przez identyfikator każdej wiadomości przechodzącej przez sieć, która musi być idempotentne.</span><span class="sxs-lookup"><span data-stu-id="33f95-336">This is implemented by wrapping the business command (in this case CreateOrderCommand) and embedding it into a generic IdentifiedCommand, which is tracked by an ID of every message coming through the network that has to be idempotent.</span></span>

<span data-ttu-id="33f95-337">W poniższym kodzie można zobaczyć, że IdentifiedCommand nie ma więcej niż DTO z i ID oraz zawiniętego obiektu polecenia biznesowego.</span><span class="sxs-lookup"><span data-stu-id="33f95-337">In the code below, you can see that the IdentifiedCommand is nothing more than a DTO with and ID plus the wrapped business command object.</span></span>

```csharp
public class IdentifiedCommand<T, R> : IRequest<R>
    where T : IRequest<R>
{
    public T Command { get; }
    public Guid Id { get; }
    public IdentifiedCommand(T command, Guid id)
    {
        Command = command;
        Id = id;
    }
}
```

<span data-ttu-id="33f95-338">Następnie CommandHandler — obiekt dla IdentifiedCommand o nazwie [IdentifiedCommandHandler.cs](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Commands/IdentifiedCommandHandler.cs) będzie w istocie sprawdzać, czy identyfikator, który jest częścią komunikatu, już istnieje w tabeli.</span><span class="sxs-lookup"><span data-stu-id="33f95-338">Then the CommandHandler for the IdentifiedCommand named [IdentifiedCommandHandler.cs](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Commands/IdentifiedCommandHandler.cs) will basically check if the ID coming as part of the message already exists in a table.</span></span> <span data-ttu-id="33f95-339">Jeśli już istnieje, to polecenie nie zostanie przetworzone ponownie, dlatego działa jako polecenie idempotentne.</span><span class="sxs-lookup"><span data-stu-id="33f95-339">If it already exists, that command won't be processed again, so it behaves as an idempotent command.</span></span> <span data-ttu-id="33f95-340">Ten kod infrastruktury jest wykonywany przez `_requestManager.ExistAsync` wywołanie metody poniżej.</span><span class="sxs-lookup"><span data-stu-id="33f95-340">That infrastructure code is performed by the `_requestManager.ExistAsync` method call below.</span></span>

```csharp
// IdentifiedCommandHandler.cs
public class IdentifiedCommandHandler<T, R> : IRequestHandler<IdentifiedCommand<T, R>, R>
        where T : IRequest<R>
{
    private readonly IMediator _mediator;
    private readonly IRequestManager _requestManager;
    private readonly ILogger<IdentifiedCommandHandler<T, R>> _logger;

    public IdentifiedCommandHandler(
        IMediator mediator,
        IRequestManager requestManager,
        ILogger<IdentifiedCommandHandler<T, R>> logger)
    {
        _mediator = mediator;
        _requestManager = requestManager;
        _logger = logger ?? throw new System.ArgumentNullException(nameof(logger));
    }

    /// <summary>
    /// Creates the result value to return if a previous request was found
    /// </summary>
    /// <returns></returns>
    protected virtual R CreateResultForDuplicateRequest()
    {
        return default(R);
    }

    /// <summary>
    /// This method handles the command. It just ensures that no other request exists with the same ID, and if this is the case
    /// just enqueues the original inner command.
    /// </summary>
    /// <param name="message">IdentifiedCommand which contains both original command & request ID</param>
    /// <returns>Return value of inner command or default value if request same ID was found</returns>
    public async Task<R> Handle(IdentifiedCommand<T, R> message, CancellationToken cancellationToken)
    {
        var alreadyExists = await _requestManager.ExistAsync(message.Id);
        if (alreadyExists)
        {
            return CreateResultForDuplicateRequest();
        }
        else
        {
            await _requestManager.CreateRequestForCommandAsync<T>(message.Id);
            try
            {
                var command = message.Command;
                var commandName = command.GetGenericTypeName();
                var idProperty = string.Empty;
                var commandId = string.Empty;

                switch (command)
                {
                    case CreateOrderCommand createOrderCommand:
                        idProperty = nameof(createOrderCommand.UserId);
                        commandId = createOrderCommand.UserId;
                        break;

                    case CancelOrderCommand cancelOrderCommand:
                        idProperty = nameof(cancelOrderCommand.OrderNumber);
                        commandId = $"{cancelOrderCommand.OrderNumber}";
                        break;

                    case ShipOrderCommand shipOrderCommand:
                        idProperty = nameof(shipOrderCommand.OrderNumber);
                        commandId = $"{shipOrderCommand.OrderNumber}";
                        break;

                    default:
                        idProperty = "Id?";
                        commandId = "n/a";
                        break;
                }

                _logger.LogInformation(
                    "----- Sending command: {CommandName} - {IdProperty}: {CommandId} ({@Command})",
                    commandName,
                    idProperty,
                    commandId,
                    command);

                // Send the embedded business command to mediator so it runs its related CommandHandler
                var result = await _mediator.Send(command, cancellationToken);

                _logger.LogInformation(
                    "----- Command result: {@Result} - {CommandName} - {IdProperty}: {CommandId} ({@Command})",
                    result,
                    commandName,
                    idProperty,
                    commandId,
                    command);

                return result;
            }
            catch
            {
                return default(R);
            }
        }
    }
}
```

<span data-ttu-id="33f95-341">Ponieważ IdentifiedCommand działa podobnie jak forma polecenia biznesowego, gdy trzeba przetworzyć polecenie biznesowe, ponieważ nie jest to powtórzony identyfikator, to wykonuje to wewnętrzne polecenie biznesowe i ponownie przesyła je do mediator, jak w ostatniej części kodu pokazanego powyżej podczas uruchamiania `_mediator.Send(message.Command)` , z [IdentifiedCommandHandler.cs](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Commands/IdentifiedCommandHandler.cs).</span><span class="sxs-lookup"><span data-stu-id="33f95-341">Since the IdentifiedCommand acts like a business command's envelope, when the business command needs to be processed because it is not a repeated ID, then it takes that inner business command and resubmits it to Mediator, as in the last part of the code shown above when running `_mediator.Send(message.Command)`, from the [IdentifiedCommandHandler.cs](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Commands/IdentifiedCommandHandler.cs).</span></span>

<span data-ttu-id="33f95-342">W takim przypadku spowoduje to połączenie i uruchomienie programu obsługi poleceń firmy, w tym przypadku [CreateOrderCommandHandler](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Commands/CreateOrderCommandHandler.cs), w którym są uruchomione transakcje względem bazy danych porządkowania, jak pokazano w poniższym kodzie.</span><span class="sxs-lookup"><span data-stu-id="33f95-342">When doing that, it will link and run the business command handler, in this case, the [CreateOrderCommandHandler](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Commands/CreateOrderCommandHandler.cs), which is running transactions against the Ordering database, as shown in the following code.</span></span>

```csharp
// CreateOrderCommandHandler.cs
public class CreateOrderCommandHandler
        : IRequestHandler<CreateOrderCommand, bool>
{
    private readonly IOrderRepository _orderRepository;
    private readonly IIdentityService _identityService;
    private readonly IMediator _mediator;
    private readonly IOrderingIntegrationEventService _orderingIntegrationEventService;
    private readonly ILogger<CreateOrderCommandHandler> _logger;

    // Using DI to inject infrastructure persistence Repositories
    public CreateOrderCommandHandler(IMediator mediator,
        IOrderingIntegrationEventService orderingIntegrationEventService,
        IOrderRepository orderRepository,
        IIdentityService identityService,
        ILogger<CreateOrderCommandHandler> logger)
    {
        _orderRepository = orderRepository ?? throw new ArgumentNullException(nameof(orderRepository));
        _identityService = identityService ?? throw new ArgumentNullException(nameof(identityService));
        _mediator = mediator ?? throw new ArgumentNullException(nameof(mediator));
        _orderingIntegrationEventService = orderingIntegrationEventService ?? throw new ArgumentNullException(nameof(orderingIntegrationEventService));
        _logger = logger ?? throw new ArgumentNullException(nameof(logger));
    }

    public async Task<bool> Handle(CreateOrderCommand message, CancellationToken cancellationToken)
    {
        // Add Integration event to clean the basket
        var orderStartedIntegrationEvent = new OrderStartedIntegrationEvent(message.UserId);
        await _orderingIntegrationEventService.AddAndSaveEventAsync(orderStartedIntegrationEvent);

        // Add/Update the Buyer AggregateRoot
        // DDD patterns comment: Add child entities and value-objects through the Order Aggregate-Root
        // methods and constructor so validations, invariants and business logic
        // make sure that consistency is preserved across the whole aggregate
        var address = new Address(message.Street, message.City, message.State, message.Country, message.ZipCode);
        var order = new Order(message.UserId, message.UserName, address, message.CardTypeId, message.CardNumber, message.CardSecurityNumber, message.CardHolderName, message.CardExpiration);

        foreach (var item in message.OrderItems)
        {
            order.AddOrderItem(item.ProductId, item.ProductName, item.UnitPrice, item.Discount, item.PictureUrl, item.Units);
        }

        _logger.LogInformation("----- Creating Order - Order: {@Order}", order);

        _orderRepository.Add(order);

        return await _orderRepository.UnitOfWork
            .SaveEntitiesAsync(cancellationToken);
    }
}
```

### <a name="register-the-types-used-by-mediatr"></a><span data-ttu-id="33f95-343">Rejestrowanie typów używanych przez MediatR</span><span class="sxs-lookup"><span data-stu-id="33f95-343">Register the types used by MediatR</span></span>

<span data-ttu-id="33f95-344">Aby MediatR był świadomy klas programu obsługi poleceń, należy zarejestrować klasy mediator i klasy obsługi poleceń w kontenerze IoC.</span><span class="sxs-lookup"><span data-stu-id="33f95-344">In order for MediatR to be aware of your command handler classes, you need to register the mediator classes and the command handler classes in your IoC container.</span></span> <span data-ttu-id="33f95-345">Domyślnie MediatR używa Autofac jako kontenera IoC, ale można również użyć wbudowanego kontenera ASP.NET Core IoC lub innego kontenera obsługiwanego przez MediatR.</span><span class="sxs-lookup"><span data-stu-id="33f95-345">By default, MediatR uses Autofac as the IoC container, but you can also use the built-in ASP.NET Core IoC container or any other container supported by MediatR.</span></span>

<span data-ttu-id="33f95-346">Poniższy kod przedstawia sposób rejestrowania typów i poleceń mediator w przypadku korzystania z modułów Autofac.</span><span class="sxs-lookup"><span data-stu-id="33f95-346">The following code shows how to register Mediator's types and commands when using Autofac modules.</span></span>

```csharp
public class MediatorModule : Autofac.Module
{
    protected override void Load(ContainerBuilder builder)
    {
        builder.RegisterAssemblyTypes(typeof(IMediator).GetTypeInfo().Assembly)
            .AsImplementedInterfaces();

        // Register all the Command classes (they implement IRequestHandler)
        // in assembly holding the Commands
        builder.RegisterAssemblyTypes(typeof(CreateOrderCommand).GetTypeInfo().Assembly)
                .AsClosedTypesOf(typeof(IRequestHandler<,>));
        // Other types registration
        //...
    }
}
```

<span data-ttu-id="33f95-347">Jest to miejsce, w którym występuje "Magic" z MediatR.</span><span class="sxs-lookup"><span data-stu-id="33f95-347">This is where "the magic happens" with MediatR.</span></span>

<span data-ttu-id="33f95-348">Ponieważ każdy program obsługi poleceń implementuje `IRequestHandler<T>` interfejs ogólny, po zarejestrowaniu zestawów przy użyciu `RegisteredAssemblyTypes` metody wszystkie typy oznaczone jako `IRequestHandler` również są rejestrowane z ich użyciem `Commands` .</span><span class="sxs-lookup"><span data-stu-id="33f95-348">As each command handler implements the generic `IRequestHandler<T>` interface, when you register the assemblies using `RegisteredAssemblyTypes` method all the types marked as `IRequestHandler` also gets registered with their `Commands`.</span></span> <span data-ttu-id="33f95-349">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="33f95-349">For   example:</span></span>

```csharp
public class CreateOrderCommandHandler
  : IRequestHandler<CreateOrderCommand, bool>
{
```

<span data-ttu-id="33f95-350">Jest to kod, który służy do skorelowania poleceń z programami obsługi poleceń.</span><span class="sxs-lookup"><span data-stu-id="33f95-350">That is the code that correlates commands with command handlers.</span></span> <span data-ttu-id="33f95-351">Procedura obsługi jest tylko prostą klasą, ale dziedziczy z `RequestHandler<T>` , gdzie T jest typem polecenia, a MediatR sprawdza, czy jest wywoływana z prawidłowym ładunkiem (polecenie).</span><span class="sxs-lookup"><span data-stu-id="33f95-351">The handler is just a simple class, but it inherits from `RequestHandler<T>`, where T is the command type, and MediatR makes sure it is invoked with the correct payload (the command).</span></span>

## <a name="apply-cross-cutting-concerns-when-processing-commands-with-the-behaviors-in-mediatr"></a><span data-ttu-id="33f95-352">Stosuj problemy z wycinaniem podczas przetwarzania poleceń za pomocą zachowań w MediatR</span><span class="sxs-lookup"><span data-stu-id="33f95-352">Apply cross-cutting concerns when processing commands with the Behaviors in MediatR</span></span>

<span data-ttu-id="33f95-353">Istnieje jeszcze jeden element: możliwość zastosowania zagadnień związanych z wycinaniem do potoku mediator.</span><span class="sxs-lookup"><span data-stu-id="33f95-353">There is one more thing: being able to apply cross-cutting concerns to the mediator pipeline.</span></span> <span data-ttu-id="33f95-354">Na końcu kodu modułu rejestracji Autofac można także sprawdzić, w jaki sposób rejestruje typ zachowania, w tym w przypadku niestandardowej klasy LoggingBehavior i klasy ValidatorBehavior.</span><span class="sxs-lookup"><span data-stu-id="33f95-354">You can also see at the end of the Autofac registration module code how it registers a behavior type, specifically, a custom LoggingBehavior class and a ValidatorBehavior class.</span></span> <span data-ttu-id="33f95-355">Można jednak również dodać inne niestandardowe zachowania.</span><span class="sxs-lookup"><span data-stu-id="33f95-355">But you could add other custom behaviors, too.</span></span>

```csharp
public class MediatorModule : Autofac.Module
{
    protected override void Load(ContainerBuilder builder)
    {
        builder.RegisterAssemblyTypes(typeof(IMediator).GetTypeInfo().Assembly)
            .AsImplementedInterfaces();

        // Register all the Command classes (they implement IRequestHandler)
        // in assembly holding the Commands
        builder.RegisterAssemblyTypes(
                              typeof(CreateOrderCommand).GetTypeInfo().Assembly).
                                   AsClosedTypesOf(typeof(IRequestHandler<,>));
        // Other types registration
        //...
        builder.RegisterGeneric(typeof(LoggingBehavior<,>)).
                                                   As(typeof(IPipelineBehavior<,>));
        builder.RegisterGeneric(typeof(ValidatorBehavior<,>)).
                                                   As(typeof(IPipelineBehavior<,>));
    }
}
```

<span data-ttu-id="33f95-356">Tę klasę [LoggingBehavior](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Behaviors/LoggingBehavior.cs) można zaimplementować jako następujący kod, który rejestruje informacje o wykonywanej obsłudze poleceń i o tym, czy zakończyły się powodzeniem, czy nie.</span><span class="sxs-lookup"><span data-stu-id="33f95-356">That [LoggingBehavior](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Behaviors/LoggingBehavior.cs) class can be implemented as the following code, which logs information about the command handler being executed and whether it was successful or not.</span></span>

```csharp
public class LoggingBehavior<TRequest, TResponse>
         : IPipelineBehavior<TRequest, TResponse>
{
    private readonly ILogger<LoggingBehavior<TRequest, TResponse>> _logger;
    public LoggingBehavior(ILogger<LoggingBehavior<TRequest, TResponse>> logger) =>
                                                                  _logger = logger;

    public async Task<TResponse> Handle(TRequest request,
                                        RequestHandlerDelegate<TResponse> next)
    {
        _logger.LogInformation($"Handling {typeof(TRequest).Name}");
        var response = await next();
        _logger.LogInformation($"Handled {typeof(TResponse).Name}");
        return response;
    }
}
```

<span data-ttu-id="33f95-357">Po prostu implementując tę klasę zachowań i rejestrując ją w potoku (w MediatorModule powyżej) wszystkie polecenia przetworzone przez MediatR będą rejestrować informacje o wykonaniu.</span><span class="sxs-lookup"><span data-stu-id="33f95-357">Just by implementing this behavior class and by registering it in the pipeline (in the MediatorModule above), all the commands processed through MediatR will be logging information about the execution.</span></span>

<span data-ttu-id="33f95-358">Mikrousługa porządkowania eShopOnContainers stosuje również drugie zachowanie dla podstawowych walidacji, Klasa [ValidatorBehavior](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Behaviors/ValidatorBehavior.cs) , która opiera się na bibliotece [FluentValidation](https://github.com/JeremySkinner/FluentValidation) , jak pokazano w poniższym kodzie:</span><span class="sxs-lookup"><span data-stu-id="33f95-358">The eShopOnContainers ordering microservice also applies a second behavior for basic validations, the [ValidatorBehavior](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Behaviors/ValidatorBehavior.cs) class that relies on the [FluentValidation](https://github.com/JeremySkinner/FluentValidation) library, as shown in the following code:</span></span>

```csharp
public class ValidatorBehavior<TRequest, TResponse>
         : IPipelineBehavior<TRequest, TResponse>
{
    private readonly IValidator<TRequest>[] _validators;
    public ValidatorBehavior(IValidator<TRequest>[] validators) =>
                                                         _validators = validators;

    public async Task<TResponse> Handle(TRequest request,
                                        RequestHandlerDelegate<TResponse> next)
    {
        var failures = _validators
            .Select(v => v.Validate(request))
            .SelectMany(result => result.Errors)
            .Where(error => error != null)
            .ToList();

        if (failures.Any())
        {
            throw new OrderingDomainException(
                $"Command Validation Errors for type {typeof(TRequest).Name}",
                        new ValidationException("Validation exception", failures));
        }

        var response = await next();
        return response;
    }
}
```

<span data-ttu-id="33f95-359">W tym miejscu zachowanie wywołuje wyjątek, jeśli Walidacja nie powiedzie się, ale można również zwrócić obiekt wynikowy, zawierający wynik polecenia, jeśli zakończyło się powodzeniem lub komunikat sprawdzania poprawności w przypadku niepowodzenia.</span><span class="sxs-lookup"><span data-stu-id="33f95-359">Here the behavior is raising an exception if validation fails, but you could also return a result object, containing the command result if it succeeded or the validation messages in case it didn't.</span></span> <span data-ttu-id="33f95-360">Prawdopodobnie ułatwi to wyświetlanie wyników walidacji dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="33f95-360">This would probably make it easier to display validation results to the user.</span></span>

<span data-ttu-id="33f95-361">Następnie na podstawie biblioteki [FluentValidation](https://github.com/JeremySkinner/FluentValidation) należy utworzyć weryfikację danych przesłanych z CreateOrderCommand, jak w poniższym kodzie:</span><span class="sxs-lookup"><span data-stu-id="33f95-361">Then, based on the [FluentValidation](https://github.com/JeremySkinner/FluentValidation) library, you would create validation for the data passed with CreateOrderCommand, as in the following code:</span></span>

```csharp
public class CreateOrderCommandValidator : AbstractValidator<CreateOrderCommand>
{
    public CreateOrderCommandValidator()
    {
        RuleFor(command => command.City).NotEmpty();
        RuleFor(command => command.Street).NotEmpty();
        RuleFor(command => command.State).NotEmpty();
        RuleFor(command => command.Country).NotEmpty();
        RuleFor(command => command.ZipCode).NotEmpty();
        RuleFor(command => command.CardNumber).NotEmpty().Length(12, 19);
        RuleFor(command => command.CardHolderName).NotEmpty();
        RuleFor(command => command.CardExpiration).NotEmpty().Must(BeValidExpirationDate).WithMessage("Please specify a valid card expiration date");
        RuleFor(command => command.CardSecurityNumber).NotEmpty().Length(3);
        RuleFor(command => command.CardTypeId).NotEmpty();
        RuleFor(command => command.OrderItems).Must(ContainOrderItems).WithMessage("No order items found");
    }

    private bool BeValidExpirationDate(DateTime dateTime)
    {
        return dateTime >= DateTime.UtcNow;
    }

    private bool ContainOrderItems(IEnumerable<OrderItemDTO> orderItems)
    {
        return orderItems.Any();
    }
}

```

<span data-ttu-id="33f95-362">Można utworzyć dodatkowe walidacje.</span><span class="sxs-lookup"><span data-stu-id="33f95-362">You could create additional validations.</span></span> <span data-ttu-id="33f95-363">Jest to bardzo czysty i elegancki sposób implementacji walidacji poleceń.</span><span class="sxs-lookup"><span data-stu-id="33f95-363">This is a very clean and elegant way to implement your command validations.</span></span>

<span data-ttu-id="33f95-364">W podobny sposób można zaimplementować inne zachowania dla dodatkowych aspektów lub obaw związanych z wycinaniem, które mają być stosowane do poleceń podczas ich obsługi.</span><span class="sxs-lookup"><span data-stu-id="33f95-364">In a similar way, you could implement other behaviors for additional aspects or cross-cutting concerns that you want to apply to commands when handling them.</span></span>

#### <a name="additional-resources"></a><span data-ttu-id="33f95-365">Zasoby dodatkowe</span><span class="sxs-lookup"><span data-stu-id="33f95-365">Additional resources</span></span>

##### <a name="the-mediator-pattern"></a><span data-ttu-id="33f95-366">Wzorzec mediator</span><span class="sxs-lookup"><span data-stu-id="33f95-366">The mediator pattern</span></span>

- <span data-ttu-id="33f95-367">**Wzorzec mediator** </span><span class="sxs-lookup"><span data-stu-id="33f95-367">**Mediator pattern** </span></span>\
  [https://en.wikipedia.org/wiki/Mediator\_pattern](https://en.wikipedia.org/wiki/Mediator_pattern)

##### <a name="the-decorator-pattern"></a><span data-ttu-id="33f95-368">Wzorzec Dekoratora</span><span class="sxs-lookup"><span data-stu-id="33f95-368">The decorator pattern</span></span>

- <span data-ttu-id="33f95-369">**Wzorzec Dekoratora** </span><span class="sxs-lookup"><span data-stu-id="33f95-369">**Decorator pattern** </span></span>\
  [https://en.wikipedia.org/wiki/Decorator\_pattern](https://en.wikipedia.org/wiki/Decorator_pattern)

##### <a name="mediatr-jimmy-bogard"></a><span data-ttu-id="33f95-370">MediatR (Jimmy Bogard)</span><span class="sxs-lookup"><span data-stu-id="33f95-370">MediatR (Jimmy Bogard)</span></span>

- <span data-ttu-id="33f95-371">**MediatR.**</span><span class="sxs-lookup"><span data-stu-id="33f95-371">**MediatR.**</span></span> <span data-ttu-id="33f95-372">Repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="33f95-372">GitHub repo.</span></span> \
  <https://github.com/jbogard/MediatR>

- <span data-ttu-id="33f95-373">**CQRS z MediatR i automapowaniem** </span><span class="sxs-lookup"><span data-stu-id="33f95-373">**CQRS with MediatR and AutoMapper** </span></span>\
  <https://lostechies.com/jimmybogard/2015/05/05/cqrs-with-mediatr-and-automapper/>

- <span data-ttu-id="33f95-374">**Umieść swoje kontrolery według pokarmu: wpisów i poleceń.**</span><span class="sxs-lookup"><span data-stu-id="33f95-374">**Put your controllers on a diet: POSTs and commands.**</span></span> \
  <https://lostechies.com/jimmybogard/2013/12/19/put-your-controllers-on-a-diet-posts-and-commands/>

- <span data-ttu-id="33f95-375">**Rozwiązywanie problemów z rozcinaniem przy użyciu potoku mediator** </span><span class="sxs-lookup"><span data-stu-id="33f95-375">**Tackling cross-cutting concerns with a mediator pipeline** </span></span>\
  <https://lostechies.com/jimmybogard/2014/09/09/tackling-cross-cutting-concerns-with-a-mediator-pipeline/>

- <span data-ttu-id="33f95-376">**CQRS i REST: idealne dopasowanie** </span><span class="sxs-lookup"><span data-stu-id="33f95-376">**CQRS and REST: the perfect match** </span></span>\
  <https://lostechies.com/jimmybogard/2016/06/01/cqrs-and-rest-the-perfect-match/>

- <span data-ttu-id="33f95-377">**Przykłady potoku MediatR** </span><span class="sxs-lookup"><span data-stu-id="33f95-377">**MediatR Pipeline Examples** </span></span>\
  <https://lostechies.com/jimmybogard/2016/10/13/mediatr-pipeline-examples/>

- <span data-ttu-id="33f95-378">**Armatura testu wycinka pionowego dla MediatR i ASP.NET Core** </span><span class="sxs-lookup"><span data-stu-id="33f95-378">**Vertical Slice Test Fixtures for MediatR and ASP.NET Core** </span></span>\
  <https://lostechies.com/jimmybogard/2016/10/24/vertical-slice-test-fixtures-for-mediatr-and-asp-net-core/>

- <span data-ttu-id="33f95-379">**Wydano rozszerzenia MediatR dla iniekcji zależności firmy Microsoft** </span><span class="sxs-lookup"><span data-stu-id="33f95-379">**MediatR Extensions for Microsoft Dependency Injection Released** </span></span>\
  <https://lostechies.com/jimmybogard/2016/07/19/mediatr-extensions-for-microsoft-dependency-injection-released/>

##### <a name="fluent-validation"></a><span data-ttu-id="33f95-380">Weryfikacja w programie Fluent</span><span class="sxs-lookup"><span data-stu-id="33f95-380">Fluent validation</span></span>

- <span data-ttu-id="33f95-381">**Jeremy Skinner. FluentValidation.**</span><span class="sxs-lookup"><span data-stu-id="33f95-381">**Jeremy Skinner. FluentValidation.**</span></span> <span data-ttu-id="33f95-382">Repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="33f95-382">GitHub repo.</span></span> \
  <https://github.com/JeremySkinner/FluentValidation>

> [!div class="step-by-step"]
> <span data-ttu-id="33f95-383">[Poprzedni](microservice-application-layer-web-api-design.md) 
>  [Dalej](../implement-resilient-applications/index.md)</span><span class="sxs-lookup"><span data-stu-id="33f95-383">[Previous](microservice-application-layer-web-api-design.md)
[Next](../implement-resilient-applications/index.md)</span></span>
