---
title: Wdrażanie aplikacji platformy .NET dla Apache Spark w kostkach
description: Dowiedz się, jak wdrożyć aplikację platformy .NET dla Apache Spark w usłudze datakostki.
ms.date: 06/25/2020
ms.topic: tutorial
ms.custom: mvc
ms.openlocfilehash: 66a5493f0084f5fa86c3eb928d2e4a4b4999e764
ms.sourcegitcommit: 40de8df14289e1e05b40d6e5c1daabd3c286d70c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/22/2020
ms.locfileid: "86924594"
---
# <a name="tutorial-deploy-a-net-for-apache-spark-application-to-databricks"></a><span data-ttu-id="228c5-103">Samouczek: wdrażanie aplikacji .NET dla Apache Spark w kostkach</span><span class="sxs-lookup"><span data-stu-id="228c5-103">Tutorial: Deploy a .NET for Apache Spark application to Databricks</span></span>

<span data-ttu-id="228c5-104">W tym samouczku przedstawiono sposób wdrażania aplikacji w chmurze za pośrednictwem Azure Databricks, opartej na Apache Sparkj platformie analitycznej z instalacją jednym kliknięciem, usprawnionych przepływów pracy i interaktywnego obszaru roboczego, który umożliwia współpracę.</span><span class="sxs-lookup"><span data-stu-id="228c5-104">This tutorial teaches you how to deploy your app to the cloud through Azure Databricks, an Apache Spark-based analytics platform with one-click setup, streamlined workflows, and interactive workspace that enables collaboration.</span></span>

<span data-ttu-id="228c5-105">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="228c5-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
>
> - <span data-ttu-id="228c5-106">Tworzenie obszaru roboczego usługi Azure Databricks.</span><span class="sxs-lookup"><span data-stu-id="228c5-106">Create an Azure Databricks workspace.</span></span>
> - <span data-ttu-id="228c5-107">Opublikuj aplikację .NET dla Apache Spark.</span><span class="sxs-lookup"><span data-stu-id="228c5-107">Publish your .NET for Apache Spark app.</span></span>
> - <span data-ttu-id="228c5-108">Utwórz zadanie platformy Spark i klaster Spark.</span><span class="sxs-lookup"><span data-stu-id="228c5-108">Create a Spark job and Spark cluster.</span></span>
> - <span data-ttu-id="228c5-109">Uruchom aplikację w klastrze Spark.</span><span class="sxs-lookup"><span data-stu-id="228c5-109">Run your app on the Spark cluster.</span></span>

