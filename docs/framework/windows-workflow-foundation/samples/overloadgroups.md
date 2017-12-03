---
title: OverloadGroups
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d1d547d2-f5fb-4de3-a959-ee6139a4f1ad
caps.latest.revision: "9"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: f644f09af3ce9e191dc6c5680472de4ef5ab727d
ms.sourcegitcommit: ce279f2d7fe2220e6ea0a25a8a7a5370ddf8d9f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/02/2017
---
# <a name="overloadgroups"></a>OverloadGroups
W tym przykładzie składa się z działania (`CreateLocation`), który ma dwie właściwości interesujące:  
  
1.  Niektóre wymagane jej argumentów i niektóre z nich opcjonalne.  
  
2.  Pozwala użytkownikowi na wybranie zapewnienie jeden z dwóch różnych zestawów argumentów.  
  
 Te zachowania, są wykonywane za pomocą te dwie funkcje:  
  
-   `[isRequired]`weryfikuje, że właściwość określonego działania jest przypisywanie, a jeśli nie, zgłasza wyjątek.  
  
-   `[OverloadGroup]`umieszcza razem zestaw argumentów, dzięki czemu można wybrać za pomocą jednego zestawu, lub inny użytkownik działania. Użytkownik nie można używać argumentów z różnych grup przeciążenia, w tym samym wystąpieniu.  
  
 Po skonfigurowaniu różnych przepływów pracy, należy wywołać <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> co powoduje zwrócenie <xref:System.Activities.Validation.ValidationResults> kolekcji <xref:System.Activities.Validation.Constraint>. Drukuj <xref:System.Activities.Validation.Constraint> obiekty do konsoli.  
  
### <a name="to-set-up-build-and-run-the-sample"></a>Aby skonfigurować, kompilacji, a następnie uruchom próbki  
  
1.  Otwórz **OverloadGroups.sln** przykładowe rozwiązanie w [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Tworzenie i uruchamianie rozwiązania.  
  
> [!IMPORTANT]
>  Próbki mogą być zainstalowane na tym komputerze. Przed kontynuowaniem sprawdź, czy są dostępne dla następującego katalogu (ustawienie domyślne).  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Jeśli ten katalog nie istnieje, przejdź do [Windows Communication Foundation (WCF) i Windows Workflow Foundation (WF) przykłady dla programu .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) pobrać wszystkie [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] i [!INCLUDE[wf1](../../../../includes/wf1-md.md)] próbek. W tym przykładzie znajduje się w następującym katalogu.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Validation\OverloadGroups`
