---
title: Reguły formatowania stylu kodu
description: Zapoznaj się z regułami stylu kodu dotyczącymi formatowania wcięć, spacji i nowych wierszy.
ms.date: 09/25/2020
ms.topic: reference
author: gewarren
ms.author: gewarren
dev_langs:
- CSharp
- VB
f1_keywords:
- IDE0055
- formatting rules
helpviewer_keywords:
- IDE0055
- formatting code style rules [EditorConfig]
- formatting rules
- EditorConfig formatting conventions
ms.openlocfilehash: 61e6f6a6afdc6aaf9710eef3143af8ae700ef612
ms.sourcegitcommit: 636af37170ae75a11c4f7d1ecd770820e7dfe7bd
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/07/2020
ms.locfileid: "96589392"
---
# <a name="formatting-rules"></a><span data-ttu-id="39635-103">Reguły formatowania</span><span class="sxs-lookup"><span data-stu-id="39635-103">Formatting rules</span></span>

<span data-ttu-id="39635-104">Reguły formatowania wpływają na to, jak wcięcia, spacje i nowe wiersze są wyrównane do konstrukcji języka programowania .NET.</span><span class="sxs-lookup"><span data-stu-id="39635-104">Formatting rules affect how indentation, spaces, and new lines are aligned around .NET programming language constructs.</span></span> <span data-ttu-id="39635-105">Reguły są uwzględniane w następujących kategoriach:</span><span class="sxs-lookup"><span data-stu-id="39635-105">The rules fall into the following categories:</span></span>

