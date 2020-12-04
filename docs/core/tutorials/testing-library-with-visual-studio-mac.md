---
title: Testowanie biblioteki klas .NET przy użyciu Visual Studio dla komputerów Mac
description: Utwórz projekt testu jednostkowego dla biblioteki klas .NET. Sprawdź, czy biblioteka klas .NET działa prawidłowo z testami jednostkowymi.
ms.date: 11/18/2020
ms.openlocfilehash: 02d5aa74258ec15c5447b23246a3c7e9c61a6760
ms.sourcegitcommit: 9d525bb8109216ca1dc9e39c149d4902f4b43da5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2020
ms.locfileid: "96599529"
---
# <a name="test-a-net-class-library-using-visual-studio"></a>Testowanie biblioteki klas .NET przy użyciu programu Visual Studio

W tym samouczku pokazano, jak zautomatyzować testy jednostkowe przez dodanie projektu testowego do rozwiązania.

## <a name="prerequisites"></a>Wymagania wstępne

- Ten samouczek współdziała z rozwiązaniem tworzonym w temacie [Tworzenie biblioteki klas platformy .NET przy użyciu Visual Studio dla komputerów Mac](library-with-visual-studio-mac.md).

## <a name="create-a-unit-test-project"></a>Tworzenie projektu testów jednostkowych

