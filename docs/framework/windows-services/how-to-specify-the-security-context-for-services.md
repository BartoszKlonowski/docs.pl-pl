---
title: 'Instrukcje: Określanie kontekstu zabezpieczeń dla usług'
description: Określ kontekst zabezpieczeń usług. Usługi są uruchamiane w domyślnym kontekście konta systemowego mają inne prawa dostępu do zasobów systemowych niż zalogowany użytkownik.
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Service applications, security
- security [Visual Studio], contexts
- contexts, Visual Studio security
- security [Visual Studio], service applications
- ServiceProcessInstaller class, security context
- services, security
- ServiceInstaller class, security context
ms.assetid: 02187c7b-dbf2-45f2-96c2-e11010225a22
ms.openlocfilehash: dcf0680f1bcb0f0e927bdb37ea56f7b3025be09b
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96270540"
---
# <a name="how-to-specify-the-security-context-for-services"></a>Instrukcje: Określanie kontekstu zabezpieczeń dla usług

Domyślnie usługi są uruchamiane w innym kontekście zabezpieczeń niż zalogowany użytkownik. Usługi są uruchamiane w kontekście domyślnego konta systemowego o nazwie `LocalSystem` , które daje im różne uprawnienia dostępu do zasobów systemowych niż użytkownik. Możesz zmienić to zachowanie, aby określić inne konto użytkownika, w ramach którego ma zostać uruchomiona usługa.  
  
 Kontekst zabezpieczeń jest ustawiany przez manipulowanie <xref:System.ServiceProcess.ServiceProcessInstaller.Account%2A> właściwością procesu, w którym działa usługa. Ta właściwość umożliwia ustawienie jednego z czterech typów kont:  
  
- `User`, co powoduje, że system monituje o podanie prawidłowej nazwy użytkownika i hasła podczas instalacji usługi i jest uruchamiany w kontekście konta określonego przez pojedynczego użytkownika w sieci;  
  
- `LocalService`, który działa w kontekście konta, które działa jako użytkownik nieuprzywilejowany na komputerze lokalnym i przedstawia anonimowe poświadczenia na dowolnym serwerze zdalnym;  
  
- `LocalSystem`, który działa w kontekście konta, które zapewnia szerokie uprawnienia lokalne, i przedstawia poświadczenia komputera na dowolnym serwerze zdalnym;  
  
- `NetworkService`, który działa w kontekście konta, które działa jako użytkownik nieuprzywilejowany na komputerze lokalnym i przedstawia poświadczenia komputera na dowolnym serwerze zdalnym.  
  
 Aby uzyskać więcej informacji, zobacz <xref:System.ServiceProcess.ServiceAccount> Wyliczenie.  
  
### <a name="to-specify-the-security-context-for-a-service"></a>Aby określić kontekst zabezpieczeń dla usługi  
  
1. Po utworzeniu usługi należy dodać do niej niezbędne Instalatory. Aby uzyskać więcej informacji, zobacz [jak: Dodawanie instalatorów do aplikacji usługi](how-to-add-installers-to-your-service-application.md).  
  
2. W projektancie uzyskaj dostęp do `ProjectInstaller` klasy i kliknij Instalatora procesów usługi dla usługi, z którą pracujesz.  
  
    > [!NOTE]
    > Dla każdej aplikacji usługi w klasie istnieją co najmniej dwa składniki instalacyjne `ProjectInstaller` — jedną, która instaluje procesy dla wszystkich usług w projekcie, oraz jeden Instalator dla każdej usługi zawierającej daną aplikację. W tym przypadku należy wybrać opcję <xref:System.ServiceProcess.ServiceProcessInstaller> .  
  
3. W oknie **Właściwości** Ustaw <xref:System.ServiceProcess.ServiceProcessInstaller.Account%2A> odpowiednią wartość.  
  
## <a name="see-also"></a>Zobacz też

- [Wprowadzenie do aplikacji usług systemu Windows](introduction-to-windows-service-applications.md)
- [Instrukcje: Dodawanie instalatorów od aplikacji usług](how-to-add-installers-to-your-service-application.md)
- [Instrukcje: Tworzenie usług systemu Windows](how-to-create-windows-services.md)
