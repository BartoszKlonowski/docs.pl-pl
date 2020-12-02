---
title: 'Wprowadzenie do języka F # w Visual Studio dla komputerów Mac'
description: 'Dowiedz się, jak używać języka F # z Visual Studio dla komputerów Mac.'
ms.date: 07/03/2018
ms.openlocfilehash: d2ad24ad18bb31419b39508f2cf555c82fbe2e0b
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96437994"
---
# <a name="get-started-with-f-in-visual-studio-for-mac"></a>Wprowadzenie do języka F # w Visual Studio dla komputerów Mac

Narzędzia F # i Visual F# są obsługiwane w Visual Studio dla komputerów Mac IDE. Upewnij się, że [zainstalowano Visual Studio dla komputerów Mac](install-fsharp.md#install-f-with-visual-studio-for-mac).

## <a name="creating-a-console-application"></a>Tworzenie aplikacji konsolowej

Jednym z najpopularniejszych projektów w Visual Studio dla komputerów Mac jest Aplikacja konsolowa.  Oto odpowiednie czynności:  Gdy Visual Studio dla komputerów Mac jest otwarty:

1. W menu **plik** wskaż polecenie **nowe rozwiązanie**.

2. W oknie dialogowym Nowy projekt istnieją 2 różne szablony dla aplikacji konsolowej.  Istnieje jedna pod innymi > .NET, która jest przeznaczona dla .NET Framework.  Drugi szablon jest objęty aplikacją .NET Core->, która jest przeznaczona dla platformy .NET Core.  Każdy szablon powinien zadziałał na potrzeby tego artykułu.

3. W obszarze aplikacja konsoli, w razie potrzeby zmień w języku C# na F #.  Wybierz przycisk **dalej** , aby przejść do przodu!  

4. Nadaj projektowi nazwę, a następnie wybierz odpowiednie opcje dla aplikacji.  Zwróć uwagę, że okienko podglądu z boku ekranu spowoduje wyświetlenie struktury katalogów, która zostanie utworzona na podstawie wybranych opcji.  

5. Kliknij pozycję **Utwórz**.  Powinien być teraz widoczny projekt F # w Eksplorator rozwiązań.

## <a name="writing-your-code"></a>Pisanie kodu

Zacznijmy od zapisania najpierw kodu.  Upewnij się, że `Program.fs` plik jest otwarty, a następnie zastąp jego zawartość następującym:

[!code-fsharp[HelloSquare](~/samples/snippets/fsharp/getting-started/hello-square.fs)]

W poprzednim przykładzie kodu zdefiniowano funkcję, `square` która przyjmuje dane wejściowe `x` i mnoży ją przez siebie.  Ponieważ F # używa [wnioskowania o typie](../language-reference/type-inference.md), `x` nie trzeba określać typu.  Kompilator F # rozumie typy, w których mnożenie jest prawidłowe i przypisuje typ na `x` podstawie sposobu `square` wywoływania.  Po umieszczeniu wskaźnika myszy na stronie `square` powinny zostać wyświetlone następujące elementy:

```console
val square: x:int -> int
```

Jest to element znany jako podpis typu funkcji.  Można go odczytać w następujący sposób: "kwadrat jest funkcją, która przyjmuje liczbę całkowitą o nazwie x i tworzy liczbę całkowitą".  Należy zauważyć, że kompilator `square` nadał `int` teraz typ. jest to spowodowane tym, że mnożenie nie jest ogólne dla *wszystkich* typów, ale raczej jest ogólny w przypadku zamkniętego zestawu typów.  Kompilator F # został pobrany `int` w tym momencie, ale dopasowuje podpis typu w przypadku wywołania `square` z innym typem danych wejściowych, na przykład `float` .

Inna funkcja, `main` ,, jest zdefiniowana z `EntryPoint` atrybutem do informowania kompilatora F # o tym, że wykonanie programu powinno się uruchomić.  Ta sama Konwencja jest zgodna z innymi [językami programowania w stylu C](https://en.wikipedia.org/wiki/Entry_point#C_and_C.2B.2B), gdzie argumenty wiersza polecenia mogą być przekazane do tej funkcji i zwracany jest kod liczby całkowitej (zazwyczaj `0` ).

Jest to funkcja, która wywołuje `square` funkcję z argumentem `12` .  Kompilator F # następnie przypisuje typ `square` do `int -> int` (czyli funkcję, która przyjmuje `int` i tworzy `int` ).  Wywołanie `printfn` jest sformatowaną funkcją drukowania, która używa ciągu formatu, podobnego do języków programowania w stylu C, parametrów, które odpowiadają określonym w ciągu formatu, a następnie drukuje wynik i nowy wiersz.

