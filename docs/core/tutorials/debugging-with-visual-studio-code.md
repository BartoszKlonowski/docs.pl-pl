---
title: Debugowanie aplikacji konsolowej .NET Core przy użyciu Visual Studio Code
description: Dowiedz się, jak debugować aplikację konsolową .NET Core przy użyciu Visual Studio Code.
ms.date: 05/26/2020
ms.openlocfilehash: 40e9b114df1bd12fb05bfb773781d6009d087a06
ms.sourcegitcommit: 1cbd77da54405ea7dba343ac0334fb03237d25d2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/11/2020
ms.locfileid: "84702130"
---
# <a name="tutorial-debug-a-net-core-console-application-using-visual-studio-code"></a><span data-ttu-id="fbfb1-103">Samouczek: debugowanie aplikacji konsolowej .NET Core przy użyciu Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="fbfb1-103">Tutorial: Debug a .NET Core console application using Visual Studio Code</span></span>

<span data-ttu-id="fbfb1-104">W tym samouczku przedstawiono narzędzia debugowania dostępne w Visual Studio Code do pracy z aplikacjami .NET Core.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-104">This tutorial introduces the debugging tools available in Visual Studio Code for working with .NET Core apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fbfb1-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fbfb1-105">Prerequisites</span></span>

- <span data-ttu-id="fbfb1-106">Ten samouczek współpracuje z aplikacją konsolową utworzoną w temacie [Tworzenie aplikacji konsolowej platformy .NET Core w Visual Studio Code](with-visual-studio-code.md).</span><span class="sxs-lookup"><span data-stu-id="fbfb1-106">This tutorial works with the console app that you create in [Create a .NET Core console application in Visual Studio Code](with-visual-studio-code.md).</span></span>

## <a name="use-debug-build-configuration"></a><span data-ttu-id="fbfb1-107">Użyj konfiguracji kompilacji debugowania</span><span class="sxs-lookup"><span data-stu-id="fbfb1-107">Use Debug build configuration</span></span>

<span data-ttu-id="fbfb1-108">*Debugowanie* i *wydanie* to wbudowane konfiguracje kompilacji platformy .NET Core.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-108">*Debug* and *Release* are .NET Core's built-in build configurations.</span></span> <span data-ttu-id="fbfb1-109">Konfiguracja kompilacji debugowania umożliwia debugowanie i konfigurację wydania dla ostatecznej dystrybucji wersji.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-109">You use the Debug build configuration for debugging and the Release configuration for the final release distribution.</span></span>

<span data-ttu-id="fbfb1-110">W konfiguracji debugowania program kompiluje z pełnymi symbolicznymi informacjami o debugowaniu i bez optymalizacji.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-110">In the Debug configuration, a program compiles with full symbolic debug information and no optimization.</span></span> <span data-ttu-id="fbfb1-111">Optymalizacja komplikuje debugowanie, ponieważ relacja między kodem źródłowym i wygenerowanymi instrukcjami jest bardziej skomplikowana.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-111">Optimization complicates debugging, because the relationship between source code and generated instructions is more complex.</span></span> <span data-ttu-id="fbfb1-112">Konfiguracja wydania programu nie ma symbolicznych informacji o debugowaniu i jest w pełni zoptymalizowana.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-112">The release configuration of a program has no symbolic debug information and is fully optimized.</span></span>

<span data-ttu-id="fbfb1-113">Domyślnie ustawienia uruchamiania Visual Studio Code używają konfiguracji kompilacji debugowania, więc nie trzeba jej zmieniać przed debugowaniem.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-113">By default, Visual Studio Code launch settings use the Debug build configuration, so you don't need to change it before debugging.</span></span>

1. <span data-ttu-id="fbfb1-114">Uruchom program Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-114">Start Visual Studio Code.</span></span>

1. <span data-ttu-id="fbfb1-115">Otwórz folder projektu, który został utworzony w temacie [Tworzenie aplikacji konsolowej platformy .NET Core w Visual Studio Code](with-visual-studio-code.md).</span><span class="sxs-lookup"><span data-stu-id="fbfb1-115">Open the folder of the project that you created in [Create a .NET Core console application in Visual Studio Code](with-visual-studio-code.md).</span></span>

