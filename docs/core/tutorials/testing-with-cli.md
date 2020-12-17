---
title: Organizowanie i testowanie projektów przy użyciu interfejsu wiersza polecenia platformy .NET
description: W tym samouczku wyjaśniono, jak organizować i testować projekty .NET z wiersza polecenia.
author: cartermp
ms.date: 09/10/2018
ms.openlocfilehash: 263eaf15beac008de8bb353a385b8f3588a7fefc
ms.sourcegitcommit: 635a0ff775d2447a81ef7233a599b8f88b162e5d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/17/2020
ms.locfileid: "97633640"
---
# <a name="organizing-and-testing-projects-with-the-net-cli"></a><span data-ttu-id="c495a-103">Organizowanie i testowanie projektów przy użyciu interfejsu wiersza polecenia platformy .NET</span><span class="sxs-lookup"><span data-stu-id="c495a-103">Organizing and testing projects with the .NET CLI</span></span>

<span data-ttu-id="c495a-104">Ten samouczek znajduje [się w samouczku: Tworzenie aplikacji konsolowej za pomocą platformy .NET przy użyciu Visual Studio Code, dzięki](with-visual-studio-code.md)czemu nie utworzysz prostej aplikacji konsolowej do tworzenia zaawansowanych i dobrze zorganizowanych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c495a-104">This tutorial follows [Tutorial: Create a console application with .NET using Visual Studio Code](with-visual-studio-code.md), taking you beyond the creation of a simple console app to develop advanced and well-organized applications.</span></span> <span data-ttu-id="c495a-105">Po podaniu, jak używać folderów do organizowania kodu, w tym samouczku pokazano, jak zwiększyć aplikację konsolową za pomocą platformy testowania [xUnit](https://xunit.net/) .</span><span class="sxs-lookup"><span data-stu-id="c495a-105">After showing you how to use folders to organize your code, this tutorial shows you how to extend a console application with the [xUnit](https://xunit.net/) testing framework.</span></span>

## <a name="using-folders-to-organize-code"></a><span data-ttu-id="c495a-106">Organizowanie kodu przy użyciu folderów</span><span class="sxs-lookup"><span data-stu-id="c495a-106">Using folders to organize code</span></span>

<span data-ttu-id="c495a-107">Jeśli chcesz wprowadzić nowe typy do aplikacji konsoli, możesz to zrobić przez dodanie plików zawierających typy do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c495a-107">If you want to introduce new types into a console app, you can do so by adding files containing the types to the app.</span></span> <span data-ttu-id="c495a-108">Na przykład w przypadku dodawania plików zawierających `AccountInformation` i `MonthlyReportRecords` typów do projektu Struktura pliku projektu jest płaska i łatwa do przechodzenia:</span><span class="sxs-lookup"><span data-stu-id="c495a-108">For example if you add files containing `AccountInformation` and `MonthlyReportRecords` types to your project, the project file structure is flat and easy to navigate:</span></span>

```
/MyProject
|__AccountInformation.cs
|__MonthlyReportRecords.cs
|__MyProject.csproj
|__Program.cs
```

<span data-ttu-id="c495a-109">Jednak jest to dobre rozwiązanie tylko wtedy, gdy rozmiar projektu jest stosunkowo mały.</span><span class="sxs-lookup"><span data-stu-id="c495a-109">However, this only works well when the size of your project is relatively small.</span></span> <span data-ttu-id="c495a-110">Czy można przystąpić do tego, co się stanie, jeśli dodasz 20 typów do projektu?</span><span class="sxs-lookup"><span data-stu-id="c495a-110">Can you imagine what will happen if you add 20 types to the project?</span></span> <span data-ttu-id="c495a-111">Projekt w nieskończoność nie może być w łatwy sposób przechodzenia i konserwowania w wielu plikach, w których znajduje się katalog główny projektu.</span><span class="sxs-lookup"><span data-stu-id="c495a-111">The project definitely wouldn't be easy to navigate and maintain with that many files littering the project's root directory.</span></span>

