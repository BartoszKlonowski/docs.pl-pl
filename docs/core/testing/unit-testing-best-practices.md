---
title: Najlepsze rozwiązania dotyczące pisania testów jednostkowych
description: Zapoznaj się z najlepszymi rozwiązaniami dotyczącymi pisania testów jednostkowych, które zapewniają jakość kodu i odporność na projekty platformy .NET Core i .NET Standard.
author: jpreese
ms.author: wiwagn
ms.date: 07/28/2018
ms.openlocfilehash: 56f51cde0e52a9e6a38e5291c81470beee61adef
ms.sourcegitcommit: 4b79862c5b41fbd86cf38f926f6a49516059f6f2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/18/2020
ms.locfileid: "97678107"
---
# <a name="unit-testing-best-practices-with-net-core-and-net-standard"></a>Najlepsze rozwiązania dotyczące testów jednostkowych przy użyciu platformy .NET Core i .NET Standard

Istnieje wiele korzyści związanych z pisaniem testów jednostkowych; ułatwiają one regresję, dostarczenie dokumentacji i ułatwiają dobre projektowanie. Jednak trudno odczytać i kruchy testy jednostkowe mogą Wreak destabilizować w bazie kodu. W tym artykule opisano niektóre najlepsze rozwiązania dotyczące projektu testów jednostkowych dla projektów .NET Core i .NET Standard.

W tym przewodniku przedstawiono niektóre najlepsze rozwiązania podczas pisania testów jednostkowych w celu zapewnienia odporności i łatwego zrozumienia testów.

[Jan Reese](https://reese.dev) z specjalne podziękowaniami do [Roy Osherove](https://osherove.com/)

## <a name="why-unit-test"></a>Dlaczego test jednostkowy?

### <a name="less-time-performing-functional-tests"></a>Krótszy czas wykonywania testów funkcjonalnych

Testy funkcjonalne są kosztowne. Zwykle wymagają otwarcia aplikacji i wykonania serii czynności, które należy wykonać (lub kogoś innego), aby sprawdzić oczekiwane zachowanie. Te kroki mogą być nieznane dla testera, co oznacza, że będą musieli skontaktować się z inną osobą w obszarze w celu przeprowadzenia testu. Testowanie może potrwać kilka sekund lub kilka minut w przypadku większych zmian. Na koniec należy powtórzyć ten proces dla każdej zmiany wprowadzonej w systemie.

Testy jednostkowe, z drugiej strony, pozostaną w milisekundach, mogą być uruchamiane przy naciśnięciu przycisku i niekoniecznie wymagają żadnej wiedzy o systemie. Niezależnie od tego, czy test lub czy nie działa, jest do modułu uruchamiającego testy, a nie do osoby.

### <a name="protection-against-regression"></a>Ochrona przed regresją

Wady regresji to wady wprowadzane po wprowadzeniu zmian w aplikacji. Jest ona wspólna dla testerów, aby nie tylko testować swoją nową funkcję, ale również funkcje, które wcześniej istniały w celu sprawdzenia, czy poprzednio zaimplementowane funkcje nadal działają zgodnie z oczekiwaniami.

W przypadku testów jednostkowych możliwe jest ponowne uruchomienie całego pakietu testów po każdej kompilacji lub nawet po zmianie wiersza kodu. Zapewnianie pewności, że nowy kod nie przerywa istniejących funkcji.

### <a name="executable-documentation"></a>Dokumentacja pliku wykonywalnego

Może to nie zawsze być oczywisty sposób działania określonej metody lub jej zachowania. Użytkownik może zadawać sobie: jak działa ta metoda, jeśli przekażę pusty ciąg? Null?

Jeśli masz zestaw dobrze wymienionych testów jednostkowych, każdy test powinien być w stanie jasno wyjaśnić oczekiwane dane wyjściowe dla danego danych wejściowych. Ponadto powinno być możliwe zweryfikowanie, czy faktycznie działa.

### <a name="less-coupled-code"></a>Mniej połączony kod

Gdy kod jest ściśle sprzężony, może być trudne do testowania jednostkowego. Bez tworzenia testów jednostkowych dla kodu, który piszesz, Sprzęg może być mniej widoczny.

Pisanie testów dla kodu spowoduje naturalnie oddzielenie kodu, ponieważ byłoby trudniejsze do przetestowania w przeciwnym razie.

## <a name="characteristics-of-a-good-unit-test"></a>Cechy dobrego testu jednostkowego

- **Szybko**. Niespotykane projekty mają tysiące testów jednostkowych. Testy jednostkowe powinny trwać bardzo mało czasu. ).
- **Izolowane**. Testy jednostkowe są autonomiczne, mogą być uruchamiane w izolacji i nie mogą być zależne od jakichkolwiek czynników zewnętrznych, takich jak system plików czy baza danych.
- **Powtarzalne**. Uruchamianie testu jednostkowego powinno być zgodne z jego wynikami, to oznacza, że zawsze zwraca ten sam wynik, jeśli nie zmieni się niczego między przebiegami.
- **Sprawdzanie samoobsługowe**. Test powinien być w stanie automatycznie wykryć, czy zakończył się powodzeniem, bez ingerencji człowieka.
- **Czasowo**. Test jednostkowy nie powinien trwać bardzo proporcjonalnie do zapisu w porównaniu z testowanym kodem. Jeśli okaże się, że test kodu zajmuje dużo czasu w porównaniu do pisania kodu, weź pod uwagę projekt, który jest bardziej weryfikowalne.

