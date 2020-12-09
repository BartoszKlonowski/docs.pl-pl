---
title: Jak utworzyć wystąpienie JsonSerializerOptions z System.Text.Json
description: Dowiedz się, jak uniknąć problemów z wydajnością oraz jak używać konstruktorów dostępnych dla wystąpień JsonSerializerOptions.
ms.date: 12/02/2020
no-loc:
- System.Text.Json
- Newtonsoft.Json
zone_pivot_groups: dotnet-version
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: 257c99e117dea9a9b3ab2352c9a442d71a2cdabd
ms.sourcegitcommit: 0014aa4d5cb2da56a70e03fc68f663d64df5247a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/09/2020
ms.locfileid: "96918557"
---
# <a name="how-to-instantiate-jsonserializeroptions-instances-with-no-locsystemtextjson"></a>Jak utworzyć wystąpienie JsonSerializerOptions wystąpień z System.Text.Json

W tym artykule wyjaśniono, jak uniknąć problemów z wydajnością podczas korzystania z programu <xref:System.Text.Json.JsonSerializerOptions> . Pokazano również, jak używać konstruktorów sparametryzowanych, które są dostępne.

## <a name="reuse-jsonserializeroptions-instances"></a>Ponowne użycie wystąpień JsonSerializerOptions

Jeśli używasz `JsonSerializerOptions` wielokrotnie z tymi samymi opcjami, nie twórz nowego `JsonSerializerOptions` wystąpienia za każdym razem, gdy go używasz. Ponownie Użyj tego samego wystąpienia dla każdego wywołania. Te wskazówki odnoszą się do kodu zapisanego w przypadku konwerterów niestandardowych i podczas wywoływania <xref:System.Text.Json.JsonSerializer.Serialize%2A?displayProperty=nameWithType> lub <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=nameWithType> .

Poniższy kod ilustruje spadek wydajności przy użyciu nowych wystąpień opcji.

:::code language="csharp" source="snippets/system-text-json-configure-options/csharp/ReuseOptionsInstances.cs":::

Poprzedni kod serializować mały obiekt 100 000 razy przy użyciu tego samego wystąpienia opcji. Następnie deserializacji ten sam obiekt o tej samej liczbie razy i tworzy nowe wystąpienie opcji za każdym razem. Typowa różnica czasu wykonywania jest 190 w porównaniu do 40 140 milisekund. Różnica jest jeszcze większa w przypadku zwiększenia liczby iteracji.

Serializator przeprowadzi fazę rozgrzewania podczas pierwszej serializacji każdego typu na grafie obiektów, gdy do niego zostanie przesłane nowe wystąpienie opcji. Ta rozgrzewanie obejmuje tworzenie pamięci podręcznej metadanych, która jest wymagana do serializacji. Metadane obejmują delegatów do metod pobierających właściwości, Setters, argumentów konstruktora, określonych atrybutów i tak dalej. Ta pamięć podręczna metadanych jest przechowywana w wystąpieniu opcji. Ten sam proces rozgrzewania i pamięć podręczna stosuje się do deserializacji.

Rozmiar pamięci podręcznej metadanych w `JsonSerializerOptions` wystąpieniu zależy od liczby typów do serializacji. W przypadku przekazania wielu typów — na przykład dynamicznie generowanych typów — do serializatora rozmiar pamięci podręcznej będzie nadal wzrastał i może zakończyć działanie `OutOfMemoryException` .

## <a name="copy-jsonserializeroptions"></a>Kopiuj JsonSerializerOptions

::: zone pivot="dotnet-5-0"
Istnieje Konstruktor [JsonSerializerOptions] (linki XREF: System.Text.Json . JsonSerializerOptions .% 23ctor ( System.Text.Json . JsonSerializerOptions)), która umożliwia utworzenie nowego wystąpienia z takimi samymi opcjami jak istniejące wystąpienie, jak pokazano w następującym przykładzie:

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/CopyOptions.cs" highlight="29":::
::: zone-end

::: zone pivot="dotnet-core-3-1"
`JsonSerializerOptions`Konstruktor, który pobiera istniejące wystąpienie, nie jest dostępny w programie .NET Core 3,1.
::: zone-end

## <a name="web-defaults-for-jsonserializeroptions"></a>Ustawienia domyślne sieci Web dla JsonSerializerOptions

::: zone pivot="dotnet-5-0"
Poniżej przedstawiono opcje, które mają różne wartości domyślne dla usługi Web Apps:

* <xref:System.Text.Json.JsonSerializerOptions.PropertyNameCaseInsensitive%2A> = `true`
* <xref:System.Text.Json.JsonNamingPolicy> = <xref:System.Text.Json.JsonNamingPolicy.CamelCase>
* <xref:System.Text.Json.JsonSerializerOptions.NumberHandling%2A> = <xref:System.Text.Json.Serialization.JsonNumberHandling.AllowReadingFromString>

Istnieje Konstruktor [JsonSerializerOptions] (linki XREF: System.Text.Json . JsonSerializerOptions .% 23ctor ( System.Text.Json . JsonSerializerDefaults)? View = NET-5,0&Preserve-View = true), która umożliwia utworzenie nowego wystąpienia z opcjami domyślnymi, które ASP.NET Core używane przez aplikacje sieci Web, jak pokazano w następującym przykładzie:

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/OptionsDefaults.cs" highlight="24":::
::: zone-end

::: zone pivot="dotnet-core-3-1"
Poniżej przedstawiono opcje, które mają różne wartości domyślne dla usługi Web Apps:

* <xref:System.Text.Json.JsonSerializerOptions.PropertyNameCaseInsensitive%2A> = `true`
* <xref:System.Text.Json.JsonNamingPolicy> = <xref:System.Text.Json.JsonNamingPolicy.CamelCase>

`JsonSerializerOptions`Konstruktor, który określa zestaw ustawień domyślnych, nie jest dostępny w programie .NET Core 3,1.
::: zone-end

## <a name="see-also"></a>Zobacz też

* [System.Text.Json Podsumowanie](system-text-json-overview.md)
* [Włączanie dopasowywania bez uwzględniania wielkości liter](system-text-json-character-casing.md)
* [Dostosowywanie nazw i wartości właściwości](system-text-json-customize-properties.md)
* [Ignorowanie właściwości](system-text-json-ignore-properties.md)
* [Zezwalanie na nieprawidłowy kod JSON](system-text-json-invalid-json.md)
* [Obsługa przepełnienia kodu JSON](system-text-json-handle-overflow.md)
* [Zachowaj odwołania cykliczne](system-text-json-preserve-references.md)
* [Niemodyfikowalne typy i niepubliczne metody dostępu](system-text-json-immutability.md)
* [Serializacja polimorficzna](system-text-json-polymorphism.md)
* [System.Text.Json Dokumentacja interfejsu API](xref:System.Text.Json)
