---
title: Co to jest ML.NET i jak to działa?
description: ML.NET umożliwia dodawanie uczenia maszynowego do aplikacji .NET, w scenariuszach w trybie online lub offline. Dzięki tej możliwości można dokonać automatycznych prognoz przy użyciu danych dostępnych dla aplikacji bez konieczności podłączania do sieci w celu użycia ML.NET. W tym artykule objaśniono podstawowe informacje dotyczące uczenia maszynowego w programie ML.NET.
ms.date: 11/5/2019
ms.topic: overview
ms.custom: mvc
ms.openlocfilehash: 2c44a83b4d45c95cbe45f125523207811f6368c2
ms.sourcegitcommit: 635a0ff775d2447a81ef7233a599b8f88b162e5d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/17/2020
ms.locfileid: "97634069"
---
# <a name="what-is-mlnet-and-how-does-it-work"></a>Co to jest ML.NET i jak to działa?

ML.NET umożliwia dodawanie uczenia maszynowego do aplikacji .NET, w scenariuszach w trybie online lub offline. Dzięki tej możliwości można dokonać automatycznych prognoz przy użyciu danych dostępnych dla aplikacji. Aplikacje do uczenia maszynowego wykorzystują wzorce w danych, aby tworzyć przewidywania, a nie muszą być jawnie programowane.

Central do ML.NET to **model** uczenia maszynowego. Model określa kroki niezbędne do przekształcenia danych wejściowych w prognozowanie. Za pomocą ML.NET można uczenie niestandardowego modelu przez określenie algorytmu lub zaimportować wstępnie szkolonych modeli TensorFlow i ONNX.

Po utworzeniu modelu możesz dodać go do swojej aplikacji, aby dokonać prognoz.

ML.NET działa w systemach Windows, Linux i macOS przy użyciu platformy .NET Core lub systemu Windows przy użyciu .NET Framework. 64 bit jest obsługiwany na wszystkich platformach. 32 bit jest obsługiwany w systemie Windows, z wyjątkiem funkcji TensorFlow, LightGBM i ONNX.

Przykłady typu przewidywania, które można wprowadzić przy użyciu ML.NET:

|||
|-|-|
|Klasyfikacja/Kategoryzacja|Automatycznie Podziel Opinie klientów na kategorie dodatnie i ujemne|
|Wartości ciągłe regresji/przewidywania|Przewidywanie ceny domów na podstawie rozmiaru i lokalizacji|
|Wykrywanie anomalii|Wykrywanie fałszywych transakcji bankowych |
|Zalecenia|Sugeruj produkty, które kupujący online może chcieć kupić, w oparciu o ich poprzednie zakupy|
|Szeregi czasowe/dane sekwencyjne|Prognoza pogody/sprzedaż produktu|
|Klasyfikacja obrazów|Kategoryzacja pathologies w obrazach medycznych|

## <a name="hello-mlnet-world"></a>Witaj w świecie ML.NET

Kod w poniższym fragmencie kodu demonstruje najprostszą aplikację ML.NET. Ten przykład tworzy model regresji liniowej do przewidywania cen dla domu przy użyciu rozmiaru domu i danych cen.

 ```csharp
    using System;
    using Microsoft.ML;
    using Microsoft.ML.Data;

    class Program
    {
        public class HouseData
        {
            public float Size { get; set; }
            public float Price { get; set; }
        }

        public class Prediction
        {
            [ColumnName("Score")]
            public float Price { get; set; }
        }

        static void Main(string[] args)
        {
            MLContext mlContext = new MLContext();

            // 1. Import or create training data
            HouseData[] houseData = {
                new HouseData() { Size = 1.1F, Price = 1.2F },
                new HouseData() { Size = 1.9F, Price = 2.3F },
                new HouseData() { Size = 2.8F, Price = 3.0F },
                new HouseData() { Size = 3.4F, Price = 3.7F } };
            IDataView trainingData = mlContext.Data.LoadFromEnumerable(houseData);

            // 2. Specify data preparation and model training pipeline
            var pipeline = mlContext.Transforms.Concatenate("Features", new[] { "Size" })
                .Append(mlContext.Regression.Trainers.Sdca(labelColumnName: "Price", maximumNumberOfIterations: 100));

            // 3. Train model
            var model = pipeline.Fit(trainingData);

            // 4. Make a prediction
            var size = new HouseData() { Size = 2.5F };
            var price = mlContext.Model.CreatePredictionEngine<HouseData, Prediction>(model).Predict(size);

            Console.WriteLine($"Predicted price for size: {size.Size*1000} sq ft= {price.Price*100:C}k");

            // Predicted price for size: 2500 sq ft= $261.98k
        }
    }
```

