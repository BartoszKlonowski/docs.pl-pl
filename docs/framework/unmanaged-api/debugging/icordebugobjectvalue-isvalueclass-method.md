---
title: ICorDebugObjectValue::IsValueClass — Metoda
ms.date: 03/30/2017
api_name:
- ICorDebugObjectValue.IsValueClass
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugObjectValue::IsValueClass
helpviewer_keywords:
- ICorDebugObjectValue::IsValueClass method [.NET Framework debugging]
- IsValueClass method [.NET Framework debugging]
ms.assetid: 13d89a4a-5d9d-4a79-9600-5e2a98c3d166
topic_type:
- apiref
ms.openlocfilehash: 7b637889986425767fd7e1166c73df3301075422
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95695286"
---
# <a name="icordebugobjectvalueisvalueclass-method"></a><span data-ttu-id="12004-102">ICorDebugObjectValue::IsValueClass — Metoda</span><span class="sxs-lookup"><span data-stu-id="12004-102">ICorDebugObjectValue::IsValueClass Method</span></span>

<span data-ttu-id="12004-103">Pobiera wartość wskazującą, czy ta wartość obiektu jest typem wartości.</span><span class="sxs-lookup"><span data-stu-id="12004-103">Gets a value that indicates whether this object value is a value type.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="12004-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="12004-104">Syntax</span></span>  
  
```cpp  
HRESULT IsValueClass (  
    [out] BOOL               *pbIsValueClass  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="12004-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="12004-105">Parameters</span></span>  

 `pbIsValueClass`  
 <span data-ttu-id="12004-106">określoną Wskaźnik do wartości logicznej, która jest `true` , jeśli wartość obiektu, reprezentowana przez ten "ICorDebugObjectValue", jest typem wartości, a nie typem referencyjnym; w przeciwnym razie `pbIsValueClass` jest `false` .</span><span class="sxs-lookup"><span data-stu-id="12004-106">[out] A pointer to a Boolean value that is `true` if the object value, represented by this "ICorDebugObjectValue", is a value type rather than a reference type; otherwise, `pbIsValueClass` is `false`.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="12004-107">Wymagania</span><span class="sxs-lookup"><span data-stu-id="12004-107">Requirements</span></span>  

 <span data-ttu-id="12004-108">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="12004-108">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="12004-109">**Nagłówek:** CorDebug. idl, CorDebug. h</span><span class="sxs-lookup"><span data-stu-id="12004-109">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="12004-110">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="12004-110">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="12004-111">**.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="12004-111">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="12004-112">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="12004-112">See also</span></span>
