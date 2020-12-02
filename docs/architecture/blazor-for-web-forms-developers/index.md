---
title: Blazor dla deweloperów ASP.NET Web Forms
description: Dowiedz się, jak tworzyć aplikacje sieci Web w pełnym stosie przy użyciu platformy .NET Blazor i platformy .NET Core w prosty i znany sposób.
author: danroth27
ms.author: daroth
no-loc:
- Blazor
- WebAssembly
ms.date: 12/01/2020
ms.openlocfilehash: 47f684e1b48ca95b8d999e6f1429840eb5f541de
ms.sourcegitcommit: 2f485e721f7f34b87856a51181b5b56624b31fd5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/02/2020
ms.locfileid: "96509770"
---
# <a name="no-locblazor-for-aspnet-web-forms-developers"></a>Blazor dla deweloperów ASP.NET Web Forms

![Zrzut ekranu przedstawiający centrum poczty elektronicznej aplikacji bezserwerowych.](./media/index/blazor-for-aspnet-web-forms-developers.png)

> Pobieranie dostępne o: <https://aka.ms/blazor-ebook>

**Wersja 1.0**

Odwołaj się do [dziennika zmian](https://aka.ms/blazor-ebook-changelog) dotyczących aktualizacji książki i wkładów społecznościowych.

OPUBLIKOWANA PRZEZ

Zespoły deweloperów firmy Microsoft, .NET i Visual Studio

Dział firmy Microsoft Corporation

One Microsoft Way

Redmond, Waszyngton 98052-6399

Prawa autorskie © 2020 przez firmę Microsoft Corporation

All rights reserved. Żadna część zawartości tej księgi nie może być odtwarzana ani przekazywana w żadnej formie ani za pomocą jakichkolwiek środków bez zgody na wydawcę.

Ta książka jest świadczona w postaci "AS-IS" i zawiera widoki i opinie autora. Widoki, opinie i informacje wyrażone w tej książce, w tym adresy URL i inne odwołania do witryn internetowych, mogą ulec zmianie bez powiadomienia.

Niektóre z przykładów przedstawiono wyłącznie do celów informacyjnych i są one fikcyjne. Żadne rzeczywiste skojarzenia lub związki nie są zamierzone ani wnioskowane.

Firma Microsoft i znaki towarowe wymienione na <https://www.microsoft.com> stronie "znaki towarowe" są znakami towarowymi grupy firm Microsoft.

Komputery Mac i macOS są znakami towarowymi firmy Apple Inc.

Wszystkie inne znaczniki i logo są własnością odpowiednich właścicieli.

Autorów

> **[Daniel Roth](https://github.com/danroth27)**, główny Menedżer programu, Microsoft Corp.

> **[Jan Fritz](https://github.com/csharpfritz)**, starszy kierownik ds. programów, Microsoft Corp.

> **[Southwick Taylor](https://github.com/twsouthwick)**, starszy inżynier ds. oprogramowania, Microsoft Corp.

> **[Scott Addie](https://github.com/scottaddie)**, Starszy programista ds. zawartości, Microsoft Corp.

> **[Steve "ardalis" Smith](https://ardalis.com)**, architekt oprogramowania i Trainer, ARDALIS Services LLC

## <a name="introduction"></a>Wprowadzenie

Platforma .NET ma długotrwałe Programowanie aplikacji sieci Web za pomocą ASP.NET, kompleksowego zestawu Platform i narzędzi do tworzenia dowolnego rodzaju aplikacji sieci Web. ASP.NET ma własne elementy platformy sieci Web i technologii, które zaczynają cały sposób z klasycznymi Active Server stronami (ASP). Struktury, takie jak ASP.NET Web Forms, ASP.NET MVC, ASP.NET Web Pages i ostatnio ASP.NET Core, zapewniają wydajny i wydajny sposób kompilowania aplikacji sieci Web *renderowanych na serwerze* , w przypadku których zawartość interfejsu użytkownika jest generowana dynamicznie na serwerze w odpowiedzi na żądania HTTP. Każdy ASP.NET Framework jest przeznaczony dla różnych grup odbiorców i tworzenia aplikacji. ASP.NET formularze sieci Web dostarczane z oryginalną wersją .NET Framework i obsługują programowanie w sieci Web przy użyciu wielu wzorców, które są znane dla deweloperów komputerów, takich jak kontrolki interfejsu użytkownika wielokrotnego użytku z prostą obsługą zdarzeń. Żadna z ofert ASP.NET nie umożliwia jednak uruchamiania kodu, który jest wykonywany w przeglądarce użytkownika. Aby to zrobić, należy napisać kod JavaScript i korzystać z dowolnej z wielu platform i narzędzi języka JavaScript, które są stopniowane i niepopularne w latach: jQuery, odcinania, kątowy, reagowanie i tak dalej.

[Blazor](https://blazor.net) to nowa platforma sieci Web, która zmienia możliwości podczas kompilowania aplikacji sieci Web za pomocą platformy .NET. Blazor to struktura interfejsu użytkownika sieci Web po stronie klienta oparta na języku C# zamiast języka JavaScript. Za pomocą Blazor programu można napisać składniki logiki i interfejsu użytkownika po stronie klienta w języku C#, skompilować je do normalnych zestawów .NET, a następnie uruchomić je bezpośrednio w przeglądarce przy użyciu nowego otwartego standardu sieci Web o nazwie WebAssembly . Program może również Blazor uruchamiać składniki interfejsu użytkownika platformy .NET na serwerze i obsługiwać wszystkie interakcje interfejsu użytkownika w czasie rzeczywistym za pośrednictwem przeglądarki. W przypadku sparowania z platformą .NET działającą na serwerze program Blazor umożliwia tworzenie aplikacji sieci Web na całym stosie przy użyciu platformy .NET. BlazorUdziały wielu commonalities z formularzami ASP.NET sieci Web, takimi jak posiadanie modelu składników wielokrotnego użytku, i prosty sposób obsługi zdarzeń użytkowników, również kompilują się z podstaw platformy .NET, aby zapewnić nowoczesne i wysoce wydajne środowisko programistyczne dla sieci Web.

W tej książce wprowadzono ASP.NET deweloperów formularzy sieci Web Blazor w sposób, który jest znany i wygodny. Wprowadzają one Blazor koncepcje równolegle z podobnymi koncepcjami w formularzach sieci Web ASP.NET, a także objaśniają nowe koncepcje, które mogą być mniej znane. Obejmuje szeroki zakres tematów i problemów, w tym Tworzenie składników, kierowanie, układ, konfigurację i zabezpieczenia. Natomiast zawartość tej książki jest przede wszystkim przeznaczona do włączenia nowego opracowywania, a także zawiera wytyczne i strategie dotyczące migrowania istniejących formularzy sieci Web ASP.NET do Blazor programu, gdy użytkownik chce przeprowadzić modernizację istniejącej aplikacji.

## <a name="who-should-use-the-book"></a>Kto powinien korzystać z książki

Ta książka jest przeznaczony dla deweloperów ASP.NET Web Forms poszukujących wprowadzenia do usługi Blazor , która odnosi się do istniejącej wiedzy i umiejętności. Ta książka może pomóc szybko rozpocząć pracę nad nowym projektem lub pomóc w założeniu planu Blazor modernizacji istniejącej aplikacji ASP.NET Web Forms.

## <a name="how-to-use-the-book"></a>Jak korzystać z książki

Pierwsza część tej książki obejmuje co Blazor to jest i porównuje ją z programowaniem aplikacji sieci Web za pomocą formularzy sieci web ASP.NET. Książka obejmuje Blazor również różne tematy, rozdział według rozdziałów i wiąże poszczególne Blazor koncepcje z odpowiednim koncepcją w postaci ASP.NET Web Forms lub wyjaśnia wszystkie zupełnie nowe koncepcje. Książka często odwołuje się również do kompletnej przykładowej aplikacji zaimplementowanej zarówno w ASP.NET Web Forms, jak i Blazor demonstrującej Blazor funkcje oraz w celu zapewnienia analizy przypadku migracji z formularzy sieci Web ASP.NET do programu Blazor . Obie implementacje przykładowej aplikacji (ASP.NET Web Forms i Blazor wersje) można znaleźć w witrynie [GitHub](https://github.com/dotnet-architecture/eshoponblazor).

## <a name="what-this-book-doesnt-cover"></a>Czym nie obejmuje ta książka

Ta książka stanowi wprowadzenie do Blazor , a nie kompleksowego przewodnika migracji. Chociaż zawiera ona wskazówki dotyczące sposobu podejścia do migracji projektu z formularzy sieci Web ASP.NET do programu Blazor , nie jest podejmowana próba pozyskania wszystkich Nuance i szczegółów. Aby uzyskać bardziej ogólne wskazówki dotyczące migracji z programu ASP.NET do ASP.NET Core, zapoznaj się ze [wskazówkami](/aspnet/core/migration/proper-to-2x/) dotyczącymi migracji w dokumentacji ASP.NET Core.

### <a name="additional-resources"></a>Dodatkowe zasoby

Oficjalną Blazor stronę główną i dokumentację można znaleźć pod adresem <https://blazor.net> .

## <a name="send-your-feedback"></a>Wyślij opinię

Ta książka i powiązane przykłady są ciągle zmieniane, dzięki czemu Twoje opinie są gotowe! Jeśli masz komentarze dotyczące sposobu, w jaki można ulepszyć tę książkę, Skorzystaj z sekcji opinia w dolnej części strony utworzonej w witrynie [GitHub](https://github.com/dotnet/docs/issues).

>[!div class="step-by-step"]
>[Dalej](introduction.md)
