---
title: Tworzenie prostej mikrousługi CRUD na podstawie danych
description: Architektura mikrousług platformy .NET dla aplikacji platformy .NET w kontenerze | Zapoznaj się z tworzeniem prostej mikrousługi CRUD (opartej na danych) w kontekście aplikacji mikrousług.
ms.date: 08/14/2020
ms.openlocfilehash: 27c9b331573ff08ea16c756552818df285156282
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96739872"
---
# <a name="creating-a-simple-data-driven-crud-microservice"></a>Tworzenie prostej mikrousługi CRUD na podstawie danych

W tej części przedstawiono sposób tworzenia prostej mikrousługi, która wykonuje operacje tworzenia, odczytu, aktualizacji i usuwania (CRUD) w źródle danych.

## <a name="designing-a-simple-crud-microservice"></a>Projektowanie prostej mikrousługi CRUD

Z punktu widzenia projektu ten typ mikrousługi kontenera jest bardzo prosty. Prawdopodobnie problem, który należy rozwiązać, jest prosty lub że implementacja jest tylko dowodem koncepcji.

![Diagram przedstawiający prosty Wzorzec projektowy mikrousług CRUD.](./media/data-driven-crud-microservice/internal-design-simple-crud-microservices.png)

**Rysunek 6-4**. Wewnętrzny projekt dla prostych mikrousług CRUD

Przykładem tego rodzaju prostej usługi dysków danych jest mikrousługa katalogu z przykładowej aplikacji eShopOnContainers. Ten typ usługi implementuje wszystkie jej funkcje w jednym ASP.NET Core projekcie interfejsu API sieci Web, który zawiera klasy dla modelu danych, jego logiki biznesowej i kod dostępu do danych. Przechowuje także powiązane z nią dane w bazie danych działającej w SQL Server (jako inny kontener do celów deweloperskich/testowych), ale może to być również dowolny zwykły SQL Server hosta, jak pokazano na rysunku 6-5.

![Diagram przedstawiający kontener mikrousług oparty na danych/CRUD.](./media/data-driven-crud-microservice/simple-data-driven-crud-microservice.png)

**Rysunek 6-5**. Prosty projekt mikrousług oparty na danych/CRUD

