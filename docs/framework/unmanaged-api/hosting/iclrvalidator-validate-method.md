---
title: ICLRValidator::Validate — Metoda
ms.date: 03/30/2017
api_name:
- ICLRValidator.Validate
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRValidator::Validate
helpviewer_keywords:
- Validate method, ICLRValidator interface [.NET Framework hosting]
- ICLRValidator::Validate method [.NET Framework hosting]
ms.assetid: 0b1b432a-d234-4002-839b-81366c3a8bdc
topic_type:
- apiref
ms.openlocfilehash: 4ce50f7706583f291d2e6a141d40ab6dd3e4b3e2
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95674388"
---
# <a name="iclrvalidatorvalidate-method"></a><span data-ttu-id="37fb8-102">ICLRValidator::Validate — Metoda</span><span class="sxs-lookup"><span data-stu-id="37fb8-102">ICLRValidator::Validate Method</span></span>

<span data-ttu-id="37fb8-103">Sprawdza poprawność przenośnego pliku wykonywalnego (PE) lub języka pośredniego firmy Microsoft (MSIL) w określonym pliku.</span><span class="sxs-lookup"><span data-stu-id="37fb8-103">Validates the portable executable (PE) or Microsoft intermediate language (MSIL) in the specified file.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="37fb8-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="37fb8-104">Syntax</span></span>  
  
```cpp  
HRESULT Validate (  
    [in] IVEHandler        *veh,  
    [in] unsigned long      ulAppDomainId,  
    [in] unsigned long      ulFlags,  
    [in] unsigned long      ulMaxError,  
    [in] unsigned long      token,  
    [in] LPWSTR             fileName,  
    [in, size_is(ulSize)] BYTE *pe,  
    [in] unsigned long      ulSize  
);
```  
  
## <a name="parameters"></a><span data-ttu-id="37fb8-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="37fb8-105">Parameters</span></span>  

 `veh`  
 <span data-ttu-id="37fb8-106">podczas Wskaźnik do `IVEHandler` wystąpienia, które obsługuje błędy walidacji.</span><span class="sxs-lookup"><span data-stu-id="37fb8-106">[in] A pointer to an `IVEHandler` instance that handles validation errors.</span></span>  
  
 `ulAppDomainId`  
 <span data-ttu-id="37fb8-107">podczas Identyfikator dla bieżącego <xref:System.AppDomain> .</span><span class="sxs-lookup"><span data-stu-id="37fb8-107">[in] The identifier for the current <xref:System.AppDomain>.</span></span>  
  
 `ulFlags`  
 <span data-ttu-id="37fb8-108">podczas Kombinacja wartości [ValidatorFlags —](validatorflags-enumeration.md) wskazujących rodzaj walidacji, który powinien zostać wykonany.</span><span class="sxs-lookup"><span data-stu-id="37fb8-108">[in] A combination of [ValidatorFlags](validatorflags-enumeration.md) values, indicating the kind of validation that should be performed.</span></span>  
  
 `ulMaxError`  
 <span data-ttu-id="37fb8-109">podczas Maksymalna liczba błędów, które należy pozostawić przed wyjściem z walidacji.</span><span class="sxs-lookup"><span data-stu-id="37fb8-109">[in] The maximum number of errors to allow before exiting the validation.</span></span>  
  
 `token`  
 <span data-ttu-id="37fb8-110">podczas Przestrzeń.</span><span class="sxs-lookup"><span data-stu-id="37fb8-110">[in] Unused.</span></span>  
  
 `fileName`  
 <span data-ttu-id="37fb8-111">podczas Nazwa pliku do zweryfikowania.</span><span class="sxs-lookup"><span data-stu-id="37fb8-111">[in] The name of the file to be validated.</span></span>  
  
 `pe`  
 <span data-ttu-id="37fb8-112">podczas Wskaźnik do buforu pliku.</span><span class="sxs-lookup"><span data-stu-id="37fb8-112">[in] A pointer to the file buffer.</span></span>  
  
 `ulSize`  
 <span data-ttu-id="37fb8-113">podczas Rozmiar pliku, który ma być zweryfikowany w bajtach.</span><span class="sxs-lookup"><span data-stu-id="37fb8-113">[in] The size, in bytes, of the file to be validated.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="37fb8-114">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="37fb8-114">Return Value</span></span>  
  
