---
title: COR_GC_STATS — Struktura
ms.date: 03/30/2017
api_name:
- COR_GC_STATS
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- COR_GC_STATS
helpviewer_keywords:
- COR_GC_STATS structure [.NET Framework hosting]
ms.assetid: 8d4ff73e-739b-40f6-9349-359fbc99c2f9
topic_type:
- apiref
ms.openlocfilehash: 53a70c53a06ac55a2dab7c646018d63189ee0b36
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95726226"
---
# <a name="cor_gc_stats-structure"></a>COR_GC_STATS — Struktura

Zawiera dane statystyczne dotyczące mechanizmu odzyskiwania pamięci środowiska uruchomieniowego języka wspólnego (CLR).  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
typedef struct _COR_GC_STATS {  
    ULONG   Flags;
    SIZE_T  ExplicitGCCount;  
    SIZE_T  GenCollectionsTaken[3];  
    SIZE_T  CommittedKBytes;
    SIZE_T  ReservedKBytes;  
    SIZE_T  Gen0HeapSizeKBytes;  
    SIZE_T  Gen1HeapSizeKBytes;  
    SIZE_T  Gen2HeapSizeKBytes;  
    SIZE_T  LargeObjectHeapSizeKBytes;  
    SIZE_T  KBytesPromotedFromGen0;  
    SIZE_T  KBytesPromotedFromGen1;  
} COR_GC_STATS;  
```  
  
## <a name="members"></a>Elementy członkowskie  
  
|Członek|Opis|  
|------------|-----------------|  
|`Flags`|Wskazuje, które wartości pól należy obliczyć i zwrócić.|  
|`ExplicitGCCount`|Wskazuje liczbę wyrzucania elementów bezużytecznych, które zostały wymuszone przez żądanie zewnętrzne.|  
|`GenCollectionsTaken`|Wskazuje liczbę wyrzucania elementów bezużytecznych wykonanych dla każdej generacji.|  
|`CommittedKBytes`|Łączna liczba kilobajtów zakontraktowanych we wszystkich stertach.|  
|`ReservedKBytes`|Łączna liczba kilobajtów zarezerwowanych na wszystkie sterty.|  
|`Gen0HeapSizeKBytes`|Rozmiar sterty generacji — w kilobajtach.|  
|`Gen1HeapSizeKBytes`|Rozmiar (w kilobajtach) sterty generacji.|  
|`Gen2HeapSizeKBytes`|Rozmiar (w kilobajtach) sterty generacji-2.|  
|`LargeObjectHeapSizeKBytes`|Rozmiar sterty dużego obiektu (w kilobajtach).|  
|`KBytesPromotedFromGen0`|Rozmiar (w kilobajtach) obiektów, które zostały podwyższenie poziomu generacji zero w celu wygenerowania jednej.|  
|`KBytesPromotedFromGen1`|Rozmiar (w kilobajtach) obiektów awansowanych od generacji jednej do generacji dwóch.|  
  
## <a name="remarks"></a>Uwagi  

 Metoda [ICLRGCManager::](iclrgcmanager-getstats-method.md) getstatistics wymaga, aby `Flags` pole `COR_GC_STATS` struktury było ustawione na co najmniej jedną wartość wyliczenia [COR_GC_STAT_TYPES](cor-gc-stat-types-enumeration.md) , aby określić, które statystyki mają być ustawione.  
  
 Poniższa tabela zawiera mapy statystyk dostarczonych przez tę strukturę do dwóch [COR_GC_STAT_TYPES](cor-gc-stat-types-enumeration.md) wartości wyliczenia `COR_GC_COUNTS` i `COR_GC_MEMORYUSAGE` .  
  
|Określone przez COR_GC_COUNTS|Określone przez COR_GC_MEMORYUSAGE|  
|----------------------------------|---------------------------------------|  
|`ExplicitGCCount`<br /><br /> `GenCollectionsTaken`|`CommittedKBytes`<br /><br /> `ReservedKBytes`<br /><br /> `Gen0HeapSizeKBytes`<br /><br /> `Gen1HeapSizeKBytes`<br /><br /> `Gen2HeapSizeKBytes`<br /><br /> `LargeObjectHeapSizeKBytes`<br /><br /> `KBytesPromotedFromGen0`<br /><br /> `KBytesPromotedFromGen1`|  
  
 Przykładem użycia jest następujący:  
  
```cpp  
COR_GC_STATS GCStats;  
GCStats.Flags = COR_GC_COUNTS | COR_GC_MEMORYUSAGE;  
pCLRGCManager->GetStats(&GCStats);  
```  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** GCHost. idl  
  
 **Biblioteka:** Uwzględnione jako zasób w MSCorEE.dll  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [Hosting — Struktury](hosting-structures.md)
- [Automatyczne zarządzanie pamięcią](../../../standard/automatic-memory-management.md)
- [Odzyskiwanie pamięci](../../../standard/garbage-collection/index.md)
