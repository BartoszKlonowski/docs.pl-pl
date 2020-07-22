---
title: 'Instrukcje: Definiowanie metody ogólnej przy użyciu emisji odbicia'
description: Zdefiniuj metodę rodzajową przy użyciu emisji odbicia. Jeden przykład tworzy metodę rodzajową z dwoma parametrami typu. Drugi przykład pokazuje, jak emitować treść metody.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- generics [.NET Framework], reflection emit
- reflection emit, generic methods
- generics [.NET Framework], dynamic types
ms.assetid: 93892fa4-90b3-4ec4-b147-4bec9880de2b
ms.openlocfilehash: 3b85fb480e5862daa3b2800f75392adbe92348f2
ms.sourcegitcommit: 3d84eac0818099c9949035feb96bbe0346358504
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/21/2020
ms.locfileid: "86865141"
---
# <a name="how-to-define-a-generic-method-with-reflection-emit"></a>Instrukcje: Definiowanie metody ogólnej przy użyciu emisji odbicia

Pierwsza procedura pokazuje, jak utworzyć prostą metodę rodzajową z dwoma parametrami typu i jak zastosować ograniczenia klas, ograniczenia interfejsu i specjalne ograniczenia do parametrów typu.

Druga procedura pokazuje, jak emitować treść metody i jak używać parametrów typu metody generycznej do tworzenia wystąpień typów ogólnych i wywoływania ich metod.

Trzecia procedura pokazuje, jak wywołać metodę rodzajową.

> [!IMPORTANT]
> Metoda nie jest typowa, ponieważ należy do typu ogólnego i używa parametrów typu tego typu. Metoda jest generyczna tylko wtedy, gdy ma własną listę parametrów typu. Metoda generyczna może być wyświetlana w nieogólnym typie, jak w tym przykładzie. Przykład niegenerycznej metody w typie ogólnym można znaleźć w temacie [How to: define The Generic Type with Reodbicie](how-to-define-a-generic-type-with-reflection-emit.md).

### <a name="to-define-a-generic-method"></a>Aby zdefiniować metodę rodzajową

