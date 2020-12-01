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
# <a name="implement-the-microservice-application-layer-using-the-web-api"></a>Implementowanie warstwy aplikacji mikrousług za pomocą internetowego interfejsu API

## <a name="use-dependency-injection-to-inject-infrastructure-objects-into-your-application-layer"></a>Użyj iniekcji zależności, aby wstrzyknąć obiekty infrastruktury do warstwy aplikacji

Jak wspomniano wcześniej, warstwa aplikacji może być implementowana w ramach kompilowanego artefaktu (zestawu), takiego jak w projekcie interfejsu API sieci Web lub w projekcie aplikacji sieci Web MVC. W przypadku mikrousługi skompilowanej przy ASP.NET Core warstwa aplikacji zazwyczaj będzie biblioteką internetowego interfejsu API. Jeśli chcesz oddzielić dane pochodzące z ASP.NET Core (infrastruktury oraz kontrolerów) z niestandardowego kodu warstwy aplikacji, możesz również umieścić warstwę aplikacji w oddzielnej bibliotece klas, ale jest to opcjonalne.

Na przykład kod warstwy aplikacji mikrousługi porządkowania jest bezpośrednio zaimplementowany jako część projektu **porządkowania. API** (projekt ASP.NET Core Web API), jak pokazano na rysunku 7-23.

:::image type="complex" source="./media/microservice-application-layer-implementation-web-api/ordering-api-microservice.png" alt-text="Zrzut ekranu przedstawiający mikrousługę porządkowanie. API w Eksplorator rozwiązań.":::
Widok Eksplorator rozwiązań mikrousługi porządkowania. API, pokazujący podfoldery w folderze aplikacji: zachowania, polecenia, DomainEventHandlers, IntegrationEvents, modele, zapytania i walidacje.
:::image-end:::

**Rysunek 7-23**. Warstwa aplikacji w projekcie interfejsu API sieci Web programu porządkowanie. API ASP.NET Core

ASP.NET Core obejmuje prosty [wbudowany kontener IOC](/aspnet/core/fundamentals/dependency-injection) (reprezentowany przez interfejs IServiceProvider), który domyślnie obsługuje iniekcję konstruktora, a ASP.NET udostępnia niektóre usługi za pomocą di. ASP.NET Core używa *usługi* Term dla dowolnego typu rejestru, który zostanie dodany przez di. Należy skonfigurować usługi wbudowanego kontenera w metodzie ConfigureServices w klasie startowej aplikacji. Zależności są implementowane w usługach, które są wymagane przez typ i rejestrowane w kontenerze IoC.

Zazwyczaj należy wstrzyknąć zależności, które implementują obiekty infrastruktury. Typową zależnością do iniekcji jest repozytorium. Można jednak wprowadzić inną zależność infrastruktury, którą może mieć. W przypadku prostszej implementacji można bezpośrednio wstrzyknąć obiekt wzorca jednostki pracy (obiekt EF DbContext), ponieważ DbContext jest również implementacją obiektów trwałości infrastruktury.

W poniższym przykładzie można zobaczyć, jak platforma .NET Core wprowadza wymagane obiekty repozytorium za pomocą konstruktora. Klasa jest programem obsługi poleceń, który zostanie uwzględniony w następnej sekcji.

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

