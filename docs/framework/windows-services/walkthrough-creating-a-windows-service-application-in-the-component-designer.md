---
title: 'Samouczek: Tworzenie aplikacji usługi systemu Windows'
description: W tym samouczku utworzysz aplikację usługi systemu Windows w programie Visual Studio, która zapisuje komunikaty w dzienniku zdarzeń. Dodawanie funkcji, Ustawianie stanu, Dodawanie instalatorów i nie tylko.
ms.date: 03/27/2019
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Windows service applications, walkthroughs
- Windows service applications, creating
ms.assetid: e24d8a3d-edc6-485c-b6e0-5672d91fb607
author: ghogen
ms.openlocfilehash: 487a974af2280a02b83fe685324c9464df705585
ms.sourcegitcommit: 40de8df14289e1e05b40d6e5c1daabd3c286d70c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/22/2020
ms.locfileid: "86925634"
---
# <a name="tutorial-create-a-windows-service-app"></a><span data-ttu-id="87685-104">Samouczek: Tworzenie aplikacji usługi systemu Windows</span><span class="sxs-lookup"><span data-stu-id="87685-104">Tutorial: Create a Windows service app</span></span>

<span data-ttu-id="87685-105">W tym artykule pokazano, jak utworzyć aplikację usługi systemu Windows w programie Visual Studio, która zapisuje komunikaty w dzienniku zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="87685-105">This article demonstrates how to create a Windows service app in Visual Studio that writes messages to an event log.</span></span>

## <a name="create-a-service"></a><span data-ttu-id="87685-106">Tworzenie usługi</span><span class="sxs-lookup"><span data-stu-id="87685-106">Create a service</span></span>

<span data-ttu-id="87685-107">Aby rozpocząć, Utwórz projekt i ustaw wartości, które są wymagane do poprawnego działania usługi.</span><span class="sxs-lookup"><span data-stu-id="87685-107">To begin, create the project and set the values that are required for the service to function correctly.</span></span>

1. <span data-ttu-id="87685-108">Z menu **plik** programu Visual Studio wybierz pozycję **Nowy**  >  **projekt** (lub naciśnij **klawisze CTRL** + **SHIFT** + **N**), aby otworzyć okno **Nowy projekt** .</span><span class="sxs-lookup"><span data-stu-id="87685-108">From the Visual Studio **File** menu, select **New** > **Project** (or press **Ctrl**+**Shift**+**N**) to open the **New Project** window.</span></span>

2. <span data-ttu-id="87685-109">Przejdź do i wybierz szablon projektu **usługi systemu Windows (.NET Framework)** .</span><span class="sxs-lookup"><span data-stu-id="87685-109">Navigate to and select the **Windows Service (.NET Framework)** project template.</span></span> <span data-ttu-id="87685-110">Aby go znaleźć, rozwiń węzeł **zainstalowane** i **Visual C#** lub **Visual Basic**, a następnie wybierz pozycję **Windows Desktop**.</span><span class="sxs-lookup"><span data-stu-id="87685-110">To find it, expand **Installed** and **Visual C#** or **Visual Basic**, then select **Windows Desktop**.</span></span> <span data-ttu-id="87685-111">Lub wprowadź *usługę systemu Windows* w polu wyszukiwania w prawym górnym rogu, a następnie naciśnij klawisz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="87685-111">Or, enter *Windows Service* in the search box on the upper right and press **Enter**.</span></span>

   ![Szablon usługi systemu Windows w oknie dialogowym Nowy projekt w programie Visual Studio](./media/new-project-dialog.png)

   > [!NOTE]
   > <span data-ttu-id="87685-113">Jeśli szablon **usługi systemu Windows** nie jest widoczny, może być konieczne zainstalowanie obciążeń **programistycznych programu .NET Desktop** :</span><span class="sxs-lookup"><span data-stu-id="87685-113">If you don't see the **Windows Service** template, you may need to install the **.NET desktop development** workload:</span></span>
   >
   > <span data-ttu-id="87685-114">W oknie dialogowym **Nowy projekt** wybierz pozycję **Otwórz Instalator programu Visual Studio** w lewym dolnym rogu.</span><span class="sxs-lookup"><span data-stu-id="87685-114">In the **New Project** dialog, select **Open Visual Studio Installer** on the lower left.</span></span> <span data-ttu-id="87685-115">Wybierz obciążenie **Programowanie aplikacji klasycznych platformy .NET** , a następnie wybierz pozycję **Modyfikuj**.</span><span class="sxs-lookup"><span data-stu-id="87685-115">Select the **.NET desktop development** workload, and then select **Modify**.</span></span>

3. <span data-ttu-id="87685-116">W obszarze **Nazwa**wpisz *MyNewService*, a następnie wybierz przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="87685-116">For **Name**, enter *MyNewService*, and then select **OK**.</span></span>

   <span data-ttu-id="87685-117">Zostanie wyświetlona karta **projektowanie** (**Service1.cs [projekt]** lub **Service1. vb [projekt]**).</span><span class="sxs-lookup"><span data-stu-id="87685-117">The **Design** tab appears (**Service1.cs [Design]** or **Service1.vb [Design]**).</span></span>

   <span data-ttu-id="87685-118">Szablon projektu zawiera klasę składnika o nazwie `Service1` , która dziedziczy z <xref:System.ServiceProcess.ServiceBase?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="87685-118">The project template includes a component class named `Service1` that inherits from <xref:System.ServiceProcess.ServiceBase?displayProperty=nameWithType>.</span></span> <span data-ttu-id="87685-119">Zawiera on wiele podstawowych kodów usług, takich jak kod do uruchomienia usługi.</span><span class="sxs-lookup"><span data-stu-id="87685-119">It includes much of the basic service code, such as the code to start the service.</span></span>

## <a name="rename-the-service"></a><span data-ttu-id="87685-120">Zmień nazwę usługi</span><span class="sxs-lookup"><span data-stu-id="87685-120">Rename the service</span></span>

<span data-ttu-id="87685-121">Zmień nazwę usługi z **Service1** na **MyNewService**.</span><span class="sxs-lookup"><span data-stu-id="87685-121">Rename the service from **Service1** to **MyNewService**.</span></span>

1. <span data-ttu-id="87685-122">W **Eksplorator rozwiązań**wybierz pozycję **Service1.cs**lub **Service1. vb**i wybierz polecenie **Zmień nazwę** z menu skrótów.</span><span class="sxs-lookup"><span data-stu-id="87685-122">In **Solution Explorer**, select **Service1.cs**, or **Service1.vb**, and choose **Rename** from the shortcut menu.</span></span> <span data-ttu-id="87685-123">Zmień nazwę pliku na **MyNewService.cs**lub **MyNewService. vb**, a następnie naciśnij klawisz **Enter** .</span><span class="sxs-lookup"><span data-stu-id="87685-123">Rename the file to **MyNewService.cs**, or **MyNewService.vb**, and then press **Enter**</span></span>

    <span data-ttu-id="87685-124">Zostanie wyświetlone okno podręczne z pytaniem, czy chcesz zmienić nazwy wszystkich odwołań do elementu kodu *Service1*.</span><span class="sxs-lookup"><span data-stu-id="87685-124">A pop-up window appears asking whether you would like to rename all references to the code element *Service1*.</span></span>

2. <span data-ttu-id="87685-125">W oknie podręcznym wybierz pozycję **tak**.</span><span class="sxs-lookup"><span data-stu-id="87685-125">In the pop-up window, select **Yes**.</span></span>

    <span data-ttu-id="87685-126">![Zmień nazwę monitu](./media/windows-service-rename.png "Monit o zmianę nazwy usługi systemu Windows")</span><span class="sxs-lookup"><span data-stu-id="87685-126">![Rename prompt](./media/windows-service-rename.png "Windows service rename prompt")</span></span>

3. <span data-ttu-id="87685-127">Na karcie **projektowanie** wybierz pozycję **Właściwości** z menu skrótów.</span><span class="sxs-lookup"><span data-stu-id="87685-127">In the **Design** tab, select **Properties** from the shortcut menu.</span></span> <span data-ttu-id="87685-128">W oknie **Właściwości** Zmień wartość właściwości **ServiceName** na *MyNewService*.</span><span class="sxs-lookup"><span data-stu-id="87685-128">From the **Properties** window, change the **ServiceName** value to *MyNewService*.</span></span>

    <span data-ttu-id="87685-129">![Właściwości usługi](./media/windows-service-properties.png "Właściwości usługi systemu Windows")</span><span class="sxs-lookup"><span data-stu-id="87685-129">![Service properties](./media/windows-service-properties.png "Windows service properties")</span></span>

4. <span data-ttu-id="87685-130">Wybierz pozycję **Zapisz wszystko** w menu **plik** .</span><span class="sxs-lookup"><span data-stu-id="87685-130">Select **Save All** from the **File** menu.</span></span>

