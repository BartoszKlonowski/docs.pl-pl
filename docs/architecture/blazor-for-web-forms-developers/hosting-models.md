---
title: Modele hostingu aplikacji Blazor
description: Poznaj różne sposoby hostowania aplikacji Blazor, w tym w przeglądarce w zestawie webassembly lub na serwerze.
author: danroth27
ms.author: daroth
ms.date: 09/11/2019
ms.openlocfilehash: 82628976bcb1f1cee3089aa25488396af44d0f1a
ms.sourcegitcommit: 4f4a32a5c16a75724920fa9627c59985c41e173c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2019
ms.locfileid: "72520298"
---
# <a name="blazor-app-hosting-models"></a>Modele hostingu aplikacji Blazor

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

Aplikacje Blazor mogą być hostowane w usługach IIS, podobnie jak aplikacje ASP.NET Web Forms. Aplikacje Blazor mogą być również hostowane w jeden z następujących sposobów:

- Po stronie klienta w przeglądarce w programie webassembly.
- Po stronie serwera w aplikacji ASP.NET Core. 

## <a name="blazor-webassembly-apps"></a>Blazor aplikacje webassembly

Blazor aplikacje webassembly są wykonywane bezpośrednio w przeglądarce w środowisku uruchomieniowym .NET opartym na zestawie. Blazor aplikacje webassembly działają w podobny sposób do platform języka JavaScript frontonu, takich jak kątowy lub reagowanie. Jednak zamiast pisania kodu JavaScript, należy napisać C#. Środowisko uruchomieniowe platformy .NET jest pobierane wraz z aplikacją wraz z zestawem aplikacji i wszystkimi wymaganymi zależnościami. Nie są wymagane żadne wtyczki ani rozszerzenia przeglądarki. 

Pobrane zestawy są normalnymi zestawami .NET, tak jak w przypadku innych aplikacji platformy .NET. Ponieważ środowisko uruchomieniowe obsługuje .NET Standard, można użyć istniejących bibliotek .NET Standard z aplikacją Blazor webassembly. Jednak te zestawy będą nadal wykonywane w piaskownicy zabezpieczeń przeglądarki. Niektóre funkcje mogą zgłosić <xref:System.PlatformNotSupportedException>, takich jak próba uzyskania dostępu do systemu plików lub otwarcie dowolnych połączeń sieciowych. 

Po załadowaniu aplikacji środowisko uruchomieniowe platformy .NET jest uruchamiane i wskazywane w zestawie aplikacji. Zostanie uruchomiona logika uruchamiania aplikacji i są renderowane składniki główne. Blazor oblicza aktualizacje interfejsu użytkownika w oparciu o renderowane dane wyjściowe ze składników. Następnie są stosowane aktualizacje modelu DOM.

![Zestaw WebAssembly Blazor](media/hosting-models/blazor-webassembly.png)

Blazor aplikacje webassembly działają czysto po stronie klienta. Takie aplikacje można wdrażać w ramach rozwiązań do hostingu witryn statycznych, takich jak strony usługi GitHub lub hostowanie statycznej witryny sieci Web platformy Azure. Platforma .NET nie jest wymagana na serwerze. Głębokie łączenie z częściami aplikacji zwykle wymaga rozwiązania routingu na serwerze. Rozwiązanie do routingu przekierowuje żądania do katalogu głównego aplikacji. Na przykład to przekierowanie może być obsługiwane przy użyciu reguł ponownego zapisywania adresów URL w usługach IIS.

Aby uzyskać wszystkie korzyści wynikające z Blazor i opracowywania aplikacji sieci Web w pełnym stosie, należy hostować aplikację webassembly Blazor przy użyciu ASP.NET Core. Korzystając z platformy .NET zarówno na kliencie, jak i na serwerze, można łatwo udostępniać kod i kompilować swoją aplikację przy użyciu jednego spójnego zestawu języków, struktur i narzędzi. Blazor udostępnia wygodne szablony służące do konfigurowania rozwiązania, które zawiera aplikację webassembly Blazor i projekt hosta ASP.NET Core. Po skompilowaniu rozwiązania skompilowane pliki statyczne z aplikacji Blazor są hostowane przez aplikację ASP.NET Core przy użyciu już skonfigurowanego routingu rezerwowego.

## <a name="blazor-server-apps"></a>Aplikacje serwera Blazor

