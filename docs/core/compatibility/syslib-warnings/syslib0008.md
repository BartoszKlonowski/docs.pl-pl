---
title: Ostrzeżenie SYSLIB0008
description: Dowiedz się więcej na temat obsoletion, który generuje ostrzeżenie SYSLIB0008 w czasie kompilacji.
ms.topic: reference
ms.date: 10/20/2020
ms.openlocfilehash: 2b573f4b28cdf79107395f5cb38a4226d0ccc11e
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/16/2020
ms.locfileid: "97596555"
---
# <a name="syslib0008-createpdbgenerator-is-not-supported"></a>SYSLIB0008: CreatePdbGenerator nie jest obsługiwana

<xref:System.Runtime.CompilerServices.DebugInfoGenerator.CreatePdbGenerator?displayProperty=nameWithType>Interfejs API jest oznaczony jako przestarzały, począwszy od platformy .net 5,0. Użycie tego interfejsu API generuje ostrzeżenie `SYSLIB0008` w czasie kompilacji.

## <a name="suppress-the-warning"></a>Pomiń ostrzeżenie

Jeśli nie możesz zmienić kodu, możesz pominąć ostrzeżenie za pomocą `#pragma` dyrektywy lub `<NoWarn>` Ustawienia projektu. Aby zapoznać się z przykładami, zobacz [pomijanie ostrzeżeń](../syslib-obsoletions.md#suppress-warnings).
