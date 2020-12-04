---
title: Tworzenie biblioteki klas .NET przy użyciu programu Visual Studio
description: Dowiedz się, jak utworzyć bibliotekę klas .NET przy użyciu programu Visual Studio.
ms.date: 08/07/2020
dev_langs:
- csharp
- vb
ms.custom: vs-dotnet,contperfq1
ms.openlocfilehash: 6a3f61525ca86afc9ee71d56cbc9450862760ba4
ms.sourcegitcommit: 9d525bb8109216ca1dc9e39c149d4902f4b43da5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2020
ms.locfileid: "96599515"
---
# <a name="tutorial-create-a-net-class-library-using-visual-studio"></a>Samouczek: Tworzenie biblioteki klas .NET przy użyciu programu Visual Studio

W tym samouczku utworzysz prostą bibliotekę klas, która zawiera pojedynczą metodę obsługi ciągów.

*Biblioteka klas* definiuje typy i metody, które są wywoływane przez aplikację. Jeśli biblioteka jest przeznaczona .NET Standard 2,0, może być wywoływana przez dowolną implementację platformy .NET (w tym .NET Framework), która obsługuje .NET Standard 2,0. Jeśli biblioteka jest przeznaczona dla platformy .NET 5, może być wywoływana przez dowolną aplikację, która jest przeznaczona dla platformy .NET 5. W tym samouczku przedstawiono sposób ukierunkowania platformy .NET 5.

Podczas tworzenia biblioteki klas można ją rozpowszechnić jako pakiet NuGet lub jako składnik powiązany z aplikacją, która go używa.

## <a name="prerequisites"></a>Wymagania wstępne

- [Program Visual Studio 2019 w wersji 16,8 lub nowszej](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) z zainstalowanym **wieloplatformowym obciążeniem programistycznym dla platformy .NET Core** . Zestaw .NET 5,0 SDK jest instalowany automatycznie po wybraniu tego obciążenia. W tym samouczku przyjęto założenie, że **w nowym projekcie zostały włączone wszystkie szablony .NET Core**, jak pokazano w [samouczku: Tworzenie aplikacji konsolowej .NET przy użyciu programu Visual Studio](with-visual-studio.md).

## <a name="create-a-solution"></a>Tworzenie rozwiązania

Zacznij od utworzenia pustego rozwiązania, aby umieścić projekt biblioteki klas w. Rozwiązanie programu Visual Studio służy jako kontener dla jednego lub wielu projektów. Dodasz kolejne powiązane projekty do tego samego rozwiązania.

Aby utworzyć puste rozwiązanie:

1. Uruchom program Visual Studio.

2. W oknie uruchamiania wybierz pozycję **Utwórz nowy projekt**.

3. Na stronie **Tworzenie nowego projektu** wprowadź **rozwiązanie** w polu wyszukiwania. Wybierz szablon **pustego rozwiązania** , a następnie wybierz przycisk **dalej**.

   :::image type="content" source="media/library-with-visual-studio/blank-solution.png" alt-text="Pusty szablon rozwiązania w programie Visual Studio":::

4. Na stronie **Konfiguruj nowy projekt** wprowadź **ClassLibraryProjects** w polu **Nazwa projektu** . Następnie wybierz pozycję **Utwórz**.

## <a name="create-a-class-library-project"></a>Tworzenie projektu biblioteki klas

1. Dodaj nowy projekt biblioteki klas .NET o nazwie "StringLibrary" do rozwiązania.

   1. Kliknij prawym przyciskiem myszy rozwiązanie w **Eksplorator rozwiązań** i wybierz polecenie **Dodaj**  >  **Nowy projekt**.

   1. Na stronie **Dodawanie nowego projektu** wprowadź **bibliotekę** w polu wyszukiwania. Wybierz pozycję **C#** lub **Visual Basic** z listy język, a następnie wybierz pozycję **wszystkie platformy** z listy platform. Wybierz szablon **Biblioteka klas** , a następnie wybierz przycisk **dalej**.

   1. Na stronie **Konfiguruj nowy projekt** wprowadź **StringLibrary** w polu **Nazwa projektu** , a następnie wybierz przycisk **dalej**.

   1. Na stronie **Informacje dodatkowe** wybierz pozycję **.NET 5,0 (bieżąca)**, a następnie wybierz pozycję **Utwórz**.

