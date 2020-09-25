---
title: <add> dla <filters>
ms.date: 03/30/2017
ms.assetid: e3bf437c-dd99-49f3-9792-9a8721e6eaad
ms.openlocfilehash: c1de0605bc8afc502a85d9b2917b975ee45a3d26
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91201658"
---
# <a name="add-of-filters"></a><span data-ttu-id="16343-102">\<add> dla \<filters></span><span class="sxs-lookup"><span data-stu-id="16343-102">\<add> of \<filters></span></span>

<span data-ttu-id="16343-103">Filtr XPath określa rodzaj wiadomości do zarejestrowania.</span><span class="sxs-lookup"><span data-stu-id="16343-103">A XPath filter that specifies the kind of message to be logged.</span></span>  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<diagnostics>**](diagnostics.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<messageLogging>**](messagelogging.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<filters>**](filters.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<add>**  
  
## <a name="syntax"></a><span data-ttu-id="16343-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="16343-104">Syntax</span></span>  
  
```xml  
<filters>
  <add filter="String" />
</filters>
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="16343-105">Atrybuty i elementy</span><span class="sxs-lookup"><span data-stu-id="16343-105">Attributes and Elements</span></span>  

 <span data-ttu-id="16343-106">W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.</span><span class="sxs-lookup"><span data-stu-id="16343-106">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="16343-107">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="16343-107">Attributes</span></span>  
  
|<span data-ttu-id="16343-108">Atrybut</span><span class="sxs-lookup"><span data-stu-id="16343-108">Attribute</span></span>|<span data-ttu-id="16343-109">Opis</span><span class="sxs-lookup"><span data-stu-id="16343-109">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="16343-110">filtr</span><span class="sxs-lookup"><span data-stu-id="16343-110">filter</span></span>|<span data-ttu-id="16343-111">Ciąg określający zapytanie na dokumencie XML zdefiniowanym przez wyrażenie XPath 1,0.</span><span class="sxs-lookup"><span data-stu-id="16343-111">A string that specifies a query on an XML document defined by an XPath 1.0 expression.</span></span> <span data-ttu-id="16343-112">Aby uzyskać więcej informacji, zobacz <xref:System.ServiceModel.Dispatcher.XPathMessageFilter>.</span><span class="sxs-lookup"><span data-stu-id="16343-112">For more information, see <xref:System.ServiceModel.Dispatcher.XPathMessageFilter>.</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="16343-113">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="16343-113">Child Elements</span></span>  

 <span data-ttu-id="16343-114">Brak.</span><span class="sxs-lookup"><span data-stu-id="16343-114">None.</span></span>  
  
### <a name="parent-elements"></a><span data-ttu-id="16343-115">Elementy nadrzędne</span><span class="sxs-lookup"><span data-stu-id="16343-115">Parent Elements</span></span>  
  
|<span data-ttu-id="16343-116">Element</span><span class="sxs-lookup"><span data-stu-id="16343-116">Element</span></span>|<span data-ttu-id="16343-117">Opis</span><span class="sxs-lookup"><span data-stu-id="16343-117">Description</span></span>|  
|-------------|-----------------|  
|[\<filters>](filters.md)|<span data-ttu-id="16343-118">Zawiera kolekcję filtrów XPath używanych do kontroli rodzaju rejestrowanych komunikatów.</span><span class="sxs-lookup"><span data-stu-id="16343-118">Contains a collection of XPath filters used to control what kind of message is logged.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="16343-119">Uwagi</span><span class="sxs-lookup"><span data-stu-id="16343-119">Remarks</span></span>  

 <span data-ttu-id="16343-120">Filtry są stosowane tylko w warstwie transportowej, określonej przez `logMessagesAtTransportLevel` is `true` .</span><span class="sxs-lookup"><span data-stu-id="16343-120">Filters are applied only at the transport layer, specified by `logMessagesAtTransportLevel` is `true`.</span></span> <span data-ttu-id="16343-121">Filtry nie wpływają na poziom usług i źle sformułowane rejestrowanie komunikatów.</span><span class="sxs-lookup"><span data-stu-id="16343-121">Service level and malformed message logging are not affected by filters.</span></span>  
  
 <span data-ttu-id="16343-122">Aby dodać filtr do kolekcji, użyj `add` słowa kluczowego.</span><span class="sxs-lookup"><span data-stu-id="16343-122">To add a filter to the collection, use the `add` keyword.</span></span> <span data-ttu-id="16343-123">Jeśli zdefiniowano co najmniej jeden filtr, rejestrowane są tylko komunikaty zgodne z co najmniej jednym filtrem.</span><span class="sxs-lookup"><span data-stu-id="16343-123">When one or more filters are defined, only messages that match at least one of the filters are logged.</span></span> <span data-ttu-id="16343-124">Jeśli żaden filtr nie jest zdefiniowany, wszystkie komunikaty są przekazywane.</span><span class="sxs-lookup"><span data-stu-id="16343-124">If no filter is defined, all messages pass through.</span></span>  
  
 <span data-ttu-id="16343-125">Filtry obsługują pełną składnię XPath i są stosowane w kolejności, w której pojawiają się w pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="16343-125">Filters support the full XPath syntax, and are applied in the order they appear in the configuration file.</span></span> <span data-ttu-id="16343-126">Składnia nieprawidłowego filtru powoduje wyjątek w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="16343-126">A syntactically incorrect filter results in a configuration exception.</span></span>  
  
 <span data-ttu-id="16343-127">Poniżej przedstawiono przykład sposobu konfigurowania filtru, który rejestruje tylko komunikaty, które mają sekcję nagłówka SOAP.</span><span class="sxs-lookup"><span data-stu-id="16343-127">The following is an example of how to configure a filter that records only messages that have a SOAP Header section.</span></span>  
  
## <a name="example"></a><span data-ttu-id="16343-128">Przykład</span><span class="sxs-lookup"><span data-stu-id="16343-128">Example</span></span>  

 <span data-ttu-id="16343-129">Poniżej przedstawiono przykład sposobu konfigurowania filtru, który rejestruje tylko komunikaty, które mają sekcję nagłówka SOAP.</span><span class="sxs-lookup"><span data-stu-id="16343-129">The following is an example of how to configure a filter that records only messages that have a SOAP Header section.</span></span>  
  
```xml  
<messageLogging logEntireMessage="true"
                logMalformedMessages="true"
                logMessagesAtServiceLevel="true"
                logMessagesAtTransportLevel="true"
                maxMessagesToLog="420">
  <filters>
    <add xmlns:soap="http://www.w3.org/2003/05/soap-envelope">
      /soap:Envelope/soap:Headers
    </add>
  </filters>
</messageLogging>
```  
  
## <a name="see-also"></a><span data-ttu-id="16343-130">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="16343-130">See also</span></span>

- <xref:System.ServiceModel.Configuration.DiagnosticSection>
- <xref:System.ServiceModel.Diagnostics>
- <xref:System.ServiceModel.Configuration.DiagnosticSection.MessageLogging%2A>
- <xref:System.ServiceModel.Configuration.MessageLoggingElement>
- <xref:System.ServiceModel.Configuration.MessageLoggingElement.Filters%2A>
- <xref:System.ServiceModel.Configuration.XPathMessageFilterElement>
- <xref:System.ServiceModel.Dispatcher.XPathMessageFilter>
- [<span data-ttu-id="16343-131">Konfigurowanie rejestrowania komunikatów</span><span class="sxs-lookup"><span data-stu-id="16343-131">Configuring Message Logging</span></span>](../../../wcf/diagnostics/configuring-message-logging.md)
- [\<messageLogging>](messagelogging.md)
