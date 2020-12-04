---
title: Konfigurowanie reguł analizy kodu
description: Dowiedz się, jak skonfigurować reguły analizy kodu w pliku konfiguracji analizatora.
ms.date: 09/24/2020
ms.topic: conceptual
no-loc:
- EditorConfig
ms.openlocfilehash: af2ebb74786f0ae884ffee4636765cae43fcb23f
ms.sourcegitcommit: 97405ed212f69b0a32faa66a5d5fae7e76628b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/01/2020
ms.locfileid: "96589336"
---
# <a name="configuration-options-for-code-analysis"></a><span data-ttu-id="fd40e-103">Opcje konfiguracji na potrzeby analizy kodu</span><span class="sxs-lookup"><span data-stu-id="fd40e-103">Configuration options for code analysis</span></span>

<span data-ttu-id="fd40e-104">Reguły analizy kodu mają różne opcje konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="fd40e-104">Code analysis rules have various configuration options.</span></span> <span data-ttu-id="fd40e-105">Te opcje są określone jako pary klucz-wartość w [pliku konfiguracji analizatora](configuration-files.md) przy użyciu składni `<option key> = <option value>` .</span><span class="sxs-lookup"><span data-stu-id="fd40e-105">These options are specified as key-value pairs in an [analyzer configuration file](configuration-files.md) using the syntax `<option key> = <option value>`.</span></span>

<span data-ttu-id="fd40e-106">Najbardziej typową opcją, którą skonfigurujesz, jest ważność reguły.</span><span class="sxs-lookup"><span data-stu-id="fd40e-106">The most common option you'll configure is a rule's severity.</span></span> <span data-ttu-id="fd40e-107">Można skonfigurować poziom ważności dla wszystkich reguł analizatora, w tym [reguły jakości kodu](quality-rules/index.md) i [reguły stylu kodu](style-rules/index.md).</span><span class="sxs-lookup"><span data-stu-id="fd40e-107">You can configure severity level for all analyzer rules, including [code quality rules](quality-rules/index.md) and [code style rules](style-rules/index.md).</span></span>

<span data-ttu-id="fd40e-108">Możesz również skonfigurować dodatkowe opcje, aby dostosować zachowanie reguły:</span><span class="sxs-lookup"><span data-stu-id="fd40e-108">You can also configure additional options to customize rule behavior:</span></span>

- <span data-ttu-id="fd40e-109">Reguły jakości kodu zawierają [dodatkowe opcje](code-quality-rule-options.md) konfigurowania zachowania, takie jak nazwa metody, do której ma zastosowanie reguła.</span><span class="sxs-lookup"><span data-stu-id="fd40e-109">Code quality rules have [additional options](code-quality-rule-options.md) to configure behavior, such as which method names a rule should apply to.</span></span>
- <span data-ttu-id="fd40e-110">Reguły stylu kodu mają [niestandardowe opcje stylu kodu](code-style-rule-options.md).</span><span class="sxs-lookup"><span data-stu-id="fd40e-110">Code style rules have [custom code style options](code-style-rule-options.md).</span></span>
- <span data-ttu-id="fd40e-111">Reguły analizatora innych firm mogą definiować własne opcje konfiguracji z niestandardowymi nazwami kluczy i formatami wartości.</span><span class="sxs-lookup"><span data-stu-id="fd40e-111">Third party analyzer rules can define their own configuration options, with custom key names and value formats.</span></span>

<span data-ttu-id="fd40e-112">Składnia służąca do konfigurowania ważności określonej reguły w [pliku konfiguracyjnym analizatora](configuration-files.md) jest następująca:</span><span class="sxs-lookup"><span data-stu-id="fd40e-112">The syntax for configuring a specific rule's severity in an [analyzer configuration file](configuration-files.md) is as follows:</span></span>

```ini
dotnet_diagnostic.<rule ID>.severity = <severity>
```

## <a name="general-options"></a><span data-ttu-id="fd40e-113">Opcje ogólne</span><span class="sxs-lookup"><span data-stu-id="fd40e-113">General options</span></span>

