---
title: ICorDebugAssembly, interfejs
ms.date: 03/30/2017
api_name:
- ICorDebugAssembly
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugAssembly
helpviewer_keywords:
- ICorDebugAssembly interface [.NET Framework debugging]
ms.assetid: 9d657a28-6984-4c5e-8a54-89d20080baff
topic_type:
- apiref
ms.openlocfilehash: 821eae8ea5b4147408e9fe60d1e5b70c7936959e
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95696248"
---
# <a name="icordebugassembly-interface"></a><span data-ttu-id="a587b-102">ICorDebugAssembly, interfejs</span><span class="sxs-lookup"><span data-stu-id="a587b-102">ICorDebugAssembly Interface</span></span>

<span data-ttu-id="a587b-103">Reprezentuje zestaw.</span><span class="sxs-lookup"><span data-stu-id="a587b-103">Represents an assembly.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="a587b-104">Metody</span><span class="sxs-lookup"><span data-stu-id="a587b-104">Methods</span></span>  
  
|<span data-ttu-id="a587b-105">Metoda</span><span class="sxs-lookup"><span data-stu-id="a587b-105">Method</span></span>|<span data-ttu-id="a587b-106">Opis</span><span class="sxs-lookup"><span data-stu-id="a587b-106">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="a587b-107">EnumerateModules, metoda</span><span class="sxs-lookup"><span data-stu-id="a587b-107">EnumerateModules Method</span></span>](icordebugassembly-enumeratemodules-method.md)|<span data-ttu-id="a587b-108">Pobiera moduł wyliczający dla modułów zawartych w zestawie.</span><span class="sxs-lookup"><span data-stu-id="a587b-108">Gets an enumerator for the modules contained in the assembly.</span></span>|  
|[<span data-ttu-id="a587b-109">GetAppDomain, metoda</span><span class="sxs-lookup"><span data-stu-id="a587b-109">GetAppDomain Method</span></span>](icordebugassembly-getappdomain-method.md)|<span data-ttu-id="a587b-110">Pobiera wskaźnik interfejsu do domeny aplikacji, która zawiera to `ICorDebugAssembly` wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="a587b-110">Gets an interface pointer to the application domain that contains this `ICorDebugAssembly` instance.</span></span>|  
|[<span data-ttu-id="a587b-111">GetCodeBase, metoda</span><span class="sxs-lookup"><span data-stu-id="a587b-111">GetCodeBase Method</span></span>](icordebugassembly-getcodebase-method.md)|<span data-ttu-id="a587b-112">Nie zaimplementowane w bieżącej wersji .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="a587b-112">Not implemented in the current version of the .NET Framework.</span></span>|  
|[<span data-ttu-id="a587b-113">GetName — Metoda</span><span class="sxs-lookup"><span data-stu-id="a587b-113">GetName Method</span></span>](icordebugassembly-getname-method.md)|<span data-ttu-id="a587b-114">Pobiera nazwę zestawu.</span><span class="sxs-lookup"><span data-stu-id="a587b-114">Gets the name of the assembly.</span></span>|  
|[<span data-ttu-id="a587b-115">GetProcess — Metoda</span><span class="sxs-lookup"><span data-stu-id="a587b-115">GetProcess Method</span></span>](icordebugassembly-getprocess-method.md)|<span data-ttu-id="a587b-116">Pobiera wystąpienie ICorDebugProcess, w którym jest uruchomiony zestaw.</span><span class="sxs-lookup"><span data-stu-id="a587b-116">Gets the ICorDebugProcess instance in which the assembly is running.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="a587b-117">Uwagi</span><span class="sxs-lookup"><span data-stu-id="a587b-117">Remarks</span></span>  
  
> [!NOTE]
> <span data-ttu-id="a587b-118">Ten interfejs nie obsługuje wywoływania zdalnego na wielu maszynach ani wielu procesów.</span><span class="sxs-lookup"><span data-stu-id="a587b-118">This interface does not support being called remotely, either cross-machine or cross-process.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="a587b-119">Wymagania</span><span class="sxs-lookup"><span data-stu-id="a587b-119">Requirements</span></span>  

 <span data-ttu-id="a587b-120">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="a587b-120">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="a587b-121">**Nagłówek:** CorDebug. idl, CorDebug. h</span><span class="sxs-lookup"><span data-stu-id="a587b-121">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="a587b-122">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="a587b-122">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="a587b-123">**.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="a587b-123">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a587b-124">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="a587b-124">See also</span></span>

- [<span data-ttu-id="a587b-125">Debugowanie — Interfejsy</span><span class="sxs-lookup"><span data-stu-id="a587b-125">Debugging Interfaces</span></span>](debugging-interfaces.md)
