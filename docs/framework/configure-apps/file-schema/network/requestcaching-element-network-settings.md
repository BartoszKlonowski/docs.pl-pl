---
title: <requestCaching>, element (ustawienia sieci)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#requestCaching
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/requestCaching
helpviewer_keywords:
- requestCaching element
- <requestCaching> element
ms.assetid: 9962a2fe-cbda-41a6-9377-571811eaea84
ms.openlocfilehash: 3eb32b7ae643efdb19892410b669c1e7ff80e0ad
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91174163"
---
# <a name="requestcaching-element-network-settings"></a><span data-ttu-id="f9e67-102">\<requestCaching>, element (ustawienia sieci)</span><span class="sxs-lookup"><span data-stu-id="f9e67-102">\<requestCaching> Element (Network Settings)</span></span>

<span data-ttu-id="f9e67-103">Kontroluje mechanizm buforowania dla żądań sieci.</span><span class="sxs-lookup"><span data-stu-id="f9e67-103">Controls the caching mechanism for network requests.</span></span>  
  
[**\<configuration>**](../configuration-element.md)  
&nbsp;&nbsp;[**\<system.net>**](system-net-element-network-settings.md)  
&nbsp;&nbsp;&nbsp;&nbsp;**\<requestCaching>**  
  
## <a name="syntax"></a><span data-ttu-id="f9e67-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="f9e67-104">Syntax</span></span>  
  