## <a name="set-a-breakpoint"></a><span data-ttu-id="fbfb1-116">Ustawianie punktu przerwania</span><span class="sxs-lookup"><span data-stu-id="fbfb1-116">Set a breakpoint</span></span>

<span data-ttu-id="fbfb1-117">*Punkt przerwania* tymczasowo przerywa wykonywanie aplikacji przed wykonaniem wiersza z punktem przerwania.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-117">A *breakpoint* temporarily interrupts the execution of the application before the line with the breakpoint is executed.</span></span>

1. <span data-ttu-id="fbfb1-118">Otwórz plik *program.cs* .</span><span class="sxs-lookup"><span data-stu-id="fbfb1-118">Open the *Program.cs* file.</span></span>

1. <span data-ttu-id="fbfb1-119">Ustaw *punkt przerwania* w wierszu, który wyświetla nazwę, datę i godzinę, klikając na lewym marginesie okna kod.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-119">Set a *breakpoint* on the line that displays the name, date, and time, by clicking in the left margin of the code window.</span></span> <span data-ttu-id="fbfb1-120">Lewy margines znajduje się po lewej stronie numerów wierszy.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-120">The left margin is to the left of the line numbers.</span></span> <span data-ttu-id="fbfb1-121">Innymi sposobami ustawiania punktu przerwania są naciśnięcie klawisza <kbd>F9</kbd> lub wybranie opcji **Uruchom**  >  **przełączanie punktu przerwania** z menu podczas wybierania wiersza kodu.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-121">Other ways to set a breakpoint are by pressing <kbd>F9</kbd> or selecting **Run** > **Toggle Breakpoint** from the menu while the line of code is selected.</span></span>

   <span data-ttu-id="fbfb1-122">Visual Studio Code wskazuje wiersz, w którym jest ustawiony punkt przerwania, wyświetlając czerwoną kropkę na lewym marginesie.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-122">Visual Studio Code indicates the line on which the breakpoint is set by displaying a red dot in the left margin.</span></span>

   :::image type="content" source="media/debugging-with-visual-studio-code/breakpoint-set.png" alt-text="Zestaw punktów przerwania":::

## <a name="set-up-for-terminal-input"></a><span data-ttu-id="fbfb1-124">Konfiguracja dla danych wejściowych terminalu</span><span class="sxs-lookup"><span data-stu-id="fbfb1-124">Set up for terminal input</span></span>

<span data-ttu-id="fbfb1-125">Punkt przerwania znajduje się po `Console.ReadLine` wywołaniu metody.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-125">The breakpoint is located after a `Console.ReadLine` method call.</span></span> <span data-ttu-id="fbfb1-126">**Konsola debugowania** nie akceptuje danych wejściowych terminalu dla uruchomionego programu.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-126">The **Debug Console** doesn't accept terminal input for a running program.</span></span> <span data-ttu-id="fbfb1-127">Aby obsłużyć dane wejściowe terminalu podczas debugowania, można użyć zintegrowanego terminalu (jednego z Visual Studio Code systemu Windows) lub terminalu zewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-127">To handle terminal input while debugging, you can use the integrated terminal (one of the Visual Studio Code windows) or an external terminal.</span></span> <span data-ttu-id="fbfb1-128">W tym samouczku użyjesz zintegrowanego terminalu.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-128">For this tutorial, you use the integrated terminal.</span></span>

1. <span data-ttu-id="fbfb1-129">Otwórz *. programu vscode/launch.jsw systemie*.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-129">Open *.vscode/launch.json*.</span></span>

1. <span data-ttu-id="fbfb1-130">Zmień `console` ustawienie na `integratedTerminal` .</span><span class="sxs-lookup"><span data-stu-id="fbfb1-130">Change the `console` setting to `integratedTerminal`.</span></span>

   <span data-ttu-id="fbfb1-131">Od:</span><span class="sxs-lookup"><span data-stu-id="fbfb1-131">From:</span></span>

   ```
   "console": "internalConsole",
   ```

   <span data-ttu-id="fbfb1-132">Do:</span><span class="sxs-lookup"><span data-stu-id="fbfb1-132">To:</span></span>

   ```
   "console": "integratedTerminal",
   ```

