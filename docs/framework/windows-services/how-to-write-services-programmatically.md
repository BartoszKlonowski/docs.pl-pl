---
title: 'Instrukcje: Programowane pisanie usług'
description: Zobacz, jak programowo pisać usługi, konfigurując dziedziczenie i inne elementy infrastruktury samodzielnie.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- services, creating
- Windows Service applications, creating
ms.assetid: 3abbb2ec-78d2-41e6-b9f9-6662d4e2cdc7
ms.openlocfilehash: cd749d325bec6636243dec1905f79abb5e42f04e
ms.sourcegitcommit: 97405ed212f69b0a32faa66a5d5fae7e76628b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/01/2020
ms.locfileid: "91608403"
---
# <a name="how-to-write-services-programmatically"></a><span data-ttu-id="3f9b9-103">Instrukcje: Programowane pisanie usług</span><span class="sxs-lookup"><span data-stu-id="3f9b9-103">How to: Write Services Programmatically</span></span>
<span data-ttu-id="3f9b9-104">Jeśli zdecydujesz się nie używać szablonu projektu usługi systemu Windows, możesz napisać własne usługi, konfigurując dziedziczenie i inne elementy infrastruktury samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="3f9b9-104">If you choose not to use the Windows Service project template, you can write your own services by setting up the inheritance and other infrastructure elements yourself.</span></span> <span data-ttu-id="3f9b9-105">W przypadku programistycznego tworzenia usługi należy wykonać kilka czynności, dla których szablon mógłby obsłużyć:</span><span class="sxs-lookup"><span data-stu-id="3f9b9-105">When you create a service programmatically, you must perform several steps that the template would otherwise handle for you:</span></span>  
  
- <span data-ttu-id="3f9b9-106">Należy skonfigurować klasę usługi, aby dziedziczyć z <xref:System.ServiceProcess.ServiceBase> klasy.</span><span class="sxs-lookup"><span data-stu-id="3f9b9-106">You must set up your service class to inherit from the <xref:System.ServiceProcess.ServiceBase> class.</span></span>  
  
- <span data-ttu-id="3f9b9-107">Należy utworzyć `Main` metodę dla projektu usługi, który definiuje usługi do uruchomienia i wywołuje <xref:System.ServiceProcess.ServiceBase.Run%2A> metodę z nich.</span><span class="sxs-lookup"><span data-stu-id="3f9b9-107">You must create a `Main` method for your service project that defines the services to run and calls the <xref:System.ServiceProcess.ServiceBase.Run%2A> method on them.</span></span>  
  
- <span data-ttu-id="3f9b9-108">Należy zastąpić <xref:System.ServiceProcess.ServiceBase.OnStart%2A> <xref:System.ServiceProcess.ServiceBase.OnStop%2A> procedury i wprowadzić dowolny kod, który ma zostać uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="3f9b9-108">You must override the <xref:System.ServiceProcess.ServiceBase.OnStart%2A> and <xref:System.ServiceProcess.ServiceBase.OnStop%2A> procedures and fill in any code you want them to run.</span></span>  
  
### <a name="to-write-a-service-programmatically"></a><span data-ttu-id="3f9b9-109">Aby programowo napisać usługę</span><span class="sxs-lookup"><span data-stu-id="3f9b9-109">To write a service programmatically</span></span>  
  
1. <span data-ttu-id="3f9b9-110">Utwórz pusty projekt i Utwórz odwołanie do odpowiednich przestrzeni nazw, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="3f9b9-110">Create an empty project and create a reference to the necessary namespaces by following these steps:</span></span>  
  
    1. <span data-ttu-id="3f9b9-111">W **Eksplorator rozwiązań**kliknij prawym przyciskiem myszy węzeł **odwołania** i kliknij polecenie **Dodaj odwołanie**.</span><span class="sxs-lookup"><span data-stu-id="3f9b9-111">In **Solution Explorer**, right-click the **References** node and click **Add Reference**.</span></span>  
  
    2. <span data-ttu-id="3f9b9-112">Na karcie **.NET Framework** przewiń do **System.dll** i kliknij pozycję **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="3f9b9-112">On the **.NET Framework** tab, scroll to **System.dll** and click **Select**.</span></span>  
  
    3. <span data-ttu-id="3f9b9-113">Przewiń do **System.ServiceProcess.dll** i kliknij przycisk **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="3f9b9-113">Scroll to **System.ServiceProcess.dll** and click **Select**.</span></span>  
  
    4. <span data-ttu-id="3f9b9-114">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="3f9b9-114">Click **OK**.</span></span>  
  
