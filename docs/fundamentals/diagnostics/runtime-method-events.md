---
title: Zdarzenia środowiska uruchomieniowego metody
description: Zobacz zdarzenia środowiska uruchomieniowego platformy .NET, które zbierają informacje diagnostyczne specyficzne dla metod, takich jak zdarzenia metody CLR, znacznik metody CLR lub zdarzenia verbose języka CLR i MethodJittingStarted.
ms.date: 11/13/2020
helpviewer_keywords:
- Method events (CoreCLR)
- ETW, EventPipe, LTTng method events (CoreCLR)
ms.openlocfilehash: f9d08efa420670cf7a8c863f115ff270998f2dca
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "96589991"
---
# <a name="net-runtime-method-events"></a>Zdarzenia metody środowiska uruchomieniowego .NET

Te zdarzenia zbierają informacje, które są specyficzne dla metod. Ładunek tych zdarzeń jest wymagany do rozpoznawania symboli. Ponadto te zdarzenia zapewniają przydatne informacje, takie jak metody, które są ładowane i zwalniane. Aby uzyskać więcej informacji na temat korzystania z tych zdarzeń w celach diagnostycznych, zobacz [Rejestrowanie i śledzenie aplikacji .NET](../../core/diagnostics/logging-tracing.md) .

Wszystkie zdarzenia metody mają poziom "informacyjny (4)". Wszystkie zdarzenia verbose metody mają poziom "verbose (5)".

Wszystkie zdarzenia metod są wywoływane za pomocą słowa `JITKeyword` kluczowego (0x10) lub `NGenKeyword` słowa kluczowego (0x20) w ramach dostawcy środowiska uruchomieniowego, lub `JitRundownKeyword` (0x10) lub `NGENRundownKeyword` (0x20) w ramach dostawcy uwalniania.

Wersja V2 tych zdarzeń zawiera ReJITID, a wersje V1 nie są.

## <a name="methodload_v1-event"></a>Zdarzenie MethodLoad_V1

W poniższej tabeli przedstawiono informacje o zdarzeniu:

|Zdarzenie|Identyfikator zdarzenia|Opis|
|-----------|--------------|-----------------|
|`MethodLoad_V1`|141|Uruchamiany, gdy metoda jest załadowana w czasie just-in-Time (załadowano JIT) lub obraz NGEN zostanie załadowany. Metody dynamiczne i ogólne nie używają tej wersji do ładowania metod. Pomocników JIT nigdy nie używają tej wersji.|

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`JITKeyword` (0x10) dostawca środowiska uruchomieniowego|Informacyjny (4)|
|`NGenKeyword` (0x20) dostawca środowiska uruchomieniowego|Informacyjny (4)|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`MethodID`|`win:UInt64`|Unikatowy identyfikator metody. W przypadku metod pomocniczych JIT jest ustawiony na adres początkowy metody.|
|`ModuleID`|`win:UInt64`|Identyfikator modułu, do którego należy ta metoda (0 dla pomocników JIT).|
|`MethodStartAddress`|`win:UInt64`|Adres początkowy metody.|
|`MethodSize`|`win:UInt32`|Rozmiar metody.|
|`MethodToken`|`win:UInt32`|0 w przypadku metod dynamicznych i pomocników JIT.|
|`MethodFlags`|`win:UInt32`|0x1: metoda dynamiczna.<br /><br /> 0x2: Metoda ogólna.<br /><br /> 0x4: Metoda kodu skompilowana przez JIT (w przeciwnym razie kod natywnego obrazu NGEN).<br /><br /> 0x8: metoda pomocnika.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="methodload_v2-event"></a>Zdarzenie MethodLoad_V2

