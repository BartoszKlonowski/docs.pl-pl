---
title: 'Instrukcje: Tworzenie przepływu pracy schematu blokowego'
description: W tym artykule opisano tworzenie przepływu pracy korzystającego z wbudowanych działań i działań niestandardowych z poprzedniego artykułu.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 185d7aea-68a6-4bd8-adde-45050f33170a
ms.openlocfilehash: f8e0703591629a72e0a8f6eeb05dd9d19c8c4c91
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96275830"
---
# <a name="how-to-create-a-flowchart-workflow"></a><span data-ttu-id="0359e-103">Instrukcje: Tworzenie przepływu pracy schematu blokowego</span><span class="sxs-lookup"><span data-stu-id="0359e-103">How to: Create a Flowchart Workflow</span></span>

<span data-ttu-id="0359e-104">Przepływy pracy mogą być zbudowane z wbudowanych działań, a także z działań niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="0359e-104">Workflows can be constructed from built-in activities as well as from custom activities.</span></span> <span data-ttu-id="0359e-105">W tym temacie przedstawiono procedurę tworzenia przepływu pracy korzystającego z obu wbudowanych działań, takich jak <xref:System.Activities.Statements.Flowchart> działanie, oraz działań niestandardowych z poprzednich instrukcji [: Create a Activity](how-to-create-an-activity.md) .</span><span class="sxs-lookup"><span data-stu-id="0359e-105">This topic steps through creating a workflow that uses both built-in activities such as the <xref:System.Activities.Statements.Flowchart> activity, and the custom activities from the previous [How to: Create an Activity](how-to-create-an-activity.md) topic.</span></span> <span data-ttu-id="0359e-106">Przepływ pracy modeluje grę z liczbą odgadnąć.</span><span class="sxs-lookup"><span data-stu-id="0359e-106">The workflow models a number guessing game.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="0359e-107">Każdy temat w samouczku Wprowadzenie zależy od poprzednich tematów.</span><span class="sxs-lookup"><span data-stu-id="0359e-107">Each topic in the Getting Started tutorial depends on the previous topics.</span></span> <span data-ttu-id="0359e-108">Aby ukończyć ten temat, należy najpierw wykonać [instrukcje: tworzenie działania](how-to-create-an-activity.md).</span><span class="sxs-lookup"><span data-stu-id="0359e-108">To complete this topic, you must first complete [How to: Create an Activity](how-to-create-an-activity.md).</span></span>  
  
