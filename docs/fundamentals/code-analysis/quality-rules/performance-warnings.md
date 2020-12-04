---
title: Reguły wydajności (analiza kodu)
description: Poznaj reguły wydajności analizy kodu.
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.performancerules
helpviewer_keywords:
- rules, performance
- performance rules
- performance, rules
- managed code analysis rules, performance rules
author: gewarren
ms.author: gewarren
ms.openlocfilehash: 4409cc46eb73f13f8e59d7a51899da27035bb6af
ms.sourcegitcommit: 2e4adc490c1d2a705a0592b295d606b10b9f51f1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/25/2020
ms.locfileid: "96586956"
---
# <a name="performance-rules"></a>Reguły wydajności

Reguły wydajności obsługują biblioteki i aplikacje o wysokiej wydajności.

## <a name="in-this-section"></a>W tej sekcji

| Reguła | Opis |
| - | - |
| [CA1802: Używaj literałów w odpowiednich miejscach](ca1802.md) | Pole jest zadeklarowane jako static i tylko do odczytu (Shared i ReadOnly w Visual Basic) i jest inicjowane z wartością, która jest obliczanej w czasie kompilacji. Ponieważ wartość przypisana do pola Target jest obliczanej w czasie kompilacji, należy zmienić deklarację na wartość const (const w Visual Basic), tak aby była obliczana w czasie kompilacji, a nie w czasie wykonywania. |
| [CA1805: Nie inicjuj niepotrzebnie](ca1805.md) | Środowisko uruchomieniowe platformy .NET inicjuje wszystkie pola typów odwołań do ich wartości domyślnych przed uruchomieniem konstruktora. W większości przypadków jawne zainicjowanie pola do jego wartości domyślnej jest nadmiarowe, co zwiększa koszty konserwacji i może obniżyć wydajność (na przykład większy rozmiar zestawu). |
| [CA1806: Nie ignoruj wyników metod](ca1806.md) | Nowy obiekt jest tworzony, ale nigdy nie jest używany lub metoda, która tworzy i zwraca nowy ciąg, jest wywoływana, a nowy ciąg nigdy nie jest używany lub metoda Component Object Model (COM) lub P/Invoke zwraca wynik HRESULT lub kod błędu, który nigdy nie jest używany. |
| [CA1810: Inicjuj pola statyczne typu referencyjnego śródwierszowo](ca1810.md) | Podczas gdy typ deklaruje jawny, statyczny konstruktor, kompilator just in time (JIT) do każdej metody statycznej dodaje sprawdzenie i konstruktora wystąpienia, aby upewnić się, że konstruktor statyczny został wcześniej wywołany. Sprawdzenia konstruktora statycznego mogą obniżyć wydajność. |
| [CA1812: Unikaj klas wewnętrznych bez wystąpień](ca1812.md) | Wystąpienie typu na poziomie zestawu nie jest tworzone przez kod w zestawie. |
| [CA1813: Unikaj niezapieczętowanych atrybutów](ca1813.md) | .NET oferuje metody pobierania atrybutów niestandardowych. Domyślnie te metody wyszukują hierarchie dziedziczenia atrybutu. Plombowanie atrybutu eliminuje wyszukiwanie przez hierarchię dziedziczenia i może zwiększyć wydajność. |
| [CA1814: Wybieraj tablice nieregularne zamiast wielowymiarowych](ca1814.md) | Nieregularna tablica to ta, której elementy są tablicami. Tablice, które składają się na elementy, mogą mieć różne rozmiary, co może spowodować mniejsze ilości wolnego miejsca dla niektórych zestawów danych. |
| [CA1815: Przesłaniaj metodę equals i operator równości w typach wartości](ca1815.md) | Dla typów wartości dziedziczona implementacja operatora Equas wykorzystuje bibliotekę odbić i porównuje zawartość wszystkich pól. Odbicie jest obliczeniowo kosztowne, a porównanie równości każdego pola może być niepotrzebne. Jeśli można się spodziewać, że użytkownicy będą porównywać lub sortować wystąpienia lub używać wystąpień jako kluczy tabel haszowanych, typ wartości powinien implementować Equals. |
| [CA1819: Właściwości nie powinny zwracać tablic](ca1819.md) | Tablice zwracane przez właściwości nie są chronione przed zapisem, nawet jeśli właściwość jest tylko do odczytu. Aby zachować tablicę odporną na manipulacje, właściwość musi zwracać kopię tablicy. Zwykle użytkownicy nie rozumieją, jakie niekorzystne następstwa dla wydajności ma wywołanie takiej właściwości. |
| [CA1820: Testuj obecność pustych ciągów przy użyciu długości ciągu](ca1820.md) | Porównywanie ciągów za pomocą właściwości String.Length lub metody String.IsNullOrEmpty jest znacznie szybsze niż użycie operatora Equals. |
| [CA1821: Usuwaj puste finalizatory](ca1821.md) | Jeśli to tylko możliwe, należy unikać finalizatorów ze względu na dodatkowe obciążenie, które bierze udział w śledzeniu okresu istnienia obiektu. Pusty finalizator wiąże się z dodatkowymi kosztami bez korzyści. |
| [CA1822: Oznaczaj składowe jako statyczne](ca1822.md) | Elementy członkowskie, które nie uzyskują dostępu do danych wystąpienia lub wywołania metody wystąpienia, mogą być oznaczone jako statyczne (udostępnione w Visual Basic). Po oznaczeniu metod jako statyczne kompilator wygeneruje niewirtualne wywołania do tych członków. To może dać wymierny zysk wydajnościowy dla kodu wrażliwego na wydajność. |
| [CA1823: Unikaj nieużywanych pól prywatnych](ca1823.md) | Zostały wykryte pola prywatne, które w zestawie nie są widoczne jako dostępne. |
| [CA1824: Oznaczaj zestawy za pomocą atrybutu NeutralResourcesLanguageAttribute](ca1824.md) | Atrybut NeutralResourcesLanguage informuje Menedżer zasobów języka, który został użyty do wyświetlenia zasobów neutralnej kultury dla zestawu. To zwiększa wydajność wyszukiwania dla pierwszego zasobu, który się ładuje i może zmniejszyć zestaw roboczy. |
| [CA1825: Unikaj alokacji tablic o zerowej długości](ca1825.md) | Inicjowanie tablicy o zerowej długości prowadzi do niepotrzebnej alokacji pamięci. Zamiast tego należy użyć statycznie przydzielonego wystąpienia pustej tablicy przez wywołanie <xref:System.Array.Empty%2A?displayProperty=nameWithType> . Alokacja pamięci jest współdzielona przez wszystkie wywołania tej metody. |
| [CA1826: Użyj właściwości zamiast metody Linq Enumerable](ca1826.md) | <xref:System.Linq.Enumerable> Metoda LINQ została użyta na typie, który obsługuje równoważną, wydajniejszą właściwość. |
| [CA1827: Nie używaj funkcji Count/LongCount, gdy można użyć funkcji Any](ca1827.md) | <xref:System.Linq.Enumerable.Count%2A> Metoda or <xref:System.Linq.Enumerable.LongCount%2A> została użyta w przypadku, gdy <xref:System.Linq.Enumerable.Any%2A> Metoda byłaby bardziej wydajna. |
| [CA1828: Nie używaj funkcji CountAsync/LongCountAsync, gdy można użyć funkcji AnyAsync](ca1828.md) | <xref:Microsoft.EntityFrameworkCore.EntityFrameworkQueryableExtensions.CountAsync%2A> Metoda or <xref:Microsoft.EntityFrameworkCore.EntityFrameworkQueryableExtensions.LongCountAsync%2A> została użyta w przypadku, gdy <xref:Microsoft.EntityFrameworkCore.EntityFrameworkQueryableExtensions.AnyAsync%2A> Metoda byłaby bardziej wydajna. |
| [CA1829: Użyj właściwości Length/Count zamiast metody Enumerable.Count](ca1829.md) | <xref:System.Linq.Enumerable.Count%2A> Metoda LINQ została użyta w typie, który obsługuje równoważną, wydajniejszą `Length` lub `Count` Właściwość. |
| [CA1830: Preferuj silnie typizowane przeciążenia metod Append i Insert w elemencie StringBuilder](ca1830.md) | <xref:System.Text.StringBuilder.Append%2A> i <xref:System.Text.StringBuilder.Insert%2A> Podaj przeciążenia dla wielu typów poza typem system. String.  Jeśli to możliwe, Preferuj silnie wpisane przeciążenia przy użyciu metody ToString () i przeciążenia opartego na ciągach. |
| [CA1831: Użyj metody AsSpan zamiast indeksatorów opartych na zakresie dla ciągów, gdy ma to zastosowanie](ca1831.md) | W przypadku korzystania z indeksatora zakresu w ciągu i niejawnego przypisywania wartości do &lt; typu char ReadOnlySpan &gt; , Metoda <xref:System.String.Substring%2A?#System_String_Substring_System_Int32_System_Int32_> zostanie użyta zamiast <xref:System.Span%601.Slice%2A?#System_Span_1_Slice_System_Int32_System_Int32_> , która tworzy kopię żądanego fragmentu ciągu. |
| [CA1832: Użyj metody AsSpan lub AsMemory zamiast indeksatorów opartych na zakresie do pobierania części ReadOnlySpan lub ReadOnlyMemory dla tablicy](ca1832.md) | W przypadku korzystania z indeksatora zakresu w tablicy i niejawnego przypisywania wartości <xref:System.ReadOnlySpan%601> do <xref:System.ReadOnlyMemory%601> typu lub, Metoda <xref:System.Runtime.CompilerServices.RuntimeHelpers.GetSubArray%2A> zostanie użyta zamiast <xref:System.Span%601.Slice%2A?#System_Span_1_Slice_System_Int32_System_Int32_> , która tworzy kopię żądanego fragmentu tablicy. |
| [CA1833: Użyj metody AsSpan lub AsMemory zamiast indeksatorów opartych na zakresie do pobierania części Memory dla tablicy](ca1833.md) | W przypadku korzystania z indeksatora zakresu w tablicy i niejawnego przypisywania wartości <xref:System.Span%601> do <xref:System.Memory%601> typu lub, Metoda <xref:System.Runtime.CompilerServices.RuntimeHelpers.GetSubArray%2A> zostanie użyta zamiast <xref:System.Span%601.Slice%2A?#System_Span_1_Slice_System_Int32_System_Int32_> , która tworzy kopię żądanego fragmentu tablicy. |
| [CA1834: Użyj StringBuilder.Append(char) dla ciągów z pojedynczym znakiem](ca1834.md) | <xref:System.Text.StringBuilder> ma `Append` Przeciążenie, które przyjmuje `char` jako argument. Preferuj wywołania `char` przeciążenia w celu zwiększenia wydajności. |
| [CA1835: Preferuj przeciążenia oparte na Memory' dla elementu "ReadAsync" i "WriteAsync"](ca1835.md) | Element "Stream" ma Przeciążenie "ReadAsync", które przyjmuje &lt; &gt; jako pierwszy argument "bajt pamięci", i Przeciążenie "WriteAsync", które pobiera "ReadOnlyMemory &lt; Byte &gt; " jako pierwszy argument. Preferuj wywoływanie przeciążeń opartych na pamięci, co jest bardziej wydajne. |
| [CA1836: Preferuj `IsEmpty` , `Count` Jeśli są dostępne](ca1836.md) | Preferuj `IsEmpty` Właściwość, która jest bardziej wydajna niż `Count` , `Length` <xref:System.Linq.Enumerable.Count%60%601%28System.Collections.Generic.IEnumerable%7B%60%600%7D%29> lub, <xref:System.Linq.Enumerable.LongCount%60%601%28System.Collections.Generic.IEnumerable%7B%60%600%7D%29> Aby określić, czy obiekt zawiera elementy, czy nie. |
| [CA1837: Użyj `Environment.ProcessId` zamiast `Process.GetCurrentProcess().Id`](ca1837.md) | `Environment.ProcessId` jest prostsze i szybsze niż `Process.GetCurrentProcess().Id` . |
| [CA1838: Unikaj `StringBuilder` parametrów dla P/Invoke](ca1838.md) | Kierowanie programu `StringBuilder` zawsze tworzy natywną kopię buforu, powodującą wiele alokacji dla jednej operacji organizowania. |
