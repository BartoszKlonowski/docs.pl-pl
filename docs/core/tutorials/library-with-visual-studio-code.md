---
title: Tworzenie biblioteki klas .NET przy użyciu Visual Studio Code
description: Dowiedz się, jak utworzyć bibliotekę klas .NET przy użyciu Visual Studio Code.
ms.date: 11/18/2020
ms.openlocfilehash: 4473163b76060623b364d7dabf7366c3575e3dcd
ms.sourcegitcommit: 9d525bb8109216ca1dc9e39c149d4902f4b43da5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2020
ms.locfileid: "96599502"
---
# <a name="tutorial-create-a-net-class-library-using-visual-studio-code"></a><span data-ttu-id="560fb-103">Samouczek: Tworzenie biblioteki klas .NET przy użyciu Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="560fb-103">Tutorial: Create a .NET class library using Visual Studio Code</span></span>

<span data-ttu-id="560fb-104">W tym samouczku utworzysz prostą bibliotekę narzędzi, która zawiera pojedynczą metodę obsługi ciągów.</span><span class="sxs-lookup"><span data-stu-id="560fb-104">In this tutorial, you create a simple utility library that contains a single string-handling method.</span></span>

<span data-ttu-id="560fb-105">*Biblioteka klas* definiuje typy i metody, które są wywoływane przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="560fb-105">A *class library* defines types and methods that are called by an application.</span></span> <span data-ttu-id="560fb-106">Jeśli biblioteka jest przeznaczona .NET Standard 2,0, może być wywoływana przez dowolną implementację platformy .NET (w tym .NET Framework), która obsługuje .NET Standard 2,0.</span><span class="sxs-lookup"><span data-stu-id="560fb-106">If the library targets .NET Standard 2.0, it can be called by any .NET implementation (including .NET Framework) that supports .NET Standard 2.0.</span></span> <span data-ttu-id="560fb-107">Jeśli biblioteka jest przeznaczona dla platformy .NET 5, może być wywoływana przez dowolną aplikację, która jest przeznaczona dla platformy .NET 5.</span><span class="sxs-lookup"><span data-stu-id="560fb-107">If the library targets .NET 5, it can be called by any application that targets .NET 5.</span></span> <span data-ttu-id="560fb-108">W tym samouczku przedstawiono sposób ukierunkowania platformy .NET 5.</span><span class="sxs-lookup"><span data-stu-id="560fb-108">This tutorial shows how to target .NET 5.</span></span>

<span data-ttu-id="560fb-109">Podczas tworzenia biblioteki klas można ją rozpowszechnić jako składnik innej firmy lub jako składnik pakietu z jedną lub wieloma aplikacjami.</span><span class="sxs-lookup"><span data-stu-id="560fb-109">When you create a class library, you can distribute it as a third-party component or as a bundled component with one or more applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="560fb-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="560fb-110">Prerequisites</span></span>

