---
title: AddFile2 — Metoda
ms.date: 03/30/2017
api_name:
- AddFile2
- IALink2.AddFile2
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- AddFile2
helpviewer_keywords:
- AddFile2 method
ms.assetid: 03bc49bf-a89b-4fb6-a88d-97482e061195
topic_type:
- apiref
ms.openlocfilehash: cff6707496c7d9657796deb8bf6fa9165ff295a2
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95717087"
---
# <a name="addfile2-method"></a><span data-ttu-id="44f9f-102">AddFile2 — Metoda</span><span class="sxs-lookup"><span data-stu-id="44f9f-102">AddFile2 Method</span></span>

<span data-ttu-id="44f9f-103">Dodaje pliki do zestawu.</span><span class="sxs-lookup"><span data-stu-id="44f9f-103">Adds files to the assembly.</span></span> <span data-ttu-id="44f9f-104">Może również służyć do tworzenia niezwiązanych modułów.</span><span class="sxs-lookup"><span data-stu-id="44f9f-104">Can also be used to create unbound modules.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="44f9f-105">Składnia</span><span class="sxs-lookup"><span data-stu-id="44f9f-105">Syntax</span></span>  
  
```cpp  
HRESULT AddFile2(  
    mdAssembly AssemblyID,  
    LPCWSTR pszFilename,  
    DWORD dwFlags,  
    IMetaDataEmit2* pEmitter,  
    mdFile* pFileToken  
) PURE;  
```  
  
## <a name="parameters"></a><span data-ttu-id="44f9f-106">Parametry</span><span class="sxs-lookup"><span data-stu-id="44f9f-106">Parameters</span></span>  

 `AssemblyID`  
 <span data-ttu-id="44f9f-107">Identyfikator zestawu, do którego zostanie dodany plik.</span><span class="sxs-lookup"><span data-stu-id="44f9f-107">ID for the assembly to which the file is added.</span></span>  
  
 `pszFilename`  
 <span data-ttu-id="44f9f-108">Nazwa pliku, który ma zostać dodany.</span><span class="sxs-lookup"><span data-stu-id="44f9f-108">Name of the file to be added.</span></span>  
  
 `dwFlags`  
 <span data-ttu-id="44f9f-109">`FileDef`Flagi com+, takie jak `ffContainsNoMetaData` i `ffWriteable` .</span><span class="sxs-lookup"><span data-stu-id="44f9f-109">COM+ `FileDef` flags such as `ffContainsNoMetaData` and `ffWriteable`.</span></span> <span data-ttu-id="44f9f-110">`dwFlags` jest przenoszona do [metody DefineFile —](../metadata/imetadataassemblyemit-definefile-method.md).</span><span class="sxs-lookup"><span data-stu-id="44f9f-110">`dwFlags` is passed to [DefineFile Method](../metadata/imetadataassemblyemit-definefile-method.md).</span></span>  
  
 `pEmitter`  
 <span data-ttu-id="44f9f-111">Interfejs do interfejsu [interfejsu IMetaDataEmit2](../metadata/imetadataemit2-interface.md) .</span><span class="sxs-lookup"><span data-stu-id="44f9f-111">Interface to [IMetaDataEmit2 Interface](../metadata/imetadataemit2-interface.md) interface.</span></span>  
  
 `pFileToken`  
 <span data-ttu-id="44f9f-112">Odbiera identyfikator dodawanego pliku.</span><span class="sxs-lookup"><span data-stu-id="44f9f-112">Receives ID for the file being added.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="44f9f-113">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="44f9f-113">Return Value</span></span>  

 <span data-ttu-id="44f9f-114">Zwraca S_OK, jeśli metoda zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="44f9f-114">Returns S_OK if the method succeeds.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="44f9f-115">Wymagania</span><span class="sxs-lookup"><span data-stu-id="44f9f-115">Requirements</span></span>  

 <span data-ttu-id="44f9f-116">Wymaga Alink. h.</span><span class="sxs-lookup"><span data-stu-id="44f9f-116">Requires alink.h.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="44f9f-117">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="44f9f-117">See also</span></span>

- [<span data-ttu-id="44f9f-118">IALink2 — Interfejs</span><span class="sxs-lookup"><span data-stu-id="44f9f-118">IALink2 Interface</span></span>](ialink2-interface.md)
- [<span data-ttu-id="44f9f-119">IALink — Interfejs</span><span class="sxs-lookup"><span data-stu-id="44f9f-119">IALink Interface</span></span>](ialink-interface.md)
- [<span data-ttu-id="44f9f-120">ALink — interfejs API</span><span class="sxs-lookup"><span data-stu-id="44f9f-120">ALink API</span></span>](index.md)
