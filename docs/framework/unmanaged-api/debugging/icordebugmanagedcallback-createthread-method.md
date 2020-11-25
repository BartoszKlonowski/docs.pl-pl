---
title: ICorDebugManagedCallback::CreateThread — Metoda
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback.CreateThread
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback::CreateThread method
helpviewer_keywords:
- ICorDebugManagedCallback::CreateThread method [.NET Framework debugging]
- CreateThread method [.NET Framework debugging]
ms.assetid: 6b961728-21c4-4e8d-ae81-197458be62f4
topic_type:
- apiref
ms.openlocfilehash: 56ec7c56b167c29c9951638c5eee159e1d3c7ffb
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95721299"
---
# <a name="icordebugmanagedcallbackcreatethread-method"></a><span data-ttu-id="33730-102">ICorDebugManagedCallback::CreateThread — Metoda</span><span class="sxs-lookup"><span data-stu-id="33730-102">ICorDebugManagedCallback::CreateThread Method</span></span>

<span data-ttu-id="33730-103">Powiadamia debuger o rozpoczęciu wykonywania kodu zarządzanego przez wątek.</span><span class="sxs-lookup"><span data-stu-id="33730-103">Notifies the debugger that a thread has started executing managed code.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="33730-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="33730-104">Syntax</span></span>  
  
```cpp  
HRESULT CreateThread (  
    [in] ICorDebugAppDomain *pAppDomain,  
    [in] ICorDebugThread    *thread  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="33730-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="33730-105">Parameters</span></span>  

 `pAppDomain`  
 <span data-ttu-id="33730-106">podczas Wskaźnik do obiektu ICorDebugAppDomain, który reprezentuje domenę aplikacji, która zawiera wątek.</span><span class="sxs-lookup"><span data-stu-id="33730-106">[in] A pointer to an ICorDebugAppDomain object that represents the application domain that contains the thread.</span></span>  
  
 `thread`  
 <span data-ttu-id="33730-107">podczas Wskaźnik do obiektu ICorDebugThread, który reprezentuje wątek.</span><span class="sxs-lookup"><span data-stu-id="33730-107">[in] A pointer to an ICorDebugThread object that represents the thread.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="33730-108">Uwagi</span><span class="sxs-lookup"><span data-stu-id="33730-108">Remarks</span></span>  

 <span data-ttu-id="33730-109">Wątek zostanie umieszczony w pierwszej instrukcji kodu zarządzanego do wykonania.</span><span class="sxs-lookup"><span data-stu-id="33730-109">The thread will be positioned at the first managed code instruction to be executed.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="33730-110">Wymagania</span><span class="sxs-lookup"><span data-stu-id="33730-110">Requirements</span></span>  

 <span data-ttu-id="33730-111">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="33730-111">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="33730-112">**Nagłówek:** CorDebug. idl, CorDebug. h</span><span class="sxs-lookup"><span data-stu-id="33730-112">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="33730-113">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="33730-113">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="33730-114">**.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="33730-114">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="33730-115">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="33730-115">See also</span></span>

- [<span data-ttu-id="33730-116">ICorDebugManagedCallback — Interfejs</span><span class="sxs-lookup"><span data-stu-id="33730-116">ICorDebugManagedCallback Interface</span></span>](icordebugmanagedcallback-interface.md)
