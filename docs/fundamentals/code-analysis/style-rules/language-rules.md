---
title: Reguły języka stylu kodu
description: Dowiedz się więcej o różnych regułach stylów kodu dotyczących używania języka C# i Visual Basic konstrukcji językowych.
ms.date: 09/25/2020
ms.topic: reference
author: gewarren
ms.author: gewarren
dev_langs:
- CSharp
- VB
helpviewer_keywords:
- language code style rules [EditorConfig]
- language rules
- EditorConfig language conventions
ms.openlocfilehash: b77d9aa2a528a6cf540babd5e5acc148e48c489c
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96590072"
---
# <a name="language-rules"></a>Reguły języka

Reguły języka stylu kodu mają wpływ na sposób używania różnych konstrukcji języków programowania .NET, na przykład modyfikatory i nawiasy. Reguły są uwzględniane w następujących kategoriach:

- [Reguły stylu platformy .NET](#net-style-rules): reguły, które dotyczą zarówno języka C#, jak i Visual Basic. Nazwy opcji EditorConfig dla tych reguł zaczynają się od `dotnet_style_` prefiksu.
- [Reguły stylu języka c#](#c-style-rules): reguły, które są specyficzne tylko dla języka C#. Nazwy opcji EditorConfig dla tych reguł zaczynają się od `csharp_style_` prefiksu.
- [Reguły stylów Visual Basic](#visual-basic-style-rules): reguły specyficzne dla języka Visual Bsic. Nazwy opcji EditorConfig dla tych reguł zaczynają się od `visual_basic_style_` prefiksu.

## <a name="option-format"></a>Format opcji

Opcje reguł języka można określić w pliku EditorConfig o następującym formacie:

`option_name = value:severity`

- **Wartość**: dla każdej reguły języka należy określić wartość określającą, czy ma być preferowany styl. Wiele reguł przyjmuje wartość `true` (Preferuj ten styl) lub `false` (nie Preferuj tego stylu). Inne reguły akceptują wartości, takie jak `when_on_single_line` lub `never` .
- **Ważność**: druga część reguły określa [poziom ważności](../configuration-options.md#severity-level) reguły. Specyfikacja ważności jako część powyższej składni opcji jest przestrzegana tylko w środowisk IDE programistycznym, takich jak program Visual Studio. To ustawienie nie jest rozpoznawane przez kompilatory języka C# lub VB, dlatego nie jest przestrzegane podczas kompilacji. Zamiast tego, aby wymusić reguły stylu kodu podczas kompilacji, należy ustawić ważność przy użyciu składni konfiguracji ważności opartej na IDENTYFIKATORze reguły dla analizatorów. Składnia przyjmuje formularz `dotnet_diagnostic.<rule ID>.severity = <severity>` , na przykład `dotnet_diagnostic.IDE0040.severity = silent` . Aby uzyskać więcej informacji, zobacz ten problem w serwisie [GitHub](https://github.com/dotnet/roslyn/issues/44201).

> [!TIP]
>
> Począwszy od programu Visual Studio 2019 w wersji 16,3, można skonfigurować reguły stylu kodu z menu żarówki [szybkie akcje](/visualstudio/ide/quick-actions) po wystąpieniu naruszenia stylu. Aby uzyskać więcej informacji, zobacz [Automatyczne konfigurowanie stylów kodu w programie Visual Studio](/visualstudio/ide/editorconfig-language-conventions#automatically-configure-code-styles-in-visual-studio).

## <a name="net-style-rules"></a>Reguły stylu .NET

Reguły stylu w tej sekcji dotyczą zarówno języka C#, jak i Visual Basic.

- [kwalifikatory "this." i "Me."](ide0003-ide0009.md)
  - [dotnet_style_qualification_for_field](ide0003-ide0009.md#dotnet_style_qualification_for_field)
  - [dotnet_style_qualification_for_property](ide0003-ide0009.md#dotnet_style_qualification_for_property)
  - [dotnet_style_qualification_for_method](ide0003-ide0009.md#dotnet_style_qualification_for_method)
  - [dotnet_style_qualification_for_event](ide0003-ide0009.md#dotnet_style_qualification_for_event)
- [Słowa kluczowe języka zamiast nazw typów struktur dla odwołań typu](ide0049.md)
  - [dotnet_style_predefined_type_for_locals_parameters_members](ide0049.md#dotnet_style_predefined_type_for_locals_parameters_members)
  - [dotnet_style_predefined_type_for_member_access](ide0049.md#dotnet_style_predefined_type_for_member_access)
- [Preferencje dotyczące modyfikatorów](modifier-preferences.md#net-modifier-preferences)
  - [dotnet_style_require_accessibility_modifiers](ide0040.md#dotnet_style_require_accessibility_modifiers)
  - [csharp_preferred_modifier_order](ide0036.md#csharp_preferred_modifier_order)
  - [visual_basic_preferred_modifier_order](ide0036.md#visual_basic_preferred_modifier_order)
  - [dotnet_style_readonly_field](ide0044.md#dotnet_style_readonly_field)
- [Preferencje dotyczące nawiasów](ide0047-ide0048.md)
  - [dotnet_style_parentheses_in_arithmetic_binary_operators](ide0047-ide0048.md#dotnet_style_parentheses_in_arithmetic_binary_operators)
  - [dotnet_style_parentheses_in_relational_binary_operators](ide0047-ide0048.md#dotnet_style_parentheses_in_relational_binary_operators)
  - [dotnet_style_parentheses_in_other_binary_operators](ide0047-ide0048.md#dotnet_style_parentheses_in_other_binary_operators)
  - [dotnet_style_parentheses_in_other_operators](ide0047-ide0048.md#dotnet_style_parentheses_in_other_operators)
- [Preferencje na poziomie wyrażeń](expression-level-preferences.md#net-expression-level-preferences)
  - [dotnet_style_object_initializer](ide0017.md#dotnet_style_object_initializer)
  - [dotnet_style_collection_initializer](ide0028.md#dotnet_style_collection_initializer)
  - [dotnet_style_explicit_tuple_names](ide0033.md#dotnet_style_explicit_tuple_names)
  - [dotnet_style_prefer_inferred_tuple_names](ide0037.md#dotnet_style_prefer_inferred_tuple_names)
  - [dotnet_style_prefer_inferred_anonymous_type_member_names](ide0037.md#dotnet_style_prefer_inferred_anonymous_type_member_names)
  - [dotnet_style_prefer_auto_properties](ide0032.md#dotnet_style_prefer_auto_properties)
  - [dotnet_style_prefer_conditional_expression_over_assignment](ide0045.md#dotnet_style_prefer_conditional_expression_over_assignment)
  - [dotnet_style_prefer_conditional_expression_over_return](ide0046.md#dotnet_style_prefer_conditional_expression_over_return)
  - [dotnet_style_prefer_compound_assignment](ide0054-ide0074.md#dotnet_style_prefer_compound_assignment)
  - [dotnet_style_prefer_simplified_interpolation](ide0071.md#dotnet_style_prefer_simplified_interpolation)
  - [dotnet_style_prefer_simplified_boolean_expressions](ide0075.md#dotnet_style_prefer_simplified_boolean_expressions)
  - [Dodaj brakujące przypadki do instrukcji switch](ide0010.md) — ta reguła nie ma opcji stylu kodu.
  - [Konwertuj typ anonimowy na krotkę](ide0050.md) — ta reguła nie ma opcji stylu kodu.
  - [Użyj metody "System. skrótu. Połącz"](ide0070.md) — ta reguła nie ma opcji stylu kodu.
  - [Konwertuj element "typeof" na "nameof"](ide0082.md) — ta reguła nie ma opcji stylu kodu.
- [Preferencje dotyczące sprawdzania wartości null](null-checking-preferences.md#net-null-checking-preferences)
  - [dotnet_style_coalesce_expression](ide0029-ide0030.md#dotnet_style_coalesce_expression)
  - [dotnet_style_null_propagation](ide0031.md#dotnet_style_null_propagation)
  - [dotnet_style_prefer_is_null_check_over_reference_equality_method](ide0041.md#dotnet_style_prefer_is_null_check_over_reference_equality_method)
- [Preferencje nagłówka pliku](ide0073.md)
  - [file_header_template](ide0073.md#file_header_template)

## <a name="c-style-rules"></a>Reguły stylu C#

Reguły stylu w tej sekcji mają zastosowanie tylko do języka C#.

- [Preferencje "var"](ide0007-ide0008.md)
  - [csharp_style_var_for_built_in_types](ide0007-ide0008.md#csharp_style_var_for_built_in_types)
  - [csharp_style_var_when_type_is_apparent](ide0007-ide0008.md#csharp_style_var_when_type_is_apparent)
  - [csharp_style_var_elsewhere](ide0007-ide0008.md#csharp_style_var_elsewhere)
- [Składowe z wyrażeniem w treści](expression-bodied-members.md)
  - [csharp_style_expression_bodied_methods](ide0022.md#csharp_style_expression_bodied_methods)
  - [csharp_style_expression_bodied_constructors](ide0021.md#csharp_style_expression_bodied_constructors)
  - [csharp_style_expression_bodied_operators](ide0023-ide0024.md#csharp_style_expression_bodied_operators)
  - [csharp_style_expression_bodied_properties](ide0025.md#csharp_style_expression_bodied_properties)
  - [csharp_style_expression_bodied_indexers](ide0026.md#csharp_style_expression_bodied_indexers)
  - [csharp_style_expression_bodied_accessors](ide0027.md#csharp_style_expression_bodied_accessors)
  - [csharp_style_expression_bodied_lambdas](ide0053.md#csharp_style_expression_bodied_lambdas)
  - [csharp_style_expression_bodied_local_functions](ide0061.md#csharp_style_expression_bodied_local_functions)
- [Preferencje dopasowywania do wzorca](pattern-matching-preferences.md)
  - [csharp_style_pattern_matching_over_is_with_cast_check](ide0020-ide0038.md#csharp_style_pattern_matching_over_is_with_cast_check)
  - [csharp_style_pattern_matching_over_as_with_null_check](ide0019.md#csharp_style_pattern_matching_over_as_with_null_check)
  - [csharp_style_prefer_switch_expression](ide0066.md#csharp_style_prefer_switch_expression)
  - [csharp_style_prefer_pattern_matching](ide0078.md#csharp_style_prefer_pattern_matching)
  - [csharp_style_prefer_not_pattern](ide0083.md#csharp_style_prefer_not_pattern)
- [Preferencje na poziomie wyrażeń](expression-level-preferences.md#c-expression-level-preferences)
  - [csharp_style_inlined_variable_declaration](ide0018.md#csharp_style_inlined_variable_declaration)
  - [csharp_prefer_simple_default_expression](ide0034.md#csharp_prefer_simple_default_expression)
  - [csharp_style_pattern_local_over_anonymous_function](ide0039.md#csharp_style_pattern_local_over_anonymous_function)
  - [csharp_style_deconstructed_variable_declaration](ide0042.md#csharp_style_deconstructed_variable_declaration)
  - [csharp_style_prefer_index_operator](ide0056.md#csharp_style_prefer_index_operator)
  - [csharp_style_prefer_range_operator](ide0057.md#csharp_style_prefer_range_operator)
  - [csharp_style_implicit_object_creation_when_type_is_apparent](ide0090.md#csharp_style_implicit_object_creation_when_type_is_apparent)
  - [Dodaj brakujące przypadki do przełączenia wyrażenia](ide0072.md) — ta reguła nie ma opcji stylu kodu.
- [Preferencje sprawdzania wartości "null"](null-checking-preferences.md#c-null-checking-preferences)
  - [csharp_style_throw_expression](ide0016.md#csharp_style_throw_expression)
  - [csharp_style_conditional_delegate_call](ide1005.md#csharp_style_conditional_delegate_call)
- [Preferencje dotyczące bloków kodu](code-block-preferences.md)
  - [csharp_prefer_braces](ide0011.md#csharp_prefer_braces)
  - [csharp_prefer_simple_using_statement](ide0063.md#csharp_prefer_simple_using_statement)
- [Preferencje dyrektywy "Using"](ide0065.md)
  - [csharp_using_directive_placement](ide0065.md#csharp_using_directive_placement)
- [Preferencje dotyczące modyfikatorów](modifier-preferences.md#c-modifier-preferences)
  - [csharp_prefer_static_local_function](ide0062.md#csharp_prefer_static_local_function)
  - [Tworzenie pól struktury do zapisu](ide0064.md) — ta reguła nie ma opcji stylu kodu.

## <a name="visual-basic-style-rules"></a>Reguły Visual Basic stylu

Reguły stylu w tej sekcji mają zastosowanie tylko do Visual Basic język.

- [Preferencje dopasowywania do wzorca](pattern-matching-preferences.md)
  - [visual_basic_style_prefer_isnot_expression](ide0084.md#visual_basic_style_prefer_isnot_expression)

## <a name="see-also"></a>Zobacz także

- [Reguły dotyczące zbędnego kodu](unnecessary-code-rules.md)
- [Reguły formatowania](formatting-rules.md)
- [Reguły nazewnictwa](naming-rules.md)
- [Dokumentacja reguł stylu kodu platformy .NET](index.md)
