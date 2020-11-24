---
title: ICorPublishProcess::EnumAppDomains — Metoda
ms.date: 03/30/2017
api_name:
- ICorPublishProcess.EnumAppDomains
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorPublishProcess::EnumAppDomains
helpviewer_keywords:
- EnumAppDomains method [.NET Framework debugging]
- ICorPublishProcess::EnumAppDomains method [.NET Framework debugging]
ms.assetid: 7da621fc-e7d0-4c00-9439-5c93619d7414
topic_type:
- apiref
ms.openlocfilehash: 2acf8fb507ab617e066a31c9c2657b1ef0d18e47
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95693284"
---
# <a name="icorpublishprocessenumappdomains-method"></a>ICorPublishProcess::EnumAppDomains — Metoda

Pobiera moduł wyliczający dla domen aplikacji w procesie, do którego odwołuje się ten [ICorPublishProcess](icorpublishprocess-interface.md).  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT EnumAppDomains (  
    [out] ICorPublishAppDomainEnum   **ppEnum  
);  
```  
  
## <a name="parameters"></a>Parametry  

 `ppEnum`  
 określoną Wskaźnik do adresu wystąpienia [ICorPublishAppDomainEnum](icorpublishappdomainenum-interface.md) , który umożliwia iterację w kolekcji domen aplikacji w tym procesie.  
  
## <a name="remarks"></a>Uwagi  

 Lista domen aplikacji jest oparta na migawce domen aplikacji, które istnieją podczas `EnumAppDomains` wywoływania metody. Ta metoda może być wywoływana więcej niż raz w celu utworzenia nowej listy aktualnych danych. Kolejne wywołania tej metody nie będą miały wpływ na istniejące listy.  
  
 Jeśli proces został zakończony, zakończy `EnumAppDomains` się niepowodzeniem z wartością HRESULT równą CORDBG_E_PROCESS_TERMINATED.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorPub. idl, CorPub. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [ICorPublishProcess — Interfejs](icorpublishprocess-interface.md)
