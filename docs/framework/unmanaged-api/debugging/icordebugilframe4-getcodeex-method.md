---
title: Metoda ICorDebugILFrame4::GetCodeEx
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- ICorDebugILFrame4.GetLocalVariableEx
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: aeda0e42-29ee-4ca8-9f21-ac4641677a62
topic_type:
- apiref
ms.openlocfilehash: 06a0a4c788155d6fb909e4537b980f0ba740f21a
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90554817"
---
# <a name="icordebugilframe4getcodeex-method"></a><span data-ttu-id="32b69-102">Metoda ICorDebugILFrame4::GetCodeEx</span><span class="sxs-lookup"><span data-stu-id="32b69-102">ICorDebugILFrame4::GetCodeEx Method</span></span>
<span data-ttu-id="32b69-103">[Obsługiwane w .NET Framework 4.5.2 i nowszych wersjach]</span><span class="sxs-lookup"><span data-stu-id="32b69-103">[Supported in the .NET Framework 4.5.2 and later versions]</span></span>  
  
 <span data-ttu-id="32b69-104">Pobiera wskaźnik do kodu, który jest wykonywany przez tę ramkę stosu.</span><span class="sxs-lookup"><span data-stu-id="32b69-104">Gets a pointer to the code that this stack frame is executing.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="32b69-105">Składnia</span><span class="sxs-lookup"><span data-stu-id="32b69-105">Syntax</span></span>  
  
```cpp
HRESULT GetCodeEx(  
   [in] ILCodeKind flags,
   [out] ICorDebugCode **ppCode  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="32b69-106">Parametry</span><span class="sxs-lookup"><span data-stu-id="32b69-106">Parameters</span></span>  
 `flags`  
 <span data-ttu-id="32b69-107">podczas Element członkowski wyliczenia [ILCodeKind](ilcodekind-enumeration.md) , który określa, czy język pośredni (IL) zdefiniowany przez żądanie ReJIT profilera zostanie uwzględniony w ramce.</span><span class="sxs-lookup"><span data-stu-id="32b69-107">[in] An [ILCodeKind](ilcodekind-enumeration.md) enumeration member that specifies whether the intermediate language (IL) defined by the profiler's ReJIT request is included in the frame.</span></span>  
  
 `ppCode`  
 <span data-ttu-id="32b69-108">określoną Wskaźnik do adresu obiektu "ICorDebugCode", który reprezentuje kod, który jest wykonywany przez tę ramkę stosu.</span><span class="sxs-lookup"><span data-stu-id="32b69-108">[out] A pointer to the address of an "ICorDebugCode" object that represents the code that this stack frame is executing.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="32b69-109">Uwagi</span><span class="sxs-lookup"><span data-stu-id="32b69-109">Remarks</span></span>  
 <span data-ttu-id="32b69-110">Ta metoda jest podobna do metody [ICorDebugFrame:: GetCode](icordebugframe-getcode-method.md) , z tą różnicą, że opcjonalnie uzyskuje dostęp do kodu zdefiniowanego przez żądanie ReJIT profilera.</span><span class="sxs-lookup"><span data-stu-id="32b69-110">This method is similar to the [ICorDebugFrame::GetCode](icordebugframe-getcode-method.md) method, except that it optionally accesses code defined by the profiler's ReJIT request.</span></span> <span data-ttu-id="32b69-111">Wywołanie tej metody z `flags` wartością `ILCODE_ORIGINAL_IL` jest równoznaczne z wywołaniem metody [GetCode](icordebugframe-getcode-method.md); Jeśli metoda ma instrumentację, jej kod IL nie będzie dostępny.</span><span class="sxs-lookup"><span data-stu-id="32b69-111">Calling this method with a `flags` value of `ILCODE_ORIGINAL_IL` is equivalent to calling [GetCode](icordebugframe-getcode-method.md); if the method is instrumented, its IL will not be accessible.</span></span> <span data-ttu-id="32b69-112">`ILCODE_REJIT_IL` zezwala debugerowi na dostęp do IL zdefiniowanego przez żądanie ReJIT profilera.</span><span class="sxs-lookup"><span data-stu-id="32b69-112">`ILCODE_REJIT_IL` allows the debugger to access the IL defined by the profiler's ReJIT request.</span></span> <span data-ttu-id="32b69-113">Jeśli IL nie ma instrumentacji, `ppCode` ma **wartość null**, a metoda zwraca `S_OK` .</span><span class="sxs-lookup"><span data-stu-id="32b69-113">If the IL is not instrumented, `ppCode` is **null**, and the method returns `S_OK`.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="32b69-114">Wymagania</span><span class="sxs-lookup"><span data-stu-id="32b69-114">Requirements</span></span>  
 <span data-ttu-id="32b69-115">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="32b69-115">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="32b69-116">**Nagłówek:** CorDebug. idl, CorDebug. h</span><span class="sxs-lookup"><span data-stu-id="32b69-116">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="32b69-117">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="32b69-117">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="32b69-118">**.NET Framework wersje:**[!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="32b69-118">**.NET Framework Versions:** [!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="32b69-119">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="32b69-119">See also</span></span>

- [<span data-ttu-id="32b69-120">Interfejs ICorDebugILFrame4</span><span class="sxs-lookup"><span data-stu-id="32b69-120">ICorDebugILFrame4 Interface</span></span>](icordebugilframe4-interface.md)
- [<span data-ttu-id="32b69-121">Debugowanie — Interfejsy</span><span class="sxs-lookup"><span data-stu-id="32b69-121">Debugging Interfaces</span></span>](debugging-interfaces.md)
- [<span data-ttu-id="32b69-122">ReJIT: Przewodnik po poradniku</span><span class="sxs-lookup"><span data-stu-id="32b69-122">ReJIT: A How-To Guide</span></span>](/archive/blogs/davbr/rejit-a-how-to-guide)
