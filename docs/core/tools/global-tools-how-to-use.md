---
title: 'Samouczek: Instalowanie i używanie narzędzia globalnego platformy .NET'
description: Dowiedz się, jak zainstalować narzędzie .NET i korzystać z niego jako narzędzia globalnego.
ms.topic: tutorial
ms.date: 02/12/2020
ms.openlocfilehash: 01b773516da92fb16fb0f67fc6617e0c70d17c9d
ms.sourcegitcommit: b201d177e01480a139622f3bf8facd367657a472
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/15/2020
ms.locfileid: "94633898"
---
# <a name="tutorial-install-and-use-a-net-global-tool-using-the-net-cli"></a>Samouczek: Instalowanie i używanie narzędzia globalnego platformy .NET przy użyciu interfejsu wiersza polecenia platformy .NET

**Ten artykuł ma zastosowanie do:** ✔️ .net Core 2,1 SDK i nowszych wersjach

W tym samouczku przedstawiono sposób instalowania i używania narzędzia globalnego. Używasz narzędzia, które tworzysz w [pierwszym samouczku tej serii](global-tools-how-to-create.md).

## <a name="prerequisites"></a>Wymagania wstępne

* Wykonaj [pierwszy samouczek tej serii](global-tools-how-to-create.md).

## <a name="use-the-tool-as-a-global-tool"></a>Użyj narzędzia jako narzędzia globalnego

1. Zainstaluj narzędzie z pakietu, uruchamiając polecenie [dotnet Tool Install](dotnet-tool-install.md) w folderze *Microsoft. botsay* Project:

   ```dotnetcli
   dotnet tool install --global --add-source ./nupkg microsoft.botsay
   ```

   `--global`Parametr nakazuje interfejsowi wiersza polecenia platformy .NET zainstalowanie plików binarnych narzędzia w domyślnej lokalizacji, która jest automatycznie dodawana do zmiennej środowiskowej PATH.

   `--add-source`Parametr informuje interfejs wiersza polecenia platformy .NET, aby tymczasowo używać katalogu *./nupkg* jako dodatkowego źródła strumieniowego dla pakietów NuGet. Pakiet ma unikatową nazwę, aby upewnić się, że zostanie on znaleziony tylko w katalogu *./nupkg* , a nie w witrynie NuGet.org.

   Dane wyjściowe przedstawiają polecenie używane do wywoływania narzędzia i zainstalowanej wersji:

   ```console
   You can invoke the tool using the following command: botsay
   Tool 'microsoft.botsay' (version '1.0.0') was successfully installed.
   ```

1. Wywołaj narzędzie:

   ```console
   botsay hello from the bot
   ```

   > [!NOTE]
   > Jeśli to polecenie nie powiedzie się, może być konieczne otwarcie nowego terminalu w celu odświeżenia ścieżki.

1. Aby usunąć narzędzie, należy wykonać polecenie [odinstalowania narzędzia dotnet](dotnet-tool-uninstall.md) :

   ```dotnetcli
   dotnet tool uninstall -g microsoft.botsay
   ```

## <a name="use-the-tool-as-a-global-tool-installed-in-a-custom-location"></a>Używanie narzędzia jako globalnego narzędzia zainstalowanego w lokalizacji niestandardowej

1. Zainstaluj narzędzie z pakietu.

   W systemie Windows:

   ```dotnetcli
   dotnet tool install --tool-path c:\dotnet-tools --add-source ./nupkg microsoft.botsay
   ```

   W systemie Linux lub macOS:

   ```dotnetcli
   dotnet tool install --tool-path ~/bin --add-source ./nupkg microsoft.botsay
   ```

   `--tool-path`Parametr nakazuje interfejsowi wiersza polecenia platformy .NET zainstalowanie plików binarnych narzędzia w określonej lokalizacji. Jeśli katalog nie istnieje, zostanie utworzony. Ten katalog nie jest automatycznie dodawany do zmiennej środowiskowej PATH.

   Dane wyjściowe przedstawiają polecenie używane do wywoływania narzędzia i zainstalowanej wersji:

   ```console
   You can invoke the tool using the following command: botsay
   Tool 'microsoft.botsay' (version '1.0.0') was successfully installed.
   ```

1. Wywołaj narzędzie:

   W systemie Windows:

   ```console
   c:\dotnet-tools\botsay hello from the bot
   ```

   W systemie Linux lub macOS:

   ```console
   ~/bin/botsay hello from the bot
   ```

1. Aby usunąć narzędzie, należy wykonać polecenie [odinstalowania narzędzia dotnet](dotnet-tool-uninstall.md) :

   W systemie Windows:

   ```dotnetcli
   dotnet tool uninstall --tool-path c:\dotnet-tools microsoft.botsay
   ```

   W systemie Linux lub macOS:

   ```dotnetcli
   dotnet tool uninstall --tool-path ~/bin microsoft.botsay
   ```

## <a name="troubleshoot"></a>Rozwiązywanie problemów

Jeśli podczas wykonywania samouczka zostanie wyświetlony komunikat o błędzie, zobacz [Rozwiązywanie problemów z użyciem narzędzia platformy .NET](troubleshoot-usage-issues.md).

## <a name="next-steps"></a>Następne kroki

W tym samouczku narzędzie zostało zainstalowane i użyte jako narzędzie globalne. Aby zainstalować narzędzie i korzystać z tego samego narzędzia co narzędzie lokalne, przejdź do następnego samouczka.

> [!div class="nextstepaction"]
> [Instalowanie i używanie lokalnych narzędzi](local-tools-how-to-use.md)
