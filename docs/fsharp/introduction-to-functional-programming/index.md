---
title: Wprowadzenie do programowania funkcyjnego w F#
description: 'Poznaj podstawy programowania funkcjonalnego w języku F #.'
ms.date: 10/29/2018
ms.openlocfilehash: fc2aebe80de16b92942c3557c0e03c198883dde1
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740331"
---
# <a name="introduction-to-functional-programming-in-f"></a>Wprowadzenie do programowania funkcjonalnego w języku F\#

Programowanie funkcjonalne to styl programowania, który kładzie nacisk na korzystanie z funkcji i niezmienne dane. Programistyczne programowanie funkcjonalne jest połączone z typami statycznymi, na przykład w języku F #. Ogólnie rzecz biorąc, następujące koncepcje zostały wyróżnione w programowaniu funkcjonalnym:

* Działa jako konstrukcje podstawowe, z których korzystasz
* Wyrażenia zamiast instrukcji
* Niezmienne wartości w zmiennych
* Programowanie deklaratywne nad bezwzględnym programowaniem

W tej serii zapoznajesz koncepcje i wzorce w programowaniu funkcjonalnym przy użyciu języka F #. W ten sposób dowiesz się, że tylko niektóre F #.

## <a name="terminology"></a>Terminologia

Programowanie funkcjonalne, takie jak inne odmiany programistyczne, zawiera słownictwo, które trzeba poznać. Poniżej przedstawiono niektóre typowe terminy, w których zobaczysz cały czas:

* **Function** -a funkcja jest konstrukcja, która spowoduje wygenerowanie danych wyjściowych po otrzymaniu danych wejściowych. Bardziej formalnie _mapuje_ element z jednego zestawu na inny. Ta formalność jest przekształcana w konkretną na wiele sposobów, szczególnie w przypadku korzystania z funkcji, które działają na kolekcjach danych. Jest to najbardziej podstawowe (i ważne) koncepcje programowania funkcjonalnego.
* **Wyrażenie** -wyrażenie jest konstrukcja w kodzie, która tworzy wartość. W języku F # ta wartość musi być powiązana lub jawnie ignorowana. Wyrażenie może być nieuproszczone zamieniane przez wywołanie funkcji.
* **Czystość** — czystość jest właściwością funkcji, w taki sposób, że jej wartość zwracana jest zawsze taka sama dla tych samych argumentów i że jej Ocena nie ma żadnych efektów ubocznych. Czysta funkcja zależy wyłącznie od jej argumentów.
* **Przezroczystość referencyjna** — przezroczystość referencyjna jest właściwością wyrażeń, które mogą zostać zastąpione danymi wyjściowymi bez wpływania na zachowanie programu.
* **Niezmienności** -niezmienności oznacza, że wartości nie można zmienić w miejscu. Jest to w przeciwieństwie do zmiennych, które mogą ulec zmianie w miejscu.

## <a name="examples"></a>Przykłady

W poniższych przykładach przedstawiono podstawowe pojęcia.

### <a name="functions"></a>Funkcje

Najbardziej typową i podstawową konstrukcją w programowaniu funkcjonalnym jest funkcja. Oto prosta funkcja, która dodaje 1 do liczby całkowitej:

```fsharp
let addOne x = x + 1
```

Podpis typu jest następujący:

```fsharp
val addOne: x:int -> int
```

Podpis może być odczytywany jako, " `addOne` akceptuje `int` nazwane `x` i spowoduje utworzenie `int` ". Bardziej formalnie `addOne` _mapuje_ wartość z zestawu liczb całkowitych na zestaw liczb całkowitych. `->`Token oznacza to mapowanie. W języku F # zwykle można przyjrzeć się sygnatury funkcji w celu uzyskania sensu, co robi.

Dlatego dlaczego sygnatura jest ważna? W przypadku programowania w określonym zakresie implementacja funkcji jest często mniej ważna niż faktyczny podpis typu! Fakt, że `addOne` wartość 1 jest dodawana do liczby całkowitej, jest interesujący w czasie wykonywania, ale podczas konstruowania programu, fakt, że akceptuje, i zwraca wartość, co informuje, `int` jak faktycznie będzie używać tej funkcji. Ponadto po poprawnym użyciu tej funkcji (w odniesieniu do podpisu typu) diagnozowanie wszelkich problemów może odbywać się tylko w treści `addOne` funkcji. Jest to tempo związane z programowaniem funkcjonalności w określonym typie.

