---
title: Jak dostosować kodowanie znaków za pomocą System.Text.Json
description: Dowiedz się, jak dostosować kodowanie znaków podczas serializacji do i deserializacji z JSON w programie .NET.
ms.date: 11/30/2020
no-loc:
- System.Text.Json
- Newtonsoft.Json
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: f6a50a3ca2a5e871294cf7c056cbf197a61cd668
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96440026"
---
# <a name="how-to-customize-character-encoding-with-no-locsystemtextjson"></a><span data-ttu-id="cb691-103">Jak dostosować kodowanie znaków za pomocą System.Text.Json</span><span class="sxs-lookup"><span data-stu-id="cb691-103">How to customize character encoding with System.Text.Json</span></span>

<span data-ttu-id="cb691-104">Domyślnie serializator wyprowadza wszystkie znaki nienależące do zestawu znaków ASCII.</span><span class="sxs-lookup"><span data-stu-id="cb691-104">By default, the serializer escapes all non-ASCII characters.</span></span> <span data-ttu-id="cb691-105">Oznacza to, że zastępuje je, `\uxxxx` gdzie `xxxx` jest kodem Unicode znaku.</span><span class="sxs-lookup"><span data-stu-id="cb691-105">That is, it replaces them with `\uxxxx` where `xxxx` is the Unicode code of the character.</span></span> <span data-ttu-id="cb691-106">Na przykład, jeśli `Summary` Właściwość w następującym formacie JSON ma wartość cyrylicy `жарко` , `WeatherForecast` obiekt jest serializowany, jak pokazano w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="cb691-106">For example, if the `Summary` property in the following JSON is set to Cyrillic `жарко`, the `WeatherForecast` object is serialized as shown in this example:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "\u0436\u0430\u0440\u043A\u043E"
}
```

## <a name="serialize-language-character-sets"></a><span data-ttu-id="cb691-107">Serializowanie zestawów znaków języka</span><span class="sxs-lookup"><span data-stu-id="cb691-107">Serialize language character sets</span></span>

<span data-ttu-id="cb691-108">Aby serializować zestawy znaków z co najmniej jednego języka bez ucieczki, określ [zakresy Unicode](xref:System.Text.Unicode.UnicodeRanges) podczas tworzenia wystąpienia <xref:System.Text.Encodings.Web.JavaScriptEncoder?displayProperty=fullName> , jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="cb691-108">To serialize the character set(s) of one or more languages without escaping, specify [Unicode range(s)](xref:System.Text.Unicode.UnicodeRanges) when creating an instance of <xref:System.Text.Encodings.Web.JavaScriptEncoder?displayProperty=fullName>, as shown in the following example:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/SerializeCustomEncoding.cs" id="Usings":::

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/SerializeCustomEncoding.cs" id="LanguageSets":::

<span data-ttu-id="cb691-109">Ten kod nie ma ucieczki znaków cyrylicy lub greckich.</span><span class="sxs-lookup"><span data-stu-id="cb691-109">This code doesn't escape Cyrillic or Greek characters.</span></span> <span data-ttu-id="cb691-110">Jeśli `Summary` Właściwość jest ustawiona na wartość cyrylicy `жарко` , `WeatherForecast` obiekt jest serializowany, jak pokazano w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="cb691-110">If the `Summary` property is set to Cyrillic `жарко`, the `WeatherForecast` object is serialized as shown in this example:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "жарко"
}
```

<span data-ttu-id="cb691-111">Aby serializować wszystkie zestawy językowe bez ucieczki, użyj <xref:System.Text.Unicode.UnicodeRanges.All?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="cb691-111">To serialize all language sets without escaping, use <xref:System.Text.Unicode.UnicodeRanges.All?displayProperty=nameWithType>.</span></span>

## <a name="serialize-specific-characters"></a><span data-ttu-id="cb691-112">Serializacja określonych znaków</span><span class="sxs-lookup"><span data-stu-id="cb691-112">Serialize specific characters</span></span>

<span data-ttu-id="cb691-113">Alternatywą jest określenie pojedynczych znaków, które mają być dozwolone, bez konieczności ucieczki.</span><span class="sxs-lookup"><span data-stu-id="cb691-113">An alternative is to specify individual characters that you want to allow through without being escaped.</span></span> <span data-ttu-id="cb691-114">Poniższy przykład serializacji tylko dwa pierwsze znaki z `жарко` :</span><span class="sxs-lookup"><span data-stu-id="cb691-114">The following example serializes only the first two characters of `жарко`:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/SerializeCustomEncoding.cs" id="Usings":::

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/SerializeCustomEncoding.cs" id="SelectedCharacters":::

