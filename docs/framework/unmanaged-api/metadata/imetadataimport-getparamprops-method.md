---
title: IMetaDataImport::GetParamProps — Metoda
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetParamProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetParamProps
helpviewer_keywords:
- IMetaDataImport::GetParamProps method [.NET Framework metadata]
- GetParamProps method [.NET Framework metadata]
ms.assetid: 4d5e5f00-bcab-4f41-b191-176511a186a7
topic_type:
- apiref
ms.openlocfilehash: a16621f4c9b06f049239dc4e2335d70a167dd756
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95729268"
---
# <a name="imetadataimportgetparamprops-method"></a><span data-ttu-id="56e25-102">IMetaDataImport::GetParamProps — Metoda</span><span class="sxs-lookup"><span data-stu-id="56e25-102">IMetaDataImport::GetParamProps Method</span></span>

<span data-ttu-id="56e25-103">Pobiera wartości metadanych dla parametru, do którego odwołuje się określony token ParamDef.</span><span class="sxs-lookup"><span data-stu-id="56e25-103">Gets metadata values for the parameter referenced by the specified ParamDef token.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="56e25-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="56e25-104">Syntax</span></span>  
  
```cpp  
HRESULT GetParamProps (  
   [in]  mdParamDef      tk,  
   [out] mdMethodDef     *pmd,  
   [out] ULONG           *pulSequence,  
   [out] LPWSTR          szName,  
   [in]  ULONG           cchName,  
   [out] ULONG           *pchName,  
   [out] DWORD           *pdwAttr,  
   [out] DWORD           *pdwCPlusTypeFlag,  
   [out] UVCP_CONSTANT   *ppValue,  
   [out] ULONG           *pcchValue  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="56e25-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="56e25-105">Parameters</span></span>  

 `tk`  
 <span data-ttu-id="56e25-106">podczas Token ParamDef reprezentujący parametr, dla którego mają zostać zwrócone metadane.</span><span class="sxs-lookup"><span data-stu-id="56e25-106">[in] A ParamDef token that represents the parameter to return metadata for.</span></span>  
  
 `pmd`  
 <span data-ttu-id="56e25-107">określoną Wskaźnik do tokenu MethodDef reprezentujący metodę, która pobiera parametr.</span><span class="sxs-lookup"><span data-stu-id="56e25-107">[out] A pointer to a MethodDef token representing the method that takes the parameter.</span></span>  
  
 `pulSequence`  
 <span data-ttu-id="56e25-108">określoną Pozycja porządkowa parametru na liście argumentów metody.</span><span class="sxs-lookup"><span data-stu-id="56e25-108">[out] The ordinal position of the parameter in the method argument list.</span></span>  
  
 `szName`  
 <span data-ttu-id="56e25-109">określoną Bufor służący do przechowywania nazwy parametru.</span><span class="sxs-lookup"><span data-stu-id="56e25-109">[out] A buffer to hold the name of the parameter.</span></span>  
  
 `cchName`  
 <span data-ttu-id="56e25-110">podczas Żądany rozmiar w postaci znaków dwubajtowych `szName` .</span><span class="sxs-lookup"><span data-stu-id="56e25-110">[in] The requested size in wide characters of `szName`.</span></span>  
  
 `pchName`  
 <span data-ttu-id="56e25-111">określoną Zwrócony rozmiar w postaci znaków dwubajtowych `szName` .</span><span class="sxs-lookup"><span data-stu-id="56e25-111">[out] The returned size in wide characters of `szName`.</span></span>  
  
 `pdwAttr`  
 <span data-ttu-id="56e25-112">określoną Wskaźnik do dowolnych flag atrybutów skojarzonych z parametrem.</span><span class="sxs-lookup"><span data-stu-id="56e25-112">[out] A pointer to any attribute flags associated with the parameter.</span></span> <span data-ttu-id="56e25-113">To jest maska bitów `CorParamAttr` wartości.</span><span class="sxs-lookup"><span data-stu-id="56e25-113">This is a bitmask of `CorParamAttr` values.</span></span>  
  
 `pdwCPlusTypeFlag`  
 <span data-ttu-id="56e25-114">określoną Wskaźnik do flagi wskazującej, że parametr jest <xref:System.ValueType> .</span><span class="sxs-lookup"><span data-stu-id="56e25-114">[out] A pointer to a flag specifying that the parameter is a <xref:System.ValueType>.</span></span>  
  
 `ppValue`  
 <span data-ttu-id="56e25-115">określoną Wskaźnik do stałego ciągu zwracanego przez parametr.</span><span class="sxs-lookup"><span data-stu-id="56e25-115">[out] A pointer to a constant string returned by the parameter.</span></span>  
  
 `pcchValue`  
 <span data-ttu-id="56e25-116">określoną Rozmiar znaków dwubajtowych `ppValue` lub zero, jeśli nie zawiera `ppValue` ciągu.</span><span class="sxs-lookup"><span data-stu-id="56e25-116">[out] The size of `ppValue` in wide characters, or zero if `ppValue` does not hold a string.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="56e25-117">Uwagi</span><span class="sxs-lookup"><span data-stu-id="56e25-117">Remarks</span></span>

<span data-ttu-id="56e25-118">Wartości sekwencji `pulSequence` zaczynają się od 1 dla parametrów.</span><span class="sxs-lookup"><span data-stu-id="56e25-118">The sequence values in `pulSequence` begin with 1 for parameters.</span></span> <span data-ttu-id="56e25-119">Wartość zwracana ma numer sekwencyjny równy 0.</span><span class="sxs-lookup"><span data-stu-id="56e25-119">A return value has a sequence number of 0.</span></span>

## <a name="requirements"></a><span data-ttu-id="56e25-120">Wymagania</span><span class="sxs-lookup"><span data-stu-id="56e25-120">Requirements</span></span>  

 <span data-ttu-id="56e25-121">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="56e25-121">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="56e25-122">**Nagłówek:** Cor. h</span><span class="sxs-lookup"><span data-stu-id="56e25-122">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="56e25-123">**Biblioteka:** Uwzględnione jako zasób w MsCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="56e25-123">**Library:** Included as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="56e25-124">**.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="56e25-124">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="56e25-125">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="56e25-125">See also</span></span>

- [<span data-ttu-id="56e25-126">IMetaDataImport — Interfejs</span><span class="sxs-lookup"><span data-stu-id="56e25-126">IMetaDataImport Interface</span></span>](imetadataimport-interface.md)
- [<span data-ttu-id="56e25-127">IMetaDataImport2 — Interfejs</span><span class="sxs-lookup"><span data-stu-id="56e25-127">IMetaDataImport2 Interface</span></span>](imetadataimport2-interface.md)
