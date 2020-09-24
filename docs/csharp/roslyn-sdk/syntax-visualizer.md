---
title: Eksplorowanie kodu za pomocą wizualizatora składni Roslyn w programie Visual Studio
description: Wizualizator składni zawiera narzędzie wizualne umożliwiające Eksplorowanie modeli, które zestaw .NET Compiler Platform SDK generuje dla kodu.
ms.date: 03/07/2018
ms.custom: mvc, vs-dotnet
ms.openlocfilehash: a911a99e78ad5a5f4c6771b91a3c541b1812d67c
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91167577"
---
# <a name="explore-code-with-the-roslyn-syntax-visualizer-in-visual-studio"></a>Eksplorowanie kodu za pomocą wizualizatora składni Roslyn w programie Visual Studio

Ten artykuł zawiera omówienie narzędzia Syntax Visualizer, które jest dostarczane jako część .NET Compiler Platform ("Roslyn") SDK. Syntax Visualizer jest oknem narzędzi, które ułatwia sprawdzanie i eksplorowanie drzew składni. Jest to podstawowe narzędzie do zrozumienia modeli dla kodu, który ma zostać przeanalizowany. Jest to również pomoc dla debugowania podczas tworzenia własnych aplikacji przy użyciu zestawu SDK .NET Compiler Platform ("Roslyn"). Otwórz to narzędzie podczas tworzenia pierwszych analizatorów. Wizualizator pomaga zrozumieć modele używane przez interfejsy API. Możesz również użyć narzędzi, takich jak [SharpLab](https://sharplab.io) lub [LINQPad](https://www.linqpad.net/) , aby sprawdzić kod i zrozumieć drzewa składniowe.

[!INCLUDE[interactive-note](~/includes/roslyn-installation.md)]

Zapoznaj się z pojęciami użytymi w zestawie SDK .NET Compiler Platform, odczytując artykuł z [omówieniem](compiler-api-model.md) . Zawiera wprowadzenie do drzew składni, węzłów, tokenów i kwizy.

## <a name="syntax-visualizer"></a>Syntax Visualizer

**Syntax Visualizer** umożliwia inspekcję drzewa składni dla pliku kodu C# lub Visual Basic w bieżącym aktywnym oknie edytora w środowisku IDE programu Visual Studio. Wizualizator można uruchomić, klikając pozycję **Wyświetl**  >  **inne okna**  >  **Syntax Visualizer**.  Możesz również użyć paska narzędzi **Szybkie uruchamianie** w prawym górnym rogu. Wpisz "składnia" i polecenie, aby otworzyć **Syntax Visualizer** powinna zostać wyświetlona.

To polecenie otwiera Syntax Visualizer jako okno narzędzi zmiennoprzecinkowych. Jeśli nie masz otwartego okna edytora kodu, ekran jest pusty, jak pokazano na poniższej ilustracji.

![Okno narzędzia Syntax Visualizer](media/syntax-visualizer/syntax-visualizer.png)

Zadokuj to okno narzędzia w wygodnej lokalizacji wewnątrz programu Visual Studio, na przykład po lewej stronie. Wizualizator pokazuje informacje o bieżącym pliku kodu.

Utwórz nowy projekt za pomocą polecenia **plik**  >  **Nowy projekt** . Można utworzyć projekt Visual Basic lub C#. Gdy program Visual Studio otwiera główny plik kodu dla tego projektu, wizualizator Wyświetla drzewo składni. Można otworzyć dowolny istniejący plik C#/Visual Basic w tym wystąpieniu programu Visual Studio, a wizualizator Wyświetla drzewo składni tego pliku. Jeśli masz otwartych wiele plików kodu w programie Visual Studio, wizualizatorer Wyświetla drzewo składni dla aktualnie aktywnego pliku kodu (plik kodu z fokusem klawiatury).

<!-- markdownlint-disable MD025 -->

# <a name="c"></a>[C#](#tab/csharp)

![Wizualizowanie drzewa składni języka C#](media/syntax-visualizer/visualize-csharp.png)

# <a name="visual-basic"></a>[Visual Basic](#tab/vb)

![Wizualizowanie drzewa składni Visual Basic](media/syntax-visualizer/visualize-visual-basic.png)

---

Jak pokazano na powyższym obrazie, okno narzędzia wizualizatora Wyświetla drzewo składni u góry i siatkę właściwości u dołu. Siatka właściwości zawiera właściwości elementu, który jest aktualnie wybrany w drzewie, w tym *Typ* .NET i *rodzaj* (elementem syntaxkind) elementu.

Drzewa składni składają się z trzech typów elementów — *węzłów*, *tokenów*i *kwizy*. Więcej informacji na temat tych typów można znaleźć w artykule dotyczącym [składni](work-with-syntax.md) . Elementy każdego typu są reprezentowane przy użyciu innego koloru. Kliknij przycisk "Legenda", aby zapoznać się z omówieniem użytych kolorów.

Każdy element w drzewie również Wyświetla własny **zakres**. **Zakres** jest indeksem (położenie początkowe i końcowe) tego węzła w pliku tekstowym.  W poprzednim przykładzie w języku C# wybrany token "UsingKeyword [0.. 5)" ma **zakres** o długości pięciu znaków, [0.. 5). Notacja "[...)" oznacza, że indeks początkowy jest częścią zakresu, ale końcowym indeksem nie jest.

Istnieją dwa sposoby nawigowania po drzewie:

* Rozwiń lub kliknij elementy w drzewie. Wizualizator automatycznie zaznaczy tekst odpowiadający zakresowi tego elementu w edytorze kodu.
* Kliknij lub zaznacz tekst w edytorze kodu. W powyższym przykładzie Visual Basic w przypadku wybrania w edytorze kodu wiersza zawierającego "module Module1" wizualizator automatycznie nawiguje do odpowiedniego węzła ModuleStatement w drzewie.

Wizualizator podświetla element w drzewie, którego zakres najlepiej pasuje do zakresu tekstu zaznaczonego w edytorze.

Wizualizator odświeża drzewo, aby dopasować modyfikacje w aktywnym pliku kodu. Dodaj wywołanie do `Console.WriteLine()` wewnątrz `Main()` . Podczas wpisywania, wizualizator odświeża drzewo.

Wstrzymaj wpisywanie po wpisaniu `Console.` . Drzewo ma pewne elementy kolorowe w kolorze różowym. W tym momencie istnieją błędy (nazywane również "diagnostyką") w określonym kodzie. Te błędy są dołączone do węzłów, tokenów i kwizy w drzewie składni. Wizualizator pokazuje, które elementy zawierają błędy dołączone do nich, podkreślając tło w kolorze różowym. Błędy w dowolnym elemencie można sprawdzić kolorem różowym, umieszczając kursor na elemencie. Wizualizator wyświetla tylko błędy składni (te błędy związane ze składnią wpisanego kodu); nie są wyświetlane żadne błędy semantyczne.

## <a name="syntax-graphs"></a>Wykresy składniowe

Kliknij prawym przyciskiem myszy dowolny element w drzewie, a następnie kliknij polecenie **Wyświetl wykres Pokierowanej składni**.

# <a name="c"></a>[C#](#tab/csharp)

Wizualizator Wyświetla graficzną reprezentację poddrzewa osadzonego na wybranym elemencie. Spróbuj wykonać następujące kroki dla węzła **MethodDeclaration** odpowiadającego `Main()` metodzie w przykładzie w języku C#. Wizualizator wyświetla wykres składni, który wygląda następująco:

![Wyświetlanie grafu składni języka C#](media/syntax-visualizer/csharp-syntax-graph.png)

# <a name="visual-basic"></a>[Visual Basic](#tab/vb)

Wypróbuj te same dla węzła **bloku** podrzędnego odpowiadającego `Main()` metodzie w poprzednim przykładzie Visual Basic. Wizualizator wyświetla wykres składni, który wygląda następująco:

![Wyświetlanie wykresu składni Visual Basic](media/syntax-visualizer/visual-basic-syntax-graph.png)

---

Przeglądarka grafu składni zawiera opcję wyświetlania legendy dla schematu kolorowania. Możesz również umieścić wskaźnik myszy nad poszczególnymi elementami na wykresie składni, aby wyświetlić właściwości odpowiadające temu elementowi.

Wykresy składniowe można wyświetlać wielokrotnie dla różnych elementów w drzewie, a wykresy będą zawsze wyświetlane w tym samym oknie w programie Visual Studio. To okno można zadokować w wygodnej lokalizacji wewnątrz programu Visual Studio, aby nie trzeba było przełączać się między kartami, aby wyświetlić nowy wykres składni. Dolna, poniżej okna edytora kodu, jest często wygodna.

Poniżej znajduje się układ dokowania, który ma być używany z oknem narzędzia wizualizatora oraz oknem grafu składni:

![Jeden układ dokowania dla wizualizatora i okna wykresu składniowego](media/syntax-visualizer/docking-layout.png)

Innym rozwiązaniem jest umieszczenie okna wykresu składniowego na drugim monitorze w konfiguracji podwójnego monitora.

## <a name="inspecting-semantics"></a>Sprawdzanie semantyki

Syntax Visualizer umożliwia inspekcję podstawowe symboli i informacji semantycznych. Wpisz `double x = 1 + 1;` wewnątrz Main () w przykładzie w języku C#. Następnie wybierz wyrażenie `1 + 1` w oknie Edytor kodu. Wizualizator podświetla węzeł **AddExpression** w wizualizatorze. Kliknij prawym przyciskiem myszy to polecenie **AddExpression** i kliknij pozycję **Wyświetl symbol (jeśli istnieje)**. Należy zauważyć, że większość elementów menu ma kwalifikator "Jeśli any". Syntax Visualizer sprawdza właściwości węzła, w tym właściwości, które mogą nie być obecne dla wszystkich węzłów.

Siatka właściwości w ramach aktualizacji wizualizatora, jak pokazano na poniższej ilustracji: symbol wyrażenia jest **SynthesizedIntrinsicOperatorSymbol** z **typem = Method**.

![Właściwości symbolu](media/syntax-visualizer/symbol-properties.png)

Spróbuj **wyświetlić TypeSymbol (jeśli istnieje)** dla tego samego węzła **AddExpression** . Siatka właściwości na stronie wizualizatora aktualizuje, jak pokazano na poniższej ilustracji, co oznacza, że typ wybranego wyrażenia to `Int32` .

![Właściwości TypeSymbol](media/syntax-visualizer/type-symbol-properties.png)

Spróbuj **wyświetlić przekonwertowane TypeSymbol (jeśli istnieje)** dla tego samego węzła **AddExpression** . Aktualizacja siatki właściwości wskazująca, że chociaż typ wyrażenia to `Int32` , przekonwertowanego typu wyrażenia jest `Double` tak jak pokazano na poniższym rysunku. Ten węzeł zawiera informacje o symbolach konwersji, ponieważ `Int32` wyrażenie występuje w kontekście, w którym musi zostać przekonwertowane na `Double` . Ta konwersja spełnia `Double` Typ określony dla zmiennej po `x` lewej stronie operatora przypisania.

![Skonwertowane właściwości TypeSymbol](media/syntax-visualizer/converted-type-symbol-properties.png)

Na koniec spróbuj **wyświetlić wartość stałą (jeśli istnieje)** dla tego samego węzła **AddExpression** . Siatka właściwości pokazuje, że wartość wyrażenia jest stałą czasu kompilacji o wartości `2` .

![Stała wartość](media/syntax-visualizer/constant-value.png)

Poprzedni przykład można także zreplikować w Visual Basic. Wpisz `Dim x As Double = 1 + 1` plik w Visual Basic. Wybierz wyrażenie `1 + 1` w oknie Edytor kodu. Wizualizator podświetla odpowiadający jej węzeł **AddExpression** w wizualizatorze. Powtórz powyższe kroki dla tego **AddExpression** i powinny być widoczne identyczne wyniki.

Przejrzyj więcej kodu w Visual Basic. Zaktualizuj główny plik Visual Basic przy użyciu następującego kodu:

```vb
Imports C = System.Console

Module Program
    Sub Main(args As String())
        C.WriteLine()
    End Sub
End Module
```

Ten kod wprowadza alias o nazwie `C` , który jest mapowany na typ `System.Console` w górnej części pliku i używa tego aliasu wewnątrz `Main()` . Wybierz użycie tego aliasu `C` w `C.WriteLine()` , wewnątrz `Main()` metody. Wizualizator wybiera odpowiedni węzeł **identyfikatorname** w wizualizatorze. Kliknij prawym przyciskiem myszy ten węzeł i kliknij pozycję **Wyświetl symbol (jeśli istnieje)**. Siatka właściwości wskazuje, że ten identyfikator jest powiązany z typem `System.Console` , jak pokazano na poniższym rysunku:

![Właściwości symbolu](media/syntax-visualizer/symbol-visual-basic.png)

Spróbuj **wyświetlić AliasSymbol (jeśli istnieje)** dla tego samego węzła **identyfikatoraname** . Siatka właściwości wskazuje, że identyfikator jest alias o nazwie `C` , która jest powiązana z `System.Console` obiektem docelowym. Innymi słowy, Siatka właściwości zawiera informacje dotyczące **AliasSymbol** odpowiadającego identyfikatorowi `C` .

![Właściwości AliasSymbol](media/syntax-visualizer/alias-symbol.png)

Zbadaj Symbol odpowiadający każdemu zadeklarowanemu typowi, metodzie, właściwości. Wybierz odpowiedni węzeł w wizualizatorze i kliknij pozycję **Wyświetl symbol (jeśli istnieje)**. Wybierz metodę `Sub Main()` , łącznie z treścią metody. Kliknij pozycję **Wyświetl symbol (jeśli istnieje)** **dla odpowiedniego węzła** podrzędnego w wizualizatorze. Siatka właściwości pokazuje **MethodSymbol** dla tego **podbloku** ma nazwę `Main` z typem zwracanym `Void` .

![Wyświetlanie symbolu dla deklaracji metody](media/syntax-visualizer/method-symbol.png)

Powyższe Visual Basic przykłady można łatwo zreplikować w języku C#. Wpisz `using C = System.Console;` miejsce `Imports C = System.Console` dla aliasu. Powyższe kroki w języku C# dają takie same wyniki w oknie wizualizatora.

Operacje inspekcji semantycznej są dostępne tylko w węzłach. Nie są one dostępne w tokenach ani kwizy. Nie wszystkie węzły mają interesujące informacje semantyczne do sprawdzenia. Gdy węzeł nie ma interesujących informacji semantycznych, kliknięcie pozycji **Wyświetl \* symbol (jeśli istnieje)** powoduje wyświetlenie pustej siatki właściwości.

Więcej informacji na temat interfejsów API do wykonywania analizy semantycznej można znaleźć w dokumencie przegląd [pracy z semantyką](work-with-semantics.md) .

## <a name="closing-the-syntax-visualizer"></a>Zamykanie wizualizatora składni

Okno wizualizatorer można zamknąć, gdy nie jest używane do badania kodu źródłowego. Wizualizator składni aktualizuje swój ekran podczas poruszania się po kodzie, edytowania i zmieniania źródła. Może to odwrócić, gdy nie jest używany.
