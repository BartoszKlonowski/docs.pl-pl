---
title: 'Samouczek: Wykrywaj anomalie w sprzedaży produktu'
description: Dowiedz się, jak utworzyć aplikację wykrywania anomalii dla danych sprzedaży produktu. W tym samouczku przedstawiono tworzenie aplikacji konsolowej C# platformy .NET Core przy użyciu programu Visual Studio 2019.
ms.date: 07/17/2019
ms.topic: tutorial
ms.custom: mvc, title-hack-0612
ms.openlocfilehash: 4228a68ad43416c6e32684441593d92dfdbfd808
ms.sourcegitcommit: 8c6426a3d2adff5fbcbe1fed0f28eda718c15351
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/02/2019
ms.locfileid: "68733280"
---
# <a name="tutorial-detect-anomalies-in-product-sales-with-mlnet"></a><span data-ttu-id="f2aa6-104">Samouczek: Wykrywaj anomalie w sprzedaży produktów za pomocą ML.NET</span><span class="sxs-lookup"><span data-stu-id="f2aa6-104">Tutorial: Detect anomalies in product sales with ML.NET</span></span>

<span data-ttu-id="f2aa6-105">Dowiedz się, jak utworzyć aplikację wykrywania anomalii dla danych sprzedaży produktu.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-105">Learn how to build an anomaly detection application for product sales data.</span></span> <span data-ttu-id="f2aa6-106">W tym samouczku przedstawiono tworzenie aplikacji konsolowej C# platformy .NET Core przy użyciu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-106">This tutorial creates a .NET Core console application using C# in Visual Studio.</span></span>

<span data-ttu-id="f2aa6-107">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="f2aa6-107">In this tutorial, you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="f2aa6-108">Ładowanie danych</span><span class="sxs-lookup"><span data-stu-id="f2aa6-108">Load the data</span></span>
> * <span data-ttu-id="f2aa6-109">Utwórz transformację wykrywania anomalii</span><span class="sxs-lookup"><span data-stu-id="f2aa6-109">Create a transform for spike anomaly detection</span></span>
> * <span data-ttu-id="f2aa6-110">Wykryj anomalie wzrostu przy użyciu transformacji</span><span class="sxs-lookup"><span data-stu-id="f2aa6-110">Detect spike anomalies with the transform</span></span>
> * <span data-ttu-id="f2aa6-111">Utwórz transformację wykrywania anomalii punktu zmiany</span><span class="sxs-lookup"><span data-stu-id="f2aa6-111">Create a transform for change point anomaly detection</span></span>
> * <span data-ttu-id="f2aa6-112">Wykryj anomalie punktu zmiany przy użyciu transformacji</span><span class="sxs-lookup"><span data-stu-id="f2aa6-112">Detect change point anomalies with the transform</span></span>

<span data-ttu-id="f2aa6-113">Kod źródłowy dla tego samouczka można znaleźć w repozytorium [dotnet/Samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/ProductSalesAnomalyDetection) .</span><span class="sxs-lookup"><span data-stu-id="f2aa6-113">You can find the source code for this tutorial at the [dotnet/samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/ProductSalesAnomalyDetection) repository.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f2aa6-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f2aa6-114">Prerequisites</span></span>

* <span data-ttu-id="f2aa6-115">[Program Visual Studio 2017 15,6 lub nowszy](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) z zainstalowanym obciążeniem "Programowanie dla wielu platform" platformy .NET Core.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-115">[Visual Studio 2017 15.6 or later](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) with the ".NET Core cross-platform development" workload installed.</span></span>

