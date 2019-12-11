---
title: Przesyłanie zadania platformy .NET dla Apache Spark do kostek
description: Dowiedz się, jak przesłać zadanie platformy .NET dla Apache Spark do datakostki przy użyciu platformy Spark — przesyłanie i Ustawianie jar.
ms.date: 12/05/2019
ms.topic: conceptual
ms.custom: mvc,how-to
ms.openlocfilehash: 9cd3d40871d4600660957ec268f192ef3e045845
ms.sourcegitcommit: a4f9b754059f0210e29ae0578363a27b9ba84b64
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2019
ms.locfileid: "74838352"
---
# <a name="submit-a-net-for-apache-spark-job-to-databricks"></a><span data-ttu-id="1e062-103">Przesyłanie zadania platformy .NET dla Apache Spark do kostek</span><span class="sxs-lookup"><span data-stu-id="1e062-103">Submit a .NET for Apache Spark job to Databricks</span></span>

<span data-ttu-id="1e062-104">Istnieją dwa sposoby wdrażania zadania programu .NET dla Apache Spark w kostkach danych: `spark-submit` i ustawienia jar.</span><span class="sxs-lookup"><span data-stu-id="1e062-104">There are two ways to deploy your .NET for Apache Spark job to Databricks: `spark-submit` and Set Jar.</span></span> 

## <a name="deploy-using-spark-submit"></a><span data-ttu-id="1e062-105">Wdrażanie przy użyciu platformy Spark — przesyłanie</span><span class="sxs-lookup"><span data-stu-id="1e062-105">Deploy using spark-submit</span></span>

