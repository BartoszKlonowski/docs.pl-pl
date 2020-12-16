---
title: Jak wybrać algorytm ML.NET
description: Dowiedz się, jak wybrać algorytm ML.NET dla modelu uczenia maszynowego
ms.topic: overview
ms.date: 06/05/2019
ms.openlocfilehash: 04cf191401c7c25f1fa341acaf9312dc19752260
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/16/2020
ms.locfileid: "97593093"
---
# <a name="how-to-choose-an-mlnet-algorithm"></a>Jak wybrać algorytm ML.NET

Dla każdego [zadania ml.NET](resources/tasks.md)istnieje wiele algorytmów szkoleniowych do wyboru. Który z nich należy wybrać, zależy od problemu, który próbujesz rozwiązać, charakterystyk danych oraz dostępnych zasobów obliczeniowych i magazynu. Należy pamiętać, że uczenie modelu uczenia maszynowego jest procesem iteracyjnym. Może być konieczne wypróbowanie wielu algorytmów w celu znalezienia tego, który działa najlepiej.

Algorytmy operują na **funkcjach**. Funkcje to wartości liczbowe obliczane na podstawie danych wejściowych. Są one optymalnymi danymi wejściowymi dla algorytmów uczenia maszynowego. Przekształć pierwotne dane wejściowe w funkcje przy użyciu co najmniej jednego [przekształcenia danych](resources/transforms.md). Na przykład dane tekstowe są przekształcane na zbiór liczników wyrazów i liczby kombinacji wyrazów. Po wyodrębnieniu funkcji z pierwotnego typu danych przy użyciu transformacji danych są one określane jako **featurized**. Na przykład featurized tekst lub featurized dane obrazu.

## <a name="trainer--algorithm--task"></a>Trainer = algorytm + zadanie

Algorytm to zapis matematyczny wykonywany w celu utworzenia **modelu**. Różne algorytmy tworzą modele o różnej charakterystyce.

W przypadku ML.NET tego samego algorytmu można zastosować do różnych zadań. Na przykład do klasyfikacji binarnej, klasyfikacji wieloklasowej i regresji można używać stochastycznego podwójnej współrzędnej. Różnica polega na tym, jak dane wyjściowe algorytmu są interpretowane w celu dopasowania do zadania.

Dla każdej kombinacji algorytmu/zadania ML.NET zapewnia składnik, który wykonuje algorytm szkolenia i wykonuje interpretację. Te składniki są nazywane instruktorami. Na przykład <xref:Microsoft.ML.Trainers.SdcaRegressionTrainer> używa algorytmu **StochasticDualCoordinatedAscent** stosowanego do zadania **regresji** .

## <a name="linear-algorithms"></a>Algorytmy liniowe

Algorytmy liniowe tworzą model, który oblicza **wyniki** z liniowej kombinacji danych wejściowych i zestawu **wag**. Wagi są parametry modelu szacowane podczas szkolenia.

