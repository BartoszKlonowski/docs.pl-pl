---
title: Pracuj z danymi w aplikacjach ASP.NET Core
description: Tworzenie architektury nowoczesnych aplikacji sieci Web przy użyciu ASP.NET Core i platformy Azure | Praca z danymi w aplikacjach ASP.NET Core
author: ardalis
ms.author: wiwagn
ms.date: 01/30/2019
ms.openlocfilehash: 3b251003a2da998936a11acff3cc2975c4b78838
ms.sourcegitcommit: c70542d02736e082e8dac67dad922c19249a8893
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/05/2019
ms.locfileid: "70373995"
---
# <a name="working-with-data-in-aspnet-core-apps"></a><span data-ttu-id="7c957-103">Praca z danymi w aplikacjach ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="7c957-103">Working with Data in ASP.NET Core Apps</span></span>

> <span data-ttu-id="7c957-104">"Dane są cenne i będą trwać dłużej niż same systemy".</span><span class="sxs-lookup"><span data-stu-id="7c957-104">"Data is a precious thing and will last longer than the systems themselves."</span></span>
>
> <span data-ttu-id="7c957-105">Tim — Lewandowski</span><span class="sxs-lookup"><span data-stu-id="7c957-105">Tim Berners-Lee</span></span>

<span data-ttu-id="7c957-106">Dostęp do danych jest ważną częścią niemal każdej aplikacji oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="7c957-106">Data access is an important part of almost any software application.</span></span> <span data-ttu-id="7c957-107">ASP.NET Core obsługuje wiele opcji dostępu do danych, w tym Entity Framework Core (i Entity Framework 6), i może współdziałać z dowolnymi strukturami dostępu do danych platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="7c957-107">ASP.NET Core supports a variety of data access options, including Entity Framework Core (and Entity Framework 6 as well), and can work with any .NET data access framework.</span></span> <span data-ttu-id="7c957-108">Wybór struktury dostępu do danych, która ma być używana, zależy od potrzeb aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7c957-108">The choice of which data access framework to use depends on the application's needs.</span></span> <span data-ttu-id="7c957-109">Abstrakcję tych opcji z projektów ApplicationCore i interfejsów użytkownika oraz Hermetyzowanie szczegółów implementacji w infrastrukturze, pomaga w wytwarzaniu luźno sprzężonych, weryfikowalne oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="7c957-109">Abstracting these choices from the ApplicationCore and UI projects, and encapsulating implementation details in Infrastructure, helps to produce loosely coupled, testable software.</span></span>

## <a name="entity-framework-core-for-relational-databases"></a><span data-ttu-id="7c957-110">Entity Framework Core (dla relacyjnych baz danych)</span><span class="sxs-lookup"><span data-stu-id="7c957-110">Entity Framework Core (for relational databases)</span></span>

<span data-ttu-id="7c957-111">Jeśli piszesz nową aplikację ASP.NET Core, która musi pracować z danymi relacyjnymi, Entity Framework Core (EF Core) jest zalecanym sposobem, aby aplikacja mogła uzyskać dostęp do swoich danych.</span><span class="sxs-lookup"><span data-stu-id="7c957-111">If you're writing a new ASP.NET Core application that needs to work with relational data, then Entity Framework Core (EF Core) is the recommended way for your application to access its data.</span></span> <span data-ttu-id="7c957-112">EF Core to Mapowanie obiektowo-relacyjne (O/RM), które umożliwia deweloperom platformy .NET utrwalanie obiektów do i ze źródła danych.</span><span class="sxs-lookup"><span data-stu-id="7c957-112">EF Core is an object-relational mapper (O/RM) that enables .NET developers to persist objects to and from a data source.</span></span> <span data-ttu-id="7c957-113">Eliminuje to potrzebę większości deweloperów kodu dostępu do danych, zwykle trzeba pisać.</span><span class="sxs-lookup"><span data-stu-id="7c957-113">It eliminates the need for most of the data access code developers would typically need to write.</span></span> <span data-ttu-id="7c957-114">Podobnie jak ASP.NET Core, EF Core został ponownie zapisany od podstaw, aby obsługiwał modularne aplikacje dla wielu platform.</span><span class="sxs-lookup"><span data-stu-id="7c957-114">Like ASP.NET Core, EF Core has been rewritten from the ground up to support modular cross-platform applications.</span></span> <span data-ttu-id="7c957-115">Należy dodać je do aplikacji jako pakiet NuGet, skonfigurować ją w programie startowym i zażądać jej za pomocą iniekcji zależności wszędzie tam, gdzie jest potrzebna.</span><span class="sxs-lookup"><span data-stu-id="7c957-115">You add it to your application as a NuGet package, configure it in Startup, and request it through dependency injection wherever you need it.</span></span>

<span data-ttu-id="7c957-116">Aby użyć EF Core z bazą danych SQL Server, uruchom następujące polecenie interfejsu wiersza polecenia dotnet:</span><span class="sxs-lookup"><span data-stu-id="7c957-116">To use EF Core with a SQL Server database, run the following dotnet CLI command:</span></span>

```console
dotnet add package Microsoft.EntityFrameworkCore.SqlServer
```

<span data-ttu-id="7c957-117">Aby dodać obsługę źródła danych inMemory, na potrzeby testowania:</span><span class="sxs-lookup"><span data-stu-id="7c957-117">To add support for an InMemory data source, for testing:</span></span>

```console
dotnet add package Microsoft.EntityFrameworkCore.InMemory
```

### <a name="the-dbcontext"></a><span data-ttu-id="7c957-118">DbContext</span><span class="sxs-lookup"><span data-stu-id="7c957-118">The DbContext</span></span>

<span data-ttu-id="7c957-119">Aby można było korzystać z EF Core, należy podklasą <xref:Microsoft.EntityFrameworkCore.DbContext>.</span><span class="sxs-lookup"><span data-stu-id="7c957-119">To work with EF Core, you need a subclass of <xref:Microsoft.EntityFrameworkCore.DbContext>.</span></span> <span data-ttu-id="7c957-120">Ta klasa zawiera właściwości reprezentujące kolekcje jednostek, z którymi aplikacja będzie współdziałać.</span><span class="sxs-lookup"><span data-stu-id="7c957-120">This class holds properties representing collections of the entities your application will work with.</span></span> <span data-ttu-id="7c957-121">Przykład eShopOnWeb zawiera CatalogContext z kolekcjami dla elementów, marek i typów:</span><span class="sxs-lookup"><span data-stu-id="7c957-121">The eShopOnWeb sample includes a CatalogContext with collections for items, brands, and types:</span></span>

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

<span data-ttu-id="7c957-122">DbContext musi mieć konstruktora akceptującego DbContextOptions i przekazać ten argument do podstawowego konstruktora DbContext.</span><span class="sxs-lookup"><span data-stu-id="7c957-122">Your DbContext must have a constructor that accepts DbContextOptions and pass this argument to the base DbContext constructor.</span></span> <span data-ttu-id="7c957-123">Należy pamiętać, że jeśli w aplikacji jest tylko jeden DbContext, można przekazać wystąpienie elementu DbContextOptions, ale jeśli masz więcej niż jeden, należy użyć typu ogólnego DbContextOptions\<T >, przekazując w typ kontekstu dbjako parametr generyczny.</span><span class="sxs-lookup"><span data-stu-id="7c957-123">Note that if you have only one DbContext in your application, you can pass an instance of DbContextOptions, but if you have more than one you must use the generic DbContextOptions\<T> type, passing in your DbContext type as the generic parameter.</span></span>

### <a name="configuring-ef-core"></a><span data-ttu-id="7c957-124">Konfigurowanie EF Core</span><span class="sxs-lookup"><span data-stu-id="7c957-124">Configuring EF Core</span></span>

<span data-ttu-id="7c957-125">W aplikacji ASP.NET Core zwykle konfigurujesz EF Core w metodzie ConfigureServices.</span><span class="sxs-lookup"><span data-stu-id="7c957-125">In your ASP.NET Core application, you'll typically configure EF Core in your ConfigureServices method.</span></span> <span data-ttu-id="7c957-126">EF Core używa DbContextOptionsBuilder, który obsługuje kilka przydatnych metod rozszerzania w celu usprawnienia jego konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="7c957-126">EF Core uses a DbContextOptionsBuilder, which supports several helpful extension methods to streamline its configuration.</span></span> <span data-ttu-id="7c957-127">Aby skonfigurować CatalogContext do używania bazy danych SQL Server z parametrami połączenia zdefiniowanymi w konfiguracji, należy dodać następujący kod do ConfigureServices:</span><span class="sxs-lookup"><span data-stu-id="7c957-127">To configure CatalogContext to use a SQL Server database with a connection string defined in Configuration, you would add the following code to ConfigureServices:</span></span>

```csharp
services.AddDbContext<CatalogContext>(options => options.UseSqlServer (Configuration.GetConnectionString("DefaultConnection")));
```

<span data-ttu-id="7c957-128">Aby użyć bazy danych znajdującej się w pamięci:</span><span class="sxs-lookup"><span data-stu-id="7c957-128">To use the in-memory database:</span></span>

```csharp
services.AddDbContext<CatalogContext>(options =>
    options.UseInMemoryDatabase());
```

<span data-ttu-id="7c957-129">Po zainstalowaniu EF Core utworzyć typ elementu podrzędnego DbContext i skonfigurować go w ConfigureServices, możesz użyć EF Core.</span><span class="sxs-lookup"><span data-stu-id="7c957-129">Once you have installed EF Core, created a DbContext child type, and configured it in ConfigureServices, you are ready to use EF Core.</span></span> <span data-ttu-id="7c957-130">Możesz zażądać wystąpienia typu DbContext w dowolnej usłudze, która go potrzebuje, i rozpocząć pracę z utrwalonymi obiektami przy użyciu LINQ tak, jakby znajdowały się one po prostu w kolekcji.</span><span class="sxs-lookup"><span data-stu-id="7c957-130">You can request an instance of your DbContext type in any service that needs it, and start working with your persisted entities using LINQ as if they were simply in a collection.</span></span> <span data-ttu-id="7c957-131">EF Core Wykonuje translację wyrażeń LINQ na zapytania SQL w celu przechowywania i pobierania danych.</span><span class="sxs-lookup"><span data-stu-id="7c957-131">EF Core does the work of translating your LINQ expressions into SQL queries to store and retrieve your data.</span></span>

