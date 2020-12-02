---
title: Wprowadzenie do usługi Blazor ASP.NET Web Forms Developers
description: Wprowadzenie do Blazor i pisanie aplikacji sieci Web w pełnym stosie przy użyciu platformy .NET
author: danroth27
ms.author: daroth
no-loc:
- Blazor
- WebAssembly
ms.date: 11/20/2020
ms.openlocfilehash: f1967dac0f46ba7cfefab62c5528dd1db8029514
ms.sourcegitcommit: 2f485e721f7f34b87856a51181b5b56624b31fd5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/02/2020
ms.locfileid: "96509718"
---
# <a name="an-introduction-to-no-locblazor-for-aspnet-web-forms-developers"></a>Wprowadzenie do usługi Blazor ASP.NET Web Forms Developers

ASP.NET Web Forms Framework to zszywanie programu .NET Web Development od momentu .NET Framework pierwszego wysłania w 2002. Z powrotem, gdy sieć Web była w znacznym stopniu nieprogramistyczna, ASP.NET Web Forms tworzy aplikacje sieci Web w prosty i wydajny sposób, wdrażając wiele wzorców, które były używane do tworzenia aplikacji klasycznych. W formularzach sieci Web ASP.NET strony sieci Web mogą szybko składać się z kontrolek interfejsu użytkownika wielokrotnego użytku. Interakcje użytkowników są obsługiwane naturalnie jako zdarzenia. Istnieje bogaty ekosystem formantów interfejsu użytkownika formularzy sieci Web udostępnianych przez firmę Microsoft i dostawców kontroli. Kontrolki ułatwiają podejmowanie połączeń ze źródłami danych i wyświetlanie bogatych wizualizacji danych. Dla wizualizacji, Projektant formularzy sieci Web udostępnia prosty interfejs przeciągania i upuszczania służący do zarządzania kontrolkami.

W ciągu lat firma Microsoft wprowadziła nowe platformy sieci Web opartych na ASP.NET w celu rozwiązania trendów związanych z programowaniem aplikacji sieci Web. Niektóre takie struktury sieci Web obejmują ASP.NET MVC, ASP.NET strony sieci Web i ostatnio ASP.NET Core. W przypadku każdej nowej struktury niektóre z nich przewidziały bezpośrednie odrzucanie formularzy sieci Web ASP.NET i criticized je jako przestarzałe, nieaktualne platformy sieci Web. Pomimo tych prognoz wiele deweloperów sieci Web platformy .NET kontynuuje wyszukiwanie ASP.NET Web Forms prostych, stabilnych i wydajnych metod wykonywania zadań.

W momencie pisania niemal połowa milionów deweloperów sieci Web używa ASP.NET formularzy sieci Web co miesiąc. Struktura formularzy sieci Web ASP.NET jest stabilna w przypadku, gdy dokumenty, przykłady, książki i wpisy w blogu z dekady temu pozostaną przydatne i istotne. W przypadku wielu deweloperów sieci Web platformy .NET "ASP.NET" jest nadal synonimem "ASP.NET Web Forms", tak jak podczas pierwszego opracowywania programu .NET. Argumenty dotyczące informatyków i wad formularzy sieci Web ASP.NET w porównaniu z innymi nowymi platformami sieci Web platformy .NET mogą próg. Formularze sieci Web ASP.NET są popularnym środowiskiem do tworzenia aplikacji sieci Web.

Nawet innowacje w programowaniu oprogramowania nie spowalniają pracy. Wszyscy deweloperzy oprogramowania muszą korzystać z nowych technologii i trendów. Rozważane są dwa trendy w szczególności:

1. Zmiana na typ Open Source i Międzyplatformowy
2. Zmiana logiki aplikacji na klienta

## <a name="an-open-source-and-cross-platform-net"></a>Platforma .NET Open Source i Międzyplatformowe