## <a name="code-coverage"></a>Pokrycie kodu

Wysoka wartość procentowa pokrycia kodu jest często skojarzona z wyższą jakością kodu. Jednak sama pomiar *nie może* ustalić jakości kodu. Ustawienie nadwyżkowej wartości procentowej pokrycia kodu ambitne podejście może być counterproductive. Wyobraź sobie złożony projekt z tysiącami gałęzi warunkowych i Wyobraź sobie, że ustawisz cel pokrycia kodu o 95%. Obecnie projekt zachowuje pokrycie kodu w 90%. Czas potrzebny na uwzględnienie wszystkich przypadków brzegowych w pozostałej części 5% może być ogromnym przedsięwzięciem, a jej wartość jest szybko zmniejszana.

Wysoki procent pokrycia kodu nie jest wskaźnikiem sukcesu ani nie ma wysokiej jakości kodu. Reprezentuje ona jedynie ilość kodu, która jest objęta testami jednostkowymi. Aby uzyskać więcej informacji, zobacz temat [pokrycie kodu testu jednostkowego](unit-testing-code-coverage.md).

## <a name="lets-speak-the-same-language"></a>Zacznijmy od tego samego języka

W przypadku korzystania z testów *często występuje* niedziałający sposób. Następujące punkty definiują najpopularniejsze *typy elementów* sztucznych podczas pisania testów jednostkowych:

*Sfałszowane* — jest to ogólny termin, który może służyć do opisywania obiektu zastępczego lub makiety. Bez względu na to, czy jest to element zastępczy, czy makieta zależy od kontekstu, w którym jest używana. Inaczej mówiąc, może to być szczątk lub makieta.

*Makieta* — obiekt obiektu jest obiektem nieprawidłowym w systemie, który decyduje o tym, czy test jednostkowy zakończył się powodzeniem, czy nie. Makieta jest uruchamiana jako fałszywa, dopóki nie zostanie potwierdzona.

*Szczątkowy* — zastępczy to przeprowadzona zmiana dla istniejącej zależności (lub współpracownika) w systemie. Za pomocą klasy zastępczej można testować kod bez bezpośredniej kontroli nad zależnością. Domyślnie element zastępczy jest uruchamiany jako sfałszowany.

Rozważmy następujący fragment kodu:

```csharp
var mockOrder = new MockOrder();
var purchase = new Purchase(mockOrder);

purchase.ValidateOrders();

Assert.True(purchase.CanBeShipped);
```

Może to być przykład klasy zastępczej, która jest nazywana makietą. W tym przypadku jest to element zastępczy. Nastąpi przekazanie w kolejności jako środek, aby można było utworzyć wystąpienie `Purchase` (system testowy). Nazwa `MockOrder` jest również myląca, ponieważ nie jest to makieta.

Lepszym rozwiązaniem będzie

```csharp
var stubOrder = new FakeOrder();
var purchase = new Purchase(stubOrder);

purchase.ValidateOrders();

Assert.True(purchase.CanBeShipped);
```

