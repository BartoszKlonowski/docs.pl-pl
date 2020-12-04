---
title: Zdarzenia czasu wykonywania puli wątków
description: Zobacz zdarzenia puli wątków środowiska uruchomieniowego platformy .NET, które zbierają informacje diagnostyczne dotyczące puli wątków w programie .NET Core. Zdarzenia puli wątków to zdarzenia puli wątków roboczych lub zdarzenia puli wątków we/wy.
ms.date: 11/13/2020
ms.topic: reference
helpviewer_keywords:
- ThreadPool events (CoreCLR)
- ETW, thread pool events (CoreCLR)
ms.openlocfilehash: cdd6041c5842d4922c60e33daf6db366f7d35327
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96590044"
---
# <a name="net-runtime-thread-pool-events"></a>Zdarzenia puli wątków środowiska uruchomieniowego .NET

Te zdarzenia zbierają informacje o wątkach procesów roboczych i we/wy w puli wątków. Aby uzyskać więcej informacji na temat korzystania z tych zdarzeń w celach diagnostycznych, zobacz [Rejestrowanie i śledzenie aplikacji .NET](../../core/diagnostics/logging-tracing.md) .

## <a name="iothreadcreate_v1-event"></a>Zdarzenie IOThreadCreate_V1

 W poniższej tabeli przedstawiono słowo kluczowe i poziom.

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`ThreadingKeyword` 0x10000|Informacyjny (4)|

 W poniższej tabeli przedstawiono informacje o zdarzeniu.

|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|
|-----------------------------------|-----------|
|`IOThreadCreate_V1`|44|W puli wątków tworzony jest wątek we/wy.|

 W poniższej tabeli przedstawiono dane zdarzenia.

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`Count`|`win:UInt64`|Liczba wątków we/wy, łącznie z nowo utworzonym wątkiem.|
|`NumRetired`|`win:UInt64`|Liczba wycofanych wątków roboczych.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia CLR lub CoreCLR.|

## <a name="iothreadterminate_v1-event"></a>Zdarzenie IOThreadTerminate_V1

 W poniższej tabeli przedstawiono słowo kluczowe i poziom

|Słowo kluczowe do podniesienia zdarzenia|Poziom
|-----------------------------------|-----------
|`ThreadingKeyword` 0x10000|Informacyjny (4)

 W poniższej tabeli przedstawiono informacje o zdarzeniu.

|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|
|-----------|--------------|-----------------|
|`IOThreadTerminate`|45|Wątek we/wy zostanie przerwany w puli wątków.|

 W poniższej tabeli przedstawiono dane zdarzenia.

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`Count`|`win:UInt64`|Liczba wątków we/wy pozostałych w puli wątków.|
|`NumRetired`|`win:UInt64`|Liczba wycofanych wątków we/wy.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia CLR lub CoreCLR.|

## <a name="iothreadretire_v1-event"></a>Zdarzenie IOThreadRetire_V1

 W poniższej tabeli przedstawiono słowo kluczowe i poziom.

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`ThreadingKeyword` 0x10000|Informacyjny (4)|

 W poniższej tabeli przedstawiono informacje o zdarzeniu.

|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|
|-----------|--------------|-----------------|
|`IOThreadRetire_V1`|46|Wątek we/wy zostaje kandydatem do wycofania.|

 W poniższej tabeli przedstawiono dane zdarzenia.

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`Count`|`win:UInt64`|Liczba wątków we/wy pozostałych w puli wątków.|
|`NumRetired`|`win:UInt64`|Liczba wycofanych wątków we/wy.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia CLR lub CoreCLR.|

## <a name="iothreadunretire_v1-event"></a>Zdarzenie IOThreadUnretire_V1

 W poniższej tabeli przedstawiono słowo kluczowe i poziom.

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`ThreadingKeyword` 0x10000|Informacyjny (4)|

 W poniższej tabeli przedstawiono informacje o zdarzeniu.

|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|
|-----------|--------------|-----------------|
|`IOThreadUnretire_V1`|47|Wątek we/wy jest wycofywany ze względu na liczbę operacji we/wy, która dotarła w czasie oczekiwania, gdy wątek stanie się kandydatem wycofania.|

 W poniższej tabeli przedstawiono dane zdarzenia.

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`Count`|`win:UInt64`|Liczba wątków we/wy w puli wątków, z uwzględnieniem tego.|
|`NumRetired`|`win:UInt64`|Liczba wycofanych wątków we/wy.|
|`ClrInstanceID`|`Win:UInt16`|Unikatowy identyfikator wystąpienia CLR lub CoreCLR.|

