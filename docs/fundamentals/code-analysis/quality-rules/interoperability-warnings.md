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
# <a name="portability-and-interoperability-rules"></a>Reguły dotyczące przenośności i współdziałania

Reguły przenośności obsługują przenośność na różnych platformach. Reguły współdziałania obsługują interakcję z klientami COM.

## <a name="in-this-section"></a>W tej sekcji

| Reguła | Opis |
| - | - |
| [CA1401: P/Invoke nie powinna być widoczna](ca1401.md) | Metoda publiczna lub chroniona w typie publicznym ma atrybut System.Runtime.InteropServices.DllImportAttribute (również zaimplementowany przez słowo kluczowe Declare w Visual Basic). Takie metody nie powinny być udostępniane. |
| [CA1416: Weryfikowanie zgodności platformy](ca1416.md) | Korzystanie z interfejsów API zależnych od platformy w składniku sprawia, że kod przestaje działać na wszystkich platformach. |
| [CA1417: nie należy używać `OutAttribute` w parametrach ciągu dla elementu P/Invoke](ca1417.md) | Parametry ciągu przesyłane przez wartość z `OutAttribute` mogą destabilizację środowiska uruchomieniowego, jeśli ciąg jest ciągiem z stażystami. |
