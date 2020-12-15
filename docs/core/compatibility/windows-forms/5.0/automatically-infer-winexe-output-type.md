---
title: 'Zmiana podziału: wartość OutputType ustawiona na WinExe dla aplikacji WPF i WinForms'
description: Dowiedz się więcej na temat istotnej zmiany w programie .NET 5,0, gdzie wartość OutputType jest automatycznie ustawiana na WinExe dla aplikacji Windows Forms.
ms.date: 09/18/2020
ms.openlocfilehash: 7b2c7a76983c9e7958808e3cc4716be7792841c6
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97513188"
---
# <a name="outputtype-set-to-winexe-for-wpf-and-winforms-apps"></a>OutputType ustawiony na WinExe dla aplikacji WPF i WinForms

`OutputType` jest automatycznie ustawiany na `WinExe` dla Windows Presentation Foundation (WPF) i Windows Forms aplikacji. Gdy `OutputType` jest ustawiona na `WinExe` , okno konsoli nie jest otwierane, gdy aplikacja jest wykonywana.

## <a name="change-description"></a>Zmień opis

W poprzednich wersjach zestawu .NET SDK wartość określona dla `OutputType` pliku projektu jest używana. Na przykład:

```xml
<PropertyGroup>
  <OutputType>Exe</OutputType>
</PropertyGroup>
```

Począwszy od wersji 5.0.1 zestawu .NET SDK, `OutputType` jest automatycznie ustawiany na `WinExe` dla WPF i Windows Forms aplikacji przeznaczonych dla dowolnej wersji platformy, w tym .NET Framework. Na przykład:

```xml
<PropertyGroup>
  <OutputType>WinExe</OutputType>
</PropertyGroup>
```

## <a name="reason-for-change"></a>Przyczyna zmiany

Zakłada się, że większość użytkowników nie chce, aby okno konsoli było otwierane podczas wykonywania aplikacji WPF lub Windows Forms. Ponadto, gdy [te typy aplikacji używają zestawu .NET SDK](sdk-and-target-framework-change.md) zamiast zestawu Windows Desktop SDK, zostanie ustawiona prawidłowa wartość domyślna. Dodatkowo, gdy zostanie dodana obsługa dla urządzeń z systemami iOS i Android, będzie ona łatwiejsza dla wielu platform, jeśli wszystkie używają tego samego typu danych wyjściowych.

## <a name="version-introduced"></a>Wprowadzona wersja

5.0.1 .NET

## <a name="recommended-action"></a>Zalecana akcja

W Twojej części nie jest wymagana żadna akcja. Jeśli jednak chcesz przywrócić stare zachowanie, ustaw `DisableWinExeOutputInference` Właściwość na `true` w pliku projektu.

```xml
<DisableWinExeOutputInference>true</DisableWinExeOutputInference>
```

## <a name="affected-apis"></a>Dotyczy interfejsów API

Nie wykrywalne za pośrednictwem analizy interfejsu API.

<!--

### Affected APIs

Not detectable via API analysis.

### Category

- Windows Forms
- Windows Presentation Framework (WPF)

-->
