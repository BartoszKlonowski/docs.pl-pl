---
title: <Library> — Element (.NET Native)
ms.date: 03/30/2017
ms.assetid: f642276b-33fb-4a81-b882-8808c31ba69e
ms.openlocfilehash: aeaa6b1a9c3c4ceebdd0eab3f331a044971398bf
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96287920"
---
# <a name="library-element-net-native"></a><span data-ttu-id="e79f5-102">\<Library> — Element (.NET Native)</span><span class="sxs-lookup"><span data-stu-id="e79f5-102">\<Library> Element (.NET Native)</span></span>

<span data-ttu-id="e79f5-103">Definiuje zestaw zawierający typy i elementy członkowskie typu, których metadane są dostępne do odbicia w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="e79f5-103">Defines the assembly that contains types and type members whose metadata is available for reflection at run time.</span></span>  
  
 <span data-ttu-id="e79f5-104">\<Directives> Element</span><span class="sxs-lookup"><span data-stu-id="e79f5-104">\<Directives> Element</span></span>  
<span data-ttu-id="e79f5-105">\<Library> Element</span><span class="sxs-lookup"><span data-stu-id="e79f5-105">\<Library> Element</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="e79f5-106">Składnia</span><span class="sxs-lookup"><span data-stu-id="e79f5-106">Syntax</span></span>  
  
