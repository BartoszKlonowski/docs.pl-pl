---
title: Debugowanie aplikacji konsolowej .NET przy użyciu Visual Studio dla komputerów Mac
description: Dowiedz się, jak debugować aplikację konsolową .NET przy użyciu programu Visual Studio Mac.
ms.date: 11/30/2020
ms.openlocfilehash: e35bbef5582b6eec00ee48669a0f5d028eb051fb
ms.sourcegitcommit: 9d525bb8109216ca1dc9e39c149d4902f4b43da5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2020
ms.locfileid: "96599619"
---
# <a name="tutorial-debug-a-net-console-application-using-visual-studio-for-mac"></a><span data-ttu-id="fa149-103">Samouczek: debugowanie aplikacji konsolowej .NET przy użyciu Visual Studio dla komputerów Mac</span><span class="sxs-lookup"><span data-stu-id="fa149-103">Tutorial: Debug a .NET console application using Visual Studio for Mac</span></span>

<span data-ttu-id="fa149-104">W tym samouczku przedstawiono narzędzia debugowania dostępne w Visual Studio dla komputerów Mac.</span><span class="sxs-lookup"><span data-stu-id="fa149-104">This tutorial introduces the debugging tools available in Visual Studio for Mac.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fa149-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fa149-105">Prerequisites</span></span>

- <span data-ttu-id="fa149-106">Ten samouczek współpracuje z aplikacją konsolową utworzoną w temacie [Tworzenie aplikacji konsolowej platformy .NET przy użyciu Visual Studio dla komputerów Mac](with-visual-studio-mac.md).</span><span class="sxs-lookup"><span data-stu-id="fa149-106">This tutorial works with the console app that you create in [Create a .NET console application using Visual Studio for Mac](with-visual-studio-mac.md).</span></span>

## <a name="use-debug-build-configuration"></a><span data-ttu-id="fa149-107">Użyj konfiguracji kompilacji debugowania</span><span class="sxs-lookup"><span data-stu-id="fa149-107">Use Debug build configuration</span></span>

<span data-ttu-id="fa149-108">*Debugowanie* i *wydanie* to wbudowane konfiguracje kompilacji programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fa149-108">*Debug* and *Release* are Visual Studio's built-in build configurations.</span></span> <span data-ttu-id="fa149-109">Konfiguracja kompilacji debugowania umożliwia debugowanie i konfigurację wydania dla ostatecznej dystrybucji wersji.</span><span class="sxs-lookup"><span data-stu-id="fa149-109">You use the Debug build configuration for debugging and the Release configuration for the final release distribution.</span></span>

<span data-ttu-id="fa149-110">W konfiguracji debugowania program kompiluje z pełnymi symbolicznymi informacjami o debugowaniu i bez optymalizacji.</span><span class="sxs-lookup"><span data-stu-id="fa149-110">In the Debug configuration, a program compiles with full symbolic debug information and no optimization.</span></span> <span data-ttu-id="fa149-111">Optymalizacja komplikuje debugowanie, ponieważ relacja między kodem źródłowym i wygenerowanymi instrukcjami jest bardziej skomplikowana.</span><span class="sxs-lookup"><span data-stu-id="fa149-111">Optimization complicates debugging, because the relationship between source code and generated instructions is more complex.</span></span> <span data-ttu-id="fa149-112">Konfiguracja wydania programu nie ma symbolicznych informacji o debugowaniu i jest w pełni zoptymalizowana.</span><span class="sxs-lookup"><span data-stu-id="fa149-112">The release configuration of a program has no symbolic debug information and is fully optimized.</span></span>

<span data-ttu-id="fa149-113">Domyślnie Visual Studio dla komputerów Mac używa konfiguracji kompilacji debugowania, więc nie trzeba jej zmieniać przed debugowaniem.</span><span class="sxs-lookup"><span data-stu-id="fa149-113">By default, Visual Studio for Mac uses the Debug build configuration, so you don't need to change it before debugging.</span></span>

1. <span data-ttu-id="fa149-114">Rozpocznij Visual Studio dla komputerów Mac.</span><span class="sxs-lookup"><span data-stu-id="fa149-114">Start Visual Studio for Mac.</span></span>

