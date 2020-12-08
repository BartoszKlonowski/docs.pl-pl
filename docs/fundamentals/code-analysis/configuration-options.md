---
title: Konfigurowanie reguł analizy kodu
description: Dowiedz się, jak skonfigurować reguły analizy kodu w pliku konfiguracji analizatora.
ms.date: 09/24/2020
ms.topic: conceptual
no-loc:
- EditorConfig
ms.openlocfilehash: 4f7b392a2b066023fec75c5295bd94651654d645
ms.sourcegitcommit: 45c7148f2483db2501c1aa696ab6ed2ed8cb71b2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/08/2020
ms.locfileid: "96851793"
---
# <a name="configuration-options-for-code-analysis"></a>Opcje konfiguracji na potrzeby analizy kodu

Reguły analizy kodu mają różne opcje konfiguracji. Te opcje są określone jako pary klucz-wartość w [pliku konfiguracji analizatora](configuration-files.md) przy użyciu składni `<option key> = <option value>` .

Najbardziej typową opcją, którą skonfigurujesz, jest [ważność reguły](#severity-level). Można skonfigurować poziom ważności dla wszystkich reguł analizatora, w tym [reguły jakości kodu](quality-rules/index.md) i [reguły stylu kodu](style-rules/index.md). Aby na przykład włączyć regułę jako ostrzeżenie, można dodać do pliku następującą parę klucz-wartość EditorConfig .

`dotnet_diagnostic.<rule ID>.severity = warning`

Możesz również skonfigurować dodatkowe opcje, aby dostosować zachowanie reguły:

- Reguły jakości kodu zawierają [dodatkowe opcje](code-quality-rule-options.md) konfigurowania zachowania, takie jak nazwa metody, do której ma zastosowanie reguła.
- Reguły stylu kodu mają [niestandardowe opcje stylu kodu](code-style-rule-options.md).
- Reguły analizatora innych firm mogą definiować własne opcje konfiguracji z niestandardowymi nazwami kluczy i formatami wartości.

Składnia służąca do konfigurowania ważności określonej reguły w [pliku konfiguracyjnym analizatora](configuration-files.md) jest następująca:

```ini
dotnet_diagnostic.<rule ID>.severity = <severity>
```

## <a name="general-options"></a>Opcje ogólne

Te opcje mają zastosowanie do analizy kodu jako całości. Nie można ich stosować tylko do jednej reguły lub zestawu reguł.

### <a name="exclude-generated-code"></a>Wyklucz wygenerowany kod

Można skonfigurować dodatkowe pliki i foldery, które mają być traktowane jako kod wygenerowany przez dodanie `generated_code = true | false` wpisu do [pliku konfiguracji](configuration-files.md). Ostrzeżenia analizatora kodu platformy .NET nie są przydatne w przypadku generowanych plików kodu, takich jak pliki generowane przez projektanta, których użytkownicy nie mogą edytować w celu naprawy jakichkolwiek naruszeń. W większości przypadków analizatory kodu pomijają wygenerowane pliki kodu i nie zgłaszają naruszeń dla tych plików.

Domyślnie pliki z określonymi rozszerzeniami plików lub wygenerowanymi automatycznie nagłówkami plików są traktowane jako pliki wygenerowanego kodu. Na przykład nazwa pliku kończąca się ciągiem `.designer.cs` lub `.generated.cs` jest uznawana za wygenerowany kod. Ta opcja konfiguracji pozwala określić dodatkowe wzorce nazewnictwa.

Na przykład, aby traktować wszystkie pliki, których nazwy kończą się `.MyGenerated.cs` jako kod wygenerowany, Dodaj następujący wpis:

```ini
[*.MyGenerated.cs]
generated_code = true
```

## <a name="rule-specific-options"></a>Opcje specyficzne dla reguły

Opcje specyficzne dla reguły można zastosować do jednej reguły, zestawu reguł lub wszystkich reguł. Opcje specyficzne dla reguły obejmują:

- [Poziom ważności reguły](#severity-level)
- [Opcje specyficzne dla reguł *jakości kodu*](code-quality-rule-options.md)

### <a name="severity-level"></a>Poziom ważności

W poniższej tabeli przedstawiono różne rodzaje reguł, które można skonfigurować dla wszystkich reguł analizatora, w tym [jakości kodu](quality-rules/index.md) i reguły [stylu kodu](style-rules/index.md) .

| Ważność | Zachowanie w czasie kompilacji |
|-|-|
| `error` | Naruszenia są wyświetlane jako *Błędy* kompilacji i powodują niepowodzenie kompilacji.|
| `warning` | Naruszenia są wyświetlane jako *ostrzeżenia* kompilacji, ale nie powodują niepowodzenia kompilacji (chyba że jest ustawiona opcja traktowania ostrzeżeń jako błędów). |
| `suggestion` | Naruszenia są wyświetlane jako *wiadomości* kompilacji i jako sugestie w środowisku IDE programu Visual Studio. |
| `silent` | Naruszenia nie są widoczne dla użytkownika. |
| `none` | Reguła została całkowicie pominięta. |
| `default` | Używana jest domyślna ważność reguły. |

> [!TIP]
> Aby uzyskać informacje o tym, jak w programie Visual Studio ma być wyświetlana reguła dotycząca odniesień, zobacz [poziomy ważności](/visualstudio/ide/editorconfig-language-conventions#severity-levels).

#### <a name="scope"></a>Zakres

Aby ustawić ważność reguły dla jednej reguły, użyj następującej składni.

```ini
dotnet_diagnostic.<rule ID>.severity = <severity value>
```

Aby ustawić domyślną ważność reguły dla kategorii reguł analizatora, należy użyć następującej składni.

```ini
dotnet_analyzer_diagnostic.category-<rule category>.severity = <severity value>
```

Aby ustawić domyślną ważność reguły dla wszystkich reguł analizatora, należy użyć następującej składni.

```ini
dotnet_analyzer_diagnostic.severity = <severity value>
```

#### <a name="precedence"></a>Pierwszeństwo

Jeśli masz wpisy konfiguracji z wieloma ważnościami, które można zastosować do tego samego identyfikatora reguły, pierwszeństwo jest wybierane w następującej kolejności:

- Wpis dla pojedynczej reguły według identyfikatora ma pierwszeństwo przed pozycją dla kategorii.
- Wpis dla kategorii ma pierwszeństwo przed wpisem dla wszystkich reguł analizatora.

Rozważmy następujący przykład, gdzie [CA1822](/visualstudio/code-quality/ca1822) ma kategorię "Performance" (wydajność):

```ini
[*.cs]
dotnet_diagnostic.CA1822.severity = error
dotnet_analyzer_diagnostic.category-performance.severity = warning
dotnet_analyzer_diagnostic.severity = suggestion
```

W poprzednim przykładzie wszystkie trzy wpisy ważności mają zastosowanie do CA1822. Jednak przy użyciu określonych reguł pierwszeństwa, pierwszy wpis oparty na IDENTYFIKATORze usługi WINS w następnych wpisach. W tym przykładzie CA1822 będzie mieć efektywną ważność `error` . Wszystkie inne reguły w kategorii "Performance" będą mieć ważność `warning` .

Aby uzyskać informacje na temat sposobu ustalania pierwszeństwa między plikami, zobacz [sekcję pierwszeństwo w artykule pliki konfiguracyjne](configuration-files.md#precedence).
