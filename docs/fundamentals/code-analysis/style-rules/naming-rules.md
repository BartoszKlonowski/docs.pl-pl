---
title: Reguły nazewnictwa stylu kodu
description: Dowiedz się więcej na temat reguł stylu kodu platformy .NET służących do nazywania elementów kodu.
ms.date: 09/25/2020
ms.topic: reference
author: gewarren
ms.author: gewarren
dev_langs:
- CSharp
- VB
f1_keywords:
- IDE1006
- naming rules
helpviewer_keywords:
- IDE1006
- naming code style rules [EditorConfig]
- naming rules
- EditorConfig naming conventions
ms.openlocfilehash: 8ce209e64ee7f9f9028c221daedef8fc6a993ef7
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96590071"
---
# <a name="naming-rules"></a>Reguły nazewnictwa

Reguły nazewnictwa dotyczą nazewnictwa elementów kodu języka programowania .NET, takich jak klasy, właściwości i metody. Można na przykład określić, że publiczne składowe muszą być pisane wielkimi literami, lub pola prywatne muszą zaczynać się od `_` .

Reguła nazewnictwa ma trzy części:

* Grupa symboli, do której się odnosi.
* Styl nazewnictwa, który ma zostać skojarzony z regułą.
* Ważność wymuszania Konwencji.

Reguły nazewnictwa są definiowane w pliku EditorConfig.

## <a name="general-syntax"></a>Składnia ogólna

Aby zdefiniować regułę nazewnictwa, grupę symboli lub styl nazewnictwa, należy ustawić jedną lub więcej właściwości, używając następującej składni:

```ini
<prefix>.<title>.<propertyName> = <propertyValue>
```

Każda właściwość powinna być ustawiona tylko raz, ale niektóre ustawienia dopuszczają wiele wartości rozdzielanych przecinkami.

Kolejność właściwości nie jest ważna.

### \<prefix>

**\<prefix>** Określa, jakiego rodzaju elementu jest definiowana &mdash; reguła nazewnictwa, Grupa symboli lub styl nazewnictwa, &mdash; i musi mieć jedną z następujących wartości:

| Aby ustawić właściwość dla | Użyj prefiksu | Przykład |
| --- | --- | -- |
| Reguła nazewnictwa | `dotnet_naming_rule` | `dotnet_naming_rule.types_should_be_pascal_case.severity = suggestion` |
| Grupa symboli | `dotnet_naming_symbols` | `dotnet_naming_symbols.interface.applicable_kinds = interface` |
| Styl nazewnictwa | `dotnet_naming_style` | `dotnet_naming_style.pascal_case.capitalization = pascal_case` |

