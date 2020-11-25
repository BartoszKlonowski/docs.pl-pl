---
title: 'ICorDebugMergedAssemblyRecord:: getculture — Metoda'
ms.date: 03/30/2017
ms.assetid: 030b2f8c-8c21-40b7-855d-3afa78975a17
ms.openlocfilehash: 636d0fd25d345f513e00504b9eb5adb4f0c03b0f
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95710652"
---
# <a name="icordebugmergedassemblyrecordgetculture-method"></a><span data-ttu-id="07fd1-102">ICorDebugMergedAssemblyRecord:: getculture — Metoda</span><span class="sxs-lookup"><span data-stu-id="07fd1-102">ICorDebugMergedAssemblyRecord::GetCulture Method</span></span>

<span data-ttu-id="07fd1-103">Pobiera ciąg nazwy kultury zestawu.</span><span class="sxs-lookup"><span data-stu-id="07fd1-103">Gets the culture name string of the assembly.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="07fd1-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="07fd1-104">Syntax</span></span>  
  
```cpp  
HRESULT GetCulture(  
   [in] ULONG32 cchCulture,
   [out] ULONG32 *pcchCulture,
   [out, size_is(cchCulture), length_is(*pcchCulture)] WCHAR szCulture[]  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="07fd1-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="07fd1-105">Parameters</span></span>  

 `cchCulture`  
 <span data-ttu-id="07fd1-106">podczas Liczba znaków w `szCulture` buforze.</span><span class="sxs-lookup"><span data-stu-id="07fd1-106">[in] The number of characters in the `szCulture` buffer.</span></span>  
  
 `pcchCulture`  
 <span data-ttu-id="07fd1-107">określoną Liczba znaków rzeczywiście zapisywana w `szCulture` buforze.</span><span class="sxs-lookup"><span data-stu-id="07fd1-107">[out] The number of characters actually written to the `szCulture` buffer.</span></span>  
  
 `szCulture`  
 <span data-ttu-id="07fd1-108">określoną Tablica znaków, która zawiera nazwę kultury.</span><span class="sxs-lookup"><span data-stu-id="07fd1-108">[out] A character array that contains the culture name.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="07fd1-109">Uwagi</span><span class="sxs-lookup"><span data-stu-id="07fd1-109">Remarks</span></span>  

 <span data-ttu-id="07fd1-110">Nazwa kultury jest unikatowym ciągiem, który identyfikuje kulturę, na przykład "en-US" (dla kultury angielskiej (Stany Zjednoczone)) lub "neutralną" (dla kultury neutralnej).</span><span class="sxs-lookup"><span data-stu-id="07fd1-110">The culture name is a unique string that identifies a culture, such as "en-US" (for the English (United States) culture), or "neutral" (for a neutral culture).</span></span>  
  
> [!NOTE]
> <span data-ttu-id="07fd1-111">Ta metoda jest dostępna tylko z .NET Native.</span><span class="sxs-lookup"><span data-stu-id="07fd1-111">This method is available with .NET Native only.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="07fd1-112">Wymagania</span><span class="sxs-lookup"><span data-stu-id="07fd1-112">Requirements</span></span>  

 <span data-ttu-id="07fd1-113">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="07fd1-113">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="07fd1-114">**Nagłówek:** CorDebug. idl, CorDebug. h</span><span class="sxs-lookup"><span data-stu-id="07fd1-114">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="07fd1-115">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="07fd1-115">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="07fd1-116">**.NET Framework wersje:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]</span><span class="sxs-lookup"><span data-stu-id="07fd1-116">**.NET Framework Versions:** [!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="07fd1-117">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="07fd1-117">See also</span></span>

- [<span data-ttu-id="07fd1-118">ICorDebugMergedAssemblyRecord, interfejs</span><span class="sxs-lookup"><span data-stu-id="07fd1-118">ICorDebugMergedAssemblyRecord Interface</span></span>](icordebugmergedassemblyrecord-interface.md)
- [<span data-ttu-id="07fd1-119">Debugowanie — Interfejsy</span><span class="sxs-lookup"><span data-stu-id="07fd1-119">Debugging Interfaces</span></span>](debugging-interfaces.md)
