---
title: DeleteMethod — funkcja (niezarządzana dokumentacja interfejsu API)
description: Funkcja DeleteMethod usuwa określoną metodę z definicji klasy CIM.
ms.date: 11/06/2017
api_name:
- DeleteMethod
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- DeleteMethod
helpviewer_keywords:
- DeleteMethod function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: 8ca58ed3510360b20577890055e4284869d1bf94
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95708104"
---
# <a name="deletemethod-function"></a><span data-ttu-id="0b06d-103">DeleteMethod, funkcja</span><span class="sxs-lookup"><span data-stu-id="0b06d-103">DeleteMethod function</span></span>

<span data-ttu-id="0b06d-104">Usuwa określoną metodę z definicji klasy CIM.</span><span class="sxs-lookup"><span data-stu-id="0b06d-104">Deletes the specified method from a CIM class definition.</span></span>

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a><span data-ttu-id="0b06d-105">Składnia</span><span class="sxs-lookup"><span data-stu-id="0b06d-105">Syntax</span></span>  
  
```cpp  
HRESULT Delete (
   [in] int               vFunc,
   [in] IWbemClassObject* ptr,
   [in] LPCWSTR           wszName
);
```  

## <a name="parameters"></a><span data-ttu-id="0b06d-106">Parametry</span><span class="sxs-lookup"><span data-stu-id="0b06d-106">Parameters</span></span>

`vFunc`  
<span data-ttu-id="0b06d-107">podczas Ten parametr jest nieużywany.</span><span class="sxs-lookup"><span data-stu-id="0b06d-107">[in] This parameter is unused.</span></span>

`ptr`  
<span data-ttu-id="0b06d-108">podczas Wskaźnik do wystąpienia [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) .</span><span class="sxs-lookup"><span data-stu-id="0b06d-108">[in] A pointer to an [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) instance.</span></span>

`wszName`  
<span data-ttu-id="0b06d-109">podczas Nazwa metody do usunięcia z tabeli klas.</span><span class="sxs-lookup"><span data-stu-id="0b06d-109">[in] The name of the method to remove from the class table.</span></span> <span data-ttu-id="0b06d-110">`wszName` musi być wskaźnikiem prawidłowym `LPCWSTR` .</span><span class="sxs-lookup"><span data-stu-id="0b06d-110">`wszName` must be a pointer to a valid `LPCWSTR`.</span></span>

## <a name="return-value"></a><span data-ttu-id="0b06d-111">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="0b06d-111">Return value</span></span>

<span data-ttu-id="0b06d-112">Następujące wartości zwracane przez tę funkcję są zdefiniowane w pliku nagłówkowym *WbemCli. h* lub można je definiować jako stałe w kodzie:</span><span class="sxs-lookup"><span data-stu-id="0b06d-112">The following values returned by this function are defined in the *WbemCli.h* header file, or you can define them as constants in your code:</span></span>

|<span data-ttu-id="0b06d-113">Stała</span><span class="sxs-lookup"><span data-stu-id="0b06d-113">Constant</span></span>  |<span data-ttu-id="0b06d-114">Wartość</span><span class="sxs-lookup"><span data-stu-id="0b06d-114">Value</span></span>  |<span data-ttu-id="0b06d-115">Opis</span><span class="sxs-lookup"><span data-stu-id="0b06d-115">Description</span></span>  |
|---------|---------|---------|
| `WBEM_E_NOT_FOUND` | <span data-ttu-id="0b06d-116">0x80041002</span><span class="sxs-lookup"><span data-stu-id="0b06d-116">0x80041002</span></span> | <span data-ttu-id="0b06d-117">Określona metoda nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="0b06d-117">The specified method does not exist.</span></span> |
| `WBEM_E_OUT_OF_MEMORY` | <span data-ttu-id="0b06d-118">0x80041006</span><span class="sxs-lookup"><span data-stu-id="0b06d-118">0x80041006</span></span> | <span data-ttu-id="0b06d-119">Za mało pamięci, aby ukończyć operację.</span><span class="sxs-lookup"><span data-stu-id="0b06d-119">There is not enough memory to complete the operation.</span></span> |
| `WBEM_S_NO_ERROR` | <span data-ttu-id="0b06d-120">0</span><span class="sxs-lookup"><span data-stu-id="0b06d-120">0</span></span> | <span data-ttu-id="0b06d-121">Wywołanie funkcji zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="0b06d-121">The function call was successful.</span></span>  |

## <a name="remarks"></a><span data-ttu-id="0b06d-122">Uwagi</span><span class="sxs-lookup"><span data-stu-id="0b06d-122">Remarks</span></span>

<span data-ttu-id="0b06d-123">Ta funkcja otacza wywołanie metody [IWbemClassObject::D eletemethod](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-deletemethod) .</span><span class="sxs-lookup"><span data-stu-id="0b06d-123">This function wraps a call to the [IWbemClassObject::DeleteMethod](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-deletemethod) method.</span></span>

<span data-ttu-id="0b06d-124">Usuwanie metody nie jest obsługiwane dla wskaźników [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) , które wskazują wystąpienia modelu wspólnych informacji.</span><span class="sxs-lookup"><span data-stu-id="0b06d-124">Method deletion is not supported for [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) pointers that point to CIM instances.</span></span>

## <a name="requirements"></a><span data-ttu-id="0b06d-125">Wymagania</span><span class="sxs-lookup"><span data-stu-id="0b06d-125">Requirements</span></span>  

 <span data-ttu-id="0b06d-126">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="0b06d-126">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="0b06d-127">**Nagłówek:** WMINet_Utils. idl</span><span class="sxs-lookup"><span data-stu-id="0b06d-127">**Header:** WMINet_Utils.idl</span></span>  
  
 <span data-ttu-id="0b06d-128">**.NET Framework wersje:**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]</span><span class="sxs-lookup"><span data-stu-id="0b06d-128">**.NET Framework Versions:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="0b06d-129">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="0b06d-129">See also</span></span>

- [<span data-ttu-id="0b06d-130">WMI i liczniki wydajności (niezarządzana dokumentacja interfejsu API)</span><span class="sxs-lookup"><span data-stu-id="0b06d-130">WMI and Performance Counters (Unmanaged API Reference)</span></span>](index.md)
