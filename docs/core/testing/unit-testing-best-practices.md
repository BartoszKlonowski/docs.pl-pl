---
title: Najlepsze rozwiązania dotyczące pisania testów jednostkowych
description: Zapoznaj się z najlepszymi rozwiązaniami dotyczącymi pisania testów jednostkowych, które zapewniają jakość kodu i odporność na projekty platformy .NET Core i .NET Standard.
author: jpreese
ms.author: wiwagn
ms.date: 07/28/2018
ms.openlocfilehash: ffeaa1e11512cab64695c120f844594b8c5014a8
ms.sourcegitcommit: 97ce5363efa88179dd76e09de0103a500ca9b659
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/13/2020
ms.locfileid: "86281111"
---
# <a name="unit-testing-best-practices-with-net-core-and-net-standard"></a><span data-ttu-id="62d2b-103">Najlepsze rozwiązania dotyczące testów jednostkowych przy użyciu platformy .NET Core i .NET Standard</span><span class="sxs-lookup"><span data-stu-id="62d2b-103">Unit testing best practices with .NET Core and .NET Standard</span></span>

<span data-ttu-id="62d2b-104">Istnieje wiele korzyści związanych z pisaniem testów jednostkowych; ułatwiają one regresję, dostarczenie dokumentacji i ułatwiają dobre projektowanie.</span><span class="sxs-lookup"><span data-stu-id="62d2b-104">There are numerous benefits to writing unit tests; they help with regression, provide documentation, and facilitate good design.</span></span> <span data-ttu-id="62d2b-105">Jednak trudno odczytać i kruchy testy jednostkowe mogą Wreak destabilizować w bazie kodu.</span><span class="sxs-lookup"><span data-stu-id="62d2b-105">However, hard to read and brittle unit tests can wreak havoc on your code base.</span></span> <span data-ttu-id="62d2b-106">W tym artykule opisano niektóre najlepsze rozwiązania dotyczące projektu testów jednostkowych dla projektów .NET Core i .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="62d2b-106">This article describes some best practices regarding unit test design for your .NET Core and .NET Standard projects.</span></span>

<span data-ttu-id="62d2b-107">W tym przewodniku przedstawiono niektóre najlepsze rozwiązania podczas pisania testów jednostkowych w celu zapewnienia odporności i łatwego zrozumienia testów.</span><span class="sxs-lookup"><span data-stu-id="62d2b-107">In this guide, you'll learn some best practices when writing unit tests to keep your tests resilient and easy to understand.</span></span>

