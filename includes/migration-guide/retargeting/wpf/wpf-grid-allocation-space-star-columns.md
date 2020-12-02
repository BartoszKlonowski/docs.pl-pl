---
ms.openlocfilehash: 28b882384760c8ac56c6d194bef6018c451fd03f
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96477257"
---
### <a name="wpf-grid-allocation-of-space-to-star-columns"></a>Alokacja siatki w usłudze WPF do kolumn w postaci gwiazdek

#### <a name="details"></a>Szczegóły

Począwszy od .NET Framework 4,7, WPF zastępuje algorytm <xref:System.Windows.Controls.Grid> używany do przydzielania przestrzeni do \* kolumn. Spowoduje to zmianę rzeczywistej szerokości przypisanej do \* kolumn w kilku przypadkach:

- Gdy co najmniej jedna \* kolumna ma także minimalną lub maksymalną szerokość, która zastępuje proporcjonalną alokację dla tego kolum. (Minimalna szerokość może pochodzić od jawnej deklaracji MinWidth lub z niejawnego minimum uzyskanego z zawartości kolumny. Maksymalną szerokość można zdefiniować jawnie, z deklaracji MaxWidth.)
- Gdy co najmniej jedna \* kolumna deklaruje bardzo dużą \* wagę, większą niż 10 ^ Karat.
- Gdy \* wagi są wystarczająco różne, aby napotkać niestabilność zmiennoprzecinkową (przepełnienie, niedomiarowe, utrata dokładności).
- Gdy jest włączone zaokrąglenie układu, a efektywne wyświetlanie DPI jest wystarczająco wysokie.
W pierwszych dwóch przypadkach szerokość wyprodukowanych przez nowy algorytm może być znacząco różna od tych, które zostały utworzone przez stary algorytm; w ostatnim przypadku różnica będzie wynosić co najwyżej jeden lub dwa piksele.<p/>Nowy algorytm naprawia kilka usterek obecnych w starym algorytmie:

- Całkowita alokacja do kolumn może przekroczyć szerokość siatki. Taka sytuacja może wystąpić, gdy przydzielasz miejsce do kolumny, której udział proporcjonalny jest mniejszy niż rozmiar minimalny. Algorytm przydziela minimalny rozmiar, co zmniejsza ilość miejsca dostępnego dla innych kolumn. Jeśli nie ma \* kolumn do przydzielenia, całkowita alokacja będzie zbyt duża.
- Całkowita Alokacja może być krótsza od szerokości siatki. Jest to podwójny problem, który należy #1, powstały podczas alokowania do kolumny, której udział proporcjonalny jest większy niż jego maksymalny rozmiar, bez \* kolumn pozostały do wykonania zapasu.
- Dwie \* kolumny mogą otrzymywać alokacje nieproporcjonalne do ich \* wag. Jest to łagodniejsza wersja #1/#2, powstała podczas przydzielania do \* kolumn a, b i C (w tej kolejności), gdzie udział proporcjonalny B narusza jego minimalne (lub maks.) ograniczenie. Jak wspomniano powyżej, spowoduje to zmianę dostępnego miejsca na kolumnę C, która jest mniej (lub większa) proporcjonalną alokacją od,
- Kolumny mające bardzo duże wagi ( &gt; 10 ^ Karat) są traktowane jak w przypadku wagi 10 ^. Proporcjonalne różnice między nimi (i między kolumnami o nieco mniejszych wagach) nie są honorowane.
- Kolumny z nieograniczoną wagą nie są poprawnie obsługiwane. [W rzeczywistości nie można ustawić wagi na nieskończoność, ale jest to sztuczne ograniczenie. Kod alokacji próbował go obsłużyć, ale wykonuje złe zadanie.]
- Kilka drobnych problemów podczas unikania przepełnienia, pośrednika, utraty dokładności i podobnych problemów zmiennoprzecinkowych.
- Korekty dotyczące zaokrąglania układu są nieprawidłowe przy wystarczająco wysokiej rozdzielczości DPI.
Nowy algorytm daje wyniki, które spełniają następujące kryteria:<p/>A. Rzeczywista szerokość przypisana do kolumny *-nigdy nie jest mniejsza niż jej minimalna szerokość ani większa niż jej maksymalna szerokość.<br/>B. Każda <em>kolumna, która nie ma przypisanej minimalnej lub maksymalnej szerokości, ma przypisaną szerokość proporcjonalną do jej <em>wagi. Aby były precyzyjne, jeśli dwie kolumny są zadeklarowane z szerokością x</em> i y</em> odpowiednio, a żadna kolumna nie otrzymuje minimalnej lub maksymalnej szerokości, rzeczywiste szerokości v i w są przypisane do kolumn są w tej samej proporcji: v/w = = x/y.<br/>C. Łączna szerokość przypisana do &quot; kolumn proporcjonalnych &quot; \* jest równa ilości dostępnego miejsca po przydzieleniu do ograniczonych kolumn (stałych, autoi \* -kolumn, które mają przydzieloną minimalną lub maksymalną szerokość). Może to być zero, na przykład jeśli suma minimalnej szerokości przekracza dostępną szerokość siatki.<br/>D. Wszystkie te instrukcje mają być interpretowane w odniesieniu do &quot; idealnego &quot; układu. Gdy zaokrąglanie układu jest stosowane, rzeczywiste szerokości mogą różnić się od idealnej szerokości o jeden piksel.<br/>Stary algorytm honoruje (A), ale nie mógł przestrzegać innych kryteriów w przypadkach przedstawionych powyżej.<p/>Wszystkie informacje dotyczące kolumn i szerokości w tym artykule mają zastosowanie również do wierszy i wysokości.

#### <a name="suggestion"></a>Sugestia

Domyślnie aplikacje przeznaczone dla wersji .NET Framework rozpoczynające się od .NET Framework 4,7 będą widziały nowy algorytm, natomiast aplikacje przeznaczone dla .NET Framework 4.6.2 lub starszych wersji będą widzieć stary algorytm.<p/>Aby zastąpić wartość domyślną, użyj następującego ustawienia konfiguracji:

<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Windows.Controls.Grid.StarDefinitionsCanExceedAvailableSpace=true&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>

Wartość `true` wybiera stary algorytm, `false` wybiera nowy algorytm.

| Nazwa    | Wartość       |
|:--------|:------------|
| Zakres   | Mały       |
| Wersja | 4.7         |
| Typ    | Przekierowanie |