<span data-ttu-id="cb691-115">Oto przykład kodu JSON utworzonego przez poprzedni kod:</span><span class="sxs-lookup"><span data-stu-id="cb691-115">Here's an example of JSON produced by the preceding code:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "жа\u0440\u043A\u043E"
}
```

## <a name="serialize-all-characters"></a><span data-ttu-id="cb691-116">Serializować wszystkie znaki</span><span class="sxs-lookup"><span data-stu-id="cb691-116">Serialize all characters</span></span>

<span data-ttu-id="cb691-117">Aby zminimalizować liczbę ucieczki, można użyć <xref:System.Text.Encodings.Web.JavaScriptEncoder.UnsafeRelaxedJsonEscaping?displayProperty=nameWithType> , jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="cb691-117">To minimize escaping you can use <xref:System.Text.Encodings.Web.JavaScriptEncoder.UnsafeRelaxedJsonEscaping?displayProperty=nameWithType>, as shown in the following example:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/SerializeCustomEncoding.cs" id="Usings":::

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/SerializeCustomEncoding.cs" id="UnsafeRelaxed":::

> [!CAUTION]
> <span data-ttu-id="cb691-118">W porównaniu z domyślnym koderem `UnsafeRelaxedJsonEscaping` koder jest bardziej ograniczając, aby umożliwić przekazywanie znaków przez niezmieniony:</span><span class="sxs-lookup"><span data-stu-id="cb691-118">Compared to the default encoder, the `UnsafeRelaxedJsonEscaping` encoder is more permissive about allowing characters to pass through unescaped:</span></span>
>
> * <span data-ttu-id="cb691-119">Nie ucieczk znaków w języku HTML, takich jak `<` , `>` , `&` , i `'` .</span><span class="sxs-lookup"><span data-stu-id="cb691-119">It doesn't escape HTML-sensitive characters such as `<`, `>`, `&`, and `'`.</span></span>
> * <span data-ttu-id="cb691-120">Nie oferuje żadnej dodatkowej ochrony przed atakami na ataki typu XSS lub ujawnienie informacji, takich jak te, które mogą wynikać z klienta i serwera bez zgody na *zestaw znaków*.</span><span class="sxs-lookup"><span data-stu-id="cb691-120">It doesn't offer any additional defense-in-depth protections against XSS or information disclosure attacks, such as those which might result from the client and server disagreeing on the *charset*.</span></span>
>
> <span data-ttu-id="cb691-121">Używaj niebezpiecznego kodera tylko wtedy, gdy wiadomo, że klient będzie interpretować otrzymany ładunek jako zakodowany w formacie JSON UTF-8.</span><span class="sxs-lookup"><span data-stu-id="cb691-121">Use the unsafe encoder only when it's known that the client will be interpreting the resulting payload as UTF-8 encoded JSON.</span></span> <span data-ttu-id="cb691-122">Można na przykład użyć go, jeśli serwer wysyła nagłówek odpowiedzi `Content-Type: application/json; charset=utf-8` .</span><span class="sxs-lookup"><span data-stu-id="cb691-122">For example, you can use it if the server is sending the response header `Content-Type: application/json; charset=utf-8`.</span></span> <span data-ttu-id="cb691-123">Nigdy nie Zezwalaj na `UnsafeRelaxedJsonEscaping` emitowanie nieprzetworzonych danych wyjściowych do strony HTML lub `<script>` elementu.</span><span class="sxs-lookup"><span data-stu-id="cb691-123">Never allow the raw `UnsafeRelaxedJsonEscaping` output to be emitted into an HTML page or a `<script>` element.</span></span>

## <a name="see-also"></a><span data-ttu-id="cb691-124">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="cb691-124">See also</span></span>

* [<span data-ttu-id="cb691-125">System.Text.Json Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="cb691-125">System.Text.Json overview</span></span>](system-text-json-overview.md)
* [<span data-ttu-id="cb691-126">Jak napisać Serializatory niestandardowe i deserializatory</span><span class="sxs-lookup"><span data-stu-id="cb691-126">How to write custom serializers and deserializers</span></span>](write-custom-serializer-deserializer.md)
* [<span data-ttu-id="cb691-127">Jak napisać konwertery niestandardowe na potrzeby serializacji JSON</span><span class="sxs-lookup"><span data-stu-id="cb691-127">How to write custom converters for JSON serialization</span></span>](system-text-json-converters-how-to.md)
* <span data-ttu-id="cb691-128">[System.Text.Json Dokumentacja interfejsu API](xref:System.Text.Json)</span><span class="sxs-lookup"><span data-stu-id="cb691-128">[System.Text.Json API reference](xref:System.Text.Json)</span></span>
