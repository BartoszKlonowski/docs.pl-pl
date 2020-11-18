---
title: Zgłaszanie wyjątku
ms.date: 10/22/2008
helpviewer_keywords:
- exceptions, throwing
- explicitly throwing exceptions
- throwing exceptions, design guidelines
ms.assetid: 5388e02b-52f5-460e-a2b5-eeafe60eeebe
ms.openlocfilehash: 6f22878a9ddfb394f6705a335930ef2cc270895f
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94821271"
---
# <a name="exception-throwing"></a>Zgłaszanie wyjątku
Zasady zgłaszania wyjątku opisane w tej sekcji wymagają odpowiedniej definicji znaczenia błędu wykonania. Niepowodzenie wykonywania występuje zawsze, gdy członek nie może wykonać czynności, do których został zaprojektowany (co oznacza nazwa elementu członkowskiego). Na przykład, jeśli `OpenFile` Metoda nie może zwrócić otwartego dojścia do pliku wywołującego, będzie traktowana jako błąd wykonania.

 Większość deweloperów była wygodna z użyciem wyjątków dla błędów użycia, takich jak dzielenie przez zero lub puste odwołania. W strukturze wyjątki są używane dla wszystkich warunków błędów, w tym błędów wykonania.

 ❌ NIE zwracają kodów błędów.

 Wyjątkiem są podstawowe metody raportowania błędów w strukturach.

 ✔️ wykonywanie raportów przez wyrzucanie wyjątków.

 ✔️ ROZWAŻYĆ zakończenie procesu przez wywołanie `System.Environment.FailFast` funkcji (.NET Framework 2,0) zamiast zgłaszania wyjątku, jeśli kod napotka sytuację, w której jest niebezpieczny do dalszej realizacji.

 ❌ NIE należy używać wyjątków dla normalnego przepływu sterowania, jeśli jest to możliwe.

 Z wyjątkiem awarii systemu i operacji z potencjalnymi warunkami wyścigu, projektanci struktury powinni projektować interfejsy API, aby użytkownicy mogli pisać kod, który nie zgłasza wyjątków. Na przykład można umożliwić sprawdzenie warunków wstępnych przed wywołaniem elementu członkowskiego, aby użytkownicy mogli pisać kod, który nie zgłasza wyjątków.

 Element członkowski używany do sprawdzania warunków wstępnych innego elementu członkowskiego jest często nazywany testerem, a element członkowski, który faktycznie wykonuje prace, nosi nazwę DOER.

 Istnieją przypadki, w których wzorzec Tester-Doer może mieć nieakceptowalne obciążenie wydajności. W takich przypadkach należy wziąć pod uwagę wzorzec tak zwany Try-Parse (zobacz [wyjątki i wydajność](exceptions-and-performance.md) , aby uzyskać więcej informacji).

 ✔️ ROZWAŻYĆ implikacje wydajności zgłaszania wyjątków. Stawki za 100 na sekundę mogą mieć zauważalny wpływ na wydajność większości aplikacji.

 ✔️ DO dokumentu wszystkie wyjątki zgłoszone przez publicznie wywoływanych członków z powodu naruszenia kontraktu elementu członkowskiego (a nie awarii systemu) i traktowania ich jako części kontraktu.

 Wyjątki, które są częścią kontraktu, nie powinny się zmieniać z jednej wersji na następną (tj. nie należy zmieniać typu wyjątku, a nowe wyjątki nie powinny być dodawane).

 ❌ NIE mają publicznych składowych, które mogą zgłosić lub nie na podstawie pewnej opcji.

 ❌ NIE mają publicznych składowych, które zwracają wyjątki jako wartość zwrotną lub `out` parametr.

 Zwracanie wyjątków z publicznych interfejsów API zamiast zgłaszania ich przez wiele zalet raportowania błędów opartych na wyjątkach.

 ✔️ ROZWAŻYĆ użycie metod konstruktora wyjątków.

 Często należy zgłosić ten sam wyjątek z różnych miejsc. Aby uniknąć przeładowanie kodu, należy użyć metod pomocnika, które tworzą wyjątki i inicjują ich właściwości.

 Ponadto elementy członkowskie, które generują wyjątki, nie są obsługiwane. Przeniesienie instrukcji throw wewnątrz konstruktora może pozwolić, aby element członkowski był wbudowany.

 ❌ NIE zgłaszaj wyjątków z bloków filtru wyjątków.

 Gdy filtr wyjątku zgłasza wyjątek, wyjątek jest przechwytywany przez środowisko CLR, a filtr zwraca wartość false. Takie zachowanie jest odróżnienie od wykonywanych przez filtr i zwraca wartość false, dlatego trudno jest debugować.

 ❌ UNIKAj jawnego zgłaszania wyjątków z bloków finally. Niejawnie zgłoszone wyjątki powstałe w wyniku wywoływania metod wywołujących są akceptowalne.

 *Fragmenty © 2005, 2009 Microsoft Corporation. Wszelkie prawa zastrzeżone.*

 *Ponownie Wydrukowano przez uprawnienie Pearson Education, Inc. z [wytycznych dotyczących projektowania platformy: konwencje, idiomy i wzorce dla bibliotek .NET do wielokrotnego użytku, 2. wydanie](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) przez Krzysztof Cwalina i Brad Abrams, opublikowane 22, 2008 przez Addison-Wesley Professional w ramach serii Microsoft Windows Development.*

## <a name="see-also"></a>Zobacz także

- [Wskazówki dotyczące projektowania struktury](index.md)
- [Wyjątki — zalecenia dotyczące projektowania](exceptions.md)
