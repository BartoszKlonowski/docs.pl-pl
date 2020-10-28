---
title: 'Instrukcje: Implementacja klienta wzorca asynchronicznego opartego na zdarzeniach'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Event-based Asynchronous Pattern
- ProgressChangedEventArgs class
- BackgroundWorker component
- events [.NET], asynchronous
- Asynchronous Pattern
- AsyncOperationManager class
- threading [.NET], asynchronous features
- components [.NET], asynchronous
- AsyncOperation class
- threading [Windows Forms], asynchronous features
- AsyncCompletedEventArgs class
ms.assetid: 21a858c1-3c99-4904-86ee-0d17b49804fa
ms.openlocfilehash: 95997f219a08c131905cfc86b78e94c36f3ec851
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/28/2020
ms.locfileid: "92888818"
---
# <a name="how-to-implement-a-client-of-the-event-based-asynchronous-pattern"></a><span data-ttu-id="c26dc-102">Instrukcje: Implementacja klienta wzorca asynchronicznego opartego na zdarzeniach</span><span class="sxs-lookup"><span data-stu-id="c26dc-102">How to: Implement a Client of the Event-based Asynchronous Pattern</span></span>
<span data-ttu-id="c26dc-103">Poniższy przykład kodu ilustruje sposób użycia składnika, który jest zgodny z [omówieniem asynchronicznego wzorca opartego na zdarzeniach](event-based-asynchronous-pattern-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c26dc-103">The following code example demonstrates how to use a component that adheres to the [Event-based Asynchronous Pattern Overview](event-based-asynchronous-pattern-overview.md).</span></span> <span data-ttu-id="c26dc-104">Formularz do tego przykładu używa `PrimeNumberCalculator` składnika opisanego w temacie [How to: Implementuj składnik, który obsługuje wzorzec asynchroniczny oparty na zdarzeniach](component-that-supports-the-event-based-asynchronous-pattern.md).</span><span class="sxs-lookup"><span data-stu-id="c26dc-104">The form for this example uses the `PrimeNumberCalculator` component described in [How to: Implement a Component That Supports the Event-based Asynchronous Pattern](component-that-supports-the-event-based-asynchronous-pattern.md).</span></span>  
  
 <span data-ttu-id="c26dc-105">Po uruchomieniu projektu, który używa tego przykładu, zobaczysz formularz "Kalkulator numeru początkowego" z siatką i dwoma przyciskami: **Uruchom nowe zadanie** i **Anuluj** .</span><span class="sxs-lookup"><span data-stu-id="c26dc-105">When you run a project that uses this example, you will see a "Prime Number Calculator" form with a grid and two buttons: **Start New Task** and **Cancel** .</span></span> <span data-ttu-id="c26dc-106">Możesz kliknąć przycisk **Rozpocznij nowe zadanie** kilka razy, a dla każdego kliknięcia, operacja asynchroniczna rozpocznie obliczenia, aby określić, czy losowo wygenerowany numer testu jest podstawowy.</span><span class="sxs-lookup"><span data-stu-id="c26dc-106">You can click the **Start New Task** button several times in succession, and for each click, an asynchronous operation will begin a computation to determine if a randomly generated test number is prime.</span></span> <span data-ttu-id="c26dc-107">Formularz będzie okresowo wyświetlał postęp i wyniki przyrostowe.</span><span class="sxs-lookup"><span data-stu-id="c26dc-107">The form will periodically display progress and incremental results.</span></span> <span data-ttu-id="c26dc-108">Każda operacja ma przypisany unikatowy identyfikator zadania.</span><span class="sxs-lookup"><span data-stu-id="c26dc-108">Each operation is assigned a unique task ID.</span></span> <span data-ttu-id="c26dc-109">Wynik obliczeń jest wyświetlany w kolumnie **wynik** ; Jeśli numer testu nie jest znakiem, jest oznaczony jako **kompozytowy** i zostanie wyświetlony pierwszy dzielnik.</span><span class="sxs-lookup"><span data-stu-id="c26dc-109">The result of the computation is displayed in the **Result** column; if the test number is not prime, it is labeled as **Composite,** and its first divisor is displayed.</span></span>  
  
 <span data-ttu-id="c26dc-110">Wszystkie oczekujące operacje można anulować przy użyciu przycisku **Anuluj** .</span><span class="sxs-lookup"><span data-stu-id="c26dc-110">Any pending operation can be canceled with the **Cancel** button.</span></span> <span data-ttu-id="c26dc-111">Można wprowadzić wiele zaznaczeń.</span><span class="sxs-lookup"><span data-stu-id="c26dc-111">Multiple selections can be made.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="c26dc-112">Większość cyfr nie będzie podstawowa.</span><span class="sxs-lookup"><span data-stu-id="c26dc-112">Most numbers will not be prime.</span></span> <span data-ttu-id="c26dc-113">Jeśli nie odnaleziono numeru początkowego po kilku ukończonych operacjach, wystarczy uruchomić więcej zadań i ostatecznie znaleźć liczby podstawowe.</span><span class="sxs-lookup"><span data-stu-id="c26dc-113">If you have not found a prime number after several completed operations, simply start more tasks, and eventually you will find some prime numbers.</span></span>  
  
## <a name="example"></a><span data-ttu-id="c26dc-114">Przykład</span><span class="sxs-lookup"><span data-stu-id="c26dc-114">Example</span></span>  
 [!code-csharp[System.ComponentModel.AsyncOperationManager#10](snippets/component-that-supports-the-event-based-asynchronous-pattern/csharp/primenumbercalculatormain.cs#10)]
 [!code-vb[System.ComponentModel.AsyncOperationManager#10](snippets/component-that-supports-the-event-based-asynchronous-pattern/vb/primenumbercalculatormain.vb#10)]  
  
## <a name="see-also"></a><span data-ttu-id="c26dc-115">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="c26dc-115">See also</span></span>

- <xref:System.ComponentModel.AsyncOperation>
- <xref:System.ComponentModel.AsyncOperationManager>
- <xref:System.Windows.Forms.WindowsFormsSynchronizationContext>
