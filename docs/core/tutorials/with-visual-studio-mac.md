---
title: Tworzenie aplikacji konsolowej .NET przy użyciu Visual Studio dla komputerów Mac
description: Dowiedz się, jak utworzyć aplikację konsolową .NET przy użyciu Visual Studio dla komputerów Mac.
ms.date: 11/30/2020
ms.openlocfilehash: 1351b06eec32cd8d3d9d44926655405fe2246f58
ms.sourcegitcommit: 9d525bb8109216ca1dc9e39c149d4902f4b43da5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2020
ms.locfileid: "96599489"
---
# <a name="tutorial-create-a-net-console-application-using-visual-studio-for-mac"></a><span data-ttu-id="f982c-103">Samouczek: Tworzenie aplikacji konsolowej .NET przy użyciu Visual Studio dla komputerów Mac</span><span class="sxs-lookup"><span data-stu-id="f982c-103">Tutorial: Create a .NET console application using Visual Studio for Mac</span></span>

<span data-ttu-id="f982c-104">W tym samouczku pokazano, jak utworzyć i uruchomić aplikację konsolową .NET przy użyciu Visual Studio dla komputerów Mac.</span><span class="sxs-lookup"><span data-stu-id="f982c-104">This tutorial shows how to create and run a .NET console application using Visual Studio for Mac.</span></span>

