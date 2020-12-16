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
# <a name="syslib0006-threadabort-is-not-supported"></a>SYSLIB0006: Thread. Abort nie jest obsługiwana

Następujące interfejsy API są oznaczone jako przestarzałe, począwszy od platformy .NET 5,0. Użycie tych interfejsów API generuje ostrzeżenie `SYSLIB0006` w czasie kompilacji.

- <xref:System.Threading.Thread.Abort?displayProperty=nameWithType>
- <xref:System.Threading.Thread.Abort(System.Object)?displayProperty=nameWithType>

## <a name="workarounds"></a>Obejścia

Użyj, <xref:System.Threading.CancellationToken> Aby przerwać przetwarzanie jednostki pracy zamiast wywoływania <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> . Poniższy przykład ilustruje użycie <xref:System.Threading.CancellationToken> .

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

## <a name="see-also"></a>Zobacz także

- [Element Thread.Abort jest przestarzały](../core-libraries/5.0/thread-abort-obsolete.md)
- [Anulowanie w zarządzanych wątkach](../../../standard/threading/cancellation-in-managed-threads.md)
