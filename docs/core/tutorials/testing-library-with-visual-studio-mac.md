---
title: Testowanie biblioteki klas .NET przy użyciu Visual Studio dla komputerów Mac
description: Utwórz projekt testu jednostkowego dla biblioteki klas .NET. Sprawdź, czy biblioteka klas .NET działa prawidłowo z testami jednostkowymi.
ms.date: 11/18/2020
ms.openlocfilehash: 02d5aa74258ec15c5447b23246a3c7e9c61a6760
ms.sourcegitcommit: 9d525bb8109216ca1dc9e39c149d4902f4b43da5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2020
ms.locfileid: "96599529"
---
# <a name="test-a-net-class-library-using-visual-studio"></a><span data-ttu-id="64811-104">Testowanie biblioteki klas .NET przy użyciu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="64811-104">Test a .NET class library using Visual Studio</span></span>

<span data-ttu-id="64811-105">W tym samouczku pokazano, jak zautomatyzować testy jednostkowe przez dodanie projektu testowego do rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="64811-105">This tutorial shows how to automate unit testing by adding a test project to a solution.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64811-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="64811-106">Prerequisites</span></span>

- <span data-ttu-id="64811-107">Ten samouczek współdziała z rozwiązaniem tworzonym w temacie [Tworzenie biblioteki klas platformy .NET przy użyciu Visual Studio dla komputerów Mac](library-with-visual-studio-mac.md).</span><span class="sxs-lookup"><span data-stu-id="64811-107">This tutorial works with the solution that you create in [Create a .NET class library using Visual Studio for Mac](library-with-visual-studio-mac.md).</span></span>

## <a name="create-a-unit-test-project"></a><span data-ttu-id="64811-108">Tworzenie projektu testów jednostkowych</span><span class="sxs-lookup"><span data-stu-id="64811-108">Create a unit test project</span></span>

