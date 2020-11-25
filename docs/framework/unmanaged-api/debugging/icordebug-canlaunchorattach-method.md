---
title: ICorDebug::CanLaunchOrAttach — Metoda
ms.date: 03/30/2017
api_name:
- ICorDebug.CanLaunchOrAttach
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebug::CanLaunchOrAttach
helpviewer_keywords:
- ICorDebug::CanLaunchOrAttach method [.NET Framework debugging]
- CanLaunchOrAttach method [.NET Framework debugging]
ms.assetid: ca7723db-7c07-4cdd-bd92-fba34928b623
topic_type:
- apiref
ms.openlocfilehash: 195c7e1e7c61fd6ac8a21226b52e3782d2f7e421
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95723496"
---
# <a name="icordebugcanlaunchorattach-method"></a><span data-ttu-id="29cad-102">ICorDebug::CanLaunchOrAttach — Metoda</span><span class="sxs-lookup"><span data-stu-id="29cad-102">ICorDebug::CanLaunchOrAttach Method</span></span>

<span data-ttu-id="29cad-103">Zwraca wartość HRESULT wskazującą, czy uruchomienie nowego procesu lub dołączenie do określonego istniejącego procesu jest możliwe w kontekście bieżącego komputera i konfiguracji środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="29cad-103">Returns an HRESULT that indicates whether launching a new process or attaching to the specified existing process is possible within the context of the current machine and runtime configuration.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="29cad-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="29cad-104">Syntax</span></span>  
  
```cpp  
HRESULT CanLaunchOrAttach (  
    [in] DWORD      dwProcessId,  
    [in] BOOL       win32DebuggingEnabled  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="29cad-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="29cad-105">Parameters</span></span>  

 `dwProcessId`  
 <span data-ttu-id="29cad-106">podczas Identyfikator istniejącego procesu.</span><span class="sxs-lookup"><span data-stu-id="29cad-106">[in] The ID of an existing process.</span></span>  
  
 `win32DebuggingEnabled`  
 <span data-ttu-id="29cad-107">podczas Zastąp `true` , jeśli planujesz uruchamianie z włączonym debugowaniem Win32 lub dołączanie z włączonym debugowaniem Win32; w przeciwnym razie Przekaż `false` .</span><span class="sxs-lookup"><span data-stu-id="29cad-107">[in] Pass in `true` if you plan to launch with Win32 debugging enabled, or to attach with Win32 debugging enabled; otherwise, pass `false`.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="29cad-108">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="29cad-108">Return Value</span></span>  

 <span data-ttu-id="29cad-109">S_OK, jeśli usługa debugowania określi, że uruchomienie nowego procesu lub dołączenie do danego procesu jest możliwe, z uwzględnieniem informacji o bieżącym komputerze i konfiguracji środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="29cad-109">S_OK if the debugging services determine that launching a new process or attaching to the given process is possible, given the information about the current machine and runtime configuration.</span></span> <span data-ttu-id="29cad-110">Możliwe wartości HRESULT to:</span><span class="sxs-lookup"><span data-stu-id="29cad-110">Possible HRESULT values are:</span></span>  
  
- <span data-ttu-id="29cad-111">S_OK</span><span class="sxs-lookup"><span data-stu-id="29cad-111">S_OK</span></span>  
  
- <span data-ttu-id="29cad-112">CORDBG_E_DEBUGGING_NOT_POSSIBLE</span><span class="sxs-lookup"><span data-stu-id="29cad-112">CORDBG_E_DEBUGGING_NOT_POSSIBLE</span></span>  
  
- <span data-ttu-id="29cad-113">CORDBG_E_KERNEL_DEBUGGER_PRESENT</span><span class="sxs-lookup"><span data-stu-id="29cad-113">CORDBG_E_KERNEL_DEBUGGER_PRESENT</span></span>  
  
- <span data-ttu-id="29cad-114">CORDBG_E_KERNEL_DEBUGGER_ENABLED</span><span class="sxs-lookup"><span data-stu-id="29cad-114">CORDBG_E_KERNEL_DEBUGGER_ENABLED</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="29cad-115">Uwagi</span><span class="sxs-lookup"><span data-stu-id="29cad-115">Remarks</span></span>  

 <span data-ttu-id="29cad-116">Ta metoda ma charakter czysty informacyjny.</span><span class="sxs-lookup"><span data-stu-id="29cad-116">This method is purely informational.</span></span> <span data-ttu-id="29cad-117">Interfejs nie zatrzymuje uruchamiania lub dołączania do procesu, niezależnie od wartości zwracanej przez `CanLaunchOrAttach` .</span><span class="sxs-lookup"><span data-stu-id="29cad-117">The interface will not stop you from launching or attaching to a process, regardless of the value returned by `CanLaunchOrAttach`.</span></span>  
  
 <span data-ttu-id="29cad-118">Jeśli planujesz uruchamianie z włączonym debugowaniem Win32 lub Dołącz z włączonym debugowaniem Win32, Przekaż `true` `win32DebuggingEnabled` .</span><span class="sxs-lookup"><span data-stu-id="29cad-118">If you plan to launch with Win32 debugging enabled or attach with Win32 debugging enabled, pass `true` for `win32DebuggingEnabled`.</span></span> <span data-ttu-id="29cad-119">Wartość HRESULT zwracaną przez `CanLaunchOrAttach` może się różnić w przypadku użycia tej opcji.</span><span class="sxs-lookup"><span data-stu-id="29cad-119">The HRESULT returned by `CanLaunchOrAttach` might differ if you use this option.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="29cad-120">Wymagania</span><span class="sxs-lookup"><span data-stu-id="29cad-120">Requirements</span></span>  

 <span data-ttu-id="29cad-121">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="29cad-121">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="29cad-122">**Nagłówek:** CorDebug. idl, CorDebug. h</span><span class="sxs-lookup"><span data-stu-id="29cad-122">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="29cad-123">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="29cad-123">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="29cad-124">**.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="29cad-124">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="29cad-125">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="29cad-125">See also</span></span>

- [<span data-ttu-id="29cad-126">ICorDebug — Interfejs</span><span class="sxs-lookup"><span data-stu-id="29cad-126">ICorDebug Interface</span></span>](icordebug-interface.md)
