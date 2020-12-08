---
title: Sprawdź zainstalowane wersje programu .NET w systemach Windows, Linux i macOS — .NET
description: Dowiedz się, jak wyświetlić listę wersji platformy .NET zainstalowanych na komputerze. Obejmuje to środowisko uruchomieniowe platformy .NET i zestaw SDK.
author: adegeo
ms.author: adegeo
ms.date: 11/10/2020
ms.custom: updateeachrelease
zone_pivot_groups: operating-systems-set-one
ms.openlocfilehash: 2fc12c8c398b1a74d623e53884df666f4d4b85f1
ms.sourcegitcommit: 45c7148f2483db2501c1aa696ab6ed2ed8cb71b2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/08/2020
ms.locfileid: "96851617"
---
# <a name="how-to-check-that-net-is-already-installed"></a>Jak sprawdzić, czy platforma .NET jest już zainstalowana

W tym artykule przedstawiono sposób sprawdzania, które wersje środowiska uruchomieniowego .NET i zestawu SDK są zainstalowane na komputerze. Jeśli masz zintegrowane środowisko programistyczne, takie jak Visual Studio lub Visual Studio dla komputerów Mac, program .NET mógł już być zainstalowany.

Zainstalowanie zestawu SDK instaluje odpowiednie środowisko uruchomieniowe.

Jeśli którykolwiek z poleceń w tym artykule nie powiedzie się, nie masz zainstalowanego środowiska uruchomieniowego lub zestawu SDK. Aby uzyskać więcej informacji, zobacz artykuły instalacyjne dla [systemu Windows](windows.md), [macOS](macos.md)lub [Linux](linux.md).

## <a name="check-sdk-versions"></a>Sprawdź wersje zestawu SDK

Możesz sprawdzić, które wersje zestawu .NET SDK są obecnie zainstalowane z terminalem. Otwórz Terminal i uruchom następujące polecenie.

```dotnetcli
dotnet --list-sdks
```

Dane wyjściowe są podobne do poniższych.

::: zone pivot="os-windows"

```console
2.1.500 [C:\program files\dotnet\sdk]
2.1.502 [C:\program files\dotnet\sdk]
2.1.504 [C:\program files\dotnet\sdk]
2.1.600 [C:\program files\dotnet\sdk]
2.1.602 [C:\program files\dotnet\sdk]
3.1.100 [C:\program files\dotnet\sdk]
5.0.100 [C:\program files\dotnet\sdk]
```

::: zone-end

::: zone pivot="os-linux"

```bash
2.1.500 [/home/user/dotnet/sdk]
2.1.502 [/home/user/dotnet/sdk]
2.1.504 [/home/user/dotnet/sdk]
2.1.600 [/home/user/dotnet/sdk]
2.1.602 [/home/user/dotnet/sdk]
3.1.100 [/home/user/dotnet/sdk]
5.0.100 [/home/user/dotnet/sdk]
```

::: zone-end

::: zone pivot="os-macos"

```bash
2.1.500 [/usr/local/share/dotnet/sdk]
2.1.502 [/usr/local/share/dotnet/sdk]
2.1.504 [/usr/local/share/dotnet/sdk]
2.1.600 [/usr/local/share/dotnet/sdk]
2.1.602 [/usr/local/share/dotnet/sdk]
3.1.100 [/usr/local/share/dotnet/sdk]
5.0.100 [/usr/local/share/dotnet/sdk]
```

::: zone-end

## <a name="check-runtime-versions"></a>Sprawdź wersje środowiska uruchomieniowego

Możesz sprawdzić, które wersje środowiska uruchomieniowego platformy .NET są obecnie zainstalowane przy użyciu następującego polecenia.

```dotnetcli
dotnet --list-runtimes
```

Dane wyjściowe są podobne do poniższych.

::: zone pivot="os-windows"

```console
Microsoft.AspNetCore.All 2.1.7 [c:\program files\dotnet\shared\Microsoft.AspNetCore.All]
Microsoft.AspNetCore.All 2.1.13 [c:\program files\dotnet\shared\Microsoft.AspNetCore.All]
Microsoft.AspNetCore.App 2.1.7 [c:\program files\dotnet\shared\Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 2.1.13 [c:\program files\dotnet\shared\Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 3.1.0 [c:\program files\dotnet\shared\Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 5.0.0 [c:\program files\dotnet\shared\Microsoft.AspNetCore.App]
Microsoft.NETCore.App 2.1.7 [c:\program files\dotnet\shared\Microsoft.NETCore.App]
Microsoft.NETCore.App 2.1.13 [c:\program files\dotnet\shared\Microsoft.NETCore.App]
Microsoft.NETCore.App 3.1.0 [c:\program files\dotnet\shared\Microsoft.NETCore.App]
Microsoft.NETCore.App 5.0.0 [c:\program files\dotnet\shared\Microsoft.NETCore.App]
Microsoft.WindowsDesktop.App 3.0.0 [c:\program files\dotnet\shared\Microsoft.WindowsDesktop.App]
Microsoft.WindowsDesktop.App 3.1.0 [c:\program files\dotnet\shared\Microsoft.WindowsDesktop.App]
Microsoft.WindowsDesktop.App 5.0.0 [c:\program files\dotnet\shared\Microsoft.WindowsDesktop.App]
```

