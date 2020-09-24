---
title: Zarządzanie wydajnością aplikacji — gRPC dla deweloperów WCF
description: Rejestrowanie, metryki i śledzenie dla ASP.NET Core aplikacji gRPC.
ms.date: 09/02/2019
ms.openlocfilehash: bccb5ba92e2dc8fa2def4dc192b0ca58b332861a
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91165913"
---
# <a name="application-performance-management"></a>Zarządzanie wydajnością aplikacji

W środowiskach produkcyjnych, takich jak Kubernetes, ważne jest monitorowanie aplikacji, aby upewnić się, że działają one optymalnie. Rejestrowanie i metryki są szczególnie ważne. ASP.NET Core, w tym gRPC, oferuje wbudowaną obsługę tworzenia komunikatów dziennika i danych metryk oraz zarządzania nimi, a także *śledzenia* danych.

## <a name="the-difference-between-logging-and-metrics"></a>Różnica między rejestrowaniem i metrykami

*Rejestrowanie* jest powiązane z wiadomościami tekstowymi, które rejestrują szczegółowe informacje o elementach, które wystąpiły w systemie. Komunikaty dziennika mogą zawierać dane wyjątku, takie jak ślady stosu lub dane strukturalne, które udostępniają kontekst dotyczące wiadomości. Dane wyjściowe rejestrowania są często zapisywane w magazynie tekstu do przeszukiwania.

*Metryki* odwołują się do danych liczbowych zaprojektowanych do agregowania i przedstawianych przy użyciu wykresów i wykresów na pulpicie nawigacyjnym. Pulpit nawigacyjny zawiera widok ogólnej kondycji i wydajności aplikacji. Dane metryk mogą być również używane do wyzwalania automatycznych alertów w przypadku przekroczenia progu. Poniżej przedstawiono kilka przykładów danych metryk:

- Czas przetwarzania żądań.
- Liczba żądań na sekundę obsługiwanych przez wystąpienie usługi.
- Liczba żądań zakończonych niepowodzeniem w wystąpieniu.

## <a name="logging-in-aspnet-core-grpc"></a>Logowanie w ASP.NET Core gRPC