## <a name="threadpoolworkerthreadstart-event"></a>Zdarzenie ThreadPoolWorkerThreadStart

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|-----------|
|`ThreadingKeyword` 0x10000|Informacyjny (4)|

|Zdarzenie|Identyfikator zdarzenia|Opis|
|-----------|--------------|-----------------|
|`ThreadPoolWorkerThreadStart`|50|Tworzony jest wątek roboczy.|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`ActiveWorkerThreadCount`|`win:UInt32`|Liczba wątków roboczych dostępnych do przetwarzania pracy, w tym tych, które już przetwarzają prace.|
|`RetiredWorkerThreadCount`|`win:UInt32`|Liczba wątków roboczych, które nie są dostępne do przetwarzania pracy, ale które są przechowywane w rezerwie w przypadku późniejszej liczby wątków.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia CLR lub CoreCLR.|

## <a name="threadpoolworkerthreadstop-event"></a>Zdarzenie ThreadPoolWorkerThreadStop

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|-----------|
|`ThreadingKeyword` 0x10000|Informacyjny (4)|

|Zdarzenie|Identyfikator zdarzenia|Opis|
|-----------|--------------|-----------------|
|`ThreadPoolWorkerThreadStop`|51|Wątek roboczy został zatrzymany.|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`ActiveWorkerThreadCount`|`win:UInt32`|Liczba wątków roboczych dostępnych do przetwarzania pracy, w tym tych, które już przetwarzają prace.|
|`RetiredWorkerThreadCount`|`win:UInt32`|Liczba wątków roboczych, które nie są dostępne do przetwarzania pracy, ale które są przechowywane w rezerwie w przypadku późniejszej liczby wątków.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia CLR lub CoreCLR.|

## <a name="threadpoolworkerthreadwait-event"></a>Zdarzenie ThreadPoolWorkerThreadWait

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|-----------|
|`ThreadingKeyword` 0x10000|Informacyjny (4)|

|Zdarzenie|Identyfikator zdarzenia|Opis|
|-----------|--------------|-----------------|
|`ThreadPoolWorkerThreadWait`|57|Wątek roboczy zaczyna czekać na pracę.|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`ActiveWorkerThreadCount`|`win:UInt32`|Liczba wątków roboczych dostępnych do przetwarzania pracy, w tym tych, które już przetwarzają prace.|
|`RetiredWorkerThreadCount`|`win:UInt32`|Liczba wątków roboczych, które nie są dostępne do przetwarzania pracy, ale które są przechowywane w rezerwie w przypadku późniejszej liczby wątków.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia CLR lub CoreCLR.|

## <a name="threadpoolworkerthreadretirementstart-event"></a>Zdarzenie ThreadPoolWorkerThreadRetirementStart

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|-----------|
|`ThreadingKeyword` 0x10000|Informacyjny (4)|

|Zdarzenie|Identyfikator zdarzenia|Opis|
|-----------|--------------|-----------------|
|`ThreadPoolWorkerThreadRetirementStart`|52|Wątek roboczy jest przeoponą.|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`ActiveWorkerThreadCount`|`win:UInt32`|Liczba wątków roboczych dostępnych do przetwarzania pracy, w tym tych, które już przetwarzają prace.|
|`RetiredWorkerThreadCount`|`win:UInt32`|Liczba wątków roboczych, które nie są dostępne do przetwarzania pracy, ale które są przechowywane w rezerwie w przypadku późniejszej liczby wątków.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia CLR lub CoreCLR.|

## <a name="threadpoolworkerthreadretirementstop-event"></a>Zdarzenie ThreadPoolWorkerThreadRetirementStop

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|-----------|
|`ThreadingKeyword` 0x10000|Informacyjny (4)|

|Zdarzenie|Identyfikator zdarzenia|Opis|
|-----------|--------------|-----------------|
|`ThreadPoolWorkerThreadRetirementStop`|53|Wycofywany wątek roboczy zostanie ponownie uaktywniony.|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`ActiveWorkerThreadCount`|`win:UInt32`|Liczba wątków roboczych dostępnych do przetwarzania pracy, w tym tych, które już przetwarzają prace.|
|`RetiredWorkerThreadCount`|`win:UInt32`|Liczba wątków roboczych, które nie są dostępne do przetwarzania pracy, ale które są przechowywane w rezerwie w przypadku późniejszej liczby wątków.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia CLR lub CoreCLR.|

## <a name="threadpoolworkerthreadadjustmentsample-event"></a>Zdarzenie ThreadPoolWorkerThreadAdjustmentSample

 W poniższej tabeli przedstawiono słowo kluczowe i poziom.

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`ThreadingKeyword` 0x10000|Informacyjny (4)|

 W poniższej tabeli przedstawiono informacje o zdarzeniu.

