---
title: Kolekcje (C#)
description: Informacje o kolekcjach w języku C#, które są używane do pracy z grupami obiektów. Kolekcje mogą być zwiększane i zmniejszane dynamicznie w miarę potrzeby zmiany aplikacji.
ms.date: 07/20/2015
ms.assetid: 317d7dc3-8587-4873-8b3e-556f86497939
ms.openlocfilehash: 2375980e2915d4daa5a221a94eee2aea41959852
ms.sourcegitcommit: 40de8df14289e1e05b40d6e5c1daabd3c286d70c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/22/2020
ms.locfileid: "86924932"
---
# <a name="collections-c"></a><span data-ttu-id="f00d9-104">Kolekcje (C#)</span><span class="sxs-lookup"><span data-stu-id="f00d9-104">Collections (C#)</span></span>

<span data-ttu-id="f00d9-105">W przypadku wielu aplikacji, należy utworzyć grupy powiązanych obiektów i zarządzać nimi.</span><span class="sxs-lookup"><span data-stu-id="f00d9-105">For many applications, you want to create and manage groups of related objects.</span></span> <span data-ttu-id="f00d9-106">Istnieją dwa sposoby grupowania obiektów: przez tworzenie tablic obiektów i tworzenie kolekcji obiektów.</span><span class="sxs-lookup"><span data-stu-id="f00d9-106">There are two ways to group objects: by creating arrays of objects, and by creating collections of objects.</span></span>

<span data-ttu-id="f00d9-107">Tablice są najbardziej przydatne do tworzenia i pracy ze stałą liczbą obiektów silnie wpisanych.</span><span class="sxs-lookup"><span data-stu-id="f00d9-107">Arrays are most useful for creating and working with a fixed number of strongly typed objects.</span></span> <span data-ttu-id="f00d9-108">Aby uzyskać informacje na temat tablic, zobacz [tablice](../arrays/index.md).</span><span class="sxs-lookup"><span data-stu-id="f00d9-108">For information about arrays, see [Arrays](../arrays/index.md).</span></span>

<span data-ttu-id="f00d9-109">Kolekcje zapewniają bardziej elastyczny sposób pracy z grupami obiektów.</span><span class="sxs-lookup"><span data-stu-id="f00d9-109">Collections provide a more flexible way to work with groups of objects.</span></span> <span data-ttu-id="f00d9-110">W przeciwieństwie do tablic, Grupa obiektów, z którymi pracujesz, może być zwiększana i zmniejszana dynamicznie w miarę potrzeby zmiany aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f00d9-110">Unlike arrays, the group of objects you work with can grow and shrink dynamically as the needs of the application change.</span></span> <span data-ttu-id="f00d9-111">W przypadku niektórych kolekcji można przypisać klucz do dowolnego obiektu, który został umieszczony w kolekcji, dzięki czemu można szybko pobrać obiekt przy użyciu klucza.</span><span class="sxs-lookup"><span data-stu-id="f00d9-111">For some collections, you can assign a key to any object that you put into the collection so that you can quickly retrieve the object by using the key.</span></span>

<span data-ttu-id="f00d9-112">Kolekcja jest klasą, więc należy zadeklarować wystąpienie klasy, aby można było dodać elementy do tej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="f00d9-112">A collection is a class, so you must declare an instance of the class before you can add elements to that collection.</span></span>

<span data-ttu-id="f00d9-113">Jeśli kolekcja zawiera elementy tylko jednego typu danych, można użyć jednej z klas w <xref:System.Collections.Generic?displayProperty=nameWithType> przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="f00d9-113">If your collection contains elements of only one data type, you can use one of the classes in the <xref:System.Collections.Generic?displayProperty=nameWithType> namespace.</span></span> <span data-ttu-id="f00d9-114">Ogólna kolekcja wymusza bezpieczeństwo typu, tak aby nie można było dodać do niego żadnego innego typu danych.</span><span class="sxs-lookup"><span data-stu-id="f00d9-114">A generic collection enforces type safety so that no other data type can be added to it.</span></span> <span data-ttu-id="f00d9-115">Po pobraniu elementu z kolekcji ogólnej nie trzeba określać jego typu danych ani go przekonwertować.</span><span class="sxs-lookup"><span data-stu-id="f00d9-115">When you retrieve an element from a generic collection, you do not have to determine its data type or convert it.</span></span>

> [!NOTE]
> <span data-ttu-id="f00d9-116">Aby zapoznać się z przykładami w tym temacie, należy uwzględnić dyrektywy [using](../../language-reference/keywords/using-directive.md) dla `System.Collections.Generic` `System.Linq` przestrzeni nazw i.</span><span class="sxs-lookup"><span data-stu-id="f00d9-116">For the examples in this topic, include [using](../../language-reference/keywords/using-directive.md) directives for the `System.Collections.Generic` and `System.Linq` namespaces.</span></span>

 <span data-ttu-id="f00d9-117">**W tym temacie**</span><span class="sxs-lookup"><span data-stu-id="f00d9-117">**In this topic**</span></span>

- [<span data-ttu-id="f00d9-118">Korzystanie z prostej kolekcji</span><span class="sxs-lookup"><span data-stu-id="f00d9-118">Using a Simple Collection</span></span>](#BKMK_SimpleCollection)

- [<span data-ttu-id="f00d9-119">Rodzaje kolekcji</span><span class="sxs-lookup"><span data-stu-id="f00d9-119">Kinds of Collections</span></span>](#BKMK_KindsOfCollections)

  - [<span data-ttu-id="f00d9-120">Klasy System. Collections. Generic</span><span class="sxs-lookup"><span data-stu-id="f00d9-120">System.Collections.Generic Classes</span></span>](#BKMK_Generic)

  - [<span data-ttu-id="f00d9-121">Klasy System. Collections. współbieżne</span><span class="sxs-lookup"><span data-stu-id="f00d9-121">System.Collections.Concurrent Classes</span></span>](#BKMK_Concurrent)

  - [<span data-ttu-id="f00d9-122">Klasy System. Collections</span><span class="sxs-lookup"><span data-stu-id="f00d9-122">System.Collections Classes</span></span>](#BKMK_Collections)

- [<span data-ttu-id="f00d9-123">Implementowanie kolekcji par klucz/wartość</span><span class="sxs-lookup"><span data-stu-id="f00d9-123">Implementing a Collection of Key/Value Pairs</span></span>](#BKMK_KeyValuePairs)

- [<span data-ttu-id="f00d9-124">Używanie LINQ do uzyskiwania dostępu do kolekcji</span><span class="sxs-lookup"><span data-stu-id="f00d9-124">Using LINQ to Access a Collection</span></span>](#BKMK_LINQ)

- [<span data-ttu-id="f00d9-125">Sortowanie kolekcji</span><span class="sxs-lookup"><span data-stu-id="f00d9-125">Sorting a Collection</span></span>](#BKMK_Sorting)

- [<span data-ttu-id="f00d9-126">Definiowanie kolekcji niestandardowej</span><span class="sxs-lookup"><span data-stu-id="f00d9-126">Defining a Custom Collection</span></span>](#BKMK_CustomCollection)

- [<span data-ttu-id="f00d9-127">Iteratory</span><span class="sxs-lookup"><span data-stu-id="f00d9-127">Iterators</span></span>](#BKMK_Iterators)

<a name="BKMK_SimpleCollection"></a>

## <a name="using-a-simple-collection"></a><span data-ttu-id="f00d9-128">Korzystanie z prostej kolekcji</span><span class="sxs-lookup"><span data-stu-id="f00d9-128">Using a Simple Collection</span></span>

<span data-ttu-id="f00d9-129">W przykładach w tej sekcji użyto klasy generycznej <xref:System.Collections.Generic.List%601> , która pozwala na współpracę z silnie wpisaną listą obiektów.</span><span class="sxs-lookup"><span data-stu-id="f00d9-129">The examples in this section use the generic <xref:System.Collections.Generic.List%601> class, which enables you to work with a strongly typed list of objects.</span></span>

<span data-ttu-id="f00d9-130">Poniższy przykład tworzy listę ciągów, a następnie iteruje przez ciągi przy użyciu instrukcji [foreach](../../language-reference/keywords/foreach-in.md) .</span><span class="sxs-lookup"><span data-stu-id="f00d9-130">The following example creates a list of strings and then iterates through the strings by using a [foreach](../../language-reference/keywords/foreach-in.md) statement.</span></span>

```csharp
// Create a list of strings.
var salmons = new List<string>();
salmons.Add("chinook");
salmons.Add("coho");
salmons.Add("pink");
salmons.Add("sockeye");

// Iterate through the list.
foreach (var salmon in salmons)
{
    Console.Write(salmon + " ");
}
// Output: chinook coho pink sockeye
```

<span data-ttu-id="f00d9-131">Jeśli zawartość kolekcji jest znana z wyprzedzeniem, można użyć *inicjatora kolekcji* w celu zainicjowania kolekcji.</span><span class="sxs-lookup"><span data-stu-id="f00d9-131">If the contents of a collection are known in advance, you can use a *collection initializer* to initialize the collection.</span></span> <span data-ttu-id="f00d9-132">Aby uzyskać więcej informacji, zobacz [Inicjatory obiektów i kolekcji](../classes-and-structs/object-and-collection-initializers.md).</span><span class="sxs-lookup"><span data-stu-id="f00d9-132">For more information, see [Object and Collection Initializers](../classes-and-structs/object-and-collection-initializers.md).</span></span>

<span data-ttu-id="f00d9-133">Poniższy przykład jest taki sam jak w poprzednim przykładzie, z wyjątkiem tego, że inicjator kolekcji jest używany do dodawania elementów do kolekcji.</span><span class="sxs-lookup"><span data-stu-id="f00d9-133">The following example is the same as the previous example, except a collection initializer is used to add elements to the collection.</span></span>

```csharp
// Create a list of strings by using a
// collection initializer.
var salmons = new List<string> { "chinook", "coho", "pink", "sockeye" };

// Iterate through the list.
foreach (var salmon in salmons)
{
    Console.Write(salmon + " ");
}
// Output: chinook coho pink sockeye
```

<span data-ttu-id="f00d9-134">Można użyć instrukcji [for](../../language-reference/keywords/for.md) zamiast `foreach` instrukcji, aby wykonać iterację w kolekcji.</span><span class="sxs-lookup"><span data-stu-id="f00d9-134">You can use a [for](../../language-reference/keywords/for.md) statement instead of a `foreach` statement to iterate through a collection.</span></span> <span data-ttu-id="f00d9-135">Można to osiągnąć, uzyskując dostęp do elementów kolekcji według pozycji indeksu.</span><span class="sxs-lookup"><span data-stu-id="f00d9-135">You accomplish this by accessing the collection elements by the index position.</span></span> <span data-ttu-id="f00d9-136">Indeks elementów zaczyna się od 0 i kończą się na liczbie elementów pomniejszonej o 1.</span><span class="sxs-lookup"><span data-stu-id="f00d9-136">The index of the elements starts at 0 and ends at the element count minus 1.</span></span>

<span data-ttu-id="f00d9-137">Poniższy przykład wykonuje iterację elementów kolekcji przy użyciu `for` zamiast `foreach` .</span><span class="sxs-lookup"><span data-stu-id="f00d9-137">The following example iterates through the elements of a collection by using `for` instead of `foreach`.</span></span>

```csharp
// Create a list of strings by using a
// collection initializer.
var salmons = new List<string> { "chinook", "coho", "pink", "sockeye" };

for (var index = 0; index < salmons.Count; index++)
{
    Console.Write(salmons[index] + " ");
}
// Output: chinook coho pink sockeye
```

<span data-ttu-id="f00d9-138">Poniższy przykład usuwa element z kolekcji przez określenie obiektu do usunięcia.</span><span class="sxs-lookup"><span data-stu-id="f00d9-138">The following example removes an element from the collection by specifying the object to remove.</span></span>

```csharp
// Create a list of strings by using a
// collection initializer.
var salmons = new List<string> { "chinook", "coho", "pink", "sockeye" };

// Remove an element from the list by specifying
// the object.
salmons.Remove("coho");

// Iterate through the list.
foreach (var salmon in salmons)
{
    Console.Write(salmon + " ");
}
// Output: chinook pink sockeye
```

<span data-ttu-id="f00d9-139">Poniższy przykład usuwa elementy z listy ogólnej.</span><span class="sxs-lookup"><span data-stu-id="f00d9-139">The following example removes elements from a generic list.</span></span> <span data-ttu-id="f00d9-140">Zamiast `foreach` instrukcji, instrukcja [for](../../language-reference/keywords/for.md) , która wykonuje iterację w kolejności malejącej, jest używana.</span><span class="sxs-lookup"><span data-stu-id="f00d9-140">Instead of a `foreach` statement, a [for](../../language-reference/keywords/for.md) statement that iterates in descending order is used.</span></span> <span data-ttu-id="f00d9-141">Wynika to z faktu, że <xref:System.Collections.Generic.List%601.RemoveAt%2A> Metoda powoduje, że elementy po usuniętym elemencie mają niższą wartość indeksu.</span><span class="sxs-lookup"><span data-stu-id="f00d9-141">This is because the <xref:System.Collections.Generic.List%601.RemoveAt%2A> method causes elements after a removed element to have a lower index value.</span></span>

```csharp
var numbers = new List<int> { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };

// Remove odd numbers.
for (var index = numbers.Count - 1; index >= 0; index--)
{
    if (numbers[index] % 2 == 1)
    {
        // Remove the element by specifying
        // the zero-based index in the list.
        numbers.RemoveAt(index);
    }
}

// Iterate through the list.
// A lambda expression is placed in the ForEach method
// of the List(T) object.
numbers.ForEach(
    number => Console.Write(number + " "));
// Output: 0 2 4 6 8
```

<span data-ttu-id="f00d9-142">Dla typu elementów w <xref:System.Collections.Generic.List%601> , można również zdefiniować własną klasę.</span><span class="sxs-lookup"><span data-stu-id="f00d9-142">For the type of elements in the <xref:System.Collections.Generic.List%601>, you can also define your own class.</span></span> <span data-ttu-id="f00d9-143">W poniższym przykładzie `Galaxy` Klasa, która jest używana przez program, <xref:System.Collections.Generic.List%601> jest zdefiniowana w kodzie.</span><span class="sxs-lookup"><span data-stu-id="f00d9-143">In the following example, the `Galaxy` class that is used by the <xref:System.Collections.Generic.List%601> is defined in the code.</span></span>

```csharp
private static void IterateThroughList()
{
    var theGalaxies = new List<Galaxy>
        {
            new Galaxy() { Name="Tadpole", MegaLightYears=400},
            new Galaxy() { Name="Pinwheel", MegaLightYears=25},
            new Galaxy() { Name="Milky Way", MegaLightYears=0},
            new Galaxy() { Name="Andromeda", MegaLightYears=3}
        };

    foreach (Galaxy theGalaxy in theGalaxies)
    {
        Console.WriteLine(theGalaxy.Name + "  " + theGalaxy.MegaLightYears);
    }

    // Output:
    //  Tadpole  400
    //  Pinwheel  25
    //  Milky Way  0
    //  Andromeda  3
}

public class Galaxy
{
    public string Name { get; set; }
    public int MegaLightYears { get; set; }
}
```

<a name="BKMK_KindsOfCollections"></a>

## <a name="kinds-of-collections"></a><span data-ttu-id="f00d9-144">Rodzaje kolekcji</span><span class="sxs-lookup"><span data-stu-id="f00d9-144">Kinds of Collections</span></span>

<span data-ttu-id="f00d9-145">Platforma .NET udostępnia wiele popularnych kolekcji.</span><span class="sxs-lookup"><span data-stu-id="f00d9-145">Many common collections are provided by .NET.</span></span> <span data-ttu-id="f00d9-146">Każdy typ kolekcji jest przeznaczony do określonego celu.</span><span class="sxs-lookup"><span data-stu-id="f00d9-146">Each type of collection is designed for a specific purpose.</span></span>

<span data-ttu-id="f00d9-147">Niektóre popularne klasy kolekcji zostały opisane w tej sekcji:</span><span class="sxs-lookup"><span data-stu-id="f00d9-147">Some of the common collection classes are described in this section:</span></span>

- <span data-ttu-id="f00d9-148"><xref:System.Collections.Generic>, klasy</span><span class="sxs-lookup"><span data-stu-id="f00d9-148"><xref:System.Collections.Generic> classes</span></span>

- <span data-ttu-id="f00d9-149"><xref:System.Collections.Concurrent>, klasy</span><span class="sxs-lookup"><span data-stu-id="f00d9-149"><xref:System.Collections.Concurrent> classes</span></span>

- <span data-ttu-id="f00d9-150"><xref:System.Collections>, klasy</span><span class="sxs-lookup"><span data-stu-id="f00d9-150"><xref:System.Collections> classes</span></span>

<a name="BKMK_Generic"></a>

### <a name="systemcollectionsgeneric-classes"></a><span data-ttu-id="f00d9-151">Klasy System. Collections. Generic</span><span class="sxs-lookup"><span data-stu-id="f00d9-151">System.Collections.Generic Classes</span></span>

<span data-ttu-id="f00d9-152">Można utworzyć ogólną kolekcję przy użyciu jednej z klas w <xref:System.Collections.Generic> przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="f00d9-152">You can create a generic collection by using one of the classes in the <xref:System.Collections.Generic> namespace.</span></span> <span data-ttu-id="f00d9-153">Kolekcja ogólna jest przydatna, gdy każdy element w kolekcji ma ten sam typ danych.</span><span class="sxs-lookup"><span data-stu-id="f00d9-153">A generic collection is useful when every item in the collection has the same data type.</span></span> <span data-ttu-id="f00d9-154">Ogólna kolekcja wymusza silne wpisywanie przez umożliwienie dodania tylko żądanego typu danych.</span><span class="sxs-lookup"><span data-stu-id="f00d9-154">A generic collection enforces strong typing by allowing only the desired data type to be added.</span></span>

<span data-ttu-id="f00d9-155">W poniższej tabeli wymieniono niektóre często używane klasy <xref:System.Collections.Generic?displayProperty=nameWithType> obszaru nazw:</span><span class="sxs-lookup"><span data-stu-id="f00d9-155">The following table lists some of the frequently used classes of the <xref:System.Collections.Generic?displayProperty=nameWithType> namespace:</span></span>

|<span data-ttu-id="f00d9-156">Klasa</span><span class="sxs-lookup"><span data-stu-id="f00d9-156">Class</span></span>|<span data-ttu-id="f00d9-157">Opis</span><span class="sxs-lookup"><span data-stu-id="f00d9-157">Description</span></span>|
|---|---|
|<xref:System.Collections.Generic.Dictionary%602>|<span data-ttu-id="f00d9-158">Reprezentuje kolekcję par klucz/wartość, które są zorganizowane na podstawie klucza.</span><span class="sxs-lookup"><span data-stu-id="f00d9-158">Represents a collection of key/value pairs that are organized based on the key.</span></span>|
|<xref:System.Collections.Generic.List%601>|<span data-ttu-id="f00d9-159">Reprezentuje listę obiektów, do których można uzyskać dostęp za pomocą indeksu.</span><span class="sxs-lookup"><span data-stu-id="f00d9-159">Represents a list of objects that can be accessed by index.</span></span> <span data-ttu-id="f00d9-160">Zapewnia metody wyszukiwania, sortowania i modyfikowania list.</span><span class="sxs-lookup"><span data-stu-id="f00d9-160">Provides methods to search, sort, and modify lists.</span></span>|
|<xref:System.Collections.Generic.Queue%601>|<span data-ttu-id="f00d9-161">Przedstawia kolekcję obiektów First In, First Out (FIFO).</span><span class="sxs-lookup"><span data-stu-id="f00d9-161">Represents a first in, first out (FIFO) collection of objects.</span></span>|
|<xref:System.Collections.Generic.SortedList%602>|<span data-ttu-id="f00d9-162">Reprezentuje kolekcję par klucz/wartość, które są posortowane według klucza w oparciu o skojarzoną <xref:System.Collections.Generic.IComparer%601> implementację.</span><span class="sxs-lookup"><span data-stu-id="f00d9-162">Represents a collection of key/value pairs that are sorted by key based on the associated <xref:System.Collections.Generic.IComparer%601> implementation.</span></span>|
|<xref:System.Collections.Generic.Stack%601>|<span data-ttu-id="f00d9-163">Przedstawia kolekcję obiektów w ostatniej pierwszej, wychodzącej (LIFO).</span><span class="sxs-lookup"><span data-stu-id="f00d9-163">Represents a last in, first out (LIFO) collection of objects.</span></span>|

<span data-ttu-id="f00d9-164">Aby uzyskać dodatkowe informacje, zobacz [często używane typy kolekcji](../../../standard/collections/commonly-used-collection-types.md), [wybór klasy kolekcji](../../../standard/collections/selecting-a-collection-class.md)i <xref:System.Collections.Generic> .</span><span class="sxs-lookup"><span data-stu-id="f00d9-164">For additional information, see [Commonly Used Collection Types](../../../standard/collections/commonly-used-collection-types.md), [Selecting a Collection Class](../../../standard/collections/selecting-a-collection-class.md), and <xref:System.Collections.Generic>.</span></span>

<a name="BKMK_Concurrent"></a>

### <a name="systemcollectionsconcurrent-classes"></a><span data-ttu-id="f00d9-165">Klasy System. Collections. współbieżne</span><span class="sxs-lookup"><span data-stu-id="f00d9-165">System.Collections.Concurrent Classes</span></span>

<span data-ttu-id="f00d9-166">W .NET Framework 4 i nowszych wersjach kolekcje w <xref:System.Collections.Concurrent> przestrzeni nazw zapewniają wydajne, bezpieczne dla wątków operacje umożliwiające dostęp do elementów kolekcji z wielu wątków.</span><span class="sxs-lookup"><span data-stu-id="f00d9-166">In .NET Framework 4 and later versions, the collections in the <xref:System.Collections.Concurrent> namespace provide efficient thread-safe operations for accessing collection items from multiple threads.</span></span>

<span data-ttu-id="f00d9-167">Klasy w <xref:System.Collections.Concurrent> przestrzeni nazw powinny być używane zamiast odpowiednich typów w <xref:System.Collections.Generic?displayProperty=nameWithType> <xref:System.Collections?displayProperty=nameWithType> przestrzeniach nazw i za każdym razem, gdy wiele wątków uzyskuje dostęp do kolekcji współbieżnie.</span><span class="sxs-lookup"><span data-stu-id="f00d9-167">The classes in the <xref:System.Collections.Concurrent> namespace should be used instead of the corresponding types in the <xref:System.Collections.Generic?displayProperty=nameWithType> and <xref:System.Collections?displayProperty=nameWithType> namespaces whenever multiple threads are accessing the collection concurrently.</span></span> <span data-ttu-id="f00d9-168">Aby uzyskać więcej informacji, zobacz [kolekcje bezpieczne dla wątków](../../../standard/collections/thread-safe/index.md) i <xref:System.Collections.Concurrent> .</span><span class="sxs-lookup"><span data-stu-id="f00d9-168">For more information, see [Thread-Safe Collections](../../../standard/collections/thread-safe/index.md) and <xref:System.Collections.Concurrent>.</span></span>

<span data-ttu-id="f00d9-169">Niektóre klasy zawarte w <xref:System.Collections.Concurrent> przestrzeni nazw to <xref:System.Collections.Concurrent.BlockingCollection%601> , <xref:System.Collections.Concurrent.ConcurrentDictionary%602> , <xref:System.Collections.Concurrent.ConcurrentQueue%601> , i <xref:System.Collections.Concurrent.ConcurrentStack%601> .</span><span class="sxs-lookup"><span data-stu-id="f00d9-169">Some classes included in the <xref:System.Collections.Concurrent> namespace are <xref:System.Collections.Concurrent.BlockingCollection%601>, <xref:System.Collections.Concurrent.ConcurrentDictionary%602>, <xref:System.Collections.Concurrent.ConcurrentQueue%601>, and <xref:System.Collections.Concurrent.ConcurrentStack%601>.</span></span>

<a name="BKMK_Collections"></a>

### <a name="systemcollections-classes"></a><span data-ttu-id="f00d9-170">Klasy System. Collections</span><span class="sxs-lookup"><span data-stu-id="f00d9-170">System.Collections Classes</span></span>

<span data-ttu-id="f00d9-171">Klasy w <xref:System.Collections?displayProperty=nameWithType> przestrzeni nazw nie przechowują elementów jako obiektów o określonych typach, ale jako obiektów typu `Object` .</span><span class="sxs-lookup"><span data-stu-id="f00d9-171">The classes in the <xref:System.Collections?displayProperty=nameWithType> namespace do not store elements as specifically typed objects, but as objects of type `Object`.</span></span>

<span data-ttu-id="f00d9-172">Jeśli to możliwe, należy używać kolekcji ogólnych w <xref:System.Collections.Generic?displayProperty=nameWithType> przestrzeni nazw lub <xref:System.Collections.Concurrent> przestrzeni nazw zamiast starszych typów w `System.Collections` przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="f00d9-172">Whenever possible, you should use the generic collections in the <xref:System.Collections.Generic?displayProperty=nameWithType> namespace or the <xref:System.Collections.Concurrent> namespace instead of the legacy types in the `System.Collections` namespace.</span></span>

<span data-ttu-id="f00d9-173">W poniższej tabeli przedstawiono niektóre z najczęściej używanych klas w `System.Collections` przestrzeni nazw:</span><span class="sxs-lookup"><span data-stu-id="f00d9-173">The following table lists some of the frequently used classes in the `System.Collections` namespace:</span></span>

|<span data-ttu-id="f00d9-174">Klasa</span><span class="sxs-lookup"><span data-stu-id="f00d9-174">Class</span></span>|<span data-ttu-id="f00d9-175">Opis</span><span class="sxs-lookup"><span data-stu-id="f00d9-175">Description</span></span>|
|---|---|
|<xref:System.Collections.ArrayList>|<span data-ttu-id="f00d9-176">Reprezentuje tablicę obiektów, których rozmiar jest dynamicznie zwiększany w miarę potrzeb.</span><span class="sxs-lookup"><span data-stu-id="f00d9-176">Represents an array of objects whose size is dynamically increased as required.</span></span>|
|<xref:System.Collections.Hashtable>|<span data-ttu-id="f00d9-177">Reprezentuje kolekcję par klucz/wartość, które są zorganizowane na podstawie kodu skrótu klucza.</span><span class="sxs-lookup"><span data-stu-id="f00d9-177">Represents a collection of key/value pairs that are organized based on the hash code of the key.</span></span>|
|<xref:System.Collections.Queue>|<span data-ttu-id="f00d9-178">Przedstawia kolekcję obiektów First In, First Out (FIFO).</span><span class="sxs-lookup"><span data-stu-id="f00d9-178">Represents a first in, first out (FIFO) collection of objects.</span></span>|
|<xref:System.Collections.Stack>|<span data-ttu-id="f00d9-179">Przedstawia kolekcję obiektów w ostatniej pierwszej, wychodzącej (LIFO).</span><span class="sxs-lookup"><span data-stu-id="f00d9-179">Represents a last in, first out (LIFO) collection of objects.</span></span>|

<span data-ttu-id="f00d9-180"><xref:System.Collections.Specialized>Przestrzeń nazw udostępnia wyspecjalizowane i silnie typy kolekcji klas, takich jak kolekcje tylko do ciągów i powiązane z listą oraz słowniki hybrydowe.</span><span class="sxs-lookup"><span data-stu-id="f00d9-180">The <xref:System.Collections.Specialized> namespace provides specialized and strongly typed collection classes, such as string-only collections and linked-list and hybrid dictionaries.</span></span>

<a name="BKMK_KeyValuePairs"></a>

## <a name="implementing-a-collection-of-keyvalue-pairs"></a><span data-ttu-id="f00d9-181">Implementowanie kolekcji par klucz/wartość</span><span class="sxs-lookup"><span data-stu-id="f00d9-181">Implementing a Collection of Key/Value Pairs</span></span>

<span data-ttu-id="f00d9-182"><xref:System.Collections.Generic.Dictionary%602>Kolekcja ogólna umożliwia dostęp do elementów w kolekcji za pomocą klucza każdego elementu.</span><span class="sxs-lookup"><span data-stu-id="f00d9-182">The <xref:System.Collections.Generic.Dictionary%602> generic collection enables you to access to elements in a collection by using the key of each element.</span></span> <span data-ttu-id="f00d9-183">Każde dodanie do słownika składa się z wartości i skojarzonego z nim klucza.</span><span class="sxs-lookup"><span data-stu-id="f00d9-183">Each addition to the dictionary consists of a value and its associated key.</span></span> <span data-ttu-id="f00d9-184">Pobieranie wartości przy użyciu jej klucza jest szybkie, ponieważ `Dictionary` Klasa jest zaimplementowana jako tablica skrótów.</span><span class="sxs-lookup"><span data-stu-id="f00d9-184">Retrieving a value by using its key is fast because the `Dictionary` class is implemented as a hash table.</span></span>

<span data-ttu-id="f00d9-185">Poniższy przykład tworzy `Dictionary` kolekcję i wykonuje iterację w słowniku przy użyciu `foreach` instrukcji.</span><span class="sxs-lookup"><span data-stu-id="f00d9-185">The following example creates a `Dictionary` collection and iterates through the dictionary by using a `foreach` statement.</span></span>

```csharp
private static void IterateThruDictionary()
{
    Dictionary<string, Element> elements = BuildDictionary();

    foreach (KeyValuePair<string, Element> kvp in elements)
    {
        Element theElement = kvp.Value;

        Console.WriteLine("key: " + kvp.Key);
        Console.WriteLine("values: " + theElement.Symbol + " " +
            theElement.Name + " " + theElement.AtomicNumber);
    }
}

private static Dictionary<string, Element> BuildDictionary()
{
    var elements = new Dictionary<string, Element>();

    AddToDictionary(elements, "K", "Potassium", 19);
    AddToDictionary(elements, "Ca", "Calcium", 20);
    AddToDictionary(elements, "Sc", "Scandium", 21);
    AddToDictionary(elements, "Ti", "Titanium", 22);

    return elements;
}

private static void AddToDictionary(Dictionary<string, Element> elements,
    string symbol, string name, int atomicNumber)
{
    Element theElement = new Element();

    theElement.Symbol = symbol;
    theElement.Name = name;
    theElement.AtomicNumber = atomicNumber;

    elements.Add(key: theElement.Symbol, value: theElement);
}

public class Element
{
    public string Symbol { get; set; }
    public string Name { get; set; }
    public int AtomicNumber { get; set; }
}
```

<span data-ttu-id="f00d9-186">Aby zamiast tego użyć inicjatora kolekcji do skompilowania `Dictionary` kolekcji, można zamienić `BuildDictionary` `AddToDictionary` metody i przy użyciu następującej metody.</span><span class="sxs-lookup"><span data-stu-id="f00d9-186">To instead use a collection initializer to build the `Dictionary` collection, you can replace the `BuildDictionary` and `AddToDictionary` methods with the following method.</span></span>

```csharp
private static Dictionary<string, Element> BuildDictionary2()
{
    return new Dictionary<string, Element>
    {
        {"K",
            new Element() { Symbol="K", Name="Potassium", AtomicNumber=19}},
        {"Ca",
            new Element() { Symbol="Ca", Name="Calcium", AtomicNumber=20}},
        {"Sc",
            new Element() { Symbol="Sc", Name="Scandium", AtomicNumber=21}},
        {"Ti",
            new Element() { Symbol="Ti", Name="Titanium", AtomicNumber=22}}
    };
}
```

<span data-ttu-id="f00d9-187">W poniższym przykładzie zastosowano <xref:System.Collections.Generic.Dictionary%602.ContainsKey%2A> metodę i <xref:System.Collections.Generic.Dictionary%602.Item%2A> Właściwość, `Dictionary` Aby szybko znaleźć element według klucza.</span><span class="sxs-lookup"><span data-stu-id="f00d9-187">The following example uses the <xref:System.Collections.Generic.Dictionary%602.ContainsKey%2A> method and the <xref:System.Collections.Generic.Dictionary%602.Item%2A> property of `Dictionary` to quickly find an item by key.</span></span> <span data-ttu-id="f00d9-188">`Item`Właściwość umożliwia dostęp do elementu w `elements` kolekcji przy użyciu `elements[symbol]` języka C#.</span><span class="sxs-lookup"><span data-stu-id="f00d9-188">The `Item` property enables you to access an item in the `elements` collection by using the `elements[symbol]` in C#.</span></span>

```csharp
private static void FindInDictionary(string symbol)
{
    Dictionary<string, Element> elements = BuildDictionary();

    if (elements.ContainsKey(symbol) == false)
    {
        Console.WriteLine(symbol + " not found");
    }
    else
    {
        Element theElement = elements[symbol];
        Console.WriteLine("found: " + theElement.Name);
    }
}
```

<span data-ttu-id="f00d9-189">Poniższy przykład używa <xref:System.Collections.Generic.Dictionary%602.TryGetValue%2A> metody szybkie znajdowanie elementu według klucza.</span><span class="sxs-lookup"><span data-stu-id="f00d9-189">The following example instead uses the <xref:System.Collections.Generic.Dictionary%602.TryGetValue%2A> method quickly find an item by key.</span></span>

```csharp
private static void FindInDictionary2(string symbol)
{
    Dictionary<string, Element> elements = BuildDictionary();

    Element theElement = null;
    if (elements.TryGetValue(symbol, out theElement) == false)
        Console.WriteLine(symbol + " not found");
    else
        Console.WriteLine("found: " + theElement.Name);
}
```

<a name="BKMK_LINQ"></a>

## <a name="using-linq-to-access-a-collection"></a><span data-ttu-id="f00d9-190">Używanie LINQ do uzyskiwania dostępu do kolekcji</span><span class="sxs-lookup"><span data-stu-id="f00d9-190">Using LINQ to Access a Collection</span></span>

<span data-ttu-id="f00d9-191">LINQ (zapytanie zintegrowane z językiem) może służyć do uzyskiwania dostępu do kolekcji.</span><span class="sxs-lookup"><span data-stu-id="f00d9-191">LINQ (Language-Integrated Query) can be used to access collections.</span></span> <span data-ttu-id="f00d9-192">Zapytania LINQ zapewniają możliwości filtrowania, porządkowania i grupowania.</span><span class="sxs-lookup"><span data-stu-id="f00d9-192">LINQ queries provide filtering, ordering, and grouping capabilities.</span></span> <span data-ttu-id="f00d9-193">Aby uzyskać więcej informacji, zobacz [wprowadzenie z LINQ w języku C#](linq/index.md).</span><span class="sxs-lookup"><span data-stu-id="f00d9-193">For more information, see [Getting Started with LINQ in C#](linq/index.md).</span></span>

<span data-ttu-id="f00d9-194">Poniższy przykład wykonuje zapytanie LINQ względem ogólnego `List` .</span><span class="sxs-lookup"><span data-stu-id="f00d9-194">The following example runs a LINQ query against a generic `List`.</span></span> <span data-ttu-id="f00d9-195">Zapytanie LINQ zwraca inną kolekcję, która zawiera wyniki.</span><span class="sxs-lookup"><span data-stu-id="f00d9-195">The LINQ query returns a different collection that contains the results.</span></span>

```csharp
private static void ShowLINQ()
{
    List<Element> elements = BuildList();

    // LINQ Query.
    var subset = from theElement in elements
                 where theElement.AtomicNumber < 22
                 orderby theElement.Name
                 select theElement;

    foreach (Element theElement in subset)
    {
        Console.WriteLine(theElement.Name + " " + theElement.AtomicNumber);
    }

    // Output:
    //  Calcium 20
    //  Potassium 19
    //  Scandium 21
}

private static List<Element> BuildList()
{
    return new List<Element>
    {
        { new Element() { Symbol="K", Name="Potassium", AtomicNumber=19}},
        { new Element() { Symbol="Ca", Name="Calcium", AtomicNumber=20}},
        { new Element() { Symbol="Sc", Name="Scandium", AtomicNumber=21}},
        { new Element() { Symbol="Ti", Name="Titanium", AtomicNumber=22}}
    };
}

public class Element
{
    public string Symbol { get; set; }
    public string Name { get; set; }
    public int AtomicNumber { get; set; }
}
```

<a name="BKMK_Sorting"></a>

## <a name="sorting-a-collection"></a><span data-ttu-id="f00d9-196">Sortowanie kolekcji</span><span class="sxs-lookup"><span data-stu-id="f00d9-196">Sorting a Collection</span></span>

<span data-ttu-id="f00d9-197">Poniższy przykład ilustruje procedurę sortowania kolekcji.</span><span class="sxs-lookup"><span data-stu-id="f00d9-197">The following example illustrates a procedure for sorting a collection.</span></span> <span data-ttu-id="f00d9-198">Przykład sortuje wystąpienia `Car` klasy, które są przechowywane w <xref:System.Collections.Generic.List%601> .</span><span class="sxs-lookup"><span data-stu-id="f00d9-198">The example sorts instances of the `Car` class that are stored in a <xref:System.Collections.Generic.List%601>.</span></span> <span data-ttu-id="f00d9-199">`Car`Klasa implementuje <xref:System.IComparable%601> interfejs, który wymaga, aby <xref:System.IComparable%601.CompareTo%2A> Metoda została zaimplementowana.</span><span class="sxs-lookup"><span data-stu-id="f00d9-199">The `Car` class implements the <xref:System.IComparable%601> interface, which requires that the <xref:System.IComparable%601.CompareTo%2A> method be implemented.</span></span>

<span data-ttu-id="f00d9-200">Każde wywołanie <xref:System.IComparable%601.CompareTo%2A> metody wykonuje pojedyncze porównanie, które jest używane do sortowania.</span><span class="sxs-lookup"><span data-stu-id="f00d9-200">Each call to the <xref:System.IComparable%601.CompareTo%2A> method makes a single comparison that is used for sorting.</span></span> <span data-ttu-id="f00d9-201">Kod pisany przez użytkownika w `CompareTo` metodzie zwraca wartość dla każdego porównania bieżącego obiektu z innym obiektem.</span><span class="sxs-lookup"><span data-stu-id="f00d9-201">User-written code in the `CompareTo` method returns a value for each comparison of the current object with another object.</span></span> <span data-ttu-id="f00d9-202">Zwracana wartość jest mniejsza niż zero, jeśli bieżący obiekt jest mniejszy niż inny obiekt, większy niż zero, jeśli bieżący obiekt jest większy niż inny obiekt, i zero, jeśli są równe.</span><span class="sxs-lookup"><span data-stu-id="f00d9-202">The value returned is less than zero if the current object is less than the other object, greater than zero if the current object is greater than the other object, and zero if they are equal.</span></span> <span data-ttu-id="f00d9-203">Dzięki temu można zdefiniować w kodzie kryteria dla wartości większej niż, mniejszej niż i równej.</span><span class="sxs-lookup"><span data-stu-id="f00d9-203">This enables you to define in code the criteria for greater than, less than, and equal.</span></span>

<span data-ttu-id="f00d9-204">W `ListCars` metodzie `cars.Sort()` instrukcja sortuje listę.</span><span class="sxs-lookup"><span data-stu-id="f00d9-204">In the `ListCars` method, the `cars.Sort()` statement sorts the list.</span></span> <span data-ttu-id="f00d9-205">To wywołanie <xref:System.Collections.Generic.List%601.Sort%2A> metody <xref:System.Collections.Generic.List%601> powoduje `CompareTo` automatyczne wywoływanie metody dla `Car` obiektów w obiekcie `List` .</span><span class="sxs-lookup"><span data-stu-id="f00d9-205">This call to the <xref:System.Collections.Generic.List%601.Sort%2A> method of the <xref:System.Collections.Generic.List%601> causes the `CompareTo` method to be called automatically for the `Car` objects in the `List`.</span></span>

```csharp
private static void ListCars()
{
    var cars = new List<Car>
    {
        { new Car() { Name = "car1", Color = "blue", Speed = 20}},
        { new Car() { Name = "car2", Color = "red", Speed = 50}},
        { new Car() { Name = "car3", Color = "green", Speed = 10}},
        { new Car() { Name = "car4", Color = "blue", Speed = 50}},
        { new Car() { Name = "car5", Color = "blue", Speed = 30}},
        { new Car() { Name = "car6", Color = "red", Speed = 60}},
        { new Car() { Name = "car7", Color = "green", Speed = 50}}
    };

    // Sort the cars by color alphabetically, and then by speed
    // in descending order.
    cars.Sort();

    // View all of the cars.
    foreach (Car thisCar in cars)
    {
        Console.Write(thisCar.Color.PadRight(5) + " ");
        Console.Write(thisCar.Speed.ToString() + " ");
        Console.Write(thisCar.Name);
        Console.WriteLine();
    }

    // Output:
    //  blue  50 car4
    //  blue  30 car5
    //  blue  20 car1
    //  green 50 car7
    //  green 10 car3
    //  red   60 car6
    //  red   50 car2
}

public class Car : IComparable<Car>
{
    public string Name { get; set; }
    public int Speed { get; set; }
    public string Color { get; set; }

    public int CompareTo(Car other)
    {
        // A call to this method makes a single comparison that is
        // used for sorting.

        // Determine the relative order of the objects being compared.
        // Sort by color alphabetically, and then by speed in
        // descending order.

        // Compare the colors.
        int compare;
        compare = String.Compare(this.Color, other.Color, true);

        // If the colors are the same, compare the speeds.
        if (compare == 0)
        {
            compare = this.Speed.CompareTo(other.Speed);

            // Use descending order for speed.
            compare = -compare;
        }

        return compare;
    }
}
```

<a name="BKMK_CustomCollection"></a>

## <a name="defining-a-custom-collection"></a><span data-ttu-id="f00d9-206">Definiowanie kolekcji niestandardowej</span><span class="sxs-lookup"><span data-stu-id="f00d9-206">Defining a Custom Collection</span></span>

<span data-ttu-id="f00d9-207">Kolekcję można zdefiniować przez implementację <xref:System.Collections.Generic.IEnumerable%601> <xref:System.Collections.IEnumerable> interfejsu lub.</span><span class="sxs-lookup"><span data-stu-id="f00d9-207">You can define a collection by implementing the <xref:System.Collections.Generic.IEnumerable%601> or <xref:System.Collections.IEnumerable> interface.</span></span>

<span data-ttu-id="f00d9-208">Chociaż można zdefiniować kolekcję niestandardową, zazwyczaj lepiej jest używać kolekcji zawartych w programie .NET, które są opisane w [rodzaju kolekcje](#BKMK_KindsOfCollections) wcześniej w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="f00d9-208">Although you can define a custom collection, it is usually better to instead use the collections that are included in .NET, which are described in [Kinds of Collections](#BKMK_KindsOfCollections) earlier in this article.</span></span>

<span data-ttu-id="f00d9-209">W poniższym przykładzie zdefiniowano klasę kolekcji niestandardowej o nazwie `AllColors` .</span><span class="sxs-lookup"><span data-stu-id="f00d9-209">The following example defines a custom collection class named `AllColors`.</span></span> <span data-ttu-id="f00d9-210">Ta klasa implementuje <xref:System.Collections.IEnumerable> interfejs, który wymaga, aby <xref:System.Collections.IEnumerable.GetEnumerator%2A> Metoda została zaimplementowana.</span><span class="sxs-lookup"><span data-stu-id="f00d9-210">This class implements the <xref:System.Collections.IEnumerable> interface, which requires that the <xref:System.Collections.IEnumerable.GetEnumerator%2A> method be implemented.</span></span>

<span data-ttu-id="f00d9-211">`GetEnumerator`Metoda zwraca wystąpienie `ColorEnumerator` klasy.</span><span class="sxs-lookup"><span data-stu-id="f00d9-211">The `GetEnumerator` method returns an instance of the `ColorEnumerator` class.</span></span> <span data-ttu-id="f00d9-212">`ColorEnumerator`implementuje <xref:System.Collections.IEnumerator> interfejs, który wymaga <xref:System.Collections.IEnumerator.Current%2A> <xref:System.Collections.IEnumerator.MoveNext%2A> zaimplementowania właściwości, metody i <xref:System.Collections.IEnumerator.Reset%2A> metody.</span><span class="sxs-lookup"><span data-stu-id="f00d9-212">`ColorEnumerator` implements the <xref:System.Collections.IEnumerator> interface, which requires that the <xref:System.Collections.IEnumerator.Current%2A> property, <xref:System.Collections.IEnumerator.MoveNext%2A> method, and <xref:System.Collections.IEnumerator.Reset%2A> method be implemented.</span></span>

```csharp
private static void ListColors()
{
    var colors = new AllColors();

    foreach (Color theColor in colors)
    {
        Console.Write(theColor.Name + " ");
    }
    Console.WriteLine();
    // Output: red blue green
}

// Collection class.
public class AllColors : System.Collections.IEnumerable
{
    Color[] _colors =
    {
        new Color() { Name = "red" },
        new Color() { Name = "blue" },
        new Color() { Name = "green" }
    };

    public System.Collections.IEnumerator GetEnumerator()
    {
        return new ColorEnumerator(_colors);

        // Instead of creating a custom enumerator, you could
        // use the GetEnumerator of the array.
        //return _colors.GetEnumerator();
    }

    // Custom enumerator.
    private class ColorEnumerator : System.Collections.IEnumerator
    {
        private Color[] _colors;
        private int _position = -1;

        public ColorEnumerator(Color[] colors)
        {
            _colors = colors;
        }

        object System.Collections.IEnumerator.Current
        {
            get
            {
                return _colors[_position];
            }
        }

        bool System.Collections.IEnumerator.MoveNext()
        {
            _position++;
            return (_position < _colors.Length);
        }

        void System.Collections.IEnumerator.Reset()
        {
            _position = -1;
        }
    }
}

// Element class.
public class Color
{
    public string Name { get; set; }
}
```

<a name="BKMK_Iterators"></a>

## <a name="iterators"></a><span data-ttu-id="f00d9-213">Iteratory</span><span class="sxs-lookup"><span data-stu-id="f00d9-213">Iterators</span></span>

<span data-ttu-id="f00d9-214">*Iterator* jest używany do wykonywania niestandardowej iteracji w kolekcji.</span><span class="sxs-lookup"><span data-stu-id="f00d9-214">An *iterator* is used to perform a custom iteration over a collection.</span></span> <span data-ttu-id="f00d9-215">Iterator może być metodą lub `get` akcesorem.</span><span class="sxs-lookup"><span data-stu-id="f00d9-215">An iterator can be a method or a `get` accessor.</span></span> <span data-ttu-id="f00d9-216">Iterator używa instrukcji [yield return](../../language-reference/keywords/yield.md) , aby zwrócić każdy element kolekcji pojedynczo.</span><span class="sxs-lookup"><span data-stu-id="f00d9-216">An iterator uses a [yield return](../../language-reference/keywords/yield.md) statement to return each element of the collection one at a time.</span></span>

<span data-ttu-id="f00d9-217">Należy wywołać iterator przy użyciu instrukcji [foreach](../../language-reference/keywords/foreach-in.md) .</span><span class="sxs-lookup"><span data-stu-id="f00d9-217">You call an iterator by using a [foreach](../../language-reference/keywords/foreach-in.md) statement.</span></span> <span data-ttu-id="f00d9-218">Każda iteracja `foreach` pętli wywołuje iterator.</span><span class="sxs-lookup"><span data-stu-id="f00d9-218">Each iteration of the `foreach` loop calls the iterator.</span></span> <span data-ttu-id="f00d9-219">Po `yield return` osiągnięciu instrukcji w iteratorze zwracane jest wyrażenie, a bieżąca lokalizacja w kodzie jest zachowywana.</span><span class="sxs-lookup"><span data-stu-id="f00d9-219">When a `yield return` statement is reached in the iterator, an expression is returned, and the current location in code is retained.</span></span> <span data-ttu-id="f00d9-220">Wykonanie jest uruchamiane ponownie z tej lokalizacji przy następnym wywołaniu iteratora.</span><span class="sxs-lookup"><span data-stu-id="f00d9-220">Execution is restarted from that location the next time that the iterator is called.</span></span>

<span data-ttu-id="f00d9-221">Aby uzyskać więcej informacji, zobacz [Iteratory (C#)](./iterators.md).</span><span class="sxs-lookup"><span data-stu-id="f00d9-221">For more information, see [Iterators (C#)](./iterators.md).</span></span>

<span data-ttu-id="f00d9-222">W poniższym przykładzie zastosowano metodę iteratora.</span><span class="sxs-lookup"><span data-stu-id="f00d9-222">The following example uses an iterator method.</span></span> <span data-ttu-id="f00d9-223">Metoda iteratora zawiera `yield return` instrukcję, która znajduje się wewnątrz pętli [for](../../language-reference/keywords/for.md) .</span><span class="sxs-lookup"><span data-stu-id="f00d9-223">The iterator method has a `yield return` statement that is inside a [for](../../language-reference/keywords/for.md) loop.</span></span> <span data-ttu-id="f00d9-224">W `ListEvenNumbers` metodzie każda iteracja `foreach` treści instrukcji tworzy wywołanie metody iteratora, która przechodzi do następnej `yield return` instrukcji.</span><span class="sxs-lookup"><span data-stu-id="f00d9-224">In the `ListEvenNumbers` method, each iteration of the `foreach` statement body creates a call to the iterator method, which proceeds to the next `yield return` statement.</span></span>

```csharp
private static void ListEvenNumbers()
{
    foreach (int number in EvenSequence(5, 18))
    {
        Console.Write(number.ToString() + " ");
    }
    Console.WriteLine();
    // Output: 6 8 10 12 14 16 18
}

private static IEnumerable<int> EvenSequence(
    int firstNumber, int lastNumber)
{
    // Yield even numbers in the range.
    for (var number = firstNumber; number <= lastNumber; number++)
    {
        if (number % 2 == 0)
        {
            yield return number;
        }
    }
}
```

## <a name="see-also"></a><span data-ttu-id="f00d9-225">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="f00d9-225">See also</span></span>

- [<span data-ttu-id="f00d9-226">Inicjatory obiektów i kolekcji</span><span class="sxs-lookup"><span data-stu-id="f00d9-226">Object and Collection Initializers</span></span>](../classes-and-structs/object-and-collection-initializers.md)
- [<span data-ttu-id="f00d9-227">Koncepcje programowania (C#)</span><span class="sxs-lookup"><span data-stu-id="f00d9-227">Programming Concepts (C#)</span></span>](./index.md)
- [<span data-ttu-id="f00d9-228">Option Strict — Instrukcja</span><span class="sxs-lookup"><span data-stu-id="f00d9-228">Option Strict Statement</span></span>](../../../visual-basic/language-reference/statements/option-strict-statement.md)
- [<span data-ttu-id="f00d9-229">LINQ to Objects (C#)</span><span class="sxs-lookup"><span data-stu-id="f00d9-229">LINQ to Objects (C#)</span></span>](./linq/linq-to-objects.md)
- [<span data-ttu-id="f00d9-230">Równoległe LINQ (PLINQ)</span><span class="sxs-lookup"><span data-stu-id="f00d9-230">Parallel LINQ (PLINQ)</span></span>](../../../standard/parallel-programming/introduction-to-plinq.md)
- [<span data-ttu-id="f00d9-231">Kolekcje i struktury danych</span><span class="sxs-lookup"><span data-stu-id="f00d9-231">Collections and Data Structures</span></span>](../../../standard/collections/index.md)
- [<span data-ttu-id="f00d9-232">Wybieranie klasy kolekcji</span><span class="sxs-lookup"><span data-stu-id="f00d9-232">Selecting a Collection Class</span></span>](../../../standard/collections/selecting-a-collection-class.md)
- [<span data-ttu-id="f00d9-233">Porównania i sortowania w kolekcjach</span><span class="sxs-lookup"><span data-stu-id="f00d9-233">Comparisons and Sorts Within Collections</span></span>](../../../standard/collections/comparisons-and-sorts-within-collections.md)
- [<span data-ttu-id="f00d9-234">Kiedy należy używać kolekcji ogólnych</span><span class="sxs-lookup"><span data-stu-id="f00d9-234">When to Use Generic Collections</span></span>](../../../standard/collections/when-to-use-generic-collections.md)
