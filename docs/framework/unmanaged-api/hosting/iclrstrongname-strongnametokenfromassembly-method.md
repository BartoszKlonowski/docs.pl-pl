---
title: ICLRStrongName::StrongNameTokenFromAssembly — Metoda
ms.date: 03/30/2017
api_name:
- ICLRStrongName.StrongNameTokenFromAssembly
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName::StrongNameTokenFromAssembly
helpviewer_keywords:
- ICLRStrongName::StrongNameTokenFromAssembly method [.NET Framework hosting]
- StrongNameTokenFromAssembly method, ICLRStrongName interface [.NET Framework hosting]
ms.assetid: fc725afb-b66b-4015-aa44-1c0d1304197f
topic_type:
- apiref
ms.openlocfilehash: 90a7e60e35e1fc555681102ffa62967eb5ac01fc
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95671541"
---
# <a name="iclrstrongnamestrongnametokenfromassembly-method"></a><span data-ttu-id="c7550-102">ICLRStrongName::StrongNameTokenFromAssembly — Metoda</span><span class="sxs-lookup"><span data-stu-id="c7550-102">ICLRStrongName::StrongNameTokenFromAssembly Method</span></span>

<span data-ttu-id="c7550-103">Tworzy token silnej nazwy z określonego pliku zestawu.</span><span class="sxs-lookup"><span data-stu-id="c7550-103">Creates a strong name token from the specified assembly file.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="c7550-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="c7550-104">Syntax</span></span>  
  
```cpp  
HRESULT StrongNameTokenFromAssembly (  
    [in]  LPCWSTR   wszFilePath,  
    [out] BYTE      **ppbStrongNameToken,  
    [out] ULONG     *pcbStrongNameToken  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="c7550-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="c7550-105">Parameters</span></span>  

 `wszFilePath`  
 <span data-ttu-id="c7550-106">podczas Ścieżka do przenośnego pliku wykonywalnego (PE) dla zestawu.</span><span class="sxs-lookup"><span data-stu-id="c7550-106">[in] The path to the portable executable (PE) file for the assembly.</span></span>  
  
 `ppbStrongNameToken`  
 <span data-ttu-id="c7550-107">określoną Zwrócony token silnej nazwy.</span><span class="sxs-lookup"><span data-stu-id="c7550-107">[out] The returned strong name token.</span></span>  
  
 `pcbStrongNameToken`  
 <span data-ttu-id="c7550-108">określoną Rozmiar (w bajtach) tokenu silnej nazwy.</span><span class="sxs-lookup"><span data-stu-id="c7550-108">[out] The size, in bytes, of the strong name token.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="c7550-109">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="c7550-109">Return Value</span></span>  

 <span data-ttu-id="c7550-110">`S_OK` Jeśli metoda została ukończona pomyślnie; w przeciwnym razie wartość HRESULT wskazująca niepowodzenie (zobacz [typowe wartości HRESULT](/windows/win32/seccrypto/common-hresult-values) dla listy).</span><span class="sxs-lookup"><span data-stu-id="c7550-110">`S_OK` if the method completed successfully; otherwise, an HRESULT value that indicates failure (see [Common HRESULT Values](/windows/win32/seccrypto/common-hresult-values) for a list).</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="c7550-111">Uwagi</span><span class="sxs-lookup"><span data-stu-id="c7550-111">Remarks</span></span>  

 <span data-ttu-id="c7550-112">Token silnej nazwy to skrócona postać klucza publicznego.</span><span class="sxs-lookup"><span data-stu-id="c7550-112">A strong name token is the shortened form of a public key.</span></span> <span data-ttu-id="c7550-113">Token jest 64-bitowym skrótem, który jest tworzony na podstawie klucza publicznego używanego do podpisywania zestawu.</span><span class="sxs-lookup"><span data-stu-id="c7550-113">The token is a 64-bit hash that is created from the public key used to sign the assembly.</span></span> <span data-ttu-id="c7550-114">Token jest częścią silnej nazwy zestawu i można go odczytać z metadanych zestawu.</span><span class="sxs-lookup"><span data-stu-id="c7550-114">The token is a part of the strong name for the assembly, and can be read from the assembly metadata.</span></span>  
  
 <span data-ttu-id="c7550-115">Po utworzeniu tokenu należy wywołać metodę [ICLRStrongName:: StrongNameFreeBuffer —](iclrstrongname-strongnamefreebuffer-method.md) , aby zwolnić przydzieloną pamięć.</span><span class="sxs-lookup"><span data-stu-id="c7550-115">After the token is created, you should call the [ICLRStrongName::StrongNameFreeBuffer](iclrstrongname-strongnamefreebuffer-method.md) method to release the allocated memory.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="c7550-116">Wymagania</span><span class="sxs-lookup"><span data-stu-id="c7550-116">Requirements</span></span>  

 <span data-ttu-id="c7550-117">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="c7550-117">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="c7550-118">**Nagłówek:** Obiekt ServiceHost. h</span><span class="sxs-lookup"><span data-stu-id="c7550-118">**Header:** MetaHost.h</span></span>  
  
 <span data-ttu-id="c7550-119">**Biblioteka:** Uwzględnione jako zasób w MSCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="c7550-119">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="c7550-120">**.NET Framework wersje:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="c7550-120">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="c7550-121">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="c7550-121">See also</span></span>

- [<span data-ttu-id="c7550-122">StrongNameTokenFromAssemblyEx, metoda</span><span class="sxs-lookup"><span data-stu-id="c7550-122">StrongNameTokenFromAssemblyEx Method</span></span>](iclrstrongname-strongnametokenfromassemblyex-method.md)
- [<span data-ttu-id="c7550-123">ICLRStrongName — Interfejs</span><span class="sxs-lookup"><span data-stu-id="c7550-123">ICLRStrongName Interface</span></span>](iclrstrongname-interface.md)
