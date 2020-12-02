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
# <a name="work-with-data"></a>Praca z danymi

Dostęp do danych to szkielet aplikacji ASP.NET Web Forms. W przypadku kompilowania formularzy dla sieci Web, co się dzieje z tymi danymi? Korzystając z formularzy sieci Web, istniały wiele technik dostępu do danych, których można użyć do współpracy z bazą danych:

- Źródła danych
- ADO.NET
- Entity Framework

Źródła danych były kontrolkami, które można umieścić na stronie formularzy sieci Web i skonfigurować tak jak inne kontrolki. Program Visual Studio udostępnia przyjazny zestaw okien dialogowych umożliwiających konfigurowanie i powiązywanie kontrolek ze stronami formularzy sieci Web. Deweloperzy korzystający z metody "Low Code" lub "No Code" preferują tę technikę, gdy formularze sieci Web zostały po raz pierwszy wydane.

![Źródła danych](media/data/datasources.png)

ADO.NET jest podejściem niskiego poziomu służącym do współdziałania z bazą danych. Aplikacje mogą utworzyć połączenie z bazą danych z poleceniami, zestawami rekordów i zestawami DataSets w celu manipulowania nimi. Wyniki można następnie powiązać z polami na ekranie bez wielu kodów. Wadą tego podejścia było to, że każdy zestaw obiektów ADO.NET ( `Connection` , `Command` i `Recordset` ) został powiązany z bibliotekami dostarczonymi przez dostawcę bazy danych. Użycie tych składników sprawia, że kod jest sztywny i trudny do migracji do innej bazy danych.

## <a name="entity-framework"></a>Entity Framework

Entity Framework (EF) to struktura mapowania relacyjnego obiektu źródłowego obsługiwana przez platformę .NET Foundation. Początkowo wydane z .NET Framework, EF umożliwia generowanie kodu dla połączeń baz danych, schematów magazynu i interakcji. Dzięki temu abstrakcji możesz skupić się na regułach firmy aplikacji i umożliwić zarządzanie bazą danych przez zaufanego administratora bazy danych. W programie .NET można użyć zaktualizowanej wersji EF o nazwie EF Core. EF Core pomaga generować i obsługiwać interakcje między kodem i bazą danych z serią poleceń, które są dostępne za pomocą `dotnet ef` narzędzia wiersza polecenia. Przyjrzyjmy się kilku przykładom, aby rozpocząć pracę z bazą danych.

### <a name="ef-code-first"></a>Dr Code First

Szybkim sposobem na rozpoczęcie tworzenia interakcji z bazą danych jest rozpoczęcie od obiektów klasy, z którymi chcesz współpracować. EF udostępnia narzędzie, które pomaga wygenerować odpowiedni kod bazy danych dla klas. Takie podejście nazywa się "Code First" programowaniem. Rozważmy następujące `Product` klasy dla przykładowej aplikacji w sklepie, która ma być przechowywana w relacyjnej bazie danych, takiej jak Microsoft SQL Server.

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

Produkt ma klucz podstawowy i trzy dodatkowe pola, które zostałyby utworzone w bazie danych:  

- EF zidentyfikuje `Id` Właściwość jako klucz podstawowy według Konwencji.
- `Name` będą przechowywane w kolumnie skonfigurowanej do przechowywania tekstu. `[Required]`Atrybut dekorowania nazwy tej właściwości spowoduje dodanie ograniczenia, `not null` które pomoże wymusić to zadeklarowane zachowanie właściwości.
- `Description` będą przechowywane w kolumnie skonfigurowanej do przechowywania tekstu i mają maksymalną długość skonfigurowaną 4000 znaków zgodnie z `[MaxLength]` atrybutem. Schemat bazy danych zostanie skonfigurowany z kolumną o nazwie `MaxLength` przy użyciu typu danych `varchar(4000)` .
- `Price`Właściwość będzie przechowywana jako waluta. Ten `[Range]` atrybut generuje odpowiednie ograniczenia, aby zapobiec przechowywaniu danych poza minimalnym i maksymalnym zadeklarowanymi wartościami.

Musimy dodać tę `Product` klasę do klasy kontekstu bazy danych, która definiuje operacje połączenia i translacji z naszą bazą danych.

```csharp
public class MyDbContext : DbContext
{
    public DbSet<Product> Products { get; set; }
}
```

`MyDbContext`Klasa zawiera jedną właściwość, która definiuje dostęp i tłumaczenie dla `Product` klasy.  Twoja aplikacja konfiguruje tę klasę do interakcji z bazą danych przy użyciu następujących wpisów w `Startup` `ConfigureServices` metodzie klasy:

```csharp
services.AddDbContext<MyDbContext>(options =>
    options.UseSqlServer("MY DATABASE CONNECTION STRING"));
```

