---
title: 'Instrukcje: Przesyłanie zmian do bazy danych'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: c7cba174-9d40-491d-b32c-f2d73b7e9eab
ms.openlocfilehash: 5952cce5469d7a7e13e8b896f91ea1279fd62d8b
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91197043"
---
# <a name="how-to-submit-changes-to-the-database"></a><span data-ttu-id="68c01-102">Instrukcje: Przesyłanie zmian do bazy danych</span><span class="sxs-lookup"><span data-stu-id="68c01-102">How to: Submit Changes to the Database</span></span>

<span data-ttu-id="68c01-103">Bez względu na liczbę zmian dokonanych w obiektach, zmiany są wprowadzane tylko do replik w pamięci.</span><span class="sxs-lookup"><span data-stu-id="68c01-103">Regardless of how many changes you make to your objects, changes are made only to in-memory replicas.</span></span> <span data-ttu-id="68c01-104">Nie wprowadzono żadnych zmian w rzeczywistych danych w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="68c01-104">You have made no changes to the actual data in the database.</span></span> <span data-ttu-id="68c01-105">Zmiany nie są przekazywane do serwera, dopóki nie zostanie jawnie wywołana <xref:System.Data.Linq.DataContext.SubmitChanges%2A> <xref:System.Data.Linq.DataContext> .</span><span class="sxs-lookup"><span data-stu-id="68c01-105">Your changes are not transmitted to the server until you explicitly call <xref:System.Data.Linq.DataContext.SubmitChanges%2A> on the <xref:System.Data.Linq.DataContext>.</span></span>  
  
 <span data-ttu-id="68c01-106">Po nadaniu tego wywołania <xref:System.Data.Linq.DataContext> próbuje przetłumaczyć zmiany na równoważne polecenia SQL.</span><span class="sxs-lookup"><span data-stu-id="68c01-106">When you make this call, the <xref:System.Data.Linq.DataContext> tries to translate your changes into equivalent SQL commands.</span></span> <span data-ttu-id="68c01-107">Możesz użyć własnej logiki niestandardowej, aby przesłonić te działania, ale kolejność przesłania jest zorganizowany przez usługę <xref:System.Data.Linq.DataContext> znanego jako *procesor zmian*.</span><span class="sxs-lookup"><span data-stu-id="68c01-107">You can use your own custom logic to override these actions, but the order of submission is orchestrated by a service of the <xref:System.Data.Linq.DataContext> known as the *change processor*.</span></span> <span data-ttu-id="68c01-108">Sekwencja zdarzeń jest następująca:</span><span class="sxs-lookup"><span data-stu-id="68c01-108">The sequence of events is as follows:</span></span>  
  
1. <span data-ttu-id="68c01-109">Po wywołaniu <xref:System.Data.Linq.DataContext.SubmitChanges%2A> , [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] sprawdza zestaw znanych obiektów, aby określić, czy zostały do nich dołączone nowe wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="68c01-109">When you call <xref:System.Data.Linq.DataContext.SubmitChanges%2A>, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] examines the set of known objects to determine whether new instances have been attached to them.</span></span> <span data-ttu-id="68c01-110">Jeśli mają, nowe wystąpienia są dodawane do zestawu śledzonych obiektów.</span><span class="sxs-lookup"><span data-stu-id="68c01-110">If they have, these new instances are added to the set of tracked objects.</span></span>  
  
2. <span data-ttu-id="68c01-111">Wszystkie obiekty, które mają oczekujące zmiany są uporządkowane w kolejności obiektów na podstawie zależności między nimi.</span><span class="sxs-lookup"><span data-stu-id="68c01-111">All objects that have pending changes are ordered into a sequence of objects based on the dependencies between them.</span></span> <span data-ttu-id="68c01-112">Obiekty, których zmiany zależą od innych obiektów, są sekwencjonowane po ich zależnościach.</span><span class="sxs-lookup"><span data-stu-id="68c01-112">Objects whose changes depend on other objects are sequenced after their dependencies.</span></span>  
  
