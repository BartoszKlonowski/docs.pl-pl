---
title: ICorDebugClass, interfejs
ms.date: 03/30/2017
api_name:
- ICorDebugClass
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugClass
helpviewer_keywords:
- ICorDebugClass interface [.NET Framework debugging]
ms.assetid: 03a6facb-f12f-49be-9839-e73b9c791cd5
topic_type:
- apiref
ms.openlocfilehash: 4f488741f4233f06c128e0a262ce798ef27af3ff
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95699641"
---
# <a name="icordebugclass-interface"></a><span data-ttu-id="a4a68-102">ICorDebugClass, interfejs</span><span class="sxs-lookup"><span data-stu-id="a4a68-102">ICorDebugClass Interface</span></span>

<span data-ttu-id="a4a68-103">Reprezentuje typ, który może być podstawowy lub złożony (to jest zdefiniowany przez użytkownika).</span><span class="sxs-lookup"><span data-stu-id="a4a68-103">Represents a type, which can be either basic or complex (that is, user-defined).</span></span> <span data-ttu-id="a4a68-104">Jeśli typ jest ogólny, `ICorDebugClass` reprezentuje typ ogólny bez wystąpień.</span><span class="sxs-lookup"><span data-stu-id="a4a68-104">If the type is generic, `ICorDebugClass` represents the uninstantiated generic type.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="a4a68-105">Metody</span><span class="sxs-lookup"><span data-stu-id="a4a68-105">Methods</span></span>  
  
|<span data-ttu-id="a4a68-106">Metoda</span><span class="sxs-lookup"><span data-stu-id="a4a68-106">Method</span></span>|<span data-ttu-id="a4a68-107">Opis</span><span class="sxs-lookup"><span data-stu-id="a4a68-107">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="a4a68-108">GetModule — Metoda</span><span class="sxs-lookup"><span data-stu-id="a4a68-108">GetModule Method</span></span>](icordebugclass-getmodule-method.md)|<span data-ttu-id="a4a68-109">Pobiera moduł, który definiuje tę klasę.</span><span class="sxs-lookup"><span data-stu-id="a4a68-109">Gets the module that defines this class.</span></span>|  
|[<span data-ttu-id="a4a68-110">GetStaticFieldValue, metoda</span><span class="sxs-lookup"><span data-stu-id="a4a68-110">GetStaticFieldValue Method</span></span>](icordebugclass-getstaticfieldvalue-method.md)|<span data-ttu-id="a4a68-111">Pobiera wartość określonego pola statycznego.</span><span class="sxs-lookup"><span data-stu-id="a4a68-111">Gets the value of the specified static field.</span></span>|  
|[<span data-ttu-id="a4a68-112">GetToken — Metoda</span><span class="sxs-lookup"><span data-stu-id="a4a68-112">GetToken Method</span></span>](icordebugclass-gettoken-method.md)|<span data-ttu-id="a4a68-113">Pobiera `TypeDef` token metadanych dla tej klasy.</span><span class="sxs-lookup"><span data-stu-id="a4a68-113">Gets the `TypeDef` metadata token for this class.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="a4a68-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="a4a68-114">Remarks</span></span>  

 <span data-ttu-id="a4a68-115">`ICorDebugClass`Interfejs reprezentuje typ ogólny bez wystąpień.</span><span class="sxs-lookup"><span data-stu-id="a4a68-115">The `ICorDebugClass` interface represents an uninstantiated generic type.</span></span> <span data-ttu-id="a4a68-116">Interfejs ICorDebugType reprezentuje typ ogólny skonkretyzowany.</span><span class="sxs-lookup"><span data-stu-id="a4a68-116">The ICorDebugType interface represents an instantiated generic type.</span></span> <span data-ttu-id="a4a68-117">Na przykład `Hashtable<K, V>` byłyby reprezentowane przez `ICorDebugClass` , a `Hashtable<Int32, String>` byłyby reprezentowane przez `ICorDebugType` .</span><span class="sxs-lookup"><span data-stu-id="a4a68-117">For example, `Hashtable<K, V>` would be represented by `ICorDebugClass`, whereas `Hashtable<Int32, String>` would be represented by `ICorDebugType`.</span></span>  
  
 <span data-ttu-id="a4a68-118">Typy inne niż ogólne są reprezentowane przez `ICorDebugClass` i `ICorDebugType` .</span><span class="sxs-lookup"><span data-stu-id="a4a68-118">Non-generic types are represented by both `ICorDebugClass` and `ICorDebugType`.</span></span> <span data-ttu-id="a4a68-119">Ten ostatni interfejs został wprowadzony w .NET Framework w wersji 2,0, aby można było zająć się tworzeniem wystąpienia typu.</span><span class="sxs-lookup"><span data-stu-id="a4a68-119">The latter interface was introduced in the .NET Framework version 2.0 to deal with type instantiation.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="a4a68-120">Ten interfejs nie obsługuje wywoływania zdalnego na wielu maszynach ani wielu procesów.</span><span class="sxs-lookup"><span data-stu-id="a4a68-120">This interface does not support being called remotely, either cross-machine or cross-process.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="a4a68-121">Wymagania</span><span class="sxs-lookup"><span data-stu-id="a4a68-121">Requirements</span></span>  

 <span data-ttu-id="a4a68-122">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="a4a68-122">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="a4a68-123">**Nagłówek:** CorDebug. idl, CorDebug. h</span><span class="sxs-lookup"><span data-stu-id="a4a68-123">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="a4a68-124">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="a4a68-124">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="a4a68-125">**.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="a4a68-125">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a4a68-126">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="a4a68-126">See also</span></span>

- [<span data-ttu-id="a4a68-127">Debugowanie — Interfejsy</span><span class="sxs-lookup"><span data-stu-id="a4a68-127">Debugging Interfaces</span></span>](debugging-interfaces.md)
