---
title: ISymUnmanagedAsyncMethodPropertiesWriter — Interfejs
ms.date: 03/30/2017
ms.assetid: caa71820-8058-4b6a-93a2-25ee757d92d3
ms.openlocfilehash: 779b737da43f61d1023a0a640dce936e11c4704c
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95707038"
---
# <a name="isymunmanagedasyncmethodpropertieswriter-interface"></a>ISymUnmanagedAsyncMethodPropertiesWriter — Interfejs

Umożliwia zdefiniowanie opcjonalnych informacji o metodzie asynchronicznej dla każdego symbolu metody. Zawsze używaj z otwartą metodą; oznacza to, między wywołaniami [metody OpenMethod —](isymunmanagedwriter-openmethod-method.md) i [CloseMethod —](isymunmanagedwriter-closemethod-method.md).  
  
## <a name="syntax"></a>Składnia  
  
```idl  
[object,uuid(FC073774-1739-4232-BD56-A027294BEC15),pointer_default(unique)]interface ISymUnmanagedAsyncMethodPropertiesWriter : IUnknown  
```  
  
## <a name="methods"></a>Metody  

 Ten interfejs zawiera następujące metody:  
  
|Metoda|Opis|  
|------------|-----------------|  
|[DefineAsyncStepInfo, metoda](isymunmanagedasyncmethodpropertieswriter-defineasyncstepinfo-method.md)|Zdefiniuj grupę asynchronicznych operacji await w bieżącej metodzie.<br /><br /> Każde przesunięcie Yield pasuje do instrukcji return oczekującej, identyfikując potencjalną rentowność. Każda `breakpointMethod` / `breakpointOffset` para identyfikuje lokalizację operacji asynchronicznej, która może być w innej metodzie.|  
|[DefineCatchHandlerILOffset, metoda](isymunmanagedasyncmethodpropertieswriter-definecatchhandleriloffset-method.md)|Ustawia przesunięcie IL dla wygenerowanego przez kompilator procedury obsługi catch, która otacza metodę asynchroniczną.<br /><br /> Przesunięcie IL wygenerowanego catch jest używane przez debuger do obsługi catch tak, jakby był kodem innym niż użytkownik, nawet jeśli może wystąpić w metodzie kodu użytkownika. W szczególności jest używany w odpowiedzi na zdarzenie wyjątku **CatchHandlerFound** .|  
|[DefineKickoffMethod, metoda](isymunmanagedasyncmethodpropertieswriter-definekickoffmethod-method.md)|Ustawia metodę początkową inicjującą operację asynchroniczną.|  
  
## <a name="requirements"></a>Wymagania  

 **Nagłówek:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Zobacz także

- [Interfejsy magazynu symboli diagnostycznych](diagnostics-symbol-store-interfaces.md)
