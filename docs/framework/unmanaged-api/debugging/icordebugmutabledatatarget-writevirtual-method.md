---
title: 'ICorDebugMutableDataTarget:: WriteVirtual —, Metoda'
ms.date: 03/30/2017
ms.assetid: 80833648-58a7-491a-8dc8-9a48e9bb3adc
ms.openlocfilehash: 453ab23e292c5eab4a8300c32bf76743b787750d
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95709339"
---
# <a name="icordebugmutabledatatargetwritevirtual-method"></a><span data-ttu-id="3a25d-102">ICorDebugMutableDataTarget:: WriteVirtual —, Metoda</span><span class="sxs-lookup"><span data-stu-id="3a25d-102">ICorDebugMutableDataTarget::WriteVirtual Method</span></span>

<span data-ttu-id="3a25d-103">Zapisuje pamięć w przestrzeni adresowej procesu docelowego.</span><span class="sxs-lookup"><span data-stu-id="3a25d-103">Writes memory into the target process address space.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="3a25d-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="3a25d-104">Syntax</span></span>  
  
```cpp  
HRESULT WriteVirtual(  
   [in] CORDB_ADDRESS address,  
   [in, size_is(bytesRequested)] const BYTE * pBuffer,  
   [in] ULONG32 bytesRequested);  
```  
  
## <a name="parameters"></a><span data-ttu-id="3a25d-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="3a25d-105">Parameters</span></span>  

 `address`  
 <span data-ttu-id="3a25d-106">podczas Adres, pod którym należy napisać zawartość `pBuffer` .</span><span class="sxs-lookup"><span data-stu-id="3a25d-106">[in] The address at which to write the contents of `pBuffer`.</span></span>  
  
 `pBuffer`  
 <span data-ttu-id="3a25d-107">podczas Wskaźnik do tablicy bajtów zawierającej bajty do zapisania.</span><span class="sxs-lookup"><span data-stu-id="3a25d-107">[in] A pointer to a byte array that contains the bytes to be written.</span></span>  
  
 `address`  
 <span data-ttu-id="3a25d-108">podczas Liczba bajtów w `pBuffer` .</span><span class="sxs-lookup"><span data-stu-id="3a25d-108">[in] The number of bytes in `pBuffer`.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="3a25d-109">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="3a25d-109">Return Value</span></span>  

 <span data-ttu-id="3a25d-110">`S_OK` po powodzeniu lub w dowolnym innym przypadku `HRESULT` awarii.</span><span class="sxs-lookup"><span data-stu-id="3a25d-110">`S_OK` on success, or any other `HRESULT` on failure.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="3a25d-111">Uwagi</span><span class="sxs-lookup"><span data-stu-id="3a25d-111">Remarks</span></span>  

 <span data-ttu-id="3a25d-112">Jeśli nie można zapisać żadnych bajtów, wywołanie metody zakończy się niepowodzeniem bez zmiany jakichkolwiek bajtów w docelowej przestrzeni adresowej.</span><span class="sxs-lookup"><span data-stu-id="3a25d-112">If any bytes cannot be written, the method call fails without changing any bytes in the target address space.</span></span> <span data-ttu-id="3a25d-113">(W przeciwnym razie element docelowy będzie w stanie niespójnym, co sprawia, że dalsze debugowanie jest niezawodne).</span><span class="sxs-lookup"><span data-stu-id="3a25d-113">(Otherwise, the target would be in an inconsistent state that makes further debugging unreliable.)</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="3a25d-114">Wymagania</span><span class="sxs-lookup"><span data-stu-id="3a25d-114">Requirements</span></span>  

 <span data-ttu-id="3a25d-115">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="3a25d-115">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="3a25d-116">**Nagłówek:** CorDebug. idl, CorDebug. h</span><span class="sxs-lookup"><span data-stu-id="3a25d-116">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="3a25d-117">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="3a25d-117">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="3a25d-118">**.NET Framework wersje:**[!INCLUDE[net_current_v46plus](../../../../includes/net-current-v46plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="3a25d-118">**.NET Framework Versions:** [!INCLUDE[net_current_v46plus](../../../../includes/net-current-v46plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="3a25d-119">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="3a25d-119">See also</span></span>

- [<span data-ttu-id="3a25d-120">ICorDebugMutableDataTarget, interfejs</span><span class="sxs-lookup"><span data-stu-id="3a25d-120">ICorDebugMutableDataTarget Interface</span></span>](icordebugmutabledatatarget-interface.md)
- [<span data-ttu-id="3a25d-121">Debugowanie — Interfejsy</span><span class="sxs-lookup"><span data-stu-id="3a25d-121">Debugging Interfaces</span></span>](debugging-interfaces.md)