1. <span data-ttu-id="fbfb1-133">Zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-133">Save your changes.</span></span>

## <a name="start-debugging"></a><span data-ttu-id="fbfb1-134">Rozpocznij debugowanie</span><span class="sxs-lookup"><span data-stu-id="fbfb1-134">Start debugging</span></span>

1. <span data-ttu-id="fbfb1-135">Otwórz widok debugowanie, wybierając ikonę debugowania w menu po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-135">Open the Debug view by selecting the Debugging icon on the left side menu.</span></span>

   :::image type="content" source="media/debugging-with-visual-studio-code/select-debug-pane.png" alt-text="Otwórz kartę debugowanie w Visual Studio Code":::

1. <span data-ttu-id="fbfb1-137">Wybierz zieloną strzałkę w górnej części okienka, obok pozycji **.NET Core Launch (konsola)**.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-137">Select the green arrow at the top of the pane, next to **.NET Core Launch (console)**.</span></span> <span data-ttu-id="fbfb1-138">Innym sposobem uruchomienia programu w trybie debugowania jest wybranie polecenia **Uruchom**  >  **debugowanie** z menu.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-138">Another way to start the program in debugging mode is by choosing **Run** > **Start Debugging** from the menu.</span></span>

   :::image type="content" source="media/debugging-with-visual-studio-code/start-debugging.png" alt-text="Rozpocznij debugowanie":::

1. <span data-ttu-id="fbfb1-140">Wybierz kartę **Terminal** , aby zobaczyć "Jaka jest Twoja nazwa?".</span><span class="sxs-lookup"><span data-stu-id="fbfb1-140">Select the **Terminal** tab to see the "What is your name?"</span></span> <span data-ttu-id="fbfb1-141">Monituj o wyświetlenie programu przed oczekiwaniem na odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-141">prompt that the program displays before waiting for a response.</span></span>

   :::image type="content" source="media/debugging-with-visual-studio-code/select-terminal.png" alt-text="Wybierz kartę Terminal":::

1. <span data-ttu-id="fbfb1-143">Wprowadź ciąg w oknie **terminalu** w odpowiedzi na monit o podanie nazwy, a następnie naciśnij klawisz <kbd>Enter</kbd>.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-143">Enter a string in the **Terminal** window in response to the prompt for a name, and then press <kbd>Enter</kbd>.</span></span>

   <span data-ttu-id="fbfb1-144">Wykonanie programu zostaje zatrzymane po osiągnięciu punktu przerwania i przed wykonaniem `Console.WriteLine` metody.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-144">Program execution stops when it reaches the breakpoint and before the `Console.WriteLine` method executes.</span></span> <span data-ttu-id="fbfb1-145">Sekcja **locales** w oknie **zmienne** zawiera wartości zmiennych, które są zdefiniowane w aktualnie wykonywanej metodzie.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-145">The **Locals** section of the **Variables** window displays the values of variables that are defined in the currently executing method.</span></span>

   :::image type="content" source="media/debugging-with-visual-studio-code/breakpoint-hit.png" alt-text="Trafienie punktu przerwania, Wyświetlanie ustawień lokalnych":::

## <a name="use-the-debug-console"></a><span data-ttu-id="fbfb1-147">Korzystanie z konsoli debugowania</span><span class="sxs-lookup"><span data-stu-id="fbfb1-147">Use the Debug Console</span></span>

<span data-ttu-id="fbfb1-148">Okno **konsoli debugowania** umożliwia korzystanie z debugowanej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-148">The **Debug Console** window lets you interact with the application you're debugging.</span></span> <span data-ttu-id="fbfb1-149">Można zmienić wartość zmiennych, aby zobaczyć, jak ma to wpływ na program.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-149">You can change the value of variables to see how it affects your program.</span></span>

1. <span data-ttu-id="fbfb1-150">Wybierz kartę **konsola debugowania** .</span><span class="sxs-lookup"><span data-stu-id="fbfb1-150">Select the **Debug Console** tab.</span></span>

