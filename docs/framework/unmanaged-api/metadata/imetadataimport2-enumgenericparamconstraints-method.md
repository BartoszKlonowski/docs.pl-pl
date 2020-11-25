---
title: IMetaDataImport2::EnumGenericParamConstraints — Metoda
ms.date: 03/30/2017
api_name:
- IMetaDataImport2.EnumGenericParamConstraints
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport2::EnumGenericParamConstraints
helpviewer_keywords:
- EnumGenericParamConstraints method [.NET Framework metadata]
- IMetaDataImport2::EnumGenericParamConstraints method [.NET Framework metadata]
ms.assetid: 8a7d4e40-28fe-4e14-b801-4049880130e7
topic_type:
- apiref
ms.openlocfilehash: 27c3ec349cf6c83f6783e252e6c5af5e99fa4b37
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95702839"
---
# <a name="imetadataimport2enumgenericparamconstraints-method"></a><span data-ttu-id="de304-102">IMetaDataImport2::EnumGenericParamConstraints — Metoda</span><span class="sxs-lookup"><span data-stu-id="de304-102">IMetaDataImport2::EnumGenericParamConstraints Method</span></span>

<span data-ttu-id="de304-103">Pobiera moduł wyliczający dla tablicy ograniczeń parametrów ogólnych skojarzonych z parametrem ogólnym reprezentowanym przez określony token.</span><span class="sxs-lookup"><span data-stu-id="de304-103">Gets an enumerator for an array of generic parameter constraints associated with the generic parameter represented by the specified token.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="de304-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="de304-104">Syntax</span></span>  
  
```cpp  
HRESULT EnumGenericParamConstraints (  
    [in, out] HCORENUM                *phEnum,  
    [in]  mdGenericParam              tk,  
    [out] mdGenericParamConstraint    rGenericParamConstraints[],  
    [in]  ULONG                       cMax,  
    [out] ULONG                       *pcGenericParamConstraints  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="de304-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="de304-105">Parameters</span></span>  

 `phEnum`  
 <span data-ttu-id="de304-106">[in. out] Wskaźnik do modułu wyliczającego.</span><span class="sxs-lookup"><span data-stu-id="de304-106">[in, out] A pointer to the enumerator.</span></span>  
  
 `tk`  
 <span data-ttu-id="de304-107">podczas   Token reprezentujący parametr generyczny, którego ograniczenia mają zostać wyliczone.</span><span class="sxs-lookup"><span data-stu-id="de304-107">[in]   A token that represents the generic parameter whose constraints are to be enumerated.</span></span>  
  
 `rGenericParamConstraints`  
 <span data-ttu-id="de304-108">określoną Tablica ograniczeń parametrów ogólnych do wyliczenia.</span><span class="sxs-lookup"><span data-stu-id="de304-108">[out] The array of generic parameter constraints to enumerate.</span></span>  
  
 `cMax`  
 <span data-ttu-id="de304-109">podczas   Żądana Maksymalna liczba tokenów do umieszczenia `rGenericParamConstraints` .</span><span class="sxs-lookup"><span data-stu-id="de304-109">[in]   The requested maximum number of tokens to place in `rGenericParamConstraints`.</span></span>  
  
 `pcGenericParamConstraints`  
 <span data-ttu-id="de304-110">określoną Wskaźnik do liczby umieszczonych tokenów `rGenericParamConstraints` .</span><span class="sxs-lookup"><span data-stu-id="de304-110">[out] A pointer to the number of tokens placed in `rGenericParamConstraints`.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="de304-111">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="de304-111">Return Value</span></span>  
  
|<span data-ttu-id="de304-112">HRESULT</span><span class="sxs-lookup"><span data-stu-id="de304-112">HRESULT</span></span>|<span data-ttu-id="de304-113">Opis</span><span class="sxs-lookup"><span data-stu-id="de304-113">Description</span></span>|  
|-------------|-----------------|  
|`S_OK`|<span data-ttu-id="de304-114">`EnumGenericParameterConstraints` pomyślnie zwrócono.</span><span class="sxs-lookup"><span data-stu-id="de304-114">`EnumGenericParameterConstraints` returned successfully.</span></span>|  
|`S_FALSE`|<span data-ttu-id="de304-115">`phEnum` nie ma elementów członkowskich.</span><span class="sxs-lookup"><span data-stu-id="de304-115">`phEnum` has no member elements.</span></span> <span data-ttu-id="de304-116">W tym przypadku `pcGenericParameterConstraints` jest ustawiona na 0 (zero).</span><span class="sxs-lookup"><span data-stu-id="de304-116">In this case, `pcGenericParameterConstraints` is set to 0 (zero).</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="de304-117">Wymagania</span><span class="sxs-lookup"><span data-stu-id="de304-117">Requirements</span></span>  

 <span data-ttu-id="de304-118">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="de304-118">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="de304-119">**Nagłówek:** Cor. h</span><span class="sxs-lookup"><span data-stu-id="de304-119">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="de304-120">**Biblioteka:** Używane jako zasób w MsCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="de304-120">**Library:** Used as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="de304-121">**.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="de304-121">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="de304-122">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="de304-122">See also</span></span>

- [<span data-ttu-id="de304-123">IMetaDataImport2 — Interfejs</span><span class="sxs-lookup"><span data-stu-id="de304-123">IMetaDataImport2 Interface</span></span>](imetadataimport2-interface.md)
- [<span data-ttu-id="de304-124">IMetaDataImport — Interfejs</span><span class="sxs-lookup"><span data-stu-id="de304-124">IMetaDataImport Interface</span></span>](imetadataimport-interface.md)