1. <span data-ttu-id="fa149-115">Otwórz projekt, który został utworzony w temacie [Tworzenie aplikacji konsolowej platformy .NET przy użyciu Visual Studio dla komputerów Mac](with-visual-studio-mac.md).</span><span class="sxs-lookup"><span data-stu-id="fa149-115">Open the project that you created in [Create a .NET console application using Visual Studio for Mac](with-visual-studio-mac.md).</span></span>

   <span data-ttu-id="fa149-116">Bieżąca konfiguracja kompilacji jest pokazywana na pasku narzędzi.</span><span class="sxs-lookup"><span data-stu-id="fa149-116">The current build configuration is shown on the toolbar.</span></span> <span data-ttu-id="fa149-117">Poniższy obraz paska narzędzi pokazuje, że program Visual Studio jest skonfigurowany do kompilowania wersji do debugowania aplikacji:</span><span class="sxs-lookup"><span data-stu-id="fa149-117">The following toolbar image shows that Visual Studio is configured to compile the Debug version of the app:</span></span>

   :::image type="content" source="media/debugging-with-visual-studio-mac/visual-studio-toolbar-debug.png" alt-text="Pasek narzędzi programu Visual Studio z wyróżnioną pozycją Debug":::

## <a name="set-a-breakpoint"></a><span data-ttu-id="fa149-119">Ustawianie punktu przerwania</span><span class="sxs-lookup"><span data-stu-id="fa149-119">Set a breakpoint</span></span>

<span data-ttu-id="fa149-120">*Punkt przerwania* tymczasowo przerywa wykonywanie aplikacji przed wykonaniem wiersza z punktem przerwania.</span><span class="sxs-lookup"><span data-stu-id="fa149-120">A *breakpoint* temporarily interrupts the execution of the application before the line with the breakpoint is executed.</span></span>

1. <span data-ttu-id="fa149-121">Ustaw punkt przerwania w wierszu, w którym wyświetlana jest nazwa, Data i godzina.</span><span class="sxs-lookup"><span data-stu-id="fa149-121">Set a breakpoint on the line that displays the name, date, and time.</span></span> <span data-ttu-id="fa149-122">Aby to zrobić, umieść kursor w wierszu kodu i naciśnij pozycję <kbd>⌘</kbd> <kbd>\\</kbd> (<kbd>polecenie</kbd> + <kbd>\\</kbd> ).</span><span class="sxs-lookup"><span data-stu-id="fa149-122">To do that, place the cursor in the line of code and press <kbd>⌘</kbd><kbd>\\</kbd> (<kbd>command</kbd>+<kbd>\\</kbd>).</span></span> <span data-ttu-id="fa149-123">Innym sposobem ustawienia punktu przerwania jest wybranie opcji **Uruchom**  >  **punkt przerwania** z menu.</span><span class="sxs-lookup"><span data-stu-id="fa149-123">Another way to set a breakpoint is by selecting **Run** > **Toggle Breakpoint** from the menu.</span></span>

   <span data-ttu-id="fa149-124">Program Visual Studio wskazuje wiersz, w którym ustawiany jest punkt przerwania, zaznaczając go i wyświetlając czerwoną kropkę na lewym marginesie.</span><span class="sxs-lookup"><span data-stu-id="fa149-124">Visual Studio indicates the line on which the breakpoint is set by highlighting it and displaying a red dot in the left margin.</span></span>

   :::image type="content" source="media/debugging-with-visual-studio-mac/set-breakpoint-in-editor.png" alt-text="Okno programu Visual Studio z ustawionym punktem przerwania":::

1. <span data-ttu-id="fa149-126">Naciśnij pozycję <kbd>⌘</kbd><kbd>↵</kbd> (<kbd>command</kbd> + <kbd>wprowadź</kbd>polecenie), aby uruchomić program w trybie debugowania.</span><span class="sxs-lookup"><span data-stu-id="fa149-126">Press <kbd>⌘</kbd><kbd>↵</kbd> (<kbd>command</kbd>+<kbd>enter</kbd>) to start the program in debugging mode.</span></span> <span data-ttu-id="fa149-127">Innym sposobem rozpoczęcia debugowania jest wybranie polecenia **Uruchom**  >  **debugowanie** z menu.</span><span class="sxs-lookup"><span data-stu-id="fa149-127">Another way to start debugging is by choosing **Run** > **Start Debugging** from the menu.</span></span>

1. <span data-ttu-id="fa149-128">Wprowadź ciąg w oknie terminalu, gdy program zapyta o nazwę, a następnie naciśnij klawisz <kbd>Enter</kbd>.</span><span class="sxs-lookup"><span data-stu-id="fa149-128">Enter a string in the terminal window when the program prompts for a name, and then press <kbd>enter</kbd>.</span></span>

