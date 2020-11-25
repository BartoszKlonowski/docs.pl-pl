---
title: ICorDebugObjectValue::GetClass — Metoda
ms.date: 03/30/2017
api_name:
- ICorDebugObjectValue.GetClass
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugObjectValue::GetClass
helpviewer_keywords:
- ICorDebugObjectValue::GetClass method [.NET Framework debugging]
- GetClass method, ICorDebugObjectValue interface [.NET Framework debugging]
ms.assetid: 5be25292-8357-445f-a09b-f997c0de761c
topic_type:
- apiref
ms.openlocfilehash: 42e5ffeeb81bc5e9a99c8ada8d58296fc9f610d3
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95695416"
---
# <a name="icordebugobjectvaluegetclass-method"></a><span data-ttu-id="6332f-102">ICorDebugObjectValue::GetClass — Metoda</span><span class="sxs-lookup"><span data-stu-id="6332f-102">ICorDebugObjectValue::GetClass Method</span></span>

<span data-ttu-id="6332f-103">Pobiera klasę tej wartości obiektu.</span><span class="sxs-lookup"><span data-stu-id="6332f-103">Gets the class of this object value.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="6332f-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="6332f-104">Syntax</span></span>  
  
```cpp  
HRESULT GetClass (  
    [out] ICorDebugClass     **ppClass  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="6332f-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="6332f-105">Parameters</span></span>  

 `ppClass`  
 <span data-ttu-id="6332f-106">określoną Wskaźnik do adresu obiektu "ICorDebugClass", który reprezentuje klasę wartości obiektu reprezentowanej przez ten obiekt "ICorDebugObjectValue".</span><span class="sxs-lookup"><span data-stu-id="6332f-106">[out] A pointer to the address of an "ICorDebugClass" object that represents the class of the object value represented by this "ICorDebugObjectValue" object.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="6332f-107">Uwagi</span><span class="sxs-lookup"><span data-stu-id="6332f-107">Remarks</span></span>  

 <span data-ttu-id="6332f-108">`GetClass`Metody i [ICorDebugValue:: GetType](icordebugvalue-gettype-method.md) każda zwracają informacje o typie wartości; są one zastępowane przez ogólne [ICorDebugValue2:: GetExactType](icordebugvalue2-getexacttype-method.md).</span><span class="sxs-lookup"><span data-stu-id="6332f-108">The `GetClass` and [ICorDebugValue::GetType](icordebugvalue-gettype-method.md) methods each return information about the type of a value; they are both superseded by the generics-aware [ICorDebugValue2::GetExactType](icordebugvalue2-getexacttype-method.md).</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="6332f-109">Wymagania</span><span class="sxs-lookup"><span data-stu-id="6332f-109">Requirements</span></span>  

 <span data-ttu-id="6332f-110">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="6332f-110">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="6332f-111">**Nagłówek:** CorDebug. idl, CorDebug. h</span><span class="sxs-lookup"><span data-stu-id="6332f-111">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="6332f-112">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="6332f-112">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="6332f-113">**.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="6332f-113">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="6332f-114">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="6332f-114">See also</span></span>
