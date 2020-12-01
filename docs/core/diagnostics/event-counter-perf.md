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
# <a name="tutorial-measure-performance-using-eventcounters-in-net-core"></a><span data-ttu-id="8f9e8-103">Samouczek: pomiar wydajności przy użyciu EventCounters w programie .NET Core</span><span class="sxs-lookup"><span data-stu-id="8f9e8-103">Tutorial: Measure performance using EventCounters in .NET Core</span></span>

<span data-ttu-id="8f9e8-104">**Ten artykuł ma zastosowanie do: ✔️** .net Core 3,0 SDK i nowszych wersjach</span><span class="sxs-lookup"><span data-stu-id="8f9e8-104">**This article applies to: ✔️** .NET Core 3.0 SDK and later versions</span></span>

<span data-ttu-id="8f9e8-105">W tym samouczku dowiesz się, w jaki sposób <xref:System.Diagnostics.Tracing.EventCounter> można mierzyć wydajność przy użyciu dużej częstotliwości zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="8f9e8-105">In this tutorial, you'll learn how an <xref:System.Diagnostics.Tracing.EventCounter> can be used to measure performance with a high frequency of events.</span></span> <span data-ttu-id="8f9e8-106">Można użyć [dostępnych liczników](event-counters.md#available-counters) opublikowanych przez różne oficjalne pakiety .NET Core, dostawców zewnętrznych lub utworzyć własne metryki do monitorowania.</span><span class="sxs-lookup"><span data-stu-id="8f9e8-106">You can use the [available counters](event-counters.md#available-counters) published by various official .NET Core packages, third-party providers, or create your own metrics for monitoring.</span></span>

<span data-ttu-id="8f9e8-107">W tym samouczku wykonasz następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="8f9e8-107">In this tutorial, you will:</span></span>

