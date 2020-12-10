---
title: Opracowywanie aplikacji ASP.NET Core MVC
description: Tworzenie architektury nowoczesnych aplikacji sieci Web przy użyciu ASP.NET Core i platformy Azure | opracowywanie aplikacji ASP.NET Core MVC
author: ardalis
ms.author: wiwagn
ms.date: 12/01/2020
no-loc:
- Blazor
- WebAssembly
ms.openlocfilehash: c0fc92b2dbc25a1a48e0264b64c79fc8631fa8f0
ms.sourcegitcommit: 81f1bba2c97a67b5ca76bcc57b37333ffca60c7b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/10/2020
ms.locfileid: "97009667"
---
# <a name="develop-aspnet-core-mvc-apps"></a>Opracowywanie aplikacji ASP.NET Core MVC

> "Nie jest ważne, aby pobrać go po raz pierwszy. Bardzo ważne jest, aby uzyskać je po raz ostatni. "
> _— Andrew polowa i David Thomas_

ASP.NET Core to międzyplatformowa platforma typu "open source" służąca do tworzenia nowoczesnych aplikacji sieci Web zoptymalizowanych pod kątem chmury. Aplikacje ASP.NET Core są lekkie i modularne, dzięki wbudowanej obsłudze iniekcji zależności, co pozwala zwiększyć możliwości testowania i utrzymania. W połączeniu z platformą MVC, która obsługuje tworzenie nowoczesnych interfejsów API sieci Web oprócz aplikacji opartych na widoku, ASP.NET Core to zaawansowana platforma, w której można tworzyć aplikacje sieci Web dla przedsiębiorstw.

## <a name="mvc-and-razor-pages"></a>MVC i Razor Pages

ASP.NET Core MVC oferuje wiele funkcji, które są przydatne do tworzenia interfejsów API i aplikacji opartych na sieci Web. Termin MVC oznacza "Model-View-Controller", wzorzec interfejsu użytkownika, który dzieli obowiązki odpowiedzi na żądania użytkowników do kilku części. Oprócz tego wzorca można także zaimplementować funkcje w ASP.NET Core aplikacji jako Razor Pages. Razor Pages są wbudowane w ASP.NET Core MVC i używają tych samych funkcji routingu, powiązania modelu, filtrów, autoryzacji itp. Jednak zamiast oddzielnych folderów i plików dla kontrolerów, modeli, widoków itp. i używania routingu opartego na atrybutach Razor Pages są umieszczane w pojedynczym folderze ("/Pages"), trasie na podstawie ich lokalizacji względnej w tym folderze i obsługi żądań z obsługą, a nie akcją kontrolera. W związku z tym podczas pracy z Razor Pages wszystkie potrzebne pliki i klasy są zwykle współzlokalizowane, a nie rozłożone w całym projekcie sieci Web.

Podczas tworzenia nowej aplikacji ASP.NET Core należy mieć plan na uwadze dla rodzaju aplikacji, którą chcesz skompilować. W programie Visual Studio będziesz wybierać spośród kilku szablonów. Trzy najpopularniejsze szablony projektów to Web API, aplikacja sieci Web i aplikacja sieci Web (Model-View-Controller). Chociaż tę decyzję można podjąć tylko podczas pierwszego tworzenia projektu, nie jest to nieodwołalna decyzja. Projekt interfejsu API sieci Web używa standardowych kontrolerów kontrolera widoku modelu — tylko domyślnie nie ma widoków. Podobnie szablon domyślnej aplikacji sieci Web używa Razor Pages, a zatem nie ma folderu widoki. Możesz później dodać folder widoki do tych projektów, aby obsługiwać zachowanie oparte na widoku. Projekty Web API i Model-View-Controller nie zawierają domyślnie folderu Pages, ale można je później dodać do obsługi zachowania opartego na Razor Pages. Te trzy szablony można traktować jako obsługujące trzy różne rodzaje domyślnej interakcji użytkownika: dane (internetowy interfejs API), oparte na stronach i widoku. Można jednak mieszać i dopasować dowolne lub wszystkie z tych szablonów w ramach pojedynczego projektu, jeśli chcesz.

### <a name="why-razor-pages"></a>Dlaczego Razor Pages?

Razor Pages to domyślne podejście do nowych aplikacji sieci Web w programie Visual Studio. Razor Pages oferuje prostszy sposób tworzenia funkcji aplikacji opartych na stronach, takich jak formularze niespa. Korzystanie z kontrolerów i widoków było powszechne dla aplikacji, które mają bardzo duże kontrolery, które pracowały z wieloma różnymi zależnościami, i wyświetlają wiele różnych widoków. Spowodowało to zwiększenie złożoności i często wynika z tego, że kontrolery, które nie były zgodne z pojedynczą zasadą odpowiedzialności lub zasady otwarte/zamknięte w praktyce. Razor Pages rozwiązuje ten problem przez hermetyzację logiki po stronie serwera dla danej logicznej "strony" w aplikacji sieci Web z oznaczeniem Razor. Strona Razor, która nie ma logiki po stronie serwera, może składać się tylko z pliku Razor (na przykład "index. cshtml"). Jednak większość nieuproszczonych Razor Pages będzie miała skojarzoną klasę modelu strony, która jest taka sama jak nazwa pliku Razor z rozszerzeniem ". cs" (na przykład "Index.cshtml.cs").

Model strony strony Razor łączy obowiązki kontrolera MVC i ViewModel. Zamiast obsługi żądań z metodami akcji kontrolera, programy obsługi modelu strony, takie jak "OnGet ()", są wykonywane, domyślnie renderuje ich skojarzone strony. Razor Pages upraszcza proces kompilowania poszczególnych stron w aplikacji ASP.NET Core, zapewniając jednocześnie wszystkie funkcje architektury ASP.NET Core MVC. Są to dobry wybór domyślny dla nowych funkcji opartych na stronach.

### <a name="when-to-use-mvc"></a>Kiedy używać MVC

Jeśli tworzysz interfejsy API sieci Web, wzorzec MVC staje się bardziej zrozumiały niż próba użycia Razor Pages. Jeśli projekt będzie uwidaczniał wyłącznie punkty końcowe interfejsu API sieci Web, należy najlepiej zacząć od szablonu projektu interfejsu API sieci Web. W przeciwnym razie można łatwo dodać kontrolery i skojarzone punkty końcowe interfejsu API do dowolnej aplikacji ASP.NET Core. Użyj podejścia MVC opartego na widokach w przypadku migrowania istniejącej aplikacji z ASP.NET MVC 5 lub starszej do ASP.NET Core MVC i chcesz to zrobić z mniejszą ilością nakładu pracy. Po przeprowadzeniu migracji wstępnej można sprawdzić, czy ma to na celu przyjęcie Razor Pages nowych funkcji, a nawet w przypadku migracji hurtowej.

Niezależnie od tego, czy wybierzesz kompilację aplikacji sieci Web przy użyciu widoków Razor Pages lub MVC, aplikacja będzie miała podobną wydajność i będzie obejmować obsługę iniekcji zależności, filtrów, powiązań modelu, walidacji itd.

## <a name="mapping-requests-to-responses"></a>Mapowanie żądań na odpowiedzi

W swoich serca ASP.NET Core aplikacje mapują przychodzące żądania na odpowiedzi wychodzące. Na niskim poziomie to mapowanie odbywa się przy użyciu oprogramowania pośredniczącego, a proste aplikacje i mikrousługi ASP.NET Core mogą obejmować wyłącznie niestandardowe oprogramowanie pośredniczące. W przypadku korzystania z ASP.NET Core MVC można korzystać na nieco wyższym poziomie, zastanawiając się pod względem _tras_, _kontrolerów_ i _akcji_. Każde żądanie przychodzące jest porównywane z tabelą routingu aplikacji. w przypadku znalezienia zgodnej trasy zostanie wywołana skojarzona Metoda akcji (należącej do kontrolera) do obsługi żądania. Jeśli nie zostanie znaleziona zgodna trasa, zostanie wywołana procedura obsługi błędów (w tym przypadku zwracająca wynik NotFound).

Aplikacje ASP.NET Core MVC mogą używać tras konwencjonalnych, tras atrybutów lub obu. Trasy konwencjonalne są zdefiniowane w kodzie, określając _konwencje_ routingu przy użyciu składni podobnej do poniższego przykładu:

```csharp
app.UseEndpoints(endpoints =>
{
    endpoints.MapControllerRoute(name: "default", pattern: "{controller=Home}/{action=Index}/{id?}");
});
```

W tym przykładzie trasa o nazwie "default" została dodana do tabeli routingu. Definiuje szablon trasy z symbolami zastępczymi dla `controller` , `action` i `id` . `controller` `action` Symbole zastępcze i mają domyślnie określony ( `Home` i `Index` , odpowiednio), a `id` symbol zastępczy jest opcjonalny (na przykład "?"). W ramach Konwencji zdefiniowanej tutaj należy określić, że pierwsza część żądania powinna odpowiadać nazwie kontrolera, drugiej części akcji, a następnie, jeśli to konieczne, trzecia część będzie reprezentować parametr ID. Trasy konwencjonalne są zwykle definiowane w jednym miejscu dla aplikacji, na przykład w `Configure` metodzie `Startup` klasy.

