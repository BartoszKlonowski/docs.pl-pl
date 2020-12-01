---
title: EventCounters na platformie .NET Core
description: W tym artykule dowiesz się, co EventCounters, jak je wdrożyć i jak je wykorzystać.
ms.date: 08/07/2020
ms.openlocfilehash: 68c831713eed8c49d24ebf93da301ef68d213bf9
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96437814"
---
# <a name="eventcounters-in-net-core"></a>EventCounters na platformie .NET Core

**Ten artykuł ma zastosowanie do: ✔️** .net Core 3,0 SDK i nowszych wersjach

EventCounters to interfejsy API platformy .NET Core używane dla lekkiej, międzyplatformowej i niemal w czasie rzeczywistym zbierania metryk wydajności. EventCounters zostały dodane jako alternatywa dla wielu platform dla "liczników wydajności" .NET Framework w systemie Windows. W tym artykule dowiesz się, co EventCounters, jak je wdrożyć i jak je wykorzystać.

Środowisko uruchomieniowe platformy .NET Core i kilka bibliotek .NET publikują podstawowe informacje diagnostyczne przy użyciu EventCounters, począwszy od platformy .NET Core 3,0. Oprócz EventCounters, które są dostarczane przez środowisko uruchomieniowe platformy .NET, można zaimplementować swój własny EventCounters. EventCounters może służyć do śledzenia różnych metryk.

EventCounters na żywo jako część <xref:System.Diagnostics.Tracing.EventSource> i są automatycznie wypychane do narzędzi odbiornika. Podobnie jak w przypadku wszystkich innych zdarzeń w <xref:System.Diagnostics.Tracing.EventSource> , mogą one być używane zarówno w procesie, jak i na zewnątrz w procesie za pośrednictwem <xref:System.Diagnostics.Tracing.EventListener> i [EventPipe](./eventpipe.md). Ten artykuł koncentruje się na funkcjach EventCounters i celowo wyklucza narzędzia PerfView i funkcję ETW (śledzenie zdarzeń dla systemu Windows), chociaż oba mogą być używane z EventCounters.

![Obraz przedstawiający diagram w procesie EventCounters i out-of-proc](media/event-counters.svg)

[!INCLUDE [available-counters](includes/available-counters.md)]

## <a name="eventcounter-api-overview"></a>Przegląd interfejsu API EventCounter

Istnieją dwie podstawowe kategorie liczników. Niektóre liczniki są przeznaczone do wartości "rate", takich jak łączna liczba wyjątków, Łączna liczba operacje odzyskiwania pamięci i łączna liczba żądań. Inne liczniki to wartości "snapshot", takie jak użycie sterty, użycie procesora CPU i rozmiar zestawu roboczego. W ramach każdej z tych kategorii liczników istnieją dwa typy liczników, które różnią się w zależności od ich wartości. Liczniki sondowania pobierają ich wartości za pośrednictwem wywołania zwrotnego, a liczniki bez sondowania mają swoje wartości bezpośrednio ustawione w wystąpieniu licznika.

Liczniki są reprezentowane przez następujące implementacje:

* <xref:System.Diagnostics.Tracing.EventCounter>
* <xref:System.Diagnostics.Tracing.IncrementingEventCounter>
* <xref:System.Diagnostics.Tracing.IncrementingPollingCounter>
* <xref:System.Diagnostics.Tracing.PollingCounter>

Odbiornik zdarzeń określa, jak długo są interwały pomiaru. Na końcu każdego interwału wartość jest przekazywana do odbiornika dla każdego licznika. Implementacje licznika określają, jakie interfejsy API i obliczenia są używane do tworzenia wartości każdego interwału.

1. <xref:System.Diagnostics.Tracing.EventCounter>Rejestruje zbiór wartości. <xref:System.Diagnostics.Tracing.EventCounter.WriteMetric%2A?displayProperty=nameWithType>Metoda dodaje nową wartość do zestawu. Dla każdego interwału obliczane jest podsumowanie statystyczne dla zestawu, takie jak min, Max i średnia. W narzędziu [dotnet-Counters](dotnet-counters.md) zawsze będzie wyświetlana wartość średnia. <xref:System.Diagnostics.Tracing.EventCounter>Jest to przydatne do opisywania dyskretnego zestawu operacji. Typowym użyciem może być monitorowanie średniego rozmiaru w bajtach ostatnich operacji we/wy lub średniej wartości pieniężnej zestawu transakcji finansowych.