1. Upewnij się, że biblioteka jest przeznaczona dla odpowiedniej wersji platformy .NET. Kliknij prawym przyciskiem myszy projekt Biblioteka w **Eksplorator rozwiązań**, a następnie wybierz polecenie **Właściwości**. Pole tekstowe **platformy docelowej** pokazuje, że projekt jest przeznaczony dla programu .NET 5,0.

1. Jeśli używasz Visual Basic, wyczyść tekst w polu tekstowym **główna przestrzeń nazw** .

   :::image type="content" source="./media/library-with-visual-studio/vb/library-project-properties.png" alt-text="Właściwości projektu dla biblioteki klas":::

   Dla każdego projektu Visual Basic automatycznie tworzy przestrzeń nazw, która odnosi się do nazwy projektu. W tym samouczku zdefiniujesz przestrzeń nazw najwyższego poziomu za pomocą [`namespace`](../../visual-basic/language-reference/statements/namespace-statement.md) słowa kluczowego w pliku kodu.

1. Zastąp kod w oknie kodu dla *Class1.cs*  lub *Class1. vb* następującym kodem i Zapisz plik. Jeśli język, którego chcesz użyć, nie jest wyświetlany, Zmień selektor języka w górnej części strony.

   :::code language="csharp" source="./snippets/library-with-visual-studio/csharp/StringLibrary/Class1.cs":::
   :::code language="vb" source="./snippets/library-with-visual-studio/vb/StringLibrary/Class1.vb":::

   Biblioteka klas, `UtilityLibraries.StringLibrary` ,,, zawiera metodę o nazwie `StartsWithUpper` . Ta metoda zwraca <xref:System.Boolean> wartość wskazującą, czy bieżące wystąpienie ciągu zaczyna się od wielkiej litery. Standard Unicode rozróżnia wielkie litery od małych liter. <xref:System.Char.IsUpper(System.Char)?displayProperty=nameWithType>Metoda zwraca `true` czy znak jest pisany wielką literą.

   `StartsWithUpper` jest zaimplementowany jako [Metoda rozszerzająca](../../csharp/programming-guide/classes-and-structs/extension-methods.md) , aby można było wywołać ją tak, jakby była elementem członkowskim <xref:System.String> klasy.

1. Na pasku menu wybierz kolejno opcje **Kompiluj** kompilacje  >  **rozwiązanie** lub naciśnij <kbd>klawisze CTRL</kbd> + <kbd>SHIFT</kbd> + <kbd>B</kbd> , aby sprawdzić, czy projekt kompiluje się bez błędu.

## <a name="add-a-console-app-to-the-solution"></a>Dodawanie aplikacji konsolowej do rozwiązania

Dodaj aplikację konsolową, która używa biblioteki klas. Aplikacja wyświetli monit o wprowadzenie ciągu i zgłoszenie, czy ciąg rozpoczyna się od wielkiej litery.

1. Dodaj nową aplikację konsolową .NET o nazwie "pokaz" do rozwiązania.

   1. Kliknij prawym przyciskiem myszy rozwiązanie w **Eksplorator rozwiązań** i wybierz polecenie **Dodaj**  >  **Nowy projekt**.

   1. Na stronie **Dodawanie nowego projektu** wprowadź w polu wyszukiwania **konsolę** . Wybierz pozycję **C#** lub **Visual Basic** z listy język, a następnie wybierz pozycję **wszystkie platformy** z listy platform.

   1. Wybierz szablon **aplikacja konsoli** , a następnie wybierz przycisk **dalej**.

   1. Na stronie **Konfiguruj nowy projekt** wprowadź wartość **Prezentacja** w polu **Nazwa projektu** . Następnie wybierz przycisk **dalej**.

   1. Na stronie **Informacje dodatkowe** wybierz pozycję **.NET 5,0 (Current)** w polu **platforma docelowa** . Następnie wybierz pozycję **Utwórz**.