1. <span data-ttu-id="fbfb1-151">Wprowadź `name = "Gracie"` w wierszu polecenia u dołu okna **konsoli debugowania** i naciśnij klawisz <kbd>Enter</kbd> .</span><span class="sxs-lookup"><span data-stu-id="fbfb1-151">Enter `name = "Gracie"` at the prompt at the bottom of the **Debug Console** window and press the <kbd>Enter</kbd> key.</span></span>

   :::image type="content" source="media/debugging-with-visual-studio-code/change-variable-values.png" alt-text="Zmień wartości zmiennych":::

1. <span data-ttu-id="fbfb1-153">Wprowadź `date = DateTime.Parse("2019-11-16T17:25:00Z").ToUniversalTime()` w dolnej części okna **konsoli debugowania** i naciśnij klawisz <kbd>Enter</kbd> .</span><span class="sxs-lookup"><span data-stu-id="fbfb1-153">Enter `date = DateTime.Parse("2019-11-16T17:25:00Z").ToUniversalTime()` at the bottom of the **Debug Console** window and press the <kbd>Enter</kbd> key.</span></span>

   <span data-ttu-id="fbfb1-154">W oknie **zmienne** są wyświetlane nowe wartości `name` `date` zmiennych i.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-154">The **Variables** window displays the new values of the `name` and `date` variables.</span></span>

1. <span data-ttu-id="fbfb1-155">Kontynuuj wykonywanie programu, wybierając przycisk **Kontynuuj** na pasku narzędzi.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-155">Continue program execution by selecting the **Continue** button in the toolbar.</span></span> <span data-ttu-id="fbfb1-156">Innym sposobem, aby kontynuować, jest naciśnięcie klawisza <kbd>F5</kbd>.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-156">Another way to continue is by pressing <kbd>F5</kbd>.</span></span>

   :::image type="content" source="media/debugging-with-visual-studio-code/continue-debugging.png" alt-text="Kontynuuj debugowanie":::

1. <span data-ttu-id="fbfb1-158">Ponownie wybierz kartę **terminala** .</span><span class="sxs-lookup"><span data-stu-id="fbfb1-158">Select the **Terminal** tab again.</span></span>

   <span data-ttu-id="fbfb1-159">Wartości wyświetlane w oknie konsoli odpowiadają zmianom wprowadzonym w **konsoli debugowania**.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-159">The values displayed in the console window correspond to the changes you made in the **Debug Console**.</span></span>

   :::image type="content" source="media/debugging-with-visual-studio-code/changed-variable-values.png" alt-text="Terminal pokazujący wprowadzone wartości":::

1. <span data-ttu-id="fbfb1-161">Naciśnij dowolny klawisz, aby zamknąć aplikację i zatrzymać debugowanie.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-161">Press any key to exit the application and stop debugging.</span></span>

## <a name="set-a-conditional-breakpoint"></a><span data-ttu-id="fbfb1-162">Ustaw punkt przerwania warunkowego</span><span class="sxs-lookup"><span data-stu-id="fbfb1-162">Set a conditional breakpoint</span></span>

<span data-ttu-id="fbfb1-163">Program wyświetla ciąg wprowadzony przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-163">The program displays the string that the user enters.</span></span> <span data-ttu-id="fbfb1-164">Co się stanie, jeśli użytkownik nie wprowadzi niczego?</span><span class="sxs-lookup"><span data-stu-id="fbfb1-164">What happens if the user doesn't enter anything?</span></span> <span data-ttu-id="fbfb1-165">Można to sprawdzić za pomocą przydatnej funkcji debugowania zwanej *warunkowym punktem przerwania*.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-165">You can test this with a useful debugging feature called a *conditional breakpoint*.</span></span>

1. <span data-ttu-id="fbfb1-166">Kliknij prawym przyciskiem myszy (<kbd>Ctrl</kbd>-kliknięcie macOS) na czerwoną kropkę reprezentującą punkt przerwania.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-166">Right-click (<kbd>Ctrl</kbd>-click on macOS) on the red dot that represents the breakpoint.</span></span> <span data-ttu-id="fbfb1-167">W menu kontekstowym wybierz pozycję **Edytuj punkt przerwania** , aby otworzyć okno dialogowe, które umożliwia wprowadzenie wyrażenia warunkowego.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-167">In the context menu, select **Edit Breakpoint** to open a dialog that lets you enter a conditional expression.</span></span>

   :::image type="content" source="media/debugging-with-visual-studio-code/breakpoint-context-menu.png" alt-text="Menu kontekstowe punktu przerwania":::

