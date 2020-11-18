---
title: Kolekcje bezpieczne wątkowo
description: Rozpocznij pracę z kolekcjami bezpiecznymi wątków przy użyciu przestrzeni nazw System. Collections. współbieżnej w programie .NET, która obejmuje bezpieczne dla wątków i skalowalne klasy kolekcji.
ms.date: 03/30/2017
helpviewer_keywords:
- thread-safe collections, overview
ms.assetid: 2e7ca21f-786c-4367-96be-0cf3f3dcc6bd
ms.openlocfilehash: 5f64d7b6a9b3564248a2b6113724e948066bf45c
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94827753"
---
# <a name="thread-safe-collections"></a>Kolekcje bezpieczne wątkowo
.NET Framework 4 wprowadza <xref:System.Collections.Concurrent?displayProperty=nameWithType> przestrzeń nazw, która zawiera kilka klas kolekcji, które są bezpieczne dla wątków i skalowalne. Wiele wątków może bezpiecznie i wydajnie dodawać lub usuwać elementy z tych kolekcji, bez konieczności przeprowadzania dodatkowej synchronizacji w kodzie użytkownika. Gdy piszesz nowy kod, użyj klas kolekcji współbieżnych, gdy wiele wątków będzie jednocześnie zapisywać do kolekcji. Jeśli z udostępnionej kolekcji odbywa się tylko odczyt, można używać klas z przestrzeni nazw <xref:System.Collections.Generic?displayProperty=nameWithType>. Zalecamy nieużywanie klas kolekcji w wersji 1.0, chyba że aplikacje mają być przeznaczone dla środowiska uruchomieniowego .NET Framework 1.1 lub starszego.  
  
## <a name="thread-synchronization-in-the-net-framework-10-and-20-collections"></a>Synchronizacja wątków w kolekcjach środowisk .NET Framework 1.0 i 2.0  
 Kolekcje wprowadzone w środowisku .NET Framework 1.0 znajdują się w przestrzeni nazw <xref:System.Collections?displayProperty=nameWithType>. Kolekcje te, wśród których są m.in. powszechnie używane <xref:System.Collections.ArrayList> i <xref:System.Collections.Hashtable>, oferują pewne bezpieczeństwo wątkowe za pomocą właściwości `Synchronized`, która zwraca bezpieczną wątkowo otokę wokół kolekcji. Otoka działa w ten sposób, że blokuje całą kolekcję podczas każdej operacji dodawania lub usuwania. W związku z tym każdy wątek, który próbuje uzyskać dostęp do kolekcji, musi czekać na swoją kolej, aby nałożyć jedną blokadę. Takie rozwiązanie nie jest skalowalne i przy dużych kolekcjach może powodować znaczne pogorszenie wydajności. Ponadto konstrukcja nie jest całkowicie chroniona przed sytuacjami wyścigu. Aby uzyskać więcej informacji, zobacz [synchronizacja w kolekcjach ogólnych](/archive/blogs/bclteam/synchronization-in-generic-collections-brian-grunkemeyer).  
  
 Klasy kolekcji wprowadzone w środowisku .NET Framework 2.0 są umieszczone w przestrzeni nazw <xref:System.Collections.Generic?displayProperty=nameWithType>. Należą do nich <xref:System.Collections.Generic.List%601>, <xref:System.Collections.Generic.Dictionary%602> itd. Te klasy oferują większe bezpieczeństwo pod względem typów i lepszą wydajność niż klasy środowiska .NET Framework 1.0. Jednak klasy kolekcji środowiska .NET Framework 2.0 nie zawierają żadnych funkcji synchronizacji wątków. Gdy elementy są dodawane lub usuwane równolegle w wielu wątkach, całą synchronizację musi zapewniać kod użytkownika.  
  
 Zalecamy stosowanie klas kolekcji współbieżnych w .NET Framework 4, ponieważ zapewniają one nie tylko bezpieczeństwo typu klasy kolekcji .NET Framework 2,0, ale również wydajniejsze i bardziej kompletne bezpieczeństwo wątku niż w przypadku kolekcji .NET Framework 1,0.  
  
## <a name="fine-grained-locking-and-lock-free-mechanisms"></a>Blokowanie szczegółowe i mechanizmy bezblokadowe  
 Niektóre typy kolekcji współbieżnych wykorzystują uproszczone mechanizmy synchronizacji, takie jak <xref:System.Threading.SpinLock> ,, <xref:System.Threading.SpinWait> <xref:System.Threading.SemaphoreSlim> i <xref:System.Threading.CountdownEvent> , które są nowe w .NET Framework 4. Te typy synchronizacji zwykle są *zajęte* przez krótki czas przed umieszczeniem wątku w stanie "prawda". Jeśli spodziewane czasy oczekiwania będą bardzo krótkie, warto stosować rotowanie, ponieważ znacznie mniej obciąża ono zasoby systemu niż przejścia jądra występujące w czekaniu. W przypadku klas kolekcji wykorzystujących mechanizm rotowania lepsza wydajność oznacza możliwość dodawania i usuwania elementów równolegle przez wiele wątków z bardzo dużą szybkością. Aby uzyskać więcej informacji na temat wirowania i blokowania, zobacz [struktury spinlock](../../threading/spinlock.md) i [metody SpinWait](../../threading/spinwait.md).  
  
 Klasy <xref:System.Collections.Concurrent.ConcurrentQueue%601> i <xref:System.Collections.Concurrent.ConcurrentStack%601> w ogóle nie nakładają blokad. Zamiast tego do zapewnienia bezpieczeństwa wątkowego wykorzystują operacje <xref:System.Threading.Interlocked>.  
  
