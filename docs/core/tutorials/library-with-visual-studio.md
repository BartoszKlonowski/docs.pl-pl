---
title: Tworzenie biblioteki klas .NET przy użyciu programu Visual Studio
description: Dowiedz się, jak utworzyć bibliotekę klas .NET przy użyciu programu Visual Studio.
ms.date: 08/07/2020
dev_langs:
- csharp
- vb
ms.custom: vs-dotnet,contperfq1
ms.openlocfilehash: 6a3f61525ca86afc9ee71d56cbc9450862760ba4
ms.sourcegitcommit: 9d525bb8109216ca1dc9e39c149d4902f4b43da5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2020
ms.locfileid: "96599515"
---
# <a name="tutorial-create-a-net-class-library-using-visual-studio"></a><span data-ttu-id="700ac-103">Samouczek: Tworzenie biblioteki klas .NET przy użyciu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="700ac-103">Tutorial: Create a .NET class library using Visual Studio</span></span>

<span data-ttu-id="700ac-104">W tym samouczku utworzysz prostą bibliotekę klas, która zawiera pojedynczą metodę obsługi ciągów.</span><span class="sxs-lookup"><span data-stu-id="700ac-104">In this tutorial, you create a simple class library that contains a single string-handling method.</span></span>

<span data-ttu-id="700ac-105">*Biblioteka klas* definiuje typy i metody, które są wywoływane przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="700ac-105">A *class library* defines types and methods that are called by an application.</span></span> <span data-ttu-id="700ac-106">Jeśli biblioteka jest przeznaczona .NET Standard 2,0, może być wywoływana przez dowolną implementację platformy .NET (w tym .NET Framework), która obsługuje .NET Standard 2,0.</span><span class="sxs-lookup"><span data-stu-id="700ac-106">If the library targets .NET Standard 2.0, it can be called by any .NET implementation (including .NET Framework) that supports .NET Standard 2.0.</span></span> <span data-ttu-id="700ac-107">Jeśli biblioteka jest przeznaczona dla platformy .NET 5, może być wywoływana przez dowolną aplikację, która jest przeznaczona dla platformy .NET 5.</span><span class="sxs-lookup"><span data-stu-id="700ac-107">If the library targets .NET 5, it can be called by any application that targets .NET 5.</span></span> <span data-ttu-id="700ac-108">W tym samouczku przedstawiono sposób ukierunkowania platformy .NET 5.</span><span class="sxs-lookup"><span data-stu-id="700ac-108">This tutorial shows how to target .NET 5.</span></span>

<span data-ttu-id="700ac-109">Podczas tworzenia biblioteki klas można ją rozpowszechnić jako pakiet NuGet lub jako składnik powiązany z aplikacją, która go używa.</span><span class="sxs-lookup"><span data-stu-id="700ac-109">When you create a class library, you can distribute it as a NuGet package or as a component bundled with the application that uses it.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="700ac-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="700ac-110">Prerequisites</span></span>

