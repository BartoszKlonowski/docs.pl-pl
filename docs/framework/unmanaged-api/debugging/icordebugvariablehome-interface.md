---
title: ICorDebugVariableHome, interfejs
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- ICorDebugVariableHome
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugVariableHome
helpviewer_keywords:
- ICorDebugVariableHome interface [.NET Framework debugging]
ms.assetid: 76f2bf3b-759f-4eed-bce7-119415b25915
topic_type:
- apiref
ms.openlocfilehash: 089e68278113dfdf509ed848f424ad32baa145ed
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95679549"
---
# <a name="icordebugvariablehome-interface"></a><span data-ttu-id="2fd70-102">ICorDebugVariableHome, interfejs</span><span class="sxs-lookup"><span data-stu-id="2fd70-102">ICorDebugVariableHome Interface</span></span>

<span data-ttu-id="2fd70-103">Reprezentuje zmienną lokalną lub argument funkcji.</span><span class="sxs-lookup"><span data-stu-id="2fd70-103">Represents a local variable or argument of a function.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="2fd70-104">Metody</span><span class="sxs-lookup"><span data-stu-id="2fd70-104">Methods</span></span>  
  
|<span data-ttu-id="2fd70-105">Metoda</span><span class="sxs-lookup"><span data-stu-id="2fd70-105">Method</span></span>|<span data-ttu-id="2fd70-106">Opis</span><span class="sxs-lookup"><span data-stu-id="2fd70-106">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="2fd70-107">GetArgumentIndex, metoda</span><span class="sxs-lookup"><span data-stu-id="2fd70-107">GetArgumentIndex Method</span></span>](icordebugvariablehome-getargumentindex-method.md)|<span data-ttu-id="2fd70-108">Pobiera indeks argumentu funkcji.</span><span class="sxs-lookup"><span data-stu-id="2fd70-108">Gets the index of a function argument.</span></span>|  
|[<span data-ttu-id="2fd70-109">GetCode, metoda</span><span class="sxs-lookup"><span data-stu-id="2fd70-109">GetCode Method</span></span>](icordebugvariablehome-getcode-method.md)|<span data-ttu-id="2fd70-110">Pobiera wystąpienie "ICorDebugCode", które zawiera ten `ICorDebugVariableHome` obiekt.</span><span class="sxs-lookup"><span data-stu-id="2fd70-110">Gets the "ICorDebugCode" instance that contains this `ICorDebugVariableHome` object.</span></span>|  
|[<span data-ttu-id="2fd70-111">GetLiveRange, metoda</span><span class="sxs-lookup"><span data-stu-id="2fd70-111">GetLiveRange Method</span></span>](icordebugvariablehome-getliverange-method.md)|<span data-ttu-id="2fd70-112">Pobiera natywny zakres, w którym znajduje się ta zmienna.</span><span class="sxs-lookup"><span data-stu-id="2fd70-112">Gets the native range over which this variable is live.</span></span>|  
|[<span data-ttu-id="2fd70-113">GetLocationType, metoda</span><span class="sxs-lookup"><span data-stu-id="2fd70-113">GetLocationType Method</span></span>](icordebugvariablehome-getlocationtype-method.md)|<span data-ttu-id="2fd70-114">Pobiera typ lokalizacji natywnej zmiennej.</span><span class="sxs-lookup"><span data-stu-id="2fd70-114">Gets the type of the variable's native location.</span></span>|  
|[<span data-ttu-id="2fd70-115">GetOffset — Metoda</span><span class="sxs-lookup"><span data-stu-id="2fd70-115">GetOffset Method</span></span>](icordebugvariablehome-getoffset-method.md)|<span data-ttu-id="2fd70-116">Pobiera przesunięcie z rejestru podstawowego dla zmiennej.</span><span class="sxs-lookup"><span data-stu-id="2fd70-116">Gets the offset from the base register for a variable.</span></span>|  
|[<span data-ttu-id="2fd70-117">GetRegister, metoda</span><span class="sxs-lookup"><span data-stu-id="2fd70-117">GetRegister Method</span></span>](icordebugvariablehome-getregister-method.md)|<span data-ttu-id="2fd70-118">Pobiera rejestr zawierający zmienną z typem lokalizacji `VLT_REGISTER` i rejestr podstawowy dla zmiennej z typem lokalizacji `VLT_REGISTER_RELATIVE` .</span><span class="sxs-lookup"><span data-stu-id="2fd70-118">Gets the register that contains a variable with a location type of `VLT_REGISTER`, and the base register for a variable with a location type of `VLT_REGISTER_RELATIVE`.</span></span>|  
|[<span data-ttu-id="2fd70-119">GetSlotIndex, metoda</span><span class="sxs-lookup"><span data-stu-id="2fd70-119">GetSlotIndex Method</span></span>](icordebugvariablehome-getslotindex-method.md)|<span data-ttu-id="2fd70-120">Pobiera zarządzany indeks szczeliny zmiennej lokalnej.</span><span class="sxs-lookup"><span data-stu-id="2fd70-120">Gets the managed slot-index of a local variable.</span></span>|  
  
