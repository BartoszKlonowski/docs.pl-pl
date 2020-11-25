---
title: SpawnInstance — funkcja (niezarządzana dokumentacja interfejsu API)
description: Funkcja SpawnInstance tworzy nowe wystąpienie klasy.
ms.date: 11/06/2017
api_name:
- SpawnInstance
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- SpawnInstance
helpviewer_keywords:
- SpawnInstance function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: 176bc83dd02381af8c2bc3995a37e7fee7c1bebf
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95732232"
---
# <a name="spawninstance-function"></a><span data-ttu-id="3b224-103">SpawnInstance, funkcja</span><span class="sxs-lookup"><span data-stu-id="3b224-103">SpawnInstance function</span></span>

<span data-ttu-id="3b224-104">Tworzy nowe wystąpienie klasy.</span><span class="sxs-lookup"><span data-stu-id="3b224-104">Creates a new instance of a class.</span></span>
  
[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a><span data-ttu-id="3b224-105">Składnia</span><span class="sxs-lookup"><span data-stu-id="3b224-105">Syntax</span></span>  
  
```cpp  
HRESULT SpawnInstance (
   [in] int                  vFunc,
   [in] IWbemClassObject*    ptr,
   [in] LONG                 lFlags,
   [out] IWbemClassObject**  ppNewInstance);
```  

## <a name="parameters"></a><span data-ttu-id="3b224-106">Parametry</span><span class="sxs-lookup"><span data-stu-id="3b224-106">Parameters</span></span>

`vFunc`  
<span data-ttu-id="3b224-107">podczas Ten parametr jest nieużywany.</span><span class="sxs-lookup"><span data-stu-id="3b224-107">[in] This parameter is unused.</span></span>

`ptr`  
<span data-ttu-id="3b224-108">podczas Wskaźnik do wystąpienia [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) .</span><span class="sxs-lookup"><span data-stu-id="3b224-108">[in] A pointer to an [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) instance.</span></span>

`lFlags`  
<span data-ttu-id="3b224-109">podczas Rezerwacj.</span><span class="sxs-lookup"><span data-stu-id="3b224-109">[in] Reserved.</span></span> <span data-ttu-id="3b224-110">Ten parametr musi być równy 0.</span><span class="sxs-lookup"><span data-stu-id="3b224-110">This parameter must be 0.</span></span>

`ppNewInstance`  
<span data-ttu-id="3b224-111">określoną Odbiera wskaźnik do nowego wystąpienia klasy.</span><span class="sxs-lookup"><span data-stu-id="3b224-111">[out] Receives the pointer to the new instance of the class.</span></span> <span data-ttu-id="3b224-112">Jeśli wystąpi błąd, nowy obiekt nie jest zwracany i `ppNewInstance` pozostaje niemodyfikowany.</span><span class="sxs-lookup"><span data-stu-id="3b224-112">If an error occurs, a new object is not returned, and `ppNewInstance` is left unmodified.</span></span>

## <a name="return-value"></a><span data-ttu-id="3b224-113">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="3b224-113">Return value</span></span>

<span data-ttu-id="3b224-114">Następujące wartości zwracane przez tę funkcję są zdefiniowane w pliku nagłówkowym *WbemCli. h* lub można je definiować jako stałe w kodzie:</span><span class="sxs-lookup"><span data-stu-id="3b224-114">The following values returned by this function are defined in the *WbemCli.h* header file, or you can define them as constants in your code:</span></span>

|<span data-ttu-id="3b224-115">Stała</span><span class="sxs-lookup"><span data-stu-id="3b224-115">Constant</span></span>  |<span data-ttu-id="3b224-116">Wartość</span><span class="sxs-lookup"><span data-stu-id="3b224-116">Value</span></span>  |<span data-ttu-id="3b224-117">Opis</span><span class="sxs-lookup"><span data-stu-id="3b224-117">Description</span></span>  |
|---------|---------|---------|
| `WBEM_E_INCOMPLETE_CLASS` | <span data-ttu-id="3b224-118">0x80041020</span><span class="sxs-lookup"><span data-stu-id="3b224-118">0x80041020</span></span> | <span data-ttu-id="3b224-119">`ptr` nie jest prawidłową definicją klasy i nie można zduplikować nowych wystąpień.</span><span class="sxs-lookup"><span data-stu-id="3b224-119">`ptr` is not a valid class definition and cannot spawn new instances.</span></span> <span data-ttu-id="3b224-120">Jest on niekompletny lub nie został zarejestrowany w usłudze Windows Management przez wywołanie [PutClassWmi](putclasswmi.md).</span><span class="sxs-lookup"><span data-stu-id="3b224-120">Either it is incomplete or it has not been registered with Windows Management by calling [PutClassWmi](putclasswmi.md).</span></span> |
| `WBEM_E_OUT_OF_MEMORY` | <span data-ttu-id="3b224-121">0x80041006</span><span class="sxs-lookup"><span data-stu-id="3b224-121">0x80041006</span></span> | <span data-ttu-id="3b224-122">Za mało dostępnej pamięci, aby ukończyć tę operację.</span><span class="sxs-lookup"><span data-stu-id="3b224-122">Not enough memory is available to complete the operation.</span></span> |
| `WBEM_E_INVALID_PARAMETER` | <span data-ttu-id="3b224-123">0x80041008</span><span class="sxs-lookup"><span data-stu-id="3b224-123">0x80041008</span></span> | <span data-ttu-id="3b224-124">`ppNewClass` to `null`.</span><span class="sxs-lookup"><span data-stu-id="3b224-124">`ppNewClass` is `null`.</span></span> |
| `WBEM_S_NO_ERROR` | <span data-ttu-id="3b224-125">0</span><span class="sxs-lookup"><span data-stu-id="3b224-125">0</span></span> | <span data-ttu-id="3b224-126">Wywołanie funkcji zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="3b224-126">The function call was successful.</span></span>  |
  
## <a name="remarks"></a><span data-ttu-id="3b224-127">Uwagi</span><span class="sxs-lookup"><span data-stu-id="3b224-127">Remarks</span></span>

<span data-ttu-id="3b224-128">Ta funkcja otacza wywołanie metody [IWbemClassObject:: SpawnInstance](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-spawninstance) .</span><span class="sxs-lookup"><span data-stu-id="3b224-128">This function wraps a call to the [IWbemClassObject::SpawnInstance](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-spawninstance) method.</span></span>

<span data-ttu-id="3b224-129">`ptr` musi być definicją klasy uzyskaną z zarządzania systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="3b224-129">`ptr` must be a class definition obtained from Windows Management.</span></span> <span data-ttu-id="3b224-130">(Należy zauważyć, że duplikowanie wystąpienia z wystąpienia jest obsługiwane, ale zwrócone wystąpienie jest puste). Następnie należy użyć tej definicji klasy do tworzenia nowych wystąpień.</span><span class="sxs-lookup"><span data-stu-id="3b224-130">(Note that spawning an instance from an instance is supported but the returned instance is empty.) You then use this class definition to create new instances.</span></span> <span data-ttu-id="3b224-131">Wywołanie funkcji [PutInstanceWmi](putinstancewmi.md) jest wymagane, jeśli zamierzasz napisać wystąpienie do zarządzania systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="3b224-131">A call to the [PutInstanceWmi](putinstancewmi.md) function is required if you intend to write the instance to Windows Management.</span></span>

<span data-ttu-id="3b224-132">Nowy obiekt zwrócony w programie `ppNewClass` automatycznie zostanie podklasą bieżącego obiektu.</span><span class="sxs-lookup"><span data-stu-id="3b224-132">The new object returned in `ppNewClass` automatically becomes a subclass of the current object.</span></span> <span data-ttu-id="3b224-133">Tego zachowania nie można zastąpić.</span><span class="sxs-lookup"><span data-stu-id="3b224-133">This behavior cannot be overridden.</span></span> <span data-ttu-id="3b224-134">Nie istnieje inna metoda, za pomocą której można tworzyć podklasy (klasy pochodne).</span><span class="sxs-lookup"><span data-stu-id="3b224-134">There is no other method by which subclasses (derived classes) can be created.</span></span>

## <a name="requirements"></a><span data-ttu-id="3b224-135">Wymagania</span><span class="sxs-lookup"><span data-stu-id="3b224-135">Requirements</span></span>  

 <span data-ttu-id="3b224-136">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="3b224-136">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="3b224-137">**Nagłówek:** WMINet_Utils. idl</span><span class="sxs-lookup"><span data-stu-id="3b224-137">**Header:** WMINet_Utils.idl</span></span>  
  
 <span data-ttu-id="3b224-138">**.NET Framework wersje:**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]</span><span class="sxs-lookup"><span data-stu-id="3b224-138">**.NET Framework Versions:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="3b224-139">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="3b224-139">See also</span></span>

- [<span data-ttu-id="3b224-140">WMI i liczniki wydajności (niezarządzana dokumentacja interfejsu API)</span><span class="sxs-lookup"><span data-stu-id="3b224-140">WMI and Performance Counters (Unmanaged API Reference)</span></span>](index.md)