1. <xref:System.Diagnostics.Tracing.IncrementingEventCounter>Rejestruje sumę całkowitą dla każdego przedziału czasu. <xref:System.Diagnostics.Tracing.IncrementingEventCounter.Increment%2A?displayProperty=nameWithType>Metoda dodaje do sumy. Na przykład, jeśli `Increment()` jest wywoływana trzy razy w jednym interwale z wartościami `1` , `2` , i `5` , wówczas suma uruchomiona wartości `8` będzie raportowana jako wartość licznika dla tego interwału. W narzędziu [dotnet-Counters](dotnet-counters.md) zostanie wyświetlona stawka jako nagrana suma/czas. <xref:System.Diagnostics.Tracing.IncrementingEventCounter>Jest to przydatne do mierzenia, jak często występuje akcja, na przykład liczby żądań przetwarzanych na sekundę.

1. <xref:System.Diagnostics.Tracing.PollingCounter>Używa wywołania zwrotnego do określenia wartości, która jest raportowana. Za każdym razem, gdy jest wywoływana funkcja wywołania zwrotnego użytkownika, a zwracana wartość jest używana jako wartość licznika. <xref:System.Diagnostics.Tracing.PollingCounter>Program może służyć do wykonywania zapytań dotyczących metryki z zewnętrznego źródła, na przykład przy pobieraniu bieżących bajtów wolnego miejsca na dysku. Może on również służyć do raportowania niestandardowych statystyk, które mogą być obliczane na żądanie przez aplikację. Przykłady obejmują raportowanie używany 95. percentylu ostatnich opóźnień żądań lub bieżącego współczynnika trafień lub chybień pamięci podręcznej.

1. <xref:System.Diagnostics.Tracing.IncrementingPollingCounter>Używa wywołania zwrotnego, aby określić raportowaną wartość przyrostu. Za każdym razem interwał wywołania zwrotnego jest wywoływany, a następnie różnica między bieżącym wywołaniem a ostatnim wywołaniem jest raportowaną wartością. W narzędziu [dotnet-Counters](dotnet-counters.md) zawsze będzie wyświetlana różnica w postaci stawki, zgłoszonej wartości/godziny. Ten licznik jest przydatny, gdy nie jest możliwe wywołanie interfejsu API dla każdego wystąpienia, ale możliwe jest zbadanie łącznej liczby wystąpień. Można na przykład zgłosić liczbę bajtów zapisanych do pliku na sekundę, nawet bez powiadomienia za każdym razem, gdy zostanie zapisany bajt.

## <a name="implement-an-eventsource"></a>Implementowanie elementu EventSource

Poniższy kod implementuje przykład <xref:System.Diagnostics.Tracing.EventSource> uwidoczniony jako nazwany `"Sample.EventCounter.Minimal"` dostawca. To źródło zawiera <xref:System.Diagnostics.Tracing.EventCounter> czas przetwarzania żądania. Taki licznik ma nazwę (czyli jego unikatowy identyfikator w źródle) i nazwę wyświetlaną używaną przez narzędzia odbiornika, takie jak [dotnet-Counter](dotnet-counters.md).

:::code language="csharp" source="snippets/EventCounters/MinimalEventCounterSource.cs":::

Służy `dotnet-counters ps` do wyświetlania listy procesów platformy .NET, które mogą być monitorowane:

```console
dotnet-counters ps
   1398652 dotnet     C:\Program Files\dotnet\dotnet.exe
   1399072 dotnet     C:\Program Files\dotnet\dotnet.exe
   1399112 dotnet     C:\Program Files\dotnet\dotnet.exe
   1401880 dotnet     C:\Program Files\dotnet\dotnet.exe
   1400180 sample-counters C:\sample-counters\bin\Debug\netcoreapp3.1\sample-counters.exe
```

Przekaż <xref:System.Diagnostics.Tracing.EventSource> nazwę do `--counters` opcji rozpoczęcia monitorowania licznika:

```console
dotnet-counters monitor --process-id 1400180 --counters Sample.EventCounter.Minimal
```

Poniższy przykład przedstawia dane wyjściowe monitora:

```console
Press p to pause, r to resume, q to quit.
    Status: Running

[Samples-EventCounterDemos-Minimal]
    Request Processing Time (ms)                            0.445
```

Naciśnij pozycję <kbd>q</kbd> , aby zatrzymać polecenie monitorowania.

#### <a name="conditional-counters"></a>Liczniki warunkowe

