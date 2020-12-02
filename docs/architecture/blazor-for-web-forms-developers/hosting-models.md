---
title: Blazor modele hostingu aplikacji
description: Poznaj różne sposoby hostowania Blazor aplikacji, w tym przeglądarki w systemie WebAssembly lub na serwerze.
author: danroth27
ms.author: daroth
no-loc:
- Blazor
- WebAssembly
ms.date: 11/20/2020
ms.openlocfilehash: 5d80b28642ee1e975d334f89504a1748d13dea8f
ms.sourcegitcommit: 2f485e721f7f34b87856a51181b5b56624b31fd5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/02/2020
ms.locfileid: "96509783"
---
# <a name="no-locblazor-app-hosting-models"></a>Blazor modele hostingu aplikacji

Blazor aplikacje mogą być hostowane w usługach IIS, podobnie jak aplikacje ASP.NET Web Forms. Blazor aplikacje mogą być również hostowane w jeden z następujących sposobów:

- Po stronie klienta w przeglądarce WebAssembly .
- Po stronie serwera w aplikacji ASP.NET Core.

## <a name="no-locblazor-no-locwebassembly-apps"></a>BlazorWebAssemblyaplikacje

BlazorWebAssemblyaplikacje są wykonywane bezpośrednio w przeglądarce w WebAssembly środowisku uruchomieniowym .NET opartym na systemie. BlazorWebAssemblyFunkcja Apps w podobny sposób do platform języka JavaScript frontonu, takich jak kątowy lub reagowanie. Jednak zamiast pisania kodu JavaScript napisanego w języku C#. Środowisko uruchomieniowe platformy .NET jest pobierane wraz z aplikacją wraz z zestawem aplikacji i wszystkimi wymaganymi zależnościami. Nie są wymagane żadne wtyczki ani rozszerzenia przeglądarki.

Pobrane zestawy są normalnymi zestawami .NET, tak jak w przypadku innych aplikacji platformy .NET. Ponieważ środowisko uruchomieniowe obsługuje .NET Standard, możesz użyć istniejących bibliotek .NET Standard z Blazor WebAssembly aplikacją. Jednak te zestawy będą nadal wykonywane w piaskownicy zabezpieczeń przeglądarki. Niektóre funkcje mogą zgłosić <xref:System.PlatformNotSupportedException> , takie jak próba uzyskania dostępu do systemu plików lub otwarcie dowolnych połączeń sieciowych.

Po załadowaniu aplikacji środowisko uruchomieniowe platformy .NET jest uruchamiane i wskazywane w zestawie aplikacji. Zostanie uruchomiona logika uruchamiania aplikacji i są renderowane składniki główne. Blazor oblicza aktualizacje interfejsu użytkownika w oparciu o renderowane dane wyjściowe ze składników. Następnie są stosowane aktualizacje modelu DOM.

![::: No-Loc (Blazor):::;:: No-Loc (webassembly)::](media/hosting-models/blazor-webassembly.png)

BlazorWebAssemblyaplikacje są uruchamiane czysto po stronie klienta. Takie aplikacje można wdrażać w ramach rozwiązań do hostingu witryn statycznych, takich jak strony usługi GitHub lub hostowanie statycznej witryny sieci Web platformy Azure. Platforma .NET nie jest wymagana na serwerze. Głębokie łączenie z częściami aplikacji zwykle wymaga rozwiązania routingu na serwerze. Rozwiązanie do routingu przekierowuje żądania do katalogu głównego aplikacji. Na przykład to przekierowanie może być obsługiwane przy użyciu reguł ponownego zapisywania adresów URL w usługach IIS.

Aby uzyskać wszystkie zalety Blazor platformy .NET Web Development i pełnego stosu, zapoznaj Blazor WebAssembly się z aplikacją za pomocą ASP.NET Core. Korzystając z platformy .NET zarówno na kliencie, jak i na serwerze, można łatwo udostępniać kod i kompilować swoją aplikację przy użyciu jednego spójnego zestawu języków, struktur i narzędzi. Blazor oferuje wygodne szablony służące do konfigurowania rozwiązania, które zawiera zarówno Blazor WebAssembly aplikację, jak i projekt hosta ASP.NET Core. Po skompilowaniu rozwiązania skompilowane pliki statyczne z Blazor aplikacji są hostowane przez aplikację ASP.NET Core przy użyciu już skonfigurowanego routingu rezerwowego.

## <a name="no-locblazor-server-apps"></a>Blazor Aplikacje serwera

