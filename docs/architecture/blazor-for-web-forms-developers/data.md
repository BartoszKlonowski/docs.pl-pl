---
title: Dostęp do danych i zarządzanie nimi
description: Dowiedz się, jak uzyskiwać dostęp do danych i obsługiwać je w ASP.NET Web Forms i Blazor .
author: csharpfritz
ms.author: jefritz
no-loc:
- Blazor
ms.date: 11/20/2020
ms.openlocfilehash: 66e6001cbcac612cb556e90fb86fd694ca7d1459
ms.sourcegitcommit: 2f485e721f7f34b87856a51181b5b56624b31fd5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/02/2020
ms.locfileid: "96509757"
---
# <a name="work-with-data"></a><span data-ttu-id="90d0c-103">Praca z danymi</span><span class="sxs-lookup"><span data-stu-id="90d0c-103">Work with data</span></span>

<span data-ttu-id="90d0c-104">Dostęp do danych to szkielet aplikacji ASP.NET Web Forms.</span><span class="sxs-lookup"><span data-stu-id="90d0c-104">Data access is the backbone of an ASP.NET Web Forms app.</span></span> <span data-ttu-id="90d0c-105">W przypadku kompilowania formularzy dla sieci Web, co się dzieje z tymi danymi?</span><span class="sxs-lookup"><span data-stu-id="90d0c-105">If you're building forms for the web, what happens to that data?</span></span> <span data-ttu-id="90d0c-106">Korzystając z formularzy sieci Web, istniały wiele technik dostępu do danych, których można użyć do współpracy z bazą danych:</span><span class="sxs-lookup"><span data-stu-id="90d0c-106">With Web Forms, there were multiple data access techniques you could use to interact with a database:</span></span>

- <span data-ttu-id="90d0c-107">Źródła danych</span><span class="sxs-lookup"><span data-stu-id="90d0c-107">Data Sources</span></span>
- <span data-ttu-id="90d0c-108">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="90d0c-108">ADO.NET</span></span>
- <span data-ttu-id="90d0c-109">Entity Framework</span><span class="sxs-lookup"><span data-stu-id="90d0c-109">Entity Framework</span></span>

<span data-ttu-id="90d0c-110">Źródła danych były kontrolkami, które można umieścić na stronie formularzy sieci Web i skonfigurować tak jak inne kontrolki.</span><span class="sxs-lookup"><span data-stu-id="90d0c-110">Data Sources were controls that you could place on a Web Forms page and configure like other controls.</span></span> <span data-ttu-id="90d0c-111">Program Visual Studio udostępnia przyjazny zestaw okien dialogowych umożliwiających konfigurowanie i powiązywanie kontrolek ze stronami formularzy sieci Web.</span><span class="sxs-lookup"><span data-stu-id="90d0c-111">Visual Studio provided a friendly set of dialogs to configure and bind the controls to your Web Forms pages.</span></span> <span data-ttu-id="90d0c-112">Deweloperzy korzystający z metody "Low Code" lub "No Code" preferują tę technikę, gdy formularze sieci Web zostały po raz pierwszy wydane.</span><span class="sxs-lookup"><span data-stu-id="90d0c-112">Developers who enjoy a "low code" or "no code" approach preferred this technique when Web Forms was first released.</span></span>

![Źródła danych](media/data/datasources.png)

<span data-ttu-id="90d0c-114">ADO.NET jest podejściem niskiego poziomu służącym do współdziałania z bazą danych.</span><span class="sxs-lookup"><span data-stu-id="90d0c-114">ADO.NET is the low-level approach to interacting with a database.</span></span> <span data-ttu-id="90d0c-115">Aplikacje mogą utworzyć połączenie z bazą danych z poleceniami, zestawami rekordów i zestawami DataSets w celu manipulowania nimi.</span><span class="sxs-lookup"><span data-stu-id="90d0c-115">Your apps could create a connection to the database with Commands, Recordsets, and Datasets for interacting.</span></span> <span data-ttu-id="90d0c-116">Wyniki można następnie powiązać z polami na ekranie bez wielu kodów.</span><span class="sxs-lookup"><span data-stu-id="90d0c-116">The results could then be bound to fields on screen without much code.</span></span> <span data-ttu-id="90d0c-117">Wadą tego podejścia było to, że każdy zestaw obiektów ADO.NET ( `Connection` , `Command` i `Recordset` ) został powiązany z bibliotekami dostarczonymi przez dostawcę bazy danych.</span><span class="sxs-lookup"><span data-stu-id="90d0c-117">The drawback of this approach was that each set of ADO.NET objects (`Connection`, `Command`, and `Recordset`) was bound to libraries provided by a database vendor.</span></span> <span data-ttu-id="90d0c-118">Użycie tych składników sprawia, że kod jest sztywny i trudny do migracji do innej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="90d0c-118">Use of these components made the code rigid and difficult to migrate to a different database.</span></span>

