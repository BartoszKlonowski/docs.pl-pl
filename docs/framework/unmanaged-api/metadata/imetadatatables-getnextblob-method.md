---
title: IMetaDataTables::GetNextBlob — Metoda
ms.date: 03/30/2017
api_name:
- IMetaDataTables.GetNextBlob
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataTables::GetNextBlob
helpviewer_keywords:
- IMetaDataTables::GetNextBlob method [.NET Framework metadata]
- GetNextBlob method [.NET Framework metadata]
ms.assetid: 017c8ab4-4c09-4754-9935-5b0b49cabecb
topic_type:
- apiref
ms.openlocfilehash: ba694f485d5a51870a1283b6ccbcb7b042a14501
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95685646"
---
# <a name="imetadatatablesgetnextblob-method"></a><span data-ttu-id="36b05-102">IMetaDataTables::GetNextBlob — Metoda</span><span class="sxs-lookup"><span data-stu-id="36b05-102">IMetaDataTables::GetNextBlob Method</span></span>

<span data-ttu-id="36b05-103">Pobiera indeks następnego obiektu binarnego (BLOB) z tabeli.</span><span class="sxs-lookup"><span data-stu-id="36b05-103">Gets the index of the next binary large object (BLOB) in the table.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="36b05-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="36b05-104">Syntax</span></span>  
  
```cpp  
HRESULT GetNextBlob (  
    [in]  ULONG   ixBlob,  
    [out] ULONG   *pNext  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="36b05-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="36b05-105">Parameters</span></span>  

 `ixBlob`  
 <span data-ttu-id="36b05-106">podczas Indeks zwrócony z kolumny obiektów BLOB.</span><span class="sxs-lookup"><span data-stu-id="36b05-106">[in] The index, as returned from a column of BLOBs.</span></span>  
  
 `pNext`  
 <span data-ttu-id="36b05-107">określoną Wskaźnik do indeksu następnego obiektu BLOB.</span><span class="sxs-lookup"><span data-stu-id="36b05-107">[out] A pointer to the index of the next BLOB.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="36b05-108">Wymagania</span><span class="sxs-lookup"><span data-stu-id="36b05-108">Requirements</span></span>  

 <span data-ttu-id="36b05-109">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="36b05-109">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="36b05-110">**Nagłówek:** Cor. h</span><span class="sxs-lookup"><span data-stu-id="36b05-110">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="36b05-111">**Biblioteka:** Używane jako zasób w MsCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="36b05-111">**Library:** Used as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="36b05-112">**.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="36b05-112">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="36b05-113">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="36b05-113">See also</span></span>

- [<span data-ttu-id="36b05-114">IMetaDataTables — Interfejs</span><span class="sxs-lookup"><span data-stu-id="36b05-114">IMetaDataTables Interface</span></span>](imetadatatables-interface.md)
- [<span data-ttu-id="36b05-115">IMetaDataTables2 — Interfejs</span><span class="sxs-lookup"><span data-stu-id="36b05-115">IMetaDataTables2 Interface</span></span>](imetadatatables2-interface.md)
