---
title: Implementowanie niestandardowego dostawcy konfiguracji w programie .NET
description: Dowiedz się, jak zaimplementować niestandardowego dostawcę konfiguracji w aplikacjach .NET.
author: IEvangelist
ms.author: dapine
ms.date: 12/04/2020
ms.topic: how-to
ms.openlocfilehash: 22e46b7df8b02421633d6be251d990879baa8b2b
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740118"
---
# <a name="implement-a-custom-configuration-provider-in-net"></a>Implementowanie niestandardowego dostawcy konfiguracji w programie .NET

Istnieje wielu [dostawców konfiguracji](configuration-providers.md) dostępnych dla wspólnych źródeł konfiguracji, takich jak pliki JSON, XML i ini. Może być konieczne zaimplementowanie niestandardowego dostawcy konfiguracji, gdy jeden z dostępnych dostawców nie odpowiada wymaganiom Twojej aplikacji. W tym artykule dowiesz się, jak zaimplementować niestandardowego dostawcę konfiguracji, który korzysta z bazy danych jako źródła konfiguracji.

## <a name="custom-configuration-provider"></a>Niestandardowy dostawca konfiguracji

Przykładowa aplikacja pokazuje, jak utworzyć podstawowego dostawcę konfiguracji, który odczytuje pary klucz-wartość konfiguracji z bazy danych przy użyciu narzędzia [Entity Framework (EF) Core](/ef/core).

Dostawca ma następującą charakterystykę:

- Baza danych EF w pamięci jest używana w celach demonstracyjnych. Aby użyć bazy danych, która wymaga parametrów połączenia, zaimplementuj dodatkową wartość w `ConfigurationBuilder` celu dostarczenia parametrów połączenia od innego dostawcy konfiguracji.
- Dostawca odczytuje tabelę bazy danych w konfiguracji podczas uruchamiania. Dostawca nie wykonuje zapytania do bazy danych w oparciu o klucz.
- Ponowne załadowanie nie zostało zaimplementowane, więc aktualizacja bazy danych po uruchomieniu aplikacji nie ma wpływu na konfigurację aplikacji.

Zdefiniuj `Settings` jednostkę typu rekordu do przechowywania wartości konfiguracji w bazie danych. Można na przykład dodać plik *Settings.cs* do folderu *models* :

:::code language="csharp" source="snippets/configuration/custom-provider/Models/Settings.cs":::

Aby uzyskać informacje na temat typów rekordów, zobacz [typy rekordów w języku C# 9](../../csharp/whats-new/csharp-9.md#record-types).

Dodaj `EntityConfigurationContext` do magazynu i uzyskaj dostęp do skonfigurowanych wartości.

*Dostawcy/EntityConfigurationContext. cs*:

:::code language="csharp" source="snippets/configuration/custom-provider/Providers/EntityConfigurationContext.cs":::

Utwórz klasę implementującą <xref:Microsoft.Extensions.Configuration.IConfigurationSource> .

*Dostawcy/EntityConfigurationSource. cs*:

:::code language="csharp" source="snippets/configuration/custom-provider/Providers/EntityConfigurationSource.cs":::

Utwórz niestandardowego dostawcę konfiguracji, dziedziczących od <xref:Microsoft.Extensions.Configuration.ConfigurationProvider> . Dostawca konfiguracji inicjuje bazę danych, gdy jest pusta. Ponieważ w kluczach konfiguracji jest rozróżniana wielkość liter, słownik używany do inicjowania bazy danych jest tworzony przy użyciu funkcji porównującej bez uwzględniania wielkości liter ([StringComparer. OrdinalIgnoreCase](xref:System.StringComparer.OrdinalIgnoreCase)).

*Dostawcy/EntityConfigurationProvider. cs*:

:::code language="csharp" source="snippets/configuration/custom-provider/Providers/EntityConfigurationProvider.cs":::

`AddEntityConfiguration`Metoda rozszerzająca zezwala na Dodawanie źródła konfiguracji do <xref:Microsoft.Extensions.Configuration.IConfigurationBuilder> wystąpienia.

*Rozszerzenia/ConfigurationBuilderExtensions. cs*:

:::code language="csharp" source="snippets/configuration/custom-provider/Extensions/ConfigurationBuilderExtensions.cs":::

Poniższy kod pokazuje, jak używać niestandardowych `EntityConfigurationProvider` w *program.cs*:

:::code language="csharp" source="snippets/configuration/custom-provider/Program.cs" highlight="27-28":::

## <a name="see-also"></a>Zobacz także

- [Konfiguracja w programie .NET](configuration.md)
- [Dostawcy konfiguracji w programie .NET](configuration-providers.md)
