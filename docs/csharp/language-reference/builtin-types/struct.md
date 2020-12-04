---
title: Typy struktur — odwołanie w C#
description: 'Dowiedz się więcej o typie struktury w języku C #'
ms.date: 10/23/2020
f1_keywords:
- struct_CSharpKeyword
helpviewer_keywords:
- struct keyword [C#]
- struct type [C#]
- structure type [C#]
ms.assetid: ff3dd9b7-dc93-4720-8855-ef5558f65c7c
ms.openlocfilehash: 96a39609e9ae8b11e9872b049134136fe1ff3e2a
ms.sourcegitcommit: 9d525bb8109216ca1dc9e39c149d4902f4b43da5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2020
ms.locfileid: "96599105"
---
# <a name="structure-types-c-reference"></a>Typy struktur (odwołanie w C#)

*Typ struktury* (lub *Typ struktury*) jest [typem wartości](value-types.md) , który może hermetyzować dane i powiązane funkcje. Użyj `struct` słowa kluczowego, aby zdefiniować typ struktury:

[!code-csharp[struct example](snippets/shared/StructType.cs#StructExample)]

Typy struktury mają *semantykę wartości*. Oznacza to, że zmienna typu struktury zawiera wystąpienie typu. Domyślnie wartości zmiennych są kopiowane przy przypisywaniu, przekazywanie argumentu do metody i zwracanie wyniku metody. W przypadku zmiennej typu struktury jest kopiowane wystąpienie typu. Aby uzyskać więcej informacji, zobacz [typy wartości](value-types.md).

Zwykle typy struktury umożliwiają projektowanie małych typów skoncentrowanych na danych, które zapewniają niewielki lub nie zachowanie. Na przykład program .NET używa typów struktury do reprezentowania liczby (zarówno [liczby całkowitej](integral-numeric-types.md) , jak i [rzeczywistej](floating-point-numeric-types.md)), [wartości logicznej](bool.md), [znaku Unicode](char.md)i [wystąpienia czasu](xref:System.DateTime). Jeśli planujesz zachowanie typu, rozważ zdefiniowanie [klasy](../keywords/class.md). Typy klas mają *semantykę odwołań*. Oznacza to, że zmienna typu klasy zawiera odwołanie do wystąpienia typu, a nie samego wystąpienia.

Ponieważ typy struktury mają semantykę wartości, zalecamy zdefiniowanie *niezmiennych* typów struktury.

## <a name="readonly-struct"></a>`readonly` konstrukcja

Począwszy od języka C# 7,2, używasz `readonly` modyfikatora, aby zadeklarować, że typ struktury jest niezmienny:

[!code-csharp[readonly struct](snippets/shared/StructType.cs#ReadonlyStruct)]

Wszystkie elementy członkowskie danych `readonly` struktury muszą być tylko do odczytu w następujący sposób:

- Dowolna deklaracja pola musi mieć [ `readonly` modyfikator](../keywords/readonly.md)
- Wszystkie właściwości, w tym implementowane przez siebie, muszą być tylko do odczytu. W języku C# 9,0 i nowszych właściwość może mieć [ `init` akcesor](../../whats-new/csharp-9.md#init-only-setters).

Gwarantuje to, że żaden element członkowski `readonly` struktury nie modyfikuje stanu struktury. W języku C# 8,0 i nowszych oznacza to, że inne elementy członkowskie wystąpienia z wyjątkiem konstruktorów są niejawnie [`readonly`](#readonly-instance-members) .

> [!NOTE]
> W `readonly` strukturze element członkowski danych modyfikowalnego typu referencyjnego nadal może mieć własny stan. Na przykład nie można zastąpić <xref:System.Collections.Generic.List%601> wystąpienia, ale można dodać do niego nowe elementy.

## <a name="readonly-instance-members"></a>`readonly` elementy członkowskie wystąpienia

Począwszy od języka C# 8,0, można również użyć `readonly` modyfikatora, aby zadeklarować, że element członkowski wystąpienia nie modyfikuje stanu struktury. Jeśli nie można zadeklarować całościowego typu struktury jako `readonly` , użyj `readonly` modyfikatora, aby oznaczyć elementy członkowskie wystąpienia, które nie modyfikują stanu struktury.

W obrębie `readonly` elementu członkowskiego wystąpienia nie można przypisać do pól wystąpienia struktury. Jednak `readonly` element członkowski może wywołać element niebędący `readonly` członkiem. W takim przypadku kompilator tworzy kopię wystąpienia struktury i wywołuje element, który nie należy do `readonly` tej kopii. W związku z tym oryginalne wystąpienie struktury nie jest modyfikowane.

Zazwyczaj należy zastosować `readonly` modyfikator do następujących rodzajów elementów członkowskich wystąpienia:

- form

  [!code-csharp[readonly method](snippets/shared/StructType.cs#ReadonlyMethod)]

  Można również zastosować `readonly` modyfikator do metod, które zastępują metody zadeklarowane w <xref:System.Object?displayProperty=nameWithType> :

  [!code-csharp[readonly override](snippets/shared/StructType.cs#ReadonlyOverride)]

- Właściwości i indeksatory:

  [!code-csharp[readonly property get](snippets/shared/StructType.cs#ReadonlyProperty)]

  Jeśli musisz zastosować `readonly` modyfikator do obu metod dostępu właściwości lub indeksatora, zastosuj go w deklaracji właściwości lub indeksatora.

  > [!NOTE]
  > Kompilator deklaruje `get` metodę dostępu do właściwości, która jest [zaimplementowana](../../programming-guide/classes-and-structs/auto-implemented-properties.md) `readonly` , niezależnie od obecności `readonly` modyfikatora w deklaracji właściwości.

  W języku C# 9,0 i nowszych można zastosować `readonly` modyfikator do właściwości lub indeksatora z `init` akcesorem:

  :::code language="csharp" source="snippets/shared/StructType.cs" id="ReadonlyWithInit":::

Nie można zastosować `readonly` modyfikatora do statycznych elementów członkowskich typu struktury.

Kompilator może używać `readonly` modyfikatora na potrzeby optymalizacji wydajności. Aby uzyskać więcej informacji, zobacz [Zapisywanie bezpiecznego i wydajnego kodu w języku C#](../../write-safe-efficient-code.md).

## <a name="limitations-with-the-design-of-a-structure-type"></a>Ograniczenia dotyczące projektowania typu struktury

Podczas projektowania typu struktury można korzystać z takich samych możliwości jak w przypadku typu [klasy](../keywords/class.md) , z następującymi wyjątkami:

- Nie można zadeklarować konstruktora bez parametrów. Każdy typ struktury zawiera już niejawny Konstruktor bez parametrów, który generuje [wartość domyślną](default-values.md) typu.

- Nie można zainicjować pola wystąpienia lub właściwości w swojej deklaracji. Można jednak zainicjować pole [static](../keywords/static.md) lub [const](../keywords/const.md) lub właściwość statyczną w swojej deklaracji.

- Konstruktor typu struktury musi inicjować wszystkie pola wystąpienia typu.

- Typ struktury nie może dziedziczyć z innego typu klasy lub struktury i nie może być podstawą klasy. Jednak typ struktury może implementować [interfejsy](../keywords/interface.md).

- Nie można zadeklarować [finalizatora](../../programming-guide/classes-and-structs/destructors.md) w obrębie typu struktury.

## <a name="instantiation-of-a-structure-type"></a>Tworzenie wystąpienia typu struktury

W języku C# należy zainicjować zadeklarowaną zmienną, zanim będzie można jej użyć. Ponieważ zmienna typu struktury nie może być `null` (chyba że jest to zmienna [typu wartości null](nullable-value-types.md)), należy utworzyć wystąpienie odpowiedniego typu. Istnieje kilka sposobów, aby to zrobić.

Zazwyczaj tworzysz typ struktury, wywołując odpowiedni Konstruktor z [`new`](../operators/new-operator.md) operatorem. Każdy typ struktury ma co najmniej jednego konstruktora. Jest to niejawny Konstruktor bez parametrów, który tworzy [wartość domyślną](default-values.md) typu. Można również użyć [domyślnego wyrażenia wartości](../operators/default.md) , aby utworzyć wartość domyślną typu.

Jeśli wszystkie pola wystąpienia typu struktury są dostępne, można również utworzyć wystąpienie go bez `new` operatora. W takim przypadku należy zainicjować wszystkie pola wystąpienia przed pierwszym użyciem wystąpienia. Poniższy przykład pokazuje, jak to zrobić:

[!code-csharp[without new](snippets/shared/StructType.cs#WithoutNew)]

W przypadku [wbudowanych typów wartości](value-types.md#built-in-value-types)Użyj odpowiednich literałów, aby określić wartość typu.

## <a name="passing-structure-type-variables-by-reference"></a>Przekazywanie zmiennych typu struktury przez odwołanie

W przypadku przekazania zmiennej typu struktury do metody jako argumentu lub zwrócenia wartości typu struktury z metody, kopiowane jest całe wystąpienie typu struktury. To może mieć wpływ na wydajność kodu w scenariuszach o wysokiej wydajności, które obejmują duże typy struktury. Można uniknąć kopiowania wartości przez przekazanie zmiennej typu struktury przez odwołanie. Użyj [`ref`](../keywords/ref.md#passing-an-argument-by-reference) [`out`](../keywords/out-parameter-modifier.md) [`in`](../keywords/in-parameter-modifier.md) modyfikatorów parametrów,, lub metody, aby wskazać, że argument musi być przekazaniem przez odwołanie. Użyj funkcji [ref](../../programming-guide/classes-and-structs/ref-returns.md) Returns, aby zwrócić wynik metody przez odwołanie. Aby uzyskać więcej informacji, zobacz [Zapisywanie bezpiecznego i wydajnego kodu w języku C#](../../write-safe-efficient-code.md).

## <a name="ref-struct"></a>`ref` konstrukcja

Począwszy od języka C# 7,2, można użyć `ref` modyfikatora w deklaracji typu struktury. Wystąpienia `ref` typu struktury są przydzielane na stosie i nie można wyjść do sterty zarządzanej. W celu zapewnienia, że kompilator ogranicza użycie `ref` typów struktur w następujący sposób:

- `ref`Struktura nie może być typem elementu tablicy.
- `ref`Struktura nie może być zadeklarowanym typem pola klasy lub bez `ref` struktury.
- `ref`Struktura nie może implementować interfejsów.
- `ref`Struktura nie może być opakowana do <xref:System.ValueType?displayProperty=nameWithType> ani <xref:System.Object?displayProperty=nameWithType> .
- `ref`Struktura nie może być argumentem typu.
- `ref`Nie można przechwycić zmiennej struktury za pomocą [wyrażenia lambda](../operators/lambda-expressions.md) lub [funkcji lokalnej](../../programming-guide/classes-and-structs/local-functions.md).
- `ref`Zmienna struktury nie może być używana w [`async`](../keywords/async.md) metodzie. Można jednak używać `ref` zmiennych struktury w metodach synchronicznych, na przykład w tych, które zwracają <xref:System.Threading.Tasks.Task> lub <xref:System.Threading.Tasks.Task%601> .
- `ref`Zmienna struktury nie może być używana w [iteratorach](../../iterators.md).

Typowo, należy zdefiniować `ref` Typ struktury, gdy potrzebny jest również element członkowski danych `ref` typów struktury:

[!code-csharp[ref struct](snippets/shared/StructType.cs#RefStruct)]

Aby zadeklarować `ref` strukturę jako [`readonly`](#readonly-struct) , Połącz `readonly` `ref` modyfikatory i w deklaracji typu ( `readonly` modyfikator musi występować przed `ref` modyfikatorem):

[!code-csharp[readonly ref struct](snippets/shared/StructType.cs#ReadonlyRef)]

W programie .NET przykłady `ref` struktury są <xref:System.Span%601?displayProperty=nameWithType> i <xref:System.ReadOnlySpan%601?displayProperty=nameWithType> .

## <a name="struct-constraint"></a>ograniczenie struktury

Możesz również użyć `struct` słowa kluczowego w [ `struct` ograniczeniu](../../programming-guide/generics/constraints-on-type-parameters.md) , aby określić, że parametr typu jest typem wartości niedopuszczający wartości null. Zarówno struktura, jak i typy [wyliczeniowe](enum.md) spełniają `struct` warunek ograniczenia.

## <a name="conversions"></a>Konwersje

Dla dowolnego typu struktury (z wyjątkiem typów [ `ref` struktury](#ref-struct) ) istnieje konwersja [opakowania i rozpakowywanie](../../programming-guide/types/boxing-and-unboxing.md) do i z <xref:System.ValueType?displayProperty=nameWithType> <xref:System.Object?displayProperty=nameWithType> typów i. Istnieje również możliwość pakowania i rozpakowywania konwersji między typem struktury i dowolnym interfejsem, który implementuje.

## <a name="c-language-specification"></a>specyfikacja języka C#

Aby uzyskać więcej informacji, zobacz sekcję [struktury](~/_csharplang/spec/structs.md) w [specyfikacji języka C#](~/_csharplang/spec/introduction.md).

Aby uzyskać więcej informacji o funkcjach wprowadzonych w języku C# 7,2 i nowszych, zobacz następujące uwagi dotyczące propozycji funkcji:

- [Struktury tylko do odczytu](~/_csharplang/proposals/csharp-7.2/readonly-ref.md#readonly-structs)
- [Elementy członkowskie wystąpień tylko do odczytu](~/_csharplang/proposals/csharp-8.0/readonly-instance-members.md)
- [Bezpieczeństwo czasu kompilowania dla typów zbliżonych do odwołań](~/_csharplang/proposals/csharp-7.2/span-safety.md)

## <a name="see-also"></a>Zobacz także

- [Dokumentacja języka C#](../index.md)
- [Wytyczne dotyczące projektowania — wybór między klasą a strukturą](../../../standard/design-guidelines/choosing-between-class-and-struct.md)
- [Wytyczne dotyczące projektowania — projekt struktury](../../../standard/design-guidelines/struct.md)
- [Klasy i struktury](../../programming-guide/classes-and-structs/index.md)
