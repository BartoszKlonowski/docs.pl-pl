---
title: Tworzenie puli obiektów przy użyciu obiekt ConcurrentBag
ms.date: 05/01/2020
dev_langs:
- csharp
- vb
helpviewer_keywords:
- object pool, in .NET Framework
ms.assetid: 0480e7ff-b6f9-480e-a889-2ed4264d8372
ms.openlocfilehash: c593c9b2011814c49563939f1094b62cd252879c
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94822909"
---
# <a name="create-an-object-pool-by-using-a-concurrentbag"></a><span data-ttu-id="fa084-102">Tworzenie puli obiektów przy użyciu obiekt ConcurrentBag</span><span class="sxs-lookup"><span data-stu-id="fa084-102">Create an object pool by using a ConcurrentBag</span></span>

<span data-ttu-id="fa084-103">Ten przykład pokazuje, jak używać <xref:System.Collections.Concurrent.ConcurrentBag%601> do implementowania puli obiektów.</span><span class="sxs-lookup"><span data-stu-id="fa084-103">This example shows how to use a <xref:System.Collections.Concurrent.ConcurrentBag%601> to implement an object pool.</span></span> <span data-ttu-id="fa084-104">Pule obiektów mogą zwiększyć wydajność aplikacji w sytuacjach, gdy wymagana jest wiele wystąpień klasy, a Klasa jest kosztowna do tworzenia lub niszczenia.</span><span class="sxs-lookup"><span data-stu-id="fa084-104">Object pools can improve application performance in situations where you require multiple instances of a class and the class is expensive to create or destroy.</span></span> <span data-ttu-id="fa084-105">Gdy program kliencki żąda nowego obiektu, Pula obiektów najpierw próbuje dostarczyć taką, która została już utworzona i zwrócona do puli.</span><span class="sxs-lookup"><span data-stu-id="fa084-105">When a client program requests a new object, the object pool first attempts to provide one that has already been created and returned to the pool.</span></span> <span data-ttu-id="fa084-106">Jeśli żaden nie jest dostępny, tylko wtedy jest tworzony nowy obiekt.</span><span class="sxs-lookup"><span data-stu-id="fa084-106">If none is available, only then is a new object created.</span></span>

<span data-ttu-id="fa084-107">Służy <xref:System.Collections.Concurrent.ConcurrentBag%601> do przechowywania obiektów, ponieważ obsługuje szybkie Wstawianie i usuwanie, szczególnie gdy ten sam wątek dodaje i usuwa elementy.</span><span class="sxs-lookup"><span data-stu-id="fa084-107">The <xref:System.Collections.Concurrent.ConcurrentBag%601> is used to store the objects because it supports fast insertion and removal, especially when the same thread is both adding and removing items.</span></span> <span data-ttu-id="fa084-108">Ten przykład może być dodatkowo rozszerzany tak, aby był zbudowany wokół <xref:System.Collections.Concurrent.IProducerConsumerCollection%601> , który jest implementowany przez strukturę danych zbioru, jak to zrobić <xref:System.Collections.Concurrent.ConcurrentQueue%601> i <xref:System.Collections.Concurrent.ConcurrentStack%601> .</span><span class="sxs-lookup"><span data-stu-id="fa084-108">This example could be further augmented to be built around a <xref:System.Collections.Concurrent.IProducerConsumerCollection%601>, which the bag data structure implements, as do <xref:System.Collections.Concurrent.ConcurrentQueue%601> and <xref:System.Collections.Concurrent.ConcurrentStack%601>.</span></span>

> [!TIP]
> <span data-ttu-id="fa084-109">W tym artykule opisano sposób pisania własnej implementacji puli obiektów z podstawowym typem współbieżnym do przechowywania obiektów do ponownego użycia.</span><span class="sxs-lookup"><span data-stu-id="fa084-109">This article defines how to write your own implementation of an object pool with an underlying concurrent type to store objects for reuse.</span></span> <span data-ttu-id="fa084-110">Jednak ten <xref:Microsoft.Extensions.ObjectPool.ObjectPool%601?displayProperty=nameWithType> Typ już istnieje w <xref:Microsoft.Extensions.ObjectPool?displayProperty=fullName> przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="fa084-110">However, the <xref:Microsoft.Extensions.ObjectPool.ObjectPool%601?displayProperty=nameWithType> type already exists under the <xref:Microsoft.Extensions.ObjectPool?displayProperty=fullName> namespace.</span></span> <span data-ttu-id="fa084-111">Rozważ użycie dostępnego typu przed utworzeniem własnej implementacji, która obejmuje wiele dodatkowych funkcji.</span><span class="sxs-lookup"><span data-stu-id="fa084-111">Consider using the available type before creating your own implementation, which includes many additional features.</span></span>

## <a name="example"></a><span data-ttu-id="fa084-112">Przykład</span><span class="sxs-lookup"><span data-stu-id="fa084-112">Example</span></span>

[!code-csharp[CDS#04](../../../../samples/snippets/csharp/VS_Snippets_Misc/cds/cs/objectpool.cs#04)]
[!code-vb[CDS#04](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds/vb/objectpool04.vb#04)]

## <a name="see-also"></a><span data-ttu-id="fa084-113">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="fa084-113">See also</span></span>

- [<span data-ttu-id="fa084-114">Kolekcje bezpieczne dla wątków</span><span class="sxs-lookup"><span data-stu-id="fa084-114">Thread-Safe Collections</span></span>](index.md)
