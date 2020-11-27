---
title: Używanie liczników wydajności
ms.date: 03/30/2017
ms.assetid: 00a787af-1876-473c-a48d-f52b51e28a3f
ms.openlocfilehash: d3e6b9805bd0b9c5eea991fce4dde2035f8f5c1b
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96294914"
---
# <a name="using-performance-counters"></a><span data-ttu-id="4fe20-102">Używanie liczników wydajności</span><span class="sxs-lookup"><span data-stu-id="4fe20-102">Using Performance Counters</span></span>

<span data-ttu-id="4fe20-103">W tym przykładzie pokazano, jak uzyskać dostęp do liczników wydajności Windows Communication Foundation (WCF) oraz jak tworzyć liczniki wydajności zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4fe20-103">This sample demonstrates how to access Windows Communication Foundation (WCF) performance counters and how to create user-defined performance counters.</span></span> <span data-ttu-id="4fe20-104">Ten przykład jest oparty na [wprowadzenie](getting-started-sample.md).</span><span class="sxs-lookup"><span data-stu-id="4fe20-104">This sample is based on the [Getting Started](getting-started-sample.md).</span></span>  
  
> [!NOTE]
> <span data-ttu-id="4fe20-105">Procedura instalacji i instrukcje dotyczące kompilacji dla tego przykładu znajdują się na końcu tego tematu.</span><span class="sxs-lookup"><span data-stu-id="4fe20-105">The setup procedure and build instructions for this sample are located at the end of this topic.</span></span>  
  
 <span data-ttu-id="4fe20-106">W tym przykładzie klient wywołuje cztery metody `ICalculator` usługi.</span><span class="sxs-lookup"><span data-stu-id="4fe20-106">In this sample, the client calls the four methods of the `ICalculator` service.</span></span> <span data-ttu-id="4fe20-107">Klient kontynuuje działanie, dopóki nie zostanie on przerwany przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4fe20-107">The client continues to do this until it is interrupted by the user.</span></span> <span data-ttu-id="4fe20-108">Usługa pozostaje niezmieniona.</span><span class="sxs-lookup"><span data-stu-id="4fe20-108">The service remains unchanged.</span></span>  
  
 <span data-ttu-id="4fe20-109">Liczniki wydajności są włączone w sekcji Diagnostyka pliku Web.config dla usługi, jak pokazano w poniższej konfiguracji przykładowej.</span><span class="sxs-lookup"><span data-stu-id="4fe20-109">Performance counters are enabled in the diagnostics section of the Web.config file for the service, as shown in the following sample configuration.</span></span>  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <diagnostics performanceCounters="All" />
  </system.serviceModel>  
