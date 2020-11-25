---
title: NextMethod — funkcja (niezarządzana dokumentacja interfejsu API)
description: Funkcja NextMethod pobiera następną metodę w wyliczeniu.
ms.date: 11/06/2017
api_name:
- NextMethod
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- NextMethod
helpviewer_keywords:
- NextMethod function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: a0466aee47b0a6142870640c78b43f49e221ac2b
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95726772"
---
# <a name="nextmethod-function"></a><span data-ttu-id="a72c1-103">NextMethod, funkcja</span><span class="sxs-lookup"><span data-stu-id="a72c1-103">NextMethod function</span></span>

<span data-ttu-id="a72c1-104">Pobiera następną metodę w wyliczeniu, która rozpoczyna się od wywołania do [BeginMethodEnumeration](beginmethodenumeration.md).</span><span class="sxs-lookup"><span data-stu-id="a72c1-104">Retrieves the next method in an enumeration that begins with a call to [BeginMethodEnumeration](beginmethodenumeration.md).</span></span>  

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a><span data-ttu-id="a72c1-105">Składnia</span><span class="sxs-lookup"><span data-stu-id="a72c1-105">Syntax</span></span>  
  
```cpp  
HRESULT NextMethod (
   [in] int                 vFunc,
   [in] IWbemClassObject*   ptr,
   [in] LONG                lFlags,
   [out] BSTR*              pName,
   [out] IWbemClassObject** ppInSignature,
   [out] IWbemClassObject** ppOutSignature
);
```  

## <a name="parameters"></a><span data-ttu-id="a72c1-106">Parametry</span><span class="sxs-lookup"><span data-stu-id="a72c1-106">Parameters</span></span>

`vFunc`  
<span data-ttu-id="a72c1-107">podczas Ten parametr jest nieużywany.</span><span class="sxs-lookup"><span data-stu-id="a72c1-107">[in] This parameter is unused.</span></span>

`ptr`  
<span data-ttu-id="a72c1-108">podczas Wskaźnik do wystąpienia [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) .</span><span class="sxs-lookup"><span data-stu-id="a72c1-108">[in] A pointer to an [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) instance.</span></span>

`lFlags`  
<span data-ttu-id="a72c1-109">podczas Rezerwacj.</span><span class="sxs-lookup"><span data-stu-id="a72c1-109">[in] Reserved.</span></span> <span data-ttu-id="a72c1-110">Ten parametr musi być równy 0.</span><span class="sxs-lookup"><span data-stu-id="a72c1-110">This parameter must be 0.</span></span>

`pName`  
<span data-ttu-id="a72c1-111">określoną Wskaźnik wskazujący `null` przed wywołaniem.</span><span class="sxs-lookup"><span data-stu-id="a72c1-111">[out] A pointer that points to `null` prior to the call.</span></span> <span data-ttu-id="a72c1-112">Gdy funkcja zwraca, adres nowej `BSTR` , która zawiera nazwę metody.</span><span class="sxs-lookup"><span data-stu-id="a72c1-112">When the function returns, the address of a new `BSTR` that contains the method name.</span></span>

`ppSignatureIn`  
<span data-ttu-id="a72c1-113">określoną Wskaźnik, który odbiera wskaźnik do elementu [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) , który zawiera `in` parametry dla metody.</span><span class="sxs-lookup"><span data-stu-id="a72c1-113">[out] A pointer that receives a pointer to an [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) that contains the `in` parameters for the method.</span></span>

`ppSignatureOut`  
<span data-ttu-id="a72c1-114">określoną Wskaźnik, który odbiera wskaźnik do elementu [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) , który zawiera `out` parametry dla metody.</span><span class="sxs-lookup"><span data-stu-id="a72c1-114">[out] A pointer that receives a pointer to an [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) that contains the `out` parameters for the method.</span></span>

## <a name="return-value"></a><span data-ttu-id="a72c1-115">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="a72c1-115">Return value</span></span>

<span data-ttu-id="a72c1-116">Następujące wartości zwracane przez tę funkcję są zdefiniowane w pliku nagłówkowym *WbemCli. h* lub można je definiować jako stałe w kodzie:</span><span class="sxs-lookup"><span data-stu-id="a72c1-116">The following values returned by this function are defined in the *WbemCli.h* header file, or you can define them as constants in your code:</span></span>

