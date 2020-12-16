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
# <a name="syslib0012-assemblycodebase-and-assemblyescapedcodebase-are-obsolete"></a>SYSLIB0012: zestaw. CodeBase i Assembly. EscapedCodeBase są przestarzałe

Następujące interfejsy API są oznaczone jako przestarzałe, począwszy od platformy .NET 5,0. Użycie ich w kodzie generuje ostrzeżenie `SYSLIB0012` w czasie kompilacji.

- <xref:System.Reflection.Assembly.CodeBase?displayProperty=nameWithType>
- <xref:System.Reflection.Assembly.EscapedCodeBase?displayProperty=nameWithType>

## <a name="workarounds"></a>Obejścia

Zamiast tego użyj polecenia cmdlet <xref:System.Reflection.Assembly.Location?displayProperty=nameWithType>.

[!INCLUDE [suppress-syslib-warning](../../../../includes/suppress-syslib-warning.md)]