### <a name="expressions"></a>Wyrażenia

Wyrażenia są konstrukcjami, które są szacowane do wartości. W przeciwieństwie do instrukcji, które wykonują akcję, wyrażenia mogą być uważane za wykonywanie akcji, która zwraca wartość. Wyrażenia są prawie zawsze używane na korzyść instrukcji w programowaniu funkcjonalnym.

Weź pod uwagę poprzednią funkcję, `addOne` . Treść `addOne` jest wyrażeniem:

```fsharp
// 'x + 1' is an expression!
let addOne x = x + 1
```

Jest to wynik tego wyrażenia, który definiuje typ wyniku `addOne` funkcji. Na przykład, wyrażenie, które powoduje, że ta funkcja może zostać zmieniony na inny typ, taki jak `string` :

```fsharp
let addOne x = x.ToString() + "1"
```

Sygnatura funkcji jest teraz:

```fsharp
val addOne: x:'a -> string
```

Ponieważ dowolny typ w języku F # może zostać `ToString()` wywołany, typ elementu `x` został utworzony jako generyczny (nazywany [automatycznym generalizacją](../language-reference/generics/automatic-generalization.md)), a wynikowy typ to `string` .

Wyrażenia nie są tylko treścią funkcji. Można utworzyć wyrażenia, które tworzą wartość używaną w innym miejscu. Typowy `if` :

```fsharp
// Checks if 'x' is odd by using the mod operator
let isOdd x = x % 2 <> 0

let addOneIfOdd input =
    let result =
        if isOdd input then
            input + 1
        else
            input

    result
```

`if`Wyrażenie generuje wartość o nazwie `result` . Należy zauważyć, że można `result` całkowicie pominąć, wprowadzając `if` wyrażenie do treści `addOneIfOdd` funkcji. Kluczem do zapamiętania w przypadku wyrażeń jest utworzenie wartości.

Istnieje typ specjalny, `unit` który jest używany, gdy nie ma niczego do zwrócenia. Rozważmy na przykład tę prostą funkcję:

```fsharp
let printString (str: string) =
    printfn $"String is: {str}"
```

Podpis wygląda następująco:

```fsharp
val printString: str:string -> unit
```

`unit`Typ wskazuje, że nie jest zwracana wartość rzeczywista. Jest to przydatne, gdy masz procedurę, która musi "do pracy" mimo braku wartości do zwrócenia w wyniku tej pracy.

Jest to bardzo zróżnicowane dla bezwzględnego programowania, gdzie równoważna `if` konstrukcja jest instrukcją, a Tworzenie wartości jest często wykonywane z mutacją zmiennych. Na przykład w języku C# kod może być zapisany w następujący sposób:

```csharp
bool IsOdd(int x) => x % 2 != 0;

int AddOneIfOdd(int input)
{
    var result = input;

    if (IsOdd(input))
    {
        result = input + 1;
    }

    return result;
}
```

Warto zauważyć, że język C# i inne języki w stylu C obsługują [wyrażenie Trzyelementowy](../../csharp/language-reference/operators/conditional-operator.md), które umożliwia programowanie warunkowe oparte na wyrażeniach.

W programowaniu funkcjonalnym rzadko można przystąpić do wartości instrukcji. Chociaż niektóre języki funkcjonalne obsługują instrukcje i mutacje, nie jest powszechna możliwość używania tych koncepcji w programowaniu funkcjonalnym.

### <a name="pure-functions"></a>Czyste funkcje

Jak wspomniano wcześniej, czyste funkcje to funkcje, które:

* Należy zawsze oszacować tę samą wartość dla tych samych danych wejściowych.
* Nie ma żadnych efektów ubocznych.

Warto traktować funkcje matematyczne w tym kontekście. W przypadku matematyki funkcje są zależne od ich argumentów i nie mają żadnych efektów ubocznych. W funkcji matematycznej `f(x) = x + 1` wartość jest `f(x)` zależna od wartości `x` . Czyste funkcje w programowaniu funkcjonalnym są takie same.

Podczas pisania czystej funkcji, funkcja musi zależeć tylko od jej argumentów i nie wykonuje żadnej akcji, która skutkuje efektem ubocznym.

