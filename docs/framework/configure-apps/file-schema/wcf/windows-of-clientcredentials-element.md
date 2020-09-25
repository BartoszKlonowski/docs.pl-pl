---
title: <windows><clientCredentials>elementu
ms.date: 03/30/2017
ms.assetid: 793e41c2-31ea-4159-abbc-2123bf097233
ms.openlocfilehash: 115e1822659c04ee37a7364f7b25616b52dc5efe
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91177829"
---
# <a name="windows-of-clientcredentials-element"></a>\<windows>\<clientCredentials>elementu

Określa ustawienia poświadczeń systemu Windows, które mają być używane do reprezentowania klienta.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<endpointBehaviors>**](endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<clientCredentials>**](clientcredentials.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<windows>**  
  
## <a name="syntax"></a>Składnia  
  
```xml  
<windows allowedImpersonationLevel="Identification/Impersonation/Delegation/Anonymous/None"
         allowNtlm="Boolean" />
```  
  
## <a name="attributes-and-elements"></a>Atrybuty i elementy  

 W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|  
|---------------|-----------------|  
|`allowedImpersonationLevel`|Ustawia preferencje personifikacji, które klient komunikuje się z serwerem. Tryb personifikacji wybierany przez klienta nie jest wymuszany na serwerze. Prawidłowe wartości to:<br /><br /> -Identyfikacja: serwer może uzyskać tożsamość i uprawnienia klienta, ale nie może personifikować klienta.<br />-Personifikacja: serwer może personifikować kontekst zabezpieczeń klienta w systemie lokalnym.<br />-Delegowanie: serwer może personifikować kontekst zabezpieczeń klienta w systemach zdalnych.<br />-Anonymous: serwer nie może personifikować lub zidentyfikować klienta.<br />-Brak: nie przypisano poziomu personifikacji.<br /><br /> Wartość domyślna to Identification. Ten atrybut jest typu <xref:System.Security.Principal.TokenImpersonationLevel> .|  
|`allowNtlm`|Ustawienie tej właściwości umożliwia `true` uwierzytelnianie w przypadku, gdy protokół Kerberos jest niedostępny.<br /><br /> Ustawienie tej właściwości `false` powoduje, że Windows Communication Foundation (WCF), aby najlepszym wysiłku zgłosić wyjątek, jeśli jest używany protokół NTLM. Należy pamiętać, że ustawienie tej właściwości na `false` nie zapobiega wysyłaniu poświadczeń NTLM za pośrednictwem sieci.|  
  
### <a name="child-elements"></a>Elementy podrzędne  

 Brak.  
  
### <a name="parent-elements"></a>Elementy nadrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|[\<clientCredentials>](clientcredentials.md)|Określa poświadczenia używane do uwierzytelniania klienta w usłudze.|  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.ServiceModel.Configuration.WindowsClientElement>
- <xref:System.ServiceModel.Configuration.ClientCredentialsElement>
- <xref:System.ServiceModel.Description.ClientCredentials>
- <xref:System.ServiceModel.Configuration.ClientCredentialsElement.Windows%2A>
- <xref:System.ServiceModel.Description.ClientCredentials>
- <xref:System.ServiceModel.Description.ClientCredentials.Windows%2A>
- <xref:System.ServiceModel.Security.WindowsClientCredential>
- [Zabezpieczanie klientów [WCF]](../../../wcf/securing-clients.md)
- [Praca z certyfikatami](../../../wcf/feature-details/working-with-certificates.md)
- [Zabezpieczanie usług i klientów](../../../wcf/feature-details/securing-services-and-clients.md)
