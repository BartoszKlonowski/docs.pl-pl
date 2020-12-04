---
title: Wstępnie zdefiniowane pliki konfiguracji (analiza kodu)
description: Dowiedz się więcej o używaniu wstępnie zdefiniowanych plików editorconfig i zestawów reguł dla konkretnych typów analizy kodu.
ms.date: 09/24/2020
ms.topic: conceptual
ms.openlocfilehash: 4937dcab1183fa3f63be4afc71627a7c7c08c6bd
ms.sourcegitcommit: 665f8fc55258356f4d2f4a6585b750c974b26675
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/30/2020
ms.locfileid: "96589331"
---
# <a name="predefined-configuration-files"></a><span data-ttu-id="7b682-103">Wstępnie zdefiniowane pliki konfiguracji</span><span class="sxs-lookup"><span data-stu-id="7b682-103">Predefined configuration files</span></span>

<span data-ttu-id="7b682-104">Wstępnie zdefiniowane pliki EditorConfig i [zestawów reguł](/visualstudio/code-quality/using-rule-sets-to-group-code-analysis-rules) są dostępne, dzięki czemu można szybko i łatwo włączyć kategorię reguł jakości kodu, takich jak zabezpieczenia czy reguły projektowania.</span><span class="sxs-lookup"><span data-stu-id="7b682-104">Predefined EditorConfig and [rule set](/visualstudio/code-quality/using-rule-sets-to-group-code-analysis-rules) files are available that make it quick and easy to enable a category of code quality rules, such as security or design rules.</span></span> <span data-ttu-id="7b682-105">Przez włączenie określonej kategorii reguł można zidentyfikować odpowiednie problemy i określone warunki.</span><span class="sxs-lookup"><span data-stu-id="7b682-105">By enabling a specific category of rules, you can identify targeted issues and specific conditions.</span></span> <span data-ttu-id="7b682-106">Aby uzyskać dostęp do tych wstępnie zdefiniowanych plików, zainstaluj pakiet analizatora NuGet [Microsoft. CodeAnalysis.](https://github.com/dotnet/roslyn-analyzers#microsoftcodeanalysisnetanalyzers)</span><span class="sxs-lookup"><span data-stu-id="7b682-106">To access these predefined files, install the [Microsoft.CodeAnalysis.NetAnalyzers](https://github.com/dotnet/roslyn-analyzers#microsoftcodeanalysisnetanalyzers) NuGet analyzer package.</span></span>

<span data-ttu-id="7b682-107">[Microsoft. CodeAnalysis. Webanalizatory](https://github.com/dotnet/roslyn-analyzers#microsoftcodeanalysisnetanalyzers) obejmuje wstępnie zdefiniowane pliki EditorConfig i zestawy reguł dla następujących kategorii reguł:</span><span class="sxs-lookup"><span data-stu-id="7b682-107">[Microsoft.CodeAnalysis.NetAnalyzers](https://github.com/dotnet/roslyn-analyzers#microsoftcodeanalysisnetanalyzers) includes predefined EditorConfig files and rule sets for the following rule categories:</span></span>

- <span data-ttu-id="7b682-108">Wszystkie reguły</span><span class="sxs-lookup"><span data-stu-id="7b682-108">All rules</span></span>
- <span data-ttu-id="7b682-109">Przepływ danych</span><span class="sxs-lookup"><span data-stu-id="7b682-109">Dataflow</span></span>
- <span data-ttu-id="7b682-110">Projekt</span><span class="sxs-lookup"><span data-stu-id="7b682-110">Design</span></span>
- <span data-ttu-id="7b682-111">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="7b682-111">Documentation</span></span>
- <span data-ttu-id="7b682-112">Globalizacja</span><span class="sxs-lookup"><span data-stu-id="7b682-112">Globalization</span></span>
- <span data-ttu-id="7b682-113">Współdziałanie</span><span class="sxs-lookup"><span data-stu-id="7b682-113">Interoperability</span></span>
- <span data-ttu-id="7b682-114">Łatwość konserwacji</span><span class="sxs-lookup"><span data-stu-id="7b682-114">Maintainability</span></span>
- <span data-ttu-id="7b682-115">Nazewnictwo</span><span class="sxs-lookup"><span data-stu-id="7b682-115">Naming</span></span>
- <span data-ttu-id="7b682-116">Wydajność</span><span class="sxs-lookup"><span data-stu-id="7b682-116">Performance</span></span>
- <span data-ttu-id="7b682-117">Przewoźny z FxCop</span><span class="sxs-lookup"><span data-stu-id="7b682-117">Ported from FxCop</span></span>
- <span data-ttu-id="7b682-118">Niezawodność</span><span class="sxs-lookup"><span data-stu-id="7b682-118">Reliability</span></span>
- <span data-ttu-id="7b682-119">Bezpieczeństwo</span><span class="sxs-lookup"><span data-stu-id="7b682-119">Security</span></span>
- <span data-ttu-id="7b682-120">Użycie</span><span class="sxs-lookup"><span data-stu-id="7b682-120">Usage</span></span>

<span data-ttu-id="7b682-121">Każda z tych kategorii reguł ma plik EditorConfig lub zestawu reguł, aby:</span><span class="sxs-lookup"><span data-stu-id="7b682-121">Each of those categories of rules has an EditorConfig or rule set file to:</span></span>

- <span data-ttu-id="7b682-122">Włącz wszystkie reguły w kategorii (i Wyłącz wszystkie inne reguły)</span><span class="sxs-lookup"><span data-stu-id="7b682-122">Enable all the rules in the category (and disable all other rules)</span></span>
- <span data-ttu-id="7b682-123">Użyj domyślnej ważności każdej reguły i włączono ją domyślnie (i Wyłącz wszystkie inne reguły)</span><span class="sxs-lookup"><span data-stu-id="7b682-123">Use each rule's default severity and enabled by default setting (and disable all other rules)</span></span>

> [!TIP]
> <span data-ttu-id="7b682-124">Kategoria "wszystkie reguły" ma dodatkowy plik EditorConfig lub zestawu reguł, aby wyłączyć wszystkie reguły.</span><span class="sxs-lookup"><span data-stu-id="7b682-124">The "all rules" category has an additional EditorConfig or rule set file to disable all rules.</span></span> <span data-ttu-id="7b682-125">Użyj tego pliku, aby szybko pozbyć się wszelkich ostrzeżeń lub błędów analizatora w projekcie.</span><span class="sxs-lookup"><span data-stu-id="7b682-125">Use this file to quickly get rid of any analyzer warnings or errors in a project.</span></span>

## <a name="predefined-editorconfig-files"></a><span data-ttu-id="7b682-126">Wstępnie zdefiniowane pliki EditorConfig</span><span class="sxs-lookup"><span data-stu-id="7b682-126">Predefined EditorConfig files</span></span>

<span data-ttu-id="7b682-127">Wstępnie zdefiniowane pliki EditorConfig dla pakietu analizatora Microsoft. CodeAnalysis. webanalyzer znajdują się w podkatalogu *EditorConfig* , w którym zainstalowano pakiet NuGet.</span><span class="sxs-lookup"><span data-stu-id="7b682-127">The predefined EditorConfig files for the Microsoft.CodeAnalysis.NetAnalyzers analyzer package are located in the *editorconfig* subdirectory of where the NuGet package was installed.</span></span> <span data-ttu-id="7b682-128">Na przykład plik EditorConfig, aby włączyć wszystkie reguły zabezpieczeń, znajduje się w *EditorConfig/SecurityRulesEnabled/. EditorConfig*.</span><span class="sxs-lookup"><span data-stu-id="7b682-128">For example, the EditorConfig file to enable all security rules is located at *editorconfig/SecurityRulesEnabled/.editorconfig*.</span></span>

<span data-ttu-id="7b682-129">Skopiuj wybrany plik *editorconfig* do katalogu głównego projektu.</span><span class="sxs-lookup"><span data-stu-id="7b682-129">Copy the chosen *.editorconfig* file to your project's root directory.</span></span>

## <a name="predefined-rule-sets"></a><span data-ttu-id="7b682-130">Zestawy wstępnie zdefiniowanych reguł</span><span class="sxs-lookup"><span data-stu-id="7b682-130">Predefined rule sets</span></span>

<span data-ttu-id="7b682-131">Wstępnie zdefiniowane pliki zestawu reguł dla pakietu Microsoft. CodeAnalysis. serviceanalizators Analyzer znajdują się w podkatalogu *zestawów reguł* , w którym zainstalowano pakiet NuGet.</span><span class="sxs-lookup"><span data-stu-id="7b682-131">The predefined rule set files for the Microsoft.CodeAnalysis.NetAnalyzers analyzer package are located in the *rulesets* subdirectory of where the NuGet package was installed.</span></span> <span data-ttu-id="7b682-132">Na przykład plik zestawu reguł, aby włączyć wszystkie reguły zabezpieczeń, znajduje się w *zestawach reguł/SecurityRulesEnabled. reguł*.</span><span class="sxs-lookup"><span data-stu-id="7b682-132">For example, the rule set file to enable all security rules is located at *rulesets/SecurityRulesEnabled.ruleset*.</span></span> <span data-ttu-id="7b682-133">Skopiuj jeden lub więcej zestawów reguł i wklej je w katalogu zawierającym Twój projekt.</span><span class="sxs-lookup"><span data-stu-id="7b682-133">Copy one or more of the rule sets and paste them in the directory that contains your project.</span></span>

## <a name="see-also"></a><span data-ttu-id="7b682-134">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="7b682-134">See also</span></span>

- [<span data-ttu-id="7b682-135">Konfiguracja analizatora</span><span class="sxs-lookup"><span data-stu-id="7b682-135">Analyzer configuration</span></span>](https://github.com/dotnet/roslyn-analyzers/blob/master/docs/Analyzer%20Configuration.md)
- [<span data-ttu-id="7b682-136">Opcje reguły stylu kodu platformy .NET dla EditorConfig</span><span class="sxs-lookup"><span data-stu-id="7b682-136">.NET code style rule options for EditorConfig</span></span>](code-style-rule-options.md)