<span data-ttu-id="fd40e-114">Te opcje mają zastosowanie do analizy kodu jako całości.</span><span class="sxs-lookup"><span data-stu-id="fd40e-114">These options apply to code analysis as a whole.</span></span> <span data-ttu-id="fd40e-115">Nie można ich stosować tylko do jednej reguły lub zestawu reguł.</span><span class="sxs-lookup"><span data-stu-id="fd40e-115">They cannot be applied only to a single rule or set of rules.</span></span>

### <a name="exclude-generated-code"></a><span data-ttu-id="fd40e-116">Wyklucz wygenerowany kod</span><span class="sxs-lookup"><span data-stu-id="fd40e-116">Exclude generated code</span></span>

<span data-ttu-id="fd40e-117">Można skonfigurować dodatkowe pliki i foldery, które mają być traktowane jako kod wygenerowany przez dodanie `generated_code = true | false` wpisu do [pliku konfiguracji](configuration-files.md).</span><span class="sxs-lookup"><span data-stu-id="fd40e-117">You can configure additional files and folders to be treated as generated code by adding a `generated_code = true | false` entry to your [configuration file](configuration-files.md).</span></span> <span data-ttu-id="fd40e-118">Ostrzeżenia analizatora kodu platformy .NET nie są przydatne w przypadku generowanych plików kodu, takich jak pliki generowane przez projektanta, których użytkownicy nie mogą edytować w celu naprawy jakichkolwiek naruszeń.</span><span class="sxs-lookup"><span data-stu-id="fd40e-118">.NET code analyzer warnings aren't useful on generated code files, such as designer-generated files, which users can't edit to fix any violations.</span></span> <span data-ttu-id="fd40e-119">W większości przypadków analizatory kodu pomijają wygenerowane pliki kodu i nie zgłaszają naruszeń dla tych plików.</span><span class="sxs-lookup"><span data-stu-id="fd40e-119">In most cases, code analyzers skip generated code files and don't report violations on these files.</span></span>

<span data-ttu-id="fd40e-120">Domyślnie pliki z określonymi rozszerzeniami plików lub wygenerowanymi automatycznie nagłówkami plików są traktowane jako pliki wygenerowanego kodu.</span><span class="sxs-lookup"><span data-stu-id="fd40e-120">By default, files with certain file extensions or auto-generated file headers are treated as generated code files.</span></span> <span data-ttu-id="fd40e-121">Na przykład nazwa pliku kończąca się ciągiem `.designer.cs` lub `.generated.cs` jest uznawana za wygenerowany kod.</span><span class="sxs-lookup"><span data-stu-id="fd40e-121">For example, a file name ending with `.designer.cs` or `.generated.cs` is considered generated code.</span></span> <span data-ttu-id="fd40e-122">Ta opcja konfiguracji pozwala określić dodatkowe wzorce nazewnictwa.</span><span class="sxs-lookup"><span data-stu-id="fd40e-122">This configuration option lets you specify additional naming patterns.</span></span>

<span data-ttu-id="fd40e-123">Na przykład, aby traktować wszystkie pliki, których nazwy kończą się `.MyGenerated.cs` jako kod wygenerowany, Dodaj następujący wpis:</span><span class="sxs-lookup"><span data-stu-id="fd40e-123">For example, to treat all files whose name ends with `.MyGenerated.cs` as generated code, add the following entry:</span></span>

```ini
[*.MyGenerated.cs]
generated_code = true
```

## <a name="rule-specific-options"></a><span data-ttu-id="fd40e-124">Opcje specyficzne dla reguły</span><span class="sxs-lookup"><span data-stu-id="fd40e-124">Rule-specific options</span></span>

<span data-ttu-id="fd40e-125">Opcje specyficzne dla reguły można zastosować do jednej reguły, zestawu reguł lub wszystkich reguł.</span><span class="sxs-lookup"><span data-stu-id="fd40e-125">Rule-specific options can be applied to a single rule, a set of rules, or all rules.</span></span> <span data-ttu-id="fd40e-126">Opcje specyficzne dla reguły obejmują:</span><span class="sxs-lookup"><span data-stu-id="fd40e-126">The rule-specific options include:</span></span>

