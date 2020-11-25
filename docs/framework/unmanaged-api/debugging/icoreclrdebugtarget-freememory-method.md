---
title: ICoreClrDebugTarget::FreeMemory — Metoda
ms.date: 03/30/2017
api_name:
- ICoreDebugTarget.FreeMemory
api_location:
- mscordbi_macx86.dll
api_type:
- COM
f1_keywords:
- ICoreClrDebugTarget::FreeMemory
helpviewer_keywords:
- remote debugging API [Silverlight]
- FreeMemory method, ICoreClrDebugTarget interface [Silverlight debugging]
- ICorClrDebugTarget::FreeMemory method [Silverlight debugging]
- Silverlight, remote debugging
ms.assetid: 98f2a0db-a6ec-4f9b-861d-f82485237d08
topic_type:
- apiref
ms.openlocfilehash: 1e159cacd297d56d63e512643ec4d3fe0c3709c0
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95694405"
---
# <a name="icoreclrdebugtargetfreememory-method"></a><span data-ttu-id="bf5d2-102">ICoreClrDebugTarget::FreeMemory — Metoda</span><span class="sxs-lookup"><span data-stu-id="bf5d2-102">ICoreClrDebugTarget::FreeMemory Method</span></span>

<span data-ttu-id="bf5d2-103">Zwalnia pamięć przydzieloną przez metody [ICoreClrDebugTarget:: EnumProcesses —](icoreclrdebugtarget-enumprocesses-method.md) i [ICoreClrDebugTarget:: EnumRuntimes —](icoreclrdebugtarget-enumruntimes-method.md) .</span><span class="sxs-lookup"><span data-stu-id="bf5d2-103">Frees the memory allocated by the [ICoreClrDebugTarget::EnumProcesses](icoreclrdebugtarget-enumprocesses-method.md) and [ICoreClrDebugTarget::EnumRuntimes](icoreclrdebugtarget-enumruntimes-method.md) methods.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="bf5d2-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="bf5d2-104">Syntax</span></span>  
  
```cpp  
void FreeMemory (  
     [in] void*pMemory);  
```  
  
## <a name="parameters"></a><span data-ttu-id="bf5d2-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="bf5d2-105">Parameters</span></span>  

 `pMemory`  
 <span data-ttu-id="bf5d2-106">podczas Wskaźnik do tablicy, który jest zwracany przez metodę [ICoreClrDebugTarget:: EnumProcesses —](icoreclrdebugtarget-enumprocesses-method.md) lub [ICoreClrDebugTarget:: EnumRuntimes —](icoreclrdebugtarget-enumruntimes-method.md) .</span><span class="sxs-lookup"><span data-stu-id="bf5d2-106">[in] A pointer to the array that is returned by either the [ICoreClrDebugTarget::EnumProcesses](icoreclrdebugtarget-enumprocesses-method.md) or the [ICoreClrDebugTarget::EnumRuntimes](icoreclrdebugtarget-enumruntimes-method.md) method.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="bf5d2-107">Wymagania</span><span class="sxs-lookup"><span data-stu-id="bf5d2-107">Requirements</span></span>  

 <span data-ttu-id="bf5d2-108">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="bf5d2-108">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="bf5d2-109">**Nagłówek:** CoreClrRemoteDebuggingInterfaces. h</span><span class="sxs-lookup"><span data-stu-id="bf5d2-109">**Header:** CoreClrRemoteDebuggingInterfaces.h</span></span>  
  
 <span data-ttu-id="bf5d2-110">**Biblioteka:** mscordbi_macx86.dll</span><span class="sxs-lookup"><span data-stu-id="bf5d2-110">**Library:** mscordbi_macx86.dll</span></span>  
  
 <span data-ttu-id="bf5d2-111">**.NET Framework wersje:** 3,5 SP1</span><span class="sxs-lookup"><span data-stu-id="bf5d2-111">**.NET Framework Versions:** 3.5 SP1</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="bf5d2-112">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="bf5d2-112">See also</span></span>

- [<span data-ttu-id="bf5d2-113">ICoreClrDebugTarget — Interfejs</span><span class="sxs-lookup"><span data-stu-id="bf5d2-113">ICoreClrDebugTarget Interface</span></span>](icoreclrdebugtarget-interface.md)
