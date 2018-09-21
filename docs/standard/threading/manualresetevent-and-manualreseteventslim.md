---
title: ManualResetEvent i ManualResetEventSlim
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- threading [.NET Framework], ManualResetEvent class
- ManualResetEvent class, about ManualResetEvent class
ms.assetid: 465fdcf9-ba24-4d8d-a43f-d983b7cb0cc6
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 4949540b9f61e71301647a83a1c05d8b4c941412
ms.sourcegitcommit: dfb2a100cfb4d3902c042f17b3204f49bc7635e7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/20/2018
ms.locfileid: "46492041"
---
# <a name="manualresetevent-and-manualreseteventslim"></a>ManualResetEvent i ManualResetEventSlim
<xref:System.Threading.ManualResetEvent?displayProperty=nameWithType> Klasa reprezentuje zdarzenie dojścia oczekiwania lokalne, które można ręcznie zresetować po zostanie zasygnalizowane. Ta klasa reprezentuje przypadkiem szczególnym klasy bazowej, <xref:System.Threading.EventWaitHandle?displayProperty=nameWithType>. Zobacz [EventWaitHandle](../../../docs/standard/threading/eventwaithandle.md) dokumentacji koncepcyjnego dla użycia i funkcje ręczne Resetowanie zdarzenia.  
  
 A <xref:System.Threading.ManualResetEvent> obiekt pozostaje sygnałowego aż do jego <xref:System.Threading.EventWaitHandle.Reset%2A?displayProperty=nameWithType> metoda jest wywoływana. Dowolną liczbę oczekujących wątki lub wątki, które oczekiwania na zdarzenie po zostało zasygnalizowane, może być zwolnione, gdy stan obiektu jest sygnalizowane.
  
 W [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], możesz użyć <xref:System.Threading.ManualResetEventSlim?displayProperty=nameWithType> klasy w celu zapewnienia lepszej wydajności po spodziewane czasy oczekiwania będą bardzo krótkie, a gdy zdarzenie nie przekraczają granice procesu. <xref:System.Threading.ManualResetEventSlim> używa zajęty, obracanie przez krótki czas podczas oczekiwania na zdarzenie zostało zasygnalizowane. W przypadku krótkie czasy oczekiwania rotowania może być znacznie mniej kosztowne niż za pomocą uchwytów oczekiwania. Jednakże, jeśli zdarzenie nie zasygnalizowane w przedziale czasu, <xref:System.Threading.ManualResetEventSlim> sortuje ponownie do oczekiwania uchwyt wydarzeń.  
  
## <a name="see-also"></a>Zobacz także

- [Wątkowość](../../../docs/standard/threading/index.md)  
- [Wątkowość obiektów i funkcji](../../../docs/standard/threading/threading-objects-and-features.md)  
- [Uchwyty oczekiwania](https://msdn.microsoft.com/library/48d10b6f-5fd7-407c-86ab-0179aef72489)  
- [AutoResetEvent](../../../docs/standard/threading/autoresetevent.md)  
- [SpinWait](../../../docs/standard/threading/spinwait.md)  
- [Semaphore i SemaphoreSlim](../../../docs/standard/threading/semaphore-and-semaphoreslim.md)
