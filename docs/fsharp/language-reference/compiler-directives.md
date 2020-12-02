---
title: Dyrektywy kompilatora
description: 'Poznaj dyrektywy preprocesora języka F #, dyrektywy warunkowej kompilacji, dyrektywy wiersza i dyrektywy kompilatora.'
ms.date: 12/10/2018
f1_keywords:
- '#endif_FS'
ms.openlocfilehash: ff106339478c3413dc6458b12f12e1d3f9cd1fe5
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96438177"
---
# <a name="compiler-directives"></a>Dyrektywy kompilatora

W tym temacie opisano dyrektywy procesora i dyrektywy kompilatora.

## <a name="preprocessor-directives"></a>Dyrektywy preprocesora

Dyrektywa preprocesora jest poprzedzona znakiem # symbol i jest wyświetlana w wierszu. Jest on interpretowany przez preprocesor, który jest uruchamiany przed samym kompilatorem.

W poniższej tabeli wymieniono dyrektywy preprocesora, które są dostępne w języku F #.

|Dyrektywę|Opis|
|---------|-----------|
|`#if`*symbol*|Obsługuje kompilację warunkową. Kod w sekcji po `#if` zostanie uwzględniony, jeśli *symbol* jest zdefiniowany. Symbol może być również negacją `!` .|
|`#else`|Obsługuje kompilację warunkową. Oznacza sekcję kodu do dołączenia, jeśli symbol używany z poprzednim `#if` nie został zdefiniowany.|
|`#endif`|Obsługuje kompilację warunkową. Oznacza koniec sekcji warunkowej kodu.|
|`#`liniow *int*,<br/>`#`liniow *int* *ciąg* int,<br/>`#`liniow *int* *Verbatim — ciąg*|Wskazuje pierwotny wiersz kodu źródłowego i nazwę pliku na potrzeby debugowania. Ta funkcja jest dostępna dla narzędzi generujących kod źródłowy języka F #.|
|`#nowarn`*WarningCode*|Wyłącza ostrzeżenie lub ostrzeżenia kompilatora. Aby wyłączyć ostrzeżenie, Znajdź jego numer z danych wyjściowych kompilatora i umieść go w cudzysłowie. Pomiń prefiks "FS". Aby wyłączyć wiele numerów ostrzeżeń w tym samym wierszu, należy uwzględnić każdą liczbę w cudzysłowie i oddzielić każdy ciąg znaków spacją. Przykład:

`#nowarn "9" "40"`

Efekt wyłączenia ostrzeżenia dotyczy całego pliku, w tym części pliku, który poprzedza dyrektywę. |

## <a name="conditional-compilation-directives"></a>Dyrektywy kompilacji warunkowej

Kod zdezaktywowany przez jedną z tych dyrektyw jest wyszarzony w edytorze Visual Studio Code.

> [!NOTE]
> Zachowanie dyrektyw kompilacji warunkowej nie jest takie samo, jak w innych językach. Na przykład nie można używać wyrażeń logicznych obejmujących symbole i `true` i `false` nie mają specjalnego znaczenia. Symbole, które są używane w `if` dyrektywie, muszą być zdefiniowane w wierszu polecenia lub w ustawieniach projektu; nie istnieje `define` dyrektywa preprocesora.

Poniższy kod ilustruje użycie `#if` `#else` dyrektyw, i `#endif` . W tym przykładzie kod zawiera dwie wersje definicji `function1` . Gdy `VERSION1` jest zdefiniowany przy użyciu [opcji-define kompilatora](./compiler-options.md), `#if` jest uaktywniany kod między dyrektywą i `#else` dyrektywą. W przeciwnym razie kod między `#else` i `#endif` jest aktywowany.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet7301.fs)]

Brak `#define` dyrektywy preprocesora w języku F #. Aby zdefiniować symbole używane przez dyrektywę, należy użyć opcji kompilatora lub ustawienia projektu `#if` .

Dyrektywy kompilacji warunkowej mogą być zagnieżdżane. Wcięcia nie są znaczące w przypadku dyrektyw preprocesora.

Możesz również Negate symbol z `!` . W tym przykładzie wartość ciągu jest coś tylko wtedy, gdy _nie_ jest debugowana:

```fsharp
#if !DEBUG
let str = "Not debugging!"
#else
let str = "Debugging!"
#endif
```

## <a name="line-directives"></a>Dyrektywy linii

Podczas kompilowania kompilator zgłasza błędy w kodzie języka F # przez odwołujące się do nich numery wierszy, na których występuje każdy błąd. Te numery wierszy zaczynają się od 1 dla pierwszego wiersza w pliku. Jeśli jednak generujesz kod źródłowy języka F # z innego narzędzia, numery wierszy w wygenerowanym kodzie nie są generalnie przydatne, ponieważ błędy w generowanym kodzie F # prawdopodobnie powstają z innego źródła. `#line`Dyrektywa zawiera sposób tworzenia przez autorów narzędzi, które generują kod źródłowy języka f # w celu przekazywania informacji o oryginalnych numerach wierszy i plikach źródłowych do wygenerowanego kodu f #.

W przypadku używania `#line` dyrektywy nazwy plików muszą być ujęte w cudzysłów. Chyba że token Verbatim ( `@` ) pojawia się przed ciągiem, należy wypróbować odwrotne ukośniki, używając dwóch ukośników odwrotnych zamiast jednego, aby użyć ich w ścieżce. Poniżej podano prawidłowe tokeny wiersza. W tych przykładach Załóżmy, że oryginalny plik `Script1` powoduje automatyczne wygenerowanie pliku kodu F #, gdy jest uruchamiany za pośrednictwem narzędzia i że kod w lokalizacji tych dyrektyw jest generowany na podstawie niektórych tokenów w wierszu 25 w pliku `Script1` .

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet7303.fs)]

Te tokeny wskazują, że kod języka F # wygenerowany w tej lokalizacji pochodzi od niektórych konstrukcji w lub blisko wiersza `25` w `Script1` .

## <a name="compiler-directives"></a>Dyrektywy kompilatora

Dyrektywy kompilatora przypominają dyrektywy preprocesora, ponieważ są poprzedzone znakiem #, ale zamiast nie są interpretowane przez preprocesor, są pozostawiane dla kompilatora, który interpretuje i działa.

W poniższej tabeli wymieniono dyrektywy kompilatora, które są dostępne w języku F #.

|Dyrektywę|Opis|
|---------|-----------|
|`#light` ["on" &#124; "off"]|Włącza lub wyłącza uproszczoną składnię w celu zapewnienia zgodności z innymi wersjami ML. Domyślnie uproszczona składnia jest włączona. Pełna składnia jest zawsze włączona. W związku z tym można użyć składni uproszczonej i pełnej składni. Sama dyrektywa `#light` jest równoważna z `#light "on"` . Jeśli określisz `#light "off"` , musisz użyć pełnej składni dla wszystkich konstrukcji językowych. Składnia w dokumentacji języka F # jest prezentowana z założeniem, że używana jest składnia uproszczona. Aby uzyskać więcej informacji, zobacz [verbose Syntax](verbose-syntax.md).|

Aby poznać dyrektywy interpretera (fsi.exe), zobacz [programowanie interaktywne przy użyciu języka F #](../tools/fsharp-interactive/index.md).

## <a name="see-also"></a>Zobacz też

- [Dokumentacja języka F #](index.md)
- [Opcje kompilatora](compiler-options.md)