1. Przed rozpoczęciem warto zapoznać się z sposobem wyświetlania metody ogólnej podczas pisania przy użyciu języka wysokiego poziomu. Poniższy kod jest zawarty w przykładowym kodzie dla tego tematu wraz z kodem do wywołania metody ogólnej. Metoda ma dwa parametry typu, `TInput` a `TOutput` drugi, który musi być typem referencyjnym ( `class` ), musi mieć Konstruktor bez parametrów ( `new` ) i musi implementować `ICollection(Of TInput)` ( `ICollection<TInput>` w języku C#). To ograniczenie interfejsu zapewnia, że <xref:System.Collections.Generic.ICollection%601.Add%2A?displayProperty=nameWithType> Metoda może być używana do dodawania elementów do `TOutput` kolekcji, którą tworzy Metoda. Metoda ma jeden parametr formalny, `input` , który jest tablicą `TInput` . Metoda tworzy kolekcję typu `TOutput` i Kopiuje elementy `input` do kolekcji.

    [!code-csharp[GenericMethodHowTo#20](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#20)]
    [!code-vb[GenericMethodHowTo#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#20)]

2. Zdefiniuj zestaw dynamiczny i moduł dynamiczny, aby zawierały typ, do którego należy Metoda ogólna. W tym przypadku zestaw ma tylko jeden moduł o nazwie `DemoMethodBuilder1` , a nazwa modułu jest taka sama jak nazwa zestawu i rozszerzenie. W tym przykładzie zestaw jest zapisywany na dysku, a także wykonywany, więc <xref:System.Reflection.Emit.AssemblyBuilderAccess.RunAndSave?displayProperty=nameWithType> został określony. Za pomocą [Ildasm.exe (Il dezasembler)](../tools/ildasm-exe-il-disassembler.md) można przeanalizować DemoMethodBuilder1.dll i porównać ją z językiem pośrednim firmy Microsoft (MSIL) dla metody pokazanej w kroku 1.

    [!code-csharp[GenericMethodHowTo#2](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#2)]
    [!code-vb[GenericMethodHowTo#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#2)]

3. Zdefiniuj typ, do którego należy Metoda ogólna. Typ nie musi być ogólny. Metoda generyczna może należeć do typu ogólnego lub nieogólnego. W tym przykładzie typ jest klasą, nie jest rodzajowy i ma nazwę `DemoType` .

    [!code-csharp[GenericMethodHowTo#3](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#3)]
    [!code-vb[GenericMethodHowTo#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#3)]

4. Zdefiniuj metodę rodzajową. Jeśli typy parametrów formalnych metody ogólnej są określone przez parametry typu ogólnego metody ogólnej, użyj <xref:System.Reflection.Emit.TypeBuilder.DefineMethod%28System.String%2CSystem.Reflection.MethodAttributes%29> przeciążenia metody, aby zdefiniować metodę. Parametry typu ogólnego metody nie są jeszcze zdefiniowane, dlatego nie można określić typów parametrów formalnych metody w wywołaniu <xref:System.Reflection.Emit.TypeBuilder.DefineMethod%2A> . W tym przykładzie metoda ma nazwę `Factory` . Metoda jest publiczna i `static` ( `Shared` w Visual Basic).

    [!code-csharp[GenericMethodHowTo#4](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#4)]
    [!code-vb[GenericMethodHowTo#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#4)]

5. Zdefiniuj parametry typu ogólnego, `DemoMethod` przekazując tablicę ciągów zawierających nazwy parametrów do <xref:System.Reflection.Emit.MethodBuilder.DefineGenericParameters%2A?displayProperty=nameWithType> metody. Dzięki temu Metoda jest metodą rodzajową. Poniższy kod tworzy `Factory` metodę rodzajową z parametrami typu `TInput` i `TOutput` . Aby ułatwić odczytywanie kodu, zmienne z tymi nazwami są tworzone w celu przechowywania <xref:System.Reflection.Emit.GenericTypeParameterBuilder> obiektów reprezentujących dwa parametry typu.

    [!code-csharp[GenericMethodHowTo#5](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#5)]
    [!code-vb[GenericMethodHowTo#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#5)]

6. Opcjonalnie Dodaj specjalne ograniczenia do parametrów typu. Specjalne ograniczenia są dodawane za pomocą <xref:System.Reflection.Emit.GenericTypeParameterBuilder.SetGenericParameterAttributes%2A> metody. W tym przykładzie `TOutput` jest ograniczone jako typ referencyjny i ma konstruktora bez parametrów.

    [!code-csharp[GenericMethodHowTo#6](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#6)]
    [!code-vb[GenericMethodHowTo#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#6)]

7. Opcjonalnie dodaj ograniczenia klas i interfejsów do parametrów typu. W tym przykładzie parametr typu `TOutput` jest ograniczony do typów, które implementują `ICollection(Of TInput)` `ICollection<TInput>` interfejs (w języku C#). Dzięki temu <xref:System.Collections.Generic.ICollection%601.Add%2A> Metoda może być używana do dodawania elementów.

    [!code-csharp[GenericMethodHowTo#7](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#7)]
    [!code-vb[GenericMethodHowTo#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#7)]

8. Zdefiniuj parametry formalne metody przy użyciu <xref:System.Reflection.Emit.MethodBuilder.SetParameters%2A> metody. W tym przykładzie `Factory` Metoda ma jeden parametr, tablicę `TInput` . Ten typ jest tworzony przez wywołanie <xref:System.Type.MakeArrayType%2A> metody <xref:System.Reflection.Emit.GenericTypeParameterBuilder> , która reprezentuje `TInput` . Argument <xref:System.Reflection.Emit.MethodBuilder.SetParameters%2A> jest tablicą <xref:System.Type> obiektów.

    [!code-csharp[GenericMethodHowTo#8](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#8)]
    [!code-vb[GenericMethodHowTo#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#8)]

9. Zdefiniuj typ zwracany dla metody przy użyciu <xref:System.Reflection.Emit.MethodBuilder.SetReturnType%2A> metody. W tym przykładzie jest zwracane wystąpienie elementu `TOutput` .

    [!code-csharp[GenericMethodHowTo#9](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#9)]
    [!code-vb[GenericMethodHowTo#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#9)]

10. Emituj treść metody przy użyciu <xref:System.Reflection.Emit.ILGenerator> . Aby uzyskać szczegółowe informacje, zobacz towarzysząca procedura emitowania treści metody.

    > [!IMPORTANT]
    > Gdy emitują wywołania do metod typów ogólnych, a argumenty typu tych typów są parametrami typu metody generycznej, należy użyć `static` <xref:System.Reflection.Emit.TypeBuilder.GetConstructor%28System.Type%2CSystem.Reflection.ConstructorInfo%29> , <xref:System.Reflection.Emit.TypeBuilder.GetMethod%28System.Type%2CSystem.Reflection.MethodInfo%29> i <xref:System.Reflection.Emit.TypeBuilder.GetField%28System.Type%2CSystem.Reflection.FieldInfo%29> przeciążania metody <xref:System.Reflection.Emit.TypeBuilder> klasy, aby uzyskać skonstruowane formularze metod. Procedura towarzysząca do emitowania treści metody pokazuje to.

11. Wypełnij typ, który zawiera metodę i Zapisz zestaw. Towarzysząca procedura wywoływania metody generycznej pokazuje dwa sposoby wywołania ukończonej metody.

    [!code-csharp[GenericMethodHowTo#14](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#14)]
    [!code-vb[GenericMethodHowTo#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#14)]

<a name="procedureSection1"></a>

### <a name="to-emit-the-method-body"></a>Aby emitować treść metody

1. Pobierz generator kodu i Zadeklaruj zmienne lokalne i etykiety. <xref:System.Reflection.Emit.ILGenerator.DeclareLocal%2A>Metoda jest używana do deklarowania zmiennych lokalnych. `Factory`Metoda ma cztery zmienne lokalne: `retVal` Aby przechowywać nowe, `TOutput` które są zwracane przez metodę, `ic` do przechowywania, `TOutput` gdy jest rzutowane na `ICollection(Of TInput)` ( `ICollection<TInput>` w języku C#), `input` do przechowywania wejściowej tablicy `TInput` obiektów oraz `index` do iteracji przez tablicę. Metoda ma również dwie etykiety, jeden do wprowadzenia pętli ( `enterLoop` ) i jeden dla górnej części pętli ( `loopAgain` ), zdefiniowany za pomocą <xref:System.Reflection.Emit.ILGenerator.DefineLabel%2A> metody.

    Pierwszym krokiem jest załadowanie przez metodę argumentu przy użyciu <xref:System.Reflection.Emit.OpCodes.Ldarg_0> kodu operacji i zapisanie go w zmiennej lokalnej `input` przy użyciu <xref:System.Reflection.Emit.OpCodes.Stloc_S> opcode.

    [!code-csharp[GenericMethodHowTo#10](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#10)]
    [!code-vb[GenericMethodHowTo#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#10)]

2. Emituj kod, aby utworzyć wystąpienie `TOutput` , przy użyciu metody ogólnego przeciążenia metody <xref:System.Activator.CreateInstance%2A?displayProperty=nameWithType> . Użycie tego przeciążenia wymaga, aby określony typ miał Konstruktor bez parametrów, który jest przyczyną dodania tego ograniczenia do `TOutput` . Utwórz utworzoną metodę rodzajową, przekazując `TOutput` do <xref:System.Reflection.MethodInfo.MakeGenericMethod%2A> . Po emisji kodu do wywołania metody, Emituj kod, aby zapisać go w zmiennej lokalnej `retVal` przy użyciu<xref:System.Reflection.Emit.OpCodes.Stloc_S>

    [!code-csharp[GenericMethodHowTo#11](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#11)]
    [!code-vb[GenericMethodHowTo#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#11)]

3. Emituj kod, aby wykonać rzutowanie nowego `TOutput` obiektu `ICollection(Of TInput)` i zapisać go w zmiennej lokalnej `ic` .

    [!code-csharp[GenericMethodHowTo#31](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#31)]
    [!code-vb[GenericMethodHowTo#31](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#31)]

4. Uzyskaj <xref:System.Reflection.MethodInfo> reprezentowanie <xref:System.Collections.Generic.ICollection%601.Add%2A?displayProperty=nameWithType> metody. Metoda działa na `ICollection(Of TInput)` ( `ICollection<TInput>` w języku C#), dlatego należy uzyskać `Add` metodę specyficzną dla tego konstruowanego typu. Nie można użyć <xref:System.Type.GetMethod%2A> metody, aby uzyskać tę <xref:System.Reflection.MethodInfo> samą wartość bezpośrednio z `icollOfTInput` , ponieważ <xref:System.Type.GetMethod%2A> nie jest ona obsługiwana dla typu, który został skonstruowany przy użyciu <xref:System.Reflection.Emit.GenericTypeParameterBuilder> . Zamiast tego należy wywołać metodę <xref:System.Type.GetMethod%2A> `icoll` , która zawiera definicję typu ogólnego dla <xref:System.Collections.Generic.ICollection%601> interfejsu generycznego. Następnie użyj <xref:System.Reflection.Emit.TypeBuilder.GetMethod%28System.Type%2CSystem.Reflection.MethodInfo%29> `static` metody, aby utworzyć <xref:System.Reflection.MethodInfo> dla konstruowanego typu. Poniższy kod ilustruje to.

    [!code-csharp[GenericMethodHowTo#12](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#12)]
    [!code-vb[GenericMethodHowTo#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#12)]

5. Emituj kod, aby zainicjować `index` zmienną, ładując 32-bitową liczbę całkowitą 0 i przechowując ją w zmiennej. Emituj kod do gałęzi do etykiety `enterLoop` . Ta etykieta nie została jeszcze oznaczona, ponieważ znajduje się wewnątrz pętli. Kod dla pętli jest emitowany w następnym kroku.

    [!code-csharp[GenericMethodHowTo#32](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#32)]
    [!code-vb[GenericMethodHowTo#32](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#32)]

6. Emituj kod dla pętli. Pierwszym krokiem jest oznaczenie górnej części pętli przez wywołanie <xref:System.Reflection.Emit.ILGenerator.MarkLabel%2A> z `loopAgain` etykietą. Instrukcje rozgałęzienia, które używają etykiety, będą teraz rozgałęziać do tego punktu w kodzie. Następnym krokiem jest wypchnięcie `TOutput` obiektu, przerzutowanie do `ICollection(Of TInput)` , na stos. Nie jest on konieczny od razu, ale musi być w pozycji do wywołania `Add` metody. Następna Tablica wejściowa jest wypychana do stosu, a następnie `index` zmiennej zawierającej bieżący indeks do tablicy. <xref:System.Reflection.Emit.OpCodes.Ldelem>Kod operacji pokazuje indeks i tablicę na stosie i wypchnięcie elementu tablicy indeksowanej na stos. Stos jest teraz gotowy do wywołania <xref:System.Collections.Generic.ICollection%601.Add%2A?displayProperty=nameWithType> metody, która wskazuje kolekcję i nowy element poza stos i dodaje element do kolekcji.

    Pozostała część kodu w pętli zwiększa indeks i testy, aby sprawdzić, czy pętla została zakończona: indeks i 32-bitową liczbę całkowitą 1 są wypychane na stos i dodawane, pozostawiając sumę na stosie; suma jest przechowywana w `index` . <xref:System.Reflection.Emit.ILGenerator.MarkLabel%2A>jest wywoływana, aby ustawić ten punkt jako punkt wejścia dla pętli. Indeks zostanie ponownie załadowany. Tablica wejściowa jest wypychana na stosie i <xref:System.Reflection.Emit.OpCodes.Ldlen> emitowana w celu uzyskania jej długości. Indeks i długość są teraz na stosie i <xref:System.Reflection.Emit.OpCodes.Clt> są emitowane w celu ich porównania. Jeśli indeks jest krótszy niż długość, <xref:System.Reflection.Emit.OpCodes.Brtrue_S> odgałęzienia odnoszą się do początku pętli.

    [!code-csharp[GenericMethodHowTo#13](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#13)]
    [!code-vb[GenericMethodHowTo#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#13)]

7. Emituj kod, aby wypchnąć `TOutput` obiekt na stos i zwrócić z metody. Zmienne lokalne `retVal` i `ic` oba zawierają odwołania do nowego `TOutput` ; `ic` są używane tylko w celu uzyskania dostępu do <xref:System.Collections.Generic.ICollection%601.Add%2A?displayProperty=nameWithType> metody.

    [!code-csharp[GenericMethodHowTo#33](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#33)]
    [!code-vb[GenericMethodHowTo#33](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#33)]

<a name="procedureSection2"></a>

### <a name="to-invoke-the-generic-method"></a>Aby wywołać metodę rodzajową

1. `Factory`jest definicją metody ogólnej. Aby można było go wywołać, należy przypisać typy do jego parametrów typu ogólnego. Użyj <xref:System.Reflection.MethodInfo.MakeGenericMethod%2A> metody, aby to zrobić. Poniższy kod tworzy skonstruowaną metodę rodzajową, określając <xref:System.String> dla `TInput` i `List(Of String)` ( `List<string>` w języku C#) dla `TOutput` , i wyświetla reprezentację ciągu dla metody.

    [!code-csharp[GenericMethodHowTo#21](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#21)]
    [!code-vb[GenericMethodHowTo#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#21)]

2. Aby wywołać metodę z późnym wiązaniem, użyj <xref:System.Reflection.MethodBase.Invoke%2A> metody. Poniższy kod tworzy tablicę <xref:System.Object> zawierającą jako tylko element tablicy ciągów i przekazuje ją jako listę argumentów dla metody ogólnej. Pierwszy parametr <xref:System.Reflection.MethodBase.Invoke%2A> jest odwołaniem o wartości null, ponieważ metoda jest `static` . Wartość zwracana jest rzutowana na `List(Of String)` , a jej pierwszy element jest wyświetlany.

    [!code-csharp[GenericMethodHowTo#22](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#22)]
    [!code-vb[GenericMethodHowTo#22](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#22)]

3. Aby wywołać metodę przy użyciu delegata, musisz mieć delegata, który jest zgodny z podpisem skonstruowanej metody ogólnej. Prostym sposobem jest utworzenie delegata ogólnego. Poniższy kod tworzy wystąpienie delegata generycznego `D` zdefiniowanego w przykładowym kodzie przy użyciu <xref:System.Delegate.CreateDelegate%28System.Type%2CSystem.Reflection.MethodInfo%29?displayProperty=nameWithType> przeciążenia metody i wywołuje delegata. Delegaty są wykonywane lepiej niż wywołania z późnym wiązaniem.

    [!code-csharp[GenericMethodHowTo#23](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#23)]
    [!code-vb[GenericMethodHowTo#23](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#23)]

4. Emitowana Metoda może być również wywołana z programu, który odwołuje się do zapisanego zestawu.

## <a name="example"></a>Przykład

Poniższy przykład kodu tworzy typ nieogólny, `DemoType` przy użyciu metody ogólnej `Factory` . Ta metoda ma dwa parametry typu ogólnego, `TInput` Aby określić typ danych wejściowych i `TOutput` określić typ danych wyjściowych. `TOutput`Parametr typu jest ograniczony do implementacji `ICollection<TInput>` ( `ICollection(Of TInput)` w Visual Basic), jako typ referencyjny i ma Konstruktor bez parametrów.

Metoda ma jeden parametr formalny, który jest tablicą `TInput` . Metoda zwraca wystąpienie `TOutput` , które zawiera wszystkie elementy tablicy wejściowej. `TOutput`może to być dowolny typ kolekcji ogólnej implementującej <xref:System.Collections.Generic.ICollection%601> interfejs generyczny.

Gdy kod jest wykonywany, zestaw dynamiczny jest zapisywany jako DemoGenericMethod1.dll i można go sprawdzić przy użyciu [Ildasm.exe (Il dezasembler)](../tools/ildasm-exe-il-disassembler.md).

> [!NOTE]
> Dobrym sposobem, aby dowiedzieć się, jak emitować kod, napisać Visual Basic, C# lub Visual C++ program wykonujący zadanie, które próbujesz emitować, i użyć dezasembler do sprawdzenia MSIL utworzonego przez kompilator.

Przykład kodu zawiera kod źródłowy, który jest odpowiednikiem emitowanej metody. Emitowana Metoda jest wywoływana z późnym wiązaniem, a także przy użyciu ogólnego delegata zadeklarowanego w przykładzie kodu.

[!code-csharp[GenericMethodHowTo#1](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#1)]
[!code-vb[GenericMethodHowTo#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#1)]

## <a name="see-also"></a>Zobacz także

- <xref:System.Reflection.Emit.MethodBuilder>
- [Instrukcje: Definiowanie typu ogólnego przy użyciu emisji odbicia](how-to-define-a-generic-type-with-reflection-emit.md)