> [!NOTE]
> <span data-ttu-id="f982c-105">Opinie są wysoce wyceniane.</span><span class="sxs-lookup"><span data-stu-id="f982c-105">Your feedback is highly valued.</span></span> <span data-ttu-id="f982c-106">Istnieją dwa sposoby przekazywania opinii zespołowi programistycznemu na Visual Studio dla komputerów Mac:</span><span class="sxs-lookup"><span data-stu-id="f982c-106">There are two ways you can provide feedback to the development team on Visual Studio for Mac:</span></span>
>
> * <span data-ttu-id="f982c-107">W Visual Studio dla komputerów Mac wybierz pozycję **Pomoc**  >  **Zgłoś problem** z menu lub **Zgłoś problem** na ekranie powitalnym, co spowoduje otwarcie okna do zgłoszenia usterki.</span><span class="sxs-lookup"><span data-stu-id="f982c-107">In Visual Studio for Mac, select **Help** > **Report a Problem** from the menu or **Report a Problem** from the Welcome screen, which will open a window for filing a bug report.</span></span> <span data-ttu-id="f982c-108">Swoje opinie możesz śledzić w portalu [Społeczność deweloperów](https://aka.ms/feedback/report?space=41).</span><span class="sxs-lookup"><span data-stu-id="f982c-108">You can track your feedback in the [Developer Community](https://aka.ms/feedback/report?space=41) portal.</span></span>
> * <span data-ttu-id="f982c-109">Aby skorzystać z sugestii, wybierz pozycję **Pomoc**  >  **Podaj sugestię** z menu lub **Podaj sugestię** na ekranie powitalnym, co spowoduje przejście do [strony internetowej społeczność deweloperów Visual Studio dla komputerów Mac](https://aka.ms/feedback/suggest?space=41).</span><span class="sxs-lookup"><span data-stu-id="f982c-109">To make a suggestion, select **Help** > **Provide a Suggestion** from the menu or **Provide a Suggestion** from the Welcome screen, which will take you to the [Visual Studio for Mac Developer Community webpage](https://aka.ms/feedback/suggest?space=41).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f982c-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f982c-110">Prerequisites</span></span>

* <span data-ttu-id="f982c-111">[Visual Studio dla komputerów Mac w wersji 8,8 lub nowszej](https://visualstudio.microsoft.com/vs/mac/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link).</span><span class="sxs-lookup"><span data-stu-id="f982c-111">[Visual Studio for Mac version 8.8 or later](https://visualstudio.microsoft.com/vs/mac/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link).</span></span> <span data-ttu-id="f982c-112">Wybierz opcję zainstalowania platformy .NET Core.</span><span class="sxs-lookup"><span data-stu-id="f982c-112">Select the option to install .NET Core.</span></span> <span data-ttu-id="f982c-113">Instalowanie platformy Xamarin jest opcjonalne w przypadku programowania na platformie .NET.</span><span class="sxs-lookup"><span data-stu-id="f982c-113">Installing Xamarin is optional for .NET development.</span></span> <span data-ttu-id="f982c-114">Więcej informacji można znaleźć w następujących zasobach:</span><span class="sxs-lookup"><span data-stu-id="f982c-114">For more information, see the following resources:</span></span>

  * <span data-ttu-id="f982c-115">[Samouczek: instalowanie Visual Studio dla komputerów Mac](/visualstudio/mac/installation).</span><span class="sxs-lookup"><span data-stu-id="f982c-115">[Tutorial: Install Visual Studio for Mac](/visualstudio/mac/installation).</span></span>
  * <span data-ttu-id="f982c-116">[Obsługiwane wersje macOS](../install/windows.md).</span><span class="sxs-lookup"><span data-stu-id="f982c-116">[Supported macOS versions](../install/windows.md).</span></span>
  * <span data-ttu-id="f982c-117">[Wersje platformy .NET obsługiwane przez Visual Studio dla komputerów Mac](/visualstudio/mac/net-core-support).</span><span class="sxs-lookup"><span data-stu-id="f982c-117">[.NET versions supported by Visual Studio for Mac](/visualstudio/mac/net-core-support).</span></span>

## <a name="create-the-app"></a><span data-ttu-id="f982c-118">Tworzenie aplikacji</span><span class="sxs-lookup"><span data-stu-id="f982c-118">Create the app</span></span>

1. <span data-ttu-id="f982c-119">Rozpocznij Visual Studio dla komputerów Mac.</span><span class="sxs-lookup"><span data-stu-id="f982c-119">Start Visual Studio for Mac.</span></span>

1. <span data-ttu-id="f982c-120">W oknie uruchamiania wybierz pozycję **Nowy** .</span><span class="sxs-lookup"><span data-stu-id="f982c-120">Select **New** in the start window.</span></span>

   :::image type="content" source="media/with-visual-studio-mac/visual-studio-mac-new-project.png" alt-text="Przycisk Nowy na ekranie startowym Visual Studio dla komputerów Mac":::

1. <span data-ttu-id="f982c-122">W oknie dialogowym **Nowy projekt** wybierz pozycję **aplikacja** w węźle **Sieć Web i konsola** .</span><span class="sxs-lookup"><span data-stu-id="f982c-122">In the **New Project** dialog, select **App** under the **Web and Console** node.</span></span> <span data-ttu-id="f982c-123">Wybierz szablon **aplikacja konsoli** , a następnie wybierz przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="f982c-123">Select the **Console Application** template, and select **Next**.</span></span>

   :::image type="content" source="media/with-visual-studio-mac/visual-studio-mac-new-dialog.png" alt-text="Lista nowych szablonów projektu":::

1. <span data-ttu-id="f982c-125">Na liście rozwijanej **platforma docelowa** okna dialogowego **Konfigurowanie nowej aplikacji konsolowej** wybierz pozycję **.NET 5,0** i wybierz pozycję **dalej**.</span><span class="sxs-lookup"><span data-stu-id="f982c-125">In the **Target Framework** drop-down of the **Configure your new Console Application** dialog, select **.NET 5.0**, and select **Next**.</span></span>

1. <span data-ttu-id="f982c-126">Wpisz "HelloWorld" jako **nazwę projektu**, a następnie wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f982c-126">Type "HelloWorld" for the **Project Name**, and select **Create**.</span></span>

   :::image type="content" source="media/with-visual-studio-mac/visual-studio-mac-new-options.png" alt-text="Okno dialogowe Konfigurowanie nowej aplikacji konsolowej":::

<span data-ttu-id="f982c-128">Szablon tworzy prostą aplikację "Hello world".</span><span class="sxs-lookup"><span data-stu-id="f982c-128">The template creates a simple "Hello World" application.</span></span> <span data-ttu-id="f982c-129">Wywołuje metodę, <xref:System.Console.WriteLine(System.String)?displayProperty=nameWithType> Aby wyświetlić "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="f982c-129">It calls the <xref:System.Console.WriteLine(System.String)?displayProperty=nameWithType> method to display "Hello World!"</span></span> <span data-ttu-id="f982c-130">w oknie terminalu.</span><span class="sxs-lookup"><span data-stu-id="f982c-130">in the terminal window.</span></span>

<span data-ttu-id="f982c-131">Kod szablonu definiuje klasę, `Program` przy użyciu pojedynczej metody, `Main` która przyjmuje <xref:System.String> tablicę jako argument:</span><span class="sxs-lookup"><span data-stu-id="f982c-131">The template code defines a class, `Program`, with a single method, `Main`, that takes a <xref:System.String> array as an argument:</span></span>

```csharp
using System;

namespace HelloWorld
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
        }
    }
}
```

<span data-ttu-id="f982c-132">`Main` jest punktem wejścia aplikacji, metoda, która jest wywoływana automatycznie przez środowisko uruchomieniowe podczas uruchamiania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f982c-132">`Main` is the application entry point, the method that's called automatically by the runtime when it launches the application.</span></span> <span data-ttu-id="f982c-133">Wszystkie argumenty wiersza polecenia dostarczone podczas uruchamiania aplikacji są dostępne w `args` tablicy.</span><span class="sxs-lookup"><span data-stu-id="f982c-133">Any command-line arguments supplied when the application is launched are available in the `args` array.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="f982c-134">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="f982c-134">Run the app</span></span>

1. <span data-ttu-id="f982c-135">Naciśnij pozycję <kbd>⌥</kbd><kbd>⌘</kbd><kbd>↵</kbd> (<kbd>Option</kbd> + <kbd>Command</kbd> + <kbd>Enter</kbd>), aby uruchomić aplikację bez debugowania.</span><span class="sxs-lookup"><span data-stu-id="f982c-135">Press <kbd>⌥</kbd><kbd>⌘</kbd><kbd>↵</kbd> (<kbd>option</kbd>+<kbd>command</kbd>+<kbd>enter</kbd>) to run the app without debugging.</span></span>

   :::image type="content" source="media/with-visual-studio-mac/visual-studio-mac-output.png" alt-text="Terminal zawiera Hello world!":::

1. <span data-ttu-id="f982c-137">Zamknij okno **terminalu** .</span><span class="sxs-lookup"><span data-stu-id="f982c-137">Close the **Terminal** window.</span></span>

## <a name="enhance-the-app"></a><span data-ttu-id="f982c-138">Ulepszanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="f982c-138">Enhance the app</span></span>

<span data-ttu-id="f982c-139">Podnieś poziom aplikacji, aby monitować użytkownika o jego nazwę i wyświetlić go wraz z datą i godziną.</span><span class="sxs-lookup"><span data-stu-id="f982c-139">Enhance the application to prompt the user for their name and display it along with the date and time.</span></span>

1. <span data-ttu-id="f982c-140">W *program.cs* Zastąp zawartość `Main` metody, która jest wierszem, który wywołuje `Console.WriteLine` , przy użyciu następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="f982c-140">In *Program.cs*, replace the contents of the `Main` method, which is the line that calls `Console.WriteLine`, with the following code:</span></span>

   :::code language="csharp" source="./snippets/with-visual-studio/csharp/Program.cs" id="MainMethod":::

   <span data-ttu-id="f982c-141">Ten kod wyświetla monit w oknie konsoli i czeka, aż użytkownik wprowadzi ciąg, a następnie klawisz <kbd>Enter</kbd> .</span><span class="sxs-lookup"><span data-stu-id="f982c-141">This code displays a prompt in the console window and waits until the user enters a string followed by the <kbd>enter</kbd> key.</span></span> <span data-ttu-id="f982c-142">Ten ciąg jest przechowywany w zmiennej o nazwie `name` .</span><span class="sxs-lookup"><span data-stu-id="f982c-142">It stores this string in a variable named `name`.</span></span> <span data-ttu-id="f982c-143">Pobiera również wartość <xref:System.DateTime.Now?displayProperty=nameWithType> właściwości, która zawiera bieżący czas lokalny i przypisuje go do zmiennej o nazwie `date` .</span><span class="sxs-lookup"><span data-stu-id="f982c-143">It also retrieves the value of the <xref:System.DateTime.Now?displayProperty=nameWithType> property, which contains the current local time, and assigns it to a variable named `date`.</span></span> <span data-ttu-id="f982c-144">I wyświetla te wartości w oknie konsoli.</span><span class="sxs-lookup"><span data-stu-id="f982c-144">And it displays these values in the console window.</span></span> <span data-ttu-id="f982c-145">Na koniec wyświetla monit w oknie konsoli i wywołuje <xref:System.Console.ReadKey(System.Boolean)?displayProperty=nameWithType> metodę, aby czekać na dane wejściowe użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f982c-145">Finally, it displays a prompt in the console window and calls the <xref:System.Console.ReadKey(System.Boolean)?displayProperty=nameWithType> method to wait for user input.</span></span>

   <span data-ttu-id="f982c-146">`\n`Reprezentuje znak nowego wiersza.</span><span class="sxs-lookup"><span data-stu-id="f982c-146">The `\n` represents a newline character.</span></span>

   <span data-ttu-id="f982c-147">Znak dolara ( `$` ) przed ciągiem umożliwia umieszczenie wyrażeń takich jak nazwy zmiennych w nawiasach klamrowych w ciągu.</span><span class="sxs-lookup"><span data-stu-id="f982c-147">The dollar sign (`$`) in front of a string lets you put expressions such as variable names in curly braces in the string.</span></span> <span data-ttu-id="f982c-148">Wartość wyrażenia jest wstawiana do ciągu zamiast wyrażenia.</span><span class="sxs-lookup"><span data-stu-id="f982c-148">The expression value is inserted into the string in place of the expression.</span></span> <span data-ttu-id="f982c-149">Ta składnia jest określana mianem [ciągów interpolowanych](../../csharp/language-reference/tokens/interpolated.md).</span><span class="sxs-lookup"><span data-stu-id="f982c-149">This syntax is referred to as [interpolated strings](../../csharp/language-reference/tokens/interpolated.md).</span></span>

1. <span data-ttu-id="f982c-150">Naciśnij pozycję <kbd>⌥</kbd><kbd>⌘</kbd><kbd>↵</kbd> (<kbd>Option</kbd> + <kbd>Command</kbd> + <kbd>Enter</kbd>), aby uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="f982c-150">Press <kbd>⌥</kbd><kbd>⌘</kbd><kbd>↵</kbd> (<kbd>option</kbd>+<kbd>command</kbd>+<kbd>enter</kbd>) to run the app.</span></span>

1. <span data-ttu-id="f982c-151">Odpowiedz na monit, wprowadzając nazwę i naciskając klawisz <kbd>Enter</kbd>.</span><span class="sxs-lookup"><span data-stu-id="f982c-151">Respond to the prompt by entering a name and pressing <kbd>enter</kbd>.</span></span>

   :::image type="content" source="media/with-visual-studio-mac/hello-world-update.png" alt-text="Terminal pokazuje zmodyfikowane dane wyjściowe programu":::

1. <span data-ttu-id="f982c-153">Zamknij Terminal.</span><span class="sxs-lookup"><span data-stu-id="f982c-153">Close the terminal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f982c-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f982c-154">Next steps</span></span>

<span data-ttu-id="f982c-155">W tym samouczku utworzono aplikację konsolową .NET.</span><span class="sxs-lookup"><span data-stu-id="f982c-155">In this tutorial, you created a .NET console application.</span></span> <span data-ttu-id="f982c-156">W następnym samouczku debugujesz aplikację.</span><span class="sxs-lookup"><span data-stu-id="f982c-156">In the next tutorial, you debug the app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f982c-157">Debugowanie aplikacji konsolowej .NET przy użyciu Visual Studio dla komputerów Mac</span><span class="sxs-lookup"><span data-stu-id="f982c-157">Debug a .NET console application using Visual Studio for Mac</span></span>](debugging-with-visual-studio-mac.md)
