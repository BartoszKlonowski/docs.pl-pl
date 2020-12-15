---
title: Inicjowanie słownika z inicjatorem kolekcji — Przewodnik programowania w języku C#
description: Dowiedz się, jak zainicjować słownik w języku C# przy użyciu metody Add lub inicjatora indeksu. Ten przykład pokazuje obie opcje.
ms.date: 12/20/2018
helpviewer_keywords:
- collection initializers [C#], with Dictionary
ms.topic: how-to
ms.custom: contperf-fy21q2
ms.assetid: 25283922-f8ee-40dc-a639-fac30804ec71
ms.openlocfilehash: bcb9c5af215ff468812d08e93d37eecc40d745ea
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97513084"
---
# <a name="how-to-initialize-a-dictionary-with-a-collection-initializer-c-programming-guide"></a><span data-ttu-id="bb921-104">Inicjowanie słownika przy użyciu inicjatora kolekcji (Przewodnik programowania w języku C#)</span><span class="sxs-lookup"><span data-stu-id="bb921-104">How to initialize a dictionary with a collection initializer (C# Programming Guide)</span></span>

<span data-ttu-id="bb921-105">A <xref:System.Collections.Generic.Dictionary%602> zawiera kolekcję par klucz/wartość.</span><span class="sxs-lookup"><span data-stu-id="bb921-105">A <xref:System.Collections.Generic.Dictionary%602> contains a collection of key/value pairs.</span></span> <span data-ttu-id="bb921-106">Jego <xref:System.Collections.Generic.Dictionary%602.Add%2A> Metoda przyjmuje dwa parametry — jeden dla klucza i jeden dla tej wartości.</span><span class="sxs-lookup"><span data-stu-id="bb921-106">Its <xref:System.Collections.Generic.Dictionary%602.Add%2A> method takes two parameters, one for the key and one for the value.</span></span> <span data-ttu-id="bb921-107">Jednym ze sposobów na zainicjowanie <xref:System.Collections.Generic.Dictionary%602> lub dowolna kolekcja, której `Add` Metoda przyjmuje wiele parametrów, jest ujęcie każdego zestawu parametrów w nawiasach klamrowych, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="bb921-107">One way to initialize a <xref:System.Collections.Generic.Dictionary%602>, or any collection whose `Add` method takes multiple parameters, is to enclose each set of parameters in braces as shown in the following example.</span></span> <span data-ttu-id="bb921-108">Innym rozwiązaniem jest użycie inicjatora indeksu, również w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="bb921-108">Another option is to use an index initializer, also shown in the following example.</span></span>

## <a name="example"></a><span data-ttu-id="bb921-109">Przykład</span><span class="sxs-lookup"><span data-stu-id="bb921-109">Example</span></span>

<span data-ttu-id="bb921-110">W poniższym przykładzie kodu element <xref:System.Collections.Generic.Dictionary%602> jest inicjowany z wystąpieniami typu `StudentName` .</span><span class="sxs-lookup"><span data-stu-id="bb921-110">In the following code example, a <xref:System.Collections.Generic.Dictionary%602> is initialized with instances of type `StudentName`.</span></span>  <span data-ttu-id="bb921-111">Pierwsze inicjowanie używa `Add` metody z dwoma argumentami.</span><span class="sxs-lookup"><span data-stu-id="bb921-111">The first initialization uses the `Add` method with two arguments.</span></span> <span data-ttu-id="bb921-112">Kompilator generuje wywołanie `Add` dla każdej pary `int` kluczy i `StudentName` wartości.</span><span class="sxs-lookup"><span data-stu-id="bb921-112">The compiler generates a call to `Add` for each of the pairs of `int` keys and `StudentName` values.</span></span> <span data-ttu-id="bb921-113">Druga używa metody indeksu publicznego odczytu/zapisu `Dictionary` klasy:</span><span class="sxs-lookup"><span data-stu-id="bb921-113">The second uses a public read / write indexer method of the `Dictionary` class:</span></span>

[!code-csharp[InitializerExample](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/object-collection-initializers/HowToDictionaryInitializer.cs#HowToDictionaryInitializer)]  

<span data-ttu-id="bb921-114">Zwróć uwagę na dwie pary nawiasów klamrowych w każdym elemencie kolekcji w pierwszej deklaracji.</span><span class="sxs-lookup"><span data-stu-id="bb921-114">Note the two pairs of braces in each element of the collection in the first declaration.</span></span> <span data-ttu-id="bb921-115">Wewnętrzne nawiasy klamrowe otaczające inicjatora obiektów dla `StudentName` , a skrajne nawiasy klamrowe obejmują inicjator dla pary klucz/wartość, które zostaną dodane do `students` <xref:System.Collections.Generic.Dictionary%602> .</span><span class="sxs-lookup"><span data-stu-id="bb921-115">The innermost braces enclose the object initializer for the `StudentName`, and the outermost braces enclose the initializer for the key/value pair that will be added to the `students` <xref:System.Collections.Generic.Dictionary%602>.</span></span> <span data-ttu-id="bb921-116">Na koniec cały inicjator kolekcji dla słownika jest ujęty w nawiasy klamrowe.</span><span class="sxs-lookup"><span data-stu-id="bb921-116">Finally, the whole collection initializer for the dictionary is enclosed in braces.</span></span> <span data-ttu-id="bb921-117">Podczas drugiego inicjowania po lewej stronie przypisania jest kluczem, a po prawej stronie jest wartością, przy użyciu inicjatora obiektu dla `StudentName` .</span><span class="sxs-lookup"><span data-stu-id="bb921-117">In the second initialization, the left side of the assignment is the key and the right side is the value, using an object initializer for `StudentName`.</span></span>

## <a name="see-also"></a><span data-ttu-id="bb921-118">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="bb921-118">See also</span></span>

- [<span data-ttu-id="bb921-119">Przewodnik programowania w języku C#</span><span class="sxs-lookup"><span data-stu-id="bb921-119">C# Programming Guide</span></span>](../index.md)
- [<span data-ttu-id="bb921-120">Inicjatory obiektów i kolekcji</span><span class="sxs-lookup"><span data-stu-id="bb921-120">Object and Collection Initializers</span></span>](./object-and-collection-initializers.md)
