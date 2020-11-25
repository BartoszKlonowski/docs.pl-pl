---
title: IHostMemoryManager::VirtualProtect — Metoda
ms.date: 03/30/2017
api_name:
- IHostMemoryManager.VirtualProtect
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostMemoryManager::VirtualProtect
helpviewer_keywords:
- IHostMemoryManager::VirtualProtect method [.NET Framework hosting]
- VirtualProtect method [.NET Framework hosting]
ms.assetid: 13be0299-df0d-4951-aabf-0676a30b385f
topic_type:
- apiref
ms.openlocfilehash: 9822e5a1fb09e9d3bce541ff63cf766ae8611789
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95731257"
---
# <a name="ihostmemorymanagervirtualprotect-method"></a><span data-ttu-id="b38f9-102">IHostMemoryManager::VirtualProtect — Metoda</span><span class="sxs-lookup"><span data-stu-id="b38f9-102">IHostMemoryManager::VirtualProtect Method</span></span>

<span data-ttu-id="b38f9-103">Służy jako otoka logiczna dla odpowiadającej jej funkcji Win32.</span><span class="sxs-lookup"><span data-stu-id="b38f9-103">Serves as a logical wrapper for the corresponding Win32 function.</span></span> <span data-ttu-id="b38f9-104">Implementacja Win32 `VirtualProtect` zmiany ochrony w regionie zatwierdzonych stron w wirtualnej przestrzeni adresowej procesu wywołującego.</span><span class="sxs-lookup"><span data-stu-id="b38f9-104">The Win32 implementation of `VirtualProtect` changes the protection on a region of committed pages in the virtual address space of the calling process.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="b38f9-105">Składnia</span><span class="sxs-lookup"><span data-stu-id="b38f9-105">Syntax</span></span>  
  
