---
title: Using — odwołanie w C#
ms.date: 04/07/2020
helpviewer_keywords:
- using statement [C#]
ms.assetid: afc355e6-f0b9-4240-94dd-0d93f17d9fc3
ms.openlocfilehash: 3c479faeeb66865b8c368edba881429a7cb956ec
ms.sourcegitcommit: 5988e9a29cedb8757320817deda3c08c6f44a6aa
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/28/2020
ms.locfileid: "82199680"
---
# <a name="using-statement-c-reference"></a>using — instrukcja (odwołanie w C#)

Zapewnia wygodną składnię, która zapewnia poprawne użycie <xref:System.IDisposable> obiektów. Począwszy od języka C# 8,0, `using` instrukcja zapewnia poprawne użycie <xref:System.IAsyncDisposable> obiektów.

## <a name="example"></a>Przykład

Poniższy przykład pokazuje, `using` jak używać instrukcji.

:::code language="csharp" source="snippets/usings.cs" id="SnippetFirstExample":::

Począwszy od języka C# 8,0, można użyć następującej składni alternatywnej dla `using` instrukcji, która nie wymaga nawiasów klamrowych:

:::code language="csharp" source="snippets/usings.cs" id="SnippetModernUsing":::

## <a name="remarks"></a>Uwagi

<xref:System.IO.File>i <xref:System.Drawing.Font> są przykładami typów zarządzanych, które uzyskują dostęp do niezarządzanych zasobów (w tym przypadku dojścia do plików i konteksty urządzenia). Istnieje wiele innych rodzajów niezarządzanych zasobów i typów bibliotek klas, które hermetyzują. Wszystkie takie typy muszą implementować <xref:System.IDisposable> interfejs lub <xref:System.IAsyncDisposable> interfejs.

Gdy okres istnienia `IDisposable` obiektu jest ograniczony do pojedynczej metody, należy zadeklarować go i utworzyć jego wystąpienie w `using` instrukcji. `using` Instrukcja wywołuje <xref:System.IDisposable.Dispose%2A> metodę dla obiektu w prawidłowy sposób i (gdy jest używany w sposób pokazany wcześniej) również powoduje, że sam obiekt nie ma zakresu od razu <xref:System.IDisposable.Dispose%2A> po wywołaniu. W `using` bloku obiekt jest tylko do odczytu i nie można go modyfikować ani ponownie przypisywać. Jeśli obiekt implementuje `IAsyncDisposable` zamiast `IDisposable`, `using` instrukcja wywołuje <xref:System.IAsyncDisposable.DisposeAsync%2A> i `awaits` zwraca <xref:System.Threading.Tasks.Task>wartość.

`using` Instrukcja gwarantuje, że <xref:System.IDisposable.Dispose%2A> (lub <xref:System.IAsyncDisposable.DisposeAsync%2A>) jest wywoływana, nawet jeśli wystąpi wyjątek w `using` bloku. Można osiągnąć `try` ten sam wynik, umieszczając obiekt wewnątrz bloku, a następnie wywołując <xref:System.IDisposable.Dispose%2A> (lub <xref:System.IAsyncDisposable.DisposeAsync%2A>) w `finally` bloku; w rzeczywistości jest to sposób tłumaczenia `using` instrukcji przez kompilator. Przykładowy kod jest rozwinięty do poniższego kodu w czasie kompilacji (należy zwrócić uwagę na dodatkowe nawiasy klamrowe, aby utworzyć ograniczony zakres dla obiektu):

:::code language="csharp" source="snippets/usings.cs" id="SnippetTryFinallyExample":::

Składnia nowszej `using` instrukcji jest tłumaczy na podobny kod. `try` Blok zostanie otwarty, gdzie zmienna jest zadeklarowana. `finally` Blok jest dodawany w pobliżu otaczającego bloku, na ogół na końcu metody.

Aby uzyskać więcej informacji na `try` - `finally` temat instrukcji, zobacz artykuł [try-finally](try-finally.md) .

Wiele wystąpień typu można zadeklarować w pojedynczej `using` instrukcji, jak pokazano w poniższym przykładzie. Należy zauważyć, że nie można używać niejawnie`var`wpisanych zmiennych (), gdy deklarujesz wiele zmiennych w pojedynczej instrukcji:

:::code language="csharp" source="snippets/usings.cs" id="SnippetDeclareMultipleVariables":::

Można połączyć wiele deklaracji tego samego typu przy użyciu nowej składni wprowadzonej w języku C# 8, jak pokazano w następującym przykładzie:

:::code language="csharp" source="snippets/usings.cs" id="SnippetModernMultipleVariables":::

Można utworzyć wystąpienie obiektu zasobu, a następnie przekazać zmienną do `using` instrukcji, ale nie jest to najlepsze rozwiązanie. W takim przypadku po opuszczeniu `using` bloku przez formant obiekt pozostaje w zakresie, ale prawdopodobnie nie ma dostępu do jego niezarządzanych zasobów. Innymi słowy, nie jest już w pełni zainicjowany. Jeśli spróbujesz użyć obiektu poza `using` blokiem, istnieje ryzyko, że zostanie zgłoszony wyjątek. Z tego powodu lepiej jest utworzyć wystąpienie obiektu w `using` instrukcji i ograniczyć jego zakres do `using` bloku.

:::code language="csharp" source="snippets/usings.cs" id="SnippetDeclareBeforeUsing":::

Aby uzyskać więcej informacji na temat `IDisposable` usuwania obiektów, zobacz [Używanie obiektów implementujących interfejs IDisposable](../../../standard/garbage-collection/using-objects.md).

## <a name="c-language-specification"></a>specyfikacja języka C#

Aby uzyskać więcej informacji, zobacz [instrukcja using](~/_csharplang/spec/statements.md#the-using-statement) w [specyfikacji języka C#](/dotnet/csharp/language-reference/language-specification/introduction). Specyfikacja języka jest ostatecznym źródłem informacji o składni i użyciu języka C#.

## <a name="see-also"></a>Zobacz także

- [Odwołanie w C#](../index.md)
- [Przewodnik programowania w języku C#](../../programming-guide/index.md)
- [Słowa kluczowe języka C#](index.md)
- [using — Dyrektywa](using-directive.md)
- [Odzyskiwanie pamięci](../../../standard/garbage-collection/index.md)
- [Używanie obiektów implementujących interfejs IDisposable](../../../standard/garbage-collection/using-objects.md)
- [Interfejs IDisposable](xref:System.IDisposable)
- [Instrukcja Using w języku C# 8,0](~/_csharplang/proposals/csharp-8.0/using.md)