<span data-ttu-id="7c957-132">Możesz zobaczyć zapytania, EF Core jest wykonywane przez skonfigurowanie rejestratora i upewnienie się, że jego poziom jest ustawiony na co najmniej informacje, jak pokazano na rysunku 8-1.</span><span class="sxs-lookup"><span data-stu-id="7c957-132">You can see the queries EF Core is executing by configuring a logger and ensuring its level is set to at least Information, as shown in Figure 8-1.</span></span>

![Rejestrowanie EF Core zapytań do konsoli](./media/image8-1.png)

<span data-ttu-id="7c957-134">**Rysunek 8-1**.</span><span class="sxs-lookup"><span data-stu-id="7c957-134">**Figure 8-1**.</span></span> <span data-ttu-id="7c957-135">Rejestrowanie EF Core zapytań do konsoli</span><span class="sxs-lookup"><span data-stu-id="7c957-135">Logging EF Core queries to the console</span></span>

### <a name="fetching-and-storing-data"></a><span data-ttu-id="7c957-136">Pobieranie i przechowywanie danych</span><span class="sxs-lookup"><span data-stu-id="7c957-136">Fetching and storing Data</span></span>

<span data-ttu-id="7c957-137">Aby pobrać dane z EF Core, można uzyskać dostęp do odpowiedniej właściwości i użyć LINQ do filtrowania wyniku.</span><span class="sxs-lookup"><span data-stu-id="7c957-137">To retrieve data from EF Core, you access the appropriate property and use LINQ to filter the result.</span></span> <span data-ttu-id="7c957-138">Można również użyć LINQ do wykonania projekcji, przekształcania wyniku z jednego typu na drugi.</span><span class="sxs-lookup"><span data-stu-id="7c957-138">You can also use LINQ to perform projection, transforming the result from one type to another.</span></span> <span data-ttu-id="7c957-139">Poniższy przykład pobiera CatalogBrands uporządkowane według nazwy, filtrowane według ich właściwości Enabled i rzutowane na typ SelectListItem:</span><span class="sxs-lookup"><span data-stu-id="7c957-139">The following example would retrieve CatalogBrands, ordered by name, filtered by their Enabled property, and projected onto a SelectListItem type:</span></span>

```csharp
var brandItems = await _context.CatalogBrands
    .Where(b => b.Enabled)
    .OrderBy(b => b.Name)
    .Select(b => new SelectListItem {
        Value = b.Id, Text = b.Name })
    .ToListAsync();
```

<span data-ttu-id="7c957-140">Ważne jest, aby w powyższym przykładzie dodać wywołanie do ToListAsync w celu natychmiastowego wykonania zapytania.</span><span class="sxs-lookup"><span data-stu-id="7c957-140">It's important in the above example to add the call to ToListAsync in order to execute the query immediately.</span></span> <span data-ttu-id="7c957-141">W przeciwnym razie instrukcja przypisze interfejs IQueryable\<SelectListItem > do brandItems, co nie zostanie wykonane, dopóki nie zostanie wyliczone.</span><span class="sxs-lookup"><span data-stu-id="7c957-141">Otherwise, the statement will assign an IQueryable\<SelectListItem> to brandItems, which will not be executed until it is enumerated.</span></span> <span data-ttu-id="7c957-142">Istnieją specjaliści i wady zwracające wyniki z metod.</span><span class="sxs-lookup"><span data-stu-id="7c957-142">There are pros and cons to returning IQueryable results from methods.</span></span> <span data-ttu-id="7c957-143">Pozwala to na dalsze modyfikacje EF Core kwerendy, ale może również powodować błędy, które występują tylko w czasie wykonywania, jeśli operacje są dodawane do zapytania, którego EF Core nie można przetłumaczyć.</span><span class="sxs-lookup"><span data-stu-id="7c957-143">It allows the query EF Core will construct to be further modified, but can also result in errors that only occur at runtime, if operations are added to the query that EF Core cannot translate.</span></span> <span data-ttu-id="7c957-144">Zwykle bezpieczniejsze jest przekazywanie dowolnych filtrów do metody wykonującej dostęp do danych i zwracanie z powrotem kolekcji w pamięci (na przykład listy\<T >) jako wyniku.</span><span class="sxs-lookup"><span data-stu-id="7c957-144">It's generally safer to pass any filters into the method performing the data access, and return back an in-memory collection (for example, List\<T>) as the result.</span></span>

<span data-ttu-id="7c957-145">EF Core śledzi zmiany w jednostkach pobieranych z trwałości.</span><span class="sxs-lookup"><span data-stu-id="7c957-145">EF Core tracks changes on entities it fetches from persistence.</span></span> <span data-ttu-id="7c957-146">Aby zapisać zmiany w monitorowanej jednostce, wystarczy wywołać metodę metody SaveChanges w kontekście DbContext, upewniając się, że jest to to samo wystąpienie DbContext, które zostało użyte do pobrania jednostki.</span><span class="sxs-lookup"><span data-stu-id="7c957-146">To save changes to a tracked entity, you just call the SaveChanges method on the DbContext, making sure it's the same DbContext instance that was used to fetch the entity.</span></span> <span data-ttu-id="7c957-147">Dodawanie i usuwanie jednostek jest bezpośrednio wykonywane na odpowiedniej właściwości Nieogólnymi, z wywołaniem metody SaveChanges w celu wykonania poleceń bazy danych.</span><span class="sxs-lookup"><span data-stu-id="7c957-147">Adding and removing entities is directly done on the appropriate DbSet property, again with a call to SaveChanges to execute the database commands.</span></span> <span data-ttu-id="7c957-148">Poniższy przykład ilustruje Dodawanie, aktualizowanie i usuwanie jednostek z trwałości.</span><span class="sxs-lookup"><span data-stu-id="7c957-148">The following example demonstrates adding, updating, and removing entities from persistence.</span></span>

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

<span data-ttu-id="7c957-149">EF Core obsługuje metody synchroniczne i asynchroniczne do pobierania i zapisywania.</span><span class="sxs-lookup"><span data-stu-id="7c957-149">EF Core supports both synchronous and async methods for fetching and saving.</span></span> <span data-ttu-id="7c957-150">W aplikacjach sieci Web zaleca się użycie wzorca Async/await z metodami asynchronicznymi, aby wątki serwera sieci Web nie były blokowane podczas oczekiwania na ukończenie operacji dostępu do danych.</span><span class="sxs-lookup"><span data-stu-id="7c957-150">In web applications, it's recommended to use the async/await pattern with the async methods, so that web server threads are not blocked while waiting for data access operations to complete.</span></span>

### <a name="fetching-related-data"></a><span data-ttu-id="7c957-151">Pobieranie powiązanych danych</span><span class="sxs-lookup"><span data-stu-id="7c957-151">Fetching related data</span></span>

<span data-ttu-id="7c957-152">Gdy EF Core Pobiera jednostki, wypełnia wszystkie właściwości, które są przechowywane bezpośrednio w tej jednostce w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="7c957-152">When EF Core retrieves entities, it populates all of the properties that are stored directly with that entity in the database.</span></span> <span data-ttu-id="7c957-153">Właściwości nawigacji, takie jak listy powiązanych jednostek, nie są wypełniane i mogą mieć ustawioną wartość null.</span><span class="sxs-lookup"><span data-stu-id="7c957-153">Navigation properties, such as lists of related entities, are not populated and may have their value set to null.</span></span> <span data-ttu-id="7c957-154">Dzięki temu EF Core nie pobiera większej ilości danych niż jest to potrzebne, co jest szczególnie ważne w przypadku aplikacji sieci Web, które muszą szybko przetwarzać żądania i zwracać odpowiedzi w wydajny sposób.</span><span class="sxs-lookup"><span data-stu-id="7c957-154">This ensures EF Core is not fetching more data than is needed, which is especially important for web applications, which must quickly process requests and return responses in an efficient manner.</span></span> <span data-ttu-id="7c957-155">Aby uwzględnić relacje z jednostką przy użyciu _ładowania eager_, należy określić właściwość przy użyciu metody include Extension w zapytaniu, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="7c957-155">To include relationships with an entity using _eager loading_, you specify the property using the Include extension method on the query, as shown:</span></span>

```csharp
// .Include requires using Microsoft.EntityFrameworkCore
var brandsWithItems = await _context.CatalogBrands
    .Include(b => b.Items)
    .ToListAsync();
```

<span data-ttu-id="7c957-156">Można uwzględnić wiele relacji i można również uwzględnić relacje podrzędne przy użyciu ThenInclude.</span><span class="sxs-lookup"><span data-stu-id="7c957-156">You can include multiple relationships, and you can also include sub-relationships using ThenInclude.</span></span> <span data-ttu-id="7c957-157">EF Core wykona pojedyncze zapytanie w celu pobrania zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="7c957-157">EF Core will execute a single query to retrieve the resulting set of entities.</span></span> <span data-ttu-id="7c957-158">Alternatywnie można uwzględnić właściwości nawigacji właściwości nawigacji poprzez przekazanie "." rozdzielany ciąg do metody `.Include()` rozszerzającej, na przykład:</span><span class="sxs-lookup"><span data-stu-id="7c957-158">Alternately you can include navigation properties of navigation properties by passing a '.'-separated string to the `.Include()` extension method, like so:</span></span>

```csharp
    .Include(“Items.Products”)
```

<span data-ttu-id="7c957-159">Oprócz hermetyzacji logiki filtrowania, Specyfikacja może określić kształt danych do zwrócenia, w tym właściwości do wypełnienia.</span><span class="sxs-lookup"><span data-stu-id="7c957-159">In addition to encapsulating filtering logic, a specification can specify the shape of the data to be returned, including which properties to populate.</span></span> <span data-ttu-id="7c957-160">Przykład eShopOnWeb zawiera kilka specyfikacji demonstrujących Hermetyzowanie eager informacji dotyczących ładowania w ramach specyfikacji.</span><span class="sxs-lookup"><span data-stu-id="7c957-160">The eShopOnWeb sample includes several specifications that demonstrate encapsulating eager loading information within the specification.</span></span> <span data-ttu-id="7c957-161">W tym miejscu można zobaczyć, jak specyfikacja jest używana jako część zapytania:</span><span class="sxs-lookup"><span data-stu-id="7c957-161">You can see how the specification is used as part of a query here:</span></span>

```csharp
// Includes all expression-based includes
query = specification.Includes.Aggregate(query,
            (current, include) => current.Include(include));

// Include any string-based include statements
query = specification.IncludeStrings.Aggregate(query,
            (current, include) => current.Include(include));
```

