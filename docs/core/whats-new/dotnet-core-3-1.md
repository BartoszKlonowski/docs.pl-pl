---
title: Co nowego w programie .NET Core 3.1
description: Dowiedz się więcej o nowych funkcjach dostępnych w programie .NET Core 3,1.
dev_langs:
- csharp
author: adegeo
ms.author: adegeo
ms.date: 12/04/2019
ms.openlocfilehash: 9caecdcc3516db2bd71420184fbd21f7837552a7
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96437928"
---
# <a name="whats-new-in-net-core-31"></a><span data-ttu-id="da603-103">Co nowego w programie .NET Core 3.1</span><span class="sxs-lookup"><span data-stu-id="da603-103">What's new in .NET Core 3.1</span></span>

<span data-ttu-id="da603-104">W tym artykule opisano nowości w programie .NET Core 3,1.</span><span class="sxs-lookup"><span data-stu-id="da603-104">This article describes what is new in .NET Core 3.1.</span></span> <span data-ttu-id="da603-105">Ta wersja zawiera drobne ulepszenia programu .NET Core 3,0, skupiając się na małych, ale ważnych poprawkach.</span><span class="sxs-lookup"><span data-stu-id="da603-105">This release contains minor improvements to .NET Core 3.0, focusing on small, but important, fixes.</span></span> <span data-ttu-id="da603-106">Najważniejszym elementem na platformie .NET Core 3,1 jest to, że jest to wersja [długoterminowa (LTS)](#long-term-support) .</span><span class="sxs-lookup"><span data-stu-id="da603-106">The most important feature about .NET Core 3.1 is that it's a [long-term support (LTS)](#long-term-support) release.</span></span>

<span data-ttu-id="da603-107">W przypadku korzystania z programu Visual Studio 2019 należy zaktualizować do [programu Visual studio 2019 w wersji 16,4 lub nowszej](https://visualstudio.microsoft.com/downloads/) , aby współpracować z projektami .net Core 3,1.</span><span class="sxs-lookup"><span data-stu-id="da603-107">If you're using Visual Studio 2019, you must update to [Visual Studio 2019 version 16.4 or later](https://visualstudio.microsoft.com/downloads/) to work with .NET Core 3.1 projects.</span></span> <span data-ttu-id="da603-108">Aby uzyskać informacje na temat Nowości w programie Visual Studio w wersji 16,4, zobacz [co nowego w programie Visual studio 2019 w wersji 16,4](/visualstudio/releases/2019/release-notes-v16.4#whats-new-in-visual-studio-2019-version-164).</span><span class="sxs-lookup"><span data-stu-id="da603-108">For information on what's new in Visual Studio version 16.4, see [What's New in Visual Studio 2019 version 16.4](/visualstudio/releases/2019/release-notes-v16.4#whats-new-in-visual-studio-2019-version-164).</span></span>

<span data-ttu-id="da603-109">Visual Studio dla komputerów Mac obsługuje również program .NET Core 3,1 w Visual Studio dla komputerów Mac 8,4.</span><span class="sxs-lookup"><span data-stu-id="da603-109">Visual Studio for Mac also supports and includes .NET Core 3.1 in Visual Studio for Mac 8.4.</span></span>

<span data-ttu-id="da603-110">Aby uzyskać więcej informacji o wersji, zobacz [anons programu .NET Core 3,1](https://devblogs.microsoft.com/dotnet/announcing-net-core-3-1/).</span><span class="sxs-lookup"><span data-stu-id="da603-110">For more information about the release, see the [.NET Core 3.1 announcement](https://devblogs.microsoft.com/dotnet/announcing-net-core-3-1/).</span></span>

- <span data-ttu-id="da603-111">[Pobierz i Rozpocznij pracę z platformą .NET Core 3,1](https://dotnet.microsoft.com/download/dotnet-core/3.1) w systemie Windows, MacOS lub Linux.</span><span class="sxs-lookup"><span data-stu-id="da603-111">[Download and get started with .NET Core 3.1](https://dotnet.microsoft.com/download/dotnet-core/3.1) on Windows, macOS, or Linux.</span></span>

## <a name="long-term-support"></a><span data-ttu-id="da603-112">Długoterminowa pomoc techniczna</span><span class="sxs-lookup"><span data-stu-id="da603-112">Long-term support</span></span>

<span data-ttu-id="da603-113">.NET Core 3,1 to wersja LTS z pomocą techniczną firmy Microsoft przez kolejne trzy lata.</span><span class="sxs-lookup"><span data-stu-id="da603-113">.NET Core 3.1 is an LTS release with support from Microsoft for the next three years.</span></span> <span data-ttu-id="da603-114">Zdecydowanie zalecamy, aby przenieść aplikacje do programu .NET Core 3,1.</span><span class="sxs-lookup"><span data-stu-id="da603-114">It's highly recommended that you move your apps to .NET Core 3.1.</span></span> <span data-ttu-id="da603-115">Bieżący cykl życia innych głównych wydań jest następujący:</span><span class="sxs-lookup"><span data-stu-id="da603-115">The current lifecycle of other major releases is as follows:</span></span>

| <span data-ttu-id="da603-116">Release</span><span class="sxs-lookup"><span data-stu-id="da603-116">Release</span></span> | <span data-ttu-id="da603-117">Uwaga</span><span class="sxs-lookup"><span data-stu-id="da603-117">Note</span></span> |
| ------- | ---- |
| <span data-ttu-id="da603-118">.NET Core 3.0</span><span class="sxs-lookup"><span data-stu-id="da603-118">.NET Core 3.0</span></span> | <span data-ttu-id="da603-119">Koniec okresu życia w dniu 3 marca 2020.</span><span class="sxs-lookup"><span data-stu-id="da603-119">End of life on March 3, 2020.</span></span>     |
| <span data-ttu-id="da603-120">.NET Core 2.2</span><span class="sxs-lookup"><span data-stu-id="da603-120">.NET Core 2.2</span></span> | <span data-ttu-id="da603-121">Koniec okresu istnienia 23 grudnia 2019.</span><span class="sxs-lookup"><span data-stu-id="da603-121">End of life on December 23, 2019.</span></span> |
| <span data-ttu-id="da603-122">.NET Core 2.1</span><span class="sxs-lookup"><span data-stu-id="da603-122">.NET Core 2.1</span></span> | <span data-ttu-id="da603-123">Koniec okresu istnienia 21 sierpnia 2021.</span><span class="sxs-lookup"><span data-stu-id="da603-123">End of life on August 21, 2021.</span></span>    |

<span data-ttu-id="da603-124">Aby uzyskać więcej informacji, zobacz [zasady obsługi .NET Core](https://dotnet.microsoft.com/platform/support/policy/dotnet-core).</span><span class="sxs-lookup"><span data-stu-id="da603-124">For more information, see the [.NET Core support policy](https://dotnet.microsoft.com/platform/support/policy/dotnet-core).</span></span>

## <a name="macos-apphost-and-notarization"></a><span data-ttu-id="da603-125">macOS appHost i notarization</span><span class="sxs-lookup"><span data-stu-id="da603-125">macOS appHost and notarization</span></span>

<span data-ttu-id="da603-126">*Tylko macOS*</span><span class="sxs-lookup"><span data-stu-id="da603-126">*macOS only*</span></span>

<span data-ttu-id="da603-127">Począwszy od zestaw .NET Core SDK 3,1 dla macOS, ustawienie appHost jest domyślnie wyłączone.</span><span class="sxs-lookup"><span data-stu-id="da603-127">Starting with the notarized .NET Core SDK 3.1 for macOS, the appHost setting is disabled by default.</span></span> <span data-ttu-id="da603-128">Aby uzyskać więcej informacji, zobacz [MacOS Catalina Notarization i wpływ na pobieranie i projekty platformy .NET Core](../install/macos-notarization-issues.md).</span><span class="sxs-lookup"><span data-stu-id="da603-128">For more information, see [macOS Catalina Notarization and the impact on .NET Core downloads and projects](../install/macos-notarization-issues.md).</span></span>

<span data-ttu-id="da603-129">Gdy ustawienie appHost jest włączone, program .NET Core generuje natywny plik konfiguracji Mach-O podczas kompilowania lub publikowania.</span><span class="sxs-lookup"><span data-stu-id="da603-129">When the appHost setting is enabled, .NET Core generates a native Mach-O executable when you build or publish.</span></span> <span data-ttu-id="da603-130">Aplikacja jest uruchamiana w kontekście appHost, gdy jest uruchamiana z kodu źródłowego za pomocą `dotnet run` polecenia lub bezpośrednio uruchamiając plik wykonywalny "Mach-O".</span><span class="sxs-lookup"><span data-stu-id="da603-130">Your app runs in the context of the appHost when it is run from source code with the `dotnet run` command, or by starting the Mach-O executable directly.</span></span>

<span data-ttu-id="da603-131">Bez appHost jedynym sposobem uruchomienia aplikacji [zależnej od platformy](../deploying/index.md#publish-framework-dependent) jest `dotnet <filename.dll>` polecenie.</span><span class="sxs-lookup"><span data-stu-id="da603-131">Without the appHost, the only way a user can start a [framework-dependent](../deploying/index.md#publish-framework-dependent) app is with the `dotnet <filename.dll>` command.</span></span> <span data-ttu-id="da603-132">AppHost jest zawsze tworzona przy publikowaniu [własnej aplikacji.](../deploying/index.md#publish-self-contained)</span><span class="sxs-lookup"><span data-stu-id="da603-132">An appHost is always created when you publish your app [self-contained](../deploying/index.md#publish-self-contained).</span></span>

<span data-ttu-id="da603-133">Można skonfigurować appHost na poziomie projektu lub przełączać appHost dla określonego `dotnet` polecenia z `-p:UseAppHost` parametrem:</span><span class="sxs-lookup"><span data-stu-id="da603-133">You can either configure the appHost at the project level, or toggle the appHost for a specific `dotnet` command with the `-p:UseAppHost` parameter:</span></span>

- <span data-ttu-id="da603-134">Plik projektu</span><span class="sxs-lookup"><span data-stu-id="da603-134">Project file</span></span>

  ```xml
  <PropertyGroup>
    <UseAppHost>true</UseAppHost>
  </PropertyGroup>
  ```

- <span data-ttu-id="da603-135">Parametr wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="da603-135">Command-line parameter</span></span>

  ```dotnetcli
  dotnet run -p:UseAppHost=true
  ```

<span data-ttu-id="da603-136">Aby uzyskać więcej informacji na temat tego `UseAppHost` Ustawienia, zobacz [Właściwości programu MSBuild dla Microsoft. NET. SDK](../project-sdk/msbuild-props.md#useapphost).</span><span class="sxs-lookup"><span data-stu-id="da603-136">For more information about the `UseAppHost` setting, see [MSBuild properties for Microsoft.NET.Sdk](../project-sdk/msbuild-props.md#useapphost).</span></span>

## <a name="windows-forms"></a><span data-ttu-id="da603-137">Windows Forms</span><span class="sxs-lookup"><span data-stu-id="da603-137">Windows Forms</span></span>

<span data-ttu-id="da603-138">*Tylko Windows*</span><span class="sxs-lookup"><span data-stu-id="da603-138">*Windows only*</span></span>

> [!WARNING]
> <span data-ttu-id="da603-139">Istnieją istotne zmiany w Windows Forms.</span><span class="sxs-lookup"><span data-stu-id="da603-139">There are breaking changes in Windows Forms.</span></span>

<span data-ttu-id="da603-140">Starsze formanty zostały uwzględnione w Windows Forms, które były niedostępne w przyborniku projektanta Visual Studio przez jakiś czas.</span><span class="sxs-lookup"><span data-stu-id="da603-140">Legacy controls were included in Windows Forms that have been unavailable in the Visual Studio Designer Toolbox for some time.</span></span> <span data-ttu-id="da603-141">Zostały one zastąpione nowymi kontrolkami z powrotem w .NET Framework 2,0.</span><span class="sxs-lookup"><span data-stu-id="da603-141">These were replaced with new controls back in .NET Framework 2.0.</span></span> <span data-ttu-id="da603-142">Zostały one usunięte z zestawu Desktop SDK dla platformy .NET Core 3,1.</span><span class="sxs-lookup"><span data-stu-id="da603-142">These have been removed from the Desktop SDK for .NET Core 3.1.</span></span>

| <span data-ttu-id="da603-143">Usunięto kontrolkę</span><span class="sxs-lookup"><span data-stu-id="da603-143">Removed control</span></span> | <span data-ttu-id="da603-144">Zalecane zastąpienie</span><span class="sxs-lookup"><span data-stu-id="da603-144">Recommended replacement</span></span> | <span data-ttu-id="da603-145">Usunięto skojarzone interfejsy API</span><span class="sxs-lookup"><span data-stu-id="da603-145">Associated APIs removed</span></span> |
| --------------- | ----------------------- | ----------------------- |
| <span data-ttu-id="da603-146">DataGrid</span><span class="sxs-lookup"><span data-stu-id="da603-146">DataGrid</span></span>        | <xref:System.Windows.Forms.DataGridView>      | <span data-ttu-id="da603-147">DataGridCell</span><span class="sxs-lookup"><span data-stu-id="da603-147">DataGridCell</span></span><br/><span data-ttu-id="da603-148">DataGridRow</span><span class="sxs-lookup"><span data-stu-id="da603-148">DataGridRow</span></span><br/><span data-ttu-id="da603-149">DataGridTableCollection</span><span class="sxs-lookup"><span data-stu-id="da603-149">DataGridTableCollection</span></span><br/><span data-ttu-id="da603-150">DataGridColumnCollection</span><span class="sxs-lookup"><span data-stu-id="da603-150">DataGridColumnCollection</span></span><br/><span data-ttu-id="da603-151">Element DataGridTableStyle</span><span class="sxs-lookup"><span data-stu-id="da603-151">DataGridTableStyle</span></span><br/><span data-ttu-id="da603-152">DataGridColumnStyle</span><span class="sxs-lookup"><span data-stu-id="da603-152">DataGridColumnStyle</span></span><br/><span data-ttu-id="da603-153">Datasiatki</span><span class="sxs-lookup"><span data-stu-id="da603-153">DataGridLineStyle</span></span><br/><span data-ttu-id="da603-154">DataGridParentRowsLabel</span><span class="sxs-lookup"><span data-stu-id="da603-154">DataGridParentRowsLabel</span></span><br/><span data-ttu-id="da603-155">DataGridParentRowsLabelStyle</span><span class="sxs-lookup"><span data-stu-id="da603-155">DataGridParentRowsLabelStyle</span></span><br/><span data-ttu-id="da603-156">DataGridBoolColumn</span><span class="sxs-lookup"><span data-stu-id="da603-156">DataGridBoolColumn</span></span><br/><span data-ttu-id="da603-157">DataGridTextBox</span><span class="sxs-lookup"><span data-stu-id="da603-157">DataGridTextBox</span></span><br/><span data-ttu-id="da603-158">GridColumnStylesCollection</span><span class="sxs-lookup"><span data-stu-id="da603-158">GridColumnStylesCollection</span></span><br/><span data-ttu-id="da603-159">GridTableStylesCollection</span><span class="sxs-lookup"><span data-stu-id="da603-159">GridTableStylesCollection</span></span><br/><span data-ttu-id="da603-160">HitTestType</span><span class="sxs-lookup"><span data-stu-id="da603-160">HitTestType</span></span> |
| <span data-ttu-id="da603-161">ToolBar</span><span class="sxs-lookup"><span data-stu-id="da603-161">ToolBar</span></span>         | <xref:System.Windows.Forms.ToolStrip>         | <span data-ttu-id="da603-162">ToolBarAppearance</span><span class="sxs-lookup"><span data-stu-id="da603-162">ToolBarAppearance</span></span> |
| <span data-ttu-id="da603-163">ToolBarButton</span><span class="sxs-lookup"><span data-stu-id="da603-163">ToolBarButton</span></span>   | <xref:System.Windows.Forms.ToolStripButton>   | <span data-ttu-id="da603-164">ToolBarButtonClickEventArgs</span><span class="sxs-lookup"><span data-stu-id="da603-164">ToolBarButtonClickEventArgs</span></span><br/><span data-ttu-id="da603-165">ToolBarButtonClickEventHandler</span><span class="sxs-lookup"><span data-stu-id="da603-165">ToolBarButtonClickEventHandler</span></span><br/><span data-ttu-id="da603-166">ToolBarButton</span><span class="sxs-lookup"><span data-stu-id="da603-166">ToolBarButtonStyle</span></span><br/><span data-ttu-id="da603-167">ToolBarTextAlign</span><span class="sxs-lookup"><span data-stu-id="da603-167">ToolBarTextAlign</span></span> |
| <span data-ttu-id="da603-168">ContextMenu</span><span class="sxs-lookup"><span data-stu-id="da603-168">ContextMenu</span></span>     | <xref:System.Windows.Forms.ContextMenuStrip>  |  |
| :::no-loc text="Menu"::: | <xref:System.Windows.Forms.ToolStripDropDown><br/><xref:System.Windows.Forms.ToolStripDropDownMenu> | <span data-ttu-id="da603-169">MenuItemCollection</span><span class="sxs-lookup"><span data-stu-id="da603-169">MenuItemCollection</span></span> |
| <span data-ttu-id="da603-170">MainMenu</span><span class="sxs-lookup"><span data-stu-id="da603-170">MainMenu</span></span>        | <xref:System.Windows.Forms.MenuStrip>         |  |
| <span data-ttu-id="da603-171">MenuItem</span><span class="sxs-lookup"><span data-stu-id="da603-171">MenuItem</span></span>        | <xref:System.Windows.Forms.ToolStripMenuItem> |  |

<span data-ttu-id="da603-172">Zalecamy zaktualizowanie aplikacji do programu .NET Core 3,1 i przejście do kontrolek zastępczych.</span><span class="sxs-lookup"><span data-stu-id="da603-172">We recommend you update your applications to .NET Core 3.1 and move to the replacement controls.</span></span> <span data-ttu-id="da603-173">Zastępowanie formantów jest prostym procesem, zasadniczo "Znajdź i Zamień" w typie.</span><span class="sxs-lookup"><span data-stu-id="da603-173">Replacing the controls is a straightforward process, essentially "find and replace" on the type.</span></span>

## <a name="ccli"></a><span data-ttu-id="da603-174">C++/CLI</span><span class="sxs-lookup"><span data-stu-id="da603-174">C++/CLI</span></span>

<span data-ttu-id="da603-175">*Tylko Windows*</span><span class="sxs-lookup"><span data-stu-id="da603-175">*Windows only*</span></span>

<span data-ttu-id="da603-176">Dodano obsługę tworzenia projektów C++/CLI (nazywanych także "zarządzanymi C++").</span><span class="sxs-lookup"><span data-stu-id="da603-176">Support has been added for creating C++/CLI (also known as "managed C++") projects.</span></span> <span data-ttu-id="da603-177">Pliki binarne wytworzone z tych projektów są zgodne z platformą .NET Core 3,0 i nowszymi wersjami.</span><span class="sxs-lookup"><span data-stu-id="da603-177">Binaries produced from these projects are compatible with .NET Core 3.0 and later versions.</span></span>

<span data-ttu-id="da603-178">Aby dodać obsługę języka C++/CLI w programie Visual Studio 2019 w wersji 16,4, zainstaluj [Programowanie aplikacji klasycznych w języku c++](/cpp/build/vscpp-step-0-installation?view=vs-2019#step-4---choose-workloads).</span><span class="sxs-lookup"><span data-stu-id="da603-178">To add support for C++/CLI in Visual Studio 2019 version 16.4, install the [Desktop development with C++ workload](/cpp/build/vscpp-step-0-installation?view=vs-2019#step-4---choose-workloads).</span></span> <span data-ttu-id="da603-179">To obciążenie dodaje dwa szablony do programu Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="da603-179">This workload adds two templates to Visual Studio:</span></span>

- <span data-ttu-id="da603-180">Biblioteka klas CLR (.NET Core)</span><span class="sxs-lookup"><span data-stu-id="da603-180">CLR Class Library (.NET Core)</span></span>
- <span data-ttu-id="da603-181">Pusty projekt CLR (.NET Core)</span><span class="sxs-lookup"><span data-stu-id="da603-181">CLR Empty Project (.NET Core)</span></span>

## <a name="next-steps"></a><span data-ttu-id="da603-182">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="da603-182">Next steps</span></span>

- [<span data-ttu-id="da603-183">Zapoznaj się z istotnymi zmianami między programem .NET Core 3,0 i 3,1.</span><span class="sxs-lookup"><span data-stu-id="da603-183">Review the breaking changes between .NET Core 3.0 and 3.1.</span></span>](../compatibility/3.1.md)
- [<span data-ttu-id="da603-184">Zapoznaj się z istotnymi zmianami w programie .NET Core 3,1 dla aplikacji Windows Forms.</span><span class="sxs-lookup"><span data-stu-id="da603-184">Review the breaking changes in .NET Core 3.1 for Windows Forms apps.</span></span>](../compatibility/winforms.md#net-core-31)
