---
title: ICLRAssemblyIdentityManager::IsStronglyNamed — Metoda
ms.date: 03/30/2017
api_name:
- ICLRAssemblyIdentityManager.IsStronglyNamed
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRAssemblyIdentityManager::IsStronglyNamed
helpviewer_keywords:
- IsStronglyNamed method [.NET Framework hosting]
- ICLRAssemblyIdentityManager::IsStronglyNamed method [.NET Framework hosting]
ms.assetid: 954bd386-2076-4d00-9d46-38c728aa9cab
topic_type:
- apiref
ms.openlocfilehash: 9ac3b2ae349a696ba0cea1bad3e3484bb1c113fa
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95679250"
---
# <a name="iclrassemblyidentitymanagerisstronglynamed-method"></a><span data-ttu-id="c8a00-102">ICLRAssemblyIdentityManager::IsStronglyNamed — Metoda</span><span class="sxs-lookup"><span data-stu-id="c8a00-102">ICLRAssemblyIdentityManager::IsStronglyNamed Method</span></span>

<span data-ttu-id="c8a00-103">Pobiera wartość wskazującą, czy określony zestaw ma silną nazwę.</span><span class="sxs-lookup"><span data-stu-id="c8a00-103">Gets a value that indicates whether the specified assembly is strongly named.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="c8a00-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="c8a00-104">Syntax</span></span>  
  
```cpp  
RESULT IsStronglyNamed (  
    [in]  LPCWSTR  pwzAssemblyIdentity,  
    [out] BOOL    *pbIsStronglyNamed  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="c8a00-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="c8a00-105">Parameters</span></span>  

 `pwzAssemblyIdentity`  
 <span data-ttu-id="c8a00-106">podczas Nieprzezroczyste dane tożsamości zestawu kanonicznego zestawu do oceny.</span><span class="sxs-lookup"><span data-stu-id="c8a00-106">[in] The opaque canonical assembly identity data of the assembly to be evaluated.</span></span>  
  
 `pbIsStronglyNamed`  
 <span data-ttu-id="c8a00-107">[out] `true` , jeśli zestaw, do którego odwołuje się `pwzAssemblyIdentity` parametr, ma silną nazwę; w przeciwnym razie `false` .</span><span class="sxs-lookup"><span data-stu-id="c8a00-107">[out] `true`, if the assembly referenced by the `pwzAssemblyIdentity` parameter is strongly named; otherwise, `false`.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="c8a00-108">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="c8a00-108">Return Value</span></span>  
  
|<span data-ttu-id="c8a00-109">HRESULT</span><span class="sxs-lookup"><span data-stu-id="c8a00-109">HRESULT</span></span>|<span data-ttu-id="c8a00-110">Opis</span><span class="sxs-lookup"><span data-stu-id="c8a00-110">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="c8a00-111">S_OK</span><span class="sxs-lookup"><span data-stu-id="c8a00-111">S_OK</span></span>|<span data-ttu-id="c8a00-112">Metoda została pomyślnie zwrócona.</span><span class="sxs-lookup"><span data-stu-id="c8a00-112">The method returned successfully.</span></span>|  
|<span data-ttu-id="c8a00-113">HOST_E_CLRNOTAVAILABLE</span><span class="sxs-lookup"><span data-stu-id="c8a00-113">HOST_E_CLRNOTAVAILABLE</span></span>|<span data-ttu-id="c8a00-114">Środowisko uruchomieniowe języka wspólnego (CLR) nie zostało załadowane do procesu lub środowisko CLR znajduje się w stanie, w którym nie można uruchomić kodu zarządzanego lub przetworzyć wywołania pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="c8a00-114">The common language runtime (CLR) has not been loaded into a process, or the CLR is in a state in which it cannot run managed code or process the call successfully.</span></span>|  
|<span data-ttu-id="c8a00-115">HOST_E_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="c8a00-115">HOST_E_TIMEOUT</span></span>|<span data-ttu-id="c8a00-116">Upłynął limit czasu połączenia.</span><span class="sxs-lookup"><span data-stu-id="c8a00-116">The call timed out.</span></span>|  
|<span data-ttu-id="c8a00-117">HOST_E_NOT_OWNER</span><span class="sxs-lookup"><span data-stu-id="c8a00-117">HOST_E_NOT_OWNER</span></span>|<span data-ttu-id="c8a00-118">Obiekt wywołujący nie jest właocicielem blokady.</span><span class="sxs-lookup"><span data-stu-id="c8a00-118">The caller does not own the lock.</span></span>|  
|<span data-ttu-id="c8a00-119">HOST_E_ABANDONED</span><span class="sxs-lookup"><span data-stu-id="c8a00-119">HOST_E_ABANDONED</span></span>|<span data-ttu-id="c8a00-120">Zdarzenie zostało anulowane podczas oczekiwania na niego zablokowanego wątku lub włókna.</span><span class="sxs-lookup"><span data-stu-id="c8a00-120">An event was canceled while a blocked thread or fiber was waiting on it.</span></span>|  
|<span data-ttu-id="c8a00-121">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="c8a00-121">E_FAIL</span></span>|<span data-ttu-id="c8a00-122">Wystąpił nieznany błąd krytyczny.</span><span class="sxs-lookup"><span data-stu-id="c8a00-122">An unknown catastrophic failure occurred.</span></span> <span data-ttu-id="c8a00-123">Jeśli metoda zwraca E_FAIL, środowisko CLR nie będzie już można używać w procesie.</span><span class="sxs-lookup"><span data-stu-id="c8a00-123">If a method returns E_FAIL, the CLR is no longer usable within the process.</span></span> <span data-ttu-id="c8a00-124">Kolejne wywołania metod hostingu zwracają HOST_E_CLRNOTAVAILABLE.</span><span class="sxs-lookup"><span data-stu-id="c8a00-124">Subsequent calls to hosting methods return HOST_E_CLRNOTAVAILABLE.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="c8a00-125">Wymagania</span><span class="sxs-lookup"><span data-stu-id="c8a00-125">Requirements</span></span>  

 <span data-ttu-id="c8a00-126">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="c8a00-126">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="c8a00-127">**Nagłówek:** MSCorEE. h</span><span class="sxs-lookup"><span data-stu-id="c8a00-127">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="c8a00-128">**Biblioteka:** Uwzględnione jako zasób w MSCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="c8a00-128">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="c8a00-129">**.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="c8a00-129">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="c8a00-130">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="c8a00-130">See also</span></span>

- [<span data-ttu-id="c8a00-131">ICLRAssemblyIdentityManager — Interfejs</span><span class="sxs-lookup"><span data-stu-id="c8a00-131">ICLRAssemblyIdentityManager Interface</span></span>](iclrassemblyidentitymanager-interface.md)
