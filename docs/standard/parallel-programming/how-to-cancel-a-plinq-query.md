---
title: 'Instrukcje: Anulowanie zapytania PLINQ'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- PLINQ queries, how to cancel
- cancellation, PLINQ
ms.assetid: 80b14640-edfa-4153-be1b-3e003d3e9c1a
ms.openlocfilehash: f8ca723ca3b9b9428c95651ebe2fa7d92e48ebbb
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95713291"
---
# <a name="how-to-cancel-a-plinq-query"></a><span data-ttu-id="8c7a6-102">Instrukcje: Anulowanie zapytania PLINQ</span><span class="sxs-lookup"><span data-stu-id="8c7a6-102">How to: Cancel a PLINQ Query</span></span>

<span data-ttu-id="8c7a6-103">W poniższych przykładach pokazano dwa sposoby anulowania zapytania PLINQ.</span><span class="sxs-lookup"><span data-stu-id="8c7a6-103">The following examples show two ways to cancel a PLINQ query.</span></span> <span data-ttu-id="8c7a6-104">Pierwszy przykład pokazuje, jak anulować zapytanie, które składa się głównie z przechodzenia do danych.</span><span class="sxs-lookup"><span data-stu-id="8c7a6-104">The first example shows how to cancel a query that consists mostly of data traversal.</span></span> <span data-ttu-id="8c7a6-105">Drugi przykład pokazuje, jak anulować zapytanie zawierające funkcję użytkownika, która jest w praktyce kosztowna.</span><span class="sxs-lookup"><span data-stu-id="8c7a6-105">The second example shows how to cancel a query that contains a user function that is computationally expensive.</span></span>

> [!NOTE]
> <span data-ttu-id="8c7a6-106">Po włączeniu "Tylko mój kod" program Visual Studio przerwie w wierszu, który zgłasza wyjątek, i wyświetla komunikat o błędzie "wyjątek nie jest obsługiwany przez kod użytkownika".</span><span class="sxs-lookup"><span data-stu-id="8c7a6-106">When "Just My Code" is enabled, Visual Studio will break on the line that throws the exception and display an error message that says "exception not handled by user code."</span></span> <span data-ttu-id="8c7a6-107">Ten błąd jest niegroźny.</span><span class="sxs-lookup"><span data-stu-id="8c7a6-107">This error is benign.</span></span> <span data-ttu-id="8c7a6-108">Możesz nacisnąć klawisz F5, aby kontynuować z niego i zobaczyć zachowanie obsługi wyjątków, które przedstawiono w poniższych przykładach.</span><span class="sxs-lookup"><span data-stu-id="8c7a6-108">You can press F5 to continue from it, and see the exception-handling behavior that is demonstrated in the examples below.</span></span> <span data-ttu-id="8c7a6-109">Aby zapobiec utracie przez program Visual Studio pierwszego błędu, po prostu usuń zaznaczenie pola wyboru "Tylko mój kod" w obszarze **Narzędzia, opcje, debugowanie, ogólne**.</span><span class="sxs-lookup"><span data-stu-id="8c7a6-109">To prevent Visual Studio from breaking on the first error, just uncheck the "Just My Code" checkbox under **Tools, Options, Debugging, General**.</span></span>
>
> <span data-ttu-id="8c7a6-110">Ten przykład jest przeznaczony do zademonstrowania użycia i może nie działać szybciej niż równoważne LINQ to Objects sekwencyjne zapytanie.</span><span class="sxs-lookup"><span data-stu-id="8c7a6-110">This example is intended to demonstrate usage, and might not run faster than the equivalent sequential LINQ to Objects query.</span></span> <span data-ttu-id="8c7a6-111">Aby uzyskać więcej informacji na temat przyspieszenie, zobacz [Opis przyspieszenie w PLINQ](understanding-speedup-in-plinq.md).</span><span class="sxs-lookup"><span data-stu-id="8c7a6-111">For more information about speedup, see [Understanding Speedup in PLINQ](understanding-speedup-in-plinq.md).</span></span>

## <a name="example"></a><span data-ttu-id="8c7a6-112">Przykład</span><span class="sxs-lookup"><span data-stu-id="8c7a6-112">Example</span></span>

