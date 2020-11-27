---
title: Konfigurowanie usługi współużytkowania portów Net.TCP
ms.date: 03/30/2017
ms.assetid: b6dd81fa-68b7-4e1b-868e-88e5901b7ea0
ms.openlocfilehash: 854cd7d26e26ee340d577b1bfd890f750e581a38
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96284150"
---
# <a name="configuring-the-nettcp-port-sharing-service"></a>Konfigurowanie usługi współużytkowania portów Net.TCP

Samoobsługowe usługi korzystające z transportu net. TCP mogą kontrolować kilka ustawień zaawansowanych, takich jak `ListenBacklog` i `MaxPendingAccepts` , które określają zachowanie bazowego gniazda TCP używanego do komunikacji sieciowej. Jednak te ustawienia dla każdego gniazda są stosowane tylko na poziomie powiązania, Jeśli powiązanie transportowe ma wyłączone Udostępnianie portów, które jest domyślnie włączone.  
  
 Gdy powiązanie net. TCP włącza Udostępnianie portów (przez ustawienie `portSharingEnabled =true` elementu powiązania transportu), niejawnie zezwala na proces zewnętrzny (mianowicie SMSvcHost.exe, który hostuje usługę udostępniania portów Net. TCP) do zarządzania gniazdem TCP w jego imieniu. Na przykład w przypadku używania protokołu TCP należy określić:  
  
```xml  
<tcpTransport portSharingEnabled="true"  />  
```  
  
 Po skonfigurowaniu w ten sposób wszystkie ustawienia gniazda określone w elemencie powiązania transportowego usługi są ignorowane na korzyść ustawień gniazda określonych przez SMSvcHost.exe.  
  
 Aby skonfigurować SMSvcHost.exe, Utwórz plik konfiguracji XML o nazwie SmSvcHost.exe.config i umieść go w tym samym katalogu fizycznym, co SMSvcHost.exe plik wykonywalny (na przykład C:\Windows\Microsoft.NET\Framework\v4.5).  
  
 Poniższy przykład ilustruje przykład SMSvcHost.exe.config, z ustawieniami domyślnymi dla wszystkich konfigurowalnych wartości jawnie.  
  
```xml  
<configuration>  
   <system.serviceModel.activation>  
       <net.tcp listenBacklog="16" <!-- 16 * # of processors -->  
          maxPendingAccepts="4"<!-- 4 * # of processors -->  
          maxPendingConnections="100"  
          receiveTimeout="00:00:30" <!-- 30 seconds -->  
          teredoEnabled="false">  
          <allowAccounts>  
             <!-- LocalSystem account -->  
             <add securityIdentifier="S-1-5-18"/>  
             <!-- LocalService account -->  
             <add securityIdentifier="S-1-5-19"/>  
             <!-- Administrators account -->  
             <add securityIdentifier="S-1-5-20"/>  
             <!-- Network Service account -->  
             <add securityIdentifier="S-1-5-32-544" />  
             <!-- IIS_IUSRS account (Vista only) -->  
             <add securityIdentifier="S-1-5-32-568"/>  
           </allowAccounts>  
       </net.tcp>  
    </system.serviceModel.activation>
</configuration>  
```  
  
## <a name="when-to-modify-smsvchostexeconfig"></a>Kiedy należy zmodyfikować SMSvcHost.exe.config  

 Ogólnie rzecz biorąc należy zachować ostrożność przy modyfikowaniu zawartości pliku SMSvcHost.exe.config, ponieważ wszystkie ustawienia konfiguracji określone w tym pliku mają wpływ na wszystkie usługi na komputerze, który używa usługi udostępniania portów Net. TCP. Obejmuje to aplikacje w systemie Windows Vista, które używają funkcji aktywacji TCP usługi aktywacji procesów systemu Windows (WAS).  
  
 Czasami jednak może zajść potrzeba zmiany konfiguracji domyślnej dla usługi udostępniania portów Net. TCP. Na przykład wartość domyślna `maxPendingAccepts` to 4 * liczba procesorów. Serwery obsługujące dużą liczbę usług korzystających z udostępniania portów mogą zwiększyć tę wartość, aby osiągnąć maksymalną przepływność. Wartość domyślna `maxPendingConnections` to 100. Należy rozważyć zwiększenie tej wartości także wtedy, gdy istnieje wielu współbieżnych klientów wywołujących usługę, a usługa porzuca połączenia klientów.  
  
 SMSvcHost.exe.config zawiera również informacje o tożsamościach procesów, które mogą korzystać z usługi udostępniania portów. Gdy proces nawiązuje połączenie z usługą udostępniania portów w celu korzystania ze współużytkowanego portu TCP, tożsamość procesu łączącego jest sprawdzana pod kątem listy tożsamości, które mogą korzystać z usługi udostępniania portów. Te tożsamości są określone jako identyfikatory zabezpieczeń (SID) w \<allowAccounts> sekcji pliku SMSvcHost.exe.config. Domyślnie uprawnienia do korzystania z usługi udostępniania portów są przyznawane kontom systemowym (LocalService, LocalSystem i NetworkService), a także członkami grupy Administratorzy. Aplikacje, które zezwalają na proces uruchomiony jako inna tożsamość (na przykład tożsamość użytkownika) w celu nawiązania połączenia z usługą udostępniania portów, muszą jawnie dodać odpowiedni identyfikator SID do SMSvcHost.exe.config (te zmiany nie są stosowane do momentu ponownego uruchomienia procesu SMSvc.exe).  
  
> [!NOTE]
> W systemach Windows Vista z włączoną funkcją kontroli konta użytkownika (UAC) Użytkownicy lokalni wymagają podwyższonego poziomu uprawnień nawet wtedy, gdy ich konto jest członkiem grupy Administratorzy. Aby umożliwić tym użytkownikom korzystanie z usługi udostępniania portów bez podniesienia uprawnień, identyfikator SID użytkownika (lub identyfikator SID grupy, w której użytkownik jest członkiem) musi zostać jawnie dodany do \<allowAccounts> sekcji SMSvcHost.exe.config.  
  
> [!WARNING]
> Domyślny SMSvcHost.exe.config plik określa niestandardową, `etwProviderId` Aby zapobiec zakłócaniu śledzenia przez SMSvcHost.exe.  
  
## <a name="see-also"></a>Zobacz też

- [\<net.tcp>](../../configure-apps/file-schema/wcf/net-tcp.md)