Podczas wdrażania klasy <xref:System.Diagnostics.Tracing.EventSource> zawierającej liczniki można warunkowo utworzyć wystąpienie, gdy <xref:System.Diagnostics.Tracing.EventSource.OnEventCommand%2A?displayProperty=nameWithType> Metoda jest wywoływana z <xref:System.Diagnostics.Tracing.EventCommandEventArgs.Command> wartością `EventCommand.Enable` . Aby bezpiecznie utworzyć wystąpienie wystąpienia licznika tylko wtedy, gdy jest to możliwe `null` , użyj [operatora przypisania łączenia z wartością null](../../csharp/language-reference/operators/null-coalescing-operator.md). Ponadto metody niestandardowe mogą oszacować metodę, <xref:System.Diagnostics.DiagnosticSource.IsEnabled%2A> Aby określić, czy bieżące źródło zdarzeń jest włączone.

:::code language="csharp" source="snippets/EventCounters/ConditionalEventCounterSource.cs":::

> [!TIP]
> Liczniki warunkowe są licznikami, które są warunkowo tworzone, a mikro Optymalizacja. Środowisko uruchomieniowe przyjmuje ten wzorzec dla scenariuszy, w których liczniki nie są zwykle używane, aby zaoszczędzić część milisekundy.

### <a name="net-core-runtime-example-counters"></a>Przykładowe liczniki środowiska uruchomieniowego platformy .NET Core

Środowisko uruchomieniowe platformy .NET Core zawiera wiele doskonałych przykładowych implementacji. Oto implementacja środowiska uruchomieniowego dla licznika, który śledzi rozmiar zestawu roboczego aplikacji.

```csharp
var workingSetCounter = new PollingCounter(
    "working-set",
    this,
    () => (double)(Environment.WorkingSet / 1_000_000))
{
    DisplayName = "Working Set",
    DisplayUnits = "MB"
};
```

<xref:System.Diagnostics.Tracing.PollingCounter>Raport przedstawia bieżącą ilość pamięci fizycznej zamapowanej na proces (zestaw roboczy) aplikacji, ponieważ w momencie przechwytuje ona metrykę. Wywołanie zwrotne do sondowania wartości jest podanym wyrażeniem lambda, które jest tylko wywołaniem <xref:System.Environment.WorkingSet?displayProperty=fullName> interfejsu API. <xref:System.Diagnostics.Tracing.DiagnosticCounter.DisplayName> i <xref:System.Diagnostics.Tracing.DiagnosticCounter.DisplayUnits> są opcjonalnymi właściwościami, które można ustawić, aby ułatwić konsumentowi licznika Wyświetlanie wartości dokładniej. Na przykład, program [dotnet-Counters](dotnet-counters.md) używa tych właściwości do wyświetlania większej przyjaznej dla wyświetlania wersji nazw liczników.

> [!IMPORTANT]
> `DisplayName`Właściwości nie są zlokalizowane.

W przypadku <xref:System.Diagnostics.Tracing.PollingCounter> <xref:System.Diagnostics.Tracing.IncrementingPollingCounter> elementów i nic nie trzeba wykonywać żadnych innych czynności. Oba te wartości są sondowane w przedziale czasowym żądanym przez klienta.

Oto przykład licznika czasu wykonywania zaimplementowanego przy użyciu <xref:System.Diagnostics.Tracing.IncrementingPollingCounter> .

```csharp
var monitorContentionCounter = new IncrementingPollingCounter(
    "monitor-lock-contention-count",
    this,
    () => Monitor.LockContentionCount
)
{
    DisplayName = "Monitor Lock Contention Count",
    DisplayRateTimeScale = TimeSpan.FromSeconds(1)
};
```

<xref:System.Diagnostics.Tracing.IncrementingPollingCounter>Używa <xref:System.Threading.Monitor.LockContentionCount?displayProperty=nameWithType> interfejsu API do raportowania przyrostu całkowitej liczby rywalizacji o blokadę. <xref:System.Diagnostics.Tracing.IncrementingPollingCounter.DisplayRateTimeScale>Właściwość jest opcjonalna, ale jeśli jest używana, może zapewnić wskazówkę dotyczącą interwału czasu, w którym licznik jest najlepiej wyświetlany. Na przykład liczba rywalizacji blokad jest najlepiej wyświetlana jako _Liczba na sekundę_, więc jej <xref:System.Diagnostics.Tracing.IncrementingPollingCounter.DisplayRateTimeScale> wartość jest równa jednej sekundzie. Współczynnik wyświetlania można dopasować dla różnych typów liczników szybkości.