<span data-ttu-id="7c957-162">Kolejną opcją ładowania powiązanych danych jest użycie _jawnego ładowania_.</span><span class="sxs-lookup"><span data-stu-id="7c957-162">Another option for loading related data is to use _explicit loading_.</span></span> <span data-ttu-id="7c957-163">Jawne ładowanie umożliwia załadowanie dodatkowych danych do jednostki, która została już pobrana.</span><span class="sxs-lookup"><span data-stu-id="7c957-163">Explicit loading allows you to load additional data into an entity that has already been retrieved.</span></span> <span data-ttu-id="7c957-164">Ponieważ obejmuje to oddzielne żądanie do bazy danych, nie jest to zalecane w przypadku aplikacji sieci Web, co powinno zminimalizować liczbę rejsów w bazie danych na żądanie.</span><span class="sxs-lookup"><span data-stu-id="7c957-164">Since this involves a separate request to the database, it's not recommended for web applications, which should minimize the number of database round trips made per request.</span></span>

<span data-ttu-id="7c957-165">_Ładowanie z opóźnieniem_ to funkcja, która automatycznie ładuje powiązane dane, ponieważ odwołuje się do niej aplikacja.</span><span class="sxs-lookup"><span data-stu-id="7c957-165">_Lazy loading_ is a feature that automatically loads related data as it is referenced by the application.</span></span> <span data-ttu-id="7c957-166">EF Core dodano obsługę ładowania z opóźnieniem w wersji 2,1.</span><span class="sxs-lookup"><span data-stu-id="7c957-166">EF Core has added support for lazy loading in version 2.1.</span></span> <span data-ttu-id="7c957-167">Ładowanie z `Microsoft.EntityFrameworkCore.Proxies`opóźnieniem nie jest domyślnie włączone i wymaga zainstalowania.</span><span class="sxs-lookup"><span data-stu-id="7c957-167">Lazy loading is not enabled by default and requires installing the `Microsoft.EntityFrameworkCore.Proxies`.</span></span> <span data-ttu-id="7c957-168">Podobnie jak w przypadku jawnego ładowania, ładowanie z opóźnieniem powinno być zwykle wyłączone dla aplikacji sieci Web, ponieważ jego użycie spowoduje, że w każdym żądaniu sieci Web zostaną wykonane dodatkowe zapytania bazy danych.</span><span class="sxs-lookup"><span data-stu-id="7c957-168">As with explicit loading, lazy loading should typically be disabled for web applications, since its use will result in additional database queries being made within each web request.</span></span> <span data-ttu-id="7c957-169">Niestety, obciążenie związane z ładowaniem opóźnionym często jest niezauważalne w czasie projektowania, gdy opóźnienie jest małe i często zestawy danych używane do testowania są małe.</span><span class="sxs-lookup"><span data-stu-id="7c957-169">Unfortunately, the overhead incurred by lazy loading often goes unnoticed at development time, when latency is small and often the data sets used for testing are small.</span></span> <span data-ttu-id="7c957-170">Jednak w środowisku produkcyjnym, z większą liczbą użytkowników, większą ilością danych i większym opóźnieniu, dodatkowe żądania bazy danych mogą być często przyczyną niskiej wydajności aplikacji sieci Web, które intensywnie wykorzystują ładowanie z opóźnieniem.</span><span class="sxs-lookup"><span data-stu-id="7c957-170">However, in production, with more users, more data, and more latency, the additional database requests can often result in poor performance for web applications that make heavy use of lazy loading.</span></span>