## <a name="add-features-to-the-service"></a><span data-ttu-id="87685-131">Dodawanie funkcji do usługi</span><span class="sxs-lookup"><span data-stu-id="87685-131">Add features to the service</span></span>

<span data-ttu-id="87685-132">W tej sekcji dodasz niestandardowy dziennik zdarzeń do usługi systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="87685-132">In this section, you add a custom event log to the Windows service.</span></span> <span data-ttu-id="87685-133"><xref:System.Diagnostics.EventLog>Składnik jest przykładem typu składnika, który można dodać do usługi systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="87685-133">The <xref:System.Diagnostics.EventLog> component is an example of the type of component you can add to a Windows service.</span></span>

### <a name="add-custom-event-log-functionality"></a><span data-ttu-id="87685-134">Dodaj niestandardową funkcję dziennika zdarzeń</span><span class="sxs-lookup"><span data-stu-id="87685-134">Add custom event log functionality</span></span>

1. <span data-ttu-id="87685-135">W **Eksplorator rozwiązań**z menu skrótów dla **MyNewService.cs**lub **MyNewService. vb**wybierz polecenie **Projektant widoków**.</span><span class="sxs-lookup"><span data-stu-id="87685-135">In **Solution Explorer**, from the shortcut menu for **MyNewService.cs**, or **MyNewService.vb**, choose **View Designer**.</span></span>

2. <span data-ttu-id="87685-136">W **przyborniku**rozwiń węzeł **składniki**, a następnie przeciągnij składnik **EventLog** do karty **Service1.cs [Design]** lub **Service1. vb [Design]** .</span><span class="sxs-lookup"><span data-stu-id="87685-136">In **Toolbox**, expand **Components**, and then drag the **EventLog** component to the **Service1.cs [Design]**, or **Service1.vb [Design]** tab.</span></span>

3. <span data-ttu-id="87685-137">W **Eksplorator rozwiązań**z menu skrótów dla **MyNewService.cs**lub **MyNewService. vb**wybierz polecenie **Wyświetl kod**.</span><span class="sxs-lookup"><span data-stu-id="87685-137">In **Solution Explorer**, from the shortcut menu for **MyNewService.cs**, or **MyNewService.vb**, choose **View Code**.</span></span>