|Zdarzenie|Identyfikator zdarzenia|Opis|
|-----------|--------------|-----------------|
|`ThreadPoolWorkerThreadAdjustmentSample`|54|Odnosi się do kolekcji informacji dla jednej próbki; oznacza to, że pomiar przepływności z pewnym poziomem współbieżności w czasie.|

 W poniższej tabeli przedstawiono dane zdarzenia.

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`Throughput`|`win:Double`|Liczba zaawansowania na jednostkę czasu.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia CLR lub CoreCLR.|

## <a name="threadpoolworkerthreadadjustmentadjustment-event"></a>Zdarzenie ThreadPoolWorkerThreadAdjustmentAdjustment

 W poniższej tabeli przedstawiono słowo kluczowe i poziom.

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`ThreadingKeyword` 0x10000|Informacyjny (4)|

 W poniższej tabeli przedstawiono informacje o zdarzeniu.

|Zdarzenie|Identyfikator zdarzenia|Opis|
|-----------|--------------|-----------------|
|`ThreadPoolWorkerThreadAdjustmentAdjustment`|55|Rejestruje zmianę w kontrolce, gdy algorytm iniekcji wątku (Hill-wspinanie się) określa, że zmiana na poziomie współbieżności jest na miejscu.|

 W poniższej tabeli przedstawiono dane zdarzenia.

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`AverageThroughput`|`win:Double`|Średnia przepływność próbki pomiarów.|
|`NewWorkerThreadCount`|`win:UInt32`|Nowa liczba aktywnych wątków roboczych.|
|`Reason`|`win:UInt32`|Przyczyna korekty.<br /><br /> `0x0` Rozgrzewania.<br /><br /> `0x1` Inicjacj.<br /><br /> `0x2` -Losowe przechodzenie.<br /><br /> `0x3` -Wspinanie się Przenieś.<br /><br /> `0x4` — Zmień punkt.<br /><br /> `0x5` Utrwala.<br /><br /> `0x6` Deficyt.<br /><br /> `0x7` — Przekroczono limit czasu wątku.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia CLR lub CoreCLR.|

## <a name="threadpoolworkerthreadadjustmentstats-event"></a>Zdarzenie ThreadPoolWorkerThreadAdjustmentStats

 W poniższej tabeli przedstawiono słowo kluczowe i poziom.

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`ThreadingKeyword` 0x10000|Verbose (5)

 W poniższej tabeli przedstawiono informacje o zdarzeniu.

|Zdarzenie|Identyfikator zdarzenia|Opis|
|-----------|--------------|-----------------|
|`ThreadPoolWorkerThreadAdjustmentStats`|56|Zbiera dane w puli wątków.|

 W poniższej tabeli przedstawiono dane zdarzenia

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`Duration`|`win:Double`|Czas (w sekundach), w którym te statystyki zostały zebrane.|
|`Throughput`|`win:Double`|Średnia liczba zaawansowanych na sekundę w tym interwale.|
|`ThreadWave`|`win:Double`|Zarezerwowane do użytku wewnętrznego.|
|`ThroughputWave`|`win:Double`|Zarezerwowane do użytku wewnętrznego.|
|`ThroughputErrorEstimate`|`win:Double`|Zarezerwowane do użytku wewnętrznego.|
|`AverageThroughputErrorEstimate`|`win:Double`|Zarezerwowane do użytku wewnętrznego.|
|`ThroughputRatio`|`win:Double`|Względne ulepszenie przepływności spowodowane przez różnice w liczbie wątków roboczych w tym interwale.|
|`Confidence`|`win:Double`|Miara ważności pola ThroughputRatio.|
|`NewcontrolSetting`|`win:Double`|Liczba aktywnych wątków roboczych, które będą stanowić podstawę dla przyszłych różnic w aktywnej liczbie wątków.|
|`NewThreadWaveMagnitude`|`win:UInt16`|Wielkość przyszłych wariantów w aktywnej liczbie wątków.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia CLR lub CoreCLR.|

## <a name="threadpoolenqueue-event"></a>Zdarzenie ThreadPoolEnqueue

 W poniższej tabeli przedstawiono słowo kluczowe i poziom.

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`ThreadingKeyword` 0x10000|Verbose (5)

 W poniższej tabeli przedstawiono informacje o zdarzeniu.

