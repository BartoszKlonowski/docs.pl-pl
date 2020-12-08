---
title: Proces programistyczny dla platformy Azure
description: Tworzenie architektury nowoczesnych aplikacji sieci Web przy użyciu ASP.NET Core i platformy Azure | Proces tworzenia aplikacji na platformie Azure
author: ardalis
ms.author: wiwagn
ms.date: 12/01/2020
ms.openlocfilehash: 2706a4091565e6f3cb795acf031a238ae55a1068
ms.sourcegitcommit: 45c7148f2483db2501c1aa696ab6ed2ed8cb71b2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/08/2020
ms.locfileid: "96851630"
---
# <a name="development-process-for-azure"></a>Proces programistyczny dla platformy Azure

> _"Dzięki chmurze użytkownicy indywidualni i małe firmy mogą przyciągnąć swoje palce i natychmiast skonfigurować usługi klasy korporacyjnej"._  
> _-Roy posta Stephan_

## <a name="vision"></a>Obraz

> *Opracowuj dobrze zaprojektowane aplikacje ASP .NET Core w odpowiedni sposób, korzystając z programu Visual Studio lub interfejsu wiersza polecenia dotnet i Visual Studio Code lub dowolnego edytora.*

## <a name="development-environment-for-aspnet-core-apps"></a>Środowisko programistyczne dla aplikacji ASP.NET Core

### <a name="development-tools-choices-ide-or-editor"></a>Opcje narzędzi programistycznych: IDE lub Edytor

Bez względu na to, czy wolisz pełną i wydajną platformę IDE, czy też Edytor uproszczony i Agile, firma Microsoft połączyła się z tworzeniem aplikacji ASP.NET Core

**Program Visual Studio 2019.** Program Visual Studio 2019 to najlepsze w swojej klasie środowisko IDE do tworzenia aplikacji do ASP.NET Core. Oferuje ona hosta funkcji, które zwiększają produktywność deweloperów. Można go używać do tworzenia aplikacji, a następnie analizowania jej wydajności i innych właściwości. Zintegrowany debuger umożliwia wstrzymywanie wykonywania kodu i wykonywanie kroków z powrotem i w górę za pomocą kodu na bieżąco, gdy jest uruchomiony. Wbudowany moduł uruchamiający testy pozwala organizować testy i ich wyniki, a także wykonywać testy jednostkowe na żywo podczas kodowania. Korzystając z Live Share, możesz współpracować w czasie rzeczywistym z innymi programistami i bezproblemowo udostępniać swoją sesję kodu za pośrednictwem sieci. Gdy wszystko będzie gotowe, program Visual Studio zawiera wszystko, co jest potrzebne do opublikowania aplikacji na platformie Azure lub wszędzie tam, gdzie można je hostować.

[Pobierz program Visual Studio 2019](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs)

**Interfejs wiersza polecenia Visual Studio Code i dotnet** (międzyplatformowe narzędzia dla systemów Mac, Linux i Windows). Jeśli wolisz uproszczony i Międzyplatformowy Edytor obsługujący dowolny język programowania, możesz użyć kodu Microsoft Visual Studio i interfejsu wiersza polecenia dotnet. Te produkty zapewniają proste, a jeszcze niezawodne środowisko, które usprawnia przepływ pracy dewelopera. Ponadto Visual Studio Code obsługuje rozszerzenia dla programowania C \# i sieci Web, które udostępnia funkcje IntelliSense i skróty w edytorze.

