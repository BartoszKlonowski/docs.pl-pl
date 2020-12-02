---
ms.openlocfilehash: ab9431780422dfece5dcf8007d13e6d584f5118f
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96478388"
---
### <a name="avoiding-endless-recursion-for-iworkflowinstancemanagementtransactedcancel-and-iworkflowinstancemanagementtransactedterminate"></a>Unikanie rekursji nieskończoności dla IWorkflowInstanceManagement. TransactedCancel i IWorkflowInstanceManagement. TransactedTerminate

#### <a name="details"></a>Szczegóły

W pewnych okolicznościach przy użyciu programu <xref:System.ServiceModel.Activities.IWorkflowInstanceManagement.TransactedCancel%2A?displayProperty=nameWithType> lub <xref:System.ServiceModel.Activities.IWorkflowInstanceManagement.TransactedTerminate%2A?displayProperty=nameWithType> interfejsów API do anulowania lub kończenia wystąpienia usługi przepływu pracy wystąpienie przepływu pracy może napotkać przepełnienie stosu z powodu nieskończonej rekursji, gdy `Workflow` środowisko uruchomieniowe próbuje utrzymać wystąpienie usługi w ramach przetwarzania żądania. Ten problem występuje, gdy wystąpienie przepływu pracy jest w stanie, w którym oczekuje na ukończenie innego oczekującego żądania WCF do innej usługi. `TransactedCancel`Operacje i `TransactedTerminate` tworzą elementy robocze, które są umieszczane w kolejce dla wystąpienia usługi przepływu pracy. Te elementy robocze nie są wykonywane w ramach przetwarzania `TransactedCancel/TransactedTerminate` żądania. Ponieważ wystąpienie usługi przepływu pracy jest zajęte, czekając na zakończenie innych oczekujących żądań WCF, element roboczy został utworzony w kolejce. `TransactedCancel/TransactedTerminate`Operacja zostanie ukończona i kontrola zostanie zwrócona z powrotem do klienta. Gdy transakcja skojarzona z operacją zostanie podjęta `TransactedCancel/TransactedTerminate` , musi zachować stan wystąpienia usługi przepływu pracy. Ale ponieważ istnieje oczekujące `WCF` żądanie wystąpienia, środowisko uruchomieniowe przepływu pracy nie może utrwalać wystąpienia usługi przepływu pracy, a pętla rekursji nieskończonej prowadzi do przepełnienia stosu. Ponieważ `TransactedCancel` i `TransactedTerminate` Utwórz tylko element roboczy w pamięci, fakt, że transakcja istnieje, nie ma żadnego efektu. Wycofanie transakcji nie odrzuci elementu pracy. Aby rozwiązać ten problem, w .NET Framework 4.7.2 został wprowadzony, `AppSetting` który można dodać do `web.config/app.config` usługi przepływu pracy, która informuje go o ignorowaniu transakcji dla `TransactedCancel` i `TransactedTerminate` . Pozwala to na zatwierdzenie transakcji bez oczekiwania na utrwalenie wystąpienia przepływu pracy. Element appSetting dla tej funkcji ma nazwę `microsoft:WorkflowServices:IgnoreTransactionsForTransactedCancelAndTransactedTerminate` . Wartość wskazuje, `true` że transakcja powinna być ignorowana, co pozwala uniknąć przepełnienia stosu. Wartość domyślna tego element appSetting to `false` , więc nie ma to żadnego oddziaływać na istniejące wystąpienia usługi przepływu pracy.

#### <a name="suggestion"></a>Sugestia

Jeśli używasz programu AppFabric lub innego <xref:System.ServiceModel.Activities.IWorkflowInstanceManagement> klienta i napotkasz przepełnienie stosu w wystąpieniu usługi przepływu pracy podczas próby anulowania lub zakończenia wystąpienia przepływu pracy, możesz dodać następujące elementy do `<appSettings>` sekcji pliku web.config/app.config dla usługi przepływu pracy:

<pre><code class="lang-xml">&lt;add key=&quot;microsoft:WorkflowServices:IgnoreTransactionsForTransactedCancelAndTransactedTerminate&quot; value=&quot;true&quot;/&gt;&#13;&#10;</code></pre>

Jeśli problem nie wystąpi, nie musisz tego robić.

| Nazwa    | Wartość       |
|:--------|:------------|
| Zakres   | Edge        |
| Wersja | 4.7.2       |
| Typ    | Przekierowanie |
