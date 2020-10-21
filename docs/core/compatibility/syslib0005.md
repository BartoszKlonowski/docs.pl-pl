---
title: Ostrzeżenie SYSLIB0005
description: Dowiedz się więcej na temat obsoletion, który generuje ostrzeżenie SYSLIB0005 w czasie kompilacji.
ms.topic: reference
ms.date: 10/20/2020
ms.openlocfilehash: 8a9893d81c781335014c8b970c460b5a4241ed18
ms.sourcegitcommit: dfcbc096ad7908cd58a5f0aeabd2256f05266bac
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/21/2020
ms.locfileid: "92333347"
---
# <a name="syslib0005-the-global-assembly-cache-gac-is-not-supported"></a>SYSLIB0005: globalna pamięć podręczna zestawów (GAC) nie jest obsługiwana

Programy .NET Core i .NET 5,0 i nowsze wersje eliminują koncepcję globalnej pamięci podręcznej zestawów (GAC), która była obecna w .NET Framework. Aby ułatwić przekierowania deweloperów z tych interfejsów API, niektóre interfejsy API związane z GAC są oznaczone jako przestarzałe, począwszy od platformy .NET 5,0. Użycie tych interfejsów API generuje ostrzeżenie `SYSLIB0005` w czasie kompilacji.

Następujące interfejsy API związane z pamięcią GAC są oznaczone jako przestarzałe:

- <xref:System.Reflection.Assembly.GlobalAssemblyCache?displayProperty=nameWithType>

  Biblioteki i aplikacje nie powinny używać <xref:System.Reflection.Assembly.GlobalAssemblyCache> interfejsu API do wprowadzania informacji o zachowaniu w czasie wykonywania, ponieważ zawsze są zwracane `false` w oprogramowaniu .NET Core i .NET 5 +.

## <a name="workaround"></a>Obejście

Jeśli aplikacja wysyła zapytanie do <xref:System.Reflection.Assembly.GlobalAssemblyCache> właściwości, należy rozważyć usunięcie wywołania. Jeśli używasz wartości, <xref:System.Reflection.Assembly.GlobalAssemblyCache> Aby wybrać między "zestaw w pamięci GAC"-Flow a "zestawem nieznajdującym się w pamięci GAC" — przepływ w czasie wykonywania, należy rozważyć, czy przepływ nadal ma sens dla aplikacji .NET 5 +.

## <a name="see-also"></a>Zobacz też

- [Globalna pamięć podręczna zestawów](../../framework/app-domains/gac.md)
