---
title: Pracuj z danymi w aplikacjach ASP.NET Core
description: Tworzenie architektury nowoczesnych aplikacji sieci Web przy użyciu ASP.NET Core i platformy Azure | Praca z danymi w aplikacjach ASP.NET Core
author: ardalis
ms.author: wiwagn
ms.date: 12/01/2020
no-loc:
- Blazor
- WebAssembly
ms.openlocfilehash: 9d85d700ecb8d6cbe7afd8d3c724f499ee5fed71
ms.sourcegitcommit: 45c7148f2483db2501c1aa696ab6ed2ed8cb71b2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/08/2020
ms.locfileid: "96851259"
---
# <a name="working-with-data-in-aspnet-core-apps"></a>Praca z danymi w aplikacjach ASP.NET Core

> "Dane są cenne i będą trwać dłużej niż same systemy".
>
> Tim Berners-Lee

Dostęp do danych jest ważną częścią niemal każdej aplikacji oprogramowania. ASP.NET Core obsługuje wiele opcji dostępu do danych, w tym Entity Framework Core (i Entity Framework 6), i może współdziałać z dowolnymi strukturami dostępu do danych platformy .NET. Wybór struktury dostępu do danych, która ma być używana, zależy od potrzeb aplikacji. Abstrakcję tych opcji z projektów ApplicationCore i interfejsów użytkownika oraz Hermetyzowanie szczegółów implementacji w infrastrukturze, pomaga w wytwarzaniu luźno sprzężonych, weryfikowalne oprogramowania.

## <a name="entity-framework-core-for-relational-databases"></a>Entity Framework Core (dla relacyjnych baz danych)

Jeśli piszesz nową aplikację ASP.NET Core, która musi pracować z danymi relacyjnymi, Entity Framework Core (EF Core) jest zalecanym sposobem, aby aplikacja mogła uzyskać dostęp do swoich danych. EF Core to Mapowanie obiektowo-relacyjne (O/RM), które umożliwia deweloperom platformy .NET utrwalanie obiektów do i ze źródła danych. Eliminuje to potrzebę większości deweloperów kodu dostępu do danych, zwykle trzeba pisać. Podobnie jak ASP.NET Core, EF Core został ponownie zapisany od podstaw, aby obsługiwał modularne aplikacje dla wielu platform. Należy dodać je do aplikacji jako pakiet NuGet, skonfigurować ją w programie startowym i zażądać jej za pomocą iniekcji zależności wszędzie tam, gdzie jest potrzebna.

Aby użyć EF Core z bazą danych SQL Server, uruchom następujące polecenie interfejsu wiersza polecenia dotnet:

```dotnetcli
dotnet add package Microsoft.EntityFrameworkCore.SqlServer
```

Aby dodać obsługę źródła danych inMemory, na potrzeby testowania:

```dotnetcli
dotnet add package Microsoft.EntityFrameworkCore.InMemory
```

### <a name="the-dbcontext"></a>DbContext

Aby można było korzystać z EF Core, należy podklasą <xref:Microsoft.EntityFrameworkCore.DbContext> . Ta klasa zawiera właściwości reprezentujące kolekcje jednostek, z którymi aplikacja będzie współdziałać. Przykład eShopOnWeb zawiera CatalogContext z kolekcjami dla elementów, marek i typów:

```csharp
public class CatalogContext : DbContext
{
    public CatalogContext(DbContextOptions<CatalogContext> options) : base(options)
    {

    }

    public DbSet<CatalogItem> CatalogItems { get; set; }

    public DbSet<CatalogBrand> CatalogBrands { get; set; }

    public DbSet<CatalogType> CatalogTypes { get; set; }
}
```

DbContext musi mieć konstruktora akceptującego DbContextOptions i przekazać ten argument do podstawowego konstruktora DbContext. Jeśli masz tylko jeden DbContext w aplikacji, możesz przekazać wystąpienie elementu DbContextOptions, ale jeśli masz więcej niż jeden, musisz użyć ogólnego \<T> typu DbContextOptions, przekazując w typ kontekstu dbjako parametr generyczny.

### <a name="configuring-ef-core"></a>Konfigurowanie EF Core

W aplikacji ASP.NET Core zwykle konfigurujesz EF Core w metodzie ConfigureServices. EF Core używa DbContextOptionsBuilder, który obsługuje kilka przydatnych metod rozszerzania w celu usprawnienia jego konfiguracji. Aby skonfigurować CatalogContext do używania bazy danych SQL Server z parametrami połączenia zdefiniowanymi w konfiguracji, należy dodać następujący kod do ConfigureServices:

```csharp
services.AddDbContext<CatalogContext>(options => options.UseSqlServer (Configuration.GetConnectionString("DefaultConnection")));
```

Aby użyć bazy danych znajdującej się w pamięci:

```csharp
services.AddDbContext<CatalogContext>(options =>
    options.UseInMemoryDatabase());
```

Po zainstalowaniu EF Core utworzyć typ elementu podrzędnego DbContext i skonfigurować go w ConfigureServices, możesz użyć EF Core. Możesz zażądać wystąpienia typu DbContext w dowolnej usłudze, która go potrzebuje, i rozpocząć pracę z utrwalonymi obiektami przy użyciu LINQ tak, jakby znajdowały się one po prostu w kolekcji. EF Core Wykonuje translację wyrażeń LINQ na zapytania SQL w celu przechowywania i pobierania danych.

Możesz zobaczyć zapytania, EF Core jest wykonywane przez skonfigurowanie rejestratora i upewnienie się, że jego poziom jest ustawiony na co najmniej informacje, jak pokazano na rysunku 8-1.

![Rejestrowanie EF Core zapytań do konsoli](./media/image8-1.png)

**Rysunek 8-1**. Rejestrowanie EF Core zapytań do konsoli

### <a name="fetching-and-storing-data"></a>Pobieranie i przechowywanie danych

Aby pobrać dane z EF Core, można uzyskać dostęp do odpowiedniej właściwości i użyć LINQ do filtrowania wyniku. Można również użyć LINQ do wykonania projekcji, przekształcania wyniku z jednego typu na drugi. Poniższy przykład pobiera CatalogBrands uporządkowane według nazwy, filtrowane według ich właściwości Enabled i rzutowane na typ SelectListItem:

