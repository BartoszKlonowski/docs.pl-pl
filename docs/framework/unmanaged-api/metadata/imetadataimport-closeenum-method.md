---
title: IMetaDataImport::CloseEnum — Metoda
ms.date: 03/30/2017
api_name:
- IMetaDataImport.CloseEnum
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::CloseEnum
helpviewer_keywords:
- IMetaDataImport::CloseEnum method [.NET Framework metadata]
- CloseEnum method, IMetaDataImport interface [.NET Framework metadata]
ms.assetid: 727819d5-1dab-4ebb-ac25-950b4111dc72
topic_type:
- apiref
ms.openlocfilehash: f418b48f1b62ae8093197d64ca44b2ef659990a3
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95701721"
---
# <a name="imetadataimportcloseenum-method"></a><span data-ttu-id="b808f-102">IMetaDataImport::CloseEnum — Metoda</span><span class="sxs-lookup"><span data-stu-id="b808f-102">IMetaDataImport::CloseEnum Method</span></span>

<span data-ttu-id="b808f-103">Zamyka moduł wyliczający, który jest identyfikowany przez określone dojście.</span><span class="sxs-lookup"><span data-stu-id="b808f-103">Closes the enumerator that is identified by the specified handle.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="b808f-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="b808f-104">Syntax</span></span>  
  
```cpp  
void CloseEnum (  
   [in] HCORENUM hEnum  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="b808f-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="b808f-105">Parameters</span></span>  

 `hEnum`  
 <span data-ttu-id="b808f-106">podczas Dojście do zamknięcia modułu wyliczającego.</span><span class="sxs-lookup"><span data-stu-id="b808f-106">[in] The handle for the enumerator to close.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="b808f-107">Uwagi</span><span class="sxs-lookup"><span data-stu-id="b808f-107">Remarks</span></span>  

 <span data-ttu-id="b808f-108">Dojście określone przez `hEnum` jest uzyskiwane z poprzedniego `Enum` wywołania *nazwy* (na przykład [IMetaDataImport:: EnumTypeDefs —](imetadataimport-enumtypedefs-method.md)).</span><span class="sxs-lookup"><span data-stu-id="b808f-108">The handle specified by `hEnum` is obtained from a previous `Enum`*Name* call (for example, [IMetaDataImport::EnumTypeDefs](imetadataimport-enumtypedefs-method.md)).</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="b808f-109">Wymagania</span><span class="sxs-lookup"><span data-stu-id="b808f-109">Requirements</span></span>  

 <span data-ttu-id="b808f-110">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="b808f-110">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="b808f-111">**Nagłówek:** Cor. h</span><span class="sxs-lookup"><span data-stu-id="b808f-111">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="b808f-112">**Biblioteka:** Uwzględnione jako zasób w MsCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="b808f-112">**Library:** Included as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="b808f-113">**.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="b808f-113">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="b808f-114">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="b808f-114">See also</span></span>

- [<span data-ttu-id="b808f-115">IMetaDataImport — Interfejs</span><span class="sxs-lookup"><span data-stu-id="b808f-115">IMetaDataImport Interface</span></span>](imetadataimport-interface.md)
- [<span data-ttu-id="b808f-116">IMetaDataImport2 — Interfejs</span><span class="sxs-lookup"><span data-stu-id="b808f-116">IMetaDataImport2 Interface</span></span>](imetadataimport2-interface.md)
