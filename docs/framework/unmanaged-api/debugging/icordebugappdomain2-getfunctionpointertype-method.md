---
title: ICorDebugAppDomain2::GetFunctionPointerType — Metoda
ms.date: 03/30/2017
api_name:
- ICorDebugAppDomain2.GetFunctionPointerType
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugAppDomain2::GetFunctionPointerType
helpviewer_keywords:
- ICorDebugAppDomain2::GetFunctionPointerType method [.NET Framework debugging]
- GetFunctionPointerType method [.NET Framework debugging]
ms.assetid: 0aba6096-5b38-435c-a72a-86d35db4daef
topic_type:
- apiref
ms.openlocfilehash: be797b1b3f288fd367d7f624e9cf33015dd114ac
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95698276"
---
# <a name="icordebugappdomain2getfunctionpointertype-method"></a><span data-ttu-id="13b9d-102">ICorDebugAppDomain2::GetFunctionPointerType — Metoda</span><span class="sxs-lookup"><span data-stu-id="13b9d-102">ICorDebugAppDomain2::GetFunctionPointerType Method</span></span>

<span data-ttu-id="13b9d-103">Pobiera wskaźnik do funkcji, która ma daną sygnaturę.</span><span class="sxs-lookup"><span data-stu-id="13b9d-103">Gets a pointer to a function that has a given signature.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="13b9d-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="13b9d-104">Syntax</span></span>  
  
```cpp  
HRESULT GetFunctionPointerType (  
    [in] ULONG32                             nTypeArgs,  
    [in, size_is(nTypeArgs)] ICorDebugType   *ppTypeArgs[],  
    [out] ICorDebugType                      **ppType  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="13b9d-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="13b9d-105">Parameters</span></span>  

 `nTypeArgs`  
 <span data-ttu-id="13b9d-106">podczas Liczba argumentów typu dla funkcji.</span><span class="sxs-lookup"><span data-stu-id="13b9d-106">[in] The number of type arguments for the function.</span></span>  
  
 `ppTypeArgs`  
 <span data-ttu-id="13b9d-107">podczas Tablica wskaźników, z których każdy wskazuje obiekt ICorDebugType, który reprezentuje argument typu funkcji.</span><span class="sxs-lookup"><span data-stu-id="13b9d-107">[in] An array of pointers, each of which points to an ICorDebugType object that represents a type argument of the function.</span></span> <span data-ttu-id="13b9d-108">Pierwszy element jest typem zwracanym; Każdy z pozostałych elementów jest typem parametru.</span><span class="sxs-lookup"><span data-stu-id="13b9d-108">The first element is the return type; each of the other elements is a parameter type.</span></span>  
  
 `ppType`  
 <span data-ttu-id="13b9d-109">określoną Wskaźnik do adresu `ICorDebugType` obiektu, który reprezentuje wskaźnik do funkcji.</span><span class="sxs-lookup"><span data-stu-id="13b9d-109">[out] A pointer to the address of an `ICorDebugType` object that represents the pointer to the function.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="13b9d-110">Wymagania</span><span class="sxs-lookup"><span data-stu-id="13b9d-110">Requirements</span></span>  

 <span data-ttu-id="13b9d-111">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="13b9d-111">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="13b9d-112">**Nagłówek:** CorDebug. idl, CorDebug. h</span><span class="sxs-lookup"><span data-stu-id="13b9d-112">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="13b9d-113">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="13b9d-113">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="13b9d-114">**.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="13b9d-114">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>
