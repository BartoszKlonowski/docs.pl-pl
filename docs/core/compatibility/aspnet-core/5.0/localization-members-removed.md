---
title: 'Nieprzerwana zmiana: Lokalizacja: Usunięto klasę ResourceManagerWithCultureStringLocalizer i element członkowski interfejsu WithCulture'
description: 'Dowiedz się więcej o zmianach w 5,0 ASP.NET Core lokalizacji zatytułowanej: Klasa ResourceManagerWithCultureStringLocalizer i element członkowski interfejsu WithCulture usunięte'
author: scottaddie
ms.author: scaddie
ms.date: 10/01/2020
ms.openlocfilehash: ac7723cd9b961b34b3f87a55119d421668c87417
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96437853"
---
# <a name="localization-resourcemanagerwithculturestringlocalizer-class-and-withculture-interface-member-removed"></a>Lokalizacja: Usunięto klasę ResourceManagerWithCultureStringLocalizer i element członkowski interfejsu WithCulture

Klasa [ResourceManagerWithCultureStringLocalizer](/dotnet/api/microsoft.extensions.localization.resourcemanagerwithculturestringlocalizer?view=dotnet-plat-ext-3.1) i Metoda [WithCulture](/dotnet/api/microsoft.extensions.localization.resourcemanagerstringlocalizer.withculture?view=dotnet-plat-ext-3.1) zostały usunięte w programie .NET 5,0 Preview 1.

W przypadku kontekstu zobacz [ASPNET/anonse # 346](https://github.com/aspnet/Announcements/issues/346) i [dotnet/aspnetcore # 3324](https://github.com/dotnet/aspnetcore/issues/3324). Aby uzyskać więcej dyskusji na temat tej zmiany, zobacz [dotnet/aspnetcore # 7756](https://github.com/dotnet/aspnetcore/issues/7756).

## <a name="version-introduced"></a>Wprowadzona wersja

5,0 wersja zapoznawcza 1

## <a name="old-behavior"></a>Stare zachowanie

`ResourceManagerWithCultureStringLocalizer`Klasa i `ResourceManagerStringLocalizer.WithCulture` Metoda są [przestarzałe w programie .NET Core 3,0 w wersji zapoznawczej 3 i nowszych](../../3.0.md#localization-resourcemanagerwithculturestringlocalizer-and-withculture-marked-obsolete).

## <a name="new-behavior"></a>Nowe zachowanie

`ResourceManagerWithCultureStringLocalizer`Klasa i Metoda zostały `ResourceManagerStringLocalizer.WithCulture` usunięte w programie .NET 5,0 Preview 1. Aby uzyskać spis zmian wprowadzonych w programie, zobacz żądanie ściągnięcia w programie [dotnet/Extensions # 2562](https://github.com/dotnet/extensions/pull/2562/files).

## <a name="reason-for-change"></a>Przyczyna zmiany

Metody [ResourceManagerWithCultureStringLocalizer](/dotnet/api/microsoft.extensions.localization.resourcemanagerwithculturestringlocalizer?view=dotnet-plat-ext-3.1) i [ResourceManagerStringLocalizer. WithCulture](/dotnet/api/microsoft.extensions.localization.resourcemanagerstringlocalizer.withculture?view=dotnet-plat-ext-3.1) często są źródłami pomyłek dla użytkowników lokalizacji. Pomyłka była szczególnie wysoka podczas tworzenia niestandardowej <xref:Microsoft.Extensions.Localization.IStringLocalizer> implementacji. Ta klasa i Metoda zapewniają konsumentom wrażenie, że `IStringLocalizer` wystąpienie jest oczekiwane na "dla poszczególnych zasobów". W rzeczywistości wystąpienie powinno mieć tylko wartość "dla zasobu". W czasie wykonywania <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=nameWithType> Właściwość określa język, który ma być używany.

## <a name="recommended-action"></a>Zalecana akcja

Zatrzymaj korzystanie z `ResourceManagerWithCultureStringLocalizer` klasy i `ResourceManagerStringLocalizer.WithCulture` metody.

## <a name="affected-apis"></a>Dotyczy interfejsów API

- [ResourceManagerWithCultureStringLocalizer](/dotnet/api/microsoft.extensions.localization.resourcemanagerwithculturestringlocalizer?view=dotnet-plat-ext-3.1)
- [ResourceManagerStringLocalizer.WithCulture](/dotnet/api/microsoft.extensions.localization.resourcemanagerstringlocalizer.withculture?view=dotnet-plat-ext-3.1)

<!--

### Category

ASP.NET Core

### Affected APIs

- `T:Microsoft.Extensions.Localization.ResourceManagerWithCultureStringLocalizer`
- `Overload:Microsoft.Extensions.Localization.ResourceManagerStringLocalizer.WithCulture`

-->