Odwołaj się z dyskusji [architektury Blazor](architecture-comparison.md#blazor) , że składniki Blazor renderują swoje dane wyjściowe do pośredniego abstrakcji o nazwie `RenderTree`. Blazor Framework następnie porównuje elementy renderowane z wcześniej renderowanymi informacjami. Różnice są stosowane do modelu DOM. Składniki Blazor są oddzielone od sposobu zastosowania ich renderowanych danych wyjściowych. W związku z tym same składniki nie muszą działać w tym samym procesie co proces aktualizowania interfejsu użytkownika. W rzeczywistości nie trzeba nawet uruchamiać ich na tym samym komputerze.

W aplikacjach serwera Blazor składniki są uruchamiane na serwerze, a nie po stronie klienta w przeglądarce. Zdarzenia interfejsu użytkownika, które wystąpiły w przeglądarce, są wysyłane do serwera przez połączenie w czasie rzeczywistym. Zdarzenia są wysyłane do poprawnych wystąpień składników. Składniki są renderowane i obliczeniowy różnic interfejsu użytkownika jest serializowany i wysyłany do przeglądarki, w której jest zastosowany do modelu DOM.

![Serwer Blazor](media/hosting-models/blazor-server.png)

Model hostingu serwera Blazor może dźwiękować, jeśli użyto ASP.NET AJAX i kontrolki <xref:System.Web.UI.UpdatePanel>. Kontrolka `UpdatePanel` obsługuje stosowanie aktualizacji stron częściowych w odpowiedzi na zdarzenia wyzwalające na stronie. Gdy jest wyzwalane, `UpdatePanel` żąda aktualizacji częściowej, a następnie stosuje ją bez konieczności odświeżania strony. Stan interfejsu użytkownika jest zarządzany przy użyciu `ViewState`. Aplikacje serwera Blazor są nieco inne w przypadku, gdy aplikacja wymaga aktywnego połączenia z klientem. Ponadto na serwerze jest zachowywany cały stan interfejsu użytkownika. Oprócz tych różnic te dwa modele są koncepcyjnie podobne.

## <a name="how-to-choose-the-right-blazor-hosting-model"></a>Jak wybrać odpowiedni model hostingu Blazor

Zgodnie z opisem w dokumentacji dotyczącej [modelu hostingu Blazor](https://docs.microsoft.com/aspnet/core/blazor/hosting-models#server-side)różne modele hostingu Blazor mają różne kompromisy.

Model hostingu zestawu webBlazor ma następujące zalety:

- Nie istnieje zależność po stronie serwera .NET. Aplikacja jest w pełni funkcjonalna po pobraniu do klienta programu.
- Zasoby i możliwości klienta są w pełni wykorzystywane.
- Zadania są Odciążone z serwera do klienta programu.
- Serwer sieci Web ASP.NET Core nie jest wymagany do hostowania aplikacji. Możliwe są scenariusze wdrażania bezserwerowego (na przykład obsługujące aplikację z sieci CDN).

Downsides modelu hostingu Blazor webassembly:

- Możliwości przeglądarki ograniczają aplikację.
- Wymagany jest sprzęt i oprogramowanie klienta (na przykład obsługa zestawu webassembly).
- Rozmiar pobieranych plików jest większy i ładowanie aplikacji trwa dłużej.
- Środowisko uruchomieniowe platformy .NET i obsługa narzędzi są mniej dojrzałe. Na przykład istnieją ograniczenia dotyczące obsługi [.NET Standard](../../standard/net-standard.md) i debugowania.

Z drugiej strony model hostingu serwera Blazor oferuje następujące korzyści:

- Rozmiar pobieranych plików jest znacznie mniejszy niż aplikacja po stronie klienta, a aplikacja jest znacznie szybsza.
- Aplikacja w pełni wykorzystuje możliwości serwera, w tym używanie dowolnego interfejsu API zgodnego z platformą .NET Core.
- Program .NET Core na serwerze jest używany do uruchamiania aplikacji, więc istniejące narzędzia platformy .NET, takie jak debugowanie, działają zgodnie z oczekiwaniami.
- Klienci zubożoni są obsługiwani. Na przykład aplikacje po stronie serwera współpracują z przeglądarkami, które nie obsługują zestawu webassembly i na urządzeniach z ograniczeniami zasobów.
- Baza danych platformy .NET/C# kodu aplikacji, w tym kod składnika aplikacji, nie jest obsługiwana dla klientów.

Downsides do modelu hostingu serwera Blazor są następujące:

- Wyższe opóźnienia interfejsu użytkownika. Każda interakcja użytkownika obejmuje przeskok sieci.
- Brak obsługi offline. Jeśli połączenie z klientem zakończy się niepowodzeniem, aplikacja przestanie działać.
- Skalowalność jest wyzwaniem dla aplikacji z wieloma użytkownikami. Serwer musi zarządzać wieloma połączeniami klientów i obsługiwać stan klienta.
- Do obsłużynia aplikacji wymagany jest serwer ASP.NET Core. Scenariusze wdrażania bez użycia serwera nie są możliwe. Nie można na przykład udostępniać aplikacji z sieci CDN.

Poprzednia lista zalet może być zastraszanie, ale model hostingu można później zmienić. Bez względu na wybrany model hostingu Blazor model składnika jest *taki sam*. W zasadzie te same składniki mogą być używane z modelem hostingu. Kod aplikacji nie zmienia się; jednak dobrym sposobem jest wprowadzenie abstrakcji, tak aby składniki nadal miały model hostingu — niezależny od. Streszczenia umożliwiają aplikacji łatwiejsze wdrażanie innego modelu hostingu.

## <a name="deploy-your-app"></a>Wdrażanie aplikacji

Aplikacje ASP.NET Web Forms są zwykle hostowane w usługach IIS na komputerze lub w klastrze z systemem Windows Server. Aplikacje Blazor mogą również:

- Być hostowane w usługach IIS, jako pliki statyczne lub jako aplikacja ASP.NET Core.
- Skorzystaj z elastyczności ASP.NET Core, która ma być hostowana na różnych platformach i infrastrukturach serwerów. Na przykład możesz hostować aplikację Blazor przy użyciu usługi [Nginx](/aspnet/core/host-and-deploy/linux-nginx) lub [Apache](/aspnet/core/host-and-deploy/linux-apache) w systemie Linux. Więcej informacji o sposobach publikowania i wdrażania aplikacji Blazor znajduje się w dokumentacji [hostingu i wdrażania](/aspnet/core/host-and-deploy/blazor/) Blazor.

W następnej sekcji dowiesz się, jak są skonfigurowane projekty dla aplikacji Blazor webassembly i Blazor Server.

>[!div class="step-by-step"]
>[Poprzedni](architecture-comparison.md)
>[Następny](project-structure.md)