[!code-csharp[PLINQ#16](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#16)]
[!code-vb[PLINQ#16](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#16)]

<span data-ttu-id="8c7a6-113">Struktura PLINQ nie jest rzutowana na <xref:System.OperationCanceledException> <xref:System.AggregateException?displayProperty=nameWithType> ; <xref:System.OperationCanceledException> musi być obsługiwana w oddzielnym bloku catch.</span><span class="sxs-lookup"><span data-stu-id="8c7a6-113">The PLINQ framework does not roll a single <xref:System.OperationCanceledException> into an <xref:System.AggregateException?displayProperty=nameWithType>; the <xref:System.OperationCanceledException> must be handled in a separate catch block.</span></span> <span data-ttu-id="8c7a6-114">Jeśli co najmniej jeden delegat użytkownika zgłosi OperationCanceledException (externalCT) (przy użyciu zewnętrznego <xref:System.Threading.CancellationToken?displayProperty=nameWithType> ), ale nie inny wyjątek, a zapytanie zostało zdefiniowane jako `AsParallel().WithCancellation(externalCT)` , a następnie PLINQ będzie wystawiał pojedynczy <xref:System.OperationCanceledException> (externalCT), a nie <xref:System.AggregateException?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="8c7a6-114">If one or more user delegates throws an OperationCanceledException(externalCT) (by using an external <xref:System.Threading.CancellationToken?displayProperty=nameWithType>) but no other exception, and the query was defined as `AsParallel().WithCancellation(externalCT)`, then PLINQ will issue a single <xref:System.OperationCanceledException> (externalCT) rather than an <xref:System.AggregateException?displayProperty=nameWithType>.</span></span> <span data-ttu-id="8c7a6-115">Jeśli jednak jeden delegat użytkownika zgłosi <xref:System.OperationCanceledException> , a inny delegat zgłosi inny typ wyjątku, oba wyjątki zostaną przeagregowane do <xref:System.AggregateException> .</span><span class="sxs-lookup"><span data-stu-id="8c7a6-115">However, if one user delegate throws an <xref:System.OperationCanceledException>, and another delegate throws another exception type, then both exceptions will be rolled into an <xref:System.AggregateException>.</span></span>

<span data-ttu-id="8c7a6-116">Ogólne wskazówki dotyczące anulowania są następujące:</span><span class="sxs-lookup"><span data-stu-id="8c7a6-116">The general guidance on cancellation is as follows:</span></span>

1. <span data-ttu-id="8c7a6-117">Jeśli wykonujesz anulowanie delegata użytkownika, należy poinformować PLINQ o zewnętrznym <xref:System.Threading.CancellationToken> i wyrzucaniu <xref:System.OperationCanceledException> (externalCT).</span><span class="sxs-lookup"><span data-stu-id="8c7a6-117">If you perform user-delegate cancellation, you should inform PLINQ about the external <xref:System.Threading.CancellationToken> and throw an <xref:System.OperationCanceledException>(externalCT).</span></span>

2. <span data-ttu-id="8c7a6-118">Jeśli wystąpiło anulowanie i nie są zgłaszane żadne inne wyjątki, należy obsłużyć <xref:System.OperationCanceledException> zamiast <xref:System.AggregateException> .</span><span class="sxs-lookup"><span data-stu-id="8c7a6-118">If cancellation occurs and no other exceptions are thrown, then handle an <xref:System.OperationCanceledException> rather than an <xref:System.AggregateException>.</span></span>

## <a name="example"></a><span data-ttu-id="8c7a6-119">Przykład</span><span class="sxs-lookup"><span data-stu-id="8c7a6-119">Example</span></span>

<span data-ttu-id="8c7a6-120">Poniższy przykład pokazuje, jak obsłużyć anulowanie, gdy w kodzie użytkownika znajduje się Funkcja obliczeniowa kosztowna.</span><span class="sxs-lookup"><span data-stu-id="8c7a6-120">The following example shows how to handle cancellation when you have a computationally expensive function in user code.</span></span>

[!code-csharp[PLINQ#17](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#17)]
[!code-vb[PLINQ#17](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#17)]

<span data-ttu-id="8c7a6-121">W przypadku obsługi anulowania w kodzie użytkownika nie trzeba używać <xref:System.Linq.ParallelEnumerable.WithCancellation%2A> w definicji zapytania.</span><span class="sxs-lookup"><span data-stu-id="8c7a6-121">When you handle the cancellation in user code, you do not have to use <xref:System.Linq.ParallelEnumerable.WithCancellation%2A> in the query definition.</span></span> <span data-ttu-id="8c7a6-122">Zaleca się jednak korzystanie z <xref:System.Linq.ParallelEnumerable.WithCancellation%2A> programu, ponieważ nie <xref:System.Linq.ParallelEnumerable.WithCancellation%2A> ma ono wpływu na wydajność zapytań i umożliwia anulowanie obsługi przez operatory zapytań oraz kod użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8c7a6-122">However, we recommended that you do use <xref:System.Linq.ParallelEnumerable.WithCancellation%2A>, because <xref:System.Linq.ParallelEnumerable.WithCancellation%2A> has no effect on query performance and it enables the cancellation to be handled by query operators and your user code.</span></span>

<span data-ttu-id="8c7a6-123">Aby zapewnić czas odpowiedzi systemu, zalecamy sprawdzenie, czy anulowanie ma być anulowane dla każdego milisekundu; Jednak okres do 10 milisekund jest uznawany za akceptowalny.</span><span class="sxs-lookup"><span data-stu-id="8c7a6-123">In order to ensure system responsiveness, we recommend that you check for cancellation around once per millisecond; however, any period up to 10 milliseconds is considered acceptable.</span></span> <span data-ttu-id="8c7a6-124">Ta częstotliwość nie powinna mieć negatywnego wpływu na wydajność kodu.</span><span class="sxs-lookup"><span data-stu-id="8c7a6-124">This frequency should not have a negative impact on your code's performance.</span></span>

<span data-ttu-id="8c7a6-125">Gdy moduł wyliczający jest usuwany, na przykład w przypadku przerwania kodu z pętli foreach (dla każdej w Visual Basic), która iteruje względem wyników zapytania, zapytanie zostanie anulowane, ale nie jest zgłaszany żaden wyjątek.</span><span class="sxs-lookup"><span data-stu-id="8c7a6-125">When an enumerator is disposed, for example when code breaks out of a foreach (For Each in Visual Basic) loop that is iterating over query results, then the query is canceled, but no exception is thrown.</span></span>

## <a name="see-also"></a><span data-ttu-id="8c7a6-126">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="8c7a6-126">See also</span></span>

- <xref:System.Linq.ParallelEnumerable>
- [<span data-ttu-id="8c7a6-127">Równoległe LINQ (PLINQ)</span><span class="sxs-lookup"><span data-stu-id="8c7a6-127">Parallel LINQ (PLINQ)</span></span>](introduction-to-plinq.md)
- [<span data-ttu-id="8c7a6-128">Anulowanie w zarządzanych wątkach</span><span class="sxs-lookup"><span data-stu-id="8c7a6-128">Cancellation in Managed Threads</span></span>](../threading/cancellation-in-managed-threads.md)
