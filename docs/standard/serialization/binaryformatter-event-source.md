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
# <a name="binaryformatter-event-source"></a><span data-ttu-id="8d465-103">Źródło zdarzenia BinaryFormatter</span><span class="sxs-lookup"><span data-stu-id="8d465-103">BinaryFormatter event source</span></span>

<span data-ttu-id="8d465-104">Począwszy od platformy .NET 5,0, <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> zawiera wbudowaną, <xref:System.Diagnostics.Tracing.EventSource> która daje wgląd w kiedy występuje Serializacja lub deserializacja obiektu.</span><span class="sxs-lookup"><span data-stu-id="8d465-104">Starting with .NET 5.0, <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> includes a built-in <xref:System.Diagnostics.Tracing.EventSource> that gives you visibility into when an object serialization or deserialization is occurring.</span></span> <span data-ttu-id="8d465-105">Aplikacje mogą używać <xref:System.Diagnostics.Tracing.EventListener> typów pochodnych do nasłuchiwania tych powiadomień i rejestrowania ich.</span><span class="sxs-lookup"><span data-stu-id="8d465-105">Apps can use <xref:System.Diagnostics.Tracing.EventListener>-derived types to listen for these notifications and log them.</span></span>

<span data-ttu-id="8d465-106">Ta funkcja nie jest zamiennikiem <xref:System.Runtime.Serialization.SerializationBinder> ani <xref:System.Runtime.Serialization.ISerializationSurrogate> i nie może służyć do modyfikowania danych, które są serializowane lub deserializowane.</span><span class="sxs-lookup"><span data-stu-id="8d465-106">This functionality is not a substitute for a <xref:System.Runtime.Serialization.SerializationBinder> or an <xref:System.Runtime.Serialization.ISerializationSurrogate> and can't be used to modify the data being serialized or deserialized.</span></span> <span data-ttu-id="8d465-107">Ten system zdarzeń jest raczej przeznaczony do zapewnienia wglądu w typy, które są serializowane lub deserializowane.</span><span class="sxs-lookup"><span data-stu-id="8d465-107">Rather, this eventing system is intended to provide insight into the types being serialized or deserialized.</span></span> <span data-ttu-id="8d465-108">Może również służyć do wykrywania niezamierzonych wywołań do `BinaryFormatter` infrastruktury, takich jak wywołania pochodzące z kodu biblioteki innej firmy.</span><span class="sxs-lookup"><span data-stu-id="8d465-108">It can also be used to detect unintended calls into the `BinaryFormatter` infrastructure, such as calls originating from third-party library code.</span></span>

## <a name="description-of-events"></a><span data-ttu-id="8d465-109">Opis zdarzeń</span><span class="sxs-lookup"><span data-stu-id="8d465-109">Description of events</span></span>

<span data-ttu-id="8d465-110">`BinaryFormatter`Źródło zdarzenia ma dobrze znaną nazwę `System.Runtime.Serialization.Formatters.Binary.BinaryFormatterEventSource` .</span><span class="sxs-lookup"><span data-stu-id="8d465-110">The `BinaryFormatter` event source has the well-known name `System.Runtime.Serialization.Formatters.Binary.BinaryFormatterEventSource`.</span></span> <span data-ttu-id="8d465-111">Odbiorniki mogą subskrybować 6 zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="8d465-111">Listeners may subscribe to 6 events.</span></span>

### <a name="serializationstart-event-id--10"></a><span data-ttu-id="8d465-112">Zdarzenie SerializationStart (ID = `10` )</span><span class="sxs-lookup"><span data-stu-id="8d465-112">SerializationStart event (id = `10`)</span></span>

<span data-ttu-id="8d465-113">Uruchamiany, gdy został <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Serialize%2A?displayProperty=nameWithType> wywołany i rozpoczął proces serializacji.</span><span class="sxs-lookup"><span data-stu-id="8d465-113">Raised when <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Serialize%2A?displayProperty=nameWithType> has been called and has started the serialization process.</span></span> <span data-ttu-id="8d465-114">To zdarzenie jest sparowane ze `SerializationEnd` zdarzeniem.</span><span class="sxs-lookup"><span data-stu-id="8d465-114">This event is paired with the `SerializationEnd` event.</span></span> <span data-ttu-id="8d465-115">`SerializationStart`Zdarzenie może być wywoływane cyklicznie, jeśli obiekt wywołuje `BinaryFormatter.Serialize` w ramach własnej procedury serializacji.</span><span class="sxs-lookup"><span data-stu-id="8d465-115">The `SerializationStart` event can be called recursively if an object calls `BinaryFormatter.Serialize` within its own serialization routine.</span></span>

