---
title: Korzystanie z notesów Jupyter
titleSuffix: .NET for Apache Spark
description: Korzystanie z platformy .NET dla Apache Spark w środowiskach interaktywnych, takich jak Jupyter Notebook, Jupyter Lab lub Visual Studio Code (VS Code)
ms.author: luquinta
author: luisquintanilla
ms.date: 10/09/2020
ms.topic: conceptual
ms.custom: mvc, how-to
ms.openlocfilehash: cf19b4e4b7a7b9033fb97b2b2736ab0383c11f93
ms.sourcegitcommit: 9d525bb8109216ca1dc9e39c149d4902f4b43da5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2020
ms.locfileid: "96598936"
---
# <a name="use-net-for-apache-spark-in-jupyter-notebooks"></a><span data-ttu-id="eac90-103">Korzystanie z platformy .NET dla Apache Spark w notesach Jupyter</span><span class="sxs-lookup"><span data-stu-id="eac90-103">Use .NET for Apache Spark in Jupyter Notebooks</span></span>

<span data-ttu-id="eac90-104">W tym artykule dowiesz się, jak uruchomić program .NET dla zadań Apache Spark interaktywnie w Jupyter Notebook i Visual Studio Code (VS Code) przy użyciu programu .NET Interactive.</span><span class="sxs-lookup"><span data-stu-id="eac90-104">In this article, you learn how to run .NET for Apache Spark jobs interactively in Jupyter Notebook and Visual Studio Code (VS Code) with .NET Interactive.</span></span>

## <a name="about-jupyter"></a><span data-ttu-id="eac90-105">Informacje o Jupyter</span><span class="sxs-lookup"><span data-stu-id="eac90-105">About Jupyter</span></span>