## <a name="entity-framework"></a><span data-ttu-id="90d0c-119">Entity Framework</span><span class="sxs-lookup"><span data-stu-id="90d0c-119">Entity Framework</span></span>

<span data-ttu-id="90d0c-120">Entity Framework (EF) to struktura mapowania relacyjnego obiektu źródłowego obsługiwana przez platformę .NET Foundation.</span><span class="sxs-lookup"><span data-stu-id="90d0c-120">Entity Framework (EF) is the open source object-relational mapping framework maintained by the .NET Foundation.</span></span> <span data-ttu-id="90d0c-121">Początkowo wydane z .NET Framework, EF umożliwia generowanie kodu dla połączeń baz danych, schematów magazynu i interakcji.</span><span class="sxs-lookup"><span data-stu-id="90d0c-121">Initially released with .NET Framework, EF allows for generating code for the database connections, storage schemas, and interactions.</span></span> <span data-ttu-id="90d0c-122">Dzięki temu abstrakcji możesz skupić się na regułach firmy aplikacji i umożliwić zarządzanie bazą danych przez zaufanego administratora bazy danych.</span><span class="sxs-lookup"><span data-stu-id="90d0c-122">With this abstraction, you can focus on your app's business rules and allow the database to be managed by a trusted database administrator.</span></span> <span data-ttu-id="90d0c-123">W programie .NET można użyć zaktualizowanej wersji EF o nazwie EF Core.</span><span class="sxs-lookup"><span data-stu-id="90d0c-123">In .NET, you can use an updated version of EF called EF Core.</span></span> <span data-ttu-id="90d0c-124">EF Core pomaga generować i obsługiwać interakcje między kodem i bazą danych z serią poleceń, które są dostępne za pomocą `dotnet ef` narzędzia wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="90d0c-124">EF Core helps generate and maintain the interactions between your code and the database with a series of commands that are available for you using the `dotnet ef` command-line tool.</span></span> <span data-ttu-id="90d0c-125">Przyjrzyjmy się kilku przykładom, aby rozpocząć pracę z bazą danych.</span><span class="sxs-lookup"><span data-stu-id="90d0c-125">Let's take a look at a few samples to get you working with a database.</span></span>

### <a name="ef-code-first"></a><span data-ttu-id="90d0c-126">Dr Code First</span><span class="sxs-lookup"><span data-stu-id="90d0c-126">EF Code First</span></span>

<span data-ttu-id="90d0c-127">Szybkim sposobem na rozpoczęcie tworzenia interakcji z bazą danych jest rozpoczęcie od obiektów klasy, z którymi chcesz współpracować.</span><span class="sxs-lookup"><span data-stu-id="90d0c-127">A quick way to get started building your database interactions is to start with the class objects you want to work with.</span></span> <span data-ttu-id="90d0c-128">EF udostępnia narzędzie, które pomaga wygenerować odpowiedni kod bazy danych dla klas.</span><span class="sxs-lookup"><span data-stu-id="90d0c-128">EF provides a tool to help generate the appropriate database code for your classes.</span></span> <span data-ttu-id="90d0c-129">Takie podejście nazywa się "Code First" programowaniem.</span><span class="sxs-lookup"><span data-stu-id="90d0c-129">This approach is called "Code First" development.</span></span> <span data-ttu-id="90d0c-130">Rozważmy następujące `Product` klasy dla przykładowej aplikacji w sklepie, która ma być przechowywana w relacyjnej bazie danych, takiej jak Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="90d0c-130">Consider the following `Product` class for a sample storefront app that we want to store in a relational database like Microsoft SQL Server.</span></span>