<span data-ttu-id="64811-109">Testy jednostkowe zapewniają zautomatyzowane testowanie oprogramowania podczas opracowywania i publikowania.</span><span class="sxs-lookup"><span data-stu-id="64811-109">Unit tests provide automated software testing during your development and publishing.</span></span> <span data-ttu-id="64811-110">[MSTest](https://github.com/Microsoft/testfx-docs) jest jednym z trzech platform testowych, spośród których można dokonać wyboru.</span><span class="sxs-lookup"><span data-stu-id="64811-110">[MSTest](https://github.com/Microsoft/testfx-docs) is one of three test frameworks you can choose from.</span></span> <span data-ttu-id="64811-111">Inne to [xUnit](https://xunit.net/) i [nunit](https://nunit.org/).</span><span class="sxs-lookup"><span data-stu-id="64811-111">The others are [xUnit](https://xunit.net/) and [nUnit](https://nunit.org/).</span></span>

1. <span data-ttu-id="64811-112">Rozpocznij Visual Studio dla komputerów Mac.</span><span class="sxs-lookup"><span data-stu-id="64811-112">Start Visual Studio for Mac.</span></span>

1. <span data-ttu-id="64811-113">Otwórz `ClassLibraryProjects` rozwiązanie utworzone w temacie [Tworzenie biblioteki klas .NET przy użyciu Visual Studio dla komputerów Mac](library-with-visual-studio-mac.md).</span><span class="sxs-lookup"><span data-stu-id="64811-113">Open the `ClassLibraryProjects` solution you created in [Create a .NET class library using Visual Studio for Mac](library-with-visual-studio-mac.md).</span></span>

1. <span data-ttu-id="64811-114">W konsoli **rozwiązania** <kbd>naciśnij klawisz Ctrl</kbd> `ClassLibraryProjects` i kliknij rozwiązanie, a następnie wybierz pozycję **Dodaj**  >  **Nowy projekt**.</span><span class="sxs-lookup"><span data-stu-id="64811-114">In the **Solution** pad, <kbd>ctrl</kbd>-click the `ClassLibraryProjects` solution and select **Add** > **New Project**.</span></span>

1. <span data-ttu-id="64811-115">W oknie dialogowym **Nowy projekt** wybierz pozycję **testy** z węzła **Sieć Web i konsola** .</span><span class="sxs-lookup"><span data-stu-id="64811-115">In the **New Project** dialog, select **Tests** from the **Web and Console** node.</span></span> <span data-ttu-id="64811-116">Wybierz **projekt MSTest** , a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="64811-116">Select the **MSTest Project** followed by **Next**.</span></span>

   :::image type="content" source="media/testing-library-with-visual-studio-mac/visual-studio-mac-unit-test-project.png" alt-text="Tworzenie projektu testowego w oknie dialogowym programu Visual Studio Mac New Project":::

1. <span data-ttu-id="64811-118">Wybierz **platformę .net 5,0** jako **platformę docelową** , a następnie wybierz pozycję **dalej**.</span><span class="sxs-lookup"><span data-stu-id="64811-118">Select **.NET 5.0** as the **Target Framework** and select **Next**.</span></span>

1. <span data-ttu-id="64811-119">Nadaj nowemu projektowi nazwę "StringLibraryTest" i wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="64811-119">Name the new project "StringLibraryTest" and select **Create**.</span></span>

   :::image type="content" source="media/testing-library-with-visual-studio-mac/visual-studio-mac-new-project-name.png" alt-text="Okno dialogowe nowego projektu programu Visual Studio dla komputerów Mac z nazwą projektu":::

   <span data-ttu-id="64811-121">Program Visual Studio tworzy plik klasy z następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="64811-121">Visual Studio creates a class file with the following code:</span></span>

   ```csharp
   using Microsoft.VisualStudio.TestTools.UnitTesting;

   namespace StringLibraryTest
   {
       [TestClass]
       public class UnitTest1
       {
           [TestMethod]
           public void TestMethod1()
           {
           }
       }
   }
   ```

   <span data-ttu-id="64811-122">Kod źródłowy utworzony przez szablon testu jednostkowego wykonuje następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="64811-122">The source code created by the unit test template does the following:</span></span>

   - <span data-ttu-id="64811-123">Importuje <xref:Microsoft.VisualStudio.TestTools.UnitTesting?displayProperty=nameWithType> przestrzeń nazw, która zawiera typy używane do testowania jednostkowego.</span><span class="sxs-lookup"><span data-stu-id="64811-123">It imports the <xref:Microsoft.VisualStudio.TestTools.UnitTesting?displayProperty=nameWithType> namespace, which contains the types used for unit testing.</span></span>
   - <span data-ttu-id="64811-124">Stosuje <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestClassAttribute> atrybut do `UnitTest1` klasy.</span><span class="sxs-lookup"><span data-stu-id="64811-124">It applies the <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestClassAttribute> attribute to the `UnitTest1` class.</span></span>
   - <span data-ttu-id="64811-125">Stosuje <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute> atrybut do `TestMethod1` .</span><span class="sxs-lookup"><span data-stu-id="64811-125">It applies the <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute> attribute to `TestMethod1`.</span></span>

   <span data-ttu-id="64811-126">Każda metoda oznaczona przy użyciu elementu [[TestMethod]](xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute) w klasie testowej oznaczona przy użyciu elementu [[TestClass]](xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestClassAttribute) jest wykonywana automatycznie, gdy test jednostkowy jest uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="64811-126">Each method tagged with [[TestMethod]](xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute) in a test class tagged with [[TestClass]](xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestClassAttribute) is executed automatically when the unit test is run.</span></span>

## <a name="add-a-project-reference"></a><span data-ttu-id="64811-127">Dodaj odwołanie do projektu</span><span class="sxs-lookup"><span data-stu-id="64811-127">Add a project reference</span></span>

<span data-ttu-id="64811-128">Aby projekt testowy mógł współpracował z `StringLibrary` klasą, Dodaj odwołanie do `StringLibrary` projektu.</span><span class="sxs-lookup"><span data-stu-id="64811-128">For the test project to work with the `StringLibrary` class, add a reference to the `StringLibrary` project.</span></span>

1. <span data-ttu-id="64811-129">W konsoli **rozwiązania** <kbd>kliknij pozycję</kbd> **zależności** w obszarze **StringLibraryTest**.</span><span class="sxs-lookup"><span data-stu-id="64811-129">In the **Solution** pad, <kbd>ctrl</kbd>-click **Dependencies** under **StringLibraryTest**.</span></span> <span data-ttu-id="64811-130">Wybierz pozycję **Dodaj odwołanie** z menu kontekstowego.</span><span class="sxs-lookup"><span data-stu-id="64811-130">Select **Add Reference** from the context menu.</span></span>

1. <span data-ttu-id="64811-131">W oknie dialogowym **odwołania** wybierz projekt **StringLibrary** .</span><span class="sxs-lookup"><span data-stu-id="64811-131">In the **References** dialog, select the **StringLibrary** project.</span></span> <span data-ttu-id="64811-132">Wybierz przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="64811-132">Select **OK**.</span></span>

      :::image type="content" source="media/testing-library-with-visual-studio-mac/visual-studio-mac-edit-references.png" alt-text="Okno dialogowe edycji odwołań dla programu Visual Studio Mac":::

## <a name="add-and-run-unit-test-methods"></a><span data-ttu-id="64811-134">Dodawanie i uruchamianie metod testów jednostkowych</span><span class="sxs-lookup"><span data-stu-id="64811-134">Add and run unit test methods</span></span>

<span data-ttu-id="64811-135">Gdy program Visual Studio uruchamia test jednostkowy, wykonuje każdą metodę, która jest oznaczona <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute> atrybutem w klasie, która jest oznaczona  <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestClassAttribute> atrybutem.</span><span class="sxs-lookup"><span data-stu-id="64811-135">When Visual Studio runs a unit test, it executes each method that is marked with the <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute> attribute in a class that is marked with the  <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestClassAttribute> attribute.</span></span> <span data-ttu-id="64811-136">Metoda testowa kończy się po znalezieniu pierwszego błędu lub gdy wszystkie testy zawarte w metodzie zakończyły się powodzeniem.</span><span class="sxs-lookup"><span data-stu-id="64811-136">A test method ends when the first failure is found or when all tests contained in the method have succeeded.</span></span>

<span data-ttu-id="64811-137">Najczęstsze testy wywołują elementy członkowskie <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert> klasy.</span><span class="sxs-lookup"><span data-stu-id="64811-137">The most common tests call members of the <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert> class.</span></span> <span data-ttu-id="64811-138">Wiele metod Assert obejmuje co najmniej dwa parametry, z których jeden jest oczekiwany wynik testu, a drugi jest rzeczywistym wynikiem testu.</span><span class="sxs-lookup"><span data-stu-id="64811-138">Many assert methods include at least two parameters, one of which is the expected test result and the other of which is the actual test result.</span></span> <span data-ttu-id="64811-139">`Assert`W poniższej tabeli przedstawiono niektóre z najczęściej wywoływanych metod:</span><span class="sxs-lookup"><span data-stu-id="64811-139">Some of the `Assert` class's most frequently called methods are shown in the following table:</span></span>

| <span data-ttu-id="64811-140">Metody Assert</span><span class="sxs-lookup"><span data-stu-id="64811-140">Assert methods</span></span>     | <span data-ttu-id="64811-141">Funkcja</span><span class="sxs-lookup"><span data-stu-id="64811-141">Function</span></span> |
| ------------------ | -------- |
| `Assert.AreEqual`  | <span data-ttu-id="64811-142">Sprawdza, czy dwie wartości lub obiekty są równe.</span><span class="sxs-lookup"><span data-stu-id="64811-142">Verifies that two values or objects are equal.</span></span> <span data-ttu-id="64811-143">Potwierdzenie kończy się niepowodzeniem, jeśli wartości lub obiekty nie są równe.</span><span class="sxs-lookup"><span data-stu-id="64811-143">The assert fails if the values or objects aren't equal.</span></span> |
| `Assert.AreSame`   | <span data-ttu-id="64811-144">Sprawdza, czy dwie zmienne obiektów odwołują się do tego samego obiektu.</span><span class="sxs-lookup"><span data-stu-id="64811-144">Verifies that two object variables refer to the same object.</span></span> <span data-ttu-id="64811-145">Potwierdzenie kończy się niepowodzeniem, jeśli zmienne odwołują się do różnych obiektów.</span><span class="sxs-lookup"><span data-stu-id="64811-145">The assert fails if the variables refer to different objects.</span></span> |
| `Assert.IsFalse`   | <span data-ttu-id="64811-146">Sprawdza, czy warunek to `false` .</span><span class="sxs-lookup"><span data-stu-id="64811-146">Verifies that a condition is `false`.</span></span> <span data-ttu-id="64811-147">Potwierdzenie kończy się niepowodzeniem, jeśli warunek ma wartość `true` .</span><span class="sxs-lookup"><span data-stu-id="64811-147">The assert fails if the condition is `true`.</span></span> |
| `Assert.IsNotNull` | <span data-ttu-id="64811-148">Sprawdza, czy obiekt nie jest `null` .</span><span class="sxs-lookup"><span data-stu-id="64811-148">Verifies that an object isn't `null`.</span></span> <span data-ttu-id="64811-149">Potwierdzenie kończy się niepowodzeniem, jeśli obiekt jest `null` .</span><span class="sxs-lookup"><span data-stu-id="64811-149">The assert fails if the object is `null`.</span></span> |

<span data-ttu-id="64811-150">Można również użyć <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.ThrowsException%2A?displayProperty=nameWithType> metody w metodzie testowej, aby wskazać typ wyjątku, który ma zostać zgłoszony.</span><span class="sxs-lookup"><span data-stu-id="64811-150">You can also use the <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.ThrowsException%2A?displayProperty=nameWithType> method in a test method to indicate the type of exception it's expected to throw.</span></span> <span data-ttu-id="64811-151">Test zakończy się niepowodzeniem, jeśli określony wyjątek nie zostanie zgłoszony.</span><span class="sxs-lookup"><span data-stu-id="64811-151">The test fails if the specified exception isn't thrown.</span></span>

<span data-ttu-id="64811-152">W testowaniu `StringLibrary.StartsWithUpper` metody, należy podać kilka ciągów zaczynających się od wielkiej litery.</span><span class="sxs-lookup"><span data-stu-id="64811-152">In testing the `StringLibrary.StartsWithUpper` method, you want to provide a number of strings that begin with an uppercase character.</span></span> <span data-ttu-id="64811-153">Oczekiwano, że metoda zwraca `true` w tych przypadkach, więc można wywołać <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.IsTrue%2A?displayProperty=nameWithType> metodę.</span><span class="sxs-lookup"><span data-stu-id="64811-153">You expect the method to return `true` in these cases, so you can call the <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.IsTrue%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="64811-154">Podobnie, chcesz podać kilka ciągów, które zaczynają się od znaku innego niż wielkie litery.</span><span class="sxs-lookup"><span data-stu-id="64811-154">Similarly, you want to provide a number of strings that begin with something other than an uppercase character.</span></span> <span data-ttu-id="64811-155">Oczekiwano, że metoda zwraca `false` w tych przypadkach, więc można wywołać <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.IsFalse%2A?displayProperty=nameWithType> metodę.</span><span class="sxs-lookup"><span data-stu-id="64811-155">You expect the method to return `false` in these cases, so you can call the <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.IsFalse%2A?displayProperty=nameWithType> method.</span></span>

<span data-ttu-id="64811-156">Ponieważ metoda biblioteki obsługuje ciągi, należy również upewnić się, że pomyślnie obsługuje [pusty ciąg ( `String.Empty` )](xref:System.String.Empty), prawidłowy ciąg, który nie zawiera znaków i <xref:System.String.Length> ma wartość 0, i `null` ciąg, który nie został zainicjowany.</span><span class="sxs-lookup"><span data-stu-id="64811-156">Since your library method handles strings, you also want to make sure that it successfully handles an [empty string (`String.Empty`)](xref:System.String.Empty), a valid string that has no characters and whose <xref:System.String.Length> is 0, and a `null` string that hasn't been initialized.</span></span> <span data-ttu-id="64811-157">Można wywołać `StartsWithUpper` bezpośrednio jako metodę statyczną i przekazać pojedynczy <xref:System.String> argument.</span><span class="sxs-lookup"><span data-stu-id="64811-157">You can call `StartsWithUpper` directly as a static method and pass a single <xref:System.String> argument.</span></span> <span data-ttu-id="64811-158">Lub można wywołać `StartsWithUpper` jako metodę rozszerzającą dla `string` zmiennej przypisanej do `null` .</span><span class="sxs-lookup"><span data-stu-id="64811-158">Or you can call `StartsWithUpper` as an extension method on a `string` variable assigned to `null`.</span></span>

<span data-ttu-id="64811-159">Zdefiniujesz trzy metody, z których każda wywołuje <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert> metodę dla każdego elementu w tablicy ciągów.</span><span class="sxs-lookup"><span data-stu-id="64811-159">You'll define three methods, each of which calls an <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert> method for each element in a string array.</span></span> <span data-ttu-id="64811-160">Wywołasz Przeciążenie metody, które pozwala określić komunikat o błędzie, który ma być wyświetlany w przypadku niepowodzenia testu.</span><span class="sxs-lookup"><span data-stu-id="64811-160">You'll call a method overload that lets you specify an error message to be displayed in case of test failure.</span></span> <span data-ttu-id="64811-161">Komunikat identyfikuje ciąg, który spowodował awarię.</span><span class="sxs-lookup"><span data-stu-id="64811-161">The message identifies the string that caused the failure.</span></span>

<span data-ttu-id="64811-162">Aby utworzyć metody testowe:</span><span class="sxs-lookup"><span data-stu-id="64811-162">To create the test methods:</span></span>

1. <span data-ttu-id="64811-163">Otwórz plik *UnitTest1.cs* i Zastąp kod następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="64811-163">Open the *UnitTest1.cs* file and replace the code with the following code:</span></span>

   :::code language="csharp" source="./snippets/library-with-visual-studio/csharp/StringLibraryTest/UnitTest1.cs":::

   <span data-ttu-id="64811-164">Test wielkich liter w `TestStartsWithUpper` metodzie zawiera alfabet grecki (u + 0391) oraz wielką literę pauzy (u + 041C).</span><span class="sxs-lookup"><span data-stu-id="64811-164">The test of uppercase characters in the `TestStartsWithUpper` method includes the Greek capital letter alpha (U+0391) and the Cyrillic capital letter EM (U+041C).</span></span> <span data-ttu-id="64811-165">Test małymi literami w `TestDoesNotStartWithUpper` metodzie obejmuje małą literę alfa (u + 03B1) i małą literę cyrylicy GHE (u + 0433).</span><span class="sxs-lookup"><span data-stu-id="64811-165">The test of lowercase characters in the `TestDoesNotStartWithUpper` method includes the Greek small letter alpha (U+03B1) and the Cyrillic small letter Ghe (U+0433).</span></span>

1. <span data-ttu-id="64811-166">Na pasku menu wybierz pozycję **plik**  >  **Zapisz jako**.</span><span class="sxs-lookup"><span data-stu-id="64811-166">On the menu bar, select **File** > **Save As**.</span></span> <span data-ttu-id="64811-167">W oknie dialogowym upewnij się, że **kodowanie** jest ustawione na **Unicode (UTF-8)**.</span><span class="sxs-lookup"><span data-stu-id="64811-167">In the dialog, make sure that **Encoding** is set to **Unicode (UTF-8)**.</span></span>

   :::image type="content" source="media/testing-library-with-visual-studio-mac/save-file-as-dialog.png" alt-text="Okno dialogowe zapisywania pliku w programie Visual Studio":::

1. <span data-ttu-id="64811-169">Gdy zostanie wyświetlony monit o zamienienie istniejącego pliku, wybierz opcję **Zastąp**.</span><span class="sxs-lookup"><span data-stu-id="64811-169">When you're asked if you want to replace the existing file, select **Replace**.</span></span>

   <span data-ttu-id="64811-170">Jeśli kod źródłowy nie zostanie zapisany jako plik zakodowany w formacie UTF8, program Visual Studio może go zapisać jako plik ASCII.</span><span class="sxs-lookup"><span data-stu-id="64811-170">If you fail to save your source code as a UTF8-encoded file, Visual Studio may save it as an ASCII file.</span></span> <span data-ttu-id="64811-171">Gdy tak się stanie, środowisko uruchomieniowe nie dekoduje znaków UTF8 poza zakresem ASCII, a wyniki testu nie będą poprawne.</span><span class="sxs-lookup"><span data-stu-id="64811-171">When that happens, the runtime doesn't accurately decode the UTF8 characters outside of the ASCII range, and the test results won't be correct.</span></span>

1. <span data-ttu-id="64811-172">Otwórz panel **testy jednostkowe** po prawej stronie ekranu.</span><span class="sxs-lookup"><span data-stu-id="64811-172">Open the **Unit Tests** panel on the right side of the screen.</span></span> <span data-ttu-id="64811-173">Wybierz pozycję **Wyświetl**  >  **testy** z menu.</span><span class="sxs-lookup"><span data-stu-id="64811-173">Select **View** > **Tests** from the menu.</span></span>

1. <span data-ttu-id="64811-174">Kliknij ikonę **dokowania** , aby pozostawić otwarty panel.</span><span class="sxs-lookup"><span data-stu-id="64811-174">Click the **Dock** icon to keep the panel open.</span></span>

   :::image type="content" source="media/testing-library-with-visual-studio-mac/visual-studio-mac-unit-test-dock-icon.png" alt-text="Ikona dokowania panelu testy jednostkowe Visual Studio dla komputerów Mac":::

1. <span data-ttu-id="64811-176">Kliknij przycisk **Uruchom wszystko** .</span><span class="sxs-lookup"><span data-stu-id="64811-176">Click the **Run All** button.</span></span>

   <span data-ttu-id="64811-177">Wszystkie testy zostały zakończone pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="64811-177">All tests pass.</span></span>

   :::image type="content" source="media/testing-library-with-visual-studio-mac/visual-studio-mac-unit-test-pass.png" alt-text="Visual Studio dla komputerów Mac oczekiwanych przebiegów testowych":::

## <a name="handle-test-failures"></a><span data-ttu-id="64811-179">Obsługa niepowodzeń testów</span><span class="sxs-lookup"><span data-stu-id="64811-179">Handle test failures</span></span>

<span data-ttu-id="64811-180">Jeśli wykonujesz programowanie sterowane testami (TDD), najpierw napiszesz testy i nie powiodą się po raz pierwszy.</span><span class="sxs-lookup"><span data-stu-id="64811-180">If you're doing test-driven development (TDD), you write tests first and they fail the first time you run them.</span></span> <span data-ttu-id="64811-181">Następnie dodasz kod do aplikacji, która pomyślnie testuje.</span><span class="sxs-lookup"><span data-stu-id="64811-181">Then you add code to the app that makes the test succeed.</span></span> <span data-ttu-id="64811-182">Na potrzeby tego samouczka utworzono test po zapisaniu kodu aplikacji, który jest weryfikowany, więc niepowodzenie testu nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="64811-182">For this tutorial, you created the test after writing the app code that it validates, so you haven't seen the test fail.</span></span> <span data-ttu-id="64811-183">Aby sprawdzić, czy test zakończy się niepowodzeniem, gdy spodziewasz się niepowodzeniem, Dodaj nieprawidłową wartość do danych wejściowych testu.</span><span class="sxs-lookup"><span data-stu-id="64811-183">To validate that a test fails when you expect it to fail, add an invalid value to the test input.</span></span>

1. <span data-ttu-id="64811-184">Zmodyfikuj `words` tablicę w `TestDoesNotStartWithUpper` metodzie, aby uwzględnić ciąg "Error".</span><span class="sxs-lookup"><span data-stu-id="64811-184">Modify the `words` array in the `TestDoesNotStartWithUpper` method to include the string "Error".</span></span> <span data-ttu-id="64811-185">Nie musisz zapisywać pliku, ponieważ program Visual Studio automatycznie zapisuje otwarte pliki w przypadku skompilowania rozwiązania do uruchamiania testów.</span><span class="sxs-lookup"><span data-stu-id="64811-185">You don't need to save the file because Visual Studio automatically saves open files when a solution is built to run tests.</span></span>

   ```csharp
   string[] words = { "alphabet", "Error", "zebra", "abc", "αυτοκινητοβιομηχανία", "государство",
                      "1234", ".", ";", " " };
   ```

1. <span data-ttu-id="64811-186">Uruchom testy ponownie.</span><span class="sxs-lookup"><span data-stu-id="64811-186">Run the tests again.</span></span>

   <span data-ttu-id="64811-187">Tym razem okno **Eksplorator testów** wskazuje, że dwa testy powiodło się i jeden z nich zakończył się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="64811-187">This time, the **Test Explorer** window indicates that two tests succeeded and one failed.</span></span>

   :::image type="content" source="media/testing-library-with-visual-studio-mac/failed-test-window.png" alt-text="Okno Eksploratora testów z niepowodzeniem testami":::

1. <span data-ttu-id="64811-189"><kbd>naciśnij klawisz Ctrl</kbd>i kliknij test zakończony niepowodzeniem, `TestDoesNotStartWithUpper` a następnie wybierz polecenie **Pokaż konsolę wyników** z menu kontekstowego.</span><span class="sxs-lookup"><span data-stu-id="64811-189"><kbd>ctrl</kbd>-click the failed test, `TestDoesNotStartWithUpper`, and select **Show Results Pad** from the context menu.</span></span>

   <span data-ttu-id="64811-190">W konsoli **wyników** zostanie wyświetlony komunikat utworzony przez potwierdzenie: "Assert. IsFalse nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="64811-190">The **Results** pad displays the message produced by the assert: "Assert.IsFalse failed.</span></span> <span data-ttu-id="64811-191">Oczekiwano dla elementu "Error": false; rzeczywista: true ".</span><span class="sxs-lookup"><span data-stu-id="64811-191">Expected for 'Error': false; actual: True".</span></span> <span data-ttu-id="64811-192">Z powodu błędu nie przetestowano ciągów w tablicy po "błędzie".</span><span class="sxs-lookup"><span data-stu-id="64811-192">Because of the failure, no strings in the array after "Error" were tested.</span></span>

   :::image type="content" source="media/testing-library-with-visual-studio-mac/visual-studio-mac-unit-test-failure.png" alt-text="Okno Eksploratora testów przedstawiające błąd potwierdzenia IsFalse":::

1. <span data-ttu-id="64811-194">Usuń ciąg "Error", który został dodany w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="64811-194">Remove the string "Error" that you added in step 1.</span></span> <span data-ttu-id="64811-195">Uruchom ponownie test i testy zakończone powodzeniem.</span><span class="sxs-lookup"><span data-stu-id="64811-195">Rerun the test and the tests pass.</span></span>

## <a name="test-the-release-version-of-the-library"></a><span data-ttu-id="64811-196">Testowanie wersji wydania biblioteki</span><span class="sxs-lookup"><span data-stu-id="64811-196">Test the Release version of the library</span></span>

<span data-ttu-id="64811-197">Teraz, gdy testy zostały zakończone przed uruchomieniem kompilacji biblioteki, należy uruchomić testy w dodatkowym czasie względem kompilacji wydania biblioteki.</span><span class="sxs-lookup"><span data-stu-id="64811-197">Now that the tests have all passed when running the Debug build of the library, run the tests an additional time against the Release build of the library.</span></span> <span data-ttu-id="64811-198">Wiele czynników, w tym Optymalizacja kompilatora, może czasami generować różne zachowanie między kompilacjami w wersji Debug i Release.</span><span class="sxs-lookup"><span data-stu-id="64811-198">A number of factors, including compiler optimizations, can sometimes produce different behavior between Debug and Release builds.</span></span>

<span data-ttu-id="64811-199">Aby przetestować kompilację wydania:</span><span class="sxs-lookup"><span data-stu-id="64811-199">To test the Release build:</span></span>

1. <span data-ttu-id="64811-200">Na pasku narzędzi programu Visual Studio Zmień konfigurację kompilacji z **Debuguj** do **Release**.</span><span class="sxs-lookup"><span data-stu-id="64811-200">In the Visual Studio toolbar, change the build configuration from **Debug** to **Release**.</span></span>

   :::image type="content" source="media/testing-library-with-visual-studio-mac/visual-studio-toolbar-release.png" alt-text="Pasek narzędzi programu Visual Studio z wyróżnioną kompilacją wydania":::

1. <span data-ttu-id="64811-202">W konsoli **rozwiązania** kliknij projekt **StringLibrary** i wybierz polecenie **Kompiluj** z menu kontekstowego <kbd>, aby</kbd>ponownie skompilować bibliotekę.</span><span class="sxs-lookup"><span data-stu-id="64811-202">In the **Solution** pad, <kbd>ctrl</kbd>-click the **StringLibrary** project and select **Build** from the context menu to recompile the library.</span></span>

   :::image type="content" source="media/testing-library-with-visual-studio-mac/build-library-context-menu.png" alt-text="Menu kontekstowe StringLibrary z poleceniem Build":::

1. <span data-ttu-id="64811-204">Uruchom ponownie testy jednostkowe.</span><span class="sxs-lookup"><span data-stu-id="64811-204">Run the unit tests again.</span></span>

   <span data-ttu-id="64811-205">Testy zostały zakończone pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="64811-205">The tests pass.</span></span>

## <a name="debug-tests"></a><span data-ttu-id="64811-206">Debuguj testy</span><span class="sxs-lookup"><span data-stu-id="64811-206">Debug tests</span></span>

<span data-ttu-id="64811-207">Jeśli używasz Visual Studio dla komputerów Mac jako środowiska IDE, możesz użyć tego samego procesu, który został przedstawiony w [samouczku: debugowanie aplikacji konsolowej .NET za pomocą Visual Studio dla komputerów Mac](debugging-with-visual-studio-mac.md) do debugowania kodu przy użyciu projektu testów jednostkowych.</span><span class="sxs-lookup"><span data-stu-id="64811-207">If you're using Visual Studio for Mac as your IDE, you can use the same process shown in [Tutorial: Debug a .NET console application using Visual Studio for Mac](debugging-with-visual-studio-mac.md) to debug code using your unit test project.</span></span> <span data-ttu-id="64811-208">Zamiast rozpoczynać projekt aplikacji *Pokaz* <kbd>, kliknij</kbd>projekt **StringLibraryTests** i wybierz pozycję **Rozpocznij debugowanie projektu** z menu kontekstowego.</span><span class="sxs-lookup"><span data-stu-id="64811-208">Instead of starting the *ShowCase* app project, <kbd>ctrl</kbd>-click the **StringLibraryTests** project, and select **Start Debugging Project** from the context menu.</span></span>

<span data-ttu-id="64811-209">Program Visual Studio uruchamia projekt testowy z dołączonym debugerem.</span><span class="sxs-lookup"><span data-stu-id="64811-209">Visual Studio starts the test project with the debugger attached.</span></span> <span data-ttu-id="64811-210">Wykonanie zostanie zatrzymane na dowolnym punkcie przerwania, który został dodany do projektu testowego lub kodu biblioteki źródłowej.</span><span class="sxs-lookup"><span data-stu-id="64811-210">Execution will stop at any breakpoint you've added to the test project or the underlying library code.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="64811-211">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="64811-211">Additional resources</span></span>

* [<span data-ttu-id="64811-212">Testy jednostkowe w programie .NET</span><span class="sxs-lookup"><span data-stu-id="64811-212">Unit testing in .NET</span></span>](../testing/index.md)

## <a name="next-steps"></a><span data-ttu-id="64811-213">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="64811-213">Next steps</span></span>

<span data-ttu-id="64811-214">W tym samouczku przetestowano bibliotekę klas.</span><span class="sxs-lookup"><span data-stu-id="64811-214">In this tutorial, you unit tested a class library.</span></span> <span data-ttu-id="64811-215">Bibliotekę można udostępniać innym osobom, publikując ją w pakiecie [NuGet](https://nuget.org) jako pakiet.</span><span class="sxs-lookup"><span data-stu-id="64811-215">You can make the library available to others by publishing it to [NuGet](https://nuget.org) as a package.</span></span> <span data-ttu-id="64811-216">Aby dowiedzieć się, jak, postępuj zgodnie z samouczkiem NuGet:</span><span class="sxs-lookup"><span data-stu-id="64811-216">To learn how, follow a NuGet tutorial:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="64811-217">Tworzenie i publikowanie pakietu (wiersz polecenia dotnet)</span><span class="sxs-lookup"><span data-stu-id="64811-217">Create and publish a package (dotnet CLI)</span></span>](/nuget/quickstart/create-and-publish-a-package-using-the-dotnet-cli)

<span data-ttu-id="64811-218">W przypadku opublikowania biblioteki jako pakietu NuGet inne osoby mogą ją zainstalować i używać.</span><span class="sxs-lookup"><span data-stu-id="64811-218">If you publish a library as a NuGet package, others can install and use it.</span></span> <span data-ttu-id="64811-219">Aby dowiedzieć się, jak, postępuj zgodnie z samouczkiem NuGet:</span><span class="sxs-lookup"><span data-stu-id="64811-219">To learn how, follow a NuGet tutorial:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="64811-220">Instalowanie i używanie pakietu w Visual Studio dla komputerów Mac</span><span class="sxs-lookup"><span data-stu-id="64811-220">Install and use a package in Visual Studio for Mac</span></span>](/nuget/quickstart/install-and-use-a-package-in-visual-studio-mac)

<span data-ttu-id="64811-221">Biblioteka nie musi być dystrybuowana jako pakiet.</span><span class="sxs-lookup"><span data-stu-id="64811-221">A library doesn't have to be distributed as a package.</span></span> <span data-ttu-id="64811-222">Można go powiązać z aplikacją konsolową, która go używa.</span><span class="sxs-lookup"><span data-stu-id="64811-222">It can be bundled with a console app that uses it.</span></span> <span data-ttu-id="64811-223">Aby dowiedzieć się, jak opublikować aplikację konsolową, zobacz wcześniejszy samouczek w tej serii:</span><span class="sxs-lookup"><span data-stu-id="64811-223">To learn how to publish a console app, see the earlier tutorial in this series:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="64811-224">Publikowanie aplikacji konsolowej .NET przy użyciu Visual Studio dla komputerów Mac</span><span class="sxs-lookup"><span data-stu-id="64811-224">Publish a .NET console application using Visual Studio for Mac</span></span>](publishing-with-visual-studio-mac.md)
