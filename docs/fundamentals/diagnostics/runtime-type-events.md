---
title: Wpisz zdarzenia środowiska uruchomieniowego systemu
description: Zobacz zdarzenia środowiska uruchomieniowego platformy .NET, które zbierają informacje diagnostyczne specyficzne dla systemu typu .NET, takie jak TypeLoadStart i TypeLoadStop.
ms.date: 11/13/2020
ms.topic: reference
helpviewer_keywords:
- type system events (CoreCLR)
- ETW, EventPipe, LTTng type system events (CoreCLR)
ms.openlocfilehash: 8eee89cddb0098da2cb449a4be21945adac725e3
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "96589988"
---
# <a name="net-runtime-type-events"></a>Zdarzenia typu środowiska uruchomieniowego .NET

Te zdarzenia zbierają informacje dotyczące typów ładowania. Aby uzyskać więcej informacji na temat korzystania z tych zdarzeń w celach diagnostycznych, zobacz [Rejestrowanie i śledzenie aplikacji .NET](../../core/diagnostics/logging-tracing.md) .

## <a name="typeloadstart-event"></a>Zdarzenie TypeLoadStart

|Słowo kluczowe do podniesienia zdarzenia|Zdarzenie|Poziom|  
|-----------------------------------|-----------|-----------|  
|`TypeDiagnosticKeyword` (0x8000000000)|Informacyjny (4)|  

|Zdarzenie|Identyfikator zdarzenia|Opis|  
|-----------|--------------|-----------------|  
|`TypeLoadStart`|73|Ładowanie typu zostało rozpoczęte.|

|Nazwa pola|Typ danych|Opis|  
|----------------|---------------|-----------------|  
|`TypeLoadStartID`|`win:UInt32`|Identyfikator operacji ładowania typu.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia CLR lub CoreCLR.|  

## <a name="typeloadstop-event"></a>Zdarzenie TypeLoadStop

|Słowo kluczowe do podniesienia zdarzenia|Poziom|  
|-----------------------------------|-----------|-----------|  
|`TypeDiagnosticKeyword` (0x8000000000)|Informacyjny (4)|  

|Zdarzenie|Identyfikator zdarzenia|Opis|  
|-----------|--------------|-----------------|  
|`TypeLoadStop`|74|Ładowanie typu zostało zakończone.|

|Nazwa pola|Typ danych|Opis|  
|----------------|---------------|-----------------|  
|`TypeLoadStartID`|`win:UInt32`|Identyfikator operacji ładowania typu (pasuje do odpowiadającego TypeLoadStartID zdarzenia TypeLoadStart).|
|`LoadLevel`|`win:UInt16`|Wpisz poziom ładowania.|
|`TypeID`|`win:UInt64`|Wskaźnik do dojścia do typu.|
|`TypeName`|`win:UnicodeString`|Nazwa typu.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia CLR lub CoreCLR.|  