Zmieniając nazwę klasy na, została `FakeOrder` utworzona bardziej generyczna Klasa, Klasa może być używana jako imitacja lub element zastępczy. W zależności od tego do przypadku testowego. W powyższym przykładzie `FakeOrder` jest używany jako zastępczy. Nie używasz `FakeOrder` w żadnym kształcie ani formularzu podczas potwierdzeń. `FakeOrder` został przesłany do `Purchase` klasy w celu spełnienia wymagań konstruktora.

Aby użyć go jako makiety, możesz zrobić coś podobnego do tego

```csharp
var mockOrder = new FakeOrder();
var purchase = new Purchase(mockOrder);

purchase.ValidateOrders();

Assert.True(mockOrder.Validated);
```

W tym przypadku sprawdzasz właściwość dla fałszywego (potwierdzania), więc w powyższym fragmencie kodu `mockOrder` jest to makieta.

> [!IMPORTANT]
> Ważne jest, aby zapewnić poprawną terminologię. Jeśli wywołujesz obiekty zastępcze "makiety", inni deweloperzy będą wprowadzać fałszywe założenia dotyczące zamiaru.

Głównym elementem, który należy pamiętać o makietach i fragmentów, jest to, że makiety są tak samo jak wycinki

## <a name="best-practices"></a>Najlepsze rozwiązania