1. <span data-ttu-id="fbfb1-169">Wybierz `Expression` z listy rozwijanej, wprowadź następujące wyrażenie warunkowe, a następnie naciśnij klawisz <kbd>Enter</kbd>.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-169">Select `Expression` in the drop-down, enter the following conditional expression, and press <kbd>Enter</kbd>.</span></span>

   ```csharp
   String.IsNullOrEmpty(name)
   ```

   :::image type="content" source="media/debugging-with-visual-studio-code/conditional-expression.png" alt-text="Wprowadź wyrażenie warunkowe":::

   <span data-ttu-id="fbfb1-171">Za każdym razem, gdy punkt przerwania został trafiony, debuger wywołuje `String.IsNullOrEmpty(name)` metodę i przerywa w tym wierszu tylko wtedy, gdy wywołanie metody zwróci wartość `true` .</span><span class="sxs-lookup"><span data-stu-id="fbfb1-171">Each time the breakpoint is hit, the debugger calls the `String.IsNullOrEmpty(name)` method, and it breaks on this line only if the method call returns `true`.</span></span>

   <span data-ttu-id="fbfb1-172">Zamiast wyrażenia warunkowego można określić *liczbę trafień*, która przerywa wykonywanie programu, zanim instrukcja zostanie wykonana określoną liczbę razy.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-172">Instead of a conditional expression, you can specify a *hit count*, which interrupts program execution before a statement is executed a specified number of times.</span></span> <span data-ttu-id="fbfb1-173">Innym rozwiązaniem jest określenie *warunku filtru*, który przerywa wykonywanie programu w oparciu o takie atrybuty jak identyfikator wątku, nazwa procesu lub nazwa wątku.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-173">Another option is to specify a *filter condition*, which interrupts program execution based on such attributes as a thread identifier, process name, or thread name.</span></span>

1. <span data-ttu-id="fbfb1-174">Uruchom program z debugowaniem, naciskając klawisz <kbd>F5</kbd>.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-174">Start the program with debugging by pressing <kbd>F5</kbd>.</span></span>

1. <span data-ttu-id="fbfb1-175">Na karcie **Terminal** naciśnij klawisz <kbd>Enter</kbd> po wyświetleniu monitu, aby wprowadzić swoją nazwę.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-175">In the **Terminal** tab, press the <kbd>Enter</kbd> key when prompted to enter your name.</span></span>

   <span data-ttu-id="fbfb1-176">Ponieważ określony warunek ( `name` is `null` lub) został <xref:System.String.Empty?displayProperty=nameWithType> spełniony, wykonanie programu zatrzyma się po osiągnięciu punktu przerwania i przed wykonaniem `Console.WriteLine` metody.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-176">Because the condition you specified (`name` is `null` or <xref:System.String.Empty?displayProperty=nameWithType>) has been satisfied, program execution stops when it reaches the breakpoint and before the `Console.WriteLine` method executes.</span></span>

   <span data-ttu-id="fbfb1-177">Okno **zmienne** pokazuje, że wartość `name` zmiennej to `""` , lub <xref:System.String.Empty?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="fbfb1-177">The **Variables** window shows that the value of the `name` variable is `""`, or <xref:System.String.Empty?displayProperty=nameWithType>.</span></span>

1. <span data-ttu-id="fbfb1-178">Potwierdź, że wartość jest pustym ciągiem, wprowadzając poniższą instrukcję w wierszu **konsoli debugowania** i naciskając klawisz <kbd>Enter</kbd>.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-178">Confirm the value is an empty string by entering the following statement at the **Debug Console** prompt and pressing <kbd>Enter</kbd>.</span></span> <span data-ttu-id="fbfb1-179">Wynik to `true` .</span><span class="sxs-lookup"><span data-stu-id="fbfb1-179">The result is `true`.</span></span>

   ```csharp
   name == String.Empty
   ```

   :::image type="content" source="media/debugging-with-visual-studio-code/expression-in-debug-console.png" alt-text="Konsola debugowania zwracająca wartość true po wykonaniu instrukcji":::

