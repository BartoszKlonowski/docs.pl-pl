---
title: Używanie śledzenia do rozwiązywania problemów z aplikacjami
ms.date: 03/30/2017
ms.assetid: 8851adde-c3c2-4391-9523-d8eb831490af
ms.openlocfilehash: fc9427d0c06ed67ea69669cab2aae64f39f7c10c
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90551291"
---
# <a name="using-tracking-to-troubleshoot-applications"></a>Używanie śledzenia do rozwiązywania problemów z aplikacjami
Funkcja Windows Workflow Foundation (WF) umożliwia śledzenie informacji związanych z przepływem pracy w celu uzyskania szczegółów dotyczących wykonywania Windows Workflow Foundation aplikacji lub usługi. Hosty Windows Workflow Foundation mogą przechwytywać zdarzenia przepływu pracy podczas wykonywania wystąpienia przepływu pracy. Jeśli przepływ pracy generuje błędy lub wyjątki, można użyć szczegółów śledzenia Windows Workflow Foundation do rozwiązywania problemów z przetwarzaniem.  
  
## <a name="troubleshooting-a-wf-using-wf-tracking"></a>Rozwiązywanie problemów z usługą WF przy użyciu śledzenia WF  
 Aby wykryć błędy w trakcie przetwarzania działania Windows Workflow Foundation, można włączyć śledzenie z profilem śledzenia, który wysyła zapytanie o <xref:System.Activities.Tracking.ActivityStateRecord> stan błędu. Odpowiednie zapytanie jest określone w poniższym kodzie.  
  
```xml  
<activityStateQueries>  
              <activityStateQuery activityName="*">  
                <states>  
                  <state name="Faulted" />  
                </states>  
              </activityStateQuery>  
 </activityStateQueries>  
```  
  
 Jeśli błąd jest propagowany i obsługiwany w ramach procedury obsługi błędów (na przykład <xref:System.Activities.Statements.TryCatch> działania), można go wykryć przy użyciu <xref:System.Activities.Tracking.FaultPropagationRecord> . <xref:System.Activities.Tracking.FaultPropagationRecord>Wskazuje aktywność źródłową błędu i nazwę programu obsługi błędów. <xref:System.Activities.Tracking.FaultPropagationRecord>Zawiera szczegóły błędu w formie stosu wyjątków dla błędu. Zapytanie w celu subskrybowania elementu <xref:System.Activities.Tracking.FaultPropagationRecord> jest pokazane w poniższym przykładzie.  
  
```xml  
<faultPropagationQueries>  
              <faultPropagationQuery faultSourceActivityName ="*" faultHandlerActivityName="*"/>  
 </faultPropagationQueries>  
```  
  
 Jeśli błąd nie jest obsługiwany w przepływie pracy, powoduje to nieobsłużony wyjątek w wystąpieniu przepływu pracy, a wystąpienie przepływu pracy zostało przerwane. Aby zrozumieć szczegóły nieobsługiwanego wyjątku, profil śledzenia musi wysyłać zapytania do rekordu wystąpienia przepływu pracy w `state name="UnhandledException"` sposób określony w poniższym przykładzie.  
  
```xml  
<workflowInstanceQueries>  
              <workflowInstanceQuery>  
                <states>  
                  <state name="UnhandledException" />  
                </states>  
              </workflowInstanceQuery>  
</workflowInstanceQueries>  
```  
  
 Gdy wystąpienie przepływu pracy napotka nieobsłużony wyjątek, <xref:System.Activities.Tracking.WorkflowInstanceUnhandledExceptionRecord> obiekt jest emitowany, jeśli śledzenie Windows Workflow Foundation zostało włączone.  
  
 Ten rekord śledzenia zawiera szczegóły błędu w formie stosu wyjątków. Ma szczegóły dotyczące źródła błędu (na przykład działania), które uległy awarii i spowodowały nieobsłużony wyjątek. Aby subskrybować zdarzenia błędów z Windows Workflow Foundation, Włącz śledzenie przez dodanie uczestnika śledzenia. Skonfiguruj tego uczestnika przy użyciu profilu śledzenia, który wysyła zapytania o `ActivityStateQuery (state="Faulted")` , <xref:System.Activities.Tracking.FaultPropagationRecord> i `WorkflowInstanceQuery (state="UnhandledException")` .  
  
 Jeśli śledzenie jest włączone przy użyciu uczestnika śledzenia funkcji ETW, zdarzenia błędów są emitowane do sesji ETW. Zdarzenia można wyświetlić za pomocą Podgląd zdarzeń Podgląd zdarzeń. Można to znaleźć w węźle **Podgląd zdarzeń->Dzienniki aplikacji i usług — >Microsoft->Windows->Application Server-Applications** w kanale analitycznym.  
  
## <a name="see-also"></a>Zobacz także

- [Monitorowanie aplikacji sieci szkieletowej systemu Windows Server](/previous-versions/appfabric/ee677251(v=azure.10))
- [Monitorowanie aplikacji przy użyciu sieci szkieletowej aplikacji](/previous-versions/appfabric/ee677276(v=azure.10))
