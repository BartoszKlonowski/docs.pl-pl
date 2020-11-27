---
title: Interakcja z zasadami pamięci podręcznej — maksymalny wiek i minimalna świeżość
ms.date: 03/30/2017
helpviewer_keywords:
- time-based cache policies
- Revalidate policy
- cache [.NET Framework], time-based policies
- freshness of cached resources
- maximum age policy
- minimum freshness policy
- age of cached resources
ms.assetid: 6567d451-ecec-496c-95a3-a415b99ba52a
ms.openlocfilehash: d4182268341f4a4334a627fc8c9e24fa235f003f
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96287556"
---
# <a name="cache-policy-interactionmaximum-age-and-minimum-freshness"></a>Interakcja z zasadami pamięci podręcznej — maksymalny wiek i minimalna świeżość

Aby zapewnić, że najnowsza zawartość jest zwracana do aplikacji klienckiej, interakcja z zasadami pamięci podręcznej klienta i wymagania dotyczące ponownego sprawdzania poprawności serwera zawsze będą mieć najważniejsze zasady pamięci podręcznej. We wszystkich przykładach w tym temacie przedstawiono zasady pamięci podręcznej dla zasobu, który jest buforowany 1 stycznia i wygasa 4 stycznia.  
  
 Poniższe przykłady ilustrują zasady pamięci podręcznej, które wynikają z interakcji maksymalnego wieku ( `maxAge` ) i minimalnej wartości Aktualności ( `minFresh` ).  
  
- Jeśli zestawy zasad pamięci podręcznej `maxAge` = 2 dni i `minFresh` nie są określone, zawartość zostanie ponownie sprawdzona w dniu 3 stycznia.  
  
- Jeśli zasady pamięci podręcznej są ustawione na `maxAge` 2 dni i `minFresh` = 1 dzień, zgodnie z `maxAge` , zawartość jest odświeżana do 3 stycznia. Zgodnie z `minFresh` , zawartość jest odświeżana do 3 stycznia. W związku z tym należy ponownie sprawdzić zawartość w dniu 3 stycznia.  
  
- Jeśli zasady pamięci podręcznej są ustawione na `maxAge` 2 dni i `minFresh` = 2 dni zgodnie z `maxAge` , zawartość jest odświeżana do 3 stycznia. Zgodnie z `minFresh` zawartością jest świeża do 2 stycznia. W związku z tym zawartość musi zostać ponownie sprawdzona w dniu 2 stycznia.  
  
## <a name="see-also"></a>Zobacz też

- [Zarządzanie pamięcią podręczną dla aplikacji sieciowych](cache-management-for-network-applications.md)
- [Zasady pamięci podręcznej](cache-policy.md)
- [Zasady pamięci podręcznej oparte na lokalizacji](location-based-cache-policies.md)
- [Zasady pamięci podręcznej oparte na czasie](time-based-cache-policies.md)
- [Konfigurowanie pamięci podręcznej w aplikacjach sieciowych](configuring-caching-in-network-applications.md)
- [Interakcja z zasadami pamięci podręcznej — maksymalny wiek i maksymalna nieaktualność](cache-policy-interaction-maximum-age-and-maximum-staleness.md)
