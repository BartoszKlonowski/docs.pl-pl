---
title: GetRequestedRuntimeVersion — Funkcja
ms.date: 03/30/2017
api_name:
- GetRequestedRuntimeVersion
api_location:
- mscoree.dll
- mscoreei.dll
api_type:
- DLLExport
f1_keywords:
- GetRequestedRuntimeVersion
helpviewer_keywords:
- GetRequestedRuntimeVersion function [.NET Framework hosting]
ms.assetid: 82f596a4-483d-4509-b0c5-a84c53c3da1b
topic_type:
- apiref
ms.openlocfilehash: 6c16b02a5ae323ba80d44937f322810022dfa9f5
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95711640"
---
# <a name="getrequestedruntimeversion-function"></a>GetRequestedRuntimeVersion — Funkcja

Pobiera numer wersji środowiska uruchomieniowego języka wspólnego (CLR) żądany przez określoną aplikację. Jeśli ta wersja nie jest zainstalowana, program pobierze najnowszą wersję, która jest zainstalowana przed żądaną wersją.  
  
 Ta funkcja jest przestarzała w .NET Framework 4.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT GetRequestedRuntimeVersion (  
    [in]  LPWSTR  pExe,
    [out] LPWSTR  pVersion,
    [in]  DWORD   cchBuffer,
    [out] DWORD  *pdwLength  
);  
```  
  
## <a name="parameters"></a>Parametry  

 `pExe`  
 podczas Nazwa aplikacji.  
  
 `pVersion`  
 określoną Bufor zawierający ciąg numeru wersji po pomyślnym zakończeniu.  
  
 `cchBuffer`  
 podczas Długość buforu wersji.  
  
 `pdwLength`  
 określoną Wskaźnik do długości ciągu numeru wersji.  
  
## <a name="return-value"></a>Wartość zwracana  

 Ta metoda zwraca kody błędów standardowego Component Object Model (COM), jak zdefiniowano w WinError. h, oprócz następujących wartości.  
  
|Kod powrotu|Opis|  
|-----------------|-----------------|  
|S_OK|Metoda została ukończona pomyślnie.|  
|ERROR_INSUFFICIENT_BUFFER|Bufor wersji nie jest wystarczająco duży, aby można było przechowywać ciąg wersji.|  
|E_POINTER|`pdwLength` ma wartość null.|  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** MSCorEE. h  
  
 **Biblioteka:** MSCorEE.dll  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v11plus](../../../../includes/net-current-v11plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [GetRequestedRuntimeInfo — Funkcja](getrequestedruntimeinfo-function.md)
- [GetVersionFromProcess — Funkcja](getversionfromprocess-function.md)
- [Przestarzałe funkcje hostingu środowiska CLR](deprecated-clr-hosting-functions.md)
