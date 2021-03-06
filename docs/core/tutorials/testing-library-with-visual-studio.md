---
title: Testowanie biblioteki klas .NET przy użyciu programu Visual Studio
description: Dowiedz się, jak utworzyć i uruchomić projekt testu jednostkowego dla biblioteki klas .NET przy użyciu programu Visual Studio.
ms.date: 11/18/2020
dev_langs:
- csharp
- vb
ms.custom: vs-dotnet
ms.openlocfilehash: 3d56627b937fa0ad5f8002f396ce617e09ce9d2c
ms.sourcegitcommit: 5114e7847e0ff8ddb8c266802d47af78567949cf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/19/2020
ms.locfileid: "94916129"
---
# <a name="tutorial-test-a-net-class-library-with-net-using-visual-studio"></a>Samouczek: testowanie biblioteki klas .NET w programie .NET przy użyciu programu Visual Studio

W tym samouczku pokazano, jak zautomatyzować testy jednostkowe przez dodanie projektu testowego do rozwiązania.

## <a name="prerequisites"></a>Wymagania wstępne

- Ten samouczek współdziała z rozwiązaniem tworzonym w temacie [Tworzenie biblioteki klas platformy .NET przy użyciu programu Visual Studio](library-with-visual-studio.md).

## <a name="create-a-unit-test-project"></a>Tworzenie projektu testu jednostkowego

