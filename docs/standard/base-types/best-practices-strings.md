---
title: Najlepsze rozwiązania dotyczące porównywania ciągów w programie .NET
description: Dowiedz się, jak skutecznie porównywać ciągi w aplikacjach .NET.
ms.date: 05/01/2019
dev_langs:
- csharp
- vb
helpviewer_keywords:
- strings [.NET],searching
- best practices,string comparison and sorting
- strings [.NET],best practices
- strings [.NET],basic string operations
- sorting strings
- strings [.NET],sorting
- string comparison [.NET],best practices
- string sorting
- comparing strings
- strings [.NET],comparing
ms.assetid: b9f0bf53-e2de-4116-8ce9-d4f91a1df4f7
ms.openlocfilehash: bf11edc3669916ba4d30a3648692ca9b084d4340
ms.sourcegitcommit: 81f1bba2c97a67b5ca76bcc57b37333ffca60c7b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/10/2020
ms.locfileid: "97009822"
---
# <a name="best-practices-for-comparing-strings-in-net"></a>Najlepsze rozwiązania dotyczące porównywania ciągów w programie .NET

Platforma .NET zapewnia rozbudowaną obsługę tworzenia zlokalizowanych i globalnych aplikacji oraz ułatwia stosowanie Konwencji dla bieżącej kultury lub określonej kultury podczas wykonywania typowych operacji, takich jak sortowanie i wyświetlanie ciągów. Jednak sortowanie lub Porównywanie ciągów nie zawsze jest operacją zależną od kultury. Na przykład ciągi, które są używane wewnętrznie przez aplikację zwykle, powinny być obsługiwane identycznie we wszystkich kulturach. Gdy niezależne od kultury dane ciągów, takie jak tagi XML, Tagi HTML, nazwy użytkowników, ścieżki plików i nazwy obiektów systemowych, są interpretowane tak, jakby były wrażliwe na kulturę, kod aplikacji może podlegać rozdrobnym usterkom, złej wydajności i, w niektórych przypadkach, problemom z zabezpieczeniami.

Ten artykuł analizuje metody sortowania, porównywania i wielkości liter w programie .NET, przedstawia zalecenia dotyczące wybierania odpowiedniej metody obsługi ciągów i zawiera dodatkowe informacje na temat metod obsługi ciągów.

## <a name="recommendations-for-string-usage"></a>Zalecenia dotyczące użycia ciągów

Podczas programowania przy użyciu platformy .NET należy przestrzegać następujących prostych zaleceń podczas porównywania ciągów:

- Używaj przeciążeń, które jawnie określają reguły porównywania ciągów dla operacji na ciągach. Zwykle wymaga to wywołania przeciążenia metody z parametrem typu <xref:System.StringComparison> .
- Użyj <xref:System.StringComparison.Ordinal?displayProperty=nameWithType> lub <xref:System.StringComparison.OrdinalIgnoreCase?displayProperty=nameWithType> do porównań jako bezpiecznie domyślnego dla dopasowania ciągu niezależny od kultury.
- Używaj porównań z <xref:System.StringComparison.Ordinal?displayProperty=nameWithType> lub <xref:System.StringComparison.OrdinalIgnoreCase?displayProperty=nameWithType> w celu uzyskania lepszej wydajności.
- Użyj operacji na ciągach, które są oparte na <xref:System.StringComparison.CurrentCulture?displayProperty=nameWithType> momencie wyświetlania danych wyjściowych dla użytkownika.
- Używaj niejęzykowych <xref:System.StringComparison.Ordinal?displayProperty=nameWithType> lub <xref:System.StringComparison.OrdinalIgnoreCase?displayProperty=nameWithType> wartościowych zamiast operacji na ciągach w zależności od <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType> tego, kiedy porównanie jest istotne dla języka (na przykład).
- Użyj <xref:System.String.ToUpperInvariant%2A?displayProperty=nameWithType> metody zamiast <xref:System.String.ToLowerInvariant%2A?displayProperty=nameWithType> metody podczas normalizacji ciągów do porównania.
- Użyj przeciążenia <xref:System.String.Equals%2A?displayProperty=nameWithType> metody, aby sprawdzić, czy dwa ciągi są równe.
- Użyj <xref:System.String.Compare%2A?displayProperty=nameWithType> metod i <xref:System.String.CompareTo%2A?displayProperty=nameWithType> , aby sortować ciągi, a nie sprawdzaj równości.
- Użyj formatowania z uwzględnieniem kultury, aby wyświetlić dane niebędące ciągami, takie jak liczby i daty, w interfejsie użytkownika. Używaj formatowania z [kulturą niezmienną](xref:System.Globalization.CultureInfo.InvariantCulture) , aby utrwalać dane niebędące ciągami w postaci ciągów.

Podczas porównywania ciągów należy unikać następujących praktyk:

- Nie należy używać przeciążeń, które nie jawnie lub niejawnie określają reguły porównywania ciągów dla operacji na ciągach.
- Nie używaj w większości przypadków operacji na ciągach <xref:System.StringComparison.InvariantCulture?displayProperty=nameWithType> . Jednym z kilku wyjątków jest to, że w przypadku utrwalania w sposób istotny, ale kulturalnie niezależny od dane.
- Nie należy używać przeciążenia <xref:System.String.Compare%2A?displayProperty=nameWithType> <xref:System.String.CompareTo%2A> metody lub i testu dla zwracanej wartości zero, aby określić, czy dwa ciągi są równe.