Poprzedni diagram przedstawia mikrousługę wykazu logicznego, która obejmuje jej bazę danych katalogu, która może być lub nie znajduje się na tym samym hoście platformy Docker. Posiadanie bazy danych na tym samym hoście platformy Docker może być dobrym rozwiązaniem do programowania, ale nie w środowisku produkcyjnym. Podczas opracowywania tego rodzaju usługi wymagany jest tylko [ASP.NET Core](/aspnet/core/) i interfejs API dostępu do danych lub ORM, jak [Entity Framework Core](/ef/core/index). Możesz również generować metadane [struktury Swagger](https://swagger.io/) automatycznie za pomocą [Swashbuckle](https://github.com/domaindrivendev/Swashbuckle.AspNetCore) , aby podać opis oferty usługi, zgodnie z opisem w następnej sekcji.

Należy pamiętać, że uruchamianie serwera bazy danych, takiego jak SQL Server w kontenerze platformy Docker, jest doskonałe dla środowisk programistycznych, ponieważ wszystkie Twoje zależności mogą działać bez konieczności aprowizacji bazy danych w chmurze lub lokalnie. Jest to bardzo wygodne w przypadku uruchamiania testów integracji. Jednak w przypadku środowisk produkcyjnych nie zaleca się korzystania z serwera bazy danych w kontenerze, ponieważ zazwyczaj nie ma wysokiej dostępności. W środowisku produkcyjnym na platformie Azure zaleca się użycie usługi Azure SQL DB lub innej technologii bazy danych, która zapewnia wysoką dostępność i wysoką skalowalność. Na przykład w przypadku podejścia NoSQL można wybrać pozycję CosmosDB.

Na koniec edytując pliki metadanych pliku dockerfile i Docker-Compose. yml, można skonfigurować sposób tworzenia obrazu tego kontenera — na podstawie obrazu podstawowego, który będzie używany, a także ustawień projektowania, takich jak nazwy wewnętrzne i zewnętrzne oraz porty TCP.

## <a name="implementing-a-simple-crud-microservice-with-aspnet-core"></a>Implementowanie prostej mikrousługi CRUD z ASP.NET Core

Aby zaimplementować prostą CRUD mikrousługi przy użyciu platformy .NET Core i programu Visual Studio, Zacznij od utworzenia prostego projektu interfejsu API sieci Web ASP.NET Core (działającego na platformie .NET Core, aby można go było uruchomić na hoście Docker systemu Linux), jak pokazano na rysunku 6-6.

![Zrzut ekranu przedstawiający wizualizację Studios, która zawiera konfigurację projektu.](./media/data-driven-crud-microservice/create-asp-net-core-web-api-project.png)

**Rysunek 6-6**. Tworzenie projektu interfejsu API sieci Web ASP.NET Core w programie Visual Studio 2019

Aby utworzyć projekt interfejsu API sieci Web ASP.NET Core, najpierw wybierz aplikację sieci Web ASP.NET Core, a następnie wybierz typ interfejsu API. Po utworzeniu projektu można zaimplementować kontrolery MVC w taki sam sposób jak w każdym innym projekcie interfejsu API sieci Web przy użyciu interfejsu API Entity Framework lub innego interfejsu API. W nowym projekcie interfejsu API sieci Web można zobaczyć, że jedyną zależnością w tej mikrousłudze jest ASP.NET Core samej. Wewnętrznie w ramach zależności *Microsoft. AspNetCore. All* odwołuje się do Entity Framework i wielu innych pakietów NuGet platformy .NET Core, jak pokazano na rysunku 6-7.

![Zrzut ekranu przedstawiający narzędzia VS pokazujące zależności NuGet składnika Catalog. API.](./media/data-driven-crud-microservice/simple-crud-web-api-microservice-dependencies.png)

**Rysunek 6-7**. Zależności w prostej mikrousłudze CRUD Web API

Projekt interfejsu API zawiera odwołania do pakietu NuGet Microsoft. AspNetCore. app, który zawiera odwołania do wszystkich najważniejszych pakietów. Może również zawierać inne pakiety.

### <a name="implementing-crud-web-api-services-with-entity-framework-core"></a>Implementowanie usług interfejsu API sieci Web CRUD za pomocą Entity Framework Core

Entity Framework (EF) Core to lekka, rozszerzalna i wieloplatformowa wersja popularnej Entity Framework technologii dostępu do danych. EF Core to Mapowanie obiektowo-relacyjne (ORM), które umożliwia deweloperom platformy .NET współdziałanie z bazą danych przy użyciu obiektów .NET.

Mikrousługa katalogu używa EF i dostawcy SQL Server, ponieważ jego baza danych działa w kontenerze z SQL Server dla obrazu platformy Docker systemu Linux. Jednak bazę danych można wdrożyć w dowolnym SQL Server, na przykład lokalnie lub w usłudze Azure SQL DB. Jedyną czynnością, którą należy zmienić, są parametry połączenia w mikrousłudze ASP.NET Web API.

#### <a name="the-data-model"></a>Model danych

W przypadku EF Core dostęp do danych odbywa się przy użyciu modelu. Model składa się z klas jednostek jednostki i kontekstu pochodnego (DbContext) reprezentujących sesję z bazą danych, co pozwala na wykonywanie zapytań i zapisywanie danych. Można wygenerować model na podstawie istniejącej bazy danych, ręcznie kod modelu do dopasowania do bazy danych lub użyć techniki migracji EF, aby utworzyć bazę danych z modelu przy użyciu podejścia pierwszego kodu (ułatwiającego rozwijanie bazy danych w miarę zmiany modelu w czasie). W przypadku mikrousługi katalogu ostatnie podejście zostało użyte. Przykład klasy jednostki CatalogItem można zobaczyć w poniższym przykładzie kodu, który jest prostą, niedawną klasą obiektu CLR ([poco](https://en.wikipedia.org/wiki/Plain_Old_CLR_Object)).

```csharp
public class CatalogItem
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string Description { get; set; }
    public decimal Price { get; set; }
    public string PictureFileName { get; set; }
    public string PictureUri { get; set; }
    public int CatalogTypeId { get; set; }
    public CatalogType CatalogType { get; set; }
    public int CatalogBrandId { get; set; }
    public CatalogBrand CatalogBrand { get; set; }
    public int AvailableStock { get; set; }
    public int RestockThreshold { get; set; }
    public int MaxStockThreshold { get; set; }

    public bool OnReorder { get; set; }
    public CatalogItem() { }

    // Additional code ...
}
```

Wymagany jest również DbContext, który reprezentuje sesję z bazą danych. W przypadku mikrousługi katalogowej Klasa CatalogContext dziedziczy z klasy podstawowej DbContext, jak pokazano w następującym przykładzie:

```csharp
public class CatalogContext : DbContext
{
    public CatalogContext(DbContextOptions<CatalogContext> options) : base(options)
    { }
    public DbSet<CatalogItem> CatalogItems { get; set; }
    public DbSet<CatalogBrand> CatalogBrands { get; set; }
    public DbSet<CatalogType> CatalogTypes { get; set; }

    // Additional code ...
}
```

Możesz mieć dodatkowe `DbContext` implementacje. Przykładowo w przypadku mikrousługi przykładowej katalogu. API istnieje druga `DbContext` Nazwa, `CatalogContextSeed` gdzie automatycznie wypełnia przykładowe dane podczas pierwszego próby dostępu do bazy danych. Ta metoda jest przydatna w przypadku danych demonstracyjnych i scenariuszy zautomatyzowanych testów.

W programie `DbContext` można użyć metody, `OnModelCreating` Aby dostosować mapowania jednostek obiektów/baz danych oraz inne [punkty rozszerzalności EF](https://devblogs.microsoft.com/dotnet/implementing-seeding-custom-conventions-and-interceptors-in-ef-core-1-0/).

##### <a name="querying-data-from-web-api-controllers"></a>Wykonywanie zapytań dotyczących danych z kontrolerów interfejsu API sieci Web

Wystąpienia klas jednostek są zwykle pobierane z bazy danych przy użyciu programu Query Integrated Language (LINQ), jak pokazano w następującym przykładzie:

```csharp
[Route("api/v1/[controller]")]
public class CatalogController : ControllerBase
{
    private readonly CatalogContext _catalogContext;
    private readonly CatalogSettings _settings;
    private readonly ICatalogIntegrationEventService _catalogIntegrationEventService;

    public CatalogController(
        CatalogContext context,
        IOptionsSnapshot<CatalogSettings> settings,
        ICatalogIntegrationEventService catalogIntegrationEventService)
    {
        _catalogContext = context ?? throw new ArgumentNullException(nameof(context));
        _catalogIntegrationEventService = catalogIntegrationEventService
            ?? throw new ArgumentNullException(nameof(catalogIntegrationEventService));

        _settings = settings.Value;
        context.ChangeTracker.QueryTrackingBehavior = QueryTrackingBehavior.NoTracking;
    }

    // GET api/v1/[controller]/items[?pageSize=3&pageIndex=10]
    [HttpGet]
    [Route("items")]
    [ProducesResponseType(typeof(PaginatedItemsViewModel<CatalogItem>), (int)HttpStatusCode.OK)]
    [ProducesResponseType(typeof(IEnumerable<CatalogItem>), (int)HttpStatusCode.OK)]
    [ProducesResponseType((int)HttpStatusCode.BadRequest)]
    public async Task<IActionResult> ItemsAsync(
        [FromQuery]int pageSize = 10,
        [FromQuery]int pageIndex = 0,
        string ids = null)
    {
        if (!string.IsNullOrEmpty(ids))
        {
            var items = await GetItemsByIdsAsync(ids);

            if (!items.Any())
            {
                return BadRequest("ids value invalid. Must be comma-separated list of numbers");
            }

            return Ok(items);
        }

        var totalItems = await _catalogContext.CatalogItems
            .LongCountAsync();

        var itemsOnPage = await _catalogContext.CatalogItems
            .OrderBy(c => c.Name)
            .Skip(pageSize * pageIndex)
            .Take(pageSize)
            .ToListAsync();

        itemsOnPage = ChangeUriPlaceholder(itemsOnPage);

        var model = new PaginatedItemsViewModel<CatalogItem>(
            pageIndex, pageSize, totalItems, itemsOnPage);

        return Ok(model);
    }
    //...
}
```

##### <a name="saving-data"></a>Zapisywanie danych

Dane są tworzone, usuwane i modyfikowane w bazie danych przy użyciu wystąpień klas jednostek. Do kontrolerów interfejsu API sieci Web można dodać kod podobny do poniższego zakodowanego przykładu (w tym przypadku dane są w tym przypadku).

```csharp
var catalogItem = new CatalogItem() {CatalogTypeId=2, CatalogBrandId=2,
                                     Name="Roslyn T-Shirt", Price = 12};
_context.Catalog.Add(catalogItem);
_context.SaveChanges();
```

##### <a name="dependency-injection-in-aspnet-core-and-web-api-controllers"></a>Wstrzykiwanie zależności w kontrolerach ASP.NET Core i interfejsu API sieci Web

W ASP.NET Core można użyć iniekcji zależności (DI) poza ramką. Nie jest konieczne skonfigurowanie kontenera kontroli (IoC) innej firmy, ale w razie potrzeby można podłączyć preferowany kontener IoC do infrastruktury ASP.NET Core. W takim przypadku oznacza to, że można bezpośrednio wstrzyknąć wymagane, EF DbContext lub dodatkowe repozytoria za pośrednictwem konstruktora kontrolera.

W `CatalogController` klasie wymienionej wcześniej `CatalogContext` (która dziedziczy z `DbContext` ) typ jest wstrzykiwany wraz z innymi wymaganymi obiektami w `CatalogController()` konstruktorze.

Ważną konfiguracją skonfigurowaną w projekcie interfejsu API sieci Web jest rejestracja klasy DbContext w kontenerze IoC usługi. Zwykle jest to wykonywane w `Startup` klasie przez wywołanie `services.AddDbContext<CatalogContext>()` metody wewnątrz `ConfigureServices()` metody, jak pokazano w poniższym **uproszczonym** przykładzie:

```csharp
public void ConfigureServices(IServiceCollection services)
{
    // Additional code...
    services.AddDbContext<CatalogContext>(options =>
    {
        options.UseSqlServer(Configuration["ConnectionString"],
        sqlServerOptionsAction: sqlOptions =>
        {
            sqlOptions.MigrationsAssembly(
                typeof(Startup).GetTypeInfo().Assembly.GetName().Name);

           //Configuring Connection Resiliency:
           sqlOptions.
               EnableRetryOnFailure(maxRetryCount: 5,
               maxRetryDelay: TimeSpan.FromSeconds(30),
               errorNumbersToAdd: null);

       });

       // Changing default behavior when client evaluation occurs to throw.
       // Default in EFCore would be to log warning when client evaluation is done.
       options.ConfigureWarnings(warnings => warnings.Throw(
           RelationalEventId.QueryClientEvaluationWarning));
   });

  //...
}
```

### <a name="additional-resources"></a>Dodatkowe zasoby

- **Wykonywanie zapytania dotyczącego danych** \
  [https://docs.microsoft.com/ef/core/querying/index](/ef/core/querying/index)

- **Zapisywanie danych** \
  [https://docs.microsoft.com/ef/core/saving/index](/ef/core/saving/index)

## <a name="the-db-connection-string-and-environment-variables-used-by-docker-containers"></a>Parametry połączenia bazy danych i zmienne środowiskowe używane przez kontenery platformy Docker

Możesz użyć ustawień ASP.NET Core i dodać Właściwość ConnectionString do settings.jsw pliku, jak pokazano w następującym przykładzie:

```json
{
    "ConnectionString": "Server=tcp:127.0.0.1,5433;Initial Catalog=Microsoft.eShopOnContainers.Services.CatalogDb;User Id=sa;Password=[PLACEHOLDER]",
    "ExternalCatalogBaseUrl": "http://localhost:5101",
    "Logging": {
        "IncludeScopes": false,
        "LogLevel": {
            "Default": "Debug",
            "System": "Information",
            "Microsoft": "Information"
        }
    }
}
```

settings.jsw pliku może mieć wartości domyślne dla właściwości ConnectionString lub dla każdej innej właściwości. Jednak te właściwości zostaną przesłonięte przez wartości zmiennych środowiskowych określonych w pliku Docker-Compose. override. yml podczas korzystania z platformy Docker.

Z plików Docker-Compose. yml lub Docker-Compose. override. yml można inicjować te zmienne środowiskowe, aby platforma Docker ustawi jako zmienne środowiskowe systemu operacyjnego, jak pokazano w następującym pliku Docker-Compose. override. yml (parametry połączenia i inne wiersze są zawijane w tym przykładzie, ale nie będzie on zawijany w Twoim pliku).

```yml
# docker-compose.override.yml

#
catalog-api:
  environment:
    - ConnectionString=Server=sqldata;Database=Microsoft.eShopOnContainers.Services.CatalogDb;User Id=sa;Password=[PLACEHOLDER]
    # Additional environment variables for this service
  ports:
    - "5101:80"
```

Pliki Docker-Compose. yml na poziomie rozwiązania nie są bardziej elastyczne niż pliki konfiguracyjne na poziomie projektu lub mikrousług, ale również bezpieczniej, jeśli zastąpisz zmienne środowiskowe zadeklarowane w plikach tworzenia platformy Docker z wartościami ustawionymi na podstawie narzędzi wdrażania, takich jak Azure DevOps Services zadań wdrażania platformy Docker.

Na koniec można uzyskać tę wartość z kodu za pomocą konfiguracji \[ "ConnectionString" \] , jak pokazano w metodzie ConfigureServices w poprzednim przykładzie kodu.

Jednak w przypadku środowisk produkcyjnych warto zapoznać się z dodatkowymi sposobami przechowywania wpisów tajnych, takich jak parametry połączenia. Doskonałym sposobem na zarządzanie wpisami tajnymi aplikacji jest użycie [Azure Key Vault](https://azure.microsoft.com/services/key-vault/).

Azure Key Vault pomaga przechowywać i chronić klucze kryptograficzne i wpisy tajne używane przez aplikacje i usługi w chmurze. Wpis tajny to wszystko, co chcesz zachować ścisłą kontrolę, podobnie jak klucze interfejsu API, parametry połączeń, hasła itp., a ścisła kontrola obejmuje rejestrowanie użycia, Ustawianie wygaśnięcia, zarządzanie dostępem *między innymi*.

Azure Key Vault pozwala na bardzo szczegółowy poziom kontroli użycia wpisów tajnych aplikacji bez konieczności poinformowania użytkownika. Wpisy tajne można nawet obrócić, aby zwiększyć bezpieczeństwo bez zakłócania programowania lub operacji.

Aplikacje muszą być zarejestrowane w Active Directory organizacji, aby mogły korzystać z Key Vault.

Więcej informacji można znaleźć w *dokumentacji dotyczącej pojęć Key Vault* .

### <a name="implementing-versioning-in-aspnet-web-apis"></a>Implementowanie obsługi wersji w interfejsach API sieci Web ASP.NET

W miarę zmiany wymagań firmy nowe kolekcje zasobów mogą zostać dodane, relacje między zasobami mogą ulec zmianie, a struktura danych w zasobach może zostać zmieniona. Aktualizacja internetowego interfejsu API do obsługi nowych wymagań jest stosunkowo prosta, ale należy wziąć pod uwagę wpływ takich zmian na aplikacje klienckie korzystające z internetowego interfejsu API. Chociaż deweloper projektujący i implementujący interfejs API sieci Web ma pełną kontrolę nad tym interfejsem API, Deweloper nie ma tego samego zakresu kontroli nad aplikacjami klienckimi, które mogą być kompilowane przez organizacje innych firm.

Obsługa wersji umożliwia korzystanie z interfejsu API sieci Web w celu wskazania dostępnych funkcji i zasobów. Aplikacja kliencka może przesyłać żądania do określonej wersji funkcji lub zasobu. Istnieje kilka sposobów implementacji wersji:

- Obsługa wersji za pomocą identyfikatora URI

- Obsługa wersji za pomocą ciągu zapytania

- Obsługa wersji za pomocą nagłówka

Jest to najprostszy do zaimplementowania ciąg zapytania i wersja identyfikatora URI. Przechowywanie wersji nagłówka jest dobrym rozwiązaniem. Przechowywanie wersji nagłówków nie jest jednak jawne i proste jako przechowywanie wersji identyfikatorów URI. Ponieważ przechowywanie wersji adresów URL jest najprostszym i najbardziej jawnym, przykładowa aplikacja eShopOnContainers korzysta z obsługi wersji identyfikatorów URI.

W przypadku obsługi wersji identyfikatorów URI, podobnie jak w przypadku przykładowej aplikacji eShopOnContainers, przy każdej modyfikacji internetowego interfejsu API lub zmianie schematu zasobów należy dodać numer wersji do identyfikatora URI dla każdego zasobu. Istniejące identyfikatory URI powinny nadal działać jak poprzednio, zwracając zasoby zgodne ze schematem, który jest zgodny z żądaną wersją.

Jak pokazano w poniższym przykładzie kodu, można ustawić wersję przy użyciu atrybutu trasy w kontrolerze internetowego interfejsu API, co spowoduje, że wersja jawnie w identyfikatorze URI (v1 w tym przypadku).

```csharp
[Route("api/v1/[controller]")]
public class CatalogController : ControllerBase
{
    // Implementation ...
```

Ten mechanizm przechowywania wersji jest prosty i zależy od serwera routingu żądania do odpowiedniego punktu końcowego. Jednak w celu uzyskania bardziej zaawansowanej wersji i najlepszej metody w przypadku korzystania z usługi REST należy użyć narzędzia z nośnika i zaimplementować [HATEOAS (hipertekst jako aparat stanu aplikacji)](/azure/architecture/best-practices/api-design#use-hateoas-to-enable-navigation-to-related-resources).

### <a name="additional-resources"></a>Dodatkowe zasoby

- **Scott Hanselman. Łatwość ASP.NET Core RESTful internetowego interfejsu API** \
  <https://www.hanselman.com/blog/ASPNETCoreRESTfulWebAPIVersioningMadeEasy.aspx>

- **Przechowywanie wersji interfejsu API sieci Web RESTful** \
  <https://docs.microsoft.com/azure/architecture/best-practices/api-design#versioning-a-restful-web-api>

- **Roy. Przechowywanie wersji, nośniki i REST** \
  <https://www.infoq.com/articles/roy-fielding-on-versioning>

## <a name="generating-swagger-description-metadata-from-your-aspnet-core-web-api"></a>Generowanie metadanych opisu struktury Swagger z internetowego interfejsu API ASP.NET Core

[Swagger](https://swagger.io/) to powszechnie używana platforma typu "open source" obsługiwana przez duży ekosystem narzędzi, które ułatwiają projektowanie, kompilowanie, dokumentowanie i Używanie interfejsów API RESTful. Staje się standardem dla domeny metadanych opisu interfejsu API. Należy uwzględnić metadane opisu struktury Swagger przy użyciu dowolnego rodzaju mikrousług, mikrousług opartych na danych lub bardziej zaawansowanych mikrousług opartych na domenie (jak wyjaśniono w poniższej sekcji).

Sercem struktury Swagger jest specyfikacja struktury Swagger, która jest metadanymi opisu interfejsu API w pliku JSON lub YAML. Specyfikacja tworzy kontrakt RESTful dla interfejsu API, szczegóły wszystkich zasobów i operacji zarówno w formacie czytelnym dla człowieka, jak i na komputerze umożliwiającym łatwe programowanie, odnajdywanie i integrację.

Specyfikacja jest podstawą specyfikacji OpenAPI (OAS) i jest opracowana w postaci otwartej, przejrzystej i współpracy ze współpracownikami w celu standaryzacji sposobu definiowania interfejsów RESTful.

Specyfikacja definiuje strukturę sposobu odnajdowania usługi i sposobu jej zrozumienia. Aby uzyskać więcej informacji, w tym Edytor sieci Web i przykłady specyfikacji struktury Swagger z firm takich jak Spotify, Uber, zapasy i Microsoft, zobacz witrynę programu Swagger ( <https://swagger.io> ).

### <a name="why-use-swagger"></a>Dlaczego warto używać struktury Swagger?

Główne przyczyny generowania metadanych struktury Swagger dla interfejsów API są następujące.

**Możliwość automatycznego wykorzystywania i integrowania interfejsów API przez inne produkty**. Liczne produkty i [Narzędzia komercyjne](https://swagger.io/commercial-tools/) oraz wiele [bibliotek i struktur obsługują strukturę](https://swagger.io/open-source-integrations/) Swagger. Firma Microsoft oferuje produkty i narzędzia wysokiego poziomu, które mogą automatycznie korzystać z interfejsów API opartych na strukturze Swagger, takich jak następujące:

- [AutoRest](https://github.com/Azure/AutoRest). Można automatycznie generować klasy klienckie platformy .NET do wywoływania struktury Swagger. To narzędzie może być używane z poziomu interfejsu wiersza polecenia i integruje się z programem Visual Studio, aby ułatwić korzystanie z interfejsu GUI.

- [Microsoft Flow](https://flow.microsoft.com/). Możesz automatycznie [użyć i zintegrować interfejs API](https://flow.microsoft.com/blog/integrating-custom-api/) w przepływie pracy Microsoft Flow wysokiego poziomu, bez konieczności korzystania z umiejętności programistycznych.

- [Microsoft powerapps](https://powerapps.microsoft.com/). Możesz automatycznie korzystać z interfejsu API z [aplikacji mobilnych powerapps](https://powerapps.microsoft.com/blog/register-and-use-custom-apis-in-powerapps/) utworzonych przy użyciu [powerapps Studio](https://powerapps.microsoft.com/build-powerapps/), bez konieczności umiejętności programistycznych.

- [Logic Apps Azure App Service](/azure/app-service-logic/app-service-logic-what-are-logic-apps). Możesz automatycznie [używać interfejsu API i zintegrować go z aplikacją logiki Azure App Service](/azure/app-service-logic/app-service-logic-custom-hosted-api), bez wymaganych umiejętności programistycznych.

**Możliwość automatycznego generowania dokumentacji interfejsu API**. Podczas tworzenia interfejsów API RESTful o dużej skali, takich jak złożone aplikacje oparte na mikrousługach, należy obsługiwać wiele punktów końcowych z różnymi modelami danych używanymi w ładunku żądania i odpowiedzi. Posiadanie odpowiedniej dokumentacji i posiadanie pełnego Eksploratora interfejsów API, jak w przypadku programu Swagger, jest kluczem dla sukcesu interfejsu API i wdrażania przez deweloperów.

Metadane struktury Swagger to Microsoft Flow, PowerApps i Azure Logic Apps używane do zrozumienia, jak używać interfejsów API i łączyć się z nimi.

Istnieje kilka opcji automatyzowania generowania metadanych struktury Swagger dla ASP.NET Core aplikacji interfejsu API REST, w formie stron pomocy interfejsu API funkcji, opartych na strukturze *Swagger-UI*.

Prawdopodobnie najlepszą wiedzą, że jest to [Swashbuckle](https://github.com/domaindrivendev/Swashbuckle.AspNetCore) , która jest obecnie używana w [eShopOnContainers](https://github.com/dotnet-architecture/eShopOnContainers) i w tym przewodniku zawarto więcej informacji, ale istnieje również opcja użycia [NSwag](https://github.com/RSuter/NSwag), która może generować klientów interfejsu API języka TypeScript i języka C \# , a także kontrolerów języka c \# , z specyfikacji struktury Swagger lub openapi, a nawet przez skanowanie pliku dll, który zawiera kontrolery, przy użyciu [NSwagStudio](https://github.com/RSuter/NSwag/wiki/NSwagStudio).

### <a name="how-to-automate-api-swagger-metadata-generation-with-the-swashbuckle-nuget-package"></a>Jak zautomatyzować generowanie metadanych struktury Swagger interfejsu API za pomocą pakietu NuGet Swashbuckle

Ręczne generowanie metadanych struktury Swagger (w pliku JSON lub YAML) może być żmudnym pracy. Można jednak zautomatyzować odnajdywanie interfejsów API ASP.NET usług interfejsu API sieci Web za pomocą [pakietu NuGet Swashbuckle](https://aka.ms/swashbuckledotnetcore) do dynamicznego generowania metadanych interfejsu API struktury Swagger.

Swashbuckle automatycznie generuje metadanych struktury Swagger dla projektów internetowego interfejsu API ASP.NET. Obsługuje ona ASP.NET Core projekty interfejsu API sieci Web oraz tradycyjnego interfejsu API sieci Web ASP.NET oraz innych typów, takich jak aplikacja interfejsu API platformy Azure, aplikacja mobilna platformy Azure, platforma Azure Service Fabric na podstawie ASP.NET. Obsługuje ona również zwykły internetowy interfejs API wdrożony w kontenerach, jak w przypadku aplikacji referencyjnej.

Swashbuckle łączy Eksploratora interfejsu API i struktury Swagger lub [Swagger-interfejs użytkownika](https://github.com/swagger-api/swagger-ui) , aby zapewnić bogate środowisko odnajdywania i dokumentacji dla odbiorców interfejsu API. Oprócz aparatu generatora metadanych struktury Swagger Swashbuckle zawiera również osadzoną wersję programu Swagger-UI, która będzie automatycznie działać po zainstalowaniu Swashbuckle.

Oznacza to, że możesz uzupełnić interfejs API za pomocą interfejsu użytkownika, aby ułatwić deweloperom korzystanie z interfejsu API. Wymaga bardzo małej ilości kodu i konserwacji, ponieważ jest automatycznie generowana, co pozwala skupić się na tworzeniu interfejsu API. Wynik dla Eksploratora interfejsu API wygląda jak rysunek 6-8.

![Zrzut ekranu przedstawiający Eksplorator interfejsu API struktury Swagger wyświetlający interfejs API eShopOContainers.](./media/data-driven-crud-microservice/swagger-metadata-eshoponcontainers-catalog-microservice.png)

**Rysunek 6-8**. Eksplorator interfejsu API Swashbuckle na podstawie metadanych struktury Swagger — mikrousługa eShopOnContainers Catalog

Dokumentacja interfejsu API interfejsu użytkownika programu Swagger wygenerowanego przez Swashbuckle obejmuje wszystkie opublikowane akcje. Eksplorator interfejsów API nie jest najważniejszym elementem w tym miejscu. Gdy dysponujesz interfejsem API sieci Web, który można opisać w metadanych struktury Swagger, interfejs API może być bezproblemowo używany z narzędzi opartych na strukturze Swagger, w tym generatory kodu klasy serwera proxy klienta, które mogą kierować wiele platform. Na przykład, jak wspomniano, [AutoRest](https://github.com/Azure/AutoRest) automatycznie generuje klasy klienckie platformy .NET. Jednak dostępne są również dodatkowe narzędzia, takie jak [Swagger-codegen](https://github.com/swagger-api/swagger-codegen) , które umożliwiają automatyczne generowanie kodu bibliotek klienckich interfejsu API, wycinków serwerów i dokumentacji.

Obecnie Swashbuckle składa się z pięciu wewnętrznych pakietów NuGet w ramach [Swashbuckle. AspNetCore](https://www.nuget.org/packages/Swashbuckle.AspNetCore) dla aplikacji ASP.NET Core.

Po zainstalowaniu tych pakietów NuGet w projekcie interfejsu API sieci Web należy skonfigurować strukturę Swagger w klasie startowej, jak w poniższym kodzie **uproszczonym** :

```csharp
public class Startup
{
    public IConfigurationRoot Configuration { get; }
    // Other startup code...

    public void ConfigureServices(IServiceCollection services)
    {
        // Other ConfigureServices() code...

        // Add framework services.
        services.AddSwaggerGen(options =>
        {
            options.DescribeAllEnumsAsStrings();
            options.SwaggerDoc("v1", new OpenApiInfo
            {
                Title = "eShopOnContainers - Catalog HTTP API",
                Version = "v1",
                Description = "The Catalog Microservice HTTP API. This is a Data-Driven/CRUD microservice sample"
            });
        });

        // Other ConfigureServices() code...
    }

    public void Configure(IApplicationBuilder app,
        IHostingEnvironment env,
        ILoggerFactory loggerFactory)
    {
        // Other Configure() code...
        // ...
        app.UseSwagger()
            .UseSwaggerUI(c =>
            {
                c.SwaggerEndpoint("/swagger/v1/swagger.json", "My API V1");
            });
    }
}
```

Po wykonaniu tej czynności możesz uruchomić aplikację i przeglądać następujące dane JSON programu Swagger i punkty końcowe interfejsu użytkownika przy użyciu adresów URL takich jak:

```console
  http://<your-root-url>/swagger/v1/swagger.json

  http://<your-root-url>/swagger/
```

Wygenerowany interfejs użytkownika utworzony przez Swashbuckle został wcześniej wyświetlony dla adresu URL, takiego jak `http://<your-root-url>/swagger` . Na rysunku 6-9 można także sprawdzić, jak można testować dowolną metodę interfejsu API.

![Zrzut ekranu przedstawiający interfejs użytkownika struktury Swagger pokazujący dostępne narzędzia do testowania.](./media/data-driven-crud-microservice/swashbuckle-ui-testing.png)

**Rysunek 6-9**. Swashbuckle interfejs użytkownika testowania metody katalogu/elementów interfejsu API

W szczegółach interfejsu API interfejsu użytkownika programu Swagger przedstawiono przykład odpowiedzi i można go użyć do wykonania rzeczywistego interfejsu API, który jest doskonałym rozwiązaniem do odnajdywania deweloperów. Na rysunku 6-10 przedstawiono metadane JSON programu Swagger wygenerowane z mikrousługi eShopOnContainers (która jest używana przez narzędzia poniżej) podczas żądania `http://<your-root-url>/swagger/v1/swagger.json` przy użyciu programu [Poster](https://www.getpostman.com/).

![Zrzut ekranu przedstawiający przykładowego interfejsu użytkownika programu do wyświetlania metadanych w formacie JSON programu Swagger.](./media/data-driven-crud-microservice/swagger-json-metadata.png)

**Rysunek 6-10**. Metadane JSON programu Swagger

Jest to proste. I ponieważ jest generowany automatycznie, podczas dodawania większej funkcjonalności do interfejsu API zostaną powiększone metadane programu Swagger.

### <a name="additional-resources"></a>Dodatkowe zasoby

- **Strony pomocy interfejsu API sieci Web ASP.NET korzystające z programu Swagger** \
  [https://docs.microsoft.com/aspnet/core/tutorials/web-api-help-pages-using-swagger](/aspnet/core/tutorials/web-api-help-pages-using-swagger)

- **Wprowadzenie do Swashbuckle i ASP.NET Core** \
  [https://docs.microsoft.com/aspnet/core/tutorials/getting-started-with-swashbuckle](/aspnet/core/tutorials/getting-started-with-swashbuckle)

- **Wprowadzenie do NSwag i ASP.NET Core** \
  [https://docs.microsoft.com/aspnet/core/tutorials/getting-started-with-nswag](/aspnet/core/tutorials/getting-started-with-nswag)

> [!div class="step-by-step"]
> [Poprzedni](microservice-application-design.md) 
>  [Dalej](multi-container-applications-docker-compose.md)