4. <span data-ttu-id="87685-138">Zdefiniuj niestandardowy dziennik zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="87685-138">Define a custom event log.</span></span> <span data-ttu-id="87685-139">W przypadku języka C# Edytuj istniejący `MyNewService()` Konstruktor, dla Visual Basic Dodaj `New()` Konstruktor:</span><span class="sxs-lookup"><span data-stu-id="87685-139">For C#, edit the existing `MyNewService()` constructor; for Visual Basic, add the `New()` constructor:</span></span>

   [!code-csharp[VbRadconService#2](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#2)]
   [!code-vb[VbRadconService#2](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#2)]

5. <span data-ttu-id="87685-140">Dodaj `using` instrukcję do **MyNewService.cs** (jeśli jeszcze nie istnieje) lub `Imports` instrukcji **MyNewService. vb**dla <xref:System.Diagnostics?displayProperty=nameWithType> przestrzeni nazw:</span><span class="sxs-lookup"><span data-stu-id="87685-140">Add a `using` statement to **MyNewService.cs** (if it doesn't already exist), or an `Imports` statement **MyNewService.vb**, for the <xref:System.Diagnostics?displayProperty=nameWithType> namespace:</span></span>

    ```csharp
    using System.Diagnostics;
    ```

    ```vb
    Imports System.Diagnostics
    ```

6. <span data-ttu-id="87685-141">Wybierz pozycję **Zapisz wszystko** w menu **plik** .</span><span class="sxs-lookup"><span data-stu-id="87685-141">Select **Save All** from the **File** menu.</span></span>

### <a name="define-what-occurs-when-the-service-starts"></a><span data-ttu-id="87685-142">Zdefiniuj, co ma miejsce w przypadku uruchomienia usługi</span><span class="sxs-lookup"><span data-stu-id="87685-142">Define what occurs when the service starts</span></span>

<span data-ttu-id="87685-143">W edytorze kodu dla **MyNewService.cs** lub **MyNewService. vb**Znajdź <xref:System.ServiceProcess.ServiceBase.OnStart%2A> metodę; Program Visual Studio automatycznie utworzył pustą definicję metody podczas tworzenia projektu.</span><span class="sxs-lookup"><span data-stu-id="87685-143">In the code editor for **MyNewService.cs** or **MyNewService.vb**, locate the <xref:System.ServiceProcess.ServiceBase.OnStart%2A> method; Visual Studio automatically created an empty method definition when you created the project.</span></span> <span data-ttu-id="87685-144">Dodaj kod, który zapisuje wpis w dzienniku zdarzeń po uruchomieniu usługi:</span><span class="sxs-lookup"><span data-stu-id="87685-144">Add code that writes an entry to the event log when the service starts:</span></span>

[!code-csharp[VbRadconService#3](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#3)]
[!code-vb[VbRadconService#3](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#3)]

#### <a name="polling"></a><span data-ttu-id="87685-145">Sondowanie</span><span class="sxs-lookup"><span data-stu-id="87685-145">Polling</span></span>

<span data-ttu-id="87685-146">Ponieważ aplikacja usługi jest zaprojektowana tak, aby była długotrwała, zwykle sonduje lub monitoruje system, który został skonfigurowany w <xref:System.ServiceProcess.ServiceBase.OnStart%2A> metodzie.</span><span class="sxs-lookup"><span data-stu-id="87685-146">Because a service application is designed to be long-running, it usually polls or monitors the system, which you set up in the <xref:System.ServiceProcess.ServiceBase.OnStart%2A> method.</span></span> <span data-ttu-id="87685-147">`OnStart`Metoda musi powrócić do systemu operacyjnego po rozpoczęciu operacji usługi, aby system nie został zablokowany.</span><span class="sxs-lookup"><span data-stu-id="87685-147">The `OnStart` method must return to the operating system after the service's operation has begun so that the system isn't blocked.</span></span>

<span data-ttu-id="87685-148">Aby skonfigurować prosty mechanizm sondowania, użyj <xref:System.Timers.Timer?displayProperty=nameWithType> składnika.</span><span class="sxs-lookup"><span data-stu-id="87685-148">To set up a simple polling mechanism, use the <xref:System.Timers.Timer?displayProperty=nameWithType> component.</span></span> <span data-ttu-id="87685-149">Czasomierz zgłasza <xref:System.Timers.Timer.Elapsed> zdarzenie w regularnych odstępach czasu, w którym usługa może przeprowadzić monitorowanie.</span><span class="sxs-lookup"><span data-stu-id="87685-149">The timer raises an <xref:System.Timers.Timer.Elapsed> event at regular intervals, at which time your service can do its monitoring.</span></span> <span data-ttu-id="87685-150">Składnik jest używany <xref:System.Timers.Timer> w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="87685-150">You use the <xref:System.Timers.Timer> component as follows:</span></span>

- <span data-ttu-id="87685-151">Ustaw właściwości <xref:System.Timers.Timer> składnika w `MyNewService.OnStart` metodzie.</span><span class="sxs-lookup"><span data-stu-id="87685-151">Set the properties of the <xref:System.Timers.Timer> component in the `MyNewService.OnStart` method.</span></span>
- <span data-ttu-id="87685-152">Uruchom czasomierz, wywołując <xref:System.Timers.Timer.Start%2A> metodę.</span><span class="sxs-lookup"><span data-stu-id="87685-152">Start the timer by calling the <xref:System.Timers.Timer.Start%2A> method.</span></span>

##### <a name="set-up-the-polling-mechanism"></a><span data-ttu-id="87685-153">Skonfiguruj mechanizm sondowania.</span><span class="sxs-lookup"><span data-stu-id="87685-153">Set up the polling mechanism.</span></span>

1. <span data-ttu-id="87685-154">Dodaj następujący kod w `MyNewService.OnStart` zdarzeniu, aby skonfigurować mechanizm sondowania:</span><span class="sxs-lookup"><span data-stu-id="87685-154">Add the following code in the `MyNewService.OnStart` event to set up the polling mechanism:</span></span>

   ```csharp
   // Set up a timer that triggers every minute.
   Timer timer = new Timer();
   timer.Interval = 60000; // 60 seconds
   timer.Elapsed += new ElapsedEventHandler(this.OnTimer);
   timer.Start();
   ```

   ```vb
   ' Set up a timer that triggers every minute.
   Dim timer As Timer = New Timer()
   timer.Interval = 60000 ' 60 seconds
   AddHandler timer.Elapsed, AddressOf Me.OnTimer
   timer.Start()
   ```

2. <span data-ttu-id="87685-155">Dodaj `using` instrukcję do **MyNewService.cs**lub `Imports` instrukcję do **MyNewService. vb**dla <xref:System.Timers?displayProperty=nameWithType> przestrzeni nazw:</span><span class="sxs-lookup"><span data-stu-id="87685-155">Add a `using` statement to **MyNewService.cs**, or an `Imports` statement to **MyNewService.vb**, for the <xref:System.Timers?displayProperty=nameWithType> namespace:</span></span>

   ```csharp
   using System.Timers;
   ```

   ```vb
   Imports System.Timers
   ```

3. <span data-ttu-id="87685-156">W `MyNewService` klasie Dodaj `OnTimer` metodę, aby obsłużyć <xref:System.Timers.Timer.Elapsed?displayProperty=nameWithType> zdarzenie:</span><span class="sxs-lookup"><span data-stu-id="87685-156">In the `MyNewService` class, add the `OnTimer` method to handle the <xref:System.Timers.Timer.Elapsed?displayProperty=nameWithType> event:</span></span>

   ```csharp
   public void OnTimer(object sender, ElapsedEventArgs args)
   {
       // TODO: Insert monitoring activities here.
       eventLog1.WriteEntry("Monitoring the System", EventLogEntryType.Information, eventId++);
   }
   ```

   ```vb
   Private Sub OnTimer(sender As Object, e As Timers.ElapsedEventArgs)
      ' TODO: Insert monitoring activities here.
      eventLog1.WriteEntry("Monitoring the System", EventLogEntryType.Information, eventId)
      eventId = eventId + 1
   End Sub
   ```

4. <span data-ttu-id="87685-157">W `MyNewService` klasie Dodaj zmienną członkowską.</span><span class="sxs-lookup"><span data-stu-id="87685-157">In the `MyNewService` class, add a member variable.</span></span> <span data-ttu-id="87685-158">Zawiera identyfikator następnego zdarzenia do zapisu w dzienniku zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="87685-158">It contains the identifier of the next event to write into the event log:</span></span>

   ```csharp
   private int eventId = 1;
   ```

   ```vb
   Private eventId As Integer = 1
   ```

<span data-ttu-id="87685-159">Zamiast uruchamiać wszystkie prace w głównym wątku, można uruchamiać zadania przy użyciu wątków roboczych w tle.</span><span class="sxs-lookup"><span data-stu-id="87685-159">Instead of running all your work on the main thread, you can run tasks by using background worker threads.</span></span> <span data-ttu-id="87685-160">Aby uzyskać więcej informacji, zobacz <xref:System.ComponentModel.BackgroundWorker?displayProperty=fullName>.</span><span class="sxs-lookup"><span data-stu-id="87685-160">For more information, see <xref:System.ComponentModel.BackgroundWorker?displayProperty=fullName>.</span></span>

### <a name="define-what-occurs-when-the-service-is-stopped"></a><span data-ttu-id="87685-161">Określ, co ma miejsce w przypadku zatrzymania usługi</span><span class="sxs-lookup"><span data-stu-id="87685-161">Define what occurs when the service is stopped</span></span>

<span data-ttu-id="87685-162">Wstaw wiersz kodu w <xref:System.ServiceProcess.ServiceBase.OnStop%2A> metodzie, która dodaje wpis do dziennika zdarzeń po zatrzymaniu usługi:</span><span class="sxs-lookup"><span data-stu-id="87685-162">Insert a line of code in the <xref:System.ServiceProcess.ServiceBase.OnStop%2A> method that adds an entry to the event log when the service is stopped:</span></span>

[!code-csharp[VbRadconService#2](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#4)]
[!code-vb[VbRadconService#4](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#4)]

### <a name="define-other-actions-for-the-service"></a><span data-ttu-id="87685-163">Zdefiniuj inne akcje dla usługi</span><span class="sxs-lookup"><span data-stu-id="87685-163">Define other actions for the service</span></span>

<span data-ttu-id="87685-164">Można zastąpić <xref:System.ServiceProcess.ServiceBase.OnPause%2A> <xref:System.ServiceProcess.ServiceBase.OnContinue%2A> metody, i, <xref:System.ServiceProcess.ServiceBase.OnShutdown%2A> Aby zdefiniować dodatkowe przetwarzanie dla składnika.</span><span class="sxs-lookup"><span data-stu-id="87685-164">You can override the <xref:System.ServiceProcess.ServiceBase.OnPause%2A>, <xref:System.ServiceProcess.ServiceBase.OnContinue%2A>, and <xref:System.ServiceProcess.ServiceBase.OnShutdown%2A> methods to define additional processing for your component.</span></span>

<span data-ttu-id="87685-165">Poniższy kod pokazuje, jak zastąpić <xref:System.ServiceProcess.ServiceBase.OnContinue%2A> metodę w `MyNewService` klasie:</span><span class="sxs-lookup"><span data-stu-id="87685-165">The following code shows how you to override the <xref:System.ServiceProcess.ServiceBase.OnContinue%2A> method in the `MyNewService` class:</span></span>

[!code-csharp[VbRadconService#5](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#5)]
[!code-vb[VbRadconService#5](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#5)]

## <a name="set-service-status"></a><span data-ttu-id="87685-166">Ustawianie stanu usługi</span><span class="sxs-lookup"><span data-stu-id="87685-166">Set service status</span></span>

<span data-ttu-id="87685-167">Usługi raportują swój stan do [Menedżera kontroli usług](/windows/desktop/Services/service-control-manager) , aby użytkownik mógł stwierdzić, czy usługa działa poprawnie.</span><span class="sxs-lookup"><span data-stu-id="87685-167">Services report their status to the [Service Control Manager](/windows/desktop/Services/service-control-manager) so that a user can tell whether a service is functioning correctly.</span></span> <span data-ttu-id="87685-168">Domyślnie usługa, która dziedziczy z raportów, zawiera <xref:System.ServiceProcess.ServiceBase> ograniczony zestaw ustawień stanu, w tym SERVICE_STOPPED, SERVICE_PAUSED i SERVICE_RUNNING.</span><span class="sxs-lookup"><span data-stu-id="87685-168">By default, a service that inherits from <xref:System.ServiceProcess.ServiceBase> reports a limited set of status settings, which include SERVICE_STOPPED, SERVICE_PAUSED, and SERVICE_RUNNING.</span></span> <span data-ttu-id="87685-169">Jeśli uruchomienie usługi trwa dłużej, warto zgłosić stan SERVICE_START_PENDING.</span><span class="sxs-lookup"><span data-stu-id="87685-169">If a service takes a while to start up, it's useful to report a SERVICE_START_PENDING status.</span></span>

<span data-ttu-id="87685-170">Można zaimplementować ustawienia stanu SERVICE_START_PENDING i SERVICE_STOP_PENDING, dodając kod, który wywołuje funkcję [SetServiceStatus](/windows/desktop/api/winsvc/nf-winsvc-setservicestatus) systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="87685-170">You can implement the SERVICE_START_PENDING and SERVICE_STOP_PENDING status settings by adding code that calls the Windows [SetServiceStatus](/windows/desktop/api/winsvc/nf-winsvc-setservicestatus) function.</span></span>

### <a name="implement-service-pending-status"></a><span data-ttu-id="87685-171">Zaimplementuj stan oczekiwania usługi</span><span class="sxs-lookup"><span data-stu-id="87685-171">Implement service pending status</span></span>

1. <span data-ttu-id="87685-172">Dodaj `using` instrukcję do **MyNewService.cs**lub `Imports` instrukcję do **MyNewService. vb**dla <xref:System.Runtime.InteropServices?displayProperty=nameWithType> przestrzeni nazw:</span><span class="sxs-lookup"><span data-stu-id="87685-172">Add a `using` statement to **MyNewService.cs**, or an `Imports` statement to **MyNewService.vb**, for the <xref:System.Runtime.InteropServices?displayProperty=nameWithType> namespace:</span></span>

    ```csharp
    using System.Runtime.InteropServices;
    ```

    ```vb
    Imports System.Runtime.InteropServices
    ```

2. <span data-ttu-id="87685-173">Dodaj następujący kod do **MyNewService.cs**lub **MyNewService. vb**, aby zadeklarować `ServiceState` wartości i dodać strukturę dla stanu, który będzie używany w wywołaniu wywołania platformy:</span><span class="sxs-lookup"><span data-stu-id="87685-173">Add the following code to **MyNewService.cs**, or **MyNewService.vb**, to declare the `ServiceState` values and to add a structure for the status, which you'll use in a platform invoke call:</span></span>

    ```csharp
    public enum ServiceState
    {
        SERVICE_STOPPED = 0x00000001,
        SERVICE_START_PENDING = 0x00000002,
        SERVICE_STOP_PENDING = 0x00000003,
        SERVICE_RUNNING = 0x00000004,
        SERVICE_CONTINUE_PENDING = 0x00000005,
        SERVICE_PAUSE_PENDING = 0x00000006,
        SERVICE_PAUSED = 0x00000007,
    }

    [StructLayout(LayoutKind.Sequential)]
    public struct ServiceStatus
    {
        public int dwServiceType;
        public ServiceState dwCurrentState;
        public int dwControlsAccepted;
        public int dwWin32ExitCode;
        public int dwServiceSpecificExitCode;
        public int dwCheckPoint;
        public int dwWaitHint;
    };
    ```

    ```vb
    Public Enum ServiceState
        SERVICE_STOPPED = 1
        SERVICE_START_PENDING = 2
        SERVICE_STOP_PENDING = 3
        SERVICE_RUNNING = 4
        SERVICE_CONTINUE_PENDING = 5
        SERVICE_PAUSE_PENDING = 6
        SERVICE_PAUSED = 7
    End Enum

    <StructLayout(LayoutKind.Sequential)>
    Public Structure ServiceStatus
        Public dwServiceType As Long
        Public dwCurrentState As ServiceState
        Public dwControlsAccepted As Long
        Public dwWin32ExitCode As Long
        Public dwServiceSpecificExitCode As Long
        Public dwCheckPoint As Long
        Public dwWaitHint As Long
    End Structure
    ```

    > [!NOTE]
    > <span data-ttu-id="87685-174">Menedżer sterowania usługami używa `dwWaitHint` i `dwCheckpoint` składowych [struktury SERVICE_STATUS](/windows/win32/api/winsvc/ns-winsvc-service_status) , aby określić czas oczekiwania na uruchomienie lub wyłączenie usługi systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="87685-174">The Service Control Manager uses the `dwWaitHint` and `dwCheckpoint` members of the [SERVICE_STATUS structure](/windows/win32/api/winsvc/ns-winsvc-service_status) to determine how much time to wait for a Windows service to start or shut down.</span></span> <span data-ttu-id="87685-175">Jeśli `OnStart` metody i `OnStop` są wykonywane długo, usługa może zażądać więcej czasu, wywołując `SetServiceStatus` ponownie z wartością przyrostową `dwCheckPoint` .</span><span class="sxs-lookup"><span data-stu-id="87685-175">If your `OnStart` and `OnStop` methods run long, your service can request more time by calling `SetServiceStatus` again with an incremented `dwCheckPoint` value.</span></span>

3. <span data-ttu-id="87685-176">W `MyNewService` klasie deklaruj funkcję [SetServiceStatus](/windows/desktop/api/winsvc/nf-winsvc-setservicestatus) przy użyciu [wywołania platformy](../interop/consuming-unmanaged-dll-functions.md):</span><span class="sxs-lookup"><span data-stu-id="87685-176">In the `MyNewService` class, declare the [SetServiceStatus](/windows/desktop/api/winsvc/nf-winsvc-setservicestatus) function by using [platform invoke](../interop/consuming-unmanaged-dll-functions.md):</span></span>

    ```csharp
    [DllImport("advapi32.dll", SetLastError = true)]
    private static extern bool SetServiceStatus(System.IntPtr handle, ref ServiceStatus serviceStatus);
    ```

    ```vb
    Declare Auto Function SetServiceStatus Lib "advapi32.dll" (ByVal handle As IntPtr, ByRef serviceStatus As ServiceStatus) As Boolean
    ```

4. <span data-ttu-id="87685-177">Aby zaimplementować stan SERVICE_START_PENDING, Dodaj następujący kod na początku <xref:System.ServiceProcess.ServiceBase.OnStart%2A> metody:</span><span class="sxs-lookup"><span data-stu-id="87685-177">To implement the SERVICE_START_PENDING status, add the following code to the beginning of the <xref:System.ServiceProcess.ServiceBase.OnStart%2A> method:</span></span>

    ```csharp
    // Update the service state to Start Pending.
    ServiceStatus serviceStatus = new ServiceStatus();
    serviceStatus.dwCurrentState = ServiceState.SERVICE_START_PENDING;
    serviceStatus.dwWaitHint = 100000;
    SetServiceStatus(this.ServiceHandle, ref serviceStatus);
    ```

    ```vb
    ' Update the service state to Start Pending.
    Dim serviceStatus As ServiceStatus = New ServiceStatus()
    serviceStatus.dwCurrentState = ServiceState.SERVICE_START_PENDING
    serviceStatus.dwWaitHint = 100000
    SetServiceStatus(Me.ServiceHandle, serviceStatus)
    ```

5. <span data-ttu-id="87685-178">Dodaj kod na końcu `OnStart` metody, aby ustawić stan na SERVICE_RUNNING:</span><span class="sxs-lookup"><span data-stu-id="87685-178">Add code to the end of the `OnStart` method to set the status to SERVICE_RUNNING:</span></span>

    ```csharp
    // Update the service state to Running.
    serviceStatus.dwCurrentState = ServiceState.SERVICE_RUNNING;
    SetServiceStatus(this.ServiceHandle, ref serviceStatus);
    ```

    ```vb
    ' Update the service state to Running.
    serviceStatus.dwCurrentState = ServiceState.SERVICE_RUNNING
    SetServiceStatus(Me.ServiceHandle, serviceStatus)
    ```

6. <span data-ttu-id="87685-179">Obowiązkowe Jeśli <xref:System.ServiceProcess.ServiceBase.OnStop%2A> jest metodą długotrwałą, powtórz tę procedurę w `OnStop` metodzie.</span><span class="sxs-lookup"><span data-stu-id="87685-179">(Optional) If <xref:System.ServiceProcess.ServiceBase.OnStop%2A> is a long-running method, repeat this procedure in the `OnStop` method.</span></span> <span data-ttu-id="87685-180">Zaimplementuj stan SERVICE_STOP_PENDING i zwróć stan SERVICE_STOPPED przed `OnStop` wyjściem z metody.</span><span class="sxs-lookup"><span data-stu-id="87685-180">Implement the SERVICE_STOP_PENDING status and return the SERVICE_STOPPED status before the `OnStop` method exits.</span></span>

   <span data-ttu-id="87685-181">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="87685-181">For example:</span></span>

    ```csharp
    // Update the service state to Stop Pending.
    ServiceStatus serviceStatus = new ServiceStatus();
    serviceStatus.dwCurrentState = ServiceState.SERVICE_STOP_PENDING;
    serviceStatus.dwWaitHint = 100000;
    SetServiceStatus(this.ServiceHandle, ref serviceStatus);

    // Update the service state to Stopped.
    serviceStatus.dwCurrentState = ServiceState.SERVICE_STOPPED;
    SetServiceStatus(this.ServiceHandle, ref serviceStatus);
    ```

    ```vb
    ' Update the service state to Stop Pending.
    Dim serviceStatus As ServiceStatus = New ServiceStatus()
    serviceStatus.dwCurrentState = ServiceState.SERVICE_STOP_PENDING
    serviceStatus.dwWaitHint = 100000
    SetServiceStatus(Me.ServiceHandle, serviceStatus)

    ' Update the service state to Stopped.
    serviceStatus.dwCurrentState = ServiceState.SERVICE_STOPPED
    SetServiceStatus(Me.ServiceHandle, serviceStatus)
    ```

## <a name="add-installers-to-the-service"></a><span data-ttu-id="87685-182">Dodawanie instalatorów do usługi</span><span class="sxs-lookup"><span data-stu-id="87685-182">Add installers to the service</span></span>

<span data-ttu-id="87685-183">Przed uruchomieniem usługi systemu Windows należy ją zainstalować, co spowoduje zarejestrowanie jej w Menedżerze kontroli usług.</span><span class="sxs-lookup"><span data-stu-id="87685-183">Before you run a Windows service, you need to install it, which registers it with the Service Control Manager.</span></span> <span data-ttu-id="87685-184">Dodaj Instalatory do projektu, aby obsłużyć szczegóły rejestracji.</span><span class="sxs-lookup"><span data-stu-id="87685-184">Add installers to your project to handle the registration details.</span></span>

1. <span data-ttu-id="87685-185">W **Eksplorator rozwiązań**z menu skrótów dla **MyNewService.cs**lub **MyNewService. vb**wybierz polecenie **Projektant widoków**.</span><span class="sxs-lookup"><span data-stu-id="87685-185">In **Solution Explorer**, from the shortcut menu for **MyNewService.cs**, or **MyNewService.vb**, choose **View Designer**.</span></span>

2. <span data-ttu-id="87685-186">W widoku **projekt** wybierz obszar tła, a następnie wybierz polecenie **Dodaj Instalatora** z menu skrótów.</span><span class="sxs-lookup"><span data-stu-id="87685-186">In the **Design** view, select the background area, then choose **Add Installer** from the shortcut menu.</span></span>

     <span data-ttu-id="87685-187">Domyślnie program Visual Studio dodaje klasę składnika o nazwie `ProjectInstaller` , która zawiera dwóch instalatorów do projektu.</span><span class="sxs-lookup"><span data-stu-id="87685-187">By default, Visual Studio adds a component class named `ProjectInstaller`, which contains two installers, to your project.</span></span> <span data-ttu-id="87685-188">Te Instalatory są przeznaczone dla usługi i dla procesu związanego z usługą.</span><span class="sxs-lookup"><span data-stu-id="87685-188">These installers are for your service and for the service's associated process.</span></span>

3. <span data-ttu-id="87685-189">W widoku **projekt** dla **ProjectInstaller**wybierz pozycję **serviceInstaller1** dla projektu Visual C# lub **serviceInstaller1** dla projektu Visual Basic, a następnie wybierz **Właściwości** z menu skrótów.</span><span class="sxs-lookup"><span data-stu-id="87685-189">In the **Design** view for **ProjectInstaller**, select **serviceInstaller1** for a Visual C# project, or **ServiceInstaller1** for a Visual Basic project, then choose **Properties** from the shortcut menu.</span></span>

4. <span data-ttu-id="87685-190">W oknie **Właściwości** Sprawdź, czy <xref:System.ServiceProcess.ServiceInstaller.ServiceName%2A> Właściwość jest ustawiona na **MyNewService**.</span><span class="sxs-lookup"><span data-stu-id="87685-190">In the **Properties** window, verify the <xref:System.ServiceProcess.ServiceInstaller.ServiceName%2A> property is set to **MyNewService**.</span></span>

5. <span data-ttu-id="87685-191">Dodaj tekst do <xref:System.ServiceProcess.ServiceInstaller.Description%2A> właściwości, takiej jak *Przykładowa usługa*.</span><span class="sxs-lookup"><span data-stu-id="87685-191">Add text to the <xref:System.ServiceProcess.ServiceInstaller.Description%2A> property, such as *A sample service*.</span></span>

     <span data-ttu-id="87685-192">Ten tekst jest wyświetlany w kolumnie **Opis** okna **usługi** i zawiera opis usługi dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="87685-192">This text appears in the **Description** column of the **Services** window and describes the service to the user.</span></span>

    <span data-ttu-id="87685-193">![Opis usługi w oknie usługi.](./media/windows-service-description.png "Opis usługi")</span><span class="sxs-lookup"><span data-stu-id="87685-193">![Service description in the Services window.](./media/windows-service-description.png "Service description")</span></span>

6. <span data-ttu-id="87685-194">Dodaj tekst do <xref:System.ServiceProcess.ServiceInstaller.DisplayName%2A> właściwości.</span><span class="sxs-lookup"><span data-stu-id="87685-194">Add text to the <xref:System.ServiceProcess.ServiceInstaller.DisplayName%2A> property.</span></span> <span data-ttu-id="87685-195">Na przykład *MyNewService nazwa wyświetlana*.</span><span class="sxs-lookup"><span data-stu-id="87685-195">For example, *MyNewService Display Name*.</span></span>

     <span data-ttu-id="87685-196">Ten tekst jest wyświetlany w kolumnie **Nazwa wyświetlana** okna **usługi** .</span><span class="sxs-lookup"><span data-stu-id="87685-196">This text appears in the **Display Name** column of the **Services** window.</span></span> <span data-ttu-id="87685-197">Ta nazwa może się różnić od <xref:System.ServiceProcess.ServiceInstaller.ServiceName%2A> właściwości, która jest nazwą używaną przez system (na przykład nazwę używaną przez `net start` polecenie w celu uruchomienia usługi).</span><span class="sxs-lookup"><span data-stu-id="87685-197">This name can be different from the <xref:System.ServiceProcess.ServiceInstaller.ServiceName%2A> property, which is the name the system uses (for example, the name you use for the `net start` command to start your service).</span></span>

7. <span data-ttu-id="87685-198">Ustaw <xref:System.ServiceProcess.ServiceInstaller.StartType%2A> Właściwość na wartość <xref:System.ServiceProcess.ServiceStartMode.Automatic> z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="87685-198">Set the <xref:System.ServiceProcess.ServiceInstaller.StartType%2A> property to <xref:System.ServiceProcess.ServiceStartMode.Automatic> from the drop-down list.</span></span>

8. <span data-ttu-id="87685-199">Po zakończeniu okna **Właściwości** powinny wyglądać tak, jak na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="87685-199">When you're finished, the **Properties** windows should look like the following figure:</span></span>

     <span data-ttu-id="87685-200">![Właściwości Instalatora dla usługi systemu Windows](./media/windows-service-installer-properties.png "Właściwości Instalatora usługi systemu Windows")</span><span class="sxs-lookup"><span data-stu-id="87685-200">![Installer Properties for a Windows service](./media/windows-service-installer-properties.png "Windows service installer properties")</span></span>

9. <span data-ttu-id="87685-201">W widoku **projekt** dla **ProjectInstaller**wybierz pozycję **ServiceProcessInstaller1** dla projektu Visual C# lub **ServiceProcessInstaller1** dla projektu Visual Basic, a następnie wybierz **Właściwości** z menu skrótów.</span><span class="sxs-lookup"><span data-stu-id="87685-201">In the **Design** view for **ProjectInstaller**, choose **serviceProcessInstaller1** for a Visual C# project, or **ServiceProcessInstaller1** for a Visual Basic project, then choose **Properties** from the shortcut menu.</span></span> <span data-ttu-id="87685-202">Ustaw <xref:System.ServiceProcess.ServiceProcessInstaller.Account%2A> Właściwość na wartość <xref:System.ServiceProcess.ServiceAccount.LocalSystem> z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="87685-202">Set the <xref:System.ServiceProcess.ServiceProcessInstaller.Account%2A> property to <xref:System.ServiceProcess.ServiceAccount.LocalSystem> from the drop-down list.</span></span>

     <span data-ttu-id="87685-203">To ustawienie powoduje zainstalowanie usługi i uruchomienie jej przy użyciu lokalnego konta systemowego.</span><span class="sxs-lookup"><span data-stu-id="87685-203">This setting installs the service and runs it by using the local system account.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="87685-204"><xref:System.ServiceProcess.ServiceAccount.LocalSystem>Konto ma szerokie uprawnienia, w tym możliwość zapisu w dzienniku zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="87685-204">The <xref:System.ServiceProcess.ServiceAccount.LocalSystem> account has broad permissions, including the ability to write to the event log.</span></span> <span data-ttu-id="87685-205">Należy go używać ostrożnie, ponieważ może zwiększyć ryzyko ataku przez złośliwe oprogramowanie.</span><span class="sxs-lookup"><span data-stu-id="87685-205">Use this account with caution, because it might increase your risk of attacks from malicious software.</span></span> <span data-ttu-id="87685-206">W przypadku innych zadań należy rozważyć użycie <xref:System.ServiceProcess.ServiceAccount.LocalService> konta, które działa jako użytkownik nieuprzywilejowany na komputerze lokalnym i prezentuje anonimowe poświadczenia na dowolnym serwerze zdalnym.</span><span class="sxs-lookup"><span data-stu-id="87685-206">For other tasks, consider using the <xref:System.ServiceProcess.ServiceAccount.LocalService> account, which acts as a non-privileged user on the local computer and presents anonymous credentials to any remote server.</span></span> <span data-ttu-id="87685-207">Ten przykład kończy się niepowodzeniem, jeśli spróbujesz użyć <xref:System.ServiceProcess.ServiceAccount.LocalService> konta, ponieważ wymaga ono uprawnienia do zapisu w dzienniku zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="87685-207">This example fails if you try to use the <xref:System.ServiceProcess.ServiceAccount.LocalService> account, because it needs permission to write to the event log.</span></span>

<span data-ttu-id="87685-208">Aby uzyskać więcej informacji na temat instalatorów, zobacz [jak: Dodawanie instalatorów do aplikacji usługi](how-to-add-installers-to-your-service-application.md).</span><span class="sxs-lookup"><span data-stu-id="87685-208">For more information about installers, see [How to: Add installers to your service application](how-to-add-installers-to-your-service-application.md).</span></span>

## <a name="optional-set-startup-parameters"></a><span data-ttu-id="87685-209">Obowiązkowe Ustaw parametry uruchamiania</span><span class="sxs-lookup"><span data-stu-id="87685-209">(Optional) Set startup parameters</span></span>

> [!NOTE]
> <span data-ttu-id="87685-210">Przed podjęciem decyzji o dodaniu parametrów uruchamiania należy rozważyć, czy jest to najlepszy sposób przekazywania informacji do usługi.</span><span class="sxs-lookup"><span data-stu-id="87685-210">Before you decide to add startup parameters, consider whether it's the best way to pass information to your service.</span></span> <span data-ttu-id="87685-211">Mimo że jest to łatwe w użyciu i przeanalizowanie, a użytkownik może je łatwo przesłonić, może być trudniejsze dla użytkownika do odnalezienia i użycia bez dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="87685-211">Although they're easy to use and parse, and a user can easily override them, they might be harder for a user to discover and use without documentation.</span></span> <span data-ttu-id="87685-212">Ogólnie rzecz biorąc, jeśli usługa wymaga więcej niż kilku parametrów uruchamiania, zamiast tego należy użyć rejestru lub pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="87685-212">Generally, if your service requires more than just a few startup parameters, you should use the registry or a configuration file instead.</span></span>

<span data-ttu-id="87685-213">Usługa systemu Windows może akceptować argumenty wiersza polecenia lub parametry uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="87685-213">A Windows service can accept command-line arguments, or startup parameters.</span></span> <span data-ttu-id="87685-214">Po dodaniu kodu do przetwarzania parametrów uruchamiania, użytkownik może uruchomić usługę z własnymi własnymi parametrami uruchamiania w oknie właściwości usługi.</span><span class="sxs-lookup"><span data-stu-id="87685-214">When you add code to process startup parameters, a user can start your service with their own custom startup parameters in the service properties window.</span></span> <span data-ttu-id="87685-215">Jednak te Parametry uruchomieniowe nie są zachowywane podczas następnego uruchomienia usługi.</span><span class="sxs-lookup"><span data-stu-id="87685-215">However, these startup parameters aren't persisted the next time the service starts.</span></span> <span data-ttu-id="87685-216">Aby trwale ustawić parametry uruchamiania, ustaw je w rejestrze.</span><span class="sxs-lookup"><span data-stu-id="87685-216">To set startup parameters permanently, set them in the registry.</span></span>

<span data-ttu-id="87685-217">Każda usługa systemu Windows ma wpis rejestru w podkluczu **HKEY_LOCAL_MACHINE \system\currentcontrolset\services** .</span><span class="sxs-lookup"><span data-stu-id="87685-217">Each Windows service has a registry entry under the **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services** subkey.</span></span> <span data-ttu-id="87685-218">W obszarze podklucza każdego usługi Użyj podklucza **Parameters** do przechowywania informacji, do których usługa może uzyskać dostęp.</span><span class="sxs-lookup"><span data-stu-id="87685-218">Under each service's subkey, use the **Parameters** subkey to store information that your service can access.</span></span> <span data-ttu-id="87685-219">Można używać plików konfiguracji aplikacji dla usługi systemu Windows w taki sam sposób jak w przypadku innych typów programów.</span><span class="sxs-lookup"><span data-stu-id="87685-219">You can use application configuration files for a Windows service the same way you do for other types of programs.</span></span> <span data-ttu-id="87685-220">Aby zapoznać się z przykładowym kodem, zobacz <xref:System.Configuration.ConfigurationManager.AppSettings?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="87685-220">For sample code, see <xref:System.Configuration.ConfigurationManager.AppSettings?displayProperty=nameWithType>.</span></span>

### <a name="to-add-startup-parameters"></a><span data-ttu-id="87685-221">Aby dodać parametry uruchamiania</span><span class="sxs-lookup"><span data-stu-id="87685-221">To add startup parameters</span></span>

1. <span data-ttu-id="87685-222">Wybierz pozycję **program.cs**lub **MyNewService. Designer. vb**, a następnie wybierz pozycję **Wyświetl kod** z menu skrótów.</span><span class="sxs-lookup"><span data-stu-id="87685-222">Select **Program.cs**, or **MyNewService.Designer.vb**, then choose **View Code** from the shortcut menu.</span></span> <span data-ttu-id="87685-223">W `Main` metodzie Zmień kod, aby dodać parametr wejściowy i przekazać go do konstruktora usługi:</span><span class="sxs-lookup"><span data-stu-id="87685-223">In the `Main` method, change the code to add an input parameter and pass it to the service constructor:</span></span>

   [!code-csharp[VbRadconService](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/Program-add-parameter.cs?highlight=1,6)]
   [!code-vb[VbRadconService](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.Designer-add-parameter.vb?highlight=1-2)]

2. <span data-ttu-id="87685-224">W **MyNewService.cs**lub **MyNewService. vb**Zmień `MyNewService` konstruktora, aby przetworzyć parametr wejściowy w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="87685-224">In **MyNewService.cs**, or **MyNewService.vb**, change the `MyNewService` constructor to process the input parameter as follows:</span></span>

   ```csharp
   using System.Diagnostics;

   public MyNewService(string[] args)
   {
       InitializeComponent();

       string eventSourceName = "MySource";
       string logName = "MyNewLog";

       if (args.Length > 0)
       {
          eventSourceName = args[0];
       }

       if (args.Length > 1)
       {
           logName = args[1];
       }

       eventLog1 = new EventLog();

       if (!EventLog.SourceExists(eventSourceName))
       {
           EventLog.CreateEventSource(eventSourceName, logName);
       }

       eventLog1.Source = eventSourceName;
       eventLog1.Log = logName;
   }
   ```

   ```vb
   Imports System.Diagnostics

   Public Sub New(ByVal cmdArgs() As String)
       InitializeComponent()
       Dim eventSourceName As String = "MySource"
       Dim logName As String = "MyNewLog"
       If (cmdArgs.Count() > 0) Then
           eventSourceName = cmdArgs(0)
       End If
       If (cmdArgs.Count() > 1) Then
           logName = cmdArgs(1)
       End If
       eventLog1 = New EventLog()
       If (Not EventLog.SourceExists(eventSourceName)) Then
           EventLog.CreateEventSource(eventSourceName, logName)
       End If
       eventLog1.Source = eventSourceName
       eventLog1.Log = logName
   End Sub
   ```

   <span data-ttu-id="87685-225">Ten kod ustawia Źródło zdarzenia i nazwę dziennika zgodnie z parametrami uruchamiania dostarczanymi przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="87685-225">This code sets the event source and log name according to the startup parameters that the user supplies.</span></span> <span data-ttu-id="87685-226">Jeśli nie podano argumentów, używa wartości domyślnych.</span><span class="sxs-lookup"><span data-stu-id="87685-226">If no arguments are supplied, it uses default values.</span></span>

3. <span data-ttu-id="87685-227">Aby określić argumenty wiersza polecenia, Dodaj następujący kod do `ProjectInstaller` klasy w **ProjectInstaller.cs**lub **ProjectInstaller. vb**:</span><span class="sxs-lookup"><span data-stu-id="87685-227">To specify the command-line arguments, add the following code to the `ProjectInstaller` class in **ProjectInstaller.cs**, or **ProjectInstaller.vb**:</span></span>

   ```csharp
   protected override void OnBeforeInstall(IDictionary savedState)
   {
       string parameter = "MySource1\" \"MyLogFile1";
       Context.Parameters["assemblypath"] = "\"" + Context.Parameters["assemblypath"] + "\" \"" + parameter + "\"";
       base.OnBeforeInstall(savedState);
   }
   ```

   ```vb
   Protected Overrides Sub OnBeforeInstall(ByVal savedState As IDictionary)
       Dim parameter As String = "MySource1"" ""MyLogFile1"
       Context.Parameters("assemblypath") = """" + Context.Parameters("assemblypath") + """ """ + parameter + """"
       MyBase.OnBeforeInstall(savedState)
   End Sub
   ```

   <span data-ttu-id="87685-228">Zazwyczaj ta wartość zawiera pełną ścieżkę do pliku wykonywalnego dla usługi systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="87685-228">Typically, this value contains the full path to the executable for the Windows service.</span></span> <span data-ttu-id="87685-229">Aby usługa została prawidłowo uruchomiona, użytkownik musi podać znaki cudzysłowu dla ścieżki i każdego parametru.</span><span class="sxs-lookup"><span data-stu-id="87685-229">For the service to start up correctly, the user must supply quotation marks for the path and each individual parameter.</span></span> <span data-ttu-id="87685-230">Aby zmienić parametry uruchamiania usługi systemu Windows, użytkownik może zmienić parametry w wpisie w rejestrze **ImagePath** .</span><span class="sxs-lookup"><span data-stu-id="87685-230">A user can change the parameters in the **ImagePath** registry entry to change the startup parameters for the Windows service.</span></span> <span data-ttu-id="87685-231">Lepszym sposobem jest jednak zmiana wartości programowo i udostępnienie funkcji w sposób przyjazny dla użytkownika, na przykład za pomocą narzędzia do zarządzania lub konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="87685-231">However, a better way is to change the value programmatically and expose the functionality in a user-friendly way, such as by using a management or configuration utility.</span></span>

## <a name="build-the-service"></a><span data-ttu-id="87685-232">Tworzenie usługi</span><span class="sxs-lookup"><span data-stu-id="87685-232">Build the service</span></span>

1. <span data-ttu-id="87685-233">W **Eksplorator rozwiązań**, wybierz **Właściwości** z menu skrótów dla projektu **MyNewService** .</span><span class="sxs-lookup"><span data-stu-id="87685-233">In **Solution Explorer**, choose **Properties** from the shortcut menu for the **MyNewService** project.</span></span>

   <span data-ttu-id="87685-234">Pojawią się strony właściwości projektu.</span><span class="sxs-lookup"><span data-stu-id="87685-234">The property pages for your project appear.</span></span>

2. <span data-ttu-id="87685-235">Na karcie **aplikacja** na liście **obiekt początkowy** wybierz **MyNewService. program**lub **Sub Main** dla projektów Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="87685-235">On the **Application** tab, in the **Startup object** list, choose **MyNewService.Program**, or **Sub Main** for Visual Basic projects.</span></span>

3. <span data-ttu-id="87685-236">Aby skompilować projekt, w **Eksplorator rozwiązań**wybierz opcję **Kompiluj** z menu skrótów dla projektu (lub naciśnij **klawisze CTRL** + **SHIFT** + **B**).</span><span class="sxs-lookup"><span data-stu-id="87685-236">To build the project, in **Solution Explorer**, choose **Build** from the shortcut menu for your project (or press **Ctrl**+**Shift**+**B**).</span></span>

## <a name="install-the-service"></a><span data-ttu-id="87685-237">Instalowanie usługi</span><span class="sxs-lookup"><span data-stu-id="87685-237">Install the service</span></span>

<span data-ttu-id="87685-238">Teraz, gdy została skompilowana usługa systemu Windows, możesz ją zainstalować.</span><span class="sxs-lookup"><span data-stu-id="87685-238">Now that you've built the Windows service, you can install it.</span></span> <span data-ttu-id="87685-239">Aby zainstalować usługę systemu Windows, musisz mieć poświadczenia administratora na komputerze, na którym jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="87685-239">To install a Windows service, you must have administrator credentials on the computer where it's installed.</span></span>

1. <span data-ttu-id="87685-240">Otwórz [wiersz polecenia dla deweloperów dla programu Visual Studio](https://docs.microsoft.com/dotnet/framework/tools/developer-command-prompt-for-vs) z poświadczeniami administracyjnymi.</span><span class="sxs-lookup"><span data-stu-id="87685-240">Open [Developer Command Prompt for Visual Studio](https://docs.microsoft.com/dotnet/framework/tools/developer-command-prompt-for-vs) with administrative credentials.</span></span> <span data-ttu-id="87685-241">Z menu **Start** systemu Windows wybierz opcję **wiersz polecenia dla deweloperów dla programu vs 2017** w folderze Visual Studio, a następnie wybierz pozycję **więcej**  >  **Uruchom jako administrator** z menu skrótów.</span><span class="sxs-lookup"><span data-stu-id="87685-241">From the Windows **Start** menu, select **Developer Command Prompt for VS 2017** in the Visual Studio folder, then select **More** > **Run as Administrator** from the shortcut menu.</span></span>

2. <span data-ttu-id="87685-242">W oknie **wiersz polecenia dla deweloperów dla programu Visual Studio** przejdź do folderu, który zawiera dane wyjściowe projektu (domyślnie podkatalog *\bin\debug* projektu).</span><span class="sxs-lookup"><span data-stu-id="87685-242">In the **Developer Command Prompt for Visual Studio** window, navigate to the folder that contains your project's output (by default, the *\bin\Debug* subdirectory of your project).</span></span>

3. <span data-ttu-id="87685-243">Wprowadź następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="87685-243">Enter the following command:</span></span>

    ```shell
    installutil MyNewService.exe
    ```

    <span data-ttu-id="87685-244">Jeśli usługa zostanie pomyślnie zainstalowana, polecenie zgłosi powodzenie.</span><span class="sxs-lookup"><span data-stu-id="87685-244">If the service installs successfully, the command reports success.</span></span>

    <span data-ttu-id="87685-245">Jeśli system nie może odnaleźć *installutil.exe*, upewnij się, że istnieje on na komputerze.</span><span class="sxs-lookup"><span data-stu-id="87685-245">If the system can't find *installutil.exe*, make sure that it exists on your computer.</span></span> <span data-ttu-id="87685-246">To narzędzie jest instalowane z .NET Framework do folderu \*%windir%\Microsoft.NET\Framework [64] \\ &lt; Framework wersja &gt; \*.</span><span class="sxs-lookup"><span data-stu-id="87685-246">This tool is installed with the .NET Framework to the folder *%windir%\Microsoft.NET\Framework[64]\\&lt;framework version&gt;*.</span></span> <span data-ttu-id="87685-247">Na przykład domyślną ścieżką dla wersji 64-bitowej jest *% windir% \Microsoft.NET\Framework64\v4.0.30319\InstallUtil.exe*.</span><span class="sxs-lookup"><span data-stu-id="87685-247">For example, the default path for the 64-bit version is *%windir%\Microsoft.NET\Framework64\v4.0.30319\InstallUtil.exe*.</span></span>

    <span data-ttu-id="87685-248">Jeśli proces **installutil.exe** nie powiedzie się, sprawdź dziennik instalacji, aby dowiedzieć się, dlaczego.</span><span class="sxs-lookup"><span data-stu-id="87685-248">If the **installutil.exe** process fails, check the install log to find out why.</span></span> <span data-ttu-id="87685-249">Domyślnie dziennik znajduje się w tym samym folderze co plik wykonywalny usługi.</span><span class="sxs-lookup"><span data-stu-id="87685-249">By default, the log is in the same folder as the service executable.</span></span> <span data-ttu-id="87685-250">Instalacja może zakończyć się niepowodzeniem, jeśli:</span><span class="sxs-lookup"><span data-stu-id="87685-250">The installation can fail if:</span></span>
    - <span data-ttu-id="87685-251"><xref:System.ComponentModel.RunInstallerAttribute>Klasa nie jest obecna w `ProjectInstaller` klasie.</span><span class="sxs-lookup"><span data-stu-id="87685-251">The <xref:System.ComponentModel.RunInstallerAttribute> class isn't present on the `ProjectInstaller` class.</span></span>
    - <span data-ttu-id="87685-252">Atrybut nie jest ustawiony na `true` .</span><span class="sxs-lookup"><span data-stu-id="87685-252">The attribute isn't set to `true`.</span></span>
    - <span data-ttu-id="87685-253">`ProjectInstaller`Klasa nie jest zdefiniowana jako `public` .</span><span class="sxs-lookup"><span data-stu-id="87685-253">The `ProjectInstaller` class isn't defined as `public`.</span></span>

<span data-ttu-id="87685-254">Aby uzyskać więcej informacji, zobacz [jak: Instalowanie i odinstalowywanie usług](how-to-install-and-uninstall-services.md).</span><span class="sxs-lookup"><span data-stu-id="87685-254">For more information, see [How to: Install and uninstall services](how-to-install-and-uninstall-services.md).</span></span>

## <a name="start-and-run-the-service"></a><span data-ttu-id="87685-255">Uruchom i uruchom usługę</span><span class="sxs-lookup"><span data-stu-id="87685-255">Start and run the service</span></span>

1. <span data-ttu-id="87685-256">W systemie Windows otwórz aplikację Desktop **Services** .</span><span class="sxs-lookup"><span data-stu-id="87685-256">In Windows, open the **Services** desktop app.</span></span> <span data-ttu-id="87685-257">Naciśnij pozycję **Windows** + **R** , aby otworzyć okno **uruchamiania** , wpisz *Services. msc*, a następnie naciśnij klawisz **Enter** lub wybierz **przycisk OK**.</span><span class="sxs-lookup"><span data-stu-id="87685-257">Press **Windows**+**R** to open the **Run** box, enter *services.msc*, and then press **Enter** or select **OK**.</span></span>

     <span data-ttu-id="87685-258">Twoja usługa powinna zostać wyświetlona na liście **usługi**, w kolejności alfabetycznej według nazwy wyświetlanej, która została ustawiona dla tego ustawienia.</span><span class="sxs-lookup"><span data-stu-id="87685-258">You should see your service listed in **Services**, displayed alphabetically by the display name that you set for it.</span></span>

     ![MyNewService w oknie usługi.](./media/windowsservices-serviceswindow.PNG)

2. <span data-ttu-id="87685-260">Aby uruchomić usługę, wybierz pozycję **Rozpocznij** od menu skrótów usługi.</span><span class="sxs-lookup"><span data-stu-id="87685-260">To start the service, choose **Start** from the service's shortcut menu.</span></span>

3. <span data-ttu-id="87685-261">Aby zatrzymać usługę, wybierz pozycję **Zatrzymaj** w menu skrótów usługi.</span><span class="sxs-lookup"><span data-stu-id="87685-261">To stop the service, choose **Stop** from the service's shortcut menu.</span></span>

4. <span data-ttu-id="87685-262">Obowiązkowe W wierszu polecenia Użyj poleceń \*\*net start &lt; Service Name &gt; \*\* i \*\*net stop &lt; Service Name &gt; \*\* , aby uruchomić i zatrzymać usługę.</span><span class="sxs-lookup"><span data-stu-id="87685-262">(Optional) From the command line, use the commands **net start &lt;service name&gt;** and **net stop &lt;service name&gt;** to start and stop your service.</span></span>

### <a name="verify-the-event-log-output-of-your-service"></a><span data-ttu-id="87685-263">Weryfikowanie danych wyjściowych dziennika zdarzeń usługi</span><span class="sxs-lookup"><span data-stu-id="87685-263">Verify the event log output of your service</span></span>

1. <span data-ttu-id="87685-264">W systemie Windows otwórz aplikację klasyczną **Podgląd zdarzeń** .</span><span class="sxs-lookup"><span data-stu-id="87685-264">In Windows, open the **Event Viewer** desktop app.</span></span> <span data-ttu-id="87685-265">Wprowadź *Podgląd zdarzeń* na pasku wyszukiwania systemu Windows, a następnie wybierz **Podgląd zdarzeń** z wyników wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="87685-265">Enter *Event Viewer* in the Windows search bar, and then select **Event Viewer** from the search results.</span></span>

   > [!TIP]
   > <span data-ttu-id="87685-266">W programie Visual Studio można uzyskać dostęp do dzienników zdarzeń, otwierając **Eksplorator serwera** z menu **Widok** (lub naciskając klawisze **Ctrl** + **Alt** + **S**) i rozszerzając węzeł **dzienniki zdarzeń** dla komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="87685-266">In Visual Studio, you can access event logs by opening **Server Explorer** from the **View** menu (or press **Ctrl**+**Alt**+**S**) and expanding the **Event Logs** node for the local computer.</span></span>

2. <span data-ttu-id="87685-267">W **Podgląd zdarzeń**rozwiń węzeł **Dzienniki aplikacji i usług**.</span><span class="sxs-lookup"><span data-stu-id="87685-267">In **Event Viewer**, expand **Applications and Services Logs**.</span></span>

3. <span data-ttu-id="87685-268">Znajdź listę dla **myNewLog** (lub **MyLogFile1** , jeśli wykonano procedurę dodawania argumentów wiersza polecenia) i rozwiń ją.</span><span class="sxs-lookup"><span data-stu-id="87685-268">Locate the listing for **MyNewLog** (or **MyLogFile1** if you followed the procedure to add command-line arguments) and expand it.</span></span> <span data-ttu-id="87685-269">Powinny zostać wyświetlone wpisy dotyczące dwóch akcji (uruchamiania i zatrzymywania) wykonywanych przez usługę.</span><span class="sxs-lookup"><span data-stu-id="87685-269">You should see the entries for the two actions (start and stop) that your service performed.</span></span>

     ![Użyj Podgląd zdarzeń, aby wyświetlić wpisy dziennika zdarzeń](./media/windows-service-event-viewer.png)

## <a name="clean-up-resources"></a><span data-ttu-id="87685-271">Czyszczenie zasobów</span><span class="sxs-lookup"><span data-stu-id="87685-271">Clean up resources</span></span>

<span data-ttu-id="87685-272">Jeśli aplikacja usługi systemu Windows nie jest już potrzebna, można ją usunąć.</span><span class="sxs-lookup"><span data-stu-id="87685-272">If you no longer need the Windows service app, you can remove it.</span></span>

1. <span data-ttu-id="87685-273">Otwórz **wiersz polecenia dla deweloperów dla programu Visual Studio** z poświadczeniami administracyjnymi.</span><span class="sxs-lookup"><span data-stu-id="87685-273">Open **Developer Command Prompt for Visual Studio** with administrative credentials.</span></span>

2. <span data-ttu-id="87685-274">W oknie **wiersz polecenia dla deweloperów dla programu Visual Studio** przejdź do folderu, który zawiera dane wyjściowe projektu.</span><span class="sxs-lookup"><span data-stu-id="87685-274">In the **Developer Command Prompt for Visual Studio** window, navigate to the folder that contains your project's output.</span></span>

3. <span data-ttu-id="87685-275">Wprowadź następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="87685-275">Enter the following command:</span></span>

    ```shell
    installutil.exe /u MyNewService.exe
    ```

   <span data-ttu-id="87685-276">Jeśli usługa została pomyślnie odinstalowana, polecenie zgłosi, że usługa została pomyślnie usunięta.</span><span class="sxs-lookup"><span data-stu-id="87685-276">If the service uninstalls successfully, the command reports that your service was successfully removed.</span></span> <span data-ttu-id="87685-277">Aby uzyskać więcej informacji, zobacz [jak: Instalowanie i odinstalowywanie usług](how-to-install-and-uninstall-services.md).</span><span class="sxs-lookup"><span data-stu-id="87685-277">For more information, see [How to: Install and uninstall services](how-to-install-and-uninstall-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="87685-278">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="87685-278">Next steps</span></span>

<span data-ttu-id="87685-279">Teraz, gdy została utworzona usługa, możesz:</span><span class="sxs-lookup"><span data-stu-id="87685-279">Now that you've created the service, you can:</span></span>

- <span data-ttu-id="87685-280">Utwórz autonomiczny program instalacyjny, który będzie używany przez inne osoby do instalacji usługi systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="87685-280">Create a standalone setup program for others to use to install your Windows service.</span></span> <span data-ttu-id="87685-281">Użyj zestawu [narzędzi WIX](https://wixtoolset.org/) , aby utworzyć Instalatora dla usługi systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="87685-281">Use the [WiX Toolset](https://wixtoolset.org/) to create an installer for a Windows service.</span></span> <span data-ttu-id="87685-282">Aby poznać inne pomysły, zobacz [Tworzenie pakietu Instalatora](/visualstudio/deployment/deploying-applications-services-and-components#create-an-installer-package-windows-desktop).</span><span class="sxs-lookup"><span data-stu-id="87685-282">For other ideas, see [Create an installer package](/visualstudio/deployment/deploying-applications-services-and-components#create-an-installer-package-windows-desktop).</span></span>

- <span data-ttu-id="87685-283">Eksploruj <xref:System.ServiceProcess.ServiceController> składnik, który umożliwia wysyłanie poleceń do zainstalowanej usługi.</span><span class="sxs-lookup"><span data-stu-id="87685-283">Explore the <xref:System.ServiceProcess.ServiceController> component, which enables you to send commands to the service you've installed.</span></span>

- <span data-ttu-id="87685-284">Zamiast tworzyć dziennik zdarzeń, gdy aplikacja jest uruchomiona, użyj Instalatora, aby utworzyć dziennik zdarzeń podczas instalowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="87685-284">Instead of creating the event log when the application runs, use an installer to create an event log when you install the application.</span></span> <span data-ttu-id="87685-285">Dziennik zdarzeń jest usuwany przez Instalatora podczas odinstalowywania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="87685-285">The event log is deleted by the installer when you uninstall the application.</span></span> <span data-ttu-id="87685-286">Aby uzyskać więcej informacji, zobacz <xref:System.Diagnostics.EventLogInstaller>.</span><span class="sxs-lookup"><span data-stu-id="87685-286">For more information, see <xref:System.Diagnostics.EventLogInstaller>.</span></span>

## <a name="see-also"></a><span data-ttu-id="87685-287">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="87685-287">See also</span></span>

- [<span data-ttu-id="87685-288">Aplikacje usług systemu Windows</span><span class="sxs-lookup"><span data-stu-id="87685-288">Windows service applications</span></span>](index.md)
- [<span data-ttu-id="87685-289">Wprowadzenie do aplikacji usług systemu Windows</span><span class="sxs-lookup"><span data-stu-id="87685-289">Introduction to Windows service applications</span></span>](introduction-to-windows-service-applications.md)
- [<span data-ttu-id="87685-290">Instrukcje: debugowanie aplikacji usługi systemu Windows</span><span class="sxs-lookup"><span data-stu-id="87685-290">How to: Debug Windows service applications</span></span>](how-to-debug-windows-service-applications.md)
- [<span data-ttu-id="87685-291">Usługi (Windows)</span><span class="sxs-lookup"><span data-stu-id="87685-291">Services (Windows)</span></span>](/windows/desktop/Services/services)
