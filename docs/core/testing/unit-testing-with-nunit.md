---
title: Testowanie C# jednostkowe za pomocą nunit i .NET Core
description: Poznaj koncepcje testów jednostkowych w C# oprogramowaniu i .NET Core za pośrednictwem interaktywnego środowiska tworzenia przykładowego rozwiązania krok po kroku przy użyciu testu dotnet i NUnit.
author: rprouse
ms.date: 08/31/2018
ms.custom: seodec18
ms.openlocfilehash: 20f81981458b7e805a917202edce671ced69d89a
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/19/2019
ms.locfileid: "71117307"
---
# <a name="unit-testing-c-with-nunit-and-net-core"></a><span data-ttu-id="13afe-103">Testowanie C# jednostkowe za pomocą nunit i .NET Core</span><span class="sxs-lookup"><span data-stu-id="13afe-103">Unit testing C# with NUnit and .NET Core</span></span>

<span data-ttu-id="13afe-104">Ten samouczek przeprowadzi Cię przez interaktywny proces tworzenia przykładowego rozwiązania krok po kroku, aby poznać koncepcje dotyczące testowania jednostkowego.</span><span class="sxs-lookup"><span data-stu-id="13afe-104">This tutorial takes you through an interactive experience building a sample solution step-by-step to learn unit testing concepts.</span></span> <span data-ttu-id="13afe-105">Jeśli wolisz postępować zgodnie z samouczkiem przy użyciu wstępnie skompilowanego rozwiązania, przed rozpoczęciem [Wyświetl lub Pobierz przykładowy kod](https://github.com/dotnet/samples/blob/master/core/getting-started/unit-testing-using-nunit/) .</span><span class="sxs-lookup"><span data-stu-id="13afe-105">If you prefer to follow the tutorial using a pre-built solution, [view or download the sample code](https://github.com/dotnet/samples/blob/master/core/getting-started/unit-testing-using-nunit/) before you begin.</span></span> <span data-ttu-id="13afe-106">Aby uzyskać instrukcje dotyczące pobierania, zobacz [przykłady i samouczki](../../samples-and-tutorials/index.md#viewing-and-downloading-samples).</span><span class="sxs-lookup"><span data-stu-id="13afe-106">For download instructions, see [Samples and Tutorials](../../samples-and-tutorials/index.md#viewing-and-downloading-samples).</span></span>

[!INCLUDE [testing an ASP.NET Core project from .NET Core](../../../includes/core-testing-note-aspnet.md)]

## <a name="prerequisites"></a><span data-ttu-id="13afe-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="13afe-107">Prerequisites</span></span>

- <span data-ttu-id="13afe-108">[Zestaw .NET Core 2,1 SDK](https://dotnet.microsoft.com/download) lub jego nowsze wersje.</span><span class="sxs-lookup"><span data-stu-id="13afe-108">[.NET Core 2.1 SDK](https://dotnet.microsoft.com/download) or later versions.</span></span>
- <span data-ttu-id="13afe-109">Edytor tekstu lub Edytor kodu.</span><span class="sxs-lookup"><span data-stu-id="13afe-109">A text editor or code editor of your choice.</span></span>

## <a name="creating-the-source-project"></a><span data-ttu-id="13afe-110">Tworzenie projektu źródłowego</span><span class="sxs-lookup"><span data-stu-id="13afe-110">Creating the source project</span></span>

<span data-ttu-id="13afe-111">Otwórz okno powłoki.</span><span class="sxs-lookup"><span data-stu-id="13afe-111">Open a shell window.</span></span> <span data-ttu-id="13afe-112">Utwórz katalog o nazwie *Unit-Test-using-nunit* , aby pomieścić rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="13afe-112">Create a directory called *unit-testing-using-nunit* to hold the solution.</span></span> <span data-ttu-id="13afe-113">W tym nowym katalogu Uruchom następujące polecenie, aby utworzyć nowy plik rozwiązania dla biblioteki klas i projektu testowego:</span><span class="sxs-lookup"><span data-stu-id="13afe-113">Inside this new directory, run the following command to create a new solution file for the class library and the test project:</span></span>

```dotnetcli
dotnet new sln
```
 
<span data-ttu-id="13afe-114">Następnie Utwórz katalog *PrimeService* .</span><span class="sxs-lookup"><span data-stu-id="13afe-114">Next, create a *PrimeService* directory.</span></span> <span data-ttu-id="13afe-115">Poniższy konspekt przedstawia strukturę katalogu i pliku do tej pory:</span><span class="sxs-lookup"><span data-stu-id="13afe-115">The following outline shows the directory and file structure so far:</span></span>

```console
/unit-testing-using-nunit
    unit-testing-using-nunit.sln
    /PrimeService
```

<span data-ttu-id="13afe-116">Ustaw *PrimeService* w bieżącym katalogu i uruchom następujące polecenie, aby utworzyć projekt źródłowy:</span><span class="sxs-lookup"><span data-stu-id="13afe-116">Make *PrimeService* the current directory and run the following command to create the source project:</span></span>

```dotnetcli
dotnet new classlib
```

<span data-ttu-id="13afe-117">Zmień nazwę *Class1.cs* na *PrimeService.cs*.</span><span class="sxs-lookup"><span data-stu-id="13afe-117">Rename *Class1.cs* to *PrimeService.cs*.</span></span> <span data-ttu-id="13afe-118">Tworzysz nieprawidłową implementację `PrimeService` klasy:</span><span class="sxs-lookup"><span data-stu-id="13afe-118">You create a failing implementation of the `PrimeService` class:</span></span>

```csharp
using System;

namespace Prime.Services
{
    public class PrimeService
    {
        public bool IsPrime(int candidate)
        {
            throw new NotImplementedException("Please create a test first.");
        }
    }
}
```

<span data-ttu-id="13afe-119">Zmień katalog z powrotem do katalogu *testowego nunit* .</span><span class="sxs-lookup"><span data-stu-id="13afe-119">Change the directory back to the *unit-testing-using-nunit* directory.</span></span> <span data-ttu-id="13afe-120">Uruchom następujące polecenie, aby dodać projekt biblioteki klas do rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="13afe-120">Run the following command to add the class library project to the solution:</span></span>

```dotnetcli
dotnet sln add PrimeService/PrimeService.csproj
```

## <a name="creating-the-test-project"></a><span data-ttu-id="13afe-121">Tworzenie projektu testowego</span><span class="sxs-lookup"><span data-stu-id="13afe-121">Creating the test project</span></span>

<span data-ttu-id="13afe-122">Następnie Utwórz katalog *PrimeService. Tests* .</span><span class="sxs-lookup"><span data-stu-id="13afe-122">Next, create the *PrimeService.Tests* directory.</span></span> <span data-ttu-id="13afe-123">Poniższy konspekt przedstawia strukturę katalogów:</span><span class="sxs-lookup"><span data-stu-id="13afe-123">The following outline shows the directory structure:</span></span>

```console
/unit-testing-using-nunit
    unit-testing-using-nunit.sln
    /PrimeService
        Source Files
        PrimeService.csproj
    /PrimeService.Tests
```

<span data-ttu-id="13afe-124">Utwórz katalog *PrimeService. Tests* jako bieżący katalog i Utwórz nowy projekt za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="13afe-124">Make the *PrimeService.Tests* directory the current directory and create a new project using the following command:</span></span>

```dotnetcli
dotnet new nunit
```

<span data-ttu-id="13afe-125">Polecenie [dotnet New](../tools/dotnet-new.md) umożliwia utworzenie projektu testowego, który używa nunit jako biblioteki testowej.</span><span class="sxs-lookup"><span data-stu-id="13afe-125">The [dotnet new](../tools/dotnet-new.md) command creates a test project that uses NUnit as the test library.</span></span> <span data-ttu-id="13afe-126">Wygenerowany szablon służy do konfigurowania modułu uruchamiającego testy w pliku *PrimeService. tests. csproj* :</span><span class="sxs-lookup"><span data-stu-id="13afe-126">The generated template configures the test runner in the *PrimeService.Tests.csproj* file:</span></span>

[!code-xml[Packages](~/samples/core/getting-started/unit-testing-using-nunit/PrimeService.Tests/PrimeService.Tests.csproj#Packages)]

<span data-ttu-id="13afe-127">Projekt testowy wymaga innych pakietów do tworzenia i uruchamiania testów jednostkowych.</span><span class="sxs-lookup"><span data-stu-id="13afe-127">The test project requires other packages to create and run unit tests.</span></span> <span data-ttu-id="13afe-128">`dotnet new`w poprzednim kroku dodano zestaw Microsoft Test SDK, NUnit Test Framework oraz adapter testowy NUnit.</span><span class="sxs-lookup"><span data-stu-id="13afe-128">`dotnet new` in the previous step added the Microsoft test SDK, the NUnit test framework, and the NUnit test adapter.</span></span> <span data-ttu-id="13afe-129">Teraz Dodaj `PrimeService` bibliotekę klas jako inną zależność do projektu.</span><span class="sxs-lookup"><span data-stu-id="13afe-129">Now, add the `PrimeService` class library as another dependency to the project.</span></span> <span data-ttu-id="13afe-130">[`dotnet add reference`](../tools/dotnet-add-reference.md) Użyj polecenia:</span><span class="sxs-lookup"><span data-stu-id="13afe-130">Use the [`dotnet add reference`](../tools/dotnet-add-reference.md) command:</span></span>

```dotnetcli
dotnet add reference ../PrimeService/PrimeService.csproj
```

<span data-ttu-id="13afe-131">Cały plik można zobaczyć w [repozytorium Samples](https://github.com/dotnet/samples/blob/master/core/getting-started/unit-testing-using-nunit/PrimeService.Tests/PrimeService.Tests.csproj) w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="13afe-131">You can see the entire file in the [samples repository](https://github.com/dotnet/samples/blob/master/core/getting-started/unit-testing-using-nunit/PrimeService.Tests/PrimeService.Tests.csproj) on GitHub.</span></span>

<span data-ttu-id="13afe-132">W poniższym konspekcie przedstawiono końcowy układ rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="13afe-132">The following outline shows the final solution layout:</span></span>

```console
/unit-testing-using-nunit
    unit-testing-using-nunit.sln
    /PrimeService
        Source Files
        PrimeService.csproj
    /PrimeService.Tests
        Test Source Files
        PrimeService.Tests.csproj
```

<span data-ttu-id="13afe-133">Wykonaj następujące polecenie w katalogu *Unit-Test-using-nunit* :</span><span class="sxs-lookup"><span data-stu-id="13afe-133">Execute the following command in the *unit-testing-using-nunit* directory:</span></span>

```dotnetcli
dotnet sln add ./PrimeService.Tests/PrimeService.Tests.csproj
```

## <a name="creating-the-first-test"></a><span data-ttu-id="13afe-134">Tworzenie pierwszego testu</span><span class="sxs-lookup"><span data-stu-id="13afe-134">Creating the first test</span></span>

<span data-ttu-id="13afe-135">Napiszesz jeden test zakończony niepowodzeniem, upewnij się, a następnie powtórz ten proces.</span><span class="sxs-lookup"><span data-stu-id="13afe-135">You write one failing test, make it pass, then repeat the process.</span></span> <span data-ttu-id="13afe-136">W katalogu *PrimeService. Tests* Zmień nazwę pliku *UnitTest1.cs* na *PrimeService_IsPrimeShould. cs* i Zastąp całą zawartość następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="13afe-136">In the *PrimeService.Tests* directory, rename the *UnitTest1.cs* file to *PrimeService_IsPrimeShould.cs* and replace its entire contents with the following code:</span></span>

```csharp
using NUnit.Framework;
using Prime.Services;

namespace Prime.UnitTests.Services
{
    [TestFixture]
    public class PrimeService_IsPrimeShould
    {
        [Test]
        public void IsPrime_InputIs1_ReturnFalse()
        {
            PrimeService primeService = CreatePrimeService();
            var result = primeService.IsPrime(1);

            Assert.IsFalse(result, "1 should not be prime");
        }
        
        /*
        More tests
        */
        
        private PrimeService CreatePrimeService()
        {
             return new PrimeService();
        }
    }
}
```

<span data-ttu-id="13afe-137">Ten `[TestFixture]` atrybut oznacza klasę, która zawiera testy jednostkowe.</span><span class="sxs-lookup"><span data-stu-id="13afe-137">The `[TestFixture]` attribute denotes a class that contains unit tests.</span></span> <span data-ttu-id="13afe-138">`[Test]` Atrybut wskazuje, że metoda jest metodą testową.</span><span class="sxs-lookup"><span data-stu-id="13afe-138">The `[Test]` attribute indicates a method is a test method.</span></span>

<span data-ttu-id="13afe-139">Zapisz ten plik i wykonaj [`dotnet test`](../tools/dotnet-test.md) , aby skompilować testy i bibliotekę klas, a następnie uruchom testy.</span><span class="sxs-lookup"><span data-stu-id="13afe-139">Save this file and execute [`dotnet test`](../tools/dotnet-test.md) to build the tests and the class library and then run the tests.</span></span> <span data-ttu-id="13afe-140">Program NUnit Test Runner zawiera punkt wejścia programu do uruchamiania testów.</span><span class="sxs-lookup"><span data-stu-id="13afe-140">The NUnit test runner contains the program entry point to run your tests.</span></span> <span data-ttu-id="13afe-141">`dotnet test`uruchamia program Test Runner przy użyciu utworzonego projektu testu jednostkowego.</span><span class="sxs-lookup"><span data-stu-id="13afe-141">`dotnet test` starts the test runner using the unit test project you've created.</span></span>

<span data-ttu-id="13afe-142">Test zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="13afe-142">Your test fails.</span></span> <span data-ttu-id="13afe-143">Nie utworzono jeszcze implementacji.</span><span class="sxs-lookup"><span data-stu-id="13afe-143">You haven't created the implementation yet.</span></span> <span data-ttu-id="13afe-144">Wykonaj ten test, pisząc najprostszy kod w `PrimeService` klasie, która działa:</span><span class="sxs-lookup"><span data-stu-id="13afe-144">Make this test pass by writing the simplest code in the `PrimeService` class that works:</span></span>

```csharp
public bool IsPrime(int candidate)
{
    if (candidate == 1)
    {
        return false;
    }
    throw new NotImplementedException("Please create a test first.");
}
```

<span data-ttu-id="13afe-145">W katalogu *testy jednostkowe-using-nunit* Uruchom `dotnet test` ponownie.</span><span class="sxs-lookup"><span data-stu-id="13afe-145">In the *unit-testing-using-nunit* directory, run `dotnet test` again.</span></span> <span data-ttu-id="13afe-146">Polecenie uruchamia kompilację `PrimeService` dla `PrimeService.Tests` projektu, a następnie dla projektu. `dotnet test`</span><span class="sxs-lookup"><span data-stu-id="13afe-146">The `dotnet test` command runs a build for the `PrimeService` project and then for the `PrimeService.Tests` project.</span></span> <span data-ttu-id="13afe-147">Po skompilowaniu obu projektów jest uruchamiany ten pojedynczy test.</span><span class="sxs-lookup"><span data-stu-id="13afe-147">After building both projects, it runs this single test.</span></span> <span data-ttu-id="13afe-148">Przekazuje.</span><span class="sxs-lookup"><span data-stu-id="13afe-148">It passes.</span></span>

## <a name="adding-more-features"></a><span data-ttu-id="13afe-149">Dodawanie większej liczby funkcji</span><span class="sxs-lookup"><span data-stu-id="13afe-149">Adding more features</span></span>

<span data-ttu-id="13afe-150">Teraz, po wykonaniu jednego przebiegu testowego, należy napisać więcej.</span><span class="sxs-lookup"><span data-stu-id="13afe-150">Now that you've made one test pass, it's time to write more.</span></span> <span data-ttu-id="13afe-151">Istnieje kilka innych prostych przypadków dla numerów pierwszych: 0, -1.</span><span class="sxs-lookup"><span data-stu-id="13afe-151">There are a few other simple cases for prime numbers: 0, -1.</span></span> <span data-ttu-id="13afe-152">Można dodać nowe testy z `[Test]` atrybutem, ale szybko żmudnym.</span><span class="sxs-lookup"><span data-stu-id="13afe-152">You could add new tests with the `[Test]` attribute, but that quickly becomes tedious.</span></span> <span data-ttu-id="13afe-153">Istnieją inne atrybuty NUnit, które umożliwiają pisanie zestawu podobnych testów.</span><span class="sxs-lookup"><span data-stu-id="13afe-153">There are other NUnit attributes that enable you to write a suite of similar tests.</span></span>  <span data-ttu-id="13afe-154">`[TestCase]` Atrybut służy do tworzenia zestawu testów, które wykonują ten sam kod, ale mają różne argumenty wejściowe.</span><span class="sxs-lookup"><span data-stu-id="13afe-154">A `[TestCase]` attribute is used to create a suite of tests that execute the same code but have different input arguments.</span></span> <span data-ttu-id="13afe-155">Możesz użyć atrybutu, `[TestCase]` aby określić wartości dla tych danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="13afe-155">You can use the `[TestCase]` attribute to specify values for those inputs.</span></span>

<span data-ttu-id="13afe-156">Zamiast tworzyć nowe testy, Zastosuj ten atrybut, aby utworzyć pojedynczy test oparty na danych.</span><span class="sxs-lookup"><span data-stu-id="13afe-156">Instead of creating new tests, apply this attribute to create a single data driven test.</span></span> <span data-ttu-id="13afe-157">Test oparty na danych to metoda, która sprawdza kilka wartości mniejszej niż dwa, co jest najniższym numerem:</span><span class="sxs-lookup"><span data-stu-id="13afe-157">The data driven test is a method that tests several values less than two, which is the lowest prime number:</span></span>

[!code-csharp[Sample_TestCode](../../../samples/core/getting-started/unit-testing-using-nunit/PrimeService.Tests/PrimeService_IsPrimeShould.cs?name=Sample_TestCode)]

<span data-ttu-id="13afe-158">Uruchom `dotnet test`i dwa z tych testów zakończą się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="13afe-158">Run `dotnet test`, and two of these tests fail.</span></span> <span data-ttu-id="13afe-159">Aby wszystkie testy zostały zakończone pomyślnie, należy zmienić `if` klauzulę na początku `Main` metody w pliku *PrimeService.cs* :</span><span class="sxs-lookup"><span data-stu-id="13afe-159">To make all of the tests pass, change the `if` clause at the beginning of the `Main` method in the *PrimeService.cs* file:</span></span>

```csharp
if (candidate < 2)
```

<span data-ttu-id="13afe-160">Kontynuuj iteracje, dodając więcej testów, więcej teorie i więcej kodu w bibliotece głównej.</span><span class="sxs-lookup"><span data-stu-id="13afe-160">Continue to iterate by adding more tests, more theories, and more code in the main library.</span></span> <span data-ttu-id="13afe-161">Masz [ukończoną wersję testów](https://github.com/dotnet/samples/blob/master/core/getting-started/unit-testing-using-nunit/PrimeService.Tests/PrimeService_IsPrimeShould.cs) i [kompletną implementację biblioteki](https://github.com/dotnet/samples/blob/master/core/getting-started/unit-testing-using-nunit/PrimeService/PrimeService.cs).</span><span class="sxs-lookup"><span data-stu-id="13afe-161">You have the [finished version of the tests](https://github.com/dotnet/samples/blob/master/core/getting-started/unit-testing-using-nunit/PrimeService.Tests/PrimeService_IsPrimeShould.cs) and the [complete implementation of the library](https://github.com/dotnet/samples/blob/master/core/getting-started/unit-testing-using-nunit/PrimeService/PrimeService.cs).</span></span>

<span data-ttu-id="13afe-162">Utworzono niewielką bibliotekę i zestaw testów jednostkowych dla tej biblioteki.</span><span class="sxs-lookup"><span data-stu-id="13afe-162">You've built a small library and a set of unit tests for that library.</span></span> <span data-ttu-id="13afe-163">Rozbudowane rozwiązanie jest przeznaczone do dodawania nowych pakietów i testów jest częścią normalnego przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="13afe-163">You've structured the solution so that adding new packages and tests is part of the normal workflow.</span></span> <span data-ttu-id="13afe-164">Zbyt najwięcej czasu i wysiłku na rozwiązywanie celów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="13afe-164">You've concentrated most of your time and effort on solving the goals of the application.</span></span>
