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
# <a name="tutorial-detect-anomalies-in-time-series-with-mlnet"></a>Samouczek: wykrywanie anomalii w szeregach czasowych przy użyciu ML.NET

Dowiedz się, jak utworzyć aplikację wykrywania anomalii dla danych szeregów czasowych. W tym samouczku przedstawiono tworzenie aplikacji konsolowej .NET Core przy użyciu języka C# w programie Visual Studio 2019.

Ten samouczek zawiera informacje na temat wykonywania następujących czynności:
> [!div class="checklist"]
>
> * Ładowanie danych
> * Wykryj okres dla szeregu czasowego
> * Wykrywaj anomalie dla okresowych szeregów czasowych

Kod źródłowy dla tego samouczka można znaleźć w repozytorium [dotnet/Samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/ProductSalesAnomalyDetection) .

## <a name="prerequisites"></a>Wymagania wstępne

* [Program Visual Studio 2019 w wersji 16.7.8 lub nowszej](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) z zainstalowanym obciążeniem "Programowanie dla wielu platform" platformy .NET Core.

* [Zestaw danych phone-calls.csv](https://raw.githubusercontent.com/dotnet/machinelearning-samples/master/samples/csharp/getting-started/AnomalyDetection_PhoneCalls/SrCnnDetection/Data/phone-calls.csv)

## <a name="create-a-console-application"></a>Tworzenie aplikacji konsolowej

1. Utwórz **aplikację konsolową .NET Core** o nazwie "ProductSalesAnomalyDetection".

2. Utwórz katalog o nazwie *dane* w projekcie, aby zapisać pliki zestawu danych.

3. Zainstaluj **pakiet NuGet Microsoft.ml**:

    [!INCLUDE [mlnet-current-nuget-version](../../../includes/mlnet-current-nuget-version.md)]

    W Eksplorator rozwiązań kliknij prawym przyciskiem myszy projekt i wybierz polecenie **Zarządzaj pakietami NuGet**. Wybierz pozycję "nuget.org" jako źródło pakietu, wybierz kartę Przeglądaj, Wyszukaj pozycję **Microsoft.ml** i wybierz przycisk **Instaluj** . Wybierz przycisk **OK** w oknie dialogowym **Podgląd zmian** , a następnie **Wybierz przycisk** Akceptuję w oknie dialogowym **akceptacji licencji** , jeśli zgadzasz się z postanowieniami licencyjnymi dotyczącymi wymienionych pakietów. Powtórz te kroki dla **Microsoft. ml. szeregów czasowych**.

4. Dodaj następujące `using` instrukcje w górnej części pliku *program.cs* :

    [!code-csharp[AddUsings](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#AddUsings "Add necessary usings")]

### <a name="download-your-data"></a>Pobierz swoje dane

1. Pobierz zestaw danych i Zapisz go w utworzonym wcześniej folderze *danych* :

    Kliknij prawym przyciskiem myszy [*phone-calls.csv*](https://raw.githubusercontent.com/dotnet/machinelearning-samples/master/samples/csharp/getting-started/AnomalyDetection_PhoneCalls/SrCnnDetection/Data/phone-calls.csv) i wybierz pozycję "Zapisz link (lub cel) jako..."

     Upewnij się, że plik CSV został zapisany w \* folderze *dane* lub po jego zapisaniu w innym miejscu Przenieś \* plik CSV do folderu *dane* .

2. W Eksplorator rozwiązań kliknij prawym przyciskiem myszy \* plik CSV i wybierz polecenie **Właściwości**. W obszarze **Zaawansowane** Zmień wartość opcji **Kopiuj do katalogu wyjściowego** na Kopiuj, **jeśli nowszy**.

Poniższa tabela zawiera podgląd danych z \* pliku CSV:

| sygnatura czasowa  | wartość |
|--------|--------------|
| 2018/9/3  | 36,69670857  |
| 2018/9/4  | 35,74160571  |
| .....  | .....  |
| 2018/10/3  | 34,49893429  |
| ...    | ....   |

Ten plik reprezentuje serię czasową. Każdy wiersz w pliku jest punktem danych. Każdy Piont danych ma dwa atrybuty, a mianowicie, `timestamp` i `value` , aby reprensent liczbę połączeń telefonicznych w każdym dniu. Liczba połączeń telefonicznych jest przekształcana w celu cofnięcia czułości.

### <a name="create-classes-and-define-paths"></a>Tworzenie klas i Definiowanie ścieżek

Następnie zdefiniuj struktury danych dla klas wejściowych i prognoz.

Dodaj nową klasę do projektu:

1. W **Eksplorator rozwiązań** kliknij prawym przyciskiem myszy projekt, a następnie wybierz pozycję **Dodaj > nowy element**.

2. W **oknie dialogowym Dodaj nowy element** wybierz pozycję **Klasa** i zmień wartość pola **Nazwa** na *PhoneCallsData.cs*. Następnie wybierz przycisk **Dodaj** .

   Plik *PhoneCallsData.cs* zostanie otwarty w edytorze kodu.

3. Dodaj następującą `using` instrukcję na początku *PhoneCallsData.cs*:

   ```csharp
   using Microsoft.ML.Data;
   ```

4. Usuń istniejącą definicję klasy i Dodaj następujący kod, który ma dwie klasy `PhoneCallsData` i `PhoneCallsPrediction` , do pliku *PhoneCallsData.cs* :

    [!code-csharp[DeclareTypes](./snippets/phone-calls-anomaly-detection/csharp/PhoneCallsData.cs#DeclareTypes "Declare data record types")]

    `PhoneCallsData` Określa klasę danych wejściowych. Atrybut [LoadColumn](xref:Microsoft.ML.Data.LoadColumnAttribute.%23ctor%28System.Int32%29) określa, które kolumny (według indeksu kolumn) w zestawie danych powinny zostać załadowane. Ma dwa atrybuty, `timestamp` `value` które są zgodne z tymi samymi atrybutami w pliku danych.

    `PhoneCallsPrediction` Określa klasę danych przewidywania. W przypadku detektora SR-CNN funkcja przewidywania zależy od określonego [trybu wykrywania](xref:Microsoft.ML.TimeSeries.SrCnnDetectMode) . W tym przykładzie wybieramy `AnomalyAndMargin` tryb. Dane wyjściowe zawierają siedem kolumn. W większości przypadków, `IsAnomaly` , `ExpectedValue` `UpperBoundary` i `LowerBoundary` są wystarczająco aktualne. Informują o tym, że punkt jest anomalią, oczekiwaną wartością punktu i dolną/górną granicę obszaru.

5. Dodaj następujący kod do wiersza bezpośrednio powyżej `Main` metody, aby określić ścieżkę do pliku danych:

    [!code-csharp[Declare global variables](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#DeclareGlobalVariables "Declare global variables")]

### <a name="initialize-variables-in-main"></a>Inicjuj zmienne w głównym

1. Zastąp `Console.WriteLine("Hello World!")` wiersz w `Main` metodzie poniższym kodem, aby zadeklarować i zainicjować `mlContext` zmienną:

    [!code-csharp[CreateMLContext](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#CreateMLContext "Create the ML Context")]

    [Klasa MLContext](xref:Microsoft.ML.MLContext) jest punktem początkowym dla wszystkich operacji ml.NET, a inicjowanie `mlContext` tworzy nowe środowisko ml.NET, które może być współużytkowane przez obiekty przepływu pracy tworzenia modelu. Jest to podobne, pojęciowo do `DBContext` w Entity Framework.

### <a name="load-the-data"></a>Ładowanie danych

Dane w ML.NET są reprezentowane jako [Klasa IDataView](xref:Microsoft.ML.IDataView). `IDataView` to elastyczny i wydajny sposób opisywania danych tabelarycznych (liczbowych i tekstowych). Dane można ładować z pliku tekstowego lub z innych źródeł (na przykład bazy danych SQL lub plików dziennika) do `IDataView` obiektu.

1. Dodaj następujący kod w następnym wierszu `Main` metody:

    [!code-csharp[LoadData](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#LoadData "loading dataset")]

    [LoadFromTextFile ()](xref:Microsoft.ML.TextLoaderSaverCatalog.LoadFromTextFile%60%601%28Microsoft.ML.DataOperationsCatalog,System.String,System.Char,System.Boolean,System.Boolean,System.Boolean,System.Boolean%29) definiuje schemat danych i odczytuje w pliku. Przyjmuje zmienne ścieżki danych i zwraca `IDataView` .

## <a name="time-series-anomaly-detection"></a>Wykrywanie anomalii szeregów czasowych

Wykrywanie anomalii szeregów czasowych to proces wykrywania odstających danych szeregów czasowych; wskazuje na dane wejściowe serie czasowe, w których zachowanie nie jest oczekiwane, lub "brzmienia". Te anomalie zwykle wskazują na niektóre zdarzenia interesujące w domenie problemu: atak cybernetycznymi na kontach użytkowników, awarię i RPS pliku na serwerze, przeciek pamięci itp.

Aby znaleźć anomalię w szeregach czasowych, należy najpierw określić okres serii. Następnie Serie czasowe mogą być rozłożone na kilka składników jako `Y = T + S + R` , gdzie `Y` jest oryginalną serią, `T` to składnik trendu, to `S` sezonowy componnent i `R` jest składnikiem końcowym serii. Ten krok jest nazywany [dekompozycją](https://en.wikipedia.org/wiki/Decomposition_of_time_series). Na koniec wykrywanie jest wykonywane na składniku końcowym, aby znaleźć anomalie. W ML.NET algorytm SR-CNN jest zaawansowanym i szczegółowym algorytmem opartym na widmie pozostałej (SR) i Splotowych neuronowych Network (CNN) w celu wykrycia anomalii w szeregach czasowych (zapoznaj się z [usługą wykrywania anomalii szeregów czasowych w dokumencie firmy Microsoft](https://arxiv.org/pdf/1906.03821.pdf) , aby uzyskać więcej informacji na temat tego algorytmu).

W tym samouczku zobaczysz, że te procedury można wykonać przy użyciu dwóch funkcji.

## <a name="detect-period"></a>Wykryj okres

W pierwszym kroku wywołujemy `DetectSeasonality` funkcję w celu określenia okresu serii.

### <a name="create-the-detectperiod-method"></a>Tworzenie metody DetectPeriod

1. Utwórz `DetectPeriod` metodę, tuż poniżej `Main` metody, przy użyciu następującego kodu:

    ```csharp
    static void DetectPeriod(MLContext mlContext, IDataView phoneCalls)
    {

    }
    ```

2. Użyj funkcji [DetectSeasonality](xref:Microsoft.ML.TimeSeriesCatalog.DetectSeasonality) , aby wykryć okres. Dodaj go do `DetectPeriod` metody przy użyciu następującego kodu:

    [!code-csharp[DetectSeasonality](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#DetectSeasonality)]

3. Wyświetl wartość okresu, dodając następujący kod jako następny wiersz kodu w `DetectPeriod` metodzie:

    [!code-csharp[DisplayPeriod](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#DisplayPeriod)]

4. Dodaj następujące wywołanie do `DetectPeriod` metody w `Main` metodzie:

    [!code-csharp[CallDetectPeriod](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#CallDetectPeriod)]

### <a name="period-detection-results"></a>Wyniki wykrywania okresu

Uruchom aplikację. Wyniki powinny wyglądać podobnie do poniższego.

```console
Period of the series is: 7.
```

## <a name="detect-anomaly"></a>Wykrywanie anomalii

W tym kroku użyjesz, [`SrCnnEntireDetector`](xref:Microsoft.ML.Transforms.TimeSeries.SrCnnEntireAnomalyDetector) Aby znaleźć anomalie.

### <a name="create-the-detectanomaly-method"></a>Tworzenie metody DetectAnomaly

1. Utwórz `DetectAnomaly` metodę, tuż poniżej `DetectPeriod` metody, przy użyciu następującego kodu:

    ```csharp
    static void DetectAnomaly(MLContext mlContext, IDataView phoneCalls, int period)
    {

    }
    ```

2. Skonfiguruj [SrCnnEntireAnomalyDetectorOptions](xref:Microsoft.ML.Transforms.TimeSeries.SrCnnEntireAnomalyDetectorOptions) w `DetectAnomaly` metodzie przy użyciu następującego kodu:

    [!code-csharp[SetupSrCnnParameters](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#SetupSrCnnParameters)]

3. Wykryj anomalię przez algorytm SR-CNN, dodając następujący wiersz kodu do `DetectAnomaly` metody:

    [!code-csharp[DetectAnomaly](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#DetectAnomaly)]

4. Konwertuj widok danych wyjściowych na silnie wpisaną, `IEnumerable` Aby ułatwić wyświetlanie przy użyciu [`CreateEnumerable`](xref:Microsoft.ML.DataOperationsCatalog.CreateEnumerable%2A) metody z następującym kodem:

    [!code-csharp[CreateEnumerableForResult](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#CreateEnumerableForResult)]

5. Utwórz nagłówek wyświetlania z następującym kodem jako następnym wierszem w `DetectAnomaly` metodzie:

    [!code-csharp[DisplayHeader](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#DisplayHeader)]

    W wynikach wykrywania punktu zmiany zostaną wyświetlone następujące informacje:

    * `Index` jest indeksem każdego punktu.
    * `Anomaly` jest wskaźnikiem wheather każdy punkt jest wykrywany jako anomalia.
    * `ExpectedValue` to Szacowana wartość każdego punktu.
    * `LowerBoundary` to najniższa wartość, którą każdy punkt może być nieanomalią.
    * `UpperBoundary` jest największą wartością, którą każdy punkt może być nieanomalią.

6. Wykonaj iterację `predictions` `IEnumerable` i Wyświetl wyniki przy użyciu następującego kodu:

    [!code-csharp[DisplayAnomalyDetectionResults](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#DisplayAnomalyDetectionResults)]

7. Dodaj następujące wywołanie do `DetectAnomaly` metody w `Main` metodzie:

    [!code-csharp[CallDetectAnomaly](./snippets/phone-calls-anomaly-detection/csharp/Program.cs#CallDetectAnomaly)]

## <a name="anomaly-detection-results"></a>Wyniki wykrywania anomalii

Uruchom aplikację. Wyniki powinny wyglądać podobnie do poniższego. Podczas przetwarzania wyświetlane są komunikaty. Mogą pojawić się ostrzeżenia lub przetwarzanie komunikatów. Niektóre komunikaty zostały usunięte z następujących wyników dla przejrzystości.

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

Gratulacje! Pomyślnie skompilowano modele uczenia maszynowego na potrzeby wykrywania okresu i anomalii w seriach okresowych.

Kod źródłowy dla tego samouczka można znaleźć w repozytorium [dotnet/Samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/PhoneCallsAnomalyDetection) .

W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:
> [!div class="checklist"]
>
> * Ładowanie danych
> * Wykryj okres w danych szeregów czasowych
> * Wykrywanie anomalii w danych szeregów czasowych

## <a name="next-steps"></a>Następne kroki

Zapoznaj się z repozytorium Machine Learning przykłady w witrynie GitHub, aby poznać przykład wykrywania anomalii dotyczącego zużycia mocy.
> [!div class="nextstepaction"]
> [dotnet/machinelearning — przykłady repozytorium GitHub](https://github.com/dotnet/machinelearning-samples/tree/master/samples/csharp/getting-started/AnomalyDetection_PowerMeterReadings)