|Zdarzenie|Identyfikator zdarzenia|Opis|
|----------------|---------------|-----------------|
|`MethodLoad_V2`|141|Uruchamiany, gdy metoda jest załadowana w czasie just-in-Time (załadowano JIT) lub obraz NGEN zostanie załadowany. Metody dynamiczne i ogólne nie używają tej wersji do ładowania metod. Pomocników JIT nigdy nie używają tej wersji.|

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`JITKeyword` (0x10) dostawca środowiska uruchomieniowego|Informacyjny (4)|
|`NGenKeyword` (0x20) dostawca środowiska uruchomieniowego|Informacyjny (4)|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`MethodID`|`win:UInt64`|Unikatowy identyfikator metody. W przypadku metod pomocniczych JIT jest ustawiony na adres początkowy metody.|
|`ModuleID`|`win:UInt64`|Identyfikator modułu, do którego należy ta metoda (0 dla pomocników JIT).|
|`MethodStartAddress`|`win:UInt64`|Adres początkowy metody.|
|`MethodSize`|`win:UInt32`|Rozmiar metody.|
|`MethodToken`|`win:UInt32`|0 w przypadku metod dynamicznych i pomocników JIT.|
|`MethodFlags`|`win:UInt32`|0x1: metoda dynamiczna.<br /><br /> 0x2: Metoda ogólna.<br /><br /> 0x4: Metoda kodu skompilowana przez JIT (w przeciwnym razie kod natywnego obrazu NGEN).<br /><br /> 0x8: metoda pomocnika.|
|`ReJITID`|`win:UInt64`|ReJIT identyfikator metody.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="methodunload_v1-event"></a>Zdarzenie MethodUnLoad_V1

|Zdarzenie|Identyfikator zdarzenia|Opis|
|----------------|---------------|-----------------|
|`MethodUnLoad_V1`|142|Uruchamiany, gdy moduł jest zwolniony, lub domena aplikacji jest niszczona. Metody dynamiczne nigdy nie używają tej wersji do zwalniania metod.|

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`JITKeyword` 0x10|Informacyjny (4)|
|`NGenKeyword` 0x20|Informacyjny (4)|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`MethodID`|`win:UInt64`|Unikatowy identyfikator metody. W przypadku metod pomocniczych JIT jest ustawiony na adres początkowy metody.|
|`ModuleID`|`win:UInt64`|Identyfikator modułu, do którego należy ta metoda (0 dla pomocników JIT).|
|`MethodStartAddress`|`win:UInt64`|Adres początkowy metody.|
|`MethodSize`|`win:UInt32`|Rozmiar metody.|
|`MethodToken`|`win:UInt32`|0 w przypadku metod dynamicznych i pomocników JIT.|
|`MethodFlags`|`win:UInt32`|0x1: metoda dynamiczna.<br /><br /> 0x2: Metoda ogólna.<br /><br /> 0x4: Metoda kodu skompilowana przez JIT (w przeciwnym razie kod natywnego obrazu NGEN).<br /><br /> 0x8: metoda pomocnika.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="methodunload_v2-event"></a>Zdarzenie MethodUnLoad_V2

|Zdarzenie|Identyfikator zdarzenia|Opis|
|----------------|---------------|-----------------|
|`MethodUnLoad_V2`|142|Uruchamiany, gdy moduł jest zwolniony, lub domena aplikacji jest niszczona. Metody dynamiczne nigdy nie używają tej wersji do zwalniania metod.|

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`JITKeyword` 0x10|Informacyjny (4)|
|`NGenKeyword` 0x20|Informacyjny (4)|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`MethodID`|`win:UInt64`|Unikatowy identyfikator metody. W przypadku metod pomocniczych JIT jest ustawiony na adres początkowy metody.|
|`ModuleID`|`win:UInt64`|Identyfikator modułu, do którego należy ta metoda (0 dla pomocników JIT).|
|`MethodStartAddress`|`win:UInt64`|Adres początkowy metody.|
|`MethodSize`|`win:UInt32`|Rozmiar metody.|
|`MethodToken`|`win:UInt32`|0 w przypadku metod dynamicznych i pomocników JIT.|
|`MethodFlags`|`win:UInt32`|0x1: metoda dynamiczna.<br /><br /> 0x2: Metoda ogólna.<br /><br /> 0x4: Metoda kodu skompilowana przez JIT (w przeciwnym razie kod natywnego obrazu NGEN).<br /><br /> 0x8: metoda pomocnika.|
|`ReJITID`|`win:UInt64`|ReJIT identyfikator metody.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="r2rgetentrypoint-event"></a>Zdarzenie R2RGetEntryPoint

|Zdarzenie|Identyfikator zdarzenia|Opis|
|----------------|---------------|-----------------|
|`R2RGetEntryPoint`|159|Uruchamiany po zakończeniu wyszukiwania punktu wejścia R2R.|

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`JITKeyword` 0x10 |Informacyjny (4)|
|`NGenKeyword` 0x20 |Informacyjny (4)|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`MethodID`|`win:UInt64`|Unikatowy identyfikator metody R2R.|
|`MethodNamespace`|`win:UnicodeString`|Przestrzeń nazw metody, która ma być wyszukiwana.|
|`MethodName`|`win:UnicodeString`|Nazwa wyszukiwanej metody.|
|`MethodSignature`|`win:UnicodeString`|Sygnatura metody (rozdzielana przecinkami lista nazw typów).|
|`EntryPoint`|`win:UInt64`|Wskaźnik do punktu wejścia metody R2R|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="r2rgetentrypointstart-event"></a>Zdarzenie R2RGetEntryPointStart

