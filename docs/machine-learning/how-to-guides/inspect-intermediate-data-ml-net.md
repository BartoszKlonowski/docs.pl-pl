---
title: Inspekcja danych pośrednich podczas przetwarzania ML.NET
description: Dowiedz się, jak przeprowadzać inspekcję danych pośrednich podczas ML.NETu załadowania, przetwarzania i modelowania potoku uczenia maszynowego w ML.NET.
ms.date: 06/25/2019
author: luisquintanilla
ms.author: luquinta
ms.custom: mvc, how-to, title-hack-0625
ms.openlocfilehash: 4f168653297594a604e6f381947f31cba5376178
ms.sourcegitcommit: aa6d8a90a4f5d8fe0f6e967980b8c98433f05a44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2020
ms.locfileid: "90679628"
---
# <a name="inspect-intermediate-data-during-processing"></a><span data-ttu-id="90e6c-103">Inspekcja danych pośrednich podczas przetwarzania</span><span class="sxs-lookup"><span data-stu-id="90e6c-103">Inspect intermediate data during processing</span></span>

<span data-ttu-id="90e6c-104">Dowiedz się, jak przeprowadzać inspekcję danych pośrednich podczas procesu ładowania, przetwarzania i tworzenia modeli w ML.NET.</span><span class="sxs-lookup"><span data-stu-id="90e6c-104">Learn how to inspect intermediate data during loading, processing, and model training steps in ML.NET.</span></span> <span data-ttu-id="90e6c-105">Dane pośrednie są danymi wyjściowymi każdego etapu w potoku uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="90e6c-105">Intermediate data is the output of each stage in the machine learning pipeline.</span></span>

<span data-ttu-id="90e6c-106">Dane pośrednie, takie jak reprezentowane poniżej, które są ładowane do programu, [`IDataView`](xref:Microsoft.ML.IDataView) można sprawdzić na różne sposoby w ml.NET.</span><span class="sxs-lookup"><span data-stu-id="90e6c-106">Intermediate data like the one represented below which is loaded into an [`IDataView`](xref:Microsoft.ML.IDataView) can be inspected in various ways in ML.NET.</span></span>

```csharp
HousingData[] housingData = new HousingData[]
{
    new HousingData
    {
        Size = 600f,
        HistoricalPrices = new float[] { 100000f ,125000f ,122000f },
        CurrentPrice = 170000f
    },
    new HousingData
    {
        Size = 1000f,
        HistoricalPrices = new float[] { 200000f, 250000f, 230000f },
        CurrentPrice = 225000f
    },
    new HousingData
    {
        Size = 1000f,
        HistoricalPrices = new float[] { 126000f, 130000f, 200000f },
        CurrentPrice = 195000f
    },
    new HousingData
    {
        Size = 850f,
        HistoricalPrices = new float[] { 150000f,175000f,210000f },
        CurrentPrice = 205000f
    },
    new HousingData
    {
        Size = 900f,
        HistoricalPrices = new float[] { 155000f, 190000f, 220000f },
        CurrentPrice = 210000f
    },
    new HousingData
    {
        Size = 550f,
        HistoricalPrices = new float[] { 99000f, 98000f, 130000f },
        CurrentPrice = 180000f
    }
};
```

## <a name="convert-idataview-to-ienumerable"></a><span data-ttu-id="90e6c-107">Konwertuj IDataView na interfejs IEnumerable</span><span class="sxs-lookup"><span data-stu-id="90e6c-107">Convert IDataView to IEnumerable</span></span>

<span data-ttu-id="90e6c-108">Jednym z najszybszych sposobów na sprawdzenie programu [`IDataView`](xref:Microsoft.ML.IDataView) jest przekształcenie go w [`IEnumerable`](xref:System.Collections.Generic.IEnumerable%601) .</span><span class="sxs-lookup"><span data-stu-id="90e6c-108">One of the quickest ways to inspect an [`IDataView`](xref:Microsoft.ML.IDataView) is to convert it to an [`IEnumerable`](xref:System.Collections.Generic.IEnumerable%601).</span></span> <span data-ttu-id="90e6c-109">Aby przekonwertować [`IDataView`](xref:Microsoft.ML.IDataView) metodę, aby [`IEnumerable`](xref:System.Collections.Generic.IEnumerable%601) użyć [`CreateEnumerable`](xref:Microsoft.ML.DataOperationsCatalog.CreateEnumerable%2A) metody.</span><span class="sxs-lookup"><span data-stu-id="90e6c-109">To convert an [`IDataView`](xref:Microsoft.ML.IDataView) to [`IEnumerable`](xref:System.Collections.Generic.IEnumerable%601) use the [`CreateEnumerable`](xref:Microsoft.ML.DataOperationsCatalog.CreateEnumerable%2A) method.</span></span>