<span data-ttu-id="c495a-112">Aby zorganizować projekt, Utwórz nowy folder i nadaj mu nazwę *modele* , aby przechowywać pliki typu.</span><span class="sxs-lookup"><span data-stu-id="c495a-112">To organize the project, create a new folder and name it *Models* to hold the type files.</span></span> <span data-ttu-id="c495a-113">Umieść pliki typu w folderze *modele* :</span><span class="sxs-lookup"><span data-stu-id="c495a-113">Place the type files into the *Models* folder:</span></span>

```
/MyProject
|__/Models
   |__AccountInformation.cs
   |__MonthlyReportRecords.cs
|__MyProject.csproj
|__Program.cs
```

<span data-ttu-id="c495a-114">Projekty, które logicznie grupują pliki do folderów, są łatwe do przechodzenia i konserwowania.</span><span class="sxs-lookup"><span data-stu-id="c495a-114">Projects that logically group files into folders are easy to navigate and maintain.</span></span> <span data-ttu-id="c495a-115">W następnej sekcji utworzysz bardziej skomplikowany przykład z użyciem folderów i testów jednostkowych.</span><span class="sxs-lookup"><span data-stu-id="c495a-115">In the next section, you create a more complex sample with folders and unit testing.</span></span>

## <a name="organizing-and-testing-using-the-newtypes-pets-sample"></a><span data-ttu-id="c495a-116">Organizowanie i testowanie przy użyciu przykładu NewTypes zwierząt domowych</span><span class="sxs-lookup"><span data-stu-id="c495a-116">Organizing and testing using the NewTypes Pets Sample</span></span>

### <a name="prerequisites"></a><span data-ttu-id="c495a-117">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c495a-117">Prerequisites</span></span>

