---
title: ICorRuntimeHost::CreateEvidence — Metoda
ms.date: 03/30/2017
api_name:
- ICorRuntimeHost.CreateEvidence
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICorRuntimeHost::CreateEvidence
helpviewer_keywords:
- CreateEvidence method [.NET Framework hosting]
- ICorRuntimeHost::CreateEvidence method [.NET Framework hosting]
ms.assetid: e235ea80-b84c-4442-a4c3-fc96c25a8eb9
topic_type:
- apiref
ms.openlocfilehash: 6627fce519934177aefd26a612e5b00ca1941d02
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95715670"
---
# <a name="icorruntimehostcreateevidence-method"></a><span data-ttu-id="753bc-102">ICorRuntimeHost::CreateEvidence — Metoda</span><span class="sxs-lookup"><span data-stu-id="753bc-102">ICorRuntimeHost::CreateEvidence Method</span></span>

<span data-ttu-id="753bc-103">Pobiera wskaźnik interfejsu typu <xref:System.Security.Principal.IIdentity?displayProperty=nameWithType> , który umożliwia hostowi tworzenie dowodu bezpieczeństwa do przekazania do metody [ondomain](icorruntimehost-createdomain-method.md) lub [CreateDomainEx —](icorruntimehost-createdomainex-method.md) .</span><span class="sxs-lookup"><span data-stu-id="753bc-103">Gets an interface pointer of type <xref:System.Security.Principal.IIdentity?displayProperty=nameWithType>, which allows the host to create security evidence to pass to the [CreateDomain](icorruntimehost-createdomain-method.md) or [CreateDomainEx](icorruntimehost-createdomainex-method.md) method.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="753bc-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="753bc-104">Syntax</span></span>  
  
```cpp  
HRESULT CreateEvidence (  
    [out] IUnknown** pEvidence  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="753bc-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="753bc-105">Parameters</span></span>  

 `pEvidence`  
 <span data-ttu-id="753bc-106">określoną Wskaźnik interfejsu do <xref:System.Security.Principal.IIdentity?displayProperty=nameWithType> wystąpienia użytego do utworzenia dowodu bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="753bc-106">[out] A interface pointer to an <xref:System.Security.Principal.IIdentity?displayProperty=nameWithType> instance used to create security evidence.</span></span> <span data-ttu-id="753bc-107">Ten wskaźnik jest wpisywany `IUnknown` , dlatego obiekty wywołujące powinny zwykle wywołać `QueryInterface` na tym interfejsie, aby uzyskać wskaźnik do <xref:System.Security.Principal.IIdentity?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="753bc-107">This pointer is typed `IUnknown`, so callers should typically call `QueryInterface` on this interface to obtain a pointer to an <xref:System.Security.Principal.IIdentity?displayProperty=nameWithType>.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="753bc-108">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="753bc-108">Return Value</span></span>  
  
|<span data-ttu-id="753bc-109">HRESULT</span><span class="sxs-lookup"><span data-stu-id="753bc-109">HRESULT</span></span>|<span data-ttu-id="753bc-110">Opis</span><span class="sxs-lookup"><span data-stu-id="753bc-110">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="753bc-111">S_OK</span><span class="sxs-lookup"><span data-stu-id="753bc-111">S_OK</span></span>|<span data-ttu-id="753bc-112">Operacja zakończyła się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="753bc-112">The operation was successful.</span></span>|  
|<span data-ttu-id="753bc-113">S_FALSE</span><span class="sxs-lookup"><span data-stu-id="753bc-113">S_FALSE</span></span>|<span data-ttu-id="753bc-114">Nie można ukończyć operacji.</span><span class="sxs-lookup"><span data-stu-id="753bc-114">The operation failed to complete.</span></span>|  
|<span data-ttu-id="753bc-115">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="753bc-115">E_FAIL</span></span>|<span data-ttu-id="753bc-116">Wystąpił nieznany, Katastrofalny błąd.</span><span class="sxs-lookup"><span data-stu-id="753bc-116">An unknown, catastrophic failure occurred.</span></span> <span data-ttu-id="753bc-117">Jeśli metoda zwraca E_FAIL, środowisko uruchomieniowe języka wspólnego (CLR) nie jest już możliwe do użycia w procesie.</span><span class="sxs-lookup"><span data-stu-id="753bc-117">If a method returns E_FAIL, the common language runtime (CLR) is no longer usable in the process.</span></span> <span data-ttu-id="753bc-118">Kolejne wywołania interfejsów API hostingu zwracają HOST_E_CLRNOTAVAILABLE.</span><span class="sxs-lookup"><span data-stu-id="753bc-118">Subsequent calls to any hosting APIs return HOST_E_CLRNOTAVAILABLE.</span></span>|  
|<span data-ttu-id="753bc-119">HOST_E_CLRNOTAVAILABLE</span><span class="sxs-lookup"><span data-stu-id="753bc-119">HOST_E_CLRNOTAVAILABLE</span></span>|<span data-ttu-id="753bc-120">Środowisko CLR nie zostało załadowane do procesu lub środowisko CLR znajduje się w stanie, w którym nie można uruchomić kodu zarządzanego lub przetworzyć wywołania pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="753bc-120">The CLR has not been loaded into a process, or the CLR is in a state in which it cannot run managed code or process the call successfully.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="753bc-121">Uwagi</span><span class="sxs-lookup"><span data-stu-id="753bc-121">Remarks</span></span>  

 <span data-ttu-id="753bc-122">Ta metoda zwraca pustą kolekcję, której nie można wypełnić z kodu natywnego.</span><span class="sxs-lookup"><span data-stu-id="753bc-122">This method returns an empty collection that cannot be populated from native code.</span></span> <span data-ttu-id="753bc-123">Zamiast tego należy użyć <xref:System.Security.Policy.Evidence> metody.</span><span class="sxs-lookup"><span data-stu-id="753bc-123">You should use the <xref:System.Security.Policy.Evidence> method instead.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="753bc-124">Wymagania</span><span class="sxs-lookup"><span data-stu-id="753bc-124">Requirements</span></span>  

 <span data-ttu-id="753bc-125">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="753bc-125">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="753bc-126">**Nagłówek:** MSCorEE. h</span><span class="sxs-lookup"><span data-stu-id="753bc-126">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="753bc-127">**Biblioteka:** Uwzględnione jako zasób w MSCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="753bc-127">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="753bc-128">**Wersja .NET Framework:** 1,0, 1,1</span><span class="sxs-lookup"><span data-stu-id="753bc-128">**.NET Framework Version:** 1.0, 1.1</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="753bc-129">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="753bc-129">See also</span></span>

- <xref:System._AppDomain>
- <xref:System.AppDomain>
- [<span data-ttu-id="753bc-130">ICorRuntimeHost — Interfejs</span><span class="sxs-lookup"><span data-stu-id="753bc-130">ICorRuntimeHost Interface</span></span>](icorruntimehost-interface.md)
