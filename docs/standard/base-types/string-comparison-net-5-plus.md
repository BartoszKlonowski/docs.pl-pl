---
title: Zachowanie zmian w przypadku porównywania ciągów w programie .NET 5 +
description: Informacje o zmianach zachowania porównania ciągów w programie .NET 5 i nowszych wersjach w systemie Windows.
ms.date: 12/07/2020
ms.openlocfilehash: a53c36b31785fb43c0aa5f5040042abb6d40031a
ms.sourcegitcommit: 45c7148f2483db2501c1aa696ab6ed2ed8cb71b2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/08/2020
ms.locfileid: "96851754"
---
# <a name="behavior-changes-when-comparing-strings-on-net-5"></a>Zachowanie zmian w przypadku porównywania ciągów w programie .NET 5 +

W programie .NET 5,0 wprowadzono zmianę behawioralną środowiska uruchomieniowego, w której interfejsy API globalizacji [teraz domyślnie używają ICU](../../core/compatibility/globalization/5.0/icu-globalization-api.md) na wszystkich obsługiwanych platformach. Jest to wyjście z wcześniejszych wersji programu .NET Core i z .NET Framework, które korzystają z funkcji obsługi języka narodowego (NLS) systemu operacyjnego w przypadku uruchamiania w systemie Windows. Aby uzyskać więcej informacji na temat tych zmian, w tym przełączników zgodności, które mogą przywrócić zmianę zachowania, zobacz [globalizacja platformy .NET i ICU](../globalization-localization/globalization-icu.md).

## <a name="reason-for-change"></a>Przyczyna zmiany

Ta zmiana została wprowadzona w celu ujednolicenia. Zachowanie globalizacji sieci we wszystkich obsługiwanych systemach operacyjnych. Zapewnia również możliwość tworzenia przez aplikacje własnych bibliotek globalizacji, a nie zależą od wbudowanych bibliotek systemu operacyjnego. Aby uzyskać więcej informacji, zobacz [powiadomienie o zmianie](../../core/compatibility/globalization/5.0/icu-globalization-api.md).

## <a name="behavioral-differences"></a>Różnice w zachowaniu

Jeśli używasz funkcji, takich jak `string.IndexOf(string)` bez wywoływania przeciążenia, które przyjmuje <xref:System.StringComparison> argument, możesz zamierzyć wyszukiwanie *porządkowe* , ale zamiast tego przypadkowo wykonujesz zależność od zachowania specyficznego dla kultury. Ponieważ funkcje NLS i ICU implementują inną logikę w ich porównania językowe, wyniki metod takich jak `string.IndexOf(string)` mogą zwracać nieoczekiwane wartości.

Może to spowodować, że jest to możliwe nawet w miejscach, w których nie zawsze oczekuje się, że funkcje globalizacji są aktywne. Na przykład poniższy kod może utworzyć inną odpowiedź w zależności od bieżącego środowiska uruchomieniowego.

```cs
string s = "Hello\r\nworld!";
int idx = s.IndexOf("\n");
Console.WriteLine(idx);

// The snippet prints:
//
// '6' when running on .NET Framework (Windows)
// '6' when running on .NET Core 2.x - 3.x (Windows)
// '-1' when running on .NET 5 (Windows)
// '-1' when running on .NET Core 2.x - 3.x or .NET 5 (non-Windows)
// '6' when running on .NET Core 2.x or .NET 5 (in invariant mode)
```

## <a name="guard-against-unexpected-behavior"></a>Ochrona przed nieoczekiwanym zachowaniem

Ta sekcja zawiera dwie opcje dotyczące postępowania z nieoczekiwanymi zmianami zachowania w programie .NET 5,0.

### <a name="enable-code-analyzers"></a>Włącz analizatory kodu

[Analizatory kodu](../../fundamentals/code-analysis/overview.md) mogą wykrywać możliwe wywołania debugowania. Aby pomóc w ochronie przed wszelkimi zachowaniami zaskakujące, zalecamy włączenie analizatorów platformy .NET kompilators (Roslyn) w projekcie. Analizatory ułatwiają flagę kodu, który może przypadkowo używać funkcji porównującej język, gdy wartośćowa wartość porównująca była prawdopodobnie zamierzona. Następujące reguły powinny pomóc w oznaczeniu tych problemów:

