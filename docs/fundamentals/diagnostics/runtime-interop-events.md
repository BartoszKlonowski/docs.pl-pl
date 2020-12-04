---
title: Zdarzenia środowiska uruchomieniowego Interop
description: Zobacz zdarzenia środowiska uruchomieniowego platformy .NET, które zbierają informacje diagnostyczne specyficzne dla międzyoperacyjności.
ms.date: 11/13/2020
ms.topic: reference
helpviewer_keywords:
- Interop events (CoreCLR)
- ETW, EventPipe, LTTng interop events (CoreCLR)
ms.openlocfilehash: 5635fb55b3a6ffa3f5611da80cdb2909e226e2ea
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "96589995"
---
# <a name="net-runtime-interop-events"></a>Zdarzenia międzyoperacyjności środowiska uruchomieniowego .NET

Te zdarzenia środowiska uruchomieniowego przechwytują informacje o generacji wygenerowanej w języku pośrednim (CIL). Aby uzyskać więcej informacji na temat korzystania z tych zdarzeń w celach diagnostycznych, zobacz [Rejestrowanie i śledzenie aplikacji .NET](../../core/diagnostics/logging-tracing.md) .

## <a name="ilstubgenerated-event"></a>Zdarzenie ILStubGenerated

|Słowo kluczowe do podniesienia zdarzenia|Poziom|
|-----------------------------------|-----------|
|`InteropKeyword` (0x2000)|Informacyjny (4)|
  
|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|
|-----------|--------------|-----------------|
|`ILStubGenerated`|88|Jest generowana Klasa zastępcza IL.|

|Nazwa pola|Typ danych|Opis|
|----------------|---------------|-----------------|
|`ModuleID`|`win:UInt16`|Identyfikator modułu.|
|`StubMethodID`|`win:UInt64`|Identyfikator metody zastępczej.|
|`StubFlags`|`win:UInt32`|Flagi dla elementu zastępczego:<br /><br /> `0x1` — Odwrotna współdziałanie.<br /><br /> `0x2` -Międzyoperacyjność COM.<br /><br /> `0x4` -Stub wygenerowany przez NGen.exe.<br /><br /> `0x8` Wierz.<br /><br /> `0x10` -Variable — argument.<br /><br /> `0x20` -Niezarządzane wywoływany.<br /><br /> `0x40` — Kierowanie strukturą|
|`ManagedInteropMethodToken`|`win:UInt32`|Token dla zarządzanej metody międzyoperacyjnego.|
|`ManagedInteropMethodNameSpace`|`win:UnicodeString`|Przestrzeń nazw i typ otaczający metody zarządzanej międzyoperacyjności.|
|`ManagedInteropMethodName`|`win:UnicodeString`|Nazwa zarządzanej metody międzyoperacyjnego.|
|`ManagedInteropMethodSignature`|`win:UnicodeString`|Sygnatura zarządzanej metody międzyoperacyjnego.|
|`NativeMethodSignature`|`win:UnicodeString`|Podpis metody natywnej.|
|`StubMethodSignature`|`win:UnicodeString`|Sygnatura metody zastępczej.|
|`StubMethodILCode`|`win:UnicodeString`|Kod wspólnego języka pośredniego (CIL) dla metody zastępczej.|
|`ClrInstanceID`|`win:UInt16`|Unikatowy identyfikator wystąpienia CLR lub CoreCLR.|
