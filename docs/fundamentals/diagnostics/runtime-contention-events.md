---
title: Monitoruj zdarzenia czasu wykonywania rywalizacji o blokadę
description: Zobacz zdarzenia ETW, które zbierają informacje specyficzne dla rywalizacji o blokadę monitora.
ms.date: 11/13/2020
ms.topic: reference
helpviewer_keywords:
- monitor lock contention events (CoreCLR)
- ETW, EventPipe, LTTng contention events (CoreCLR)
ms.openlocfilehash: 38e5f493d4b223b4839dbd6f814cf656722189b2
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "96589999"
---
# <a name="net-runtime-contention-events"></a>Zdarzenia rywalizacji o środowisko uruchomieniowe platformy .NET

Te zdarzenia środowiska uruchomieniowego przechwytują informacje o rywalizacjach o blokadę monitora, takich jak program `Monitor.Enter` lub słowo kluczowe lock języka C#. Aby uzyskać więcej informacji na temat korzystania z tych zdarzeń w celach diagnostycznych, zobacz [Rejestrowanie i śledzenie aplikacji .NET](../../core/diagnostics/logging-tracing.md) .

## <a name="contentionstart_v1-event"></a>Zdarzenie ContentionStart_V1

To zdarzenie jest emitowane na początku rywalizacji o blokadę monitora.

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`ContentionKeyword` 0x4000|Informacyjny (4)|

 W poniższej tabeli przedstawiono informacje o zdarzeniach.

|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|
|-----------|--------------|-----------------|
|`ContentionStart_V1`|81|Rozpocznie się rywalizacja o blokady monitora.|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`Flags`|`win:UInt8`|`0` dla zarządzanych; `1` dla natywnego.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|

## <a name="contentionstop_v1-event"></a>Zdarzenie ContentionStop_V1

To zdarzenie jest emitowane po zakończeniu rywalizacji o blokadę monitora.

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`ContentionKeyword` 0x4000|Informacyjny (4)|

 W poniższej tabeli przedstawiono informacje o zdarzeniach.

|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|
|-----------|--------------|-----------------|
|`ContentionStop_V1`|91|Zakończyło się rywalizacja blokady monitora.|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`Flags`|`win:UInt8`|`0` dla zarządzanych; `1` dla natywnego.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia elementu CoreCLR.|
|`DurationNs`|`win:Double`|Czas trwania rywalizacji w nanosekundach.|
