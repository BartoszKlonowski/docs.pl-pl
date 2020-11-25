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
# <a name="icoreclrdebugtargetfreememory-method"></a>ICoreClrDebugTarget::FreeMemory — Metoda

Zwalnia pamięć przydzieloną przez metody [ICoreClrDebugTarget:: EnumProcesses —](icoreclrdebugtarget-enumprocesses-method.md) i [ICoreClrDebugTarget:: EnumRuntimes —](icoreclrdebugtarget-enumruntimes-method.md) .  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
void FreeMemory (  
     [in] void*pMemory);  
```  
  
## <a name="parameters"></a>Parametry  

 `pMemory`  
 podczas Wskaźnik do tablicy, który jest zwracany przez metodę [ICoreClrDebugTarget:: EnumProcesses —](icoreclrdebugtarget-enumprocesses-method.md) lub [ICoreClrDebugTarget:: EnumRuntimes —](icoreclrdebugtarget-enumruntimes-method.md) .  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CoreClrRemoteDebuggingInterfaces. h  
  
 **Biblioteka:** mscordbi_macx86.dll  
  
 **.NET Framework wersje:** 3,5 SP1  
  
## <a name="see-also"></a>Zobacz także

- [ICoreClrDebugTarget — Interfejs](icoreclrdebugtarget-interface.md)
