---
title: Zdarzenia środowiska uruchomieniowego modułu ładującego i spinacza
description: Zobacz zdarzenia środowiska uruchomieniowego platformy .NET, które zbierają informacje diagnostyczne specyficzne dla zdarzeń modułu ładującego i programu Binder, które zbierają informacje dotyczące modułu ładującego zestawy i programu Binder.
ms.date: 11/13/2020
ms.topic: reference
helpviewer_keywords:
- Assembly Loader events (CoreCLR)
- Assembly Binder events (CoreCLR)
- ETW, EventPipe, LTTng assembly loader and binder events (CoreCLR)
ms.openlocfilehash: 2284c580482f6b93a77f44649225ff7e5485666a
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96590036"
---
# <a name="net-runtime-loader-and-binder-events"></a>Zdarzenia modułu ładującego i spinacza środowiska uruchomieniowego .NET

Te zdarzenia zbierają informacje dotyczące ładowania i zwalniania zestawów i modułów. Aby uzyskać więcej informacji na temat korzystania z tych zdarzeń w celach diagnostycznych, zobacz [Rejestrowanie i śledzenie aplikacji .NET](../../core/diagnostics/logging-tracing.md) .

|Słowo kluczowe do podniesienia zdarzenia|Zdarzenie|Poziom|
|-----------------------------------|-----------|-----------|
|`LoaderKeyword` 0x8|`DomainModuleLoad_V1`|Informacyjny (4)|

|Zdarzenie|Identyfikator zdarzenia|Opis|
|-----------|--------------|-----------------|
|`DomainModuleLoad_V1`|151|Uruchamiany, gdy moduł jest ładowany dla domeny aplikacji.|

## <a name="moduleload_v2-event"></a>Zdarzenie ModuleLoad_V2

|Słowo kluczowe do podniesienia zdarzenia|Zdarzenie|Poziom|
|-----------------------------------|-----------|-----------|
|`LoaderKeyword` 0x8|`DomainModuleLoad_V1`|Informacyjny (4)|

|Zdarzenie|Identyfikator zdarzenia|Opis|
|-----------|--------------|-----------------|
|`ModuleLoad_V2`|152|Uruchamiany, gdy moduł jest ładowany w okresie istnienia procesu.|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`ModuleID`|`win:UInt64`|Unikatowy identyfikator modułu.|
|`AssemblyID`|`win:UInt64`|Identyfikator zestawu, w którym znajduje się ten moduł.|
|`ModuleFlags`|`win:UInt32`|0x1: moduł neutralny dla domeny.<br /><br /> 0x2: moduł ma obraz natywny.<br /><br /> 0x4: moduł dynamiczny.<br /><br /> 0x8: moduł manifestu.|
|`Reserved1`|`win:UInt32`|Pole zastrzeżone.|
|`ModuleILPath`|`win:UnicodeString`|Ścieżka obrazu wspólnego języka pośredniego (CIL) dla modułu lub nazwy modułu dynamicznego, jeśli jest to zestaw dynamiczny (zakończony zerem).|
|`ModuleNativePath`|`win:UnicodeString`|Ścieżka do obrazu natywnego modułu, jeśli jest obecny (zakończony zerem).|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia CLR lub CoreCLR.|
|`ManagedPdbSignature`|`win:GUID`|Sygnatura identyfikatora GUID programu Managed Database (PDB), która jest zgodna z tym modułem.|
|`ManagedPdbAge`|`win:UInt32`|Numer wieku zapisany w zarządzanym pliku PDB, który jest zgodny z tym modułem.|
|`ManagedPdbBuildPath`|`win:UnicodeString`|Ścieżka do lokalizacji, w której został skompilowany zarządzany plik PDB zgodny z tym modułem. W niektórych przypadkach może to być nazwa pliku.|
|`NativePdbSignature`|`win:GUID`|Podpis GUID pliku PDB (Native Image Generator), który jest zgodny z tym modułem, jeśli ma zastosowanie.|
|`NativePdbAge`|`win:UInt32`|Numer wieku zapisany w pliku PDB programu NGen, który jest zgodny z tym modułem, jeśli ma zastosowanie.|
|`NativePdbBuildPath`|`win:UnicodeString`|Ścieżka do lokalizacji, w której został skompilowany plik PDB programu NGen pasujący do tego modułu, jeśli ma zastosowanie. W niektórych przypadkach może to być nazwa pliku.|