<span data-ttu-id="8d465-116">To zdarzenie nie zawiera ładunku.</span><span class="sxs-lookup"><span data-stu-id="8d465-116">This event doesn't contain a payload.</span></span>

### <a name="serializationend-event-id--11"></a><span data-ttu-id="8d465-117">Zdarzenie SerializationEnd (ID = `11` )</span><span class="sxs-lookup"><span data-stu-id="8d465-117">SerializationEnd event (id = `11`)</span></span>

<span data-ttu-id="8d465-118">Uruchamiany po `BinaryFormatter.Serialize` zakończeniu pracy.</span><span class="sxs-lookup"><span data-stu-id="8d465-118">Raised when `BinaryFormatter.Serialize` has completed its work.</span></span> <span data-ttu-id="8d465-119">Każde wystąpienie `SerializationEnd` oznacza zakończenie ostatniego niesparowanego `SerializationStart` zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="8d465-119">Each occurrence of `SerializationEnd` denotes the completion of the last unpaired `SerializationStart` event.</span></span>

<span data-ttu-id="8d465-120">To zdarzenie nie zawiera ładunku.</span><span class="sxs-lookup"><span data-stu-id="8d465-120">This event doesn't contain a payload.</span></span>

### <a name="serializingobject-event-id--12"></a><span data-ttu-id="8d465-121">Zdarzenie SerializingObject (ID = `12` )</span><span class="sxs-lookup"><span data-stu-id="8d465-121">SerializingObject event (id = `12`)</span></span>

<span data-ttu-id="8d465-122">Uruchamiany, gdy `BinaryFormatter.Serialize` jest w trakcie serializacji typu niepierwotnego.</span><span class="sxs-lookup"><span data-stu-id="8d465-122">Raised when `BinaryFormatter.Serialize` is in the process of serializing a non-primitive type.</span></span> <span data-ttu-id="8d465-123">`BinaryFormatter`Specjalne przypadki infrastruktury określone typy (takie jak `string` i `int` ) i nie zgłaszają tego zdarzenia w przypadku napotkania tych typów.</span><span class="sxs-lookup"><span data-stu-id="8d465-123">The `BinaryFormatter` infrastructure special-cases certain types (such as `string` and `int`) and doesn't raise this event when these types are encountered.</span></span> <span data-ttu-id="8d465-124">To zdarzenie jest zgłaszane dla typów zdefiniowanych przez użytkownika i innych typów, które `BinaryFormatter` nie są natywnie zrozumiałe.</span><span class="sxs-lookup"><span data-stu-id="8d465-124">This event is raised for user-defined types and other types that `BinaryFormatter` doesn't natively understand.</span></span>

<span data-ttu-id="8d465-125">To zdarzenie może być zgłoszone zero lub więcej razy między `SerializationStart` i `SerializationEnd` zdarzeniami.</span><span class="sxs-lookup"><span data-stu-id="8d465-125">This event may be raised zero or more times between `SerializationStart` and `SerializationEnd` events.</span></span>

<span data-ttu-id="8d465-126">To zdarzenie zawiera ładunek z jednym argumentem:</span><span class="sxs-lookup"><span data-stu-id="8d465-126">This event contains a payload with one argument:</span></span>

* <span data-ttu-id="8d465-127">`typeName` ( `string` ): Kwalifikowana nazwa zestawu (zobacz <xref:System.Type.AssemblyQualifiedName?displayProperty=nameWithType> ) typu, który jest serializowany.</span><span class="sxs-lookup"><span data-stu-id="8d465-127">`typeName` (`string`): The assembly-qualified name (see <xref:System.Type.AssemblyQualifiedName?displayProperty=nameWithType>) of the type being serialized.</span></span>

### <a name="deserializationstart-event-id--20"></a><span data-ttu-id="8d465-128">Zdarzenie DeserializationStart (ID = `20` )</span><span class="sxs-lookup"><span data-stu-id="8d465-128">DeserializationStart event (id = `20`)</span></span>

<span data-ttu-id="8d465-129">Uruchamiany, gdy został <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize%2A?displayProperty=nameWithType> wywołany i rozpoczął proces deserializacji.</span><span class="sxs-lookup"><span data-stu-id="8d465-129">Raised when <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize%2A?displayProperty=nameWithType> has been called and has started the deserialization process.</span></span> <span data-ttu-id="8d465-130">To zdarzenie jest sparowane ze `DeserializationEnd` zdarzeniem.</span><span class="sxs-lookup"><span data-stu-id="8d465-130">This event is paired with the `DeserializationEnd` event.</span></span> <span data-ttu-id="8d465-131">`DeserializationStart`Zdarzenie może być wywoływane cyklicznie, jeśli obiekt wywołuje `BinaryFormatter.Deserialize` w ramach własnej procedury deserializacji.</span><span class="sxs-lookup"><span data-stu-id="8d465-131">The `DeserializationStart` event can be called recursively if an object calls `BinaryFormatter.Deserialize` within its own deserialization routine.</span></span>

