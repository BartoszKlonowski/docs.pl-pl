---
title: Debugowanie wysokiego użycia procesora CPU — .NET Core
description: Samouczek, który przeprowadzi Cię przez debugowanie wysokiego użycia procesora CPU w programie .NET Core.
ms.topic: tutorial
ms.date: 07/20/2020
ms.openlocfilehash: 91f31f77b54398d2f9816890338955bc9b0852e4
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96437836"
---
# <a name="debug-high-cpu-usage-in-net-core"></a>Debugowanie wysokiego użycia procesora CPU w programie .NET Core

**Ten artykuł ma zastosowanie do: ✔️** .net Core 3,1 SDK i nowszych wersjach

W tym samouczku dowiesz się, jak debugować nadmierne scenariusze użycia procesora CPU. Korzystając z podanego ASP.NET Core przykładowego repozytorium kodu źródłowego [aplikacji sieci Web](/samples/dotnet/samples/diagnostic-scenarios) , można przypadkowo zaistnieć zakleszczenie. Punkt końcowy będzie miał Rozwieszanie i kumulację wątków. Dowiesz się, jak za pomocą różnych narzędzi można zdiagnozować ten scenariusz za pomocą kilku kluczowych fragmentów danych diagnostycznych.

W tym samouczku wykonasz następujące czynności:

> [!div class="checklist"]
>
> - Zbadaj duże użycie procesora CPU
> - Określanie użycia procesora przy użyciu [liczników dotnet](dotnet-counters.md)
> - Użyj [śledzenia dotnet](dotnet-trace.md) do generowania śladu
> - Wydajność profilowania w programie narzędzia PerfView
> - Diagnozowanie i rozwiązywanie nadmiernego użycia procesora CPU

## <a name="prerequisites"></a>Wymagania wstępne

Samouczek używa:

