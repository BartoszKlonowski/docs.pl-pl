---
title: Tworzenie architektury nowoczesnych aplikacji internetowych za pomocą platformy ASP.NET Core i platformy Azure
description: Przewodnik, który oferuje kompleksowe wskazówki dotyczące tworzenia monolitycznych aplikacji sieci Web przy użyciu ASP.NET Core i platformy Azure.
author: ardalis
ms.author: wiwagn
ms.date: 12/07/2020
ms.openlocfilehash: 90d092b2269315e5b6734430e82cc7211324479b
ms.sourcegitcommit: 45c7148f2483db2501c1aa696ab6ed2ed8cb71b2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/08/2020
ms.locfileid: "96851298"
---
# <a name="architect-modern-web-applications-with-aspnet-core-and-azure"></a>Tworzenie architektury nowoczesnych aplikacji internetowych za pomocą platformy ASP.NET Core i platformy Azure

![Obraz okładki książki nowoczesnej aplikacji sieci Web.](./media/index/web-application-guide-cover-image.png)

**Edition w wersji 5.0** — zaktualizowane do ASP.NET Core 5,0

Odwołaj się do [dziennika zmian](https://aka.ms/aspnet-ebook-changelog) dotyczących aktualizacji książki i wkładów społecznościowych.

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

Logo Docker Whale jest zastrzeżonym znakiem towarowym platformy Docker, Inc. używanym przez uprawnienie.

Wszystkie inne znaczniki i logo są własnością odpowiednich właścicieli.

Autor:

> **Steve "ardalis" Smith** — architekt oprogramowania i Trainer- [Ardalis.com](https://ardalis.com)

Edytory

> **Maira Wenzel**

## <a name="action-links"></a>Linki akcji

- Ta książka elektroniczna jest również dostępna w formacie PDF (tylko wersja w języku angielskim [).](https://aka.ms/webappebook)

- Klonowanie/rozwidlenie aplikacji referencyjnej [eShopOnWeb w witrynie GitHub](https://github.com/dotnet-architecture/eShopOnWeb)

## <a name="introduction"></a>Wprowadzenie

Program .NET 5 i ASP.NET Core oferują kilka korzyści w porównaniu z tradycyjnym programowaniem platformy .NET. Należy używać programu .NET 5 dla aplikacji serwerowych, jeśli niektóre lub wszystkie z następujących elementów są ważne dla sukcesu aplikacji:

- Obsługa wielu platform.

- Korzystanie z mikrousług.

- Korzystanie z kontenerów platformy Docker.

- Wymagania dotyczące wysokiej wydajności i skalowalności.

- Równoczesne przechowywanie wersji platformy .NET według aplikacji na tym samym serwerze.

Tradycyjne aplikacje .NET mogą i obsługują wiele z tych wymagań, ale ASP.NET Core i .NET 5 zostały zoptymalizowane w celu zapewnienia lepszej obsługi powyższych scenariuszy.

Więcej i więcej organizacji umożliwia hostowanie aplikacji sieci Web w chmurze przy użyciu usług takich jak Microsoft Azure. Należy rozważyć hosting aplikacji w chmurze, jeśli istnieją następujące istotne dla Twojej aplikacji lub organizacji:

- Zmniejszona inwestycja w koszty centrum danych (sprzęt, oprogramowanie, miejsce, narzędzia, zarządzanie serwerem itd.)

- Elastyczne ceny (płatność na podstawie użycia, nie do bezczynnej wydajności).

- Wysoka niezawodność.

- Lepsza mobilność aplikacji; łatwo zmieniaj miejsce i sposób wdrożenia aplikacji.

- Elastyczna pojemność; skalowanie w górę lub w dół na podstawie rzeczywistych potrzeb.

Tworzenie aplikacji sieci Web za pomocą ASP.NET Core hostowanych na platformie Azure oferuje wiele konkurencyjnych korzyści w porównaniu z tradycyjnymi alternatywami. ASP.NET Core jest zoptymalizowany pod kątem nowoczesnych rozwiązań do tworzenia aplikacji sieci Web i scenariuszy hostingu w chmurze. W tym przewodniku dowiesz się, jak zaprojektować ASP.NET Core aplikacje, aby najlepiej wykorzystać te możliwości.

## <a name="version"></a>Wersja

Ten przewodnik został zmieniony w celu uwzględnienia wersji **programu .net 5,0** wraz z wieloma dodatkowymi aktualizacjami związanymi z tym samymi "" Wave "technologiami (czyli platformą Azure i dodatkowymi technologiami innych firm), które są zgodne z wersją platformy .NET 5,0. Dlatego też wersja książki została zaktualizowana do wersji **5,0**.

## <a name="purpose"></a>Przeznaczenie

Ten przewodnik zawiera kompleksowe wskazówki dotyczące tworzenia *monolitycznych* aplikacji sieci Web przy użyciu ASP.NET Core i platformy Azure. W tym kontekście "monolityczne" odnosi się do faktu, że te aplikacje są wdrażane jako pojedyncza jednostka, nie jako kolekcja współpracujących usług i aplikacji.

Ten przewodnik uzupełnia ["_mikrousługi platformy .NET". Architektura dla kontenerów aplikacji .NET_](../microservices/index.md), które koncentrują się na platformach Docker, mikrousług i wdrażaniu kontenerów w celu hostowania aplikacji dla przedsiębiorstw.

### <a name="net-microservices-architecture-for-containerized-net-applications"></a>Mikrousługi platformy .NET. architektura konteneryzowanych aplikacji .NET

- **książka elektroniczna**  
  <https://aka.ms/MicroservicesEbook>
- **Przykładowa aplikacja**  
  <https://aka.ms/microservicesarchitecture>

## <a name="who-should-use-this-guide"></a>Kto powinien korzystać z tego przewodnika

Odbiorcy tego przewodnika są głównie deweloperzy, liderzy programistyczni i architektzy, którzy chcą tworzyć nowoczesne aplikacje sieci Web przy użyciu technologii i usług firmy Microsoft w chmurze.

Dodatkowymi odbiorcami są osoby podejmujące decyzje techniczne, które już znają ASP.NET lub platformę Azure i poszukują informacji na temat tego, czy warto przeprowadzić uaktualnienie do ASP.NET Core dla nowych lub istniejących projektów.

## <a name="how-you-can-use-this-guide"></a>Jak można użyć tego przewodnika

Ten przewodnik został skrócony do stosunkowo małego dokumentu, który koncentruje się na tworzeniu aplikacji sieci Web przy użyciu nowoczesnych technologii .NET i platformy Azure. W związku z tym może być odczytany w całości, aby zapewnić podstawę interpretacji takich aplikacji i ich zagadnień technicznych. Przewodnik wraz z przykładową aplikacją może również stanowić punkt początkowy lub odwołanie. Użyj skojarzonej przykładowej aplikacji jako szablonu dla własnych aplikacji lub, aby zobaczyć, w jaki sposób można organizować części składnika aplikacji. Zapoznaj się z artykułami dotyczącymi zasad i zakresu architektury i technologii oraz zagadnieniami dotyczącymi decyzji o tym, kiedy oceniasz wybór dla własnej aplikacji.

Możesz przesłać dalej ten przewodnik do zespołu, aby pomóc w zapewnieniu powszechnej wiedzy na temat tych zagadnień i możliwości. Korzystanie ze wspólnego zestawu terminologii i podstawowych zasad pomaga zapewnić spójne stosowanie wzorców i praktyk architektury.

## <a name="references"></a>Odwołania

- **Wybór między platformą .NET 5 i .NET Framework dla aplikacji serwerowych**  
  [https://docs.microsoft.com/dotnet/standard/choosing-core-framework-server](../../standard/choosing-core-framework-server.md)

>[!div class="step-by-step"]
>[Dalej](modern-web-applications-characteristics.md)
