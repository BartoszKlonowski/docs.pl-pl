---
title: Debugowanie aplikacji konsolowej .NET przy użyciu Visual Studio Code
description: Dowiedz się, jak debugować aplikację konsolową .NET przy użyciu Visual Studio Code.
ms.date: 05/26/2020
ms.openlocfilehash: 7215ed4a93b31ebac313c04708734667148c4e02
ms.sourcegitcommit: 30fef5b0ed76e334377d28fa8e80159b29353e10
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/03/2020
ms.locfileid: "96556112"
---
# <a name="tutorial-debug-a-net-console-application-using-visual-studio-code"></a>Samouczek: debugowanie aplikacji konsolowej .NET przy użyciu Visual Studio Code

W tym samouczku przedstawiono narzędzia debugowania dostępne w Visual Studio Code do pracy z aplikacjami .NET.

## <a name="prerequisites"></a>Wymagania wstępne

- Ten samouczek współpracuje z aplikacją konsolową utworzoną w temacie [Tworzenie aplikacji konsolowej platformy .NET przy użyciu Visual Studio Code](with-visual-studio-code.md).

## <a name="use-debug-build-configuration"></a>Użyj konfiguracji kompilacji debugowania

*Debugowanie* i *wydanie* to wbudowane konfiguracje kompilacji platformy .NET Core. Konfiguracja kompilacji debugowania umożliwia debugowanie i konfigurację wydania dla ostatecznej dystrybucji wersji.

W konfiguracji debugowania program kompiluje z pełnymi symbolicznymi informacjami o debugowaniu i bez optymalizacji. Optymalizacja komplikuje debugowanie, ponieważ relacja między kodem źródłowym i wygenerowanymi instrukcjami jest bardziej skomplikowana. Konfiguracja wydania programu nie ma symbolicznych informacji o debugowaniu i jest w pełni zoptymalizowana.

Domyślnie ustawienia uruchamiania Visual Studio Code używają konfiguracji kompilacji debugowania, więc nie trzeba jej zmieniać przed debugowaniem.

1. Uruchom program Visual Studio Code.

1. Otwórz folder projektu, który został utworzony w temacie [Tworzenie aplikacji konsolowej platformy .NET przy użyciu Visual Studio Code](with-visual-studio-code.md).

## <a name="set-a-breakpoint"></a>Ustawianie punktu przerwania

*Punkt przerwania* tymczasowo przerywa wykonywanie aplikacji przed wykonaniem wiersza z punktem przerwania.

1. Otwórz plik *program.cs* .

1. Ustaw *punkt przerwania* w wierszu, który wyświetla nazwę, datę i godzinę, klikając na lewym marginesie okna kod. Lewy margines znajduje się po lewej stronie numerów wierszy. Innymi sposobami ustawiania punktu przerwania są naciśnięcie klawisza <kbd>F9</kbd> **lub wybranie polecenia**  >  **Przełącz punkt przerwania** z menu podczas wybierania wiersza kodu.

   Visual Studio Code wskazuje wiersz, w którym jest ustawiony punkt przerwania, wyświetlając czerwoną kropkę na lewym marginesie.

   :::image type="content" source="media/debugging-with-visual-studio-code/breakpoint-set.png" alt-text="Zestaw punktów przerwania":::

## <a name="set-up-for-terminal-input"></a>Konfiguracja dla danych wejściowych terminalu

Punkt przerwania znajduje się po `Console.ReadLine` wywołaniu metody. **Konsola debugowania** nie akceptuje danych wejściowych terminalu dla uruchomionego programu. Aby obsługiwać dane wejściowe terminalu podczas debugowania, można użyć terminalu zintegrowanego (jednego z okien programu Visual Studio Code) lub terminalu zewnętrznego. W tym samouczku użyjesz zintegrowanego terminalu.

1. Otwórz plik *.vscode/launch.json*.

1. Zmień `console` ustawienie z `internalConsole` na `integratedTerminal` :

   ```json
   "console": "integratedTerminal",
   ```

1. Zapisz zmiany.

## <a name="start-debugging"></a>Rozpocznij debugowanie