Algorytmy liniowe działają dobrze w przypadku funkcji, które są [rozdzielone liniowo](https://en.wikipedia.org/wiki/Linear_separability).

Przed rozpoczęciem szkolenia przy użyciu algorytmu liniowego należy znormalizować funkcje. Dzięki temu jedna funkcja nie ma więcej wpływu na wynik niż inne.

Ogólnie rzecz biorąc, algorytmy liniowe są skalowalne, szybkie, Tanie do uczenia się i tanie do przewidywania. Są one skalowane przez liczbę funkcji i przybliżone według rozmiaru zestawu danych szkoleniowych.

Algorytmy liniowe czynią wiele przebiegów przez dane szkoleniowe. Jeśli zestaw danych mieści się w pamięci, dodanie [punktu kontrolnego pamięci podręcznej](xref:Microsoft.ML.LearningPipelineExtensions.AppendCacheCheckpoint%2A) do potoku ml.NET przed dołączeniem Trainer spowoduje szybsze działanie szkolenia.

**Instruktorzy liniowi**

|Algorytm|Właściwości|Instruktorów|
|---------|----------|--------|
|Średnia Perceptron|Najlepsza dla klasyfikacji tekstu|<xref:Microsoft.ML.Trainers.AveragedPerceptronTrainer>|
|Stochastycznego Dual coordinateal|Dostrajanie nie jest wymagane dla dobrej wydajności domyślnej|<xref:Microsoft.ML.Trainers.SdcaLogisticRegressionBinaryTrainer> <xref:Microsoft.ML.Trainers.SdcaNonCalibratedBinaryTrainer> <xref:Microsoft.ML.Trainers.SdcaMaximumEntropyMulticlassTrainer> <xref:Microsoft.ML.Trainers.SdcaNonCalibratedMulticlassTrainer> <xref:Microsoft.ML.Trainers.SdcaRegressionTrainer>|
|L — BFGS|Użyj, gdy liczba funkcji jest duża. Tworzy statystykę szkoleniową z zakresu regresji logistycznej, ale nie skaluje się, a także AveragedPerceptronTrainer|<xref:Microsoft.ML.Trainers.LbfgsLogisticRegressionBinaryTrainer> <xref:Microsoft.ML.Trainers.LbfgsMaximumEntropyMulticlassTrainer> <xref:Microsoft.ML.Trainers.LbfgsPoissonRegressionTrainer>|
|Stochastycznego symboliczny gradient|Najszybsze i najbardziej precyzyjne Trainer klasyfikacji liniowej. Skaluj z liczbą procesorów|<xref:Microsoft.ML.Trainers.SymbolicSgdLogisticRegressionBinaryTrainer>|

## <a name="decision-tree-algorithms"></a>Algorytmy drzewa decyzyjnego

Algorytmy drzewa decyzyjne tworzą model zawierający serię decyzji: efektywnie wykres przepływu za pomocą wartości danych.

Funkcje te nie muszą być liniowie oddzielone, aby można było używać tego typu algorytmu. Funkcje i nie muszą być znormalizowane, ponieważ poszczególne wartości w wektorze funkcji są używane niezależnie w procesie decyzyjnym.

Algorytmy drzewa decyzyjnego są generalnie bardzo dokładne.

Z wyjątkiem ogólnych modeli addytywne (GAMs), modele drzewa mogą nie mieć możliwości wyjaśnienia, gdy liczba funkcji jest duża.

Algorytmy drzewa decyzyjne pobierają więcej zasobów i nie są skalowane, a także liniowe. Działają one wydajnie w zestawach danych, które mogą być dopasowane do pamięci.

Podwyższenie drzewa decyzyjne to zbiór małych drzew, w których każde drzewo ocenia dane wejściowe i przekazuje wynik do następnego drzewa, aby utworzyć lepszy wynik i tak dalej, gdzie poszczególne drzewa w ramach elementu szeregowego usprawniają poprzednią.

**Instruktorzy drzewa decyzyjnego**

|Algorytm|Właściwości|Instruktorów|
|---------|----------|--------|
|Komputer z zwiększona gradientem świetlnym|Najszybsze i najdokładniejsze instruktorów drzewa klasyfikacji binarnej. Wysoce możliwość dostosowania|<xref:Microsoft.ML.Trainers.LightGbm.LightGbmBinaryTrainer> <xref:Microsoft.ML.Trainers.LightGbm.LightGbmMulticlassTrainer> <xref:Microsoft.ML.Trainers.LightGbm.LightGbmRegressionTrainer> <xref:Microsoft.ML.Trainers.LightGbm.LightGbmRankingTrainer>|
|Szybkie drzewo|Używane dla danych obrazu featurized. Odporne na dane niezrównoważone. Wysoce możliwość dostosowania | <xref:Microsoft.ML.Trainers.FastTree.FastTreeBinaryTrainer> <xref:Microsoft.ML.Trainers.FastTree.FastTreeRegressionTrainer> <xref:Microsoft.ML.Trainers.FastTree.FastTreeTweedieTrainer> <xref:Microsoft.ML.Trainers.FastTree.FastTreeRankingTrainer>|
|Szybki Las|Dobrze sprawdza się w przypadku danych o zakłóceniach|<xref:Microsoft.ML.Trainers.FastTree.FastForestBinaryTrainer> <xref:Microsoft.ML.Trainers.FastTree.FastForestRegressionTrainer>|
|Model ogólnego zastosowania (mapie GAM)|Najlepsze w przypadku problemów, które dobrze sprawdzają się przy użyciu algorytmów drzewa, ale gdzie wyjaśnienie jest priorytetem|<xref:Microsoft.ML.Trainers.FastTree.GamBinaryTrainer> <xref:Microsoft.ML.Trainers.FastTree.GamRegressionTrainer>|

## <a name="matrix-factorization"></a>Factorization macierzy

|Właściwości|Instruktorów|
|----------|--------|
|Najlepsze dla rozrzedzonych danych kategorii z dużymi zbiorami|<xref:Microsoft.ML.Trainers.FieldAwareFactorizationMachineTrainer>|

## <a name="meta-algorithms"></a>Algorytmy meta

Ci instruktorzy tworzą wieloklasowe Trainer z Trainer binarnych. Użyj z <xref:Microsoft.ML.Trainers.AveragedPerceptronTrainer> ,,,,, <xref:Microsoft.ML.Trainers.LbfgsLogisticRegressionBinaryTrainer> <xref:Microsoft.ML.Trainers.SymbolicSgdLogisticRegressionBinaryTrainer> <xref:Microsoft.ML.Trainers.LightGbm.LightGbmBinaryTrainer> <xref:Microsoft.ML.Trainers.FastTree.FastTreeBinaryTrainer> <xref:Microsoft.ML.Trainers.FastTree.FastForestBinaryTrainer> , <xref:Microsoft.ML.Trainers.FastTree.GamBinaryTrainer> .

|Algorytm|Właściwości|Instruktorów|
|---------|----------|--------|
|Jeden a wszystko|Ten klasyfikator wieloklasowy pociąga za sobą jeden klasyfikator binarny dla każdej klasy, co odróżnia tę klasę od wszystkich innych klas. Jest ograniczone w skali przez liczbę klas do kategoryzacji|[OneVersusAllTrainer\<BinaryClassificationTrainer>](xref:Microsoft.ML.Trainers.OneVersusAllTrainer) |
|Sprzęganie parowania|Ten klasyfikator wieloklasowy pociąga za sobą binarny algorytm klasyfikacji dla każdej pary klas. Jest ograniczone w skali przez liczbę klas, ponieważ każda kombinacja dwóch klas musi być przeszkolone.|[PairwiseCouplingTrainer\<BinaryClassificationTrainer>](xref:Microsoft.ML.Trainers.PairwiseCouplingTrainer)|

## <a name="k-means"></a>K — oznacza

|Właściwości|Instruktorów|
|----------|--------|
|Użyj do klastrowania|<xref:Microsoft.ML.Trainers.KMeansTrainer>|

## <a name="principal-component-analysis"></a>Analiza składników głównych

|Właściwości|Instruktorów|
|----------|--------|
|Użyj na potrzeby wykrywania anomalii|<xref:Microsoft.ML.Trainers.RandomizedPcaTrainer>|

## <a name="naive-bayes"></a>Prosty algorytm Bayesa

|Właściwości|Instruktorów|
|----------|--------|
|Użyj tej Trainer klasyfikacji wieloklasowej, gdy funkcje są niezależne, a zestaw danych szkoleniowych jest mały.|<xref:Microsoft.ML.Trainers.NaiveBayesMulticlassTrainer>|

## <a name="prior-trainer"></a>Poprzedni Trainer

|Właściwości|Instruktorów|
|----------|--------|
|Użyj tej klasyfikacji binarnej Trainer, aby obsłużyć wydajność innych instruktorów. Aby zapewnić skuteczność, metryki innych instruktorów powinny być lepsze niż wcześniejsze Trainer. |<xref:Microsoft.ML.Trainers.PriorTrainer>|