## <a name="running-your-code"></a>Uruchamianie kodu

Możesz uruchomić kod i zobaczyć wyniki, klikając polecenie **Uruchom** w menu najwyższego poziomu, a następnie **uruchamiając bez debugowania**.  Spowoduje to uruchomienie programu bez debugowania i umożliwi wyświetlenie wyników.

W oknie konsoli powinna zostać wyświetlona następująca wartość, która Visual Studio dla komputerów Mac zdjęte:

```console
12 squared is 144!
```

Gratulacje!  Utworzono pierwszy projekt F # w Visual Studio dla komputerów Mac, napisanie funkcji języka F # spowodowało wydrukowanie wyników wywołania tej funkcji i uruchomienie projektu w celu wyświetlenia niektórych wyników.

## <a name="using-f-interactive"></a>Używanie F# Interactive

Jedną z najlepszych funkcji narzędzi Visual F# w Visual Studio dla komputerów Mac jest okno F# Interactive.  Umożliwia wysyłanie kodu do procesu, w którym można wywołać ten kod i interaktywnie zobaczyć wynik.

Aby rozpocząć korzystanie z niego, zaznacz `square` funkcję zdefiniowaną w kodzie.  Następnie kliknij pozycję **Edytuj** w menu najwyższego poziomu.  Następnie wybierz pozycję **Wyślij zaznaczenie do F# Interactive**.  Spowoduje to wykonanie kodu w oknie F# Interactive.  Alternatywnie możesz kliknąć prawym przyciskiem myszy zaznaczenie i wybrać polecenie **Wyślij zaznaczenie do F# Interactive**.  Powinno zostać wyświetlone okno F# Interactive z następującym w nim:

```console
>

val square : x:int -> int

>
```

Pokazuje to ten sam podpis funkcji dla `square` funkcji, która została wcześniej umieszczona po umieszczeniu wskaźnika myszy nad funkcją.  Ponieważ `square` jest teraz zdefiniowany w procesie F# Interactive, można wywołać go z różnymi wartościami:

```console
> square 12;;
val it : int = 144
>square 13;;
val it : int = 169
```

Wykonuje funkcję, wiąże wynik z nową nazwą `it` i wyświetla typ i wartość `it` .  Należy pamiętać, że każdy wiersz należy zamknąć za pomocą `;;` .  Jest to sposób, w jaki F# Interactive wie, gdy wywołanie funkcji zostało zakończone.  Można także definiować nowe funkcje w F# Interactive:

```console
> let isOdd x = x % 2 <> 0;;

val isOdd : x:int -> bool

> isOdd 12;;
val it : bool = false
```

Powyższe definiuje nową funkcję, `isOdd` która pobiera `int` i sprawdza, czy jest nieparzysta.  Możesz wywołać tę funkcję, aby zobaczyć, co zwraca z innymi danymi wejściowymi.  Można wywoływać funkcje w ramach wywołań funkcji:

```console
> isOdd (square 15);;
val it : bool = true
```

Można również użyć [operatora przekazywania potoków](../language-reference/symbol-and-operator-reference/index.md) , aby przekierować wartość do dwóch funkcji:

```console
> 15 |> square |> isOdd;;
val it : bool = true
```

Operator przekazujący przekazanie dalej i inne są omówione w kolejnych samouczkach.

Jest to tylko możliwość wypróbowania innowacyjnego do tego, co można zrobić z F# Interactive.  Aby dowiedzieć się więcej, zapoznaj się [z programowaniem interaktywnym przy użyciu języka F #](../tools/fsharp-interactive/index.md).

## <a name="next-steps"></a>Następne kroki

Jeśli jeszcze tego nie zrobiono, zapoznaj się [z przewodnikiem języka f #](../tour.md), który obejmuje niektóre podstawowe funkcje języka f #.  Udostępnimy przegląd niektórych możliwości języka F # i udostępniamy dużo przykładów kodu, które można skopiować do Visual Studio dla komputerów Mac i uruchamiać.  Istnieją również pewne doskonałe zasoby zewnętrzne, których można użyć w [przewodniku F #](../index.yml).

## <a name="see-also"></a>Zobacz też

- [Podręcznik języka F#](../index.yml)
- [Przewodnik po środowisku F#](../tour.md)
- [Materiały referencyjne dotyczące języka F#](../language-reference/index.md)
- [Wnioskowanie o typie](../language-reference/type-inference.md)
- [Odwołanie do symbolu i operatora](../language-reference/symbol-and-operator-reference/index.md)