Trasy atrybutów są stosowane bezpośrednio do kontrolerów i akcji, a nie do określonych globalnie. Takie podejście ma znacznie większą możliwość odnajdywania, gdy przeglądasz określoną metodę, ale oznacza to, że informacje o routingu nie są przechowywane w jednym miejscu w aplikacji. Korzystając z tras atrybutów, można łatwo określić wiele tras dla danej akcji, a także połączyć trasy między kontrolerami i akcjami. Przykład:

```csharp
[Route("Home")]
public class HomeController : Controller
{
    [Route("")] // Combines to define the route template "Home"
    [Route("Index")] // Combines to define route template "Home/Index"
    [Route("/")] // Does not combine, defines the route template ""
    public IActionResult Index() {}
}
```

Trasy można określić w [narzędzia HttpGet] i podobnych atrybutach, unikając konieczności dodawania oddzielnych atrybutów [Route]. Trasy atrybutu mogą również używać tokenów, aby ograniczyć potrzebę powtarzania nazw kontrolerów lub akcji, jak pokazano poniżej:

```csharp
[Route("[controller]")]
public class ProductsController : Controller
{
    [Route("")] // Matches 'Products'
    [Route("Index")] // Matches 'Products/Index'
    public IActionResult Index() {}
}
```

Razor Pages nie używa routingu atrybutów. Jako część swojej dyrektywy można określić dodatkowe informacje o szablonie trasy dla strony Razor `@page` :

```csharp
@page "{id:int}"
```

W poprzednim przykładzie dana strona będzie pasowała do trasy z `id` parametrem Integer. Na przykład strona *Products. cshtml* znajdująca się w folderze głównym `/Pages` ma następującą trasę:

```csharp
"/Products/123"
```

Po dopasowaniu danego żądania do trasy, ale przed wywołaniem metody akcji, ASP.NET Core MVC będzie wykonywał [powiązania modelu](/aspnet/core/mvc/models/model-binding) i [Sprawdzanie poprawności modelu](/aspnet/core/mvc/models/validation) na żądanie. Powiązanie modelu jest odpowiedzialne za konwertowanie przychodzących danych HTTP na typy .NET określone jako parametry metody akcji, która ma zostać wywołana. Na przykład jeśli metoda akcja oczekuje `int id` parametru, powiązanie modelu podejmie próbę podania tego parametru z wartości dostarczonej jako część żądania. W tym celu powiązanie modelu wyszukuje wartości w opublikowanym formularzu, wartości w samej trasie i wartości ciągu zapytania. Przy założeniu `id` , że wartość zostanie znaleziona, zostanie przekonwertowana na liczbę całkowitą przed przekazaniem do metody akcji.

Po powiązaniu modelu, ale przed wywołaniem metody akcji, następuje Walidacja modelu. Walidacja modelu używa opcjonalnych atrybutów dla typu modelu i może pomóc zapewnić, że udostępniony obiekt modelu spełnia określone wymagania dotyczące danych. Niektóre wartości mogą być określone jako wymagane lub ograniczone do określonej długości lub zakresu liczbowego itd. Jeśli określono atrybuty walidacji, ale model nie spełnia wymagań, właściwość ModelState. IsValid ma wartość false, a zestaw reguł walidacji z błędami będzie dostępny do wysłania do klienta wysyłającego żądanie.

W przypadku korzystania z walidacji modelu należy zawsze sprawdzić, czy model jest prawidłowy przed wykonaniem jakichkolwiek poleceń zmiany stanu, aby upewnić się, że aplikacja nie jest uszkodzona przez nieprawidłowe dane. Możesz użyć [filtru](/aspnet/core/mvc/controllers/filters) , aby uniknąć konieczności dodawania kodu dla tej walidacji w każdej akcji. ASP.NET Core filtry MVC oferują sposób przechwytywania grup żądań, dzięki czemu można zastosować typowe zasady i zagadnienia dotyczące krzyżowego rozliczania. Filtry mogą być stosowane do poszczególnych akcji, całych kontrolerów lub globalnie dla aplikacji.

W przypadku interfejsów API sieci Web ASP.NET Core MVC obsługuje [_negocjowanie zawartości_](/aspnet/core/mvc/models/formatting), umożliwiając żądanie określenia sposobu formatowania odpowiedzi. W oparciu o nagłówki podane w żądaniu akcje zwracające dane spowodują sformatowanie odpowiedzi w formacie XML, JSON lub innym obsługiwanym formacie. Ta funkcja umożliwia korzystanie z tego samego interfejsu API przez wielu klientów z różnymi wymaganiami dotyczącymi formatu danych.

Projekty interfejsu API sieci Web należy rozważyć przy użyciu `[ApiController]` atrybutu, który można zastosować do poszczególnych kontrolerów, do podstawowej klasy kontrolera lub do całego zestawu. Ten atrybut dodaje Automatyczne sprawdzanie poprawności modelu, a każda akcja z nieprawidłowym modelem zwróci nieprawidłowego żądania z informacjami o błędach walidacji. Ten atrybut wymaga również, aby wszystkie akcje miały atrybut trasy, zamiast używać trasy konwencjonalnej i zwracają bardziej szczegółowe informacje ProblemDetails w odpowiedzi na błędy.

### <a name="keeping-controllers-under-control"></a>Utrzymywanie kontrolerów pod kontrolą

W przypadku aplikacji opartych na stronach Razor Pages wykonać doskonałe zadanie utrzymywania zbyt dużej liczby kontrolerów. Każda Strona otrzymuje własne pliki i klasy, które są przeznaczone tylko dla jego programów obsługi. Przed wprowadzeniem Razor Pages wiele aplikacji zorientowanych na widok będzie miała duże klasy kontrolerów odpowiedzialne za wiele różnych akcji i widoków. Te klasy byłyby naturalnie rosnące w celu posiadania wielu obowiązków i zależności, co utrudnia ich konserwację. Jeśli okaże się, że Twoje kontrolery widoków są zbyt duże, rozważ ich refaktoryzację do użycia Razor Pages lub wprowadzenie wzorca, takiego jak mediator.