1. <span data-ttu-id="fa149-129">Wykonanie programu zostaje zatrzymane po osiągnięciu punktu przerwania, zanim `Console.WriteLine` Metoda zostanie wykonana.</span><span class="sxs-lookup"><span data-stu-id="fa149-129">Program execution stops when it reaches the breakpoint, before the `Console.WriteLine` method executes.</span></span>

   :::image type="content" source="media/debugging-with-visual-studio-mac/breakpoint-hit.png" alt-text="Zrzut ekranu punktu przerwania w programie Visual Studio":::

## <a name="use-the-immediate-window"></a><span data-ttu-id="fa149-131">Korzystanie z okna bezpośredniego</span><span class="sxs-lookup"><span data-stu-id="fa149-131">Use the Immediate window</span></span>

<span data-ttu-id="fa149-132">Okno **bezpośrednie** umożliwia korzystanie z debugowanej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fa149-132">The **Immediate** window lets you interact with the application you're debugging.</span></span> <span data-ttu-id="fa149-133">Możesz interaktywnie zmienić wartość zmiennych, aby zobaczyć, jak ma to wpływ na program.</span><span class="sxs-lookup"><span data-stu-id="fa149-133">You can interactively change the value of variables to see how it affects your program.</span></span>

1. <span data-ttu-id="fa149-134">Jeśli okno **bezpośrednie** nie jest widoczne, Wyświetl je, wybierając pozycję **Wyświetl**  >  **konsole debugowania**  >  **natychmiast**.</span><span class="sxs-lookup"><span data-stu-id="fa149-134">If the **Immediate** window is not visible, display it by choosing **View** > **Debug Pads** > **Immediate**.</span></span>

1. <span data-ttu-id="fa149-135">Wprowadź `name = "Gracie"` w oknie **bezpośrednim** i naciśnij klawisz <kbd>Enter</kbd>.</span><span class="sxs-lookup"><span data-stu-id="fa149-135">Enter `name = "Gracie"` in the **Immediate** window and press <kbd>enter</kbd>.</span></span>

1. <span data-ttu-id="fa149-136">Wprowadź `date = date.AddDays(1)` w oknie **bezpośrednim** i naciśnij klawisz <kbd>Enter</kbd>.</span><span class="sxs-lookup"><span data-stu-id="fa149-136">Enter `date = date.AddDays(1)` in the **Immediate** window and press <kbd>enter</kbd>.</span></span>

   <span data-ttu-id="fa149-137">W oknie **bezpośrednim** zostanie wyświetlona nowa wartość zmiennej ciągu i właściwości <xref:System.DateTime> wartości.</span><span class="sxs-lookup"><span data-stu-id="fa149-137">The **Immediate** window displays the new value of the string variable and the properties of the <xref:System.DateTime> value.</span></span>

   :::image type="content" source="media/debugging-with-visual-studio-mac/immediate-window.png" alt-text="Okno bezpośrednie w programie Visual Studio":::

   <span data-ttu-id="fa149-139">W oknie **Ustawienia lokalne** są wyświetlane wartości zmiennych, które są zdefiniowane w aktualnie wykonywanej metodzie.</span><span class="sxs-lookup"><span data-stu-id="fa149-139">The **Locals** window displays the values of variables that are defined in the currently executing method.</span></span> <span data-ttu-id="fa149-140">Wartości zmiennych, które właśnie zmieniono, są aktualizowane w oknie **zmiennych lokalnych** .</span><span class="sxs-lookup"><span data-stu-id="fa149-140">The values of the variables that you just changed are updated in the **Locals** window.</span></span>

   :::image type="content" source="media/debugging-with-visual-studio-mac/locals-window.png" alt-text="Okno zmiennych lokalnych w programie Visual Studio":::