1. <span data-ttu-id="fbfb1-181">Wybierz przycisk **Kontynuuj** na pasku narzędzi, aby kontynuować wykonywanie programu.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-181">Select the **Continue** button on the toolbar to continue program execution.</span></span>

1. <span data-ttu-id="fbfb1-182">Wybierz kartę **Terminal** i naciśnij dowolny klawisz, aby wyjść z programu i zatrzymać debugowanie.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-182">Select the **Terminal** tab, and press any key to exit the program and stop debugging.</span></span>

1. <span data-ttu-id="fbfb1-183">Wyczyść punkt przerwania, klikając kropkę na lewym marginesie okna kod.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-183">Clear the breakpoint by clicking on the dot in the left margin of the code window.</span></span> <span data-ttu-id="fbfb1-184">Innymi sposobami czyszczenia punktu przerwania są naciśnięcie klawisza <kbd>F9</kbd> lub wybranie polecenia **Uruchom > Przełącz punkt przerwania** z menu podczas wybierania wiersza kodu.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-184">Other ways to clear a breakpoint are by pressing <kbd>F9</kbd> or choosing **Run > Toggle Breakpoint** from the menu while the line of code is selected.</span></span>

1. <span data-ttu-id="fbfb1-185">Jeśli zostanie wyświetlone ostrzeżenie, że warunek punktu przerwania zostanie utracony, wybierz pozycję **Usuń punkt przerwania**.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-185">If you get a warning that the breakpoint condition will be lost, select **Remove Breakpoint**.</span></span>

## <a name="step-through-a-program"></a><span data-ttu-id="fbfb1-186">Przechodzenie przez program</span><span class="sxs-lookup"><span data-stu-id="fbfb1-186">Step through a program</span></span>

<span data-ttu-id="fbfb1-187">Visual Studio Code umożliwia również krok po kroku w wierszu przez program i monitorowanie jego wykonania.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-187">Visual Studio Code also allows you to step line by line through a program and monitor its execution.</span></span> <span data-ttu-id="fbfb1-188">Zwykle ustawiasz punkt przerwania i obserwuj przepływ programu za pomocą niewielkiej części kodu programu.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-188">Ordinarily, you'd set a breakpoint and follow program flow through a small part of your program code.</span></span> <span data-ttu-id="fbfb1-189">Ponieważ ten program jest mały, możesz przejść przez cały program.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-189">Since this program is small, you can step through the entire program.</span></span>

1. <span data-ttu-id="fbfb1-190">Ustaw punkt przerwania w otwierającym nawiasie klamrowym `Main` metody.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-190">Set a breakpoint on the opening curly brace of the `Main` method.</span></span>

1. <span data-ttu-id="fbfb1-191">Naciśnij klawisz <kbd>F5</kbd>, aby uruchomić debugowanie.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-191">Press <kbd>F5</kbd> to start debugging.</span></span>

   <span data-ttu-id="fbfb1-192">Visual Studio Code podświetla linię punktu przerwania.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-192">Visual Studio Code highlights the breakpoint line.</span></span>

   <span data-ttu-id="fbfb1-193">W tym momencie okno **zmienne** pokazuje, że `args` Tablica jest pusta i `name` i `date` ma wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-193">At this point, the **Variables** window shows that the `args` array is empty, and `name` and `date` have default values.</span></span>

1. <span data-ttu-id="fbfb1-194">Wybierz pozycję **Uruchom**  >  **krok do** lub naciśnij klawisz <kbd>F11</kbd>.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-194">Select **Run** > **Step Into** or press <kbd>F11</kbd>.</span></span>

   :::image type="content" source="media/debugging-with-visual-studio-code/step-into.png" alt-text="Przycisk "krok po kroku"":::

   <span data-ttu-id="fbfb1-196">Visual Studio Code podświetla następny wiersz.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-196">Visual Studio Code highlights the next line.</span></span>