|Zdarzenie|Identyfikator zdarzenia|Opis|
|----------------|---------------|-----------------|
|`R2RGetEntryPointStart`|160|Uruchamiany po rozpoczęciu wyszukiwania punktu wejścia R2R.|

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`JITKeyword` 0x10 |Informacyjny (4)|
|`NGenKeyword` 0x20 |Informacyjny (4)|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`MethodID`|`win:UInt64`|Unikatowy identyfikator metody R2R.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="methodloadverbose_v1-event"></a>Zdarzenie MethodLoadVerbose_V1

|Zdarzenie|Identyfikator zdarzenia|Opis|
|-----------|--------------|-----------------|
|`MethodLoadVerbose_V1`|143|Uruchamiany, gdy metoda jest załadowana przy użyciu JIT lub jest ładowany obraz NGEN. Metody dynamiczne i ogólne zawsze używają tej wersji do ładowania metod. Pomocników JIT zawsze używają tej wersji.|

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`JITKeyword` 0x10 |Informacyjny (4)|
|`NGenKeyword` 0x20 |Informacyjny (4)|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`MethodID`|`win:UInt64`|Unikatowy identyfikator metody. Dla metod pomocniczych JIT Ustaw adres początkowy metody.|
|`ModuleID`|`win:UInt64`|Identyfikator modułu, do którego należy ta metoda (0 dla pomocników JIT).|
|`MethodStartAddress`|`win:UInt64`|Adres początkowy.|
|`MethodSize`|`win:UInt32`|Długość metody.|
|`MethodToken`|`win:UInt32`|0 w przypadku metod dynamicznych i pomocników JIT.|
|`MethodFlags`|`win:UInt32`|0x1: metoda dynamiczna.<br /><br /> 0x2: Metoda ogólna.<br /><br /> 0x4: Metoda skompilowana JIT (w przeciwnym razie wygenerowana przez NGen.exe)<br /><br /> 0x8: metoda pomocnika.|
|`MethodNameSpace`|`win:UnicodeString`|Pełna nazwa przestrzeni nazw skojarzona z metodą.|
|`MethodName`|`win:UnicodeString`|Pełna nazwa klasy skojarzona z metodą.|
|`MethodSignature`|`win:UnicodeString`|Sygnatura metody (rozdzielana przecinkami lista nazw typów).|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="methodloadverbose_v2-event"></a>Zdarzenie MethodLoadVerbose_V2

|Zdarzenie|Identyfikator zdarzenia|Opis|
|-----------|--------------|-----------------|
|`MethodLoadVerbose_V1`|143|Uruchamiany, gdy metoda jest załadowana przy użyciu JIT lub jest ładowany obraz NGEN. Metody dynamiczne i ogólne zawsze używają tej wersji do ładowania metod. Pomocników JIT zawsze używają tej wersji.|

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`JITKeyword` 0x10 |Informacyjny (4)|
|`NGenKeyword` 0x20 |Informacyjny (4)|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`MethodID`|`win:UInt64`|Unikatowy identyfikator metody. Dla metod pomocniczych JIT Ustaw adres początkowy metody.|
|`ModuleID`|`win:UInt64`|Identyfikator modułu, do którego należy ta metoda (0 dla pomocników JIT).|
|`MethodStartAddress`|`win:UInt64`|Adres początkowy.|
|`MethodSize`|`win:UInt32`|Długość metody.|
|`MethodToken`|`win:UInt32`|0 w przypadku metod dynamicznych i pomocników JIT.|
|`MethodFlags`|`win:UInt32`|0x1: metoda dynamiczna.<br /><br /> 0x2: Metoda ogólna.<br /><br /> 0x4: Metoda skompilowana JIT (w przeciwnym razie wygenerowana przez NGen.exe)<br /><br /> 0x8: metoda pomocnika.|
|`MethodNameSpace`|`win:UnicodeString`|Pełna nazwa przestrzeni nazw skojarzona z metodą.|
|`MethodName`|`win:UnicodeString`|Pełna nazwa klasy skojarzona z metodą.|
|`MethodSignature`|`win:UnicodeString`|Sygnatura metody (rozdzielana przecinkami lista nazw typów).|
|`ReJITID`|`win:UInt64`|ReJIT identyfikator metody.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="methodunloadverbose_v1-event"></a>Zdarzenie MethodUnLoadVerbose_V1