1. <span data-ttu-id="fa149-142">Naciśnij pozycję <kbd>⌘</kbd><kbd>↵</kbd> (<kbd>command</kbd> + <kbd>wprowadź</kbd>polecenie), aby kontynuować debugowanie.</span><span class="sxs-lookup"><span data-stu-id="fa149-142">Press <kbd>⌘</kbd><kbd>↵</kbd> (<kbd>command</kbd>+<kbd>enter</kbd>) to continue debugging.</span></span>

   <span data-ttu-id="fa149-143">Wartości wyświetlane w terminalu odpowiadają zmianom wprowadzonym w oknie **bezpośrednim** .</span><span class="sxs-lookup"><span data-stu-id="fa149-143">The values displayed in the terminal correspond to the changes you made in the **Immediate** window.</span></span>

   <span data-ttu-id="fa149-144">Jeśli nie widzisz terminalu, wybierz pozycję **Terminal — HelloWorld** na dolnym pasku nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="fa149-144">If you don't see the Terminal, select **Terminal - HelloWorld** in the bottom navigation bar.</span></span>

   :::image type="content" source="media/debugging-with-visual-studio-mac/terminal-hello-world.png" alt-text="Hello world terminalu na dolnym pasku nawigacyjnym":::

1. <span data-ttu-id="fa149-146">Naciśnij dowolny klawisz, aby zakończyć program.</span><span class="sxs-lookup"><span data-stu-id="fa149-146">Press any key to exit the program.</span></span>

1. <span data-ttu-id="fa149-147">Zamknij okno terminalu.</span><span class="sxs-lookup"><span data-stu-id="fa149-147">Close the terminal window.</span></span>

## <a name="set-a-conditional-breakpoint"></a><span data-ttu-id="fa149-148">Ustaw punkt przerwania warunkowego</span><span class="sxs-lookup"><span data-stu-id="fa149-148">Set a conditional breakpoint</span></span>

<span data-ttu-id="fa149-149">Program wyświetla ciąg wprowadzony przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fa149-149">The program displays a string that the user enters.</span></span> <span data-ttu-id="fa149-150">Co się stanie, jeśli użytkownik nie wprowadzi niczego?</span><span class="sxs-lookup"><span data-stu-id="fa149-150">What happens if the user doesn't enter anything?</span></span> <span data-ttu-id="fa149-151">Można to sprawdzić za pomocą przydatnej funkcji debugowania zwanej *warunkowym punktem przerwania*.</span><span class="sxs-lookup"><span data-stu-id="fa149-151">You can test this with a useful debugging feature called a *conditional breakpoint*.</span></span>

1. <span data-ttu-id="fa149-152"><kbd>naciśnij klawisz Ctrl</kbd>i kliknij czerwoną kropkę, która reprezentuje punkt przerwania.</span><span class="sxs-lookup"><span data-stu-id="fa149-152"><kbd>ctrl</kbd>-click on the red dot that represents the breakpoint.</span></span> <span data-ttu-id="fa149-153">W menu kontekstowym wybierz polecenie **Edytuj punkt przerwania**.</span><span class="sxs-lookup"><span data-stu-id="fa149-153">In the context menu, select **Edit Breakpoint**.</span></span>

1. <span data-ttu-id="fa149-154">W oknie dialogowym **Edytowanie punktu przerwania** wprowadź następujący kod w poniższym polu **i następujący warunek jest spełniony**, a następnie wybierz pozycję **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="fa149-154">In the **Edit Breakpoint** dialog, enter the following code in the field that follows **And the following condition is true**, and select **Apply**.</span></span>

   ```csharp
   String.IsNullOrEmpty(name)
   ```

   :::image type="content" source="media/debugging-with-visual-studio-mac/breakpoint-settings.png" alt-text="Edytor przedstawiający panel ustawień punktu przerwania":::

   <span data-ttu-id="fa149-156">Za każdym razem, gdy punkt przerwania został trafiony, debuger wywołuje `String.IsNullOrEmpty(name)` metodę i przerywa w tym wierszu tylko wtedy, gdy wywołanie metody zwróci wartość `true` .</span><span class="sxs-lookup"><span data-stu-id="fa149-156">Each time the breakpoint is hit, the debugger calls the `String.IsNullOrEmpty(name)` method, and it breaks on this line only if the method call returns `true`.</span></span>

   <span data-ttu-id="fa149-157">Zamiast wyrażenia warunkowego można określić *liczbę trafień*, która przerywa wykonywanie programu, zanim instrukcja zostanie wykonana określoną liczbę razy.</span><span class="sxs-lookup"><span data-stu-id="fa149-157">Instead of a conditional expression, you can specify a *hit count*, which interrupts program execution before a statement is executed a specified number of times.</span></span>