Po pierwszym wysłaniu formularzy sieci Web platformy .NET i ASP.NET, ekosystem platformy wyglądał znacznie inaczej niż dzisiaj. Rynki pulpitów i serwerów zostały zdominowane przez system Windows. Alternatywne platformy, takie jak macOS i Linux, były nadal zoptymalizowaniem do zdobycia trakcji. Formularze sieci Web ASP.NET są dostarczane z .NET Framework jako składnik tylko dla systemu Windows, co oznacza, że aplikacje ASP.NET Web Forms mogą działać tylko na maszynach z systemem Windows Server. Wiele nowoczesnych środowisk korzysta teraz z różnych rodzajów platform dla serwerów i maszyn programistycznych, takich jak obsługa wielu platform przez wiele użytkowników jest wymaganiem bezwzględnym.

Większość nowoczesnych platform sieci Web jest teraz również typu open source, który ma wiele korzyści. Użytkownicy nie beheld się do jednego właściciela projektu, aby naprawić błędy i dodać funkcje. Projekty open source zapewniają lepszą przejrzystość w zakresie postępu tworzenia i nadchodzących zmian. Projekty typu open source korzystają z wkładów z całej społeczności i wspierają ekosystem typu "open source". Pomimo ryzyka dotyczącego typu "open source", wielu odbiorców i współautorów znalazły odpowiednie środki zaradcze, które umożliwiają im korzystanie z zalet ekosystemu typu "open source" w bezpieczny i racjonalny sposób. Przykłady takich środków zaradczych dotyczą umów licencyjnych współautora, przyjaznych licencji, skanowania rodowodowego i obsługi.