1. Otwórz widok debugowanie, wybierając ikonę debugowania w menu po lewej stronie.

   :::image type="content" source="media/debugging-with-visual-studio-code/select-debug-pane.png" alt-text="Otwórz kartę debugowanie w Visual Studio Code":::

1. Wybierz zieloną strzałkę w górnej części okienka, obok pozycji **.NET Core Launch (konsola)**. Innymi sposobami uruchamiania programu w trybie debugowania są naciśnięcie klawisza <kbd>F5</kbd> lub wybranie polecenia **Uruchom**  >  **debugowanie** z menu.

   :::image type="content" source="media/debugging-with-visual-studio-code/start-debugging.png" alt-text="Rozpocznij debugowanie":::

1. Wybierz kartę **Terminal** , aby zobaczyć "Jaka jest Twoja nazwa?". Monituj o wyświetlenie programu przed oczekiwaniem na odpowiedź.

   :::image type="content" source="media/debugging-with-visual-studio-code/select-terminal.png" alt-text="Wybierz kartę Terminal":::

1. Wprowadź ciąg w oknie **terminalu** w odpowiedzi na monit o podanie nazwy, a następnie naciśnij klawisz <kbd>Enter</kbd>.

   Wykonanie programu zostaje zatrzymane po osiągnięciu punktu przerwania i przed wykonaniem `Console.WriteLine` metody. Sekcja **locales** w oknie **zmienne** zawiera wartości zmiennych, które są zdefiniowane w aktualnie wykonywanej metodzie.

   :::image type="content" source="media/debugging-with-visual-studio-code/breakpoint-hit.png" alt-text="Trafienie punktu przerwania, Wyświetlanie ustawień lokalnych":::

## <a name="use-the-debug-console"></a>Korzystanie z konsoli debugowania

Okno **konsoli debugowania** umożliwia korzystanie z debugowanej aplikacji. Można zmienić wartość zmiennych, aby zobaczyć, jak ma to wpływ na program.

1. Wybierz kartę **konsola debugowania** .

1. Wprowadź `name = "Gracie"` w wierszu polecenia u dołu okna **konsoli debugowania** i naciśnij klawisz <kbd>Enter</kbd> .

   :::image type="content" source="media/debugging-with-visual-studio-code/change-variable-values.png" alt-text="Zmień wartości zmiennych":::

1. Wprowadź `date = DateTime.Parse("2019-11-16T17:25:00Z").ToUniversalTime()` w dolnej części okna **konsoli debugowania** i naciśnij klawisz <kbd>Enter</kbd> .

   W oknie **zmienne** są wyświetlane nowe wartości `name` `date` zmiennych i.

1. Kontynuuj wykonywanie programu, wybierając przycisk **Kontynuuj** na pasku narzędzi. Innym sposobem, aby kontynuować, jest naciśnięcie klawisza <kbd>F5</kbd>.

   :::image type="content" source="media/debugging-with-visual-studio-code/continue-debugging.png" alt-text="Kontynuuj debugowanie":::

1. Ponownie wybierz kartę **terminala** .

   Wartości wyświetlane w oknie konsoli odpowiadają zmianom wprowadzonym w **konsoli debugowania**.

   :::image type="content" source="media/debugging-with-visual-studio-code/changed-variable-values.png" alt-text="Terminal pokazujący wprowadzone wartości":::

1. Naciśnij dowolny klawisz, aby zamknąć aplikację i zatrzymać debugowanie.

## <a name="set-a-conditional-breakpoint"></a>Ustaw punkt przerwania warunkowego

Program wyświetla ciąg wprowadzony przez użytkownika. Co się stanie, jeśli użytkownik nie wprowadzi niczego? Można to sprawdzić za pomocą przydatnej funkcji debugowania zwanej *warunkowym punktem przerwania*.

1. Kliknij prawym przyciskiem myszy (<kbd>Ctrl</kbd>-kliknięcie macOS) na czerwoną kropkę reprezentującą punkt przerwania. W menu kontekstowym wybierz pozycję **Edytuj punkt przerwania** , aby otworzyć okno dialogowe, które umożliwia wprowadzenie wyrażenia warunkowego.

   :::image type="content" source="media/debugging-with-visual-studio-code/breakpoint-context-menu.png" alt-text="Menu kontekstowe punktu przerwania":::

