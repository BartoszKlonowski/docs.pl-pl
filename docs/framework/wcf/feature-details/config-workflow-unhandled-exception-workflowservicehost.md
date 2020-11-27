---
title: 'Instrukcje: konfigurowanie zachowania dotyczącego nieobsługiwanego wyjątku przepływu pracy przy użyciu klasy WorkflowServiceHost'
ms.date: 03/30/2017
ms.assetid: 51b25c86-292c-43e4-8d13-273d2badc8ad
ms.openlocfilehash: 93eb2f4493b70f54336a5d47957c6913239088e5
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96264858"
---
# <a name="how-to-configure-workflow-unhandled-exception-behavior-with-workflowservicehost"></a>Instrukcje: konfigurowanie zachowania dotyczącego nieobsługiwanego wyjątku przepływu pracy przy użyciu klasy WorkflowServiceHost

<xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior>Jest zachowanie, które pozwala określić akcję do wykonania, jeśli wystąpi nieobsługiwany wyjątek w przepływie pracy hostowanym w <xref:System.ServiceModel.Activities.WorkflowServiceHost> . W tym temacie opisano sposób konfigurowania tego zachowania w pliku konfiguracji.  
  
### <a name="to-configure-workflowunhandledexceptionbehavior"></a>Aby skonfigurować WorkflowUnhandledExceptionBehavior  
  
1. Dodaj element <`workflowUnhandledException`> w elemencie <> w elemencie `behavior` <`serviceBehaviors`>, używając `action` atrybutu, aby określić akcję wykonywaną po wystąpieniu nieobsługiwanego wyjątku, jak pokazano w poniższym przykładzie.  
  
    ```xml  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="">  
          <workflowUnhandledException action="abandonAndSuspend"/>
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
    ```  
  
    > [!NOTE]
    > Poprzedni przykład konfiguracji używa uproszczonej konfiguracji. Aby uzyskać więcej informacji, zobacz [Uproszczona konfiguracja](../simplified-configuration.md).  
  
     Takie zachowanie można skonfigurować w kodzie, jak pokazano w poniższym przykładzie.  
  
    ```csharp  
    host.Description.Behaviors.Add(new WorkflowUnhandledExceptionBehavior { Action = WorkflowUnhandledExceptionAction.AbandonAndSuspend });  
    ```  
  
     `action`Atrybut <`workflowUnhandledException` elementu> można ustawić na jedną z następujących wartości:  
  
     **rzucić**  
     Przerywa wystąpienie w pamięci bez dotykania utrwalonego stanu wystąpienia (oznacza to, że wraca do ostatniego punktu utrwalania).  
  
     **abandonAndSuspend**  
     Przerywa wystąpienie w pamięci i aktualizuje wystąpienie trwałe, które zostanie zawieszone.  
  
     **Anuluj**  
     Wywołuje programy obsługi anulowania dla wystąpienia, a następnie kończy wystąpienie w pamięci, co może również usunąć je z magazynu wystąpień  
  
     **kończyć**  
     Kończy wystąpienie w pamięci i usuwa je z magazynu wystąpień.  
  
     Aby uzyskać więcej informacji na temat <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior> , zobacz [Rozszerzalność hosta usługi przepływu pracy](workflow-service-host-extensibility.md).  
  
## <a name="see-also"></a>Zobacz też

- [Rozszerzalność hosta usługi przepływu pracy](workflow-service-host-extensibility.md)
- [Usługi przepływu pracy](workflow-services.md)