## <a name="specifying-string-comparisons-explicitly"></a>Jawne określanie porównywania ciągów

Większość metod manipulowania ciągami w .NET jest przeciążona. Zazwyczaj co najmniej jedno Przeciążenie przyjmuje ustawienia domyślne, natomiast inne nie akceptują żadnych ustawień domyślnych, a zamiast tego definiują precyzyjne metody porównywania ciągów lub manipulowania nimi. Większość metod, które nie bazują na wartościach domyślnych, zawiera parametr typu <xref:System.StringComparison> , który jest wyliczeniem, które jawnie określa reguły dla porównania ciągów przez kulturę i wielkość liter. W poniższej tabeli opisano <xref:System.StringComparison> elementy członkowskie wyliczenia.

|StringComparison element członkowski|Opis|
|-----------------------------|-----------------|
|<xref:System.StringComparison.CurrentCulture>|Wykonuje porównanie z rozróżnianiem wielkości liter przy użyciu bieżącej kultury.|
|<xref:System.StringComparison.CurrentCultureIgnoreCase>|Wykonuje porównanie bez uwzględniania wielkości liter przy użyciu bieżącej kultury.|
|<xref:System.StringComparison.InvariantCulture>|Wykonuje porównanie z rozróżnianiem wielkości liter przy użyciu niezmiennej kultury.|
|<xref:System.StringComparison.InvariantCultureIgnoreCase>|Wykonuje porównanie bez uwzględniania wielkości liter przy użyciu niezmiennej kultury.|
|<xref:System.StringComparison.Ordinal>|Wykonuje porównanie porządkowe.|
|<xref:System.StringComparison.OrdinalIgnoreCase>|Wykonuje porównanie porządkowe bez uwzględniania wielkości liter.|

Na przykład <xref:System.String.IndexOf%2A> Metoda, która zwraca indeks podciągu w <xref:System.String> obiekcie, który pasuje do znaku lub ciągu, ma dziewięć przeciążeń:

- <xref:System.String.IndexOf%28System.Char%29>, <xref:System.String.IndexOf%28System.Char%2CSystem.Int32%29> , i <xref:System.String.IndexOf%28System.Char%2CSystem.Int32%2CSystem.Int32%29> , która domyślnie wykonuje numer porządkowy (bez uwzględniania wielkości liter i kulturowo), wyszukiwanie znaku w ciągu.
- <xref:System.String.IndexOf%28System.String%29>, <xref:System.String.IndexOf%28System.String%2CSystem.Int32%29> , i <xref:System.String.IndexOf%28System.String%2CSystem.Int32%2CSystem.Int32%29> , które domyślnie wykonują wyszukiwanie podciągów z uwzględnieniem wielkości liter i z uwzględnieniem ustawień kulturowych w ciągu.
- <xref:System.String.IndexOf%28System.String%2CSystem.StringComparison%29>, <xref:System.String.IndexOf%28System.String%2CSystem.Int32%2CSystem.StringComparison%29> , i <xref:System.String.IndexOf%28System.String%2CSystem.Int32%2CSystem.Int32%2CSystem.StringComparison%29> , które zawierają parametr typu <xref:System.StringComparison> , który umożliwia określenie formy porównania.

Zalecamy wybranie przeciążenia, które nie używa wartości domyślnych, z następujących powodów:

