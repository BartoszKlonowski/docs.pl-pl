---
title: Śledzenie przepływu pracy
ms.date: 03/30/2017
ms.assetid: 18737989-0502-4367-b5f6-617ebfb77c96
ms.openlocfilehash: fc27be295cbf0a83b65ff03e36f2aeffeda12db9
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90557505"
---
# <a name="workflow-tracing"></a>Śledzenie przepływu pracy
Śledzenie przepływu pracy umożliwia przechwytywanie informacji diagnostycznych przy użyciu detektorów śledzenia .NET Framework. Śledzenie można włączyć, jeśli problem zostanie wykryty w aplikacji, a następnie ponownie wyłączony po rozwiązaniu problemu. Istnieją dwa sposoby włączania śledzenia debugowania dla przepływów pracy. Można go skonfigurować przy użyciu podglądu śledzenia zdarzeń lub użyć <xref:System.Diagnostics> do wysyłania zdarzeń śledzenia do pliku.  
  
## <a name="enabling-debug-tracing-in-etw"></a>Włączanie śledzenia debugowania w ETW  
 Aby włączyć śledzenie przy użyciu funkcji ETW, Włącz kanał debugowania w Podgląd zdarzeń:  
  
1. Przejdź do węzła dzienniki analityczne i debugowania w Podgląd zdarzeń.  
  
2. W widoku drzewa w Podgląd zdarzeń przejdź do **Podgląd zdarzeń >aplikacje i usługi Dzienniki — >Microsoft->Windows->aplikacji**. Kliknij prawym przyciskiem myszy pozycję **serwer aplikacji — aplikacje** i wybierz polecenie **Widok->Pokaż dzienniki analityczne i debugowania**. Kliknij prawym przyciskiem myszy pozycję **Debuguj** i wybierz pozycję **Włącz dziennik**.  
  
3. Gdy przepływ pracy uruchamia debugowanie i ślady są emitowane do kanału debugowania ETW, można je wyświetlić w Podgląd zdarzeń. Przejdź do **Podgląd zdarzeń->Dzienniki aplikacji i usług->Microsoft->Windows->aplikacji**. Kliknij prawym przyciskiem myszy pozycję **Debuguj** i wybierz polecenie **Odśwież**.  
  
4. Domyślny rozmiar buforu śledzenia analitycznego to tylko 4 kilobajty (KB); zaleca się zwiększenie rozmiaru do 32 KB. Aby to zrobić, wykonaj następujące czynności.  
  
    1. Wykonaj następujące polecenie w bieżącym katalogu struktury (na przykład C:\Windows\Microsoft.NET\Framework\v4.0.21203): `wevtutil um Microsoft.Windows.ApplicationServer.Applications.man`  
  
    2. Zmień \<bufferSize> wartość w pliku Windows. ApplicationServer. Applications. Man na 32.  
  
        ```xml  
        <channel name="Microsoft-Windows-Application Server-Applications/Analytic" chid="ANALYTIC_CHANNEL" symbol="ANALYTIC_CHANNEL" type="Analytic" enabled="false" isolation="Application" message="$(string.MICROSOFT_WINDOWS_APPLICATIONSERVER_APPLICATIONS.channel.ANALYTIC_CHANNEL.message)" >  
                    <publishing>  
                      <bufferSize>32</bufferSize>  
                    </publishing>  
                  </channel>  
        ```  
  
    3. Wykonaj następujące polecenie w bieżącym katalogu struktury (na przykład C:\Windows\Microsoft.NET\Framework\v4.0.21203): `wevtutil im Microsoft.Windows.ApplicationServer.Applications.man`  
  
> [!NOTE]
> Jeśli używasz profilu klienta .NET Framework 4, musisz najpierw zarejestrować manifest ETW, uruchamiając następujące polecenie w katalogu .NET Framework 4: `ServiceModelReg.exe –i –c:etw`  
  
## <a name="enabling-debug-tracing-using-systemdiagnostics"></a>Włączanie śledzenia debugowania przy użyciu System. Diagnostics  
 Te odbiorniki można skonfigurować w pliku App.config aplikacji przepływu pracy lub Web.config dla usługi przepływu pracy. W tym przykładzie <xref:System.Diagnostics.TextWriterTraceListener> jest skonfigurowany do zapisywania informacji o śledzeniu do pliku MyTraceLog.txt w bieżącym katalogu.  
  
```xml  
<configuration>  
  <system.diagnostics>  
    <sources>  
      <source name="System.Activities" switchValue="Information">  
        <listeners>  
          <add name="textListener" />  
          <remove name="Default" />  
        </listeners>  
      </source>  
    </sources>  
    <sharedListeners>  
      <add name="textListener"  
           type="System.Diagnostics.TextWriterTraceListener"  
           initializeData="MyTraceLog.txt"  
           traceOutputOptions="ProcessId, DateTime" />  
    </sharedListeners>  
    <trace autoflush="true" indentsize="4">  
      <listeners>  
        <add name="textListener" />  
      </listeners>  
    </trace>  
  </system.diagnostics>  
</configuration>  
```  
  
## <a name="see-also"></a>Zobacz także

- [Monitorowanie aplikacji sieci szkieletowej systemu Windows Server](/previous-versions/appfabric/ee677251(v=azure.10))
- [Monitorowanie aplikacji przy użyciu sieci szkieletowej aplikacji](/previous-versions/appfabric/ee677276(v=azure.10))
