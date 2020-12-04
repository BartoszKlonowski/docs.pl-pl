---
title: Tworzenie biblioteki klas .NET przy użyciu Visual Studio dla komputerów Mac
description: Dowiedz się, jak utworzyć bibliotekę klas .NET przy użyciu Visual Studio dla komputerów Mac.
ms.date: 11/30/2020
ms.openlocfilehash: 1b6b26de06d18d505fa6dde3ff9779a3dab3f1e6
ms.sourcegitcommit: 9d525bb8109216ca1dc9e39c149d4902f4b43da5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2020
ms.locfileid: "96599312"
---
# <a name="tutorial-create-a-net-class-library-using-visual-studio-for-mac"></a><span data-ttu-id="dc111-103">Samouczek: Tworzenie biblioteki klas .NET przy użyciu Visual Studio dla komputerów Mac</span><span class="sxs-lookup"><span data-stu-id="dc111-103">Tutorial: Create a .NET class library using Visual Studio for Mac</span></span>

<span data-ttu-id="dc111-104">W tym samouczku utworzysz bibliotekę klas, która zawiera jedną metodę obsługi ciągów.</span><span class="sxs-lookup"><span data-stu-id="dc111-104">In this tutorial, you create a class library that contains a single string-handling method.</span></span>

<span data-ttu-id="dc111-105">*Biblioteka klas* definiuje typy i metody, które są wywoływane przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="dc111-105">A *class library* defines types and methods that are called by an application.</span></span> <span data-ttu-id="dc111-106">Jeśli biblioteka jest przeznaczona .NET Standard 2,0, może być wywoływana przez dowolną implementację platformy .NET (w tym .NET Framework), która obsługuje .NET Standard 2,0.</span><span class="sxs-lookup"><span data-stu-id="dc111-106">If the library targets .NET Standard 2.0, it can be called by any .NET implementation (including .NET Framework) that supports .NET Standard 2.0.</span></span> <span data-ttu-id="dc111-107">Jeśli biblioteka jest przeznaczona dla platformy .NET 5, może być wywoływana przez dowolną aplikację, która jest przeznaczona dla platformy .NET 5.</span><span class="sxs-lookup"><span data-stu-id="dc111-107">If the library targets .NET 5, it can be called by any application that targets .NET 5.</span></span> <span data-ttu-id="dc111-108">W tym samouczku przedstawiono sposób ukierunkowania platformy .NET 5.</span><span class="sxs-lookup"><span data-stu-id="dc111-108">This tutorial shows how to target .NET 5.</span></span>

