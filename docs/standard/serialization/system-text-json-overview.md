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
# <a name="json-serialization-and-deserialization-marshalling-and-unmarshalling-in-net---overview"></a><span data-ttu-id="92f03-103">Serializacja i deserializacja kodu JSON (kierowanie i cofanie) w programie .NET — Omówienie</span><span class="sxs-lookup"><span data-stu-id="92f03-103">JSON serialization and deserialization (marshalling and unmarshalling) in .NET - overview</span></span>

<span data-ttu-id="92f03-104">`System.Text.Json`Przestrzeń nazw zawiera funkcje serializacji do i deserializacji z JavaScript Object Notation (JSON).</span><span class="sxs-lookup"><span data-stu-id="92f03-104">The `System.Text.Json` namespace provides functionality for serializing to and deserializing from JavaScript Object Notation (JSON).</span></span>

<span data-ttu-id="92f03-105">Projekt biblioteki wyróżnia wysoką wydajność i małą alokację pamięci w ramach rozbudowanego zestawu funkcji.</span><span class="sxs-lookup"><span data-stu-id="92f03-105">The library design emphasizes high performance and low memory allocation over an extensive feature set.</span></span> <span data-ttu-id="92f03-106">Wbudowana obsługa UTF-8 optymalizuje proces odczytywania i pisania tekstu JSON zakodowanego w formacie UTF-8, który jest najbardziej rozpowszechnionym kodowaniem danych w sieci Web i plikach na dysku.</span><span class="sxs-lookup"><span data-stu-id="92f03-106">Built-in UTF-8 support optimizes the process of reading and writing JSON text encoded as UTF-8, which is the most prevalent encoding for data on the web and files on disk.</span></span>

<span data-ttu-id="92f03-107">Biblioteka zawiera również klasy umożliwiające pracę z modelem DOM (Document objecting) w pamięci.</span><span class="sxs-lookup"><span data-stu-id="92f03-107">The library also provides classes for working with an in-memory document object model (DOM).</span></span> <span data-ttu-id="92f03-108">Ta funkcja włącza losowy dostęp tylko do odczytu do elementów w pliku JSON lub ciągu.</span><span class="sxs-lookup"><span data-stu-id="92f03-108">This feature enables random read-only access of the elements in a JSON file or string.</span></span>

## <a name="how-to-get-the-library"></a><span data-ttu-id="92f03-109">Jak uzyskać bibliotekę</span><span class="sxs-lookup"><span data-stu-id="92f03-109">How to get the library</span></span>