<span data-ttu-id="8d465-132">To zdarzenie nie zawiera ładunku.</span><span class="sxs-lookup"><span data-stu-id="8d465-132">This event doesn't contain a payload.</span></span>

### <a name="deserializationend-event-id--21"></a><span data-ttu-id="8d465-133">Zdarzenie DeserializationEnd (ID = `21` )</span><span class="sxs-lookup"><span data-stu-id="8d465-133">DeserializationEnd event (id = `21`)</span></span>

<span data-ttu-id="8d465-134">Uruchamiany po `BinaryFormatter.Deserialize` zakończeniu pracy.</span><span class="sxs-lookup"><span data-stu-id="8d465-134">Raised when `BinaryFormatter.Deserialize` has completed its work.</span></span> <span data-ttu-id="8d465-135">Każde wystąpienie `DeserializationEnd` oznacza zakończenie ostatniego niesparowanego `DeserializationStart` zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="8d465-135">Each occurrence of `DeserializationEnd` denotes the completion of the last unpaired `DeserializationStart` event.</span></span>

<span data-ttu-id="8d465-136">To zdarzenie nie zawiera ładunku.</span><span class="sxs-lookup"><span data-stu-id="8d465-136">This event doesn't contain a payload.</span></span>

### <a name="deserializingobject-event-id--22"></a><span data-ttu-id="8d465-137">Zdarzenie DeserializingObject (ID = `22` )</span><span class="sxs-lookup"><span data-stu-id="8d465-137">DeserializingObject event (id = `22`)</span></span>

<span data-ttu-id="8d465-138">Uruchamiany, gdy `BinaryFormatter.Deserialize` jest w trakcie deserializacji niepierwotnego typu.</span><span class="sxs-lookup"><span data-stu-id="8d465-138">Raised when `BinaryFormatter.Deserialize` is in the process of deserializing a non-primitive type.</span></span> <span data-ttu-id="8d465-139">`BinaryFormatter`Specjalne przypadki infrastruktury określone typy (takie jak `string` i `int` ) i nie zgłaszają tego zdarzenia w przypadku napotkania tych typów.</span><span class="sxs-lookup"><span data-stu-id="8d465-139">The `BinaryFormatter` infrastructure special-cases certain types (such as `string` and `int`) and doesn't raise this event when these types are encountered.</span></span> <span data-ttu-id="8d465-140">To zdarzenie jest zgłaszane dla typów zdefiniowanych przez użytkownika i innych typów, które `BinaryFormatter` nie są natywnie zrozumiałe.</span><span class="sxs-lookup"><span data-stu-id="8d465-140">This event is raised for user-defined types and other types that `BinaryFormatter` doesn't natively understand.</span></span>

<span data-ttu-id="8d465-141">To zdarzenie może być zgłoszone zero lub więcej razy między `DeserializationStart` i `DeserializationEnd` zdarzeniami.</span><span class="sxs-lookup"><span data-stu-id="8d465-141">This event may be raised zero or more times between `DeserializationStart` and `DeserializationEnd` events.</span></span>

<span data-ttu-id="8d465-142">To zdarzenie zawiera ładunek z jednym argumentem.</span><span class="sxs-lookup"><span data-stu-id="8d465-142">This event contains a payload with one argument.</span></span>

* <span data-ttu-id="8d465-143">`typeName` ( `string` ): Kwalifikowana nazwa zestawu (zobacz <xref:System.Type.AssemblyQualifiedName?displayProperty=nameWithType> ) deserializowany typ.</span><span class="sxs-lookup"><span data-stu-id="8d465-143">`typeName` (`string`): The assembly-qualified name (see <xref:System.Type.AssemblyQualifiedName?displayProperty=nameWithType>) of the type being deserialized.</span></span>

### <a name="advanced-subscribing-to-a-subset-of-notifications"></a><span data-ttu-id="8d465-144">\[Zaawansowana \] subskrypcja podzbioru powiadomień</span><span class="sxs-lookup"><span data-stu-id="8d465-144">\[Advanced\] Subscribing to a subset of notifications</span></span>

<span data-ttu-id="8d465-145">Detektory, którzy chcą subskrybować tylko podzestaw powiadomień, mogą wybrać słowa kluczowe do włączenia.</span><span class="sxs-lookup"><span data-stu-id="8d465-145">Listeners who wish to subscribe to only a subset of notifications can choose which keywords to enable.</span></span>

