---
title: Mierzenie wydajności za pomocą EventCounters w programie .NET Core
description: W tym samouczku dowiesz się, jak zmierzyć wydajność przy użyciu EventCounters.
ms.date: 08/07/2020
ms.topic: tutorial
ms.openlocfilehash: 75f6f1469c87eb1fe8a3064a815ec72943771f88
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96437457"
---
# <a name="tutorial-measure-performance-using-eventcounters-in-net-core"></a>Samouczek: pomiar wydajności przy użyciu EventCounters w programie .NET Core

**Ten artykuł ma zastosowanie do: ✔️** .net Core 3,0 SDK i nowszych wersjach

W tym samouczku dowiesz się, w jaki sposób <xref:System.Diagnostics.Tracing.EventCounter> można mierzyć wydajność przy użyciu dużej częstotliwości zdarzeń. Można użyć [dostępnych liczników](event-counters.md#available-counters) opublikowanych przez różne oficjalne pakiety .NET Core, dostawców zewnętrznych lub utworzyć własne metryki do monitorowania.

W tym samouczku wykonasz następujące czynności:

> [!div class="checklist"]
>
> - Zaimplementuj <xref:System.Diagnostics.Tracing.EventSource> .
> - Monitoruj liczniki przy użyciu programu [dotnet-Counters](dotnet-counters.md).

## <a name="prerequisites"></a>Wymagania wstępne

Samouczek używa:

- [.NET Core 3,1 SDK](https://dotnet.microsoft.com/download/dotnet-core) lub nowsza wersja.
- [dotnet-Counters](dotnet-counters.md) do monitorowania liczników zdarzeń.
- [Przykładowa](/samples/dotnet/samples/diagnostic-scenarios) aplikacja do debugowania do diagnozowania.

## <a name="get-the-source"></a>Pobierz Źródło

Przykładowa aplikacja zostanie użyta jako podstawa monitorowania. [Przykładowe repozytorium ASP.NET Core](/samples/dotnet/samples/diagnostic-scenarios) jest dostępne w przeglądarce przykładów. Pobierzesz plik zip, wyodrębnisz go po pobraniu i otworzysz go w ulubionym środowisku IDE. Skompiluj i uruchom aplikację, aby upewnić się, że działa prawidłowo, a następnie Zatrzymaj aplikację.

## <a name="implement-an-eventsource"></a>Implementowanie elementu EventSource

W przypadku zdarzeń, które są wykonywane co kilka milisekund, narzuty na zdarzenie będzie niskie (mniejsze niż milisekundy). W przeciwnym razie wpływ na wydajność będzie znaczący. Rejestrowanie zdarzenia oznacza, że zamierzasz napisać coś na dysku. Jeśli dysk nie jest wystarczająco szybki, utracisz zdarzenia. Potrzebne jest rozwiązanie inne niż rejestrowanie samego zdarzenia.

W przypadku dużej liczby zdarzeń znajomość miary na zdarzenie nie jest przydatna. Większość potrzebnych informacji to tylko niektóre z nich. Dzięki temu można uzyskać statystykę w ramach procesu, a następnie napisać wydarzenie raz w czasie, aby zgłosić dane statystyczne <xref:System.Diagnostics.Tracing.EventCounter> .

Poniżej przedstawiono przykład sposobu implementacji <xref:System.Diagnostics.Tracing.EventSource?displayProperty=fullName> . Utwórz nowy plik o nazwie *MinimalEventCounterSource.cs* i użyj fragmentu kodu jako źródła:

:::code language="csharp" source="snippets/EventCounters/MinimalEventCounterSource.cs":::

<xref:System.Diagnostics.Tracing.EventSource.WriteEvent%2A?displayProperty=nameWithType>Wiersz jest <xref:System.Diagnostics.Tracing.EventSource> częścią i nie jest częścią <xref:System.Diagnostics.Tracing.EventCounter> . został zapisany, aby pokazać, że można rejestrować komunikat razem z licznikiem zdarzeń.

## <a name="add-an-action-filter"></a>Dodawanie filtru akcji

Przykładowy kod źródłowy jest projektem ASP.NET Core. Można dodać [Filtr akcji](/aspnet/core/mvc/controllers/filters#action-filters) globalnie, który będzie rejestrował łączny czas żądania. Utwórz nowy plik o nazwie *LogRequestTimeFilterAttribute.cs* i użyj następującego kodu:

```csharp
using System.Diagnostics;
using Microsoft.AspNetCore.Http.Extensions;
using Microsoft.AspNetCore.Mvc.Filters;

namespace DiagnosticScenarios
{
    public class LogRequestTimeFilterAttribute : ActionFilterAttribute
    {
        readonly Stopwatch _stopwatch = new Stopwatch();

        public override void OnActionExecuting(ActionExecutingContext context) => _stopwatch.Start();

        public override void OnActionExecuted(ActionExecutedContext context)
        {
            _stopwatch.Stop();

            MinimalEventCounterSource.Log.Request(
                context.HttpContext.Request.GetDisplayUrl(), _stopwatch.ElapsedMilliseconds);
        }
    }
}
```

Filtr akcji rozpoczyna się od <xref:System.Diagnostics.Stopwatch> momentu rozpoczęcia żądania i kończy się po jego zakończeniu, przechwytując czas, który upłynął. Łączny czas w milisekundach jest rejestrowany w `MinimalEventCounterSource` pojedynczym wystąpieniu. Aby można było zastosować ten filtr, należy dodać go do kolekcji filtrów. W pliku *Startup.cs* zaktualizuj `ConfigureServices` metodę z uwzględnieniem tego filtru.

```csharp
public void ConfigureServices(IServiceCollection services) =>
    services.AddControllers(options => options.Filters.Add<LogRequestTimeFilterAttribute>())
            .AddNewtonsoftJson();
```

## <a name="monitor-event-counter"></a>Monitoruj licznik zdarzeń

Z implementacją na <xref:System.Diagnostics.Tracing.EventSource> i niestandardową akcję filtr Kompiluj i uruchamiaj aplikację.
Metryka została zarejestrowana w usłudze <xref:System.Diagnostics.Tracing.EventCounter> , ale jeśli nie masz dostępu do statystyk z tego elementu, nie jest ona przydatna. Aby uzyskać statystykę, należy włączyć tę funkcję, <xref:System.Diagnostics.Tracing.EventCounter> tworząc czasomierz, który jest uruchamiany tak często, jak zdarzenia, a także odbiornik do przechwytywania zdarzeń. W tym celu można użyć [liczników dotnet-Counters](dotnet-counters.md).

Użyj polecenia [dotnet-Counters PS](dotnet-counters.md#dotnet-counters-ps) , aby wyświetlić listę procesów platformy .NET, które mogą być monitorowane.

```console
dotnet-counters ps
```

Korzystając z identyfikatora procesu z danych wyjściowych `dotnet-counters ps` polecenia, można rozpocząć monitorowanie licznika zdarzeń za pomocą następującego `dotnet-counters monitor` polecenia:

```console
dotnet-counters monitor --process-id 2196 --counters Sample.EventCounter.Minimal,Microsoft.AspNetCore.Hosting[total-requests,requests-per-second],System.Runtime[cpu-usage]
```

Gdy `dotnet-counters monitor` polecenie jest uruchomione, przytrzymaj klawisz <kbd>F5</kbd> , aby rozpocząć generowanie żądań ciągłych do `https://localhost:5001/api/values` punktu końcowego. Po upływie kilku sekund Zatrzymaj, naciskając klawisz <kbd>q</kbd>

```console
Press p to pause, r to resume, q to quit.
    Status: Running

[Microsoft.AspNetCore.Hosting]
    Request Rate / 1 sec                               9
    Total Requests                                   134
[System.Runtime]
    CPU Usage (%)                                     13
[Sample.EventCounter.Minimal]
    Request Processing Time (ms)                      34.5
```

`dotnet-counters monitor`Polecenie jest doskonałe do aktywnego monitorowania. Można jednak zebrać te metryki diagnostyczne na potrzeby przetwarzania i analizy. W tym celu należy użyć `dotnet-counters collect` polecenia. `collect`Polecenie Switch jest podobne do `monitor` polecenia, ale akceptuje kilka dodatkowych parametrów. Można określić żądaną nazwę i format pliku wyjściowego. W przypadku pliku JSON o nazwie *diagnostics.jsprzy* użyciu następującego polecenia:

```console
dotnet-counters collect --process-id 2196 --format json -o diagnostics.json --counters Sample.EventCounter.Minimal,Microsoft.AspNetCore.Hosting[total-requests,requests-per-second],System.Runtime[cpu-usage]
```

Gdy polecenie jest uruchomione, przytrzymaj klawisz <kbd>F5</kbd> w przeglądarce, aby zacząć wystawiać ciągłe żądania do `https://localhost:5001/api/values` punktu końcowego. Po zakończeniu kilku sekund Zatrzymaj, naciskając klawisz <kbd>q</kbd>. *diagnostics.jsw* pliku jest zapisywana. Plik JSON, który jest pisany, nie jest jednak wcięty; Aby uzyskać czytelność, należy zrobić to w tym miejscu.

```json
{
  "TargetProcess": "DiagnosticScenarios",
  "StartTime": "8/5/2020 3:02:45 PM",
  "Events": [
    {
      "timestamp": "2020-08-05 15:02:47Z",
      "provider": "System.Runtime",
      "name": "CPU Usage (%)",
      "counterType": "Metric",
      "value": 0
    },
    {
      "timestamp": "2020-08-05 15:02:47Z",
      "provider": "Microsoft.AspNetCore.Hosting",
      "name": "Request Rate / 1 sec",
      "counterType": "Rate",
      "value": 0
    },
    {
      "timestamp": "2020-08-05 15:02:47Z",
      "provider": "Microsoft.AspNetCore.Hosting",
      "name": "Total Requests",
      "counterType": "Metric",
      "value": 134
    },
    {
      "timestamp": "2020-08-05 15:02:47Z",
      "provider": "Sample.EventCounter.Minimal",
      "name": "Request Processing Time (ms)",
      "counterType": "Metric",
      "value": 0
    },
    {
      "timestamp": "2020-08-05 15:02:47Z",
      "provider": "System.Runtime",
      "name": "CPU Usage (%)",
      "counterType": "Metric",
      "value": 0
    },
    {
      "timestamp": "2020-08-05 15:02:48Z",
      "provider": "Microsoft.AspNetCore.Hosting",
      "name": "Request Rate / 1 sec",
      "counterType": "Rate",
      "value": 0
    },
    {
      "timestamp": "2020-08-05 15:02:48Z",
      "provider": "Microsoft.AspNetCore.Hosting",
      "name": "Total Requests",
      "counterType": "Metric",
      "value": 134
    },
    {
      "timestamp": "2020-08-05 15:02:48Z",
      "provider": "Sample.EventCounter.Minimal",
      "name": "Request Processing Time (ms)",
      "counterType": "Metric",
      "value": 0
    },
    {
      "timestamp": "2020-08-05 15:02:48Z",
      "provider": "System.Runtime",
      "name": "CPU Usage (%)",
      "counterType": "Metric",
      "value": 0
    },
    {
      "timestamp": "2020-08-05 15:02:50Z",
      "provider": "Microsoft.AspNetCore.Hosting",
      "name": "Request Rate / 1 sec",
      "counterType": "Rate",
      "value": 0
    },
    {
      "timestamp": "2020-08-05 15:02:50Z",
      "provider": "Microsoft.AspNetCore.Hosting",
      "name": "Total Requests",
      "counterType": "Metric",
      "value": 134
    },
    {
      "timestamp": "2020-08-05 15:02:50Z",
      "provider": "Sample.EventCounter.Minimal",
      "name": "Request Processing Time (ms)",
      "counterType": "Metric",
      "value": 0
    }
  ]
}
```

## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [EventCounters](event-counters.md)
