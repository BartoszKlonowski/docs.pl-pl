---
title: Omówienie narzędzi diagnostycznych — .NET Core
description: Przegląd narzędzi i technik dostępnych do diagnozowania aplikacji .NET Core.
ms.date: 07/16/2020
ms.topic: overview
ms.openlocfilehash: 0aa404497cb7d6a488fb51e1df8f7f45d4f213fd
ms.sourcegitcommit: 4b79862c5b41fbd86cf38f926f6a49516059f6f2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/18/2020
ms.locfileid: "97678103"
---
# <a name="what-diagnostic-tools-are-available-in-net-core"></a>Jakie narzędzia diagnostyczne są dostępne w środowisku .NET Core?

Oprogramowanie nie zawsze zachowuje się w oczekiwany sposób, ale .NET Core ma narzędzia i interfejsy API, które ułatwią zdiagnozowanie tych problemów szybko i efektywnie.

Ten artykuł ułatwia znalezienie różnych potrzebnych narzędzi.

## <a name="managed-debuggers"></a>Debugery zarządzane

[Zarządzane debugery](managed-debuggers.md) umożliwiają korzystanie z programu. Wstrzymywanie, przyrostowe wykonywanie, badanie i wznawianie zawiera szczegółowe informacje o zachowaniu kodu. Debuger to pierwszy wybór służący do diagnozowania problemów funkcjonalnych, które można łatwo odtworzyć.

## <a name="logging-and-tracing"></a>Rejestrowanie i śledzenie

[Rejestrowanie i śledzenie](logging-tracing.md) to powiązane techniki. Odnoszą się one do kodu instrumentacji do tworzenia plików dziennika. Pliki rejestrują szczegóły działania programu. Te szczegółowe informacje mogą służyć do diagnozowania najbardziej złożonych problemów. W połączeniu z sygnaturami czasowymi te techniki są również przydatne w badaniach wydajności.

## <a name="metrics"></a>Metryki

[EventCounters](event-counters.md) umożliwia pisanie metryk w celu identyfikowania i monitorowania problemów z wydajnością. Metryki wiążą się z mniejszym obciążeniem wydajności w porównaniu z śledzeniem, dzięki czemu jest bardziej odpowiednie do monitorowania wydajności. Środowisko uruchomieniowe i biblioteki platformy .NET publikuje kilka [dobrze znanych EventCounters](available-counters.md) , które można monitorować.

## <a name="unit-testing"></a>Testowanie jednostek

[Testowanie jednostkowe](../testing/index.md) to kluczowy składnik ciągłej integracji i wdrażania wysokiej jakości oprogramowania. Testy jednostkowe zostały zaprojektowane w celu zapewnienia wczesnego ostrzegania w przypadku wystąpienia elementu.

## <a name="dumps"></a>Zrzuty

[Zrzut](./dumps.md) to plik zawierający migawkę procesu w momencie tworzenia. Mogą one być przydatne do sprawdzania stanu aplikacji na potrzeby debugowania.

## <a name="collect-diagnostics-in-containers"></a>Zbieranie danych diagnostycznych w kontenerach

Te same narzędzia diagnostyczne, które są używane w środowiskach z systemem Linux, mogą również służyć do [zbierania danych diagnostycznych w kontenerach](diagnostics-in-containers.md). Istnieje tylko kilka zmian użycia wymaganych do upewnienia się, że narzędzia działają w kontenerze platformy Docker.

## <a name="net-core-diagnostic-global-tools"></a>Narzędzia diagnostyczne programu .NET Core

### <a name="dotnet-counters"></a>dotnet-counters

[dotnet-Counters](dotnet-counters.md) to narzędzie do monitorowania wydajności służące do monitorowania kondycji pierwszego poziomu i badania wydajności. Obserwuje wartości liczników wydajności publikowane za pośrednictwem <xref:System.Diagnostics.Tracing.EventCounter> interfejsu API. Można na przykład szybko monitorować elementy, takie jak użycie procesora CPU, lub częstotliwość zgłaszania wyjątków w aplikacji .NET Core.

### <a name="dotnet-dump"></a>dotnet-dump