<span data-ttu-id="1e062-106">Można użyć polecenia [Spark-Submit](https://spark.apache.org/docs/latest/submitting-applications.html) do przesyłania zadań programu .net dla Apache Spark do datakostki.</span><span class="sxs-lookup"><span data-stu-id="1e062-106">You can use the [spark-submit](https://spark.apache.org/docs/latest/submitting-applications.html) command to submit .NET for Apache Spark jobs to Databricks.</span></span> <span data-ttu-id="1e062-107">`spark-submit` umożliwia przesyłanie tylko do klastra, który tworzy na żądanie.</span><span class="sxs-lookup"><span data-stu-id="1e062-107">`spark-submit` allows submission only to a cluster that gets created on-demand.</span></span>

1. <span data-ttu-id="1e062-108">Przejdź do obszaru roboczego datakostki i Utwórz zadanie.</span><span class="sxs-lookup"><span data-stu-id="1e062-108">Navigate to your Databricks Workspace and create a job.</span></span> <span data-ttu-id="1e062-109">Wybierz tytuł zadania, a następnie wybierz pozycję Skonfiguruj platformę **Spark-Submit**.</span><span class="sxs-lookup"><span data-stu-id="1e062-109">Choose a title for your job, and then select **Configure spark-submit**.</span></span> <span data-ttu-id="1e062-110">Wklej następujące parametry w konfiguracji zadania, a następnie wybierz pozycję **Potwierdź**.</span><span class="sxs-lookup"><span data-stu-id="1e062-110">Paste the following parameters in the job configuration, then select **Confirm**.</span></span>

    ```
    ["--files","/dbfs/<path-to>/<app assembly/file to deploy to worker>","--class","org.apache.spark.deploy.dotnet.DotnetRunner","/dbfs/<path-to>/microsoft-spark-<spark_majorversion.spark_minorversion.x>-<spark_dotnet_version>.jar","/dbfs/<path-to>/<app name>.zip","<app bin name>","app arg1","app arg2"]
    ```

    > [!NOTE]
    > <span data-ttu-id="1e062-111">Zaktualizuj zawartość powyższego parametru w oparciu o określone pliki i konfigurację.</span><span class="sxs-lookup"><span data-stu-id="1e062-111">Update the contents of the above parameter based on your specific files and configuration.</span></span> <span data-ttu-id="1e062-112">Na przykład należy odwołać się do wersji pliku JAR Microsoft. Spark przekazanego do DBFS i użyć odpowiedniej nazwy aplikacji i pliku zip opublikowanej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1e062-112">For instance, reference the version of the Microsoft.Spark jar file that you uploaded to DBFS, and use the appropriate name of your app and published app zip file.</span></span>

2. <span data-ttu-id="1e062-113">Przejdź do zadania i wybierz pozycję **Edytuj** , aby skonfigurować klaster zadania.</span><span class="sxs-lookup"><span data-stu-id="1e062-113">Navigate to your job and select **Edit** to configure your job's cluster.</span></span> <span data-ttu-id="1e062-114">Ustaw wersję Databricks Runtime na podstawie wersji Apache Spark, która ma być używana we wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="1e062-114">Set the Databricks Runtime Version based on the version of Apache Spark you wish to use in your deployment.</span></span> <span data-ttu-id="1e062-115">Następnie wybierz **Opcje zaawansowane > init scripts**i Ustaw ścieżkę skryptu init jako `dbfs:/spark-dotnet/db-init.sh`.</span><span class="sxs-lookup"><span data-stu-id="1e062-115">Then select **Advanced Options > Init Scripts**, and set Init Script Path as `dbfs:/spark-dotnet/db-init.sh`.</span></span> <span data-ttu-id="1e062-116">Wybierz pozycję **Potwierdź** , aby potwierdzić ustawienia klastra.</span><span class="sxs-lookup"><span data-stu-id="1e062-116">Select **Confirm** to confirm your cluster settings.</span></span>

3. <span data-ttu-id="1e062-117">Przejdź do zadania i wybierz pozycję **Uruchom teraz** , aby uruchomić zadanie w nowo skonfigurowanym klastrze Spark.</span><span class="sxs-lookup"><span data-stu-id="1e062-117">Navigate to your job and select **Run Now** to run your job on your newly configured Spark cluster.</span></span> <span data-ttu-id="1e062-118">Utworzenie klastra zadania może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="1e062-118">It takes a few minutes for the job's cluster to be created.</span></span> <span data-ttu-id="1e062-119">Po jego utworzeniu zadanie zostanie przesłane.</span><span class="sxs-lookup"><span data-stu-id="1e062-119">Once it is created, your job will be submitted.</span></span> <span data-ttu-id="1e062-120">Możesz wyświetlić dane wyjściowe, wybierając pozycję **klastry** z menu po lewej stronie obszaru roboczego dane, a następnie wybierz polecenie **dzienniki sterowników**.</span><span class="sxs-lookup"><span data-stu-id="1e062-120">You can view the output by selecting **Clusters** from the left menu of your Databricks workspace, then select **Driver Logs**.</span></span>

## <a name="deploy-using-set-jar"></a><span data-ttu-id="1e062-121">Wdrażanie przy użyciu zestawu jar</span><span class="sxs-lookup"><span data-stu-id="1e062-121">Deploy using Set Jar</span></span>

<span data-ttu-id="1e062-122">Alternatywnie możesz użyć [Ustawienia jar](https://docs.microsoft.com/azure/databricks/jobs#--create-a-job) w obszarze roboczym datakosteks, aby przesłać środowisko .net dla Apache Spark zadań do kostek.</span><span class="sxs-lookup"><span data-stu-id="1e062-122">Alternatively, you can use [Set Jar](https://docs.microsoft.com/azure/databricks/jobs#--create-a-job) in your Databricks workspace to submit .NET for Apache Spark jobs to Databricks.</span></span> <span data-ttu-id="1e062-123">*Ustawienie jar* umożliwia przesyłanie zadań do istniejącego aktywnego klastra.</span><span class="sxs-lookup"><span data-stu-id="1e062-123">*Set Jar* allows job submission to an existing active cluster.</span></span>

### <a name="one-time-setup"></a><span data-ttu-id="1e062-124">Konfiguracja jednorazowa</span><span class="sxs-lookup"><span data-stu-id="1e062-124">One-time setup</span></span>

1. <span data-ttu-id="1e062-125">Przejdź do klastra datakosteks i wybierz pozycję **Jobs (zadania** ) z menu po lewej stronie, a następnie **Ustaw jar**.</span><span class="sxs-lookup"><span data-stu-id="1e062-125">Navigate to your Databricks cluster and select **Jobs** from the left-side menu, followed by **Set JAR**.</span></span>

2. <span data-ttu-id="1e062-126">Przekaż odpowiednie `microsoft-spark-<spark-version>-<spark-dotnet-version>.jar`.</span><span class="sxs-lookup"><span data-stu-id="1e062-126">Upload the appropriate `microsoft-spark-<spark-version>-<spark-dotnet-version>.jar`.</span></span>

3. <span data-ttu-id="1e062-127">Zmodyfikuj następujące parametry, aby uwzględnić poprawną nazwę pliku wykonywalnego, który został opublikowany zamiast `<your-app-name>`:</span><span class="sxs-lookup"><span data-stu-id="1e062-127">Modify the following parameters to include the correct name for the executable that you published in place of `<your-app-name>`:</span></span>

    ```
    Main Class: org.apache.spark.deploy.dotnet.DotnetRunner
    Arguments /dbfs/apps/<your-app-name>.zip <your-app-name>
    ```

4. <span data-ttu-id="1e062-128">Skonfiguruj klaster tak, aby wskazywał istniejący klaster, dla którego został już ustawiony skrypt init.</span><span class="sxs-lookup"><span data-stu-id="1e062-128">Configure the cluster to point to an existing cluster for which you have already set the init script.</span></span>

### <a name="publish-and-run-your-app"></a><span data-ttu-id="1e062-129">Publikowanie i uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="1e062-129">Publish and run your app</span></span>

1. <span data-ttu-id="1e062-130">Upewnij się, że aplikacja została opublikowana i że kod aplikacji nie używa `SparkSession.Stop()`.</span><span class="sxs-lookup"><span data-stu-id="1e062-130">Ensure you have published your app, and that your application code does not use `SparkSession.Stop()`.</span></span>

2. <span data-ttu-id="1e062-131">Użyj [interfejsu wiersza polecenia datakosteks](https://docs.microsoft.com/azure/databricks/dev-tools/databricks-cli) , aby przekazać aplikację do klastra datakostks.</span><span class="sxs-lookup"><span data-stu-id="1e062-131">Use [Databricks CLI](https://docs.microsoft.com/azure/databricks/dev-tools/databricks-cli) to upload your application to your Databricks cluster.</span></span> <span data-ttu-id="1e062-132">Na przykład użyj następującego polecenia, aby przekazać opublikowaną aplikację do klastra:</span><span class="sxs-lookup"><span data-stu-id="1e062-132">For example, use the following command to upload your published app to your cluster:</span></span>

    ```console
    cd <path-to-your-app-publish-directory>
    databricks fs cp <your-app-name>.zip dbfs:/apps/<your-app-name>.zip
    ```

3. <span data-ttu-id="1e062-133">Jeśli masz jakiekolwiek funkcje zdefiniowane przez użytkownika w aplikacji, zestawy aplikacji, takie jak biblioteki DLL, które zawierają funkcje zdefiniowane przez użytkownika wraz z ich zależnościami, muszą być umieszczone w katalogu roboczym każdego *Microsoft. Spark. Worker*.</span><span class="sxs-lookup"><span data-stu-id="1e062-133">If you have any user-defined functions in your app, the app assemblies, such as DLLs that contain user-defined functions along with their dependencies, need to be placed in the working directory of each *Microsoft.Spark.Worker*.</span></span>

    <span data-ttu-id="1e062-134">Przekaż zestawy aplikacji do klastra datakostki:</span><span class="sxs-lookup"><span data-stu-id="1e062-134">Upload your application assemblies to your Databricks cluster:</span></span>

    ```console
    cd <path-to-your-app-publish-directory>
    databricks fs cp <assembly>.dll dbfs:/apps/dependencies
    ```

    <span data-ttu-id="1e062-135">Usuń komentarz i Zmodyfikuj sekcję zależności aplikacji w [DB-init.sh](https://github.com/dotnet/spark/blob/master/deployment/db-init.sh) , aby wskazywała ścieżkę zależności aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1e062-135">Uncomment and modify the app dependencies section in [db-init.sh](https://github.com/dotnet/spark/blob/master/deployment/db-init.sh) to point to your app dependencies path.</span></span> <span data-ttu-id="1e062-136">Następnie Przekaż zaktualizowane *DB-init.sh* do klastra:</span><span class="sxs-lookup"><span data-stu-id="1e062-136">Then, upload the updated *db-init.sh* to your cluster:</span></span>

    ```console
    cd <path-to-db-init-and-install-worker>
    databricks fs cp db-init.sh dbfs:/spark-dotnet/db-init.sh
    ```

4. <span data-ttu-id="1e062-137">Przejdź do **klastra datakostks > zadania > [nazwa zadania] > Uruchom teraz** , aby uruchomić zadanie.</span><span class="sxs-lookup"><span data-stu-id="1e062-137">Navigate to **Databricks cluster > Jobs > [Job-name] > Run Now** to run your job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e062-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1e062-138">Next steps</span></span>

* [<span data-ttu-id="1e062-139">Wprowadzenie do platformy .NET dla Apache Spark</span><span class="sxs-lookup"><span data-stu-id="1e062-139">Get started with .NET for Apache Spark</span></span>](../tutorials/get-started.md)
* [<span data-ttu-id="1e062-140">Wdrażanie aplikacji platformy .NET dla Apache Spark w kostkach</span><span class="sxs-lookup"><span data-stu-id="1e062-140">Deploy a .NET for Apache Spark application to Databricks</span></span>](../tutorials/databricks-deployment.md)
* [<span data-ttu-id="1e062-141">Dokumentacja Azure Databricks</span><span class="sxs-lookup"><span data-stu-id="1e062-141">Azure Databricks Documentation</span></span>](https://docs.microsoft.com/azure/azure-databricks/)