Testy jednostkowe zapewniają zautomatyzowane testowanie oprogramowania podczas opracowywania i publikowania. [MSTest](https://github.com/Microsoft/testfx-docs) jest jednym z trzech platform testowych, spośród których można dokonać wyboru. Inne to [xUnit](https://xunit.net/) i [nunit](https://nunit.org/).

1. Rozpocznij Visual Studio dla komputerów Mac.

1. Otwórz `ClassLibraryProjects` rozwiązanie utworzone w temacie [Tworzenie biblioteki klas .NET przy użyciu Visual Studio dla komputerów Mac](library-with-visual-studio-mac.md).

1. W konsoli **rozwiązania** <kbd>naciśnij klawisz Ctrl</kbd> `ClassLibraryProjects` i kliknij rozwiązanie, a następnie wybierz pozycję **Dodaj**  >  **Nowy projekt**.

1. W oknie dialogowym **Nowy projekt** wybierz pozycję **testy** z węzła **Sieć Web i konsola** . Wybierz **projekt MSTest** , a następnie kliknij przycisk **dalej**.

   :::image type="content" source="media/testing-library-with-visual-studio-mac/visual-studio-mac-unit-test-project.png" alt-text="Tworzenie projektu testowego w oknie dialogowym programu Visual Studio Mac New Project":::

1. Wybierz **platformę .net 5,0** jako **platformę docelową** , a następnie wybierz pozycję **dalej**.

1. Nadaj nowemu projektowi nazwę "StringLibraryTest" i wybierz pozycję **Utwórz**.

   :::image type="content" source="media/testing-library-with-visual-studio-mac/visual-studio-mac-new-project-name.png" alt-text="Okno dialogowe nowego projektu programu Visual Studio dla komputerów Mac z nazwą projektu":::

   Program Visual Studio tworzy plik klasy z następującym kodem:

   ```csharp
   using Microsoft.VisualStudio.TestTools.UnitTesting;

   namespace StringLibraryTest
   {
       [TestClass]
       public class UnitTest1
       {
           [TestMethod]
           public void TestMethod1()
           {
           }
       }
   }
   ```

   Kod źródłowy utworzony przez szablon testu jednostkowego wykonuje następujące czynności:

   - Importuje <xref:Microsoft.VisualStudio.TestTools.UnitTesting?displayProperty=nameWithType> przestrzeń nazw, która zawiera typy używane do testowania jednostkowego.
   - Stosuje <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestClassAttribute> atrybut do `UnitTest1` klasy.
   - Stosuje <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute> atrybut do `TestMethod1` .

   Każda metoda oznaczona przy użyciu elementu [[TestMethod]](xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute) w klasie testowej oznaczona przy użyciu elementu [[TestClass]](xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestClassAttribute) jest wykonywana automatycznie, gdy test jednostkowy jest uruchamiany.

## <a name="add-a-project-reference"></a>Dodaj odwołanie do projektu

Aby projekt testowy mógł współpracował z `StringLibrary` klasą, Dodaj odwołanie do `StringLibrary` projektu.

1. W konsoli **rozwiązania** <kbd>kliknij pozycję</kbd> **zależności** w obszarze **StringLibraryTest**. Wybierz pozycję **Dodaj odwołanie** z menu kontekstowego.

1. W oknie dialogowym **odwołania** wybierz projekt **StringLibrary** . Wybierz przycisk **OK**.

      :::image type="content" source="media/testing-library-with-visual-studio-mac/visual-studio-mac-edit-references.png" alt-text="Okno dialogowe edycji odwołań dla programu Visual Studio Mac":::

## <a name="add-and-run-unit-test-methods"></a>Dodawanie i uruchamianie metod testów jednostkowych

Gdy program Visual Studio uruchamia test jednostkowy, wykonuje każdą metodę, która jest oznaczona <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute> atrybutem w klasie, która jest oznaczona  <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestClassAttribute> atrybutem. Metoda testowa kończy się po znalezieniu pierwszego błędu lub gdy wszystkie testy zawarte w metodzie zakończyły się powodzeniem.

Najczęstsze testy wywołują elementy członkowskie <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert> klasy. Wiele metod Assert obejmuje co najmniej dwa parametry, z których jeden jest oczekiwany wynik testu, a drugi jest rzeczywistym wynikiem testu. `Assert`W poniższej tabeli przedstawiono niektóre z najczęściej wywoływanych metod:

| Metody Assert     | Funkcja |
| ------------------ | -------- |
| `Assert.AreEqual`  | Sprawdza, czy dwie wartości lub obiekty są równe. Potwierdzenie kończy się niepowodzeniem, jeśli wartości lub obiekty nie są równe. |
| `Assert.AreSame`   | Sprawdza, czy dwie zmienne obiektów odwołują się do tego samego obiektu. Potwierdzenie kończy się niepowodzeniem, jeśli zmienne odwołują się do różnych obiektów. |
| `Assert.IsFalse`   | Sprawdza, czy warunek to `false` . Potwierdzenie kończy się niepowodzeniem, jeśli warunek ma wartość `true` . |
| `Assert.IsNotNull` | Sprawdza, czy obiekt nie jest `null` . Potwierdzenie kończy się niepowodzeniem, jeśli obiekt jest `null` . |

Można również użyć <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.ThrowsException%2A?displayProperty=nameWithType> metody w metodzie testowej, aby wskazać typ wyjątku, który ma zostać zgłoszony. Test zakończy się niepowodzeniem, jeśli określony wyjątek nie zostanie zgłoszony.

W testowaniu `StringLibrary.StartsWithUpper` metody, należy podać kilka ciągów zaczynających się od wielkiej litery. Oczekiwano, że metoda zwraca `true` w tych przypadkach, więc można wywołać <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.IsTrue%2A?displayProperty=nameWithType> metodę. Podobnie, chcesz podać kilka ciągów, które zaczynają się od znaku innego niż wielkie litery. Oczekiwano, że metoda zwraca `false` w tych przypadkach, więc można wywołać <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.IsFalse%2A?displayProperty=nameWithType> metodę.

Ponieważ metoda biblioteki obsługuje ciągi, należy również upewnić się, że pomyślnie obsługuje [pusty ciąg ( `String.Empty` )](xref:System.String.Empty), prawidłowy ciąg, który nie zawiera znaków i <xref:System.String.Length> ma wartość 0, i `null` ciąg, który nie został zainicjowany. Można wywołać `StartsWithUpper` bezpośrednio jako metodę statyczną i przekazać pojedynczy <xref:System.String> argument. Lub można wywołać `StartsWithUpper` jako metodę rozszerzającą dla `string` zmiennej przypisanej do `null` .

Zdefiniujesz trzy metody, z których każda wywołuje <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert> metodę dla każdego elementu w tablicy ciągów. Wywołasz Przeciążenie metody, które pozwala określić komunikat o błędzie, który ma być wyświetlany w przypadku niepowodzenia testu. Komunikat identyfikuje ciąg, który spowodował awarię.

Aby utworzyć metody testowe:

1. Otwórz plik *UnitTest1.cs* i Zastąp kod następującym kodem:

   :::code language="csharp" source="./snippets/library-with-visual-studio/csharp/StringLibraryTest/UnitTest1.cs":::

   Test wielkich liter w `TestStartsWithUpper` metodzie zawiera alfabet grecki (u + 0391) oraz wielką literę pauzy (u + 041C). Test małymi literami w `TestDoesNotStartWithUpper` metodzie obejmuje małą literę alfa (u + 03B1) i małą literę cyrylicy GHE (u + 0433).

1. Na pasku menu wybierz pozycję **plik**  >  **Zapisz jako**. W oknie dialogowym upewnij się, że **kodowanie** jest ustawione na **Unicode (UTF-8)**.

   :::image type="content" source="media/testing-library-with-visual-studio-mac/save-file-as-dialog.png" alt-text="Okno dialogowe zapisywania pliku w programie Visual Studio":::

1. Gdy zostanie wyświetlony monit o zamienienie istniejącego pliku, wybierz opcję **Zastąp**.

   Jeśli kod źródłowy nie zostanie zapisany jako plik zakodowany w formacie UTF8, program Visual Studio może go zapisać jako plik ASCII. Gdy tak się stanie, środowisko uruchomieniowe nie dekoduje znaków UTF8 poza zakresem ASCII, a wyniki testu nie będą poprawne.

1. Otwórz panel **testy jednostkowe** po prawej stronie ekranu. Wybierz pozycję **Wyświetl**  >  **testy** z menu.

1. Kliknij ikonę **dokowania** , aby pozostawić otwarty panel.

   :::image type="content" source="media/testing-library-with-visual-studio-mac/visual-studio-mac-unit-test-dock-icon.png" alt-text="Ikona dokowania panelu testy jednostkowe Visual Studio dla komputerów Mac":::

1. Kliknij przycisk **Uruchom wszystko** .

   Wszystkie testy zostały zakończone pomyślnie.

   :::image type="content" source="media/testing-library-with-visual-studio-mac/visual-studio-mac-unit-test-pass.png" alt-text="Visual Studio dla komputerów Mac oczekiwanych przebiegów testowych":::

## <a name="handle-test-failures"></a>Obsługa niepowodzeń testów

Jeśli wykonujesz programowanie sterowane testami (TDD), najpierw napiszesz testy i nie powiodą się po raz pierwszy. Następnie dodasz kod do aplikacji, która pomyślnie testuje. Na potrzeby tego samouczka utworzono test po zapisaniu kodu aplikacji, który jest weryfikowany, więc niepowodzenie testu nie powiodło się. Aby sprawdzić, czy test zakończy się niepowodzeniem, gdy spodziewasz się niepowodzeniem, Dodaj nieprawidłową wartość do danych wejściowych testu.

1. Zmodyfikuj `words` tablicę w `TestDoesNotStartWithUpper` metodzie, aby uwzględnić ciąg "Error". Nie musisz zapisywać pliku, ponieważ program Visual Studio automatycznie zapisuje otwarte pliki w przypadku skompilowania rozwiązania do uruchamiania testów.

   ```csharp
   string[] words = { "alphabet", "Error", "zebra", "abc", "αυτοκινητοβιομηχανία", "государство",
                      "1234", ".", ";", " " };
   ```

1. Uruchom testy ponownie.

   Tym razem okno **Eksplorator testów** wskazuje, że dwa testy powiodło się i jeden z nich zakończył się niepowodzeniem.

   :::image type="content" source="media/testing-library-with-visual-studio-mac/failed-test-window.png" alt-text="Okno Eksploratora testów z niepowodzeniem testami":::

1. <kbd>naciśnij klawisz Ctrl</kbd>i kliknij test zakończony niepowodzeniem, `TestDoesNotStartWithUpper` a następnie wybierz polecenie **Pokaż konsolę wyników** z menu kontekstowego.

   W konsoli **wyników** zostanie wyświetlony komunikat utworzony przez potwierdzenie: "Assert. IsFalse nie powiodło się. Oczekiwano dla elementu "Error": false; rzeczywista: true ". Z powodu błędu nie przetestowano ciągów w tablicy po "błędzie".

   :::image type="content" source="media/testing-library-with-visual-studio-mac/visual-studio-mac-unit-test-failure.png" alt-text="Okno Eksploratora testów przedstawiające błąd potwierdzenia IsFalse":::

1. Usuń ciąg "Error", który został dodany w kroku 1. Uruchom ponownie test i testy zakończone powodzeniem.

## <a name="test-the-release-version-of-the-library"></a>Testowanie wersji wydania biblioteki

Teraz, gdy testy zostały zakończone przed uruchomieniem kompilacji biblioteki, należy uruchomić testy w dodatkowym czasie względem kompilacji wydania biblioteki. Wiele czynników, w tym Optymalizacja kompilatora, może czasami generować różne zachowanie między kompilacjami w wersji Debug i Release.

Aby przetestować kompilację wydania:

1. Na pasku narzędzi programu Visual Studio Zmień konfigurację kompilacji z **Debuguj** do **Release**.

   :::image type="content" source="media/testing-library-with-visual-studio-mac/visual-studio-toolbar-release.png" alt-text="Pasek narzędzi programu Visual Studio z wyróżnioną kompilacją wydania":::

1. W konsoli **rozwiązania** kliknij projekt **StringLibrary** i wybierz polecenie **Kompiluj** z menu kontekstowego <kbd>, aby</kbd>ponownie skompilować bibliotekę.

   :::image type="content" source="media/testing-library-with-visual-studio-mac/build-library-context-menu.png" alt-text="Menu kontekstowe StringLibrary z poleceniem Build":::

1. Uruchom ponownie testy jednostkowe.

   Testy zostały zakończone pomyślnie.

## <a name="debug-tests"></a>Debuguj testy

Jeśli używasz Visual Studio dla komputerów Mac jako środowiska IDE, możesz użyć tego samego procesu, który został przedstawiony w [samouczku: debugowanie aplikacji konsolowej .NET za pomocą Visual Studio dla komputerów Mac](debugging-with-visual-studio-mac.md) do debugowania kodu przy użyciu projektu testów jednostkowych. Zamiast rozpoczynać projekt aplikacji *Pokaz* <kbd>, kliknij</kbd>projekt **StringLibraryTests** i wybierz pozycję **Rozpocznij debugowanie projektu** z menu kontekstowego.

Program Visual Studio uruchamia projekt testowy z dołączonym debugerem. Wykonanie zostanie zatrzymane na dowolnym punkcie przerwania, który został dodany do projektu testowego lub kodu biblioteki źródłowej.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Testy jednostkowe w programie .NET](../testing/index.md)

