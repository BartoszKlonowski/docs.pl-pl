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
# <a name="whats-new-in-net-core-31"></a>Co nowego w programie .NET Core 3.1

W tym artykule opisano nowości w programie .NET Core 3,1. Ta wersja zawiera drobne ulepszenia programu .NET Core 3,0, skupiając się na małych, ale ważnych poprawkach. Najważniejszym elementem na platformie .NET Core 3,1 jest to, że jest to wersja [długoterminowa (LTS)](#long-term-support) .

W przypadku korzystania z programu Visual Studio 2019 należy zaktualizować do [programu Visual studio 2019 w wersji 16,4 lub nowszej](https://visualstudio.microsoft.com/downloads/) , aby współpracować z projektami .net Core 3,1. Aby uzyskać informacje na temat Nowości w programie Visual Studio w wersji 16,4, zobacz [co nowego w programie Visual studio 2019 w wersji 16,4](/visualstudio/releases/2019/release-notes-v16.4#whats-new-in-visual-studio-2019-version-164).

Visual Studio dla komputerów Mac obsługuje również program .NET Core 3,1 w Visual Studio dla komputerów Mac 8,4.

Aby uzyskać więcej informacji o wersji, zobacz [anons programu .NET Core 3,1](https://devblogs.microsoft.com/dotnet/announcing-net-core-3-1/).

- [Pobierz i Rozpocznij pracę z platformą .NET Core 3,1](https://dotnet.microsoft.com/download/dotnet-core/3.1) w systemie Windows, MacOS lub Linux.

## <a name="long-term-support"></a>Długoterminowa pomoc techniczna

.NET Core 3,1 to wersja LTS z pomocą techniczną firmy Microsoft przez kolejne trzy lata. Zdecydowanie zalecamy, aby przenieść aplikacje do programu .NET Core 3,1. Bieżący cykl życia innych głównych wydań jest następujący:

| Release | Uwaga |
| ------- | ---- |
| .NET Core 3.0 | Koniec okresu życia w dniu 3 marca 2020.     |
| .NET Core 2.2 | Koniec okresu istnienia 23 grudnia 2019. |
| .NET Core 2.1 | Koniec okresu istnienia 21 sierpnia 2021.    |

Aby uzyskać więcej informacji, zobacz [zasady obsługi .NET Core](https://dotnet.microsoft.com/platform/support/policy/dotnet-core).

## <a name="macos-apphost-and-notarization"></a>macOS appHost i notarization

*Tylko macOS*

Począwszy od zestaw .NET Core SDK 3,1 dla macOS, ustawienie appHost jest domyślnie wyłączone. Aby uzyskać więcej informacji, zobacz [MacOS Catalina Notarization i wpływ na pobieranie i projekty platformy .NET Core](../install/macos-notarization-issues.md).

Gdy ustawienie appHost jest włączone, program .NET Core generuje natywny plik konfiguracji Mach-O podczas kompilowania lub publikowania. Aplikacja jest uruchamiana w kontekście appHost, gdy jest uruchamiana z kodu źródłowego za pomocą `dotnet run` polecenia lub bezpośrednio uruchamiając plik wykonywalny "Mach-O".

Bez appHost jedynym sposobem uruchomienia aplikacji [zależnej od platformy](../deploying/index.md#publish-framework-dependent) jest `dotnet <filename.dll>` polecenie. AppHost jest zawsze tworzona przy publikowaniu [własnej aplikacji.](../deploying/index.md#publish-self-contained)

Można skonfigurować appHost na poziomie projektu lub przełączać appHost dla określonego `dotnet` polecenia z `-p:UseAppHost` parametrem:

- Plik projektu

  ```xml
  <PropertyGroup>
    <UseAppHost>true</UseAppHost>
  </PropertyGroup>
  ```

- Parametr wiersza polecenia

  ```dotnetcli
  dotnet run -p:UseAppHost=true
  ```

Aby uzyskać więcej informacji na temat tego `UseAppHost` Ustawienia, zobacz [Właściwości programu MSBuild dla Microsoft. NET. SDK](../project-sdk/msbuild-props.md#useapphost).

## <a name="windows-forms"></a>Windows Forms

*Tylko Windows*

> [!WARNING]
> Istnieją istotne zmiany w Windows Forms.

Starsze formanty zostały uwzględnione w Windows Forms, które były niedostępne w przyborniku projektanta Visual Studio przez jakiś czas. Zostały one zastąpione nowymi kontrolkami z powrotem w .NET Framework 2,0. Zostały one usunięte z zestawu Desktop SDK dla platformy .NET Core 3,1.

| Usunięto kontrolkę | Zalecane zastąpienie | Usunięto skojarzone interfejsy API |
| --------------- | ----------------------- | ----------------------- |
| DataGrid        | <xref:System.Windows.Forms.DataGridView>      | DataGridCell<br/>DataGridRow<br/>DataGridTableCollection<br/>DataGridColumnCollection<br/>Element DataGridTableStyle<br/>DataGridColumnStyle<br/>Datasiatki<br/>DataGridParentRowsLabel<br/>DataGridParentRowsLabelStyle<br/>DataGridBoolColumn<br/>DataGridTextBox<br/>GridColumnStylesCollection<br/>GridTableStylesCollection<br/>HitTestType |
| ToolBar         | <xref:System.Windows.Forms.ToolStrip>         | ToolBarAppearance |
| ToolBarButton   | <xref:System.Windows.Forms.ToolStripButton>   | ToolBarButtonClickEventArgs<br/>ToolBarButtonClickEventHandler<br/>ToolBarButton<br/>ToolBarTextAlign |
| ContextMenu     | <xref:System.Windows.Forms.ContextMenuStrip>  |  |
| :::no-loc text="Menu"::: | <xref:System.Windows.Forms.ToolStripDropDown><br/><xref:System.Windows.Forms.ToolStripDropDownMenu> | MenuItemCollection |
| MainMenu        | <xref:System.Windows.Forms.MenuStrip>         |  |
| MenuItem        | <xref:System.Windows.Forms.ToolStripMenuItem> |  |

Zalecamy zaktualizowanie aplikacji do programu .NET Core 3,1 i przejście do kontrolek zastępczych. Zastępowanie formantów jest prostym procesem, zasadniczo "Znajdź i Zamień" w typie.

## <a name="ccli"></a>C++/CLI

*Tylko Windows*

Dodano obsługę tworzenia projektów C++/CLI (nazywanych także "zarządzanymi C++"). Pliki binarne wytworzone z tych projektów są zgodne z platformą .NET Core 3,0 i nowszymi wersjami.

Aby dodać obsługę języka C++/CLI w programie Visual Studio 2019 w wersji 16,4, zainstaluj [Programowanie aplikacji klasycznych w języku c++](/cpp/build/vscpp-step-0-installation?view=vs-2019#step-4---choose-workloads). To obciążenie dodaje dwa szablony do programu Visual Studio:

- Biblioteka klas CLR (.NET Core)
- Pusty projekt CLR (.NET Core)

## <a name="next-steps"></a>Następne kroki

- [Zapoznaj się z istotnymi zmianami między programem .NET Core 3,0 i 3,1.](../compatibility/3.1.md)
- [Zapoznaj się z istotnymi zmianami w programie .NET Core 3,1 dla aplikacji Windows Forms.](../compatibility/winforms.md#net-core-31)