> [!div class="checklist"]
>
> - <span data-ttu-id="8f9e8-108">Zaimplementuj <xref:System.Diagnostics.Tracing.EventSource> .</span><span class="sxs-lookup"><span data-stu-id="8f9e8-108">Implement an <xref:System.Diagnostics.Tracing.EventSource>.</span></span>
> - <span data-ttu-id="8f9e8-109">Monitoruj liczniki przy użyciu programu [dotnet-Counters](dotnet-counters.md).</span><span class="sxs-lookup"><span data-stu-id="8f9e8-109">Monitor counters with [dotnet-counters](dotnet-counters.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f9e8-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8f9e8-110">Prerequisites</span></span>

<span data-ttu-id="8f9e8-111">Samouczek używa:</span><span class="sxs-lookup"><span data-stu-id="8f9e8-111">The tutorial uses:</span></span>

- <span data-ttu-id="8f9e8-112">[.NET Core 3,1 SDK](https://dotnet.microsoft.com/download/dotnet-core) lub nowsza wersja.</span><span class="sxs-lookup"><span data-stu-id="8f9e8-112">[.NET Core 3.1 SDK](https://dotnet.microsoft.com/download/dotnet-core) or a later version.</span></span>
- <span data-ttu-id="8f9e8-113">[dotnet-Counters](dotnet-counters.md) do monitorowania liczników zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="8f9e8-113">[dotnet-counters](dotnet-counters.md) to monitor event counters.</span></span>
- <span data-ttu-id="8f9e8-114">[Przykładowa](/samples/dotnet/samples/diagnostic-scenarios) aplikacja do debugowania do diagnozowania.</span><span class="sxs-lookup"><span data-stu-id="8f9e8-114">A [sample debug target](/samples/dotnet/samples/diagnostic-scenarios) app to diagnose.</span></span>

## <a name="get-the-source"></a><span data-ttu-id="8f9e8-115">Pobierz Źródło</span><span class="sxs-lookup"><span data-stu-id="8f9e8-115">Get the source</span></span>

<span data-ttu-id="8f9e8-116">Przykładowa aplikacja zostanie użyta jako podstawa monitorowania.</span><span class="sxs-lookup"><span data-stu-id="8f9e8-116">The sample application will be used as a basis for monitoring.</span></span> <span data-ttu-id="8f9e8-117">[Przykładowe repozytorium ASP.NET Core](/samples/dotnet/samples/diagnostic-scenarios) jest dostępne w przeglądarce przykładów.</span><span class="sxs-lookup"><span data-stu-id="8f9e8-117">The [sample ASP.NET Core repository](/samples/dotnet/samples/diagnostic-scenarios) is available from the samples browser.</span></span> <span data-ttu-id="8f9e8-118">Pobierzesz plik zip, wyodrębnisz go po pobraniu i otworzysz go w ulubionym środowisku IDE.</span><span class="sxs-lookup"><span data-stu-id="8f9e8-118">You download the zip file, extract it once downloaded, and open it in your favorite IDE.</span></span> <span data-ttu-id="8f9e8-119">Skompiluj i uruchom aplikację, aby upewnić się, że działa prawidłowo, a następnie Zatrzymaj aplikację.</span><span class="sxs-lookup"><span data-stu-id="8f9e8-119">Build and run the application to ensure that it works properly, then stop the application.</span></span>

## <a name="implement-an-eventsource"></a><span data-ttu-id="8f9e8-120">Implementowanie elementu EventSource</span><span class="sxs-lookup"><span data-stu-id="8f9e8-120">Implement an EventSource</span></span>

<span data-ttu-id="8f9e8-121">W przypadku zdarzeń, które są wykonywane co kilka milisekund, narzuty na zdarzenie będzie niskie (mniejsze niż milisekundy).</span><span class="sxs-lookup"><span data-stu-id="8f9e8-121">For events that happen every few milliseconds, you'll want the overhead per event to be low (less than a millisecond).</span></span> <span data-ttu-id="8f9e8-122">W przeciwnym razie wpływ na wydajność będzie znaczący.</span><span class="sxs-lookup"><span data-stu-id="8f9e8-122">Otherwise, the impact on performance will be significant.</span></span> <span data-ttu-id="8f9e8-123">Rejestrowanie zdarzenia oznacza, że zamierzasz napisać coś na dysku.</span><span class="sxs-lookup"><span data-stu-id="8f9e8-123">Logging an event means you're going to write something to disk.</span></span> <span data-ttu-id="8f9e8-124">Jeśli dysk nie jest wystarczająco szybki, utracisz zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="8f9e8-124">If the disk is not fast enough, you will lose events.</span></span> <span data-ttu-id="8f9e8-125">Potrzebne jest rozwiązanie inne niż rejestrowanie samego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="8f9e8-125">You need a solution other than logging the event itself.</span></span>

<span data-ttu-id="8f9e8-126">W przypadku dużej liczby zdarzeń znajomość miary na zdarzenie nie jest przydatna.</span><span class="sxs-lookup"><span data-stu-id="8f9e8-126">When dealing with a large number of events, knowing the measure per event is not useful either.</span></span> <span data-ttu-id="8f9e8-127">Większość potrzebnych informacji to tylko niektóre z nich.</span><span class="sxs-lookup"><span data-stu-id="8f9e8-127">Most of the time all you need is just some statistics out of it.</span></span> <span data-ttu-id="8f9e8-128">Dzięki temu można uzyskać statystykę w ramach procesu, a następnie napisać wydarzenie raz w czasie, aby zgłosić dane statystyczne <xref:System.Diagnostics.Tracing.EventCounter> .</span><span class="sxs-lookup"><span data-stu-id="8f9e8-128">So you could get the statistics within the process itself and then write an event once in a while to report the statistics, that's what <xref:System.Diagnostics.Tracing.EventCounter> will do.</span></span>

<span data-ttu-id="8f9e8-129">Poniżej przedstawiono przykład sposobu implementacji <xref:System.Diagnostics.Tracing.EventSource?displayProperty=fullName> .</span><span class="sxs-lookup"><span data-stu-id="8f9e8-129">Below is an example of how to implement an <xref:System.Diagnostics.Tracing.EventSource?displayProperty=fullName>.</span></span> <span data-ttu-id="8f9e8-130">Utwórz nowy plik o nazwie *MinimalEventCounterSource.cs* i użyj fragmentu kodu jako źródła:</span><span class="sxs-lookup"><span data-stu-id="8f9e8-130">Create a new file named *MinimalEventCounterSource.cs* and use the code snippet as its source:</span></span>

:::code language="csharp" source="snippets/EventCounters/MinimalEventCounterSource.cs":::

<span data-ttu-id="8f9e8-131"><xref:System.Diagnostics.Tracing.EventSource.WriteEvent%2A?displayProperty=nameWithType>Wiersz jest <xref:System.Diagnostics.Tracing.EventSource> częścią i nie jest częścią <xref:System.Diagnostics.Tracing.EventCounter> . został zapisany, aby pokazać, że można rejestrować komunikat razem z licznikiem zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="8f9e8-131">The <xref:System.Diagnostics.Tracing.EventSource.WriteEvent%2A?displayProperty=nameWithType> line is the <xref:System.Diagnostics.Tracing.EventSource> part and is not part of <xref:System.Diagnostics.Tracing.EventCounter>, it was written to show that you can log a message together with the event counter.</span></span>

## <a name="add-an-action-filter"></a><span data-ttu-id="8f9e8-132">Dodawanie filtru akcji</span><span class="sxs-lookup"><span data-stu-id="8f9e8-132">Add an action filter</span></span>

<span data-ttu-id="8f9e8-133">Przykładowy kod źródłowy jest projektem ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="8f9e8-133">The sample source code is an ASP.NET Core project.</span></span> <span data-ttu-id="8f9e8-134">Można dodać [Filtr akcji](/aspnet/core/mvc/controllers/filters#action-filters) globalnie, który będzie rejestrował łączny czas żądania.</span><span class="sxs-lookup"><span data-stu-id="8f9e8-134">You can add an [action filter](/aspnet/core/mvc/controllers/filters#action-filters) globally that will log the total request time.</span></span> <span data-ttu-id="8f9e8-135">Utwórz nowy plik o nazwie *LogRequestTimeFilterAttribute.cs* i użyj następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="8f9e8-135">Create a new file named *LogRequestTimeFilterAttribute.cs*, and use the following code:</span></span>

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

<span data-ttu-id="8f9e8-136">Filtr akcji rozpoczyna się od <xref:System.Diagnostics.Stopwatch> momentu rozpoczęcia żądania i kończy się po jego zakończeniu, przechwytując czas, który upłynął.</span><span class="sxs-lookup"><span data-stu-id="8f9e8-136">The action filter starts a <xref:System.Diagnostics.Stopwatch> as the request begins, and stops after it has completed, capturing the elapsed time.</span></span> <span data-ttu-id="8f9e8-137">Łączny czas w milisekundach jest rejestrowany w `MinimalEventCounterSource` pojedynczym wystąpieniu.</span><span class="sxs-lookup"><span data-stu-id="8f9e8-137">The total milliseconds is logged to the `MinimalEventCounterSource` singleton instance.</span></span> <span data-ttu-id="8f9e8-138">Aby można było zastosować ten filtr, należy dodać go do kolekcji filtrów.</span><span class="sxs-lookup"><span data-stu-id="8f9e8-138">In order for this filter to be applied, you need to add it to the filters collection.</span></span> <span data-ttu-id="8f9e8-139">W pliku *Startup.cs* zaktualizuj `ConfigureServices` metodę z uwzględnieniem tego filtru.</span><span class="sxs-lookup"><span data-stu-id="8f9e8-139">In the *Startup.cs* file, update the `ConfigureServices` method in include this filter.</span></span>

```csharp
public void ConfigureServices(IServiceCollection services) =>
    services.AddControllers(options => options.Filters.Add<LogRequestTimeFilterAttribute>())
            .AddNewtonsoftJson();
```

## <a name="monitor-event-counter"></a><span data-ttu-id="8f9e8-140">Monitoruj licznik zdarzeń</span><span class="sxs-lookup"><span data-stu-id="8f9e8-140">Monitor event counter</span></span>

<span data-ttu-id="8f9e8-141">Z implementacją na <xref:System.Diagnostics.Tracing.EventSource> i niestandardową akcję filtr Kompiluj i uruchamiaj aplikację.</span><span class="sxs-lookup"><span data-stu-id="8f9e8-141">With the implementation on an <xref:System.Diagnostics.Tracing.EventSource> and the custom action filter, build and launch the application.</span></span>
<span data-ttu-id="8f9e8-142">Metryka została zarejestrowana w usłudze <xref:System.Diagnostics.Tracing.EventCounter> , ale jeśli nie masz dostępu do statystyk z tego elementu, nie jest ona przydatna.</span><span class="sxs-lookup"><span data-stu-id="8f9e8-142">You logged the metric to the <xref:System.Diagnostics.Tracing.EventCounter>, but unless you access the statistics from of it, it is not useful.</span></span> <span data-ttu-id="8f9e8-143">Aby uzyskać statystykę, należy włączyć tę funkcję, <xref:System.Diagnostics.Tracing.EventCounter> tworząc czasomierz, który jest uruchamiany tak często, jak zdarzenia, a także odbiornik do przechwytywania zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="8f9e8-143">To get the statistics, you need to enable the <xref:System.Diagnostics.Tracing.EventCounter> by creating a timer that fires as frequently as you want the events, as well as a listener to capture the events.</span></span> <span data-ttu-id="8f9e8-144">W tym celu można użyć [liczników dotnet-Counters](dotnet-counters.md).</span><span class="sxs-lookup"><span data-stu-id="8f9e8-144">To do that, you can use [dotnet-counters](dotnet-counters.md).</span></span>

<span data-ttu-id="8f9e8-145">Użyj polecenia [dotnet-Counters PS](dotnet-counters.md#dotnet-counters-ps) , aby wyświetlić listę procesów platformy .NET, które mogą być monitorowane.</span><span class="sxs-lookup"><span data-stu-id="8f9e8-145">Use the [dotnet-counters ps](dotnet-counters.md#dotnet-counters-ps) command to display a list of .NET processes that can be monitored.</span></span>

```console
dotnet-counters ps
```

<span data-ttu-id="8f9e8-146">Korzystając z identyfikatora procesu z danych wyjściowych `dotnet-counters ps` polecenia, można rozpocząć monitorowanie licznika zdarzeń za pomocą następującego `dotnet-counters monitor` polecenia:</span><span class="sxs-lookup"><span data-stu-id="8f9e8-146">Using the process identifier from the output of the `dotnet-counters ps` command, you can start monitoring the event counter with the following `dotnet-counters monitor` command:</span></span>

```console
dotnet-counters monitor --process-id 2196 --counters Sample.EventCounter.Minimal,Microsoft.AspNetCore.Hosting[total-requests,requests-per-second],System.Runtime[cpu-usage]
```

<span data-ttu-id="8f9e8-147">Gdy `dotnet-counters monitor` polecenie jest uruchomione, przytrzymaj klawisz <kbd>F5</kbd> , aby rozpocząć generowanie żądań ciągłych do `https://localhost:5001/api/values` punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="8f9e8-147">While the `dotnet-counters monitor` command is running, hold <kbd>F5</kbd> on the browser to start issuing continuous requests to the `https://localhost:5001/api/values` endpoint.</span></span> <span data-ttu-id="8f9e8-148">Po upływie kilku sekund Zatrzymaj, naciskając klawisz <kbd>q</kbd></span><span class="sxs-lookup"><span data-stu-id="8f9e8-148">After a few seconds stop by pressing <kbd>q</kbd></span></span>

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

<span data-ttu-id="8f9e8-149">`dotnet-counters monitor`Polecenie jest doskonałe do aktywnego monitorowania.</span><span class="sxs-lookup"><span data-stu-id="8f9e8-149">The `dotnet-counters monitor` command is great for active monitoring.</span></span> <span data-ttu-id="8f9e8-150">Można jednak zebrać te metryki diagnostyczne na potrzeby przetwarzania i analizy.</span><span class="sxs-lookup"><span data-stu-id="8f9e8-150">However, you may want to collect these diagnostic metrics for post processing and analysis.</span></span> <span data-ttu-id="8f9e8-151">W tym celu należy użyć `dotnet-counters collect` polecenia.</span><span class="sxs-lookup"><span data-stu-id="8f9e8-151">For that, use the `dotnet-counters collect` command.</span></span> <span data-ttu-id="8f9e8-152">`collect`Polecenie Switch jest podobne do `monitor` polecenia, ale akceptuje kilka dodatkowych parametrów.</span><span class="sxs-lookup"><span data-stu-id="8f9e8-152">The `collect` switch command is similar to the `monitor` command, but accepts a few additional parameters.</span></span> <span data-ttu-id="8f9e8-153">Można określić żądaną nazwę i format pliku wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="8f9e8-153">You can specify the desired output file name and format.</span></span> <span data-ttu-id="8f9e8-154">W przypadku pliku JSON o nazwie *diagnostics.jsprzy* użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="8f9e8-154">For a JSON file named *diagnostics.json* use the following command:</span></span>

```console
dotnet-counters collect --process-id 2196 --format json -o diagnostics.json --counters Sample.EventCounter.Minimal,Microsoft.AspNetCore.Hosting[total-requests,requests-per-second],System.Runtime[cpu-usage]
```

<span data-ttu-id="8f9e8-155">Gdy polecenie jest uruchomione, przytrzymaj klawisz <kbd>F5</kbd> w przeglądarce, aby zacząć wystawiać ciągłe żądania do `https://localhost:5001/api/values` punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="8f9e8-155">Again, while the command is running, hold <kbd>F5</kbd> on the browser to start issuing continuous requests to the `https://localhost:5001/api/values` endpoint.</span></span> <span data-ttu-id="8f9e8-156">Po zakończeniu kilku sekund Zatrzymaj, naciskając klawisz <kbd>q</kbd>.</span><span class="sxs-lookup"><span data-stu-id="8f9e8-156">After a few seconds stop by pressing <kbd>q</kbd>.</span></span> <span data-ttu-id="8f9e8-157">*diagnostics.jsw* pliku jest zapisywana.</span><span class="sxs-lookup"><span data-stu-id="8f9e8-157">The *diagnostics.json* file is written.</span></span> <span data-ttu-id="8f9e8-158">Plik JSON, który jest pisany, nie jest jednak wcięty; Aby uzyskać czytelność, należy zrobić to w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="8f9e8-158">The JSON file that is written is not indented, however; for readability it is indented here.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8f9e8-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8f9e8-159">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8f9e8-160">EventCounters</span><span class="sxs-lookup"><span data-stu-id="8f9e8-160">EventCounters</span></span>](event-counters.md)