Odwołaj się z dyskusji o [ Blazor architekturze](architecture-comparison.md#blazor) , że Blazor składniki renderują swoje dane wyjściowe do pośredniego abstrakcji o nazwie a `RenderTree` . BlazorStruktura następnie porównuje elementy renderowane z wcześniej renderowanymi informacjami. Różnice są stosowane do modelu DOM. Blazor składniki są oddzielone od sposobu zastosowania ich renderowanych danych wyjściowych. W związku z tym same składniki nie muszą działać w tym samym procesie co proces aktualizowania interfejsu użytkownika. W rzeczywistości nie trzeba nawet uruchamiać ich na tym samym komputerze.

W obszarze Blazor aplikacje serwera składniki są uruchamiane na serwerze, a nie po stronie klienta w przeglądarce. Zdarzenia interfejsu użytkownika, które wystąpiły w przeglądarce, są wysyłane do serwera przez połączenie w czasie rzeczywistym. Zdarzenia są wysyłane do poprawnych wystąpień składników. Składniki są renderowane i obliczeniowy różnic interfejsu użytkownika jest serializowany i wysyłany do przeglądarki, w której jest zastosowany do modelu DOM.

![::: No-Loc (Blazor)::: serwer](media/hosting-models/blazor-server.png)

BlazorModel hostingu serwera może dźwiękować, jeśli użyto ASP.NET AJAX i <xref:System.Web.UI.UpdatePanel> kontrolki. `UpdatePanel`Kontrolka obsługuje stosowanie aktualizacji stron częściowych w odpowiedzi na zdarzenia wyzwalające na stronie. Gdy jest wyzwalane, `UpdatePanel` żąda aktualizacji częściowej, a następnie stosuje ją bez konieczności odświeżania strony. Stan interfejsu użytkownika jest zarządzany przy użyciu programu `ViewState` . Blazor Aplikacje serwera różnią się nieco w zależności od tego, że aplikacja wymaga aktywnego połączenia z klientem. Ponadto na serwerze jest zachowywany cały stan interfejsu użytkownika. Oprócz tych różnic te dwa modele są koncepcyjnie podobne.

## <a name="how-to-choose-the-right-no-locblazor-hosting-model"></a>Jak wybrać odpowiedni Blazor model hostingu

Zgodnie z opisem w dokumentacji dotyczącej [ Blazor modelu hostingu](/aspnet/core/blazor/hosting-models)różne Blazor modele hostingu mają różne kompromisy.

Blazor WebAssembly Model hostingu ma następujące zalety:

- Nie istnieje zależność po stronie serwera .NET. Aplikacja jest w pełni funkcjonalna po pobraniu do klienta programu.
- Zasoby i możliwości klienta są w pełni wykorzystywane.
- Zadania są Odciążone z serwera do klienta programu.
- Serwer sieci Web ASP.NET Core nie jest wymagany do hostowania aplikacji. Możliwe są scenariusze wdrażania bezserwerowego (na przykład obsługujące aplikację z sieci CDN).

Downsides Blazor WebAssembly modelu hostingu:

- Możliwości przeglądarki ograniczają aplikację.
- Wymagany jest sprzęt i oprogramowanie klienta (na przykład WebAssembly Pomoc techniczna).
- Rozmiar pobieranych plików jest większy i ładowanie aplikacji trwa dłużej.
- Środowisko uruchomieniowe platformy .NET i obsługa narzędzi są mniej dojrzałe. Na przykład istnieją ograniczenia dotyczące obsługi [.NET Standard](../../standard/net-standard.md) i debugowania.

Z drugiej strony Blazor model hostingu serwera oferuje następujące korzyści:

- Rozmiar pobieranych plików jest znacznie mniejszy niż aplikacja po stronie klienta, a aplikacja jest znacznie szybsza.
- Aplikacja w pełni wykorzystuje możliwości serwera, łącznie z użyciem wszelkich zgodnych interfejsów API platformy .NET.
- Program .NET na serwerze jest używany do uruchamiania aplikacji, więc istniejące narzędzia platformy .NET, takie jak debugowanie, działają zgodnie z oczekiwaniami.
- Klienci zubożoni są obsługiwani. Na przykład aplikacje po stronie serwera współpracują z przeglądarkami, które nie obsługują WebAssembly i na urządzeniach z ograniczeniami zasobów.
- Baza kodu platformy .NET/C#, w tym kod składnika aplikacji, nie jest obsługiwana dla klientów.

Downsides do Blazor modelu hostingu serwera są następujące:

- Wyższe opóźnienia interfejsu użytkownika. Każda interakcja użytkownika obejmuje przeskok sieci.
- Brak obsługi offline. Jeśli połączenie z klientem zakończy się niepowodzeniem, aplikacja przestanie działać.
- Skalowalność jest wyzwaniem dla aplikacji z wieloma użytkownikami. Serwer musi zarządzać wieloma połączeniami klientów i obsługiwać stan klienta.
- Do obsłużynia aplikacji wymagany jest serwer ASP.NET Core. Scenariusze wdrażania bez użycia serwera nie są możliwe. Nie można na przykład udostępniać aplikacji z sieci CDN.

Poprzednia lista zalet może być zastraszanie, ale model hostingu można później zmienić. Niezależnie od Blazor wybranego modelu hostingu model składnika jest *taki sam*. W zasadzie te same składniki mogą być używane z modelem hostingu. Kod aplikacji nie zmienia się; jednak dobrym sposobem jest wprowadzenie abstrakcji, tak aby składniki nadal miały model hostingu — niezależny od. Streszczenia umożliwiają aplikacji łatwiejsze wdrażanie innego modelu hostingu.

## <a name="deploy-your-app"></a>Wdrażanie aplikacji

Aplikacje ASP.NET Web Forms są zwykle hostowane w usługach IIS na komputerze lub w klastrze z systemem Windows Server. Blazor aplikacje mogą również:

- Być hostowane w usługach IIS, jako pliki statyczne lub jako aplikacja ASP.NET Core.
- Skorzystaj z elastyczności ASP.NET Core, która ma być hostowana na różnych platformach i infrastrukturach serwerów. Na przykład możesz hostować Blazor aplikację przy użyciu usługi [Nginx](/aspnet/core/host-and-deploy/linux-nginx) lub [Apache](/aspnet/core/host-and-deploy/linux-apache) w systemie Linux. Więcej informacji o sposobach publikowania i wdrażania Blazor aplikacji znajduje się w dokumentacji Blazor [hostingu i wdrażania](/aspnet/core/host-and-deploy/blazor/) .

W następnej sekcji powiesz się, jak Blazor WebAssembly Blazor są konfigurowane projekty i aplikacje serwera.

>[!div class="step-by-step"]
>[Poprzedni](architecture-comparison.md) 
> [Dalej](project-structure.md)