```csharp
var brandItems = await _context.CatalogBrands
    .Where(b => b.Enabled)
    .OrderBy(b => b.Name)
    .Select(b => new SelectListItem {
        Value = b.Id, Text = b.Name })
    .ToListAsync();
```

Ważne jest, aby w powyższym przykładzie dodać wywołanie do ToListAsync w celu natychmiastowego wykonania zapytania. W przeciwnym razie instrukcja przypisze interfejs IQueryable \<SelectListItem> do brandItems, który nie będzie wykonywany do momentu wyliczenia. Istnieją specjaliści i wady zwracające wyniki z metod. Pozwala to na dalsze modyfikacje EF Core kwerendy, ale może również powodować błędy, które występują tylko w czasie wykonywania, jeśli operacje są dodawane do zapytania, którego EF Core nie można przetłumaczyć. Zazwyczaj bezpieczniejsze jest przekazywanie wszelkich filtrów do metody wykonującej dostęp do danych i zwracanie z powrotem kolekcji w pamięci (na przykład listy \<T> ) jako wyniku.

EF Core śledzi zmiany w jednostkach pobieranych z trwałości. Aby zapisać zmiany w monitorowanej jednostce, wystarczy wywołać metodę metody SaveChanges w kontekście DbContext, upewniając się, że jest to to samo wystąpienie DbContext, które zostało użyte do pobrania jednostki. Dodawanie i usuwanie jednostek jest bezpośrednio wykonywane na odpowiedniej właściwości Nieogólnymi, z wywołaniem metody SaveChanges w celu wykonania poleceń bazy danych. Poniższy przykład ilustruje Dodawanie, aktualizowanie i usuwanie jednostek z trwałości.

```csharp
// create
var newBrand = new CatalogBrand() { Brand = "Acme" };
_context.Add(newBrand);
await _context.SaveChangesAsync();

// read and update
var existingBrand = _context.CatalogBrands.Find(1);
existingBrand.Brand = "Updated Brand";
await _context.SaveChangesAsync();

// read and delete (alternate Find syntax)
var brandToDelete = _context.Find<CatalogBrand>(2);
_context.CatalogBrands.Remove(brandToDelete);
await _context.SaveChangesAsync();
```

EF Core obsługuje metody synchroniczne i asynchroniczne do pobierania i zapisywania. W aplikacjach sieci Web zaleca się użycie wzorca Async/await z metodami asynchronicznymi, aby wątki serwera sieci Web nie były blokowane podczas oczekiwania na ukończenie operacji dostępu do danych.

### <a name="fetching-related-data"></a>Pobieranie powiązanych danych

Gdy EF Core Pobiera jednostki, wypełnia wszystkie właściwości, które są przechowywane bezpośrednio w tej jednostce w bazie danych. Właściwości nawigacji, takie jak listy powiązanych jednostek, nie są wypełniane i mogą mieć ustawioną wartość null. Ten proces zapewnia, że EF Core nie pobiera większej ilości danych niż jest to konieczne, co jest szczególnie ważne w przypadku aplikacji sieci Web, które muszą szybko przetwarzać żądania i zwracać odpowiedzi w wydajny sposób. Aby uwzględnić relacje z jednostką przy użyciu _ładowania eager_, należy określić właściwość przy użyciu metody include Extension w zapytaniu, jak pokazano poniżej:

```csharp
// .Include requires using Microsoft.EntityFrameworkCore
var brandsWithItems = await _context.CatalogBrands
    .Include(b => b.Items)
    .ToListAsync();
```

Można uwzględnić wiele relacji, a także dołączyć podrelacje przy użyciu ThenInclude. EF Core wykona pojedyncze zapytanie w celu pobrania zestawu wyników. Alternatywnie można uwzględnić właściwości nawigacji właściwości nawigacji poprzez przekazanie "." rozdzielany ciąg do `.Include()` metody rozszerzającej, na przykład:

```csharp
    .Include("Items.Products")
```

Oprócz hermetyzacji logiki filtrowania, Specyfikacja może określić kształt danych do zwrócenia, w tym właściwości do wypełnienia. Przykład eShopOnWeb zawiera kilka specyfikacji demonstrujących Hermetyzowanie eager informacji dotyczących ładowania w ramach specyfikacji. W tym miejscu można zobaczyć, jak specyfikacja jest używana jako część zapytania:

```csharp
// Includes all expression-based includes
query = specification.Includes.Aggregate(query,
            (current, include) => current.Include(include));

// Include any string-based include statements
query = specification.IncludeStrings.Aggregate(query,
            (current, include) => current.Include(include));
```

Kolejną opcją ładowania powiązanych danych jest użycie _jawnego ładowania_. Jawne ładowanie umożliwia załadowanie dodatkowych danych do jednostki, która została już pobrana. Ponieważ takie podejście obejmuje oddzielne żądanie do bazy danych, nie jest to zalecane w przypadku aplikacji sieci Web, co powinno zminimalizować liczbę rejsów w bazie danych na żądanie.

_Ładowanie z opóźnieniem_ to funkcja, która automatycznie ładuje powiązane dane, ponieważ odwołuje się do niej aplikacja. EF Core dodano obsługę ładowania z opóźnieniem w wersji 2,1. Ładowanie z opóźnieniem nie jest domyślnie włączone i wymaga zainstalowania `Microsoft.EntityFrameworkCore.Proxies` . Podobnie jak w przypadku jawnego ładowania, ładowanie z opóźnieniem powinno być zwykle wyłączone dla aplikacji sieci Web, ponieważ jego użycie spowoduje, że w każdym żądaniu sieci Web zostaną wykonane dodatkowe zapytania bazy danych. Niestety, narzuty związane z ładowaniem opóźnionym często są niezauważalne w czasie projektowania, gdy opóźnienie jest małe i często zestawy danych używane do testowania są małe. Jednak w środowisku produkcyjnym, z większą liczbą użytkowników, większą ilością danych i większym opóźnieniu, dodatkowe żądania bazy danych mogą być często przyczyną niskiej wydajności aplikacji sieci Web, które intensywnie wykorzystują ładowanie z opóźnieniem.

