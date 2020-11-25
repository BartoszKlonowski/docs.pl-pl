---
title: GetHashFromFile — Funkcja
ms.date: 03/30/2017
api_name:
- GetHashFromFile
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- GetHashFromFile
helpviewer_keywords:
- GetHashFromFile function [.NET Framework strong naming]
ms.assetid: b3c526a4-8fb4-4ad6-b6af-42ce9c06492e
topic_type:
- apiref
ms.openlocfilehash: ee9f9cd9a9f35c6c54497ad382bb6f9817d186bd
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95732375"
---
# <a name="gethashfromfile-function"></a><span data-ttu-id="b3e43-102">GetHashFromFile — Funkcja</span><span class="sxs-lookup"><span data-stu-id="b3e43-102">GetHashFromFile Function</span></span>

<span data-ttu-id="b3e43-103">Generuje skrót do zawartości określonego pliku.</span><span class="sxs-lookup"><span data-stu-id="b3e43-103">Generates a hash over the contents of the specified file.</span></span>  
  
 <span data-ttu-id="b3e43-104">Ta funkcja jest przestarzała.</span><span class="sxs-lookup"><span data-stu-id="b3e43-104">This function has been deprecated.</span></span> <span data-ttu-id="b3e43-105">Zamiast tego użyj metody [ICLRStrongName:: GetHashFromFile —](../hosting/iclrstrongname-gethashfromfile-method.md) .</span><span class="sxs-lookup"><span data-stu-id="b3e43-105">Use the [ICLRStrongName::GetHashFromFile](../hosting/iclrstrongname-gethashfromfile-method.md) method instead.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="b3e43-106">Składnia</span><span class="sxs-lookup"><span data-stu-id="b3e43-106">Syntax</span></span>  
  
```cpp  
HRESULT GetHashFromFile (  
    [in]  LPCSTR   szFilePath,  
    [in, out] unsigned int   *piHashAlg,
    [out] BYTE     *pbHash,
    [in]  DWORD    cchHash,
    [out] DWORD    *pchHash  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="b3e43-107">Parametry</span><span class="sxs-lookup"><span data-stu-id="b3e43-107">Parameters</span></span>  

 `szFilePath`  
 <span data-ttu-id="b3e43-108">podczas Nazwa pliku do skrótu.</span><span class="sxs-lookup"><span data-stu-id="b3e43-108">[in] The name of the file to hash.</span></span>  
  
 `piHashAlg`  
 <span data-ttu-id="b3e43-109">[in. out] Algorytm, który ma być używany podczas generowania skrótu.</span><span class="sxs-lookup"><span data-stu-id="b3e43-109">[in, out] The algorithm to use when generating the hash.</span></span> <span data-ttu-id="b3e43-110">Prawidłowymi algorytmami są te zdefiniowane przez interfejs CryptoAPI Win32.</span><span class="sxs-lookup"><span data-stu-id="b3e43-110">Valid algorithms are those defined by the Win32 CryptoAPI.</span></span> <span data-ttu-id="b3e43-111">Jeśli `piHashAlg` jest ustawiona na 0, zostanie użyty domyślny algorytm CALG_SHA-1.</span><span class="sxs-lookup"><span data-stu-id="b3e43-111">If `piHashAlg` is set to 0, the default algorithm CALG_SHA-1 is used.</span></span>  
  
 `pbHash`  
 <span data-ttu-id="b3e43-112">określoną Tablica bajtowa zawierająca wygenerowany skrót.</span><span class="sxs-lookup"><span data-stu-id="b3e43-112">[out] A byte array containing the generated hash.</span></span>  
  
 `cchHash`  
 <span data-ttu-id="b3e43-113">podczas Maksymalny rozmiar buforu, który `pbHash` wskazuje.</span><span class="sxs-lookup"><span data-stu-id="b3e43-113">[in] The maximum size of the buffer that `pbHash` points to.</span></span>  
  
 `pchHash`  
 <span data-ttu-id="b3e43-114">określoną Rozmiar zwracanych wartości (w bajtach) `pbHash` .</span><span class="sxs-lookup"><span data-stu-id="b3e43-114">[out] The size, in bytes, of the returned `pbHash`.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="b3e43-115">Uwagi</span><span class="sxs-lookup"><span data-stu-id="b3e43-115">Remarks</span></span>  

 <span data-ttu-id="b3e43-116">Ta funkcja jest taka sama jak [GetHashFromFileW —](gethashfromfilew-function.md), z tą różnicą, że Specyfikacja nazwy pliku jest ANSI zamiast Unicode.</span><span class="sxs-lookup"><span data-stu-id="b3e43-116">This function is the same as [GetHashFromFileW](gethashfromfilew-function.md), except that the file name specification is ANSI instead of Unicode.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="b3e43-117">Wymagania</span><span class="sxs-lookup"><span data-stu-id="b3e43-117">Requirements</span></span>  

 <span data-ttu-id="b3e43-118">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="b3e43-118">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="b3e43-119">**Nagłówek:** StrongName. h</span><span class="sxs-lookup"><span data-stu-id="b3e43-119">**Header:** StrongName.h</span></span>  
  
 <span data-ttu-id="b3e43-120">**Biblioteka:** Uwzględnione jako zasób w MsCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="b3e43-120">**Library:** Included as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="b3e43-121">**.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="b3e43-121">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="b3e43-122">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="b3e43-122">See also</span></span>

- [<span data-ttu-id="b3e43-123">GetHashFromFile, metoda</span><span class="sxs-lookup"><span data-stu-id="b3e43-123">GetHashFromFile Method</span></span>](../hosting/iclrstrongname-gethashfromfile-method.md)
- [<span data-ttu-id="b3e43-124">GetHashFromFileW, metoda</span><span class="sxs-lookup"><span data-stu-id="b3e43-124">GetHashFromFileW Method</span></span>](../hosting/iclrstrongname-gethashfromfilew-method.md)
- [<span data-ttu-id="b3e43-125">ICLRStrongName — Interfejs</span><span class="sxs-lookup"><span data-stu-id="b3e43-125">ICLRStrongName Interface</span></span>](../hosting/iclrstrongname-interface.md)
