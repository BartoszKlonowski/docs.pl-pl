---
title: Bezpieczne sesje
ms.date: 03/30/2017
ms.assetid: 7b50602f-d7b5-42e9-8e92-1f0413df0d8b
ms.openlocfilehash: fd8406af0c37981b2ddc7ab8ddb0c82c63cbc0b1
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96288556"
---
# <a name="secure-sessions"></a>Bezpieczne sesje

Funkcja programu Windows Communication Foundation (WCF) to niezawodne sesje, które gwarantują otrzymywanie komunikatów w kolejności, w jakiej zostały wysłane. W tematach w tej sekcji omówiono implikacje związane z zabezpieczeniami, które należy wziąć pod uwagę podczas tworzenia niezawodnej sesji. Aby uzyskać więcej informacji na temat sesji niezawodnych, zobacz [using Sessions](../using-sessions.md).  
  
> [!NOTE]
> Jeśli w systemie Windows XP jest wymagana personifikacja, należy użyć bezpiecznej sesji bez tokenu stanu zabezpieczenia stanowe (SCT). Gdy stanowe SCTs są używane z personifikacją, <xref:System.InvalidOperationException> jest generowany. Aby uzyskać więcej informacji, zobacz [scenariusze nieobsługiwane](unsupported-scenarios.md).  
  
## <a name="in-this-section"></a>W tej sekcji  
  
|||  
|-|-|  
|[Bezpieczne konwersacje i bezpieczne sesje](secure-conversations-and-secure-sessions.md)|Bezpieczne konwersacje i bezpieczne sesje są synonimami. W tym temacie wyjaśniono, jak działa bezpieczna konwersacja oraz kiedy i dlaczego należy używać wzorca.|  
|[Instrukcje: tworzenie bezpiecznej sesji](how-to-create-a-secure-session.md)|Instruktaż przedstawia podstawy tworzenia bezpiecznej sesji.|  
|[Instrukcje: tworzenie tokenu kontekstu zabezpieczeń dla bezpiecznej sesji](how-to-create-a-security-context-token-for-a-secure-session.md)|W tym kroku opisano kroki tworzenia kolektywu serwerów sieci Web, które będą obsługiwać stan i sesje z klientami.|  
|[Zagadnienia dotyczące zabezpieczeń bezpiecznych sesji](security-considerations-for-secure-sessions.md)|Opisuje specjalne zagadnienia dotyczące bezpiecznych sesji.|  
  
## <a name="reference"></a>Dokumentacja  

 <xref:System.ServiceModel>  
  
 <xref:System.ServiceModel.Channels>  
  
## <a name="related-sections"></a>Sekcje pokrewne  

 [Sesje, tworzenie wystąpień i współbieżność](sessions-instancing-and-concurrency.md)  
  
 [Projektowanie i implementowanie usług](../designing-and-implementing-services.md)  
  
## <a name="see-also"></a>Zobacz też

- [Instrukcje: włączanie wykrywania powtarzania komunikatu](how-to-enable-message-replay-detection.md)
- [Ataki oparte na metodzie powtórzeń](replay-attacks.md)
- [Instrukcje: tworzenie usługi, która wymaga użycia sesji](how-to-create-a-service-that-requires-sessions.md)