|Zdarzenie|Identyfikator zdarzenia|Opis|
|-----------|--------------|-----------------|
|`MethodUnLoadVerbose_V1`|144|Uruchamiany, gdy metoda dynamiczna jest niszczona, moduł jest zwalniany lub domena aplikacji jest niszczona. Metody dynamiczne zawsze używają tej wersji do zwalniania metod.|

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`JITKeyword` 0x10 |Informacyjny (4)|
|`NGenKeyword` 0x20 |Informacyjny (4)|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`MethodID`|`win:UInt64`|Unikatowy identyfikator metody. Dla metod pomocniczych JIT Ustaw adres początkowy metody.|
|`ModuleID`|`win:UInt64`|Identyfikator modułu, do którego należy ta metoda (0 dla pomocników JIT).|
|`MethodStartAddress`|`win:UInt64`|Adres początkowy.|
|`MethodSize`|`win:UInt32`|Długość metody.|
|`MethodToken`|`win:UInt32`|0 w przypadku metod dynamicznych i pomocników JIT.|
|`MethodFlags`|`win:UInt32`|0x1: metoda dynamiczna.<br /><br /> 0x2: Metoda ogólna.<br /><br /> 0x4: Metoda skompilowana JIT (w przeciwnym razie wygenerowana przez NGen.exe)<br /><br /> 0x8: metoda pomocnika.|
|`MethodNameSpace`|`win:UnicodeString`|Pełna nazwa przestrzeni nazw skojarzona z metodą.|
|`MethodName`|`win:UnicodeString`|Pełna nazwa klasy skojarzona z metodą.|
|`MethodSignature`|`win:UnicodeString`|Sygnatura metody (rozdzielana przecinkami lista nazw typów).|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="methodunloadverbose_v2-event"></a>Zdarzenie MethodUnLoadVerbose_V2

|Zdarzenie|Identyfikator zdarzenia|Opis|
|-----------|--------------|-----------------|
|`MethodUnLoadVerbose_V2`|144|Uruchamiany, gdy metoda dynamiczna jest niszczona, moduł jest zwalniany lub domena aplikacji jest niszczona. Metody dynamiczne zawsze używają tej wersji do zwalniania metod.|

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`JITKeyword` 0x10 |Informacyjny (4)|
|`NGenKeyword` 0x20 |Informacyjny (4)|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`MethodID`|`win:UInt64`|Unikatowy identyfikator metody. Dla metod pomocniczych JIT Ustaw adres początkowy metody.|
|`ModuleID`|`win:UInt64`|Identyfikator modułu, do którego należy ta metoda (0 dla pomocników JIT).|
|`MethodStartAddress`|`win:UInt64`|Adres początkowy.|
|`MethodSize`|`win:UInt32`|Długość metody.|
|`MethodToken`|`win:UInt32`|0 w przypadku metod dynamicznych i pomocników JIT.|
|`MethodFlags`|`win:UInt32`|0x1: metoda dynamiczna.<br /><br /> 0x2: Metoda ogólna.<br /><br /> 0x4: Metoda skompilowana JIT (w przeciwnym razie wygenerowana przez NGen.exe)<br /><br /> 0x8: metoda pomocnika.|
|`MethodNameSpace`|`win:UnicodeString`|Pełna nazwa przestrzeni nazw skojarzona z metodą.|
|`MethodName`|`win:UnicodeString`|Pełna nazwa klasy skojarzona z metodą.|
|`MethodSignature`|`win:UnicodeString`|Sygnatura metody (rozdzielana przecinkami lista nazw typów).|
|`ReJITID`|`win:UInt64`|ReJIT identyfikator metody.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="methodjittingstarted_v1-event"></a>Zdarzenie MethodJittingStarted_V1

W poniższej tabeli przedstawiono słowo kluczowe i poziom:

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`JITKeyword` 0x10 |Verbose (5)|
|`NGenKeyword` 0x20 |Verbose (5)|