<span data-ttu-id="62d2b-108">[Jan Reese](https://reese.dev) z specjalne podziękowaniami do [Roy Osherove](https://osherove.com/)</span><span class="sxs-lookup"><span data-stu-id="62d2b-108">By [John Reese](https://reese.dev) with special thanks to [Roy Osherove](https://osherove.com/)</span></span>

## <a name="why-unit-test"></a><span data-ttu-id="62d2b-109">Dlaczego test jednostkowy?</span><span class="sxs-lookup"><span data-stu-id="62d2b-109">Why unit test?</span></span>

### <a name="less-time-performing-functional-tests"></a><span data-ttu-id="62d2b-110">Krótszy czas wykonywania testów funkcjonalnych</span><span class="sxs-lookup"><span data-stu-id="62d2b-110">Less time performing functional tests</span></span>

<span data-ttu-id="62d2b-111">Testy funkcjonalne są kosztowne.</span><span class="sxs-lookup"><span data-stu-id="62d2b-111">Functional tests are expensive.</span></span> <span data-ttu-id="62d2b-112">Zwykle wymagają otwarcia aplikacji i wykonania serii czynności, które należy wykonać (lub kogoś innego), aby sprawdzić oczekiwane zachowanie.</span><span class="sxs-lookup"><span data-stu-id="62d2b-112">They typically involve opening up the application and performing a series of steps that you (or someone else), must follow in order to validate the expected behavior.</span></span> <span data-ttu-id="62d2b-113">Te kroki mogą być nieznane dla testera, co oznacza, że będą musieli skontaktować się z inną osobą w obszarze w celu przeprowadzenia testu.</span><span class="sxs-lookup"><span data-stu-id="62d2b-113">These steps may not always be known to the tester, which means they will have to reach out to someone more knowledgeable in the area in order to carry out the test.</span></span> <span data-ttu-id="62d2b-114">Testowanie może potrwać kilka sekund lub kilka minut w przypadku większych zmian.</span><span class="sxs-lookup"><span data-stu-id="62d2b-114">Testing itself could take seconds for trivial changes, or minutes for larger changes.</span></span> <span data-ttu-id="62d2b-115">Na koniec należy powtórzyć ten proces dla każdej zmiany wprowadzonej w systemie.</span><span class="sxs-lookup"><span data-stu-id="62d2b-115">Lastly, this process must be repeated for every change that you make in the system.</span></span>

<span data-ttu-id="62d2b-116">Testy jednostkowe, z drugiej strony, pozostaną w milisekundach, mogą być uruchamiane przy naciśnięciu przycisku i niekoniecznie wymagają żadnej wiedzy o systemie.</span><span class="sxs-lookup"><span data-stu-id="62d2b-116">Unit tests, on the other hand, take milliseconds, can be run at the press of a button, and don't necessarily require any knowledge of the system at large.</span></span> <span data-ttu-id="62d2b-117">Niezależnie od tego, czy test lub czy nie działa, jest do modułu uruchamiającego testy, a nie do osoby.</span><span class="sxs-lookup"><span data-stu-id="62d2b-117">Whether or not the test passes or fails is up to the test runner, not the individual.</span></span>

### <a name="protection-against-regression"></a><span data-ttu-id="62d2b-118">Ochrona przed regresją</span><span class="sxs-lookup"><span data-stu-id="62d2b-118">Protection against regression</span></span>

<span data-ttu-id="62d2b-119">Wady regresji to wady wprowadzane po wprowadzeniu zmian w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="62d2b-119">Regression defects are defects that are introduced when a change is made to the application.</span></span> <span data-ttu-id="62d2b-120">Jest ona wspólna dla testerów, aby nie tylko testować swoją nową funkcję, ale również funkcje, które wcześniej istniały w celu sprawdzenia, czy poprzednio zaimplementowane funkcje nadal działają zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="62d2b-120">It is common for testers to not only test their new feature but also features that existed beforehand in order to verify that previously implemented features still function as expected.</span></span>

<span data-ttu-id="62d2b-121">W przypadku testów jednostkowych możliwe jest ponowne uruchomienie całego pakietu testów po każdej kompilacji lub nawet po zmianie wiersza kodu.</span><span class="sxs-lookup"><span data-stu-id="62d2b-121">With unit testing, it's possible to rerun your entire suite of tests after every build or even after you change a line of code.</span></span> <span data-ttu-id="62d2b-122">Zapewnianie pewności, że nowy kod nie przerywa istniejących funkcji.</span><span class="sxs-lookup"><span data-stu-id="62d2b-122">Giving you confidence that your new code does not break existing functionality.</span></span>

### <a name="executable-documentation"></a><span data-ttu-id="62d2b-123">Dokumentacja pliku wykonywalnego</span><span class="sxs-lookup"><span data-stu-id="62d2b-123">Executable documentation</span></span>

<span data-ttu-id="62d2b-124">Może to nie zawsze być oczywisty sposób działania określonej metody lub jej zachowania.</span><span class="sxs-lookup"><span data-stu-id="62d2b-124">It may not always be obvious what a particular method does or how it behaves given a certain input.</span></span> <span data-ttu-id="62d2b-125">Użytkownik może zadawać sobie: jak działa ta metoda, jeśli przekażę pusty ciąg?</span><span class="sxs-lookup"><span data-stu-id="62d2b-125">You may ask yourself: How does this method behave if I pass it a blank string?</span></span> <span data-ttu-id="62d2b-126">Null?</span><span class="sxs-lookup"><span data-stu-id="62d2b-126">Null?</span></span>

<span data-ttu-id="62d2b-127">Jeśli masz zestaw dobrze wymienionych testów jednostkowych, każdy test powinien być w stanie jasno wyjaśnić oczekiwane dane wyjściowe dla danego danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="62d2b-127">When you have a suite of well-named unit tests, each test should be able to clearly explain the expected output for a given input.</span></span> <span data-ttu-id="62d2b-128">Ponadto powinno być możliwe zweryfikowanie, czy faktycznie działa.</span><span class="sxs-lookup"><span data-stu-id="62d2b-128">In addition, it should be able to verify that it actually works.</span></span>

### <a name="less-coupled-code"></a><span data-ttu-id="62d2b-129">Mniej połączony kod</span><span class="sxs-lookup"><span data-stu-id="62d2b-129">Less coupled code</span></span>

<span data-ttu-id="62d2b-130">Gdy kod jest ściśle sprzężony, może być trudne do testowania jednostkowego.</span><span class="sxs-lookup"><span data-stu-id="62d2b-130">When code is tightly coupled, it can be difficult to unit test.</span></span> <span data-ttu-id="62d2b-131">Bez tworzenia testów jednostkowych dla kodu, który piszesz, Sprzęg może być mniej widoczny.</span><span class="sxs-lookup"><span data-stu-id="62d2b-131">Without creating unit tests for the code that you're writing, coupling may be less apparent.</span></span>

<span data-ttu-id="62d2b-132">Pisanie testów dla kodu spowoduje naturalnie oddzielenie kodu, ponieważ byłoby trudniejsze do przetestowania w przeciwnym razie.</span><span class="sxs-lookup"><span data-stu-id="62d2b-132">Writing tests for your code will naturally decouple your code, because it would be more difficult to test otherwise.</span></span>

## <a name="characteristics-of-a-good-unit-test"></a><span data-ttu-id="62d2b-133">Cechy dobrego testu jednostkowego</span><span class="sxs-lookup"><span data-stu-id="62d2b-133">Characteristics of a good unit test</span></span>

- <span data-ttu-id="62d2b-134">**Szybko**.</span><span class="sxs-lookup"><span data-stu-id="62d2b-134">**Fast**.</span></span> <span data-ttu-id="62d2b-135">Niespotykane projekty mają tysiące testów jednostkowych.</span><span class="sxs-lookup"><span data-stu-id="62d2b-135">It is not uncommon for mature projects to have thousands of unit tests.</span></span> <span data-ttu-id="62d2b-136">Testy jednostkowe powinny trwać bardzo mało czasu.</span><span class="sxs-lookup"><span data-stu-id="62d2b-136">Unit tests should take very little time to run.</span></span> <span data-ttu-id="62d2b-137">).</span><span class="sxs-lookup"><span data-stu-id="62d2b-137">Milliseconds.</span></span>
- <span data-ttu-id="62d2b-138">**Izolowany**.</span><span class="sxs-lookup"><span data-stu-id="62d2b-138">**Isolated**.</span></span> <span data-ttu-id="62d2b-139">Testy jednostkowe są autonomiczne, mogą być uruchamiane w izolacji i nie mogą być zależne od jakichkolwiek czynników zewnętrznych, takich jak system plików czy baza danych.</span><span class="sxs-lookup"><span data-stu-id="62d2b-139">Unit tests are standalone, can be run in isolation, and have no dependencies on any outside factors such as a file system or database.</span></span>
- <span data-ttu-id="62d2b-140">**Powtarzalne**.</span><span class="sxs-lookup"><span data-stu-id="62d2b-140">**Repeatable**.</span></span> <span data-ttu-id="62d2b-141">Uruchamianie testu jednostkowego powinno być zgodne z jego wynikami, to oznacza, że zawsze zwraca ten sam wynik, jeśli nie zmieni się niczego między przebiegami.</span><span class="sxs-lookup"><span data-stu-id="62d2b-141">Running a unit test should be consistent with its results, that is, it always returns the same result if you do not change anything in between runs.</span></span>
- <span data-ttu-id="62d2b-142">**Sprawdzanie samoobsługowe**.</span><span class="sxs-lookup"><span data-stu-id="62d2b-142">**Self-Checking**.</span></span> <span data-ttu-id="62d2b-143">Test powinien być w stanie automatycznie wykryć, czy zakończył się powodzeniem, bez ingerencji człowieka.</span><span class="sxs-lookup"><span data-stu-id="62d2b-143">The test should be able to automatically detect if it passed or failed without any human interaction.</span></span>
- <span data-ttu-id="62d2b-144">**Czasowo**.</span><span class="sxs-lookup"><span data-stu-id="62d2b-144">**Timely**.</span></span> <span data-ttu-id="62d2b-145">Test jednostkowy nie powinien trwać bardzo proporcjonalnie do zapisu w porównaniu z testowanym kodem.</span><span class="sxs-lookup"><span data-stu-id="62d2b-145">A unit test should not take a disproportionately long time to write compared to the code being tested.</span></span> <span data-ttu-id="62d2b-146">Jeśli okaże się, że test kodu zajmuje dużo czasu w porównaniu do pisania kodu, weź pod uwagę projekt, który jest bardziej weryfikowalne.</span><span class="sxs-lookup"><span data-stu-id="62d2b-146">If you find testing the code taking a large amount of time compared to writing the code, consider a design that is more testable.</span></span>

## <a name="code-coverage"></a><span data-ttu-id="62d2b-147">Pokrycie kodu</span><span class="sxs-lookup"><span data-stu-id="62d2b-147">Code coverage</span></span>

