---
title: Zdarzenia środowiska uruchomieniowego odzyskiwania pamięci
description: Zobacz zdarzenia środowiska uruchomieniowego platformy .NET, które zbierają informacje diagnostyczne specyficzne dla modułu zbierającego elementy bezużyteczne platformy .NET.
ms.date: 11/13/2020
ms.topic: reference
helpviewer_keywords:
- GC events
- garbage collection events (CoreCLR)
- ETW, EventPipe, LTTng garbage collection events (CoreCLR)
ms.openlocfilehash: 2799a93f351baf23ec7a359b0b4b2be5c216dc4d
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "96590000"
---
# <a name="net-runtime-garbage-collection-events"></a>Zdarzenia odzyskiwania pamięci środowiska uruchomieniowego platformy .NET

Te zdarzenia zbierają informacje dotyczące wyrzucania elementów bezużytecznych. Ułatwiają one diagnostykę i debugowanie, w tym określanie, ile razy zostało wykonane wyrzucanie elementów bezużytecznych, ile pamięci zostało zwolnione podczas wyrzucania elementów bezużytecznych itp. Aby uzyskać więcej informacji na temat korzystania z tych zdarzeń w celach diagnostycznych, zobacz [Rejestrowanie i śledzenie aplikacji .NET](../../core/diagnostics/logging-tracing.md) .

## <a name="gcstart_v2-event"></a>Zdarzenie GCStart_V2

W poniższej tabeli przedstawiono słowo kluczowe i poziom:

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`GCKeyword` 0x1|Informacyjny (4)|

W poniższej tabeli przedstawiono informacje o zdarzeniu:

|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|
|-----------|--------------|-----------------|
|`GCStart_V1`|1|Rozpoczęto odzyskiwanie pamięci.|

W poniższej tabeli przedstawiono dane zdarzenia:

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`Count`|`win:UInt32`|*N*-ta kolekcja elementów bezużytecznych.|
|`Depth`|`win:UInt32`|Generacja, która jest zbierana.|
|`Reason`|`win:UInt32`|Dlaczego wyzwolono wyrzucanie elementów bezużytecznych:<br /><br /> `0x0` -Alokacja sterty dla małego obiektu.<br /><br /> `0x1` Wywołano.<br /><br /> `0x2` -Mało pamięci.<br /><br /> `0x3` Ciągiem.<br /><br /> `0x4` -Alokacja sterty dla dużego obiektu.<br /><br /> `0x5` -Brak miejsca (dla sterty małego obiektu).<br /><br /> `0x6` -Brak miejsca (dla sterty dużego obiektu).<br /><br /> `0x7` -Wywołano, ale nie wymuszono blokowania.|
|`Type`|`win:UInt32`|`0x0` -Blokowanie odzyskiwania pamięci wystąpiło poza odzyskiwaniem pamięci w tle.<br /><br /> `0x1` -Wyrzucanie elementów bezużytecznych w tle.<br /><br /> `0x2` -Blokowanie odzyskiwania pamięci wystąpiło podczas odzyskiwania pamięci w tle.|
|`ClrInstanceID`|win: UInt16|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="gcend_v1-event"></a>Zdarzenie GCEnd_V1

W poniższej tabeli przedstawiono słowo kluczowe i poziom:

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`GCKeyword` 0x1|Informacyjny (4)|

W poniższej tabeli przedstawiono informacje o zdarzeniu:

|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|
|-----------|--------------|-----------------|
|`GCEnd_V1`|2|Wyrzucanie elementów bezużytecznych zostało zakończone.|

W poniższej tabeli przedstawiono dane zdarzenia:

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`Count`|`win:UInt32`|*N*-ta kolekcja elementów bezużytecznych.|
|`Depth`|`win:UInt32`|Generacja, która została zebrana.|
|`ClrInstanceID`|win: UInt16|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="gcheapstats_v2-event"></a>Zdarzenie GCHeapStats_V2

