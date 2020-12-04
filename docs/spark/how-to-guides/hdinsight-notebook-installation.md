---
title: Zainstaluj platformę .NET dla Apache Spark w notesach Jupyter w klastrach Azure HDInsight Spark
description: Dowiedz się, jak zainstalować platformę .NET dla Apache Spark w notesach Jupyter usługi Azure HDInsight.
ms.date: 10/09/2020
ms.topic: conceptual
ms.custom: mvc,how-to
ms.openlocfilehash: ff6b3a64c01fb9148d3abe3d04579233d11a4f73
ms.sourcegitcommit: 9d525bb8109216ca1dc9e39c149d4902f4b43da5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2020
ms.locfileid: "96599658"
---
# <a name="install-net-for-apache-spark-on-jupyter-notebooks-on-azure-hdinsight-spark-clusters"></a><span data-ttu-id="72260-103">Zainstaluj platformę .NET dla Apache Spark w notesach Jupyter w klastrach Azure HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="72260-103">Install .NET for Apache Spark on Jupyter Notebooks on Azure HDInsight Spark clusters</span></span>

<span data-ttu-id="72260-104">W tym artykule przedstawiono sposób instalowania programu .NET for Apache Spark w notesach Jupyter w klastrach Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="72260-104">This article teaches you how to install .NET for Apache Spark on Jupyter Notebooks on Azure HDInsight Spark clusters.</span></span> <span data-ttu-id="72260-105">Platformę .NET dla Apache Spark w klastrach usługi Azure HDInsight można wdrożyć za pomocą kombinacji wiersza polecenia i Azure Portal (Aby uzyskać więcej informacji, zobacz artykuł [jak wdrożyć aplikację .net for Apache Spark w usłudze Azure HDInsight](../tutorials/hdinsight-deployment.md)), ale notesy zapewniają bardziej interaktywną i iteracyjną pracę.</span><span class="sxs-lookup"><span data-stu-id="72260-105">You can deploy .NET for Apache Spark on Azure HDInsight clusters through a combination of the command line and the Azure portal (for more information, see [how to deploy a .NET for Apache Spark application to Azure HDInsight](../tutorials/hdinsight-deployment.md)), but notebooks provide a more interactive and iterative experience.</span></span>

<span data-ttu-id="72260-106">Klastry usługi Azure HDInsight są już dołączone do notesów Jupyter, więc wystarczy skonfigurować notesy Jupyter do uruchamiania programu .NET dla Apache Spark.</span><span class="sxs-lookup"><span data-stu-id="72260-106">Azure HDInsight clusters already come with Jupyter Notebooks, so all you have to do is configure the Jupyter Notebooks to run .NET for Apache Spark.</span></span> <span data-ttu-id="72260-107">Aby można było używać platformy .NET do Apache Spark w notesach Jupyter, w języku c# REPL jest potrzebny do wykonania kodu w języku C# i zachowania stanu wykonywania w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="72260-107">To use .NET for Apache Spark in your Jupyter Notebooks, a C# REPL is needed to execute your C# code line-by-line and to preserve execution state when necessary.</span></span> <span data-ttu-id="72260-108">[Wypróbuj platformę .NET](https://github.com/dotnet/try) jako oficjalną REPL .NET.</span><span class="sxs-lookup"><span data-stu-id="72260-108">[Try .NET](https://github.com/dotnet/try) has been integrated as the official .NET REPL.</span></span>

<span data-ttu-id="72260-109">Aby włączyć platformę .NET dla Apache Spark za pomocą środowiska Jupyter notesy, należy wykonać kilka ręcznych czynności za pomocą [Ambari](/azure/hdinsight/hdinsight-hadoop-manage-ambari) i przesłać [Akcje skryptu](/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux) w klastrze usługi HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="72260-109">To enable .NET for Apache Spark through the Jupyter Notebooks experience, you need to follow a few manual steps through [Ambari](/azure/hdinsight/hdinsight-hadoop-manage-ambari) and submit [script actions](/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux) on the HDInsight Spark cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="72260-110">Ta funkcja jest *eksperymentalna* i nie jest obsługiwana przez zespół usługi HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="72260-110">This feature is *experimental* and is not supported by the HDInsight Spark team.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72260-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="72260-111">Prerequisites</span></span>