<span data-ttu-id="90e6c-110">Aby zoptymalizować wydajność, ustaw `reuseRowObject` wartość `true` .</span><span class="sxs-lookup"><span data-stu-id="90e6c-110">To optimize performance, set `reuseRowObject` to `true`.</span></span> <span data-ttu-id="90e6c-111">Wykonanie tej czynności spowoduje opóźnieniem wypełnienie tego samego obiektu danymi bieżącego wiersza, ponieważ jest ono oceniane jako przeciwieństwem do tworzenia nowego obiektu dla każdego wiersza w zestawie danych.</span><span class="sxs-lookup"><span data-stu-id="90e6c-111">Doing so will lazily populate the same object with the data of the current row as it's being evaluated as opposed to creating a new object for each row in the dataset.</span></span>

```csharp
// Create an IEnumerable of HousingData objects from IDataView
IEnumerable<HousingData> housingDataEnumerable =
    mlContext.Data.CreateEnumerable<HousingData>(data, reuseRowObject: true);

// Iterate over each row
foreach (HousingData row in housingDataEnumerable)
{
    // Do something (print out Size property) with current Housing Data object being evaluated
    Console.WriteLine(row.Size);
}
```

## <a name="accessing-specific-indices-with-ienumerable"></a><span data-ttu-id="90e6c-112">Uzyskiwanie dostępu do określonych indeksów przy użyciu interfejsu IEnumerable</span><span class="sxs-lookup"><span data-stu-id="90e6c-112">Accessing specific indices with IEnumerable</span></span>

<span data-ttu-id="90e6c-113">Jeśli potrzebujesz tylko dostępu do części danych lub określonych indeksów, użyj [`CreateEnumerable`](xref:Microsoft.ML.DataOperationsCatalog.CreateEnumerable%2A) i ustaw `reuseRowObject` wartość parametru na tak, aby `false` nowy obiekt został utworzony dla każdego z żądanych wierszy w zestawie danych.</span><span class="sxs-lookup"><span data-stu-id="90e6c-113">If you only need access to a portion of the data or specific indices, use [`CreateEnumerable`](xref:Microsoft.ML.DataOperationsCatalog.CreateEnumerable%2A) and set the `reuseRowObject` parameter value to `false` so a new object is created for each of the requested rows in the dataset.</span></span> <span data-ttu-id="90e6c-114">Następnie przekonwertuj [`IEnumerable`](xref:System.Collections.Generic.IEnumerable%601) na tablicę lub listę.</span><span class="sxs-lookup"><span data-stu-id="90e6c-114">Then, convert the [`IEnumerable`](xref:System.Collections.Generic.IEnumerable%601) to an array or list.</span></span>

> [!WARNING]
> <span data-ttu-id="90e6c-115">Konwersja wyniku [`CreateEnumerable`](xref:Microsoft.ML.DataOperationsCatalog.CreateEnumerable%2A) do tablicy lub listy spowoduje załadowanie wszystkich żądanych [`IDataView`](xref:Microsoft.ML.IDataView) wierszy do pamięci, co może wpłynąć na wydajność.</span><span class="sxs-lookup"><span data-stu-id="90e6c-115">Converting the result of [`CreateEnumerable`](xref:Microsoft.ML.DataOperationsCatalog.CreateEnumerable%2A) to an array or list will load all the requested [`IDataView`](xref:Microsoft.ML.IDataView) rows into memory which may affect performance.</span></span>

<span data-ttu-id="90e6c-116">Po utworzeniu kolekcji można wykonywać operacje na danych.</span><span class="sxs-lookup"><span data-stu-id="90e6c-116">Once the collection has been created, you can perform operations on the data.</span></span> <span data-ttu-id="90e6c-117">Poniższy fragment kodu pobiera pierwsze trzy wiersze w zestawie danych i oblicza średnią bieżącą cenę.</span><span class="sxs-lookup"><span data-stu-id="90e6c-117">The code snippet below takes the first three rows in the dataset and calculates the average current price.</span></span>

```csharp
// Create an Array of HousingData objects from IDataView
HousingData[] housingDataArray =
    mlContext.Data.CreateEnumerable<HousingData>(data, reuseRowObject: false)
        .Take(3)
        .ToArray();

// Calculate Average CurrentPrice of First Three Elements
HousingData firstRow = housingDataArray[0];
HousingData secondRow = housingDataArray[1];
HousingData thirdRow = housingDataArray[2];
float averageCurrentPrice = (firstRow.CurrentPrice + secondRow.CurrentPrice + thirdRow.CurrentPrice) / 3;
```

