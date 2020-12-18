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
# <a name="unit-testing-best-practices-with-net-core-and-net-standard"></a><span data-ttu-id="7e5fa-103">Najlepsze rozwiązania dotyczące testów jednostkowych przy użyciu platformy .NET Core i .NET Standard</span><span class="sxs-lookup"><span data-stu-id="7e5fa-103">Unit testing best practices with .NET Core and .NET Standard</span></span>

<span data-ttu-id="7e5fa-104">Istnieje wiele korzyści związanych z pisaniem testów jednostkowych; ułatwiają one regresję, dostarczenie dokumentacji i ułatwiają dobre projektowanie.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-104">There are numerous benefits to writing unit tests; they help with regression, provide documentation, and facilitate good design.</span></span> <span data-ttu-id="7e5fa-105">Jednak trudno odczytać i kruchy testy jednostkowe mogą Wreak destabilizować w bazie kodu.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-105">However, hard to read and brittle unit tests can wreak havoc on your code base.</span></span> <span data-ttu-id="7e5fa-106">W tym artykule opisano niektóre najlepsze rozwiązania dotyczące projektu testów jednostkowych dla projektów .NET Core i .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-106">This article describes some best practices regarding unit test design for your .NET Core and .NET Standard projects.</span></span>

<span data-ttu-id="7e5fa-107">W tym przewodniku przedstawiono niektóre najlepsze rozwiązania podczas pisania testów jednostkowych w celu zapewnienia odporności i łatwego zrozumienia testów.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-107">In this guide, you'll learn some best practices when writing unit tests to keep your tests resilient and easy to understand.</span></span>