<span data-ttu-id="72260-112">Jeśli jeszcze tego nie masz, Utwórz klaster [Azure HDInsight Spark](/azure/hdinsight/spark/apache-spark-jupyter-spark-sql-use-portal#create-an-apache-spark-cluster-in-hdinsight) .</span><span class="sxs-lookup"><span data-stu-id="72260-112">If you don't already have one, create an [Azure HDInsight Spark](/azure/hdinsight/spark/apache-spark-jupyter-spark-sql-use-portal#create-an-apache-spark-cluster-in-hdinsight) cluster.</span></span>

1. <span data-ttu-id="72260-113">Odwiedź [Azure Portal](https://portal.azure.com) i wybierz pozycję **+ Utwórz zasób**.</span><span class="sxs-lookup"><span data-stu-id="72260-113">Visit the [Azure portal](https://portal.azure.com) and select **+ Create a Resource**.</span></span>

1. <span data-ttu-id="72260-114">Utwórz nowy zasób klastra usługi Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="72260-114">Create a new Azure HDInsight cluster resource.</span></span> <span data-ttu-id="72260-115">Wybierz pozycję **Spark 2,4** i **HDI 4,0** podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="72260-115">Select **Spark 2.4** and **HDI 4.0** during cluster creation.</span></span>

## <a name="install-net-for-apache-spark"></a><span data-ttu-id="72260-116">Zainstaluj platformę .NET dla Apache Spark</span><span class="sxs-lookup"><span data-stu-id="72260-116">Install .NET for Apache Spark</span></span>

<span data-ttu-id="72260-117">W Azure Portal wybierz **klaster HDInsight Spark** utworzony w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="72260-117">In the Azure portal, select the **HDInsight Spark cluster** you created in the previous step.</span></span>

### <a name="stop-the-livy-server"></a><span data-ttu-id="72260-118">Zatrzymaj serwer usługi Livy</span><span class="sxs-lookup"><span data-stu-id="72260-118">Stop the Livy server</span></span>

1. <span data-ttu-id="72260-119">W portalu wybierz pozycję **Przegląd**, a następnie wybierz pozycję **Strona główna Ambari**.</span><span class="sxs-lookup"><span data-stu-id="72260-119">From the portal, select **Overview**, and then select **Ambari home**.</span></span> <span data-ttu-id="72260-120">Jeśli zostanie wyświetlony monit, wprowadź poświadczenia logowania dla klastra.</span><span class="sxs-lookup"><span data-stu-id="72260-120">If prompted, enter the login credentials for the cluster.</span></span>

   ![Zatrzymaj serwer usługi Livy](./media/hdinsight-notebook-installation/select-ambari.png)

2. <span data-ttu-id="72260-122">Wybierz pozycję **Spark2** w menu nawigacji po lewej stronie, a następnie wybierz pozycję **usługi LIVY dla Spark2 Server**.</span><span class="sxs-lookup"><span data-stu-id="72260-122">Select **Spark2** from the left navigation menu, and select **LIVY FOR SPARK2 SERVER**.</span></span>

   ![Zatrzymaj serwer usługi Livy](./media/hdinsight-notebook-installation/select-livyserver.png)

3. <span data-ttu-id="72260-124">Wybierz **hn0... Host**.</span><span class="sxs-lookup"><span data-stu-id="72260-124">Select **hn0... host**.</span></span>

   ![Zatrzymaj serwer usługi Livy](./media/hdinsight-notebook-installation/select-host.png)

4. <span data-ttu-id="72260-126">Wybierz wielokropek obok pozycji **usługi Livy dla serwera Spark2** i wybierz pozycję **Zatrzymaj**.</span><span class="sxs-lookup"><span data-stu-id="72260-126">Select the ellipsis next to **Livy for Spark2 Server** and select **Stop**.</span></span> <span data-ttu-id="72260-127">Po wyświetleniu monitu wybierz pozycję **OK** , aby wykonać operację.</span><span class="sxs-lookup"><span data-stu-id="72260-127">When prompted, select **OK** to proceed.</span></span>

   <span data-ttu-id="72260-128">Zatrzymaj usługi Livy dla serwera Spark2.</span><span class="sxs-lookup"><span data-stu-id="72260-128">Stop Livy for Spark2 Server.</span></span>
   <span data-ttu-id="72260-129">![Zatrzymaj serwer usługi Livy](./media/hdinsight-notebook-installation/stop-server.png)</span><span class="sxs-lookup"><span data-stu-id="72260-129">![Stop Livy Server](./media/hdinsight-notebook-installation/stop-server.png)</span></span>

5. <span data-ttu-id="72260-130">Powtórz poprzednie kroki dla **hn1... Host**.</span><span class="sxs-lookup"><span data-stu-id="72260-130">Repeat the previous steps for **hn1... host**.</span></span>

### <a name="submit-an-hdinsight-script-action"></a><span data-ttu-id="72260-131">Prześlij akcję skryptu usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="72260-131">Submit an HDInsight script action</span></span>

1. <span data-ttu-id="72260-132">`install-interactive-notebook.sh`To skrypt instalujący platformę .NET dla Apache Spark i wprowadza zmiany w oprogramowaniu Apache usługi Livy i sparkmagic.</span><span class="sxs-lookup"><span data-stu-id="72260-132">The `install-interactive-notebook.sh` is a script that installs .NET for Apache Spark and makes changes to Apache Livy and sparkmagic.</span></span> <span data-ttu-id="72260-133">Przed przesłaniem akcji skryptu do usługi HDInsight należy utworzyć i przekazać `install-interactive-notebook.sh` .</span><span class="sxs-lookup"><span data-stu-id="72260-133">Before you submit a script action to HDInsight, you need to create and upload `install-interactive-notebook.sh`.</span></span>

   <span data-ttu-id="72260-134">Utwórz nowy plik o nazwie **Install-Interactive-Notebook.sh** na komputerze lokalnym i wklej zawartość [Install-Interactive-Notebook.sh zawartości](https://raw.githubusercontent.com/dotnet/spark/master/deployment/HDI-Spark/Notebooks/install-interactive-notebook.sh).</span><span class="sxs-lookup"><span data-stu-id="72260-134">Create a new file named **install-interactive-notebook.sh** in your local computer and paste the contents of [install-interactive-notebook.sh contents](https://raw.githubusercontent.com/dotnet/spark/master/deployment/HDI-Spark/Notebooks/install-interactive-notebook.sh).</span></span>

   <span data-ttu-id="72260-135">Przekaż skrypt do [identyfikatora URI](/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#understand-script-actions) , który jest dostępny z klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="72260-135">Upload the script to a [URI](/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#understand-script-actions) that's accessible from the HDInsight cluster.</span></span> <span data-ttu-id="72260-136">Na przykład `https://<my storage account>.blob.core.windows.net/<my container>/<some dir>/install-interactive-notebook.sh`.</span><span class="sxs-lookup"><span data-stu-id="72260-136">For example, `https://<my storage account>.blob.core.windows.net/<my container>/<some dir>/install-interactive-notebook.sh`.</span></span>

2. <span data-ttu-id="72260-137">Uruchom `install-interactive-notebook.sh` w klastrze przy użyciu [akcji skryptu HDInsight](/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="72260-137">Run `install-interactive-notebook.sh` on the cluster using [HDInsight Script Actions](/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>

   <span data-ttu-id="72260-138">Wróć do klastra HDI w Azure Portal i wybierz pozycję **Akcje skryptu** z opcji po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="72260-138">Return to your HDI cluster in the Azure portal, and select **Script actions** from the options on the left.</span></span> <span data-ttu-id="72260-139">Przesyłasz jedną akcję skryptu do wdrożenia platformy .NET dla Apache Spark REPL w klastrze usługi HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="72260-139">You submit one script action to deploy the .NET for Apache Spark REPL on your HDInsight Spark cluster.</span></span> <span data-ttu-id="72260-140">Użyj następujących ustawień:</span><span class="sxs-lookup"><span data-stu-id="72260-140">Use the following settings:</span></span>

   |<span data-ttu-id="72260-141">Właściwość</span><span class="sxs-lookup"><span data-stu-id="72260-141">Property</span></span>  |<span data-ttu-id="72260-142">Opis</span><span class="sxs-lookup"><span data-stu-id="72260-142">Description</span></span>  |
   |---------|---------|
   | <span data-ttu-id="72260-143">Typ skryptu</span><span class="sxs-lookup"><span data-stu-id="72260-143">Script type</span></span> | <span data-ttu-id="72260-144">Niestandardowy</span><span class="sxs-lookup"><span data-stu-id="72260-144">Custom</span></span> |
   | <span data-ttu-id="72260-145">Nazwa</span><span class="sxs-lookup"><span data-stu-id="72260-145">Name</span></span> | <span data-ttu-id="72260-146">*Zainstaluj program .NET dla Apache Spark interaktywnego środowiska notesu*</span><span class="sxs-lookup"><span data-stu-id="72260-146">*Install .NET for Apache Spark Interactive Notebook Experience*</span></span> |
   | <span data-ttu-id="72260-147">Identyfikator URI skryptu bash</span><span class="sxs-lookup"><span data-stu-id="72260-147">Bash script URI</span></span> | <span data-ttu-id="72260-148">Identyfikator URI, do którego został przekazany `install-interactive-notebook.sh` .</span><span class="sxs-lookup"><span data-stu-id="72260-148">The URI to which you uploaded `install-interactive-notebook.sh`.</span></span> |
   | <span data-ttu-id="72260-149">Typy węzłów</span><span class="sxs-lookup"><span data-stu-id="72260-149">Node type(s)</span></span>| <span data-ttu-id="72260-150">Kierownik i proces roboczy</span><span class="sxs-lookup"><span data-stu-id="72260-150">Head and Worker</span></span> |
   | <span data-ttu-id="72260-151">Parametry</span><span class="sxs-lookup"><span data-stu-id="72260-151">Parameters</span></span> | <span data-ttu-id="72260-152">Wersja platformy .NET dla Apache Spark.</span><span class="sxs-lookup"><span data-stu-id="72260-152">.NET for Apache Spark version.</span></span> <span data-ttu-id="72260-153">Możesz sprawdzić, czy program [.net ma Apache Spark wydania](https://github.com/dotnet/spark/releases).</span><span class="sxs-lookup"><span data-stu-id="72260-153">You can check [.NET for Apache Spark releases](https://github.com/dotnet/spark/releases).</span></span> <span data-ttu-id="72260-154">Na przykład jeśli chcesz zainstalować program Sparkdotnet w wersji 1.0.0, może to być `1.0.0` .</span><span class="sxs-lookup"><span data-stu-id="72260-154">For example, if you want to install Sparkdotnet version 1.0.0 then it would be `1.0.0`.</span></span>

   <span data-ttu-id="72260-155">Przejdź do następnego kroku, gdy zielony znacznik wyboru pojawia się obok stanu akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="72260-155">Move to the next step when green checkmarks appear next to the status of the script action.</span></span>

### <a name="start-the-livy-server"></a><span data-ttu-id="72260-156">Uruchom serwer usługi Livy</span><span class="sxs-lookup"><span data-stu-id="72260-156">Start the Livy server</span></span>

<span data-ttu-id="72260-157">Postępuj zgodnie z instrukcjami w sekcji [Zatrzymaj usługi Livy Server](#stop-the-livy-server) , aby **uruchomić** (zamiast **zatrzymać**) usługi Livy for Spark2 Server for hosts **hn0** and **hn1**.</span><span class="sxs-lookup"><span data-stu-id="72260-157">Follow the instructions in the [Stop Livy server](#stop-the-livy-server) section to **Start** (rather than **Stop**) the Livy for Spark2 Server for hosts **hn0** and **hn1**.</span></span>

### <a name="set-up-spark-default-configurations"></a><span data-ttu-id="72260-158">Konfigurowanie domyślnych konfiguracji platformy Spark</span><span class="sxs-lookup"><span data-stu-id="72260-158">Set up Spark default configurations</span></span>

1. <span data-ttu-id="72260-159">W portalu wybierz pozycję **Przegląd**, a następnie wybierz pozycję **Strona główna Ambari**.</span><span class="sxs-lookup"><span data-stu-id="72260-159">From the portal, select **Overview**, and then select **Ambari home**.</span></span> <span data-ttu-id="72260-160">Jeśli zostanie wyświetlony monit, wprowadź poświadczenia logowania dla klastra.</span><span class="sxs-lookup"><span data-stu-id="72260-160">If prompted, enter the cluster login credentials for the cluster.</span></span>

2. <span data-ttu-id="72260-161">Wybierz pozycję **Spark2** i **configs**.</span><span class="sxs-lookup"><span data-stu-id="72260-161">Select **Spark2** and **CONFIGS**.</span></span> <span data-ttu-id="72260-162">Następnie wybierz pozycję **niestandardowe spark2 — ustawienia domyślne**.</span><span class="sxs-lookup"><span data-stu-id="72260-162">Then, select **Custom spark2-defaults**.</span></span>

   ![Ustawienia konfiguracji](./media/hdinsight-notebook-installation/spark-configs.png)

3. <span data-ttu-id="72260-164">Wybierz pozycję **Dodaj właściwość...** , aby dodać domyślne ustawienia platformy Spark.</span><span class="sxs-lookup"><span data-stu-id="72260-164">Select **Add Property...** to add Spark default settings.</span></span>

   ![Dodaj właściwość](./media/hdinsight-notebook-installation/add-property.png)

   <span data-ttu-id="72260-166">Istnieją trzy poszczególne właściwości.</span><span class="sxs-lookup"><span data-stu-id="72260-166">There are three individual properties.</span></span> <span data-ttu-id="72260-167">Dodaj je pojedynczo przy użyciu typu właściwości **Text** w trybie dodawania pojedynczej właściwości.</span><span class="sxs-lookup"><span data-stu-id="72260-167">Add them one at a time using the **TEXT** property type in Single property add mode.</span></span> <span data-ttu-id="72260-168">Sprawdź, czy nie masz żadnych dodatkowych spacji przed ani po żadnym z kluczy/wartości.</span><span class="sxs-lookup"><span data-stu-id="72260-168">Check that you don't have any extra spaces before or after any of the keys/values.</span></span>

   * <span data-ttu-id="72260-169">**Właściwość 1**</span><span class="sxs-lookup"><span data-stu-id="72260-169">**Property 1**</span></span>
       * <span data-ttu-id="72260-170">Głównych&ensp;&ensp;`spark.dotnet.shell.command`</span><span class="sxs-lookup"><span data-stu-id="72260-170">Key:&ensp;&ensp;`spark.dotnet.shell.command`</span></span>
       * <span data-ttu-id="72260-171">Wartość: `/usr/share/dotnet-tools/dotnet-try,kernel-server,--default-kernel,csharp`</span><span class="sxs-lookup"><span data-stu-id="72260-171">Value: `/usr/share/dotnet-tools/dotnet-try,kernel-server,--default-kernel,csharp`</span></span>

   * <span data-ttu-id="72260-172">**Właściwość 2** Użyj wersji platformy .NET dla Apache Spark, która została uwzględniona w poprzedniej akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="72260-172">**Property 2** Use the version of .NET for Apache Spark which you had included in the previous script action.</span></span>
       * <span data-ttu-id="72260-173">Głównych&ensp;&ensp;`spark.dotnet.packages`</span><span class="sxs-lookup"><span data-stu-id="72260-173">Key:&ensp;&ensp;`spark.dotnet.packages`</span></span>
       * <span data-ttu-id="72260-174">Wartość: `["nuget: Microsoft.Spark, 1.0.0", "nuget: Microsoft.Spark.Extensions.Delta, 1.0.0"]`</span><span class="sxs-lookup"><span data-stu-id="72260-174">Value: `["nuget: Microsoft.Spark, 1.0.0", "nuget: Microsoft.Spark.Extensions.Delta, 1.0.0"]`</span></span>

   * <span data-ttu-id="72260-175">**Właściwość 3**</span><span class="sxs-lookup"><span data-stu-id="72260-175">**Property 3**</span></span>
       * <span data-ttu-id="72260-176">Głównych&ensp;&ensp;`spark.dotnet.interpreter`</span><span class="sxs-lookup"><span data-stu-id="72260-176">Key:&ensp;&ensp;`spark.dotnet.interpreter`</span></span>
       * <span data-ttu-id="72260-177">Wartość: `try`</span><span class="sxs-lookup"><span data-stu-id="72260-177">Value: `try`</span></span>

   <span data-ttu-id="72260-178">Na przykład poniższy obraz przechwytuje ustawienie do dodawania właściwości 1:</span><span class="sxs-lookup"><span data-stu-id="72260-178">For example, the following image captures the setting for adding property 1:</span></span>

   ![Ustawienia konfiguracji](./media/hdinsight-notebook-installation/add-sparkconfig.png)

   <span data-ttu-id="72260-180">Po dodaniu trzech właściwości wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="72260-180">After adding the three properties, select **SAVE**.</span></span> <span data-ttu-id="72260-181">Jeśli widzisz ekran ostrzegawczy zaleceń dotyczących konfiguracji, wybierz pozycję **nadal mimo wszystko**.</span><span class="sxs-lookup"><span data-stu-id="72260-181">If you see a warning screen of config recommendations, select **PROCEED ANYWAY**.</span></span>

4. <span data-ttu-id="72260-182">Uruchom ponownie składniki, których to dotyczy.</span><span class="sxs-lookup"><span data-stu-id="72260-182">Restart affected components.</span></span>

   <span data-ttu-id="72260-183">Po dodaniu nowych właściwości należy ponownie uruchomić składniki, na które miały wpływ zmiany.</span><span class="sxs-lookup"><span data-stu-id="72260-183">After adding the new properties, you need to restart components that were affected by the changes.</span></span> <span data-ttu-id="72260-184">W górnej części wybierz pozycję **Uruchom ponownie**, a następnie **ponownie uruchom wszystkie** z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="72260-184">At the top, select **RESTART**, and then **Restart All Affected** from the drop-down.</span></span>

   ![Ustawienia konfiguracji](./media/hdinsight-notebook-installation/restart-affected.png)

   <span data-ttu-id="72260-186">Po wyświetleniu monitu wybierz pozycję **Potwierdź ponowne uruchomienie wszystkiego** , aby kontynuować, a następnie kliknij przycisk **OK** , aby zakończyć.</span><span class="sxs-lookup"><span data-stu-id="72260-186">When prompted, select **CONFIRM RESTART ALL** to continue, then click **OK** to finish.</span></span>

## <a name="submit-jobs-through-a-jupyter-notebook"></a><span data-ttu-id="72260-187">Przesyłanie zadań za pomocą Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="72260-187">Submit jobs through a Jupyter Notebook</span></span>

<span data-ttu-id="72260-188">Po zakończeniu poprzednich kroków można teraz przesyłać zadania platformy .NET dla Apache Spark za pomocą notesów Jupyter.</span><span class="sxs-lookup"><span data-stu-id="72260-188">After finishing the previous steps, you can now submit your .NET for Apache Spark jobs through Jupyter Notebooks.</span></span>

1. <span data-ttu-id="72260-189">Utwórz nowy Notes platformy .NET dla Apache Spark.</span><span class="sxs-lookup"><span data-stu-id="72260-189">Create a new .NET for Apache Spark notebook.</span></span> <span data-ttu-id="72260-190">W Azure Portal Uruchom Jupyter Notebook z klastra HDI.</span><span class="sxs-lookup"><span data-stu-id="72260-190">Launch a Jupyter Notebook from your HDI cluster in the Azure portal.</span></span>

   ![Jupyter Notebook uruchamiania](./media/hdinsight-notebook-installation/launch-notebook.png)

   <span data-ttu-id="72260-192">Następnie wybierz pozycję **Nowy**  >  **.NET Spark (C#)** , aby utworzyć Notes.</span><span class="sxs-lookup"><span data-stu-id="72260-192">Then, select **New** > **.NET Spark (C#)** to create a notebook.</span></span>

   ![Notes Jupyter](./media/hdinsight-notebook-installation/create-sparkdotnet-notebook.png)

2. <span data-ttu-id="72260-194">Przesyłanie zadań przy użyciu platformy .NET dla Apache Spark.</span><span class="sxs-lookup"><span data-stu-id="72260-194">Submit jobs using .NET for Apache Spark.</span></span>

   <span data-ttu-id="72260-195">Użyj poniższego fragmentu kodu, aby utworzyć ramkę danych:</span><span class="sxs-lookup"><span data-stu-id="72260-195">Use the following code snippet to create a DataFrame:</span></span>

   ```csharp
   var df = spark.Range(0,5);
   df.Show();
   ```

   ![Prześlij zadanie platformy Spark](./media/hdinsight-notebook-installation/create-df.png)

   <span data-ttu-id="72260-197">Poniższy fragment kodu służy do rejestrowania funkcji zdefiniowanej przez użytkownika (UDF) i używania UDF z ramkami danych:</span><span class="sxs-lookup"><span data-stu-id="72260-197">Use the following code snippet to register a user-defined function (UDF) and use the UDF with DataFrames:</span></span>

   ```csharp
   var myawesomeudf = Udf<int, string>((id) => $"hello {id}");
   df.Select(myawesomeudf(df["id"])).Show();
   ```

   ![Prześlij zadanie platformy Spark](./media/hdinsight-notebook-installation/run-udf.png)

## <a name="next-steps"></a><span data-ttu-id="72260-199">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="72260-199">Next steps</span></span>

* [<span data-ttu-id="72260-200">Wdrażanie aplikacji platformy .NET dla Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="72260-200">Deploy a .NET for Apache Spark application to Azure HDInsight</span></span>](../tutorials/hdinsight-deployment.md)
* [<span data-ttu-id="72260-201">Dokumentacja usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="72260-201">HDInsight Documentation</span></span>](/azure/hdinsight/)
