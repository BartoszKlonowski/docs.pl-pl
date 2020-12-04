---
title: Opcje konfiguracji reguł jakości kodu
description: Dowiedz się, jak określić dodatkowe opcje konfiguracji dla reguł jakości kodu.
ms.date: 09/24/2020
ms.topic: conceptual
no-loc:
- EditorConfig
ms.openlocfilehash: af2984e73c554e8a1e1b32df9460933f86cc41be
ms.sourcegitcommit: 2e4adc490c1d2a705a0592b295d606b10b9f51f1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/25/2020
ms.locfileid: "96587125"
---
# <a name="code-quality-rule-configuration-options"></a>Opcje konfiguracji reguł jakości kodu

Reguły *jakości kodu* mają dodatkowe opcje konfiguracji, oprócz [konfigurowania ich ważności](configuration-options.md#severity-level). Na przykład każdy Analizator jakości kodu można skonfigurować tak, aby dotyczył tylko określonych części bazy kodu. Aby określić te opcje, należy dodać pary klucz-wartość do tego samego pliku, w [EditorConfig](https://editorconfig.org) którym można określić rozwiązania reguły i ogólne preferencje edytora.

## <a name="option-scopes"></a>Zakresy opcji

Każdą opcję rafinacji można skonfigurować dla wszystkich reguł, dla kategorii reguł (na przykład zabezpieczeń lub projektowania) lub dla określonej reguły.

### <a name="all-rules"></a>Wszystkie reguły

Składnia służąca do konfigurowania opcji dla *wszystkich* reguł jest następująca:

|Składnia|Przykład|
|-|-|
| dotnet_code_quality. OptionName = optionvalue | `dotnet_code_quality.api_surface = public` |

### <a name="category-of-rules"></a>Kategoria reguł

Składnia służąca do konfigurowania opcji dla *kategorii* reguł (na przykład nazewnictwa, projektowania lub wydajności) jest następująca:

|Składnia|Przykład|
|-|-|
| dotnet_code_quality. RuleCategory. optionName = optionvalue | `dotnet_code_quality.Naming.api_surface = public` |

### <a name="specific-rule"></a>Określona reguła

Składnia służąca do konfigurowania opcji dla *określonej* reguły jest następująca:

|Składnia|Przykład|
|-|-|
| dotnet_code_quality. RuleId. optionName = optionvalue | `dotnet_code_quality.CA1040.api_surface = public` |

## <a name="options"></a>Opcje

W tej sekcji wymieniono niektóre z dostępnych opcji. Aby wyświetlić pełną listę dostępnych opcji, zobacz temat [Konfiguracja analizatora](https://github.com/dotnet/roslyn-analyzers/blob/master/docs/Analyzer%20Configuration.md).

### <a name="api_surface"></a>api_surface

| Opis | Dozwolone wartości | Wartość domyślna | Konfigurowalne reguły |
| - | - | - | - |
| Która część powierzchni interfejsu API do przeanalizowania | `public`<br/>`internal` lub `friend`<br/>`private`<br/>`all`<br/><br/>Rozdziel wiele wartości przecinkami (,) | `public` | [CA1000](quality-rules/ca1000.md) [CA1003](quality-rules/ca1003.md) [CA1008](quality-rules/ca1008.md) [CA1010](quality-rules/ca1010.md)<br/>[CA1012](quality-rules/ca1012.md) [CA1024](quality-rules/ca1024.md) [CA1027](quality-rules/ca1027.md) [CA1028](quality-rules/ca1028.md)<br/>[CA1030](quality-rules/ca1030.md) [CA1036](quality-rules/ca1036.md) [CA1040](quality-rules/ca1040.md) [CA1041](quality-rules/ca1041.md)<br/>[CA1043](quality-rules/ca1043.md) [CA1044](quality-rules/ca1044.md) [CA1051](quality-rules/ca1051.md) [CA1052](quality-rules/ca1052.md)<br/>[CA1054](quality-rules/ca1054.md) [CA1055](quality-rules/ca1055.md) [CA1056](quality-rules/ca1056.md) [CA1058](quality-rules/ca1058.md)<br/>[CA1063](quality-rules/ca1063.md) [CA1708](quality-rules/ca1708.md) [CA1710](quality-rules/ca1710.md) [CA1711](quality-rules/ca1711.md)<br/>[CA1714](quality-rules/ca1714.md) [CA1715](quality-rules/ca1715.md) [CA1716](quality-rules/ca1716.md) [CA1717](quality-rules/ca1717.md)<br/>[CA1720](quality-rules/ca1720.md) [CA1721](quality-rules/ca1721.md) [CA1725](quality-rules/ca1725.md) [CA1801](quality-rules/ca1801.md)<br/>[CA1802](quality-rules/ca1802.md) [CA1815](quality-rules/ca1815.md) [CA1819](quality-rules/ca1819.md) [CA2217](quality-rules/ca2217.md)<br/>[CA2225](quality-rules/ca2225.md) [CA2226](quality-rules/ca2226.md) [CA2231](quality-rules/ca2231.md) [CA2234](quality-rules/ca2234.md)<br/>|

### <a name="exclude_async_void_methods"></a>exclude_async_void_methods

| Opis | Dozwolone wartości | Wartość domyślna | Konfigurowalne reguły |
| - | - | - | - |
| Czy ignorować metody asynchroniczne, które nie zwracają wartości | `true`<br/>`false` | `false` | [CA2007](quality-rules/ca2007.md) |

> [!NOTE]
> Ta opcja została nazwana `skip_async_void_methods` w starszej wersji.

### <a name="exclude_single_letter_type_parameters"></a>exclude_single_letter_type_parameters

| Opis | Dozwolone wartości | Wartość domyślna | Konfigurowalne reguły |
| - | - | - | - |
| Określa, czy wykluczyć z reguły [parametry typu](../../csharp/programming-guide/generics/generic-type-parameters.md) o pojedynczym znaku, na przykład `S` w `Collection<S>` | `true`<br/>`false` | `false` | [CA1715](quality-rules/ca1715.md) |

> [!NOTE]
> Ta opcja została nazwana `allow_single_letter_type_parameters` w starszej wersji.

### <a name="output_kind"></a>output_kind

| Opis | Dozwolone wartości | Wartość domyślna | Konfigurowalne reguły |
| - | - | - | - |
| Określa, że kod w projekcie, który generuje ten typ zestawu, powinien być analizowany | Co najmniej jedno pole <xref:Microsoft.CodeAnalysis.OutputKind> wyliczenia<br/><br/>Rozdziel wiele wartości przecinkami (,) | Wszystkie rodzaje danych wyjściowych | [CA2007](quality-rules/ca2007.md) |

### <a name="required_modifiers"></a>required_modifiers

| Opis | Dozwolone wartości | Wartość domyślna | Konfigurowalne reguły |
| - | - | - | - |
| Określa wymagane Modyfikatory dla interfejsów API, które powinny być analizowane | Jedna lub więcej wartości z poniższej dozwolonej tabeli modyfikatorów<br/><br/>Rozdziel wiele wartości przecinkami (,) | Zależy od każdej reguły | [CA1802](quality-rules/ca1802.md) |

| Dozwolony modyfikator | Podsumowanie |
| --- | --- |
| `none` | Brak wymagania modyfikatora |
| `static` lub `Shared` | Musi być zadeklarowana jako `static` ( `Shared` w Visual Basic) |
| `const` | Musi być zadeklarowany jako `const` |
| `readonly` | Musi być zadeklarowany jako `readonly` |
| `abstract` | Musi być zadeklarowany jako `abstract` |
| `virtual` | Musi być zadeklarowany jako `virtual` |
| `override` | Musi być zadeklarowany jako `override` |
| `sealed` | Musi być zadeklarowany jako `sealed` |
| `extern` | Musi być zadeklarowany jako `extern` |
| `async` | Musi być zadeklarowany jako `async` |

### <a name="exclude_extension_method_this_parameter"></a>exclude_extension_method_this_parameter

| Opis | Dozwolone wartości | Wartość domyślna | Konfigurowalne reguły |
| - | - | - | - |
| Czy pominąć analizę dla `this` parametru metod rozszerzenia | `true`<br/>`false` | `false` | [CA1062](quality-rules/ca1062.md) |

### <a name="null_check_validation_methods"></a>null_check_validation_methods

| Opis | Dozwolone wartości | Wartość domyślna | Konfigurowalne reguły |
| - | - | - | - |
| Nazwy metod sprawdzania poprawności kontroli wartości null, które sprawdzają, czy argumenty przekazane do metody są inne niż null. | Dozwolone formaty nazw metod (oddzielone przecinkami `|` ):<br/> -Tylko nazwa metody (zawiera wszystkie metody o nazwie, niezależnie od typu zawierającego lub przestrzeni nazw)<br/> — W pełni kwalifikowane nazwy w [formacie identyfikatora dokumentacji](https://github.com/dotnet/csharplang/blob/master/spec/documentation-comments.md#id-string-format)symbolu, z opcjonalnym `M:` prefiksem | Brak | [CA1062](quality-rules/ca1062.md) |

### <a name="additional_string_formatting_methods"></a>additional_string_formatting_methods

| Opis | Dozwolone wartości | Wartość domyślna | Konfigurowalne reguły |
| - | - | - | - |
| Nazwy dodatkowych metod formatowania ciągu | Dozwolone formaty nazw metod (oddzielone przecinkami `|` ):<br/> -Tylko nazwa metody (zawiera wszystkie metody o nazwie, niezależnie od typu zawierającego lub przestrzeni nazw)<br/> — W pełni kwalifikowane nazwy w [formacie identyfikatora dokumentacji](/dotnet/csharp/language-reference/language-specification/documentation-comments#id-string-format)symbolu, z opcjonalnym `M:` prefiksem | Brak | [CA2241](quality-rules/ca2241.md) |

### <a name="excluded_type_names_with_derived_types"></a>excluded_type_names_with_derived_types

| Opis | Dozwolone wartości | Wartość domyślna | Konfigurowalne reguły |
| - | - | - | - |
| Nazwy typów, takie jak typ i wszystkie jego typy pochodne, są wykluczone na potrzeby analizy | Dozwolone formaty nazw symboli (oddzielone przecinkami `|` ):<br/> -Tylko nazwa typu (obejmuje wszystkie typy z nazwą, niezależnie od typu zawierającego lub przestrzeni nazw)<br/> — W pełni kwalifikowane nazwy w [formacie identyfikatora dokumentacji](/dotnet/csharp/language-reference/language-specification/documentation-comments#id-string-format)symbolu, z opcjonalnym `T:` prefiksem | Brak | [CA1303](quality-rules/ca1303.md) |

### <a name="excluded_symbol_names"></a>excluded_symbol_names

| Opis | Dozwolone wartości | Wartość domyślna | Konfigurowalne reguły |
| - | - | - | - |
| Nazwy symboli, które są wykluczone na potrzeby analizy | Dozwolone formaty nazw symboli (oddzielone przecinkami `|` ):<br/> -Tylko nazwa symbolu (zawiera wszystkie symbole z nazwą, niezależnie od typu zawierającego lub przestrzeni nazw)<br/> — W pełni kwalifikowane nazwy w [formacie identyfikatora dokumentacji](/dotnet/csharp/language-reference/language-specification/documentation-comments#id-string-format)symbolu. Każda nazwa symbolu wymaga prefiksu rodzaju symboli, takiego jak `M:` prefiks dla metod, `T:` prefiks dla typów i `N:` prefiks dla przestrzeni nazw.<br/> - `.ctor` dla konstruktorów i `.cctor` dla konstruktorów statycznych | Brak | [CA1062](quality-rules/ca1062.md) [CA1303](quality-rules/ca1303.md) [CA2000](quality-rules/ca2000.md) [CA2100](quality-rules/ca2100.md) [CA2301](quality-rules/ca2301.md) [CA2302](quality-rules/ca2302.md)<br/>[CA2311](quality-rules/ca2311.md) [CA2312](quality-rules/ca2312.md) [CA2321](quality-rules/ca2321.md) [CA2322](quality-rules/ca2322.md) [CA2327](quality-rules/ca2327.md) [CA2328](quality-rules/ca2328.md)<br/>[CA2329](quality-rules/ca2329.md) [CA2330](quality-rules/ca2330.md) [CA3001](quality-rules/ca3001.md) [CA3002](quality-rules/ca3002.md) [CA3003](quality-rules/ca3003.md) [CA3004](quality-rules/ca3004.md)<br/>[CA3005](quality-rules/ca3005.md) [CA3006](quality-rules/ca3006.md) [CA3007](quality-rules/ca3007.md) [CA3008](quality-rules/ca3008.md) [CA3009](quality-rules/ca3009.md) [CA3010](quality-rules/ca3010.md)<br/>[CA3011](quality-rules/ca3011.md) [CA3012](quality-rules/ca3012.md) [CA5361](quality-rules/ca5361.md) CA5376 CA5377 [CA5378](quality-rules/ca5378.md)<br/>[CA5380](quality-rules/ca5380.md) [CA5381](quality-rules/ca5381.md) CA5382 CA5383 CA5384 CA5387<br/>CA5388 [CA5389](quality-rules/ca5389.md) CA5390 |

### <a name="disallowed_symbol_names"></a>disallowed_symbol_names

| Opis | Dozwolone wartości | Wartość domyślna | Konfigurowalne reguły |
| - | - | - | - |
| Nazwy symboli, które są niedozwolone w kontekście analizy | Dozwolone formaty nazw symboli (oddzielone przecinkami `|` ):<br/> -Tylko nazwa symbolu (zawiera wszystkie symbole z nazwą, niezależnie od typu zawierającego lub przestrzeni nazw)<br/> — W pełni kwalifikowane nazwy w [formacie identyfikatora dokumentacji](/dotnet/csharp/language-reference/language-specification/documentation-comments#id-string-format)symbolu. Każda nazwa symbolu wymaga prefiksu rodzaju symboli, takiego jak `M:` prefiks dla metod, `T:` prefiks dla typów i `N:` prefiks dla przestrzeni nazw.<br/> - `.ctor` dla konstruktorów i `.cctor` dla konstruktorów statycznych | Brak | [CA1031](quality-rules/ca1031.md) |
