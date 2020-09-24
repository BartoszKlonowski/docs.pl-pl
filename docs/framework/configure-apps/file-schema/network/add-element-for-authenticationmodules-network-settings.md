---
title: <add>, element dla authenticationModules (ustawienia sieci)
description: <add>Element ustawienia sieci dla connectionManagement dodaje adres IP lub nazwę DNS do listy zarządzania połączeniami w .NET Framework.
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#add
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/authenticationModules/add
helpviewer_keywords:
- authenticationModules, add element
- add element, authenticationModules
- <authenticationModules>, add element
- <add> element, authenticationModules
ms.assetid: 333c5fb0-a2ab-4db8-8531-a7fe37bb9b5b
ms.openlocfilehash: f679a43ed1851e9681a2a57ca1639f8aa75aa8b3
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91149507"
---
# <a name="add-element-for-authenticationmodules-network-settings"></a><span data-ttu-id="af024-103">\<add>, element dla authenticationModules (ustawienia sieci)</span><span class="sxs-lookup"><span data-stu-id="af024-103">\<add> Element for authenticationModules (Network Settings)</span></span>

<span data-ttu-id="af024-104">Dodaje moduł uwierzytelniania do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="af024-104">Adds an authentication module to the application.</span></span>  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.net>**](system-net-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<authenticationModules>**](authenticationmodules-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<add>**

## <a name="syntax"></a><span data-ttu-id="af024-105">Składnia</span><span class="sxs-lookup"><span data-stu-id="af024-105">Syntax</span></span>  
  
```xml  
<add
  type="type_fullname, assembly_fullname"
/>  
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="af024-106">Atrybuty i elementy</span><span class="sxs-lookup"><span data-stu-id="af024-106">Attributes and Elements</span></span>  

 <span data-ttu-id="af024-107">W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.</span><span class="sxs-lookup"><span data-stu-id="af024-107">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="af024-108">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="af024-108">Attributes</span></span>  
  
|<span data-ttu-id="af024-109">**Atrybut**</span><span class="sxs-lookup"><span data-stu-id="af024-109">**Attribute**</span></span>|<span data-ttu-id="af024-110">**Opis**</span><span class="sxs-lookup"><span data-stu-id="af024-110">**Description**</span></span>|  
|-------------------|---------------------|  
|`type`|<span data-ttu-id="af024-111">W pełni kwalifikowana nazwa typu (wskazywana przez <xref:System.Type.FullName%2A> Właściwość) i nazwa zestawu (wskazywanym przez <xref:System.Reflection.Assembly.FullName%2A> Właściwość) oddzielone przecinkami.</span><span class="sxs-lookup"><span data-stu-id="af024-111">The fully qualified type name (indicated by the <xref:System.Type.FullName%2A> property) and the assembly name (indicated by the <xref:System.Reflection.Assembly.FullName%2A> property), separated by a comma.</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="af024-112">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="af024-112">Child Elements</span></span>  

 <span data-ttu-id="af024-113">Brak.</span><span class="sxs-lookup"><span data-stu-id="af024-113">None.</span></span>  
  
### <a name="parent-elements"></a><span data-ttu-id="af024-114">Elementy nadrzędne</span><span class="sxs-lookup"><span data-stu-id="af024-114">Parent Elements</span></span>  
  
|<span data-ttu-id="af024-115">**Postaci**</span><span class="sxs-lookup"><span data-stu-id="af024-115">**Element**</span></span>|<span data-ttu-id="af024-116">**Opis**</span><span class="sxs-lookup"><span data-stu-id="af024-116">**Description**</span></span>|  
|-----------------|---------------------|  
|[<span data-ttu-id="af024-117">authenticationModules</span><span class="sxs-lookup"><span data-stu-id="af024-117">authenticationModules</span></span>](authenticationmodules-element-network-settings.md)|<span data-ttu-id="af024-118">Określa moduły używane do uwierzytelniania żądań sieci.</span><span class="sxs-lookup"><span data-stu-id="af024-118">Specifies modules used to authenticate network requests.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="af024-119">Uwagi</span><span class="sxs-lookup"><span data-stu-id="af024-119">Remarks</span></span>  

 <span data-ttu-id="af024-120">`add`Element dodaje moduł uwierzytelniania na końcu listy zarejestrowanych modułów uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="af024-120">The `add` element adds an authentication module to the end of the list of registered authentication modules.</span></span> <span data-ttu-id="af024-121">Moduły uwierzytelniania są wywoływane w kolejności, w jakiej zostały dodane do listy.</span><span class="sxs-lookup"><span data-stu-id="af024-121">Authentication modules are called in the order in which they were added to the list.</span></span>  
  
 <span data-ttu-id="af024-122">Wartość `type` atrybutu powinna być prawidłową nazwą typu i odpowiadającą jej nazwą zestawu, rozdzieloną przecinkami.</span><span class="sxs-lookup"><span data-stu-id="af024-122">The value for the `type` attribute should be a valid type name and corresponding assembly name, separated by a comma.</span></span>  
  
## <a name="configuration-files"></a><span data-ttu-id="af024-123">Pliki konfiguracji</span><span class="sxs-lookup"><span data-stu-id="af024-123">Configuration Files</span></span>  

 <span data-ttu-id="af024-124">Tego elementu można użyć w pliku konfiguracyjnym aplikacji lub pliku konfiguracji komputera (Machine.config).</span><span class="sxs-lookup"><span data-stu-id="af024-124">This element can be used in the application configuration file or the machine configuration file (Machine.config).</span></span>  
  
## <a name="example"></a><span data-ttu-id="af024-125">Przykład</span><span class="sxs-lookup"><span data-stu-id="af024-125">Example</span></span>  

 <span data-ttu-id="af024-126">W poniższym przykładzie są włączane domyślne moduły uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="af024-126">The following example enables the default authentication modules.</span></span> <span data-ttu-id="af024-127">Należy zastąpić wartości wersji i PublicKeyToken wartościami prawidłowymi dla określonego modułu.</span><span class="sxs-lookup"><span data-stu-id="af024-127">You should replace the values for Version and PublicKeyToken with the correct values for the specified module.</span></span>  
  
```xml  
<configuration>  
  <system.net>  
        <authenticationModules>  
            <add type="System.Net.DigestClient, System, Version=2.0.3600.0,  
                 Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
            <add type="System.Net.NegotiateClient, System, Version=2.0.3600.0,  
                 Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
            <add type="System.Net.KerberosClient, System, Version=2.0.3600.0,  
                 Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
            <add type="System.Net.NtlmClient, System, Version=2.0.3600.0,  
                 Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
            <add type="System.Net.BasicClient, System, Version=2.0.3600.0,  
                 Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
        </authenticationModules>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a><span data-ttu-id="af024-128">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="af024-128">See also</span></span>

- <xref:System.Net.IAuthenticationModule>
- <xref:System.Net.AuthenticationManager>
- [<span data-ttu-id="af024-129">Schemat ustawień sieciowych</span><span class="sxs-lookup"><span data-stu-id="af024-129">Network Settings Schema</span></span>](index.md)
