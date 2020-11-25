---
title: CoEEShutDownCOM — Funkcja
ms.date: 03/30/2017
api_name:
- CoEEShutDownCOM
api_location:
- mscoree.dll
- clr.dll
- mscorwks.dll
- mscoreei.dll
- mscorsvr.dll
api_type:
- DLLExport
f1_keywords:
- CoEEShutDownCOM
helpviewer_keywords:
- CoEEShutDownCOM function [.NET Framework hosting]
ms.assetid: b634cae2-632f-4737-9be4-92d0652844d7
topic_type:
- apiref
ms.openlocfilehash: 774704698f92d546d6bafa61c65d18d083c65f89
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95716762"
---
# <a name="coeeshutdowncom-function"></a>CoEEShutDownCOM — Funkcja

Wymusza, aby środowisko uruchomieniowe języka wspólnego (CLR) zwolnił wszystkie wskaźniki interfejsu, które znajdują się wewnątrz wywoływanych otok (RCW) środowiska uruchomieniowego. Ma to wpływ na zwalnianie wszystkich pamięci podręcznych OTOKi. Ta funkcja globalna jest przestarzała w .NET Framework 4. Zamiast tego należy użyć punktu wejścia dla określonego środowiska uruchomieniowego.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
void CoEEShutDownCOM ();  
```  
  
## <a name="remarks"></a>Uwagi  

 `CoEEShutDownCOM`Funkcja najpierw zwalnia wszystkie RCW we wszystkich kontekstach i we wszystkich pamięciach podręcznych, a następnie usuwa wszelkie powiadomienia o rozrywaniu istniejące w instalatorze. Brak wyładowywania biblioteki DLL.  
  
> [!CAUTION]
> Ta funkcja ma wpływ na wszystkie środowiska uruchomieniowe, które są ładowane do procesu.  
  
 Począwszy od .NET Framework 4, wywołaj punkt wejścia dla tej funkcji w konkretnym środowisku uruchomieniowym, którego chcesz dotyczyć. Aby uzyskać punkt wejścia, wywołaj metodę [ICLRRuntimeInfo:: GetProcAddress](iclrruntimeinfo-getprocaddress-method.md) i określ wartość "CoEEShutDownCOM —".  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** Cor. h  
  
 **Biblioteka:** Uwzględnione jako zasób w MsCorEE.dll  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [Statyczne funkcje globalne metadanych](../metadata/metadata-global-static-functions.md)
