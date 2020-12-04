---
title: Przenośność i reguły współdziałania (analiza kodu)
description: Poznaj reguły dotyczące przenośności reguł analizy kodu i współdziałania
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.Portablityrules
- vs.codeanalysis.Interoperabilityrules
helpviewer_keywords:
- managed code analysis rules, interoperability rules, portability rules
- portability rules
- warnings, portability
- interoperability rules
- warnings, interoperability
author: gewarren
ms.author: gewarren
ms.openlocfilehash: a20cd77e13c4a8b95633d129990667f0a8de3ee8
ms.sourcegitcommit: 2e4adc490c1d2a705a0592b295d606b10b9f51f1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/25/2020
ms.locfileid: "96586963"
---
# <a name="portability-and-interoperability-rules"></a><span data-ttu-id="e5d16-103">Reguły dotyczące przenośności i współdziałania</span><span class="sxs-lookup"><span data-stu-id="e5d16-103">Portability and interoperability rules</span></span>

<span data-ttu-id="e5d16-104">Reguły przenośności obsługują przenośność na różnych platformach.</span><span class="sxs-lookup"><span data-stu-id="e5d16-104">Portability rules support portability across different platforms.</span></span> <span data-ttu-id="e5d16-105">Reguły współdziałania obsługują interakcję z klientami COM.</span><span class="sxs-lookup"><span data-stu-id="e5d16-105">Interoperability rules support interaction with COM clients.</span></span>

## <a name="in-this-section"></a><span data-ttu-id="e5d16-106">W tej sekcji</span><span class="sxs-lookup"><span data-stu-id="e5d16-106">In this section</span></span>

| <span data-ttu-id="e5d16-107">Reguła</span><span class="sxs-lookup"><span data-stu-id="e5d16-107">Rule</span></span> | <span data-ttu-id="e5d16-108">Opis</span><span class="sxs-lookup"><span data-stu-id="e5d16-108">Description</span></span> |
| - | - |
| [<span data-ttu-id="e5d16-109">CA1401: P/Invoke nie powinna być widoczna</span><span class="sxs-lookup"><span data-stu-id="e5d16-109">CA1401: P/Invokes should not be visible</span></span>](ca1401.md) | <span data-ttu-id="e5d16-110">Metoda publiczna lub chroniona w typie publicznym ma atrybut System.Runtime.InteropServices.DllImportAttribute (również zaimplementowany przez słowo kluczowe Declare w Visual Basic).</span><span class="sxs-lookup"><span data-stu-id="e5d16-110">A public or protected method in a public type has the System.Runtime.InteropServices.DllImportAttribute attribute (also implemented by the Declare keyword in Visual Basic).</span></span> <span data-ttu-id="e5d16-111">Takie metody nie powinny być udostępniane.</span><span class="sxs-lookup"><span data-stu-id="e5d16-111">Such methods should not be exposed.</span></span> |
| [<span data-ttu-id="e5d16-112">CA1416: Weryfikowanie zgodności platformy</span><span class="sxs-lookup"><span data-stu-id="e5d16-112">CA1416: Validate platform compatibility</span></span>](ca1416.md) | <span data-ttu-id="e5d16-113">Korzystanie z interfejsów API zależnych od platformy w składniku sprawia, że kod przestaje działać na wszystkich platformach.</span><span class="sxs-lookup"><span data-stu-id="e5d16-113">Using platform-dependent APIs on a component makes the code no longer work across all platforms.</span></span> |
| [<span data-ttu-id="e5d16-114">CA1417: nie należy używać `OutAttribute` w parametrach ciągu dla elementu P/Invoke</span><span class="sxs-lookup"><span data-stu-id="e5d16-114">CA1417: Do not use `OutAttribute` on string parameters for P/Invokes</span></span>](ca1417.md) | <span data-ttu-id="e5d16-115">Parametry ciągu przesyłane przez wartość z `OutAttribute` mogą destabilizację środowiska uruchomieniowego, jeśli ciąg jest ciągiem z stażystami.</span><span class="sxs-lookup"><span data-stu-id="e5d16-115">String parameters passed by value with the `OutAttribute` can destabilize the runtime if the string is an interned string.</span></span> |
