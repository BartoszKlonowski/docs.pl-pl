---
title: 'Samouczek: wykrywanie anomalii w połączeniach telefonicznych'
description: Dowiedz się, jak utworzyć aplikację wykrywania anomalii dla danych szeregów czasowych. W tym samouczku przedstawiono tworzenie aplikacji konsolowej .NET Core przy użyciu języka C# w programie Visual Studio 2019.
ms.date: 12/04/2020
ms.topic: tutorial
ms.custom: mvc
ms.openlocfilehash: 69b617e760c1dd6a579c925168c92630756f92fc
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/16/2020
ms.locfileid: "97596616"
---
# <a name="tutorial-detect-anomalies-in-time-series-with-mlnet"></a><span data-ttu-id="26f7f-104">Samouczek: wykrywanie anomalii w szeregach czasowych przy użyciu ML.NET</span><span class="sxs-lookup"><span data-stu-id="26f7f-104">Tutorial: Detect anomalies in time series with ML.NET</span></span>

<span data-ttu-id="26f7f-105">Dowiedz się, jak utworzyć aplikację wykrywania anomalii dla danych szeregów czasowych.</span><span class="sxs-lookup"><span data-stu-id="26f7f-105">Learn how to build an anomaly detection application for time series data.</span></span> <span data-ttu-id="26f7f-106">W tym samouczku przedstawiono tworzenie aplikacji konsolowej .NET Core przy użyciu języka C# w programie Visual Studio 2019.</span><span class="sxs-lookup"><span data-stu-id="26f7f-106">This tutorial creates a .NET Core console application using C# in Visual Studio 2019.</span></span>

<span data-ttu-id="26f7f-107">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="26f7f-107">In this tutorial, you learn how to:</span></span>
> [!div class="checklist"]
>
> * <span data-ttu-id="26f7f-108">Ładowanie danych</span><span class="sxs-lookup"><span data-stu-id="26f7f-108">Load the data</span></span>
> * <span data-ttu-id="26f7f-109">Wykryj okres dla szeregu czasowego</span><span class="sxs-lookup"><span data-stu-id="26f7f-109">Detect period for a time series</span></span>
> * <span data-ttu-id="26f7f-110">Wykrywaj anomalie dla okresowych szeregów czasowych</span><span class="sxs-lookup"><span data-stu-id="26f7f-110">Detect anomaly for a periodical time series</span></span>

<span data-ttu-id="26f7f-111">Kod źródłowy dla tego samouczka można znaleźć w repozytorium [dotnet/Samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/ProductSalesAnomalyDetection) .</span><span class="sxs-lookup"><span data-stu-id="26f7f-111">You can find the source code for this tutorial at the [dotnet/samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/ProductSalesAnomalyDetection) repository.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26f7f-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="26f7f-112">Prerequisites</span></span>

* <span data-ttu-id="26f7f-113">[Program Visual Studio 2019 w wersji 16.7.8 lub nowszej](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) z zainstalowanym obciążeniem "Programowanie dla wielu platform" platformy .NET Core.</span><span class="sxs-lookup"><span data-stu-id="26f7f-113">[Visual Studio 2019 version 16.7.8 or later](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) with the ".NET Core cross-platform development" workload installed.</span></span>