1. <span data-ttu-id="560fb-111">[Visual Studio Code](https://code.visualstudio.com/) z zainstalowanym [rozszerzeniem języka C#](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp) .</span><span class="sxs-lookup"><span data-stu-id="560fb-111">[Visual Studio Code](https://code.visualstudio.com/) with the [C# extension](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp) installed.</span></span> <span data-ttu-id="560fb-112">Aby uzyskać informacje na temat sposobu instalowania rozszerzeń na Visual Studio Code, zobacz [vs Code rozszerzenia Marketplace](https://code.visualstudio.com/docs/editor/extension-gallery).</span><span class="sxs-lookup"><span data-stu-id="560fb-112">For information about how to install extensions on Visual Studio Code, see [VS Code Extension Marketplace](https://code.visualstudio.com/docs/editor/extension-gallery).</span></span>
2. <span data-ttu-id="560fb-113">[Zestaw .net 5,0 SDK lub nowszy](https://dotnet.microsoft.com/download)</span><span class="sxs-lookup"><span data-stu-id="560fb-113">The [.NET 5.0 SDK or later](https://dotnet.microsoft.com/download)</span></span>

## <a name="create-a-solution"></a><span data-ttu-id="560fb-114">Tworzenie rozwiązania</span><span class="sxs-lookup"><span data-stu-id="560fb-114">Create a solution</span></span>

<span data-ttu-id="560fb-115">Zacznij od utworzenia pustego rozwiązania, aby umieścić projekt biblioteki klas w.</span><span class="sxs-lookup"><span data-stu-id="560fb-115">Start by creating a blank solution to put the class library project in.</span></span> <span data-ttu-id="560fb-116">Rozwiązanie służy jako kontener dla jednego lub wielu projektów.</span><span class="sxs-lookup"><span data-stu-id="560fb-116">A solution serves as a container for one or more projects.</span></span> <span data-ttu-id="560fb-117">Dodasz kolejne powiązane projekty do tego samego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="560fb-117">You'll add additional, related projects to the same solution.</span></span>

1. <span data-ttu-id="560fb-118">Uruchom program Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="560fb-118">Start Visual Studio Code.</span></span>

1. <span data-ttu-id="560fb-119">Wybierz pozycję **plik**  >  **Otwórz folder** (**Otwórz...** na macOS) z menu głównego</span><span class="sxs-lookup"><span data-stu-id="560fb-119">Select **File** > **Open Folder** (**Open...** on macOS) from the main menu</span></span>

1. <span data-ttu-id="560fb-120">W oknie dialogowym **Otwieranie folderu** Utwórz folder *ClassLibraryProjects* , a następnie kliknij pozycję **Wybierz folder** (**Otwórz** w macOS).</span><span class="sxs-lookup"><span data-stu-id="560fb-120">In the **Open Folder** dialog, create a *ClassLibraryProjects* folder and click **Select Folder** (**Open** on macOS).</span></span>

1. <span data-ttu-id="560fb-121">Otwórz **Terminal** w Visual Studio Code, wybierając pozycję **Wyświetl**  >  **Terminal** z menu głównego.</span><span class="sxs-lookup"><span data-stu-id="560fb-121">Open the **Terminal** in Visual Studio Code by selecting **View** > **Terminal** from the main menu.</span></span>

   <span data-ttu-id="560fb-122">Zostanie otwarty **Terminal** z wierszem polecenia w folderze *ClassLibraryProjects* .</span><span class="sxs-lookup"><span data-stu-id="560fb-122">The **Terminal** opens with the command prompt in the *ClassLibraryProjects* folder.</span></span>

1. <span data-ttu-id="560fb-123">W **terminalu** wprowadź następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="560fb-123">In the **Terminal**, enter the following command:</span></span>

   ```dotnetcli
   dotnet new sln
   ```

   <span data-ttu-id="560fb-124">Dane wyjściowe terminalu wyglądają podobnie jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="560fb-124">The terminal output looks like the following example:</span></span>

   ```output
   The template "Solution File" was created successfully.
   ```

## <a name="create-a-class-library-project"></a><span data-ttu-id="560fb-125">Tworzenie projektu biblioteki klas</span><span class="sxs-lookup"><span data-stu-id="560fb-125">Create a class library project</span></span>

<span data-ttu-id="560fb-126">Dodaj nowy projekt biblioteki klas .NET o nazwie "StringLibrary" do rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="560fb-126">Add a new .NET class library project named "StringLibrary" to the solution.</span></span>

1. <span data-ttu-id="560fb-127">W terminalu uruchom następujące polecenie, aby utworzyć projekt biblioteki:</span><span class="sxs-lookup"><span data-stu-id="560fb-127">In the terminal, run the following command to create the library project:</span></span>

   ```dotnetcli
   dotnet new classlib -o StringLibrary
   ```

   <span data-ttu-id="560fb-128">`-o`Polecenie lub `--output` określa lokalizację, w której mają zostać umieszczone wygenerowane dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="560fb-128">The `-o` or `--output` command specifies the location to place the generated output.</span></span>

   <span data-ttu-id="560fb-129">Dane wyjściowe terminalu wyglądają podobnie jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="560fb-129">The terminal output looks like the following example:</span></span>

   ```output
   The template "Class library" was created successfully.
   Processing post-creation actions...
   Running 'dotnet restore' on StringLibrary\StringLibrary.csproj...
     Determining projects to restore...
     Restored C:\Projects\ClassLibraryProjects\StringLibrary\StringLibrary.csproj (in 328 ms).
   Restore succeeded.
   ```

1. <span data-ttu-id="560fb-130">Uruchom następujące polecenie, aby dodać projekt biblioteki do rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="560fb-130">Run the following command to add the library project to the solution:</span></span>

   ```dotnetcli
   dotnet sln add StringLibrary/StringLibrary.csproj
   ```

   <span data-ttu-id="560fb-131">Dane wyjściowe terminalu wyglądają podobnie jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="560fb-131">The terminal output looks like the following example:</span></span>

   ```output
   Project `StringLibrary\StringLibrary.csproj` added to the solution.
   ```

1. <span data-ttu-id="560fb-132">Upewnij się, że biblioteka jest przeznaczona dla platformy .NET 5.</span><span class="sxs-lookup"><span data-stu-id="560fb-132">Check to make sure that the library targets .NET 5.</span></span> <span data-ttu-id="560fb-133">W **Eksploratorze** Otwórz *StringLibrary/StringLibrary. csproj*.</span><span class="sxs-lookup"><span data-stu-id="560fb-133">In **Explorer**, open *StringLibrary/StringLibrary.csproj*.</span></span>

   <span data-ttu-id="560fb-134">`TargetFramework`Element pokazuje, że projekt jest przeznaczony dla programu .net 5,0.</span><span class="sxs-lookup"><span data-stu-id="560fb-134">The `TargetFramework` element shows that the project targets .NET 5.0.</span></span>

   ```xml
   <Project Sdk="Microsoft.NET.Sdk">

     <PropertyGroup>
       <TargetFramework>net5.0</TargetFramework>
     </PropertyGroup>

   </Project>
   ```

1. <span data-ttu-id="560fb-135">Otwórz *Class1.cs* i Zastąp kod następującym kodem.</span><span class="sxs-lookup"><span data-stu-id="560fb-135">Open *Class1.cs* and replace the code with the following code.</span></span>

   :::code language="csharp" source="./snippets/library-with-visual-studio/csharp/StringLibrary/Class1.cs":::

   <span data-ttu-id="560fb-136">Biblioteka klas, `UtilityLibraries.StringLibrary` ,,, zawiera metodę o nazwie `StartsWithUpper` .</span><span class="sxs-lookup"><span data-stu-id="560fb-136">The class library, `UtilityLibraries.StringLibrary`, contains a method named `StartsWithUpper`.</span></span> <span data-ttu-id="560fb-137">Ta metoda zwraca <xref:System.Boolean> wartość wskazującą, czy bieżące wystąpienie ciągu zaczyna się od wielkiej litery.</span><span class="sxs-lookup"><span data-stu-id="560fb-137">This method returns a <xref:System.Boolean> value that indicates whether the current string instance begins with an uppercase character.</span></span> <span data-ttu-id="560fb-138">Standard Unicode rozróżnia wielkie litery od małych liter.</span><span class="sxs-lookup"><span data-stu-id="560fb-138">The Unicode standard distinguishes uppercase characters from lowercase characters.</span></span> <span data-ttu-id="560fb-139"><xref:System.Char.IsUpper(System.Char)?displayProperty=nameWithType>Metoda zwraca `true` czy znak jest pisany wielką literą.</span><span class="sxs-lookup"><span data-stu-id="560fb-139">The <xref:System.Char.IsUpper(System.Char)?displayProperty=nameWithType> method returns `true` if a character is uppercase.</span></span>

1. <span data-ttu-id="560fb-140">Zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="560fb-140">Save the file.</span></span>

1. <span data-ttu-id="560fb-141">Uruchom następujące polecenie, aby skompilować rozwiązanie i sprawdzić, czy projekt kompiluje się bez błędu.</span><span class="sxs-lookup"><span data-stu-id="560fb-141">Run the following command to build the solution and verify that the project compiles without error.</span></span>

   ```dotnetcli
   dotnet build
   ```

   <span data-ttu-id="560fb-142">Dane wyjściowe terminalu wyglądają podobnie jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="560fb-142">The terminal output looks like the following example:</span></span>

   ```output
   Microsoft (R) Build Engine version 16.7.0+b89cb5fde for .NET
   Copyright (C) Microsoft Corporation. All rights reserved.
     Determining projects to restore...
     All projects are up-to-date for restore.
     StringLibrary -> C:\Projects\ClassLibraryProjects\StringLibrary\bin\Debug\net5.0\StringLibrary.dll
   Build succeeded.
       0 Warning(s)
       0 Error(s)
   Time Elapsed 00:00:02.78
   ```

## <a name="add-a-console-app-to-the-solution"></a><span data-ttu-id="560fb-143">Dodawanie aplikacji konsolowej do rozwiązania</span><span class="sxs-lookup"><span data-stu-id="560fb-143">Add a console app to the solution</span></span>

<span data-ttu-id="560fb-144">Dodaj aplikację konsolową, która używa biblioteki klas.</span><span class="sxs-lookup"><span data-stu-id="560fb-144">Add a console application that uses the class library.</span></span> <span data-ttu-id="560fb-145">Aplikacja wyświetli monit o wprowadzenie ciągu i zgłoszenie, czy ciąg rozpoczyna się od wielkiej litery.</span><span class="sxs-lookup"><span data-stu-id="560fb-145">The app will prompt the user to enter a string and report whether the string begins with an uppercase character.</span></span>

1. <span data-ttu-id="560fb-146">W terminalu uruchom następujące polecenie, aby utworzyć projekt aplikacji konsoli:</span><span class="sxs-lookup"><span data-stu-id="560fb-146">In the terminal, run the following command to create the console app project:</span></span>

   ```dotnetcli
   dotnet new console -o ShowCase
   ```

   <span data-ttu-id="560fb-147">Dane wyjściowe terminalu wyglądają podobnie jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="560fb-147">The terminal output looks like the following example:</span></span>

   ```output
   The template "Console Application" was created successfully.
   Processing post-creation actions...
   Running 'dotnet restore' on ShowCase\ShowCase.csproj...  
     Determining projects to restore...
     Restored C:\Projects\ClassLibraryProjects\ShowCase\ShowCase.csproj (in 210 ms).
   Restore succeeded.
   ```

1. <span data-ttu-id="560fb-148">Uruchom następujące polecenie, aby dodać projekt aplikacji konsolowej do rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="560fb-148">Run the following command to add the console app project to the solution:</span></span>

   ```dotnetcli
   dotnet sln add ShowCase/ShowCase.csproj
   ```

   <span data-ttu-id="560fb-149">Dane wyjściowe terminalu wyglądają podobnie jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="560fb-149">The terminal output looks like the following example:</span></span>

   ```output
   Project `ShowCase\ShowCase.csproj` added to the solution.
   ```

1. <span data-ttu-id="560fb-150">Otwórz *Pokaz/Program. cs* i Zastąp cały kod następującym kodem.</span><span class="sxs-lookup"><span data-stu-id="560fb-150">Open *ShowCase/Program.cs* and replace all of the code with the following code.</span></span>

   :::code language="csharp" source="./snippets/library-with-visual-studio/csharp/ShowCase/Program.cs":::

   <span data-ttu-id="560fb-151">Kod używa `row` zmiennej do obsługi liczby wierszy danych zapisywana w oknie konsoli.</span><span class="sxs-lookup"><span data-stu-id="560fb-151">The code uses the `row` variable to maintain a count of the number of rows of data written to the console window.</span></span> <span data-ttu-id="560fb-152">Za każdym razem, gdy jest większy lub równy 25, kod czyści okno konsoli i wyświetla komunikat dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="560fb-152">Whenever it's greater than or equal to 25, the code clears the console window and displays a message to the user.</span></span>

   <span data-ttu-id="560fb-153">Program poprosi użytkownika o wprowadzenie ciągu.</span><span class="sxs-lookup"><span data-stu-id="560fb-153">The program prompts the user to enter a string.</span></span> <span data-ttu-id="560fb-154">Wskazuje, czy ciąg rozpoczyna się od wielkiej litery.</span><span class="sxs-lookup"><span data-stu-id="560fb-154">It indicates whether the string starts with an uppercase character.</span></span> <span data-ttu-id="560fb-155">Jeśli użytkownik naciśnie klawisz <kbd>Enter</kbd> bez wprowadzania ciągu, aplikacja zostanie zakończona, a okno konsoli zostanie zamknięte.</span><span class="sxs-lookup"><span data-stu-id="560fb-155">If the user presses the <kbd>Enter</kbd> key without entering a string, the application ends, and the console window closes.</span></span>

1. <span data-ttu-id="560fb-156">Zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="560fb-156">Save your changes.</span></span>

## <a name="add-a-project-reference"></a><span data-ttu-id="560fb-157">Dodaj odwołanie do projektu</span><span class="sxs-lookup"><span data-stu-id="560fb-157">Add a project reference</span></span>

<span data-ttu-id="560fb-158">Początkowo nowy projekt aplikacji konsolowej nie ma dostępu do biblioteki klas.</span><span class="sxs-lookup"><span data-stu-id="560fb-158">Initially, the new console app project doesn't have access to the class library.</span></span> <span data-ttu-id="560fb-159">Aby zezwolić na wywoływanie metod w bibliotece klas, Utwórz odwołanie do projektu do projektu biblioteki klas.</span><span class="sxs-lookup"><span data-stu-id="560fb-159">To allow it to call methods in the class library, create a project reference to the class library project.</span></span>

1. <span data-ttu-id="560fb-160">Uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="560fb-160">Run the following command:</span></span>

   ```dotnetcli
   dotnet add ShowCase/ShowCase.csproj reference StringLibrary/StringLibrary.csproj
   ```

   <span data-ttu-id="560fb-161">Dane wyjściowe terminalu wyglądają podobnie jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="560fb-161">The terminal output looks like the following example:</span></span>

   ```output
   Reference `..\StringLibrary\StringLibrary.csproj` added to the project.
   ```

## <a name="run-the-app"></a><span data-ttu-id="560fb-162">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="560fb-162">Run the app</span></span>

1. <span data-ttu-id="560fb-163">W terminalu uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="560fb-163">Run the following command in the terminal:</span></span>

   ```dotnetcli
   dotnet run --project ShowCase/ShowCase.csproj
   ```

1. <span data-ttu-id="560fb-164">Wypróbuj program, wprowadzając ciągi i naciskając klawisz <kbd>Enter</kbd>, a następnie naciśnij klawisz <kbd>Enter</kbd> , aby wyjść.</span><span class="sxs-lookup"><span data-stu-id="560fb-164">Try out the program by entering strings and pressing <kbd>Enter</kbd>, then press <kbd>Enter</kbd> to exit.</span></span>

   <span data-ttu-id="560fb-165">Dane wyjściowe terminalu wyglądają podobnie jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="560fb-165">The terminal output looks like the following example:</span></span>

   ```output
   Press <Enter> only to exit; otherwise, enter a string and press <Enter>:

   A string that starts with an uppercase letter
   Input: A string that starts with an uppercase letter
   Begins with uppercase? : Yes

   a string that starts with a lowercase letter
   Input: a string that starts with a lowercase letter
   Begins with uppercase? : No
   ```

## <a name="additional-resources"></a><span data-ttu-id="560fb-166">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="560fb-166">Additional resources</span></span>

* [<span data-ttu-id="560fb-167">Tworzenie bibliotek przy użyciu interfejsu wiersza polecenia platformy .NET</span><span class="sxs-lookup"><span data-stu-id="560fb-167">Develop libraries with the .NET CLI</span></span>](libraries.md)
* <span data-ttu-id="560fb-168">[Wersje .NET Standard i obsługiwane przez nich platformy](../../standard/net-standard.md).</span><span class="sxs-lookup"><span data-stu-id="560fb-168">[.NET Standard versions and the platforms they support](../../standard/net-standard.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="560fb-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="560fb-169">Next steps</span></span>

<span data-ttu-id="560fb-170">W tym samouczku utworzono rozwiązanie, dodano projekt biblioteki i dodano projekt aplikacji konsolowej, który używa biblioteki.</span><span class="sxs-lookup"><span data-stu-id="560fb-170">In this tutorial, you created a solution, added a library project, and added a console app project that uses the library.</span></span> <span data-ttu-id="560fb-171">W następnym samouczku dodasz projekt testu jednostkowego do rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="560fb-171">In the next tutorial, you add a unit test project to the solution.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="560fb-172">Testowanie biblioteki klas .NET za pomocą platformy .NET przy użyciu Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="560fb-172">Test a .NET class library with .NET using Visual Studio Code</span></span>](testing-library-with-visual-studio-code.md)
