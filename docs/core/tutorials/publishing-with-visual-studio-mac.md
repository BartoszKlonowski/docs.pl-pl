---
title: Publikowanie aplikacji konsolowej .NET przy użyciu Visual Studio dla komputerów Mac
description: Dowiedz się, jak za pomocą Visual Studio dla komputerów Mac utworzyć zestaw plików, które są konieczne do uruchomienia aplikacji platformy .NET.
ms.date: 11/30/2020
ms.openlocfilehash: 88f143011b19ca8eda6610803c894e619d06a635
ms.sourcegitcommit: 9d525bb8109216ca1dc9e39c149d4902f4b43da5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2020
ms.locfileid: "96599192"
---
# <a name="tutorial-publish-a-net-console-application-using-visual-studio-for-mac"></a>Samouczek: publikowanie aplikacji konsolowej .NET przy użyciu Visual Studio dla komputerów Mac

W tym samouczku pokazano, jak opublikować aplikację konsolową, tak aby inni użytkownicy mogli ją uruchomić. Publikowanie tworzy zestaw plików, które są konieczne do uruchomienia aplikacji. Aby wdrożyć pliki, skopiuj je na maszynę docelową.

## <a name="prerequisites"></a>Wymagania wstępne

- Ten samouczek współpracuje z aplikacją konsolową utworzoną w temacie [Tworzenie aplikacji konsolowej platformy .NET przy użyciu Visual Studio dla komputerów Mac](with-visual-studio-mac.md).

## <a name="publish-the-app"></a>Publikowanie aplikacji

1. Rozpocznij Visual Studio dla komputerów Mac.

1. Otwórz projekt HelloWorld, który został utworzony w temacie [Tworzenie aplikacji konsolowej platformy .NET przy użyciu Visual Studio dla komputerów Mac](with-visual-studio-mac.md).

1. Upewnij się, że program Visual Studio kompiluje wydaną wersję aplikacji. W razie potrzeby zmień ustawienie konfiguracji kompilacji na pasku narzędzi z **Debuguj** na **Release**.

   :::image type="content" source="media/publishing-with-visual-studio-mac/toolbar-release.png" alt-text="Program Visual Studio Toolbar z wybraną kompilacją wydania":::

1. Z menu głównego wybierz polecenie **Kompiluj**  >  **Publikuj do folderu.**...

   :::image type="content" source="media/publishing-with-visual-studio-mac/publish-context-menu.png" alt-text="Menu kontekstowe publikacji programu Visual Studio":::

1. W oknie dialogowym **Publikowanie do folderu** wybierz pozycję **Publikuj**.

   :::image type="content" source="media/publishing-with-visual-studio-mac/publish-to-folder-dialog.png" alt-text="Okno dialogowe publikowania do folderu programu Visual Studio":::

   Zostanie otwarty folder publikowanie zawierający pliki, które zostały utworzone.

   :::image type="content" source="media/publishing-with-visual-studio-mac/publish-folder.png" alt-text="folder publikacji":::

1. Wybierz ikonę koła zębatego, a następnie wybierz pozycję **Kopiuj "Publikuj" jako nazwę ścieżki** z menu kontekstowego.

   :::image type="content" source="media/publishing-with-visual-studio-mac/copy-path.png" alt-text="Kopiuj ścieżkę do folderu publikowania":::

## <a name="inspect-the-files"></a>Inspekcja plików

Proces publikowania tworzy wdrożenie zależne od platformy, które jest typem wdrożenia, gdzie opublikowana aplikacja jest uruchamiana na komputerze, na którym zainstalowano środowisko uruchomieniowe platformy .NET. Użytkownicy mogą uruchamiać opublikowaną aplikację, uruchamiając `dotnet HelloWorld.dll` polecenie z poziomu wiersza polecenia.

Jak widać na poprzedniej ilustracji, opublikowane dane wyjściowe zawierają następujące pliki:

* *HelloWorld.deps.jsna*

  Jest to plik zależności środowiska uruchomieniowego aplikacji. Definiuje składniki platformy .NET i biblioteki (w tym bibliotekę dołączaną dynamicznie, która zawiera aplikację) potrzebną do uruchomienia aplikacji. Aby uzyskać więcej informacji, zobacz [pliki konfiguracji środowiska uruchomieniowego](https://github.com/dotnet/cli/blob/85ca206d84633d658d7363894c4ea9d59e515c1a/Documentation/specs/runtime-configuration-file.md).

* *HelloWorld.dll*

   Jest to [zależna od platformy wersja wdrożenia](../deploying/deploy-with-cli.md#framework-dependent-deployment) aplikacji. Aby wykonać tę bibliotekę dołączaną dynamicznie, wprowadź `dotnet HelloWorld.dll` w wierszu polecenia. Ta metoda uruchamiania aplikacji działa na dowolnej platformie, na której zainstalowano środowisko uruchomieniowe platformy .NET.

* *HelloWorld. pdb* (opcjonalnie dla wdrożenia)

   Jest to plik symboli debugowania. Nie musisz wdrażać tego pliku wraz z aplikacją, chociaż należy je zapisać w zdarzeniu, które trzeba debugować opublikowaną wersję aplikacji.

* *HelloWorld.runtimeconfig.jsna*

   To jest plik konfiguracji czasu wykonywania aplikacji. Identyfikuje wersję platformy .NET, w której aplikacja została skompilowana. Możesz również dodać do niej opcje konfiguracji. Aby uzyskać więcej informacji, zobacz [Ustawienia konfiguracji środowiska uruchomieniowego .NET](../run-time-config/index.md#runtimeconfigjson).

## <a name="run-the-published-app"></a>Uruchom opublikowaną aplikację

1. Otwórz Terminal i przejdź do folderu *Publikowanie* . W tym celu wprowadź, `cd` a następnie wklej wcześniej skopiowaną ścieżkę. Na przykład:

   ```console
   cd ~/Projects/HelloWorld/HelloWorld/bin/Release/net5.0/publish/
   ```

1. Uruchom aplikację za pomocą `dotnet` polecenia:

   1. Wprowadź `dotnet HelloWorld.dll` i naciśnij klawisz <kbd>Enter</kbd>.

   1. Wprowadź nazwę w odpowiedzi na monit, a następnie naciśnij dowolny klawisz, aby wyjść.

## <a name="additional-resources"></a>Dodatkowe zasoby

- [Wdrażanie aplikacji .NET](../deploying/index.md)

## <a name="next-steps"></a>Następne kroki

W tym samouczku opublikowano aplikację konsolową. W następnym samouczku utworzysz bibliotekę klas.

> [!div class="nextstepaction"]
> [Tworzenie biblioteki .NET przy użyciu Visual Studio dla komputerów Mac](library-with-visual-studio-mac.md)
