---
title: Ostrzeżenie SYSLIB0006
description: Dowiedz się więcej o Obsoletions, które generują ostrzeżenie SYSLIB0006 w czasie kompilacji.
ms.topic: reference
ms.date: 10/20/2020
ms.openlocfilehash: a5ab4fe4576bd336cb7de0a91b889fa48ac5650a
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96437468"
---
# <a name="syslib0006-threadabort-is-not-supported"></a><span data-ttu-id="c3277-103">SYSLIB0006: Thread. Abort nie jest obsługiwana</span><span class="sxs-lookup"><span data-stu-id="c3277-103">SYSLIB0006: Thread.Abort is not supported</span></span>

<span data-ttu-id="c3277-104">Następujące interfejsy API są oznaczone jako przestarzałe, począwszy od platformy .NET 5,0.</span><span class="sxs-lookup"><span data-stu-id="c3277-104">The following APIs are marked obsolete, starting in .NET 5.0.</span></span> <span data-ttu-id="c3277-105">Użycie tych interfejsów API generuje ostrzeżenie `SYSLIB0006` w czasie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="c3277-105">Use of these APIs generates warning `SYSLIB0006` at compile time.</span></span>

- <xref:System.Threading.Thread.Abort?displayProperty=nameWithType>
- <xref:System.Threading.Thread.Abort(System.Object)?displayProperty=nameWithType>

## <a name="workarounds"></a><span data-ttu-id="c3277-106">Obejścia</span><span class="sxs-lookup"><span data-stu-id="c3277-106">Workarounds</span></span>

<span data-ttu-id="c3277-107">Użyj, <xref:System.Threading.CancellationToken> Aby przerwać przetwarzanie jednostki pracy zamiast wywoływania <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="c3277-107">Use a <xref:System.Threading.CancellationToken> to abort processing of a unit of work instead of calling <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType>.</span></span> <span data-ttu-id="c3277-108">Poniższy przykład ilustruje użycie <xref:System.Threading.CancellationToken> .</span><span class="sxs-lookup"><span data-stu-id="c3277-108">The following example illustrates the use of <xref:System.Threading.CancellationToken>.</span></span>

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

[!INCLUDE [suppress-syslib-warning](../../../includes/suppress-syslib-warning.md)]

## <a name="see-also"></a><span data-ttu-id="c3277-109">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="c3277-109">See also</span></span>

- [<span data-ttu-id="c3277-110">Element Thread.Abort jest przestarzały</span><span class="sxs-lookup"><span data-stu-id="c3277-110">Thread.Abort is obsolete</span></span>](core-libraries/5.0/thread-abort-obsolete.md)
- [<span data-ttu-id="c3277-111">Anulowanie w zarządzanych wątkach</span><span class="sxs-lookup"><span data-stu-id="c3277-111">Cancellation in managed threads</span></span>](../../standard/threading/cancellation-in-managed-threads.md)
