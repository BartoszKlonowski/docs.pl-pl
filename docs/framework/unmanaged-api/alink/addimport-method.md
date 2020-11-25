---
title: AddImport — Metoda
ms.date: 03/30/2017
api_name:
- AddImport
- IALink.AddImport
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- AddImport
helpviewer_keywords:
- AddImport method
ms.assetid: 4fedf8a0-08c8-43d0-aa00-20f2a521c991
topic_type:
- apiref
ms.openlocfilehash: cf73ada36be66edb3fa267d61873ae9acb088a34
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95717048"
---
# <a name="addimport-method"></a><span data-ttu-id="013f6-102">AddImport — Metoda</span><span class="sxs-lookup"><span data-stu-id="013f6-102">AddImport Method</span></span>

<span data-ttu-id="013f6-103">Dodaje Importy do zestawu.</span><span class="sxs-lookup"><span data-stu-id="013f6-103">Adds imports to the assembly.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="013f6-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="013f6-104">Syntax</span></span>  
  
```cpp  
HRESULT AddImport(  
    mdAssembly      AssemblyID,  
    mdToken         ImportToken,  
    DWORD           dwFlags,  
    mdFile*         pFileToken  
) PURE;  
```  
  
## <a name="parameters"></a><span data-ttu-id="013f6-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="013f6-105">Parameters</span></span>  

 `AssemblyID`  
 <span data-ttu-id="013f6-106">Unikatowy identyfikator zestawu, który ma zostać rozszerzony.</span><span class="sxs-lookup"><span data-stu-id="013f6-106">Unique ID of assembly to be augmented.</span></span>  
  
 `ImportToken`  
 <span data-ttu-id="013f6-107">Unikatowy identyfikator, pobrany z [metody ImportFile —](importfile-method.md), pliku do zaimportowania.</span><span class="sxs-lookup"><span data-stu-id="013f6-107">Unique ID, retrieved from [ImportFile Method](importfile-method.md), of file to be imported.</span></span>  
  
 `dwFlags`  
 <span data-ttu-id="013f6-108">Flagi FileDef modelu COM+, takie jak `ffContainsNoMetaData` i `ffWriteable` .</span><span class="sxs-lookup"><span data-stu-id="013f6-108">COM+ FileDef flags such as `ffContainsNoMetaData` and `ffWriteable`.</span></span> <span data-ttu-id="013f6-109">`dwFlags` jest przenoszona do [metody DefineFile —](../metadata/imetadataassemblyemit-definefile-method.md).</span><span class="sxs-lookup"><span data-stu-id="013f6-109">`dwFlags` is passed to [DefineFile Method](../metadata/imetadataassemblyemit-definefile-method.md).</span></span>  
  
 `pFileToken`  
 <span data-ttu-id="013f6-110">Wskaźnik do tokenu, który odbiera identyfikator dla tworzonego pliku.</span><span class="sxs-lookup"><span data-stu-id="013f6-110">Pointer to token that receives the ID for the resulting file.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="013f6-111">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="013f6-111">Return Value</span></span>  

 <span data-ttu-id="013f6-112">Zwraca S_OK, jeśli metoda zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="013f6-112">Returns S_OK if the method succeeds.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="013f6-113">Wymagania</span><span class="sxs-lookup"><span data-stu-id="013f6-113">Requirements</span></span>  

 <span data-ttu-id="013f6-114">Wymaga Alink. h</span><span class="sxs-lookup"><span data-stu-id="013f6-114">Requires alink.h</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="013f6-115">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="013f6-115">See also</span></span>

- [<span data-ttu-id="013f6-116">IALink — Interfejs</span><span class="sxs-lookup"><span data-stu-id="013f6-116">IALink Interface</span></span>](ialink-interface.md)
- [<span data-ttu-id="013f6-117">IALink2 — Interfejs</span><span class="sxs-lookup"><span data-stu-id="013f6-117">IALink2 Interface</span></span>](ialink2-interface.md)
- [<span data-ttu-id="013f6-118">ALink — interfejs API</span><span class="sxs-lookup"><span data-stu-id="013f6-118">ALink API</span></span>](index.md)