1. <span data-ttu-id="fa149-158">Naciśnij pozycję <kbd>⌘</kbd><kbd>↵</kbd> (<kbd>command</kbd> + <kbd>wprowadź</kbd>polecenie), aby rozpocząć debugowanie.</span><span class="sxs-lookup"><span data-stu-id="fa149-158">Press <kbd>⌘</kbd><kbd>↵</kbd> (<kbd>command</kbd>+<kbd>enter</kbd>) to start debugging.</span></span>

1. <span data-ttu-id="fa149-159">W oknie terminalu naciśnij klawisz <kbd>Enter</kbd> po wyświetleniu monitu o wprowadzenie nazwy.</span><span class="sxs-lookup"><span data-stu-id="fa149-159">In the terminal window, press <kbd>enter</kbd> when prompted to enter your name.</span></span>

   <span data-ttu-id="fa149-160">Ponieważ określony warunek ( `name` is `null` lub <xref:System.String.Empty?displayProperty=nameWithType> ) został spełniony, wykonanie programu zatrzyma się po osiągnięciu punktu przerwania.</span><span class="sxs-lookup"><span data-stu-id="fa149-160">Because the condition you specified (`name` is either `null` or <xref:System.String.Empty?displayProperty=nameWithType>) has been satisfied, program execution stops when it reaches the breakpoint.</span></span>

1. <span data-ttu-id="fa149-161">Wybierz okno zmienne **lokalne** , które pokazuje wartości zmiennych, które są lokalne dla aktualnie wykonywanej metody.</span><span class="sxs-lookup"><span data-stu-id="fa149-161">Select the **Locals** window, which shows the values of variables that are local to the currently executing method.</span></span> <span data-ttu-id="fa149-162">W tym przypadku `Main` jest obecnie wykonywana metoda.</span><span class="sxs-lookup"><span data-stu-id="fa149-162">In this case, `Main` is the currently executing method.</span></span> <span data-ttu-id="fa149-163">Zwróć uwagę, że wartość `name` zmiennej to `""` <xref:System.String.Empty?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="fa149-163">Observe that the value of the `name` variable is `""`, that is, <xref:System.String.Empty?displayProperty=nameWithType>.</span></span>

1. <span data-ttu-id="fa149-164">Możesz również sprawdzić, czy wartość jest pustym ciągiem, wprowadzając `name` nazwę zmiennej w oknie **bezpośrednim** i naciskając klawisz <kbd>Enter</kbd>.</span><span class="sxs-lookup"><span data-stu-id="fa149-164">You can also see that the value is an empty string by entering the `name` variable name in the **Immediate** window and pressing <kbd>enter</kbd>.</span></span>

   :::image type="content" source="media/debugging-with-visual-studio-mac/immediate-window-output.png" alt-text="Bezpośrednie okno pokazujące nazwę jest pustym ciągiem":::

1. <span data-ttu-id="fa149-166">Naciśnij pozycję <kbd>⌘</kbd><kbd>↵</kbd> (<kbd>command</kbd> + <kbd>wprowadź</kbd>polecenie), aby kontynuować debugowanie.</span><span class="sxs-lookup"><span data-stu-id="fa149-166">Press <kbd>⌘</kbd><kbd>↵</kbd> (<kbd>command</kbd>+<kbd>enter</kbd>) to continue debugging.</span></span>

1. <span data-ttu-id="fa149-167">W oknie terminalu naciśnij dowolny klawisz, aby wyjść z programu.</span><span class="sxs-lookup"><span data-stu-id="fa149-167">In the terminal window, press any key to exit the program.</span></span>

1. <span data-ttu-id="fa149-168">Zamknij okno terminalu.</span><span class="sxs-lookup"><span data-stu-id="fa149-168">Close the terminal window.</span></span>

1. <span data-ttu-id="fa149-169">Wyczyść punkt przerwania, klikając czerwoną kropkę na lewym marginesie okna kod.</span><span class="sxs-lookup"><span data-stu-id="fa149-169">Clear the breakpoint by clicking on the red dot in the left margin of the code window.</span></span> <span data-ttu-id="fa149-170">Innym sposobem na wyczyszczenie punktu przerwania jest wybranie opcji **uruchom > Przełącz punkt przerwania** , gdy zostanie wybrany wiersz kodu.</span><span class="sxs-lookup"><span data-stu-id="fa149-170">Another way to clear a breakpoint is by choosing **Run > Toggle Breakpoint** while the line of code is selected.</span></span>

## <a name="step-through-a-program"></a><span data-ttu-id="fa149-171">Przechodzenie przez program</span><span class="sxs-lookup"><span data-stu-id="fa149-171">Step through a program</span></span>

