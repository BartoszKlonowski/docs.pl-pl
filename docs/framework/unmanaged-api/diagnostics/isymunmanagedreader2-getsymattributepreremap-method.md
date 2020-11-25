---
title: ISymUnmanagedReader2::GetSymAttributePreRemap — Metoda
ms.date: 03/30/2017
api_name:
- ISymUnmanagedReader2.GetSymAttributePreRemap
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedReader2::GetSymAttributePreRemap
helpviewer_keywords:
- GetSymAttributePreRemap method [.NET Framework debugging]
- ISymUnmanagedReader2::GetSymAttributePreRemap method [.NET Framework debugging]
ms.assetid: 7580d546-a709-40c5-ad02-aa70d774fd0b
topic_type:
- apiref
ms.openlocfilehash: 812c0d08930efff9140c6e897d3f93c4909e8464
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95709092"
---
# <a name="isymunmanagedreader2getsymattributepreremap-method"></a><span data-ttu-id="34d24-102">ISymUnmanagedReader2::GetSymAttributePreRemap — Metoda</span><span class="sxs-lookup"><span data-stu-id="34d24-102">ISymUnmanagedReader2::GetSymAttributePreRemap Method</span></span>

<span data-ttu-id="34d24-103">Pobiera atrybut niestandardowy na podstawie jego nazwy.</span><span class="sxs-lookup"><span data-stu-id="34d24-103">Gets a custom attribute based upon its name.</span></span> <span data-ttu-id="34d24-104">W przeciwieństwie do atrybutów niestandardowych metadanych, te atrybuty są przechowywane w magazynie symboli.</span><span class="sxs-lookup"><span data-stu-id="34d24-104">Unlike metadata custom attributes, these attributes are held in the symbol store.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="34d24-105">Składnia</span><span class="sxs-lookup"><span data-stu-id="34d24-105">Syntax</span></span>  
  
```cpp  
HRESULT GetSymAttributePreRemap(  
    [in]  mdToken  parent,  
    [in]  WCHAR    *name,  
    [in]  ULONG32  cBuffer,  
    [out] ULONG32  *pcBuffer,  
    [out, size_is(cBuffer),  
        length_is(*pcBuffer)] BYTE buffer[]);  
```  
  
## <a name="parameters"></a><span data-ttu-id="34d24-106">Parametry</span><span class="sxs-lookup"><span data-stu-id="34d24-106">Parameters</span></span>  

 `parent`  
 <span data-ttu-id="34d24-107">podczas Token metadanych elementu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="34d24-107">[in] The metadata token of the parent.</span></span>  
  
 `name`  
 <span data-ttu-id="34d24-108">podczas Wskaźnik do `WCHAR` , który zawiera nazwę.</span><span class="sxs-lookup"><span data-stu-id="34d24-108">[in] A pointer to a `WCHAR` that contains the name.</span></span>  
  
 `cBuffer`  
 <span data-ttu-id="34d24-109">podczas `ULONG32` Wskazuje rozmiar `buffer` tablicy.</span><span class="sxs-lookup"><span data-stu-id="34d24-109">[in] A `ULONG32` that indicates the size of the `buffer` array.</span></span>  
  
 `pcBuffer`  
 <span data-ttu-id="34d24-110">określoną Wskaźnik do obiektu `ULONG32` , który odbiera rozmiar buforu wymaganego do uwzględnienia bajtów atrybutu.</span><span class="sxs-lookup"><span data-stu-id="34d24-110">[out] A pointer to a `ULONG32` that receives the size of the buffer required to contain the attribute bytes.</span></span>  
  
 `buffer`  
 <span data-ttu-id="34d24-111">określoną Wskaźnik do buforu, który odbiera bajty atrybutu.</span><span class="sxs-lookup"><span data-stu-id="34d24-111">[out] A pointer to the buffer that receives the attribute bytes.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="34d24-112">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="34d24-112">Return Value</span></span>  

 <span data-ttu-id="34d24-113">S_OK, jeśli metoda się powiedzie; w przeciwnym razie E_FAIL lub inny kod błędu.</span><span class="sxs-lookup"><span data-stu-id="34d24-113">S_OK if the method succeeds; otherwise, E_FAIL or some other error code.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="34d24-114">Wymagania</span><span class="sxs-lookup"><span data-stu-id="34d24-114">Requirements</span></span>  

 <span data-ttu-id="34d24-115">**Nagłówek:** CorSym. idl, CorSym. h</span><span class="sxs-lookup"><span data-stu-id="34d24-115">**Header:** CorSym.idl, CorSym.h</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="34d24-116">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="34d24-116">See also</span></span>

- [<span data-ttu-id="34d24-117">ISymUnmanagedReader2 — Interfejs</span><span class="sxs-lookup"><span data-stu-id="34d24-117">ISymUnmanagedReader2 Interface</span></span>](isymunmanagedreader2-interface.md)