<span data-ttu-id="62d2b-148">Wysoka wartość procentowa pokrycia kodu jest często skojarzona z wyższą jakością kodu.</span><span class="sxs-lookup"><span data-stu-id="62d2b-148">A high code coverage percentage is often associated with a higher quality of code.</span></span> <span data-ttu-id="62d2b-149">Jednak sama pomiar *nie może* ustalić jakości kodu.</span><span class="sxs-lookup"><span data-stu-id="62d2b-149">However, the measurement itself *cannot* determine the quality of code.</span></span> <span data-ttu-id="62d2b-150">Ustawienie nadwyżkowej wartości procentowej pokrycia kodu ambitne podejście może być counterproductive.</span><span class="sxs-lookup"><span data-stu-id="62d2b-150">Setting an overly ambitious code coverage percentage goal can be counterproductive.</span></span> <span data-ttu-id="62d2b-151">Wyobraź sobie złożony projekt z tysiącami gałęzi warunkowych i Wyobraź sobie, że ustawisz cel pokrycia kodu o 95%.</span><span class="sxs-lookup"><span data-stu-id="62d2b-151">Imagine a complex project with thousands of conditional branches, and imagine that you set a goal of 95% code coverage.</span></span> <span data-ttu-id="62d2b-152">Obecnie projekt zachowuje pokrycie kodu w 90%.</span><span class="sxs-lookup"><span data-stu-id="62d2b-152">Currently the project maintains 90% code coverage.</span></span> <span data-ttu-id="62d2b-153">Czas potrzebny na uwzględnienie wszystkich przypadków brzegowych w pozostałej części 5% może być ogromnym przedsięwzięciem, a jej wartość jest szybko zmniejszana.</span><span class="sxs-lookup"><span data-stu-id="62d2b-153">The amount of time it takes to account for all of the edge cases in the remaining 5% could be a massive undertaking, and the value proposition quickly diminishes.</span></span>

<span data-ttu-id="62d2b-154">Wysoki procent pokrycia kodu nie jest wskaźnikiem sukcesu ani nie ma wysokiej jakości kodu.</span><span class="sxs-lookup"><span data-stu-id="62d2b-154">A high code coverage percentage is not an indicator of success, nor does it imply high code quality.</span></span> <span data-ttu-id="62d2b-155">Reprezentuje ona jedynie ilość kodu, która jest objęta testami jednostkowymi.</span><span class="sxs-lookup"><span data-stu-id="62d2b-155">It just represents the amount of code that is covered by unit tests.</span></span> <span data-ttu-id="62d2b-156">Aby uzyskać więcej informacji, zobacz temat [pokrycie kodu testu jednostkowego](unit-testing-code-coverage.md).</span><span class="sxs-lookup"><span data-stu-id="62d2b-156">For more information, see [unit testing code coverage](unit-testing-code-coverage.md).</span></span>

## <a name="lets-speak-the-same-language"></a><span data-ttu-id="62d2b-157">Zacznijmy od tego samego języka</span><span class="sxs-lookup"><span data-stu-id="62d2b-157">Let's speak the same language</span></span>

<span data-ttu-id="62d2b-158">W przypadku korzystania z testów *często występuje* niedziałający sposób.</span><span class="sxs-lookup"><span data-stu-id="62d2b-158">The term *mock* is unfortunately often misused when talking about testing.</span></span> <span data-ttu-id="62d2b-159">Następujące punkty definiują najpopularniejsze *typy elementów* sztucznych podczas pisania testów jednostkowych:</span><span class="sxs-lookup"><span data-stu-id="62d2b-159">The following points define the most common types of *fakes* when writing unit tests:</span></span>

<span data-ttu-id="62d2b-160">*Sfałszowane* — jest to ogólny termin, który może służyć do opisywania obiektu zastępczego lub makiety.</span><span class="sxs-lookup"><span data-stu-id="62d2b-160">*Fake* - A fake is a generic term that can be used to describe either a stub or a mock object.</span></span> <span data-ttu-id="62d2b-161">Bez względu na to, czy jest to element zastępczy, czy makieta zależy od kontekstu, w którym jest używana.</span><span class="sxs-lookup"><span data-stu-id="62d2b-161">Whether it's a stub or a mock depends on the context in which it's used.</span></span> <span data-ttu-id="62d2b-162">Inaczej mówiąc, może to być szczątk lub makieta.</span><span class="sxs-lookup"><span data-stu-id="62d2b-162">So in other words, a fake can be a stub or a mock.</span></span>

<span data-ttu-id="62d2b-163">*Makieta* — obiekt obiektu jest obiektem nieprawidłowym w systemie, który decyduje o tym, czy test jednostkowy zakończył się powodzeniem, czy nie.</span><span class="sxs-lookup"><span data-stu-id="62d2b-163">*Mock* - A mock object is a fake object in the system that decides whether or not a unit test has passed or failed.</span></span> <span data-ttu-id="62d2b-164">Makieta jest uruchamiana jako fałszywa, dopóki nie zostanie potwierdzona.</span><span class="sxs-lookup"><span data-stu-id="62d2b-164">A mock starts out as a Fake until it's asserted against.</span></span>

<span data-ttu-id="62d2b-165">*Szczątkowy* — zastępczy to przeprowadzona zmiana dla istniejącej zależności (lub współpracownika) w systemie.</span><span class="sxs-lookup"><span data-stu-id="62d2b-165">*Stub* - A stub is a controllable replacement for an existing dependency (or collaborator) in the system.</span></span> <span data-ttu-id="62d2b-166">Za pomocą klasy zastępczej można testować kod bez bezpośredniej kontroli nad zależnością.</span><span class="sxs-lookup"><span data-stu-id="62d2b-166">By using a stub, you can test your code without dealing with the dependency directly.</span></span> <span data-ttu-id="62d2b-167">Domyślnie, fałszywe jest uruchamiany jako element zastępczy.</span><span class="sxs-lookup"><span data-stu-id="62d2b-167">By default, a fake starts out as a stub.</span></span>

<span data-ttu-id="62d2b-168">Rozważmy następujący fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="62d2b-168">Consider the following code snippet:</span></span>

```csharp
var mockOrder = new MockOrder();
var purchase = new Purchase(mockOrder);

purchase.ValidateOrders();

Assert.True(purchase.CanBeShipped);
```

<span data-ttu-id="62d2b-169">Może to być przykład klasy zastępczej, która jest nazywana makietą.</span><span class="sxs-lookup"><span data-stu-id="62d2b-169">This would be an example of stub being referred to as a mock.</span></span> <span data-ttu-id="62d2b-170">W tym przypadku jest to element zastępczy.</span><span class="sxs-lookup"><span data-stu-id="62d2b-170">In this case, it is a stub.</span></span> <span data-ttu-id="62d2b-171">Nastąpi przekazanie w kolejności jako środek, aby można było utworzyć wystąpienie `Purchase` (system testowy).</span><span class="sxs-lookup"><span data-stu-id="62d2b-171">You're just passing in the Order as a means to be able to instantiate `Purchase` (the system under test).</span></span> <span data-ttu-id="62d2b-172">Nazwa `MockOrder` jest również myląca, ponieważ nie jest to makieta.</span><span class="sxs-lookup"><span data-stu-id="62d2b-172">The name `MockOrder` is also misleading because again, the order is not a mock.</span></span>

<span data-ttu-id="62d2b-173">Lepszym rozwiązaniem będzie</span><span class="sxs-lookup"><span data-stu-id="62d2b-173">A better approach would be</span></span>

```csharp
var stubOrder = new FakeOrder();
var purchase = new Purchase(stubOrder);

purchase.ValidateOrders();

Assert.True(purchase.CanBeShipped);
```

