---
title: 'Testowanie jednostkowe języka F # w programie .NET Core z testowaniem dotnet i xUnit'
description: 'Poznaj koncepcje testów jednostkowych dla języka F # w programie .NET Core za pośrednictwem interaktywnego środowiska tworzenia przykładowego rozwiązania krok po kroku przy użyciu testu dotnet i xUnit.'
author: billwagner
ms.author: wiwagn
ms.date: 08/30/2017
ms.openlocfilehash: e0f2b6f88a650f412148f51cc0236fa46ed8c618
ms.sourcegitcommit: c4a15c6c4ecbb8a46ad4e67d9b3ab9b8b031d849
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88656556"
---
# <a name="unit-testing-f-libraries-in-net-core-using-dotnet-test-and-xunit"></a><span data-ttu-id="8cb42-103">Testowanie jednostkowe bibliotek języka F # w programie .NET Core przy użyciu testu dotnet i xUnit</span><span class="sxs-lookup"><span data-stu-id="8cb42-103">Unit testing F# libraries in .NET Core using dotnet test and xUnit</span></span>

<span data-ttu-id="8cb42-104">Ten samouczek przeprowadzi Cię przez interaktywny proces tworzenia przykładowego rozwiązania krok po kroku, aby poznać koncepcje dotyczące testowania jednostkowego.</span><span class="sxs-lookup"><span data-stu-id="8cb42-104">This tutorial takes you through an interactive experience building a sample solution step-by-step to learn unit testing concepts.</span></span> <span data-ttu-id="8cb42-105">Jeśli wolisz postępować zgodnie z samouczkiem przy użyciu wstępnie skompilowanego rozwiązania, przed rozpoczęciem [Wyświetl lub Pobierz przykładowy kod](https://github.com/dotnet/samples/tree/master/core/getting-started/unit-testing-with-fsharp/) .</span><span class="sxs-lookup"><span data-stu-id="8cb42-105">If you prefer to follow the tutorial using a pre-built solution, [view or download the sample code](https://github.com/dotnet/samples/tree/master/core/getting-started/unit-testing-with-fsharp/) before you begin.</span></span> <span data-ttu-id="8cb42-106">Aby uzyskać instrukcje dotyczące pobierania, zobacz [przykłady i samouczki](../../samples-and-tutorials/index.md#view-and-download-samples).</span><span class="sxs-lookup"><span data-stu-id="8cb42-106">For download instructions, see [Samples and Tutorials](../../samples-and-tutorials/index.md#view-and-download-samples).</span></span>

[!INCLUDE [testing an ASP.NET Core project from .NET Core](../../../includes/core-testing-note-aspnet.md)]

## <a name="creating-the-source-project"></a><span data-ttu-id="8cb42-107">Tworzenie projektu źródłowego</span><span class="sxs-lookup"><span data-stu-id="8cb42-107">Creating the source project</span></span>

<span data-ttu-id="8cb42-108">Otwórz okno powłoki.</span><span class="sxs-lookup"><span data-stu-id="8cb42-108">Open a shell window.</span></span> <span data-ttu-id="8cb42-109">Utwórz katalog o nazwie *Unit-Test-with-FSharp* , aby pomieścić rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="8cb42-109">Create a directory called *unit-testing-with-fsharp* to hold the solution.</span></span>
<span data-ttu-id="8cb42-110">W tym nowym katalogu Uruchom polecenie, `dotnet new sln` Aby utworzyć nowe rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="8cb42-110">Inside this new directory, run `dotnet new sln` to create a new solution.</span></span> <span data-ttu-id="8cb42-111">Ułatwia to zarządzanie biblioteką klas i projektem testów jednostkowych.</span><span class="sxs-lookup"><span data-stu-id="8cb42-111">This makes it easier to manage both the class library and the unit test project.</span></span>
<span data-ttu-id="8cb42-112">W katalogu rozwiązania Utwórz katalog *mathservice* .</span><span class="sxs-lookup"><span data-stu-id="8cb42-112">Inside the solution directory, create a *MathService* directory.</span></span> <span data-ttu-id="8cb42-113">W tej chwili struktura katalogów i plików jest pokazana poniżej:</span><span class="sxs-lookup"><span data-stu-id="8cb42-113">The directory and file structure thus far is shown below:</span></span>

```
/unit-testing-with-fsharp
    unit-testing-with-fsharp.sln
    /MathService
```

<span data-ttu-id="8cb42-114">Ustaw *mathservice* jako bieżący katalog i uruchom polecenie, `dotnet new classlib -lang "F#"` Aby utworzyć projekt źródłowy.</span><span class="sxs-lookup"><span data-stu-id="8cb42-114">Make *MathService* the current directory, and run `dotnet new classlib -lang "F#"` to create the source project.</span></span> <span data-ttu-id="8cb42-115">Utworzysz nieprawidłową implementację usługi matematycznej:</span><span class="sxs-lookup"><span data-stu-id="8cb42-115">You'll create a failing implementation of the math service:</span></span>

```fsharp
module MyMath =
    let squaresOfOdds xs = raise (System.NotImplementedException("You haven't written a test yet!"))
```

<span data-ttu-id="8cb42-116">Zmień katalog z powrotem na katalog *test-z-FSharp* .</span><span class="sxs-lookup"><span data-stu-id="8cb42-116">Change the directory back to the *unit-testing-with-fsharp* directory.</span></span> <span data-ttu-id="8cb42-117">Uruchom `dotnet sln add .\MathService\MathService.fsproj` , aby dodać projekt biblioteki klas do rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="8cb42-117">Run `dotnet sln add .\MathService\MathService.fsproj` to add the class library project to the solution.</span></span>

## <a name="creating-the-test-project"></a><span data-ttu-id="8cb42-118">Tworzenie projektu testowego</span><span class="sxs-lookup"><span data-stu-id="8cb42-118">Creating the test project</span></span>

<span data-ttu-id="8cb42-119">Następnie Utwórz katalog *mathservice. Tests* .</span><span class="sxs-lookup"><span data-stu-id="8cb42-119">Next, create the *MathService.Tests* directory.</span></span> <span data-ttu-id="8cb42-120">Poniższy konspekt przedstawia strukturę katalogów:</span><span class="sxs-lookup"><span data-stu-id="8cb42-120">The following outline shows the directory structure:</span></span>

```
/unit-testing-with-fsharp
    unit-testing-with-fsharp.sln
    /MathService
        Source Files
        MathService.fsproj
    /MathService.Tests
```

<span data-ttu-id="8cb42-121">Utwórz katalog *mathservice. Tests* jako bieżący katalog i Utwórz nowy projekt za pomocą polecenia `dotnet new xunit -lang "F#"` .</span><span class="sxs-lookup"><span data-stu-id="8cb42-121">Make the *MathService.Tests* directory the current directory and create a new project using `dotnet new xunit -lang "F#"`.</span></span> <span data-ttu-id="8cb42-122">Spowoduje to utworzenie projektu testowego, który używa xUnit jako biblioteki testowej.</span><span class="sxs-lookup"><span data-stu-id="8cb42-122">This creates a test project that uses xUnit as the test library.</span></span> <span data-ttu-id="8cb42-123">Wygenerowany szablon służy do konfigurowania modułu uruchamiającego testy w *MathServiceTests. fsproj*:</span><span class="sxs-lookup"><span data-stu-id="8cb42-123">The generated template configures the test runner in the *MathServiceTests.fsproj*:</span></span>

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.NET.Test.Sdk" Version="15.3.0-preview-20170628-02" />
  <PackageReference Include="xunit" Version="2.2.0" />
  <PackageReference Include="xunit.runner.visualstudio" Version="2.2.0" />
</ItemGroup>
```

<span data-ttu-id="8cb42-124">Projekt testowy wymaga innych pakietów do tworzenia i uruchamiania testów jednostkowych.</span><span class="sxs-lookup"><span data-stu-id="8cb42-124">The test project requires other packages to create and run unit tests.</span></span> <span data-ttu-id="8cb42-125">`dotnet new` w poprzednim kroku dodano xUnit i moduł uruchamiający xUnit.</span><span class="sxs-lookup"><span data-stu-id="8cb42-125">`dotnet new` in the previous step added xUnit and the xUnit runner.</span></span> <span data-ttu-id="8cb42-126">Teraz Dodaj `MathService` bibliotekę klas jako inną zależność do projektu.</span><span class="sxs-lookup"><span data-stu-id="8cb42-126">Now, add the `MathService` class library as another dependency to the project.</span></span> <span data-ttu-id="8cb42-127">Użyj `dotnet add reference` polecenia:</span><span class="sxs-lookup"><span data-stu-id="8cb42-127">Use the `dotnet add reference` command:</span></span>

```dotnetcli
dotnet add reference ../MathService/MathService.fsproj
```

<span data-ttu-id="8cb42-128">Cały plik można zobaczyć w [repozytorium Samples](https://github.com/dotnet/samples/blob/master/core/getting-started/unit-testing-with-fsharp/MathService.Tests/MathService.Tests.fsproj) w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="8cb42-128">You can see the entire file in the [samples repository](https://github.com/dotnet/samples/blob/master/core/getting-started/unit-testing-with-fsharp/MathService.Tests/MathService.Tests.fsproj) on GitHub.</span></span>

<span data-ttu-id="8cb42-129">Dysponujesz następującym końcowym układem rozwiązań:</span><span class="sxs-lookup"><span data-stu-id="8cb42-129">You have the following final solution layout:</span></span>

```
/unit-testing-with-fsharp
    unit-testing-with-fsharp.sln
    /MathService
        Source Files
        MathService.fsproj
    /MathService.Tests
        Test Source Files
        MathServiceTests.fsproj
```

<span data-ttu-id="8cb42-130">Wykonaj `dotnet sln add .\MathService.Tests\MathService.Tests.fsproj` w katalogu *test-z-FSharp* .</span><span class="sxs-lookup"><span data-stu-id="8cb42-130">Execute `dotnet sln add .\MathService.Tests\MathService.Tests.fsproj` in the *unit-testing-with-fsharp* directory.</span></span>

## <a name="creating-the-first-test"></a><span data-ttu-id="8cb42-131">Tworzenie pierwszego testu</span><span class="sxs-lookup"><span data-stu-id="8cb42-131">Creating the first test</span></span>

<span data-ttu-id="8cb42-132">Napiszesz jeden test zakończony niepowodzeniem, upewnij się, a następnie powtórz ten proces.</span><span class="sxs-lookup"><span data-stu-id="8cb42-132">You write one failing test, make it pass, then repeat the process.</span></span> <span data-ttu-id="8cb42-133">Otwórz aplet *testy. FS* i Dodaj następujący kod:</span><span class="sxs-lookup"><span data-stu-id="8cb42-133">Open *Tests.fs* and add the following code:</span></span>

```fsharp
[<Fact>]
let ``My test`` () =
    Assert.True(true)

[<Fact>]
let ``Fail every time`` () = Assert.True(false)
```

<span data-ttu-id="8cb42-134">Ten `[<Fact>]` atrybut oznacza metodę testową, która jest uruchamiana przez program Test Runner.</span><span class="sxs-lookup"><span data-stu-id="8cb42-134">The `[<Fact>]` attribute denotes a test method that is run by the test runner.</span></span> <span data-ttu-id="8cb42-135">Z *jednostki-test-with-FSharp*należy wykonać, `dotnet test` Aby skompilować testy i bibliotekę klas, a następnie uruchomić testy.</span><span class="sxs-lookup"><span data-stu-id="8cb42-135">From the *unit-testing-with-fsharp*, execute `dotnet test` to build the tests and the class library and then run the tests.</span></span> <span data-ttu-id="8cb42-136">Program xUnit Test Runner zawiera punkt wejścia programu do uruchamiania testów.</span><span class="sxs-lookup"><span data-stu-id="8cb42-136">The xUnit test runner contains the program entry point to run your tests.</span></span> <span data-ttu-id="8cb42-137">`dotnet test` uruchamia program Test Runner przy użyciu utworzonego projektu testu jednostkowego.</span><span class="sxs-lookup"><span data-stu-id="8cb42-137">`dotnet test` starts the test runner using the unit test project you've created.</span></span>

<span data-ttu-id="8cb42-138">Te dwa testy pokazują najbardziej podstawowe testy dotyczące przekazywania i niepowodzenia.</span><span class="sxs-lookup"><span data-stu-id="8cb42-138">These two tests show the most basic passing and failing tests.</span></span> <span data-ttu-id="8cb42-139">`My test``Fail every time`kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="8cb42-139">`My test` passes, and `Fail every time` fails.</span></span> <span data-ttu-id="8cb42-140">Teraz Utwórz test dla `squaresOfOdds` metody.</span><span class="sxs-lookup"><span data-stu-id="8cb42-140">Now, create a test for the `squaresOfOdds` method.</span></span> <span data-ttu-id="8cb42-141">`squaresOfOdds`Metoda zwraca sekwencję kwadratów wszystkich nieparzystych wartości całkowitych, które są częścią sekwencji wejściowej.</span><span class="sxs-lookup"><span data-stu-id="8cb42-141">The `squaresOfOdds` method returns a sequence of the squares of all odd integer values that are part of the input sequence.</span></span> <span data-ttu-id="8cb42-142">Zamiast próbować zapisywać wszystkie te funkcje jednocześnie, można iteracyjnie utworzyć testy, które weryfikują funkcjonalność.</span><span class="sxs-lookup"><span data-stu-id="8cb42-142">Rather than trying to write all of those functions at once, you can iteratively create tests that validate the functionality.</span></span> <span data-ttu-id="8cb42-143">Każdy przebieg testowy oznacza tworzenie niezbędnych funkcji dla metody.</span><span class="sxs-lookup"><span data-stu-id="8cb42-143">Making each test pass means creating the necessary functionality for the method.</span></span>

<span data-ttu-id="8cb42-144">Najprostszym testem możemy napisać jest wywołanie `squaresOfOdds` ze wszystkimi parzystymi liczbami, gdzie wynik powinien być pustą sekwencją liczb całkowitych.</span><span class="sxs-lookup"><span data-stu-id="8cb42-144">The simplest test we can write is to call `squaresOfOdds` with all even numbers, where the result should be an empty sequence of integers.</span></span>  <span data-ttu-id="8cb42-145">Oto test:</span><span class="sxs-lookup"><span data-stu-id="8cb42-145">Here's that test:</span></span>

```fsharp
[<Fact>]
let ``Sequence of Evens returns empty collection`` () =
    let expected = Seq.empty<int>
    let actual = MyMath.squaresOfOdds [2; 4; 6; 8; 10]
    Assert.Equal<Collections.Generic.IEnumerable<int>>(expected, actual)
```

<span data-ttu-id="8cb42-146">Test zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="8cb42-146">Your test fails.</span></span> <span data-ttu-id="8cb42-147">Nie utworzono jeszcze implementacji.</span><span class="sxs-lookup"><span data-stu-id="8cb42-147">You haven't created the implementation yet.</span></span> <span data-ttu-id="8cb42-148">Wykonaj ten test, pisząc najprostszy kod w `MathService` klasie, która działa:</span><span class="sxs-lookup"><span data-stu-id="8cb42-148">Make this test pass by writing the simplest code in the `MathService` class that works:</span></span>

```fsharp
let squaresOfOdds xs =
    Seq.empty<int>
```

<span data-ttu-id="8cb42-149">W katalogu *testy jednostkowe-with-FSharp* Uruchom `dotnet test` ponownie.</span><span class="sxs-lookup"><span data-stu-id="8cb42-149">In the *unit-testing-with-fsharp* directory, run `dotnet test` again.</span></span> <span data-ttu-id="8cb42-150">`dotnet test`Polecenie uruchamia kompilację dla `MathService` projektu, a następnie dla `MathService.Tests` projektu.</span><span class="sxs-lookup"><span data-stu-id="8cb42-150">The `dotnet test` command runs a build for the `MathService` project and then for the `MathService.Tests` project.</span></span> <span data-ttu-id="8cb42-151">Po skompilowaniu obu projektów jest uruchamiany ten pojedynczy test.</span><span class="sxs-lookup"><span data-stu-id="8cb42-151">After building both projects, it runs this single test.</span></span> <span data-ttu-id="8cb42-152">Przekazuje.</span><span class="sxs-lookup"><span data-stu-id="8cb42-152">It passes.</span></span>

## <a name="completing-the-requirements"></a><span data-ttu-id="8cb42-153">Spełnienie wymagań</span><span class="sxs-lookup"><span data-stu-id="8cb42-153">Completing the requirements</span></span>

<span data-ttu-id="8cb42-154">Teraz, po wykonaniu jednego przebiegu testowego, należy napisać więcej.</span><span class="sxs-lookup"><span data-stu-id="8cb42-154">Now that you've made one test pass, it's time to write more.</span></span> <span data-ttu-id="8cb42-155">Następny prosty przypadek działa z sekwencją, której jedyną liczbą nieparzystą jest `1` .</span><span class="sxs-lookup"><span data-stu-id="8cb42-155">The next simple case works with a sequence whose only odd number is `1`.</span></span> <span data-ttu-id="8cb42-156">Numer 1 jest łatwiejszy, ponieważ kwadrat 1 ma wartość 1.</span><span class="sxs-lookup"><span data-stu-id="8cb42-156">The number 1 is easier because the square of 1 is 1.</span></span> <span data-ttu-id="8cb42-157">Oto następny test:</span><span class="sxs-lookup"><span data-stu-id="8cb42-157">Here's that next test:</span></span>

```fsharp
[<Fact>]
let ``Sequences of Ones and Evens returns Ones`` () =
    let expected = [1; 1; 1; 1]
    let actual = MyMath.squaresOfOdds [2; 1; 4; 1; 6; 1; 8; 1; 10]
    Assert.Equal<Collections.Generic.IEnumerable<int>>(expected, actual)
```

<span data-ttu-id="8cb42-158">Wykonanie `dotnet test` uruchamia testy i pokazuje, że nowy test zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="8cb42-158">Executing `dotnet test` runs your tests and shows you that the new test fails.</span></span> <span data-ttu-id="8cb42-159">Teraz zaktualizuj metodę, `squaresOfOdds` Aby obsłużyć ten nowy test.</span><span class="sxs-lookup"><span data-stu-id="8cb42-159">Now, update the `squaresOfOdds` method to handle this new test.</span></span> <span data-ttu-id="8cb42-160">Wszystkie liczby parzyste z sekwencji są filtrowane, aby wykonać ten test.</span><span class="sxs-lookup"><span data-stu-id="8cb42-160">You filter all the even numbers out of the sequence to make this test pass.</span></span> <span data-ttu-id="8cb42-161">Możesz to zrobić, pisząc małą funkcję filtrowania i używając `Seq.filter` :</span><span class="sxs-lookup"><span data-stu-id="8cb42-161">You can do that by writing a small filter function and using `Seq.filter`:</span></span>

```fsharp
let private isOdd x = x % 2 <> 0

let squaresOfOdds xs =
    xs
    |> Seq.filter isOdd
```

<span data-ttu-id="8cb42-162">Istnieje jeden krok do przechodzenia: kwadrat każdej z liczb nieparzystych.</span><span class="sxs-lookup"><span data-stu-id="8cb42-162">There's one more step to go: square each of the odd numbers.</span></span> <span data-ttu-id="8cb42-163">Zacznij od zapisania nowego testu:</span><span class="sxs-lookup"><span data-stu-id="8cb42-163">Start by writing a new test:</span></span>

```fsharp
[<Fact>]
let ``SquaresOfOdds works`` () =
    let expected = [1; 9; 25; 49; 81]
    let actual = MyMath.squaresOfOdds [1; 2; 3; 4; 5; 6; 7; 8; 9; 10]
    Assert.Equal(expected, actual)
```

<span data-ttu-id="8cb42-164">Możesz naprawić test, przechodząc sekwencję przefiltrowanych przez operację mapowania, aby obliczyć kwadrat dla każdej liczby nieparzystej:</span><span class="sxs-lookup"><span data-stu-id="8cb42-164">You can fix the test by piping the filtered sequence through a map operation to compute the square of each odd number:</span></span>

```fsharp
let private square x = x * x
let private isOdd x = x % 2 <> 0

let squaresOfOdds xs =
    xs
    |> Seq.filter isOdd
    |> Seq.map square
```

<span data-ttu-id="8cb42-165">Utworzono niewielką bibliotekę i zestaw testów jednostkowych dla tej biblioteki.</span><span class="sxs-lookup"><span data-stu-id="8cb42-165">You've built a small library and a set of unit tests for that library.</span></span> <span data-ttu-id="8cb42-166">Rozbudowane rozwiązanie jest przeznaczone do dodawania nowych pakietów i testów jest częścią normalnego przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="8cb42-166">You've structured the solution so that adding new packages and tests is part of the normal workflow.</span></span> <span data-ttu-id="8cb42-167">Zbyt najwięcej czasu i wysiłku na rozwiązywanie celów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8cb42-167">You've concentrated most of your time and effort on solving the goals of the application.</span></span>

## <a name="see-also"></a><span data-ttu-id="8cb42-168">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="8cb42-168">See also</span></span>

- [<span data-ttu-id="8cb42-169">dotnet new</span><span class="sxs-lookup"><span data-stu-id="8cb42-169">dotnet new</span></span>](../tools/dotnet-new.md)
- [<span data-ttu-id="8cb42-170">dotnet sln</span><span class="sxs-lookup"><span data-stu-id="8cb42-170">dotnet sln</span></span>](../tools/dotnet-new.md)
- [<span data-ttu-id="8cb42-171">dotnet add reference</span><span class="sxs-lookup"><span data-stu-id="8cb42-171">dotnet add reference</span></span>](../tools/dotnet-add-reference.md)
- [<span data-ttu-id="8cb42-172">dotnet test</span><span class="sxs-lookup"><span data-stu-id="8cb42-172">dotnet test</span></span>](../tools/dotnet-test.md)
