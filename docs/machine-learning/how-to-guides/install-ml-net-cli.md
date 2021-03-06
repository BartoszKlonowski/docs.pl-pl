---
title: Jak zainstalować narzędzie ML.NET interfejsu wiersza polecenia (CLI)
description: Dowiedz się, jak zainstalować, uaktualnić, obniżyć i odinstalować narzędzie ML.NET interfejsu wiersza polecenia (CLI).
ms.date: 06/08/2020
ms.custom: mlnet-tooling
ms.openlocfilehash: 13203246411deadf3ab13a5eba0d2c8e6e9027c5
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2020
ms.locfileid: "84602274"
---
# <a name="how-to-install-the-mlnet-command-line-interface-cli-tool"></a>Jak zainstalować narzędzie ML.NET interfejsu wiersza polecenia (CLI)

Dowiedz się, jak zainstalować interfejs wiersza polecenia ML.NET w systemie Windows, Mac lub Linux.

Interfejs wiersza polecenia ML.NET generuje dobrą jakość modeli ML.NET i kod źródłowy przy użyciu zautomatyzowanego uczenia maszynowego (AutoML) i zestawu danych szkoleniowych.

> [!NOTE]
> Ten temat dotyczy ML.NET interfejsu wiersza polecenia i ML.NET AutoML, które są obecnie dostępne w wersji zapoznawczej, a materiał może ulec zmianie.

## <a name="pre-requisites"></a>Wymagania wstępne

