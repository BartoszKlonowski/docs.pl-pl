---
title: Testowanie aplikacji ASP.NET Core MVC
description: Tworzenie architektury nowoczesnych aplikacji sieci Web przy użyciu ASP.NET Core i platformy Azure | Testowanie aplikacji ASP.NET Core MVC
author: ardalis
ms.author: wiwagn
ms.date: 12/01/2020
ms.openlocfilehash: b253cfb90487cc462b0f3b8a7564c97ad403aa06
ms.sourcegitcommit: 45c7148f2483db2501c1aa696ab6ed2ed8cb71b2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/08/2020
ms.locfileid: "96851402"
---
# <a name="test-aspnet-core-mvc-apps"></a><span data-ttu-id="2d567-103">Testowanie aplikacji ASP.NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="2d567-103">Test ASP.NET Core MVC apps</span></span>

> <span data-ttu-id="2d567-104">*"Jeśli nie podoba Ci się testowanie jednostkowe produktu, najprawdopodobniej nie chcesz przetestować go."*</span><span class="sxs-lookup"><span data-stu-id="2d567-104">*"If you don't like unit testing your product, most likely your customers won't like to test it, either."*</span></span>
 > <span data-ttu-id="2d567-105">\_Anonimowe</span><span class="sxs-lookup"><span data-stu-id="2d567-105">\_- Anonymous-</span></span>

<span data-ttu-id="2d567-106">Oprogramowanie dowolnej złożoności może zakończyć się niepowodzeniem na nieoczekiwanych sposobach w reakcji na zmiany.</span><span class="sxs-lookup"><span data-stu-id="2d567-106">Software of any complexity can fail in unexpected ways in response to changes.</span></span> <span data-ttu-id="2d567-107">W ten sposób testowanie po wprowadzeniu zmian jest wymagane dla wszystkich, ale najbardziej prostych (lub najmniej krytycznych) aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2d567-107">Thus, testing after making changes is required for all but the most trivial (or least critical) applications.</span></span> <span data-ttu-id="2d567-108">Testowanie ręczne to najwolniejsze, najmniej niezawodne, najbardziej kosztowne rozwiązanie do testowania oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="2d567-108">Manual testing is the slowest, least reliable, most expensive way to test software.</span></span> <span data-ttu-id="2d567-109">Niestety, jeśli aplikacje nie mają być weryfikowalne, może to być tylko dostępne.</span><span class="sxs-lookup"><span data-stu-id="2d567-109">Unfortunately, if applications aren't designed to be testable, it can be the only means available.</span></span> <span data-ttu-id="2d567-110">Aplikacje przygotowane do przestrzegania zasad architektonicznych, które zostały określone w [rozdziale 4](architectural-principles.md) powinny być weryfikowalne jednostkowym.</span><span class="sxs-lookup"><span data-stu-id="2d567-110">Applications written to follow the architectural principles laid out in [chapter 4](architectural-principles.md) should be unit testable.</span></span> <span data-ttu-id="2d567-111">Aplikacje ASP.NET Core obsługują zautomatyzowaną integrację i testowanie funkcjonalne.</span><span class="sxs-lookup"><span data-stu-id="2d567-111">ASP.NET Core applications support automated integration and functional testing.</span></span>

## <a name="kinds-of-automated-tests"></a><span data-ttu-id="2d567-112">Rodzaje testów automatycznych</span><span class="sxs-lookup"><span data-stu-id="2d567-112">Kinds of automated tests</span></span>

<span data-ttu-id="2d567-113">Istnieje wiele rodzajów zautomatyzowanych testów dla aplikacji oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="2d567-113">There are many kinds of automated tests for software applications.</span></span> <span data-ttu-id="2d567-114">Najprostszym, najniższym poziomem testu jest test jednostkowy.</span><span class="sxs-lookup"><span data-stu-id="2d567-114">The simplest, lowest level test is the unit test.</span></span> <span data-ttu-id="2d567-115">Na nieco wyższym poziomie istnieją testy integracji i testy funkcjonalne.</span><span class="sxs-lookup"><span data-stu-id="2d567-115">At a slightly higher level, there are integration tests and functional tests.</span></span> <span data-ttu-id="2d567-116">Inne rodzaje testów, takie jak testy interfejsu użytkownika, testy obciążeniowe, testy obciążeniowe i testy dymu, wykraczają poza zakres tego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="2d567-116">Other kinds of tests, such as UI tests, load tests, stress tests, and smoke tests, are beyond the scope of this document.</span></span>

### <a name="unit-tests"></a><span data-ttu-id="2d567-117">Testy jednostkowe</span><span class="sxs-lookup"><span data-stu-id="2d567-117">Unit tests</span></span>

<span data-ttu-id="2d567-118">Test jednostkowy testów pojedynczej części logiki aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2d567-118">A unit test tests a single part of your application's logic.</span></span> <span data-ttu-id="2d567-119">Jeden z nich może jeszcze bardziej opisać, wyświetlając niektóre z tych rzeczy.</span><span class="sxs-lookup"><span data-stu-id="2d567-119">One can further describe it by listing some of the things that it isn't.</span></span> <span data-ttu-id="2d567-120">Test jednostkowy nie testuje, w jaki sposób kod współpracuje z zależnościami lub infrastrukturą — to są testy integracji.</span><span class="sxs-lookup"><span data-stu-id="2d567-120">A unit test doesn't test how your code works with dependencies or infrastructure – that's what integration tests are for.</span></span> <span data-ttu-id="2d567-121">Test jednostkowy nie przetestuje struktury kodu, w którym jest on pisany — należy zastanowić się, że działa lub, jeśli okaże się, że nie, należy zgłosić błąd i napisać obejście problemu.</span><span class="sxs-lookup"><span data-stu-id="2d567-121">A unit test doesn't test the framework your code is written on – you should assume it works or, if you find it doesn't, file a bug and code a workaround.</span></span> <span data-ttu-id="2d567-122">Test jednostkowy jest całkowicie wykonywany w pamięci i w procesie.</span><span class="sxs-lookup"><span data-stu-id="2d567-122">A unit test runs completely in memory and in process.</span></span> <span data-ttu-id="2d567-123">Nie komunikuje się z systemem plików, siecią lub bazą danych.</span><span class="sxs-lookup"><span data-stu-id="2d567-123">It doesn't communicate with the file system, the network, or a database.</span></span> <span data-ttu-id="2d567-124">Testy jednostkowe powinny tylko testować kod.</span><span class="sxs-lookup"><span data-stu-id="2d567-124">Unit tests should only test your code.</span></span>

<span data-ttu-id="2d567-125">Testy jednostkowe, na mocy których testuje tylko jedną jednostkę kodu bez zależności zewnętrznych, powinny być wykonywane bardzo szybko.</span><span class="sxs-lookup"><span data-stu-id="2d567-125">Unit tests, by virtue of the fact that they test only a single unit of your code, with no external dependencies, should execute extremely fast.</span></span> <span data-ttu-id="2d567-126">Z tego względu powinno być możliwe uruchamianie zestawów testów dla setek testów jednostkowych w ciągu kilku sekund.</span><span class="sxs-lookup"><span data-stu-id="2d567-126">Thus, you should be able to run test suites of hundreds of unit tests in a few seconds.</span></span> <span data-ttu-id="2d567-127">Uruchamiaj je często, najlepiej przed każdym wypchnięciem do udostępnionego repozytorium kontroli źródła i z pewnością przy każdej zautomatyzowanej kompilacji na serwerze kompilacji.</span><span class="sxs-lookup"><span data-stu-id="2d567-127">Run them frequently, ideally before every push to a shared source control repository, and certainly with every automated build on your build server.</span></span>

