---
title: 'Instrukcje: Rejestrowanie informacji o usługach'
description: Dowiedz się, jak rejestrować informacje o usługach. Ustaw właściwość AutoLog, jeśli chcesz, aby projekt usługi systemu Windows był współpracujący z dziennikiem zdarzeń aplikacji.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- AutoLog property
- services, logging information
- Windows Service applications, logging information about
- event logs, service applications
- application event logs, service applications
- logs, service applications
ms.assetid: c0d8140f-c055-4d8e-a2e0-37358a550116
ms.openlocfilehash: 2e5f1fd8ebbbb218e8d6eba9b2d30d05e7c0e62c
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96270579"
---
# <a name="how-to-log-information-about-services"></a>Instrukcje: Rejestrowanie informacji o usługach

Domyślnie wszystkie projekty usług systemu Windows mają możliwość korzystania z dziennika zdarzeń aplikacji i zapisywania do niego informacji oraz wyjątków. Użyj właściwości, <xref:System.ServiceProcess.ServiceBase.AutoLog%2A> Aby określić, czy chcesz, aby ta funkcja w aplikacji. Domyślnie rejestrowanie jest włączone dla każdej usługi utworzonej przy użyciu szablonu projektu usługi systemu Windows. Możesz użyć statycznej formy <xref:System.Diagnostics.EventLog> klasy do zapisywania informacji o usłudze w dzienniku bez konieczności tworzenia wystąpienia <xref:System.Diagnostics.EventLog> składnika lub ręcznego rejestrowania źródła.  
  
 Instalator usługi automatycznie rejestruje każdą usługę w projekcie jako prawidłowe źródło zdarzeń w dzienniku aplikacji na komputerze, na którym zainstalowano usługę, gdy rejestrowanie jest włączone. Usługa rejestruje informacje za każdym razem, gdy usługa jest uruchomiona, zatrzymana, wstrzymana, wznowiona, zainstalowana lub odinstalowana. Rejestruje także wszystkie błędy, które wystąpiły. Nie trzeba pisać żadnego kodu w celu zapisania wpisów w dzienniku, gdy jest używane zachowanie domyślne; usługa obsługuje to automatycznie.  
  
 Jeśli chcesz zapisać w dzienniku zdarzeń innym niż dziennik aplikacji, musisz ustawić <xref:System.ServiceProcess.ServiceBase.AutoLog%2A> Właściwość na `false` , utworzyć własny dziennik zdarzeń w kodzie usług i zarejestrować usługę jako prawidłowe Źródło wpisów dla tego dziennika. Następnie należy napisać kod, aby zarejestrować wpisy w dzienniku za każdym razem, gdy akcja jest zainteresowana.  
  
> [!NOTE]
> Jeśli używasz niestandardowego dziennika zdarzeń i skonfigurujesz aplikację usługi do zapisu w niej, nie musisz próbować uzyskać dostępu do dziennika zdarzeń przed ustawieniem <xref:System.ServiceProcess.ServiceBase.ServiceName%2A> właściwości usługi w kodzie. Dziennik zdarzeń wymaga wartości tej właściwości, aby zarejestrować usługę jako prawidłowe źródło zdarzeń.  
  
### <a name="to-enable-default-event-logging-for-your-service"></a>Aby włączyć domyślne rejestrowanie zdarzeń dla usługi  
  
- Ustaw <xref:System.ServiceProcess.ServiceBase.AutoLog%2A> Właściwość dla składnika na `true` .  
  
    > [!NOTE]
    > Domyślnie wartość tej właściwości to `true`. Nie musisz jawnie ustawiać tego ustawienia, chyba że tworzysz bardziej skomplikowane przetwarzanie, takie jak szacowanie warunku, a następnie Ustawianie <xref:System.ServiceProcess.ServiceBase.AutoLog%2A> właściwości na podstawie wyniku tego warunku.  
  
### <a name="to-disable-event-logging-for-your-service"></a>Aby wyłączyć rejestrowanie zdarzeń dla usługi  
  
- Ustaw <xref:System.ServiceProcess.ServiceBase.AutoLog%2A> Właściwość dla składnika na `false` .  
  
     [!code-csharp[VbRadconService#17](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#17)]
     [!code-vb[VbRadconService#17](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#17)]  
  
### <a name="to-set-up-logging-to-a-custom-log"></a>Aby skonfigurować rejestrowanie do dziennika niestandardowego  
  
1. Ustaw <xref:System.ServiceProcess.ServiceBase.AutoLog%2A> Właściwość na wartość `false` .  
  
    > [!NOTE]
    > Aby można było <xref:System.ServiceProcess.ServiceBase.AutoLog%2A> użyć dziennika niestandardowego, należy ustawić wartość false.  
  
2. Skonfiguruj wystąpienie <xref:System.Diagnostics.EventLog> składnika w aplikacji usługi systemu Windows.  
  
3. Utwórz dziennik niestandardowy, wywołując <xref:System.Diagnostics.EventLog.CreateEventSource%2A> metodę i określając ciąg źródłowy i nazwę pliku dziennika, który chcesz utworzyć.  
  
4. Ustaw <xref:System.Diagnostics.EventLog.Source%2A> Właściwość w <xref:System.Diagnostics.EventLog> wystąpieniu składnika na ciąg źródłowy, który został utworzony w kroku 3.  
  
5. Zapisz swoje wpisy, uzyskując dostęp do <xref:System.Diagnostics.EventLog.WriteEntry%2A> metody w <xref:System.Diagnostics.EventLog> wystąpieniu składnika.  
  
     Poniższy kod pokazuje, jak skonfigurować rejestrowanie w dzienniku niestandardowym.  
  
    > [!NOTE]
    > W tym przykładzie kodu wystąpienie <xref:System.Diagnostics.EventLog> składnika nosi nazwę `eventLog1` ( `EventLog1` w Visual Basic). Jeśli utworzono wystąpienie z inną nazwą w kroku 2, Zmień kod odpowiednio.  
  
     [!code-csharp[VbRadconService#14](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#14)]
     [!code-vb[VbRadconService#14](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#14)]  
    [!code-csharp[VbRadconService#15](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#15)]
    [!code-vb[VbRadconService#15](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#15)]  
  
## <a name="see-also"></a>Zobacz też

- [Wprowadzenie do aplikacji usług systemu Windows](introduction-to-windows-service-applications.md)
