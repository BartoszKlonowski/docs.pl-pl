---
title: Tworzenie działań przepływu pracy przy użyciu klasy elementu CodeActivity
ms.date: 03/30/2017
ms.assetid: cfe315c1-f86d-43ec-b9ce-2f8c469b1106
ms.openlocfilehash: 714e0971a006db20d002b0f3a486533b1357fba7
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96293822"
---
# <a name="workflow-activity-authoring-using-the-codeactivity-class"></a><span data-ttu-id="dbb92-102">Tworzenie działań przepływu pracy przy użyciu klasy elementu CodeActivity</span><span class="sxs-lookup"><span data-stu-id="dbb92-102">Workflow Activity Authoring Using the CodeActivity Class</span></span>

<span data-ttu-id="dbb92-103">Działania utworzone przez dziedziczenie z <xref:System.Activities.CodeActivity> mogą implementować podstawowe zachowanie, zastępując <xref:System.Activities.CodeActivity.Execute%2A> metodę.</span><span class="sxs-lookup"><span data-stu-id="dbb92-103">Activities created by inheriting from <xref:System.Activities.CodeActivity> can implement basic imperative behavior by overriding the <xref:System.Activities.CodeActivity.Execute%2A> method.</span></span>

## <a name="using-codeactivitycontext"></a><span data-ttu-id="dbb92-104">Korzystanie z CodeActivityContext</span><span class="sxs-lookup"><span data-stu-id="dbb92-104">Using CodeActivityContext</span></span>

 <span data-ttu-id="dbb92-105">Dostęp do funkcji środowiska uruchomieniowego przepływu pracy można uzyskać z poziomu <xref:System.Activities.CodeActivity.Execute%2A> metody przy użyciu elementów członkowskich `context` parametru typu <xref:System.Activities.CodeActivityContext> .</span><span class="sxs-lookup"><span data-stu-id="dbb92-105">Features of the workflow runtime can be accessed from within the <xref:System.Activities.CodeActivity.Execute%2A> method by using members of the `context` parameter, of type <xref:System.Activities.CodeActivityContext>.</span></span> <span data-ttu-id="dbb92-106">Dostępne są następujące funkcje <xref:System.Activities.CodeActivityContext> :</span><span class="sxs-lookup"><span data-stu-id="dbb92-106">The features available through <xref:System.Activities.CodeActivityContext> include the following:</span></span>

- <span data-ttu-id="dbb92-107">Pobieranie i ustawianie wartości zmiennych i argumentów.</span><span class="sxs-lookup"><span data-stu-id="dbb92-107">Getting and setting the values of variables and arguments.</span></span>

- <span data-ttu-id="dbb92-108">Niestandardowe funkcje śledzenia przy użyciu programu <xref:System.Activities.CodeActivityContext.Track%2A> .</span><span class="sxs-lookup"><span data-stu-id="dbb92-108">Custom tracking features using <xref:System.Activities.CodeActivityContext.Track%2A>.</span></span>

- <span data-ttu-id="dbb92-109">Dostęp do właściwości wykonywania działania przy użyciu <xref:System.Activities.CodeActivityContext.GetProperty%2A> .</span><span class="sxs-lookup"><span data-stu-id="dbb92-109">Access to the activity’s execution properties using <xref:System.Activities.CodeActivityContext.GetProperty%2A>.</span></span>

#### <a name="to-create-a-custom-activity-that-inherits-from-codeactivity"></a><span data-ttu-id="dbb92-110">Aby utworzyć niestandardowe działanie, które dziedziczy z elementu CodeActivity</span><span class="sxs-lookup"><span data-stu-id="dbb92-110">To create a custom activity that inherits from CodeActivity</span></span>

1. <span data-ttu-id="dbb92-111">Otwórz program Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="dbb92-111">Open Visual Studio 2010.</span></span>

2. <span data-ttu-id="dbb92-112">Wybierz kolejno opcje **plik**, **Nowy** i **projekt**.</span><span class="sxs-lookup"><span data-stu-id="dbb92-112">Select **File**, **New**, and then **Project**.</span></span> <span data-ttu-id="dbb92-113">Wybierz pozycję **Workflow 4,0** w obszarze **Visual C#** w oknie **typy projektów** , a następnie wybierz węzeł **V2010** .</span><span class="sxs-lookup"><span data-stu-id="dbb92-113">Select **Workflow 4.0** under **Visual C#** in the **Project Types** window, and select the **v2010** node.</span></span> <span data-ttu-id="dbb92-114">Wybierz pozycję **Biblioteka działań** w oknie **Szablony** .</span><span class="sxs-lookup"><span data-stu-id="dbb92-114">Select **Activity Library** in the **Templates** window.</span></span> <span data-ttu-id="dbb92-115">Nadaj nazwę nowej powitaniu projektu.</span><span class="sxs-lookup"><span data-stu-id="dbb92-115">Name the new project HelloActivity.</span></span>

3. <span data-ttu-id="dbb92-116">Kliknij prawym przyciskiem myszy pozycję zakończeniu. XAML w projekcie Hello i wybierz polecenie **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="dbb92-116">Right-click Activity1.xaml in the HelloActivity project and select **Delete**.</span></span>

4. <span data-ttu-id="dbb92-117">Kliknij prawym przyciskiem myszy projekt Hello i wybierz polecenie **Dodaj** , a następnie **klasy**.</span><span class="sxs-lookup"><span data-stu-id="dbb92-117">Right-click the HelloActivity project and select **Add** , and then **Class**.</span></span> <span data-ttu-id="dbb92-118">Nadaj nowej klasie nazwę HelloActivity.cs.</span><span class="sxs-lookup"><span data-stu-id="dbb92-118">Name the new class HelloActivity.cs.</span></span>

5. <span data-ttu-id="dbb92-119">W pliku HelloActivity.cs Dodaj następujące `using` dyrektywy.</span><span class="sxs-lookup"><span data-stu-id="dbb92-119">In the HelloActivity.cs file, add the following `using` directives.</span></span>

    ```csharp
    using System.Activities;
    using System.Activities.Statements;
    ```

6. <span data-ttu-id="dbb92-120">Uczyń nową klasę dziedziczą <xref:System.Activities.CodeActivity> przez dodanie klasy bazowej do deklaracji klasy.</span><span class="sxs-lookup"><span data-stu-id="dbb92-120">Make the new class inherit from <xref:System.Activities.CodeActivity> by adding a base class to the class declaration.</span></span>

    ```csharp
    class HelloActivity : CodeActivity
    ```

7. <span data-ttu-id="dbb92-121">Dodaj funkcję do klasy, dodając <xref:System.Activities.CodeActivity.Execute%2A> metodę.</span><span class="sxs-lookup"><span data-stu-id="dbb92-121">Add functionality to the class by adding an <xref:System.Activities.CodeActivity.Execute%2A> method.</span></span>

    ```csharp
    protected override void Execute(CodeActivityContext context)
    {
        Console.WriteLine("Hello World!");
    }
    ```

8. <span data-ttu-id="dbb92-122">Użyj, <xref:System.Activities.CodeActivityContext> Aby utworzyć rekord śledzenia.</span><span class="sxs-lookup"><span data-stu-id="dbb92-122">Use the <xref:System.Activities.CodeActivityContext> to create a tracking record.</span></span>

    ```csharp
    protected override void Execute(CodeActivityContext context)
    {
        Console.WriteLine("Hello World!");
        CustomTrackingRecord record = new CustomTrackingRecord("MyRecord");
        record.Data.Add(new KeyValuePair<String, Object>("ExecutionTime", DateTime.Now));
        context.Track(record);
    }
    ```