- [CA1307: Określ parametr StringComparison w celu zapewnienia jednoznaczności](../../fundamentals/code-analysis/quality-rules/ca1307.md)
- [CA1309: Użyj porządkowego ustawienia właściwości StringComparison](../../fundamentals/code-analysis/quality-rules/ca1309.md)
- [CA1310: Określ parametr StringComparison w celu zapewnienia poprawności](../../fundamentals/code-analysis/quality-rules/ca1310.md)

Te określone reguły nie są domyślnie włączone. Aby je włączyć i pokazać wszystkie naruszenia jako błędy kompilacji, ustaw następujące właściwości w pliku projektu:

```xml
<PropertyGroup>
  <AnalysisMode>AllEnabledByDefault</AnalysisMode>
  <WarningsAsErrors>$(WarningsAsErrors);CA1307;CA1309;CA1310</WarningsAsErrors>
</PropertyGroup>
```

Poniższy fragment kodu przedstawia przykłady kodów, które tworzą odpowiednie ostrzeżenia analizatora kodu lub błędy.

```cs
//
// Potentially incorrect code - answer might vary based on locale.
//
string s = GetString();
// Produces analyzer warning CA1310 for string; CA1307 matches on char ','
int idx = s.IndexOf(",");
Console.WriteLine(idx);

//
// Corrected code - matches the literal substring ",".
//
string s = GetString();
int idx = s.IndexOf(",", StringComparison.Ordinal);
Console.WriteLine(idx);

//
// Corrected code (alternative) - searches for the literal ',' character.
//
string s = GetString();
int idx = s.IndexOf(',');
Console.WriteLine(idx);
```

Podobnie podczas tworzenia wystąpienia posortowanej kolekcji ciągów lub sortowania istniejącej kolekcji opartej na ciągach należy określić jawną funkcję porównującą.

```cs
//
// Potentially incorrect code - behavior might vary based on locale.
//
SortedSet<string> mySet = new SortedSet<string>();
List<string> list = GetListOfStrings();
list.Sort();

//
// Corrected code - uses ordinal sorting; doesn't vary by locale.
//
SortedSet<string> mySet = new SortedSet<string>(StringComparer.Ordinal);
List<string> list = GetListOfStrings();
list.Sort(StringComparer.Ordinal);
```

### <a name="revert-back-to-nls-behaviors"></a>Przywracanie zachowań NLS

Aby przywrócić aplikacje .NET 5 z powrotem do starszych zachowań funkcji NLS podczas działania w systemie Windows, wykonaj kroki opisane w temacie [globalizacja i ICU platformy .NET](../globalization-localization/globalization-icu.md). Ten przełącznik zgodności dla całej aplikacji musi być ustawiony na poziomie aplikacji. Poszczególne biblioteki nie mogą korzystać z tego zachowania ani go wycofać.

