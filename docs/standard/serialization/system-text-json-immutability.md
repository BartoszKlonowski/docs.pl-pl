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
ms.openlocfilehash: d3e61d44ce22b7f50838b6d3ba9cf64004bd3725
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96439964"
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

## <a name="see-also"></a>Zobacz też

* [System.Text.Json Podsumowanie](system-text-json-overview.md)
* [Tworzenie wystąpienia JsonSerializerOptions](system-text-json-configure-options.md)
* [Włącz dopasowywanie bez uwzględniania wielkości liter](system-text-json-character-casing.md)
* [Dostosowywanie nazw i wartości właściwości](system-text-json-customize-properties.md)
* [Ignoruj właściwości](system-text-json-ignore-properties.md)
* [Zezwalaj na nieprawidłowy kod JSON](system-text-json-invalid-json.md)
* [Obsługa przepełnienia kodu JSON](system-text-json-handle-overflow.md)
* [Zachowaj odwołania cykliczne](system-text-json-preserve-references.md)
* [Serializacja polimorficzna](system-text-json-polymorphism.md)
* [System.Text.Json Dokumentacja interfejsu API](xref:System.Text.Json)
