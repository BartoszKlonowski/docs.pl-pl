---
title: Debugowanie aplikacji konsolowej .NET przy użyciu Visual Studio dla komputerów Mac
description: Dowiedz się, jak debugować aplikację konsolową .NET przy użyciu programu Visual Studio Mac.
ms.date: 11/30/2020
ms.openlocfilehash: e35bbef5582b6eec00ee48669a0f5d028eb051fb
ms.sourcegitcommit: 9d525bb8109216ca1dc9e39c149d4902f4b43da5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2020
ms.locfileid: "96599619"
---
# <a name="tutorial-debug-a-net-console-application-using-visual-studio-for-mac"></a>Samouczek: debugowanie aplikacji konsolowej .NET przy użyciu Visual Studio dla komputerów Mac

W tym samouczku przedstawiono narzędzia debugowania dostępne w Visual Studio dla komputerów Mac.

## <a name="prerequisites"></a>Wymagania wstępne

- Ten samouczek współpracuje z aplikacją konsolową utworzoną w temacie [Tworzenie aplikacji konsolowej platformy .NET przy użyciu Visual Studio dla komputerów Mac](with-visual-studio-mac.md).

## <a name="use-debug-build-configuration"></a>Użyj konfiguracji kompilacji debugowania

*Debugowanie* i *wydanie* to wbudowane konfiguracje kompilacji programu Visual Studio. Konfiguracja kompilacji debugowania umożliwia debugowanie i konfigurację wydania dla ostatecznej dystrybucji wersji.

W konfiguracji debugowania program kompiluje z pełnymi symbolicznymi informacjami o debugowaniu i bez optymalizacji. Optymalizacja komplikuje debugowanie, ponieważ relacja między kodem źródłowym i wygenerowanymi instrukcjami jest bardziej skomplikowana. Konfiguracja wydania programu nie ma symbolicznych informacji o debugowaniu i jest w pełni zoptymalizowana.

Domyślnie Visual Studio dla komputerów Mac używa konfiguracji kompilacji debugowania, więc nie trzeba jej zmieniać przed debugowaniem.

1. Rozpocznij Visual Studio dla komputerów Mac.

1. Otwórz projekt, który został utworzony w temacie [Tworzenie aplikacji konsolowej platformy .NET przy użyciu Visual Studio dla komputerów Mac](with-visual-studio-mac.md).

   Bieżąca konfiguracja kompilacji jest pokazywana na pasku narzędzi. Poniższy obraz paska narzędzi pokazuje, że program Visual Studio jest skonfigurowany do kompilowania wersji do debugowania aplikacji:

   :::image type="content" source="media/debugging-with-visual-studio-mac/visual-studio-toolbar-debug.png" alt-text="Pasek narzędzi programu Visual Studio z wyróżnioną pozycją Debug":::

## <a name="set-a-breakpoint"></a>Ustawianie punktu przerwania

*Punkt przerwania* tymczasowo przerywa wykonywanie aplikacji przed wykonaniem wiersza z punktem przerwania.

1. Ustaw punkt przerwania w wierszu, w którym wyświetlana jest nazwa, Data i godzina. Aby to zrobić, umieść kursor w wierszu kodu i naciśnij pozycję <kbd>⌘</kbd> <kbd>\\</kbd> (<kbd>polecenie</kbd> + <kbd>\\</kbd> ). Innym sposobem ustawienia punktu przerwania jest wybranie opcji **Uruchom**  >  **punkt przerwania** z menu.

   Program Visual Studio wskazuje wiersz, w którym ustawiany jest punkt przerwania, zaznaczając go i wyświetlając czerwoną kropkę na lewym marginesie.

   :::image type="content" source="media/debugging-with-visual-studio-mac/set-breakpoint-in-editor.png" alt-text="Okno programu Visual Studio z ustawionym punktem przerwania":::