<span data-ttu-id="fa149-172">Program Visual Studio umożliwia również krok po kroku w wierszu przez program i monitorowanie jego wykonania.</span><span class="sxs-lookup"><span data-stu-id="fa149-172">Visual Studio also allows you to step line by line through a program and monitor its execution.</span></span> <span data-ttu-id="fa149-173">Zwykle ustawiasz punkt przerwania i obserwuj przepływ programu za pomocą niewielkiej części kodu programu.</span><span class="sxs-lookup"><span data-stu-id="fa149-173">Ordinarily, you'd set a breakpoint and follow program flow through a small part of your program code.</span></span> <span data-ttu-id="fa149-174">Ponieważ ten program jest mały, możesz przejść przez cały program.</span><span class="sxs-lookup"><span data-stu-id="fa149-174">Since this program is small, you can step through the entire program.</span></span>

1. <span data-ttu-id="fa149-175">Ustaw punkt przerwania w nawiasach klamrowych, który oznacza początek `Main` metody (naciśnięcie <kbd>polecenia</kbd> + <kbd>\\</kbd> ).</span><span class="sxs-lookup"><span data-stu-id="fa149-175">Set a breakpoint on the curly brace that marks the start of the `Main` method (press <kbd>command</kbd>+<kbd>\\</kbd>).</span></span>

1. <span data-ttu-id="fa149-176">Naciśnij pozycję <kbd>⌘</kbd><kbd>↵</kbd> (<kbd>command</kbd> + <kbd>wprowadź</kbd>polecenie), aby rozpocząć debugowanie.</span><span class="sxs-lookup"><span data-stu-id="fa149-176">Press <kbd>⌘</kbd><kbd>↵</kbd> (<kbd>command</kbd>+<kbd>enter</kbd>) to start debugging.</span></span>

   <span data-ttu-id="fa149-177">Program Visual Studio przestaje działać w wierszu z punktem przerwania.</span><span class="sxs-lookup"><span data-stu-id="fa149-177">Visual Studio stops on the line with the breakpoint.</span></span>

1. <span data-ttu-id="fa149-178">Naciśnij <kbd>⇧</kbd><kbd>⌘</kbd><kbd>I</kbd> (<kbd>SHIFT</kbd> + <kbd>Command</kbd> + <kbd>i</kbd>) lub wybierz pozycję **Uruchom**  >  **krok** do góry, aby przejść do wiersza.</span><span class="sxs-lookup"><span data-stu-id="fa149-178">Press <kbd>⇧</kbd><kbd>⌘</kbd><kbd>I</kbd> (<kbd>shift</kbd>+<kbd>command</kbd>+<kbd>I</kbd>) or select **Run** > **Step Into** to advance one line.</span></span>

   <span data-ttu-id="fa149-179">Program Visual Studio podświetla i wyświetli strzałkę obok następnego wiersza wykonania.</span><span class="sxs-lookup"><span data-stu-id="fa149-179">Visual Studio highlights and displays an arrow beside the next line of execution.</span></span>

   :::image type="content" source="media/debugging-with-visual-studio-mac/step-into-method.png" alt-text="Visual Studio — Wkrocz do metody":::

   <span data-ttu-id="fa149-181">W tym momencie okno zmienne **lokalne** pokazuje, że `args` Tablica jest pusta i `name` i `date` ma wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="fa149-181">At this point, the **Locals** window shows that the `args` array is empty, and `name` and `date` have default values.</span></span> <span data-ttu-id="fa149-182">Ponadto program Visual Studio otworzył pusty Terminal.</span><span class="sxs-lookup"><span data-stu-id="fa149-182">In addition, Visual Studio has opened a blank terminal.</span></span>

1. <span data-ttu-id="fa149-183">Naciśnij pozycję <kbd>⇧</kbd><kbd>⌘</kbd><kbd>i</kbd> (<kbd>SHIFT</kbd> + <kbd>Command</kbd> + <kbd>i</kbd>).</span><span class="sxs-lookup"><span data-stu-id="fa149-183">Press <kbd>⇧</kbd><kbd>⌘</kbd><kbd>I</kbd> (<kbd>shift</kbd>+<kbd>command</kbd>+<kbd>I</kbd>).</span></span>

   <span data-ttu-id="fa149-184">Program Visual Studio podświetla instrukcję, która zawiera `name` przypisanie zmiennej.</span><span class="sxs-lookup"><span data-stu-id="fa149-184">Visual Studio highlights the statement that includes the `name` variable assignment.</span></span> <span data-ttu-id="fa149-185">W oknie **Ustawienia lokalne** zostanie wyświetlona `name` wartość `null` , a w terminalu zostanie wyświetlony ciąg "co to jest Twoja nazwa?".</span><span class="sxs-lookup"><span data-stu-id="fa149-185">The **Locals** window shows that `name` is `null`, and the terminal displays the string "What is your name?".</span></span>