## <a name="inspect-values-in-a-single-column"></a><span data-ttu-id="90e6c-118">Inspekcja wartości w pojedynczej kolumnie</span><span class="sxs-lookup"><span data-stu-id="90e6c-118">Inspect values in a single column</span></span>

<span data-ttu-id="90e6c-119">W dowolnym momencie procesu tworzenia modelu wartości w jednej kolumnie są [`IDataView`](xref:Microsoft.ML.IDataView) dostępne przy użyciu [`GetColumn`](xref:Microsoft.ML.Data.ColumnCursorExtensions.GetColumn%2A) metody.</span><span class="sxs-lookup"><span data-stu-id="90e6c-119">At any point in the model building process, values in a single column of an [`IDataView`](xref:Microsoft.ML.IDataView) can be accessed using the [`GetColumn`](xref:Microsoft.ML.Data.ColumnCursorExtensions.GetColumn%2A) method.</span></span> <span data-ttu-id="90e6c-120">[`GetColumn`](xref:Microsoft.ML.Data.ColumnCursorExtensions.GetColumn%2A)Metoda zwraca wszystkie wartości z pojedynczej kolumny jako [`IEnumerable`](xref:System.Collections.Generic.IEnumerable%601) .</span><span class="sxs-lookup"><span data-stu-id="90e6c-120">The [`GetColumn`](xref:Microsoft.ML.Data.ColumnCursorExtensions.GetColumn%2A) method returns all of the values in a single column as an [`IEnumerable`](xref:System.Collections.Generic.IEnumerable%601).</span></span>

```csharp
IEnumerable<float> sizeColumn = data.GetColumn<float>("Size").ToList();
```

## <a name="inspect-idataview-values-one-row-at-a-time"></a><span data-ttu-id="90e6c-121">Inspekcja wartości IDataView po jednym wierszu</span><span class="sxs-lookup"><span data-stu-id="90e6c-121">Inspect IDataView values one row at a time</span></span>

<span data-ttu-id="90e6c-122">[`IDataView`](xref:Microsoft.ML.IDataView) opóźnieniem.</span><span class="sxs-lookup"><span data-stu-id="90e6c-122">[`IDataView`](xref:Microsoft.ML.IDataView) is lazily evaluated.</span></span> <span data-ttu-id="90e6c-123">Aby wykonać iterację wierszy [`IDataView`](xref:Microsoft.ML.IDataView) bez konwersji na [`IEnumerable`](xref:System.Collections.Generic.IEnumerable%601) tak jak pokazano w poprzednich sekcjach tego dokumentu, Utwórz [`DataViewRowCursor`](xref:Microsoft.ML.DataViewRowCursor) za pomocą [`GetRowCursor`](xref:Microsoft.ML.IDataView.GetRowCursor%2A) metody i przekazując w [DataViewSchema](xref:Microsoft.ML.DataViewSchema) [`IDataView`](xref:Microsoft.ML.IDataView) jako parametr.</span><span class="sxs-lookup"><span data-stu-id="90e6c-123">To iterate over the rows of an [`IDataView`](xref:Microsoft.ML.IDataView) without converting to an [`IEnumerable`](xref:System.Collections.Generic.IEnumerable%601) as demonstrated in previous sections of this document, create a [`DataViewRowCursor`](xref:Microsoft.ML.DataViewRowCursor) by using the [`GetRowCursor`](xref:Microsoft.ML.IDataView.GetRowCursor%2A) method and passing in the [DataViewSchema](xref:Microsoft.ML.DataViewSchema) of your [`IDataView`](xref:Microsoft.ML.IDataView) as a parameter.</span></span> <span data-ttu-id="90e6c-124">Następnie, aby wykonać iterację wierszy, użyj [`MoveNext`](xref:Microsoft.ML.DataViewRowCursor.MoveNext%2A) metody Cursor wraz z [`ValueGetter`](xref:Microsoft.ML.ValueGetter%601) delegatami, aby wyodrębnić odpowiednie wartości z poszczególnych kolumn.</span><span class="sxs-lookup"><span data-stu-id="90e6c-124">Then, to iterate over rows, use the [`MoveNext`](xref:Microsoft.ML.DataViewRowCursor.MoveNext%2A) cursor method along with [`ValueGetter`](xref:Microsoft.ML.ValueGetter%601) delegates to extract the respective values from each of the columns.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="90e6c-125">W celu zapewnienia wydajności wektory w ML.NET używają [`VBuffer`](xref:Microsoft.ML.Data.VBuffer%601) zamiast natywnych typów kolekcji (czyli `Vector` , `float[]` ).</span><span class="sxs-lookup"><span data-stu-id="90e6c-125">For performance purposes, vectors in ML.NET use [`VBuffer`](xref:Microsoft.ML.Data.VBuffer%601) instead of native collection types (that is, `Vector`,`float[]`).</span></span>