Nie należy wprowadzać zależności od infrastruktury podczas pisania testów jednostkowych. Te testy są powolne i kruchy i powinny być zarezerwowane dla testów integracji. Można uniknąć tych zależności w aplikacji, postępując zgodnie z [zasadami jawnych zależności](https://deviq.com/explicit-dependencies-principle) i przy użyciu [iniekcji zależności](../extensions/dependency-injection.md). Możesz również utrzymać testy jednostkowe w osobnym projekcie od testów integracji. Gwarantuje to, że projekt testu jednostkowego nie zawiera odwołań do pakietów infrastruktury ani ich zależności.

### <a name="naming-your-tests"></a>Nazywanie testów

Nazwa testu powinna składać się z trzech części:

- Nazwa testowanej metody.
- Scenariusz, w którym jest testowany.
- Oczekiwane zachowanie, gdy scenariusz jest wywoływany.

#### <a name="why"></a>Dlaczego?

- Wzorce nazewnictwa są ważne, ponieważ wyraźnie wyrażają intencję testu.

Testy są większe niż tylko w celu upewnienia się, że kod działa, ale również zawiera dokumentację. Wystarczy, że szukasz zestawu testów jednostkowych, można wywnioskować zachowanie kodu bez konieczności przeglądania kodu. Ponadto, gdy testy zakończą się niepowodzeniem, można zobaczyć, które scenariusze nie spełniają oczekiwań.

#### <a name="bad"></a>Źle:

[!code-csharp[BeforeNaming](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/before/StringCalculatorTests.cs#BeforeNaming)]

#### <a name="better"></a>Bardziej

[!code-csharp[AfterNamingAndMinimallyPassing](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/after/StringCalculatorTests.cs#AfterNamingAndMinimallyPassing)]

### <a name="arranging-your-tests"></a>Rozmieszczanie testów

**Rozmieść, Act, Assert** jest typowym wzorcem podczas testowania jednostkowego. Jak nazwa oznacza, składa się z trzech głównych akcji:

- *Rozmieszczanie* obiektów, tworzenie i konfigurowanie ich w razie potrzeby.
- *Działanie* na obiekcie.
- *Potwierdź* , że coś jest zgodnie z oczekiwaniami.

#### <a name="why"></a>Dlaczego?

- Wyraźnie oddzieli to, co jest testowane z kroków *rozmieszczenia* i *potwierdzeń* .
- Mniejsza szansa, aby Intermix potwierdzenia z kodem "Act".

Czytelność to jeden z najważniejszych aspektów związanych z pisaniem testu. Oddzielenie każdej z tych akcji w ramach testu wyraźnie podkreśla zależności wymagane do wywołania kodu, sposobu wywoływania kodu i tego, co próbujesz przedstawić. Chociaż może być możliwe połączenie niektórych kroków i zmniejszenie rozmiaru testu, głównym celem jest przeprowadzenie testu jako możliwego do odczytania.

#### <a name="bad"></a>Źle:

[!code-csharp[BeforeArranging](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/before/StringCalculatorTests.cs#BeforeArranging)]

#### <a name="better"></a>Bardziej

[!code-csharp[AfterArranging](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/after/StringCalculatorTests.cs#AfterArranging)]

### <a name="write-minimally-passing-tests"></a>Zapisz minimalnie przekazanie testów

Dane wejściowe do użycia w teście jednostkowym powinny być najprostszym możliwym do zweryfikowania zachowania, które jest obecnie testowane.

#### <a name="why"></a>Dlaczego?

- Testy stają się bardziej odporne na przyszłe zmiany w bazie kodu.
- Bliżej działania testowania nad implementacją.

Testy, które zawierają więcej informacji, niż jest to wymagane do przekazania testu, mają większą szansę na wprowadzenie błędów do testu i mogą sprawić, że zamiar testu jest mniej oczywisty. Podczas pisania testów należy skoncentrować się na zachowaniu. Ustawienie dodatkowych właściwości dla modeli lub użycie niezerowych wartości, gdy nie jest to wymagane, powoduje tylko rozciąganie z tego, co próbujesz udowodnić.

#### <a name="bad"></a>Źle:

[!code-csharp[BeforeMinimallyPassing](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/before/StringCalculatorTests.cs#BeforeMinimallyPassing)]

#### <a name="better"></a>Bardziej

[!code-csharp[AfterNamingAndMinimallyPassing](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/after/StringCalculatorTests.cs#AfterNamingAndMinimallyPassing)]

### <a name="avoid-magic-strings"></a>Unikaj ciągów Magic

Zmienne nazewnictwa w testach jednostkowych są ważne, jeśli nie są ważniejsze niż zmienne nazw w kodzie produkcyjnym. Testy jednostkowe nie powinny zawierać ciągów Magic.

#### <a name="why"></a>Dlaczego?

- Zapobiega potrzebom czytnika testów w celu sprawdzenia kodu produkcyjnego w celu ustalenia, co sprawia, że wartość jest specjalna.
- Jawnie pokazuje, co próbujesz *udowodnić* , zamiast podejmować próbę *wykonania*.

Ciągi Magic mogą spowodować pomyłkę dla czytnika testów. Jeśli ciąg wyróżni się od zwykłego, może się zastanawiać, dlaczego określona wartość została wybrana dla parametru lub wartości zwracanej. Może to prowadzić do bliższego przyjrzeć się szczegółowym informacjom dotyczącym implementacji, zamiast skupić się na teście.

> [!TIP]
> Podczas pisania testów należy zamierzyć możliwie jak najwięcej założeń. W przypadku ciągów magicznych dobrym rozwiązaniem jest przypisanie tych wartości do stałych.

#### <a name="bad"></a>Źle:

[!code-csharp[BeforeMagicString](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/before/StringCalculatorTests.cs#BeforeMagicString)]

#### <a name="better"></a>Bardziej

[!code-csharp[AfterMagicString](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/after/StringCalculatorTests.cs#AfterMagicString)]

### <a name="avoid-logic-in-tests"></a>Unikanie logiki w testach

Podczas pisania testów jednostkowych należy unikać ręcznego łączenia ciągów i warunków logicznych, takich jak,,, `if` `while` `for` `switch` itd.

#### <a name="why"></a>Dlaczego?

- Mniejsza szansa, aby wprowadzić usterkę w testach.
- Skup się na wyniku końca, a nie w szczegółach implementacji.

Gdy wprowadzasz logikę do zestawu testów, szansa na ich zwiększenie znacznie rośnie. Ostatnim miejscem, w którym chcesz znaleźć usterkę, jest zestaw testów. Należy mieć wysoki poziom pewności, że testy działają, w przeciwnym razie nie będzie można ich ufać. Testy, które nie są zaufane, nie zapewniają żadnej wartości. Gdy test zakończy się niepowodzeniem, warto mieć sens, że coś w rzeczywistości jest nieprawidłowe w kodzie i że nie można go zignorować.

> [!TIP]
> Jeśli logika w teście wydaje się nienieunikniona, rozważ podzielenie testu na dwa lub więcej różnych testów.

#### <a name="bad"></a>Źle:

[!code-csharp[LogicInTests](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/before/StringCalculatorTests.cs#LogicInTests)]

#### <a name="better"></a>Bardziej

[!code-csharp[AfterTestLogic](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/after/StringCalculatorTests.cs#AfterTestLogic)]

### <a name="prefer-helper-methods-to-setup-and-teardown"></a>Preferuj metody pomocnika do instalacji i usuwania

Jeśli potrzebujesz podobnego obiektu lub stanu dla testów, Preferuj metodę pomocnika, która jest używana, `Setup` `Teardown` Jeśli istnieją.

#### <a name="why"></a>Dlaczego?

- Mniej pomyłek podczas odczytywania testów, ponieważ cały kod jest widoczny w ramach każdego testu.
- Mniejsza szansa, że zbyt wiele lub zbyt mała dla danego testu.
- Mniejsza szansa stanu udostępniania między testami, która tworzy niepożądane zależności między nimi.

W strukturach testów jednostkowych `Setup` jest wywoływana przed każdym testem jednostkowym w ramach zestawu testów. Niektóre mogą być widoczne jako przydatne narzędzia, zazwyczaj kończą się wiodącym bloated i trudnym do odczytania testów. Każdy test ma zwykle różne wymagania, aby można było je uruchomić. Niestety, `Setup` wymusza użycie dokładnie tych samych wymagań dla każdego testu.

> [!NOTE]
> xUnit usunął zarówno Instalatora, jak i usuwania w wersji 2. x

#### <a name="bad"></a>Źle:

[!code-csharp[BeforeSetup](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/before/StringCalculatorTests.cs#BeforeSetup)]

```csharp
// more tests...
```

[!code-csharp[BeforeHelperMethod](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/before/StringCalculatorTests.cs#BeforeHelperMethod)]

#### <a name="better"></a>Bardziej

[!code-csharp[AfterHelperMethod](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/after/StringCalculatorTests.cs#AfterHelperMethod)]

```csharp
// more tests...
```

[!code-csharp[AfterSetup](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/after/StringCalculatorTests.cs#AfterSetup)]

### <a name="avoid-multiple-asserts"></a>Unikaj wielu potwierdzeń

Podczas pisania testów, spróbuj uwzględnić tylko jedno potwierdzenie na test. Typowe podejścia do korzystania tylko z jednego potwierdzenia obejmują:

- Utwórz oddzielny test dla każdego potwierdzenia.
- Użyj testów sparametryzowanych.

#### <a name="why"></a>Dlaczego?

- Jeśli jedno potwierdzenie nie powiedzie się, kolejne potwierdzenia nie zostaną ocenione.
- Gwarantuje, że nie postanowisz wielu przypadków w testach.
- Zapewnia cały obraz, dlaczego testy kończą się niepowodzeniem.

W przypadku wprowadzenia wielu potwierdzeń do przypadku testowego nie ma gwarancji, że wszystkie potwierdzenia zostaną wykonane. W większości platform testów jednostkowych, gdy potwierdzenie kończy się niepowodzeniem w teście jednostkowym, testy postępu są automatycznie uważane za zakończone niepowodzeniem. Może to być mylące, ponieważ funkcje, które faktycznie działają, będą wyświetlane jako niepowodzenie.

> [!NOTE]
> Typowym wyjątkiem od tej reguły jest potwierdzenie obiektu. W takim przypadku ogólnie akceptowalne jest posiadanie wielu potwierdzeń dla każdej właściwości, aby upewnić się, że obiekt znajduje się w stanie, w którym oczekujesz.

#### <a name="bad"></a>Źle:

[!code-csharp[BeforeMultipleAsserts](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/before/StringCalculatorTests.cs#BeforeMultipleAsserts)]

#### <a name="better"></a>Bardziej

[!code-csharp[AfterMultipleAsserts](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/after/StringCalculatorTests.cs#AfterMultipleAsserts)]

### <a name="validate-private-methods-by-unit-testing-public-methods"></a>Weryfikowanie metod prywatnych według metod publicznych testów jednostkowych

W większości przypadków nie powinno być konieczne przetestowanie metody prywatnej. Metody prywatne są szczegółami implementacji. Można to traktować w ten sposób: metody prywatne nigdy nie istnieją w izolacji. W pewnym momencie istnieje metoda publiczna, która wywołuje metodę prywatną w ramach jej implementacji. Informacje o tym, co należy wiedzieć, to wynik metody publicznej, która wywołuje do prywatnego.

Rozważmy następujący przypadek

```csharp
public string ParseLogLine(string input)
{
    var sanitizedInput = TrimInput(input);
    return sanitizedInput;
}

private string TrimInput(string input)
{
    return input.Trim();
}
```

Pierwszą odpowiedzią może być rozpoczęcie pisania testu dla `TrimInput` , ponieważ chcesz upewnić się, że metoda działa zgodnie z oczekiwaniami. Jednak jest on w pełni możliwy, aby `ParseLogLine` manipulować `sanitizedInput` w taki sposób, że nie jest to oczekiwane, renderowanie testu przed `TrimInput` bezużyteczny.

Rzeczywisty test powinien być wykonywany w oparciu o publiczną metodę dodaną `ParseLogLine` , ponieważ to to, co powinno być ostatecznie ważne.

```csharp
public void ParseLogLine_StartsAndEndsWithSpace_ReturnsTrimmedResult()
{
    var parser = new Parser();

    var result = parser.ParseLogLine(" a ");

    Assert.Equals("a", result);
}
```

Jeśli w tym obszarze widać, że jest wyświetlana Metoda prywatna, Znajdź metodę publiczną i napisz testy dla tej metody. Tylko dlatego, że Metoda prywatna zwraca oczekiwany wynik, nie oznacza, że system, który ostatecznie wywołuje metodę prywatną, użyje poprawnego wyniku.

### <a name="stub-static-references"></a>Zastępcze odwołania statyczne

Jedną z zasad testów jednostkowych jest to, że musi ona mieć pełną kontrolę nad testowanym systemem. Może to być problematyczne, gdy kod produkcyjny zawiera wywołania do odwołań statycznych (na przykład `DateTime.Now` ). Rozważmy następujący kod

```csharp
public int GetDiscountedPrice(int price)
{
    if (DateTime.Now.DayOfWeek == DayOfWeek.Tuesday)
    {
        return price / 2;
    }
    else
    {
        return price;
    }
}
```

Jak ten kod może być testowany jednostkowo? Możesz wypróbować takie podejście jak

```csharp
public void GetDiscountedPrice_NotTuesday_ReturnsFullPrice()
{
    var priceCalculator = new PriceCalculator();

    var actual = priceCalculator.GetDiscountedPrice(2);

    Assert.Equals(2, actual)
}

public void GetDiscountedPrice_OnTuesday_ReturnsHalfPrice()
{
    var priceCalculator = new PriceCalculator();

    var actual = priceCalculator.GetDiscountedPrice(2);

    Assert.Equals(1, actual);
}
```

Niestety, możesz szybko zapamiętać, że istnieje kilka problemów z testami.

- Jeśli zestaw testów jest uruchamiany w wtorek, drugi test zostanie przekazany, ale pierwszy test zakończy się niepowodzeniem.
- Jeśli zestaw testów jest uruchamiany z dowolnego innego dnia, pierwszy test zostanie przekazany, ale drugi test zakończy się niepowodzeniem.

Aby rozwiązać te problemy, należy wprowadzić *szew* w kodzie produkcyjnym. Jednym z metod jest Zawijanie kodu, który należy kontrolować w interfejsie i że kod produkcyjny zależy od tego interfejsu.

```csharp
public interface IDateTimeProvider
{
    DayOfWeek DayOfWeek();
}

public int GetDiscountedPrice(int price, IDateTimeProvider dateTimeProvider)
{
    if (dateTimeProvider.DayOfWeek() == DayOfWeek.Tuesday)
    {
        return price / 2;
    }
    else
    {
        return price;
    }
}
```

Zestaw testów zostanie teraz

```csharp
public void GetDiscountedPrice_NotTuesday_ReturnsFullPrice()
{
    var priceCalculator = new PriceCalculator();
    var dateTimeProviderStub = new Mock<IDateTimeProvider>();
    dateTimeProviderStub.Setup(dtp => dtp.DayOfWeek()).Returns(DayOfWeek.Monday);

    var actual = priceCalculator.GetDiscountedPrice(2, dateTimeProviderStub);

    Assert.Equals(2, actual);
}

public void GetDiscountedPrice_OnTuesday_ReturnsHalfPrice()
{
    var priceCalculator = new PriceCalculator();
    var dateTimeProviderStub = new Mock<IDateTimeProvider>();
    dateTimeProviderStub.Setup(dtp => dtp.DayOfWeek()).Returns(DayOfWeek.Tuesday);

    var actual = priceCalculator.GetDiscountedPrice(2, dateTimeProviderStub);

    Assert.Equals(1, actual);
}
```

Teraz zestaw testów ma pełną kontrolę nad `DateTime.Now` i może być dowolną wartością podczas wywoływania metody.
