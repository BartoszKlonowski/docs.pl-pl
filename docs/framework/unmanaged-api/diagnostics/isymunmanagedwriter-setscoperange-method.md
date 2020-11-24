---
title: ISymUnmanagedWriter::SetScopeRange — Metoda
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter.SetScopeRange
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter::SetScopeRange
helpviewer_keywords:
- SetScopeRange method [.NET Framework debugging]
- ISymUnmanagedWriter::SetScopeRange method [.NET Framework debugging]
ms.assetid: d4d98676-444b-46ca-bfe6-0d827385cd22
topic_type:
- apiref
ms.openlocfilehash: 06dff4847ec3d15f446f1c89219b10eddb8eec4f
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95683527"
---
# <a name="isymunmanagedwritersetscoperange-method"></a><span data-ttu-id="8bab6-102">ISymUnmanagedWriter::SetScopeRange — Metoda</span><span class="sxs-lookup"><span data-stu-id="8bab6-102">ISymUnmanagedWriter::SetScopeRange Method</span></span>

<span data-ttu-id="8bab6-103">Definiuje zakres przesunięć dla określonego zakresu leksykalnego.</span><span class="sxs-lookup"><span data-stu-id="8bab6-103">Defines the offset range for the specified lexical scope.</span></span> <span data-ttu-id="8bab6-104">Zakres będzie nowym bieżącym zakresem i jest wypychany do stosu zakresów.</span><span class="sxs-lookup"><span data-stu-id="8bab6-104">The scope becomes the new current scope and is pushed onto a stack of scopes.</span></span> <span data-ttu-id="8bab6-105">Zakresy muszą tworzyć hierarchię.</span><span class="sxs-lookup"><span data-stu-id="8bab6-105">Scopes must form a hierarchy.</span></span> <span data-ttu-id="8bab6-106">Elementy równorzędne nie mogą nakładać się na siebie.</span><span class="sxs-lookup"><span data-stu-id="8bab6-106">Siblings are not allowed to overlap.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="8bab6-107">Składnia</span><span class="sxs-lookup"><span data-stu-id="8bab6-107">Syntax</span></span>  
  
```cpp  
HRESULT OpenScope(  
    [in] ULONG32  scopeID,  
    [in] ULONG32  startOffset,  
    [in] ULONG32  endOffset);  
```  
  
## <a name="parameters"></a><span data-ttu-id="8bab6-108">Parametry</span><span class="sxs-lookup"><span data-stu-id="8bab6-108">Parameters</span></span>  

 `scopeId`  
 <span data-ttu-id="8bab6-109">podczas Identyfikator zakresu dla zakresu.</span><span class="sxs-lookup"><span data-stu-id="8bab6-109">[in] The scope identifier for the scope.</span></span>  
  
 `startOffset`  
 <span data-ttu-id="8bab6-110">podczas Przesunięcie, w bajtach, pierwszej instrukcji w zakresie leksykalnym od początku metody.</span><span class="sxs-lookup"><span data-stu-id="8bab6-110">[in] The offset, in bytes, of the first instruction in the lexical scope from the beginning of the method.</span></span>  
  
 `endOffset`  
 <span data-ttu-id="8bab6-111">podczas Przesunięcie, w bajtach, ostatniej instrukcji w zakresie leksykalnym od początku metody.</span><span class="sxs-lookup"><span data-stu-id="8bab6-111">[in] The offset, in bytes, of the last instruction in the lexical scope from the beginning of the method.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="8bab6-112">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="8bab6-112">Return Value</span></span>  

 <span data-ttu-id="8bab6-113">S_OK, jeśli metoda się powiedzie; w przeciwnym razie E_FAIL lub inny kod błędu.</span><span class="sxs-lookup"><span data-stu-id="8bab6-113">S_OK if the method succeeds; otherwise, E_FAIL or some other error code.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="8bab6-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="8bab6-114">Remarks</span></span>  

 <span data-ttu-id="8bab6-115">[ISymUnmanagedWriter:: OpenScope —](isymunmanagedwriter-openscope-method.md) zwraca nieprzezroczysty identyfikator zakresu, którego można użyć w `ISymUnmanagedWriter::SetScopeRange` celu zdefiniowania początkowego i końcowego przesunięcia zakresu w późniejszym czasie.</span><span class="sxs-lookup"><span data-stu-id="8bab6-115">[ISymUnmanagedWriter::OpenScope](isymunmanagedwriter-openscope-method.md) returns an opaque scope identifier that can be used with `ISymUnmanagedWriter::SetScopeRange` to define a scope's starting and ending offset at a later time.</span></span> <span data-ttu-id="8bab6-116">W takim przypadku przesunięcia przesłane do `ISymUnmanagedWriter::OpenScope` i [ISymUnmanagedWriter:: CloseScope —](isymunmanagedwriter-closescope-method.md) są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="8bab6-116">In this case, the offsets passed to `ISymUnmanagedWriter::OpenScope` and [ISymUnmanagedWriter::CloseScope](isymunmanagedwriter-closescope-method.md) are ignored.</span></span> <span data-ttu-id="8bab6-117">Identyfikatory zakresów są prawidłowe tylko w bieżącej metodzie.</span><span class="sxs-lookup"><span data-stu-id="8bab6-117">Scope identifiers are only valid in the current method.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="8bab6-118">Wymagania</span><span class="sxs-lookup"><span data-stu-id="8bab6-118">Requirements</span></span>  

 <span data-ttu-id="8bab6-119">**Nagłówek:** CorSym. idl, CorSym. h</span><span class="sxs-lookup"><span data-stu-id="8bab6-119">**Header:** CorSym.idl, CorSym.h</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="8bab6-120">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="8bab6-120">See also</span></span>

- [<span data-ttu-id="8bab6-121">ISymUnmanagedWriter — Interfejs</span><span class="sxs-lookup"><span data-stu-id="8bab6-121">ISymUnmanagedWriter Interface</span></span>](isymunmanagedwriter-interface.md)