[Pobierz zestaw .NET SDK](https://dotnet.microsoft.com/download)

[Pobierz program Visual Studio Code](https://code.visualstudio.com/download)

## <a name="development-workflow-for-azure-hosted-aspnet-core-apps"></a>Przepływ pracy deweloperskiej dla aplikacji ASP.NET Core hostowanych przez platformę Azure

Cykl programowania aplikacji zaczyna się od maszyny każdego dewelopera, co oznacza, że aplikacja zostanie zaprojektowana przy użyciu preferowanego języka i przetestowana lokalnie. Deweloperzy mogą wybrać swój preferowany system kontroli źródła i skonfigurować ciągłą integrację (CI) i/lub ciągłe dostarczanie/wdrażanie (CD) przy użyciu serwera kompilacji lub na podstawie wbudowanych funkcji platformy Azure.

Aby rozpocząć tworzenie aplikacji ASP.NET Core przy użyciu ciągłej integracji/ciągłego wdrażania, możesz użyć Azure DevOps Services lub własnych Team Foundation Server organizacji (TFS).

### <a name="initial-setup"></a>Początkowa konfiguracja

Aby utworzyć potok wydania dla aplikacji, musisz mieć kod aplikacji w kontroli źródła. Skonfiguruj lokalne repozytorium i podłącz je do zdalnego repozytorium w projekcie zespołowym. Wykonaj następujące instrukcje:

- [Udostępnianie kodu za pomocą narzędzia Git i programu Visual Studio](/azure/devops/git/share-your-code-in-git-vs) lub

- [Udostępnianie kodu za pomocą TFVC i programu Visual Studio](/azure/devops/tfvc/share-your-code-in-tfvc-vs)

Utwórz Azure App Service, w którym zostanie wdrożona aplikacja. Utwórz aplikację internetową, przechodząc do bloku App Services w Azure Portal. Kliknij pozycję + Dodaj, wybierz szablon aplikacja sieci Web, kliknij przycisk Utwórz i podaj nazwę oraz inne szczegóły. Aplikacja sieci Web będzie dostępna z poziomu aplikacji {Name}. azurewebsites. NET.

![AzureWebApp](./media/image10-2.png)

**Rysunek 10-1.** Tworzenie nowej aplikacji sieci Web Azure App Service w witrynie Azure Portal.

Proces kompilacji CI wykonuje zautomatyzowaną kompilację za każdym razem, gdy nowy kod zostanie przekazany do repozytorium kontroli źródła projektu. Ten proces daje natychmiastowe informacje o tym, że kod kompiluje (i najlepiej przekazuje testy automatyczne) i może zostać wdrożony. Ta kompilacja elementu konfiguracji spowoduje utworzenie artefaktu pakietu Narzędzia Web Deploy i opublikowanie go do użycia przez proces tworzenia dysku CD.

[Zdefiniuj proces kompilacji elementu konfiguracji](/azure/devops/pipelines/ecosystems/dotnet-core)

Pamiętaj, aby włączyć integrację ciągłą, aby system ustawił w kolejce kompilację, gdy ktoś w zespole zatwierdzi nowy kod. Przetestuj kompilację i sprawdź, czy produkuje pakiet Web Deploy jako jeden z jego artefaktów.

Gdy kompilacja zakończy się pomyślnie, proces dysku CD wdróże wyniki kompilacji CI w aplikacji sieci Web platformy Azure. Aby skonfigurować ten krok, należy utworzyć i skonfigurować *wydanie*, które zostanie wdrożone w Azure App Service.

[Wdrażanie aplikacji internetowej platformy Azure](/azure/devops/pipelines/targets/webapp)

Po skonfigurowaniu potoku ciągłej integracji/ciągłego wdrażania możesz łatwo wprowadzać aktualizacje aplikacji sieci Web i zatwierdzić je do kontroli źródła, aby zostały wdrożone.

### <a name="workflow-for-developing-azure-hosted-aspnet-core-applications"></a>Przepływ pracy służący do tworzenia aplikacji ASP.NET Core hostowanych na platformie Azure

Po skonfigurowaniu konta platformy Azure i procesu ciągłej integracji/ciągłego opracowywania aplikacji ASP.NET Core hostowanych na platformie Azure jest prosta. Poniżej przedstawiono podstawowe kroki, które zwykle są wykonywane podczas kompilowania aplikacji ASP.NET Core hostowanej w Azure App Service jako aplikacja internetowa, jak pokazano na rysunku 10-2.

![EndToEndDevDeployWorkflow](./media/image10-3.png)

**Rysunek 10-2.** Przepływ pracy krok po kroku służący do kompilowania aplikacji ASP.NET Core i hostowania ich na platformie Azure

#### <a name="step-1-local-dev-environment-inner-loop"></a>Krok 1. Pętla wewnętrzna lokalnego środowiska deweloperskiego

Opracowywanie aplikacji ASP.NET Core na potrzeby wdrażania na platformie Azure nie różni się od tworzenia aplikacji w inny sposób. Korzystaj z lokalnego środowiska programistycznego, z którym masz doświadczenie, niezależnie od tego, czy jest to program Visual Studio 2019, czy interfejs wiersza polecenia dotnet i Visual Studio Code lub preferowany Edytor. Można napisać kod, uruchamiać i debugować zmiany, uruchamiać testy automatyczne i przekazywać lokalne zatwierdzenia do kontroli źródła do momentu, gdy wszystko będzie gotowe do wypchnięcia zmian do udostępnionego repozytorium kontroli źródła.

#### <a name="step-2-application-code-repository"></a>Krok 2. Repozytorium kodu aplikacji

Gdy wszystko jest gotowe do udostępnienia kodu zespołowi, należy wypchnąć zmiany z repozytorium lokalnego źródła do udostępnionego repozytorium źródłowego zespołu. Jeśli pracujesz w rozgałęzieniu niestandardowym, ten krok zazwyczaj polega na scaleniu kodu w rozgałęzieniu udostępnionym (na przykład za pomocą [żądania ściągnięcia](/azure/devops/git/pull-requests)).

#### <a name="step-3-build-server-continuous-integration-build-test-package"></a>Krok 3. Serwer kompilacji: Ciągła integracja. Kompilacja, test, pakiet

Nowa kompilacja jest wyzwalana na serwerze kompilacji za każdym razem, gdy w repozytorium kodu aplikacji udostępnionej zostanie wykonane nowe zatwierdzenie. W ramach procesu CI kompilacja powinna w pełni kompilować aplikację i uruchamiać testy automatyczne, aby upewnić się, że wszystko działa zgodnie z oczekiwaniami. Wynik końcowy procesu CI powinien być spakowaną wersją aplikacji sieci Web, gotowa do wdrożenia.

#### <a name="step-4-build-server-continuous-delivery"></a>Krok 4. Serwer kompilacji: ciągłe dostarczanie

Gdy kompilacja zakończyła się powodzeniem, proces tworzenia dysków CD zostanie pobrany z utworzonych artefaktów kompilacji. Ten proces obejmie pakiet narzędzia Web Deploy. Serwer kompilacji wdroży ten pakiet w Azure App Service, zastępując istniejącą usługę nowo utworzoną. Zazwyczaj ten krok jest przeznaczony dla środowiska przejściowego, ale niektóre aplikacje wdrażają bezpośrednio w środowisku produkcyjnym przez proces CD.

#### <a name="step-5-azure-app-service-web-app"></a>Krok 5. Aplikacja internetowa usługi Azure App Service

Po wdrożeniu aplikacja ASP.NET Core działa w kontekście aplikacji internetowej Azure App Service. Tę aplikację sieci Web można monitorować i konfigurować przy użyciu witryny Azure Portal.

#### <a name="step-6-production-monitoring-and-diagnostics"></a>Krok 6. Monitorowanie i Diagnostyka produkcji

Gdy aplikacja sieci Web jest uruchomiona, można monitorować kondycję aplikacji i zbierać dane dotyczące diagnostyki i zachowania użytkowników. Application Insights jest dołączona do programu Visual Studio i oferuje automatyczną instrumentację dla aplikacji ASP.NET. Może on dostarczyć informacji na temat użycia, wyjątków, żądań, wydajności i dzienników.

## <a name="references"></a>Odwołania

**Kompilowanie i wdrażanie aplikacji ASP.NET Core na platformie Azure**  
<https://docs.microsoft.com/azure/devops/build-release/apps/aspnet/build-aspnet-core>

>[!div class="step-by-step"]
>[Poprzedni](test-asp-net-core-mvc-apps.md) 
> [Dalej](azure-hosting-recommendations-for-asp-net-web-apps.md)
