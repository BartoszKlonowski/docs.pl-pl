---
title: 'Instrukcje: ręczne generowanie klas usługi danych klienta (Usługi danych programu WCF)'
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, configuring
- WCF Data Services, client library
ms.assetid: b98cb1d6-956a-4e50-add6-67e4f2587346
ms.openlocfilehash: 368f2546652d21be44c0ffb4cc5f279c56beda51
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91165995"
---
# <a name="how-to-manually-generate-client-data-service-classes-wcf-data-services"></a><span data-ttu-id="ef1cc-102">Instrukcje: ręczne generowanie klas usługi danych klienta (Usługi danych programu WCF)</span><span class="sxs-lookup"><span data-stu-id="ef1cc-102">How to: Manually Generate Client Data Service Classes (WCF Data Services)</span></span>

<span data-ttu-id="ef1cc-103">Usługi danych programu WCF integruje się z programem Visual Studio, aby umożliwić automatyczne generowanie klas usługi danych klienta w przypadku używania okna dialogowego **Dodaj odwołanie do usługi** do dodawania odwołania do usługi danych w projekcie programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ef1cc-103">WCF Data Services integrates with Visual Studio to enable you to automatically generate client data service classes when you use the **Add Service Reference** dialog box to add a reference to a data service in a Visual Studio project.</span></span> <span data-ttu-id="ef1cc-104">Aby uzyskać więcej informacji, zobacz [jak: Dodawanie odwołania do usługi danych](how-to-add-a-data-service-reference-wcf-data-services.md).</span><span class="sxs-lookup"><span data-stu-id="ef1cc-104">For more information, see [How to: Add a Data Service Reference](how-to-add-a-data-service-reference-wcf-data-services.md).</span></span> <span data-ttu-id="ef1cc-105">Można również ręcznie generować te same klasy usługi danych klienta przy użyciu narzędzia do generowania kodu `DataSvcUtil.exe` .</span><span class="sxs-lookup"><span data-stu-id="ef1cc-105">You can also manually generate the same client data service classes by using the code-generation tool, `DataSvcUtil.exe`.</span></span> <span data-ttu-id="ef1cc-106">To narzędzie, które jest dołączone do Usługi danych programu WCF, generuje klasy .NET Framework z definicji usługi danych.</span><span class="sxs-lookup"><span data-stu-id="ef1cc-106">This tool, which is included with WCF Data Services, generates .NET Framework classes from the data service definition.</span></span> <span data-ttu-id="ef1cc-107">Można go również użyć do wygenerowania klas usługi danych z pliku modelu koncepcyjnego (. csdl) i pliku edmx, który reprezentuje model Entity Framework w projekcie programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ef1cc-107">It can also be used to generate data service classes from the conceptual model (.csdl) file and from the .edmx file that represents an Entity Framework model in a Visual Studio project.</span></span>

 <span data-ttu-id="ef1cc-108">W przykładzie w tym temacie opisano tworzenie klas usługi danych klienta na podstawie przykładowej usługi danych Northwind.</span><span class="sxs-lookup"><span data-stu-id="ef1cc-108">The example in this topic creates client data service classes based on the Northwind sample data service.</span></span> <span data-ttu-id="ef1cc-109">Ta usługa jest tworzona po zakończeniu [usługi danych programu WCF przewodnika Szybki Start](quickstart-wcf-data-services.md).</span><span class="sxs-lookup"><span data-stu-id="ef1cc-109">This service is created when you complete the [WCF Data Services quickstart](quickstart-wcf-data-services.md).</span></span> <span data-ttu-id="ef1cc-110">Niektóre przykłady w tym temacie wymagają pliku modelu koncepcyjnego dla modelu Northwind.</span><span class="sxs-lookup"><span data-stu-id="ef1cc-110">Some examples in this topic require the conceptual model file for the Northwind model.</span></span> <span data-ttu-id="ef1cc-111">Aby uzyskać więcej informacji, zobacz [How to: Use EdmGen.exe by wygenerować model i pliki mapowania](../adonet/ef/how-to-use-edmgen-exe-to-generate-the-model-and-mapping-files.md).</span><span class="sxs-lookup"><span data-stu-id="ef1cc-111">For more information, see [How to: Use EdmGen.exe to Generate the Model and Mapping Files](../adonet/ef/how-to-use-edmgen-exe-to-generate-the-model-and-mapping-files.md).</span></span> <span data-ttu-id="ef1cc-112">Niektóre przykłady w tym temacie wymagają pliku. edmx dla modelu Northwind.</span><span class="sxs-lookup"><span data-stu-id="ef1cc-112">Some examples in this topic require the .edmx file for the Northwind model.</span></span> <span data-ttu-id="ef1cc-113">Aby uzyskać więcej informacji, zobacz [plik. edmx — Omówienie](/previous-versions/dotnet/netframework-4.0/cc982042(v=vs.100)).</span><span class="sxs-lookup"><span data-stu-id="ef1cc-113">For more information, see [.edmx File Overview](/previous-versions/dotnet/netframework-4.0/cc982042(v=vs.100)).</span></span>

