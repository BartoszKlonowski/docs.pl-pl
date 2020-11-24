---
title: Funkcja CertFreeAuthenticodeSignerInfo
ms.date: 03/30/2017
api_name:
- CertFreeAuthenticodeSignerInfo
api_location:
- clr.dll
api_type:
- DLLExport
ms.assetid: 8029633c-b6e4-4665-a7c2-89607c3247ef
ms.openlocfilehash: dc6bb5a137a50ec07f89f292e5d9beac4349c3c7
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95674180"
---
# <a name="certfreeauthenticodesignerinfo-function"></a><span data-ttu-id="e767b-102">Funkcja CertFreeAuthenticodeSignerInfo</span><span class="sxs-lookup"><span data-stu-id="e767b-102">CertFreeAuthenticodeSignerInfo Function</span></span>

<span data-ttu-id="e767b-103">Zwalnia zasoby przydzieloną dla struktury [AXL_AUTHENTICODE_SIGNER_INFO](axl-authenticode-signer-info-structure.md) .</span><span class="sxs-lookup"><span data-stu-id="e767b-103">Frees resources allocated for the [AXL_AUTHENTICODE_SIGNER_INFO](axl-authenticode-signer-info-structure.md) structure.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="e767b-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="e767b-104">Syntax</span></span>  
  
```cpp  
HRESULT CertFreeAuthenticodeSignerInfo (  
    [in, out]  PAXL_AUTHENTICODE_SIGNER_INFO   pSignerInfo);  
```  
  
## <a name="parameters"></a><span data-ttu-id="e767b-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="e767b-105">Parameters</span></span>  

 `pSignerInfo`  
 <span data-ttu-id="e767b-106">[in. out] Informacje o logowaniu do zwolnienia.</span><span class="sxs-lookup"><span data-stu-id="e767b-106">[in, out] Signer information to be released.</span></span> <span data-ttu-id="e767b-107">Zobacz strukturę [AXL_AUTHENTICODE_SIGNER_INFO](axl-authenticode-signer-info-structure.md) .</span><span class="sxs-lookup"><span data-stu-id="e767b-107">See the [AXL_AUTHENTICODE_SIGNER_INFO](axl-authenticode-signer-info-structure.md) structure.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="e767b-108">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="e767b-108">Return Value</span></span>  

 <span data-ttu-id="e767b-109">`S_OK` Jeśli funkcja się powiedzie.</span><span class="sxs-lookup"><span data-stu-id="e767b-109">`S_OK` if the function succeeds.</span></span> <span data-ttu-id="e767b-110">W przeciwnym razie zwraca kod błędu.</span><span class="sxs-lookup"><span data-stu-id="e767b-110">Otherwise, returns an error code.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e767b-111">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="e767b-111">See also</span></span>

- [<span data-ttu-id="e767b-112">Authenticode</span><span class="sxs-lookup"><span data-stu-id="e767b-112">Authenticode</span></span>](index.md)