1. <span data-ttu-id="fbfb1-197">Wybierz pozycję **Uruchom**  >  **krok do** lub naciśnij klawisz <kbd>F11</kbd>.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-197">Select **Run** > **Step Into** or press <kbd>F11</kbd>.</span></span>

   <span data-ttu-id="fbfb1-198">Visual Studio Code wykonuje `Console.WriteLine` monit o podanie nazwy i wyróżnia następny wiersz wykonania.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-198">Visual Studio Code executes the `Console.WriteLine` for the name prompt and highlights the next line of execution.</span></span> <span data-ttu-id="fbfb1-199">Następnym wierszem jest `Console.ReadLine` `name` .</span><span class="sxs-lookup"><span data-stu-id="fbfb1-199">The next line is the `Console.ReadLine` for the `name`.</span></span> <span data-ttu-id="fbfb1-200">Okno **zmiennych** jest niezmienione, a na karcie **terminala** zostanie wyświetlona wartość "co to jest Twoja nazwa?"</span><span class="sxs-lookup"><span data-stu-id="fbfb1-200">The **Variables** window is unchanged, and the **Terminal** tab shows the "What is your name?"</span></span> <span data-ttu-id="fbfb1-201">pytać.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-201">prompt.</span></span>

1. <span data-ttu-id="fbfb1-202">Wybierz pozycję **Uruchom**  >  **krok do** lub naciśnij klawisz <kbd>F11</kbd>.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-202">Select **Run** > **Step Into** or press <kbd>F11</kbd>.</span></span>

   <span data-ttu-id="fbfb1-203">Program Visual Studio podświetla `name` przypisanie zmiennej.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-203">Visual Studio highlights the `name` variable assignment.</span></span> <span data-ttu-id="fbfb1-204">Okno **zmienne** pokazuje, że `name` jest nadal `null` .</span><span class="sxs-lookup"><span data-stu-id="fbfb1-204">The **Variables** window shows that `name` is still `null`.</span></span>

1. <span data-ttu-id="fbfb1-205">Odpowiedz na monit, wprowadzając ciąg na karcie Terminal i naciskając klawisz <kbd>Enter</kbd>.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-205">Respond to the prompt by entering a string in the Terminal tab and pressing <kbd>Enter</kbd>.</span></span>

   <span data-ttu-id="fbfb1-206">Na karcie **terminala** może nie być wyświetlany ciąg wprowadzony podczas jego wprowadzania, ale <xref:System.Console.ReadLine%2A?displayProperty=nameWithType> Metoda przechwytuje dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-206">The **Terminal** tab might not display the string you enter while you're entering it, but the <xref:System.Console.ReadLine%2A?displayProperty=nameWithType> method will capture your input.</span></span>

1. <span data-ttu-id="fbfb1-207">Wybierz pozycję **Uruchom**  >  **krok do** lub naciśnij klawisz <kbd>F11</kbd>.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-207">Select **Run** > **Step Into** or press <kbd>F11</kbd>.</span></span>

   <span data-ttu-id="fbfb1-208">Visual Studio Code podświetla `date` przypisanie zmiennej.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-208">Visual Studio Code highlights the `date` variable assignment.</span></span> <span data-ttu-id="fbfb1-209">Okno **zmienne** pokazuje wartość zwracaną przez wywołanie <xref:System.Console.ReadLine%2A?displayProperty=nameWithType> metody.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-209">The **Variables** window shows the value returned by the call to the <xref:System.Console.ReadLine%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="fbfb1-210">Na karcie **Terminal** zostanie wyświetlony ciąg wprowadzony w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-210">The **Terminal** tab displays the string you entered at the prompt.</span></span>

1. <span data-ttu-id="fbfb1-211">Wybierz pozycję **Uruchom**  >  **krok do** lub naciśnij klawisz <kbd>F11</kbd>.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-211">Select **Run** > **Step Into** or press <kbd>F11</kbd>.</span></span>

   <span data-ttu-id="fbfb1-212">Okno **zmienne** zawiera wartość `date` zmiennej po przypisaniu z <xref:System.DateTime.Now?displayProperty=nameWithType> właściwości.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-212">The **Variables** window shows the value of the `date` variable after the assignment from the <xref:System.DateTime.Now?displayProperty=nameWithType> property.</span></span>

