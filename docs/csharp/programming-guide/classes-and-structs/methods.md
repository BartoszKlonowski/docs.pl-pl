---
title: Metody — Przewodnik programowania w języku C#
description: Metoda w języku C# jest blokiem kodu, który zawiera serie instrukcji. Program uruchamia instrukcje, wywołując metodę i określając argumenty.
ms.date: 07/20/2015
helpviewer_keywords:
- methods [C#]
- C# language, methods
ms.assetid: cc738f07-e8cd-4683-9585-9f40c0667c37
ms.openlocfilehash: 7b411283822360f3057b0d4f4e60ebade4fe45bc
ms.sourcegitcommit: 9c45035b781caebc63ec8ecf912dc83fb6723b1f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/25/2020
ms.locfileid: "88810940"
---
# <a name="methods-c-programming-guide"></a>Metody (Przewodnik programowania w języku C#)

Metoda jest blokiem kodu, który zawiera serie instrukcji. Program powoduje wykonanie instrukcji przez wywołanie metody i określenie wszelkich wymaganych argumentów metody. W języku C# Każda wykonana instrukcja jest wykonywana w kontekście metody. `Main`Metoda jest punktem wejścia dla każdej aplikacji w języku C# i jest wywoływana przez środowisko uruchomieniowe języka wspólnego (CLR), gdy program jest uruchomiony.

> [!NOTE]
> W tym artykule omówiono nazwane metody. Aby uzyskać informacje na temat funkcji anonimowych, zobacz [funkcje anonimowe](../statements-expressions-operators/anonymous-functions.md).

## <a name="method-signatures"></a>Sygnatury metod

Metody są zadeklarowane w [klasie](../../language-reference/keywords/class.md), [strukturze](../../language-reference/builtin-types/struct.md)lub [interfejsie](../interfaces/index.md) przez określenie poziomu dostępu, takiego jak `public` lub `private` , Modyfikatory opcjonalne, takie jak `abstract` lub `sealed` , wartość zwracana, nazwa metody i wszystkie parametry metody. Te części razem są sygnaturą metody.

> [!IMPORTANT]
> Zwracany typ metody nie jest częścią podpisu metody do celów przeciążania metody. Jednakże jest częścią podpisu metody podczas określania zgodności między delegatem a metodą, do której wskazuje.

Parametry metody są ujęte w nawiasy i są rozdzielone przecinkami. Puste nawiasy wskazują, że metoda nie wymaga żadnych parametrów. Ta klasa zawiera cztery metody:

[!code-csharp[csProgGuideObjects#40](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#40)]

## <a name="method-access"></a>Dostęp do metody

Wywołanie metody na obiekcie jest podobne do uzyskiwania dostępu do pola. Po nazwie obiektu Dodaj kropkę, nazwę metody i nawiasów. Argumenty są wyświetlane w nawiasach i są oddzielone przecinkami. Metody `Motorcycle` klasy mogą więc być wywoływane jak w poniższym przykładzie:

[!code-csharp[csProgGuideObjects#41](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#41)]

## <a name="method-parameters-vs-arguments"></a>Parametry metody a argumenty

Definicja metody Określa nazwy i typy wymaganych parametrów. Gdy Wywoływanie kodu wywołuje metodę, dostarcza konkretnych wartości nazywanych argumentami dla każdego parametru. Argumenty muszą być zgodne z typem parametru, ale nazwa argumentu (jeśli istnieje) użyta w kodzie wywołującym nie musi być taka sama jak parametr o nazwie zdefiniowanej w metodzie. Na przykład:

[!code-csharp[csProgGuideObjects#74](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#74)]

## <a name="passing-by-reference-vs-passing-by-value"></a>Przekazywanie przez odwołanie a przekazywanie przez wartość

Domyślnie, gdy wystąpienie [typu wartości](../../language-reference/builtin-types/value-types.md) jest przenoszone do metody, jego kopia jest przenoszona zamiast samego wystąpienia. W związku z tym zmiany argumentu nie mają wpływu na oryginalne wystąpienie w metodzie wywołującej. Aby przekazać wystąpienie typu wartości przez odwołanie, użyj `ref` słowa kluczowego. Aby uzyskać więcej informacji, zobacz [przekazywanie parametrów typu wartości](./passing-value-type-parameters.md).

Gdy obiekt typu referencyjnego jest przenoszona do metody, odwołanie do obiektu jest przesyłane. Oznacza to, że metoda nie odbiera samego obiektu, ale argument, który wskazuje lokalizację obiektu. Jeśli zmienisz element członkowski obiektu za pomocą tego odwołania, zmiana zostanie odzwierciedlona w argumencie metody wywołującej, nawet jeśli przekażesz obiekt przez wartość.

Typ referencyjny można utworzyć za pomocą `class` słowa kluczowego, jak pokazano w poniższym przykładzie:

[!code-csharp[csProgGuideObjects#42](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#42)]

Teraz, Jeśli przekażesz obiekt, który jest oparty na tym typie metody, odwołanie do obiektu zostanie przekazane. Poniższy przykład przekazuje obiekt typu `SampleRefType` do metody `ModifyObject` :

[!code-csharp[csProgGuideObjects#75](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#75)]

Przykład zasadniczo działa tak samo jak w poprzednim przykładzie, że przekazuje argument przez wartość do metody. Jednak, ponieważ jest używany typ referencyjny, wynik jest różny. Modyfikacja wprowadzona w `ModifyObject` `value` polu parametru, `obj` , również zmiana `value` pola argumentu, `rt` , w `TestRefType` metodzie. `TestRefType`Metoda wyświetla 33 jako dane wyjściowe.

Aby uzyskać więcej informacji na temat przekazywania typów odwołań przez odwołanie i wartość, zobacz [przekazywanie parametrów typu odwołania](./passing-reference-type-parameters.md) i [typy odwołań](../../language-reference/keywords/reference-types.md).

## <a name="return-values"></a>Wartości zwracane

Metody mogą zwracać wartość do obiektu wywołującego. Jeśli zwracany typ, typ wymieniony przed nazwą metody nie jest `void` , Metoda może zwrócić wartość przy użyciu `return` słowa kluczowego. Instrukcja ze `return` słowem kluczowym, po której następuje wartość zgodna z typem zwracanym, zwróci tę wartość do obiektu wywołującego metody.

Wartość można zwrócić do obiektu wywołującego przez wartość lub, rozpoczynając od języka C# [7,0.](ref-returns.md) Wartości są zwracane do obiektu wywołującego przez odwołanie, jeśli `ref` słowo kluczowe jest używane w podpisie metody i następuje po każdym `return` słowie kluczowym. Na przykład następująca sygnatura metody i instrukcja return wskazują, że metoda zwraca nazwy zmiennych `estDistance` przez odwołanie do obiektu wywołującego.

```csharp
public ref double GetEstimatedDistance()
{
    return ref estDistance;
}
```

`return`Słowo kluczowe również przerywa wykonywanie metody. Jeśli zwracanym typem jest `void` , `return` instrukcja bez wartości jest nadal przydatna do zatrzymania wykonywania metody. Bez `return` słowa kluczowego, Metoda zostanie zatrzymana po osiągnięciu końca bloku kodu. Metody z typem zwracanym innym niż void są wymagane do `return` zwrócenia wartości za pomocą słowa kluczowego. Na przykład te dwie metody używają `return` słowa kluczowego do zwracania liczb całkowitych:

[!code-csharp[csProgGuideObjects#44](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#44)]

Aby użyć wartości zwracanej z metody, Metoda wywołująca może użyć wywołania metody, wszędzie tam, gdzie wartość tego samego typu byłaby wystarczająca. Możesz również przypisać wartość zwracaną do zmiennej. Na przykład następujące dwa przykłady kodu mają ten sam cel:

[!code-csharp[csProgGuideObjects#45](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#45)]

[!code-csharp[csProgGuideObjects#46](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#46)]

Użycie zmiennej lokalnej, w tym przypadku, `result` do przechowywania wartości jest opcjonalne. Może to pomóc w czytelności kodu lub może być konieczne, jeśli konieczne będzie przechowywanie pierwotnej wartości argumentu dla całego zakresu metody.

Aby użyć wartości zwracanej przez odwołanie z metody, należy zadeklarować zmienną [lokalną ref](ref-returns.md#ref-locals) , jeśli zamierzasz zmodyfikować jej wartość. Na przykład, jeśli `Planet.GetEstimatedDistance` Metoda zwraca <xref:System.Double> wartość przez odwołanie, można ją zdefiniować jako zmienną lokalną ref z kodem podobnym do poniższego:

```csharp
ref int distance = plant
```

Zwracanie wielowymiarowej tablicy z metody, `M` która modyfikuje zawartość tablicy, nie jest konieczna, jeśli wywoływana funkcja przekazała tablicę do `M` .  Można zwrócić wynikową tablicę z `M` dla dobrego stylu lub przepływu funkcjonalnego wartości, ale nie jest to konieczne, ponieważ C# przekazuje wszystkie typy odwołań przez wartość, a wartość odwołania tablicy jest wskaźnikiem do tablicy. W metodzie `M` wszelkie zmiany zawartości tablicy są zauważalne przez dowolny kod, który ma odwołanie do tablicy, jak pokazano w następującym przykładzie:

```csharp
static void Main(string[] args)
{
    int[,] matrix = new int[2, 2];
    FillMatrix(matrix);
    // matrix is now full of -1
}

public static void FillMatrix(int[,] matrix)
{
    for (int i = 0; i < matrix.GetLength(0); i++)
    {
        for (int j = 0; j < matrix.GetLength(1); j++)
        {
            matrix[i, j] = -1;
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [Return](../../language-reference/keywords/return.md).

## <a name="async-methods"></a>Metody asynchroniczne

Za pomocą funkcji asynchronicznej można wywołać metody asynchroniczne bez używania jawnych wywołań zwrotnych lub ręcznie podzielić kod na wiele metod lub wyrażenia lambda.

Jeśli oznaczesz metodę za pomocą modyfikatora [asynchronicznego](../../language-reference/keywords/async.md) , możesz użyć operatora [await](../../language-reference/operators/await.md) w metodzie. Gdy kontrolka osiągnie wyrażenie await w metodzie asynchronicznej, sterowanie powraca do obiektu wywołującego, a postęp w metodzie jest zawieszony do momentu zakończenia zadania oczekiwania. Po zakończeniu zadania wykonywanie może zostać wznowione w metodzie.

> [!NOTE]
> Metoda asynchroniczna wraca do obiektu wywołującego, gdy napotka on pierwszy oczekujący obiekt, który nie został jeszcze ukończony lub otrzymuje koniec metody asynchronicznej, zależnie od tego, co się dzieje.

Metoda asynchroniczna może mieć zwracany typ <xref:System.Threading.Tasks.Task%601> , <xref:System.Threading.Tasks.Task> lub void. Typ zwracany void jest używany głównie do definiowania programów obsługi zdarzeń, gdzie wymagany jest zwracany typ void. Metoda asynchroniczna zwracająca typ void nie może być oczekiwana, a obiekt wywołujący metodę void nie może przechwytywać wyjątków, które metoda zgłasza.

W poniższym przykładzie `DelayAsync` jest metoda async, która ma zwracany typ <xref:System.Threading.Tasks.Task%601> . `DelayAsync` zawiera `return` instrukcję zwracającą liczbę całkowitą. W związku z tym Deklaracja metody `DelayAsync` musi mieć typ zwracany `Task<int>` . Ponieważ typem zwracanym jest `Task<int>` , obliczanie `await` wyrażenia w `DoSomethingAsync` tworzy liczbę całkowitą, jak pokazano w poniższej instrukcji: `int result = await delayTask` .

`Main`Metoda jest przykładem metody asynchronicznej, która ma zwracany typ <xref:System.Threading.Tasks.Task> . Przechodzi do `DoSomethingAsync` metody, a ponieważ jest wyrażana z pojedynczym wierszem, może pominąć `async` `await` słowa kluczowe i. Ponieważ `DoSomethingAsync` jest to Metoda asynchroniczna, zadanie dla wywołania `DoSomethingAsync` musi być oczekiwane, jak pokazano w poniższej instrukcji: `await DoSomethingAsync();` .

:::code language="csharp" source="snippets/classes-and-structs/methods/Program.cs":::

Metoda async nie może deklarować parametrów [ref](../../language-reference/keywords/ref.md) ani [out](../../language-reference/keywords/out-parameter-modifier.md) , ale może wywoływać metody, które mają takie parametry.

Aby uzyskać więcej informacji na temat metod asynchronicznych, zobacz [programowanie asynchroniczne z asynchroniczne i oczekujące](../concepts/async/index.md) i [asynchroniczne typy zwracane](../concepts/async/async-return-types.md).

## <a name="expression-body-definitions"></a>Definicje treści wyrażenia

Często istnieją definicje metod, które po prostu zwracają bezpośrednio z wynikiem wyrażenia lub które mają pojedynczą instrukcję jako treść metody. Istnieje skrót do definiowania takich metod przy użyciu `=>` :

```csharp
public Point Move(int dx, int dy) => new Point(x + dx, y + dy);
public void Print() => Console.WriteLine(First + " " + Last);
// Works with operators, properties, and indexers too.
public static Complex operator +(Complex a, Complex b) => a.Add(b);
public string Name => First + " " + Last;
public Customer this[long id] => store.LookupCustomer(id);
```

Jeśli metoda zwraca `void` lub jest metodą asynchroniczną, treść metody musi być wyrażeniem instrukcji (analogicznie jak w przypadku wyrażeń lambda). W przypadku właściwości i indeksatorów muszą one być tylko do odczytu i nie można używać `get` słowa kluczowego metody dostępu.

## <a name="iterators"></a>Iteratory

Iterator wykonuje niestandardową iterację w kolekcji, na przykład listę lub tablicę. Iterator używa instrukcji [yield return](../../language-reference/keywords/yield.md) , aby zwrócić każdy element po jednym naraz. Po osiągnięciu instrukcji [yield return](../../language-reference/keywords/yield.md) bieżąca lokalizacja w kodzie jest zapamiętywana. Wykonanie jest uruchamiane ponownie z tej lokalizacji, kiedy iterator jest wywoływana następnym razem.

Należy wywołać iterator z kodu klienta przy użyciu instrukcji [foreach](../../language-reference/keywords/foreach-in.md) .

Zwracany typ iteratora może mieć wartość <xref:System.Collections.IEnumerable> , <xref:System.Collections.Generic.IEnumerable%601> , <xref:System.Collections.IEnumerator> , lub <xref:System.Collections.Generic.IEnumerator%601> .

Aby uzyskać więcej informacji, zobacz [Iteratory](../concepts/iterators.md).

## <a name="c-language-specification"></a>specyfikacja języka C#

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>Zobacz też

- [Przewodnik programowania w języku C#](../index.md)
- [Klasy i struktury](index.md)
- [Modyfikatory dostępu](access-modifiers.md)
- [Klasy statyczne i statyczni członkowie klas](static-classes-and-static-class-members.md)
- [Dziedziczenie](inheritance.md)
- [Klasy abstrakcyjne i zapieczętowane oraz członkowie klas](abstract-and-sealed-classes-and-class-members.md)
- [params](../../language-reference/keywords/params.md)
- [return](../../language-reference/keywords/return.md)
- [określoną](../../language-reference/keywords/out.md)
- [ref](../../language-reference/keywords/ref.md)
- [Przekazywanie parametrów](passing-parameters.md)
