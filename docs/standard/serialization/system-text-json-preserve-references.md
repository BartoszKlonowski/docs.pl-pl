---
title: Jak zachować odwołania za pomocą System.Text.Json
description: Dowiedz się, jak zachować odwołania i obsłużyć odwołania cykliczne podczas serializacji do i deserializacji z JSON w programie .NET.
ms.date: 11/30/2020
no-loc:
- System.Text.Json
- Newtonsoft.Json
zone_pivot_groups: dotnet-version
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: 9254ca261c7d748c04c311fa56359014f752ff31
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96439970"
---
# <a name="how-to-handle-circular-references-with-no-locsystemtextjson"></a>Jak obsłużyć odwołania cykliczne z System.Text.Json

W tym artykule dowiesz się, jak obsługiwać odwołania cykliczne z `System.Text.Json` przestrzeni nazw.

## <a name="preserve-references-and-handle-circular-references"></a>Zachowaj odwołania i dojścia cykliczne odwołania

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

## <a name="see-also"></a>Zobacz też

* [System.Text.Json Podsumowanie](system-text-json-overview.md)
* [Tworzenie wystąpienia JsonSerializerOptions](system-text-json-configure-options.md)
* [Włącz dopasowywanie bez uwzględniania wielkości liter](system-text-json-character-casing.md)
* [Dostosowywanie nazw i wartości właściwości](system-text-json-customize-properties.md)
* [Ignoruj właściwości](system-text-json-ignore-properties.md)
* [Zezwalaj na nieprawidłowy kod JSON](system-text-json-invalid-json.md)
* [Obsługa przepełnienia kodu JSON](system-text-json-handle-overflow.md)
* [Niemodyfikowalne typy i niepubliczne metody dostępu](system-text-json-immutability.md)
* [Serializacja polimorficzna](system-text-json-polymorphism.md)
* [System.Text.Json Dokumentacja interfejsu API](xref:System.Text.Json)
