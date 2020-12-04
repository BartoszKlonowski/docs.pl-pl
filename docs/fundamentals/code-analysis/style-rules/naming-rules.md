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
# <a name="naming-rules"></a><span data-ttu-id="6cb33-103">Reguły nazewnictwa</span><span class="sxs-lookup"><span data-stu-id="6cb33-103">Naming rules</span></span>

<span data-ttu-id="6cb33-104">Reguły nazewnictwa dotyczą nazewnictwa elementów kodu języka programowania .NET, takich jak klasy, właściwości i metody.</span><span class="sxs-lookup"><span data-stu-id="6cb33-104">Naming rules concern the naming of .NET programming language code elements, such as classes, properties, and methods.</span></span> <span data-ttu-id="6cb33-105">Można na przykład określić, że publiczne składowe muszą być pisane wielkimi literami, lub pola prywatne muszą zaczynać się od `_` .</span><span class="sxs-lookup"><span data-stu-id="6cb33-105">For example, you can specify that public members must be capitalized or that private fields must begin with `_`.</span></span>

<span data-ttu-id="6cb33-106">Reguła nazewnictwa ma trzy części:</span><span class="sxs-lookup"><span data-stu-id="6cb33-106">A naming rule has three parts:</span></span>

* <span data-ttu-id="6cb33-107">Grupa symboli, do której się odnosi.</span><span class="sxs-lookup"><span data-stu-id="6cb33-107">The group of symbols it applies to.</span></span>
* <span data-ttu-id="6cb33-108">Styl nazewnictwa, który ma zostać skojarzony z regułą.</span><span class="sxs-lookup"><span data-stu-id="6cb33-108">The naming style to associate with the rule.</span></span>
* <span data-ttu-id="6cb33-109">Ważność wymuszania Konwencji.</span><span class="sxs-lookup"><span data-stu-id="6cb33-109">The severity for enforcing the convention.</span></span>

<span data-ttu-id="6cb33-110">Reguły nazewnictwa są definiowane w pliku EditorConfig.</span><span class="sxs-lookup"><span data-stu-id="6cb33-110">You define naming rules in an EditorConfig file.</span></span>

## <a name="general-syntax"></a><span data-ttu-id="6cb33-111">Składnia ogólna</span><span class="sxs-lookup"><span data-stu-id="6cb33-111">General syntax</span></span>

<span data-ttu-id="6cb33-112">Aby zdefiniować regułę nazewnictwa, grupę symboli lub styl nazewnictwa, należy ustawić jedną lub więcej właściwości, używając następującej składni:</span><span class="sxs-lookup"><span data-stu-id="6cb33-112">To define a naming rule, symbol group, or naming style, set one or more properties using the following syntax:</span></span>

```ini
<prefix>.<title>.<propertyName> = <propertyValue>
```

<span data-ttu-id="6cb33-113">Każda właściwość powinna być ustawiona tylko raz, ale niektóre ustawienia dopuszczają wiele wartości rozdzielanych przecinkami.</span><span class="sxs-lookup"><span data-stu-id="6cb33-113">Each property should only be set once, but some settings allow multiple, comma-separated values.</span></span>

<span data-ttu-id="6cb33-114">Kolejność właściwości nie jest ważna.</span><span class="sxs-lookup"><span data-stu-id="6cb33-114">The order of the properties is not important.</span></span>

### \<prefix>

<span data-ttu-id="6cb33-115">**\<prefix>** Określa, jakiego rodzaju elementu jest definiowana &mdash; reguła nazewnictwa, Grupa symboli lub styl nazewnictwa, &mdash; i musi mieć jedną z następujących wartości:</span><span class="sxs-lookup"><span data-stu-id="6cb33-115">**\<prefix>** specifies which kind of element is being defined&mdash;naming rule, symbol group, or naming style&mdash;and must be one of the following:</span></span>

