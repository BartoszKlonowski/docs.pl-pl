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
# <a name="outputtype-set-to-winexe-for-wpf-and-winforms-apps"></a><span data-ttu-id="b0c50-103">OutputType ustawiony na WinExe dla aplikacji WPF i WinForms</span><span class="sxs-lookup"><span data-stu-id="b0c50-103">OutputType set to WinExe for WPF and WinForms apps</span></span>

<span data-ttu-id="b0c50-104">`OutputType` jest automatycznie ustawiany na `WinExe` dla Windows Presentation Foundation (WPF) i Windows Forms aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b0c50-104">`OutputType` is automatically set to `WinExe` for Windows Presentation Foundation (WPF) and Windows Forms apps.</span></span> <span data-ttu-id="b0c50-105">Gdy `OutputType` jest ustawiona na `WinExe` , okno konsoli nie jest otwierane, gdy aplikacja jest wykonywana.</span><span class="sxs-lookup"><span data-stu-id="b0c50-105">When `OutputType` is set to `WinExe`, a console window doesn't open when the app is executed.</span></span>

## <a name="change-description"></a><span data-ttu-id="b0c50-106">Zmień opis</span><span class="sxs-lookup"><span data-stu-id="b0c50-106">Change description</span></span>

<span data-ttu-id="b0c50-107">W poprzednich wersjach zestawu .NET SDK wartość określona dla `OutputType` pliku projektu jest używana.</span><span class="sxs-lookup"><span data-stu-id="b0c50-107">In previous versions of the .NET SDK, the value that's specified for `OutputType` in the project file is used.</span></span> <span data-ttu-id="b0c50-108">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="b0c50-108">For example:</span></span>

```xml
<PropertyGroup>
  <OutputType>Exe</OutputType>
</PropertyGroup>
```

<span data-ttu-id="b0c50-109">Począwszy od wersji 5.0.1 zestawu .NET SDK, `OutputType` jest automatycznie ustawiany na `WinExe` dla WPF i Windows Forms aplikacji przeznaczonych dla dowolnej wersji platformy, w tym .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="b0c50-109">Starting in the 5.0.1 version of the .NET SDK, `OutputType` is automatically set to `WinExe` for WPF and Windows Forms apps that target any framework version, including .NET Framework.</span></span> <span data-ttu-id="b0c50-110">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="b0c50-110">For example:</span></span>

```xml
<PropertyGroup>
  <OutputType>WinExe</OutputType>
</PropertyGroup>
```

## <a name="reason-for-change"></a><span data-ttu-id="b0c50-111">Przyczyna zmiany</span><span class="sxs-lookup"><span data-stu-id="b0c50-111">Reason for change</span></span>

<span data-ttu-id="b0c50-112">Zakłada się, że większość użytkowników nie chce, aby okno konsoli było otwierane podczas wykonywania aplikacji WPF lub Windows Forms.</span><span class="sxs-lookup"><span data-stu-id="b0c50-112">It's assumed that most users don't want a console window to open when a WPF or Windows Forms app is executed.</span></span> <span data-ttu-id="b0c50-113">Ponadto, gdy [te typy aplikacji używają zestawu .NET SDK](sdk-and-target-framework-change.md) zamiast zestawu Windows Desktop SDK, zostanie ustawiona prawidłowa wartość domyślna.</span><span class="sxs-lookup"><span data-stu-id="b0c50-113">In addition, [now that these application types use the .NET SDK](sdk-and-target-framework-change.md) instead of the Windows Desktop SDK, the correct default will be set.</span></span> <span data-ttu-id="b0c50-114">Dodatkowo, gdy zostanie dodana obsługa dla urządzeń z systemami iOS i Android, będzie ona łatwiejsza dla wielu platform, jeśli wszystkie używają tego samego typu danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="b0c50-114">Further, when support for targeting iOS and Android is added, it will be easier to multi-target between multiple platforms if they all use the same output type.</span></span>

## <a name="version-introduced"></a><span data-ttu-id="b0c50-115">Wprowadzona wersja</span><span class="sxs-lookup"><span data-stu-id="b0c50-115">Version introduced</span></span>

<span data-ttu-id="b0c50-116">5.0.1 .NET</span><span class="sxs-lookup"><span data-stu-id="b0c50-116">.NET 5.0.1</span></span>

## <a name="recommended-action"></a><span data-ttu-id="b0c50-117">Zalecana akcja</span><span class="sxs-lookup"><span data-stu-id="b0c50-117">Recommended action</span></span>

<span data-ttu-id="b0c50-118">W Twojej części nie jest wymagana żadna akcja.</span><span class="sxs-lookup"><span data-stu-id="b0c50-118">No action is required in your part.</span></span> <span data-ttu-id="b0c50-119">Jeśli jednak chcesz przywrócić stare zachowanie, ustaw `DisableWinExeOutputInference` Właściwość na `true` w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="b0c50-119">However, if you want to revert to the old behavior, set the `DisableWinExeOutputInference` property to `true` in your project file.</span></span>

```xml
<DisableWinExeOutputInference>true</DisableWinExeOutputInference>
```

## <a name="affected-apis"></a><span data-ttu-id="b0c50-120">Dotyczy interfejsów API</span><span class="sxs-lookup"><span data-stu-id="b0c50-120">Affected APIs</span></span>

<span data-ttu-id="b0c50-121">Nie wykrywalne za pośrednictwem analizy interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="b0c50-121">Not detectable via API analysis.</span></span>

<!--

### Affected APIs

Not detectable via API analysis.

### Category

- Windows Forms
- Windows Presentation Framework (WPF)

-->