- <span data-ttu-id="700ac-111">[Program Visual Studio 2019 w wersji 16,8 lub nowszej](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) z zainstalowanym **wieloplatformowym obciążeniem programistycznym dla platformy .NET Core** .</span><span class="sxs-lookup"><span data-stu-id="700ac-111">[Visual Studio 2019 version 16.8 or a later version](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) with the **.NET Core cross-platform development** workload installed.</span></span> <span data-ttu-id="700ac-112">Zestaw .NET 5,0 SDK jest instalowany automatycznie po wybraniu tego obciążenia.</span><span class="sxs-lookup"><span data-stu-id="700ac-112">The .NET 5.0 SDK is automatically installed when you select this workload.</span></span> <span data-ttu-id="700ac-113">W tym samouczku przyjęto założenie, że **w nowym projekcie zostały włączone wszystkie szablony .NET Core**, jak pokazano w [samouczku: Tworzenie aplikacji konsolowej .NET przy użyciu programu Visual Studio](with-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="700ac-113">This tutorial assumes you have enabled **Show all .NET Core templates in the New project**, as shown in [Tutorial: Create a .NET console application using Visual Studio](with-visual-studio.md).</span></span>

## <a name="create-a-solution"></a><span data-ttu-id="700ac-114">Tworzenie rozwiązania</span><span class="sxs-lookup"><span data-stu-id="700ac-114">Create a solution</span></span>

<span data-ttu-id="700ac-115">Zacznij od utworzenia pustego rozwiązania, aby umieścić projekt biblioteki klas w.</span><span class="sxs-lookup"><span data-stu-id="700ac-115">Start by creating a blank solution to put the class library project in.</span></span> <span data-ttu-id="700ac-116">Rozwiązanie programu Visual Studio służy jako kontener dla jednego lub wielu projektów.</span><span class="sxs-lookup"><span data-stu-id="700ac-116">A Visual Studio solution serves as a container for one or more projects.</span></span> <span data-ttu-id="700ac-117">Dodasz kolejne powiązane projekty do tego samego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="700ac-117">You'll add additional, related projects to the same solution.</span></span>

<span data-ttu-id="700ac-118">Aby utworzyć puste rozwiązanie:</span><span class="sxs-lookup"><span data-stu-id="700ac-118">To create the blank solution:</span></span>

1. <span data-ttu-id="700ac-119">Uruchom program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="700ac-119">Start Visual Studio.</span></span>

2. <span data-ttu-id="700ac-120">W oknie uruchamiania wybierz pozycję **Utwórz nowy projekt**.</span><span class="sxs-lookup"><span data-stu-id="700ac-120">On the start window, choose **Create a new project**.</span></span>

3. <span data-ttu-id="700ac-121">Na stronie **Tworzenie nowego projektu** wprowadź **rozwiązanie** w polu wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="700ac-121">On the **Create a new project** page, enter **solution** in the search box.</span></span> <span data-ttu-id="700ac-122">Wybierz szablon **pustego rozwiązania** , a następnie wybierz przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="700ac-122">Choose the **Blank Solution** template, and then choose **Next**.</span></span>

   :::image type="content" source="media/library-with-visual-studio/blank-solution.png" alt-text="Pusty szablon rozwiązania w programie Visual Studio":::

4. <span data-ttu-id="700ac-124">Na stronie **Konfiguruj nowy projekt** wprowadź **ClassLibraryProjects** w polu **Nazwa projektu** .</span><span class="sxs-lookup"><span data-stu-id="700ac-124">On the **Configure your new project** page, enter **ClassLibraryProjects** in the **Project name** box.</span></span> <span data-ttu-id="700ac-125">Następnie wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="700ac-125">Then choose **Create**.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="700ac-126">Tworzenie projektu biblioteki klas</span><span class="sxs-lookup"><span data-stu-id="700ac-126">Create a class library project</span></span>

1. <span data-ttu-id="700ac-127">Dodaj nowy projekt biblioteki klas .NET o nazwie "StringLibrary" do rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="700ac-127">Add a new .NET class library project named "StringLibrary" to the solution.</span></span>

   1. <span data-ttu-id="700ac-128">Kliknij prawym przyciskiem myszy rozwiązanie w **Eksplorator rozwiązań** i wybierz polecenie **Dodaj**  >  **Nowy projekt**.</span><span class="sxs-lookup"><span data-stu-id="700ac-128">Right-click on the solution in **Solution Explorer** and select **Add** > **New Project**.</span></span>

   1. <span data-ttu-id="700ac-129">Na stronie **Dodawanie nowego projektu** wprowadź **bibliotekę** w polu wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="700ac-129">On the **Add a new project** page, enter **library** in the search box.</span></span> <span data-ttu-id="700ac-130">Wybierz pozycję **C#** lub **Visual Basic** z listy język, a następnie wybierz pozycję **wszystkie platformy** z listy platform.</span><span class="sxs-lookup"><span data-stu-id="700ac-130">Choose **C#** or **Visual Basic** from the Language list, and then choose **All platforms** from the Platform list.</span></span> <span data-ttu-id="700ac-131">Wybierz szablon **Biblioteka klas** , a następnie wybierz przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="700ac-131">Choose the **Class Library** template, and then choose **Next**.</span></span>

   1. <span data-ttu-id="700ac-132">Na stronie **Konfiguruj nowy projekt** wprowadź **StringLibrary** w polu **Nazwa projektu** , a następnie wybierz przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="700ac-132">On the **Configure your new project** page, enter **StringLibrary** in the **Project name** box, and then choose **Next**.</span></span>

   1. <span data-ttu-id="700ac-133">Na stronie **Informacje dodatkowe** wybierz pozycję **.NET 5,0 (bieżąca)**, a następnie wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="700ac-133">On the **Additional information** page, select **.NET 5.0 (Current)**, and then choose **Create**.</span></span>

1. <span data-ttu-id="700ac-134">Upewnij się, że biblioteka jest przeznaczona dla odpowiedniej wersji platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="700ac-134">Check to make sure that the library targets the correct version of .NET.</span></span> <span data-ttu-id="700ac-135">Kliknij prawym przyciskiem myszy projekt Biblioteka w **Eksplorator rozwiązań**, a następnie wybierz polecenie **Właściwości**.</span><span class="sxs-lookup"><span data-stu-id="700ac-135">Right-click on the library project in **Solution Explorer**, and then select **Properties**.</span></span> <span data-ttu-id="700ac-136">Pole tekstowe **platformy docelowej** pokazuje, że projekt jest przeznaczony dla programu .NET 5,0.</span><span class="sxs-lookup"><span data-stu-id="700ac-136">The **Target Framework** text box shows that the project targets .NET 5.0.</span></span>

1. <span data-ttu-id="700ac-137">Jeśli używasz Visual Basic, wyczyść tekst w polu tekstowym **główna przestrzeń nazw** .</span><span class="sxs-lookup"><span data-stu-id="700ac-137">If you're using Visual Basic, clear the text in the **Root namespace** text box.</span></span>

   :::image type="content" source="./media/library-with-visual-studio/vb/library-project-properties.png" alt-text="Właściwości projektu dla biblioteki klas":::

   <span data-ttu-id="700ac-139">Dla każdego projektu Visual Basic automatycznie tworzy przestrzeń nazw, która odnosi się do nazwy projektu.</span><span class="sxs-lookup"><span data-stu-id="700ac-139">For each project, Visual Basic automatically creates a namespace that corresponds to the project name.</span></span> <span data-ttu-id="700ac-140">W tym samouczku zdefiniujesz przestrzeń nazw najwyższego poziomu za pomocą [`namespace`](../../visual-basic/language-reference/statements/namespace-statement.md) słowa kluczowego w pliku kodu.</span><span class="sxs-lookup"><span data-stu-id="700ac-140">In this tutorial, you define a top-level namespace by using the [`namespace`](../../visual-basic/language-reference/statements/namespace-statement.md) keyword in the code file.</span></span>

1. <span data-ttu-id="700ac-141">Zastąp kod w oknie kodu dla *Class1.cs*  lub *Class1. vb* następującym kodem i Zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="700ac-141">Replace the code in the code window for *Class1.cs*  or *Class1.vb* with the following code, and save the file.</span></span> <span data-ttu-id="700ac-142">Jeśli język, którego chcesz użyć, nie jest wyświetlany, Zmień selektor języka w górnej części strony.</span><span class="sxs-lookup"><span data-stu-id="700ac-142">If the language you want to use is not shown, change the language selector at the top of the page.</span></span>

   :::code language="csharp" source="./snippets/library-with-visual-studio/csharp/StringLibrary/Class1.cs":::
   :::code language="vb" source="./snippets/library-with-visual-studio/vb/StringLibrary/Class1.vb":::

   <span data-ttu-id="700ac-143">Biblioteka klas, `UtilityLibraries.StringLibrary` ,,, zawiera metodę o nazwie `StartsWithUpper` .</span><span class="sxs-lookup"><span data-stu-id="700ac-143">The class library, `UtilityLibraries.StringLibrary`, contains a method named `StartsWithUpper`.</span></span> <span data-ttu-id="700ac-144">Ta metoda zwraca <xref:System.Boolean> wartość wskazującą, czy bieżące wystąpienie ciągu zaczyna się od wielkiej litery.</span><span class="sxs-lookup"><span data-stu-id="700ac-144">This method returns a <xref:System.Boolean> value that indicates whether the current string instance begins with an uppercase character.</span></span> <span data-ttu-id="700ac-145">Standard Unicode rozróżnia wielkie litery od małych liter.</span><span class="sxs-lookup"><span data-stu-id="700ac-145">The Unicode standard distinguishes uppercase characters from lowercase characters.</span></span> <span data-ttu-id="700ac-146"><xref:System.Char.IsUpper(System.Char)?displayProperty=nameWithType>Metoda zwraca `true` czy znak jest pisany wielką literą.</span><span class="sxs-lookup"><span data-stu-id="700ac-146">The <xref:System.Char.IsUpper(System.Char)?displayProperty=nameWithType> method returns `true` if a character is uppercase.</span></span>

   <span data-ttu-id="700ac-147">`StartsWithUpper` jest zaimplementowany jako [Metoda rozszerzająca](../../csharp/programming-guide/classes-and-structs/extension-methods.md) , aby można było wywołać ją tak, jakby była elementem członkowskim <xref:System.String> klasy.</span><span class="sxs-lookup"><span data-stu-id="700ac-147">`StartsWithUpper` is implemented as an [extension method](../../csharp/programming-guide/classes-and-structs/extension-methods.md) so that you can call it as if it were a member of the <xref:System.String> class.</span></span>

1. <span data-ttu-id="700ac-148">Na pasku menu wybierz kolejno opcje **Kompiluj** kompilacje  >  **rozwiązanie** lub naciśnij <kbd>klawisze CTRL</kbd> + <kbd>SHIFT</kbd> + <kbd>B</kbd> , aby sprawdzić, czy projekt kompiluje się bez błędu.</span><span class="sxs-lookup"><span data-stu-id="700ac-148">On the menu bar, select **Build** > **Build Solution** or press <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>B</kbd> to verify that the project compiles without error.</span></span>

## <a name="add-a-console-app-to-the-solution"></a><span data-ttu-id="700ac-149">Dodawanie aplikacji konsolowej do rozwiązania</span><span class="sxs-lookup"><span data-stu-id="700ac-149">Add a console app to the solution</span></span>

<span data-ttu-id="700ac-150">Dodaj aplikację konsolową, która używa biblioteki klas.</span><span class="sxs-lookup"><span data-stu-id="700ac-150">Add a console application that uses the class library.</span></span> <span data-ttu-id="700ac-151">Aplikacja wyświetli monit o wprowadzenie ciągu i zgłoszenie, czy ciąg rozpoczyna się od wielkiej litery.</span><span class="sxs-lookup"><span data-stu-id="700ac-151">The app will prompt the user to enter a string and report whether the string begins with an uppercase character.</span></span>

1. <span data-ttu-id="700ac-152">Dodaj nową aplikację konsolową .NET o nazwie "pokaz" do rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="700ac-152">Add a new .NET console application named "ShowCase" to the solution.</span></span>

   1. <span data-ttu-id="700ac-153">Kliknij prawym przyciskiem myszy rozwiązanie w **Eksplorator rozwiązań** i wybierz polecenie **Dodaj**  >  **Nowy projekt**.</span><span class="sxs-lookup"><span data-stu-id="700ac-153">Right-click on the solution in **Solution Explorer** and select **Add** > **New project**.</span></span>

   1. <span data-ttu-id="700ac-154">Na stronie **Dodawanie nowego projektu** wprowadź w polu wyszukiwania **konsolę** .</span><span class="sxs-lookup"><span data-stu-id="700ac-154">On the **Add a new project** page, enter **console** in the search box.</span></span> <span data-ttu-id="700ac-155">Wybierz pozycję **C#** lub **Visual Basic** z listy język, a następnie wybierz pozycję **wszystkie platformy** z listy platform.</span><span class="sxs-lookup"><span data-stu-id="700ac-155">Choose **C#** or **Visual Basic** from the Language list, and then choose **All platforms** from the Platform list.</span></span>

   1. <span data-ttu-id="700ac-156">Wybierz szablon **aplikacja konsoli** , a następnie wybierz przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="700ac-156">Choose the **Console Application** template, and then choose **Next**.</span></span>

   1. <span data-ttu-id="700ac-157">Na stronie **Konfiguruj nowy projekt** wprowadź wartość **Prezentacja** w polu **Nazwa projektu** .</span><span class="sxs-lookup"><span data-stu-id="700ac-157">On the **Configure your new project** page, enter **ShowCase** in the **Project name** box.</span></span> <span data-ttu-id="700ac-158">Następnie wybierz przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="700ac-158">Then choose **Next**.</span></span>

   1. <span data-ttu-id="700ac-159">Na stronie **Informacje dodatkowe** wybierz pozycję **.NET 5,0 (Current)** w polu **platforma docelowa** .</span><span class="sxs-lookup"><span data-stu-id="700ac-159">On the **Additional information** page, select **.NET 5.0 (Current)** in the **Target Framework** box.</span></span> <span data-ttu-id="700ac-160">Następnie wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="700ac-160">Then choose **Create**.</span></span>

1. <span data-ttu-id="700ac-161">W oknie kodu dla pliku *program.cs* lub *program. vb* Zastąp cały kod następującym kodem.</span><span class="sxs-lookup"><span data-stu-id="700ac-161">In the code window for the *Program.cs* or *Program.vb* file, replace all of the code with the following code.</span></span>

   :::code language="csharp" source="./snippets/library-with-visual-studio/csharp/ShowCase/Program.cs":::
   :::code language="vb" source="./snippets/library-with-visual-studio/vb/ShowCase/Program.vb":::

   <span data-ttu-id="700ac-162">Kod używa `row` zmiennej do obsługi liczby wierszy danych zapisywana w oknie konsoli.</span><span class="sxs-lookup"><span data-stu-id="700ac-162">The code uses the `row` variable to maintain a count of the number of rows of data written to the console window.</span></span> <span data-ttu-id="700ac-163">Za każdym razem, gdy jest większy lub równy 25, kod czyści okno konsoli i wyświetla komunikat dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="700ac-163">Whenever it's greater than or equal to 25, the code clears the console window and displays a message to the user.</span></span>

   <span data-ttu-id="700ac-164">Program poprosi użytkownika o wprowadzenie ciągu.</span><span class="sxs-lookup"><span data-stu-id="700ac-164">The program prompts the user to enter a string.</span></span> <span data-ttu-id="700ac-165">Wskazuje, czy ciąg rozpoczyna się od wielkiej litery.</span><span class="sxs-lookup"><span data-stu-id="700ac-165">It indicates whether the string starts with an uppercase character.</span></span> <span data-ttu-id="700ac-166">Jeśli użytkownik naciśnie klawisz <kbd>Enter</kbd> bez wprowadzania ciągu, aplikacja zostanie zakończona, a okno konsoli zostanie zamknięte.</span><span class="sxs-lookup"><span data-stu-id="700ac-166">If the user presses the <kbd>Enter</kbd> key without entering a string, the application ends, and the console window closes.</span></span>

## <a name="add-a-project-reference"></a><span data-ttu-id="700ac-167">Dodaj odwołanie do projektu</span><span class="sxs-lookup"><span data-stu-id="700ac-167">Add a project reference</span></span>

<span data-ttu-id="700ac-168">Początkowo nowy projekt aplikacji konsolowej nie ma dostępu do biblioteki klas.</span><span class="sxs-lookup"><span data-stu-id="700ac-168">Initially, the new console app project doesn't have access to the class library.</span></span> <span data-ttu-id="700ac-169">Aby zezwolić na wywoływanie metod w bibliotece klas, Utwórz odwołanie do projektu do projektu biblioteki klas.</span><span class="sxs-lookup"><span data-stu-id="700ac-169">To allow it to call methods in the class library, create a project reference to the class library project.</span></span>

1. <span data-ttu-id="700ac-170">W **Eksplorator rozwiązań** kliknij prawym przyciskiem myszy `ShowCase` węzeł **zależności** projektu i wybierz polecenie **Dodaj odwołanie do projektu**.</span><span class="sxs-lookup"><span data-stu-id="700ac-170">In **Solution Explorer**, right-click the `ShowCase` project's **Dependencies** node, and select **Add Project Reference**.</span></span>

   :::image type="content" source="media/library-with-visual-studio/add-reference-context-menu.png" alt-text="Dodaj menu kontekstowe odwołania w programie Visual Studio":::

1. <span data-ttu-id="700ac-172">W oknie dialogowym **Menedżer odwołań** wybierz projekt **StringLibrary** , a następnie wybierz **przycisk OK**.</span><span class="sxs-lookup"><span data-stu-id="700ac-172">In the **Reference Manager** dialog, select the **StringLibrary** project, and select **OK**.</span></span>

   :::image type="content" source="media/library-with-visual-studio/manage-project-references.png" alt-text="Okno dialogowe programu Reference Manager z wybraną pozycją StringLibrary":::

## <a name="run-the-app"></a><span data-ttu-id="700ac-174">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="700ac-174">Run the app</span></span>

1. <span data-ttu-id="700ac-175">W **Eksplorator rozwiązań** kliknij prawym przyciskiem myszy projekt **pokazu** i wybierz polecenie **Ustaw jako projekt startowy** w menu kontekstowym.</span><span class="sxs-lookup"><span data-stu-id="700ac-175">In **Solution Explorer**, right-click the **ShowCase** project and select **Set as StartUp Project** in the context menu.</span></span>

   :::image type="content" source="media/library-with-visual-studio/set-startup-project-context-menu.png" alt-text="Menu kontekstowe projektu programu Visual Studio, aby ustawić projekt startowy":::

1. <span data-ttu-id="700ac-177">Naciśnij klawisz <kbd>Ctrl</kbd> + <kbd>F5</kbd> , aby skompilować i uruchomić program bez debugowania.</span><span class="sxs-lookup"><span data-stu-id="700ac-177">Press <kbd>Ctrl</kbd>+<kbd>F5</kbd> to compile and run the program without debugging.</span></span>

   :::image type="content" source="media/library-with-visual-studio/visual-studio-project-toolbar.png" alt-text="Pasek narzędzi projektu programu Visual Studio z widocznym przyciskiem Debuguj":::

1. <span data-ttu-id="700ac-179">Wypróbuj program, wprowadzając ciągi i naciskając klawisz <kbd>Enter</kbd>, a następnie naciśnij klawisz <kbd>Enter</kbd> , aby wyjść.</span><span class="sxs-lookup"><span data-stu-id="700ac-179">Try out the program by entering strings and pressing <kbd>Enter</kbd>, then press <kbd>Enter</kbd> to exit.</span></span>

   :::image type="content" source="media/library-with-visual-studio/run-showcase.png" alt-text="Okno konsoli z uruchomionym pokazem":::

## <a name="additional-resources"></a><span data-ttu-id="700ac-181">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="700ac-181">Additional resources</span></span>

* [<span data-ttu-id="700ac-182">Tworzenie bibliotek przy użyciu interfejsu wiersza polecenia platformy .NET</span><span class="sxs-lookup"><span data-stu-id="700ac-182">Develop libraries with the .NET CLI</span></span>](libraries.md)
* <span data-ttu-id="700ac-183">[Wersje .NET Standard i obsługiwane przez nich platformy](../../standard/net-standard.md).</span><span class="sxs-lookup"><span data-stu-id="700ac-183">[.NET Standard versions and the platforms they support](../../standard/net-standard.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="700ac-184">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="700ac-184">Next steps</span></span>

<span data-ttu-id="700ac-185">W tym samouczku utworzono bibliotekę klas.</span><span class="sxs-lookup"><span data-stu-id="700ac-185">In this tutorial, you created a class library.</span></span> <span data-ttu-id="700ac-186">W następnym samouczku dowiesz się, jak jednostkowo testować bibliotekę klas.</span><span class="sxs-lookup"><span data-stu-id="700ac-186">In the next tutorial, you learn how to unit test the class library.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="700ac-187">Testowanie jednostkowe biblioteki klas .NET przy użyciu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="700ac-187">Unit test a .NET class library using Visual Studio</span></span>](testing-library-with-visual-studio.md)

<span data-ttu-id="700ac-188">Możesz też pominąć zautomatyzowane testowanie jednostkowe i dowiedzieć się, jak udostępnić bibliotekę, tworząc pakiet NuGet:</span><span class="sxs-lookup"><span data-stu-id="700ac-188">Or you can skip automated unit testing and learn how to share the library by creating a NuGet package:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="700ac-189">Tworzenie i publikowanie pakietu przy użyciu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="700ac-189">Create and publish a package using Visual Studio</span></span>](/nuget/quickstart/create-and-publish-a-package-using-visual-studio)

<span data-ttu-id="700ac-190">Lub Dowiedz się, jak opublikować aplikację konsolową.</span><span class="sxs-lookup"><span data-stu-id="700ac-190">Or learn how to publish a console app.</span></span> <span data-ttu-id="700ac-191">Jeśli opublikujesz aplikację konsolową z rozwiązania utworzonego w tym samouczku, Biblioteka klas przejdzie z nim jako plik *. dll* .</span><span class="sxs-lookup"><span data-stu-id="700ac-191">If you publish the console app from the solution you created in this tutorial, the class library goes with it as a *.dll* file.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="700ac-192">Publikowanie aplikacji konsolowej .NET przy użyciu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="700ac-192">Publish a .NET console application using Visual Studio</span></span>](publishing-with-visual-studio.md)