ASP.NET Core zapewnia wbudowaną obsługę rejestrowania w postaci pakietu NuGet [Microsoft. Extensions. Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging) . Podstawowe części tej biblioteki są dołączone do zestawu SDK sieci Web, więc nie trzeba instalować go ręcznie. Domyślnie komunikaty dziennika są zapisywane w standardowym wyjściu (konsoli) i w dowolnym dołączonym debugerze. Aby pisać dzienniki do trwałych zewnętrznych magazynów danych, może zajść potrzeba zaimportowania [opcjonalnych pakietów ujścia rejestrowania](/aspnet/core/fundamentals/logging/?view=aspnetcore-3.0#third-party-logging-providers).

ASP.NET Core gRPC Framework zapisuje szczegółowe komunikaty rejestrowania diagnostycznego do tej struktury rejestrowania, dzięki czemu mogą być przetwarzane i przechowywane wraz z własnymi komunikatami aplikacji.

### <a name="produce-log-messages"></a>Generowanie komunikatów dziennika

Rozszerzenie rejestrowania jest automatycznie rejestrowane w systemie ASP.NET Core, aby można było określić rejestratory jako parametr konstruktora dla typów usługi gRPC.

```csharp
public class StockData : Stocks.StocksBase
{
    private readonly ILogger<StockData> _logger;

    public StockData(ILogger<StockData> logger)
    {
        _logger = logger;
    }
}
```

Wiele komunikatów dziennika, takich jak żądania i wyjątki, są dostarczane przez składniki ASP.NET Core i gRPC Framework. Dodaj własne wiadomości dziennika w celu zapewnienia szczegółowych informacji i kontekstu logiki aplikacji, a nie zagadnień niższego poziomu.

Aby uzyskać więcej informacji na temat pisania komunikatów dziennika i dostępnych ujść i elementów docelowych rejestrowania, zobacz  [Rejestrowanie w programie .NET Core i ASP.NET Core](/aspnet/core/fundamentals/logging/).

## <a name="metrics-in-aspnet-core-grpc"></a>Metryki w ASP.NET Core gRPC

Środowisko uruchomieniowe programu .NET Core udostępnia zestaw składników do emitowania i obserwowania metryk. Obejmują one interfejsy API, takie <xref:System.Diagnostics.Tracing.EventSource> jak <xref:System.Diagnostics.Tracing.EventCounter> klasy i. Te interfejsy API mogą emitować podstawowe dane liczbowe, które mogą być używane przez procesy zewnętrzne, takie jak [globalne narzędzie liczników dotnet](../../core/diagnostics/dotnet-counters.md)lub śledzenie zdarzeń dla systemu Windows. Aby uzyskać więcej informacji na temat używania `EventCounter` w własnym kodzie, zobacz [wprowadzenie do EventCounter](https://github.com/dotnet/runtime/blob/master/src/libraries/System.Diagnostics.Tracing/documentation/EventCounterTutorial.md).

W przypadku bardziej zaawansowanych metryk i zapisywania danych metryk w szerszym zakresie magazynów danych można spróbować utworzyć projekt typu "open source" o nazwie [metryki aplikacji](https://www.app-metrics.io). Ten pakiet bibliotek zawiera rozbudowany zestaw typów służący do Instrumentacji kodu. Oferuje również pakiety do zapisywania metryk do różnych rodzajów obiektów docelowych, które obejmują bazy danych szeregów czasowych, takich jak Prometheus i InfluxDB, oraz [Application Insights](/azure/azure-monitor/app/app-insights-overview). Pakiet NuGet [App. Metrics. AspNetCore. MVC](https://www.nuget.org/packages/App.Metrics.AspNetCore.Mvc/) dodatkowo dodaje kompleksowy zestaw podstawowych metryk, które są generowane automatycznie przez integrację z platformą ASP.NET Core. Witryna sieci Web projektu udostępnia [Szablony](https://www.app-metrics.io/samples/grafana/) do wyświetlania tych metryk przy użyciu platformy wizualizacji [Grafana](https://grafana.com/) .

### <a name="produce-metrics"></a>Tworzenie metryk

Większość platform metryk obsługuje następujące typy:

| Typ metryki | Opis |
| ----------- | ----------- |
| Licznik     | Śledzi, jak często coś się dzieje, takich jak żądania i błędy. |
| Miernik       | Rejestruje pojedynczą wartość, która zmienia się w czasie, na przykład aktywne połączenia. |
| Histogram   | Mierzy rozkład wartości w ramach dowolnych limitów. Na przykład histogram może śledzić rozmiar zestawu danych, zliczać informacje o liczbie zawartych <10 rekordów, liczbie zawartych 11-100 rekordów, liczbie zawartych 101-1000 rekordów i liczbie zawartych >1000 rekordów. |
| Miernik       | Mierzy szybkość, z jaką zdarzenie występuje w różnych przedziałach czasowych. |
| Czasomierz       | Śledzi czas trwania zdarzeń i szybkość ich występowania, przechowywane jako histogram. |

Korzystając z *metryk aplikacji*, `IMetrics` można uzyskać interfejs za pośrednictwem iniekcji zależności, który służy do rejestrowania dowolnej z tych metryk dla usługi gRPC. Poniższy przykład pokazuje, jak zliczyć liczbę `Get` żądań wykonanych w czasie:

```csharp
public class StockData : Stocks.StocksBase
{
    private static readonly CounterOptions GetRequestCounter = new CounterOptions
    {
        Name = "StockData_Get_Requests",
        MeasurementUnit = Unit.Calls
    };

    private readonly IStockRepository _repository;
    private readonly IMetrics _metrics;

    public StockData(IStockRepository repository, IMetrics metrics)
    {
        _repository = repository;
        _metrics = metrics;
    }

    public override async Task<GetResponse> Get(GetRequest request, ServerCallContext context)
    {
        _metrics.Measure.Counter.Increment(GetRequestCounter);

        // Serve request...
    }
}
```

### <a name="store-and-visualize-metrics-data"></a>Przechowywanie i Wizualizacja danych metryk

Najlepszym sposobem przechowywania danych metryk znajduje się w *bazie danych szeregów czasowych*, wyspecjalizowany magazyn danych przeznaczony do rejestrowania liczbowych serii danych oznaczonych sygnaturami czasowymi. Najpopularniejsze bazy danych to [Prometheus](https://prometheus.io/) i [InfluxDB](https://www.influxdata.com/products/influxdb-overview/). Microsoft Azure udostępnia również dedykowany magazyn metryk za pomocą usługi [Azure monitor](/azure/azure-monitor/overview) .

Obecne rozwiązanie do wizualizacji danych metryk to [Grafana](https://grafana.com), które współpracuje z szeroką gamę dostawców magazynu. Na poniższej ilustracji przedstawiono przykładowy pulpit nawigacyjny Grafana, w którym są wyświetlane metryki z sieci łączącej usługi z uruchomioną próbą StockData:

![Zrzut ekranu przedstawiający pulpit nawigacyjny Grafana](media/application-performance-management/grafana-screenshot.png)

### <a name="metrics-based-alerting"></a>Alerty oparte na metrykach

Liczbowy charakter danych metryk oznacza, że jest to idealne rozwiązanie w przypadku systemów ostrzegających o alertach, które są przeznaczone dla deweloperów lub inżynierów pomocy technicznej, gdy wartość wykracza poza pewną określoną tolerancję. Już wspomniane platformy zapewniają obsługę alertów za pośrednictwem różnych opcji, w tym wiadomości e-mail, wiadomości SMS lub wizualizacji w pulpicie nawigacyjnym.

## <a name="distributed-tracing"></a>Śledzenie rozproszone

Śledzenie rozproszone to stosunkowo niedawne programowanie w zakresie monitorowania, które powstało na podstawie zwiększenia użycia mikrousług i rozproszonych architektur. Pojedyncze żądanie z przeglądarki klienta, aplikacji lub urządzenia można podzielić na wiele kroków i żądań podrzędnych oraz korzystać z wielu usług w sieci. Utrudnia to skorelowanie komunikatów dziennika i metryk z konkretnym żądaniem, które je wywołało. Śledzenie rozproszone stosuje identyfikatory do żądań i umożliwia skorelowanie dzienników i metryk z określoną operacją. Jest to podobne do [kompleksowego śledzenia usługi WCF](../../framework/wcf/diagnostics/tracing/end-to-end-tracing.md), ale jest ono stosowane na wielu platformach.

Śledzenie rozproszone jest szybko uprawiane w popularności i zaczyna się od normalizacji. Natywna platforma obliczeniowa w chmurze stworzyła [model śledzenia Open](https://opentracing.io), próbując udostępnić niezależnym od dostawcy biblioteki do pracy z zapleczem, np. [Jaeger](https://www.jaegertracing.io/) i [elastyczny system APM](https://www.elastic.co/products/apm). W tym samym czasie, firma Google utworzyła [projekt OpenCensus](https://opencensus.io/) w celu rozwiązania tego samego zestawu problemów. Te dwa projekty są scalane do nowego projektu, [OpenTelemetry](https://opentelemetry.io), który ma być standardem branżowym w przyszłości.

### <a name="how-distributed-tracing-works"></a>Jak działa śledzenie rozproszone

Śledzenie rozproszone opiera się na koncepcji *zakresów*: nazwanych, czasochłonnych operacjach, które są częścią pojedynczego *śledzenia*, które mogą obejmować przetwarzanie na wielu węzłach systemu. Po zainicjowaniu nowej operacji jest tworzony ślad z unikatowym identyfikatorem. Dla każdej operacji podrzędnej zakres jest tworzony z własnym identyfikatorem i identyfikatorem śledzenia. Gdy żądanie przebiega w systemie, różne składniki mogą tworzyć zakresy *podrzędne* , które zawierają identyfikator ich *elementu nadrzędnego*. Zakres ma *kontekst*, który zawiera identyfikatory śledzenia i zakresu, a także przydatne dane w postaci par klucz-wartość (zwany *bagażem*).

### <a name="distributed-tracing-with-diagnosticsource"></a>Śledzenie rozproszone z `DiagnosticSource`

Platforma .NET Core ma wewnętrzny moduł, który jest dobrze mapowany do dystrybuowanych śladów i zakresów: [DiagnosticSource](https://github.com/dotnet/runtime/blob/master/src/libraries/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md#diagnosticsource-users-guide). A także zapewnić prostą metodę tworzenia i korzystania z diagnostyki w ramach procesu, `DiagnosticSource` moduł ma koncepcję *działania*. Działanie jest efektywnie implementacją rozproszonego śledzenia lub zakresu w śladzie. Elementy wewnętrzne modułu wykorzystują działania nadrzędne i podrzędne, w tym przydzielanie identyfikatorów. Aby uzyskać więcej informacji na temat korzystania z `Activity` typu, zobacz [Podręcznik użytkownika działania w witrynie GitHub](https://github.com/dotnet/runtime/blob/master/src/libraries/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md#activity-user-guide).

Ponieważ `DiagnosticSource` jest częścią podstawowego środowiska, jest obsługiwana przez kilka podstawowych składników. Obejmują one <xref:System.Net.Http.HttpClient> , Entity Framework Core i ASP.NET Core, w tym jawne wsparcie w strukturze gRPC. Gdy ASP.NET Core odbiera żądanie, sprawdza parę nagłówków HTTP zgodnych ze standardem [kontekstu śledzenia W3C](https://www.w3.org/TR/trace-context) . Jeśli nagłówki zostaną znalezione, działanie jest uruchamiane przy użyciu wartości tożsamości i kontekstu z nagłówków. Jeśli nie zostaną znalezione żadne nagłówki, działanie jest uruchamiane z wygenerowanymi wartościami tożsamości, które pasują do formatu standardowego. Wszystkie diagnostyki generowane przez platformę lub przez kod aplikacji w okresie istnienia tego działania mogą być otagowane przy użyciu identyfikatorów śledzenia i zakresu. `HttpClient`Pomoc techniczna rozszerza to dodatkowo, sprawdzając dostępność bieżącego działania na każdym żądaniu i automatycznie dodając nagłówki śledzenia do żądania wychodzącego.

Biblioteka gRPC klienta i serwera zawiera jawną pomoc techniczną dla `DiagnosticSource` i i `Activity` tworzy działania oraz automatycznie stosuje i wykorzystuje informacje nagłówka. ASP.NET Core

> [!NOTE]
> Wszystko to zdarza się tylko wtedy, gdy odbiornik zużywa informacje diagnostyczne. Jeśli nie ma odbiornika, Diagnostyka nie jest zapisywana i żadne działania nie są tworzone.

### <a name="add-your-own-diagnosticsource-and-activity"></a>Dodaj własne `DiagnosticSource` i `Activity`

Aby dodać własną diagnostykę lub utworzyć jawne zakresy w kodzie aplikacji, zobacz Podręcznik użytkownika programu [DiagnosticSource](https://github.com/dotnet/runtime/blob/master/src/libraries/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md#instrumenting-with-diagnosticsourcediagnosticlistener) i [Podręcznik użytkownika działania](https://github.com/dotnet/runtime/blob/master/src/libraries/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md#activity-usage).

### <a name="store-distributed-trace-data"></a>Przechowywanie danych śledzenia rozproszonego

W momencie pisania projekt OpenTelemetry jest nadal w wczesnych etapach i dostępne są tylko pakiety o wysokiej jakości dla aplikacji .NET. Projekt OpenTracing obecnie oferuje bardziej dojrzałe biblioteki.

Interfejs API OpenTracing został opisany w następnej sekcji. Jeśli zamiast tego chcesz użyć interfejsu API OpenTelemetry w aplikacji, zapoznaj się z [repozytorium zestawu SDK platformy .NET OpenTelemetry](https://github.com/open-telemetry/opentelemetry-dotnet) w witrynie GitHub.

#### <a name="use-the-opentracing-package-to-store-distributed-trace-data"></a>Przechowywanie danych śledzenia rozproszonego przy użyciu pakietu OpenTracing

[Pakiet NuGet OpenTracing](https://www.nuget.org/packages/OpenTracing/) obsługuje wszystkie zaplecza zgodne z OpenTracing (które mogą być używane niezależnie od systemu `DiagnosticSource` ). Istnieje dodatkowy pakiet z projektu OpenTracing API [OpenTracing. contrib. Core](https://www.nuget.org/packages/OpenTracing.Contrib.NetCore/). Ten pakiet dodaje `DiagnosticSource` odbiornik i zapisuje zdarzenia i działania do zaplecza automatycznie. Włączenie tego pakietu jest proste, ponieważ instalowanie go z narzędzia NuGet i dodawanie go jako usługi w `Startup` klasie.

```csharp
public class Startup
{
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddOpenTracing();
    }
}
```

Pakiet OpenTracing jest warstwą abstrakcji i dlatego wymaga implementacji specyficznej dla zaplecza. Implementacje interfejsu API OpenTracing są dostępne dla następujących zaplecza Open Source.

| Nazwa | Pakiet | Witryna internetowa |
| ---- | ------- | -------- |
| Jaeger | [Jaeger](https://www.nuget.org/packages/Jaeger/) | [jaegertracing.io](https://jaegertracing.io) |
| Elastyczny system APM | [Elastyczny. APM. NetCoreAll](https://www.nuget.org/packages/Elastic.Apm.NetCoreAll/) | [elastic.co/products/apm](https://www.elastic.co/products/apm) |

Aby uzyskać więcej informacji na temat interfejsu API OpenTracing dla platformy .NET, zobacz [OpenTracing for c#](https://github.com/opentracing/opentracing-csharp) i [OpenTracing contrib c#/.NET](https://github.com/opentracing-contrib/csharp-netcore) w serwisie GitHub.

>[!div class="step-by-step"]
>[Poprzedni](load-balancing.md) 
> [Dalej](appendix.md)
