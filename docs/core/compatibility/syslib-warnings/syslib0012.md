---
title: Ostrzeżenie SYSLIB0012
description: Dowiedz się więcej o Obsoletions, które generują ostrzeżenie SYSLIB0012 w czasie kompilacji.
ms.topic: reference
ms.date: 10/20/2020
ms.openlocfilehash: 9b3fa94029efb2343e6dbbeb3ae36195f0956523
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/16/2020
ms.locfileid: "97596552"
---
# <a name="syslib0012-assemblycodebase-and-assemblyescapedcodebase-are-obsolete"></a><span data-ttu-id="11df1-103">SYSLIB0012: zestaw. CodeBase i Assembly. EscapedCodeBase są przestarzałe</span><span class="sxs-lookup"><span data-stu-id="11df1-103">SYSLIB0012: Assembly.CodeBase and Assembly.EscapedCodeBase are obsolete</span></span>

<span data-ttu-id="11df1-104">Następujące interfejsy API są oznaczone jako przestarzałe, począwszy od platformy .NET 5,0.</span><span class="sxs-lookup"><span data-stu-id="11df1-104">The following APIs are marked as obsolete, starting in .NET 5.0.</span></span> <span data-ttu-id="11df1-105">Użycie ich w kodzie generuje ostrzeżenie `SYSLIB0012` w czasie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="11df1-105">Using them in code generates warning `SYSLIB0012` at compile time.</span></span>

- <xref:System.Reflection.Assembly.CodeBase?displayProperty=nameWithType>
- <xref:System.Reflection.Assembly.EscapedCodeBase?displayProperty=nameWithType>

## <a name="workarounds"></a><span data-ttu-id="11df1-106">Obejścia</span><span class="sxs-lookup"><span data-stu-id="11df1-106">Workarounds</span></span>

<span data-ttu-id="11df1-107">Zamiast tego użyj polecenia cmdlet <xref:System.Reflection.Assembly.Location?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="11df1-107">Use <xref:System.Reflection.Assembly.Location?displayProperty=nameWithType> instead.</span></span>

[!INCLUDE [suppress-syslib-warning](../../../../includes/suppress-syslib-warning.md)]
