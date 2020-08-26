---
title: Ciągi
description: 'Dowiedz się, jak typ "String" języka F # reprezentuje niezmienny tekst jako sekwencję znaków Unicode.'
ms.date: 08/15/2020
ms.openlocfilehash: f6ec36feeb197bf785c702e7b626cf5cf80696ab
ms.sourcegitcommit: 9c45035b781caebc63ec8ecf912dc83fb6723b1f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/25/2020
ms.locfileid: "88812214"
---
# <a name="strings"></a>Ciągi

`string`Typ reprezentuje niezmienny tekst jako sekwencję znaków Unicode. `string` jest aliasem dla `System.String` platformy .NET.

## <a name="remarks"></a>Uwagi

Literały ciągów są rozdzielane znakami cudzysłowu ("). Znak ukośnika odwrotnego ( \\ ) jest używany do kodowania niektórych znaków specjalnych. Ukośnik odwrotny i następny znak razem są znane jako *sekwencja ucieczki*. W poniższej tabeli przedstawiono sekwencje unikowe obsługiwane w literałach ciągu języka F #.

|Znak|Sekwencja ucieczki|
|---------|---------------|
|Alerty|`\a`|
|Backspace|`\b`|
|Kanał informacyjny formularza|`\f`|
|Ani|`\n`|
|Znak powrotu karetki|`\r`|
|Tab|`\t`|
|Tabulator pionowy|`\v`|
|Ukośnika odwrotnego|`\\`|
|Cudzysłów|`\"`|
|Apostrof|`\'`|
|znak Unicode|`\DDD` (gdzie `D` wskazuje cyfrę dziesiętną; zakres 000-255; na przykład `\231` = "ç")|
|znak Unicode|`\xHH` (gdzie `H` wskazuje cyfrę szesnastkową; zakres 00-FF; na przykład `\xE7` = "ç")|
|znak Unicode|`\uHHHH` (UTF-16) (gdzie `H` wskazuje cyfrę szesnastkową; zakres 0000-FFFF;  na przykład `\u00E7` = "ç")|
|znak Unicode|`\U00HHHHHH` (UTF-32) (gdzie `H` wskazuje cyfrę szesnastkową; zakres 000000-10FFFF;  na przykład `\U0001F47D` = " 👽 ")|

> [!IMPORTANT]
> `\DDD`Sekwencja ucieczki jest notacją dziesiętną, a nie notacją ósemkową, taką jak w większości innych języków. W związku z tym cyfry `8` i `9` są prawidłowe, a sekwencja `\032` reprezentuje spację (U + 0020), natomiast ten sam punkt kodu w notacji ósemkowej będzie `\040` .

> [!NOTE]
> Są ograniczone do zakresu 0-255 (0xFF), `\DDD` a `\x` Sekwencje ucieczki są efektywnie zestawem znaków [ISO-8859-1](https://en.wikipedia.org/wiki/ISO/IEC_8859-1#Code_page_layout) , ponieważ dopasowuje pierwsze 256 punktów kodowych Unicode.

## <a name="verbatim-strings"></a>Verbatim ciągi

Jeśli poprzedzany przez symbol @, literał jest ciągiem Verbatim. Oznacza to, że wszystkie sekwencje ucieczki są ignorowane, z tą różnicą, że dwa znaki cudzysłowu są interpretowane jako jeden znak cudzysłowu.

## <a name="triple-quoted-strings"></a>Potrójne ciągi ujęte w cudzysłów

Ponadto ciąg może być ujęty w potrójne cudzysłowy. W takim przypadku wszystkie sekwencje ucieczki są ignorowane, w tym znaki podwójnego cudzysłowu. Aby określić ciąg zawierający osadzony ciąg ujęty w cudzysłów, można użyć ciągu Verbatim lub ciągu z potrójnym cudzysłowem. W przypadku używania ciągu Verbatim należy określić dwa znaki cudzysłowu, aby wskazać znak pojedynczego cudzysłowu. Jeśli używasz ciągu z potrójnym cudzysłowem, możesz użyć znaków pojedynczego cudzysłowu bez ich analizowania jako końca ciągu. Ta technika może być przydatna podczas pracy z danymi XML lub innymi strukturami, które zawierają osadzone znaki cudzysłowu.

```fsharp
// Using a verbatim string
let xmlFragment1 = @"<book author=""Milton, John"" title=""Paradise Lost"">"

// Using a triple-quoted string
let xmlFragment2 = """<book author="Milton, John" title="Paradise Lost">"""
```

W kodzie, ciągi, które mają podziały wierszy są akceptowane, a podziały wierszy są interpretowane dosłownie jako znaki nowego wiersza, chyba że znak ukośnika odwrotnego jest ostatnim znakiem przed przerwaniem. Wiodący biały znak w następnym wierszu jest ignorowany, gdy jest używany ukośnik odwrotny. Poniższy kod generuje ciąg `str1` , który ma wartość `"abc\ndef"` i ciąg `str2` , który ma wartość `"abcdef"` .

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1001.fs)]

## <a name="string-indexing-and-slicing"></a>Indeksowanie ciągów i skalowanie

Można uzyskać dostęp do pojedynczych znaków w ciągu za pomocą składni podobnej do tablicy, jak pokazano poniżej.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1002.fs)]

Wynik to `b`.

Lub można wyodrębnić podciągi przy użyciu składni wycinka tablicy, jak pokazano w poniższym kodzie.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1003.fs)]

Dane wyjściowe są następujące:

```console
abc
def
```

Ciągi ASCII można reprezentować według tablic bajtów bez znaku `byte[]` . Należy dodać sufiks `B` do literału ciągu, aby wskazać, że jest to ciąg ASCII. Literały ciągu ASCII używane z tablicami bajtowymi obsługują te same sekwencje unikowe co ciągi Unicode, z wyjątkiem sekwencji unikowych Unicode.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1004.fs)]

## <a name="string-operators"></a>Operatory ciągów

`+`Operatora można używać do łączenia ciągów, zapewniając zgodność z funkcjami obsługi ciągów .NET Framework. Poniższy przykład ilustruje łączenie ciągów.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1006.fs)]

## <a name="string-class"></a>String — Klasa

Ponieważ typ ciągu w F # jest w rzeczywistości typem .NET Framework `System.String` , wszystkie `System.String` elementy członkowskie są dostępne. Obejmuje `+` operator, który jest używany do łączenia ciągów, `Length` Właściwość i `Chars` Właściwość, która zwraca ciąg jako tablicę znaków Unicode. Aby uzyskać więcej informacji na temat ciągów, zobacz `System.String` .

Za pomocą `Chars` właściwości `System.String` , można uzyskać dostęp do poszczególnych znaków w ciągu, określając indeks, jak pokazano w poniższym kodzie.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1005.fs)]

## <a name="string-module"></a>Moduł String

Dodatkowe funkcje obsługi ciągów są zawarte w `String` module w `FSharp.Core` przestrzeni nazw. Aby uzyskać więcej informacji, zobacz temat [String module](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-stringmodule.html).

## <a name="see-also"></a>Zobacz też

- [Dokumentacja języka F #](index.md)
