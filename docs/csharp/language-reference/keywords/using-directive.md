---
description: Using — odwołanie w C#
title: Using — odwołanie w C#
ms.date: 07/20/2015
f1_keywords:
- using_CSharpKeyword
helpviewer_keywords:
- using directive [C#]
ms.assetid: b42b8e61-5e7e-439c-bb71-370094b44ae8
ms.openlocfilehash: 77d9c894dae9adc24343ce3a639a4afb904fb0a1
ms.sourcegitcommit: 9d525bb8109216ca1dc9e39c149d4902f4b43da5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2020
ms.locfileid: "96599412"
---
# <a name="using-directive-c-reference"></a>Using — dyrektywa (odwołanie w C#)

`using`Dyrektywa ma trzy zastosowania:

- Aby zezwolić na używanie typów w przestrzeni nazw, aby nie trzeba było kwalifikować użycia typu w tej przestrzeni nazw:

    ```csharp
    using System.Text;
    ```

- Aby umożliwić dostęp do statycznych elementów członkowskich i typów zagnieżdżonych typu bez konieczności kwalifikowania dostępu przy użyciu nazwy typu.

    ```csharp
    using static System.Math;
    ```

    Aby uzyskać więcej informacji, zobacz [Using static dyrektywą](using-static.md).

- Aby utworzyć alias dla przestrzeni nazw lub typu. Ta nazwa jest nazywana *dyrektywą aliasu using*.

    ```csharp
    using Project = PC.MyCompany.Project;
    ```

`using`Słowo kluczowe jest również używane do tworzenia *instrukcji using*, które pomagają zagwarantować, że <xref:System.IDisposable> obiekty takie jak pliki i czcionki są obsługiwane poprawnie. Aby uzyskać więcej informacji, zobacz [używanie instrukcji using](using-statement.md) .

## <a name="using-static-type"></a>Używanie typu statycznego

Można uzyskać dostęp do statycznych elementów członkowskich typu bez konieczności kwalifikowania dostępu przy użyciu nazwy typu:

```csharp
using static System.Console;
using static System.Math;
class Program
{
    static void Main()
    {
        WriteLine(Sqrt(3*3 + 4*4));
    }
}
```

## <a name="remarks"></a>Uwagi

Zakres `using` dyrektywy jest ograniczony do pliku, w którym występuje.

`using`Może pojawić się dyrektywa:

- Na początku pliku kodu źródłowego przed dowolnymi obszarami nazw lub definicjami typów.
- W dowolnej przestrzeni nazw, ale przed wszelkimi obszarami nazw lub typami zadeklarowanymi w tej przestrzeni nazw.

W przeciwnym razie zostanie wygenerowany błąd kompilatora [CS1529](../../misc/cs1529.md) .

Utwórz `using` dyrektywę aliasu, aby ułatwić kwalifikowanie identyfikatora do przestrzeni nazw lub typu. W dowolnej `using` dyrektywie w pełni kwalifikowana przestrzeń nazw lub typ muszą być używane niezależnie od `using` dyrektyw, które przed nim pochodzą. Nie `using` można użyć aliasu w deklaracji `using` dyrektywy. Na przykład poniższy kod generuje błąd kompilatora:

```csharp
using s = System.Text;
using s.RegularExpressions; // Generates a compiler error.
```

Utwórz `using` dyrektywę, aby użyć typów w przestrzeni nazw bez konieczności określania przestrzeni nazw. `using`Dyrektywa nie daje dostępu do żadnych przestrzeni nazw, które są zagnieżdżone w określonym obszarze nazw.

Przestrzenie nazw są dostępne w dwóch kategoriach: zdefiniowane przez użytkownika i zdefiniowane przez system. Przestrzenie nazw zdefiniowane przez użytkownika to przestrzenie nazw zdefiniowane w kodzie. Aby uzyskać listę przestrzeni nazw zdefiniowanych przez system, zobacz [.NET API Browser](../../../../api/index.md).

## <a name="example-1"></a>Przykład 1

Poniższy przykład pokazuje, jak zdefiniować `using` alias dla przestrzeni nazw i używać go:

[!code-csharp[csrefKeywordsNamespace#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsNamespace/CS/csrefKeywordsNamespace2.cs#8)]

Dyrektywa using alias nie może mieć otwartego typu ogólnego po prawej stronie. Na przykład nie można utworzyć aliasu using dla elementu `List<T>` , ale można go utworzyć dla elementu `List<int>` .

## <a name="example-2"></a>Przykład 2

Poniższy przykład pokazuje, jak zdefiniować `using` dyrektywę i `using` alias dla klasy:

[!code-csharp[csrefKeywordsNamespace#9](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsNamespace/CS/csrefKeywordsNamespace2.cs#9)]

## <a name="c-language-specification"></a>specyfikacja języka C#

Aby uzyskać więcej informacji, zobacz [using dyrektywy](~/_csharplang/spec/namespaces.md#using-directives) w [specyfikacji języka C#](/dotnet/csharp/language-reference/language-specification/introduction). Specyfikacja języka jest ostatecznym źródłem informacji o składni i użyciu języka C#.

## <a name="see-also"></a>Zobacz także

- [Odwołanie w C#](../index.md)
- [Przewodnik programowania w języku C#](../../programming-guide/index.md)
- [Używanie przestrzeni nazw](../../programming-guide/namespaces/using-namespaces.md)
- [Słowa kluczowe języka C#](index.md)
- [Przestrzenie nazw](../../programming-guide/namespaces/index.md)
- [using, instrukcja](using-statement.md)