## <a name="code-workflow"></a>Przepływ pracy kodu

Poniższy diagram przedstawia strukturę kodu aplikacji, a także proces iteracyjny projektowania modelu:

- Zbieranie i ładowanie danych szkoleniowych do obiektu **IDataView**
- Określ potok operacji, aby wyodrębnić funkcje i zastosować algorytm uczenia maszynowego
- Uczenie modelu przez wywoływanie funkcji **dopasowania ()** na potoku
- Oceń model i wykonaj iterację w celu usprawnienia
- Zapisz model w formacie binarnym, który ma być używany w aplikacji
- Załaduj model z powrotem do obiektu **ITransformer**
- Wykonaj przewidywania, wywołując **CreatePredictionEngine. predykcyjny ()**

![Przepływ tworzenia aplikacji ML.NET, w tym składniki służące do generowania danych, tworzenia potoku, szkolenia modeli, oceny modelu i użycia modelu](./media/mldotnet-annotated-workflow.png)

Przyjrzyjmy się nieco bardziej szczegółowym koncepcjom.

## <a name="machine-learning-model"></a>Model uczenia maszynowego

Model ML.NET jest obiektem, który zawiera przekształcenia do wykonania na danych wejściowych w celu osiągnięcia przewidywanych danych wyjściowych.

### <a name="basic"></a>Podstawowy

Najpopularniejszym modelem jest dwuwymiarowa regresja liniowa, w której jedna ciągła ilość jest proporcjonalna do innej, jak w powyższym przykładzie cen domu.

![Model regresji liniowej z parametrami bias i wagi](./media/linear-regression-model.svg)

Model jest po prostu: $Price = b + rozmiar * w $. Parametry $b $ i $w $ są szacowane przez dopasowanie wiersza do pary par (size, Price). Dane używane do znajdowania parametrów modelu są nazywane **danymi szkoleniowymi**. Dane wejściowe modelu uczenia maszynowego są nazywane **funkcjami**. W tym przykładzie $Size $ jest jedyną funkcją. Wartości typu podstawa — prawdziwie używane do uczenia modelu uczenia maszynowego są nazywane **etykietami**. W tym miejscu $Price $ wartości w zestawie danych szkoleniowych są etykietami.

### <a name="more-complex"></a>Bardziej skomplikowane

Bardziej skomplikowany model klasyfikuje transakcje finansowe do kategorii przy użyciu opisu tekstu transakcji.

Każdy opis transakcji jest podzielony na zestaw funkcji przez usunięcie zbędnych słów i znaków oraz liczenie kombinacji wyrazów i znaków. Zestaw funkcji służy do uczenia modelu liniowego na podstawie zestawu kategorii w danych szkoleniowych. Im bardziej podobne są nowe opisy w zestawie szkoleniowym, tym bardziej prawdopodobnie zostanie przypisany do tej samej kategorii.

![Model klasyfikacji tekstu](./media/text-classification-model.svg)

Model cen domu i model klasyfikacji tekstu to modele **liniowe** . W zależności od charakteru danych i rozwiązywanego problemu można także używać modeli **drzewa decyzyjnego** , **ogólnych modeli dodatków** i innych. Więcej informacji o modelach można znaleźć w części [zadania](./resources/tasks.md).

