---
title: Wyświetlanie dzienników komunikatów
ms.date: 03/30/2017
ms.assetid: 3012fa13-f650-45fb-aaea-c5cca8c7d372
ms.openlocfilehash: c8313b14a45051b7828a1ab223a3da63b2e7a153
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96291157"
---
# <a name="viewing-message-logs"></a>Wyświetlanie dzienników komunikatów

W tym temacie opisano sposób wyświetlania dzienników komunikatów.  
  
## <a name="viewing-message-logs-in-the-service-trace-viewer"></a>Wyświetlanie dzienników komunikatów w przeglądarce śledzenia usługi  

 Komunikat zostanie przekształcony, ponieważ jest przetwarzany przez funkcję WCF. W związku z tym rejestrowany komunikat odzwierciedla tylko zawartość komunikatu w punkcie, w którym została zarejestrowana, a nie zawartość w sieci.  
  
 Ponieważ dane wyjściowe rejestrowania komunikatów nie mają relacji z formatem transferu wiadomości, funkcja rejestrowania komunikatów zawsze wyświetla zdekodowany komunikat. Jeśli skonfigurowano rejestrowanie komunikatów prawidłowo, każdy zarejestrowany komunikat powinien być w postaci zwykłego tekstu. Na przykład format (zwykły tekst) rejestrowanych komunikatów nie ma wpływ na użycie kodera komunikatów binarnych.  
  
 Dane wyjściowe XmlWriterTraceListener to plik zawierający sekwencję fragmentów kodu XML. Należy pamiętać, że plik nie jest prawidłowym plikiem XML. Zalecane jest używanie [narzędzia Podgląd śledzenia usługi (SvcTraceViewer.exe)](../service-trace-viewer-tool-svctraceviewer-exe.md) do wyświetlania plików dziennika komunikatów. Aby uzyskać więcej informacji na temat korzystania z tego narzędzia, zobacz [Używanie przeglądarki śledzenia usługi do wyświetlania skorelowanych śladów i rozwiązywania problemów](./tracing/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting.md).  
  
 W przeglądarce śledzenia usługi komunikaty są wyświetlane na karcie **wiadomość** . Komunikaty, które spowodowały lub są związane z, błędem przetwarzania są wyróżnione kolorem żółtym (poziom ostrzegawczy) lub czerwony (poziom błędu), w zależności od wagi błędu. Dwukrotne kliknięcie komunikatu powoduje wyświetlenie śledzenia komunikatów w kontekście żądania przetwarzania.  
  
> [!NOTE]
> Jeśli komunikat nie ma nagłówka, żaden `<header/>` tag nie jest rejestrowany.  
  
## <a name="viewing-messages-logged-by-a-client-a-relay-and-a-service"></a>Wyświetlanie komunikatów zarejestrowanych przez klienta, przekaźnik i usługę  

 Środowisko może zawierać klienta, który wysyła komunikat do przekaźnika, który następnie przekazuje komunikat do usługi. Gdy funkcja rejestrowania komunikatów jest włączona we wszystkich trzech lokalizacjach, a wszystkie trzy dzienniki komunikatów są wyświetlane w [narzędziu Podgląd śledzenia usługi (SvcTraceViewer.exe)](../service-trace-viewer-tool-svctraceviewer-exe.md) jednocześnie, wymiany dzienników komunikatów będą nieprawidłowo renderowane. Dzieje się tak, ponieważ `CorrelationId` i `ActivityId` w nagłówku wiadomości nie są unikatowe dla każdej pary wysyłania i odbierania.  
  
 Aby rozwiązać ten problem, można użyć jednej z poniższych metod.  
  
- W dowolnym momencie należy wyświetlać dwa z trzech dzienników komunikatów w [narzędziu Podgląd śledzenia usługi (SvcTraceViewer.exe)](../service-trace-viewer-tool-svctraceviewer-exe.md) .  
  
- Jeśli musisz wyświetlić wszystkie trzy dzienniki w [narzędziu Podgląd śledzenia usługi (SvcTraceViewer.exe)](../service-trace-viewer-tool-svctraceviewer-exe.md) w tym samym czasie, możesz zmodyfikować usługę przekaźnika, tworząc nowe <xref:System.ServiceModel.Channels.Message> wystąpienie. To wystąpienie powinno być kopią treści wiadomości przychodzącej oraz wszystkimi nagłówkami z wyjątkiem `ActivityId` `Action` nagłówków i. Poniższy przykład kodu demonstruje, jak to zrobić.  
  
```csharp
Message outgoingMessage = Message.CreateMessage(incomingMessage.Version, incomingMessage.Headers.Action, incomingMessage.GetReaderAtBodyContents());  
  
for (int i = 0; i < incomingMessage.Headers.Count; i++)  
{  
   if (incomingMessage.Headers[i].Name.Equals("ActivityId", StringComparison.InvariantCultureIgnoreCase) ||  
incomingMessage.Headers[i].Name.Equals("Action", StringComparison.InvariantCultureIgnoreCase))  
   {  
      continue;  
    }  
    outgoingMessage.Headers.CopyHeaderFrom(incomingMessage, i);  
}  
```  
  
## <a name="exceptional-cases-for-inaccurate-message-logging-content"></a>Wyjątkowe przypadki dotyczące niedokładnej zawartości rejestrowania komunikatów  

 W następujących warunkach rejestrowane komunikaty mogą nie być dokładną reprezentacją strumienia oktetów obecnego w sieci.  
  
- W przypadku BasicHttpBinding nagłówki kopert są rejestrowane dla wiadomości przychodzących w przestrzeni nazw/Addressing/none.  
  
- Białe znaki mogą być niezgodne.  
  
- W przypadku wiadomości przychodzących puste elementy mogą być reprezentowane w różny sposób. Na przykład \<tag> \</tag> zamiast\<tag/>  
  
- W przypadku wyłączenia znanego rejestrowania przez dane OSOBowe są domyślnie lub jawne ustawienie enableLoggingKnownPii = "true".  
  
- Kodowanie jest włączone do przekształcania na UTF-8.  
  
## <a name="see-also"></a>Zobacz też

- [Narzędzie do przeglądania danych śledzenia usług (SvcTraceViewer.exe)](../service-trace-viewer-tool-svctraceviewer-exe.md)
- [Używanie przeglądarki danych śledzenia usługi do wyświetlania skorelowanych danych śledzenia i rozwiązywania problemów](./tracing/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting.md)
- [Rejestrowanie komunikatów](message-logging.md)
