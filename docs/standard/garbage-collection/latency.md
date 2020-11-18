---
title: Tryby opóźnienia
ms.date: 03/30/2017
helpviewer_keywords:
- garbage collection, intrusiveness
- garbage collection, latency modes
ms.assetid: 96278bb7-6eab-4612-8594-ceebfc887d81
ms.openlocfilehash: 2e7b30a50e2513c567abf2116ab5495e717a8e22
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94831198"
---
# <a name="latency-modes"></a>Tryby opóźnienia

Aby odzyskiwać obiekty, Moduł wyrzucania elementów bezużytecznych (GC) musi zatrzymać wszystkie wątki wykonywane w aplikacji. Okres, w którym aktywny jest moduł wyrzucania elementów bezużytecznych, jest określany jako *czas opóźnienia*.

W niektórych sytuacjach, na przykład gdy aplikacja pobiera dane lub wyświetla zawartość, pełne wyrzucanie elementów bezużytecznych może wystąpić w krytycznym czasie i utrudnić wydajność. Można dostosować inwazyjność modułu wyrzucania elementów bezużytecznych, ustawiając <xref:System.Runtime.GCSettings.LatencyMode%2A?displayProperty=nameWithType> Właściwość na jedną z <xref:System.Runtime.GCLatencyMode?displayProperty=nameWithType> wartości.

## <a name="low-latency-settings"></a>Ustawienia małych opóźnień

Użycie ustawienia opóźnienia "niska" oznacza, że moduł wyrzucania elementów bezużytecznych wystawia się mniej w aplikacji. Wyrzucanie elementów bezużytecznych jest bardziej ostrożne w zakresie odzyskiwania pamięci.

<xref:System.Runtime.GCLatencyMode?displayProperty=nameWithType>Wyliczenie zawiera dwa ustawienia dotyczące małych opóźnień:

- [GCLatencyMode. LowLatency](xref:System.Runtime.GCLatencyMode.LowLatency) pomija kolekcje generacji 2 i wykonuje tylko kolekcje generacji 0 i 1. Może być używany tylko przez krótki okresy czasu. W dłuższym czasie, jeśli system jest w obszarze pamięci, Moduł wyrzucania elementów bezużytecznych wywoła kolekcję, która może krótko zawieszać aplikację i przerwać operację krytyczną czasu. To ustawienie jest dostępne tylko dla wyrzucania elementów bezużytecznych stacji roboczej.

- [GCLatencyMode. SustainedLowLatency](xref:System.Runtime.GCLatencyMode.SustainedLowLatency) pomija kolekcje pierwszego planu 2 i wykonuje tylko kolekcje generacji 0, 1 i 2. generacji w tle. Może być używany przez dłuższy okres czasu i jest dostępny zarówno dla stacji roboczej, jak i serwera. Nie można użyć tego ustawienia, jeśli wyrzucanie elementów bezużytecznych w tle jest wyłączone.

Podczas małych okresów opóźnienia kolekcje 2 generacji są pomijane, chyba że wystąpią następujące sytuacje:

- System odbiera powiadomienie o niskim poziomie pamięci z systemu operacyjnego.

- Kod aplikacji wywołuje kolekcję przez wywołanie <xref:System.GC.Collect%2A?displayProperty=nameWithType> metody i określenie 2 dla `generation` parametru.

## <a name="scenarios"></a>Scenariusze

W poniższej tabeli wymieniono scenariusze aplikacji dotyczące używania <xref:System.Runtime.GCLatencyMode> wartości:

|Tryb opóźnień|Scenariusze aplikacji|
|------------------|---------------------------|
|<xref:System.Runtime.GCLatencyMode.Batch>|W przypadku aplikacji, które nie mają interfejsu użytkownika lub operacji po stronie serwera.<br /><br />Gdy wyrzucanie elementów bezużytecznych w tle jest wyłączone, jest to domyślny tryb dla stacji roboczej i odzyskiwania pamięci serwera. <xref:System.Runtime.GCLatencyMode.Batch> tryb zastępuje również ustawienie [gcConcurrent](../../framework/configure-apps/file-schema/runtime/gcconcurrent-element.md) , czyli uniemożliwia wykonywanie w tle lub współbieżnych kolekcji.|
|<xref:System.Runtime.GCLatencyMode.Interactive>|Dla większości aplikacji, które mają interfejs użytkownika.<br /><br />Jest to domyślny tryb dla stacji roboczej i wyrzucania elementów bezużytecznych serwera. Jednak jeśli aplikacja jest hostowana, ustawienia modułu zbierającego elementy bezużyteczne procesu hostingu mają pierwszeństwo.|
|<xref:System.Runtime.GCLatencyMode.LowLatency>|W przypadku aplikacji, które mają krótkoterminowe, zależne od czasu operacje, w których przerwy między modułem wyrzucania elementów bezużytecznych mogą powodować zakłócenia. Na przykład aplikacje, które renderują animacje lub funkcje pozyskiwania danych.|
|<xref:System.Runtime.GCLatencyMode.SustainedLowLatency>|W przypadku aplikacji, które mają dane zależne od czasu, ale dłuższy czas, w którym przerwy z modułu wyrzucania elementów bezużytecznych mogą być zakłócone. Na przykład aplikacje, które wymagają krótkich czasów odpowiedzi jako zmiany danych rynkowych w godzinach pracy.<br /><br />Ten tryb powoduje zwiększenie rozmiaru zarządzanego sterty niż inne tryby. Ponieważ nie kompaktuje sterty zarządzanej, możliwe jest zwiększenie fragmentacji. Upewnij się, że dostępna jest wystarczająca ilość pamięci.|

## <a name="guidelines-for-using-low-latency"></a>Wskazówki dotyczące korzystania z małych opóźnień

W przypadku korzystania z trybu [GCLatencyMode. LowLatency](xref:System.Runtime.GCLatencyMode.LowLatency) należy wziąć pod uwagę następujące wytyczne:

- Przechowuj okres czasu w małych opóźnieniach, tak jak to możliwe.

- Unikaj alokowania dużych ilości pamięci podczas okresów o małym opóźnieniu. Powiadomienia o niskiej ilości pamięci mogą wystąpić, ponieważ odzyskiwanie pamięci przejmuje mniej obiektów.

- W trybie niskiego opóźnienia Zminimalizuj liczbę nowych alokacji, w szczególności przydziały do sterty dużego obiektu i przypiętych obiektów.

- Należy pamiętać o wątkach, które mogą być przydzielane. Ponieważ <xref:System.Runtime.GCSettings.LatencyMode%2A> ustawienie właściwości to cały proces, <xref:System.OutOfMemoryException> wyjątki mogą być generowane na dowolnym wątku, który jest przydzielany.

- Zawiń kod małych opóźnień w regionach ograniczonego wykonania. Aby uzyskać więcej informacji, zobacz [ograniczone regiony wykonania](../../framework/performance/constrained-execution-regions.md).

- Można wymusić kolekcje generacji 2 w okresie o małym opóźnieniu, wywołując <xref:System.GC.Collect%28System.Int32%2CSystem.GCCollectionMode%29?displayProperty=nameWithType> metodę.

## <a name="see-also"></a>Zobacz także

- <xref:System.GC?displayProperty=nameWithType>
- [Wywołane Kolekcje](induced.md)
- [Odzyskiwanie pamięci](index.md)
