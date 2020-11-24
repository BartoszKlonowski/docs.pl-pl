---
title: ICLRStrongName::StrongNameKeyGen — Metoda
ms.date: 03/30/2017
api_name:
- ICLRStrongName.StrongNameKeyGen
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName::StrongNameKeyGen
helpviewer_keywords:
- StrongNameKeyGen method, ICLRStrongName interface [.NET Framework hosting]
- ICLRStrongName::StrongNameKeyGen method [.NET Framework hosting]
ms.assetid: ac5c1245-9acf-4271-9c08-3d9b7c670df3
topic_type:
- apiref
ms.openlocfilehash: 42a9fc1a05e97bbd893f0a2e77087e6524ad844f
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95674544"
---
# <a name="iclrstrongnamestrongnamekeygen-method"></a><span data-ttu-id="56c8a-102">ICLRStrongName::StrongNameKeyGen — Metoda</span><span class="sxs-lookup"><span data-stu-id="56c8a-102">ICLRStrongName::StrongNameKeyGen Method</span></span>

<span data-ttu-id="56c8a-103">Tworzy nową parę kluczy publiczny/prywatny w celu użycia silnej nazwy.</span><span class="sxs-lookup"><span data-stu-id="56c8a-103">Creates a new public/private key pair for strong name use.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="56c8a-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="56c8a-104">Syntax</span></span>  
  
```cpp  
HRESULT StrongNameKeyGen (  
    [in]  LPCWSTR   wszKeyContainer,  
    [in]  DWORD     dwFlags,  
    [out] BYTE      **ppbKeyBlob,  
    [out] ULONG     *pcbKeyBlob  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="56c8a-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="56c8a-105">Parameters</span></span>  

 `wszKeyContainer`  
 <span data-ttu-id="56c8a-106">podczas Nazwa żądanego kontenera kluczy.</span><span class="sxs-lookup"><span data-stu-id="56c8a-106">[in] The requested key container name.</span></span> <span data-ttu-id="56c8a-107">`wszKeyContainer` do wygenerowania nazwy tymczasowej musi być niepustym ciągiem lub wartością null.</span><span class="sxs-lookup"><span data-stu-id="56c8a-107">`wszKeyContainer` must either be a non-empty string or null to generate a temporary name.</span></span>  
  
 `dwFlags`  
 <span data-ttu-id="56c8a-108">podczas Wartość określająca, czy klucz ma pozostać zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="56c8a-108">[in] A value that specifies whether to leave the key registered.</span></span> <span data-ttu-id="56c8a-109">Obsługiwane są następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="56c8a-109">The following values are supported:</span></span>  
  
- <span data-ttu-id="56c8a-110">0x00000000 — używany, gdy `wszKeyContainer` ma wartość null, aby wygenerować nazwę kontenera kluczy tymczasowych.</span><span class="sxs-lookup"><span data-stu-id="56c8a-110">0x00000000 - Used when `wszKeyContainer` is null to generate a temporary key container name.</span></span>  
  
- <span data-ttu-id="56c8a-111">0x00000001 ( `SN_LEAVE_KEY` ) — określa, że klucz powinien pozostać zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="56c8a-111">0x00000001 (`SN_LEAVE_KEY`) - Specifies that the key should be left registered.</span></span>  
  
 `ppbKeyBlob`  
 <span data-ttu-id="56c8a-112">określoną Zwracana para kluczy publiczny/prywatny.</span><span class="sxs-lookup"><span data-stu-id="56c8a-112">[out] The returned public/private key pair.</span></span>  
  
 `pcbKeyBlob`  
 <span data-ttu-id="56c8a-113">określoną Rozmiar, w bajtach, z `ppbKeyBlob` .</span><span class="sxs-lookup"><span data-stu-id="56c8a-113">[out] The size, in bytes, of `ppbKeyBlob`.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="56c8a-114">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="56c8a-114">Return Value</span></span>  

 <span data-ttu-id="56c8a-115">`S_OK` Jeśli metoda została ukończona pomyślnie; w przeciwnym razie wartość HRESULT wskazująca niepowodzenie (zobacz [typowe wartości HRESULT](/windows/win32/seccrypto/common-hresult-values) dla listy).</span><span class="sxs-lookup"><span data-stu-id="56c8a-115">`S_OK` if the method completed successfully; otherwise, an HRESULT value that indicates failure (see [Common HRESULT Values](/windows/win32/seccrypto/common-hresult-values) for a list).</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="56c8a-116">Uwagi</span><span class="sxs-lookup"><span data-stu-id="56c8a-116">Remarks</span></span>  

 <span data-ttu-id="56c8a-117">[ICLRStrongName:: StrongNameKeyGen —](iclrstrongname-strongnamekeygen-method.md) Metoda tworzy klucz 1024-bitowy.</span><span class="sxs-lookup"><span data-stu-id="56c8a-117">The [ICLRStrongName::StrongNameKeyGen](iclrstrongname-strongnamekeygen-method.md) method creates a 1024-bit key.</span></span> <span data-ttu-id="56c8a-118">Po pobraniu klucza należy wywołać metodę [ICLRStrongName:: StrongNameFreeBuffer —](iclrstrongname-strongnamefreebuffer-method.md) , aby zwolnić przydzieloną pamięć.</span><span class="sxs-lookup"><span data-stu-id="56c8a-118">After the key is retrieved, you should call the [ICLRStrongName::StrongNameFreeBuffer](iclrstrongname-strongnamefreebuffer-method.md) method to release the allocated memory.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="56c8a-119">Wymagania</span><span class="sxs-lookup"><span data-stu-id="56c8a-119">Requirements</span></span>  

 <span data-ttu-id="56c8a-120">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="56c8a-120">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="56c8a-121">**Nagłówek:** Obiekt ServiceHost. h</span><span class="sxs-lookup"><span data-stu-id="56c8a-121">**Header:** MetaHost.h</span></span>  
  
 <span data-ttu-id="56c8a-122">**Biblioteka:** Uwzględnione jako zasób w MSCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="56c8a-122">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="56c8a-123">**.NET Framework wersje:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="56c8a-123">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="56c8a-124">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="56c8a-124">See also</span></span>

- [<span data-ttu-id="56c8a-125">StrongNameKeyGenEx, metoda</span><span class="sxs-lookup"><span data-stu-id="56c8a-125">StrongNameKeyGenEx Method</span></span>](iclrstrongname-strongnamekeygenex-method.md)
- [<span data-ttu-id="56c8a-126">ICLRStrongName — Interfejs</span><span class="sxs-lookup"><span data-stu-id="56c8a-126">ICLRStrongName Interface</span></span>](iclrstrongname-interface.md)