## <a name="moduleunload_v2-event"></a>Zdarzenie ModuleUnload_V2

|Słowo kluczowe do podniesienia zdarzenia|Zdarzenie|Poziom|
|-----------------------------------|-----------|-----------|
|`LoaderKeyword` 0x8|`DomainModuleLoad_V1`|Informacyjny (4)|

|Zdarzenie|Identyfikator zdarzenia|Opis|
|-----------|--------------|-----------------|
|`ModuleUnload_V2`|153|Uruchamiany, gdy moduł zostanie zwolniony w okresie istnienia procesu.|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`ModuleID`|`win:UInt64`|Unikatowy identyfikator modułu.|
|`AssemblyID`|`win:UInt64`|Identyfikator zestawu, w którym znajduje się ten moduł.|
|`ModuleFlags`|`win:UInt32`|0x1: moduł neutralny dla domeny.<br /><br /> 0x2: moduł ma obraz natywny.<br /><br /> 0x4: moduł dynamiczny.<br /><br /> 0x8: moduł manifestu.|
|`Reserved1`|`win:UInt32`|Pole zastrzeżone.|
|`ModuleILPath`|`win:UnicodeString`|Ścieżka obrazu wspólnego języka pośredniego (CIL) dla modułu lub nazwy modułu dynamicznego, jeśli jest to zestaw dynamiczny (zakończony zerem).|
|`ModuleNativePath`|`win:UnicodeString`|Ścieżka do obrazu natywnego modułu, jeśli jest obecny (zakończony zerem).|
|`ClrInstanceID`|``win:UInt16``|Unikatowy identyfikator wystąpienia CLR lub CoreCLR.|
|`ManagedPdbSignature`|`win:GUID`|Sygnatura identyfikatora GUID programu Managed Database (PDB), która jest zgodna z tym modułem.|
|`ManagedPdbAge`|`win:UInt32`|Numer wieku zapisany w zarządzanym pliku PDB, który jest zgodny z tym modułem.|
|`ManagedPdbBuildPath`|`win:UnicodeString`|Ścieżka do lokalizacji, w której został skompilowany zarządzany plik PDB zgodny z tym modułem. W niektórych przypadkach może to być nazwa pliku.|
|`NativePdbSignature`|`win:GUID`|Podpis GUID pliku PDB (Native Image Generator), który jest zgodny z tym modułem, jeśli ma zastosowanie.|
|`NativePdbAge`|`win:UInt32`|Numer wieku zapisany w pliku PDB programu NGen, który jest zgodny z tym modułem, jeśli ma zastosowanie.|
|`NativePdbBuildPath`|`win:UnicodeString`|Ścieżka do lokalizacji, w której został skompilowany plik PDB programu NGen pasujący do tego modułu, jeśli ma zastosowanie. W niektórych przypadkach może to być nazwa pliku.|

## <a name="moduledcstart_v2-event"></a>Zdarzenie ModuleDCStart_V2

|Słowo kluczowe do podniesienia zdarzenia|Zdarzenie|Poziom|
|-----------------------------------|-----------|-----------|
|`LoaderKeyword` 0x8|`DomainModuleLoad_V1`|Informacyjny (4)

