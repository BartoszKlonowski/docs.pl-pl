---
title: Jak zachować odwołania za pomocą System.Text.Json
description: Dowiedz się, jak zachować odwołania i obsłużyć odwołania cykliczne podczas serializacji do i deserializacji z JSON w programie .NET.
ms.date: 12/09/2020
no-loc:
- System.Text.Json
- Newtonsoft.Json
zone_pivot_groups: dotnet-version
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: d358c953c0979ca097c080fcd750d5ef95b07de0
ms.sourcegitcommit: 81f1bba2c97a67b5ca76bcc57b37333ffca60c7b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/10/2020
ms.locfileid: "97008737"
---
# <a name="how-to-preserve-references-and-handle-circular-references-with-no-locsystemtextjson"></a>Jak zachować odwołania i obsłużyć odwołania cykliczne z System.Text.Json

::: zone pivot="dotnet-5-0"

Aby zachować odwołania i obsłużyć odwołania cykliczne, ustaw wartość <xref:System.Text.Json.JsonSerializerOptions.ReferenceHandler%2A> <xref:System.Text.Json.Serialization.ReferenceHandler.Preserve%2A> . To ustawienie powoduje następujące zachowanie:

* Podczas serializacji:

  Podczas pisania typów złożonych, serializator również zapisuje właściwości metadanych ( `$id` , `$values` i `$ref` ).

* Przy deserializacji:

  Oczekiwana jest wartość metadanych (choć nie jest obowiązkowa), a Deserializator próbuje zrozumieć ten element.

Poniższy kod ilustruje użycie tego `Preserve` Ustawienia.

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/PreserveReferences.cs" highlight="34":::

Tej funkcji nie można używać do zachowywania typów wartości lub niezmiennych typów. Podczas deserializacji wystąpienie niezmiennego typu jest tworzone po odczytaniu całego ładunku. W związku z tym może być niemożliwe deserializacja tego samego wystąpienia, jeśli odwołanie do niego pojawia się w ramach ładunku JSON.

W przypadku typów wartości, niemodyfikowalnych typów i tablic nie są serializowane żadne metadane odwołania. Podczas deserializacji wyjątek jest zgłaszany, jeśli `$ref` lub `$id` zostanie znaleziony. Jednak typy wartości ignorują `$id` (i `$values` w przypadku kolekcji), aby umożliwić deserializacji ładunków, które zostały zserializowane przy użyciu Newtonsoft.Json .  Newtonsoft.Json wykonuje serializacji metadanych dla takich typów.

Aby określić, czy obiekty są równe, System.Text.Json używa <xref:System.Collections.Generic.ReferenceEqualityComparer.Instance%2A?displayProperty=nameWithType> , który używa równości odwołań ( <xref:System.Object.ReferenceEquals(System.Object,System.Object)?displayProperty=nameWithType> ) zamiast równości wartości ( <xref:System.Object.Equals(System.Object)?displayProperty=nameWithType> podczas porównywania dwóch wystąpień obiektów.

Aby uzyskać więcej informacji o tym, jak odwołania są serializowane i deserializowane, zobacz <xref:System.Text.Json.Serialization.ReferenceHandler.Preserve%2A?displayProperty=nameWithType> .

<xref:System.Text.Json.Serialization.ReferenceResolver>Klasa definiuje zachowanie zachowywania odwołań podczas serializacji i deserializacji. Utwórz klasę pochodną, aby określić zachowanie niestandardowe. Aby zapoznać się z przykładem, zobacz [GuidReferenceResolver](https://github.com/dotnet/docs/blob/9d5e88edbd7f12be463775ffebbf07ac8415fe18/docs/standard/serialization/snippets/system-text-json-how-to-5-0/csharp/GuidReferenceResolverExample.cs).

::: zone-end

::: zone pivot="dotnet-core-3-1"
System.Text.Json w programie .NET Core 3,1 obsługuje Serializacja przez wartość i zgłasza wyjątek dla odwołań cyklicznych.
::: zone-end

## <a name="see-also"></a>Zobacz także

* [System.Text.Json Podsumowanie](system-text-json-overview.md)
* [Jak serializować i deserializować dane JSON](system-text-json-how-to.md)
* [Tworzenie wystąpienia JsonSerializerOptions wystąpień](system-text-json-configure-options.md)
* [Włączanie dopasowywania bez uwzględniania wielkości liter](system-text-json-character-casing.md)
* [Dostosowywanie nazw i wartości właściwości](system-text-json-customize-properties.md)
* [Ignorowanie właściwości](system-text-json-ignore-properties.md)
* [Zezwalanie na nieprawidłowy kod JSON](system-text-json-invalid-json.md)
* [Obsługa przepełnienia kodu JSON](system-text-json-handle-overflow.md)
* [Niemodyfikowalne typy i niepubliczne metody dostępu](system-text-json-immutability.md)
* [Serializacja polimorficzna](system-text-json-polymorphism.md)
* [Migruj z Newtonsoft.Json do System.Text.Json](system-text-json-migrate-from-newtonsoft-how-to.md)
* [Dostosowywanie kodowania znaków](system-text-json-character-encoding.md)
* [Napisz niestandardowe serializatory i deserializatory](write-custom-serializer-deserializer.md)
* [Zapisz konwertery niestandardowe na potrzeby serializacji JSON](system-text-json-converters-how-to.md)
* [Obsługa wartości DateTime i DateTimeOffset](../datetime/system-text-json-support.md)
* [System.Text.Json Dokumentacja interfejsu API](xref:System.Text.Json)
* [System.Text.Json. Dokumentacja interfejsu API serializacji](xref:System.Text.Json.Serialization)
