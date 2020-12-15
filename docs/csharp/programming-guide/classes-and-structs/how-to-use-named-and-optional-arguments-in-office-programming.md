---
title: Jak używać argumentów nazwanych i opcjonalnych w programowaniu pakietu Office — Przewodnik programowania w języku C#
description: Dowiedz się, jak używać argumentów nazwanych i opcjonalnych argumentów, aby ułatwić dostęp do interfejsów COM, takich jak Microsoft Office interfejsów API automatyzacji.
ms.date: 07/20/2015
helpviewer_keywords:
- named and optional arguments [C#], Office programming
- optional arguments [C#], Office programming
- named arguments [C#], Office programming
ms.topic: how-to
ms.custom: contperf-fy21q2
ms.assetid: 65b8a222-bcd8-454c-845f-84adff5a356f
ms.openlocfilehash: de0545131385c13a79fd35df74e3a04da98ad8fb
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97512479"
---
# <a name="how-to-use-named-and-optional-arguments-in-office-programming-c-programming-guide"></a><span data-ttu-id="50241-103">Jak używać argumentów nazwanych i opcjonalnych w programowaniu pakietu Office (Przewodnik programowania w języku C#)</span><span class="sxs-lookup"><span data-stu-id="50241-103">How to use named and optional arguments in Office programming (C# Programming Guide)</span></span>

<span data-ttu-id="50241-104">Argumenty nazwane i opcjonalne argumenty, wprowadzone w języku C# 4, zwiększają wygodę, elastyczność i czytelność w programowaniu języka C#.</span><span class="sxs-lookup"><span data-stu-id="50241-104">Named arguments and optional arguments, introduced in C# 4, enhance convenience, flexibility, and readability in C# programming.</span></span> <span data-ttu-id="50241-105">Ponadto te funkcje znacznie ułatwiają dostęp do interfejsów COM, takich jak interfejsy API automatyzacji Microsoft Office.</span><span class="sxs-lookup"><span data-stu-id="50241-105">In addition, these features greatly facilitate access to COM interfaces such as the Microsoft Office automation APIs.</span></span>

<span data-ttu-id="50241-106">W poniższym przykładzie metoda [ConvertToTable](<xref:Microsoft.Office.Interop.Word.Range.ConvertToTable%2A>) ma szesnaste parametry, które reprezentują cechy tabeli, takie jak liczba kolumn i wierszy, formatowanie, obramowania, czcionki i kolory.</span><span class="sxs-lookup"><span data-stu-id="50241-106">In the following example, method [ConvertToTable](<xref:Microsoft.Office.Interop.Word.Range.ConvertToTable%2A>) has sixteen parameters that represent characteristics of a table, such as number of columns and rows, formatting, borders, fonts, and colors.</span></span> <span data-ttu-id="50241-107">Wszystkie 16 parametrów są opcjonalne, ponieważ większość z nich nie chce określać konkretnych wartości dla wszystkich z nich.</span><span class="sxs-lookup"><span data-stu-id="50241-107">All sixteen parameters are optional, because most of the time you do not want to specify particular values for all of them.</span></span> <span data-ttu-id="50241-108">Jednakże bez argumentów nazwanych i opcjonalnych należy podać wartość lub symbol zastępczy dla każdego parametru.</span><span class="sxs-lookup"><span data-stu-id="50241-108">However, without named and optional arguments, a value or a placeholder value has to be provided for each parameter.</span></span> <span data-ttu-id="50241-109">Za pomocą argumentów nazwanych i opcjonalnych można określić wartości tylko dla parametrów, które są wymagane dla projektu.</span><span class="sxs-lookup"><span data-stu-id="50241-109">With named and optional arguments, you specify values only for the parameters that are required for your project.</span></span>

<span data-ttu-id="50241-110">Aby wykonać te procedury, na komputerze musi być zainstalowany program Microsoft Office Word.</span><span class="sxs-lookup"><span data-stu-id="50241-110">You must have Microsoft Office Word installed on your computer to complete these procedures.</span></span>

[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]

## <a name="to-create-a-new-console-application"></a><span data-ttu-id="50241-111">Aby utworzyć nową aplikację konsolową</span><span class="sxs-lookup"><span data-stu-id="50241-111">To create a new console application</span></span>

1. <span data-ttu-id="50241-112">Uruchom program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="50241-112">Start Visual Studio.</span></span>

2. <span data-ttu-id="50241-113">W menu **plik** wskaż polecenie **Nowy**, a następnie kliknij pozycję **projekt**.</span><span class="sxs-lookup"><span data-stu-id="50241-113">On the **File** menu, point to **New**, and then click **Project**.</span></span>

3. <span data-ttu-id="50241-114">W okienku **Kategorie szablonów** rozwiń węzeł **Visual C#**, a następnie kliknij pozycję **Windows**.</span><span class="sxs-lookup"><span data-stu-id="50241-114">In the **Templates Categories** pane, expand **Visual C#**, and then click **Windows**.</span></span>

4. <span data-ttu-id="50241-115">Poszukaj w górnej części okienka **Szablony** , aby upewnić się, że **.NET Framework 4** pojawia się w polu **platforma docelowa** .</span><span class="sxs-lookup"><span data-stu-id="50241-115">Look in the top of the **Templates** pane to make sure that **.NET Framework 4** appears in the **Target Framework** box.</span></span>

5. <span data-ttu-id="50241-116">W okienku **Szablony** kliknij pozycję **Aplikacja konsolowa**.</span><span class="sxs-lookup"><span data-stu-id="50241-116">In the **Templates** pane, click **Console Application**.</span></span>

6. <span data-ttu-id="50241-117">Wpisz nazwę projektu w polu **Nazwa** .</span><span class="sxs-lookup"><span data-stu-id="50241-117">Type a name for your project in the **Name** field.</span></span>

7. <span data-ttu-id="50241-118">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="50241-118">Click **OK**.</span></span>

     <span data-ttu-id="50241-119">Nowy projekt zostanie wyświetlony w **Eksplorator rozwiązań**.</span><span class="sxs-lookup"><span data-stu-id="50241-119">The new project appears in **Solution Explorer**.</span></span>

## <a name="to-add-a-reference"></a><span data-ttu-id="50241-120">Aby dodać odwołanie</span><span class="sxs-lookup"><span data-stu-id="50241-120">To add a reference</span></span>

1. <span data-ttu-id="50241-121">W **Eksplorator rozwiązań** kliknij prawym przyciskiem myszy nazwę projektu, a następnie kliknij pozycję **Dodaj odwołanie**.</span><span class="sxs-lookup"><span data-stu-id="50241-121">In **Solution Explorer**, right-click your project's name and then click **Add Reference**.</span></span> <span data-ttu-id="50241-122">Zostanie wyświetlone okno dialogowe **Dodawanie odwołania** .</span><span class="sxs-lookup"><span data-stu-id="50241-122">The **Add Reference** dialog box appears.</span></span>

2. <span data-ttu-id="50241-123">Na stronie **.NET** wybierz pozycję **Microsoft. Office. Interop. Word** na liście **Nazwa składnika** .</span><span class="sxs-lookup"><span data-stu-id="50241-123">On the **.NET** page, select **Microsoft.Office.Interop.Word** in the **Component Name** list.</span></span>

3. <span data-ttu-id="50241-124">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="50241-124">Click **OK**.</span></span>

## <a name="to-add-necessary-using-directives"></a><span data-ttu-id="50241-125">Aby dodać wymagane dyrektywy using</span><span class="sxs-lookup"><span data-stu-id="50241-125">To add necessary using directives</span></span>

1. <span data-ttu-id="50241-126">W **Eksplorator rozwiązań** kliknij prawym przyciskiem myszy plik *program.cs* , a następnie kliknij polecenie **Wyświetl kod**.</span><span class="sxs-lookup"><span data-stu-id="50241-126">In **Solution Explorer**, right-click the *Program.cs* file and then click **View Code**.</span></span>

2. <span data-ttu-id="50241-127">Dodaj następujące `using` dyrektywy na początku pliku kodu:</span><span class="sxs-lookup"><span data-stu-id="50241-127">Add the following `using` directives to the top of the code file:</span></span>

     [!code-csharp[csProgGuideNamedAndOptional#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/wordprogram.cs#4)]

## <a name="to-display-text-in-a-word-document"></a><span data-ttu-id="50241-128">Aby wyświetlić tekst w dokumencie programu Word</span><span class="sxs-lookup"><span data-stu-id="50241-128">To display text in a Word document</span></span>

1. <span data-ttu-id="50241-129">W `Program` klasie w *program.cs* Dodaj następującą metodę w celu utworzenia aplikacji programu Word i dokumentu programu Word.</span><span class="sxs-lookup"><span data-stu-id="50241-129">In the `Program` class in *Program.cs*, add the following method to create a Word application and a Word document.</span></span> <span data-ttu-id="50241-130">Metoda [Add](<xref:Microsoft.Office.Interop.Word.Documents.Add%2A>) ma cztery parametry opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="50241-130">The [Add](<xref:Microsoft.Office.Interop.Word.Documents.Add%2A>) method has four optional parameters.</span></span> <span data-ttu-id="50241-131">W tym przykładzie używane są wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="50241-131">This example uses their default values.</span></span> <span data-ttu-id="50241-132">W związku z tym nie są wymagane żadne argumenty w instrukcji wywołującej.</span><span class="sxs-lookup"><span data-stu-id="50241-132">Therefore, no arguments are necessary in the calling statement.</span></span>

     [!code-csharp[csProgGuideNamedAndOptional#6](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/wordprogram.cs#6)]

2. <span data-ttu-id="50241-133">Dodaj następujący kod na końcu metody, aby określić, gdzie ma być wyświetlany tekst w dokumencie i jaki tekst ma być wyświetlany:</span><span class="sxs-lookup"><span data-stu-id="50241-133">Add the following code at the end of the method to define where to display text in the document, and what text to display:</span></span>

     [!code-csharp[csProgGuideNamedAndOptional#7](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/wordprogram.cs#7)]

## <a name="to-run-the-application"></a><span data-ttu-id="50241-134">Aby uruchomić aplikację</span><span class="sxs-lookup"><span data-stu-id="50241-134">To run the application</span></span>

1. <span data-ttu-id="50241-135">Dodaj następującą instrukcję do głównej:</span><span class="sxs-lookup"><span data-stu-id="50241-135">Add the following statement to Main:</span></span>

     [!code-csharp[csProgGuideNamedAndOptional#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/wordprogram.cs#8)]

2. <span data-ttu-id="50241-136">Naciśnij klawisz <kbd>Ctrl</kbd> + <kbd>F5</kbd> , aby uruchomić projekt.</span><span class="sxs-lookup"><span data-stu-id="50241-136">Press <kbd>CTRL</kbd>+<kbd>F5</kbd> to run the project.</span></span> <span data-ttu-id="50241-137">Zostanie wyświetlony dokument programu Word zawierający określony tekst.</span><span class="sxs-lookup"><span data-stu-id="50241-137">A Word document appears that contains the specified text.</span></span>

## <a name="to-change-the-text-to-a-table"></a><span data-ttu-id="50241-138">Aby zmienić tekst na tabelę</span><span class="sxs-lookup"><span data-stu-id="50241-138">To change the text to a table</span></span>
  
1. <span data-ttu-id="50241-139">Użyj `ConvertToTable` metody, aby ująć tekst w tabeli.</span><span class="sxs-lookup"><span data-stu-id="50241-139">Use the `ConvertToTable` method to enclose the text in a table.</span></span> <span data-ttu-id="50241-140">Metoda ma szesnaste parametry opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="50241-140">The method has sixteen optional parameters.</span></span> <span data-ttu-id="50241-141">Funkcja IntelliSense ujmuje opcjonalne parametry w nawiasach, jak pokazano na poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="50241-141">IntelliSense encloses optional parameters in brackets, as shown in the following illustration.</span></span>

     ![Lista parametrów dla metody ConvertToTable](./media/how-to-use-named-and-optional-arguments-in-office-programming/convert-table-parameters.png)

     <span data-ttu-id="50241-143">Argumenty nazwane i opcjonalne umożliwiają określenie wartości tylko dla parametrów, które mają zostać zmienione.</span><span class="sxs-lookup"><span data-stu-id="50241-143">Named and optional arguments enable you to specify values for only the parameters that you want to change.</span></span> <span data-ttu-id="50241-144">Dodaj następujący kod na końcu metody `DisplayInWord` , aby utworzyć prostą tabelę.</span><span class="sxs-lookup"><span data-stu-id="50241-144">Add the following code to the end of method `DisplayInWord` to create a simple table.</span></span> <span data-ttu-id="50241-145">Argument określa, że przecinki w ciągu tekstowym `range` oddzielają komórki tabeli.</span><span class="sxs-lookup"><span data-stu-id="50241-145">The argument specifies that the commas in the text string in `range` separate the cells of the table.</span></span>

     [!code-csharp[csProgGuideNamedAndOptional#9](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/wordprogram.cs#9)]

     <span data-ttu-id="50241-146">We wcześniejszych wersjach języka C# wywołanie `ConvertToTable` wymaga argumentu odwołania dla każdego parametru, jak pokazano w poniższym kodzie:</span><span class="sxs-lookup"><span data-stu-id="50241-146">In earlier versions of C#, the call to `ConvertToTable` requires a reference argument for each parameter, as shown in the following code:</span></span>
  
     [!code-csharp[csProgGuideNamedAndOptional#14](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/wordprogram.cs#14)]

2. <span data-ttu-id="50241-147">Naciśnij klawisz <kbd>Ctrl</kbd> + <kbd>F5</kbd> , aby uruchomić projekt.</span><span class="sxs-lookup"><span data-stu-id="50241-147">Press <kbd>CTRL</kbd>+<kbd>F5</kbd> to run the project.</span></span>

## <a name="to-experiment-with-other-parameters"></a><span data-ttu-id="50241-148">Aby eksperymentować z innymi parametrami</span><span class="sxs-lookup"><span data-stu-id="50241-148">To experiment with other parameters</span></span>

1. <span data-ttu-id="50241-149">Aby zmienić tabelę tak, aby stała się jedną kolumną i trzema wierszami, Zastąp ostatni wiersz w `DisplayInWord` następującej instrukcji, a następnie wpisz <kbd>Ctrl</kbd> + <kbd>F5</kbd>.</span><span class="sxs-lookup"><span data-stu-id="50241-149">To change the table so that it has one column and three rows, replace the last line in `DisplayInWord` with the following statement and then type <kbd>CTRL</kbd>+<kbd>F5</kbd>.</span></span>  

     [!code-csharp[csProgGuideNamedAndOptional#10](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/wordprogram.cs#10)]

2. <span data-ttu-id="50241-150">Aby określić wstępnie zdefiniowany format tabeli, Zastąp ostatni wiersz w `DisplayInWord` z następującą instrukcją, a następnie wpisz <kbd>Ctrl</kbd> + <kbd>F5</kbd>.</span><span class="sxs-lookup"><span data-stu-id="50241-150">To specify a predefined format for the table, replace the last line in `DisplayInWord` with the following statement and then type <kbd>CTRL</kbd>+<kbd>F5</kbd>.</span></span> <span data-ttu-id="50241-151">Format może być dowolną ze stałych [WdTableFormat](<xref:Microsoft.Office.Interop.Word.WdTableFormat>) .</span><span class="sxs-lookup"><span data-stu-id="50241-151">The format can be any of the [WdTableFormat](<xref:Microsoft.Office.Interop.Word.WdTableFormat>) constants.</span></span>

     [!code-csharp[csProgGuideNamedAndOptional#11](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/wordprogram.cs#11)]

## <a name="example"></a><span data-ttu-id="50241-152">Przykład</span><span class="sxs-lookup"><span data-stu-id="50241-152">Example</span></span>

<span data-ttu-id="50241-153">Poniższy kod zawiera pełny przykład:</span><span class="sxs-lookup"><span data-stu-id="50241-153">The following code includes the full example:</span></span>

 [!code-csharp[csProgGuideNamedAndOptional#12](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/wordprogram.cs#12)]

## <a name="see-also"></a><span data-ttu-id="50241-154">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="50241-154">See also</span></span>

- [<span data-ttu-id="50241-155">Argumenty nazwane i opcjonalne</span><span class="sxs-lookup"><span data-stu-id="50241-155">Named and Optional Arguments</span></span>](./named-and-optional-arguments.md)
