---
title: ICorPublish::GetProcess — Metoda
ms.date: 03/30/2017
api_name:
- ICorPublish.GetProcess
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorPublish::GetProcess
helpviewer_keywords:
- ICorPublish::GetProcess method [.NET Framework debugging]
- GetProcess method, ICorPublish interface [.NET Framework debugging]
ms.assetid: c5143805-2eb7-45b8-85ed-c8fb34df1084
topic_type:
- apiref
ms.openlocfilehash: a45f613b7547e2e80abdbd8ac85cb0b2b6a499e5
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95716892"
---
# <a name="icorpublishgetprocess-method"></a><span data-ttu-id="75736-102">ICorPublish::GetProcess — Metoda</span><span class="sxs-lookup"><span data-stu-id="75736-102">ICorPublish::GetProcess Method</span></span>

<span data-ttu-id="75736-103">Pobiera wystąpienie [ICorPublishProcess](icorpublishprocess-interface.md) , które reprezentuje proces o określonym identyfikatorze.</span><span class="sxs-lookup"><span data-stu-id="75736-103">Gets an [ICorPublishProcess](icorpublishprocess-interface.md) instance that represents the process with the specified identifier.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="75736-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="75736-104">Syntax</span></span>  
  
```cpp  
HRESULT GetProcess(  
    [in] unsigned              pid,
    [out] ICorPublishProcess   **ppProcess  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="75736-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="75736-105">Parameters</span></span>  

 `pid`  
 <span data-ttu-id="75736-106">podczas Identyfikator procesu.</span><span class="sxs-lookup"><span data-stu-id="75736-106">[in] The identifier of the process.</span></span>  
  
 `ppProcess`  
 <span data-ttu-id="75736-107">określoną Wskaźnik do adresu `ICorPublishProcess` wystąpienia, które reprezentuje proces.</span><span class="sxs-lookup"><span data-stu-id="75736-107">[out] A pointer to the address of an `ICorPublishProcess` instance that represents the process.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="75736-108">Uwagi</span><span class="sxs-lookup"><span data-stu-id="75736-108">Remarks</span></span>  

 <span data-ttu-id="75736-109">`GetProcess` Niepowodzenie, jeśli proces nie istnieje lub nie jest procesem zarządzanym, który może być debugowany przez bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="75736-109">`GetProcess` fails if the process doesn't exist, or isn't a managed process that can be debugged by the current user.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="75736-110">Wymagania</span><span class="sxs-lookup"><span data-stu-id="75736-110">Requirements</span></span>  

 <span data-ttu-id="75736-111">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="75736-111">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="75736-112">**Nagłówek:** CorPub. idl, CorPub. h</span><span class="sxs-lookup"><span data-stu-id="75736-112">**Header:** CorPub.idl, CorPub.h</span></span>  
  
 <span data-ttu-id="75736-113">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="75736-113">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="75736-114">**.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="75736-114">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="75736-115">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="75736-115">See also</span></span>

- [<span data-ttu-id="75736-116">ICorPublish — Interfejs</span><span class="sxs-lookup"><span data-stu-id="75736-116">ICorPublish Interface</span></span>](icorpublish-interface.md)
