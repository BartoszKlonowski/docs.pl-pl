---
title: Źródło zdarzenia BinaryFormatter
description: Dowiedz się, jak używać źródła zdarzeń BinaryFormatter do rejestrowania podczas serializacji lub deserializacji.
ms.date: 12/03/2020
ms.author: levib
author: GrabYourPitchforks
ms.openlocfilehash: 9ae2af77b6cfc270207fb0f2969ada8c2eca1153
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740421"
---
# <a name="binaryformatter-event-source"></a>Źródło zdarzenia BinaryFormatter

Począwszy od platformy .NET 5,0, <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> zawiera wbudowaną, <xref:System.Diagnostics.Tracing.EventSource> która daje wgląd w kiedy występuje Serializacja lub deserializacja obiektu. Aplikacje mogą używać <xref:System.Diagnostics.Tracing.EventListener> typów pochodnych do nasłuchiwania tych powiadomień i rejestrowania ich.

Ta funkcja nie jest zamiennikiem <xref:System.Runtime.Serialization.SerializationBinder> ani <xref:System.Runtime.Serialization.ISerializationSurrogate> i nie może służyć do modyfikowania danych, które są serializowane lub deserializowane. Ten system zdarzeń jest raczej przeznaczony do zapewnienia wglądu w typy, które są serializowane lub deserializowane. Może również służyć do wykrywania niezamierzonych wywołań do `BinaryFormatter` infrastruktury, takich jak wywołania pochodzące z kodu biblioteki innej firmy.

## <a name="description-of-events"></a>Opis zdarzeń

`BinaryFormatter`Źródło zdarzenia ma dobrze znaną nazwę `System.Runtime.Serialization.Formatters.Binary.BinaryFormatterEventSource` . Odbiorniki mogą subskrybować 6 zdarzeń.

### <a name="serializationstart-event-id--10"></a>Zdarzenie SerializationStart (ID = `10` )

Uruchamiany, gdy został <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Serialize%2A?displayProperty=nameWithType> wywołany i rozpoczął proces serializacji. To zdarzenie jest sparowane ze `SerializationEnd` zdarzeniem. `SerializationStart`Zdarzenie może być wywoływane cyklicznie, jeśli obiekt wywołuje `BinaryFormatter.Serialize` w ramach własnej procedury serializacji.

To zdarzenie nie zawiera ładunku.

### <a name="serializationend-event-id--11"></a>Zdarzenie SerializationEnd (ID = `11` )

Uruchamiany po `BinaryFormatter.Serialize` zakończeniu pracy. Każde wystąpienie `SerializationEnd` oznacza zakończenie ostatniego niesparowanego `SerializationStart` zdarzenia.

To zdarzenie nie zawiera ładunku.

### <a name="serializingobject-event-id--12"></a>Zdarzenie SerializingObject (ID = `12` )

Uruchamiany, gdy `BinaryFormatter.Serialize` jest w trakcie serializacji typu niepierwotnego. `BinaryFormatter`Specjalne przypadki infrastruktury określone typy (takie jak `string` i `int` ) i nie zgłaszają tego zdarzenia w przypadku napotkania tych typów. To zdarzenie jest zgłaszane dla typów zdefiniowanych przez użytkownika i innych typów, które `BinaryFormatter` nie są natywnie zrozumiałe.

To zdarzenie może być zgłoszone zero lub więcej razy między `SerializationStart` i `SerializationEnd` zdarzeniami.

To zdarzenie zawiera ładunek z jednym argumentem:

* `typeName` ( `string` ): Kwalifikowana nazwa zestawu (zobacz <xref:System.Type.AssemblyQualifiedName?displayProperty=nameWithType> ) typu, który jest serializowany.

### <a name="deserializationstart-event-id--20"></a>Zdarzenie DeserializationStart (ID = `20` )

Uruchamiany, gdy został <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize%2A?displayProperty=nameWithType> wywołany i rozpoczął proces deserializacji. To zdarzenie jest sparowane ze `DeserializationEnd` zdarzeniem. `DeserializationStart`Zdarzenie może być wywoływane cyklicznie, jeśli obiekt wywołuje `BinaryFormatter.Deserialize` w ramach własnej procedury deserializacji.

To zdarzenie nie zawiera ładunku.

### <a name="deserializationend-event-id--21"></a>Zdarzenie DeserializationEnd (ID = `21` )

