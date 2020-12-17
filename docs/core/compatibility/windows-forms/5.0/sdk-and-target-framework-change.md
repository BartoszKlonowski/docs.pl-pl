---
title: 'Nieprzerwana zmiana: aplikacje WinForms i WPF korzystają z Microsoft. NET. Sdk'
description: Dowiedz się więcej na temat istotnej zmiany w programie .NET 5,0, w której aplikacje Windows Forms i Windows Presentation Framework używają teraz zestawu .NET SDK zamiast narzędzi .NET Core WinForms i WPF SDK.
ms.date: 09/18/2020
ms.openlocfilehash: 5eafed03fbf034f6a6457217a8527a877214e239
ms.sourcegitcommit: 635a0ff775d2447a81ef7233a599b8f88b162e5d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/17/2020
ms.locfileid: "97633822"
---
# <a name="winforms-and-wpf-apps-use-microsoftnetsdk"></a><span data-ttu-id="24058-103">WinForms i aplikacje WPF używają Microsoft. NET. Sdk</span><span class="sxs-lookup"><span data-stu-id="24058-103">WinForms and WPF apps use Microsoft.NET.Sdk</span></span>

<span data-ttu-id="24058-104">Aplikacje Windows Forms i Windows Presentation Framework (WPF) używają teraz zestawu .NET SDK ( `Microsoft.NET.Sdk` ) zamiast programu .NET Core WinForms i zestawu WPF SDK ( `Microsoft.NET.Sdk.WindowsDesktop` ).</span><span class="sxs-lookup"><span data-stu-id="24058-104">Windows Forms and Windows Presentation Framework (WPF) apps now use the .NET SDK (`Microsoft.NET.Sdk`) instead of the .NET Core WinForms and WPF SDK (`Microsoft.NET.Sdk.WindowsDesktop`).</span></span>

## <a name="change-description"></a><span data-ttu-id="24058-105">Zmień opis</span><span class="sxs-lookup"><span data-stu-id="24058-105">Change description</span></span>

<span data-ttu-id="24058-106">W poprzednich wersjach programu .NET Core, WinForms i aplikacje WPF używały oddzielnego [zestawu SDK projektu](../../../project-sdk/overview.md) ( `Microsoft.NET.Sdk.WindowsDesktop` ).</span><span class="sxs-lookup"><span data-stu-id="24058-106">In previous .NET Core versions, WinForms and WPF apps used a separate [project SDK](../../../project-sdk/overview.md) (`Microsoft.NET.Sdk.WindowsDesktop`).</span></span> <span data-ttu-id="24058-107">Począwszy od platformy .NET 5,0, kontrolki WinForm i zestaw WPF SDK zostały ujednolicone z zestawem SDK platformy .NET ( `Microsoft.NET.Sdk` ).</span><span class="sxs-lookup"><span data-stu-id="24058-107">Starting in .NET 5.0, the WinForms and WPF SDK has been unified with the .NET SDK (`Microsoft.NET.Sdk`).</span></span> <span data-ttu-id="24058-108">Ponadto nowe [monikery platformy docelowej (TFM)](../../../../standard/frameworks.md) zastępują `netcoreapp` i `netstandard` w programie .NET 5.</span><span class="sxs-lookup"><span data-stu-id="24058-108">In addition, new [target framework monikers (TFM)](../../../../standard/frameworks.md) replace `netcoreapp` and `netstandard` in .NET 5.</span></span> <span data-ttu-id="24058-109">Poniższy przykład pokazuje zmiany, które należy wprowadzić dla pliku projektu WPF podczas przekierowywania do programu .NET 5,0 lub nowszego.</span><span class="sxs-lookup"><span data-stu-id="24058-109">The following example shows the changes you'd need to make for a WPF project file when retargeting to .NET 5.0 or later.</span></span>

<span data-ttu-id="24058-110">W poprzednich wersjach programu .NET Core:</span><span class="sxs-lookup"><span data-stu-id="24058-110">In previous .NET Core versions:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk.WindowsDesktop">

  <PropertyGroup>
    <OutputType>WinExe</OutputType>
    <TargetFramework>netcoreapp3.1</TargetFramework>
    <UseWPF>true</UseWPF>
  </PropertyGroup>

</Project>
```

<span data-ttu-id="24058-111">W programie .NET 5,0 i jego nowszych wersjach:</span><span class="sxs-lookup"><span data-stu-id="24058-111">In .NET 5.0 and later versions:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>WinExe</OutputType>
    <TargetFramework>net5.0-windows</TargetFramework>
    <UseWPF>true</UseWPF>
  </PropertyGroup>

</Project>
```

## <a name="version-introduced"></a><span data-ttu-id="24058-112">Wprowadzona wersja</span><span class="sxs-lookup"><span data-stu-id="24058-112">Version introduced</span></span>

<span data-ttu-id="24058-113">5.0.100 ZESTAWU .NET SDK</span><span class="sxs-lookup"><span data-stu-id="24058-113">.NET SDK 5.0.100</span></span>

## <a name="recommended-action"></a><span data-ttu-id="24058-114">Zalecana akcja</span><span class="sxs-lookup"><span data-stu-id="24058-114">Recommended action</span></span>

<span data-ttu-id="24058-115">W pliku projektu WPF lub Windows Forms:</span><span class="sxs-lookup"><span data-stu-id="24058-115">In your WPF or Windows Forms project file:</span></span>

- <span data-ttu-id="24058-116">Zaktualizuj `Sdk` atrybut do `Microsoft.NET.Sdk` .</span><span class="sxs-lookup"><span data-stu-id="24058-116">Update the `Sdk` attribute  to `Microsoft.NET.Sdk`.</span></span>
- <span data-ttu-id="24058-117">Zaktualizuj `TargetFramework` Właściwość do `net5.0-windows` .</span><span class="sxs-lookup"><span data-stu-id="24058-117">Update the `TargetFramework` property to `net5.0-windows`.</span></span>

## <a name="affected-apis"></a><span data-ttu-id="24058-118">Dotyczy interfejsów API</span><span class="sxs-lookup"><span data-stu-id="24058-118">Affected APIs</span></span>

<span data-ttu-id="24058-119">Nie wykrywalne za pośrednictwem analizy interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="24058-119">Not detectable via API analysis.</span></span>

<!--

### Affected APIs

Not detectable via API analysis.

### Category

- Windows Forms
- Windows Presentation Framework (WPF)

-->