- <span data-ttu-id="39635-106">[Reguły formatowania platformy .NET](#net-formatting-rules): reguły, które mają zastosowanie do języka C# i Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="39635-106">[.NET formatting rules](#net-formatting-rules): Rules that apply to both C# and Visual Basic.</span></span> <span data-ttu-id="39635-107">Nazwy opcji EditorConfig dla tych reguł zaczynają się od `dotnet_` prefiksu.</span><span class="sxs-lookup"><span data-stu-id="39635-107">The EditorConfig option names for these rules start with `dotnet_` prefix.</span></span>
- <span data-ttu-id="39635-108">[Reguły formatowania języka c#](#c-formatting-rules): reguły, które są specyficzne tylko dla języka C#.</span><span class="sxs-lookup"><span data-stu-id="39635-108">[C# formatting rules](#c-formatting-rules): Rules that are specific to C# language only.</span></span> <span data-ttu-id="39635-109">Nazwy opcji EditorConfig dla tych reguł zaczynają się od `csharp_` prefiksu.</span><span class="sxs-lookup"><span data-stu-id="39635-109">The EditorConfig option names for these rules start with `csharp_` prefix.</span></span>

## <a name="rule-id-ide0055-fix-formatting"></a><span data-ttu-id="39635-110">Identyfikator reguły: "IDE0055" (Popraw formatowanie)</span><span class="sxs-lookup"><span data-stu-id="39635-110">Rule ID: "IDE0055" (Fix formatting)</span></span>

<span data-ttu-id="39635-111">Wszystkie opcje formatowania mają identyfikator `IDE0055` i tytuł reguły `Fix formatting` .</span><span class="sxs-lookup"><span data-stu-id="39635-111">All formatting options have rule ID `IDE0055` and title `Fix formatting`.</span></span> <span data-ttu-id="39635-112">Ustaw ważność naruszenia formatowania w pliku EditorConfig przy użyciu następującego wiersza konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="39635-112">Set the severity of a formatting violation in an EditorConfig file using the following configuration line.</span></span>

```ini
dotnet_diagnostic.IDE0055.severity = <severity value>
```

<span data-ttu-id="39635-113">Wartość ważności musi być `warning` `error` [wymuszana w kompilacji](../overview.md#code-style-analysis).</span><span class="sxs-lookup"><span data-stu-id="39635-113">The severity value must be `warning` or `error` to be [enforced on build](../overview.md#code-style-analysis).</span></span> <span data-ttu-id="39635-114">Dla wszystkich możliwych wartości ważności zobacz [poziom ważności](../configuration-options.md#severity-level).</span><span class="sxs-lookup"><span data-stu-id="39635-114">For all possible severity values, see [severity level](../configuration-options.md#severity-level).</span></span>

## <a name="option-format"></a><span data-ttu-id="39635-115">Format opcji</span><span class="sxs-lookup"><span data-stu-id="39635-115">Option format</span></span>

<span data-ttu-id="39635-116">Opcje formatowania reguł można określić w pliku EditorConfig o następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="39635-116">Options for formatting rules can be specified in an EditorConfig file with the following format:</span></span>

`rule_name = value`

<span data-ttu-id="39635-117">W przypadku wielu reguł należy określić jeden `true` (Preferuj ten styl) lub `false` (nie Preferuj tego stylu) dla `value` .</span><span class="sxs-lookup"><span data-stu-id="39635-117">For many rules, you specify either `true` (prefer this style) or `false` (do not prefer this style) for `value`.</span></span> <span data-ttu-id="39635-118">W przypadku innych reguł należy określić wartość taką jak `flush_left` lub, `before_and_after` aby opisać, kiedy i gdzie należy zastosować regułę.</span><span class="sxs-lookup"><span data-stu-id="39635-118">For other rules, you specify a value such as `flush_left` or `before_and_after` to describe when and where to apply the rule.</span></span> <span data-ttu-id="39635-119">Nie określisz ważności.</span><span class="sxs-lookup"><span data-stu-id="39635-119">You don't specify a severity.</span></span>

## <a name="net-formatting-rules"></a><span data-ttu-id="39635-120">Reguły formatowania platformy .NET</span><span class="sxs-lookup"><span data-stu-id="39635-120">.NET formatting rules</span></span>

<span data-ttu-id="39635-121">Reguły formatowania w tej sekcji dotyczą zarówno języka C#, jak i Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="39635-121">The formatting rules in this section apply to both C# and Visual Basic.</span></span>

- [<span data-ttu-id="39635-122">Organizuj użycia</span><span class="sxs-lookup"><span data-stu-id="39635-122">Organize usings</span></span>](#organize-using-directives)
  - <span data-ttu-id="39635-123">dotnet_sort_system_directives_first</span><span class="sxs-lookup"><span data-stu-id="39635-123">dotnet_sort_system_directives_first</span></span>
  - <span data-ttu-id="39635-124">dotnet_separate_import_directive_groups</span><span class="sxs-lookup"><span data-stu-id="39635-124">dotnet_separate_import_directive_groups</span></span>

### <a name="organize-using-directives"></a><span data-ttu-id="39635-125">Organizuj dyrektywy using</span><span class="sxs-lookup"><span data-stu-id="39635-125">Organize using directives</span></span>

<span data-ttu-id="39635-126">Te reguły formatowania dotyczą sortowania i wyświetlania `using` dyrektyw i `Imports` instrukcji.</span><span class="sxs-lookup"><span data-stu-id="39635-126">These formatting rules concern the sorting and display of `using` directives and `Imports` statements.</span></span>

<span data-ttu-id="39635-127">Przykładowy plik *. editorconfig* :</span><span class="sxs-lookup"><span data-stu-id="39635-127">Example *.editorconfig* file:</span></span>

```ini
# .NET formatting rules
[*.{cs,vb}]
dotnet_sort_system_directives_first = true
dotnet_separate_import_directive_groups = true
```

#### <a name="dotnet_sort_system_directives_first"></a><span data-ttu-id="39635-128">\_ \_ directives_first systemu sortowania \_ dotnet</span><span class="sxs-lookup"><span data-stu-id="39635-128">dotnet\_sort\_system\_directives_first</span></span>

|<span data-ttu-id="39635-129">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-129">Property</span></span>|<span data-ttu-id="39635-130">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-130">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-131">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-131">**Option name**</span></span> | <span data-ttu-id="39635-132">dotnet_sort_system_directives_first</span><span class="sxs-lookup"><span data-stu-id="39635-132">dotnet_sort_system_directives_first</span></span> |
| <span data-ttu-id="39635-133">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-133">**Applicable languages**</span></span> | <span data-ttu-id="39635-134">C# i Visual Basic</span><span class="sxs-lookup"><span data-stu-id="39635-134">C# and Visual Basic</span></span> |
| <span data-ttu-id="39635-135">**Wprowadzona wersja**</span><span class="sxs-lookup"><span data-stu-id="39635-135">**Introduced version**</span></span> | <span data-ttu-id="39635-136">Visual Studio 2017, wersja 15.3</span><span class="sxs-lookup"><span data-stu-id="39635-136">Visual Studio 2017 version 15.3</span></span> |
| <span data-ttu-id="39635-137">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-137">**Option values**</span></span> | <span data-ttu-id="39635-138">`true` -Sortuj `System.*` `using` dyrektywy alfabetycznie i umieść je przed innymi przy użyciu dyrektyw.</span><span class="sxs-lookup"><span data-stu-id="39635-138">`true` - Sort `System.*` `using` directives alphabetically, and place them before other using directives.</span></span><br /><br /><span data-ttu-id="39635-139">`false` — Nie należy umieszczać `System.*` `using` dyrektyw przed innymi `using` dyrektywami.</span><span class="sxs-lookup"><span data-stu-id="39635-139">`false` - Do not place `System.*` `using` directives before other `using` directives.</span></span> |

<span data-ttu-id="39635-140">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-140">Code examples:</span></span>

```csharp
// dotnet_sort_system_directives_first = true
using System.Collections.Generic;
using System.Threading.Tasks;
using Octokit;

// dotnet_sort_system_directives_first = false
using System.Collections.Generic;
using Octokit;
using System.Threading.Tasks;
```

#### <a name="dotnet_separate_import_directive_groups"></a><span data-ttu-id="39635-141">\_ \_ \_ grupy dyrektywy dotyczącej importowania oddzielnych dotnet \_</span><span class="sxs-lookup"><span data-stu-id="39635-141">dotnet\_separate\_import\_directive\_groups</span></span>

|<span data-ttu-id="39635-142">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-142">Property</span></span>|<span data-ttu-id="39635-143">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-143">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-144">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-144">**Option name**</span></span> | <span data-ttu-id="39635-145">dotnet_separate_import_directive_groups</span><span class="sxs-lookup"><span data-stu-id="39635-145">dotnet_separate_import_directive_groups</span></span> |
| <span data-ttu-id="39635-146">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-146">**Applicable languages**</span></span> | <span data-ttu-id="39635-147">C# i Visual Basic</span><span class="sxs-lookup"><span data-stu-id="39635-147">C# and Visual Basic</span></span> |
| <span data-ttu-id="39635-148">**Wprowadzona wersja**</span><span class="sxs-lookup"><span data-stu-id="39635-148">**Introduced version**</span></span> | <span data-ttu-id="39635-149">Visual Studio 2017, wersja 15.5</span><span class="sxs-lookup"><span data-stu-id="39635-149">Visual Studio 2017 version 15.5</span></span> |
| <span data-ttu-id="39635-150">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-150">**Option values**</span></span> | <span data-ttu-id="39635-151">`true` — Należy umieścić pusty wiersz między `using` grupami dyrektyw.</span><span class="sxs-lookup"><span data-stu-id="39635-151">`true` - Place a blank line between `using` directive groups.</span></span><br /><br /><span data-ttu-id="39635-152">`false` — Nie umieszczaj pustego wiersza między `using` grupami dyrektyw.</span><span class="sxs-lookup"><span data-stu-id="39635-152">`false` - Do not place a blank line between `using` directive groups.</span></span> |

<span data-ttu-id="39635-153">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-153">Code examples:</span></span>

```csharp
// dotnet_separate_import_directive_groups = true
using System.Collections.Generic;
using System.Threading.Tasks;

using Octokit;

// dotnet_separate_import_directive_groups = false
using System.Collections.Generic;
using System.Threading.Tasks;
using Octokit;
```

## <a name="c-formatting-rules"></a><span data-ttu-id="39635-154">Reguły formatowania języka C#</span><span class="sxs-lookup"><span data-stu-id="39635-154">C# formatting rules</span></span>

<span data-ttu-id="39635-155">Reguły formatowania w tej sekcji dotyczą tylko kodu w języku C#.</span><span class="sxs-lookup"><span data-stu-id="39635-155">The formatting rules in this section apply only to C# code.</span></span>

- [<span data-ttu-id="39635-156">Opcje nowego wiersza</span><span class="sxs-lookup"><span data-stu-id="39635-156">Newline options</span></span>](#new-line-options)
  - <span data-ttu-id="39635-157">csharp_new_line_before_open_brace</span><span class="sxs-lookup"><span data-stu-id="39635-157">csharp_new_line_before_open_brace</span></span>
  - <span data-ttu-id="39635-158">csharp_new_line_before_else</span><span class="sxs-lookup"><span data-stu-id="39635-158">csharp_new_line_before_else</span></span>
  - <span data-ttu-id="39635-159">csharp_new_line_before_catch</span><span class="sxs-lookup"><span data-stu-id="39635-159">csharp_new_line_before_catch</span></span>
  - <span data-ttu-id="39635-160">csharp_new_line_before_finally</span><span class="sxs-lookup"><span data-stu-id="39635-160">csharp_new_line_before_finally</span></span>
  - <span data-ttu-id="39635-161">csharp_new_line_before_members_in_object_initializers</span><span class="sxs-lookup"><span data-stu-id="39635-161">csharp_new_line_before_members_in_object_initializers</span></span>
  - <span data-ttu-id="39635-162">csharp_new_line_before_members_in_anonymous_types</span><span class="sxs-lookup"><span data-stu-id="39635-162">csharp_new_line_before_members_in_anonymous_types</span></span>
  - <span data-ttu-id="39635-163">csharp_new_line_between_query_expression_clauses</span><span class="sxs-lookup"><span data-stu-id="39635-163">csharp_new_line_between_query_expression_clauses</span></span>
- [<span data-ttu-id="39635-164">Opcje wcięć</span><span class="sxs-lookup"><span data-stu-id="39635-164">Indentation options</span></span>](#indentation-options)
  - <span data-ttu-id="39635-165">csharp_indent_case_contents</span><span class="sxs-lookup"><span data-stu-id="39635-165">csharp_indent_case_contents</span></span>
  - <span data-ttu-id="39635-166">csharp_indent_switch_labels</span><span class="sxs-lookup"><span data-stu-id="39635-166">csharp_indent_switch_labels</span></span>
  - <span data-ttu-id="39635-167">csharp_indent_labels</span><span class="sxs-lookup"><span data-stu-id="39635-167">csharp_indent_labels</span></span>
  - <span data-ttu-id="39635-168">csharp_indent_block_contents</span><span class="sxs-lookup"><span data-stu-id="39635-168">csharp_indent_block_contents</span></span>
  - <span data-ttu-id="39635-169">csharp_indent_braces</span><span class="sxs-lookup"><span data-stu-id="39635-169">csharp_indent_braces</span></span>
  - <span data-ttu-id="39635-170">csharp_indent_case_contents_when_block</span><span class="sxs-lookup"><span data-stu-id="39635-170">csharp_indent_case_contents_when_block</span></span>
- [<span data-ttu-id="39635-171">Opcje odstępów</span><span class="sxs-lookup"><span data-stu-id="39635-171">Spacing options</span></span>](#spacing-options)
  - <span data-ttu-id="39635-172">csharp_space_after_cast</span><span class="sxs-lookup"><span data-stu-id="39635-172">csharp_space_after_cast</span></span>
  - <span data-ttu-id="39635-173">csharp_space_after_keywords_in_control_flow_statements</span><span class="sxs-lookup"><span data-stu-id="39635-173">csharp_space_after_keywords_in_control_flow_statements</span></span>
  - <span data-ttu-id="39635-174">csharp_space_between_parentheses</span><span class="sxs-lookup"><span data-stu-id="39635-174">csharp_space_between_parentheses</span></span>
  - <span data-ttu-id="39635-175">csharp_space_before_colon_in_inheritance_clause</span><span class="sxs-lookup"><span data-stu-id="39635-175">csharp_space_before_colon_in_inheritance_clause</span></span>
  - <span data-ttu-id="39635-176">csharp_space_after_colon_in_inheritance_clause</span><span class="sxs-lookup"><span data-stu-id="39635-176">csharp_space_after_colon_in_inheritance_clause</span></span>
  - <span data-ttu-id="39635-177">csharp_space_around_binary_operators</span><span class="sxs-lookup"><span data-stu-id="39635-177">csharp_space_around_binary_operators</span></span>
  - <span data-ttu-id="39635-178">csharp_space_between_method_declaration_parameter_list_parentheses</span><span class="sxs-lookup"><span data-stu-id="39635-178">csharp_space_between_method_declaration_parameter_list_parentheses</span></span>
  - <span data-ttu-id="39635-179">csharp_space_between_method_declaration_empty_parameter_list_parentheses</span><span class="sxs-lookup"><span data-stu-id="39635-179">csharp_space_between_method_declaration_empty_parameter_list_parentheses</span></span>
  - <span data-ttu-id="39635-180">csharp_space_between_method_declaration_name_and_open_parenthesis</span><span class="sxs-lookup"><span data-stu-id="39635-180">csharp_space_between_method_declaration_name_and_open_parenthesis</span></span>
  - <span data-ttu-id="39635-181">csharp_space_between_method_call_parameter_list_parentheses</span><span class="sxs-lookup"><span data-stu-id="39635-181">csharp_space_between_method_call_parameter_list_parentheses</span></span>
  - <span data-ttu-id="39635-182">csharp_space_between_method_call_empty_parameter_list_parentheses</span><span class="sxs-lookup"><span data-stu-id="39635-182">csharp_space_between_method_call_empty_parameter_list_parentheses</span></span>
  - <span data-ttu-id="39635-183">csharp_space_between_method_call_name_and_opening_parenthesis</span><span class="sxs-lookup"><span data-stu-id="39635-183">csharp_space_between_method_call_name_and_opening_parenthesis</span></span>
  - <span data-ttu-id="39635-184">csharp_space_after_comma</span><span class="sxs-lookup"><span data-stu-id="39635-184">csharp_space_after_comma</span></span>
  - <span data-ttu-id="39635-185">csharp_space_before_comma</span><span class="sxs-lookup"><span data-stu-id="39635-185">csharp_space_before_comma</span></span>
  - <span data-ttu-id="39635-186">csharp_space_after_dot</span><span class="sxs-lookup"><span data-stu-id="39635-186">csharp_space_after_dot</span></span>
  - <span data-ttu-id="39635-187">csharp_space_before_dot</span><span class="sxs-lookup"><span data-stu-id="39635-187">csharp_space_before_dot</span></span>
  - <span data-ttu-id="39635-188">csharp_space_after_semicolon_in_for_statement</span><span class="sxs-lookup"><span data-stu-id="39635-188">csharp_space_after_semicolon_in_for_statement</span></span>
  - <span data-ttu-id="39635-189">csharp_space_before_semicolon_in_for_statement</span><span class="sxs-lookup"><span data-stu-id="39635-189">csharp_space_before_semicolon_in_for_statement</span></span>
  - <span data-ttu-id="39635-190">csharp_space_around_declaration_statements</span><span class="sxs-lookup"><span data-stu-id="39635-190">csharp_space_around_declaration_statements</span></span>
  - <span data-ttu-id="39635-191">csharp_space_before_open_square_brackets</span><span class="sxs-lookup"><span data-stu-id="39635-191">csharp_space_before_open_square_brackets</span></span>
  - <span data-ttu-id="39635-192">csharp_space_between_empty_square_brackets</span><span class="sxs-lookup"><span data-stu-id="39635-192">csharp_space_between_empty_square_brackets</span></span>
  - <span data-ttu-id="39635-193">csharp_space_between_square_brackets</span><span class="sxs-lookup"><span data-stu-id="39635-193">csharp_space_between_square_brackets</span></span>
- [<span data-ttu-id="39635-194">Opcje zawijania</span><span class="sxs-lookup"><span data-stu-id="39635-194">Wrap options</span></span>](#wrap-options)
  - <span data-ttu-id="39635-195">csharp_preserve_single_line_statements</span><span class="sxs-lookup"><span data-stu-id="39635-195">csharp_preserve_single_line_statements</span></span>
  - <span data-ttu-id="39635-196">csharp_preserve_single_line_blocks</span><span class="sxs-lookup"><span data-stu-id="39635-196">csharp_preserve_single_line_blocks</span></span>
- [<span data-ttu-id="39635-197">Korzystanie z opcji dyrektywy</span><span class="sxs-lookup"><span data-stu-id="39635-197">Using directive options</span></span>](#using-directive-options)
  - <span data-ttu-id="39635-198">csharp_using_directive_placement</span><span class="sxs-lookup"><span data-stu-id="39635-198">csharp_using_directive_placement</span></span>

### <a name="new-line-options"></a><span data-ttu-id="39635-199">Opcje nowego wiersza</span><span class="sxs-lookup"><span data-stu-id="39635-199">New-line options</span></span>

<span data-ttu-id="39635-200">Te reguły formatowania dotyczą korzystania z nowych wierszy do formatowania kodu.</span><span class="sxs-lookup"><span data-stu-id="39635-200">These formatting rules concern the use of new lines to format code.</span></span>

<span data-ttu-id="39635-201">Przykładowy plik *. editorconfig* :</span><span class="sxs-lookup"><span data-stu-id="39635-201">Example *.editorconfig* file:</span></span>

```ini
# CSharp formatting rules:
[*.cs]
csharp_new_line_before_open_brace = methods, properties, control_blocks, types
csharp_new_line_before_else = true
csharp_new_line_before_catch = true
csharp_new_line_before_finally = true
csharp_new_line_before_members_in_object_initializers = true
csharp_new_line_before_members_in_anonymous_types = true
csharp_new_line_between_query_expression_clauses = true
```

#### <a name="csharp_new_line_before_open_brace"></a><span data-ttu-id="39635-202">CSharp \_ Nowy \_ wiersz \_ przed \_ open_brace</span><span class="sxs-lookup"><span data-stu-id="39635-202">csharp\_new\_line\_before\_open_brace</span></span>

<span data-ttu-id="39635-203">Ta zasada ma wpływ na to, czy otwierający nawias klamrowy `{` powinien być umieszczony w tym samym wierszu co poprzedni kod, czy w nowym wierszu.</span><span class="sxs-lookup"><span data-stu-id="39635-203">This rule concerns whether an open brace `{` should be placed on the same line as the preceding code, or on a new line.</span></span> <span data-ttu-id="39635-204">Dla tej reguły należy określić **wszystkie**, **Brak** lub co najmniej jeden element kodu, taki jak **metody** lub **Właściwości**, aby określić, kiedy ta reguła ma być stosowana.</span><span class="sxs-lookup"><span data-stu-id="39635-204">For this rule, you specify **all**, **none**, or one or more code elements such as **methods** or **properties**, to define when this rule should be applied.</span></span> <span data-ttu-id="39635-205">Aby określić wiele elementów kodu, rozdziel je przecinkami (,).</span><span class="sxs-lookup"><span data-stu-id="39635-205">To specify multiple code elements, separate them with a comma (,).</span></span>

|<span data-ttu-id="39635-206">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-206">Property</span></span>|<span data-ttu-id="39635-207">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-207">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-208">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-208">**Option name**</span></span> | <span data-ttu-id="39635-209">csharp_new_line_before_open_brace</span><span class="sxs-lookup"><span data-stu-id="39635-209">csharp_new_line_before_open_brace</span></span> |
| <span data-ttu-id="39635-210">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-210">**Applicable languages**</span></span> | <span data-ttu-id="39635-211">C#</span><span class="sxs-lookup"><span data-stu-id="39635-211">C#</span></span> |
| <span data-ttu-id="39635-212">**Wprowadzona wersja**</span><span class="sxs-lookup"><span data-stu-id="39635-212">**Introduced version**</span></span> | <span data-ttu-id="39635-213">Visual Studio 2017, wersja 15.3</span><span class="sxs-lookup"><span data-stu-id="39635-213">Visual Studio 2017 version 15.3</span></span> |
| <span data-ttu-id="39635-214">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-214">**Option values**</span></span> | <span data-ttu-id="39635-215">`all` -Wymagaj nawiasów klamrowych w nowym wierszu dla wszystkich wyrażeń (styl "Allman").</span><span class="sxs-lookup"><span data-stu-id="39635-215">`all` - Require braces to be on a new line for all expressions ("Allman" style).</span></span><br /><br /><span data-ttu-id="39635-216">`none` -Wymagaj nawiasów klamrowych w tym samym wierszu dla wszystkich wyrażeń ("K&R").</span><span class="sxs-lookup"><span data-stu-id="39635-216">`none` - Require braces to be on the same line for all expressions ("K&R").</span></span><br /><br /><span data-ttu-id="39635-217">`accessors`,,,,,,,,,, `anonymous_methods` `anonymous_types` `control_blocks` `events` `indexers` `lambdas` `local_functions` `methods` `object_collection_array_initializers` `properties` , `types` — Wymagaj nawiasów klamrowych, aby znajdować się w nowym wierszu dla określonego elementu kodu (styl "Allman").</span><span class="sxs-lookup"><span data-stu-id="39635-217">`accessors`, `anonymous_methods`, `anonymous_types`, `control_blocks`, `events`, `indexers`, `lambdas`, `local_functions`, `methods`, `object_collection_array_initializers`, `properties`, `types` - Require braces to be on a new line for the specified code element ("Allman" style).</span></span> |

<span data-ttu-id="39635-218">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-218">Code examples:</span></span>

```csharp
// csharp_new_line_before_open_brace = all
void MyMethod()
{
    if (...)
    {
        ...
    }
}

// csharp_new_line_before_open_brace = none
void MyMethod() {
    if (...) {
        ...
    }
}
```

#### <a name="csharp_new_line_before_else"></a><span data-ttu-id="39635-219">CSharp \_ Nowy \_ wiersz \_ before_else</span><span class="sxs-lookup"><span data-stu-id="39635-219">csharp\_new\_line\_before_else</span></span>

|<span data-ttu-id="39635-220">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-220">Property</span></span>|<span data-ttu-id="39635-221">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-221">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-222">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-222">**Option name**</span></span> | <span data-ttu-id="39635-223">csharp_new_line_before_else</span><span class="sxs-lookup"><span data-stu-id="39635-223">csharp_new_line_before_else</span></span> |
| <span data-ttu-id="39635-224">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-224">**Applicable languages**</span></span> | <span data-ttu-id="39635-225">C#</span><span class="sxs-lookup"><span data-stu-id="39635-225">C#</span></span> |
| <span data-ttu-id="39635-226">**Wprowadzona wersja**</span><span class="sxs-lookup"><span data-stu-id="39635-226">**Introduced version**</span></span> | <span data-ttu-id="39635-227">Visual Studio 2017, wersja 15.3</span><span class="sxs-lookup"><span data-stu-id="39635-227">Visual Studio 2017 version 15.3</span></span> |
| <span data-ttu-id="39635-228">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-228">**Option values**</span></span> | <span data-ttu-id="39635-229">`true` -Umieść `else` instrukcje w nowym wierszu.</span><span class="sxs-lookup"><span data-stu-id="39635-229">`true` - Place `else` statements on a new line.</span></span><br /><br /><span data-ttu-id="39635-230">`false` -Umieść `else` instrukcje w tym samym wierszu.</span><span class="sxs-lookup"><span data-stu-id="39635-230">`false` - Place `else` statements on the same line.</span></span> |

<span data-ttu-id="39635-231">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-231">Code examples:</span></span>

```csharp
// csharp_new_line_before_else = true
if (...) {
    ...
}
else {
    ...
}

// csharp_new_line_before_else = false
if (...) {
    ...
} else {
    ...
}
```

#### <a name="csharp_new_line_before_catch"></a><span data-ttu-id="39635-232">CSharp \_ Nowy \_ wiersz \_ before_catch</span><span class="sxs-lookup"><span data-stu-id="39635-232">csharp\_new\_line\_before_catch</span></span>

|<span data-ttu-id="39635-233">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-233">Property</span></span>|<span data-ttu-id="39635-234">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-234">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-235">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-235">**Option name**</span></span> | <span data-ttu-id="39635-236">csharp_new_line_before_catch</span><span class="sxs-lookup"><span data-stu-id="39635-236">csharp_new_line_before_catch</span></span> |
| <span data-ttu-id="39635-237">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-237">**Applicable languages**</span></span> | <span data-ttu-id="39635-238">C#</span><span class="sxs-lookup"><span data-stu-id="39635-238">C#</span></span> |
| <span data-ttu-id="39635-239">**Wprowadzona wersja**</span><span class="sxs-lookup"><span data-stu-id="39635-239">**Introduced version**</span></span> | <span data-ttu-id="39635-240">Visual Studio 2017, wersja 15.3</span><span class="sxs-lookup"><span data-stu-id="39635-240">Visual Studio 2017 version 15.3</span></span> |
| <span data-ttu-id="39635-241">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-241">**Option values**</span></span> | <span data-ttu-id="39635-242">`true` -Umieść `catch` instrukcje w nowym wierszu.</span><span class="sxs-lookup"><span data-stu-id="39635-242">`true` - Place `catch` statements on a new line.</span></span><br /><br /><span data-ttu-id="39635-243">`false` -Umieść `catch` instrukcje w tym samym wierszu.</span><span class="sxs-lookup"><span data-stu-id="39635-243">`false` - Place `catch` statements on the same line.</span></span> |

<span data-ttu-id="39635-244">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-244">Code examples:</span></span>

```csharp
// csharp_new_line_before_catch = true
try {
    ...
}
catch (Exception e) {
    ...
}

// csharp_new_line_before_catch = false
try {
    ...
} catch (Exception e) {
    ...
}
```

#### <a name="csharp_new_line_before_finally"></a><span data-ttu-id="39635-245">CSharp \_ Nowy \_ wiersz \_ before_finally</span><span class="sxs-lookup"><span data-stu-id="39635-245">csharp\_new\_line\_before_finally</span></span>

|<span data-ttu-id="39635-246">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-246">Property</span></span>|<span data-ttu-id="39635-247">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-247">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-248">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-248">**Option name**</span></span> | <span data-ttu-id="39635-249">csharp_new_line_before_finally</span><span class="sxs-lookup"><span data-stu-id="39635-249">csharp_new_line_before_finally</span></span> |
| <span data-ttu-id="39635-250">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-250">**Applicable languages**</span></span> | <span data-ttu-id="39635-251">C#</span><span class="sxs-lookup"><span data-stu-id="39635-251">C#</span></span> |
| <span data-ttu-id="39635-252">**Wprowadzona wersja**</span><span class="sxs-lookup"><span data-stu-id="39635-252">**Introduced version**</span></span> | <span data-ttu-id="39635-253">Visual Studio 2017, wersja 15.3</span><span class="sxs-lookup"><span data-stu-id="39635-253">Visual Studio 2017 version 15.3</span></span> |
| <span data-ttu-id="39635-254">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-254">**Option values**</span></span> | <span data-ttu-id="39635-255">`true` -Wymagaj `finally` instrukcji w nowym wierszu po nawiasie zamykającym.</span><span class="sxs-lookup"><span data-stu-id="39635-255">`true` - Require `finally` statements to be on a new line after the closing brace.</span></span><br /><br /><span data-ttu-id="39635-256">`false` -Wymagaj `finally` instrukcji w tym samym wierszu co zamykający nawias klamrowy.</span><span class="sxs-lookup"><span data-stu-id="39635-256">`false` - Require `finally` statements to be on the same line as the closing brace.</span></span> |

<span data-ttu-id="39635-257">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-257">Code examples:</span></span>

```csharp
// csharp_new_line_before_finally = true
try {
    ...
}
catch (Exception e) {
    ...
}
finally {
    ...
}

// csharp_new_line_before_finally = false
try {
    ...
} catch (Exception e) {
    ...
} finally {
    ...
}
```

#### <a name="csharp_new_line_before_members_in_object_initializers"></a><span data-ttu-id="39635-258">CSharp \_ Nowy \_ wiersz \_ przed \_ elementami członkowskimi \_ w \_ object_initializers</span><span class="sxs-lookup"><span data-stu-id="39635-258">csharp\_new\_line\_before\_members\_in\_object_initializers</span></span>

|<span data-ttu-id="39635-259">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-259">Property</span></span>|<span data-ttu-id="39635-260">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-260">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-261">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-261">**Option name**</span></span> | <span data-ttu-id="39635-262">csharp_new_line_before_members_in_object_initializers</span><span class="sxs-lookup"><span data-stu-id="39635-262">csharp_new_line_before_members_in_object_initializers</span></span> |
| <span data-ttu-id="39635-263">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-263">**Applicable languages**</span></span> | <span data-ttu-id="39635-264">C#</span><span class="sxs-lookup"><span data-stu-id="39635-264">C#</span></span> |
| <span data-ttu-id="39635-265">**Wprowadzona wersja**</span><span class="sxs-lookup"><span data-stu-id="39635-265">**Introduced version**</span></span> | <span data-ttu-id="39635-266">Visual Studio 2017, wersja 15.3</span><span class="sxs-lookup"><span data-stu-id="39635-266">Visual Studio 2017 version 15.3</span></span> |
| <span data-ttu-id="39635-267">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-267">**Option values**</span></span> | <span data-ttu-id="39635-268">`true` -Wymagane składowe inicjatorów obiektów muszą znajdować się w osobnych wierszach</span><span class="sxs-lookup"><span data-stu-id="39635-268">`true` - Require members of object initializers to be on separate lines</span></span><br /><br /><span data-ttu-id="39635-269">`false` -Wymagane składowe inicjatorów obiektów powinny znajdować się w tym samym wierszu</span><span class="sxs-lookup"><span data-stu-id="39635-269">`false` - Require members of object initializers to be on the same line</span></span> |

<span data-ttu-id="39635-270">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-270">Code examples:</span></span>

```csharp
// csharp_new_line_before_members_in_object_initializers = true
var z = new B()
{
    A = 3,
    B = 4
}

// csharp_new_line_before_members_in_object_initializers = false
var z = new B()
{
    A = 3, B = 4
}
```

#### <a name="csharp_new_line_before_members_in_anonymous_types"></a><span data-ttu-id="39635-271">CSharp \_ Nowy \_ wiersz \_ przed \_ elementami członkowskimi \_ w \_ anonymous_types</span><span class="sxs-lookup"><span data-stu-id="39635-271">csharp\_new\_line\_before\_members\_in\_anonymous_types</span></span>

|<span data-ttu-id="39635-272">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-272">Property</span></span>|<span data-ttu-id="39635-273">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-273">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-274">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-274">**Option name**</span></span> | <span data-ttu-id="39635-275">csharp_new_line_before_members_in_anonymous_types</span><span class="sxs-lookup"><span data-stu-id="39635-275">csharp_new_line_before_members_in_anonymous_types</span></span> |
| <span data-ttu-id="39635-276">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-276">**Applicable languages**</span></span> | <span data-ttu-id="39635-277">C#</span><span class="sxs-lookup"><span data-stu-id="39635-277">C#</span></span> |
| <span data-ttu-id="39635-278">**Wprowadzona wersja**</span><span class="sxs-lookup"><span data-stu-id="39635-278">**Introduced version**</span></span> | <span data-ttu-id="39635-279">Visual Studio 2017, wersja 15.3</span><span class="sxs-lookup"><span data-stu-id="39635-279">Visual Studio 2017 version 15.3</span></span> |
| <span data-ttu-id="39635-280">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-280">**Option values**</span></span> | <span data-ttu-id="39635-281">`true` -Wymagaj elementów członkowskich typu anonimowego w osobnych wierszach</span><span class="sxs-lookup"><span data-stu-id="39635-281">`true` - Require members of anonymous types to be on separate lines</span></span><br /><br /><span data-ttu-id="39635-282">`false` -Wymagane składowe typów anonimowych mogą znajdować się w tym samym wierszu</span><span class="sxs-lookup"><span data-stu-id="39635-282">`false` - Require members of anonymous types to be on the same line</span></span> |

<span data-ttu-id="39635-283">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-283">Code examples:</span></span>

```csharp
// csharp_new_line_before_members_in_anonymous_types = true
var z = new
{
    A = 3,
    B = 4
}

// csharp_new_line_before_members_in_anonymous_types = false
var z = new
{
    A = 3, B = 4
}
```

#### <a name="csharp_new_line_between_query_expression_clauses"></a><span data-ttu-id="39635-284">csharp_new_line_between_query_expression_clauses</span><span class="sxs-lookup"><span data-stu-id="39635-284">csharp_new_line_between_query_expression_clauses</span></span>

|<span data-ttu-id="39635-285">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-285">Property</span></span>|<span data-ttu-id="39635-286">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-286">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-287">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-287">**Option name**</span></span> | <span data-ttu-id="39635-288">csharp_new_line_between_query_expression_clauses</span><span class="sxs-lookup"><span data-stu-id="39635-288">csharp_new_line_between_query_expression_clauses</span></span> |
| <span data-ttu-id="39635-289">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-289">**Applicable languages**</span></span> | <span data-ttu-id="39635-290">C#</span><span class="sxs-lookup"><span data-stu-id="39635-290">C#</span></span> |
| <span data-ttu-id="39635-291">**Wprowadzona wersja**</span><span class="sxs-lookup"><span data-stu-id="39635-291">**Introduced version**</span></span> | <span data-ttu-id="39635-292">Visual Studio 2017, wersja 15.3</span><span class="sxs-lookup"><span data-stu-id="39635-292">Visual Studio 2017 version 15.3</span></span> |
| <span data-ttu-id="39635-293">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-293">**Option values**</span></span> | <span data-ttu-id="39635-294">`true` -Wymagaj elementów klauzul wyrażeń zapytania w osobnych wierszach</span><span class="sxs-lookup"><span data-stu-id="39635-294">`true` - Require elements of query expression clauses to be on separate lines</span></span><br /><br /><span data-ttu-id="39635-295">`false` -Wymagaj elementów klauzul wyrażeń zapytania, aby znajdować się w tym samym wierszu</span><span class="sxs-lookup"><span data-stu-id="39635-295">`false` - Require elements of query expression clauses to be on the same line</span></span> |

<span data-ttu-id="39635-296">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-296">Code examples:</span></span>

```csharp
// csharp_new_line_between_query_expression_clauses = true
var q = from a in e
        from b in e
        select a * b;

// csharp_new_line_between_query_expression_clauses = false
var q = from a in e from b in e
        select a * b;
```

### <a name="indentation-options"></a><span data-ttu-id="39635-297">Opcje wcięć</span><span class="sxs-lookup"><span data-stu-id="39635-297">Indentation options</span></span>

<span data-ttu-id="39635-298">Te reguły formatowania dotyczą użycia wcięć do formatowania kodu.</span><span class="sxs-lookup"><span data-stu-id="39635-298">These formatting rules concern the use of indentation to format code.</span></span>

<span data-ttu-id="39635-299">Przykładowy plik *. editorconfig* :</span><span class="sxs-lookup"><span data-stu-id="39635-299">Example *.editorconfig* file:</span></span>

```ini
# CSharp formatting rules:
[*.cs]
csharp_indent_case_contents = true
csharp_indent_switch_labels = true
csharp_indent_labels = flush_left
csharp_indent_block_contents = true
csharp_indent_braces = false
csharp_indent_case_contents_when_block = true
```

#### <a name="csharp_indent_case_contents"></a><span data-ttu-id="39635-300">CSharp \_ wcięcie \_ case_contents</span><span class="sxs-lookup"><span data-stu-id="39635-300">csharp\_indent\_case_contents</span></span>

|<span data-ttu-id="39635-301">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-301">Property</span></span>|<span data-ttu-id="39635-302">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-302">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-303">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-303">**Option name**</span></span> | <span data-ttu-id="39635-304">csharp_indent_case_contents</span><span class="sxs-lookup"><span data-stu-id="39635-304">csharp_indent_case_contents</span></span> |
| <span data-ttu-id="39635-305">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-305">**Applicable languages**</span></span> | <span data-ttu-id="39635-306">C#</span><span class="sxs-lookup"><span data-stu-id="39635-306">C#</span></span> |
| <span data-ttu-id="39635-307">**Wprowadzona wersja**</span><span class="sxs-lookup"><span data-stu-id="39635-307">**Introduced version**</span></span> | <span data-ttu-id="39635-308">Visual Studio 2017, wersja 15.3</span><span class="sxs-lookup"><span data-stu-id="39635-308">Visual Studio 2017 version 15.3</span></span> |
| <span data-ttu-id="39635-309">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-309">**Option values**</span></span> | <span data-ttu-id="39635-310">`true` — Wcięcie `switch` zawartości przypadku</span><span class="sxs-lookup"><span data-stu-id="39635-310">`true` - Indent `switch` case contents</span></span><br /><br /><span data-ttu-id="39635-311">`false` -Nie Wetnij `switch` zawartości wielkości liter</span><span class="sxs-lookup"><span data-stu-id="39635-311">`false` - Do not indent `switch` case contents</span></span> |

- <span data-ttu-id="39635-312">Gdy ta reguła ma **wartość true**, i.</span><span class="sxs-lookup"><span data-stu-id="39635-312">When this rule is set to **true**, i.</span></span>
- <span data-ttu-id="39635-313">Gdy ta reguła jest ustawiona na **false**, d.</span><span class="sxs-lookup"><span data-stu-id="39635-313">When this rule is set to **false**, d.</span></span>

<span data-ttu-id="39635-314">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-314">Code examples:</span></span>

```csharp
// csharp_indent_case_contents = true
switch(c) {
    case Color.Red:
        Console.WriteLine("The color is red");
        break;
    case Color.Blue:
        Console.WriteLine("The color is blue");
        break;
    default:
        Console.WriteLine("The color is unknown.");
        break;
}

// csharp_indent_case_contents = false
switch(c) {
    case Color.Red:
    Console.WriteLine("The color is red");
    break;
    case Color.Blue:
    Console.WriteLine("The color is blue");
    break;
    default:
    Console.WriteLine("The color is unknown.");
    break;
}
```

#### <a name="csharp_indent_switch_labels"></a><span data-ttu-id="39635-315">CSharp \_ wcięcie \_ switch_labels</span><span class="sxs-lookup"><span data-stu-id="39635-315">csharp\_indent\_switch_labels</span></span>

|<span data-ttu-id="39635-316">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-316">Property</span></span>|<span data-ttu-id="39635-317">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-317">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-318">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-318">**Option name**</span></span> | <span data-ttu-id="39635-319">csharp_indent_switch_labels</span><span class="sxs-lookup"><span data-stu-id="39635-319">csharp_indent_switch_labels</span></span> |
| <span data-ttu-id="39635-320">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-320">**Applicable languages**</span></span> | <span data-ttu-id="39635-321">C#</span><span class="sxs-lookup"><span data-stu-id="39635-321">C#</span></span> |
| <span data-ttu-id="39635-322">**Wprowadzona wersja**</span><span class="sxs-lookup"><span data-stu-id="39635-322">**Introduced version**</span></span> | <span data-ttu-id="39635-323">Visual Studio 2017, wersja 15.3</span><span class="sxs-lookup"><span data-stu-id="39635-323">Visual Studio 2017 version 15.3</span></span> |
| <span data-ttu-id="39635-324">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-324">**Option values**</span></span> | <span data-ttu-id="39635-325">`true` -Wcięcia `switch` etykiet</span><span class="sxs-lookup"><span data-stu-id="39635-325">`true` - Indent `switch` labels</span></span><br /><br /><span data-ttu-id="39635-326">`false` — Nie Wetnij `switch` etykiet</span><span class="sxs-lookup"><span data-stu-id="39635-326">`false` - Do not indent `switch` labels</span></span> |

<span data-ttu-id="39635-327">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-327">Code examples:</span></span>

```csharp
// csharp_indent_switch_labels = true
switch(c) {
    case Color.Red:
        Console.WriteLine("The color is red");
        break;
    case Color.Blue:
        Console.WriteLine("The color is blue");
        break;
    default:
        Console.WriteLine("The color is unknown.");
        break;
}

// csharp_indent_switch_labels = false
switch(c) {
case Color.Red:
    Console.WriteLine("The color is red");
    break;
case Color.Blue:
    Console.WriteLine("The color is blue");
    break;
default:
    Console.WriteLine("The color is unknown.");
    break;
}
```

#### <a name="csharp_indent_labels"></a><span data-ttu-id="39635-328">CSharp \_ indent_labels</span><span class="sxs-lookup"><span data-stu-id="39635-328">csharp\_indent_labels</span></span>

|<span data-ttu-id="39635-329">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-329">Property</span></span>|<span data-ttu-id="39635-330">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-330">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-331">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-331">**Option name**</span></span> | <span data-ttu-id="39635-332">csharp_indent_labels</span><span class="sxs-lookup"><span data-stu-id="39635-332">csharp_indent_labels</span></span> |
| <span data-ttu-id="39635-333">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-333">**Applicable languages**</span></span> | <span data-ttu-id="39635-334">C#</span><span class="sxs-lookup"><span data-stu-id="39635-334">C#</span></span> |
| <span data-ttu-id="39635-335">**Wprowadzona wersja**</span><span class="sxs-lookup"><span data-stu-id="39635-335">**Introduced version**</span></span> | <span data-ttu-id="39635-336">Visual Studio 2017, wersja 15.3</span><span class="sxs-lookup"><span data-stu-id="39635-336">Visual Studio 2017 version 15.3</span></span> |
| <span data-ttu-id="39635-337">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-337">**Option values**</span></span> | <span data-ttu-id="39635-338">`flush_left` -Etykiety są umieszczane w kolumnie z lewej strony</span><span class="sxs-lookup"><span data-stu-id="39635-338">`flush_left` - Labels are placed at the leftmost column</span></span><br /><br /><span data-ttu-id="39635-339">`one_less_than_current` -Etykiety są umieszczane w jednym z niższych wcięć w bieżącym kontekście</span><span class="sxs-lookup"><span data-stu-id="39635-339">`one_less_than_current` - Labels are placed at one less indent to the current context</span></span><br /><br /><span data-ttu-id="39635-340">`no_change` -Etykiety są umieszczane w tym samym powiększeniu co bieżący kontekst</span><span class="sxs-lookup"><span data-stu-id="39635-340">`no_change` - Labels are placed at the same indent as the current context</span></span> |

<span data-ttu-id="39635-341">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-341">Code examples:</span></span>

```csharp
// csharp_indent_labels= flush_left
class C
{
    private string MyMethod(...)
    {
        if (...) {
            goto error;
        }
error:
        throw new Exception(...);
    }
}

// csharp_indent_labels = one_less_than_current
class C
{
    private string MyMethod(...)
    {
        if (...) {
            goto error;
        }
    error:
        throw new Exception(...);
    }
}

// csharp_indent_labels= no_change
class C
{
    private string MyMethod(...)
    {
        if (...) {
            goto error;
        }
        error:
        throw new Exception(...);
    }
}
```

#### <a name="csharp_indent_block_contents"></a><span data-ttu-id="39635-342">csharp_indent_block_contents</span><span class="sxs-lookup"><span data-stu-id="39635-342">csharp_indent_block_contents</span></span>

|<span data-ttu-id="39635-343">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-343">Property</span></span>|<span data-ttu-id="39635-344">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-344">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-345">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-345">**Option name**</span></span> | <span data-ttu-id="39635-346">csharp_indent_block_contents</span><span class="sxs-lookup"><span data-stu-id="39635-346">csharp_indent_block_contents</span></span> |
| <span data-ttu-id="39635-347">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-347">**Applicable languages**</span></span> | <span data-ttu-id="39635-348">C#</span><span class="sxs-lookup"><span data-stu-id="39635-348">C#</span></span> |
| <span data-ttu-id="39635-349">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-349">**Option values**</span></span> | `true` - <br /><br />`false` -  |

<span data-ttu-id="39635-350">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-350">Code examples:</span></span>

```csharp
// csharp_indent_block_contents = true
static void Hello()
{
    Console.WriteLine("Hello");
}

// csharp_indent_block_contents = false
static void Hello()
{
Console.WriteLine("Hello");
}
```

#### <a name="csharp_indent_braces"></a><span data-ttu-id="39635-351">csharp_indent_braces</span><span class="sxs-lookup"><span data-stu-id="39635-351">csharp_indent_braces</span></span>

|<span data-ttu-id="39635-352">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-352">Property</span></span>|<span data-ttu-id="39635-353">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-353">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-354">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-354">**Option name**</span></span> | <span data-ttu-id="39635-355">csharp_indent_braces</span><span class="sxs-lookup"><span data-stu-id="39635-355">csharp_indent_braces</span></span> |
| <span data-ttu-id="39635-356">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-356">**Applicable languages**</span></span> | <span data-ttu-id="39635-357">C#</span><span class="sxs-lookup"><span data-stu-id="39635-357">C#</span></span> |
| <span data-ttu-id="39635-358">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-358">**Option values**</span></span> | `true` - <br /><br />`false` -  |

<span data-ttu-id="39635-359">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-359">Code examples:</span></span>

```csharp
// csharp_indent_braces = true
static void Hello()
    {
    Console.WriteLine("Hello");
    }

// csharp_indent_braces = false
static void Hello()
{
    Console.WriteLine("Hello");
}
```

#### <a name="csharp_indent_case_contents_when_block"></a><span data-ttu-id="39635-360">csharp_indent_case_contents_when_block</span><span class="sxs-lookup"><span data-stu-id="39635-360">csharp_indent_case_contents_when_block</span></span>

|<span data-ttu-id="39635-361">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-361">Property</span></span>|<span data-ttu-id="39635-362">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-362">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-363">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-363">**Option name**</span></span> | <span data-ttu-id="39635-364">csharp_indent_case_contents_when_block</span><span class="sxs-lookup"><span data-stu-id="39635-364">csharp_indent_case_contents_when_block</span></span> |
| <span data-ttu-id="39635-365">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-365">**Applicable languages**</span></span> | <span data-ttu-id="39635-366">C#</span><span class="sxs-lookup"><span data-stu-id="39635-366">C#</span></span> |
| <span data-ttu-id="39635-367">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-367">**Option values**</span></span> | `true` - <br /><br />`false` -  |

<span data-ttu-id="39635-368">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-368">Code examples:</span></span>

```csharp
// csharp_indent_case_contents_when_block = true
case 0:
    {
        Console.WriteLine("Hello");
        break;
    }

// csharp_indent_case_contents_when_block = false
case 0:
{
    Console.WriteLine("Hello");
    break;
}
```

### <a name="spacing-options"></a><span data-ttu-id="39635-369">Opcje odstępów</span><span class="sxs-lookup"><span data-stu-id="39635-369">Spacing options</span></span>

<span data-ttu-id="39635-370">Te reguły formatowania dotyczą używania znaków spacji do formatowania kodu.</span><span class="sxs-lookup"><span data-stu-id="39635-370">These formatting rules concern the use of space characters to format code.</span></span>

<span data-ttu-id="39635-371">Przykładowy plik *. editorconfig* :</span><span class="sxs-lookup"><span data-stu-id="39635-371">Example *.editorconfig* file:</span></span>

```ini
# CSharp formatting rules:
[*.cs]
csharp_space_after_cast = true
csharp_space_after_keywords_in_control_flow_statements = true
csharp_space_between_parentheses = control_flow_statements, type_casts
csharp_space_before_colon_in_inheritance_clause = true
csharp_space_after_colon_in_inheritance_clause = true
csharp_space_around_binary_operators = before_and_after
csharp_space_between_method_declaration_parameter_list_parentheses = true
csharp_space_between_method_declaration_empty_parameter_list_parentheses = false
csharp_space_between_method_declaration_name_and_open_parenthesis = false
csharp_space_between_method_call_parameter_list_parentheses = true
csharp_space_between_method_call_empty_parameter_list_parentheses = false
csharp_space_between_method_call_name_and_opening_parenthesis = false
csharp_space_after_comma = true
csharp_space_before_comma = false
csharp_space_after_dot = false
csharp_space_before_dot = false
csharp_space_after_semicolon_in_for_statement = true
csharp_space_before_semicolon_in_for_statement = false
csharp_space_around_declaration_statements = false
csharp_space_before_open_square_brackets = false
csharp_space_between_empty_square_brackets = false
csharp_space_between_square_brackets = false
```

#### <a name="csharp_space_after_cast"></a><span data-ttu-id="39635-372">CSharp \_ \_ after_cast miejsca</span><span class="sxs-lookup"><span data-stu-id="39635-372">csharp\_space\_after_cast</span></span>

|<span data-ttu-id="39635-373">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-373">Property</span></span>|<span data-ttu-id="39635-374">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-374">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-375">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-375">**Option name**</span></span> | <span data-ttu-id="39635-376">csharp_space_after_cast</span><span class="sxs-lookup"><span data-stu-id="39635-376">csharp_space_after_cast</span></span> |
| <span data-ttu-id="39635-377">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-377">**Applicable languages**</span></span> | <span data-ttu-id="39635-378">C#</span><span class="sxs-lookup"><span data-stu-id="39635-378">C#</span></span> |
| <span data-ttu-id="39635-379">**Wprowadzona wersja**</span><span class="sxs-lookup"><span data-stu-id="39635-379">**Introduced version**</span></span> | <span data-ttu-id="39635-380">Visual Studio 2017, wersja 15.3</span><span class="sxs-lookup"><span data-stu-id="39635-380">Visual Studio 2017 version 15.3</span></span> |
| <span data-ttu-id="39635-381">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-381">**Option values**</span></span> | <span data-ttu-id="39635-382">`true` -Umieść znak spacji między rzutem a wartością</span><span class="sxs-lookup"><span data-stu-id="39635-382">`true` - Place a space character between a cast and the value</span></span><br /><br /><span data-ttu-id="39635-383">`false` -Usuń odstęp między rzutem a wartością</span><span class="sxs-lookup"><span data-stu-id="39635-383">`false` - Remove space between the cast and the value</span></span> |

<span data-ttu-id="39635-384">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-384">Code examples:</span></span>

```csharp
// csharp_space_after_cast = true
int y = (int) x;

// csharp_space_after_cast = false
int y = (int)x;
```

#### <a name="csharp_space_after_keywords_in_control_flow_statements"></a><span data-ttu-id="39635-385">csharp_space_after_keywords_in_control_flow_statements</span><span class="sxs-lookup"><span data-stu-id="39635-385">csharp_space_after_keywords_in_control_flow_statements</span></span>

|<span data-ttu-id="39635-386">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-386">Property</span></span>|<span data-ttu-id="39635-387">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-387">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-388">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-388">**Option name**</span></span> | <span data-ttu-id="39635-389">csharp_space_after_keywords_in_control_flow_statements</span><span class="sxs-lookup"><span data-stu-id="39635-389">csharp_space_after_keywords_in_control_flow_statements</span></span> |
| <span data-ttu-id="39635-390">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-390">**Applicable languages**</span></span> | <span data-ttu-id="39635-391">C#</span><span class="sxs-lookup"><span data-stu-id="39635-391">C#</span></span> |
| <span data-ttu-id="39635-392">**Wprowadzona wersja**</span><span class="sxs-lookup"><span data-stu-id="39635-392">**Introduced version**</span></span> | <span data-ttu-id="39635-393">Visual Studio 2017, wersja 15.3</span><span class="sxs-lookup"><span data-stu-id="39635-393">Visual Studio 2017 version 15.3</span></span> |
| <span data-ttu-id="39635-394">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-394">**Option values**</span></span> | <span data-ttu-id="39635-395">`true` -Umieść znak spacji po słowie kluczowym w instrukcji przepływu sterowania, takiej jak `for` Pętla</span><span class="sxs-lookup"><span data-stu-id="39635-395">`true` - Place a space character after a keyword in a control flow statement such as a `for` loop</span></span><br /><br /><span data-ttu-id="39635-396">`false` -Usuń spację po słowie kluczowym w instrukcji przepływu sterowania, takiej jak `for` Pętla</span><span class="sxs-lookup"><span data-stu-id="39635-396">`false` - Remove space after a keyword in a control flow statement such as a `for` loop</span></span> |

<span data-ttu-id="39635-397">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-397">Code examples:</span></span>

```csharp
// csharp_space_after_keywords_in_control_flow_statements = true
for (int i;i<x;i++) { ... }

// csharp_space_after_keywords_in_control_flow_statements = false
for(int i;i<x;i++) { ... }
```

#### <a name="csharp_space_between_parentheses"></a><span data-ttu-id="39635-398">csharp_space_between_parentheses</span><span class="sxs-lookup"><span data-stu-id="39635-398">csharp_space_between_parentheses</span></span>

|<span data-ttu-id="39635-399">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-399">Property</span></span>|<span data-ttu-id="39635-400">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-400">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-401">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-401">**Option name**</span></span> | <span data-ttu-id="39635-402">csharp_space_between_parentheses</span><span class="sxs-lookup"><span data-stu-id="39635-402">csharp_space_between_parentheses</span></span> |
| <span data-ttu-id="39635-403">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-403">**Applicable languages**</span></span> | <span data-ttu-id="39635-404">C#</span><span class="sxs-lookup"><span data-stu-id="39635-404">C#</span></span> |
| <span data-ttu-id="39635-405">**Wprowadzona wersja**</span><span class="sxs-lookup"><span data-stu-id="39635-405">**Introduced version**</span></span> | <span data-ttu-id="39635-406">Visual Studio 2017, wersja 15.3</span><span class="sxs-lookup"><span data-stu-id="39635-406">Visual Studio 2017 version 15.3</span></span> |
| <span data-ttu-id="39635-407">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-407">**Option values**</span></span> | <span data-ttu-id="39635-408">`control_flow_statements` -Umieść miejsce między nawiasami instrukcji przepływu sterowania</span><span class="sxs-lookup"><span data-stu-id="39635-408">`control_flow_statements` - Place space between parentheses of control flow statements</span></span><br /><br /><span data-ttu-id="39635-409">`expressions` -Miejsce między nawiasami wyrażenia</span><span class="sxs-lookup"><span data-stu-id="39635-409">`expressions` - Place space between parentheses of expressions</span></span><br /><br /><span data-ttu-id="39635-410">`type_casts` -Umieść miejsce między nawiasami w rzutach typu</span><span class="sxs-lookup"><span data-stu-id="39635-410">`type_casts` - Place space between parentheses in type casts</span></span> |

<span data-ttu-id="39635-411">Jeśli pominięto tę regułę lub użyjesz wartości innej niż `control_flow_statements` , `expressions` lub `type_casts` , to ustawienie nie jest stosowane.</span><span class="sxs-lookup"><span data-stu-id="39635-411">If you omit this rule or use a value other than `control_flow_statements`, `expressions`, or `type_casts`, the setting is not applied.</span></span>

<span data-ttu-id="39635-412">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-412">Code examples:</span></span>

```csharp
// csharp_space_between_parentheses = control_flow_statements
for ( int i = 0; i < 10; i++ ) { }

// csharp_space_between_parentheses = expressions
var z = ( x * y ) - ( ( y - x ) * 3 );

// csharp_space_between_parentheses = type_casts
int y = ( int )x;
```

#### <a name="csharp_space_before_colon_in_inheritance_clause"></a><span data-ttu-id="39635-413">CSharp \_ spację \_ przed \_ dwukropkiem \_ w \_ inheritance_clause</span><span class="sxs-lookup"><span data-stu-id="39635-413">csharp\_space\_before\_colon\_in\_inheritance_clause</span></span>

|<span data-ttu-id="39635-414">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-414">Property</span></span>|<span data-ttu-id="39635-415">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-415">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-416">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-416">**Option name**</span></span> | <span data-ttu-id="39635-417">csharp_space_before_colon_in_inheritance_clause</span><span class="sxs-lookup"><span data-stu-id="39635-417">csharp_space_before_colon_in_inheritance_clause</span></span> |
| <span data-ttu-id="39635-418">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-418">**Applicable languages**</span></span> | <span data-ttu-id="39635-419">C#</span><span class="sxs-lookup"><span data-stu-id="39635-419">C#</span></span> |
| <span data-ttu-id="39635-420">**Wprowadzona wersja**</span><span class="sxs-lookup"><span data-stu-id="39635-420">**Introduced version**</span></span> | <span data-ttu-id="39635-421">Visual Studio 2017 w wersji 15.7</span><span class="sxs-lookup"><span data-stu-id="39635-421">Visual Studio 2017 version 15.7</span></span> |
| <span data-ttu-id="39635-422">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-422">**Option values**</span></span> | <span data-ttu-id="39635-423">`true` -Umieść znak spacji przed dwukropkiem dla baz lub interfejsów w deklaracji typu</span><span class="sxs-lookup"><span data-stu-id="39635-423">`true` - Place a space character before the colon for bases or interfaces in a type declaration</span></span><br /><br /><span data-ttu-id="39635-424">`false` -Usuń spację przed dwukropkiem dla baz lub interfejsów w deklaracji typu</span><span class="sxs-lookup"><span data-stu-id="39635-424">`false` - Remove space before the colon for bases or interfaces in a type declaration</span></span> |

<span data-ttu-id="39635-425">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-425">Code examples:</span></span>

```csharp
// csharp_space_before_colon_in_inheritance_clause = true
interface I
{

}

class C : I
{

}

// csharp_space_before_colon_in_inheritance_clause = false
interface I
{

}

class C: I
{

}
```

#### <a name="csharp_space_after_colon_in_inheritance_clause"></a><span data-ttu-id="39635-426">CSharp \_ spację \_ po \_ dwukropku \_ w \_ inheritance_clause</span><span class="sxs-lookup"><span data-stu-id="39635-426">csharp\_space\_after\_colon\_in\_inheritance_clause</span></span>

|<span data-ttu-id="39635-427">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-427">Property</span></span>|<span data-ttu-id="39635-428">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-428">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-429">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-429">**Option name**</span></span> | <span data-ttu-id="39635-430">csharp_space_after_colon_in_inheritance_clause</span><span class="sxs-lookup"><span data-stu-id="39635-430">csharp_space_after_colon_in_inheritance_clause</span></span> |
| <span data-ttu-id="39635-431">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-431">**Applicable languages**</span></span> | <span data-ttu-id="39635-432">C#</span><span class="sxs-lookup"><span data-stu-id="39635-432">C#</span></span> |
| <span data-ttu-id="39635-433">**Wprowadzona wersja**</span><span class="sxs-lookup"><span data-stu-id="39635-433">**Introduced version**</span></span> | <span data-ttu-id="39635-434">Visual Studio 2017 w wersji 15.7</span><span class="sxs-lookup"><span data-stu-id="39635-434">Visual Studio 2017 version 15.7</span></span> |
| <span data-ttu-id="39635-435">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-435">**Option values**</span></span> | <span data-ttu-id="39635-436">`true` -Umieść znak spacji po dwukropku dla baz lub interfejsów w deklaracji typu</span><span class="sxs-lookup"><span data-stu-id="39635-436">`true` - Place a space character after the colon for bases or interfaces in a type declaration</span></span><br /><br /><span data-ttu-id="39635-437">`false` -Usuń spację po dwukropku dla podstaw lub interfejsów w deklaracji typu</span><span class="sxs-lookup"><span data-stu-id="39635-437">`false` - Remove space after the colon for bases or interfaces in a type declaration</span></span> |

<span data-ttu-id="39635-438">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-438">Code examples:</span></span>

```csharp
// csharp_space_after_colon_in_inheritance_clause = true
interface I
{

}

class C : I
{

}

// csharp_space_after_colon_in_inheritance_clause = false
interface I
{

}

class C :I
{

}
```

#### <a name="csharp_space_around_binary_operators"></a><span data-ttu-id="39635-439">CSharp \_ miejsce \_ dookoła \_ binary_operators</span><span class="sxs-lookup"><span data-stu-id="39635-439">csharp\_space\_around\_binary_operators</span></span>

|<span data-ttu-id="39635-440">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-440">Property</span></span>|<span data-ttu-id="39635-441">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-441">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-442">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-442">**Option name**</span></span> | <span data-ttu-id="39635-443">csharp_space_around_binary_operators</span><span class="sxs-lookup"><span data-stu-id="39635-443">csharp_space_around_binary_operators</span></span> |
| <span data-ttu-id="39635-444">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-444">**Applicable languages**</span></span> | <span data-ttu-id="39635-445">C#</span><span class="sxs-lookup"><span data-stu-id="39635-445">C#</span></span> |
| <span data-ttu-id="39635-446">**Wprowadzona wersja**</span><span class="sxs-lookup"><span data-stu-id="39635-446">**Introduced version**</span></span> | <span data-ttu-id="39635-447">Visual Studio 2017 w wersji 15.7</span><span class="sxs-lookup"><span data-stu-id="39635-447">Visual Studio 2017 version 15.7</span></span> |
| <span data-ttu-id="39635-448">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-448">**Option values**</span></span> | <span data-ttu-id="39635-449">`before_and_after` -Wstaw spację przed i po operatorze Binary</span><span class="sxs-lookup"><span data-stu-id="39635-449">`before_and_after` - Insert space before and after the binary operator</span></span><br /><br /><span data-ttu-id="39635-450">`none` -Usuń odstępy przed i po operatorze Binary</span><span class="sxs-lookup"><span data-stu-id="39635-450">`none` - Remove spaces before and after the binary operator</span></span><br /><br /><span data-ttu-id="39635-451">`ignore` -Ignoruj odstępy dookoła operatorów binarnych</span><span class="sxs-lookup"><span data-stu-id="39635-451">`ignore` - Ignore spaces around binary operators</span></span> |

<span data-ttu-id="39635-452">Jeśli pominięto tę regułę lub używasz wartości innej niż `before_and_after` , `none` lub `ignore` , ustawienie nie jest stosowane.</span><span class="sxs-lookup"><span data-stu-id="39635-452">If you omit this rule, or use a value other than `before_and_after`, `none`, or `ignore`, the setting is not applied.</span></span>

<span data-ttu-id="39635-453">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-453">Code examples:</span></span>

```csharp
// csharp_space_around_binary_operators = before_and_after
return x * (x - y);

// csharp_space_around_binary_operators = none
return x*(x-y);

// csharp_space_around_binary_operators = ignore
return x  *  (x-y);
```

#### <a name="csharp_space_between_method_declaration_parameter_list_parentheses"></a><span data-ttu-id="39635-454">csharp_space_between_method_declaration_parameter_list_parentheses</span><span class="sxs-lookup"><span data-stu-id="39635-454">csharp_space_between_method_declaration_parameter_list_parentheses</span></span>

|<span data-ttu-id="39635-455">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-455">Property</span></span>|<span data-ttu-id="39635-456">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-456">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-457">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-457">**Option name**</span></span> | <span data-ttu-id="39635-458">csharp_space_between_method_declaration_parameter_list_parentheses</span><span class="sxs-lookup"><span data-stu-id="39635-458">csharp_space_between_method_declaration_parameter_list_parentheses</span></span> |
| <span data-ttu-id="39635-459">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-459">**Applicable languages**</span></span> | <span data-ttu-id="39635-460">C#</span><span class="sxs-lookup"><span data-stu-id="39635-460">C#</span></span> |
| <span data-ttu-id="39635-461">**Wprowadzona wersja**</span><span class="sxs-lookup"><span data-stu-id="39635-461">**Introduced version**</span></span> | <span data-ttu-id="39635-462">Visual Studio 2017, wersja 15.3</span><span class="sxs-lookup"><span data-stu-id="39635-462">Visual Studio 2017 version 15.3</span></span> |
| <span data-ttu-id="39635-463">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-463">**Option values**</span></span> | <span data-ttu-id="39635-464">`true` -Umieść znak spacji po nawiasie otwierającym i przed nawiasem zamykającym listy parametrów deklaracji metody</span><span class="sxs-lookup"><span data-stu-id="39635-464">`true` - Place a space character after the opening parenthesis and before the closing parenthesis of a method declaration parameter list</span></span><br /><br /><span data-ttu-id="39635-465">`false` -Usuń znaki spacji po nawiasie otwierającym i przed nawiasem zamykającym listy parametrów deklaracji metody</span><span class="sxs-lookup"><span data-stu-id="39635-465">`false` - Remove space characters after the opening parenthesis and before the closing parenthesis of a method declaration parameter list</span></span> |

<span data-ttu-id="39635-466">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-466">Code examples:</span></span>

```csharp
// csharp_space_between_method_declaration_parameter_list_parentheses = true
void Bark( int x ) { ... }

// csharp_space_between_method_declaration_parameter_list_parentheses = false
void Bark(int x) { ... }
```

#### <a name="csharp_space_between_method_declaration_empty_parameter_list_parentheses"></a><span data-ttu-id="39635-467">csharp_space_between_method_declaration_empty_parameter_list_parentheses</span><span class="sxs-lookup"><span data-stu-id="39635-467">csharp_space_between_method_declaration_empty_parameter_list_parentheses</span></span>

|<span data-ttu-id="39635-468">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-468">Property</span></span>|<span data-ttu-id="39635-469">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-469">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-470">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-470">**Option name**</span></span> | <span data-ttu-id="39635-471">csharp_space_between_method_declaration_empty_parameter_list_parentheses</span><span class="sxs-lookup"><span data-stu-id="39635-471">csharp_space_between_method_declaration_empty_parameter_list_parentheses</span></span> |
| <span data-ttu-id="39635-472">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-472">**Applicable languages**</span></span> | <span data-ttu-id="39635-473">C#</span><span class="sxs-lookup"><span data-stu-id="39635-473">C#</span></span> |
| <span data-ttu-id="39635-474">**Wprowadzona wersja**</span><span class="sxs-lookup"><span data-stu-id="39635-474">**Introduced version**</span></span> | <span data-ttu-id="39635-475">Visual Studio 2017 w wersji 15.7</span><span class="sxs-lookup"><span data-stu-id="39635-475">Visual Studio 2017 version 15.7</span></span> |
| <span data-ttu-id="39635-476">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-476">**Option values**</span></span> | <span data-ttu-id="39635-477">`true` -Wstaw odstęp wewnątrz nawiasów listy pustych parametrów dla deklaracji metody</span><span class="sxs-lookup"><span data-stu-id="39635-477">`true` - Insert space within empty parameter list parentheses for a method declaration</span></span><br /><br /><span data-ttu-id="39635-478">`false` -Usuń spację w nawiasach listy pustych parametrów dla deklaracji metody</span><span class="sxs-lookup"><span data-stu-id="39635-478">`false` - Remove space within empty parameter list parentheses for a method declaration</span></span> |

<span data-ttu-id="39635-479">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-479">Code examples:</span></span>

```csharp
// csharp_space_between_method_declaration_empty_parameter_list_parentheses = true
void Goo( )
{
    Goo(1);
}

void Goo(int x)
{
    Goo();
}

// csharp_space_between_method_declaration_empty_parameter_list_parentheses = false
void Goo()
{
    Goo(1);
}

void Goo(int x)
{
    Goo();
}
```

#### <a name="csharp_space_between_method_declaration_name_and_open_parenthesis"></a><span data-ttu-id="39635-480">csharp_space_between_method_declaration_name_and_open_parenthesis</span><span class="sxs-lookup"><span data-stu-id="39635-480">csharp_space_between_method_declaration_name_and_open_parenthesis</span></span>

|<span data-ttu-id="39635-481">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-481">Property</span></span>|<span data-ttu-id="39635-482">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-482">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-483">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-483">**Option name**</span></span> | <span data-ttu-id="39635-484">csharp_space_between_method_declaration_name_and_open_parenthesis</span><span class="sxs-lookup"><span data-stu-id="39635-484">csharp_space_between_method_declaration_name_and_open_parenthesis</span></span> |
| <span data-ttu-id="39635-485">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-485">**Applicable languages**</span></span> | <span data-ttu-id="39635-486">C#</span><span class="sxs-lookup"><span data-stu-id="39635-486">C#</span></span> |
| <span data-ttu-id="39635-487">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-487">**Option values**</span></span> | <span data-ttu-id="39635-488">`true` -Umieść znak spacji między nazwą metody i nawiasem otwierającym w deklaracji metody</span><span class="sxs-lookup"><span data-stu-id="39635-488">`true` - Place a space character between the method name and opening parenthesis in the method declaration</span></span><br /><br /><span data-ttu-id="39635-489">`false` -Usuń znaki spacji między nazwą metody i nawiasem otwierającym w deklaracji metody</span><span class="sxs-lookup"><span data-stu-id="39635-489">`false` - Remove space characters between the method name and opening parenthesis in the method declaration</span></span> |

<span data-ttu-id="39635-490">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-490">Code examples:</span></span>

```csharp
// csharp_space_between_method_declaration_name_and_open_parenthesis = true
void M () { }

// csharp_space_between_method_declaration_name_and_open_parenthesis = false
void M() { }
```

#### <a name="csharp_space_between_method_call_parameter_list_parentheses"></a><span data-ttu-id="39635-491">csharp_space_between_method_call_parameter_list_parentheses</span><span class="sxs-lookup"><span data-stu-id="39635-491">csharp_space_between_method_call_parameter_list_parentheses</span></span>

|<span data-ttu-id="39635-492">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-492">Property</span></span>|<span data-ttu-id="39635-493">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-493">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-494">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-494">**Option name**</span></span> | <span data-ttu-id="39635-495">csharp_space_between_method_call_parameter_list_parentheses</span><span class="sxs-lookup"><span data-stu-id="39635-495">csharp_space_between_method_call_parameter_list_parentheses</span></span> |
| <span data-ttu-id="39635-496">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-496">**Applicable languages**</span></span> | <span data-ttu-id="39635-497">C#</span><span class="sxs-lookup"><span data-stu-id="39635-497">C#</span></span> |
| <span data-ttu-id="39635-498">**Wprowadzona wersja**</span><span class="sxs-lookup"><span data-stu-id="39635-498">**Introduced version**</span></span> | <span data-ttu-id="39635-499">Visual Studio 2017, wersja 15.3</span><span class="sxs-lookup"><span data-stu-id="39635-499">Visual Studio 2017 version 15.3</span></span> |
| <span data-ttu-id="39635-500">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-500">**Option values**</span></span> | <span data-ttu-id="39635-501">`true` -Umieść znak spacji po nawiasie otwierającym i przed nawiasem zamykającym wywołania metody</span><span class="sxs-lookup"><span data-stu-id="39635-501">`true` - Place a space character after the opening parenthesis and before the closing parenthesis of a method call</span></span><br /><br /><span data-ttu-id="39635-502">`false` -Usuń znaki spacji po nawiasie otwierającym i przed nawiasem zamykającym wywołania metody</span><span class="sxs-lookup"><span data-stu-id="39635-502">`false` - Remove space characters after the opening parenthesis and before the closing parenthesis of a method call</span></span> |

<span data-ttu-id="39635-503">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-503">Code examples:</span></span>

```csharp
// csharp_space_between_method_call_parameter_list_parentheses = true
MyMethod( argument );

// csharp_space_between_method_call_parameter_list_parentheses = false
MyMethod(argument);
```

#### <a name="csharp_space_between_method_call_empty_parameter_list_parentheses"></a><span data-ttu-id="39635-504">csharp_space_between_method_call_empty_parameter_list_parentheses</span><span class="sxs-lookup"><span data-stu-id="39635-504">csharp_space_between_method_call_empty_parameter_list_parentheses</span></span>

|<span data-ttu-id="39635-505">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-505">Property</span></span>|<span data-ttu-id="39635-506">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-506">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-507">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-507">**Option name**</span></span> | <span data-ttu-id="39635-508">csharp_space_between_method_call_empty_parameter_list_parentheses</span><span class="sxs-lookup"><span data-stu-id="39635-508">csharp_space_between_method_call_empty_parameter_list_parentheses</span></span> |
| <span data-ttu-id="39635-509">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-509">**Applicable languages**</span></span> | <span data-ttu-id="39635-510">C#</span><span class="sxs-lookup"><span data-stu-id="39635-510">C#</span></span> |
| <span data-ttu-id="39635-511">**Wprowadzona wersja**</span><span class="sxs-lookup"><span data-stu-id="39635-511">**Introduced version**</span></span> | <span data-ttu-id="39635-512">Visual Studio 2017 w wersji 15.7</span><span class="sxs-lookup"><span data-stu-id="39635-512">Visual Studio 2017 version 15.7</span></span> |
| <span data-ttu-id="39635-513">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-513">**Option values**</span></span> | <span data-ttu-id="39635-514">`true` -Wstaw odstęp wewnątrz nawiasów listy pustych argumentów</span><span class="sxs-lookup"><span data-stu-id="39635-514">`true` - Insert space within empty argument list parentheses</span></span><br /><br /><span data-ttu-id="39635-515">`false` -Usuń spację w nawiasach listy pustych argumentów</span><span class="sxs-lookup"><span data-stu-id="39635-515">`false` - Remove space within empty argument list parentheses</span></span> |

<span data-ttu-id="39635-516">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-516">Code examples:</span></span>

```csharp
// csharp_space_between_method_call_empty_parameter_list_parentheses = true
void Goo()
{
    Goo(1);
}

void Goo(int x)
{
    Goo( );
}

// csharp_space_between_method_call_empty_parameter_list_parentheses = false
void Goo()
{
    Goo(1);
}

void Goo(int x)
{
    Goo();
}
```

#### <a name="csharp_space_between_method_call_name_and_opening_parenthesis"></a><span data-ttu-id="39635-517">csharp_space_between_method_call_name_and_opening_parenthesis</span><span class="sxs-lookup"><span data-stu-id="39635-517">csharp_space_between_method_call_name_and_opening_parenthesis</span></span>

|<span data-ttu-id="39635-518">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-518">Property</span></span>|<span data-ttu-id="39635-519">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-519">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-520">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-520">**Option name**</span></span> | <span data-ttu-id="39635-521">csharp_space_between_method_call_name_and_opening_parenthesis</span><span class="sxs-lookup"><span data-stu-id="39635-521">csharp_space_between_method_call_name_and_opening_parenthesis</span></span> |
| <span data-ttu-id="39635-522">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-522">**Applicable languages**</span></span> | <span data-ttu-id="39635-523">C#</span><span class="sxs-lookup"><span data-stu-id="39635-523">C#</span></span> |
| <span data-ttu-id="39635-524">**Wprowadzona wersja**</span><span class="sxs-lookup"><span data-stu-id="39635-524">**Introduced version**</span></span> | <span data-ttu-id="39635-525">Visual Studio 2017 w wersji 15.7</span><span class="sxs-lookup"><span data-stu-id="39635-525">Visual Studio 2017 version 15.7</span></span> |
| <span data-ttu-id="39635-526">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-526">**Option values**</span></span> | <span data-ttu-id="39635-527">`true` -Wstaw spację między nazwą wywołania metody i nawiasem otwierającym</span><span class="sxs-lookup"><span data-stu-id="39635-527">`true` - Insert space between method call name and opening parenthesis</span></span><br /><br /><span data-ttu-id="39635-528">`false` -Usuń spację między nazwą wywołania metody i nawiasem otwierającym</span><span class="sxs-lookup"><span data-stu-id="39635-528">`false` - Remove space between method call name and opening parenthesis</span></span> |

<span data-ttu-id="39635-529">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-529">Code examples:</span></span>

```csharp
// csharp_space_between_method_call_name_and_opening_parenthesis = true
void Goo()
{
    Goo (1);
}

void Goo(int x)
{
    Goo ();
}

// csharp_space_between_method_call_name_and_opening_parenthesis = false
void Goo()
{
    Goo(1);
}

void Goo(int x)
{
    Goo();
}
```

#### <a name="csharp_space_after_comma"></a><span data-ttu-id="39635-530">csharp_space_after_comma</span><span class="sxs-lookup"><span data-stu-id="39635-530">csharp_space_after_comma</span></span>

|<span data-ttu-id="39635-531">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-531">Property</span></span>|<span data-ttu-id="39635-532">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-532">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-533">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-533">**Option name**</span></span> | <span data-ttu-id="39635-534">csharp_space_after_comma</span><span class="sxs-lookup"><span data-stu-id="39635-534">csharp_space_after_comma</span></span> |
| <span data-ttu-id="39635-535">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-535">**Applicable languages**</span></span> | <span data-ttu-id="39635-536">C#</span><span class="sxs-lookup"><span data-stu-id="39635-536">C#</span></span> |
| <span data-ttu-id="39635-537">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-537">**Option values**</span></span> | <span data-ttu-id="39635-538">`true` -Wstaw odstęp po przecinku</span><span class="sxs-lookup"><span data-stu-id="39635-538">`true` - Insert space after a comma</span></span><br /><br /><span data-ttu-id="39635-539">`false` -Usuń spację po przecinku</span><span class="sxs-lookup"><span data-stu-id="39635-539">`false` - Remove space after a comma</span></span> |

<span data-ttu-id="39635-540">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-540">Code examples:</span></span>

```csharp
// csharp_space_after_comma = true
int[] x = new int[] { 1, 2, 3, 4, 5 };

// csharp_space_after_comma = false
int[] x = new int[] { 1,2,3,4,5 }
```

#### <a name="csharp_space_before_comma"></a><span data-ttu-id="39635-541">csharp_space_before_comma</span><span class="sxs-lookup"><span data-stu-id="39635-541">csharp_space_before_comma</span></span>

|<span data-ttu-id="39635-542">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-542">Property</span></span>|<span data-ttu-id="39635-543">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-543">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-544">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-544">**Option name**</span></span> | <span data-ttu-id="39635-545">csharp_space_before_comma</span><span class="sxs-lookup"><span data-stu-id="39635-545">csharp_space_before_comma</span></span> |
| <span data-ttu-id="39635-546">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-546">**Applicable languages**</span></span> | <span data-ttu-id="39635-547">C#</span><span class="sxs-lookup"><span data-stu-id="39635-547">C#</span></span> |
| <span data-ttu-id="39635-548">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-548">**Option values**</span></span> | <span data-ttu-id="39635-549">`true` -Wstaw odstęp przed przecinkiem</span><span class="sxs-lookup"><span data-stu-id="39635-549">`true` - Insert space before a comma</span></span><br /><br /><span data-ttu-id="39635-550">`false` -Usuń odstęp przed przecinkiem</span><span class="sxs-lookup"><span data-stu-id="39635-550">`false` - Remove space before a comma</span></span> |

<span data-ttu-id="39635-551">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-551">Code examples:</span></span>

```csharp
// csharp_space_before_comma = true
int[] x = new int[] { 1 , 2 , 3 , 4 , 5 };

// csharp_space_before_comma = false
int[] x = new int[] { 1, 2, 3, 4, 5 };
```

#### <a name="csharp_space_after_dot"></a><span data-ttu-id="39635-552">csharp_space_after_dot</span><span class="sxs-lookup"><span data-stu-id="39635-552">csharp_space_after_dot</span></span>

|<span data-ttu-id="39635-553">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-553">Property</span></span>|<span data-ttu-id="39635-554">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-554">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-555">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-555">**Option name**</span></span> | <span data-ttu-id="39635-556">csharp_space_after_dot</span><span class="sxs-lookup"><span data-stu-id="39635-556">csharp_space_after_dot</span></span> |
| <span data-ttu-id="39635-557">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-557">**Applicable languages**</span></span> | <span data-ttu-id="39635-558">C#</span><span class="sxs-lookup"><span data-stu-id="39635-558">C#</span></span> |
| <span data-ttu-id="39635-559">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-559">**Option values**</span></span> | <span data-ttu-id="39635-560">`true` -Wstaw odstęp po kropce</span><span class="sxs-lookup"><span data-stu-id="39635-560">`true` - Insert space after a dot</span></span><br /><br /><span data-ttu-id="39635-561">`false` -Usuń odstęp po kropce</span><span class="sxs-lookup"><span data-stu-id="39635-561">`false` - Remove space after a dot</span></span> |

<span data-ttu-id="39635-562">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-562">Code examples:</span></span>

```csharp
// csharp_space_after_dot = true
this. Goo();

// csharp_space_after_dot = false
this.Goo();
```

#### <a name="csharp_space_before_dot"></a><span data-ttu-id="39635-563">csharp_space_before_dot</span><span class="sxs-lookup"><span data-stu-id="39635-563">csharp_space_before_dot</span></span>

|<span data-ttu-id="39635-564">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-564">Property</span></span>|<span data-ttu-id="39635-565">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-565">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-566">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-566">**Option name**</span></span> | <span data-ttu-id="39635-567">csharp_space_before_dot</span><span class="sxs-lookup"><span data-stu-id="39635-567">csharp_space_before_dot</span></span> |
| <span data-ttu-id="39635-568">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-568">**Applicable languages**</span></span> | <span data-ttu-id="39635-569">C#</span><span class="sxs-lookup"><span data-stu-id="39635-569">C#</span></span> |
| <span data-ttu-id="39635-570">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-570">**Option values**</span></span> | <span data-ttu-id="39635-571">`true` -Wstaw odstęp przed kropką</span><span class="sxs-lookup"><span data-stu-id="39635-571">`true` - Insert space before a dot</span></span> <br /><br /><span data-ttu-id="39635-572">`false` -Usuń odstęp przed kropką</span><span class="sxs-lookup"><span data-stu-id="39635-572">`false` - Remove space before a dot</span></span> |

<span data-ttu-id="39635-573">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-573">Code examples:</span></span>

```csharp
// csharp_space_before_dot = true
this .Goo();

// csharp_space_before_dot = false
this.Goo();
```

#### <a name="csharp_space_after_semicolon_in_for_statement"></a><span data-ttu-id="39635-574">csharp_space_after_semicolon_in_for_statement</span><span class="sxs-lookup"><span data-stu-id="39635-574">csharp_space_after_semicolon_in_for_statement</span></span>

|<span data-ttu-id="39635-575">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-575">Property</span></span>|<span data-ttu-id="39635-576">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-576">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-577">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-577">**Option name**</span></span> | <span data-ttu-id="39635-578">csharp_space_after_semicolon_in_for_statement</span><span class="sxs-lookup"><span data-stu-id="39635-578">csharp_space_after_semicolon_in_for_statement</span></span> |
| <span data-ttu-id="39635-579">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-579">**Applicable languages**</span></span> | <span data-ttu-id="39635-580">C#</span><span class="sxs-lookup"><span data-stu-id="39635-580">C#</span></span> |
| <span data-ttu-id="39635-581">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-581">**Option values**</span></span> | <span data-ttu-id="39635-582">`true` -Wstaw odstęp po każdym średniku w `for` instrukcji</span><span class="sxs-lookup"><span data-stu-id="39635-582">`true` - Insert space after each semicolon in a `for` statement</span></span><br /><br /><span data-ttu-id="39635-583">`false` -Usuń odstęp po każdym średniku w `for` instrukcji</span><span class="sxs-lookup"><span data-stu-id="39635-583">`false` - Remove space after each semicolon in a `for` statement</span></span> |

<span data-ttu-id="39635-584">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-584">Code examples:</span></span>

```csharp
// csharp_space_after_semicolon_in_for_statement = true
for (int i = 0; i < x.Length; i++)

// csharp_space_after_semicolon_in_for_statement = false
for (int i = 0;i < x.Length;i++)
```

##### <a name="csharp_space_before_semicolon_in_for_statement"></a><span data-ttu-id="39635-585">csharp_space_before_semicolon_in_for_statement</span><span class="sxs-lookup"><span data-stu-id="39635-585">csharp_space_before_semicolon_in_for_statement</span></span>

|<span data-ttu-id="39635-586">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-586">Property</span></span>|<span data-ttu-id="39635-587">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-587">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-588">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-588">**Option name**</span></span> | <span data-ttu-id="39635-589">csharp_space_before_semicolon_in_for_statement</span><span class="sxs-lookup"><span data-stu-id="39635-589">csharp_space_before_semicolon_in_for_statement</span></span> |
| <span data-ttu-id="39635-590">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-590">**Applicable languages**</span></span> | <span data-ttu-id="39635-591">C#</span><span class="sxs-lookup"><span data-stu-id="39635-591">C#</span></span> |
| <span data-ttu-id="39635-592">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-592">**Option values**</span></span> | <span data-ttu-id="39635-593">`true` -Wstawiaj spację przed każdym średnikiem w `for` instrukcji</span><span class="sxs-lookup"><span data-stu-id="39635-593">`true` - Insert space before each semicolon in a `for` statement</span></span> <br /><br /><span data-ttu-id="39635-594">`false` -Usuń odstęp przed każdym średnikiem w `for` instrukcji</span><span class="sxs-lookup"><span data-stu-id="39635-594">`false` - Remove space before each semicolon in a `for` statement</span></span> |

<span data-ttu-id="39635-595">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-595">Code examples:</span></span>

```csharp
// csharp_space_before_semicolon_in_for_statement = true
for (int i = 0 ; i < x.Length ; i++)

// csharp_space_before_semicolon_in_for_statement = false
for (int i = 0; i < x.Length; i++)
```

#### <a name="csharp_space_around_declaration_statements"></a><span data-ttu-id="39635-596">csharp_space_around_declaration_statements</span><span class="sxs-lookup"><span data-stu-id="39635-596">csharp_space_around_declaration_statements</span></span>

|<span data-ttu-id="39635-597">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-597">Property</span></span>|<span data-ttu-id="39635-598">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-598">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-599">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-599">**Option name**</span></span> | <span data-ttu-id="39635-600">csharp_space_around_declaration_statements</span><span class="sxs-lookup"><span data-stu-id="39635-600">csharp_space_around_declaration_statements</span></span> |
| <span data-ttu-id="39635-601">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-601">**Applicable languages**</span></span> | <span data-ttu-id="39635-602">C#</span><span class="sxs-lookup"><span data-stu-id="39635-602">C#</span></span> |
| <span data-ttu-id="39635-603">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-603">**Option values**</span></span> | <span data-ttu-id="39635-604">`ignore` — Nie usuwaj dodatkowych znaków spacji w instrukcjach deklaracji</span><span class="sxs-lookup"><span data-stu-id="39635-604">`ignore` - Don't remove extra space characters in declaration statements</span></span><br /><br /><span data-ttu-id="39635-605">`false` -Usuń dodatkowe znaki spacji w instrukcjach deklaracji</span><span class="sxs-lookup"><span data-stu-id="39635-605">`false` - Remove extra space characters in declaration statements</span></span> |

<span data-ttu-id="39635-606">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-606">Code examples:</span></span>

```csharp
// csharp_space_around_declaration_statements = ignore
int    x    =    0   ;

// csharp_space_around_declaration_statements = false
int x = 0;
```

#### <a name="csharp_space_before_open_square_brackets"></a><span data-ttu-id="39635-607">csharp_space_before_open_square_brackets</span><span class="sxs-lookup"><span data-stu-id="39635-607">csharp_space_before_open_square_brackets</span></span>

|<span data-ttu-id="39635-608">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-608">Property</span></span>|<span data-ttu-id="39635-609">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-609">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-610">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-610">**Option name**</span></span> | <span data-ttu-id="39635-611">csharp_space_before_open_square_brackets</span><span class="sxs-lookup"><span data-stu-id="39635-611">csharp_space_before_open_square_brackets</span></span> |
| <span data-ttu-id="39635-612">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-612">**Applicable languages**</span></span> | <span data-ttu-id="39635-613">C#</span><span class="sxs-lookup"><span data-stu-id="39635-613">C#</span></span> |
| <span data-ttu-id="39635-614">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-614">**Option values**</span></span> | <span data-ttu-id="39635-615">`true` -Wstaw spację przed otwierającymi nawiasami kwadratowymi `[`</span><span class="sxs-lookup"><span data-stu-id="39635-615">`true` - Insert space before opening square brackets `[`</span></span> <br /><br /><span data-ttu-id="39635-616">`false` -Usuń spację przed otwierającymi nawiasami kwadratowymi `[`</span><span class="sxs-lookup"><span data-stu-id="39635-616">`false` - Remove space before opening square brackets `[`</span></span> |

<span data-ttu-id="39635-617">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-617">Code examples:</span></span>

```csharp
// csharp_space_before_open_square_brackets = true
int [] numbers = new int [] { 1, 2, 3, 4, 5 };

// csharp_space_before_open_square_brackets = false
int[] numbers = new int[] { 1, 2, 3, 4, 5 };
```

#### <a name="csharp_space_between_empty_square_brackets"></a><span data-ttu-id="39635-618">csharp_space_between_empty_square_brackets</span><span class="sxs-lookup"><span data-stu-id="39635-618">csharp_space_between_empty_square_brackets</span></span>

|<span data-ttu-id="39635-619">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-619">Property</span></span>|<span data-ttu-id="39635-620">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-620">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-621">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-621">**Option name**</span></span> | <span data-ttu-id="39635-622">csharp_space_between_empty_square_brackets</span><span class="sxs-lookup"><span data-stu-id="39635-622">csharp_space_between_empty_square_brackets</span></span> |
| <span data-ttu-id="39635-623">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-623">**Applicable languages**</span></span> | <span data-ttu-id="39635-624">C#</span><span class="sxs-lookup"><span data-stu-id="39635-624">C#</span></span> |
| <span data-ttu-id="39635-625">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-625">**Option values**</span></span> | <span data-ttu-id="39635-626">`true` -Wstaw odstęp między pustymi nawiasami kwadratowymi `[ ]`</span><span class="sxs-lookup"><span data-stu-id="39635-626">`true` - Insert space between empty square brackets `[ ]`</span></span> <br /><br /><span data-ttu-id="39635-627">`false` -Usuń odstęp między pustymi nawiasami kwadratowymi `[]`</span><span class="sxs-lookup"><span data-stu-id="39635-627">`false` - Remove space between empty square brackets `[]`</span></span> |

<span data-ttu-id="39635-628">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-628">Code examples:</span></span>

```csharp
// csharp_space_between_empty_square_brackets = true
int[ ] numbers = new int[ ] { 1, 2, 3, 4, 5 };

// csharp_space_between_empty_square_brackets = false
int[] numbers = new int[] { 1, 2, 3, 4, 5 };
```

#### <a name="csharp_space_between_square_brackets"></a><span data-ttu-id="39635-629">csharp_space_between_square_brackets</span><span class="sxs-lookup"><span data-stu-id="39635-629">csharp_space_between_square_brackets</span></span>

|<span data-ttu-id="39635-630">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-630">Property</span></span>|<span data-ttu-id="39635-631">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-631">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-632">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-632">**Option name**</span></span> | <span data-ttu-id="39635-633">csharp_space_between_square_brackets</span><span class="sxs-lookup"><span data-stu-id="39635-633">csharp_space_between_square_brackets</span></span> |
| <span data-ttu-id="39635-634">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-634">**Applicable languages**</span></span> | <span data-ttu-id="39635-635">C#</span><span class="sxs-lookup"><span data-stu-id="39635-635">C#</span></span> |
| <span data-ttu-id="39635-636">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-636">**Option values**</span></span> | <span data-ttu-id="39635-637">`true` -Wstaw znaki spacji w niepustych nawiasach kwadratowych `[ 0 ]`</span><span class="sxs-lookup"><span data-stu-id="39635-637">`true` - Insert space characters in non-empty square brackets `[ 0 ]`</span></span> <br /><br /><span data-ttu-id="39635-638">`false` -Usuń spacje w nawiasach kwadratowych, które nie są puste `[0]`</span><span class="sxs-lookup"><span data-stu-id="39635-638">`false` - Remove space characters in non-empty square brackets `[0]`</span></span> |

<span data-ttu-id="39635-639">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-639">Code examples:</span></span>

```csharp
// csharp_space_between_square_brackets = true
int index = numbers[ 0 ];

// csharp_space_between_square_brackets = false
int index = numbers[0];
```

### <a name="wrap-options"></a><span data-ttu-id="39635-640">Opcje zawijania</span><span class="sxs-lookup"><span data-stu-id="39635-640">Wrap options</span></span>

<span data-ttu-id="39635-641">Te reguły formatowania dotyczą korzystania z pojedynczych wierszy w oddzielnym wierszu dla instrukcji i bloków kodu.</span><span class="sxs-lookup"><span data-stu-id="39635-641">These formatting rules concern the use of single lines versus separate lines for statements and code blocks.</span></span>

<span data-ttu-id="39635-642">Przykładowy plik *. editorconfig* :</span><span class="sxs-lookup"><span data-stu-id="39635-642">Example *.editorconfig* file:</span></span>

```ini
# CSharp formatting rules:
[*.cs]
csharp_preserve_single_line_statements = true
csharp_preserve_single_line_blocks = true
```

#### <a name="csharp_preserve_single_line_statements"></a><span data-ttu-id="39635-643">csharp_preserve_single_line_statements</span><span class="sxs-lookup"><span data-stu-id="39635-643">csharp_preserve_single_line_statements</span></span>

|<span data-ttu-id="39635-644">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-644">Property</span></span>|<span data-ttu-id="39635-645">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-645">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-646">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-646">**Option name**</span></span> | <span data-ttu-id="39635-647">csharp_preserve_single_line_statements</span><span class="sxs-lookup"><span data-stu-id="39635-647">csharp_preserve_single_line_statements</span></span> |
| <span data-ttu-id="39635-648">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-648">**Applicable languages**</span></span> | <span data-ttu-id="39635-649">C#</span><span class="sxs-lookup"><span data-stu-id="39635-649">C#</span></span> |
| <span data-ttu-id="39635-650">**Wprowadzona wersja**</span><span class="sxs-lookup"><span data-stu-id="39635-650">**Introduced version**</span></span> | <span data-ttu-id="39635-651">Visual Studio 2017, wersja 15.3</span><span class="sxs-lookup"><span data-stu-id="39635-651">Visual Studio 2017 version 15.3</span></span> |
| <span data-ttu-id="39635-652">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-652">**Option values**</span></span> | <span data-ttu-id="39635-653">`true` -Pozostaw instrukcje i deklaracje składowych w tym samym wierszu</span><span class="sxs-lookup"><span data-stu-id="39635-653">`true` - Leave statements and member declarations on the same line</span></span><br /><br /><span data-ttu-id="39635-654">`false` — Pozostaw instrukcje i deklaracje składowych w różnych wierszach</span><span class="sxs-lookup"><span data-stu-id="39635-654">`false` - Leave statements and member declarations on different lines</span></span> |

<span data-ttu-id="39635-655">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-655">Code examples:</span></span>

```csharp
//csharp_preserve_single_line_statements = true
int i = 0; string name = "John";

//csharp_preserve_single_line_statements = false
int i = 0;
string name = "John";
```

#### <a name="csharp_preserve_single_line_blocks"></a><span data-ttu-id="39635-656">csharp_preserve_single_line_blocks</span><span class="sxs-lookup"><span data-stu-id="39635-656">csharp_preserve_single_line_blocks</span></span>

|<span data-ttu-id="39635-657">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-657">Property</span></span>|<span data-ttu-id="39635-658">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-658">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-659">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-659">**Option name**</span></span> | <span data-ttu-id="39635-660">csharp_preserve_single_line_blocks</span><span class="sxs-lookup"><span data-stu-id="39635-660">csharp_preserve_single_line_blocks</span></span> |
| <span data-ttu-id="39635-661">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-661">**Applicable languages**</span></span> | <span data-ttu-id="39635-662">C#</span><span class="sxs-lookup"><span data-stu-id="39635-662">C#</span></span> |
| <span data-ttu-id="39635-663">**Wprowadzona wersja**</span><span class="sxs-lookup"><span data-stu-id="39635-663">**Introduced version**</span></span> | <span data-ttu-id="39635-664">Visual Studio 2017, wersja 15.3</span><span class="sxs-lookup"><span data-stu-id="39635-664">Visual Studio 2017 version 15.3</span></span> |
| <span data-ttu-id="39635-665">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-665">**Option values**</span></span> | <span data-ttu-id="39635-666">`true` — Pozostaw blok kodu w pojedynczym wierszu</span><span class="sxs-lookup"><span data-stu-id="39635-666">`true` - Leave code block on single line</span></span><br /><br /><span data-ttu-id="39635-667">`false` — Pozostaw blok kodu w osobnych wierszach</span><span class="sxs-lookup"><span data-stu-id="39635-667">`false` - Leave code block on separate lines</span></span> |

<span data-ttu-id="39635-668">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-668">Code examples:</span></span>

```csharp
//csharp_preserve_single_line_blocks = true
public int Foo { get; set; }

//csharp_preserve_single_line_blocks = false
public int MyProperty
{
    get; set;
}
```

### <a name="using-directive-options"></a><span data-ttu-id="39635-669">Korzystanie z opcji dyrektywy</span><span class="sxs-lookup"><span data-stu-id="39635-669">Using directive options</span></span>

<span data-ttu-id="39635-670">Ta reguła formatowania ma wpływ na użycie dyrektyw using umieszczonych wewnątrz i poza obszarem nazw.</span><span class="sxs-lookup"><span data-stu-id="39635-670">This formatting rule concerns the use of using directives being placed inside versus outside a namespace.</span></span>

<span data-ttu-id="39635-671">Przykładowy plik *. editorconfig* :</span><span class="sxs-lookup"><span data-stu-id="39635-671">Example *.editorconfig* file:</span></span>

```ini
# 'using' directive preferences
[*.cs]
csharp_using_directive_placement = outside_namespace
csharp_using_directive_placement = inside_namespace
```

#### <a name="csharp_using_directive_placement"></a><span data-ttu-id="39635-672">csharp_using_directive_placement</span><span class="sxs-lookup"><span data-stu-id="39635-672">csharp_using_directive_placement</span></span>

|<span data-ttu-id="39635-673">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39635-673">Property</span></span>|<span data-ttu-id="39635-674">Wartość</span><span class="sxs-lookup"><span data-stu-id="39635-674">Value</span></span>|
|-|-|
| <span data-ttu-id="39635-675">**Nazwa opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-675">**Option name**</span></span> | <span data-ttu-id="39635-676">csharp_using_directive_placement</span><span class="sxs-lookup"><span data-stu-id="39635-676">csharp_using_directive_placement</span></span> |
| <span data-ttu-id="39635-677">**Odpowiednie języki**</span><span class="sxs-lookup"><span data-stu-id="39635-677">**Applicable languages**</span></span> | <span data-ttu-id="39635-678">C#</span><span class="sxs-lookup"><span data-stu-id="39635-678">C#</span></span> |
| <span data-ttu-id="39635-679">**Wprowadzona wersja**</span><span class="sxs-lookup"><span data-stu-id="39635-679">**Introduced version**</span></span> | <span data-ttu-id="39635-680">Visual Studio 2019 w wersji 16.1</span><span class="sxs-lookup"><span data-stu-id="39635-680">Visual Studio 2019 version 16.1</span></span> |
| <span data-ttu-id="39635-681">**Wartości opcji**</span><span class="sxs-lookup"><span data-stu-id="39635-681">**Option values**</span></span> | <span data-ttu-id="39635-682">`outside_namespace` -Pozostaw dyrektywy using poza obszarem nazw</span><span class="sxs-lookup"><span data-stu-id="39635-682">`outside_namespace` - Leave using directives outside namespace</span></span><br /><br /><span data-ttu-id="39635-683">`inside_namespace` -Pozostaw dyrektywy using w przestrzeni nazw</span><span class="sxs-lookup"><span data-stu-id="39635-683">`inside_namespace` - Leave using directives inside namespace</span></span> |

<span data-ttu-id="39635-684">Przykłady kodu:</span><span class="sxs-lookup"><span data-stu-id="39635-684">Code examples:</span></span>

```csharp
// csharp_using_directive_placement = outside_namespace
using System;

namespace Conventions
{

}

// csharp_using_directive_placement = inside_namespace
namespace Conventions
{
    using System;
}
```

## <a name="see-also"></a><span data-ttu-id="39635-685">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="39635-685">See also</span></span>

- [<span data-ttu-id="39635-686">Reguły języka</span><span class="sxs-lookup"><span data-stu-id="39635-686">Language rules</span></span>](language-rules.md)
- [<span data-ttu-id="39635-687">Reguły nazewnictwa</span><span class="sxs-lookup"><span data-stu-id="39635-687">Naming rules</span></span>](naming-rules.md)
- [<span data-ttu-id="39635-688">Dokumentacja reguł stylu kodu platformy .NET</span><span class="sxs-lookup"><span data-stu-id="39635-688">.NET code style rules reference</span></span>](index.md)
