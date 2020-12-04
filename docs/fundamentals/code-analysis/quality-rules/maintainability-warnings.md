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
# <a name="maintainability-rules"></a><span data-ttu-id="d04a0-103">Reguły utrzymania kodu</span><span class="sxs-lookup"><span data-stu-id="d04a0-103">Maintainability rules</span></span>

<span data-ttu-id="d04a0-104">Reguły utrzymania obsługują konserwację biblioteki i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d04a0-104">Maintainability rules support library and application maintenance.</span></span>

## <a name="in-this-section"></a><span data-ttu-id="d04a0-105">W tej sekcji</span><span class="sxs-lookup"><span data-stu-id="d04a0-105">In this section</span></span>

| <span data-ttu-id="d04a0-106">Reguła</span><span class="sxs-lookup"><span data-stu-id="d04a0-106">Rule</span></span> | <span data-ttu-id="d04a0-107">Opis</span><span class="sxs-lookup"><span data-stu-id="d04a0-107">Description</span></span> |
|-----------|-----------------------------------|
| [<span data-ttu-id="d04a0-108">CA1501: Unikaj nadmiernego dziedziczenia</span><span class="sxs-lookup"><span data-stu-id="d04a0-108">CA1501: Avoid excessive inheritance</span></span>](ca1501.md) | <span data-ttu-id="d04a0-109">Typ jest głęboki na więcej niż cztery poziomy w hierarchii dziedziczenia.</span><span class="sxs-lookup"><span data-stu-id="d04a0-109">A type is more than four levels deep in its inheritance hierarchy.</span></span> <span data-ttu-id="d04a0-110">Hierarchie typów głęboko zagnieżdżonych mogą być trudne do śledzenia, zrozumienia i utrzymania.</span><span class="sxs-lookup"><span data-stu-id="d04a0-110">Deeply nested type hierarchies can be difficult to follow, understand, and maintain.</span></span> |
| [<span data-ttu-id="d04a0-111">CA1502: Unikaj nadmiernej złożoności</span><span class="sxs-lookup"><span data-stu-id="d04a0-111">CA1502: Avoid excessive complexity</span></span>](ca1502.md) | <span data-ttu-id="d04a0-112">Ta reguła mierzy liczbę liniowo niezależnych ścieżek za pośrednictwem metody, która jest określona przez liczbę i złożoność rozgałęzień warunkowych.</span><span class="sxs-lookup"><span data-stu-id="d04a0-112">This rule measures the number of linearly independent paths through the method, which is determined by the number and complexity of conditional branches.</span></span> |
| [<span data-ttu-id="d04a0-113">CA1505: Unikaj kodu trudnego w utrzymaniu</span><span class="sxs-lookup"><span data-stu-id="d04a0-113">CA1505: Avoid unmaintainable code</span></span>](ca1505.md) | <span data-ttu-id="d04a0-114">Typ lub metoda ma niską wartość indeksu konserwacji.</span><span class="sxs-lookup"><span data-stu-id="d04a0-114">A type or method has a low maintainability index value.</span></span> <span data-ttu-id="d04a0-115">Niski indeks konserwacji wskazuje, że typ lub metoda są prawdopodobnie trudne do utrzymania i są dobrymi kandydatami do przeprojektowania.</span><span class="sxs-lookup"><span data-stu-id="d04a0-115">A low maintainability index indicates that a type or method is probably difficult to maintain and would be a good candidate for redesign.</span></span> |
| [<span data-ttu-id="d04a0-116">CA1506: Unikaj nadmiernego sprzężenia klas</span><span class="sxs-lookup"><span data-stu-id="d04a0-116">CA1506: Avoid excessive class coupling</span></span>](ca1506.md) | <span data-ttu-id="d04a0-117">Ta reguła mierzy sprzęgnięcie klasy przez liczenie unikatowych odwołań typów, które zawiera typ lub metoda.</span><span class="sxs-lookup"><span data-stu-id="d04a0-117">This rule measures class coupling by counting the number of unique type references that a type or method contains.</span></span> |
| [<span data-ttu-id="d04a0-118">CA1507: Użyj operatora nameof zamiast ciągu</span><span class="sxs-lookup"><span data-stu-id="d04a0-118">CA1507: Use nameof in place of string</span></span>](ca1507.md) | <span data-ttu-id="d04a0-119">Literał ciągu jest używany jako argument, w którym `nameof` można użyć wyrażenia.</span><span class="sxs-lookup"><span data-stu-id="d04a0-119">A string literal is used as an argument where a `nameof` expression could be used.</span></span> |
| [<span data-ttu-id="d04a0-120">CA1508: Unikaj martwego kodu warunku</span><span class="sxs-lookup"><span data-stu-id="d04a0-120">CA1508: Avoid dead conditional code</span></span>](ca1508.md) | <span data-ttu-id="d04a0-121">Metoda ma kod warunkowy, który zawsze jest obliczany `true` lub `false` w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="d04a0-121">A method has conditional code that always evaluates to `true` or `false` at runtime.</span></span> <span data-ttu-id="d04a0-122">Prowadzi to do nieaktywnego kodu w `false` gałęzi warunku.</span><span class="sxs-lookup"><span data-stu-id="d04a0-122">This leads to dead code in the `false` branch of the condition.</span></span> |
| [<span data-ttu-id="d04a0-123">CA1509: Nieprawidłowy wpis w pliku konfiguracji metryk kodu</span><span class="sxs-lookup"><span data-stu-id="d04a0-123">CA1509: Invalid entry in code metrics configuration file</span></span>](ca1509.md) | <span data-ttu-id="d04a0-124">Reguły metryk kodu, takie jak [CA1501](ca1501.md), [CA1502](ca1502.md), [CA1505](ca1505.md) i [CA1506](ca1506.md), dostarczyły plik konfiguracji o nazwie `CodeMetricsConfig.txt` z nieprawidłowym wpisem.</span><span class="sxs-lookup"><span data-stu-id="d04a0-124">Code metrics rules, such as [CA1501](ca1501.md), [CA1502](ca1502.md), [CA1505](ca1505.md) and [CA1506](ca1506.md), supplied a configuration file named `CodeMetricsConfig.txt` that has an invalid entry.</span></span> |

## <a name="see-also"></a><span data-ttu-id="d04a0-125">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="d04a0-125">See also</span></span>

- [<span data-ttu-id="d04a0-126">Mierzenie złożoności i łatwość utrzymania kodu zarządzanego</span><span class="sxs-lookup"><span data-stu-id="d04a0-126">Measure Complexity and Maintainability of Managed Code</span></span>](/visualstudio/code-quality/code-metrics-values)
