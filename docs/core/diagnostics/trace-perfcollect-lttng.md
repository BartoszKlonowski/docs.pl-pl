---
title: Śledzenie aplikacji .NET za pomocą PerfCollect.
description: Samouczek, który przeprowadzi Cię przez zbieranie śladów z perfcollect na platformie .NET.
ms.topic: tutorial
ms.date: 10/23/2020
ms.openlocfilehash: 53e4584953d2af4e766daadfa757cca752ae7329
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/16/2020
ms.locfileid: "97593223"
---
# <a name="trace-net-applications-with-perfcollect"></a>Śledzenie aplikacji .NET za pomocą PerfCollect

**Ten artykuł ma zastosowanie do: ✔️** .net Core 2,1 SDK i nowszych wersjach

W przypadku wystąpienia problemów z wydajnością w systemie Linux zbieranie danych śledzenia za pomocą `perfcollect` może służyć do zbierania szczegółowych informacji na temat tego, co się dzieje na komputerze w momencie problemu z wydajnością.

`perfcollect` to skrypt bash, który wykorzystuje [generowanie śledzenia Tookit-Next systemu Linux (LTTng)](https://lttng.org) do zbierania zdarzeń utworzonych na podstawie środowiska uruchomieniowego lub dowolnego elementu [EventSource](xref:System.Diagnostics.Tracing.EventListener), a także [wydajności](https://perf.wiki.kernel.org/) do zbierania próbek procesora CPU procesu docelowego.

## <a name="prepare-your-machine"></a>Przygotuj maszynę

Wykonaj następujące kroki, aby przygotować komputer do zbierania danych śledzenia wydajności za pomocą programu `perfcollect` .

> [!NOTE]
> Jeśli jesteś w środowisku kontenera, kontener musi mieć `SYS_ADMIN` możliwość. Aby uzyskać więcej informacji na temat śledzenia aplikacji wewnątrz kontenerów za pomocą PerfCollect, zobacz [zbieranie danych diagnostycznych w kontenerach](./diagnostics-in-containers.md).

1. Pobierz `perfcollect` .

    > ```bash
    > curl -OL https://aka.ms/perfcollect
    > ```

2. Utwórz plik wykonywalny skryptu.

    > ```bash
    > chmod +x perfcollect
    > ```

3. Wymagania wstępne dotyczące śledzenia instalacji — są to rzeczywiste biblioteki śledzenia.

    > ```bash
    > sudo ./perfcollect install
    > ```

    Spowoduje to zainstalowanie następujących warunków wstępnych na maszynie:

    1. `perf`: podsystem zdarzeń wydajności systemu Linux oraz aplikacja do zbierania/przeglądania w trybie użytkownika. `perf` jest częścią źródła jądra systemu Linux, ale zazwyczaj nie jest instalowany domyślnie.

    2. `LTTng`: Służy do przechwytywania danych zdarzeń emitowanych w czasie wykonywania przez CoreCLR. Te dane są następnie używane do analizowania zachowania różnych składników środowiska uruchomieniowego, takich jak GC, JIT i Pula wątków.

Najnowsze wersje programu .NET Core i narzędzie wydajności systemu Linux obsługują automatyczne rozpoznawanie nazw metod dla kodu struktury. Jeśli pracujesz z platformą .NET Core w wersji 3,1 lub mniejszej, konieczny jest dodatkowy krok. Aby uzyskać szczegółowe informacje, zobacz [Rozpoznawanie symboli struktury](#resolve-framework-symbols) .

W przypadku rozpoznawania nazw metod natywnych bibliotek DLL środowiska uruchomieniowego (takich jak libcoreclr.so) program `perfcollect` rozpozna symbole dla nich podczas konwertowania danych, ale tylko wtedy, gdy są obecne symbole dla tych plików binarnych. Aby uzyskać szczegółowe informacje, zobacz sekcję [pobieranie symboli dla natywnego środowiska uruchomieniowego](#get-symbols-for-the-native-runtime) .

## <a name="collect-a-trace"></a>Zbieranie śladu

1. Dostępne są dwie powłoki — jeden do sterowania śledzeniem, zwany jako **[Trace]**, i jeden do uruchamiania aplikacji, zwany jako **[app]**.

2. **[Trace]** Rozpocznij zbieranie danych.

    > ```bash
    > sudo ./perfcollect collect sampleTrace
    > ```

    Oczekiwane dane wyjściowe:

    > ```bash
    > Collection started.  Press CTRL+C to stop.
    > ```

3. **[Aplikacja]** Skonfiguruj powłokę aplikacji z następującymi zmiennymi środowiskowymi — umożliwia to konfigurację śledzenia CoreCLR.

    > ```bash
    > export COMPlus_PerfMapEnabled=1
    > export COMPlus_EnableEventLog=1
    > ```

4. **[Aplikacja]** Uruchom aplikację — niech działa tak długo, jak w celu przechwycenia problemu z wydajnością. Dokładna długość może być tak mała, jak jest to konieczne, tak długo, jak przechwytuje okno czasu, w którym występuje problem z wydajnością.

    > ```bash
    > dotnet run
    > ```

5. **[Trace]** Zatrzymaj zbieranie — naciśnij klawisze CTRL + C.

    > ```bash
    > ^C
    > ...STOPPED.
    >
    > Starting post-processing. This may take some time.
    >
    > Generating native image symbol files
    > ...SKIPPED
    > Saving native symbols
    > ...FINISHED
    > Exporting perf.data file
    > ...FINISHED
    > Compressing trace files
    > ...FINISHED
    > Cleaning up artifacts
    > ...FINISHED
    >
    > Trace saved to sampleTrace.trace.zip
    > ```

    Skompresowany plik śledzenia jest teraz przechowywany w bieżącym katalogu roboczym.

## <a name="view-a-trace"></a>Wyświetlanie śladu

Istnieje kilka opcji wyświetlania śladu, który został zebrany. Ślady są najlepiej oglądane przy użyciu [Narzędzia PerfView](https://aka.ms/perfview) w systemie Windows, ale mogą być wyświetlane bezpośrednio w systemie Linux przy użyciu `PerfCollect` samego siebie lub `TraceCompass` .

### <a name="use-perfcollect-to-view-the-trace-file"></a>Użyj PerfCollect, aby wyświetlić plik śledzenia

Możesz użyć perfcollect, aby wyświetlić zebrany ślad. Aby to zrobić, użyj następującego polecenia:

```bash
./perfcollect view sampleTrace.trace.zip
```

Domyślnie zostanie wyświetlone śledzenie procesora CPU aplikacji przy użyciu programu `perf` .

Aby sprawdzić zdarzenia, które zostały zebrane za pośrednictwem `LTTng` , można przekazać flagę w `-viewer lttng` celu wyświetlenia poszczególnych zdarzeń:

```bash
./perfcollect view sampleTrace.trace.zip -viewer lttng
```

Spowoduje to `babeltrace` wydrukowanie ładunku zdarzeń przy użyciu przeglądarki:

```bash
# [01:02:18.189217659] (+0.020132603) ubuntu-xenial DotNETRuntime:ExceptionThrown_V1: { cpu_id = 0 }, { ExceptionType = "System.Exception", ExceptionMessage = "An exception happened", ExceptionEIP = 139875671834775, ExceptionHRESULT = 2148734208, ExceptionFlags = 16, ClrInstanceID = 0 }
# [01:02:18.189250227] (+0.020165171) ubuntu-xenial DotNETRuntime:ExceptionCatchStart: { cpu_id = 0 }, { EntryEIP = 139873639728404, MethodID = 139873626968120, MethodName = "void [helloworld] helloworld.Program::Main(string[])", ClrInstanceID = 0 }
```

### <a name="use-perfview-to-open-the-trace-file"></a>Użyj narzędzia PerfView, aby otworzyć plik śledzenia

Aby wyświetlić Zagregowany widok zarówno przykładowego procesora, jak i zdarzeń, można użyć `PerfView` na komputerze z systemem Windows.

1. Skopiuj plik trace.zip z systemu Linux na komputer z systemem Windows.

2. Pobierz narzędzia PerfView z <https://aka.ms/perfview> .

3. Uruchom PerfView.exe

    > ```cmd
    > PerfView.exe <path to trace.zip file>
    > ```

Narzędzia PerfView wyświetli listę widoków, które są obsługiwane w oparciu o dane zawarte w pliku śledzenia.

- W obszarze badania procesora wybierz **stosy procesora**.

- Aby uzyskać szczegółowe informacje dotyczące GC, wybierz **GCStats**.

- Dla informacji JIT dla poszczególnych procesów/modułów/metod, wybierz **JITStats**.

- Jeśli nie ma widoku dla potrzebnych informacji, możesz spróbować wyszukać zdarzenia w widoku nieprzetworzone zdarzenia.  Wybierz pozycję **zdarzenia**.

Aby uzyskać więcej informacji na temat interpretowania widoków w programie narzędzia PerfView, zobacz linki pomocy w samym widoku lub w oknie głównym w narzędzia PerfView, wybierz opcję **Pomoc->użytkownicy przewodnika**.

### <a name="use-tracecompass-to-open-the-trace-file"></a>Użyj TraceCompass, aby otworzyć plik śledzenia

Aby wyświetlić dane śledzenia, można użyć opcji [zaćmienie TraceCompass](https://www.eclipse.org/tracecompass/) . `TraceCompass` działa również na maszynach z systemem Linux, dzięki czemu nie musisz przenosić śladu do komputera z systemem Windows. Aby można było `TraceCompass` otworzyć plik śledzenia przy użyciu programu, należy rozpakować plik.

```bash
unzip myTrace.trace.zip
```

`perfcollect` program zapisze ślad LTTng zebrany w formacie pliku COLLABORATIVE w podkatalogu w `lttngTrace` . Plik COLLABORATIVE zostanie umieszczony w katalogu, który wygląda jak `lttngTrace/auto-20201025-101230\ust\uid\1000\64-bit\` .

Plik śledzenia COLLABORATIVE można otworzyć w programie `TraceCompass` , zaznaczając `File -> Open Trace` i wybierając `metadata` plik.

Aby uzyskać więcej informacji, zapoznaj się z [ `TraceCompass` dokumentacją](https://www.eclipse.org/tracecompass/).

## <a name="resolve-framework-symbols"></a>Rozpoznawanie symboli struktury

Symbole struktury muszą być generowane ręcznie podczas zbierania śladu. Różnią się one od symboli poziomu aplikacji, ponieważ struktura jest wstępnie skompilowana, podczas gdy kod aplikacji jest kompilowany dokładnie na czas. W przypadku kodu struktury, który został wstępnie skompilowany do kodu natywnego, należy wywołać `crossgen` , który wie, jak generować mapowanie z kodu natywnego do nazwy metod.

`perfcollect` może obsłużyć większość szczegółowych informacji, ale muszą być `crossgen` dostępne. Domyślnie nie jest on instalowany z dystrybucją programu .NET. Jeśli `crossgen` go nie ma, `perfcollect` ostrzega użytkownika i odwołuje się do tych instrukcji. Aby rozwiązać problemy, musisz pobrać dokładnie odpowiednią wersję crossgen dla używanego środowiska uruchomieniowego. Jeśli umieścisz narzędzie crossgen w tym samym katalogu, co biblioteki DLL środowiska uruchomieniowego .NET (na przykład libcoreclr.so), `perfcollect` można je znaleźć i dodać do pliku śledzenia symbole struktury.

Zwykle podczas tworzenia aplikacji platformy .NET po prostu jest generowana Biblioteka DLL dla napisanego kodu, przy użyciu udostępnionej kopii środowiska uruchomieniowego dla pozostałych.   Można jednak również generować informacje o nazwie "samodzielne" aplikacji i zawiera wszystkie biblioteki DLL środowiska uruchomieniowego. `crossgen` jest częścią pakietu NuGet, który jest używany do tworzenia samodzielnych aplikacji, więc jednym ze sposobów uzyskania odpowiedniej wersji programu `crossgen` jest utworzenie samodzielnego pakietu aplikacji.

Przykład:

   >```bash
   > mkdir helloWorld
   > cd helloWorld
   > dotnet new console
   > dotnet publish --self-contained -r linux-x64
   >```

Spowoduje to utworzenie nowej aplikacji Hello world i utworzenie jej jako aplikacji samodzielnej.

Jako efekt po stronie tworzenia samodzielnej aplikacji Narzędzie dotnet pobierze pakiet NuGet o nazwie Runtime. linux-x64. Microsoft. WebCore. app i umieści go w katalogu ~/.nuget/packages/runtime.linux-x64.microsoft.netcore.app/VERSION, gdzie wersja jest numerem wersji środowiska uruchomieniowego platformy .NET Core (na przykład 2.1.0). W obszarze, który jest katalogiem narzędzi i w tym miejscu jest potrzebne narzędzie crossgen. Począwszy od platformy .NET Core 3,0, lokalizacja pakietu to ~/.nuget/packages/microsoft.netcore.app.runtime.linux-x64/VERSION.

`crossgen`Narzędzie należy umieścić obok środowiska uruchomieniowego, które jest aktualnie używane przez aplikację. Zazwyczaj aplikacja używa udostępnionej wersji platformy .NET Core, która jest zainstalowana w/usr/share/dotnet/shared/Microsoft.NETCore.App/VERSION, gdzie wersja jest numerem wersji środowiska uruchomieniowego .NET. Jest to lokalizacja udostępniona, dlatego musisz być administratorem. Jeśli wersja jest 2.1.0, polecenia do zaktualizowania `crossgen` byłyby następujące:

   >```bash
   > sudo bash
   > cp ~/.nuget/packages/runtime.linux-x64.microsoft.netcore.app/2.1.0/tools/crossgen /usr/share/dotnet/shared/Microsoft.NETCore.App/2.1.0
   >```

Po wykonaniu tej czynności program `perfcollect` użyje crossgen w celu uwzględnienia symboli struktury. Ostrzeżenie, które `perfcollect` ma zostać użyte do wystawienia, powinno odejść. Musi to być jeden raz dla każdego komputera (do momentu zaktualizowania środowiska uruchomieniowego).

### <a name="alternative-turn-off-use-of-precompiled-code"></a>Alternatywa: wyłącz użycie wstępnie skompilowanego kodu

Jeśli nie masz możliwości zaktualizowania środowiska uruchomieniowego .NET (do dodania `crossgen` ) lub jeśli powyższa procedura nie zadziałała z jakiegoś powodu, istnieje inne podejście do uzyskiwania symboli struktury. Możesz powiedzieć środowisko uruchomieniowe, aby po prostu nie używać wstępnie skompilowanego kodu struktury. Kod zostanie skompilowany dokładnie i `crossgen` nie jest wymagany.

> [!NOTE]
> Wybranie tej metody może wydłużyć czas uruchamiania aplikacji.

W tym celu można dodać następującą zmienną środowiskową:

```bash
export COMPlus_ZapDisable=1
```

Po wprowadzeniu tej zmiany należy uzyskać symbole dla całego kodu platformy .NET.

## <a name="get-symbols-for-the-native-runtime"></a>Pobierz symbole dla natywnego środowiska uruchomieniowego

Większość czasu interesujący Twój własny kod, który jest `perfcollect` rozpoznawany domyślnie. Czasami warto zobaczyć, co się dzieje w bibliotekach DLL platformy .NET (co to jest Ostatnia sekcja), ale czasami co się dzieje w natywnych bibliotekach DLL środowiska uruchomieniowego (zazwyczaj libcoreclr.so).  `perfcollect` program rozpozna symbole dla tych, gdy konwertuje swoje dane, ale tylko wtedy, gdy są obecne symbole dla tych natywnych bibliotek DLL (i znajdują się obok biblioteki, do której się odnoszą).

Istnieje polecenie globalne zwane [symbolem dotnet](https://github.com/dotnet/symstore/blob/master/src/dotnet-symbol/README.md#symbol-downloader-dotnet-cli-extension) . Aby użyć symbolu dotnet-symbol w celu uzyskania natywnych symboli środowiska uruchomieniowego:

1. Zainstaluj program `dotnet-symbol`:

    ```bash
    dotnet tool install -g dotnet-symbol
    ```

2. Pobierz symbole. Jeśli zainstalowana wersja środowiska uruchomieniowego .NET Core to 2.1.0, polecenie to jest następujące:

    ```bash
    mkdir mySymbols
    dotnet symbol --symbols --output mySymbols  /usr/share/dotnet/shared/Microsoft.NETCore.App/2.1.0/lib*.so
    ```

3. Skopiuj symbole do poprawnego miejsca.

    ```bash
    sudo cp mySymbols/* /usr/share/dotnet/shared/Microsoft.NETCore.App/2.1.0
    ```

    Jeśli nie można tego zrobić, ponieważ nie masz dostępu do zapisu do odpowiedniego katalogu, możesz użyć, `perf buildid-cache` Aby dodać symbole.

Następnie należy uzyskać nazwy symboliczne natywnych bibliotek DLL podczas uruchamiania `perfcollect` .

## <a name="collect-in-a-docker-container"></a>Zbieranie danych w kontenerze platformy Docker

Aby uzyskać więcej informacji na temat używania `perfcollect` w środowiskach kontenerów, zobacz [zbieranie danych diagnostycznych w kontenerach](./diagnostics-in-containers.md).

## <a name="learn-more-about-collection-options"></a>Dowiedz się więcej na temat opcji kolekcji

Możesz określić następujące opcjonalne flagi, `perfcollect` Aby lepiej odpowiadały potrzebom diagnostycznym.

### <a name="collect-for-a-specific-duration"></a>Zbieraj przez określony czas trwania

Gdy chcesz zbierać ślady dla określonego czasu trwania, możesz użyć `-collectsec` opcji, a po niej liczby określającej łączną liczbę sekund do zebrania śladu.

### <a name="collect-threadtime-traces"></a>Zbierz ślady threadtime

Określenie `-threadtime` `perfcollect` opcji with umożliwia zbieranie danych użycia procesora CPU dla wątków. Dzięki temu można analizować, gdzie każdy wątek spędza czas procesora CPU.

### <a name="collect-traces-for-managed-memory-and-garbage-collector-performance"></a>Zbieranie śladów wydajności pamięci zarządzanej i modułu wyrzucania elementów bezużytecznych

Poniższe opcje pozwalają na zbieranie zdarzeń GC z środowiska uruchomieniowego.

* `perfcollect collect -gccollectonly`

Zbiera tylko minimalny zestaw zdarzeń zbierania danych GC. Jest to najmniej pełny profil kolekcji zdarzeń GC o najniższym wpływie na wydajność aplikacji docelowej. To polecenie jest analogiczne do `PerfView.exe /GCCollectOnly collect` polecenia w narzędzia PerfView.

* `perfcollect collect -gconly`

Zbieraj więcej szczegółowych zdarzeń zbierania danych GC z zdarzeniami JIT, Loader i Exception. Powoduje to zażądanie więcej zdarzeń pełnych (takich jak informacje o alokacji i informacje o przyłączeniu GC) i ma większy wpływ na wydajność aplikacji docelowej niż `-gccollectonly` opcja. To polecenie jest analogiczne do `PerfView.exe /GCOnly collect` polecenia w narzędzia PerfView.

* `perfcollect collect -gcwithheap`

Zbierz najbardziej szczegółowe zdarzenia zbierania danych GC, które śledzą przeżycie sterty i przesunięcia. Zapewnia to szczegółową analizę zachowania GC, ale powiąże się z dużym kosztem wydajności, ponieważ każda GLOBALna wydajność może trwać dłużej niż dwa razy. Zaleca się zrozumienie implikacji wydajności korzystania z tej opcji śledzenia podczas śledzenia w środowiskach produkcyjnych.