Społeczność .NET wykorzystuje zarówno obsługę międzyplatformową, jak i open-source. .NET Core to wieloplatformowa implementacja programu .NET, która działa na mnóstwo platform, w tym Windows, macOS i różnych dystrybucji systemu Linux. Środowisko Xamarin zapewnia wersję platformy .NET typu open source. Mono działa w systemach Android, iOS i różnych innych, takich jak zegarki i inteligentne telewizory. Firma Microsoft wyłączyła [platformę .NET 5](https://devblogs.microsoft.com/dotnet/announcing-net-5-0/) uzgodnioną z platformą .NET Core i mono do "pojedynczego środowiska uruchomieniowego platformy .NET i platformy, które mogą być używane wszędzie i które mają ujednolicone zachowania środowiska uruchomieniowego i środowiska deweloperskie".

Czy program będzie ASP.NET korzystanie z formularzy sieci Web od przejścia do usługi Open Source i dla wielu platform? Odpowiedź, niestety, nie jest ani co najmniej w tym samym zakresie, jak reszta platformy. Zespół .NET [niedawno wyczyścił](https://devblogs.microsoft.com/dotnet/net-core-is-the-future-of-net/) , że ASP.NET formularzy sieci Web nie będzie można przenieść do platformy .NET Core lub .NET 5. Dlaczego?

Wystąpiły wysiłki w wczesnych dniach programu .NET Core do portów ASP.NET Web Forms. Liczba niepotrzebnych zmian, które są zbyt drastyczne, jest zbyt duża. Istnieje również możliwość odłożenia tego, że nawet w przypadku firmy Microsoft istnieje ograniczenie liczby platform sieci Web, które może obsługiwać jednocześnie. Prawdopodobnie ktoś w społeczności będzie miał przyczynę utworzenia otwartej i wieloplatformowej wersji formularzy sieci Web ASP.NET. [Kod źródłowy formularzy sieci Web ASP.NET](https://github.com/microsoft/referencesource) został udostępniony publicznie w formie referencyjnej. Jednak w takim przypadku wygląda na to, że formularze sieci Web ASP.NET będą pozostawać tylko w systemie Windows i bez modelu udziału Open Source. Jeśli obsługa wielu platform lub Open Source stanie się ważna dla Twoich scenariuszy, należy wyszukać coś nowego.

Czy oznacza to, że ASP.NET formularze sieci Web są *martwe* i nie powinny być już używane? Oczywiście nie! Tak długo, jak .NET Framework są dostarczane jako część systemu Windows, ASP.NET Web Forms będzie obsługiwaną strukturą. W przypadku wielu deweloperów korzystających z formularzy sieci Web nie jest to problem z obsługą międzyplatformowego i typu open-source. Jeśli nie masz wymaganego wsparcia dla wielu platform, typu open source lub innych nowych funkcji w programie .NET Core lub .NET 5, naklejanie do ASP.NET formularzy sieci Web w systemie Windows jest odpowiednie. ASP.NET Web Forms będzie w dalszym ciągu wydajnym sposobem pisania aplikacji internetowych przez wiele lat.

Jednak istnieje inny trend rozważania i jest to zmiana na klienta.

## <a name="client-side-web-development"></a>Programowanie aplikacji sieci Web po stronie klienta

Wszystkie. Platformy sieci Web oparte na protokole NET, w tym formularze sieci Web ASP.NET, mają w historyczny sposób wspólne: te, które są *renderowane na serwerze*. W przypadku aplikacji sieci Web renderowanych na serwerze przeglądarka wysyła żądanie do serwera, który wykonuje kod (kod platformy .NET w aplikacjach ASP.NET) w celu utworzenia odpowiedzi. Ta odpowiedź jest wysyłana z powrotem do przeglądarki w celu obsługi. W tym modelu przeglądarka jest używana jako aparat renderowania cienkiego. Na serwerze występuje poprawność tworzenia interfejsu użytkownika, uruchamiania logiki biznesowej i zarządzania stanem.

Jednak przeglądarki stają się uniwersalną platformą. Implementują one coraz większą liczbę otwartych standardów sieci Web, które zapewniają dostęp do możliwości komputera użytkownika. Dlaczego nie należy korzystać z mocy obliczeniowej, magazynu, pamięci i innych zasobów urządzenia klienckiego? Interakcje interfejsu użytkownika w szczególności mogą korzystać z bogatszego i bardziej interaktywnego działania, gdy jest obsługiwany co najmniej częściowo lub całkowicie po stronie klienta. Logika i dane, które powinny być obsługiwane na serwerze, nadal mogą być obsługiwane po stronie serwera. Można używać wywołań interfejsu API sieci Web lub nawet protokołów w czasie rzeczywistym, takich jak WebSockets. Te korzyści są dostępne dla deweloperów sieci Web bezpłatnie, jeśli chcą pisać kod JavaScript. Struktury interfejsu użytkownika po stronie klienta, takie jak kątowy, reagowanie i Vue, upraszczają Programowanie aplikacji sieci Web po stronie klienta i osiągnęły popularność. Deweloperzy ASP.NET Web Forms mogą również korzystać z klienta programu, a nawet korzystać z wbudowanych platform języka JavaScript, takich jak ASP.NET AJAX.

Mostkowanie obejmuje dwie różne platformy i ekosystemy (.NET i JavaScript). Wiedza jest wymagana w dwóch równoległych światach z różnymi językami, strukturami i narzędziami. Kod i logika nie mogą być łatwo udostępniane między klientem i serwerem, co skutkuje duplikowaniem i pracą inżynieryjną. Może być również trudne do utrzymania w ekosystemie JavaScript, który ma historię rozwoju na szybkości breakneck. Narzędzia platformy frontonu i preferencji narzędzi do kompilacji szybko zmieniają się. Branża zaobserwowano postęp od grunt do Gulp z pakietem WebPack i tak dalej. Te same Restless zmiany wystąpiły z platformami frontonu, takimi jak jQuery, odcinanie, kątowe, reagowanie i Vue. Jednak podano nieznaczny monopol przeglądarki JavaScript. Oznacza to, że do momentu, aż społeczność internetowa się nie *pomiraclea* .

## <a name="no-locwebassembly-fulfills-a-need"></a>WebAssembly spełnia potrzeby

W 2015, głównym dostawcom przeglądarki przyłączono siły w grupie społeczność W3C, aby utworzyć nowy otwarty standard sieci Web o nazwie WebAssembly . WebAssembly jest kodem bajtowym dla sieci Web. Jeśli możesz skompilować swój kod do WebAssembly programu, można go uruchomić w dowolnej przeglądarce na dowolnej platformie, w niemal większej szybkości. Początkowe wysiłki skupiające się na C/C++. Wynikiem jest znaczną prezentację uruchamiania natywnych aparatów graficznych 3W bezpośrednio w przeglądarce bez wtyczek. WebAssembly czy zostały ustandaryzowane i zaimplementowane przez wszystkie główne przeglądarki.

Działanie na uruchomionym platformie .NET WebAssembly zostało ogłoszone w późnej 2017 i wydane w 2020, w tym na pomoc techniczną z platformy .NET 5. Możliwość uruchamiania kodu platformy .NET bezpośrednio w przeglądarce umożliwia tworzenie aplikacji sieci Web na całym stosie przy użyciu platformy .NET.

## <a name="no-locblazor-full-stack-web-development-with-net"></a>Blazor: Programowanie aplikacji sieci Web w pełnym stosie przy użyciu platformy .NET

Ponadto możliwość uruchamiania kodu platformy .NET w przeglądarce nie zapewnia kompleksowego środowiska tworzenia aplikacji sieci Web po stronie klienta. Jest to miejsce, w którym się Blazor znajduje. Blazor to struktura interfejsu użytkownika sieci Web po stronie klienta oparta na języku C# zamiast języka JavaScript. Blazor można uruchamiać bezpośrednio w przeglądarce za pośrednictwem programu WebAssembly . Nie są wymagane żadne wtyczki przeglądarki. Alternatywnie Blazor aplikacje mogą uruchamiać serwer w programie .NET i obsługiwać wszystkie interakcje użytkowników w czasie rzeczywistym z przeglądarką.

Blazor ma wspaniałe narzędzia obsługiwane w programie Visual Studio i Visual Studio Code. Struktura zawiera również pełny model składników interfejsu użytkownika i oferuje wbudowane funkcje programu:

- Formularze i walidacja
- Wstrzykiwanie zależności
- Routing po stronie klienta
- Układy
- Debugowanie w przeglądarce
- Międzyoperacyjność w języku JavaScript

Blazor ma dużą wspólną postać ASP.NET Web Forms. Obie te platformy oferują modele programowania opartego na składnikach, sterowanych zdarzeniami. Główną różnicą architektury jest to, że ASP.NET Web Forms działa tylko na serwerze. Blazor można uruchomić na kliencie programu w przeglądarce. Ale jeśli korzystasz z tła ASP.NET formularzy sieci Web, istnieje wiele, Blazor co będzie znane. Blazor to rozwiązanie naturalne przeznaczone dla deweloperów ASP.NET Web Forms, który umożliwia korzystanie z funkcji tworzenia po stronie klienta i środowiska typu open-source w przyszłości dla platformy .NET.

Ta książka zawiera wprowadzenie do programu Blazor , który jest przeznaczony dla deweloperów ASP.NET Web Forms. Każde Blazor pojęcie koncepcji jest prezentowane w kontekście analogicznych funkcji i praktyk formularzy sieci Web ASP.NET. Na koniec tej książki znajdziesz następujące informacje:

- Jak tworzyć Blazor aplikacje.
- Jak Blazor działa.
- BlazorOdnosi się do programu .NET.
- Rozsądne strategie migracji istniejących aplikacji ASP.NET Web Forms do Blazor odpowiednich potrzeb.

## <a name="get-started-with-no-locblazor"></a>Wprowadzenie do Blazor

Wprowadzenie do programu Blazor jest proste. Przejdź do <https://blazor.net> i postępuj zgodnie z linkami, aby zainstalować odpowiedni zestaw .NET SDK i Blazor Szablony projektów. Znajdziesz również instrukcje dotyczące konfigurowania Blazor narzędzi w programie Visual Studio lub Visual Studio Code.

>[!div class="step-by-step"]
>[Poprzedni](index.md) 
> [Dalej](architecture-comparison.md)