```csharp
public class Product
{
    public int Id { get; set; }

    [Required]
    public string Name { get; set; }

    [MaxLength(4000)]
    public string Description { get; set; }

    [Range(0, 99999,99)]
    [DataType(DataType.Currency)]
    public decimal Price { get; set; }
}
```

<span data-ttu-id="90d0c-131">Produkt ma klucz podstawowy i trzy dodatkowe pola, które zostałyby utworzone w bazie danych:</span><span class="sxs-lookup"><span data-stu-id="90d0c-131">Product has a primary key and three additional fields that would be created in our database:</span></span>  

- <span data-ttu-id="90d0c-132">EF zidentyfikuje `Id` Właściwość jako klucz podstawowy według Konwencji.</span><span class="sxs-lookup"><span data-stu-id="90d0c-132">EF will identify the `Id` property as a primary key by convention.</span></span>
- <span data-ttu-id="90d0c-133">`Name` będą przechowywane w kolumnie skonfigurowanej do przechowywania tekstu.</span><span class="sxs-lookup"><span data-stu-id="90d0c-133">`Name` will be stored in a column configured for text storage.</span></span> <span data-ttu-id="90d0c-134">`[Required]`Atrybut dekorowania nazwy tej właściwości spowoduje dodanie ograniczenia, `not null` które pomoże wymusić to zadeklarowane zachowanie właściwości.</span><span class="sxs-lookup"><span data-stu-id="90d0c-134">The `[Required]` attribute decorating this property will add a `not null` constraint to help enforce this declared behavior of the property.</span></span>
- <span data-ttu-id="90d0c-135">`Description` będą przechowywane w kolumnie skonfigurowanej do przechowywania tekstu i mają maksymalną długość skonfigurowaną 4000 znaków zgodnie z `[MaxLength]` atrybutem.</span><span class="sxs-lookup"><span data-stu-id="90d0c-135">`Description` will be stored in a column configured for text storage, and have a maximum length configured of 4000 characters as dictated by the `[MaxLength]` attribute.</span></span> <span data-ttu-id="90d0c-136">Schemat bazy danych zostanie skonfigurowany z kolumną o nazwie `MaxLength` przy użyciu typu danych `varchar(4000)` .</span><span class="sxs-lookup"><span data-stu-id="90d0c-136">The database schema will be configured with a column named `MaxLength` using data type `varchar(4000)`.</span></span>
- <span data-ttu-id="90d0c-137">`Price`Właściwość będzie przechowywana jako waluta.</span><span class="sxs-lookup"><span data-stu-id="90d0c-137">The `Price` property will be stored as currency.</span></span> <span data-ttu-id="90d0c-138">Ten `[Range]` atrybut generuje odpowiednie ograniczenia, aby zapobiec przechowywaniu danych poza minimalnym i maksymalnym zadeklarowanymi wartościami.</span><span class="sxs-lookup"><span data-stu-id="90d0c-138">The `[Range]` attribute will generate appropriate constraints to prevent data storage outside of the minimum and maximum values declared.</span></span>

<span data-ttu-id="90d0c-139">Musimy dodać tę `Product` klasę do klasy kontekstu bazy danych, która definiuje operacje połączenia i translacji z naszą bazą danych.</span><span class="sxs-lookup"><span data-stu-id="90d0c-139">We need to add this `Product` class to a database context class that defines the connection and translation operations with our database.</span></span>

```csharp
public class MyDbContext : DbContext
{
    public DbSet<Product> Products { get; set; }
}
```

<span data-ttu-id="90d0c-140">`MyDbContext`Klasa zawiera jedną właściwość, która definiuje dostęp i tłumaczenie dla `Product` klasy.</span><span class="sxs-lookup"><span data-stu-id="90d0c-140">The `MyDbContext` class provides the one property that defines the access and translation for the `Product` class.</span></span>  <span data-ttu-id="90d0c-141">Twoja aplikacja konfiguruje tę klasę do interakcji z bazą danych przy użyciu następujących wpisów w `Startup` `ConfigureServices` metodzie klasy:</span><span class="sxs-lookup"><span data-stu-id="90d0c-141">Your application configures this class for interaction with the database using the following entries in the `Startup` class's `ConfigureServices` method:</span></span>