## <a name="data-preparation"></a>Przygotowywanie danych

W większości przypadków dostępne dane nie są odpowiednie do użycia bezpośrednio do uczenia modelu uczenia maszynowego. Dane pierwotne muszą zostać przygotowane lub wstępnie przetworzone, aby można było ich użyć w celu znalezienia parametrów modelu. Może być konieczne przekonwertowanie danych z wartości ciągu na reprezentację liczbową. Dane wejściowe mogą zawierać nadmiarowe informacje. Może być konieczne zmniejszenie lub powiększenie wymiarów danych wejściowych. Może być konieczne znormalizowanie lub skalowanie danych.

W [samouczkach ml.NET](./tutorials/index.md) przedstawiono różne potoki przetwarzania danych dotyczące tekstu, obrazów, liczb i danych szeregów czasowych używanych do określonych zadań uczenia maszynowego.

[Sposób przygotowania danych](./how-to-guides/prepare-data-ml-net.md) pokazuje, jak bardziej ogólnie stosować Przygotowywanie danych.

Dodatek wszystkich [dostępnych transformacji](./resources/transforms.md) można znaleźć w sekcji Resources (zasoby).

## <a name="model-evaluation"></a>Ocena modelu

Po przeprowadzeniu szkolenia modelu wiesz, jak dobrze będzie w przyszłości prognozować? Dzięki ML.NET można oszacować model na podstawie nowych danych testowych.

Każdy typ zadania uczenia maszynowego ma metryki używane do oszacowania dokładności i dokładności modelu względem zestawu danych testowych.

W naszym przykładzie cen domu użyto zadania **regresji** . Aby oszacować model, Dodaj następujący kod do oryginalnego przykładu.

```csharp
        HouseData[] testHouseData =
        {
            new HouseData() { Size = 1.1F, Price = 0.98F },
            new HouseData() { Size = 1.9F, Price = 2.1F },
            new HouseData() { Size = 2.8F, Price = 2.9F },
            new HouseData() { Size = 3.4F, Price = 3.6F }
        };

        var testHouseDataView = mlContext.Data.LoadFromEnumerable(testHouseData);
        var testPriceDataView = model.Transform(testHouseDataView);

        var metrics = mlContext.Regression.Evaluate(testPriceDataView, labelColumnName: "Price");

        Console.WriteLine($"R^2: {metrics.RSquared:0.##}");
        Console.WriteLine($"RMS error: {metrics.RootMeanSquaredError:0.##}");

        // R^2: 0.96
        // RMS error: 0.19
```

Metryki oceny informują o tym, że błąd ma niską ish i że korelacja między przewidywanym wyjściem i wyjściem testu jest wysoka. To było łatwe! W rzeczywistych przykładach zwiększa się to w celu osiągnięcia dobrych metryk modelu.

## <a name="mlnet-architecture"></a>Architektura ML.NET

W tej sekcji przejdziemy do wzorca architektury ML.NET. Jeśli jesteś doświadczonym deweloperem platformy .NET, niektóre z tych wzorców będą znane użytkownikowi, a niektóre z nich będą mniej znane. Zaczekaj, aż szczegółowemy!

Aplikacja ML.NET rozpoczyna się od <xref:Microsoft.ML.MLContext> obiektu. Ten obiekt singleton zawiera **wykazy**. Katalog jest fabryką służącą do ładowania i zapisywania danych, przekształcania, instruktorów i składników operacji modelu. Każdy obiekt wykazu ma metody do tworzenia różnych typów składników:

