---
title: Standardowe ciągi formatujące datę i godzinę
description: Dowiedz się, jak używać standardowego ciągu formatu daty i godziny, aby zdefiniować tekstową reprezentację wartości daty i godziny w programie .NET.
ms.date: 12/07/2020
dev_langs:
- csharp
- vb
helpviewer_keywords:
- formatting [.NET], dates
- custom DateTime format string
- format specifiers, custom date and time
- format strings
- custom date and time format strings
- formatting [.NET], time
- date and time strings
ms.topic: reference
ms.custom: contperfq2
ms.openlocfilehash: 688aaf7a1814e132f3bffa48394873653bf314e8
ms.sourcegitcommit: 45c7148f2483db2501c1aa696ab6ed2ed8cb71b2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/08/2020
ms.locfileid: "96851135"
---
# <a name="standard-date-and-time-format-strings"></a>Standardowe ciągi formatujące datę i godzinę

Standardowy ciąg formatu daty i godziny używa pojedynczego znaku jako specyfikatora formatu do definiowania tekstowej reprezentacji <xref:System.DateTime> lub <xref:System.DateTimeOffset> wartości. Dowolny ciąg formatu daty i godziny, który zawiera więcej niż jeden znak, w tym znak odstępu, jest interpretowany jako [ciąg niestandardowego formatu daty i godziny](custom-date-and-time-format-strings.md). Ciągu formatu standardowego lub niestandardowego można używać na dwa sposoby:

- Aby zdefiniować ciąg będący wynikiem operacji formatowania.

- Aby zdefiniować tekstową reprezentację wartości daty i godziny, która może zostać przekonwertowana <xref:System.DateTime> na <xref:System.DateTimeOffset> wartość lub przez operację analizowania.

