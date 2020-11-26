---
title: Ataki oparte na metodzie powtórzeń
ms.date: 03/30/2017
ms.assetid: 7a17e040-93cd-4432-81b9-9f62fec78c8f
ms.openlocfilehash: 4325b3747074f13cf02752f99b25fa02e4117b4c
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96239084"
---
# <a name="replay-attacks"></a>Ataki oparte na metodzie powtórzeń

*Ataku powtarzania* występuje, gdy osoba atakująca kopiuje strumień komunikatów między dwiema stronami i odtwarza strumień do co najmniej jednej ze stron. O ile nie zostanie to skorygowane, komputery, które podlegają atakom, przetwarzają strumień jako wiarygodne wiadomości, co skutkuje zakresem nieprawidłowych skutków, takich jak nadmiarowe zamówienia elementu.  
  
## <a name="bindings-may-be-subject-to-reflection-attacks"></a>Powiązania mogą podlegać atakom odbicia  

 *Ataki odbicia* to odtwarzanie komunikatów z powrotem do nadawcy tak, jakby znajdowały się one w odbiorcy jako odpowiedź. Standardowe *wykrywanie powtarzania* w mechanizmie Windows Communication Foundation (WCF) nie obsługuje tego automatycznie.  
  
 Ataki odbicia są domyślnie zmniejszane, ponieważ model usługi WCF dodaje podpisany identyfikator wiadomości do żądania komunikatów i oczekuje podpisanego `relates-to` nagłówka w komunikatach odpowiedzi. W związku z tym komunikat żądania nie może zostać odtworzony jako odpowiedź. W scenariuszach z bezpiecznym niezawodnym komunikatem (RM) ataki na odbicie są ograniczane, ponieważ:  
  
- Schematy tworzenia sekwencji i tworzenia komunikatów odpowiedzi są różne.  
  
- W przypadku sekwencji jednostronnych wiadomości sekwencji wysyłane przez klienta nie mogą być ponownie odtwarzane, ponieważ klient nie może zrozumieć takich komunikatów.  
  
- W przypadku sekwencji dupleksowych dwa identyfikatory sekwencji muszą być unikatowe. W związku z tym nie można odtworzyć wychodzącego komunikatu sekwencji jako wiadomości przychodzącej sekwencji (wszystkie nagłówki sekwencji i treści są również podpisane).  
  
 Jedyne powiązania, które są podatne na ataki odbicia, są takie same, jak w przypadku adresów WS-Addressing: niestandardowe powiązania, które mają WS-Addressing wyłączone i używają zabezpieczeń opartych na kluczach symetryczne. Program nie <xref:System.ServiceModel.BasicHttpBinding> używa WS-Addressing domyślnie, ale nie korzysta z zabezpieczeń opartych na kluczach symetrycznych w taki sposób, aby mógł on być narażony na ataki.  
  
 Środki zaradcze dla powiązań niestandardowych nie ustanawiają kontekstu zabezpieczeń ani nie wymagają nagłówków WS-Addressing.  
  
## <a name="web-farm-attacker-replays-request-to-multiple-nodes"></a>Farma sieci Web: osoba atakująca odtwarza żądanie do wielu węzłów  

 Klient korzysta z usługi, która jest zaimplementowana w kolektywie serwerów sieci Web. Osoba atakująca odtwarza żądanie, które zostało wysłane do jednego węzła w farmie, do innego węzła w farmie. Ponadto, jeśli usługa zostanie ponownie uruchomiona, pamięć podręczna powtarzania zostanie opróżniona, co umożliwi atakującemu odtworzenie żądania. (Pamięć podręczna zawiera używane, wcześniej widoczne wartości sygnatur komunikatów i uniemożliwia ponowne odtwarzanie, aby te sygnatury mogły być używane tylko raz. Pamięć podręczna powtarzania nie jest udostępniana w kolektywie serwerów sieci Web.  
  
 Środki zaradcze obejmują:  
  
- Korzystanie z zabezpieczeń trybu komunikatów ze stanowymi tokenami kontekstu zabezpieczeń (z włączoną obsługą bezpiecznej konwersacji lub bez niej). Aby uzyskać więcej informacji, zobacz [jak: Tworzenie tokenu kontekstu zabezpieczeń dla bezpiecznej sesji](how-to-create-a-security-context-token-for-a-secure-session.md).  
  
- Skonfiguruj usługę tak, aby korzystała z zabezpieczeń na poziomie transportu.  
  
## <a name="see-also"></a>Zobacz też

- [Zagadnienia dotyczące zabezpieczeń](security-considerations-in-wcf.md)
- [Information Disclosure (ujawnienie informacji)](information-disclosure.md)
- [Elevation of Privilege (podniesienie uprawnień)](elevation-of-privilege.md)
- [Denial of Service (odmowa usługi)](denial-of-service.md)
- [Tampering (manipulowanie)](tampering.md)
- [Nieobsługiwane scenariusze](unsupported-scenarios.md)