[!INCLUDE [spark-preview-note](../../../includes/spark-preview-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="228c5-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="228c5-110">Prerequisites</span></span>

<span data-ttu-id="228c5-111">Przed rozpoczęciem wykonaj następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="228c5-111">Before you start, do the following tasks:</span></span>

* <span data-ttu-id="228c5-112">Jeśli nie masz konta platformy Azure, Utwórz [bezpłatne konto](https://azure.microsoft.com/free/dotnet/).</span><span class="sxs-lookup"><span data-stu-id="228c5-112">If you don't have an Azure account, create a [free account](https://azure.microsoft.com/free/dotnet/).</span></span>
* <span data-ttu-id="228c5-113">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="228c5-113">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
* <span data-ttu-id="228c5-114">Ukończ [platformę .NET dla Apache Spark — Rozpocznij pracę w 10-minutowym](https://dotnet.microsoft.com/learn/data/spark-tutorial/intro) samouczku.</span><span class="sxs-lookup"><span data-stu-id="228c5-114">Complete the [.NET for Apache Spark - Get Started in 10-Minutes](https://dotnet.microsoft.com/learn/data/spark-tutorial/intro) tutorial.</span></span>

## <a name="create-an-azure-databricks-workspace"></a><span data-ttu-id="228c5-115">Tworzenie obszaru roboczego usługi Azure Databricks</span><span class="sxs-lookup"><span data-stu-id="228c5-115">Create an Azure Databricks workspace</span></span>

> [!Note]
> <span data-ttu-id="228c5-116">Tego samouczka nie można przeprowadzić za pomocą **subskrypcji bezpłatnej wersji próbnej platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="228c5-116">This tutorial cannot be carried out using **Azure Free Trial Subscription**.</span></span>
> <span data-ttu-id="228c5-117">Jeśli masz bezpłatne konto, przejdź do swojego profilu i Zmień subskrypcję na **płatność zgodnie z rzeczywistym**użyciem.</span><span class="sxs-lookup"><span data-stu-id="228c5-117">If you have a free account, go to your profile and change your subscription to **pay-as-you-go**.</span></span> <span data-ttu-id="228c5-118">Aby uzyskać więcej informacji, zobacz [Bezpłatne konto platformy Azure](https://azure.microsoft.com/free/dotnet/).</span><span class="sxs-lookup"><span data-stu-id="228c5-118">For more information, see [Azure free account](https://azure.microsoft.com/free/dotnet/).</span></span> <span data-ttu-id="228c5-119">Następnie [Usuń limit wydatków](https://docs.microsoft.com/azure/billing/billing-spending-limit#why-you-might-want-to-remove-the-spending-limit)i [Poproś o zwiększenie limitu przydziału](https://docs.microsoft.com/azure/azure-supportability/resource-manager-core-quotas-request) dla procesorów wirtualnych vCPU w Twoim regionie.</span><span class="sxs-lookup"><span data-stu-id="228c5-119">Then, [remove the spending limit](https://docs.microsoft.com/azure/billing/billing-spending-limit#why-you-might-want-to-remove-the-spending-limit), and [request a quota increase](https://docs.microsoft.com/azure/azure-supportability/resource-manager-core-quotas-request) for vCPUs in your region.</span></span> <span data-ttu-id="228c5-120">Podczas tworzenia obszaru roboczego Azure Databricks możesz wybrać warstwę cenową **wersji próbnej (Premium-14-Days Free dBu)** , aby umożliwić dostęp do obszaru roboczego bezpłatnie Azure Databricks DBU przez 14 dni.</span><span class="sxs-lookup"><span data-stu-id="228c5-120">When you create your Azure Databricks workspace, you can select the **Trial (Premium - 14-Days Free DBUs)** pricing tier to give the workspace access to free Premium Azure Databricks DBUs for 14 days.</span></span>

<span data-ttu-id="228c5-121">W tej sekcji utworzysz obszar roboczy usługi Azure Databricks przy użyciu witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="228c5-121">In this section, you create an Azure Databricks workspace using the Azure portal.</span></span>

1. <span data-ttu-id="228c5-122">W Azure Portal wybierz pozycję **Utwórz**  >  **Analytics**  >  **Azure Databricks**analizy zasobów.</span><span class="sxs-lookup"><span data-stu-id="228c5-122">In the Azure portal, select **Create a resource** > **Analytics** > **Azure Databricks**.</span></span>

   ![Tworzenie zasobu Azure Databricks w Azure Portal](./media/databricks-deployment/create-databricks-resource.png)

2. <span data-ttu-id="228c5-124">W obszarze **Usługa Azure Databricks** podaj wartości umożliwiające utworzenie obszaru roboczego usługi Databricks.</span><span class="sxs-lookup"><span data-stu-id="228c5-124">Under **Azure Databricks Service**, provide the values to create a Databricks workspace.</span></span>

    |<span data-ttu-id="228c5-125">Właściwość</span><span class="sxs-lookup"><span data-stu-id="228c5-125">Property</span></span>  |<span data-ttu-id="228c5-126">Opis</span><span class="sxs-lookup"><span data-stu-id="228c5-126">Description</span></span>  |
    |---------|---------|
    |<span data-ttu-id="228c5-127">**Nazwa obszaru roboczego**</span><span class="sxs-lookup"><span data-stu-id="228c5-127">**Workspace name**</span></span>     | <span data-ttu-id="228c5-128">Podaj nazwę obszaru roboczego usługi Databricks.</span><span class="sxs-lookup"><span data-stu-id="228c5-128">Provide a name for your Databricks workspace.</span></span>        |
    |<span data-ttu-id="228c5-129">**Subskrypcja**</span><span class="sxs-lookup"><span data-stu-id="228c5-129">**Subscription**</span></span>     | <span data-ttu-id="228c5-130">Z listy rozwijanej wybierz subskrypcję platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="228c5-130">From the drop-down, select your Azure subscription.</span></span>        |
    |<span data-ttu-id="228c5-131">**Grupa zasobów**</span><span class="sxs-lookup"><span data-stu-id="228c5-131">**Resource group**</span></span>     | <span data-ttu-id="228c5-132">Określ, czy chcesz utworzyć nową grupę zasobów, czy użyć istniejącej grupy.</span><span class="sxs-lookup"><span data-stu-id="228c5-132">Specify whether you want to create a new resource group or use an existing one.</span></span> <span data-ttu-id="228c5-133">Grupa zasobów to kontener zawierający powiązane zasoby dla rozwiązania platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="228c5-133">A resource group is a container that holds related resources for an Azure solution.</span></span> <span data-ttu-id="228c5-134">Aby uzyskać więcej informacji, zobacz [Omówienie usługi Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span><span class="sxs-lookup"><span data-stu-id="228c5-134">For more information, see [Azure Resource Group overview](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span></span> |
    |<span data-ttu-id="228c5-135">**Lokalizacja**</span><span class="sxs-lookup"><span data-stu-id="228c5-135">**Location**</span></span>     | <span data-ttu-id="228c5-136">Wybierz preferowany region.</span><span class="sxs-lookup"><span data-stu-id="228c5-136">Select your preferred region.</span></span> <span data-ttu-id="228c5-137">Aby uzyskać informacje na temat dostępnych regionów, zobacz [usługi platformy Azure dostępne według regionów](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="228c5-137">For information about available regions, see [Azure services available by region](https://azure.microsoft.com/regions/services/).</span></span>        |
    |<span data-ttu-id="228c5-138">**Warstwa cenowa**</span><span class="sxs-lookup"><span data-stu-id="228c5-138">**Pricing Tier**</span></span>     |  <span data-ttu-id="228c5-139">Wybierz warstwę **standardowa**, **Premium**lub **wersja próbna**.</span><span class="sxs-lookup"><span data-stu-id="228c5-139">Choose between **Standard**, **Premium**, or **Trial**.</span></span> <span data-ttu-id="228c5-140">Aby uzyskać więcej informacji o tych warstwach, zobacz [stronę usługi Databricks](https://azure.microsoft.com/pricing/details/databricks/).</span><span class="sxs-lookup"><span data-stu-id="228c5-140">For more information on these tiers, see [Databricks pricing page](https://azure.microsoft.com/pricing/details/databricks/).</span></span>       |
    |<span data-ttu-id="228c5-141">**Virtual Network**</span><span class="sxs-lookup"><span data-stu-id="228c5-141">**Virtual Network**</span></span>     |   <span data-ttu-id="228c5-142">Nie</span><span class="sxs-lookup"><span data-stu-id="228c5-142">No</span></span>       |

3. <span data-ttu-id="228c5-143">Wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="228c5-143">Select **Create**.</span></span> <span data-ttu-id="228c5-144">Tworzenie obszaru roboczego trwa kilka minut.</span><span class="sxs-lookup"><span data-stu-id="228c5-144">The workspace creation takes a few minutes.</span></span> <span data-ttu-id="228c5-145">Podczas tworzenia obszaru roboczego można wyświetlić stan wdrożenia w obszarze **powiadomienia**.</span><span class="sxs-lookup"><span data-stu-id="228c5-145">During workspace creation, you can view the deployment status in **Notifications**.</span></span>

## <a name="install-azure-databricks-tools"></a><span data-ttu-id="228c5-146">Zainstaluj narzędzia Azure Databricks</span><span class="sxs-lookup"><span data-stu-id="228c5-146">Install Azure Databricks tools</span></span>

<span data-ttu-id="228c5-147">Korzystając z **interfejsu wiersza polecenia datacegłs** , można nawiązać połączenie z klastrami Azure Databricks i przekazywać do nich pliki z komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="228c5-147">You can use the **Databricks CLI** to connect to Azure Databricks clusters and upload files to them from your local machine.</span></span> <span data-ttu-id="228c5-148">Klastry datacegły uzyskują dostęp do plików za poorednictwem DBFS (system plików).</span><span class="sxs-lookup"><span data-stu-id="228c5-148">Databricks clusters access files through DBFS (Databricks File System).</span></span>

1. <span data-ttu-id="228c5-149">Interfejs wiersza polecenia datakostki wymaga języka Python 3,6 lub nowszego.</span><span class="sxs-lookup"><span data-stu-id="228c5-149">The Databricks CLI requires Python 3.6 or above.</span></span> <span data-ttu-id="228c5-150">Jeśli masz już zainstalowany język Python, możesz pominąć ten krok.</span><span class="sxs-lookup"><span data-stu-id="228c5-150">If you already have Python installed, you can skip this step.</span></span>

   <span data-ttu-id="228c5-151">**Dla systemu Windows:**</span><span class="sxs-lookup"><span data-stu-id="228c5-151">**For Windows:**</span></span>

   [<span data-ttu-id="228c5-152">Pobierz Język Python dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="228c5-152">Download Python for Windows</span></span>](https://www.python.org/ftp/python/3.7.4/python-3.7.4.exe)

   <span data-ttu-id="228c5-153">**Dla systemu Linux:** Środowisko Python jest preinstalowane na większości dystrybucji systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="228c5-153">**For Linux:** Python comes preinstalled on most Linux distributions.</span></span> <span data-ttu-id="228c5-154">Uruchom następujące polecenie, aby sprawdzić, która wersja została zainstalowana:</span><span class="sxs-lookup"><span data-stu-id="228c5-154">Run the following command to see which version you have installed:</span></span>

   ```bash
   python3 --version
   ```

2. <span data-ttu-id="228c5-155">Użyj narzędzia PIP, aby zainstalować interfejs wiersza polecenia datakosteks.</span><span class="sxs-lookup"><span data-stu-id="228c5-155">Use pip to install the Databricks CLI.</span></span> <span data-ttu-id="228c5-156">Środowisko Python 3,4 i nowsze zawierają domyślnie funkcję PIP.</span><span class="sxs-lookup"><span data-stu-id="228c5-156">Python 3.4 and later include pip by default.</span></span> <span data-ttu-id="228c5-157">Użyj PIP3 dla języka Python 3.</span><span class="sxs-lookup"><span data-stu-id="228c5-157">Use pip3 for Python 3.</span></span> <span data-ttu-id="228c5-158">Uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="228c5-158">Run the following command:</span></span>

   ```bash
   pip3 install databricks-cli
   ```

3. <span data-ttu-id="228c5-159">Po zainstalowaniu interfejsu wiersza polecenia datakostki Otwórz nowy wiersz poleceń i uruchom polecenie `databricks` .</span><span class="sxs-lookup"><span data-stu-id="228c5-159">Once you've installed the Databricks CLI, open a new command prompt and run the command `databricks`.</span></span> <span data-ttu-id="228c5-160">Jeśli zostanie wyświetlony komunikat " **" nie jest rozpoznawany jako błąd wewnętrzny lub zewnętrzny**, upewnij się, że otwarto nowy wiersz polecenia.</span><span class="sxs-lookup"><span data-stu-id="228c5-160">If you receive a **'databricks' is not recognized as an internal or external command error**, make sure you opened a new command prompt.</span></span>

## <a name="set-up-azure-databricks"></a><span data-ttu-id="228c5-161">Skonfiguruj Azure Databricks</span><span class="sxs-lookup"><span data-stu-id="228c5-161">Set up Azure Databricks</span></span>

<span data-ttu-id="228c5-162">Teraz, gdy masz zainstalowany interfejs wiersza polecenia datakosteks, musisz skonfigurować szczegóły uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="228c5-162">Now that you have the Databricks CLI installed, you need to set up authentication details.</span></span>

1. <span data-ttu-id="228c5-163">Uruchom polecenie CLI w interfejsie wiersza polecenia `databricks configure --token` .</span><span class="sxs-lookup"><span data-stu-id="228c5-163">Run the Databricks CLI command `databricks configure --token`.</span></span>

2. <span data-ttu-id="228c5-164">Po uruchomieniu polecenia Konfiguruj zostanie wyświetlony monit o wprowadzenie hosta.</span><span class="sxs-lookup"><span data-stu-id="228c5-164">After running the configure command, you are prompted to enter a host.</span></span> <span data-ttu-id="228c5-165">Adres URL hosta używa formatu: `https://<Location>.azuredatabricks.net` .</span><span class="sxs-lookup"><span data-stu-id="228c5-165">Your host URL uses the format: `https://<Location>.azuredatabricks.net`.</span></span> <span data-ttu-id="228c5-166">Na przykład jeśli podczas tworzenia usługi Azure Databricks wybrano opcję **eastus2** , host będzie miał wartość `https://eastus2.azuredatabricks.net` .</span><span class="sxs-lookup"><span data-stu-id="228c5-166">For instance, if you selected **eastus2** during Azure Databricks Service creation, the host would be `https://eastus2.azuredatabricks.net`.</span></span>

3. <span data-ttu-id="228c5-167">Po wprowadzeniu hosta zostanie wyświetlony monit o wprowadzenie tokenu.</span><span class="sxs-lookup"><span data-stu-id="228c5-167">After entering your host, you are prompted to enter a token.</span></span> <span data-ttu-id="228c5-168">W Azure Portal wybierz pozycję **Uruchom obszar roboczy** , aby uruchomić Azure Databricks obszar roboczy.</span><span class="sxs-lookup"><span data-stu-id="228c5-168">In the Azure portal, select **Launch Workspace** to launch your Azure Databricks workspace.</span></span>

   ![Uruchom Azure Databricks obszar roboczy](./media/databricks-deployment/launch-databricks-workspace.png)

4. <span data-ttu-id="228c5-170">Na stronie głównej obszaru roboczego wybierz pozycję **Ustawienia użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="228c5-170">On the home page of your workspace, select **User Settings**.</span></span>

   ![Ustawienia użytkownika w obszarze roboczym Azure Databricks](./media/databricks-deployment/databricks-user-settings.png)

5. <span data-ttu-id="228c5-172">Na stronie Ustawienia użytkownika można wygenerować nowy token.</span><span class="sxs-lookup"><span data-stu-id="228c5-172">On the User Settings page, you can generate a new token.</span></span> <span data-ttu-id="228c5-173">Skopiuj wygenerowany token i wklej go z powrotem do wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="228c5-173">Copy the generated token and paste it back into your command prompt.</span></span>

   ![Generuj nowy token dostępu w obszarze roboczym Azure Databricks](./media/databricks-deployment/generate-token.png)

<span data-ttu-id="228c5-175">Teraz powinno być możliwe uzyskanie dostępu do dowolnych klastrów Azure Databricks tworzenia i przekazywania plików do DBFS.</span><span class="sxs-lookup"><span data-stu-id="228c5-175">You should now be able to access any Azure Databricks clusters you create and upload files to the DBFS.</span></span>

## <a name="download-worker-dependencies"></a><span data-ttu-id="228c5-176">Pobierz zależności procesów roboczych</span><span class="sxs-lookup"><span data-stu-id="228c5-176">Download worker dependencies</span></span>

1. <span data-ttu-id="228c5-177">Aplikacja Microsoft. Spark. Worker ułatwia Apache Spark wykonywanie aplikacji, na przykład dowolnych funkcji zdefiniowanych przez użytkownika (UDF).</span><span class="sxs-lookup"><span data-stu-id="228c5-177">Microsoft.Spark.Worker helps Apache Spark execute your app, such as any user-defined functions (UDFs) you may have written.</span></span> <span data-ttu-id="228c5-178">Pobierz [pakiet Microsoft. Spark. Worker](https://github.com/dotnet/spark/releases/download/v0.6.0/Microsoft.Spark.Worker.netcoreapp2.1.linux-x64-0.6.0.tar.gz).</span><span class="sxs-lookup"><span data-stu-id="228c5-178">Download [Microsoft.Spark.Worker](https://github.com/dotnet/spark/releases/download/v0.6.0/Microsoft.Spark.Worker.netcoreapp2.1.linux-x64-0.6.0.tar.gz).</span></span>

2. <span data-ttu-id="228c5-179">*Install-Worker.sh* to skrypt, który umożliwia skopiowanie programu .net dla Apache Spark plików zależnych do węzłów klastra.</span><span class="sxs-lookup"><span data-stu-id="228c5-179">The *install-worker.sh* is a script that lets you copy .NET for Apache Spark dependent files into the nodes of your cluster.</span></span>

   <span data-ttu-id="228c5-180">Utwórz nowy plik o nazwie **Install-Worker.sh** na komputerze lokalnym i wklej [zawartość Install-Worker.sh](https://raw.githubusercontent.com/dotnet/spark/master/deployment/install-worker.sh) znajdującą się w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="228c5-180">Create a new file named **install-worker.sh** on your local computer, and paste the [install-worker.sh contents](https://raw.githubusercontent.com/dotnet/spark/master/deployment/install-worker.sh) located on GitHub.</span></span>

3. <span data-ttu-id="228c5-181">*DB-init.sh* to skrypt służący do instalowania zależności w klastrze danych platformy Spark.</span><span class="sxs-lookup"><span data-stu-id="228c5-181">The *db-init.sh* is a script that installs dependencies onto your Databricks Spark cluster.</span></span>

   <span data-ttu-id="228c5-182">Utwórz nowy plik o nazwie **DB-init.sh** na komputerze lokalnym i wklej [zawartość DB-init.sh](https://github.com/dotnet/spark/blob/master/deployment/db-init.sh) znajdującą się w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="228c5-182">Create a new file named **db-init.sh** on your local computer, and paste the [db-init.sh contents](https://github.com/dotnet/spark/blob/master/deployment/db-init.sh) located on GitHub.</span></span>

   <span data-ttu-id="228c5-183">W właśnie utworzonym pliku Ustaw `DOTNET_SPARK_RELEASE` zmienną na `https://github.com/dotnet/spark/releases/download/v0.6.0/Microsoft.Spark.Worker.netcoreapp2.1.linux-x64-0.6.0.tar.gz` .</span><span class="sxs-lookup"><span data-stu-id="228c5-183">In the file you just created, set the `DOTNET_SPARK_RELEASE` variable to `https://github.com/dotnet/spark/releases/download/v0.6.0/Microsoft.Spark.Worker.netcoreapp2.1.linux-x64-0.6.0.tar.gz`.</span></span> <span data-ttu-id="228c5-184">Pozostaw resztę pliku *DB-init.sh* .</span><span class="sxs-lookup"><span data-stu-id="228c5-184">Leave the rest of the *db-init.sh* file as-is.</span></span>

> [!Note]
> <span data-ttu-id="228c5-185">Jeśli używasz systemu Windows, upewnij się, że końce wiersza w skryptach *Install-Worker.sh* i *DB-init.sh* są w stylu systemu UNIX (LF).</span><span class="sxs-lookup"><span data-stu-id="228c5-185">If you are using Windows, verify that the line-endings in your *install-worker.sh* and *db-init.sh* scripts are Unix-style (LF).</span></span> <span data-ttu-id="228c5-186">Końce wierszy można zmienić za pomocą edytorów tekstu, takich jak Notatnik + + i Atom.</span><span class="sxs-lookup"><span data-stu-id="228c5-186">You can change line endings through text editors like Notepad++ and Atom.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="228c5-187">Publikowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="228c5-187">Publish your app</span></span>

<span data-ttu-id="228c5-188">Następnie opublikujesz *mySparkApp* utworzoną w programie [.net for Apache Spark — Rozpocznij w 10-minutowym](https://dotnet.microsoft.com/learn/data/spark-tutorial/intro) samouczku, aby zapewnić, że klaster Spark ma dostęp do wszystkich plików potrzebnych do uruchomienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="228c5-188">Next, you publish the *mySparkApp* created in the [.NET for Apache Spark - Get Started in 10-Minutes](https://dotnet.microsoft.com/learn/data/spark-tutorial/intro) tutorial to ensure your Spark cluster has access to all the files it needs to run your app.</span></span>

1. <span data-ttu-id="228c5-189">Uruchom następujące polecenia, aby opublikować *mySparkApp*:</span><span class="sxs-lookup"><span data-stu-id="228c5-189">Run the following commands to publish the *mySparkApp*:</span></span>

   ```dotnetcli
   cd mySparkApp
   dotnet publish -c Release -f netcoreapp3.1 -r ubuntu.16.04-x64
   ```

2. <span data-ttu-id="228c5-190">Wykonaj następujące zadania w celu przesłania plików opublikowanych aplikacji, aby można je było łatwo przekazać do klastra Spark.</span><span class="sxs-lookup"><span data-stu-id="228c5-190">Do the following tasks to zip your published app files so that you can easily upload them to your Databricks Spark cluster.</span></span>

   <span data-ttu-id="228c5-191">**W systemie Windows:**</span><span class="sxs-lookup"><span data-stu-id="228c5-191">**On Windows:**</span></span>

   <span data-ttu-id="228c5-192">Przejdź do mySparkApp/bin/Release/netcoreapp 3.1/Ubuntu. 16.04-x64.</span><span class="sxs-lookup"><span data-stu-id="228c5-192">Navigate to mySparkApp/bin/Release/netcoreapp3.1/ubuntu.16.04-x64.</span></span> <span data-ttu-id="228c5-193">Następnie kliknij prawym przyciskiem myszy folder **Publikowanie** i wybierz polecenie **Wyślij do > folder skompresowany (zip)**.</span><span class="sxs-lookup"><span data-stu-id="228c5-193">Then, right-click on **Publish** folder and select **Send to > Compressed (zipped) folder**.</span></span> <span data-ttu-id="228c5-194">Nadaj nazwę nowemu folderowi **publish.zip**.</span><span class="sxs-lookup"><span data-stu-id="228c5-194">Name the new folder **publish.zip**.</span></span>

   <span data-ttu-id="228c5-195">**W systemie Linux Uruchom następujące polecenie:**</span><span class="sxs-lookup"><span data-stu-id="228c5-195">**On Linux, run the following command:**</span></span>

   ```bash
   zip -r publish.zip .
   ```

## <a name="upload-files"></a><span data-ttu-id="228c5-196">Przekazywanie plików</span><span class="sxs-lookup"><span data-stu-id="228c5-196">Upload files</span></span>

<span data-ttu-id="228c5-197">W tej sekcji przekazano kilka plików do DBFS, aby klaster miał wszystko, czego potrzebuje do uruchomienia aplikacji w chmurze.</span><span class="sxs-lookup"><span data-stu-id="228c5-197">In this section, you upload several files to DBFS so that your cluster has everything it needs to run your app in the cloud.</span></span> <span data-ttu-id="228c5-198">Za każdym razem, gdy przekażesz plik do DBFS, upewnij się, że znajduje się w katalogu, w którym znajduje się ten plik na komputerze.</span><span class="sxs-lookup"><span data-stu-id="228c5-198">Each time you upload a file to the DBFS, make sure you are in the directory where that file is located on your computer.</span></span>

1. <span data-ttu-id="228c5-199">Uruchom następujące polecenia, aby przekazać *DB-init.sh*, *Install-Worker.sh*i *Microsoft. Spark. Worker* do DBFS:</span><span class="sxs-lookup"><span data-stu-id="228c5-199">Run the following commands to upload the *db-init.sh*, *install-worker.sh*, and *Microsoft.Spark.Worker* to DBFS:</span></span>

   ```console
   databricks fs cp db-init.sh dbfs:/spark-dotnet/db-init.sh
   databricks fs cp install-worker.sh dbfs:/spark-dotnet/install-worker.sh
   databricks fs cp Microsoft.Spark.Worker.netcoreapp3.1.linux-x64-0.6.0.tar.gz dbfs:/spark-dotnet/Microsoft.Spark.Worker.netcoreapp2.1.linux-x64-0.6.0.tar.gz
   ```

2. <span data-ttu-id="228c5-200">Uruchom następujące polecenia, aby przekazać pozostałe pliki, do których klaster będzie musiał uruchomić aplikację: spakowanego folderu publikowania, *input.txt*i *Microsoft-Spark-2.4. x-0.3.1. jar*.</span><span class="sxs-lookup"><span data-stu-id="228c5-200">Run the following commands to upload the remaining files your cluster will need to run your app: the zipped publish folder, *input.txt*, and *microsoft-spark-2.4.x-0.3.1.jar*.</span></span>

   ```console
   cd mySparkApp
   databricks fs cp input.txt dbfs:/input.txt

   cd mySparkApp\bin\Release\netcoreapp3.1\ubuntu.16.04-x64 directory
   databricks fs cp publish.zip dbfs:/spark-dotnet/publish.zip
   databricks fs cp microsoft-spark-2.4.x-0.6.0.jar dbfs:/spark-dotnet/microsoft-spark-2.4.x-0.6.0.jar
   ```

## <a name="create-a-job"></a><span data-ttu-id="228c5-201">Tworzenie zadania</span><span class="sxs-lookup"><span data-stu-id="228c5-201">Create a job</span></span>

<span data-ttu-id="228c5-202">Aplikacja jest uruchamiana na Azure Databricks za pomocą zadania uruchamiającego żądanie uruchomienia platformy **Spark**, które jest poleceniem używanym do uruchamiania programu .net dla Apache Spark zadań.</span><span class="sxs-lookup"><span data-stu-id="228c5-202">Your app runs on Azure Databricks through a job that runs **spark-submit**, which is the command you use to run .NET for Apache Spark jobs.</span></span>

1. <span data-ttu-id="228c5-203">W obszarze roboczym Azure Databricks wybierz ikonę **zadania** , a następnie pozycję **+ Utwórz zadanie**.</span><span class="sxs-lookup"><span data-stu-id="228c5-203">In your Azure Databricks Workspace, select the **Jobs** icon and then **+ Create Job**.</span></span>

   ![Tworzenie zadania Azure Databricks](./media/databricks-deployment/create-job.png)

2. <span data-ttu-id="228c5-205">Wybierz tytuł zadania, a następnie wybierz pozycję Skonfiguruj platformę **Spark-Submit**.</span><span class="sxs-lookup"><span data-stu-id="228c5-205">Choose a title for your job, and then select **Configure spark-submit**.</span></span>

   ![Konfigurowanie usługi Spark-Submit dla zadań datakostek](./media/databricks-deployment/configure-spark-submit.png)

3. <span data-ttu-id="228c5-207">Wklej następujące parametry w konfiguracji zadania.</span><span class="sxs-lookup"><span data-stu-id="228c5-207">Paste the following parameters in the job configuration.</span></span> <span data-ttu-id="228c5-208">Następnie wybierz pozycję **Potwierdź**.</span><span class="sxs-lookup"><span data-stu-id="228c5-208">Then, select **Confirm**.</span></span>

   ```
   ["--class","org.apache.spark.deploy.dotnet.DotnetRunner","/dbfs/spark-dotnet/microsoft-spark-2.4.x-0.6.0.jar","/dbfs/spark-dotnet/publish.zip","mySparkApp"]
   ```

## <a name="create-a-cluster"></a><span data-ttu-id="228c5-209">Tworzenie klastra</span><span class="sxs-lookup"><span data-stu-id="228c5-209">Create a cluster</span></span>

1. <span data-ttu-id="228c5-210">Przejdź do zadania i wybierz pozycję **Edytuj** , aby skonfigurować klaster zadania.</span><span class="sxs-lookup"><span data-stu-id="228c5-210">Navigate to your job and select **Edit** to configure your job's cluster.</span></span>

2. <span data-ttu-id="228c5-211">Ustaw klaster na platformę **Spark 2.4.1**.</span><span class="sxs-lookup"><span data-stu-id="228c5-211">Set your cluster to **Spark 2.4.1**.</span></span> <span data-ttu-id="228c5-212">Następnie wybierz pozycję **Opcje zaawansowane**  >  **init skrypty**.</span><span class="sxs-lookup"><span data-stu-id="228c5-212">Then, select **Advanced Options** > **Init Scripts**.</span></span> <span data-ttu-id="228c5-213">Ustaw ścieżkę skryptu init jako `dbfs:/spark-dotnet/db-init.sh` .</span><span class="sxs-lookup"><span data-stu-id="228c5-213">Set Init Script Path as `dbfs:/spark-dotnet/db-init.sh`.</span></span>

   ![Skonfiguruj klaster Spark w Azure Databricks](./media/databricks-deployment/cluster-config.png)

3. <span data-ttu-id="228c5-215">Wybierz pozycję **Potwierdź** , aby potwierdzić ustawienia klastra.</span><span class="sxs-lookup"><span data-stu-id="228c5-215">Select **Confirm** to confirm your cluster settings.</span></span>

## <a name="run-your-app"></a><span data-ttu-id="228c5-216">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="228c5-216">Run your app</span></span>

1. <span data-ttu-id="228c5-217">Przejdź do zadania i wybierz pozycję **Uruchom teraz** , aby uruchomić zadanie w nowo skonfigurowanym klastrze Spark.</span><span class="sxs-lookup"><span data-stu-id="228c5-217">Navigate to your job and select **Run Now** to run your job on your newly configured Spark cluster.</span></span>

2. <span data-ttu-id="228c5-218">Utworzenie klastra zadania może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="228c5-218">It takes a few minutes for the job's cluster to create.</span></span> <span data-ttu-id="228c5-219">Po jego utworzeniu zadanie zostanie przesłane i będzie można wyświetlić dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="228c5-219">Once it is created, your job will be submitted, and you can view the output.</span></span>

3. <span data-ttu-id="228c5-220">Z menu po lewej stronie wybierz pozycję **klastry** , a następnie nazwę i uruchomienie zadania.</span><span class="sxs-lookup"><span data-stu-id="228c5-220">Select **Clusters** from the left menu, and then the name and run of your job.</span></span>

4. <span data-ttu-id="228c5-221">Wybierz pozycję **dzienniki sterowników** , aby wyświetlić dane wyjściowe zadania.</span><span class="sxs-lookup"><span data-stu-id="228c5-221">Select **Driver Logs** to view the output of your job.</span></span> <span data-ttu-id="228c5-222">Gdy aplikacja zakończy wykonywanie, zobaczysz tę samą tabelę Count wyrazów z uruchomienia lokalnego uruchamiania zapisaną w standardowej konsoli wyjściowej.</span><span class="sxs-lookup"><span data-stu-id="228c5-222">When your app finishes executing, you see the same word count table from the getting started local run written to the standard output console.</span></span>

   ![Azure Databricks tabeli wyjściowej zadania](./media/databricks-deployment/table-output.png)

   <span data-ttu-id="228c5-224">Gratulacje, uruchomiono pierwszą aplikację platformy .NET dla Apache Spark w chmurze!</span><span class="sxs-lookup"><span data-stu-id="228c5-224">Congratulations, you've run your first .NET for Apache Spark application in the cloud!</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="228c5-225">Czyszczenie zasobów</span><span class="sxs-lookup"><span data-stu-id="228c5-225">Clean up resources</span></span>

<span data-ttu-id="228c5-226">Jeśli obszar roboczy datakostki nie jest już potrzebny, możesz usunąć zasób Azure Databricks w Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="228c5-226">If you no longer need the Databricks workspace, you can delete your Azure Databricks resource in the Azure portal.</span></span> <span data-ttu-id="228c5-227">Dodatkowo możesz wybrać nazwę grupy zasobów, aby otworzyć stronę grupy zasobów, a następnie wybrać pozycję **Usuń grupę zasobów**.</span><span class="sxs-lookup"><span data-stu-id="228c5-227">You can also select the resource group name to open the resource group page, and then select **Delete resource group**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="228c5-228">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="228c5-228">Next steps</span></span>

<span data-ttu-id="228c5-229">W tym samouczku wdrożono aplikację .NET dla Apache Spark w usłudze datakostki.</span><span class="sxs-lookup"><span data-stu-id="228c5-229">In this tutorial, you deployed your .NET for Apache Spark application to Databricks.</span></span> <span data-ttu-id="228c5-230">Aby dowiedzieć się więcej na temat datakostki, przejdź do dokumentacji Azure Databricks.</span><span class="sxs-lookup"><span data-stu-id="228c5-230">To learn more about Databricks, continue to the Azure Databricks Documentation.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="228c5-231">Dokumentacja usługi Azure Databricks</span><span class="sxs-lookup"><span data-stu-id="228c5-231">Azure Databricks Documentation</span></span>](https://docs.microsoft.com/azure/azure-databricks/)
