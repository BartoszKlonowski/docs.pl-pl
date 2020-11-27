---
title: Zagadnienia dotyczące zabezpieczeń internetowych i zdalnego dostępu
description: Informacje o kwestiach dotyczących zabezpieczeń w odniesieniu do usług zdalnych, które umożliwiają skonfigurowanie przezroczystego wywoływania między domenami aplikacji, procesami lub komputerami.
ms.date: 03/30/2017
helpviewer_keywords:
- code security, remoting
- remoting, security
- security [.NET Framework], remoting
- secure coding, remoting
ms.assetid: 125d2ab8-55a4-4e5f-af36-a7d401a37ab0
ms.openlocfilehash: 883c20483c4d315a45e1f4dab959d42cbb6e3c4b
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96288206"
---
# <a name="security-and-remoting-considerations"></a>Zagadnienia dotyczące zabezpieczeń internetowych i zdalnego dostępu

[!INCLUDE[net_security_note](../../../includes/net-security-note-md.md)]

Komunikacja zdalna umożliwia skonfigurowanie przezroczystego wywoływania między domenami aplikacji, procesami lub komputerami. Jednak przechodzenie przez stos zabezpieczeń dostępu kodu nie może przekroczyć procesu ani granic maszyn (stosuje się między domenami aplikacji tego samego procesu).  
  
 Każda klasa, która jest zdalna (pochodząca z <xref:System.MarshalByRefObject> klasy) musi podejmować odpowiedzialność za zabezpieczenia. Kod powinien być używany tylko w środowiskach zamkniętych, w których kod wywołujący może być niejawnie zaufany lub wywołania komunikacji zdalnej powinny być zaprojektowane tak, aby nie podlegać chronionemu kodowi, który mógłby być użyty złośliwie.  
  
 Ogólnie rzecz biorąc nie należy ujawniać metod, właściwości ani zdarzeń chronionych przez deklaracyjne [LinkDemand](link-demands.md) i <xref:System.Security.Permissions.SecurityAction.InheritanceDemand> kontrole zabezpieczeń. W przypadku komunikacji zdalnej te sprawdzenia nie są wymuszane. Inne sprawdzenia zabezpieczeń, takie jak <xref:System.Security.Permissions.SecurityAction.Demand> , [Assert](using-the-assert-method.md)i tak dalej, działają między domenami aplikacji w ramach procesu, ale nie działają w scenariuszach obejmujących wiele procesów lub międzymaszynowo.  
  
## <a name="protected-objects"></a>Chronione obiekty  

 Niektóre obiekty przechowują stan zabezpieczeń we własnym zakresie. Tych obiektów nie należy przekazywać do niezaufanego kodu, który następnie uzyskuje autoryzację zabezpieczeń poza jej własnymi uprawnieniami.  
  
 Przykładem jest utworzenie <xref:System.IO.FileStream> obiektu. <xref:System.Security.Permissions.FileIOPermission>Jest zapotrzebowanie na czas tworzenia i, jeśli zakończy się pomyślnie, obiekt pliku jest zwracany. Jeśli jednak odwołanie do obiektu zostanie przesłane do kodu bez uprawnień do pliku, obiekt będzie mógł odczytywać i zapisywać dane w tym pliku.  
  
 Najprostszą obroną takiego obiektu jest zażądanie tego samego **FileIOPermission** dowolnego kodu, który poszukuje odwołania do obiektu za pomocą publicznego elementu interfejsu API.  
  
## <a name="application-domain-crossing-issues"></a>Problemy z przekroczeniem domeny aplikacji  

 Aby izolować kod w zarządzanych środowiskach hostingu, często generowane są wiele podrzędnych domen aplikacji z jawnymi zasadami zmniejszającymi poziomy uprawnień dla różnych zestawów. Jednak zasady dla tych zestawów pozostaną niezmienione w domyślnej domenie aplikacji. Jeśli jedna z domen aplikacji podrzędnych może wymusić załadowanie zestawu przez domyślną domenę aplikacji, efekt izolacji kodu zostanie utracony, a typy w załadowanym zestawie będzie można uruchamiać kod na wyższym poziomie zaufania.  
  
 Domena aplikacji może zmusić inną domenę aplikacji do załadowania zestawu i uruchomienia kodu zawartego w nim przez wywołanie serwera proxy do obiektu hostowanego w innej domenie aplikacji. Aby uzyskać serwer proxy domeny między aplikacjami, domena aplikacji hostującym obiekt musi być dystrybuowana przez parametr wywołania metody lub wartość zwracaną. Lub, jeśli domena aplikacji została właśnie utworzona, twórca ma domyślnie serwer proxy do <xref:System.AppDomain> obiektu. W ten sposób, aby uniknąć przerywania izolacji kodu, domena aplikacji o wyższym poziomie zaufania nie powinna rozpowszechniać odwołań do obiektów zorganizowanych przez odwołanie (wystąpień klas pochodnych od <xref:System.MarshalByRefObject> ) w domenie do domen aplikacji o niższych poziomach zaufania.  
  
 Zwykle domyślna domena aplikacji tworzy podrzędne domeny aplikacji z obiektem kontrolnym w każdym z nich. Obiekt Control zarządza nową domeną aplikacji i okresowo przyjmuje zamówienia z domyślnej domeny aplikacji, ale nie może fizycznie skontaktować się bezpośrednio z domeną. Czasami domyślna domena aplikacji wywołuje swój serwer proxy do obiektu Control. Mogą jednak wystąpić sytuacje, w których obiekt sterowania może wywoływać z powrotem do domyślnej domeny aplikacji. W takich przypadkach domyślna domena aplikacji przekazuje obiekt wywołania zwrotnego marshal-by-reference do konstruktora obiektu Control. Jest odpowiedzialny za obiekt sterowania do ochrony tego serwera proxy. Jeśli obiekt sterowania umieści serwer proxy w publicznym polu statycznym klasy publicznej lub w inny sposób publicznie ujawniony serwer proxy, zostanie otwarty niebezpieczny mechanizm dla innego kodu, który będzie mógł wywoływać z powrotem do domyślnej domeny aplikacji. Z tego powodu obiekty sterujące są zawsze niejawnie zaufane, aby zachować prywatny serwer proxy.  
  
## <a name="see-also"></a>Zobacz też

- [Wytyczne dotyczące bezpiecznego programowania](../../standard/security/secure-coding-guidelines.md)