```csharp
// Get DataViewSchema of IDataView
DataViewSchema columns = data.Schema;

// Create DataViewCursor
using (DataViewRowCursor cursor = data.GetRowCursor(columns))
{
    // Define variables where extracted values will be stored to
    float size = default;
    VBuffer<float> historicalPrices = default;
    float currentPrice = default;

    // Define delegates for extracting values from columns
    ValueGetter<float> sizeDelegate = cursor.GetGetter<float>(columns[0]);
    ValueGetter<VBuffer<float>> historicalPriceDelegate = cursor.GetGetter<VBuffer<float>>(columns[1]);
    ValueGetter<float> currentPriceDelegate = cursor.GetGetter<float>(columns[2]);

    // Iterate over each row
    while (cursor.MoveNext())
    {
        //Get values from respective columns
        sizeDelegate.Invoke(ref size);
        historicalPriceDelegate.Invoke(ref historicalPrices);
        currentPriceDelegate.Invoke(ref currentPrice);
    }
}
```

## <a name="preview-result-of-pre-processing-or-training-on-a-subset-of-the-data"></a><span data-ttu-id="90e6c-126">Podgląd wyniku wstępnego przetwarzania lub szkoleń dotyczących podzestawu danych</span><span class="sxs-lookup"><span data-stu-id="90e6c-126">Preview result of pre-processing or training on a subset of the data</span></span>

> [!WARNING]
> <span data-ttu-id="90e6c-127">Nie należy używać `Preview` w kodzie produkcyjnym, ponieważ jest on przeznaczony do debugowania i może obniżyć wydajność.</span><span class="sxs-lookup"><span data-stu-id="90e6c-127">Do not use `Preview` in production code because it is intended for debugging and may reduce performance.</span></span>

<span data-ttu-id="90e6c-128">Proces konstruowania modelu jest eksperymentalny i iteracyjny.</span><span class="sxs-lookup"><span data-stu-id="90e6c-128">The model building process is experimental and iterative.</span></span> <span data-ttu-id="90e6c-129">Aby sprawdzić, jakie dane będą wyglądały po przetworzeniu wstępnego przetwarzania lub uczeniu modelu uczenia maszynowego na podzestawie danych, użyj [`Preview`](xref:Microsoft.ML.DebuggerExtensions.Preview%2A) metody, która zwraca [`DataDebuggerPreview`](xref:Microsoft.ML.Data.DataDebuggerPreview) .</span><span class="sxs-lookup"><span data-stu-id="90e6c-129">To preview what data would look like after pre-processing or training a machine learning model on a subset of the data, use the [`Preview`](xref:Microsoft.ML.DebuggerExtensions.Preview%2A) method which returns a [`DataDebuggerPreview`](xref:Microsoft.ML.Data.DataDebuggerPreview).</span></span> <span data-ttu-id="90e6c-130">Wynikiem jest obiekt z `ColumnView` i właściwości, `RowView` które są zarówno [`IEnumerable`](xref:System.Collections.Generic.IEnumerable%601) i zawierają wartości w określonej kolumnie lub wierszu.</span><span class="sxs-lookup"><span data-stu-id="90e6c-130">The result is an object with `ColumnView` and `RowView` properties which are both an [`IEnumerable`](xref:System.Collections.Generic.IEnumerable%601) and contain the values in a particular column or row.</span></span> <span data-ttu-id="90e6c-131">Określ liczbę wierszy, do których mają zostać zastosowane przekształcenia z `maxRows` parametrem.</span><span class="sxs-lookup"><span data-stu-id="90e6c-131">Specify the number of rows to apply the transformation to with the `maxRows` parameter.</span></span>

![Obiekt podglądu debugera danych](./media/inspect-intermediate-data-ml-net/data-debugger-preview-01.png)

<span data-ttu-id="90e6c-133">Wynik inspekcji [`IDataView`](xref:Microsoft.ML.IDataView) będzie wyglądać podobnie do poniższego:</span><span class="sxs-lookup"><span data-stu-id="90e6c-133">The result of inspecting an [`IDataView`](xref:Microsoft.ML.IDataView) would look similar to the following:</span></span>

![Widok wiersza podglądu debugera danych](./media/inspect-intermediate-data-ml-net/data-debugger-preview-02.png)