::: zone-end

::: zone pivot="os-linux"

```bash
Microsoft.AspNetCore.All 2.1.7 [/home/user/dotnet/shared/Microsoft.AspNetCore.All]
Microsoft.AspNetCore.All 2.1.13 [/home/user/dotnet/shared/Microsoft.AspNetCore.All]
Microsoft.AspNetCore.App 2.1.7 [/home/user/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 2.1.13 [/home/user/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 3.1.0 [/home/user/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 5.0.0 [/home/user/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.NETCore.App 2.1.7 [/home/user/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.1.13 [/home/user/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 3.1.0 [/home/user/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 5.0.0 [/home/user/dotnet/shared/Microsoft.NETCore.App]
```

::: zone-end

::: zone pivot="os-macos"

```bash
Microsoft.AspNetCore.All 2.1.7 [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.All]
Microsoft.AspNetCore.All 2.1.13 [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.All]
Microsoft.AspNetCore.App 2.1.7 [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 2.1.13 [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 3.1.0 [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 5.0.0 [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.NETCore.App 2.1.7 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.1.13 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 3.1.0 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 5.0.0 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
```

::: zone-end

## <a name="check-for-install-folders"></a>Sprawdź foldery instalacji

Istnieje możliwość, że platforma .NET jest zainstalowana, ale nie została dodana do `PATH` zmiennej dla systemu operacyjnego lub profilu użytkownika. W takim przypadku polecenia z poprzednich sekcji mogą nie funkcjonować. Alternatywnie można sprawdzić, czy istnieją foldery instalacji platformy .NET.

W przypadku instalowania programu .NET z Instalatora lub skryptu jest on instalowany w folderze standardowym. Większość czasu Instalator lub skrypt używany do instalowania programu .NET udostępnia opcję instalacji w innym folderze. Jeśli zdecydujesz się zainstalować w innym folderze, Dostosuj początek ścieżki folderu.

::: zone pivot="os-windows"

- **plik wykonywalny dotnet**\
_C: \\ program files \\ \\dotnet.exedotnet_

- **ZESTAW SDK PLATFORMY .NET**\
_C: \\ Program Files \\ \\ zestaw dotnet SDK \\ {Version}\\_

- **Środowisko uruchomieniowe platformy .NET**\
_C: \\ Program Files \\ \\ Shared dotnet \\ {Runtime-Type} \\ {Version}\\_

::: zone-end

::: zone pivot="os-linux"

- **plik wykonywalny dotnet**\
_/home/user/share/dotnet/dotnet_

- **ZESTAW SDK PLATFORMY .NET**\
_/home/user/share/dotnet/sdk/{version}/_

- **Środowisko uruchomieniowe platformy .NET**\
_/home/user/share/dotnet/shared/{runtime-type}/{version}/_

::: zone-end

::: zone pivot="os-macos"

- **plik wykonywalny dotnet**\
_/usr/local/share/dotnet/dotnet_

- **ZESTAW SDK PLATFORMY .NET**\
_/usr/local/share/dotnet/sdk/{version}/_

- **Środowisko uruchomieniowe platformy .NET**\
_/usr/local/share/dotnet/shared/{runtime-type}/{version}/_

::: zone-end

## <a name="more-information"></a>Więcej informacji

Można wyświetlić zarówno wersje zestawu SDK, jak i wersje środowiska uruchomieniowego za pomocą polecenia `dotnet --info` . Uzyskasz również inne informacje dotyczące środowiska, takie jak wersja systemu operacyjnego i identyfikator środowiska uruchomieniowego (RID).

## <a name="next-steps"></a>Następne kroki

- [Zainstaluj środowisko uruchomieniowe platformy .NET i zestaw SDK dla systemu Windows](windows.md).
- [Zainstaluj środowisko uruchomieniowe platformy .NET i zestaw SDK dla macOS](macos.md).
- [Zainstaluj środowisko uruchomieniowe platformy .NET i zestaw SDK dla systemu Linux](linux.md).

## <a name="see-also"></a>Zobacz też

- [Ustal, które wersje .NET Framework są zainstalowane](../../framework/migration-guide/how-to-determine-which-versions-are-installed.md)