W poniższej tabeli przedstawiono słowo kluczowe i poziom:

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`GCKeyword` 0x1|Informacyjny (4)|

W poniższej tabeli przedstawiono informacje o zdarzeniu:

|Zdarzenie|Identyfikator zdarzenia|Opis|
|-----------|--------------|-----------------|
|`GCHeapStats_V2`|4|Pokazuje statystyki sterty na końcu każdego wyrzucania elementów bezużytecznych.|

W poniższej tabeli przedstawiono dane zdarzenia:

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`GenerationSize0`|`win:UInt64`|Rozmiar (w bajtach) pamięci generacji 0.|
|`TotalPromotedSize0`|`win:UInt64`|Liczba bajtów, które są podwyższane z generacji 0 do generacji 1.|
|`GenerationSize1`|`win:UInt64`|Rozmiar (w bajtach) pamięci pierwszej generacji 1.|
|`TotalPromotedSize1`|`win:UInt64`|Liczba bajtów, które są podwyższane z generacji 1 do generacji 2.|
|`GenerationSize2`|`win:UInt64`|Rozmiar (w bajtach) pamięci podnoszącej 2 generacji.|
|`TotalPromotedSize2`|`win:UInt64`|Liczba bajtów, które przeżyły w generacji 2 po ostatniej kolekcji.|
|`GenerationSize3`|`win:UInt64`|Rozmiar sterty dużego obiektu w bajtach.|
|`TotalPromotedSize3`|`win:UInt64`|Liczba bajtów przeczytanych z sterty dużego obiektu po ostatniej kolekcji.|
|`FinalizationPromotedSize`|`win:UInt64`|Łączny rozmiar (w bajtach) obiektów, które są gotowe do finalizacji.|
|`FinalizationPromotedCount`|`win:UInt64`|Liczba obiektów, które są gotowe do finalizacji.|
|`PinnedObjectCount`|`win:UInt32`|Liczba przypiętych (nieruchomych) obiektów.|
|`SinkBlockCount`|`win:UInt32`|Liczba bloków synchronizacji w użyciu.|
|`GCHandleCount`|`win:UInt32`|Liczba dojść do wyrzucania elementów bezużytecznych w użyciu.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|
|`GenerationSize4`|`win:UInt64`|Rozmiar, w bajtach, przypiętej sterty obiektu.|
|`TotalPromotedSize4`|`win:UInt64`|Liczba bajtów, które przeżyły na stercie przypiętych obiektów po ostatniej kolekcji.|

## <a name="gccreatesegment_v1-event"></a>Zdarzenie GCCreateSegment_V1

W poniższej tabeli przedstawiono słowo kluczowe i poziom:

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`GCKeyword` 0x1|Informacyjny (4)|

W poniższej tabeli przedstawiono informacje o zdarzeniu:

|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|
|-----------|--------------|-----------------|
|`GCCreateSegment_V1`|5|Utworzono nowy segment wyrzucania elementów bezużytecznych. Ponadto po włączeniu śledzenia dla procesu, który jest już uruchomiony, to zdarzenie jest zgłaszane dla każdego istniejącego segmentu.|

W poniższej tabeli przedstawiono dane zdarzenia:

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`Address`|`win:UInt64`|Adres segmentu.|
|`Size`|`win:UInt64`|Rozmiar segmentu.|
|`Type`|`win:UInt32`|0x0 — sterta małego obiektu.<br /><br /> 0x1 — sterta dużego obiektu.<br /><br /> 0x2 — sterta tylko do odczytu.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

Należy zauważyć, że rozmiar segmentów przydzielone przez moduł wyrzucania elementów bezużytecznych jest specyficzny dla implementacji i może ulec zmianie w dowolnym momencie, łącznie z okresowymi aktualizacjami. Aplikacja nigdy nie powinna mieć założeń lub zależeć od określonego rozmiaru segmentu ani nie powinna próbować skonfigurować ilości pamięci dostępnej dla alokacji segmentu.

