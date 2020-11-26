---
title: 'Instrukcje: tworzenie niestandardowej tożsamości podmiotu zabezpieczeń'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- IPrincipal
- IAuthorizationPolicy
- PrincipalPermissionMode
- PrincipalPermissionAttribute
ms.assetid: c4845fca-0ed9-4adf-bbdc-10812be69b61
ms.openlocfilehash: 6c50d6b0ac2baa2dc61431af4afb8dca3860456a
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96249309"
---
# <a name="how-to-create-a-custom-principal-identity"></a><span data-ttu-id="ed824-102">Instrukcje: tworzenie niestandardowej tożsamości podmiotu zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="ed824-102">How to: Create a Custom Principal Identity</span></span>

<span data-ttu-id="ed824-103"><xref:System.Security.Permissions.PrincipalPermissionAttribute>Jest deklaratywnym sposobem kontrolowania dostępu do metod usługi.</span><span class="sxs-lookup"><span data-stu-id="ed824-103">The <xref:System.Security.Permissions.PrincipalPermissionAttribute> is a declarative means of controlling access to service methods.</span></span> <span data-ttu-id="ed824-104">W przypadku korzystania z tego atrybutu <xref:System.ServiceModel.Description.PrincipalPermissionMode> Wyliczenie określa tryb wykonywania kontroli autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="ed824-104">When using this attribute, the <xref:System.ServiceModel.Description.PrincipalPermissionMode> enumeration specifies the mode for performing authorization checks.</span></span> <span data-ttu-id="ed824-105">Gdy ten tryb jest ustawiony na <xref:System.ServiceModel.Description.PrincipalPermissionMode.Custom> , umożliwia użytkownikowi określenie <xref:System.Security.Principal.IPrincipal> klasy niestandardowej zwracanej przez <xref:System.Threading.Thread.CurrentPrincipal%2A> Właściwość.</span><span class="sxs-lookup"><span data-stu-id="ed824-105">When this mode is set to <xref:System.ServiceModel.Description.PrincipalPermissionMode.Custom>, it enables the user to specify a custom <xref:System.Security.Principal.IPrincipal> class returned by the <xref:System.Threading.Thread.CurrentPrincipal%2A> property.</span></span> <span data-ttu-id="ed824-106">W tym temacie przedstawiono scenariusz, gdy <xref:System.ServiceModel.Description.PrincipalPermissionMode.Custom> jest używany w połączeniu z niestandardowymi zasadami autoryzacji i niestandardowym podmiotem zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="ed824-106">This topic illustrates the scenario when <xref:System.ServiceModel.Description.PrincipalPermissionMode.Custom> is used in combination with a custom authorization policy and a custom principal.</span></span>  
  
 <span data-ttu-id="ed824-107">Aby uzyskać więcej informacji o używaniu programu <xref:System.Security.Permissions.PrincipalPermissionAttribute> , zobacz [How to: ograniczanie dostępu za pomocą klasy PrincipalPermissionAttribute](../how-to-restrict-access-with-the-principalpermissionattribute-class.md).</span><span class="sxs-lookup"><span data-stu-id="ed824-107">For more information about using the <xref:System.Security.Permissions.PrincipalPermissionAttribute>, see [How to: Restrict Access with the PrincipalPermissionAttribute Class](../how-to-restrict-access-with-the-principalpermissionattribute-class.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="ed824-108">Przykład</span><span class="sxs-lookup"><span data-stu-id="ed824-108">Example</span></span>  

 [!code-csharp[PrincipalPermissionMode#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/principalpermissionmode/cs/source.cs#8)]
 [!code-vb[PrincipalPermissionMode#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/principalpermissionmode/vb/source.vb#8)]  
  
## <a name="compiling-the-code"></a><span data-ttu-id="ed824-109">Kompilowanie kodu</span><span class="sxs-lookup"><span data-stu-id="ed824-109">Compiling the Code</span></span>  

 <span data-ttu-id="ed824-110">Do kompilowania kodu są konieczne odwołania do następujących przestrzeni nazw:</span><span class="sxs-lookup"><span data-stu-id="ed824-110">References to the following namespaces are needed to compile the code:</span></span>  
  
- <xref:System>  
  
- <xref:System.Collections.Generic>  
  
- <xref:System.Security.Permissions>  
  
- <xref:System.Security.Principal>  
  
- <xref:System.Threading>  
  
- <xref:System.ServiceModel>  
  
- <xref:System.ServiceModel.Channels>  
  
- <xref:System.ServiceModel.Description>  
  
- <xref:System.IdentityModel.Claims>  
  
- <xref:System.IdentityModel.Policy>  
  
## <a name="see-also"></a><span data-ttu-id="ed824-111">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="ed824-111">See also</span></span>

- <xref:System.ServiceModel.Description.PrincipalPermissionMode>
- <xref:System.Security.Permissions.PrincipalPermissionAttribute>
- [<span data-ttu-id="ed824-112">Instrukcje: używanie dostawcy ról ASP.NET razem z usługą</span><span class="sxs-lookup"><span data-stu-id="ed824-112">How to: Use the ASP.NET Role Provider with a Service</span></span>](../feature-details/how-to-use-the-aspnet-role-provider-with-a-service.md)
- [<span data-ttu-id="ed824-113">Instrukcje: Ograniczanie dostępu przy użyciu klasy PrincipalPermissionAttribute</span><span class="sxs-lookup"><span data-stu-id="ed824-113">How to: Restrict Access with the PrincipalPermissionAttribute Class</span></span>](../how-to-restrict-access-with-the-principalpermissionattribute-class.md)