Poprzedni kod będzie łączyć się z bazą danych SQL Server przy użyciu określonych parametrów połączenia. Parametry połączenia można umieścić w *appsettings.jsw* pliku, zmiennych środowiskowych lub w innych lokalizacjach magazynu konfiguracji i odpowiednio zastąpić ten osadzony ciąg.

Następnie można wygenerować tabelę bazy danych odpowiednią dla tej klasy przy użyciu następujących poleceń:

```dotnetcli
dotnet ef migrations add 'Create Product table'
dotnet ef database update
```

Pierwsze polecenie definiuje zmiany wprowadzane w schemacie bazy danych jako nową migrację EF o nazwie `Create Product table` .  Migracja definiuje sposób stosowania i usuwania nowych zmian w bazie danych.

Po zastosowaniu należy mieć prostą `Product` tabelę w bazie danych oraz kilka nowych klas dodanych do projektu, które ułatwiają zarządzanie schematem bazy danych.  Te wygenerowane klasy można domyślnie znaleźć w nowym folderze o nazwie *migrations*.  Po wprowadzeniu zmian w `Product` klasie lub dodaniu bardziej powiązanych klas, które mają być używane z bazą danych, należy ponownie uruchomić polecenia wiersza polecenia przy użyciu nowej nazwy migracji.  To polecenie spowoduje wygenerowanie innego zestawu klas migracji w celu zaktualizowania schematu bazy danych.

### <a name="ef-database-first"></a>Dr Database First

W przypadku istniejących baz danych można generować klasy dla EF Core przy użyciu narzędzi wiersza polecenia platformy .NET. Aby szkieletować klasy, należy użyć odmiany następującego polecenia:

```dotnetcli
dotnet ef dbcontext scaffold "CONNECTION STRING" Microsoft.EntityFrameworkCore.SqlServer -c MyDbContext -t Product -t Customer
```

Poprzednie polecenie nawiązuje połączenie z bazą danych przy użyciu określonych parametrów połączenia i `Microsoft.EntityFrameworkCore.SqlServer` dostawcy. Po nawiązaniu połączenia tworzona jest Klasa kontekstu bazy danych o nazwie `MyDbContext` . Ponadto klasy pomocnicze są tworzone dla `Product` tabel i `Customer` , które zostały określone z `-t` opcjami. Istnieje wiele opcji konfiguracji tego polecenia, aby wygenerować hierarchię klas odpowiednią dla bazy danych. Pełne odwołanie można znaleźć [w dokumentacji polecenia](/ef/core/miscellaneous/cli/dotnet#dotnet-ef-dbcontext-scaffold).

Więcej informacji na temat [EF Core](/ef/core/) można znaleźć w witrynie Microsoft docs.

## <a name="interact-with-web-services"></a>Korzystanie z usług sieci Web

Po pierwszym wydaniu ASP.NET usługi SOAP były preferowanym sposobem wymiany danych przez serwery i klientów sieci Web. Znacznie zmienił się od tego czasu, a preferowane interakcje z usługami zostały przesunięte w celu bezpośredniego interakcji z klientami HTTP. Za pomocą ASP.NET Core i można Blazor zarejestrować konfigurację `HttpClient` w `Startup` `ConfigureServices` metodzie klasy. Tej konfiguracji należy użyć, gdy trzeba korzystać z punktu końcowego HTTP. Rozważmy następujący kod konfiguracyjny:

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

Za każdym razem, gdy potrzebujesz dostępu do danych z usługi GitHub, Utwórz klienta o nazwie `github` . Klient jest skonfigurowany przy użyciu adresu podstawowego, a nagłówki żądań są odpowiednio ustawiane. Wstrzyknąć `IHttpClientFactory` do Blazor składników za pomocą `@inject` dyrektywy lub `[Inject]` atrybutu właściwości. Utwórz użytkownika o nazwie i pracuj z usługami przy użyciu następującej składni:

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

Ta metoda zwraca ciąg opisujący kolekcję problemów w repozytorium GitHub */docs* . Zwraca zawartość w formacie JSON i jest deserializowana w odpowiednich obiektach wydania usługi GitHub. Istnieje wiele sposobów konfigurowania programu w `HttpClientFactory` celu dostarczania wstępnie skonfigurowanych `HttpClient` obiektów. Spróbuj skonfigurować wiele `HttpClient` wystąpień o różnych nazwach i punktach końcowych dla różnych usług sieci Web, z którymi pracujesz. Takie podejście umożliwia łatwiejsze współdziałanie z tymi usługami na każdej stronie. Aby uzyskać więcej informacji, zapoznaj się [z dokumentacją IHttpClientFactory](/aspnet/core/fundamentals/http-requests).

>[!div class="step-by-step"]
>[Poprzedni](forms-validation.md) 
> [Dalej](middleware.md)
