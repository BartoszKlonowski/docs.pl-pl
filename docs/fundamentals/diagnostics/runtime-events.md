---
title: Zdarzenia środowiska uruchomieniowego
description: Przeglądanie zdarzeń diagnostycznych emitowanych przez środowisko uruchomieniowe platformy .NET (CoreCLR), które mogą być używane z funkcją ETW, LTTng lub EventPipe.
ms.date: 11/13/2020
ms.topic: reference
helpviewer_keywords:
- runtime events (CoreCLR)
- ETW, EventPipe runtime events (CoreCLR)
ms.openlocfilehash: 33fa7275ce40934ce043b4d0dba5749c37515755
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "96589996"
---
# <a name="net-runtime-events"></a>Zdarzenia środowiska uruchomieniowego platformy .NET

Środowisko uruchomieniowe .NET (CoreCLR) emituje różne zdarzenia, których można użyć do diagnozowania problemów z aplikacją .NET, które mogą być używane przez różne mechanizmy `ETW` , takie jak, `LTTng` i `EventPipe` .

Ten dokument służy jako odwołanie do zdarzeń, które są wywoływane przez środowisko uruchomieniowe platformy .NET Core.

Zdarzenia środowiska uruchomieniowego w .NET Framework można znaleźć w temacie [zdarzenia ETW środowiska CLR](../../framework/performance/clr-etw-events.md).

## <a name="in-this-section"></a>W tej sekcji

[Zdarzenia rywalizacji](runtime-contention-events.md)\
Te zdarzenia zbierają informacje o rywalizacjach o blokady monitora.

[Zdarzenia wyrzucania elementów bezużytecznych](runtime-garbage-collection-events.md)\
Te zdarzenia zbierają informacje dotyczące wyrzucania elementów bezużytecznych. Ułatwiają one diagnostykę i debugowanie, w tym określanie, ile razy zostało wykonane wyrzucanie elementów bezużytecznych, ile pamięci zostało zwolnione podczas wyrzucania elementów bezużytecznych itp.

[Zdarzenia wyjątków](runtime-exception-events.md)\
Te zdarzenia środowiska uruchomieniowego przechwytują informacje o zgłaszanych wyjątkach.

[Zdarzenia międzyoperacyjności](runtime-interop-events.md)\
Te zdarzenia środowiska uruchomieniowego przechwytują informacje o generacji wygenerowanej w języku pośrednim (CIL).

[Zdarzenia modułu ładującego i spinacza](runtime-loader-binder-events.md)\
Te zdarzenia zbierają informacje dotyczące ładowania i zwalniania zestawów i modułów.

[Zdarzenia metody](runtime-method-events.md)\
Te zdarzenia zbierają informacje, które są specyficzne dla metod. Ładunek tych zdarzeń jest wymagany do rozpoznawania symboli. Ponadto te zdarzenia zapewniają przydatne informacje, takie jak liczba przypadków wywołania metody.

[Zdarzenia wątku](runtime-thread-events.md)\
Te zdarzenia zbierają informacje o wątkach procesów roboczych i we/wy.

[Zdarzenia typu](runtime-type-events.md)\
Te zdarzenia zbierają informacje o systemie typów.
