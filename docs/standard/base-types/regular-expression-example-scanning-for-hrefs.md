---
title: 'Przykład wyrażenia regularnego: wyszukiwanie wartości HREF'
description: Zobacz przykład wyrażeń regularnych w programie .NET. Przykład wyszukuje ciąg wejściowy i wyświetla wszystkie wartości atrybutów href i ich lokalizacje.
ms.date: 06/30/2020
dev_langs:
- csharp
- vb
helpviewer_keywords:
- searching with regular expressions, examples
- parsing text with regular expressions, examples
- regular expressions, examples
- .NET regular expressions, examples
- regular expressions [.NET], examples
- pattern-matching with regular expressions, examples
ms.assetid: fae2c15b-7adf-4b15-b118-58eb3906994f
ms.openlocfilehash: 659ba966ab18f2c5db13af3ac687af57dea7b126
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97513214"
---
# <a name="regular-expression-example-scanning-for-hrefs"></a>Przykład wyrażenia regularnego: wyszukiwanie wartości HREF

Poniższy przykład wyszukuje ciąg wejściowy i wyświetla wszystkie odwołania href = "..." wartości i ich lokalizacje w ciągu.  

[!INCLUDE [regex](../../../includes/regex.md)]

## <a name="the-regex-object"></a>Obiekt Regex

 Ponieważ `DumpHRefs` Metoda może być wywoływana wiele razy z kodu użytkownika, używa `static` `Shared` metody (w Visual Basic) <xref:System.Text.RegularExpressions.Regex.Match%28System.String%2CSystem.String%2CSystem.Text.RegularExpressions.RegexOptions%29?displayProperty=nameWithType> . Dzięki temu aparat wyrażeń regularnych może buforować wyrażenie regularne i pozwala uniknąć obciążenia wystąpienia nowego <xref:System.Text.RegularExpressions.Regex> obiektu za każdym razem, gdy wywoływana jest metoda. <xref:System.Text.RegularExpressions.Match>Obiekt jest następnie używany do iteracji we wszystkich dopasowaniach w ciągu.  
  
 [!code-csharp[RegularExpressions.Examples.HREF#1](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.HREF/cs/example.cs#1)]
 [!code-vb[RegularExpressions.Examples.HREF#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.HREF/vb/example.vb#1)]  
  
 Poniższy przykład ilustruje wywołanie `DumpHRefs` metody.  
  
 [!code-csharp[RegularExpressions.Examples.HREF#2](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.HREF/cs/example.cs#2)]
 [!code-vb[RegularExpressions.Examples.HREF#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.HREF/vb/example.vb#2)]  
  
 Wzorzec wyrażenia regularnego `href\s*=\s*(?:["'](?<1>[^"']*)["']|(?<1>\S+))` jest interpretowany jak pokazano w poniższej tabeli.  
  
|Wzorce|Opis|  
|-------------|-----------------|  
|`href`|Dopasowuje ciąg literału "href". W dopasowaniu nie jest rozróżniana wielkość liter.|  
|`\s*`|Dopasowanie do zera lub większej liczby znaków odstępu.|  
|`=`|Dopasowuje znak równości.|  
|`\s*`|Dopasowanie do zera lub większej liczby znaków odstępu.|  
|`(?:\["'\](?<1>\[^"'\]*)["']\|(?<1>\S+))`|Dopasowanie jednego z następujących elementów bez przypisywania wyniku do przechwyconej grupy:<br /> <ul><li><p>Znak cudzysłowu lub apostrofu, po którym następuje zero lub więcej wystąpień dowolnego znaku innego niż znak cudzysłowu lub apostrofu, po którym następuje znak cudzysłowu lub apostrof. Grupa o nazwie `1` jest uwzględniona w tym wzorcu.</p></li><li><p>Co najmniej jeden znak niebędący odstępem. Grupa o nazwie `1` jest uwzględniona w tym wzorcu.</p></li></ul>|  
|`(?<1>[^"']*)`|Przypisz zero lub więcej wystąpień dowolnego znaku innego niż znak cudzysłowu lub apostrofu do grupy przechwytywania o nazwie `1` .|  
|`(?<1>\S+)`|Przypisz co najmniej jeden znak niebędący odstępem do grupy przechwytywania o nazwie `1` .|  
  
## <a name="match-result-class"></a>Dopasuj wynik klasy  

 Wyniki wyszukiwania są przechowywane w <xref:System.Text.RegularExpressions.Match> klasie, która zapewnia dostęp do wszystkich podciągów wyodrębnionych przez wyszukiwanie. Odwołuje się również do wyszukiwanego ciągu i używanego wyrażenia regularnego, dzięki czemu można wywołać <xref:System.Text.RegularExpressions.Match.NextMatch%2A?displayProperty=nameWithType> metodę, aby wykonać inne wyszukiwanie, rozpoczynając od ostatniego zakończono.  
  
## <a name="explicitly-named-captures"></a>Przechwytuje wyraźnie nazwane  

 W tradycyjnych wyrażeniach regularnych przechwytywanie nawiasów jest numerowane kolejno automatycznie. Prowadzi to do dwóch problemów. Po pierwsze, jeśli wyrażenie regularne jest modyfikowane przez wstawianie lub usuwanie zestawu nawiasów, cały kod, który odwołuje się do numerowanych przechwytywania, musi zostać ponownie zapisany w celu odzwierciedlenia nowej numeracji. Drugi, ponieważ różne zestawy nawiasów często są używane do zapewnienia dwóch alternatywnych wyrażeń dla akceptowalnego dopasowania, może być trudne do ustalenia, które z dwóch wyrażeń faktycznie zwracają wynik.  
  
 Aby rozwiązać te problemy, <xref:System.Text.RegularExpressions.Regex> Klasa obsługuje składnię `(?<name>…)` przechwytywania dopasowania do określonego miejsca (miejsce może być nazwane przy użyciu ciągu lub liczby całkowitej; liczby całkowite można wielokrotnie odwoływać). W rezultacie alternatywne dopasowania dla tego samego ciągu All można skierować do tego samego miejsca. W przypadku konfliktu ostatnie dopasowanie opuszczone w gnieździe to pomyślne dopasowanie. (Jednak kompletna lista wielu dopasowań dla jednego gniazda jest dostępna. Szczegółowe informacje znajdują się w <xref:System.Text.RegularExpressions.Group.Captures%2A?displayProperty=nameWithType> kolekcji.  
  
## <a name="see-also"></a>Zobacz też

- [Wyrażenia regularne .NET](regular-expressions.md)
