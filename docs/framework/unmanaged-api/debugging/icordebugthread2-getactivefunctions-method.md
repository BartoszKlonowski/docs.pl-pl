---
title: ICorDebugThread2::GetActiveFunctions — Metoda
ms.date: 03/30/2017
api_name:
- ICorDebugThread2.GetActiveFunctions
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread2::GetActiveFunctions
helpviewer_keywords:
- GetActiveFunctions method [.NET Framework debugging]
- ICorDebugThread2::GetActiveFunctions method [.NET Framework debugging]
ms.assetid: 27fae01a-ecec-423a-973e-24f8de55826c
topic_type:
- apiref
ms.openlocfilehash: 2d5674d6b5962ca539de02cda1e5658daed83622
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95678756"
---
# <a name="icordebugthread2getactivefunctions-method"></a><span data-ttu-id="9dba4-102">ICorDebugThread2::GetActiveFunctions — Metoda</span><span class="sxs-lookup"><span data-stu-id="9dba4-102">ICorDebugThread2::GetActiveFunctions Method</span></span>

<span data-ttu-id="9dba4-103">Pobiera informacje o aktywnej funkcji w poszczególnych ramkach tego wątku.</span><span class="sxs-lookup"><span data-stu-id="9dba4-103">Gets information about the active function in each of this thread's frames.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="9dba4-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="9dba4-104">Syntax</span></span>  
  
```cpp  
HRESULT GetActiveFunctions (  
    [in]   ULONG32             cFunctions,  
    [out]  ULONG32             *pcFunctions,  
    [in, out, size_is(cFunctions), length_is(*pcFunctions)]  
        COR_ACTIVE_FUNCTION    pFunctions[]  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="9dba4-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="9dba4-105">Parameters</span></span>  

 `cFunctions`  
 <span data-ttu-id="9dba4-106">podczas Rozmiar `pFunctions` tablicy.</span><span class="sxs-lookup"><span data-stu-id="9dba4-106">[in] The size of the `pFunctions` array.</span></span>  
  
 `pcFunctions`  
 <span data-ttu-id="9dba4-107">określoną Wskaźnik do liczby obiektów zwracanych w `pFunctions` tablicy.</span><span class="sxs-lookup"><span data-stu-id="9dba4-107">[out] A pointer to the number of objects returned in the `pFunctions` array.</span></span> <span data-ttu-id="9dba4-108">Liczba zwracanych obiektów będzie równa liczbie zarządzanych ramek na stosie.</span><span class="sxs-lookup"><span data-stu-id="9dba4-108">The number of objects returned will be equal to the number of managed frames on the stack.</span></span>  
  
 `pFunctions`  
 <span data-ttu-id="9dba4-109">[in. out] Tablica obiektów COR_ACTIVE_FUNCTION, z których każdy zawiera informacje o aktywnych funkcjach w ramkach tego wątku.</span><span class="sxs-lookup"><span data-stu-id="9dba4-109">[in, out] An array of COR_ACTIVE_FUNCTION objects, each of which contains information about the active functions in this thread's frames.</span></span>  
  
 <span data-ttu-id="9dba4-110">Pierwszy element zostanie użyty dla ramki liścia i tak dalej, jak z powrotem do korzenia stosu.</span><span class="sxs-lookup"><span data-stu-id="9dba4-110">The first element will be used for the leaf frame, and so on back to the root of the stack.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="9dba4-111">Uwagi</span><span class="sxs-lookup"><span data-stu-id="9dba4-111">Remarks</span></span>  

 <span data-ttu-id="9dba4-112">Jeśli wartość `pFunctions` jest równa null, `GetActiveFunctions` zwraca tylko liczbę funkcji, które znajdują się na stosie.</span><span class="sxs-lookup"><span data-stu-id="9dba4-112">If `pFunctions` is null on input, `GetActiveFunctions` returns only the number of functions that are on the stack.</span></span> <span data-ttu-id="9dba4-113">Oznacza to, że jeśli `pFunctions` wartość jest równa null przy wejściu, `GetActiveFunctions` Funkcja zwraca tylko wartości w `pcFunctions` .</span><span class="sxs-lookup"><span data-stu-id="9dba4-113">That is, If `pFunctions` is null on input, `GetActiveFunctions` returns a value only in `pcFunctions`.</span></span>  
  
 <span data-ttu-id="9dba4-114">`GetActiveFunctions`Metoda jest przeznaczona do optymalizacji nad uzyskaniem tych samych informacji z ramek w ślad stosu i zawiera tylko ramki, które miały obiekt ICorDebugILFrame dla nich w pełnym śladzie stosu.</span><span class="sxs-lookup"><span data-stu-id="9dba4-114">The `GetActiveFunctions` method is intended as an optimization over getting the same information from frames in a stack trace, and includes only frames that would have had an ICorDebugILFrame object for them in the full stack trace.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="9dba4-115">Wymagania</span><span class="sxs-lookup"><span data-stu-id="9dba4-115">Requirements</span></span>  

 <span data-ttu-id="9dba4-116">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="9dba4-116">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="9dba4-117">**Nagłówek:** CorDebug. idl, CorDebug. h</span><span class="sxs-lookup"><span data-stu-id="9dba4-117">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="9dba4-118">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="9dba4-118">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="9dba4-119">**.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="9dba4-119">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>
