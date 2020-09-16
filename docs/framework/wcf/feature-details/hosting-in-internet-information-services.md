---
title: Hostowanie przez Internetowe usługi informacyjne
ms.date: 03/30/2017
helpviewer_keywords:
- hosting services [WCF], IIS
ms.assetid: ddae14e8-143c-442d-b660-2046809b2d43
ms.openlocfilehash: 7bfdf2b057c791da7e15619d69c0314557944093
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90555838"
---
# <a name="host-in-internet-information-services"></a>Host w Internet Information Services

Jedna z opcji hostingu usług Windows Communication Foundation (WCF) znajduje się w aplikacji Internet Information Services (IIS). Ten model hostingu jest podobny do modelu używanego przez usługi sieci Web usług ASP.NET i ASP.NET (ASMX).

## <a name="versions-of-iis"></a>Wersje usług IIS

Środowisko WCF może być hostowane w następujących wersjach usług IIS w następujących systemach operacyjnych:

- Usługi IIS 5,1 w systemie Windows XP z dodatkiem SP2. To środowisko jest przydatne do projektowania i opracowywania aplikacji hostowanych przez usługi IIS, które zostały później wdrożone w systemie operacyjnym serwera, takim jak Windows Server 2003.

- Usługi IIS 6,0 w systemie Windows Server 2003. Usługi IIS 6,0 oferują zaawansowany model procesów, który oferuje ulepszoną skalowalność, niezawodność i izolację aplikacji. To środowisko jest odpowiednie do wdrożenia produkcyjnego usług WCF, które używają wyłącznie komunikacji protokołu HTTP.

- Usługi IIS 7,0 w systemach Windows Vista i Windows Server 2008. Usługi IIS 7,0 oferują ten sam zaawansowany model procesów co IIS 6,0, ale używa usługi aktywacji procesów systemu Windows (WAS) do zezwalania na aktywację i komunikację sieciową za pośrednictwem protokołów innych niż HTTP. To środowisko jest odpowiednie do tworzenia usług WCF, które komunikują się za pośrednictwem dowolnego protokołu sieciowego obsługiwanego przez WCF (w tym HTTP, net. TCP, net. pipe i net. MSMQ). Aby uzyskać więcej informacji na temat programu, zobacz [hosting w usłudze aktywacji procesów systemu Windows](hosting-in-windows-process-activation-service.md).

- [System Windows Server AppFabric](/previous-versions/appfabric/ff384253(v=azure.10)) współpracuje z usługami IIS 7,0 i usługą aktywacji procesów systemu Windows (was), aby zapewnić rozbudowane środowisko hostingu aplikacji dla usług NET4 WCF i WF. Te korzyści obejmują proces zarządzania cyklem życia procesów, odtwarzania procesów, hostingu udostępnionego, szybkiej ochrony przed awariami, oddzielania procesów, aktywacji na żądanie i monitorowania kondycji. Aby uzyskać szczegółowe informacje, zobacz temat [funkcje hostingu platformy AppFabric](/previous-versions/appfabric/ee677189(v=azure.10)) i [pojęcia hostingu platformy AppFabric](/previous-versions/appfabric/ee677371(v=azure.10)).

## <a name="benefits-of-iis-hosting"></a>Zalety hostingu usług IIS

Hosting usług WCF w usługach IIS ma kilka zalet:

- Usługi WCF hostowane w usługach IIS są wdrażane i zarządzane w taki sam sposób jak każdy inny typ aplikacji usług IIS, w tym aplikacje ASP.NET i ASMX.

- Usługi IIS zapewniają aktywację procesów, zarządzanie kondycją i możliwości odtwarzania w celu zwiększenia niezawodności aplikacji hostowanych.

- Podobnie jak w przypadku ASP.NET, usługi WCF hostowane w usłudze ASP.NET mogą korzystać z modelu hostingu ASP.NET, gdzie wiele aplikacji znajduje się w typowym procesie roboczym, aby zwiększyć gęstość i skalowalność serwera.

- Usługi WCF hostowane w usługach IIS używają tego samego dynamicznego modelu kompilacji co ASP.NET 2,0, co upraszcza opracowywanie i wdrażanie usług hostowanych.

Podczas decydowania o hostowanie usług WCF w usługach IIS należy pamiętać, że usługi IIS 5,1 i IIS 6,0 są ograniczone tylko do komunikacji HTTP. Aby uzyskać więcej informacji na temat wybierania środowiska hostingu, zobacz [usługi hostingu](../hosting-services.md).

## <a name="deploy-an-iis-hosted-wcf-service"></a>Wdrażanie usługi WCF hostowanej przez usługi IIS

Tworzenie i wdrażanie usługi WCF hostowanej przez usługi IIS obejmuje następujące zadania:

- Upewnij się, że składnik usług IIS, ASP.NET, WCF i HTTP WCF są poprawnie zainstalowane i zarejestrowane.

- Utwórz nową aplikację usług IIS lub ponownie Użyj istniejącej aplikacji ASP.NET.

- Utwórz plik SVC dla usługi WCF.

- Wdróż implementację usługi w aplikacji usług IIS.

- Skonfiguruj usługę WCF.

Aby zapoznać się z omówieniem każdego z tych zadań, zobacz [wdrażanie usługi WCF hostowanej w Internet Information Services](deploying-an-internet-information-services-hosted-wcf-service.md).

## <a name="wcf-services-and-aspnet"></a>Usługi WCF i ASP.NET

Usługi WCF mogą być hostowane równolegle z usługą ASP.NET lub ASP.NET w trybie zgodności, w którym usługi mogą w pełni korzystać z funkcji udostępnianych przez platformę aplikacji sieci Web ASP.NET. Dyskusje na temat tych funkcji znajdują się w temacie [usługi WCF i ASP.NET](wcf-services-and-aspnet.md).

## <a name="see-also"></a>Zobacz także

- [Rozszerzanie hostingu za pomocą elementu ServiceHostFactory](../extending/extending-hosting-using-servicehostfactory.md)
- [Wdrażanie usługi WCF hostowanej przez Internetowe usługi informacyjne](deploying-an-internet-information-services-hosted-wcf-service.md)
- [Usługi WCF i platforma ASP.NET](wcf-services-and-aspnet.md)
- [Najlepsze rozwiązania dotyczące hostowania Internetowych usług informacyjnych](internet-information-services-hosting-best-practices.md)
- [Konfigurowanie Internetowych usług informacyjnych 7.0 na potrzeby programu Windows Communication Foundation](configuring-iis-for-wcf.md)
- [Funkcje hostingu sieci szkieletowej aplikacji systemu Windows Server](/previous-versions/appfabric/ee677189(v=azure.10))