- [Zestaw SDK platformy .NET Core 3,1](https://dotnet.microsoft.com/download/dotnet-core/3.1)

- Obowiązkowe [Program Visual Studio 2019](https://visualstudio.microsoft.com/vs/)

Można uruchomić wygenerowane projekty kodu C# w programie Visual Studio, naciskając klawisz `F5` lub z `dotnet run` (interfejs wiersza polecenia platformy .NET Core).

Uwaga: Jeśli po zainstalowaniu zestaw .NET Core SDK `dotnet tool` polecenie nie działa, Wyloguj się z systemu Windows i zaloguj się ponownie.

## <a name="install"></a>Zainstaluj

Interfejs wiersza polecenia ML.NET jest instalowany jak każdy inny narzędzie globalne dotnet. Używasz `dotnet tool install` polecenia interfejs wiersza polecenia platformy .NET Core.

Poniższy przykład pokazuje, jak zainstalować interfejs wiersza polecenia ML.NET w domyślnej lokalizacji źródła danych NuGet:

```dotnetcli
dotnet tool install -g mlnet
```

Jeśli nie można zainstalować narzędzia (czyli jeśli nie jest ono dostępne w domyślnym źródle danych NuGet), wyświetlane są komunikaty o błędach. Sprawdź, czy wybrane źródła danych są sprawdzane.

Jeśli instalacja zakończy się pomyślnie, zostanie wyświetlony komunikat z poleceniem, które służy do wywoływania narzędzia i zainstalowanej wersji, podobnie jak w poniższym przykładzie:

```console
You can invoke the tool using the following command: mlnet
Tool 'mlnet' (version 'X.X.X') was successfully installed.
```

Można potwierdzić, że instalacja zakończyła się pomyślnie, wpisując następujące polecenie:

```console
mlnet
```

Powinna zostać wyświetlona Pomoc dotycząca dostępnych poleceń dla narzędzia mlnet, takiego jak polecenie "Klasyfikacja".

## <a name="install-a-specific-release-version"></a>Zainstaluj określoną wersję wydania

Jeśli próbujesz zainstalować wersję wstępną lub określoną wersję narzędzia, możesz określić [strukturę](../../standard/frameworks.md) przy użyciu następującego formatu:

```dotnetcli
dotnet tool install -g mlnet --framework <FRAMEWORK>
```

Możesz również sprawdzić, czy pakiet jest prawidłowo zainstalowany, wpisując następujące polecenie:

```dotnetcli
dotnet tool list -g
```

## <a name="uninstall-the-cli-package"></a>Odinstalowywanie pakietu interfejsu wiersza polecenia

Wpisz następujące polecenie, aby odinstalować pakiet z komputera lokalnego:

```dotnetcli
dotnet tool uninstall mlnet -g
```

## <a name="update-the-cli-package"></a>Aktualizowanie pakietu interfejsu wiersza polecenia

Wpisz następujące polecenie, aby zaktualizować pakiet z komputera lokalnego:

```dotnetcli
dotnet tool update -g mlnet
```

## <a name="set-up-cli-suggestions-tab-based-auto-completion"></a>Konfigurowanie sugestii interfejsu wiersza polecenia (funkcja automatycznego uzupełniania oparta na kartach)

Ponieważ interfejs wiersza polecenia ML.NET jest oparty na systemie `System.CommandLine` , ma wbudowaną obsługę uzupełniania kart.

Przykład sposobu, w jaki działa funkcja automatycznego uzupełniania kart, jest pokazana w następującej animacji:

![image (obraz)](./media/cli-tab-completion.gif)

"Autouzupełnianie oparte na kartach" (sugestie dotyczące parametrów) działają w programie *Windows PowerShell* i *macOS/Linux bash* , ale nie będzie działać w programie *Windows cmd*.

Aby włączyć tę funkcję, w bieżącej wersji zapoznawczej użytkownik końcowy musi wykonać kilka kroków raz na powłokę poniżej. Po wykonaniu tych czynności uzupełnianie będzie działało dla wszystkich aplikacji, które zostały utworzone przy użyciu `System.CommandLine` takiego interfejsu wiersza polecenia ml.NET.

Na komputerze, na którym chcesz włączyć uzupełnianie, musisz wykonać dwie czynności.

1. Zainstaluj `dotnet-suggest` Narzędzie globalne, uruchamiając następujące polecenie:

    ```dotnetcli
    dotnet tool install dotnet-suggest -g
    ```

2. Dodaj odpowiedni skrypt podkładki do profilu powłoki. Może być konieczne utworzenie pliku profilu powłoki. Skrypt podkładki przekaże żądania ukończenia z powłoki do `dotnet-suggest` Narzędzia, które deleguje do odpowiedniej `System.CommandLine` aplikacji opartej na usłudze.

    - W przypadku bash Dodaj zawartość elementu [dotnet-sugerował-podkładkę. bash](https://github.com/dotnet/System.CommandLine/blob/master/src/System.CommandLine.Suggest/dotnet-suggest-shim.bash) do `~/.bash_profile` .

    - W przypadku programu PowerShell Dodaj zawartość [dotnet-Suggest-Shim. ps1](https://github.com/dotnet/System.CommandLine/blob/master/src/System.CommandLine.Suggest/dotnet-suggest-shim.ps1) do profilu programu PowerShell. Oczekiwaną ścieżkę do profilu programu PowerShell można znaleźć, uruchamiając następujące polecenie w konsoli programu:

    ```console
    echo $profile
    ```

(W przypadku innych powłok należy [poszukać](https://github.com/dotnet/System.CommandLine/issues?q=is%3Aissue+is%3Aopen+label%3A%22shell+suggestion%22) lub otworzyć [problem](https://github.com/dotnet/System.CommandLine/issues)).

## <a name="installation-directory"></a>Katalog instalacji

Interfejs wiersza polecenia ML.NET można zainstalować w katalogu domyślnym lub w określonej lokalizacji. Domyślne katalogi są następujące:

| System operacyjny          | Ścieżka                          |
|-------------|-------------------------------|
| Linux/macOS | `$HOME/.dotnet/tools`         |
| Windows     | `%USERPROFILE%\.dotnet\tools` |

Te lokalizacje są dodawane do ścieżki użytkownika podczas pierwszego uruchomienia zestawu SDK, dzięki czemu globalne narzędzia mogą być wywoływane bezpośrednio.

Uwaga: globalne narzędzia to specyficzne dla użytkownika, a nie globalne maszyny. Specyficzne dla użytkownika oznacza, że nie można zainstalować narzędzia globalnego, które jest dostępne dla wszystkich użytkowników komputera. Narzędzie jest dostępne tylko dla każdego profilu użytkownika, w którym zainstalowano narzędzie.

Narzędzia globalne można także zainstalować w określonym katalogu. Po zainstalowaniu w określonym katalogu użytkownik musi upewnić się, że polecenie jest dostępne, dołączając ten katalog w ścieżce, wywołując polecenie z określonym katalogiem lub wywołując narzędzie z w określonym katalogu.
W takim przypadku interfejs wiersza polecenia platformy .NET Core nie dodaje automatycznie tej lokalizacji do zmiennej środowiskowej PATH.

## <a name="see-also"></a>Zobacz też

- [Przegląd interfejsu wiersza polecenia ML.NET](../automate-training-with-cli.md)
- [Samouczek: analizowanie tonacji za pomocą interfejsu wiersza polecenia ML.NET](../tutorials/sentiment-analysis-cli.md)
- [Przewodnik dotyczący poleceń autouczenia interfejsu wiersza polecenia ML.NET](../reference/ml-net-cli-reference.md)
- [Dane telemetryczne w interfejsie wiersza polecenia ML.NET](../resources/ml-net-cli-telemetry.md)