|<span data-ttu-id="a72c1-117">Stała</span><span class="sxs-lookup"><span data-stu-id="a72c1-117">Constant</span></span>  |<span data-ttu-id="a72c1-118">Wartość</span><span class="sxs-lookup"><span data-stu-id="a72c1-118">Value</span></span>  |<span data-ttu-id="a72c1-119">Opis</span><span class="sxs-lookup"><span data-stu-id="a72c1-119">Description</span></span>  |
|---------|---------|---------|
| `WBEM_E_UNEXPECTED` | <span data-ttu-id="a72c1-120">0x8004101d</span><span class="sxs-lookup"><span data-stu-id="a72c1-120">0x8004101d</span></span> | <span data-ttu-id="a72c1-121">Brak wywołania [`BeginEnumeration`](beginenumeration.md) funkcji.</span><span class="sxs-lookup"><span data-stu-id="a72c1-121">There was no call to the [`BeginEnumeration`](beginenumeration.md) function.</span></span> |
| `WBEM_S_NO_ERROR` | <span data-ttu-id="a72c1-122">0</span><span class="sxs-lookup"><span data-stu-id="a72c1-122">0</span></span> | <span data-ttu-id="a72c1-123">Wywołanie funkcji zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="a72c1-123">The function call was successful.</span></span>  |
| `WBEM_S_NO_MORE_DATA` | <span data-ttu-id="a72c1-124">0x40005</span><span class="sxs-lookup"><span data-stu-id="a72c1-124">0x40005</span></span> | <span data-ttu-id="a72c1-125">Nie ma więcej właściwości w wyliczeniu.</span><span class="sxs-lookup"><span data-stu-id="a72c1-125">There are no more properties in the enumeration.</span></span> |
  
## <a name="remarks"></a><span data-ttu-id="a72c1-126">Uwagi</span><span class="sxs-lookup"><span data-stu-id="a72c1-126">Remarks</span></span>

<span data-ttu-id="a72c1-127">Ta funkcja otacza wywołanie metody [IWbemClassObject:: NextMethod](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-nextmethod) .</span><span class="sxs-lookup"><span data-stu-id="a72c1-127">This function wraps a call to the [IWbemClassObject::NextMethod](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-nextmethod) method.</span></span>

<span data-ttu-id="a72c1-128">Obiekt wywołujący rozpoczyna sekwencję wyliczenia, wywołując funkcję [BeginMethodEnumeration](beginmethodenumeration.md) , a następnie wywołuje funkcję [NextMethod] do momentu, gdy funkcja zwróci wartość `WBEM_S_NO_MORE_DATA` .</span><span class="sxs-lookup"><span data-stu-id="a72c1-128">The caller begins the enumeration sequence by calling the [BeginMethodEnumeration](beginmethodenumeration.md) function, and then calls the [NextMethod] function until the function returns `WBEM_S_NO_MORE_DATA`.</span></span> <span data-ttu-id="a72c1-129">Opcjonalnie obiekt wywołujący kończy sekwencję przez wywołanie [EndMethodEnumeration](endmethodenumeration.md).</span><span class="sxs-lookup"><span data-stu-id="a72c1-129">Optionally, the caller finishes the sequence by calling [EndMethodEnumeration](endmethodenumeration.md).</span></span> <span data-ttu-id="a72c1-130">Obiekt wywołujący może zakończyć Wyliczenie wczesne przez wywołanie [EndMethodEnumeration](endmethodenumeration.md) w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="a72c1-130">The caller may terminate the enumeration early by calling [EndMethodEnumeration](endmethodenumeration.md) at any time.</span></span>

## <a name="example"></a><span data-ttu-id="a72c1-131">Przykład</span><span class="sxs-lookup"><span data-stu-id="a72c1-131">Example</span></span>

<span data-ttu-id="a72c1-132">Aby zapoznać się z przykładem w języku C++, zobacz [IWbemClassObject:: NextMethod](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-nextmethod) .</span><span class="sxs-lookup"><span data-stu-id="a72c1-132">For a C++ example, see the [IWbemClassObject::NextMethod](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-nextmethod) method.</span></span>

## <a name="requirements"></a><span data-ttu-id="a72c1-133">Wymagania</span><span class="sxs-lookup"><span data-stu-id="a72c1-133">Requirements</span></span>  

 <span data-ttu-id="a72c1-134">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="a72c1-134">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="a72c1-135">**Nagłówek:** WMINet_Utils. idl</span><span class="sxs-lookup"><span data-stu-id="a72c1-135">**Header:** WMINet_Utils.idl</span></span>  
  
 <span data-ttu-id="a72c1-136">**.NET Framework wersje:**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]</span><span class="sxs-lookup"><span data-stu-id="a72c1-136">**.NET Framework Versions:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a72c1-137">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="a72c1-137">See also</span></span>

- [<span data-ttu-id="a72c1-138">WMI i liczniki wydajności (niezarządzana dokumentacja interfejsu API)</span><span class="sxs-lookup"><span data-stu-id="a72c1-138">WMI and Performance Counters (Unmanaged API Reference)</span></span>](index.md)
