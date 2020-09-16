---
title: Zabezpieczanie usług i klientów
ms.date: 03/30/2017
helpviewer_keywords:
- message security [WCF]
ms.assetid: e681f3bd-0c09-4a58-b0e4-0ecbdf1aa6c7
ms.openlocfilehash: 713737b129771967958fddf44e9ef28583d49422
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90554081"
---
# <a name="securing-services-and-clients"></a>Zabezpieczanie usług i klientów
Informacje przedstawione w tej sekcji koncentrują się na zabezpieczeniach programistycznych w programie Windows Communication Foundation (WCF). Ogólnie rzecz biorąc, obejmuje to wybranie odpowiedniego powiązania dostarczonego przez system, ustawienie właściwości elementu zabezpieczeń, a następnie ustawienie właściwości zachowań usługi, które określają sposób pobierania poświadczeń do użycia przez usługę lub klienta. Te techniki obejmują wymagania dotyczące zabezpieczeń większości użytkowników w większości scenariuszy, jak pokazano w [typowych scenariuszach zabezpieczeń](common-security-scenarios.md). Jeśli scenariusz wymaga większej liczby możliwości, należy najpierw zapoznać [się z funkcjami zabezpieczeń i powiązaniami niestandardowymi](security-capabilities-with-custom-bindings.md); Jeśli rozwiązanie nie jest widoczne, zobacz [rozszerzanie zabezpieczeń](../extending/extending-security.md). W przypadku tworzenia (lub współpracy z programem) systemu, który używa rozbudowanych oświadczeń, zapoznaj się z tematami w temacie [autoryzacja](authorization-in-wcf.md).  
  
## <a name="in-this-section"></a>W tej sekcji  
 [Programowanie zabezpieczeń WCF](programming-wcf-security.md)  
 Omówienie modelu programowania używanego do zabezpieczania wiadomości.  
  
 [Przegląd zabezpieczeń transportu](transport-security-overview.md)  
 Omówienie sposobów zabezpieczania komunikatów za pomocą warstwy transportowej.  
  
 [Zabezpieczenia komunikatów](message-security-in-wcf.md)  
 Podsumowuje przyczyny używania zabezpieczeń na poziomie komunikatów w Windows Communication Foundation (WCF).  
  
 [Bezpieczne sesje](secure-sessions.md)  
 Omówienie zagadnień wymaganych podczas zabezpieczania sesji programu WCF.  
  
 [Praca z certyfikatami](working-with-certificates.md)  
 Wyjaśnienie niektórych typowych zadań wymaganych w przypadku używania certyfikatów X. 509.  
  
## <a name="reference"></a>Tematy pomocy  
 <xref:System.ServiceModel>  
  
 <xref:System.ServiceModel.Channels>  
  
 <xref:System.ServiceModel.Security>  
  
## <a name="related-sections"></a>Sekcje pokrewne  
 [Pojęcia dotyczące zabezpieczeń](security-concepts.md)  
  
 [Rozszerzanie zabezpieczeń](../extending/extending-security.md)  
  
 [Typowe scenariusze zabezpieczeń](common-security-scenarios.md)  
  
 [Wiązania i zabezpieczenia](bindings-and-security.md)  
  
 [Możliwości zabezpieczeń wiązań niestandardowych](security-capabilities-with-custom-bindings.md)  
  
 [Rozszerzanie zabezpieczeń](../extending/extending-security.md)  
  
 [Autoryzacja](authorization-in-wcf.md)  
  
## <a name="see-also"></a>Zobacz także

- [Podstawy programowania przy użyciu programu WCF](../basic-wcf-programming.md)
- [Model zabezpieczeń dla sieci szkieletowej aplikacji systemu Windows Server](/previous-versions/appfabric/ee677202(v=azure.10))
