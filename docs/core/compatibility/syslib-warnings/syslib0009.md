---
title: Ostrzeżenie SYSLIB0009
description: Dowiedz się więcej o Obsoletions, które generują ostrzeżenie SYSLIB0009 w czasie kompilacji.
ms.topic: reference
ms.date: 10/20/2020
ms.openlocfilehash: 922fcc30b2b1577976e4e88e3f7631e19d4b2cce
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/16/2020
ms.locfileid: "97596576"
---
# <a name="syslib0009-the-authenticationmanager-authenticate-and-preauthenticate-methods-are-not-supported"></a><span data-ttu-id="72bbc-103">SYSLIB0009: metody uwierzytelniania i wstępnego uwierzytelnianiamanager nie są obsługiwane</span><span class="sxs-lookup"><span data-stu-id="72bbc-103">SYSLIB0009: The AuthenticationManager Authenticate and PreAuthenticate methods are not supported</span></span>

<span data-ttu-id="72bbc-104">Następujące interfejsy API są oznaczone jako przestarzałe, począwszy od platformy .NET 5,0.</span><span class="sxs-lookup"><span data-stu-id="72bbc-104">The following APIs are marked obsolete, starting in .NET 5.0.</span></span> <span data-ttu-id="72bbc-105">Użycie tych interfejsów API generuje ostrzeżenie `SYSLIB0009` w czasie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="72bbc-105">Use of these APIs generates warning `SYSLIB0009` at compile time.</span></span>

- <xref:System.Net.AuthenticationManager.Authenticate%2A?displayProperty=nameWithType>
- <xref:System.Net.AuthenticationManager.PreAuthenticate%2A?displayProperty=nameWithType>

## <a name="suppress-the-warning"></a><span data-ttu-id="72bbc-106">Pomiń ostrzeżenie</span><span class="sxs-lookup"><span data-stu-id="72bbc-106">Suppress the warning</span></span>

<span data-ttu-id="72bbc-107">Jeśli nie możesz zmienić kodu, możesz pominąć ostrzeżenie za pomocą `#pragma` dyrektywy lub `<NoWarn>` Ustawienia projektu.</span><span class="sxs-lookup"><span data-stu-id="72bbc-107">If you cannot change your code, you can suppress the warning through a `#pragma` directive or a `<NoWarn>` project setting.</span></span> <span data-ttu-id="72bbc-108">Aby zapoznać się z przykładami, zobacz [pomijanie ostrzeżeń](../syslib-obsoletions.md#suppress-warnings).</span><span class="sxs-lookup"><span data-stu-id="72bbc-108">For examples, see [Suppress warnings](../syslib-obsoletions.md#suppress-warnings).</span></span>
