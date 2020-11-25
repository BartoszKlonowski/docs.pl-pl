---
title: CLRCreateInstance — Funkcja
ms.date: 03/30/2017
api_name:
- CLRCreateInstance
api_location:
- mscoree.dll
- mscoreei.dll
api_type:
- COM
f1_keywords:
- CLRCreateInstance
helpviewer_keywords:
- CLRCreateInstance function [.NET Framework hosting]
ms.assetid: 5de13327-96c6-4697-a89e-b8bf40717855
topic_type:
- apiref
ms.openlocfilehash: 3c7a14f828e55310435a99693c1195f2f0dd40c6
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95711679"
---
# <a name="clrcreateinstance-function"></a><span data-ttu-id="c1423-102">CLRCreateInstance — Funkcja</span><span class="sxs-lookup"><span data-stu-id="c1423-102">CLRCreateInstance Function</span></span>

<span data-ttu-id="c1423-103">Udostępnia jeden z trzech interfejsów: [ICLRMetaHost](iclrmetahost-interface.md), [ICLRMetaHostPolicy](iclrmetahostpolicy-interface.md)lub [ICLRDebugging](../debugging/iclrdebugging-interface.md).</span><span class="sxs-lookup"><span data-stu-id="c1423-103">Provides one of three interfaces: [ICLRMetaHost](iclrmetahost-interface.md), [ICLRMetaHostPolicy](iclrmetahostpolicy-interface.md), or [ICLRDebugging](../debugging/iclrdebugging-interface.md).</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="c1423-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="c1423-104">Syntax</span></span>  
  
```cpp  
HRESULT CLRCreateInstance(  
    [in]  REFCLSID  clsid,  
    [in]  REFIID     riid,  
    [out] LPVOID  * ppInterface  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="c1423-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="c1423-105">Parameters</span></span>  

 `clsid`  
 <span data-ttu-id="c1423-106">podczas Jeden z trzech identyfikatorów klasy: CLSID_CLRMetaHost, CLSID_CLRMetaHostPolicy lub CLSID_CLRDebugging.</span><span class="sxs-lookup"><span data-stu-id="c1423-106">[in] One of three class identifiers: CLSID_CLRMetaHost, CLSID_CLRMetaHostPolicy, or CLSID_CLRDebugging.</span></span>  
  
 `riid`  
 <span data-ttu-id="c1423-107">podczas Jeden z trzech identyfikatorów interfejsu (IID): IID_ICLRMetaHost, IID_ICLRMetaHostPolicy lub IID_ICLRDebugging.</span><span class="sxs-lookup"><span data-stu-id="c1423-107">[in] One of three interface identifiers (IIDs): IID_ICLRMetaHost, IID_ICLRMetaHostPolicy, or IID_ICLRDebugging.</span></span>  
  
 `ppInterface`  
 <span data-ttu-id="c1423-108">określoną Jeden z trzech interfejsów: [ICLRMetaHost](iclrmetahost-interface.md), [ICLRMetaHostPolicy](iclrmetahostpolicy-interface.md)lub [ICLRDebugging](../debugging/iclrdebugging-interface.md).</span><span class="sxs-lookup"><span data-stu-id="c1423-108">[out] One of three interfaces: [ICLRMetaHost](iclrmetahost-interface.md), [ICLRMetaHostPolicy](iclrmetahostpolicy-interface.md), or [ICLRDebugging](../debugging/iclrdebugging-interface.md).</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="c1423-109">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="c1423-109">Return Value</span></span>  

 <span data-ttu-id="c1423-110">Ta metoda zwraca następujące określone wartości HRESULT oraz błędy HRESULT wskazujące niepowodzenie metody.</span><span class="sxs-lookup"><span data-stu-id="c1423-110">This method returns the following specific HRESULTs as well as HRESULT errors that indicate method failure.</span></span>  
  
|<span data-ttu-id="c1423-111">HRESULT</span><span class="sxs-lookup"><span data-stu-id="c1423-111">HRESULT</span></span>|<span data-ttu-id="c1423-112">Opis</span><span class="sxs-lookup"><span data-stu-id="c1423-112">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="c1423-113">S_OK</span><span class="sxs-lookup"><span data-stu-id="c1423-113">S_OK</span></span>|<span data-ttu-id="c1423-114">Metoda została ukończona pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="c1423-114">The method completed successfully.</span></span>|  
|<span data-ttu-id="c1423-115">E_POINTER</span><span class="sxs-lookup"><span data-stu-id="c1423-115">E_POINTER</span></span>|<span data-ttu-id="c1423-116">`ppInterface` ma wartość null.</span><span class="sxs-lookup"><span data-stu-id="c1423-116">`ppInterface` is null.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="c1423-117">Uwagi</span><span class="sxs-lookup"><span data-stu-id="c1423-117">Remarks</span></span>  

 <span data-ttu-id="c1423-118">W poniższej tabeli przedstawiono obsługiwane kombinacje dla programów `clsid` i `riid` .</span><span class="sxs-lookup"><span data-stu-id="c1423-118">The following table shows the supported combinations for `clsid` and `riid`.</span></span>  
  
|`clsid`|`riid`|  
|--------------|------------|  
|<span data-ttu-id="c1423-119">CLSID_CLRMetaHost</span><span class="sxs-lookup"><span data-stu-id="c1423-119">CLSID_CLRMetaHost</span></span>|<span data-ttu-id="c1423-120">IID_ICLRMetaHost</span><span class="sxs-lookup"><span data-stu-id="c1423-120">IID_ICLRMetaHost</span></span>|  
|<span data-ttu-id="c1423-121">CLSID_CLRMetaHostPolicy</span><span class="sxs-lookup"><span data-stu-id="c1423-121">CLSID_CLRMetaHostPolicy</span></span>|<span data-ttu-id="c1423-122">IID_ICLRMetaHostPolicy</span><span class="sxs-lookup"><span data-stu-id="c1423-122">IID_ICLRMetaHostPolicy</span></span>|  
|<span data-ttu-id="c1423-123">CLSID_CLRDebugging</span><span class="sxs-lookup"><span data-stu-id="c1423-123">CLSID_CLRDebugging</span></span>|<span data-ttu-id="c1423-124">IID_ICLRDebugging</span><span class="sxs-lookup"><span data-stu-id="c1423-124">IID_ICLRDebugging</span></span>|  
  
 <span data-ttu-id="c1423-125">Poniższy kod przedstawia sposób użycia `CLRCreateInstance` programu w celu uzyskania wszystkich trzech interfejsów:</span><span class="sxs-lookup"><span data-stu-id="c1423-125">The following code shows how to use `CLRCreateInstance` to get all three interfaces:</span></span>  
  
```cpp  
#include <metahost.h>  
#pragma comment(lib, "mscoree.lib")  
  