1. Naciśnij pozycję <kbd>⌘</kbd><kbd>↵</kbd> (<kbd>command</kbd> + <kbd>wprowadź</kbd>polecenie), aby uruchomić program w trybie debugowania. Innym sposobem rozpoczęcia debugowania jest wybranie polecenia **Uruchom**  >  **debugowanie** z menu.

1. Wprowadź ciąg w oknie terminalu, gdy program zapyta o nazwę, a następnie naciśnij klawisz <kbd>Enter</kbd>.

1. Wykonanie programu zostaje zatrzymane po osiągnięciu punktu przerwania, zanim `Console.WriteLine` Metoda zostanie wykonana.

   :::image type="content" source="media/debugging-with-visual-studio-mac/breakpoint-hit.png" alt-text="Zrzut ekranu punktu przerwania w programie Visual Studio":::

## <a name="use-the-immediate-window"></a>Korzystanie z okna bezpośredniego

Okno **bezpośrednie** umożliwia korzystanie z debugowanej aplikacji. Możesz interaktywnie zmienić wartość zmiennych, aby zobaczyć, jak ma to wpływ na program.

1. Jeśli okno **bezpośrednie** nie jest widoczne, Wyświetl je, wybierając pozycję **Wyświetl**  >  **konsole debugowania**  >  **natychmiast**.

1. Wprowadź `name = "Gracie"` w oknie **bezpośrednim** i naciśnij klawisz <kbd>Enter</kbd>.

1. Wprowadź `date = date.AddDays(1)` w oknie **bezpośrednim** i naciśnij klawisz <kbd>Enter</kbd>.

   W oknie **bezpośrednim** zostanie wyświetlona nowa wartość zmiennej ciągu i właściwości <xref:System.DateTime> wartości.

   :::image type="content" source="media/debugging-with-visual-studio-mac/immediate-window.png" alt-text="Okno bezpośrednie w programie Visual Studio":::

   W oknie **Ustawienia lokalne** są wyświetlane wartości zmiennych, które są zdefiniowane w aktualnie wykonywanej metodzie. Wartości zmiennych, które właśnie zmieniono, są aktualizowane w oknie **zmiennych lokalnych** .

   :::image type="content" source="media/debugging-with-visual-studio-mac/locals-window.png" alt-text="Okno zmiennych lokalnych w programie Visual Studio":::

1. Naciśnij pozycję <kbd>⌘</kbd><kbd>↵</kbd> (<kbd>command</kbd> + <kbd>wprowadź</kbd>polecenie), aby kontynuować debugowanie.

   Wartości wyświetlane w terminalu odpowiadają zmianom wprowadzonym w oknie **bezpośrednim** .

   Jeśli nie widzisz terminalu, wybierz pozycję **Terminal — HelloWorld** na dolnym pasku nawigacyjnym.

   :::image type="content" source="media/debugging-with-visual-studio-mac/terminal-hello-world.png" alt-text="Hello world terminalu na dolnym pasku nawigacyjnym":::

1. Naciśnij dowolny klawisz, aby zakończyć program.

1. Zamknij okno terminalu.

## <a name="set-a-conditional-breakpoint"></a>Ustaw punkt przerwania warunkowego

Program wyświetla ciąg wprowadzony przez użytkownika. Co się stanie, jeśli użytkownik nie wprowadzi niczego? Można to sprawdzić za pomocą przydatnej funkcji debugowania zwanej *warunkowym punktem przerwania*.

1. <kbd>naciśnij klawisz Ctrl</kbd>i kliknij czerwoną kropkę, która reprezentuje punkt przerwania. W menu kontekstowym wybierz polecenie **Edytuj punkt przerwania**.

1. W oknie dialogowym **Edytowanie punktu przerwania** wprowadź następujący kod w poniższym polu **i następujący warunek jest spełniony**, a następnie wybierz pozycję **Zastosuj**.

   ```csharp
   String.IsNullOrEmpty(name)
   ```

   :::image type="content" source="media/debugging-with-visual-studio-mac/breakpoint-settings.png" alt-text="Edytor przedstawiający panel ustawień punktu przerwania":::

   Za każdym razem, gdy punkt przerwania został trafiony, debuger wywołuje `String.IsNullOrEmpty(name)` metodę i przerywa w tym wierszu tylko wtedy, gdy wywołanie metody zwróci wartość `true` .

   Zamiast wyrażenia warunkowego można określić *liczbę trafień*, która przerywa wykonywanie programu, zanim instrukcja zostanie wykonana określoną liczbę razy.

