---
title: Zdarzenie ETW stosu
description: Przeczytaj o zdarzeniu ETW stosu, który powinien być używany w połączeniu z innymi zdarzeniami w celu wygenerowania śladów stosu po podniesieniu zdarzenia.
ms.date: 03/30/2017
helpviewer_keywords:
- stack event [.NET Framework]
- ETW, stack event (CLR)
ms.assetid: f612fa5b-4b62-4593-a19e-85c9b1018dce
ms.openlocfilehash: cab496615c4ef17831895b72c8987917e3c06e77
ms.sourcegitcommit: cf5a800a33de64d0aad6d115ffcc935f32375164
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/20/2020
ms.locfileid: "86474140"
---
# <a name="stack-etw-event"></a>Zdarzenie ETW stosu
Zdarzenia stosu należy używać w połączeniu z innymi zdarzeniami w celu generowania śladów stosu po podniesieniu zdarzenia. Jest on rejestrowany po włączeniu dostawcy środowiska uruchomieniowego. Jest to zdarzenie o dużej częstotliwości, ponieważ jest zgłaszane przy każdym wywołaniu innego zdarzenia środowiska uruchomieniowego. Z tego powodu zaleca się użycie tego zdarzenia z zachowaniem ostrożności.  
  
 W poniższej tabeli przedstawiono słowo kluczowe i poziom. (Aby uzyskać więcej informacji, zobacz [słowa kluczowe i poziomy ETW CLR](clr-etw-keywords-and-levels.md)).  
  
|Słowo kluczowe do podniesienia zdarzenia|Poziom|  
|-----------------------------------|-----------|  
|`StackKeyword`0x40000000|LogAlways (0)|  
  
 W poniższej tabeli przedstawiono informacje o zdarzeniu.  
  
|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|  
|-----------|--------------|-----------------|  
|`CLRStackWalk`|82|W połączeniu z innymi zdarzeniami do generowania śladów stosu po zdarzeniu.|  
  
 W poniższej tabeli przedstawiono dane zdarzenia.  
  
|Nazwa pola|Typ danych|Opis|  
|----------------|---------------|-----------------|  
|ClrInstanceID|win: UInt16|Unikatowy identyfikator środowiska uruchomieniowego.|  
|Reserved1|win: UInt8|Zarezerwowany.|  
|Reserved2|win: UInt8|Zarezerwowany.|  
|FrameCount|win: UInt32|Liczba ramek w śladzie stosu.|  
|Stos|win: wskaźnik|Kolumny wskaźników instrukcji.|  
  
## <a name="see-also"></a>Zobacz także

- [Zdarzenia ETW CLR](clr-etw-events.md)
