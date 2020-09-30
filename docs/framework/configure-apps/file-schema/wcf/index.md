---
title: Schemat konfiguracji programu WCF
ms.date: 03/30/2017
ms.assetid: c282aeb5-91f0-4522-8e2f-704c1ef3651f
ms.openlocfilehash: 44d5e0acc6f5a9ca43949bce0c7964354ad18270
ms.sourcegitcommit: 665f8fc55258356f4d2f4a6585b750c974b26675
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/30/2020
ms.locfileid: "91573660"
---
# <a name="wcf-configuration-schema"></a><span data-ttu-id="93f64-102">Schemat konfiguracji programu WCF</span><span class="sxs-lookup"><span data-stu-id="93f64-102">WCF Configuration Schema</span></span>

<span data-ttu-id="93f64-103">Elementy konfiguracji programu Windows Communication Foundation (WCF) umożliwiają skonfigurowanie usług i aplikacji klienckich platformy WCF.</span><span class="sxs-lookup"><span data-stu-id="93f64-103">Windows Communication Foundation (WCF) configuration elements enable you to configure WCF service and client applications.</span></span> <span data-ttu-id="93f64-104">Za pomocą [Narzędzia Edytora konfiguracji (SvcConfigEditor.exe)](../../../wcf/configuration-editor-tool-svcconfigeditor-exe.md) można tworzyć i modyfikować pliki konfiguracji dla klientów i usług.</span><span class="sxs-lookup"><span data-stu-id="93f64-104">You can use the [Configuration Editor Tool (SvcConfigEditor.exe)](../../../wcf/configuration-editor-tool-svcconfigeditor-exe.md) to create and modify configuration files for clients and services.</span></span> <span data-ttu-id="93f64-105">Ponieważ pliki konfiguracji są sformatowane jako XML, należy zapoznać się z kodem XML, aby ręcznie edytować je za pomocą edytora tekstu.</span><span class="sxs-lookup"><span data-stu-id="93f64-105">Since the configuration files are formatted as XML, you must be familiar with XML if you want to manually edit them using a text editor.</span></span> <span data-ttu-id="93f64-106">W przeciwnym razie może wystąpić problemy, takie jak unfound tagu elementu XML lub atrybut.</span><span class="sxs-lookup"><span data-stu-id="93f64-106">Otherwise, you may run into issues such as an unfound XML element tag or attribute.</span></span> <span data-ttu-id="93f64-107">Wynika to z tagów elementu XML i atrybutów jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="93f64-107">This is because XML element tags and attributes are case-sensitive.</span></span>  
  
 <span data-ttu-id="93f64-108">System konfiguracji WCF jest oparty na <xref:System.Configuration> przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="93f64-108">The WCF configuration system is based on the <xref:System.Configuration> namespace.</span></span> <span data-ttu-id="93f64-109">W związku z tym możesz użyć wszystkich funkcji standardowych dostępnych w <xref:System.Configuration> przestrzeni nazw, takich jak blokowanie konfiguracji, szyfrowanie i scalanie, aby zwiększyć bezpieczeństwo aplikacji i jej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="93f64-109">Therefore, you can use all the standard features provided by the <xref:System.Configuration> namespace, such as configuration locking, encryption and merging to increase the security of your application and its configuration.</span></span> <span data-ttu-id="93f64-110">Aby uzyskać więcej informacji na temat tych pojęć, zobacz następujące tematy.</span><span class="sxs-lookup"><span data-stu-id="93f64-110">For more information on these concepts, see the following topics.</span></span>  
  
 <span data-ttu-id="93f64-111">[Szyfrowanie informacji o konfiguracji](/previous-versions/aspnet/53tyfkaw(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="93f64-111">[Encrypting Configuration Information](/previous-versions/aspnet/53tyfkaw(v=vs.100))</span></span>  
  
 <span data-ttu-id="93f64-112">[Blokowanie ustawień konfiguracji](/previous-versions/aspnet/55th21y4(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="93f64-112">[Locking Configuration Settings](/previous-versions/aspnet/55th21y4(v=vs.100))</span></span>  
  
 <span data-ttu-id="93f64-113">W tej sekcji opisano wszystkie możliwe wartości poszczególnych elementów konfiguracji oraz sposób współdziałania z innymi elementami konfiguracji WCF.</span><span class="sxs-lookup"><span data-stu-id="93f64-113">This section describes all possible values of each configuration item, and how it interacts with other WCF configuration elements.</span></span> <span data-ttu-id="93f64-114">Poniższa mapa ilustruje Schemat konfiguracji programu WCF:</span><span class="sxs-lookup"><span data-stu-id="93f64-114">The following map illustrates the WCF configuration schema:</span></span>

:::image type="content" source="./media/index/windows-communication-foundation-configuration-schema.gif" alt-text="Diagram przedstawiający Schemat konfiguracji programu WCF." lightbox="./media/index/windows-communication-foundation-configuration-schema.gif":::
  
> [!CAUTION]
> <span data-ttu-id="93f64-116">Aby zapobiec potencjalnym zagrożeniom bezpieczeństwa, należy chronić sekcje konfiguracyjne programu WCF w plikach konfiguracyjnych aplikacji (app.config) z odpowiednimi listami Access Control.</span><span class="sxs-lookup"><span data-stu-id="93f64-116">Protect WCF configuration sections in your application configuration files (app.config) with appropriate Access Control Lists (ACL) to prevent any potential security threats.</span></span> <span data-ttu-id="93f64-117">Należy na przykład upewnić się, że tylko odpowiednie osoby mogą uzyskać dostęp do ustawień zabezpieczeń dla powiązań aplikacji lub zmodyfikować je w sekcji model usługi w pliku konfiguracji usługi.</span><span class="sxs-lookup"><span data-stu-id="93f64-117">For example, make sure that only the appropriate people can access or modify the security settings on application bindings, or the service model section of the configuration file for a service.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="93f64-118">W tej sekcji</span><span class="sxs-lookup"><span data-stu-id="93f64-118">In This Section</span></span>  

 [\<system.serviceModel>](system-servicemodel.md)  
 <span data-ttu-id="93f64-119">Opisuje `ServiceModel` elementu.</span><span class="sxs-lookup"><span data-stu-id="93f64-119">Describes the `ServiceModel` element.</span></span>  
  
 [\<system.serviceModel.activation>](system-servicemodel-activation.md)  
 <span data-ttu-id="93f64-120">Konfiguruje narzędzie SMSvcHost.exe.</span><span class="sxs-lookup"><span data-stu-id="93f64-120">Configures the SMSvcHost.exe tool.</span></span>  
  
 [\<system.runtime.serialization>](system-runtime-serialization.md)  
 <span data-ttu-id="93f64-121">Element najwyższego poziomu służący do ustawiania opcji przy użyciu serializatorów, takich jak <xref:System.Runtime.Serialization.DataContractSerializer> .</span><span class="sxs-lookup"><span data-stu-id="93f64-121">The top-level element for setting options when using serializers such as the <xref:System.Runtime.Serialization.DataContractSerializer>.</span></span>  
  
## <a name="related-sections"></a><span data-ttu-id="93f64-122">Sekcje pokrewne</span><span class="sxs-lookup"><span data-stu-id="93f64-122">Related Sections</span></span>  

 [<span data-ttu-id="93f64-123">Konfigurowanie aplikacji Windows Communication Foundation</span><span class="sxs-lookup"><span data-stu-id="93f64-123">Configuring Windows Communication Foundation Applications</span></span>](../../../wcf/configuring-services.md)  
 <span data-ttu-id="93f64-124">Opisuje sposób konfigurowania usług i klientów programu WCF.</span><span class="sxs-lookup"><span data-stu-id="93f64-124">Describes how to configure WCF services and clients.</span></span>