- Niektóre przeciążenia z domyślnymi parametrami (te, które wyszukują <xref:System.Char> w wystąpieniu ciągu) wykonują porównanie porządkowe, natomiast inne (te, które wyszukują ciąg w wystąpieniu ciągu) są zależne od kultury. Trudno jest pamiętać, która metoda używa tej wartości domyślnej i łatwej do odróżnienia przeciążenia.
- Zamiar kodu, który opiera się na wartościach domyślnych dla wywołań metod, nie jest jasne. W poniższym przykładzie, który opiera się na wartościach domyślnych, trudno jest wiedzieć, czy deweloper rzeczywiście zamierzy numer porządkowy, czy też jest porównywany z dwoma ciągami, czy też różnica wielkości liter między `protocol` i "http" może spowodować zwrócenie testu równości `false` .

     [!code-csharp[Conceptual.Strings.BestPractices#1](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/explicitargs1.cs#1)]
     [!code-vb[Conceptual.Strings.BestPractices#1](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/explicitargs1.vb#1)]

Ogólnie rzecz biorąc zalecamy wywołanie metody, która nie polega na wartościach domyślnych, ponieważ sprawia, że zamiar kodu jest niejednoznaczny. Dzięki temu kod staje się bardziej czytelny i łatwiejszy w debugowaniu i obsłudze. Poniższy przykład dotyczy odpowiedzi na pytania dotyczące poprzedniego przykładu. Sprawia, że jest ono jasne, że jest używane porównanie porządkowe oraz że różnice w przypadku są ignorowane.

[!code-csharp[Conceptual.Strings.BestPractices#2](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/explicitargs1.cs#2)]
[!code-vb[Conceptual.Strings.BestPractices#2](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/explicitargs1.vb#2)]

## <a name="the-details-of-string-comparison"></a>Szczegóły porównania ciągów

Porównanie ciągów jest sercem wielu operacji związanych z ciągami, szczególnie sortowania i testowania pod kątem równości. Ciągi są sortowane w określonej kolejności: Jeśli "my" pojawia się przed "String" na posortowanej liście ciągów, "my" musi być porównane lub równe "String". Ponadto porównanie niejawnie definiuje równość. Operacja porównywania zwraca wartość zero dla ciągów, które uzna za równe. Dobrą interpretacją jest to, że żaden ciąg nie jest mniejszy od drugiego. Większość znaczących operacji obejmujących ciągi zawierają jedną lub obie te procedury: porównanie z innym ciągiem i wykonywanie dobrze zdefiniowanej operacji sortowania.

> [!NOTE]
> Można pobrać [tabele wagi sortowania](https://www.microsoft.com/download/details.aspx?id=10921), zestaw plików tekstowych, które zawierają informacje o wagach znaków używanych w operacjach sortowania i porównywania dla systemów operacyjnych Windows, a także [domyślną tabelę elementów sortowania Unicode](https://www.unicode.org/Public/UCA/latest/allkeys.txt), najnowszą wersję tabeli Sortuj wagi dla systemu Linux i macOS. Określona wersja tabeli posortowanych wag w systemie Linux i macOS zależy od wersji [międzynarodowych składników dla bibliotek Unicode](http://site.icu-project.org/) zainstalowanych w systemie. Aby uzyskać informacje na temat wersji ICU i wersji standardu Unicode, które implementują, zobacz [pobieranie ICU](http://site.icu-project.org/download).

Jednak Ocena dwóch ciągów dla równości lub kolejności sortowania nie daje pojedynczego prawidłowego wyniku; wyniki są zależne od kryteriów używanych do porównywania ciągów. W szczególności porównania ciągów, które są numerami porządkowymi lub które są oparte na konwencjach wielkości liter i sortowania bieżącej kultury lub [niezmiennej kultury](xref:System.Globalization.CultureInfo.InvariantCulture) (niezależny od kultury opartej na języku angielskim) mogą generować różne wyniki.

Ponadto porównania ciągów przy użyciu różnych wersji programu .NET lub programu .NET w różnych systemach operacyjnych lub wersjach systemu operacyjnego mogą zwracać różne wyniki. Aby uzyskać więcej informacji, zobacz [ciągi i standard Unicode](xref:System.String#Unicode).

### <a name="string-comparisons-that-use-the-current-culture"></a>Porównania ciągów, które używają bieżącej kultury

Jedno kryterium obejmuje stosowanie Konwencji bieżącej kultury podczas porównywania ciągów. Porównania, które są oparte na bieżącej kulturze, wykorzystują bieżącą kulturę lub ustawienia regionalne wątku. Jeśli kultura nie jest ustawiona przez użytkownika, domyślnie jest to ustawienie w oknie **Opcje regionalne** w panelu sterowania. Należy zawsze używać porównań, które są oparte na bieżącej kulturze, gdy dane są istotne dla kultury, a kiedy odzwierciedlają interakcję z użytkownikiem uwzględniającą kulturę.

Jednak porównanie i wielkość liter w programie .NET zmieniają się po zmianie kultury. Dzieje się tak, gdy aplikacja jest wykonywana na komputerze z inną kulturą niż komputer, na którym aplikacja została opracowana, lub gdy wątek wykonawczy zmienia jego kulturę. To zachowanie jest zamierzone, ale pozostaje nieoczywista dla wielu deweloperów. Poniższy przykład ilustruje różnice w kolejności sortowania między kulturą w Stanach Zjednoczonych ("en-US") i szwedzkim ("SV-SE"). Zwróć uwagę, że słowa "Ångström", "Windows" i "Visual Studio" pojawiają się w różnych pozycjach w posortowanych tablicach ciągów.

[!code-csharp[Conceptual.Strings.BestPractices#3](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/comparison1.cs#3)]
[!code-vb[Conceptual.Strings.BestPractices#3](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/comparison1.vb#3)]

Porównania bez uwzględniania wielkości liter, które używają bieżącej kultury, są takie same jak porównania uwzględniające kulturę, z tą różnicą, że ignorowanie wielkości liter jako podyktowanych przez bieżącą kulturę wątku. Takie zachowanie może być również w porządku sortowania.

Porównania, które używają bieżącej semantyki kultury, są domyślne dla następujących metod:

- <xref:System.String.Compare%2A?displayProperty=nameWithType> przeciążenia, które nie zawierają <xref:System.StringComparison> parametru.
- <xref:System.String.CompareTo%2A?displayProperty=nameWithType> przeciążenia.
- Metoda Domyślna <xref:System.String.StartsWith%28System.String%29?displayProperty=nameWithType> oraz <xref:System.String.StartsWith%28System.String%2CSystem.Boolean%2CSystem.Globalization.CultureInfo%29?displayProperty=nameWithType> Metoda z `null` <xref:System.Globalization.CultureInfo> parametrem.
- Metoda Domyślna <xref:System.String.EndsWith%28System.String%29?displayProperty=nameWithType> oraz <xref:System.String.EndsWith%28System.String%2CSystem.Boolean%2CSystem.Globalization.CultureInfo%29?displayProperty=nameWithType> Metoda z `null` <xref:System.Globalization.CultureInfo> parametrem.
- <xref:System.String.IndexOf%2A?displayProperty=nameWithType> przeciążenia, które akceptują <xref:System.String> jako parametr wyszukiwania i nie mają <xref:System.StringComparison> parametru.
- <xref:System.String.LastIndexOf%2A?displayProperty=nameWithType> przeciążenia, które akceptują <xref:System.String> jako parametr wyszukiwania i nie mają <xref:System.StringComparison> parametru.

W każdym przypadku zalecamy wywołanie przeciążenia, które ma <xref:System.StringComparison> parametr, aby przeznaczenie metody zostało wyczyszczone.

Subtelne i nietak rozdrobne usterki mogą naciągać się, gdy dane nielingwistyczne nie są interpretowane językowo lub gdy dane ciągów z określonej kultury są interpretowane przy użyciu konwencji innej kultury. Przykładem kanonicznym jest problem z tureckim I.

W przypadku niemal wszystkich alfabetów łacińskich, w tym w języku angielskim (Stany Zjednoczone), znak "i" (\u0069) to mała wersja znaku "I" (\u0049). Ta reguła wielkości liter jest szybko zmieniana na wartość domyślną dla programowania osób w takiej kulturze. Alfabet turecki ("TR-TR") zawiera jednak znak "i" (\u0130), czyli "i" w Wielkiej wersji "i". Turecki zawiera również małe litery "i bez kropki", "ı" (\u0131), które zaczynają się od litery "I". To zachowanie występuje również w kulturze azerski ("AZ").

W związku z tym, założenia dotyczące Wielkiej litery "i" lub "lowercasing" nie są prawidłowe we wszystkich kulturach. Jeśli użyjesz domyślnych przeciążeń dla procedur porównywania ciągów, będą one podlegać wariancji między kulturami. Jeśli dane, które mają być porównane, nie są językowe, użycie domyślnych przeciążeń może dawać niepożądane wyniki, ponieważ poniżej podjęto próbę wykonania porównania ciągów "File" i "FILE" bez uwzględniania wielkości liter.

[!code-csharp[Conceptual.Strings.BestPractices#11](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/turkish1.cs#11)]
[!code-vb[Conceptual.Strings.BestPractices#11](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/turkish1.vb#11)]

To porównanie może spowodować znaczne problemy, jeśli kultura jest przypadkowo używana w ustawieniach zabezpieczeń, jak w poniższym przykładzie. Wywołanie metody, takie jak `IsFileURI("file:")` zwraca `true` , jeśli bieżącą kulturą jest angielski (Stany Zjednoczone), ale `false` Jeśli bieżąca kultura to turecki. W takim przypadku, w systemach tureckich, ktoś może obejść środki bezpieczeństwa, które blokują dostęp do identyfikatorów URI bez uwzględniania wielkości liter zaczynających się od "FILE:".

[!code-csharp[Conceptual.Strings.BestPractices#12](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/turkish1.cs#12)]
[!code-vb[Conceptual.Strings.BestPractices#12](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/turkish1.vb#12)]

W tym przypadku, ponieważ "plik:" ma być interpretowany jako niezależny od języka, kod powinien być zapisany, jak pokazano w następującym przykładzie:

[!code-csharp[Conceptual.Strings.BestPractices#13](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/turkish1.cs#13)]
[!code-vb[Conceptual.Strings.BestPractices#13](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/turkish1.vb#13)]

### <a name="ordinal-string-operations"></a>Operacje na ciągach porządkowych

Określenie <xref:System.StringComparison.Ordinal?displayProperty=nameWithType> wartości lub <xref:System.StringComparison.OrdinalIgnoreCase?displayProperty=nameWithType> w wywołaniu metody oznacza, że jest to porównanie w języku innym niż język, w którym funkcje języków naturalnych są ignorowane. Metody, które są wywoływane z tymi <xref:System.StringComparison> wartościami, podejmuje decyzje dotyczące operacji na ciągach prostych w przypadku porównywania bajtów zamiast wielkości liter lub tabel równoważności, które są sparametryzowane przez kulturę. W większości przypadków takie podejście najlepiej pasuje do zamierzonej interpretacji ciągów podczas szybszego wykonywania kodu i bardziej niezawodnego.

Porównania porządkowe to porównania ciągów, w których każdy bajt każdego ciągu jest porównywany bez interpretacji językowej; na przykład "Windows" nie pasuje do "Windows". Jest to zasadniczo wywołanie funkcji środowiska uruchomieniowego języka C `strcmp` . Użyj tego porównania, gdy kontekst określa, że ciągi powinny być dokładnie dopasowane lub wymagające ostrożnej zgodności z zasadami. Ponadto, porównanie porządkowe jest najszybszą operacją porównywania, ponieważ nie stosuje żadnych reguł lingwistycznych podczas określania wyniku.

Ciągi w programie .NET mogą zawierać osadzone znaki o wartości null. Jedną z najwyraźniejszych różnic między porównaniem porządkowym i kulturowym (w tym porównaniami korzystającymi z niezmiennej kultury) jest obsługa osadzonych znaków null w ciągu. Te znaki są ignorowane w przypadku używania <xref:System.String.Compare%2A?displayProperty=nameWithType> metod i <xref:System.String.Equals%2A?displayProperty=nameWithType> do wykonywania porównań z uwzględnieniem kultury (w tym porównań, które używają niezmiennej kultury). W związku z tym w porównaniach wrażliwych na kulturę ciągi zawierające osadzone znaki null mogą być traktowane jako równe ciągom, które nie.

> [!IMPORTANT]
> Chociaż metody porównywania ciągów zignorują osadzone znaki null, metody wyszukiwania ciągów, takie jak,,, <xref:System.String.Contains%2A?displayProperty=nameWithType> <xref:System.String.EndsWith%2A?displayProperty=nameWithType> <xref:System.String.IndexOf%2A?displayProperty=nameWithType> <xref:System.String.LastIndexOf%2A?displayProperty=nameWithType> , i nie <xref:System.String.StartsWith%2A?displayProperty=nameWithType> .

Poniższy przykład wykonuje porównanie z uwzględnieniem kultury ciągu "AA" z podobnym ciągiem, który zawiera kilka osadzonych znaków o wartości null między "A" i "a" i pokazuje, jak dwa ciągi są uważane za równe:

[!code-csharp[Conceptual.Strings.BestPractices#19](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/embeddednulls1.cs#19)]
 [!code-vb[Conceptual.Strings.BestPractices#19](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/embeddednulls1.vb#19)]

Jednak ciągi nie są uważane za równe w przypadku używania porównania porządkowego, jak pokazano na poniższym przykładzie:

[!code-csharp[Conceptual.Strings.BestPractices#20](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/embeddednulls2.cs#20)]
[!code-vb[Conceptual.Strings.BestPractices#20](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/embeddednulls2.vb#20)]

Porównywanie porządkowe bez uwzględniania wielkości liter jest kolejnym najbardziej rygorystycznym podejściem. Te porównania ignorują większość wielkości liter; na przykład "Windows" dopasowuje "Windows". W przypadku znaków ASCII te zasady są równoważne z <xref:System.StringComparison.Ordinal?displayProperty=nameWithType> , z tą różnicą, że ignoruje zwykłe wielkości liter ASCII. W związku z tym każdy znak w [A, Z] (\u0041-\u005A) pasuje do odpowiadającego mu znaku w [a, z] (\u0061-\007A). Wielkość liter poza zakresem ASCII używa tabel niezmiennej kultury. W związku z tym następujące porównanie:

[!code-csharp[Conceptual.Strings.BestPractices#4](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/comparison2.cs#4)]
[!code-vb[Conceptual.Strings.BestPractices#4](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/comparison2.vb#4)]

jest odpowiednikiem (ale szybszym niż) tego porównania:

[!code-csharp[Conceptual.Strings.BestPractices#5](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/comparison2.cs#5)]
[!code-vb[Conceptual.Strings.BestPractices#5](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/comparison2.vb#5)]

Te porównania są nadal bardzo szybkie.

Zarówno <xref:System.StringComparison.Ordinal?displayProperty=nameWithType> , jak i <xref:System.StringComparison.OrdinalIgnoreCase?displayProperty=nameWithType> używają wartości binarnych, są one najlepiej dopasowane do dopasowywania. Gdy nie masz pewności co do ustawień porównania, użyj jednej z tych dwóch wartości. Jednak ze względu na to, że wykonują porównywanie bajt po bajcie, nie sortuje według języka porządku sortowania (na przykład słownika angielskiego), ale według binarnej kolejności sortowania. Wyniki mogą wyglądać nieparzystie w większości kontekstów, jeśli są wyświetlane użytkownikom.

Semantyka porządkowa jest wartością domyślną dla <xref:System.String.Equals%2A?displayProperty=nameWithType> przeciążeń, które nie zawierają <xref:System.StringComparison> argumentu (łącznie z operatorem równości). W każdym przypadku zalecamy wywołanie przeciążenia z <xref:System.StringComparison> parametrem.

### <a name="string-operations-that-use-the-invariant-culture"></a>Operacje na ciągach, które używają niezmiennej kultury

Porównania z kulturą niezmienną używają <xref:System.Globalization.CultureInfo.CompareInfo%2A> Właściwości zwróconej przez właściwość statyczną <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType> . Takie zachowanie jest takie samo w przypadku wszystkich systemów; tłumaczy wszelkie znaki spoza zakresu na to, co jest uważane za równoważne znaki niezmienne. Te zasady mogą być przydatne do obsługi jednego zestawu zachowań ciągów między kulturami, ale często zapewniają nieoczekiwane wyniki.

Porównania bez uwzględniania wielkości liter z kulturą niezmienną należy używać <xref:System.Globalization.CultureInfo.CompareInfo%2A> właściwości statycznej zwróconej przez właściwość statyczną <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType> dla informacji porównawczych. Wszelkie różnice wielkości liter między tymi przetłumaczonymi znakami są ignorowane.

Porównania, które używają <xref:System.StringComparison.InvariantCulture?displayProperty=nameWithType> i <xref:System.StringComparison.Ordinal?displayProperty=nameWithType> działają identycznie na ciągach ASCII. Jednak program <xref:System.StringComparison.InvariantCulture?displayProperty=nameWithType> podejmuje decyzje językowe, które mogą nie być odpowiednie dla ciągów, które muszą być interpretowane jako zestaw bajtów. `CultureInfo.InvariantCulture.CompareInfo`Obiekt sprawia, że <xref:System.String.Compare%2A> Metoda interpretuje niektóre zestawy znaków jako równoważne. Na przykład następująca równoważność jest prawidłowa dla niezmiennej kultury:

InvariantCulture: a + ̊ = a

Mała litera "a" (\u0061), gdy jest obok znaku ŁĄCZĄCego powyżej znak "+" ̊ "(\u030a), jest interpretowana jako mała litera A z PIERŚCIENIem powyżej znaku" a "(\u00e5). Jak pokazano na poniższym przykładzie, to zachowanie różni się od porównania liczb porządkowych.

[!code-csharp[Conceptual.Strings.BestPractices#15](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/comparison3.cs#15)]
[!code-vb[Conceptual.Strings.BestPractices#15](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/comparison3.vb#15)]

W przypadku interpretacji nazw plików, plików cookie lub innych elementów, w których może się pojawić kombinacja, taka jak "a", porównania porządkowe nadal zapewniają najbardziej przejrzyste i niedopasowane zachowanie.

W przypadku niezmiennej kultura ma bardzo kilka właściwości, które ułatwiają porównywanie. Jest to porównywane w sposób istotny, który uniemożliwia mu zagwarantowanie pełnego równoważności symbolicznej, ale nie jest to możliwe do wyświetlania w żadnej kulturze. Jedną z kilku powodów użycia <xref:System.StringComparison.InvariantCulture?displayProperty=nameWithType> do porównania jest utrwalanie uporządkowanych danych dla różnych kulturowo identycznych ekranów. Na przykład jeśli plik danych o dużym rozmiarze zawierający listę posortowanych identyfikatorów dla wyświetlania towarzyszy aplikacji, dodanie do tej listy będzie wymagało wstawienia z sortowaniem w stylu niezmiennym.

## <a name="choosing-a-stringcomparison-member-for-your-method-call"></a>Wybieranie elementu członkowskiego StringComparison dla wywołania metody

Poniższa tabela zawiera opis mapowania z kontekstu ciągu semantycznego do <xref:System.StringComparison> elementu członkowskiego wyliczenia:

|Dane|Zachowanie|Odpowiadający system. StringComparison<br /><br /> wartość|
|----------|--------------|-----------------------------------------------------|
|Identyfikatory wewnętrzne z uwzględnieniem wielkości liter.<br /><br /> Identyfikatory z uwzględnieniem wielkości liter w standardach, takich jak XML i HTTP.<br /><br /> Ustawienia związane z zabezpieczeniami z uwzględnieniem wielkości liter.|Identyfikator niebędący językiem, gdzie bajty są dokładnie zgodne.|<xref:System.StringComparison.Ordinal>|
|Identyfikatory wewnętrzne bez uwzględniania wielkości liter.<br /><br /> Identyfikatory bez uwzględniania wielkości liter w standardach, takich jak XML i HTTP.<br /><br /> Ścieżki plików.<br /><br /> Klucze i wartości rejestru.<br /><br /> Zmienne środowiskowe.<br /><br /> Identyfikatory zasobów (na przykład nazwy uchwytów).<br /><br /> Ustawienia związane z zabezpieczeniami bez uwzględniania wielkości liter.|Identyfikator niebędący językiem, gdzie przypadek jest nieistotny; szczególnie dane przechowywane w większości usług systemu Windows.|<xref:System.StringComparison.OrdinalIgnoreCase>|
|Pewne utrwalone, językowe dane.<br /><br /> Wyświetlanie danych lingwistycznych, które wymagają stałego porządku sortowania.|Kulturowo niezależny od dane, które nadal są istotne dla języka.|<xref:System.StringComparison.InvariantCulture><br /><br /> -lub-<br /><br /> <xref:System.StringComparison.InvariantCultureIgnoreCase>|
|Dane wyświetlane użytkownikowi.<br /><br /> Większość danych wejściowych użytkownika.|Dane wymagające lokalnego języka.|<xref:System.StringComparison.CurrentCulture><br /><br /> -lub-<br /><br /> <xref:System.StringComparison.CurrentCultureIgnoreCase>|

## <a name="common-string-comparison-methods-in-net"></a>Typowe metody porównywania ciągów w programie .NET

W poniższych sekcjach opisano metody, które są najczęściej używane do porównywania ciągów.

### <a name="stringcompare"></a>Funkcja String.Compare

Domyślna interpretacja: <xref:System.StringComparison.CurrentCulture?displayProperty=nameWithType> .

Jako że operacja najważniejsza do interpretacji ciągów, wszystkie wystąpienia tych wywołań metod powinny być badane w celu określenia, czy ciągi powinny być interpretowane zgodnie z bieżącą kulturą, czy też odwoływać się od kultury (symbolicznie). Zwykle jest to ostatni i <xref:System.StringComparison.Ordinal?displayProperty=nameWithType> zamiast tego należy użyć porównania.

<xref:System.Globalization.CompareInfo?displayProperty=nameWithType>Klasa, która jest zwracana przez <xref:System.Globalization.CultureInfo.CompareInfo%2A?displayProperty=nameWithType> Właściwość, również zawiera <xref:System.Globalization.CompareInfo.Compare%2A> metodę, która dostarcza wiele pasujących opcji (numer porządkowy, ignorowanie białego znaku, ignorowanie typu kana itd.) za pomocą <xref:System.Globalization.CompareOptions> wyliczenia flag.

### <a name="stringcompareto"></a>Funkcja String.CompareTo

Domyślna interpretacja: <xref:System.StringComparison.CurrentCulture?displayProperty=nameWithType> .

Ta metoda obecnie nie oferuje przeciążenia, które określa <xref:System.StringComparison> Typ. Zwykle jest możliwe przekonwertowanie tej metody na zalecaną <xref:System.String.Compare%28System.String%2CSystem.String%2CSystem.StringComparison%29?displayProperty=nameWithType> formę.

Typy, które implementują <xref:System.IComparable> <xref:System.IComparable%601> interfejsy i implementują tę metodę. Ponieważ nie oferuje opcji <xref:System.StringComparison> parametru, implementacja typów często zezwala użytkownikowi na określenie <xref:System.StringComparer> w konstruktorze. W poniższym przykładzie zdefiniowano `FileName` klasę, której Konstruktor klasy zawiera <xref:System.StringComparer> parametr. Ten <xref:System.StringComparer> obiekt jest następnie używany w `FileName.CompareTo` metodzie.

[!code-csharp[Conceptual.Strings.BestPractices#6](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/api1.cs#6)]
[!code-vb[Conceptual.Strings.BestPractices#6](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/api1.vb#6)]

### <a name="stringequals"></a>Funkcja String.Equals

Domyślna interpretacja: <xref:System.StringComparison.Ordinal?displayProperty=nameWithType> .

<xref:System.String>Klasa umożliwia przetestowanie pod kątem równości przez wywołanie metody statycznej lub <xref:System.String.Equals%2A> przeciążenia lub użycie statycznego operatora równości. Przeciążenia i operator domyślnie używają porównania porządkowego. Mimo to nadal zalecamy wywołanie przeciążenia, które jawnie określa <xref:System.StringComparison> Typ nawet w przypadku, gdy chcesz wykonać porównanie porządkowe; ułatwia to wyszukiwanie w kodzie dla określonej interpretacji ciągów.

### <a name="stringtoupper-and-stringtolower"></a>String.ToUpper i String.ToLower

Domyślna interpretacja: <xref:System.StringComparison.CurrentCulture?displayProperty=nameWithType> .

Należy zachować ostrożność w przypadku korzystania z tych metod, ponieważ wymuszanie ciągu do wielkich lub małych liter jest często używane jako mała normalizacja do porównywania ciągów, niezależnie od wielkości liter. Jeśli tak, rozważ użycie porównania bez uwzględniania wielkości liter.

<xref:System.String.ToUpperInvariant%2A?displayProperty=nameWithType> <xref:System.String.ToLowerInvariant%2A?displayProperty=nameWithType> Dostępne są również metody i. <xref:System.String.ToUpperInvariant%2A> jest standardowym sposobem normalizacji wielkości liter. Porównania wykonywane przy użyciu <xref:System.StringComparison.OrdinalIgnoreCase?displayProperty=nameWithType> są zachowaniem składu dwóch wywołań: wywoływanie <xref:System.String.ToUpperInvariant%2A> dla obu argumentów ciągów i wykonywanie porównania przy użyciu <xref:System.StringComparison.Ordinal?displayProperty=nameWithType> .

Przeciążenia są również dostępne do przekonwertowania na wielkie i małe litery w określonej kulturze, przekazując <xref:System.Globalization.CultureInfo> obiekt, który reprezentuje tę kulturę do metody.

### <a name="chartoupper-and-chartolower"></a>Char.ToUpper i Char.ToLower

Domyślna interpretacja: <xref:System.StringComparison.CurrentCulture?displayProperty=nameWithType> .

Metody te działają podobnie jak <xref:System.String.ToUpper%2A?displayProperty=nameWithType> metody i <xref:System.String.ToLower%2A?displayProperty=nameWithType> opisane w poprzedniej sekcji.

### <a name="stringstartswith-and-stringendswith"></a>String.StartsWith i String.EndsWith

Domyślna interpretacja: <xref:System.StringComparison.CurrentCulture?displayProperty=nameWithType> .

Domyślnie obie te metody wykonują porównanie z uwzględnieniem kultury.

### <a name="stringindexof-and-stringlastindexof"></a>String.IndexOf i String.LastIndexOf

Domyślna interpretacja: <xref:System.StringComparison.CurrentCulture?displayProperty=nameWithType> .

Brak spójności w sposobie wykonywania porównań przez domyślne przeciążenia tych metod. Wszystkie <xref:System.String.IndexOf%2A?displayProperty=nameWithType> i <xref:System.String.LastIndexOf%2A?displayProperty=nameWithType> metody, które zawierają <xref:System.Char> parametr, wykonują porównanie porządkowe, ale domyślne <xref:System.String.IndexOf%2A?displayProperty=nameWithType> i <xref:System.String.LastIndexOf%2A?displayProperty=nameWithType> metody, które zawierają <xref:System.String> parametr, wykonują porównanie z uwzględnieniem kultury.

W przypadku wywołania <xref:System.String.IndexOf%28System.String%29?displayProperty=nameWithType> metody lub <xref:System.String.LastIndexOf%28System.String%29?displayProperty=nameWithType> i przekazania do niej ciągu w celu zlokalizowania w bieżącym wystąpieniu zalecamy wywołanie przeciążenia, które jawnie określa <xref:System.StringComparison> Typ. Przeciążenia, które zawierają <xref:System.Char> argument, nie pozwalają na określenie <xref:System.StringComparison> typu.

## <a name="methods-that-perform-string-comparison-indirectly"></a>Metody, które pośrednio wykonują Porównywanie ciągów

Niektóre metody niebędące ciągami, które mają porównanie ciągów jako operacji centralnej używają <xref:System.StringComparer> typu. <xref:System.StringComparer>Klasa zawiera sześć właściwości statycznych, które zwracają <xref:System.StringComparer> wystąpienia, których <xref:System.StringComparer.Compare%2A?displayProperty=nameWithType> metody wykonują następujące typy porównań ciągów:

- Porównania ciągów zależnych od kultury przy użyciu bieżącej kultury. Ten <xref:System.StringComparer> obiekt jest zwracany przez <xref:System.StringComparer.CurrentCulture%2A?displayProperty=nameWithType> Właściwość.
- Porównania bez uwzględniania wielkości liter przy użyciu bieżącej kultury. Ten <xref:System.StringComparer> obiekt jest zwracany przez <xref:System.StringComparer.CurrentCultureIgnoreCase%2A?displayProperty=nameWithType> Właściwość.
- Porównania niewrażliwe na kulturę przy użyciu reguł porównania wyrazów niezmiennej kultury. Ten <xref:System.StringComparer> obiekt jest zwracany przez <xref:System.StringComparer.InvariantCulture%2A?displayProperty=nameWithType> Właściwość.
- Porównania bez uwzględniania wielkości liter i nieuwzględniania kultur przy użyciu reguł porównania wyrazów niezmiennej kultury. Ten <xref:System.StringComparer> obiekt jest zwracany przez <xref:System.StringComparer.InvariantCultureIgnoreCase%2A?displayProperty=nameWithType> Właściwość.
- Porównanie porządkowe. Ten <xref:System.StringComparer> obiekt jest zwracany przez <xref:System.StringComparer.Ordinal%2A?displayProperty=nameWithType> Właściwość.
- Porównanie porządkowe bez uwzględniania wielkości liter. Ten <xref:System.StringComparer> obiekt jest zwracany przez <xref:System.StringComparer.OrdinalIgnoreCase%2A?displayProperty=nameWithType> Właściwość.

### <a name="arraysort-and-arraybinarysearch"></a>Array.Sort i Array.BinarySearch

Domyślna interpretacja: <xref:System.StringComparison.CurrentCulture?displayProperty=nameWithType> .

W przypadku przechowywania danych w kolekcji lub odczytywania utrwalonych danych z pliku lub bazy danych do kolekcji, przełączenie bieżącej kultury może spowodować unieważnienie niezmiennych w kolekcji. <xref:System.Array.BinarySearch%2A?displayProperty=nameWithType>Metoda zakłada, że elementy w tablicy, które mają być przeszukiwane, są już posortowane. Aby posortować dowolny element ciągu w tablicy, <xref:System.Array.Sort%2A?displayProperty=nameWithType> Metoda wywołuje <xref:System.String.Compare%2A?displayProperty=nameWithType> metodę w celu uporządkowania poszczególnych elementów. Użycie funkcji porównującej uwzględniającej kulturę może być niebezpieczne, jeśli kultura zmieni się między posortowaną tablicą a jego zawartością jest przeszukiwana. Na przykład, w poniższym kodzie, magazyn i pobieranie działają na porównującej, który jest dostarczany niejawnie przez `Thread.CurrentThread.CurrentCulture` Właściwość. Jeśli kultura może zmienić między wywołaniami do `StoreNames` i `DoesNameExist` , a zwłaszcza jeśli zawartość tablicy jest utrwalana między dwoma wywołaniami metod, wyszukiwanie binarne może zakończyć się niepowodzeniem.

[!code-csharp[Conceptual.Strings.BestPractices#7](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/indirect1.cs#7)]
 [!code-vb[Conceptual.Strings.BestPractices#7](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/indirect1.vb#7)]

W poniższym przykładzie zostanie wyświetlona zalecana odmiana, która używa tej samej wartości porządkowej (bez uwzględniania kultury) zarówno do sortowania, jak i do przeszukiwania tablicy. Kod zmiany jest widoczny w wierszach oznaczonych `Line A` i `Line B` w dwóch przykładach.

[!code-csharp[Conceptual.Strings.BestPractices#8](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/indirect1.cs#8)]
[!code-vb[Conceptual.Strings.BestPractices#8](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/indirect1.vb#8)]

Jeśli te dane są utrwalane i przenoszone między kulturami, a sortowanie służy do prezentowania tych danych użytkownikowi, można rozważyć użycie <xref:System.StringComparison.InvariantCulture?displayProperty=nameWithType> , który działa w sposób językowy dla lepszych danych wyjściowych użytkownika, ale nie ma wpływ na zmiany w kulturze. Poniższy przykład modyfikuje dwa poprzednie przykłady, aby użyć niezmiennej kultury do sortowania i przeszukiwania tablicy.

[!code-csharp[Conceptual.Strings.BestPractices#9](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/indirect1.cs#9)]
[!code-vb[Conceptual.Strings.BestPractices#9](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/indirect1.vb#9)]

### <a name="collections-example-hashtable-constructor"></a>Przykład kolekcji: Konstruktor Hashtable

Ciągi mieszania zawierają drugi przykład operacji, na które ma wpływ, w jaki sposób ciągi są porównywane.

Poniższy przykład tworzy wystąpienie <xref:System.Collections.Hashtable> obiektu przez przekazanie go do <xref:System.StringComparer> obiektu, który jest zwracany przez <xref:System.StringComparer.OrdinalIgnoreCase%2A?displayProperty=nameWithType> Właściwość. Ponieważ Klasa, <xref:System.StringComparer> która pochodzi od <xref:System.StringComparer> implementuje <xref:System.Collections.IEqualityComparer> interfejs, jego <xref:System.Collections.IEqualityComparer.GetHashCode%2A> Metoda jest używana do obliczania kodu skrótu ciągów w tabeli skrótów.

[!code-csharp[Conceptual.Strings.BestPractices#10](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/indirect2.cs#10)]
[!code-vb[Conceptual.Strings.BestPractices#10](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/indirect2.vb#10)]

## <a name="see-also"></a>Zobacz także

- [Globalizacja w aplikacjach .NET](../globalization-localization/globalization.md)