</configuration>  
```  
  
 <span data-ttu-id="4fe20-110">To zadanie można również wykonać za pomocą [Narzędzia Edytora konfiguracji (SvcConfigEditor.exe)](../configuration-editor-tool-svcconfigeditor-exe.md).</span><span class="sxs-lookup"><span data-stu-id="4fe20-110">This task can also be done using the [Configuration Editor Tool (SvcConfigEditor.exe)](../configuration-editor-tool-svcconfigeditor-exe.md).</span></span>  
  
 <span data-ttu-id="4fe20-111">Po włączeniu liczników wydajności cały pakiet liczników wydajności programu WCF jest włączony dla usługi.</span><span class="sxs-lookup"><span data-stu-id="4fe20-111">When performance counters are enabled, the entire suite of WCF performance counters is enabled for the service.</span></span> <span data-ttu-id="4fe20-112">.NET Framework automatycznie utrzymuje dane dotyczące wydajności na trzech poziomach: `ServiceModelService` , `ServiceModelEndpoint` i `ServiceModelOperation` .</span><span class="sxs-lookup"><span data-stu-id="4fe20-112">The .NET Framework automatically maintains performance data at three levels: `ServiceModelService`, `ServiceModelEndpoint` and `ServiceModelOperation`.</span></span> <span data-ttu-id="4fe20-113">Każdy z tych poziomów ma liczniki wydajności, takie jak "wywołania", "wywołania na sekundę" i "wywołania zabezpieczeń, które nie są autoryzowane".</span><span class="sxs-lookup"><span data-stu-id="4fe20-113">Each of these levels has performance counters such as "Calls", "Calls per Second", and "Security Calls Not Authorized".</span></span>  
  
### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="4fe20-114">Aby skonfigurować, skompilować i uruchomić przykład</span><span class="sxs-lookup"><span data-stu-id="4fe20-114">To set up, build, and run the sample</span></span>  
  
1. <span data-ttu-id="4fe20-115">Upewnij się, że została wykonana [Procedura konfiguracji jednorazowej dla przykładów Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4fe20-115">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>  
  
2. <span data-ttu-id="4fe20-116">Aby skompilować wersję rozwiązania w języku C# lub Visual Basic .NET, postępuj zgodnie z instrukcjami w temacie [Tworzenie przykładów Windows Communication Foundation](building-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4fe20-116">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>  
  
3. <span data-ttu-id="4fe20-117">Aby uruchomić przykład w konfiguracji na jednym lub wielu komputerach, postępuj zgodnie z instrukcjami w temacie [Uruchamianie przykładów Windows Communication Foundation](running-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4fe20-117">To run the sample in a single- or cross-computer configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>  
  
### <a name="to-view-performance-data"></a><span data-ttu-id="4fe20-118">Aby wyświetlić dane wydajności</span><span class="sxs-lookup"><span data-stu-id="4fe20-118">To view performance data</span></span>  
  
1. <span data-ttu-id="4fe20-119">Uruchom narzędzie Monitor wydajności, klikając przycisk **Start**, **Uruchom polecenie...**, wprowadź `perfmon` i kliknij przycisk **OK,** lub z panelu sterowania wybierz pozycję **Narzędzia administracyjne** , a następnie kliknij dwukrotnie pozycję **wydajność**.</span><span class="sxs-lookup"><span data-stu-id="4fe20-119">Start the Performance Monitor Tool by clicking **Start**, **Run…**, enter `perfmon` and click **OK,** or from Control Panel, select **Administrative Tools** and double-click **Performance**.</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="4fe20-120">Nie można dodać liczników do momentu uruchomienia przykładowego kodu.</span><span class="sxs-lookup"><span data-stu-id="4fe20-120">You cannot add counters until the sample code is running.</span></span>  
  
2. <span data-ttu-id="4fe20-121">Usuń liczniki wydajności, które znajdują się na liście, zaznaczając je i naciskając klawisz Delete.</span><span class="sxs-lookup"><span data-stu-id="4fe20-121">Remove the performance counters that are listed by selecting them and pressing the Delete key.</span></span>  
  
3. <span data-ttu-id="4fe20-122">Dodaj liczniki WCF, klikając prawym przyciskiem myszy okienko wykresu i wybierając polecenie **Dodaj liczniki**.</span><span class="sxs-lookup"><span data-stu-id="4fe20-122">Add WCF counters by right-clicking the graph pane and selecting **Add Counters**.</span></span> <span data-ttu-id="4fe20-123">W oknie dialogowym **Dodawanie liczników** wybierz pozycję **ServiceModelOperation 3.0.0.0, ServiceModelEndpoint 3.0.0.0 lub ServiceModelService 3.0.0.0** w polu listy rozwijanej obiekt wydajności.</span><span class="sxs-lookup"><span data-stu-id="4fe20-123">In the **Add Counters** dialog box, select **ServiceModelOperation 3.0.0.0, ServiceModelEndpoint 3.0.0.0, or ServiceModelService 3.0.0.0** in the Performance object drop down list box.</span></span> <span data-ttu-id="4fe20-124">Wybierz liczniki, które chcesz wyświetlić z listy.</span><span class="sxs-lookup"><span data-stu-id="4fe20-124">Select the counters you want to view from the list.</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="4fe20-125">Brak liczników wydajności programu WCF dla usługi, jeśli na komputerze nie są uruchomione żadne usługi WCF.</span><span class="sxs-lookup"><span data-stu-id="4fe20-125">There are no WCF performance counters for a service if there are no WCF services running on the computer.</span></span>  
  
### <a name="to-use-the-configuration-editor-to-enable-counters"></a><span data-ttu-id="4fe20-126">Aby włączyć liczniki przy użyciu edytora konfiguracji</span><span class="sxs-lookup"><span data-stu-id="4fe20-126">To use the Configuration Editor to enable counters</span></span>  
  
1. <span data-ttu-id="4fe20-127">Otwórz wystąpienie SvcConfigEditor.exe.</span><span class="sxs-lookup"><span data-stu-id="4fe20-127">Open an instance of the SvcConfigEditor.exe.</span></span>  
  
2. <span data-ttu-id="4fe20-128">W menu plik kliknij polecenie **Otwórz** , a następnie kliknij pozycję **plik konfiguracji..**..</span><span class="sxs-lookup"><span data-stu-id="4fe20-128">On the File menu, click **Open** and then click **Config file…**.</span></span>  
  
3. <span data-ttu-id="4fe20-129">Przejdź do folderu usługi przykładowej aplikacji i Otwórz plik Web.config.</span><span class="sxs-lookup"><span data-stu-id="4fe20-129">Navigate to the sample application's service folder and open the Web.config file.</span></span>  
  
4. <span data-ttu-id="4fe20-130">W drzewie konfiguracji kliknij pozycję **Diagnostyka** .</span><span class="sxs-lookup"><span data-stu-id="4fe20-130">Click **Diagnostics** on the Configuration tree.</span></span>  
  
5. <span data-ttu-id="4fe20-131">Przełącz **licznik wydajności** w oknie **Diagnostyka** , aby pokazać opcję "wszystkie".</span><span class="sxs-lookup"><span data-stu-id="4fe20-131">Toggle **Performance Counter** in the **Diagnostics** window to show 'All'.</span></span>  
  
6. <span data-ttu-id="4fe20-132">Zapisz plik konfiguracji i Zamknij Edytor.</span><span class="sxs-lookup"><span data-stu-id="4fe20-132">Save the configuration file and exit the editor.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="4fe20-133">Przykłady mogą być już zainstalowane na komputerze.</span><span class="sxs-lookup"><span data-stu-id="4fe20-133">The samples may already be installed on your computer.</span></span> <span data-ttu-id="4fe20-134">Przed kontynuowaniem Wyszukaj następujący katalog (domyślny).</span><span class="sxs-lookup"><span data-stu-id="4fe20-134">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="4fe20-135">Jeśli ten katalog nie istnieje, przejdź do [przykładów Windows Communication Foundation (WCF) i Windows Workflow Foundation (WF) dla .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) , aby pobrać wszystkie Windows Communication Foundation (WCF) i [!INCLUDE[wf1](../../../../includes/wf1-md.md)] przykłady.</span><span class="sxs-lookup"><span data-stu-id="4fe20-135">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="4fe20-136">Ten przykład znajduje się w następującym katalogu.</span><span class="sxs-lookup"><span data-stu-id="4fe20-136">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Management\PerfCounters`  
  
## <a name="see-also"></a><span data-ttu-id="4fe20-137">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="4fe20-137">See also</span></span>

- <span data-ttu-id="4fe20-138">[Przykłady monitorowania oprogramowania AppFabric](/previous-versions/appfabric/ff383407(v=azure.10))</span><span class="sxs-lookup"><span data-stu-id="4fe20-138">[AppFabric Monitoring Samples](/previous-versions/appfabric/ff383407(v=azure.10))</span></span>