### <a name="integration-tests"></a><span data-ttu-id="2d567-128">Testy integracji</span><span class="sxs-lookup"><span data-stu-id="2d567-128">Integration tests</span></span>

<span data-ttu-id="2d567-129">Chociaż dobrym pomysłem jest Hermetyzowanie kodu, który współdziała z infrastrukturą, taką jak bazy danych i systemy plików, nadal będziesz mieć część tego kodu i prawdopodobnie chcesz go przetestować.</span><span class="sxs-lookup"><span data-stu-id="2d567-129">Although it's a good idea to encapsulate your code that interacts with infrastructure like databases and file systems, you will still have some of that code, and you will probably want to test it.</span></span> <span data-ttu-id="2d567-130">Ponadto należy sprawdzić, czy warstwy kodu działają w oczekiwany sposób, gdy zależności aplikacji są w pełni rozwiązane.</span><span class="sxs-lookup"><span data-stu-id="2d567-130">Additionally, you should verify that your code's layers interact as you expect when your application's dependencies are fully resolved.</span></span> <span data-ttu-id="2d567-131">Ta funkcja jest odpowiedzialna za testy integracji.</span><span class="sxs-lookup"><span data-stu-id="2d567-131">This functionality is the responsibility of integration tests.</span></span> <span data-ttu-id="2d567-132">Testy integracji są znacznie wolniejsze i trudniejsze do skonfigurowania niż testy jednostkowe, ponieważ często zależą od zewnętrznych zależności i infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="2d567-132">Integration tests tend to be slower and more difficult to set up than unit tests, because they often depend on external dependencies and infrastructure.</span></span> <span data-ttu-id="2d567-133">W tym celu należy unikać testowania, które mogą być testowane przy użyciu testów jednostkowych w testach integracji.</span><span class="sxs-lookup"><span data-stu-id="2d567-133">Thus, you should avoid testing things that could be tested with unit tests in integration tests.</span></span> <span data-ttu-id="2d567-134">Jeśli można testować dany scenariusz z testem jednostkowym, należy przetestować go z testem jednostkowym.</span><span class="sxs-lookup"><span data-stu-id="2d567-134">If you can test a given scenario with a unit test, you should test it with a unit test.</span></span> <span data-ttu-id="2d567-135">Jeśli nie jest to możliwe, rozważ użycie testu integracji.</span><span class="sxs-lookup"><span data-stu-id="2d567-135">If you can't, then consider using an integration test.</span></span>

<span data-ttu-id="2d567-136">Testy integracji często mają bardziej skomplikowane ustawienia i usuwania procedury niż testy jednostkowe.</span><span class="sxs-lookup"><span data-stu-id="2d567-136">Integration tests will often have more complex setup and teardown procedures than unit tests.</span></span> <span data-ttu-id="2d567-137">Na przykład test integracji, który przechodzi względem rzeczywistej bazy danych, będzie wymagał metody przywrócenia bazy danych do znanego stanu przed każdym uruchomieniem testu.</span><span class="sxs-lookup"><span data-stu-id="2d567-137">For example, an integration test that goes against an actual database will need a way to return the database to a known state before each test run.</span></span> <span data-ttu-id="2d567-138">Po dodaniu nowych testów, a produkcyjny schemat bazy danych, te skrypty te zależą od rozmiaru i złożoności.</span><span class="sxs-lookup"><span data-stu-id="2d567-138">As new tests are added and the production database schema evolves, these test scripts will tend to grow in size and complexity.</span></span> <span data-ttu-id="2d567-139">W wielu dużych systemach nie ma praktycznego uruchamiania pełnych zestawów testów integracji na stacjach roboczych deweloperów przed zaewidencjonowaniem zmian w udostępnionej kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="2d567-139">In many large systems, it is impractical to run full suites of integration tests on developer workstations before checking in changes to shared source control.</span></span> <span data-ttu-id="2d567-140">W takich przypadkach testy integracji mogą być uruchamiane na serwerze kompilacji.</span><span class="sxs-lookup"><span data-stu-id="2d567-140">In these cases, integration tests may be run on a build server.</span></span>

### <a name="functional-tests"></a><span data-ttu-id="2d567-141">Testy funkcjonalne</span><span class="sxs-lookup"><span data-stu-id="2d567-141">Functional tests</span></span>

<span data-ttu-id="2d567-142">Testy integracji są napisywane od perspektywy dewelopera, aby sprawdzić, czy niektóre składniki systemu działają prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="2d567-142">Integration tests are written from the perspective of the developer, to verify that some components of the system work correctly together.</span></span> <span data-ttu-id="2d567-143">Testy funkcjonalne są zapisywane z perspektywy użytkownika i sprawdzają poprawność systemu w zależności od wymagań.</span><span class="sxs-lookup"><span data-stu-id="2d567-143">Functional tests are written from the perspective of the user, and verify the correctness of the system based on its requirements.</span></span> <span data-ttu-id="2d567-144">Poniższy fragment przedstawia przydatną funkcję analogową do rozważania, jak należy wziąć pod uwagę testy funkcjonalne w porównaniu z testami jednostkowymi:</span><span class="sxs-lookup"><span data-stu-id="2d567-144">The following excerpt offers a useful analogy for how to think about functional tests, compared to unit tests:</span></span>

> <span data-ttu-id="2d567-145">"Wiele razy rozwój systemu jest likened do budynku w domu.</span><span class="sxs-lookup"><span data-stu-id="2d567-145">"Many times the development of a system is likened to the building of a house.</span></span> <span data-ttu-id="2d567-146">Chociaż ta wartość analogiczna nie jest poprawna, możemy ją rozłożyć na potrzeby ustalenia różnicy między testami jednostkowymi i funkcjonalnymi.</span><span class="sxs-lookup"><span data-stu-id="2d567-146">While this analogy isn't quite correct, we can extend it for the purposes of understanding the difference between unit and functional tests.</span></span> <span data-ttu-id="2d567-147">Testy jednostkowe są analogiczne do Inspektora konstrukcyjnego odwiedzającego witrynę konstrukcyjną domu.</span><span class="sxs-lookup"><span data-stu-id="2d567-147">Unit testing is analogous to a building inspector visiting a house's construction site.</span></span> <span data-ttu-id="2d567-148">Koncentruje się na różnych systemach wewnętrznych, fundamentach, ramkach, elektrycznych, wodociągowych i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="2d567-148">He is focused on the various internal systems of the house, the foundation, framing, electrical, plumbing, and so on.</span></span> <span data-ttu-id="2d567-149">Gwarantuje (testy), że części domu będą działały prawidłowo i bezpiecznie, czyli spełniają kod budynku.</span><span class="sxs-lookup"><span data-stu-id="2d567-149">He ensures (tests) that the parts of the house will work correctly and safely, that is, meet the building code.</span></span> <span data-ttu-id="2d567-150">Testy funkcjonalne w tym scenariuszu są analogiczne do Homeowner odwiedzania tej samej lokacji konstrukcja.</span><span class="sxs-lookup"><span data-stu-id="2d567-150">Functional tests in this scenario are analogous to the homeowner visiting this same construction site.</span></span> <span data-ttu-id="2d567-151">Przyjęto założenie, że systemy wewnętrzne będą działać odpowiednio, że Inspektor budynku wykonuje jego zadanie.</span><span class="sxs-lookup"><span data-stu-id="2d567-151">He assumes that the internal systems will behave appropriately, that the building inspector is performing his task.</span></span> <span data-ttu-id="2d567-152">Homeowner koncentruje się na tym, co będzie wyglądać na żywo w tym domu.</span><span class="sxs-lookup"><span data-stu-id="2d567-152">The homeowner is focused on what it will be like to live in this house.</span></span> <span data-ttu-id="2d567-153">Ma ona wpływ na wygląd domu, czy różne pokoje są wygodne, czy najlepiej odpowiadają potrzebom rodziny, czy w systemie Windows jest dobrym miejscem, aby przechwycić rano Sun.</span><span class="sxs-lookup"><span data-stu-id="2d567-153">He is concerned with how the house looks, are the various rooms a comfortable size, does the house fit the family's needs, are the windows in a good spot to catch the morning sun.</span></span> <span data-ttu-id="2d567-154">Homeowner wykonuje testy funkcjonalne w domu.</span><span class="sxs-lookup"><span data-stu-id="2d567-154">The homeowner is performing functional tests on the house.</span></span> <span data-ttu-id="2d567-155">Ma perspektywę użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2d567-155">He has the user's perspective.</span></span> <span data-ttu-id="2d567-156">Inspektor budowlany przeprowadza testy jednostkowe w domu.</span><span class="sxs-lookup"><span data-stu-id="2d567-156">The building inspector is performing unit tests on the house.</span></span> <span data-ttu-id="2d567-157">Ma perspektywę konstruktora ".</span><span class="sxs-lookup"><span data-stu-id="2d567-157">He has the builder's perspective."</span></span>

