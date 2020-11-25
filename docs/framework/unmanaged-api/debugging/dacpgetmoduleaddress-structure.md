---
title: DacpGetModuleAddress, struktura
ms.date: 01/16/2019
api.name:
- DacpGetModuleAddress Structure
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- DacpGetModuleAddress Structure
helpviewer.keywords:
- DacpGetModuleAddress Structure [.NET Framework debugging]
topic_type:
- apiref
author: cshung
ms.author: andrewau
ms.openlocfilehash: a65fa9974165fa36e59a7fb83dca6dd902f7d8dc
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95724398"
---
# <a name="dacpgetmoduleaddress-structure"></a><span data-ttu-id="7be11-102">DacpGetModuleAddress, struktura</span><span class="sxs-lookup"><span data-stu-id="7be11-102">DacpGetModuleAddress Structure</span></span>

<span data-ttu-id="7be11-103">Definiuje kontener dla żądania adresu modułu.</span><span class="sxs-lookup"><span data-stu-id="7be11-103">Defines the container for a module address request.</span></span>

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="syntax"></a><span data-ttu-id="7be11-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="7be11-104">Syntax</span></span>

```cpp
struct DacpGetModuleAddress
{
    CLRDATA_ADDRESS ModulePtr;
};
```

## <a name="members"></a><span data-ttu-id="7be11-105">Elementy członkowskie</span><span class="sxs-lookup"><span data-stu-id="7be11-105">Members</span></span>

| <span data-ttu-id="7be11-106">Członek</span><span class="sxs-lookup"><span data-stu-id="7be11-106">Member</span></span>      | <span data-ttu-id="7be11-107">Opis</span><span class="sxs-lookup"><span data-stu-id="7be11-107">Description</span></span>                |
| ----------- | -------------------------- |
| `ModulePtr` | <span data-ttu-id="7be11-108">Wskaźnik do modułu.</span><span class="sxs-lookup"><span data-stu-id="7be11-108">The pointer to the module.</span></span> |

## <a name="methods"></a><span data-ttu-id="7be11-109">Metody</span><span class="sxs-lookup"><span data-stu-id="7be11-109">Methods</span></span>

| <span data-ttu-id="7be11-110">Metoda</span><span class="sxs-lookup"><span data-stu-id="7be11-110">Method</span></span>                                                                                               | <span data-ttu-id="7be11-111">Opis</span><span class="sxs-lookup"><span data-stu-id="7be11-111">Description</span></span>                                                                    |
| ---------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| [<span data-ttu-id="7be11-112">Żądanie</span><span class="sxs-lookup"><span data-stu-id="7be11-112">Request</span></span>](dacpgetmoduleaddress-request-method.md) | <span data-ttu-id="7be11-113">Wykonuje żądanie wypełnienia struktury z danej struktury środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="7be11-113">Performs a request to populate the structure from the given runtime structure.</span></span> |

## <a name="remarks"></a><span data-ttu-id="7be11-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="7be11-114">Remarks</span></span>

<span data-ttu-id="7be11-115">Ta struktura jest w czasie wykonywania i nie jest udostępniana za pomocą żadnych plików nagłówkowych ani bibliotek.</span><span class="sxs-lookup"><span data-stu-id="7be11-115">This structure lives inside the runtime and is not exposed through any headers or library files.</span></span> <span data-ttu-id="7be11-116">Aby go użyć, Zdefiniuj strukturę jak określono powyżej, gdzie `CLRDATA_ADDRESS` jest 64-bitową liczbą całkowitą bez znaku.</span><span class="sxs-lookup"><span data-stu-id="7be11-116">To use it, define the structure as specified above, where `CLRDATA_ADDRESS` is a 64-bit unsigned integer.</span></span>

## <a name="requirements"></a><span data-ttu-id="7be11-117">Wymagania</span><span class="sxs-lookup"><span data-stu-id="7be11-117">Requirements</span></span>

<span data-ttu-id="7be11-118">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="7be11-118">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
<span data-ttu-id="7be11-119">**Nagłówek:** Dawaj</span><span class="sxs-lookup"><span data-stu-id="7be11-119">**Header:** None</span></span>  
<span data-ttu-id="7be11-120">**Biblioteka:** Dawaj</span><span class="sxs-lookup"><span data-stu-id="7be11-120">**Library:** None</span></span>  
<span data-ttu-id="7be11-121">**.NET Framework wersje:**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]</span><span class="sxs-lookup"><span data-stu-id="7be11-121">**.NET Framework Versions:** [!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]</span></span>  

## <a name="see-also"></a><span data-ttu-id="7be11-122">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="7be11-122">See also</span></span>

- [<span data-ttu-id="7be11-123">Debugowanie</span><span class="sxs-lookup"><span data-stu-id="7be11-123">Debugging</span></span>](index.md)
- [<span data-ttu-id="7be11-124">Struktury debugowania</span><span class="sxs-lookup"><span data-stu-id="7be11-124">Debugging Structures</span></span>](debugging-structures.md)