Każdy typ &mdash; [reguły nazewnictwa](#naming-rule-properties)definicji, [grupy symboli](#symbol-group-properties)lub [stylu nazewnictwa](#naming-style-properties) &mdash; ma własne obsługiwane właściwości, zgodnie z opisem w poniższych sekcjach.

### \<title>

**\<title>** jest wybraną nazwą opisową, która kojarzy wiele ustawień właściwości w jedną definicję. Na przykład następujące właściwości tworzą dwa definicje grup symboli `interface` i `types` , z których każdy ma ustawione dwie właściwości.

```ini
dotnet_naming_symbols.interface.applicable_kinds = interface
dotnet_naming_symbols.interface.applicable_accessibilities = public, internal, private, protected, protected_internal, private_protected

dotnet_naming_symbols.types.applicable_kinds = class, struct, interface, enum, delegate
dotnet_naming_symbols.types.applicable_accessibilities = public, internal, private, protected, protected_internal, private_protected
```

## <a name="naming-rule-properties"></a>Właściwości reguły nazewnictwa

Aby reguła zaczęła obowiązywać, wymagane są wszystkie właściwości reguły nazewnictwa.

| Właściwość | Opis |
| -- | -- |
| `symbols` | Tytuł grupy symboli definiujący symbole, do których ma zostać zastosowana ta reguła. |
| `style` | Tytuł stylu nazewnictwa, który powinien zostać skojarzony z tą regułą. |
| `severity` |  Ustawia ważność, przy której ma być wymuszana reguła nazewnictwa. Ustaw skojarzoną wartość na jeden z dostępnych [poziomów ważności](https://docs.microsoft.com/dotnet/fundamentals/code-analysis/configuration-options#severity-level). <sup>1</sup> |

**Uwagi:**

1. Specyfikacja ważności w ramach reguły nazewnictwa jest przestrzegana tylko w środowisk ideach programistycznych, takich jak program Visual Studio. To ustawienie nie jest rozpoznawane przez kompilatory języka C# lub VB, dlatego nie jest przestrzegane podczas kompilacji. Zamiast tego, aby wymusić reguły stylu nazewnictwa w kompilacji, należy ustawić ważność przy użyciu konfiguracji o ważności opartej na IDENTYFIKATORze reguły zgodnie z opisem w [tej sekcji](#rule-id-ide1006-naming-rule-violation). Aby uzyskać więcej informacji, zobacz ten problem w serwisie [GitHub](https://github.com/dotnet/roslyn/issues/44201).

## <a name="rule-order"></a>Kolejność reguł

Kolejność, w której reguły nazewnictwa są zdefiniowane w pliku EditorConfig, nie ma znaczenia. Reguły nazewnictwa są automatycznie uporządkowane zgodnie z definicją samych reguł. [Rozszerzenie usługi języka EditorConfig](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.EditorConfig) może analizować plik EditorConfig i zgłaszać przypadki, w których kolejność sortowania reguł w pliku różni się od tego, co kompilator będzie używać w czasie wykonywania.

> [!NOTE]
>
> Jeśli używasz wersji programu Visual Studio starszej niż Visual Studio 2019 w wersji 16,2, reguły nazewnictwa powinny być uporządkowane z najbardziej szczegółowych elementów w pliku EditorConfig. Pierwsza napotkana reguła jest jedyną zastosowanym regułą. Jeśli jednak istnieje wiele *Właściwości* reguł o tej samej nazwie, pierwszeństwo ma właściwość ostatnio znaleziona o tej nazwie. Aby uzyskać więcej informacji, zobacz [Hierarchia plików i pierwszeństwo](/visualstudio/ide/create-portable-custom-editor-options#file-hierarchy-and-precedence).

## <a name="symbol-group-properties"></a>Właściwości grupy symboli

Można ustawić następujące właściwości dla grup symboli, aby ograniczyć liczbę symboli uwzględnionych w grupie. Aby określić wiele wartości w jednym ustawieniu właściwości, rozdziel je przecinkami.

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| -- | -- | -- | -- |
| `applicable_kinds` | Rodzaje symboli w grupie <sup>1</sup> | `*` (Użyj tej wartości, aby określić wszystkie symbole)<br/>`namespace`<br/>`class`<br/>`struct`<br/>`interface`<br/>`enum`<br/>`property`<br/>`method`<br/>`field`<br/>`event`<br/>`delegate`<br/>`parameter`<br/>`type_parameter`<br/>`local`<br/>`local_function` | Tak |
| `applicable_accessibilities` | Poziomy ułatwień dostępu symboli w grupie | `*` (Użyj tej wartości, aby określić wszystkie poziomy ułatwień dostępu)<br/>`public`<br/>`internal` lub `friend`<br/>`private`<br/>`protected`<br/>`protected_internal` lub `protected_friend`<br/>`private_protected`<br/>`local` (dla symboli zdefiniowanych w ramach metody) | Tak |
| `required_modifiers` | Dopasowuje tylko symbole ze _wszystkimi_ określonymi modyfikatorami <sup>2</sup> | `abstract` lub `must_inherit`<br/>`async`<br/>`const`<br/>`readonly`<br/>`static` lub `shared` <sup>3</sup> | Nie |

**Uwagi:**

1. Elementy członkowskie krotek nie są obecnie obsługiwane w programie `applicable_kinds` .
2. Grupa symboli dopasowuje _wszystkie_ Modyfikatory we `required_modifiers` właściwości.  W przypadku pominięcia tej właściwości nie są wymagane żadne specyficzne Modyfikatory dla dopasowania. Oznacza to, że Modyfikatory symbolu nie mają wpływu na to, czy ta reguła jest stosowana.
3. Jeśli grupa ma `static` lub `shared` we `required_modifiers` właściwości, grupa będzie zawierać również `const` symbole, ponieważ są one niejawnie `static` / `Shared` . Jeśli jednak `static` reguły nazewnictwa nie mają być stosowane do `const` symboli, można utworzyć nową regułę nazewnictwa z grupą symboli `const` .

## <a name="naming-style-properties"></a>Właściwości stylu nazewnictwa

Styl nazewnictwa definiuje konwencje, które mają zostać wymuszone przez regułę. Na przykład:

* Używaj wielką literą `PascalCase`
* Rozpoczyna się od `m_`
* Kończący się na `_g`
* Oddziel wyrazy `__`

Dla stylu nazewnictwa można ustawić następujące właściwości:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| -- | -- | -- | -- |
| `capitalization` | Styl wersalików dla słów w symbolu | `pascal_case`<br/>`camel_case`<br/>`first_word_upper`<br/>`all_upper`<br/>`all_lower` | Tak<sup>1</sup> |
| `required_prefix` | Musi zaczynać się od tych znaków | | Nie |
| `required_suffix` | Musi kończyć się tymi znakami | | Nie |
| `word_separator` | Słowa w symbolu muszą być rozdzielone znakiem tego znaku | | Nie |

**Uwagi:**

1. Należy określić styl kapitalizacji jako część stylu nazewnictwa. w przeciwnym razie styl nazewnictwa może zostać zignorowany.

## <a name="default-naming-styles"></a>Domyślne style nazewnictwa

Jeśli nie określisz żadnych niestandardowych reguł nazewnictwa, zostaną użyte następujące style domyślne:

- W przypadku klas, struktur, wyliczeń, właściwości i zdarzeń z `public` , `private` , `internal` ,, `protected` lub `protected_internal` dostępności, domyślny styl nazewnictwa to przypadek Pascal.

- W przypadku interfejsów z `public` ,,,, `private` `internal` `protected` lub `protected_internal` dostępności, domyślny styl nazewnictwa jest przypadek Pascal z wymaganym prefiksem **I**.

## <a name="example"></a>Przykład

Następujący plik *. editorconfig* zawiera konwencję nazewnictwa, która określa, że właściwości publiczne, metody, pola, zdarzenia i Delegaty muszą być pisane wielkimi literami. Należy zauważyć, że ta konwencja nazewnictwa określa wiele rodzajów symboli, do których ma zostać zastosowana reguła, przy użyciu przecinka do oddzielenia wartości.

```ini
[*.{cs,vb}]

# Defining the 'public_symbols' symbol group
dotnet_naming_symbols.public_symbols.applicable_kinds           = property,method,field,event,delegate
dotnet_naming_symbols.public_symbols.applicable_accessibilities = public
dotnet_naming_symbols.public_symbols.required_modifiers         = readonly

# Defining the `first_word_upper_case_style` naming style
dotnet_naming_style.first_word_upper_case_style.capitalization = first_word_upper

# Defining the `public_members_must_be_capitalized` naming rule, by setting the symbol group to the 'public symbols' symbol group,
dotnet_naming_rule.public_members_must_be_capitalized.symbols   = public_symbols
# setting the naming style to the `first_word_upper_case_style` naming style,
dotnet_naming_rule.public_members_must_be_capitalized.style    = first_word_upper_case_style
# and setting the severity.
dotnet_naming_rule.public_members_must_be_capitalized.severity = suggestion
```

## <a name="rule-id-ide1006-naming-rule-violation"></a><a name="rule-id-ide1006-naming-rule-violation"></a>Identyfikator reguły: "IDE1006" (naruszenie reguły nazewnictwa)

Wszystkie opcje nazewnictwa mają Identyfikator reguły `IDE1006` i tytuł `Naming rule violation` . Ważność naruszeń nazw można skonfigurować globalnie w pliku EditorConfig o następującej składni:

```ini
dotnet_diagnostic.IDE1006.severity = <severity value>
```

Wartość ważności musi być `warning` `error` [wymuszana w kompilacji](../overview.md#code-style-analysis). Dla wszystkich możliwych wartości ważności zobacz [poziom ważności](../configuration-options.md#severity-level).

## <a name="see-also"></a>Zobacz także

- [Reguły języka](language-rules.md)
- [Reguły formatowania](formatting-rules.md)
- [Roslyn reguły nazewnictwa](https://github.com/dotnet/roslyn/blob/master/.editorconfig#L63)
- [Dokumentacja reguł stylu kodu platformy .NET](index.md)