|Zdarzenie|Identyfikator zdarzenia|Opis
|-----------|--------------|-----------------|
|`ModuleDCStart_V2`|153|Wylicza moduły podczas uruchamiania.|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`ModuleID`|`win:UInt64`|Unikatowy identyfikator modułu.|
|`AssemblyID`|`win:UInt64`|Identyfikator zestawu, w którym znajduje się ten moduł.|
|`ModuleFlags`|`win:UInt32`|0x1: moduł neutralny dla domeny.<br /><br /> 0x2: moduł ma obraz natywny.<br /><br /> 0x4: moduł dynamiczny.<br /><br /> 0x8: moduł manifestu.|
|`Reserved1`|`win:UInt32`|Pole zastrzeżone.|
|`ModuleILPath`|`win:UnicodeString`|Ścieżka obrazu wspólnego języka pośredniego (CIL) dla modułu lub nazwy modułu dynamicznego, jeśli jest to zestaw dynamiczny (zakończony zerem).|
|`ModuleNativePath`|`win:UnicodeString`|Ścieżka do obrazu natywnego modułu, jeśli jest obecny (zakończony zerem).|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia CLR lub CoreCLR.|
|`ManagedPdbSignature`|`win:GUID`|Sygnatura identyfikatora GUID programu Managed Database (PDB), która jest zgodna z tym modułem.|
|`ManagedPdbAge`|`win:UInt32`|Numer wieku zapisany w zarządzanym pliku PDB, który jest zgodny z tym modułem.|
|`ManagedPdbBuildPath`|`win:UnicodeString`|Ścieżka do lokalizacji, w której został skompilowany zarządzany plik PDB zgodny z tym modułem. W niektórych przypadkach może to być nazwa pliku.|
|`NativePdbSignature`|`win:GUID`|Podpis GUID pliku PDB (Native Image Generator), który jest zgodny z tym modułem, jeśli ma zastosowanie.|
|`NativePdbAge`|`win:UInt32`|Numer wieku zapisany w pliku PDB programu NGen, który jest zgodny z tym modułem, jeśli ma zastosowanie.|
|`NativePdbBuildPath`|`win:UnicodeString`|Ścieżka do lokalizacji, w której został skompilowany plik PDB programu NGen pasujący do tego modułu, jeśli ma zastosowanie. W niektórych przypadkach może to być nazwa pliku.|

## <a name="moduledcend_v2-event"></a>Zdarzenie ModuleDCEnd_V2

|Słowo kluczowe do podniesienia zdarzenia|Zdarzenie|Poziom|
|-----------------------------------|-----------|-----------|
|`LoaderKeyword` 0x8|`DomainModuleLoad_V1`|Informacyjny (4)|

|Zdarzenie|Identyfikator zdarzenia|Opis|
|-----------|--------------|-----------------|
|`ModuleDCEnd_V2`|154|Wylicza moduły podczas końcowego uwalniania.|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`ModuleID`|`win:UInt64`|Unikatowy identyfikator modułu.|
|`AssemblyID`|`win:UInt64`|Identyfikator zestawu, w którym znajduje się ten moduł.|
|`ModuleFlags`|`win:UInt32`|0x1: moduł neutralny dla domeny.<br /><br /> 0x2: moduł ma obraz natywny.<br /><br /> 0x4: moduł dynamiczny.<br /><br /> 0x8: moduł manifestu.|
|`Reserved1`|`win:UInt32`|Pole zastrzeżone.|
|`ModuleILPath`|`win:UnicodeString`|Ścieżka obrazu wspólnego języka pośredniego (CIL) dla modułu lub nazwy modułu dynamicznego, jeśli jest to zestaw dynamiczny (zakończony zerem).|
|`ModuleNativePath`|`win:UnicodeString`|Ścieżka do obrazu natywnego modułu, jeśli jest obecny (zakończony zerem).|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia CLR lub CoreCLR.|
|`ManagedPdbSignature`|`win:GUID`|Sygnatura identyfikatora GUID programu Managed Database (PDB), która jest zgodna z tym modułem.|
|`ManagedPdbAge`|`win:UInt32`|Numer wieku zapisany w zarządzanym pliku PDB, który jest zgodny z tym modułem.|
|`ManagedPdbBuildPath`|`win:UnicodeString`|Ścieżka do lokalizacji, w której został skompilowany zarządzany plik PDB zgodny z tym modułem. W niektórych przypadkach może to być nazwa pliku.|
|`NativePdbSignature`|`win:GUID`|Podpis GUID pliku PDB (Native Image Generator), który jest zgodny z tym modułem, jeśli ma zastosowanie.|
|`NativePdbAge`|`win:UInt32`|Numer wieku zapisany w pliku PDB programu NGen, który jest zgodny z tym modułem, jeśli ma zastosowanie.|
|`NativePdbBuildPath`|`win:UnicodeString`|Ścieżka do lokalizacji, w której został skompilowany plik PDB programu NGen pasujący do tego modułu, jeśli ma zastosowanie. W niektórych przypadkach może to być nazwa pliku.|