1. Wybierz `Expression` z listy rozwijanej, wprowadź następujące wyrażenie warunkowe, a następnie naciśnij klawisz <kbd>Enter</kbd>.

   ```csharp
   String.IsNullOrEmpty(name)
   ```

   :::image type="content" source="media/debugging-with-visual-studio-code/conditional-expression.png" alt-text="Wprowadź wyrażenie warunkowe":::

   Za każdym razem, gdy punkt przerwania został trafiony, debuger wywołuje `String.IsNullOrEmpty(name)` metodę i przerywa w tym wierszu tylko wtedy, gdy wywołanie metody zwróci wartość `true` .

   Zamiast wyrażenia warunkowego można określić *liczbę trafień*, która przerywa wykonywanie programu, zanim instrukcja zostanie wykonana określoną liczbę razy. Innym rozwiązaniem jest określenie *warunku filtru*, który przerywa wykonywanie programu w oparciu o takie atrybuty jak identyfikator wątku, nazwa procesu lub nazwa wątku.

1. Uruchom program z debugowaniem, naciskając klawisz <kbd>F5</kbd>.

1. Na karcie **Terminal** naciśnij klawisz <kbd>Enter</kbd> po wyświetleniu monitu, aby wprowadzić swoją nazwę.

   Ponieważ określony warunek ( `name` is `null` lub <xref:System.String.Empty?displayProperty=nameWithType> ) został spełniony, wykonanie programu zatrzyma się po osiągnięciu punktu przerwania i przed wykonaniem `Console.WriteLine` metody.

   Okno **zmienne** pokazuje, że wartość `name` zmiennej to `""` , lub <xref:System.String.Empty?displayProperty=nameWithType> .

1. Potwierdź, że wartość jest pustym ciągiem, wprowadzając poniższą instrukcję w wierszu **konsoli debugowania** i naciskając klawisz <kbd>Enter</kbd>. Wynik to `true` .

   ```csharp
   name == String.Empty
   ```

   :::image type="content" source="media/debugging-with-visual-studio-code/expression-in-debug-console.png" alt-text="Konsola debugowania zwracająca wartość true po wykonaniu instrukcji":::

1. Wybierz przycisk **Kontynuuj** na pasku narzędzi, aby kontynuować wykonywanie programu.

1. Wybierz kartę **Terminal** i naciśnij dowolny klawisz, aby wyjść z programu i zatrzymać debugowanie.

1. Wyczyść punkt przerwania, klikając kropkę na lewym marginesie okna kod. Innymi sposobami czyszczenia punktu przerwania są naciśnięcie klawisza <kbd>F9</kbd> lub wybranie polecenia **Uruchom > Przełącz punkt przerwania** z menu podczas wybierania wiersza kodu.

1. Jeśli zostanie wyświetlone ostrzeżenie, że warunek punktu przerwania zostanie utracony, wybierz pozycję **Usuń punkt przerwania**.

## <a name="step-through-a-program"></a>Przechodzenie przez program

Visual Studio Code umożliwia również krok po kroku w wierszu przez program i monitorowanie jego wykonania. Zwykle ustawiasz punkt przerwania i obserwuj przepływ programu za pomocą niewielkiej części kodu programu. Ponieważ ten program jest mały, możesz przejść przez cały program.

1. Ustaw punkt przerwania w otwierającym nawiasie klamrowym `Main` metody.

1. Naciśnij klawisz <kbd>F5</kbd>, aby uruchomić debugowanie.

   Visual Studio Code podświetla linię punktu przerwania.

   W tym momencie okno **zmienne** pokazuje, że `args` Tablica jest pusta i `name` i `date` ma wartości domyślne.

