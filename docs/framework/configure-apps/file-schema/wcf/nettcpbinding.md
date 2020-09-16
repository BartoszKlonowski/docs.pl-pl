---
title: <netTcpBinding>
description: Reprezentuje bezpieczne, niezawodne i zoptymalizowane powiązanie przeznaczone tylko dla komunikacji między komputerami WCF przy użyciu protokołu TCP. Niezawodna obsługa komunikatów jest domyślnie wyłączona.
ms.date: 03/30/2017
helpviewer_keywords:
- netTcpBinding Element
ms.assetid: 5c5104a7-8754-4335-8233-46a45322503e
ms.openlocfilehash: a366b26d87c8796822e4fbbb2001823c116f2629
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90556131"
---
# \<netTcpBinding>

<span data-ttu-id="ea51d-103">Określa bezpieczne, niezawodne i zoptymalizowane powiązanie odpowiednie dla komunikacji między komputerami.</span><span class="sxs-lookup"><span data-stu-id="ea51d-103">Specifies a secure, reliable, optimized binding suitable for cross-machine communication.</span></span> <span data-ttu-id="ea51d-104">Domyślnie generuje stos komunikacji środowiska uruchomieniowego z zabezpieczeniami systemu Windows w celu zabezpieczenia i uwierzytelniania komunikatów, protokołu TCP na potrzeby dostarczania komunikatów i kodowania komunikatów binarnych.</span><span class="sxs-lookup"><span data-stu-id="ea51d-104">By default, it generates a runtime communication stack with Windows Security for message security and authentication, TCP for message delivery, and binary message encoding.</span></span>

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<bindings>**](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<netTcpBinding>**  
  
## <a name="syntax"></a><span data-ttu-id="ea51d-105">Składnia</span><span class="sxs-lookup"><span data-stu-id="ea51d-105">Syntax</span></span>  
  
```xml  
<netTcpBinding>
  <binding closeTimeout="TimeSpan"
           hostNameComparisonMode="StrongWildCard/Exact/WeakWildcard"
           listenBacklog="Integer"
           maxBufferPoolSize="integer"
           maxBufferSize="Integer"
           maxConnections="Integer"
           maxReceivedMessageSize="Integer"
           name="string"
           openTimeout="TimeSpan"
           portSharingEnabled="Boolean"
           receiveTimeout="TimeSpan"
           sendTimeout="TimeSpan"
           transactionFlow="Boolean"
           transactionProtocol="OleTransactions/WSAtomicTransactionOctober2004"
           transferMode="Buffered/Streamed/StreamedRequest/StreamedResponse">
    <reliableSession ordered="Boolean"
                     inactivityTimeout="TimeSpan"
                     enabled="Boolean" />
    <security mode="None/Transport/Message/Both">
      <message clientCredentialType="None/Windows/UserName/Certificate/CardSpace"
               algorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15" />
      <transport clientCredentialType="None/Windows/Certificate"
                 protectionLevel="None/Sign/EncryptAndSign" />
    </security>
    <readerQuotas maxArrayLength="Integer"
                  maxBytesPerRead="Integer"
                  maxDepth="Integer"
                  maxNameTableCharCount="Integer"
                  maxStringContentLength="Integer" />
  </binding>
</netTcpBinding>
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="ea51d-106">Atrybuty i elementy</span><span class="sxs-lookup"><span data-stu-id="ea51d-106">Attributes and elements</span></span>

<span data-ttu-id="ea51d-107">W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.</span><span class="sxs-lookup"><span data-stu-id="ea51d-107">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="ea51d-108">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="ea51d-108">Attributes</span></span>  
  
|<span data-ttu-id="ea51d-109">Atrybut</span><span class="sxs-lookup"><span data-stu-id="ea51d-109">Attribute</span></span>|<span data-ttu-id="ea51d-110">Opis</span><span class="sxs-lookup"><span data-stu-id="ea51d-110">Description</span></span>|  
|---------------|-----------------|  
|`closeTimeout`|<span data-ttu-id="ea51d-111"><xref:System.TimeSpan>Wartość określająca interwał czasu podanego do ukończenia operacji zamknięcia.</span><span class="sxs-lookup"><span data-stu-id="ea51d-111">A <xref:System.TimeSpan> value that specifies the interval of time provided for a close operation to complete.</span></span> <span data-ttu-id="ea51d-112">Ta wartość powinna być większa lub równa <xref:System.TimeSpan.Zero> .</span><span class="sxs-lookup"><span data-stu-id="ea51d-112">This value should be greater than or equal to <xref:System.TimeSpan.Zero>.</span></span> <span data-ttu-id="ea51d-113">Wartość domyślna to 00:01:00.</span><span class="sxs-lookup"><span data-stu-id="ea51d-113">The default is 00:01:00.</span></span>|  
|`hostNameComparisonMode`|<span data-ttu-id="ea51d-114">Określa tryb porównania nazw hostów HTTP używany do analizowania identyfikatorów URI.</span><span class="sxs-lookup"><span data-stu-id="ea51d-114">Specifies the HTTP hostname comparison mode used to parse URIs.</span></span> <span data-ttu-id="ea51d-115">Ten atrybut jest typu <xref:System.ServiceModel.HostNameComparisonMode> , który wskazuje, czy nazwa hosta jest używana do uzyskiwania dostępu do usługi podczas dopasowywania identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="ea51d-115">This attribute is of type <xref:System.ServiceModel.HostNameComparisonMode>, which indicates whether the hostname is used to reach the service when matching on the URI.</span></span> <span data-ttu-id="ea51d-116">Wartość domyślna to <xref:System.ServiceModel.HostNameComparisonMode.StrongWildcard> , co powoduje ignorowanie nazwy hosta w dopasowaniu.</span><span class="sxs-lookup"><span data-stu-id="ea51d-116">The default value is <xref:System.ServiceModel.HostNameComparisonMode.StrongWildcard>, which ignores the hostname in the match.</span></span>|  
|`listenBacklog`|<span data-ttu-id="ea51d-117">Dodatnia liczba całkowita, która określa maksymalną liczbę kanałów oczekujących na akceptację odbiornika.</span><span class="sxs-lookup"><span data-stu-id="ea51d-117">A positive integer that specifies the maximum number of channels waiting to be accepted on the listener.</span></span> <span data-ttu-id="ea51d-118">Połączenia o przekroczeniu tego limitu są umieszczane w kolejce do momentu udostępnienia przestrzeni poniżej limitu.</span><span class="sxs-lookup"><span data-stu-id="ea51d-118">Connections in excess of this limit are queued until space below the limit becomes available.</span></span> <span data-ttu-id="ea51d-119">`connectionTimeout`Atrybut ogranicza czas, przez który klient będzie oczekiwał na połączenie przed wygenerowaniem wyjątku połączenia.</span><span class="sxs-lookup"><span data-stu-id="ea51d-119">The `connectionTimeout` attribute limits the time a client will wait to be connected before throwing a connection exception.</span></span> <span data-ttu-id="ea51d-120">Wartość domyślna to 10.</span><span class="sxs-lookup"><span data-stu-id="ea51d-120">The default is 10.</span></span>|  
|`maxBufferPoolSize`|<span data-ttu-id="ea51d-121">Liczba całkowita określająca maksymalny rozmiar puli buforów dla tego powiązania.</span><span class="sxs-lookup"><span data-stu-id="ea51d-121">An integer that specifies the maximum buffer pool size for this binding.</span></span> <span data-ttu-id="ea51d-122">Wartość domyślna to 512 \* 1024 bajtów.</span><span class="sxs-lookup"><span data-stu-id="ea51d-122">The default is 512 \* 1024 bytes.</span></span> <span data-ttu-id="ea51d-123">Wiele części Windows Communication Foundation (WCF) używa buforów.</span><span class="sxs-lookup"><span data-stu-id="ea51d-123">Many parts of Windows Communication Foundation (WCF) use buffers.</span></span> <span data-ttu-id="ea51d-124">Tworzenie i niszczenie buforów za każdym razem, gdy są używane, jest kosztowne i wyrzucanie elementów bezużytecznych dla buforów jest również kosztowne.</span><span class="sxs-lookup"><span data-stu-id="ea51d-124">Creating and destroying buffers each time they are used is expensive, and garbage collection for buffers is also expensive.</span></span> <span data-ttu-id="ea51d-125">W przypadku pul buforów można pobrać bufor z puli, użyć go i zwrócić do puli po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="ea51d-125">With buffer pools, you can take a buffer from the pool, use it, and return it to the pool once you are done.</span></span> <span data-ttu-id="ea51d-126">W ten sposób nie ma konieczności narzutu na tworzenie i niszczenie buforów.</span><span class="sxs-lookup"><span data-stu-id="ea51d-126">Thus the overhead in creating and destroying buffers is avoided.</span></span>|  
|`maxBufferSize`|<span data-ttu-id="ea51d-127">Dodatnia liczba całkowita, która określa maksymalny rozmiar buforu używany do przechowywania komunikatów w pamięci.</span><span class="sxs-lookup"><span data-stu-id="ea51d-127">A positive integer that specifies the maximum size, in bytes, of the buffer used to store messages in memory.</span></span><br /><br /> <span data-ttu-id="ea51d-128">Jeśli `transferMode` atrybut jest równy `Buffered` , ten atrybut powinien być równy `maxReceivedMessageSize` wartości atrybutu.</span><span class="sxs-lookup"><span data-stu-id="ea51d-128">If the `transferMode` attribute equals to `Buffered`, this attribute should be equal to the `maxReceivedMessageSize` attribute value.</span></span><br /><br /> <span data-ttu-id="ea51d-129">Jeśli `transferMode` atrybut jest równy `Streamed` , ten atrybut nie może być większy niż `maxReceivedMessageSize` wartość atrybutu i powinien mieć co najmniej rozmiar nagłówków.</span><span class="sxs-lookup"><span data-stu-id="ea51d-129">If the `transferMode` attribute equals to `Streamed`, this attribute cannot be more than the `maxReceivedMessageSize` attribute value, and should be at least the size of the headers.</span></span><br /><br /> <span data-ttu-id="ea51d-130">Wartość domyślna to 65536.</span><span class="sxs-lookup"><span data-stu-id="ea51d-130">The default is 65536.</span></span> <span data-ttu-id="ea51d-131">Aby uzyskać więcej informacji, zobacz <xref:System.ServiceModel.Configuration.NetNamedPipeBindingElement.MaxBufferSize%2A>.</span><span class="sxs-lookup"><span data-stu-id="ea51d-131">For more information, see <xref:System.ServiceModel.Configuration.NetNamedPipeBindingElement.MaxBufferSize%2A>.</span></span>|  
|`maxConnections`|<span data-ttu-id="ea51d-132">Liczba całkowita określająca maksymalną liczbę połączeń wychodzących i przychodzących, które usługa zostanie utworzona/zaakceptowana.</span><span class="sxs-lookup"><span data-stu-id="ea51d-132">An integer that specifies the maximum number of outbound and inbound connections the service will create/accept.</span></span> <span data-ttu-id="ea51d-133">Połączenia przychodzące i wychodzące są liczone względem oddzielnego limitu określonego przez ten atrybut.</span><span class="sxs-lookup"><span data-stu-id="ea51d-133">Incoming and outgoing connections are counted against a separate limit specified by this attribute.</span></span><br /><br /> <span data-ttu-id="ea51d-134">Połączenia przychodzące przekraczające limit są umieszczane w kolejce do momentu udostępnienia odstępu poniżej limitu.</span><span class="sxs-lookup"><span data-stu-id="ea51d-134">Inbound connections in excess of the limit are queued until a space below the limit becomes available.</span></span><br /><br /> <span data-ttu-id="ea51d-135">Połączenia wychodzące przekraczające limit są umieszczane w kolejce do momentu udostępnienia odstępu poniżej limitu.</span><span class="sxs-lookup"><span data-stu-id="ea51d-135">Outbound connections in excess of the limit are queued until a space below the limit becomes available.</span></span><br /><br /> <span data-ttu-id="ea51d-136">Wartość domyślna to 10.</span><span class="sxs-lookup"><span data-stu-id="ea51d-136">The default is 10.</span></span>|  
|`maxReceivedMessageSize`|<span data-ttu-id="ea51d-137">Dodatnia liczba całkowita, która określa maksymalny rozmiar wiadomości (w bajtach), w tym nagłówki, które można odbierać w kanale skonfigurowanym dla tego powiązania.</span><span class="sxs-lookup"><span data-stu-id="ea51d-137">A positive integer that specifies the maximum message size, in bytes, including headers, that can be received on a channel configured with this binding.</span></span> <span data-ttu-id="ea51d-138">Nadawca komunikatu przekraczającego ten limit otrzyma błąd protokołu SOAP.</span><span class="sxs-lookup"><span data-stu-id="ea51d-138">The sender of a message exceeding this limit will receive a SOAP fault.</span></span> <span data-ttu-id="ea51d-139">Odbiorca odrzuca komunikat i tworzy wpis zdarzenia w dzienniku śledzenia.</span><span class="sxs-lookup"><span data-stu-id="ea51d-139">The receiver drops the message and creates an entry of the event in the trace log.</span></span> <span data-ttu-id="ea51d-140">Wartość domyślna to 65536.</span><span class="sxs-lookup"><span data-stu-id="ea51d-140">The default is 65536.</span></span>|  
|`name`|<span data-ttu-id="ea51d-141">Ciąg zawierający nazwę konfiguracji powiązania.</span><span class="sxs-lookup"><span data-stu-id="ea51d-141">A string that contains the configuration name of the binding.</span></span> <span data-ttu-id="ea51d-142">Ta wartość powinna być unikatowa, ponieważ jest używana jako identyfikacja dla powiązania.</span><span class="sxs-lookup"><span data-stu-id="ea51d-142">This value should be unique because it is used as an identification for the binding.</span></span> <span data-ttu-id="ea51d-143">Począwszy od .NET Framework 4, powiązania i zachowania nie muszą mieć nazwy.</span><span class="sxs-lookup"><span data-stu-id="ea51d-143">Starting with .NET Framework 4, bindings and behaviors are not required to have a name.</span></span> <span data-ttu-id="ea51d-144">Aby uzyskać więcej informacji na temat konfiguracji domyślnej i powiązań pustego i zachowań, zobacz [Uproszczona konfiguracja](../../../wcf/simplified-configuration.md) i [Uproszczona konfiguracja dla usług WCF](../../../wcf/samples/simplified-configuration-for-wcf-services.md).</span><span class="sxs-lookup"><span data-stu-id="ea51d-144">For more information about default configuration and nameless bindings and behaviors, see [Simplified Configuration](../../../wcf/simplified-configuration.md) and [Simplified Configuration for WCF Services](../../../wcf/samples/simplified-configuration-for-wcf-services.md).</span></span>|  
|`openTimeout`|<span data-ttu-id="ea51d-145"><xref:System.TimeSpan>Wartość, która określa przedział czasu podanego na zakończenie operacji otwarcia.</span><span class="sxs-lookup"><span data-stu-id="ea51d-145">A <xref:System.TimeSpan> value that specifies the interval of time provided for an open operation to complete.</span></span> <span data-ttu-id="ea51d-146">Ta wartość powinna być większa lub równa <xref:System.TimeSpan.Zero> .</span><span class="sxs-lookup"><span data-stu-id="ea51d-146">This value should be greater than or equal to <xref:System.TimeSpan.Zero>.</span></span> <span data-ttu-id="ea51d-147">Wartość domyślna to 00:01:00.</span><span class="sxs-lookup"><span data-stu-id="ea51d-147">The default is 00:01:00.</span></span>|  
|`portSharingEnabled`|<span data-ttu-id="ea51d-148">Wartość logiczna określająca, czy włączone jest Udostępnianie portów TCP dla tego połączenia.</span><span class="sxs-lookup"><span data-stu-id="ea51d-148">A Boolean value that specifies whether TCP port sharing is enabled for this connection.</span></span> <span data-ttu-id="ea51d-149">W takim przypadku `false` każde powiązanie używa własnego portu wyłącznego.</span><span class="sxs-lookup"><span data-stu-id="ea51d-149">If this is `false`, each binding uses its own exclusive port.</span></span> <span data-ttu-id="ea51d-150">To ustawienie ma zastosowanie tylko do usług, ponieważ nie ma to znaczenia dla klientów.</span><span class="sxs-lookup"><span data-stu-id="ea51d-150">This setting is relevant only to services, because clients are not affected.</span></span>|  
|`receiveTimeout`|<span data-ttu-id="ea51d-151">Wartość określająca <xref:System.TimeSpan> interwał czasu podanego do ukończenia operacji odbioru.</span><span class="sxs-lookup"><span data-stu-id="ea51d-151">A <xref:System.TimeSpan> value that specifies the interval of time provided for a receive operation to complete.</span></span> <span data-ttu-id="ea51d-152">Ta wartość powinna być większa lub równa <xref:System.TimeSpan.Zero> .</span><span class="sxs-lookup"><span data-stu-id="ea51d-152">This value should be greater than or equal to <xref:System.TimeSpan.Zero>.</span></span> <span data-ttu-id="ea51d-153">Wartość domyślna to 00:10:00.</span><span class="sxs-lookup"><span data-stu-id="ea51d-153">The default is 00:10:00.</span></span>|  
|`sendTimeout`|<span data-ttu-id="ea51d-154"><xref:System.TimeSpan>Wartość określająca interwał czasu podanego do ukończenia operacji wysyłania.</span><span class="sxs-lookup"><span data-stu-id="ea51d-154">A <xref:System.TimeSpan> value that specifies the interval of time provided for a send operation to complete.</span></span> <span data-ttu-id="ea51d-155">Ta wartość powinna być większa lub równa <xref:System.TimeSpan.Zero> .</span><span class="sxs-lookup"><span data-stu-id="ea51d-155">This value should be greater than or equal to <xref:System.TimeSpan.Zero>.</span></span> <span data-ttu-id="ea51d-156">Wartość domyślna to 00:01:00.</span><span class="sxs-lookup"><span data-stu-id="ea51d-156">The default is 00:01:00.</span></span>|  
|`transactionFlow`|<span data-ttu-id="ea51d-157">Wartość logiczna określająca, czy powiązanie obsługuje przepływy WS-Transactions.</span><span class="sxs-lookup"><span data-stu-id="ea51d-157">A Boolean value that specifies whether the binding supports flowing WS-Transactions.</span></span> <span data-ttu-id="ea51d-158">Wartość domyślna to `false`.</span><span class="sxs-lookup"><span data-stu-id="ea51d-158">The default is `false`.</span></span>|  
|`transactionProtocol`|<span data-ttu-id="ea51d-159">Określa protokół transakcji, który ma być używany z tym powiązaniem.</span><span class="sxs-lookup"><span data-stu-id="ea51d-159">Specifies the transaction protocol to be used with this binding.</span></span> <span data-ttu-id="ea51d-160">Prawidłowe wartości to</span><span class="sxs-lookup"><span data-stu-id="ea51d-160">Valid values are</span></span><br /><br /> <span data-ttu-id="ea51d-161">-OleTransactions</span><span class="sxs-lookup"><span data-stu-id="ea51d-161">-   OleTransactions</span></span><br /><span data-ttu-id="ea51d-162">- WSAtomicTransactionOctober2004</span><span class="sxs-lookup"><span data-stu-id="ea51d-162">-   WSAtomicTransactionOctober2004</span></span><br /><br /> <span data-ttu-id="ea51d-163">Wartość domyślna to OleTransactions.</span><span class="sxs-lookup"><span data-stu-id="ea51d-163">The default is OleTransactions.</span></span> <span data-ttu-id="ea51d-164">Ten atrybut jest typu <xref:System.ServiceModel.TransactionProtocol> .</span><span class="sxs-lookup"><span data-stu-id="ea51d-164">This attribute is of type <xref:System.ServiceModel.TransactionProtocol>.</span></span>|  
|`transferMode`|<span data-ttu-id="ea51d-165">Wartość określająca <xref:System.ServiceModel.TransferMode> , czy komunikaty są buforowane, czy przesyłane strumieniowo, czy też żądanie lub odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="ea51d-165">A <xref:System.ServiceModel.TransferMode> value that specifies whether messages are buffered or streamed or a request or response.</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="ea51d-166">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="ea51d-166">Child elements</span></span>  
  
|<span data-ttu-id="ea51d-167">Element</span><span class="sxs-lookup"><span data-stu-id="ea51d-167">Element</span></span>|<span data-ttu-id="ea51d-168">Opis</span><span class="sxs-lookup"><span data-stu-id="ea51d-168">Description</span></span>|  
|-------------|-----------------|  
|[\<security>](security-of-nettcpbinding.md)|<span data-ttu-id="ea51d-169">Definiuje ustawienia zabezpieczeń dla powiązania.</span><span class="sxs-lookup"><span data-stu-id="ea51d-169">Defines the security settings for the binding.</span></span> <span data-ttu-id="ea51d-170">Ten element jest typu <xref:System.ServiceModel.Configuration.NetTcpSecurityElement> .</span><span class="sxs-lookup"><span data-stu-id="ea51d-170">This element is of type <xref:System.ServiceModel.Configuration.NetTcpSecurityElement>.</span></span>|  
|[\<readerQuotas>](/previous-versions/dotnet/netframework-4.0/ms731325(v=vs.100))|<span data-ttu-id="ea51d-171">Definiuje ograniczenia złożoności komunikatów protokołu SOAP, które mogą być przetwarzane przez punkty końcowe skonfigurowane za pomocą tego powiązania.</span><span class="sxs-lookup"><span data-stu-id="ea51d-171">Defines the constraints on the complexity of SOAP messages that can be processed by endpoints configured with this binding.</span></span> <span data-ttu-id="ea51d-172">Ten element jest typu <xref:System.ServiceModel.Configuration.XmlDictionaryReaderQuotasElement> .</span><span class="sxs-lookup"><span data-stu-id="ea51d-172">This element is of type <xref:System.ServiceModel.Configuration.XmlDictionaryReaderQuotasElement>.</span></span>|  
|[\<reliableSession>](/previous-versions/ms731375(v=vs.90))|<span data-ttu-id="ea51d-173">Określa, czy niezawodne sesje są nawiązywane między punktami końcowymi kanałów.</span><span class="sxs-lookup"><span data-stu-id="ea51d-173">Specifies if reliable sessions are established between channel endpoints.</span></span>|  
  
### <a name="parent-elements"></a><span data-ttu-id="ea51d-174">Elementy nadrzędne</span><span class="sxs-lookup"><span data-stu-id="ea51d-174">Parent elements</span></span>  
  
|<span data-ttu-id="ea51d-175">Element</span><span class="sxs-lookup"><span data-stu-id="ea51d-175">Element</span></span>|<span data-ttu-id="ea51d-176">Opis</span><span class="sxs-lookup"><span data-stu-id="ea51d-176">Description</span></span>|  
|-------------|-----------------|  
|[\<bindings>](bindings.md)|<span data-ttu-id="ea51d-177">Ten element zawiera kolekcję powiązań standardowych i niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="ea51d-177">This element holds a collection of standard and custom bindings.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="ea51d-178">Uwagi</span><span class="sxs-lookup"><span data-stu-id="ea51d-178">Remarks</span></span>

<span data-ttu-id="ea51d-179">To powiązanie generuje stos komunikacji w czasie wykonywania domyślnie, który korzysta z zabezpieczeń transportu, protokołu TCP do dostarczania komunikatów i kodowania komunikatów binarnych.</span><span class="sxs-lookup"><span data-stu-id="ea51d-179">This binding generates a run-time communication stack by default, which uses transport security, TCP for message delivery, and a binary message encoding.</span></span> <span data-ttu-id="ea51d-180">To powiązanie jest odpowiednim wyborem systemu Windows Communication Foundation (WCF) w przypadku komunikacji za pośrednictwem intranetu.</span><span class="sxs-lookup"><span data-stu-id="ea51d-180">This binding is an appropriate Windows Communication Foundation (WCF) system-provided choice for communicating over an Intranet.</span></span>  
  
 <span data-ttu-id="ea51d-181">Konfiguracja domyślna dla programu `netTcpBinding` jest szybsza niż konfiguracja podana przez `wsHttpBinding` , ale jest przeznaczona tylko do komunikacji z WCF.</span><span class="sxs-lookup"><span data-stu-id="ea51d-181">The default configuration for the `netTcpBinding` is faster than the configuration provided by the `wsHttpBinding`, but it is intended only for WCF communication.</span></span> <span data-ttu-id="ea51d-182">Zachowanie zabezpieczeń można skonfigurować przy użyciu opcjonalnego `securityMode` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="ea51d-182">The security behavior is configurable using the optional `securityMode` attribute.</span></span> <span data-ttu-id="ea51d-183">Korzystanie z protokołu WS-ReliableMessaging można skonfigurować przy użyciu opcjonalnego `reliableSessionEnabled` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="ea51d-183">The use of WS-ReliableMessaging is configurable using the optional `reliableSessionEnabled` attribute.</span></span> <span data-ttu-id="ea51d-184">Jednak niezawodna obsługa komunikatów jest domyślnie wyłączona.</span><span class="sxs-lookup"><span data-stu-id="ea51d-184">But reliable messaging is off by default.</span></span> <span data-ttu-id="ea51d-185">Ogólnie rzecz biorąc, powiązania dostarczone przez system HTTP, takie jak `wsHttpBinding` i, `basicHttpBinding` są domyślnie skonfigurowane do włączania funkcji, natomiast `netTcpBinding` powiązanie to jest domyślnie wyłączone, dzięki czemu trzeba się dowiedzieć, aby uzyskać pomoc techniczną, na przykład dla jednej ze specyfikacji WS-\*.</span><span class="sxs-lookup"><span data-stu-id="ea51d-185">More generally, the HTTP system-provided bindings such as `wsHttpBinding` and `basicHttpBinding` are configured to turn things on by default, whereas the `netTcpBinding` binding turns things off by default so that you have to opt-in to get support, for example, for one of the WS-\* specifications.</span></span> <span data-ttu-id="ea51d-186">Oznacza to, że domyślna konfiguracja protokołu TCP jest szybsza podczas wymiany komunikatów między punktami końcowymi niż te skonfigurowane dla powiązań HTTP domyślnie.</span><span class="sxs-lookup"><span data-stu-id="ea51d-186">This means that the default configuration for TCP is faster at exchanging messages between endpoints than those configured for the HTTP bindings by default.</span></span>  
  
## <a name="example"></a><span data-ttu-id="ea51d-187">Przykład</span><span class="sxs-lookup"><span data-stu-id="ea51d-187">Example</span></span>

<span data-ttu-id="ea51d-188">Powiązanie jest określone w plikach konfiguracji klienta i usługi.</span><span class="sxs-lookup"><span data-stu-id="ea51d-188">The binding is specified in the configuration files for the client and service.</span></span> <span data-ttu-id="ea51d-189">Typ powiązania jest określony w `binding` atrybucie `<endpoint>` elementu.</span><span class="sxs-lookup"><span data-stu-id="ea51d-189">The binding type is specified in the `binding` attribute of the `<endpoint>` element.</span></span> <span data-ttu-id="ea51d-190">Jeśli chcesz skonfigurować powiązanie netTcpBinding i zmienić niektóre z jego ustawień, musisz zdefiniować konfigurację powiązania.</span><span class="sxs-lookup"><span data-stu-id="ea51d-190">If you want to configure the netTcpBinding binding and change some of its settings, it is necessary to define a binding configuration.</span></span> <span data-ttu-id="ea51d-191">Punkt końcowy musi odwoływać się do konfiguracji powiązania z `bindingConfiguration` atrybutem.</span><span class="sxs-lookup"><span data-stu-id="ea51d-191">The endpoint must reference the binding configuration with a `bindingConfiguration` attribute.</span></span> <span data-ttu-id="ea51d-192">W poniższym przykładzie zdefiniowano konfigurację powiązania.</span><span class="sxs-lookup"><span data-stu-id="ea51d-192">In the following example, a binding configuration is defined.</span></span>  
  
```xml  
<services>
  <service name="Microsoft.ServiceModel.Samples.CalculatorService"
           behaviorConfiguration="CalculatorServiceBehavior">
    ...
    <endpoint address=""
              binding="netTcpBinding"
              contract="Microsoft.ServiceModel.Samples.ICalculator" />
    ...
  </service>
</services>
<bindings>
  <netTcpBinding>
    <binding closeTimeout="00:01:00"
             openTimeout="00:01:00"
             receiveTimeout="00:10:00"
             sendTimeout="00:01:00"
             transactionFlow="false"
             transferMode="Buffered"
             transactionProtocol="OleTransactions"
             hostNameComparisonMode="StrongWildcard"
             listenBacklog="10"
             maxBufferPoolSize="524288"
             maxBufferSize="65536"
             maxConnections="10"
             maxReceivedMessageSize="65536">
      <readerQuotas maxDepth="32"
                    maxStringContentLength="8192"
                    maxArrayLength="16384"
                    maxBytesPerRead="4096"
                    maxNameTableCharCount="16384" />
      <reliableSession ordered="true"
                       inactivityTimeout="00:10:00"
                       enabled="false" />
      <security mode="Transport">
        <transport clientCredentialType="Windows" protectionLevel="EncryptAndSign" />
      </security>
    </binding>
  </netTcpBinding>
</bindings>
```  
  
## <a name="see-also"></a><span data-ttu-id="ea51d-193">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="ea51d-193">See also</span></span>

- <xref:System.ServiceModel.NetTcpBinding>
- <xref:System.ServiceModel.Configuration.NetTcpBindingElement>
- [<span data-ttu-id="ea51d-194">Powiązania</span><span class="sxs-lookup"><span data-stu-id="ea51d-194">Bindings</span></span>](../../../wcf/bindings.md)
- [<span data-ttu-id="ea51d-195">Konfigurowanie powiązań dostarczanych przez system</span><span class="sxs-lookup"><span data-stu-id="ea51d-195">Configuring System-Provided Bindings</span></span>](../../../wcf/feature-details/configuring-system-provided-bindings.md)
- [<span data-ttu-id="ea51d-196">Konfigurowanie usług i klientów za pomocą wiązań</span><span class="sxs-lookup"><span data-stu-id="ea51d-196">Using Bindings to Configure Services and Clients</span></span>](../../../wcf/using-bindings-to-configure-services-and-clients.md)
- [\<binding>](bindings.md)