> [!NOTE]
> <xref:System.Diagnostics.Tracing.IncrementingPollingCounter.DisplayRateTimeScale> _Nie_ jest używany przez program [dotnet-Counters](dotnet-counters.md), a detektory zdarzeń nie są wymagane do korzystania z niego.

Istnieje więcej implementacji liczników do użycia jako odwołanie w repozytorium [środowiska uruchomieniowego platformy .NET](https://github.com/dotnet/runtime/blob/master/src/libraries/System.Private.CoreLib/src/System/Diagnostics/Tracing/RuntimeEventSource.cs) .

## <a name="concurrency"></a>Współbieżność

> [!TIP]
> Interfejs API EventCounters nie gwarantuje bezpieczeństwa wątków. Gdy Delegaty przechodzą do <xref:System.Diagnostics.Tracing.PollingCounter> lub <xref:System.Diagnostics.Tracing.IncrementingPollingCounter> wystąpienia są wywoływane przez wiele wątków, odpowiedzialność za zagwarantowanie bezpieczeństwa wątków delegatów.

Rozważmy na przykład następujące, <xref:System.Diagnostics.Tracing.EventSource> Aby śledzić żądania.

:::code language="csharp" source="snippets/EventCounters/RequestEventSource.cs":::

`AddRequest()`Metodę można wywołać z procedury obsługi żądań, a następnie `RequestRateCounter` sonduje wartość w interwale określonym przez odbiorcę licznika. Jednak `AddRequest()` Metoda może być wywoływana przez wiele wątków jednocześnie, co w przypadku wystąpienia warunku `_requestCount` . Bezpieczny wątkowo alternatywny sposób, aby zwiększyć `_requestCount` użycie <xref:System.Threading.Interlocked.Increment%2A?displayProperty=nameWithType> .

```csharp
public void AddRequest() => Interlocked.Increment(ref _requestCount);
```

Aby zapobiec rozdartym odczytom (na 32-bitowych architekturach) `long` `_requestCount` użycia pola <xref:System.Threading.Interlocked.Read%2A?displayProperty=nameWithType> .

```csharp
_requestRateCounter = new IncrementingPollingCounter("request-rate", this, () => Interlocked.Read(ref _requestCount))
{
    DisplayName = "Request Rate",
    DisplayRateTimeScale = TimeSpan.FromSeconds(1)
};
```

## <a name="consume-eventcounters"></a>Korzystanie z EventCounters

Istnieją dwa podstawowe sposoby używania EventCounters, w ramach procesu lub out-of-proc. Użycie EventCounters można podzielić na trzy warstwy różnych zużywanych technologii.

- Transportowanie zdarzeń w strumieniu nieprzetworzonym za pośrednictwem funkcji ETW lub EventPipe:
  - Interfejsy API ETW są dostarczane z systemem operacyjnym Windows, a EventPipe jest dostępny jako [interfejs API platformy .NET](https://github.com/dotnet/diagnostics/blob/master/documentation/design-docs/diagnostics-client-library.md#1-attaching-to-a-process-and-dumping-out-all-the-runtime-gc-events-in-real-time-to-the-console)lub diagnostyczny [Protokół IPC](https://github.com/dotnet/diagnostics/blob/master/documentation/design-docs/ipc-protocol.md).
- Dekodowanie strumienia zdarzeń binarnych do zdarzeń:
  - [Biblioteka zdarzenie śledzenia](https://www.nuget.org/packages/Microsoft.Diagnostics.Tracing.TraceEvent) obsługuje zarówno formaty strumieni ETW, jak i EventPipe.
- Narzędzia wiersza polecenia i graficznego interfejsu użytkownika:
  - Narzędzia takie jak narzędzia PerfView (ETW lub EventPipe), dotnet-Counters (tylko EventPipe) i monitor dotnet (tylko EventPipe).

### <a name="consume-out-of-proc"></a>Korzystanie z zewnątrz procesu

Korzystanie z EventCounters out-of-proc jest bardzo typowym podejściem. Za pomocą programu [dotnet-Counters](dotnet-counters.md) można korzystać na wielu platformach za pośrednictwem EventPipe. To `dotnet-counters` Narzędzie jest globalnym narzędziem interfejsu wiersza polecenia dotnet dla wielu platform, które może służyć do monitorowania wartości liczników. Aby dowiedzieć się, jak używać `dotnet-counters` do monitorowania liczników, zobacz [dotnet-Counters](dotnet-counters.md)lub pracuj przez [wydajność miary za pomocą](event-counter-perf.md) samouczka EventCounters.

#### <a name="dotnet-trace"></a>dotnet-trace

`dotnet-trace`Za pomocą tego narzędzia można korzystać z danych licznika przez EventPipe. Oto przykład użycia `dotnet-trace` do zbierania danych licznika.

```console
dotnet-trace collect --process-id <pid> Sample.EventCounter.Minimal:0:0:EventCounterIntervalSec=1
```

Aby uzyskać więcej informacji na temat zbierania wartości licznika w czasie, zobacz dokumentację [śledzenia dotnet](dotnet-trace.md#use-dotnet-trace-to-collect-counter-values-over-time) .

#### <a name="azure-application-insights"></a>Azure Application Insights

EventCounters mogą być używane przez Azure Monitor, w tym Application Insights platformy Azure. Liczniki można dodawać i usuwać oraz korzystać z nich, aby można było określić liczniki niestandardowe lub dobrze znane liczniki. Aby uzyskać więcej informacji, zobacz [Dostosowywanie liczników do zebrania](/azure/azure-monitor/app/eventcounters#customizing-counters-to-be-collected).

#### <a name="dotnet-monitor"></a>dotnet-monitor

`dotnet-monitor`Narzędzie to eksperymentalne narzędzie, które ułatwia uzyskiwanie dostępu do informacji diagnostycznych w procesie platformy .NET. Narzędzie służy jako nadzbiór wszystkich narzędzi diagnostycznych. Oprócz śledzenia można monitorować metryki, zbierać zrzuty pamięci i zbierać zrzuty GC. Jest dystrybuowany jako narzędzie interfejsu wiersza polecenia i obraz platformy Docker. Udostępnia interfejs API REST, a kolekcja artefaktów diagnostycznych odbywa się za pomocą wywołań REST.

Aby uzyskać więcej informacji, zobacz [wprowadzenie do monitora dotnet-monitor, narzędzia eksperymentalne](https://devblogs.microsoft.com/dotnet/introducing-dotnet-monitor).

### <a name="consume-in-proc"></a>Używanie w procesie

Można korzystać z wartości licznika za pośrednictwem <xref:System.Diagnostics.Tracing.EventListener> interfejsu API. <xref:System.Diagnostics.Tracing.EventListener>Jest to wewnątrzprocesowy sposób zużywania wszelkich zdarzeń, które są zapisywane przez wszystkie wystąpienia <xref:System.Diagnostics.Tracing.EventSource> w aplikacji. Aby uzyskać więcej informacji na temat korzystania z `EventListener` interfejsu API, zobacz <xref:System.Diagnostics.Tracing.EventListener> .

Najpierw należy <xref:System.Diagnostics.Tracing.EventSource> włączyć wartość licznika. Zastąp <xref:System.Diagnostics.Tracing.EventListener.OnEventSourceCreated%2A?displayProperty=nameWithType> metodę, aby otrzymać powiadomienie, gdy <xref:System.Diagnostics.Tracing.EventSource> zostanie utworzony, a jeśli jest to poprawne <xref:System.Diagnostics.Tracing.EventSource> w EventCounters, możesz je wywoływać <xref:System.Diagnostics.Tracing.EventListener.EnableEvents%2A?displayProperty=nameWithType> . Oto przykładowe przesłonięcie:

:::code language="csharp" source="snippets/EventCounters/SimpleEventListener.cs" range="16-27":::

#### <a name="sample-code"></a>Przykładowy kod

Poniżej znajduje się przykładowa <xref:System.Diagnostics.Tracing.EventListener> Klasa, która drukuje wszystkie nazwy liczników i wartości z środowiska uruchomieniowego platformy .NET <xref:System.Diagnostics.Tracing.EventSource> , aby opublikować jego liczniki wewnętrzne ( `System.Runtime` ) w pewnym interwale.

:::code language="csharp" source="snippets/EventCounters/SimpleEventListener.cs":::

Jak pokazano powyżej, _należy_ upewnić się, że `"EventCounterIntervalSec"` argument jest ustawiony w `filterPayload` argumencie podczas wywoływania <xref:System.Diagnostics.Tracing.EventListener.EnableEvents%2A> . W przeciwnym razie liczniki nie będą mogły opróżniać wartości, ponieważ nie wie, z jakim interwałem należy uzyskać opróżnianie.

## <a name="see-also"></a>Zobacz też

- [dotnet-counters](dotnet-counters.md)
- [dotnet-trace](dotnet-trace.md)
- <xref:System.Diagnostics.Tracing.EventCounter>
- <xref:System.Diagnostics.Tracing.EventListener>
- <xref:System.Diagnostics.Tracing.EventSource>
