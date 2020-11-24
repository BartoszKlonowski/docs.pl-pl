---
title: IMetaDataImport::EnumMethodImpls — Metoda
ms.date: 03/30/2017
api_name:
- IMetaDataImport.EnumMethodImpls
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::EnumMethodImpls
helpviewer_keywords:
- EnumMethodImpls method [.NET Framework metadata]
- IMetaDataImport::EnumMethodImpls method [.NET Framework metadata]
ms.assetid: 4e0f865d-88b5-44bd-be35-492622e5e08e
topic_type:
- apiref
ms.openlocfilehash: 40ab610110e96018b1c598d04b24a762ecb50717
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95690520"
---
# <a name="imetadataimportenummethodimpls-method"></a><span data-ttu-id="64e17-102">IMetaDataImport::EnumMethodImpls — Metoda</span><span class="sxs-lookup"><span data-stu-id="64e17-102">IMetaDataImport::EnumMethodImpls Method</span></span>

<span data-ttu-id="64e17-103">Wylicza tokeny MethodBody i MethodDeclaration reprezentujące metody określonego typu.</span><span class="sxs-lookup"><span data-stu-id="64e17-103">Enumerates MethodBody and MethodDeclaration tokens representing methods of the specified type.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="64e17-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="64e17-104">Syntax</span></span>  
  
```cpp  
HRESULT EnumMethodImpls (  
   [in, out] HCORENUM    *phEnum,
   [in]      mdTypeDef   td,
   [out]     mdToken     rMethodBody[],
   [out]     mdToken     rMethodDecl[],
   [in]      ULONG       cMax,
   [in]      ULONG       *pcTokens  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="64e17-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="64e17-105">Parameters</span></span>  

 `phEnum`  
 <span data-ttu-id="64e17-106">[in. out] Wskaźnik do modułu wyliczającego.</span><span class="sxs-lookup"><span data-stu-id="64e17-106">[in, out] A pointer to the enumerator.</span></span> <span data-ttu-id="64e17-107">Musi ona mieć wartość NULL dla pierwszego wywołania tej metody.</span><span class="sxs-lookup"><span data-stu-id="64e17-107">This must be NULL for the first call of this method.</span></span>  
  
 `td`  
 <span data-ttu-id="64e17-108">podczas Token TypeDef dla typu, którego implementacje metod mają zostać wyliczone.</span><span class="sxs-lookup"><span data-stu-id="64e17-108">[in] A TypeDef token for the type whose method implementations to enumerate.</span></span>  
  
 `rMethodBody`  
 <span data-ttu-id="64e17-109">określoną Tablica do przechowywania tokenów MethodBody.</span><span class="sxs-lookup"><span data-stu-id="64e17-109">[out] The array to store the MethodBody tokens.</span></span>  
  
 `rMethodDecl`  
 <span data-ttu-id="64e17-110">określoną Tablica do przechowywania tokenów MethodDeclaration.</span><span class="sxs-lookup"><span data-stu-id="64e17-110">[out] The array to store the MethodDeclaration tokens.</span></span>  
  
 `cMax`  
 <span data-ttu-id="64e17-111">podczas Maksymalny rozmiar `rMethodBody` `rMethodDecl` tablic i.</span><span class="sxs-lookup"><span data-stu-id="64e17-111">[in] The maximum size of the `rMethodBody` and `rMethodDecl` arrays.</span></span>  
  
 `pcTokens`  
 <span data-ttu-id="64e17-112">podczas Rzeczywista liczba metod zwróconych w `rMethodBody` i `rMethodDecl` .</span><span class="sxs-lookup"><span data-stu-id="64e17-112">[in] The actual number of methods returned in `rMethodBody` and `rMethodDecl`.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="64e17-113">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="64e17-113">Return Value</span></span>  
  
|<span data-ttu-id="64e17-114">HRESULT</span><span class="sxs-lookup"><span data-stu-id="64e17-114">HRESULT</span></span>|<span data-ttu-id="64e17-115">Opis</span><span class="sxs-lookup"><span data-stu-id="64e17-115">Description</span></span>|  
|-------------|-----------------|  
|`S_OK`|<span data-ttu-id="64e17-116">`EnumMethodImpls` pomyślnie zwrócono.</span><span class="sxs-lookup"><span data-stu-id="64e17-116">`EnumMethodImpls` returned successfully.</span></span>|  
|`S_FALSE`|<span data-ttu-id="64e17-117">Brak tokenów metody do wyliczenia.</span><span class="sxs-lookup"><span data-stu-id="64e17-117">There are no method tokens to enumerate.</span></span> <span data-ttu-id="64e17-118">W takim przypadku `pcTokens` jest równa zero.</span><span class="sxs-lookup"><span data-stu-id="64e17-118">In that case, `pcTokens` is zero.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="64e17-119">Wymagania</span><span class="sxs-lookup"><span data-stu-id="64e17-119">Requirements</span></span>  

 <span data-ttu-id="64e17-120">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="64e17-120">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="64e17-121">**Nagłówek:** Cor. h</span><span class="sxs-lookup"><span data-stu-id="64e17-121">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="64e17-122">**Biblioteka:** Uwzględnione jako zasób w MsCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="64e17-122">**Library:** Included as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="64e17-123">**.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="64e17-123">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="64e17-124">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="64e17-124">See also</span></span>

- [<span data-ttu-id="64e17-125">IMetaDataImport — Interfejs</span><span class="sxs-lookup"><span data-stu-id="64e17-125">IMetaDataImport Interface</span></span>](imetadataimport-interface.md)
- [<span data-ttu-id="64e17-126">IMetaDataImport2 — Interfejs</span><span class="sxs-lookup"><span data-stu-id="64e17-126">IMetaDataImport2 Interface</span></span>](imetadataimport2-interface.md)