|||||
|-|-|-|-|
|Ładowanie i zapisywanie danych||<xref:Microsoft.ML.DataOperationsCatalog>||
|Przygotowywanie danych||<xref:Microsoft.ML.TransformsCatalog>||
|Algorytmy szkoleniowe|Klasyfikacja binarna|<xref:Microsoft.ML.BinaryClassificationCatalog>||
||Klasyfikacja wieloklasowa|<xref:Microsoft.ML.MulticlassClassificationCatalog>||
||Wykrywanie anomalii|<xref:Microsoft.ML.AnomalyDetectionCatalog>||
||Klastrowanie|<xref:Microsoft.ML.ClusteringCatalog>||
||Prognozowanie|<xref:Microsoft.ML.ForecastingCatalog>||
||Określania|<xref:Microsoft.ML.RankingCatalog>||
||Regresja|<xref:Microsoft.ML.RegressionCatalog>||
||Zalecenie|<xref:Microsoft.ML.RecommendationCatalog>|Dodawanie `Microsoft.ML.Recommender` pakietu NuGet|
||Szeregów czasowych|<xref:Microsoft.ML.TimeSeriesCatalog>|Dodawanie `Microsoft.ML.TimeSeries` pakietu NuGet|
|Użycie modelu ||<xref:Microsoft.ML.ModelOperationsCatalog>||

Możesz przejść do metod tworzenia w każdej z powyższych kategorii. W przypadku korzystania z programu Visual Studio wykazy są wyświetlane za pośrednictwem technologii IntelliSense.

   ![Technologia IntelliSense dla instruktorów regresji](./media/catalog-intellisense.png)

### <a name="build-the-pipeline"></a>Kompilowanie potoku

W każdym katalogu jest zestaw metod rozszerzających. Przyjrzyjmy się sposobom, w jaki metody rozszerzające są używane do tworzenia potoku szkoleniowego.

```csharp
    var pipeline = mlContext.Transforms.Concatenate("Features", new[] { "Size" })
        .Append(mlContext.Regression.Trainers.Sdca(labelColumnName: "Price", maximumNumberOfIterations: 100));
```

W tym fragmencie kodu `Concatenate` i `Sdca` są obie metody w wykazie. Każdy z nich tworzy obiekt [IEstimator](xref:Microsoft.ML.IEstimator%601) , który jest dołączany do potoku.

W tym momencie obiekty są tworzone tylko. Nie wykonano żadnego wykonania.

### <a name="train-the-model"></a>Trenowanie modelu

Po utworzeniu obiektów w potoku, dane mogą być używane do uczenia modelu.

```csharp
    var model = pipeline.Fit(trainingData);
```

Wywołanie `Fit()` używa danych szkolenia wejściowego do oszacowania parametrów modelu. Jest to nazywane uczeniem modelu. Należy pamiętać, że model regresji liniowej powyżej ma dwa parametry modelu: **bias** i **waga**. Po `Fit()` wywołaniu wartości parametrów są znane. Większość modeli będzie zawierać wiele innych parametrów niż to.

Więcej informacji na temat szkolenia modeli można znaleźć w temacie [Jak szkolić model](./how-to-guides/train-machine-learning-model-ml-net.md).

Obiekt modelu z wynikiem jest zaimplementowany przez <xref:Microsoft.ML.ITransformer> interfejs. Oznacza to, że model przekształca dane wejściowe w przewidywania.

```csharp
   IDataView predictions = model.Transform(inputData);
```

### <a name="use-the-model"></a>Korzystanie z modelu

Można przekształcać dane wejściowe w prognozy zbiorcze lub pojedyncze dane wejściowe. W przykładzie cen domu firma Microsoft: w sposób zbiorczy na potrzeby oceny modelu i po jednym naraz, aby utworzyć nowe prognozowanie. Przyjrzyjmy się tworzeniu pojedynczych prognoz.

```csharp
    var size = new HouseData() { Size = 2.5F };
    var predEngine = mlContext.CreatePredictionEngine<HouseData, Prediction>(model);
    var price = predEngine.Predict(size);
```

`CreatePredictionEngine()`Metoda przyjmuje klasę wejściową i klasę wyjściową. Nazwy pól i/lub atrybuty kodu określają nazwy kolumn danych używanych podczas szkoleń i prognozowania modeli. Aby uzyskać więcej informacji, zobacz [Tworzenie prognoz przy użyciu nauczonego modelu](how-to-guides/machine-learning-model-predictions-ml-net.md).