<span data-ttu-id="62d2b-174">Zmieniając nazwę klasy na, została `FakeOrder` utworzona bardziej generyczna Klasa, Klasa może być używana jako imitacja lub element zastępczy.</span><span class="sxs-lookup"><span data-stu-id="62d2b-174">By renaming the class to `FakeOrder`, you've made the class a lot more generic, the class can be used as a mock or a stub.</span></span> <span data-ttu-id="62d2b-175">W zależności od tego do przypadku testowego.</span><span class="sxs-lookup"><span data-stu-id="62d2b-175">Whichever is better for the test case.</span></span> <span data-ttu-id="62d2b-176">W powyższym przykładzie `FakeOrder` jest używany jako zastępczy.</span><span class="sxs-lookup"><span data-stu-id="62d2b-176">In the above example, `FakeOrder` is used as a stub.</span></span> <span data-ttu-id="62d2b-177">Nie używasz `FakeOrder` w żadnym kształcie ani formularzu podczas potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="62d2b-177">You're not using the `FakeOrder` in any shape or form during the assert.</span></span> <span data-ttu-id="62d2b-178">`FakeOrder`został przesłany do `Purchase` klasy w celu spełnienia wymagań konstruktora.</span><span class="sxs-lookup"><span data-stu-id="62d2b-178">`FakeOrder` was passed into the `Purchase` class to satisfy the requirements of the constructor.</span></span>

<span data-ttu-id="62d2b-179">Aby użyć go jako makiety, możesz zrobić coś podobnego do tego</span><span class="sxs-lookup"><span data-stu-id="62d2b-179">To use it as a Mock, you could do something like this</span></span>

```csharp
var mockOrder = new FakeOrder();
var purchase = new Purchase(mockOrder);

purchase.ValidateOrders();

Assert.True(mockOrder.Validated);
```

<span data-ttu-id="62d2b-180">W tym przypadku sprawdzasz właściwość dla fałszywego (potwierdzania), więc w powyższym fragmencie kodu `mockOrder` jest to makieta.</span><span class="sxs-lookup"><span data-stu-id="62d2b-180">In this case, you are checking a property on the Fake (asserting against it), so in the above code snippet, the `mockOrder` is a Mock.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="62d2b-181">Ważne jest, aby zapewnić poprawną terminologię.</span><span class="sxs-lookup"><span data-stu-id="62d2b-181">It's important to get this terminology correct.</span></span> <span data-ttu-id="62d2b-182">Jeśli wywołujesz obiekty zastępcze "makiety", inni deweloperzy będą wprowadzać fałszywe założenia dotyczące zamiaru.</span><span class="sxs-lookup"><span data-stu-id="62d2b-182">If you call your stubs "mocks", other developers are going to make false assumptions about your intent.</span></span>

<span data-ttu-id="62d2b-183">Głównym elementem, który należy pamiętać o makietach i fragmentów, jest to, że makiety są tak samo jak wycinki</span><span class="sxs-lookup"><span data-stu-id="62d2b-183">The main thing to remember about mocks versus stubs is that mocks are just like stubs, but you assert against the mock object, whereas you do not assert against a stub.</span></span>

## <a name="best-practices"></a><span data-ttu-id="62d2b-184">Najlepsze rozwiązania</span><span class="sxs-lookup"><span data-stu-id="62d2b-184">Best practices</span></span>

### <a name="naming-your-tests"></a><span data-ttu-id="62d2b-185">Nazywanie testów</span><span class="sxs-lookup"><span data-stu-id="62d2b-185">Naming your tests</span></span>

<span data-ttu-id="62d2b-186">Nazwa testu powinna składać się z trzech części:</span><span class="sxs-lookup"><span data-stu-id="62d2b-186">The name of your test should consist of three parts:</span></span>

- <span data-ttu-id="62d2b-187">Nazwa testowanej metody.</span><span class="sxs-lookup"><span data-stu-id="62d2b-187">The name of the method being tested.</span></span>
- <span data-ttu-id="62d2b-188">Scenariusz, w którym jest testowany.</span><span class="sxs-lookup"><span data-stu-id="62d2b-188">The scenario under which it's being tested.</span></span>
- <span data-ttu-id="62d2b-189">Oczekiwane zachowanie, gdy scenariusz jest wywoływany.</span><span class="sxs-lookup"><span data-stu-id="62d2b-189">The expected behavior when the scenario is invoked.</span></span>

#### <a name="why"></a><span data-ttu-id="62d2b-190">Dlaczego?</span><span class="sxs-lookup"><span data-stu-id="62d2b-190">Why?</span></span>

- <span data-ttu-id="62d2b-191">Wzorce nazewnictwa są ważne, ponieważ wyraźnie wyrażają intencję testu.</span><span class="sxs-lookup"><span data-stu-id="62d2b-191">Naming standards are important because they explicitly express the intent of the test.</span></span>

<span data-ttu-id="62d2b-192">Testy są większe niż tylko w celu upewnienia się, że kod działa, ale również zawiera dokumentację.</span><span class="sxs-lookup"><span data-stu-id="62d2b-192">Tests are more than just making sure your code works, they also provide documentation.</span></span> <span data-ttu-id="62d2b-193">Wystarczy, że szukasz zestawu testów jednostkowych, można wywnioskować zachowanie kodu bez konieczności przeglądania kodu.</span><span class="sxs-lookup"><span data-stu-id="62d2b-193">Just by looking at the suite of unit tests, you should be able to infer the behavior of your code without even looking at the code itself.</span></span> <span data-ttu-id="62d2b-194">Ponadto, gdy testy zakończą się niepowodzeniem, można zobaczyć, które scenariusze nie spełniają oczekiwań.</span><span class="sxs-lookup"><span data-stu-id="62d2b-194">Additionally, when tests fail, you can see exactly which scenarios do not meet your expectations.</span></span>

#### <a name="bad"></a><span data-ttu-id="62d2b-195">Źle:</span><span class="sxs-lookup"><span data-stu-id="62d2b-195">Bad:</span></span>

