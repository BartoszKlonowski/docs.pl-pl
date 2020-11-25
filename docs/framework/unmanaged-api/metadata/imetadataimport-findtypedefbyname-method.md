---
title: IMetaDataImport::FindTypeDefByName — Metoda
ms.date: 03/30/2017
api_name:
- IMetaDataImport.FindTypeDefByName
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::FindTypeDefByName
helpviewer_keywords:
- FindTypeDefByName method [.NET Framework metadata]
- IMetaDataImport::FindTypeDefByName method [.NET Framework metadata]
ms.assetid: f4c2cd88-ac28-4bad-9ab1-2cf9d2de41e6
topic_type:
- apiref
ms.openlocfilehash: df1516a916b2b48080e4f94937fba063926330ba
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95711302"
---
# <a name="imetadataimportfindtypedefbyname-method"></a><span data-ttu-id="9dca2-102">IMetaDataImport::FindTypeDefByName — Metoda</span><span class="sxs-lookup"><span data-stu-id="9dca2-102">IMetaDataImport::FindTypeDefByName Method</span></span>

<span data-ttu-id="9dca2-103">Pobiera wskaźnik do tokenu metadanych TypeDef dla <xref:System.Type> o podanej nazwie.</span><span class="sxs-lookup"><span data-stu-id="9dca2-103">Gets a pointer to the TypeDef metadata token for the <xref:System.Type> with the specified name.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="9dca2-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="9dca2-104">Syntax</span></span>  
  
```cpp  
HRESULT FindTypeDefByName  
   [in]  LPCWSTR       szTypeDef,  
   [in]  mdToken       tkEnclosingClass,  
   [out] mdTypeDef     *ptd  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="9dca2-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="9dca2-105">Parameters</span></span>  

 `szTypeDef`  
 <span data-ttu-id="9dca2-106">podczas Nazwa typu, dla którego ma zostać pobrany token TypeDef.</span><span class="sxs-lookup"><span data-stu-id="9dca2-106">[in] The name of the type for which to get the TypeDef token.</span></span>  
  
 `tkEnclosingClass`  
 <span data-ttu-id="9dca2-107">podczas Token TypeDef lub TypeRef reprezentujący otaczającą klasę.</span><span class="sxs-lookup"><span data-stu-id="9dca2-107">[in] A TypeDef or TypeRef token representing the enclosing class.</span></span> <span data-ttu-id="9dca2-108">Jeśli typ do znalezienia nie jest klasą zagnieżdżoną, ustaw tę wartość na NULL.</span><span class="sxs-lookup"><span data-stu-id="9dca2-108">If the type to find is not a nested class, set this value to NULL.</span></span>  
  
 `ptd`  
 <span data-ttu-id="9dca2-109">określoną Wskaźnik do zgodnego tokenu TypeDef.</span><span class="sxs-lookup"><span data-stu-id="9dca2-109">[out] A pointer to the matching TypeDef token.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="9dca2-110">Wymagania</span><span class="sxs-lookup"><span data-stu-id="9dca2-110">Requirements</span></span>  

 <span data-ttu-id="9dca2-111">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="9dca2-111">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="9dca2-112">**Nagłówek:** Cor. h</span><span class="sxs-lookup"><span data-stu-id="9dca2-112">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="9dca2-113">**Biblioteka:** Uwzględnione jako zasób w MsCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="9dca2-113">**Library:** Included as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="9dca2-114">**.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="9dca2-114">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="9dca2-115">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="9dca2-115">See also</span></span>

- [<span data-ttu-id="9dca2-116">IMetaDataImport — Interfejs</span><span class="sxs-lookup"><span data-stu-id="9dca2-116">IMetaDataImport Interface</span></span>](imetadataimport-interface.md)
- [<span data-ttu-id="9dca2-117">IMetaDataImport2 — Interfejs</span><span class="sxs-lookup"><span data-stu-id="9dca2-117">IMetaDataImport2 Interface</span></span>](imetadataimport2-interface.md)
