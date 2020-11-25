---
title: ICorDebugEval, interfejs
ms.date: 03/30/2017
api_name:
- ICorDebugEval
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugEval
helpviewer_keywords:
- ICorDebugEval interface [.NET Framework debugging]
ms.assetid: 3a5c9815-832d-47e1-b7f7-bbba135d7cf1
topic_type:
- apiref
ms.openlocfilehash: 5d8fd79b242f2b88b82c5c3d78dfe45d80f1194f
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95729788"
---
# <a name="icordebugeval-interface"></a>ICorDebugEval, interfejs

Dostarcza metody umożliwiające debugerowi wykonywanie kodu w kontekście debugowanego kodu.  
  
## <a name="methods"></a>Metody  
  
|Metoda|Opis|  
|------------|-----------------|  
|[Abort — Metoda](icordebugeval-abort-method.md)|Przerywa obliczenia wykonywane przez ten `ICorDebugEval` obiekt.|  
|[CallFunction, metoda](icordebugeval-callfunction-method.md)|Konfiguruje wywołanie do określonej funkcji. (Przestarzałe w .NET Framework w wersji 2,0; Użyj zamiast tego [ICorDebugEval2:: CallParameterizedFunction —](icordebugeval2-callparameterizedfunction-method.md) ).|  
|[CreateValue, metoda](icordebugeval-createvalue-method.md)|Pobiera wskaźnik interfejsu do obiektu "ICorDebugValue" określonego typu z początkową wartością zero lub null. (Przestarzałe w .NET Framework 2,0; Użyj zamiast tego [ICorDebugEval2:: CreateValueForType —](icordebugeval2-createvaluefortype-method.md) ).|  
|[GetResult, metoda](icordebugeval-getresult-method.md)|Pobiera wskaźnik interfejsu do obiektu `ICorDebugValue` , który zawiera wyniki obliczania.|  
|[GetThread, metoda](icordebugeval-getthread-method.md)|Pobiera wskaźnik interfejsu do elementu "ICorDebugThread", w którym ta Ocena wykonuje lub zostanie wykonana.|  
|[IsActive — Metoda](icordebugeval-isactive-method.md)|Pobiera wartość wskazującą, czy ten `ICorDebugEval` obiekt jest aktualnie wykonywany.|  
|[NewArray, metoda](icordebugeval-newarray-method.md)|Przypisuje nową tablicę określonego typu elementu i wymiarów. (Przestarzałe w .NET Framework 2,0; Użyj zamiast tego [ICorDebugEval2:: NewParameterizedArray —](icordebugeval2-newparameterizedarray-method.md) ).|  
|[NewObject, metoda](icordebugeval-newobject-method.md)|Przydziela nowe wystąpienie obiektu i wywołuje określoną metodę konstruktora. (Przestarzałe w .NET Framework 2,0; Użyj zamiast tego [ICorDebugEval2:: NewParameterizedObject —](icordebugeval2-newparameterizedobject-method.md) ).|  
|[NewObjectNoConstructor, metoda](icordebugeval-newobjectnoconstructor-method.md)|Przydziela nowe wystąpienie obiektu określonego typu, bez próby wywołania metody konstruktora. (Przestarzałe w .NET Framework 2,0; Użyj zamiast tego [ICorDebugEval2:: NewParameterizedObjectNoConstructor —](icordebugeval2-newparameterizedobjectnoconstructor-method.md) ).|  
|[NewString, metoda](icordebugeval-newstring-method.md)|Przypisuje nowy obiekt ciągu z określoną zawartością.|  
  
## <a name="remarks"></a>Uwagi  

 `ICorDebugEval`Obiekt jest tworzony w kontekście określonego wątku, który jest używany do wykonywania obliczeń. Wszystkie obiekty i typy używane w danej ocenie muszą znajdować się w tej samej domenie aplikacji. Ta domena aplikacji nie musi być taka sama, jak bieżąca domena aplikacji wątku. Obliczenia mogą być zagnieżdżane.  
  
 Operacje oceny nie zostaną ukończone, dopóki debuger nie wywoła [ICorDebugController:: Continue](icordebugcontroller-continue-method.md), a następnie odbiera wywołanie zwrotne [ICorDebugManagedCallback:: EvalComplete —](icordebugmanagedcallback-evalcomplete-method.md) . Jeśli konieczne jest użycie funkcji oceny bez zezwalania na uruchamianie innych wątków, należy wstrzymać wątki przy użyciu jednej z [ICorDebugController:: SetAllThreadsDebugState —](icordebugcontroller-setallthreadsdebugstate-method.md) lub [ICorDebugController:: Stop](icordebugcontroller-stop-method.md) przed wywołaniem [ICorDebugController:: Continue](icordebugcontroller-continue-method.md).  
  
 Ponieważ kod użytkownika jest uruchamiany, gdy trwa szacowanie, mogą wystąpić wszystkie zdarzenia debugowania, w tym obciążenia klas i punkty przerwania. Debuger otrzyma wywołania zwrotne, tak jak normalne, dla tych zdarzeń. Stan oceny będzie widoczny jako część inspekcji normalnego stanu programu. Łańcuch stosu będzie `CHAIN_FUNC_EVAL` łańcuchem (zobacz Wyliczenie "CorDebugStepReason —" i [ICorDebugChain:: getprzyczyna](icordebugchain-getreason-method.md) ). Interfejs API pełnego debugera będzie kontynuował normalne działanie.  
  
 Jeśli wystąpi zakleszczenie lub nieskończone sytuacje pętli, kod użytkownika może nigdy nie zostać ukończony. W takim przypadku należy wywołać [ICorDebugEval:: Abort](icordebugeval-abort-method.md) przed wznowieniem działania programu.  
  
> [!NOTE]
> Ten interfejs nie obsługuje wywoływania zdalnego na wielu maszynach ani wielu procesów.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorDebug. idl, CorDebug. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [Debugowanie — Interfejsy](debugging-interfaces.md)
