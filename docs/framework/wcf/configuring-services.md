---
title: Konfigurowanie usług WCF
ms.date: 03/30/2017
helpviewer_keywords:
- configuration [WCF]
ms.assetid: beac771e-f28e-4f84-9ff1-ad9251c726d3
ms.openlocfilehash: a5fe0cabb1a6be7f93bf5f4d753e9bb08a39cea3
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96253339"
---
# <a name="configuring-wcf-services"></a>Konfigurowanie usług WCF

Po zaprojektowaniu i wdrożeniu kontraktu usługi możesz przystąpić do konfigurowania usługi. Jest to miejsce, w którym można definiować i dostosowywać sposób, w jaki usługa jest narażona na komputery klienckie, w tym określenie adresu, pod którym można je znaleźć, używanego do wysyłania i odbierania komunikatów oraz typu bezpieczeństwa, którego wymaga.  
  
 Konfiguracja użyta w tym miejscu obejmuje wszystkie metody, w sposób niezależny w kodzie lub przy użyciu pliku konfiguracji, w którym można definiować i dostosowywać różne aspekty usługi, takie jak określanie adresów punktów końcowych, używanych transportów i ich schematów zabezpieczeń. W tym przypadku Zapisywanie konfiguracji jest główną częścią programowania aplikacji WCF.  
  
## <a name="in-this-section"></a>W tej sekcji  

 [Uproszczona konfiguracja](simplified-configuration.md)  
 Począwszy od .NET Framework 4, platforma WCF udostępnia nowy domyślny model konfiguracji, który upraszcza wymagania dotyczące konfiguracji programu WCF. Jeśli nie podasz żadnej konfiguracji WCF dla określonej usługi, środowisko uruchomieniowe automatycznie skonfiguruje usługę przy użyciu domyślnych punktów końcowych, powiązań i zachowań.  
  
 [Konfigurowanie usług za pomocą plików konfiguracji](configuring-services-using-configuration-files.md)  
 Usługa Windows Communication Foundation (WCF) można skonfigurować przy użyciu technologii konfiguracji .NET Framework. Najczęściej elementy XML są dodawane do pliku Web.config dla witryny Internet Information Services (IIS), która hostuje usługę WCF. Elementy umożliwiają zmianę szczegółów, takich jak adresy punktów końcowych (rzeczywiste adresy używane do komunikowania się z usługą) na poszczególnych komputerach.  
  
 [Powiązania](bindings.md)  
 Ponadto program WCF zawiera kilka typowych konfiguracji dostarczonych przez system w formie powiązań, które umożliwiają szybkie wybieranie najbardziej podstawowych funkcji komunikacji klienta i usługi, takich jak transporty, zabezpieczenia i używane kodowanie komunikatów.  
  
 [Punkty końcowe](endpoints.md)  
 Cała komunikacja z usługą WCF odbywa się za pomocą *punktów końcowych* usługi. Punkty końcowe zawierają kontrakt, informacje o konfiguracji określone w powiązaniach oraz adresy wskazujące, gdzie znaleźć usługę lub gdzie mają zostać uzyskane informacje o usłudze.  
  
 [Zabezpieczanie usług](securing-services.md)  
 Korzystając z programu WCF i istniejących mechanizmów zabezpieczeń, można zaimplementować poufność, integralność, uwierzytelnianie i autoryzację w dowolnej usłudze. Możesz także przeprowadzić inspekcję pod kątem sukcesów i niepowodzeń zabezpieczeń.  
  
 [Tworzenie usług międzyoperacyjnych 1.1 profilu podstawowego WS-I](./creating-ws-i-basic-profile-1-1-interoperable-services.md)  
 Wymagania dotyczące wdrażania usługi, która jest współdziałania z usługami i klientami na dowolnej innej platformie lub systemie operacyjnym, opisano w specyfikacji WS-I Basic Profile 1,1.  
  
## <a name="reference"></a>Dokumentacja  

 <xref:System.ServiceModel>  
  
 <xref:System.ServiceModel.Channels>  
  
 <xref:System.ServiceModel.Description>  
  
## <a name="related-sections"></a>Sekcje pokrewne  

 [Podstawowy cykl życia programowania](basic-programming-lifecycle.md)  
  
 [Projektowanie i implementowanie usług](designing-and-implementing-services.md)  
  
 [Usługi hostingowe](hosting-services.md)  
  
 [Kompilowanie klientów](building-clients.md)  
  
 [Wprowadzenie do rozszerzalności](introduction-to-extensibility.md)  
  
 [Administracja i Diagnostyka](./diagnostics/index.md)  
  
## <a name="see-also"></a>Zobacz też

- [Podstawy programowania przy użyciu programu WCF](basic-wcf-programming.md)
- [Omówienie pojęć](conceptual-overview.md)
- [Szczegóły funkcji WCF](./feature-details/index.md)