## <a name="gcfreesegment_v1-event"></a>Zdarzenie GCFreeSegment_V1

W poniższej tabeli przedstawiono słowo kluczowe i poziom:

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`GCKeyword` 0x1|Informacyjny (4)|

W poniższej tabeli przedstawiono informacje o zdarzeniu:

|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|
|-----------|--------------|-----------------|
|`GCFreeSegment_V1`|6|Wydano segment wyrzucania elementów bezużytecznych.|

W poniższej tabeli przedstawiono dane zdarzenia:

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`Address`|`win:UInt64`|Adres segmentu.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="gcrestarteebegin_v1-event"></a>Zdarzenie GCRestartEEBegin_V1

W poniższej tabeli przedstawiono słowo kluczowe i poziom:

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`GCKeyword` 0x1|Informacyjny (4)|

W poniższej tabeli przedstawiono informacje o zdarzeniu:

|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|
|-----------|--------------|-----------------|
|`GCRestartEEBegin_V1`|7|Rozpoczęto wznawianie od zawieszenia środowiska uruchomieniowego języka wspólnego.|

To zdarzenie nie zawiera żadnych danych zdarzenia.

## <a name="gcrestarteeend_v1-event"></a>Zdarzenie GCRestartEEEnd_V1

W poniższej tabeli przedstawiono słowo kluczowe i poziom:

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`GCKeyword` 0x1|Informacyjny (4)|

W poniższej tabeli przedstawiono informacje o zdarzeniu:

|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|
|-----------|--------------|-----------------|
|`GCRestartEEEnd_V1`|3|Zakończono wznawianie z zawieszenia środowiska uruchomieniowego języka wspólnego.|

To zdarzenie nie zawiera żadnych danych zdarzenia.

## <a name="gcsuspendeeend_v1-event"></a>Zdarzenie GCSuspendEEEnd_V1

W poniższej tabeli przedstawiono słowo kluczowe i poziom:

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`GCKeyword` 0x1|Informacyjny (4)|

W poniższej tabeli przedstawiono informacje o zdarzeniu:

|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|
|-----------|--------------|-----------------|
|`GCSuspendEEEnd_V1`|8|Koniec zawieszenia aparatu wykonywania na potrzeby wyrzucania elementów bezużytecznych.|

To zdarzenie nie zawiera żadnych danych zdarzenia.

## <a name="gcsuspendeebegin_v1-event"></a>Zdarzenie GCSuspendEEBegin_V1

W poniższej tabeli przedstawiono słowo kluczowe i poziom:

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`GCKeyword` 0x1|Informacyjny (4)|

W poniższej tabeli przedstawiono informacje o zdarzeniu:

|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|
|-----------|--------------|-----------------|
|`GCSuspendEEBegin_V1`|8|Początek zawieszenia aparatu wykonywania na potrzeby wyrzucania elementów bezużytecznych.|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`Count`|`win:UInt32`|*N*-ta kolekcja elementów bezużytecznych.|
|`Reason`|`win:UInt32`|Przyczyna zawieszenia usługi EE.<br/><br/>`0x0`: Wstrzymywanie dla innych<br/><br/>`0x1`: Suspend dla GC.<br/><br/>`0x2`: Wstrzymanie do zamknięcia domeny aplikacji.<br/><br/>`0x3`: Wstrzymywanie do pochylenia kodu.<br/><br/>`0x4`: Wstrzymaj do zamknięcia.<br/><br/>`0x5`: Suspend for Debugger.<br/><br/>`0x6`: Wstrzymaj przygotowanie do przygotowania do odzyskiwania pamięci.<br/><br/>`0x7`: Wstrzymanie do odchylenia debugera|

## <a name="gcallocationtick_v3-event"></a>Zdarzenie GCAllocationTick_V3

W poniższej tabeli przedstawiono słowo kluczowe i poziom:

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`GCKeyword` 0x1|Verbose (4)|