|Zdarzenie|Identyfikator zdarzenia|Opis|
|-----------|--------------|-----------------|
|`ThreadPoolEnqueue`|61|Element roboczy został poddany do kolejki w kolejce puli wątków.|

 W poniższej tabeli przedstawiono dane zdarzenia

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`WorkID`|`win:Pointer`|Wskaźnik na żądanie służbowe.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="threadpooldequeue-event"></a>Zdarzenie ThreadPoolDequeue

 W poniższej tabeli przedstawiono słowo kluczowe i poziom.

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`ThreadingKeyword` 0x10000|Verbose (5)

 W poniższej tabeli przedstawiono informacje o zdarzeniu.

|Zdarzenie|Identyfikator zdarzenia|Opis|
|-----------|--------------|-----------------|
|`ThreadPoolDequeue`|62|Element roboczy został usunięty z kolejki puli wątków.|

 W poniższej tabeli przedstawiono dane zdarzenia

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`WorkID`|`win:Pointer`|Wskaźnik na żądanie służbowe.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="threadpoolioenqueue-event"></a>Zdarzenie ThreadPoolIOEnqueue

 W poniższej tabeli przedstawiono słowo kluczowe i poziom.

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`ThreadingKeyword` 0x10000|Verbose (5)

 W poniższej tabeli przedstawiono informacje o zdarzeniu.

|Zdarzenie|Identyfikator zdarzenia|Opis|
|-----------|--------------|-----------------|
|`ThreadPoolIOEnqueue`|63|Wątek enqueues powiadomienie o ukończeniu operacji we/wy po wystąpieniu asynchronicznej operacji we/wy.|

 W poniższej tabeli przedstawiono dane zdarzenia

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`NativeOverlapped`|`win:Pointer`|Zarezerwowane do użytku wewnętrznego.|
|`Overlapped`|`win:Pointer`|Zarezerwowane do użytku wewnętrznego.|
|`MultiDequeues`|`win:Boolean`|Zarezerwowane do użytku wewnętrznego.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="threadpooliodequeue-event"></a>Zdarzenie ThreadPoolIODequeue

 W poniższej tabeli przedstawiono słowo kluczowe i poziom.

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`ThreadingKeyword` 0x10000|Verbose (5)

 W poniższej tabeli przedstawiono informacje o zdarzeniu.

|Zdarzenie|Identyfikator zdarzenia|Opis|
|-----------|--------------|-----------------|
|`ThreadPoolIODequeue`|64|Wątek usuwa powiadomienie o ukończeniu operacji we/wy.|

 W poniższej tabeli przedstawiono dane zdarzenia

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`NativeOverlapped`|`win:Pointer`|Zarezerwowane do użytku wewnętrznego.|
|`Overlapped`|`win:Pointer`|Zarezerwowane do użytku wewnętrznego.|
|`MultiDequeues`|`win:Boolean`|Zarezerwowane do użytku wewnętrznego.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="threadpooliopack-event"></a>Zdarzenie ThreadPoolIOPack

 W poniższej tabeli przedstawiono słowo kluczowe i poziom.

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`ThreadingKeyword` 0x10000|Verbose (5)|

 W poniższej tabeli przedstawiono informacje o zdarzeniu.

|Zdarzenie|Identyfikator zdarzenia|Opis|
|-----------|--------------|-----------------|
|`ThreadPoolIOPack`|65|Jest wywoływany pakiet operacji we/wy nakładający się na siebie.|

 W poniższej tabeli przedstawiono dane zdarzenia

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`NativeOverlapped`|`win:Pointer`|Zarezerwowane do użytku wewnętrznego.|
|`Overlapped`|`win:Pointer`|Zarezerwowane do użytku wewnętrznego.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="threadcreating-event"></a>Zdarzenie ThreadCreating

 W poniższej tabeli przedstawiono słowa kluczowe i poziom.

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`ThreadingKeyword` 0x10000|Informacyjny (4)|

 W poniższej tabeli przedstawiono informacje o zdarzeniu.

|Zdarzenie|Identyfikator zdarzenia|Opis|
|----------------|---------------|-----------------|
|`ThreadCreating`|70|Utworzono wątek.|

 W poniższej tabeli przedstawiono dane zdarzenia.

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`ID`|`win:Pointer`|Identyfikator wątku|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="threadrunning-event"></a>Zdarzenie ThreadRunning

 W poniższej tabeli przedstawiono słowa kluczowe i poziom.

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`ThreadingKeyword` 0x10000|Informacyjny (4)|

 W poniższej tabeli przedstawiono informacje o zdarzeniu.

|Zdarzenie|Identyfikator zdarzenia|Opis|
|----------------|---------------|-----------------|
|`ThreadRunning`|71|Wątek został uruchomiony.|

 W poniższej tabeli przedstawiono dane zdarzenia.

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`ID`|`win:Pointer`|Identyfikator wątku|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|
