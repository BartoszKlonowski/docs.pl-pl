---
title: Obsługa współużytkowania wątkowości w aplikacjach asynchronicznych (C#)
description: Dowiedz się, jak obsłużyć współużytkowania wątkowości w aplikacjach asynchronicznych C#, które odwołują się do przeprowadzenia operacji asynchronicznej przed zakończeniem z możliwymi nieoczekiwanymi wynikami.
ms.date: 07/20/2015
ms.assetid: 47c5075e-c448-45ce-9155-ed4e7e98c677
ms.openlocfilehash: fdd440d167b95268a5ae6de0e57a32f0fad66b7c
ms.sourcegitcommit: 40de8df14289e1e05b40d6e5c1daabd3c286d70c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/22/2020
ms.locfileid: "86925244"
---
# <a name="handling-reentrancy-in-async-apps-c"></a><span data-ttu-id="88171-103">Obsługa współużytkowania wątkowości w aplikacjach asynchronicznych (C#)</span><span class="sxs-lookup"><span data-stu-id="88171-103">Handling Reentrancy in Async Apps (C#)</span></span>

<span data-ttu-id="88171-104">Po dołączeniu kodu asynchronicznego do aplikacji należy rozważyć i prawdopodobnie zapobiec współużytkowania wątkowości, który odwołuje się do ponownego wprowadzania operacji asynchronicznej przed ukończeniem.</span><span class="sxs-lookup"><span data-stu-id="88171-104">When you include asynchronous code in your app, you should consider and possibly prevent reentrancy, which refers to reentering an asynchronous operation before it has completed.</span></span> <span data-ttu-id="88171-105">Jeśli nie zidentyfikujesz i obsłużysz możliwości współużytkowania wątkowości, może to spowodować nieoczekiwane wyniki.</span><span class="sxs-lookup"><span data-stu-id="88171-105">If you don't identify and handle possibilities for reentrancy, it can cause unexpected results.</span></span>

<span data-ttu-id="88171-106">**W tym temacie**</span><span class="sxs-lookup"><span data-stu-id="88171-106">**In this topic**</span></span>

- [<span data-ttu-id="88171-107">Rozpoznawanie współużytkowania wątkowości</span><span class="sxs-lookup"><span data-stu-id="88171-107">Recognizing Reentrancy</span></span>](#BKMK_RecognizingReentrancy)

- [<span data-ttu-id="88171-108">Obsługa współużytkowania wątkowości</span><span class="sxs-lookup"><span data-stu-id="88171-108">Handling Reentrancy</span></span>](#BKMK_HandlingReentrancy)

  - [<span data-ttu-id="88171-109">Wyłącz przycisk Start</span><span class="sxs-lookup"><span data-stu-id="88171-109">Disable the Start Button</span></span>](#BKMK_DisableTheStartButton)

  - [<span data-ttu-id="88171-110">Anuluj i ponownie uruchom operację</span><span class="sxs-lookup"><span data-stu-id="88171-110">Cancel and Restart the Operation</span></span>](#BKMK_CancelAndRestart)

  - [<span data-ttu-id="88171-111">Uruchamianie wielu operacji i Kolejkowanie danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="88171-111">Run Multiple Operations and Queue the Output</span></span>](#BKMK_RunMultipleOperations)

- [<span data-ttu-id="88171-112">Przeglądanie i uruchamianie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="88171-112">Reviewing and Running the Example App</span></span>](#BKMD_SettingUpTheExample)

> [!NOTE]
> <span data-ttu-id="88171-113">Aby uruchomić przykład, musisz mieć zainstalowany na komputerze program Visual Studio 2012 lub nowszy oraz .NET Framework 4,5 lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="88171-113">To run the example, you must have Visual Studio 2012 or newer and .NET Framework 4.5 or newer installed on your computer.</span></span>

> [!NOTE]
> <span data-ttu-id="88171-114">Transport Layer Security (TLS) w wersji 1,2 jest teraz minimalną wersją do użycia podczas opracowywania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="88171-114">Transport Layer Security (TLS) version 1.2 is now the minimum version to use in your app development.</span></span> <span data-ttu-id="88171-115">Jeśli aplikacja jest przeznaczona dla .NET Framework wersji wcześniejszej niż 4,7, zapoznaj się z poniższym artykułem dotyczącym [Transport Layer Security (TLS) najlepszych](../../../../framework/network-programming/tls.md)rozwiązań dotyczących usługi .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="88171-115">If your app targets a .NET Framework version earlier than 4.7, refer to the following article for [Transport Layer Security (TLS) best practices with .NET Framework](../../../../framework/network-programming/tls.md).</span></span>

## <a name="recognizing-reentrancy"></a><a name="BKMK_RecognizingReentrancy"></a><span data-ttu-id="88171-116">Rozpoznawanie współużytkowania wątkowości</span><span class="sxs-lookup"><span data-stu-id="88171-116">Recognizing Reentrancy</span></span>

<span data-ttu-id="88171-117">W przykładzie w tym temacie użytkownicy wybierają przycisk **Start** , aby zainicjować aplikację asynchroniczną, która pobiera serię witryn sieci Web i oblicza łączną liczbę pobieranych bajtów.</span><span class="sxs-lookup"><span data-stu-id="88171-117">In the example in this topic, users choose a **Start** button to initiate an asynchronous app that downloads a series of websites and calculates the total number of bytes that are downloaded.</span></span> <span data-ttu-id="88171-118">Synchroniczna wersja przykładu reaguje w taki sam sposób, niezależnie od tego, ile razy użytkownik wybierze przycisk, ponieważ po raz pierwszy wątek interfejsu użytkownika ignoruje te zdarzenia do momentu zakończenia działania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="88171-118">A synchronous version of the example would respond the same way regardless of how many times a user chooses the button because, after the first time, the UI thread ignores those events until the app finishes running.</span></span> <span data-ttu-id="88171-119">W aplikacji asynchronicznej jednak wątek interfejsu użytkownika nadal odpowiada i można ponownie wprowadzić operację asynchroniczną przed jej ukończeniem.</span><span class="sxs-lookup"><span data-stu-id="88171-119">In an asynchronous app, however, the UI thread continues to respond, and you might reenter the asynchronous operation before it has completed.</span></span>

<span data-ttu-id="88171-120">W poniższym przykładzie pokazano oczekiwane dane wyjściowe, jeśli użytkownik wybierze przycisk **Start** tylko raz.</span><span class="sxs-lookup"><span data-stu-id="88171-120">The following example shows the expected output if the user chooses the **Start** button only once.</span></span> <span data-ttu-id="88171-121">Zostanie wyświetlona lista pobranych witryn sieci Web z rozmiarem w bajtach każdej lokacji.</span><span class="sxs-lookup"><span data-stu-id="88171-121">A list of the downloaded websites appears with the size, in bytes, of each site.</span></span> <span data-ttu-id="88171-122">Całkowita liczba bajtów pojawia się na końcu.</span><span class="sxs-lookup"><span data-stu-id="88171-122">The total number of bytes appears at the end.</span></span>

```output
1. msdn.microsoft.com/library/hh191443.aspx                83732
2. msdn.microsoft.com/library/aa578028.aspx               205273
3. msdn.microsoft.com/library/jj155761.aspx                29019
4. msdn.microsoft.com/library/hh290140.aspx               117152
5. msdn.microsoft.com/library/hh524395.aspx                68959
6. msdn.microsoft.com/library/ms404677.aspx               197325
7. msdn.microsoft.com                                            42972
8. msdn.microsoft.com/library/ff730837.aspx               146159

TOTAL bytes returned:  890591
```

<span data-ttu-id="88171-123">Jeśli jednak użytkownik wybierze przycisk więcej niż raz, program obsługi zdarzeń jest wywoływany wielokrotnie, a proces pobierania jest ponownie wprowadzany za każdym razem.</span><span class="sxs-lookup"><span data-stu-id="88171-123">However, if the user chooses the button more than once, the event handler is invoked repeatedly, and the download process is reentered each time.</span></span> <span data-ttu-id="88171-124">W związku z tym kilka operacji asynchronicznych jest uruchomionych w tym samym czasie, dane wyjściowe pozostawią wyniki, a całkowita liczba bajtów jest myląca.</span><span class="sxs-lookup"><span data-stu-id="88171-124">As a result, several asynchronous operations are running at the same time, the output interleaves the results, and the total number of bytes is confusing.</span></span>

```output
1. msdn.microsoft.com/library/hh191443.aspx                83732
2. msdn.microsoft.com/library/aa578028.aspx               205273
3. msdn.microsoft.com/library/jj155761.aspx                29019
4. msdn.microsoft.com/library/hh290140.aspx               117152
5. msdn.microsoft.com/library/hh524395.aspx                68959
1. msdn.microsoft.com/library/hh191443.aspx                83732
2. msdn.microsoft.com/library/aa578028.aspx               205273
6. msdn.microsoft.com/library/ms404677.aspx               197325
3. msdn.microsoft.com/library/jj155761.aspx                29019
7. msdn.microsoft.com                                            42972
4. msdn.microsoft.com/library/hh290140.aspx               117152
8. msdn.microsoft.com/library/ff730837.aspx               146159

TOTAL bytes returned:  890591

5. msdn.microsoft.com/library/hh524395.aspx                68959
1. msdn.microsoft.com/library/hh191443.aspx                83732
2. msdn.microsoft.com/library/aa578028.aspx               205273
6. msdn.microsoft.com/library/ms404677.aspx               197325
3. msdn.microsoft.com/library/jj155761.aspx                29019
4. msdn.microsoft.com/library/hh290140.aspx               117152
7. msdn.microsoft.com                                            42972
5. msdn.microsoft.com/library/hh524395.aspx                68959
8. msdn.microsoft.com/library/ff730837.aspx               146159

TOTAL bytes returned:  890591

6. msdn.microsoft.com/library/ms404677.aspx               197325
7. msdn.microsoft.com                                            42972
8. msdn.microsoft.com/library/ff730837.aspx               146159

TOTAL bytes returned:  890591
```

<span data-ttu-id="88171-125">Możesz przejrzeć kod tworzący dane wyjściowe, przewijając do końca tego tematu.</span><span class="sxs-lookup"><span data-stu-id="88171-125">You can review the code that produces this output by scrolling to the end of this topic.</span></span> <span data-ttu-id="88171-126">Można eksperymentować z kodem, pobierając rozwiązanie na komputer lokalny, a następnie uruchamiając projekt WebsiteDownload lub używając kodu na końcu tego tematu w celu utworzenia własnego projektu.</span><span class="sxs-lookup"><span data-stu-id="88171-126">You can experiment with the code by downloading the solution to your local computer and then running the WebsiteDownload project or by using the code at the end of this topic to create your own project.</span></span> <span data-ttu-id="88171-127">Aby uzyskać więcej informacji i instrukcje, zobacz [przeglądanie i uruchamianie przykładowej aplikacji](#BKMD_SettingUpTheExample).</span><span class="sxs-lookup"><span data-stu-id="88171-127">For more information and instructions, see [Reviewing and Running the Example App](#BKMD_SettingUpTheExample).</span></span>

## <a name="handling-reentrancy"></a><a name="BKMK_HandlingReentrancy"></a><span data-ttu-id="88171-128">Obsługa współużytkowania wątkowości</span><span class="sxs-lookup"><span data-stu-id="88171-128">Handling Reentrancy</span></span>

<span data-ttu-id="88171-129">Możesz obsłużyć współużytkowania wątkowości na różne sposoby, w zależności od tego, co aplikacja ma robić.</span><span class="sxs-lookup"><span data-stu-id="88171-129">You can handle reentrancy in a variety of ways, depending on what you want your app to do.</span></span> <span data-ttu-id="88171-130">W tym temacie przedstawiono następujące przykłady:</span><span class="sxs-lookup"><span data-stu-id="88171-130">This topic presents the following examples:</span></span>

- [<span data-ttu-id="88171-131">Wyłącz przycisk Start</span><span class="sxs-lookup"><span data-stu-id="88171-131">Disable the Start Button</span></span>](#BKMK_DisableTheStartButton)

  <span data-ttu-id="88171-132">Wyłącz przycisk **Start** , gdy operacja jest uruchomiona, aby użytkownik nie mógł go przerwać.</span><span class="sxs-lookup"><span data-stu-id="88171-132">Disable the **Start** button while the operation is running so that the user can't interrupt it.</span></span>

- [<span data-ttu-id="88171-133">Anuluj i ponownie uruchom operację</span><span class="sxs-lookup"><span data-stu-id="88171-133">Cancel and Restart the Operation</span></span>](#BKMK_CancelAndRestart)

  <span data-ttu-id="88171-134">Anuluj wszystkie operacje, które nadal działają, gdy użytkownik wybierze ponownie przycisk **Start** , a następnie pozwól na kontynuowanie ostatnio żądanej operacji.</span><span class="sxs-lookup"><span data-stu-id="88171-134">Cancel any operation that is still running when the user chooses the **Start** button again, and then let the most recently requested operation continue.</span></span>

- [<span data-ttu-id="88171-135">Uruchamianie wielu operacji i Kolejkowanie danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="88171-135">Run Multiple Operations and Queue the Output</span></span>](#BKMK_RunMultipleOperations)

  <span data-ttu-id="88171-136">Zezwalaj na działanie wszystkich żądanych operacji asynchronicznie, ale koordynuj wyświetlanie danych wyjściowych, tak aby wyniki każdej operacji były wyświetlane razem i w określonej kolejności.</span><span class="sxs-lookup"><span data-stu-id="88171-136">Allow all requested operations to run asynchronously, but coordinate the display of output so that the results from each operation appear together and in order.</span></span>

### <a name="disable-the-start-button"></a><a name="BKMK_DisableTheStartButton"></a><span data-ttu-id="88171-137">Wyłącz przycisk Start</span><span class="sxs-lookup"><span data-stu-id="88171-137">Disable the Start Button</span></span>

<span data-ttu-id="88171-138">Można zablokować przycisk **Start** , gdy operacja jest uruchomiona, wyłączając przycisk w górnej części `StartButton_Click` procedury obsługi zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="88171-138">You can block the **Start** button while an operation is running by disabling the button at the top of the `StartButton_Click` event handler.</span></span> <span data-ttu-id="88171-139">Następnie można ponownie włączyć przycisk w `finally` bloku po zakończeniu operacji, aby umożliwić użytkownikom ponowne uruchomienie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="88171-139">You can then reenable the button from within a  `finally` block when the operation finishes so that users can run the app again.</span></span>

<span data-ttu-id="88171-140">Aby skonfigurować ten scenariusz, wprowadź następujące zmiany w kodzie podstawowym, który jest dostępny podczas [przeglądania i uruchamiania przykładowej aplikacji](#BKMD_SettingUpTheExample).</span><span class="sxs-lookup"><span data-stu-id="88171-140">To set up this scenario, make the following changes to the basic code that is provided in [Reviewing and Running the Example App](#BKMD_SettingUpTheExample).</span></span> <span data-ttu-id="88171-141">Możesz również pobrać ukończoną aplikację z [przykładów asynchronicznych: współużytkowania wątkowości w aplikacjach klasycznych platformy .NET](https://code.msdn.microsoft.com/Async-Sample-Preventing-a8489f06).</span><span class="sxs-lookup"><span data-stu-id="88171-141">You can also download the finished app from [Async Samples: Reentrancy in .NET Desktop Apps](https://code.msdn.microsoft.com/Async-Sample-Preventing-a8489f06).</span></span> <span data-ttu-id="88171-142">Nazwa projektu to DisableStartButton.</span><span class="sxs-lookup"><span data-stu-id="88171-142">The name of the project is DisableStartButton.</span></span>

```csharp
private async void StartButton_Click(object sender, RoutedEventArgs e)
{
    // This line is commented out to make the results clearer in the output.
    //ResultsTextBox.Text = "";

    // ***Disable the Start button until the downloads are complete.
    StartButton.IsEnabled = false;

    try
    {
        await AccessTheWebAsync();
    }
    catch (Exception)
    {
        ResultsTextBox.Text += "\r\nDownloads failed.";
    }
    // ***Enable the Start button in case you want to run the program again.
    finally
    {
        StartButton.IsEnabled = true;
    }
}
```

<span data-ttu-id="88171-143">W wyniku zmian przycisk nie odpowiada, podczas gdy `AccessTheWebAsync` Pobiera witryny sieci Web, więc nie można ponownie wprowadzić tego procesu.</span><span class="sxs-lookup"><span data-stu-id="88171-143">As a result of the changes, the button doesn't respond while `AccessTheWebAsync` is downloading the websites, so the process can't be reentered.</span></span>

### <a name="cancel-and-restart-the-operation"></a><a name="BKMK_CancelAndRestart"></a><span data-ttu-id="88171-144">Anuluj i ponownie uruchom operację</span><span class="sxs-lookup"><span data-stu-id="88171-144">Cancel and Restart the Operation</span></span>

<span data-ttu-id="88171-145">Zamiast wyłączać przycisk **Start** , można zachować aktywny przycisk, ale jeśli użytkownik ponownie wybierze ten przycisk, należy anulować operację, która jest już uruchomiona, i pozostawić ostatnio uruchomioną operację.</span><span class="sxs-lookup"><span data-stu-id="88171-145">Instead of disabling the **Start** button, you can keep the button active but, if the user chooses that button again, cancel the operation that's already running and let the most recently started operation continue.</span></span>

<span data-ttu-id="88171-146">Aby uzyskać więcej informacji na temat anulowania, zobacz [dostrajanie aplikacji asynchronicznej (C#)](./fine-tuning-your-async-application.md).</span><span class="sxs-lookup"><span data-stu-id="88171-146">For more information about cancellation, see [Fine-Tuning Your Async Application (C#)](./fine-tuning-your-async-application.md).</span></span>

<span data-ttu-id="88171-147">Aby skonfigurować ten scenariusz, wprowadź następujące zmiany w kodzie podstawowym, który jest dostępny podczas [przeglądania i uruchamiania przykładowej aplikacji](#BKMD_SettingUpTheExample).</span><span class="sxs-lookup"><span data-stu-id="88171-147">To set up this scenario, make the following changes to the basic code that is provided in [Reviewing and Running the Example App](#BKMD_SettingUpTheExample).</span></span> <span data-ttu-id="88171-148">Możesz również pobrać ukończoną aplikację z [przykładów asynchronicznych: współużytkowania wątkowości w aplikacjach klasycznych platformy .NET](https://code.msdn.microsoft.com/Async-Sample-Preventing-a8489f06).</span><span class="sxs-lookup"><span data-stu-id="88171-148">You can also download the finished app from [Async Samples: Reentrancy in .NET Desktop Apps](https://code.msdn.microsoft.com/Async-Sample-Preventing-a8489f06).</span></span> <span data-ttu-id="88171-149">Nazwa projektu to CancelAndRestart.</span><span class="sxs-lookup"><span data-stu-id="88171-149">The name of the project is CancelAndRestart.</span></span>

1. <span data-ttu-id="88171-150">Zadeklaruj <xref:System.Threading.CancellationTokenSource> zmienną, `cts` która znajduje się w zakresie dla wszystkich metod.</span><span class="sxs-lookup"><span data-stu-id="88171-150">Declare a <xref:System.Threading.CancellationTokenSource> variable, `cts`, that's in scope for all methods.</span></span>

    ```csharp
    public partial class MainWindow : Window   // Or class MainPage
    {
        // *** Declare a System.Threading.CancellationTokenSource.
        CancellationTokenSource cts;
    ```

2. <span data-ttu-id="88171-151">W programie `StartButton_Click` Ustal, czy operacja jest już w toku.</span><span class="sxs-lookup"><span data-stu-id="88171-151">In `StartButton_Click`, determine whether an operation is already underway.</span></span> <span data-ttu-id="88171-152">Jeśli wartość `cts` jest równa null, żadna operacja nie jest już aktywna.</span><span class="sxs-lookup"><span data-stu-id="88171-152">If the value of `cts` is null, no operation is already active.</span></span> <span data-ttu-id="88171-153">Jeśli wartość nie jest równa null, operacja, która jest już uruchomiona, została anulowana.</span><span class="sxs-lookup"><span data-stu-id="88171-153">If the value isn't null, the operation that is already running is canceled.</span></span>

    ```csharp
    // *** If a download process is already underway, cancel it.
    if (cts != null)
    {
        cts.Cancel();
    }
    ```

3. <span data-ttu-id="88171-154">Ustaw `cts` inną wartość, która reprezentuje bieżący proces.</span><span class="sxs-lookup"><span data-stu-id="88171-154">Set `cts` to a different value that represents the current process.</span></span>

    ```csharp
    // *** Now set cts to a new value that you can use to cancel the current process
    // if the button is chosen again.
    CancellationTokenSource newCTS = new CancellationTokenSource();
    cts = newCTS;
    ```

4. <span data-ttu-id="88171-155">Na końcu `StartButton_Click` bieżący proces jest zakończony, więc ustaw wartość z `cts` powrotem na wartość null.</span><span class="sxs-lookup"><span data-stu-id="88171-155">At the end of `StartButton_Click`, the current process is complete, so set the value of `cts` back to null.</span></span>

    ```csharp
    // *** When the process is complete, signal that another process can begin.
    if (cts == newCTS)
        cts = null;
    ```

<span data-ttu-id="88171-156">Poniższy kod przedstawia wszystkie zmiany w `StartButton_Click` .</span><span class="sxs-lookup"><span data-stu-id="88171-156">The following code shows all the changes in `StartButton_Click`.</span></span> <span data-ttu-id="88171-157">Dodatki są oznaczone gwiazdkami.</span><span class="sxs-lookup"><span data-stu-id="88171-157">The additions are marked with asterisks.</span></span>

```csharp
private async void StartButton_Click(object sender, RoutedEventArgs e)
{
    // This line is commented out to make the results clearer in the output.
    //ResultsTextBox.Clear();

    // *** If a download process is already underway, cancel it.
    if (cts != null)
    {
        cts.Cancel();
    }

    // *** Now set cts to cancel the current process if the button is chosen again.
    CancellationTokenSource newCTS = new CancellationTokenSource();
    cts = newCTS;

    try
    {
        // ***Send cts.Token to carry the message if there is a cancellation request.
        await AccessTheWebAsync(cts.Token);

    }
    // *** Catch cancellations separately.
    catch (OperationCanceledException)
    {
        ResultsTextBox.Text += "\r\nDownloads canceled.\r\n";
    }
    catch (Exception)
    {
        ResultsTextBox.Text += "\r\nDownloads failed.\r\n";
    }
    // *** When the process is complete, signal that another process can proceed.
    if (cts == newCTS)
        cts = null;
}
```

<span data-ttu-id="88171-158">`AccessTheWebAsync`Wprowadź następujące zmiany w programie.</span><span class="sxs-lookup"><span data-stu-id="88171-158">In `AccessTheWebAsync`, make the following changes.</span></span>

- <span data-ttu-id="88171-159">Dodaj parametr, aby zaakceptować token anulowania z `StartButton_Click` .</span><span class="sxs-lookup"><span data-stu-id="88171-159">Add a parameter to accept the cancellation token from `StartButton_Click`.</span></span>

- <span data-ttu-id="88171-160">Użyj <xref:System.Net.Http.HttpClient.GetAsync%2A> metody, aby pobrać witryny sieci Web, ponieważ `GetAsync` akceptuje <xref:System.Threading.CancellationToken> argument.</span><span class="sxs-lookup"><span data-stu-id="88171-160">Use the <xref:System.Net.Http.HttpClient.GetAsync%2A> method to download the websites because `GetAsync` accepts a <xref:System.Threading.CancellationToken> argument.</span></span>

- <span data-ttu-id="88171-161">Przed wywołaniem `DisplayResults` , aby wyświetlić wyniki dla każdej pobranej witryny sieci Web, sprawdź, czy `ct` bieżąca operacja nie została anulowana.</span><span class="sxs-lookup"><span data-stu-id="88171-161">Before calling `DisplayResults` to display the results for each downloaded website, check `ct` to verify that the current operation hasn't been canceled.</span></span>

<span data-ttu-id="88171-162">Poniższy kod przedstawia te zmiany, które są oznaczone gwiazdkami.</span><span class="sxs-lookup"><span data-stu-id="88171-162">The following code shows these changes, which are marked with asterisks.</span></span>

```csharp
// *** Provide a parameter for the CancellationToken from StartButton_Click.
async Task AccessTheWebAsync(CancellationToken ct)
{
    // Declare an HttpClient object.
    HttpClient client = new HttpClient();

    // Make a list of web addresses.
    List<string> urlList = SetUpURLList();

    var total = 0;
    var position = 0;

    foreach (var url in urlList)
    {
        // *** Use the HttpClient.GetAsync method because it accepts a
        // cancellation token.
        HttpResponseMessage response = await client.GetAsync(url, ct);

        // *** Retrieve the website contents from the HttpResponseMessage.
        byte[] urlContents = await response.Content.ReadAsByteArrayAsync();

        // *** Check for cancellations before displaying information about the
        // latest site.
        ct.ThrowIfCancellationRequested();

        DisplayResults(url, urlContents, ++position);

        // Update the total.
        total += urlContents.Length;
    }

    // Display the total count for all of the websites.
    ResultsTextBox.Text +=
        $"\r\n\r\nTOTAL bytes returned:  {total}\r\n";
}
```

<span data-ttu-id="88171-163">Jeśli wybierzesz przycisk **Start** kilka razy podczas działania tej aplikacji, powinny one generować wyniki podobne do następujących.</span><span class="sxs-lookup"><span data-stu-id="88171-163">If you choose the **Start** button several times while this app is running, it should produce results that resemble the following output.</span></span>

```output
1. msdn.microsoft.com/library/hh191443.aspx                83732
2. msdn.microsoft.com/library/aa578028.aspx               205273
3. msdn.microsoft.com/library/jj155761.aspx                29019
4. msdn.microsoft.com/library/hh290140.aspx               122505
5. msdn.microsoft.com/library/hh524395.aspx                68959
6. msdn.microsoft.com/library/ms404677.aspx               197325
Download canceled.

1. msdn.microsoft.com/library/hh191443.aspx                83732
2. msdn.microsoft.com/library/aa578028.aspx               205273
3. msdn.microsoft.com/library/jj155761.aspx                29019
Download canceled.

1. msdn.microsoft.com/library/hh191443.aspx                83732
2. msdn.microsoft.com/library/aa578028.aspx               205273
3. msdn.microsoft.com/library/jj155761.aspx                29019
4. msdn.microsoft.com/library/hh290140.aspx               117152
5. msdn.microsoft.com/library/hh524395.aspx                68959
6. msdn.microsoft.com/library/ms404677.aspx               197325
7. msdn.microsoft.com                                            42972
8. msdn.microsoft.com/library/ff730837.aspx               146159

TOTAL bytes returned:  890591
```

<span data-ttu-id="88171-164">Aby wyeliminować częściowe listy, Usuń komentarz z pierwszego wiersza kodu w, `StartButton_Click` Aby wyczyścić pole tekstowe za każdym razem, gdy użytkownik ponownie uruchomi operację.</span><span class="sxs-lookup"><span data-stu-id="88171-164">To eliminate the partial lists, uncomment the first line of code in `StartButton_Click` to clear the text box each time the user restarts the operation.</span></span>

### <a name="run-multiple-operations-and-queue-the-output"></a><a name="BKMK_RunMultipleOperations"></a><span data-ttu-id="88171-165">Uruchamianie wielu operacji i Kolejkowanie danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="88171-165">Run Multiple Operations and Queue the Output</span></span>

<span data-ttu-id="88171-166">Trzeci przykład to najbardziej skomplikowany sposób, w jaki aplikacja uruchamia kolejną operację asynchroniczną za każdym razem, gdy użytkownik wybierze przycisk **Start** , a wszystkie operacje są wykonywane do ukończenia.</span><span class="sxs-lookup"><span data-stu-id="88171-166">This third example is the most complicated in that the app starts another asynchronous operation each time that the user chooses the **Start** button, and all the operations run to completion.</span></span> <span data-ttu-id="88171-167">Wszystkie żądane operacje pobierają witryny sieci Web z listy asynchronicznie, ale dane wyjściowe operacji są prezentowane sekwencyjnie.</span><span class="sxs-lookup"><span data-stu-id="88171-167">All the requested operations download websites from the list asynchronously, but the output from the operations is presented sequentially.</span></span> <span data-ttu-id="88171-168">Oznacza to, że rzeczywista czynność pobierania jest przeplatana, ponieważ dane wyjściowe [rozpoznawania współużytkowania wątkowości](#BKMK_RecognizingReentrancy) są wyświetlane, ale lista wyników dla każdej grupy jest prezentowana osobno.</span><span class="sxs-lookup"><span data-stu-id="88171-168">That is, the actual downloading activity is interleaved, as the output in [Recognizing Reentrancy](#BKMK_RecognizingReentrancy) shows, but the list of results for each group is presented separately.</span></span>

<span data-ttu-id="88171-169">Operacje współużytkują globalny <xref:System.Threading.Tasks.Task> , `pendingWork` , który służy jako strażnik dla procesu wyświetlania.</span><span class="sxs-lookup"><span data-stu-id="88171-169">The operations share a global <xref:System.Threading.Tasks.Task>, `pendingWork`, which serves as a gatekeeper for the display process.</span></span>

<span data-ttu-id="88171-170">Aby skonfigurować ten scenariusz, wprowadź następujące zmiany w kodzie podstawowym, który jest dostępny podczas [przeglądania i uruchamiania przykładowej aplikacji](#BKMD_SettingUpTheExample).</span><span class="sxs-lookup"><span data-stu-id="88171-170">To set up this scenario, make the following changes to the basic code that is provided in [Reviewing and Running the Example App](#BKMD_SettingUpTheExample).</span></span> <span data-ttu-id="88171-171">Możesz również pobrać ukończoną aplikację z [przykładów asynchronicznych: współużytkowania wątkowości w aplikacjach klasycznych platformy .NET](https://code.msdn.microsoft.com/Async-Sample-Preventing-a8489f06).</span><span class="sxs-lookup"><span data-stu-id="88171-171">You can also download the finished app from [Async Samples: Reentrancy in .NET Desktop Apps](https://code.msdn.microsoft.com/Async-Sample-Preventing-a8489f06).</span></span> <span data-ttu-id="88171-172">Nazwa projektu to QueueResults.</span><span class="sxs-lookup"><span data-stu-id="88171-172">The name of the project is QueueResults.</span></span>

<span data-ttu-id="88171-173">Poniższe dane wyjściowe pokazują wynik, jeśli użytkownik wybierze przycisk **Start** tylko raz.</span><span class="sxs-lookup"><span data-stu-id="88171-173">The following output shows the result if the user chooses the **Start** button only once.</span></span> <span data-ttu-id="88171-174">Etykieta litery, A, wskazuje, że wynik jest z pierwszego momentu wybrania przycisku **Start** .</span><span class="sxs-lookup"><span data-stu-id="88171-174">The letter label, A, indicates that the result is from the first time the **Start** button is chosen.</span></span> <span data-ttu-id="88171-175">Liczby pokazują kolejność adresów URL na liście celów pobierania.</span><span class="sxs-lookup"><span data-stu-id="88171-175">The numbers show the order of the URLs in the list of download targets.</span></span>

```output
#Starting group A.
#Task assigned for group A.

A-1. msdn.microsoft.com/library/hh191443.aspx                87389
A-2. msdn.microsoft.com/library/aa578028.aspx               209858
A-3. msdn.microsoft.com/library/jj155761.aspx                30870
A-4. msdn.microsoft.com/library/hh290140.aspx               119027
A-5. msdn.microsoft.com/library/hh524395.aspx                71260
A-6. msdn.microsoft.com/library/ms404677.aspx               199186
A-7. msdn.microsoft.com                                            53266
A-8. msdn.microsoft.com/library/ff730837.aspx               148020

TOTAL bytes returned:  918876

#Group A is complete.
```

<span data-ttu-id="88171-176">Jeśli użytkownik wybierze przycisk **Start** trzy razy, aplikacja generuje dane wyjściowe podobne do następujących wierszy.</span><span class="sxs-lookup"><span data-stu-id="88171-176">If the user chooses the **Start** button three times, the app produces output that resembles the following lines.</span></span> <span data-ttu-id="88171-177">Linie informacyjne, które zaczynają się od znaku funta (#) śledzą postęp aplikacji.</span><span class="sxs-lookup"><span data-stu-id="88171-177">The information lines that start with a pound sign (#) trace the progress of the application.</span></span>

```output
#Starting group A.
#Task assigned for group A.

A-1. msdn.microsoft.com/library/hh191443.aspx                87389
A-2. msdn.microsoft.com/library/aa578028.aspx               207089
A-3. msdn.microsoft.com/library/jj155761.aspx                30870
A-4. msdn.microsoft.com/library/hh290140.aspx               119027
A-5. msdn.microsoft.com/library/hh524395.aspx                71259
A-6. msdn.microsoft.com/library/ms404677.aspx               199185

#Starting group B.
#Task assigned for group B.

A-7. msdn.microsoft.com                                            53266

#Starting group C.
#Task assigned for group C.

A-8. msdn.microsoft.com/library/ff730837.aspx               148010

TOTAL bytes returned:  916095

B-1. msdn.microsoft.com/library/hh191443.aspx                87389
B-2. msdn.microsoft.com/library/aa578028.aspx               207089
B-3. msdn.microsoft.com/library/jj155761.aspx                30870
B-4. msdn.microsoft.com/library/hh290140.aspx               119027
B-5. msdn.microsoft.com/library/hh524395.aspx                71260
B-6. msdn.microsoft.com/library/ms404677.aspx               199186

#Group A is complete.

B-7. msdn.microsoft.com                                            53266
B-8. msdn.microsoft.com/library/ff730837.aspx               148010

TOTAL bytes returned:  916097

C-1. msdn.microsoft.com/library/hh191443.aspx                87389
C-2. msdn.microsoft.com/library/aa578028.aspx               207089

#Group B is complete.

C-3. msdn.microsoft.com/library/jj155761.aspx                30870
C-4. msdn.microsoft.com/library/hh290140.aspx               119027
C-5. msdn.microsoft.com/library/hh524395.aspx                72765
C-6. msdn.microsoft.com/library/ms404677.aspx               199186
C-7. msdn.microsoft.com                                            56190
C-8. msdn.microsoft.com/library/ff730837.aspx               148010

TOTAL bytes returned:  920526

#Group C is complete.
```

<span data-ttu-id="88171-178">Grupy B i C rozpoczynają się przed zakończeniem grupy A, ale dane wyjściowe dla każdej grupy są wyświetlane oddzielnie.</span><span class="sxs-lookup"><span data-stu-id="88171-178">Groups B and C start before group A has finished, but the output for the each group appears separately.</span></span> <span data-ttu-id="88171-179">Wszystkie dane wyjściowe dla grupy A są wyświetlane jako pierwsze, po których następuje wszystkie dane wyjściowe dla grupy B, a następnie wszystkie dane wyjściowe dla grupy C. Aplikacja zawsze wyświetla grupy w kolejności i, dla każdej grupy, zawsze wyświetla informacje o poszczególnych witrynach sieci Web w kolejności, w jakiej znajdują się na liście adresów URL.</span><span class="sxs-lookup"><span data-stu-id="88171-179">All the output for group A appears first, followed by all the output for group B, and then all the output for group C. The app always displays the groups in order and, for each group, always displays the information about the individual websites in the order that the URLs appear in the list of URLs.</span></span>

<span data-ttu-id="88171-180">Nie można jednak przewidzieć kolejności, w której istnieją pliki do pobrania.</span><span class="sxs-lookup"><span data-stu-id="88171-180">However, you can't predict the order in which the downloads actually happen.</span></span> <span data-ttu-id="88171-181">Po rozpoczęciu wielu grup zadania pobierania, które generują, są aktywne.</span><span class="sxs-lookup"><span data-stu-id="88171-181">After multiple groups have been started, the download tasks that they generate are all active.</span></span> <span data-ttu-id="88171-182">Nie można założyć, że wartość-1 zostanie pobrana przed B-1 i nie można założyć, że A-1 zostanie pobrane przed-2.</span><span class="sxs-lookup"><span data-stu-id="88171-182">You can't assume that A-1 will be downloaded before B-1, and you can't assume that A-1 will be downloaded before A-2.</span></span>

#### <a name="global-definitions"></a><span data-ttu-id="88171-183">Definicje globalne</span><span class="sxs-lookup"><span data-stu-id="88171-183">Global Definitions</span></span>

<span data-ttu-id="88171-184">Przykładowy kod zawiera następujące dwie deklaracje globalne, które są widoczne dla wszystkich metod.</span><span class="sxs-lookup"><span data-stu-id="88171-184">The sample code contains the following two global declarations that are visible from all methods.</span></span>

```csharp
public partial class MainWindow : Window  // Class MainPage in Windows Store app.
{
    // ***Declare the following variables where all methods can access them.
    private Task pendingWork = null;
    private char group = (char)('A' - 1);
```

<span data-ttu-id="88171-185">`Task`Zmienna, `pendingWork` , widzi proces wyświetlania i uniemożliwia każdej grupie przerwanie operacji wyświetlania innej grupy.</span><span class="sxs-lookup"><span data-stu-id="88171-185">The `Task` variable, `pendingWork`, oversees the display process and prevents any group from interrupting another group's display operation.</span></span> <span data-ttu-id="88171-186">Zmienna znaku, `group` , oznacza dane wyjściowe z różnych grup, aby sprawdzić, czy wyniki są wyświetlane w oczekiwanej kolejności.</span><span class="sxs-lookup"><span data-stu-id="88171-186">The character variable, `group`, labels the output from different groups to verify that results appear in the expected order.</span></span>

#### <a name="the-click-event-handler"></a><span data-ttu-id="88171-187">Procedura obsługi zdarzeń kliknięcia</span><span class="sxs-lookup"><span data-stu-id="88171-187">The Click Event Handler</span></span>

<span data-ttu-id="88171-188">Program obsługi zdarzeń, `StartButton_Click` , zwiększa literę grupy za każdym razem, gdy użytkownik wybierze przycisk **Start** .</span><span class="sxs-lookup"><span data-stu-id="88171-188">The event handler, `StartButton_Click`, increments the group letter each time the user chooses the **Start** button.</span></span> <span data-ttu-id="88171-189">Następnie procedura obsługi wywołuje `AccessTheWebAsync` do uruchomienia operacji pobierania.</span><span class="sxs-lookup"><span data-stu-id="88171-189">Then the handler calls `AccessTheWebAsync` to run the downloading operation.</span></span>

```csharp
private async void StartButton_Click(object sender, RoutedEventArgs e)
{
    // ***Verify that each group's results are displayed together, and that
    // the groups display in order, by marking each group with a letter.
    group = (char)(group + 1);
    ResultsTextBox.Text += $"\r\n\r\n#Starting group {group}.";

    try
    {
        // *** Pass the group value to AccessTheWebAsync.
        char finishedGroup = await AccessTheWebAsync(group);

        // The following line verifies a successful return from the download and
        // display procedures.
        ResultsTextBox.Text += $"\r\n\r\n#Group {finishedGroup} is complete.\r\n";
    }
    catch (Exception)
    {
        ResultsTextBox.Text += "\r\nDownloads failed.";
    }
}
```

#### <a name="the-accessthewebasync-method"></a><span data-ttu-id="88171-190">Metoda AccessTheWebAsync</span><span class="sxs-lookup"><span data-stu-id="88171-190">The AccessTheWebAsync Method</span></span>

<span data-ttu-id="88171-191">Ten przykład dzieli `AccessTheWebAsync` na dwie metody.</span><span class="sxs-lookup"><span data-stu-id="88171-191">This example splits `AccessTheWebAsync` into two methods.</span></span> <span data-ttu-id="88171-192">Pierwsza metoda, `AccessTheWebAsync` , uruchamia wszystkie zadania pobierania dla grupy i konfiguruje, `pendingWork` Aby kontrolować proces wyświetlania.</span><span class="sxs-lookup"><span data-stu-id="88171-192">The first method, `AccessTheWebAsync`, starts all the download tasks for a group and sets up `pendingWork` to control the display process.</span></span> <span data-ttu-id="88171-193">Metoda używa języka Integrated Query (zapytanie LINQ) i <xref:System.Linq.Enumerable.ToArray%2A> do uruchamiania wszystkich zadań pobierania w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="88171-193">The method uses a Language Integrated Query (LINQ query) and <xref:System.Linq.Enumerable.ToArray%2A> to start all the download tasks at the same time.</span></span>

<span data-ttu-id="88171-194">`AccessTheWebAsync`następnie wywołuje `FinishOneGroupAsync` do czeka na zakończenie każdego pobierania i wyświetla jego długość.</span><span class="sxs-lookup"><span data-stu-id="88171-194">`AccessTheWebAsync` then calls `FinishOneGroupAsync` to await the completion of each download and display its length.</span></span>

<span data-ttu-id="88171-195">`FinishOneGroupAsync`zwraca zadanie, które jest przypisane do elementu `pendingWork` w `AccessTheWebAsync` .</span><span class="sxs-lookup"><span data-stu-id="88171-195">`FinishOneGroupAsync` returns a task that's assigned to `pendingWork` in `AccessTheWebAsync`.</span></span> <span data-ttu-id="88171-196">Ta wartość uniemożliwia przerwanie przez inną operację przed ukończeniem zadania.</span><span class="sxs-lookup"><span data-stu-id="88171-196">That value prevents interruption by another operation before the task is complete.</span></span>

```csharp
private async Task<char> AccessTheWebAsync(char grp)
{
    HttpClient client = new HttpClient();

    // Make a list of the web addresses to download.
    List<string> urlList = SetUpURLList();

    // ***Kick off the downloads. The application of ToArray activates all the download tasks.
    Task<byte[]>[] getContentTasks = urlList.Select(url => client.GetByteArrayAsync(url)).ToArray();

    // ***Call the method that awaits the downloads and displays the results.
    // Assign the Task that FinishOneGroupAsync returns to the gatekeeper task, pendingWork.
    pendingWork = FinishOneGroupAsync(urlList, getContentTasks, grp);

    ResultsTextBox.Text += $"\r\n#Task assigned for group {grp}. Download tasks are active.\r\n";

    // ***This task is complete when a group has finished downloading and displaying.
    await pendingWork;

    // You can do other work here or just return.
    return grp;
}
```

#### <a name="the-finishonegroupasync-method"></a><span data-ttu-id="88171-197">Metoda FinishOneGroupAsync</span><span class="sxs-lookup"><span data-stu-id="88171-197">The FinishOneGroupAsync Method</span></span>

<span data-ttu-id="88171-198">Ta metoda przechodzi przez zadania pobierania w grupie, czekające na każdą z nich, wyświetlając długość pobranej witryny sieci Web i dodając do niej długość.</span><span class="sxs-lookup"><span data-stu-id="88171-198">This method cycles through the download tasks in a group, awaiting each one, displaying the length of the downloaded website, and adding the length to the total.</span></span>

<span data-ttu-id="88171-199">Pierwsza instrukcja w programie `FinishOneGroupAsync` używa do upewnienia się `pendingWork` , że wprowadzenie metody nie zakłóca operacji, która jest już w procesie wyświetlania lub już oczekuje.</span><span class="sxs-lookup"><span data-stu-id="88171-199">The first statement in `FinishOneGroupAsync` uses `pendingWork` to make sure that entering the method doesn't interfere with an operation that is already in the display process or that's already waiting.</span></span> <span data-ttu-id="88171-200">Jeśli taka operacja jest w toku, operacja wprowadzania musi czekać na jej włączenie.</span><span class="sxs-lookup"><span data-stu-id="88171-200">If such an operation is in progress, the entering operation must wait its turn.</span></span>

```csharp
private async Task FinishOneGroupAsync(List<string> urls, Task<byte[]>[] contentTasks, char grp)
{
    // ***Wait for the previous group to finish displaying results.
    if (pendingWork != null) await pendingWork;

    int total = 0;

    // contentTasks is the array of Tasks that was created in AccessTheWebAsync.
    for (int i = 0; i < contentTasks.Length; i++)
    {
        // Await the download of a particular URL, and then display the URL and
        // its length.
        byte[] content = await contentTasks[i];
        DisplayResults(urls[i], content, i, grp);
        total += content.Length;
    }

    // Display the total count for all of the websites.
    ResultsTextBox.Text +=
        $"\r\n\r\nTOTAL bytes returned:  {total}\r\n";
}
```

#### <a name="points-of-interest"></a><span data-ttu-id="88171-201">Punkty orientacyjne</span><span class="sxs-lookup"><span data-stu-id="88171-201">Points of Interest</span></span>

<span data-ttu-id="88171-202">Linie informacyjne, które zaczynają się od znaku funta (#) w danych wyjściowych, wyjaśniają sposób działania tego przykładu.</span><span class="sxs-lookup"><span data-stu-id="88171-202">The information lines that start with a pound sign (#) in the output clarify how this example works.</span></span>

<span data-ttu-id="88171-203">Dane wyjściowe przedstawiają następujące wzorce.</span><span class="sxs-lookup"><span data-stu-id="88171-203">The output shows the following patterns.</span></span>

- <span data-ttu-id="88171-204">Grupę można uruchomić, gdy poprzednia grupa wyświetla dane wyjściowe, ale nie przerywa się wyświetlania danych wyjściowych poprzedniej grupy.</span><span class="sxs-lookup"><span data-stu-id="88171-204">A group can be started while a previous group is displaying its output, but the display of the previous group's output isn't interrupted.</span></span>

    ```output
    #Starting group A.
    #Task assigned for group A. Download tasks are active.

    A-1. msdn.microsoft.com/library/hh191443.aspx                87389
    A-2. msdn.microsoft.com/library/aa578028.aspx               207089
    A-3. msdn.microsoft.com/library/jj155761.aspx                30870
    A-4. msdn.microsoft.com/library/hh290140.aspx               119037
    A-5. msdn.microsoft.com/library/hh524395.aspx                71260

    #Starting group B.
    #Task assigned for group B. Download tasks are active.

    A-6. msdn.microsoft.com/library/ms404677.aspx               199186
    A-7. msdn.microsoft.com                                            53078
    A-8. msdn.microsoft.com/library/ff730837.aspx               148010

    TOTAL bytes returned:  915919

    B-1. msdn.microsoft.com/library/hh191443.aspx                87388
    B-2. msdn.microsoft.com/library/aa578028.aspx               207089
    B-3. msdn.microsoft.com/library/jj155761.aspx                30870

    #Group A is complete.

    B-4. msdn.microsoft.com/library/hh290140.aspx               119027
    B-5. msdn.microsoft.com/library/hh524395.aspx                71260
    B-6. msdn.microsoft.com/library/ms404677.aspx               199186
    B-7. msdn.microsoft.com                                            53078
    B-8. msdn.microsoft.com/library/ff730837.aspx               148010

    TOTAL bytes returned:  915908
    ```

- <span data-ttu-id="88171-205">`pendingWork`Zadanie ma wartość null na początku `FinishOneGroupAsync` tylko dla grupy A, która rozpoczęła się w pierwszej kolejności.</span><span class="sxs-lookup"><span data-stu-id="88171-205">The `pendingWork` task is null  at the start of `FinishOneGroupAsync` only for group A, which started first.</span></span> <span data-ttu-id="88171-206">Grupa A jeszcze nie ukończyła wyrażenia await, gdy osiągnie `FinishOneGroupAsync` .</span><span class="sxs-lookup"><span data-stu-id="88171-206">Group A hasn't yet completed an await expression when it reaches `FinishOneGroupAsync`.</span></span> <span data-ttu-id="88171-207">W związku z tym formant nie został zwrócony do `AccessTheWebAsync` i pierwsze przypisanie do nie zostało wykonane `pendingWork` .</span><span class="sxs-lookup"><span data-stu-id="88171-207">Therefore, control hasn't returned to `AccessTheWebAsync`, and the first assignment to `pendingWork` hasn't occurred.</span></span>

- <span data-ttu-id="88171-208">Dwa następujące wiersze są zawsze wyświetlane razem w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="88171-208">The following two lines always appear together in the output.</span></span> <span data-ttu-id="88171-209">Kod nigdy nie zostanie przerwany między rozpoczęciem operacji grupy w `StartButton_Click` i przypisaniem zadania dla grupy do `pendingWork` .</span><span class="sxs-lookup"><span data-stu-id="88171-209">The code is never interrupted between starting a group's operation in `StartButton_Click` and assigning a task for the group to `pendingWork`.</span></span>

    ```output
    #Starting group B.
    #Task assigned for group B. Download tasks are active.
    ```

    <span data-ttu-id="88171-210">Po wprowadzeniu grupy `StartButton_Click` operacja nie kończy wyrażenia await do momentu wejścia operacji `FinishOneGroupAsync` .</span><span class="sxs-lookup"><span data-stu-id="88171-210">After a group enters `StartButton_Click`, the operation doesn't complete an await expression until the operation enters `FinishOneGroupAsync`.</span></span> <span data-ttu-id="88171-211">W związku z tym żadna inna operacja nie może uzyskać kontroli podczas tego segmentu kodu.</span><span class="sxs-lookup"><span data-stu-id="88171-211">Therefore, no other operation can gain control during that segment of code.</span></span>

## <a name="reviewing-and-running-the-example-app"></a><a name="BKMD_SettingUpTheExample"></a><span data-ttu-id="88171-212">Przeglądanie i uruchamianie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="88171-212">Reviewing and Running the Example App</span></span>

<span data-ttu-id="88171-213">Aby lepiej zrozumieć przykładową aplikację, możesz ją pobrać, skompilować samodzielnie lub przejrzeć kod na końcu tego tematu bez wdrażania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="88171-213">To better understand the example app, you can download it, build it yourself, or review the code at the end of this topic without implementing the app.</span></span>

> [!NOTE]
> <span data-ttu-id="88171-214">Aby uruchomić przykład jako aplikację klasyczną Windows Presentation Foundation (WPF), na komputerze musi być zainstalowany program Visual Studio 2012 lub nowszy oraz .NET Framework 4,5 lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="88171-214">To run the example as a Windows Presentation Foundation (WPF) desktop app, you must have Visual Studio 2012 or newer and the .NET Framework 4.5 or newer installed on your computer.</span></span>

### <a name="downloading-the-app"></a><a name="BKMK_DownloadingTheApp"></a><span data-ttu-id="88171-215">Pobieranie aplikacji</span><span class="sxs-lookup"><span data-stu-id="88171-215">Downloading the App</span></span>

1. <span data-ttu-id="88171-216">Pobierz skompresowany plik z [próbek asynchronicznych: współużytkowania wątkowości w aplikacjach klasycznych platformy .NET](https://code.msdn.microsoft.com/Async-Sample-Preventing-a8489f06).</span><span class="sxs-lookup"><span data-stu-id="88171-216">Download the compressed file from [Async Samples: Reentrancy in .NET Desktop Apps](https://code.msdn.microsoft.com/Async-Sample-Preventing-a8489f06).</span></span>

2. <span data-ttu-id="88171-217">Dekompresuj pobrany plik, a następnie uruchom program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="88171-217">Decompress the file that you downloaded, and then start Visual Studio.</span></span>

3. <span data-ttu-id="88171-218">Na pasku menu wybierz **plik**, **Otwórz**, **projekt/rozwiązanie**.</span><span class="sxs-lookup"><span data-stu-id="88171-218">On the menu bar, choose **File**, **Open**, **Project/Solution**.</span></span>

4. <span data-ttu-id="88171-219">Przejdź do folderu, który zawiera zdekompresować przykładowy kod, a następnie otwórz plik rozwiązania (. sln).</span><span class="sxs-lookup"><span data-stu-id="88171-219">Navigate to the folder that holds the decompressed sample code, and then open the solution (.sln) file.</span></span>

5. <span data-ttu-id="88171-220">W **Eksplorator rozwiązań**Otwórz menu skrótów dla projektu, który chcesz uruchomić, a następnie wybierz polecenie **Ustaw jako StartUpProject**.</span><span class="sxs-lookup"><span data-stu-id="88171-220">In **Solution Explorer**, open the shortcut menu for the project that you want to run, and then choose **Set as StartUpProject**.</span></span>

6. <span data-ttu-id="88171-221">Wybierz kombinację klawiszy CTRL + F5, aby skompilować i uruchomić projekt.</span><span class="sxs-lookup"><span data-stu-id="88171-221">Choose the CTRL+F5 keys to build and run the project.</span></span>

### <a name="building-the-app"></a><a name="BKMK_BuildingTheApp"></a><span data-ttu-id="88171-222">Kompilowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="88171-222">Building the App</span></span>

<span data-ttu-id="88171-223">Poniższa sekcja zawiera kod służący do kompilowania przykładu jako aplikacji WPF.</span><span class="sxs-lookup"><span data-stu-id="88171-223">The following section provides the code to build the example as a WPF app.</span></span>

##### <a name="to-build-a-wpf-app"></a><span data-ttu-id="88171-224">Aby skompilować aplikację WPF</span><span class="sxs-lookup"><span data-stu-id="88171-224">To build a WPF app</span></span>

1. <span data-ttu-id="88171-225">Uruchom program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="88171-225">Start Visual Studio.</span></span>

2. <span data-ttu-id="88171-226">Na pasku menu wybierz **plik**, **Nowy**, **projekt**.</span><span class="sxs-lookup"><span data-stu-id="88171-226">On the menu bar, choose **File**, **New**, **Project**.</span></span>

     <span data-ttu-id="88171-227">Zostanie otwarte okno dialogowe **Nowy projekt** .</span><span class="sxs-lookup"><span data-stu-id="88171-227">The **New Project** dialog box opens.</span></span>

3. <span data-ttu-id="88171-228">W okienku **zainstalowane szablony** rozwiń pozycję **Visual C#**, a następnie rozwiń pozycję **Windows**.</span><span class="sxs-lookup"><span data-stu-id="88171-228">In the **Installed Templates** pane, expand **Visual C#**, and then expand **Windows**.</span></span>

4. <span data-ttu-id="88171-229">Na liście typów projektów wybierz pozycję **Aplikacja WPF**.</span><span class="sxs-lookup"><span data-stu-id="88171-229">In the list of project types, choose **WPF Application**.</span></span>

5. <span data-ttu-id="88171-230">Nazwij projekt `WebsiteDownloadWPF` , wybierz .NET Framework wersja 4,6 lub nowsza, a następnie kliknij przycisk **OK** .</span><span class="sxs-lookup"><span data-stu-id="88171-230">Name the project `WebsiteDownloadWPF`, choose .NET Framework version of 4.6 or higher, and then click the **OK** button.</span></span>

     <span data-ttu-id="88171-231">Nowy projekt zostanie wyświetlony w **Eksplorator rozwiązań**.</span><span class="sxs-lookup"><span data-stu-id="88171-231">The new project appears in **Solution Explorer**.</span></span>

6. <span data-ttu-id="88171-232">W edytorze Visual Studio Code wybierz kartę **MainWindow. XAML** .</span><span class="sxs-lookup"><span data-stu-id="88171-232">In the Visual Studio Code Editor, choose the **MainWindow.xaml** tab.</span></span>

     <span data-ttu-id="88171-233">Jeśli karta nie jest widoczna, otwórz menu skrótów dla MainWindow. XAML w **Eksplorator rozwiązań**, a następnie wybierz polecenie **Wyświetl kod**.</span><span class="sxs-lookup"><span data-stu-id="88171-233">If the tab isn't visible, open the shortcut menu for MainWindow.xaml in **Solution Explorer**, and then choose **View Code**.</span></span>

7. <span data-ttu-id="88171-234">W widoku **XAML** MainWindow. XAML Zastąp kod następującym kodem.</span><span class="sxs-lookup"><span data-stu-id="88171-234">In the **XAML** view of MainWindow.xaml, replace the code with the following code.</span></span>

    ```csharp
    <Window x:Class="WebsiteDownloadWPF.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:local="using:WebsiteDownloadWPF"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        mc:Ignorable="d">

        <Grid Width="517" Height="360">
            <Button x:Name="StartButton" Content="Start" HorizontalAlignment="Left" Margin="-1,0,0,0" VerticalAlignment="Top" Click="StartButton_Click" Height="53" Background="#FFA89B9B" FontSize="36" Width="518"  />
            <TextBox x:Name="ResultsTextBox" HorizontalAlignment="Left" Margin="-1,53,0,-36" TextWrapping="Wrap" VerticalAlignment="Top" Height="343" FontSize="10" ScrollViewer.VerticalScrollBarVisibility="Visible" Width="518" FontFamily="Lucida Console" />
        </Grid>
    </Window>
    ```

     <span data-ttu-id="88171-235">Proste okno zawierające pole tekstowe i przycisk pojawia się w widoku **projekt** MainWindow. XAML.</span><span class="sxs-lookup"><span data-stu-id="88171-235">A simple window that contains a text box and a button appears in the **Design** view of MainWindow.xaml.</span></span>

8. <span data-ttu-id="88171-236">W **Eksplorator rozwiązań**kliknij prawym przyciskiem myszy pozycję **odwołania** i wybierz polecenie **Dodaj odwołanie**.</span><span class="sxs-lookup"><span data-stu-id="88171-236">In **Solution Explorer**, right-click on **References** and select **Add Reference**.</span></span>

     <span data-ttu-id="88171-237">Dodaj odwołanie do <xref:System.Net.Http> , jeśli nie zostało jeszcze wybrane.</span><span class="sxs-lookup"><span data-stu-id="88171-237">Add a reference for <xref:System.Net.Http>, if it is not selected already.</span></span>

9. <span data-ttu-id="88171-238">W **Eksplorator rozwiązań**Otwórz menu skrótów dla MainWindow.XAML.cs, a następnie wybierz polecenie **Wyświetl kod**.</span><span class="sxs-lookup"><span data-stu-id="88171-238">In **Solution Explorer**, open the shortcut menu for MainWindow.xaml.cs, and then choose **View Code**.</span></span>

10. <span data-ttu-id="88171-239">W MainWindow.xaml.cs Zastąp kod następującym kodem.</span><span class="sxs-lookup"><span data-stu-id="88171-239">In MainWindow.xaml.cs, replace the code with the following code.</span></span>

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Windows;
    using System.Windows.Controls;
    using System.Windows.Data;
    using System.Windows.Documents;
    using System.Windows.Input;
    using System.Windows.Media;
    using System.Windows.Media.Imaging;
    using System.Windows.Navigation;
    using System.Windows.Shapes;

    // Add the following using directives, and add a reference for System.Net.Http.
    using System.Net.Http;
    using System.Threading;

    namespace WebsiteDownloadWPF
    {
        public partial class MainWindow : Window
        {
            public MainWindow()
            {
                System.Net.ServicePointManager.SecurityProtocol |= System.Net.SecurityProtocolType.Tls12;
                InitializeComponent();
            }

            private async void StartButton_Click(object sender, RoutedEventArgs e)
            {
                // This line is commented out to make the results clearer in the output.
                //ResultsTextBox.Text = "";

                try
                {
                    await AccessTheWebAsync();
                }
                catch (Exception)
                {
                    ResultsTextBox.Text += "\r\nDownloads failed.";
                }
            }

            private async Task AccessTheWebAsync()
            {
                // Declare an HttpClient object.
                HttpClient client = new HttpClient();

                // Make a list of web addresses.
                List<string> urlList = SetUpURLList();

                var total = 0;
                var position = 0;

                foreach (var url in urlList)
                {
                    // GetByteArrayAsync returns a task. At completion, the task
                    // produces a byte array.
                    byte[] urlContents = await client.GetByteArrayAsync(url);

                    DisplayResults(url, urlContents, ++position);

                    // Update the total.
                    total += urlContents.Length;
                }

                // Display the total count for all of the websites.
                ResultsTextBox.Text +=
                    $"\r\n\r\nTOTAL bytes returned:  {total}\r\n";
            }

            private List<string> SetUpURLList()
            {
                List<string> urls = new List<string>
                {
                    "https://msdn.microsoft.com/library/hh191443.aspx",
                    "https://msdn.microsoft.com/library/aa578028.aspx",
                    "https://msdn.microsoft.com/library/jj155761.aspx",
                    "https://msdn.microsoft.com/library/hh290140.aspx",
                    "https://msdn.microsoft.com/library/hh524395.aspx",
                    "https://msdn.microsoft.com/library/ms404677.aspx",
                    "https://msdn.microsoft.com",
                    "https://msdn.microsoft.com/library/ff730837.aspx"
                };
                return urls;
            }

            private void DisplayResults(string url, byte[] content, int pos)
            {
                // Display the length of each website. The string format is designed
                // to be used with a monospaced font, such as Lucida Console or
                // Global Monospace.

                // Strip off the "https://".
                var displayURL = url.Replace("https://", "");
                // Display position in the URL list, the URL, and the number of bytes.
                ResultsTextBox.Text += $"\n{pos}. {displayURL,-58} {content.Length,8}";
            }
        }
    }
    ```

11. <span data-ttu-id="88171-240">Naciśnij klawisze CTRL + F5, aby uruchomić program, a następnie wybierz przycisk **Start** kilka razy.</span><span class="sxs-lookup"><span data-stu-id="88171-240">Choose the CTRL+F5 keys to run the program, and then choose the **Start** button several times.</span></span>

12. <span data-ttu-id="88171-241">Wprowadź zmiany, aby [wyłączyć przycisk Start](#BKMK_DisableTheStartButton), [anulować i ponownie uruchomić operację](#BKMK_CancelAndRestart)albo [uruchomić wiele operacji i kolejkować dane wyjściowe](#BKMK_RunMultipleOperations) , aby obsłużyć współużytkowania wątkowości.</span><span class="sxs-lookup"><span data-stu-id="88171-241">Make the changes from [Disable the Start Button](#BKMK_DisableTheStartButton), [Cancel and Restart the Operation](#BKMK_CancelAndRestart), or [Run Multiple Operations and Queue the Output](#BKMK_RunMultipleOperations) to handle the reentrancy.</span></span>

## <a name="see-also"></a><span data-ttu-id="88171-242">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="88171-242">See also</span></span>

- [<span data-ttu-id="88171-243">Przewodnik: uzyskiwanie dostępu do sieci Web za pomocą Async i Await (C#)</span><span class="sxs-lookup"><span data-stu-id="88171-243">Walkthrough: Accessing the Web by Using async and await (C#)</span></span>](./walkthrough-accessing-the-web-by-using-async-and-await.md)
- [<span data-ttu-id="88171-244">Programowanie asynchroniczne z Async i Await (C#)</span><span class="sxs-lookup"><span data-stu-id="88171-244">Asynchronous Programming with async and await (C#)</span></span>](./index.md)
