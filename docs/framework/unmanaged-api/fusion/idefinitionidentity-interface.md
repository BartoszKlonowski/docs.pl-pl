---
title: IDefinitionIdentity — Interfejs
ms.date: 03/30/2017
api_name:
- IDefinitionIdentity
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- IDefinitionIdentity
helpviewer_keywords:
- IDefinitionIdentity interface [.NET Framework fusion]
ms.assetid: ce5ba888-5fbe-4efd-91cf-f0ff94d8428b
topic_type:
- apiref
ms.openlocfilehash: 4f08fbbf9c8be16dff092327713e731c5aa14661
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95732882"
---
# <a name="idefinitionidentity-interface"></a><span data-ttu-id="435f7-102">IDefinitionIdentity — Interfejs</span><span class="sxs-lookup"><span data-stu-id="435f7-102">IDefinitionIdentity Interface</span></span>

<span data-ttu-id="435f7-103">Reprezentuje unikatowy podpis kodu, który definiuje aplikację w bieżącym zakresie.</span><span class="sxs-lookup"><span data-stu-id="435f7-103">Represents the unique signature of the code that defines the application in the current scope.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="435f7-104">Metody</span><span class="sxs-lookup"><span data-stu-id="435f7-104">Methods</span></span>  
  
|<span data-ttu-id="435f7-105">Metoda</span><span class="sxs-lookup"><span data-stu-id="435f7-105">Method</span></span>|<span data-ttu-id="435f7-106">Opis</span><span class="sxs-lookup"><span data-stu-id="435f7-106">Description</span></span>|  
|------------|-----------------|  
|`IDefinitionIdentity::Clone`|<span data-ttu-id="435f7-107">Pobiera wskaźnik interfejsu do nowego `IDefinitionIdentity` obiektu, który jest identyczny z tym `IDefinitionIdentity` , z wyjątkiem określonych zmian atrybutów.</span><span class="sxs-lookup"><span data-stu-id="435f7-107">Gets an interface pointer to a new `IDefinitionIdentity` object that is identical to this `IDefinitionIdentity`, except for the specified attribute changes.</span></span>|  
|`IDefinitionIdentity::EnumAttributes`|<span data-ttu-id="435f7-108">Pobiera wskaźnik interfejsu do obiektu [IEnumIDENTITY_ATTRIBUTE](ienumidentity-attribute-interface.md) , który zawiera atrybuty skojarzone z tym `IDefinitionIdentity` .</span><span class="sxs-lookup"><span data-stu-id="435f7-108">Gets an interface pointer to an [IEnumIDENTITY_ATTRIBUTE](ienumidentity-attribute-interface.md) object that contains the attributes associated with this `IDefinitionIdentity`.</span></span>|  
|`IDefinitionIdentity::GetAttribute`|<span data-ttu-id="435f7-109">Pobiera wartość atrybutu o określonej nazwie w określonym obszarze nazw.</span><span class="sxs-lookup"><span data-stu-id="435f7-109">Gets the value of the attribute with the specified name in the specified namespace.</span></span>|  
|`IDefinitionIdentity::SetAttribute`|<span data-ttu-id="435f7-110">Ustawia atrybut, który ma określoną nazwę w określonym obszarze nazw do określonej wartości.</span><span class="sxs-lookup"><span data-stu-id="435f7-110">Sets the attribute that has the specified name in the specified namespace to the specified value.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="435f7-111">Wymagania</span><span class="sxs-lookup"><span data-stu-id="435f7-111">Requirements</span></span>  

 <span data-ttu-id="435f7-112">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="435f7-112">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="435f7-113">**Nagłówek:** Izolacja. h</span><span class="sxs-lookup"><span data-stu-id="435f7-113">**Header:** Isolation.h</span></span>  
  
 <span data-ttu-id="435f7-114">**.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="435f7-114">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="435f7-115">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="435f7-115">See also</span></span>

- [<span data-ttu-id="435f7-116">Interfejsy łączenia</span><span class="sxs-lookup"><span data-stu-id="435f7-116">Fusion Interfaces</span></span>](fusion-interfaces.md)