* [<span data-ttu-id="26f7f-114">Zestaw danych phone-calls.csv</span><span class="sxs-lookup"><span data-stu-id="26f7f-114">The phone-calls.csv dataset</span></span>](https://raw.githubusercontent.com/dotnet/machinelearning-samples/master/samples/csharp/getting-started/AnomalyDetection_PhoneCalls/SrCnnDetection/Data/phone-calls.csv)

## <a name="create-a-console-application"></a><span data-ttu-id="26f7f-115">Tworzenie aplikacji konsolowej</span><span class="sxs-lookup"><span data-stu-id="26f7f-115">Create a console application</span></span>

1. <span data-ttu-id="26f7f-116">Utwórz **aplikację konsolową .NET Core** o nazwie "ProductSalesAnomalyDetection".</span><span class="sxs-lookup"><span data-stu-id="26f7f-116">Create a **C# .NET Core Console Application** called "ProductSalesAnomalyDetection".</span></span>

2. <span data-ttu-id="26f7f-117">Utwórz katalog o nazwie *dane* w projekcie, aby zapisać pliki zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="26f7f-117">Create a directory named *Data* in your project to save your data set files.</span></span>

3. <span data-ttu-id="26f7f-118">Zainstaluj **pakiet NuGet Microsoft.ml**:</span><span class="sxs-lookup"><span data-stu-id="26f7f-118">Install the **Microsoft.ML NuGet Package**:</span></span>

    [!INCLUDE [mlnet-current-nuget-version](../../../includes/mlnet-current-nuget-version.md)]

    <span data-ttu-id="26f7f-119">W Eksplorator rozwiązań kliknij prawym przyciskiem myszy projekt i wybierz polecenie **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="26f7f-119">In Solution Explorer, right-click on your project and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="26f7f-120">Wybierz pozycję "nuget.org" jako źródło pakietu, wybierz kartę Przeglądaj, Wyszukaj pozycję **Microsoft.ml** i wybierz przycisk **Instaluj** .</span><span class="sxs-lookup"><span data-stu-id="26f7f-120">Choose "nuget.org" as the Package source, select the Browse tab, search for **Microsoft.ML** and select the **Install** button.</span></span> <span data-ttu-id="26f7f-121">Wybierz przycisk **OK** w oknie dialogowym **Podgląd zmian** , a następnie **Wybierz przycisk** Akceptuję w oknie dialogowym **akceptacji licencji** , jeśli zgadzasz się z postanowieniami licencyjnymi dotyczącymi wymienionych pakietów.</span><span class="sxs-lookup"><span data-stu-id="26f7f-121">Select the **OK** button on the **Preview Changes** dialog and then select the **I Accept** button on the **License Acceptance** dialog if you agree with the license terms for the packages listed.</span></span> <span data-ttu-id="26f7f-122">Powtórz te kroki dla **Microsoft. ml. szeregów czasowych**.</span><span class="sxs-lookup"><span data-stu-id="26f7f-122">Repeat these steps for **Microsoft.ML.TimeSeries**.</span></span>

4. <span data-ttu-id="26f7f-123">Dodaj następujące `using` instrukcje w górnej części pliku *program.cs* :</span><span class="sxs-lookup"><span data-stu-id="26f7f-123">Add the following `using` statements at the top of your *Program.cs* file:</span></span>

    [!code-csharp[AddUsings](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#AddUsings "Add necessary usings")]

### <a name="download-your-data"></a><span data-ttu-id="26f7f-124">Pobierz swoje dane</span><span class="sxs-lookup"><span data-stu-id="26f7f-124">Download your data</span></span>

1. <span data-ttu-id="26f7f-125">Pobierz zestaw danych i Zapisz go w utworzonym wcześniej folderze *danych* :</span><span class="sxs-lookup"><span data-stu-id="26f7f-125">Download the dataset and save it to the *Data* folder you previously created:</span></span>

    <span data-ttu-id="26f7f-126">Kliknij prawym przyciskiem myszy [*phone-calls.csv*](https://raw.githubusercontent.com/dotnet/machinelearning-samples/master/samples/csharp/getting-started/AnomalyDetection_PhoneCalls/SrCnnDetection/Data/phone-calls.csv) i wybierz pozycję "Zapisz link (lub cel) jako..."</span><span class="sxs-lookup"><span data-stu-id="26f7f-126">Right click on [*phone-calls.csv*](https://raw.githubusercontent.com/dotnet/machinelearning-samples/master/samples/csharp/getting-started/AnomalyDetection_PhoneCalls/SrCnnDetection/Data/phone-calls.csv) and select "Save Link (or Target) As..."</span></span>

     <span data-ttu-id="26f7f-127">Upewnij się, że plik CSV został zapisany w \* folderze *dane* lub po jego zapisaniu w innym miejscu Przenieś \* plik CSV do folderu *dane* .</span><span class="sxs-lookup"><span data-stu-id="26f7f-127">Make sure you either save the \*.csv file to the *Data* folder, or after you save it elsewhere, move the \*.csv file to the *Data* folder.</span></span>

2. <span data-ttu-id="26f7f-128">W Eksplorator rozwiązań kliknij prawym przyciskiem myszy \* plik CSV i wybierz polecenie **Właściwości**.</span><span class="sxs-lookup"><span data-stu-id="26f7f-128">In Solution Explorer, right-click the \*.csv file and select **Properties**.</span></span> <span data-ttu-id="26f7f-129">W obszarze **Zaawansowane** Zmień wartość opcji **Kopiuj do katalogu wyjściowego** na Kopiuj, **jeśli nowszy**.</span><span class="sxs-lookup"><span data-stu-id="26f7f-129">Under **Advanced**, change the value of **Copy to Output Directory** to **Copy if newer**.</span></span>

<span data-ttu-id="26f7f-130">Poniższa tabela zawiera podgląd danych z \* pliku CSV:</span><span class="sxs-lookup"><span data-stu-id="26f7f-130">The following table is a data preview from your \*.csv file:</span></span>

| <span data-ttu-id="26f7f-131">sygnatura czasowa</span><span class="sxs-lookup"><span data-stu-id="26f7f-131">timestamp</span></span>  | <span data-ttu-id="26f7f-132">wartość</span><span class="sxs-lookup"><span data-stu-id="26f7f-132">value</span></span> |
|--------|--------------|
| <span data-ttu-id="26f7f-133">2018/9/3</span><span class="sxs-lookup"><span data-stu-id="26f7f-133">2018/9/3</span></span>  | <span data-ttu-id="26f7f-134">36,69670857</span><span class="sxs-lookup"><span data-stu-id="26f7f-134">36.69670857</span></span>  |
| <span data-ttu-id="26f7f-135">2018/9/4</span><span class="sxs-lookup"><span data-stu-id="26f7f-135">2018/9/4</span></span>  | <span data-ttu-id="26f7f-136">35,74160571</span><span class="sxs-lookup"><span data-stu-id="26f7f-136">35.74160571</span></span>  |
| <span data-ttu-id="26f7f-137">.....</span><span class="sxs-lookup"><span data-stu-id="26f7f-137">.....</span></span>  | <span data-ttu-id="26f7f-138">.....</span><span class="sxs-lookup"><span data-stu-id="26f7f-138">.....</span></span>  |
| <span data-ttu-id="26f7f-139">2018/10/3</span><span class="sxs-lookup"><span data-stu-id="26f7f-139">2018/10/3</span></span>  | <span data-ttu-id="26f7f-140">34,49893429</span><span class="sxs-lookup"><span data-stu-id="26f7f-140">34.49893429</span></span>  |
| <span data-ttu-id="26f7f-141">...</span><span class="sxs-lookup"><span data-stu-id="26f7f-141">...</span></span>    | <span data-ttu-id="26f7f-142">....</span><span class="sxs-lookup"><span data-stu-id="26f7f-142">....</span></span>   |

<span data-ttu-id="26f7f-143">Ten plik reprezentuje serię czasową.</span><span class="sxs-lookup"><span data-stu-id="26f7f-143">This file represents a time-series.</span></span> <span data-ttu-id="26f7f-144">Każdy wiersz w pliku jest punktem danych.</span><span class="sxs-lookup"><span data-stu-id="26f7f-144">Each row in the file is a data point.</span></span> <span data-ttu-id="26f7f-145">Każdy Piont danych ma dwa atrybuty, a mianowicie, `timestamp` i `value` , aby reprensent liczbę połączeń telefonicznych w każdym dniu.</span><span class="sxs-lookup"><span data-stu-id="26f7f-145">Each data piont has two attributes, namely, `timestamp` and `value`, to reprensent the number of phone calls at each day.</span></span> <span data-ttu-id="26f7f-146">Liczba połączeń telefonicznych jest przekształcana w celu cofnięcia czułości.</span><span class="sxs-lookup"><span data-stu-id="26f7f-146">The number of phone calls is transformed to de-sensitivity.</span></span>

### <a name="create-classes-and-define-paths"></a><span data-ttu-id="26f7f-147">Tworzenie klas i Definiowanie ścieżek</span><span class="sxs-lookup"><span data-stu-id="26f7f-147">Create classes and define paths</span></span>

<span data-ttu-id="26f7f-148">Następnie zdefiniuj struktury danych dla klas wejściowych i prognoz.</span><span class="sxs-lookup"><span data-stu-id="26f7f-148">Next, define your input and prediction class data structures.</span></span>

<span data-ttu-id="26f7f-149">Dodaj nową klasę do projektu:</span><span class="sxs-lookup"><span data-stu-id="26f7f-149">Add a new class to your project:</span></span>

1. <span data-ttu-id="26f7f-150">W **Eksplorator rozwiązań** kliknij prawym przyciskiem myszy projekt, a następnie wybierz pozycję **Dodaj > nowy element**.</span><span class="sxs-lookup"><span data-stu-id="26f7f-150">In **Solution Explorer**, right-click the project, and then select **Add > New Item**.</span></span>

2. <span data-ttu-id="26f7f-151">W **oknie dialogowym Dodaj nowy element** wybierz pozycję **Klasa** i zmień wartość pola **Nazwa** na *PhoneCallsData.cs*.</span><span class="sxs-lookup"><span data-stu-id="26f7f-151">In the **Add New Item dialog box**, select **Class** and change the **Name** field to *PhoneCallsData.cs*.</span></span> <span data-ttu-id="26f7f-152">Następnie wybierz przycisk **Dodaj** .</span><span class="sxs-lookup"><span data-stu-id="26f7f-152">Then, select the **Add** button.</span></span>

   <span data-ttu-id="26f7f-153">Plik *PhoneCallsData.cs* zostanie otwarty w edytorze kodu.</span><span class="sxs-lookup"><span data-stu-id="26f7f-153">The *PhoneCallsData.cs* file opens in the code editor.</span></span>

3. <span data-ttu-id="26f7f-154">Dodaj następującą `using` instrukcję na początku *PhoneCallsData.cs*:</span><span class="sxs-lookup"><span data-stu-id="26f7f-154">Add the following `using` statement to the top of *PhoneCallsData.cs*:</span></span>

   ```csharp
   using Microsoft.ML.Data;
   ```

4. <span data-ttu-id="26f7f-155">Usuń istniejącą definicję klasy i Dodaj następujący kod, który ma dwie klasy `PhoneCallsData` i `PhoneCallsPrediction` , do pliku *PhoneCallsData.cs* :</span><span class="sxs-lookup"><span data-stu-id="26f7f-155">Remove the existing class definition and add the following code, which has two classes `PhoneCallsData` and `PhoneCallsPrediction`, to the *PhoneCallsData.cs* file:</span></span>

    [!code-csharp[DeclareTypes](./snippets/phone-calls-anomaly-detection/csharp/PhoneCallsData.cs#DeclareTypes "Declare data record types")]

    <span data-ttu-id="26f7f-156">`PhoneCallsData` Określa klasę danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="26f7f-156">`PhoneCallsData` specifies an input data class.</span></span> <span data-ttu-id="26f7f-157">Atrybut [LoadColumn](xref:Microsoft.ML.Data.LoadColumnAttribute.%23ctor%28System.Int32%29) określa, które kolumny (według indeksu kolumn) w zestawie danych powinny zostać załadowane.</span><span class="sxs-lookup"><span data-stu-id="26f7f-157">The [LoadColumn](xref:Microsoft.ML.Data.LoadColumnAttribute.%23ctor%28System.Int32%29) attribute specifies which columns (by column index) in the dataset should be loaded.</span></span> <span data-ttu-id="26f7f-158">Ma dwa atrybuty, `timestamp` `value` które są zgodne z tymi samymi atrybutami w pliku danych.</span><span class="sxs-lookup"><span data-stu-id="26f7f-158">It has two attributes `timestamp` and `value` that correspond to the same attributes in the data file.</span></span>

    <span data-ttu-id="26f7f-159">`PhoneCallsPrediction` Określa klasę danych przewidywania.</span><span class="sxs-lookup"><span data-stu-id="26f7f-159">`PhoneCallsPrediction` specifies the prediction data class.</span></span> <span data-ttu-id="26f7f-160">W przypadku detektora SR-CNN funkcja przewidywania zależy od określonego [trybu wykrywania](xref:Microsoft.ML.TimeSeries.SrCnnDetectMode) .</span><span class="sxs-lookup"><span data-stu-id="26f7f-160">For SR-CNN detector, the prediction depends on the [detect mode](xref:Microsoft.ML.TimeSeries.SrCnnDetectMode) specified.</span></span> <span data-ttu-id="26f7f-161">W tym przykładzie wybieramy `AnomalyAndMargin` tryb.</span><span class="sxs-lookup"><span data-stu-id="26f7f-161">In this sample we select the `AnomalyAndMargin` mode.</span></span> <span data-ttu-id="26f7f-162">Dane wyjściowe zawierają siedem kolumn.</span><span class="sxs-lookup"><span data-stu-id="26f7f-162">The output contains seven columns.</span></span> <span data-ttu-id="26f7f-163">W większości przypadków, `IsAnomaly` , `ExpectedValue` `UpperBoundary` i `LowerBoundary` są wystarczająco aktualne.</span><span class="sxs-lookup"><span data-stu-id="26f7f-163">In most cases, `IsAnomaly`, `ExpectedValue`, `UpperBoundary` and `LowerBoundary` are informative enough.</span></span> <span data-ttu-id="26f7f-164">Informują o tym, że punkt jest anomalią, oczekiwaną wartością punktu i dolną/górną granicę obszaru.</span><span class="sxs-lookup"><span data-stu-id="26f7f-164">They tell you if a point is an anomaly, the expected value of the point and the lower / upper boundary region of the point.</span></span>

5. <span data-ttu-id="26f7f-165">Dodaj następujący kod do wiersza bezpośrednio powyżej `Main` metody, aby określić ścieżkę do pliku danych:</span><span class="sxs-lookup"><span data-stu-id="26f7f-165">Add the following code to the line right above the `Main` method to specify the path to your data file:</span></span>

    [!code-csharp[Declare global variables](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#DeclareGlobalVariables "Declare global variables")]

### <a name="initialize-variables-in-main"></a><span data-ttu-id="26f7f-166">Inicjuj zmienne w głównym</span><span class="sxs-lookup"><span data-stu-id="26f7f-166">Initialize variables in Main</span></span>

1. <span data-ttu-id="26f7f-167">Zastąp `Console.WriteLine("Hello World!")` wiersz w `Main` metodzie poniższym kodem, aby zadeklarować i zainicjować `mlContext` zmienną:</span><span class="sxs-lookup"><span data-stu-id="26f7f-167">Replace the `Console.WriteLine("Hello World!")` line in the `Main` method with the following code to declare and initialize the `mlContext` variable:</span></span>

    [!code-csharp[CreateMLContext](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#CreateMLContext "Create the ML Context")]

    <span data-ttu-id="26f7f-168">[Klasa MLContext](xref:Microsoft.ML.MLContext) jest punktem początkowym dla wszystkich operacji ml.NET, a inicjowanie `mlContext` tworzy nowe środowisko ml.NET, które może być współużytkowane przez obiekty przepływu pracy tworzenia modelu.</span><span class="sxs-lookup"><span data-stu-id="26f7f-168">The [MLContext class](xref:Microsoft.ML.MLContext) is a starting point for all ML.NET operations, and initializing `mlContext` creates a new ML.NET environment that can be shared across the model creation workflow objects.</span></span> <span data-ttu-id="26f7f-169">Jest to podobne, pojęciowo do `DBContext` w Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="26f7f-169">It's similar, conceptually, to `DBContext` in Entity Framework.</span></span>

### <a name="load-the-data"></a><span data-ttu-id="26f7f-170">Ładowanie danych</span><span class="sxs-lookup"><span data-stu-id="26f7f-170">Load the data</span></span>

<span data-ttu-id="26f7f-171">Dane w ML.NET są reprezentowane jako [Klasa IDataView](xref:Microsoft.ML.IDataView).</span><span class="sxs-lookup"><span data-stu-id="26f7f-171">Data in ML.NET is represented as an [IDataView class](xref:Microsoft.ML.IDataView).</span></span> <span data-ttu-id="26f7f-172">`IDataView` to elastyczny i wydajny sposób opisywania danych tabelarycznych (liczbowych i tekstowych).</span><span class="sxs-lookup"><span data-stu-id="26f7f-172">`IDataView` is a flexible, efficient way of describing tabular data (numeric and text).</span></span> <span data-ttu-id="26f7f-173">Dane można ładować z pliku tekstowego lub z innych źródeł (na przykład bazy danych SQL lub plików dziennika) do `IDataView` obiektu.</span><span class="sxs-lookup"><span data-stu-id="26f7f-173">Data can be loaded from a text file or from other sources (for example, SQL database or log files) to an `IDataView` object.</span></span>

1. <span data-ttu-id="26f7f-174">Dodaj następujący kod w następnym wierszu `Main` metody:</span><span class="sxs-lookup"><span data-stu-id="26f7f-174">Add the following code as the next line of the `Main` method:</span></span>

    [!code-csharp[LoadData](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#LoadData "loading dataset")]

    <span data-ttu-id="26f7f-175">[LoadFromTextFile ()](xref:Microsoft.ML.TextLoaderSaverCatalog.LoadFromTextFile%60%601%28Microsoft.ML.DataOperationsCatalog,System.String,System.Char,System.Boolean,System.Boolean,System.Boolean,System.Boolean%29) definiuje schemat danych i odczytuje w pliku.</span><span class="sxs-lookup"><span data-stu-id="26f7f-175">The [LoadFromTextFile()](xref:Microsoft.ML.TextLoaderSaverCatalog.LoadFromTextFile%60%601%28Microsoft.ML.DataOperationsCatalog,System.String,System.Char,System.Boolean,System.Boolean,System.Boolean,System.Boolean%29) defines the data schema and reads in the file.</span></span> <span data-ttu-id="26f7f-176">Przyjmuje zmienne ścieżki danych i zwraca `IDataView` .</span><span class="sxs-lookup"><span data-stu-id="26f7f-176">It takes in the data path variables and returns an `IDataView`.</span></span>

## <a name="time-series-anomaly-detection"></a><span data-ttu-id="26f7f-177">Wykrywanie anomalii szeregów czasowych</span><span class="sxs-lookup"><span data-stu-id="26f7f-177">Time series anomaly detection</span></span>

<span data-ttu-id="26f7f-178">Wykrywanie anomalii szeregów czasowych to proces wykrywania odstających danych szeregów czasowych; wskazuje na dane wejściowe serie czasowe, w których zachowanie nie jest oczekiwane, lub "brzmienia".</span><span class="sxs-lookup"><span data-stu-id="26f7f-178">Time series anomaly detection is the process of detecting time-series data outliers; points on a given input time-series where the behavior isn't what was expected, or "weird".</span></span> <span data-ttu-id="26f7f-179">Te anomalie zwykle wskazują na niektóre zdarzenia interesujące w domenie problemu: atak cybernetycznymi na kontach użytkowników, awarię i RPS pliku na serwerze, przeciek pamięci itp.</span><span class="sxs-lookup"><span data-stu-id="26f7f-179">These anomalies are typically indicative of some events of interest in the problem domain: a cyber-attack on user accounts, power outage, bursting RPS on a server, memory leak, etc.</span></span>

<span data-ttu-id="26f7f-180">Aby znaleźć anomalię w szeregach czasowych, należy najpierw określić okres serii.</span><span class="sxs-lookup"><span data-stu-id="26f7f-180">To find anomaly on time series, you should first determine the period of the series.</span></span> <span data-ttu-id="26f7f-181">Następnie Serie czasowe mogą być rozłożone na kilka składników jako `Y = T + S + R` , gdzie `Y` jest oryginalną serią, `T` to składnik trendu, to `S` sezonowy componnent i `R` jest składnikiem końcowym serii.</span><span class="sxs-lookup"><span data-stu-id="26f7f-181">Then, the time series can be decomposed into several components as `Y = T + S + R`, where `Y` is the original series, `T` is the trend component, `S` is the seasonal componnent and `R` is the residual component of the series.</span></span> <span data-ttu-id="26f7f-182">Ten krok jest nazywany [dekompozycją](https://en.wikipedia.org/wiki/Decomposition_of_time_series).</span><span class="sxs-lookup"><span data-stu-id="26f7f-182">This step is called [decomposition](https://en.wikipedia.org/wiki/Decomposition_of_time_series).</span></span> <span data-ttu-id="26f7f-183">Na koniec wykrywanie jest wykonywane na składniku końcowym, aby znaleźć anomalie.</span><span class="sxs-lookup"><span data-stu-id="26f7f-183">Finally, detection is performed on the residual component to find the anomalies.</span></span> <span data-ttu-id="26f7f-184">W ML.NET algorytm SR-CNN jest zaawansowanym i szczegółowym algorytmem opartym na widmie pozostałej (SR) i Splotowych neuronowych Network (CNN) w celu wykrycia anomalii w szeregach czasowych (zapoznaj się z [usługą wykrywania anomalii szeregów czasowych w dokumencie firmy Microsoft](https://arxiv.org/pdf/1906.03821.pdf) , aby uzyskać więcej informacji na temat tego algorytmu).</span><span class="sxs-lookup"><span data-stu-id="26f7f-184">In ML.NET, The SR-CNN algorithm is an advanced and novel algorithm that is based on Spectral Residual (SR) and Convolutional Neural Network(CNN) to detect anomaly on time-series( Refer to the [Time-Series Anomaly Detection Service at Microsoft](https://arxiv.org/pdf/1906.03821.pdf) paper for more details on this algorithm).</span></span>

<span data-ttu-id="26f7f-185">W tym samouczku zobaczysz, że te procedury można wykonać przy użyciu dwóch funkcji.</span><span class="sxs-lookup"><span data-stu-id="26f7f-185">In this tutorial, you will see that these procedures can be completed using two functions.</span></span>

## <a name="detect-period"></a><span data-ttu-id="26f7f-186">Wykryj okres</span><span class="sxs-lookup"><span data-stu-id="26f7f-186">Detect Period</span></span>

<span data-ttu-id="26f7f-187">W pierwszym kroku wywołujemy `DetectSeasonality` funkcję w celu określenia okresu serii.</span><span class="sxs-lookup"><span data-stu-id="26f7f-187">In the first step, we invoke the `DetectSeasonality` function to determine the period of the series.</span></span>

### <a name="create-the-detectperiod-method"></a><span data-ttu-id="26f7f-188">Tworzenie metody DetectPeriod</span><span class="sxs-lookup"><span data-stu-id="26f7f-188">Create the DetectPeriod method</span></span>

1. <span data-ttu-id="26f7f-189">Utwórz `DetectPeriod` metodę, tuż poniżej `Main` metody, przy użyciu następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="26f7f-189">Create the `DetectPeriod` method, just below the `Main` method, using the following code:</span></span>

    ```csharp
    static void DetectPeriod(MLContext mlContext, IDataView phoneCalls)
    {

    }
    ```

2. <span data-ttu-id="26f7f-190">Użyj funkcji [DetectSeasonality](xref:Microsoft.ML.TimeSeriesCatalog.DetectSeasonality) , aby wykryć okres.</span><span class="sxs-lookup"><span data-stu-id="26f7f-190">Use the [DetectSeasonality](xref:Microsoft.ML.TimeSeriesCatalog.DetectSeasonality) function to detect period.</span></span> <span data-ttu-id="26f7f-191">Dodaj go do `DetectPeriod` metody przy użyciu następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="26f7f-191">Add it to the `DetectPeriod` method with the following code:</span></span>

    [!code-csharp[DetectSeasonality](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#DetectSeasonality)]

3. <span data-ttu-id="26f7f-192">Wyświetl wartość okresu, dodając następujący kod jako następny wiersz kodu w `DetectPeriod` metodzie:</span><span class="sxs-lookup"><span data-stu-id="26f7f-192">Display the period value by adding the following as the next line of code in the `DetectPeriod` method:</span></span>

    [!code-csharp[DisplayPeriod](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#DisplayPeriod)]

4. <span data-ttu-id="26f7f-193">Dodaj następujące wywołanie do `DetectPeriod` metody w `Main` metodzie:</span><span class="sxs-lookup"><span data-stu-id="26f7f-193">Add the following call to the `DetectPeriod` method in the `Main` method:</span></span>

    [!code-csharp[CallDetectPeriod](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#CallDetectPeriod)]

### <a name="period-detection-results"></a><span data-ttu-id="26f7f-194">Wyniki wykrywania okresu</span><span class="sxs-lookup"><span data-stu-id="26f7f-194">Period detection results</span></span>

<span data-ttu-id="26f7f-195">Uruchom aplikację.</span><span class="sxs-lookup"><span data-stu-id="26f7f-195">Run the application.</span></span> <span data-ttu-id="26f7f-196">Wyniki powinny wyglądać podobnie do poniższego.</span><span class="sxs-lookup"><span data-stu-id="26f7f-196">Your results should be similar to the following.</span></span>

```console
Period of the series is: 7.
```

## <a name="detect-anomaly"></a><span data-ttu-id="26f7f-197">Wykrywanie anomalii</span><span class="sxs-lookup"><span data-stu-id="26f7f-197">Detect Anomaly</span></span>

<span data-ttu-id="26f7f-198">W tym kroku użyjesz, [`SrCnnEntireDetector`](xref:Microsoft.ML.Transforms.TimeSeries.SrCnnEntireAnomalyDetector) Aby znaleźć anomalie.</span><span class="sxs-lookup"><span data-stu-id="26f7f-198">In this step, you use the [`SrCnnEntireDetector`](xref:Microsoft.ML.Transforms.TimeSeries.SrCnnEntireAnomalyDetector) to find anomalies.</span></span>

### <a name="create-the-detectanomaly-method"></a><span data-ttu-id="26f7f-199">Tworzenie metody DetectAnomaly</span><span class="sxs-lookup"><span data-stu-id="26f7f-199">Create the DetectAnomaly method</span></span>

1. <span data-ttu-id="26f7f-200">Utwórz `DetectAnomaly` metodę, tuż poniżej `DetectPeriod` metody, przy użyciu następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="26f7f-200">Create the `DetectAnomaly` method, just below the `DetectPeriod` method, using the following code:</span></span>

    ```csharp
    static void DetectAnomaly(MLContext mlContext, IDataView phoneCalls, int period)
    {

    }
    ```

2. <span data-ttu-id="26f7f-201">Skonfiguruj [SrCnnEntireAnomalyDetectorOptions](xref:Microsoft.ML.Transforms.TimeSeries.SrCnnEntireAnomalyDetectorOptions) w `DetectAnomaly` metodzie przy użyciu następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="26f7f-201">Setup [SrCnnEntireAnomalyDetectorOptions](xref:Microsoft.ML.Transforms.TimeSeries.SrCnnEntireAnomalyDetectorOptions) in the `DetectAnomaly` method with the following code:</span></span>

    [!code-csharp[SetupSrCnnParameters](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#SetupSrCnnParameters)]

3. <span data-ttu-id="26f7f-202">Wykryj anomalię przez algorytm SR-CNN, dodając następujący wiersz kodu do `DetectAnomaly` metody:</span><span class="sxs-lookup"><span data-stu-id="26f7f-202">Detect anomaly by SR-CNN algorithm by adding the following line of code in the `DetectAnomaly` method:</span></span>

    [!code-csharp[DetectAnomaly](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#DetectAnomaly)]

4. <span data-ttu-id="26f7f-203">Konwertuj widok danych wyjściowych na silnie wpisaną, `IEnumerable` Aby ułatwić wyświetlanie przy użyciu [`CreateEnumerable`](xref:Microsoft.ML.DataOperationsCatalog.CreateEnumerable%2A) metody z następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="26f7f-203">Convert the output data view into a strongly typed `IEnumerable` for easier display using the [`CreateEnumerable`](xref:Microsoft.ML.DataOperationsCatalog.CreateEnumerable%2A) method with the following code:</span></span>

    [!code-csharp[CreateEnumerableForResult](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#CreateEnumerableForResult)]

5. <span data-ttu-id="26f7f-204">Utwórz nagłówek wyświetlania z następującym kodem jako następnym wierszem w `DetectAnomaly` metodzie:</span><span class="sxs-lookup"><span data-stu-id="26f7f-204">Create a display header with the following code as the next line in the `DetectAnomaly` method:</span></span>

    [!code-csharp[DisplayHeader](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#DisplayHeader)]

    <span data-ttu-id="26f7f-205">W wynikach wykrywania punktu zmiany zostaną wyświetlone następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="26f7f-205">You'll display the following information in your change point detection results:</span></span>

    * <span data-ttu-id="26f7f-206">`Index` jest indeksem każdego punktu.</span><span class="sxs-lookup"><span data-stu-id="26f7f-206">`Index` is the index of each point.</span></span>
    * <span data-ttu-id="26f7f-207">`Anomaly` jest wskaźnikiem wheather każdy punkt jest wykrywany jako anomalia.</span><span class="sxs-lookup"><span data-stu-id="26f7f-207">`Anomaly` is the indicator of wheather each point is detected as anomaly.</span></span>
    * <span data-ttu-id="26f7f-208">`ExpectedValue` to Szacowana wartość każdego punktu.</span><span class="sxs-lookup"><span data-stu-id="26f7f-208">`ExpectedValue` is the estimated value of each point.</span></span>
    * <span data-ttu-id="26f7f-209">`LowerBoundary` to najniższa wartość, którą każdy punkt może być nieanomalią.</span><span class="sxs-lookup"><span data-stu-id="26f7f-209">`LowerBoundary` is the lowest value each point can be to be not anomaly.</span></span>
    * <span data-ttu-id="26f7f-210">`UpperBoundary` jest największą wartością, którą każdy punkt może być nieanomalią.</span><span class="sxs-lookup"><span data-stu-id="26f7f-210">`UpperBoundary` is the highest value each point can be to be not anomaly.</span></span>

6. <span data-ttu-id="26f7f-211">Wykonaj iterację `predictions` `IEnumerable` i Wyświetl wyniki przy użyciu następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="26f7f-211">Iterate through the `predictions` `IEnumerable` and display the results with the following code:</span></span>

    [!code-csharp[DisplayAnomalyDetectionResults](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#DisplayAnomalyDetectionResults)]

7. <span data-ttu-id="26f7f-212">Dodaj następujące wywołanie do `DetectAnomaly` metody w `Main` metodzie:</span><span class="sxs-lookup"><span data-stu-id="26f7f-212">Add the following call to the `DetectAnomaly` method in the `Main` method:</span></span>

    [!code-csharp[CallDetectAnomaly](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#CallDetectAnomaly)]

## <a name="anomaly-detection-results"></a><span data-ttu-id="26f7f-213">Wyniki wykrywania anomalii</span><span class="sxs-lookup"><span data-stu-id="26f7f-213">Anomaly detection results</span></span>

<span data-ttu-id="26f7f-214">Uruchom aplikację.</span><span class="sxs-lookup"><span data-stu-id="26f7f-214">Run the application.</span></span> <span data-ttu-id="26f7f-215">Wyniki powinny wyglądać podobnie do poniższego.</span><span class="sxs-lookup"><span data-stu-id="26f7f-215">Your results should be similar to the following.</span></span> <span data-ttu-id="26f7f-216">Podczas przetwarzania wyświetlane są komunikaty.</span><span class="sxs-lookup"><span data-stu-id="26f7f-216">During processing, messages are displayed.</span></span> <span data-ttu-id="26f7f-217">Mogą pojawić się ostrzeżenia lub przetwarzanie komunikatów.</span><span class="sxs-lookup"><span data-stu-id="26f7f-217">You may see warnings, or processing messages.</span></span> <span data-ttu-id="26f7f-218">Niektóre komunikaty zostały usunięte z następujących wyników dla przejrzystości.</span><span class="sxs-lookup"><span data-stu-id="26f7f-218">Some messages have been removed from the following results for clarity.</span></span>

```console
Detect period of the series
Period of the series is: 7.
Detect anomaly points in the series
Index   Data    Anomaly AnomalyScore    Mag     ExpectedValue   BoundaryUnit    UpperBoundary   LowerBoundary
0,0,36.841787256739266,41.14206982401966,32.541504689458876
1,0,35.67303618137362,39.97331874865401,31.372753614093227
2,0,34.710132999891826,39.029491313022824,30.390774686760828
3,0,33.44765248883495,37.786086547816545,29.10921842985335
4,0,28.937110922276364,33.25646923540736,24.61775260914537
5,0,5.143895892785781,9.444178460066171,0.843613325505391
6,0,5.163325228419392,9.463607795699783,0.8630426611390014
7,0,36.76414836240396,41.06443092968435,32.46386579512357
8,0,35.77908590657007,40.07936847385046,31.478803339289676
9,0,34.547259536635245,38.847542103915636,30.246976969354854
10,0,33.55193524820608,37.871293561337076,29.23257693507508
11,0,29.091800129624648,33.392082696905035,24.79151756234426
12,0,5.154836630338823,9.455119197619213,0.8545540630584334
13,0,5.234332502492464,9.534615069772855,0.934049935212073
14,0,36.54992549471526,40.85020806199565,32.24964292743487
15,0,35.79526470980883,40.095547277089224,31.494982142528443
16,0,34.34099013096804,38.64127269824843,30.040707563687647
17,0,33.61201516582131,37.9122977331017,29.31173259854092
18,0,29.223563320561812,33.5238458878422,24.923280753281425
19,0,5.170512168851533,9.470794736131923,0.8702296015711433
20,0,5.2614938889462834,9.561776456226674,0.9612113216658926
21,0,36.37103858487317,40.67132115215356,32.07075601759278
22,0,35.813544599026855,40.113827166307246,31.513262031746464
23,0,34.05600492733225,38.356287494612644,29.755722360051863
24,0,33.65828319077884,37.95856575805923,29.358000623498448
25,0,29.381125690882463,33.681408258162854,25.080843123602072
26,0,5.261543539820418,9.561826107100808,0.9612609725400283
27,0,5.4873712582971805,9.787653825577571,1.1870886910167897
28,1,36.504694001629254,40.804976568909645,32.20441143434886  <-- alert is on, detecte anomaly
...
```

<span data-ttu-id="26f7f-219">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="26f7f-219">Congratulations!</span></span> <span data-ttu-id="26f7f-220">Pomyślnie skompilowano modele uczenia maszynowego na potrzeby wykrywania okresu i anomalii w seriach okresowych.</span><span class="sxs-lookup"><span data-stu-id="26f7f-220">You've now successfully built machine learning models for detecting period and anomaly on a periodical series.</span></span>

<span data-ttu-id="26f7f-221">Kod źródłowy dla tego samouczka można znaleźć w repozytorium [dotnet/Samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/PhoneCallsAnomalyDetection) .</span><span class="sxs-lookup"><span data-stu-id="26f7f-221">You can find the source code for this tutorial at the [dotnet/samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/PhoneCallsAnomalyDetection) repository.</span></span>

<span data-ttu-id="26f7f-222">W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="26f7f-222">In this tutorial, you learned how to:</span></span>
> [!div class="checklist"]
>
> * <span data-ttu-id="26f7f-223">Ładowanie danych</span><span class="sxs-lookup"><span data-stu-id="26f7f-223">Load the data</span></span>
> * <span data-ttu-id="26f7f-224">Wykryj okres w danych szeregów czasowych</span><span class="sxs-lookup"><span data-stu-id="26f7f-224">Detect period on the time series data</span></span>
> * <span data-ttu-id="26f7f-225">Wykrywanie anomalii w danych szeregów czasowych</span><span class="sxs-lookup"><span data-stu-id="26f7f-225">Detect anomaly on the time series data</span></span>

## <a name="next-steps"></a><span data-ttu-id="26f7f-226">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="26f7f-226">Next steps</span></span>

<span data-ttu-id="26f7f-227">Zapoznaj się z repozytorium Machine Learning przykłady w witrynie GitHub, aby poznać przykład wykrywania anomalii dotyczącego zużycia mocy.</span><span class="sxs-lookup"><span data-stu-id="26f7f-227">Check out the Machine Learning samples GitHub repository to explore a Power Consumption Anomaly Detection sample.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="26f7f-228">dotnet/machinelearning — przykłady repozytorium GitHub</span><span class="sxs-lookup"><span data-stu-id="26f7f-228">dotnet/machinelearning-samples GitHub repository</span></span>](https://github.com/dotnet/machinelearning-samples/tree/master/samples/csharp/getting-started/AnomalyDetection_PowerMeterReadings)
