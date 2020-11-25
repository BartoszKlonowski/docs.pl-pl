---
title: ICorDebugFunction::GetNativeCode — Metoda
ms.date: 03/30/2017
api_name:
- ICorDebugFunction.GetNativeCode
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugFunction::GetNativeCode
helpviewer_keywords:
- GetNativeCode method [.NET Framework debugging]
- ICorDebugFunction::GetNativeCode method [.NET Framework debugging]
ms.assetid: c8a34916-0eef-4987-8d29-c8bcb4be9cf6
topic_type:
- apiref
ms.openlocfilehash: e34dff2ebdb6e1ea56c2682b351c3e17a44416f3
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95726317"
---
# <a name="icordebugfunctiongetnativecode-method"></a>ICorDebugFunction::GetNativeCode — Metoda

Pobiera kod natywny dla funkcji reprezentowanej przez to wystąpienie ICorDebugFunction.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT GetNativeCode (  
    [out] ICorDebugCode **ppCode  
);  
```  
  
## <a name="parameters"></a>Parametry  

 `ppCode`  
 określoną Wskaźnik do wystąpienia ICorDebugCode, który reprezentuje kod natywny dla tej funkcji, lub wartość null, jeśli ta funkcja jest kodem języka pośredniego firmy Microsoft (MSIL), który nie został skompilowany jako just-in-Time (JIT).  
  
## <a name="remarks"></a>Uwagi  

 Jeśli funkcja reprezentowana przez to wystąpienie została skompilowana w trybie `ICorDebugFunction` JIT więcej niż raz, jak w przypadku typów ogólnych, `GetNativeCode` zwraca losowy obiekt kodu natywnego.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorDebug. idl, CorDebug. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