Narzędzie [dotnet-dump](dotnet-dump.md) to sposób zbierania i analizowania zrzutów podstawowych systemów Windows i Linux bez natywnego debugera.

### <a name="dotnet-gcdump"></a>dotnet-gcdump

Narzędzie [dotnet-gcdump](dotnet-gcdump.md) to sposób zbierania zrzutów pamięci podręcznej (Moduł wyrzucania elementów bezużytecznych) na żywo procesów platformy .NET.

### <a name="dotnet-trace"></a>dotnet-trace

Program .NET Core zawiera informacje o tym, w jaki sposób są `EventPipe` udostępniane dane diagnostyczne. Narzędzie do [śledzenia dotnet](dotnet-trace.md) umożliwia korzystanie z interesujących danych profilowania z poziomu aplikacji, które mogą pomóc w scenariuszach, w których konieczne jest powolne działanie aplikacji.

### <a name="dotnet-symbol"></a>dotnet-symbol

polecenie [dotnet-symbol](dotnet-symbol.md) umożliwia pobieranie plików (symboli, DAC/DBI, plików hosta itp.), które są konieczne do otwarcia podstawowego zrzutu lub minizrzutu. Użyj tego narzędzia, jeśli potrzebujesz symboli i modułów do debugowania pliku zrzutu przechwytywanego na innym komputerze.

### <a name="dotnet-sos"></a>dotnet-sos

[dotnet-sos](dotnet-sos.md) służy do instalowania [rozszerzenia debugowania SOS](../../framework/tools/sos-dll-sos-debugging-extension.md) w systemie Linux lub MacOS (lub w systemie Windows, jeśli są używane starsze narzędzia debugowania).

### <a name="perfcollect"></a>PerfCollect

[PerfCollect](trace-perfcollect-lttng.md) to skrypt bash, którego można użyć do zbierania śladów z `perf` i `LTTng` bardziej szczegółowej analizy wydajności aplikacji .NET działających w ramach dystrybucji systemu Linux.

## <a name="net-core-diagnostics-tutorials"></a>Samouczki dotyczące diagnostyki platformy .NET Core

### <a name="debug-a-memory-leak"></a>Debugowanie przecieku pamięci

[Samouczek: debugowanie przecieku pamięci](debug-memory-leak.md) przeprowadzi przez znalezienie przecieku pamięci. Narzędzie [dotnet-Counters](dotnet-counters.md) służy do potwierdzenia przecieku i narzędzia [dotnet-dump](dotnet-dump.md) służy do diagnozowania wycieku.

### <a name="debug-high-cpu-usage"></a>Debugowanie wysokiego użycia procesora

[Samouczek: debugowanie dużego użycia procesora CPU](debug-highcpu.md) przeprowadzi Cię przez badanie wysokiego użycia procesora CPU. Za pomocą narzędzia [dotnet-Counters](dotnet-counters.md) można potwierdzić duże użycie procesora CPU. Następnie przeprowadzi Cię przez proces [śledzenia narzędzia do analizy wydajności ( `dotnet-trace` )](dotnet-trace.md) lub systemu Linux `perf` w celu zbierania i wyświetlania profilu użycia procesora CPU.

### <a name="debug-deadlock"></a>Debugowanie zakleszczenia

[Samouczek: zakleszczenie debugowania](debug-deadlock.md) pokazuje, w jaki sposób używać narzędzia [dotnet-dump](dotnet-dump.md) do badania wątków i blokad.

### <a name="debug-linux-dumps"></a>Debugowanie zrzutów systemu Linux

[Debugowanie zrzutów systemu Linux](debug-linux-dumps.md) wyjaśnia, jak zbierać i analizować zrzuty w systemie Linux.

### <a name="measure-performance-using-eventcounters"></a>Mierzenie wydajności przy użyciu EventCounters

[Samouczek: pomiar wydajności za pomocą EventCounters w programie .NET](event-counter-perf.md) pokazuje, jak używać <xref:System.Diagnostics.Tracing.EventCounter> interfejsu API do mierzenia wydajności aplikacji .NET.