|<span data-ttu-id="37fb8-115">HRESULT</span><span class="sxs-lookup"><span data-stu-id="37fb8-115">HRESULT</span></span>|<span data-ttu-id="37fb8-116">Opis</span><span class="sxs-lookup"><span data-stu-id="37fb8-116">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="37fb8-117">S_OK</span><span class="sxs-lookup"><span data-stu-id="37fb8-117">S_OK</span></span>|<span data-ttu-id="37fb8-118">`Validate` pomyślnie zwrócono.</span><span class="sxs-lookup"><span data-stu-id="37fb8-118">`Validate` returned successfully.</span></span>|  
|<span data-ttu-id="37fb8-119">HOST_E_CLRNOTAVAILABLE</span><span class="sxs-lookup"><span data-stu-id="37fb8-119">HOST_E_CLRNOTAVAILABLE</span></span>|<span data-ttu-id="37fb8-120">Środowisko uruchomieniowe języka wspólnego (CLR) nie zostało załadowane do procesu lub środowisko CLR znajduje się w stanie, w którym nie można uruchomić kodu zarządzanego lub przetworzyć wywołania pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="37fb8-120">The common language runtime (CLR) has not been loaded into a process, or the CLR is in a state in which it cannot run managed code or process the call successfully.</span></span>|  
|<span data-ttu-id="37fb8-121">HOST_E_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="37fb8-121">HOST_E_TIMEOUT</span></span>|<span data-ttu-id="37fb8-122">Upłynął limit czasu połączenia.</span><span class="sxs-lookup"><span data-stu-id="37fb8-122">The call timed out.</span></span>|  
|<span data-ttu-id="37fb8-123">HOST_E_NOT_OWNER</span><span class="sxs-lookup"><span data-stu-id="37fb8-123">HOST_E_NOT_OWNER</span></span>|<span data-ttu-id="37fb8-124">Obiekt wywołujący nie jest właocicielem blokady.</span><span class="sxs-lookup"><span data-stu-id="37fb8-124">The caller does not own the lock.</span></span>|  
|<span data-ttu-id="37fb8-125">HOST_E_ABANDONED</span><span class="sxs-lookup"><span data-stu-id="37fb8-125">HOST_E_ABANDONED</span></span>|<span data-ttu-id="37fb8-126">Zdarzenie zostało anulowane podczas oczekiwania na niego zablokowanego wątku lub włókna.</span><span class="sxs-lookup"><span data-stu-id="37fb8-126">An event was canceled while a blocked thread or fiber was waiting on it.</span></span>|  
|<span data-ttu-id="37fb8-127">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="37fb8-127">E_FAIL</span></span>|<span data-ttu-id="37fb8-128">Wystąpił nieznany błąd krytyczny.</span><span class="sxs-lookup"><span data-stu-id="37fb8-128">An unknown catastrophic failure occurred.</span></span> <span data-ttu-id="37fb8-129">Gdy metoda zwraca E_FAIL, środowisko CLR nie będzie już można używać w procesie.</span><span class="sxs-lookup"><span data-stu-id="37fb8-129">When a method returns E_FAIL, the CLR is no longer usable within the process.</span></span> <span data-ttu-id="37fb8-130">Kolejne wywołania metod hostingu zwracają HOST_E_CLRNOTAVAILABLE.</span><span class="sxs-lookup"><span data-stu-id="37fb8-130">Subsequent calls to hosting methods return HOST_E_CLRNOTAVAILABLE.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="37fb8-131">Wymagania</span><span class="sxs-lookup"><span data-stu-id="37fb8-131">Requirements</span></span>  

 <span data-ttu-id="37fb8-132">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="37fb8-132">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="37fb8-133">**Nagłówek:** IValidator. idl, IValidator. h</span><span class="sxs-lookup"><span data-stu-id="37fb8-133">**Header:** IValidator.idl, IValidator.h</span></span>  
  
 <span data-ttu-id="37fb8-134">**Biblioteka:** Uwzględnione jako zasób w MSCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="37fb8-134">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="37fb8-135">**.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="37fb8-135">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="37fb8-136">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="37fb8-136">See also</span></span>

- [<span data-ttu-id="37fb8-137">ICLRValidator — Interfejs</span><span class="sxs-lookup"><span data-stu-id="37fb8-137">ICLRValidator Interface</span></span>](iclrvalidator-interface.md)