* [<span data-ttu-id="f2aa6-116">Zestaw danych Product-Sales. csv</span><span class="sxs-lookup"><span data-stu-id="f2aa6-116">The product-sales.csv dataset</span></span>](https://raw.githubusercontent.com/dotnet/machinelearning-samples/master/samples/csharp/getting-started/AnomalyDetection_Sales/SpikeDetection/Data/product-sales.csv)

>[!NOTE]
> <span data-ttu-id="f2aa6-117">Format danych w programie `product-sales.csv` jest oparty na zestawie danych "szampon Sales w okresie trzech lat", pierwotnie pochodzący od DataMarket i udostępnianych przez bibliotekę danych szeregów czasowych (TSDL) utworzonych przez Roba Hyndman.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-117">The data format in `product-sales.csv` is based on the dataset “Shampoo Sales Over a Three Year Period” originally sourced from DataMarket and provided by Time Series Data Library (TSDL), created by Rob Hyndman.</span></span>
> <span data-ttu-id="f2aa6-118">"Szampon Sales w okresie trzech lat", który jest licencjonowany w ramach domyślnej licencji Open w ramach programu DataMarket.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-118">“Shampoo Sales Over a Three Year Period” Dataset Licensed Under the DataMarket Default Open License.</span></span>

## <a name="create-a-console-application"></a><span data-ttu-id="f2aa6-119">Tworzenie aplikacji konsolowej</span><span class="sxs-lookup"><span data-stu-id="f2aa6-119">Create a console application</span></span>

1. <span data-ttu-id="f2aa6-120">Utwórz **aplikację konsolową .NET Core** o nazwie "ProductSalesAnomalyDetection".</span><span class="sxs-lookup"><span data-stu-id="f2aa6-120">Create a **.NET Core Console Application** called "ProductSalesAnomalyDetection".</span></span>

2. <span data-ttu-id="f2aa6-121">Utwórz katalog o nazwie *dane* w projekcie, aby zapisać pliki zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-121">Create a directory named *Data* in your project to save your data set files.</span></span>

3. <span data-ttu-id="f2aa6-122">Zainstaluj **pakiet NuGet Microsoft.ml**:</span><span class="sxs-lookup"><span data-stu-id="f2aa6-122">Install the **Microsoft.ML NuGet Package**:</span></span>

    <span data-ttu-id="f2aa6-123">W Eksplorator rozwiązań kliknij prawym przyciskiem myszy projekt i wybierz polecenie **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-123">In Solution Explorer, right-click on your project and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="f2aa6-124">Wybierz pozycję "nuget.org" jako źródło pakietu, wybierz kartę Przeglądaj, Wyszukaj pozycję **Microsoft.ml**, wybierz pakiet **v 1.0.0** na liście, a następnie wybierz przycisk **Instaluj** .</span><span class="sxs-lookup"><span data-stu-id="f2aa6-124">Choose "nuget.org" as the Package source, select the Browse tab, search for **Microsoft.ML**, select the **v1.0.0** package in the list, and select the **Install** button.</span></span> <span data-ttu-id="f2aa6-125">Wybierz przycisk **OK** w oknie dialogowym **Podgląd zmian** , a następnie wybierz przycisk Akceptuję w oknie dialogowym **akceptacji licencji** , jeśli zgadzasz się z postanowieniami licencyjnymi dotyczącymi wymienionych pakietów.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-125">Select the **OK** button on the **Preview Changes** dialog and then select the **I Accept** button on the **License Acceptance** dialog if you agree with the license terms for the packages listed.</span></span> <span data-ttu-id="f2aa6-126">Powtórz te kroki dla **Microsoft. ml. szeregów czasowych v 0.12.0**.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-126">Repeat these steps for **Microsoft.ML.TimeSeries v0.12.0**.</span></span>

4. <span data-ttu-id="f2aa6-127">Dodaj następujące `using` instrukcje w górnej części pliku *program.cs* :</span><span class="sxs-lookup"><span data-stu-id="f2aa6-127">Add the following `using` statements at the top of your *Program.cs* file:</span></span>

    [!code-csharp[AddUsings](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#AddUsings "Add necessary usings")]

### <a name="download-your-data"></a><span data-ttu-id="f2aa6-128">Pobieranie danych</span><span class="sxs-lookup"><span data-stu-id="f2aa6-128">Download your data</span></span>

1. <span data-ttu-id="f2aa6-129">Pobierz zestaw danych i Zapisz go w utworzonym wcześniej folderze *danych* :</span><span class="sxs-lookup"><span data-stu-id="f2aa6-129">Download the dataset and save it to the *Data* folder you previously created:</span></span>

   * <span data-ttu-id="f2aa6-130">Kliknij prawym przyciskiem myszy plik [*Product-Sales. csv*](https://raw.githubusercontent.com/dotnet/machinelearning-samples/master/samples/csharp/getting-started/AnomalyDetection_Sales/SpikeDetection/Data/product-sales.csv) i wybierz pozycję "Zapisz link (lub cel) jako..."</span><span class="sxs-lookup"><span data-stu-id="f2aa6-130">Right click on [*product-sales.csv*](https://raw.githubusercontent.com/dotnet/machinelearning-samples/master/samples/csharp/getting-started/AnomalyDetection_Sales/SpikeDetection/Data/product-sales.csv) and select "Save Link (or Target) As..."</span></span>

     <span data-ttu-id="f2aa6-131">Upewnij się, że plik CSV \*został zapisany w folderze *dane* lub po jego zapisaniu w \*innym miejscu Przenieś plik CSV do folderu *dane* .</span><span class="sxs-lookup"><span data-stu-id="f2aa6-131">Make sure you either save the \*.csv file to the *Data* folder, or after you save it elsewhere, move the \*.csv file to the *Data* folder.</span></span>

2. <span data-ttu-id="f2aa6-132">W Eksplorator rozwiązań kliknij prawym przyciskiem \*myszy plik CSV i wybierz polecenie **Właściwości**.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-132">In Solution Explorer, right-click the \*.csv file and select **Properties**.</span></span> <span data-ttu-id="f2aa6-133">W obszarze **Zaawansowane**Zmień wartość opcji **Kopiuj do katalogu wyjściowego** na Kopiuj, **jeśli nowszy**.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-133">Under **Advanced**, change the value of **Copy to Output Directory** to **Copy if newer**.</span></span>

<span data-ttu-id="f2aa6-134">Poniższa tabela zawiera podgląd danych z \*pliku CSV:</span><span class="sxs-lookup"><span data-stu-id="f2aa6-134">The following table is a data preview from your \*.csv file:</span></span>

|<span data-ttu-id="f2aa6-135">Bieżącym</span><span class="sxs-lookup"><span data-stu-id="f2aa6-135">Month</span></span>  |<span data-ttu-id="f2aa6-136">ProductSales</span><span class="sxs-lookup"><span data-stu-id="f2aa6-136">ProductSales</span></span> |
|-------|-------------|
|<span data-ttu-id="f2aa6-137">1 stycznia</span><span class="sxs-lookup"><span data-stu-id="f2aa6-137">1-Jan</span></span>  |    <span data-ttu-id="f2aa6-138">271</span><span class="sxs-lookup"><span data-stu-id="f2aa6-138">271</span></span>      |
|<span data-ttu-id="f2aa6-139">2-sty</span><span class="sxs-lookup"><span data-stu-id="f2aa6-139">2-Jan</span></span>  |    <span data-ttu-id="f2aa6-140">150,9</span><span class="sxs-lookup"><span data-stu-id="f2aa6-140">150.9</span></span>    |
|<span data-ttu-id="f2aa6-141">.....</span><span class="sxs-lookup"><span data-stu-id="f2aa6-141">.....</span></span>  |    <span data-ttu-id="f2aa6-142">.....</span><span class="sxs-lookup"><span data-stu-id="f2aa6-142">.....</span></span>    |
|<span data-ttu-id="f2aa6-143">1 — Luty</span><span class="sxs-lookup"><span data-stu-id="f2aa6-143">1-Feb</span></span>  |    <span data-ttu-id="f2aa6-144">199,3</span><span class="sxs-lookup"><span data-stu-id="f2aa6-144">199.3</span></span>    |
|<span data-ttu-id="f2aa6-145">.....</span><span class="sxs-lookup"><span data-stu-id="f2aa6-145">.....</span></span>  |    <span data-ttu-id="f2aa6-146">.....</span><span class="sxs-lookup"><span data-stu-id="f2aa6-146">.....</span></span>    |

### <a name="create-classes-and-define-paths"></a><span data-ttu-id="f2aa6-147">Tworzenie klas i Definiowanie ścieżek</span><span class="sxs-lookup"><span data-stu-id="f2aa6-147">Create classes and define paths</span></span>

<span data-ttu-id="f2aa6-148">Następnie zdefiniuj struktury danych dla klas wejściowych i prognoz.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-148">Next, define your input and prediction class data structures.</span></span>

<span data-ttu-id="f2aa6-149">Dodaj nową klasę do projektu:</span><span class="sxs-lookup"><span data-stu-id="f2aa6-149">Add a new class to your project:</span></span>

1. <span data-ttu-id="f2aa6-150">W **Eksplorator rozwiązań**kliknij prawym przyciskiem myszy projekt, a następnie wybierz pozycję **Dodaj > nowy element**.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-150">In **Solution Explorer**, right-click the project, and then select **Add > New Item**.</span></span>

2. <span data-ttu-id="f2aa6-151">W **oknie dialogowym Dodaj nowy element**wybierz pozycję **Klasa** i zmień wartość pola **Nazwa** na *ProductSalesData.cs*.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-151">In the **Add New Item dialog box**, select **Class** and change the **Name** field to *ProductSalesData.cs*.</span></span> <span data-ttu-id="f2aa6-152">Następnie wybierz przycisk **Dodaj** .</span><span class="sxs-lookup"><span data-stu-id="f2aa6-152">Then, select the **Add** button.</span></span>

   <span data-ttu-id="f2aa6-153">Plik *ProductSalesData.cs* zostanie otwarty w edytorze kodu.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-153">The *ProductSalesData.cs* file opens in the code editor.</span></span>

3. <span data-ttu-id="f2aa6-154">Dodaj następującą `using` instrukcję na początku *ProductSalesData.cs*:</span><span class="sxs-lookup"><span data-stu-id="f2aa6-154">Add the following `using` statement to the top of *ProductSalesData.cs*:</span></span>

   ```csharp
   using Microsoft.ML.Data;
   ```

4. <span data-ttu-id="f2aa6-155">Usuń istniejącą definicję klasy i Dodaj następujący kod, który ma dwie klasy `ProductSalesData` i `ProductSalesPrediction`, do pliku *ProductSalesData.cs* :</span><span class="sxs-lookup"><span data-stu-id="f2aa6-155">Remove the existing class definition and add the following code, which has two classes `ProductSalesData` and `ProductSalesPrediction`, to the *ProductSalesData.cs* file:</span></span>

    [!code-csharp[DeclareTypes](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/ProductSalesData.cs#DeclareTypes "Declare data record types")]

    <span data-ttu-id="f2aa6-156">`ProductSalesData`Określa klasę danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-156">`ProductSalesData` specifies an input data class.</span></span> <span data-ttu-id="f2aa6-157">Atrybut [LoadColumn](xref:Microsoft.ML.Data.LoadColumnAttribute.%23ctor%28System.Int32%29) określa, które kolumny (według indeksu kolumn) w zestawie danych powinny zostać załadowane.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-157">The [LoadColumn](xref:Microsoft.ML.Data.LoadColumnAttribute.%23ctor%28System.Int32%29) attribute specifies which columns (by column index) in the dataset should be loaded.</span></span>

    <span data-ttu-id="f2aa6-158">`ProductSalesPrediction`Określa klasę danych przewidywania.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-158">`ProductSalesPrediction` specifies the prediction data class.</span></span> <span data-ttu-id="f2aa6-159">W przypadku wykrywania anomalii Funkcja prognozowania składa się z alertu, aby wskazać, czy występuje anomalia, nieprzetworzony wynik i wartość p.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-159">For anomaly detection, the prediction consists of an alert to indicate whether there is an anomaly, a raw score, and p-value.</span></span> <span data-ttu-id="f2aa6-160">Bliżej wartości p jest równa 0, tym bardziej prawdopodobnie wystąpił anomalia.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-160">The closer the p-value is to 0, the more likely an anomaly has occurred.</span></span>

5. <span data-ttu-id="f2aa6-161">Utwórz dwa pola globalne do przechowywania ostatnio pobranej ścieżki pliku zestawu danych i zapisanej ścieżki pliku modelu:</span><span class="sxs-lookup"><span data-stu-id="f2aa6-161">Create two global fields to hold the recently downloaded dataset file path and the saved model file path:</span></span>

    * <span data-ttu-id="f2aa6-162">`_dataPath`ma ścieżkę do zestawu danych używanego do uczenia modelu.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-162">`_dataPath` has the path to the dataset used to train the model.</span></span>
    * <span data-ttu-id="f2aa6-163">`_docsize`zawiera liczbę rekordów w pliku DataSet.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-163">`_docsize` has the number of records in dataset file.</span></span> <span data-ttu-id="f2aa6-164">Użyjesz `_docSize` do obliczenia `pvalueHistoryLength`.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-164">You'll use `_docSize` to calculate `pvalueHistoryLength`.</span></span>

6. <span data-ttu-id="f2aa6-165">Dodaj następujący kod do wiersza bezpośrednio powyżej metody, `Main` aby określić te ścieżki:</span><span class="sxs-lookup"><span data-stu-id="f2aa6-165">Add the following code to the line right above the `Main` method to specify those paths:</span></span>

    [!code-csharp[Declare global variables](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#DeclareGlobalVariables "Declare global variables")]

### <a name="initialize-variables-in-main"></a><span data-ttu-id="f2aa6-166">Inicjuj zmienne w głównym</span><span class="sxs-lookup"><span data-stu-id="f2aa6-166">Initialize variables in Main</span></span>

1. <span data-ttu-id="f2aa6-167">Zastąp `Main` `mlContext` wiersz w metodzie poniższym kodem, aby zadeklarować i zainicjować zmienną: `Console.WriteLine("Hello World!")`</span><span class="sxs-lookup"><span data-stu-id="f2aa6-167">Replace the `Console.WriteLine("Hello World!")` line in the `Main` method with the following code to declare and initialize the `mlContext` variable:</span></span>

    [!code-csharp[CreateMLContext](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#CreateMLContext "Create the ML Context")]

    <span data-ttu-id="f2aa6-168">[Klasa MLContext](xref:Microsoft.ML.MLContext) jest punktem początkowym dla wszystkich operacji ml.NET, a inicjowanie `mlContext` tworzy nowe środowisko ml.NET, które może być współużytkowane przez obiekty przepływu pracy tworzenia modelu.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-168">The [MLContext class](xref:Microsoft.ML.MLContext) is a starting point for all ML.NET operations, and initializing `mlContext` creates a new ML.NET environment that can be shared across the model creation workflow objects.</span></span> <span data-ttu-id="f2aa6-169">Jest to podobne, pojęciowo do `DBContext` w Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-169">It's similar, conceptually, to `DBContext` in Entity Framework.</span></span>

### <a name="load-the-data"></a><span data-ttu-id="f2aa6-170">Ładowanie danych</span><span class="sxs-lookup"><span data-stu-id="f2aa6-170">Load the data</span></span>

<span data-ttu-id="f2aa6-171">Dane w ML.NET są reprezentowane jako [Klasa IDataView](xref:Microsoft.ML.IDataView).</span><span class="sxs-lookup"><span data-stu-id="f2aa6-171">Data in ML.NET is represented as an [IDataView class](xref:Microsoft.ML.IDataView).</span></span> <span data-ttu-id="f2aa6-172">`IDataView`to elastyczny i wydajny sposób opisywania danych tabelarycznych (liczbowych i tekstowych).</span><span class="sxs-lookup"><span data-stu-id="f2aa6-172">`IDataView` is a flexible, efficient way of describing tabular data (numeric and text).</span></span> <span data-ttu-id="f2aa6-173">Dane można ładować z pliku tekstowego lub z innych źródeł (na przykład bazy danych SQL lub plików dziennika) do `IDataView` obiektu.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-173">Data can be loaded from a text file or from other sources (for example, SQL database or log files) to an `IDataView` object.</span></span>

1. <span data-ttu-id="f2aa6-174">Dodaj następujący kod w następnym wierszu `Main()` metody:</span><span class="sxs-lookup"><span data-stu-id="f2aa6-174">Add the following code as the next line of the `Main()` method:</span></span>

    [!code-csharp[LoadData](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#LoadData "loading dataset")]

    <span data-ttu-id="f2aa6-175">[LoadFromTextFile ()](xref:Microsoft.ML.TextLoaderSaverCatalog.LoadFromTextFile%60%601%28Microsoft.ML.DataOperationsCatalog,System.String,System.Char,System.Boolean,System.Boolean,System.Boolean,System.Boolean%29) definiuje schemat danych i odczytuje w pliku.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-175">The [LoadFromTextFile()](xref:Microsoft.ML.TextLoaderSaverCatalog.LoadFromTextFile%60%601%28Microsoft.ML.DataOperationsCatalog,System.String,System.Char,System.Boolean,System.Boolean,System.Boolean,System.Boolean%29) defines the data schema and reads in the file.</span></span> <span data-ttu-id="f2aa6-176">Przyjmuje zmienne ścieżki danych i zwraca `IDataView`.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-176">It takes in the data path variables and returns an `IDataView`.</span></span>

## <a name="time-series-anomaly-detection"></a><span data-ttu-id="f2aa6-177">Wykrywanie anomalii szeregów czasowych</span><span class="sxs-lookup"><span data-stu-id="f2aa6-177">Time series anomaly detection</span></span>

<span data-ttu-id="f2aa6-178">Wykrywanie anomalii flagi nieoczekiwane lub nietypowe zdarzenia lub zachowania.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-178">Anomaly detection flags unexpected or unusual events or behaviors.</span></span> <span data-ttu-id="f2aa6-179">Zawiera wskazówki, gdzie szukać problemów i pomaga odpowiedzieć na pytanie "czy to brzmienia?".</span><span class="sxs-lookup"><span data-stu-id="f2aa6-179">It gives clues where to look for problems and helps you answer the question "Is this weird?".</span></span>

![Czy ten brzmienia](./media/sales-anomaly-detection/anomalydetection.png)

<span data-ttu-id="f2aa6-181">Wykrywanie anomalii to proces wykrywania wartości odstających danych szeregów czasowych; wskazuje na dane wejściowe serie czasowe, w których zachowanie nie jest oczekiwane, lub "brzmienia".</span><span class="sxs-lookup"><span data-stu-id="f2aa6-181">Anomaly detection is the process of detecting time-series data outliers; points on a given input time-series where the behavior isn't what was expected, or "weird".</span></span>

<span data-ttu-id="f2aa6-182">Wykrywanie anomalii może być przydatne na wiele sposobów.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-182">Anomaly detection can be useful in lots of ways.</span></span> <span data-ttu-id="f2aa6-183">Przykład:</span><span class="sxs-lookup"><span data-stu-id="f2aa6-183">For instance:</span></span>

<span data-ttu-id="f2aa6-184">Jeśli masz samochód, warto wiedzieć: Czy ten miernik oleju jest odczytywany w normalnym lub czy mam wyciek?</span><span class="sxs-lookup"><span data-stu-id="f2aa6-184">If you have a car, you might want to know: Is this oil gauge reading normal, or do I have a leak?</span></span>
<span data-ttu-id="f2aa6-185">Jeśli monitorujesz zużycie mocy, warto wiedzieć: Czy wystąpił przestój?</span><span class="sxs-lookup"><span data-stu-id="f2aa6-185">If you're monitoring power consumption, you’d want to know: Is there an outage?</span></span>

<span data-ttu-id="f2aa6-186">Istnieją dwa typy anomalii szeregów czasowych, które mogą zostać wykryte:</span><span class="sxs-lookup"><span data-stu-id="f2aa6-186">There are two types of time series anomalies that can be detected:</span></span>

* <span data-ttu-id="f2aa6-187">**Skoki** wskazują tymczasowe rozerwania nietypowego zachowania w systemie.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-187">**Spikes** indicate temporary bursts of anomalous behavior in the system.</span></span>

* <span data-ttu-id="f2aa6-188">**Punkty zmian** wskazują początek trwałych zmian w czasie w systemie.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-188">**Change points** indicate the beginning of persistent changes over time in the system.</span></span>

<span data-ttu-id="f2aa6-189">W programie ML.NET algorytmy wykrywania i wykrywania punktu zmiany identyfikatora IID są odpowiednie dla niezależnych [i identycznie rozproszonych zestawów danych](https://en.wikipedia.org/wiki/Independent_and_identically_distributed_random_variables).</span><span class="sxs-lookup"><span data-stu-id="f2aa6-189">In ML.NET, The IID Spike Detection or IID Change point Detection algorithms are suited for [independent and identically distributed datasets](https://en.wikipedia.org/wiki/Independent_and_identically_distributed_random_variables).</span></span>

<span data-ttu-id="f2aa6-190">W przeciwieństwie do modeli w innych samouczkach, program wykrywania anomalii w szeregach czasowych działa bezpośrednio na danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-190">Unlike the models in the other tutorials, the time series anomaly detector transforms operate directly on input data.</span></span> <span data-ttu-id="f2aa6-191">`IEstimator.Fit()` Metoda nie potrzebuje danych szkoleniowych do wygenerowania transformacji.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-191">The `IEstimator.Fit()` method does not need training data to produce the transform.</span></span> <span data-ttu-id="f2aa6-192">Wymaga schematu danych, który jest dostarczany przez widok danych wygenerowany na podstawie pustej listy `ProductSalesData`.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-192">It does need the data schema though, which is provided by a data view generated from an empty list of `ProductSalesData`.</span></span>

<span data-ttu-id="f2aa6-193">Przeanalizujesz te same dane sprzedaży produktu w celu wykrywania skoków i punktów zmian.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-193">You'll analyze the same product sales data to detect spikes and change points.</span></span> <span data-ttu-id="f2aa6-194">Proces kompilowania i uczenia jest taki sam, jak w celu uzyskania wykrywalności i wykrywania punktów zmiany; Główną różnicą jest używany algorytm wykrywania.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-194">The building and training model process is the same for spike detection and change point detection; the main difference is the specific detection algorithm used.</span></span>

## <a name="spike-detection"></a><span data-ttu-id="f2aa6-195">Wykrywanie</span><span class="sxs-lookup"><span data-stu-id="f2aa6-195">Spike detection</span></span>

<span data-ttu-id="f2aa6-196">Celem w zakresie wykrywania jest zidentyfikowanie nagłych obciążeń tymczasowych, które znacząco różnią się od większości wartości danych szeregów czasowych.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-196">The goal of spike detection is to identify sudden yet temporary bursts that significantly differ from the majority of the time series data values.</span></span> <span data-ttu-id="f2aa6-197">Ważne jest, aby wykrywać te podejrzane rzadkie elementy, zdarzenia lub obserwacje w odpowiednim czasie, aby być zminimalizowane.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-197">It's important to detect these suspicious rare items, events, or observations in a timely manner to be minimized.</span></span> <span data-ttu-id="f2aa6-198">Poniższe podejście może służyć do wykrywania różnych anomalii, takich jak: awaria, ataki cybernetycznymi lub wirusowej zawartości sieci Web.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-198">The following approach can be used to detect a variety of anomalies such as: outages, cyber-attacks, or viral web content.</span></span> <span data-ttu-id="f2aa6-199">Na poniższej ilustracji przedstawiono przykład skoków w zestawie danych szeregów czasowych:</span><span class="sxs-lookup"><span data-stu-id="f2aa6-199">The following image is an example of spikes in a time series dataset:</span></span>

![SpikeDetection](./media/sales-anomaly-detection/SpikeDetection.png)

### <a name="add-the-createemptydataview-method"></a><span data-ttu-id="f2aa6-201">Dodaj metodę CreateEmptyDataView ()</span><span class="sxs-lookup"><span data-stu-id="f2aa6-201">Add the CreateEmptyDataView() method</span></span>

<span data-ttu-id="f2aa6-202">Dodaj następującą metodę do `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="f2aa6-202">Add the following method to `Program.cs`:</span></span>

[!code-csharp[CreateEmptyDataView](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#CreateEmptyDataView)]

<span data-ttu-id="f2aa6-203">Powoduje utworzenie pustego obiektu widoku danych z prawidłowym schematem, który będzie używany jako dane `IEstimator.Fit()` wejściowe metody. `CreateEmptyDataView()`</span><span class="sxs-lookup"><span data-stu-id="f2aa6-203">The `CreateEmptyDataView()` produces an empty data view object with the correct schema to be used as input to the `IEstimator.Fit()` method.</span></span>

### <a name="create-the-detectspike-method"></a><span data-ttu-id="f2aa6-204">Tworzenie metody DetectSpike ()</span><span class="sxs-lookup"><span data-stu-id="f2aa6-204">Create the DetectSpike() method</span></span>

<span data-ttu-id="f2aa6-205">`DetectSpike()` Metody:</span><span class="sxs-lookup"><span data-stu-id="f2aa6-205">The `DetectSpike()` method:</span></span>

* <span data-ttu-id="f2aa6-206">Tworzy transformację z szacowania.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-206">Creates the transform from the estimator.</span></span>
* <span data-ttu-id="f2aa6-207">Wykrywa skoki na podstawie historycznych danych sprzedaży.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-207">Detects spikes based on historical sales data.</span></span>
* <span data-ttu-id="f2aa6-208">Wyświetla wyniki.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-208">Displays the results.</span></span>

1. <span data-ttu-id="f2aa6-209">Utwórz metodę, tuż po metodzie, przy użyciu następującego kodu: `Main()` `DetectSpike()`</span><span class="sxs-lookup"><span data-stu-id="f2aa6-209">Create the `DetectSpike()` method, just after the `Main()` method, using the following code:</span></span>

    ```csharp
    static void DetectSpike(MLContext mlContext, int docSize, IDataView productSales)
    {

    }
    ```

1. <span data-ttu-id="f2aa6-210">Użyj [IidSpikeEstimator](xref:Microsoft.ML.Transforms.TimeSeries.IidSpikeEstimator) , aby nauczyć model na potrzeby wykrywania.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-210">Use the [IidSpikeEstimator](xref:Microsoft.ML.Transforms.TimeSeries.IidSpikeEstimator) to train the model for spike detection.</span></span> <span data-ttu-id="f2aa6-211">Dodaj go do `DetectSpike()` metody przy użyciu następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="f2aa6-211">Add it to the `DetectSpike()` method with the following code:</span></span>

    [!code-csharp[AddSpikeTrainer](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#AddSpikeTrainer)]

1. <span data-ttu-id="f2aa6-212">Utwórz transformację wykrycia, dodając następujący kod jako następny wiersz kodu w `DetectSpike()` metodzie:</span><span class="sxs-lookup"><span data-stu-id="f2aa6-212">Create the spike detection transform by adding the following as the next line of code in the `DetectSpike()` method:</span></span>

    [!code-csharp[TrainModel1](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#TrainModel1)]

1. <span data-ttu-id="f2aa6-213">Dodaj następujący wiersz kodu, aby przekształcić `productSales` dane jako następny wiersz `DetectSpike()` w metodzie:</span><span class="sxs-lookup"><span data-stu-id="f2aa6-213">Add the following line of code to transform the `productSales` data as the next line in the `DetectSpike()` method:</span></span>

    [!code-csharp[TransformData1](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#TransformData1)]

    <span data-ttu-id="f2aa6-214">Poprzedni kod używa metody [Transform ()](xref:Microsoft.ML.ITransformer.Transform%2A) do prognozowania dla wielu wierszy wejściowych zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-214">The previous code uses the [Transform()](xref:Microsoft.ML.ITransformer.Transform%2A) method to make predictions for multiple input rows of a dataset.</span></span>

1. <span data-ttu-id="f2aa6-215">Konwertuj na silnie wpisaną `IEnumerable` wartość, aby ułatwić wyświetlanie przy użyciu metody "xmlliczaln [()](xref:Microsoft.ML.DataOperationsCatalog.CreateEnumerable%2A) " z następującym kodem: `transformedData`</span><span class="sxs-lookup"><span data-stu-id="f2aa6-215">Convert your `transformedData` into a strongly-typed `IEnumerable` for easier display using the [CreateEnumerable()](xref:Microsoft.ML.DataOperationsCatalog.CreateEnumerable%2A) method with the following code:</span></span>

    [!code-csharp[CreateEnumerable1](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#CreateEnumerable1)]

1. <span data-ttu-id="f2aa6-216">Utwórz wiersz nagłówka wyświetlanego przy użyciu następującego <xref:System.Console.WriteLine?displayProperty=nameWithType> kodu:</span><span class="sxs-lookup"><span data-stu-id="f2aa6-216">Create a display header line using the following <xref:System.Console.WriteLine?displayProperty=nameWithType> code:</span></span>

    [!code-csharp[DisplayHeader1](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#DisplayHeader1)]

    <span data-ttu-id="f2aa6-217">Następujące informacje zostaną wyświetlone w wynikach wykrywania:</span><span class="sxs-lookup"><span data-stu-id="f2aa6-217">You'll display the following information in your spike detection results:</span></span>

    * <span data-ttu-id="f2aa6-218">`Alert`wskazuje alert dla danego punktu danych.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-218">`Alert` indicates a spike alert for a given data point.</span></span>
    * <span data-ttu-id="f2aa6-219">`Score``ProductSales` jest wartością dla danego punktu danych w zestawie danych.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-219">`Score` is the `ProductSales` value for a given data point in the dataset.</span></span>
    * <span data-ttu-id="f2aa6-220">`P-Value`"P" oznacza prawdopodobieństwo.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-220">`P-Value` The "P" stands for probability.</span></span> <span data-ttu-id="f2aa6-221">Im bliżej wartości p jest to 0, tym bardziej prawdopodobnie punkt danych jest anomalią.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-221">The closer the p-value is to 0, the more likely the data point is an anomaly.</span></span>

1. <span data-ttu-id="f2aa6-222">Użyj poniższego kodu, aby wykonać iterację `predictions` `IEnumerable` i wyświetlić wyniki:</span><span class="sxs-lookup"><span data-stu-id="f2aa6-222">Use the following code to iterate through the `predictions` `IEnumerable` and display the results:</span></span>

    [!code-csharp[DisplayResults1](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#DisplayResults1)]

1. <span data-ttu-id="f2aa6-223">Dodaj wywołanie `DetectSpike()`metody `Main()` w metodzie:</span><span class="sxs-lookup"><span data-stu-id="f2aa6-223">Add the call to the `DetectSpike()`method in the `Main()` method:</span></span>

    [!code-csharp[CallDetectSpike](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#CallDetectSpike)]

## <a name="spike-detection-results"></a><span data-ttu-id="f2aa6-224">Skoki wyników wykrywania</span><span class="sxs-lookup"><span data-stu-id="f2aa6-224">Spike detection results</span></span>

<span data-ttu-id="f2aa6-225">Wyniki powinny wyglądać podobnie do poniższego.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-225">Your results should be similar to the following.</span></span> <span data-ttu-id="f2aa6-226">Podczas przetwarzania wyświetlane są komunikaty.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-226">During processing, messages are displayed.</span></span> <span data-ttu-id="f2aa6-227">Mogą pojawić się ostrzeżenia lub przetwarzanie komunikatów.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-227">You may see warnings, or processing messages.</span></span> <span data-ttu-id="f2aa6-228">Niektóre z tych komunikatów zostały usunięte z następujących wyników dla przejrzystości.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-228">Some of the messages have been removed from the following results for clarity.</span></span>

```console
Detect temporary changes in pattern
=============== Training the model ===============
=============== End of training process ===============
Alert   Score   P-Value
0       271.00  0.50
0       150.90  0.00
0       188.10  0.41
0       124.30  0.13
0       185.30  0.47
0       173.50  0.47
0       236.80  0.19
0       229.50  0.27
0       197.80  0.48
0       127.90  0.13
1       341.50  0.00 <-- Spike detected
0       190.90  0.48
0       199.30  0.48
0       154.50  0.24
0       215.10  0.42
0       278.30  0.19
0       196.40  0.43
0       292.00  0.17
0       231.00  0.45
0       308.60  0.18
0       294.90  0.19
1       426.60  0.00 <-- Spike detected
0       269.50  0.47
0       347.30  0.21
0       344.70  0.27
0       445.40  0.06
0       320.90  0.49
0       444.30  0.12
0       406.30  0.29
0       442.40  0.21
1       580.50  0.00 <-- Spike detected
0       412.60  0.45
1       687.00  0.01 <-- Spike detected
0       480.30  0.40
0       586.30  0.20
0       651.90  0.14
```

## <a name="change-point-detection"></a><span data-ttu-id="f2aa6-229">Wykrywanie punktu zmiany</span><span class="sxs-lookup"><span data-stu-id="f2aa6-229">Change point detection</span></span>

<span data-ttu-id="f2aa6-230">`Change points`są trwałymi zmianami w czasie dystrybucji strumienia zdarzeń szeregów czasowych, takich jak zmiany poziomów i trendy.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-230">`Change points` are persistent changes in a time series event stream distribution of values, like level changes and trends.</span></span> <span data-ttu-id="f2aa6-231">Te trwałe zmiany są ostatnie znacznie dłużej `spikes` niż i mogą wskazywać na katastrofalne zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-231">These persistent changes last much longer than `spikes` and could indicate catastrophic event(s).</span></span> <span data-ttu-id="f2aa6-232">`Change points`nie są zwykle widoczne dla gołym okiem, ale mogą być wykrywane w danych przy użyciu podejścia, takiego jak w poniższej metodzie.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-232">`Change points` are not usually visible to the naked eye, but can be detected in your data using approaches such as in the following method.</span></span>  <span data-ttu-id="f2aa6-233">Na poniższej ilustracji przedstawiono przykład wykrywania punktu zmiany:</span><span class="sxs-lookup"><span data-stu-id="f2aa6-233">The following image is an example of a change point detection:</span></span>

![ChangePointDetection](./media/sales-anomaly-detection/ChangePointDetection.png)

### <a name="create-the-detectchangepoint-method"></a><span data-ttu-id="f2aa6-235">Tworzenie metody DetectChangepoint ()</span><span class="sxs-lookup"><span data-stu-id="f2aa6-235">Create the DetectChangepoint() method</span></span>

<span data-ttu-id="f2aa6-236">`DetectChangepoint()` Metoda wykonuje następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="f2aa6-236">The `DetectChangepoint()` method executes the following tasks:</span></span>

* <span data-ttu-id="f2aa6-237">Tworzy transformację z szacowania.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-237">Creates the transform from the estimator.</span></span>
* <span data-ttu-id="f2aa6-238">Wykrywa punkty zmian w oparciu o dane dotyczące sprzedaży historycznej.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-238">Detects change points based on historical sales data.</span></span>
* <span data-ttu-id="f2aa6-239">Wyświetla wyniki.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-239">Displays the results.</span></span>

1. <span data-ttu-id="f2aa6-240">Utwórz metodę, tuż po metodzie, przy użyciu następującego kodu: `Main()` `DetectChangepoint()`</span><span class="sxs-lookup"><span data-stu-id="f2aa6-240">Create the `DetectChangepoint()` method, just after the `Main()` method, using the following code:</span></span>

    ```csharp
    static void DetectChangepoint(MLContext mlContext, int docSize, IDataView productSales)
    {

    }
    ```

1. <span data-ttu-id="f2aa6-241">Utwórz [iidChangePointEstimator](xref:Microsoft.ML.Transforms.TimeSeries.IidChangePointEstimator) w `DetectChangepoint()` metodzie przy użyciu następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="f2aa6-241">Create the [iidChangePointEstimator](xref:Microsoft.ML.Transforms.TimeSeries.IidChangePointEstimator) in the `DetectChangepoint()` method with the following code:</span></span>

    [!code-csharp[AddChangepointTrainer](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#AddChangepointTrainer)]

1. <span data-ttu-id="f2aa6-242">Jak wcześniej, Utwórz transformację z szacowania, dodając następujący wiersz kodu w `DetectChangePoint()` metodzie:</span><span class="sxs-lookup"><span data-stu-id="f2aa6-242">As you did previously, create the transform from the estimator by adding the following line of code in the `DetectChangePoint()` method:</span></span>

    [!code-csharp[TrainModel2](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#TrainModel2)]

1. <span data-ttu-id="f2aa6-243">Użyj metody do przekształcenia danych, dodając następujący kod do `DetectChangePoint()`: `Transform()`</span><span class="sxs-lookup"><span data-stu-id="f2aa6-243">Use the `Transform()` method to transform the data by adding the following code to `DetectChangePoint()`:</span></span>

    [!code-csharp[TransformData2](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#TransformData2)]

1. <span data-ttu-id="f2aa6-244">Tak jak wcześniej, przekonwertuj `transformedData` na silnie wpisaną `IEnumerable` wartość, `CreateEnumerable()`aby ułatwić wyświetlanie przy użyciu metody z następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="f2aa6-244">As you did previously, convert your `transformedData` into a strongly-typed `IEnumerable` for easier display using the `CreateEnumerable()`method with the following code:</span></span>

    [!code-csharp[CreateEnumerable2](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#CreateEnumerable2)]

1. <span data-ttu-id="f2aa6-245">Utwórz nagłówek wyświetlania z następującym kodem jako następnym wierszem w `DetectChangePoint()` metodzie:</span><span class="sxs-lookup"><span data-stu-id="f2aa6-245">Create a display header with the following code as the next line in the `DetectChangePoint()` method:</span></span>

    [!code-csharp[DisplayHeader2](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#DisplayHeader2)]

    <span data-ttu-id="f2aa6-246">W wynikach wykrywania punktu zmiany zostaną wyświetlone następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="f2aa6-246">You'll display the following information in your change point detection results:</span></span>

    * <span data-ttu-id="f2aa6-247">`Alert`wskazuje alert punktu zmiany dla danego punktu danych.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-247">`Alert` indicates a change point alert for a given data point.</span></span>
    * <span data-ttu-id="f2aa6-248">`Score``ProductSales` jest wartością dla danego punktu danych w zestawie danych.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-248">`Score` is the `ProductSales` value for a given data point in the dataset.</span></span>
    * <span data-ttu-id="f2aa6-249">`P-Value`"P" oznacza prawdopodobieństwo.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-249">`P-Value` The "P" stands for probability.</span></span> <span data-ttu-id="f2aa6-250">Im bliżej wartości P jest to 0, tym bardziej prawdopodobnie punkt danych jest anomalią.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-250">The closer the P-value is to 0, the more likely the data point is an anomaly.</span></span>
    * <span data-ttu-id="f2aa6-251">`Martingale value`służy do identyfikowania, jak "brzmienia" punkt danych jest oparty na sekwencji wartości P.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-251">`Martingale value` is used to identify how "weird" a data point is, based on the sequence of P-values.</span></span>

1. <span data-ttu-id="f2aa6-252">Wykonaj iterację i Wyświetl wyniki przy użyciu następującego kodu: `IEnumerable` `predictions`</span><span class="sxs-lookup"><span data-stu-id="f2aa6-252">Iterate through the `predictions` `IEnumerable` and display the results with the following code:</span></span>

    [!code-csharp[DisplayResults2](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#DisplayResults2)]

1. <span data-ttu-id="f2aa6-253">Dodaj następujące wywołanie do `DetectChangepoint()`metody `Main()` w metodzie:</span><span class="sxs-lookup"><span data-stu-id="f2aa6-253">Add the following call to the `DetectChangepoint()`method in the `Main()` method:</span></span>

    [!code-csharp[CallDetectChangepoint](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#CallDetectChangepoint)]

## <a name="change-point-detection-results"></a><span data-ttu-id="f2aa6-254">Wyniki wykrywania punktu zmiany</span><span class="sxs-lookup"><span data-stu-id="f2aa6-254">Change point detection results</span></span>

<span data-ttu-id="f2aa6-255">Wyniki powinny wyglądać podobnie do poniższego.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-255">Your results should be similar to the following.</span></span> <span data-ttu-id="f2aa6-256">Podczas przetwarzania wyświetlane są komunikaty.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-256">During processing, messages are displayed.</span></span> <span data-ttu-id="f2aa6-257">Mogą pojawić się ostrzeżenia lub przetwarzanie komunikatów.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-257">You may see warnings, or processing messages.</span></span> <span data-ttu-id="f2aa6-258">Niektóre komunikaty zostały usunięte z następujących wyników dla przejrzystości.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-258">Some messages have been removed from the following results for clarity.</span></span>

```console
Detect Persistent changes in pattern
=============== Training the model Using Change Point Detection Algorithm===============
=============== End of training process ===============
Alert   Score   P-Value Martingale value
0       271.00  0.50    0.00
0       150.90  0.00    2.33
0       188.10  0.41    2.80
0       124.30  0.13    9.16
0       185.30  0.47    9.77
0       173.50  0.47    10.41
0       236.80  0.19    24.46
0       229.50  0.27    42.38
1       197.80  0.48    44.23 <-- alert is on, predicted changepoint
0       127.90  0.13    145.25
0       341.50  0.00    0.01
0       190.90  0.48    0.01
0       199.30  0.48    0.00
0       154.50  0.24    0.00
0       215.10  0.42    0.00
0       278.30  0.19    0.00
0       196.40  0.43    0.00
0       292.00  0.17    0.01
0       231.00  0.45    0.00
0       308.60  0.18    0.00
0       294.90  0.19    0.00
0       426.60  0.00    0.00
0       269.50  0.47    0.00
0       347.30  0.21    0.00
0       344.70  0.27    0.00
0       445.40  0.06    0.02
0       320.90  0.49    0.01
0       444.30  0.12    0.02
0       406.30  0.29    0.01
0       442.40  0.21    0.01
0       580.50  0.00    0.01
0       412.60  0.45    0.01
0       687.00  0.01    0.12
0       480.30  0.40    0.08
0       586.30  0.20    0.03
0       651.90  0.14    0.09
```

<span data-ttu-id="f2aa6-259">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="f2aa6-259">Congratulations!</span></span> <span data-ttu-id="f2aa6-260">Pomyślnie skompilowano modele uczenia maszynowego na potrzeby wykrywania skoków i różnic punktów zmian w danych sprzedaży.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-260">You've now successfully built machine learning models for detecting spikes and change point anomalies in sales data.</span></span>

<span data-ttu-id="f2aa6-261">Kod źródłowy dla tego samouczka można znaleźć w repozytorium [dotnet/Samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/ProductSalesAnomalyDetection) .</span><span class="sxs-lookup"><span data-stu-id="f2aa6-261">You can find the source code for this tutorial at the [dotnet/samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/ProductSalesAnomalyDetection) repository.</span></span>

<span data-ttu-id="f2aa6-262">W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="f2aa6-262">In this tutorial, you learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="f2aa6-263">Ładowanie danych</span><span class="sxs-lookup"><span data-stu-id="f2aa6-263">Load the data</span></span>
> * <span data-ttu-id="f2aa6-264">Uczenie modelu umożliwiającego przeprowadzenie wykrywania anomalii</span><span class="sxs-lookup"><span data-stu-id="f2aa6-264">Train the model for spike anomaly detection</span></span>
> * <span data-ttu-id="f2aa6-265">Wykrywaj anomalie wzrostu przy użyciu przeszkolonego modelu</span><span class="sxs-lookup"><span data-stu-id="f2aa6-265">Detect spike anomalies with the trained model</span></span>
> * <span data-ttu-id="f2aa6-266">Uczenie modelu wykrywania anomalii punktu zmiany</span><span class="sxs-lookup"><span data-stu-id="f2aa6-266">Train the model for change point anomaly detection</span></span>
> * <span data-ttu-id="f2aa6-267">Wykryj anomalie punktu zmiany w trybie przeszkolonym</span><span class="sxs-lookup"><span data-stu-id="f2aa6-267">Detect change point anomalies with the trained mode</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2aa6-268">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f2aa6-268">Next steps</span></span>

<span data-ttu-id="f2aa6-269">Zapoznaj się z repozytorium Machine Learning przykłady w witrynie GitHub, aby poznać przykład wykrywania anomalii dotyczącego zużycia mocy.</span><span class="sxs-lookup"><span data-stu-id="f2aa6-269">Check out the Machine Learning samples GitHub repository to explore a Power Consumption Anomaly Detection sample.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="f2aa6-270">dotnet/machinelearning — przykłady repozytorium GitHub</span><span class="sxs-lookup"><span data-stu-id="f2aa6-270">dotnet/machinelearning-samples GitHub repository</span></span>](https://github.com/dotnet/machinelearning-samples/tree/master/samples/csharp/getting-started/AnomalyDetection_PowerMeterReadings)