```csharp
services.AddDbContext<MyDbContext>(options =>
    options.UseSqlServer("MY DATABASE CONNECTION STRING"));
```

<span data-ttu-id="90d0c-142">Poprzedni kod będzie łączyć się z bazą danych SQL Server przy użyciu określonych parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="90d0c-142">The preceding code will connect to a SQL Server database with the specified connection string.</span></span> <span data-ttu-id="90d0c-143">Parametry połączenia można umieścić w *appsettings.jsw* pliku, zmiennych środowiskowych lub w innych lokalizacjach magazynu konfiguracji i odpowiednio zastąpić ten osadzony ciąg.</span><span class="sxs-lookup"><span data-stu-id="90d0c-143">You can place the connection string in your *appsettings.json* file, environment variables, or other configuration storage locations and replace this embedded string appropriately.</span></span>

<span data-ttu-id="90d0c-144">Następnie można wygenerować tabelę bazy danych odpowiednią dla tej klasy przy użyciu następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="90d0c-144">You can then generate the database table appropriate for this class using the following commands:</span></span>

```dotnetcli
dotnet ef migrations add 'Create Product table'
dotnet ef database update
```

<span data-ttu-id="90d0c-145">Pierwsze polecenie definiuje zmiany wprowadzane w schemacie bazy danych jako nową migrację EF o nazwie `Create Product table` .</span><span class="sxs-lookup"><span data-stu-id="90d0c-145">The first command defines the changes you're making to the database schema as a new EF Migration called `Create Product table`.</span></span>  <span data-ttu-id="90d0c-146">Migracja definiuje sposób stosowania i usuwania nowych zmian w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="90d0c-146">A Migration defines how to apply and remove your new database changes.</span></span>

<span data-ttu-id="90d0c-147">Po zastosowaniu należy mieć prostą `Product` tabelę w bazie danych oraz kilka nowych klas dodanych do projektu, które ułatwiają zarządzanie schematem bazy danych.</span><span class="sxs-lookup"><span data-stu-id="90d0c-147">Once applied, you have a simple `Product` table in your database and some new classes added to the project that help manage the database schema.</span></span>  <span data-ttu-id="90d0c-148">Te wygenerowane klasy można domyślnie znaleźć w nowym folderze o nazwie *migrations*.</span><span class="sxs-lookup"><span data-stu-id="90d0c-148">You can find these generated classes, by default, in a new folder called *Migrations*.</span></span>  <span data-ttu-id="90d0c-149">Po wprowadzeniu zmian w `Product` klasie lub dodaniu bardziej powiązanych klas, które mają być używane z bazą danych, należy ponownie uruchomić polecenia wiersza polecenia przy użyciu nowej nazwy migracji.</span><span class="sxs-lookup"><span data-stu-id="90d0c-149">When you make changes to the `Product` class or add more related classes you would like interacting with your database, you need to run the command-line commands again with a new name of the migration.</span></span>  <span data-ttu-id="90d0c-150">To polecenie spowoduje wygenerowanie innego zestawu klas migracji w celu zaktualizowania schematu bazy danych.</span><span class="sxs-lookup"><span data-stu-id="90d0c-150">This command will generate another set of migration classes to update your database schema.</span></span>

### <a name="ef-database-first"></a><span data-ttu-id="90d0c-151">Dr Database First</span><span class="sxs-lookup"><span data-stu-id="90d0c-151">EF Database First</span></span>

<span data-ttu-id="90d0c-152">W przypadku istniejących baz danych można generować klasy dla EF Core przy użyciu narzędzi wiersza polecenia platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="90d0c-152">For existing databases, you can generate the classes for EF Core by using the .NET command-line tools.</span></span> <span data-ttu-id="90d0c-153">Aby szkieletować klasy, należy użyć odmiany następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="90d0c-153">To scaffold the classes, use a variation of the following command:</span></span>

```dotnetcli
dotnet ef dbcontext scaffold "CONNECTION STRING" Microsoft.EntityFrameworkCore.SqlServer -c MyDbContext -t Product -t Customer
```

