---
title: 'Zmiana podziału: Blazor: zmiany w logice routingu w aplikacjach Blazor'
description: 'Dowiedz się więcej o istotnej zmianie w ASP.NET Core 5,0 zatytułowanej Blazor: zmiany w logice routingu w aplikacjach Blazor'
author: scottaddie
ms.author: scaddie
ms.date: 12/14/2020
ms.openlocfilehash: 4ab8289565c88b17eb204a11724bb12a09b033c2
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97513524"
---
# <a name="blazor-route-precedence-logic-changed-in-blazor-apps"></a>Blazor: Logika pierwszeństwa trasy została zmieniona w aplikacjach Blazor

Usterka w implementacji routingu Blazor ma wpływ na sposób określania priorytetu tras. Ta usterka ma wpływ na wszystkie trasy lub trasy z opcjonalnymi parametrami w aplikacji Blazor.

## <a name="version-introduced"></a>Wprowadzona wersja

5.0.1

## <a name="old-behavior"></a>Stare zachowanie

W przypadku błędnego zachowania trasy o niższym priorytecie są brane pod uwagę i dopasowywane przez trasy o wyższym priorytecie. Na przykład `{*slug}` trasa jest dopasowana wcześniej `/customer/{id}` .

## <a name="new-behavior"></a>Nowe zachowanie

Bieżące zachowanie jest dokładniej zgodne z zachowaniem routingu zdefiniowanym w ASP.NET Core aplikacjach. Struktura określa najpierw pierwszeństwo tras dla każdego segmentu. Długość trasy jest używana tylko jako drugie kryterium podziału powiązań.

## <a name="reason-for-change"></a>Przyczyna zmiany

Oryginalne zachowanie jest uznawane za usterkę w implementacji. W rezultacie system routingu w aplikacjach Blazor powinien działać tak samo jak w przypadku systemu routingu w pozostałej części ASP.NET Core.

## <a name="recommended-action"></a>Zalecana akcja

W przypadku uaktualniania z poprzednich wersji programu Blazor do 5. x Użyj `PreferExactMatches` atrybutu `Router` składnika. Ten atrybut może być używany do poprawnego działania. Na przykład:

```razor
<Router AppAssembly="@typeof(Program).Assembly" PreferExactMatches="true">
```

Gdy `PreferExactMatches` jest ustawiona na `true` , dopasowanie trasy preferuje dokładne dopasowania w przypadku symboli wieloznacznych.

## <a name="affected-apis"></a>Dotyczy interfejsów API

Brak

<!--

## Category

ASP.NET Core

## Affected APIs

Not detectable via API analysis

-->
