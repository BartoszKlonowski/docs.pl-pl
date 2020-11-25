---
title: ISymUnmanagedBinder2::GetReaderForFile2 — Metoda
ms.date: 03/30/2017
api_name:
- ISymUnmanagedBinder2.GetReaderForFile2
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedBinder2::GetReaderForFile2
helpviewer_keywords:
- ISymUnmanagedBinder2::GetReaderForFile2 method [.NET Framework debugging]
- GetReaderForFile2 method [.NET Framework debugging]
ms.assetid: dd92dcaf-403c-464d-a254-21594985dddd
topic_type:
- apiref
ms.openlocfilehash: e0fc6cf2a08de4a00cb8b7f98d3922df98f427c5
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95706973"
---
# <a name="isymunmanagedbinder2getreaderforfile2-method"></a><span data-ttu-id="d476c-102">ISymUnmanagedBinder2::GetReaderForFile2 — Metoda</span><span class="sxs-lookup"><span data-stu-id="d476c-102">ISymUnmanagedBinder2::GetReaderForFile2 Method</span></span>

<span data-ttu-id="d476c-103">Podanym interfejsem metadanych i nazwą pliku zwraca poprawny interfejs [ISymUnmanagedReader](isymunmanagedreader-interface.md) , który odczytuje symbole debugowania skojarzone z modułem.</span><span class="sxs-lookup"><span data-stu-id="d476c-103">Given a metadata interface and a file name, returns the correct [ISymUnmanagedReader](isymunmanagedreader-interface.md) interface that will read the debugging symbols associated with the module.</span></span>  
  
 <span data-ttu-id="d476c-104">Ta metoda zapewnia bardziej rozległe wyszukiwanie pliku bazy danych programu (PDB) niż Metoda [ISymUnmanagedBinder:: GetReaderForFile —](isymunmanagedbinder-getreaderforfile-method.md) .</span><span class="sxs-lookup"><span data-stu-id="d476c-104">This method provides a more extensive search for the program database (PDB) file than the [ISymUnmanagedBinder::GetReaderForFile](isymunmanagedbinder-getreaderforfile-method.md) method.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="d476c-105">Składnia</span><span class="sxs-lookup"><span data-stu-id="d476c-105">Syntax</span></span>  
  
```cpp  
HRESULT GetReaderForFile2(  
    [in]  IUnknown     *importer,  
    [in]  const WCHAR  *fileName,  
    [in]  const WCHAR  *searchPath,  
    [in]  ULONG32      searchPolicy,  
    [out,retval] ISymUnmanagedReader  **pRetVal);  
```  
  
## <a name="parameters"></a><span data-ttu-id="d476c-106">Parametry</span><span class="sxs-lookup"><span data-stu-id="d476c-106">Parameters</span></span>  

 `importer`  
 <span data-ttu-id="d476c-107">podczas Wskaźnik do interfejsu importowania metadanych.</span><span class="sxs-lookup"><span data-stu-id="d476c-107">[in] A pointer to the metadata import interface.</span></span>  
  
 `fileName`  
 <span data-ttu-id="d476c-108">podczas Wskaźnik do nazwy pliku.</span><span class="sxs-lookup"><span data-stu-id="d476c-108">[in] A pointer to the file name.</span></span>  
  
 `searchPath`  
 <span data-ttu-id="d476c-109">podczas Wskaźnik do ścieżki wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="d476c-109">[in] A pointer to the search path.</span></span>  
  
 `searchPolicy`  
 <span data-ttu-id="d476c-110">podczas Wartość wyliczenia [CorSymSearchPolicyAttributes —](corsymsearchpolicyattributes-enumeration.md) , która określa zasady, które mają być używane podczas wyszukiwania czytnika symboli.</span><span class="sxs-lookup"><span data-stu-id="d476c-110">[in] A value of the [CorSymSearchPolicyAttributes](corsymsearchpolicyattributes-enumeration.md) enumeration that specifies the policy to be used when doing a search for a symbol reader.</span></span>  
  
 `pRetVal`  
 <span data-ttu-id="d476c-111">określoną Wskaźnik, który jest ustawiony na zwracany Interfejs [ISymUnmanagedReader](isymunmanagedreader-interface.md) .</span><span class="sxs-lookup"><span data-stu-id="d476c-111">[out] A pointer that is set to the returned [ISymUnmanagedReader](isymunmanagedreader-interface.md) interface.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="d476c-112">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="d476c-112">Return Value</span></span>  

 <span data-ttu-id="d476c-113">S_OK, jeśli metoda się powiedzie; w przeciwnym razie E_FAIL lub inny kod błędu.</span><span class="sxs-lookup"><span data-stu-id="d476c-113">S_OK if the method succeeds; otherwise, E_FAIL or some other error code.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="d476c-114">Wymagania</span><span class="sxs-lookup"><span data-stu-id="d476c-114">Requirements</span></span>  

 <span data-ttu-id="d476c-115">**Nagłówek:** CorSym. idl, CorSym. h</span><span class="sxs-lookup"><span data-stu-id="d476c-115">**Header:** CorSym.idl, CorSym.h</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="d476c-116">Uwagi</span><span class="sxs-lookup"><span data-stu-id="d476c-116">Remarks</span></span>  

 <span data-ttu-id="d476c-117">Ta wersja metody może wyszukiwać plik PDB w obszarach innych niż bezpośrednio obok modułu.</span><span class="sxs-lookup"><span data-stu-id="d476c-117">This version of the method can search for the PDB file in areas other than right next to the module.</span></span> <span data-ttu-id="d476c-118">Zasady wyszukiwania można kontrolować, łącząc [CorSymSearchPolicyAttributes —](corsymsearchpolicyattributes-enumeration.md).</span><span class="sxs-lookup"><span data-stu-id="d476c-118">The search policy can be controlled by combining [CorSymSearchPolicyAttributes](corsymsearchpolicyattributes-enumeration.md).</span></span> <span data-ttu-id="d476c-119">Program `AllowReferencePathAccess | AllowSymbolServerAccess` wyszukuje na przykład plik PDB obok pliku wykonywalnego i na serwerze symboli, ale nie wysyła zapytania do rejestru ani nie używa ścieżki w pliku wykonywalnym.</span><span class="sxs-lookup"><span data-stu-id="d476c-119">For example, `AllowReferencePathAccess | AllowSymbolServerAccess` looks for the PDB next to the executable file and on a symbol server, but does not query the registry or use the path in the executable file.</span></span> <span data-ttu-id="d476c-120">W przypadku `searchPath` podanego parametru te katalogi będą zawsze przeszukiwane.</span><span class="sxs-lookup"><span data-stu-id="d476c-120">If the `searchPath` parameter is provided, those directories will always be searched.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="d476c-121">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="d476c-121">See also</span></span>

- [<span data-ttu-id="d476c-122">ISymUnmanagedBinder2 — Interfejs</span><span class="sxs-lookup"><span data-stu-id="d476c-122">ISymUnmanagedBinder2 Interface</span></span>](isymunmanagedbinder2-interface.md)
- [<span data-ttu-id="d476c-123">GetReaderForFile, metoda</span><span class="sxs-lookup"><span data-stu-id="d476c-123">GetReaderForFile Method</span></span>](isymunmanagedbinder-getreaderforfile-method.md)