1. Naciśnij pozycję <kbd>⌘</kbd><kbd>↵</kbd> (<kbd>command</kbd> + <kbd>wprowadź</kbd>polecenie), aby rozpocząć debugowanie.

1. W oknie terminalu naciśnij klawisz <kbd>Enter</kbd> po wyświetleniu monitu o wprowadzenie nazwy.

   Ponieważ określony warunek ( `name` is `null` lub <xref:System.String.Empty?displayProperty=nameWithType> ) został spełniony, wykonanie programu zatrzyma się po osiągnięciu punktu przerwania.

1. Wybierz okno zmienne **lokalne** , które pokazuje wartości zmiennych, które są lokalne dla aktualnie wykonywanej metody. W tym przypadku `Main` jest obecnie wykonywana metoda. Zwróć uwagę, że wartość `name` zmiennej to `""` <xref:System.String.Empty?displayProperty=nameWithType> .

1. Możesz również sprawdzić, czy wartość jest pustym ciągiem, wprowadzając `name` nazwę zmiennej w oknie **bezpośrednim** i naciskając klawisz <kbd>Enter</kbd>.

   :::image type="content" source="media/debugging-with-visual-studio-mac/immediate-window-output.png" alt-text="Bezpośrednie okno pokazujące nazwę jest pustym ciągiem":::

1. Naciśnij pozycję <kbd>⌘</kbd><kbd>↵</kbd> (<kbd>command</kbd> + <kbd>wprowadź</kbd>polecenie), aby kontynuować debugowanie.

1. W oknie terminalu naciśnij dowolny klawisz, aby wyjść z programu.

1. Zamknij okno terminalu.

1. Wyczyść punkt przerwania, klikając czerwoną kropkę na lewym marginesie okna kod. Innym sposobem na wyczyszczenie punktu przerwania jest wybranie opcji **uruchom > Przełącz punkt przerwania** , gdy zostanie wybrany wiersz kodu.

## <a name="step-through-a-program"></a>Przechodzenie przez program

Program Visual Studio umożliwia również krok po kroku w wierszu przez program i monitorowanie jego wykonania. Zwykle ustawiasz punkt przerwania i obserwuj przepływ programu za pomocą niewielkiej części kodu programu. Ponieważ ten program jest mały, możesz przejść przez cały program.

1. Ustaw punkt przerwania w nawiasach klamrowych, który oznacza początek `Main` metody (naciśnięcie <kbd>polecenia</kbd> + <kbd>\\</kbd> ).

1. Naciśnij pozycję <kbd>⌘</kbd><kbd>↵</kbd> (<kbd>command</kbd> + <kbd>wprowadź</kbd>polecenie), aby rozpocząć debugowanie.

   Program Visual Studio przestaje działać w wierszu z punktem przerwania.

1. Naciśnij <kbd>⇧</kbd><kbd>⌘</kbd><kbd>I</kbd> (<kbd>SHIFT</kbd> + <kbd>Command</kbd> + <kbd>i</kbd>) lub wybierz pozycję **Uruchom**  >  **krok** do góry, aby przejść do wiersza.

   Program Visual Studio podświetla i wyświetli strzałkę obok następnego wiersza wykonania.

   :::image type="content" source="media/debugging-with-visual-studio-mac/step-into-method.png" alt-text="Visual Studio — Wkrocz do metody":::

   W tym momencie okno zmienne **lokalne** pokazuje, że `args` Tablica jest pusta i `name` i `date` ma wartości domyślne. Ponadto program Visual Studio otworzył pusty Terminal.

