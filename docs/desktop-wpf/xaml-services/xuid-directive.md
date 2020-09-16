---
title: x:Uid — dyrektywa
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [XAML Services], localizable content attribute
- XAML [XAML Services], x:Uid attribute
- x:Uid attribute [XAML Services]
- Uid attribute [XAML Services]
ms.assetid: 81defade-483b-4a89-b76d-9b25bba34010
ms.openlocfilehash: 3de02702e6fd2be63bc2d099dad11f896b281ad1
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90543501"
---
# <a name="xuid-directive"></a>x:Uid — dyrektywa

Zapewnia unikatowy identyfikator dla elementów znaczników. W wielu scenariuszach Ten unikatowy identyfikator jest używany przez procesy i narzędzia lokalizacji XAML.

## <a name="xaml-attribute-usage"></a>Użycie atrybutu języka XAML

```xaml
<object x:Uid="identifier"... />
```

## <a name="xaml-values"></a>Wartości XAML

|||
|-|-|
|`identifier`|Ręcznie utworzony lub generowany automatycznie ciąg, który powinien być unikatowy w pliku, gdy jest interpretowany przez `x:Uid` konsumenta.|

## <a name="remarks"></a>Uwagi

W [MS-XAML] program `x:Uid` jest zdefiniowany jako dyrektywa. Aby uzyskać więcej informacji, zobacz [ \[ sekcję MS-XAML \] 5.3.6](/previous-versions/msp-n-p/ff650760(v=pandp.10)).

`x:Uid` jest dyskretny ze `x:Name` względu na podanego scenariusza lokalizacji XAML i dlatego, że identyfikatory, które są używane na potrzeby lokalizacji nie mają żadnych zależności względem modelu programowania `x:Name` . Również podlega zasadom `x:Name` języka XAML namescope, jednak `x:Uid` nie podlega żadnym określonym w języku XAML koncepcji wymuszania unikatowości. Procesory XAML w szerokim sensie (procesory, które nie są częścią procesu lokalizacji) nie powinny wymuszać unikatowej `x:Uid` wartości. Ta odpowiedzialność jest koncepcyjnie zależna od nadawcy wartości. Oczekiwana jest unikatowość `x:Uid` wartości w ramach jednego źródła XAML, który jest rozsądny dla konsumentów wartości, takich jak dedykowane procesy globalizacji lub narzędzia. Typowym modelem unikatowym jest to, że `x:Uid` wartości są unikatowe w pliku zakodowanym w formacie XML, który reprezentuje kod XAML.

Narzędzia, które mają znaczącą wiedzę o określonym schemacie XAML, mogą być stosowane `x:Uid` tylko dla prawdziwych lokalizowalnych ciągów, a nie dla wszystkich przypadków, w których napotkano wartość ciągu tekstowego w znaczniku.

Struktury mogą określać określoną właściwość w modelu obiektów, aby była aliasem `x:Uid` przez zastosowanie atrybutu <xref:System.Windows.Markup.UidPropertyAttribute> do typu definiującego. Jeśli struktura określa określoną właściwość, nie jest ona prawidłowa, aby można było określić zarówno, `x:Uid` jak i element członkowski z aliasem dla tego samego obiektu. Jeśli `x:Uid` określono zarówno, jak i element członkowski z aliasem, interfejs API usług XAML platformy .NET zwykle zgłasza <xref:System.Xaml.XamlDuplicateMemberException> w tym przypadku.

## <a name="wpf-usage-notes"></a>Uwagi dotyczące użycia WPF

Aby uzyskać więcej informacji na temat roli `x:Uid` w procesie lokalizowania WPF i w formie BAML języka XAML, zobacz [globalizacja dla WPF](/dotnet/desktop/wpf/advanced/globalization-for-wpf) lub <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A>

## <a name="see-also"></a>Zobacz także

- <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A>
- <xref:Microsoft.Build.Tasks.Windows.UidManager>
- [Globalizacja dla WPF](/dotnet/desktop/wpf/advanced/globalization-for-wpf)
