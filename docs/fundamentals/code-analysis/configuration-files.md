---
title: Pliki konfiguracji dla reguł analizy kodu
description: Więcej informacji na temat różnych plików konfiguracji w celu skonfigurowania reguł analizy kodu.
ms.date: 09/24/2020
ms.topic: conceptual
no-loc:
- EditorConfig
ms.openlocfilehash: 0d64df42ffb1763afed3e883c4f043755e158489
ms.sourcegitcommit: 635a0ff775d2447a81ef7233a599b8f88b162e5d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/17/2020
ms.locfileid: "97633991"
---
# <a name="configuration-files-for-code-analysis-rules"></a><span data-ttu-id="a7fa1-103">Pliki konfiguracji dla reguł analizy kodu</span><span class="sxs-lookup"><span data-stu-id="a7fa1-103">Configuration files for code analysis rules</span></span>

<span data-ttu-id="a7fa1-104">Reguły analizy kodu mają różne [Opcje konfiguracji](configuration-options.md).</span><span class="sxs-lookup"><span data-stu-id="a7fa1-104">Code analysis rules have various [configuration options](configuration-options.md).</span></span> <span data-ttu-id="a7fa1-105">Te opcje należy określić jako pary klucz-wartość w jednym z następujących plików konfiguracji analizatora:</span><span class="sxs-lookup"><span data-stu-id="a7fa1-105">You specify these options as key-value pairs in one of the following analyzer configuration files:</span></span>

