---
title: Używanie zmiennych emisji w programie .NET dla Apache Spark
description: Dowiedz się, jak używać zmiennych emisji w programie .NET dla aplikacji Apache Spark.
ms.author: nidutta
author: Niharikadutta
ms.date: 10/09/2020
ms.topic: conceptual
ms.custom: mvc,how-to
ms.openlocfilehash: ca6dab01cbd639594da0b51f145272a9a150e93c
ms.sourcegitcommit: 34968a61e9bac0f6be23ed6ffb837f52d2390c85
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/17/2020
ms.locfileid: "94687756"
---
# <a name="use-broadcast-variables-in-net-for-apache-spark"></a><span data-ttu-id="97418-103">Używanie zmiennych emisji w programie .NET dla Apache Spark</span><span class="sxs-lookup"><span data-stu-id="97418-103">Use broadcast variables in .NET for Apache Spark</span></span>

<span data-ttu-id="97418-104">W tym artykule dowiesz się, jak używać zmiennych emisji w programie .NET dla Apache Spark.</span><span class="sxs-lookup"><span data-stu-id="97418-104">In this article, you learn how to use broadcast variables in .NET for Apache Spark.</span></span> <span data-ttu-id="97418-105">[Zmienne emisji w Apache Spark](https://spark.apache.org/docs/2.2.0/rdd-programming-guide.html#broadcast-variables) są mechanizmami do udostępniania zmiennych w ramach wykonawców, które są przeznaczone tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="97418-105">[Broadcast variables in Apache Spark](https://spark.apache.org/docs/2.2.0/rdd-programming-guide.html#broadcast-variables) are mechanisms for sharing variables across executors that are meant to be read-only.</span></span> <span data-ttu-id="97418-106">Zmienne emisji umożliwiają zachowanie zmiennej tylko do odczytu w pamięci podręcznej na poszczególnych maszynach, a nie dostarczenie kopii jej z zadaniami.</span><span class="sxs-lookup"><span data-stu-id="97418-106">Broadcast variables allow you to keep a read-only variable cached on each machine rather than shipping a copy of it with tasks.</span></span> <span data-ttu-id="97418-107">Zmiennych emisji można użyć, aby przydzielić każdemu węzłowi kopię dużego wejściowego zestawu danych w efektywny sposób.</span><span class="sxs-lookup"><span data-stu-id="97418-107">You can use broadcast variables to give every node a copy of a large input dataset in an efficient manner.</span></span>

<span data-ttu-id="97418-108">Ponieważ dane są wysyłane tylko raz, zmienne emisji mają korzyści z wydajności w porównaniu do zmiennych lokalnych, które są wysyłane do modułów wykonujących wszystkie zadania.</span><span class="sxs-lookup"><span data-stu-id="97418-108">Because the data is sent only once, broadcast variables have performance benefits when compared to local variables that are shipped to the executors with each task.</span></span> <span data-ttu-id="97418-109">Zapoznaj się z [dokumentacją oficjalną zmienna emisji](https://spark.apache.org/docs/2.2.0/rdd-programming-guide.html#broadcast-variables) , aby lepiej zrozumieć zmienne emisji i dlaczego są one używane.</span><span class="sxs-lookup"><span data-stu-id="97418-109">Refer to the [official broadcast variable documentation](https://spark.apache.org/docs/2.2.0/rdd-programming-guide.html#broadcast-variables) to get a deeper understanding of broadcast variables and why they are used.</span></span>

## <a name="create-broadcast-variables"></a><span data-ttu-id="97418-110">Utwórz zmienne emisji</span><span class="sxs-lookup"><span data-stu-id="97418-110">Create broadcast variables</span></span>

<span data-ttu-id="97418-111">Aby utworzyć zmienną emisji, wywołaj `SparkContext.Broadcast(v)` dla każdej zmiennej `v` .</span><span class="sxs-lookup"><span data-stu-id="97418-111">To create a broadcast variable, call `SparkContext.Broadcast(v)` for any variable `v`.</span></span> <span data-ttu-id="97418-112">Zmienna emisji jest otoką wokół zmiennej `v` , a jej wartość jest dostępna poprzez wywołanie `Value()` metody.</span><span class="sxs-lookup"><span data-stu-id="97418-112">The broadcast variable is a wrapper around the variable `v`, and its value can be accessed by calling the `Value()` method.</span></span>

<span data-ttu-id="97418-113">W poniższym fragmencie kodu `v` zostanie utworzona zmienna ciągu, a zmienna emisji `bv` jest tworzona, gdy `SparkContext.Broadcast(v)` jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="97418-113">In the following code snippet, a string variable `v` is created, and a broadcast variable `bv` is created when `SparkContext.Broadcast(v)`is called.</span></span> <span data-ttu-id="97418-114">Zwróć uwagę na parametr typu dla parametru, który jest `Broadcast` zgodny z typem rozgłaszanej zmiennej.</span><span class="sxs-lookup"><span data-stu-id="97418-114">Notice the type parameter for `Broadcast`, string, matches the type of the variable being broadcasted.</span></span> <span data-ttu-id="97418-115">Funkcja zdefiniowana przez użytkownika (UDF) zwraca wartość `bv` .</span><span class="sxs-lookup"><span data-stu-id="97418-115">The user-defined function (UDF) returns the value of `bv`.</span></span>

```csharp
string v = "Variable to be broadcasted";
Broadcast<string> bv = SparkContext.Broadcast(v);

Func<Column, Column> udf = Udf<string, string>(
    str => $"{str}: {bv.Value()}");
```

## <a name="delete-broadcast-variables"></a><span data-ttu-id="97418-116">Usuń zmienne emisji</span><span class="sxs-lookup"><span data-stu-id="97418-116">Delete broadcast variables</span></span>

<span data-ttu-id="97418-117">Zmienną emisji można usunąć ze wszystkich modułów wykonujących, wywołując `Destroy()` metodę.</span><span class="sxs-lookup"><span data-stu-id="97418-117">The broadcast variable can be deleted from all executors by calling the `Destroy()` method.</span></span>

```csharp
bv.Destroy();
```

<span data-ttu-id="97418-118">`Destroy()` usuwa wszystkie dane i metadane związane ze zmienną emisji i powinny być używane z zachowaniem ostrożności.</span><span class="sxs-lookup"><span data-stu-id="97418-118">`Destroy()` deletes all data and metadata related to the broadcast variable and should be used with caution.</span></span> <span data-ttu-id="97418-119">Gdy zmienna emisji zostanie zniszczona, nie można jej użyć ponownie.</span><span class="sxs-lookup"><span data-stu-id="97418-119">Once a broadcast variable is destroyed, it can't be used again.</span></span>

## <a name="limit-broadcast-variable-scope-in-udfs"></a><span data-ttu-id="97418-120">Ogranicz zakres zmiennej emisji w UDF</span><span class="sxs-lookup"><span data-stu-id="97418-120">Limit broadcast variable scope in UDFs</span></span>

<span data-ttu-id="97418-121">W przypadku używania zmiennych emisji w UDF należy ograniczyć zakres zmiennej tylko do formatu UDF, który odwołuje się do zmiennej.</span><span class="sxs-lookup"><span data-stu-id="97418-121">When you use broadcast variables in UDFs, you need to limit the scope of the variable to only the UDF that is referencing the variable.</span></span> <span data-ttu-id="97418-122">[Przewodnik po użyciu UDF](udf-guide.md) zawiera szczegółowy opis tego zjawiska.</span><span class="sxs-lookup"><span data-stu-id="97418-122">The [guide to using UDFs](udf-guide.md) describes this phenomenon in detail.</span></span> <span data-ttu-id="97418-123">Zakres jest szczególnie decydujący podczas wywoływania `Destroy()` zmiennej emisji.</span><span class="sxs-lookup"><span data-stu-id="97418-123">Scope is especially crucial when you call `Destroy()` on the broadcast variable.</span></span>

<span data-ttu-id="97418-124">Jeśli zmienna emisji, która została zniszczona, jest widoczna dla innych UDF lub dostępna z niej, jest pobierana do serializacji przez wszystkie UDF, nawet jeśli nie odwołują się do nich.</span><span class="sxs-lookup"><span data-stu-id="97418-124">If the broadcast variable that has been destroyed is visible to or accessible from other UDFs, it gets picked up for serialization by all of the UDFs, even if it is not being referenced by them.</span></span> <span data-ttu-id="97418-125">Platforma .NET dla Apache Spark nie może serializować zniszczonej zmiennej emisji, co spowoduje wystąpienie błędu.</span><span class="sxs-lookup"><span data-stu-id="97418-125">.NET for Apache Spark is unable to serialize the destroyed broadcast variable, which results in an error.</span></span> <span data-ttu-id="97418-126">Poniższy fragment kodu ilustruje ten błąd:</span><span class="sxs-lookup"><span data-stu-id="97418-126">The following code snippet demonstrates this error:</span></span>

```csharp
string v = "Variable to be broadcasted";
Broadcast<string> bv = SparkContext.Broadcast(v);

// Using the broadcast variable in a UDF:
Func<Column, Column> udf1 = Udf<string, string>(
    str => $"{str}: {bv.Value()}");

// Destroying bv
bv.Destroy();

// Calling udf1 after destroying bv throws the following expected exception:
// org.apache.spark.SparkException: Attempted to use Broadcast(0) after it was destroyed
df.Select(udf1(df["_1"])).Show();

// Different UDF udf2 that is not referencing bv
Func<Column, Column> udf2 = Udf<string, string>(
    str => $"{str}: not referencing broadcast variable");

// Calling udf2 throws the following (unexpected) exception:
// [Error] [JvmBridge] org.apache.spark.SparkException: Task not serializable
df.Select(udf2(df["_1"])).Show();
```

<span data-ttu-id="97418-127">Poniższy fragment kodu pokazuje, jak upewnić się, że niszczenie `bv` nie ma wpływu na `udf2` skutek nieoczekiwanego zachowania serializacji:</span><span class="sxs-lookup"><span data-stu-id="97418-127">The following code snippet demonstrates how to ensure that destroying `bv` doesn't affect `udf2` because of an unexpected serialization behavior:</span></span>

```csharp
string v = "Variable to be broadcasted";
// Restricting the visibility of bv to only the UDF referencing it
{
    Broadcast<string> bv = SparkContext.Broadcast(v);

    // Using the broadcast variable in a UDF:
    Func<Column, Column> udf1 = Udf<string, string>(
        str => $"{str}: {bv.Value()}");

    // Destroying bv
    bv.Destroy();
}

// Different UDF udf2 that is not referencing bv
Func<Column, Column> udf2 = Udf<string, string>(
    str => $"{str}: not referencing broadcast variable");

// Calling udf2 works fine as expected
df.Select(udf2(df["_1"])).Show();
```

## <a name="faqs"></a><span data-ttu-id="97418-128">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="97418-128">FAQs</span></span>

<span data-ttu-id="97418-129">**Dlaczego zmienne nie są emitowane w programie .NET Interactive?**</span><span class="sxs-lookup"><span data-stu-id="97418-129">**Why don't Broadcast Variables work with .NET Interactive?**</span></span>  
<span data-ttu-id="97418-130">Zmienne emisji nie współpracują ze scenariuszami interaktywnymi ze względu na projekt środowiska .NET Interactive, który jest dołączany do każdego obiektu zdefiniowanego w komórce przy użyciu jego klasy przesłaniania komórki, która nie jest oznaczona jako możliwa do serializacji, kończy się niepowodzeniem</span><span class="sxs-lookup"><span data-stu-id="97418-130">Broadcast variables don't work with interactive scenarios because of .NET interactive's design of appending each object defined in a cell with its cell submission class, which since is not marked serializable, fails with the same exception as shown previously.</span></span> <span data-ttu-id="97418-131">Aby uzyskać więcej informacji, zapoznaj się z [tym artykułem](dotnet-interactive-udf-issue.md).</span><span class="sxs-lookup"><span data-stu-id="97418-131">For more information, please check out [this article](dotnet-interactive-udf-issue.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="97418-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="97418-132">Next steps</span></span>

* [<span data-ttu-id="97418-133">Wprowadzenie do platformy .NET dla Apache Spark</span><span class="sxs-lookup"><span data-stu-id="97418-133">Get started with .NET for Apache Spark</span></span>](../tutorials/get-started.md)
* [<span data-ttu-id="97418-134">Debugowanie aplikacji .NET dla Apache Spark w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="97418-134">Debug a .NET for Apache Spark application on Windows</span></span>](debug.md)
* [<span data-ttu-id="97418-135">Wdróż platformę .NET dla Apache Spark procesów roboczych i plików binarnych funkcji zdefiniowanych przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="97418-135">Deploy .NET for Apache Spark worker and user-defined function binaries</span></span>](deploy-worker-udf-binaries.md)