1. Naciśnij pozycję <kbd>⇧</kbd><kbd>⌘</kbd><kbd>i</kbd> (<kbd>SHIFT</kbd> + <kbd>Command</kbd> + <kbd>i</kbd>).

   Program Visual Studio podświetla instrukcję, która zawiera `name` przypisanie zmiennej. W oknie **Ustawienia lokalne** zostanie wyświetlona `name` wartość `null` , a w terminalu zostanie wyświetlony ciąg "co to jest Twoja nazwa?".

1. Odpowiedz na monit, wprowadzając ciąg w oknie konsoli i naciskając klawisz <kbd>Enter</kbd>.

1. Naciśnij pozycję <kbd>⇧</kbd><kbd>⌘</kbd><kbd>i</kbd> (<kbd>SHIFT</kbd> + <kbd>Command</kbd> + <kbd>i</kbd>).

   Program Visual Studio podświetla instrukcję, która zawiera `date` przypisanie zmiennej. Okno zmienne **lokalne** pokazuje wartość zwracaną przez wywołanie <xref:System.Console.ReadLine%2A?displayProperty=nameWithType> metody. Terminal wyświetla ciąg wprowadzony w wierszu polecenia.

1. Naciśnij pozycję <kbd>⇧</kbd><kbd>⌘</kbd><kbd>i</kbd> (<kbd>SHIFT</kbd> + <kbd>Command</kbd> + <kbd>i</kbd>).

   Okno **lokalne** pokazuje wartość `date` zmiennej po przypisaniu z <xref:System.DateTime.Now?displayProperty=nameWithType> właściwości. Terminal nie jest zmieniany.

1. Naciśnij pozycję <kbd>⇧</kbd><kbd>⌘</kbd><kbd>i</kbd> (<kbd>SHIFT</kbd> + <kbd>Command</kbd> + <kbd>i</kbd>).

   Program Visual Studio wywołuje <xref:System.Console.WriteLine(System.String,System.Object,System.Object)?displayProperty=nameWithType> metodę. Terminal wyświetla sformatowany ciąg.

1. Naciśnij <kbd>⇧</kbd><kbd>⌘</kbd><kbd>U</kbd> (<kbd>SHIFT</kbd> + <kbd>Command</kbd> + <kbd>u</kbd>) lub wybierz opcję **Run**  >  **Wyjdź out**.

   Terminal wyświetla komunikat i czeka na naciśnięcie klawisza.

1. Naciśnij dowolny klawisz, aby zakończyć program.

## <a name="use-release-build-configuration"></a>Użyj konfiguracji kompilacji wydania

Po przetestowaniu wersji debugowania aplikacji należy również skompilować i przetestować wersję publikacji. Wersja wydania obejmuje optymalizacje kompilatora, które mogą negatywnie wpłynąć na zachowanie aplikacji. Na przykład optymalizacje kompilatora, które mają na celu poprawę wydajności, mogą tworzyć sytuacje wyścigu w aplikacjach wielowątkowych.

Aby skompilować i przetestować wydaną wersję aplikacji konsolowej, wykonaj następujące czynności:

1. Zmień konfigurację kompilacji na pasku narzędzi z **Debuguj** do **Release**.

   :::image type="content" source="media/debugging-with-visual-studio-mac/visual-studio-toolbar-release.png" alt-text="domyślny pasek narzędzi programu Visual Studio z wyróżnioną pozycją Debug":::

1. Naciśnij pozycję <kbd>⌥</kbd><kbd>⌘</kbd><kbd>↵</kbd> (<kbd>Option</kbd> + <kbd>Command</kbd> + <kbd>Enter</kbd>), aby uruchomić bez debugowania.

## <a name="next-steps"></a>Następne kroki

W tym samouczku użyto narzędzi debugowania programu Visual Studio. W następnym samouczku zostanie opublikowana wersja aplikacji, którą można wdrożyć.

> [!div class="nextstepaction"]
> [Publikowanie aplikacji konsolowej .NET przy użyciu Visual Studio dla komputerów Mac](publishing-with-visual-studio-mac.md)