> [!NOTE]
> <span data-ttu-id="0359e-109">Aby pobrać kompletną wersję samouczka, zobacz [Windows Workflow Foundation (WF45) — samouczek wprowadzenie](https://go.microsoft.com/fwlink/?LinkID=248976).</span><span class="sxs-lookup"><span data-stu-id="0359e-109">To download a completed version of the tutorial, see [Windows Workflow Foundation (WF45) - Getting Started Tutorial](https://go.microsoft.com/fwlink/?LinkID=248976).</span></span>  
  
### <a name="to-create-the-workflow"></a><span data-ttu-id="0359e-110">Aby utworzyć przepływ pracy</span><span class="sxs-lookup"><span data-stu-id="0359e-110">To create the workflow</span></span>  
  
1. <span data-ttu-id="0359e-111">Kliknij prawym przyciskiem myszy pozycję **NumberGuessWorkflowActivities** w **Eksplorator rozwiązań** a następnie wybierz pozycję **Dodaj**, **nowy element**.</span><span class="sxs-lookup"><span data-stu-id="0359e-111">Right-click **NumberGuessWorkflowActivities** in **Solution Explorer** and select **Add**, **New Item**.</span></span>  
  
2. <span data-ttu-id="0359e-112">W węźle **zainstalowane**, **wspólne elementy** wybierz pozycję **przepływ pracy**.</span><span class="sxs-lookup"><span data-stu-id="0359e-112">In the **Installed**, **Common Items** node, select **Workflow**.</span></span> <span data-ttu-id="0359e-113">Wybierz **działanie** z listy **przepływów pracy** .</span><span class="sxs-lookup"><span data-stu-id="0359e-113">Select **Activity** from the **Workflow** list.</span></span>  
  
3. <span data-ttu-id="0359e-114">Wpisz tekst `FlowchartNumberGuessWorkflow` w polu **Nazwa** , a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="0359e-114">Type `FlowchartNumberGuessWorkflow` into the **Name** box and click **Add**.</span></span>  
  
4. <span data-ttu-id="0359e-115">Przeciągnij działanie **Flowchart** z sekcji **Flowchart** w **przyborniku** i upuść je do **działania Drop tutaj** etykieta na powierzchni projektowej przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="0359e-115">Drag a **Flowchart** activity from the **Flowchart** section of the **Toolbox** and drop it onto the **Drop activity here** label on the workflow design surface.</span></span>  
  
### <a name="to-create-the-workflow-variables-and-arguments"></a><span data-ttu-id="0359e-116">Aby utworzyć zmienne i argumenty przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="0359e-116">To create the workflow variables and arguments</span></span>  
  
1. <span data-ttu-id="0359e-117">Kliknij dwukrotnie pozycję **FlowchartNumberGuessWorkflow. XAML** w **Eksplorator rozwiązań** , aby wyświetlić przepływ pracy w projektancie, jeśli nie jest on jeszcze wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="0359e-117">Double-click **FlowchartNumberGuessWorkflow.xaml** in **Solution Explorer** to display the workflow in the designer, if it is not already displayed.</span></span>  
  
2. <span data-ttu-id="0359e-118">Kliknij pozycję **argumenty** w lewej dolnej części projektanta przepływu pracy, aby wyświetlić okienko **argumenty** .</span><span class="sxs-lookup"><span data-stu-id="0359e-118">Click **Arguments** in the lower-left side of the workflow designer to display the **Arguments** pane.</span></span>  
  
3. <span data-ttu-id="0359e-119">Kliknij przycisk **Utwórz argument**.</span><span class="sxs-lookup"><span data-stu-id="0359e-119">Click **Create Argument**.</span></span>  
  
4. <span data-ttu-id="0359e-120">Wpisz `MaxNumber` **w** polu **Nazwa** , wybierz z listy rozwijanej **kierunek** , wybierz **Int32** z listy rozwijanej **Typ argumentu** , a następnie naciśnij klawisz ENTER, aby zapisać argument.</span><span class="sxs-lookup"><span data-stu-id="0359e-120">Type `MaxNumber` into the **Name** box, select **In** from the **Direction** drop-down list, select **Int32** from the **Argument type** drop-down list, and then press ENTER to save the argument.</span></span>  
  
5. <span data-ttu-id="0359e-121">Kliknij przycisk **Utwórz argument**.</span><span class="sxs-lookup"><span data-stu-id="0359e-121">Click **Create Argument**.</span></span>  
  
6. <span data-ttu-id="0359e-122">Wpisz `Turns` w polu **Nazwa** , który znajduje się poniżej nowo dodanego `MaxNumber` argumentu **Out** , wybierz pozycję z listy rozwijanej **kierunek** , wybierz pozycję **Int32** z listy rozwijanej **Typ argumentu** , a następnie naciśnij klawisz ENTER.</span><span class="sxs-lookup"><span data-stu-id="0359e-122">Type `Turns` into the **Name** box that is below the newly added `MaxNumber` argument, select **Out** from the **Direction** drop-down list, select **Int32** from the **Argument type** drop-down list, and then press ENTER.</span></span>  
  
7. <span data-ttu-id="0359e-123">Kliknij pozycję **argumenty** w lewym dolnym rogu projektanta działań, aby zamknąć okienko **argumenty** .</span><span class="sxs-lookup"><span data-stu-id="0359e-123">Click **Arguments** in the lower-left side of the activity designer to close the **Arguments** pane.</span></span>  
  
8. <span data-ttu-id="0359e-124">Kliknij przycisk **zmienne** w lewej dolnej części projektanta przepływu pracy, aby wyświetlić okienko **zmienne** .</span><span class="sxs-lookup"><span data-stu-id="0359e-124">Click **Variables** in the lower-left side of the workflow designer to display the **Variables** pane.</span></span>  
  
9. <span data-ttu-id="0359e-125">Kliknij pozycję **Utwórz zmienną**.</span><span class="sxs-lookup"><span data-stu-id="0359e-125">Click **Create Variable**.</span></span>  
  
    > [!TIP]
    > <span data-ttu-id="0359e-126">Jeśli nie zostanie wyświetlone pole **Utwórz zmienną** , kliknij <xref:System.Activities.Statements.Flowchart> działanie na powierzchni projektanta przepływu pracy, aby je wybrać.</span><span class="sxs-lookup"><span data-stu-id="0359e-126">If no **Create Variable** box is displayed, click the <xref:System.Activities.Statements.Flowchart> activity on the workflow designer surface to select it.</span></span>  
  
10. <span data-ttu-id="0359e-127">Wpisz `Guess` w polu **Nazwa** , wybierz wartość **Int32** z listy rozwijanej **Typ zmiennej** , a następnie naciśnij klawisz ENTER, aby zapisać zmienną.</span><span class="sxs-lookup"><span data-stu-id="0359e-127">Type `Guess` into the **Name** box, select **Int32** from the **Variable type** drop-down list, and then press ENTER to save the variable.</span></span>  
  
11. <span data-ttu-id="0359e-128">Kliknij pozycję **Utwórz zmienną**.</span><span class="sxs-lookup"><span data-stu-id="0359e-128">Click **Create Variable**.</span></span>  
  
12. <span data-ttu-id="0359e-129">Wpisz `Target` w polu **Nazwa** , wybierz wartość **Int32** z listy rozwijanej **Typ zmiennej** , a następnie naciśnij klawisz ENTER, aby zapisać zmienną.</span><span class="sxs-lookup"><span data-stu-id="0359e-129">Type `Target` into the **Name** box, select **Int32** from the **Variable type** drop-down list, and then press ENTER to save the variable.</span></span>  
  
13. <span data-ttu-id="0359e-130">Kliknij pozycję **zmienne** w lewej dolnej części okna projektanta działań, aby zamknąć okienko **zmienne** .</span><span class="sxs-lookup"><span data-stu-id="0359e-130">Click **Variables** in the lower-left side of the activity designer to close the **Variables** pane.</span></span>  
  
### <a name="to-add-the-workflow-activities"></a><span data-ttu-id="0359e-131">Aby dodać działania przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="0359e-131">To add the workflow activities</span></span>  
  
1. <span data-ttu-id="0359e-132">Przeciągnij działanie **Przypisz** z sekcji elementy **pierwotne** w **przyborniku** i umieść je nad węzłem **początkowym** znajdującym się w górnej części schematu blokowego.</span><span class="sxs-lookup"><span data-stu-id="0359e-132">Drag an **Assign** activity from the **Primitives** section of the **Toolbox** and hover it over the **Start** node, which is at the top of the flowchart.</span></span> <span data-ttu-id="0359e-133">Gdy działanie **Assign** znajduje się nad węzłem **startowym** , zostaną wyświetlone trzy trójkąty wokół węzła **Start** .</span><span class="sxs-lookup"><span data-stu-id="0359e-133">When the **Assign** activity is over the **Start** node, three triangles will appear around the **Start** node.</span></span> <span data-ttu-id="0359e-134">Upuść działanie **Assign** na trójkącie, które znajduje się bezpośrednio pod węzłem **początkowym** .</span><span class="sxs-lookup"><span data-stu-id="0359e-134">Drop the **Assign** activity on the triangle that is directly below the **Start** node.</span></span> <span data-ttu-id="0359e-135">Spowoduje to połączenie dwóch elementów i wyznaczenie działania **przypisania** jako pierwszego działania w schemacie blokowym.</span><span class="sxs-lookup"><span data-stu-id="0359e-135">This will link the two items together and designates the **Assign** activity as the first activity in the flowchart.</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="0359e-136">Działania mogą być również wskazywane jako działanie uruchamiania w przepływie pracy przez ręczne łączenie z tym działaniem z węzłem początkowym.</span><span class="sxs-lookup"><span data-stu-id="0359e-136">Activities can also be indicated as the starting activity in the workflow by manually linking them activity to the start node.</span></span> <span data-ttu-id="0359e-137">Aby to zrobić, umieść kursor myszy nad węzłem **startowym** , kliknij jeden z prostokątów, który pojawia się, gdy wskaźnik myszy znajduje się nad węzłem **startowym** , i przeciągnij linię łączącą w dół do żądanego działania i upuść ją na jednym z prostokątów, które są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="0359e-137">To do this, hover the mouse over the **Start** node, click one of the rectangles that appear when the mouse is over the **Start** node, and drag the connecting line down to the desired activity and drop it on one of the rectangles that appear.</span></span> <span data-ttu-id="0359e-138">Możesz również wyznaczyć działanie jako działanie uruchamiania, klikając je prawym przyciskiem myszy i wybierając pozycję **Ustaw jako węzeł startowy**.</span><span class="sxs-lookup"><span data-stu-id="0359e-138">You can also designate an activity as the starting activity by right-clicking the it and choosing **Set as Start Node**.</span></span>  
  
2. <span data-ttu-id="0359e-139">Wpisz `Target` w polu **do** i poniższe wyrażenie w polu **wprowadź wyrażenie języka C#** lub **wprowadź wyrażenie VB** .</span><span class="sxs-lookup"><span data-stu-id="0359e-139">Type `Target` into the **To** box and the following expression into the **Enter a C# Expression** or **Enter a VB expression** box.</span></span>  
  
    ```vb  
    New System.Random().Next(1, MaxNumber + 1)  
    ```  
  
    ```csharp  
    new System.Random().Next(1, MaxNumber + 1)  
    ```  
  
    > [!TIP]
    > <span data-ttu-id="0359e-140">Jeśli okno **Przybornik** nie jest wyświetlane, wybierz pozycję **Przybornik** z menu **Widok** .</span><span class="sxs-lookup"><span data-stu-id="0359e-140">If the **Toolbox** window is not displayed, select **Toolbox** from the **View** menu.</span></span>  
  
3. <span data-ttu-id="0359e-141">Przeciągnij działanie **monitu** z sekcji **NumberGuessWorkflowActivities** w **przyborniku**, upuść je poniżej akcji **Przypisz** z poprzedniego kroku, a następnie połącz działanie **monitu** z **przypisaniem** działania.</span><span class="sxs-lookup"><span data-stu-id="0359e-141">Drag a **Prompt** activity from the **NumberGuessWorkflowActivities** section of the **Toolbox**, drop it below the **Assign** activity from the previous step, and connect the **Prompt** activity to the **Assign** activity.</span></span> <span data-ttu-id="0359e-142">Istnieją trzy sposoby łączenia tych dwóch działań.</span><span class="sxs-lookup"><span data-stu-id="0359e-142">There are three ways to connect the two activities.</span></span> <span data-ttu-id="0359e-143">Pierwszy sposób polega na nawiązaniu połączenia w trakcie upuszczania działania **monitu** w przepływie pracy.</span><span class="sxs-lookup"><span data-stu-id="0359e-143">The first way is to connect them as you drop the **Prompt** activity on the workflow.</span></span> <span data-ttu-id="0359e-144">Przeciągając działanie **monitu** do przepływu pracy, umieść je nad przydziałem **Assign** i upuść je na jednym z czterech trójkątów, które pojawiają się, gdy działanie **monitu** znajduje się nad **przypisaniem** .</span><span class="sxs-lookup"><span data-stu-id="0359e-144">As you are dragging the **Prompt** activity to the workflow, hover it over the **Assign** activity and drop it onto one of the four triangles that appear when the **Prompt** activity is over the **Assign** activity.</span></span> <span data-ttu-id="0359e-145">Drugi sposób polega na porzucenia działania **monitu** na przepływ pracy w odpowiedniej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="0359e-145">The second way is to drop the **Prompt** activity onto the workflow at the desired location.</span></span> <span data-ttu-id="0359e-146">Następnie przesuń wskaźnik myszy nad działanie **przypisywania** i przeciągnij jeden z prostokątów, które pojawiają się w dół do działania **monitu** .</span><span class="sxs-lookup"><span data-stu-id="0359e-146">Then, hover the mouse over the **Assign** activity and drag one of the rectangles that appears down to the **Prompt** activity.</span></span> <span data-ttu-id="0359e-147">Przeciągnij myszą tak, aby linia łącząca z działania **Assign** łączyła się z jednym z prostokątów działania **monitu** , a następnie zwolnij przycisk myszy.</span><span class="sxs-lookup"><span data-stu-id="0359e-147">Drag the mouse so that the connecting line from the **Assign** activity connects to one of the rectangles of the **Prompt** activity, and then release the mouse button.</span></span> <span data-ttu-id="0359e-148">Trzeci sposób jest bardzo podobny do pierwszego, z tą różnicą, że zamiast przeciągać działanie **monitu** z **przybornika**, przeciągniesz go z jego lokalizacji na powierzchni projektowej przepływu pracy, umieścisz go nad działaniem **przypisywania** i upuść je na jeden z wyświetlonych trójkątów.</span><span class="sxs-lookup"><span data-stu-id="0359e-148">The third way is very similar to the first way, except that instead of dragging the **Prompt** activity from the **Toolbox**, you drag it from its location on the workflow design surface, hover it over the **Assign** activity, and drop it onto one of the triangles that appears.</span></span>  
  
4. <span data-ttu-id="0359e-149">W **oknie właściwości** działania **monitu** wpisz, w `"EnterGuess"` tym cudzysłowy w polu wartość właściwości **zakładkaname** .</span><span class="sxs-lookup"><span data-stu-id="0359e-149">In the **Properties Window** for the **Prompt** activity, type `"EnterGuess"` including the quotes into the **BookmarkName** property value box.</span></span> <span data-ttu-id="0359e-150">Wpisz `Guess` w polu wartość właściwości **wynik** i wpisz następujące wyrażenie w polu właściwości **Text** .</span><span class="sxs-lookup"><span data-stu-id="0359e-150">Type `Guess` into the **Result** property value box, and type the following expression into the **Text** property box.</span></span>  
  
    ```vb  
    "Please enter a number between 1 and " & MaxNumber  
    ```  
  
    ```csharp  
    "Please enter a number between 1 and " + MaxNumber  
    ```  
  
    > [!TIP]
    > <span data-ttu-id="0359e-151">Jeśli **okno właściwości** nie jest wyświetlane, wybierz pozycję **okno właściwości** w menu **Widok** .</span><span class="sxs-lookup"><span data-stu-id="0359e-151">If the **Properties Window** is not displayed, select **Properties Window** from the **View** menu.</span></span>  
  
5. <span data-ttu-id="0359e-152">Przeciągnij działanie **Przypisz** z sekcji elementy **pierwotne** w **przyborniku** i połącz je przy użyciu jednej z metod opisanych w poprzednim kroku, tak aby była niższa od działania **monitu** .</span><span class="sxs-lookup"><span data-stu-id="0359e-152">Drag an **Assign** activity from the **Primitives** section of the **Toolbox** and connect it using one of the methods described in the previous step so that it is below the **Prompt** activity.</span></span>  
  
6. <span data-ttu-id="0359e-153">Wpisz `Turns` w polu **do** i `Turns + 1` w polu **wprowadź wyrażenie języka C#**  lub **wprowadź wyrażenie w języku VB** .</span><span class="sxs-lookup"><span data-stu-id="0359e-153">Type `Turns` into the **To** box and `Turns + 1` into the **Enter a C# expression**  or **Enter a VB expression** box.</span></span>  
  
7. <span data-ttu-id="0359e-154">Przeciągnij element **FlowDecision** z sekcji **Flowchart** w **przyborniku** i połącz go pod działaniem **Assign** .</span><span class="sxs-lookup"><span data-stu-id="0359e-154">Drag a **FlowDecision** from the **Flowchart** section of the **Toolbox** and connect it below the **Assign** activity.</span></span> <span data-ttu-id="0359e-155">W **oknie właściwości** wpisz następujące wyrażenie w polu wartość właściwości **warunek** .</span><span class="sxs-lookup"><span data-stu-id="0359e-155">In the **Properties Window**, type the following expression into the **Condition** property value box.</span></span>  
  
    ```vb  
    Guess = Target  
    ```  
  
    ```csharp  
    Guess == Target  
    ```  
  
8. <span data-ttu-id="0359e-156">Przeciągnij kolejną aktywność **FlowDecision** z **przybornika** i upuść ją poniżej pierwszego.</span><span class="sxs-lookup"><span data-stu-id="0359e-156">Drag another **FlowDecision** activity from the **Toolbox** and drop it below the first one.</span></span> <span data-ttu-id="0359e-157">Połącz dwa działania, przeciągając od prostokąta, który jest oznaczony jako **false** w górnym działaniu **FlowDecision** do prostokąta w górnej części drugiego działania **FlowDecision** .</span><span class="sxs-lookup"><span data-stu-id="0359e-157">Connect the two activities by dragging from the rectangle that is labeled **False** on the top **FlowDecision** activity to the rectangle at the top of the second **FlowDecision** activity.</span></span>  
  
    > [!TIP]
    > <span data-ttu-id="0359e-158">Jeśli nie widzisz etykiet **prawda** i **Fałsz** w **FlowDecision**, umieść wskaźnik myszy nad **FlowDecisionem**.</span><span class="sxs-lookup"><span data-stu-id="0359e-158">If you do not see the **True** and **False** labels on the **FlowDecision**, hover the mouse over the **FlowDecision**.</span></span>  
  
9. <span data-ttu-id="0359e-159">Kliknij drugie działanie **FlowDecision** , aby je wybrać.</span><span class="sxs-lookup"><span data-stu-id="0359e-159">Click the second **FlowDecision** activity to select it.</span></span> <span data-ttu-id="0359e-160">W **oknie właściwości** wpisz następujące wyrażenie w polu wartość właściwości **warunek** .</span><span class="sxs-lookup"><span data-stu-id="0359e-160">In the **Properties Window**, type the following expression into the **Condition** property value box.</span></span>  
  
    ```text
    Guess < Target
    ```  
  
10. <span data-ttu-id="0359e-161">Przeciągnij dwie działania **WriteLine** z sekcji elementy **pierwotne** w **przyborniku** i upuść je tak, aby znajdowały się obok dwóch działań **FlowDecision** .</span><span class="sxs-lookup"><span data-stu-id="0359e-161">Drag two **WriteLine** activities from the **Primitives** section of the **Toolbox** and drop them so that they are side by side below the two **FlowDecision** activities.</span></span> <span data-ttu-id="0359e-162">Połącz **rzeczywistą** akcję dolnego działania **FlowDecision** do lewego działania **WriteLine** i **wartość false** dla działania **WriteLine** z prawej strony.</span><span class="sxs-lookup"><span data-stu-id="0359e-162">Connect the **True** action of the bottom **FlowDecision** activity to the leftmost **WriteLine** activity, and the **False** action to the rightmost **WriteLine** activity.</span></span>  
  
11. <span data-ttu-id="0359e-163">Kliknij z lewej strony działanie **WriteLine** , aby je zaznaczyć, a następnie wpisz następujące wyrażenie w polu wartość właściwości **tekst** w **oknie właściwości**.</span><span class="sxs-lookup"><span data-stu-id="0359e-163">Click the leftmost **WriteLine** activity to select it, and type the following expression into the **Text** property value box in the **Properties Window**.</span></span>  
  
    ```text
    "Your guess is too low."  
    ```  
  
12. <span data-ttu-id="0359e-164">Połącz metodę **WriteLine** z lewą stroną działania **monitu** o powyższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="0359e-164">Connect the **WriteLine** to the left side of the **Prompt** activity that is above it.</span></span>  
  
13. <span data-ttu-id="0359e-165">Kliknij **prawym** przyciskiem, aby go zaznaczyć, i wpisz następujące wyrażenie w polu wartość właściwości **tekst** w **oknie właściwości**.</span><span class="sxs-lookup"><span data-stu-id="0359e-165">Click the rightmost **WriteLine** activity to select it, and type the following expression into the **Text** property value box in the **Properties Window**.</span></span>  
  
    ```text
    "Your guess is too high."  
    ```  
  
14. <span data-ttu-id="0359e-166">Połącz działanie **WriteLine** z prawą stroną działania **monitu** .</span><span class="sxs-lookup"><span data-stu-id="0359e-166">Connect the **WriteLine** activity to the right side of the **Prompt** activity above it.</span></span>  
  
     <span data-ttu-id="0359e-167">Poniższy przykład ilustruje ukończony przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="0359e-167">The following example illustrates the completed workflow.</span></span>  
  
     ![Diagram przedstawiający ukończony schemat blokowy Windows Workflow Foundation.](./media/how-to-create-a-flowchart-workflow/completed-windows-workflow-flowchart.png)  
  
### <a name="to-build-the-workflow"></a><span data-ttu-id="0359e-169">Aby skompilować przepływ pracy</span><span class="sxs-lookup"><span data-stu-id="0359e-169">To build the workflow</span></span>  
  
1. <span data-ttu-id="0359e-170">Naciśnij kombinację klawiszy CTRL+SHIFT+B w celu skompilowania rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="0359e-170">Press CTRL+SHIFT+B to build the solution.</span></span>  
  
     <span data-ttu-id="0359e-171">Aby uzyskać instrukcje dotyczące sposobu uruchamiania przepływu pracy, zobacz następny temat, [jak: uruchamianie przepływu pracy](how-to-run-a-workflow.md).</span><span class="sxs-lookup"><span data-stu-id="0359e-171">For instructions on how to run the workflow, please see the next topic, [How to: Run a Workflow](how-to-run-a-workflow.md).</span></span> <span data-ttu-id="0359e-172">Jeśli zostały już wykonane kroki [: uruchamianie przepływu pracy](how-to-run-a-workflow.md) z innym stylem przepływu pracy i chcesz uruchomić go za pomocą przepływu pracy Flowchart z tego kroku, przejdź do tematu, [Aby skompilować i uruchomić aplikację](how-to-run-a-workflow.md#BKMK_ToRunTheApplication) w temacie [jak uruchomić przepływ pracy](how-to-run-a-workflow.md).</span><span class="sxs-lookup"><span data-stu-id="0359e-172">If you have already completed the [How to: Run a Workflow](how-to-run-a-workflow.md) step with a different style of workflow and wish to run it using the flowchart workflow from this step, skip ahead to the [To build and run the application](how-to-run-a-workflow.md#BKMK_ToRunTheApplication) section of [How to: Run a Workflow](how-to-run-a-workflow.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="0359e-173">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="0359e-173">See also</span></span>

- <xref:System.Activities.Statements.Flowchart>
- <xref:System.Activities.Statements.FlowDecision>
- [<span data-ttu-id="0359e-174">Programowanie w programie Windows Workflow Foundation</span><span class="sxs-lookup"><span data-stu-id="0359e-174">Windows Workflow Foundation Programming</span></span>](programming.md)
- [<span data-ttu-id="0359e-175">Projektowanie przepływów pracy</span><span class="sxs-lookup"><span data-stu-id="0359e-175">Designing Workflows</span></span>](designing-workflows.md)
- [<span data-ttu-id="0359e-176">Wprowadzenie — samouczek</span><span class="sxs-lookup"><span data-stu-id="0359e-176">Getting Started Tutorial</span></span>](getting-started-tutorial.md)
- [<span data-ttu-id="0359e-177">Instrukcje: Tworzenie działania</span><span class="sxs-lookup"><span data-stu-id="0359e-177">How to: Create an Activity</span></span>](how-to-create-an-activity.md)
- [<span data-ttu-id="0359e-178">Instrukcje: Uruchamianie przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="0359e-178">How to: Run a Workflow</span></span>](how-to-run-a-workflow.md)
