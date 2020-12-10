---
title: Serializowanie i deserializacja JSON przy użyciu języka C# — .NET
description: To omówienie zawiera opis System.Text.Json funkcji przestrzeni nazw do serializacji do i deserializacji z JSON w programie .NET.
ms.date: 01/10/2020
no-loc:
- System.Text.Json
- Newtonsoft.Json
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: cb5c15c2a5c336e2d5b4a3754fa7a02a370602f3
ms.sourcegitcommit: 81f1bba2c97a67b5ca76bcc57b37333ffca60c7b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/10/2020
ms.locfileid: "97009888"
---
# <a name="json-serialization-and-deserialization-marshalling-and-unmarshalling-in-net---overview"></a>Serializacja i deserializacja kodu JSON (kierowanie i cofanie) w programie .NET — Omówienie

`System.Text.Json`Przestrzeń nazw zawiera funkcje serializacji do i deserializacji z JavaScript Object Notation (JSON).

Projekt biblioteki wyróżnia wysoką wydajność i małą alokację pamięci w ramach rozbudowanego zestawu funkcji. Wbudowana obsługa UTF-8 optymalizuje proces odczytywania i pisania tekstu JSON zakodowanego w formacie UTF-8, który jest najbardziej rozpowszechnionym kodowaniem danych w sieci Web i plikach na dysku.

Biblioteka zawiera również klasy umożliwiające pracę z modelem DOM (Document objecting) w pamięci. Ta funkcja włącza losowy dostęp tylko do odczytu do elementów w pliku JSON lub ciągu.

## <a name="how-to-get-the-library"></a>Jak uzyskać bibliotekę

* Biblioteka jest wbudowana w ramach współdzielonej struktury dla platformy .NET Core 3,0 i nowszych.
* W przypadku wcześniejszych wersji platformy zainstaluj [System.Text.Json](https://www.nuget.org/packages/System.Text.Json) pakiet NuGet. Pakiet obsługuje:

  * .NET Standard 2,0 i nowsze wersje
  * .NET Framework 4.7.2 i nowsze wersje
  * .NET Core 2,0, 2,1 i 2,2

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Jak używać biblioteki](system-text-json-how-to.md)
* [Tworzenie wystąpienia JsonSerializerOptions wystąpień](system-text-json-configure-options.md)
* [Włączanie dopasowywania bez uwzględniania wielkości liter](system-text-json-character-casing.md)
* [Dostosowywanie nazw i wartości właściwości](system-text-json-customize-properties.md)
* [Ignorowanie właściwości](system-text-json-ignore-properties.md)
* [Zezwalanie na nieprawidłowy kod JSON](system-text-json-invalid-json.md)
* [Obsługa przepełnienia kodu JSON](system-text-json-handle-overflow.md)
* [Zachowywanie odwołań](system-text-json-preserve-references.md)
* [Niemodyfikowalne typy i niepubliczne metody dostępu](system-text-json-immutability.md)
* [Serializacja polimorficzna](system-text-json-polymorphism.md)
* [Migruj z Newtonsoft.Json do System.Text.Json](system-text-json-migrate-from-newtonsoft-how-to.md)
* [Dostosowywanie kodowania znaków](system-text-json-character-encoding.md)
* [Napisz niestandardowe serializatory i deserializatory](write-custom-serializer-deserializer.md)
* [Zapisz konwertery niestandardowe na potrzeby serializacji JSON](system-text-json-converters-how-to.md)
* [Obsługa wartości DateTime i DateTimeOffset](../datetime/system-text-json-support.md)
* [System.Text.Json Dokumentacja interfejsu API](xref:System.Text.Json)
* [System.Text.Json. Dokumentacja interfejsu API serializacji](xref:System.Text.Json.Serialization)
