---
title: ICeeGen::GetIlSection — Metoda
ms.date: 03/30/2017
api_name:
- ICeeGen.GetIlSection
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICeeGen::GetIlSection
helpviewer_keywords:
- GetIlSection method [.NET Framework metadata]
- ICeeGen::GetIlSection method [.NET Framework metadata]
ms.assetid: 6f2db2ca-203f-4ac3-9530-208642ca385e
topic_type:
- apiref
ms.openlocfilehash: c179d5e1ca976d8f425e7c408ceb663cba64f641
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95715345"
---
# <a name="iceegengetilsection-method"></a><span data-ttu-id="4a667-102">ICeeGen::GetIlSection — Metoda</span><span class="sxs-lookup"><span data-stu-id="4a667-102">ICeeGen::GetIlSection Method</span></span>

<span data-ttu-id="4a667-103">Pobiera sekcję bazy kodu języka pośredniego, do której odwołuje się określone dojście.</span><span class="sxs-lookup"><span data-stu-id="4a667-103">Gets the section of the intermediate language code base referenced by the specified handle.</span></span>  
  
 <span data-ttu-id="4a667-104">Ta metoda jest przestarzała i nie powinna być używana.</span><span class="sxs-lookup"><span data-stu-id="4a667-104">This method is obsolete and should not be used.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="4a667-105">Składnia</span><span class="sxs-lookup"><span data-stu-id="4a667-105">Syntax</span></span>  
  
```cpp  
HRESULT GetIlSection (  
    [in] HCEESECTION  *section  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="4a667-106">Parametry</span><span class="sxs-lookup"><span data-stu-id="4a667-106">Parameters</span></span>  

 `section`  
 <span data-ttu-id="4a667-107">podczas Dojście do sekcji do pobrania.</span><span class="sxs-lookup"><span data-stu-id="4a667-107">[in] The handle to the section to get.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="4a667-108">Wymagania</span><span class="sxs-lookup"><span data-stu-id="4a667-108">Requirements</span></span>  

 <span data-ttu-id="4a667-109">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="4a667-109">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="4a667-110">**Nagłówek:** Cor. h</span><span class="sxs-lookup"><span data-stu-id="4a667-110">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="4a667-111">**Biblioteka:** Używane jako zasób w MsCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="4a667-111">**Library:** Used as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="4a667-112">**.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="4a667-112">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="4a667-113">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="4a667-113">See also</span></span>

- [<span data-ttu-id="4a667-114">ICeeGen — Interfejs</span><span class="sxs-lookup"><span data-stu-id="4a667-114">ICeeGen Interface</span></span>](iceegen-interface.md)