|Zdarzenie|Identyfikator zdarzenia|Opis|
|-----------|--------------|-----------------|
|`MethodJittingStarted_V1`|145|Uruchamiany, gdy metoda jest skompilowana w trybie JIT.|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`MethodID`|`win:UInt64`|Unikatowy identyfikator metody.|
|`ModuleID`|`win:UInt64`|Identyfikator modułu, do którego należy ta metoda.|
|`MethodToken`|`win:UInt32`|0 w przypadku metod dynamicznych i pomocników JIT.|
|`MethodILSize`|`win:UInt32`|Rozmiar wspólnego języka pośredniego (CIL) dla metody, która jest kompilowana w trybie JIT.|
|`MethodNameSpace`|`win:UnicodeString`|Pełna nazwa klasy skojarzona z metodą.|
|`MethodName`|`win:UnicodeString`|Nazwa metody.|
|`MethodSignature`|`win:UnicodeString`|Sygnatura metody (rozdzielana przecinkami lista nazw typów).|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="methodjitinliningsucceeded-event"></a>Zdarzenie MethodJitInliningSucceeded

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`JITTracingKeyword` (0x1000) |Verbose (5)|

|Zdarzenie|Identyfikator zdarzenia|Opis|
|-----------|--------------|-----------------|
|`MethodJitInliningSucceeded`|185|Uruchamiany, gdy metoda została pomyślnie zakreślona przez kompilator JIT.|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`MethodBeingCompiledNamespace`|`win:UnicodeString`|Przestrzeń nazw kompilowanej metody.|
|`MethodBeingCompiledName`|`win:UnicodeString`|Nazwa skompilowanej metody.|
|`MethodBeingCompiledNameSignature`|`win:UnicodeString`|Sygnatura metody (rozdzielana przecinkami lista nazw typów), które są kompilowane.|
|`InlinerNamespace`|`win:UnicodeString`|Przestrzeń nazw ("Parent") metody.|
|`InlinerName`|`win:UnicodeString`|Nazwa metody inline ("Parent").|
|`InlinerNameSignature`|`win:UnicodeString`|Sygnatura metody inline ("Parent") (rozdzielana przecinkami lista nazw typów).|
|`InlineeNamespace`|`win:UnicodeString`|Przestrzeń nazw metody inline ("Child").|
|`InlineeName`|`win:UnicodeString`|Nazwa metody inline ("Child").|
|`InlineeNameSignature`|`win:UnicodeString`|Sygnatura metody inline ("Child") (rozdzielana przecinkami lista nazw typów).|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="methodjitinliningfailed-event"></a>Zdarzenie MethodJitInliningFailed

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`JITTracingKeyword` (0x1000) |Verbose (5)|

|Zdarzenie|Identyfikator zdarzenia|Opis|
|-----------|--------------|-----------------|
|`MethodJitInliningFailed`|192|Uruchamiany, gdy nie powiodło się przekreślenie metody przez kompilator JIT.|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`MethodBeingCompiledNamespace`|`win:UnicodeString`|Przestrzeń nazw kompilowanej metody.|
|`MethodBeingCompiledName`|`win:UnicodeString`|Nazwa skompilowanej metody.|
|`MethodBeingCompiledNameSignature`|`win:UnicodeString`|Sygnatura metody (rozdzielana przecinkami lista nazw typów), które są kompilowane.|
|`InlinerNamespace`|`win:UnicodeString`|Przestrzeń nazw ("Parent") metody.|
|`InlinerName`|`win:UnicodeString`|Nazwa metody inline ("Parent").|
|`InlinerNameSignature`|`win:UnicodeString`|Sygnatura metody inline ("Parent") (rozdzielana przecinkami lista nazw typów).|
|`InlineeNamespace`|`win:UnicodeString`|Przestrzeń nazw metody inline ("Child").|
|`InlineeName`|`win:UnicodeString`|Nazwa metody inline ("Child").|
|`InlineeNameSignature`|`win:UnicodeString`|Sygnatura metody inline ("Child") (rozdzielana przecinkami lista nazw typów).|
|`FailAlways`|`win:Boolean`|Czy metoda jest oznaczona jako nie wbudowania.|
|`FailReason`|`win:UnicodeString`|Nie można wykreślać przyczyny.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="methodjittailcallsucceeded-event"></a>Zdarzenie MethodJitTailCallSucceeded

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`JITTracingKeyword` (0x1000) |Verbose (5)|

