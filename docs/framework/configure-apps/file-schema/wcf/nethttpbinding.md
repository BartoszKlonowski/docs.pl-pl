---
title: <netHttpBinding>
ms.date: 03/30/2017
ms.assetid: b0d81ca0-87c5-4090-8baa-e390fd3656d2
ms.openlocfilehash: f788849a9b11b81b4542eb2c6f855a8d4db4dd44
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90555487"
---
# \<netHttpBinding>
Reprezentuje powiązanie, za pomocą którego usługa Windows Communication Foundation (WCF) może skonfigurować i uwidocznić punkty końcowe, które mogą komunikować się za pośrednictwem protokołu HTTP. W przypadku użycia z umową dupleksową zostaną użyte gniazda sieci Web, w przeciwnym razie zostanie użyta wartość HTTP.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<bindings>**](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<netHttpBinding>**  
  
## <a name="syntax"></a>Składnia  
  
```xml  
<netHttpBinding>
  <binding allowCookies="Boolean"
           bypassProxyOnLocal="Boolean"
           closeTimeout="TimeSpan"
           hostNameComparisonMode="StrongWildCard/Exact/WeakWildcard"
           maxBufferPoolSize="Integer"
           maxBufferSize="Integer"
           maxReceivedMessageSize="Integer"
           messageEncoding="Binary/Text/Mtom"
           name="String"
           openTimeout="TimeSpan"
           proxyAddress="URI"
           receiveTimeout="TimeSpan"
           sendTimeout="TimeSpan"
           textEncoding="UnicodeFffeTextEncoding/Utf16TextEncoding/Utf8TextEncoding"
           transferMode="Buffered/Streamed/StreamedRequest/StreamedResponse"
           useDefaultWebProxy="Boolean">
    <security mode="None/Transport/Message/TransportWithMessageCredential/TransportCredentialOnly">
      <transport clientCredentialType="None/Basic/Digest/Ntlm/Windows/Certificate"
                 proxyCredentialType="None/Basic/Digest/Ntlm/Windows"
                 realm="string" />
      <message algorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15"
               clientCredentialType="UserName/Certificate" />
    </security>
    <readerQuotas maxArrayLength="Integer"
                  maxBytesPerRead="Integer"
                  maxDepth="Integer"
                  maxNameTableCharCount="Integer"
                  maxStringContentLength="Integer" />
  </binding>
</netHttpBinding>
```  
  
## <a name="type"></a>Typ  
 `Type`  
  
## <a name="attributes-and-elements"></a>Atrybuty i elementy  
 W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|  
|---------------|-----------------|  
|`allowCookies`|Wartość logiczna wskazująca, czy klient akceptuje pliki cookie i propaguje je do przyszłych żądań. Wartość domyślna to `false`.<br /><br /> Tej właściwości można użyć podczas współpracy z usługami sieci Web ASMX, które korzystają z plików cookie. W ten sposób można mieć pewność, że pliki cookie zwrócone z serwera są automatycznie kopiowane do wszystkich przyszłych żądań klientów dla tej usługi.|  
|`bypassProxyOnLocal`|Wartość logiczna wskazująca, czy pominąć serwer proxy dla adresów lokalnych. Wartość domyślna to `false`.<br /><br /> Zasób internetowy jest lokalny, jeśli ma adres lokalny. Adres lokalny to taki, który znajduje się na tym samym komputerze, w lokalnej sieci LAN lub intranecie i jest identyfikowany, syntaktycznie przez brak kropki (.), jak w identyfikatorach URI `http://webserver/` i `http://localhost/` .<br /><br /> Ustawienie tego atrybutu określa, czy punkty końcowe skonfigurowane za pomocą BasicHttpBinding używają serwera proxy podczas uzyskiwania dostępu do zasobów lokalnych. Jeśli ten atrybut jest `true` , żądania do lokalnych zasobów internetowych nie korzystają z serwera proxy. Jeśli klient ma przechodzić przez serwer proxy podczas rozmowy z usługami na tym samym komputerze, gdy ten atrybut jest ustawiony na, należy użyć nazwy hosta (zamiast hosta lokalnego) `true` .<br /><br /> Gdy ten atrybut ma wartość `false` , wszystkie żądania internetowe są nawiązywane za pomocą serwera proxy.|  
|`closeTimeout`|<xref:System.TimeSpan>Wartość określająca interwał czasu podanego do ukończenia operacji zamknięcia. Ta wartość powinna być większa lub równa <xref:System.TimeSpan.Zero> . Wartość domyślna to 00:01:00.|  
|`hostNameComparisonMode`|Określa tryb porównania nazw hostów HTTP używany do analizowania identyfikatorów URI. Ten atrybut jest typu <xref:System.ServiceModel.HostNameComparisonMode> , który wskazuje, czy nazwa hosta jest używana do uzyskiwania dostępu do usługi podczas dopasowywania identyfikatora URI. Wartość domyślna to <xref:System.ServiceModel.HostNameComparisonMode.StrongWildcard> , co powoduje ignorowanie nazwy hosta w dopasowaniu.|  
|`maxBufferPoolSize`|Wartość całkowita określająca maksymalną ilość pamięci przydzieloną do użytku przez Menedżera buforów komunikatów, które odbierają komunikaty z kanału. Wartość domyślna to 524288 (0x80000) b.<br /><br /> Menedżer buforów minimalizuje koszt używania buforów przy użyciu puli buforów. Bufory są wymagane do przetwarzania komunikatów przez usługę, gdy wychodzą z kanału. Jeśli w puli buforów nie ma wystarczającej ilości pamięci do przetworzenia ładowania komunikatów, Menedżer buforów musi przydzielić dodatkową pamięć ze sterty CLR, co spowoduje zwiększenie nakładu wyrzucania elementów bezużytecznych. Rozbudowana alokacja ze sterty elementów bezużytecznych CLR wskazuje, że rozmiar puli buforów jest zbyt mały i można zwiększyć wydajność z większą alokacją przez zwiększenie limitu określonego przez ten atrybut.|  
|`maxBufferSize`|Wartość całkowita, która określa maksymalny rozmiar bufora, w bajtach, który przechowuje komunikaty podczas przetwarzania dla punktu końcowego skonfigurowanego za pomocą tego powiązania. Wartość domyślna to 65 536 bajtów.|  
|`maxReceivedMessageSize`|Dodatnia liczba całkowita, która określa maksymalny rozmiar wiadomości w bajtach, w tym nagłówki, dla wiadomości, które można odbierać w kanale skonfigurowanym za pomocą tego powiązania. Nadawca odbiera błąd protokołu SOAP, jeśli komunikat jest zbyt duży dla odbiornika. Odbiorca odrzuca komunikat i tworzy wpis zdarzenia w dzienniku śledzenia. Wartość domyślna to 65 536 bajtów.|  
|`messageEncoding`|Definiuje koder używany do kodowania komunikatu protokołu SOAP. Prawidłowe wartości to:<br /><br /> -Text: Użyj kodera wiadomości tekstowej.<br />-MTOM: Użyj mechanizmu organizacji przesyłania komunikatów 1,0 (MTOM) kodera.<br /><br /> Wartość domyślna to Text. Ten atrybut jest typu <xref:System.ServiceModel.WSMessageEncoding> .|  
|`name`|Ciąg zawierający nazwę konfiguracji powiązania. Ta wartość powinna być unikatowa, ponieważ jest używana jako identyfikacja dla powiązania. Począwszy od .NET Framework 4, powiązania i zachowania nie muszą mieć nazwy. Aby uzyskać więcej informacji na temat konfiguracji domyślnej i powiązań pustego i zachowań, zobacz [Uproszczona konfiguracja](../../../wcf/simplified-configuration.md) i [Uproszczona konfiguracja dla usług WCF](../../../wcf/samples/simplified-configuration-for-wcf-services.md).|  
|`openTimeout`|<xref:System.TimeSpan>Wartość, która określa przedział czasu podanego na zakończenie operacji otwarcia. Ta wartość powinna być większa lub równa <xref:System.TimeSpan.Zero> . Wartość domyślna to 00:01:00.|  
|`proxyAddress`|Identyfikator URI, który zawiera adres serwera proxy HTTP. Jeśli `useSystemWebProxy` jest ustawiona na `true` , to ustawienie musi być `null` . Wartość domyślna to `null`.|  
|`receiveTimeout`|Wartość określająca <xref:System.TimeSpan> interwał czasu podanego do ukończenia operacji odbioru. Ta wartość powinna być większa lub równa <xref:System.TimeSpan.Zero> . Wartość domyślna to 00:10:00.|  
|`sendTimeout`|<xref:System.TimeSpan>Wartość określająca interwał czasu podanego do ukończenia operacji wysyłania. Ta wartość powinna być większa lub równa <xref:System.TimeSpan.Zero> . Wartość domyślna to 00:01:00.|  
|`textEncoding`|Ustawia kodowanie zestawu znaków, który ma być używany do emitowania komunikatów w powiązaniu. Prawidłowe wartości to:<br /><br /> -BigEndianUnicode: kodowanie Unicode BigEndian.<br />-Unicode: kodowanie 16-bitowe.<br />-UTF8: kodowanie 8-bitowe<br /><br /> Wartość domyślna to UTF8. Ten atrybut jest typu <xref:System.Text.Encoding> .|  
|`transferMode`|Prawidłowa wartość określająca <xref:System.ServiceModel.TransferMode> , czy komunikaty są buforowane, czy przesyłane strumieniowo na żądanie lub odpowiedź.|  
|`useDefaultWebProxy`|Wartość logiczna określająca, czy ma być używany autokonfigurowany serwer proxy HTTP systemu, jeśli jest dostępny. Wartość domyślna to `true`.|  
|||  
  
### <a name="child-elements"></a>Elementy podrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|[\<security>](security-of-basichttpbinding.md)|Definiuje ustawienia zabezpieczeń dla powiązania. Ten element jest typu <xref:System.ServiceModel.Configuration.BasicHttpSecurityElement> .|  
|[\<readerQuotas>](/previous-versions/dotnet/netframework-4.0/ms731325(v=vs.100))|Definiuje ograniczenia złożoności komunikatów protokołu SOAP, które mogą być przetwarzane przez punkty końcowe skonfigurowane za pomocą tego powiązania. Ten element jest typu <xref:System.ServiceModel.Configuration.XmlDictionaryReaderQuotasElement> .|  
  
### <a name="parent-elements"></a>Elementy nadrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|[\<bindings>](bindings.md)|Ten element zawiera kolekcję powiązań standardowych i niestandardowych.|  
  
## <a name="remarks"></a>Uwagi  
 Protokół HttpBinding używa protokołu HTTP jako transportu do wysyłania wiadomości. W przypadku użycia z umową dupleksową będą używane gniazda sieci Web.  W przypadku użycia z kontraktem typu żądanie-odpowiedź element HttpBinding będzie zachowywać się jak BasicHttpBinding z koderem binarnym.  
  
 Zabezpieczenia są domyślnie wyłączone, ale można je dodać, ustawiając atrybut mode [\<security>](security-of-basichttpbinding.md) elementu podrzędnego na wartość inną niż `None` . Domyślnie używa kodowania tekstu "text" i kodowania tekstu UTF-8.  
  
## <a name="example"></a>Przykład  
 Poniższy przykład ilustruje użycie programu <xref:System.ServiceModel.NetHttpBinding> , który zapewnia komunikację HTTP i maksymalną współdziałanie z usługami sieci Web pierwszej i drugiej generacji. Powiązanie jest określone w plikach konfiguracji klienta i usługi. Typ powiązania jest określany przy użyciu `binding` atrybutu `<endpoint>` elementu. Jeśli chcesz skonfigurować powiązanie podstawowe i zmienić niektóre z jego ustawień, musisz zdefiniować konfigurację powiązania. Punkt końcowy musi odwoływać się do konfiguracji powiązania przez nazwę przy użyciu `bindingConfiguration` atrybutu `<endpoint>` elementu, jak pokazano w poniższym kodzie konfiguracji usługi.  
  
```xml  
<system.serviceModel>
  <services>
    <service type="Microsoft.ServiceModel.Samples.CalculatorService"
             behaviorConfiguration="CalculatorServiceBehavior">
      <endpoint address=""
                binding="netHttpBinding"
                bindingConfiguration="Binding1"
                contract="Microsoft.ServiceModel.Samples.ICalculator" />
    </service>
  </services>
  <bindings>
    <netHttpBinding>
      <binding name="Binding1"
               hostNameComparisonMode="StrongWildcard"
               receiveTimeout="00:10:00"
               sendTimeout="00:10:00"
               openTimeout="00:10:00"
               closeTimeout="00:10:00"
               maxReceivedMessageSize="65536"
               maxBufferSize="65536"
               maxBufferPoolSize="524288"
               transferMode="Buffered"
               messageEncoding="Binary"
               textEncoding="utf-8"
               bypassProxyOnLocal="false"
               useDefaultWebProxy="true">
        <security mode="None" />
      </binding>
    </netHttpBinding>
  </bindings>
</system.serviceModel>
```  
  
## <a name="example"></a>Przykład  
 Począwszy od .NET Framework 4, powiązania i zachowania nie muszą mieć nazwy. Funkcję z poprzedniego przykładu można osiągnąć, usuwając bindingConfiguration z adresu punktu końcowego i nazwę z powiązania.  
  
```xml  
<system.serviceModel>
  <services>
    <service type="Microsoft.ServiceModel.Samples.CalculatorService"
             behaviorConfiguration="CalculatorServiceBehavior">
      <endpoint address=""
                binding="netHttpBinding"
                contract="Microsoft.ServiceModel.Samples.ICalculator" />
    </service>
  </services>
  <bindings>
    <netHttpBinding>
      <binding hostNameComparisonMode="StrongWildcard"
               receiveTimeout="00:10:00"
               sendTimeout="00:10:00"
               openTimeout="00:10:00"
               closeTimeout="00:10:00"
               maxReceivedMessageSize="65536"
               maxBufferSize="65536"
               maxBufferPoolSize="524288"
               transferMode="Buffered"
               messageEncoding="Binary"
               textEncoding="utf-8"
               bypassProxyOnLocal="false"
               useDefaultWebProxy="true">
        <security mode="None" />
      </binding>
    </netHttpBinding>
  </bindings>
</system.serviceModel>
```  
  
 Aby uzyskać więcej informacji na temat konfiguracji domyślnej i powiązań pustego i zachowań, zobacz [Uproszczona konfiguracja](../../../wcf/simplified-configuration.md) i [Uproszczona konfiguracja dla usług WCF](../../../wcf/samples/simplified-configuration-for-wcf-services.md).  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.ServiceModel.Channels.Binding>
- <xref:System.ServiceModel.Channels.BindingElement>
- <xref:System.ServiceModel.BasicHttpBinding>
- <xref:System.ServiceModel.Configuration.BasicHttpBindingElement>
- [Powiązania](../../../wcf/bindings.md)
- [Konfigurowanie powiązań dostarczanych przez system](../../../wcf/feature-details/configuring-system-provided-bindings.md)
- [Konfigurowanie usług i klientów za pomocą wiązań](../../../wcf/using-bindings-to-configure-services-and-clients.md)
- [\<binding>](bindings.md)