1. <span data-ttu-id="fbfb1-213">Wybierz pozycję **Uruchom**  >  **krok do** lub naciśnij klawisz <kbd>F11</kbd>.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-213">Select **Run** > **Step Into** or press <kbd>F11</kbd>.</span></span>

   <span data-ttu-id="fbfb1-214">Visual Studio Code wywołuje <xref:System.Console.WriteLine(System.String,System.Object,System.Object)?displayProperty=nameWithType> metodę.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-214">Visual Studio Code calls the <xref:System.Console.WriteLine(System.String,System.Object,System.Object)?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="fbfb1-215">W oknie konsoli zostanie wyświetlony sformatowany ciąg.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-215">The console window displays the formatted string.</span></span>

1. <span data-ttu-id="fbfb1-216">Wybierz pozycję **Uruchom**  >  **Wyjdź** lub naciśnij klawisz <kbd>SHIFT</kbd> + <kbd>F11</kbd>.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-216">Select **Run** > **Step Out** or press <kbd>Shift</kbd>+<kbd>F11</kbd>.</span></span>

   :::image type="content" source="media/debugging-with-visual-studio-code/step-out.png" alt-text="Przycisk krok po kroku":::

1. <span data-ttu-id="fbfb1-218">Wybierz kartę **Terminal** .</span><span class="sxs-lookup"><span data-stu-id="fbfb1-218">Select the **Terminal** tab.</span></span>

   <span data-ttu-id="fbfb1-219">W terminalu zostanie wyświetlony komunikat "naciśnij dowolny klawisz, aby wyjść..."</span><span class="sxs-lookup"><span data-stu-id="fbfb1-219">The terminal displays "Press any key to exit..."</span></span>

1. <span data-ttu-id="fbfb1-220">Naciśnij dowolny klawisz, aby wyjść z programu.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-220">Press any key to exit the program.</span></span>

## <a name="use-release-build-configuration"></a><span data-ttu-id="fbfb1-221">Użyj konfiguracji kompilacji wydania</span><span class="sxs-lookup"><span data-stu-id="fbfb1-221">Use Release build configuration</span></span>

<span data-ttu-id="fbfb1-222">Po przetestowaniu wersji debugowania aplikacji należy również skompilować i przetestować wersję publikacji.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-222">Once you've tested the Debug version of your application, you should also compile and test the Release version.</span></span> <span data-ttu-id="fbfb1-223">Wersja wydania obejmuje optymalizacje kompilatora, które mogą mieć wpływ na zachowanie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-223">The Release version incorporates compiler optimizations that can affect the behavior of an application.</span></span> <span data-ttu-id="fbfb1-224">Na przykład optymalizacje kompilatora, które mają na celu poprawę wydajności, mogą tworzyć sytuacje wyścigu w aplikacjach wielowątkowych.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-224">For example, compiler optimizations that are designed to improve performance can create race conditions in multithreaded applications.</span></span>

<span data-ttu-id="fbfb1-225">Aby skompilować i przetestować wydaną wersję aplikacji konsolowej, Otwórz **Terminal** i uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="fbfb1-225">To build and test the Release version of your console application, open the **Terminal** and run the following command:</span></span>

```dotnetcli
dotnet run --configuration Release
```

## <a name="additional-resources"></a><span data-ttu-id="fbfb1-226">Zasoby dodatkowe</span><span class="sxs-lookup"><span data-stu-id="fbfb1-226">Additional resources</span></span>

* [<span data-ttu-id="fbfb1-227">Debugowanie w Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="fbfb1-227">Debugging in Visual Studio Code</span></span>](https://code.visualstudio.com/docs/editor/debugging)

## <a name="next-steps"></a><span data-ttu-id="fbfb1-228">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fbfb1-228">Next steps</span></span>

<span data-ttu-id="fbfb1-229">W tym samouczku użyto narzędzi debugowania Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-229">In this tutorial, you used Visual Studio Code debugging tools.</span></span> <span data-ttu-id="fbfb1-230">W następnym samouczku zostanie opublikowana wersja aplikacji, którą można wdrożyć.</span><span class="sxs-lookup"><span data-stu-id="fbfb1-230">In the next tutorial, you publish a deployable version of the app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fbfb1-231">Publikowanie aplikacji konsolowej .NET Core za pomocą Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="fbfb1-231">Publish a .NET Core console application with Visual Studio Code</span></span>](publishing-with-visual-studio-code.md)