1. Wybierz pozycję **Uruchom**  >  **krok do** lub naciśnij klawisz <kbd>F11</kbd>.

   :::image type="content" source="media/debugging-with-visual-studio-code/step-into.png" alt-text="Przycisk &quot;krok po kroku&quot;":::

   Visual Studio Code podświetla następny wiersz.

1. Wybierz pozycję **Uruchom**  >  **krok do** lub naciśnij klawisz <kbd>F11</kbd>.

   Visual Studio Code wykonuje `Console.WriteLine` monit o podanie nazwy i wyróżnia następny wiersz wykonania. Następnym wierszem jest `Console.ReadLine` `name` . Okno **zmiennych** jest niezmienione, a na karcie **terminala** zostanie wyświetlona wartość "co to jest Twoja nazwa?" pytać.

1. Wybierz pozycję **Uruchom**  >  **krok do** lub naciśnij klawisz <kbd>F11</kbd>.

   Program Visual Studio podświetla `name` przypisanie zmiennej. Okno **zmienne** pokazuje, że `name` jest nadal `null` .

1. Odpowiedz na monit, wprowadzając ciąg na karcie Terminal i naciskając klawisz <kbd>Enter</kbd>.

   Na karcie **terminala** może nie być wyświetlany ciąg wprowadzony podczas jego wprowadzania, ale <xref:System.Console.ReadLine%2A?displayProperty=nameWithType> Metoda przechwytuje dane wejściowe.

1. Wybierz pozycję **Uruchom**  >  **krok do** lub naciśnij klawisz <kbd>F11</kbd>.

   Visual Studio Code podświetla `date` przypisanie zmiennej. Okno **zmienne** pokazuje wartość zwracaną przez wywołanie <xref:System.Console.ReadLine%2A?displayProperty=nameWithType> metody. Na karcie **Terminal** zostanie wyświetlony ciąg wprowadzony w wierszu polecenia.

1. Wybierz pozycję **Uruchom**  >  **krok do** lub naciśnij klawisz <kbd>F11</kbd>.

   Okno **zmienne** zawiera wartość `date` zmiennej po przypisaniu z <xref:System.DateTime.Now?displayProperty=nameWithType> właściwości.

1. Wybierz pozycję **Uruchom**  >  **krok do** lub naciśnij klawisz <kbd>F11</kbd>.

   Visual Studio Code wywołuje <xref:System.Console.WriteLine(System.String,System.Object,System.Object)?displayProperty=nameWithType> metodę. W oknie konsoli zostanie wyświetlony sformatowany ciąg.

1. Wybierz pozycję **Uruchom**  >  **Wyjdź** lub naciśnij klawisz <kbd>SHIFT</kbd> + <kbd>F11</kbd>.

   :::image type="content" source="media/debugging-with-visual-studio-code/step-out.png" alt-text="Przycisk krok po kroku":::

1. Wybierz kartę **Terminal** .

   W terminalu zostanie wyświetlony komunikat "naciśnij dowolny klawisz, aby wyjść..."

1. Naciśnij dowolny klawisz, aby zakończyć program.

## <a name="use-release-build-configuration"></a>Użyj konfiguracji kompilacji wydania

Po przetestowaniu wersji debugowania aplikacji należy również skompilować i przetestować wersję publikacji. Wersja wydania obejmuje optymalizacje kompilatora, które mogą mieć wpływ na zachowanie aplikacji. Na przykład optymalizacje kompilatora, które mają na celu poprawę wydajności, mogą tworzyć sytuacje wyścigu w aplikacjach wielowątkowych.

Aby skompilować i przetestować wydaną wersję aplikacji konsolowej, Otwórz **Terminal** i uruchom następujące polecenie:

```dotnetcli
dotnet run --configuration Release
```

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Debugowanie w Visual Studio Code](https://code.visualstudio.com/docs/editor/debugging)

## <a name="next-steps"></a>Następne kroki

W tym samouczku użyto narzędzi debugowania Visual Studio Code. W następnym samouczku zostanie opublikowana wersja aplikacji, którą można wdrożyć.

> [!div class="nextstepaction"]
> [Publikowanie aplikacji konsolowej .NET przy użyciu Visual Studio Code](publishing-with-visual-studio-code.md)
