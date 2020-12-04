---
title: Pliki konfiguracji dla reguł analizy kodu
description: Więcej informacji na temat różnych plików konfiguracji w celu skonfigurowania reguł analizy kodu.
ms.date: 09/24/2020
ms.topic: conceptual
no-loc:
- EditorConfig
ms.openlocfilehash: cf9b8f4033e6774684b2b7e3b788ef3c157d95df
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96590040"
---
# <a name="configuration-files-for-code-analysis-rules"></a>Pliki konfiguracji dla reguł analizy kodu

Reguły analizy kodu mają różne [Opcje konfiguracji](configuration-options.md). Te opcje należy określić jako pary klucz-wartość w jednym z następujących plików konfiguracji analizatora:

- [EditorConfig](#editorconfig) plik: opcje konfiguracji oparte na plikach lub folderach.
- [Globalny plik AnalyzerConfig](#global-analyzerconfig) : opcje konfiguracji na poziomie projektu.

## EditorConfig

[EditorConfig](/visualstudio/ide/create-portable-custom-editor-options) Pliki służą do udostępniania **opcji, które mają zastosowanie do określonych plików lub folderów źródłowych**. Opcje są umieszczane w nagłówkach sekcji, aby identyfikować odpowiednie pliki i foldery. Dodaj wpis dla każdej reguły, którą chcesz skonfigurować, i umieść ją w odpowiedniej sekcji rozszerzenia pliku, na przykład `[*.cs]` .

```ini
[*.cs]
<option_name> = <option_value>
```

W powyższym przykładzie `[*.cs]` jest editorconfig nagłówka sekcji, aby zaznaczyć wszystkie pliki C# z `.cs` rozszerzeniem pliku w bieżącym folderze, w tym podfolderami. Kolejny wpis, `<option_name> = <option_value>` , jest opcją analizatora, która zostanie zastosowana do wszystkich plików w języku C#.

EditorConfigKonwencje plików można stosować do folderu, projektu lub całego repozytorium przez umieszczenie pliku w odpowiednim katalogu. Te opcje są stosowane podczas wykonywania analizy w czasie kompilacji i podczas edycji kodu w programie Visual Studio.

Jeśli masz istniejący plik *. editorconfig* dla ustawień edytora, takich jak rozmiar wcięcia lub to, czy ma zostać przycinania końcowe odstępy, możesz umieścić opcje konfiguracji analizy kodu w tym samym pliku.

> [!TIP]
> Program Visual Studio udostępnia szablon elementu *. editorconfig* , który ułatwia dodawanie jednego z tych plików do projektu. Aby uzyskać więcej informacji, zobacz [Dodawanie EditorConfig pliku do projektu](/visualstudio/ide/create-portable-custom-editor-options#add-an-editorconfig-file-to-a-project).

### <a name="example"></a>Przykład

Poniżej znajduje się przykładowy EditorConfig plik służący do konfigurowania opcji i ważności reguły:

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

## <a name="global-analyzerconfig"></a>AnalyzerConfig globalne

Począwszy od zestawu SDK programu .NET 5,0 (który jest obsługiwany w programie Visual Studio 2019 w wersji 16,8 i nowszych), można również skonfigurować opcje analizatora przy użyciu globalnych plików _AnalyzerConfig_ . Te pliki są używane do udostępniania **opcji, które mają zastosowanie do wszystkich plików źródłowych w projekcie**, niezależnie od ich nazw plików lub ścieżek plików.

W przeciwieństwie [EditorConfig](#editorconfig) do plików, globalne pliki konfiguracyjne nie mogą być używane do konfigurowania ustawień stylu edytora dla środowisk IDE, takie jak rozmiar wcięcia lub odstęp końcowy. Zamiast tego są one przeznaczone wyłącznie do określania opcji konfiguracji analizatora poziomu projektu.

### <a name="format"></a>Format

W przeciwieństwie EditorConfig do plików, które muszą mieć nagłówki sekcji, takie jak `[*.cs]` , aby identyfikować odpowiednie pliki i foldery, globalne pliki AnalyzerConfig nie mają nagłówków sekcji. Zamiast tego wymagają wpisu najwyższego poziomu formularza, `is_global = true` Aby odróżnić je od zwykłych EditorConfig plików. Oznacza to, że wszystkie opcje w pliku mają zastosowanie do całego projektu. Na przykład:

```ini
is_global = true
<option_name> = <option_value>
```

### <a name="naming"></a>Nazewnictwo

W przeciwieństwie do EditorConfig plików, które muszą być nazwane `.editorconfig` , globalne pliki konfiguracji nie muszą mieć określonej nazwy ani rozszerzenia. Jednak w przypadku nazywania tych plików `.globalconfig` zostaną one zastosowane niejawnie do wszystkich projektów C# i Visual Basic w bieżącym folderze, w tym podfolderach. W przeciwnym razie musisz jawnie dodać `GlobalAnalyzerConfigFiles` element do pliku projektu programu MSBuild:

```xml
<ItemGroup>
  <GlobalAnalyzerConfigFiles Include="<path_to_global_analyzer_config>" />
</ItemGroup>
```

> [!NOTE]
> Wpis najwyższego poziomu `is_global = true` jest wymagany nawet wtedy, gdy plik ma nazwę `.globalconfig` .

### <a name="example"></a>Przykład

Poniżej znajduje się przykładowy plik Global AnalyzerConfig służący do konfigurowania opcji i ważności reguły na poziomie projektu:

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

## <a name="precedence"></a>Pierwszeństwo

Zarówno EditorConfig pliki, jak i globalne pliki AnalyzerConfig określają parę klucz-wartość dla każdej opcji. Konflikty powstają, gdy istnieje wiele wpisów z tym samym kluczem, ale różne wartości.

### <a name="general-options"></a>Opcje ogólne

Gdy występują konflikty między opcjami, następujące reguły pierwszeństwa są używane do rozwiązywania konfliktów:

- Wpisy powodujące konflikt w tym samym pliku konfiguracyjnym: wpis, który pojawia się później w pliku WINS. Dotyczy to wpisów powodujących konflikty w pojedynczym EditorConfig pliku, a także w jednym globalnym pliku AnalyzerConfig.

- Wpisy powodujące konflikt w dwóch EditorConfig plikach: wpis w EditorConfig pliku, który jest bardziej szczegółowy w systemie plików, a tym samym ma więcej ścieżki pliku, WINS.

- Wpisy powodujące konflikt w dwóch globalnych plikach AnalyzerConfig: raportowane jest ostrzeżenie kompilatora i oba wpisy są ignorowane.

- Wpisy powodujące konflikt w EditorConfig pliku i globalnym pliku AnalyzerConfig: wpis w EditorConfig pliku WINS.

### <a name="severity-options"></a>Opcje ważności

Poprzednie [reguły ogólnego pierwszeństwa](#general-options) są stosowane dla wszystkich opcji określonych w plikach konfiguracji. W przypadku opcji [konfiguracji ważności](configuration-options.md#severity-level) obowiązują następujące dodatkowe reguły pierwszeństwa:

- Opcje ważności określone w wierszu polecenia jako opcje kompilatora ( `/nowarn` lub `/warnaserror` ) zawsze przesłaniają opcje [konfiguracji ważności](configuration-options.md#severity-level) określone w EditorConfig i globalnych plikach AnalyzerConfig.

- Opcje ważności można także określić przy użyciu pliku zestawu [reguł](/visualstudio/code-quality/using-rule-sets-to-group-code-analysis-rules) . Jednak pliki zestawów reguł są przestarzałe na rzecz EditorConfig i globalnych plikach AnalyzerConfig. Zaleca się [przekonwertowanie plików zestawu reguł na odpowiedni EditorConfig plik](/visualstudio/code-quality/use-roslyn-analyzers#convert-an-existing-ruleset-file-to-editorconfig-file). Pierwszeństwo wpisów ważności powodujących konflikty z pliku zestawu reguł EditorConfig lub plików Global AnalyzerConfig jest _niezdefiniowany_.

- Aby uzyskać informacje o regułach pierwszeństwa dla pokrewnych opcji ważności z różnymi kluczami, na przykład gdy dla jednej reguły określono różne wartości, a dla kategorii, w której znajduje się dana reguła, zobacz [Opcje konfiguracji na potrzeby analizy kodu](configuration-options.md#precedence).

## <a name="see-also"></a>Zobacz także

- [EditorConfig problem z projektowaniem globalnego AnalyzerConfig](https://github.com/dotnet/roslyn/issues/47707)