Klasa używa wstrzykniętych repozytoriów, aby wykonać transakcję i zachować zmiany stanu. Nie ma znaczenia, czy ta klasa jest programem obsługi poleceń, metodą ASP.NET Core kontrolerem interfejsu API sieci Web, czy [usługą aplikacji DDD](https://lostechies.com/jimmybogard/2008/08/21/services-in-domain-driven-design/). Jest ona ostatecznie prostą klasą, która używa repozytoriów, jednostek domeny i innej koordynacji aplikacji w sposób podobny do procedury obsługi poleceń. Iniekcja zależności działa tak samo jak w przypadku wszystkich wymienionych klas, jak w przykładzie przy użyciu DI na podstawie konstruktora.

### <a name="register-the-dependency-implementation-types-and-interfaces-or-abstractions"></a>Rejestrowanie typów implementacji zależności oraz interfejsów lub streszczeń

Przed użyciem obiektów wstrzykiwanych za pomocą konstruktorów należy wiedzieć, gdzie należy zarejestrować interfejsy i klasy, które tworzą obiekty wstrzykiwane do klas aplikacji za pomocą DI. (Podobnie jak w przypadku konstruktora, jak pokazano wcześniej).

#### <a name="use-the-built-in-ioc-container-provided-by-aspnet-core"></a>Użyj wbudowanego kontenera IoC zapewnianego przez ASP.NET Core

W przypadku korzystania z wbudowanego kontenera IoC dostarczonego przez ASP.NET Core należy zarejestrować typy, które mają zostać dodane w metodzie ConfigureServices w pliku Startup.cs, tak jak w poniższym kodzie:

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

Typowym wzorcem rejestrowania typów w kontenerze IoC jest zarejestrowanie pary typów — interfejsu i powiązanej klasy implementacji. Następnie po zażądaniu obiektu z kontenera IoC za pomocą dowolnego konstruktora należy zażądać obiektu określonego typu interfejsu. Na przykład, w poprzednim przykładzie, ostatni wiersz stan, gdy którykolwiek z konstruktorów ma zależność od IMyCustomRepository (interfejs lub Abstrakcja), kontener IoC będzie wstrzyknąć wystąpienie klasy implementacji MyCustomSQLServerRepository.

#### <a name="use-the-scrutor-library-for-automatic-types-registration"></a>Rejestracja typów automatycznych przy użyciu biblioteki Scrutor

W przypadku korzystania z funkcji DI w oprogramowaniu .NET Core warto mieć możliwość skanowania zestawu i automatycznego rejestrowania jego typów według Konwencji. Ta funkcja nie jest obecnie dostępna w ASP.NET Core. Można jednak użyć biblioteki [Scrutor](https://github.com/khellang/Scrutor) dla tego programu. Takie podejście jest wygodne, gdy masz dziesiątki typów, które muszą być zarejestrowane w kontenerze IoC.

#### <a name="additional-resources"></a>Zasoby dodatkowe

- **Matthew króla. Rejestrowanie usług w usłudze Scrutor** \
  <https://www.mking.net/blog/registering-services-with-scrutor>

- **Kristian Hellang. Scrutor.** Repozytorium GitHub. \
  <https://github.com/khellang/Scrutor>

#### <a name="use-autofac-as-an-ioc-container"></a>Używanie Autofac jako kontenera IoC

Można również użyć dodatkowych kontenerów IoC i podłączyć je do potoku ASP.NET Core, jak w mikrousłudze porządkowania w eShopOnContainers, która używa [Autofac](https://autofac.org/). W przypadku korzystania z Autofac zazwyczaj rejestruje się typy za pośrednictwem modułów, które umożliwiają podział typów rejestracji między wiele plików w zależności od tego, gdzie są typy, podobnie jak w przypadku typów aplikacji rozproszonych w wielu bibliotekach klas.

Na przykład poniżej przedstawiono [moduł aplikacji Autofac](https://github.com/dotnet-architecture/eShopOnContainers/blob/master/src/Services/Ordering/Ordering.API/Infrastructure/AutofacModules/ApplicationModule.cs) dla projektu [interfejsu API sieci Web porządkowania. API](https://github.com/dotnet-architecture/eShopOnContainers/tree/master/src/Services/Ordering/Ordering.API) z typami, które mają zostać dodane.

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

Autofac ma również funkcję do [skanowania zestawów i rejestrowania typów według konwencji nazw](https://autofac.readthedocs.io/en/latest/register/scanning.html).

Proces rejestracji i pojęcia są bardzo podobne do sposobu rejestrowania typów przy użyciu wbudowanego kontenera ASP.NET Core IoC, ale Składnia używana Autofac jest nieco inna.

W przykładowym kodzie IOrderRepository abstrakcji jest rejestrowany wraz z klasą implementacji OrderRepository. Oznacza to, że za każdym razem, gdy Konstruktor deklaruje zależność poprzez abstrakcyjność lub interfejs IOrderRepository, kontener IoC będzie wstrzyknąć wystąpienie klasy OrderRepository.

Typ zakresu wystąpienia określa, jak wystąpienie jest udostępniane między żądaniami dla tej samej usługi lub zależności. Gdy żądanie jest tworzone dla zależności, kontener IoC może zwrócić następujące elementy:

- Pojedyncze wystąpienie na okres istnienia (określone w ASP.NET Core kontener IoC jako *objęty zakresem*).

- Nowe wystąpienie na zależność (określone w ASP.NET Core kontener IoC jako *przejściowy*).

- Pojedyncze wystąpienie współużytkowane przez wszystkie obiekty używające kontenera IoC (określane w kontenerze ASP.NET Core IoC jako *pojedyncze*).

#### <a name="additional-resources"></a>Zasoby dodatkowe

- **Wprowadzenie do iniekcji zależności w ASP.NET Core** \
  [https://docs.microsoft.com/aspnet/core/fundamentals/dependency-injection](/aspnet/core/fundamentals/dependency-injection)

- **Autofac.** Oficjalna dokumentacja. \
  <https://docs.autofac.org/en/latest/>

- **Porównanie ASP.NET Core okresów istnienia usługi kontenera IoC z wystąpieniami Autofac IoC Container Scopes-Cesar de La Torre.** \
  <https://devblogs.microsoft.com/cesardelatorre/comparing-asp-net-core-ioc-service-life-times-and-autofac-ioc-instance-scopes/>

## <a name="implement-the-command-and-command-handler-patterns"></a>Implementowanie wzorców programu obsługi poleceń i poleceń

W przykładzie między konstruktorem pokazanym w poprzedniej sekcji kontener IoC został wstrzykiwany przez Konstruktor w klasie. Ale dokładnie tam, gdzie zostały wprowadzone? W prostym interfejsie API sieci Web (na przykład mikrousługi w katalogu eShopOnContainers) można wstrzyknąć je na poziomie kontrolerów MVC, w konstruktorze kontrolera, w ramach potoku żądania ASP.NET Core. Jednak w początkowym kodzie tej sekcji (Klasa [CreateOrderCommandHandler](https://github.com/dotnet-architecture/eShopOnContainers/blob/master/src/Services/Ordering/Ordering.API/Application/Commands/CreateOrderCommandHandler.cs) z usługi PORZĄDKOWANIA. API w eShopOnContainers), iniekcja zależności odbywa się za pośrednictwem konstruktora określonego polecenia. Przekaż nam wyjaśnienie, czym jest procedura obsługi poleceń i dlaczego warto z niej korzystać.

Wzorzec polecenia jest wewnętrznie związany ze wzorcem CQRS, który został wprowadzony wcześniej w tym przewodniku. CQRS ma dwie strony. Pierwszy obszar jest kwerendami, przy użyciu uproszczonych zapytań z [Dapper](https://github.com/StackExchange/dapper-dot-net) Micro ORM, który został wcześniej wyjaśniony. Drugi obszar to polecenia, które są punktem początkowym dla transakcji i kanałem wejściowym spoza usługi.

Jak pokazano na rysunku 7-24, wzorzec opiera się na akceptowaniu poleceń po stronie klienta, przetwarzaniu ich na podstawie reguł modelu domeny, a wreszcie utrzymując Stany przy użyciu transakcji.

![Diagram przedstawiający przepływ danych wysokiego poziomu z klienta do bazy danych programu.](./media/microservice-application-layer-implementation-web-api/high-level-writes-side.png)

**Rysunek 7-24**. Widok wysokiego poziomu poleceń lub "Strona transakcyjna" w wzorcu CQRS

Rysunek 7-24 pokazuje, że aplikacja interfejsu użytkownika wysyła polecenie za pomocą interfejsu API, który jest `CommandHandler` zależny od modelu domeny i infrastruktury, aby zaktualizować bazę danych.

### <a name="the-command-class"></a>Klasa polecenia

Polecenie to żądanie systemu do wykonania akcji, która zmienia stan systemu. Polecenia są bezwzględnie i powinny być przetwarzane tylko raz.

Ponieważ polecenia są bezwzględne, zazwyczaj nazywa się czasownikiem w bezwzględnym nastroju (na przykład "Create" lub "Update") i mogą zawierać typ agregacji, na przykład CreateOrderCommand. W przeciwieństwie do zdarzenia, polecenie nie jest faktem z przeszłości; jest to tylko żądanie i dlatego może zostać odrzucone.

Polecenia mogą pochodzić z interfejsu użytkownika w wyniku użytkownika inicjującego żądanie lub z Menedżera procesów, gdy Menedżer procesów kieruje wartość zagregowaną w celu wykonania akcji.

Ważną cechą polecenia jest to, że należy je przetworzyć tylko raz przez jednego odbiorcę. Wynika to z tego, że polecenie jest pojedynczą akcją lub transakcją, którą chcesz wykonać w aplikacji. Na przykład to samo polecenie tworzenia kolejności nie powinno być przetwarzane więcej niż raz. Jest to ważna różnica między poleceniami i zdarzeniami. Zdarzenia mogą być przetwarzane wiele razy, ponieważ wiele systemów lub mikrousług może być zainteresowanych wydarzeniem.

Ponadto ważne jest, aby polecenie było przetwarzane tylko raz w przypadku, gdy polecenie nie jest idempotentne. Polecenie jest idempotentne, jeśli może być wykonywane wiele razy bez zmiany wyniku, ze względu na charakter polecenia lub w sposób, w jaki system obsługuje polecenie.

Dobrym rozwiązaniem jest udostępnienie poleceń i aktualizacji idempotentne, gdy jest to zrozumiałe dla reguł firmy i niezwiązanych z tą domeną. Na przykład, aby użyć tego samego przykładu, jeśli z jakiegoś powodu (logika ponawiania, działanie hakerskie itp.) to samo polecenie "zbyt Order" dotrze do systemu, powinno być możliwe jego zidentyfikowanie i upewnienie się, że nie utworzysz wielu zamówień. Aby to zrobić, należy dołączyć rodzaj tożsamości w operacjach i określić, czy polecenie lub aktualizacja zostały już przetworzone.

Wysyłasz polecenie do pojedynczego odbiorcy; nie publikujesz polecenia. Publikowanie jest dla zdarzeń, które określają fakt, że coś się stało i mogą być interesujące dla odbiorców zdarzeń. W przypadku zdarzeń Wydawca nie ma obaw dotyczących tego, które osoby odbierające uzyskują wydarzenie lub co robią. Ale zdarzenia związane z domeną lub integracją to różne historie już wprowadzone w poprzednich sekcjach.

Polecenie jest implementowane z klasą zawierającą pola danych lub kolekcje ze wszystkimi informacjami, które są konieczne, aby można było wykonać to polecenie. Polecenie jest specjalnym rodzajem obiektu Transfer danych (DTO), który jest specjalnie używany do żądania zmian lub transakcji. Samo polecenie jest zależne od informacji, które są zbędne do przetwarzania polecenia i nic nie rób.

W poniższym przykładzie pokazano klasę uproszczoną `CreateOrderCommand` . Jest to niezmienne polecenie, które jest używane w mikrousłudze porządkowania w eShopOnContainers.

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

Zasadniczo Klasa Command zawiera wszystkie dane potrzebne do wykonania transakcji biznesowej przy użyciu obiektów modelu domeny. W ten sposób polecenia są po prostu strukturą danych, która zawiera dane tylko do odczytu, i bez zachowania. Nazwa polecenia wskazuje jego przeznaczenie. W wielu językach, takich jak C#, polecenia są reprezentowane jako klasy, ale nie są to klasy prawdziwe w rzeczywistości zorientowane obiektowo.

Jako dodatkową cechą polecenia są niezmienne, ponieważ oczekiwane użycie polega na tym, że są przetwarzane bezpośrednio przez model domeny. Nie trzeba zmieniać ich w przewidywanym okresie istnienia. W klasie języka C# niezmienności można osiągnąć, nie ma żadnych metod ustawiających ani inne metody, które zmieniają stan wewnętrzny.

Należy pamiętać, że jeśli planujesz lub oczekujesz, że polecenia przechodzą przez proces serializacji/deserializacji, właściwości muszą mieć prywatną metodę ustawiającą oraz `[DataMember]` atrybut (lub `[JsonProperty]` ). W przeciwnym razie Deserializator nie będzie w stanie odtworzyć obiektu w miejscu docelowym przy użyciu wymaganych wartości. Można również użyć prawdziwie właściwości tylko do odczytu, jeśli klasa ma konstruktora z parametrami dla wszystkich właściwości, z normalną konwencją nazewnictwa camelCase, i dodając adnotację do konstruktora jako `[JsonConstructor]` . Jednak ta opcja wymaga więcej kodu.

Na przykład Klasa poleceń do tworzenia zamówienia jest prawdopodobnie podobna pod względem danych do zamówienia, które chcesz utworzyć, ale prawdopodobnie nie potrzebujesz tych samych atrybutów. Na przykład nie `CreateOrderCommand` ma identyfikatora zamówienia, ponieważ zamówienie nie zostało jeszcze utworzone.

Wiele klas poleceń może być proste, wymagając tylko kilku pól, które wymagają zmiany. W przypadku zmiany stanu zamówienia z "w toku" na "płatne" lub "wysłane" przy użyciu polecenia podobnego do poniższego:

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

Niektórzy deweloperzy sprawiają, że obiekty żądania interfejsu użytkownika są oddzielone od ich DTO poleceń, ale jest to tylko preferencja. Jest to żmudnyma separacja z nieznacznie większą wartością, a obiekty są niemal dokładnie takie same. Na przykład w eShopOnContainers niektóre polecenia są dostępne bezpośrednio po stronie klienta.

### <a name="the-command-handler-class"></a>Klasa procedury obsługi poleceń

Należy zaimplementować konkretną klasę programu obsługi poleceń dla każdego polecenia. To w jaki sposób działa wzorzec oraz miejsce użycia obiektu polecenia, obiektów domeny i obiektów repozytorium infrastruktury. Program obsługi poleceń jest w rzeczywistości sercem warstwy aplikacji pod kątem CQRS i DDD. Jednak cała Logika domeny powinna być zawarta w klasach domeny — w ramach agregacji głównych (jednostek głównych), jednostek podrzędnych lub [usług domenowych](https://lostechies.com/jimmybogard/2008/08/21/services-in-domain-driven-design/), ale nie w ramach procedury obsługi poleceń, która jest klasą z warstwy aplikacji.

Klasa procedury obsługi poleceń oferuje silny punkt taktowania w celu osiągnięcia jednej zasady odpowiedzialności (SRP) wymienionej w poprzedniej sekcji.

Procedura obsługi poleceń odbiera polecenie i uzyskuje wynik z używanej wartości zagregowanej. Wynikiem może być pomyślne wykonanie polecenia lub wyjątek. W przypadku wyjątku, stan systemu powinien być niezmieniony.

Procedura obsługi poleceń zazwyczaj wykonuje następujące czynności:

- Odbierze obiekt polecenia, taki jak DTO (z [mediator](https://en.wikipedia.org/wiki/Mediator_pattern) lub innego obiektu infrastruktury).

- Sprawdza, czy polecenie jest prawidłowe (jeśli nie jest zweryfikowane przez mediator).

- Tworzy wystąpienie zagregowanego wystąpienia agregacji, które jest elementem docelowym bieżącego polecenia.

- Wykonuje metodę w wystąpieniu agregacji głównej, pobierając wymagane dane z polecenia.

- Zachowuje nowy stan agregacji w powiązanej bazie danych. Ta ostatnia operacja to rzeczywista transakcja.

Zazwyczaj procedura obsługi poleceń zajmuje się pojedynczym agregowaniem, który jest oparty na jego zagregowanym elemencie głównym (jednostki głównej). Jeśli odbiór jednego polecenia ma wpływ na wiele agregacji, można użyć zdarzeń domeny do propagowania stanów lub akcji w wielu agregacjach.

Ważnym punktem jest to, że podczas przetwarzania polecenia Cała logika domeny powinna znajdować się wewnątrz modelu domeny (Agregaty), w pełni hermetyzowane i gotowe do testowania jednostkowego. Procedura obsługi poleceń działa jako sposób uzyskania modelu domeny z bazy danych i jako ostatni krok, aby określić warstwę infrastruktury (repozytoria), aby zachować zmiany, gdy model zostanie zmieniony. Zaletą tego podejścia jest możliwość refaktoryzacji logiki domeny w odizolowanym, w pełni wbudowanym, rozbudowanym modelu domeny bez zmiany kodu w warstwach aplikacji lub infrastruktury, które są poziomem instalacji (programy obsługi poleceń, internetowy interfejs API, repozytoria itp.).

Gdy programy obsługi poleceń są złożone z zbyt dużą ilością logiki, która może być zapachem kodu. Zapoznaj się z nimi, a jeśli znajdziesz logikę domeny, Refaktoryzacja kodu, aby przenieść zachowanie domeny do metod obiektów domeny (agregacja elementu głównego i podrzędnego).

Przykładem klasy procedury obsługi poleceń Poniższy kod przedstawia tę samą `CreateOrderCommandHandler` klasę, która została wyświetlona na początku tego rozdziału. W tym przypadku wyróżnia również metodę dojścia i operacje przy użyciu obiektów modelu domeny/agregacji.

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

Są to dodatkowe kroki, które powinien wykonać procedura obsługi polecenia:

- Użyj danych polecenia do działania z metodami i zachowaniem zagregowanego elementu.

- Wewnętrznie w obiektach domeny, należy podnieść zdarzenia domeny podczas wykonywania transakcji, ale jest to niewidoczne z punktu widzenia procedury obsługi polecenia.

- Jeśli wynik operacji agregacji zakończy się pomyślnie i po zakończeniu transakcji, zgłoś zdarzenia integracji. (Mogą one być również zgłaszane przez klasy infrastruktury, takie jak repozytoria).

#### <a name="additional-resources"></a>Zasoby dodatkowe

- **Oznacz Seemann. W granicach aplikacje nie są zorientowane obiektowo** \
  <https://blog.ploeh.dk/2011/05/31/AttheBoundaries,ApplicationsareNotObject-Oriented/>

- **Polecenia i zdarzenia** \
  <https://cqrs.nu/Faq/commands-and-events>

- **Do czego służy procedura obsługi poleceń?** \
  <https://cqrs.nu/Faq/command-handlers>

- **Jimmy Bogard. Wzorce poleceń domeny — programy obsługi** \
  <https://jimmybogard.com/domain-command-patterns-handlers/>

- **Jimmy Bogard. Wzorce poleceń domeny — Walidacja** \
  <https://jimmybogard.com/domain-command-patterns-validation/>

## <a name="the-command-process-pipeline-how-to-trigger-a-command-handler"></a>Potok procesu polecenia: jak wyzwolić procedurę obsługi polecenia

Następnym pytaniem jest wywołanie procedury obsługi polecenia. Można go ręcznie wywołać z każdego powiązanego kontrolera ASP.NET Core. Jednak takie podejście byłoby zbyt sprzężone i nie jest idealnym rozwiązaniem.

Pozostałe dwie główne opcje, które są zalecanymi opcjami, to:

- Za poorednictwem artefaktu wzorca mediator w pamięci.

- Z asynchronicznej kolejki komunikatów, między kontrolerami i obsługą.

### <a name="use-the-mediator-pattern-in-memory-in-the-command-pipeline"></a>Używanie wzorca mediator (w pamięci) w potoku poleceń

Jak pokazano na rysunku 7-25, w podejściu CQRS można użyć inteligentnego mediator, podobnego do magistrali w pamięci, która jest wystarczająco inteligentna, aby przekierować do prawej obsługi poleceń na podstawie typu polecenia lub DTO. Pojedyncze czarne strzałki między składnikami reprezentują zależności między obiektami (w wielu przypadkach, które są wprowadzane przez DI) wraz z ich powiązaniami.

![Diagram przedstawiający bardziej szczegółowy przepływ danych z klienta do bazy danych.](./media/microservice-application-layer-implementation-web-api/mediator-cqrs-microservice.png)

**Rysunek 7-25**. Używanie wzorca mediator w procesie w jednej mikrousłudze CQRS

Na powyższym diagramie przedstawiono powiększenie z obrazu 7-24: kontroler ASP.NET Core wysyła polecenie do potoku poleceń MediatR, dzięki czemu uzyskuje się do odpowiedniej procedury obsługi.

Przyczyną użycia wzorca mediator jest to, że w aplikacjach dla przedsiębiorstw żądania przetwarzania mogą być skomplikowane. Chcesz mieć możliwość dodawania otwartej liczby zagadnień związanych z wycinaniem, takich jak rejestrowanie, walidacje, Inspekcja i zabezpieczenia. W takich przypadkach można polegać na potoku mediator (zobacz [wzorzec mediator](https://en.wikipedia.org/wiki/Mediator_pattern)), aby zapewnić możliwość wykonania tych dodatkowych zachowań lub obaw związanych z wycinaniem.

Mediator to obiekt, który hermetyzuje "jak" tego procesu: koordynuje wykonywanie w oparciu o stan, sposób wywoływania obsługi poleceń lub ładunek, który jest udostępniany do obsługi. Za pomocą składnika mediator można zastosować problemy z wycinaniem i w sposób przejrzysty, stosując dekoratory (lub [zachowania potoku](https://github.com/jbogard/MediatR/wiki/Behaviors) od [MediatR 3](https://www.nuget.org/packages/MediatR/3.0.0)). Aby uzyskać więcej informacji, zobacz [wzorzec dekoratora](https://en.wikipedia.org/wiki/Decorator_pattern).

Dekoratory i zachowania są podobne do [programowania zorientowanego na proporcje (AOP)](https://en.wikipedia.org/wiki/Aspect-oriented_programming), stosowane tylko do określonego potoku procesu zarządzanego przez składnik mediator. Aspekty w AOP, które implementują zagadnienia dotyczące krzyżowego stosowania, są stosowane na podstawie *splotów aspektów* wprowadzonych w czasie kompilacji lub w oparciu o przechwycenie wywołania obiektu. Obydwie typowe podejścia AOP są czasami nazywane "jak Magic", ponieważ nie jest to łatwe do sprawdzenia, jak AOP działa. W przypadku poważnych problemów lub usterek AOP może być trudne do debugowania. Z drugiej strony te dekoratory/zachowania są jawne i stosowane tylko w kontekście mediator, dlatego debugowanie jest znacznie bardziej przewidywalne i łatwe.

Na przykład w mikrousłudze porządkowania eShopOnContainers ma implementację dwóch przykładowych zachowań, klasy [LogBehavior](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Behaviors/LoggingBehavior.cs) i klasy [ValidatorBehavior](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Behaviors/ValidatorBehavior.cs) . Implementacja zachowań została omówiona w następnej sekcji, pokazując sposób, w jaki eShopOnContainers używa zachowań [MediatR](https://www.nuget.org/packages/MediatR) [behaviors](https://github.com/jbogard/MediatR/wiki/Behaviors).

### <a name="use-message-queues-out-of-proc-in-the-commands-pipeline"></a>Używanie kolejek komunikatów (out-of-proc) w potoku polecenia

Kolejną opcją jest użycie komunikatów asynchronicznych opartych na brokerach lub kolejkach komunikatów, jak pokazano na rysunku 7-26. Tę opcję można również połączyć ze składnikiem mediator bezpośrednio przed programem obsługi poleceń.

![Diagram przedstawiający przepływu danych przy użyciu kolejki komunikatów o dużej dostępności.](./media/microservice-application-layer-implementation-web-api/add-ha-message-queue.png)

**Rysunek 7-26**. Korzystanie z kolejek komunikatów (poza procesem i komunikacją między procesami) za pomocą poleceń CQRS

Potok poleceń może być również obsługiwany przez kolejkę komunikatów o wysokiej dostępności w celu dostarczenia poleceń do odpowiedniej procedury obsługi. Użycie kolejek komunikatów do akceptowania poleceń może dodatkowo zawęzić potoku poleceń, ponieważ prawdopodobnie trzeba będzie podzielić potok na dwa procesy połączone za pośrednictwem zewnętrznej kolejki komunikatów. Nadal powinien być używany, jeśli trzeba zwiększyć skalowalność i wydajność na podstawie asynchronicznych komunikatów. Należy wziąć pod uwagę, że w przypadku rysunku 7-26 kontroler po prostu przesyła komunikat polecenia do kolejki i zwraca. Następnie programy obsługi poleceń przetwarzają komunikaty we własnym tempie. Jest to świetna korzyść dla kolejek: Kolejka komunikatów może działać jako bufor w przypadkach, gdy wymagana jest skalowalność funkcji Hyper-, na przykład w przypadku zasobów lub dowolnego innego scenariusza z dużą ilością danych wejściowych.

Jednak ze względu na asynchroniczny charakter kolejek komunikatów należy dowiedzieć się, jak komunikować się z aplikacją kliencką dotyczącą sukcesu lub niepowodzenia procesu polecenia. Jako regułę nie należy nigdy używać poleceń "Fire i zapomnij". Każda aplikacja biznesowa musi wiedzieć, czy polecenie zostało przetworzone pomyślnie, czy co najmniej zweryfikowane i zaakceptowane.

W związku z tym, możliwość odpowiedzi na klienta po zweryfikowaniu komunikatu polecenia, który został przesłany do kolejki asynchronicznej, dodaje złożoność systemu w porównaniu do procesu polecenia w procesie, który zwraca wynik operacji po uruchomieniu transakcji. Korzystając z kolejek, może być konieczne zwrócenie wyniku procesu polecenia przez inne komunikaty wynikowe operacji, które będą wymagały dodatkowych składników i niestandardowej komunikacji w systemie.

Ponadto polecenia asynchroniczne są poleceniami jednokierunkowymi, które w wielu przypadkach mogą nie być konieczne, jak wyjaśniono w następującej interesującej wymianie między Burtsev Alexey i Gregem młodych w [konwersacji online](https://groups.google.com/forum/#!msg/dddcqrs/xhJHVxDx2pM/WP9qP8ifYCwJ):

> \[Burtsev Alexey \] mogę znaleźć wiele kodów, w których ludzie wykorzystują obsługę poleceń asynchronicznych lub jednokierunkową obsługę komunikatów z poleceniami bez żadnych powodów (nie wykonują długotrwałej operacji, nie wykonują zewnętrznych kodów asynchronicznych, ale nie wykonują nawet granicy między aplikacjami, aby korzystać z magistrali komunikatów). Dlaczego wprowadzają tę niezbędną złożoność? W rzeczywistości nie widzę przykładu kodu CQRS z programami obsługi poleceń blokujących do tej pory, chociaż będzie ona działać tylko w większości przypadków.
>
> \[Greg Young \] \[ ... \] polecenie asynchroniczne nie istnieje; jest to inne zdarzenie. Jeśli muszę zaakceptować to, co wysłałeś, i zgłosić wydarzenie, jeśli nie, już nie wiesz, jak to zrobić, to \[ nie jest polecenie \] . Poinformujemy Cię o tym, że coś zostało już zrobione. Wydaje się to bardzo niewielką różnicą w pierwszej kolejności, ale ma wiele konsekwencji.

Asynchroniczne polecenia znacznie zwiększają złożoność systemu, ponieważ nie ma prostego sposobu wskazywania niepowodzeń. W związku z tym polecenia asynchroniczne nie są zalecane, niż w przypadku gdy wymagania dotyczące skalowania są wymagane lub w szczególnych przypadkach podczas komunikacji mikrousług wewnętrznych przy użyciu komunikatów. W takich przypadkach należy zaprojektować oddzielny system raportowania i odzyskiwania pod kątem błędów.

W początkowej wersji programu eShopOnContainers podjęto decyzję o użyciu przetwarzania polecenia synchronicznego, uruchomione z żądań HTTP i przez wzorzec mediator. Dzięki temu można łatwo zwrócić sukces lub niepowodzenie procesu, tak jak w implementacji [CreateOrderCommandHandler](https://github.com/dotnet-architecture/eShopOnContainers/blob/netcore1.1/src/Services/Ordering/Ordering.API/Application/Commands/CreateOrderCommandHandler.cs) .

W każdym przypadku powinna to być decyzja oparta na wymaganiach firmy aplikacji lub mikrousług.

## <a name="implement-the-command-process-pipeline-with-a-mediator-pattern-mediatr"></a>Implementowanie potoku procesu polecenia za pomocą wzorca mediator (MediatR)

W ramach przykładowej implementacji ten przewodnik proponuje użycie potoku w procesie opartym na wzorcu mediator w celu kierowania poleceń związanych z pozyskiwaniem poleceń i trasą w pamięci do odpowiednich programów obsługi poleceń. W przewodniku zawarto również zaproponować stosowanie [zachowań](https://github.com/jbogard/MediatR/wiki/Behaviors) w celu oddzielenia problemów związanych z rozcinaniem.

W przypadku implementacji w programie .NET Core istnieje wiele dostępnych bibliotek typu "open source", które implementują wzorzec mediator. Biblioteka użyta w tym przewodniku jest biblioteką Open Source [MediatR](https://github.com/jbogard/MediatR) (utworzoną przez Jimmy Bogard), ale można użyć innej metody. MediatR to mała i prosta biblioteka, która umożliwia przetwarzanie komunikatów znajdujących się w pamięci, takich jak polecenie, podczas stosowania dekoratory lub zachowań.

Użycie wzorca mediator pomaga zredukować sprzężenie i odizolować problemy związane z zażądaną pracy, podczas gdy automatycznie nawiązuje połączenie z programem obsługi, który wykonuje tę działania — w tym przypadku do obsługi poleceń.

Kolejną dobrą przyczyną użycia wzorca mediator został wyjaśniony przez Jimmy Bogard podczas przeglądania tego przewodnika:

> Uważam, że w tym miejscu może być warto wspominać o testowaniu — zapewnia to spójne okno do zachowania systemu. Żądanie żądania. Wiemy, że aspekt jest całkiem cenny w tworzeniu spójnych testów.

Najpierw przyjrzyjmy się przykładowym kontrolerowi WebAPI, w którym faktycznie będzie używany obiekt mediator. Jeśli nie korzystasz z obiektu mediator, musisz wstrzyknąć wszystkie zależności dla tego kontrolera, takie jak obiekt rejestratora i inne. W związku z tym Konstruktor zostałby skomplikowany. Z drugiej strony, jeśli używasz obiektu mediator, Konstruktor kontrolera może być znacznie prostszy, z zaledwie kilkoma zależnościami, a nie z wieloma zależnościami, jeśli istniała jedna dla operacji wycinania, jak w poniższym przykładzie:

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

Można zobaczyć, że mediator zapewnia czysty i oszczędny Konstruktor kontrolera interfejsu API sieci Web. Ponadto w ramach metod kontrolera kod wysyłający polecenie do obiektu mediator jest niemal jeden wiersz:

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

### <a name="implement-idempotent-commands"></a>Implementowanie poleceń idempotentne

W **eShopOnContainers**, bardziej zaawansowany przykład niż powyżej, przesyła obiekt CreateOrderCommand z mikrousługi porządkowania. Jednak ponieważ proces biznesowy porządkowania jest nieco bardziej skomplikowany i, w naszym przypadku, faktycznie zaczyna się w mikrousłudze koszyka, ta akcja przesyłania obiektu CreateOrderCommand jest wykonywana z programu obsługi zdarzeń integracji o nazwie [UserCheckoutAcceptedIntegrationEventHandler](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/IntegrationEvents/EventHandling/UserCheckoutAcceptedIntegrationEventHandler.cs) zamiast prostego kontrolera WebAPI wywołana z poziomu aplikacji klienckiej, jak w poprzednim, prostszym przykładzie.

Niemniej jednak akcja przesłania polecenia do MediatR jest bardzo podobna, jak pokazano w poniższym kodzie.

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

Jednak ten przypadek jest również nieco bardziej zaawansowany, ponieważ implementujemy również polecenia idempotentne. Proces CreateOrderCommand powinien mieć wartość idempotentne, więc jeśli ten sam komunikat jest zduplikowany za pomocą sieci, ze względu na to, co się dzieje, takie samo zamówienie jest przetwarzane tylko raz.

Jest to implementowane przez zapakowanie polecenia biznesowego (w tym przypadku CreateOrderCommand) i osadzenie go w ogólnym IdentifiedCommand, który jest śledzony przez identyfikator każdej wiadomości przechodzącej przez sieć, która musi być idempotentne.

W poniższym kodzie można zobaczyć, że IdentifiedCommand nie ma więcej niż DTO z i ID oraz zawiniętego obiektu polecenia biznesowego.

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

Następnie CommandHandler — obiekt dla IdentifiedCommand o nazwie [IdentifiedCommandHandler.cs](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Commands/IdentifiedCommandHandler.cs) będzie w istocie sprawdzać, czy identyfikator, który jest częścią komunikatu, już istnieje w tabeli. Jeśli już istnieje, to polecenie nie zostanie przetworzone ponownie, dlatego działa jako polecenie idempotentne. Ten kod infrastruktury jest wykonywany przez `_requestManager.ExistAsync` wywołanie metody poniżej.

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

Ponieważ IdentifiedCommand działa podobnie jak forma polecenia biznesowego, gdy trzeba przetworzyć polecenie biznesowe, ponieważ nie jest to powtórzony identyfikator, to wykonuje to wewnętrzne polecenie biznesowe i ponownie przesyła je do mediator, jak w ostatniej części kodu pokazanego powyżej podczas uruchamiania `_mediator.Send(message.Command)` , z [IdentifiedCommandHandler.cs](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Commands/IdentifiedCommandHandler.cs).

W takim przypadku spowoduje to połączenie i uruchomienie programu obsługi poleceń firmy, w tym przypadku [CreateOrderCommandHandler](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Commands/CreateOrderCommandHandler.cs), w którym są uruchomione transakcje względem bazy danych porządkowania, jak pokazano w poniższym kodzie.

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

### <a name="register-the-types-used-by-mediatr"></a>Rejestrowanie typów używanych przez MediatR

Aby MediatR był świadomy klas programu obsługi poleceń, należy zarejestrować klasy mediator i klasy obsługi poleceń w kontenerze IoC. Domyślnie MediatR używa Autofac jako kontenera IoC, ale można również użyć wbudowanego kontenera ASP.NET Core IoC lub innego kontenera obsługiwanego przez MediatR.

Poniższy kod przedstawia sposób rejestrowania typów i poleceń mediator w przypadku korzystania z modułów Autofac.

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

Jest to miejsce, w którym występuje "Magic" z MediatR.

Ponieważ każdy program obsługi poleceń implementuje `IRequestHandler<T>` interfejs ogólny, po zarejestrowaniu zestawów przy użyciu `RegisteredAssemblyTypes` metody wszystkie typy oznaczone jako `IRequestHandler` również są rejestrowane z ich użyciem `Commands` . Na przykład:

```csharp
public class CreateOrderCommandHandler
  : IRequestHandler<CreateOrderCommand, bool>
{
```

Jest to kod, który służy do skorelowania poleceń z programami obsługi poleceń. Procedura obsługi jest tylko prostą klasą, ale dziedziczy z `RequestHandler<T>` , gdzie T jest typem polecenia, a MediatR sprawdza, czy jest wywoływana z prawidłowym ładunkiem (polecenie).

## <a name="apply-cross-cutting-concerns-when-processing-commands-with-the-behaviors-in-mediatr"></a>Stosuj problemy z wycinaniem podczas przetwarzania poleceń za pomocą zachowań w MediatR

Istnieje jeszcze jeden element: możliwość zastosowania zagadnień związanych z wycinaniem do potoku mediator. Na końcu kodu modułu rejestracji Autofac można także sprawdzić, w jaki sposób rejestruje typ zachowania, w tym w przypadku niestandardowej klasy LoggingBehavior i klasy ValidatorBehavior. Można jednak również dodać inne niestandardowe zachowania.

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

Tę klasę [LoggingBehavior](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Behaviors/LoggingBehavior.cs) można zaimplementować jako następujący kod, który rejestruje informacje o wykonywanej obsłudze poleceń i o tym, czy zakończyły się powodzeniem, czy nie.

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

Po prostu implementując tę klasę zachowań i rejestrując ją w potoku (w MediatorModule powyżej) wszystkie polecenia przetworzone przez MediatR będą rejestrować informacje o wykonaniu.

Mikrousługa porządkowania eShopOnContainers stosuje również drugie zachowanie dla podstawowych walidacji, Klasa [ValidatorBehavior](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Behaviors/ValidatorBehavior.cs) , która opiera się na bibliotece [FluentValidation](https://github.com/JeremySkinner/FluentValidation) , jak pokazano w poniższym kodzie:

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

W tym miejscu zachowanie wywołuje wyjątek, jeśli Walidacja nie powiedzie się, ale można również zwrócić obiekt wynikowy, zawierający wynik polecenia, jeśli zakończyło się powodzeniem lub komunikat sprawdzania poprawności w przypadku niepowodzenia. Prawdopodobnie ułatwi to wyświetlanie wyników walidacji dla użytkownika.

Następnie na podstawie biblioteki [FluentValidation](https://github.com/JeremySkinner/FluentValidation) należy utworzyć weryfikację danych przesłanych z CreateOrderCommand, jak w poniższym kodzie:

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

Można utworzyć dodatkowe walidacje. Jest to bardzo czysty i elegancki sposób implementacji walidacji poleceń.

W podobny sposób można zaimplementować inne zachowania dla dodatkowych aspektów lub obaw związanych z wycinaniem, które mają być stosowane do poleceń podczas ich obsługi.

#### <a name="additional-resources"></a>Zasoby dodatkowe

##### <a name="the-mediator-pattern"></a>Wzorzec mediator

- **Wzorzec mediator** \
  [https://en.wikipedia.org/wiki/Mediator\_pattern](https://en.wikipedia.org/wiki/Mediator_pattern)

##### <a name="the-decorator-pattern"></a>Wzorzec Dekoratora

- **Wzorzec Dekoratora** \
  [https://en.wikipedia.org/wiki/Decorator\_pattern](https://en.wikipedia.org/wiki/Decorator_pattern)

##### <a name="mediatr-jimmy-bogard"></a>MediatR (Jimmy Bogard)

- **MediatR.** Repozytorium GitHub. \
  <https://github.com/jbogard/MediatR>

- **CQRS z MediatR i automapowaniem** \
  <https://lostechies.com/jimmybogard/2015/05/05/cqrs-with-mediatr-and-automapper/>

- **Umieść swoje kontrolery według pokarmu: wpisów i poleceń.** \
  <https://lostechies.com/jimmybogard/2013/12/19/put-your-controllers-on-a-diet-posts-and-commands/>

- **Rozwiązywanie problemów z rozcinaniem przy użyciu potoku mediator** \
  <https://lostechies.com/jimmybogard/2014/09/09/tackling-cross-cutting-concerns-with-a-mediator-pipeline/>

- **CQRS i REST: idealne dopasowanie** \
  <https://lostechies.com/jimmybogard/2016/06/01/cqrs-and-rest-the-perfect-match/>

- **Przykłady potoku MediatR** \
  <https://lostechies.com/jimmybogard/2016/10/13/mediatr-pipeline-examples/>

- **Armatura testu wycinka pionowego dla MediatR i ASP.NET Core** \
  <https://lostechies.com/jimmybogard/2016/10/24/vertical-slice-test-fixtures-for-mediatr-and-asp-net-core/>

- **Wydano rozszerzenia MediatR dla iniekcji zależności firmy Microsoft** \
  <https://lostechies.com/jimmybogard/2016/07/19/mediatr-extensions-for-microsoft-dependency-injection-released/>

##### <a name="fluent-validation"></a>Weryfikacja w programie Fluent

- **Jeremy Skinner. FluentValidation.** Repozytorium GitHub. \
  <https://github.com/JeremySkinner/FluentValidation>

> [!div class="step-by-step"]
> [Poprzedni](microservice-application-layer-web-api-design.md) 
>  [Dalej](../implement-resilient-applications/index.md)