ICLRMetaHost       *pMetaHost       = NULL;  
ICLRMetaHostPolicy *pMetaHostPolicy = NULL;  
ICLRDebugging      *pCLRDebugging   = NULL;  
HRESULT hr;  
hr = CLRCreateInstance(CLSID_CLRMetaHost, IID_ICLRMetaHost,  
                    (LPVOID*)&pMetaHost);  
hr = CLRCreateInstance (CLSID_CLRMetaHostPolicy, IID_ICLRMetaHostPolicy,  
                    (LPVOID*)&pMetaHostPolicy);  
hr = CLRCreateInstance (CLSID_CLRDebugging, IID_ICLRDebugging,  
                    (LPVOID*)&pCLRDebugging);  
```  
  
## <a name="requirements"></a><span data-ttu-id="c1423-126">Wymagania</span><span class="sxs-lookup"><span data-stu-id="c1423-126">Requirements</span></span>  

 <span data-ttu-id="c1423-127">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="c1423-127">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="c1423-128">**Nagłówek:** Obiekt ServiceHost. h</span><span class="sxs-lookup"><span data-stu-id="c1423-128">**Header:** MetaHost.h</span></span>  
  
 <span data-ttu-id="c1423-129">**Biblioteka:** Uwzględnione jako zasób w MSCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="c1423-129">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="c1423-130">**.NET Framework wersje:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="c1423-130">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="c1423-131">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="c1423-131">See also</span></span>

- [<span data-ttu-id="c1423-132">Hosting</span><span class="sxs-lookup"><span data-stu-id="c1423-132">Hosting</span></span>](index.md)