> [!TIP]
> Możesz pobrać **Narzędzie formatowania**, aplikację platformy .NET Windows Forms, która umożliwia stosowanie ciągów formatowania do wartości liczbowych lub daty i godziny i wyświetlanie ciągu wynikowego. Kod źródłowy jest dostępny dla [języków C#](/samples/dotnet/samples/windowsforms-formatting-utility-cs) i [Visual Basic](/samples/dotnet/samples/windowsforms-formatting-utility-vb).

[!INCLUDE[C# interactive-note](~/includes/csharp-interactive-with-utc-partial-note.md)]

## <a name="table-of-format-specifiers"></a>Tabela specyfikatorów formatu

<a name="table"></a> W poniższej tabeli opisano specyfikatory standardowego formatu daty i godziny. O ile nie zaznaczono inaczej, określony standardowy specyfikator formatu daty i godziny generuje identyczny ciąg reprezentacji, niezależnie od tego, czy jest używany z <xref:System.DateTime> lub <xref:System.DateTimeOffset> wartością. Zobacz [Ustawienia panelu sterowania](#control-panel-settings) i [właściwości DateTimeFormatInfo](#datetimeformatinfo-properties) , aby uzyskać dodatkowe informacje na temat korzystania z ciągów standardowych formatów daty i godziny.

|Specyfikator formatu|Opis|Przykłady|
|----------------------|-----------------|--------------|
|„d”|Wzorzec daty krótkiej.<br /><br /> Więcej informacji:[specyfikator formatu daty krótkiej ("d")](#ShortDate).|2009-06-15T13:45:30-> 6/15/2009 (EN-US)<br /><br /> 2009-06-15T13:45:30-> 15/06/2009 (fr-FR)<br /><br /> 2009-06-15T13:45:30-> 2009/06/15 (ja-JP)|
|„D”|Wzorzec daty długiej.<br /><br /> Więcej informacji:[specyfikator formatu daty długiej ("D")](#LongDate).|2009-06-15T13:45:30-> poniedziałek, 15 czerwca, 2009 (EN-US)<br /><br /> 2009-06-15T13:45:30-> 15 июня 2009 г. (ru-RU)<br /><br /> 2009-06-15T13:45:30-> Montag, 15. Juni 2009 (de-DE)|
|„f”|Wzorzec pełnej daty/godziny (godzina krótka).<br /><br /> Więcej informacji: [specyfikator formatu pełnej daty i godziny krótkiej ("f")](#FullDateShortTime).|2009-06-15T13:45:30-> poniedziałek, 15 czerwca, 2009 1:45 PM (pl-US)<br /><br /> 2009-06-15T13:45:30-> Den 15 Juni 2009 13:45 (SV-SE)<br /><br /> 2009-06-15T13:45:30-> Δευτέρα, 15 Ιουνίου 2009 1:45 Μμ (El-GR)|
|„F”|Wzorzec pełnej daty/godziny (godzina długa).<br /><br /> Więcej informacji: [specyfikator formatu pełnej daty i godziny długiej ("F")](#FullDateLongTime).|2009-06-15T13:45:30-> poniedziałek, 15 czerwca, 2009 1:45:30 PM (pl-US)<br /><br /> 2009-06-15T13:45:30-> Den 15 Juni 2009 13:45:30 (SV-SE)<br /><br /> 2009-06-15T13:45:30-> Δευτέρα, 15 Ιουνίου 2009 1:45:30 Μμ (El-GR)|
|„g”|Wzorzec ogólnej daty/godziny (godzina krótka).<br /><br /> Więcej informacji: [specyfikator formatu daty ogólnej i godziny krótkiej ("g")](#GeneralDateShortTime).|2009-06-15T13:45:30-> 6/15/2009 1:45 PM (pl-US)<br /><br /> 2009-06-15T13:45:30-> 15/06/2009 13:45 (es-ES)<br /><br /> 2009-06-15T13:45:30-> 2009/6/15 13:45 (zh-CN)|
|„G”|Wzorzec ogólnej daty/godziny (godzina długa).<br /><br /> Więcej informacji: [specyfikator formatu daty ogólnej godziny długiej ("G")](#GeneralDateLongTime).|2009-06-15T13:45:30-> 6/15/2009 1:45:30 PM (pl-US)<br /><br /> 2009-06-15T13:45:30-> 15/06/2009 13:45:30 (es-ES)<br /><br /> 2009-06-15T13:45:30-> 2009/6/15 13:45:30 (zh-CN)|
|„M”, „m”|Wzorzec miesiąc/dzień.<br /><br /> Więcej informacji: [specyfikator formatu miesiąca ("m", "m")](#MonthDay).|2009-06-15T13:45:30 — > Czerwiec 15 (EN-US)<br /><br /> 2009 — 06-15T13:45:30-> 15. Juni (da-DK)<br /><br /> 2009-06-15T13:45:30-> 15 Juni (identyfikator ID)|
|„O”, „o”|wzorzec daty/godziny rundy.<br /><br /> Więcej informacji: [specyfikator formatu rundying ("o", "o")](#Roundtrip).|<xref:System.DateTime> wartością<br /><br /> 2009-06-15T13:45:30 (DateTimeKind. local)--> 2009-06-15T13:45:30.0000000-07:00<br /><br /> 2009-06-15T13:45:30 (DateTimeKind. UTC)--> 2009-06-15T13:45:30.0000000 Z<br /><br /> 2009-06-15T13:45:30 (DateTimeKind.)--> 2009-06-15T13:45:30.0000000<br /><br /> <xref:System.DateTimeOffset> wartością<br /><br /> 2009-06-15T13:45:30-07:00--> 2009-06-15T13:45:30.0000000-07:00|
|„R”, „r”|Wzorzec RFC1123.<br /><br /> Więcej informacji: [specyfikator formatu RFC1123 ("r", "r")](#RFC1123).|2009-06-15T13:45:30-> PN, 15 Jun 2009 20:45:30 GMT|
|„s”|Wzorzec sortowalnej daty/godziny.<br /><br /> Więcej informacji: [specyfikator formatu sortowania ("s")](#Sortable).|2009-06-15T13:45:30 (DateTimeKind. local)-> 2009-06-15T13:45:30<br /><br /> 2009-06-15T13:45:30 (DateTimeKind. UTC)-> 2009-06-15T13:45:30|
|„t”|Wzorzec godziny krótkiej.<br /><br /> Więcej informacji: [specyfikator formatu godziny krótkiej ("t")](#ShortTime).|2009-06-15T13:45:30-> 1:45 PM (pl-US)<br /><br /> 2009-06-15T13:45:30-> 13:45 (HR-HR)<br /><br /> 2009-06-15T13:45:30-> 01:45 م (AR-EG)|
|„T”|Wzorzec godziny długiej.<br /><br /> Więcej informacji: [specyfikator formatu godziny długiej ("T")](#LongTime).|2009-06-15T13:45:30-> 1:45:30 PM (pl-US)<br /><br /> 2009-06-15T13:45:30-> 13:45:30 (HR-HR)<br /><br /> 2009-06-15T13:45:30-> 01:45:30 م (AR-EG)|
|„u”|Wzorzec uniwersalnej sortowalnej daty/godziny.<br /><br /> Więcej informacji: [specyfikator formatu uniwersalnego sortowania ("u")](#UniversalSortable).|Mając <xref:System.DateTime> wartość: 2009-06-15T13:45:30-> 2009-06-15 13:45:30Z<br /><br /> Mając <xref:System.DateTimeOffset> wartość: 2009-06-15T13:45:30-> 2009-06-15 20:45:30Z|
|„U”|Wzorzec uniwersalnej pełnej daty/godziny.<br /><br /> Więcej informacji: [specyfikator formatu uniwersalnego pełnego ("U")](#UniversalFull).|2009-06-15T13:45:30-> poniedziałek, 15 czerwca, 2009 8:45:30 PM (pl-US)<br /><br /> 2009-06-15T13:45:30-> Den 15 Juni 2009 20:45:30 (SV-SE)<br /><br /> 2009-06-15T13:45:30-> Δευτέρα, 15 Ιουνίου 2009 8:45:30 Μμ (El-GR)|
|„Y”, „y”|Wzorzec roku i miesiąca.<br /><br /> Więcej informacji: [specyfikator formatu roku miesiąca ("Y")](#YearMonth).|2009-06-15T13:45:30-> czerwiec 2009 (EN-US)<br /><br /> 2009-06-15T13:45:30-> Juni 2009 (da-DK)<br /><br /> 2009-06-15T13:45:30-> Juni 2009 (identyfikator ID)|
|Jakikolwiek inny pojedynczy znak|Nieznany specyfikator.|Zgłasza czas wykonywania <xref:System.FormatException> .|

## <a name="how-standard-format-strings-work"></a>Jak działają ciągi formatu standardowego

W operacji formatowania ciąg formatu standardowego jest po prostu aliasem ciągu formatu niestandardowego. Zaletą użycia aliasu w celu odwołania się do ciągu formatu niestandardowego jest to, że ciąg formatu niestandardowego może być różny, mimo że alias pozostaje niezmienny. Jest to ważne, ponieważ ciągi reprezentujące wartości daty i godziny są zazwyczaj różne w zależności od kultury. Na przykład ciąg formatu standardowego „d” wskazuje, że wartość daty i godziny zostanie wyświetlona przy użyciu wzorca daty krótkiej. Ten wzorzec dla niezmiennej kultury to „MM/dd/yyyy”. Dla kultury fr-FR jest to „dd/MM/yyyy”. Dla kultury ja-JP jest to „yyyy/MM/dd”.

Jeśli ciąg formatu standardowego w operacji formatowania jest mapowany na ciąg formatu niestandardowego danej kultury, aplikacja może definiować określoną kulturę, której ciągi formatu niestandardowego są używane na jeden z poniższych sposobów:

- Można użyć domyślnej (bieżącej) kultury. W poniższym przykładzie data jest wyświetlana przy użyciu formatu daty krótkiej dla bieżącej kultury. Bieżącą kulturą jest w tym przypadku kultura en-US.

  [!code-csharp-interactive[System.DateTime.Conceptual.Formatting#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTime.Conceptual.Formatting/cs/StandardFormats1.cs#1)]
  [!code-vb[System.DateTime.Conceptual.Formatting#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTime.Conceptual.Formatting/vb/StandardFormats1.vb#1)]

- Można przekazać <xref:System.Globalization.CultureInfo> obiekt reprezentujący kulturę, której formatowanie ma być używane do metody, która ma <xref:System.IFormatProvider> parametr. W poniższym przykładzie data jest wyświetlana przy użyciu formatu daty krótkiej dla kultury pt-BR.

  [!code-csharp[System.DateTime.Conceptual.Formatting#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTime.Conceptual.Formatting/cs/StandardFormats1.cs#2)]
  [!code-vb[System.DateTime.Conceptual.Formatting#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTime.Conceptual.Formatting/vb/StandardFormats1.vb#2)]

- Można przekazać <xref:System.Globalization.DateTimeFormatInfo> obiekt, który dostarcza informacje o formatowaniu do metody, która ma <xref:System.IFormatProvider> parametr. Poniższy przykład wyświetla datę przy użyciu formatu daty krótkiej z <xref:System.Globalization.DateTimeFormatInfo> obiektu dla kultury HR-HR.

  [!code-csharp[System.DateTime.Conceptual.Formatting#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTime.Conceptual.Formatting/cs/StandardFormats1.cs#3)]
  [!code-vb[System.DateTime.Conceptual.Formatting#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTime.Conceptual.Formatting/vb/StandardFormats1.vb#3)]

> [!NOTE]
> Aby uzyskać informacje na temat dostosowywania wzorców lub ciągów używanych w formatowaniu wartości daty i godziny, zobacz <xref:System.Globalization.NumberFormatInfo> temat Klasa.

W niektórych przypadkach ciąg formatu standardowego służy jako wygodny skrót dla dłuższego ciągu formatu niestandardowego, który jest niezmienny. Cztery ciągi formatu standardowego należą do tej kategorii: „O” (lub „o”), „R” (lub „r”), „s” i „u”. Te ciągi odpowiadają ciągom formatów niestandardowych, które są zdefiniowane przez niezmienną kulturę. Wytwarzają one reprezentacje wartości daty i godziny w postaci ciągu, które mają być identyczne dla różnych kultur. W poniższej tabeli przedstawiono informacje dotyczące tych czterech ciągów standardowych formatów daty i godziny.

|Ciąg formatu standardowego|Definiowany przez właściwość DateTimeFormatInfo.InvariantInfo|Ciąg formatu niestandardowego|
|----------------------------|----------------------------------------------------------|--------------------------|
|„O” lub „o”|Brak|yyyy'-'MM'-'dd'T'HH':'mm':'ss'.'fffffffzz|
|„R” lub „r”|<xref:System.Globalization.DateTimeFormatInfo.RFC1123Pattern%2A>|ddd, dd MMM yyyy HH':'mm':'ss 'GMT'|
|„s”|<xref:System.Globalization.DateTimeFormatInfo.SortableDateTimePattern%2A>|yyyy'-'MM'-'dd'T'HH':'mm':'ss|
|„u”|<xref:System.Globalization.DateTimeFormatInfo.UniversalSortableDateTimePattern%2A>|yyyy'-'MM'-'dd HH':'mm':'ss'Z'|

Ciągi formatu standardowego mogą być również używane podczas analizowania operacji przy użyciu <xref:System.DateTime.ParseExact%2A?displayProperty=nameWithType> <xref:System.DateTimeOffset.ParseExact%2A?displayProperty=nameWithType> metod lub, które wymagają, aby ciąg wejściowy był dokładnie zgodny z określonym wzorcem w celu pomyślnego wykonania operacji analizy. Wiele ciągów formatów standardowych jest mapowanych na wielu ciągów formatów niestandardowych, więc wartość daty i godziny może być reprezentowana przez wiele formatów, a operacja analizy i tak zakończy się powodzeniem. Możesz określić ciąg formatu niestandardowego lub ciągi, które odpowiadają ciągowi standardowego formatu, wywołując <xref:System.Globalization.DateTimeFormatInfo.GetAllDateTimePatterns%28System.Char%29?displayProperty=nameWithType> metodę. W poniższym przykładzie są wyświetlane ciągi formatów niestandardowych mapowane na ciąg formatu standardowego „d” (wzorzec daty krótkiej).

[!code-csharp[Formatting.DateAndTime.Standard#17](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/stdandparsing1.cs#17)]
[!code-vb[Formatting.DateAndTime.Standard#17](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/stdandparsing1.vb#17)]

W poniższych sekcjach opisano specyfikatory formatu standardowego <xref:System.DateTime> i <xref:System.DateTimeOffset> wartości.

## <a name="date-formats"></a>Formaty dat

Ta grupa zawiera następujące formaty:

- [Specyfikator formatu daty krótkiej ("d")](#the-short-date-d-format-specifier)
- [Specyfikator formatu daty długiej ("D")](#the-long-date-d-format-specifier)

<a name="ShortDate"></a>

### <a name="the-short-date-d-format-specifier"></a>Specyfikator formatu daty krótkiej ("d")

Specyfikator formatu standardowego "d" reprezentuje ciąg niestandardowego formatu daty i godziny, który jest definiowany przez określoną <xref:System.Globalization.DateTimeFormatInfo.ShortDatePattern%2A?displayProperty=nameWithType> Właściwość kultury. Na przykład ciąg formatu niestandardowego, który jest zwracany przez <xref:System.Globalization.DateTimeFormatInfo.ShortDatePattern%2A> Właściwość niezmiennej kultury to "mm/dd/rrrr".

Poniższa tabela zawiera listę <xref:System.Globalization.DateTimeFormatInfo> właściwości obiektu, które sterują formatowaniem zwracanego ciągu.

|Właściwość|Opis|
|--------------|-----------------|
|<xref:System.Globalization.DateTimeFormatInfo.ShortDatePattern%2A>|Definiuje ogólny format ciągu wynikowego.|
|<xref:System.Globalization.DateTimeFormatInfo.DateSeparator%2A>|Określa ciąg, który oddziela składniki daty: rok, miesiąc i dzień.|

W poniższym przykładzie użyto specyfikatora formatu „d”, aby wyświetlić wartość daty i godziny.

[!code-csharp[Formatting.DateAndTime.Standard#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#1)]
[!code-vb[Formatting.DateAndTime.Standard#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#1)]

[Wróć do tabeli](#table)

<a name="LongDate"></a>

### <a name="the-long-date-d-format-specifier"></a>Specyfikator formatu daty długiej ("D")

Specyfikator formatu standardowego "D" reprezentuje ciąg niestandardowego formatu daty i godziny, który jest definiowany przez bieżącą <xref:System.Globalization.DateTimeFormatInfo.LongDatePattern%2A?displayProperty=nameWithType> Właściwość. Na przykład ciąg formatu niestandardowego dla niezmiennej kultury to „dddd, dd MMMM yyyy”.

Poniższa tabela zawiera listę właściwości <xref:System.Globalization.DateTimeFormatInfo> obiektu, które sterują formatowaniem zwracanego ciągu.

|Właściwość|Opis|
|--------------|-----------------|
|<xref:System.Globalization.DateTimeFormatInfo.LongDatePattern%2A>|Definiuje ogólny format ciągu wynikowego.|
|<xref:System.Globalization.DateTimeFormatInfo.DayNames%2A>|Definiuje zlokalizowane nazwy dni, które mogą być wyświetlane w ciągu wynikowym.|
|<xref:System.Globalization.DateTimeFormatInfo.MonthNames%2A>|Definiuje zlokalizowane nazwy miesięcy, które mogą być wyświetlane w ciągu wynikowym.|

W poniższym przykładzie użyto specyfikatora formatu „D”, aby wyświetlić wartość daty i godziny.

[!code-csharp[Formatting.DateAndTime.Standard#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#2)]
[!code-vb[Formatting.DateAndTime.Standard#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#2)]

[Wróć do tabeli](#table)

## <a name="date-and-time-formats"></a>Formaty daty i godziny

Ta grupa zawiera następujące formaty:

- [Specyfikator formatu pełnej daty i godziny krótkiej ("f")](#the-full-date-short-time-f-format-specifier)
- [Specyfikator formatu pełnej daty i godziny długiej ("F")](#the-full-date-long-time-f-format-specifier)
- [Specyfikator formatu daty ogólnej i godziny krótkiej ("g")](#the-general-date-short-time-g-format-specifier)
- [Specyfikator formatu daty/godziny długiej ("G")](#the-general-date-long-time-g-format-specifier)
- [Specyfikator formatu rundy ("O", "o")](#the-round-trip-o-o-format-specifier)
- [Specyfikator formatu RFC1123 ("R", "r")](#the-rfc1123-r-r-format-specifier)
- [Specyfikator formatu sortowania ("s")](#the-sortable-s-format-specifier)
- [Specyfikator formatu uniwersalnego sortowania ("u")](#the-universal-sortable-u-format-specifier)
- [Specyfikator formatu uniwersalnej pełnej ("U")](#the-universal-full-u-format-specifier)

<a name="FullDateShortTime"></a>

### <a name="the-full-date-short-time-f-format-specifier"></a>Specyfikator formatu pełnej daty i godziny krótkiej ("f")

Specyfikator formatu standardowego „f” reprezentuje kombinację wzorców daty długiej („D”) i godziny krótkiej („t”), rozdzielonych spacją.

Informacje o formatowaniu określonego obiektu mają wpływ na ciąg wynikowy <xref:System.Globalization.DateTimeFormatInfo> . Poniższa tabela zawiera listę <xref:System.Globalization.DateTimeFormatInfo> właściwości obiektu, które mogą kontrolować formatowanie zwracanego ciągu. Specyfikator formatu niestandardowego zwracany przez <xref:System.Globalization.DateTimeFormatInfo.LongDatePattern%2A?displayProperty=nameWithType> <xref:System.Globalization.DateTimeFormatInfo.ShortTimePattern%2A?displayProperty=nameWithType> właściwości i niektórych kultur może nie używać wszystkich właściwości.

|Właściwość|Opis|
|--------------|-----------------|
|<xref:System.Globalization.DateTimeFormatInfo.LongDatePattern%2A>|Definiuje format składnika daty w ciągu wynikowym.|
|<xref:System.Globalization.DateTimeFormatInfo.ShortTimePattern%2A>|Definiuje format składnika godziny w ciągu wynikowym.|
|<xref:System.Globalization.DateTimeFormatInfo.DayNames%2A>|Definiuje zlokalizowane nazwy dni, które mogą być wyświetlane w ciągu wynikowym.|
|<xref:System.Globalization.DateTimeFormatInfo.MonthNames%2A>|Definiuje zlokalizowane nazwy miesięcy, które mogą być wyświetlane w ciągu wynikowym.|
|<xref:System.Globalization.DateTimeFormatInfo.TimeSeparator%2A>|Definiuje ciąg, który rozdziela składniki godziny, minuty i sekundy w ciągu reprezentującym godzinę.|
|<xref:System.Globalization.DateTimeFormatInfo.AMDesignator%2A>|Określa ciąg, który wskazuje czas od północy do południa (z wyłączeniem południa), w formacie 12-godzinnym.|
|<xref:System.Globalization.DateTimeFormatInfo.PMDesignator%2A>|Określa ciąg, który wskazuje czas od południa do północy (z wyłączeniem północy), w formacie 12-godzinnym.|

W poniższym przykładzie użyto specyfikatora formatu „f”, aby wyświetlić wartość daty i godziny.

[!code-csharp[Formatting.DateAndTime.Standard#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#3)]
[!code-vb[Formatting.DateAndTime.Standard#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#3)]

[Wróć do tabeli](#table)

<a name="FullDateLongTime"></a>

### <a name="the-full-date-long-time-f-format-specifier"></a>Specyfikator formatu pełnej daty i godziny długiej ("F")

Specyfikator formatu standardowego "F" reprezentuje ciąg niestandardowego formatu daty i godziny, który jest definiowany przez bieżącą <xref:System.Globalization.DateTimeFormatInfo.FullDateTimePattern%2A?displayProperty=nameWithType> Właściwość. Na przykład ciąg formatu niestandardowego dla niezmiennej kultury to „dddd, dd MMMM yyyy HH:mm:ss”.

Poniższa tabela zawiera listę <xref:System.Globalization.DateTimeFormatInfo> właściwości obiektu, które mogą kontrolować formatowanie zwracanego ciągu. Specyfikator formatu niestandardowego zwracany przez <xref:System.Globalization.DateTimeFormatInfo.FullDateTimePattern%2A> Właściwość niektórych kultur może nie używać wszystkich właściwości.

|Właściwość|Opis|
|--------------|-----------------|
|<xref:System.Globalization.DateTimeFormatInfo.FullDateTimePattern%2A>|Definiuje ogólny format ciągu wynikowego.|
|<xref:System.Globalization.DateTimeFormatInfo.DayNames%2A>|Definiuje zlokalizowane nazwy dni, które mogą być wyświetlane w ciągu wynikowym.|
|<xref:System.Globalization.DateTimeFormatInfo.MonthNames%2A>|Definiuje zlokalizowane nazwy miesięcy, które mogą być wyświetlane w ciągu wynikowym.|
|<xref:System.Globalization.DateTimeFormatInfo.TimeSeparator%2A>|Definiuje ciąg, który rozdziela składniki godziny, minuty i sekundy w ciągu reprezentującym godzinę.|
|<xref:System.Globalization.DateTimeFormatInfo.AMDesignator%2A>|Określa ciąg, który wskazuje czas od północy do południa (z wyłączeniem południa), w formacie 12-godzinnym.|
|<xref:System.Globalization.DateTimeFormatInfo.PMDesignator%2A>|Określa ciąg, który wskazuje czas od południa do północy (z wyłączeniem północy), w formacie 12-godzinnym.|

W poniższym przykładzie użyto specyfikatora formatu „F”, aby wyświetlić wartość daty i godziny.

[!code-csharp[Formatting.DateAndTime.Standard#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#4)]
[!code-vb[Formatting.DateAndTime.Standard#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#4)]

[Wróć do tabeli](#table)

<a name="GeneralDateShortTime"></a>

### <a name="the-general-date-short-time-g-format-specifier"></a>Specyfikator formatu daty ogólnej i godziny krótkiej ("g")

Specyfikator formatu standardowego „g” reprezentuje kombinację wzorców daty krótkiej („g”) i godziny krótkiej („t”), rozdzielonych spacją.

Informacje o formatowaniu określonego obiektu mają wpływ na ciąg wynikowy <xref:System.Globalization.DateTimeFormatInfo> . Poniższa tabela zawiera listę <xref:System.Globalization.DateTimeFormatInfo> właściwości obiektu, które mogą kontrolować formatowanie zwracanego ciągu. Specyfikator formatu niestandardowego zwracany przez <xref:System.Globalization.DateTimeFormatInfo.ShortDatePattern%2A?displayProperty=nameWithType> <xref:System.Globalization.DateTimeFormatInfo.ShortTimePattern%2A?displayProperty=nameWithType> właściwości i niektórych kultur może nie używać wszystkich właściwości.

|Właściwość|Opis|
|--------------|-----------------|
|<xref:System.Globalization.DateTimeFormatInfo.ShortDatePattern%2A>|Definiuje format składnika daty w ciągu wynikowym.|
|<xref:System.Globalization.DateTimeFormatInfo.ShortTimePattern%2A>|Definiuje format składnika godziny w ciągu wynikowym.|
|<xref:System.Globalization.DateTimeFormatInfo.DateSeparator%2A>|Określa ciąg, który oddziela składniki daty: rok, miesiąc i dzień.|
|<xref:System.Globalization.DateTimeFormatInfo.TimeSeparator%2A>|Definiuje ciąg, który rozdziela składniki godziny, minuty i sekundy w ciągu reprezentującym godzinę.|
|<xref:System.Globalization.DateTimeFormatInfo.AMDesignator%2A>|Określa ciąg, który wskazuje czas od północy do południa (z wyłączeniem południa), w formacie 12-godzinnym.|
|<xref:System.Globalization.DateTimeFormatInfo.PMDesignator%2A>|Określa ciąg, który wskazuje czas od południa do północy (z wyłączeniem północy), w formacie 12-godzinnym.|

W poniższym przykładzie użyto specyfikatora formatu „g”, aby wyświetlić wartość daty i godziny.

[!code-csharp[Formatting.DateAndTime.Standard#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#5)]
[!code-vb[Formatting.DateAndTime.Standard#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#5)]

[Wróć do tabeli](#table)

<a name="GeneralDateLongTime"></a>

### <a name="the-general-date-long-time-g-format-specifier"></a>Specyfikator formatu daty/godziny długiej ("G")

Specyfikator formatu standardowego „G” reprezentuje kombinację wzorców daty krótkiej („d”) i godziny długiej („T”), rozdzielonych spacją.

Informacje o formatowaniu określonego obiektu mają wpływ na ciąg wynikowy <xref:System.Globalization.DateTimeFormatInfo> . Poniższa tabela zawiera listę <xref:System.Globalization.DateTimeFormatInfo> właściwości obiektu, które mogą kontrolować formatowanie zwracanego ciągu. Specyfikator formatu niestandardowego zwracany przez <xref:System.Globalization.DateTimeFormatInfo.ShortDatePattern%2A?displayProperty=nameWithType> <xref:System.Globalization.DateTimeFormatInfo.LongTimePattern%2A?displayProperty=nameWithType> właściwości i niektórych kultur może nie używać wszystkich właściwości.

|Właściwość|Opis|
|--------------|-----------------|
|<xref:System.Globalization.DateTimeFormatInfo.ShortDatePattern%2A>|Definiuje format składnika daty w ciągu wynikowym.|
|<xref:System.Globalization.DateTimeFormatInfo.LongTimePattern%2A>|Definiuje format składnika godziny w ciągu wynikowym.|
|<xref:System.Globalization.DateTimeFormatInfo.DateSeparator%2A>|Określa ciąg, który oddziela składniki daty: rok, miesiąc i dzień.|
|<xref:System.Globalization.DateTimeFormatInfo.TimeSeparator%2A>|Definiuje ciąg, który rozdziela składniki godziny, minuty i sekundy w ciągu reprezentującym godzinę.|
|<xref:System.Globalization.DateTimeFormatInfo.AMDesignator%2A>|Określa ciąg, który wskazuje czas od północy do południa (z wyłączeniem południa), w formacie 12-godzinnym.|
|<xref:System.Globalization.DateTimeFormatInfo.PMDesignator%2A>|Określa ciąg, który wskazuje czas od południa do północy (z wyłączeniem północy), w formacie 12-godzinnym.|

W poniższym przykładzie użyto specyfikatora formatu „G”, aby wyświetlić wartość daty i godziny.

[!code-csharp[Formatting.DateAndTime.Standard#6](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#6)]
[!code-vb[Formatting.DateAndTime.Standard#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#6)]

[Wróć do tabeli](#table)

<a name="Roundtrip"></a>

### <a name="the-round-trip-o-o-format-specifier"></a>Specyfikator formatu rundy ("O", "o")

Specyfikator formatu standardowego "O" lub "o" reprezentuje ciąg niestandardowego formatu daty i godziny przy użyciu wzorca, który zachowuje informacje o strefie czasowej i emituje ciąg wynikowy, który jest zgodny z normą ISO 8601. Dla <xref:System.DateTime> wartości, ten specyfikator formatu jest przeznaczony do zachowywania wartości daty i godziny wraz z <xref:System.DateTime.Kind%2A?displayProperty=nameWithType> właściwością w tekście. Sformatowany ciąg może być analizowany z powrotem przy użyciu <xref:System.DateTime.Parse%28System.String%2CSystem.IFormatProvider%2CSystem.Globalization.DateTimeStyles%29?displayProperty=nameWithType> metody lub, <xref:System.DateTime.ParseExact%2A?displayProperty=nameWithType> Jeśli `styles` parametr jest ustawiony na <xref:System.Globalization.DateTimeStyles.RoundtripKind?displayProperty=nameWithType> .

Specyfikator formatu standardowego "O" lub "o" odpowiada elementowi "yyyy'-'MM'-'dd'T'HH": "mm": "SS". fffffffK "niestandardowy ciąg formatu dla <xref:System.DateTime> wartości i do" yyyy'-'MM'-'dd'T'HH ":" mm ":" SS "." fffffffzzz "niestandardowy ciąg formatu dla <xref:System.DateTimeOffset> wartości. W tym ciągu pary znaków apostrofu, które oddzielają pojedyncze znaki, takie jak łączniki, dwukropki i litera „T”, wskazują, że indywidualny znak jest literałem, który nie może być zmieniony. Apostrofy nie znajdują się w ciągu wyjściowym.

Specyfikator formatu standardowego "O" lub "o" (oraz "yyyy'-'MM'-'dd'T'HH": "mm": "SS". " fffffffK "niestandardowy ciąg formatu) korzysta z trzech sposobów, w jaki ISO 8601 reprezentuje informacje o strefie czasowej, aby zachować <xref:System.DateTime.Kind%2A> Właściwość <xref:System.DateTime> wartości:

- Składnik strefy czasowej <xref:System.DateTimeKind.Local?displayProperty=nameWithType> wartości daty i godziny jest przesunięciem od czasu UTC (na przykład + 01:00,-07:00). Wszystkie <xref:System.DateTimeOffset> wartości są również reprezentowane w tym formacie.

- Składnik strefy czasowej <xref:System.DateTimeKind.Utc?displayProperty=nameWithType> wartości daty i godziny używa "Z" (co oznacza przesunięcie zerowe) do reprezentowania czasu UTC.

- <xref:System.DateTimeKind.Unspecified?displayProperty=nameWithType> wartości daty i godziny nie zawierają informacji o strefie czasowej.

Ze względu na to, że specyfikator formatu standardowego "O" lub "o" jest zgodny ze standardem międzynarodowym, Operacja formatowania lub analizowania, która używa specyfikatora zawsze używa niezmiennej kultury i kalendarza gregoriańskiego.

Ciągi, które są przesyłane do `Parse` `TryParse` `ParseExact` `TryParseExact` metod <xref:System.DateTime> i <xref:System.DateTimeOffset> można analizować przy użyciu specyfikatora formatu "O" lub "o", jeśli znajdują się w jednym z tych formatów. W przypadku <xref:System.DateTime> obiektów, przetwarzanie przeciążenia, które można wywołać, powinno również zawierać `styles` parametr z wartością <xref:System.Globalization.DateTimeStyles.RoundtripKind?displayProperty=nameWithType> . Należy pamiętać, że w przypadku wywołania metody analizy z niestandardowym ciągiem formatu, który odpowiada specyfikatorowi formatu "O" lub "o", nie da się uzyskać tych samych wyników co "O" lub "o". Wynika to z faktu, że metody analizy używające niestandardowego ciągu formatu nie mogą przeanalizować ciągu reprezentującego wartości daty i godziny, które nie są składnikiem strefy czasowej, lub użyć "Z", aby wskazać czas UTC.

W poniższym przykładzie pokazano użycie specyfikatora formatu "o", aby wyświetlić serię <xref:System.DateTime> wartości i <xref:System.DateTimeOffset> wartość w systemie w strefie czasowej pacyficznego w Stanach Zjednoczonych.

[!code-csharp[Formatting.DateAndTime.Standard#8](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/o1.cs#8)]
[!code-vb[Formatting.DateAndTime.Standard#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/o1.vb#8)]

Poniższy przykład używa specyfikatora formatu "o", aby utworzyć sformatowany ciąg, a następnie przywraca oryginalną wartość daty i godziny przez wywołanie metody daty i godziny `Parse` .

[!code-csharp[Formatting.DateandTime.Standard#16](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Roundtrip1.cs#16)]
[!code-vb[Formatting.DateandTime.Standard#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/RoundTrip1.vb#16)]

[Wróć do tabeli](#table)

<a name="RFC1123"></a>

### <a name="the-rfc1123-r-r-format-specifier"></a>Specyfikator formatu RFC1123 ("R", "r")

Specyfikator formatu standardowego "R" lub "r" reprezentuje ciąg niestandardowego formatu daty i godziny, który jest zdefiniowany przez <xref:System.Globalization.DateTimeFormatInfo.RFC1123Pattern%2A?displayProperty=nameWithType> Właściwość. Wzorzec odzwierciedla zdefiniowany standard, a właściwość jest tylko do odczytu. Dlatego też zawsze jest taki sam, niezależnie od używanej kultury oraz dostarczonego dostawcy formatów. Ciąg formatu niestandardowego to „ddd, dd MMM yyyy HH':'mm':'ss 'GMT'”. Gdy jest używany ten specyfikator formatu standardowego, w operacji formatowania lub analizowania zawsze jest używana niezmienna kultura.

Ciąg wynikowy ma wpływ na następujące właściwości <xref:System.Globalization.DateTimeFormatInfo> obiektu zwróconego przez <xref:System.Globalization.DateTimeFormatInfo.InvariantInfo%2A?displayProperty=nameWithType> Właściwość, która reprezentuje niezmienną kulturę.

|Właściwość|Opis|
|--------------|-----------------|
|<xref:System.Globalization.DateTimeFormatInfo.RFC1123Pattern%2A>|Definiuje format ciągu wynikowego.|
|<xref:System.Globalization.DateTimeFormatInfo.AbbreviatedDayNames%2A>|Definiuje skrócone nazwy dni, które mogą być wyświetlane w ciągu wynikowym.|
|<xref:System.Globalization.DateTimeFormatInfo.AbbreviatedMonthNames%2A>|Definiuje skrócone nazwy miesięcy, które mogą być wyświetlane w ciągu wynikowym.|

Mimo że standard RFC 1123 wyraża czas jako uniwersalny czas koordynowany (UTC), Operacja formatowania nie modyfikuje wartości <xref:System.DateTime> formatowanego obiektu. W związku z tym należy przekonwertować <xref:System.DateTime> wartość na czas UTC, wywołując <xref:System.DateTime.ToUniversalTime%2A?displayProperty=nameWithType> metodę przed wykonaniem operacji formatowania. W przeciwieństwie do <xref:System.DateTimeOffset> wartości powoduje automatyczne przeprowadzenie konwersji. nie ma potrzeby wywoływania <xref:System.DateTimeOffset.ToUniversalTime%2A?displayProperty=nameWithType> metody przed operacją formatowania.

W poniższym przykładzie pokazano użycie specyfikatora formatu "r" w celu wyświetlenia <xref:System.DateTime> i <xref:System.DateTimeOffset> wartości w systemie w strefie czasowej pacyficznego w Stanach Zjednoczonych.

[!code-csharp-interactive[Formatting.DateAndTime.Standard#9](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#9)]
[!code-vb[Formatting.DateAndTime.Standard#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#9)]

[Wróć do tabeli](#table)

<a name="Sortable"></a>

### <a name="the-sortable-s-format-specifier"></a>Specyfikator formatu sortowania ("s")

Specyfikator formatu standardowego "s" reprezentuje ciąg niestandardowego formatu daty i godziny zdefiniowany przez <xref:System.Globalization.DateTimeFormatInfo.SortableDateTimePattern%2A?displayProperty=nameWithType> Właściwość. Wzorzec odzwierciedla zdefiniowany standard (ISO 8601), a właściwość jest tylko do odczytu. Dlatego też zawsze jest taki sam, niezależnie od używanej kultury oraz dostarczonego dostawcy formatów. Ciąg formatu niestandardowego to „yyyy'-'MM'-'dd'T'HH':'mm':'ss”.

Specyfikator formatu "s" polega na wykorzystaniu ciągów wynikowych, które są sortowane w kolejności rosnącej lub malejącej na podstawie wartości daty i godziny. W związku z tym, mimo że specyfikator formatu standardowego "s" reprezentuje wartość daty i godziny w spójnym formacie, Operacja formatowania nie modyfikuje wartości obiektu daty i godziny, który jest formatowany w celu odzwierciedlenia jego <xref:System.DateTime.Kind%2A?displayProperty=nameWithType> właściwości lub jego <xref:System.DateTimeOffset.Offset%2A?displayProperty=nameWithType> wartości. Na przykład ciągi wynikowe tworzone przez formatowanie wartości daty i godziny 2014-11-15T18:32:17 + 00:00 i 2014-11-15T18:32:17 + 08:00 są identyczne.

Gdy jest używany ten specyfikator formatu standardowego, w operacji formatowania lub analizowania zawsze jest używana niezmienna kultura.

W poniższym przykładzie pokazano użycie specyfikatora formatu "s", aby wyświetlić <xref:System.DateTime> i <xref:System.DateTimeOffset> wartość w systemie w strefie czasowej pacyficznego w Stanach Zjednoczonych.

[!code-csharp-interactive[Formatting.DateAndTime.Standard#10](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#10)]
[!code-vb[Formatting.DateAndTime.Standard#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#10)]

[Wróć do tabeli](#table)

<a name="UniversalSortable"></a>

### <a name="the-universal-sortable-u-format-specifier"></a>Specyfikator formatu uniwersalnego sortowania ("u")

Specyfikator formatu standardowego "u" reprezentuje ciąg niestandardowego formatu daty i godziny zdefiniowany przez <xref:System.Globalization.DateTimeFormatInfo.UniversalSortableDateTimePattern%2A?displayProperty=nameWithType> Właściwość. Wzorzec odzwierciedla zdefiniowany standard, a właściwość jest tylko do odczytu. Dlatego też zawsze jest taki sam, niezależnie od używanej kultury oraz dostarczonego dostawcy formatów. Ciąg formatu niestandardowego to „yyyy'-'MM'-'dd HH':'mm':'ss'Z'”. Gdy jest używany ten specyfikator formatu standardowego, w operacji formatowania lub analizowania zawsze jest używana niezmienna kultura.

Chociaż ciąg wynikowy powinien wyrażać czas jako uniwersalny czas koordynowany (UTC), konwersja pierwotnej <xref:System.DateTime> wartości nie jest wykonywana podczas operacji formatowania. W związku z tym należy przekonwertować <xref:System.DateTime> wartość na czas UTC, wywołując <xref:System.DateTime.ToUniversalTime%2A?displayProperty=nameWithType> metodę przed jej formatowaniem.  W przeciwieństwie do <xref:System.DateTimeOffset> wartości powoduje automatyczne przeprowadzenie konwersji. nie ma potrzeby wywoływania <xref:System.DateTimeOffset.ToUniversalTime%2A?displayProperty=nameWithType> metody przed operacją formatowania.

W poniższym przykładzie użyto specyfikatora formatu „u”, aby wyświetlić wartość daty i godziny.

[!code-csharp-interactive[Formatting.DateAndTime.Standard#13](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#13)]
[!code-vb[Formatting.DateAndTime.Standard#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#13)]

[Wróć do tabeli](#table)

<a name="UniversalFull"></a>

### <a name="the-universal-full-u-format-specifier"></a>Specyfikator formatu uniwersalnej pełnej ("U")

Specyfikator formatu standardowego "U" reprezentuje ciąg niestandardowego formatu daty i godziny, który jest definiowany przez określoną <xref:System.Globalization.DateTimeFormatInfo.FullDateTimePattern%2A?displayProperty=nameWithType> Właściwość kultury. Wzorzec jest taki sam, jak wzorzec specyfikatora „F”. Jednak <xref:System.DateTime> wartość jest automatycznie konwertowana na czas UTC przed sformatowaniem.

Poniższa tabela zawiera listę <xref:System.Globalization.DateTimeFormatInfo> właściwości obiektu, które mogą kontrolować formatowanie zwracanego ciągu. Specyfikator formatu niestandardowego zwracany przez <xref:System.Globalization.DateTimeFormatInfo.FullDateTimePattern%2A> Właściwość niektórych kultur może nie używać wszystkich właściwości.

|Właściwość|Opis|
|--------------|-----------------|
|<xref:System.Globalization.DateTimeFormatInfo.FullDateTimePattern%2A>|Definiuje ogólny format ciągu wynikowego.|
|<xref:System.Globalization.DateTimeFormatInfo.DayNames%2A>|Definiuje zlokalizowane nazwy dni, które mogą być wyświetlane w ciągu wynikowym.|
|<xref:System.Globalization.DateTimeFormatInfo.MonthNames%2A>|Definiuje zlokalizowane nazwy miesięcy, które mogą być wyświetlane w ciągu wynikowym.|
|<xref:System.Globalization.DateTimeFormatInfo.TimeSeparator%2A>|Definiuje ciąg, który rozdziela składniki godziny, minuty i sekundy w ciągu reprezentującym godzinę.|
|<xref:System.Globalization.DateTimeFormatInfo.AMDesignator%2A>|Określa ciąg, który wskazuje czas od północy do południa (z wyłączeniem południa), w formacie 12-godzinnym.|
|<xref:System.Globalization.DateTimeFormatInfo.PMDesignator%2A>|Określa ciąg, który wskazuje czas od południa do północy (z wyłączeniem północy), w formacie 12-godzinnym.|

Specyfikator formatu "U" nie jest obsługiwany przez <xref:System.DateTimeOffset> Typ i zgłasza, <xref:System.FormatException> Jeśli jest używany do formatowania <xref:System.DateTimeOffset> wartości.

W poniższym przykładzie użyto specyfikatora formatu „U”, aby wyświetlić wartość daty i godziny.

[!code-csharp[Formatting.DateAndTime.Standard#14](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#14)]
[!code-vb[Formatting.DateAndTime.Standard#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#14)]

[Wróć do tabeli](#table)

## <a name="time-formats"></a>Formaty czasu

Ta grupa zawiera następujące formaty:

- [Specyfikator formatu godziny krótkiej ("t")](#the-short-time-t-format-specifier)
- [Specyfikator formatu godziny długiej ("T")](#the-long-time-t-format-specifier)

<a name="ShortTime"></a>

### <a name="the-short-time-t-format-specifier"></a>Specyfikator formatu godziny krótkiej ("t")

Specyfikator formatu standardowego "t" reprezentuje ciąg niestandardowego formatu daty i godziny, który jest definiowany przez bieżącą <xref:System.Globalization.DateTimeFormatInfo.ShortTimePattern%2A?displayProperty=nameWithType> Właściwość. Na przykład ciąg formatu niestandardowego dla niezmiennej kultury to „HH:mm”.

Informacje o formatowaniu określonego obiektu mają wpływ na ciąg wynikowy <xref:System.Globalization.DateTimeFormatInfo> . Poniższa tabela zawiera listę <xref:System.Globalization.DateTimeFormatInfo> właściwości obiektu, które mogą kontrolować formatowanie zwracanego ciągu. Specyfikator formatu niestandardowego zwracany przez <xref:System.Globalization.DateTimeFormatInfo.ShortTimePattern%2A?displayProperty=nameWithType> Właściwość niektórych kultur może nie używać wszystkich właściwości.

|Właściwość|Opis|
|--------------|-----------------|
|<xref:System.Globalization.DateTimeFormatInfo.ShortTimePattern%2A>|Definiuje format składnika godziny w ciągu wynikowym.|
|<xref:System.Globalization.DateTimeFormatInfo.TimeSeparator%2A>|Definiuje ciąg, który rozdziela składniki godziny, minuty i sekundy w ciągu reprezentującym godzinę.|
|<xref:System.Globalization.DateTimeFormatInfo.AMDesignator%2A>|Określa ciąg, który wskazuje czas od północy do południa (z wyłączeniem południa), w formacie 12-godzinnym.|
|<xref:System.Globalization.DateTimeFormatInfo.PMDesignator%2A>|Określa ciąg, który wskazuje czas od południa do północy (z wyłączeniem północy), w formacie 12-godzinnym.|

W poniższym przykładzie użyto specyfikatora formatu „t”, aby wyświetlić wartość daty i godziny.

[!code-csharp[Formatting.DateAndTime.Standard#11](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#11)]
[!code-vb[Formatting.DateAndTime.Standard#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#11)]

[Wróć do tabeli](#table)

<a name="LongTime"></a>

### <a name="the-long-time-t-format-specifier"></a>Specyfikator formatu godziny długiej ("T")

Specyfikator formatu standardowego "T" reprezentuje ciąg niestandardowego formatu daty i godziny, który jest definiowany przez określoną <xref:System.Globalization.DateTimeFormatInfo.LongTimePattern%2A?displayProperty=nameWithType> Właściwość kultury. Na przykład ciąg formatu niestandardowego dla niezmiennej kultury to „HH:mm:ss”.

Poniższa tabela zawiera listę <xref:System.Globalization.DateTimeFormatInfo> właściwości obiektu, które mogą kontrolować formatowanie zwracanego ciągu. Specyfikator formatu niestandardowego zwracany przez <xref:System.Globalization.DateTimeFormatInfo.LongTimePattern%2A?displayProperty=nameWithType> Właściwość niektórych kultur może nie używać wszystkich właściwości.

|Właściwość|Opis|
|--------------|-----------------|
|<xref:System.Globalization.DateTimeFormatInfo.LongTimePattern%2A>|Definiuje format składnika godziny w ciągu wynikowym.|
|<xref:System.Globalization.DateTimeFormatInfo.TimeSeparator%2A>|Definiuje ciąg, który rozdziela składniki godziny, minuty i sekundy w ciągu reprezentującym godzinę.|
|<xref:System.Globalization.DateTimeFormatInfo.AMDesignator%2A>|Określa ciąg, który wskazuje czas od północy do południa (z wyłączeniem południa), w formacie 12-godzinnym.|
|<xref:System.Globalization.DateTimeFormatInfo.PMDesignator%2A>|Określa ciąg, który wskazuje czas od południa do północy (z wyłączeniem północy), w formacie 12-godzinnym.|

W poniższym przykładzie użyto specyfikatora formatu „T”, aby wyświetlić wartość daty i godziny.

[!code-csharp[Formatting.DateAndTime.Standard#12](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#12)]
[!code-vb[Formatting.DateAndTime.Standard#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#12)]

[Wróć do tabeli](#table)

## <a name="partial-date-formats"></a>Częściowe formaty dat

Ta grupa zawiera następujące formaty:

- [Specyfikator formatu miesiąca ("M", "m")](#the-month-m-m-format-specifier)
- [Specyfikator formatu roku miesiąca ("Y", "y")](#the-year-month-y-y-format-specifier)

<a name="MonthDay"></a>

### <a name="the-month-m-m-format-specifier"></a>Specyfikator formatu miesiąca ("M", "m")

Specyfikator formatu standardowego "M" lub "m" reprezentuje ciąg niestandardowego formatu daty i godziny, który jest zdefiniowany przez bieżącą <xref:System.Globalization.DateTimeFormatInfo.MonthDayPattern%2A?displayProperty=nameWithType> Właściwość. Na przykład ciąg formatu niestandardowego dla niezmiennej kultury to „MMMM dd”.

Poniższa tabela zawiera listę <xref:System.Globalization.DateTimeFormatInfo> właściwości obiektu, które sterują formatowaniem zwracanego ciągu.

|Właściwość|Opis|
|--------------|-----------------|
|<xref:System.Globalization.DateTimeFormatInfo.MonthDayPattern%2A>|Definiuje ogólny format ciągu wynikowego.|
|<xref:System.Globalization.DateTimeFormatInfo.MonthNames%2A>|Definiuje zlokalizowane nazwy miesięcy, które mogą być wyświetlane w ciągu wynikowym.|

W poniższym przykładzie użyto specyfikatora formatu „m”, aby wyświetlić wartość daty i godziny.

[!code-csharp[Formatting.DateAndTime.Standard#7](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#7)]
[!code-vb[Formatting.DateAndTime.Standard#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#7)]

[Wróć do tabeli](#table)

<a name="YearMonth"></a>

### <a name="the-year-month-y-y-format-specifier"></a>Specyfikator formatu roku miesiąca ("Y", "y")

Specyfikator formatu standardowego "Y" lub "y" reprezentuje ciąg niestandardowego formatu daty i godziny, który jest zdefiniowany przez <xref:System.Globalization.DateTimeFormatInfo.YearMonthPattern%2A?displayProperty=nameWithType> Właściwość określonej kultury. Na przykład ciąg formatu niestandardowego dla niezmiennej kultury to „yyyy MMMM”.

Poniższa tabela zawiera listę <xref:System.Globalization.DateTimeFormatInfo> właściwości obiektu, które sterują formatowaniem zwracanego ciągu.

|Właściwość|Opis|
|--------------|-----------------|
|<xref:System.Globalization.DateTimeFormatInfo.YearMonthPattern%2A>|Definiuje ogólny format ciągu wynikowego.|
|<xref:System.Globalization.DateTimeFormatInfo.MonthNames%2A>|Definiuje zlokalizowane nazwy miesięcy, które mogą być wyświetlane w ciągu wynikowym.|

W poniższym przykładzie użyto specyfikatora formatu „y”, aby wyświetlić wartość daty i godziny.

[!code-csharp[Formatting.DateAndTime.Standard#15](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#15)]
[!code-vb[Formatting.DateAndTime.Standard#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#15)]

[Wróć do tabeli](#table)

<a name="Notes"></a>

## <a name="control-panel-settings"></a>Ustawienia panelu sterowania

W systemie Windows ustawienia w pozycji **Opcje regionalne i językowe** w panelu sterowania wpływają na ciąg wynikowy generowany przez operację formatowania. Te ustawienia są używane do inicjowania <xref:System.Globalization.DateTimeFormatInfo> obiektu skojarzonego z bieżącą kulturą wątku, która zapewnia wartości używane do zarządzania formatowaniem. Na komputerach, na których są używane różne ustawienia, są generowane różne ciągi wynikowe.

Ponadto, jeśli używasz <xref:System.Globalization.CultureInfo.%23ctor%28System.String%29> konstruktora do utworzenia wystąpienia nowego <xref:System.Globalization.CultureInfo> obiektu, który reprezentuje tę samą kulturę co bieżąca kultura systemu, wszelkie dostosowania ustanowione przez element **Opcje regionalne i językowe** w panelu sterowania zostaną zastosowane do nowego <xref:System.Globalization.CultureInfo> obiektu. Można użyć konstruktora, <xref:System.Globalization.CultureInfo.%23ctor%28System.String%2CSystem.Boolean%29> Aby utworzyć <xref:System.Globalization.CultureInfo> obiekt, który nie odzwierciedla dostosowań systemu.

## <a name="datetimeformatinfo-properties"></a>Właściwości DateTimeFormatInfo

Na formatowanie mają wpływ właściwości bieżącego <xref:System.Globalization.DateTimeFormatInfo> obiektu, które są dostarczane niejawnie przez bieżącą kulturę wątku lub jawnie przez <xref:System.IFormatProvider> parametr metody, która wywołuje formatowanie. Dla <xref:System.IFormatProvider> parametru, aplikacja powinna określać <xref:System.Globalization.CultureInfo> obiekt, który reprezentuje kulturę, lub <xref:System.Globalization.DateTimeFormatInfo> obiekt, który reprezentuje konwencje formatowania daty i godziny określonej kultury. Wiele specyfikatorów standardowego formatu daty i godziny to aliasy dla wzorców formatowania zdefiniowanych przez właściwości bieżącego <xref:System.Globalization.DateTimeFormatInfo> obiektu. Aplikacja może zmienić wynik wygenerowany przez niektóre standardowe specyfikatory formatu daty i godziny, zmieniając odpowiednie wzorce formatu daty i godziny odpowiedniej <xref:System.Globalization.DateTimeFormatInfo> właściwości.

## <a name="see-also"></a>Zobacz też

- <xref:System.DateTime?displayProperty=nameWithType>
- <xref:System.DateTimeOffset?displayProperty=nameWithType>
- [Formatowanie typów](formatting-types.md)
- [Niestandardowe ciągi formatujące datę i godzinę](custom-date-and-time-format-strings.md)
- [Przykład: Narzędzie formatowania programu .NET Core WinForms (C#)](/samples/dotnet/samples/windowsforms-formatting-utility-cs)
- [Przykład: Narzędzie formatowania programu .NET Core WinForms (Visual Basic)](/samples/dotnet/samples/windowsforms-formatting-utility-vb)
