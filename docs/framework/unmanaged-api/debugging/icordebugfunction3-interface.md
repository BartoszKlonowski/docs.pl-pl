---
title: Interfejs ICorDebugFunction3
ms.date: 03/30/2017
api_name:
- ICorDebugFunction3
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: b22717b9-ead5-4eea-887e-789b52d613dc
topic_type:
- apiref
ms.openlocfilehash: 8c9c507f00780d5ef5c5aeb28a1b10493351f37e
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90546975"
---
# <a name="icordebugfunction3-interface"></a><span data-ttu-id="bd8d5-102">Interfejs ICorDebugFunction3</span><span class="sxs-lookup"><span data-stu-id="bd8d5-102">ICorDebugFunction3 Interface</span></span>
<span data-ttu-id="bd8d5-103">[Obsługiwane w .NET Framework 4.5.2 i nowszych wersjach]</span><span class="sxs-lookup"><span data-stu-id="bd8d5-103">[Supported in the .NET Framework 4.5.2 and later versions]</span></span>  
  
 <span data-ttu-id="bd8d5-104">Logicznie rozszerza interfejs ICorDebugFunction w celu zapewnienia dostępu do kodu z żądania ReJIT.</span><span class="sxs-lookup"><span data-stu-id="bd8d5-104">Logically extends the ICorDebugFunction interface to provide access to code from a ReJIT request.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="bd8d5-105">Metody</span><span class="sxs-lookup"><span data-stu-id="bd8d5-105">Methods</span></span>  
  
|<span data-ttu-id="bd8d5-106">Metoda</span><span class="sxs-lookup"><span data-stu-id="bd8d5-106">Method</span></span>|<span data-ttu-id="bd8d5-107">Opis</span><span class="sxs-lookup"><span data-stu-id="bd8d5-107">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="bd8d5-108">GetActiveReJitRequestILCode, metoda</span><span class="sxs-lookup"><span data-stu-id="bd8d5-108">GetActiveReJitRequestILCode Method</span></span>](icordebugfunction3-getactiverejitrequestilcode-method.md)|<span data-ttu-id="bd8d5-109">Pobiera wskaźnik interfejsu do [ICorDebugILCode](icordebugilcode-interface.md) zawierającego Il z aktywnego żądania ReJIT.</span><span class="sxs-lookup"><span data-stu-id="bd8d5-109">Gets an interface pointer to an [ICorDebugILCode](icordebugilcode-interface.md) that contains the IL from an active ReJIT request.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="bd8d5-110">Uwagi</span><span class="sxs-lookup"><span data-stu-id="bd8d5-110">Remarks</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="bd8d5-111">Wymagania</span><span class="sxs-lookup"><span data-stu-id="bd8d5-111">Requirements</span></span>  
 <span data-ttu-id="bd8d5-112">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="bd8d5-112">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="bd8d5-113">**Nagłówek:** CorDebug. idl, CorDebug. h</span><span class="sxs-lookup"><span data-stu-id="bd8d5-113">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="bd8d5-114">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="bd8d5-114">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="bd8d5-115">**.NET Framework wersje:**[!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="bd8d5-115">**.NET Framework Versions:** [!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="bd8d5-116">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="bd8d5-116">See also</span></span>

- [<span data-ttu-id="bd8d5-117">Debugowanie — Interfejsy</span><span class="sxs-lookup"><span data-stu-id="bd8d5-117">Debugging Interfaces</span></span>](debugging-interfaces.md)
- [<span data-ttu-id="bd8d5-118">Debugowanie</span><span class="sxs-lookup"><span data-stu-id="bd8d5-118">Debugging</span></span>](index.md)
- [<span data-ttu-id="bd8d5-119">ReJIT: Przewodnik po poradniku</span><span class="sxs-lookup"><span data-stu-id="bd8d5-119">ReJIT: A How-To Guide</span></span>](/archive/blogs/davbr/rejit-a-how-to-guide)
