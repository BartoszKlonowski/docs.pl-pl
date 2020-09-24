---
title: <shadowCopyVerifyByTimestamp> Element
ms.date: 03/30/2017
helpviewer_keywords:
- <shadowCopyTimeStampVerification> element
- shadowCopyTimeStampVerification element
ms.assetid: 2f1648e5-997b-435e-a4f9-d236c574c66c
ms.openlocfilehash: c0dc190e69ca9650d518ee297b12f79f8c47d58b
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91183978"
---
# <a name="shadowcopyverifybytimestamp-element"></a><span data-ttu-id="c973f-102">\<shadowCopyVerifyByTimestamp> Element</span><span class="sxs-lookup"><span data-stu-id="c973f-102">\<shadowCopyVerifyByTimestamp> Element</span></span>

<span data-ttu-id="c973f-103">Określa, czy kopiowanie w tle używa domyślnego zachowania uruchamiania wprowadzonego w .NET Framework 4, czy przywraca zachowanie uruchamiania wcześniejszych wersji .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="c973f-103">Specifies whether shadow copying uses the default startup behavior introduced in the .NET Framework 4, or reverts to the startup behavior of earlier versions of the .NET Framework.</span></span>  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<runtime>**](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<shadowCopyVerifyByTimestamp>**  
  
## <a name="syntax"></a><span data-ttu-id="c973f-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="c973f-104">Syntax</span></span>  
  
```xml  
<shadowCopyVerifyByTimestamp enabled="true|false" />  
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="c973f-105">Atrybuty i elementy</span><span class="sxs-lookup"><span data-stu-id="c973f-105">Attributes and Elements</span></span>  

 <span data-ttu-id="c973f-106">W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.</span><span class="sxs-lookup"><span data-stu-id="c973f-106">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="c973f-107">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="c973f-107">Attributes</span></span>  
  
|<span data-ttu-id="c973f-108">Atrybut</span><span class="sxs-lookup"><span data-stu-id="c973f-108">Attribute</span></span>|<span data-ttu-id="c973f-109">Opis</span><span class="sxs-lookup"><span data-stu-id="c973f-109">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="c973f-110">enabled</span><span class="sxs-lookup"><span data-stu-id="c973f-110">enabled</span></span>|<span data-ttu-id="c973f-111">Atrybut wymagany.</span><span class="sxs-lookup"><span data-stu-id="c973f-111">Required attribute.</span></span><br /><br /> <span data-ttu-id="c973f-112">Określa, czy domeny aplikacji używające kopiowania w tle porównują sygnatury czasowe zestawów podczas uruchamiania, aby określić, czy zestaw został zaktualizowany przed skopiowaniem zestawu w tle.</span><span class="sxs-lookup"><span data-stu-id="c973f-112">Specifies whether application domains that use shadow copying compare assembly time stamps when starting up, to determine whether an assembly has been updated before shadow copying the assembly.</span></span>|  
  
## <a name="enabled-attribute"></a><span data-ttu-id="c973f-113">Atrybut włączony</span><span class="sxs-lookup"><span data-stu-id="c973f-113">enabled Attribute</span></span>  
  
|<span data-ttu-id="c973f-114">Wartość</span><span class="sxs-lookup"><span data-stu-id="c973f-114">Value</span></span>|<span data-ttu-id="c973f-115">Opis</span><span class="sxs-lookup"><span data-stu-id="c973f-115">Description</span></span>|  
|-----------|-----------------|  
|<span data-ttu-id="c973f-116">true</span><span class="sxs-lookup"><span data-stu-id="c973f-116">true</span></span>|<span data-ttu-id="c973f-117">Podczas uruchamiania program kopiuje tylko te zestawy, które zostały zaktualizowane od czasu ostatniego skopiowania do katalogu kopii w tle.</span><span class="sxs-lookup"><span data-stu-id="c973f-117">At startup, copies only assemblies that have been updated since they were last copied to the shadow copy directory.</span></span> <span data-ttu-id="c973f-118">Jest to wartość domyślna dla .NET Framework 4.</span><span class="sxs-lookup"><span data-stu-id="c973f-118">This is the default for the .NET Framework 4.</span></span>|  
|<span data-ttu-id="c973f-119">fałsz</span><span class="sxs-lookup"><span data-stu-id="c973f-119">false</span></span>|<span data-ttu-id="c973f-120">Przywraca zachowanie uruchamiania poprzednich wersji .NET Framework, które było skopiowane wszystkie pliki podczas uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="c973f-120">Reverts to the startup behavior of previous versions of the .NET Framework, which was to copy all files at startup.</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="c973f-121">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="c973f-121">Child Elements</span></span>  

 <span data-ttu-id="c973f-122">Brak.</span><span class="sxs-lookup"><span data-stu-id="c973f-122">None.</span></span>  
  
### <a name="parent-elements"></a><span data-ttu-id="c973f-123">Elementy nadrzędne</span><span class="sxs-lookup"><span data-stu-id="c973f-123">Parent Elements</span></span>  
  
|<span data-ttu-id="c973f-124">Element</span><span class="sxs-lookup"><span data-stu-id="c973f-124">Element</span></span>|<span data-ttu-id="c973f-125">Opis</span><span class="sxs-lookup"><span data-stu-id="c973f-125">Description</span></span>|  
|-------------|-----------------|  
|`configuration`|<span data-ttu-id="c973f-126">Element główny w każdym pliku konfiguracji używanym przez środowisko uruchomieniowe języka wspólnego i aplikacje programu .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="c973f-126">The root element in every configuration file used by the common language runtime and .NET Framework applications.</span></span>|  
|`runtime`|<span data-ttu-id="c973f-127">Zawiera informacje dotyczące powiązania zestawu oraz wyrzucania elementów bezużytecznych.</span><span class="sxs-lookup"><span data-stu-id="c973f-127">Contains information about assembly binding and garbage collection.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="c973f-128">Uwagi</span><span class="sxs-lookup"><span data-stu-id="c973f-128">Remarks</span></span>  

 <span data-ttu-id="c973f-129">Począwszy od .NET Framework 4, zestawy są kopiowane w tle, tylko wtedy, gdy ich sygnatury czasowe wskazują, że zostały zmienione od czasu ostatniego skopiowania do katalogu kopii w tle.</span><span class="sxs-lookup"><span data-stu-id="c973f-129">Starting with the .NET Framework 4, assemblies are shadow copied only if their time stamps indicate that they have changed since they were last copied to the shadow copy directory.</span></span> <span data-ttu-id="c973f-130">Skraca to czas uruchamiania dla wielu aplikacji używających kopiowania w tle, zgodnie z opisem w obszarze [kopiowania w tle](../../../app-domains/shadow-copy-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="c973f-130">This improves startup times for many applications that use shadow copying, as described in [Shadow Copying Assemblies](../../../app-domains/shadow-copy-assemblies.md).</span></span> <span data-ttu-id="c973f-131">W przypadku aplikacji z wysoką wartością procentową i częstotliwością aktualizacji zestawu mogą nie być korzystne zmiany w zachowaniu.</span><span class="sxs-lookup"><span data-stu-id="c973f-131">Applications that have a high percentage and frequency of assembly updates might not benefit from this change in behavior.</span></span> <span data-ttu-id="c973f-132">W takim przypadku można użyć tego elementu, aby przywrócić zachowanie poprzednich wersji .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="c973f-132">In that case, you can use this element to restore the behavior of previous versions of the .NET Framework.</span></span>  
  
## <a name="example"></a><span data-ttu-id="c973f-133">Przykład</span><span class="sxs-lookup"><span data-stu-id="c973f-133">Example</span></span>  

 <span data-ttu-id="c973f-134">Poniższy przykład pokazuje, jak wyłączyć domyślne zachowanie podczas uruchamiania kopiowania w tle w .NET Framework 4 i przywrócić zachowanie uruchamiania poprzednich wersji .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="c973f-134">The following example shows how to disable the default startup behavior of shadow copying in the .NET Framework 4, and revert to the startup behavior of previous versions of the .NET Framework.</span></span>  
  
```xml  
<configuration>  
   <runtime>  
      <shadowCopyVerifyByTimestamp enabled="false" />  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a><span data-ttu-id="c973f-135">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="c973f-135">See also</span></span>

- [<span data-ttu-id="c973f-136">Schemat ustawień środowiska uruchomieniowego</span><span class="sxs-lookup"><span data-stu-id="c973f-136">Runtime Settings Schema</span></span>](index.md)
- [<span data-ttu-id="c973f-137">Schemat pliku konfiguracji</span><span class="sxs-lookup"><span data-stu-id="c973f-137">Configuration File Schema</span></span>](../index.md)
- [<span data-ttu-id="c973f-138">Kopiowanie zestawów w tle</span><span class="sxs-lookup"><span data-stu-id="c973f-138">Shadow Copying Assemblies</span></span>](../../../app-domains/shadow-copy-assemblies.md)