Uruchamiany po `BinaryFormatter.Deserialize` zakończeniu pracy. Każde wystąpienie `DeserializationEnd` oznacza zakończenie ostatniego niesparowanego `DeserializationStart` zdarzenia.

To zdarzenie nie zawiera ładunku.

### <a name="deserializingobject-event-id--22"></a>Zdarzenie DeserializingObject (ID = `22` )

Uruchamiany, gdy `BinaryFormatter.Deserialize` jest w trakcie deserializacji niepierwotnego typu. `BinaryFormatter`Specjalne przypadki infrastruktury określone typy (takie jak `string` i `int` ) i nie zgłaszają tego zdarzenia w przypadku napotkania tych typów. To zdarzenie jest zgłaszane dla typów zdefiniowanych przez użytkownika i innych typów, które `BinaryFormatter` nie są natywnie zrozumiałe.

To zdarzenie może być zgłoszone zero lub więcej razy między `DeserializationStart` i `DeserializationEnd` zdarzeniami.

To zdarzenie zawiera ładunek z jednym argumentem.

* `typeName` ( `string` ): Kwalifikowana nazwa zestawu (zobacz <xref:System.Type.AssemblyQualifiedName?displayProperty=nameWithType> ) deserializowany typ.

### <a name="advanced-subscribing-to-a-subset-of-notifications"></a>\[Zaawansowana \] subskrypcja podzbioru powiadomień

Detektory, którzy chcą subskrybować tylko podzestaw powiadomień, mogą wybrać słowa kluczowe do włączenia.

* `Serialization` = `(EventKeywords)1`: Wywołuje `SerializationStart` zdarzenia, `SerializationEnd` i `SerializingObject` .
* `Deserialization` = `(EventKeywords)2`: Wywołuje `DeserializationStart` zdarzenia, `DeserializationEnd` i `DeserializingObject` .

Jeśli podczas rejestrowania nie są dostępne żadne filtry słów kluczowych `EventListener` , zostaną zgłoszone wszystkie zdarzenia.

Aby uzyskać więcej informacji, zobacz <xref:System.Diagnostics.Tracing.EventKeywords?displayProperty=nameWithType>.

## <a name="sample-code"></a>Przykładowy kod

Następujący kod:

- tworzy `EventListener` Typ pochodny, który zapisuje w `System.Console` ,
- subskrybuje `BinaryFormatter` wygenerowane powiadomienia,
- serializować i deserializacji prostego grafu obiektów przy użyciu `BinaryFormatter` , i
- analizuje zdarzenia, które zostały zgłoszone.

:::code language="csharp" source="snippets/binaryformatter-event-source/csharp/Program.cs":::

Poprzedni kod generuje dane wyjściowe podobne do następującego przykładu:

```output
Event SerializationStart (id=10) received.
Event SerializingObject (id=12) received.
typeName = BinaryFormatterEventSample.Person, BinaryFormatterEventSample, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null
Event SerializingObject (id=12) received.
typeName = BinaryFormatterEventSample.Book, BinaryFormatterEventSample, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null
Event SerializationStop (id=11) received.
Event DeserializationStart (id=20) received.
Event DeserializingObject (id=22) received.
typeName = BinaryFormatterEventSample.Person, BinaryFormatterEventSample, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null
Event DeserializingObject (id=22) received.
typeName = BinaryFormatterEventSample.Book, BinaryFormatterEventSample, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null
Event DeserializationStop (id=21) received.
Rehydrated person Logan Edwards
Favorite book: A Tale of Two Cities by Charles Dickens, list price 10.25
```

W tym przykładzie dzienników opartych na konsoli, `EventListener` których Serializacja zaczyna się, wystąpienia `Person` i `Book` są serializowane, a następnie zakończenie serializacji. Podobnie po rozpoczęciu deserializacji wystąpienia `Person` i `Book` są deserializowane, a następnie ukończono deserializacji.

Następnie aplikacja drukuje wartości zawarte w deserializacji, `Person` Aby wykazać, że obiekt został prawidłowo Zserializowany i deserializacji.

## <a name="see-also"></a>Zobacz także

Aby uzyskać więcej informacji na temat korzystania `EventListener` z powiadomień na temat odbierania `EventSource` , zobacz [ `EventListener` Klasa](xref:System.Diagnostics.Tracing.EventListener).