## <a name="assemblyload_v1-event"></a>Zdarzenie AssemblyLoad_V1

|Słowo kluczowe do podniesienia zdarzenia|Zdarzenie|Poziom|
|-----------------------------------|-----------|-----------|
|`LoaderKeyword` 0x8|`DomainModuleLoad_V1`|Informacyjny (4)|

|Zdarzenie|Identyfikator zdarzenia|Opis|
|-----------|--------------|-----------------|
|`AssemblyLoad_V1`|154|Uruchamiany po załadowaniu zestawu.|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`AssemblyID`|`win:UInt64`|Unikatowy identyfikator zestawu.|
|`AppDomainID`|`win:UInt64`|Identyfikator domeny tego zestawu.|
|`BindingID`|`win:UInt64`|Identyfikator, który jednoznacznie identyfikuje powiązanie zestawu.|
|`AssemblyFlags`|`win:UInt32`|0x1: zestaw neutralny dla domeny.<br /><br /> 0x2: zestaw dynamiczny.<br /><br /> 0x4: zestaw ma obraz natywny.<br /><br /> 0x8: zestaw kolekcjonowany.|
|`AssemblyName`|`win:UnicodeString`|W pełni kwalifikowana nazwa zestawu.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.

## <a name="assemblyunload_v1-event"></a>Zdarzenie AssemblyUnload_V1

|Słowo kluczowe do podniesienia zdarzenia|Zdarzenie|Poziom|
|-----------------------------------|-----------|-----------|
|`LoaderKeyword` 0x8|`DomainModuleLoad_V1`|Informacyjny (4)|

|Zdarzenie|Identyfikator zdarzenia|Opis|
|-----------|--------------|-----------------|
|`FireAssemblyUnload_V1`|155|Uruchamiany po załadowaniu zestawu.|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`AssemblyID`|`win:UInt64`|Unikatowy identyfikator zestawu.|
|`AppDomainID`|`win:UInt64`|Identyfikator domeny tego zestawu.|
|`BindingID`|`win:UInt64`|Identyfikator, który jednoznacznie identyfikuje powiązanie zestawu.|
|`AssemblyFlags`|`win:UInt32`|0x1: zestaw neutralny dla domeny.<br /><br /> 0x2: zestaw dynamiczny.<br /><br /> 0x4: zestaw ma obraz natywny.<br /><br /> 0x8: zestaw kolekcjonowany.|
|`AssemblyName`|`win:UnicodeString`|W pełni kwalifikowana nazwa zestawu.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="assemblydcstart_v1-event"></a>Zdarzenie AssemblyDCStart_V1

|Słowo kluczowe do podniesienia zdarzenia|Zdarzenie|Poziom|
|-----------------------------------|-----------|-----------|
|`LoaderKeyword` 0x8|`DomainModuleLoad_V1`|Informacyjny (4)|

|Zdarzenie|Identyfikator zdarzenia|Opis|
|-----------|--------------|-----------------|
|`AssemblyDCStart_V1`|155|Wylicza zestawy w trakcie początkowego uwalniania.|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`AssemblyID`|`win:UInt64`|Unikatowy identyfikator zestawu.|
|`AppDomainID`|`win:UInt64`|Identyfikator domeny tego zestawu.|
|`BindingID`|`win:UInt64`|Identyfikator, który jednoznacznie identyfikuje powiązanie zestawu.|
|`AssemblyFlags`|`win:UInt32`|0x1: zestaw neutralny dla domeny.<br /><br /> 0x2: zestaw dynamiczny.<br /><br /> 0x4: zestaw ma obraz natywny.<br /><br /> 0x8: zestaw kolekcjonowany.|
|`AssemblyName`|`win:UnicodeString`|W pełni kwalifikowana nazwa zestawu.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="assemblyloadstart-event"></a>Zdarzenie AssemblyLoadStart