<span data-ttu-id="eac90-106">[Jupyter](https://jupyter.org/) to środowisko obliczeniowe typu "open source", które zapewnia użytkownikom interaktywny prototyp i programowanie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eac90-106">[Jupyter](https://jupyter.org/) is an open-source, cross-platform computing environment that provides a way for users to prototype and develop applications interactively.</span></span> <span data-ttu-id="eac90-107">Można korzystać z Jupyter za pomocą wielu różnych interfejsów, takich jak Jupyter Notebook, Jupyter Lab i VS Code.</span><span class="sxs-lookup"><span data-stu-id="eac90-107">You can interact with Jupyter through a wide variety of interfaces such as Jupyter Notebook, Jupyter Lab, and VS Code.</span></span>

<span data-ttu-id="eac90-108">W kontekście platformy .NET, [.NET Interactive](https://github.com/dotnet/interactive), narzędzia globalne platformy .NET Core, zapewnia jądro do pisania kodu platformy .NET (C#/f #) w środowiskach interaktywnego przetwarzania, takich jak Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="eac90-108">In the context of .NET, [.NET Interactive](https://github.com/dotnet/interactive), a .NET Core global tool, provides a kernel for writing .NET code (C#/F#) in interactive computing environments such as Jupyter Notebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eac90-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="eac90-109">Prerequisites</span></span>

- [<span data-ttu-id="eac90-110">Zestaw SDK platformy .NET Core 3,1</span><span class="sxs-lookup"><span data-stu-id="eac90-110">.NET Core 3.1 SDK</span></span>](../../core/install/index.yml)
- [<span data-ttu-id="eac90-111">Apache Spark</span><span class="sxs-lookup"><span data-stu-id="eac90-111">Apache Spark</span></span>](https://spark.apache.org/downloads.html)
- [<span data-ttu-id="eac90-112">Apache Spark proces roboczy platformy .NET</span><span class="sxs-lookup"><span data-stu-id="eac90-112">Apache Spark .NET Worker</span></span>](https://github.com/dotnet/spark/releases)

<span data-ttu-id="eac90-113">Zobacz [samouczek wprowadzenie](../tutorials/get-started.md) , aby uzyskać więcej informacji na temat konfigurowania środowiska .net for Apache Spark.</span><span class="sxs-lookup"><span data-stu-id="eac90-113">See the [getting started tutorial](../tutorials/get-started.md) for more information on setting up your .NET for Apache Spark environment.</span></span>

## <a name="prepare-environment"></a><span data-ttu-id="eac90-114">Przygotowywanie środowiska</span><span class="sxs-lookup"><span data-stu-id="eac90-114">Prepare environment</span></span>

<span data-ttu-id="eac90-115">Aby pracować z notesami Jupyter, musisz mieć dwie rzeczy.</span><span class="sxs-lookup"><span data-stu-id="eac90-115">To work with Jupyter Notebooks, you'll need two things.</span></span>

1. <span data-ttu-id="eac90-116">Zainstaluj [interaktywne narzędzie .NET Interactive](https://github.com/dotnet/interactive/blob/main/docs/NotebooksLocalExperience.md)</span><span class="sxs-lookup"><span data-stu-id="eac90-116">Install the [.NET Interactive global .NET tool](https://github.com/dotnet/interactive/blob/main/docs/NotebooksLocalExperience.md)</span></span>
1. <span data-ttu-id="eac90-117">Pobierz `Microsoft.Spark` pakiet NuGet.</span><span class="sxs-lookup"><span data-stu-id="eac90-117">Download the `Microsoft.Spark` NuGet package.</span></span>
    1. <span data-ttu-id="eac90-118">Przejdź do strony pakietu NuGet [Microsoft. Spark](https://www.nuget.org/packages/Microsoft.Spark/) .</span><span class="sxs-lookup"><span data-stu-id="eac90-118">Navigate to the [Microsoft.Spark](https://www.nuget.org/packages/Microsoft.Spark/) NuGet package page.</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="eac90-119">Domyślnie pobierana jest Najnowsza wersja pakietu.</span><span class="sxs-lookup"><span data-stu-id="eac90-119">By default, the latest version of the package is downloaded.</span></span> <span data-ttu-id="eac90-120">**Upewnij się, że pobierana wersja jest taka sama jak Apache Spark roboczym programu .NET.**</span><span class="sxs-lookup"><span data-stu-id="eac90-120">**Make sure that the version you download is the same as your Apache Spark .NET Worker.**</span></span>

    1. <span data-ttu-id="eac90-121">W okienku **informacje** wybierz pozycję **Pobierz pakiet** , aby pobrać najnowszą wersję pakietu.</span><span class="sxs-lookup"><span data-stu-id="eac90-121">In the **Info** pane, select **Download package** to download the latest version of the package.</span></span> <span data-ttu-id="eac90-122">Nazwa pakietu jest podobna do  *Microsoft. Spark. [ Pakiet — wersja]. nupkg*.</span><span class="sxs-lookup"><span data-stu-id="eac90-122">The name of the package is similar to  *microsoft.spark.[PACKAGE-VERSION].nupkg*.</span></span>
    1. <span data-ttu-id="eac90-123">Rozpakuj pobrany pakiet.</span><span class="sxs-lookup"><span data-stu-id="eac90-123">Unzip the downloaded package.</span></span> <span data-ttu-id="eac90-124">Niespakowany katalog powinien zawierać podkatalog o nazwie *Jars*.</span><span class="sxs-lookup"><span data-stu-id="eac90-124">The unzipped directory should contain a subdirectory called *jars*.</span></span> <span data-ttu-id="eac90-125">Zanotuj ścieżkę, ponieważ jest ona używana w późniejszym czasie.</span><span class="sxs-lookup"><span data-stu-id="eac90-125">Take note of the path since it's used at a later time.</span></span>

## <a name="start-net-for-apache-spark"></a><span data-ttu-id="eac90-126">Uruchom platformę .NET dla Apache Spark</span><span class="sxs-lookup"><span data-stu-id="eac90-126">Start .NET for Apache Spark</span></span>

<span data-ttu-id="eac90-127">Uruchom następujące polecenie, aby uruchomić platformę .NET dla Apache Spark w trybie debugowania.</span><span class="sxs-lookup"><span data-stu-id="eac90-127">Run the following command to start .NET for Apache Spark in debug mode.</span></span> <span data-ttu-id="eac90-128">To `spark-submit` polecenie uruchamia proces i czeka na połączenia z [SparkSession](xref:Microsoft.Spark.Sql.SparkSession).</span><span class="sxs-lookup"><span data-stu-id="eac90-128">This `spark-submit` command starts a process and waits for connections from a [SparkSession](xref:Microsoft.Spark.Sql.SparkSession).</span></span> <span data-ttu-id="eac90-129">Upewnij się, że ścieżka do `microsoft-spark-<spark_majorversion-spark_minorversion>_<scala_majorversion.scala_minorversion>-<spark_dotnet_version>.jar` odpowiedniej wersji platformy .NET dla Apache Spark jest używana.</span><span class="sxs-lookup"><span data-stu-id="eac90-129">Make sure to provide the path to the `microsoft-spark-<spark_majorversion-spark_minorversion>_<scala_majorversion.scala_minorversion>-<spark_dotnet_version>.jar` for the respective version of .NET for Apache Spark you're using.</span></span>

<span data-ttu-id="eac90-130">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="eac90-130">**Ubuntu**</span></span>

```bash
spark-submit \
    --class org.apache.spark.deploy.dotnet.DotnetRunner \
    --master local \
    <path-to-microsoft-spark-jar> \
    debug
```

<span data-ttu-id="eac90-131">**Windows**</span><span class="sxs-lookup"><span data-stu-id="eac90-131">**Windows**</span></span>

```cmd
spark-submit ^
    --class org.apache.spark.deploy.dotnet.DotnetRunner ^
    --master local ^
    <path-to-microsoft-spark-jar> ^
    debug
```

## <a name="create-a-notebook"></a><span data-ttu-id="eac90-132">Tworzenie notesu</span><span class="sxs-lookup"><span data-stu-id="eac90-132">Create a notebook</span></span>

<span data-ttu-id="eac90-133">Można użyć różnych interfejsów do współpracy z Jupyter.</span><span class="sxs-lookup"><span data-stu-id="eac90-133">You can use different interfaces to interact with Jupyter.</span></span> <span data-ttu-id="eac90-134">W przypadku interfejsu opartego na przeglądarce należy używać notesów Jupyter lub laboratorium Jupyter.</span><span class="sxs-lookup"><span data-stu-id="eac90-134">For a browser-based interface, use Jupyter Notebooks or Jupyter Lab.</span></span> <span data-ttu-id="eac90-135">W przypadku środowiska lokalnego edytora Użyj VS Code.</span><span class="sxs-lookup"><span data-stu-id="eac90-135">For a local editor experience, use VS Code.</span></span>

### <a name="jupyter-notebooks--jupyter-lab"></a><span data-ttu-id="eac90-136">Jupyter notesy & Jupyter Lab</span><span class="sxs-lookup"><span data-stu-id="eac90-136">Jupyter Notebooks & Jupyter Lab</span></span>

1. <span data-ttu-id="eac90-137">W innym wierszu polecenia Uruchom Jupyter Notebook lub Jupyter Lab przy użyciu jednego z poniższych poleceń:</span><span class="sxs-lookup"><span data-stu-id="eac90-137">In another command prompt, start Jupyter Notebook or Jupyter Lab using one of the commands below:</span></span>

    <span data-ttu-id="eac90-138">**Jupyter Notebook**</span><span class="sxs-lookup"><span data-stu-id="eac90-138">**Jupyter Notebook**</span></span>

    ```bash
    jupyter notebook
    ```

    <span data-ttu-id="eac90-139">**Jupyter Lab**</span><span class="sxs-lookup"><span data-stu-id="eac90-139">**Jupyter Lab**</span></span>

    ```bash
    jupyter lab
    ```

    <span data-ttu-id="eac90-140">Te polecenia powodują uruchomienie okna przeglądarki z interfejsem laboratorium Jupyter Notebook lub Jupyter.</span><span class="sxs-lookup"><span data-stu-id="eac90-140">These commands launch a browser window with the Jupyter Notebook or Jupyter Lab interface.</span></span>

1. <span data-ttu-id="eac90-141">W przeglądarce Utwórz nowy Notes.</span><span class="sxs-lookup"><span data-stu-id="eac90-141">In the browser, create a new notebook.</span></span>

    <span data-ttu-id="eac90-142">**Jupyter Notebook**</span><span class="sxs-lookup"><span data-stu-id="eac90-142">**Jupyter Notebook**</span></span>

    <span data-ttu-id="eac90-143">Wybierz pozycję **nowy > .NET (C#)** lub **Nowy > .NET (F #)**</span><span class="sxs-lookup"><span data-stu-id="eac90-143">Select **New > .NET (C#)** or **New > .NET (F#)**</span></span>

    <span data-ttu-id="eac90-144">**Jupyter Lab**</span><span class="sxs-lookup"><span data-stu-id="eac90-144">**Jupyter Lab**</span></span>

    <span data-ttu-id="eac90-145">W oknie uruchamiania wybierz pozycję **.NET (C#)** lub **.NET (F #)**</span><span class="sxs-lookup"><span data-stu-id="eac90-145">In the Launcher window, select **.NET (C#)** or **.NET (F#)**</span></span>

### <a name="visual-studio-code-preview"></a><span data-ttu-id="eac90-146">Visual Studio Code (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="eac90-146">Visual Studio Code (preview)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="eac90-147">Aby korzystać z notesów Jupyter w VS Code, należy zainstalować następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="eac90-147">To use Jupyter Notebooks in VS Code, you have to install:</span></span>
>
>- [<span data-ttu-id="eac90-148">VS Code niejawnych testerów</span><span class="sxs-lookup"><span data-stu-id="eac90-148">VS Code Insiders</span></span>](https://code.visualstudio.com/insiders/)
>- [<span data-ttu-id="eac90-149">Rozszerzenie programu .NET Interactive Notes</span><span class="sxs-lookup"><span data-stu-id="eac90-149">.NET Interactive Notebooks extension</span></span>](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.dotnet-interactive-vscode)

1. <span data-ttu-id="eac90-150">Otwórz program VS Code.</span><span class="sxs-lookup"><span data-stu-id="eac90-150">Open VS Code.</span></span>
1. <span data-ttu-id="eac90-151">Otwórz widok palety poleceń **> palecie poleceń**.</span><span class="sxs-lookup"><span data-stu-id="eac90-151">Open the command palette **View > Command Palette**.</span></span>

    <span data-ttu-id="eac90-152">Gdy zostanie wyświetlona paleta poleceń, wprowadź następujące polecenie, aby utworzyć nowy interaktywny Notes .NET:</span><span class="sxs-lookup"><span data-stu-id="eac90-152">When the command palette appears, enter the following command to create a new .NET Interactive notebook:</span></span>

    ```text
    >.NET Interactive: Create new blank notebook
    ```

    <span data-ttu-id="eac90-153">Alternatywnie, jeśli chcesz otworzyć istniejący Notes programu .NET Interactive z rozszerzeniem *ipynb* , użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="eac90-153">Alternatively, if you want to open an existing .NET Interactive notebook with the *.ipynb* extension, use the following command:</span></span>

    ```text
    >.NET Interactive: Open notebook
    ```

## <a name="initialize-a-spark-session"></a><span data-ttu-id="eac90-154">Inicjowanie sesji platformy Spark</span><span class="sxs-lookup"><span data-stu-id="eac90-154">Initialize a Spark Session</span></span>

1. <span data-ttu-id="eac90-155">Po otwarciu notesu zainstaluj `Microsoft.Spark` pakiet NuGet.</span><span class="sxs-lookup"><span data-stu-id="eac90-155">When the notebook opens, install the `Microsoft.Spark` NuGet package.</span></span> <span data-ttu-id="eac90-156">Upewnij się, że instalowana wersja jest taka sama jak proces roboczy platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="eac90-156">Make sure the version you install is the same as the .NET Worker.</span></span>

    ```text
    #r "nuget:Microsoft.Spark, 0.12.1"
    ```

1. <span data-ttu-id="eac90-157">Dodaj następującą instrukcję using do notesu.</span><span class="sxs-lookup"><span data-stu-id="eac90-157">Add the following using statement to the notebook.</span></span>

    ```csharp
    using Microsoft.Spark.Sql;
    ```

1. <span data-ttu-id="eac90-158">Zainicjuj [SparkSession](xref:Microsoft.Spark.Sql.SparkSession).</span><span class="sxs-lookup"><span data-stu-id="eac90-158">Initialize your [SparkSession](xref:Microsoft.Spark.Sql.SparkSession).</span></span>

    ```csharp
    var sparkSession =
    SparkSession
        .Builder()
        .AppName("dotnet-interactive-spark")
        .GetOrCreate();
    ```

<span data-ttu-id="eac90-159">Notes powinien wyglądać podobnie do poniższego na poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="eac90-159">The notebook should look similar to the one in the following image.</span></span> <span data-ttu-id="eac90-160">Ten przykład używa VS Code, ale Jupyter Notebook i Jupyter Lab powinien wyglądać tak samo.</span><span class="sxs-lookup"><span data-stu-id="eac90-160">This example uses VS Code, but Jupyter Notebook and Jupyter Lab should look about the same.</span></span>

> [!div class="mx-imgBorder"]
<span data-ttu-id="eac90-161">![Środowisko .NET dla Apache Spark Jupyter Notebook VS Code](media/dotnet-spark-jupyter-notebooks/jupyter-notebooks-dotnet-spark-vscode.png)</span><span class="sxs-lookup"><span data-stu-id="eac90-161">![.NET for Apache Spark Jupyter Notebook VS Code](media/dotnet-spark-jupyter-notebooks/jupyter-notebooks-dotnet-spark-vscode.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="eac90-162">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="eac90-162">Next Steps</span></span>

- [<span data-ttu-id="eac90-163">Wprowadzenie do platformy .NET dla Apache Spark</span><span class="sxs-lookup"><span data-stu-id="eac90-163">Get started with .NET for Apache Spark</span></span>](../tutorials/get-started.md)
- [<span data-ttu-id="eac90-164">Przewidywania tonacji przy użyciu platformy .NET dla Apache Spark i ML.NET</span><span class="sxs-lookup"><span data-stu-id="eac90-164">Predict sentiment using .NET for Apache Spark and ML.NET</span></span>](../tutorials/ml-sentiment-analysis.md)
- <span data-ttu-id="eac90-165">Aby uzyskać więcej informacji na temat programu .NET Interactive, zapoznaj się z [dokumentacją programu .NET Interactive](https://github.com/dotnet/interactive/blob/main/docs/README.md).</span><span class="sxs-lookup"><span data-stu-id="eac90-165">For more information on .NET Interactive, see the [.NET Interactive documentation](https://github.com/dotnet/interactive/blob/main/docs/README.md).</span></span>
