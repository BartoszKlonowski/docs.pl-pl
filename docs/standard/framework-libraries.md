---
title: Biblioteki platformy
description: Dowiedz się, w jaki sposób biblioteki zapewniają implementacje dla wielu typów ogólnych i specyficznych dla aplikacji, algorytmów i funkcji narzędzi.
author: richlander
ms.date: 06/20/2016
ms.assetid: 7b77b6c1-8367-4602-bff3-91e4c05ac643
ms.openlocfilehash: 4e71f81b0dd72f4569d8b6b319b9e97491533d28
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96438205"
---
# <a name="framework-libraries"></a>Biblioteki platformy

Platforma .NET ma standardowy zestaw klas rozległych, nazywanych bibliotekami klas podstawowych (zestaw podstawowy) lub bibliotekami klas platformy (kompletna). Te biblioteki zapewniają implementacje dla wielu typów ogólnych i specyficznych dla aplikacji, algorytmy i funkcje narzędzia. Biblioteki komercyjne i społecznościowe są tworzone na podstawie bibliotek klas platformy, co pozwala łatwo korzystać z bibliotek znajdujących się poza półkami dla szerokiego zestawu zadań obliczeniowych.

Podzbiór tych bibliotek jest dostarczany z każdą implementacją platformy .NET. Interfejsy API biblioteki podstawowej klasy (BCL) są oczekiwane w przypadku każdej implementacji platformy .NET, ponieważ chcą, aby były one potrzebne. Biblioteki specyficzne dla aplikacji powyżej BCL, takie jak ASP.NET, nie będą dostępne we wszystkich implementacjach platformy .NET.

## <a name="base-class-libraries"></a>Biblioteki klas bazowych

BCL zapewnia najpopularniejsze typy i funkcje narzędziowe oraz są podstawą wszystkich innych bibliotek klas platformy .NET. Mają one na celu dostarczenie bardzo ogólnych implementacji bez jakichkolwiek postanowień w obciążeniu. Wydajność jest zawsze ważnym zagadnieniem, ponieważ aplikacje mogą preferować konkretne zasady, takie jak niskie opóźnienie do wysokiej przepływności lub niskiej ilości pamięci do użycia w niskich PROCESORAch. Te biblioteki mają ogólne znaczenie dla wysokiej wydajności i przyjmują podejście środkowe w zależności od tego, jakie są problemy z wydajnością. W przypadku większości aplikacji to podejście zostało wykonane prawidłowo.

## <a name="primitive-types"></a>Typy pierwotne

Platforma .NET zawiera zestaw typów pierwotnych, które są używane (w różnym stopniu) w przypadku wszystkich programów. Te typy zawierają dane, takie jak liczby, ciągi, bajty i dowolnych obiektów. Język C# zawiera słowa kluczowe dla tych typów. Poniżej znajduje się przykładowy zestaw tych typów z pasującymi słowami kluczowymi języka C#.

* <xref:System.Object?displayProperty=nameWithType> ([Object](../csharp/language-reference/builtin-types/reference-types.md#the-object-type)) — Klasa podstawowa klasy bazowej w systemie typów CLR. Jest to katalog główny hierarchii typów.
* <xref:System.Int16?displayProperty=nameWithType> ([Krótki](../csharp/language-reference/builtin-types/integral-numeric-types.md)) — 16-bitowy typ liczby całkowitej ze znakiem. Niepodpisany <xref:System.UInt16> również istnieje.
* <xref:System.Int32?displayProperty=nameWithType> ([int](../csharp/language-reference/builtin-types/integral-numeric-types.md))-A 32-bitowy typ liczby całkowitej ze znakiem. Wartość [UInt32](../csharp/language-reference/builtin-types/integral-numeric-types.md) nie jest również dostępna.
* <xref:System.Single?displayProperty=nameWithType> ([float](../csharp/language-reference/builtin-types/floating-point-numeric-types.md))-A 32-bitowy typ zmiennoprzecinkowy.
* <xref:System.Decimal?displayProperty=nameWithType> ([Decimal](../csharp/language-reference/builtin-types/floating-point-numeric-types.md))-A 128-bitowy typ dziesiętny.
* <xref:System.Byte?displayProperty=nameWithType> ([Byte](../csharp/language-reference/builtin-types/integral-numeric-types.md)) — 8-bitowa liczba całkowita bez znaku reprezentująca bajt pamięci.
* <xref:System.Boolean?displayProperty=nameWithType> ([bool](../csharp/language-reference/builtin-types/bool.md)) — typ Boolean reprezentujący `true` lub `false` .
* <xref:System.Char?displayProperty=nameWithType> ([char](../csharp/language-reference/builtin-types/char.md)) — 16-bitowy typ liczbowy reprezentujący znak Unicode.
* <xref:System.String?displayProperty=nameWithType> ([String](../csharp/language-reference/builtin-types/reference-types.md#the-string-type)) — reprezentuje serię znaków. Różni się od `char[]` , ale umożliwia indeksowanie poszczególnych osób `char` w `string` .

## <a name="data-structures"></a>Struktury danych

Platforma .NET zawiera zestaw struktur danych, które są workhorsesą prawie wszystkich aplikacji platformy .NET. Są to najczęściej kolekcje, ale również zawierają inne typy.

* <xref:System.Array> -Reprezentuje tablicę obiektów o jednoznacznie określonym typie, do których można uzyskać dostęp za pomocą indeksu. Ma stały rozmiar dla swojej konstrukcji.
* <xref:System.Collections.Generic.List%601> -Reprezentuje silnie wpisaną listę obiektów, do których można uzyskać dostęp za pomocą indeksu. Rozmiar jest zmieniany automatycznie zgodnie z wymaganiami.
* <xref:System.Collections.Generic.Dictionary%602> -Reprezentuje kolekcję wartości, które są indeksowane przez klucz. Do wartości można uzyskać dostęp za pośrednictwem klucza. Rozmiar jest zmieniany automatycznie zgodnie z wymaganiami.
* <xref:System.Uri> — Oferuje reprezentację obiektu o jednolitym identyfikatorze zasobów (URI) i łatwy dostęp do części identyfikatora URI.
* <xref:System.DateTime> -Reprezentuje chwilę, zwykle wyrażoną jako dzień i godzinę.

## <a name="utility-apis"></a>Interfejsy API narzędzi

Platforma .NET zawiera zestaw interfejsów API narzędzi, które udostępniają funkcje dla wielu ważnych zadań.

* <xref:System.Net.Http.HttpClient> -Interfejs API do wysyłania żądań HTTP i otrzymywania odpowiedzi HTTP z zasobu identyfikowanego przez identyfikator URI.
* <xref:System.Xml.Linq.XDocument> -Interfejs API służący do ładowania i wykonywania zapytań o dokumenty XML za pomocą LINQ.
* <xref:System.IO.StreamReader> -Interfejs API służący do odczytywania plików.
* <xref:System.IO.StreamWriter> -Interfejs API do zapisywania plików.

## <a name="app-model-apis"></a>Interfejsy API App-Model

Istnieje wiele modeli aplikacji, których można używać w połączeniu z platformą .NET.

* [ASP.NET](https://www.asp.net) — udostępnia platformę internetową do tworzenia witryn i usług sieci Web. Obsługiwane w systemach Windows, Linux i macOS (zależy od wersji ASP.NET).
