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
# <a name="predefined-configuration-files"></a>Wstępnie zdefiniowane pliki konfiguracji

Wstępnie zdefiniowane pliki EditorConfig i [zestawów reguł](/visualstudio/code-quality/using-rule-sets-to-group-code-analysis-rules) są dostępne, dzięki czemu można szybko i łatwo włączyć kategorię reguł jakości kodu, takich jak zabezpieczenia czy reguły projektowania. Przez włączenie określonej kategorii reguł można zidentyfikować odpowiednie problemy i określone warunki. Aby uzyskać dostęp do tych wstępnie zdefiniowanych plików, zainstaluj pakiet analizatora NuGet [Microsoft. CodeAnalysis.](https://github.com/dotnet/roslyn-analyzers#microsoftcodeanalysisnetanalyzers)

[Microsoft. CodeAnalysis. Webanalizatory](https://github.com/dotnet/roslyn-analyzers#microsoftcodeanalysisnetanalyzers) obejmuje wstępnie zdefiniowane pliki EditorConfig i zestawy reguł dla następujących kategorii reguł:

- Wszystkie reguły
- Przepływ danych
- Projekt
- Dokumentacja
- Globalizacja
- Współdziałanie
- Łatwość konserwacji
- Nazewnictwo
- Wydajność
- Przewoźny z FxCop
- Niezawodność
- Bezpieczeństwo
- Użycie

Każda z tych kategorii reguł ma plik EditorConfig lub zestawu reguł, aby:

- Włącz wszystkie reguły w kategorii (i Wyłącz wszystkie inne reguły)
- Użyj domyślnej ważności każdej reguły i włączono ją domyślnie (i Wyłącz wszystkie inne reguły)

> [!TIP]
> Kategoria "wszystkie reguły" ma dodatkowy plik EditorConfig lub zestawu reguł, aby wyłączyć wszystkie reguły. Użyj tego pliku, aby szybko pozbyć się wszelkich ostrzeżeń lub błędów analizatora w projekcie.

## <a name="predefined-editorconfig-files"></a>Wstępnie zdefiniowane pliki EditorConfig

Wstępnie zdefiniowane pliki EditorConfig dla pakietu analizatora Microsoft. CodeAnalysis. webanalyzer znajdują się w podkatalogu *EditorConfig* , w którym zainstalowano pakiet NuGet. Na przykład plik EditorConfig, aby włączyć wszystkie reguły zabezpieczeń, znajduje się w *EditorConfig/SecurityRulesEnabled/. EditorConfig*.

Skopiuj wybrany plik *editorconfig* do katalogu głównego projektu.

## <a name="predefined-rule-sets"></a>Zestawy wstępnie zdefiniowanych reguł

Wstępnie zdefiniowane pliki zestawu reguł dla pakietu Microsoft. CodeAnalysis. serviceanalizators Analyzer znajdują się w podkatalogu *zestawów reguł* , w którym zainstalowano pakiet NuGet. Na przykład plik zestawu reguł, aby włączyć wszystkie reguły zabezpieczeń, znajduje się w *zestawach reguł/SecurityRulesEnabled. reguł*. Skopiuj jeden lub więcej zestawów reguł i wklej je w katalogu zawierającym Twój projekt.

## <a name="see-also"></a>Zobacz także

- [Konfiguracja analizatora](https://github.com/dotnet/roslyn-analyzers/blob/master/docs/Analyzer%20Configuration.md)
- [Opcje reguły stylu kodu platformy .NET dla EditorConfig](code-style-rule-options.md)