### <a name="to-generate-c-classes-that-support-data-binding"></a><span data-ttu-id="ef1cc-114">Aby wygenerować klasy języka C# obsługujące powiązanie danych</span><span class="sxs-lookup"><span data-stu-id="ef1cc-114">To generate C# classes that support data binding</span></span>

- <span data-ttu-id="ef1cc-115">W wierszu polecenia wykonaj następujące polecenie bez podziałów wierszy:</span><span class="sxs-lookup"><span data-stu-id="ef1cc-115">At the command prompt, execute the following command without line breaks:</span></span>

    ```console
    "%windir%\Microsoft.NET\Framework\v3.5\DataSvcUtil.exe" /dataservicecollection /version:2.0 /language:CSharp /out:Northwind.cs /uri:http://localhost:12345/Northwind.svc
    ```

    > [!NOTE]
    > <span data-ttu-id="ef1cc-116">Należy zastąpić wartość dostarczoną do `/uri:` parametru identyfikatorem URI wystąpienia przykładowej usługi danych Northwind.</span><span class="sxs-lookup"><span data-stu-id="ef1cc-116">You must replace the value supplied to the `/uri:` parameter with the URI of your instance of the Northwind sample data service.</span></span>

### <a name="to-generate-visual-basic-classes-that-support-data-binding"></a><span data-ttu-id="ef1cc-117">Aby wygenerować klasy Visual Basic obsługujące powiązanie danych</span><span class="sxs-lookup"><span data-stu-id="ef1cc-117">To generate Visual Basic classes that support data binding</span></span>

- <span data-ttu-id="ef1cc-118">W wierszu polecenia wykonaj następujące polecenie bez podziałów wierszy:</span><span class="sxs-lookup"><span data-stu-id="ef1cc-118">At the command prompt, execute the following command without line breaks:</span></span>

    ```console
    "%windir%\Microsoft.NET\Framework\v3.5\DataSvcUtil.exe" /dataservicecollection /version:2.0 /language:VB /out:Northwind.vb /uri:http://localhost:12345/Northwind.svc
    ```

    > [!NOTE]
    > <span data-ttu-id="ef1cc-119">Należy zastąpić wartość dostarczoną do `/uri:` parametru identyfikatorem URI wystąpienia przykładowej usługi danych Northwind.</span><span class="sxs-lookup"><span data-stu-id="ef1cc-119">You must replace value supplied to the `/uri:` parameter with the URI of your instance of the Northwind sample data service.</span></span>

### <a name="to-generate-c-classes-based-on-the-service-uri"></a><span data-ttu-id="ef1cc-120">Aby wygenerować klasy C# na podstawie identyfikatora URI usługi</span><span class="sxs-lookup"><span data-stu-id="ef1cc-120">To generate C# classes based on the service URI</span></span>

- <span data-ttu-id="ef1cc-121">W wierszu polecenia wykonaj następujące polecenie bez podziałów wierszy:</span><span class="sxs-lookup"><span data-stu-id="ef1cc-121">At the command prompt, execute the following command without line breaks:</span></span>

    ```console
    "%windir%\Microsoft.NET\Framework\v3.5\DataSvcUtil.exe" /language:CSharp /out:northwind.cs /uri:http://localhost:12345/Northwind.svc
    ```

    > [!NOTE]
    > <span data-ttu-id="ef1cc-122">Należy zastąpić wartość dostarczoną do `/uri:` parametru identyfikatorem URI wystąpienia przykładowej usługi danych Northwind.</span><span class="sxs-lookup"><span data-stu-id="ef1cc-122">You must replace the value supplied to the `/uri:` parameter with the URI of your instance of the Northwind sample data service.</span></span>

### <a name="to-generate-visual-basic-classes-based-on-the-service-uri"></a><span data-ttu-id="ef1cc-123">Aby wygenerować klasy Visual Basic na podstawie identyfikatora URI usługi</span><span class="sxs-lookup"><span data-stu-id="ef1cc-123">To generate Visual Basic classes based on the service URI</span></span>