### <a name="data-models-and-schema"></a>Modele danych i schemat

Na początku potoku uczenia maszynowego ML.NET są obiekty [DataView](xref:Microsoft.ML.IDataView) .

Każda transformacja w potoku ma schemat wejściowy (nazwy danych, typy i rozmiary, których transformacja oczekuje na dane wejściowe); oraz schemat danych wyjściowych (nazwy danych, typy i rozmiary generowane przez transformację po przekształceniu).

Jeśli schemat danych wyjściowych z jednego przekształcenia w potoku nie jest zgodny ze schematem wejściowym kolejnej transformacji, ML.NET zgłosi wyjątek.

Obiekt widoku danych ma kolumny i wiersze. Każda kolumna ma nazwę i typ i długość. Na przykład kolumny wejściowe z przykładu ceny domu mają **rozmiar** i **cenę**. Są one zarówno typu, jak i są liczbami skalarnymi, a nie wektorami.

   ![Przykład widoku danych ML.NET z danymi prognozowania cen domu](./media/ml-net-dataview.png)

Wszystkie algorytmy ML.NET szukają kolumny wejściowej, która jest wektorem. Domyślnie ta kolumna wektora jest nazywana **funkcjami**. To dlatego, że połączymy kolumnę **size** z nową kolumną o nazwie **Features** w naszym przykładzie cen domu.

 ```csharp
    var pipeline = mlContext.Transforms.Concatenate("Features", new[] { "Size" })
 ```

Wszystkie algorytmy również tworzą nowe kolumny po przeprowadzeniu przewidywania. Stałe nazwy tych nowych kolumn zależą od typu algorytmu uczenia maszynowego. W przypadku zadania regresji jedna z nowych kolumn jest nazywana **wynikiem**. To dlatego, że nasze dane cen są przypisane do tej nazwy.

```csharp
    public class Prediction
    {
        [ColumnName("Score")]
        public float Price { get; set; }
    }
```

Więcej informacji na temat kolumn wyjściowych różnych zadań uczenia maszynowego można znaleźć w przewodniku [zadania Machine Learning](resources/tasks.md) .

Ważną właściwością obiektów DataView jest to, że są one oceniane **opóźnieniem**. Widoki danych są ładowane i obsługiwane tylko podczas szkoleń i oceny modelu oraz do przewidywania danych. Podczas pisania i testowania aplikacji ML.NET można użyć debugera programu Visual Studio, aby uzyskać wgląd w dowolny obiekt widoku danych przez wywołanie metody [podglądu](xref:Microsoft.ML.DebuggerExtensions.Preview%2A) .

```csharp
    var debug = testPriceDataView.Preview();
```

Możesz obejrzeć `debug` zmienną w debugerze i przeanalizować jej zawartość. Nie używaj metody Preview w kodzie produkcyjnym, ponieważ znacząco obniża ona wydajność.

### <a name="model-deployment"></a>Wdrożenie modelu

W aplikacjach w czasie rzeczywistym model szkoleń i oceny kodu zostanie oddzielony od prognoz. W rzeczywistości te dwa działania są często wykonywane przez oddzielne zespoły. Zespół projektowy modelu może zapisać model do użycia w aplikacji predykcyjnej.

```csharp
   mlContext.Model.Save(model, trainingData.Schema,"model.zip");
```

## <a name="next-steps"></a>Następne kroki

* Dowiedz się, jak tworzyć aplikacje przy użyciu różnych zadań uczenia maszynowego z bardziej realistycznymi zestawami danych w [samouczkach](./tutorials/index.md).

* Więcej informacji na temat szczegółowych tematów znajduje się w temacie [jak przewodniki](./how-to-guides/index.md).

* Jeśli jesteś super Keen, możesz szczegółowe bezpośrednio do [dokumentacji dotyczącej interfejsu API](../../api/index.md?view=ml-dotnet).
