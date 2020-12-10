---
title: Jak używać niejawnych typów i niepublicznych metod dostępu za pomocą System.Text.Json
description: Dowiedz się, jak korzystać z niemodyfikowalnych typów i niepublicznych metod dostępu podczas serializacji do i deserializacji z formatu JSON w programie .NET.
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
ms.openlocfilehash: ff8ecec0d70c877b7cbbd0297b85f0d9578ab828
ms.sourcegitcommit: 81f1bba2c97a67b5ca76bcc57b37333ffca60c7b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/10/2020
ms.locfileid: "97008828"
---
# <a name="how-to-use-immutable-types-and-non-public-accessors-with-no-locsystemtextjson"></a>Jak używać niejawnych typów i niepublicznych metod dostępu za pomocą System.Text.Json

W tym artykule dowiesz się, jak używać niemodyfikowalnych typów, takich jak rekordy, z `System.Text.Json` przestrzenią nazw.

## <a name="immutable-types-and-records"></a>Niezmienne typy i rekordy

::: zone pivot="dotnet-5-0"
`System.Text.Json` można użyć sparametryzowanego konstruktora, który umożliwia deserializacja niezmiennej klasy lub struktury. W przypadku klasy, jeśli jedynym konstruktorem jest sparametryzowane, ten Konstruktor zostanie użyty. Dla struktury lub klasy z wieloma konstruktorami Określ tę, która ma być używana przez zastosowanie atrybutu [[JsonConstructor]](xref:System.Text.Json.Serialization.JsonConstructorAttribute.%23ctor%2A) . Gdy atrybut nie jest używany, w przypadku obecności jest zawsze używany publiczny Konstruktor bez parametrów. Atrybutu można używać tylko z konstruktorami publicznymi. W poniższym przykładzie zastosowano `[JsonConstructor]` atrybut:

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/ImmutableTypes.cs" highlight="13":::

Rekordy w języku C# 9 są również obsługiwane, jak pokazano w następującym przykładzie:

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/Records.cs":::

W przypadku typów, które są niezmienne, ponieważ wszystkie ich metody ustawiające właściwości są niepubliczne, zapoznaj się z następującą sekcją dotyczącą [metod dostępu do właściwości niepublicznych](#non-public-property-accessors).
::: zone-end

::: zone pivot="dotnet-core-3-1"
`JsonConstructorAttribute` Obsługa rekordów w języku C# 9 nie jest dostępna w programie .NET Core 3,1.
::: zone-end

## <a name="non-public-property-accessors"></a>Metody dostępu do właściwości niepublicznych

::: zone pivot="dotnet-5-0"
Aby włączyć użycie niepublicznego dostępu do właściwości, Użyj atrybutu [[JsonInclude]](xref:System.Text.Json.Serialization.JsonIncludeAttribute) , jak pokazano w następującym przykładzie:

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/NonPublicAccessors.cs" highlight="12,15":::
::: zone-end

::: zone pivot="dotnet-core-3-1"
Metody dostępu do właściwości niepublicznych nie są obsługiwane w programie .NET Core 3,1. Aby uzyskać więcej informacji, zobacz [Migrowanie z Newtonsoft.Json artykułu](system-text-json-migrate-from-newtonsoft-how-to.md#non-public-property-setters-and-getters).
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
* [Zachowywanie odwołań](system-text-json-preserve-references.md)
* [Serializacja polimorficzna](system-text-json-polymorphism.md)
* [Migruj z Newtonsoft.Json do System.Text.Json](system-text-json-migrate-from-newtonsoft-how-to.md)
* [Dostosowywanie kodowania znaków](system-text-json-character-encoding.md)
* [Napisz niestandardowe serializatory i deserializatory](write-custom-serializer-deserializer.md)
* [Zapisz konwertery niestandardowe na potrzeby serializacji JSON](system-text-json-converters-how-to.md)
* [Obsługa wartości DateTime i DateTimeOffset](../datetime/system-text-json-support.md)
* [System.Text.Json Dokumentacja interfejsu API](xref:System.Text.Json)
* [System.Text.Json. Dokumentacja interfejsu API serializacji](xref:System.Text.Json.Serialization)