W poniższej tabeli przedstawiono informacje o zdarzeniu:

|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|
|-----------|--------------|-----------------|
|`GCAllocationTick_V3`|10|Za każdym razem przydzielono około 100 KB.|

W poniższej tabeli przedstawiono dane zdarzenia:

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`AllocationAmount`|`win:UInt32`|Rozmiar alokacji w bajtach. Ta wartość jest dokładna dla przydziałów, które są mniejsze niż długość ULONG (4 294 967 295 bajtów). Jeśli alokacja jest większa, to pole zawiera obciętą wartość. Używane `AllocationAmount64` dla bardzo dużych alokacji.|
|`AllocationKind`|`win:UInt32`|`0x0` — Alokacja małego obiektu (alokacja jest w ramach sterty małego obiektu).<br /><br /> `0x1` -Alokacja dużego obiektu (alokacja jest w stosie dużego obiektu).|
|`AllocationAmount64`|`win:UInt64`|Rozmiar alokacji w bajtach. Ta wartość jest dokładna dla bardzo dużych alokacji.|
|`TypeId`|`win:Pointer`|Adres metody. Jeśli istnieje kilka typów obiektów, które zostały przydzieloną w trakcie tego zdarzenia, jest to adres metody, która odnosi się do ostatniego przydzielony obiekt (obiekt, który spowodował przekroczenie 100 KB progu).|
|`TypeName`|`win:UnicodeString`|Nazwa przydzieloną typ. Jeśli istnieje kilka typów obiektów, które zostały przydzieloną w trakcie tego zdarzenia, jest to typ ostatniego przydzielono obiektu (obiektu, który spowodował przekroczenie 100 KB).|
|`HeapIndex`|`win:UInt32`|Sterta, do której został przydzielony obiekt. Ta wartość jest równa 0 (zero) podczas uruchamiania z odzyskiwaniem pamięci stacji roboczej.|
|`Address`|`win:Pointer`|Adres ostatniego przyznanego obiektu.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="gccreateconcurrentthread_v1-event"></a>Zdarzenie GCCreateConcurrentThread_V1

W poniższej tabeli przedstawiono słowo kluczowe i poziom:

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`GCKeyword` 0x1|Informacyjny (4)|
|`ThreadingKeyword` 0x10000|Informacyjny (4)|

W poniższej tabeli przedstawiono informacje o zdarzeniu:

|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|
|-----------|--------------|-----------------|
|`GCCreateConcurrentThread_V1`|11|Utworzono wątek współbieżnego wyrzucania elementów bezużytecznych.|

To zdarzenie nie zawiera żadnych danych zdarzenia.

## <a name="gcterminateconcurrentthread_v1-event"></a>Zdarzenie GCTerminateConcurrentThread_V1

W poniższej tabeli przedstawiono słowo kluczowe i poziom:

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`GCKeyword` 0x1|Informacyjny (4)|
|`ThreadingKeyword` 0x10000|Informacyjny (4)|

W poniższej tabeli przedstawiono informacje o zdarzeniu:

|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|
|-----------|--------------|-----------------|
|`GCTerminateConcurrentThread_V1`|12|Wątek współbieżnego wyrzucania elementów bezużytecznych został zakończony.|

To zdarzenie nie zawiera żadnych danych zdarzenia.

## <a name="gcfinalizersbegin_v1-event"></a>Zdarzenie GCFinalizersBegin_V1

W poniższej tabeli przedstawiono słowo kluczowe i poziom:

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`GCKeyword` 0x1|Informacyjny (4)|

W poniższej tabeli przedstawiono informacje o zdarzeniu:

|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|
|-----------|--------------|-----------------|
|`GCFinalizersBegin_V1`|14|Początek uruchamiania finalizatorów.|

To zdarzenie nie zawiera żadnych danych zdarzenia.

## <a name="gcfinalizersend_v1-event"></a>Zdarzenie GCFinalizersEnd_V1

