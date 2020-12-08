---
title: Rejestrowanie w programie .NET
author: IEvangelist
description: Dowiedz się, jak używać struktury rejestrowania dostarczonej przez pakiet NuGet Microsoft. Extensions. Logging.
ms.author: dapine
ms.date: 09/30/2020
ms.openlocfilehash: 73c16c80e7e000533b880e908b38109d2b1e88fd
ms.sourcegitcommit: 45c7148f2483db2501c1aa696ab6ed2ed8cb71b2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/08/2020
ms.locfileid: "96851730"
---
# <a name="logging-in-net"></a>Rejestrowanie w programie .NET

Platforma .NET obsługuje interfejs API rejestrowania, który współpracuje z różnymi dostawcami rejestrowania wbudowanych i innych firm. W tym artykule pokazano, jak używać interfejsu API rejestrowania z wbudowanymi dostawcami. Większość przykładów kodu przedstawionych w tym artykule ma zastosowanie do dowolnej aplikacji platformy .NET korzystającej z [hosta ogólnego](generic-host.md). W przypadku aplikacji, które nie korzystają z hosta ogólnego, zobacz [Aplikacja konsolowa niebędąca hostem](#non-host-console-app).

## <a name="create-logs"></a>Tworzenie dzienników

Aby utworzyć dzienniki, użyj <xref:Microsoft.Extensions.Logging.ILogger%601> obiektu z [iniekcji zależności (di)](dependency-injection.md).

Poniższy przykład:

- Tworzy rejestrator, `ILogger<Worker>` który używa *kategorii* dziennika w pełni kwalifikowanej nazwy typu `Worker` . Kategoria dziennika jest ciągiem, który jest skojarzony z każdym dziennikiem.
- Wywołania <xref:Microsoft.Extensions.Logging.LoggerExtensions.LogInformation%2A> do rejestrowania na `Information` poziomie. *Poziom* dziennika wskazuje ważność rejestrowanego zdarzenia.

:::code language="csharp" source="snippets/configuration/worker-service/Worker.cs" range="9-24" highlight="12":::

[Poziomy](#log-level) i [Kategorie](#log-category) zostały wyjaśnione bardziej szczegółowo w dalszej części tego artykułu.

## <a name="configure-logging"></a>Konfigurowanie rejestrowania

Konfiguracja rejestrowania jest zwykle udostępniana w `Logging` sekcji *AppSettings*. `{Environment}` pliki *. JSON* . Następujące *appsettings.Development.js* pliku są generowane przez szablony usługi procesu roboczego platformy .NET:

:::code language="json" source="snippets/configuration/worker-service/appsettings.Development.json":::

W powyższym kodzie JSON:

- `"Default"`Określono, `"Microsoft"` , i `"Microsoft.Hosting.Lifetime"` Kategorie.
- `"Microsoft"`Kategoria dotyczy wszystkich kategorii, które zaczynają się od `"Microsoft"` .
- `"Microsoft"`Kategoria rejestruje się na poziomie dziennika `Warning` lub wyższym.
- `"Microsoft.Hosting.Lifetime"`Kategoria jest bardziej precyzyjna niż `"Microsoft"` Kategoria, więc jest `"Microsoft.Hosting.Lifetime"` rejestrowana w kategorii na poziomie dziennika "informacje" i wyższych.
- Określony dostawca dziennika nie został określony, dlatego `LogLevel` dotyczy wszystkich włączonych dostawców rejestrowania z wyjątkiem [dziennika zdarzeń systemu Windows](logging-providers.md#windows-eventlog).

`Logging`Właściwość może mieć <xref:Microsoft.Extensions.Logging.LogLevel> właściwości dostawcy dzienników i. `LogLevel`Określa minimalny [poziom](#log-level) rejestrowania wybranych kategorii. W poprzednim pliku JSON `Information` i `Warning` poziomy dziennika są określone. `LogLevel` wskazuje ważność dziennika i zakres od 0 do 6:

`Trace` = 0, `Debug` = 1, `Information` = 2, `Warning` = 3, `Error` = 4, `Critical` = 5 i `None` = 6.

Gdy `LogLevel` jest określony, funkcja rejestrowania jest włączona dla komunikatów na określonym poziomie i wyższych. W poprzednim pliku JSON `Default` Kategoria jest zarejestrowana dla `Information` i wyższa. Na przykład,,, `Information` `Warning` `Error` i `Critical` komunikaty są rejestrowane. Jeśli nie `LogLevel` jest określony, rejestrowane są wartości domyślne na `Information` poziomie. Aby uzyskać więcej informacji, zobacz [poziomy dzienników](#log-level).

Właściwość dostawcy może określać `LogLevel` Właściwość. `LogLevel` w obszarze dostawca Określa poziomy do rejestrowania dla tego dostawcy i zastępuje ustawienia dziennika niedostawcy. Rozważmy następujące *appsettings.js* pliku:

:::code language="json" source="snippets/configuration/worker-service/appsettings.Staging.json":::

Ustawienia w `Logging.{ProviderName}.LogLevel` ustawieniach przesłonięcia w programie `Logging.LogLevel` . W powyższym kodzie JSON `Debug` domyślny poziom rejestrowania dostawcy jest ustawiany na `Information` :

`Logging:Debug:LogLevel:Default:Information`

Powyższe ustawienie określa `Information` poziom rejestrowania dla każdej `Logging:Debug:` kategorii z wyjątkiem `Microsoft.Hosting` . Gdy określona kategoria jest wymieniona, określona Kategoria zastępuje domyślną kategorię. W powyższym formacie JSON `Logging:Debug:LogLevel` Kategorie `"Microsoft.Hosting"` i `"Default"` zastępują ustawienia w `Logging:LogLevel`

Minimalny poziom dziennika można określić dla dowolnego z:

- Określeni dostawcy: na przykład `Logging:EventSource:LogLevel:Default:Information`
- Określone kategorie: na przykład `Logging:LogLevel:Microsoft:Warning`
- Wszyscy dostawcy i wszystkie kategorie: `Logging:LogLevel:Default:Warning`

Wszystkie dzienniki poniżej minimalnego poziomu są ***not** _:

- Przeszedł do dostawcy.
- Zarejestrowane lub wyświetlone.

Aby pominąć wszystkie dzienniki, należy określić [wartość LogLevel. None](xref:Microsoft.Extensions.Logging.LogLevel). `LogLevel.None` ma wartość 6, która jest większa niż `LogLevel.Critical` (5).

Jeśli dostawca obsługuje [zakresy rejestrowania](#log-scopes), `IncludeScopes` wskazuje, czy są one włączone. Aby uzyskać więcej informacji, zobacz [zakresy dzienników](#log-scopes)

Następujące _appsettings.jsw pliku * zawierają ustawienia dla wszystkich wbudowanych dostawców:

:::code language="json" source="snippets/configuration/worker-service/appsettings.Production.json":::

W poprzednim przykładzie:

- Kategorie i poziomy nie są sugerowanymi wartościami. Przykład podano, aby wyświetlić wszystkich dostawców domyślnych.
- Ustawienia w `Logging.{ProviderName}.LogLevel` ustawieniach przesłonięcia w programie `Logging.LogLevel` . Na przykład poziom w `Debug.LogLevel.Default` zastępują poziom w `LogLevel.Default` .
- *Alias* każdego dostawcy jest używany. Każdy dostawca definiuje *alias* , który może być używany w konfiguracji zamiast w pełni kwalifikowanej nazwy typu. Aliasy wbudowane dostawcy to:
  - Konsola
  - Debugowanie
  - EventSource
  - Elemencie
  - AzureAppServicesFile
  - AzureAppServicesBlob
  - ApplicationInsights

### <a name="set-log-level-by-command-line-environment-variables-and-other-configuration"></a>Ustawianie poziomu dziennika według wiersza polecenia, zmiennych środowiskowych i innych konfiguracji

Poziom dziennika może być ustawiony przez dowolnego [dostawcę konfiguracji](configuration-providers.md).

Następujące polecenia:

- Ustaw klucz środowiska na `Logging:LogLevel:Microsoft` wartość `Information` w systemie Windows.
- Przetestuj ustawienia w przypadku korzystania z aplikacji utworzonej przy użyciu szablonów usługi procesu roboczego platformy .NET. `dotnet run`Polecenie musi być uruchamiane w katalogu projektu po użyciu `set` .

```cmd
set Logging__LogLevel__Microsoft=Information
dotnet run
```

Poprzednie ustawienie środowiska:

- Jest ustawiana tylko w ramach procesów uruchomionych z poziomu okna polecenia, które zostały ustawione w.
- Nie są odczytywane przez aplikacje uruchomione w programie Visual Studio.

Następujące polecenie [setx](/windows-server/administration/windows-commands/setx) ustawia również klucz środowiska i wartość w systemie Windows. W przeciwieństwie do `set` , `setx` Ustawienia są utrwalane. `/M`Przełącznik ustawia zmienną w środowisku systemowym. Jeśli `/M` nie jest używany, zmienna środowiskowa użytkownika jest ustawiona.

```cmd
setx Logging__LogLevel__Microsoft=Information /M
```

Na [Azure App Service](https://azure.microsoft.com/services/app-service/)wybierz pozycję **nowe ustawienie aplikacji** na stronie **Konfiguracja > ustawienia** . Ustawienia aplikacji Azure App Service są następujące:

- Szyfrowane i przesyłane przez zaszyfrowanego kanału.
- Uwidocznione jako zmienne środowiskowe.

Aby uzyskać więcej informacji na temat ustawiania wartości konfiguracyjnych platformy .NET przy użyciu zmiennych środowiskowych, zobacz [zmienne środowiskowe](configuration-providers.md#environment-variable-configuration-provider).

## <a name="how-filtering-rules-are-applied"></a>Jak są stosowane reguły filtrowania

Po <xref:Microsoft.Extensions.Logging.ILogger%601> utworzeniu obiektu <xref:Microsoft.Extensions.Logging.ILoggerFactory> obiekt wybiera jedną regułę dla każdego dostawcy, która ma zostać zastosowana do tego rejestratora. Wszystkie komunikaty zapisywane przez `ILogger` wystąpienie są filtrowane na podstawie wybranych reguł. Dla każdego dostawcy i pary kategorii jest wybierana najbardziej konkretna reguła z dostępnych reguł.

Następujący algorytm jest używany dla każdego dostawcy, gdy `ILogger` jest tworzony dla danej kategorii:

- Wybierz wszystkie reguły, które pasują do dostawcy lub jego aliasu. Jeśli nie zostanie znalezione dopasowanie, zaznacz wszystkie reguły z pustym dostawcą.
- W wyniku poprzedniego kroku wybierz pozycję reguły z najdłuższym prefiksem kategorii. Jeśli nie zostanie znalezione dopasowanie, zaznacz wszystkie reguły, które nie określają kategorii.
- Jeśli wybrano wiele reguł, zrób to **ostatnie** .
- Jeśli nie wybrano żadnych reguł, użyj, <xref:Microsoft.Extensions.Logging.LoggingBuilderExtensions.SetMinimumLevel(Microsoft.Extensions.Logging.ILoggingBuilder,Microsoft.Extensions.Logging.LogLevel)?displayProperty=nameWithType> Aby określić minimalny poziom rejestrowania.

## <a name="log-category"></a>Kategoria dziennika

Po `ILogger` utworzeniu obiektu zostanie określona *Kategoria* . Ta kategoria jest dołączona do każdego komunikatu dziennika utworzonego przez to wystąpienie `ILogger` . Ciąg kategorii jest dowolny, ale Konwencja ma używać nazwy klasy. Na przykład w aplikacji z usługą zdefiniowaną jako następujący obiekt może być kategorią `"Example.DefaultService"` :

```csharp
namespace Example
{
    public class DefaultService : IService
    {
        private readonly ILogger<DefaultService> _logger;

        public DefaultService(ILogger<DefaultService> logger) =>
            _logger = logger;

        // ...
    }
}
```

Aby jawnie określić kategorię, wywołaj <xref:Microsoft.Extensions.Logging.LoggerFactory.CreateLogger%2A?displayProperty=nameWithType> :

```csharp
namespace Example
{
    public class DefaultService : IService
    {
        private readonly ILogger _logger;

        public DefaultService(ILoggerFactory loggerFactory) =>
            _logger = loggerFactory.CreateLogger("CustomCategory");

        // ...
    }
}
```

Wywoływanie `CreateLogger` przy użyciu stałej nazwy może być przydatne w przypadku używania wielu metod, dzięki czemu zdarzenia mogą być zorganizowane według kategorii.

`ILogger<T>` jest odpowiednikiem wywołania `CreateLogger` z w pełni kwalifikowaną nazwą typu `T` .

## <a name="log-level"></a>Poziom dziennika

W poniższej tabeli wymieniono <xref:Microsoft.Extensions.Logging.LogLevel> wartości, wygodną `Log{LogLevel}` metodę rozszerzenia oraz Sugerowane użycie:

| LogLevel | Wartość | Metoda | Opis |
|--|--|--|--|
| [Ślad](xref:Microsoft.Extensions.Logging.LogLevel) | 0 | <xref:Microsoft.Extensions.Logging.LoggerExtensions.LogTrace%2A> | Zawierają najwięcej szczegółowych komunikatów. Te komunikaty mogą zawierać poufne dane aplikacji. Te komunikaty są domyślnie wyłączone i **nie** powinny być włączone w środowisku produkcyjnym. |
| [Debugowanie](xref:Microsoft.Extensions.Logging.LogLevel) | 1 | <xref:Microsoft.Extensions.Logging.LoggerExtensions.LogDebug%2A> | Na potrzeby debugowania i programowania. W środowisku produkcyjnym należy używać ostrożnie z powodu dużego wolumenu. |
| [Informacje](xref:Microsoft.Extensions.Logging.LogLevel) | 2 | <xref:Microsoft.Extensions.Logging.LoggerExtensions.LogInformation%2A> | Śledzi ogólny przepływ aplikacji. Może mieć wartość długoterminową. |
| [Ostrzeżenie](xref:Microsoft.Extensions.Logging.LogLevel) | 3 | <xref:Microsoft.Extensions.Logging.LoggerExtensions.LogWarning%2A> | Dla nietypowych lub nieoczekiwanych zdarzeń. Zwykle zawiera błędy lub warunki, które nie powodują błędu aplikacji. |
| [Błąd](xref:Microsoft.Extensions.Logging.LogLevel) | 4 | <xref:Microsoft.Extensions.Logging.LoggerExtensions.LogError%2A> | W przypadku błędów i wyjątków, których nie można obsłużyć. Te komunikaty wskazują na niepowodzenie podczas bieżącej operacji lub żądania, a nie awarię całej aplikacji. |
| [Krytyczne](xref:Microsoft.Extensions.Logging.LogLevel) | 5 | <xref:Microsoft.Extensions.Logging.LoggerExtensions.LogCritical%2A> | Dla niepowodzeń, które wymagają natychmiastowej uwagi. Przykłady: scenariusze utraty danych, brak miejsca na dysku. |
| [Brak](xref:Microsoft.Extensions.Logging.LogLevel) | 6 |  | Określa, że nie należy zapisywać żadnych komunikatów. |

W poprzedniej tabeli `LogLevel` znajduje się na liście od najniższej do najwyższej wagi.

Pierwszy parametr metody [log](xref:Microsoft.Extensions.Logging.LoggerExtensions) <xref:Microsoft.Extensions.Logging.LogLevel> wskazuje ważność dziennika. Zamiast wywoływania `Log(LogLevel, ...)` , większość deweloperów wywołuje metody rozszerzenia [dziennika {LogLevel}](xref:Microsoft.Extensions.Logging.LoggerExtensions) . `Log{LogLevel}`Metody rozszerzające [wywołują metodę log i określają wartość LogLevel](https://github.com/dotnet/extensions/blob/release/3.1/src/Logging/Logging.Abstractions/src/LoggerExtensions.cs). Na przykład następujące dwa wywołania rejestrowania są funkcjonalnie równoważne i generują ten sam dziennik:

```csharp
public void LogDetails()
{
    var logMessage = "Details for log.";

    _logger.Log(LogLevel.Information, AppLogEvents.Details, logMessage);
    _logger.LogInformation(AppLogEvents.Details, logMessage);
}
```

`AppLogEvents.Details` jest IDENTYFIKATORem zdarzenia i jest niejawnie reprezentowany przez wartość stałą <xref:System.Int32> . `AppLogEvents` jest klasą, która ujawnia różne nazwane identyfikatory i jest wyświetlana w sekcji [Identyfikator zdarzenia dziennika](#log-event-id) .

Poniższy kod tworzy `Information` i `Warning` rejestruje:

```csharp
public async Task<T> GetAsync<T>(string id)
{
    _logger.LogInformation(AppLogEvents.Read, "Reading value for {Id}", id);

    var result = await _repository.GetAsync(id);
    if (result is null)
    {
        _logger.LogWarning(AppLogEvents.ReadNotFound, "GetAsync({Id}) not found", id);
    }

    return result;
}
```

W poprzednim kodzie pierwszy `Log{LogLevel}` parametr, `AppLogEvents.Read` , jest [Identyfikator zdarzenia dziennika](#log-event-id). Drugi parametr jest szablonem wiadomości z symbolami zastępczymi dla wartości argumentów dostarczonych przez pozostałe parametry metody. Parametry metody zostały wyjaśnione w sekcji [szablon komunikatu](#log-message-template) w dalszej części tego artykułu.

Skonfiguruj odpowiedni poziom dziennika i Wywołaj odpowiednie `Log{LogLevel}` metody, aby kontrolować, ile danych wyjściowych dziennika jest zapisywana w określonym nośniku magazynowania. Na przykład:

- W środowisku produkcyjnym:
  - Rejestrowanie na poziomie `Trace` lub `Information` powoduje utworzenie dużej ilości szczegółowych komunikatów dziennika. Aby kontrolować koszty i nie przekraczać limitów magazynowania danych `Trace` , `Information` komunikaty dzienników i na poziomie magazynu o dużej ilości danych. Rozważ ograniczenie `Trace` i `Information` do określonych kategorii.
  - Rejestrowanie przy `Warning` użyciu `Critical` poziomów powinno generować kilka komunikatów dziennika.
    - Koszty i limity magazynu zazwyczaj nie są przedmiotem obaw.
    - Niektóre dzienniki zapewniają większą elastyczność w zakresie wyboru magazynu danych.
- W programie Development:
  - Ustaw wartość `Warning`.
  - Dodawanie `Trace` lub `Information` komunikaty podczas rozwiązywania problemów. Aby ograniczyć ilość danych wyjściowych, ustaw `Trace` lub `Information` tylko dla kategorii poddawanych badaniu.

Następujące zestawy JSON `Logging:Console:LogLevel:Microsoft:Information` :

:::code language="json" source="snippets/configuration/worker-service/appsettings.MSFT.json":::

## <a name="log-event-id"></a>Identyfikator zdarzenia dziennika

Każdy dziennik może określać _event identyfikator *, <xref:Microsoft.Extensions.Logging.EventId> jest strukturą z `Id` i opcjonalnymi `Name` właściwościami tylko do odczytu. Przykładowy kod źródłowy używa `AppLogEvents` klasy do definiowania identyfikatorów zdarzeń:

```csharp
internal static class AppLogEvents
{
    internal const int Create = 1000;
    internal const int Read = 1001;
    internal const int Update = 1002;
    internal const int Delete = 1003;

    internal const int Details = 3000;
    internal const int Error = 3001;

    internal const int ReadNotFound = 4000;
    internal const int UpdateNotFound = 4001;

    // ...
}
```

Identyfikator zdarzenia kojarzy zestaw zdarzeń. Na przykład wszystkie dzienniki związane z odczytem wartości z repozytorium mogą być `1001` .

Dostawca rejestrowania może rejestrować identyfikator zdarzenia w polu identyfikatora, w komunikacie rejestrowania lub wcale. Dostawca debugowania nie pokazuje identyfikatorów zdarzeń. Dostawca konsoli pokazuje identyfikatory zdarzeń w nawiasach po kategorii:

```console
info: Example.DefaultService.GetAsync[1001]
      Reading value for a1b2c3
warn: Example.DefaultService.GetAsync[4000]
      GetAsync(a1b2c3) not found
```

Niektórzy dostawcy rejestrowania przechowują identyfikator zdarzenia w polu, co umożliwia filtrowanie identyfikatorów.

## <a name="log-message-template"></a>Szablon komunikatu dziennika

Każdy interfejs API dziennika używa szablonu wiadomości. Szablon wiadomości może zawierać symbole zastępcze, dla których podano argumenty. Użyj nazw dla symboli zastępczych, a nie liczby. Kolejność symboli zastępczych, nie ich nazw, określa, które parametry są używane do dostarczania ich wartości. W poniższym kodzie nazwy parametrów są spoza sekwencji w szablonie wiadomości:

```csharp
string p1 = "param1";
string p2 = "param2";
_logger.LogInformation("Parameter values: {p2}, {p1}", p1, p2);
```

Poprzedni kod tworzy komunikat dziennika z wartościami parametrów w kolejności:

```text
Parameter values: param1, param2
```

Takie podejście umożliwia dostawcom rejestrowania implementowanie [semantyki lub rejestrowania strukturalnego](https://github.com/NLog/NLog/wiki/How-to-use-structured-logging). Same argumenty są przesyłane do systemu rejestrowania, a nie tylko dla sformatowanego szablonu wiadomości. Umożliwia to dostawcom rejestrowania przechowywanie wartości parametrów jako pól. Rozważmy następujące metody rejestrowania:

```csharp
_logger.LogInformation("Getting item {Id} at {RunTime}", id, DateTime.Now);
```

Na przykład podczas rejestrowania w usłudze Azure Table Storage:

- Każda jednostka tabeli platformy Azure może `ID` mieć `RunTime` właściwości i.
- Tabele z właściwościami upraszczają zapytania dotyczące zarejestrowanych danych. Na przykład zapytanie może znaleźć wszystkie dzienniki w określonym `RunTime` zakresie bez konieczności analizowania limitu czasu wiadomości tekstowej.

## <a name="log-exceptions"></a>Rejestrowanie wyjątków

Metody rejestratora mają przeciążenia przyjmujące parametr wyjątku:

```csharp
public void Test(string id)
{
    try
    {
        if (id == "none")
        {
            throw new Exception("Default Id detected.");
        }
    }
    catch (Exception ex)
    {
        _logger.LogWarning(
            AppLogEvents.Error, ex,
            "Failed to process iteration: {Id}", id)
    }
}
```

Rejestrowanie wyjątków jest specyficzne dla dostawcy.

### <a name="default-log-level"></a>Domyślny poziom dziennika

Jeśli domyślny poziom rejestrowania nie jest ustawiony, domyślna wartość poziomu dziennika to `Information` .

Rozważmy na przykład następującą aplikację usługi Worker:

- Utworzono za pomocą szablonów procesów roboczych platformy .NET.
- *appsettings.json* i *appsettings.Development.jspo* usunięciu lub zmianie nazwy.

Po powyższej instalacji przechodzenie do strony prywatność lub Strona główna powoduje utworzenie wielu `Trace` , `Debug` i `Information`  komunikatów z `Microsoft` nazwą kategorii.

Poniższy kod ustawia domyślny poziom rejestrowania, jeśli domyślny poziom rejestrowania nie jest ustawiony w konfiguracji:

```csharp
class Program
{
    static Task Main(string[] args) =>
        CreateHostBuilder(args).Build().RunAsync();

    static IHostBuilder CreateHostBuilder(string[] args) =>
        Host.CreateDefaultBuilder(args)
            .ConfigureLogging(logging => logging.SetMinimumLevel(LogLevel.Warning));
}
```

### <a name="filter-function"></a>Funkcja filtrowania

Funkcja filtru jest wywoływana dla wszystkich dostawców i kategorii, które nie mają przypisanych do nich reguł przez konfigurację lub kod:

```csharp
class Program
{
    static Task Main(string[] args) =>
        CreateHostBuilder(args).Build().RunAsync();

    static IHostBuilder CreateHostBuilder(string[] args) =>
        Host.CreateDefaultBuilder(args)
            .ConfigureLogging(logging =>
                logging.AddFilter((provider, category, logLevel) =>
                {
                    return provider.Contains("ConsoleLoggerProvider")
                        && (category.Contains("Example") || category.Contains("Microsoft"))
                        && logLevel >= LogLevel.Information;
                }));
}
```

Poprzedni kod wyświetla dzienniki konsoli, gdy kategoria zawiera `Example` lub `Microsoft` i poziom dziennika jest `Information` lub wyższy.

## <a name="log-scopes"></a>Zakresy dziennika

 *Zakres* może grupować zestaw operacji logicznych. Takie grupowanie może służyć do dołączania tych samych danych do każdego dziennika, który został utworzony jako część zestawu. Na przykład każdy dziennik utworzony w ramach przetwarzania transakcji może zawierać identyfikator transakcji.

Zakres:

- Jest <xref:System.IDisposable> typem zwracanym przez <xref:Microsoft.Extensions.Logging.ILogger.BeginScope%2A> metodę.
- Obowiązuje do momentu jego usunięcia.

Następujące dostawcy obsługują zakresy:

- `Console`
- [AzureAppServicesFile i AzureAppServicesBlob](xref:Microsoft.Extensions.Logging.AzureAppServices.BatchingLoggerOptions.IncludeScopes)

Użyj zakresu przez Zawijanie wywołań rejestratora w `using` bloku:

```csharp
public async Task<T> GetAsync<T>(string id)
{
    T result;

    using (_logger.BeginScope("using block message"))
    {
        _logger.LogInformation(
            AppLogEvents.Read, "Reading value for {Id}", id);

        var result = await _repository.GetAsync(id);
        if (result is null)
        {
            _logger.LogWarning(
                AppLogEvents.ReadNotFound, "GetAsync({Id}) not found", id);
        }
    }

    return result;
}
```

Poniższy kod JSON włącza zakresy dla dostawcy konsoli:

:::code language="json" source="snippets/configuration/worker-service/appsettings.IncludeScopes.json" highlight="9":::

Poniższy kod włącza zakresy dla dostawcy konsoli:

```csharp
class Program
{
    static Task Main(string[] args) =>
        CreateHostBuilder(args).Build().RunAsync();

    static IHostBuilder CreateHostBuilder(string[] args) =>
        Host.CreateDefaultBuilder(args)
            .ConfigureLogging((_, logging) =>
                logging.ClearProviders()
                    .AddConsole(options => options.IncludeScopes = true));
}
```

## <a name="non-host-console-app"></a>Aplikacja konsolowa niebędąca hostem

Rejestrowanie kodu dla aplikacji, które nie jest [hostem ogólnym](generic-host.md) , różni się w sposób, w jaki [są dodawane dostawcy](logging-providers.md#built-in-logging-providers) i [są tworzone rejestratory](#create-logs). W aplikacji konsolowej innej niż host Wywołaj `Add{provider name}` metodę rozszerzenia dostawcy podczas tworzenia `LoggerFactory` :

```csharp
class Program
{
    static void Main(string[] args)
    {
        using var loggerFactory = LoggerFactory.Create(builder =>
        {
            builder
                .AddFilter("Microsoft", LogLevel.Warning)
                .AddFilter("System", LogLevel.Warning)
                .AddFilter("LoggingConsoleApp.Program", LogLevel.Debug)
                .AddConsole();
        });

        ILogger logger = loggerFactory.CreateLogger<Program>();
        logger.LogInformation("Example log message");
    }
}
```

`loggerFactory`Obiekt jest używany do tworzenia <xref:Microsoft.Extensions.Logging.ILogger> wystąpienia.

## <a name="create-logs-in-main"></a>Tworzenie dzienników w głównej

Następujący kod jest zarejestrowana `Main` przez pobranie `ILogger` wystąpienia z programu di po skompilowaniu hosta:

```csharp
using System;
using System.Threading.Tasks;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
using Microsoft.Extensions.Logging;

class Program
{
    static Task Main(string[] args)
    {
        IHost host = Host.CreateDefaultBuilder(args).Build();

        var logger = host.Services.GetRequiredService<ILogger<Program>>();
        logger.LogInformation("Host created.");

        return host.RunAsync();
    }
}
```

### <a name="no-asynchronous-logger-methods"></a>Brak metod rejestratora asynchronicznego

Rejestracja powinna być tak szybka, że nie jest to koszt wydajności kodu asynchronicznego. Jeśli magazyn danych rejestrowania jest wolny, nie zapisuj go bezpośrednio. Rozważ ręczne zapisanie komunikatów dziennika w szybkim magazynie, a następnie przeniesienie ich do wolnego magazynu później. Na przykład podczas rejestrowania do SQL Server nie należy tego robić bezpośrednio w `Log` metodzie, ponieważ `Log` metody są synchroniczne. Zamiast tego można synchronicznie dodawać komunikaty dziennika do kolejki w pamięci, a proces roboczy w tle ściągał komunikaty z kolejki, aby wykonać asynchroniczne działanie wypychania danych do SQL Server.

## <a name="change-log-levels-in-a-running-app"></a>Zmień poziomy dziennika w działającej aplikacji

Interfejs API rejestrowania nie zawiera scenariusza zmiany poziomów rejestrowania, gdy aplikacja jest uruchomiona. Niektórzy dostawcy konfiguracji mogą jednak ponownie ładować konfigurację, która zacznie natychmiastowo wpływać na konfigurację rejestrowania. Na przykład [dostawca konfiguracji plików](configuration-providers.md#file-configuration-provider) ponownie ładuje konfigurację rejestrowania domyślnie. Jeśli konfiguracja zostanie zmieniona w kodzie w czasie, gdy aplikacja jest uruchomiona, aplikacja może wywołać [IConfigurationRoot. reload](xref:Microsoft.Extensions.Configuration.IConfigurationRoot.Reload%2A) , aby zaktualizować konfigurację rejestrowania aplikacji.

## <a name="nuget-packages"></a>Pakiety NuGet

<xref:Microsoft.Extensions.Logging.ILogger%601>Interfejsy i <xref:Microsoft.Extensions.Logging.ILoggerFactory> i implementacje są zawarte w zestaw .NET Core SDK. Są one również dostępne w następujących pakietach NuGet:

- Interfejsy są w [Microsoft. Extensions. Logging. Abstracts](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Abstractions).
- Implementacje domyślne są w [Microsoft. Extensions. Logging](https://www.nuget.org/packages/microsoft.extensions.logging).

## <a name="apply-log-filter-rules-in-code"></a>Zastosuj reguły filtru dziennika w kodzie

Preferowanym podejściem do ustawiania reguł filtru dziennika jest użycie [konfiguracji](configuration.md).

Poniższy przykład pokazuje, jak zarejestrować reguły filtru w kodzie:

```csharp
class Program
{
    static Task Main(string[] args) =>
        CreateHostBuilder(args).Build().RunAsync();

    static IHostBuilder CreateHostBuilder(string[] args) =>
        Host.CreateDefaultBuilder(args)
            .ConfigureLogging(logging =>
               logging.AddFilter("System", LogLevel.Debug)
                  .AddFilter<DebugLoggerProvider>("Microsoft", LogLevel.Information)
                  .AddFilter<ConsoleLoggerProvider>("Microsoft", LogLevel.Trace));
}
```

`logging.AddFilter("System", LogLevel.Debug)` Określa `System` kategorię i poziom dziennika `Debug` . Filtr jest stosowany do wszystkich dostawców, ponieważ określony dostawca nie został skonfigurowany.

`AddFilter<DebugLoggerProvider>("Microsoft", LogLevel.Information)` określając

- `Debug`Dostawca rejestrowania.
- Poziom dziennika `Information` lub wyższy.
- Wszystkie kategorie zaczynające się od `"Microsoft"` .

## <a name="see-also"></a>Zobacz też

- [Dostawcy rejestrowania w programie .NET](logging-providers.md)
- [Implementowanie niestandardowego dostawcy rejestrowania w programie .NET](custom-logging-provider.md)
- [Formatowanie dziennika konsoli](console-log-formatter.md)
- [Rejestrowanie o wysokiej wydajności w programie .NET](high-performance-logging.md)
- Błędy rejestrowania należy utworzyć w repozytorium [GitHub.com/dotnet/Extensions](https://github.com/dotnet/extensions/issues)