## <a name="next-steps"></a>Następne kroki

W tym samouczku przetestowano bibliotekę klas. Bibliotekę można udostępniać innym osobom, publikując ją w pakiecie [NuGet](https://nuget.org) jako pakiet. Aby dowiedzieć się, jak, postępuj zgodnie z samouczkiem NuGet:

> [!div class="nextstepaction"]
> [Tworzenie i publikowanie pakietu (wiersz polecenia dotnet)](/nuget/quickstart/create-and-publish-a-package-using-the-dotnet-cli)

W przypadku opublikowania biblioteki jako pakietu NuGet inne osoby mogą ją zainstalować i używać. Aby dowiedzieć się, jak, postępuj zgodnie z samouczkiem NuGet:

> [!div class="nextstepaction"]
> [Instalowanie i używanie pakietu w Visual Studio dla komputerów Mac](/nuget/quickstart/install-and-use-a-package-in-visual-studio-mac)

Biblioteka nie musi być dystrybuowana jako pakiet. Można go powiązać z aplikacją konsolową, która go używa. Aby dowiedzieć się, jak opublikować aplikację konsolową, zobacz wcześniejszy samouczek w tej serii:

> [!div class="nextstepaction"]
> [Publikowanie aplikacji konsolowej .NET przy użyciu Visual Studio dla komputerów Mac](publishing-with-visual-studio-mac.md)