Testy jednostkowe zapewniają zautomatyzowane testowanie oprogramowania podczas opracowywania i publikowania. [MSTest](https://github.com/Microsoft/testfx-docs) jest jednym z trzech platform testowych, spośród których można dokonać wyboru. Inne to [xUnit](https://xunit.net/) i [nunit](https://nunit.org/).

1. Uruchom program Visual Studio.

1. Otwórz `ClassLibraryProjects` rozwiązanie utworzone w temacie [Tworzenie biblioteki klas .NET przy użyciu programu Visual Studio](library-with-visual-studio.md).

1. Dodaj nowy projekt testu jednostkowego o nazwie "StringLibraryTest" do rozwiązania.

   1. Kliknij prawym przyciskiem myszy rozwiązanie w **Eksplorator rozwiązań** i wybierz polecenie **Dodaj**  >  **Nowy projekt**.

   1. Na stronie **Dodawanie nowego projektu** wprowadź **MSTest** w polu wyszukiwania. Wybierz pozycję **C#** lub **Visual Basic** z listy język, a następnie wybierz pozycję **wszystkie platformy** z listy platform.

   1. Wybierz szablon **projektu test jednostkowy** , a następnie wybierz przycisk **dalej**.

   1. Na stronie **Konfiguruj nowy projekt** wprowadź **StringLibraryTest** w polu **Nazwa projektu** . Następnie wybierz przycisk **dalej**.

   1. Na stronie **Informacje dodatkowe** wybierz pozycję **.NET 5,0 (Current)** w polu **platforma docelowa** . Następnie wybierz pozycję **Utwórz**.

1. Program Visual Studio tworzy projekt i otwiera plik klasy w oknie kodu przy użyciu następującego kodu. Jeśli język, którego chcesz użyć, nie jest wyświetlany, Zmień selektor języka w górnej części strony.

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

   ```vb
   Imports Microsoft.VisualStudio.TestTools.UnitTesting

   Namespace StringLibraryTest
       <TestClass>
       Public Class UnitTest1
           <TestMethod>
           Sub TestSub()

           End Sub
       End Class
   End Namespace
   ```

   Kod źródłowy utworzony przez szablon testu jednostkowego wykonuje następujące czynności:

   - Importuje <xref:Microsoft.VisualStudio.TestTools.UnitTesting?displayProperty=nameWithType> przestrzeń nazw, która zawiera typy używane do testowania jednostkowego.
   - Stosuje <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestClassAttribute> atrybut do `UnitTest1` klasy.
   - Stosuje <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute> atrybut do definiowania `TestMethod1` w języku C# lub `TestSub` w Visual Basic.

   Każda metoda oznaczona przy użyciu elementu [[TestMethod]](xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute) w klasie testowej oznaczona przy użyciu elementu [[TestClass]](xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestClassAttribute) jest wykonywana automatycznie, gdy test jednostkowy jest uruchamiany.

## <a name="add-a-project-reference"></a>Dodaj odwołanie do projektu

Aby projekt testowy mógł współpracował z `StringLibrary` klasą, Dodaj odwołanie w projekcie **StringLibraryTest** do `StringLibrary` projektu.

1. W **Eksplorator rozwiązań** kliknij prawym przyciskiem myszy węzeł **zależności** projektu **StringLibraryTest** i wybierz polecenie **Dodaj odwołanie do projektu** z menu kontekstowego.

1. W oknie dialogowym **Menedżer odwołań** rozwiń węzeł **projekty** , a następnie zaznacz pole wyboru obok pozycji **StringLibrary**. Dodanie odwołania do `StringLibrary` zestawu umożliwia kompilatorowi znalezienie metod **StringLibrary** podczas kompilowania projektu **StringLibraryTest** .

1. Wybierz przycisk **OK**.

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

1. W oknie kod *UnitTest1.cs* lub *UnitTest1. vb* Zastąp kod następującym kodem:

   :::code language="csharp" source="./snippets/library-with-visual-studio/csharp/StringLibraryTest/UnitTest1.cs":::
   :::code language="vb" source="./snippets/library-with-visual-studio/vb/StringLibraryTest/UnitTest1.vb":::

   Test wielkich liter w `TestStartsWithUpper` metodzie zawiera alfabet grecki (u + 0391) oraz wielką literę pauzy (u + 041C). Test małymi literami w `TestDoesNotStartWithUpper` metodzie obejmuje małą literę alfa (u + 03B1) i małą literę cyrylicy GHE (u + 0433).

1. Na pasku menu wybierz pozycję **plik**  >  **Zapisz UnitTest1.cs jako** lub Zapisz **plik**  >  **UnitTest1. vb jako**. W oknie dialogowym **Zapisz plik jako** wybierz strzałkę obok przycisku **Zapisz** , a następnie wybierz pozycję **Zapisz z kodowaniem**.

   > [!div class="mx-imgBorder"]
   > :::image type="content" source="./media/testing-library-with-visual-studio/save-file-as-dialog.png" alt-text="Okno dialogowe zapisywania pliku w programie Visual Studio":::

1. W oknie dialogowym **Potwierdzanie zapisywania jako** wybierz przycisk **tak** , aby zapisać plik.

1. W oknie dialogowym **Zaawansowane opcje zapisywania** wybierz pozycję **Unicode (UTF-8 z podpisem)-strona kodowa 65001** z listy rozwijanej **kodowanie** i wybierz **przycisk OK**.

   > [!div class="mx-imgBorder"]
   > :::image type="content" source="./media/testing-library-with-visual-studio/advanced-save-options.png" alt-text="Zaawansowane opcje zapisywania programu Visual Studio — okno dialogowe":::

   Jeśli kod źródłowy nie zostanie zapisany jako plik zakodowany w formacie UTF8, program Visual Studio może go zapisać jako plik ASCII. Gdy tak się stanie, środowisko uruchomieniowe nie dekoduje znaków UTF8 poza zakresem ASCII, a wyniki testu nie będą poprawne.

1. Na pasku menu wybierz kolejno opcje **test**  >  **Uruchom wszystkie testy**. Jeśli okno **Eksplorator testów** nie jest otwarte, otwórz je, wybierając **Testuj**  >  **Eksploratora testów**. Trzy testy są wymienione w sekcji **testy zakończone** , a sekcja **podsumowania** raportuje wynik przebiegu testu.

   > [!div class="mx-imgBorder"]
   > :::image type="content" source="./media/testing-library-with-visual-studio/test-explorer-window.png" alt-text="Okno Eksploratora testów z przekazaniem testów":::

## <a name="handle-test-failures"></a>Obsługa niepowodzeń testów

Jeśli wykonujesz programowanie sterowane testami (TDD), najpierw napiszesz testy i nie powiodą się po raz pierwszy. Następnie dodasz kod do aplikacji, która pomyślnie testuje. Na potrzeby tego samouczka utworzono test po zapisaniu kodu aplikacji, który jest weryfikowany, więc niepowodzenie testu nie powiodło się. Aby sprawdzić, czy test zakończy się niepowodzeniem, gdy spodziewasz się niepowodzeniem, Dodaj nieprawidłową wartość do danych wejściowych testu.

1. Zmodyfikuj `words` tablicę w `TestDoesNotStartWithUpper` metodzie, aby uwzględnić ciąg "Error". Nie musisz zapisywać pliku, ponieważ program Visual Studio automatycznie zapisuje otwarte pliki w przypadku skompilowania rozwiązania do uruchamiania testów.

   ```csharp
   string[] words = { "alphabet", "Error", "zebra", "abc", "αυτοκινητοβιομηχανία", "государство",
                      "1234", ".", ";", " " };
   ```

   ```vb
   Dim words() As String = { "alphabet", "Error", "zebra", "abc", "αυτοκινητοβιομηχανία", "государство",
                      "1234", ".", ";", " " }

   ```

1. Uruchom test, wybierając pozycję **test**  >  **Uruchom wszystkie testy** z paska menu. Okno **Eksplorator testów** wskazuje, że dwa testy zostały wykonane pomyślnie i jeden z nich zakończył się niepowodzeniem.

   > [!div class="mx-imgBorder"]
   > :::image type="content" source="./media/testing-library-with-visual-studio/failed-test-window.png" alt-text="Okno Eksploratora testów z niepowodzeniem testami":::

1. Wybierz test zakończony niepowodzeniem `TestDoesNotStartWith` .

   W oknie **Eksplorator testów** zostanie wyświetlony komunikat utworzony przez potwierdzenie: "Assert. IsFalse nie powiodło się. Oczekiwano dla elementu "Error": false; rzeczywista: true ". Z powodu błędu nie przetestowano ciągów w tablicy po "błędzie".

   > [!div class="mx-imgBorder"]
   > :::image type="content" source="./media/testing-library-with-visual-studio/failed-test-detail.png" alt-text="Okno Eksploratora testów przedstawiające błąd potwierdzenia IsFalse":::

1. Usuń ciąg "Error", który został dodany w kroku 1. Uruchom ponownie test i testy zakończone powodzeniem.

## <a name="test-the-release-version-of-the-library"></a>Testowanie wersji wydania biblioteki

Teraz, gdy testy zostały zakończone przed uruchomieniem kompilacji biblioteki, należy uruchomić testy w dodatkowym czasie względem kompilacji wydania biblioteki. Wiele czynników, w tym Optymalizacja kompilatora, może czasami generować różne zachowanie między kompilacjami w wersji Debug i Release.

Aby przetestować kompilację wydania:

1. Na pasku narzędzi programu Visual Studio Zmień konfigurację kompilacji z **Debuguj** do **Release**.

   > [!div class="mx-imgBorder"]
   > :::image type="content" source="./media/testing-library-with-visual-studio/visual-studio-toolbar-release.png" alt-text="Pasek narzędzi programu Visual Studio z wyróżnioną kompilacją wydania":::

1. W **Eksplorator rozwiązań** kliknij prawym przyciskiem myszy projekt **StringLibrary** i wybierz polecenie **Kompiluj** z menu kontekstowego, aby ponownie skompilować bibliotekę.

   > [!div class="mx-imgBorder"]
   > :::image type="content" source="./media/testing-library-with-visual-studio/build-library-context-menu.png" alt-text="Menu kontekstowe StringLibrary z poleceniem Build":::

1. Uruchom testy jednostkowe, wybierając pozycję **test Uruchom**  >  **wszystkie testy** z paska menu. Testy zostały zakończone pomyślnie.

## <a name="debug-tests"></a>Debuguj testy

Jeśli używasz programu Visual Studio jako środowiska IDE, możesz użyć tego samego procesu, który został przedstawiony w [samouczku: debugowanie aplikacji konsolowej .NET za pomocą programu Visual Studio](debugging-with-visual-studio.md) do debugowania kodu przy użyciu projektu testów jednostkowych. Zamiast rozpoczynać projekt aplikacji *Prezentacja* , kliknij prawym przyciskiem myszy projekt **StringLibraryTests** , a następnie wybierz polecenie **Debuguj testy** z menu kontekstowego.

Program Visual Studio uruchamia projekt testowy z dołączonym debugerem. Wykonanie zostanie zatrzymane na dowolnym punkcie przerwania, który został dodany do projektu testowego lub kodu biblioteki źródłowej.

## <a name="additional-resources"></a>Zasoby dodatkowe

* [Podstawowe informacje o teście jednostkowym — Visual Studio](/visualstudio/test/unit-test-basics)
* [Testy jednostkowe w programie .NET](../testing/index.md)

## <a name="next-steps"></a>Następne kroki

W tym samouczku przetestowano bibliotekę klas. Bibliotekę można udostępniać innym osobom, publikując ją w pakiecie [NuGet](https://nuget.org) jako pakiet. Aby dowiedzieć się, jak, postępuj zgodnie z samouczkiem NuGet:

> [!div class="nextstepaction"]
> [Tworzenie i publikowanie pakietu NuGet przy użyciu programu Visual Studio](/nuget/quickstart/create-and-publish-a-package-using-visual-studio?tabs=netcore-cli)

W przypadku opublikowania biblioteki jako pakietu NuGet inne osoby mogą ją zainstalować i używać. Aby dowiedzieć się, jak, postępuj zgodnie z samouczkiem NuGet:

> [!div class="nextstepaction"]
> [Instalowanie i używanie pakietu w programie Visual Studio](/nuget/quickstart/install-and-use-a-package-in-visual-studio)

Biblioteka nie musi być dystrybuowana jako pakiet. Można go powiązać z aplikacją konsolową, która go używa. Aby dowiedzieć się, jak opublikować aplikację konsolową, zobacz wcześniejszy samouczek w tej serii:

> [!div class="nextstepaction"]
> [Publikowanie aplikacji konsolowej .NET przy użyciu programu Visual Studio](publishing-with-visual-studio.md)