- <span data-ttu-id="a7fa1-106">[EditorConfig](#editorconfig) plik: opcje konfiguracji oparte na plikach lub folderach.</span><span class="sxs-lookup"><span data-stu-id="a7fa1-106">[EditorConfig](#editorconfig) file: File-based or folder-based configuration options.</span></span>
- <span data-ttu-id="a7fa1-107">[Globalny plik AnalyzerConfig](#global-analyzerconfig) : opcje konfiguracji na poziomie projektu.</span><span class="sxs-lookup"><span data-stu-id="a7fa1-107">[Global AnalyzerConfig](#global-analyzerconfig) file: Project-level configuration options.</span></span>

## EditorConfig

<span data-ttu-id="a7fa1-108">[EditorConfig](/visualstudio/ide/create-portable-custom-editor-options) Pliki służą do udostępniania **opcji, które mają zastosowanie do określonych plików lub folderów źródłowych**.</span><span class="sxs-lookup"><span data-stu-id="a7fa1-108">[EditorConfig](/visualstudio/ide/create-portable-custom-editor-options) files are used to provide **options that apply to specific source files or folders**.</span></span> <span data-ttu-id="a7fa1-109">Opcje są umieszczane w nagłówkach sekcji, aby identyfikować odpowiednie pliki i foldery.</span><span class="sxs-lookup"><span data-stu-id="a7fa1-109">Options are placed under section headers to identify the applicable files and folders.</span></span> <span data-ttu-id="a7fa1-110">Dodaj wpis dla każdej reguły, którą chcesz skonfigurować, i umieść ją w odpowiedniej sekcji rozszerzenia pliku, na przykład `[*.cs]` .</span><span class="sxs-lookup"><span data-stu-id="a7fa1-110">Add an entry for each rule you want to configure, and place it under the corresponding file extension section, for example, `[*.cs]`.</span></span>

```ini
[*.cs]
<option_name> = <option_value>
```

<span data-ttu-id="a7fa1-111">W powyższym przykładzie `[*.cs]` jest editorconfig nagłówka sekcji, aby zaznaczyć wszystkie pliki C# z `.cs` rozszerzeniem pliku w bieżącym folderze, w tym podfolderami.</span><span class="sxs-lookup"><span data-stu-id="a7fa1-111">In the above example, `[*.cs]` is an editorconfig section header to select all C# files with `.cs` file extension within the current folder, including subfolders.</span></span> <span data-ttu-id="a7fa1-112">Kolejny wpis, `<option_name> = <option_value>` , jest opcją analizatora, która zostanie zastosowana do wszystkich plików w języku C#.</span><span class="sxs-lookup"><span data-stu-id="a7fa1-112">The subsequent entry, `<option_name> = <option_value>`, is an analyzer option that will be applied to all the C# files.</span></span>

<span data-ttu-id="a7fa1-113">EditorConfigKonwencje plików można stosować do folderu, projektu lub całego repozytorium przez umieszczenie pliku w odpowiednim katalogu.</span><span class="sxs-lookup"><span data-stu-id="a7fa1-113">You can apply EditorConfig file conventions to a folder, a project, or an entire repo by placing the file in the corresponding directory.</span></span> <span data-ttu-id="a7fa1-114">Te opcje są stosowane podczas wykonywania analizy w czasie kompilacji i podczas edycji kodu w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a7fa1-114">These options are applied when executing the analysis at build time and while you edit code in Visual Studio.</span></span>

<span data-ttu-id="a7fa1-115">Jeśli masz istniejący plik *. editorconfig* dla ustawień edytora, takich jak rozmiar wcięcia lub to, czy ma zostać przycinania końcowe odstępy, możesz umieścić opcje konfiguracji analizy kodu w tym samym pliku.</span><span class="sxs-lookup"><span data-stu-id="a7fa1-115">If you have an existing *.editorconfig* file for editor settings such as indent size or whether to trim trailing whitespace, you can place your code analysis configuration options in the same file.</span></span>

> [!TIP]
> <span data-ttu-id="a7fa1-116">Program Visual Studio udostępnia szablon elementu *. editorconfig* , który ułatwia dodawanie jednego z tych plików do projektu.</span><span class="sxs-lookup"><span data-stu-id="a7fa1-116">Visual Studio provides an *.editorconfig* item template that makes is easy to add one of these files to your project.</span></span> <span data-ttu-id="a7fa1-117">Aby uzyskać więcej informacji, zobacz [Dodawanie EditorConfig pliku do projektu](/visualstudio/ide/create-portable-custom-editor-options#add-an-editorconfig-file-to-a-project).</span><span class="sxs-lookup"><span data-stu-id="a7fa1-117">For more information, see [Add an EditorConfig file to a project](/visualstudio/ide/create-portable-custom-editor-options#add-an-editorconfig-file-to-a-project).</span></span>

### <a name="example"></a><span data-ttu-id="a7fa1-118">Przykład</span><span class="sxs-lookup"><span data-stu-id="a7fa1-118">Example</span></span>

<span data-ttu-id="a7fa1-119">Poniżej znajduje się przykładowy EditorConfig plik służący do konfigurowania opcji i ważności reguły:</span><span class="sxs-lookup"><span data-stu-id="a7fa1-119">Following is an example EditorConfig file to configure options and rule severity:</span></span>

```ini
# Remove the line below if you want to inherit .editorconfig settings from higher directories
root = true

# C# files
[*.cs]

#### Core EditorConfig Options ####

# Indentation and spacing
indent_size = 4
indent_style = space
tab_width = 4

#### .NET Coding Conventions ####

# this. and Me. preferences
dotnet_style_qualification_for_method = true:warning

#### Diagnostic configuration ####

# CA1000: Do not declare static members on generic types
dotnet_diagnostic.CA1000.severity = warning
```

## <a name="global-analyzerconfig"></a><span data-ttu-id="a7fa1-120">AnalyzerConfig globalne</span><span class="sxs-lookup"><span data-stu-id="a7fa1-120">Global AnalyzerConfig</span></span>

<span data-ttu-id="a7fa1-121">Począwszy od zestawu SDK programu .NET 5 (który jest obsługiwany w programie Visual Studio 2019 w wersji 16,8 lub nowszej), można również skonfigurować opcje analizatora przy użyciu globalnych plików _AnalyzerConfig_ .</span><span class="sxs-lookup"><span data-stu-id="a7fa1-121">Starting with the .NET 5 SDK (which is supported in Visual Studio 2019 version 16.8 and later versions), you can also configure analyzer options with global _AnalyzerConfig_ files.</span></span> <span data-ttu-id="a7fa1-122">Te pliki są używane do udostępniania **opcji, które mają zastosowanie do wszystkich plików źródłowych w projekcie**, niezależnie od ich nazw plików lub ścieżek plików.</span><span class="sxs-lookup"><span data-stu-id="a7fa1-122">These files are used to provide **options that apply to all the source files in a project**, regardless of their file names or file paths.</span></span>

<span data-ttu-id="a7fa1-123">W przeciwieństwie [EditorConfig](#editorconfig) do plików, globalne pliki konfiguracyjne nie mogą być używane do konfigurowania ustawień stylu edytora dla środowisk IDE, takie jak rozmiar wcięcia lub odstęp końcowy.</span><span class="sxs-lookup"><span data-stu-id="a7fa1-123">Unlike [EditorConfig](#editorconfig) files, global config files can't be used to configure editor style settings for IDEs, such as indent size or whether to trim trailing whitespace.</span></span> <span data-ttu-id="a7fa1-124">Zamiast tego są one przeznaczone wyłącznie do określania opcji konfiguracji analizatora poziomu projektu.</span><span class="sxs-lookup"><span data-stu-id="a7fa1-124">Instead, they are designed purely for specifying project-level analyzer configuration options.</span></span>

### <a name="format"></a><span data-ttu-id="a7fa1-125">Format</span><span class="sxs-lookup"><span data-stu-id="a7fa1-125">Format</span></span>

<span data-ttu-id="a7fa1-126">W przeciwieństwie EditorConfig do plików, które muszą mieć nagłówki sekcji, takie jak `[*.cs]` , aby identyfikować odpowiednie pliki i foldery, globalne pliki AnalyzerConfig nie mają nagłówków sekcji.</span><span class="sxs-lookup"><span data-stu-id="a7fa1-126">Unlike EditorConfig files, which must have section headers, such as `[*.cs]`, to identify the applicable files and folders, global AnalyzerConfig files don't have section headers.</span></span> <span data-ttu-id="a7fa1-127">Zamiast tego wymagają wpisu najwyższego poziomu formularza, `is_global = true` Aby odróżnić je od zwykłych EditorConfig plików.</span><span class="sxs-lookup"><span data-stu-id="a7fa1-127">Instead, they require a top level entry of the form `is_global = true` to differentiate them from regular EditorConfig files.</span></span> <span data-ttu-id="a7fa1-128">Oznacza to, że wszystkie opcje w pliku mają zastosowanie do całego projektu.</span><span class="sxs-lookup"><span data-stu-id="a7fa1-128">This indicates that all the options in the file apply to the entire project.</span></span> <span data-ttu-id="a7fa1-129">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="a7fa1-129">For example:</span></span>

```ini
is_global = true
<option_name> = <option_value>
```

### <a name="naming"></a><span data-ttu-id="a7fa1-130">Nazewnictwo</span><span class="sxs-lookup"><span data-stu-id="a7fa1-130">Naming</span></span>

<span data-ttu-id="a7fa1-131">W przeciwieństwie do EditorConfig plików, które muszą być nazwane `.editorconfig` , globalne pliki konfiguracji nie muszą mieć określonej nazwy ani rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="a7fa1-131">Unlike EditorConfig files, which must be named `.editorconfig`, global config files do not need to have a specific name or extension.</span></span> <span data-ttu-id="a7fa1-132">Jednak w przypadku nazywania tych plików `.globalconfig` zostaną one zastosowane niejawnie do wszystkich projektów C# i Visual Basic w bieżącym folderze, w tym podfolderach.</span><span class="sxs-lookup"><span data-stu-id="a7fa1-132">However, if you name these files as `.globalconfig` then they will be implicitly applied to all the C# and Visual Basic projects within the current folder, including subfolders.</span></span> <span data-ttu-id="a7fa1-133">W przeciwnym razie musisz jawnie dodać `GlobalAnalyzerConfigFiles` element do pliku projektu programu MSBuild:</span><span class="sxs-lookup"><span data-stu-id="a7fa1-133">Otherwise, you must explicitly add the `GlobalAnalyzerConfigFiles` item to your MSBuild project file:</span></span>

```xml
<ItemGroup>
  <GlobalAnalyzerConfigFiles Include="<path_to_global_analyzer_config>" />
</ItemGroup>
```

> [!NOTE]
> <span data-ttu-id="a7fa1-134">Wpis najwyższego poziomu `is_global = true` jest wymagany nawet wtedy, gdy plik ma nazwę `.globalconfig` .</span><span class="sxs-lookup"><span data-stu-id="a7fa1-134">The top-level entry `is_global = true` is required even when the file is named `.globalconfig`.</span></span>

### <a name="example"></a><span data-ttu-id="a7fa1-135">Przykład</span><span class="sxs-lookup"><span data-stu-id="a7fa1-135">Example</span></span>

<span data-ttu-id="a7fa1-136">Poniżej znajduje się przykładowy plik Global AnalyzerConfig służący do konfigurowania opcji i ważności reguły na poziomie projektu:</span><span class="sxs-lookup"><span data-stu-id="a7fa1-136">Following is an example global AnalyzerConfig file to configure options and rule severity at the project level:</span></span>

```ini
# Top level entry required to mark this as a global AnalyzerConfig file
is_global = true

# NOTE: No section headers for configuration entries

#### .NET Coding Conventions ####

# this. and Me. preferences
dotnet_style_qualification_for_method = true:warning

#### Diagnostic configuration ####

# CA1000: Do not declare static members on generic types
dotnet_diagnostic.CA1000.severity = warning
```

## <a name="precedence"></a><span data-ttu-id="a7fa1-137">Pierwszeństwo</span><span class="sxs-lookup"><span data-stu-id="a7fa1-137">Precedence</span></span>

<span data-ttu-id="a7fa1-138">Zarówno EditorConfig pliki, jak i globalne pliki AnalyzerConfig określają parę klucz-wartość dla każdej opcji.</span><span class="sxs-lookup"><span data-stu-id="a7fa1-138">Both EditorConfig files and global AnalyzerConfig files specify a key-value pair for each option.</span></span> <span data-ttu-id="a7fa1-139">Konflikty powstają, gdy istnieje wiele wpisów z tym samym kluczem, ale różne wartości.</span><span class="sxs-lookup"><span data-stu-id="a7fa1-139">Conflicts arise when there are multiple entries with the same key but different values.</span></span>

### <a name="general-options"></a><span data-ttu-id="a7fa1-140">Opcje ogólne</span><span class="sxs-lookup"><span data-stu-id="a7fa1-140">General options</span></span>

<span data-ttu-id="a7fa1-141">Gdy występują konflikty między opcjami, następujące reguły pierwszeństwa są używane do rozwiązywania konfliktów:</span><span class="sxs-lookup"><span data-stu-id="a7fa1-141">When conflicts arise between options, the following precedence rules are used to resolve the conflicts:</span></span>

- <span data-ttu-id="a7fa1-142">Wpisy powodujące konflikt w tym samym pliku konfiguracyjnym: wpis, który pojawia się później w pliku WINS.</span><span class="sxs-lookup"><span data-stu-id="a7fa1-142">Conflicting entries in the same configuration file: The entry that appears later in the file wins.</span></span> <span data-ttu-id="a7fa1-143">Dotyczy to wpisów powodujących konflikty w pojedynczym EditorConfig pliku, a także w jednym globalnym pliku AnalyzerConfig.</span><span class="sxs-lookup"><span data-stu-id="a7fa1-143">This is true for conflicting entries within a single EditorConfig file and also within a single global AnalyzerConfig file.</span></span>

- <span data-ttu-id="a7fa1-144">Wpisy powodujące konflikt w dwóch EditorConfig plikach: wpis w EditorConfig pliku, który jest bardziej szczegółowy w systemie plików, a tym samym ma więcej ścieżki pliku, WINS.</span><span class="sxs-lookup"><span data-stu-id="a7fa1-144">Conflicting entries in two EditorConfig files: The entry in the EditorConfig file that's deeper in the file system, and hence has a longer file path, wins.</span></span>

- <span data-ttu-id="a7fa1-145">Wpisy powodujące konflikt w dwóch globalnych plikach AnalyzerConfig: raportowane jest ostrzeżenie kompilatora i oba wpisy są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="a7fa1-145">Conflicting entries in two global AnalyzerConfig files: A compiler warning is reported and both entries are ignored.</span></span>

- <span data-ttu-id="a7fa1-146">Wpisy powodujące konflikt w EditorConfig pliku i globalnym pliku AnalyzerConfig: wpis w EditorConfig pliku WINS.</span><span class="sxs-lookup"><span data-stu-id="a7fa1-146">Conflicting entries in an EditorConfig file and a Global AnalyzerConfig file: The entry in the EditorConfig file wins.</span></span>

### <a name="severity-options"></a><span data-ttu-id="a7fa1-147">Opcje ważności</span><span class="sxs-lookup"><span data-stu-id="a7fa1-147">Severity options</span></span>

<span data-ttu-id="a7fa1-148">Poprzednie [reguły ogólnego pierwszeństwa](#general-options) są stosowane dla wszystkich opcji określonych w plikach konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="a7fa1-148">The previous [general precedence rules](#general-options) apply for all options specified in configuration files.</span></span> <span data-ttu-id="a7fa1-149">W przypadku opcji [konfiguracji ważności](configuration-options.md#severity-level) obowiązują następujące dodatkowe reguły pierwszeństwa:</span><span class="sxs-lookup"><span data-stu-id="a7fa1-149">For [severity configuration](configuration-options.md#severity-level) options, the following additional precedence rules apply:</span></span>

- <span data-ttu-id="a7fa1-150">Opcje ważności określone w wierszu polecenia jako opcje kompilatora ( `/nowarn` lub `/warnaserror` ) zawsze przesłaniają opcje [konfiguracji ważności](configuration-options.md#severity-level) określone w EditorConfig i globalnych plikach AnalyzerConfig.</span><span class="sxs-lookup"><span data-stu-id="a7fa1-150">Severity options specified at the command line as compiler options (`/nowarn` or `/warnaserror`) always override [severity configuration](configuration-options.md#severity-level) options specified in EditorConfig and global AnalyzerConfig files.</span></span>

- <span data-ttu-id="a7fa1-151">Opcje ważności można także określić przy użyciu pliku zestawu [reguł](/visualstudio/code-quality/using-rule-sets-to-group-code-analysis-rules) .</span><span class="sxs-lookup"><span data-stu-id="a7fa1-151">Severity options can also be specified with a [Ruleset](/visualstudio/code-quality/using-rule-sets-to-group-code-analysis-rules) file.</span></span> <span data-ttu-id="a7fa1-152">Jednak pliki zestawów reguł są przestarzałe na rzecz EditorConfig i globalnych plikach AnalyzerConfig.</span><span class="sxs-lookup"><span data-stu-id="a7fa1-152">However, rulesets files are deprecated in favor of EditorConfig and global AnalyzerConfig files.</span></span> <span data-ttu-id="a7fa1-153">Zaleca się [przekonwertowanie plików zestawu reguł na odpowiedni EditorConfig plik](/visualstudio/code-quality/use-roslyn-analyzers#convert-an-existing-ruleset-file-to-editorconfig-file).</span><span class="sxs-lookup"><span data-stu-id="a7fa1-153">It's recommended that you [convert ruleset files to an equivalent EditorConfig file](/visualstudio/code-quality/use-roslyn-analyzers#convert-an-existing-ruleset-file-to-editorconfig-file).</span></span> <span data-ttu-id="a7fa1-154">Pierwszeństwo wpisów ważności powodujących konflikty z pliku zestawu reguł EditorConfig lub plików Global AnalyzerConfig jest _niezdefiniowany_.</span><span class="sxs-lookup"><span data-stu-id="a7fa1-154">Precedence for conflicting severity entries from a ruleset file and EditorConfig or global AnalyzerConfig files is _undefined_.</span></span>

- <span data-ttu-id="a7fa1-155">Aby uzyskać informacje o regułach pierwszeństwa dla pokrewnych opcji ważności z różnymi kluczami, na przykład gdy dla jednej reguły określono różne wartości, a dla kategorii, w której znajduje się dana reguła, zobacz [Opcje konfiguracji na potrzeby analizy kodu](configuration-options.md#precedence).</span><span class="sxs-lookup"><span data-stu-id="a7fa1-155">For information about precedence rules for related severity options with different keys, for example, when different severities are specified for a single rule and for the category that rule falls under, see [Configuration options for code analysis](configuration-options.md#precedence).</span></span>

## <a name="see-also"></a><span data-ttu-id="a7fa1-156">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="a7fa1-156">See also</span></span>

- [<span data-ttu-id="a7fa1-157">EditorConfig problem z projektowaniem globalnego AnalyzerConfig</span><span class="sxs-lookup"><span data-stu-id="a7fa1-157">EditorConfig vs global AnalyzerConfig design issue</span></span>](https://github.com/dotnet/roslyn/issues/47707)