[!code-csharp[BeforeNaming](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/before/StringCalculatorTests.cs#BeforeNaming)]

#### <a name="better"></a><span data-ttu-id="62d2b-196">Bardziej</span><span class="sxs-lookup"><span data-stu-id="62d2b-196">Better:</span></span>

[!code-csharp[AfterNamingAndMinimallyPassing](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/after/StringCalculatorTests.cs#AfterNamingAndMinimallyPassing)]

### <a name="arranging-your-tests"></a><span data-ttu-id="62d2b-197">Rozmieszczanie testów</span><span class="sxs-lookup"><span data-stu-id="62d2b-197">Arranging your tests</span></span>

<span data-ttu-id="62d2b-198">**Rozmieść, Act, Assert** jest typowym wzorcem podczas testowania jednostkowego.</span><span class="sxs-lookup"><span data-stu-id="62d2b-198">**Arrange, Act, Assert** is a common pattern when unit testing.</span></span> <span data-ttu-id="62d2b-199">Jak nazwa oznacza, składa się z trzech głównych akcji:</span><span class="sxs-lookup"><span data-stu-id="62d2b-199">As the name implies, it consists of three main actions:</span></span>

- <span data-ttu-id="62d2b-200">*Rozmieszczanie* obiektów, tworzenie i konfigurowanie ich w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="62d2b-200">*Arrange* your objects, creating and setting them up as necessary.</span></span>
- <span data-ttu-id="62d2b-201">*Działanie* na obiekcie.</span><span class="sxs-lookup"><span data-stu-id="62d2b-201">*Act* on an object.</span></span>
- <span data-ttu-id="62d2b-202">*Potwierdź* , że coś jest zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="62d2b-202">*Assert* that something is as expected.</span></span>

#### <a name="why"></a><span data-ttu-id="62d2b-203">Dlaczego?</span><span class="sxs-lookup"><span data-stu-id="62d2b-203">Why?</span></span>

- <span data-ttu-id="62d2b-204">Wyraźnie oddzieli to, co jest testowane z kroków *rozmieszczenia* i *potwierdzeń* .</span><span class="sxs-lookup"><span data-stu-id="62d2b-204">Clearly separates what is being tested from the *arrange* and *assert* steps.</span></span>
- <span data-ttu-id="62d2b-205">Mniejsza szansa, aby Intermix potwierdzenia z kodem "Act".</span><span class="sxs-lookup"><span data-stu-id="62d2b-205">Less chance to intermix assertions with "Act" code.</span></span>

<span data-ttu-id="62d2b-206">Czytelność to jeden z najważniejszych aspektów związanych z pisaniem testu.</span><span class="sxs-lookup"><span data-stu-id="62d2b-206">Readability is one of the most important aspects when writing a test.</span></span> <span data-ttu-id="62d2b-207">Oddzielenie każdej z tych akcji w ramach testu wyraźnie podkreśla zależności wymagane do wywołania kodu, sposobu wywoływania kodu i tego, co próbujesz przedstawić.</span><span class="sxs-lookup"><span data-stu-id="62d2b-207">Separating each of these actions within the test clearly highlight the dependencies required to call your code, how your code is being called, and what you are trying to assert.</span></span> <span data-ttu-id="62d2b-208">Chociaż może być możliwe połączenie niektórych kroków i zmniejszenie rozmiaru testu, głównym celem jest przeprowadzenie testu jako możliwego do odczytania.</span><span class="sxs-lookup"><span data-stu-id="62d2b-208">While it may be possible to combine some steps and reduce the size of your test, the primary goal is to make the test as readable as possible.</span></span>

#### <a name="bad"></a><span data-ttu-id="62d2b-209">Źle:</span><span class="sxs-lookup"><span data-stu-id="62d2b-209">Bad:</span></span>

[!code-csharp[BeforeArranging](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/before/StringCalculatorTests.cs#BeforeArranging)]

#### <a name="better"></a><span data-ttu-id="62d2b-210">Bardziej</span><span class="sxs-lookup"><span data-stu-id="62d2b-210">Better:</span></span>

[!code-csharp[AfterArranging](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/after/StringCalculatorTests.cs#AfterArranging)]

### <a name="write-minimally-passing-tests"></a><span data-ttu-id="62d2b-211">Zapisz minimalnie przekazanie testów</span><span class="sxs-lookup"><span data-stu-id="62d2b-211">Write minimally passing tests</span></span>

<span data-ttu-id="62d2b-212">Dane wejściowe do użycia w teście jednostkowym powinny być najprostszym możliwym do zweryfikowania zachowania, które jest obecnie testowane.</span><span class="sxs-lookup"><span data-stu-id="62d2b-212">The input to be used in a unit test should be the simplest possible in order to verify the behavior that you are currently testing.</span></span>

#### <a name="why"></a><span data-ttu-id="62d2b-213">Dlaczego?</span><span class="sxs-lookup"><span data-stu-id="62d2b-213">Why?</span></span>

- <span data-ttu-id="62d2b-214">Testy stają się bardziej odporne na przyszłe zmiany w bazie kodu.</span><span class="sxs-lookup"><span data-stu-id="62d2b-214">Tests become more resilient to future changes in the codebase.</span></span>
- <span data-ttu-id="62d2b-215">Bliżej działania testowania nad implementacją.</span><span class="sxs-lookup"><span data-stu-id="62d2b-215">Closer to testing behavior over implementation.</span></span>

<span data-ttu-id="62d2b-216">Testy, które zawierają więcej informacji, niż jest to wymagane do przekazania testu, mają większą szansę na wprowadzenie błędów do testu i mogą sprawić, że zamiar testu jest mniej oczywisty.</span><span class="sxs-lookup"><span data-stu-id="62d2b-216">Tests that include more information than required to pass the test have a higher chance of introducing errors into the test and can make the intent of the test less clear.</span></span> <span data-ttu-id="62d2b-217">Podczas pisania testów należy skoncentrować się na zachowaniu.</span><span class="sxs-lookup"><span data-stu-id="62d2b-217">When writing tests, you want to focus on the behavior.</span></span> <span data-ttu-id="62d2b-218">Ustawienie dodatkowych właściwości dla modeli lub użycie niezerowych wartości, gdy nie jest to wymagane, powoduje tylko rozciąganie z tego, co próbujesz udowodnić.</span><span class="sxs-lookup"><span data-stu-id="62d2b-218">Setting extra properties on models or using non-zero values when not required, only detracts from what you are trying to prove.</span></span>

#### <a name="bad"></a><span data-ttu-id="62d2b-219">Źle:</span><span class="sxs-lookup"><span data-stu-id="62d2b-219">Bad:</span></span>

[!code-csharp[BeforeMinimallyPassing](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/before/StringCalculatorTests.cs#BeforeMinimallyPassing)]

#### <a name="better"></a><span data-ttu-id="62d2b-220">Bardziej</span><span class="sxs-lookup"><span data-stu-id="62d2b-220">Better:</span></span>

[!code-csharp[AfterNamingAndMinimallyPassing](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/after/StringCalculatorTests.cs#AfterNamingAndMinimallyPassing)]

### <a name="avoid-magic-strings"></a><span data-ttu-id="62d2b-221">Unikaj ciągów Magic</span><span class="sxs-lookup"><span data-stu-id="62d2b-221">Avoid magic strings</span></span>

<span data-ttu-id="62d2b-222">Zmienne nazewnictwa w testach jednostkowych są ważne, jeśli nie są ważniejsze niż zmienne nazw w kodzie produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="62d2b-222">Naming variables in unit tests is as important, if not more important, than naming variables in production code.</span></span> <span data-ttu-id="62d2b-223">Testy jednostkowe nie powinny zawierać ciągów Magic.</span><span class="sxs-lookup"><span data-stu-id="62d2b-223">Unit tests should not contain magic strings.</span></span>

#### <a name="why"></a><span data-ttu-id="62d2b-224">Dlaczego?</span><span class="sxs-lookup"><span data-stu-id="62d2b-224">Why?</span></span>

- <span data-ttu-id="62d2b-225">Zapobiega potrzebom czytnika testów w celu sprawdzenia kodu produkcyjnego w celu ustalenia, co sprawia, że wartość jest specjalna.</span><span class="sxs-lookup"><span data-stu-id="62d2b-225">Prevents the need for the reader of the test to inspect the production code in order to figure out what makes the value special.</span></span>
- <span data-ttu-id="62d2b-226">Jawnie pokazuje, co próbujesz *udowodnić* , zamiast podejmować próbę *wykonania*.</span><span class="sxs-lookup"><span data-stu-id="62d2b-226">Explicitly shows what you're trying to *prove* rather than trying to *accomplish*.</span></span>

<span data-ttu-id="62d2b-227">Ciągi Magic mogą spowodować pomyłkę dla czytnika testów.</span><span class="sxs-lookup"><span data-stu-id="62d2b-227">Magic strings can cause confusion to the reader of your tests.</span></span> <span data-ttu-id="62d2b-228">Jeśli ciąg wyróżni się od zwykłego, może się zastanawiać, dlaczego określona wartość została wybrana dla parametru lub wartości zwracanej.</span><span class="sxs-lookup"><span data-stu-id="62d2b-228">If a string looks out of the ordinary, they may wonder why a certain value was chosen for a parameter or return value.</span></span> <span data-ttu-id="62d2b-229">Może to prowadzić do bliższego przyjrzeć się szczegółowym informacjom dotyczącym implementacji, zamiast skupić się na teście.</span><span class="sxs-lookup"><span data-stu-id="62d2b-229">This may lead them to take a closer look at the implementation details, rather than focus on the test.</span></span>

> [!TIP]
> <span data-ttu-id="62d2b-230">Podczas pisania testów należy zamierzyć możliwie jak najwięcej założeń.</span><span class="sxs-lookup"><span data-stu-id="62d2b-230">When writing tests, you should aim to express as much intent as possible.</span></span> <span data-ttu-id="62d2b-231">W przypadku ciągów magicznych dobrym rozwiązaniem jest przypisanie tych wartości do stałych.</span><span class="sxs-lookup"><span data-stu-id="62d2b-231">In the case of magic strings, a good approach is to assign these values to constants.</span></span>

#### <a name="bad"></a><span data-ttu-id="62d2b-232">Źle:</span><span class="sxs-lookup"><span data-stu-id="62d2b-232">Bad:</span></span>

[!code-csharp[BeforeMagicString](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/before/StringCalculatorTests.cs#BeforeMagicString)]

#### <a name="better"></a><span data-ttu-id="62d2b-233">Bardziej</span><span class="sxs-lookup"><span data-stu-id="62d2b-233">Better:</span></span>

[!code-csharp[AfterMagicString](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/after/StringCalculatorTests.cs#AfterMagicString)]

### <a name="avoid-logic-in-tests"></a><span data-ttu-id="62d2b-234">Unikanie logiki w testach</span><span class="sxs-lookup"><span data-stu-id="62d2b-234">Avoid logic in tests</span></span>

<span data-ttu-id="62d2b-235">Podczas pisania testów jednostkowych należy unikać ręcznego łączenia ciągów i warunków logicznych, takich jak,,, `if` `while` `for` `switch` itd.</span><span class="sxs-lookup"><span data-stu-id="62d2b-235">When writing your unit tests avoid manual string concatenation and logical conditions such as `if`, `while`, `for`, `switch`, etc.</span></span>

#### <a name="why"></a><span data-ttu-id="62d2b-236">Dlaczego?</span><span class="sxs-lookup"><span data-stu-id="62d2b-236">Why?</span></span>

- <span data-ttu-id="62d2b-237">Mniejsza szansa, aby wprowadzić usterkę w testach.</span><span class="sxs-lookup"><span data-stu-id="62d2b-237">Less chance to introduce a bug inside of your tests.</span></span>
- <span data-ttu-id="62d2b-238">Skup się na wyniku końca, a nie w szczegółach implementacji.</span><span class="sxs-lookup"><span data-stu-id="62d2b-238">Focus on the end result, rather than implementation details.</span></span>

<span data-ttu-id="62d2b-239">Gdy wprowadzasz logikę do zestawu testów, szansa na ich zwiększenie znacznie rośnie.</span><span class="sxs-lookup"><span data-stu-id="62d2b-239">When you introduce logic into your test suite, the chance of introducing a bug into it increases dramatically.</span></span> <span data-ttu-id="62d2b-240">Ostatnim miejscem, w którym chcesz znaleźć usterkę, jest zestaw testów.</span><span class="sxs-lookup"><span data-stu-id="62d2b-240">The last place that you want to find a bug is within your test suite.</span></span> <span data-ttu-id="62d2b-241">Należy mieć wysoki poziom pewności, że testy działają, w przeciwnym razie nie będzie można ich ufać.</span><span class="sxs-lookup"><span data-stu-id="62d2b-241">You should have a high level of confidence that your tests work, otherwise, you will not trust them.</span></span> <span data-ttu-id="62d2b-242">Testy, które nie są zaufane, nie zapewniają żadnej wartości.</span><span class="sxs-lookup"><span data-stu-id="62d2b-242">Tests that you do not trust, do not provide any value.</span></span> <span data-ttu-id="62d2b-243">Gdy test zakończy się niepowodzeniem, warto mieć sens, że coś w rzeczywistości jest nieprawidłowe w kodzie i że nie można go zignorować.</span><span class="sxs-lookup"><span data-stu-id="62d2b-243">When a test fails, you want to have a sense that something is actually wrong with your code and that it cannot be ignored.</span></span>

> [!TIP]
> <span data-ttu-id="62d2b-244">Jeśli logika w teście wydaje się nienieunikniona, rozważ podzielenie testu na dwa lub więcej różnych testów.</span><span class="sxs-lookup"><span data-stu-id="62d2b-244">If logic in your test seems unavoidable, consider splitting the test up into two or more different tests.</span></span>

#### <a name="bad"></a><span data-ttu-id="62d2b-245">Źle:</span><span class="sxs-lookup"><span data-stu-id="62d2b-245">Bad:</span></span>

[!code-csharp[LogicInTests](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/before/StringCalculatorTests.cs#LogicInTests)]

#### <a name="better"></a><span data-ttu-id="62d2b-246">Bardziej</span><span class="sxs-lookup"><span data-stu-id="62d2b-246">Better:</span></span>

[!code-csharp[AfterTestLogic](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/after/StringCalculatorTests.cs#AfterTestLogic)]

### <a name="prefer-helper-methods-to-setup-and-teardown"></a><span data-ttu-id="62d2b-247">Preferuj metody pomocnika do instalacji i usuwania</span><span class="sxs-lookup"><span data-stu-id="62d2b-247">Prefer helper methods to setup and teardown</span></span>

<span data-ttu-id="62d2b-248">Jeśli potrzebujesz podobnego obiektu lub stanu dla testów, Preferuj metodę pomocnika, korzystając z atrybutów Setup i usuwania, jeśli istnieją.</span><span class="sxs-lookup"><span data-stu-id="62d2b-248">If you require a similar object or state for your tests, prefer a helper method than leveraging Setup and Teardown attributes if they exist.</span></span>

#### <a name="why"></a><span data-ttu-id="62d2b-249">Dlaczego?</span><span class="sxs-lookup"><span data-stu-id="62d2b-249">Why?</span></span>

- <span data-ttu-id="62d2b-250">Mniej pomyłek podczas odczytywania testów, ponieważ cały kod jest widoczny w ramach każdego testu.</span><span class="sxs-lookup"><span data-stu-id="62d2b-250">Less confusion when reading the tests since all of the code is visible from within each test.</span></span>
- <span data-ttu-id="62d2b-251">Mniejsza szansa, że zbyt wiele lub zbyt mała dla danego testu.</span><span class="sxs-lookup"><span data-stu-id="62d2b-251">Less chance of setting up too much or too little for the given test.</span></span>
- <span data-ttu-id="62d2b-252">Mniejsza szansa stanu udostępniania między testami, która tworzy niepożądane zależności między nimi.</span><span class="sxs-lookup"><span data-stu-id="62d2b-252">Less chance of sharing state between tests, which creates unwanted dependencies between them.</span></span>

<span data-ttu-id="62d2b-253">W strukturach testów jednostkowych `Setup` jest wywoływana przed każdym testem jednostkowym w ramach zestawu testów.</span><span class="sxs-lookup"><span data-stu-id="62d2b-253">In unit testing frameworks, `Setup` is called before each and every unit test within your test suite.</span></span> <span data-ttu-id="62d2b-254">Niektóre mogą być widoczne jako przydatne narzędzia, zazwyczaj kończą się wiodącym bloated i trudnym do odczytania testów.</span><span class="sxs-lookup"><span data-stu-id="62d2b-254">While some may see this as a useful tool, it generally ends up leading to bloated and hard to read tests.</span></span> <span data-ttu-id="62d2b-255">Każdy test ma zwykle różne wymagania, aby można było je uruchomić.</span><span class="sxs-lookup"><span data-stu-id="62d2b-255">Each test will generally have different requirements in order to get the test up and running.</span></span> <span data-ttu-id="62d2b-256">Niestety, `Setup` wymusza użycie dokładnie tych samych wymagań dla każdego testu.</span><span class="sxs-lookup"><span data-stu-id="62d2b-256">Unfortunately, `Setup` forces you to use the exact same requirements for each test.</span></span>

> [!NOTE]
> <span data-ttu-id="62d2b-257">xUnit usunął zarówno Instalatora, jak i usuwania w wersji 2. x</span><span class="sxs-lookup"><span data-stu-id="62d2b-257">xUnit has removed both SetUp and TearDown as of version 2.x</span></span>

#### <a name="bad"></a><span data-ttu-id="62d2b-258">Źle:</span><span class="sxs-lookup"><span data-stu-id="62d2b-258">Bad:</span></span>

[!code-csharp[BeforeSetup](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/before/StringCalculatorTests.cs#BeforeSetup)]

```csharp
// more tests...
```

[!code-csharp[BeforeHelperMethod](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/before/StringCalculatorTests.cs#BeforeHelperMethod)]

#### <a name="better"></a><span data-ttu-id="62d2b-259">Bardziej</span><span class="sxs-lookup"><span data-stu-id="62d2b-259">Better:</span></span>

[!code-csharp[AfterHelperMethod](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/after/StringCalculatorTests.cs#AfterHelperMethod)]

```csharp
// more tests...
```

[!code-csharp[AfterSetup](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/after/StringCalculatorTests.cs#AfterSetup)]

### <a name="avoid-multiple-asserts"></a><span data-ttu-id="62d2b-260">Unikaj wielu potwierdzeń</span><span class="sxs-lookup"><span data-stu-id="62d2b-260">Avoid multiple asserts</span></span>

<span data-ttu-id="62d2b-261">Podczas pisania testów, spróbuj uwzględnić tylko jedno potwierdzenie na test.</span><span class="sxs-lookup"><span data-stu-id="62d2b-261">When writing your tests, try to only include one Assert per test.</span></span> <span data-ttu-id="62d2b-262">Typowe podejścia do korzystania tylko z jednego potwierdzenia obejmują:</span><span class="sxs-lookup"><span data-stu-id="62d2b-262">Common approaches to using only one assert include:</span></span>

- <span data-ttu-id="62d2b-263">Utwórz oddzielny test dla każdego potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="62d2b-263">Create a separate test for each assert.</span></span>
- <span data-ttu-id="62d2b-264">Użyj testów sparametryzowanych.</span><span class="sxs-lookup"><span data-stu-id="62d2b-264">Use parameterized tests.</span></span>

#### <a name="why"></a><span data-ttu-id="62d2b-265">Dlaczego?</span><span class="sxs-lookup"><span data-stu-id="62d2b-265">Why?</span></span>

- <span data-ttu-id="62d2b-266">Jeśli jedno potwierdzenie nie powiedzie się, kolejne potwierdzenia nie zostaną ocenione.</span><span class="sxs-lookup"><span data-stu-id="62d2b-266">If one Assert fails, the subsequent Asserts will not be evaluated.</span></span>
- <span data-ttu-id="62d2b-267">Gwarantuje, że nie postanowisz wielu przypadków w testach.</span><span class="sxs-lookup"><span data-stu-id="62d2b-267">Ensures you are not asserting multiple cases in your tests.</span></span>
- <span data-ttu-id="62d2b-268">Zapewnia cały obraz, dlaczego testy kończą się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="62d2b-268">Gives you the entire picture as to why your tests are failing.</span></span>

<span data-ttu-id="62d2b-269">W przypadku wprowadzenia wielu potwierdzeń do przypadku testowego nie ma gwarancji, że wszystkie potwierdzenia zostaną wykonane.</span><span class="sxs-lookup"><span data-stu-id="62d2b-269">When introducing multiple asserts into a test case, it is not guaranteed that all of the asserts will be executed.</span></span> <span data-ttu-id="62d2b-270">W większości platform testów jednostkowych, gdy potwierdzenie kończy się niepowodzeniem w teście jednostkowym, testy postępu są automatycznie uważane za zakończone niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="62d2b-270">In most unit testing frameworks, once an assertion fails in a unit test, the proceeding tests are automatically considered to be failing.</span></span> <span data-ttu-id="62d2b-271">Może to być mylące, ponieważ funkcje, które faktycznie działają, będą wyświetlane jako niepowodzenie.</span><span class="sxs-lookup"><span data-stu-id="62d2b-271">This can be confusing as functionality that is actually working, will be shown as failing.</span></span>

> [!NOTE]
> <span data-ttu-id="62d2b-272">Typowym wyjątkiem od tej reguły jest potwierdzenie obiektu.</span><span class="sxs-lookup"><span data-stu-id="62d2b-272">A common exception to this rule is when asserting against an object.</span></span> <span data-ttu-id="62d2b-273">W takim przypadku ogólnie akceptowalne jest posiadanie wielu potwierdzeń dla każdej właściwości, aby upewnić się, że obiekt znajduje się w stanie, w którym oczekujesz.</span><span class="sxs-lookup"><span data-stu-id="62d2b-273">In this case, it is generally acceptable to have multiple asserts against each property to ensure the object is in the state that you expect it to be in.</span></span>

#### <a name="bad"></a><span data-ttu-id="62d2b-274">Źle:</span><span class="sxs-lookup"><span data-stu-id="62d2b-274">Bad:</span></span>

[!code-csharp[BeforeMultipleAsserts](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/before/StringCalculatorTests.cs#BeforeMultipleAsserts)]

#### <a name="better"></a><span data-ttu-id="62d2b-275">Bardziej</span><span class="sxs-lookup"><span data-stu-id="62d2b-275">Better:</span></span>

[!code-csharp[AfterMultipleAsserts](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/after/StringCalculatorTests.cs#AfterMultipleAsserts)]

### <a name="validate-private-methods-by-unit-testing-public-methods"></a><span data-ttu-id="62d2b-276">Weryfikowanie metod prywatnych według metod publicznych testów jednostkowych</span><span class="sxs-lookup"><span data-stu-id="62d2b-276">Validate private methods by unit testing public methods</span></span>

<span data-ttu-id="62d2b-277">W większości przypadków nie powinno być konieczne przetestowanie metody prywatnej.</span><span class="sxs-lookup"><span data-stu-id="62d2b-277">In most cases, there should not be a need to test a private method.</span></span> <span data-ttu-id="62d2b-278">Metody prywatne są szczegółami implementacji.</span><span class="sxs-lookup"><span data-stu-id="62d2b-278">Private methods are an implementation detail.</span></span> <span data-ttu-id="62d2b-279">Można to traktować w ten sposób: metody prywatne nigdy nie istnieją w izolacji.</span><span class="sxs-lookup"><span data-stu-id="62d2b-279">You can think of it this way: private methods never exist in isolation.</span></span> <span data-ttu-id="62d2b-280">W pewnym momencie istnieje metoda publiczna, która wywołuje metodę prywatną w ramach jej implementacji.</span><span class="sxs-lookup"><span data-stu-id="62d2b-280">At some point, there is going to be a public facing method that calls the private method as part of its implementation.</span></span> <span data-ttu-id="62d2b-281">Informacje o tym, co należy wiedzieć, to wynik metody publicznej, która wywołuje do prywatnego.</span><span class="sxs-lookup"><span data-stu-id="62d2b-281">What you should care about is the end result of the public method that calls into the private one.</span></span>

<span data-ttu-id="62d2b-282">Rozważmy następujący przypadek</span><span class="sxs-lookup"><span data-stu-id="62d2b-282">Consider the following case</span></span>

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

<span data-ttu-id="62d2b-283">Pierwszą odpowiedzią może być rozpoczęcie pisania testu dla `TrimInput` , ponieważ chcesz upewnić się, że metoda działa zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="62d2b-283">Your first reaction may be to start writing a test for `TrimInput` because you want to make sure that the method is working as expected.</span></span> <span data-ttu-id="62d2b-284">Jednak jest on w pełni możliwy, aby `ParseLogLine` manipulować `sanitizedInput` w taki sposób, że nie jest to oczekiwane, renderowanie testu przed `TrimInput` bezużyteczny.</span><span class="sxs-lookup"><span data-stu-id="62d2b-284">However, it is entirely possible that `ParseLogLine` manipulates `sanitizedInput` in such a way that you do not expect, rendering a test against `TrimInput` useless.</span></span>

<span data-ttu-id="62d2b-285">Rzeczywisty test powinien być wykonywany w oparciu o publiczną metodę dodaną `ParseLogLine` , ponieważ to to, co powinno być ostatecznie ważne.</span><span class="sxs-lookup"><span data-stu-id="62d2b-285">The real test should be done against the public facing method `ParseLogLine` because that is what you should ultimately care about.</span></span>

```csharp
public void ParseLogLine_StartsAndEndsWithSpace_ReturnsTrimmedResult()
{
    var parser = new Parser();

    var result = parser.ParseLogLine(" a ");

    Assert.Equals("a", result);
}
```

<span data-ttu-id="62d2b-286">Jeśli w tym obszarze widać, że jest wyświetlana Metoda prywatna, Znajdź metodę publiczną i napisz testy dla tej metody.</span><span class="sxs-lookup"><span data-stu-id="62d2b-286">With this viewpoint, if you see a private method, find the public method and write your tests against that method.</span></span> <span data-ttu-id="62d2b-287">Tylko dlatego, że Metoda prywatna zwraca oczekiwany wynik, nie oznacza, że system, który ostatecznie wywołuje metodę prywatną, użyje poprawnego wyniku.</span><span class="sxs-lookup"><span data-stu-id="62d2b-287">Just because a private method returns the expected result, does not mean the system that eventually calls the private method uses the result correctly.</span></span>

### <a name="stub-static-references"></a><span data-ttu-id="62d2b-288">Zastępcze odwołania statyczne</span><span class="sxs-lookup"><span data-stu-id="62d2b-288">Stub static references</span></span>

<span data-ttu-id="62d2b-289">Jedną z zasad testów jednostkowych jest to, że musi ona mieć pełną kontrolę nad testowanym systemem.</span><span class="sxs-lookup"><span data-stu-id="62d2b-289">One of the principles of a unit test is that it must have full control of the system under test.</span></span> <span data-ttu-id="62d2b-290">Może to być problematyczne, gdy kod produkcyjny zawiera wywołania do odwołań statycznych (na przykład `DateTime.Now` ).</span><span class="sxs-lookup"><span data-stu-id="62d2b-290">This can be problematic when production code includes calls to static references (for example, `DateTime.Now`).</span></span> <span data-ttu-id="62d2b-291">Rozważmy następujący kod</span><span class="sxs-lookup"><span data-stu-id="62d2b-291">Consider the following code</span></span>

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

<span data-ttu-id="62d2b-292">Jak ten kod może być testowany jednostkowo?</span><span class="sxs-lookup"><span data-stu-id="62d2b-292">How can this code possibly be unit tested?</span></span> <span data-ttu-id="62d2b-293">Możesz wypróbować takie podejście jak</span><span class="sxs-lookup"><span data-stu-id="62d2b-293">You may try an approach such as</span></span>

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

<span data-ttu-id="62d2b-294">Niestety, możesz szybko zapamiętać, że istnieje kilka problemów z testami.</span><span class="sxs-lookup"><span data-stu-id="62d2b-294">Unfortunately, you will quickly realize that there are a couple problems with your tests.</span></span>

- <span data-ttu-id="62d2b-295">Jeśli zestaw testów jest uruchamiany w wtorek, drugi test zostanie przekazany, ale pierwszy test zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="62d2b-295">If the test suite is run on a Tuesday, the second test will pass, but the first test will fail.</span></span>
- <span data-ttu-id="62d2b-296">Jeśli zestaw testów jest uruchamiany z dowolnego innego dnia, pierwszy test zostanie przekazany, ale drugi test zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="62d2b-296">If the test suite is run on any other day, the first test will pass, but the second test will fail.</span></span>

<span data-ttu-id="62d2b-297">Aby rozwiązać te problemy, należy wprowadzić *szew* w kodzie produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="62d2b-297">To solve these problems, you'll need to introduce a *seam* into your production code.</span></span> <span data-ttu-id="62d2b-298">Jednym z metod jest Zawijanie kodu, który należy kontrolować w interfejsie i że kod produkcyjny zależy od tego interfejsu.</span><span class="sxs-lookup"><span data-stu-id="62d2b-298">One approach is to wrap the code that you need to control in an interface and have the production code depend on that interface.</span></span>

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

<span data-ttu-id="62d2b-299">Zestaw testów zostanie teraz</span><span class="sxs-lookup"><span data-stu-id="62d2b-299">Your test suite now becomes</span></span>

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

<span data-ttu-id="62d2b-300">Teraz zestaw testów ma pełną kontrolę nad `DateTime.Now` i może być dowolną wartością podczas wywoływania metody.</span><span class="sxs-lookup"><span data-stu-id="62d2b-300">Now the test suite has full control over `DateTime.Now` and can stub any value when calling into the method.</span></span>
