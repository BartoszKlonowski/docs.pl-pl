---
title: 'Instrukcje: tworzenie niestandardowego weryfikatora tożsamości klienta'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: f2d34e43-fa8b-46d2-91cf-d2960e13e16b
ms.openlocfilehash: 84982aca06bacb5718855602872fe4dab2376a9d
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96256069"
---
# <a name="how-to-create-a-custom-client-identity-verifier"></a>Instrukcje: tworzenie niestandardowego weryfikatora tożsamości klienta

Funkcja *Identity* programu Windows Communication Foundation (WCF) pozwala klientowi określić z wyprzedzeniem oczekiwaną tożsamość usługi. Za każdym razem, gdy serwer uwierzytelnia się na kliencie, tożsamość jest sprawdzana pod kątem oczekiwanej tożsamości. (Aby uzyskać wyjaśnienie tożsamości i sposobu jej działania, zobacz [tożsamość usługi i uwierzytelnianie](../feature-details/service-identity-and-authentication.md)).  
  
 W razie konieczności weryfikacja można dostosować przy użyciu niestandardowego weryfikatora tożsamości. Można na przykład przeprowadzić dodatkowe testy weryfikacyjne tożsamości usługi. W tym przykładzie weryfikator tożsamości niestandardowej sprawdza dodatkowe oświadczenia w certyfikacie X. 509 zwróconym z serwera. Aby zapoznać się z przykładową aplikacją, zobacz [przykład Identity Service](../samples/service-identity-sample.md).  
  
### <a name="to-extend-the-endpointidentity-class"></a>Aby zwiększyć klasę EndpointIdentity  
  
1. Zdefiniuj nową klasę, która dziedziczy z <xref:System.ServiceModel.EndpointIdentity> klasy. Ten przykład nazywa rozszerzenie `OrgEndpointIdentity` .  
  
