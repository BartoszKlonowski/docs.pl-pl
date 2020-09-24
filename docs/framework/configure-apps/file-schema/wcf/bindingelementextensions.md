---
title: <bindingElementExtensions>
ms.date: 03/30/2017
ms.assetid: bb597fc0-c947-451c-afda-bf23d42f4f4d
ms.openlocfilehash: 6ba97adfa696e00b4d6b75faf104c31436e25447
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91151133"
---
# \<bindingElementExtensions>

<span data-ttu-id="9e2d9-101">Ta sekcja umożliwia korzystanie z niestandardowego elementu powiązania z pliku konfiguracji komputera lub aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9e2d9-101">This section enables the use of a custom binding element from a machine or application configuration file.</span></span> <span data-ttu-id="9e2d9-102">Można dodać niestandardowy element powiązania do tej kolekcji przy użyciu `add` słowa kluczowego i ustawić `type` atrybut elementu na rozszerzenie elementu powiązania, a także `name` atrybut elementu niestandardowego powiązania.</span><span class="sxs-lookup"><span data-stu-id="9e2d9-102">You can add a custom binding element to this collection by using the `add` keyword, and setting the `type` attribute of the element to a binding element extension, as well as the `name` attribute to the custom binding element.</span></span>  
  
 <span data-ttu-id="9e2d9-103">Rozszerzenia powiązań umożliwiają użytkownikowi tworzenie elementów powiązania zdefiniowanych przez użytkownika do użycia w ramach powiązań niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="9e2d9-103">Binding extensions enable the user to create user-defined binding elements for use as part of custom bindings.</span></span> <span data-ttu-id="9e2d9-104">Programowe rozszerzenie powiązania jest typem, który implementuje klasę abstrakcyjną <xref:System.ServiceModel.Channels.BindingElement> .</span><span class="sxs-lookup"><span data-stu-id="9e2d9-104">Programmatically, a binding extension is a type that implements the abstract class <xref:System.ServiceModel.Channels.BindingElement>.</span></span> <span data-ttu-id="9e2d9-105">W pliku konfiguracji `bindingElementExtensions` sekcja służy do definiowania elementu rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="9e2d9-105">In the configuration file, the `bindingElementExtensions` section is used to define an extension element.</span></span>  
  
 <span data-ttu-id="9e2d9-106">Poniższy przykład używa `add` elementu, a także `name` atrybutu, aby dodać rozszerzenie powiązania do `bindingElementExtensions` sekcji pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="9e2d9-106">The following example uses the `add` element, as well as the `name` attribute to add a binding extension to the `bindingElementExtensions` section of the configuration file.</span></span>  
  
```xml  
<system.serviceModel>
  <extensions>
    <bindingElementExtensions>
      <add name="udpTransport"
           type="Microsoft.ServiceModel.Samples.UdpTransportSection, UdpTransport,
                 Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
    </bindingElementExtensions>
  </extensions>
</system.serviceModel>
```  
  
 <span data-ttu-id="9e2d9-107">Aby dodać możliwości konfiguracji do elementu, użytkownik musi napisać i zarejestrować `bindingElementExtensionSection` element.</span><span class="sxs-lookup"><span data-stu-id="9e2d9-107">To add configuration abilities to the element, the user needs to write and register a `bindingElementExtensionSection` element.</span></span> <span data-ttu-id="9e2d9-108">Aby uzyskać więcej informacji na ten temat, zapoznaj się z <xref:System.Configuration> dokumentacją.</span><span class="sxs-lookup"><span data-stu-id="9e2d9-108">For more information on this, see the <xref:System.Configuration> documentation.</span></span>  
  
 <span data-ttu-id="9e2d9-109">Po zdefiniowaniu elementu i jego typu konfiguracji rozszerzenie może być używane jako część niestandardowego powiązania, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="9e2d9-109">After the element and its configuration type are defined, the extension can be used as part of a custom binding as shown in the following example.</span></span>  
  
```xml  
<customBinding>
  <binding name="test2">
    <udpTransport />
    <binaryMessageEncoding maxReadPoolSize="211"
                           maxWritePoolSize="2132"
                           maxSessionSize="3141" />
  </binding>
</customBinding>
```  
  
## <a name="see-also"></a><span data-ttu-id="9e2d9-110">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="9e2d9-110">See also</span></span>

- <xref:System.ServiceModel.Configuration.BindingElementExtensionElement>
- [<span data-ttu-id="9e2d9-111">Rozszerzanie powiązań</span><span class="sxs-lookup"><span data-stu-id="9e2d9-111">Extending Bindings</span></span>](../../../wcf/extending/extending-bindings.md)
