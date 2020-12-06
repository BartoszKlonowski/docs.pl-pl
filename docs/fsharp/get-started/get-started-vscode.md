---
title: Rozpoczynanie pracy z językiem F# w programie Visual Studio Code
description: 'Dowiedz się, jak używać języka F # z Visual Studio Code i pakietem wtyczek Ionide.'
ms.date: 12/23/2018
ms.openlocfilehash: 11fb0d443fb7c2b3f270d45bfeaa91102ba28efd
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96739805"
---
# <a name="get-started-with-f-in-visual-studio-code"></a>Rozpoczynanie pracy z językiem F# w programie Visual Studio Code

Możesz napisać F # w [Visual Studio Code](https://code.visualstudio.com) z [wtyczką Ionide](https://marketplace.visualstudio.com/items?itemName=Ionide.Ionide-fsharp) , aby uzyskać wspaniałe, międzyplatformowe, uproszczone zintegrowane środowisko programistyczne (IDE) z technologią IntelliSense i refaktoryzacji kodu. Odwiedź stronę [Ionide.IO](https://ionide.io) , aby dowiedzieć się więcej na temat wtyczki.

Aby rozpocząć, upewnij się, że [poprawnie zainstalowano wtyczkę F # i Ionide](install-fsharp.md#install-f-with-visual-studio-code).

## <a name="create-your-first-project-with-ionide"></a>Tworzenie pierwszego projektu przy użyciu Ionide

Aby utworzyć nowy projekt F #, Otwórz wiersz polecenia i Utwórz nowy projekt z interfejs wiersza polecenia platformy .NET Core:

```dotnetcli
dotnet new console -lang "F#" -o FirstIonideProject
```

Po jego zakończeniu Zmień katalog na projekt i otwórz Visual Studio Code:

```console
cd FirstIonideProject
code .
```

Po załadowaniu projektu na Visual Studio Code powinien zostać wyświetlony okienko Eksplorator rozwiązań F # po lewej stronie otwartego okna. Oznacza to, że Ionide pomyślnie załadował projekt, który został właśnie utworzony. Możesz napisać kod w edytorze przed tym punktem w czasie, ale gdy tak się stanie, wszystko zakończyło ładowanie.

## <a name="configure-f-interactive"></a>Konfiguruj język F # Interactive

Najpierw upewnij się, że obsługa skryptów .NET Core jest domyślnym środowiskiem tworzenia skryptów:

1. Otwórz ustawienia Visual Studio Code (**Code**  >  **Preferences**  >  **Ustawienia** preferencji kodu).
1. Wyszukaj termin " **skrypt F #**".
1. Kliknij pole wyboru, które mówi **FSharp: Użyj skryptów zestawu SDK**.

Jest to obecnie konieczne z powodu niektórych starszych zachowań w skryptach opartych na .NET Framework, które nie współpracują z obsługą skryptów .NET Core, a Ionide jest obecnie striving w celu zapewnienia zgodności z poprzednimi wersjami. W przyszłości skrypty środowiska .NET Core staną się domyślne.

### <a name="write-your-first-script"></a>Napisz swój pierwszy skrypt

Po skonfigurowaniu Visual Studio Code do korzystania ze skryptów .NET Core przejdź do widoku Eksplorator w Visual Studio Code i Utwórz nowy plik. Nadaj mu nazwę *MyFirstScript. FSX*.

Teraz Dodaj do niego następujący kod:

[!code-fsharp[ToPigLatin](~/samples/snippets/fsharp/getting-started/to-pig-latin.fsx)]

Ta funkcja konwertuje wyraz na formę [surówki](https://en.wikipedia.org/wiki/Pig_Latin). Następnym krokiem jest oszacowanie go przy użyciu F# Interactive (FSI).

Zaznacz całą funkcję (powinna być 11 wierszy). Gdy zostanie on wyróżniony, przytrzymaj wciśnięty klawisz **Alt** i naciśnij klawisz **Enter**. Zobaczysz okno terminalu w dolnej części ekranu i będzie wyglądać podobnie do tego:

![Przykład danych wyjściowych F# Interactive z Ionide](./media/getting-started-vscode/vscode-fsi.png)

Było to trzy rzeczy:

1. Uruchomiono proces FSI.
2. Wysłano kod wyróżniony w procesie FSI.
3. Proces FSI ocenia kod, który został wysłany.

Ponieważ wysłane przez Ciebie elementy były [funkcją](../language-reference/functions/index.md), można teraz wywołać tę funkcję za pomocą FSI! W oknie interaktywnym wpisz następujące polecenie:

```fsharp
toPigLatin "banana";;
```

Powinien zostać wyświetlony następujący wynik:

```fsharp
val it : string = "ananabay"
```

Teraz Wypróbujmy samogłosy jako pierwszą literę. Wprowadź następujące dane:

```fsharp
toPigLatin "apple";;
```

Powinien zostać wyświetlony następujący wynik:

```fsharp
val it : string = "appleyay"
```

Funkcja wydaje się działać zgodnie z oczekiwaniami. Gratulacje, po prostu Zapisano pierwszą funkcję F # w Visual Studio Code i oceniamy ją za pomocą FSI!

> [!NOTE]
> Jak zauważono, wiersze w FSI są kończone z `;;` . Dzieje się tak, ponieważ FSI umożliwia wprowadzanie wielu wierszy. Na `;;` końcu FSI wie, kiedy kod został ukończony.

## <a name="explaining-the-code"></a>Objaśnienie kodu

Jeśli nie masz pewności, co robi kod w rzeczywistości, wykonaj instrukcje krok po kroku.

Jak widać, `toPigLatin` to funkcja, która pobiera słowo jako dane wejściowe i konwertuje ją na Pig-Latin reprezentację tego wyrazu. Te reguły są następujące:

Jeśli pierwszy znak w wyrazie zaczyna się od samogłosek, Dodaj "Yay" do końca wyrazu. Jeśli nie zaczyna się od samogłosek, Przenieś ten pierwszy znak na koniec wyrazu i Dodaj do niego wartość "AY".

W FSI mogły być zauważone następujące elementy:

```fsharp
val toPigLatin : word:string -> string
```

To Stany, które `toPigLatin` są funkcją, która przyjmuje `string` jako dane wejściowe (nazywane `word` ) i zwraca inną `string` . Jest to tzw. [sygnatura typu funkcji](https://fsharpforfunandprofit.com/posts/function-signatures/), czyli podstawowa część języka f # służąca do poznania kodu f #. Zauważmy również, że po umieszczeniu wskaźnika myszy nad funkcją w Visual Studio Code.

W treści funkcji widoczne są dwie odrębne części:

1. Wewnętrzna funkcja, wywołana `isVowel` , która określa, czy dany znak ( `c` ) jest wygłosami przez sprawdzenie, czy pasuje do jednego z dostarczonych wzorców przez [dopasowanie wzorca](../language-reference/pattern-matching.md):

   [!code-fsharp[ToPigLatin](~/samples/snippets/fsharp/getting-started/to-pig-latin.fsx#L2-L6)]

2. [`if..then..else`](../language-reference/conditional-expressions-if-then-else.md)Wyrażenie, które sprawdza, czy pierwszy znak jest samogłosek i konstruuje zwracaną wartość z znaków wejściowych w oparciu o to, czy pierwszy znak był samogłosek lub nie:

   [!code-fsharp[ToPigLatin](~/samples/snippets/fsharp/getting-started/to-pig-latin.fsx#L8-L11)]

Przepływ `toPigLatin` jest następujący:

Sprawdź, czy pierwszy znak wyrazu wejściowego to samogłoski. Jeśli tak, Dołącz "Yay" do końca wyrazu. W przeciwnym razie Przenieś ten pierwszy znak na koniec wyrazu i Dodaj do niego wartość "AY".

Należy zwrócić uwagę na następujące informacje: w języku F # nie ma żadnej bezpośredniej instrukcji zwracanej przez funkcję. Wynika to z faktu, że język F # jest oparty na wyrażeniach, a ostatnie wyrażenie obliczane w treści funkcji określa wartość zwracaną przez tę funkcję. Ponieważ `if..then..else` jest samo wyrażeniem, obliczanie treści `then` bloku lub treści `else` bloku określa wartość zwracaną przez `toPigLatin` funkcję.

## <a name="turn-the-console-app-into-a-pig-latin-generator"></a>Przekształcanie aplikacji konsolowej w generator łaciński

W poprzednich sekcjach tego artykułu przedstawiono typowy pierwszy krok pisania kodu F #: pisząc funkcję początkową i wykonując ją interaktywnie przy użyciu FSI. Jest to nazywane programowaniem opartym na REPL, gdzie [REPL](https://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop) to "Read-Szacuj-Print pętl". Jest to doskonały sposób na eksperymentowanie z funkcjami do momentu, w którym będzie działać.

Następnym krokiem w programowaniu opartym na REPL polega na przeniesieniu kodu roboczego do pliku implementacji języka F #. Może zostać następnie skompilowany przez kompilator F # do zestawu, który może być wykonywany.

Aby rozpocząć, Otwórz plik *program. FS* , który został utworzony wcześniej przy użyciu interfejs wiersza polecenia platformy .NET Core. Zauważysz, że jakiś kod już istnieje.

Następnie utwórz nową [`module`](../language-reference/modules.md) nazwę `PigLatin` i skopiuj `toPigLatin` wcześniej utworzoną funkcję w taki sposób, aby:

[!code-fsharp[ToPigLatin](~/samples/snippets/fsharp/getting-started/pig-latin.fs#L3-L14)]

Ten moduł powinien znajdować się powyżej `main` funkcji i poniżej `open System` deklaracji. Porządek deklaracji w języku F #, dlatego należy zdefiniować funkcję przed wywołaniem jej w pliku.

Teraz w `main` funkcji należy wywołać funkcję generatora w postaci trzody chlewnej na argumentach:

```fsharp
[<EntryPoint>]
let main argv =
    for name in argv do
        let newName = PigLatin.toPigLatin name
        printfn %"{name} in Pig Latin is: {newName}"

    0
```

Teraz możesz uruchomić aplikację konsolową z poziomu wiersza polecenia:

```dotnetcli
dotnet run apple banana
```

Zobaczysz, że ten sam wynik będzie taki sam jak plik skryptu, ale ten czas jest uruchomionym programem.

## <a name="troubleshooting-ionide"></a>Rozwiązywanie problemów z Ionide

Poniżej przedstawiono kilka sposobów rozwiązywania niektórych problemów, które mogą być wykonywane w programie:

1. Aby uzyskać funkcje edytowania kodu Ionide, pliki języka F # muszą być zapisane na dysku i wewnątrz folderu, który jest otwarty w obszarze roboczym Visual Studio Code.
1. Jeśli wprowadzono zmiany w systemie lub zainstalowano wymagania wstępne Ionide z Visual Studio Code Otwórz, uruchom ponownie Visual Studio Code.
1. Jeśli w katalogach projektu znajdują się nieprawidłowe znaki, Ionide może nie zadziałał.  W takim przypadku Zmień nazwy katalogów projektu.
1. Jeśli żaden z poleceń Ionide nie działa, sprawdź [powiązania klucza Visual Studio Code](https://code.visualstudio.com/docs/getstarted/keybindings#_advanced-customization) , aby sprawdzić, czy są one zastępowane.
1. Jeśli Ionide jest przerwany na komputerze, a żaden z powyższych elementów nie rozwiązał problemu, spróbuj usunąć `ionide-fsharp` katalog na maszynie i ponownie zainstalować pakiet wtyczek.
1. Jeśli załadowanie projektu nie powiodło się (zostanie wyświetlony Eksplorator rozwiązań F #), kliknij prawym przyciskiem myszy projekt i kliknij pozycję **Wyświetl szczegóły** , aby uzyskać więcej informacji diagnostycznych.

Ionide to projekt typu "open source" skompilowany i obsługiwany przez członków społeczności języka F #. Zgłoś problemy i śmiało, aby współtworzyć w [repozytorium GitHub ionide-programu vscode-FSharp](https://github.com/ionide/ionide-vscode-fsharp).

Możesz również poszukać dalszej pomocy od deweloperów Ionide i społeczności języka F # w [kanale warunkom Ionide](https://gitter.im/ionide/ionide-project).

## <a name="next-steps"></a>Następne kroki

Aby dowiedzieć się więcej o języku F # i funkcjach języka, zapoznaj się [z samouczkiem języka f #](../tour.md).