2. Dodaj prywatne elementy członkowskie wraz z właściwościami, które będą używane przez <xref:System.ServiceModel.Security.IdentityVerifier> klasę rozszerzoną do przeprowadzenia sprawdzania tożsamości dla oświadczeń w tokenie zabezpieczającym zwracanym przez usługę. Ten przykład definiuje jedną właściwość: `OrganizationClaim` Właściwość.  
  
     [!code-csharp[c_HowToSetCustomClientIdentity#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#6)]
     [!code-vb[c_HowToSetCustomClientIdentity#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#6)]  
  
### <a name="to-extend-the-identityverifier-class"></a>Aby zwiększyć klasę IdentityVerifier  
  
1. Zdefiniuj nową klasę, która pochodzi od <xref:System.ServiceModel.Security.IdentityVerifier> . Ten przykład nazywa rozszerzenie `CustomIdentityVerifier` .  
  
     [!code-csharp[c_HowToSetCustomClientIdentity#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#7)]
     [!code-vb[c_HowToSetCustomClientIdentity#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#7)]  
  
2. Zastąp <xref:System.ServiceModel.Security.IdentityVerifier.CheckAccess%2A> metodę. Metoda określa, czy sprawdzanie tożsamości zakończyło się powodzeniem, czy niepowodzeniem.  
  
3. `CheckAccess`Metoda ma dwa parametry. Pierwszy jest wystąpieniem <xref:System.ServiceModel.EndpointIdentity> klasy. Drugim jest wystąpieniem <xref:System.IdentityModel.Policy.AuthorizationContext> klasy.  
  
     W implementacji metody Sprawdź kolekcję oświadczeń zwracanych przez <xref:System.IdentityModel.Policy.AuthorizationContext.ClaimSets%2A> Właściwość <xref:System.IdentityModel.Policy.AuthorizationContext> klasy i wykonaj testy uwierzytelniania zgodnie z wymaganiami. Ten przykład rozpoczyna się od znalezienia wszelkich roszczeń typu "nazwa wyróżniająca", a następnie porównuje nazwę z rozszerzeniem <xref:System.ServiceModel.EndpointIdentity> ( `OrgEndpointIdentity` ).  
  
     [!code-csharp[c_HowToSetCustomClientIdentity#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#1)]
     [!code-vb[c_HowToSetCustomClientIdentity#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#1)]  
  
### <a name="to-implement-the-trygetidentity-method"></a>Aby zaimplementować metodę TryGetIdentity  
  
1. Zaimplementuj <xref:System.ServiceModel.Security.IdentityVerifier.TryGetIdentity%2A> metodę, która określa, czy wystąpienie <xref:System.ServiceModel.EndpointIdentity> klasy może być zwracane przez klienta. Infrastruktura WCF najpierw wywołuje implementację `TryGetIdentity` metody w celu pobrania tożsamości usługi z wiadomości. Następnie infrastruktura wywołuje `CheckAccess` implementację z zwracanymi `EndpointIdentity` i <xref:System.IdentityModel.Policy.AuthorizationContext> .  
  
2. W `TryGetIdentity` metodzie należy umieścić następujący kod:  
  
     [!code-csharp[c_HowToSetCustomClientIdentity#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#2)]
     [!code-vb[c_HowToSetCustomClientIdentity#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#2)]  
  
### <a name="to-implement-a-custom-binding-and-set-the-custom-identityverifier"></a>Aby zaimplementować niestandardowe powiązanie i ustawić niestandardowe IdentityVerifier  
  
1. Utwórz metodę, która zwraca <xref:System.ServiceModel.Channels.Binding> obiekt. Ten przykład rozpoczyna Tworzenie wystąpienia <xref:System.ServiceModel.WSHttpBinding> klasy i ustawia jego tryb zabezpieczeń na <xref:System.ServiceModel.SecurityMode.Message> , a <xref:System.ServiceModel.MessageSecurityOverHttp.ClientCredentialType%2A> do <xref:System.ServiceModel.MessageCredentialType.None> .  
  
2. Utwórz <xref:System.ServiceModel.Channels.BindingElementCollection> za pomocą <xref:System.ServiceModel.WSHttpBinding.CreateBindingElements%2A> metody.  
  
3. Zwróć <xref:System.ServiceModel.Channels.SecurityBindingElement> z kolekcji i przerzucaj ją do <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> zmiennej.  
  
4. Ustaw <xref:System.ServiceModel.Channels.LocalClientSecuritySettings.IdentityVerifier%2A> Właściwość <xref:System.ServiceModel.Channels.LocalClientSecuritySettings> klasy na nowe wystąpienie `CustomIdentityVerifier` klasy utworzonej wcześniej.  
  
     [!code-csharp[c_HowToSetCustomClientIdentity#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#3)]
     [!code-vb[c_HowToSetCustomClientIdentity#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#3)]  
  
5. Zwracane niestandardowe powiązanie służy do tworzenia wystąpienia klienta i klasy. Klient może następnie wykonać sprawdzenie niestandardowej weryfikacji tożsamości usługi, jak pokazano w poniższym kodzie.  
  
     [!code-csharp[c_HowToSetCustomClientIdentity#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#4)]
     [!code-vb[c_HowToSetCustomClientIdentity#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#4)]  
  
## <a name="example"></a>Przykład  

 Poniższy przykład pokazuje kompletną implementację <xref:System.ServiceModel.Security.IdentityVerifier> klasy.  
  
 [!code-csharp[c_HowToSetCustomClientIdentity#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#5)]
 [!code-vb[c_HowToSetCustomClientIdentity#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#5)]  
  
## <a name="example"></a>Przykład  

 Poniższy przykład pokazuje kompletną implementację <xref:System.ServiceModel.EndpointIdentity> klasy.  
  
 [!code-csharp[c_HowToSetCustomClientIdentity#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#6)]
 [!code-vb[c_HowToSetCustomClientIdentity#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#6)]  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.ServiceModel.ServiceAuthorizationManager>
- <xref:System.ServiceModel.EndpointIdentity>
- <xref:System.ServiceModel.Security.IdentityVerifier>
- [Tożsamość usług — przykład](../samples/service-identity-sample.md)
- [Zasady autoryzacji](../samples/authorization-policy.md)
