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
# <a name="systemtextjson-requires-single-char-string-to-deserialize-a-char"></a><span data-ttu-id="bad03-103">System.Text.Json wymaga ciągu pojedynczego znaku do deserializacji znaku</span><span class="sxs-lookup"><span data-stu-id="bad03-103">System.Text.Json requires single-char string to deserialize a char</span></span>

<span data-ttu-id="bad03-104">Aby pomyślnie zdeserializować <xref:System.Char> przy użyciu <xref:System.Text.Json> , ciąg JSON musi zawierać pojedynczy znak.</span><span class="sxs-lookup"><span data-stu-id="bad03-104">To successfully deserialize a <xref:System.Char> using <xref:System.Text.Json>, the JSON string must contain a single character.</span></span>

## <a name="change-description"></a><span data-ttu-id="bad03-105">Zmień opis</span><span class="sxs-lookup"><span data-stu-id="bad03-105">Change description</span></span>

<span data-ttu-id="bad03-106">W poprzednich wersjach programu .NET wiele `char` ciągów w formacie JSON została pomyślnie odszeregowana do `char` właściwości lub pola.</span><span class="sxs-lookup"><span data-stu-id="bad03-106">In previous .NET versions, a multi-`char` string in the JSON is successfully deserialized to a `char` property or field.</span></span> <span data-ttu-id="bad03-107">`char`Używany jest tylko pierwszy ciąg, jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="bad03-107">Only the first `char` of the string is used, as in the following example:</span></span>

```csharp
// .NET Core 3.0 and 3.1: Returns the first char 'a'.
// .NET 5.0 and later: Throws JsonException because payload has more than one char.
char deserializedChar = JsonSerializer.Deserialize<char>("\"abc\"");
```

<span data-ttu-id="bad03-108">W przypadku platformy .NET 5,0 i nowszych wszystkie inne niż pojedyncze `char` ciągi powodują, że w <xref:System.Text.Json.JsonException> przypadku gdy obiekt docelowy deserializacji jest `char` .</span><span class="sxs-lookup"><span data-stu-id="bad03-108">In .NET 5.0 and later, anything other than a single-`char` string causes a <xref:System.Text.Json.JsonException> to be thrown when the deserialization target is a `char`.</span></span> <span data-ttu-id="bad03-109">Następujący przykładowy ciąg został pomyślnie odszeregowany we wszystkich wersjach .NET:</span><span class="sxs-lookup"><span data-stu-id="bad03-109">The following example string is successfully deserialized in all .NET versions:</span></span>

```csharp
// Correct usage.
char deserializedChar = JsonSerializer.Deserialize<char>("\"a\"");
```

## <a name="version-introduced"></a><span data-ttu-id="bad03-110">Wprowadzona wersja</span><span class="sxs-lookup"><span data-stu-id="bad03-110">Version introduced</span></span>

<span data-ttu-id="bad03-111">5,0</span><span class="sxs-lookup"><span data-stu-id="bad03-111">5.0</span></span>

## <a name="reason-for-change"></a><span data-ttu-id="bad03-112">Przyczyna zmiany</span><span class="sxs-lookup"><span data-stu-id="bad03-112">Reason for change</span></span>

<span data-ttu-id="bad03-113">Analizowanie dla deserializacji powinno zakończyć się powodzeniem tylko wtedy, gdy podany ładunek jest prawidłowy dla typu docelowego.</span><span class="sxs-lookup"><span data-stu-id="bad03-113">Parsing for deserialization should only succeed when the provided payload is valid for the target type.</span></span> <span data-ttu-id="bad03-114">Dla `char` typu Jedynym prawidłowym ładunkiem jest pojedynczy `char` ciąg.</span><span class="sxs-lookup"><span data-stu-id="bad03-114">For a `char` type, the only valid payload is a single-`char` string.</span></span>

## <a name="recommended-action"></a><span data-ttu-id="bad03-115">Zalecana akcja</span><span class="sxs-lookup"><span data-stu-id="bad03-115">Recommended action</span></span>

<span data-ttu-id="bad03-116">Podczas deserializacji JSON do `char` elementu docelowego upewnij się, że ciąg składa się z jednego `char` .</span><span class="sxs-lookup"><span data-stu-id="bad03-116">When you deserialize JSON into a `char` target, make sure the string consists of a single `char`.</span></span>

## <a name="affected-apis"></a><span data-ttu-id="bad03-117">Dotyczy interfejsów API</span><span class="sxs-lookup"><span data-stu-id="bad03-117">Affected APIs</span></span>

- <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=fullName>

<!--

### Affected APIs

- `Overload:System.Text.Json.JsonSerializer.Deserialize`

### Category

Serialization

-->