```cpp  
HRESULT VirtualProtect (  
    [in]  void*   lpAddress,  
    [in]  SIZE_T  dwSize,  
    [in]  DWORD   flNewProtect,  
    [out] DWORD*  pflOldProtect  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="b38f9-106">Parametry</span><span class="sxs-lookup"><span data-stu-id="b38f9-106">Parameters</span></span>  

 `lpAddress`  
 <span data-ttu-id="b38f9-107">podczas Wskaźnik na adres podstawowy pamięci wirtualnej, której atrybuty ochrony mają zostać zmienione.</span><span class="sxs-lookup"><span data-stu-id="b38f9-107">[in] A pointer to the base address of the virtual memory whose protection attributes are to be changed.</span></span>  
  
 `dwSize`  
 <span data-ttu-id="b38f9-108">podczas Rozmiar (w bajtach) regionu stron pamięci, który ma zostać zmieniony.</span><span class="sxs-lookup"><span data-stu-id="b38f9-108">[in] The size, in bytes, of the region of memory pages to be changed.</span></span>  
  
 `flNewProtect`  
 <span data-ttu-id="b38f9-109">podczas Typ ochrony pamięci, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="b38f9-109">[in] The type of memory protection to apply.</span></span>  
  
 `pflOldProtect`  
 <span data-ttu-id="b38f9-110">określoną Wskaźnik do poprzedniej wartości ochrony pamięci.</span><span class="sxs-lookup"><span data-stu-id="b38f9-110">[out] A pointer to the previous memory protection value.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="b38f9-111">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="b38f9-111">Return Value</span></span>  
  
|<span data-ttu-id="b38f9-112">HRESULT</span><span class="sxs-lookup"><span data-stu-id="b38f9-112">HRESULT</span></span>|<span data-ttu-id="b38f9-113">Opis</span><span class="sxs-lookup"><span data-stu-id="b38f9-113">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="b38f9-114">S_OK</span><span class="sxs-lookup"><span data-stu-id="b38f9-114">S_OK</span></span>|<span data-ttu-id="b38f9-115">`VirtualProtect` pomyślnie zwrócono.</span><span class="sxs-lookup"><span data-stu-id="b38f9-115">`VirtualProtect` returned successfully.</span></span>|  
|<span data-ttu-id="b38f9-116">HOST_E_CLRNOTAVAILABLE</span><span class="sxs-lookup"><span data-stu-id="b38f9-116">HOST_E_CLRNOTAVAILABLE</span></span>|<span data-ttu-id="b38f9-117">Środowisko uruchomieniowe języka wspólnego (CLR) nie zostało załadowane do procesu lub środowisko CLR znajduje się w stanie, w którym nie można uruchomić kodu zarządzanego lub przetworzyć wywołania pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="b38f9-117">The common language runtime (CLR) has not been loaded into a process, or the CLR is in a state in which it cannot run managed code or process the call successfully.</span></span>|  
|<span data-ttu-id="b38f9-118">HOST_E_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="b38f9-118">HOST_E_TIMEOUT</span></span>|<span data-ttu-id="b38f9-119">Upłynął limit czasu połączenia.</span><span class="sxs-lookup"><span data-stu-id="b38f9-119">The call timed out.</span></span>|  
|<span data-ttu-id="b38f9-120">HOST_E_NOT_OWNER</span><span class="sxs-lookup"><span data-stu-id="b38f9-120">HOST_E_NOT_OWNER</span></span>|<span data-ttu-id="b38f9-121">Obiekt wywołujący nie jest właocicielem blokady.</span><span class="sxs-lookup"><span data-stu-id="b38f9-121">The caller does not own the lock.</span></span>|  
|<span data-ttu-id="b38f9-122">HOST_E_ABANDONED</span><span class="sxs-lookup"><span data-stu-id="b38f9-122">HOST_E_ABANDONED</span></span>|<span data-ttu-id="b38f9-123">Zdarzenie zostało anulowane podczas oczekiwania na niego zablokowanego wątku lub włókna.</span><span class="sxs-lookup"><span data-stu-id="b38f9-123">An event was canceled while a blocked thread or fiber was waiting on it.</span></span>|  
|<span data-ttu-id="b38f9-124">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="b38f9-124">E_FAIL</span></span>|<span data-ttu-id="b38f9-125">Wystąpił nieznany błąd krytyczny.</span><span class="sxs-lookup"><span data-stu-id="b38f9-125">An unknown catastrophic failure occurred.</span></span> <span data-ttu-id="b38f9-126">Gdy metoda zwraca E_FAIL, środowisko CLR nie będzie już można używać w procesie.</span><span class="sxs-lookup"><span data-stu-id="b38f9-126">When a method returns E_FAIL, the CLR is no longer usable within the process.</span></span> <span data-ttu-id="b38f9-127">Kolejne wywołania metod hostingu zwracają HOST_E_CLRNOTAVAILABLE.</span><span class="sxs-lookup"><span data-stu-id="b38f9-127">Subsequent calls to hosting methods return HOST_E_CLRNOTAVAILABLE.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="b38f9-128">Uwagi</span><span class="sxs-lookup"><span data-stu-id="b38f9-128">Remarks</span></span>  

 <span data-ttu-id="b38f9-129">Ta implementacja `VirtualProtect` zwraca wartość HRESULT, podczas gdy implementacja Win32 zwraca wartość różną od zera, aby wskazywała powodzenie, i wartość zerową, aby wskazać błąd.</span><span class="sxs-lookup"><span data-stu-id="b38f9-129">This implementation of `VirtualProtect` returns an HRESULT value, while the Win32 implementation returns a non-zero value to indicate success, and a zero value to indicate failure.</span></span> <span data-ttu-id="b38f9-130">Aby uzyskać więcej informacji, zobacz dokumentację platformy systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="b38f9-130">For more information, see the Windows Platform documentation.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="b38f9-131">Wymagania</span><span class="sxs-lookup"><span data-stu-id="b38f9-131">Requirements</span></span>  

 <span data-ttu-id="b38f9-132">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="b38f9-132">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="b38f9-133">**Nagłówek:** MSCorEE. h</span><span class="sxs-lookup"><span data-stu-id="b38f9-133">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="b38f9-134">**Biblioteka:** Uwzględnione jako zasób w MSCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="b38f9-134">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="b38f9-135">**.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="b38f9-135">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="b38f9-136">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="b38f9-136">See also</span></span>

- [<span data-ttu-id="b38f9-137">IHostMemoryManager — Interfejs</span><span class="sxs-lookup"><span data-stu-id="b38f9-137">IHostMemoryManager Interface</span></span>](ihostmemorymanager-interface.md)