1. <span data-ttu-id="fa149-186">Odpowiedz na monit, wprowadzając ciąg w oknie konsoli i naciskając klawisz <kbd>Enter</kbd>.</span><span class="sxs-lookup"><span data-stu-id="fa149-186">Respond to the prompt by entering a string in the console window and pressing <kbd>enter</kbd>.</span></span>

1. <span data-ttu-id="fa149-187">Naciśnij pozycję <kbd>⇧</kbd><kbd>⌘</kbd><kbd>i</kbd> (<kbd>SHIFT</kbd> + <kbd>Command</kbd> + <kbd>i</kbd>).</span><span class="sxs-lookup"><span data-stu-id="fa149-187">Press <kbd>⇧</kbd><kbd>⌘</kbd><kbd>I</kbd> (<kbd>shift</kbd>+<kbd>command</kbd>+<kbd>I</kbd>).</span></span>

   <span data-ttu-id="fa149-188">Program Visual Studio podświetla instrukcję, która zawiera `date` przypisanie zmiennej.</span><span class="sxs-lookup"><span data-stu-id="fa149-188">Visual Studio highlights the statement that includes the `date` variable assignment.</span></span> <span data-ttu-id="fa149-189">Okno zmienne **lokalne** pokazuje wartość zwracaną przez wywołanie <xref:System.Console.ReadLine%2A?displayProperty=nameWithType> metody.</span><span class="sxs-lookup"><span data-stu-id="fa149-189">The **Locals** window shows the value returned by the call to the <xref:System.Console.ReadLine%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="fa149-190">Terminal wyświetla ciąg wprowadzony w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="fa149-190">The terminal displays the string you entered at the prompt.</span></span>

1. <span data-ttu-id="fa149-191">Naciśnij pozycję <kbd>⇧</kbd><kbd>⌘</kbd><kbd>i</kbd> (<kbd>SHIFT</kbd> + <kbd>Command</kbd> + <kbd>i</kbd>).</span><span class="sxs-lookup"><span data-stu-id="fa149-191">Press <kbd>⇧</kbd><kbd>⌘</kbd><kbd>I</kbd> (<kbd>shift</kbd>+<kbd>command</kbd>+<kbd>I</kbd>).</span></span>

   <span data-ttu-id="fa149-192">Okno **lokalne** pokazuje wartość `date` zmiennej po przypisaniu z <xref:System.DateTime.Now?displayProperty=nameWithType> właściwości.</span><span class="sxs-lookup"><span data-stu-id="fa149-192">The **Locals** window shows the value of the `date` variable after the assignment from the <xref:System.DateTime.Now?displayProperty=nameWithType> property.</span></span> <span data-ttu-id="fa149-193">Terminal nie jest zmieniany.</span><span class="sxs-lookup"><span data-stu-id="fa149-193">The terminal is unchanged.</span></span>

1. <span data-ttu-id="fa149-194">Naciśnij pozycję <kbd>⇧</kbd><kbd>⌘</kbd><kbd>i</kbd> (<kbd>SHIFT</kbd> + <kbd>Command</kbd> + <kbd>i</kbd>).</span><span class="sxs-lookup"><span data-stu-id="fa149-194">Press <kbd>⇧</kbd><kbd>⌘</kbd><kbd>I</kbd> (<kbd>shift</kbd>+<kbd>command</kbd>+<kbd>I</kbd>).</span></span>

   <span data-ttu-id="fa149-195">Program Visual Studio wywołuje <xref:System.Console.WriteLine(System.String,System.Object,System.Object)?displayProperty=nameWithType> metodę.</span><span class="sxs-lookup"><span data-stu-id="fa149-195">Visual Studio calls the <xref:System.Console.WriteLine(System.String,System.Object,System.Object)?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="fa149-196">Terminal wyświetla sformatowany ciąg.</span><span class="sxs-lookup"><span data-stu-id="fa149-196">The terminal displays the formatted string.</span></span>

