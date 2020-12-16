---
title: Ostrzeżenie SYSLIB0010
description: Dowiedz się więcej o Obsoletions, które generują ostrzeżenie SYSLIB0010 w czasie kompilacji.
ms.topic: reference
ms.date: 10/20/2020
ms.openlocfilehash: 289fb3f766a6e1d37bea8faec1896d20442f43f9
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/16/2020
ms.locfileid: "97596556"
---
# <a name="syslib0010-unsupported-remoting-apis"></a><span data-ttu-id="c5e5b-103">SYSLIB0010: nieobsługiwane interfejsy API komunikacji zdalnej</span><span class="sxs-lookup"><span data-stu-id="c5e5b-103">SYSLIB0010: Unsupported remoting APIs</span></span>

<span data-ttu-id="c5e5b-104">[Komunikacja zdalna .NET](/previous-versions/dotnet/netframework-1.1/kwdt6w2k(v=vs.71)) to Starsza technologia, a infrastruktura istnieje tylko w .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="c5e5b-104">[.NET remoting](/previous-versions/dotnet/netframework-1.1/kwdt6w2k(v=vs.71)) is a legacy technology, and the infrastructure exists only in .NET Framework.</span></span> <span data-ttu-id="c5e5b-105">Następujące interfejsy API związane z usługami zdalnymi są oznaczone jako przestarzałe, począwszy od platformy .NET 5,0.</span><span class="sxs-lookup"><span data-stu-id="c5e5b-105">The following remoting-related APIs are marked as obsolete, starting in .NET 5.0.</span></span> <span data-ttu-id="c5e5b-106">Użycie ich w kodzie generuje ostrzeżenie `SYSLIB0010` w czasie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="c5e5b-106">Using them in code generates warning `SYSLIB0010` at compile time.</span></span>

- <xref:System.MarshalByRefObject.GetLifetimeService?displayProperty=nameWithType>
- <xref:System.MarshalByRefObject.InitializeLifetimeService?displayProperty=nameWithType>

## <a name="workarounds"></a><span data-ttu-id="c5e5b-107">Obejścia</span><span class="sxs-lookup"><span data-stu-id="c5e5b-107">Workarounds</span></span>

<span data-ttu-id="c5e5b-108">Należy rozważyć użycie usług REST lub opartych na protokole HTTP w celu komunikowania się z obiektami w innych aplikacjach lub na różnych komputerach.</span><span class="sxs-lookup"><span data-stu-id="c5e5b-108">Consider using WCF or HTTP-based REST services to communicate with objects in other applications or across machines.</span></span> <span data-ttu-id="c5e5b-109">Aby uzyskać więcej informacji, zobacz [technologie .NET Framework niedostępne w programie .NET Core](../../porting/net-framework-tech-unavailable.md).</span><span class="sxs-lookup"><span data-stu-id="c5e5b-109">For more information, see [.NET Framework technologies unavailable on .NET Core](../../porting/net-framework-tech-unavailable.md).</span></span>

[!INCLUDE [suppress-syslib-warning](../../../../includes/suppress-syslib-warning.md)]

## <a name="see-also"></a><span data-ttu-id="c5e5b-110">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="c5e5b-110">See also</span></span>

- <span data-ttu-id="c5e5b-111">[Komunikacja zdalna .NET](/previous-versions/dotnet/netframework-1.1/kwdt6w2k(v=vs.71))</span><span class="sxs-lookup"><span data-stu-id="c5e5b-111">[.NET remoting](/previous-versions/dotnet/netframework-1.1/kwdt6w2k(v=vs.71))</span></span>