* <span data-ttu-id="92f03-110">Biblioteka jest wbudowana w ramach współdzielonej struktury dla platformy .NET Core 3,0 i nowszych.</span><span class="sxs-lookup"><span data-stu-id="92f03-110">The library is built-in as part of the shared framework for .NET Core 3.0 and later versions.</span></span>
* <span data-ttu-id="92f03-111">W przypadku wcześniejszych wersji platformy zainstaluj [System.Text.Json](https://www.nuget.org/packages/System.Text.Json) pakiet NuGet.</span><span class="sxs-lookup"><span data-stu-id="92f03-111">For earlier framework versions, install the [System.Text.Json](https://www.nuget.org/packages/System.Text.Json) NuGet package.</span></span> <span data-ttu-id="92f03-112">Pakiet obsługuje:</span><span class="sxs-lookup"><span data-stu-id="92f03-112">The package supports:</span></span>

  * <span data-ttu-id="92f03-113">.NET Standard 2,0 i nowsze wersje</span><span class="sxs-lookup"><span data-stu-id="92f03-113">.NET Standard 2.0 and later versions</span></span>
  * <span data-ttu-id="92f03-114">.NET Framework 4.7.2 i nowsze wersje</span><span class="sxs-lookup"><span data-stu-id="92f03-114">.NET Framework 4.7.2 and later versions</span></span>
  * <span data-ttu-id="92f03-115">.NET Core 2,0, 2,1 i 2,2</span><span class="sxs-lookup"><span data-stu-id="92f03-115">.NET Core 2.0, 2.1, and 2.2</span></span>

## <a name="additional-resources"></a><span data-ttu-id="92f03-116">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="92f03-116">Additional resources</span></span>

* [<span data-ttu-id="92f03-117">Jak używać biblioteki</span><span class="sxs-lookup"><span data-stu-id="92f03-117">How to use the library</span></span>](system-text-json-how-to.md)
* [<span data-ttu-id="92f03-118">Tworzenie wystąpienia JsonSerializerOptions wystąpień</span><span class="sxs-lookup"><span data-stu-id="92f03-118">Instantiate JsonSerializerOptions instances</span></span>](system-text-json-configure-options.md)
* [<span data-ttu-id="92f03-119">Włączanie dopasowywania bez uwzględniania wielkości liter</span><span class="sxs-lookup"><span data-stu-id="92f03-119">Enable case-insensitive matching</span></span>](system-text-json-character-casing.md)
* [<span data-ttu-id="92f03-120">Dostosowywanie nazw i wartości właściwości</span><span class="sxs-lookup"><span data-stu-id="92f03-120">Customize property names and values</span></span>](system-text-json-customize-properties.md)
* [<span data-ttu-id="92f03-121">Ignorowanie właściwości</span><span class="sxs-lookup"><span data-stu-id="92f03-121">Ignore properties</span></span>](system-text-json-ignore-properties.md)
* [<span data-ttu-id="92f03-122">Zezwalanie na nieprawidłowy kod JSON</span><span class="sxs-lookup"><span data-stu-id="92f03-122">Allow invalid JSON</span></span>](system-text-json-invalid-json.md)
* [<span data-ttu-id="92f03-123">Obsługa przepełnienia kodu JSON</span><span class="sxs-lookup"><span data-stu-id="92f03-123">Handle overflow JSON</span></span>](system-text-json-handle-overflow.md)
* [<span data-ttu-id="92f03-124">Zachowywanie odwołań</span><span class="sxs-lookup"><span data-stu-id="92f03-124">Preserve references</span></span>](system-text-json-preserve-references.md)
* [<span data-ttu-id="92f03-125">Niemodyfikowalne typy i niepubliczne metody dostępu</span><span class="sxs-lookup"><span data-stu-id="92f03-125">Immutable types and non-public accessors</span></span>](system-text-json-immutability.md)
* [<span data-ttu-id="92f03-126">Serializacja polimorficzna</span><span class="sxs-lookup"><span data-stu-id="92f03-126">Polymorphic serialization</span></span>](system-text-json-polymorphism.md)
* [<span data-ttu-id="92f03-127">Migruj z Newtonsoft.Json do System.Text.Json</span><span class="sxs-lookup"><span data-stu-id="92f03-127">Migrate from Newtonsoft.Json to System.Text.Json</span></span>](system-text-json-migrate-from-newtonsoft-how-to.md)
* [<span data-ttu-id="92f03-128">Dostosowywanie kodowania znaków</span><span class="sxs-lookup"><span data-stu-id="92f03-128">Customize character encoding</span></span>](system-text-json-character-encoding.md)
* [<span data-ttu-id="92f03-129">Napisz niestandardowe serializatory i deserializatory</span><span class="sxs-lookup"><span data-stu-id="92f03-129">Write custom serializers and deserializers</span></span>](write-custom-serializer-deserializer.md)
* [<span data-ttu-id="92f03-130">Zapisz konwertery niestandardowe na potrzeby serializacji JSON</span><span class="sxs-lookup"><span data-stu-id="92f03-130">Write custom converters for JSON serialization</span></span>](system-text-json-converters-how-to.md)
* [<span data-ttu-id="92f03-131">Obsługa wartości DateTime i DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="92f03-131">DateTime and DateTimeOffset support</span></span>](../datetime/system-text-json-support.md)
* <span data-ttu-id="92f03-132">[System.Text.Json Dokumentacja interfejsu API](xref:System.Text.Json)</span><span class="sxs-lookup"><span data-stu-id="92f03-132">[System.Text.Json API reference](xref:System.Text.Json)</span></span>
* <span data-ttu-id="92f03-133">[System.Text.Json. Dokumentacja interfejsu API serializacji](xref:System.Text.Json.Serialization)</span><span class="sxs-lookup"><span data-stu-id="92f03-133">[System.Text.Json.Serialization API reference](xref:System.Text.Json.Serialization)</span></span>