1. <span data-ttu-id="fa149-197">Naciśnij <kbd>⇧</kbd><kbd>⌘</kbd><kbd>U</kbd> (<kbd>SHIFT</kbd> + <kbd>Command</kbd> + <kbd>u</kbd>) lub wybierz opcję **Run**  >  **Wyjdź out**.</span><span class="sxs-lookup"><span data-stu-id="fa149-197">Press <kbd>⇧</kbd><kbd>⌘</kbd><kbd>U</kbd> (<kbd>shift</kbd>+<kbd>command</kbd>+<kbd>U</kbd>) or select **Run** > **Step Out**.</span></span>

   <span data-ttu-id="fa149-198">Terminal wyświetla komunikat i czeka na naciśnięcie klawisza.</span><span class="sxs-lookup"><span data-stu-id="fa149-198">The terminal displays a message and waits for you to press a key.</span></span>

1. <span data-ttu-id="fa149-199">Naciśnij dowolny klawisz, aby zakończyć program.</span><span class="sxs-lookup"><span data-stu-id="fa149-199">Press any key to exit the program.</span></span>

## <a name="use-release-build-configuration"></a><span data-ttu-id="fa149-200">Użyj konfiguracji kompilacji wydania</span><span class="sxs-lookup"><span data-stu-id="fa149-200">Use Release build configuration</span></span>

<span data-ttu-id="fa149-201">Po przetestowaniu wersji debugowania aplikacji należy również skompilować i przetestować wersję publikacji.</span><span class="sxs-lookup"><span data-stu-id="fa149-201">Once you've tested the Debug version of your application, you should also compile and test the Release version.</span></span> <span data-ttu-id="fa149-202">Wersja wydania obejmuje optymalizacje kompilatora, które mogą negatywnie wpłynąć na zachowanie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fa149-202">The Release version incorporates compiler optimizations that can negatively affect the behavior of an application.</span></span> <span data-ttu-id="fa149-203">Na przykład optymalizacje kompilatora, które mają na celu poprawę wydajności, mogą tworzyć sytuacje wyścigu w aplikacjach wielowątkowych.</span><span class="sxs-lookup"><span data-stu-id="fa149-203">For example, compiler optimizations that are designed to improve performance can create race conditions in multithreaded applications.</span></span>

<span data-ttu-id="fa149-204">Aby skompilować i przetestować wydaną wersję aplikacji konsolowej, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fa149-204">To build and test the Release version of the console application, do the following steps:</span></span>

1. <span data-ttu-id="fa149-205">Zmień konfigurację kompilacji na pasku narzędzi z **Debuguj** do **Release**.</span><span class="sxs-lookup"><span data-stu-id="fa149-205">Change the build configuration on the toolbar from **Debug** to **Release**.</span></span>

   :::image type="content" source="media/debugging-with-visual-studio-mac/visual-studio-toolbar-release.png" alt-text="domyślny pasek narzędzi programu Visual Studio z wyróżnioną pozycją Debug":::

1. <span data-ttu-id="fa149-207">Naciśnij pozycję <kbd>⌥</kbd><kbd>⌘</kbd><kbd>↵</kbd> (<kbd>Option</kbd> + <kbd>Command</kbd> + <kbd>Enter</kbd>), aby uruchomić bez debugowania.</span><span class="sxs-lookup"><span data-stu-id="fa149-207">Press <kbd>⌥</kbd><kbd>⌘</kbd><kbd>↵</kbd> (<kbd>option</kbd>+<kbd>command</kbd>+<kbd>enter</kbd>) to run without debugging.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa149-208">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fa149-208">Next steps</span></span>

<span data-ttu-id="fa149-209">W tym samouczku użyto narzędzi debugowania programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fa149-209">In this tutorial, you used Visual Studio debugging tools.</span></span> <span data-ttu-id="fa149-210">W następnym samouczku zostanie opublikowana wersja aplikacji, którą można wdrożyć.</span><span class="sxs-lookup"><span data-stu-id="fa149-210">In the next tutorial, you publish a deployable version of the app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fa149-211">Publikowanie aplikacji konsolowej .NET przy użyciu Visual Studio dla komputerów Mac</span><span class="sxs-lookup"><span data-stu-id="fa149-211">Publish a .NET console application using Visual Studio for Mac</span></span>](publishing-with-visual-studio-mac.md)
