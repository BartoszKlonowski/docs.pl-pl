---
title: ICorDebugModule2::SetJMCStatus — Metoda
ms.date: 03/30/2017
api_name:
- ICorDebugModule2.SetJMCStatus
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugModule2::SetJMCStatus
helpviewer_keywords:
- SetJMCStatus method, ICorDebugModule2 interface [.NET Framework debugging]
- ICorDebugModule2::SetJMCStatus method [.NET Framework debugging]
ms.assetid: 8c6d2089-4dbb-4715-b9e9-2a4491c8c9ce
topic_type:
- apiref
ms.openlocfilehash: cfa6df7a812559f05a4c57381a5007c9c90238e1
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95709657"
---
# <a name="icordebugmodule2setjmcstatus-method"></a><span data-ttu-id="05f3f-102">ICorDebugModule2::SetJMCStatus — Metoda</span><span class="sxs-lookup"><span data-stu-id="05f3f-102">ICorDebugModule2::SetJMCStatus Method</span></span>

<span data-ttu-id="05f3f-103">Ustawia stan Tylko mój kod (JMC) dla wszystkich metod wszystkich klas w tym ICorDebugModule2 do określonej wartości, z wyjątkiem tych w `pTokens` tablicy, które są ustawiane na wartość odwrotną.</span><span class="sxs-lookup"><span data-stu-id="05f3f-103">Sets the Just My Code (JMC) status of all methods of all the classes in this ICorDebugModule2 to the specified value, except those in the `pTokens` array, which it sets to the opposite value.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="05f3f-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="05f3f-104">Syntax</span></span>  
  
```cpp  
HRESULT SetJMCStatus (  
    [in] BOOL                        bIsJustMyCode,  
    [in] ULONG32                     cTokens,  
    [in, size_is(cTokens)] mdToken   pTokens[]  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="05f3f-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="05f3f-105">Parameters</span></span>  

 `bIsJustMycode`  
 <span data-ttu-id="05f3f-106">podczas Ustaw na `true` , jeśli kod ma być debugowany; w przeciwnym razie ustaw wartość `false` .</span><span class="sxs-lookup"><span data-stu-id="05f3f-106">[in] Set to `true` if the code is to be debugged; otherwise, set to `false`.</span></span>  
  
 `cTokens`  
 <span data-ttu-id="05f3f-107">podczas Rozmiar `pTokens` tablicy.</span><span class="sxs-lookup"><span data-stu-id="05f3f-107">[in] The size of the `pTokens` array.</span></span>  
  
 `pTokens`  
 <span data-ttu-id="05f3f-108">podczas Tablica `mdToken` wartości, z których każdy odwołuje się do metody, która ma ustawiony stan JMC! `bIsJustMycode` .</span><span class="sxs-lookup"><span data-stu-id="05f3f-108">[in] An array of `mdToken` values, each of which refers to a method that will have its JMC status set to !`bIsJustMycode`.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="05f3f-109">Uwagi</span><span class="sxs-lookup"><span data-stu-id="05f3f-109">Remarks</span></span>  

 <span data-ttu-id="05f3f-110">Stan JMC każdej metody określonej w `pTokens` tablicy jest ustawiony na odwrotność `bIsJustMycode` wartości.</span><span class="sxs-lookup"><span data-stu-id="05f3f-110">The JMC status of each method that is specified in the `pTokens` array is set to the opposite of the `bIsJustMycode` value.</span></span> <span data-ttu-id="05f3f-111">Stan wszystkich innych metod w tym module jest ustawiony na `bIsJustMycode` wartość.</span><span class="sxs-lookup"><span data-stu-id="05f3f-111">The status of all other methods in this module is set to the `bIsJustMycode` value.</span></span>  
  
 <span data-ttu-id="05f3f-112">`SetJMCStatus`Metoda powoduje wymazanie wszystkich poprzednich ustawień JMC w tym module.</span><span class="sxs-lookup"><span data-stu-id="05f3f-112">The `SetJMCStatus` method erases all previous JMC settings in this module.</span></span>  
  
 <span data-ttu-id="05f3f-113">`SetJMCStatus`Metoda zwraca S_OK HRESULT, jeśli wszystkie funkcje zostały ustawione pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="05f3f-113">The `SetJMCStatus` method returns an S_OK HRESULT if all functions were set successfully.</span></span> <span data-ttu-id="05f3f-114">Zwraca CORDBG_E_FUNCTION_NOT_DEBUGGABLE HRESULT, jeśli niektóre funkcje, które są oznaczone, `true` nie są możliwością debugowania.</span><span class="sxs-lookup"><span data-stu-id="05f3f-114">It returns a CORDBG_E_FUNCTION_NOT_DEBUGGABLE HRESULT if some functions that are marked `true` are not debuggable.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="05f3f-115">Wymagania</span><span class="sxs-lookup"><span data-stu-id="05f3f-115">Requirements</span></span>  

 <span data-ttu-id="05f3f-116">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="05f3f-116">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="05f3f-117">**Nagłówek:** CorDebug. idl, CorDebug. h</span><span class="sxs-lookup"><span data-stu-id="05f3f-117">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="05f3f-118">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="05f3f-118">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="05f3f-119">**.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="05f3f-119">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>