- <span data-ttu-id="ef1cc-124">W wierszu polecenia wykonaj następujące polecenie bez podziałów wierszy:</span><span class="sxs-lookup"><span data-stu-id="ef1cc-124">At the command prompt, execute the following command without line breaks:</span></span>

    ```console
    "%windir%\Microsoft.NET\Framework\v3.5\datasvcutil.exe" /language:VB /out:Northwind.vb /uri:http://localhost:12345/Northwind.svc
    ```

    > [!NOTE]
    > <span data-ttu-id="ef1cc-125">Należy zastąpić wartość dostarczoną do `/uri:` parametru identyfikatorem URI wystąpienia przykładowej usługi danych Northwind.</span><span class="sxs-lookup"><span data-stu-id="ef1cc-125">You must replace value supplied to the `/uri:` parameter with the URI of your instance of the Northwind sample data service.</span></span>

### <a name="to-generate-c-classes-based-on-the-conceptual-model-file-csdl"></a><span data-ttu-id="ef1cc-126">Aby wygenerować klasy C# na podstawie pliku modelu koncepcyjnego (CSDL)</span><span class="sxs-lookup"><span data-stu-id="ef1cc-126">To generate C# classes based on the conceptual model file (CSDL)</span></span>

- <span data-ttu-id="ef1cc-127">W wierszu polecenia wykonaj następujące polecenie bez podziałów wierszy:</span><span class="sxs-lookup"><span data-stu-id="ef1cc-127">At the command prompt, execute the following command without line breaks:</span></span>

    ```console
    "%windir%\Microsoft.NET\Framework\v3.5\datasvcutil.exe" /language:CSharp /in:Northwind.csdl /out:Northwind.cs
    ```

### <a name="to-generate-visual-basic-classes-based-on-the-conceptual-model-file-csdl"></a><span data-ttu-id="ef1cc-128">Aby wygenerować klasy Visual Basic na podstawie pliku modelu koncepcyjnego (CSDL)</span><span class="sxs-lookup"><span data-stu-id="ef1cc-128">To generate Visual Basic classes based on the conceptual model file (CSDL)</span></span>

- <span data-ttu-id="ef1cc-129">W wierszu polecenia wykonaj następujące polecenie bez podziałów wierszy:</span><span class="sxs-lookup"><span data-stu-id="ef1cc-129">At the command prompt, execute the following command without line breaks:</span></span>

    ```console
    "%windir%\Microsoft.NET\Framework\v3.5\datasvcutil.exe" /language:VB /in:Northwind.csdl /out:Northwind.vb
    ```

### <a name="to-generate-c-classes-based-on-the-edmx-file"></a><span data-ttu-id="ef1cc-130">Aby wygenerować klasy C# na podstawie pliku. edmx</span><span class="sxs-lookup"><span data-stu-id="ef1cc-130">To generate C# classes based on the .edmx file</span></span>

- <span data-ttu-id="ef1cc-131">W wierszu polecenia wykonaj następujące polecenie bez podziałów wierszy:</span><span class="sxs-lookup"><span data-stu-id="ef1cc-131">At the command prompt, execute the following command without line breaks:</span></span>

    ```console
    "%windir%\Microsoft.NET\Framework\v3.5\datasvcutil.exe" /language:CSharp /in:Northwind.edmx /out:c:\northwind.cs
    ```

### <a name="to-generate-visual-basic-classes-based-on-the-edmx-file"></a><span data-ttu-id="ef1cc-132">Aby wygenerować klasy Visual Basic na podstawie pliku. edmx</span><span class="sxs-lookup"><span data-stu-id="ef1cc-132">To generate Visual Basic classes based on the .edmx file</span></span>

- <span data-ttu-id="ef1cc-133">W wierszu polecenia wykonaj następujące polecenie bez podziałów wierszy:</span><span class="sxs-lookup"><span data-stu-id="ef1cc-133">At the command prompt, execute the following command without line breaks:</span></span>

    ```console
    "%windir%\Microsoft.NET\Framework\v3.5\datasvcutil.exe" /language:VB /in:Northwind.edmx /out:c:\northwind.vb
    ```

## <a name="see-also"></a><span data-ttu-id="ef1cc-134">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="ef1cc-134">See also</span></span>

- [<span data-ttu-id="ef1cc-135">Generowanie biblioteki klienta usługi danych</span><span class="sxs-lookup"><span data-stu-id="ef1cc-135">Generating the Data Service Client Library</span></span>](generating-the-data-service-client-library-wcf-data-services.md)
- [<span data-ttu-id="ef1cc-136">Instrukcje: Dodawanie odwołania do usługi danych</span><span class="sxs-lookup"><span data-stu-id="ef1cc-136">How to: Add a Data Service Reference</span></span>](how-to-add-a-data-service-reference-wcf-data-services.md)
- [<span data-ttu-id="ef1cc-137">Narzędzie klienta usługi danych WCF (DataSvcUtil.exe)</span><span class="sxs-lookup"><span data-stu-id="ef1cc-137">WCF Data Service Client Utility (DataSvcUtil.exe)</span></span>](wcf-data-service-client-utility-datasvcutil-exe.md)
