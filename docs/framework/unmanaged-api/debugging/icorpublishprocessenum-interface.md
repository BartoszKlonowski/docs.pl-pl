---
title: ICorPublishProcessEnum — Interfejs
ms.date: 03/30/2017
api_name:
- ICorPublishProcessEnum
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorPublishProcessEnum
helpviewer_keywords:
- ICorPublishProcessEnum interface [.NET Framework debugging]
ms.assetid: aac8fcf9-ac09-437c-bd5c-2fda14ae1007
topic_type:
- apiref
ms.openlocfilehash: ebf484524b32d8e917d88c21425fab314dfc41be
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95692621"
---
# <a name="icorpublishprocessenum-interface"></a>ICorPublishProcessEnum — Interfejs

Podklasa interfejsu [ICorPublishEnum](icorpublishenum-interface.md) , która dostarcza metody umożliwiające przechodzenie kolekcji obiektów [ICorPublishProcess](icorpublishprocess-interface.md) .  
  
## <a name="methods"></a>Metody  
  
|Metoda|Opis|  
|------------|-----------------|  
|[Next, metoda](icorpublishprocessenum-next-method.md)|Pobiera określoną liczbę `ICorPublishProcess` wystąpień z kolekcji, rozpoczynając od bieżącego położenia.|  
  
## <a name="remarks"></a>Uwagi  

 `ICorPublishProcessEnum`Interfejs implementuje metody interfejsu abstrakcyjnego, [ICorPublishEnum](icorpublishenum-interface.md).  
  
 `ICorPublishProcessEnum`Wystąpienie jest tworzone przez metodę [ICorPublish:: EnumProcesses —](icorpublish-enumprocesses-method.md) . Przechodzenie kolekcji `ICorPublishProcess` obiektów jest oparte na kryteriach filtrowania określonych w momencie `ICorPublishProcessEnum` utworzenia wystąpienia.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorPub. idl, CorPub. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [Debugowanie — Interfejsy](debugging-interfaces.md)
- [CorpubPublish — Klasa coclass](corpubpublish-coclass.md)