<span data-ttu-id="7e5fa-108">[Jan Reese](https://reese.dev) z specjalne podziękowaniami do [Roy Osherove](https://osherove.com/)</span><span class="sxs-lookup"><span data-stu-id="7e5fa-108">By [John Reese](https://reese.dev) with special thanks to [Roy Osherove](https://osherove.com/)</span></span>

## <a name="why-unit-test"></a><span data-ttu-id="7e5fa-109">Dlaczego test jednostkowy?</span><span class="sxs-lookup"><span data-stu-id="7e5fa-109">Why unit test?</span></span>

### <a name="less-time-performing-functional-tests"></a><span data-ttu-id="7e5fa-110">Krótszy czas wykonywania testów funkcjonalnych</span><span class="sxs-lookup"><span data-stu-id="7e5fa-110">Less time performing functional tests</span></span>

<span data-ttu-id="7e5fa-111">Testy funkcjonalne są kosztowne.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-111">Functional tests are expensive.</span></span> <span data-ttu-id="7e5fa-112">Zwykle wymagają otwarcia aplikacji i wykonania serii czynności, które należy wykonać (lub kogoś innego), aby sprawdzić oczekiwane zachowanie.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-112">They typically involve opening up the application and performing a series of steps that you (or someone else), must follow in order to validate the expected behavior.</span></span> <span data-ttu-id="7e5fa-113">Te kroki mogą być nieznane dla testera, co oznacza, że będą musieli skontaktować się z inną osobą w obszarze w celu przeprowadzenia testu.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-113">These steps may not always be known to the tester, which means they will have to reach out to someone more knowledgeable in the area in order to carry out the test.</span></span> <span data-ttu-id="7e5fa-114">Testowanie może potrwać kilka sekund lub kilka minut w przypadku większych zmian.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-114">Testing itself could take seconds for trivial changes, or minutes for larger changes.</span></span> <span data-ttu-id="7e5fa-115">Na koniec należy powtórzyć ten proces dla każdej zmiany wprowadzonej w systemie.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-115">Lastly, this process must be repeated for every change that you make in the system.</span></span>

<span data-ttu-id="7e5fa-116">Testy jednostkowe, z drugiej strony, pozostaną w milisekundach, mogą być uruchamiane przy naciśnięciu przycisku i niekoniecznie wymagają żadnej wiedzy o systemie.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-116">Unit tests, on the other hand, take milliseconds, can be run at the press of a button, and don't necessarily require any knowledge of the system at large.</span></span> <span data-ttu-id="7e5fa-117">Niezależnie od tego, czy test lub czy nie działa, jest do modułu uruchamiającego testy, a nie do osoby.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-117">Whether or not the test passes or fails is up to the test runner, not the individual.</span></span>

### <a name="protection-against-regression"></a><span data-ttu-id="7e5fa-118">Ochrona przed regresją</span><span class="sxs-lookup"><span data-stu-id="7e5fa-118">Protection against regression</span></span>

<span data-ttu-id="7e5fa-119">Wady regresji to wady wprowadzane po wprowadzeniu zmian w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-119">Regression defects are defects that are introduced when a change is made to the application.</span></span> <span data-ttu-id="7e5fa-120">Jest ona wspólna dla testerów, aby nie tylko testować swoją nową funkcję, ale również funkcje, które wcześniej istniały w celu sprawdzenia, czy poprzednio zaimplementowane funkcje nadal działają zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-120">It is common for testers to not only test their new feature but also features that existed beforehand in order to verify that previously implemented features still function as expected.</span></span>

<span data-ttu-id="7e5fa-121">W przypadku testów jednostkowych możliwe jest ponowne uruchomienie całego pakietu testów po każdej kompilacji lub nawet po zmianie wiersza kodu.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-121">With unit testing, it's possible to rerun your entire suite of tests after every build or even after you change a line of code.</span></span> <span data-ttu-id="7e5fa-122">Zapewnianie pewności, że nowy kod nie przerywa istniejących funkcji.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-122">Giving you confidence that your new code does not break existing functionality.</span></span>

### <a name="executable-documentation"></a><span data-ttu-id="7e5fa-123">Dokumentacja pliku wykonywalnego</span><span class="sxs-lookup"><span data-stu-id="7e5fa-123">Executable documentation</span></span>

<span data-ttu-id="7e5fa-124">Może to nie zawsze być oczywisty sposób działania określonej metody lub jej zachowania.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-124">It may not always be obvious what a particular method does or how it behaves given a certain input.</span></span> <span data-ttu-id="7e5fa-125">Użytkownik może zadawać sobie: jak działa ta metoda, jeśli przekażę pusty ciąg?</span><span class="sxs-lookup"><span data-stu-id="7e5fa-125">You may ask yourself: How does this method behave if I pass it a blank string?</span></span> <span data-ttu-id="7e5fa-126">Null?</span><span class="sxs-lookup"><span data-stu-id="7e5fa-126">Null?</span></span>

<span data-ttu-id="7e5fa-127">Jeśli masz zestaw dobrze wymienionych testów jednostkowych, każdy test powinien być w stanie jasno wyjaśnić oczekiwane dane wyjściowe dla danego danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-127">When you have a suite of well-named unit tests, each test should be able to clearly explain the expected output for a given input.</span></span> <span data-ttu-id="7e5fa-128">Ponadto powinno być możliwe zweryfikowanie, czy faktycznie działa.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-128">In addition, it should be able to verify that it actually works.</span></span>

### <a name="less-coupled-code"></a><span data-ttu-id="7e5fa-129">Mniej połączony kod</span><span class="sxs-lookup"><span data-stu-id="7e5fa-129">Less coupled code</span></span>

<span data-ttu-id="7e5fa-130">Gdy kod jest ściśle sprzężony, może być trudne do testowania jednostkowego.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-130">When code is tightly coupled, it can be difficult to unit test.</span></span> <span data-ttu-id="7e5fa-131">Bez tworzenia testów jednostkowych dla kodu, który piszesz, Sprzęg może być mniej widoczny.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-131">Without creating unit tests for the code that you're writing, coupling may be less apparent.</span></span>

<span data-ttu-id="7e5fa-132">Pisanie testów dla kodu spowoduje naturalnie oddzielenie kodu, ponieważ byłoby trudniejsze do przetestowania w przeciwnym razie.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-132">Writing tests for your code will naturally decouple your code, because it would be more difficult to test otherwise.</span></span>

## <a name="characteristics-of-a-good-unit-test"></a><span data-ttu-id="7e5fa-133">Cechy dobrego testu jednostkowego</span><span class="sxs-lookup"><span data-stu-id="7e5fa-133">Characteristics of a good unit test</span></span>

- <span data-ttu-id="7e5fa-134">**Szybko**.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-134">**Fast**.</span></span> <span data-ttu-id="7e5fa-135">Niespotykane projekty mają tysiące testów jednostkowych.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-135">It is not uncommon for mature projects to have thousands of unit tests.</span></span> <span data-ttu-id="7e5fa-136">Testy jednostkowe powinny trwać bardzo mało czasu.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-136">Unit tests should take very little time to run.</span></span> <span data-ttu-id="7e5fa-137">).</span><span class="sxs-lookup"><span data-stu-id="7e5fa-137">Milliseconds.</span></span>
- <span data-ttu-id="7e5fa-138">**Izolowane**.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-138">**Isolated**.</span></span> <span data-ttu-id="7e5fa-139">Testy jednostkowe są autonomiczne, mogą być uruchamiane w izolacji i nie mogą być zależne od jakichkolwiek czynników zewnętrznych, takich jak system plików czy baza danych.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-139">Unit tests are standalone, can be run in isolation, and have no dependencies on any outside factors such as a file system or database.</span></span>
- <span data-ttu-id="7e5fa-140">**Powtarzalne**.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-140">**Repeatable**.</span></span> <span data-ttu-id="7e5fa-141">Uruchamianie testu jednostkowego powinno być zgodne z jego wynikami, to oznacza, że zawsze zwraca ten sam wynik, jeśli nie zmieni się niczego między przebiegami.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-141">Running a unit test should be consistent with its results, that is, it always returns the same result if you do not change anything in between runs.</span></span>
- <span data-ttu-id="7e5fa-142">**Sprawdzanie samoobsługowe**.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-142">**Self-Checking**.</span></span> <span data-ttu-id="7e5fa-143">Test powinien być w stanie automatycznie wykryć, czy zakończył się powodzeniem, bez ingerencji człowieka.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-143">The test should be able to automatically detect if it passed or failed without any human interaction.</span></span>
- <span data-ttu-id="7e5fa-144">**Czasowo**.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-144">**Timely**.</span></span> <span data-ttu-id="7e5fa-145">Test jednostkowy nie powinien trwać bardzo proporcjonalnie do zapisu w porównaniu z testowanym kodem.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-145">A unit test should not take a disproportionately long time to write compared to the code being tested.</span></span> <span data-ttu-id="7e5fa-146">Jeśli okaże się, że test kodu zajmuje dużo czasu w porównaniu do pisania kodu, weź pod uwagę projekt, który jest bardziej weryfikowalne.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-146">If you find testing the code taking a large amount of time compared to writing the code, consider a design that is more testable.</span></span>

## <a name="code-coverage"></a><span data-ttu-id="7e5fa-147">Pokrycie kodu</span><span class="sxs-lookup"><span data-stu-id="7e5fa-147">Code coverage</span></span>

<span data-ttu-id="7e5fa-148">Wysoka wartość procentowa pokrycia kodu jest często skojarzona z wyższą jakością kodu.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-148">A high code coverage percentage is often associated with a higher quality of code.</span></span> <span data-ttu-id="7e5fa-149">Jednak sama pomiar *nie może* ustalić jakości kodu.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-149">However, the measurement itself *cannot* determine the quality of code.</span></span> <span data-ttu-id="7e5fa-150">Ustawienie nadwyżkowej wartości procentowej pokrycia kodu ambitne podejście może być counterproductive.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-150">Setting an overly ambitious code coverage percentage goal can be counterproductive.</span></span> <span data-ttu-id="7e5fa-151">Wyobraź sobie złożony projekt z tysiącami gałęzi warunkowych i Wyobraź sobie, że ustawisz cel pokrycia kodu o 95%.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-151">Imagine a complex project with thousands of conditional branches, and imagine that you set a goal of 95% code coverage.</span></span> <span data-ttu-id="7e5fa-152">Obecnie projekt zachowuje pokrycie kodu w 90%.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-152">Currently the project maintains 90% code coverage.</span></span> <span data-ttu-id="7e5fa-153">Czas potrzebny na uwzględnienie wszystkich przypadków brzegowych w pozostałej części 5% może być ogromnym przedsięwzięciem, a jej wartość jest szybko zmniejszana.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-153">The amount of time it takes to account for all of the edge cases in the remaining 5% could be a massive undertaking, and the value proposition quickly diminishes.</span></span>

<span data-ttu-id="7e5fa-154">Wysoki procent pokrycia kodu nie jest wskaźnikiem sukcesu ani nie ma wysokiej jakości kodu.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-154">A high code coverage percentage is not an indicator of success, nor does it imply high code quality.</span></span> <span data-ttu-id="7e5fa-155">Reprezentuje ona jedynie ilość kodu, która jest objęta testami jednostkowymi.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-155">It just represents the amount of code that is covered by unit tests.</span></span> <span data-ttu-id="7e5fa-156">Aby uzyskać więcej informacji, zobacz temat [pokrycie kodu testu jednostkowego](unit-testing-code-coverage.md).</span><span class="sxs-lookup"><span data-stu-id="7e5fa-156">For more information, see [unit testing code coverage](unit-testing-code-coverage.md).</span></span>

## <a name="lets-speak-the-same-language"></a><span data-ttu-id="7e5fa-157">Zacznijmy od tego samego języka</span><span class="sxs-lookup"><span data-stu-id="7e5fa-157">Let's speak the same language</span></span>

<span data-ttu-id="7e5fa-158">W przypadku korzystania z testów *często występuje* niedziałający sposób.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-158">The term *mock* is unfortunately often misused when talking about testing.</span></span> <span data-ttu-id="7e5fa-159">Następujące punkty definiują najpopularniejsze *typy elementów* sztucznych podczas pisania testów jednostkowych:</span><span class="sxs-lookup"><span data-stu-id="7e5fa-159">The following points define the most common types of *fakes* when writing unit tests:</span></span>

<span data-ttu-id="7e5fa-160">*Sfałszowane* — jest to ogólny termin, który może służyć do opisywania obiektu zastępczego lub makiety.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-160">*Fake* - A fake is a generic term that can be used to describe either a stub or a mock object.</span></span> <span data-ttu-id="7e5fa-161">Bez względu na to, czy jest to element zastępczy, czy makieta zależy od kontekstu, w którym jest używana.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-161">Whether it's a stub or a mock depends on the context in which it's used.</span></span> <span data-ttu-id="7e5fa-162">Inaczej mówiąc, może to być szczątk lub makieta.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-162">So in other words, a fake can be a stub or a mock.</span></span>

<span data-ttu-id="7e5fa-163">*Makieta* — obiekt obiektu jest obiektem nieprawidłowym w systemie, który decyduje o tym, czy test jednostkowy zakończył się powodzeniem, czy nie.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-163">*Mock* - A mock object is a fake object in the system that decides whether or not a unit test has passed or failed.</span></span> <span data-ttu-id="7e5fa-164">Makieta jest uruchamiana jako fałszywa, dopóki nie zostanie potwierdzona.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-164">A mock starts out as a Fake until it's asserted against.</span></span>

<span data-ttu-id="7e5fa-165">*Szczątkowy* — zastępczy to przeprowadzona zmiana dla istniejącej zależności (lub współpracownika) w systemie.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-165">*Stub* - A stub is a controllable replacement for an existing dependency (or collaborator) in the system.</span></span> <span data-ttu-id="7e5fa-166">Za pomocą klasy zastępczej można testować kod bez bezpośredniej kontroli nad zależnością.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-166">By using a stub, you can test your code without dealing with the dependency directly.</span></span> <span data-ttu-id="7e5fa-167">Domyślnie element zastępczy jest uruchamiany jako sfałszowany.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-167">By default, a stub starts out as a fake.</span></span>

<span data-ttu-id="7e5fa-168">Rozważmy następujący fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="7e5fa-168">Consider the following code snippet:</span></span>

```csharp
var mockOrder = new MockOrder();
var purchase = new Purchase(mockOrder);

purchase.ValidateOrders();

Assert.True(purchase.CanBeShipped);
```

<span data-ttu-id="7e5fa-169">Może to być przykład klasy zastępczej, która jest nazywana makietą.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-169">This would be an example of stub being referred to as a mock.</span></span> <span data-ttu-id="7e5fa-170">W tym przypadku jest to element zastępczy.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-170">In this case, it is a stub.</span></span> <span data-ttu-id="7e5fa-171">Nastąpi przekazanie w kolejności jako środek, aby można było utworzyć wystąpienie `Purchase` (system testowy).</span><span class="sxs-lookup"><span data-stu-id="7e5fa-171">You're just passing in the Order as a means to be able to instantiate `Purchase` (the system under test).</span></span> <span data-ttu-id="7e5fa-172">Nazwa `MockOrder` jest również myląca, ponieważ nie jest to makieta.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-172">The name `MockOrder` is also misleading because again, the order is not a mock.</span></span>

<span data-ttu-id="7e5fa-173">Lepszym rozwiązaniem będzie</span><span class="sxs-lookup"><span data-stu-id="7e5fa-173">A better approach would be</span></span>

```csharp
var stubOrder = new FakeOrder();
var purchase = new Purchase(stubOrder);

purchase.ValidateOrders();

Assert.True(purchase.CanBeShipped);
```

<span data-ttu-id="7e5fa-174">Zmieniając nazwę klasy na, została `FakeOrder` utworzona bardziej generyczna Klasa, Klasa może być używana jako imitacja lub element zastępczy.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-174">By renaming the class to `FakeOrder`, you've made the class a lot more generic, the class can be used as a mock or a stub.</span></span> <span data-ttu-id="7e5fa-175">W zależności od tego do przypadku testowego.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-175">Whichever is better for the test case.</span></span> <span data-ttu-id="7e5fa-176">W powyższym przykładzie `FakeOrder` jest używany jako zastępczy.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-176">In the above example, `FakeOrder` is used as a stub.</span></span> <span data-ttu-id="7e5fa-177">Nie używasz `FakeOrder` w żadnym kształcie ani formularzu podczas potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-177">You're not using the `FakeOrder` in any shape or form during the assert.</span></span> <span data-ttu-id="7e5fa-178">`FakeOrder` został przesłany do `Purchase` klasy w celu spełnienia wymagań konstruktora.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-178">`FakeOrder` was passed into the `Purchase` class to satisfy the requirements of the constructor.</span></span>

<span data-ttu-id="7e5fa-179">Aby użyć go jako makiety, możesz zrobić coś podobnego do tego</span><span class="sxs-lookup"><span data-stu-id="7e5fa-179">To use it as a Mock, you could do something like this</span></span>

```csharp
var mockOrder = new FakeOrder();
var purchase = new Purchase(mockOrder);

purchase.ValidateOrders();

Assert.True(mockOrder.Validated);
```

<span data-ttu-id="7e5fa-180">W tym przypadku sprawdzasz właściwość dla fałszywego (potwierdzania), więc w powyższym fragmencie kodu `mockOrder` jest to makieta.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-180">In this case, you are checking a property on the Fake (asserting against it), so in the above code snippet, the `mockOrder` is a Mock.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7e5fa-181">Ważne jest, aby zapewnić poprawną terminologię.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-181">It's important to get this terminology correct.</span></span> <span data-ttu-id="7e5fa-182">Jeśli wywołujesz obiekty zastępcze "makiety", inni deweloperzy będą wprowadzać fałszywe założenia dotyczące zamiaru.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-182">If you call your stubs "mocks", other developers are going to make false assumptions about your intent.</span></span>

<span data-ttu-id="7e5fa-183">Głównym elementem, który należy pamiętać o makietach i fragmentów, jest to, że makiety są tak samo jak wycinki</span><span class="sxs-lookup"><span data-stu-id="7e5fa-183">The main thing to remember about mocks versus stubs is that mocks are just like stubs, but you assert against the mock object, whereas you do not assert against a stub.</span></span>

## <a name="best-practices"></a><span data-ttu-id="7e5fa-184">Najlepsze rozwiązania</span><span class="sxs-lookup"><span data-stu-id="7e5fa-184">Best practices</span></span>

<span data-ttu-id="7e5fa-185">Nie należy wprowadzać zależności od infrastruktury podczas pisania testów jednostkowych.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-185">Try not to introduce dependencies on infrastructure when writing unit tests.</span></span> <span data-ttu-id="7e5fa-186">Te testy są powolne i kruchy i powinny być zarezerwowane dla testów integracji.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-186">These make the tests slow and brittle and should be reserved for integration tests.</span></span> <span data-ttu-id="7e5fa-187">Można uniknąć tych zależności w aplikacji, postępując zgodnie z [zasadami jawnych zależności](https://deviq.com/explicit-dependencies-principle) i przy użyciu [iniekcji zależności](../extensions/dependency-injection.md).</span><span class="sxs-lookup"><span data-stu-id="7e5fa-187">You can avoid these dependencies in your application by following the [Explicit Dependencies Principle](https://deviq.com/explicit-dependencies-principle) and using [Dependency Injection](../extensions/dependency-injection.md).</span></span> <span data-ttu-id="7e5fa-188">Możesz również utrzymać testy jednostkowe w osobnym projekcie od testów integracji.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-188">You can also keep your unit tests in a separate project from your integration tests.</span></span> <span data-ttu-id="7e5fa-189">Gwarantuje to, że projekt testu jednostkowego nie zawiera odwołań do pakietów infrastruktury ani ich zależności.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-189">This ensures your unit test project doesn't have references to or dependencies on infrastructure packages.</span></span>

### <a name="naming-your-tests"></a><span data-ttu-id="7e5fa-190">Nazywanie testów</span><span class="sxs-lookup"><span data-stu-id="7e5fa-190">Naming your tests</span></span>

<span data-ttu-id="7e5fa-191">Nazwa testu powinna składać się z trzech części:</span><span class="sxs-lookup"><span data-stu-id="7e5fa-191">The name of your test should consist of three parts:</span></span>

- <span data-ttu-id="7e5fa-192">Nazwa testowanej metody.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-192">The name of the method being tested.</span></span>
- <span data-ttu-id="7e5fa-193">Scenariusz, w którym jest testowany.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-193">The scenario under which it's being tested.</span></span>
- <span data-ttu-id="7e5fa-194">Oczekiwane zachowanie, gdy scenariusz jest wywoływany.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-194">The expected behavior when the scenario is invoked.</span></span>

#### <a name="why"></a><span data-ttu-id="7e5fa-195">Dlaczego?</span><span class="sxs-lookup"><span data-stu-id="7e5fa-195">Why?</span></span>

- <span data-ttu-id="7e5fa-196">Wzorce nazewnictwa są ważne, ponieważ wyraźnie wyrażają intencję testu.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-196">Naming standards are important because they explicitly express the intent of the test.</span></span>

<span data-ttu-id="7e5fa-197">Testy są większe niż tylko w celu upewnienia się, że kod działa, ale również zawiera dokumentację.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-197">Tests are more than just making sure your code works, they also provide documentation.</span></span> <span data-ttu-id="7e5fa-198">Wystarczy, że szukasz zestawu testów jednostkowych, można wywnioskować zachowanie kodu bez konieczności przeglądania kodu.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-198">Just by looking at the suite of unit tests, you should be able to infer the behavior of your code without even looking at the code itself.</span></span> <span data-ttu-id="7e5fa-199">Ponadto, gdy testy zakończą się niepowodzeniem, można zobaczyć, które scenariusze nie spełniają oczekiwań.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-199">Additionally, when tests fail, you can see exactly which scenarios do not meet your expectations.</span></span>

#### <a name="bad"></a><span data-ttu-id="7e5fa-200">Źle:</span><span class="sxs-lookup"><span data-stu-id="7e5fa-200">Bad:</span></span>

[!code-csharp[BeforeNaming](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/before/StringCalculatorTests.cs#BeforeNaming)]

#### <a name="better"></a><span data-ttu-id="7e5fa-201">Bardziej</span><span class="sxs-lookup"><span data-stu-id="7e5fa-201">Better:</span></span>

[!code-csharp[AfterNamingAndMinimallyPassing](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/after/StringCalculatorTests.cs#AfterNamingAndMinimallyPassing)]

### <a name="arranging-your-tests"></a><span data-ttu-id="7e5fa-202">Rozmieszczanie testów</span><span class="sxs-lookup"><span data-stu-id="7e5fa-202">Arranging your tests</span></span>

<span data-ttu-id="7e5fa-203">**Rozmieść, Act, Assert** jest typowym wzorcem podczas testowania jednostkowego.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-203">**Arrange, Act, Assert** is a common pattern when unit testing.</span></span> <span data-ttu-id="7e5fa-204">Jak nazwa oznacza, składa się z trzech głównych akcji:</span><span class="sxs-lookup"><span data-stu-id="7e5fa-204">As the name implies, it consists of three main actions:</span></span>

- <span data-ttu-id="7e5fa-205">*Rozmieszczanie* obiektów, tworzenie i konfigurowanie ich w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-205">*Arrange* your objects, creating and setting them up as necessary.</span></span>
- <span data-ttu-id="7e5fa-206">*Działanie* na obiekcie.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-206">*Act* on an object.</span></span>
- <span data-ttu-id="7e5fa-207">*Potwierdź* , że coś jest zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-207">*Assert* that something is as expected.</span></span>

#### <a name="why"></a><span data-ttu-id="7e5fa-208">Dlaczego?</span><span class="sxs-lookup"><span data-stu-id="7e5fa-208">Why?</span></span>

- <span data-ttu-id="7e5fa-209">Wyraźnie oddzieli to, co jest testowane z kroków *rozmieszczenia* i *potwierdzeń* .</span><span class="sxs-lookup"><span data-stu-id="7e5fa-209">Clearly separates what is being tested from the *arrange* and *assert* steps.</span></span>
- <span data-ttu-id="7e5fa-210">Mniejsza szansa, aby Intermix potwierdzenia z kodem "Act".</span><span class="sxs-lookup"><span data-stu-id="7e5fa-210">Less chance to intermix assertions with "Act" code.</span></span>

<span data-ttu-id="7e5fa-211">Czytelność to jeden z najważniejszych aspektów związanych z pisaniem testu.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-211">Readability is one of the most important aspects when writing a test.</span></span> <span data-ttu-id="7e5fa-212">Oddzielenie każdej z tych akcji w ramach testu wyraźnie podkreśla zależności wymagane do wywołania kodu, sposobu wywoływania kodu i tego, co próbujesz przedstawić.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-212">Separating each of these actions within the test clearly highlight the dependencies required to call your code, how your code is being called, and what you are trying to assert.</span></span> <span data-ttu-id="7e5fa-213">Chociaż może być możliwe połączenie niektórych kroków i zmniejszenie rozmiaru testu, głównym celem jest przeprowadzenie testu jako możliwego do odczytania.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-213">While it may be possible to combine some steps and reduce the size of your test, the primary goal is to make the test as readable as possible.</span></span>

#### <a name="bad"></a><span data-ttu-id="7e5fa-214">Źle:</span><span class="sxs-lookup"><span data-stu-id="7e5fa-214">Bad:</span></span>

[!code-csharp[BeforeArranging](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/before/StringCalculatorTests.cs#BeforeArranging)]

#### <a name="better"></a><span data-ttu-id="7e5fa-215">Bardziej</span><span class="sxs-lookup"><span data-stu-id="7e5fa-215">Better:</span></span>

[!code-csharp[AfterArranging](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/after/StringCalculatorTests.cs#AfterArranging)]

### <a name="write-minimally-passing-tests"></a><span data-ttu-id="7e5fa-216">Zapisz minimalnie przekazanie testów</span><span class="sxs-lookup"><span data-stu-id="7e5fa-216">Write minimally passing tests</span></span>

<span data-ttu-id="7e5fa-217">Dane wejściowe do użycia w teście jednostkowym powinny być najprostszym możliwym do zweryfikowania zachowania, które jest obecnie testowane.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-217">The input to be used in a unit test should be the simplest possible in order to verify the behavior that you are currently testing.</span></span>

#### <a name="why"></a><span data-ttu-id="7e5fa-218">Dlaczego?</span><span class="sxs-lookup"><span data-stu-id="7e5fa-218">Why?</span></span>

- <span data-ttu-id="7e5fa-219">Testy stają się bardziej odporne na przyszłe zmiany w bazie kodu.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-219">Tests become more resilient to future changes in the codebase.</span></span>
- <span data-ttu-id="7e5fa-220">Bliżej działania testowania nad implementacją.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-220">Closer to testing behavior over implementation.</span></span>

<span data-ttu-id="7e5fa-221">Testy, które zawierają więcej informacji, niż jest to wymagane do przekazania testu, mają większą szansę na wprowadzenie błędów do testu i mogą sprawić, że zamiar testu jest mniej oczywisty.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-221">Tests that include more information than required to pass the test have a higher chance of introducing errors into the test and can make the intent of the test less clear.</span></span> <span data-ttu-id="7e5fa-222">Podczas pisania testów należy skoncentrować się na zachowaniu.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-222">When writing tests, you want to focus on the behavior.</span></span> <span data-ttu-id="7e5fa-223">Ustawienie dodatkowych właściwości dla modeli lub użycie niezerowych wartości, gdy nie jest to wymagane, powoduje tylko rozciąganie z tego, co próbujesz udowodnić.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-223">Setting extra properties on models or using non-zero values when not required, only detracts from what you are trying to prove.</span></span>

#### <a name="bad"></a><span data-ttu-id="7e5fa-224">Źle:</span><span class="sxs-lookup"><span data-stu-id="7e5fa-224">Bad:</span></span>

[!code-csharp[BeforeMinimallyPassing](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/before/StringCalculatorTests.cs#BeforeMinimallyPassing)]

#### <a name="better"></a><span data-ttu-id="7e5fa-225">Bardziej</span><span class="sxs-lookup"><span data-stu-id="7e5fa-225">Better:</span></span>

[!code-csharp[AfterNamingAndMinimallyPassing](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/after/StringCalculatorTests.cs#AfterNamingAndMinimallyPassing)]

### <a name="avoid-magic-strings"></a><span data-ttu-id="7e5fa-226">Unikaj ciągów Magic</span><span class="sxs-lookup"><span data-stu-id="7e5fa-226">Avoid magic strings</span></span>

<span data-ttu-id="7e5fa-227">Zmienne nazewnictwa w testach jednostkowych są ważne, jeśli nie są ważniejsze niż zmienne nazw w kodzie produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-227">Naming variables in unit tests is as important, if not more important, than naming variables in production code.</span></span> <span data-ttu-id="7e5fa-228">Testy jednostkowe nie powinny zawierać ciągów Magic.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-228">Unit tests should not contain magic strings.</span></span>

#### <a name="why"></a><span data-ttu-id="7e5fa-229">Dlaczego?</span><span class="sxs-lookup"><span data-stu-id="7e5fa-229">Why?</span></span>

- <span data-ttu-id="7e5fa-230">Zapobiega potrzebom czytnika testów w celu sprawdzenia kodu produkcyjnego w celu ustalenia, co sprawia, że wartość jest specjalna.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-230">Prevents the need for the reader of the test to inspect the production code in order to figure out what makes the value special.</span></span>
- <span data-ttu-id="7e5fa-231">Jawnie pokazuje, co próbujesz *udowodnić* , zamiast podejmować próbę *wykonania*.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-231">Explicitly shows what you're trying to *prove* rather than trying to *accomplish*.</span></span>

<span data-ttu-id="7e5fa-232">Ciągi Magic mogą spowodować pomyłkę dla czytnika testów.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-232">Magic strings can cause confusion to the reader of your tests.</span></span> <span data-ttu-id="7e5fa-233">Jeśli ciąg wyróżni się od zwykłego, może się zastanawiać, dlaczego określona wartość została wybrana dla parametru lub wartości zwracanej.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-233">If a string looks out of the ordinary, they may wonder why a certain value was chosen for a parameter or return value.</span></span> <span data-ttu-id="7e5fa-234">Może to prowadzić do bliższego przyjrzeć się szczegółowym informacjom dotyczącym implementacji, zamiast skupić się na teście.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-234">This may lead them to take a closer look at the implementation details, rather than focus on the test.</span></span>

> [!TIP]
> <span data-ttu-id="7e5fa-235">Podczas pisania testów należy zamierzyć możliwie jak najwięcej założeń.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-235">When writing tests, you should aim to express as much intent as possible.</span></span> <span data-ttu-id="7e5fa-236">W przypadku ciągów magicznych dobrym rozwiązaniem jest przypisanie tych wartości do stałych.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-236">In the case of magic strings, a good approach is to assign these values to constants.</span></span>

#### <a name="bad"></a><span data-ttu-id="7e5fa-237">Źle:</span><span class="sxs-lookup"><span data-stu-id="7e5fa-237">Bad:</span></span>

[!code-csharp[BeforeMagicString](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/before/StringCalculatorTests.cs#BeforeMagicString)]

#### <a name="better"></a><span data-ttu-id="7e5fa-238">Bardziej</span><span class="sxs-lookup"><span data-stu-id="7e5fa-238">Better:</span></span>

[!code-csharp[AfterMagicString](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/after/StringCalculatorTests.cs#AfterMagicString)]

### <a name="avoid-logic-in-tests"></a><span data-ttu-id="7e5fa-239">Unikanie logiki w testach</span><span class="sxs-lookup"><span data-stu-id="7e5fa-239">Avoid logic in tests</span></span>

<span data-ttu-id="7e5fa-240">Podczas pisania testów jednostkowych należy unikać ręcznego łączenia ciągów i warunków logicznych, takich jak,,, `if` `while` `for` `switch` itd.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-240">When writing your unit tests avoid manual string concatenation and logical conditions such as `if`, `while`, `for`, `switch`, etc.</span></span>

#### <a name="why"></a><span data-ttu-id="7e5fa-241">Dlaczego?</span><span class="sxs-lookup"><span data-stu-id="7e5fa-241">Why?</span></span>

- <span data-ttu-id="7e5fa-242">Mniejsza szansa, aby wprowadzić usterkę w testach.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-242">Less chance to introduce a bug inside of your tests.</span></span>
- <span data-ttu-id="7e5fa-243">Skup się na wyniku końca, a nie w szczegółach implementacji.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-243">Focus on the end result, rather than implementation details.</span></span>

<span data-ttu-id="7e5fa-244">Gdy wprowadzasz logikę do zestawu testów, szansa na ich zwiększenie znacznie rośnie.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-244">When you introduce logic into your test suite, the chance of introducing a bug into it increases dramatically.</span></span> <span data-ttu-id="7e5fa-245">Ostatnim miejscem, w którym chcesz znaleźć usterkę, jest zestaw testów.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-245">The last place that you want to find a bug is within your test suite.</span></span> <span data-ttu-id="7e5fa-246">Należy mieć wysoki poziom pewności, że testy działają, w przeciwnym razie nie będzie można ich ufać.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-246">You should have a high level of confidence that your tests work, otherwise, you will not trust them.</span></span> <span data-ttu-id="7e5fa-247">Testy, które nie są zaufane, nie zapewniają żadnej wartości.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-247">Tests that you do not trust, do not provide any value.</span></span> <span data-ttu-id="7e5fa-248">Gdy test zakończy się niepowodzeniem, warto mieć sens, że coś w rzeczywistości jest nieprawidłowe w kodzie i że nie można go zignorować.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-248">When a test fails, you want to have a sense that something is actually wrong with your code and that it cannot be ignored.</span></span>

> [!TIP]
> <span data-ttu-id="7e5fa-249">Jeśli logika w teście wydaje się nienieunikniona, rozważ podzielenie testu na dwa lub więcej różnych testów.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-249">If logic in your test seems unavoidable, consider splitting the test up into two or more different tests.</span></span>

#### <a name="bad"></a><span data-ttu-id="7e5fa-250">Źle:</span><span class="sxs-lookup"><span data-stu-id="7e5fa-250">Bad:</span></span>

[!code-csharp[LogicInTests](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/before/StringCalculatorTests.cs#LogicInTests)]

#### <a name="better"></a><span data-ttu-id="7e5fa-251">Bardziej</span><span class="sxs-lookup"><span data-stu-id="7e5fa-251">Better:</span></span>

[!code-csharp[AfterTestLogic](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/after/StringCalculatorTests.cs#AfterTestLogic)]

### <a name="prefer-helper-methods-to-setup-and-teardown"></a><span data-ttu-id="7e5fa-252">Preferuj metody pomocnika do instalacji i usuwania</span><span class="sxs-lookup"><span data-stu-id="7e5fa-252">Prefer helper methods to setup and teardown</span></span>

<span data-ttu-id="7e5fa-253">Jeśli potrzebujesz podobnego obiektu lub stanu dla testów, Preferuj metodę pomocnika, która jest używana, `Setup` `Teardown` Jeśli istnieją.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-253">If you require a similar object or state for your tests, prefer a helper method than leveraging `Setup` and `Teardown` attributes if they exist.</span></span>

#### <a name="why"></a><span data-ttu-id="7e5fa-254">Dlaczego?</span><span class="sxs-lookup"><span data-stu-id="7e5fa-254">Why?</span></span>

- <span data-ttu-id="7e5fa-255">Mniej pomyłek podczas odczytywania testów, ponieważ cały kod jest widoczny w ramach każdego testu.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-255">Less confusion when reading the tests since all of the code is visible from within each test.</span></span>
- <span data-ttu-id="7e5fa-256">Mniejsza szansa, że zbyt wiele lub zbyt mała dla danego testu.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-256">Less chance of setting up too much or too little for the given test.</span></span>
- <span data-ttu-id="7e5fa-257">Mniejsza szansa stanu udostępniania między testami, która tworzy niepożądane zależności między nimi.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-257">Less chance of sharing state between tests, which creates unwanted dependencies between them.</span></span>

<span data-ttu-id="7e5fa-258">W strukturach testów jednostkowych `Setup` jest wywoływana przed każdym testem jednostkowym w ramach zestawu testów.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-258">In unit testing frameworks, `Setup` is called before each and every unit test within your test suite.</span></span> <span data-ttu-id="7e5fa-259">Niektóre mogą być widoczne jako przydatne narzędzia, zazwyczaj kończą się wiodącym bloated i trudnym do odczytania testów.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-259">While some may see this as a useful tool, it generally ends up leading to bloated and hard to read tests.</span></span> <span data-ttu-id="7e5fa-260">Każdy test ma zwykle różne wymagania, aby można było je uruchomić.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-260">Each test will generally have different requirements in order to get the test up and running.</span></span> <span data-ttu-id="7e5fa-261">Niestety, `Setup` wymusza użycie dokładnie tych samych wymagań dla każdego testu.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-261">Unfortunately, `Setup` forces you to use the exact same requirements for each test.</span></span>

> [!NOTE]
> <span data-ttu-id="7e5fa-262">xUnit usunął zarówno Instalatora, jak i usuwania w wersji 2. x</span><span class="sxs-lookup"><span data-stu-id="7e5fa-262">xUnit has removed both SetUp and TearDown as of version 2.x</span></span>

#### <a name="bad"></a><span data-ttu-id="7e5fa-263">Źle:</span><span class="sxs-lookup"><span data-stu-id="7e5fa-263">Bad:</span></span>

[!code-csharp[BeforeSetup](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/before/StringCalculatorTests.cs#BeforeSetup)]

```csharp
// more tests...
```

[!code-csharp[BeforeHelperMethod](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/before/StringCalculatorTests.cs#BeforeHelperMethod)]

#### <a name="better"></a><span data-ttu-id="7e5fa-264">Bardziej</span><span class="sxs-lookup"><span data-stu-id="7e5fa-264">Better:</span></span>

[!code-csharp[AfterHelperMethod](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/after/StringCalculatorTests.cs#AfterHelperMethod)]

```csharp
// more tests...
```

[!code-csharp[AfterSetup](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/after/StringCalculatorTests.cs#AfterSetup)]

### <a name="avoid-multiple-asserts"></a><span data-ttu-id="7e5fa-265">Unikaj wielu potwierdzeń</span><span class="sxs-lookup"><span data-stu-id="7e5fa-265">Avoid multiple asserts</span></span>

<span data-ttu-id="7e5fa-266">Podczas pisania testów, spróbuj uwzględnić tylko jedno potwierdzenie na test.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-266">When writing your tests, try to only include one Assert per test.</span></span> <span data-ttu-id="7e5fa-267">Typowe podejścia do korzystania tylko z jednego potwierdzenia obejmują:</span><span class="sxs-lookup"><span data-stu-id="7e5fa-267">Common approaches to using only one assert include:</span></span>

- <span data-ttu-id="7e5fa-268">Utwórz oddzielny test dla każdego potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-268">Create a separate test for each assert.</span></span>
- <span data-ttu-id="7e5fa-269">Użyj testów sparametryzowanych.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-269">Use parameterized tests.</span></span>

#### <a name="why"></a><span data-ttu-id="7e5fa-270">Dlaczego?</span><span class="sxs-lookup"><span data-stu-id="7e5fa-270">Why?</span></span>

- <span data-ttu-id="7e5fa-271">Jeśli jedno potwierdzenie nie powiedzie się, kolejne potwierdzenia nie zostaną ocenione.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-271">If one Assert fails, the subsequent Asserts will not be evaluated.</span></span>
- <span data-ttu-id="7e5fa-272">Gwarantuje, że nie postanowisz wielu przypadków w testach.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-272">Ensures you are not asserting multiple cases in your tests.</span></span>
- <span data-ttu-id="7e5fa-273">Zapewnia cały obraz, dlaczego testy kończą się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-273">Gives you the entire picture as to why your tests are failing.</span></span>

<span data-ttu-id="7e5fa-274">W przypadku wprowadzenia wielu potwierdzeń do przypadku testowego nie ma gwarancji, że wszystkie potwierdzenia zostaną wykonane.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-274">When introducing multiple asserts into a test case, it is not guaranteed that all of the asserts will be executed.</span></span> <span data-ttu-id="7e5fa-275">W większości platform testów jednostkowych, gdy potwierdzenie kończy się niepowodzeniem w teście jednostkowym, testy postępu są automatycznie uważane za zakończone niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-275">In most unit testing frameworks, once an assertion fails in a unit test, the proceeding tests are automatically considered to be failing.</span></span> <span data-ttu-id="7e5fa-276">Może to być mylące, ponieważ funkcje, które faktycznie działają, będą wyświetlane jako niepowodzenie.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-276">This can be confusing as functionality that is actually working, will be shown as failing.</span></span>

> [!NOTE]
> <span data-ttu-id="7e5fa-277">Typowym wyjątkiem od tej reguły jest potwierdzenie obiektu.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-277">A common exception to this rule is when asserting against an object.</span></span> <span data-ttu-id="7e5fa-278">W takim przypadku ogólnie akceptowalne jest posiadanie wielu potwierdzeń dla każdej właściwości, aby upewnić się, że obiekt znajduje się w stanie, w którym oczekujesz.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-278">In this case, it is generally acceptable to have multiple asserts against each property to ensure the object is in the state that you expect it to be in.</span></span>

#### <a name="bad"></a><span data-ttu-id="7e5fa-279">Źle:</span><span class="sxs-lookup"><span data-stu-id="7e5fa-279">Bad:</span></span>

[!code-csharp[BeforeMultipleAsserts](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/before/StringCalculatorTests.cs#BeforeMultipleAsserts)]

#### <a name="better"></a><span data-ttu-id="7e5fa-280">Bardziej</span><span class="sxs-lookup"><span data-stu-id="7e5fa-280">Better:</span></span>

[!code-csharp[AfterMultipleAsserts](../../../samples/snippets/core/testing/unit-testing-best-practices/csharp/after/StringCalculatorTests.cs#AfterMultipleAsserts)]

### <a name="validate-private-methods-by-unit-testing-public-methods"></a><span data-ttu-id="7e5fa-281">Weryfikowanie metod prywatnych według metod publicznych testów jednostkowych</span><span class="sxs-lookup"><span data-stu-id="7e5fa-281">Validate private methods by unit testing public methods</span></span>

<span data-ttu-id="7e5fa-282">W większości przypadków nie powinno być konieczne przetestowanie metody prywatnej.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-282">In most cases, there should not be a need to test a private method.</span></span> <span data-ttu-id="7e5fa-283">Metody prywatne są szczegółami implementacji.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-283">Private methods are an implementation detail.</span></span> <span data-ttu-id="7e5fa-284">Można to traktować w ten sposób: metody prywatne nigdy nie istnieją w izolacji.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-284">You can think of it this way: private methods never exist in isolation.</span></span> <span data-ttu-id="7e5fa-285">W pewnym momencie istnieje metoda publiczna, która wywołuje metodę prywatną w ramach jej implementacji.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-285">At some point, there is going to be a public facing method that calls the private method as part of its implementation.</span></span> <span data-ttu-id="7e5fa-286">Informacje o tym, co należy wiedzieć, to wynik metody publicznej, która wywołuje do prywatnego.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-286">What you should care about is the end result of the public method that calls into the private one.</span></span>

<span data-ttu-id="7e5fa-287">Rozważmy następujący przypadek</span><span class="sxs-lookup"><span data-stu-id="7e5fa-287">Consider the following case</span></span>

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

<span data-ttu-id="7e5fa-288">Pierwszą odpowiedzią może być rozpoczęcie pisania testu dla `TrimInput` , ponieważ chcesz upewnić się, że metoda działa zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-288">Your first reaction may be to start writing a test for `TrimInput` because you want to make sure that the method is working as expected.</span></span> <span data-ttu-id="7e5fa-289">Jednak jest on w pełni możliwy, aby `ParseLogLine` manipulować `sanitizedInput` w taki sposób, że nie jest to oczekiwane, renderowanie testu przed `TrimInput` bezużyteczny.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-289">However, it is entirely possible that `ParseLogLine` manipulates `sanitizedInput` in such a way that you do not expect, rendering a test against `TrimInput` useless.</span></span>

<span data-ttu-id="7e5fa-290">Rzeczywisty test powinien być wykonywany w oparciu o publiczną metodę dodaną `ParseLogLine` , ponieważ to to, co powinno być ostatecznie ważne.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-290">The real test should be done against the public facing method `ParseLogLine` because that is what you should ultimately care about.</span></span>

```csharp
public void ParseLogLine_StartsAndEndsWithSpace_ReturnsTrimmedResult()
{
    var parser = new Parser();

    var result = parser.ParseLogLine(" a ");

    Assert.Equals("a", result);
}
```

<span data-ttu-id="7e5fa-291">Jeśli w tym obszarze widać, że jest wyświetlana Metoda prywatna, Znajdź metodę publiczną i napisz testy dla tej metody.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-291">With this viewpoint, if you see a private method, find the public method and write your tests against that method.</span></span> <span data-ttu-id="7e5fa-292">Tylko dlatego, że Metoda prywatna zwraca oczekiwany wynik, nie oznacza, że system, który ostatecznie wywołuje metodę prywatną, użyje poprawnego wyniku.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-292">Just because a private method returns the expected result, does not mean the system that eventually calls the private method uses the result correctly.</span></span>

### <a name="stub-static-references"></a><span data-ttu-id="7e5fa-293">Zastępcze odwołania statyczne</span><span class="sxs-lookup"><span data-stu-id="7e5fa-293">Stub static references</span></span>

<span data-ttu-id="7e5fa-294">Jedną z zasad testów jednostkowych jest to, że musi ona mieć pełną kontrolę nad testowanym systemem.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-294">One of the principles of a unit test is that it must have full control of the system under test.</span></span> <span data-ttu-id="7e5fa-295">Może to być problematyczne, gdy kod produkcyjny zawiera wywołania do odwołań statycznych (na przykład `DateTime.Now` ).</span><span class="sxs-lookup"><span data-stu-id="7e5fa-295">This can be problematic when production code includes calls to static references (for example, `DateTime.Now`).</span></span> <span data-ttu-id="7e5fa-296">Rozważmy następujący kod</span><span class="sxs-lookup"><span data-stu-id="7e5fa-296">Consider the following code</span></span>

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

<span data-ttu-id="7e5fa-297">Jak ten kod może być testowany jednostkowo?</span><span class="sxs-lookup"><span data-stu-id="7e5fa-297">How can this code possibly be unit tested?</span></span> <span data-ttu-id="7e5fa-298">Możesz wypróbować takie podejście jak</span><span class="sxs-lookup"><span data-stu-id="7e5fa-298">You may try an approach such as</span></span>

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

<span data-ttu-id="7e5fa-299">Niestety, możesz szybko zapamiętać, że istnieje kilka problemów z testami.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-299">Unfortunately, you will quickly realize that there are a couple problems with your tests.</span></span>

- <span data-ttu-id="7e5fa-300">Jeśli zestaw testów jest uruchamiany w wtorek, drugi test zostanie przekazany, ale pierwszy test zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-300">If the test suite is run on a Tuesday, the second test will pass, but the first test will fail.</span></span>
- <span data-ttu-id="7e5fa-301">Jeśli zestaw testów jest uruchamiany z dowolnego innego dnia, pierwszy test zostanie przekazany, ale drugi test zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-301">If the test suite is run on any other day, the first test will pass, but the second test will fail.</span></span>

<span data-ttu-id="7e5fa-302">Aby rozwiązać te problemy, należy wprowadzić *szew* w kodzie produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-302">To solve these problems, you'll need to introduce a *seam* into your production code.</span></span> <span data-ttu-id="7e5fa-303">Jednym z metod jest Zawijanie kodu, który należy kontrolować w interfejsie i że kod produkcyjny zależy od tego interfejsu.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-303">One approach is to wrap the code that you need to control in an interface and have the production code depend on that interface.</span></span>

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

<span data-ttu-id="7e5fa-304">Zestaw testów zostanie teraz</span><span class="sxs-lookup"><span data-stu-id="7e5fa-304">Your test suite now becomes</span></span>

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

<span data-ttu-id="7e5fa-305">Teraz zestaw testów ma pełną kontrolę nad `DateTime.Now` i może być dowolną wartością podczas wywoływania metody.</span><span class="sxs-lookup"><span data-stu-id="7e5fa-305">Now the test suite has full control over `DateTime.Now` and can stub any value when calling into the method.</span></span>
