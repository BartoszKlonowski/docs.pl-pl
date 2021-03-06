---
title: Wdrażanie projektu biblioteki WCF
ms.date: 03/30/2017
ms.assetid: 9f9222fe-d358-443c-9a49-12c5498e35e7
ms.openlocfilehash: e3a90f03639a888b4528a1962a24b7adc5d43c58
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96260893"
---
# <a name="deploying-a-wcf-library-project"></a>Wdrażanie projektu biblioteki WCF

W tym temacie opisano, jak można wdrożyć projekt biblioteki usług Windows Communication Foundation (WCF).  
  
## <a name="deploying-a-wcf-service-library"></a>Wdrażanie biblioteki usługi WCF  

 Biblioteka usługi WCF jest biblioteką dołączaną dynamicznie (DLL). W związku z tym nie można jej wykonać samodzielnie. Należy ją wdrożyć w środowisku hostingu. Aby uzyskać więcej informacji o tym procesie, zobacz [hosting i używanie usług WCF](/previous-versions/dotnet/articles/bb332338(v=msdn.10)).  
  
 Bibliotekę usług WCF można wdrożyć podobnie jak w przypadku każdej innej usługi WCF. Należy jednak pamiętać, że .NET Framework nie obsługuje konfiguracji bibliotek DLL. <xref:System.Configuration> obsługuje jeden plik konfiguracji na domenę aplikacji. Projekt biblioteki usług WCF pozwala uniknąć tego ograniczenia, dostarczając plik App.config biblioteki podczas opracowywania. Jednak plik App.config nie jest rozpoznawany po wdrożeniu.  
  
 Musisz przenieść kod konfiguracyjny do pliku konfiguracyjnego rozpoznawanego przez środowisko hostingu. W przypadku samodzielnego udostępniania należy skopiować zawartość pliku App.config do pliku App.config zawierającego plik wykonywalny. Jeśli używasz usług IIS do hostowania usługi, skopiuj zawartość pliku App.config do pliku Web.config katalogu wirtualnego.
