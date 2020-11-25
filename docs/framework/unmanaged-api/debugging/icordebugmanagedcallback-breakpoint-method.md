---
title: ICorDebugManagedCallback::Breakpoint — Metoda
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback.Breakpoint
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback::Breakpoint
helpviewer_keywords:
- ICorDebugManagedCallback::Breakpoint method [.NET Framework debugging]
- Breakpoint method [.NET Framework debugging]
ms.assetid: 60b279b0-a726-46d2-8c53-76986a007ebb
topic_type:
- apiref
ms.openlocfilehash: d7cf966f407572cc681f641b63791906a5c015f3
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95731868"
---
# <a name="icordebugmanagedcallbackbreakpoint-method"></a><span data-ttu-id="4c50d-102">ICorDebugManagedCallback::Breakpoint — Metoda</span><span class="sxs-lookup"><span data-stu-id="4c50d-102">ICorDebugManagedCallback::Breakpoint Method</span></span>

<span data-ttu-id="4c50d-103">Powiadamia debuger w przypadku napotkania punktu przerwania.</span><span class="sxs-lookup"><span data-stu-id="4c50d-103">Notifies the debugger when a breakpoint is encountered.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="4c50d-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="4c50d-104">Syntax</span></span>  
  
```cpp  
HRESULT Breakpoint (  
    [in] ICorDebugAppDomain  *pAppDomain,  
    [in] ICorDebugThread     *pThread,  
    [in] ICorDebugBreakpoint *pBreakpoint  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="4c50d-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="4c50d-105">Parameters</span></span>  

 `pAppDomain`  
 <span data-ttu-id="4c50d-106">podczas Wskaźnik do obiektu ICorDebugAppDomain, który reprezentuje domenę aplikacji, która zawiera punkt przerwania.</span><span class="sxs-lookup"><span data-stu-id="4c50d-106">[in] A pointer to an ICorDebugAppDomain object that represents the application domain that contains the breakpoint.</span></span>  
  
 `pThread`  
 <span data-ttu-id="4c50d-107">podczas Wskaźnik do obiektu ICorDebugThread, który reprezentuje wątek, który zawiera punkt przerwania.</span><span class="sxs-lookup"><span data-stu-id="4c50d-107">[in] A pointer to an ICorDebugThread object that represents the thread that contains the breakpoint.</span></span>  
  
 `pBreakpoint`  
 <span data-ttu-id="4c50d-108">podczas Wskaźnik do obiektu ICorDebugBreakpoint, który reprezentuje punkt przerwania.</span><span class="sxs-lookup"><span data-stu-id="4c50d-108">[in] A pointer to an ICorDebugBreakpoint object that represents the breakpoint.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="4c50d-109">Wymagania</span><span class="sxs-lookup"><span data-stu-id="4c50d-109">Requirements</span></span>  

 <span data-ttu-id="4c50d-110">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="4c50d-110">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="4c50d-111">**Nagłówek:** CorDebug. idl, CorDebug. h</span><span class="sxs-lookup"><span data-stu-id="4c50d-111">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="4c50d-112">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="4c50d-112">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="4c50d-113">**.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="4c50d-113">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="4c50d-114">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="4c50d-114">See also</span></span>

- [<span data-ttu-id="4c50d-115">ICorDebugManagedCallback — Interfejs</span><span class="sxs-lookup"><span data-stu-id="4c50d-115">ICorDebugManagedCallback Interface</span></span>](icordebugmanagedcallback-interface.md)
