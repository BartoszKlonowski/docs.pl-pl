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
# <a name="architect-modern-web-applications-with-aspnet-core-and-azure"></a><span data-ttu-id="7e484-103">Tworzenie architektury nowoczesnych aplikacji internetowych za pomocą platformy ASP.NET Core i platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7e484-103">Architect Modern Web Applications with ASP.NET Core and Azure</span></span>

![Obraz okładki książki nowoczesnej aplikacji sieci Web.](./media/index/web-application-guide-cover-image.png)

<span data-ttu-id="7e484-105">**Edition w wersji 5.0** — zaktualizowane do ASP.NET Core 5,0</span><span class="sxs-lookup"><span data-stu-id="7e484-105">**EDITION v5.0** - Updated to ASP.NET Core 5.0</span></span>

<span data-ttu-id="7e484-106">Odwołaj się do [dziennika zmian](https://aka.ms/aspnet-ebook-changelog) dotyczących aktualizacji książki i wkładów społecznościowych.</span><span class="sxs-lookup"><span data-stu-id="7e484-106">Refer [changelog](https://aka.ms/aspnet-ebook-changelog) for the book updates and community contributions.</span></span>

<span data-ttu-id="7e484-107">OPUBLIKOWANA PRZEZ</span><span class="sxs-lookup"><span data-stu-id="7e484-107">PUBLISHED BY</span></span>

<span data-ttu-id="7e484-108">Zespoły deweloperów firmy Microsoft, .NET i Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7e484-108">Microsoft Developer Division, .NET, and Visual Studio product teams</span></span>

<span data-ttu-id="7e484-109">Dział firmy Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="7e484-109">A division of Microsoft Corporation</span></span>

<span data-ttu-id="7e484-110">One Microsoft Way</span><span class="sxs-lookup"><span data-stu-id="7e484-110">One Microsoft Way</span></span>

<span data-ttu-id="7e484-111">Redmond, Waszyngton 98052-6399</span><span class="sxs-lookup"><span data-stu-id="7e484-111">Redmond, Washington 98052-6399</span></span>

<span data-ttu-id="7e484-112">Prawa autorskie © 2020 przez firmę Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="7e484-112">Copyright © 2020 by Microsoft Corporation</span></span>

<span data-ttu-id="7e484-113">All rights reserved.</span><span class="sxs-lookup"><span data-stu-id="7e484-113">All rights reserved.</span></span> <span data-ttu-id="7e484-114">Żadna część zawartości tej księgi nie może być odtwarzana ani przekazywana w żadnej formie ani za pomocą jakichkolwiek środków bez zgody na wydawcę.</span><span class="sxs-lookup"><span data-stu-id="7e484-114">No part of the contents of this book may be reproduced or transmitted in any form or by any means without the written permission of the publisher.</span></span>

<span data-ttu-id="7e484-115">Ta książka jest świadczona w postaci "AS-IS" i zawiera widoki i opinie autora.</span><span class="sxs-lookup"><span data-stu-id="7e484-115">This book is provided "as-is" and expresses the author's views and opinions.</span></span> <span data-ttu-id="7e484-116">Widoki, opinie i informacje wyrażone w tej książce, w tym adresy URL i inne odwołania do witryn internetowych, mogą ulec zmianie bez powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="7e484-116">The views, opinions, and information expressed in this book, including URL and other Internet website references, may change without notice.</span></span>

<span data-ttu-id="7e484-117">Niektóre z przykładów przedstawiono wyłącznie do celów informacyjnych i są one fikcyjne.</span><span class="sxs-lookup"><span data-stu-id="7e484-117">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="7e484-118">Żadne rzeczywiste skojarzenia lub związki nie są zamierzone ani wnioskowane.</span><span class="sxs-lookup"><span data-stu-id="7e484-118">No real association or connection is intended or should be inferred.</span></span>

<span data-ttu-id="7e484-119">Firma Microsoft i znaki towarowe wymienione na <https://www.microsoft.com> stronie "znaki towarowe" są znakami towarowymi grupy firm Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7e484-119">Microsoft and the trademarks listed at <https://www.microsoft.com> on the "Trademarks" webpage are trademarks of the Microsoft group of companies.</span></span>

<span data-ttu-id="7e484-120">Komputery Mac i macOS są znakami towarowymi firmy Apple Inc.</span><span class="sxs-lookup"><span data-stu-id="7e484-120">Mac and macOS are trademarks of Apple Inc.</span></span>

<span data-ttu-id="7e484-121">Logo Docker Whale jest zastrzeżonym znakiem towarowym platformy Docker, Inc. używanym przez uprawnienie.</span><span class="sxs-lookup"><span data-stu-id="7e484-121">The Docker whale logo is a registered trademark of Docker, Inc. Used by permission.</span></span>

<span data-ttu-id="7e484-122">Wszystkie inne znaczniki i logo są własnością odpowiednich właścicieli.</span><span class="sxs-lookup"><span data-stu-id="7e484-122">All other marks and logos are property of their respective owners.</span></span>

<span data-ttu-id="7e484-123">Autor:</span><span class="sxs-lookup"><span data-stu-id="7e484-123">Author:</span></span>

> <span data-ttu-id="7e484-124">**Steve "ardalis" Smith** — architekt oprogramowania i Trainer- [Ardalis.com](https://ardalis.com)</span><span class="sxs-lookup"><span data-stu-id="7e484-124">**Steve "ardalis" Smith** - Software Architect and Trainer - [Ardalis.com](https://ardalis.com)</span></span>

<span data-ttu-id="7e484-125">Edytory</span><span class="sxs-lookup"><span data-stu-id="7e484-125">Editors:</span></span>

> <span data-ttu-id="7e484-126">**Maira Wenzel**</span><span class="sxs-lookup"><span data-stu-id="7e484-126">**Maira Wenzel**</span></span>

## <a name="action-links"></a><span data-ttu-id="7e484-127">Linki akcji</span><span class="sxs-lookup"><span data-stu-id="7e484-127">Action links</span></span>

- <span data-ttu-id="7e484-128">Ta książka elektroniczna jest również dostępna w formacie PDF (tylko wersja w języku angielskim [).](https://aka.ms/webappebook)</span><span class="sxs-lookup"><span data-stu-id="7e484-128">This e-book is also available in a PDF format (English version only) [Download](https://aka.ms/webappebook)</span></span>

- <span data-ttu-id="7e484-129">Klonowanie/rozwidlenie aplikacji referencyjnej [eShopOnWeb w witrynie GitHub](https://github.com/dotnet-architecture/eShopOnWeb)</span><span class="sxs-lookup"><span data-stu-id="7e484-129">Clone/Fork the reference application [eShopOnWeb on GitHub](https://github.com/dotnet-architecture/eShopOnWeb)</span></span>

## <a name="introduction"></a><span data-ttu-id="7e484-130">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="7e484-130">Introduction</span></span>

<span data-ttu-id="7e484-131">Program .NET 5 i ASP.NET Core oferują kilka korzyści w porównaniu z tradycyjnym programowaniem platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="7e484-131">.NET 5 and ASP.NET Core offer several advantages over traditional .NET development.</span></span> <span data-ttu-id="7e484-132">Należy używać programu .NET 5 dla aplikacji serwerowych, jeśli niektóre lub wszystkie z następujących elementów są ważne dla sukcesu aplikacji:</span><span class="sxs-lookup"><span data-stu-id="7e484-132">You should use .NET 5 for your server applications if some or all of the following are important to your application's success:</span></span>

- <span data-ttu-id="7e484-133">Obsługa wielu platform.</span><span class="sxs-lookup"><span data-stu-id="7e484-133">Cross-platform support.</span></span>

- <span data-ttu-id="7e484-134">Korzystanie z mikrousług.</span><span class="sxs-lookup"><span data-stu-id="7e484-134">Use of microservices.</span></span>

- <span data-ttu-id="7e484-135">Korzystanie z kontenerów platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="7e484-135">Use of Docker containers.</span></span>

- <span data-ttu-id="7e484-136">Wymagania dotyczące wysokiej wydajności i skalowalności.</span><span class="sxs-lookup"><span data-stu-id="7e484-136">High performance and scalability requirements.</span></span>

- <span data-ttu-id="7e484-137">Równoczesne przechowywanie wersji platformy .NET według aplikacji na tym samym serwerze.</span><span class="sxs-lookup"><span data-stu-id="7e484-137">Side-by-side versioning of .NET versions by application on the same server.</span></span>

<span data-ttu-id="7e484-138">Tradycyjne aplikacje .NET mogą i obsługują wiele z tych wymagań, ale ASP.NET Core i .NET 5 zostały zoptymalizowane w celu zapewnienia lepszej obsługi powyższych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="7e484-138">Traditional .NET applications can and do support many of these requirements, but ASP.NET Core and .NET 5 have been optimized to offer improved support for the above scenarios.</span></span>

<span data-ttu-id="7e484-139">Więcej i więcej organizacji umożliwia hostowanie aplikacji sieci Web w chmurze przy użyciu usług takich jak Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7e484-139">More and more organizations are choosing to host their web applications in the cloud using services like Microsoft Azure.</span></span> <span data-ttu-id="7e484-140">Należy rozważyć hosting aplikacji w chmurze, jeśli istnieją następujące istotne dla Twojej aplikacji lub organizacji:</span><span class="sxs-lookup"><span data-stu-id="7e484-140">You should consider hosting your application in the cloud if the following are important to your application or organization:</span></span>

- <span data-ttu-id="7e484-141">Zmniejszona inwestycja w koszty centrum danych (sprzęt, oprogramowanie, miejsce, narzędzia, zarządzanie serwerem itd.)</span><span class="sxs-lookup"><span data-stu-id="7e484-141">Reduced investment in data center costs (hardware, software, space, utilities, server management, etc.)</span></span>

- <span data-ttu-id="7e484-142">Elastyczne ceny (płatność na podstawie użycia, nie do bezczynnej wydajności).</span><span class="sxs-lookup"><span data-stu-id="7e484-142">Flexible pricing (pay based on usage, not for idle capacity).</span></span>

- <span data-ttu-id="7e484-143">Wysoka niezawodność.</span><span class="sxs-lookup"><span data-stu-id="7e484-143">Extreme reliability.</span></span>

- <span data-ttu-id="7e484-144">Lepsza mobilność aplikacji; łatwo zmieniaj miejsce i sposób wdrożenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7e484-144">Improved app mobility; easily change where and how your app is deployed.</span></span>

- <span data-ttu-id="7e484-145">Elastyczna pojemność; skalowanie w górę lub w dół na podstawie rzeczywistych potrzeb.</span><span class="sxs-lookup"><span data-stu-id="7e484-145">Flexible capacity; scale up or down based on actual needs.</span></span>

<span data-ttu-id="7e484-146">Tworzenie aplikacji sieci Web za pomocą ASP.NET Core hostowanych na platformie Azure oferuje wiele konkurencyjnych korzyści w porównaniu z tradycyjnymi alternatywami.</span><span class="sxs-lookup"><span data-stu-id="7e484-146">Building web applications with ASP.NET Core, hosted in Azure, offers many competitive advantages over traditional alternatives.</span></span> <span data-ttu-id="7e484-147">ASP.NET Core jest zoptymalizowany pod kątem nowoczesnych rozwiązań do tworzenia aplikacji sieci Web i scenariuszy hostingu w chmurze.</span><span class="sxs-lookup"><span data-stu-id="7e484-147">ASP.NET Core is optimized for modern web application development practices and cloud hosting scenarios.</span></span> <span data-ttu-id="7e484-148">W tym przewodniku dowiesz się, jak zaprojektować ASP.NET Core aplikacje, aby najlepiej wykorzystać te możliwości.</span><span class="sxs-lookup"><span data-stu-id="7e484-148">In this guide, you'll learn how to architect your ASP.NET Core applications to best take advantage of these capabilities.</span></span>

## <a name="version"></a><span data-ttu-id="7e484-149">Wersja</span><span class="sxs-lookup"><span data-stu-id="7e484-149">Version</span></span>

<span data-ttu-id="7e484-150">Ten przewodnik został zmieniony w celu uwzględnienia wersji **programu .net 5,0** wraz z wieloma dodatkowymi aktualizacjami związanymi z tym samymi "" Wave "technologiami (czyli platformą Azure i dodatkowymi technologiami innych firm), które są zgodne z wersją platformy .NET 5,0.</span><span class="sxs-lookup"><span data-stu-id="7e484-150">This guide has been revised to cover **.NET 5.0** version along with many additional updates related to the same "wave" of technologies (that is, Azure and additional third-party technologies) coinciding in time with the .NET 5.0 release.</span></span> <span data-ttu-id="7e484-151">Dlatego też wersja książki została zaktualizowana do wersji **5,0**.</span><span class="sxs-lookup"><span data-stu-id="7e484-151">That's why the book version has also been updated to version **5.0**.</span></span>

## <a name="purpose"></a><span data-ttu-id="7e484-152">Przeznaczenie</span><span class="sxs-lookup"><span data-stu-id="7e484-152">Purpose</span></span>

<span data-ttu-id="7e484-153">Ten przewodnik zawiera kompleksowe wskazówki dotyczące tworzenia *monolitycznych* aplikacji sieci Web przy użyciu ASP.NET Core i platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7e484-153">This guide provides end-to-end guidance on building *monolithic* web applications using ASP.NET Core and Azure.</span></span> <span data-ttu-id="7e484-154">W tym kontekście "monolityczne" odnosi się do faktu, że te aplikacje są wdrażane jako pojedyncza jednostka, nie jako kolekcja współpracujących usług i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7e484-154">In this context, "monolithic" refers to the fact that these applications are deployed as a single unit, not as a collection of interacting services and applications.</span></span>

<span data-ttu-id="7e484-155">Ten przewodnik uzupełnia ["_mikrousługi platformy .NET". Architektura dla kontenerów aplikacji .NET_](../microservices/index.md), które koncentrują się na platformach Docker, mikrousług i wdrażaniu kontenerów w celu hostowania aplikacji dla przedsiębiorstw.</span><span class="sxs-lookup"><span data-stu-id="7e484-155">This guide is complementary to ["_.NET Microservices. Architecture for Containerized .NET Applications_"](../microservices/index.md), which focuses more on Docker, microservices, and deployment of containers to host enterprise applications.</span></span>

### <a name="net-microservices-architecture-for-containerized-net-applications"></a><span data-ttu-id="7e484-156">Mikrousługi platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="7e484-156">.NET Microservices.</span></span> <span data-ttu-id="7e484-157">architektura konteneryzowanych aplikacji .NET</span><span class="sxs-lookup"><span data-stu-id="7e484-157">Architecture for Containerized .NET Applications</span></span>

- <span data-ttu-id="7e484-158">**książka elektroniczna**</span><span class="sxs-lookup"><span data-stu-id="7e484-158">**e-book**</span></span>  
  <https://aka.ms/MicroservicesEbook>
- <span data-ttu-id="7e484-159">**Przykładowa aplikacja**</span><span class="sxs-lookup"><span data-stu-id="7e484-159">**Sample Application**</span></span>  
  <https://aka.ms/microservicesarchitecture>

## <a name="who-should-use-this-guide"></a><span data-ttu-id="7e484-160">Kto powinien korzystać z tego przewodnika</span><span class="sxs-lookup"><span data-stu-id="7e484-160">Who should use this guide</span></span>

<span data-ttu-id="7e484-161">Odbiorcy tego przewodnika są głównie deweloperzy, liderzy programistyczni i architektzy, którzy chcą tworzyć nowoczesne aplikacje sieci Web przy użyciu technologii i usług firmy Microsoft w chmurze.</span><span class="sxs-lookup"><span data-stu-id="7e484-161">The audience for this guide is mainly developers, development leads, and architects who are interested in building modern web applications using Microsoft technologies and services in the cloud.</span></span>

<span data-ttu-id="7e484-162">Dodatkowymi odbiorcami są osoby podejmujące decyzje techniczne, które już znają ASP.NET lub platformę Azure i poszukują informacji na temat tego, czy warto przeprowadzić uaktualnienie do ASP.NET Core dla nowych lub istniejących projektów.</span><span class="sxs-lookup"><span data-stu-id="7e484-162">A secondary audience is technical decision makers who are already familiar ASP.NET or Azure and are looking for information on whether it makes sense to upgrade to ASP.NET Core for new or existing projects.</span></span>

## <a name="how-you-can-use-this-guide"></a><span data-ttu-id="7e484-163">Jak można użyć tego przewodnika</span><span class="sxs-lookup"><span data-stu-id="7e484-163">How you can use this guide</span></span>

<span data-ttu-id="7e484-164">Ten przewodnik został skrócony do stosunkowo małego dokumentu, który koncentruje się na tworzeniu aplikacji sieci Web przy użyciu nowoczesnych technologii .NET i platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7e484-164">This guide has been condensed into a relatively small document that focuses on building web applications with modern .NET technologies and Azure.</span></span> <span data-ttu-id="7e484-165">W związku z tym może być odczytany w całości, aby zapewnić podstawę interpretacji takich aplikacji i ich zagadnień technicznych.</span><span class="sxs-lookup"><span data-stu-id="7e484-165">As such, it can be read in its entirety to provide a foundation of understanding such applications and their technical considerations.</span></span> <span data-ttu-id="7e484-166">Przewodnik wraz z przykładową aplikacją może również stanowić punkt początkowy lub odwołanie.</span><span class="sxs-lookup"><span data-stu-id="7e484-166">The guide, along with its sample application, can also serve as a starting point or reference.</span></span> <span data-ttu-id="7e484-167">Użyj skojarzonej przykładowej aplikacji jako szablonu dla własnych aplikacji lub, aby zobaczyć, w jaki sposób można organizować części składnika aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7e484-167">Use the associated sample application as a template for your own applications, or to see how you might organize your application's component parts.</span></span> <span data-ttu-id="7e484-168">Zapoznaj się z artykułami dotyczącymi zasad i zakresu architektury i technologii oraz zagadnieniami dotyczącymi decyzji o tym, kiedy oceniasz wybór dla własnej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7e484-168">Refer back to the guide's principles and coverage of architecture and technology options and decision considerations when you're weighing these choices for your own application.</span></span>

<span data-ttu-id="7e484-169">Możesz przesłać dalej ten przewodnik do zespołu, aby pomóc w zapewnieniu powszechnej wiedzy na temat tych zagadnień i możliwości.</span><span class="sxs-lookup"><span data-stu-id="7e484-169">Feel free to forward this guide to your team to help ensure a common understanding of these considerations and opportunities.</span></span> <span data-ttu-id="7e484-170">Korzystanie ze wspólnego zestawu terminologii i podstawowych zasad pomaga zapewnić spójne stosowanie wzorców i praktyk architektury.</span><span class="sxs-lookup"><span data-stu-id="7e484-170">Having everybody working from a common set of terminology and underlying principles helps ensure consistent application of architectural patterns and practices.</span></span>

## <a name="references"></a><span data-ttu-id="7e484-171">Odwołania</span><span class="sxs-lookup"><span data-stu-id="7e484-171">References</span></span>

- <span data-ttu-id="7e484-172">**Wybór między platformą .NET 5 i .NET Framework dla aplikacji serwerowych**</span><span class="sxs-lookup"><span data-stu-id="7e484-172">**Choosing between .NET 5 and .NET Framework for server apps**</span></span>  
  [https://docs.microsoft.com/dotnet/standard/choosing-core-framework-server](../../standard/choosing-core-framework-server.md)

>[!div class="step-by-step"]
>[<span data-ttu-id="7e484-173">Dalej</span><span class="sxs-lookup"><span data-stu-id="7e484-173">Next</span></span>](modern-web-applications-characteristics.md)
