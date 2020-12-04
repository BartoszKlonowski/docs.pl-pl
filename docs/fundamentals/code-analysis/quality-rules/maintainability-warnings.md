---
title: Reguły utrzymania (analiza kodu)
description: Dowiedz się więcej o regułach utrzymania analizy kodu.
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.maintainabilityrules
helpviewer_keywords:
- rules, maintainability
- managed code analysis rules, maintainability rules
- maintainability rules
author: gewarren
ms.author: gewarren
ms.openlocfilehash: fc2ef2b42eeba241b7af66b579a60365ad2b88c7
ms.sourcegitcommit: 2e4adc490c1d2a705a0592b295d606b10b9f51f1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/25/2020
ms.locfileid: "96586962"
---
# <a name="maintainability-rules"></a>Reguły utrzymania kodu

Reguły utrzymania obsługują konserwację biblioteki i aplikacji.

## <a name="in-this-section"></a>W tej sekcji

| Reguła | Opis |
|-----------|-----------------------------------|
| [CA1501: Unikaj nadmiernego dziedziczenia](ca1501.md) | Typ jest głęboki na więcej niż cztery poziomy w hierarchii dziedziczenia. Hierarchie typów głęboko zagnieżdżonych mogą być trudne do śledzenia, zrozumienia i utrzymania. |
| [CA1502: Unikaj nadmiernej złożoności](ca1502.md) | Ta reguła mierzy liczbę liniowo niezależnych ścieżek za pośrednictwem metody, która jest określona przez liczbę i złożoność rozgałęzień warunkowych. |
| [CA1505: Unikaj kodu trudnego w utrzymaniu](ca1505.md) | Typ lub metoda ma niską wartość indeksu konserwacji. Niski indeks konserwacji wskazuje, że typ lub metoda są prawdopodobnie trudne do utrzymania i są dobrymi kandydatami do przeprojektowania. |
| [CA1506: Unikaj nadmiernego sprzężenia klas](ca1506.md) | Ta reguła mierzy sprzęgnięcie klasy przez liczenie unikatowych odwołań typów, które zawiera typ lub metoda. |
| [CA1507: Użyj operatora nameof zamiast ciągu](ca1507.md) | Literał ciągu jest używany jako argument, w którym `nameof` można użyć wyrażenia. |
| [CA1508: Unikaj martwego kodu warunku](ca1508.md) | Metoda ma kod warunkowy, który zawsze jest obliczany `true` lub `false` w czasie wykonywania. Prowadzi to do nieaktywnego kodu w `false` gałęzi warunku. |
| [CA1509: Nieprawidłowy wpis w pliku konfiguracji metryk kodu](ca1509.md) | Reguły metryk kodu, takie jak [CA1501](ca1501.md), [CA1502](ca1502.md), [CA1505](ca1505.md) i [CA1506](ca1506.md), dostarczyły plik konfiguracji o nazwie `CodeMetricsConfig.txt` z nieprawidłowym wpisem. |

## <a name="see-also"></a>Zobacz także

- [Mierzenie złożoności i łatwość utrzymania kodu zarządzanego](/visualstudio/code-quality/code-metrics-values)
