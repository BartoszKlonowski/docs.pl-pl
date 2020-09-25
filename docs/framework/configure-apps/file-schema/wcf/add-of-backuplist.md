---
title: <add> dla <backupList>
ms.date: 03/30/2017
ms.assetid: bc5939fc-314a-4ea4-a533-c96958da7173
ms.openlocfilehash: 6d8fd26170059226583a300b1b48b849666db929
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91181625"
---
# <a name="add-of-backuplist"></a><span data-ttu-id="6d15c-102">\<add> dla \<backupList></span><span class="sxs-lookup"><span data-stu-id="6d15c-102">\<add> of \<backupList></span></span>

<span data-ttu-id="6d15c-103">Reprezentuje element konfiguracji, który definiuje kopię zapasową elementu punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="6d15c-103">Represents a configuration element that defines a backup endpoint element.</span></span>  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<routing>**](routing.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<backupLists>**](backuplists.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<backupList>**](backuplist.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<add>**  
  
## <a name="syntax"></a><span data-ttu-id="6d15c-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="6d15c-104">Syntax</span></span>  
  
```xml  
<routing>
  <backupLists>
    <backupList name="String">
      <add endpointName="String" />
    </backupList>
  </backupLists>
</routing>
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="6d15c-105">Atrybuty i elementy</span><span class="sxs-lookup"><span data-stu-id="6d15c-105">Attributes and Elements</span></span>  

 <span data-ttu-id="6d15c-106">W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.</span><span class="sxs-lookup"><span data-stu-id="6d15c-106">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="6d15c-107">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="6d15c-107">Attributes</span></span>  
  
|<span data-ttu-id="6d15c-108">Atrybut</span><span class="sxs-lookup"><span data-stu-id="6d15c-108">Attribute</span></span>|<span data-ttu-id="6d15c-109">Opis</span><span class="sxs-lookup"><span data-stu-id="6d15c-109">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="6d15c-110">name</span><span class="sxs-lookup"><span data-stu-id="6d15c-110">name</span></span>|<span data-ttu-id="6d15c-111">Ciąg określający nazwę punktu końcowego kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="6d15c-111">A string that specifies the name of the backup endpoint.</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="6d15c-112">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="6d15c-112">Child Elements</span></span>  

 <span data-ttu-id="6d15c-113">Brak.</span><span class="sxs-lookup"><span data-stu-id="6d15c-113">None.</span></span>  
  
### <a name="parent-elements"></a><span data-ttu-id="6d15c-114">Elementy nadrzędne</span><span class="sxs-lookup"><span data-stu-id="6d15c-114">Parent Elements</span></span>  
  
|<span data-ttu-id="6d15c-115">Element</span><span class="sxs-lookup"><span data-stu-id="6d15c-115">Element</span></span>|<span data-ttu-id="6d15c-116">Opis</span><span class="sxs-lookup"><span data-stu-id="6d15c-116">Description</span></span>|  
|-------------|-----------------|  
|[\<routing>](routing.md)|<span data-ttu-id="6d15c-117">Zawiera listę punktów końcowych, które mają być używane przez usługę routingu w przypadku, gdy podstawowy punkt końcowy nie zostanie osiągnięty.</span><span class="sxs-lookup"><span data-stu-id="6d15c-117">Contains a list of endpoints that you would like the Routing Service to use in case the primary endpoint can't be reached.</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="6d15c-118">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="6d15c-118">See also</span></span>

- <xref:System.ServiceModel.Routing.Configuration.BackupEndpointElement?displayProperty=nameWithType>