| <span data-ttu-id="6cb33-116">Aby ustawić właściwość dla</span><span class="sxs-lookup"><span data-stu-id="6cb33-116">To set a property for</span></span> | <span data-ttu-id="6cb33-117">Użyj prefiksu</span><span class="sxs-lookup"><span data-stu-id="6cb33-117">Use the prefix</span></span> | <span data-ttu-id="6cb33-118">Przykład</span><span class="sxs-lookup"><span data-stu-id="6cb33-118">Example</span></span> |
| --- | --- | -- |
| <span data-ttu-id="6cb33-119">Reguła nazewnictwa</span><span class="sxs-lookup"><span data-stu-id="6cb33-119">Naming rule</span></span> | `dotnet_naming_rule` | `dotnet_naming_rule.types_should_be_pascal_case.severity = suggestion` |
| <span data-ttu-id="6cb33-120">Grupa symboli</span><span class="sxs-lookup"><span data-stu-id="6cb33-120">Symbol group</span></span> | `dotnet_naming_symbols` | `dotnet_naming_symbols.interface.applicable_kinds = interface` |
| <span data-ttu-id="6cb33-121">Styl nazewnictwa</span><span class="sxs-lookup"><span data-stu-id="6cb33-121">Naming style</span></span> | `dotnet_naming_style` | `dotnet_naming_style.pascal_case.capitalization = pascal_case` |