```xml  
<Library Name="assembly_name" />  
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="e79f5-107">Atrybuty i elementy</span><span class="sxs-lookup"><span data-stu-id="e79f5-107">Attributes and Elements</span></span>  

 <span data-ttu-id="e79f5-108">W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.</span><span class="sxs-lookup"><span data-stu-id="e79f5-108">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="e79f5-109">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="e79f5-109">Attributes</span></span>  
  
|<span data-ttu-id="e79f5-110">Atrybut</span><span class="sxs-lookup"><span data-stu-id="e79f5-110">Attribute</span></span>|<span data-ttu-id="e79f5-111">Opis</span><span class="sxs-lookup"><span data-stu-id="e79f5-111">Description</span></span>|  
|---------------|-----------------|  
|`Name`|<span data-ttu-id="e79f5-112">Atrybut wymagany.</span><span class="sxs-lookup"><span data-stu-id="e79f5-112">Required attribute.</span></span> <span data-ttu-id="e79f5-113">Określa nazwę zestawu.</span><span class="sxs-lookup"><span data-stu-id="e79f5-113">Specifies the name of an assembly.</span></span> <span data-ttu-id="e79f5-114">Elementy podrzędne tego `<Library>` elementu definiują zasady odbicia środowiska uruchomieniowego dla typów i elementów członkowskich typu znalezionych w tym zestawie.</span><span class="sxs-lookup"><span data-stu-id="e79f5-114">Child elements of this `<Library>` element define the runtime reflection policy for types and type members found in this assembly.</span></span>|  
  
## <a name="name-attribute"></a><span data-ttu-id="e79f5-115">Atrybut nazwy</span><span class="sxs-lookup"><span data-stu-id="e79f5-115">Name attribute</span></span>  
  
|<span data-ttu-id="e79f5-116">Wartość</span><span class="sxs-lookup"><span data-stu-id="e79f5-116">Value</span></span>|<span data-ttu-id="e79f5-117">Opis</span><span class="sxs-lookup"><span data-stu-id="e79f5-117">Description</span></span>|  
|-----------|-----------------|  
|<span data-ttu-id="e79f5-118">*assembly_name*</span><span class="sxs-lookup"><span data-stu-id="e79f5-118">*assembly_name*</span></span>|<span data-ttu-id="e79f5-119">Prosta nazwa zestawu bez rozszerzenia pliku.</span><span class="sxs-lookup"><span data-stu-id="e79f5-119">The simple name of the assembly, without its file extension.</span></span> <span data-ttu-id="e79f5-120">Ten atrybut odpowiada <xref:System.Reflection.AssemblyName.Name%2A?displayProperty=nameWithType> właściwości.</span><span class="sxs-lookup"><span data-stu-id="e79f5-120">This attribute corresponds to the <xref:System.Reflection.AssemblyName.Name%2A?displayProperty=nameWithType> property.</span></span> <span data-ttu-id="e79f5-121">Na przykład nazwa zestawu o nazwie Extensions.dll to "Extensions".</span><span class="sxs-lookup"><span data-stu-id="e79f5-121">For example, the name of an assembly named Extensions.dll is "Extensions".</span></span> <span data-ttu-id="e79f5-122">Zobacz sekcję Uwagi, aby uzyskać specjalną formę *assembly_name* , która obsługuje warunkowe dołączanie metadanych z zestawu.</span><span class="sxs-lookup"><span data-stu-id="e79f5-122">See the Remarks section for a special form of *assembly_name* that supports conditional inclusion of metadata from the assembly.</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="e79f5-123">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="e79f5-123">Child Elements</span></span>  
  
|<span data-ttu-id="e79f5-124">Element</span><span class="sxs-lookup"><span data-stu-id="e79f5-124">Element</span></span>|<span data-ttu-id="e79f5-125">Opis</span><span class="sxs-lookup"><span data-stu-id="e79f5-125">Description</span></span>|  
|-------------|-----------------|  
|[\<Assembly>](assembly-element-net-native.md)|<span data-ttu-id="e79f5-126">Stosuje zasady do wszystkich typów w określonym zestawie.</span><span class="sxs-lookup"><span data-stu-id="e79f5-126">Applies policy to all the types in a particular assembly.</span></span>|  
|[\<Namespace>](namespace-element-net-native.md)|<span data-ttu-id="e79f5-127">Stosuje zasady do wszystkich typów w konkretnym obszarze nazw.</span><span class="sxs-lookup"><span data-stu-id="e79f5-127">Applies policy to all the types in a particular namespace.</span></span>|  
|[\<Type>](type-element-net-native.md)|<span data-ttu-id="e79f5-128">Stosuje zasady do określonego typu, na przykład klasy lub struktury.</span><span class="sxs-lookup"><span data-stu-id="e79f5-128">Applies policy to a particular type, such as a class or structure.</span></span>|  
|[\<TypeInstantiation>](typeinstantiation-element-net-native.md)|<span data-ttu-id="e79f5-129">Stosuje zasady do skonstruowanego typu ogólnego.</span><span class="sxs-lookup"><span data-stu-id="e79f5-129">Applies policy to a constructed generic type.</span></span> <span data-ttu-id="e79f5-130">Na przykład [\<TypeInstantiation>](typeinstantiation-element-net-native.md) element może służyć do definiowania zasad dla `List<String>` typu.</span><span class="sxs-lookup"><span data-stu-id="e79f5-130">For example, a [\<TypeInstantiation>](typeinstantiation-element-net-native.md) element could be used to define policy for a `List<String>` type.</span></span>|  
  
### <a name="parent-elements"></a><span data-ttu-id="e79f5-131">Elementy nadrzędne</span><span class="sxs-lookup"><span data-stu-id="e79f5-131">Parent Elements</span></span>  
  
|<span data-ttu-id="e79f5-132">Element</span><span class="sxs-lookup"><span data-stu-id="e79f5-132">Element</span></span>|<span data-ttu-id="e79f5-133">Opis</span><span class="sxs-lookup"><span data-stu-id="e79f5-133">Description</span></span>|  
|-------------|-----------------|  
|[\<Directives>](directives-element-net-native.md)|<span data-ttu-id="e79f5-134">Element główny pliku dyrektywy środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="e79f5-134">The root element of a runtime directives file.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="e79f5-135">Uwagi</span><span class="sxs-lookup"><span data-stu-id="e79f5-135">Remarks</span></span>  

 <span data-ttu-id="e79f5-136">[\<Directives>](directives-element-net-native.md)Element może zawierać zero, jeden lub więcej `<Library>` elementów.</span><span class="sxs-lookup"><span data-stu-id="e79f5-136">The [\<Directives>](directives-element-net-native.md) element can contain zero, one, or more `<Library>` elements.</span></span>  
  
 <span data-ttu-id="e79f5-137">`<Library>`Element służy jako kontener do definiowania elementów programu, których metadane są konieczne w czasie wykonywania; ten element nie ma zasad ekspresowych.</span><span class="sxs-lookup"><span data-stu-id="e79f5-137">The `<Library>` element serves as a container to define the program elements whose metadata is needed at run time; this element doesn't express policy.</span></span> <span data-ttu-id="e79f5-138">W czasie kompilacji narzędzia kompilatora przeszukują tylko bibliotekę wyznaczony przez `<Library>` element dla elementów programu identyfikowanych przez jego elementy podrzędne.</span><span class="sxs-lookup"><span data-stu-id="e79f5-138">At compile time, compiler tools search only the library designated by the `<Library>` element for program elements identified by its child elements.</span></span> <span data-ttu-id="e79f5-139">Z kolei narzędzia kompilatora przeszukują wszystkie biblioteki, including.NET Framework Core librarys dla elementów programu identyfikowanych przez elementy podrzędne [\<Application>](application-element-net-native.md) elementu.</span><span class="sxs-lookup"><span data-stu-id="e79f5-139">In contrast, compiler tools search all libraries, including.NET Framework core libraries, for program elements identified by child elements of the [\<Application>](application-element-net-native.md) element.</span></span>  
  
 <span data-ttu-id="e79f5-140">`<Library>` dyrektywy mogą być warunkowo wykorzystywane.</span><span class="sxs-lookup"><span data-stu-id="e79f5-140">`<Library>` directives may be conditionally utilized.</span></span> <span data-ttu-id="e79f5-141">Jeśli nazwa `<Library>` elementu zaczyna się i kończy się gwiazdką ( \* ), `<Library>` dyrektywa ma wpływ tylko wtedy, gdy zestaw określony między gwiazdkami jest przywoływany przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="e79f5-141">If the name of the `<Library>` element starts and ends with an asterisk (\*), the `<Library>` directive has an effect only if the assembly specified between the asterisks is referenced by the app.</span></span> <span data-ttu-id="e79f5-142">Na przykład następująca dyrektywa środowiska uruchomieniowego ma zastosowanie tylko wtedy, gdy aplikacja jest odwołująca się do zestawu Utilities.dll.</span><span class="sxs-lookup"><span data-stu-id="e79f5-142">For example, the following runtime directive applies only if the Utilities.dll assembly is referenced by the app.</span></span>  
  
```xml  
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
  <Library Name="*Utilities*">  
   ...  
  </Library>  
</Directives>  
```  
  
## <a name="see-also"></a><span data-ttu-id="e79f5-143">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="e79f5-143">See also</span></span>

- [<span data-ttu-id="e79f5-144">\<Application> Postaci</span><span class="sxs-lookup"><span data-stu-id="e79f5-144">\<Application> Element</span></span>](application-element-net-native.md)
- [<span data-ttu-id="e79f5-145">\<Directives> Postaci</span><span class="sxs-lookup"><span data-stu-id="e79f5-145">\<Directives> Element</span></span>](directives-element-net-native.md)
- [<span data-ttu-id="e79f5-146">Dokumentacja pliku konfiguracji dyrektyw środowiska uruchomieniowego (rd.xml)</span><span class="sxs-lookup"><span data-stu-id="e79f5-146">Runtime Directives (rd.xml) Configuration File Reference</span></span>](runtime-directives-rd-xml-configuration-file-reference.md)
- [<span data-ttu-id="e79f5-147">Elementy dyrektyw środowiska uruchomieniowego</span><span class="sxs-lookup"><span data-stu-id="e79f5-147">Runtime Directive Elements</span></span>](runtime-directive-elements.md)