|Zdarzenie|Identyfikator zdarzenia|Opis|
|-----------|--------------|-----------------|
|`MethodJitTailCallSucceeded`|192|Wywoływane przez kompilator JIT, gdy metoda może zostać wywołana pomyślnie.|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`MethodBeingCompiledNamespace`|`win:UnicodeString`|Przestrzeń nazw kompilowanej metody.|
|`MethodBeingCompiledName`|`win:UnicodeString`|Nazwa skompilowanej metody.|
|`MethodBeingCompiledNameSignature`|`win:UnicodeString`|Sygnatura metody (rozdzielana przecinkami lista nazw typów), które są kompilowane.|
|`CallerNamespace`|`win:UnicodeString`|Przestrzeń nazw metody wywołującej.|
|`CallerName`|`win:UnicodeString`|Nazwa metody wywołującej.|
|`CallerNameSignature`|`win:UnicodeString`|Sygnatura metody wywołującej (rozdzielana przecinkami lista nazw typów).|
|`CalleeNamespace`|`win:UnicodeString`|Przestrzeń nazw metody wywoływanej.|
|`CalleeName`|`win:UnicodeString`|Nazwa metody wywoływanej.|
|`CalleeNameSignature`|`win:UnicodeString`|Sygnatura metody wywoływanej (rozdzielana przecinkami lista nazw typów).|
|`TailPrefix`|`win:Boolean`|Czy jest instrukcją prefiksu tail.|
|`TailCallType`|`win:UInt32`|Typ wywołania tail.<br/><br/>0: zoptymalizowane wywołanie tail (epilogu + element JMP)<br/><br/>1: cykliczne wywołanie tail (wywołania metody końcowego)<br/><br/>2: wywołanie tailowe wspomagane przez pomocnika|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="methodjittailcallfailed-event"></a>Zdarzenie MethodJitTailCallFailed

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`JITTracingKeyword` (0x1000) |Verbose (5)|

|Zdarzenie|Identyfikator zdarzenia|Opis|
|-----------|--------------|-----------------|
|`MethodJitTailCallFailed`|191|Wywoływane przez kompilator JIT, gdy metoda nie mogła zostać wywołana.|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`MethodBeingCompiledNamespace`|`win:UnicodeString`|Przestrzeń nazw kompilowanej metody.|
|`MethodBeingCompiledName`|`win:UnicodeString`|Nazwa skompilowanej metody.|
|`MethodBeingCompiledNameSignature`|`win:UnicodeString`|Sygnatura metody (rozdzielana przecinkami lista nazw typów), które są kompilowane.|
|`CallerNamespace`|`win:UnicodeString`|Przestrzeń nazw metody wywołującej.|
|`CallerNam`adres|`win:UnicodeString`|Nazwa metody wywołującej.|
|`CallerNameSignature`|`win:UnicodeString`|Sygnatura metody wywołującej (rozdzielana przecinkami lista nazw typów).|
|`CalleeNamespace`|`win:UnicodeString`|Przestrzeń nazw metody wywoływanej.|
|`CalleeName`|`win:UnicodeString`|Nazwa metody wywoływanej.|
|`CalleeNameSignature`|`win:UnicodeString`|Sygnatura metody wywoływanej (rozdzielana przecinkami lista nazw typów).|
|`TailPrefix`|`win:Boolean`|Czy jest instrukcją prefiksu tail.|
|`FailReason`|`win:UnicodeString`|Wywołanie tail przyczyny nie powiodło się.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="methodiltonativemap-event"></a>Zdarzenie MethodILToNativeMap

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`JittedMethodILToNativeMapKeyword` (0x20000) |Verbose (5)|

|Zdarzenie|Identyfikator zdarzenia|Opis|
|----------------|---------------|-----------------|
|`MethodILToNativeMap`|190|Mapuje wydarzenie IL-to-native map dla metod skompilowanych w trybie JIT.|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`MethodID`|`win:UInt64`|Unikatowy identyfikator metody.|
|`ReJITID`|`win:UInt64`|Identyfikator ReJIT metody.|
|`MethodExtent`|`win:UInt8`|Zakres dla metody trybie JIT.|
|`CountOfMapEntries`|`win:UInt8`|Liczba wpisów mapy|
|`ILOffsets`|`win:UInt32`|Przesunięcie IL.|
|`NativeOffsets`|`win:UInt32`|Przesunięcie kodu natywnego.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|
