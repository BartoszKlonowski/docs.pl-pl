---
title: IMetaDataTables::GetBlob — Metoda
ms.date: 03/30/2017
api_name:
- IMetaDataTables.GetBlob
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataTables::GetBlob
helpviewer_keywords:
- GetBlob method [.NET Framework metadata]
- IMetaDataTables::GetBlob method [.NET Framework metadata]
ms.assetid: 94667c1c-6d58-4aa7-b74e-530b11e2a276
topic_type:
- apiref
ms.openlocfilehash: 32f32625ee40d50249ce3e009add543c4137b196
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95726473"
---
# <a name="imetadatatablesgetblob-method"></a><span data-ttu-id="c2b99-102">IMetaDataTables::GetBlob — Metoda</span><span class="sxs-lookup"><span data-stu-id="c2b99-102">IMetaDataTables::GetBlob Method</span></span>

<span data-ttu-id="c2b99-103">Pobiera wskaźnik do dużego obiektu binarnego (BLOB) w określonym indeksie kolumny.</span><span class="sxs-lookup"><span data-stu-id="c2b99-103">Gets a pointer to the binary large object (BLOB) at the specified column index.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="c2b99-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="c2b99-104">Syntax</span></span>  
  
```cpp  
HRESULT GetBlob (  
    [in]  ULONG          ixBlob,  
    [out] ULONG          *pcbData,  
    [out] const void     **ppData  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="c2b99-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="c2b99-105">Parameters</span></span>  

 `ixBlob`  
 <span data-ttu-id="c2b99-106">podczas Adres pamięci, z którego ma zostać pobrany `ppData` .</span><span class="sxs-lookup"><span data-stu-id="c2b99-106">[in] The memory address from which to get `ppData`.</span></span>  
  
 `pcbData`  
 <span data-ttu-id="c2b99-107">określoną Wskaźnik do rozmiaru, w bajtach, z `ppData` .</span><span class="sxs-lookup"><span data-stu-id="c2b99-107">[out] A pointer to the size, in bytes, of `ppData`.</span></span>  
  
 `ppData`  
 <span data-ttu-id="c2b99-108">określoną Pobrano wskaźnik do wskaźnika do danych binarnych.</span><span class="sxs-lookup"><span data-stu-id="c2b99-108">[out] A pointer to a pointer to the binary data retrieved.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="c2b99-109">Wymagania</span><span class="sxs-lookup"><span data-stu-id="c2b99-109">Requirements</span></span>  

 <span data-ttu-id="c2b99-110">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="c2b99-110">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="c2b99-111">**Nagłówek:** Cor. h</span><span class="sxs-lookup"><span data-stu-id="c2b99-111">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="c2b99-112">**Biblioteka:** Używane jako zasób w MsCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="c2b99-112">**Library:** Used as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="c2b99-113">**.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="c2b99-113">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="c2b99-114">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="c2b99-114">See also</span></span>

- [<span data-ttu-id="c2b99-115">IMetaDataTables — Interfejs</span><span class="sxs-lookup"><span data-stu-id="c2b99-115">IMetaDataTables Interface</span></span>](imetadatatables-interface.md)
- [<span data-ttu-id="c2b99-116">IMetaDataTables2 — Interfejs</span><span class="sxs-lookup"><span data-stu-id="c2b99-116">IMetaDataTables2 Interface</span></span>](imetadatatables2-interface.md)
