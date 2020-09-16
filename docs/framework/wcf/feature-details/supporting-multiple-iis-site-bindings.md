---
title: Obsługa wielu wiązań witryny usług IIS
description: Dowiedz się, w jaki sposób udostępnić wiele adresów bazowych, które używają tego samego protokołu w tej samej lokacji podczas hostowania usługi WCF w usługach IIS.
ms.date: 03/30/2017
ms.assetid: 40440495-254d-45c8-a8c6-b29f364892ba
ms.openlocfilehash: 6af4d885c7fc3d4dcc12ffb4bf6670f1a9b3d78c
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90546201"
---
# <a name="supporting-multiple-iis-site-bindings"></a>Obsługa wielu wiązań witryny usług IIS
W przypadku hostowania usługi Windows Communication Foundation (WCF) w obszarze Internet Information Services (IIS) 7,0 możesz chcieć podać wiele adresów bazowych, które używają tego samego protokołu w tej samej lokacji. Dzięki temu ta sama usługa może odpowiadać na wiele różnych identyfikatorów URI. Jest to przydatne, gdy chcesz hostować usługę, która nasłuchuje w systemach `http://www.contoso.com` i `http://contoso.com` . Warto również utworzyć usługę mającą adres podstawowy dla użytkowników wewnętrznych oraz oddzielny adres podstawowy dla użytkowników zewnętrznych. Przykład: `http://internal.contoso.com` i `http://www.contoso.com`.  
  
> [!NOTE]
> Ta funkcja jest dostępna tylko przy użyciu protokołu HTTP.  
  
## <a name="multiple-base-addresses"></a>Wiele adresów podstawowych  
 Ta funkcja jest dostępna tylko dla usług WCF hostowanych w ramach usług IIS. Ta funkcja nie jest domyślnie włączona. Aby włączyć tę opcję, należy dodać `multipleSiteBindingsEnabled` atrybut do <`serviceHostingEnvironment`> elementu w pliku Web.config i ustawić go na `true` , jak pokazano w poniższym przykładzie.  
  
```xml  
<serviceHostingEnvironment multipleSiteBindingsEnabled="true"/>  
```  
  
 W przypadku hostowania usługi WCF w ramach usług IIS program IIS tworzy jeden adres podstawowy na podstawie identyfikatora URI dla katalogu wirtualnego, który zawiera aplikację. Można dodać kolejne adresy podstawowe, które używają tego samego protokołu przy użyciu Menedżera Internet Information Services, aby dodać jedno lub więcej powiązań do witryny sieci Web. Dla każdego powiązania Określ protokół (HTTP lub HTTPS), adres IP, port i nazwę hosta. Aby uzyskać więcej informacji o korzystaniu z programu Internet Information Services Manager, zobacz [Menedżer usług IIS (IIS 7)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753842(v=ws.10)). Aby uzyskać więcej informacji na temat dodawania powiązań do lokacji, zobacz [Tworzenie witryny sieci Web (IIS 7)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc772350(v=ws.10))  
  
 Określenie wielu adresów bazowych dla tej samej witryny ma wpływ na zawartość strony pomocy programu WCF, importowanie schematu oraz informacje WSDL/MEX wygenerowane przez usługę. Na stronie pomocy programu WCF zostanie wyświetlony wiersz polecenia służący do generowania klienta WCF, który może komunikować się z usługą. Ten wiersz polecenia zawiera tylko pierwszy adres określony w powiązaniu IIS dla witryny sieci Web. Podobnie podczas importowania schematu używane są tylko pierwsze adresy podstawowe określone w powiązaniu IIS. Dane WSDL i MEX zawierają wszystkie adresy podstawowe określone w powiązaniach usług IIS.  
  
> [!WARNING]
> Oznacza to, że jeśli usługa ma dwa adresy podstawowe, jeden dla użytkowników wewnętrznych i jeden dla użytkowników zewnętrznych, oba są określone w informacjach WSDL/MEX generowanych przez usługę.