> [!TIP]
> Zdecydowanie zalecamy włączenie reguł analizy kodu [CA1307](../../fundamentals/code-analysis/quality-rules/ca1307.md), [CA1309](../../fundamentals/code-analysis/quality-rules/ca1309.md)i [CA1310](../../fundamentals/code-analysis/quality-rules/ca1310.md) , aby pomóc w ulepszaniu higieny kodu i wykryciu wszelkich istniejących błędów. Aby uzyskać więcej informacji, zobacz [Włączanie analizatorów kodu](#enable-code-analyzers).

## <a name="affected-apis"></a>Dotyczy interfejsów API

Większość aplikacji .NET nie napotka nieoczekiwanych zachowań spowodowanych zmianami w programie .NET 5,0. Jednak ze względu na liczbę uszkodzonych interfejsów API i podstaw tych interfejsów API do szerszego ekosystemu .NET, należy pamiętać o potencjale dla programu .NET 5,0, aby wprowadzić niepożądane zachowania lub ujawnić ukryte usterki, które już istnieją w aplikacji.

Narażone interfejsy API obejmują:

- <xref:System.String.Compare%2A?displayProperty=fullName>
- <xref:System.String.EndsWith%2A?displayProperty=fullName>
- <xref:System.String.IndexOf%2A?displayProperty=fullName>
- <xref:System.String.StartsWith%2A?displayProperty=fullName>
- <xref:System.String.ToLower%2A?displayProperty=fullName>
- <xref:System.String.ToLowerInvariant%2A?displayProperty=fullName>
- <xref:System.String.ToUpper%2A?displayProperty=fullName>
- <xref:System.String.ToUpperInvariant%2A?displayProperty=fullName>
- <xref:System.Globalization.TextInfo?displayProperty=fullName> (większość elementów członkowskich)
- <xref:System.Globalization.CompareInfo?displayProperty=fullName> (większość elementów członkowskich)
- <xref:System.Array.Sort%2A?displayProperty=fullName> (podczas sortowania tablic ciągów)
- <xref:System.Collections.Generic.List%601.Sort?displayProperty=fullName> (gdy elementy listy są ciągami)
- <xref:System.Collections.Generic.SortedDictionary%602?displayProperty=fullName> (gdy klucze są ciągami)
- <xref:System.Collections.Generic.SortedList%602?displayProperty=fullName> (gdy klucze są ciągami)
- <xref:System.Collections.Generic.SortedSet%601?displayProperty=fullName> (gdy zestaw zawiera ciągi)

> [!NOTE]
> Nie jest to pełna lista interfejsów API, których to dotyczy.

Wszystkie powyższe interfejsy API używają domyślnie wyszukiwania ciągów *językowych* i porównywania przy użyciu [bieżącej kultury](xref:System.Threading.Thread.CurrentCulture)wątku. Różnice między *językiem* a przeszukiwaniem i porównaniem *porządkowym* są określane w [liczbie porządkowej a przeszukiwaniu i porównaniu językowej](#ordinal-vs-linguistic-search-and-comparison).

Ponieważ ICU implementują porównania ciągów językowych inaczej niż w przypadku aplikacji NLS, opartych na systemie Windows, które uaktualniają do programu .NET 5,0 ze starszej wersji programu .NET Core lub .NET Framework, a wywołanie jednego z tych interfejsów API może zauważyć, że interfejsy API zaczynają się od innych zachowań.

### <a name="exceptions"></a>Wyjątki

* Jeśli interfejs API akceptuje jawnie `StringComparison` lub `CultureInfo` parametr, ten parametr zastępuje zachowanie domyślne interfejsu API.
* `System.String` elementy członkowskie, w których pierwszy parametr jest typu `char` (na przykład <xref:System.String.IndexOf(System.Char)?displayProperty=nameWithType> ) używają wyszukiwania porządkowego, chyba że obiekt wywołujący przekazuje jawny `StringComparison` argument, który określa `CurrentCulture[IgnoreCase]` lub `InvariantCulture[IgnoreCase]` .

Aby zapoznać się z bardziej szczegółową analizą zachowania poszczególnych <xref:System.String> interfejsów API, zobacz sekcję [domyślne typy wyszukiwania i porównywania](#default-search-and-comparison-types) .

## <a name="ordinal-vs-linguistic-search-and-comparison"></a>Liczba porządkowa a wyszukiwanie lingwistyczne i porównanie

*Liczba porządkowa* (znana także jako *niejęzykowa*) Wyszukiwanie i porównywanie składa ciąg w poszczególnych `char` elementach i wykonuje wyszukiwanie typu char-by-char. Na przykład ciągi `"dog"` i `"dog"` porównywanie jako *takie* same, jak w przypadku opcji `Ordinal` porównującej, ponieważ dwa ciągi składają się z dokładnie tej samej sekwencji znaków. Jednakże `"dog"` i `"Dog"` porównać *nie równa* się w ramach opcji `Ordinal` porównującej, ponieważ nie zawierają dokładnie tej samej sekwencji znaków. Oznacza to, że wielkie litery `'D'` `U+0044` występuje przed punktem kodu małymi literami `'d'` `U+0064` , co spowoduje `"dog"` sortowanie przed `"Dog"` .

`OrdinalIgnoreCase`Funkcja porównująca nadal działa na zasadzie typu char-by-char, ale eliminuje różnice wielkości liter podczas wykonywania operacji. W obszarze `OrdinalIgnoreCase` porównującym pary znaków `'d'` i są `'D'` porównywane jako *równe*, tak jak pary char `'á'` i `'Á'` . Ale nieakcentowane znak jest `'a'` porównywany z *nierównym* znakiem akcentu `'á'` .

Kilka przykładów tego typu przedstawiono w poniższej tabeli:

| Ciąg 1 | Ciąg 2 | `Ordinal` prowadzone | `OrdinalIgnoreCase` prowadzone |
|---|---|---|---|
| `"dog"` | `"dog"` | equal | equal |
| `"dog"` | `"Dog"` | nie równa się | equal |
| `"resume"` | `"Resume"` | nie równa się | equal |
| `"resume"` | `"résumé"` | nie równa się | nie równa się |

Unicode umożliwia również ciągów, które mają kilka różnych reprezentacji w pamięci. Na przykład e-ostra (é) może być reprezentowana na dwa możliwe sposoby:

* Pojedynczy znak literału `'é'` (również zapisany jako `'\u00E9'` ).
* Znak nieakcentowane literału `'e'` , po którym następuje łączenie znaku modyfikatora akcentu `'\u0301'` .

Oznacza to, że _four_ `"résumé"` podczas wyświetlania są wyświetlane następujące cztery ciągi, nawet jeśli ich elementy składowe różnią się. Ciągi używają kombinacji znaków literału `'é'` lub literałów nieakcentowanech `'e'` znaków oraz łączenia modyfikatora akcentu `'\u0301'` .

* `"r\u00E9sum\u00E9"`
* `"r\u00E9sume\u0301"`
* `"re\u0301sum\u00E9"`
* `"re\u0301sume\u0301"`

W obszarze porównującej wartości porządkowej żaden z tych ciągów nie jest porównywany ze sobą. Wynika to z faktu, że wszystkie one zawierają różne sekwencje znaków, nawet jeśli są renderowane na ekranie, wszystkie wyglądają tak samo.

Podczas wykonywania `string.IndexOf(..., StringComparison.Ordinal)` operacji środowisko uruchomieniowe szuka dokładnego dopasowania podciągu. Wyniki są następujące.

```cs
Console.WriteLine("resume".IndexOf("e", StringComparison.Ordinal)); // prints '1'
Console.WriteLine("r\u00E9sum\u00E9".IndexOf("e", StringComparison.Ordinal)); // prints '-1'
Console.WriteLine("r\u00E9sume\u0301".IndexOf("e", StringComparison.Ordinal)); // prints '5'
Console.WriteLine("re\u0301sum\u00E9".IndexOf("e", StringComparison.Ordinal)); // prints '1'
Console.WriteLine("re\u0301sume\u0301".IndexOf("e", StringComparison.Ordinal)); // prints '1'
Console.WriteLine("resume".IndexOf("E", StringComparison.OrdinalIgnoreCase)); // prints '1'
Console.WriteLine("r\u00E9sum\u00E9".IndexOf("E", StringComparison.OrdinalIgnoreCase)); // prints '-1'
Console.WriteLine("r\u00E9sume\u0301".IndexOf("E", StringComparison.OrdinalIgnoreCase)); // prints '5'
Console.WriteLine("re\u0301sum\u00E9".IndexOf("E", StringComparison.OrdinalIgnoreCase)); // prints '1'
Console.WriteLine("re\u0301sume\u0301".IndexOf("E", StringComparison.OrdinalIgnoreCase)); // prints '1'
```

Ustawienie kultury bieżącego wątku nie ma żadnego wpływania na liczby porządkowe wyszukiwania i procedury porównania.

Procedury wyszukiwania i porównywania *lingwistycznego* służą do rozdzielania ciągu na *elementy sortowania* i wykonywania wyszukiwania lub porównywania tych elementów. Nie jest konieczne mapowanie 1:1 między znakami ciągu a jego elementami sortowania elementów. Na przykład ciąg o długości 2 może składać się tylko z pojedynczego elementu sortowania. Gdy dwa ciągi są porównywane w sposób obsługujący język, funkcja porównująca sprawdza, czy elementy sortowania dwóch ciągów mają takie same semantykę, nawet jeśli znaki literału ciągu są różne.

Rozważ ponownie ciąg `"résumé"` i cztery różne reprezentacje. W poniższej tabeli przedstawiono każdą reprezentację rozdzielona na elementy sortowania.

| Ciąg | Jako elementy sortowania |
|---|---|
| `"r\u00E9sum\u00E9"` | `"r" + "\u00E9" + "s" + "u" + "m" + "\u00E9"` |
| `"r\u00E9sume\u0301"` | `"r" + "\u00E9" + "s" + "u" + "m" + "e\u0301"` |
| `"re\u0301sum\u00E9"` | `"r" + "e\u0301" + "s" + "u" + "m" + "\u00E9"` |
| `"re\u0301sume\u0301"` | `"r" + "e\u00E9" + "s" + "u" + "m" + "e\u0301"` |

Element sortowania ponosi swobodne informacje o tym, co czytelnicy mogą traktować jako pojedynczy znak lub klaster znaków. Jest on koncepcyjnie podobny do [klastra Grapheme](character-encoding-introduction.md#grapheme-clusters) , ale obejmuje nieco większy parasol.

W przypadku opcji porównującej język dokładne dopasowania nie są konieczne. W przeciwieństwie do ich semantyki są porównywane elementy sortowania. Na przykład, funkcja porównująca język traktuje podciągi `"\u00E9"` i jest `"e\u0301"` równe, ponieważ obie semantyką oznaczają "małą literę e z ostrym modyfikatorem akcentu". Dzięki temu `IndexOf` Metoda pasuje do podciągu `"e\u0301"` w większym ciągu zawierającym semantycznie równoważny podciąg `"\u00E9"` , jak pokazano w poniższym przykładzie kodu.

```cs
Console.WriteLine("r\u00E9sum\u00E9".IndexOf("e")); // prints '-1' (not found)
Console.WriteLine("r\u00E9sum\u00E9".IndexOf("e\u00E9")); // prints '1'
Console.WriteLine("\u00E9".IndexOf("e\u00E9")); // prints '0'
```

W związku z tym dwa ciągi o różnych długości mogą być porównywane tak samo, jak w przypadku użycia porównania językowe. Obiekty wywołujące powinny zadbać o to, aby nie występowały specyficzne dla logiki wielkości liter, która zajmuje się długością ciągu w takich scenariuszach.

Procedury wyszukiwania i porównywania *z obsługą kultur* są specjalną formą procedur wyszukiwania i porównywania języków. W obszarze porównującym z kulturą pojęcie elementu sortowania jest rozszerzane w celu uwzględnienia informacji specyficznych dla określonej kultury.

Na przykład [w alfabecie węgierskim](https://en.wikipedia.org/wiki/Hungarian_alphabet), gdy dwa znaki \<dz\> są wyświetlane z powrotem do tyłu, są uznawane za ich własną unikatową literę inną niż \<d\> lub \<z\> . Oznacza to, że kiedy \<dz\> występuje w ciągu, węgierskia funkcja porównująca z obsługą kultur traktuje ją jako pojedynczy element sortowania.

| Ciąg | Jako elementy sortowania | Uwagi |
|---|---|---|
| `"endz"` | `"e" + "n" + "d" + "z"` | (przy użyciu standardowej funkcji porównującej język) |
| `"endz"` | `"e" + "n" + "dz"` | (przy użyciu węgierskiej funkcji porównującej z kulturą) |

W przypadku korzystania z funkcji porównującej opartej na kulturze węgierskiej, oznacza to, że ciąg nie `"endz"` *does not* kończy się podciągiem `"z"` , ponieważ < \dz \> i < \z \> są uważane za elementy sortowania o różnym znaczeniu semantycznym.

```cs
// Set thread culture to Hungarian
CultureInfo.CurrentCulture = CultureInfo.GetCultureInfo("hu-HU");
Console.WriteLine("endz".EndsWith("z")); // Prints 'False'

// Set thread culture to invariant culture
CultureInfo.CurrentCulture = CultureInfo.InvariantCulture;
Console.WriteLine("endz".EndsWith("z")); // Prints 'True'
```

> [!NOTE]
>
> - Zachowanie: w przypadku języków i funkcji porównujących z obsługą kultur mogą być poddawane korekty zachowań od czasu do czasu. Zarówno ICU, jak i Starsza funkcja funkcji NLS systemu Windows są aktualizowane w celu uwzględnienia zmian w językach świata. Aby uzyskać więcej informacji, zobacz zmiany danych regionalnych wpisów w blogu [(kulturę)](/archive/blogs/shawnste/locale-culture-data-churn). Zachowanie funkcji porównującej *liczby porządkowej* nigdy nie ulegnie zmianie, ponieważ wykonuje dokładne wyszukiwanie bitowe i porównanie. Jednak zachowanie funkcji porównującej *OrdinalIgnoreCase* może ulec zmianie w miarę zwiększania rozmiaru Unicode, aby obejmowało więcej zestawów znaków i poprawiał pominięcia w istniejących danych o wielkości liter.
> - Użycie: funkcje porównujące `StringComparison.InvariantCulture` i `StringComparison.InvariantCultureIgnoreCase` są to porównania językowe, które nie obsługują kultury. Oznacza to, że te porównania są zrozumiałe dla pojęć, takich jak znak wyróżniony é, z wieloma możliwymi reprezentacjami, i że wszystkie takie reprezentacje powinny być traktowane jako równe. Ale nieoparte na kulturze funkcje porównujące nie będą zawierały specjalnej obsługi dla elementu \<dz\> DISTINCT z \<d\> lub \<z\> , jak pokazano powyżej. Nie mogą również zawierać specjalnych liter, takich jak niemiecki Eszett (ß).

Platforma .NET oferuje również *niezmienną tryb globalizacji*. Ten tryb rezygnacji wyłącza ścieżki kodu, które zajmują się przeszukiwaniem językowym i procedurami porównania. W tym trybie wszystkie operacje używają wartości *porządkowych* lub *OrdinalIgnoreCase* , niezależnie od tego, `CultureInfo` co `StringComparison` lub argument obiektu wywołującego. Aby uzyskać więcej informacji, zobacz [Opcje konfiguracji czasu wykonywania dla globalizacji](../../core/run-time-config/globalization.md) i [tryb niezmienny globalizacji platformy .NET Core](https://github.com/dotnet/runtime/blob/master/docs/design/features/globalization-invariant-mode.md).

Aby uzyskać więcej informacji, zobacz [najlepsze rozwiązania dotyczące porównywania ciągów w programie .NET](best-practices-strings.md).

## <a name="security-implications"></a>Implikacje dotyczące bezpieczeństwa

Jeśli aplikacja korzysta z dostosowanego do filtrowania interfejsu API, zalecamy włączenie reguł analizy kodu CA1307 i CA1309, aby pomóc w znalezieniu miejsc, w których wyszukiwanie lingwistyczne mogło przypadkowo zostać użyte zamiast wyszukiwania porządkowego. Wzorce kodu podobne do poniższych mogą być podatne na luki w zabezpieczeniach.

```cs
//
// THIS SAMPLE CODE IS INCORRECT.
// DO NOT USE IT IN PRODUCTION.
//
public bool ContainsHtmlSensitiveCharacters(string input)
{
    if (input.IndexOf("<") >= 0) { return true; }
    if (input.IndexOf("&") >= 0) { return true; }
    return false;
}
```

Ponieważ `string.IndexOf(string)` Metoda domyślnie używa wyszukiwania w języku językowym, możliwe jest, aby ciąg zawierał literał `'<'` lub `'&'` znak i dla `string.IndexOf(string)` procedury zwracanej `-1` , wskazujący, że nie znaleziono podciągu wyszukiwania. Reguły analizy kodu CA1307 i CA1309 flag takich, które wywołują Lokacje i ostrzegają dewelopera o potencjalnym problemie.

## <a name="default-search-and-comparison-types"></a>Domyślne typy wyszukiwania i porównywania

W poniższej tabeli wymieniono domyślne typy wyszukiwania i porównywania dla różnych interfejsów API w postaci ciągów i ciągów. Jeśli obiekt wywołujący dostarcza jawny `CultureInfo` lub `StringComparison` parametr, ten parametr będzie honorować domyślnie.

| interfejs API | Zachowanie domyślne | Uwagi |
|---|---|---|
| `string.Compare` | CurrentCulture | |
| `string.CompareTo` | CurrentCulture | |
| `string.Contains` | Liczba porządkowa | |
| `string.EndsWith` | Liczba porządkowa | (gdy pierwszy parametr to a `char` ) |
| `string.EndsWith` | CurrentCulture | (gdy pierwszy parametr to a `string` ) |
| `string.Equals` | Liczba porządkowa | |
| `string.GetHashCode` | Liczba porządkowa | |
| `string.IndexOf` | Liczba porządkowa | (gdy pierwszy parametr to a `char` ) |
| `string.IndexOf` | CurrentCulture | (gdy pierwszy parametr to a `string` ) |
| `string.IndexOfAny` | Liczba porządkowa | |
| `string.LastIndexOf` | Liczba porządkowa | (gdy pierwszy parametr to a `char` ) |
| `string.LastIndexOf` | CurrentCulture | (gdy pierwszy parametr to a `string` ) |
| `string.LastIndexOfAny` | Liczba porządkowa | |
| `string.Replace` | Liczba porządkowa | |
| `string.Split` | Liczba porządkowa | |
| `string.StartsWith` | Liczba porządkowa | (gdy pierwszy parametr to a `char` ) |
| `string.StartsWith` | CurrentCulture | (gdy pierwszy parametr to a `string` ) |
| `string.ToLower` | CurrentCulture | |
| `string.ToLowerInvariant` | InvariantCulture | |
| `string.ToUpper` | CurrentCulture | |
| `string.ToUpperInvariant` | InvariantCulture | |
| `string.Trim` | Liczba porządkowa | |
| `string.TrimEnd` | Liczba porządkowa | |
| `string.TrimStart` | Liczba porządkowa | |
| `string == string` | Liczba porządkowa | |
| `string != string` | Liczba porządkowa | |

W przeciwieństwie do `string` interfejsów API, wszystkie `MemoryExtensions` interfejsy API domyślnie wykonują wyszukiwanie *porządkowe* i porównania z następującymi wyjątkami.

| interfejs API | Zachowanie domyślne | Uwagi |
|---|---|---|
| `MemoryExtensions.ToLower` | CurrentCulture | (gdy przeszedł argument o wartości null `CultureInfo` ) |
| `MemoryExtensions.ToLowerInvariant` | InvariantCulture | |
| `MemoryExtensions.ToUpper` | CurrentCulture | (gdy przeszedł argument o wartości null `CultureInfo` ) |
| `MemoryExtensions.ToUpperInvariant` | InvariantCulture | |

Jest to, że podczas konwertowania kodu z konsumowania `string` do konsumowania `ReadOnlySpan<char>` zmiany behawioralne mogą być wprowadzane przypadkowo. Przykład poniżej.

```cs
string str = GetString();
if (str.StartsWith("Hello")) { /* do something */ } // this is a CULTURE-AWARE (linguistic) comparison

ReadOnlySpan<char> span = s.AsSpan();
if (span.StartsWith("Hello")) { /* do something */ } // this is an ORDINAL (non-linguistic) comparison
```

Zalecanym sposobem na rozwiązanie tego jest przekazanie jawnego `StringComparison` parametru do tych interfejsów API. Reguły analizy kodu CA1307 i CA1309 mogą pomóc w tym.

```cs
string str = GetString();
if (str.StartsWith("Hello", StringComparison.Ordinal)) { /* do something */ } // ordinal comparison

ReadOnlySpan<char> span = s.AsSpan();
if (span.StartsWith("Hello", StringComparison.Ordinal)) { /* do something */ } // ordinal comparison
```

## <a name="see-also"></a>Zobacz też

- [Zmiany dotyczące podziału globalizacji](../../core/compatibility/globalization.md)
- [Najlepsze rozwiązania dotyczące porównywania ciągów w programie .NET](best-practices-strings.md)
- [Jak porównać ciągi w języku C #](../../csharp/how-to/compare-strings.md)
- [Globalizacja i ICU platformy .NET](../globalization-localization/globalization-icu.md)
- [Liczba porządkowa a operacje na ciągach zależnych od kultury](/dotnet/api/system.string#ordinal-vs-culture-sensitive-operations)
- [Przegląd analizy kodu źródłowego platformy .NET](../../fundamentals/code-analysis/overview.md)