- [.NET Core 3,1 SDK](https://dotnet.microsoft.com/download/dotnet-core) lub nowsza wersja.
- [Przykładowy obiekt docelowy debugowania](/samples/dotnet/samples/diagnostic-scenarios) , aby wyzwolić scenariusz.
- [dotnet-Trace](dotnet-trace.md) do wyświetlania listy procesów i generowania profilu.
- [dotnet-Counters](dotnet-counters.md) do monitorowania użycia procesora CPU.

## <a name="cpu-counters"></a>Liczniki procesora CPU

Przed próbą zebrania danych diagnostycznych należy obserwować wysoki poziom procesora CPU. Uruchom [przykładową aplikację](/samples/dotnet/samples/diagnostic-scenarios) przy użyciu następującego polecenia w katalogu głównym projektu.

```dotnetcli
dotnet run
```

Aby znaleźć identyfikator procesu, użyj następującego polecenia:

```dotnetcli
dotnet-trace ps
```

Zanotuj identyfikator procesu z danych wyjściowych polecenia. Nasz identyfikator procesu został utworzony `22884` , ale będzie się różnić. Aby sprawdzić bieżące użycie procesora, użyj polecenia narzędzia [dotnet-Counters](dotnet-counters.md) :

```dotnetcli
dotnet-counters monitor --refresh-interval 1 -p 22884
```

`refresh-interval`Jest to liczba sekund między wartościami procesora sondowania licznika. Dane wyjściowe będą podobne do następujących:

```console
Press p to pause, r to resume, q to quit.
    Status: Running

[System.Runtime]
    % Time in GC since last GC (%)                         0
    Allocation Rate / 1 sec (B)                            0
    CPU Usage (%)                                          0
    Exception Count / 1 sec                                0
    GC Heap Size (MB)                                      4
    Gen 0 GC Count / 60 sec                                0
    Gen 0 Size (B)                                         0
    Gen 1 GC Count / 60 sec                                0
    Gen 1 Size (B)                                         0
    Gen 2 GC Count / 60 sec                                0
    Gen 2 Size (B)                                         0
    LOH Size (B)                                           0
    Monitor Lock Contention Count / 1 sec                  0
    Number of Active Timers                                1
    Number of Assemblies Loaded                          140
    ThreadPool Completed Work Item Count / 1 sec           3
    ThreadPool Queue Length                                0
    ThreadPool Thread Count                                7
    Working Set (MB)                                      63
```

Gdy aplikacja sieci Web działa natychmiast po uruchomieniu, procesor CPU nie jest zużywany w ogóle i jest raportowany pod adresem `0%` . Przejdź do `api/diagscenario/highcpu` trasy `60000` jako parametr trasy:

`https://localhost:5001/api/diagscenario/highcpu/60000`

Teraz ponownie uruchom polecenie [dotnet-Counters](dotnet-counters.md) . Aby monitorować tylko `cpu-usage` , określ `System.Runtime[cpu-usage]` jako część polecenia.

```dotnetcli
dotnet-counters monitor --counters System.Runtime[cpu-usage] -p 22884 --refresh-interval 1
```

Powinno zostać wyświetlone zwiększenie użycia procesora CPU, jak pokazano poniżej:

```console
Press p to pause, r to resume, q to quit.
    Status: Running

[System.Runtime]
    CPU Usage (%)                                         25
```

Przez cały czas trwania żądania użycie procesora CPU zostanie aktywowane na około 25%. W zależności od komputera hosta należy oczekiwać różnego użycia procesora CPU.

> [!TIP]
> Aby wizualizować nawet wyższe użycie procesora CPU, można jednocześnie korzystać z tego punktu końcowego na wielu kartach przeglądarki.

W tym momencie można bezpiecznie wypowiedzieć, że procesor CPU jest uruchomiony na wyższym poziomie niż oczekiwano.

## <a name="trace-generation"></a>Generowanie śladu

Podczas analizowania powolnego żądania potrzebne jest narzędzie diagnostyczne, które może zapewnić wgląd w to, co robi kod. Typowym wyborem jest Profiler, a istnieją różne opcje profilera do wyboru.

### <a name="linux"></a>[Linux](#tab/linux)

Za `perf` pomocą tego narzędzia można generować profile aplikacji .NET Core. Wyjdź z poprzedniego wystąpienia [przykładowego celu debugowania](/samples/dotnet/samples/diagnostic-scenarios).

Ustaw `COMPlus_PerfMapEnabled` zmienną środowiskową, aby spowodować, że aplikacja .NET Core utworzy `map` plik w `/tmp` katalogu. Ten `map` plik jest używany przez program `perf` do mapowania adresu procesora CPU na funkcje generowane przez JIT według nazwy. Aby uzyskać więcej informacji, zobacz [Zapisywanie mapy wydajności](../run-time-config/debugging-profiling.md#write-perf-map).

Uruchom [przykładowy cel debugowania](/samples/dotnet/samples/diagnostic-scenarios) w tej samej sesji terminala.

```dotnetcli
export COMPlus_PerfMapEnabled=1
dotnet run
```

Wykorzystaj ponownie wysoki punkt końcowy interfejsu API procesora CPU ( `https://localhost:5001/api/diagscenario/highcpu/60000` ). Gdy jest uruchomiona w ramach żądania 1-minutowego, uruchom `perf` polecenie z identyfikatorem procesu:

```bash
sudo perf record -p 2266 -g
```

`perf`Polecenie uruchamia proces zbierania danych o wydajności. Pozwól na około 20-30 sekund, a następnie naciśnij <kbd>klawisze CTRL + C</kbd> , aby wyjść z procesu kolekcjonowania. Możesz użyć tego samego `perf` polecenia, aby wyświetlić dane wyjściowe śledzenia.

```bash
sudo perf report -f
```

Możesz również generować _grafy płomieniowe_ za pomocą następujących poleceń:

```bash
git clone --depth=1 https://github.com/BrendanGregg/FlameGraph
sudo perf script | FlameGraph/stackcollapse-perf.pl | FlameGraph/flamegraph.pl > flamegraph.svg
```

To polecenie spowoduje wygenerowanie elementu `flamegraph.svg` , który można wyświetlić w przeglądarce, aby zbadać problem z wydajnością:

[![Obraz SVG grafu](media/flamegraph.jpg)](media/flamegraph.jpg#lightbox)

### <a name="windows"></a>[Windows](#tab/windows)

W systemie Windows można użyć narzędzia do [śledzenia dotnet](dotnet-trace.md) jako profilera. Korzystając z poprzedniego [przykładowego celu debugowania](/samples/dotnet/samples/diagnostic-scenarios), należy ponownie wykonać wysoki punkt końcowy procesora CPU ( `https://localhost:5001/api/diagscenario/highcpu/60000` ). Gdy jest uruchomiona w ramach żądania 1-minutowego, użyj `collect` polecenia w następujący sposób:

```dotnetcli
dotnet-trace collect -p 22884 --providers Microsoft-DotNETCore-SampleProfiler
```

Zezwól na uruchomienie programu [dotnet-Trace](dotnet-trace.md) przez około 20-30 sekund, a następnie naciśnij klawisz <kbd>Enter</kbd> , aby wyjść z kolekcji. Wynik jest `nettrace` plikiem znajdującym się w tym samym folderze. `nettrace`Pliki są świetnym sposobem korzystania z istniejących narzędzi analitycznych w systemie Windows.

Otwórz `nettrace` program, [`PerfView`](https://github.com/microsoft/perfview/blob/master/documentation/Downloading.md) tak jak pokazano poniżej.

[![Obraz narzędzia PerfView](media/perfview.jpg)](media/perfview.jpg#lightbox)

---

## <a name="see-also"></a>Zobacz też

- [dotnet-Trace](dotnet-trace.md) do procesów list
- [dotnet-Counters](dotnet-counters.md) , aby sprawdzić użycie pamięci zarządzanej
- [dotnet-dump](dotnet-dump.md) aby zebrać i przeanalizować plik zrzutu
- [dotnet/Diagnostyka](https://github.com/dotnet/diagnostics/tree/master/documentation/tutorial)

## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [Debugowanie zakleszczenia w programie .NET Core](debug-deadlock.md)
