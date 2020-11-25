---
title: BlessIWbemServicesObject — funkcja (niezarządzana dokumentacja interfejsu API)
description: Funkcja BlessIWbemServicesObject wskazuje, czy poświadczenia użytkownika zezwalają na dostęp do obiektu IWbemServices
ms.date: 11/06/2017
api_name:
- BlessIWbemServicesObject
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- BlessIWbemServicesObject
helpviewer_keywords:
- BlessIWbemServicesObject function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: 1aab2076f57f938715a3e65481a3540dc52279c6
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95719752"
---
# <a name="blessiwbemservicesobject-function"></a><span data-ttu-id="b8029-103">BlessIWbemServicesObject, funkcja</span><span class="sxs-lookup"><span data-stu-id="b8029-103">BlessIWbemServicesObject function</span></span>

<span data-ttu-id="b8029-104">Wskazuje, czy poświadczenia użytkownika zezwalają na dostęp do określonego obiektu [IWbemServices](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemservices) .</span><span class="sxs-lookup"><span data-stu-id="b8029-104">Indicates whether the user credentials permit access to a specified [IWbemServices](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemservices) object.</span></span>

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a><span data-ttu-id="b8029-105">Składnia</span><span class="sxs-lookup"><span data-stu-id="b8029-105">Syntax</span></span>

```cpp
HRESULT BlessIWbemServicesObject (
   [in] IUnknown* pIUnknown,
   [in] BSTR strUser,
   [in] BSTR strPassword,
   [in] BSTR strAuthority,
   [in] DWORD impLevel,
   [in] DWORD authnLevel
);
```

## <a name="parameters"></a><span data-ttu-id="b8029-106">Parametry</span><span class="sxs-lookup"><span data-stu-id="b8029-106">Parameters</span></span>

`pIWbemServices`\
<span data-ttu-id="b8029-107">podczas Wskaźnik do obiektu usługi WMI.</span><span class="sxs-lookup"><span data-stu-id="b8029-107">[in] A pointer to a WMI service object.</span></span>

`strUser`\
<span data-ttu-id="b8029-108">podczas Nazwa użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b8029-108">[in] The user name.</span></span>

`strPassword`\
<span data-ttu-id="b8029-109">podczas Hasło skojarzone z `strUser` .</span><span class="sxs-lookup"><span data-stu-id="b8029-109">[in] The password associated with `strUser`.</span></span>

`strAuthority`\
<span data-ttu-id="b8029-110">podczas Nazwa domeny użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b8029-110">[in] The domain name of the user.</span></span> <span data-ttu-id="b8029-111">Zobacz funkcję [ConnectServerWmi](connectserverwmi.md) , aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="b8029-111">See the [ConnectServerWmi](connectserverwmi.md) function for more information.</span></span>

`impLevel`\
<span data-ttu-id="b8029-112">podczas Poziom personifikacji.</span><span class="sxs-lookup"><span data-stu-id="b8029-112">[in] The impersonation level.</span></span>

`authnLevel`\
<span data-ttu-id="b8029-113">podczas Poziom autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="b8029-113">[in] The authorization level.</span></span>

## <a name="return-value"></a><span data-ttu-id="b8029-114">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="b8029-114">Return value</span></span>

<span data-ttu-id="b8029-115">Następujące wartości zwracane przez tę funkcję są zdefiniowane w pliku nagłówkowym *Winerror. h* lub można je definiować jako stałe w kodzie:</span><span class="sxs-lookup"><span data-stu-id="b8029-115">The following values returned by this function are defined in the *WinError.h* header file, or you can define them as constants in your code:</span></span>

|<span data-ttu-id="b8029-116">Stała</span><span class="sxs-lookup"><span data-stu-id="b8029-116">Constant</span></span>  |<span data-ttu-id="b8029-117">Wartość</span><span class="sxs-lookup"><span data-stu-id="b8029-117">Value</span></span>  |<span data-ttu-id="b8029-118">Opis</span><span class="sxs-lookup"><span data-stu-id="b8029-118">Description</span></span>  |
|---------|---------|---------|
| `E_INVALIDARG` | <span data-ttu-id="b8029-119">0x80070057</span><span class="sxs-lookup"><span data-stu-id="b8029-119">0x80070057</span></span> | <span data-ttu-id="b8029-120">Co najmniej jeden argument jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="b8029-120">One or more arguments are invalid.</span></span> |
| `E_POINTER` | <span data-ttu-id="b8029-121">0x80004003</span><span class="sxs-lookup"><span data-stu-id="b8029-121">0x80004003</span></span> | <span data-ttu-id="b8029-122">`pIWbemServices` to `null`.</span><span class="sxs-lookup"><span data-stu-id="b8029-122">`pIWbemServices` is `null`.</span></span> |
| `E_FAIL` | <span data-ttu-id="b8029-123">0x80000008</span><span class="sxs-lookup"><span data-stu-id="b8029-123">0x80000008</span></span> | <span data-ttu-id="b8029-124">Wystąpił nieokreślony błąd.</span><span class="sxs-lookup"><span data-stu-id="b8029-124">An unspecified error has occurred.</span></span> |
| `E_OUTOFMEMORY` | <span data-ttu-id="b8029-125">0x80000002</span><span class="sxs-lookup"><span data-stu-id="b8029-125">0x80000002</span></span> | <span data-ttu-id="b8029-126">Za mało dostępnej pamięci, aby wykonać tę operację.</span><span class="sxs-lookup"><span data-stu-id="b8029-126">Insufficient memory is available to perform the operation.</span></span> |
| `S_OK` | <span data-ttu-id="b8029-127">0</span><span class="sxs-lookup"><span data-stu-id="b8029-127">0</span></span> | <span data-ttu-id="b8029-128">Wywołanie funkcji zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="b8029-128">The function call was successful.</span></span> |

## <a name="requirements"></a><span data-ttu-id="b8029-129">Wymagania</span><span class="sxs-lookup"><span data-stu-id="b8029-129">Requirements</span></span>

 <span data-ttu-id="b8029-130">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="b8029-130">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>

 <span data-ttu-id="b8029-131">**Nagłówek:** WMINet_Utils. idl</span><span class="sxs-lookup"><span data-stu-id="b8029-131">**Header:** WMINet_Utils.idl</span></span>

 <span data-ttu-id="b8029-132">**.NET Framework wersje:**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]</span><span class="sxs-lookup"><span data-stu-id="b8029-132">**.NET Framework Versions:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]</span></span>

## <a name="see-also"></a><span data-ttu-id="b8029-133">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="b8029-133">See also</span></span>

- [<span data-ttu-id="b8029-134">WMI i liczniki wydajności (niezarządzana dokumentacja interfejsu API)</span><span class="sxs-lookup"><span data-stu-id="b8029-134">WMI and Performance Counters (Unmanaged API Reference)</span></span>](index.md)