2. <span data-ttu-id="3f9b9-115">Dodaj klasę i skonfiguruj ją, aby dziedziczyć z <xref:System.ServiceProcess.ServiceBase> :</span><span class="sxs-lookup"><span data-stu-id="3f9b9-115">Add a class and configure it to inherit from <xref:System.ServiceProcess.ServiceBase>:</span></span>  
  
     [!code-csharp[VbRadconService#7](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#7)]
     [!code-vb[VbRadconService#7](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#7)]  
  
3. <span data-ttu-id="3f9b9-116">Dodaj następujący kod, aby skonfigurować klasę usługi:</span><span class="sxs-lookup"><span data-stu-id="3f9b9-116">Add the following code to configure your service class:</span></span>  
  
     [!code-csharp[VbRadconService#8](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#8)]
     [!code-vb[VbRadconService#8](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#8)]  
  
4. <span data-ttu-id="3f9b9-117">Utwórz `Main` metodę dla klasy i użyj jej do zdefiniowania usługi, która będzie zawierała Klasa; `userService1` jest nazwą klasy:</span><span class="sxs-lookup"><span data-stu-id="3f9b9-117">Create a `Main` method for your class, and use it to define the service your class will contain; `userService1` is the name of the class:</span></span>  
  
     [!code-csharp[VbRadconService#9](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#9)]
     [!code-vb[VbRadconService#9](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#9)]  
  
5. <span data-ttu-id="3f9b9-118">Zastąp <xref:System.ServiceProcess.ServiceBase.OnStart%2A> metodę i zdefiniuj wszelkie przetwarzanie, które mają być wykonywane, gdy usługa zostanie uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="3f9b9-118">Override the <xref:System.ServiceProcess.ServiceBase.OnStart%2A> method, and define any processing you want to occur when your service is started.</span></span>  
  
     [!code-csharp[VbRadconService#10](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#10)]
     [!code-vb[VbRadconService#10](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#10)]  
  
6. <span data-ttu-id="3f9b9-119">Zastąp wszystkie inne metody, dla których chcesz zdefiniować niestandardowe przetwarzanie, i napisz kod, aby określić działania, które usługa powinna wykonać w każdym przypadku.</span><span class="sxs-lookup"><span data-stu-id="3f9b9-119">Override any other methods you want to define custom processing for, and write code to determine the actions the service should take in each case.</span></span>  
  
7. <span data-ttu-id="3f9b9-120">Dodanie niezbędnych instalatorów dla aplikacji usługi.</span><span class="sxs-lookup"><span data-stu-id="3f9b9-120">Add the necessary installers for your service application.</span></span> <span data-ttu-id="3f9b9-121">Aby uzyskać więcej informacji, zobacz [jak: Dodawanie instalatorów do aplikacji usługi](how-to-add-installers-to-your-service-application.md).</span><span class="sxs-lookup"><span data-stu-id="3f9b9-121">For more information, see [How to: Add Installers to Your Service Application](how-to-add-installers-to-your-service-application.md).</span></span>  
  
8. <span data-ttu-id="3f9b9-122">Skompiluj projekt, wybierając opcję **Kompiluj rozwiązanie** w menu **kompilacja** .</span><span class="sxs-lookup"><span data-stu-id="3f9b9-122">Build your project by selecting **Build Solution** from the **Build** menu.</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="3f9b9-123">Nie należy naciskać klawisza F5, aby uruchomić projekt — nie można uruchomić projektu usługi w ten sposób.</span><span class="sxs-lookup"><span data-stu-id="3f9b9-123">Do not press F5 to run your project — you cannot run a service project in this way.</span></span>  
  
9. <span data-ttu-id="3f9b9-124">Utwórz projekt konfiguracji i akcje niestandardowe w celu zainstalowania usługi.</span><span class="sxs-lookup"><span data-stu-id="3f9b9-124">Create a setup project and the custom actions to install your service.</span></span> <span data-ttu-id="3f9b9-125">Aby zapoznać się z przykładem, zobacz [Przewodnik: Tworzenie aplikacji usługi systemu Windows w projektancie składników](walkthrough-creating-a-windows-service-application-in-the-component-designer.md).</span><span class="sxs-lookup"><span data-stu-id="3f9b9-125">For an example, see [Walkthrough: Creating a Windows Service Application in the Component Designer](walkthrough-creating-a-windows-service-application-in-the-component-designer.md).</span></span>  
  
10. <span data-ttu-id="3f9b9-126">Zainstaluj usługę.</span><span class="sxs-lookup"><span data-stu-id="3f9b9-126">Install the service.</span></span> <span data-ttu-id="3f9b9-127">Aby uzyskać więcej informacji, zobacz [jak: Instalowanie i odinstalowywanie usług](how-to-install-and-uninstall-services.md).</span><span class="sxs-lookup"><span data-stu-id="3f9b9-127">For more information, see [How to: Install and Uninstall Services](how-to-install-and-uninstall-services.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="3f9b9-128">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="3f9b9-128">See also</span></span>

- [<span data-ttu-id="3f9b9-129">Wprowadzenie do aplikacji usług systemu Windows</span><span class="sxs-lookup"><span data-stu-id="3f9b9-129">Introduction to Windows Service Applications</span></span>](introduction-to-windows-service-applications.md)
- [<span data-ttu-id="3f9b9-130">Instrukcje: Tworzenie usług systemu Windows</span><span class="sxs-lookup"><span data-stu-id="3f9b9-130">How to: Create Windows Services</span></span>](how-to-create-windows-services.md)
- [<span data-ttu-id="3f9b9-131">Instrukcje: Dodawanie instalatorów od aplikacji usług</span><span class="sxs-lookup"><span data-stu-id="3f9b9-131">How to: Add Installers to Your Service Application</span></span>](how-to-add-installers-to-your-service-application.md)
- [<span data-ttu-id="3f9b9-132">Instrukcje: Rejestrowanie informacji o usługach</span><span class="sxs-lookup"><span data-stu-id="3f9b9-132">How to: Log Information About Services</span></span>](how-to-log-information-about-services.md)
- [<span data-ttu-id="3f9b9-133">Przewodnik: tworzenie aplikacji usługowej systemu Windows w Projektancie składników</span><span class="sxs-lookup"><span data-stu-id="3f9b9-133">Walkthrough: Creating a Windows Service Application in the Component Designer</span></span>](walkthrough-creating-a-windows-service-application-in-the-component-designer.md)
