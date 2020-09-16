---
title: Obsługiwane scenariusze wdrażania
ms.date: 03/30/2017
ms.assetid: 3399f208-3504-4c70-a22e-a7c02a8b94a6
ms.openlocfilehash: 299c8f2e29806a123e0a8b6e1e70d8cc13daa7bf
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90546253"
---
# <a name="supported-deployment-scenarios"></a>Obsługiwane scenariusze wdrażania

Podzbiór funkcji Windows Communication Foundation (WCF) obsługiwanych w przypadku częściowo zaufanych aplikacji został zaprojektowany w celu spełnienia wymagań niektórych, ale nie wszystkich, scenariuszy korzystania z programu WCF. Na serwerze platforma WCF spełnia wymagania dotyczące współużytkowanych dostawców usług hostingowych w skali Internetu, którzy uruchamiają aplikacje innych firm w zestawie uprawnień do średniego zaufania ASP.NET 2,0 ze względów bezpieczeństwa. Na kliencie obsługa częściowego zaufania WCF została zaprojektowana tak, aby spełniała wymagania technologii wdrażania, takich jak [wdrażanie ClickOnce](/visualstudio/deployment/clickonce-security-and-deployment) lub technologia aplikacji przeglądarki XAML WPF, które umożliwiają bezproblemowe i bezpieczne wdrażanie aplikacji klasycznych z niezaufanych witryn.

## <a name="minimum-permission-requirements"></a>Minimalne wymagania dotyczące uprawnień

Usługa WCF obsługuje podzestaw funkcji w aplikacjach uruchamianych w ramach jednego z następujących standardowych zestawów uprawnień:

- Uprawnienia średniego zaufania

- Uprawnienia strefy internetowej

Próba użycia programu WCF w częściowo zaufanych aplikacjach z bardziej restrykcyjnymi uprawnieniami może skutkować wyjątkami zabezpieczeń w czasie wykonywania.

Aby uzyskać więcej informacji o funkcjach obsługiwanych w tych zestawach uprawnień, zobacz [Częściowa zgodność funkcji zaufania](partial-trust-feature-compatibility.md).

## <a name="partial-trust-on-the-server"></a>Częściowe zaufanie na serwerze

Wielu komercyjnych dostawców usług hostingu aplikacji sieci Web ASP.NET, że aplikacje działające na serwerach działają w zestawie uprawnień do średniego zaufania ASP.NET 2,0. Usługi WCF mogą działać w tych środowiskach, pod warunkiem, że korzystają z <xref:System.ServiceModel.BasicHttpBinding> <xref:System.ServiceModel.WebHttpBinding> zabezpieczeń, lub <xref:System.ServiceModel.WSHttpBinding> z zabezpieczeniami na poziomie transportu.

Usługi WCF działające w środowiskach hostingu średniego zaufania mogą również pełnić rolę usług warstwy środkowej przez wysyłanie komunikatów do innych serwerów w odpowiedzi na żądania klientów. Scenariusze warstwy środkowej na serwerze są obsługiwane, jeśli środowisko hostingu udzieliło aplikacji odpowiedniej <xref:System.Net.WebPermission> do wykonania żądań wychodzących do żądanego serwera.

Oprócz obsługi komunikatów SOAP przy użyciu jednego z obsługiwanych powiązań protokołu SOAP, WCF obsługuje <xref:System.ServiceModel.WebHttpBinding> Tworzenie usług w stylu sieci Web w częściowo zaufanych aplikacjach. [Model programowania HTTP sieci Web WCF](wcf-web-http-programming-model.md), [zespalanie programu WCF](wcf-syndication.md)i [integracja AJAX oraz funkcje obsługi JSON](ajax-integration-and-json-support.md) w usłudze WCF są obsługiwane w częściowej relacji zaufania.

Usługi przepływu pracy wymagają uprawnień pełnego zaufania i nie mogą być używane w częściowo zaufanych aplikacjach.

Aby uzyskać więcej informacji, zobacz [How to: use medium Trust in ASP.NET 2,0](/previous-versions/msp-n-p/ff648344(v=pandp.10)).

## <a name="partial-trust-on-the-client"></a>Częściowe zaufanie na kliencie

Podczas pobierania i uruchamiania kodu z niezaufanych witryn internetowych należy podjąć pewne środki ostrożności dotyczące zabezpieczeń. Zarówno [wdrożenie ClickOnce](/visualstudio/deployment/clickonce-security-and-deployment) , jak i technologia aplikacji przeglądarki XAML (XBAP) WPF używają częściowej relacji zaufania do przyznawania ograniczonych uprawnień (strefa internetowa) do niezaufanego kodu.

Programu WCF można używać do komunikowania się z serwerami zdalnymi z poziomu częściowo zaufanych aplikacji wdrożonych w ramach [wdrażania ClickOnce](/visualstudio/deployment/clickonce-security-and-deployment) lub XBAP. Zestaw uprawnień strefy internetowej obejmuje <xref:System.Net.WebPermission> dla hosta źródłowego, który umożliwia aplikacjom komunikowanie się z serwerem pochodzenia przy użyciu dowolnego z obsługiwanych powiązań WCF opisanych w [częściowej zgodności funkcji zaufania](partial-trust-feature-compatibility.md).

## <a name="see-also"></a>Zobacz także

- [Zabezpieczenia dostępu kodu](../../misc/code-access-security.md)
- [Omówienie Windows Presentation Foundation aplikacji hostowanych w przeglądarce](/dotnet/desktop/wpf/app-development/wpf-xaml-browser-applications-overview)
- [Zaufanie częściowe](partial-trust.md)
- [ASP.NET poziomów zaufania i plików zasad](/previous-versions/wyts434y(v=vs.140))