1. W oknie kodu dla pliku *program.cs* lub *program. vb* Zastąp cały kod następującym kodem.

   :::code language="csharp" source="./snippets/library-with-visual-studio/csharp/ShowCase/Program.cs":::
   :::code language="vb" source="./snippets/library-with-visual-studio/vb/ShowCase/Program.vb":::

   Kod używa `row` zmiennej do obsługi liczby wierszy danych zapisywana w oknie konsoli. Za każdym razem, gdy jest większy lub równy 25, kod czyści okno konsoli i wyświetla komunikat dla użytkownika.

   Program poprosi użytkownika o wprowadzenie ciągu. Wskazuje, czy ciąg rozpoczyna się od wielkiej litery. Jeśli użytkownik naciśnie klawisz <kbd>Enter</kbd> bez wprowadzania ciągu, aplikacja zostanie zakończona, a okno konsoli zostanie zamknięte.

## <a name="add-a-project-reference"></a>Dodaj odwołanie do projektu

Początkowo nowy projekt aplikacji konsolowej nie ma dostępu do biblioteki klas. Aby zezwolić na wywoływanie metod w bibliotece klas, Utwórz odwołanie do projektu do projektu biblioteki klas.

1. W **Eksplorator rozwiązań** kliknij prawym przyciskiem myszy `ShowCase` węzeł **zależności** projektu i wybierz polecenie **Dodaj odwołanie do projektu**.

   :::image type="content" source="media/library-with-visual-studio/add-reference-context-menu.png" alt-text="Dodaj menu kontekstowe odwołania w programie Visual Studio":::

1. W oknie dialogowym **Menedżer odwołań** wybierz projekt **StringLibrary** , a następnie wybierz **przycisk OK**.

   :::image type="content" source="media/library-with-visual-studio/manage-project-references.png" alt-text="Okno dialogowe programu Reference Manager z wybraną pozycją StringLibrary":::

## <a name="run-the-app"></a>Uruchamianie aplikacji

1. W **Eksplorator rozwiązań** kliknij prawym przyciskiem myszy projekt **pokazu** i wybierz polecenie **Ustaw jako projekt startowy** w menu kontekstowym.

   :::image type="content" source="media/library-with-visual-studio/set-startup-project-context-menu.png" alt-text="Menu kontekstowe projektu programu Visual Studio, aby ustawić projekt startowy":::

1. Naciśnij klawisz <kbd>Ctrl</kbd> + <kbd>F5</kbd> , aby skompilować i uruchomić program bez debugowania.

   :::image type="content" source="media/library-with-visual-studio/visual-studio-project-toolbar.png" alt-text="Pasek narzędzi projektu programu Visual Studio z widocznym przyciskiem Debuguj":::

1. Wypróbuj program, wprowadzając ciągi i naciskając klawisz <kbd>Enter</kbd>, a następnie naciśnij klawisz <kbd>Enter</kbd> , aby wyjść.

   :::image type="content" source="media/library-with-visual-studio/run-showcase.png" alt-text="Okno konsoli z uruchomionym pokazem":::

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Tworzenie bibliotek przy użyciu interfejsu wiersza polecenia platformy .NET](libraries.md)
* [Wersje .NET Standard i obsługiwane przez nich platformy](../../standard/net-standard.md).

## <a name="next-steps"></a>Następne kroki

W tym samouczku utworzono bibliotekę klas. W następnym samouczku dowiesz się, jak jednostkowo testować bibliotekę klas.

> [!div class="nextstepaction"]
> [Testowanie jednostkowe biblioteki klas .NET przy użyciu programu Visual Studio](testing-library-with-visual-studio.md)

Możesz też pominąć zautomatyzowane testowanie jednostkowe i dowiedzieć się, jak udostępnić bibliotekę, tworząc pakiet NuGet:

> [!div class="nextstepaction"]
> [Tworzenie i publikowanie pakietu przy użyciu programu Visual Studio](/nuget/quickstart/create-and-publish-a-package-using-visual-studio)

Lub Dowiedz się, jak opublikować aplikację konsolową. Jeśli opublikujesz aplikację konsolową z rozwiązania utworzonego w tym samouczku, Biblioteka klas przejdzie z nim jako plik *. dll* .

> [!div class="nextstepaction"]
> [Publikowanie aplikacji konsolowej .NET przy użyciu programu Visual Studio](publishing-with-visual-studio.md)