[Unikaj załadowania jednostek w aplikacjach sieci Web](https://ardalis.com/avoid-lazy-loading-entities-in-asp-net-applications)

### <a name="encapsulating-data"></a>Hermetyzowanie danych

EF Core obsługuje kilka funkcji, które umożliwiają modelowi prawidłowe hermetyzację stanu. Typowym problemem w modelach domen jest ujawnienie przez nich właściwości nawigacji kolekcji jako typy list dostępnych publicznie. Ten problem umożliwia jakiemukolwiek współpracownikowi manipulowanie zawartością tych typów kolekcji, co może spowodować obejście ważnych reguł firmy związanych z kolekcją, prawdopodobnie pozostawiając obiekt w nieprawidłowym stanie. Rozwiązaniem tego problemu jest ujawnienie dostępu tylko do odczytu do powiązanych kolekcji i jawne udostępnienie metod definiujących sposoby manipulowania nimi przez klientów, jak w tym przykładzie:

```csharp
public class Basket : BaseEntity
{
    public string BuyerId { get; set; }
    private readonly List<BasketItem> _items = new List<BasketItem>();
    public IReadOnlyCollection<BasketItem> Items => _items.AsReadOnly();

    public void AddItem(int catalogItemId, decimal unitPrice, int quantity = 1)
    {
        if (!Items.Any(i => i.CatalogItemId == catalogItemId))
        {
            _items.Add(new BasketItem()
            {
                CatalogItemId = catalogItemId,
                Quantity = quantity,
                UnitPrice = unitPrice
            });
            return;
        }
        var existingItem = Items.FirstOrDefault(i => i.CatalogItemId == catalogItemId);
        existingItem.Quantity += quantity;
    }
}
```

Ten typ jednostki nie uwidacznia publicznej `List` lub `ICollection` właściwości, ale zamiast tego ujawnia `IReadOnlyCollection` Typ, który otacza bazowego typu listy. Korzystając z tego wzorca, można wskazać, aby Entity Framework Core, aby użyć pola zapasowego, takiego jak:

```csharp
private void ConfigureBasket(EntityTypeBuilder<Basket> builder)
{
    var navigation = builder.Metadata.FindNavigation(nameof(Basket.Items));

    navigation.SetPropertyAccessMode(PropertyAccessMode.Field);
}
```

Innym sposobem, w którym można poprawić model domeny, jest użycie obiektów wartości dla typów, które nie mają tożsamości i są rozróżniane przez ich właściwości. Użycie takich typów jako właściwości jednostek może pomóc w utrzymaniu logiki specyficznej dla obiektu wartości, do którego należy, i może uniknąć zduplikowanej logiki między wieloma jednostkami, które korzystają z tego samego pojęcia. W Entity Framework Core można utrwalać obiekty wartości w tej samej tabeli co ich jednostka będąca właścicielem przez skonfigurowanie typu jako jednostki należącej, na przykład:

```csharp
private void ConfigureOrder(EntityTypeBuilder<Order> builder)
{
    builder.OwnsOne(o => o.ShipToAddress);
}
```

W tym przykładzie `ShipToAddress` Właściwość jest typu `Address` . `Address` jest obiektem wartości z kilkoma właściwościami, takimi jak `Street` i `City` . EF Core mapuje `Order` obiekt na tabelę z jedną kolumną na `Address` Właściwość, dodając prefiks nazwy każdej kolumny przy użyciu nazwy właściwości. W tym przykładzie `Order` tabela będzie zawierać kolumny, takie jak `ShipToAddress_Street` i `ShipToAddress_City` . Istnieje również możliwość przechowywania typów posiadanych w oddzielnych tabelach, w razie potrzeby.

Dowiedz się więcej o [obsłudze jednostek należących do EF Core](/ef/core/modeling/owned-entities).

### <a name="resilient-connections"></a>Odporne połączenia

Zasoby zewnętrzne, takie jak bazy danych SQL, mogą być czasami niedostępne. W przypadku tymczasowej niedostępności aplikacje mogą używać logiki ponawiania, aby uniknąć ponoszenia wyjątku. Ta technika jest często określana jako _odporność połączenia_. Możesz zaimplementować [własne ponowienie próby przy użyciu wykładniczej techniki wycofywania](/azure/architecture/patterns/retry) , próbując ponowić próbę przy użyciu wykładniczego wzrostu czasu oczekiwania, dopóki nie zostanie osiągnięta maksymalna liczba ponownych prób. Ta technika obejmuje fakt, że zasoby chmury mogą sporadycznie być niedostępne przez krótki okresy, co powoduje niepowodzenie niektórych żądań.

W przypadku usługi Azure SQL DB Entity Framework Core już zapewnia odporność połączenia wewnętrznej bazy danych i logikę ponawiania. Należy jednak włączyć strategię wykonywania Entity Framework dla każdego połączenia DbContext, jeśli chcesz mieć odporne EF Core połączenia.

Na przykład poniższy kod na poziomie połączenia EF Core włącza odporne połączenia SQL, które są ponawiane, jeśli połączenie nie powiedzie się.

```csharp
// Startup.cs from any ASP.NET Core Web API
public class Startup
{
    public IServiceProvider ConfigureServices(IServiceCollection services)
    {
        //...
        services.AddDbContext<OrderingContext>(options =>
        {
            options.UseSqlServer(Configuration["ConnectionString"],
            sqlServerOptionsAction: sqlOptions =>
        {
            sqlOptions.EnableRetryOnFailure(
            maxRetryCount: 5,
            maxRetryDelay: TimeSpan.FromSeconds(30),
            errorNumbersToAdd: null);
        });
    });
}
//...
```

#### <a name="execution-strategies-and-explicit-transactions-using-begintransaction-and-multiple-dbcontexts"></a>Strategie wykonywania i jawne transakcje przy użyciu BeginTransaction i wielu dbcontexts

Po włączeniu ponownych prób w EF Core połączeniach każda operacja wykonywana przy użyciu EF Core będzie własną operacją ponawiania. Każde zapytanie i każde wywołanie do metody SaveChanges zostanie ponowione w przypadku wystąpienia błędu przejściowego.

Jeśli jednak kod inicjuje transakcję przy użyciu BeginTransaction, definiujesz własną grupę operacji, która musi być traktowana jako jednostka; Jeśli wystąpi awaria, wszystkie elementy wewnątrz transakcji należy wycofać. Jeśli spróbujesz wykonać tę transakcję podczas korzystania z strategii wykonywania EF (zasady ponawiania), zostanie wyświetlony wyjątek, który będzie zawierał kilka metody SaveChanges z wielu dbcontexts.

System. InvalidOperationException: skonfigurowana strategia wykonywania "SqlServerRetryingExecutionStrategy" nie obsługuje transakcji inicjowanych przez użytkownika. Użyj strategii wykonywania zwróconej przez obiekt "DbContext. Database. CreateExecutionStrategy ()", aby wykonać wszystkie operacje w transakcji jako jednostkę, którą można ponowić.

Rozwiązaniem jest ręczne Wywołaj strategię wykonywania EF z delegatem reprezentującym wszystkie elementy, które należy wykonać. Jeśli wystąpi błąd przejściowy, strategia wykonywania ponownie wywoła delegata. Poniższy kod przedstawia sposób wdrożenia tego podejścia:

```csharp
// Use of an EF Core resiliency strategy when using multiple DbContexts
// within an explicit transaction
// See:
// https://docs.microsoft.com/ef/core/miscellaneous/connection-resiliency
var strategy = _catalogContext.Database.CreateExecutionStrategy();
await strategy.ExecuteAsync(async () =>
{
    // Achieving atomicity between original Catalog database operation and the
    // IntegrationEventLog thanks to a local transaction
    using (var transaction = _catalogContext.Database.BeginTransaction())
    {
        _catalogContext.CatalogItems.Update(catalogItem);
        await _catalogContext.SaveChangesAsync();

        // Save to EventLog only if product price changed
        if (raiseProductPriceChangedEvent)
            await _integrationEventLogService.SaveEventAsync(priceChangedEvent);
        transaction.Commit();
    }
});
```

Pierwszy DbContext to catalogContext, \_ a drugi DbContext znajduje się w \_ obiekcie integrationEventLogService. Na koniec akcja zatwierdzania będzie wykonywana z wieloma kontekstami DbContext i przy użyciu strategii wykonywania EF.

> ### <a name="references--entity-framework-core"></a>Odwołania — Entity Framework Core
>
> - **Dokumentacja EF Core**
>   <https://docs.microsoft.com/ef/>
> - **EF Core: powiązane dane**
>   <https://docs.microsoft.com/ef/core/querying/related-data>
> - **Unikaj powolnych jednostek ładowania w aplikacjach ASPNET**
>   <https://ardalis.com/avoid-lazy-loading-entities-in-asp-net-applications>

## <a name="ef-core-or-micro-orm"></a>EF Core lub mikro-ORM?

Chociaż EF Core to doskonały wybór w zakresie zarządzania trwałością, a w większości przypadków dane bazy danych są hermetyzowane przez deweloperów aplikacji, nie jest to jedyne rozwiązanie. Kolejną popularną alternatywą typu "open source" jest [Dapper](https://github.com/StackExchange/Dapper), a więc nazywamy mikro-ORM. Mikro-ORM to lekkie, mniej funkcjonalne narzędzie do mapowania obiektów do struktur danych. W przypadku Dapper, jego cele projektowe koncentrują się na wydajności, a nie w pełni hermetyzowaniu podstawowych zapytań używanych do pobierania i aktualizowania danych. Ponieważ nie jest to abstrakcyjny kod SQL od dewelopera, Dapper jest "bliżej metalu" i umożliwia deweloperom pisanie dokładnych zapytań, których chcą używać dla danej operacji dostępu do danych.

EF Core ma dwie znaczące funkcje, które zapewnia oddzielenie go od Dapper, ale również zwiększenie wydajności. Pierwszy to tłumaczenie z wyrażeń LINQ do SQL. Te tłumaczenia są przechowywane w pamięci podręcznej, ale nawet wtedy, gdy są wykonywane po raz pierwszy. Druga funkcja śledzenia zmian w jednostkach (tak, aby można było generować wydajne instrukcje Update). To zachowanie można wyłączyć dla konkretnych zapytań przy użyciu <xref:System.Data.Entity.DbExtensions.AsNoTracking%2A> rozszerzenia. EF Core generuje również zapytania SQL, które zwykle są bardzo wydajne i w każdym przypadku idealnie akceptowalne z punktu widzenia wydajności, ale jeśli potrzebujesz precyzyjnej kontroli nad precyzyjnym zapytaniem, można przekazać niestandardowe SQL (lub wykonać procedurę składowaną) przy użyciu EF Core. W takim przypadku Dapper nadal wykonuje EF Core, ale tylko nieco. Julie Lerman przedstawia pewne dane dotyczące wydajności, które mogą być 2016 artykułów MSDN [Dapper, Entity Framework i hybrydowych](/archive/msdn-magazine/2016/may/data-points-dapper-entity-framework-and-hybrid-apps). Dodatkowe dane porównawcze wydajności dla różnych metod dostępu do danych można znaleźć w [witrynie Dapper](https://github.com/StackExchange/Dapper).

Aby zobaczyć, jak składnia Dapper różni się od EF Core, należy wziąć pod uwagę te dwie wersje tej samej metody do pobierania listy elementów:

```csharp
// EF Core
private readonly CatalogContext _context;
public async Task<IEnumerable<CatalogType>> GetCatalogTypes()
{
    return await _context.CatalogTypes.ToListAsync();
}

// Dapper
private readonly SqlConnection _conn;
public async Task<IEnumerable<CatalogType>> GetCatalogTypesWithDapper()
{
    return await _conn.QueryAsync<CatalogType>("SELECT * FROM CatalogType");
}
```

Jeśli konieczne jest skompilowanie bardziej złożonych grafów obiektów za pomocą Dapper, należy napisać powiązane zapytania samodzielnie (w przeciwieństwie do dodania dołączenia w EF Core). Ta funkcja jest obsługiwana za pomocą różnych składni, w tym funkcji o nazwie mapowanie wielokrotne, która umożliwia mapowanie poszczególnych wierszy na wiele mapowanych obiektów. Na przykład, jeśli dane wpisu klasy są właścicielami właściwości typu użytkownika, następujące SQL zwróci wszystkie niezbędne dane:

```sql
select * from #Posts p
left join #Users u on u.Id = p.OwnerId
Order by p.Id
```

Każdy zwrócony wiersz zawiera dane użytkownika i danych post. Ponieważ dane użytkownika powinny być dołączone do danych post za pośrednictwem jego właściwości Owner, używana jest następująca funkcja:

```csharp
(post, user) => { post.Owner = user; return post; }
```

Pełen kod, który ma zwracać kolekcję wpisów wraz z ich właściwością Owner, wypełnionymi danymi użytkownika:

```csharp
var sql = @"select * from #Posts p
left join #Users u on u.Id = p.OwnerId
Order by p.Id";
var data = connection.Query<Post, User, Post>(sql,
(post, user) => { post.Owner = user; return post;});
```

Ponieważ oferuje mniej hermetyzacji, Dapper wymaga, aby deweloperzy wiedzieli, jak ich dane są przechowywane, jak wykonywać zapytania efektywnie i pisać więcej kodu w celu pobrania go. Gdy model ulegnie zmianie, zamiast po prostu utworzyć nową migrację (inną funkcję EF Core) i/lub zaktualizować informacje o mapowaniu w jednym miejscu w DbContext, należy zaktualizować wszystkie zapytania, na które ma wpływ. Te zapytania nie mają gwarancji w czasie kompilacji, więc mogą być przerywane w czasie wykonywania w odpowiedzi na zmiany modelu lub bazy danych, co sprawia, że błędy są trudniejsze do wykrycia szybko. W programie Exchange dla tych kompromisów Dapper oferuje bardzo szybką wydajność.

W przypadku większości aplikacji i większości części prawie wszystkich aplikacji EF Core oferuje akceptowalną wydajność. W ten sposób korzyści związane z produktywnością dla deweloperów mogą przeważyć wydajność. W przypadku zapytań, które mogą korzystać z buforowania, rzeczywiste zapytanie może być wykonywane tylko przez niewielki procent czasu, co powoduje stosunkowo małe różnice wydajności zapytań Moot.

## <a name="sql-or-nosql"></a>SQL lub NoSQL

Tradycyjnie relacyjne bazy danych, takie jak SQL Server, korzystają z witryny Marketplace na potrzeby trwałego magazynowania danych, ale nie są jedynymi dostępnymi rozwiązaniami. Bazy danych NoSQL, takie jak [MongoDB](https://www.mongodb.com/what-is-mongodb) , oferują inne podejście do przechowywania obiektów. Zamiast mapowania obiektów do tabel i wierszy, kolejną opcją jest Serializacja całego wykresu obiektów i przechowywanie wyniku. Zalety tego podejścia, co najmniej początkowo, są prostoty i wydajności. Prostszym sposobem jest przechowywanie pojedynczego serializowanego obiektu z kluczem niż w celu rozdzielenia obiektu na wiele tabel z relacjami i aktualizacji oraz wierszy, które mogły ulec zmianie od czasu ostatniego pobrania obiektu z bazy danych. Podobnie pobieranie i deserializacja pojedynczego obiektu z magazynu opartego na kluczach jest zwykle znacznie szybsze i łatwiejsze niż złożone sprzężenia lub wiele zapytań bazy danych wymaganych do pełnego zredagowania tego samego obiektu z relacyjnej bazy danych. Brak blokad lub transakcji lub stały schemat sprawia również, że bazy danych NoSQL mogą być skalowane na wielu maszynach i obsługują bardzo duże zestawy danych.

Z drugiej strony bazy danych NoSQL (jak są zwykle wywoływane) mają swoje wady. Relacyjne bazy danych wykorzystują normalizację w celu wymuszenia spójności i uniknięcia duplikowania danych. Takie podejście zmniejsza łączny rozmiar bazy danych i gwarantuje, że aktualizacje udostępnionych danych będą dostępne bezpośrednio w całej bazie danych. W relacyjnej bazie danych tabela adresów może odwoływać się do tabeli kraju według identyfikatora, w taki sposób, że jeśli nazwa kraju/regionu została zmieniona, rekordy adresów byłyby korzystne dla aktualizacji, które nie będą musiały zostać zaktualizowane. Jednak w NoSQL bazie danych, adres i skojarzony z nim kraj mogą być serializowane w ramach wielu przechowywanych obiektów. Aktualizacja nazwy kraju/regionu wymagała aktualizacji wszystkich takich obiektów, a nie jednego wiersza. Relacyjne bazy danych mogą również zapewnić relacyjną integralność, wymuszając reguły, takie jak klucze obce. Bazy danych NoSQL zazwyczaj nie oferują takich ograniczeń dla swoich danych.

Inne bazy danych NoSQL złożoności muszą zająć się przechowywaniem wersji. Zmiany właściwości obiektu mogą nie być możliwe do deserializacji z wcześniejszych wersji, które były przechowywane. W ten sposób wszystkie istniejące obiekty, które mają serializowaną (poprzednią) wersję obiektu, muszą zostać zaktualizowane, aby były zgodne ze swoim nowym schematem. Ta metoda nie różni się koncepcyjnie od relacyjnej bazy danych, gdzie zmiany schematu czasami wymagają skryptów aktualizacji lub mapowania aktualizacji. Jednak liczba wpisów, które muszą zostać zmodyfikowane, jest często znacznie większa w podejściu NoSQL, ponieważ istnieje więcej duplikacji danych.

Istnieje możliwość, że w bazach danych NoSQL są przechowywane wiele wersji obiektów, ale nie są zwykle obsługiwane. Jednak w tym przypadku kod aplikacji będzie musiał uwzględnić istnienie poprzednich wersji obiektów, co zwiększa złożoność.

Bazy danych NoSQL zazwyczaj nie wymuszają stosowania [kwasów](https://en.wikipedia.org/wiki/ACID), co oznacza, że mają one zalety wydajności i skalowalności w porównaniu z relacyjnymi bazami danych. Doskonale nadają się do bardzo dużych zestawów danych i obiektów, które nie są dobrze dopasowane do magazynu w znormalizowanych strukturach tabel. Nie ma powodów, dla których pojedyncze aplikacje nie mogą korzystać z baz danych relacyjnych i NoSQL, przy użyciu każdego z nich, gdzie jest najlepiej dopasowany.

## <a name="azure-cosmos-db"></a>Azure Cosmos DB

Azure Cosmos DB to w pełni zarządzana usługa bazy danych NoSQL, która oferuje oparty na chmurze magazyn danych bez schematu. Azure Cosmos DB został zbudowany w celu uzyskania szybkiej i przewidywalnej wydajności, wysokiej dostępności, elastycznego skalowania i globalnej dystrybucji. Mimo że nie jest to baza danych NoSQL, deweloperzy mogą korzystać z zaawansowanych i znanych funkcji zapytań SQL dotyczących danych JSON. Wszystkie zasoby w Azure Cosmos DB są przechowywane jako dokumenty JSON. Zasoby są zarządzane jako _elementy_, które są dokumentami zawierającymi metadane, a także _źródła danych_, które są kolekcjami elementów. Rysunek 8-2 przedstawia relację między różnymi zasobami Azure Cosmos DB.

![Hierarchiczna relacja między zasobami w Azure Cosmos DB, baza danych JSON NoSQL](./media/image8-2.png)

**Rysunek 8-2.** Organizacja zasobów Azure Cosmos DB.

Język zapytań Azure Cosmos DB to prosty, jeszcze zaawansowany interfejs do wykonywania zapytań w dokumentach JSON. Język obsługuje podzbiór gramatyki ANSI SQL i dodaje głęboką integrację obiektów, tablic, konstrukcji obiektów i wywoływania funkcji języka JavaScript.

**Odwołania — Azure Cosmos DB**

- Azure Cosmos DB wprowadzenie <https://docs.microsoft.com/azure/cosmos-db/introduction>

## <a name="other-persistence-options"></a>Inne opcje trwałości

Oprócz opcji magazynu relacyjnego i NoSQL aplikacje ASP.NET Core mogą używać usługi Azure Storage do przechowywania różnorodnych formatów danych i plików w sposób skalowalny w chmurze. Usługa Azure Storage jest wysoce skalowalna, co pozwala na rozpoczęcie przechowywania małych ilości danych i skalowanie w górę w celu przechowywania setek lub terabajtów, jeśli aplikacja tego wymaga. Usługa Azure Storage obsługuje cztery rodzaje danych:

- Blob Storage dla magazynu tekstowego lub binarnego bez struktury, nazywanego również magazynem obiektów.

- Table Storage dla zestawów danych ze strukturą, dostępne za pośrednictwem kluczy wierszy.

- Queue Storage dla niezawodnej obsługi komunikatów na podstawie kolejki.

- File Storage dostępu do udostępnionego pliku między maszynami wirtualnymi platformy Azure i aplikacjami lokalnymi.

**Odwołania — Azure Storage**

- Wprowadzenie do usługi Azure Storage <https://docs.microsoft.com/azure/storage/common/storage-introduction>

## <a name="caching"></a>Buforowanie

W aplikacjach internetowych każde żądanie sieci Web powinno być wykonywane w najkrótszym możliwym czasie. Jednym ze sposobów osiągnięcia tej funkcji jest ograniczenie liczby wywołań zewnętrznych, które serwer musi wykonać, aby zakończyć żądanie. Buforowanie obejmuje przechowywanie kopii danych na serwerze (lub w innym magazynie danych, który jest bardziej czytelny niż źródło danych). Aplikacje sieci Web, a w szczególności niespa tradycyjne aplikacje sieci Web, muszą kompilować cały interfejs użytkownika przy użyciu każdego żądania. Takie podejście często polega na tym, że wiele z tych samych kwerend bazy danych jest wielokrotnie powtarzanych z jednego żądania użytkownika do następnego. W większości przypadków te zmiany danych są rzadko zmieniane, więc istnieje nieco powód, aby ciągle zażądać ich z bazy danych. ASP.NET Core obsługuje buforowanie odpowiedzi, do buforowania całych stron i buforowania danych, co zapewnia bardziej szczegółowe zachowanie buforowania.

Podczas implementowania buforowania należy pamiętać o rozdzieleniu obaw. Unikaj implementowania logiki buforowania w logice dostępu do danych lub w interfejsie użytkownika. Zamiast tego hermetyzowaj buforowanie we własnych klasach i używaj konfiguracji do zarządzania zachowaniem. Takie podejście następuje zgodnie z zasadami dotyczącymi otwartych/zamkniętych i pojedynczych odpowiedzialności. ułatwi to zarządzanie sposobem korzystania z pamięci podręcznej w aplikacji podczas jej rozszerzania.

### <a name="aspnet-core-response-caching"></a>Buforowanie odpowiedzi ASP.NET Core

ASP.NET Core obsługuje dwa poziomy buforowania odpowiedzi. Pierwszy poziom nie buforuje żadnych elementów na serwerze, ale dodaje nagłówki HTTP, które instruują klientów i serwery proxy w celu buforowania odpowiedzi. Ta funkcja jest implementowana przez dodanie atrybutu ResponseCache do poszczególnych kontrolerów lub akcji:

```csharp
[ResponseCache(Duration = 60)]
public IActionResult Contact()
{
    ViewData["Message"] = "Your contact page.";
    return View();
}
```

W poprzednim przykładzie zostanie dodany następujący nagłówek do odpowiedzi, co powoduje, że klienci buforują wynik przez maksymalnie 60 sekund.

Cache-Control: Public, max-age = 60

Aby dodać pamięć podręczną po stronie serwera do aplikacji, należy odwołać się do pakietu NuGet Microsoft. AspNetCore. ResponseCaching, a następnie dodać oprogramowanie pośredniczące buforowania odpowiedzi. To oprogramowanie pośredniczące jest konfigurowane zarówno w ConfigureServices, jak i w trakcie uruchamiania:

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddResponseCaching();
}

public void Configure(IApplicationBuilder app)
{
    app.UseResponseCaching();
}
```

Oprogramowanie pośredniczące buforowania odpowiedzi automatycznie buforuje odpowiedzi na podstawie zestawu warunków, które można dostosować. Domyślnie tylko odpowiedzi 200 (OK) wymagane przez metody GET lub z pamięci podręcznej są buforowane. Ponadto żądania muszą mieć odpowiedź w nagłówku Cache-Control: Public i nie mogą zawierać nagłówków autoryzacji lub Set-cookie. Zapoznaj się z [pełną listą warunków buforowania używanych przez oprogramowanie pośredniczące buforowania odpowiedzi](/aspnet/core/performance/caching/middleware#conditions-for-caching).

### <a name="data-caching"></a>Buforowanie danych

Zamiast (lub oprócz) buforowania pełnych odpowiedzi sieci Web, można buforować wyniki poszczególnych zapytań dotyczących danych. W przypadku tej funkcji można użyć usługi do buforowania pamięci na serwerze sieci Web lub użyć [rozproszonej pamięci podręcznej](/aspnet/core/performance/caching/distributed). W tej sekcji pokazano, jak zaimplementować program w pamięci podręcznej.

Dodano obsługę buforowania pamięci (lub rozproszonego) w ConfigureServices:

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMemoryCache();
    services.AddMvc();
}
```

Pamiętaj, aby dodać również pakiet NuGet Microsoft. Extensions. buforowanie. Memory.

Po dodaniu usługi żądanie IMemoryCache za pośrednictwem iniekcji zależności wszędzie tam, gdzie trzeba uzyskać dostęp do pamięci podręcznej. W tym przykładzie CachedCatalogService korzysta ze wzorca projektowego serwera proxy (lub dekoratora), dostarczając alternatywną implementację ICatalogService, która kontroluje dostęp do (lub dodaje zachowanie do) bazowej implementacji CatalogService.

```csharp
public class CachedCatalogService : ICatalogService
{
    private readonly IMemoryCache _cache;
    private readonly CatalogService _catalogService;
    private static readonly string _brandsKey = "brands";
    private static readonly string _typesKey = "types";
    private static readonly TimeSpan _defaultCacheDuration = TimeSpan.FromSeconds(30);
    public CachedCatalogService(IMemoryCache cache,
    CatalogService catalogService)
    {
        _cache = cache;
        _catalogService = catalogService;
    }

    public async Task<IEnumerable<SelectListItem>> GetBrands()
    {
        return await _cache.GetOrCreateAsync(_brandsKey, async entry =>
        {
            entry.SlidingExpiration = _defaultCacheDuration;
            return await _catalogService.GetBrands();
        });
    }

    public async Task<Catalog> GetCatalogItems(int pageIndex, int itemsPage, int? brandID, int? typeId)
    {
        string cacheKey = $"items-{pageIndex}-{itemsPage}-{brandID}-{typeId}";
        return await _cache.GetOrCreateAsync(cacheKey, async entry =>
        {
            entry.SlidingExpiration = _defaultCacheDuration;
            return await _catalogService.GetCatalogItems(pageIndex, itemsPage, brandID, typeId);
        });
    }

    public async Task<IEnumerable<SelectListItem>> GetTypes()
    {
        return await _cache.GetOrCreateAsync(_typesKey, async entry =>
        {
            entry.SlidingExpiration = _defaultCacheDuration;
            return await _catalogService.GetTypes();
        });
    }
}
```

Aby skonfigurować aplikację do korzystania z buforowanej wersji usługi, ale nadal zezwolić usłudze na uzyskanie wystąpienia CatalogService, które jest potrzebne w jego konstruktorze, Dodaj następujące wiersze w ConfigureServices:

```csharp
services.AddMemoryCache();
services.AddScoped<ICatalogService, CachedCatalogService>();
services.AddScoped<CatalogService>();
```

W przypadku tego kodu program wywołuje pobieranie danych wykazu tylko raz na minutę, a nie na każdym żądaniu. W zależności od ruchu do lokacji może to mieć znaczny wpływ na liczbę zapytań wykonywanych w bazie danych oraz średni czas ładowania strony dla strony głównej, który jest obecnie zależny od wszystkich trzech zapytań narażonych na tę usługę.

Problem, który powstaje, gdy buforowanie jest zaimplementowane, to _dane nieodświeżone_ — czyli dane, które uległy zmianie w źródle, ale w pamięci podręcznej pozostaje nieaktualna wersja. Prostym sposobem na ograniczenie tego problemu jest użycie małych okresów pamięci podręcznej, ponieważ w przypadku zajętej aplikacji istnieje ograniczone dodatkowe korzyści umożliwiające rozszerzanie danych długości. Rozważmy na przykład stronę, która tworzy zapytanie pojedynczej bazy danych i żąda 10 razy na sekundę. Jeśli ta strona jest buforowana przez jedną minutę, spowoduje to liczbę zapytań bazy danych wykonanych na minutę do porzucenia z 600 do 1, zmniejszenie 99,8%. Jeśli zamiast tego czas trwania pamięci podręcznej został wykonany jedną godzinę, ogólna obniżka wynosi 99,997%, ale teraz prawdopodobieństwo i potencjalny wiek starych danych są znacznie większe.

Innym podejściem jest proaktywnie Usuwanie wpisów pamięci podręcznej po zaktualizowaniu zawartych w nich danych. Każdy wpis można usunąć, jeśli jego klucz jest znany:

```csharp
_cache.Remove(cacheKey);
```

Jeśli aplikacja ujawnia funkcje do aktualizowania wpisów, które są buforowane, można usunąć odpowiednie wpisy pamięci podręcznej w kodzie, który wykonuje aktualizacje. Czasami może istnieć wiele różnych wpisów, które są zależne od określonego zestawu danych. W takim przypadku może być przydatne do tworzenia zależności między wpisami pamięci podręcznej przy użyciu CancellationChangeToken. Za pomocą CancellationChangeToken można wycofać wiele wpisów w pamięci podręcznej naraz, anulując token.

```csharp
// configure CancellationToken and add entry to cache
var cts = new CancellationTokenSource();
_cache.Set("cts", cts);
_cache.Set(cacheKey,
itemToCache,
new CancellationChangeToken(cts.Token));

// elsewhere, expire the cache by cancelling the token\
_cache.Get<CancellationTokenSource>("cts").Cancel();
```

Buforowanie może znacząco poprawić wydajność stron sieci Web, które wielokrotnie żądają tych samych wartości z bazy danych. Należy pamiętać, aby zmierzyć dostęp do danych i wydajność stron przed zastosowaniem buforowania, i zastosować buforowanie tylko w przypadku, gdy zobaczysz potrzebę ulepszenia. Buforowanie zużywa zasoby pamięci serwera sieci Web i zwiększa złożoność aplikacji, dlatego ważne jest, aby nie zoptymalizować się za pomocą tej techniki.

## <a name="getting-data-to-no-locblazor-no-locwebassembly-apps"></a>Pobieranie danych do Blazor WebAssembly aplikacji

W przypadku tworzenia aplikacji korzystających z Blazor serwera można używać Entity Framework i innych technologii bezpośredniego dostępu do danych, ponieważ zostały one omówione w tym rozdziale w tym zakresie. Jednak podczas kompilowania Blazor WebAssembly aplikacji, takich jak inne platformy Spa, będzie potrzebna inna Strategia dostępu do danych. Zazwyczaj te aplikacje uzyskują dostęp do danych i współpracują z serwerem za pomocą punktów końcowych interfejsu API sieci Web.

Jeśli wykonywane dane lub operacje są poufne, należy zapoznać się z sekcją zabezpieczenia w [poprzednim rozdziale](develop-asp-net-core-mvc-apps.md) i chronić interfejsy API przed nieautoryzowanym dostępem.

Przykład aplikacji można znaleźć Blazor WebAssembly w [aplikacji eShopOnWeb Reference](https://github.com/dotnet-architecture/eShopOnWeb)w Blazor projekcie administratora. Ten projekt jest hostowany w projekcie sieci Web eShopOnWeb i umożliwia użytkownikom z grupy administratorów Zarządzanie elementami w sklepie. Zrzut ekranu aplikacji można zobaczyć na rysunku 8-3.

![Zrzut ekranu administratora katalogu eShopOnWeb](./media/image8-3.jpg)

**Rysunek 8-3.** Zrzut ekranu administratora katalogu eShopOnWeb.

Podczas pobierania danych z interfejsów API sieci Web w Blazor WebAssembly aplikacji wystarczy użyć wystąpienia `HttpClient` tak samo jak w przypadku dowolnej aplikacji .NET. Podstawowe kroki polegają na utworzeniu żądania wysłania (jeśli to konieczne, zazwyczaj w przypadku żądań POST lub PUT), od samego żądania, sprawdzenia kodu stanu i deserializacji odpowiedzi. Jeśli zamierzasz wykonać wiele żądań do danego zestawu interfejsów API, warto hermetyzować interfejsy API i konfigurować `HttpClient` adres podstawowy centralnie. W ten sposób, jeśli musisz dostosować dowolne z tych ustawień między środowiskami, możesz wprowadzić zmiany w jednym miejscu. Obsługę tej usługi należy dodać w programie `Program.Main` :

```csharp
builder.Services.AddScoped(sp =>
    new HttpClient
    {
        BaseAddress = new Uri(builder.HostEnvironment.BaseAddress)
    });
```

Aby bezpiecznie uzyskać dostęp do usług, należy uzyskać dostęp do bezpiecznego tokenu i skonfigurować `HttpClient` do przekazywania tego tokenu jako nagłówek uwierzytelniania przy każdym żądaniu:

```csharp
_httpClient.DefaultRequestHeaders.Authorization =
    new AuthenticationHeaderValue("Bearer", token);
```

To działanie można wykonać z dowolnego składnika, który został wprowadzony `HttpClient` do niego, pod warunkiem, że `HttpClient` nie został dodany do usług aplikacji z `Transient` okresem istnienia. Każde odwołanie do `HttpClient` w aplikacji odwołuje się do tego samego wystąpienia, więc zmiany w nim w jednym przepływie składnika przez całą aplikację. Dobrym miejscem do wykonania tego sprawdzenia uwierzytelniania (po określeniu tokenu) jest składnik współużytkowany, taki jak główna Nawigacja dla witryny. Dowiedz się więcej na temat tego podejścia w `BlazorAdmin` projekcie w [aplikacji eShopOnWeb Reference](https://github.com/dotnet-architecture/eShopOnWeb).

Jedną z korzyści w Blazor WebAssembly porównaniu do tradycyjnych aplikacji jednostronicowych języka JavaScript jest to, że nie trzeba przechowywać zsynchronizowanych kopii obiektów transferów danych (DTO). Projekt Blazor WebAssembly i projekt interfejsu API sieci Web mogą współużytkować ten sam DTO w wspólnym projekcie udostępnionym. Takie podejście eliminuje pewne tarcie dotyczące opracowywania aplikacji jednostronicowych.

Aby szybko pobrać dane z punktu końcowego interfejsu API, można użyć wbudowanej metody pomocnika `GetFromJsonAsync` . Istnieją podobne metody dla wpisów POST, PUT itp. Poniżej pokazano, jak uzyskać CatalogItem z punktu końcowego interfejsu API przy użyciu skonfigurowanej `HttpClient` w Blazor WebAssembly aplikacji:

```csharp
var item = await _httpClient.GetFromJsonAsync<CatalogItem>($"catalog-items/{id}");
```

Gdy masz potrzebne dane, zazwyczaj śledźsz zmiany lokalnie. Jeśli chcesz zaktualizować magazyn danych zaplecza, w tym celu wywołaj dodatkowe interfejsy API sieci Web.

**References — Blazor dane**

- Wywoływanie internetowego interfejsu API z ASP.NET Core Blazor
  <https://docs.microsoft.com/aspnet/core/blazor/call-web-api>

>[!div class="step-by-step"]
>[Poprzedni](develop-asp-net-core-mvc-apps.md) 
> [Dalej](test-asp-net-core-mvc-apps.md)
