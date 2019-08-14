---
title: ICorProfilerInfo10, interfejs
ms.date: 08/06/2019
author: davmason
ms.author: davmason
ms.openlocfilehash: 496959ecac5b16f1faa138aec90c5194d15cb105
ms.sourcegitcommit: a97ecb94437362b21fffc5eb3c38b6c0b4368999
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/13/2019
ms.locfileid: "68973751"
---
# <a name="icorprofilerinfo10-interface"></a><span data-ttu-id="535d9-102">ICorProfilerInfo10, interfejs</span><span class="sxs-lookup"><span data-stu-id="535d9-102">ICorProfilerInfo10 Interface</span></span>

<span data-ttu-id="535d9-103">Podklasa elementu [ICorProfilerInfo9](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo9-interface.md) , która udostępnia metody modyfikowania funkcji IL, zapytania o informacje z środowiska uruchomieniowego oraz wstrzymywanie i wznawianie środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="535d9-103">A subclass of [ICorProfilerInfo9](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo9-interface.md) that provides methods to modify function IL, query information from the runtime, and suspend and resume the runtime.</span></span>

## <a name="methods"></a><span data-ttu-id="535d9-104">Metody</span><span class="sxs-lookup"><span data-stu-id="535d9-104">Methods</span></span>  

| <span data-ttu-id="535d9-105">Metoda</span><span class="sxs-lookup"><span data-stu-id="535d9-105">Method</span></span>|<span data-ttu-id="535d9-106">Opis</span><span class="sxs-lookup"><span data-stu-id="535d9-106">Description</span></span>|  
| ------------|-----------------|  
|[<span data-ttu-id="535d9-107">EnumerateObjectReferences, Metoda</span><span class="sxs-lookup"><span data-stu-id="535d9-107">EnumerateObjectReferences Method</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo10-enumerateobjectreferences-method.md)|<span data-ttu-id="535d9-108">Podanym identyfikatorem ObjectID, wywołaniem zwrotnym i clientData, wylicza każde odwołanie do obiektu (jeśli istnieje).</span><span class="sxs-lookup"><span data-stu-id="535d9-108">Given an ObjectID, callback and clientData, enumerates each object reference (if any).</span></span> |
|[<span data-ttu-id="535d9-109">Zamrożonobject, Metoda</span><span class="sxs-lookup"><span data-stu-id="535d9-109">IsFrozenObject Method</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo10-isfrozenobject-method.md)|<span data-ttu-id="535d9-110">Przy użyciu identyfikatora ObjectID określa, czy obiekt znajduje się w segmencie tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="535d9-110">Given an ObjectID, determines whether the object is in a read-only segment.</span></span> |
|[<span data-ttu-id="535d9-111">GetLOHObjectSizeThreshold, Metoda</span><span class="sxs-lookup"><span data-stu-id="535d9-111">GetLOHObjectSizeThreshold Method</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo10-getlohobjectsizethreshold-method.md)|<span data-ttu-id="535d9-112">Pobiera wartość skonfigurowanego progu LOH.</span><span class="sxs-lookup"><span data-stu-id="535d9-112">Gets the value of the configured LOH threshold.</span></span> |
|[<span data-ttu-id="535d9-113">RequestReJITWithInliners, Metoda</span><span class="sxs-lookup"><span data-stu-id="535d9-113">RequestReJITWithInliners Method</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo10-requestrejitwithinliners-method.md)| <span data-ttu-id="535d9-114">ReJITs wymagane metody, a także wszystkie wbudowane metody.</span><span class="sxs-lookup"><span data-stu-id="535d9-114">ReJITs the methods requested, as well as any inliners of the methods requested.</span></span>  |
|[<span data-ttu-id="535d9-115">SuspendRuntime, Metoda</span><span class="sxs-lookup"><span data-stu-id="535d9-115">SuspendRuntime Method</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo10-suspendruntime-method.md)| <span data-ttu-id="535d9-116">Wstrzymuje środowisko uruchomieniowe bez wykonywania operacji GC.</span><span class="sxs-lookup"><span data-stu-id="535d9-116">Suspends the runtime without performing a GC.</span></span> |
|[<span data-ttu-id="535d9-117">ResumeRuntime, Metoda</span><span class="sxs-lookup"><span data-stu-id="535d9-117">ResumeRuntime Method</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo10-resumeruntime-method.md)| <span data-ttu-id="535d9-118">Wznawia środowisko uruchomieniowe bez wykonywania operacji GC.</span><span class="sxs-lookup"><span data-stu-id="535d9-118">Resumes the runtime without performing a GC.</span></span> |

## <a name="requirements"></a><span data-ttu-id="535d9-119">Wymagania</span><span class="sxs-lookup"><span data-stu-id="535d9-119">Requirements</span></span>  
<span data-ttu-id="535d9-120">**Poszczególnych** Zobacz [obsługiwane systemy operacyjne .NET Core](../../../core/windows-prerequisites.md#net-core-supported-operating-systems).</span><span class="sxs-lookup"><span data-stu-id="535d9-120">**Platforms:** See [.NET Core supported operating systems](../../../core/windows-prerequisites.md#net-core-supported-operating-systems).</span></span>  
<span data-ttu-id="535d9-121">**Nagłówki** CorProf. idl, CorProf. h</span><span class="sxs-lookup"><span data-stu-id="535d9-121">**Header:** CorProf.idl, CorProf.h</span></span>  
<span data-ttu-id="535d9-122">**Wersje .NET:** [!INCLUDE[net_core_22](../../../../includes/net-core-30-md.md)]</span><span class="sxs-lookup"><span data-stu-id="535d9-122">**.NET Versions:** [!INCLUDE[net_core_22](../../../../includes/net-core-30-md.md)]</span></span> 
## <a name="see-also"></a><span data-ttu-id="535d9-123">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="535d9-123">See also</span></span>
- [<span data-ttu-id="535d9-124">Interfejsy profilowania</span><span class="sxs-lookup"><span data-stu-id="535d9-124">Profiling Interfaces</span></span>](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)