> [!NOTE]
> <span data-ttu-id="dc111-109">Opinie są wysoce wyceniane.</span><span class="sxs-lookup"><span data-stu-id="dc111-109">Your feedback is highly valued.</span></span> <span data-ttu-id="dc111-110">Istnieją dwa sposoby przekazywania opinii zespołowi programistycznemu na Visual Studio dla komputerów Mac:</span><span class="sxs-lookup"><span data-stu-id="dc111-110">There are two ways you can provide feedback to the development team on Visual Studio for Mac:</span></span>
>
> - <span data-ttu-id="dc111-111">W Visual Studio dla komputerów Mac wybierz pozycję **Pomoc**  >  **Zgłoś problem** z menu lub **Zgłoś problem** na ekranie powitalnym, co spowoduje otwarcie okna umożliwiającego zgłoszenie usterki.</span><span class="sxs-lookup"><span data-stu-id="dc111-111">In Visual Studio for Mac, select **Help** > **Report a Problem** from the menu or **Report a Problem** from the Welcome screen, which opens a window for filing a bug report.</span></span> <span data-ttu-id="dc111-112">Swoje opinie możesz śledzić w portalu [Społeczność deweloperów](https://aka.ms/feedback/report?space=41).</span><span class="sxs-lookup"><span data-stu-id="dc111-112">You can track your feedback in the [Developer Community](https://aka.ms/feedback/report?space=41) portal.</span></span>
> - <span data-ttu-id="dc111-113">Aby dokonać sugestii, wybierz pozycję **Pomoc**  >  **Podaj sugestię** z menu lub **Podaj sugestię** z ekranu powitalnego, który przeprowadzi Cię do [witryny internetowej społeczność deweloperów Visual Studio dla komputerów Mac](https://aka.ms/feedback/suggest?space=41).</span><span class="sxs-lookup"><span data-stu-id="dc111-113">To make a suggestion, select **Help** > **Provide a Suggestion** from the menu or **Provide a Suggestion** from the Welcome screen, which takes you to the [Visual Studio for Mac Developer Community webpage](https://aka.ms/feedback/suggest?space=41).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc111-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="dc111-114">Prerequisites</span></span>

* <span data-ttu-id="dc111-115">[Zainstaluj program Visual Studio dla komputerów Mac w wersji 8,8 lub nowszej](https://visualstudio.microsoft.com/vs/mac/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link).</span><span class="sxs-lookup"><span data-stu-id="dc111-115">[Install Visual Studio for Mac version 8.8 or later](https://visualstudio.microsoft.com/vs/mac/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link).</span></span> <span data-ttu-id="dc111-116">Wybierz opcję zainstalowania platformy .NET Core.</span><span class="sxs-lookup"><span data-stu-id="dc111-116">Select the option to install .NET Core.</span></span> <span data-ttu-id="dc111-117">Instalowanie platformy Xamarin jest opcjonalne w przypadku programowania na platformie .NET.</span><span class="sxs-lookup"><span data-stu-id="dc111-117">Installing Xamarin is optional for .NET development.</span></span> <span data-ttu-id="dc111-118">Więcej informacji można znaleźć w następujących zasobach:</span><span class="sxs-lookup"><span data-stu-id="dc111-118">For more information, see the following resources:</span></span>

  * <span data-ttu-id="dc111-119">[Samouczek: instalowanie Visual Studio dla komputerów Mac](/visualstudio/mac/installation).</span><span class="sxs-lookup"><span data-stu-id="dc111-119">[Tutorial: Install Visual Studio for Mac](/visualstudio/mac/installation).</span></span>
  * <span data-ttu-id="dc111-120">[Obsługiwane wersje macOS](../install/macos.md).</span><span class="sxs-lookup"><span data-stu-id="dc111-120">[Supported macOS versions](../install/macos.md).</span></span>
  * <span data-ttu-id="dc111-121">[Wersje platformy .NET obsługiwane przez Visual Studio dla komputerów Mac](/visualstudio/mac/net-core-support).</span><span class="sxs-lookup"><span data-stu-id="dc111-121">[.NET versions supported by Visual Studio for Mac](/visualstudio/mac/net-core-support).</span></span>

## <a name="create-a-solution-with-a-class-library-project"></a><span data-ttu-id="dc111-122">Utwórz rozwiązanie z projektem biblioteki klas</span><span class="sxs-lookup"><span data-stu-id="dc111-122">Create a solution with a class library project</span></span>

<span data-ttu-id="dc111-123">Rozwiązanie programu Visual Studio służy jako kontener dla jednego lub wielu projektów.</span><span class="sxs-lookup"><span data-stu-id="dc111-123">A Visual Studio solution serves as a container for one or more projects.</span></span> <span data-ttu-id="dc111-124">Utwórz rozwiązanie i projekt biblioteki klas w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="dc111-124">Create a solution and a class library project in the solution.</span></span> <span data-ttu-id="dc111-125">Kolejne powiązane projekty zostaną dodane do tego samego rozwiązania później.</span><span class="sxs-lookup"><span data-stu-id="dc111-125">You'll add additional, related projects to the same solution later.</span></span>

1. <span data-ttu-id="dc111-126">Rozpocznij Visual Studio dla komputerów Mac.</span><span class="sxs-lookup"><span data-stu-id="dc111-126">Start Visual Studio for Mac.</span></span>

1. <span data-ttu-id="dc111-127">W oknie uruchamiania wybierz pozycję **Nowy projekt**.</span><span class="sxs-lookup"><span data-stu-id="dc111-127">In the start window, select **New Project**.</span></span>

1. <span data-ttu-id="dc111-128">W oknie dialogowym **Wybierz szablon dla nowego projektu** wybierz bibliotekę Biblioteka **klas sieci Web i konsoli**  >  **Library**  >  **Class Library**, a następnie wybierz przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="dc111-128">In the **Choose a template for your new project** dialog select **Web and Console** > **Library** > **Class Library**, and then select **Next**.</span></span>

   :::image type="content" source="media/library-with-visual-studio-mac/visual-studio-mac-new-project.png" alt-text="Okno dialogowe Nowy projekt":::

1. <span data-ttu-id="dc111-130">W oknie dialogowym **Konfigurowanie nowej biblioteki klas** wybierz pozycję **.NET 5,0** i wybierz pozycję **dalej**.</span><span class="sxs-lookup"><span data-stu-id="dc111-130">In the **Configure your new Class Library** dialog, choose **.NET 5.0**, and select **Next**.</span></span>

1. <span data-ttu-id="dc111-131">Nadaj projektowi nazwę "StringLibrary" i rozwiązanie "ClassLibraryProjects".</span><span class="sxs-lookup"><span data-stu-id="dc111-131">Name the project "StringLibrary" and the solution "ClassLibraryProjects".</span></span> <span data-ttu-id="dc111-132">Pozostaw opcję **Utwórz katalog projektu w wybranym katalogu rozwiązania** .</span><span class="sxs-lookup"><span data-stu-id="dc111-132">Leave **Create a project directory within the solution directory** selected.</span></span> <span data-ttu-id="dc111-133">Wybierz przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="dc111-133">Select **Create**.</span></span>

   :::image type="content" source="media/library-with-visual-studio-mac/visual-studio-mac-new-project-options.png" alt-text="Opcje okna dialogowego Visual Studio dla komputerów Mac nowego projektu":::

1. <span data-ttu-id="dc111-135">Z menu głównego wybierz pozycję **Wyświetl**  >  **rozwiązanie** i wybierz ikonę dokowania, aby zachować otwartą konsolę.</span><span class="sxs-lookup"><span data-stu-id="dc111-135">From the main menu, select **View** > **Solution**, and select the dock icon to keep the pad open.</span></span>

   :::image type="content" source="media/library-with-visual-studio-mac/solution-dock-icon.png" alt-text="Ikona dokowania dla konsoli rozwiązania":::

1. <span data-ttu-id="dc111-137">W konsoli **rozwiązania** rozwiń `StringLibrary` węzeł, aby odsłonić plik klasy dostarczony przez szablon, *Class1.cs*.</span><span class="sxs-lookup"><span data-stu-id="dc111-137">In the **Solution** pad, expand the `StringLibrary` node to reveal the class file provided by the template, *Class1.cs*.</span></span> <span data-ttu-id="dc111-138"><kbd>naciśnij klawisz Ctrl</kbd>i kliknij plik, wybierz polecenie **Zmień nazwę** z menu kontekstowego, a następnie zmień nazwę pliku na *StringLibrary.cs*.</span><span class="sxs-lookup"><span data-stu-id="dc111-138"><kbd>ctrl</kbd>-click the file, select **Rename** from the context menu, and rename the file to *StringLibrary.cs*.</span></span> <span data-ttu-id="dc111-139">Otwórz plik i Zastąp jego zawartość następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="dc111-139">Open the file and replace the contents with the following code:</span></span>

   :::code language="csharp" source="./snippets/library-with-visual-studio/csharp/StringLibrary/Class1.cs":::

1. <span data-ttu-id="dc111-140">Naciśnij pozycję <kbd>⌘</kbd><kbd>s</kbd> (<kbd>Command</kbd> + <kbd>s</kbd>), aby zapisać plik.</span><span class="sxs-lookup"><span data-stu-id="dc111-140">Press <kbd>⌘</kbd><kbd>S</kbd> (<kbd>command</kbd>+<kbd>S</kbd>) to save the file.</span></span>

1. <span data-ttu-id="dc111-141">Wybierz pozycję **Błędy** na marginesie u dołu okna IDE, aby otworzyć panel **Błędy** .</span><span class="sxs-lookup"><span data-stu-id="dc111-141">Select **Errors** in the margin at the bottom of the IDE window to open the **Errors** panel.</span></span> <span data-ttu-id="dc111-142">Wybierz przycisk **kompilacja danych wyjściowych** .</span><span class="sxs-lookup"><span data-stu-id="dc111-142">Select the **Build Output** button.</span></span>

   :::image type="content" source="media/library-with-visual-studio-mac/visual-studio-mac-error-button.png" alt-text="Dolny margines środowiska IDE programu Visual Studio Mac przedstawiającego przycisk błędy":::

1. <span data-ttu-id="dc111-144">Z menu wybierz pozycję **kompilacja**  >  **Kompiluj wszystko** .</span><span class="sxs-lookup"><span data-stu-id="dc111-144">Select **Build** > **Build All** from the menu.</span></span>

   <span data-ttu-id="dc111-145">Rozwiązanie kompiluje.</span><span class="sxs-lookup"><span data-stu-id="dc111-145">The solution builds.</span></span> <span data-ttu-id="dc111-146">Panel dane wyjściowe kompilacji pokazuje, że kompilacja zakończyła się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="dc111-146">The build output panel shows that the build is successful.</span></span>

   :::image type="content" source="media/library-with-visual-studio-mac/visual-studio-mac-build-panel.png" alt-text="Okienko danych wyjściowych kompilacji programu Visual Studio dla komputerów Mac w panelu Błędy z komunikatem Kompilacja zakończona pomyślnie":::

## <a name="add-a-console-app-to-the-solution"></a><span data-ttu-id="dc111-148">Dodawanie aplikacji konsolowej do rozwiązania</span><span class="sxs-lookup"><span data-stu-id="dc111-148">Add a console app to the solution</span></span>

<span data-ttu-id="dc111-149">Dodaj aplikację konsolową, która używa biblioteki klas.</span><span class="sxs-lookup"><span data-stu-id="dc111-149">Add a console application that uses the class library.</span></span> <span data-ttu-id="dc111-150">Aplikacja wyświetli monit o wprowadzenie ciągu i zgłoszenie, czy ciąg rozpoczyna się od wielkiej litery.</span><span class="sxs-lookup"><span data-stu-id="dc111-150">The app will prompt the user to enter a string and report whether the string begins with an uppercase character.</span></span>

1. <span data-ttu-id="dc111-151">W konsoli **rozwiązania** <kbd>naciśnij klawisz Ctrl</kbd>i kliknij `ClassLibraryProjects` rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="dc111-151">In the **Solution** pad, <kbd>ctrl</kbd>-click the `ClassLibraryProjects` solution.</span></span> <span data-ttu-id="dc111-152">Dodaj nowy projekt **aplikacji konsoli** , wybierając szablon z szablonów aplikacji **sieci Web i konsoli**  >  **App** , a następnie wybierz przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="dc111-152">Add a new **Console Application** project by selecting the template from the **Web and Console** > **App** templates, and select **Next**.</span></span>

1. <span data-ttu-id="dc111-153">Wybierz **platformę .net 5,0** jako **platformę docelową** , a następnie wybierz pozycję **dalej**.</span><span class="sxs-lookup"><span data-stu-id="dc111-153">Select **.NET 5.0** as the **Target Framework** and select **Next**.</span></span>

1. <span data-ttu-id="dc111-154">Nadaj nazwę **pokazowi** projektu.</span><span class="sxs-lookup"><span data-stu-id="dc111-154">Name the project **ShowCase**.</span></span> <span data-ttu-id="dc111-155">Wybierz pozycję **Utwórz** , aby utworzyć projekt w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="dc111-155">Select **Create** to create the project in the solution.</span></span>

   :::image type="content" source="media/library-with-visual-studio-mac/add-showcase-project.png" alt-text="Dodaj projekt pokazu":::

1. <span data-ttu-id="dc111-157">Otwórz plik *program.cs* .</span><span class="sxs-lookup"><span data-stu-id="dc111-157">Open the *Program.cs* file.</span></span> <span data-ttu-id="dc111-158">Zastąp kod następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="dc111-158">Replace the code with the following code:</span></span>

   :::code language="csharp" source="./snippets/library-with-visual-studio/csharp/ShowCase/Program.cs":::

   <span data-ttu-id="dc111-159">Program poprosi użytkownika o wprowadzenie ciągu.</span><span class="sxs-lookup"><span data-stu-id="dc111-159">The program prompts the user to enter a string.</span></span> <span data-ttu-id="dc111-160">Wskazuje, czy ciąg rozpoczyna się od wielkiej litery.</span><span class="sxs-lookup"><span data-stu-id="dc111-160">It indicates whether the string starts with an uppercase character.</span></span> <span data-ttu-id="dc111-161">Jeśli użytkownik naciśnie klawisz <kbd>Enter</kbd> bez wprowadzania ciągu, aplikacja zostanie zakończona, a okno konsoli zostanie zamknięte.</span><span class="sxs-lookup"><span data-stu-id="dc111-161">If the user presses the <kbd>enter</kbd> key without entering a string, the application ends, and the console window closes.</span></span>

   <span data-ttu-id="dc111-162">Kod używa `row` zmiennej do obsługi liczby wierszy danych zapisywana w oknie konsoli.</span><span class="sxs-lookup"><span data-stu-id="dc111-162">The code uses the `row` variable to maintain a count of the number of rows of data written to the console window.</span></span> <span data-ttu-id="dc111-163">Za każdym razem, gdy jest większy lub równy 25, kod czyści okno konsoli i wyświetla komunikat dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="dc111-163">Whenever it's greater than or equal to 25, the code clears the console window and displays a message to the user.</span></span>

## <a name="add-a-project-reference"></a><span data-ttu-id="dc111-164">Dodaj odwołanie do projektu</span><span class="sxs-lookup"><span data-stu-id="dc111-164">Add a project reference</span></span>

<span data-ttu-id="dc111-165">Początkowo nowy projekt aplikacji konsolowej nie ma dostępu do biblioteki klas.</span><span class="sxs-lookup"><span data-stu-id="dc111-165">Initially, the new console app project doesn't have access to the class library.</span></span> <span data-ttu-id="dc111-166">Aby zezwolić na wywoływanie metod w bibliotece klas, Utwórz odwołanie do projektu do projektu biblioteki klas.</span><span class="sxs-lookup"><span data-stu-id="dc111-166">To allow it to call methods in the class library, create a project reference to the class library project.</span></span>

1. <span data-ttu-id="dc111-167">W konsoli **rozwiązania** <kbd>, kliknij</kbd>węzeł **zależności** w nowym projekcie **pokazu** .</span><span class="sxs-lookup"><span data-stu-id="dc111-167">In the **Solutions** pad, <kbd>ctrl</kbd>-click the **Dependencies** node of the new **ShowCase** project.</span></span> <span data-ttu-id="dc111-168">W menu kontekstowym wybierz polecenie **Dodaj odwołanie**.</span><span class="sxs-lookup"><span data-stu-id="dc111-168">In the context menu, select **Add Reference**.</span></span>

1. <span data-ttu-id="dc111-169">W oknie dialogowym **odwołania** wybierz pozycję **StringLibrary** , a następnie wybierz pozycję **OK**.</span><span class="sxs-lookup"><span data-stu-id="dc111-169">In the **References** dialog, select **StringLibrary** and select **OK**.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="dc111-170">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="dc111-170">Run the app</span></span>

1. <span data-ttu-id="dc111-171"><kbd>naciśnij klawisz Ctrl</kbd>i kliknij projekt **pokazu** i wybierz polecenie **Uruchom projekt** z menu kontekstowego.</span><span class="sxs-lookup"><span data-stu-id="dc111-171"><kbd>ctrl</kbd>-click the **ShowCase** project and select **Run project** from the context menu.</span></span>

1. <span data-ttu-id="dc111-172">Wypróbuj program, wprowadzając ciągi i naciskając klawisz <kbd>Enter</kbd>, a następnie naciśnij klawisz <kbd>Enter</kbd> , aby wyjść.</span><span class="sxs-lookup"><span data-stu-id="dc111-172">Try out the program by entering strings and pressing <kbd>enter</kbd>, then press <kbd>enter</kbd> to exit.</span></span>

   :::image type="content" source="media/library-with-visual-studio-mac/visual-studio-mac-console-window.png" alt-text="Visual Studio dla komputerów Mac okno konsoli z uruchomioną aplikacją":::

## <a name="additional-resources"></a><span data-ttu-id="dc111-174">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="dc111-174">Additional resources</span></span>

* [<span data-ttu-id="dc111-175">Tworzenie bibliotek przy użyciu interfejsu wiersza polecenia platformy .NET</span><span class="sxs-lookup"><span data-stu-id="dc111-175">Develop libraries with the .NET CLI</span></span>](libraries.md)
* [<span data-ttu-id="dc111-176">Visual Studio 2019 dla komputerów Mac — Informacje o wersji</span><span class="sxs-lookup"><span data-stu-id="dc111-176">Visual Studio 2019 for Mac Release Notes</span></span>](/visualstudio/releasenotes/vs2019-mac-relnotes)
* <span data-ttu-id="dc111-177">[Wersje .NET Standard i obsługiwane przez nich platformy](../../standard/net-standard.md).</span><span class="sxs-lookup"><span data-stu-id="dc111-177">[.NET Standard versions and the platforms they support](../../standard/net-standard.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc111-178">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dc111-178">Next steps</span></span>

<span data-ttu-id="dc111-179">W tym samouczku utworzono rozwiązanie i projekt biblioteki oraz dodano projekt aplikacji konsoli, który używa biblioteki.</span><span class="sxs-lookup"><span data-stu-id="dc111-179">In this tutorial, you created a solution and a library project, and added a console app project that uses the library.</span></span> <span data-ttu-id="dc111-180">W następnym samouczku dodasz projekt testu jednostkowego do rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="dc111-180">In the next tutorial, you add a unit test project to the solution.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dc111-181">Testowanie biblioteki klas .NET przy użyciu Visual Studio dla komputerów Mac</span><span class="sxs-lookup"><span data-stu-id="dc111-181">Test a .NET class library using Visual Studio for Mac</span></span>](testing-library-with-visual-studio-mac.md)
