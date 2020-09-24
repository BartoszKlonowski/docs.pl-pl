---
title: <roleClaimType>
ms.date: 03/30/2017
ms.assetid: 69a49deb-6369-41ba-806b-ae8d21fac64b
author: BrucePerlerMS
ms.openlocfilehash: 36d727f97597df816779da1c1f7ed5da1a1697f2
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91164938"
---
# \<roleClaimType>

<span data-ttu-id="64caa-101">Określa typ oświadczenia, który definiuje oświadczenia typu roli w kolekcji <xref:System.Security.Claims.ClaimsIdentity> obiektów zwracanych przez <xref:System.IdentityModel.Tokens.SecurityTokenHandler.ValidateToken%2A> metodę procedury obsługi tokenu.</span><span class="sxs-lookup"><span data-stu-id="64caa-101">Specifies the claim type that defines the role type claims in the collection of <xref:System.Security.Claims.ClaimsIdentity> objects returned by the <xref:System.IdentityModel.Tokens.SecurityTokenHandler.ValidateToken%2A> method of the token handler.</span></span>  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.identityModel>**](system-identitymodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<identityConfiguration>**](identityconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<securityTokenHandlers>**](securitytokenhandlers.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<add>**](add.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<samlSecurityTokenRequirement>**](samlsecuritytokenrequirement.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<roleClaimType>**  
  
## <a name="syntax"></a><span data-ttu-id="64caa-102">Składnia</span><span class="sxs-lookup"><span data-stu-id="64caa-102">Syntax</span></span>  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <add>  
        <samlSecurityTokenRequirement>  
          <roleClaimType value=xs:string>  
          </roleClaimType>  
        </samlSecurityTokenRequirement>  
      </add>  
    </securityTokenHandlers>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="64caa-103">Atrybuty i elementy</span><span class="sxs-lookup"><span data-stu-id="64caa-103">Attributes and Elements</span></span>  

 <span data-ttu-id="64caa-104">W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.</span><span class="sxs-lookup"><span data-stu-id="64caa-104">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="64caa-105">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="64caa-105">Attributes</span></span>  
  
|<span data-ttu-id="64caa-106">Atrybut</span><span class="sxs-lookup"><span data-stu-id="64caa-106">Attribute</span></span>|<span data-ttu-id="64caa-107">Opis</span><span class="sxs-lookup"><span data-stu-id="64caa-107">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="64caa-108">wartość</span><span class="sxs-lookup"><span data-stu-id="64caa-108">value</span></span>|<span data-ttu-id="64caa-109">Ciąg określający identyfikator URI, który reprezentuje typ zgłoszenia do użycia dla typu roli.</span><span class="sxs-lookup"><span data-stu-id="64caa-109">A string that specifies the URI that represents the claim type of the claim to use for the role claim type.</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="64caa-110">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="64caa-110">Child Elements</span></span>  

 <span data-ttu-id="64caa-111">Brak</span><span class="sxs-lookup"><span data-stu-id="64caa-111">None</span></span>  
  
### <a name="parent-elements"></a><span data-ttu-id="64caa-112">Elementy nadrzędne</span><span class="sxs-lookup"><span data-stu-id="64caa-112">Parent Elements</span></span>  
  
|<span data-ttu-id="64caa-113">Element</span><span class="sxs-lookup"><span data-stu-id="64caa-113">Element</span></span>|<span data-ttu-id="64caa-114">Opis</span><span class="sxs-lookup"><span data-stu-id="64caa-114">Description</span></span>|  
|-------------|-----------------|  
|[\<samlSecurityTokenRequirement>](samlsecuritytokenrequirement.md)|<span data-ttu-id="64caa-115">Zapewnia konfigurację <xref:System.IdentityModel.Tokens.SamlSecurityTokenHandler> klasy, <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler> klasy lub klasy pochodnej jednej z tych klas.</span><span class="sxs-lookup"><span data-stu-id="64caa-115">Provides configuration for the <xref:System.IdentityModel.Tokens.SamlSecurityTokenHandler> class, the <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler> class, or a derived class of either of these classes.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="64caa-116">Uwagi</span><span class="sxs-lookup"><span data-stu-id="64caa-116">Remarks</span></span>  

 <span data-ttu-id="64caa-117">`<roleClaimType>`Element ustawia właściwość, <xref:System.IdentityModel.Tokens.SamlSecurityTokenRequirement.RoleClaimType%2A> gdy <xref:System.IdentityModel.Tokens.SamlSecurityTokenRequirement> obiekt jest inicjowany z konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="64caa-117">The `<roleClaimType>` element sets the <xref:System.IdentityModel.Tokens.SamlSecurityTokenRequirement.RoleClaimType%2A> property when a <xref:System.IdentityModel.Tokens.SamlSecurityTokenRequirement> object is initialized from configuration.</span></span>  
  
## <a name="example"></a><span data-ttu-id="64caa-118">Przykład</span><span class="sxs-lookup"><span data-stu-id="64caa-118">Example</span></span>  
  
```xml  
<add type="System.IdentityModel.Tokens.SamlSecurityTokenHandler, System.IdentityModel">  
    <samlSecurityTokenRequirement>  
        <roleClaimType value="schemas.microsoft.com/ws/2006/04/identity/claims/role" />  
    </samlSecurityTokenRequirement>  
</add>  
```  
  
## <a name="see-also"></a><span data-ttu-id="64caa-119">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="64caa-119">See also</span></span>

- <xref:System.IdentityModel.Tokens.SamlSecurityTokenRequirement.RoleClaimType%2A>
