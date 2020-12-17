---
title: 'Istotna zmiana: deserializacja znaku wymaga ciągu znaków pojedynczego znaku'
description: Dowiedz się więcej o istotnej zmianie w programie .NET 5,0, gdzie System.Text.Json wymaga ciągu pojedynczego znaku w kodzie JSON podczas deserializacji do obiektu docelowego char.
ms.date: 12/15/2020
ms.openlocfilehash: 39a2d25b00bf8855cfbf46a4d78b8545052703e5
ms.sourcegitcommit: 635a0ff775d2447a81ef7233a599b8f88b162e5d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/17/2020
ms.locfileid: "97633874"
---
# <a name="systemtextjson-requires-single-char-string-to-deserialize-a-char"></a>System.Text.Json wymaga ciągu pojedynczego znaku do deserializacji znaku

Aby pomyślnie zdeserializować <xref:System.Char> przy użyciu <xref:System.Text.Json> , ciąg JSON musi zawierać pojedynczy znak.

## <a name="change-description"></a>Zmień opis

W poprzednich wersjach programu .NET wiele `char` ciągów w formacie JSON została pomyślnie odszeregowana do `char` właściwości lub pola. `char`Używany jest tylko pierwszy ciąg, jak w poniższym przykładzie:

```csharp
// .NET Core 3.0 and 3.1: Returns the first char 'a'.
// .NET 5.0 and later: Throws JsonException because payload has more than one char.
char deserializedChar = JsonSerializer.Deserialize<char>("\"abc\"");
```

W przypadku platformy .NET 5,0 i nowszych wszystkie inne niż pojedyncze `char` ciągi powodują, że w <xref:System.Text.Json.JsonException> przypadku gdy obiekt docelowy deserializacji jest `char` . Następujący przykładowy ciąg został pomyślnie odszeregowany we wszystkich wersjach .NET:

```csharp
// Correct usage.
char deserializedChar = JsonSerializer.Deserialize<char>("\"a\"");
```

## <a name="version-introduced"></a>Wprowadzona wersja

5,0

## <a name="reason-for-change"></a>Przyczyna zmiany

Analizowanie dla deserializacji powinno zakończyć się powodzeniem tylko wtedy, gdy podany ładunek jest prawidłowy dla typu docelowego. Dla `char` typu Jedynym prawidłowym ładunkiem jest pojedynczy `char` ciąg.

## <a name="recommended-action"></a>Zalecana akcja

Podczas deserializacji JSON do `char` elementu docelowego upewnij się, że ciąg składa się z jednego `char` .

## <a name="affected-apis"></a>Dotyczy interfejsów API

- <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=fullName>

<!--

### Affected APIs

- `Overload:System.Text.Json.JsonSerializer.Deserialize`

### Category

Serialization

-->