<span data-ttu-id="2d567-158">Źródło: [testowanie jednostkowe i testy funkcjonalne](https://www.softwaretestingtricks.com/2007/01/unit-testing-versus-functional-tests.html)</span><span class="sxs-lookup"><span data-stu-id="2d567-158">Source: [Unit Testing versus Functional Tests](https://www.softwaretestingtricks.com/2007/01/unit-testing-versus-functional-tests.html)</span></span>

<span data-ttu-id="2d567-159">Fond się powiedzieć "jako Deweloperzy, ale kończymy się niepowodzeniem na dwa sposoby: możemy utworzyć niewłaściwy element lub stworzyć niewłaściwy element".</span><span class="sxs-lookup"><span data-stu-id="2d567-159">I'm fond of saying "As developers, we fail in two ways: we build the thing wrong, or we build the wrong thing."</span></span> <span data-ttu-id="2d567-160">Testy jednostkowe gwarantują, że tworzysz to prawo; testy funkcjonalne zapewniają, że tworzysz odpowiednie rzeczy.</span><span class="sxs-lookup"><span data-stu-id="2d567-160">Unit tests ensure you are building the thing right; functional tests ensure you are building the right thing.</span></span>

<span data-ttu-id="2d567-161">Ponieważ testy funkcjonalne działają na poziomie systemu, mogą wymagać pewnego stopnia automatyzacji interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2d567-161">Since functional tests operate at the system level, they may require some degree of UI automation.</span></span> <span data-ttu-id="2d567-162">Podobnie jak w przypadku testów integracji, zazwyczaj działają one również w przypadku niektórych rodzajów infrastruktury testowej.</span><span class="sxs-lookup"><span data-stu-id="2d567-162">Like integration tests, they usually work with some kind of test infrastructure as well.</span></span> <span data-ttu-id="2d567-163">To działanie sprawia, że są one wolniejsze i bardziej kruchy niż testy jednostkowe i integracji.</span><span class="sxs-lookup"><span data-stu-id="2d567-163">This activity makes them slower and more brittle than unit and integration tests.</span></span> <span data-ttu-id="2d567-164">Należy mieć tylko tyle testów funkcjonalnych, ile trzeba mieć pewność, że system zachowuje się, gdy użytkownicy oczekują.</span><span class="sxs-lookup"><span data-stu-id="2d567-164">You should have only as many functional tests as you need to be confident the system is behaving as users expect.</span></span>

### <a name="testing-pyramid"></a><span data-ttu-id="2d567-165">Piramida testowania</span><span class="sxs-lookup"><span data-stu-id="2d567-165">Testing Pyramid</span></span>

<span data-ttu-id="2d567-166">Fowlera Martin na temat ostrosłupa testowego, którego przykład przedstawiono na rysunku 9-1.</span><span class="sxs-lookup"><span data-stu-id="2d567-166">Martin Fowler wrote about the testing pyramid, an example of which is shown in Figure 9-1.</span></span>

![Piramida testowania](./media/image9-1.png)

<span data-ttu-id="2d567-168">**Rysunek 9-1**.</span><span class="sxs-lookup"><span data-stu-id="2d567-168">**Figure 9-1**.</span></span> <span data-ttu-id="2d567-169">Piramida testowania</span><span class="sxs-lookup"><span data-stu-id="2d567-169">Testing Pyramid</span></span>

<span data-ttu-id="2d567-170">Różne warstwy ostrosłupa i ich względne rozmiary reprezentują różne rodzaje testów oraz liczbę elementów, które należy napisać dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2d567-170">The different layers of the pyramid, and their relative sizes, represent different kinds of tests and how many you should write for your application.</span></span> <span data-ttu-id="2d567-171">Jak widać, zalecenie ma mieć dużą podstawę testów jednostkowych, które są obsługiwane przez niższą warstwę testów integracji, z jeszcze mniejszą warstwą testów funkcjonalnych.</span><span class="sxs-lookup"><span data-stu-id="2d567-171">As you can see, the recommendation is to have a large base of unit tests, supported by a smaller layer of integration tests, with an even smaller layer of functional tests.</span></span> <span data-ttu-id="2d567-172">Każda warstwa powinna mieć idealny tylko testy, które nie mogą być wykonywane odpowiednio na niższej warstwie.</span><span class="sxs-lookup"><span data-stu-id="2d567-172">Each layer should ideally only have tests in it that cannot be performed adequately at a lower layer.</span></span> <span data-ttu-id="2d567-173">Zadbaj o to, aby określić, jakiego rodzaju testu potrzebujesz w konkretnym scenariuszu.</span><span class="sxs-lookup"><span data-stu-id="2d567-173">Keep the testing pyramid in mind when you are trying to decide which kind of test you need for a particular scenario.</span></span>

### <a name="what-to-test"></a><span data-ttu-id="2d567-174">Co należy przetestować</span><span class="sxs-lookup"><span data-stu-id="2d567-174">What to test</span></span>

<span data-ttu-id="2d567-175">Typowy problem dla deweloperów, którzy są niedoświadczeni z pisaniem zautomatyzowanych testów, jest tworzony z przeznaczeniem do przetestowania.</span><span class="sxs-lookup"><span data-stu-id="2d567-175">A common problem for developers who are inexperienced with writing automated tests is coming up with what to test.</span></span> <span data-ttu-id="2d567-176">Dobrym punktem początkowym jest Testowanie logiki warunkowej.</span><span class="sxs-lookup"><span data-stu-id="2d567-176">A good starting point is to test conditional logic.</span></span> <span data-ttu-id="2d567-177">Wszędzie tam, gdzie masz metodę z zachowaniem, która zmienia się na podstawie instrukcji warunkowej (if-else, Switch itd.), powinna być dostępna co najmniej kilka testów, które potwierdzają poprawne zachowanie określonych warunków.</span><span class="sxs-lookup"><span data-stu-id="2d567-177">Anywhere you have a method with behavior that changes based on a conditional statement (if-else, switch, and so on), you should be able to come up with at least a couple of tests that confirm the correct behavior for certain conditions.</span></span> <span data-ttu-id="2d567-178">Jeśli kod zawiera warunki błędu, warto napisać co najmniej jeden test dla "silnej ścieżki" przez kod (bez błędów) i co najmniej jeden test dla "ścieżki sad" (z błędami lub nietypowymi wynikami), aby potwierdzić, że aplikacja działa zgodnie z oczekiwaniami w przypadku błędów.</span><span class="sxs-lookup"><span data-stu-id="2d567-178">If your code has error conditions, it's good to write at least one test for the "happy path" through the code (with no errors), and at least one test for the "sad path" (with errors or atypical results) to confirm your application behaves as expected in the face of errors.</span></span> <span data-ttu-id="2d567-179">Na koniec spróbuj skupić się na testowaniu rzeczy, które mogą się nie powieść, zamiast skupić się na metrykach, takich jak pokrycie kodu.</span><span class="sxs-lookup"><span data-stu-id="2d567-179">Finally, try to focus on testing things that can fail, rather than focusing on metrics like code coverage.</span></span> <span data-ttu-id="2d567-180">Większa ilość pokrycia kodu jest lepsza niż mniej, ogólnie.</span><span class="sxs-lookup"><span data-stu-id="2d567-180">More code coverage is better than less, generally.</span></span> <span data-ttu-id="2d567-181">Jednak zapisanie kilku dodatkowych testów złożonej i krytycznej dla firmy jest zwykle lepszym wykorzystaniem czasu niż podczas pisania testów dla właściwości autoproperties tylko w celu poprawy metryk pokrycia kodu testowego.</span><span class="sxs-lookup"><span data-stu-id="2d567-181">However, writing a few more tests of a complex and business-critical method is usually a better use of time than writing tests for auto-properties just to improve test code coverage metrics.</span></span>

## <a name="organizing-test-projects"></a><span data-ttu-id="2d567-182">Organizowanie projektów testowych</span><span class="sxs-lookup"><span data-stu-id="2d567-182">Organizing test projects</span></span>

<span data-ttu-id="2d567-183">Projekty testowe mogą być zorganizowane, jednak najlepiej sprawdzają się.</span><span class="sxs-lookup"><span data-stu-id="2d567-183">Test projects can be organized however works best for you.</span></span> <span data-ttu-id="2d567-184">Dobrym pomysłem jest oddzielenie testów według typu (test jednostkowy, test integracji) i ich testowanie (według projektu, według przestrzeni nazw).</span><span class="sxs-lookup"><span data-stu-id="2d567-184">It's a good idea to separate tests by type (unit test, integration test) and by what they are testing (by project, by namespace).</span></span> <span data-ttu-id="2d567-185">Czy ta separacja składa się z folderów w ramach pojedynczego projektu testowego lub wielu projektów testowych, stanowi decyzję projektową.</span><span class="sxs-lookup"><span data-stu-id="2d567-185">Whether this separation consists of folders within a single test project, or multiple test projects, is a design decision.</span></span> <span data-ttu-id="2d567-186">Jeden projekt jest najprostszy, ale w przypadku dużych projektów z wieloma testami lub w celu łatwiejszego uruchamiania różnych zestawów testów można chcieć mieć kilka różnych projektów testowych.</span><span class="sxs-lookup"><span data-stu-id="2d567-186">One project is simplest, but for large projects with many tests, or in order to more easily run different sets of tests, you might want to have several different test projects.</span></span> <span data-ttu-id="2d567-187">Wiele zespołów organizuje projekty testowe na podstawie testowanego projektu, co w przypadku aplikacji z więcej niż kilkoma projektami może spowodować powstanie dużej liczby projektów testowych, szczególnie w przypadku, gdy te dane są nadal dzielone zgodnie z typem testów w każdym projekcie.</span><span class="sxs-lookup"><span data-stu-id="2d567-187">Many teams organize test projects based on the project they are testing, which for applications with more than a few projects can result in a large number of test projects, especially if you still break these down according to what kind of tests are in each project.</span></span> <span data-ttu-id="2d567-188">Podejście do kompromisu polega na tym, że jeden projekt dla każdego rodzaju testu, na aplikację, z folderami w projektach testowych, ma wskazywać testowany projekt (i klasę).</span><span class="sxs-lookup"><span data-stu-id="2d567-188">A compromise approach is to have one project per kind of test, per application, with folders inside the test projects to indicate the project (and class) being tested.</span></span>

<span data-ttu-id="2d567-189">Typowym podejściem jest organizowanie projektów aplikacji w folderze "src" i projektów testowych aplikacji w ramach równoległego folderu "Tests".</span><span class="sxs-lookup"><span data-stu-id="2d567-189">A common approach is to organize the application projects under a 'src' folder, and the application's test projects under a parallel 'tests' folder.</span></span> <span data-ttu-id="2d567-190">Można utworzyć dopasowane foldery rozwiązań w programie Visual Studio, jeśli okaże się to przydatne w tej organizacji.</span><span class="sxs-lookup"><span data-stu-id="2d567-190">You can create matching solution folders in Visual Studio, if you find this organization useful.</span></span>

![Testowanie organizacji w rozwiązaniu](./media/image9-2.png)

<span data-ttu-id="2d567-192">**Rysunek 9-2**.</span><span class="sxs-lookup"><span data-stu-id="2d567-192">**Figure 9-2**.</span></span> <span data-ttu-id="2d567-193">Testowanie organizacji w rozwiązaniu</span><span class="sxs-lookup"><span data-stu-id="2d567-193">Test organization in your solution</span></span>

<span data-ttu-id="2d567-194">Możesz użyć niezależnej platformy testowej.</span><span class="sxs-lookup"><span data-stu-id="2d567-194">You can use whichever test framework you prefer.</span></span> <span data-ttu-id="2d567-195">Środowisko xUnit Framework działa prawidłowo i jest zapisywana wszystkie ASP.NET Core i EF Core testy.</span><span class="sxs-lookup"><span data-stu-id="2d567-195">The xUnit framework works well and is what all of the ASP.NET Core and EF Core tests are written in.</span></span> <span data-ttu-id="2d567-196">Możesz dodać projekt testu xUnit w programie Visual Studio przy użyciu szablonu pokazanego na rysunku 9-3 lub interfejsu wiersza polecenia przy użyciu polecenia `dotnet new xunit` .</span><span class="sxs-lookup"><span data-stu-id="2d567-196">You can add an xUnit test project in Visual Studio using the template shown in Figure 9-3, or from the CLI using `dotnet new xunit`.</span></span>

![Dodawanie projektu testowego xUnit w programie Visual Studio](./media/image9-3.png)

<span data-ttu-id="2d567-198">**Rysunek 9-3**.</span><span class="sxs-lookup"><span data-stu-id="2d567-198">**Figure 9-3**.</span></span> <span data-ttu-id="2d567-199">Dodawanie projektu testowego xUnit w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2d567-199">Add an xUnit Test Project in Visual Studio</span></span>

### <a name="test-naming"></a><span data-ttu-id="2d567-200">Nazwa testu</span><span class="sxs-lookup"><span data-stu-id="2d567-200">Test naming</span></span>

<span data-ttu-id="2d567-201">Nazwij testy w spójny sposób, podając nazwy wskazujące, co każdy test wykonuje.</span><span class="sxs-lookup"><span data-stu-id="2d567-201">Name your tests in a consistent fashion, with names that indicate what each test does.</span></span> <span data-ttu-id="2d567-202">Jednym z metod, które mam doskonałe sukces, jest nazwa klasy testowej zgodnie z klasą i metodą, które są testowane.</span><span class="sxs-lookup"><span data-stu-id="2d567-202">One approach I've had great success with is to name test classes according to the class and method they are testing.</span></span> <span data-ttu-id="2d567-203">To podejście skutkuje wieloma niewielkimi klasami testowymi, ale wyraźnie czyści, do czego każdy test jest odpowiedzialny.</span><span class="sxs-lookup"><span data-stu-id="2d567-203">This approach results in many small test classes, but it makes it extremely clear what each test is responsible for.</span></span> <span data-ttu-id="2d567-204">Po skonfigurowaniu nazwy klasy testowej, aby zidentyfikować klasę i metodę do przetestowania, nazwa metody testowej może służyć do określenia testowanego zachowania.</span><span class="sxs-lookup"><span data-stu-id="2d567-204">With the test class name set up, to identify the class and method to be tested, the test method name can be used to specify the behavior being tested.</span></span> <span data-ttu-id="2d567-205">Ta nazwa powinna zawierać oczekiwane zachowanie i wszelkie dane wejściowe lub założenia, które powinny spowodować takie zachowanie.</span><span class="sxs-lookup"><span data-stu-id="2d567-205">This name should include the expected behavior and any inputs or assumptions that should yield this behavior.</span></span> <span data-ttu-id="2d567-206">Przykładowe nazwy testów:</span><span class="sxs-lookup"><span data-stu-id="2d567-206">Some example test names:</span></span>

- `CatalogControllerGetImage.CallsImageServiceWithId`

- `CatalogControllerGetImage.LogsWarningGivenImageMissingException`

- `CatalogControllerGetImage.ReturnsFileResultWithBytesGivenSuccess`

- `CatalogControllerGetImage.ReturnsNotFoundResultGivenImageMissingException`

<span data-ttu-id="2d567-207">Zmiana tego podejścia spowoduje zakończenie każdej klasy testowej o nazwie "powinien" i nieco modyfikuje intensywność:</span><span class="sxs-lookup"><span data-stu-id="2d567-207">A variation of this approach ends each test class name with "Should" and modifies the tense slightly:</span></span>

- <span data-ttu-id="2d567-208">`CatalogControllerGetImage`**Powinien** `.` **Wywołanie**`ImageServiceWithId`</span><span class="sxs-lookup"><span data-stu-id="2d567-208">`CatalogControllerGetImage`**Should**`.`**Call**`ImageServiceWithId`</span></span>

- <span data-ttu-id="2d567-209">`CatalogControllerGetImage`**Powinien** `.` **Dziennik**`WarningGivenImageMissingException`</span><span class="sxs-lookup"><span data-stu-id="2d567-209">`CatalogControllerGetImage`**Should**`.`**Log**`WarningGivenImageMissingException`</span></span>

<span data-ttu-id="2d567-210">Niektóre zespoły szukają drugiego podejścia do nazewnictwa, chociaż nieco bardziej pełne.</span><span class="sxs-lookup"><span data-stu-id="2d567-210">Some teams find the second naming approach clearer, though slightly more verbose.</span></span> <span data-ttu-id="2d567-211">W każdym przypadku spróbuj użyć konwencji nazewnictwa, która zapewnia wgląd w działanie testowe, dzięki czemu w przypadku niepowodzenia co najmniej jednego testu, jest oczywiste z nazw, których przypadki zakończyły się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="2d567-211">In any case, try to use a naming convention that provides insight into test behavior, so that when one or more tests fail, it's obvious from their names what cases have failed.</span></span> <span data-ttu-id="2d567-212">Unikaj niejasnego nazewnictwa testów, takich jak ControllerTests. TEST1, ponieważ te nazwy nie oferują wartości, gdy są widoczne w wynikach testu.</span><span class="sxs-lookup"><span data-stu-id="2d567-212">Avoid naming your tests vaguely, such as ControllerTests.Test1, as these names offer no value when you see them in test results.</span></span>

<span data-ttu-id="2d567-213">Jeśli przestrzegasz konwencji nazewnictwa, takiej jak powyżej, która tworzy wiele małych klas testowych, dobrym pomysłem jest dalsze organizowanie testów przy użyciu folderów i przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="2d567-213">If you follow a naming convention like the one above that produces many small test classes, it's a good idea to further organize your tests using folders and namespaces.</span></span> <span data-ttu-id="2d567-214">Rysunek 9-4 przedstawia jedno podejście do organizowania testów według folderu w kilku projektach testowych.</span><span class="sxs-lookup"><span data-stu-id="2d567-214">Figure 9-4 shows one approach to organizing tests by folder within several test projects.</span></span>

![Organizowanie klas testowych według folderu na podstawie testowanej klasy](./media/image9-4.png)

<span data-ttu-id="2d567-216">**Rysunek 9-4.**</span><span class="sxs-lookup"><span data-stu-id="2d567-216">**Figure 9-4.**</span></span> <span data-ttu-id="2d567-217">Organizowanie klas testowych według folderu na podstawie testowanej klasy.</span><span class="sxs-lookup"><span data-stu-id="2d567-217">Organizing test classes by folder based on class being tested.</span></span>

<span data-ttu-id="2d567-218">Jeśli określona Klasa aplikacji ma wiele metod do przetestowania (i w ten sposób wiele klas testowych), warto umieścić te klasy w folderze odpowiadającym klasie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2d567-218">If a particular application class has many methods being tested (and thus many test classes), it may make sense to place these classes in a folder corresponding to the application class.</span></span> <span data-ttu-id="2d567-219">Ta organizacja nie różni się od sposobu, w jaki można organizować pliki w folderach w innym miejscu.</span><span class="sxs-lookup"><span data-stu-id="2d567-219">This organization is no different than how you might organize files into folders elsewhere.</span></span> <span data-ttu-id="2d567-220">Jeśli masz więcej niż trzy lub cztery powiązane pliki w folderze zawierającym wiele innych plików, często warto przenieść je do własnego podfolderu.</span><span class="sxs-lookup"><span data-stu-id="2d567-220">If you have more than three or four related files in a folder containing many other files, it's often helpful to move them into their own subfolder.</span></span>

## <a name="unit-testing-aspnet-core-apps"></a><span data-ttu-id="2d567-221">Testowanie jednostkowe ASP.NET Core aplikacji</span><span class="sxs-lookup"><span data-stu-id="2d567-221">Unit testing ASP.NET Core apps</span></span>

<span data-ttu-id="2d567-222">W dobrze zaprojektowanej aplikacji ASP.NET Core większość złożoności i logiki biznesowej będzie hermetyzowana w jednostkach firmy i w różnych usługach.</span><span class="sxs-lookup"><span data-stu-id="2d567-222">In a well-designed ASP.NET Core application, most of the complexity and business logic will be encapsulated in business entities and a variety of services.</span></span> <span data-ttu-id="2d567-223">Sama aplikacja MVC ASP.NET Core ze swoimi kontrolerami, filtrami, modele widoków i widokami powinna wymagać kilku testów jednostkowych.</span><span class="sxs-lookup"><span data-stu-id="2d567-223">The ASP.NET Core MVC app itself, with its controllers, filters, viewmodels, and views, should require few unit tests.</span></span> <span data-ttu-id="2d567-224">Większość funkcjonalności danej akcji leży poza samą metodą akcji.</span><span class="sxs-lookup"><span data-stu-id="2d567-224">Much of the functionality of a given action lies outside the action method itself.</span></span> <span data-ttu-id="2d567-225">Testowanie, czy kierowanie i globalna obsługa błędów działają poprawnie, nie można efektywnie wykonać test jednostkowy.</span><span class="sxs-lookup"><span data-stu-id="2d567-225">Testing whether routing or global error handling work correctly cannot be done effectively with a unit test.</span></span> <span data-ttu-id="2d567-226">Analogicznie, wszelkie filtry, w tym Walidacja modelu i filtry uwierzytelniania i autoryzacji, nie mogą być badane jednostkowo z testem docelowym metody akcji kontrolera.</span><span class="sxs-lookup"><span data-stu-id="2d567-226">Likewise, any filters, including model validation and authentication and authorization filters, cannot be unit tested with a test targeting a controller's action method.</span></span> <span data-ttu-id="2d567-227">Bez tych źródeł zachowania większość metod działania powinna być bardzo mała, co pozwala na ich przetestowanie do usług, które mogą być testowane niezależnie od kontrolera, który z nich korzysta.</span><span class="sxs-lookup"><span data-stu-id="2d567-227">Without these sources of behavior, most action methods should be trivially small, delegating the bulk of their work to services that can be tested independent of the controller that uses them.</span></span>

<span data-ttu-id="2d567-228">Czasami konieczne będzie Refaktoryzacja kodu w celu przetestowania go jednostkowo.</span><span class="sxs-lookup"><span data-stu-id="2d567-228">Sometimes you'll need to refactor your code in order to unit test it.</span></span> <span data-ttu-id="2d567-229">Często to działanie obejmuje identyfikowanie abstrakcji i użycie iniekcji zależności w celu uzyskania dostępu do abstrakcji w kodzie, który chcesz przetestować, zamiast kodowania bezpośrednio względem infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="2d567-229">Frequently this activity involves identifying abstractions and using dependency injection to access the abstraction in the code you'd like to test, rather than coding directly against infrastructure.</span></span> <span data-ttu-id="2d567-230">Rozważmy na przykład tę prostą metodę działania do wyświetlania obrazów:</span><span class="sxs-lookup"><span data-stu-id="2d567-230">For example, consider this easy action method for displaying images:</span></span>

```csharp
[HttpGet("[controller]/pic/{id}")]
public IActionResult GetImage(int id)
{
    var contentRoot = _env.ContentRootPath + "//Pics";
    var path = Path.Combine(contentRoot, id + ".png");
    Byte[] b = System.IO.File.ReadAllBytes(path);
    return File(b, "image/png");
}
```

<span data-ttu-id="2d567-231">Testy jednostkowe tej metody są utrudnione w zależności od tego `System.IO.File` , która z nich używa do odczytu z systemu plików.</span><span class="sxs-lookup"><span data-stu-id="2d567-231">Unit testing this method is made difficult by its direct dependency on `System.IO.File`, which it uses to read from the file system.</span></span> <span data-ttu-id="2d567-232">Możesz przetestować to zachowanie, aby upewnić się, że działa zgodnie z oczekiwaniami, ale jest to test integracji z rzeczywistymi plikami.</span><span class="sxs-lookup"><span data-stu-id="2d567-232">You can test this behavior to ensure it works as expected, but doing so with real files is an integration test.</span></span> <span data-ttu-id="2d567-233">Warto zauważyć, że nie można testować jednostkowo trasy tej metody, zobaczysz, &mdash; jak wkrótce wykonać te testy z testem funkcjonalnym.</span><span class="sxs-lookup"><span data-stu-id="2d567-233">It's worth noting you can't unit test this method's route&mdash;you'll see how to do this testing with a functional test shortly.</span></span>

<span data-ttu-id="2d567-234">Jeśli nie można bezpośrednio przetestować zachowania systemu plików i nie można przetestować trasy, co to jest?</span><span class="sxs-lookup"><span data-stu-id="2d567-234">If you can't unit test the file system behavior directly, and you can't test the route, what is there to test?</span></span> <span data-ttu-id="2d567-235">Ponadto po refaktoryzacji w celu przeprowadzenia testów jednostkowych można wykryć niektóre przypadki testowe i brakujące zachowanie, takie jak obsługa błędów.</span><span class="sxs-lookup"><span data-stu-id="2d567-235">Well, after refactoring to make unit testing possible, you may discover some test cases and missing behavior, such as error handling.</span></span> <span data-ttu-id="2d567-236">Co robią metoda po znalezieniu pliku?</span><span class="sxs-lookup"><span data-stu-id="2d567-236">What does the method do when a file isn't found?</span></span> <span data-ttu-id="2d567-237">Co należy zrobić?</span><span class="sxs-lookup"><span data-stu-id="2d567-237">What should it do?</span></span> <span data-ttu-id="2d567-238">W tym przykładzie metoda refaktoryzacji wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="2d567-238">In this example, the refactored method looks like this:</span></span>

```csharp
[HttpGet("[controller]/pic/{id}")]
public IActionResult GetImage(int id)
{
    byte[] imageBytes;
    try
    {
        imageBytes = _imageService.GetImageBytesById(id);
    }
    catch (CatalogImageMissingException ex)
    {
        _logger.LogWarning($"No image found for id: {id}");
        return NotFound();
    }
    return File(imageBytes, "image/png");
}
```

<span data-ttu-id="2d567-239">`_logger` i `_imageService` są zarówno wstrzykiwane jak i zależności.</span><span class="sxs-lookup"><span data-stu-id="2d567-239">`_logger` and `_imageService` are both injected as dependencies.</span></span> <span data-ttu-id="2d567-240">Teraz można testować, że ten sam identyfikator, który jest przesyłany do metody akcji, jest przenoszona do `_imageService` i że wynikowe bajty są zwracane jako część FileResult.</span><span class="sxs-lookup"><span data-stu-id="2d567-240">Now you can test that the same ID that is passed to the action method is passed to `_imageService`, and that the resulting bytes are returned as part of the FileResult.</span></span> <span data-ttu-id="2d567-241">Możesz również sprawdzić, czy rejestrowanie błędów odbywa się zgodnie z oczekiwaniami, a `NotFound` wynik jest zwracany, jeśli brakuje obrazu, przy założeniu, że to zachowanie jest ważnym zachowaniem aplikacji (czyli nie tylko kod tymczasowy dodany przez dewelopera w celu zdiagnozowania problemu).</span><span class="sxs-lookup"><span data-stu-id="2d567-241">You can also test that error logging is happening as expected, and that a `NotFound` result is returned if the image is missing, assuming this behavior is important application behavior (that is, not just temporary code the developer added to diagnose an issue).</span></span> <span data-ttu-id="2d567-242">Rzeczywista logika pliku została przeniesiona do oddzielnej usługi implementacji i została uzupełniona, aby zwracała wyjątek specyficzny dla aplikacji w przypadku brakujących plików.</span><span class="sxs-lookup"><span data-stu-id="2d567-242">The actual file logic has moved into a separate implementation service, and has been augmented to return an application-specific exception for the case of a missing file.</span></span> <span data-ttu-id="2d567-243">Tę implementację można przetestować niezależnie przy użyciu testu integracji.</span><span class="sxs-lookup"><span data-stu-id="2d567-243">You can test this implementation independently, using an integration test.</span></span>

<span data-ttu-id="2d567-244">W większości przypadków należy użyć globalnych programów obsługi wyjątków na kontrolerach, więc ilość logiki w nich powinna być minimalna i prawdopodobnie nie być testowana.</span><span class="sxs-lookup"><span data-stu-id="2d567-244">In most cases, you'll want to use global exception handlers in your controllers, so the amount of logic in them should be minimal and probably not worth unit testing.</span></span> <span data-ttu-id="2d567-245">Wykonaj większość testów akcji kontrolera przy użyciu testów funkcjonalnych i `TestServer` klasy opisanej poniżej.</span><span class="sxs-lookup"><span data-stu-id="2d567-245">Do most of your testing of controller actions using functional tests and the `TestServer` class described below.</span></span>

## <a name="integration-testing-aspnet-core-apps"></a><span data-ttu-id="2d567-246">Testowanie integracji ASP.NET Core aplikacje</span><span class="sxs-lookup"><span data-stu-id="2d567-246">Integration testing ASP.NET Core apps</span></span>

<span data-ttu-id="2d567-247">Większość testów integracji w aplikacjach ASP.NET Core należy przetestować usługi i inne typy implementacji zdefiniowane w projekcie infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="2d567-247">Most of the integration tests in your ASP.NET Core apps should be testing services and other implementation types defined in your Infrastructure project.</span></span> <span data-ttu-id="2d567-248">Można na przykład [sprawdzić, czy EF Core pomyślnie zaktualizować i pobrać dane, których oczekujesz](/ef/core/miscellaneous/testing/) od klas dostępu do danych znajdujących się w projekcie infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="2d567-248">For example, you could [test that EF Core was successfully updating and retrieving the data that you expect](/ef/core/miscellaneous/testing/) from your data access classes residing in the Infrastructure project.</span></span> <span data-ttu-id="2d567-249">Najlepszym sposobem, aby sprawdzić, czy projekt ASP.NET Core MVC działa prawidłowo, jest testami funkcjonalnymi uruchamianymi względem aplikacji działającej na hoście testowym.</span><span class="sxs-lookup"><span data-stu-id="2d567-249">The best way to test that your ASP.NET Core MVC project is behaving correctly is with functional tests that run against your app running in a test host.</span></span>

## <a name="functional-testing-aspnet-core-apps"></a><span data-ttu-id="2d567-250">Testowanie funkcjonalne ASP.NET Core aplikacji</span><span class="sxs-lookup"><span data-stu-id="2d567-250">Functional testing ASP.NET Core apps</span></span>

<span data-ttu-id="2d567-251">W przypadku aplikacji ASP.NET Core `TestServer` Klasa sprawia, że testy funkcjonalne są dość łatwe do zapisu.</span><span class="sxs-lookup"><span data-stu-id="2d567-251">For ASP.NET Core applications, the `TestServer` class makes functional tests fairly easy to write.</span></span> <span data-ttu-id="2d567-252">Można skonfigurować `TestServer` za pomocą `WebHostBuilder` (lub `HostBuilder` ) bezpośrednio (jak zwykle w przypadku aplikacji) lub z `WebApplicationFactory` typem (dostępnym od wersji 2,1).</span><span class="sxs-lookup"><span data-stu-id="2d567-252">You configure a `TestServer` using a `WebHostBuilder` (or `HostBuilder`) directly (as you normally do for your application), or with the `WebApplicationFactory` type (available since version 2.1).</span></span> <span data-ttu-id="2d567-253">Spróbuj dokładnie dopasować hosta testowego do hosta produkcyjnego, aby testy były wykonywane podobnie jak w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="2d567-253">Try to match your test host to your production host as closely as possible, so your tests exercise behavior similar to what the app will do in production.</span></span> <span data-ttu-id="2d567-254">`WebApplicationFactory`Klasa jest przydatna do konfigurowania ContentRoot TestServer, który jest używany przez ASP.NET Core do lokalizowania zasobów statycznych, takich jak widoki.</span><span class="sxs-lookup"><span data-stu-id="2d567-254">The `WebApplicationFactory` class is helpful for configuring the TestServer's ContentRoot, which is used by ASP.NET Core to locate static resource like Views.</span></span>

<span data-ttu-id="2d567-255">Można utworzyć proste testy funkcjonalne przez utworzenie klasy testowej implementującej `IClassFixture\<WebApplicationFactory\<TEntry>>` , gdzie `TEntry` jest klasą aplikacji sieci Web `Startup` .</span><span class="sxs-lookup"><span data-stu-id="2d567-255">You can create simple functional tests by creating a test class that implements `IClassFixture\<WebApplicationFactory\<TEntry>>`, where `TEntry` is your web application's `Startup` class.</span></span> <span data-ttu-id="2d567-256">W tym interfejsie, armatura testowa może utworzyć klienta przy użyciu `CreateClient` metody fabryki:</span><span class="sxs-lookup"><span data-stu-id="2d567-256">With this interface in place, your test fixture can create a client using the factory's `CreateClient` method:</span></span>

```csharp
public class BasicWebTests : IClassFixture<WebApplicationFactory<Startup>>
{
    protected readonly HttpClient _client;

    public BasicWebTests(WebApplicationFactory<Startup> factory)
    {
        _client = factory.CreateClient();
    }

    // write tests that use _client
}
```

<span data-ttu-id="2d567-257">Często podczas każdego przebiegu testowego należy wykonać dodatkową konfigurację lokacji, na przykład Konfigurując aplikację do używania magazynu danych w pamięci, a następnie wypełniania aplikacji danymi testowymi.</span><span class="sxs-lookup"><span data-stu-id="2d567-257">Frequently, you'll want to perform some additional configuration of your site before each test runs, such as configuring the application to use an in-memory data store and then seeding the application with test data.</span></span> <span data-ttu-id="2d567-258">Aby osiągnąć tę funkcję, Utwórz własną podklasę `WebApplicationFactory\<TEntry>` i Zastąp jej `ConfigureWebHost` metodę.</span><span class="sxs-lookup"><span data-stu-id="2d567-258">To achieve this functionality, create your own subclass of `WebApplicationFactory\<TEntry>` and override its `ConfigureWebHost` method.</span></span> <span data-ttu-id="2d567-259">Poniższy przykład pochodzi z projektu eShopOnWeb FunctionalTests i jest używany jako część testów w głównej aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="2d567-259">The example below is from the eShopOnWeb FunctionalTests project and is used as part of the tests on the main web application.</span></span>

```csharp
using Microsoft.AspNetCore.Hosting;
using Microsoft.AspNetCore.Identity;
using Microsoft.AspNetCore.Mvc.Testing;
using Microsoft.EntityFrameworkCore;
using Microsoft.eShopWeb.Infrastructure.Data;
using Microsoft.eShopWeb.Infrastructure.Identity;
using Microsoft.eShopWeb.Web;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Logging;
using System;

namespace Microsoft.eShopWeb.FunctionalTests.Web
{
    public class WebTestFixture : WebApplicationFactory<Startup>
    {
        protected override void ConfigureWebHost(IWebHostBuilder builder)
        {
            builder.UseEnvironment("Testing");

            builder.ConfigureServices(services =>
            {
                 services.AddEntityFrameworkInMemoryDatabase();

                // Create a new service provider.
                var provider = services
                    .AddEntityFrameworkInMemoryDatabase()
                    .BuildServiceProvider();

                // Add a database context (ApplicationDbContext) using an in-memory
                // database for testing.
                services.AddDbContext<CatalogContext>(options =>
                {
                    options.UseInMemoryDatabase("InMemoryDbForTesting");
                    options.UseInternalServiceProvider(provider);
                });

                services.AddDbContext<AppIdentityDbContext>(options =>
                {
                    options.UseInMemoryDatabase("Identity");
                    options.UseInternalServiceProvider(provider);
                });

                // Build the service provider.
                var sp = services.BuildServiceProvider();

                // Create a scope to obtain a reference to the database
                // context (ApplicationDbContext).
                using (var scope = sp.CreateScope())
                {
                    var scopedServices = scope.ServiceProvider;
                    var db = scopedServices.GetRequiredService<CatalogContext>();
                    var loggerFactory = scopedServices.GetRequiredService<ILoggerFactory>();

                    var logger = scopedServices
                        .GetRequiredService<ILogger<WebTestFixture>>();

                    // Ensure the database is created.
                    db.Database.EnsureCreated();

                    try
                    {
                        // Seed the database with test data.
                        CatalogContextSeed.SeedAsync(db, loggerFactory).Wait();

                        // seed sample user data
                        var userManager = scopedServices.GetRequiredService<UserManager<ApplicationUser>>();
                        var roleManager = scopedServices.GetRequiredService<RoleManager<IdentityRole>>();
                        AppIdentityDbContextSeed.SeedAsync(userManager, roleManager).Wait();
                    }
                    catch (Exception ex)
                    {
                        logger.LogError(ex, $"An error occurred seeding the " +
                            "database with test messages. Error: {ex.Message}");
                    }
                }
            });
        }
    }
}
```

<span data-ttu-id="2d567-260">Testy mogą korzystać z tego niestandardowego WebApplicationFactory przy użyciu go do tworzenia klienta, a następnie do wykonywania żądań do aplikacji przy użyciu tego wystąpienia klienta.</span><span class="sxs-lookup"><span data-stu-id="2d567-260">Tests can make use of this custom WebApplicationFactory by using it to create a client and then making requests to the application using this client instance.</span></span> <span data-ttu-id="2d567-261">Aplikacja będzie zawierać dane, które mogą być używane jako część zatwierdzeń testu.</span><span class="sxs-lookup"><span data-stu-id="2d567-261">The application will have data seeded that can be used as part of the test's assertions.</span></span> <span data-ttu-id="2d567-262">Poniższy test sprawdza, czy Strona główna aplikacji eShopOnWeb jest poprawnie załadowana i zawiera listę produktów, która została dodana do aplikacji w ramach danych inicjatora.</span><span class="sxs-lookup"><span data-stu-id="2d567-262">The following test verifies that the home page of the eShopOnWeb application loads correctly and includes a product listing that was added to the application as part of the seed data.</span></span>

```csharp
using Microsoft.eShopWeb.FunctionalTests.Web;
using System.Net.Http;
using System.Threading.Tasks;
using Xunit;

namespace Microsoft.eShopWeb.FunctionalTests.WebRazorPages
{
    [Collection("Sequential")]
    public class HomePageOnGet : IClassFixture<WebTestFixture>
    {
        public HomePageOnGet(WebTestFixture factory)
        {
            Client = factory.CreateClient();
        }

        public HttpClient Client { get; }

        [Fact]
        public async Task ReturnsHomePageWithProductListing()
        {
            // Arrange & Act
            var response = await Client.GetAsync("/");
            response.EnsureSuccessStatusCode();
            var stringResponse = await response.Content.ReadAsStringAsync();

            // Assert
            Assert.Contains(".NET Bot Black Sweatshirt", stringResponse);
        }
    }
}
```

<span data-ttu-id="2d567-263">Ten test funkcjonalny wykonuje pełny ASP.NET Core stos aplikacji MVC/Razor Pages, w tym wszystkie oprogramowanie pośredniczące, filtry i powiązania, które mogą być stosowane.</span><span class="sxs-lookup"><span data-stu-id="2d567-263">This functional test exercises the full ASP.NET Core MVC / Razor Pages application stack, including all middleware, filters, and binders that may be in place.</span></span> <span data-ttu-id="2d567-264">Sprawdza, czy dana trasa ("/") zwraca oczekiwany kod stanu sukcesu i dane wyjściowe HTML.</span><span class="sxs-lookup"><span data-stu-id="2d567-264">It verifies that a given route ("/") returns the expected success status code and HTML output.</span></span> <span data-ttu-id="2d567-265">Nie konfiguruje prawdziwy serwer sieci Web i pozwala uniknąć większości brittleness, które mogą korzystać z rzeczywistego serwera sieci Web do testowania (na przykład problemy z ustawieniami zapory).</span><span class="sxs-lookup"><span data-stu-id="2d567-265">It does so without setting up a real web server, and avoids much of the brittleness that using a real web server for testing can experience (for example, problems with firewall settings).</span></span> <span data-ttu-id="2d567-266">Testy funkcjonalne uruchamiane względem TestServer są zwykle wolniejsze niż testy integracji i jednostkowe, ale są znacznie szybsze niż testy, które byłyby wykonywane przez sieć, do testowego serwera sieci Web.</span><span class="sxs-lookup"><span data-stu-id="2d567-266">Functional tests that run against TestServer are usually slower than integration and unit tests, but are much faster than tests that would run over the network to a test web server.</span></span> <span data-ttu-id="2d567-267">Użyj testów funkcjonalnych, aby upewnić się, że stos frontonu aplikacji działa zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="2d567-267">Use functional tests to ensure your application's front-end stack is working as expected.</span></span> <span data-ttu-id="2d567-268">Te testy są szczególnie przydatne w przypadku znalezienia duplikatów na kontrolerach lub stronach i poprawnego duplikowania przez dodanie filtrów.</span><span class="sxs-lookup"><span data-stu-id="2d567-268">These tests are especially useful when you find duplication in your controllers or pages and you address the duplication by adding filters.</span></span> <span data-ttu-id="2d567-269">W idealnym przypadku ten Refaktoryzacja nie zmienia zachowania aplikacji, a zestaw testów funkcjonalnych sprawdzi, czy jest to przypadek.</span><span class="sxs-lookup"><span data-stu-id="2d567-269">Ideally, this refactoring won't change the behavior of the application, and a suite of functional tests will verify this is the case.</span></span>

> ### <a name="references--test-aspnet-core-mvc-apps"></a><span data-ttu-id="2d567-270">References — testowanie ASP.NET Core aplikacji MVC</span><span class="sxs-lookup"><span data-stu-id="2d567-270">References – Test ASP.NET Core MVC apps</span></span>
>
> - <span data-ttu-id="2d567-271">**Testowanie w ASP.NET Core** </span><span class="sxs-lookup"><span data-stu-id="2d567-271">**Testing in ASP.NET Core** </span></span>\
>   <https://docs.microsoft.com/aspnet/core/testing/>
> - <span data-ttu-id="2d567-272">**Konwencja nazewnictwa testów jednostkowych** </span><span class="sxs-lookup"><span data-stu-id="2d567-272">**Unit Test Naming Convention** </span></span>\
>   <https://ardalis.com/unit-test-naming-convention>
> - <span data-ttu-id="2d567-273">**Testowanie EF Core** </span><span class="sxs-lookup"><span data-stu-id="2d567-273">**Testing EF Core** </span></span>\
>   <https://docs.microsoft.com/ef/core/miscellaneous/testing/>
> - <span data-ttu-id="2d567-274">**Testy integracji w ASP.NET Core** </span><span class="sxs-lookup"><span data-stu-id="2d567-274">**Integration tests in ASP.NET Core** </span></span>\
>   <https://docs.microsoft.com/aspnet/core/test/integration-tests>

>[!div class="step-by-step"]
><span data-ttu-id="2d567-275">[Poprzedni](work-with-data-in-asp-net-core-apps.md) 
> [Dalej](development-process-for-azure.md)</span><span class="sxs-lookup"><span data-stu-id="2d567-275">[Previous](work-with-data-in-asp-net-core-apps.md)
[Next](development-process-for-azure.md)</span></span>
