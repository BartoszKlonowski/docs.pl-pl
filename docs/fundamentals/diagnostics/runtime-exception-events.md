---
title: Zdarzenia środowiska uruchomieniowego wyjątku
description: Zobacz zdarzenia środowiska uruchomieniowego platformy .NET, które zbierają informacje diagnostyczne specyficzne dla wyjątków i obsługi wyjątków.
ms.date: 11/13/2020
ms.topic: reference
helpviewer_keywords:
- exception events (CoreCLR)
- exception handling events (CoreCLR)
- ETW, EventPipe, LTTng exception events (CoreCLR)
ms.openlocfilehash: f4f63c8469f9c734b872ddaec8d1d7f7f0427576
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96590032"
---
# <a name="net-runtime-exception-events"></a>Zdarzenia wyjątków środowiska uruchomieniowego .NET

Te zdarzenia środowiska uruchomieniowego przechwytują informacje o zgłaszanych wyjątkach. Aby uzyskać więcej informacji na temat korzystania z tych zdarzeń w celach diagnostycznych, zobacz [Rejestrowanie i śledzenie aplikacji .NET](../../core/diagnostics/logging-tracing.md) .

## <a name="exceptionthrown_v1-event"></a>Zdarzenie ExceptionThrown_V1

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`ExceptionKeyword` 0x8000|Błąd (1)|

 W poniższej tabeli przedstawiono informacje o zdarzeniach.

|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|
|-----------|--------------|-----------------|
|`ExceptionThrown_V1`|80|Generowany jest wyjątek zarządzany.|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`ExceptionType`|`win:UnicodeString`|Typ wyjątku; na przykład `System.NullReferenceException` .|
|`ExceptionMessage`|`win:UnicodeString`|Rzeczywisty komunikat o wyjątku.|
|`EIPCodeThrow`|`win:Pointer`|Wskaźnik instrukcji, w którym wystąpił wyjątek.|
|`ExceptionHR`|`win:UInt32`|Wyjątek [HRESULT](/openspecs/windows_protocols/ms-erref/0642cb2f-2075-4469-918c-4441e69c548a).|
|`ExceptionFlags`|`win:UInt16`|`0x01`: HasInnerException.<br /><br /> `0x02`: Isnestexception.<br /><br /> `0x04`: IsRethrownException.<br /><br /> `0x08`: IsCorruptedStateException (wskazuje, że stan procesu jest uszkodzony; zobacz [Obsługa wyjątków uszkodzonego stanu](/archive/msdn-magazine/2009/february/clr-inside-out-handling-corrupted-state-exceptions)).<br /><br /> `0x10`: IsCLSCompliant (wyjątek pochodzący z <xref:System.Exception> jest zgodny ze specyfikacją CLS; w przeciwnym razie nie jest zgodny ze specyfikacją CLS).|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia CLR lub CoreCLR.|

## <a name="exceptioncatchstart-event"></a>Zdarzenie ExceptionCatchStart

To zdarzenie jest emitowane po rozpoczęciu procedury obsługi catch o wyjątku zarządzanym.

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`ExceptionKeyword` 0x8000|Informacyjny (4)|

 W poniższej tabeli przedstawiono informacje o zdarzeniach.

|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|
|-----------|--------------|-----------------|
|`ExceptionCatchStart`|250|Wyjątek zarządzany jest obsługiwany przez środowisko uruchomieniowe.|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`EIPCodeThrow`|`win:Pointer`|Wskaźnik instrukcji, w którym wystąpił wyjątek.|
|`MethodID`|`win:Pointer`|Wskaźnik do deskryptora metody na metodzie, w której wystąpił wyjątek.|
|`MethodName`|`win:UnicodeString`|Nazwa metody, w której wystąpił wyjątek.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia CLR lub CoreCLR.|

## <a name="exceptioncatchstop-event"></a>Zdarzenie ExceptionCatchStop

To zdarzenie jest emitowane po zakończeniu obsługi catch o wyjątku zarządzanym.

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`ExceptionKeyword` 0x8000|Informacyjny (4)|

 W poniższej tabeli przedstawiono informacje o zdarzeniach.

|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|
|-----------|--------------|-----------------|
|`ExceptionCatchStop`|251|Wykonano procedurę obsługi catch o wyjątku zarządzanym.|

## <a name="exceptionfinallystart-event"></a>Zdarzenie ExceptionFinallyStart

To zdarzenie jest emitowane po rozpoczęciu obsługi wyjątku zarządzanego finally.

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`ExceptionKeyword` 0x8000|Informacyjny (4)|

 W poniższej tabeli przedstawiono informacje o zdarzeniach.

|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|
|-----------|--------------|-----------------|
|`ExceptionFinallyStart`|252|Wyjątek zarządzany jest obsługiwany przez środowisko uruchomieniowe.|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`EIPCodeThrow`|`win:Pointer`|Wskaźnik instrukcji, w którym wystąpił wyjątek.|
|`MethodID`|`win:Pointer`|Wskaźnik do deskryptora metody na metodzie, w której wystąpił wyjątek.|
|`MethodName`|`win:UnicodeString`|Nazwa metody, w której wystąpił wyjątek.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia CLR lub CoreCLR.|

## <a name="exceptionfinallystop-event"></a>Zdarzenie ExceptionFinallyStop

To zdarzenie jest emitowane po zakończeniu obsługi catch o wyjątku zarządzanym.

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`ExceptionKeyword` 0x8000|Informacyjny (4)|

 W poniższej tabeli przedstawiono informacje o zdarzeniach.

|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|
|-----------|--------------|-----------------|
|`ExceptionFinallyStop`|253|Zakończono procedurę obsługi finally wyjątku zarządzanego.|

## <a name="exceptionfilterstart-event"></a>Zdarzenie ExceptionFilterStart

To zdarzenie jest emitowane po rozpoczęciu filtrowania zarządzanego wyjątku.

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`ExceptionKeyword` 0x8000|Informacyjny (4)|

 W poniższej tabeli przedstawiono informacje o zdarzeniach.

|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|
|-----------|--------------|-----------------|
|`ExceptionFilterStart`|254|Rozpocznie się filtrowanie zarządzanych wyjątków.|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`EIPCodeThrow`|`win:Pointer`|Wskaźnik instrukcji, w którym wystąpił wyjątek.|
|`MethodID`|`win:Pointer`|Wskaźnik do deskryptora metody na metodzie, w której wystąpił wyjątek.|
|`MethodName`|`win:UnicodeString`|Nazwa metody, w której wystąpił wyjątek.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="exceptionfilterstop-event"></a>Zdarzenie ExceptionFilterStop

To zdarzenie jest emitowane po zakończeniu filtrowania zarządzanego wyjątku.

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`ExceptionKeyword` 0x8000|Informacyjny (4)|

 W poniższej tabeli przedstawiono informacje o zdarzeniach.

|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|
|-----------|--------------|-----------------|
|`ExceptionFilteringStart`|255|Zostanie zakończone filtrowanie wyjątków zarządzanych.|

## <a name="exceptionthrownstop-event"></a>Zdarzenie ExceptionThrownStop

To zdarzenie jest emitowane, gdy środowisko uruchomieniowe zakończy obsługę zgłoszonego wyjątku.

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`ExceptionKeyword` 0x8000|Informacyjny (4)|
  
 W poniższej tabeli przedstawiono informacje o zdarzeniach.

|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|
|-----------|--------------|-----------------|
|`ExceptionThrownStop`|256|Zostanie zakończone filtrowanie wyjątków zarządzanych.|
