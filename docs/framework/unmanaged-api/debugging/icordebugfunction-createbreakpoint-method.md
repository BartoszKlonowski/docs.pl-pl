---
title: ICorDebugFunction::CreateBreakpoint — Metoda
ms.date: 03/30/2017
api_name:
- ICorDebugFunction.CreateBreakpoint
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugFunction::CreateBreakpoint
helpviewer_keywords:
- ICorDebugFunction::CreateBreakpoint method [.NET Framework debugging]
- CreateBreakpoint method, ICorDebugFunction interface [.NET Framework debugging]
ms.assetid: ffd0f708-0d21-4fae-a395-63b6c45828fa
topic_type:
- apiref
ms.openlocfilehash: 2d1846acae51f416471404389dd1dbcfb2383760
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95728176"
---
# <a name="icordebugfunctioncreatebreakpoint-method"></a><span data-ttu-id="ca07d-102">ICorDebugFunction::CreateBreakpoint — Metoda</span><span class="sxs-lookup"><span data-stu-id="ca07d-102">ICorDebugFunction::CreateBreakpoint Method</span></span>

<span data-ttu-id="ca07d-103">Tworzy punkt przerwania na początku tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="ca07d-103">Creates a breakpoint at the beginning of this function.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="ca07d-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="ca07d-104">Syntax</span></span>  
  
```cpp  
HRESULT CreateBreakpoint (  
    [out] ICorDebugFunctionBreakpoint **ppBreakpoint  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="ca07d-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="ca07d-105">Parameters</span></span>  

 `ppBreakpoint`  
 <span data-ttu-id="ca07d-106">określoną Wskaźnik do adresu obiektu ICorDebugFunctionBreakpoint, który reprezentuje nowy punkt przerwania dla funkcji.</span><span class="sxs-lookup"><span data-stu-id="ca07d-106">[out] A pointer to the address of an ICorDebugFunctionBreakpoint object that represents the new breakpoint for the function.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="ca07d-107">Wymagania</span><span class="sxs-lookup"><span data-stu-id="ca07d-107">Requirements</span></span>  

 <span data-ttu-id="ca07d-108">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="ca07d-108">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="ca07d-109">**Nagłówek:** CorDebug. idl, CorDebug. h</span><span class="sxs-lookup"><span data-stu-id="ca07d-109">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="ca07d-110">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="ca07d-110">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="ca07d-111">**.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="ca07d-111">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>