|Słowo kluczowe do podniesienia zdarzenia|Zdarzenie|Poziom|
|-----------------------------------|-----------|-----------|
|`Binder` 0x4|`AssemblyLoadStart`|Informacyjny (4)|

|Zdarzenie|Identyfikator zdarzenia|Opis|
|-----------|--------------|-----------------|
|`AssemblyLoadStart`|290|Zażądano obciążenia zestawu.

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`AssemblyName`|`win:UnicodeString`|Nazwa zestawu.|
|`AssemblyPath`|`win:UnicodeString`|Ścieżka nazwy zestawu.|
|`RequestingAssembly`|`win:UnicodeString`|Nazwa zestawu żądającego ("Parent").|
|`AssemblyLoadContext`|`win:UnicodeString`|Kontekst ładowania zestawu.|
|`RequestingAssemblyLoadContext`|`win:UnicodeString`|Kontekst ładowania zestawu żądającego ("nadrzędny").|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="assemblyloadstop-event"></a>Zdarzenie AssemblyLoadStop

|Słowo kluczowe do podniesienia zdarzenia|Zdarzenie|Poziom|
|-----------------------------------|-----------|-----------|
|`Binder` 0x4|`AssemblyLoadStart`|Informacyjny (4)|

|Zdarzenie|Identyfikator zdarzenia|Opis|
|-----------|--------------|-----------------|
|`AssemblyLoadStart`|291|Zażądano obciążenia zestawu.

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`AssemblyName`|`win:UnicodeString`|Nazwa zestawu.|
|`AssemblyPath`|`win:UnicodeString`|Ścieżka nazwy zestawu.|
|`RequestingAssembly`|`win:UnicodeString`|Nazwa zestawu żądającego ("Parent").|
|`AssemblyLoadContext`|`win:UnicodeString`|Kontekst ładowania zestawu.|
|`RequestingAssemblyLoadContext`|`win:UnicodeString`|Kontekst ładowania zestawu żądającego ("nadrzędny").|
|`Success`|`win:Boolean`|Czy ładowanie zestawu zakończyło się pomyślnie.|
|`ResultAssemblyName`|`win:UnicodeString`|Nazwa załadowanego zestawu.|
|`ResultAssemblyPath`|`win:UnicodeString`|Ścieżka zestawu, z którego została załadowana.|
|`Cached`|`win:UnicodeString`|Czy ładowanie było buforowane.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="resolutionattempted-event"></a>Zdarzenie ResolutionAttempted

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|-----------|
|`Binder` 0x4|Informacyjny (4)|

|Zdarzenie|Identyfikator zdarzenia|Opis|
|-----------|--------------|-----------------|
|`ResolutionAttempted`|292|Zażądano obciążenia zestawu.

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`AssemblyName`|`win:UnicodeString`|Nazwa zestawu.|
|`Stage`|`win:UInt16`|Etap rozwiązywania.<br/><br/>0: Znajdź w obciążeniu.<br/><br/>1: kontekst ładowania zestawu</br><br/>2: zestawy aplikacji.<br/><br/>3: domyślne rezerwy kontekstu ładowania zestawu. <br/><br/>4: Rozwiązywanie zestawu satelickiego. <br/><br/>5: Rozpoznawanie kontekstu ładowania zestawu.<br/><br/>6: Rozpoznawanie zestawu obiektów AppDomain.
|`AssemblyLoadContext`|`win:UnicodeString`|Kontekst ładowania zestawu.|
|`Result`|`win:UInt16`|Wynik próby rozwiązania.<br/><br/>0: sukces<br/><br/>1: zestaw NotFound<br/><br/>2: niezgodna wersja<br/><br/>3: niezgodna nazwa zestawu<br/><br/>4: niepowodzenie<br/><br/>5: wyjątek|
|`ResultAssemblyName`|`win:UnicodeString`|Nazwa zestawu, który został rozwiązany.|
|`ResultAssemblyPath`|`win:UnicodeString`|Ścieżka zestawu, z którego został rozwiązany.|
|`ErrorMessage`|`win:UnicodeString`|Komunikat o błędzie, jeśli wystąpił wyjątek.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="assemblyloadcontextresolvinghandlerinvoked-event"></a>Zdarzenie AssemblyLoadContextResolvingHandlerInvoked

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|-----------|
|`Binder` 0x4|Informacyjny (4)|