<span data-ttu-id="6cb33-122">Każdy typ &mdash; [reguły nazewnictwa](#naming-rule-properties)definicji, [grupy symboli](#symbol-group-properties)lub [stylu nazewnictwa](#naming-style-properties) &mdash; ma własne obsługiwane właściwości, zgodnie z opisem w poniższych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="6cb33-122">Each type of definition&mdash;[naming rule](#naming-rule-properties), [symbol group](#symbol-group-properties), or [naming style](#naming-style-properties)&mdash;has its own supported properties, as described in the following sections.</span></span>

### \<title>

<span data-ttu-id="6cb33-123">**\<title>** jest wybraną nazwą opisową, która kojarzy wiele ustawień właściwości w jedną definicję.</span><span class="sxs-lookup"><span data-stu-id="6cb33-123">**\<title>** is a descriptive name you choose that associates multiple property settings into a single definition.</span></span> <span data-ttu-id="6cb33-124">Na przykład następujące właściwości tworzą dwa definicje grup symboli `interface` i `types` , z których każdy ma ustawione dwie właściwości.</span><span class="sxs-lookup"><span data-stu-id="6cb33-124">For example, the following properties produce two symbol group definitions, `interface` and `types`, each of which has two properties set on it.</span></span>

```ini
dotnet_naming_symbols.interface.applicable_kinds = interface
dotnet_naming_symbols.interface.applicable_accessibilities = public, internal, private, protected, protected_internal, private_protected

dotnet_naming_symbols.types.applicable_kinds = class, struct, interface, enum, delegate
dotnet_naming_symbols.types.applicable_accessibilities = public, internal, private, protected, protected_internal, private_protected
```

## <a name="naming-rule-properties"></a><span data-ttu-id="6cb33-125">Właściwości reguły nazewnictwa</span><span class="sxs-lookup"><span data-stu-id="6cb33-125">Naming rule properties</span></span>

<span data-ttu-id="6cb33-126">Aby reguła zaczęła obowiązywać, wymagane są wszystkie właściwości reguły nazewnictwa.</span><span class="sxs-lookup"><span data-stu-id="6cb33-126">All naming rule properties are required for a rule to take effect.</span></span>

| <span data-ttu-id="6cb33-127">Właściwość</span><span class="sxs-lookup"><span data-stu-id="6cb33-127">Property</span></span> | <span data-ttu-id="6cb33-128">Opis</span><span class="sxs-lookup"><span data-stu-id="6cb33-128">Description</span></span> |
| -- | -- |
| `symbols` | <span data-ttu-id="6cb33-129">Tytuł grupy symboli definiujący symbole, do których ma zostać zastosowana ta reguła.</span><span class="sxs-lookup"><span data-stu-id="6cb33-129">The title of the symbol group, defining the symbols to which this rule should be applied</span></span> |
| `style` | <span data-ttu-id="6cb33-130">Tytuł stylu nazewnictwa, który powinien zostać skojarzony z tą regułą.</span><span class="sxs-lookup"><span data-stu-id="6cb33-130">The title of the naming style which should be associated with this rule</span></span> |
| `severity` |  <span data-ttu-id="6cb33-131">Ustawia ważność, przy której ma być wymuszana reguła nazewnictwa.</span><span class="sxs-lookup"><span data-stu-id="6cb33-131">Sets the severity with which to enforce the naming rule.</span></span> <span data-ttu-id="6cb33-132">Ustaw skojarzoną wartość na jeden z dostępnych [poziomów ważności](https://docs.microsoft.com/dotnet/fundamentals/code-analysis/configuration-options#severity-level). <sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="6cb33-132">Set the associated value to one of the available [severity levels](https://docs.microsoft.com/dotnet/fundamentals/code-analysis/configuration-options#severity-level).<sup>1</sup></span></span> |

<span data-ttu-id="6cb33-133">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="6cb33-133">**Notes:**</span></span>

1. <span data-ttu-id="6cb33-134">Specyfikacja ważności w ramach reguły nazewnictwa jest przestrzegana tylko w środowisk ideach programistycznych, takich jak program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6cb33-134">Severity specification within a naming rule is only respected inside development IDEs, such as Visual Studio.</span></span> <span data-ttu-id="6cb33-135">To ustawienie nie jest rozpoznawane przez kompilatory języka C# lub VB, dlatego nie jest przestrzegane podczas kompilacji.</span><span class="sxs-lookup"><span data-stu-id="6cb33-135">This setting is not understood by the C# or VB compilers, hence not respected during build.</span></span> <span data-ttu-id="6cb33-136">Zamiast tego, aby wymusić reguły stylu nazewnictwa w kompilacji, należy ustawić ważność przy użyciu konfiguracji o ważności opartej na IDENTYFIKATORze reguły zgodnie z opisem w [tej sekcji](#rule-id-ide1006-naming-rule-violation).</span><span class="sxs-lookup"><span data-stu-id="6cb33-136">Instead, to enforce naming style rules on build, you should set the severity by using the rule ID-based severity configuration as explained in [this section](#rule-id-ide1006-naming-rule-violation).</span></span> <span data-ttu-id="6cb33-137">Aby uzyskać więcej informacji, zobacz ten problem w serwisie [GitHub](https://github.com/dotnet/roslyn/issues/44201).</span><span class="sxs-lookup"><span data-stu-id="6cb33-137">For more information, see this [GitHub issue](https://github.com/dotnet/roslyn/issues/44201).</span></span>

## <a name="rule-order"></a><span data-ttu-id="6cb33-138">Kolejność reguł</span><span class="sxs-lookup"><span data-stu-id="6cb33-138">Rule order</span></span>

<span data-ttu-id="6cb33-139">Kolejność, w której reguły nazewnictwa są zdefiniowane w pliku EditorConfig, nie ma znaczenia.</span><span class="sxs-lookup"><span data-stu-id="6cb33-139">The order in which naming rules are defined in an EditorConfig file doesn't matter.</span></span> <span data-ttu-id="6cb33-140">Reguły nazewnictwa są automatycznie uporządkowane zgodnie z definicją samych reguł.</span><span class="sxs-lookup"><span data-stu-id="6cb33-140">The naming rules are automatically ordered according to the definition of the rules themselves.</span></span> <span data-ttu-id="6cb33-141">[Rozszerzenie usługi języka EditorConfig](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.EditorConfig) może analizować plik EditorConfig i zgłaszać przypadki, w których kolejność sortowania reguł w pliku różni się od tego, co kompilator będzie używać w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="6cb33-141">The [EditorConfig Language Service extension](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.EditorConfig) can analyze an EditorConfig file and report cases where the rule ordering in the file is different to what the compiler will use at run time.</span></span>

> [!NOTE]
>
> <span data-ttu-id="6cb33-142">Jeśli używasz wersji programu Visual Studio starszej niż Visual Studio 2019 w wersji 16,2, reguły nazewnictwa powinny być uporządkowane z najbardziej szczegółowych elementów w pliku EditorConfig.</span><span class="sxs-lookup"><span data-stu-id="6cb33-142">If you're using a version of Visual Studio earlier than Visual Studio 2019 version 16.2, naming rules should be ordered from most-specific to least-specific in the EditorConfig file.</span></span> <span data-ttu-id="6cb33-143">Pierwsza napotkana reguła jest jedyną zastosowanym regułą.</span><span class="sxs-lookup"><span data-stu-id="6cb33-143">The first rule encountered that can be applied is the only rule that is applied.</span></span> <span data-ttu-id="6cb33-144">Jeśli jednak istnieje wiele *Właściwości* reguł o tej samej nazwie, pierwszeństwo ma właściwość ostatnio znaleziona o tej nazwie.</span><span class="sxs-lookup"><span data-stu-id="6cb33-144">However, if there are multiple rule *properties* with the same name, the most recently found property with that name takes precedence.</span></span> <span data-ttu-id="6cb33-145">Aby uzyskać więcej informacji, zobacz [Hierarchia plików i pierwszeństwo](/visualstudio/ide/create-portable-custom-editor-options#file-hierarchy-and-precedence).</span><span class="sxs-lookup"><span data-stu-id="6cb33-145">For more information, see [File hierarchy and precedence](/visualstudio/ide/create-portable-custom-editor-options#file-hierarchy-and-precedence).</span></span>

## <a name="symbol-group-properties"></a><span data-ttu-id="6cb33-146">Właściwości grupy symboli</span><span class="sxs-lookup"><span data-stu-id="6cb33-146">Symbol group properties</span></span>

<span data-ttu-id="6cb33-147">Można ustawić następujące właściwości dla grup symboli, aby ograniczyć liczbę symboli uwzględnionych w grupie.</span><span class="sxs-lookup"><span data-stu-id="6cb33-147">You can set the following properties for symbol groups, to limit which symbols are included in the group.</span></span> <span data-ttu-id="6cb33-148">Aby określić wiele wartości w jednym ustawieniu właściwości, rozdziel je przecinkami.</span><span class="sxs-lookup"><span data-stu-id="6cb33-148">To specify multiple values in a single property setting, separate them with a comma.</span></span>

| <span data-ttu-id="6cb33-149">Właściwość</span><span class="sxs-lookup"><span data-stu-id="6cb33-149">Property</span></span> | <span data-ttu-id="6cb33-150">Opis</span><span class="sxs-lookup"><span data-stu-id="6cb33-150">Description</span></span> | <span data-ttu-id="6cb33-151">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="6cb33-151">Allowed values</span></span> | <span data-ttu-id="6cb33-152">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6cb33-152">Required</span></span> |
| -- | -- | -- | -- |
| `applicable_kinds` | <span data-ttu-id="6cb33-153">Rodzaje symboli w grupie <sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="6cb33-153">Kinds of symbols in the group <sup>1</sup></span></span> | <span data-ttu-id="6cb33-154">`*` (Użyj tej wartości, aby określić wszystkie symbole)</span><span class="sxs-lookup"><span data-stu-id="6cb33-154">`*` (use this value to specify all symbols)</span></span><br/>`namespace`<br/>`class`<br/>`struct`<br/>`interface`<br/>`enum`<br/>`property`<br/>`method`<br/>`field`<br/>`event`<br/>`delegate`<br/>`parameter`<br/>`type_parameter`<br/>`local`<br/>`local_function` | <span data-ttu-id="6cb33-155">Tak</span><span class="sxs-lookup"><span data-stu-id="6cb33-155">Yes</span></span> |
| `applicable_accessibilities` | <span data-ttu-id="6cb33-156">Poziomy ułatwień dostępu symboli w grupie</span><span class="sxs-lookup"><span data-stu-id="6cb33-156">Accessibility levels of the symbols in the group</span></span> | <span data-ttu-id="6cb33-157">`*` (Użyj tej wartości, aby określić wszystkie poziomy ułatwień dostępu)</span><span class="sxs-lookup"><span data-stu-id="6cb33-157">`*` (use this value to specify all accessibility levels)</span></span><br/>`public`<br/><span data-ttu-id="6cb33-158">`internal` lub `friend`</span><span class="sxs-lookup"><span data-stu-id="6cb33-158">`internal` or `friend`</span></span><br/>`private`<br/>`protected`<br/><span data-ttu-id="6cb33-159">`protected_internal` lub `protected_friend`</span><span class="sxs-lookup"><span data-stu-id="6cb33-159">`protected_internal` or `protected_friend`</span></span><br/>`private_protected`<br/><span data-ttu-id="6cb33-160">`local` (dla symboli zdefiniowanych w ramach metody)</span><span class="sxs-lookup"><span data-stu-id="6cb33-160">`local` (for symbols defined within a method)</span></span> | <span data-ttu-id="6cb33-161">Tak</span><span class="sxs-lookup"><span data-stu-id="6cb33-161">Yes</span></span> |
| `required_modifiers` | <span data-ttu-id="6cb33-162">Dopasowuje tylko symbole ze _wszystkimi_ określonymi modyfikatorami <sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="6cb33-162">Only match symbols with _all_ the specified modifiers <sup>2</sup></span></span> | <span data-ttu-id="6cb33-163">`abstract` lub `must_inherit`</span><span class="sxs-lookup"><span data-stu-id="6cb33-163">`abstract` or `must_inherit`</span></span><br/>`async`<br/>`const`<br/>`readonly`<br/><span data-ttu-id="6cb33-164">`static` lub `shared` <sup>3</sup></span><span class="sxs-lookup"><span data-stu-id="6cb33-164">`static` or `shared` <sup>3</sup></span></span> | <span data-ttu-id="6cb33-165">Nie</span><span class="sxs-lookup"><span data-stu-id="6cb33-165">No</span></span> |

<span data-ttu-id="6cb33-166">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="6cb33-166">**Notes:**</span></span>

1. <span data-ttu-id="6cb33-167">Elementy członkowskie krotek nie są obecnie obsługiwane w programie `applicable_kinds` .</span><span class="sxs-lookup"><span data-stu-id="6cb33-167">Tuple members aren't currently supported in `applicable_kinds`.</span></span>
2. <span data-ttu-id="6cb33-168">Grupa symboli dopasowuje _wszystkie_ Modyfikatory we `required_modifiers` właściwości.</span><span class="sxs-lookup"><span data-stu-id="6cb33-168">The symbol group matches _all_ the modifiers in the `required_modifiers` property.</span></span>  <span data-ttu-id="6cb33-169">W przypadku pominięcia tej właściwości nie są wymagane żadne specyficzne Modyfikatory dla dopasowania.</span><span class="sxs-lookup"><span data-stu-id="6cb33-169">If you omit this property, no specific modifiers are required for a match.</span></span> <span data-ttu-id="6cb33-170">Oznacza to, że Modyfikatory symbolu nie mają wpływu na to, czy ta reguła jest stosowana.</span><span class="sxs-lookup"><span data-stu-id="6cb33-170">This means a symbol's modifiers have no effect on whether or not this rule is applied.</span></span>
3. <span data-ttu-id="6cb33-171">Jeśli grupa ma `static` lub `shared` we `required_modifiers` właściwości, grupa będzie zawierać również `const` symbole, ponieważ są one niejawnie `static` / `Shared` .</span><span class="sxs-lookup"><span data-stu-id="6cb33-171">If your group has `static` or `shared` in the `required_modifiers` property, the group will also include `const` symbols because they are implicitly `static`/`Shared`.</span></span> <span data-ttu-id="6cb33-172">Jeśli jednak `static` reguły nazewnictwa nie mają być stosowane do `const` symboli, można utworzyć nową regułę nazewnictwa z grupą symboli `const` .</span><span class="sxs-lookup"><span data-stu-id="6cb33-172">However, if you don't want the `static` naming rule to apply to `const` symbols, you can create a new naming rule with a symbol group of `const`.</span></span>

## <a name="naming-style-properties"></a><span data-ttu-id="6cb33-173">Właściwości stylu nazewnictwa</span><span class="sxs-lookup"><span data-stu-id="6cb33-173">Naming style properties</span></span>

<span data-ttu-id="6cb33-174">Styl nazewnictwa definiuje konwencje, które mają zostać wymuszone przez regułę.</span><span class="sxs-lookup"><span data-stu-id="6cb33-174">A naming style defines the conventions you want to enforce with the rule.</span></span> <span data-ttu-id="6cb33-175">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="6cb33-175">For example:</span></span>

* <span data-ttu-id="6cb33-176">Używaj wielką literą `PascalCase`</span><span class="sxs-lookup"><span data-stu-id="6cb33-176">Capitalize with `PascalCase`</span></span>
* <span data-ttu-id="6cb33-177">Rozpoczyna się od `m_`</span><span class="sxs-lookup"><span data-stu-id="6cb33-177">Starts with `m_`</span></span>
* <span data-ttu-id="6cb33-178">Kończący się na `_g`</span><span class="sxs-lookup"><span data-stu-id="6cb33-178">Ends with `_g`</span></span>
* <span data-ttu-id="6cb33-179">Oddziel wyrazy `__`</span><span class="sxs-lookup"><span data-stu-id="6cb33-179">Separate words with `__`</span></span>

<span data-ttu-id="6cb33-180">Dla stylu nazewnictwa można ustawić następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="6cb33-180">You can set the following properties for a naming style:</span></span>

| <span data-ttu-id="6cb33-181">Właściwość</span><span class="sxs-lookup"><span data-stu-id="6cb33-181">Property</span></span> | <span data-ttu-id="6cb33-182">Opis</span><span class="sxs-lookup"><span data-stu-id="6cb33-182">Description</span></span> | <span data-ttu-id="6cb33-183">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="6cb33-183">Allowed values</span></span> | <span data-ttu-id="6cb33-184">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6cb33-184">Required</span></span> |
| -- | -- | -- | -- |
| `capitalization` | <span data-ttu-id="6cb33-185">Styl wersalików dla słów w symbolu</span><span class="sxs-lookup"><span data-stu-id="6cb33-185">Capitalization style for words within the symbol</span></span> | `pascal_case`<br/>`camel_case`<br/>`first_word_upper`<br/>`all_upper`<br/>`all_lower` | <span data-ttu-id="6cb33-186">Tak<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="6cb33-186">Yes<sup>1</sup></span></span> |
| `required_prefix` | <span data-ttu-id="6cb33-187">Musi zaczynać się od tych znaków</span><span class="sxs-lookup"><span data-stu-id="6cb33-187">Must begin with these characters</span></span> | | <span data-ttu-id="6cb33-188">Nie</span><span class="sxs-lookup"><span data-stu-id="6cb33-188">No</span></span> |
| `required_suffix` | <span data-ttu-id="6cb33-189">Musi kończyć się tymi znakami</span><span class="sxs-lookup"><span data-stu-id="6cb33-189">Must end with these characters</span></span> | | <span data-ttu-id="6cb33-190">Nie</span><span class="sxs-lookup"><span data-stu-id="6cb33-190">No</span></span> |
| `word_separator` | <span data-ttu-id="6cb33-191">Słowa w symbolu muszą być rozdzielone znakiem tego znaku</span><span class="sxs-lookup"><span data-stu-id="6cb33-191">Words within the symbol need to be separated with this character</span></span> | | <span data-ttu-id="6cb33-192">Nie</span><span class="sxs-lookup"><span data-stu-id="6cb33-192">No</span></span> |

<span data-ttu-id="6cb33-193">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="6cb33-193">**Notes:**</span></span>

1. <span data-ttu-id="6cb33-194">Należy określić styl kapitalizacji jako część stylu nazewnictwa. w przeciwnym razie styl nazewnictwa może zostać zignorowany.</span><span class="sxs-lookup"><span data-stu-id="6cb33-194">You must specify a capitalization style as part of your naming style, otherwise your naming style might be ignored.</span></span>

## <a name="default-naming-styles"></a><span data-ttu-id="6cb33-195">Domyślne style nazewnictwa</span><span class="sxs-lookup"><span data-stu-id="6cb33-195">Default naming styles</span></span>

<span data-ttu-id="6cb33-196">Jeśli nie określisz żadnych niestandardowych reguł nazewnictwa, zostaną użyte następujące style domyślne:</span><span class="sxs-lookup"><span data-stu-id="6cb33-196">If you don't specify any custom naming rules, the following default styles are used:</span></span>

- <span data-ttu-id="6cb33-197">W przypadku klas, struktur, wyliczeń, właściwości i zdarzeń z `public` , `private` , `internal` ,, `protected` lub `protected_internal` dostępności, domyślny styl nazewnictwa to przypadek Pascal.</span><span class="sxs-lookup"><span data-stu-id="6cb33-197">For classes, structs, enumerations, properties, and events with `public`, `private`, `internal`, `protected`, or `protected_internal` accessibility, the default naming style is Pascal case.</span></span>

- <span data-ttu-id="6cb33-198">W przypadku interfejsów z `public` ,,,, `private` `internal` `protected` lub `protected_internal` dostępności, domyślny styl nazewnictwa jest przypadek Pascal z wymaganym prefiksem **I**.</span><span class="sxs-lookup"><span data-stu-id="6cb33-198">For interfaces with `public`, `private`, `internal`, `protected`, or `protected_internal` accessibility, the default naming style is Pascal case with a required prefix of **I**.</span></span>

## <a name="example"></a><span data-ttu-id="6cb33-199">Przykład</span><span class="sxs-lookup"><span data-stu-id="6cb33-199">Example</span></span>

<span data-ttu-id="6cb33-200">Następujący plik *. editorconfig* zawiera konwencję nazewnictwa, która określa, że właściwości publiczne, metody, pola, zdarzenia i Delegaty muszą być pisane wielkimi literami.</span><span class="sxs-lookup"><span data-stu-id="6cb33-200">The following *.editorconfig* file contains a naming convention that specifies that public properties, methods, fields, events, and delegates must be capitalized.</span></span> <span data-ttu-id="6cb33-201">Należy zauważyć, że ta konwencja nazewnictwa określa wiele rodzajów symboli, do których ma zostać zastosowana reguła, przy użyciu przecinka do oddzielenia wartości.</span><span class="sxs-lookup"><span data-stu-id="6cb33-201">Notice that this naming convention specifies multiple kinds of symbol to apply the rule to, using a comma to separate the values.</span></span>

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

## <a name="rule-id-ide1006-naming-rule-violation"></a><a name="rule-id-ide1006-naming-rule-violation"></a><span data-ttu-id="6cb33-202">Identyfikator reguły: "IDE1006" (naruszenie reguły nazewnictwa)</span><span class="sxs-lookup"><span data-stu-id="6cb33-202">Rule ID: "IDE1006" (Naming rule violation)</span></span>

<span data-ttu-id="6cb33-203">Wszystkie opcje nazewnictwa mają Identyfikator reguły `IDE1006` i tytuł `Naming rule violation` .</span><span class="sxs-lookup"><span data-stu-id="6cb33-203">All naming options have rule ID `IDE1006` and title `Naming rule violation`.</span></span> <span data-ttu-id="6cb33-204">Ważność naruszeń nazw można skonfigurować globalnie w pliku EditorConfig o następującej składni:</span><span class="sxs-lookup"><span data-stu-id="6cb33-204">You can configure the severity of naming violations globally in an EditorConfig file with the following syntax:</span></span>

```ini
dotnet_diagnostic.IDE1006.severity = <severity value>
```

<span data-ttu-id="6cb33-205">Wartość ważności musi być `warning` `error` [wymuszana w kompilacji](../overview.md#code-style-analysis).</span><span class="sxs-lookup"><span data-stu-id="6cb33-205">The severity value must be `warning` or `error` to be [enforced on build](../overview.md#code-style-analysis).</span></span> <span data-ttu-id="6cb33-206">Dla wszystkich możliwych wartości ważności zobacz [poziom ważności](../configuration-options.md#severity-level).</span><span class="sxs-lookup"><span data-stu-id="6cb33-206">For all possible severity values, see [severity level](../configuration-options.md#severity-level).</span></span>

## <a name="see-also"></a><span data-ttu-id="6cb33-207">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="6cb33-207">See also</span></span>

- [<span data-ttu-id="6cb33-208">Reguły języka</span><span class="sxs-lookup"><span data-stu-id="6cb33-208">Language rules</span></span>](language-rules.md)
- [<span data-ttu-id="6cb33-209">Reguły formatowania</span><span class="sxs-lookup"><span data-stu-id="6cb33-209">Formatting rules</span></span>](formatting-rules.md)
- [<span data-ttu-id="6cb33-210">Roslyn reguły nazewnictwa</span><span class="sxs-lookup"><span data-stu-id="6cb33-210">Roslyn naming rules</span></span>](https://github.com/dotnet/roslyn/blob/master/.editorconfig#L63)
- [<span data-ttu-id="6cb33-211">Dokumentacja reguł stylu kodu platformy .NET</span><span class="sxs-lookup"><span data-stu-id="6cb33-211">.NET code style rules reference</span></span>](index.md)