Oto przykład funkcji nieczystych, ponieważ zależy ona od globalnego, modyfikowalnego stanu:

```fsharp
let mutable value = 1

let addOneToValue x = x + value
```

`addOneToValue`Funkcja jest jasno nieczytelna, ponieważ `value` można ją zmienić w dowolnym momencie, aby miała inną wartość niż 1. Ten wzorzec w zależności od wartości globalnej należy unikać w programowaniu funkcjonalnym.

Oto inny przykład nieczystej funkcji, ponieważ wykonuje efekt uboczny:

```fsharp
let addOneToValue x =
    printfn $"x is %d{x}"
    x + 1
```

Chociaż ta funkcja nie jest zależna od wartości globalnej, zapisuje wartość `x` do danych wyjściowych programu. Chociaż nie ma żadnego niewłaściwego w tym celu, oznacza to, że funkcja nie jest czysta. Jeśli inna część programu zależy od elementu zewnętrznego do programu, takiego jak bufor wyjściowy, wywołanie tej funkcji może mieć wpływ na tę inną część programu.

Usunięcie `printfn` instrukcji powoduje, że funkcja ma charakter czysty:

```fsharp
let addOneToValue x = x + 1
```

Mimo że ta funkcja nie jest jeszcze _lepsza_ niż poprzednia wersja z `printfn` instrukcją, gwarantuje, że cała ta funkcja zwraca wartość. Wywołanie tej funkcji dowolna liczba razy daje ten sam wynik: po prostu tworzy wartość. Przewidywalność podaną przez czystość to coś wielu programistów.

### <a name="immutability"></a>Niezmienność

Na koniec jednym z najważniejszych koncepcji programowania funkcjonalnego z typem jest niezmienności. W języku F # wszystkie wartości są domyślnie niezmienne. Oznacza to, że nie można ich zmodyfikować w miejscu, chyba że jawnie Oznacz je jako modyfikowalne.

W tym przypadku praca z niezmiennymi wartościami oznacza zmianę podejścia do programowania z, "muszę zmienić coś" na "chcę utworzyć nową wartość".

Na przykład dodanie 1 do wartości oznacza wygenerowanie nowej wartości, a nie mutację istniejącej:

```fsharp
let value = 1
let secondValue = value + 1
```

W języku F # następujący **kod nie ma mutacji** `value` funkcji; zamiast tego wykonuje kontrolę równości:

```fsharp
let value = 1
value = value + 1 // Produces a 'bool' value!
```

Niektóre funkcjonalne Języki programowania nie obsługują mutacji. W języku F # jest obsługiwane, ale nie jest to domyślne zachowanie dla wartości.

Koncepcja ta rozszerza jeszcze więcej do struktur danych. W programowaniu funkcjonalnym niezmienne struktury danych, takie jak zestawy (i wiele innych), mają inną implementację niż oczekiwano. Ze względu na to, że dodanie elementu do zestawu nie powoduje zmiany zestawu, tworzy _Nowy_ zestaw z dodaną wartością. W obszarze okładek jest to często realizowane przez inną strukturę danych, która umożliwia efektywne śledzenie wartości, dzięki czemu w wyniku tego można otrzymać odpowiednią reprezentację danych.

Ten styl pracy z wartościami i strukturami danych jest krytyczny, ponieważ Wymusza traktowanie dowolnej operacji, która modyfikuje coś, tak jakby tworzy nową wersję tego elementu. Pozwala to na takie jak równość i porównywalność w programach.

## <a name="next-steps"></a>Następne kroki

W następnej sekcji znajdują się dokładne funkcje, eksplorowanie różnych sposobów korzystania z nich w programowaniu funkcjonalnym.

[Funkcje pierwszej klasy](first-class-functions.md) eksplorują funkcje głęboko i pokazują, jak można ich używać w różnych kontekstach.

## <a name="further-reading"></a>Dalsze informacje

Warto zastanowić [się, że szereg funkcjonalny](https://fsharpforfunandprofit.com/posts/thinking-functionally-intro/) jest innym doskonałym zasobem, aby uzyskać informacje na temat programowania funkcjonalnego w języku F # Obejmuje ona podstawowe programowanie funkcjonalne w sposób pragmatyczny i łatwy do odczytu, przy użyciu funkcji języka F # do zilustrowania koncepcji.
