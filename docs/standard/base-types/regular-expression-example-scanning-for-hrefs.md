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
# <a name="regular-expression-example-scanning-for-hrefs"></a><span data-ttu-id="2da11-104">Przykład wyrażenia regularnego: wyszukiwanie wartości HREF</span><span class="sxs-lookup"><span data-stu-id="2da11-104">Regular Expression Example: Scanning for HREFs</span></span>

<span data-ttu-id="2da11-105">Poniższy przykład wyszukuje ciąg wejściowy i wyświetla wszystkie odwołania href = "..." wartości i ich lokalizacje w ciągu.</span><span class="sxs-lookup"><span data-stu-id="2da11-105">The following example searches an input string and displays all the href="…" values and their locations in the string.</span></span>  

[!INCLUDE [regex](../../../includes/regex.md)]

## <a name="the-regex-object"></a><span data-ttu-id="2da11-106">Obiekt Regex</span><span class="sxs-lookup"><span data-stu-id="2da11-106">The Regex Object</span></span>

 <span data-ttu-id="2da11-107">Ponieważ `DumpHRefs` Metoda może być wywoływana wiele razy z kodu użytkownika, używa `static` `Shared` metody (w Visual Basic) <xref:System.Text.RegularExpressions.Regex.Match%28System.String%2CSystem.String%2CSystem.Text.RegularExpressions.RegexOptions%29?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="2da11-107">Because the `DumpHRefs` method can be called multiple times from user code, it uses the `static` (`Shared` in Visual Basic) <xref:System.Text.RegularExpressions.Regex.Match%28System.String%2CSystem.String%2CSystem.Text.RegularExpressions.RegexOptions%29?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="2da11-108">Dzięki temu aparat wyrażeń regularnych może buforować wyrażenie regularne i pozwala uniknąć obciążenia wystąpienia nowego <xref:System.Text.RegularExpressions.Regex> obiektu za każdym razem, gdy wywoływana jest metoda.</span><span class="sxs-lookup"><span data-stu-id="2da11-108">This enables the regular expression engine to cache the regular expression and avoids the overhead of instantiating a new <xref:System.Text.RegularExpressions.Regex> object each time the method is called.</span></span> <span data-ttu-id="2da11-109"><xref:System.Text.RegularExpressions.Match>Obiekt jest następnie używany do iteracji we wszystkich dopasowaniach w ciągu.</span><span class="sxs-lookup"><span data-stu-id="2da11-109">A <xref:System.Text.RegularExpressions.Match> object is then used to iterate through all matches in the string.</span></span>  
  
 [!code-csharp[RegularExpressions.Examples.HREF#1](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.HREF/cs/example.cs#1)]
 [!code-vb[RegularExpressions.Examples.HREF#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.HREF/vb/example.vb#1)]  
  
 <span data-ttu-id="2da11-110">Poniższy przykład ilustruje wywołanie `DumpHRefs` metody.</span><span class="sxs-lookup"><span data-stu-id="2da11-110">The following example then illustrates a call to the `DumpHRefs` method.</span></span>  
  
 [!code-csharp[RegularExpressions.Examples.HREF#2](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.HREF/cs/example.cs#2)]
 [!code-vb[RegularExpressions.Examples.HREF#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.HREF/vb/example.vb#2)]  
  
 <span data-ttu-id="2da11-111">Wzorzec wyrażenia regularnego `href\s*=\s*(?:["'](?<1>[^"']*)["']|(?<1>\S+))` jest interpretowany jak pokazano w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="2da11-111">The regular expression pattern `href\s*=\s*(?:["'](?<1>[^"']*)["']|(?<1>\S+))` is interpreted as shown in the following table.</span></span>  
  
|<span data-ttu-id="2da11-112">Wzorce</span><span class="sxs-lookup"><span data-stu-id="2da11-112">Pattern</span></span>|<span data-ttu-id="2da11-113">Opis</span><span class="sxs-lookup"><span data-stu-id="2da11-113">Description</span></span>|  
|-------------|-----------------|  
|`href`|<span data-ttu-id="2da11-114">Dopasowuje ciąg literału "href".</span><span class="sxs-lookup"><span data-stu-id="2da11-114">Match the literal string "href".</span></span> <span data-ttu-id="2da11-115">W dopasowaniu nie jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="2da11-115">The match is case-insensitive.</span></span>|  
|`\s*`|<span data-ttu-id="2da11-116">Dopasowanie do zera lub większej liczby znaków odstępu.</span><span class="sxs-lookup"><span data-stu-id="2da11-116">Match zero or more white-space characters.</span></span>|  
|`=`|<span data-ttu-id="2da11-117">Dopasowuje znak równości.</span><span class="sxs-lookup"><span data-stu-id="2da11-117">Match the equals sign.</span></span>|  
|`\s*`|<span data-ttu-id="2da11-118">Dopasowanie do zera lub większej liczby znaków odstępu.</span><span class="sxs-lookup"><span data-stu-id="2da11-118">Match zero or more white-space characters.</span></span>|  
|`(?:\["'\](?<1>\[^"'\]*)["']\|(?<1>\S+))`|<span data-ttu-id="2da11-119">Dopasowanie jednego z następujących elementów bez przypisywania wyniku do przechwyconej grupy:</span><span class="sxs-lookup"><span data-stu-id="2da11-119">Match one of the following without assigning the result to a captured group:</span></span><br /> <ul><li><p><span data-ttu-id="2da11-120">Znak cudzysłowu lub apostrofu, po którym następuje zero lub więcej wystąpień dowolnego znaku innego niż znak cudzysłowu lub apostrofu, po którym następuje znak cudzysłowu lub apostrof.</span><span class="sxs-lookup"><span data-stu-id="2da11-120">A quotation mark or apostrophe, followed by zero or more occurrences of any character other than a quotation mark or apostrophe, followed by a quotation mark or apostrophe.</span></span> <span data-ttu-id="2da11-121">Grupa o nazwie `1` jest uwzględniona w tym wzorcu.</span><span class="sxs-lookup"><span data-stu-id="2da11-121">The group named `1` is included in this pattern.</span></span></p></li><li><p><span data-ttu-id="2da11-122">Co najmniej jeden znak niebędący odstępem.</span><span class="sxs-lookup"><span data-stu-id="2da11-122">One or more non-white-space characters.</span></span> <span data-ttu-id="2da11-123">Grupa o nazwie `1` jest uwzględniona w tym wzorcu.</span><span class="sxs-lookup"><span data-stu-id="2da11-123">The group named `1` is included in this pattern.</span></span></p></li></ul>|  
|`(?<1>[^"']*)`|<span data-ttu-id="2da11-124">Przypisz zero lub więcej wystąpień dowolnego znaku innego niż znak cudzysłowu lub apostrofu do grupy przechwytywania o nazwie `1` .</span><span class="sxs-lookup"><span data-stu-id="2da11-124">Assign zero or more occurrences of any character other than a quotation mark or apostrophe to the capturing group named `1`.</span></span>|  
|`(?<1>\S+)`|<span data-ttu-id="2da11-125">Przypisz co najmniej jeden znak niebędący odstępem do grupy przechwytywania o nazwie `1` .</span><span class="sxs-lookup"><span data-stu-id="2da11-125">Assign one or more non-white-space characters to the capturing group named `1`.</span></span>|  
  
## <a name="match-result-class"></a><span data-ttu-id="2da11-126">Dopasuj wynik klasy</span><span class="sxs-lookup"><span data-stu-id="2da11-126">Match Result Class</span></span>  

 <span data-ttu-id="2da11-127">Wyniki wyszukiwania są przechowywane w <xref:System.Text.RegularExpressions.Match> klasie, która zapewnia dostęp do wszystkich podciągów wyodrębnionych przez wyszukiwanie.</span><span class="sxs-lookup"><span data-stu-id="2da11-127">The results of a search are stored in the <xref:System.Text.RegularExpressions.Match> class, which provides access to all the substrings extracted by the search.</span></span> <span data-ttu-id="2da11-128">Odwołuje się również do wyszukiwanego ciągu i używanego wyrażenia regularnego, dzięki czemu można wywołać <xref:System.Text.RegularExpressions.Match.NextMatch%2A?displayProperty=nameWithType> metodę, aby wykonać inne wyszukiwanie, rozpoczynając od ostatniego zakończono.</span><span class="sxs-lookup"><span data-stu-id="2da11-128">It also remembers the string being searched and the regular expression being used, so it can call the <xref:System.Text.RegularExpressions.Match.NextMatch%2A?displayProperty=nameWithType> method to perform another search starting where the last one ended.</span></span>  
  
## <a name="explicitly-named-captures"></a><span data-ttu-id="2da11-129">Przechwytuje wyraźnie nazwane</span><span class="sxs-lookup"><span data-stu-id="2da11-129">Explicitly Named Captures</span></span>  

 <span data-ttu-id="2da11-130">W tradycyjnych wyrażeniach regularnych przechwytywanie nawiasów jest numerowane kolejno automatycznie.</span><span class="sxs-lookup"><span data-stu-id="2da11-130">In traditional regular expressions, capturing parentheses are automatically numbered sequentially.</span></span> <span data-ttu-id="2da11-131">Prowadzi to do dwóch problemów.</span><span class="sxs-lookup"><span data-stu-id="2da11-131">This leads to two problems.</span></span> <span data-ttu-id="2da11-132">Po pierwsze, jeśli wyrażenie regularne jest modyfikowane przez wstawianie lub usuwanie zestawu nawiasów, cały kod, który odwołuje się do numerowanych przechwytywania, musi zostać ponownie zapisany w celu odzwierciedlenia nowej numeracji.</span><span class="sxs-lookup"><span data-stu-id="2da11-132">First, if a regular expression is modified by inserting or removing a set of parentheses, all code that refers to the numbered captures must be rewritten to reflect the new numbering.</span></span> <span data-ttu-id="2da11-133">Drugi, ponieważ różne zestawy nawiasów często są używane do zapewnienia dwóch alternatywnych wyrażeń dla akceptowalnego dopasowania, może być trudne do ustalenia, które z dwóch wyrażeń faktycznie zwracają wynik.</span><span class="sxs-lookup"><span data-stu-id="2da11-133">Second, because different sets of parentheses often are used to provide two alternative expressions for an acceptable match, it might be difficult to determine which of the two expressions actually returned a result.</span></span>  
  
 <span data-ttu-id="2da11-134">Aby rozwiązać te problemy, <xref:System.Text.RegularExpressions.Regex> Klasa obsługuje składnię `(?<name>…)` przechwytywania dopasowania do określonego miejsca (miejsce może być nazwane przy użyciu ciągu lub liczby całkowitej; liczby całkowite można wielokrotnie odwoływać).</span><span class="sxs-lookup"><span data-stu-id="2da11-134">To address these problems, the <xref:System.Text.RegularExpressions.Regex> class supports the syntax `(?<name>…)` for capturing a match into a specified slot (the slot can be named using a string or an integer; integers can be recalled more quickly).</span></span> <span data-ttu-id="2da11-135">W rezultacie alternatywne dopasowania dla tego samego ciągu All można skierować do tego samego miejsca.</span><span class="sxs-lookup"><span data-stu-id="2da11-135">Thus, alternative matches for the same string all can be directed to the same place.</span></span> <span data-ttu-id="2da11-136">W przypadku konfliktu ostatnie dopasowanie opuszczone w gnieździe to pomyślne dopasowanie.</span><span class="sxs-lookup"><span data-stu-id="2da11-136">In case of a conflict, the last match dropped into a slot is the successful match.</span></span> <span data-ttu-id="2da11-137">(Jednak kompletna lista wielu dopasowań dla jednego gniazda jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="2da11-137">(However, a complete list of multiple matches for a single slot is available.</span></span> <span data-ttu-id="2da11-138">Szczegółowe informacje znajdują się w <xref:System.Text.RegularExpressions.Group.Captures%2A?displayProperty=nameWithType> kolekcji.</span><span class="sxs-lookup"><span data-stu-id="2da11-138">See the <xref:System.Text.RegularExpressions.Group.Captures%2A?displayProperty=nameWithType> collection for details.)</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="2da11-139">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="2da11-139">See also</span></span>

- [<span data-ttu-id="2da11-140">Wyrażenia regularne .NET</span><span class="sxs-lookup"><span data-stu-id="2da11-140">.NET Regular Expressions</span></span>](regular-expressions.md)
