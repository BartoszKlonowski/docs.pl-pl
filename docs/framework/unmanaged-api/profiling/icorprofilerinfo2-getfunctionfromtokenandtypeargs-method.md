---
title: ICorProfilerInfo2::GetFunctionFromTokenAndTypeArgs — Metoda
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo2.GetFunctionFromTokenAndTypeArgs
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo2::GetFunctionFromTokenAndTypeArgs
helpviewer_keywords:
- ICorProfilerInfo2::GetFunctionFromTokenAndTypeArgs method [.NET Framework profiling]
- GetFunctionFromTokenAndTypeArgs method [.NET Framework profiling]
ms.assetid: ce8f6aa6-4ebf-4a86-b429-4bbc8af41a8f
topic_type:
- apiref
ms.openlocfilehash: 17a6220598010c0bee9c3f0485860aa0b2dc5f3a
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95727110"
---
# <a name="icorprofilerinfo2getfunctionfromtokenandtypeargs-method"></a>ICorProfilerInfo2::GetFunctionFromTokenAndTypeArgs — Metoda

Pobiera `FunctionID` funkcję przy użyciu określonego tokenu metadanych, zawierającego klasę i `ClassID` wartości dowolnego argumentu typu.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT GetFunctionFromTokenAndTypeArgs(  
    [in] ModuleID moduleID,  
    [in] mdMethodDef funcDef,  
    [in] ClassID classId,  
    [in] ULONG32 cTypeArgs,  
    [in, size_is(cTypeArgs)] ClassID typeArgs[],  
    [out] FunctionID* pFunctionID);  
```  
  
## <a name="parameters"></a>Parametry  

 `moduleID`  
 podczas Identyfikator modułu, w którym znajduje się funkcja.  
  
 `funcDef`  
 podczas `mdMethodDef` Token metadanych, który odwołuje się do funkcji.  
  
 `classId`  
 podczas Identyfikator klasy zawierającej funkcję.  
  
 `cTypeArgs`  
 podczas Liczba parametrów typu dla danej funkcji. Ta wartość musi być równa zero w przypadku funkcji innych niż ogólne.  
  
 `typeArgs`  
 podczas Tablica `ClassID` wartości, z których każdy jest argumentem funkcji. Wartość `typeArgs` może być równa null, jeśli `cTypeArgs` jest ustawiona na zero.  
  
 `pFunctionID`  
 określoną Wskaźnik do `FunctionID` określonej funkcji.  
  
## <a name="remarks"></a>Uwagi  

 Wywołanie `GetFunctionFromTokenAndTypeArgs` metody z `mdMethodRef` metadanymi zamiast `mdMethodDef` tokenu metadanych może mieć nieprzewidywalne wyniki. Podczas przekazywania obiekty wywołujące powinny rozwiązać ten problem `mdMethodRef` `mdMethodDef` .  
  
 Jeśli funkcja nie jest już załadowana, wywołanie `GetFunctionFromTokenAndTypeArgs` spowoduje wystąpienie załadowania, które jest niebezpieczną operacją w wielu kontekstach. Na przykład wywołanie tej metody podczas ładowania modułów lub typów może prowadzić do nieskończonej pętli, ponieważ środowisko uruchomieniowe próbuje cyklicznie ładować elementy.  
  
 Ogólnie rzecz biorąc, użycie `GetFunctionFromTokenAndTypeArgs` nie jest zalecane. Jeśli zainteresują Cię zdarzenia dotyczące konkretnej funkcji, powinny one przechowywać `ModuleID` i tej `mdMethodDef` funkcji, a następnie używać [ICorProfilerInfo2:: GetFunctionInfo2 —](icorprofilerinfo2-getfunctioninfo2-method.md) , aby sprawdzić, czy dana jest dana `FunctionID` żądana funkcja.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorProf. idl, CorProf. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [ICorProfilerInfo — Interfejs](icorprofilerinfo-interface.md)
- [ICorProfilerInfo2 — Interfejs](icorprofilerinfo2-interface.md)
