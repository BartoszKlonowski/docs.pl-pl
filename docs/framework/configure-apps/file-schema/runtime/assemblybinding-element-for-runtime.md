---
title: <assemblyBinding>, element dla <runtime>
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/assemblyBinding
helpviewer_keywords:
- <assemblyBinding> element
- assemblyBinding element
- container tags, <assemblyBinding> element
ms.assetid: 964cbb35-ab49-4498-8471-209689e5dada
ms.openlocfilehash: b6a39bcecfd2485481677496adcf026d986c283b
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91170249"
---
# <a name="assemblybinding-element-for-runtime"></a><span data-ttu-id="3d3d7-102">\<assemblyBinding>, element dla \<runtime></span><span class="sxs-lookup"><span data-stu-id="3d3d7-102">\<assemblyBinding> Element for \<runtime></span></span>

<span data-ttu-id="3d3d7-103">Zawiera informacje o przekierowaniu wersji zestawu i lokalizacji zestawów.</span><span class="sxs-lookup"><span data-stu-id="3d3d7-103">Contains information about assembly version redirection and the locations of assemblies.</span></span>  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<runtime>**](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<assemblyBinding>**  
  
## <a name="syntax"></a><span data-ttu-id="3d3d7-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="3d3d7-104">Syntax</span></span>  
  
```xml  
      <assemblyBinding
   xmlns="urn:schemas-microsoft-com:asm.v1" appliesTo="v1.0.3705">  
</assemblyBinding>  
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="3d3d7-105">Atrybuty i elementy</span><span class="sxs-lookup"><span data-stu-id="3d3d7-105">Attributes and Elements</span></span>  

 <span data-ttu-id="3d3d7-106">W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.</span><span class="sxs-lookup"><span data-stu-id="3d3d7-106">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="3d3d7-107">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="3d3d7-107">Attributes</span></span>  
  
|<span data-ttu-id="3d3d7-108">Atrybut</span><span class="sxs-lookup"><span data-stu-id="3d3d7-108">Attribute</span></span>|<span data-ttu-id="3d3d7-109">Opis</span><span class="sxs-lookup"><span data-stu-id="3d3d7-109">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="3d3d7-110">**'xmlns**</span><span class="sxs-lookup"><span data-stu-id="3d3d7-110">**xmlns**</span></span>|<span data-ttu-id="3d3d7-111">Atrybut wymagany.</span><span class="sxs-lookup"><span data-stu-id="3d3d7-111">Required attribute.</span></span><br /><br /> <span data-ttu-id="3d3d7-112">Określa przestrzeń nazw XML wymaganą dla powiązania zestawu.</span><span class="sxs-lookup"><span data-stu-id="3d3d7-112">Specifies the XML namespace required for assembly binding.</span></span> <span data-ttu-id="3d3d7-113">Użyj ciągu "urn: schematys-Microsoft-com: ASM. v1" jako wartości.</span><span class="sxs-lookup"><span data-stu-id="3d3d7-113">Use the string "urn:schemas-microsoft-com:asm.v1" as the value.</span></span>|  
|<span data-ttu-id="3d3d7-114">**Zignorowan**</span><span class="sxs-lookup"><span data-stu-id="3d3d7-114">**appliesTo**</span></span>|<span data-ttu-id="3d3d7-115">Określa wersję środowiska uruchomieniowego, do której odnosi się przekierowanie zestawu .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="3d3d7-115">Specifies the runtime version the .NET Framework assembly redirection applies to.</span></span> <span data-ttu-id="3d3d7-116">Ten opcjonalny atrybut używa numeru wersji .NET Framework, aby wskazać, której wersji dotyczy.</span><span class="sxs-lookup"><span data-stu-id="3d3d7-116">This optional attribute uses a .NET Framework version number to indicate what version it applies to.</span></span> <span data-ttu-id="3d3d7-117">Jeśli nie określono atrybutu **AppliesTo** , **\<assemblyBinding>** element ma zastosowanie do wszystkich wersji .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="3d3d7-117">If no **appliesTo** attribute is specified, the **\<assemblyBinding>** element applies to all versions of the .NET Framework.</span></span> <span data-ttu-id="3d3d7-118">Atrybut **AppliesTo** został wprowadzony w .NET Framework w wersji 1,1; jest on ignorowany przez .NET Framework w wersji 1,0.</span><span class="sxs-lookup"><span data-stu-id="3d3d7-118">The **appliesTo** attribute was introduced in .NET Framework version 1.1; it is ignored by the .NET Framework version 1.0.</span></span> <span data-ttu-id="3d3d7-119">Oznacza to, że wszystkie **\<assemblyBinding>** elementy są stosowane w przypadku używania .NET Framework w wersji 1,0, nawet jeśli określono atrybut **AppliesTo** .</span><span class="sxs-lookup"><span data-stu-id="3d3d7-119">This means that all **\<assemblyBinding>** elements are applied when using the .NET Framework version 1.0, even if an **appliesTo** attribute is specified.</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="3d3d7-120">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="3d3d7-120">Child Elements</span></span>  
  
|<span data-ttu-id="3d3d7-121">Element</span><span class="sxs-lookup"><span data-stu-id="3d3d7-121">Element</span></span>|<span data-ttu-id="3d3d7-122">Opis</span><span class="sxs-lookup"><span data-stu-id="3d3d7-122">Description</span></span>|  
|-------------|-----------------|  
|[\<dependentAssembly>](dependentassembly-element.md)|<span data-ttu-id="3d3d7-123">Hermetyzuje zasady powiązań i lokalizację zestawu.</span><span class="sxs-lookup"><span data-stu-id="3d3d7-123">Encapsulates binding policy and assembly location for an assembly.</span></span> <span data-ttu-id="3d3d7-124">Użyj jednego **\<dependentAssembly>** tagu dla każdego zestawu.</span><span class="sxs-lookup"><span data-stu-id="3d3d7-124">Use one **\<dependentAssembly>** tag for each assembly.</span></span>|  
|[\<probing>](probing-element.md)|<span data-ttu-id="3d3d7-125">Określa podkatalogi przeszukiwania środowiska uruchomieniowego języka wspólnego podczas ładowania zestawów.</span><span class="sxs-lookup"><span data-stu-id="3d3d7-125">Specifies subdirectories the common language runtime searches when loading assemblies.</span></span>|  
|[\<publisherPolicy>](publisherpolicy-element.md)|<span data-ttu-id="3d3d7-126">Określa, czy środowisko uruchomieniowe stosuje zasady wydawcy.</span><span class="sxs-lookup"><span data-stu-id="3d3d7-126">Specifies whether the runtime applies publisher policy.</span></span>|  
|[\<qualifyAssembly>](qualifyassembly-element.md)|<span data-ttu-id="3d3d7-127">Określa pełną nazwę zestawu, który ma być dynamicznie ładowany, gdy zostanie użyta nazwa częściowa.</span><span class="sxs-lookup"><span data-stu-id="3d3d7-127">Specifies the full name of the assembly that should be dynamically loaded when a partial name is used.</span></span>|  
  
### <a name="parent-elements"></a><span data-ttu-id="3d3d7-128">Elementy nadrzędne</span><span class="sxs-lookup"><span data-stu-id="3d3d7-128">Parent Elements</span></span>  
  
|<span data-ttu-id="3d3d7-129">Element</span><span class="sxs-lookup"><span data-stu-id="3d3d7-129">Element</span></span>|<span data-ttu-id="3d3d7-130">Opis</span><span class="sxs-lookup"><span data-stu-id="3d3d7-130">Description</span></span>|  
|-------------|-----------------|  
|`configuration`|<span data-ttu-id="3d3d7-131">Element główny w każdym pliku konfiguracji używanym przez środowisko uruchomieniowe języka wspólnego i aplikacje programu .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="3d3d7-131">The root element in every configuration file used by the common language runtime and .NET Framework applications.</span></span>|  
|`runtime`|<span data-ttu-id="3d3d7-132">Zawiera informacje dotyczące powiązania zestawu oraz wyrzucania elementów bezużytecznych.</span><span class="sxs-lookup"><span data-stu-id="3d3d7-132">Contains information about assembly binding and garbage collection.</span></span>|  
  
## <a name="example"></a><span data-ttu-id="3d3d7-133">Przykład</span><span class="sxs-lookup"><span data-stu-id="3d3d7-133">Example</span></span>  

 <span data-ttu-id="3d3d7-134">Poniższy przykład pokazuje, jak przekierować jedną wersję zestawu do innej i podać bazę kodu.</span><span class="sxs-lookup"><span data-stu-id="3d3d7-134">The following example shows how to redirect one assembly version to another and provide a codebase.</span></span>  
  
```xml  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <dependentAssembly>  
            <assemblyIdentity name="myAssembly"  
                              publicKeyToken="32ab4ba45e0a69a1"  
                              culture="neutral" />  
            <bindingRedirect oldVersion="1.0.0.0"  
                             newVersion="2.0.0.0"/>  
            <codeBase version="2.0.0.0"  
                      href="http://www.litwareinc.com/myAssembly.dll"/>  
         </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
 <span data-ttu-id="3d3d7-135">Poniższy przykład pokazuje, jak używać atrybutu **AppliesTo** do przekierowywania powiązań zestawu .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="3d3d7-135">The following example shows how to use the **appliesTo** attribute to redirect binding of a .NET Framework assembly.</span></span>  
  
```xml  
<runtime>  
   <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1" appliesTo="v1.0.3705">  
      <dependentAssembly>
         <assemblyIdentity name="mscorcfg" publicKeyToken="b03f5f7f11d50a3a" culture=""/>  
         <bindingRedirect oldVersion="0.0.0.0-65535.65535.65535.65535" newVersion="1.0.3300.0"/>  
      </dependentAssembly>  
   </assemblyBinding>  
</runtime>  
```  
  
## <a name="see-also"></a><span data-ttu-id="3d3d7-136">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="3d3d7-136">See also</span></span>

- [<span data-ttu-id="3d3d7-137">Schemat ustawień środowiska uruchomieniowego</span><span class="sxs-lookup"><span data-stu-id="3d3d7-137">Runtime Settings Schema</span></span>](index.md)
- [<span data-ttu-id="3d3d7-138">Schemat pliku konfiguracji</span><span class="sxs-lookup"><span data-stu-id="3d3d7-138">Configuration File Schema</span></span>](../index.md)
- [<span data-ttu-id="3d3d7-139">Przekierowywanie wersji zestawu</span><span class="sxs-lookup"><span data-stu-id="3d3d7-139">Redirecting Assembly Versions</span></span>](../../redirect-assembly-versions.md)