* <span data-ttu-id="c495a-118">[.Net 5,0 SDK](https://dotnet.microsoft.com/download) lub nowsza wersja.</span><span class="sxs-lookup"><span data-stu-id="c495a-118">[.NET 5.0 SDK](https://dotnet.microsoft.com/download) or a later version.</span></span>

### <a name="building-the-sample"></a><span data-ttu-id="c495a-119">Kompilowanie przykładu</span><span class="sxs-lookup"><span data-stu-id="c495a-119">Building the sample</span></span>

<span data-ttu-id="c495a-120">Poniższe kroki można wykonać przy użyciu [przykładowej NewTypes zwierząt domowych](https://github.com/dotnet/samples/tree/master/core/console-apps/NewTypesMsBuild) lub utworzyć własne pliki i foldery.</span><span class="sxs-lookup"><span data-stu-id="c495a-120">For the following steps, you can either follow along using the [NewTypes Pets Sample](https://github.com/dotnet/samples/tree/master/core/console-apps/NewTypesMsBuild) or create your own files and folders.</span></span> <span data-ttu-id="c495a-121">Typy są logicznie zorganizowane ze strukturą folderów, która umożliwia dodanie więcej typów później, a testy są również logicznie umieszczane w folderach, co pozwala na dodanie dalszych testów później.</span><span class="sxs-lookup"><span data-stu-id="c495a-121">The types are logically organized into a folder structure that permits the addition of more types later, and tests are also logically placed in folders permitting the addition of more tests later.</span></span>

<span data-ttu-id="c495a-122">Przykład zawiera dwa typy `Dog` i `Cat` i ma implementację wspólnego interfejsu, `IPet` .</span><span class="sxs-lookup"><span data-stu-id="c495a-122">The sample contains two types, `Dog` and `Cat`, and has them implement a common interface, `IPet`.</span></span> <span data-ttu-id="c495a-123">W przypadku `NewTypes` projektu celem jest zorganizowanie typów związanych z PET w folderze *zwierząt domowych* .</span><span class="sxs-lookup"><span data-stu-id="c495a-123">For the `NewTypes` project, your goal is to organize the pet-related types into a *Pets* folder.</span></span> <span data-ttu-id="c495a-124">Jeśli później zostanie dodany inny zestaw typów, *WildAnimals* na przykład, są umieszczane w folderze *NewTypes* obok folderu *zwierzęta* .</span><span class="sxs-lookup"><span data-stu-id="c495a-124">If another set of types is added later, *WildAnimals* for example, they're placed in the *NewTypes* folder alongside the *Pets* folder.</span></span> <span data-ttu-id="c495a-125">Folder *WildAnimals* może zawierać typy dla zwierząt, które nie są zwierzętami, takimi jak `Squirrel` i `Rabbit` .</span><span class="sxs-lookup"><span data-stu-id="c495a-125">The *WildAnimals* folder may contain types for animals that aren't pets, such as `Squirrel` and `Rabbit` types.</span></span> <span data-ttu-id="c495a-126">W ten sposób, gdy są dodawane typy, projekt pozostaje dobrze zorganizowany.</span><span class="sxs-lookup"><span data-stu-id="c495a-126">In this way as types are added, the project remains well organized.</span></span>

<span data-ttu-id="c495a-127">Utwórz następującą strukturę folderów z wyróżnioną zawartością pliku:</span><span class="sxs-lookup"><span data-stu-id="c495a-127">Create the following folder structure with file content indicated:</span></span>

```
/NewTypes
|__/src
   |__/NewTypes
      |__/Pets
         |__Dog.cs
         |__Cat.cs
         |__IPet.cs
      |__Program.cs
      |__NewTypes.csproj
```

<span data-ttu-id="c495a-128">*IPet.cs*:</span><span class="sxs-lookup"><span data-stu-id="c495a-128">*IPet.cs*:</span></span>

[!code-csharp[IPet interface](../../../samples/snippets/core/tutorials/testing-with-cli/csharp/src/NewTypes/Pets/IPet.cs)]

<span data-ttu-id="c495a-129">*Dog.cs*:</span><span class="sxs-lookup"><span data-stu-id="c495a-129">*Dog.cs*:</span></span>

[!code-csharp[Dog class](../../../samples/snippets/core/tutorials/testing-with-cli/csharp/src/NewTypes/Pets/Dog.cs)]

<span data-ttu-id="c495a-130">*Cat.cs*:</span><span class="sxs-lookup"><span data-stu-id="c495a-130">*Cat.cs*:</span></span>

[!code-csharp[Cat class](../../../samples/snippets/core/tutorials/testing-with-cli/csharp/src/NewTypes/Pets/Cat.cs)]

<span data-ttu-id="c495a-131">*Program.cs*:</span><span class="sxs-lookup"><span data-stu-id="c495a-131">*Program.cs*:</span></span>

[!code-csharp[Main](../../../samples/snippets/core/tutorials/testing-with-cli/csharp/src/NewTypes/Program.cs)]

<span data-ttu-id="c495a-132">*NewTypes. csproj*:</span><span class="sxs-lookup"><span data-stu-id="c495a-132">*NewTypes.csproj*:</span></span>

[!code-xml[NewTypes csproj](../../../samples/snippets/core/tutorials/testing-with-cli/csharp/src/NewTypes/NewTypes.csproj)]

<span data-ttu-id="c495a-133">Uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="c495a-133">Execute the following command:</span></span>

```dotnetcli
dotnet run
```

<span data-ttu-id="c495a-134">Uzyskaj następujące dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="c495a-134">Obtain the following output:</span></span>

```console
Woof!
Meow!
```

<span data-ttu-id="c495a-135">Ćwiczenie opcjonalne: można dodać nowy typ PET, taki jak `Bird` , rozszerzając ten projekt.</span><span class="sxs-lookup"><span data-stu-id="c495a-135">Optional exercise: You can add a new pet type, such as a `Bird`, by extending this project.</span></span> <span data-ttu-id="c495a-136">`TalkToOwner`Nadaj metodu ptakowi wartość `Tweet!` Owner.</span><span class="sxs-lookup"><span data-stu-id="c495a-136">Make the bird's `TalkToOwner` method give a `Tweet!` to the owner.</span></span> <span data-ttu-id="c495a-137">Ponownie uruchom aplikację.</span><span class="sxs-lookup"><span data-stu-id="c495a-137">Run the app again.</span></span> <span data-ttu-id="c495a-138">Dane wyjściowe będą zawierać `Tweet!`</span><span class="sxs-lookup"><span data-stu-id="c495a-138">The output will include `Tweet!`</span></span>

### <a name="testing-the-sample"></a><span data-ttu-id="c495a-139">Testowanie przykładu</span><span class="sxs-lookup"><span data-stu-id="c495a-139">Testing the sample</span></span>

<span data-ttu-id="c495a-140">`NewTypes`Projekt jest na miejscu i został zorganizowany przez utrzymywanie typów związanych ze zwierzętami ze zwierząt domowych w folderze.</span><span class="sxs-lookup"><span data-stu-id="c495a-140">The `NewTypes` project is in place, and you've organized it by keeping the pets-related types in a folder.</span></span> <span data-ttu-id="c495a-141">Następnie utwórz projekt testowy i zacznij pisać testy za pomocą platformy testów [xUnit](https://xunit.net/) .</span><span class="sxs-lookup"><span data-stu-id="c495a-141">Next, create your test project and start writing tests with the [xUnit](https://xunit.net/) test framework.</span></span> <span data-ttu-id="c495a-142">Testy jednostkowe umożliwiają automatyczne sprawdzanie zachowania typów PET w celu potwierdzenia, że działają prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="c495a-142">Unit testing allows you to automatically check the behavior of your pet types to confirm that they're operating properly.</span></span>

<span data-ttu-id="c495a-143">Przejdź z powrotem do folderu *src* i Utwórz folder *testowy* z folderem *NewTypesTests* w nim.</span><span class="sxs-lookup"><span data-stu-id="c495a-143">Navigate back to the *src* folder and create a *test* folder with a *NewTypesTests* folder within it.</span></span> <span data-ttu-id="c495a-144">W wierszu polecenia w folderze *NewTypesTests* wykonaj polecenie `dotnet new xunit` .</span><span class="sxs-lookup"><span data-stu-id="c495a-144">At a command prompt from the *NewTypesTests* folder, execute `dotnet new xunit`.</span></span> <span data-ttu-id="c495a-145">Spowoduje to utworzenie dwóch plików: *NewTypesTests. csproj* i *UnitTest1.cs*.</span><span class="sxs-lookup"><span data-stu-id="c495a-145">This produces two files: *NewTypesTests.csproj* and *UnitTest1.cs*.</span></span>

<span data-ttu-id="c495a-146">Projekt testowy nie może obecnie testować typów w `NewTypes` i wymaga odwołania projektu do `NewTypes` projektu.</span><span class="sxs-lookup"><span data-stu-id="c495a-146">The test project cannot currently test the types in `NewTypes` and requires a project reference to the `NewTypes` project.</span></span> <span data-ttu-id="c495a-147">Aby dodać odwołanie do projektu, użyj [`dotnet add reference`](../tools/dotnet-add-reference.md) polecenia:</span><span class="sxs-lookup"><span data-stu-id="c495a-147">To add a project reference, use the [`dotnet add reference`](../tools/dotnet-add-reference.md) command:</span></span>

```dotnetcli
dotnet add reference ../../src/NewTypes/NewTypes.csproj
```

<span data-ttu-id="c495a-148">Lub można także ręcznie dodać odwołanie do projektu przez dodanie `<ItemGroup>` węzła do pliku *NewTypesTests. csproj* :</span><span class="sxs-lookup"><span data-stu-id="c495a-148">Or, you also have the option of manually adding the project reference by adding an `<ItemGroup>` node to the *NewTypesTests.csproj* file:</span></span>

```xml
<ItemGroup>
  <ProjectReference Include="../../src/NewTypes/NewTypes.csproj" />
</ItemGroup>
```

<span data-ttu-id="c495a-149">*NewTypesTests. csproj*:</span><span class="sxs-lookup"><span data-stu-id="c495a-149">*NewTypesTests.csproj*:</span></span>

[!code-xml[NewTypesTests csproj](../../../samples/snippets/core/tutorials/testing-with-cli/csharp/test/NewTypesTests/NewTypesTests.csproj)]

<span data-ttu-id="c495a-150">Plik *NewTypesTests. csproj* zawiera następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="c495a-150">The *NewTypesTests.csproj* file contains the following:</span></span>

* <span data-ttu-id="c495a-151">Odwołanie do pakietu `Microsoft.NET.Test.Sdk` , do infrastruktury testowania .NET</span><span class="sxs-lookup"><span data-stu-id="c495a-151">Package reference to `Microsoft.NET.Test.Sdk`, the .NET testing infrastructure</span></span>
* <span data-ttu-id="c495a-152">Odwołanie do pakietu `xunit` , do struktury testowania xUnit</span><span class="sxs-lookup"><span data-stu-id="c495a-152">Package reference to `xunit`, the xUnit testing framework</span></span>
* <span data-ttu-id="c495a-153">Odwołanie do pakietu `xunit.runner.visualstudio` , do modułu uruchamiającego testy</span><span class="sxs-lookup"><span data-stu-id="c495a-153">Package reference to `xunit.runner.visualstudio`, the test runner</span></span>
* <span data-ttu-id="c495a-154">Odwołanie do projektu do `NewTypes` , kod do przetestowania</span><span class="sxs-lookup"><span data-stu-id="c495a-154">Project reference to `NewTypes`, the code to test</span></span>

<span data-ttu-id="c495a-155">Zmień nazwę *UnitTest1.cs* na *PetTests.cs* i Zastąp kod w pliku następującym:</span><span class="sxs-lookup"><span data-stu-id="c495a-155">Change the name of *UnitTest1.cs* to *PetTests.cs* and replace the code in the file with the following:</span></span>

```csharp
using System;
using Xunit;
using Pets;

public class PetTests
{
    [Fact]
    public void DogTalkToOwnerReturnsWoof()
    {
        string expected = "Woof!";
        string actual = new Dog().TalkToOwner();

        Assert.NotEqual(expected, actual);
    }

    [Fact]
    public void CatTalkToOwnerReturnsMeow()
    {
        string expected = "Meow!";
        string actual = new Cat().TalkToOwner();

        Assert.NotEqual(expected, actual);
    }
}
```

<span data-ttu-id="c495a-156">Opcjonalne ćwiczenie: Jeśli wcześniej dodano `Bird` Typ, który przekazuje `Tweet!` do właściciela, Dodaj metodę testową do pliku *PetTests.cs* , `BirdTalkToOwnerReturnsTweet` Aby sprawdzić, czy `TalkToOwner` Metoda działa prawidłowo dla tego `Bird` typu.</span><span class="sxs-lookup"><span data-stu-id="c495a-156">Optional exercise: If you added a `Bird` type earlier that yields a `Tweet!` to the owner, add a test method to the *PetTests.cs* file, `BirdTalkToOwnerReturnsTweet`, to check that the `TalkToOwner` method works correctly for the `Bird` type.</span></span>

> [!NOTE]
> <span data-ttu-id="c495a-157">Chociaż oczekuje się, że `expected` `actual` wartości i są równe, wstępne potwierdzenie ze `Assert.NotEqual` sprawdzaniem określa, że te wartości *nie są równe*.</span><span class="sxs-lookup"><span data-stu-id="c495a-157">Although you expect that the `expected` and `actual` values are equal, an initial assertion with the `Assert.NotEqual` check specifies that these values are *not equal*.</span></span> <span data-ttu-id="c495a-158">Zawsze należy utworzyć test, aby nie można było sprawdzić logiki testu.</span><span class="sxs-lookup"><span data-stu-id="c495a-158">Always initially create a test to fail in order to check the logic of the test.</span></span> <span data-ttu-id="c495a-159">Po upewnieniu się, że test zakończy się niepowodzeniem, Dostosuj potwierdzenie, aby zezwolić na przekazanie testu.</span><span class="sxs-lookup"><span data-stu-id="c495a-159">After you confirm that the test fails, adjust the assertion to allow the test to pass.</span></span>

<span data-ttu-id="c495a-160">Poniżej przedstawiono kompletną strukturę projektu:</span><span class="sxs-lookup"><span data-stu-id="c495a-160">The following shows the complete project structure:</span></span>

```
/NewTypes
|__/src
   |__/NewTypes
      |__/Pets
         |__Dog.cs
         |__Cat.cs
         |__IPet.cs
      |__Program.cs
      |__NewTypes.csproj
|__/test
   |__NewTypesTests
      |__PetTests.cs
      |__NewTypesTests.csproj
```

<span data-ttu-id="c495a-161">Uruchom w katalogu *test/NewTypesTests* .</span><span class="sxs-lookup"><span data-stu-id="c495a-161">Start in the *test/NewTypesTests* directory.</span></span> <span data-ttu-id="c495a-162">Uruchom testy za pomocą [`dotnet test`](../tools/dotnet-test.md) polecenia.</span><span class="sxs-lookup"><span data-stu-id="c495a-162">Run the tests with the [`dotnet test`](../tools/dotnet-test.md) command.</span></span> <span data-ttu-id="c495a-163">To polecenie uruchamia program Test Runner określony w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="c495a-163">This command starts the test runner specified in the project file.</span></span>

<span data-ttu-id="c495a-164">Zgodnie z oczekiwaniami testowanie nie powiedzie się, a w konsoli programu zostaną wyświetlone następujące dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="c495a-164">As expected, testing fails, and the console displays the following output:</span></span>

```output
Test run for C:\Source\dotnet\docs\samples\snippets\core\tutorials\testing-with-cli\csharp\test\NewTypesTests\bin\Debug\net5.0\NewTypesTests.dll (.NETCoreApp,Version=v5.0)
Microsoft (R) Test Execution Command Line Tool Version 16.8.1
Copyright (c) Microsoft Corporation.  All rights reserved.

Starting test execution, please wait...
A total of 1 test files matched the specified pattern.
[xUnit.net 00:00:00.50]     PetTests.DogTalkToOwnerReturnsWoof [FAIL]
  Failed PetTests.DogTalkToOwnerReturnsWoof [6 ms]
  Error Message:
   Assert.NotEqual() Failure
Expected: Not "Woof!"
Actual:   "Woof!"
  Stack Trace:
     at PetTests.DogTalkToOwnerReturnsWoof() in C:\Source\dotnet\docs\samples\snippets\core\tutorials\testing-with-cli\csharp\test\NewTypesTests\PetTests.cs:line 13

Failed!  - Failed:     1, Passed:     1, Skipped:     0, Total:     2, Duration: 8 ms - NewTypesTests.dll (net5.0)
```

<span data-ttu-id="c495a-165">Zmień potwierdzenia testów z `Assert.NotEqual` na `Assert.Equal` :</span><span class="sxs-lookup"><span data-stu-id="c495a-165">Change the assertions of your tests from `Assert.NotEqual` to `Assert.Equal`:</span></span>

[!code-csharp[PetTests class](../../../samples/snippets/core/tutorials/testing-with-cli/csharp/test/NewTypesTests/PetTests.cs)]

<span data-ttu-id="c495a-166">Uruchom testy przy użyciu `dotnet test` polecenia i uzyskaj następujące dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="c495a-166">Re-run the tests with the `dotnet test` command and obtain the following output:</span></span>

```output
Test run for C:\Source\dotnet\docs\samples\snippets\core\tutorials\testing-with-cli\csharp\test\NewTypesTests\bin\Debug\net5.0\NewTypesTests.dll (.NETCoreApp,Version=v5.0)
Microsoft (R) Test Execution Command Line Tool Version 16.8.1
Copyright (c) Microsoft Corporation.  All rights reserved.

Starting test execution, please wait...
A total of 1 test files matched the specified pattern.

Passed!  - Failed:     0, Passed:     2, Skipped:     0, Total:     2, Duration: 2 ms - NewTypesTests.dll (net5.0)
```

<span data-ttu-id="c495a-167">Testowanie przebiega.</span><span class="sxs-lookup"><span data-stu-id="c495a-167">Testing passes.</span></span> <span data-ttu-id="c495a-168">Metody typów PET zwracają poprawne wartości podczas rozmowy z właścicielem.</span><span class="sxs-lookup"><span data-stu-id="c495a-168">The pet types' methods return the correct values when talking to the owner.</span></span>

<span data-ttu-id="c495a-169">Wiesz już, jak można organizować i testować projekty przy użyciu xUnit.</span><span class="sxs-lookup"><span data-stu-id="c495a-169">You've learned techniques for organizing and testing projects using xUnit.</span></span> <span data-ttu-id="c495a-170">Przejdź do tych technik, stosując je we własnych projektach.</span><span class="sxs-lookup"><span data-stu-id="c495a-170">Go forward with these techniques applying them in your own projects.</span></span> <span data-ttu-id="c495a-171">*Radosne kodowanie!*</span><span class="sxs-lookup"><span data-stu-id="c495a-171">*Happy coding!*</span></span>