|Zdarzenie|Identyfikator zdarzenia|Opis|
|-----------|--------------|-----------------|
|`AssemblyLoadContextResolvingHandlerInvoked`|293|Wywołano procedurę obsługi [AssemblyLoadContext. rozpoznawania](xref:System.Runtime.Loader.AssemblyLoadContext.Resolving) .|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`AssemblyName`|`win:UnicodeString`|Nazwa zestawu.|
|`HandlerName`|`win:UnicodeString`|Nazwa wywoływanej procedury obsługi.|
|`AssemblyLoadContext`|`win:UnicodeString`|Kontekst ładowania zestawu.|
|`ResultAssemblyName`|`win:UnicodeString`|Nazwa zestawu, który został rozwiązany.|
|`ResultAssemblyPath`|`win:UnicodeString`|Ścieżka zestawu, z którego został rozwiązany.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="appdomainassemblyresolvehandlerinvoked-event"></a>Zdarzenie AppDomainAssemblyResolveHandlerInvoked

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|-----------|
|`Binder` 0x4|Informacyjny (4)|

|Zdarzenie|Identyfikator zdarzenia|Opis|
|-----------|--------------|-----------------|
|`AppDomainAssemblyResolveHandlerInvoked`|294|<xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType>Wywołano procedurę obsługi.|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`AssemblyName`|`win:UnicodeString`|Nazwa zestawu.|
|`HandlerName`|`win:UnicodeString`|Nazwa wywoływanej procedury obsługi.|
|`ResultAssemblyName`|`win:UnicodeString`|Nazwa zestawu, który został rozwiązany.|
|`ResultAssemblyPath`|`win:UnicodeString`|Ścieżka zestawu, z którego został rozwiązany.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="assemblyloadfromresolvehandlerinvoked-event"></a>Zdarzenie AssemblyLoadFromResolveHandlerInvoked

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|-----------|
|`Binder` 0x4|Informacyjny (4)|

|Zdarzenie|Identyfikator zdarzenia|Opis|
|-----------|--------------|-----------------|
|`AssemblyLoadFromResolveHandlerInvoked`|295|<xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType>Wywołano procedurę obsługi.|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`AssemblyName`|`win:UnicodeString`|Nazwa zestawu.|
|`IsTrackedLoad`|`win:Boolean`|Czy obciążenie zestawu jest śledzone.|
|`RequestingAssemblyPath`|`win:UnicodeString`|Ścieżka do zestawu żądającego.|
|`ComputedRequestedAssemblyPath`|`win:UnicodeString`|Ścieżka żądanego zestawu.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="knownpathprobed-event"></a>Zdarzenie KnownPathProbed

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|-----------|
|`Binder` 0x4|Informacyjny (4)|

|Zdarzenie|Identyfikator zdarzenia|Opis|
|-----------|--------------|-----------------|
|`KnownPathProbed`|296|Dla zestawu jest sondowana znana ścieżka.|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`FilePath`|`win:UnicodeString`|Ścieżka sondowania.|
|`Source`|`win:UInt16`|Źródło ścieżki sondowania.<br/><br/>0x0: zestawy aplikacji.<br/><br/>0x1: ścieżka obrazu natywnego aplikacji.<br/><br/>0x2: ścieżka aplikacji.</br><br/>0x3: elementy główne zasobów platformy.<br/><br/>0x4: podkatalog satelity.</br>|
|`Result`|`win:UInt32`|Wartość HRESULT dla sondy.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|
