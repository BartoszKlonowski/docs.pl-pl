---
title: LPTHREAD_START_ROUTINE — Wskaźnik funkcji
ms.date: 03/30/2017
api_name:
- LPTHREAD_START_ROUTINE
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- LPTHREAD_START_ROUTINE
helpviewer_keywords:
- LPTHREAD_START_ROUTINE function pointer [.NET Framework hosting]
ms.assetid: 7b9b93b0-fe92-42ba-8693-701168a29dde
topic_type:
- apiref
ms.openlocfilehash: c86b65e136869603f93253678108b2ffa9d388e1
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95730074"
---
# <a name="lpthread_start_routine-function-pointer"></a><span data-ttu-id="41515-102">LPTHREAD_START_ROUTINE — Wskaźnik funkcji</span><span class="sxs-lookup"><span data-stu-id="41515-102">LPTHREAD_START_ROUTINE Function Pointer</span></span>

<span data-ttu-id="41515-103">Wskazuje funkcję, która powiadamia hosta o rozpoczęciu wykonywania wątku.</span><span class="sxs-lookup"><span data-stu-id="41515-103">Points to a function that notifies the host that a thread has started to execute.</span></span>  
  
 <span data-ttu-id="41515-104">Ten wskaźnik funkcji został uznany za przestarzały w .NET Framework 4.</span><span class="sxs-lookup"><span data-stu-id="41515-104">This function pointer has been deprecated in the .NET Framework 4.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="41515-105">Składnia</span><span class="sxs-lookup"><span data-stu-id="41515-105">Syntax</span></span>  
  
```cpp  
typedef DWORD (__stdcall *LPTHREAD_START_ROUTINE) (  
    [in] LPVOID lpThreadParameter  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="41515-106">Parametry</span><span class="sxs-lookup"><span data-stu-id="41515-106">Parameters</span></span>  

 `lpThreadParameter`  
 <span data-ttu-id="41515-107">podczas Wskaźnik do kodu, który rozpoczął wykonywanie.</span><span class="sxs-lookup"><span data-stu-id="41515-107">[in] A pointer to the code that has started executing.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="41515-108">Uwagi</span><span class="sxs-lookup"><span data-stu-id="41515-108">Remarks</span></span>  

 <span data-ttu-id="41515-109">Funkcja, do której `LPTHREAD_START_ROUTINE` punkty jest funkcją wywołania zwrotnego i musi być implementowana przez moduł zapisujący aplikacji hostingowej.</span><span class="sxs-lookup"><span data-stu-id="41515-109">The function to which `LPTHREAD_START_ROUTINE` points is a callback function and must be implemented by the writer of the hosting application.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="41515-110">Wymagania</span><span class="sxs-lookup"><span data-stu-id="41515-110">Requirements</span></span>  

 <span data-ttu-id="41515-111">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="41515-111">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="41515-112">**Nagłówek:** MSCorEE. h</span><span class="sxs-lookup"><span data-stu-id="41515-112">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="41515-113">**Biblioteka:** MSCorWks.dll</span><span class="sxs-lookup"><span data-stu-id="41515-113">**Library:** MSCorWks.dll</span></span>  
  
 <span data-ttu-id="41515-114">**.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="41515-114">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="41515-115">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="41515-115">See also</span></span>

- [<span data-ttu-id="41515-116">Przestarzałe funkcje hostingu środowiska CLR</span><span class="sxs-lookup"><span data-stu-id="41515-116">Deprecated CLR Hosting Functions</span></span>](deprecated-clr-hosting-functions.md)