> [!NOTE]
> Ponieważ klasy kolekcji współbieżnych obsługują interfejs <xref:System.Collections.ICollection>, implementują one właściwości <xref:System.Collections.ICollection.IsSynchronized%2A> i <xref:System.Collections.ICollection.SyncRoot%2A>, nawet jeśli te właściwości są nieistotne. Właściwość `IsSynchronized` zawsze zwraca wartość `false`, a właściwość `SyncRoot` zawsze ma wartość `null` (`Nothing` w języku Visual Basic).  
  
 W tabeli poniżej wymieniono typy kolekcji istniejące w przestrzeni nazw <xref:System.Collections.Concurrent?displayProperty=nameWithType>.  
  
|Typ|Opis|  
|----------|-----------------|  
|<xref:System.Collections.Concurrent.BlockingCollection%601>|Zapewnia funkcjonalność ograniczania i blokowania dla wszystkich typów implementujących interfejs <xref:System.Collections.Concurrent.IProducerConsumerCollection%601>. Aby uzyskać więcej informacji, zobacz [BlockingCollection Overview (przegląd](blockingcollection-overview.md)).|  
|<xref:System.Collections.Concurrent.ConcurrentDictionary%602>|Bezpieczna wątkowo implementacja słownika par klucz-wartość.|  
|<xref:System.Collections.Concurrent.ConcurrentQueue%601>|Bezpieczna wątkowo implementacja kolejki FIFO („pierwszy na wejściu, pierwszy na wyjściu”).|  
|<xref:System.Collections.Concurrent.ConcurrentStack%601>|Bezpieczna wątkowo implementacja stosu LIFO („ostatni na wejściu, pierwszy na wyjściu”).|  
|<xref:System.Collections.Concurrent.ConcurrentBag%601>|Bezpieczna wątkowo implementacja nieuporządkowanej kolekcji elementów.|  
|<xref:System.Collections.Concurrent.IProducerConsumerCollection%601>|Interfejs, który musi implementować typ, aby mógł być używany w klasie `BlockingCollection`.|  
  
## <a name="related-topics"></a>Tematy pokrewne  
  
|Tytuł|Opis|  
|-----------|-----------------|  
|[BlockingCollection — Przegląd](blockingcollection-overview.md)|Opisuje funkcje zawarte w typie <xref:System.Collections.Concurrent.BlockingCollection%601>.|  
|[Instrukcje: Dodawanie elementów do kolekcji ConcurrentDictionary i ich usuwanie](how-to-add-and-remove-items.md)|Opisuje metody dodawania i usuwania elementów w klasie <xref:System.Collections.Concurrent.ConcurrentDictionary%602>.|  
|[Instrukcje: Dodawanie i pobieranie elementów osobno w ramach kolekcji BlockingCollection](how-to-add-and-take-items.md)|Opisuje metody dodawania i pobierania elementów z kolekcji blokującej bez używania modułu wyliczającego z właściwością tylko do odczytu.|  
|[Instrukcje: Dodawanie funkcji blokujących i ograniczających do kolekcji](how-to-add-bounding-and-blocking.md)|Opisuje wykorzystywanie klas kolekcji jako podstawowego mechanizmu przechowywania dla kolekcji <xref:System.Collections.Concurrent.IProducerConsumerCollection%601>.|  
|[Instrukcje: Używanie metody ForEach do usuwania elementów z kolekcji BlockingCollection](how-to-use-foreach-to-remove.md)|Opisuje zastosowanie instrukcji `foreach` (`For Each` w języku Visual Basic) do usuwania wszystkich elementów w kolekcji blokującej.|  
|[Instrukcje: Używanie tablic kolekcji blokujących w potoku](how-to-use-arrays-of-blockingcollections.md)|Opisuje zastosowanie wielu kolekcji blokujących równocześnie w celu zaimplementowania potoku.|  
|[Instrukcje: Tworzenie puli obiektów przy użyciu obiektu ConcurrentBag](how-to-create-an-object-pool.md)|Pokazuje, jak za pomocą współbieżnego zbioru poprawić wydajność w scenariuszach, gdzie można wykorzystywać istniejące obiekty zamiast ciągle tworzyć nowe.|  
  
## <a name="reference"></a>Tematy pomocy  
 <xref:System.Collections.Concurrent?displayProperty=nameWithType>
