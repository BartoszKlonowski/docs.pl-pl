---
title: Ostrzeżenie SYSLIB0006
description: Dowiedz się więcej o Obsoletions, które generują ostrzeżenie SYSLIB0006 w czasie kompilacji.
ms.topic: reference
ms.date: 10/20/2020
ms.openlocfilehash: c1eecade9280ac37917bc24aa2973756c7f08d87
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/16/2020
ms.locfileid: "97596559"
---
# <a name="syslib0006-threadabort-is-not-supported"></a><span data-ttu-id="5ad3c-103">SYSLIB0006: Thread. Abort nie jest obsługiwana</span><span class="sxs-lookup"><span data-stu-id="5ad3c-103">SYSLIB0006: Thread.Abort is not supported</span></span>

<span data-ttu-id="5ad3c-104">Następujące interfejsy API są oznaczone jako przestarzałe, począwszy od platformy .NET 5,0.</span><span class="sxs-lookup"><span data-stu-id="5ad3c-104">The following APIs are marked obsolete, starting in .NET 5.0.</span></span> <span data-ttu-id="5ad3c-105">Użycie tych interfejsów API generuje ostrzeżenie `SYSLIB0006` w czasie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="5ad3c-105">Use of these APIs generates warning `SYSLIB0006` at compile time.</span></span>

- <xref:System.Threading.Thread.Abort?displayProperty=nameWithType>
- <xref:System.Threading.Thread.Abort(System.Object)?displayProperty=nameWithType>

## <a name="workarounds"></a><span data-ttu-id="5ad3c-106">Obejścia</span><span class="sxs-lookup"><span data-stu-id="5ad3c-106">Workarounds</span></span>

<span data-ttu-id="5ad3c-107">Użyj, <xref:System.Threading.CancellationToken> Aby przerwać przetwarzanie jednostki pracy zamiast wywoływania <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="5ad3c-107">Use a <xref:System.Threading.CancellationToken> to abort processing of a unit of work instead of calling <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType>.</span></span> <span data-ttu-id="5ad3c-108">Poniższy przykład ilustruje użycie <xref:System.Threading.CancellationToken> .</span><span class="sxs-lookup"><span data-stu-id="5ad3c-108">The following example illustrates the use of <xref:System.Threading.CancellationToken>.</span></span>

```csharp
void ProcessPendingWorkItemsNew(CancellationToken cancellationToken)
{
    if (QueryIsMoreWorkPending())
    {
        // If the CancellationToken is marked as "needs to cancel",
        // this will throw the appropriate exception.
        cancellationToken.ThrowIfCancellationRequested();

        WorkItem work = DequeueWorkItem();
        ProcessWorkItem(work);
    }
}
```

[!INCLUDE [suppress-syslib-warning](../../../../includes/suppress-syslib-warning.md)]

## <a name="see-also"></a><span data-ttu-id="5ad3c-109">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="5ad3c-109">See also</span></span>

- [<span data-ttu-id="5ad3c-110">Element Thread.Abort jest przestarzały</span><span class="sxs-lookup"><span data-stu-id="5ad3c-110">Thread.Abort is obsolete</span></span>](../core-libraries/5.0/thread-abort-obsolete.md)
- [<span data-ttu-id="5ad3c-111">Anulowanie w zarządzanych wątkach</span><span class="sxs-lookup"><span data-stu-id="5ad3c-111">Cancellation in managed threads</span></span>](../../../standard/threading/cancellation-in-managed-threads.md)