* <span data-ttu-id="8d465-146">`Serialization` = `(EventKeywords)1`: Wywołuje `SerializationStart` zdarzenia, `SerializationEnd` i `SerializingObject` .</span><span class="sxs-lookup"><span data-stu-id="8d465-146">`Serialization` = `(EventKeywords)1`: Raises the `SerializationStart`, `SerializationEnd`, and `SerializingObject` events.</span></span>
* <span data-ttu-id="8d465-147">`Deserialization` = `(EventKeywords)2`: Wywołuje `DeserializationStart` zdarzenia, `DeserializationEnd` i `DeserializingObject` .</span><span class="sxs-lookup"><span data-stu-id="8d465-147">`Deserialization` = `(EventKeywords)2`: Raises the `DeserializationStart`, `DeserializationEnd`, and `DeserializingObject` events.</span></span>

<span data-ttu-id="8d465-148">Jeśli podczas rejestrowania nie są dostępne żadne filtry słów kluczowych `EventListener` , zostaną zgłoszone wszystkie zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="8d465-148">If no keyword filters are provided during `EventListener` registration, all events are raised.</span></span>

<span data-ttu-id="8d465-149">Aby uzyskać więcej informacji, zobacz <xref:System.Diagnostics.Tracing.EventKeywords?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="8d465-149">For more information, see <xref:System.Diagnostics.Tracing.EventKeywords?displayProperty=nameWithType>.</span></span>

## <a name="sample-code"></a><span data-ttu-id="8d465-150">Przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="8d465-150">Sample code</span></span>

<span data-ttu-id="8d465-151">Następujący kod:</span><span class="sxs-lookup"><span data-stu-id="8d465-151">The following code:</span></span>

- <span data-ttu-id="8d465-152">tworzy `EventListener` Typ pochodny, który zapisuje w `System.Console` ,</span><span class="sxs-lookup"><span data-stu-id="8d465-152">creates an `EventListener`-derived type that writes to `System.Console`,</span></span>
- <span data-ttu-id="8d465-153">subskrybuje `BinaryFormatter` wygenerowane powiadomienia,</span><span class="sxs-lookup"><span data-stu-id="8d465-153">subscribes that listener to `BinaryFormatter`-produced notifications,</span></span>
- <span data-ttu-id="8d465-154">serializować i deserializacji prostego grafu obiektów przy użyciu `BinaryFormatter` , i</span><span class="sxs-lookup"><span data-stu-id="8d465-154">serializes and deserializes a simple object graph using `BinaryFormatter`, and</span></span>
- <span data-ttu-id="8d465-155">analizuje zdarzenia, które zostały zgłoszone.</span><span class="sxs-lookup"><span data-stu-id="8d465-155">analyzes the events that have been raised.</span></span>

:::code language="csharp" source="snippets/binaryformatter-event-source/csharp/Program.cs":::

<span data-ttu-id="8d465-156">Poprzedni kod generuje dane wyjściowe podobne do następującego przykładu:</span><span class="sxs-lookup"><span data-stu-id="8d465-156">The preceding code produces output similar to the following example:</span></span>

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

<span data-ttu-id="8d465-157">W tym przykładzie dzienników opartych na konsoli, `EventListener` których Serializacja zaczyna się, wystąpienia `Person` i `Book` są serializowane, a następnie zakończenie serializacji.</span><span class="sxs-lookup"><span data-stu-id="8d465-157">In this sample, the console-based `EventListener` logs that serialization starts, instances of `Person` and `Book` are serialized, and then serialization completes.</span></span> <span data-ttu-id="8d465-158">Podobnie po rozpoczęciu deserializacji wystąpienia `Person` i `Book` są deserializowane, a następnie ukończono deserializacji.</span><span class="sxs-lookup"><span data-stu-id="8d465-158">Similarly, once deserialization has started, instances of `Person` and `Book` are deserialized, and then deserialization completes.</span></span>

<span data-ttu-id="8d465-159">Następnie aplikacja drukuje wartości zawarte w deserializacji, `Person` Aby wykazać, że obiekt został prawidłowo Zserializowany i deserializacji.</span><span class="sxs-lookup"><span data-stu-id="8d465-159">The app then prints the values contained in the deserialized `Person` to demonstrate that the object did in fact serialize and deserialize properly.</span></span>

## <a name="see-also"></a><span data-ttu-id="8d465-160">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="8d465-160">See also</span></span>

<span data-ttu-id="8d465-161">Aby uzyskać więcej informacji na temat korzystania `EventListener` z powiadomień na temat odbierania `EventSource` , zobacz [ `EventListener` Klasa](xref:System.Diagnostics.Tracing.EventListener).</span><span class="sxs-lookup"><span data-stu-id="8d465-161">For more information on using `EventListener` to receive `EventSource`-based notifications, see [the `EventListener` class](xref:System.Diagnostics.Tracing.EventListener).</span></span>
