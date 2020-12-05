---
title: Dostawcy rejestrowania w programie .NET
description: Dowiedz się, w jaki sposób interfejs API dostawcy rejestrowania jest używany w aplikacjach .NET.
author: IEvangelist
ms.author: dapine
ms.date: 12/04/2020
ms.openlocfilehash: fdec9018e58c6038b5589c01e775bbb5f10b6b10
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740091"
---
# <a name="logging-providers-in-net"></a>Dostawcy rejestrowania w programie .NET

Dostawcy rejestrowania utrwalają dzienniki, z wyjątkiem `Console` dostawcy, które wyświetlają tylko dzienniki jako dane wyjściowe Standard. Na przykład dostawca usługi Azure Application Insights przechowuje dzienniki w usłudze Azure Application Insights. Można włączyć wielu dostawców.

Domyślne szablony aplikacji programu .NET Worker:

- Użyj [hosta ogólnego](generic-host.md).
- Wywołanie <xref:Microsoft.Extensions.Hosting.Host.CreateDefaultBuilder%2A> , które dodaje następujących dostawców rejestrowania:
  - [Konsola](#console)
  - [Rozpocząć](#debug)
  - [EventSource](#event-source)
  - [EventLog](#windows-eventlog): tylko system Windows

:::code language="csharp" source="snippets/configuration/console/Program.cs" highlight="18":::

Poprzedni kod przedstawia `Program` klasę utworzoną za pomocą szablonów aplikacji roboczych platformy .NET. W następnych sekcjach przedstawiono przykłady na podstawie szablonów aplikacji procesów roboczych platformy .NET, które korzystają z hosta ogólnego.

Aby zastąpić domyślny zestaw dostawców rejestrowania dodanych przez `Host.CreateDefaultBuilder` , wywołaj `ClearProviders` i Dodaj żądanych dostawców rejestrowania. Na przykład następujący kod:

- Wywołuje, <xref:Microsoft.Extensions.Logging.LoggingBuilderExtensions.ClearProviders%2A> Aby usunąć wszystkie <xref:Microsoft.Extensions.Logging.ILoggerProvider> wystąpienia z konstruktora.
- Dodaje dostawcę rejestrowania [konsoli](#console) .

```csharp
static IHostBuilder CreateHostBuilder(string[] args) =>
    Host.CreateDefaultBuilder(args)
        .ConfigureLogging(logging =>
        {
            logging.ClearProviders();
            logging.AddConsole();
        });
```

Aby uzyskać dodatkowych dostawców, zobacz:

- [Wbudowani dostawcy rejestrowania](#built-in-logging-providers).
- [Dostawcy rejestrowania innych firm](#third-party-logging-providers).

## <a name="configure-a-service-that-depends-on-ilogger"></a>Konfigurowanie usługi, która zależy od ILogger

Aby skonfigurować usługę, która jest zależna od `ILogger<T>` programu, należy użyć iniekcji konstruktora lub dostarczyć metody fabryki. Podejście metody fabryki jest zalecane tylko wtedy, gdy nie ma żadnych innych opcji. Rozważmy na przykład usługę, która wymaga `ILogger<T>` wystąpienia przez di:

```csharp
.ConfigureServices(services =>
    services.AddSingleton<IExampleService>(container =>
        new DefaultExampleService
        {
            Logger = container.GetRequiredService<ILogger<IExampleService>>()
        }));
```

Poprzedzający kod to [Func<IServiceProvider, IExampleService>](/dotnet/api/system.func-2) , który jest uruchamiany po raz pierwszy, należy utworzyć wystąpienie `IExampleService` . W ten sposób można uzyskać dostęp do dowolnych zarejestrowanych usług.

## <a name="built-in-logging-providers"></a>Wbudowani dostawcy rejestrowania

Rozszerzenia firmy Microsoft obejmują następujących dostawców rejestrowania w ramach bibliotek środowiska uruchomieniowego:

- [Konsola](#console)
- [Rozpocząć](#debug)
- [EventSource](#event-source)
- [Elemencie](#windows-eventlog)

Następujący dostawcy rejestrowania są dostarczani przez firmę Microsoft, ale nie jako część bibliotek środowiska uruchomieniowego. Muszą być zainstalowane jako dodatkowe pakiety NuGet.

- [AzureAppServicesFile i AzureAppServicesBlob](#azure-app-service)
- [ApplicationInsights](#azure-application-insights)

### <a name="console"></a>Konsola

`Console`Dostawca rejestruje dane wyjściowe w konsoli programu.

### <a name="debug"></a>Debugowanie

`Debug`Dostawca zapisuje dane wyjściowe dziennika za pomocą klasy [System. Diagnostics. Debug](/dotnet/api/system.diagnostics.debug) . Wywołania do `System.Diagnostics.Debug.WriteLine` zapisu dla `Debug` dostawcy.

W systemie Linux `Debug` Lokalizacja dziennika dostawcy jest zależna od dystrybucji i może być jedną z następujących czynności:

- */var/log/message*
- */var/log/syslog*

### <a name="event-source"></a>Źródło zdarzeń

`EventSource`Dostawca zapisuje do międzyplatformowego źródła zdarzeń o nazwie `Microsoft-Extensions-Logging` . W systemie Windows Dostawca używa [funkcji ETW](/windows/win32/etw/event-tracing-portal).

#### <a name="dotnet-trace-tooling"></a>narzędzia śledzenia dotnet

Narzędzie do [śledzenia dotnet](../diagnostics/dotnet-trace.md) to międzyplatformowe narzędzie globalne interfejsu wiersza polecenia, które umożliwia zbieranie śladów programu .NET Core uruchomionego procesu. Narzędzie zbiera <xref:Microsoft.Extensions.Logging.EventSource> dane dostawcy za pomocą <xref:Microsoft.Extensions.Logging.EventSource.LoggingEventSource> .

Aby uzyskać instrukcje dotyczące instalacji, zobacz [dotnet-Trace](../diagnostics/dotnet-trace.md) . Aby zapoznać się z samouczkiem diagnostycznym korzystającym z programu `dotnet-trace` , zobacz [debugowanie wysokiego użycia procesora CPU w programie .NET Core](../diagnostics/debug-highcpu.md).

### <a name="windows-eventlog"></a>Dziennik zdarzeń systemu Windows

`EventLog`Dostawca wysyła dane wyjściowe dziennika do dziennika zdarzeń systemu Windows. W przeciwieństwie do innych dostawców, `EventLog` dostawca programu nie **not** powinien dziedziczyć domyślnych ustawień nienależących do dostawcy. Jeśli `EventLog` nie określono ustawień dziennika, domyślnie są one `LogLevel.Warning` .

Aby rejestrować zdarzenia mniejsze niż <xref:Microsoft.Extensions.Logging.LogLevel.Warning?displayProperty=nameWithType> , jawnie ustaw poziom dziennika. Poniższy przykład ustawia domyślny poziom dziennika dziennika zdarzeń <xref:Microsoft.Extensions.Logging.LogLevel.Information?displayProperty=nameWithType> :

```json
"Logging": {
  "EventLog": {
    "LogLevel": {
      "Default": "Information"
    }
  }
}
```

[Przeciążania addeventlog](xref:Microsoft.Extensions.Logging.EventLoggerFactoryExtensions) można przekazać <xref:Microsoft.Extensions.Logging.EventLog.EventLogSettings> . Jeśli `null` lub nie zostanie określony, są używane następujące ustawienia domyślne:

- `LogName`: "Aplikacja"
- `SourceName`: "Środowisko uruchomieniowe platformy .NET"
- `MachineName`: Nazwa komputera lokalnego jest używana.

Poniższy kod zmienia `SourceName` wartość domyślną na `".NET Runtime"` `CustomLogs` :

```csharp
public class Program
{
    static async Task Main(string[] args)
    {
        using IHost host = CreateHostBuilder(args).Build();

        // Application code should start here.

        await host.RunAsync();
    }

    static IHostBuilder CreateHostBuilder(string[] args) =>
        Host.CreateDefaultBuilder(args)
            .ConfigureLogging(logging =>
                logging.AddEventLog(configuration =>
                    configuration.SourceName = "CustomLogs"));
}
```

### <a name="azure-app-service"></a>Azure App Service

Pakiet [Microsoft. Extensions. Logging. AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices) Provider zapisuje dzienniki w plikach tekstowych w systemie plików aplikacji Azure App Service i w usłudze [BLOB Storage](/azure/storage/blobs/storage-quickstart-blobs-dotnet#what-is-blob-storage) na koncie usługi Azure Storage.

Pakiet dostawcy nie jest uwzględniony w bibliotekach środowiska uruchomieniowego. Aby użyć dostawcy, Dodaj pakiet dostawcy do projektu.

Aby skonfigurować ustawienia dostawcy, użyj <xref:Microsoft.Extensions.Logging.AzureAppServices.AzureFileLoggerOptions> i <xref:Microsoft.Extensions.Logging.AzureAppServices.AzureBlobLoggerOptions> , jak pokazano w następującym przykładzie:

```csharp
class Program
{
    static async Task Main(string[] args)
    {
        using IHost host = CreateHostBuilder(args).Build();

        // Application code should start here.

        await host.RunAsync();
    }

    static IHostBuilder CreateHostBuilder(string[] args) =>
        Host.CreateDefaultBuilder(args)
            .ConfigureLogging(logging =>
                logging.AddAzureWebAppDiagnostics())
            .ConfigureServices(services =>
                services.Configure<AzureFileLoggerOptions>(options =>
                {
                    options.FileName = "azure-diagnostics-";
                    options.FileSizeLimit = 50 _ 1024;
                    options.RetainedFileCountLimit = 5;
                })
                .Configure<AzureBlobLoggerOptions>(options =>
                {
                    options.BlobName = "log.txt";
                }));
}
```

Po wdrożeniu do Azure App Service aplikacja korzysta z ustawień w sekcji [dzienniki App Service](/azure/app-service/web-sites-enable-diagnostic-log/#enable-application-logging-windows) na stronie **App Service** Azure Portal. Po zaktualizowaniu następujących ustawień zmiany zaczynają obowiązywać natychmiast, bez konieczności ponownego uruchomienia lub ponownej wdrożenia aplikacji.

- **Rejestrowanie aplikacji (system plików)**
- **Rejestrowanie aplikacji (BLOB)**

Domyślną lokalizacją plików dziennika jest folder *D: \\ Home \\ \\ LogFiles* , a domyślna nazwa pliku to *diagnostics-yyyymmdd.txt*. Domyślny limit rozmiaru pliku wynosi 10 MB, a domyślna maksymalna liczba zachowywanych plików to 2. Domyślną nazwą obiektu BLOB jest *{App-Name} {timestamp}/yyyy/mm/dd/hh/{guid} -applicationLog.txt*.

Ten dostawca rejestruje się tylko wtedy, gdy projekt jest uruchomiony w środowisku platformy Azure.

#### <a name="azure-log-streaming"></a>Przesyłanie strumieniowe dzienników Azure

Przesyłanie strumieniowe w usłudze Azure log obsługuje wyświetlanie dziennika w czasie rzeczywistym z:

- Serwer aplikacji
- Serwer sieci Web
- Śledzenie nieudanych żądań

Aby skonfigurować przesyłanie strumieniowe dzienników Azure:

- Przejdź do strony **dzienników App Service** ze strony portalu aplikacji.
- Ustaw **Rejestrowanie aplikacji (system plików)** na **włączone**.
- Wybierz **poziom** dziennika. To ustawienie dotyczy tylko przesyłania strumieniowego dzienników Azure.

Przejdź do strony **strumień dziennika** , aby wyświetlić dzienniki. Zarejestrowane komunikaty są rejestrowane przy użyciu `ILogger` interfejsu.

### <a name="azure-application-insights"></a>Azure Application Insights

Pakiet [Microsoft. Extensions. Logging. ApplicationInsights](https://www.nuget.org/packages/Microsoft.Extensions.Logging.ApplicationInsights) Provider zapisuje dzienniki na [platformie Azure Application Insights](/azure/azure-monitor/app/cloudservices). Application Insights to usługa, która monitoruje aplikację internetową i udostępnia narzędzia do wykonywania zapytań i analizowania danych telemetrycznych. Jeśli używasz tego dostawcy, możesz wysyłać zapytania i analizować dzienniki przy użyciu narzędzi Application Insights.

Więcej informacji można znaleźć w następujących zasobach:

- [Omówienie usługi Application Insights](/azure/application-insights/app-insights-overview)
- [ApplicationInsightsLoggerProvider for .NET Core ILogger](/azure/azure-monitor/app/ilogger) — Rozpocznij tutaj, jeśli chcesz zaimplementować dostawcę rejestrowania bez pozostałej części telemetrii Application Insights.
- [Karty rejestrowania Application Insights](/azure/azure-monitor/app/asp-net-trace-logs).
- [Zainstaluj, skonfiguruj i zainicjuj samouczek Application INSIGHTS SDK](/learn/modules/instrument-web-app-code-with-application-insights) — interaktywny w witrynie Microsoft Learn.

## <a name="third-party-logging-providers"></a>Dostawcy rejestrowania innych firm

Oto kilka platform rejestrowania innych firm, które współpracują z różnymi obciążeniami platformy .NET:

- [ELMAH.IO](https://elmah.io) ([repozytorium GitHub](https://github.com/elmahio/Elmah.Io.Extensions.Logging))
- [Gelf](https://docs.graylog.org/en/2.3/pages/gelf.html) ([repozytorium GitHub](https://github.com/mattwcole/gelf-extensions-logging))
- [JSNLog](http://jsnlog.com) ([repozytorium GitHub](https://github.com/mperdeck/jsnlog))
- [KissLog.NET](https://kisslog.net) ([repozytorium GitHub](https://github.com/catalingavan/KissLog-net))
- [Log4Net](https://logging.apache.org/log4net) ([repozytorium GitHub](https://github.com/apache/logging-log4net))
- [Loggr](https://loggr.net) ([repozytorium GitHub](https://github.com/imobile3/Loggr.Extensions.Logging))
- [NLOG](https://nlog-project.org) ([repozytorium GitHub](https://github.com/NLog/NLog.Extensions.Logging))
- [Sentry](https://sentry.io/welcome) ([repozytorium GitHub](https://github.com/getsentry/sentry-dotnet))
- [Serilog](https://serilog.net) ([repozytorium GitHub](https://github.com/serilog/serilog-sinks-console))
- [Stackdriver](https://cloud.google.com/dotnet/docs/stackdriver#logging) ([repozytorium GitHub](https://github.com/googleapis/google-cloud-dotnet))

Niektóre struktury innych firm mogą wykonywać [Rejestrowanie semantyczne, znane także jako rejestrowanie strukturalne](https://softwareengineering.stackexchange.com/questions/312197/benefits-of-structured-logging-vs-basic-logging).

Korzystanie z struktury innej firmy jest podobne do korzystania z jednego z wbudowanych dostawców:

1. Dodaj pakiet NuGet do projektu.
1. Wywoływanie `ILoggerFactory` `ILoggingBuilder` metody rozszerzenia lub dostarczonej przez platformę rejestrowania.

Aby uzyskać więcej informacji, zobacz dokumentację każdego dostawcy. Dostawcy rejestrowania innych firm nie są obsługiwani przez firmę Microsoft.

## <a name="see-also"></a>Zobacz także

- [Rejestrowanie w programie .NET](logging.md).
- [Zaimplementuj niestandardowego dostawcę rejestrowania w programie .NET](custom-logging-provider.md).
- [Rejestrowanie o wysokiej wydajności w programie .NET](high-performance-logging.md).