## <a name="example"></a><span data-ttu-id="2fd70-121">Przykład</span><span class="sxs-lookup"><span data-stu-id="2fd70-121">Example</span></span>  

 <span data-ttu-id="2fd70-122">Poniższy fragment kodu używa obiektu [ICorDebugCode4](icordebugcode4-interface.md) o nazwie `pCode4` .</span><span class="sxs-lookup"><span data-stu-id="2fd70-122">The following code fragment uses the [ICorDebugCode4](icordebugcode4-interface.md) object named `pCode4`.</span></span>  
  
```cpp  
ICorDebugCode4 *pCode4 = NULL;  
pCode->QueryInterface(IID_ICorDebugCode4, &pCode4);  
  
ICorDebugVariableEnum *pVarLocEnum = NULL;  
pCode4->EnumerateVariableHomes(&pVarLocEnum);  
  
// retrieve local variables and arguments  
ULONG celt = 0;  
pVarLocEnum->GetCount(&celt);  
ICorDebugVariableHome **homes = new ICorDebugVariableHome *[celt];  
ULONG celtFetched = 0;  
pVarLocEnum->Next(celt, homes, &celtFetched);  
  
for (int i = 0; i < celtFetched; i++)  
{  
    VariableLocationType locType = VLT_INVALID;  
    homes[i].GetLocationType(&locType);  
    switch (locType)  
    {  
    case VLT_REGISTER:  
        CorDebugRegister register = 0;  
        locals[i].GetRegister(&register);  
        // now we know which register it is in  
        break;  
    case VLT_REGISTER_RELATIVE:  
        CorDebugRegister baseRegister = 0;  
        LONG offset = 0;  
        locals[i].GetRegister(&register);  
        locals[i].GetOffset(&offset);  
        // now we know the register-relative offset  
        break;  
    case VLT_INVALID:  
        // handle case where we can't access the location  
        break;  
    }  
}  
```  
  
## <a name="requirements"></a><span data-ttu-id="2fd70-123">Wymagania</span><span class="sxs-lookup"><span data-stu-id="2fd70-123">Requirements</span></span>  

 <span data-ttu-id="2fd70-124">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="2fd70-124">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="2fd70-125">**Nagłówek:** CorDebug. idl, CorDebug. h</span><span class="sxs-lookup"><span data-stu-id="2fd70-125">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="2fd70-126">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="2fd70-126">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="2fd70-127">**.NET Framework wersje:**[!INCLUDE[net_current_v462plus](../../../../includes/net-current-v462plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="2fd70-127">**.NET Framework Versions:** [!INCLUDE[net_current_v462plus](../../../../includes/net-current-v462plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="2fd70-128">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="2fd70-128">See also</span></span>

- [<span data-ttu-id="2fd70-129">Debugowanie — Interfejsy</span><span class="sxs-lookup"><span data-stu-id="2fd70-129">Debugging Interfaces</span></span>](debugging-interfaces.md)
- [<span data-ttu-id="2fd70-130">ICorDebugVariableHomeEnum, interfejs</span><span class="sxs-lookup"><span data-stu-id="2fd70-130">ICorDebugVariableHomeEnum Interface</span></span>](icordebugvariablehomeenum-interface.md)