```xml  
<requestCaching  
  isPrivateCache ="true|false"  
  disableAllCaching="true|false"  
  defaultPolicyLevel="BypassCache|Default|CacheOnly|CacheIfAvailable|Revalidate|Reload|NoCacheNoStore|Revalidate"  
  unspecifiedMaximumAge= "d.hh:mm:ss">  
    <defaultHttpCachePolicy>...</defaultHttpCachePolicy>  
    <defaultFtpCachePolicy>...</defaultFtpCachePolicy>  
</requestCaching>
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="f9e67-105">Atrybuty i elementy</span><span class="sxs-lookup"><span data-stu-id="f9e67-105">Attributes and Elements</span></span>  

 <span data-ttu-id="f9e67-106">W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.</span><span class="sxs-lookup"><span data-stu-id="f9e67-106">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="f9e67-107">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="f9e67-107">Attributes</span></span>  
  
|<span data-ttu-id="f9e67-108">Atrybut</span><span class="sxs-lookup"><span data-stu-id="f9e67-108">Attribute</span></span>|<span data-ttu-id="f9e67-109">Opis</span><span class="sxs-lookup"><span data-stu-id="f9e67-109">Description</span></span>|  
|---------------|-----------------|  
|`isPrivateCache`|<span data-ttu-id="f9e67-110">Określa, czy pamięć podręczna zapewnia izolację między informacjami różnych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="f9e67-110">Specifies whether the cache provides isolation between the information of different users.</span></span> <span data-ttu-id="f9e67-111">Wartość domyślna to `true`.</span><span class="sxs-lookup"><span data-stu-id="f9e67-111">The default value is `true`.</span></span> <span data-ttu-id="f9e67-112">Ta wartość powinna być `false` dla aplikacji warstwy środkowej.</span><span class="sxs-lookup"><span data-stu-id="f9e67-112">This value should be `false` for middle tier applications.</span></span>|  
|`disableAllCaching`|<span data-ttu-id="f9e67-113">Określa, że buforowanie jest wyłączone dla wszystkich odpowiedzi sieci Web i nie może zostać przesłonięte programowo.</span><span class="sxs-lookup"><span data-stu-id="f9e67-113">Specifies that caching is disabled for all Web responses, and cannot be overridden programmatically.</span></span>|  
|`defaultPolicyLevel`|<span data-ttu-id="f9e67-114">Jedna z wartości w <xref:System.Net.Cache.RequestCacheLevel> wyliczeniu.</span><span class="sxs-lookup"><span data-stu-id="f9e67-114">One of the values in the <xref:System.Net.Cache.RequestCacheLevel> enumeration.</span></span> <span data-ttu-id="f9e67-115">Wartość domyślna to `BypassCache`.</span><span class="sxs-lookup"><span data-stu-id="f9e67-115">The default value is `BypassCache`.</span></span>|  
|`unspecifiedMaximumAge`|<span data-ttu-id="f9e67-116">Określa domyślny czas, po którym zawartość jest oznaczona jako wygasła.</span><span class="sxs-lookup"><span data-stu-id="f9e67-116">Specifies the default time after which content is marked as expired.</span></span>|  
  
## <a name="policylevel-attribute"></a><span data-ttu-id="f9e67-117">policyLevel — atrybut</span><span class="sxs-lookup"><span data-stu-id="f9e67-117">policyLevel Attribute</span></span>  
  
|<span data-ttu-id="f9e67-118">Wartość</span><span class="sxs-lookup"><span data-stu-id="f9e67-118">Value</span></span>|<span data-ttu-id="f9e67-119">Opis</span><span class="sxs-lookup"><span data-stu-id="f9e67-119">Description</span></span>|  
|-----------|-----------------|  
|`Default`|<span data-ttu-id="f9e67-120">Zwraca buforowany zasób, jeśli zasób jest świeży, długość zawartości jest dokładna i atrybuty daty wygaśnięcia, modyfikacji i długości zawartości są obecne.</span><span class="sxs-lookup"><span data-stu-id="f9e67-120">Returns the cached resource if the resource is fresh, the content length is accurate, and the expiration, modification, and content length attributes are present.</span></span>|  
|`BypassCache`|<span data-ttu-id="f9e67-121">Zwraca zasób z serwera.</span><span class="sxs-lookup"><span data-stu-id="f9e67-121">Returns the resource from the server.</span></span>|  
|`CacheOnly`|<span data-ttu-id="f9e67-122">Zwraca buforowany zasób, jeśli długość zawartości jest obecna i jest zgodna z rozmiarem wpisu.</span><span class="sxs-lookup"><span data-stu-id="f9e67-122">Returns the cached resource if the content length is present and matches the entry size.</span></span>|  
|`CacheIfAvailable`|<span data-ttu-id="f9e67-123">Zwraca buforowany zasób, jeśli długość zawartości jest podana i jest zgodna z rozmiarem wpisu; w przeciwnym razie zasób jest pobierany z serwera i zwracany do obiektu wywołującego.</span><span class="sxs-lookup"><span data-stu-id="f9e67-123">Returns the cached resource if the content length is provided and matches the entry size; otherwise, the resource is downloaded from the server and is returned to the caller.</span></span>|  
|`Revalidate`|<span data-ttu-id="f9e67-124">Zwraca buforowany zasób, jeśli sygnatura czasowa zasobu w pamięci podręcznej jest taka sama jak sygnatura czasowa zasobu na serwerze; w przeciwnym razie zasób jest pobierany z serwera, przechowywany w pamięci podręcznej i zwracany do obiektu wywołującego.</span><span class="sxs-lookup"><span data-stu-id="f9e67-124">Returns the cached resource if the timestamp of the cached resource is the same as the timestamp of the resource on the server; otherwise, the resource is downloaded from the server, stored in the cache, and is returned to the caller.</span></span>|  
|`Reload`|<span data-ttu-id="f9e67-125">Pobiera zasób z serwera, zapisuje go w pamięci podręcznej i zwraca zasób do obiektu wywołującego.</span><span class="sxs-lookup"><span data-stu-id="f9e67-125">Downloads the resource from the server, stores it in the cache, and returns the resource to the caller.</span></span>|  
|`NoCacheNoStore`|<span data-ttu-id="f9e67-126">Jeśli istnieje zasób w pamięci podręcznej, zostanie on usunięty.</span><span class="sxs-lookup"><span data-stu-id="f9e67-126">If a cached resource exists, it is deleted.</span></span> <span data-ttu-id="f9e67-127">Zasób jest pobierany z serwera i zwracany do obiektu wywołującego.</span><span class="sxs-lookup"><span data-stu-id="f9e67-127">The resource is downloaded from the server and is returned to the caller.</span></span>|  
|`Revalidate`|<span data-ttu-id="f9e67-128">Program spełnia żądanie przy użyciu buforowanej kopii zasobu, jeśli sygnatura czasowa jest taka sama jak sygnatura czasowa zasobu na serwerze; w przeciwnym razie zasób zostanie pobrany z serwera, który jest prezentowany obiektowi wywołującemu, i jest przechowywany w pamięci podręcznej,</span><span class="sxs-lookup"><span data-stu-id="f9e67-128">Satisfies a request by using the cached copy of the resource if the timestamp is the same as the timestamp of the resource on the server; otherwise, the resource is downloaded from the server, presented to the caller, and is stored in the cache,</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="f9e67-129">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="f9e67-129">Child Elements</span></span>  
  
|<span data-ttu-id="f9e67-130">Element</span><span class="sxs-lookup"><span data-stu-id="f9e67-130">Element</span></span>|<span data-ttu-id="f9e67-131">Opis</span><span class="sxs-lookup"><span data-stu-id="f9e67-131">Description</span></span>|  
|-------------|-----------------|  
|[<span data-ttu-id="f9e67-132">defaultHttpCachePolicy</span><span class="sxs-lookup"><span data-stu-id="f9e67-132">defaultHttpCachePolicy</span></span>](defaulthttpcachepolicy-element-network-settings.md)|<span data-ttu-id="f9e67-133">Element opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="f9e67-133">Optional element.</span></span><br /><br /> <span data-ttu-id="f9e67-134">Opisuje, czy buforowanie HTTP jest aktywne i opisuje domyślne zasady buforowania.</span><span class="sxs-lookup"><span data-stu-id="f9e67-134">Describes whether HTTP caching is active and describes the default caching policy.</span></span>|  
|[<span data-ttu-id="f9e67-135">\<defaultFtpCachePolicy> — Element (Ustawienia sieci)</span><span class="sxs-lookup"><span data-stu-id="f9e67-135">\<defaultFtpCachePolicy> Element (Network Settings)</span></span>](defaultftpcachepolicy-element-network-settings.md)|<span data-ttu-id="f9e67-136">Element opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="f9e67-136">Optional element.</span></span><br /><br /> <span data-ttu-id="f9e67-137">Opisuje, czy buforowanie FTP jest aktywne i opisuje domyślne zasady buforowania.</span><span class="sxs-lookup"><span data-stu-id="f9e67-137">Describes whether FTP caching is active and describes the default caching policy.</span></span>|  
  
### <a name="parent-elements"></a><span data-ttu-id="f9e67-138">Elementy nadrzędne</span><span class="sxs-lookup"><span data-stu-id="f9e67-138">Parent Elements</span></span>  
  
|<span data-ttu-id="f9e67-139">Element</span><span class="sxs-lookup"><span data-stu-id="f9e67-139">Element</span></span>|<span data-ttu-id="f9e67-140">Opis</span><span class="sxs-lookup"><span data-stu-id="f9e67-140">Description</span></span>|  
|-------------|-----------------|  
|[<span data-ttu-id="f9e67-141">system.net</span><span class="sxs-lookup"><span data-stu-id="f9e67-141">system.net</span></span>](system-net-element-network-settings.md)|<span data-ttu-id="f9e67-142">Zawiera ustawienia, które określają, w jaki sposób .NET Framework nawiązuje połączenie z siecią.</span><span class="sxs-lookup"><span data-stu-id="f9e67-142">Contains settings that specify how the .NET Framework connects to the network.</span></span>|  
  
## <a name="example"></a><span data-ttu-id="f9e67-143">Przykład</span><span class="sxs-lookup"><span data-stu-id="f9e67-143">Example</span></span>  

 <span data-ttu-id="f9e67-144">Poniższy przykład pokazuje, jak wyłączyć wszystkie buforowanie.</span><span class="sxs-lookup"><span data-stu-id="f9e67-144">The following example shows how to disable all caching.</span></span>  
  
```xml  
<configuration>  
  <system.net>  
    <requestCaching  
      disableAllCaching="true"  
    />  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a><span data-ttu-id="f9e67-145">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="f9e67-145">See also</span></span>

- <xref:System.Net.Cache?displayProperty=nameWithType>
- [<span data-ttu-id="f9e67-146">Schemat ustawień sieciowych</span><span class="sxs-lookup"><span data-stu-id="f9e67-146">Network Settings Schema</span></span>](index.md)