<span data-ttu-id="90d0c-154">Poprzednie polecenie nawiązuje połączenie z bazą danych przy użyciu określonych parametrów połączenia i `Microsoft.EntityFrameworkCore.SqlServer` dostawcy.</span><span class="sxs-lookup"><span data-stu-id="90d0c-154">The preceding command connects to the database using the specified connection string and the `Microsoft.EntityFrameworkCore.SqlServer` provider.</span></span> <span data-ttu-id="90d0c-155">Po nawiązaniu połączenia tworzona jest Klasa kontekstu bazy danych o nazwie `MyDbContext` .</span><span class="sxs-lookup"><span data-stu-id="90d0c-155">Once connected, a database context class named `MyDbContext` is created.</span></span> <span data-ttu-id="90d0c-156">Ponadto klasy pomocnicze są tworzone dla `Product` tabel i `Customer` , które zostały określone z `-t` opcjami.</span><span class="sxs-lookup"><span data-stu-id="90d0c-156">Additionally, supporting classes are created for the `Product` and `Customer` tables that were specified with the `-t` options.</span></span> <span data-ttu-id="90d0c-157">Istnieje wiele opcji konfiguracji tego polecenia, aby wygenerować hierarchię klas odpowiednią dla bazy danych.</span><span class="sxs-lookup"><span data-stu-id="90d0c-157">There are many configuration options for this command to generate the class hierarchy appropriate for your database.</span></span> <span data-ttu-id="90d0c-158">Pełne odwołanie można znaleźć [w dokumentacji polecenia](/ef/core/miscellaneous/cli/dotnet#dotnet-ef-dbcontext-scaffold).</span><span class="sxs-lookup"><span data-stu-id="90d0c-158">For a complete reference, see [the command's documentation](/ef/core/miscellaneous/cli/dotnet#dotnet-ef-dbcontext-scaffold).</span></span>

<span data-ttu-id="90d0c-159">Więcej informacji na temat [EF Core](/ef/core/) można znaleźć w witrynie Microsoft docs.</span><span class="sxs-lookup"><span data-stu-id="90d0c-159">More information about [EF Core](/ef/core/) can be found on the Microsoft Docs site.</span></span>

## <a name="interact-with-web-services"></a><span data-ttu-id="90d0c-160">Korzystanie z usług sieci Web</span><span class="sxs-lookup"><span data-stu-id="90d0c-160">Interact with web services</span></span>

<span data-ttu-id="90d0c-161">Po pierwszym wydaniu ASP.NET usługi SOAP były preferowanym sposobem wymiany danych przez serwery i klientów sieci Web.</span><span class="sxs-lookup"><span data-stu-id="90d0c-161">When ASP.NET was first released, SOAP services were the preferred way for web servers and clients to exchange data.</span></span> <span data-ttu-id="90d0c-162">Znacznie zmienił się od tego czasu, a preferowane interakcje z usługami zostały przesunięte w celu bezpośredniego interakcji z klientami HTTP.</span><span class="sxs-lookup"><span data-stu-id="90d0c-162">Much has changed since that time, and the preferred interactions with services have shifted to direct HTTP client interactions.</span></span> <span data-ttu-id="90d0c-163">Za pomocą ASP.NET Core i można Blazor zarejestrować konfigurację `HttpClient` w `Startup` `ConfigureServices` metodzie klasy.</span><span class="sxs-lookup"><span data-stu-id="90d0c-163">With ASP.NET Core and Blazor, you can register the configuration of your `HttpClient` in the `Startup` class's `ConfigureServices` method.</span></span> <span data-ttu-id="90d0c-164">Tej konfiguracji należy użyć, gdy trzeba korzystać z punktu końcowego HTTP.</span><span class="sxs-lookup"><span data-stu-id="90d0c-164">Use that configuration when you need to interact with the HTTP endpoint.</span></span> <span data-ttu-id="90d0c-165">Rozważmy następujący kod konfiguracyjny:</span><span class="sxs-lookup"><span data-stu-id="90d0c-165">Consider the following configuration code:</span></span>

```csharp
services.AddHttpClient("github", client =>
{
    client.BaseAddress = new Uri("http://api.github.com/");
    // Github API versioning
    client.DefaultRequestHeaders.Add("Accept", "application/vnd.github.v3+json");
    // Github requires a user-agent
    client.DefaultRequestHeaders.Add("User-Agent", "BlazorWebForms-Sample");
});
```

<span data-ttu-id="90d0c-166">Za każdym razem, gdy potrzebujesz dostępu do danych z usługi GitHub, Utwórz klienta o nazwie `github` .</span><span class="sxs-lookup"><span data-stu-id="90d0c-166">Whenever you need to access data from GitHub, create a client with a name of `github`.</span></span> <span data-ttu-id="90d0c-167">Klient jest skonfigurowany przy użyciu adresu podstawowego, a nagłówki żądań są odpowiednio ustawiane.</span><span class="sxs-lookup"><span data-stu-id="90d0c-167">The client is configured with the base address, and the request headers are set appropriately.</span></span> <span data-ttu-id="90d0c-168">Wstrzyknąć `IHttpClientFactory` do Blazor składników za pomocą `@inject` dyrektywy lub `[Inject]` atrybutu właściwości.</span><span class="sxs-lookup"><span data-stu-id="90d0c-168">Inject the `IHttpClientFactory` into your Blazor components with the `@inject` directive or an `[Inject]` attribute on a property.</span></span> <span data-ttu-id="90d0c-169">Utwórz użytkownika o nazwie i pracuj z usługami przy użyciu następującej składni:</span><span class="sxs-lookup"><span data-stu-id="90d0c-169">Create your named client and interact with services using the following syntax:</span></span>

```razor
@inject IHttpClientFactory factory

...

@code {
    protected override async Task OnInitializedAsync()
    {
        var client = factory.CreateClient("github");
        var response = await client.GetAsync("repos/dotnet/docs/issues");
        response.EnsureStatusCode();
        var content = await response.Content.ReadAsStringAsync();
    }
}
```

<span data-ttu-id="90d0c-170">Ta metoda zwraca ciąg opisujący kolekcję problemów w repozytorium GitHub */docs* .</span><span class="sxs-lookup"><span data-stu-id="90d0c-170">This method returns the string describing the collection of issues in the *dotnet/docs* GitHub repository.</span></span> <span data-ttu-id="90d0c-171">Zwraca zawartość w formacie JSON i jest deserializowana w odpowiednich obiektach wydania usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="90d0c-171">It returns content in JSON format and is deserialized into appropriate GitHub issue objects.</span></span> <span data-ttu-id="90d0c-172">Istnieje wiele sposobów konfigurowania programu w `HttpClientFactory` celu dostarczania wstępnie skonfigurowanych `HttpClient` obiektów.</span><span class="sxs-lookup"><span data-stu-id="90d0c-172">There are many ways that you can configure the `HttpClientFactory` to deliver preconfigured `HttpClient` objects.</span></span> <span data-ttu-id="90d0c-173">Spróbuj skonfigurować wiele `HttpClient` wystąpień o różnych nazwach i punktach końcowych dla różnych usług sieci Web, z którymi pracujesz.</span><span class="sxs-lookup"><span data-stu-id="90d0c-173">Try configuring multiple `HttpClient` instances with different names and endpoints for the various web services you work with.</span></span> <span data-ttu-id="90d0c-174">Takie podejście umożliwia łatwiejsze współdziałanie z tymi usługami na każdej stronie.</span><span class="sxs-lookup"><span data-stu-id="90d0c-174">This approach will make your interactions with those services easier to work with on each page.</span></span> <span data-ttu-id="90d0c-175">Aby uzyskać więcej informacji, zapoznaj się [z dokumentacją IHttpClientFactory](/aspnet/core/fundamentals/http-requests).</span><span class="sxs-lookup"><span data-stu-id="90d0c-175">For more details, read [the documentation for the IHttpClientFactory](/aspnet/core/fundamentals/http-requests).</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="90d0c-176">[Poprzedni](forms-validation.md) 
> [Dalej](middleware.md)</span><span class="sxs-lookup"><span data-stu-id="90d0c-176">[Previous](forms-validation.md)
[Next](middleware.md)</span></span>