- [<span data-ttu-id="fd40e-127">Poziom ważności reguły</span><span class="sxs-lookup"><span data-stu-id="fd40e-127">Rule severity level</span></span>](#severity-level)
- [<span data-ttu-id="fd40e-128">Opcje specyficzne dla reguł *jakości kodu*</span><span class="sxs-lookup"><span data-stu-id="fd40e-128">Options specific to *code-quality* rules</span></span>](code-quality-rule-options.md)

### <a name="severity-level"></a><span data-ttu-id="fd40e-129">Poziom ważności</span><span class="sxs-lookup"><span data-stu-id="fd40e-129">Severity level</span></span>

<span data-ttu-id="fd40e-130">W poniższej tabeli przedstawiono różne rodzaje reguł, które można skonfigurować dla wszystkich reguł analizatora, w tym [jakości kodu](quality-rules/index.md) i reguły [stylu kodu](style-rules/index.md) .</span><span class="sxs-lookup"><span data-stu-id="fd40e-130">The following table shows the different rule severities that you can configure for all analyzer rules, including [code quality](quality-rules/index.md) and [code style](style-rules/index.md) rules.</span></span>

| <span data-ttu-id="fd40e-131">Ważność</span><span class="sxs-lookup"><span data-stu-id="fd40e-131">Severity</span></span> | <span data-ttu-id="fd40e-132">Zachowanie w czasie kompilacji</span><span class="sxs-lookup"><span data-stu-id="fd40e-132">Build-time behavior</span></span> |
|-|-|
| `error` | <span data-ttu-id="fd40e-133">Naruszenia są wyświetlane jako *Błędy* kompilacji i powodują niepowodzenie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="fd40e-133">Violations appear as build *errors* and cause builds to fail.</span></span>|
| `warning` | <span data-ttu-id="fd40e-134">Naruszenia są wyświetlane jako *ostrzeżenia* kompilacji, ale nie powodują niepowodzenia kompilacji (chyba że jest ustawiona opcja traktowania ostrzeżeń jako błędów).</span><span class="sxs-lookup"><span data-stu-id="fd40e-134">Violations appear as build *warnings* but do not cause builds to fail (unless you have an option set to treat warnings as errors).</span></span> |
| `suggestion` | <span data-ttu-id="fd40e-135">Naruszenia są wyświetlane jako *wiadomości* kompilacji i jako sugestie w środowisku IDE programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fd40e-135">Violations appear as build *messages* and as suggestions in the Visual Studio IDE.</span></span> |
| `silent` | <span data-ttu-id="fd40e-136">Naruszenia nie są widoczne dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fd40e-136">Violations aren't visible to the user.</span></span> |
| `none` | <span data-ttu-id="fd40e-137">Reguła została całkowicie pominięta.</span><span class="sxs-lookup"><span data-stu-id="fd40e-137">Rule is suppressed completely.</span></span> |
| `default` | <span data-ttu-id="fd40e-138">Używana jest domyślna ważność reguły.</span><span class="sxs-lookup"><span data-stu-id="fd40e-138">The default severity of the rule is used.</span></span> |

> [!TIP]
> <span data-ttu-id="fd40e-139">Aby uzyskać informacje o tym, jak w programie Visual Studio ma być wyświetlana reguła dotycząca odniesień, zobacz [poziomy ważności](/visualstudio/ide/editorconfig-language-conventions#severity-levels).</span><span class="sxs-lookup"><span data-stu-id="fd40e-139">For information about how rule severities surface in Visual Studio, see [Severity levels](/visualstudio/ide/editorconfig-language-conventions#severity-levels).</span></span>

#### <a name="scope"></a><span data-ttu-id="fd40e-140">Zakres</span><span class="sxs-lookup"><span data-stu-id="fd40e-140">Scope</span></span>

<span data-ttu-id="fd40e-141">Aby ustawić ważność reguły dla jednej reguły, użyj następującej składni.</span><span class="sxs-lookup"><span data-stu-id="fd40e-141">To set the rule severity for a single rule, use the following syntax.</span></span>

```ini
dotnet_diagnostic.<rule ID>.severity = <severity value>
```

<span data-ttu-id="fd40e-142">Aby ustawić domyślną ważność reguły dla kategorii reguł analizatora, należy użyć następującej składni.</span><span class="sxs-lookup"><span data-stu-id="fd40e-142">To set the default rule severity for a category of analyzer rules, use the following syntax.</span></span>

```ini
dotnet_analyzer_diagnostic.category-<rule category>.severity = <severity value>
```

<span data-ttu-id="fd40e-143">Aby ustawić domyślną ważność reguły dla wszystkich reguł analizatora, należy użyć następującej składni.</span><span class="sxs-lookup"><span data-stu-id="fd40e-143">To set the default rule severity for all analyzer rules, use the following syntax.</span></span>

```ini
dotnet_analyzer_diagnostic.severity = <severity value>
```

#### <a name="precedence"></a><span data-ttu-id="fd40e-144">Pierwszeństwo</span><span class="sxs-lookup"><span data-stu-id="fd40e-144">Precedence</span></span>

<span data-ttu-id="fd40e-145">Jeśli masz wpisy konfiguracji z wieloma ważnościami, które można zastosować do tego samego identyfikatora reguły, pierwszeństwo jest wybierane w następującej kolejności:</span><span class="sxs-lookup"><span data-stu-id="fd40e-145">If you have multiple severity configuration entries that can be applied to the same rule ID, precedence is chosen in the following order:</span></span>

- <span data-ttu-id="fd40e-146">Wpis dla pojedynczej reguły według identyfikatora ma pierwszeństwo przed pozycją dla kategorii.</span><span class="sxs-lookup"><span data-stu-id="fd40e-146">An entry for an individual rule by ID takes precedence over an entry for a category.</span></span>
- <span data-ttu-id="fd40e-147">Wpis dla kategorii ma pierwszeństwo przed wpisem dla wszystkich reguł analizatora.</span><span class="sxs-lookup"><span data-stu-id="fd40e-147">An entry for a category takes precedence over an entry for all analyzer rules.</span></span>

<span data-ttu-id="fd40e-148">Rozważmy następujący przykład, gdzie [CA1822](/visualstudio/code-quality/ca1822) ma kategorię "Performance" (wydajność):</span><span class="sxs-lookup"><span data-stu-id="fd40e-148">Consider the following example, where [CA1822](/visualstudio/code-quality/ca1822) has the category "Performance":</span></span>

```ini
[*.cs]
dotnet_diagnostic.CA1822.severity = error
dotnet_analyzer_diagnostic.category-performance.severity = warning
dotnet_analyzer_diagnostic.severity = suggestion
```

<span data-ttu-id="fd40e-149">W poprzednim przykładzie wszystkie trzy wpisy ważności mają zastosowanie do CA1822.</span><span class="sxs-lookup"><span data-stu-id="fd40e-149">In the preceding example, all three severity entries are applicable to CA1822.</span></span> <span data-ttu-id="fd40e-150">Jednak przy użyciu określonych reguł pierwszeństwa, pierwszy wpis oparty na IDENTYFIKATORze usługi WINS w następnych wpisach.</span><span class="sxs-lookup"><span data-stu-id="fd40e-150">However, using the specified precedence rules, the first rule ID-based entry wins over the next entries.</span></span> <span data-ttu-id="fd40e-151">W tym przykładzie CA1822 będzie mieć efektywną ważność `error` .</span><span class="sxs-lookup"><span data-stu-id="fd40e-151">In this example, CA1822 will have an effective severity of `error`.</span></span> <span data-ttu-id="fd40e-152">Wszystkie inne reguły w kategorii "Performance" będą mieć ważność `warning` .</span><span class="sxs-lookup"><span data-stu-id="fd40e-152">All other rules within the "Performance" category will have a severity of `warning`.</span></span>

<span data-ttu-id="fd40e-153">Aby uzyskać informacje na temat sposobu ustalania pierwszeństwa między plikami, zobacz [sekcję pierwszeństwo w artykule pliki konfiguracyjne](configuration-files.md#precedence).</span><span class="sxs-lookup"><span data-stu-id="fd40e-153">For information about how inter-file precedence is decided, see the [Precedence section of the Configuration files article](configuration-files.md#precedence).</span></span>
