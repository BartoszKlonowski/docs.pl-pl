---
title: Bezpieczeństwo wątków w wyrażeniach regularnych
ms.date: 03/30/2017
helpviewer_keywords:
- .NET regular expressions, threads
- regular expressions, threads
- searching with regular expressions, threads
- parsing text with regular expressions, threads
- pattern-matching with regular expressions, threads
ms.assetid: 7c4a167b-5236-4cde-a2ca-58646230730f
ms.openlocfilehash: 8f4930e0bc1fca51164d1108b169d35c8e73987d
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94818742"
---
# <a name="thread-safety-in-regular-expressions"></a><span data-ttu-id="13430-102">Bezpieczeństwo wątków w wyrażeniach regularnych</span><span class="sxs-lookup"><span data-stu-id="13430-102">Thread Safety in Regular Expressions</span></span>
<span data-ttu-id="13430-103"><xref:System.Text.RegularExpressions.Regex>Sama klasa jest bezpieczna wątkowo i niezmienna (tylko do odczytu).</span><span class="sxs-lookup"><span data-stu-id="13430-103">The <xref:System.Text.RegularExpressions.Regex> class itself is thread safe and immutable (read-only).</span></span> <span data-ttu-id="13430-104">Oznacza to, że obiekty **wyrażenia regularnego** można tworzyć w dowolnym wątku i współdzielonym przez wątki. Metody pasujące mogą być wywoływane z dowolnego wątku i nigdy nie zmieniają żadnego stanu globalnego.</span><span class="sxs-lookup"><span data-stu-id="13430-104">That is, **Regex** objects can be created on any thread and shared between threads; matching methods can be called from any thread and never alter any global state.</span></span>  
  
 <span data-ttu-id="13430-105">Jednak obiekty wynikowe (**Match** i **MatchCollection**) zwracane przez **wyrażenie regularne** powinny być używane w pojedynczym wątku.</span><span class="sxs-lookup"><span data-stu-id="13430-105">However, result objects (**Match** and **MatchCollection**) returned by **Regex** should be used on a single thread.</span></span> <span data-ttu-id="13430-106">Chociaż wiele z tych obiektów jest logicznie niezmienne, ich implementacje mogą opóźniać Obliczanie niektórych wyników w celu zwiększenia wydajności i w związku z tym wywołujący muszą serializować dostęp do nich.</span><span class="sxs-lookup"><span data-stu-id="13430-106">Although many of these objects are logically immutable, their implementations could delay computation of some results to improve performance, and as a result, callers must serialize access to them.</span></span>  
  
 <span data-ttu-id="13430-107">Jeśli istnieje potrzeba udostępniania obiektów wynikowych **wyrażeń regularnych** w wielu wątkach, te obiekty mogą być konwertowane na wystąpienia z bezpiecznymi wątkami przez wywołanie ich zsynchronizowanych metod.</span><span class="sxs-lookup"><span data-stu-id="13430-107">If there is a need to share **Regex** result objects on multiple threads, these objects can be converted to thread-safe instances by calling their synchronized methods.</span></span> <span data-ttu-id="13430-108">Z wyjątkiem modułów wyliczających wszystkie klasy wyrażeń regularnych są bezpieczne wątkowo lub mogą być konwertowane na obiekty z bezpiecznymi wątkami przez zsynchronizowaną metodę.</span><span class="sxs-lookup"><span data-stu-id="13430-108">With the exception of enumerators, all regular expression classes are thread safe or can be converted into thread-safe objects by a synchronized method.</span></span>  
  
 <span data-ttu-id="13430-109">Numeratory są jedynym wyjątkiem.</span><span class="sxs-lookup"><span data-stu-id="13430-109">Enumerators are the only exception.</span></span> <span data-ttu-id="13430-110">Aplikacja musi serializować wywołania do modułów wyliczających kolekcje.</span><span class="sxs-lookup"><span data-stu-id="13430-110">An application must serialize calls to collection enumerators.</span></span> <span data-ttu-id="13430-111">Zasada polega na tym, że jeśli kolekcja może zostać wyliczona jednocześnie w więcej niż jednym wątku, należy synchronizować metody modułu wyliczającego w obiekcie głównym kolekcji przechodzącej przez moduł wyliczający.</span><span class="sxs-lookup"><span data-stu-id="13430-111">The rule is that if a collection can be enumerated on more than one thread simultaneously, you should synchronize enumerator methods on the root object of the collection traversed by the enumerator.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="13430-112">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="13430-112">See also</span></span>

- [<span data-ttu-id="13430-113">Wyrażenia regularne .NET</span><span class="sxs-lookup"><span data-stu-id="13430-113">.NET Regular Expressions</span></span>](regular-expressions.md)