W poniższej tabeli przedstawiono słowo kluczowe i poziom:

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`GCKeyword` 0x1|Informacyjny (4)|

W poniższej tabeli przedstawiono informacje o zdarzeniu:

|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|
|-----------|--------------|-----------------|
|`GCFinalizersEnd_V1`|13|Koniec uruchomionych finalizatorów.|

W poniższej tabeli przedstawiono dane zdarzenia:

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`Count`|`win:UInt32`|Liczba uruchomionych finalizatorów.|
|`ClrInstanceID`|win: UInt16|Unikatowy identyfikator wystąpienia CLR lub CoreCLR.|

## <a name="setgchandle-event"></a>Zdarzenie SetGCHandle

W poniższej tabeli przedstawiono słowo kluczowe i poziom:

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`GCHandleKeyword` 0x2|Informacyjny (4)|

W poniższej tabeli przedstawiono informacje o zdarzeniu:

|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|
|-----------|--------------|-----------------|
|`SetGCHandle`|30|Dojście GC zostało ustawione.|

W poniższej tabeli przedstawiono dane zdarzenia:

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`HandleID`|`win:Pointer`|Adres przydzielnego dojścia.|
|`ObjectID`|`win:Pointer`|Adres obiektu, którego dojście zostało utworzone.|
|`Kind`|`win:UInt32`|Typ dojścia GC, który został ustawiony. <br /><br />`0x0`: WeakShort <br/><br/>`0x1`: WeakLong <br /><br />`0x2`: Strong <br /><br />`0x3`: Przypięty <br /><br />`0x4`: Zmienna<br /><br />`0x5`: RefCounted <br /><br />`0x6`: Zależne<br /><br />`0x7`: AsyncPinned<br /><br />`0x8`: Dojście SizedRef|
|`Generation`|`win:UInt32`|Generacja obiektu, którego dojście zostało utworzone.|
|`AppDomainID`|`win:UInt64`|Identyfikator domeny aplikacji.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="destroygchandle-event"></a>Zdarzenie DestroyGCHandle

W poniższej tabeli przedstawiono słowo kluczowe i poziom:

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`GCHandleKeyword` 0x2|Informacyjny (4)|

W poniższej tabeli przedstawiono informacje o zdarzeniu:

|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|
|-----------|--------------|-----------------|
|`DestroyGCHandle`|31|Dojście GC zostało zniszczone.|

W poniższej tabeli przedstawiono dane zdarzenia:

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`HandleID`|`win:Pointer`|Adres zniszczonego dojścia.|
|`ClrInstanceID`|win: UInt16|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="pinobjectatgctime-event"></a>Zdarzenie PinObjectAtGCTime

W poniższej tabeli przedstawiono słowo kluczowe i poziom:

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`GCKeyword` 0x1|Verbose (5)|

W poniższej tabeli przedstawiono informacje o zdarzeniu:

|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|
|-----------|--------------|-----------------|
|`PinObjectAtGCTime`|33|Obiekt został przypięty podczas operacji GC.|

W poniższej tabeli przedstawiono dane zdarzenia:

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`HandleID`|`win:Pointer`|Adres dojścia.|
|`ObjectID`|`win:Pointer`|Adres przypiętego obiektu.|
|`ObjectSize`|`win:UInt64`|Rozmiar przypiętego obiektu.|
|`TypeName`|`win:UnicodeString`|Nazwa typu przypiętego obiektu.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="gctriggered-event"></a>Zdarzenie GCTriggered

W poniższej tabeli przedstawiono słowo kluczowe i poziom:

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`GCKeyword` 0x1|Verbose (5)|

W poniższej tabeli przedstawiono informacje o zdarzeniu:

|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|
|-----------|--------------|-----------------|
|`GCTriggered`|33|Wyzwolono wykaz globalny.|