Wzorzec projektowy mediator jest używany do zredukowania sprzęgania między klasami, jednocześnie umożliwiając komunikację między nimi. W aplikacjach ASP.NET Core MVC ten wzorzec jest często stosowany do podziału kontrolerów na mniejsze części za pomocą *programów obsługi* w celu wykonywania pracy z metodami akcji. Popularny [pakiet NuGet MediatR](https://www.nuget.org/packages/MediatR/) jest często używany do osiągnięcia tego celu. Zazwyczaj kontrolery obejmują wiele różnych metod akcji, z których każdy może wymagać pewnych zależności. Zestaw wszystkich zależności wymaganych przez dowolną akcję musi być przekazaniem do konstruktora kontrolera. W przypadku korzystania z MediatR jedyną zależnością jest kontroler w wystąpieniu mediator. Każda akcja następnie używa wystąpienia mediator do wysyłania komunikatu, który jest przetwarzany przez procedurę obsługi. Procedura obsługi jest specyficzna dla jednej akcji i w ten sposób wymaga tylko zależności wymaganych przez tę akcję. Przykładem kontrolera korzystającego z MediatR jest następujący:

```csharp
public class OrderController : Controller
{
    private readonly IMediator _mediator;

    public OrderController(IMediator mediator)
    {
        _mediator = mediator;
    }

    [HttpGet]
    public async Task<IActionResult> MyOrders()
    {
        var viewModel = await _mediator.Send(new GetMyOrders(User.Identity.Name));

        return View(viewModel);
    }

    // other actions implemented similarly
}
```

W `MyOrders` akcji wywołanie `Send` `GetMyOrders` komunikatu jest obsługiwane przez tę klasę:

```csharp
public class GetMyOrdersHandler : IRequestHandler<GetMyOrders, IEnumerable<OrderViewModel>>
{
    private readonly IOrderRepository _orderRepository;

    public GetMyOrdersHandler(IOrderRepository orderRepository)
    {
        _orderRepository = orderRepository;
    }

    public async Task<IEnumerable<OrderViewModel>> Handle(GetMyOrders request, CancellationToken cancellationToken)
    {
        var specification = new CustomerOrdersWithItemsSpecification(request.UserName);
        var orders = await _orderRepository.ListAsync(specification);

        return orders.Select(o => new OrderViewModel
        {
            OrderDate = o.OrderDate,
            OrderItems = o.OrderItems?.Select(oi => new OrderItemViewModel()
            {
                PictureUrl = oi.ItemOrdered.PictureUri,
                ProductId = oi.ItemOrdered.CatalogItemId,
                ProductName = oi.ItemOrdered.ProductName,
                UnitPrice = oi.UnitPrice,
                Units = oi.Units
            }).ToList(),
            OrderNumber = o.Id,
            ShippingAddress = o.ShipToAddress,
            Total = o.Total()
        });
    }
}
```

Rezultatem tego podejścia jest to, że kontrolery są znacznie mniejsze i koncentrują się głównie na powiązaniach routingu i modelu, natomiast poszczególne programy obsługi są odpowiedzialne za określone zadania wymagające danego punktu końcowego. Takie podejście można również uzyskać bez MediatR za pomocą [pakietu NuGet ApiEndpoints](https://www.nuget.org/packages/Ardalis.ApiEndpoints/), który próbuje przełączyć się do kontrolerów interfejsu API te same korzyści, Razor Pages są one wbudowane dla kontrolerów opartych na widoku.

> ### <a name="references--mapping-requests-to-responses"></a>References — mapowanie żądań na odpowiedzi
>
> - **Routing do akcji kontrolera**\
 > <https://docs.microsoft.com/aspnet/core/mvc/controllers/routing>
> - **Powiązanie modelu**\
 > <https://docs.microsoft.com/aspnet/core/mvc/models/model-binding>
> - **Walidacja modelu**\
 > <https://docs.microsoft.com/aspnet/core/mvc/models/validation>
> - **Filtry**\
 > <https://docs.microsoft.com/aspnet/core/mvc/controllers/filters>
> - **ApiController — atrybut**\
 > <https://docs.microsoft.com/aspnet/core/web-api/>

## <a name="working-with-dependencies"></a>Praca z zależnościami

ASP.NET Core ma wbudowaną obsługę i wewnętrznie wykorzystuje technikę znaną jako [iniekcja zależności](/aspnet/core/fundamentals/dependency-injection). Wstrzykiwanie zależności to technika, która umożliwia swobodne sprzęganie różnych części aplikacji. Sprzężenie luźne jest pożądane, ponieważ ułatwia izolowanie części aplikacji, co pozwala na testowanie lub zastępowanie. Sprawia również, że zmiana w jednej części aplikacji będzie miała nieoczekiwany wpływ w innym miejscu aplikacji. Iniekcja zależności jest oparta na zasadzie niewersji zależności i jest często kluczem do osiągnięcia zasady otwarte/zamknięte. Podczas oceniania, jak działa Twoja aplikacja wraz z jej zależnościami, należy pamiętać o kodzie [static cling](https://deviq.com/static-cling/) zapachu i pamiętaj, że aphorism "[New to Glue](https://ardalis.com/new-is-glue)".

Statyczne cling występuje, gdy klasy umożliwiają wywoływanie metod statycznych lub dostęp do właściwości statycznych, które mają efekty uboczne lub zależności dotyczące infrastruktury. Na przykład jeśli masz metodę, która wywołuje metodę statyczną, która z kolei zapisuje dane w bazie danych, metoda jest ściśle sprzężona z bazą danych. Wszystkie elementy, które dzielą się tym wywołaniem bazy danych, spowodują uszkodzenie metody. Testowanie takich metod jest trudne, ponieważ takie testy wymagają, aby komercyjne biblioteki do zasymulować wywołania statyczne lub mogły być testowane tylko z testową bazą danych. Wywołania statyczne, które nie mają żadnych zależności względem infrastruktury, szczególnie te, które są całkowicie bezstanowe, są bardzo ważne do wywołania i nie mają wpływu na sprzężenie lub możliwości testowania (poza kodem sprzęgania do samego wywołania statycznego).

Wielu programistów zna ryzyko związane ze statycznym clingm i globalnym stanem, ale nadal ściśle połączy swój kod z określonymi implementacjami za pośrednictwem bezpośredniego tworzenia wystąpienia. "New to Glue" to przypomnienie dotyczące sprzęgu, a nie ogólne Condemnation użycia `new` słowa kluczowego. Podobnie jak w przypadku wywołań metod statycznych, nowe wystąpienia typów, które nie mają zależności zewnętrznych, zazwyczaj nie umożliwiają ścisłego podzielenia kodu na szczegóły implementacji lub sprawiają, że testowanie jest trudniejsze. Ale za każdym razem, gdy Klasa jest tworzona, Poświęć nieco chwilę, aby rozważyć, czy ma to sens, że ma to na celu wyznaczenie, że ma to miejsce w konkretnym miejscu w danej lokalizacji, czy też będzie lepszym rozwiązaniem do żądania tego wystąpienia jako zależności.

### <a name="declare-your-dependencies"></a>Deklarowanie zależności

ASP.NET Core jest oparty na tym, że metody i klasy deklarują swoje zależności, żądając ich jako argumentów. Aplikacje ASP.NET są zwykle konfigurowane w klasie startowej, która jest konfigurowana do obsługi iniekcji zależności w kilku punktach. Jeśli Klasa startowa ma Konstruktor, może zażądać zależności za pomocą konstruktora, tak więc:

```csharp
public class Startup
{
    public Startup(IHostingEnvironment env)
    {
        var builder = new ConfigurationBuilder()
            .SetBasePath(env.ContentRootPath)
            .AddJsonFile("appsettings.json", optional: false, reloadOnChange: true)
            .AddJsonFile($"appsettings.{env.EnvironmentName}.json", optional: true);
    }
}
```

Klasa uruchomieniowa jest interesująca, że nie ma żadnych jawnych wymagań dla tego typu. Nie dziedziczy po specjalnej początkowej klasie bazowej ani nie implementuje żadnego konkretnego interfejsu. Możesz nadać mu konstruktora, a nie, i można określić dowolną liczbę parametrów w konstruktorze. Po uruchomieniu hosta sieci Web, który został skonfigurowany dla aplikacji, zostanie wywołana Klasa startowa, której użyto, i użyje iniekcji zależności do wypełnienia wszelkich zależności wymaganych przez klasę uruchomieniową. Oczywiście, jeśli poprosisz o parametry, które nie są skonfigurowane w kontenerze usług używanym przez ASP.NET Core, otrzymasz wyjątek, ale o ile przejdziesz do zależności, których dotyczy ten kontener, możesz poprosić o dowolne elementy.

Iniekcja zależności jest wbudowana w aplikacje ASP.NET Core bezpośrednio od początku, podczas tworzenia wystąpienia uruchamiania. Nie powoduje zatrzymania klasy startowej. Możesz również zażądać zależności w metodzie konfigurowania:

```csharp
public void Configure(IApplicationBuilder app,
    IHostingEnvironment env,
    ILoggerFactory loggerFactory)
{

}
```

Metoda ConfigureServices to wyjątek dla tego zachowania; musi on mieć tylko jeden parametr typu IServiceCollection. Nie ma potrzeby obsługi iniekcji zależności, ponieważ z jednej strony jest odpowiedzialny za Dodawanie obiektów do kontenera usługi, a w drugiej, ma dostęp do wszystkich aktualnie skonfigurowanych usług za pośrednictwem parametru IServiceCollection. Z tego względu można pracować z zależnościami zdefiniowanymi w kolekcji usług ASP.NET Core Services w każdej części klasy uruchomieniowej, żądając wymaganej usługi jako parametru lub przez pracę z IServiceCollection w ConfigureServices.

> [!NOTE]
> Jeśli musisz upewnić się, że niektóre usługi są dostępne dla klasy startowej, możesz je skonfigurować przy użyciu metody IWebHostBuilder i ConfigureServices w wywołaniu CreateDefaultBuilder.

Klasa startowa to model służący do tworzenia struktury innych części aplikacji ASP.NET Core, od kontrolerów do oprogramowania pośredniczącego, do filtrów do własnych usług. W każdym przypadku należy postępować zgodnie z [zasadami jawnych zależności](https://deviq.com/explicit-dependencies-principle/), żądając zależności, a nie ich bezpośrednio tworzyć i wykorzystując iniekcję zależności w całej aplikacji. Należy zachować ostrożność, gdzie i w jaki sposób bezpośrednio utworzyć wystąpienia implementacji, szczególnie usług i obiektów, które pracują z infrastrukturą, lub mieć skutki uboczne. Preferuj pracę z abstrakcyjnymi definicjami w rdzeńu aplikacji i przekazane jako argumenty do zakodowana odwołań do określonych typów implementacji.

## <a name="structuring-the-application"></a>Tworzenie struktury aplikacji

Aplikacje monolityczne zwykle mają jeden punkt wejścia. W przypadku ASP.NET Core aplikacji sieci Web punkt wejścia będzie ASP.NET Core projekcie sieci Web. Nie oznacza to jednak, że rozwiązanie powinno zawierać tylko jeden projekt. Warto podzielić aplikację na różne warstwy, aby obserwować rozdzielenie problemów. Po podpisaniu na warstwach warto przekroczyć foldery do oddzielnych projektów, co może pomóc w osiągnięciu lepszego hermetyzacji. Najlepszym podejściem do osiągnięcia tych celów za pomocą aplikacji ASP.NET Core jest odmiana czystego architektury omówionego w rozdziale 5. Po tym podejściu rozwiązanie aplikacji będzie obejmować oddzielne biblioteki dla interfejsu użytkownika, infrastruktury i ApplicationCore.

Poza tymi projektami są również dołączone oddzielne projekty testowe (testowanie jest omówione w rozdziale 9).

Model obiektów i interfejsy aplikacji należy umieścić w projekcie ApplicationCore. Ten projekt będzie miał możliwie najmniejszej liczby zależności, a inne projekty w rozwiązaniu będą odwoływać się do niego. Jednostki biznesowe, które muszą być utrwalane, są zdefiniowane w projekcie ApplicationCore, podobnie jak usługi, które nie zależą bezpośrednio od infrastruktury.

Szczegóły implementacji, takie jak trwałość lub sposób wysyłania powiadomień do użytkownika, są przechowywane w projekcie infrastruktury. Ten projekt będzie odwoływać się do pakietów specyficznych dla implementacji, takich jak Entity Framework Core, ale nie powinien ujawniać szczegółowych informacji o tych implementacjach poza projektem. Usługi infrastruktury i repozytoria powinny implementować interfejsy, które są zdefiniowane w projekcie ApplicationCore, a jego implementacje trwałości są odpowiedzialne za pobieranie i przechowywanie jednostek zdefiniowanych w ApplicationCore.

Projekt interfejsu użytkownika ASP.NET Core jest odpowiedzialny za wszelkie wątpliwości dotyczące poziomu interfejsu użytkownika, ale nie powinien obejmować logiki biznesowej ani szczegółów infrastruktury. W rzeczywistości najlepiej nie powinien on mieć zależności od projektu infrastruktury, co pomaga zapewnić, że żadna zależność między tymi dwoma projektami nie zostanie wprowadzona przypadkowo. Można to osiągnąć za pomocą innych kontenerów DI innych firm, takich jak Autofac, co pozwala na definiowanie reguł DI w klasach modułów w każdym projekcie.

Inne podejście do oddzielenia aplikacji od szczegółów implementacji ma na celu wywołanie mikrousług, które mogą być wdrożone w poszczególnych kontenerach platformy Docker. Zapewnia to jeszcze większe rozdzielenie problemów i rozróżnienie niż wykorzystanie dwóch projektów, ale ma dodatkową złożoność.

### <a name="feature-organization"></a>Organizacja funkcji

Domyślnie aplikacje ASP.NET Core organizują strukturę folderów w taki sposób, aby obejmowały kontrolery i widoki oraz często modele widoków. Kod po stronie klienta do obsługi tych struktur po stronie serwera jest zazwyczaj przechowywany osobno w folderze wwwroot. Jednak duże aplikacje mogą napotkać problemy z tą organizacją, ponieważ praca nad daną funkcją często wymaga przechodzenia między tymi folderami. Jest to bardziej trudne i trudniejsze w miarę zwiększania się liczby plików i podfolderów w każdym folderze, dzięki czemu można przewijać Eksplorator rozwiązań. Jednym z rozwiązań tego problemu jest organizowanie kodu aplikacji według _funkcji_ zamiast według typu plików. Ten styl organizacyjny jest zwykle określany jako foldery funkcji lub [wycinki funkcji](/archive/msdn-magazine/2016/september/asp-net-core-feature-slices-for-asp-net-core-mvc) (Zobacz również: [wycinki pionowe](https://deviq.com/vertical-slices/)).

ASP.NET Core MVC obsługuje obszary do tego celu. Korzystając z obszarów, można utworzyć osobne zestawy kontrolerów i folderów widoków (oraz wszelkich skojarzonych modeli) w każdym folderze obszaru. Rysunek 7-1 pokazuje przykładową strukturę folderów przy użyciu obszarów.

![Przykładowa organizacja obszaru](./media/image7-1.png)

**Rysunek 7-1**. Przykładowa organizacja obszaru

W przypadku korzystania z obszarów należy użyć atrybutów do dekorować kontrolerów z nazwą obszaru, do którego należą:

```csharp
[Area("Catalog")]
public class HomeController
{}
```

Musisz również dodać obsługę obszaru do swoich tras:

```csharp
app.UseEndpoints(endpoints =>
{
    endpoints.MapControllerRoute(name: "areaRoute", pattern: "{area:exists}/{controller=Home}/{action=Index}/{id?}");
    endpoints.MapControllerRoute(name: "default", pattern: "{controller=Home}/{action=Index}/{id?}");
});
```

Oprócz wbudowanej obsługi obszarów, można również użyć własnej struktury folderów oraz Konwencji zamiast atrybutów i tras niestandardowych. Dzięki temu można mieć foldery funkcji, które nie zawierały oddzielnych folderów dla widoków, kontrolerów itp., utrzymując hierarchię Flatter i ułatwiając wyświetlanie wszystkich powiązanych plików w jednym miejscu dla każdej funkcji.

ASP.NET Core używa wbudowanych typów Konwencji do sterowania jego zachowaniem. Możesz zmodyfikować lub zastąpić te konwencje. Na przykład można utworzyć Konwencję, która będzie automatycznie pobierać nazwę funkcji dla danego kontrolera na podstawie jego przestrzeni nazw (co zazwyczaj jest skorelowane z folderem, w którym znajduje się kontroler):

```csharp
public class FeatureConvention : IControllerModelConvention
{
    public void Apply(ControllerModel controller)
    {
        controller.Properties.Add("feature",
        GetFeatureName(controller.ControllerType));
    }

    private string GetFeatureName(TypeInfo controllerType)
    {
        string[] tokens = controllerType.FullName.Split('.');
        if (!tokens.Any(t => t == "Features")) return "";
        string featureName = tokens
        .SkipWhile(t => !t.Equals("features",
        StringComparison.CurrentCultureIgnoreCase))
        .Skip(1)
        .Take(1)
        .FirstOrDefault();
        return featureName;
    }
}
```

Następnie należy określić tę Konwencję jako opcję po dodaniu obsługi MVC do aplikacji w ConfigureServices:

```csharp
services.AddMvc(o => o.Conventions.Add(new FeatureConvention()));
```

ASP.NET Core MVC używa również Konwencji do lokalizowania widoków. Można zastąpić go Konwencją niestandardową, aby widoki znajdowały się w folderach funkcji (przy użyciu nazwy funkcji dostarczonej przez FeatureConvention). Możesz dowiedzieć się więcej o tym podejściu i pobrać przykład roboczy z artykułu magazynowego MSDN, [wycinki funkcji dla ASP.NET Core MVC](/archive/msdn-magazine/2016/september/asp-net-core-feature-slices-for-asp-net-core-mvc).

### <a name="apis-and-no-locblazor-applications"></a>Interfejsy API i Blazor aplikacje

Jeśli aplikacja zawiera zestaw interfejsów API sieci Web, które muszą być zabezpieczone, te interfejsy API należy najlepiej skonfigurować jako oddzielny projekt z widoku lub aplikacji Razor Pages. Oddzielanie interfejsów API, szczególnie publicznych interfejsów API, z aplikacji sieci Web po stronie serwera ma wiele korzyści. Te aplikacje często będą mieć unikatowe charakterystyki wdrożenia i obciążenia. Są one również bardzo prawdopodobnie do wdrażania różnych mechanizmów zabezpieczeń, dzięki standardowym aplikacjom opartym na formularzach, wykorzystującym uwierzytelnianie oparte na plikach cookie i interfejsy API najprawdopodobniej przy użyciu uwierzytelniania opartego na tokenach.

Ponadto Blazor aplikacje, bez względu na to, czy program korzysta z Blazor serwera, czy też Blazor WebAssembly , powinny być skompilowane jako oddzielne projekty. Aplikacje mają różne charakterystyki środowiska uruchomieniowego, a także modele zabezpieczeń. Mogą współużytkować typowe typy z aplikacją sieci Web po stronie serwera (lub projektem interfejsu API), a typy te powinny być zdefiniowane we wspólnym projekcie udostępnionym.

Dodanie Blazor WebAssembly interfejsu administratora do eShopOnWeb wymaga dodania kilku nowych projektów. Blazor WebAssembly Sam projekt, `BlazorAdmin` . Nowy zestaw publicznych punktów końcowych interfejsu API używany przez program `BlazorAdmin` i skonfigurowany do korzystania z uwierzytelniania opartego na tokenach jest zdefiniowany w `PublicApi` projekcie. Niektóre typy udostępnione używane przez oba te projekty są przechowywane w nowym `BlazorShared` projekcie.

Jeden z nich może zadawać, dlaczego należy dodać oddzielny `BlazorShared` projekt, jeśli istnieje już wspólny `ApplicationCore` projekt, którego można użyć do udostępniania dowolnego typu wymaganego przez oba `PublicApi` i `BlazorAdmin` ? Odpowiedź polega na tym, że ten projekt zawiera całą logikę biznesową aplikacji i jest dużo większy niż to konieczne, a także znacznie bardziej niezbędny jest bezpieczny na serwerze. Należy pamiętać, że każda biblioteka, do której odwołuje się `BlazorAdmin` program, zostanie pobrana do przeglądarek użytkowników podczas ładowania Blazor aplikacji.

W zależności od tego, czy jest używany [wzorzec frontonu (BFF)](/azure/architecture/patterns/backends-for-frontends), interfejsy API używane przez Blazor WebAssembly aplikację nie mogą udostępniać ich typów 100% z Blazor . W szczególności publiczny interfejs API, który ma być używany przez wielu różnych klientów, może definiować własne żądanie i typy wyników, zamiast udostępniać je w projekcie udostępnionym specyficznym dla klienta. W przykładzie eShopOnWeb założono, że `PublicApi` projekt jest w rzeczywistości hostem publicznego interfejsu API, dlatego nie wszystkie typy żądań i odpowiedzi pochodzą z `BlazorShared` projektu.

### <a name="cross-cutting-concerns"></a>Zagadnienia ogólne

Po rozbudowywaniu aplikacji coraz bardziej ważne jest, aby wyeliminować problemy związane z wycinaniem i zachować spójność. Niektóre przykłady zagadnień związanych z obcinaniem w aplikacjach ASP.NET Core to uwierzytelnianie, reguły walidacji modelu, buforowanie danych wyjściowych i obsługa błędów, chociaż istnieje wiele innych. ASP.NET Core [filtry](/aspnet/core/mvc/controllers/filters) MVC umożliwiają uruchamianie kodu przed określonymi krokami w potoku przetwarzania żądań lub po nich. Na przykład filtr może zostać uruchomiony przed i po powiązaniu modelu, przed i po akcji lub przed i po wyniku akcji. Można również użyć filtru autoryzacji, aby kontrolować dostęp do reszty potoku. Ilustracje 7-2 pokazuje, w jaki sposób przepływają żądania wykonania przez filtry, jeśli są skonfigurowane.

![Żądanie jest przetwarzane przez filtry autoryzacji, filtry zasobów, powiązania modelu, filtry akcji, wykonywanie akcji i konwersję wyników akcji, filtry wyjątków, filtry wynikowe i wykonywanie wyniku. W ten sposób żądanie jest przetwarzane tylko przez filtry wyników i filtry zasobów przed wysłaniem odpowiedzi do klienta.](./media/image7-2.png)

**Rysunek 7-2**. Zażądaj wykonania przez filtry i potok żądań.

Filtry są zwykle zaimplementowane jako atrybuty, więc można je stosować do kontrolerów lub akcji (lub nawet globalnie). Po dodaniu w ten sposób filtry określone na poziomie akcji przesłaniają lub kompilują przy użyciu filtrów określonych na poziomie kontrolera, które same przesłaniają filtry globalne. Na przykład \[ \] atrybut trasy może służyć do tworzenia tras między kontrolerami i akcjami. Podobnie można skonfigurować autoryzację na poziomie kontrolera, a następnie przesłonić poszczególne akcje, jak pokazano w poniższym przykładzie:

```csharp
[Authorize]
public class AccountController : Controller

{
    [AllowAnonymous] // overrides the Authorize attribute
    public async Task<IActionResult> Login() {}
    public async Task<IActionResult> ForgotPassword() {}
}
```

Pierwsza metoda, login, używa filtru AllowAnonymous (atrybut), aby zastąpić filtr autoryzacji ustawiony na poziomie kontrolera. Akcja ForgotPassword (i jakakolwiek inna akcja w klasie, która nie ma atrybutu AllowAnonymous) będzie wymagała uwierzytelnionego żądania.

Filtry mogą służyć do eliminacji duplikatów w postaci typowych zasad obsługi błędów dla interfejsów API. Na przykład typowe zasady interfejsu API to zwrócenie odpowiedzi NotFound do żądań odwołujących się do kluczy, które nie istnieją, i odpowiedzi nieprawidłowego żądania, jeśli Walidacja modelu kończy się niepowodzeniem. Poniższy przykład ilustruje te dwie zasady w działaniu:

```csharp
[HttpPut("{id}")]
public async Task<IActionResult> Put(int id, [FromBody]Author author)
{
    if ((await _authorRepository.ListAsync()).All(a => a.Id != id))
    {
        return NotFound(id);
    }
    if (!ModelState.IsValid)
    {
        return BadRequest(ModelState);
    }
    author.Id = id;
    await _authorRepository.UpdateAsync(author);
    return Ok();
}
```

Nie należy zezwalać na bałaganie metod akcji przy użyciu kodu warunkowego, takiego jak ten. Zamiast tego należy ściągnąć zasady do filtrów, które mogą być stosowane w zależności od tego, co jest potrzebne. W tym przykładzie sprawdzanie poprawności modelu, który powinien wystąpić za każdym razem, gdy polecenie jest wysyłane do interfejsu API, może być zastąpione przez następujący atrybut:

```csharp
public class ValidateModelAttribute : ActionFilterAttribute
{
    public override void OnActionExecuting(ActionExecutingContext context)
    {
        if (!context.ModelState.IsValid)
        {
            context.Result = new BadRequestObjectResult(context.ModelState);
        }
    }
}
```

Można dodać `ValidateModelAttribute` do projektu jako zależność NuGet, dołączając pakiet [Ardalis. ValidateModel](https://www.nuget.org/packages/Ardalis.ValidateModel) . W przypadku interfejsów API można użyć `ApiController` atrybutu, aby wymusić to zachowanie bez potrzeby osobnego `ValidateModel` filtru.

Analogicznie, filtr może służyć do sprawdzenia, czy rekord istnieje i zwrócić 404 przed wykonaniem akcji, eliminując konieczność wykonywania tych testów w akcji. Po pobraniu wspólnych Konwencji i zorganizowaniu rozwiązania w celu oddzielenia kodu infrastruktury i logiki biznesowej od interfejsu użytkownika, metody akcji MVC powinny być niezwykle cienkie:

```csharp
[HttpPut("{id}")]
[ValidateAuthorExists]
public async Task<IActionResult> Put(int id, [FromBody]Author author)
{
    await _authorRepository.UpdateAsync(author);
    return Ok();
}
```

Aby dowiedzieć się więcej na temat implementowania filtrów i pobrać przykład roboczy z magazynu MSDN, zobacz [Real-World ASP.NET Core filters MVC](/archive/msdn-magazine/2016/august/asp-net-core-real-world-asp-net-core-mvc-filters).

> ### <a name="references--structuring-applications"></a>References — Tworzenie struktury aplikacji
>
> - **Obszarach**\
>   <https://docs.microsoft.com/aspnet/core/mvc/controllers/areas>
> - **Magazyn MSDN — wycinki funkcji dla ASP.NET Core MVC**\
>   <https://docs.microsoft.com/archive/msdn-magazine/2016/september/asp-net-core-feature-slices-for-asp-net-core-mvc>
> - **Filtry**\
>   <https://docs.microsoft.com/aspnet/core/mvc/controllers/filters>
> - **MSDN Magazine — Real World ASP.NET Core Filters**\
>   <https://docs.microsoft.com/archive/msdn-magazine/2016/august/asp-net-core-real-world-asp-net-core-mvc-filters>

## <a name="security"></a>Zabezpieczenia

Zabezpieczanie aplikacji sieci Web to duży temat z wieloma kwestiami. Na najbardziej podstawowym poziomie zabezpieczenia polegają na tym, że wiesz, z kogo pochodzi żądanie, a następnie upewniając się, że żądanie ma tylko dostęp do zasobów, które powinny. Uwierzytelnianie to proces porównujący poświadczenia dostarczone z żądaniem do tych w zaufanym magazynie danych, aby sprawdzić, czy żądanie powinno być traktowane jako pochodzące ze znanej jednostki. Autoryzacja to proces ograniczania dostępu do określonych zasobów na podstawie tożsamości użytkownika. Trzeci problem dotyczący zabezpieczeń chroni żądania przed podsłuchiwaniem przez inne osoby, dla którego należy [upewnić się, że protokół SSL jest używany przez aplikację](/aspnet/core/security/enforcing-ssl).

### <a name="identity"></a>Tożsamość

ASP.NET Core tożsamością jest system członkostwa, którego można użyć do obsługi funkcji logowania dla aplikacji. Obsługuje ona konta użytkowników lokalnych, a także dostawcę logowania zewnętrznego od dostawców, takich jak konto Microsoft, Twitter, Facebook, Google i inne. Oprócz tożsamości ASP.NET Core aplikacja może korzystać z uwierzytelniania systemu Windows lub innego dostawcy tożsamości, takiego jak [serwer tożsamości](https://github.com/IdentityServer/IdentityServer4).

ASP.NET Core tożsamość jest dołączana do nowych szablonów projektu, jeśli wybrano opcję konta poszczególnych użytkowników. Ten szablon obejmuje obsługę rejestracji, logowania, logowania zewnętrznego, zapomnianych haseł i dodatkowych funkcji.

![Wybieranie kont poszczególnych użytkowników w celu skonfigurowania tożsamości](./media/image7-3.png)

**Rysunek 7-3**. Wybierz opcję konta poszczególnych użytkowników, aby mieć wstępnie skonfigurowaną tożsamość.

Obsługa tożsamości jest konfigurowana podczas uruchamiania, zarówno w ConfigureServices, jak i w konfiguracji:

```csharp
public void ConfigureServices(IServiceCollection services)
{
    // Add framework services.
    services.AddDbContext<ApplicationDbContext>(options =>
    options.UseSqlServer(Configuration.GetConnectionString("DefaultConnection")));
    services.AddIdentity<ApplicationUser, IdentityRole>()
        .AddEntityFrameworkStores<ApplicationDbContext>()
        .AddDefaultTokenProviders();
    services.AddMvc();
}

public void Configure(IApplicationBuilder app)
{
    app.UseStaticFiles();
    app.UseIdentity();
    app.UseEndpoints(endpoints =>
    {
        endpoints.MapControllerRoute(name: "default", pattern: "{controller=Home}/{action=Index}/{id?}");
    });
}
```

Ważne jest, aby UseIdentity pojawił się przed UseMvc w metodzie Configure. Podczas konfigurowania tożsamości w programie ConfigureServices należy zauważyć wywołanie AddDefaultTokenProviders. Nie ma nic do wykonania w przypadku tokenów, które mogą być używane do zabezpieczania komunikacji w sieci Web, ale zamiast tego odnoszą się do dostawców, którzy tworzą monity, które mogą być wysyłane do użytkowników za pośrednictwem wiadomości SMS lub poczty e-mail w celu potwierdzenia tożsamości.

Więcej informacji na temat [konfigurowania uwierzytelniania dwuskładnikowego](/aspnet/core/security/authentication/2fa) i [włączania zewnętrznych dostawców logowania](/aspnet/core/security/authentication/social/) można znaleźć w oficjalnym ASP.NET Core dokumentach.

### <a name="authentication"></a>Authentication

Uwierzytelnianie to proces określania, kto uzyskuje dostęp do systemu. Jeśli używasz tożsamości ASP.NET Core i metod konfiguracji przedstawionych w poprzedniej sekcji, spowoduje to automatyczne skonfigurowanie niektórych ustawień uwierzytelniania w aplikacji. Można jednak również skonfigurować te ustawienia domyślne ręcznie lub zastąpić je zestawem AddIdentity. Jeśli używasz tożsamości, konfiguruje uwierzytelnianie oparte na plikach cookie jako *schemat* domyślny.

W przypadku uwierzytelniania opartego na sieci Web w programie istnieje zazwyczaj pięć akcji, które mogą być wykonywane w trakcie uwierzytelniania klienta systemu. Są to:

- Potwierdza. Użyj informacji dostarczonych przez klienta, aby utworzyć tożsamość do użycia w aplikacji.
- Sprawdz. Ta akcja służy do wymagania, aby klient mógł identyfikować siebie.
- Uniemożliwia. Informowanie klienta, aby nie wykonywał akcji.
- Logowanie. W jakiś sposób Utrwalaj istniejącego klienta.
- Wyloguj się. Usuń klienta z trwałości.

Istnieje kilka typowych technik uwierzytelniania w aplikacjach sieci Web. Są one nazywane schematami. Dany schemat definiuje akcje dla niektórych lub wszystkich powyższych opcji. Niektóre schematy obsługują tylko podzbiór akcji i mogą wymagać oddzielnego schematu, aby wykonać te czynności, które nie są obsługiwane. Na przykład schemat OpenId-Connect (OIDC) nie obsługuje logowania ani wylogowywania, ale jest często skonfigurowany do korzystania z uwierzytelniania plików cookie dla tej trwałości.

W aplikacji ASP.NET Core można skonfigurować `DefaultAuthenticateScheme` oraz opcjonalne określone schematy dla każdej akcji opisanej powyżej. Na przykład, `DefaultChallengeScheme` `DefaultForbidScheme` itp. Wywołanie [`AddIdentity<TUser,TRole>`](https://github.com/dotnet/aspnetcore/blob/release/3.1/src/Identity/Core/src/IdentityServiceCollectionExtensions.cs#L38-L102) konfiguruje kilka aspektów aplikacji i dodaje wiele wymaganych usług. Obejmuje to również wywołanie konfigurowania schematu uwierzytelniania:

```csharp
services.AddAuthentication(options =>
{
    options.DefaultAuthenticateScheme = IdentityConstants.ApplicationScheme;
    options.DefaultChallengeScheme = IdentityConstants.ApplicationScheme;
    options.DefaultSignInScheme = IdentityConstants.ExternalScheme;
});
```

Te schematy używają plików cookie w celu zapewnienia trwałości i przekierowania do stron logowania w celu uwierzytelniania domyślnego. Te schematy są odpowiednie dla aplikacji sieci Web, które współpracują z użytkownikami za pośrednictwem przeglądarek sieci Web, ale nie są zalecane dla interfejsów API. Zamiast tego interfejsy API zwykle używają innej formy uwierzytelniania, takiej jak tokeny okaziciela JWT.

Interfejsy API sieci Web są używane przez kod, taki jak `HttpClient` aplikacje .NET i równoważne typy w innych strukturach. Ci klienci oczekują użytecznej odpowiedzi z wywołania interfejsu API lub kodu stanu wskazującego, czy wystąpił problem. Ci klienci nie korzystają z przeglądarki i nie renderują kodu HTML ani nie mogą z nimi korzystać. Z tego względu nie są odpowiednie dla punktów końcowych interfejsu API, aby przekierować klientów do stron logowania, jeśli nie są uwierzytelnione. Inny schemat jest bardziej odpowiedni.

Aby skonfigurować uwierzytelnianie dla interfejsów API, można skonfigurować uwierzytelnianie podobne do następujących, które są używane przez `PublicApi` projekt w aplikacji eShopOnWeb Reference:

```csharp
services.AddAuthentication(config =>
{
    config.DefaultScheme = JwtBearerDefaults.AuthenticationScheme;
})
    .AddJwtBearer(config =>
    {
        config.RequireHttpsMetadata = false;
        config.SaveToken = true;
        config.TokenValidationParameters = new TokenValidationParameters
        {
            ValidateIssuerSigningKey = true,
            IssuerSigningKey = new SymmetricSecurityKey(key),
            ValidateIssuer = false,
            ValidateAudience = false
        };
    });
```

Chociaż istnieje możliwość skonfigurowania wielu różnych schematów uwierzytelniania w ramach jednego projektu, można skonfigurować jeden domyślny schemat. Z tego powodu, aplikacja referencyjna eShopOnWeb oddziela swoje interfejsy API do własnego projektu, `PublicApi` niezależnie od projektu głównego, `Web` zawierającego widoki i Razor Pages aplikacji.

#### <a name="authentication-in-no-locblazor-apps"></a>Uwierzytelnianie w Blazor aplikacjach

Blazor Aplikacje serwera mogą korzystać z tych samych funkcji uwierzytelniania co inna aplikacja ASP.NET Core. Blazorw WebAssembly aplikacjach nie można używać wbudowanych dostawców tożsamości i uwierzytelniania, ponieważ są one uruchamiane w przeglądarce. BlazorWebAssemblyaplikacje mogą lokalnie przechowywać stan uwierzytelniania użytkownika i uzyskiwać dostęp do oświadczeń, aby określić akcje, które użytkownicy powinni wykonywać. Wszystkie testy uwierzytelniania i autoryzacji należy jednak wykonać na serwerze niezależnie od implementacji logiki w Blazor WebAssembly aplikacji, ponieważ użytkownicy mogą łatwo obejść aplikację i bezpośrednio korzystać z interfejsów API.

> ### <a name="references--authentication"></a>Odwołania — uwierzytelnianie
>
> - **Akcje uwierzytelniania i ustawienia domyślne**\
>   <https://stackoverflow.com/a/52493428>
> - **Uwierzytelnianie i autoryzacja dla aplikacji jednostronicowych**\
>   <https://docs.microsoft.com/aspnet/core/security/authentication/identity-api-authorization>
> - **ASP.NET Core Blazor uwierzytelnianie i autoryzacja**\
>   <https://docs.microsoft.com/aspnet/core/blazor/security/>
> - **Zabezpieczenia: uwierzytelnianie i autoryzacja w ASP.NET Web Forms i Blazor**\
>   <https://docs.microsoft.com/dotnet/architecture/blazor-for-web-forms-developers/security-authentication-authorization>

### <a name="authorization"></a>Autoryzacja

Najprostsza forma autoryzacji obejmuje ograniczenie dostępu do użytkowników anonimowych. Tę funkcję można osiągnąć, stosując \[ \] atrybut Autoryzuj do określonych kontrolerów lub akcji. Jeśli role są używane, atrybut można rozszerzyć, aby ograniczyć dostęp do użytkowników, którzy należą do określonych ról, jak pokazano poniżej:

```csharp
[Authorize(Roles = "HRManager,Finance")]
public class SalaryController : Controller
{

}
```

W takim przypadku użytkownicy należący do `HRManager` lub `Finance` role (lub obie) będą mieli dostęp do SalaryController. Aby wymagać, aby użytkownik należał do wielu ról (nie tylko jeden z kilku), można zastosować atrybut wielokrotnie, określając wymaganą rolę za każdym razem.

Określanie niektórych zestawów ról jako ciągów w wielu różnych kontrolerach i akcjach może prowadzić do niepożądanego powtórzenia. Należy określić co najmniej stałe dla tych literałów ciągów i użyć stałych w dowolnym miejscu, aby podać ciąg. Istnieje również możliwość skonfigurowania zasad autoryzacji, które hermetyzują reguły autoryzacji, a następnie określania zasad zamiast poszczególnych ról przy zastosowaniu \[ \] atrybutu Autoryzuj:

```csharp
[Authorize(Policy = "CanViewPrivateReport")]
public IActionResult ExecutiveSalaryReport()
{
    return View();
}
```

Korzystając z zasad w ten sposób, można oddzielić rodzaje akcji, które są ograniczone z określonych ról lub reguł, które mają zastosowanie. Później, jeśli utworzysz nową rolę, która musi mieć dostęp do określonych zasobów, można po prostu zaktualizować zasady, zamiast aktualizować każdą listę ról przy każdym \[ autoryzowanym \] atrybucie.

#### <a name="claims"></a>Oświadczenia

Oświadczenia są parami wartości nazw, które reprezentują właściwości uwierzytelnionego użytkownika. Na przykład użytkownik może przechowywać numer pracownika jako roszczeń. Oświadczenia mogą być następnie używane jako część zasad autoryzacji. Można utworzyć zasady o nazwie "EmployeeOnly", które wymagają istnienia żądania o nazwie "EmployeeNumber", jak pokazano w poniższym przykładzie:

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc();
    services.AddAuthorization(options =>
    {
        options.AddPolicy("EmployeeOnly", policy => policy.RequireClaim("EmployeeNumber"));
    });
}
```

Te zasady mogą być następnie używane z \[ \] atrybutem Autoryzuj do ochrony dowolnego kontrolera i/lub akcji, zgodnie z powyższym opisem.

#### <a name="securing-web-apis"></a>Zabezpieczanie interfejsów API sieci Web

Większość interfejsów API sieci Web powinna implementować system uwierzytelniania oparty na tokenach. Uwierzytelnianie tokenu jest bezstanowe i zaprojektowane do skalowalności. W systemie uwierzytelniania opartego na tokenach klient musi najpierw przeprowadzić uwierzytelnienie u dostawcy uwierzytelniania. Jeśli to się powiedzie, klient wystawia token, który jest po prostu zrozumiałą w sposób kryptograficznie ciągiem znaków. Najbardziej typowym formatem tokenów jest token sieci Web JSON lub JWT (często wymawiane "notowania"). Gdy klient musi wydać żądanie do interfejsu API, dodaje ten token jako nagłówek w żądaniu. Następnie serwer sprawdza poprawność tokenu znalezionego w nagłówku żądania przed ukończeniem żądania. Rysunek 7-4 ilustruje ten proces.

![TokenAuth](./media/image7-4.png)

**Rysunek 7-4.** Uwierzytelnianie oparte na tokenach dla interfejsów API sieci Web.

Możesz utworzyć własną usługę uwierzytelniania, zintegrować ją z usługą Azure AD i uwierzytelnianiem OAuth lub wdrożyć usługę przy użyciu narzędzia typu open source, takiego jak [IdentityServer](https://github.com/IdentityServer).

Tokeny JWT mogą osadzać oświadczenia dotyczące użytkownika, które można odczytać na kliencie lub serwerze. Możesz użyć narzędzia, takiego jak [JWT.IO](https://jwt.io/) , aby wyświetlić zawartość tokenu JWT. Nie należy przechowywać poufnych danych, takich jak hasła lub klucze w tokenach JTW, ponieważ ich zawartość jest łatwo odczytywana.

W przypadku używania tokenów JWT z SPA lub Blazor WebAssembly aplikacjami należy przechowywać token w dowolnym miejscu na kliencie, a następnie dodać go do każdego wywołania interfejsu API. To działanie jest zwykle wykonywane jako nagłówek, ponieważ ilustruje poniższy kod:

```csharp
// AuthService.cs in BlazorAdmin project of eShopOnWeb
private async Task SetAuthorizationHeader()
{
    var token = await GetToken();
    _httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
}
```

Po wywołaniu powyższej metody żądania wykonane przy użyciu `_httpClient` będą mieć token osadzony w nagłówkach żądania, co umożliwia interfejsowi API po stronie serwera uwierzytelnianie i Autoryzowanie żądania.

#### <a name="custom-security"></a>Zabezpieczenia niestandardowe

Należy zwrócić szczególną uwagę na "wycofywanie własnych" implementacji kryptografii, członkostwa użytkowników lub systemu generacji tokenów. Istnieje wiele dostępnych alternatyw komercyjnych i typu "open source", które niemal wykorzystają lepsze zabezpieczenia niż implementacja niestandardowa.

> ### <a name="references--security"></a>Odwołania — zabezpieczenia
>
> - **Przegląd dokumentów dotyczących zabezpieczeń**\
>   <https://docs.microsoft.com/aspnet/core/security/>
> - **Wymuszanie protokołu SSL w aplikacji ASP.NET Core**\
>   <https://docs.microsoft.com/aspnet/core/security/enforcing-ssl>
> - **Wprowadzenie do tożsamości**\
>   <https://docs.microsoft.com/aspnet/core/security/authentication/identity>
> - **Wprowadzenie do autoryzacji**\
>   <https://docs.microsoft.com/aspnet/core/security/authorization/introduction>
> - **Uwierzytelnianie i autoryzacja API Apps w Azure App Service**\
>   <https://docs.microsoft.com/azure/app-service-api/app-service-api-authentication>
> - **Serwer tożsamości**\
>   <https://github.com/IdentityServer>

## <a name="client-communication"></a>Komunikacja z klientem

Oprócz obsługi stron i reagowania na żądania danych za pośrednictwem interfejsów API sieci Web aplikacje ASP.NET Core mogą komunikować się bezpośrednio z połączonymi klientami. Ta komunikacja wychodząca może korzystać z różnych technologii transportu, najczęściej używanych przez obiekty WebSockets. ASP.NET Core sygnalizujący to biblioteka, która ułatwia dodawanie funkcji komunikacji między klientami w czasie rzeczywistym do aplikacji. Program sygnalizujący obsługuje różne technologie transportowe, w tym elementy WebSockets, i dzieli wiele szczegółów implementacji od dewelopera.

Komunikacja klientów w czasie rzeczywistym, bez względu na to, czy używanie funkcji WebSockets bezpośrednio czy z innymi technikami jest przydatne w różnych scenariuszach aplikacji. Oto niektóre przykłady:

- Aplikacje do pokoju rozmów na żywo

- Monitorowanie aplikacji

- Aktualizacje postępu zadania

- Powiadomienia

- Interaktywne aplikacje formularzy

Podczas tworzenia komunikacji z klientem w aplikacjach są zwykle dwa składniki:

- Menedżer połączeń po stronie serwera (centrum sygnałów, websocketmanager WebSocketHandler)

- Biblioteka po stronie klienta

Klienci nie są ograniczeni do przeglądarek — aplikacje mobilne, aplikacje konsolowe i inne aplikacje natywne mogą również komunikować się przy użyciu sygnałów/obiektów WebSockets. Następujący prosty program umożliwia echo całej zawartości wysyłanej do aplikacji czatu do konsoli programu w ramach przykładowej aplikacji websocketmanager:

```csharp
public class Program
{
    private static Connection _connection;
    public static void Main(string[] args)
    {
        StartConnectionAsync();
        _connection.On("receiveMessage", (arguments) =>
        {
            Console.WriteLine($"{arguments[0]} said: {arguments[1]}");
        });
        Console.ReadLine();
        StopConnectionAsync();
    }

    public static async Task StartConnectionAsync()
    {
        _connection = new Connection();
        await _connection.StartConnectionAsync("ws://localhost:65110/chat");
    }

    public static async Task StopConnectionAsync()
    {
        await _connection.StopConnectionAsync();
    }
}
```

Rozważ sposoby, w których aplikacje komunikują się bezpośrednio z aplikacjami klienckimi i należy rozważyć, czy komunikacja w czasie rzeczywistym poprawi środowisko użytkownika aplikacji.

> ### <a name="references--client-communication"></a>Odwołania — komunikacja z klientem
>
> - **ASP.NET Core sygnalizujący**\
>   <https://github.com/dotnet/aspnetcore/tree/master/src/SignalR>
> - **Menedżer obiektów WebSocket**\
>   <https://github.com/radu-matei/websocket-manager>

## <a name="domain-driven-design--should-you-apply-it"></a>Projektowanie oparte na domenie — czy należy je zastosować?

Domain-Driven Design (DDD) to Agile podejście do tworzenia oprogramowania, które kładzie nacisk na _domenę biznesową_. W dużym stopniu naciska na komunikację i interakcję z ekspertami domeny biznesowej, którzy mogą odnosić się do deweloperów, w jaki działa system w świecie rzeczywistym. Jeśli na przykład tworzysz system, który obsługuje handel giełdowy, ekspertem domeny może być doświadczony Broker ds. it. DDD jest przeznaczony do rozwiązywania dużych i złożonych problemów związanych z biznesem. często nie jest to konieczne w przypadku mniejszych, prostszych aplikacji, ponieważ inwestycje w zrozumieniu i modelowania domeny nie są w tej samej postaci.

Podczas kompilowania oprogramowania po drodze, zespół (w tym udziałowcy nietechniczne i współautorzy) powinien opracować powszechny _Język_ dla obszaru problemu. Oznacza to, że ta sama terminologia powinna zostać użyta w przypadku modelowania rzeczywistego pojęcia, odpowiedniki oprogramowania i wszelkich struktur, które mogą istnieć, aby zachować koncepcję (na przykład tabele bazy danych). W związku z tym koncepcje opisane w języku powszechnym powinny stanowić podstawę dla _modelu domeny_.

Model domeny obejmuje obiekty, które współdziałają ze sobą, aby reprezentować zachowanie systemu. Te obiekty mogą należeć do następujących kategorii:

- [Jednostki](https://deviq.com/entity/)reprezentujące obiekty z wątkiem tożsamości. Jednostki są zwykle przechowywane w stanie trwałości przy użyciu klucza, za pomocą którego mogą być później pobierane.

- [Agregaty](https://deviq.com/aggregate-pattern/)reprezentujące grupy obiektów, które powinny być utrwalane jako jednostka.

- [Obiekty wartości](https://deviq.com/value-object/), które reprezentują koncepcje, które mogą być porównane na podstawie sumy wartości ich właściwości. Na przykład DateRange składa się z daty rozpoczęcia i zakończenia.

- [Zdarzenia domeny](https://martinfowler.com/eaaDev/DomainEvent.html), które reprezentują rzeczy wykonywane w systemie, które są istotne dla innych części systemu.

Model domeny DDD powinien hermetyzować złożone zachowanie w modelu. Jednostki, w szczególności nie powinny być kolekcjami właściwości. Gdy model domeny nie ma zachowania i jedynie reprezentuje stan systemu, jest on uznawany za [model Anemic](https://deviq.com/anemic-model/), który jest NIEPOŻĄDANY w DDD.

Oprócz tych typów modeli DDD zazwyczaj wykorzystuje różne wzorce:

- [Repozytorium](https://deviq.com/repository-pattern/), aby uzyskać szczegółowe informacje o trwałości.

- [Fabryka](https://en.wikipedia.org/wiki/Factory_method_pattern)dla hermetyzowania złożonego tworzenia obiektów.

- [Usługi](http://gorodinski.com/blog/2012/04/14/services-in-domain-driven-design-ddd/)dla hermetyzowania złożonych zachowań i/lub szczegółów implementacji infrastruktury.

- [Polecenia](https://en.wikipedia.org/wiki/Command_pattern), do oddzielania poleceń i wykonywania polecenia.

- [Specyfikacja](https://deviq.com/specification-pattern/)dla hermetyzowania szczegółów zapytania.

DDD również zaleca użycie czystej architektury omówionej wcześniej, co pozwala na swobodne sprzęganie, hermetyzację i kod, który można łatwo zweryfikować przy użyciu testów jednostkowych.

### <a name="when-should-you-apply-ddd"></a>Kiedy należy zastosować DDD

DDD jest dobrze dostosowany do dużych aplikacji z znaczącą złożonością firmy (nie tylko technicznie). Aplikacja powinna wymagać znajomości ekspertów domeny. Istnieje duże zachowanie w modelu domeny, reprezentujące reguły biznesowe i interakcje wykraczające poza zwykłe przechowywanie i pobieranie bieżącego stanu różnych rekordów z magazynów danych.

### <a name="when-shouldnt-you-apply-ddd"></a>Kiedy nie należy stosować DDD

DDD obejmuje inwestycje w modelowanie, architekturę i komunikację, które mogą nie być uzasadnione w przypadku mniejszych aplikacji lub aplikacji, które zasadniczo CRUD (Tworzenie/odczytywanie/aktualizowanie/usuwanie). W przypadku wybrania podejścia do Twojej aplikacji po DDD, ale dowiesz się, że domena ma model Anemic bez zachowań, może być konieczne ponowne zawieszanie się z podejściem. Twoja aplikacja może nie potrzebować DDD lub może być potrzebna pomoc w refaktoryzacji aplikacji w celu hermetyzacji logiki biznesowej w modelu domeny, a nie w bazie danych lub interfejsie użytkownika.

Podejście hybrydowe będzie używać DDD tylko dla transakcyjnych lub bardziej złożonych obszarów aplikacji, ale nie dla prostszej CRUD lub tylko do odczytu części aplikacji. Na przykład nie są wymagane ograniczenia agregacji, jeśli tworzysz zapytanie o dane w celu wyświetlenia raportu lub wizualizacji danych dla pulpitu nawigacyjnego. Doskonale akceptowalne jest oddzielny, prostszy model odczytu dla takich wymagań.

> ### <a name="references--domain-driven-design"></a>Odwołania — projektowanie Domain-Driven
>
> - **DDD w zwykłym języku angielskim (odpowiedź StackOverflow)**\
>   <https://stackoverflow.com/questions/1222392/can-someone-explain-domain-driven-design-ddd-in-plain-english-please/1222488#1222488>

## <a name="deployment"></a>Wdrożenie

W procesie wdrażania aplikacji ASP.NET Core należy wykonać kilka kroków, bez względu na to, gdzie będzie ona hostowana. Pierwszym krokiem jest opublikowanie aplikacji, którą można wykonać przy użyciu `dotnet publish` interfejsu wiersza polecenia. Ten krok spowoduje skompilowanie aplikacji i umieszczenie wszystkich plików wymaganych do uruchomienia aplikacji w wydzielonym folderze. W przypadku wdrażania z programu Visual Studio ten krok jest wykonywany automatycznie. Folder publikowania zawiera pliki. exe i. dll dla aplikacji i jej zależności. Aplikacja samodzielna zawiera również wersję środowiska uruchomieniowego .NET. Aplikacje ASP.NET Core zawierają również pliki konfiguracji, statyczne zasoby klienta i widoki MVC.

Aplikacje ASP.NET Core są aplikacjami konsolowymi, które należy uruchomić, gdy serwer jest uruchamiany i uruchamiany ponownie, jeśli wystąpi awaria aplikacji (lub serwera). Za pomocą Menedżera procesów można zautomatyzować ten proces. Najbardziej typowymi menedżerami procesów dla ASP.NET Core są Nginx i Apache w systemach Linux i IIS lub Windows Service w systemie Windows.

Oprócz Menedżera procesów aplikacje ASP.NET Core mogą korzystać z serwera proxy zwrotnego. Odwrotny serwer proxy odbiera żądania HTTP z Internetu i przekazuje je do Kestrel po pewnej wstępnej obsłudze. Odwrotne serwery proxy zapewniają warstwę zabezpieczeń aplikacji. Kestrel również nie obsługuje hostowania wielu aplikacji na tym samym porcie, dlatego nie można używać technik takich jak nagłówki hosta, aby umożliwić hostowanie wielu aplikacji na tym samym porcie i adresie IP.

![Kestrel z Internetem](./media/image7-5.png)

**Rysunek 7-5**. ASP.NET hostowane w Kestrel za odwrotnym serwerze proxy

Innym scenariuszem, w którym może być przydatny zwrotny serwer proxy, jest zabezpieczanie wielu aplikacji przy użyciu protokołu SSL/HTTPS. W takim przypadku tylko zwrotny serwer proxy musi mieć skonfigurowany protokół SSL. Komunikacja między odwrotnym serwerem proxy a Kestrel może odbywać się za pośrednictwem protokołu HTTP, jak pokazano na rysunku 7-6.

![ASP.NET hostowane za pośrednictwem protokołu HTTPS zwrotnego serwera proxy](./media/image7-6.png)

**Rysunek 7-6**. ASP.NET hostowane za pośrednictwem protokołu HTTPS zwrotnego serwera proxy

Coraz bardziej popularne podejście polega na hostowaniu ASP.NET Core aplikacji w kontenerze platformy Docker, który można hostować lokalnie lub wdrożyć na platformie Azure na potrzeby hostingu opartego na chmurze. Kontener platformy Docker może zawierać kod aplikacji działający w Kestrel i zostałby wdrożony za odwrotnym serwerem proxy, jak pokazano powyżej.

Jeśli aplikacja jest obsługiwana na platformie Azure, można użyć Application Gateway Microsoft Azure jako dedykowanego urządzenia wirtualnego, aby zapewnić kilka usług. Oprócz działania jako zwrotny serwer proxy dla poszczególnych aplikacji, Application Gateway może również oferować następujące funkcje:

- Równoważenie obciążenia HTTP

- Odciążanie protokołu SSL (tylko protokół SSL do Internetu)

- Kompleksowa próba SSL

- Routing między lokacjami (konsolidowanie do 20 lokacji na jednym Application Gateway)

- Zapora aplikacji internetowej

- Obsługa protokołu WebSocket

- Zaawansowana diagnostyka

_Dowiedz się więcej o opcjach wdrażania platformy Azure w [rozdziale 10](development-process-for-azure.md)._

> ### <a name="references--deployment"></a>Odwołania — wdrażanie
>
> - **Omówienie hostingu i wdrażania**\
>   <https://docs.microsoft.com/aspnet/core/publishing/>
> - **Kiedy używać Kestrel z zwrotnym serwerem proxy**\
>   <https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy>
> - **Hostowanie aplikacji ASP.NET Core w platformie Docker**\
>   <https://docs.microsoft.com/aspnet/core/publishing/docker>
> - **Wprowadzenie do usługi Azure Application Gateway**\
>   <https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction>

>[!div class="step-by-step"]
>[Poprzedni](common-client-side-web-technologies.md) 
> [Dalej](work-with-data-in-asp-net-core-apps.md)
