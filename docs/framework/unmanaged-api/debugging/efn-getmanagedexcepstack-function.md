---
title: _EFN_GetManagedExcepStack — Funkcja
ms.date: 03/30/2017
api_name:
- _EFN_GetManagedExcepStack
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- _EFN_GetManagedExcepStack
helpviewer_keywords:
- _EFN_GetManagedExcepStack function [.NET Framework debugging]
ms.assetid: 21ceed9e-62b2-4024-b027-6d095109955a
topic_type:
- apiref
ms.openlocfilehash: b86277836b1be48c9f8020d59071aba8c5b1e457
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95676234"
---
# <a name="_efn_getmanagedexcepstack-function"></a><span data-ttu-id="a8366-102">\_\_Funkcja EFN GetManagedExcepStack</span><span class="sxs-lookup"><span data-stu-id="a8366-102">\_EFN\_GetManagedExcepStack Function</span></span>

<span data-ttu-id="a8366-103">Dany adres obiektu wyjątku zarządzanego zwraca wersję ciągu śledzenia stosu zawartych wewnątrz.</span><span class="sxs-lookup"><span data-stu-id="a8366-103">Given a managed exception object address, returns a string version of the stack trace contained inside.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="a8366-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="a8366-104">Syntax</span></span>  
  
```cpp  
HRESULT _EFN_GetManagedExcepStack(  
    [in]  PDEBUG_CLIENT Client,  
    [in]  ULONG64       StackObjAddr,  
    [out] __out_ecount(cbString) PSTR szStackString,  
    [out] ULONG         cbString  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="a8366-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="a8366-105">Parameters</span></span>  

 `Client`  
 <span data-ttu-id="a8366-106">podczas Debugowany klient.</span><span class="sxs-lookup"><span data-stu-id="a8366-106">[in] The client being debugged.</span></span>  
  
 `StackObjAddr`  
 <span data-ttu-id="a8366-107">podczas Wskaźnik obiektu zarządzanego, pochodzący z <xref:System.Exception> .</span><span class="sxs-lookup"><span data-stu-id="a8366-107">[in] A managed object pointer, derived from <xref:System.Exception>.</span></span>  
  
 <span data-ttu-id="a8366-108">szStackString</span><span class="sxs-lookup"><span data-stu-id="a8366-108">szStackString</span></span>  
 <span data-ttu-id="a8366-109">określoną Zwrócony ciąg.</span><span class="sxs-lookup"><span data-stu-id="a8366-109">[out] The returned string.</span></span>  
  
 `cbString`  
 <span data-ttu-id="a8366-110">określoną Liczba znaków dostępnych w buforze ciągów.</span><span class="sxs-lookup"><span data-stu-id="a8366-110">[out] The number of characters available in the string buffer.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="a8366-111">Uwagi</span><span class="sxs-lookup"><span data-stu-id="a8366-111">Remarks</span></span>  

 <span data-ttu-id="a8366-112">W przypadku braku kodu zarządzanego w wątku, który jest obecnie w kontekście, funkcja zwraca wartość HRESULT SOS_E_NOMANAGEDCODE z wartością instrumentu 0xa0 i kodem błędu 0x1000.</span><span class="sxs-lookup"><span data-stu-id="a8366-112">If there is no managed code on the thread currently in context, the function returns HRESULT SOS_E_NOMANAGEDCODE with a facility value of 0xa0 and an error code of 0x1000.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="a8366-113">Wymagania</span><span class="sxs-lookup"><span data-stu-id="a8366-113">Requirements</span></span>  

 <span data-ttu-id="a8366-114">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="a8366-114">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="a8366-115">**Nagłówek:** SOS_Stacktrace. h</span><span class="sxs-lookup"><span data-stu-id="a8366-115">**Header:** SOS_Stacktrace.h</span></span>  
  
 <span data-ttu-id="a8366-116">**Wersja .NET Framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="a8366-116">**.NET Framework Version:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a8366-117">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="a8366-117">See also</span></span>

- [<span data-ttu-id="a8366-118">Debugowanie statycznych funkcji globalnych</span><span class="sxs-lookup"><span data-stu-id="a8366-118">Debugging Global Static Functions</span></span>](debugging-global-static-functions.md)