W poniższej tabeli przedstawiono dane zdarzenia:

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`Reason`|`win:UInt32`|Przyczyna wyzwolenia GC.<br/><br/>`0x0`: AllocSmall<br/><br/>`0x1`: Wywołane <br/><br/>`0x2`: LowMemory <br/><br/>`0x3`: Puste <br/><br/>`0x4`: AllocLarge <br/><br/>`0x5`: OutOfSpaceSmallObjectHeap <br/><br/>`0x6`: OutOfSpaceLargeObjectHeap <br/><br/>`0x7`:InducedNoForce <br/><br/>`0x8`: Naprężenie <br/><br/>`0x9`: InducedLowMemory|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="increasememorypressure-event"></a>Zdarzenie IncreaseMemoryPressure

W poniższej tabeli przedstawiono słowo kluczowe i poziom:

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`GCKeyword` 0x1|Informacje (4)|

W poniższej tabeli przedstawiono informacje o zdarzeniu:

|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|
|----------------|---------------|-----------------|
|`IncreaseMemoryPressure`|200|Zwiększono wykorzystanie pamięci.|

W poniższej tabeli przedstawiono dane zdarzenia:

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`ClrInstanceID`|win: UInt16|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="decreasememorypressure-event"></a>Zdarzenie DecreaseMemoryPressure

W poniższej tabeli przedstawiono słowo kluczowe i poziom:

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`GCKeyword` 0x1|Informacje (4)|

W poniższej tabeli przedstawiono informacje o zdarzeniu:

|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|
|----------------|---------------|-----------------|
|`DecreaseMemoryPressure`|201|Obniżono wykorzystanie pamięci.|

W poniższej tabeli przedstawiono dane zdarzenia:

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`BytesFreed`|`win:UInt32`|Bajty zwolnione.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="gcmarkwithtype-event"></a>Zdarzenie GCMarkWithType

W poniższej tabeli przedstawiono słowo kluczowe i poziom:

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`GCKeyword` 0x1|Informacje (4)|

W poniższej tabeli przedstawiono informacje o zdarzeniu:

|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|
|----------------|---------------|-----------------|
|`GCMarkWithType`|202|Element główny GC został oznaczony podczas fazy znacznika GC.|

W poniższej tabeli przedstawiono dane zdarzenia:

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`HeapNum`|`win:UInt32`|Numer sterty.|
|`ClrInstanceID`|win: UInt16|Unikatowy identyfikator wystąpienia elementu CoreCLR.|
|`Type`|`win:UInt32`|Typ główny GC.<br/><br/>`0x0`: Stos<br/><br/>`0x1`: Finalizator<br/><br/>`0x2`: Uchwyt<br/><br/>`0x3`: Starsze<br/><br/>`0x4`: Dojście SizedRef<br/><br/>`0x5`: Przepełnienie<br/><br/>|
|`Bytes`|`win:UInt64`|Liczba bajtów oznaczonych.|

## <a name="gcjoin_v2-event"></a>Zdarzenie GCJoin_V2

W poniższej tabeli przedstawiono słowo kluczowe i poziom:

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`GCKeyword` 0x1|Verbose (5)|

W poniższej tabeli przedstawiono informacje o zdarzeniu:

|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|
|-----------|--------------|-----------------|
|`GCJoin_V2`|203|Przyłączony wątek GC.|

W poniższej tabeli przedstawiono dane zdarzenia:

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`Heap`|`win:UInt32`|Numer sterty|
|`JoinTime`|`win:UInt32`|Wskazuje, czy to zdarzenie jest wyzwalane na początku sprzężenia, czy na końcu sprzężenia (w celu rozpoczęcia dołączania `0x0` `0x1` w celu dołączenia)|
|`JoinType`|`win:UInt32`|Typ sprzężenia. <br/><br/>`0x0`: Ostatnie połączenie<br/><br/>`0x1`: Dołącz <br/><br/>`0x2`: Uruchom ponownie <br/><br/>`0x3`: Pierwsze odwrotne sprzężenie<br/><br/>`0x4`: Odwrotne sprzężenie<br/><br/>|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|
