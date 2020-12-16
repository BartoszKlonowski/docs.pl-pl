---
title: Ostrzeżenie SYSLIB0005
description: Dowiedz się więcej na temat obsoletion, który generuje ostrzeżenie SYSLIB0005 w czasie kompilacji.
ms.topic: reference
ms.date: 10/20/2020
ms.openlocfilehash: 1263a4d327c735268f77ed56bdcea6a4cbed4bfa
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/16/2020
ms.locfileid: "97596585"
---
# <a name="syslib0005-the-global-assembly-cache-gac-is-not-supported"></a><span data-ttu-id="bd257-103">SYSLIB0005: globalna pamięć podręczna zestawów (GAC) nie jest obsługiwana</span><span class="sxs-lookup"><span data-stu-id="bd257-103">SYSLIB0005: The global assembly cache (GAC) is not supported</span></span>

<span data-ttu-id="bd257-104">Programy .NET Core i .NET 5,0 i nowsze wersje eliminują koncepcję globalnej pamięci podręcznej zestawów (GAC), która była obecna w .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="bd257-104">.NET Core and .NET 5.0 and later versions eliminate the concept of the global assembly cache (GAC) that was present in .NET Framework.</span></span> <span data-ttu-id="bd257-105">Aby ułatwić przekierowania deweloperów z tych interfejsów API, niektóre interfejsy API związane z GAC są oznaczone jako przestarzałe, począwszy od platformy .NET 5,0.</span><span class="sxs-lookup"><span data-stu-id="bd257-105">To help steer developers away from these APIs, some GAC-related APIs are marked as obsolete, starting in .NET 5.0.</span></span> <span data-ttu-id="bd257-106">Użycie tych interfejsów API generuje ostrzeżenie `SYSLIB0005` w czasie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="bd257-106">Using these APIs generates warning `SYSLIB0005` at compile time.</span></span>

<span data-ttu-id="bd257-107">Następujące interfejsy API związane z pamięcią GAC są oznaczone jako przestarzałe:</span><span class="sxs-lookup"><span data-stu-id="bd257-107">The following GAC-related APIs are marked obsolete:</span></span>

- <xref:System.Reflection.Assembly.GlobalAssemblyCache?displayProperty=nameWithType>

  <span data-ttu-id="bd257-108">Biblioteki i aplikacje nie powinny używać <xref:System.Reflection.Assembly.GlobalAssemblyCache> interfejsu API do wprowadzania informacji o zachowaniu w czasie wykonywania, ponieważ zawsze są zwracane `false` w oprogramowaniu .NET Core i .NET 5 +.</span><span class="sxs-lookup"><span data-stu-id="bd257-108">Libraries and apps should not use the <xref:System.Reflection.Assembly.GlobalAssemblyCache> API to make determinations about run-time behavior, as it always returns `false` in .NET Core and .NET 5+.</span></span>

## <a name="workarounds"></a><span data-ttu-id="bd257-109">Obejścia</span><span class="sxs-lookup"><span data-stu-id="bd257-109">Workarounds</span></span>

<span data-ttu-id="bd257-110">Jeśli aplikacja wysyła zapytanie do <xref:System.Reflection.Assembly.GlobalAssemblyCache> właściwości, należy rozważyć usunięcie wywołania.</span><span class="sxs-lookup"><span data-stu-id="bd257-110">If your application queries the <xref:System.Reflection.Assembly.GlobalAssemblyCache> property, consider removing the call.</span></span> <span data-ttu-id="bd257-111">Jeśli używasz wartości, <xref:System.Reflection.Assembly.GlobalAssemblyCache> Aby wybrać między "zestaw w pamięci GAC"-Flow a "zestawem nieznajdującym się w pamięci GAC" — przepływ w czasie wykonywania, należy rozważyć, czy przepływ nadal ma sens dla aplikacji .NET 5 +.</span><span class="sxs-lookup"><span data-stu-id="bd257-111">If you use the <xref:System.Reflection.Assembly.GlobalAssemblyCache> value to choose between an "assembly in the GAC"-flow vs. an "assembly not in the GAC"-flow at run time, reconsider whether the flow still makes sense for a .NET 5+ application.</span></span>

[!INCLUDE [suppress-syslib-warning](../../../../includes/suppress-syslib-warning.md)]

## <a name="see-also"></a><span data-ttu-id="bd257-112">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="bd257-112">See also</span></span>

- [<span data-ttu-id="bd257-113">Globalna pamięć podręczna zestawów</span><span class="sxs-lookup"><span data-stu-id="bd257-113">Global assembly cache</span></span>](../../../framework/app-domains/gac.md)