[<span data-ttu-id="7c957-171">Unikaj załadowania jednostek w aplikacjach sieci Web</span><span class="sxs-lookup"><span data-stu-id="7c957-171">Avoid Lazy Loading Entities in Web Applications</span></span>](https://ardalis.com/avoid-lazy-loading-entities-in-asp-net-applications)

### <a name="encapsulating-data"></a><span data-ttu-id="7c957-172">Hermetyzowanie danych</span><span class="sxs-lookup"><span data-stu-id="7c957-172">Encapsulating data</span></span>

<span data-ttu-id="7c957-173">EF Core obsługuje kilka funkcji, które umożliwiają modelowi prawidłowe hermetyzację stanu.</span><span class="sxs-lookup"><span data-stu-id="7c957-173">EF Core supports several features that allow your model to properly encapsulate its state.</span></span> <span data-ttu-id="7c957-174">Typowym problemem w modelach domen jest ujawnienie przez nich właściwości nawigacji kolekcji jako typy list dostępnych publicznie.</span><span class="sxs-lookup"><span data-stu-id="7c957-174">A common problem in domain models is that they expose collection navigation properties as publicly accessible list types.</span></span> <span data-ttu-id="7c957-175">Pozwala to dowolnym współpracownikowi na manipulowanie zawartością tych typów kolekcji, co może spowodować obejście ważnych reguł firmy związanych z kolekcją, prawdopodobnie pozostawiając obiekt w nieprawidłowym stanie.</span><span class="sxs-lookup"><span data-stu-id="7c957-175">This allows any collaborator to manipulate the contents of these collection types, which may bypass important business rules related to the collection, possibly leaving the object in an invalid state.</span></span> <span data-ttu-id="7c957-176">Rozwiązaniem tego problemu jest udostępnienie dostępu tylko do odczytu do powiązanych kolekcji i jawne udostępnienie metod definiujących sposoby manipulowania nimi przez klientów, jak w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="7c957-176">The solution to this is to expose read-only access to related collections, and explicitly provide methods defining ways in which clients can manipulate them, as in this example:</span></span>

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

<span data-ttu-id="7c957-177">Należy zauważyć, że ten typ jednostki nie uwidacznia `List` publicznej `ICollection` lub właściwości `IReadOnlyCollection` , ale zamiast tego ujawnia typ, który otacza podstawowy typ listy.</span><span class="sxs-lookup"><span data-stu-id="7c957-177">Note that this entity type doesn’t expose a public `List` or `ICollection` property, but instead exposes an `IReadOnlyCollection` type that wraps the underlying List type.</span></span> <span data-ttu-id="7c957-178">Korzystając z tego wzorca, można wskazać, aby Entity Framework Core, aby użyć pola zapasowego, takiego jak:</span><span class="sxs-lookup"><span data-stu-id="7c957-178">When using this pattern, you can indicate to Entity Framework Core to use the backing field like so:</span></span>

```csharp
private void ConfigureBasket(EntityTypeBuilder<Basket> builder)
{
    var navigation = builder.Metadata.FindNavigation(nameof(Basket.Items));

    navigation.SetPropertyAccessMode(PropertyAccessMode.Field);
}
```

<span data-ttu-id="7c957-179">Innym sposobem, w którym można poprawić model domeny, jest użycie obiektów wartości dla typów, które nie mają tożsamości i są rozróżniane przez ich właściwości.</span><span class="sxs-lookup"><span data-stu-id="7c957-179">Another way in which you can improve your domain model is through the use of value objects for types that lack identity and are only distinguished by their properties.</span></span> <span data-ttu-id="7c957-180">Użycie takich typów jako właściwości jednostek może pomóc w utrzymaniu logiki specyficznej dla obiektu wartości, do którego należy, i może uniknąć zduplikowanej logiki między wieloma jednostkami, które korzystają z tego samego pojęcia.</span><span class="sxs-lookup"><span data-stu-id="7c957-180">Using such types as properties of your entities can help keep logic specific to the value object where it belongs, and can avoid duplicate logic between multiple entities that use the same concept.</span></span> <span data-ttu-id="7c957-181">W Entity Framework Core można utrwalać obiekty wartości w tej samej tabeli co ich jednostka będąca właścicielem przez skonfigurowanie typu jako jednostki należącej, na przykład:</span><span class="sxs-lookup"><span data-stu-id="7c957-181">In Entity Framework Core, you can persist value objects in the same table as their owning entity by configuring the type as an owned entity, like so:</span></span>

```csharp
private void ConfigureOrder(EntityTypeBuilder<Order> builder)
{
    builder.OwnsOne(o => o.ShipToAddress);
}
```

<span data-ttu-id="7c957-182">W tym przykładzie `ShipToAddress` właściwość jest typu `Address`.</span><span class="sxs-lookup"><span data-stu-id="7c957-182">In this example, the `ShipToAddress` property is of type `Address`.</span></span> <span data-ttu-id="7c957-183">`Address`jest obiektem wartości z kilkoma właściwościami, `Street` takimi jak i `City`.</span><span class="sxs-lookup"><span data-stu-id="7c957-183">`Address` is a value object with several properties such as `Street` and `City`.</span></span> <span data-ttu-id="7c957-184">EF Core mapuje `Order` obiekt na tabelę z jedną kolumną na `Address` właściwość, dodając prefiks nazwy każdej kolumny przy użyciu nazwy właściwości.</span><span class="sxs-lookup"><span data-stu-id="7c957-184">EF Core maps the `Order` object to its table with one column per `Address` property, prefixing each column name with the name of the property.</span></span> <span data-ttu-id="7c957-185">W tym przykładzie `Order` tabela będzie zawierać kolumny, takie jak `ShipToAddress_Street` i `ShipToAddress_City`.</span><span class="sxs-lookup"><span data-stu-id="7c957-185">In this example, the `Order` table would include columns such as `ShipToAddress_Street` and `ShipToAddress_City`.</span></span>

[<span data-ttu-id="7c957-186">EF Core 2,2 wprowadza obsługę kolekcji jednostek będących własnością</span><span class="sxs-lookup"><span data-stu-id="7c957-186">EF Core 2.2 introduces support for collections of owned entities</span></span>](https://docs.microsoft.com/ef/core/what-is-new/ef-core-2.2#collections-of-owned-entities)

### <a name="resilient-connections"></a><span data-ttu-id="7c957-187">Odporne połączenia</span><span class="sxs-lookup"><span data-stu-id="7c957-187">Resilient connections</span></span>

<span data-ttu-id="7c957-188">Zasoby zewnętrzne, takie jak bazy danych SQL, mogą być czasami niedostępne.</span><span class="sxs-lookup"><span data-stu-id="7c957-188">External resources like SQL databases may occasionally be unavailable.</span></span> <span data-ttu-id="7c957-189">W przypadku tymczasowej niedostępności aplikacje mogą używać logiki ponawiania, aby uniknąć ponoszenia wyjątku.</span><span class="sxs-lookup"><span data-stu-id="7c957-189">In cases of temporary unavailability, applications can use retry logic to avoid raising an exception.</span></span> <span data-ttu-id="7c957-190">Ta technika jest często określana jako _odporność połączenia_.</span><span class="sxs-lookup"><span data-stu-id="7c957-190">This technique is commonly referred to as _connection resiliency_.</span></span> <span data-ttu-id="7c957-191">Możesz zaimplementować [własne ponowienie próby przy użyciu wykładniczej techniki wycofywania](https://docs.microsoft.com/azure/architecture/patterns/retry) , próbując ponowić próbę przy użyciu wykładniczego wzrostu czasu oczekiwania, dopóki nie zostanie osiągnięta maksymalna liczba ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="7c957-191">You can implement your [own retry with exponential backoff](https://docs.microsoft.com/azure/architecture/patterns/retry) technique by attempting to retry with an exponentially increasing wait time, until a maximum retry count has been reached.</span></span> <span data-ttu-id="7c957-192">Ta technika obejmuje fakt, że zasoby chmury mogą sporadycznie być niedostępne przez krótki okresy, co powoduje niepowodzenie niektórych żądań.</span><span class="sxs-lookup"><span data-stu-id="7c957-192">This technique embraces the fact that cloud resources might intermittently be unavailable for short periods of time, resulting in failure of some requests.</span></span>

<span data-ttu-id="7c957-193">W przypadku usługi Azure SQL DB Entity Framework Core już zapewnia odporność połączenia wewnętrznej bazy danych i logikę ponawiania.</span><span class="sxs-lookup"><span data-stu-id="7c957-193">For Azure SQL DB, Entity Framework Core already provides internal database connection resiliency and retry logic.</span></span> <span data-ttu-id="7c957-194">Należy jednak włączyć strategię wykonywania Entity Framework dla każdego połączenia DbContext, jeśli chcesz mieć odporne EF Core połączenia.</span><span class="sxs-lookup"><span data-stu-id="7c957-194">But you need to enable the Entity Framework execution strategy for each DbContext connection if you want to have resilient EF Core connections.</span></span>

<span data-ttu-id="7c957-195">Na przykład poniższy kod na poziomie połączenia EF Core włącza odporne połączenia SQL, które są ponawiane, jeśli połączenie nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="7c957-195">For instance, the following code at the EF Core connection level enables resilient SQL connections that are retried if the connection fails.</span></span>

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

#### <a name="execution-strategies-and-explicit-transactions-using-begintransaction-and-multiple-dbcontexts"></a><span data-ttu-id="7c957-196">Strategie wykonywania i jawne transakcje przy użyciu BeginTransaction i wielu dbcontexts</span><span class="sxs-lookup"><span data-stu-id="7c957-196">Execution strategies and explicit transactions using BeginTransaction and multiple DbContexts</span></span>

<span data-ttu-id="7c957-197">Po włączeniu ponownych prób w EF Core połączeniach każda operacja wykonywana przy użyciu EF Core będzie własną operacją wywołały.</span><span class="sxs-lookup"><span data-stu-id="7c957-197">When retries are enabled in EF Core connections, each operation you perform using EF Core becomes its own retriable operation.</span></span> <span data-ttu-id="7c957-198">Każde zapytanie i każde wywołanie do metody SaveChanges zostanie ponowione w przypadku wystąpienia błędu przejściowego.</span><span class="sxs-lookup"><span data-stu-id="7c957-198">Each query and each call to SaveChanges will be retried as a unit if a transient failure occurs.</span></span>

<span data-ttu-id="7c957-199">Jeśli jednak kod inicjuje transakcję przy użyciu BeginTransaction, definiujesz własną grupę operacji, która musi być traktowana jako jednostka; Jeśli wystąpi awaria, wszystkie elementy wewnątrz transakcji należy wycofać.</span><span class="sxs-lookup"><span data-stu-id="7c957-199">However, if your code initiates a transaction using BeginTransaction, you are defining your own group of operations that need to be treated as a unit; everything inside the transaction has to be rolled back if a failure occurs.</span></span> <span data-ttu-id="7c957-200">Jeśli spróbujesz wykonać tę transakcję podczas korzystania z strategii wykonywania EF (zasady ponawiania), zostanie wyświetlony wyjątek, który będzie zawierał kilka metody SaveChanges z wielu dbcontexts.</span><span class="sxs-lookup"><span data-stu-id="7c957-200">You will see an exception like the following if you attempt to execute that transaction when using an EF execution strategy (retry policy) and you include several SaveChanges from multiple DbContexts in it.</span></span>

<span data-ttu-id="7c957-201">System.InvalidOperationException: Skonfigurowana strategia wykonywania "SqlServerRetryingExecutionStrategy" nie obsługuje transakcji inicjowanych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7c957-201">System.InvalidOperationException: The configured execution strategy 'SqlServerRetryingExecutionStrategy' does not support user initiated transactions.</span></span> <span data-ttu-id="7c957-202">Użyj strategii wykonywania zwróconej przez obiekt "DbContext. Database. CreateExecutionStrategy ()", aby wykonać wszystkie operacje w transakcji jako jednostkę wywołały.</span><span class="sxs-lookup"><span data-stu-id="7c957-202">Use the execution strategy returned by 'DbContext.Database.CreateExecutionStrategy()' to execute all the operations in the transaction as a retriable unit.</span></span>

<span data-ttu-id="7c957-203">Rozwiązaniem jest ręczne Wywołaj strategię wykonywania EF z delegatem reprezentującym wszystkie elementy, które należy wykonać.</span><span class="sxs-lookup"><span data-stu-id="7c957-203">The solution is to manually invoke the EF execution strategy with a delegate representing everything that needs to be executed.</span></span> <span data-ttu-id="7c957-204">Jeśli wystąpi błąd przejściowy, strategia wykonywania wywoła ponownie delegata.</span><span class="sxs-lookup"><span data-stu-id="7c957-204">If a transient failure occurs, the execution strategy will invoke the delegate again.</span></span> <span data-ttu-id="7c957-205">Poniższy kod przedstawia sposób wdrożenia tego podejścia:</span><span class="sxs-lookup"><span data-stu-id="7c957-205">The following code shows how to implement this approach:</span></span>

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

<span data-ttu-id="7c957-206">Pierwszy DbContext to \_catalogContext, a drugi DbContext znajduje się \_w obiekcie integrationEventLogService.</span><span class="sxs-lookup"><span data-stu-id="7c957-206">The first DbContext is the \_catalogContext and the second DbContext is within the \_integrationEventLogService object.</span></span> <span data-ttu-id="7c957-207">Na koniec akcja zatwierdzania będzie wykonywana z wieloma kontekstami DbContext i przy użyciu strategii wykonywania EF.</span><span class="sxs-lookup"><span data-stu-id="7c957-207">Finally, the Commit action would be performed multiple DbContexts and using an EF Execution Strategy.</span></span>

> ### <a name="references--entity-framework-core"></a><span data-ttu-id="7c957-208">Odwołania — Entity Framework Core</span><span class="sxs-lookup"><span data-stu-id="7c957-208">References – Entity Framework Core</span></span>
>
> - <span data-ttu-id="7c957-209">**Dokumentacja EF Core**</span><span class="sxs-lookup"><span data-stu-id="7c957-209">**EF Core Docs**</span></span>  
>   <https://docs.microsoft.com/ef/>
> - <span data-ttu-id="7c957-210">**EF Core: Powiązane dane**</span><span class="sxs-lookup"><span data-stu-id="7c957-210">**EF Core: Related Data**</span></span>  
>   <https://docs.microsoft.com/ef/core/querying/related-data>
> - <span data-ttu-id="7c957-211">**Unikaj powolnych jednostek ładowania w aplikacjach ASPNET**</span><span class="sxs-lookup"><span data-stu-id="7c957-211">**Avoid Lazy Loading Entities in ASPNET Applications**</span></span>  
>   <https://ardalis.com/avoid-lazy-loading-entities-in-asp-net-applications>

## <a name="ef-core-or-micro-orm"></a><span data-ttu-id="7c957-212">EF Core lub mikro-ORM?</span><span class="sxs-lookup"><span data-stu-id="7c957-212">EF Core or micro-ORM?</span></span>

<span data-ttu-id="7c957-213">Chociaż EF Core to doskonały wybór w zakresie zarządzania trwałością, a w większości przypadków dane są hermetyzowane przez deweloperów aplikacji, nie jest to jedyne rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="7c957-213">While EF Core is a great choice for managing persistence, and for the most part encapsulates database details from application developers, it is not the only choice.</span></span> <span data-ttu-id="7c957-214">Kolejną popularną alternatywą typu open source jest [Dapper](https://github.com/StackExchange/Dapper), a więc nazywamy mikro-ORM.</span><span class="sxs-lookup"><span data-stu-id="7c957-214">Another popular open source alternative is [Dapper](https://github.com/StackExchange/Dapper), a so-called micro-ORM.</span></span> <span data-ttu-id="7c957-215">Mikro-ORM to lekkie, mniej funkcjonalne narzędzie do mapowania obiektów do struktur danych.</span><span class="sxs-lookup"><span data-stu-id="7c957-215">A micro-ORM is a lightweight, less full-featured tool for mapping objects to data structures.</span></span> <span data-ttu-id="7c957-216">W przypadku Dapper, jego cele projektowe koncentrują się na wydajności, a nie w pełni hermetyzowaniu podstawowych zapytań używanych do pobierania i aktualizowania danych.</span><span class="sxs-lookup"><span data-stu-id="7c957-216">In the case of Dapper, its design goals focus on performance, rather than fully encapsulating the underlying queries it uses to retrieve and update data.</span></span> <span data-ttu-id="7c957-217">Ponieważ nie jest to abstrakcyjny kod SQL od dewelopera, Dapper jest "bliżej metalu" i umożliwia deweloperom pisanie dokładnych zapytań, których chcą używać dla danej operacji dostępu do danych.</span><span class="sxs-lookup"><span data-stu-id="7c957-217">Because it doesn't abstract SQL from the developer, Dapper is "closer to the metal" and lets developers write the exact queries they want to use for a given data access operation.</span></span>

<span data-ttu-id="7c957-218">EF Core ma dwie znaczące funkcje, które zapewnia oddzielenie go od Dapper, ale również zwiększenie wydajności.</span><span class="sxs-lookup"><span data-stu-id="7c957-218">EF Core has two significant features it provides which separate it from Dapper but also add to its performance overhead.</span></span> <span data-ttu-id="7c957-219">Pierwszy to tłumaczenie z wyrażeń LINQ do SQL.</span><span class="sxs-lookup"><span data-stu-id="7c957-219">The first is translation from LINQ expressions into SQL.</span></span> <span data-ttu-id="7c957-220">Te tłumaczenia są przechowywane w pamięci podręcznej, ale nawet wtedy, gdy są wykonywane po raz pierwszy.</span><span class="sxs-lookup"><span data-stu-id="7c957-220">These translations are cached, but even so there is overhead in performing them the first time.</span></span> <span data-ttu-id="7c957-221">Druga funkcja śledzenia zmian w jednostkach (tak, aby można było generować wydajne instrukcje Update).</span><span class="sxs-lookup"><span data-stu-id="7c957-221">The second is change tracking on entities (so that efficient update statements can be generated).</span></span> <span data-ttu-id="7c957-222">To zachowanie można wyłączyć dla konkretnych zapytań przy użyciu rozszerzenia AsNotTracking.</span><span class="sxs-lookup"><span data-stu-id="7c957-222">This behavior can be turned off for specific queries by using the AsNotTracking extension.</span></span> <span data-ttu-id="7c957-223">EF Core generuje również zapytania SQL, które zwykle są bardzo wydajne i w każdym przypadku idealnie akceptowalne z punktu widzenia wydajności, ale jeśli potrzebujesz precyzyjnej kontroli nad precyzyjnym zapytaniem, można przekazać niestandardowe SQL (lub wykonać procedurę składowaną) przy użyciu EF Rdzeń.</span><span class="sxs-lookup"><span data-stu-id="7c957-223">EF Core also generates SQL queries that usually are very efficient and in any case perfectly acceptable from a performance standpoint, but if you need fine control over the precise query to be executed, you can pass in custom SQL (or execute a stored procedure) using EF Core, too.</span></span> <span data-ttu-id="7c957-224">W takim przypadku Dapper nadal wykonuje EF Core, ale tylko nieco.</span><span class="sxs-lookup"><span data-stu-id="7c957-224">In this case, Dapper still outperforms EF Core, but only slightly.</span></span> <span data-ttu-id="7c957-225">Julie Lerman przedstawia pewne dane dotyczące wydajności, które mogą być 2016 artykułów MSDN [Dapper, Entity Framework i hybrydowych](https://msdn.microsoft.com/magazine/mt703432.aspx).</span><span class="sxs-lookup"><span data-stu-id="7c957-225">Julie Lerman presents some performance data in her May 2016 MSDN article [Dapper, Entity Framework, and Hybrid Apps](https://msdn.microsoft.com/magazine/mt703432.aspx).</span></span> <span data-ttu-id="7c957-226">Dodatkowe dane porównawcze wydajności dla różnych metod dostępu do danych można znaleźć w [witrynie Dapper](https://github.com/StackExchange/Dapper).</span><span class="sxs-lookup"><span data-stu-id="7c957-226">Additional performance benchmark data for a variety of data access methods can be found on [the Dapper site](https://github.com/StackExchange/Dapper).</span></span>

<span data-ttu-id="7c957-227">Aby zobaczyć, jak składnia Dapper różni się od EF Core, należy wziąć pod uwagę te dwie wersje tej samej metody do pobierania listy elementów:</span><span class="sxs-lookup"><span data-stu-id="7c957-227">To see how the syntax for Dapper varies from EF Core, consider these two versions of the same method for retrieving a list of items:</span></span>

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

<span data-ttu-id="7c957-228">Jeśli konieczne jest skompilowanie bardziej złożonych grafów obiektów za pomocą Dapper, należy napisać powiązane zapytania samodzielnie (w przeciwieństwie do dodania dołączenia w EF Core).</span><span class="sxs-lookup"><span data-stu-id="7c957-228">If you need to build more complex object graphs with Dapper, you need to write the associated queries yourself (as opposed to adding an Include as you would in EF Core).</span></span> <span data-ttu-id="7c957-229">Jest to obsługiwane za pomocą różnych składni, w tym funkcji o nazwie mapowanie wielokrotne, która umożliwia mapowanie poszczególnych wierszy na wiele mapowanych obiektów.</span><span class="sxs-lookup"><span data-stu-id="7c957-229">This is supported through a variety of syntaxes, including a feature called Multi Mapping that lets you map individual rows to multiple mapped objects.</span></span> <span data-ttu-id="7c957-230">Na przykład, jeśli dane wpisu klasy są właścicielami właściwości typu użytkownika, następujące SQL zwróci wszystkie niezbędne dane:</span><span class="sxs-lookup"><span data-stu-id="7c957-230">For example, given a class Post with a property Owner of type User, the following SQL would return all of the necessary data:</span></span>

```sql
select * from #Posts p
left join #Users u on u.Id = p.OwnerId
Order by p.Id
```

<span data-ttu-id="7c957-231">Każdy zwrócony wiersz zawiera dane użytkownika i danych post.</span><span class="sxs-lookup"><span data-stu-id="7c957-231">Each returned row includes both User and Post data.</span></span> <span data-ttu-id="7c957-232">Ponieważ dane użytkownika powinny być dołączone do danych post za pośrednictwem jego właściwości Owner, używana jest następująca funkcja:</span><span class="sxs-lookup"><span data-stu-id="7c957-232">Since the User data should be attached to the Post data via its Owner property, the following function is used:</span></span>

```csharp
(post, user) => { post.Owner = user; return post; }
```

<span data-ttu-id="7c957-233">Pełen kod, który ma zwracać kolekcję wpisów wraz z ich właściwością Owner, wypełnionymi danymi użytkownika:</span><span class="sxs-lookup"><span data-stu-id="7c957-233">The full code listing to return a collection of posts with their Owner property populated with the associated user data would be:</span></span>

```csharp
var sql = @"select * from #Posts p
left join #Users u on u.Id = p.OwnerId
Order by p.Id";
var data = connection.Query<Post, User, Post>(sql,
(post, user) => { post.Owner = user; return post;});
```

<span data-ttu-id="7c957-234">Ponieważ oferuje mniej hermetyzacji, Dapper wymaga, aby deweloperzy wiedzieli, jak ich dane są przechowywane, jak wykonywać zapytania efektywnie i pisać więcej kodu w celu pobrania go.</span><span class="sxs-lookup"><span data-stu-id="7c957-234">Because it offers less encapsulation, Dapper requires developers know more about how their data is stored, how to query it efficiently, and write more code to fetch it.</span></span> <span data-ttu-id="7c957-235">Gdy model ulegnie zmianie, zamiast po prostu utworzyć nową migrację (inną funkcję EF Core) i/lub zaktualizować informacje o mapowaniu w jednym miejscu w DbContext, należy zaktualizować wszystkie zapytania, na które ma wpływ.</span><span class="sxs-lookup"><span data-stu-id="7c957-235">When the model changes, instead of simply creating a new migration (another EF Core feature), and/or updating mapping information in one place in a DbContext, every query that is impacted must be updated.</span></span> <span data-ttu-id="7c957-236">Te zapytania nie mają gwarancji czasu kompilacji, więc mogą przerywać pracę w czasie wykonywania w odpowiedzi na zmiany modelu lub bazy danych, co sprawia, że błędy są trudniejsze do wykrycia szybko.</span><span class="sxs-lookup"><span data-stu-id="7c957-236">These queries have no compile time guarantees, so they may break at runtime in response to changes to the model or database, making errors more difficult to detect quickly.</span></span> <span data-ttu-id="7c957-237">W programie Exchange dla tych kompromisów Dapper oferuje bardzo szybką wydajność.</span><span class="sxs-lookup"><span data-stu-id="7c957-237">In exchange for these tradeoffs, Dapper offers extremely fast performance.</span></span>

<span data-ttu-id="7c957-238">W przypadku większości aplikacji i większości części prawie wszystkich aplikacji EF Core oferuje akceptowalną wydajność.</span><span class="sxs-lookup"><span data-stu-id="7c957-238">For most applications, and most parts of almost all applications, EF Core offers acceptable performance.</span></span> <span data-ttu-id="7c957-239">W ten sposób korzyści związane z produktywnością dla deweloperów mogą przeważyć wydajność.</span><span class="sxs-lookup"><span data-stu-id="7c957-239">Thus, its developer productivity benefits are likely to outweigh its performance overhead.</span></span> <span data-ttu-id="7c957-240">W przypadku zapytań, które mogą korzystać z buforowania, rzeczywiste zapytanie może być wykonywane tylko przez niewielki procent czasu, co powoduje stosunkowo małe różnice wydajności zapytań Moot.</span><span class="sxs-lookup"><span data-stu-id="7c957-240">For queries that can benefit from caching, the actual query may only be executed a tiny percentage of the time, making relatively small query performance differences moot.</span></span>

## <a name="sql-or-nosql"></a><span data-ttu-id="7c957-241">SQL lub NoSQL</span><span class="sxs-lookup"><span data-stu-id="7c957-241">SQL or NoSQL</span></span>

<span data-ttu-id="7c957-242">Tradycyjnie relacyjne bazy danych, takie jak SQL Server, korzystają z witryny Marketplace na potrzeby trwałego magazynowania danych, ale nie są jedynymi dostępnymi rozwiązaniami.</span><span class="sxs-lookup"><span data-stu-id="7c957-242">Traditionally, relational databases like SQL Server have dominated the marketplace for persistent data storage, but they are not the only solution available.</span></span> <span data-ttu-id="7c957-243">Bazy danych NoSQL, takie jak [MongoDB](https://www.mongodb.com/what-is-mongodb) , oferują inne podejście do przechowywania obiektów.</span><span class="sxs-lookup"><span data-stu-id="7c957-243">NoSQL databases like [MongoDB](https://www.mongodb.com/what-is-mongodb) offer a different approach to storing objects.</span></span> <span data-ttu-id="7c957-244">Zamiast mapowania obiektów do tabel i wierszy, kolejną opcją jest Serializacja całego wykresu obiektów i przechowywanie wyniku.</span><span class="sxs-lookup"><span data-stu-id="7c957-244">Rather than mapping objects to tables and rows, another option is to serialize the entire object graph, and store the result.</span></span> <span data-ttu-id="7c957-245">Zalety tego podejścia, co najmniej początkowo, są prostoty i wydajności.</span><span class="sxs-lookup"><span data-stu-id="7c957-245">The benefits of this approach, at least initially, are simplicity and performance.</span></span> <span data-ttu-id="7c957-246">Bardzo prostsze jest przechowywanie pojedynczego serializowanego obiektu z kluczem niż w celu rozdzielenia obiektu na wiele tabel z relacjami i aktualizacji oraz wierszy, które mogły ulec zmianie od czasu ostatniego pobrania obiektu z bazy danych.</span><span class="sxs-lookup"><span data-stu-id="7c957-246">It's certainly simpler to store a single serialized object with a key than to decompose the object into many tables with relationships and update and rows that may have changed since the object was last retrieved from the database.</span></span> <span data-ttu-id="7c957-247">Podobnie pobieranie i deserializacja pojedynczego obiektu z magazynu opartego na kluczach jest zwykle znacznie szybsze i łatwiejsze niż złożone sprzężenia lub wiele zapytań bazy danych wymaganych do pełnego zredagowania tego samego obiektu z relacyjnej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="7c957-247">Likewise, fetching and deserializing a single object from a key-based store is typically much faster and easier than complex joins or multiple database queries required to fully compose the same object from a relational database.</span></span> <span data-ttu-id="7c957-248">Brak blokad lub transakcji lub stały schemat sprawia również, że bazy danych NoSQL są bardzo łatwo do skalowania na wielu maszynach, obsługując bardzo duże zestawy danych.</span><span class="sxs-lookup"><span data-stu-id="7c957-248">The lack of locks or transactions or a fixed schema also makes NoSQL databases very amenable to scaling across many machines, supporting very large datasets.</span></span>

<span data-ttu-id="7c957-249">Z drugiej strony bazy danych NoSQL (jak są zwykle wywoływane) mają swoje wady.</span><span class="sxs-lookup"><span data-stu-id="7c957-249">On the other hand, NoSQL databases (as they are typically called) have their drawbacks.</span></span> <span data-ttu-id="7c957-250">Relacyjne bazy danych wykorzystują normalizację w celu wymuszenia spójności i uniknięcia duplikowania danych.</span><span class="sxs-lookup"><span data-stu-id="7c957-250">Relational databases use normalization to enforce consistency and avoid duplication of data.</span></span> <span data-ttu-id="7c957-251">Pozwala to zmniejszyć łączny rozmiar bazy danych i zapewnić, że aktualizacje udostępnionych danych będą dostępne natychmiast w całej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="7c957-251">This reduces the total size of the database and ensures that updates to shared data are available immediately throughout the database.</span></span> <span data-ttu-id="7c957-252">W relacyjnej bazie danych tabela adresów może odwoływać się do tabeli kraju według identyfikatora, w taki sposób, że jeśli nazwa kraju/regionu została zmieniona, rekordy adresów byłyby korzystne dla aktualizacji, które nie będą musiały zostać zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="7c957-252">In a relational database, an Address table might reference a Country table by ID, such that if the name of a country/region were changed, the address records would benefit from the update without themselves having to be updated.</span></span> <span data-ttu-id="7c957-253">Jednak w przypadku bazy danych NoSQL adres i jego stowarzyszony kraj mogą być serializowane w ramach wielu przechowywanych obiektów.</span><span class="sxs-lookup"><span data-stu-id="7c957-253">However, in a NoSQL database, Address and its associated Country might be serialized as part of many stored objects.</span></span> <span data-ttu-id="7c957-254">Aktualizacja nazwy kraju/regionu wymagała aktualizacji wszystkich takich obiektów, a nie jednego wiersza.</span><span class="sxs-lookup"><span data-stu-id="7c957-254">An update to a country/region name would require all such objects to be updated, rather than a single row.</span></span> <span data-ttu-id="7c957-255">Relacyjne bazy danych mogą również zapewnić relacyjną integralność, wymuszając reguły, takie jak klucze obce.</span><span class="sxs-lookup"><span data-stu-id="7c957-255">Relational databases can also ensure relational integrity by enforcing rules like foreign keys.</span></span> <span data-ttu-id="7c957-256">Bazy danych NoSQL zazwyczaj nie oferują takich ograniczeń dla swoich danych.</span><span class="sxs-lookup"><span data-stu-id="7c957-256">NoSQL databases typically do not offer such constraints on their data.</span></span>

<span data-ttu-id="7c957-257">Inne bazy danych NoSQL złożoności muszą zająć się przechowywaniem wersji.</span><span class="sxs-lookup"><span data-stu-id="7c957-257">Another complexity NoSQL databases must deal with is versioning.</span></span> <span data-ttu-id="7c957-258">Zmiany właściwości obiektu mogą nie być możliwe do deserializacji z wcześniejszych wersji, które były przechowywane.</span><span class="sxs-lookup"><span data-stu-id="7c957-258">When an object's properties change, it may not be able to be deserialized from past versions that were stored.</span></span> <span data-ttu-id="7c957-259">W ten sposób wszystkie istniejące obiekty, które mają serializowaną (poprzednią) wersję obiektu, muszą zostać zaktualizowane, aby były zgodne ze swoim nowym schematem.</span><span class="sxs-lookup"><span data-stu-id="7c957-259">Thus, all existing objects that have a serialized (previous) version of the object must be updated to conform to its new schema.</span></span> <span data-ttu-id="7c957-260">Nie różni się to od relacyjnej bazy danych, gdzie zmiany schematu czasami wymagają skryptów aktualizacji lub mapowania aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="7c957-260">This is not conceptually different from a relational database, where schema changes sometimes require update scripts or mapping updates.</span></span> <span data-ttu-id="7c957-261">Jednak liczba wpisów, które muszą zostać zmodyfikowane, jest często znacznie większa w podejściu NoSQL, ponieważ istnieje więcej duplikacji danych.</span><span class="sxs-lookup"><span data-stu-id="7c957-261">However, the number of entries that must be modified is often much greater in the NoSQL approach, because there is more duplication of data.</span></span>

<span data-ttu-id="7c957-262">Istnieje możliwość, że w bazach danych NoSQL są przechowywane wiele wersji obiektów, ale nie są zwykle obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="7c957-262">It's possible in NoSQL databases to store multiple versions of objects, something fixed schema relational databases typically do not support.</span></span> <span data-ttu-id="7c957-263">Jednak w tym przypadku kod aplikacji będzie musiał uwzględnić istnienie poprzednich wersji obiektów, co zwiększa złożoność.</span><span class="sxs-lookup"><span data-stu-id="7c957-263">However, in this case your application code will need to account for the existence of previous versions of objects, adding additional complexity.</span></span>

<span data-ttu-id="7c957-264">Bazy danych NoSQL zazwyczaj nie wymuszają stosowania [kwasów](https://en.wikipedia.org/wiki/ACID), co oznacza, że mają one zalety wydajności i skalowalności w porównaniu z relacyjnymi bazami danych.</span><span class="sxs-lookup"><span data-stu-id="7c957-264">NoSQL databases typically do not enforce [ACID](https://en.wikipedia.org/wiki/ACID), which means they have both performance and scalability benefits over relational databases.</span></span> <span data-ttu-id="7c957-265">Są one odpowiednie dla bardzo dużych zestawów danych i obiektów, które nie są dobrze dopasowane do magazynu w znormalizowanych strukturach tabel.</span><span class="sxs-lookup"><span data-stu-id="7c957-265">They're well-suited to extremely large datasets and objects that are not well-suited to storage in normalized table structures.</span></span> <span data-ttu-id="7c957-266">Nie ma powodów, dla których pojedyncze aplikacje nie mogą korzystać z baz danych relacyjnych i NoSQL, przy użyciu każdego z nich, gdzie jest najlepiej dopasowany.</span><span class="sxs-lookup"><span data-stu-id="7c957-266">There is no reason why a single application cannot take advantage of both relational and NoSQL databases, using each where it is best suited.</span></span>

## <a name="azure-documentdb"></a><span data-ttu-id="7c957-267">Azure DocumentDB</span><span class="sxs-lookup"><span data-stu-id="7c957-267">Azure DocumentDB</span></span>

<span data-ttu-id="7c957-268">Azure DocumentDB to w pełni zarządzana usługa bazy danych NoSQL, która oferuje oparty na chmurze magazyn danych bez schematu.</span><span class="sxs-lookup"><span data-stu-id="7c957-268">Azure DocumentDB is a fully managed NoSQL database service that offers cloud-based schema-free data storage.</span></span> <span data-ttu-id="7c957-269">DocumentDB jest zbudowany na potrzeby szybkiej i przewidywalnej wydajności, wysokiej dostępności, elastycznego skalowania i globalnej dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="7c957-269">DocumentDB is built for fast and predictable performance, high availability, elastic scaling, and global distribution.</span></span> <span data-ttu-id="7c957-270">Mimo że nie jest to baza danych NoSQL, deweloperzy mogą korzystać z zaawansowanych i znanych funkcji zapytań SQL dotyczących danych JSON.</span><span class="sxs-lookup"><span data-stu-id="7c957-270">Despite being a NoSQL database, developers can use rich and familiar SQL query capabilities on JSON data.</span></span> <span data-ttu-id="7c957-271">Wszystkie zasoby w DocumentDB są przechowywane jako dokumenty JSON.</span><span class="sxs-lookup"><span data-stu-id="7c957-271">All resources in DocumentDB are stored as JSON documents.</span></span> <span data-ttu-id="7c957-272">Zasoby są zarządzane jako _elementy_, które są dokumentami zawierającymi metadane, a także _źródła danych_, które są kolekcjami elementów.</span><span class="sxs-lookup"><span data-stu-id="7c957-272">Resources are managed as _items_, which are documents containing metadata, and _feeds_, which are collections of items.</span></span> <span data-ttu-id="7c957-273">Rysunek 8-2 przedstawia relację między różnymi zasobami DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="7c957-273">Figure 8-2 shows the relationship between different DocumentDB resources.</span></span>

![Hierarchiczna relacja między zasobami w DocumentDB, NoSQL w bazie danych JSON](./media/image8-2.png)

<span data-ttu-id="7c957-275">**Rysunek 8-2.**</span><span class="sxs-lookup"><span data-stu-id="7c957-275">**Figure 8-2.**</span></span> <span data-ttu-id="7c957-276">Organizacja zasobów DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="7c957-276">DocumentDB resource organization.</span></span>

<span data-ttu-id="7c957-277">Język zapytań DocumentDB to prosty, jeszcze zaawansowany interfejs do wykonywania zapytań w dokumentach JSON.</span><span class="sxs-lookup"><span data-stu-id="7c957-277">The DocumentDB query language is a simple yet powerful interface for querying JSON documents.</span></span> <span data-ttu-id="7c957-278">Język obsługuje podzbiór gramatyki SQL ANSI i dodaje głębokiej integracji obiektów JavaScript, tablic, konstrukcji obiektów i wywołania funkcji.</span><span class="sxs-lookup"><span data-stu-id="7c957-278">The language supports a subset of ANSI SQL grammar and adds deep integration of JavaScript object, arrays, object construction, and function invocation.</span></span>

<span data-ttu-id="7c957-279">**References — DocumentDB**</span><span class="sxs-lookup"><span data-stu-id="7c957-279">**References – DocumentDB**</span></span>

- <span data-ttu-id="7c957-280">Wprowadzenie do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="7c957-280">DocumentDB Introduction</span></span>  
  <https://docs.microsoft.com/azure/documentdb/documentdb-introduction>

## <a name="other-persistence-options"></a><span data-ttu-id="7c957-281">Inne opcje trwałości</span><span class="sxs-lookup"><span data-stu-id="7c957-281">Other persistence options</span></span>

<span data-ttu-id="7c957-282">Oprócz opcji magazynu relacyjnego i NoSQL aplikacje ASP.NET Core mogą używać usługi Azure Storage do przechowywania różnorodnych formatów danych i plików w sposób skalowalny w chmurze.</span><span class="sxs-lookup"><span data-stu-id="7c957-282">In addition to relational and NoSQL storage options, ASP.NET Core applications can use Azure Storage to store a variety of data formats and files in a cloud-based, scalable fashion.</span></span> <span data-ttu-id="7c957-283">Usługa Azure Storage jest wysoce skalowalna, co pozwala na rozpoczęcie przechowywania małych ilości danych i skalowanie w górę w celu przechowywania setek lub terabajtów, jeśli aplikacja tego wymaga.</span><span class="sxs-lookup"><span data-stu-id="7c957-283">Azure Storage is massively scalable, so you can start out storing small amounts of data and scale up to storing hundreds or terabytes if your application requires it.</span></span> <span data-ttu-id="7c957-284">Usługa Azure Storage obsługuje cztery rodzaje danych:</span><span class="sxs-lookup"><span data-stu-id="7c957-284">Azure Storage supports four kinds of data:</span></span>

- <span data-ttu-id="7c957-285">Blob Storage dla magazynu tekstowego lub binarnego bez struktury, nazywanego również magazynem obiektów.</span><span class="sxs-lookup"><span data-stu-id="7c957-285">Blob Storage for unstructured text or binary storage, also referred to as object storage.</span></span>

- <span data-ttu-id="7c957-286">Table Storage dla zestawów danych ze strukturą, dostępne za pośrednictwem kluczy wierszy.</span><span class="sxs-lookup"><span data-stu-id="7c957-286">Table Storage for structured datasets, accessible via row keys.</span></span>

- <span data-ttu-id="7c957-287">Queue Storage dla niezawodnej obsługi komunikatów na podstawie kolejki.</span><span class="sxs-lookup"><span data-stu-id="7c957-287">Queue Storage for reliable queue-based messaging.</span></span>

- <span data-ttu-id="7c957-288">File Storage dostępu do udostępnionego pliku między maszynami wirtualnymi platformy Azure i aplikacjami lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="7c957-288">File Storage for shared file access between Azure virtual machines and on-premises applications.</span></span>

<span data-ttu-id="7c957-289">**Odwołania — Azure Storage**</span><span class="sxs-lookup"><span data-stu-id="7c957-289">**References – Azure Storage**</span></span>

- <span data-ttu-id="7c957-290">Wprowadzenie do usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="7c957-290">Azure Storage Introduction</span></span>  
  <https://docs.microsoft.com/azure/storage/storage-introduction>

## <a name="caching"></a><span data-ttu-id="7c957-291">Buforowanie</span><span class="sxs-lookup"><span data-stu-id="7c957-291">Caching</span></span>

<span data-ttu-id="7c957-292">W aplikacjach internetowych każde żądanie sieci Web powinno być wykonywane w najkrótszym możliwym czasie.</span><span class="sxs-lookup"><span data-stu-id="7c957-292">In web applications, each web request should be completed in the shortest time possible.</span></span> <span data-ttu-id="7c957-293">Jednym ze sposobów osiągnięcia tego celu jest ograniczenie liczby wywołań zewnętrznych, które serwer musi wykonać, aby zakończyć żądanie.</span><span class="sxs-lookup"><span data-stu-id="7c957-293">One way to achieve this is to limit the number of external calls the server must make to complete the request.</span></span> <span data-ttu-id="7c957-294">Buforowanie obejmuje przechowywanie kopii danych na serwerze (lub w innym magazynie danych, który jest bardziej czytelny niż źródło danych).</span><span class="sxs-lookup"><span data-stu-id="7c957-294">Caching involves storing a copy of data on the server (or another data store that is more easily queried than the source of the data).</span></span> <span data-ttu-id="7c957-295">Aplikacje sieci Web, a w szczególności niespa tradycyjne aplikacje sieci Web, muszą kompilować cały interfejs użytkownika przy użyciu każdego żądania.</span><span class="sxs-lookup"><span data-stu-id="7c957-295">Web applications, and especially non-SPA traditional web applications, need to build the entire user interface with every request.</span></span> <span data-ttu-id="7c957-296">Często wiąże się to z wielokrotnym wykonywaniem wielu zapytań bazy danych z jednego żądania użytkownika do następnego.</span><span class="sxs-lookup"><span data-stu-id="7c957-296">This frequently involves making many of the same database queries repeatedly from one user request to the next.</span></span> <span data-ttu-id="7c957-297">W większości przypadków te zmiany danych są rzadko zmieniane, więc istnieje nieco powód, aby ciągle zażądać ich z bazy danych.</span><span class="sxs-lookup"><span data-stu-id="7c957-297">In most cases, this data changes rarely, so there is little reason to constantly request it from the database.</span></span> <span data-ttu-id="7c957-298">ASP.NET Core obsługuje buforowanie odpowiedzi, do buforowania całych stron i buforowania danych, co zapewnia bardziej szczegółowe zachowanie buforowania.</span><span class="sxs-lookup"><span data-stu-id="7c957-298">ASP.NET Core supports response caching, for caching entire pages, and data caching, which supports more granular caching behavior.</span></span>

<span data-ttu-id="7c957-299">Podczas implementowania buforowania należy pamiętać o rozdzieleniu obaw.</span><span class="sxs-lookup"><span data-stu-id="7c957-299">When implementing caching, it's important to keep in mind separation of concerns.</span></span> <span data-ttu-id="7c957-300">Unikaj implementowania logiki buforowania w logice dostępu do danych lub w interfejsie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7c957-300">Avoid implementing caching logic in your data access logic, or in your user interface.</span></span> <span data-ttu-id="7c957-301">Zamiast tego hermetyzowaj buforowanie we własnych klasach i używaj konfiguracji do zarządzania zachowaniem.</span><span class="sxs-lookup"><span data-stu-id="7c957-301">Instead, encapsulate caching in its own classes, and use configuration to manage its behavior.</span></span> <span data-ttu-id="7c957-302">Jest to zgodne z zasadami dotyczącymi otwartych/zamkniętych i pojedynczych odpowiedzialności. ułatwia to zarządzanie sposobem korzystania z pamięci podręcznej w aplikacji podczas jej rozszerzania.</span><span class="sxs-lookup"><span data-stu-id="7c957-302">This follows the Open/Closed and Single Responsibility principles, and will make it easier for you to manage how you use caching in your application as it grows.</span></span>

### <a name="aspnet-core-response-caching"></a><span data-ttu-id="7c957-303">Buforowanie odpowiedzi ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="7c957-303">ASP.NET Core response caching</span></span>

<span data-ttu-id="7c957-304">ASP.NET Core obsługuje dwa poziomy buforowania odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="7c957-304">ASP.NET Core supports two levels of response caching.</span></span> <span data-ttu-id="7c957-305">Pierwszy poziom nie buforuje żadnych elementów na serwerze, ale dodaje nagłówki HTTP, które instruują klientów i serwery proxy w celu buforowania odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="7c957-305">The first level does not cache anything on the server, but adds HTTP headers that instruct clients and proxy servers to cache responses.</span></span> <span data-ttu-id="7c957-306">Jest to implementowane przez dodanie atrybutu ResponseCache do poszczególnych kontrolerów lub akcji:</span><span class="sxs-lookup"><span data-stu-id="7c957-306">This is implemented by adding the ResponseCache attribute to individual controllers or actions:</span></span>

```csharp
    [ResponseCache(Duration = 60)]
    public IActionResult Contact()
    { }

    ViewData["Message"] = "Your contact page.";
    return View();
}
```

<span data-ttu-id="7c957-307">W poprzednim przykładzie zostanie dodany następujący nagłówek do odpowiedzi, co powoduje, że klienci buforują wynik przez maksymalnie 60 sekund.</span><span class="sxs-lookup"><span data-stu-id="7c957-307">The previous example will result in the following header being added to the response, instructing clients to cache the result for up to 60 seconds.</span></span>

<span data-ttu-id="7c957-308">Cache-Control: Public, max-age = 60</span><span class="sxs-lookup"><span data-stu-id="7c957-308">Cache-Control: public,max-age=60</span></span>

<span data-ttu-id="7c957-309">Aby dodać pamięć podręczną po stronie serwera do aplikacji, należy odwołać się do pakietu NuGet Microsoft. AspNetCore. ResponseCaching, a następnie dodać oprogramowanie pośredniczące buforowania odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="7c957-309">In order to add server-side in-memory caching to the application, you must reference the Microsoft.AspNetCore.ResponseCaching NuGet package, and then add the Response Caching middleware.</span></span> <span data-ttu-id="7c957-310">To oprogramowanie pośredniczące jest konfigurowane zarówno w ConfigureServices, jak i w trakcie uruchamiania:</span><span class="sxs-lookup"><span data-stu-id="7c957-310">This middleware is configured in both ConfigureServices and Configure in Startup:</span></span>

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

<span data-ttu-id="7c957-311">Oprogramowanie pośredniczące buforowania odpowiedzi automatycznie buforuje odpowiedzi na podstawie zestawu warunków, które można dostosować.</span><span class="sxs-lookup"><span data-stu-id="7c957-311">The Response Caching Middleware will automatically cache responses based on a set of conditions, which you can customize.</span></span> <span data-ttu-id="7c957-312">Domyślnie tylko odpowiedzi 200 (OK) wymagane przez metody GET lub z pamięci podręcznej są buforowane.</span><span class="sxs-lookup"><span data-stu-id="7c957-312">By default, only 200 (OK) responses requested via GET or HEAD methods are cached.</span></span> <span data-ttu-id="7c957-313">Ponadto żądania muszą mieć odpowiedź w nagłówku Cache-Control: Public i nie mogą zawierać nagłówków autoryzacji lub Set-cookie.</span><span class="sxs-lookup"><span data-stu-id="7c957-313">In addition, requests must have a response with a Cache-Control: public header, and cannot include headers for Authorization or Set-Cookie.</span></span> <span data-ttu-id="7c957-314">Zapoznaj się z [pełną listą warunków buforowania używanych przez oprogramowanie pośredniczące buforowania odpowiedzi](/aspnet/core/performance/caching/middleware#conditions-for-caching).</span><span class="sxs-lookup"><span data-stu-id="7c957-314">See a [complete list of the caching conditions used by the response caching middleware](/aspnet/core/performance/caching/middleware#conditions-for-caching).</span></span>

### <a name="data-caching"></a><span data-ttu-id="7c957-315">Buforowanie danych</span><span class="sxs-lookup"><span data-stu-id="7c957-315">Data caching</span></span>

<span data-ttu-id="7c957-316">Zamiast (lub oprócz) buforowania pełnych odpowiedzi sieci Web, można buforować wyniki poszczególnych zapytań dotyczących danych.</span><span class="sxs-lookup"><span data-stu-id="7c957-316">Rather than (or in addition to) caching full web responses, you can cache the results of individual data queries.</span></span> <span data-ttu-id="7c957-317">W tym celu można użyć usługi do buforowania pamięci na serwerze sieci Web lub użyć [rozproszonej pamięci podręcznej](/aspnet/core/performance/caching/distributed).</span><span class="sxs-lookup"><span data-stu-id="7c957-317">For this, you can use in memory caching on the web server, or use [a distributed cache](/aspnet/core/performance/caching/distributed).</span></span> <span data-ttu-id="7c957-318">W tej sekcji pokazano, jak zaimplementować program w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="7c957-318">This section will demonstrate how to implement in memory caching.</span></span>

<span data-ttu-id="7c957-319">Dodano obsługę buforowania pamięci (lub rozproszonego) w ConfigureServices:</span><span class="sxs-lookup"><span data-stu-id="7c957-319">You add support for memory (or distributed) caching in ConfigureServices:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMemoryCache();
    services.AddMvc();
}
```

<span data-ttu-id="7c957-320">Pamiętaj, aby dodać również pakiet NuGet Microsoft. Extensions. buforowanie. Memory.</span><span class="sxs-lookup"><span data-stu-id="7c957-320">Be sure to add the Microsoft.Extensions.Caching.Memory NuGet package as well.</span></span>

<span data-ttu-id="7c957-321">Po dodaniu usługi żądanie IMemoryCache za pośrednictwem iniekcji zależności wszędzie tam, gdzie trzeba uzyskać dostęp do pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="7c957-321">Once you've added the service, you request IMemoryCache via dependency injection wherever you need to access the cache.</span></span> <span data-ttu-id="7c957-322">W tym przykładzie CachedCatalogService korzysta ze wzorca projektowego serwera proxy (lub dekoratora), dostarczając alternatywną implementację ICatalogService, która kontroluje dostęp do (lub dodaje zachowanie do) bazowej implementacji CatalogService.</span><span class="sxs-lookup"><span data-stu-id="7c957-322">In this example, the CachedCatalogService is using the Proxy (or Decorator) design pattern, by providing an alternative implementation of ICatalogService that controls access to (or adds behavior to) the underlying CatalogService implementation.</span></span>

```csharp
public class CachedCatalogService : ICatalogService
{
    private readonly IMemoryCache _cache;
    private readonly CatalogService _catalogService;
    private static readonly string _brandsKey = "brands";
    private static readonly string _typesKey = "types";
    private static readonly string _itemsKeyTemplate = "items-{0}-{1}-{2}-{3}";
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
        string cacheKey = String.Format(_itemsKeyTemplate, pageIndex, itemsPage, brandID, typeId);
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

<span data-ttu-id="7c957-323">Aby skonfigurować aplikację do korzystania z buforowanej wersji usługi, ale nadal zezwolić usłudze na uzyskanie wystąpienia CatalogService, którego potrzebuje w jego konstruktorze, Dodaj następujące elementy w ConfigureServices:</span><span class="sxs-lookup"><span data-stu-id="7c957-323">To configure the application to use the cached version of the service, but still allow the service to get the instance of CatalogService it needs in its constructor, you would add the following in ConfigureServices:</span></span>

```csharp
services.AddMemoryCache();
services.AddScoped<ICatalogService, CachedCatalogService>();
services.AddScoped<CatalogService>();
```

<span data-ttu-id="7c957-324">W tym miejscu baza danych wywołuje pobieranie danych wykazu tylko raz na minutę, a nie na każdym żądaniu.</span><span class="sxs-lookup"><span data-stu-id="7c957-324">With this in place, the database calls to fetch the catalog data will only be made once per minute, rather than on every request.</span></span> <span data-ttu-id="7c957-325">W zależności od ruchu do lokacji może to mieć bardzo znaczący wpływ na liczbę zapytań wykonywanych w bazie danych oraz średni czas ładowania strony dla strony głównej, który jest aktualnie zależny od wszystkich trzech zapytań narażonych na tę usługę.</span><span class="sxs-lookup"><span data-stu-id="7c957-325">Depending on the traffic to the site, this can have a very significant impact on the number of queries made to the database, and the average page load time for the home page that currently depends on all three of the queries exposed by this service.</span></span>

<span data-ttu-id="7c957-326">Problem, który powstaje, gdy buforowanie jest zaimplementowane, jest _przestarzałe dane_ — to oznacza, że dane, które uległy zmianie w źródle, ale w pamięci podręcznej pozostają nieaktualne.</span><span class="sxs-lookup"><span data-stu-id="7c957-326">An issue that arises when caching is implemented is _stale data_ – that is, data that has changed at the source but an out of date version remains in the cache.</span></span> <span data-ttu-id="7c957-327">Prostym sposobem na ograniczenie tego problemu jest użycie małych okresów pamięci podręcznej, ponieważ w przypadku zajętej aplikacji istnieje ograniczone dodatkowe korzyści umożliwiające rozszerzanie danych długości.</span><span class="sxs-lookup"><span data-stu-id="7c957-327">A simple way to mitigate this issue is to use small cache durations, since for a busy application there is limited additional benefit to extending the length data is cached.</span></span> <span data-ttu-id="7c957-328">Rozważmy na przykład stronę, która tworzy zapytanie pojedynczej bazy danych i żąda 10 razy na sekundę.</span><span class="sxs-lookup"><span data-stu-id="7c957-328">For example, consider a page that makes a single database query, and is requested 10 times per second.</span></span> <span data-ttu-id="7c957-329">Jeśli ta strona jest buforowana przez jedną minutę, spowoduje to liczbę zapytań bazy danych wykonanych na minutę do porzucenia z 600 do 1, zmniejszenie 99,8%.</span><span class="sxs-lookup"><span data-stu-id="7c957-329">If this page is cached for one minute, it will result in the number of database queries made per minute to drop from 600 to 1, a reduction of 99.8%.</span></span> <span data-ttu-id="7c957-330">Jeśli zamiast tego czas trwania pamięci podręcznej został wykonany jedną godzinę, ogólna obniżka wynosi 99,997%, ale teraz prawdopodobieństwo i potencjalny wiek starych danych są znacznie większe.</span><span class="sxs-lookup"><span data-stu-id="7c957-330">If instead the cache duration were made one hour, the overall reduction would be 99.997%, but now the likelihood and potential age of stale data are both increased dramatically.</span></span>

<span data-ttu-id="7c957-331">Innym podejściem jest proaktywnie Usuwanie wpisów pamięci podręcznej po zaktualizowaniu zawartych w nich danych.</span><span class="sxs-lookup"><span data-stu-id="7c957-331">Another approach is to proactively remove cache entries when the data they contain is updated.</span></span> <span data-ttu-id="7c957-332">Każdy wpis można usunąć, jeśli jego klucz jest znany:</span><span class="sxs-lookup"><span data-stu-id="7c957-332">Any individual entry can be removed if its key is known:</span></span>

```csharp
_cache.Remove(cacheKey);
```

<span data-ttu-id="7c957-333">Jeśli aplikacja ujawnia funkcje do aktualizowania wpisów, które są buforowane, można usunąć odpowiednie wpisy pamięci podręcznej w kodzie, który wykonuje aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="7c957-333">If your application exposes functionality for updating entries that it caches, you can remove the corresponding cache entries in your code that performs the updates.</span></span> <span data-ttu-id="7c957-334">Czasami może istnieć wiele różnych wpisów, które są zależne od określonego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="7c957-334">Sometimes there may be many different entries that depend on a particular set of data.</span></span> <span data-ttu-id="7c957-335">W takim przypadku może być przydatne do tworzenia zależności między wpisami pamięci podręcznej przy użyciu CancellationChangeToken.</span><span class="sxs-lookup"><span data-stu-id="7c957-335">In that case, it can be useful to create dependencies between cache entries, by using a CancellationChangeToken.</span></span> <span data-ttu-id="7c957-336">Za pomocą CancellationChangeToken można wycofać wiele wpisów pamięci podręcznej jednocześnie przez anulowanie tokenu.</span><span class="sxs-lookup"><span data-stu-id="7c957-336">With a CancellationChangeToken, you can expire multiple cache entries at once by cancelling the token.</span></span>

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

<span data-ttu-id="7c957-337">Buforowanie może znacząco poprawić wydajność stron sieci Web, które wielokrotnie żądają tych samych wartości z bazy danych.</span><span class="sxs-lookup"><span data-stu-id="7c957-337">Caching can dramatically improve the performance of web pages that repeatedly request the same values from the database.</span></span> <span data-ttu-id="7c957-338">Należy pamiętać, aby zmierzyć dostęp do danych i wydajność stron przed zastosowaniem buforowania, i zastosować buforowanie tylko w przypadku, gdy zobaczysz potrzebę ulepszenia.</span><span class="sxs-lookup"><span data-stu-id="7c957-338">Be sure to measure data access and page performance before applying caching, and only apply caching where you see a need for improvement.</span></span> <span data-ttu-id="7c957-339">Buforowanie zużywa zasoby pamięci serwera sieci Web i zwiększa złożoność aplikacji, dlatego ważne jest, aby nie zoptymalizować się za pomocą tej techniki.</span><span class="sxs-lookup"><span data-stu-id="7c957-339">Caching consumes web server memory resources and increases the complexity of the application, so it’s important you don’t prematurely optimize using this technique.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="7c957-340">[Poprzedni](develop-asp-net-core-mvc-apps.md)Następny
>[](test-asp-net-core-mvc-apps.md)</span><span class="sxs-lookup"><span data-stu-id="7c957-340">[Previous](develop-asp-net-core-mvc-apps.md)
[Next](test-asp-net-core-mvc-apps.md)</span></span>