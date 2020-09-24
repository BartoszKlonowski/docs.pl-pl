---
title: <bindingRedirect> Element
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/assemblyBinding/dependentAssembly/bindingRedirect
- http://schemas.microsoft.com/.NetConfiguration/v2.0#bindingRedirect
helpviewer_keywords:
- <bindingRedirect> element
- container tags, <bindingRedirect> element
- bindingRedirect element
ms.assetid: 67784ecd-9663-434e-bd6a-26975e447ac0
ms.openlocfilehash: 7667f78d2c341990585526fd153c0b230658a2ee
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91167252"
---
# <a name="bindingredirect-element"></a><span data-ttu-id="8775f-102">\<bindingRedirect> Element</span><span class="sxs-lookup"><span data-stu-id="8775f-102">\<bindingRedirect> Element</span></span>

<span data-ttu-id="8775f-103">Przekierowuje jedną wersję zestawu do innej.</span><span class="sxs-lookup"><span data-stu-id="8775f-103">Redirects one assembly version to another.</span></span>  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<runtime>**](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<assemblyBinding>**](assemblybinding-element-for-runtime.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<dependentAssembly>**](dependentassembly-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<bindingRedirect>**  
  
## <a name="syntax"></a><span data-ttu-id="8775f-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="8775f-104">Syntax</span></span>  
  
```xml  
   <bindingRedirect
oldVersion="existing assembly version"  
newVersion="new assembly version"/>  
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="8775f-105">Atrybuty i elementy</span><span class="sxs-lookup"><span data-stu-id="8775f-105">Attributes and Elements</span></span>  

 <span data-ttu-id="8775f-106">W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.</span><span class="sxs-lookup"><span data-stu-id="8775f-106">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="8775f-107">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="8775f-107">Attributes</span></span>  
  
|<span data-ttu-id="8775f-108">Atrybut</span><span class="sxs-lookup"><span data-stu-id="8775f-108">Attribute</span></span>|<span data-ttu-id="8775f-109">Opis</span><span class="sxs-lookup"><span data-stu-id="8775f-109">Description</span></span>|  
|---------------|-----------------|  
|`oldVersion`|<span data-ttu-id="8775f-110">Atrybut wymagany.</span><span class="sxs-lookup"><span data-stu-id="8775f-110">Required attribute.</span></span><br /><br /> <span data-ttu-id="8775f-111">Określa pierwotnie żądaną wersję zestawu.</span><span class="sxs-lookup"><span data-stu-id="8775f-111">Specifies the version of the assembly that was originally requested.</span></span> <span data-ttu-id="8775f-112">Format numeru wersji zestawu to *główna. pomocnicza. kompilacja. poprawka*.</span><span class="sxs-lookup"><span data-stu-id="8775f-112">The format of an assembly version number is *major.minor.build.revision*.</span></span> <span data-ttu-id="8775f-113">Prawidłowe wartości każdej części tego numeru wersji należą do zakresu od 0 do 65535.</span><span class="sxs-lookup"><span data-stu-id="8775f-113">Valid values for each part of this version number are 0 to 65535.</span></span><br /><br /> <span data-ttu-id="8775f-114">Można również określić zakres wersji w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="8775f-114">You can also specify a range of versions in the following format:</span></span><br /><br /> <span data-ttu-id="8775f-115">*n. n. n. n-n. n. n. n*</span><span class="sxs-lookup"><span data-stu-id="8775f-115">*n.n.n.n - n.n.n.n*</span></span>|  
|`newVersion`|<span data-ttu-id="8775f-116">Atrybut wymagany.</span><span class="sxs-lookup"><span data-stu-id="8775f-116">Required attribute.</span></span><br /><br /> <span data-ttu-id="8775f-117">Określa wersję zestawu do użycia zamiast pierwotnie żądanej wersji w formacie: *n. n. n. n*</span><span class="sxs-lookup"><span data-stu-id="8775f-117">Specifies the version of the assembly to use instead of the originally requested version in the format: *n.n.n.n*</span></span><br /><br /> <span data-ttu-id="8775f-118">Ta wartość może określać wcześniejszą wersję niż `oldVersion` .</span><span class="sxs-lookup"><span data-stu-id="8775f-118">This value can specify an earlier version than `oldVersion`.</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="8775f-119">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="8775f-119">Child Elements</span></span>  
  
|<span data-ttu-id="8775f-120">Element</span><span class="sxs-lookup"><span data-stu-id="8775f-120">Element</span></span>|<span data-ttu-id="8775f-121">Opis</span><span class="sxs-lookup"><span data-stu-id="8775f-121">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="8775f-122">Brak</span><span class="sxs-lookup"><span data-stu-id="8775f-122">None</span></span>||  
  
### <a name="parent-elements"></a><span data-ttu-id="8775f-123">Elementy nadrzędne</span><span class="sxs-lookup"><span data-stu-id="8775f-123">Parent Elements</span></span>  
  
|<span data-ttu-id="8775f-124">Element</span><span class="sxs-lookup"><span data-stu-id="8775f-124">Element</span></span>|<span data-ttu-id="8775f-125">Opis</span><span class="sxs-lookup"><span data-stu-id="8775f-125">Description</span></span>|  
|-------------|-----------------|  
|`assemblyBinding`|<span data-ttu-id="8775f-126">Zawiera informacje o przekierowaniu wersji zestawu i lokalizacji zestawów.</span><span class="sxs-lookup"><span data-stu-id="8775f-126">Contains information about assembly version redirection and the locations of assemblies.</span></span>|  
|`configuration`|<span data-ttu-id="8775f-127">Element główny w każdym pliku konfiguracji używanym przez środowisko uruchomieniowe języka wspólnego i aplikacje programu .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="8775f-127">The root element in every configuration file used by the common language runtime and .NET Framework applications.</span></span>|  
|`dependentAssembly`|<span data-ttu-id="8775f-128">Hermetyzuje zasady powiązań oraz lokalizację zestawu dla każdego zestawu.</span><span class="sxs-lookup"><span data-stu-id="8775f-128">Encapsulates binding policy and assembly location for each assembly.</span></span> <span data-ttu-id="8775f-129">Dla każdego zestawu należy użyć jednego elementu dependentAssembly.</span><span class="sxs-lookup"><span data-stu-id="8775f-129">Use one dependentAssembly element for each assembly.</span></span>|  
|`runtime`|<span data-ttu-id="8775f-130">Zawiera informacje dotyczące powiązania zestawu oraz wyrzucania elementów bezużytecznych.</span><span class="sxs-lookup"><span data-stu-id="8775f-130">Contains information about assembly binding and garbage collection.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="8775f-131">Uwagi</span><span class="sxs-lookup"><span data-stu-id="8775f-131">Remarks</span></span>  

 <span data-ttu-id="8775f-132">W przypadku skompilowania aplikacji programu .NET Framework z użyciem zestawu o silnej nazwie aplikacja domyślnie używa tej wersji w czasie działania, nawet jeśli jest dostępna nowa wersja.</span><span class="sxs-lookup"><span data-stu-id="8775f-132">When you build a .NET Framework application against a strong-named assembly, the application uses that version of the assembly at run time by default, even if a new version is available.</span></span> <span data-ttu-id="8775f-133">Można jednak skonfigurować aplikację do działania z użyciem nowszej wersji zestawu.</span><span class="sxs-lookup"><span data-stu-id="8775f-133">However, you can configure the application to run against a newer version of the assembly.</span></span> <span data-ttu-id="8775f-134">Aby uzyskać szczegółowe informacje dotyczące sposobu, w jaki środowisko uruchomieniowe używa tych plików do określenia wersji zestawu do użycia, zobacz [jak środowisko uruchomieniowe lokalizuje zestawy](../../../deployment/how-the-runtime-locates-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="8775f-134">For details on how the runtime uses these files to determine which assembly version to use, see [How the Runtime Locates Assemblies](../../../deployment/how-the-runtime-locates-assemblies.md).</span></span>  
  
 <span data-ttu-id="8775f-135">Można przekierować więcej niż jedną wersję zestawu, dołączając wiele `bindingRedirect` elementów w `dependentAssembly` elemencie.</span><span class="sxs-lookup"><span data-stu-id="8775f-135">You can redirect more than one assembly version by including multiple `bindingRedirect` elements in a `dependentAssembly` element.</span></span> <span data-ttu-id="8775f-136">Można również wykonać przekierowanie z nowszej wersji zestawu do starszej.</span><span class="sxs-lookup"><span data-stu-id="8775f-136">You can also redirect from a newer version to an older version of the assembly.</span></span>  
  
 <span data-ttu-id="8775f-137">Jawne przekierowanie powiązań zestawu w pliku konfiguracji aplikacji wymaga uprawnienia zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="8775f-137">Explicit assembly binding redirection in an application configuration file requires a security permission.</span></span> <span data-ttu-id="8775f-138">Dotyczy to przekierowań zestawów programu .NET Framework i zestawów firm trzecich.</span><span class="sxs-lookup"><span data-stu-id="8775f-138">This applies to redirection of .NET Framework assemblies and assemblies from third parties.</span></span> <span data-ttu-id="8775f-139">Uprawnienie jest udzielane przez ustawienie <xref:System.Security.Permissions.SecurityPermissionFlag> flagi na <xref:System.Security.Permissions.SecurityPermission> .</span><span class="sxs-lookup"><span data-stu-id="8775f-139">The permission is granted by setting the <xref:System.Security.Permissions.SecurityPermissionFlag> flag on the <xref:System.Security.Permissions.SecurityPermission>.</span></span> <span data-ttu-id="8775f-140">Aby uzyskać więcej informacji, zobacz [uprawnienia zabezpieczeń przekierowania powiązania zestawu](../../assembly-binding-redirection-security-permission.md).</span><span class="sxs-lookup"><span data-stu-id="8775f-140">For more information, see [Assembly Binding Redirection Security Permission](../../assembly-binding-redirection-security-permission.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="8775f-141">Przykład</span><span class="sxs-lookup"><span data-stu-id="8775f-141">Example</span></span>  

 <span data-ttu-id="8775f-142">W poniższym przykładzie pokazano sposób przekierowywania wersji zestawu.</span><span class="sxs-lookup"><span data-stu-id="8775f-142">The following example shows how to redirect one assembly version to another.</span></span>  
  
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
         </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a><span data-ttu-id="8775f-143">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="8775f-143">See also</span></span>

- [<span data-ttu-id="8775f-144">Schemat ustawień środowiska uruchomieniowego</span><span class="sxs-lookup"><span data-stu-id="8775f-144">Runtime Settings Schema</span></span>](index.md)
- [<span data-ttu-id="8775f-145">Schemat pliku konfiguracji</span><span class="sxs-lookup"><span data-stu-id="8775f-145">Configuration File Schema</span></span>](../index.md)
- [<span data-ttu-id="8775f-146">Przekierowywanie wersji zestawu</span><span class="sxs-lookup"><span data-stu-id="8775f-146">Redirecting Assembly Versions</span></span>](../../redirect-assembly-versions.md)