3. <span data-ttu-id="68c01-113">Natychmiast przed przesłaniem rzeczywistych zmian program [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] uruchamia transakcję w celu hermetyzacji szeregu poszczególnych poleceń.</span><span class="sxs-lookup"><span data-stu-id="68c01-113">Immediately before any actual changes are transmitted, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] starts a transaction to encapsulate the series of individual commands.</span></span>  
  
4. <span data-ttu-id="68c01-114">Zmiany w obiektach są tłumaczone pojedynczo do poleceń SQL i wysyłane do serwera.</span><span class="sxs-lookup"><span data-stu-id="68c01-114">The changes to the objects are translated one by one to SQL commands and sent to the server.</span></span>  
  
 <span data-ttu-id="68c01-115">W tym momencie wszystkie błędy wykryte przez bazę danych powodują zatrzymanie procesu wysyłania i zgłaszany jest wyjątek.</span><span class="sxs-lookup"><span data-stu-id="68c01-115">At this point, any errors detected by the database cause the submission process to stop, and an exception is raised.</span></span> <span data-ttu-id="68c01-116">Wszystkie zmiany w bazie danych są wycofywane tak, jakby nie miały żadnych przesłanych elementów.</span><span class="sxs-lookup"><span data-stu-id="68c01-116">All changes to the database are rolled back as if no submissions ever occurred.</span></span> <span data-ttu-id="68c01-117"><xref:System.Data.Linq.DataContext>Nadal ma pełne nagranie wszystkich zmian.</span><span class="sxs-lookup"><span data-stu-id="68c01-117">The <xref:System.Data.Linq.DataContext> still has a full recording of all changes.</span></span> <span data-ttu-id="68c01-118">W związku z tym możesz spróbować rozwiązać problem i <xref:System.Data.Linq.DataContext.SubmitChanges%2A> ponownie wywołać, jak w poniższym przykładzie kodu.</span><span class="sxs-lookup"><span data-stu-id="68c01-118">You can therefore try to correct the problem and call <xref:System.Data.Linq.DataContext.SubmitChanges%2A> again, as in the code example that follows.</span></span>  
  
## <a name="example"></a><span data-ttu-id="68c01-119">Przykład</span><span class="sxs-lookup"><span data-stu-id="68c01-119">Example</span></span>  

 <span data-ttu-id="68c01-120">Po pomyślnym zakończeniu transakcji w <xref:System.Data.Linq.DataContext> celu zaakceptowania zmian w obiektach zostaną one zignorowane.</span><span class="sxs-lookup"><span data-stu-id="68c01-120">When the transaction around the submission is completed successfully, the <xref:System.Data.Linq.DataContext> accepts the changes to the objects by ignoring the change-tracking information.</span></span>  
  
 [!code-csharp[DLinqSubmittingChanges#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSubmittingChanges/cs/Program.cs#1)]
 [!code-vb[DLinqSubmittingChanges#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSubmittingChanges/vb/Module1.vb#1)]  
  
## <a name="see-also"></a><span data-ttu-id="68c01-121">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="68c01-121">See also</span></span>

- [<span data-ttu-id="68c01-122">Instrukcje: Wykrywanie i rozwiązywanie powodujących konflikt przesłań</span><span class="sxs-lookup"><span data-stu-id="68c01-122">How to: Detect and Resolve Conflicting Submissions</span></span>](how-to-detect-and-resolve-conflicting-submissions.md)
- [<span data-ttu-id="68c01-123">Instrukcje: Zarządzanie konfliktami zmian</span><span class="sxs-lookup"><span data-stu-id="68c01-123">How to: Manage Change Conflicts</span></span>](how-to-manage-change-conflicts.md)
- [<span data-ttu-id="68c01-124">Pobieranie przykładowych baz danych</span><span class="sxs-lookup"><span data-stu-id="68c01-124">Downloading Sample Databases</span></span>](downloading-sample-databases.md)
- [<span data-ttu-id="68c01-125">Tworzenie i przesyłanie zmian danych</span><span class="sxs-lookup"><span data-stu-id="68c01-125">Making and Submitting Data Changes</span></span>](making-and-submitting-data-changes.md)
